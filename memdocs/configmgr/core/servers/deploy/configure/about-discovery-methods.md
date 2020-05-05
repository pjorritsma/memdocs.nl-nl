---
title: Detectie methoden
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare detectie methoden voor het zoeken van apparaten op uw netwerk, van Active Directory of Azure Active Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: af35d5a941d5fd9bde2f87c8fb700b9d85e10b00
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078648"
---
# <a name="about-discovery-methods-for-configuration-manager"></a>Over detectie methoden voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager detectie methoden zoeken verschillende apparaten op uw netwerk, apparaten en gebruikers van Active Directory of gebruikers van Azure Active Directory (Azure AD). Als u een detectie methode efficiënt wilt gebruiken, moet u de beschik bare configuraties en beperkingen begrijpen.  



##  <a name="active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a>Active Directory forest-detectie  
 **Configureerbaar:** Klikt  

 **Standaard ingeschakeld:** Geen  

 **Accounts** die u kunt gebruiken om deze methode uit te voeren:  

-   **Active Directory-forest-detectie account** (door de gebruiker gedefinieerd)  

-   **Computer account** van de site server  

In tegens telling tot andere Active Directory detectie methoden detecteert Active Directory forest Discovery geen resources die u kunt beheren. In plaats daarvan detecteert deze methode netwerk locaties die zijn geconfigureerd in Active Directory. Dit kan deze locaties omzetten in grenzen voor gebruik in de hele hiërarchie.  

Wanneer deze methode wordt uitgevoerd, doorzoekt de lokale Active Directory-forest, elk vertrouwd forest en elk extra forest dat u configureert in het knoop punt **Active Directory forests** van de Configuration Manager-console.  

Active Directory forest-detectie gebruiken om:  

-   Detecteer Active Directory sites en subnetten en maak vervolgens Configuration Manager grenzen op basis van die netwerk locaties.  

-   Identificeer de supernetten die aan een Active Directory-site zijn toegewezen. Converteer elke supernet naar een IP-adres bereik grens.  

-   Publiceren naar Active Directory Domain Services (AD DS) in een forest wanneer het publiceren naar die forest is ingeschakeld. Het opgegeven Active Directory-forest-account moet machtigingen hebben voor het forest.  

U kunt Active Directory forest-detectie beheren in de Configuration Manager-console. Ga naar de werk ruimte **beheer** en vouw **hiërarchie configuratie**uit.   

-   **Detectie methoden**: Schakel Active Directory forest-detectie in om uit te voeren op de site op het hoogste niveau van uw hiërarchie. U kunt ook een eenvoudig schema opgeven om detectie uit te voeren. Configureer deze om automatisch grenzen te maken op basis van de IP-subnetten en Active Directory sites die worden gedetecteerd. Active Directory forest-detectie kan niet worden uitgevoerd op een onderliggende primaire site of op een secundaire site.  

-   **Active Directory forests**: Configureer de extra forests om te detecteren, geef elk Active Directory forest-account op en configureer publicatie naar elk forest. Het detectie proces bewaken. Voeg IP-subnetten en Active Directory-sites toe als Configuration Manager grenzen en leden van grens groepen.  

Als u publiceren voor Active Directory forests wilt configureren voor elke site in uw hiërarchie, verbindt u uw Configuration Manager-console met de site op het hoogste niveau van uw hiërarchie. Op het tabblad **publiceren** in het dialoog venster **eigenschappen** van een Active Directory-site kunnen alleen de huidige site en de onderliggende sites worden weer gegeven. Wanneer publiceren is ingeschakeld voor een forest en het schema van dat forest is uitgebreid voor Configuration Manager, wordt de volgende informatie gepubliceerd voor elke site die is ingeschakeld voor publicatie naar die Active Directory forest:  

-    **SMS-site-&lt;site code>**

-   **SMS-MP-&lt;site code>-&lt;site systeem server naam>**  

-   **SMS-SLP-&lt;site code>-&lt;site systeem server naam>**  

-   **SMS-&lt;site code>-&lt;Active Directory site naam of-subnet>**  

> [!NOTE]  
>  Secundaire sites gebruiken steeds het computeraccount van de secundaire siteserver om naar Active Directory te publiceren. Als u wilt dat secundaire sites naar Active Directory publiceren, moet u ervoor zorgen dat het computer account van de secundaire site server over machtigingen beschikt om naar Active Directory te publiceren. Een secundaire site kan geen gegevens publiceren naar een niet-vertrouwd forest.  

> [!CAUTION]  
>  Wanneer u de optie voor het publiceren van een site naar een Active Directory-forest uitschakelt, wordt alle eerder gepubliceerde informatie voor die site, inclusief de beschik bare site systeem rollen, verwijderd uit Active Directory.  

Acties voor de detectie van Active Directory forests worden vastgelegd in de volgende logboeken:  

-   Alle acties, met uitzonde ring van acties met betrekking tot publiceren, worden vastgelegd in het bestand **ADForestDisc. log** in de ** &lt;map InstallationPath> \logs** op de site server.  

-   Active Directory publicatie acties voor forest-detectie worden vastgelegd in de bestanden **hman. log** en **sitecomp. log** in de ** &lt;map InstallationPath> \logs** op de site server.  

Zie [detectie methoden configureren](configure-discovery-methods.md#BKMK_ConfigADForestDisc)voor meer informatie over het configureren van deze detectie methode.  



##  <a name="active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a>Groeps detectie Active Directory  
**Configureerbaar:** Klikt  

**Standaard ingeschakeld:** Geen  

**Accounts** die u kunt gebruiken om deze methode uit te voeren:  

-   **Active Directory groeps detectie account** (door de gebruiker gedefinieerd)  

-   **Computer account** van de site server  

> [!TIP]  
>  Naast de informatie in deze sectie, Zie [algemene functies van Active Directory groep, systeem en gebruikers detectie](#bkmk_shared).  

Gebruik deze methode om Active Directory Domain Services te zoeken om te identificeren:  

-   Lokale, globale en universele beveiligings groepen.  

-   Het lidmaatschap van groepen.  

-   Beperkte informatie over de lidcomputers en gebruikers van een groep, zelfs wanneer een andere detectie methode deze computers en gebruikers niet eerder heeft gedetecteerd.  

Deze detectie methode is bedoeld om groepen en de groeps relaties van leden van groepen te identificeren. Standaard worden alleen beveiligings groepen gedetecteerd. Als u ook het lidmaatschap van distributie groepen wilt vinden, moet u het selectie vakje voor de optie **het lidmaatschap van distributie groepen detecteren** op het tabblad **optie** in het dialoog venster **eigenschappen van groeps detectie Active Directory** .  

Active Directory groeps detectie biedt geen ondersteuning voor de uitgebreide Active Directory kenmerken die kunnen worden geïdentificeerd met behulp van Active Directory systeem detectie of Active Directory gebruikers detectie. Omdat deze detectie methode niet is geoptimaliseerd om computer-en gebruikers bronnen te detecteren, kunt u overwegen deze detectie methode uit te voeren nadat u Active Directory systeem detectie hebt uitgevoerd en de detectie van Active Directory gebruikers. Deze suggestie is omdat met deze methode een volledige detectie gegevens record (DDR) wordt gemaakt voor groepen, maar alleen een beperkte DDR voor computers en gebruikers die lid zijn van groepen.  

U kunt de volgende detectie bereiken configureren die bepalen hoe deze methode zoekt naar informatie:  

-   **Locatie**: gebruik een locatie als u wilt zoeken in een of meer Active Directory containers. Deze scope optie ondersteunt een recursieve zoek opdracht van de opgegeven Active Directory containers. Dit proces doorzoekt elke onderliggende container onder de door u opgegeven container. Het proces wordt voortgezet totdat er geen onderliggende containers meer worden gevonden.  

-   **Groepen**: gebruik groepen als u wilt zoeken naar een of meer specifieke Active Directory groepen. U kunt **Active Directory-domein** configureren voor het gebruik van het standaard domein en-forest of de zoek opdracht beperken tot een afzonderlijke domein controller. Daarnaast kunt u een of meer groepen opgeven waarnaar u wilt zoeken. Als u niet ten minste één groep opgeeft, worden alle groepen die zijn gevonden op de opgegeven **Active Directory-domein** locatie doorzocht.  

> [!CAUTION]  
>  Wanneer u een detectie bereik configureert, kiest u alleen de groepen die u moet detecteren. Deze aanbeveling is omdat Active Directory groeps detectie elk lid van elke groep in het detectie bereik probeert te detecteren. Voor de detectie van grote groepen kan een uitgebreid gebruik van band breedte en Active Directory resources nodig zijn.  

> [!NOTE]  
>  Voordat u verzamelingen kunt maken die zijn gebaseerd op uitgebreide Active Directory kenmerken en om nauw keurige detectie resultaten voor computers en gebruikers te garanderen, moet u Active Directory systeem detectie of Active Directory gebruikers detectie uitvoeren, afhankelijk van wat u wilt detecteren.  

Acties voor de detectie van Active Directory groepen worden vastgelegd in het bestand **adsgdis. log** in de ** &lt;map InstallationPath\>\LOGS** op de site server.  

Zie [detectie methoden configureren](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral)voor meer informatie over het configureren van deze detectie methode.  



##  <a name="active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a>Systeem detectie Active Directory  
**Configureerbaar:** Klikt  

**Standaard ingeschakeld:** Geen  

**Accounts** die u kunt gebruiken om deze methode uit te voeren:  

-   **Active Directory systeem detectie account** (door de gebruiker gedefinieerd)  

-   **Computer account** van de site server  

> [!TIP]  
>  Naast de informatie in deze sectie, Zie [algemene functies van Active Directory groep, systeem en gebruikers detectie](#bkmk_shared).  

Gebruik deze detectie methode om te zoeken naar de opgegeven Active Directory Domain Services locaties voor computer resources die kunnen worden gebruikt om verzamelingen en query's te maken. U kunt de Configuration Manager-client ook installeren op een gedetecteerd apparaat door gebruik te maken van client push installatie.  

Deze methode detecteert standaard basis informatie over de computer, met inbegrip van de volgende kenmerken:  

-   Computernaam  

-   Besturings systeem en versie  

-   Active Directory container naam  

-   IP-adres  

-   Active Directory-site  

-   Tijds tempel van recentste aanmelding  

Als u een DDR voor een computer wilt maken, moet Active Directory systeem detectie het computer account kunnen identificeren en vervolgens de computer naam kunnen omzetten in een IP-adres.  

U kunt in het dialoog venster **Eigenschappen van Active Directory systeem detectie** op het tabblad **Active Directory kenmerken** de volledige lijst met standaard object kenmerken weer geven die worden gedetecteerd. U kunt ook de methode configureren voor het detecteren van aanvullende (uitgebreide) kenmerken.  

Acties voor Active Directory systeem detectie worden vastgelegd in het bestand **adsysdis. log** in de ** &lt;map\>InstallationPath \LOGS** op de site server.  

Zie [detectie methoden configureren](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral)voor meer informatie over het configureren van deze detectie methode.  



##  <a name="active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a>Gebruikers detectie Active Directory  
**Configureerbaar:** Klikt  

**Standaard ingeschakeld:** Geen  

**Accounts** die u kunt gebruiken om deze methode uit te voeren:  

-   **Active Directory gebruikers detectie account** (door de gebruiker gedefinieerd)  

-   **Computer account** van de site server  

> [!TIP]  
>  Naast de informatie in deze sectie, Zie [algemene functies van Active Directory groep, systeem en gebruikers detectie](#bkmk_shared).  

Gebruik deze detectie methode om Active Directory Domain Services te zoeken om gebruikers accounts en gekoppelde kenmerken te identificeren. Deze methode detecteert standaard basis informatie over het gebruikers account, met inbegrip van de volgende kenmerken:  

-   Gebruikersnaam  

-   Unieke gebruikers naam (inclusief domein naam)  

-   Domain  

-   Active Directory container namen  

U kunt in het dialoog venster **Eigenschappen voor gebruikers detectie Active Directory** op het tabblad **Active Directory kenmerken** de volledige standaard lijst met object kenmerken weer geven die wordt gedetecteerd. U kunt ook de methode configureren voor het detecteren van aanvullende (uitgebreide) kenmerken.

Acties voor de detectie van Active Directory gebruikers worden vastgelegd in het bestand **adusrdis. log** in de ** &lt;map InstallationPath\>\LOGS** op de site server.  

Zie [detectie methoden configureren](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral)voor meer informatie over het configureren van deze detectie methode.  



## <a name="azure-active-directory-user-discovery"></a><a name="azureaddisc"></a>Gebruikers detectie Azure Active Directory

Gebruik Azure Active Directory (Azure AD) gebruikers detectie om uw Azure AD-abonnement te doorzoeken op gebruikers met een moderne Cloud-identiteit. Azure AD-gebruikers detectie kan de volgende kenmerken vinden:

- Id
- displayName
- mail
- mailNickname
- onPremisesSecurityIdentifier
- userPrincipalName
- AAD tenantID
- onPremisesDomainName
- onPremisesSamAccountName
- onPremisesDistinguishedName

Deze methode ondersteunt de volledige en Delta synchronisatie van gebruikers kenmerken vanuit Azure AD. Deze informatie kan vervolgens worden gebruikt voor de detectie gegevens aan de volgende zijde die u van de andere detectie methoden verzamelt.

Acties voor Azure AD-gebruikers detectie worden vastgelegd in het bestand **SMS_AZUREAD_DISCOVERY_AGENT. log** op de site server op het hoogste niveau van de hiërarchie.

Zie [Azure-Services configureren](azure-services-wizard.md) voor Cloud beheer voor meer informatie over het configureren van Azure AD-gebruikers detectie. Zie [Azure AD-gebruikers detectie configureren](configure-discovery-methods.md#azureaadisc)voor meer informatie over het configureren van deze detectie methode.

## <a name="azure-active-directory-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Detectie van gebruikers groepen Azure Active Directory
<!--3611956-->
*(Geïntroduceerd als een [voorlopige functie](../../manage/pre-release-features.md) in versie 1906)*

U kunt gebruikers groepen en leden van deze groepen vinden vanuit Azure Active Directory (Azure AD). De detectie van Azure AD-gebruikers groepen kan de volgende kenmerken vinden:

- Id
- displayName
- mailNickname
- onPremisesSecurityIdentifier
- AAD tenantID

Acties voor de detectie van Azure AD-gebruikers groepen worden vastgelegd in het bestand **SMS_AZUREAD_DISCOVERY_AGENT. log** op de site server op het hoogste niveau van de hiërarchie. Zie [detectie van Azure AD-gebruikers groepen configureren](configure-discovery-methods.md#bkmk_azuregroupdisco)voor meer informatie over het configureren van deze detectie methode.

##  <a name="heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a>Heartbeat-detectie  
**Configureerbaar:** Klikt  

**Standaard ingeschakeld:** Klikt  

**Accounts** die u kunt gebruiken om deze methode uit te voeren:  

-   **Computer account** van de site server  

Heartbeat-detectie wijkt af van andere Configuration Manager detectie methoden. Het is standaard ingeschakeld en wordt uitgevoerd op elke computer client (in plaats van op een site server) om een DDR te maken. Voor mobiele apparaatclients wordt dit DDR gemaakt door het beheer punt dat door de client voor mobiele apparaten wordt gebruikt. Schakel heartbeat-detectie niet uit om de database record van Configuration Manager-clients bij te houden. Naast het onderhouden van de database record kan deze methode de detectie van een computer als een nieuwe bron record afdwingen. Het kan ook de database record van een computer die uit de data base is verwijderd, opnieuw vullen.  

Heartbeat-detectie wordt uitgevoerd volgens een schema dat is geconfigureerd voor alle clients in de hiërarchie. Het standaard schema voor heartbeat-detectie is ingesteld op elke zeven dagen. Als u het heartbeat-detectie-interval wijzigt, moet u ervoor zorgen dat het vaker wordt uitgevoerd dan de onderhouds taak van de site **verouderde detectie gegevens verwijderen**. Met deze taak worden niet-actieve client records uit de site database verwijderd. U kunt de taak **verouderde detectie gegevens verwijderen** alleen configureren voor primaire sites. 

U kunt ook hand matig heartbeat-detectie op een specifieke client aanroepen. Voer de **Verzamel fase detectie gegevens** uit op het tabblad **actie** van het configuratie scherm van een Configuration Manager client.  

Wanneer heartbeat-detectie wordt uitgevoerd, maakt het een DDR met de huidige informatie van de client. De client kopieert dit kleine bestand (ongeveer 1 KB) naar een beheer punt zodat een primaire site het kan verwerken. Het bestand bevat de volgende informatie:  

-   Netwerk locatie  

-   NetBIOS-naam  

-   Versie van de client agent  

-   Details van operationele status  

Heartbeat-detectie is de enige detectie methode die informatie geeft over de installatie status van de client. Dit doet u door het client kenmerk systeem bron bij te werken om een waarde in te stellen die gelijk is aan **Ja**.  

> [!NOTE]  
>  Zelfs als heartbeat-detectie is uitgeschakeld, worden er nog steeds Ddr's gemaakt en verzonden voor actieve clients voor mobiele apparaten. Dit gedrag zorgt ervoor dat de taak voor het **verwijderen van verouderde detectie gegevens** geen invloed heeft op actieve mobiele apparaten. Wanneer de taak **verouderde detectie gegevens verwijderen** een database record voor een mobiel apparaat verwijdert, wordt het certificaat van het apparaat ook ingetrokken. Met deze actie wordt het mobiele apparaat geblokkeerd om verbinding te maken met beheer punten.  

Acties voor heartbeat-detectie worden op de volgende locaties vastgelegd:  

-   Voor computer clients worden heartbeat-detectie acties op de client vastgelegd in het bestand **InventoryAgent. log** in de map *%windir%\CCM\Logs* .  

-   Voor mobiele apparaatclients worden acties voor heartbeat-detectie vastgelegd in het bestand **DMPRP. log** in de map *% Program Files%\CCM\Logs* van het beheer punt dat door de client voor mobiele apparaten wordt gebruikt.  

Zie [detectie methoden configureren](configure-discovery-methods.md#BKMK_ConfigHBDisc)voor meer informatie over het configureren van deze detectie methode.  



##  <a name="network-discovery"></a><a name="bkmk_aboutNetwork"></a>Netwerk detectie  
**Configureerbaar:** Klikt  

**Standaard ingeschakeld:** Geen  

**Accounts** die u kunt gebruiken om deze methode uit te voeren:  

-   **Computer account** van de site server  

Gebruik deze methode om de topologie van uw netwerk te detecteren en apparaten op uw netwerk te detecteren die een IP-adres hebben. Netwerk detectie doorzoekt uw netwerk op IP-bronnen door query's uit te scha kelen op de volgende entiteiten: 
- Servers waarop een micro soft-implementatie van DHCP wordt uitgevoerd
- ARP-caches (Address Resolution Protocol) in netwerk routers
- Apparaten met SNMP
- Active Directory domeinen  

Voordat u netwerk detectie kunt gebruiken, moet u het *niveau* van detectie opgeven dat moet worden uitgevoerd. U kunt ook een of meer detectie mechanismen configureren om netwerk detectie in te scha kelen voor netwerk segmenten of apparaten. U kunt ook instellingen configureren waarmee detectie acties op het netwerk worden beheerd. Ten slotte definieert u een of meer schema's voor wanneer netwerk detectie wordt uitgevoerd.  

Voor deze methode om een resource te detecteren, moet netwerk detectie het IP-adres en het subnetmasker van de bron identificeren. De volgende methoden worden gebruikt om het subnetmasker van een object te identificeren:  

-   **ARP-cache van de router:** Netwerk detectie voert een query uit op de ARP-cache van een router om subnetgegevens te vinden. Gegevens in een router ARP-cache hebben doorgaans een korte time-to-Live. Daarom is het mogelijk dat de ARP-cache geen informatie over het aangevraagde object meer bevat wanneer netwerk detectie de ARP-cache doorzoekt.  

-   **DHCP:** Netwerk detectie doorzoekt elke DHCP-server die u opgeeft om de apparaten te detecteren waarvoor de DHCP-server een lease heeft opgegeven. Netwerk detectie ondersteunt alleen DHCP-servers waarop de micro soft-implementatie van DHCP wordt uitgevoerd.  

-   **SNMP-apparaat:** Netwerk detectie kan rechtstreeks een query uitvoeren op een SNMP-apparaat. Voor netwerk detectie om een apparaat op te vragen, moet op het apparaat een lokale SNMP-agent zijn geïnstalleerd. Configureer ook netwerk detectie om de community-naam te gebruiken die door de SNMP-agent wordt gebruikt.  

Wanneer detectie een IP-adresseerbaar object identificeert en het subnetmasker van het object kan bepalen, maakt het een DDR voor dat object. Omdat verschillende typen apparaten verbinding maken met het netwerk, detecteert netwerk detectie resources die de Configuration Manager-client niet ondersteunen. Apparaten die kunnen worden gedetecteerd, maar niet worden beheerd, zijn bijvoorbeeld printers en routers.  

Netwerk detectie kan verschillende kenmerken retour neren als onderdeel van de detectie record die het maakt. Deze kenmerken zijn onder andere:  

-   NetBIOS-naam  

-   IP-adressen  

-   Bron domein  

-   Systeem rollen  

-   SNMP-communitynaam  

-   MAC-adressen  

De activiteit netwerk detectie wordt vastgelegd in het bestand **netdisc. log** in * &lt;\>InstallationPath \Logs* op de site server die detectie uitvoert.  

 Zie [detectie methoden configureren](configure-discovery-methods.md#BKMK_ConfigNetworkDisc)voor meer informatie over het configureren van deze detectie methode.  

> [!NOTE]  
>  Complexe netwerken en verbindingen met een lage band breedte kunnen ertoe leiden dat netwerk detectie langzaam wordt uitgevoerd en aanzienlijke netwerk verkeer kan genereren. Voer netwerk detectie als best practice alleen uit wanneer de andere detectie methoden de bronnen die u moet detecteren, niet kunnen vinden. Gebruik bijvoorbeeld netwerk detectie als u werkgroepcomputers moet detecteren. Andere detectie methoden detecteren geen werkgroepcomputers.  

###  <a name="levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a>Niveaus van netwerk detectie  
Wanneer u netwerk detectie configureert, kunt u een van de drie detectie niveaus opgeven:  

|Niveau van detectie|Details|  
|------------------------|-------------|  
|Topologie|Op dit niveau worden routers en subnetten gedetecteerd, maar wordt geen subnetmasker voor objecten geïdentificeerd.|  
|Topologie en client|Naast topologie detecteert dit niveau potentiële clients, zoals computers en bronnen als printers en routers. Dit detectie niveau probeert het subnetmasker te identificeren van de objecten die worden gevonden.|  
|Topologie, client en besturings systeem van de client|Naast topologie en mogelijke clients probeert dit niveau de naam en versie van het besturings systeem van de computer te detecteren. Op dit niveau worden Windows-browser-en Windows-netwerk aanroepen gebruikt.|  

 Bij elk incrementeel niveau verhoogt netwerk detectie de activiteiten en het gebruik van de netwerk bandbreedte. Denk na over het netwerk verkeer dat kan worden gegenereerd voordat u alle aspecten van netwerk detectie inschakelt.  

 Wanneer u bijvoorbeeld netwerk detectie voor het eerst gebruikt, kunt u beginnen met alleen het topologie niveau om uw netwerk infrastructuur te identificeren. Configureer netwerk detectie vervolgens opnieuw om objecten en hun besturings systemen van apparaten te detecteren. U kunt ook instellingen configureren die netwerk detectie beperken tot een specifiek bereik van netwerk segmenten. Op die manier detecteert u objecten in netwerk locaties die u nodig hebt en vermijdt u onnodig netwerk verkeer. Met dit proces kunt u ook objecten van Edge-routers of van buiten uw netwerk detecteren.  

###  <a name="network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a>Opties voor netwerk detectie  
Configureer een of meer van deze opties om netwerk detectie in te scha kelen om te zoeken naar IP-adresseer bare apparaten.  

> [!NOTE]  
>  Netwerk detectie wordt uitgevoerd in de context van het computer account van de site server die detectie uitvoert. Als het computer account geen machtigingen heeft voor een niet-vertrouwd domein, kunnen de configuraties van het domein en de DHCP-server geen bronnen detecteren.  

#### <a name="dhcp"></a>DHCP  

Geef elke DHCP-server op die u wilt laten doorzoeken door netwerk detectie. (Netwerk detectie ondersteunt alleen DHCP-servers waarop de micro soft-implementatie van DHCP wordt uitgevoerd.)  

-   Netwerk detectie haalt gegevens op met behulp van externe procedure aanroepen naar de Data Base op de DHCP-server.  

-   Netwerk detectie kan voor een lijst met apparaten die zijn geregistreerd bij elke server een query uitvoeren op zowel 32-bits als 64-bits DHCP-servers.  

-   Voor netwerk detectie om een DHCP-server te doorzoeken, moet het computer account van de server die detectie uitvoert, lid zijn van de groep DHCP-gebruikers op de DHCP-server. Dit toegangs niveau bestaat bijvoorbeeld wanneer een van de volgende-instructies waar is:  

    -   De opgegeven DHCP-server is de DHCP-server van de server die detectie uitvoert.  

    -   De computer die detectie uitvoert en de DHCP-server bevinden zich in hetzelfde domein.  

    -   Er bestaat een twee richtings vertrouwensrelatie tussen de computer die detectie uitvoert en de DHCP-server.  

    -   De site server is lid van de groep DHCP-gebruikers.  

-   Wanneer netwerk detectie een DHCP-server inventariseert, detecteert deze niet altijd vaste IP-adressen. Netwerk detectie kan geen IP-adressen vinden die deel uitmaken van een uitgesloten bereik van IP-adressen op de DHCP-server. Er worden ook geen IP-adressen gedetecteerd die zijn gereserveerd voor hand matige toewijzing.  

#### <a name="domains"></a>Domeinen  

Geef elk domein op dat u door netwerk detectie wilt laten doorzoeken.  

-   Het computer account van de site server die detectie uitvoert, moet machtigingen hebben om de domein controllers in elk opgegeven domein te lezen.  

-   Als u computers van het lokale domein wilt detecteren, moet u de computer browser-service op ten minste één computer inschakelen. Deze computer moet zich in hetzelfde subnet bevinden als de site server waarop netwerk detectie wordt uitgevoerd.  

-   Netwerk detectie kan elke computer detecteren die u vanaf de site server kunt weer geven wanneer u door het netwerk bladert.  

-   Netwerk detectie haalt het IP-adres op. Vervolgens wordt een Internet Control Message Protocol (ICMP) Echo-aanvraag gebruikt voor het pingen van elk apparaat dat wordt gevonden. De **ping** -opdracht helpt te bepalen welke computers momenteel actief zijn.  

#### <a name="snmp-devices"></a>SNMP-apparaten  

Geef elk SNMP-apparaat op dat door netwerk detectie moet worden opgevraagd.  

-   Netwerk detectie haalt de ipNetToMediaTable-waarde op van een SNMP-apparaat dat reageert op de query. Deze waarde retourneert matrices van IP-adressen die client computers of andere bronnen zijn, zoals printers, routers of andere IP-adresseer bare apparaten.  

-   Als u een query wilt uitvoeren op een apparaat, moet u het IP-adres of de NetBIOS-naam van het apparaat opgeven.  

-   Configureer netwerk detectie om de community-naam van het apparaat te gebruiken, of het apparaat weigert de op SNMP gebaseerde query.  


###  <a name="limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a>Netwerk detectie beperken  
Wanneer netwerk detectie een SNMP-apparaat aan de rand van uw netwerk doorzoekt, kan dit informatie identificeren over subnetten en SNMP-apparaten buiten uw directe netwerk. Gebruik de volgende informatie om netwerk detectie te beperken door de SNMP-apparaten te configureren waarmee detectie kan communiceren en door de netwerk segmenten op te geven die u wilt doorzoeken.  

#### <a name="subnets"></a>Subnetten  

Configureer de subnetten die netwerk detectie query's uitvoert wanneer het de SNMP-en DHCP-opties gebruikt. Deze twee opties doorzoeken alleen de ingeschakelde subnetten.  

Een DHCP-aanvraag kan bijvoorbeeld apparaten retour neren van locaties in uw hele netwerk. Als u alleen apparaten op een specifiek subnet wilt detecteren, moet u dat specifieke subnet opgeven en inschakelen op het tabblad **subnetten** in het dialoog venster **Eigenschappen van netwerk detectie** . Wanneer u subnetten opgeeft en inschakelt, kunt u toekomstige DHCP-en SNMP-detectie taken beperken tot deze subnetten.  

> [!NOTE]  
>  Subnet-configuraties beperken de objecten die de optie voor de detectie van **domeinen** detecteert niet.  

#### <a name="snmp-community-names"></a>SNMP-communitynamen  

Configureer netwerk detectie met de community-naam van het apparaat om netwerk detectie in te scha kelen voor het uitvoeren van een query op een SNMP-apparaat. Als netwerk detectie niet is geconfigureerd met behulp van de community-naam van het SNMP-apparaat, wordt de query geweigerd door het apparaat.  

#### <a name="maximum-hops"></a>Maximum aantal hops  

Wanneer u het maximum aantal router-hops configureert, beperkt u het aantal netwerk segmenten en routers dat door netwerk detectie kan worden opgevraagd met behulp van SNMP.  

Het aantal hops dat u configureert, beperkt het aantal extra apparaten en netwerk segmenten dat door netwerk detectie kan worden opgevraagd.  

Bijvoorbeeld: een detectie met alleen topologie met **0** (nul) router-hops detecteert het subnet waarop de oorspronkelijke server zich bevindt. Het bevat alle routers in dat subnet.  

In het volgende diagram ziet u wat een topologie netwerk detectie query vindt wanneer deze wordt uitgevoerd op Server 1 met 0 router-hops opgegeven: subnet D en router 1.  

 ![Afbeelding van detectie met nul router sprong](media/Disc-0.gif)  

 In het volgende diagram ziet u wat een topologie en client netwerk detectie query vindt wanneer deze wordt uitgevoerd op Server 1 met 0 router-hops opgegeven: subnet D en router 1, en alle potentiële clients op subnet D.  

 ![Afbeelding van detectie met één router sprong](media/Disc-1.gif)  

 Houd rekening met het volgende netwerk om een beter beeld te krijgen van hoe extra router-hops de hoeveelheid gedetecteerde netwerk bronnen kan verg Roten:  

 ![Afbeelding van detectie met twee router sprongen](media/Disc-2.gif)  

 Als u een alleen-topologie netwerk detectie uitvoert vanaf server 1 met één router-hop, worden de volgende entiteiten gedetecteerd:  

-   Router 1 en subnet 10.1.10.0 (gevonden met een hops van nul)  

-   Subnetten 10.1.20.0 en 10.1.30.0, subnet A en router 2 (gevonden op de eerste hop)  

> [!WARNING]  
>  Elke toename van het aantal router-hops kan het aantal Detecteer bare bronnen aanzienlijk verhogen en de netwerk bandbreedte verg Roten die netwerk detectie gebruikt.  



##  <a name="server-discovery"></a><a name="bkmk_aboutServer"></a>Server detectie  
**Configureerbaar:** Geen  

Naast de door de gebruiker Configureer bare detectie methoden gebruikt Configuration Manager een proces met de naam **Server detectie** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Deze detectie methode maakt bron records voor computers die site systemen zijn, zoals een computer die is geconfigureerd als een beheer punt.  



##  <a name="common-features-of-active-directory-group-discovery-system-discovery-and-user-discovery"></a><a name="bkmk_shared"></a>Algemene functies van Active Directory groeps detectie, systeem detectie en detectie van gebruikers  
Deze sectie bevat informatie over functies die gemeen schappelijk zijn voor de volgende detectie methoden:  

-   Active Directory-groepdetectie  

-   Active Directory-systeemdetectie  

-   Detectie Active Directory-gebruiker  

> [!NOTE]  
>  De informatie in deze sectie is niet van toepassing op Active Directory forest-detectie.  

Deze drie detectie methoden zijn vergelijkbaar in configuratie en werking. Ze kunnen computers, gebruikers en informatie ontdekken over groepslid maatschappen van resources die zijn opgeslagen in Active Directory Domain Services. Het detectie proces wordt beheerd door een detectie agent. De agent wordt uitgevoerd op de site server op elke site waar detectie is geconfigureerd om te worden uitgevoerd. U kunt elk van deze detectie methoden configureren om een of meer Active Directory locaties te doorzoeken als locatie-exemplaren in het lokale forest of externe forests.  

Wanneer detectie zoekt naar een niet-vertrouwd forest voor bronnen, moet de detectie agent het volgende kunnen omzetten om succesvol te zijn:  

-   Als u een computer bron wilt detecteren met behulp van Active Directory systeem detectie, moet de detectie agent de FQDN-naam van de bron kunnen omzetten. Als de FQDN niet kan worden omgezet, wordt geprobeerd om de bron op te lossen met de NetBIOS-naam.  

-   Om een gebruikers-of groeps bron te detecteren met behulp van Active Directory gebruikers detectie of Active Directory groeps detectie, moet de detectie agent de FQDN kunnen omzetten van de domein controller naam die u opgeeft voor de locatie van de Active Directory.  

Voor elke locatie die u opgeeft, kunt u afzonderlijke Zoek opties configureren, zoals het inschakelen van een recursieve zoek opdracht van de Active Directory onderliggende containers van de locatie. U kunt ook een uniek account configureren dat moet worden gebruikt bij het zoeken naar die locatie. Dit account biedt flexibiliteit bij het configureren van een detectie methode op één site om meerdere Active Directory locaties in meerdere forests te doorzoeken. U hoeft geen enkel account te configureren dat machtigingen heeft voor alle locaties.  

Wanneer elk van deze drie detectie methoden op een specifieke site wordt uitgevoerd, neemt de Configuration Manager site server op die site contact op met de dichtstbijzijnde domein controller in het opgegeven Active Directory forest om Active Directory resources te zoeken. Het domein en het forest kunnen in elke ondersteunde Active Directory modus worden uitgevoerd. Het account dat u toewijst aan elk locatie-exemplaar moet **Lees** toegang hebben tot de opgegeven Active Directory locaties.

Detectie zoekt naar de opgegeven locaties voor objecten en probeert vervolgens informatie over die objecten te verzamelen. Er wordt een DDR gemaakt wanneer voldoende informatie over een bron kan worden geïdentificeerd. De vereiste informatie is afhankelijk van de detectie methode die wordt gebruikt.  

Als u dezelfde detectie methode configureert om te worden uitgevoerd op verschillende Configuration Manager sites om te profiteren van het uitvoeren van query's op lokale Active Directory servers, kunt u elke site configureren met een unieke set detectie opties. Omdat detectie gegevens worden gedeeld met elke site in de hiërarchie, moet u overlap tussen deze configuraties voor komen dat elke resource één keer efficiënt wordt gedetecteerd.

Voor kleinere omgevingen kunt u overwegen om elke detectie methode uit te voeren op slechts één site in uw hiërarchie. Deze configuratie vermindert de administratieve overhead en de kans dat meerdere detectie acties dezelfde bronnen opnieuw kunnen detecteren. Wanneer u het aantal sites dat detectie uitvoert minimaliseert, vermindert u de totale netwerk bandbreedte die detectie gebruikt. U kunt ook het totale aantal gegenereerde Ddr's verminderen dat door uw site servers moet worden verwerkt.  

Veel van de configuratie van de detectie methode zijn zelf uitleg. Gebruik de volgende secties voor meer informatie over de detectie opties die mogelijk aanvullende informatie vereisen voordat u ze configureert.  

De volgende opties zijn beschikbaar voor gebruik met meerdere Active Directory detectie methoden:  

-   [Detectie van verschillen](#bkmk_delta)  

-   [Verlopen computer records filteren op domein aanmelding](#bkmk_stalelogon)  

-   [Verlopen records filteren op computer wachtwoord](#bkmk_stalepassword)  

-   [Aangepaste kenmerken van Active Directory zoeken](#bkmk_customAD)  


###  <a name="delta-discovery"></a><a name="bkmk_delta"></a>Detectie van verschillen  
Beschikbaar voor:  

-   Active Directory-groepdetectie  

-   Active Directory-systeemdetectie  

-   Detectie Active Directory-gebruiker  

Detectie van verschillen is geen onafhankelijke detectie methode, maar een optie die beschikbaar is voor de toepasselijke detectie methoden. Delta detectie zoekt naar specifieke Active Directory kenmerken voor wijzigingen die zijn aangebracht sinds de laatste volledige detectie cyclus van de toepasselijke detectie methode. De kenmerk wijzigingen worden naar de Configuration Manager-Data Base verzonden om de detectie record van de bron bij te werken.  

Detectie van verschillen wordt standaard uitgevoerd op een cyclus van vijf minuten. Dit schema is veel vaker dan het gebruikelijke schema voor een volledige detectie cyclus. Deze frequente cyclus is mogelijk omdat Delta detectie minder site server-en netwerk bronnen gebruikt dan een volledige detectie cyclus. Wanneer u Delta detectie gebruikt, kunt u de frequentie van de volledige detectie cyclus voor die detectie methode verlagen.  

Hier volgen de meest voorkomende wijzigingen die detectie van verschillen detecteert:  

-   Nieuwe computers of gebruikers die zijn toegevoegd aan Active Directory  

-   Wijzigingen in basis computer-en gebruikers gegevens  

-   Nieuwe computers of gebruikers die zijn toegevoegd aan een groep  

-   Computers of gebruikers die zijn verwijderd uit een groep  

-   Wijzigingen in systeem groeps objecten  

Hoewel de detectie van verschillen nieuwe bronnen en wijzigingen in groepslid maatschappen kan detecteren, kan niet worden gedetecteerd wanneer een bron is verwijderd uit Active Directory. Ddr's die zijn gemaakt door de detectie van verschillen, worden verwerkt op dezelfde manier als de Ddr's die worden gemaakt door een volledige detectie cyclus.  

U configureert de detectie van verschillen op het tabblad **polling schema** in de eigenschappen voor elke detectie methode.  


###  <a name="filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a>Verlopen computer records filteren op domein aanmelding  
Beschikbaar voor:  

-   Active Directory-groepdetectie  

-   Active Directory-systeemdetectie  

U kunt detectie configureren om computers met een verouderde computer record uit te sluiten. Deze uitsluiting is gebaseerd op de laatste aanmelding bij het domein van de computer. Wanneer deze optie is ingeschakeld, wordt door Active Directory-systeem detectie elke computer geëvalueerd die wordt geïdentificeerd. Active Directory groeps detectie evalueert elke computer die lid is van een groep die wordt gedetecteerd.  

Als u deze optie wilt gebruiken:  

-   Computers moeten worden geconfigureerd om het kenmerk **lastLogonTimeStamp** bij te werken in Active Directory Domain Services.  

-   Het functionele domein niveau van Active Directory moet worden ingesteld op Windows Server 2003 of hoger.  

Wanneer u de tijd configureert na de laatste aanmelding die u voor deze instelling wilt gebruiken, moet u rekening houden met het interval voor replicatie tussen domein controllers.  

U configureert filtering op het tabblad **optie** in de dialoog vensters **Active Directory systeem detectie-eigenschappen** en **Active Directory groeps detectie-eigenschappen** . Kies **alleen computers detecteren die zijn aangemeld bij een domein in een bepaalde periode**.  

> [!WARNING]  
>  Wanneer u dit filter configureert en **verouderde records filtert op computer wachtwoord**, sluit detectie computers uit die voldoen aan de criteria van een filter.  


###  <a name="filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a>Verlopen records filteren op computer wachtwoord  
Beschikbaar voor:  

-   Active Directory-groepdetectie  

-   Active Directory-systeemdetectie  

U kunt detectie configureren om computers met een verouderde computer record uit te sluiten. Deze uitsluiting is gebaseerd op het wacht woord van de laatste computer account dat door de computer wordt bijgewerkt. Wanneer deze optie is ingeschakeld, wordt door Active Directory-systeem detectie elke computer geëvalueerd die wordt geïdentificeerd. Active Directory groeps detectie evalueert elke computer die lid is van een groep die wordt gedetecteerd.  

Als u deze optie wilt gebruiken:  

-   Computers moeten worden geconfigureerd om het kenmerk **pwdLastSet** bij te werken in Active Directory Domain Services.  

Wanneer u deze optie configureert, moet u rekening houden met het interval voor updates van dit kenmerk. Houd ook rekening met het replicatie-interval tussen domein controllers.  

U configureert filtering op het tabblad **optie** in de dialoog vensters **Active Directory systeem detectie-eigenschappen** en **Active Directory groeps detectie-eigenschappen** . U kunt **alleen computers detecteren die het wacht woord van hun computer account hebben bijgewerkt in een bepaalde periode**.  

> [!WARNING]  
>  Wanneer u dit filter configureert en **verouderde records filtert op domein aanmelding**, sluit detectie computers uit die voldoen aan de criteria van een filter.  


###  <a name="search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a>Aangepaste kenmerken van Active Directory zoeken  
 Beschikbaar voor:  

-   Active Directory-systeemdetectie  

-   Detectie Active Directory-gebruiker  

Elke detectie methode ondersteunt een unieke lijst met Active Directory kenmerken die kunnen worden gedetecteerd.  

U kunt de lijst met aangepaste kenmerken weer geven en configureren op het tabblad **kenmerken van Active Directory** in de **Active Directory eigenschappen van systeem detectie** en Active Directory dialoog vensters **Eigenschappen voor gebruikers detectie** .  

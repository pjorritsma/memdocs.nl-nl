---
title: Vereisten voor Windows-client implementatie
titleSuffix: Configuration Manager
description: Meer informatie over de vereisten voor het implementeren van de Configuration Manager-client op Windows-computers.
ms.date: 06/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2aa375d0521e6088904ebe9a1f10af83f4bc261f
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428557"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Vereisten voor het implementeren van clients op Windows-computers in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het implementeren van Configuration Manager-clients in uw omgeving heeft de volgende externe afhankelijkheden en afhankelijkheden binnen het product. Bovendien, heeft elke client-implementatiemethode zijn eigen afhankelijkheden waaraan moet worden voldaan opdat de clientinstallaties succesvol zouden zijn.  

Zie [ondersteunde configuraties](../../plan-design/configs/supported-configurations.md)voor meer informatie over de minimale hardware-en besturingssysteem vereisten voor de Configuration Manager-client.  

> [!NOTE]  
> De in dit artikel vermelde softwareversienummers zijn alleen de minimaal vereiste versienummers.  

## <a name="prerequisites-for-windows-clients"></a><a name="BKMK_prereqs_computers"></a>Vereisten voor Windows-clients  

Gebruik de volgende informatie om de vereisten te bepalen voor wanneer u de Configuration Manager-client op Windows-apparaten installeert.  

### <a name="dependencies-external-to-configuration-manager"></a>Afhankelijkheden extern aan Configuration Manager

Veel van deze onderdelen zijn services of functies die standaard door Windows worden ingeschakeld. Schakel deze onderdelen niet uit op Configuration Manager-clients.

|Onderdeel|Beschrijving|
|---|---|
|Windows Installer|Vereist ter ondersteuning van het gebruik van Windows Installer bestanden voor toepassingen en software-updates.|
|Micro soft Background Intelligent Transfer Service (BITS)|Vereist om beperkte gegevens overdracht tussen de client computer en Configuration Manager site systemen toe te staan.|
|Microsoft Task Scheduler|Vereist voor client bewerkingen, zoals het regel matig evalueren van de status van de Configuration Manager client.|
|Microsoft Remote Differential Compression (RDC)|Vereist om gegevensoverdracht te optimaliseren via het netwerk.|
|SHA-2-ondersteuning voor ondertekening van programma code|Vanaf versie 1906 vereisen clients ondersteuning voor het algoritme voor het ondertekenen van de SHA-2-code. Zie [ondersteuning voor SHA-2-code ondertekening](#bkmk_sha2)voor meer informatie.|

#### <a name="sha-2-code-signing-support"></a><a name="bkmk_sha2"></a>SHA-2-ondersteuning voor ondertekening van programma code

<!--SCCMDocs-pr#3404-->
Vanwege de nadelen van het algoritme SHA-1 en om af te stemmen op industrie standaarden, wordt micro soft nu alleen gebruikgemaakt van Configuration Manager binaire bestanden met het algoritme voor meer beveiliging SHA-2. Oudere versies van Windows-besturings systemen vereisen een update voor de ondersteuning van SHA-2-code ondertekening. Zie voor meer informatie [2019 SHA-2-ondersteuning voor het ondertekenen van code voor Windows en WSUS](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus).

Als u deze versies van het besturings systeem niet bijwerkt, kunt u de Configuration Manager-client versie 1906 niet installeren. Dit gedrag is van toepassing op een nieuwe client installatie of bij het bijwerken van een eerdere versie.

Als u een-client wilt beheren in een versie van Windows die niet is bijgewerkt, of ouder is dan de hierboven vermelde versies, gebruikt u de Configuration Manager Extended samenwerkings client (EIC) versie 1902. Zie [Extended interoperabiliteit client](../../understand/interoperability-client.md)voor meer informatie.

> [!Tip]  
> Als u geen [automatische client update](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)gebruikt en clients met een ander mechanisme bijwerkt, moet u ervoor zorgen dat u de versie van ccmsetup bijwerkt. Een oudere versie van ccmsetup valideert het nieuwe SHA-2-handtekening certificaat niet correct op de binaire bestanden van de versie 1906-client. Bijvoorbeeld, als u ccmsetup. exe kopieert naar een bestands share of gebruikmaakt van ccmsetup. MSI met groeps beleid.<!-- 4963362 -->
>
> De volgende client update mechanismen mogen niet worden beïnvloed:
>
> - Push-client installatie: maakt gebruik van het client pakket van de site
> - Installatie op basis van software-updates: de site-update publiceert opnieuw naar WSUS
> - Door intune MDM beheerde Windows-apparaten: de ondersteunde versie voor dit mechanisme ondersteunt al SHA-2-ondertekening, maar het is nog steeds belang rijk dat u de meest recente ccmsetup. msi gebruikt

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a><a name="bkmk_ExternalDependencies"></a>Afhankelijkheden extern op Configuration Manager en automatisch gedownload tijdens de installatie  

De Configuration Manager-client heeft externe afhankelijkheden. Deze afhankelijkheden zijn afhankelijk van de versie van het besturings systeem en de geïnstalleerde software op de client computer.  

Als de client deze afhankelijkheden vereist om de installatie te volt ooien, worden ze automatisch geïnstalleerd.

|Onderdeel|Beschrijving|
|---|---|
|Micro soft Core XML Services (MSXML) versie 6.20.5002 of hoger ( `msxml6.msi` )|Vereist voor ondersteuning voor de verwerking van XML-documenten in Windows.|
|Micro soft Visual C++ 2013 Redistributable versie 12.0.40660.0 ( `vcredist_x*.exe` )|Vereist ter ondersteuning van clientbewerkingen. Wanneer u deze update op client computers installeert, is het mogelijk dat de computer opnieuw moet worden opgestart om de installatie te volt ooien.|<!-- SCCMDocs#1526 -->
|Windows Imaging Api's 6.0.6001.18000 of hoger ( `wimgapi.msi` )|Vereist om Configuration Manager toe te staan Windows-installatie kopie bestanden (. Wim) te beheren.|
|Microsoft-beleidsplatform 1.2.3514.0 of hoger ( `MicrosoftPolicyPlatformSetup.msi` )|Vereist om clients toe te staan voor de evaluatie van de instellingen voor naleving.|  
|Microsoft .NET Framework versie 4.5.2 of hoger ( `NDP452-KB2901907-x86-x64-AllOS-ENU.exe` )|Vereist ter ondersteuning van clientbewerkingen. Automatisch geïnstalleerd op de client computer als Microsoft .NET Framework versie 4,5 of hoger niet is geïnstalleerd. Voor meer informatie, zie [Aanvullende informatie over Microsoft .NET Framework versie 4.5.2](#dotNet).|  
|Microsoft SQL Server Compact 4,0 SP1-onderdelen|Vereist voor het opslaan van informatie met betrekking tot clientbewerkingen.|  

> [!Important]
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  
>
> Als u nog steeds de Application catalog-website gebruikers ervaring gebruikt, is voor de client micro soft Silverlight 5.1.41212.0 vereist. Silverlight wordt niet automatisch geïnstalleerd door de client. De primaire functionaliteit van de toepassings catalogus is nu opgenomen in Software Center.<!--1356195-->

#### <a name="additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a>Aanvullende informatie over Microsoft .NET Framework versie 4.5.2  

> [!NOTE]  
> .NET 4,0, 4,5 en 4.5.1 worden niet meer ondersteund. Zie de [Veelgestelde vragen over het Microsoft .NET Framework Support Lifecycle-beleid](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)voor meer informatie.  

Microsoft .NET Framework versie 4.5.2 moet mogelijk opnieuw worden opgestart om de installatie te volt ooien. De gebruiker ziet een melding dat de **computer opnieuw** moet worden opgestart in het systeemvak. De volgende algemene scenario's vereisen dat client computers opnieuw worden opgestart:  

- .NET-toepassingen of -services worden op de computer uitgevoerd.  

- Er ontbreken een of meer software-updates die voor de installatie van .NET vereist zijn.  

- Het opnieuw opstarten van de computer is in behandeling voor een eerdere installatie van software-updates voor .NET Framework.  

Nadat .NET Framework 4.5.2 is geïnstalleerd, zijn mogelijk aanvullende updates vereist. Voor deze latere updates moet mogelijk extra computer opnieuw worden opgestart.  

### <a name="configuration-manager-dependencies"></a>Configuration Manager-afhankelijkheden  

Zie [de site systeem rollen voor clients bepalen](plan/determine-the-site-system-roles-for-clients.md)voor meer informatie.  

|Onderdeel|Beschrijving|  
|---|---|  
|Beheerpunt|Als u de Configuration Manager-client wilt implementeren, hebt u geen beheer punt nodig. Clients hebben een beheer punt nodig om informatie over te dragen met de-site. Zonder een beheer punt kunt u geen client computers beheren.|  
|Distributiepunt|Het distributie punt is een optionele, maar aanbevolen site systeemrol voor client implementatie en-beheer. Alle distributie punten hosten de client bron bestanden. Clients vinden het dichtstbijzijnde distributie punt van waaruit de bron bestanden moeten worden gedownload tijdens de implementatie of update van de client. Als de site geen distributie punt heeft, downloaden de computers de bron bestanden van de client van hun beheer punt.|  
|Terugvalstatuspunt|Het terugvalstatuspunt is een optioneel, maar aanbevolen sitesysteemrol voor clientimplementatie. Het terugval status punt traceert client implementatie en schakelt computers in de Configuration Manager-site in staat om status berichten te verzenden wanneer ze niet kunnen communiceren met een beheer punt.|  
|Reporting Services-punt|Het Reporting Services-punt is een optionele, maar aanbevolen site systeemrol. Het geeft rapporten weer die betrekking hebben op client implementatie en-beheer. Zie [Introduction to Reporting](../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.|  

### <a name="installation-method-dependencies"></a>Afhankelijkheden van installatie methoden  

De volgende vereisten zijn specifiek voor de verschillende methodes van clientinstallatie.  

#### <a name="client-push-installation"></a>Clientpushinstallatie  

- De site gebruikt accounts voor push-installatie van de client om verbinding te maken met computers om de client te installeren. Geef deze accounts op op het tabblad **accounts** van de eigenschappen van de Push-client installatie. Het account moet lid zijn van de lokale groep Administrators op de doel computer.  

    Als u geen account voor push-installatie van de client opgeeft, wordt het computer account van de site server gebruikt.  

- De site moet de computer detecteren waarop u de-client installeert. Er is ten minste één Configuration Manager detectie methode vereist.  

- De computer heeft een ADMIN$-share.  

- Als u de Configuration Manager-client automatisch naar gedetecteerde bronnen wilt pushen, selecteert u de optie voor het **inschakelen van client push installatie naar toegewezen bronnen** in de client push installatie-eigenschappen.  

- De client computer moet communiceren met een distributie punt of een beheer punt om de bron bestanden te downloaden.  

- Wanneer u wederzijdse Kerberos-verificatie nodig hebt, moeten clients zich in een vertrouwde Active Directory-forest bevinden. Kerberos in Windows is afhankelijk van Active Directory voor wederzijdse verificatie.<!--1358204-->  

Als u client-push wilt gebruiken, hebt u de volgende beveiligings machtigingen nodig:  

- Het account voor push-installatie van de client configureren: machtiging voor **wijzigen** en **lezen** voor het **site** -object.  

- Client-push gebruiken om de client te installeren op verzamelingen, apparaten en query's: machtiging voor **resource wijzigen** en **lezen** voor het object **verzameling** .  

De standaard beveiligingsrol **infrastructuur beheerder** bevat de vereiste machtigingen voor het beheren van client push installaties.  

#### <a name="software-update-point-based-installation"></a>Installatie op basis van software-updatepunten  

- Als u het Active Directory schema niet hebt uitgebreid of als u clients van een andere forest installeert, gebruikt u groeps beleid om installatie parameters in te richten voor CCMSetup. exe. Zie [Eigenschappen van client installatie inrichten](deploy-clients-to-windows-computers.md#BKMK_Provision)voor meer informatie.  

- Publiceer de Configuration Manager-client naar het software-update punt.  

- De client computer moet communiceren met een distributie punt of een beheer punt om de bron bestanden te downloaden.  

Zie [vereisten voor software-updates](../../../sum/plan-design/prerequisites-for-software-updates.md)voor de beveiligings machtigingen die zijn vereist voor het beheren van Configuration Manager software-updates.  

#### <a name="group-policy-based-installation"></a>Installatie op basis van groeps beleid  

- Als u het Active Directory schema niet hebt uitgebreid of als u clients van een andere forest installeert, gebruikt u groeps beleid om installatie parameters in te richten voor CCMSetup. exe. Zie [Eigenschappen van client installatie inrichten](deploy-clients-to-windows-computers.md#BKMK_Provision)voor meer informatie.  

- De client computer moet communiceren met een distributie punt of een beheer punt om de bron bestanden te downloaden.  

#### <a name="logon-script-based-installation"></a>Aanmeldingscriptinstallatie  

De client computer moet communiceren met een distributie punt of een beheer punt om de bron bestanden te downloaden. Tenzij u CCMSetup. exe hebt opgegeven met de volgende opdracht regel parameter:`ccmsetup /source`  

#### <a name="manual-installation"></a>Handmatige installatie  

De client computer moet communiceren met een distributie punt of een beheer punt om de bron bestanden te downloaden. Tenzij u CCMSetup. exe hebt opgegeven met de volgende opdracht regel parameter:`ccmsetup /source`  

#### <a name="microsoft-intune-mdm-installation"></a>Installatie van Microsoft Intune MDM

- Vereist een Microsoft Intune abonnement en de juiste licenties.  

- Vereist dat het apparaat toegang heeft tot internet, zelfs als dit niet op internet is gebaseerd.  

- Afhankelijk van de use-case, kunt u ook een of beide van de volgende technologieën vereisen:  

    - Azure Active Directory  

    - Cloudbeheergateway  

#### <a name="workgroup-computer-installation"></a>Installatie van de computerwerkgroep  

Als u toegang wilt krijgen tot resources in het domein van de Configuration Manager site server, configureert u een netwerk toegangs account voor de site.  

Zie de [basis concepten voor inhouds beheer](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)voor meer informatie over het configureren van het netwerk toegangs account.  

#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Distributie op basis van een software-installatie (alleen voor upgrades)  

- Als u het Active Directory schema niet hebt uitgebreid of als u clients van een andere forest installeert, gebruikt u groeps beleid om installatie parameters in te richten voor CCMSetup. exe. Zie [Eigenschappen van client installatie inrichten](deploy-clients-to-windows-computers.md#BKMK_Provision)voor meer informatie.

- De client computer moet communiceren met een distributie punt of een beheer punt om de bron bestanden te downloaden.  

Zie [beveiliging en privacy voor toepassings beheer](../../../apps/plan-design/security-and-privacy-for-application-management.md)voor de beveiligings machtigingen die zijn vereist voor het bijwerken van de Configuration Manager-client met behulp van toepassings beheer.  

#### <a name="automatic-client-upgrades"></a>Automatische clientupgrade  

U moet lid zijn van de beveiligingsrol **Volledige beheerder** om de automatische clientupgrades te kunnen configureren.  

### <a name="firewall-requirements"></a>Firewallvereisten  

Als er een firewall is tussen de site systeem servers en de computers waarop u de Configuration Manager-client wilt installeren, raadpleegt u [Windows Firewall en poort instellingen voor clients](windows-firewall-and-port-settings-for-clients.md).  


## <a name="prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a>Vereisten voor clients voor mobiele apparaten  

Wanneer u de Configuration Manager-client op mobiele apparaten installeert en deze registreert, kunt u deze informatie gebruiken om de vereisten te bepalen.  

### <a name="dependencies-external-to-configuration-manager"></a>Afhankelijkheden extern aan Configuration Manager

- Een Microsoftenterprise certificeringsinstantie (CA) met certificaatsjablonen om de vereiste certificaten voor mobiele apparaten te implementeren en te beheren.  

    De uitgevende CA moet automatisch certificaatverzoeken van de gebruikers van mobiele apparaten goedkeuren tijdens het registratieproces.  

    Zie [beveiliging en privacy voor certificaat profielen](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md)voor meer informatie over de certificaat vereisten.  

- Een beveiligingsgroep die gebruikers bevat die hun mobiele apparaten kunnen registreren.  

    Deze beveiligingsgroep wordt gebruikt om het certificaatsjabloon te configureren dat is gebruikt gedurende de registratie van het mobiele apparaat.  

- Optioneel, maar aanbevolen: een DNS-alias (CNAME-record) met de naam **ConfigMgrEnroll**. Configureer deze alias voor de server naam van het inschrijvings proxy punt.  

    Deze DNS-alias is vereist voor de ondersteuning van automatische detectie voor de registratie service. Als u deze DNS-record niet configureert, moeten gebruikers hand matig de naam van het inschrijvings proxy punt opgeven als onderdeel van het registratie proces.  

- Site systeemrol afhankelijkheden voor de computers waarop het inschrijvings punt en de site systeem rollen van het registratie-proxy punt worden uitgevoerd.  

    Zie [ondersteunde besturings systemen voor site systeem servers](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)voor meer informatie.  

### <a name="configuration-manager-dependencies"></a>Configuration Manager-afhankelijkheden

Zie [de site systeem rollen voor clients bepalen](plan/determine-the-site-system-roles-for-clients.md)voor meer informatie.  

- Beheer punt dat is geconfigureerd voor HTTPS-client verbindingen en ingeschakeld is voor mobiele apparaten  

    Een beheer punt is altijd vereist om de Configuration Manager-client op mobiele apparaten te installeren. Naast de configuratie vereisten van HTTPS en ingeschakeld voor mobiele apparaten, moet het beheer punt worden geconfigureerd met een Internet FQDN en client verbindingen van het Internet accepteren.  

- Registratiepunt en proxypunt voor registratie  

    Een registratie-proxypunt beheert registratieverzoeken van mobiele apparaten en het registratiepunt vervolledigt het registratieproces. Het registratiepunt moet hetzelfde zijn in de Active Directory-forest als op de siteserver, maar het registratie-proxypunt kan zich in een andere forest bevinden.  

- Clientinstellingen voor registratie van mobiel apparaat  

    Configureer clientinstellingen om gebruikers toe te laten om mobiele apparaten te registreren en minstens een registratieprofiel te configureren.  

- Reporting Services-punt  

    Het Reporting Services-punt is een optionele, maar aanbevolen sitesysteemrol die rapporten kan weergeven gerelateerd aan registratie van mobiele apparaten en clientbeheer.  

    Zie [Introduction to Reporting](../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.  

- Om registratie te configureren voor mobiele apparaten, moet u de volgende beveiligingsmachtigingen hebben:  

    - Als u de registratie van sitesysteemrollen wilt toevoegen, wijzigen en verwijderen: machtiging voor **wijzigen** voor het **Site**-object.  

    - Als u de clientinstellingen voor registratie wilt configureren: voor standaardclientinstellingen is machtiging voor het **wijzigen** van het **Site**-object vereist en voor aangepaste clientinstellingen zijn **Clientagent**-machtigingen vereist.  

    De standaard beveiligingsrol **volledige beheerder** bevat de vereiste machtigingen voor het configureren van de inschrijvings site systeem rollen.  

- Om geregistreerde mobiele apparaten te beheren, moet u de volgende beveiligingsmachtigingen hebben:  

    - Een mobiel apparaat wissen of buiten gebruik stellen: **resource verwijderen** voor het **verzamelings**object.  

    - Een opdracht wissen of buiten gebruik stellen: **resource verwijderen** voor het **verzamelings**object.  

    - Mobiele apparaat toestaan en blokkeren: **resource wijzigen** voor het **verzamelings**object.  

    - De wachtwoordcode op een mobiel apparaat op afstand vergrendelen of opnieuw instellen: de resource **wijzigen** voor het **verzamelings**object.  

    De standaard beveiligingsrol **Operations-beheerder** bevat de vereiste machtigingen voor het beheren van mobiele apparaten.  

    Zie voor meer informatie over het configureren van beveiligings machtigingen [basis principes van op rollen gebaseerd beheer](../../understand/fundamentals-of-role-based-administration.md) en [Configureer op rollen gebaseerd beheer](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Firewallvereisten

Tussenkomende netwerkapparaten zoals routers en firewalls, en Windows Firewall indien van toepassing, moeten het verkeer toestaan dat gekoppeld is aan inschrijvingen van mobiele apparaten:  

- Tussen mobiele apparaten en het registratieproxypunt: HTTPS (standaard TCP 443)  

- Tussen het registratieproxypunt en het registratiepunt: HTTPS (standaard TCP 443)  

Als u een proxy webserver gebruikt, moet deze worden geconfigureerd voor SSL-Tunneling. SSL-bridging wordt niet ondersteund voor mobiele apparaten.  

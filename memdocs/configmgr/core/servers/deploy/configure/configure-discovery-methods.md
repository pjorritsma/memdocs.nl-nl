---
title: Detectie configureren
titleSuffix: Configuration Manager
description: Configureer detectie methoden om te zoeken naar resources die u wilt beheren vanuit uw netwerk, Active Directory en Azure Active Directory.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3bd03cb15ae1633d8ddfc8c2f26a741d2679b083
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721043"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Detectie methoden voor Configuration Manager configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configureer detectie methoden om te zoeken naar resources die u wilt beheren vanuit uw netwerk, Active Directory en Azure Active Directory (Azure AD). Eerst inschakelen en vervolgens elke methode configureren die u wilt gebruiken om uw omgeving te doorzoeken. U kunt een methode ook uitschakelen met behulp van dezelfde procedure die u gebruikt om deze in te scha kelen. De enige uitzonde ringen op dit proces zijn heartbeat-detectie en server detectie:  

- **Heartbeat-detectie** is standaard al ingeschakeld wanneer u een Configuration Manager primaire site installeert. Het is geconfigureerd om te worden uitgevoerd volgens een basis schema. Zorg dat heartbeat-detectie is ingeschakeld. Hiermee zorgt u ervoor dat de detectie gegevens records (Ddr's) voor apparaten up-to-date zijn. Zie [about heartbeat Discovery](about-discovery-methods.md#bkmk_aboutHeartbeat)(Engelstalig) voor meer informatie over heartbeat-detectie.  

- **Server detectie** is een automatische detectie methode. Er worden computers gevonden die u als site systeem gebruikt. U kunt deze niet configureren of uitschakelen.  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a>Active Directory forest-detectie  

Configureer de instellingen op de volgende locaties van de Configuration Manager-console om de configuratie van Active Directory forest-detectie te volt ooien:  

- In het knoop punt **detectie methoden** :

  - Deze detectie methode in te scha kelen.  

  - Stel een polling planning in.  

  - Selecteer of detectie automatisch grenzen maakt voor de Active Directory-sites en-subnetten die worden gedetecteerd.  

- In het knoop punt **Active Directory forests** :

  - Voeg forests toe die u wilt detecteren.  

  - Detectie van Active Directory-sites en subnetten in dat forest inschakelen.  

  - Instellingen configureren waarmee Configuration Manager-sites hun site gegevens naar het forest kunnen publiceren.  

  - Wijs een account toe om te gebruiken als Active Directory-forest-account voor elk forest.  

Gebruik de volgende procedures om Active Directory forest-detectie in te scha kelen en om afzonderlijke forests te configureren voor gebruik met Active Directory forest-detectie.  

### <a name="configure-active-directory-forest-discovery"></a>Active Directory forest-detectie configureren  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **hiërarchie configuratie**uit en selecteer het knoop punt **detectie methoden** .  

2. Selecteer de Active Directory-forest-detectie methode voor de site waar u detectie wilt configureren.  

3. Selecteer **Eigenschappen**op het tabblad **Start** van het lint.  

4. Configureer op het tabblad **Algemeen** van de eigenschappen de volgende instellingen:  

    - De detectie methode in te scha kelen.

    - Geef opties op voor het maken van site grenzen voor gedetecteerde locaties.  

    - Geef een schema op voor het uitvoeren van detectie.  

5. Selecteer **OK** om de configuratie op te slaan.  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Een forest configureren voor de detectie van Active Directory forests  

1. Vouw in de werk ruimte **beheer** de optie **hiërarchie configuratie**uit en selecteer het knoop punt **Active Directory forests** . Als Active Directory-forestdetectie eerder is uitgevoerd, ziet u iedere gedetecteerde forest in het resultatenvenster. Wanneer deze detectie methode wordt uitgevoerd, detecteert deze het lokale forest en alle vertrouwde forests. Hand matig niet-vertrouwde forests toevoegen.  

    - Als u een eerder gedetecteerd forest wilt configureren, selecteert u het forest in het resultaten venster. Selecteer in het lint **Eigenschappen** om de forest-eigenschappen te openen.

    - Als u een nieuw forest wilt configureren dat niet wordt weer gegeven, selecteert u in de groep **maken** op het tabblad **Start** van het lint de optie **forest toevoegen**. Met deze actie wordt het dialoog venster **forests toevoegen** geopend.

2. Op het tabblad **Algemeen** voltooit u de configuraties voor het forest dat u wilt detecteren en geeft u het **Active Directory forest-account**op. Zie [accounts](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account)voor meer informatie over dit account.  

    > [!NOTE]  
    > Voor Active Directory-forestdetectie is een globaal account nodig om niet-vertrouwde forests te detecteren en ernaar te publiceren. Als u het computer account van de site server niet gebruikt, kunt u alleen een globaal account selecteren.  

3. Als u van plan bent om sites site gegevens te laten publiceren naar dit forest, kunt u op het tabblad **publiceren** de configuraties volt ooien om naar dit forest te publiceren.  

    > [!NOTE]  
    > Als u sites naar een forest wilt publiceren, breidt u het Active Directory schema van dat forest uit voor Configuration Manager. Het Active Directory forest-account moet machtigingen voor volledig beheer hebben voor de systeem container in dat forest.  

4. Selecteer **OK** om de configuratie op te slaan.  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a>Detectie Active Directory voor computers, gebruikers of groepen  

Als u de detectie van computers, gebruikers of groepen wilt configureren, begint u met de volgende algemene stappen:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **hiërarchie configuratie**uit en selecteer het knoop punt **detectie methoden** .  

2. Selecteer de methode voor de site waar u detectie wilt configureren.  

3. Selecteer **Eigenschappen**op het tabblad **Start** van het lint.  

4. Schakel op het tabblad **Algemeen** van de eigenschappen het selectie vakje in om detectie in te scha kelen. U kunt de detectie nu ook configureren en vervolgens teruggaan om de detectie later in te scha kelen.  

Gebruik vervolgens de informatie in de volgende secties om de specifieke detectie methoden te configureren:  

- [Active Directory-groepdetectie](#bkmk_config-adgd)  

- [Active Directory-systeemdetectie](#bkmk_config-adgd)  

- [Detectie Active Directory-gebruiker](#bkmk_config-adud)  

> [!NOTE]  
> De informatie in deze sectie is niet van toepassing op Active Directory forest-detectie.  

Hoewel al deze detectie methoden onafhankelijk van elkaar zijn, delen ze vergelijk bare opties. Zie voor meer informatie over deze configuratie opties [gedeelde opties voor groeps-, systeem-en gebruikers detectie](about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
> De Active Directory polling door elk van deze detectie methoden kan aanzienlijke netwerk verkeer genereren. Overweeg elke detectie methode te plannen om uit te voeren op het moment dat dit netwerk verkeer geen nadelige invloed heeft op het zakelijke gebruik van uw netwerk.  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a>Detectie van Active Directory groepen configureren  

1. Selecteer op het tabblad **Algemeen** van de Active Directory groeps detectie venster Eigenschappen **toevoegen** om een detectie bereik te configureren. Selecteer **groepen** of **locatie**. Voltooi vervolgens de volgende configuraties in het dialoog venster **groepen toevoegen** of **Active Directory locatie toevoegen** :  

    1. Geef een **naam** op voor dit detectie bereik.  

    2. Geef een **Active Directory-domein** of **locatie** op waarnaar moet worden gezocht:  

        - Als u **groepen**hebt gekozen, geeft u een of meer Active Directory groepen op die moeten worden gedetecteerd.  

        - Als u **locatie**hebt gekozen, geeft u een Active Directory container op als locatie die u wilt detecteren. U kunt ook een recursieve zoek opdracht van Active Directory onderliggende containers inschakelen voor deze locatie.  

    3. Geef het **detectie account** van de Active Directory-groep op die de site gebruikt om dit detectie bereik te doorzoeken. Zie [accounts](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account)voor meer informatie.  

    4. Selecteer **OK** om de configuratie van het detectie bereik op te slaan.  

2. Herhaal de vorige stappen voor elk extra detectie bereik dat u wilt definiëren.  

3. Configureer op het tabblad **polling schema** zowel de volledige detectie polling-planning als de detectie van verschillen.

4. Configureer op het tabblad **Opties de optie** instellingen om verouderde computer records te filteren of uit te sluiten van detectie. Configureer ook de detectie van het lidmaatschap van distributie groepen.  

    > [!NOTE]  
    > Active Directory groeps detectie detecteert standaard alleen het lidmaatschap van beveiligings groepen.  

5. Selecteer **OK** om de configuratie op te slaan.  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a>Active Directory systeem detectie configureren  

1. Op het tabblad **Algemeen** van de venster Eigenschappen Active Directory systeem detectie selecteert](media/Disc_new_Icon.gif) u het pictogram **nieuw** pictogram ![om een nieuwe Active Directory-container op te geven. In het dialoog venster **Active Directory container** voltooit u de volgende configuraties:  

    1. Typ of blader naar een locatie voor het **pad**. Deze waarde is een geldig LDAP-pad naar een container of organisatie-eenheid (OE). De site voert een query uit op dit pad naar bronnen. Bijvoorbeeld: `LDAP://CN=Computers,DC=contoso,DC=com`  

    2. Opties opgeven waarmee het zoek gedrag wordt gewijzigd:  

        - **Objecten in Active Directory groepen detecteren**: de site zoekt ook naar het lidmaatschap van groepen in dit pad.  

        - **Recursief zoeken Active Directory onderliggende containers**: als u deze optie inschakelt, doorzoekt de site eventuele extra containers of organisatie-eenheden binnen het bovenstaande pad. Als u deze optie uitschakelt, zoekt de site alleen naar bronnen in het specifieke pad.  

          Vanaf versie 1806 selecteert u subcontainers die moeten worden uitgesloten van deze recursieve zoek opdracht. Deze optie helpt u bij het verminderen van het aantal gedetecteerde objecten. Selecteer **toevoegen** om de containers onder het bovenstaande pad te kiezen. Selecteer in het dialoog venster nieuwe container selecteren een onderliggende container die u wilt uitsluiten. Selecteer **OK** om het dialoog venster nieuwe container selecteren te sluiten.<!--1358143-->

          > [!Tip]  
          > De lijst met Active Directory containers in het Active Directory systeem detectie venster Eigenschappen bevat een kolom met **uitsluitingen**. Wanneer u containers selecteert om uit te sluiten, is deze waarde **Ja**.  

    3. Geef voor elke locatie het account op dat moet worden gebruikt als het **detectie account Active Directory**. Zie [accounts](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account)voor meer informatie.  

        > [!TIP]  
        > Voor elke opgegeven locatie kunt u een set detectie opties en een uniek Active Directory detectie account configureren.  

    4. Selecteer **OK** om de Active Directory container configuratie op te slaan.  

2. Configureer op het tabblad **polling schema** zowel de volledige detectie polling-planning als de detectie van verschillen.  

3. Configureer op het tabblad **kenmerken van Active Directory** aanvullende Active Directory kenmerken voor computers die u wilt detecteren. Op dit tabblad worden de standaard object kenmerken weer gegeven.  

    > [!Tip]  
    > Uw organisatie gebruikt bijvoorbeeld het kenmerk **Beschrijving** voor het computer account in Active Directory. Selecteer **aangepast**en voeg toe `Description` als aangepast kenmerk. Nadat deze detectie methode is uitgevoerd, wordt dit kenmerk weer gegeven op het tabblad apparaateigenschappen in de Configuration Manager-console.<!--513948-->  

4. Configureer op het tabblad **Opties de optie** instellingen om verouderde computer records te filteren of uit te sluiten van detectie.  

5. Selecteer **OK** om de configuratie op te slaan.  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a>Active Directory gebruikers detectie configureren  

1. Op het tabblad **Algemeen** van de Active Directory gebruikers detectie venster Eigenschappen selecteert](media/Disc_new_Icon.gif) u het pictogram **nieuw** pictogram ![om een nieuwe Active Directory-container op te geven. In het dialoog venster **Active Directory container** voltooit u de volgende configuraties:  

    1. Geef een of meer locaties op waarnaar moet worden gezocht.  

    2. Geef voor elke locatie opties op waarmee het zoek gedrag wordt gewijzigd.  

    3. Geef voor elke locatie het account op dat moet worden gebruikt als het **detectie account Active Directory**. Zie [accounts](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account)voor meer informatie.  

        > [!NOTE]  
        > Voor elke opgegeven locatie kunt u een unieke set detectie opties en een uniek Active Directory detectie account configureren.  

    4. Selecteer **OK** om de Active Directory container configuratie op te slaan.  

2. Configureer op het tabblad **polling schema** zowel de volledige detectie polling-planning als de detectie van verschillen.  

3. Configureer op het tabblad **kenmerken van Active Directory** aanvullende Active Directory kenmerken voor computers die u wilt detecteren. Op dit tabblad worden de standaard object kenmerken weer gegeven.  

4. Selecteer **OK** om de configuratie op te slaan.  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a>Azure AD-gebruikers detectie

Azure AD-gebruikers detectie is niet ingeschakeld of geconfigureerd op dezelfde manier als andere detectie methoden. Configureer deze wanneer u de Configuration Manager-site onboardt naar Azure AD.

Zie [Azure AD-gebruikers detectie](about-discovery-methods.md#azureaddisc)voor meer informatie.

### <a name="prerequisites"></a>Vereisten

[Configureer Azure-Services](azure-services-wizard.md) voor **Cloud beheer**om deze detectie methode in te scha kelen en te configureren.

Als u Configuration Manager gebruikt om de Azure-app te *maken* , wordt de app geconfigureerd met de juiste machtigingen.

Als u eerst de app in azure maakt en deze vervolgens in Configuration Manager *importeert* , moet u de app hand matig configureren. Deze configuratie omvat het verlenen van de server app-machtiging voor het lezen van Directory gegevens.

1. Open de [Azure Portal](https://portal.azure.com) als gebruiker met *globale beheerders* machtigingen. Ga naar **Azure Active Directory**en selecteer **app-registraties**. Schakel zo nodig over naar **alle toepassingen** .

1. Selecteer de doel toepassing.

1. Selecteer in het menu **beheren** de optie **API-machtigingen**.  

    1. Selecteer **een machtiging toevoegen**in het deel venster **API-machtigingen** .  

    2. Schakel in het deel venster **API-machtigingen voor aanvragen** over naar api's die **Mijn organisatie gebruikt**.  

    3. Zoek en selecteer de **Microsoft Graph** -API.  

        > [!Tip]
        > Gebruik in versie 1810 en eerder de **Azure Active Directory Graph** API.

    4. Selecteer de groep **toepassings machtigingen** . Vouw **map**uit en selecteer **Directory. Read. all**.  

    5. Selecteer **machtigingen toevoegen**.  

1. Selecteer in het deel venster **API-machtigingen** in de sectie **toestemming geven** de optie **beheerder toestemming geven...**. Selecteer **Ja**.  

### <a name="configure-azure-ad-user-discovery"></a>Azure AD-gebruikers detectie configureren

Bij het configureren van de Azure-service voor **Cloud beheer** :

- Selecteer op de pagina **detectie** van de wizard de optie voor het **inschakelen van Azure Active Directory gebruikers detectie**.
- **Instellingen**selecteren.
- Configureer in het dialoog venster instellingen van Azure AD-gebruikers detectie een schema voor wanneer detectie plaatsvindt. U kunt ook Delta detectie inschakelen, waarmee alleen wordt gecontroleerd op nieuwe of gewijzigde accounts in azure AD.

> [!Note]  
> Als de gebruiker een federatieve of gesynchroniseerde identiteit is, moet u Configuration Manager [Active Directory gebruikers detectie](about-discovery-methods.md#bkmk_aboutUser) en Azure AD-gebruikers detectie gebruiken. Zie [een strategie voor het implementeren van een hybride identiteit definiëren](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy)voor meer informatie over hybride identiteiten.<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Detectie van Azure AD-gebruikers groepen

<!--3611956-->
> [!Tip]  
> Deze functie werd voor het eerst in versie 1906 geïntroduceerd als een [voorlopige functie](../../manage/pre-release-features.md). Vanaf versie 2002 is het niet langer een functie van de voorlopige versie.  

U kunt gebruikers groepen en leden van deze groepen vinden vanuit Azure AD. Wanneer de site gebruikers detecteert in azure AD-groepen die niet eerder zijn gedetecteerd, worden deze toegevoegd als nieuwe gebruikers resources in Configuration Manager. Er wordt een resource record voor een gebruikers groep gemaakt wanneer de groep een beveiligings groep is.

### <a name="prerequisites"></a>Vereisten

- Azure- [service](azure-services-wizard.md) voor Cloud beheer
- Machtiging voor het lezen en doorzoeken van Azure AD-groepen

### <a name="limitations"></a>Beperkingen

Detectie van verschillen in azure AD-gebruikers groepen is momenteel uitgeschakeld.

### <a name="log-files"></a>Logboekbestanden

Gebruik het SMS_AZUREAD_DISCOVERY_AGENT. log voor het oplossen van problemen. Dit logboek wordt ook gedeeld met Azure AD-gebruikers detectie. Zie [logboek bestanden](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs)voor meer informatie.

### <a name="enable-azure-ad-user-group-discovery"></a>Detectie van Azure AD-gebruikers groepen inschakelen

Detectie inschakelen voor een bestaande Azure-service voor **Cloud beheer** :

1. Ga naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure-Services** .
1. Selecteer een van uw Azure-Services en selecteer **Eigenschappen** in het lint.
1. Schakel op het tabblad **detectie** het selectie vakje **Azure Active Directory groeps detectie inschakelen**in en selecteer vervolgens **instellingen**.
1. Selecteer **toevoegen** onder het tabblad **detectie bereiken** .
    - U kunt het **polling-schema** op het andere tabblad wijzigen.
1. Selecteer een of meer gebruikers groepen. U kunt op naam **zoeken** en kiezen of u **alleen beveiligings groepen**wilt weer geven.
    - U wordt gevraagd om u aan te melden bij Azure wanneer u de eerste keer **zoeken** selecteert.
1. Selecteer **OK** wanneer u klaar bent met het selecteren van groepen.
1. Zodra de detectie is voltooid, kunt u door uw Azure AD-gebruikers groepen bladeren in het knoop punt **gebruikers** .

Detectie inschakelen bij het configureren van een nieuwe Azure-service voor **Cloud beheer** :

- Selecteer op de pagina **detectie** van de wizard de optie voor het **inschakelen van Azure Active Directory groeps detectie**.
- **Instellingen**selecteren.
- In het dialoog venster instellingen voor de Azure AD-groeps detectie configureert u het detectie bereik en een schema voor wanneer detectie plaatsvindt.


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a>Heartbeat-detectie

Configuration Manager schakelt de heartbeat-detectie methode in wanneer u een primaire site installeert. Als u het standaard schema van elke zeven dagen wilt gebruiken, is er niets anders om te configureren. Als dat niet het geval is, hoeft u alleen de planning te configureren voor hoe vaak clients de heartbeat-detectie gegevens record naar een beheer punt verzenden.  

> [!NOTE]  
> Als u zowel de Push-client installatie als de site onderhouds taak voor **duidelijke installatie vlag** op dezelfde site inschakelt, stelt u het schema van de heartbeat-detectie in op minder dan de **herdetectieperiode** van de client voor de onderhouds taak **voor het wissen van installatie vlag** . Zie [onderhouds taken](../../manage/maintenance-tasks.md)voor meer informatie over site-onderhouds taken.  

### <a name="configure-the-heartbeat-discovery-schedule"></a>Het heartbeat-detectie schema configureren  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **hiërarchie configuratie**uit en selecteer het knoop punt **detectie methoden** .  

2. Selecteer de **heartbeat-detectie** methode voor de site waar u heartbeat-detectie wilt configureren.  

3. Selecteer **Eigenschappen**op het tabblad **Start** van het lint.  

4. Configureer de frequentie waarmee clients een record met heartbeat-detectie gegevens verzenden. Selecteer **OK** om de configuratie op te slaan.  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a>Netwerk detectie  

Meer informatie over de volgende onderwerpen voordat u netwerk detectie configureert:  

- Beschik bare niveaus van netwerk detectie  

- Beschik bare opties voor netwerk detectie  

- Netwerk detectie op het netwerk beperken  

Zie [over netwerk detectie](about-discovery-methods.md#bkmk_aboutNetwork)voor meer informatie.  

De volgende secties bevatten informatie over algemene configuraties voor netwerk detectie. U kunt een of meer van deze configuraties configureren voor gebruik tijdens dezelfde detectie-uitvoering. Als u meerdere configuraties gebruikt, moet u de interacties plannen die van invloed kunnen zijn op de resultaten van de detectie.  

U kunt bijvoorbeeld alle Simple Network Management Protocol-apparaten (SNMP) detecteren die gebruikmaken van een specifieke SNMP-communitynaam. Voor dezelfde detectie-uitvoering schakelt u detectie uit op een specifiek subnet. Wanneer detectie wordt uitgevoerd, detecteert netwerk detectie de SNMP-apparaten met de opgegeven naam van de community niet op het subnet dat u hebt uitgeschakeld.  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a>Uw netwerk topologie bepalen  

U kunt een alleen-topologie detectie gebruiken om uw netwerk toe te wijzen. Dit type detectie detecteert geen potentiële clients. De netwerk detectie met alleen topologie is afhankelijk van SNMP.  

Wanneer u uw netwerk topologie toewijst, configureert u de **maximale hops** op het tabblad **SNMP** in het dialoog venster **netwerk detectie-eigenschappen** . Slechts enkele hops kunnen helpen de netwerk bandbreedte te beheren die wordt gebruikt wanneer detectie wordt uitgevoerd. Naarmate u meer van uw netwerk ontdekt, verhoogt u het aantal hops om een beter inzicht te krijgen in uw netwerk topologie.  

Nadat u uw netwerk topologie hebt begrepen, configureert u extra eigenschappen voor netwerk detectie. Met deze eigenschappen kunnen potentiële clients en hun besturings systemen worden gedetecteerd. Configureer ook netwerk detectie om de netwerk segmenten te beperken waarop de zoek actie kan worden doorzocht.  

Zie [hoe u uw netwerk topologie kunt bepalen](#bkmk_proc-top) voor meer informatie

### <a name="network-discovery-search-options"></a>Zoek opties voor netwerk detectie

Configuration Manager ondersteunt de volgende methoden om het netwerk te doorzoeken:

- [Zoek opdrachten beperken met behulp van subnetten](#BKMK_LimitBySubnet)
- [Zoeken in een specifiek domein](#BKMK_SearchByDomain)
- [Zoek opdrachten beperken met behulp van SNMP-communitynamen](#BKMK_LimitBySNMPname)
- [Zoeken naar een specifieke DHCP-server](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a>Zoek opdrachten beperken met behulp van subnetten  

U kunt netwerk detectie configureren om te zoeken naar specifieke subnetten tijdens het uitvoeren van een detectie. Standaard zoekt netwerk detectie in het subnet van de server die detectie uitvoert. Alle extra subnetten die u configureert en inschakelt, zijn alleen van toepassing op SNMP-en DHCP-Zoek opties. Wanneer netwerk detectie domeinen doorzoekt, wordt het niet beperkt door configuraties voor subnetten.  

Als u een of meer subnetten opgeeft op het tabblad **subnetten** in het dialoog venster **netwerk detectie-eigenschappen** , wordt alleen gezocht in de subnetten die u markeert als **ingeschakeld**.  

Wanneer u een subnet uitschakelt, wordt het door de site uitgesloten van detectie en gelden de volgende voor waarden:  

- Op SNMP gebaseerde query's worden niet uitgevoerd op het subnet.  

- DHCP-servers beantwoorden niet met een lijst met resources die zich in het subnet bevinden.  

- Op domein gebaseerde query's kunnen bronnen detecteren die zich in het subnet bevinden.  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a>Zoeken in een specifiek domein  

U kunt netwerk detectie configureren om te zoeken in een specifiek domein of een set domeinen tijdens het uitvoeren van een detectie. Netwerk detectie doorzoekt standaard het lokale domein van de server die detectie uitvoert.  

Als u een of meer domeinen opgeeft op het tabblad **domeinen** in het dialoog venster **netwerk detectie-eigenschappen** , wordt alleen gezocht in de domeinen die u als **ingeschakeld**markeert.  

Wanneer u een domein uitschakelt, wordt het door de site uitgesloten van detectie en zijn de volgende voor waarden van toepassing:  

- Netwerk detectie zoekt geen domein controllers in dat domein op.  

- Op SNMP gebaseerde query's kunnen nog steeds worden uitgevoerd op subnetten in het domein.  

- DHCP-servers kunnen nog steeds antwoorden met een lijst met resources die zich in het domein bevinden.  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a>Zoek opdrachten beperken met behulp van SNMP-communitynamen  

U kunt netwerk detectie configureren om te zoeken in een specifieke SNMP-community of een set van community's tijdens een detectie-uitvoering. Met de-methode wordt standaard de naam van de **open bare** Community geconfigureerd.  

Netwerk detectie gebruikt community-namen om toegang te krijgen tot routers die SNMP-apparaten zijn. Een router kan netwerk detectie leveren met informatie over andere routers en subnetten die zijn gekoppeld aan de eerste router.  

> [!NOTE]  
> SNMP-community-namen lijken op wacht woorden. Netwerk detectie kan alleen informatie ophalen van een SNMP-apparaat waarvoor u een community-naam hebt opgegeven. Elk SNMP-apparaat kan een eigen community-naam hebben, maar vaak wordt dezelfde communitynaam gedeeld op verschillende apparaten. Daarnaast hebben de meeste SNMP-apparaten de standaard communitynaam **openbaar**. Maar sommige organisaties verwijderen de naam van de **open bare** community van hun apparaten als een veiligheids maatregel.  

Als u meer dan één SNMP-community opneemt op het tabblad **SNMP** in het dialoog venster **netwerk detectie-eigenschappen** , wordt deze gezocht in de volg orde waarin ze worden weer gegeven. Zorg ervoor dat de meestgebruikte namen boven aan de lijst staan. Deze configuratie helpt het netwerk verkeer te minimaliseren dat door de site wordt gegenereerd wanneer wordt geprobeerd verbinding te maken met een apparaat met behulp van verschillende namen.

> [!NOTE]  
> Naast het gebruik van de SNMP-communitynaam, kunt u het IP-adres of de omgezette naam van een specifiek SNMP-apparaat opgeven. U kunt deze actie uitvoeren op het tabblad **SNMP-apparaten** in het dialoog venster **netwerk detectie-eigenschappen** .  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a>Zoeken naar een specifieke DHCP-server  

U kunt netwerk detectie configureren voor het gebruik van een specifieke DHCP-server of meerdere servers om DHCP-clients te detecteren tijdens het uitvoeren van een detectie.  

Netwerk detectie doorzoekt elke DHCP-server die u opgeeft op het tabblad **DHCP** in het dialoog venster **netwerk detectie-eigenschappen** . Als op de server waarop de detectie wordt uitgevoerd, het IP-adres van een DHCP-server wordt gebruikt, kunt u detectie configureren om de DHCP-server te doorzoeken. Schakel dit gedrag in met de optie voor **het toevoegen van de DHCP-server die de site server heeft geconfigureerd voor gebruik**.  

> [!NOTE]  
> Voor een geslaagde configuratie van een DHCP-server in netwerk detectie moet uw omgeving IPv4 ondersteunen. U kunt netwerk detectie niet configureren voor het gebruik van een DHCP-server in een systeem eigen IPv6-omgeving.  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a>Netwerk detectie configureren  

Gebruik de volgende procedures om eerst alleen uw netwerk topologie te detecteren en vervolgens netwerk detectie te configureren om potentiële clients te detecteren door gebruik te maken van een of meer van de beschik bare opties voor netwerk detectie.  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a>Uw netwerk topologie bepalen  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **hiërarchie configuratie**uit en selecteer het knoop punt **detectie methoden** .  

2. Selecteer de **netwerk detectie** methode voor de site waar u netwerk bronnen wilt detecteren.  

3. Selecteer **Eigenschappen**op het tabblad **Start** van het lint.  

    - Selecteer op het tabblad **Algemeen** de optie om **netwerk detectie in te scha kelen**. Selecteer vervolgens **topologie** uit het **type detectie** opties.  

    - Op het tabblad **subnetten** selecteert u de optie **lokale subnetten zoeken** .  

      > [!TIP]  
      > Als u de specifieke subnetten kent die uw netwerk vormen, schakelt u het selectie vakje **lokale subnetten zoeken** uit. Selecteer vervolgens het **New** pictogram nieuw ![pictogram](media/Disc_new_Icon.gif)en voeg de specifieke subnetten toe die u wilt doorzoeken. Voor grote netwerken zoekt u slechts één of twee subnetten tegelijk om het gebruik van netwerk bandbreedte te minimaliseren.  

    - Selecteer op het tabblad **domeinen** de optie voor het **zoeken naar het lokale domein**.  

    - Selecteer op het tabblad **SNMP** een optie in de vervolg keuzelijst **maximum aantal hops** . Met deze optie geeft u op hoeveel router-hops netwerk detectie kan uitvoeren bij het toewijzen van uw topologie.  

      > [!TIP]  
      > Wanneer u uw netwerk topologie voor het eerst toewijst, configureert u slechts een paar router-hops om het gebruik van netwerk bandbreedte te minimaliseren.  

4. Op het tabblad **planning** selecteert u het pictogram **Nieuw** pictogram ![](media/Disc_new_Icon.gif)en stelt u een planning in voor het uitvoeren van detectie.  

    > [!NOTE]  
    > U kunt geen andere detectie configuratie toewijzen aan afzonderlijke planningen voor netwerk detectie. Telkens wanneer netwerk detectie wordt uitgevoerd, wordt de huidige detectie configuratie gebruikt.  

5. Selecteer **OK** om de configuraties te accepteren. Netwerk detectie wordt op de geplande tijd uitgevoerd.  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a>Netwerk detectie configureren  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **hiërarchie configuratie**uit en selecteer het knoop punt **detectie methoden** .  

2. Selecteer de **netwerk detectie** methode voor de site waar u netwerk bronnen wilt detecteren.  

3. Selecteer **Eigenschappen**op het tabblad **Start** van het lint.  

4. Selecteer op het tabblad **Algemeen** de optie om **netwerk detectie in te scha kelen**.  

    - Selecteer in het **type detectie** opties het type detectie dat u wilt uitvoeren.  

    - Schakel de optie voor **trage netwerken** in voor Configuration Manager om automatische aanpassingen te maken voor netwerken met een lage band breedte.  

5. Schakel over naar het tabblad **subnetten** om detectie te configureren voor het zoeken naar subnetten. Configureer vervolgens een of meer van de volgende opties:  

    - Als u detectie wilt uitvoeren op subnetten die lokaal zijn voor de computer die detectie uitvoert, schakelt u de optie voor het **zoeken van lokale subnetten**in.  

    - Als u een specifiek subnet wilt doorzoeken, controleert u of het subnet wordt weer gegeven in **subnetten om te zoeken** en heeft de **Zoek** waarde **ingeschakeld**:  

      1. Als het subnet niet wordt weer gegeven, selecteert u ![het nieuwe](media/Disc_new_Icon.gif) **pictogram Nieuw** pictogram. Voer in het dialoog venster **nieuwe toewijzing van subnet** de informatie over het **subnet** en **masker** in en selecteer vervolgens **OK**. Een nieuw subnet is standaard ingeschakeld voor zoeken.  

      2. Als u de **Zoek** waarde voor een vermeld subnet wilt wijzigen, selecteert u deze in de lijst. Selecteer vervolgens de **wissel** knop om de waarde te scha kelen tussen **uitgeschakeld** en **ingeschakeld**.  

6. Als u detectie wilt configureren om domeinen te zoeken, gaat u naar het tabblad **domeinen** . Configureer vervolgens een of meer van de volgende opties:  

    - Als u detectie wilt uitvoeren op het domein van de computer die detectie uitvoert, schakelt u de optie voor het zoeken naar het **lokale domein**in.  

    - Als u een specifiek domein wilt doorzoeken, moet u ervoor zorgen dat het domein wordt weer gegeven in **domeinen** en dat er een **Zoek** waarde is **ingeschakeld**:  

      1. Als het domein niet wordt weer gegeven, selecteert u ![het nieuwe](media/Disc_new_Icon.gif) **pictogram Nieuw** pictogram. Voer in het dialoog venster **domein eigenschappen** de **domein** informatie in en selecteer **OK**. Een nieuw domein is standaard ingeschakeld voor zoeken.  

      2. Als u de **Zoek** waarde voor een vermeld domein wilt wijzigen, selecteert u deze in de lijst. Selecteer vervolgens de **wissel** knop om de waarde te scha kelen tussen **uitgeschakeld** en **ingeschakeld**.  

7. Als u detectie wilt configureren om te zoeken naar specifieke SNMP-communitynamen voor SNMP-apparaten, gaat u naar het tabblad **SNMP** . Configureer vervolgens een of meer van de volgende opties:  

    - Als u een SNMP-communitynaam wilt toevoegen aan de lijst met **SNMP**-communitynamen, selecteert ![u het](media/Disc_new_Icon.gif)pictogram **Nieuw** pictogram. Geef in het dialoog venster **nieuwe SNMP-communitynaam** de **naam** op van de SNMP-community en selecteer **OK**.  

    - Als u een SNMP-communitynaam wilt verwijderen, selecteert u de naam van de community en ![selecteert u](media/Disc_delete_Icon.gif)vervolgens het pictogram **verwijderen** pictogram verwijderen.  

    - Als u de zoek volgorde van SNMP-communitynamen wilt aanpassen, selecteert u een community-naam in de lijst. Selecteer vervolgens het **pictogram item** ![omhoog verplaatsen](media/Disc_moveUp_Icon.gif) of het pictogram **item omlaag** verplaatsen omlaag ![bewegen.](media/Disc_moveDown_Icon.gif) Wanneer detectie wordt uitgevoerd, worden communitynamen in een volg orde van boven naar beneden doorzocht. 

    - Als u het maximum aantal router-hops wilt configureren voor gebruik door SNMP-Zoek opdrachten, selecteert u het aantal hops in de vervolg keuzelijst **maximum aantal hops** .  

8. Als u een SNMP-apparaat wilt configureren, gaat u naar het tabblad **SNMP-apparaten** . Als het apparaat niet wordt weer gegeven, selecteert u ![het nieuwe](media/Disc_new_Icon.gif) **pictogram Nieuw** pictogram. Geef in het dialoog venster **Nieuw SNMP-apparaat** het IP-adres of de apparaatnaam van het SNMP-apparaat op en selecteer vervolgens **OK**.  

    > [!NOTE]  
    > Als u een apparaatnaam opgeeft, moet Configuration Manager de NetBIOS-naam kunnen omzetten in een IP-adres.  

9. Schakel over naar het tabblad **DHCP** om detectie te configureren voor het uitvoeren van query's op specifieke DHCP-servers. Configureer vervolgens een of meer van de volgende opties:  

    - Als u een query wilt uitvoeren op de DHCP-server op de computer waarop de detectie wordt uitgevoerd, schakelt u de optie in om **altijd de DHCP-server van de site server te gebruiken**.  

      > [!NOTE]  
      > Als u deze optie wilt gebruiken, moet de server zijn IP-adres van een DHCP-server leasen en kan geen statisch IP-adres gebruiken.  

    - Als u een query wilt uitvoeren op een specifieke DHCP- ![server,](media/Disc_new_Icon.gif)selecteert u het pictogram **Nieuw** pictogram. Geef in het dialoog venster **nieuwe DHCP-server** het IP-adres of de server naam van de DHCP-server op en selecteer **OK**.  

      > [!NOTE]  
      > Als u een server naam opgeeft, moet Configuration Manager de NetBIOS-naam kunnen omzetten in een IP-adres.  

10. Als u wilt configureren wanneer detectie wordt uitgevoerd, gaat u naar het tabblad **planning** . Selecteer vervolgens het **New** pictogram nieuw ![pictogram](media/Disc_new_Icon.gif) om een planning in te stellen voor het uitvoeren van netwerk detectie. U kunt meerdere terugkerende schema's en meerdere schema's zonder terugkeer patroon configureren.  

    > [!NOTE]  
    > Als op het tabblad **planning** meer dan één schema tegelijk wordt weer gegeven, wordt netwerk detectie uitgevoerd voor alle planningen die worden geconfigureerd op het tijdstip dat is opgegeven in de planning. Dit gedrag geldt ook voor terugkerende schema's.  

11. Selecteer **OK** om uw configuraties op te slaan.  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a>Controleren of de netwerk detectie is voltooid  

De tijd die nodig is om netwerk detectie te volt ooien, kan variëren, afhankelijk van een of meer van de volgende factoren:  

- De grootte van uw netwerk  

- De topologie van uw netwerk  

- Het maximum aantal hops dat is geconfigureerd voor het vinden van routers in het netwerk  

- Het type detectie dat wordt uitgevoerd  

Netwerk detectie maakt geen berichten om u te waarschuwen wanneer het is voltooid. Gebruik de volgende procedure om te controleren wanneer de detectie is voltooid:  

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** . Vouw **systeem status**uit en selecteer vervolgens het knoop punt **status bericht query's** .  

2. Selecteer de query **alle status berichten** .  

3. Selecteer op het tabblad **Start** van het lint de optie **berichten weer geven**in de groep **status bericht query's** .  

4. Selecteer in het venster alle status berichten een waarde in de vervolg keuzelijst **datum en tijd selecteren** die bevat hoelang geleden de detectie is gestart. Selecteer vervolgens **OK** om de **Configuration Manager Status Message Viewer**te openen.  

    > [!TIP]  
    > U kunt ook de optie **datum en tijd opgeven** gebruiken om een bepaalde datum en tijd te selecteren waarop de detectie is uitgevoerd. Deze optie is handig wanneer u netwerk detectie op een bepaalde datum hebt uitgevoerd en alleen berichten vanaf die datum wilt ophalen.  

5. Als u wilt valideren dat netwerk detectie is voltooid, zoekt u naar een status bericht met de volgende details:  

    - Bericht-ID: **502**  

    - Onderdeel: **SMS_NETWORK_DISCOVERY**  

    - Beschrijving: **dit onderdeel is gestopt**  

    Als dit status bericht niet aanwezig is, is de netwerk detectie nog niet voltooid.  

6. Als u wilt valideren wanneer netwerk detectie gestart is, zoekt u naar een status bericht met de volgende details:  

    - Bericht-ID: **500**  

    - Onderdeel: **SMS_NETWORK_DISCOVERY**  

    - Beschrijving: **dit onderdeel is gestart**  

    Deze informatie controleert of netwerk detectie is gestart. Als deze informatie niet aanwezig is, moet u netwerk detectie opnieuw plannen.  

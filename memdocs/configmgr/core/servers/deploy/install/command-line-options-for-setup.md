---
title: Opdracht regel opties voor Setup
titleSuffix: Configuration Manager
description: Maak automatiserings scripts om Configuration Manager te installeren vanaf een opdracht regel.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e4950e32fa5ddc0a4fc1a13ec8e584dc1ae9ff3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718250"
---
# <a name="command-line-options-for-configuration-manager-setup"></a>Opdracht regel opties voor het instellen van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de volgende informatie om scripts te configureren of om Configuration Manager te installeren vanaf een opdracht regel.  

## <a name="command-line-options-for-setup"></a><a name="bkmk_setup"></a>Opdracht regel opties voor installatie

Voer Setup uit vanuit `\BIN\X64` de map van het installatiepad van Configuration Manager op de site server.

### `/DEINSTALL`

Verwijder de site. Voer Setup uit vanaf de site Server computer.  

### `/DONTSTARTSITECOMP`

Een site installeren, maar voor komt dat de Site Component Manager-service wordt gestart. De site is pas actief wanneer de Site Component Manager-service wordt gestart. De Site Component Manager is verantwoordelijk voor het installeren en starten van de SMS_Executive-service en voor aanvullende processen op de site. Wanneer de installatie van de site is voltooid en u de Site Component Manager-service start, wordt de SMS_Executive-service en aanvullende processen geïnstalleerd die nodig zijn om de site te kunnen uitvoeren.  

### `/HIDDEN`

Verberg de gebruikers interface tijdens de installatie. Gebruik deze optie alleen in combi natie met de optie **/script** . Het script bestand voor installatie zonder toezicht moet alle vereiste opties bevatten of het installatie programma mislukt.  

### `/NOUSERINPUT`

Gebruikers invoer uitschakelen tijdens de installatie, maar de wizard Setup wordt weer gegeven. Gebruik deze optie alleen in combi natie met de optie **/script** . Het script bestand voor installatie zonder toezicht moet alle vereiste opties bevatten of het installatie programma mislukt.  

### `/RESETSITE`

Voer een site opnieuw in om de data base en service accounts voor de site opnieuw in te stellen.

Zie [Run a site reset](../../manage/modify-your-infrastructure.md#bkmk_reset)(Engelstalig) voor meer informatie.  

### `/TESTDBUPGRADE`

Voer een test uit op een back-up van de site database om er zeker van te zijn dat de data base kan worden bijgewerkt.

> [!IMPORTANT]  
> Voer deze opdracht regel optie niet uit op uw productie site database. Als u deze opdracht regel optie uitvoert op de data base van uw productie site, wordt de site database bijgewerkt en kan de site onbruikbaar worden weer gegeven.

#### <a name="usage"></a>Gebruik

Geef de exemplaar naam en de database naam voor de site database op. Als u alleen de database naam opgeeft, gebruikt Setup de naam van de standaard instantie.  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

Voer een upgrade zonder toezicht van een site uit. Geef de product code op, inclusief de streepjes`-`(). Geef ook het pad op naar de eerder gedownloade vereiste bestanden voor de installatie.  

Zie het [Download programma](setup-downloader.md)voor meer informatie over de vereiste bestanden voor de installatie.  

#### <a name="usage"></a>Gebruik

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

Een installatie zonder toezicht uitvoeren. Gebruik deze optie om een installatie-initialisatie bestand te gebruiken. Zie [sites installeren met een opdracht regel](use-a-command-line-to-install-sites.md)voor meer informatie over het uitvoeren van installatie zonder toezicht.  

#### <a name="usage"></a>Gebruik

`/SCRIPT <setup script path>`

### `/SDKINST`

Installeer de SMS-provider op de opgegeven computer. Geef de Fully Qualified Domain Name (FQDN) voor de computer van de SMS-provider op. Zie voor meer informatie over de SMS-provider [plannen voor de SMS-provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="usage"></a>Gebruik

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

Verwijder de SMS-provider op de opgegeven computer. Geef de FQDN-naam voor de computer van de SMS-provider op.  

#### <a name="usage"></a>Gebruik

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

De talen beheren die zijn geïnstalleerd op een eerder geïnstalleerde site. Geef de locatie op voor het taal script bestand dat de taal instellingen bevat. Zie de sectie [opdracht regel opties voor het beheren van talen](#bkmk_Lang) voor meer informatie.  

#### <a name="usage"></a>Gebruik

`/MANAGELANGS <Language script path>`


## <a name="command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a>Opdracht regel opties voor het beheren van talen

### <a name="identification"></a>Identificatie

- **Naam sleutel:** Action  

    - **Vereist:** ja  

    - **Waarden:**`ManageLanguages`  

    - **Details:** Beheert de server-, client-en Mobile client-taal ondersteuning op een site.  

### <a name="options"></a>Opties

- **Sleutel naam:** AddServerLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee geeft u de server talen op die beschikbaar zijn voor de Configuration Manager-console,-rapporten en-Configuration Manager-objecten. Engels is standaard beschikbaar.  

- **Sleutel naam:** AddClientLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee geeft u de talen op die beschikbaar zijn voor client computers. Engels is standaard beschikbaar.  

- **Sleutel naam:** DeleteServerLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee geeft u de talen op die u wilt verwijderen en die niet langer beschikbaar zijn voor de Configuration Manager-console,-rapporten en-Configuration Manager objecten. Engels is standaard beschikbaar, u kunt dit niet verwijderen.  

- **Sleutel naam:** DeleteClientLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee geeft u de talen op die moeten worden verwijderd en die niet meer beschikbaar zijn voor client computers. Engels is standaard beschikbaar, u kunt dit niet verwijderen.  

- **Sleutel naam:** MobileDeviceLanguage  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee wordt aangegeven of de talen van de client voor mobiele apparaten zijn geïnstalleerd.  

- **Sleutelnaam:** PrerequisiteComp  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Downloaden  

        - `1`= Al gedownload  

    - **Details:** Hiermee geeft u op of de vereiste bestanden voor de installatie al zijn gedownload. Als u bijvoorbeeld een waarde van `0`gebruikt, worden de bestanden door Setup gedownload.  

- **Sleutelnaam:** PrerequisitePath  

    - **Vereist:** ja  

    - **Waarden:** <*pad naar vereiste bestanden instellen*>  

    - **Details:** Hiermee geeft u het pad op naar de vereiste bestanden voor de installatie. Afhankelijk van de waarde van **PrerequisiteComp** , gebruikt Setup dit pad om gedownloade bestanden op te slaan of om eerder gedownloade bestanden te zoeken.  


## <a name="unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a>Script bestand sleutels voor installatie zonder toezicht

Gebruik de volgende secties om u te helpen bij het maken van een script voor installatie zonder toezicht. De lijsten worden weer gegeven:

- De beschik bare installatie script sleutels en de bijbehorende waarden
- Als ze vereist zijn
- Van welk type installatie ze worden gebruikt
- Een korte beschrijving van de sleutel

### <a name="unattended-install-for-a-central-administration-site-cas"></a>Installatie zonder toezicht voor een centrale beheer site (CAS)

Gebruik de volgende informatie om een certificerings instantie te installeren met behulp van een script bestand voor installatie zonder toezicht.  

#### <a name="identification"></a>Identificatie

- **Naam sleutel:** Action  

    - **Vereist:** ja  

    - **Waarden:**`InstallCAS`  

    - **Details:** Hiermee installeert u een certificerings instantie.  

- **Sleutel naam:** CDLatest  

    - **Vereist:** Ja, alleen wanneer media vanaf de CD worden gebruikt. Meest recente map.

    - **Gegevens**

        - `1`= u gebruikt media vanaf CD. Jongste

        - Een andere waarde dan 1 = u gebruikt geen CD. Nieuwste media

    - **Details:** Wanneer u een primaire site of certificerings instantie installeert of herstelt, en u Setup uitvoert vanaf de CD. De meest recente map, voeg deze sleutel en waarde toe. Met deze waarde wordt de installatie van de media van de CD omgevormd. Jongste.

#### <a name="options"></a>Opties

- **Sleutelnaam:** ProductID  

    - **Vereist:** ja  

    - **Gegevens**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= een geldige product code met streepjes

        - `Eval`= Installeer de evaluatie versie van Configuration Manager

    - **Details:** Hiermee geeft u de product code voor de Configuration Manager-installatie, inclusief de streepjes.

- **Sleutelnaam:** SiteCode  

    - **Vereist:** ja  

    - **Waarden:** <*site code*>, bijvoorbeeld`ABC`

    - **Details:** Hiermee geeft u drie alfanumerieke tekens op die de site in uw hiërarchie op unieke wijze identificeren.  

- **Sleutel naam:** Site naam  

    - **Vereist:** ja  

    - **Waarden:** <*site naam*>  

    - **Details:** Hiermee geeft u de naam op voor deze site.  

- **Sleutelnaam:** SMSInstallDir  

    - **Vereist:** ja  

    - **Waarden:** <*installatiepad Configuration Manager*>  

    - **Details:** Hiermee geeft u de installatiemap op voor de Configuration Manager-programma bestanden.  

- **Sleutelnaam:** SDKServer  

    - **Vereist:** ja  

    - **Waarden:** <*FQDN* van de SMS-provider>  

    - **Details:** hiermee geeft u de FDQN op voor de server die als host fungeert voor de SMS-provider. U kunt bijkomende SMS-providers voor de site configureren na de eerste installatie.  

- **Sleutelnaam:** PrerequisiteComp  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Downloaden  

        - `1`= Al gedownload  

    - **Details:** Hiermee geeft u op of de vereiste bestanden voor de installatie al zijn gedownload. Als u bijvoorbeeld een waarde van `0`gebruikt, worden de bestanden door Setup gedownload.  

- **Sleutelnaam:** PrerequisitePath  

    - **Vereist:** ja  

    - **Waarden:** <*pad naar vereiste bestanden instellen*>  

    - **Details:** Hiermee geeft u het pad op naar de vereiste bestanden voor de installatie. Afhankelijk van de waarde van **PrerequisiteComp** , gebruikt Setup dit pad om gedownloade bestanden op te slaan of om eerder gedownloade bestanden te zoeken.  

- **Sleutelnaam:** AdminConsole  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of de Configuration Manager-console moet worden geïnstalleerd.  

- **Sleutelnaam:** JoinCEIP  

    > [!Note]  
    > Vanaf Configuration Manager versie 1802 wordt de functie CEIP verwijderd uit het product.

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet toevoegen  

        - `1`= Lid worden  

    - **Details:** Hiermee wordt opgegeven of de Customer Experience Improvement Program (CEIP) moet worden toegevoegd.  

- **Sleutel naam:** AddServerLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee geeft u de server talen op die beschikbaar zijn voor de Configuration Manager-console,-rapporten en-Configuration Manager-objecten. Engels is standaard beschikbaar.  

- **Sleutel naam:** AddClientLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee geeft u de talen op die beschikbaar zijn voor client computers. Engels is standaard beschikbaar.  

- **Sleutel naam:** DeleteServerLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee wijzigt u een site nadat deze is geïnstalleerd. Hiermee geeft u de talen op die u wilt verwijderen en die niet langer beschikbaar zijn voor de Configuration Manager-console,-rapporten en-Configuration Manager objecten. Engels is standaard beschikbaar, u kunt dit niet verwijderen.  

- **Sleutel naam:** DeleteClientLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee wijzigt u een site nadat deze is geïnstalleerd. Hiermee geeft u de talen op die moeten worden verwijderd en die niet meer beschikbaar zijn voor client computers. Engels is standaard beschikbaar, u kunt dit niet verwijderen.  

- **Sleutel naam:** MobileDeviceLanguage  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee wordt aangegeven of de talen van de client voor mobiele apparaten zijn geïnstalleerd.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Sleutelnaam:** SQLServerName  

    - **Vereist:** ja  

    - **Waarden:** <*SQL Server-naam*>  

    - **Details:** Hiermee geeft u de naam op van de server of het geclusterde exemplaar waarop SQL Server worden uitgevoerd om de site database te hosten.  

- **Sleutelnaam:** DatabaseName  

    - **Vereist:** ja  

    - **Waarden:** <naam van*site database*> of <*exemplaar naam*>\\<*site database naam*>  

    - **Details:** Hiermee geeft u de naam op van de SQL Server Data Base die moet worden gemaakt of de SQL Server-Data Base die moet worden gebruikt wanneer Setup de CAS-data base installeert.  

        > [!IMPORTANT]  
        > Als u het standaard exemplaar niet gebruikt, geeft u de exemplaar naam en de naam van de site database op.  

- **Sleutelnaam:** SQLSSBPort  

    - **Vereist:** nee  

    - **Waarden:** <*SSB-poort nummer*>  

    - **Details:** Hiermee geeft u de SQL Server Service Broker (SSB) poort op die SQL Server gebruikt. SSB maakt standaard gebruik van TCP-poort 4022, maar u kunt een andere poort gebruiken.  

- **Sleutel naam:** SQLDataFilePath  

    - **Vereist:** nee  

    - **Waarden:** <*pad naar het bestand data base. mdb*>  

    - **Details:** Hiermee geeft u een alternatieve locatie op voor het maken van het data base. mdb-bestand.  

- **Sleutel naam:** SQLLogFilePath  

    - **Vereist:** nee  

    - **Waarden:** <*pad naar het bestand data base. ldf*>  

    - **Details:** Hiermee geeft u een alternatieve locatie op voor het maken van het. LDF-bestand van de data base.  

#### <a name="cloudconnectoroptions"></a>Hierarchyoptions

- **Sleutel naam:** Cloud connector  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of een service verbindings punt moet worden geïnstalleerd op deze site. Omdat u het service aansluitpunt alleen op de site op het hoogste niveau van een hiërarchie kunt installeren, stelt u `1` deze waarde in op voor een onderliggende primaire site.  

- **Sleutel naam:** CloudConnectorServer  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Waarden:** <FQDN van de server voor het*service verbindings punt*>  

    - **Details:** Hiermee geeft u de FQDN-naam op van de server die als host fungeert voor de site systeemrol voor het service aansluitpunt.  

- **Sleutel naam:** UseProxy  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of het service verbindings punt een proxy server gebruikt.  

- **Sleutel naam:** Proxynaam  

    - **Vereist:** Vereist wanneer **UseProxy** gelijk is aan 1  

    - **Waarden:** <*FQDN van proxy server*>  

    - **Details:** Hiermee geeft u de FQDN op van de proxy server die door het service aansluitpunt wordt gebruikt.  

- **Sleutel naam:** Proxy port  

    - **Vereist:** Vereist wanneer **UseProxy** gelijk is aan 1  

    - **Waarden:** <*poort nummer*>  

    - **Details:** Hiermee geeft u het poort nummer op dat moet worden gebruikt voor de Proxy poort.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Sleutel naam:** SAActive

    - **Vereist:** nee

    - **Gegevens**

        - `0`= U hebt geen Software Assurance

        - `1`= Software Assurance is actief

    - **Details:** Geef op of u actieve Software Assurance hebt. Zie [Veelgestelde vragen over producten en licenties](../../../understand/product-and-licensing-faq.md)voor meer informatie.

- **Sleutel naam:** CurrentBranch

    - **Vereist:** nee

    - **Gegevens**

        - `0`= De LTSB installeren

        - `1`= Huidige branch installeren

    - **Details:** Geef op of u Configuration Manager huidige vertakking of Long-term Servicing Branch (LTSB) wilt gebruiken. Zie [welke vertakking van Configuration Manager moet ik gebruiken?](../../../understand/which-branch-should-i-use.md)voor meer informatie.

### <a name="unattended-install-for-a-primary-site"></a>Installatie zonder toezicht voor een primaire site

Gebruik de volgende informatie voor het installeren van een primaire site met behulp van een script bestand voor installatie zonder toezicht.  

#### <a name="identification"></a>Identificatie

- **Naam sleutel:** Action  

    - **Vereist:** ja  

    - **Waarden:**`InstallPrimarySite`  

    - **Details:** Hiermee installeert u een primaire site.  

- **Sleutel naam:** CDLatest  

    - **Vereist:** Ja, alleen wanneer media vanaf de CD worden gebruikt. Meest recente map.

    - **Gegevens**

        - `1`= u gebruikt media vanaf CD. Jongste

        - Een andere waarde dan 1 = u gebruikt geen CD. Nieuwste media

    - **Details:** Wanneer u een primaire site of certificerings instantie installeert of herstelt, en u Setup uitvoert vanaf de CD. De meest recente map, voeg deze sleutel en waarde toe. Met deze waarde wordt de installatie van de media van de CD omgevormd. Jongste.

#### <a name="options"></a>Opties

- **Sleutelnaam:** ProductID  

    - **Vereist:** ja  

    - **Gegevens**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= een geldige product code met streepjes

        - `Eval`= Installeer de evaluatie versie van Configuration Manager

    - **Details:** Hiermee geeft u de product code voor de Configuration Manager-installatie, inclusief de streepjes.

- **Sleutelnaam:** SiteCode  

    - **Vereist:** ja  

    - **Waarden:** <*site code*>  

    - **Details:** Hiermee geeft u drie alfanumerieke tekens op die de site in uw hiërarchie op unieke wijze identificeren.  

- **Sleutelnaam:** SiteName  

    - **Vereist:** ja  

    - **Waarden:** <*site naam*>  

    - **Details:** Hiermee geeft u de naam op voor deze site.  

- **Sleutelnaam:** SMSInstallDir  

    - **Vereist:** ja  

    - **Waarden:** <*installatiepad Configuration Manager*>

    - **Details:** Hiermee geeft u de installatiemap op voor de Configuration Manager-programma bestanden.  

- **Sleutelnaam:** SDKServer  

    - **Vereist:** ja  

    - **Waarden:** <*FQDN* van de SMS-provider>  

    - **Details:** hiermee geeft u de FDQN op voor de server die als host fungeert voor de SMS-provider. U kunt bijkomende SMS-providers voor de site configureren na de eerste installatie.  

- **Sleutelnaam:** PrerequisiteComp  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Downloaden  

        - `1`= Al gedownload  

    - **Details:** Hiermee geeft u op of de vereiste bestanden voor de installatie al zijn gedownload. Als u bijvoorbeeld een waarde van `0`gebruikt, worden de bestanden door Setup gedownload.  

- **Sleutelnaam:** PrerequisitePath  

    - **Vereist:** ja  

    - **Waarden:** <*pad naar vereiste bestanden instellen*>  

    - **Details:** Hiermee geeft u het pad op naar de vereiste bestanden voor de installatie. Afhankelijk van de waarde van **PrerequisiteComp** , gebruikt Setup dit pad om gedownloade bestanden op te slaan of om eerder gedownloade bestanden te zoeken.  

- **Sleutelnaam:** AdminConsole  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of de Configuration Manager-console moet worden geïnstalleerd.  

- **Sleutelnaam:** JoinCEIP  

    > [!Note]  
    > Vanaf Configuration Manager versie 1802 wordt de functie CEIP verwijderd uit het product.

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet toevoegen  

        - `1`= Lid worden  

    - **Details:** Hiermee wordt aangegeven of het CEIP moet worden toegevoegd.  

- **Sleutel naam:** ManagementPoint  

    - **Vereist:** nee  

    - **Waarden:** <*FQDN van de site server van het beheer punt*>  

    - **Details:** Hiermee geeft u de FQDN-naam op van de server die als host fungeert voor de site systeemrol van het beheer punt.  

- **Sleutel naam:** ManagementPointProtocol  

    - **Vereist:** nee  

    - **Waarden:** `HTTPS` of`HTTP`  

    - **Details:** Hiermee geeft u het protocol op dat voor het beheer punt moet worden gebruikt.  

- **Sleutel naam:** DistributionPoint  

    - **Vereist:** nee  

    - **Waarden:** <*FQDN van de site server van het distributie punt*>  

    - **Details:** Hiermee geeft u de FQDN-naam op van de server die als host fungeert voor de site systeemrol van het distributie punt.  

- **Sleutel naam:** DistributionPointProtocol  

    - **Vereist:** nee  

    - **Waarden:** `HTTPS` of`HTTP`  

    - **Details:** Hiermee geeft u het protocol op dat voor het distributie punt moet worden gebruikt.  

- **Sleutel naam:** RoleCommunicationProtocol  

    - **Vereist:** ja  

    - **Waarden:** `EnforceHTTPS` of`HTTPorHTTPS`  

    - **Details:** Hiermee geeft u op of alle site systemen zo moeten worden geconfigureerd dat alleen HTTPS-communicatie van clients wordt geaccepteerd, of dat de communicatie methode voor elke site systeemrol moet worden geconfigureerd. Wanneer u selecteert `EnforceHTTPS`, moeten clients een geldig PKI-certificaat (Public Key Infrastructure) voor client verificatie hebben.  

- **Sleutel naam:** ClientsUsePKICertificate  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet gebruiken  

        - `1`= Gebruik  

    - **Details:** Hiermee wordt aangegeven of clients een PKI-client certificaat gebruiken om te communiceren met site systeem rollen.  

- **Sleutel naam:** AddServerLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee geeft u de server talen op die beschikbaar zijn voor de Configuration Manager-console,-rapporten en-Configuration Manager-objecten. Engels is standaard beschikbaar.  

- **Sleutel naam:** AddClientLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee geeft u de talen op die beschikbaar zijn voor client computers. Engels is standaard beschikbaar.  

- **Sleutel naam:** DeleteServerLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee wijzigt u een site nadat deze is geïnstalleerd. Hiermee geeft u de talen op die u wilt verwijderen en die niet langer beschikbaar zijn voor de Configuration Manager-console,-rapporten en-Configuration Manager objecten. Engels is standaard beschikbaar, u kunt dit niet verwijderen.  

- **Sleutel naam:** DeleteClientLanguages  

    - **Vereist:** nee  

    - **Waarden:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK of ZHH  

    - **Details:** Hiermee wijzigt u een site nadat deze is geïnstalleerd. Hiermee geeft u de talen op die moeten worden verwijderd en die niet meer beschikbaar zijn voor client computers. Engels is standaard beschikbaar, u kunt dit niet verwijderen.  

- **Sleutel naam:** MobileDeviceLanguage  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee wordt aangegeven of de talen van de client voor mobiele apparaten zijn geïnstalleerd.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Sleutelnaam:** SQLServerName  

    - **Vereist:** ja  

    - **Waarden:** <*SQL Server-naam*>  

    - **Details:** Hiermee geeft u de naam op van de server of het geclusterde exemplaar waarop SQL Server worden uitgevoerd om de site database te hosten.  

- **Sleutelnaam:** DatabaseName  

    - **Vereist:** ja  

    - **Waarden:** <naam van*site database*> of <*exemplaar naam*>\\<*site database naam*>  

    - **Details:** Hiermee geeft u de naam op van de SQL Server Data Base die moet worden gemaakt of de SQL Server-Data Base die moet worden gebruikt bij de installatie van de primaire site database.  

        > [!IMPORTANT]  
        > Als u het standaard exemplaar niet gebruikt, geeft u de exemplaar naam en de naam van de site database op.  

- **Sleutelnaam:** SQLSSBPort  

    - **Vereist:** nee  

    - **Waarden:** <*SSB-poort nummer*>  

    - **Details:** Hiermee geeft u de SSB-poort op die SQL Server gebruikt. SSB maakt standaard gebruik van TCP-poort 4022, maar u kunt een andere poort gebruiken.  

- **Sleutel naam:** SQLDataFilePath  

    - **Vereist:** nee  

    - **Waarden:** <*pad naar het bestand data base. mdb*>  

    - **Details:** Hiermee geeft u een alternatieve locatie op voor het maken van het data base. mdb-bestand.  

- **Sleutel naam:** SQLLogFilePath  

    - **Vereist:** nee  

    - **Waarden:** <*pad naar het bestand data base. ldf*>  

    - **Details:** Hiermee geeft u een alternatieve locatie op voor het maken van het. LDF-bestand van de data base.  

#### <a name="hierarchyexpansionoption"></a>HierarchyExpansionOption

- **Sleutelnaam:** CCARSiteServer  

    - **Vereist:** nee  

    - **Waarden:** <*FQDN van centrale beheer site*>  

    - **Details:** Hiermee geeft u de certificerings instanties op waaraan een primaire site wordt gekoppeld wanneer deze lid wordt van de Configuration Manager-hiërarchie. Geef de CA'S op tijdens de installatie.  

- **Sleutelnaam:** CASRetryInterval  

    - **Vereist:** nee  

    - **Waarden:** <*interval in minuten*>  

    - **Details:** Hiermee geeft u het interval voor opnieuw proberen in minuten om een verbinding met de CAS te proberen nadat de verbinding is mislukt. Als de verbinding met de certificerings instantie mislukt, wacht de primaire site bijvoorbeeld het aantal minuten dat u opgeeft voor de waarde **CASRetryInterval** en probeert de verbinding vervolgens opnieuw.  

- **Sleutelnaam:** WaitForCASTimeout  

    - **Vereist:** nee  

    - **Waarden:** <*time-out in minuten van 0 tot 100*>  

    - **Details:** Hiermee geeft u de maximale time-outwaarde (in minuten) voor een primaire site om verbinding te maken met de CAS. Als een primaire site bijvoorbeeld geen verbinding kan maken met een certificerings instantie, probeert de primaire site opnieuw de verbinding met de CAS op basis van de **CASRetryInterval** -waarde tot de **WaitForCASTimeout** -periode is bereikt. U kunt een waarde opgeven van `0` tot `100`.  

#### <a name="cloudconnectoroptions"></a>Hierarchyoptions

- **Sleutel naam:** Cloud connector  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of een service verbindings punt moet worden geïnstalleerd op deze site. Omdat u het service aansluitpunt alleen op de site op het hoogste niveau van een hiërarchie kunt installeren, stelt u `0` deze waarde in op voor een onderliggende primaire site.  

- **Sleutel naam:** CloudConnectorServer  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Waarden:** <FQDN van de server voor het*service verbindings punt*\>  

    - **Details:** Hiermee geeft u de FQDN-naam op van de server die als host fungeert voor de site systeemrol voor het service aansluitpunt.  

- **Sleutel naam:** UseProxy  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of het service verbindings punt een proxy server gebruikt.  

- **Sleutel naam:** Proxynaam  

    - **Vereist:** Vereist wanneer **UseProxy** gelijk is aan 1  

    - **Waarden:** <*FQDN van proxy server*>  

    - **Details:** Hiermee geeft u de FQDN op van de proxy server die door het service aansluitpunt wordt gebruikt.  

- **Sleutel naam:** Proxy port  

    - **Vereist:** Vereist wanneer **UseProxy** gelijk is aan 1  

    - **Waarden:** <*poort nummer*>  

    - **Details:** Hiermee geeft u het poort nummer op dat moet worden gebruikt voor de Proxy poort.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Sleutel naam:** SAActive

    - **Vereist:** nee

    - **Gegevens**

        - `0`= U hebt geen Software Assurance

        - `1`= Software Assurance is actief

    - **Details:** Geef op of u actieve Software Assurance hebt. Zie [Veelgestelde vragen over producten en licenties](../../../understand/product-and-licensing-faq.md)voor meer informatie.

- **Sleutel naam:** CurrentBranch

    - **Vereist:** nee

    - **Gegevens**

        - `0`= De LTSB installeren

        - `1`= Huidige branch installeren

    - **Details:** Geef op of u Configuration Manager huidige vertakking of Long-term Servicing Branch (LTSB) wilt gebruiken. Zie [welke vertakking van Configuration Manager moet ik gebruiken?](../../../understand/which-branch-should-i-use.md)voor meer informatie.

### <a name="unattended-recovery-for-a-cas"></a>Herstel zonder toezicht voor een certificerings instantie

Gebruik de volgende informatie om een certificerings instantie te herstellen met een script bestand voor installatie zonder toezicht.  

#### <a name="identification"></a>Identificatie

- **Naam sleutel:** Action  

    - **Vereist:** ja  

    - **Waarden:**`RecoverCCAR`  

    - **Details:** Hiermee herstelt u een certificerings instantie.  

- **Sleutel naam:** CDLatest  

    - **Vereist:** Ja, alleen wanneer media vanaf de CD worden gebruikt. Meest recente map.

    - **Gegevens**

        - `1`= u gebruikt media vanaf CD. Jongste

        - Een andere waarde dan 1 = u gebruikt geen CD. Nieuwste media

    - **Details:** Wanneer u een primaire site of certificerings instantie installeert of herstelt, en u Setup uitvoert vanaf de CD. De meest recente map, voeg deze sleutel en waarde toe. Met deze waarde wordt de installatie van de media van de CD omgevormd. Jongste.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Sleutelnaam:** ServerRecoveryOptions  

    - **Vereist:** ja  

    - **Gegevens**

        - `1`= Site server en SQL Server herstellen

        - `2`= Alleen site server herstellen

        - `4`= Alleen SQL Server herstellen  

    - **Details:** Hiermee geeft u op of het installatie programma de site server, SQL Server of beide moet herstellen. De volgende opties zijn ook vereist op basis van de opgegeven waarde:  

        - **1** of **2**: als u de site wilt herstellen met behulp van een back-up van een site, geeft u een waarde op voor **sleutel siteserverbackuplocation**. Als u geen waarde opgeeft, wordt de site door Setup opnieuw geïnstalleerd zonder dat deze wordt teruggezet vanuit een back-upset.  

        - **4**: de **sleutel backuplocation** -sleutel is vereist wanneer u een waarde van **10** configureert voor de **Database Recovery options** -sleutel, waarmee u de site database kunt herstellen vanuit een back-up.  

- **Sleutelnaam:** DatabaseRecoveryOptions  

    - **Vereist:** Deze sleutel is vereist wanneer de instelling **Server Recovery options** een waarde heeft van **1** of **4**.  

    - **Gegevens**

        - `10`= De site database herstellen vanuit een back-up.  

        - `20`= Een site database gebruiken die u hand matig hebt hersteld met een andere methode.  

        - `40`= Een nieuwe data base maken voor de site. Gebruik deze optie wanneer er geen back-up van de site database beschikbaar is. De site herstelt globale en site gegevens via replicatie vanaf andere sites.  

        - `80`= Database herstel overs Laan.  

    - **Details:** Hiermee geeft u op hoe de site database in SQL Server wordt hersteld door Setup.  

- **Sleutelnaam:** ReferenceSite  

    - **Vereist:** Deze sleutel is vereist wanneer de instelling **Database Recovery options** een waarde heeft van **40**.  

    - **Waarden:** <*referentie site-FQDN*>  

    - **Details:** Als de back-up van de data base ouder is dan de Bewaar periode voor het bijhouden van wijzigingen of wanneer u de site herstelt zonder een back-up, geeft u de primaire referentie site op die de certificerings instantie gebruikt om globale gegevens te herstellen.  

        Wanneer u geen referentie site opgeeft en de back-up ouder is dan de Bewaar periode voor het bijhouden van wijzigingen, worden alle primaire sites opnieuw geïnitialiseerd met de herstelde gegevens van de certificerings instanties.  

        Wanneer u geen referentie site opgeeft en de back-up valt binnen de Bewaar periode voor het bijhouden van wijzigingen, worden alleen de wijzigingen die zijn aangebracht na de back-up gerepliceerd van primaire sites. Wanneer er conflicterende wijzigingen van verschillende primaire sites zijn, gebruikt de CAS de eerste die het ontvangt.  

- **Sleutelnaam:** SiteServerBackupLocation  

    - **Vereist:** nee  

    - **Waarden:** <*pad naar back-upset van site server*>  

    - **Details:** hiermee geeft u het pad op naar de back-upset van de siteserver. Deze sleutel is optioneel wanneer de instelling **ServerRecoveryOptions** een waarde heeft van **1** of **2**. Geef een waarde op voor de sleutel **SiteServerBackupLocation** om de site te herstellen met behulp van een siteback-up. Als u geen waarde opgeeft, wordt de site door Setup opnieuw geïnstalleerd zonder dat deze wordt teruggezet vanuit een back-upset.  

- **Sleutelnaam:** BackupLocation  

    - **Vereist:** Deze sleutel is vereist wanneer u een waarde van **1** of **4** configureert voor de sleutel **Server Recovery options** en u een waarde van **10** configureert voor de sleutel **Database Recovery options** .  

    - **Waarden:** <*pad naar de back-upset van de site database*>  

    - **Details:** hiermee geeft u het pad op naar de back-upset van de sitedatabase.  

#### <a name="options"></a>Opties

- **Sleutelnaam:** ProductID  

    - **Vereist:** ja  

    - **Gegevens**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= een geldige product code met streepjes

        - `Eval`= Installeer de evaluatie versie van Configuration Manager

    - **Details:** Hiermee geeft u de product code voor de Configuration Manager-installatie, inclusief de streepjes.

- **Sleutelnaam:** SiteCode  

    - **Vereist:** ja  

    - **Waarden:** <*site code*>  

    - **Details:** Hiermee geeft u drie alfanumerieke tekens op die de site in uw hiërarchie op unieke wijze identificeren. Geef de site code op die de site heeft gebruikt vóór de fout.

- **Sleutelnaam:** SiteName  

    - **Vereist:** nee  

    - **Waarden:** <*site naam*>  

    - **Details:** Hiermee geeft u de naam op voor deze site.  

- **Sleutelnaam:** SMSInstallDir  

    - **Vereist:** ja  

    - **Waarden:** <*installatiepad Configuration Manager*>  

    - **Details:** Hiermee geeft u de installatiemap op voor de Configuration Manager-programma bestanden.  

- **Sleutelnaam:** SDKServer  

    - **Vereist:** ja  

    - **Waarden:** <*FQDN* van de SMS-provider>  

    - **Details:** Hiermee geeft u de FQDN-naam op van de server die als host fungeert voor de SMS-provider. Geef de server op die de SMS-provider heeft gehost vóór de fout.  

        Na de eerste installatie kunt u aanvullende SMS-providers voor de site configureren. Zie voor meer informatie over de SMS-provider [plannen voor de SMS-provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Sleutelnaam:** PrerequisiteComp  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Downloaden  

        - `1`= Al gedownload  

    - **Details:** Hiermee geeft u op of de vereiste bestanden voor de installatie al zijn gedownload. Als u bijvoorbeeld de waarde **0**gebruikt, downloadt Setup de bestanden.  

- **Sleutelnaam:** PrerequisitePath  

    - **Vereist:** ja  

    - **Waarden:** <*pad naar vereiste bestanden instellen*>  

    - **Details:** Hiermee geeft u het pad op naar de vereiste bestanden voor de installatie. Afhankelijk van de waarde van **PrerequisiteComp** , gebruikt Setup dit pad om gedownloade bestanden op te slaan of om eerder gedownloade bestanden te zoeken.  

- **Sleutelnaam:** AdminConsole  

    - **Vereist:** Deze sleutel is vereist, behalve wanneer de instelling **Server Recovery options** een waarde heeft van **4**.  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of de Configuration Manager-console moet worden geïnstalleerd.  

- **Sleutelnaam:** JoinCEIP  

    > [!Note]  
    > Vanaf Configuration Manager versie 1802 wordt de functie CEIP verwijderd uit het product.

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet toevoegen  

        - `1`= Lid worden  

    - **Details:** Hiermee wordt aangegeven of het CEIP moet worden toegevoegd.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Sleutelnaam:** SQLServerName  

    - **Vereist:** ja  

    - **Waarden:** <*SQL Server-naam*>  

    - **Details:** Hiermee geeft u de naam van de server of het geclusterde exemplaar waarop SQL Server wordt uitgevoerd en die als host fungeert voor de site database. Geef de server op die de site database heeft gehost vóór de fout.  

- **Sleutelnaam:** DatabaseName  

    - **Vereist:** ja  

    - **Waarden:** <naam van*site database*> of <*exemplaar naam*>\\<*site database naam*>  

    - **Details:** Hiermee geeft u de naam op van de SQL Server-Data Base die moet worden gemaakt of de SQL Server-Data Base die moet worden gebruikt bij het installeren van de CAS Geef dezelfde database naam op die werd gebruikt vóór de fout.  

        > [!IMPORTANT]  
        > Als u het standaard exemplaar niet gebruikt, geeft u de exemplaar naam en de naam van de site database op.  

- **Sleutelnaam:** SQLSSBPort  

    - **Vereist:** ja  

    - **Waarden:** <*SSB-poort nummer*>  

    - **Details:** Hiermee geeft u de SSB-poort op die SQL Server gebruikt. SSB maakt standaard gebruik van TCP-poort 4022. Geef dezelfde SSB-poort op die voor de fout is gebruikt.  

- **Sleutel naam:** SQLDataFilePath  

    - **Vereist:** nee  

    - **Waarden:** <*pad naar het bestand data base. mdb*>  

    - **Details:** Hiermee geeft u een alternatieve locatie op voor het maken van het data base. mdb-bestand.  

- **Sleutel naam:** SQLLogFilePath  

    - **Vereist:** nee  

    - **Waarden:** <*pad naar het bestand data base. ldf*>  

    - **Details:** Hiermee geeft u een alternatieve locatie op voor het maken van het. LDF-bestand van de data base.  

#### <a name="cloudconnectoroptions"></a>Hierarchyoptions

- **Sleutel naam:** Cloud connector  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of een service verbindings punt moet worden geïnstalleerd op deze site. Omdat u het service aansluitpunt alleen op de site op het hoogste niveau van een hiërarchie kunt installeren, moet deze waarde **0** zijn voor een onderliggende primaire site.  

- **Sleutel naam:** CloudConnectorServer  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Waarden:** <FQDN van de server voor het*service verbindings punt*>  

    - **Details:** Hiermee geeft u de FQDN-naam op van de server die als host fungeert voor de site systeemrol voor het service aansluitpunt.  

- **Sleutel naam:** UseProxy  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of het service verbindings punt een proxy server gebruikt.  

- **Sleutel naam:** Proxynaam  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Waarden:** <*FQDN van proxy server*>  

    - **Details:** Hiermee geeft u de FQDN op van de proxy server die door het service aansluitpunt wordt gebruikt.  

- **Sleutel naam:** Proxy port  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Waarden:** <*poort nummer*>  

    - **Details:** Hiermee geeft u het poort nummer op dat moet worden gebruikt voor de Proxy poort.  

### <a name="unattended-recovery-for-a-primary-site"></a>Herstel zonder toezicht voor een primaire site

Gebruik de volgende informatie voor het herstellen van een primaire site met behulp van een script bestand voor installatie zonder toezicht.  

#### <a name="identification"></a>Identificatie

- **Naam sleutel:** Action  

    - **Vereist:** ja  

    - **Waarden:**`RecoverPrimarySite`  

    - **Details:** Hiermee herstelt u een primaire site.  

- **Sleutel naam:** CDLatest  

    - **Vereist:** Ja, alleen wanneer media vanaf de CD worden gebruikt. Meest recente map.

    - **Gegevens**

        - `1`= u gebruikt media vanaf CD. Jongste

        - Een andere waarde dan 1 = u gebruikt geen CD. Nieuwste media

    - **Details:** Wanneer u een primaire site of certificerings instantie installeert of herstelt, en u Setup uitvoert vanaf de CD. De meest recente map, voeg deze sleutel en waarde toe. Met deze waarde wordt de installatie van de media van de CD omgevormd. Jongste.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Sleutelnaam:** ServerRecoveryOptions  

    - **Vereist:** ja  

    - **Gegevens**

        - `1`= Site server en SQL Server herstellen

        - `2`= Alleen site server herstellen

        - `4`= Alleen SQL Server herstellen  

    - **Details:** Hiermee geeft u op of het installatie programma de site server, SQL Server of beide moet herstellen. De volgende opties zijn ook vereist op basis van de opgegeven waarde:  

        - **1** of **2**: als u de site wilt herstellen met behulp van een back-up van een site, geeft u een waarde op voor **sleutel siteserverbackuplocation**. Als u geen waarde opgeeft, wordt de site door Setup opnieuw geïnstalleerd zonder dat deze wordt teruggezet vanuit een back-upset.  

        - **4**: de **sleutel backuplocation** -sleutel is vereist wanneer u een waarde van **10** configureert voor de **Database Recovery options** -sleutel, waarmee u de site database kunt herstellen vanuit een back-up.  

- **Sleutelnaam:** DatabaseRecoveryOptions  

    - **Vereist:** Deze sleutel is vereist wanneer de instelling **Server Recovery options** een waarde heeft van **1** of **4**.  

    - **Gegevens**

        - `10`= De site database herstellen vanuit een back-up.  

        - `20`= Een site database gebruiken die u hand matig hebt hersteld met een andere methode.  

        - `40`= Een nieuwe data base maken voor de site. Gebruik deze optie wanneer er geen back-up van de site database beschikbaar is. De site herstelt globale en site gegevens via replicatie vanaf andere sites.  

        - `80`= Database herstel overs Laan.  

    - **Details:** Hiermee geeft u op hoe de site database in SQL Server wordt hersteld door Setup.  

- **Sleutelnaam:** SiteServerBackupLocation  

    - **Vereist:** nee  

    - **Waarden:** <*pad naar back-upset van site server*>  

    - **Details:** hiermee geeft u het pad op naar de back-upset van de siteserver. Deze sleutel is optioneel wanneer de instelling **ServerRecoveryOptions** een waarde heeft van **1** of **2**. Geef een waarde op voor de sleutel **SiteServerBackupLocation** om de site te herstellen met behulp van een siteback-up. Als u geen waarde opgeeft, wordt de site door Setup opnieuw geïnstalleerd zonder dat deze wordt teruggezet vanuit een back-upset.  

- **Sleutelnaam:** BackupLocation  

    - **Vereist:** Deze sleutel is vereist wanneer u een waarde van **1** of **4** configureert voor de sleutel **Server Recovery options** en een waarde van **10** configureert voor de sleutel **Database Recovery options** .  

    - **Waarden:** <*pad naar de back-upset van de site database*>  

    - **Details:** hiermee geeft u het pad op naar de back-upset van de sitedatabase.  

#### <a name="options"></a>Opties

- **Sleutelnaam:** ProductID  

    - **Vereist:** ja  

    - **Gegevens**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= een geldige product code met streepjes

        - `Eval`= Installeer de evaluatie versie van Configuration Manager

    - **Details:** Hiermee geeft u de product code voor de Configuration Manager-installatie, inclusief de streepjes.

- **Sleutelnaam:** SiteCode  

    - **Vereist:** ja  

    - **Waarden:** <*site code*>  

    - **Details:** Hiermee geeft u drie alfanumerieke tekens op die de site in uw hiërarchie op unieke wijze identificeren. Geef de site code op die de site heeft gebruikt vóór de fout.

- **Sleutelnaam:** SiteName  

    - **Vereist:** nee  

    - **Waarden:** <*site naam*>  

    - **Details:** Hiermee geeft u de naam op voor deze site.  

- **Sleutelnaam:** SMSInstallDir  

    - **Vereist:** ja  

    - **Waarden:** <*installatiepad Configuration Manager*>  

    - **Details:** Hiermee geeft u de installatiemap op voor de Configuration Manager-programma bestanden.  

- **Sleutelnaam:** SDKServer  

    - **Vereist:** ja  

    - **Waarden:** <*FQDN* van de SMS-provider>  

    - **Details:** Hiermee geeft u de FQDN-naam op van de server die als host fungeert voor de SMS-provider. Geef de server op die de SMS-provider heeft gehost vóór de fout. Na de eerste installatie kunt u aanvullende SMS-providers voor de site configureren. Zie voor meer informatie over de SMS-provider [plannen voor de SMS-provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Sleutelnaam:** PrerequisiteComp  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Downloaden  

        - `1`= Al gedownload  

    - **Details:** Hiermee geeft u op of de vereiste bestanden voor de installatie al zijn gedownload. Als u bijvoorbeeld de waarde **0**gebruikt, downloadt Setup de bestanden.  

- **Sleutelnaam:** PrerequisitePath  

    - **Vereist:** ja  

    - **Waarden:** <*pad naar vereiste bestanden instellen*>  

    - **Details:** Hiermee geeft u het pad op naar de vereiste bestanden voor de installatie. Afhankelijk van de waarde van **PrerequisiteComp** , gebruikt Setup dit pad om gedownloade bestanden op te slaan of om eerder gedownloade bestanden te zoeken.  

- **Sleutelnaam:** AdminConsole  

    - **Vereist:** Deze sleutel is vereist, behalve wanneer de instelling **Server Recovery options** een waarde heeft van **4**.  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of de Configuration Manager-console moet worden geïnstalleerd.  

- **Sleutelnaam:** JoinCEIP  

    > [!Note]  
    > Vanaf Configuration Manager versie 1802 wordt de functie CEIP verwijderd uit het product.

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet toevoegen  

        - `1`= Lid worden  

    - **Details:** Hiermee wordt aangegeven of het CEIP moet worden toegevoegd.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Sleutelnaam:** SQLServerName  

    - **Vereist:** ja  

    - **Waarden:** <*SQL Server-naam*>  

    - **Details:** Hiermee geeft u de naam op van de server of het geclusterde exemplaar waarop SQL Server worden uitgevoerd om de site database te hosten. Geef de server op die de site database heeft gehost vóór de fout.  

- **Sleutelnaam:** DatabaseName  

    - **Vereist:** ja  

    - **Waarden:** <naam van*site database*> of <*exemplaar naam*>\\<*site database naam*>

    - **Details:** Hiermee geeft u de naam op van de SQL Server-Data Base die moet worden gemaakt of de SQL Server-Data Base die moet worden gebruikt bij het installeren van de CAS Geef dezelfde database naam op die werd gebruikt vóór de fout.  

        > [!IMPORTANT]  
        > Als u het standaard exemplaar niet gebruikt, geeft u de exemplaar naam en de naam van de site database op.  

- **Sleutelnaam:** SQLSSBPort  

    - **Vereist:** ja  

    - **Waarden:** <*SSB-poort nummer*>  

    - **Details:** Hiermee geeft u de SSB-poort op die SQL Server gebruikt. SSB maakt standaard gebruik van TCP-poort 4022. Geef dezelfde SSB-poort op die voor de fout is gebruikt.  

- **Sleutel naam:** SQLDataFilePath  

    - **Vereist:** nee  

    - **Waarden:** <*pad naar het bestand data base. mdb*>  

    - **Details:** Hiermee geeft u een alternatieve locatie op voor het maken van het data base. mdb-bestand.  

- **Sleutel naam:** SQLLogFilePath  

    - **Vereist:** nee  

    - **Waarden:** <*pad naar het bestand data base. ldf*>  

    - **Details:** Hiermee geeft u een alternatieve locatie op voor het maken van het. LDF-bestand van de data base.  

#### <a name="hierarchyexpansionoptions"></a>HierarchyExpansionOptions

- **Sleutelnaam:** CCARSiteServer  

    - **Vereist:** Details weer geven.  

    - **Waarden:** <*site code voor CAS*>  

    - **Details:** Hiermee geeft u de certificerings instanties op waaraan een primaire site wordt gekoppeld wanneer deze lid wordt van de Configuration Manager hiërarchie. Deze instelling is vereist als de primaire site is gekoppeld aan een certificerings instantie vóór de fout. Geef de site code op die voor de certificerings instantie is gebruikt vóór de fout.  

- **Sleutelnaam:** CASRetryInterval  

    - **Vereist:** nee  

    - **Waarden:** <*interval in minuten*>  

    - **Details:** Hiermee geeft u het interval voor opnieuw proberen in minuten om een verbinding met de CAS te proberen nadat de verbinding is mislukt. Als de verbinding met de certificerings instantie mislukt, wacht de primaire site bijvoorbeeld het aantal minuten dat u opgeeft voor de waarde **CASRetryInterval** en wordt de verbinding vervolgens opnieuw geprobeerd.  

- **Sleutelnaam:** WaitForCASTimeout  

    - **Vereist:** nee  

    - **Waarden:** <*time-out in minuten*>  

    - **Details:** Hiermee geeft u de maximale time-outwaarde (in minuten) voor een primaire site om verbinding te maken met de CAS. Als een primaire site bijvoorbeeld geen verbinding kan maken met een certificerings instantie, probeert de primaire site opnieuw de verbinding met de CAS op basis van de **CASRetryInterval** -waarde tot de **WaitForCASTimeout** -periode is bereikt. U kunt een waarde opgeven `0` voor. `100`  

#### <a name="cloudconnectoroptions"></a>Hierarchyoptions

- **Sleutel naam:** Cloud connector  

    - **Vereist:** ja  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of een service verbindings punt moet worden geïnstalleerd op deze site. Omdat u het service aansluitpunt alleen op de site op het hoogste niveau van een hiërarchie kunt installeren, moet deze `0` waarde voor een onderliggende primaire site zijn.  

- **Sleutel naam:** CloudConnectorServer  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Waarden:** <FQDN van de server voor het*service verbindings punt*>  

    - **Details:** Hiermee geeft u de FQDN-naam op van de server die als host fungeert voor de site systeemrol voor het service aansluitpunt.  

- **Sleutel naam:** UseProxy  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Gegevens**

        - `0`= Niet installeren  

        - `1`= Installeren  

    - **Details:** Hiermee geeft u op of het service verbindings punt een proxy server gebruikt.  

- **Sleutel naam:** Proxynaam  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Waarden:** <*FQDN van proxy server*>  

    - **Details:** Hiermee geeft u de FQDN op van de proxy server die door het service aansluitpunt wordt gebruikt.  

- **Sleutel naam:** Proxy port  

    - **Vereist:** Vereist wanneer **Cloud connector** gelijk is aan 1  

    - **Waarden:** <*poort nummer*>  

    - **Details:** Hiermee geeft u het poort nummer op dat moet worden gebruikt voor de Proxy poort.  

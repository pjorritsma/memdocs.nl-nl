---
title: Plannen voor de SMS-provider
titleSuffix: Configuration Manager
description: Meer informatie over de site systeemrol van de SMS-provider in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01ea9b089da3cfcfc3e8d23e7ad25d27ab2fec7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712552"
---
# <a name="plan-for-the-sms-provider"></a>Plannen voor de SMS-provider

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u Configuration Manager wilt beheren, gebruikt u een Configuration Manager-console die verbinding maakt met een exemplaar van de **SMS-provider**. Standaard wordt een SMS-provider geïnstalleerd op de site server wanneer u een centrale beheer site of primaire site installeert.

## <a name="about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a>Over de SMS-provider  

De SMS-provider is een Windows Management Instrumentation provider (WMI) die **Lees** -en **Schrijf** toegang toewijst aan de Configuration Manager-Data Base op een site.  

- Elke centrale beheersite of primaire site moet ten minste één SMS-provider bevatten. U kunt indien nodig aanvullende providers installeren.  

- De beveiligings groep **SMS admins** biedt toegang tot de SMS-provider. Configuration Manager maakt deze groep automatisch op de site server en op elke computer waarop u een exemplaar van de SMS-provider installeert. Zie [SMS-beheerders](accounts.md#sms-admins)voor meer informatie.  

- Secundaire sites bieden geen ondersteuning voor de functie SMS-provider.  

Configuration Manager gebruikers met beheerders rechten een SMS-provider gebruiken om toegang te krijgen tot gegevens die zijn opgeslagen in de-data base. Beheerders kunnen hiervoor gebruikmaken van de Configuration Manager-console, resource Explorer, hulpprogram ma's en aangepaste scripts. De SMS-provider communiceert niet met Configuration Manager-clients. Wanneer een Configuration Manager-console verbinding maakt met een site, vraagt deze WMI op de site server om een instantie te vinden van de te gebruiken SMS-provider.  

De SMS-provider helpt bij het afdwingen van Configuration Manager beveiliging. Het retourneert alleen de informatie die de console gebruiker mag weer geven.  

De SMS-provider biedt ook API-interoperabiliteits toegang via HTTPS, de **beheer service**genoemd. Deze REST API kan worden gebruikt in plaats van een aangepaste webservice om toegang te krijgen tot informatie van de site. Zie [Wat is de beheer service?](../../../develop/adminservice/overview.md)voor meer informatie.

> [!IMPORTANT]  
> Wanneer elk exemplaar van de SMS-provider voor een site offline is, kunnen Configuration Manager-consoles geen verbinding maken met de site.  

Zie [de SMS-provider beheren](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)voor meer informatie over het beheren van de SMS-provider.  

## <a name="installation-prerequisites"></a>Installatievereisten  

Ter ondersteuning van de SMS-provider moet de doel server voldoen aan de volgende vereisten:  

- In hetzelfde domein als de site server en de site database site systemen  

- Kan geen site systeemrol van een andere site hebben  

- Er kan geen SMS-provider van een site aanwezig zijn  

- Een ondersteunde versie van het besturings systeem uitvoeren  

- Ten minste 650 MB beschik bare schijf ruimte voor de ondersteuning van de Windows ADK-onderdelen. Zie [implementatie vereisten voor besturings systemen](#BKMK_WAIKforSMSProv)voor meer informatie over Windows ADk en de SMS-provider.  

- Voor de [beheer service](../../../develop/adminservice/overview.md) rest API:

  - .NET 4,5 of hoger

  - Windows Server Role **Web Server (IIS)** inschakelen

    > [!Note]  
    > Elke SMS-provider probeert de beheer service te installeren. hiervoor is een certificaat vereist. Deze service heeft een afhankelijkheid van IIS om dat certificaat te binden aan HTTPS-poort 443. Als u [Enhanced http](enhanced-http.md)inschakelt, koppelt de site dat certificaat aan het gebruik van IIS api's. Als uw site gebruikmaakt van PKI, moet u een PKI-certificaat hand matig binden in IIS op de SMS-provider. Vanaf versie 2002 gebruikt de site automatisch het zelfondertekende certificaat van de site.

## <a name="locations"></a><a name="bkmk_location"></a>Maplocaties  

Wanneer u een-site installeert, installeert u automatisch de eerste SMS-provider voor de site. U kunt elk van de volgende ondersteunde locaties opgeven voor de SMS-provider:  

- De site server  

- De site database server  

- Een andere server die voldoet aan de [installatie vereisten](#installation-prerequisites)  

De locaties van elke SMS-provider voor een site weer geven:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer vervolgens het knoop punt **sites** .  

2. Selecteer de gewenste site in de lijst en kies vervolgens **Eigenschappen** in het lint.  

3. Bekijk op het tabblad **Algemeen** van de site- **Eigenschappen**het **locatie veld SMS-provider** .  

Elke SMS-provider ondersteunt gelijktijdige verbindingen met betrekking tot meerdere aanvragen. De enige beperkingen met betrekking tot deze verbindingen zijn het aantal server verbindingen dat beschikbaar is voor Windows en de beschik bare bronnen op de server om de verbindings aanvragen te verwerken.  

Nadat u een site hebt geïnstalleerd, kunt u Configuration Manager Setup opnieuw uitvoeren op de site server. Gebruik Setup om de locatie van een bestaande SMS-provider te wijzigen of om aanvullende SMS-providers op die site te installeren. Installeer slechts één SMS-provider op een computer. Een computer kan geen SMS-provider hosten van meer dan een site.  

### <a name="choosing-a-location"></a>Een locatie kiezen

In de volgende secties worden de voor delen en nadelen beschreven van het installeren van een SMS-provider op elke ondersteunde locatie:  

#### <a name="configuration-manager-site-server"></a>Site Server Configuration Manager

- **Delen**  

  - De SMS-provider gebruikt geen systeem bronnen van de site database computer.  

  - Deze locatie is in staat om betere prestaties te bieden dan een SMS-provider op een andere computer dan de siteserver of sitedatabasecomputer.  

- **Nadelen**  

  - De SMS-provider gebruikt systeem- en netwerkbronnen die kunnen worden toegekend voor siteserverbewerkingen.  

#### <a name="sql-server-that-hosts-the-site-database"></a>SQL Server die als host fungeert voor de site database

- **Delen**  

  - De SMS-provider gebruikt geen systeem bronnen op de site server.  

  - Deze locatie kan de beste prestaties bieden van de drie locaties wanneer er voldoende serverbronnen beschikbaar zijn.  

- **Nadelen**  

  - De SMS-provider gebruikt systeem- en netwerkbronnen die kunnen worden toegekend voor sitedatabasebewerkingen.  

  - Wanneer de site database wordt gehost op een geclusterd exemplaar van SQL Server, kunt u deze locatie niet gebruiken.  

#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>Andere computer dan de site server of site database server

- **Delen**  

  - SMS-provider gebruikt geen systeem bronnen voor site server of site database.  

  - Het type locatie stelt u in staat om aanvullende SMS-providers te implementeren om een hoge beschikbaarheid voor verbindingen te bieden.  

- **Nadelen**  

  - De prestaties van de SMS-provider zijn mogelijk beperkt. Dit gedrag wordt veroorzaakt door de extra netwerk activiteit die nodig is om te coördineren met de site server en de site database computer.  

  - Deze server moet altijd toegankelijk zijn voor de site database server en op alle computers waarop de Configuration Manager-console is geïnstalleerd.  

  - Deze locatie kan systeembronnen gebruiken die anders aan andere services worden toegekend.  

## <a name="authentication"></a><a name="bkmk_auth"></a>Verificatie

<!--1357013-->
Vanaf versie 1810 kunt u het minimale verificatie niveau voor beheerders opgeven om toegang te krijgen tot Configuration Manager-sites. Deze functie dwingt beheerders af om zich aan te melden bij Windows met het vereiste niveau. Dit geldt voor alle onderdelen die toegang hebben tot de SMS-provider. Bijvoorbeeld de Configuration Manager-console, SDK-methoden en Windows Power shell-cmdlets.

### <a name="configure-authentication"></a>Verificatie configureren

Als u deze instelling wilt configureren, meldt u zich eerst aan bij Windows met het gewenste verificatie niveau.

> [!Important]  
> Deze configuratie is een instelling voor de hele hiërarchie. Voordat u deze instelling wijzigt, moet u ervoor zorgen dat alle Configuration Manager beheerders zich kunnen aanmelden bij Windows met het vereiste verificatie niveau.

Als u deze instelling wilt configureren, gebruikt u de volgende stappen:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Selecteer **hiërarchie-instellingen** in het lint.  

3. Ga naar het tabblad **verificatie** . Selecteer het gewenste [verificatie niveau](#authentication-levels)en selecteer vervolgens **OK**.  

    - Selecteer alleen wanneer dat nodig is **toevoegen** om specifieke gebruikers of groepen uit te sluiten. Zie [uitzonde ringen](#exclusions)voor meer informatie.  

### <a name="authentication-levels"></a>Verificatie niveaus

De volgende niveaus zijn beschikbaar:

- **Windows-verificatie**: authenticatie met Active Directory domein referenties vereisen. Deze instelling is het vorige gedrag en de huidige standaard instelling. Wanneer u de site bijwerkt, is er geen wijziging in het verificatie niveau.  

- **Certificaat verificatie**: authenticatie vereisen met een geldig certificaat dat is uitgegeven door een vertrouwde PKI-certificerings instantie. U kunt dit certificaat niet configureren in Configuration Manager. Configuration Manager moet de beheerder zijn aangemeld bij Windows met behulp van PKI.  

- **Windows hello voor bedrijven-verificatie**: authenticatie vereisen met een sterke twee ledige verificatie die is gekoppeld aan een apparaat en biometrie of een pincode gebruikt. Zie [Windows hello voor bedrijven](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)voor meer informatie.  

### <a name="exclusions"></a>Uitsluitingen

Op het tabblad **verificatie** van hiërarchie-instellingen kunt u ook bepaalde gebruikers of groepen uitsluiten. Gebruik deze optie spaarzaam. Bijvoorbeeld wanneer specifieke gebruikers toegang nodig hebben tot de Configuration Manager-console, maar niet op het vereiste niveau kunnen verifiëren met Windows. Het kan ook nodig zijn voor Automation of services die worden uitgevoerd in de context van een systeem account.

## <a name="about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a>Over SMS-provider talen  

De SMS-provider werkt onafhankelijk van de weergave taal van de server waarop u deze installeert.  

Wanneer een gebruiker met beheerders rechten of Configuration Manager gegevens aanvragen met behulp van de SMS-provider, probeert die gegevens te retour neren in een indeling die overeenkomt met de taal van het besturings systeem van de aanvragende computer.

De manier waarop deze overeenkomt met de taal is indirect. De SMS-provider vertaalt geen informatie van de ene naar de andere. Wanneer gegevens worden geretourneerd voor weer gave in de Configuration Manager-console, is de weergave taal van de gegevens afhankelijk van de bron van het object en het type opslag.  

Wanneer Configuration Manager gegevens opslaat voor een object in de-data base, zijn de beschik bare talen afhankelijk van de volgende factoren:  

- Configuration Manager objecten die worden gemaakt, worden opgeslagen met ondersteuning voor meerdere talen. Het object wordt opgeslagen in de site database met behulp van de talen die u configureert voor de site wanneer u Setup uitvoert. In de Configuration Manager-console worden deze objecten weer gegeven in de weergave taal van de aanvragende computer, wanneer die taal beschikbaar is voor het object. Als de console het object niet kan weer geven in de weergave taal van de aanvragende computer, wordt het object weer gegeven in de standaard taal, Engels.  

- Configuration Manager slaat objecten op die een gebruiker met beheerders rechten maakt met behulp van de taal die is gebruikt om het object te maken. Deze objecten worden in deze zelfde taal weer gegeven in de Configuration Manager-console. De SMS-provider kan deze niet omzetten en ze hebben geen meerdere taal opties.  

## <a name="use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a>Meerdere SMS-providers gebruiken  

Nadat het installeren van een site is voltooid, kunt u aanvullende SMS-providers voor de site installeren. Als u aanvullende SMS-providers wilt installeren, voert u Configuration Manager Setup uit op de site server.

Overweeg om aanvullende SMS-providers te installeren wanneer een van de volgende voor waarden waar is:  

- Veel gebruikers met beheerders rechten moeten de Configuration Manager-console gebruiken en tegelijk verbinding maken met een site.  

- U gebruikt de Configuration Manager SDK of andere producten, die mogelijk veelvuldige aanroepen naar de SMS-provider veroorzaken.  

- U hebt een zakelijke vereiste voor een hoge Beschik baarheid van de SMS-provider.  

Wanneer u meerdere SMS-providers op een site installeert en er een verbindings aanvraag wordt gedaan, wijst de site elke nieuwe verbindings aanvraag wille keurig toe om een geïnstalleerde SMS-provider te gebruiken. U kunt de SMS-provider die moet worden gebruikt met een specifieke verbindings sessie niet opgeven.  

> [!NOTE]  
> Houd rekening met de voor-en nadelen van elke SMS-provider locatie. Zie [locaties](#bkmk_location)voor meer informatie. Houd rekening met de informatie die u niet kunt bepalen welke SMS-provider voor elke nieuwe verbinding wordt gebruikt.  

Wanneer u een Configuration Manager-console voor het eerst verbindt met een site, wordt de verbindings query uitgevoerd op WMI op de site server. Met deze query wordt een exemplaar geïdentificeerd van de SMS-provider die de-console gebruikt. Deze specifieke instantie van de SMS-provider blijft in gebruik door de console totdat de sessie wordt beëindigd. Als de sessie wordt beëindigd omdat de server van de SMS-provider niet beschikbaar is op het netwerk, wordt de eerste query herhaald als u de-console opnieuw verbindt met de site. De site heeft mogelijk hetzelfde exemplaar van de SMS-provider toegewezen dat niet beschikbaar is. Als dit het geval is, probeert u opnieuw verbinding te maken met de console totdat de site een beschik bare SMS-provider retourneert.  

## <a name="about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a>Over de SMS-provider naam ruimte  

Het WMI-schema Configuration Manager definieert de structuur van de SMS-provider. Schema naam ruimten beschrijven de locatie van Configuration Manager gegevens binnen het SMS-provider schema. De volgende tabel bevat enkele van de algemene naam ruimten die door de SMS-provider worden gebruikt:  

|Naamruimte|Beschrijving|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|De SMS-provider, die uitgebreid wordt gebruikt door de Configuration Manager-console, resource Explorer, Configuration Manager-hulpprogram ma's en scripts.|  
|`Root\SMS\SMS_ProviderLocation`|De locatie van de SMS-provider computers voor een site.|  
|`Root\CIMv2`|De locatie die voor de WMI-naam ruimte gegevens is geïnventariseerd tijdens hardware-en software-inventarisatie.|  
|`Root\CCM`|Configuration Manager client configuratie beleid en client gegevens.|  
|`Root\CIMv2\SMS`|De locatie van de inventaris rapportage klassen die de inventaris-client agent verzamelt. Clients compileren deze instellingen tijdens de evaluatie van computer beleid. Deze instellingen zijn gebaseerd op de configuratie van client instellingen voor de computer.|  

## <a name="os-deployment-requirements"></a><a name="BKMK_WAIKforSMSProv"></a>Implementatie vereisten voor besturings systemen

Op de computer waarop u een exemplaar van de SMS-provider installeert, moet een ondersteunde versie van de Windows ADK worden ondersteund.  

Zie vereisten voor de [infra structuur voor besturingssysteem implementatie](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10) en [ondersteuning voor Windows 10](../configs/support-for-windows-10.md)voor meer informatie over deze vereiste.  

Wanneer u implementaties van besturings systemen beheert, laat de Windows ADK de SMS-provider verschillende taken uitvoeren, zoals:  

- Details WIM-bestand weergeven  

- Stuurprogramma's toevoegen aan bestaande opstartinstallatiekopieën  

- ISO-bestanden voor opstarten maken  

De installatie van Windows ADK kan tot 650 MB vrije schijfruimte vereisen op elke computer waarop de SMS-provider wordt geïnstalleerd. Deze vereiste hoge schijf ruimte is nodig om Configuration Manager de Windows PE-opstart installatie kopieën te installeren.  

## <a name="administration-service"></a><a name="bkmk_admin-service"></a>Beheer service

<!--3607711, fka 1321523-->

De SMS-provider biedt API-interoperabiliteits toegang via een HTTPS OData-verbinding, die de **beheer service**wordt genoemd. Deze REST API kan worden gebruikt in plaats van een aangepaste webservice om toegang te krijgen tot informatie van de site.

Zie [Wat is de beheer service?](../../../develop/adminservice/overview.md) voor meer informatie.

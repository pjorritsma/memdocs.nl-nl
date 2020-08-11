---
title: Problemen met Desktop Analytics oplossen
titleSuffix: Configuration Manager
description: Technische Details voor hulp bij het oplossen van problemen met Desktop Analytics.
ms.date: 08/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: e83e8d5d967b4cd3bbcb817c149cd40284bb5f9c
ms.sourcegitcommit: 66c58078a32af3872d98f7c62af4f8047ee81b50
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/11/2020
ms.locfileid: "88089942"
---
# <a name="troubleshoot-desktop-analytics"></a>Problemen met Desktop Analytics oplossen

Gebruik de informatie in dit artikel voor hulp bij het oplossen van problemen met Desktop Analytics die is geïntegreerd met Configuration Manager.

## <a name="confirm-prerequisites"></a>Vereisten bevestigen

Veel veelvoorkomende problemen worden veroorzaakt door ontbrekende vereisten. Bevestig eerst de volgende configuraties:

- [Vereisten](overview.md#prerequisites)  

- [Updates voor Windows-onderdelen](enroll-devices.md#update-devices)  

- Het inschakelen van het [delen van gegevens](enable-data-sharing.md), waarin de volgende onderwerpen worden behandeld:  

  - Internet-eind punten waarmee clients verbinding moeten maken  

  - Verificatie van de proxy server  

  - Niveaus van diagnostische gegevens  

## <a name="monitor-connection-health"></a>Status van de verbinding bewaken

Gebruik het dash board **verbindings status** in Configuration Manager om in categorieën in te zoomen op de status van apparaten. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw het knoop punt **Desktop Analytics Servicing** uit en selecteer het dash board **verbindings status** .  

Zie [verbindings status controleren](monitor-connection-health.md)voor meer informatie.

> [!NOTE]
> De Configuration Manager verbinding met Desktop Analytics is afhankelijk van het service verbindings punt. Wijzigingen in deze site systeemrol kunnen van invloed zijn op de synchronisatie met de Cloud service. Zie [about the Service Connection Point](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move)(Engelstalig) voor meer informatie.

Vanaf versie 2002, als de Configuration Manager-site geen verbinding kan maken met de vereiste eind punten voor een Cloud service, wordt een kritieke status bericht-ID 11488 gegenereerd. Wanneer er geen verbinding kan worden gemaakt met de service, wordt de status van het SMS_SERVICE_CONNECTOR onderdeel gewijzigd in kritiek. Bekijk de gedetailleerde status in het knoop punt [onderdeel status](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) van de Configuration Manager-console.<!-- 5566763 -->

## <a name="log-files"></a>Logboekbestanden

Zie [logboek bestanden voor desktop Analytics](../core/plan-design/hierarchy/log-files.md#desktop-analytics) voor meer informatie

Vanaf Configuration Manager versie 1906 gebruikt u het **DesktopAnalyticsLogsCollector.ps1** hulp programma van de Configuration Manager installatiemap om te helpen bij het oplossen van problemen met Desktop Analytics. Er worden enkele basis stappen voor probleem oplossing uitgevoerd en de relevante logboeken worden in één werkmap verzameld. Zie [Logboeken](log-collector.md)voor meer informatie.

### <a name="enable-verbose-logging"></a>Uitgebreide logboekregistratie inschakelen

1. Ga op het service aansluitpunt naar de volgende register sleutel:`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Stel de waarde voor **LoggingLevel** in op`0`  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a>Azure AD-toepassingen

Desktop Analytics voegt de volgende toepassingen toe aan uw Azure AD:

- **Configuration Manager micro service**: verbindt Configuration Manager met Desktop Analytics. Deze app heeft geen toegangs vereisten.  

- **MALogAnalyticsReader**: controleert uw Azure log Analytics-werk ruimte om te controleren of de dagelijkse moment opname is gekopieerd. Zie [MALogAnalyticsReader Application Role](#bkmk_MALogAnalyticsReader)(Engelstalig) voor meer informatie.  

- **Desktop Analytics**: hiermee wordt Configuration Manager het ophalen van informatie over het implementatie plan en de gereedheids status van het apparaat vanuit Desktop Analytics ingeschakeld.

Als u deze apps na het volt ooien van de installatie wilt inrichten, gaat u naar het deel venster **verbonden services** . Selecteer **gebruikers en apps toegang configureren**en richt de apps in.  

- **Azure AD-App voor Configuration Manager**. Als u verbindings problemen wilt inrichten of oplossen na het volt ooien van de installatie, raadpleegt u [app maken en importeren voor Configuration Manager](#create-and-import-app-for-configuration-manager). Deze app vereist het **schrijven van gegevens in cm** en het lezen van cm- **verzamelings gegevens** in de API van de **Configuration Manager-service** .  

    > [!NOTE]
    > Desktop Analytics ondersteunt meerdere Configuration Manager hiërarchieën die rapporteren aan één Azure AD-Tenant.<!-- 4814075 --> Als u meerdere hiërarchieën in uw omgeving hebt geconfigureerd met dezelfde commerciële ID, kunt u de Azure AD-Tenant en het bureau blad Analytics-exemplaar delen met [verschillende apps](connect-configmgr.md#bkmk_connect) voor elke hiërarchie.

### <a name="create-and-import-app-for-configuration-manager"></a>App voor Configuration Manager maken en importeren

Als u de Azure AD-App voor Configuration Manager niet kunt maken met de wizard Azure-Services configureren of als u een bestaande app opnieuw wilt gebruiken, moet u deze hand matig maken en importeren. Gebruik de volgende stappen na het volt ooien van de [eerste onboarding](set-up.md#initial-onboarding) op de Desktop Analytics-portal:

#### <a name="create-app-in-azure-ad"></a>App maken in azure AD

1. Open de [Azure Portal](https://portal.azure.com) als gebruiker met *globale beheerders* machtigingen, gaat u naar **Azure Active Directory**en selecteert u **app-registraties**. Selecteer vervolgens **nieuwe registratie**.  

2. Configureer de volgende instellingen in het deel venster **maken** :  

    - **Naam**: een unieke naam waarmee de app wordt aangeduid, bijvoorbeeld:`Desktop-Analytics-Connection`  

    - **Ondersteunde account typen**: **accounts in deze organisatie-Directory alleen (Contoso)**

    - **Omleidings-URI (optioneel)**: **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Selecteer **Registreren**.  

3. Selecteer de app, noteer de ID van de **toepassing (client)** en de **map (Tenant)**. De waarden zijn GUID'S die worden gebruikt voor het configureren van de Configuration Manager verbinding.  

4. Selecteer in het menu **beheren** de optie **certificaten & geheimen**. Selecteer **Nieuw clientgeheim**. Voer een **Beschrijving**in, geef een verloop duur op en selecteer vervolgens **toevoegen**. Kopieer de **waarde** van de sleutel, die wordt gebruikt om de Configuration Manager verbinding te configureren.

    > [!Important]  
    > Dit is de enige mogelijkheid om de sleutel waarde te kopiëren. Als u de app nu niet kopieert, moet u een andere sleutel maken.  
    >
    > Sla de sleutel waarde op een veilige locatie op.  

5. Selecteer in het menu **beheren** de optie **API-machtigingen**.  

    1. Selecteer **een machtiging toevoegen**in het deel venster **API-machtigingen** .  

    2. Schakel in het deel venster **API-machtigingen voor aanvragen** over naar api's die **Mijn organisatie gebruikt**.  

    3. Zoek en selecteer de **Configuration Manager micro service** -API.  

    4. Selecteer de groep **toepassings machtigingen** . Vouw **CmCollectionData**uit en selecteer beide van de volgende machtigingen: gegevens over het **verzamelen van cm** en lees bewerkingen in **cm verzamelen**.  

    5. Selecteer **Machtigingen toevoegen**.  

6. Selecteer in het deel venster **API-machtigingen** de optie **beheerder toestemming geven...**. Selecteer **Ja**.  

#### <a name="import-app-in-configuration-manager"></a>App importeren in Configuration Manager

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure-Services** . Selecteer **Azure-Services configureren** in het lint.  

2. Configureer de volgende instellingen op de pagina **Azure-Services** van de wizard Azure-Services:  

    - Geef een **naam** op voor het object in Configuration Manager.  

    - Geef een optionele **Beschrijving** op die u kan helpen bij het identificeren van de service.  

    - Selecteer **Desktop Analytics** in de lijst met beschik bare Services.  
  
   Selecteer **Next**.  

3. Selecteer op de pagina **app** de juiste **Azure-omgeving**. Selecteer vervolgens **importeren** voor de web-app. Configureer de volgende instellingen in het venster **apps importeren** :  

    - **Azure AD-Tenant naam**: deze naam heeft de naam in Configuration Manager  

    - **Azure AD-Tenant-id**: de **Directory-id** die u vanuit Azure AD hebt gekopieerd  

    - **Client-id**: de **toepassings-id** die u hebt gekopieerd uit de Azure AD-app  

    - **Geheime sleutel**: de sleutel **waarde** die u hebt gekopieerd uit de Azure AD-app  

    - **Verlopen van geheime sleutel**: dezelfde verval datum van de sleutel  

    - **App-ID-URI**: deze instelling moet automatisch worden ingevuld met de volgende waarde:`https://cmmicrosvc.manage.microsoft.com/`  
  
   Selecteer **controleren**en selecteer **OK** om het venster apps importeren te sluiten. Selecteer **volgende** op de pagina app van de wizard Azure-Services.  

Zie [verbinding maken met de service](connect-configmgr.md#bkmk_connect)om door te gaan met de rest van de wizard op de pagina **Diagnostische gegevens** .

#### <a name="troubleshoot-app-in-configuration-manager"></a>Problemen met de app in Configuration Manager oplossen

Als u problemen ondervindt bij het maken of importeren van de app, controleert u eerst **SMSAdminUI. log** op de specifieke fout. Controleer vervolgens de volgende configuraties:

- De Tenant is geregistreerd bij de Desktop Analytics-service. Zie [Desktop Analytics instellen](set-up.md)voor meer informatie.

- Alle vereiste eind punten zijn toegankelijk. Zie [eind punten](enable-data-sharing.md#endpoints)voor meer informatie.

- Zorg ervoor dat de gebruiker die zich aanmeldt over de juiste machtigingen beschikt. Zie [vereisten](overview.md#prerequisites)voor meer informatie.

- Zorg ervoor dat de gebruiker zich in het algemeen kan aanmelden bij Azure. Met deze actie wordt bepaald of er algemene problemen met Azure AD-verificatie zijn.

- Controleer status berichten voor het **SMS_SERVICE_CONNECTOR** onderdeel met betrekking tot de *Desktop Analytics-werk nemer*.

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a>Toepassingsrol MALogAnalyticsReader

Wanneer u Desktop Analytics instelt, gaat u namens uw organisatie akkoord. Deze toestemming is het toewijzen van de MALogAnalyticsReader-toepassing de rol van Log Analytics lezer voor de werk ruimte. Deze toepassingsrol is vereist voor desktop Analytics.

Als er tijdens de installatie een probleem is met dit proces, gebruikt u het volgende proces om deze machtiging hand matig toe te voegen:

1. Ga naar de [Azure Portal](https://portal.azure.com)en selecteer **alle resources**. Selecteer de werk ruimte van het type **log Analytics**.  

2. Selecteer **toegangs beheer (IAM)** in het menu van de werk ruimte en selecteer vervolgens **toevoegen**.  

3. Configureer de volgende instellingen in het deel venster **machtigingen toevoegen** :  

    - **Rol**: **lezer**  

    - **Toegang toewijzen aan**: **Azure AD-gebruiker,-groep of-toepassing**  

    - **Select**: **MALogAnalyticsReader**  

4. Selecteer **Opslaan**.

De portal toont een melding dat de roltoewijzing is toegevoegd.

## <a name="data-latency"></a>Gegevenslatentie

<!-- 3846531 -->
Wanneer u Desktop Analytics voor het eerst instelt, nieuwe clients inschrijft of nieuwe implementatie plannen configureert, worden de rapporten in Configuration Manager en de Desktop Analytics-Portal mogelijk niet meteen volledig weer gegeven. Het kan 2-3 dagen duren voordat de volgende stappen worden uitgevoerd:

- Actieve apparaten verzenden diagnostische gegevens naar de Desktop Analytics-Service
- De gegevens worden verwerkt door de service
- De service synchroniseert met uw Configuration Manager-site

Wanneer u apparaat verzamelingen synchroniseert van uw Configuration Manager-hiërarchie naar Desktop Analytics, kan het één uur duren voordat deze verzamelingen worden weer gegeven in de portal voor desktop Analytics. Wanneer u een implementatie plan in Desktop Analytics maakt, kan het tot één uur duren voordat de nieuwe verzamelingen die zijn gekoppeld aan het implementatie plan worden weer gegeven in uw Configuration Manager-hiërarchie. De primaire sites maken de verzamelingen en de centrale beheer site synchroniseert met Desktop Analytics. Het kan tot 24 uur duren om het lidmaatschap van de verzameling te evalueren en bij te werken. Configuration Manager U kunt dit proces versnellen door het lidmaatschap van de verzameling hand matig bij te werken.<!-- 4984639 -->

> [!Note]
> Voor hand matige verzamelings updates om wijzigingen weer te geven, moet het SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker onderdeel eerst worden gesynchroniseerd. Het kan een uur duren voordat dit proces wordt uitgevoerd. Zie **M365ADeploymentPlanWorker. log**voor meer informatie.

In de portal voor desktop Analytics zijn er twee soorten gegevens: **beheerders gegevens** en **Diagnostische gegevens**:

- De gegevens van de **beheerder** verwijzen naar de wijzigingen die u in uw werkruimte configuratie aanbrengt. Wanneer u bijvoorbeeld de beslissing of het **belang** van de **upgrade** van een activum wijzigt, wijzigt u de beheerder gegevens. Deze wijzigingen hebben vaak een samenstellende uitwerking, omdat ze de gereedheids status van een apparaat kunnen wijzigen als de betreffende Asset is geïnstalleerd.

- **Diagnostische gegevens** verwijzen naar de meta gegevens van het systeem die van client apparaten naar micro soft worden geüpload. Met deze gegevens worden Desktop Analytics gebevoegdheidd. Het bevat kenmerken zoals de inventaris van apparaten en de update status van de beveiliging en onderdelen.

Standaard worden alle gegevens in de Desktop Analytics-Portal dagelijks automatisch vernieuwd. Deze vernieuwing omvat wijzigingen in diagnostische gegevens van twee dagen geleden en alle wijzigingen die u aanbrengt in de configuratie (beheerders gegevens). Deze moet worden weer gegeven in uw Desktop Analytics-Portal met een UTC van 08:00 uur per dag.

Wanneer u wijzigingen aanbrengt aan de beheerders gegevens, kunt u een vernieuwing op aanvraag van de beheerders gegevens in uw werk ruimte activeren. Open vanuit een pagina in de Desktop Analytics-Portal de gegevens in de flyout data currency:

![Scherm afbeelding van het tabblad Data Currency-flyout in de Desktop Analytics-Portal](media/data-currency-flyout.png)

Selecteer vervolgens **wijzigingen Toep assen**:

![Scherm opname van de uitgevouwen flyout data Currency in de Desktop Analytics-Portal](media/data-currency-flyout-expand.png)

Dit proces duurt over het algemeen tussen 15-60 minuten. De timing is afhankelijk van de grootte van uw werk ruimte en het bereik van de wijzigingen die moeten worden verwerkt. Wanneer u een gegevens vernieuwing op aanvraag aanvraagt, worden er geen wijzigingen aangebracht in de diagnostische gegevens.  Zie [Veelgestelde vragen over desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)voor meer informatie.

Als u geen wijzigingen ziet die zijn bijgewerkt binnen de hierboven vermelde tijd, wacht u nog eens 24 uur voor de volgende dagelijkse vernieuwing. Als u langere vertragingen ziet, controleert u het dash board voor service status. Als de service rapporteert als in orde, neemt u contact op met micro soft ondersteuning.<!-- 3896921 -->

> [!IMPORTANT]
> De optie Desktop Analytics om **recente gegevens weer te geven** , is afgeschaft. Deze actie wordt verwijderd in een toekomstige versie van de Desktop Analytics-service. Zie [afgeschafte functies](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.<!--7080949-->  

## <a name="service-notifications"></a>Servicemeldingen

<!-- 4982509 -->

De Desktop Analytics-Portal kan meldings banners voor beheerders weer geven. Met deze meldingen kan micro soft met u communiceren over belang rijke gebeurtenissen en problemen. In de volgende secties worden de meldingen beschreven die mogelijk worden weer gegeven.

### <a name="see-whats-new-this-month-in-desktop-analytics"></a>Wat is er nieuw in deze maand in Desktop Analytics?

Met deze informatieve melding wordt u op de hoogte gebracht van wijzigingen in de service. Zie [what's New in Desktop Analytics](whats-new.md) () voor meer informatie `https://aka.ms/danews` .

### <a name="there-are-new-prerequisites-to-continue-using-desktop-analytics-review-the-new-requirements"></a>Er zijn nieuwe vereisten. Als u wilt door gaan met het gebruik van Desktop Analytics, raadpleegt u de nieuwe vereisten

Met deze informatieve melding wordt u op de hoogte gebracht van wijzigingen in de vereisten. Bijvoorbeeld een nieuw Internet-eind punt of software-update. Zie [vereisten](overview.md#prerequisites) () voor meer informatie `https://aka.ms/daprereqs` .

### <a name="were-investigating-an-issue-that-impacts-desktop-analytics"></a>Er wordt een probleem onderzocht dat van invloed is op Desktop Analytics

Deze waarschuwing geeft aan dat micro soft op de hoogte is van een probleem dat van invloed is op de Desktop Analytics-service. Het probleem wordt meestal veroorzaakt door het genereren van moment opnamen. Wanneer u deze melding ziet, onderzoekt micro soft het probleem om het bereik en de bron van de impact te bepalen. U hoeft geen contact op te nemen met Microsoft Ondersteuning. Zie [Data flow](privacy.md#data-flow)voor meer informatie.

### <a name="were-investigating-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>Er wordt een probleem met de gegevens latentie onderzocht. Als u nieuwe apparaten hebt Inge schreven of activa in de afgelopen 24 uur hebt gewijzigd, worden ze mogelijk niet meteen weer gegeven

Deze waarschuwing geeft aan dat micro soft op de hoogte is van een probleem dat van invloed is op de Desktop Analytics-service. Micro soft bewaakt voortdurend de service om te bevestigen dat alle onderdelen moment opnamen bijwerken op de juiste tijdstippen. Tijdens deze bewaking is een van deze onderdelen niet voltooid zoals verwacht. Wanneer u deze melding ziet, onderzoekt micro soft het probleem. U hoeft geen contact op te nemen met Microsoft Ondersteuning. Zie [Data flow](privacy.md#data-flow)voor meer informatie.

Als u onlangs [apparaten](enroll-devices.md) of gewijzigde [assets](about-assets.md)hebt geregistreerd, wacht u totdat het probleem door micro soft is opgelost. U hoeft geen acties te herhalen.

### <a name="weve-resolved-a-temporary-issue-with-data-latency-daily-refresh-of-portal-data-is-delayed"></a>Er is een tijdelijk probleem met de gegevens latentie opgelost. Het dagelijks vernieuwen van de portal gegevens is vertraagd

Deze melding laat u weten dat er een probleem is met de gegevens latentie. De service verwerkt nog steeds de moment opname en het vernieuwen van de gegevens is vertraagd. Zie [Data latentie](#data-latency)voor meer informatie.

### <a name="weve-resolved-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>Er is een probleem met de gegevens latentie opgelost. Als u nieuwe apparaten hebt Inge schreven of activa in de afgelopen 24 uur hebt gewijzigd, worden ze mogelijk niet meteen weer gegeven

Deze melding laat u weten dat micro soft een eerder gemeld probleem met de gegevens latentie heeft opgelost. Mogelijk ziet u verouderde gegevens voor de moment opname van morgen. Als u apparaten in de afgelopen 24 uur hebt [Inge schreven](enroll-devices.md) of wijzigingen in de apparaatconfiguratie hebt aangebracht, worden deze niet meteen weer gegeven in de portal. U kunt Desktop Analytics blijven gebruiken om [activa](about-assets.md) te categoriseren en [implementatie plannen](about-deployment-plans.md)voor te bereiden. Deze acties kunnen gebruikmaken van gegevens uit de vorige moment opname.

### <a name="weve-resolved-an-issue-with-desktop-analytics-daily-refresh-of-the-portal-data-is-on-track"></a>Er is een probleem met Desktop Analytics opgelost. Dagelijkse vernieuwing van de portal gegevens is op schema

Deze melding laat u weten dat micro soft een moment opname onderdeel heeft geïdentificeerd dat tijdens de verwerking niet meer werkt. Micro soft heeft het onderdeel opnieuw gestart, wat tijd zal duren om de moment opname te verwerken. Micro soft bewaakt voortdurend de service om te bevestigen dat alle onderdelen moment opnamen bijwerken op de juiste tijdstippen.

---
title: Problemen met MSfB-integratie oplossen
titleSuffix: Configuration Manager
description: Biedt suggesties en oplossingen voor het oplossen van enkele van de meest voorkomende problemen met Microsoft Store voor de integratie van Business en Education.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149091"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>Problemen oplossen met de Microsoft Store voor zakelijke en onderwijs integratie met Configuration Manager

Dit artikel bevat tips en oplossingen voor het oplossen van problemen met een aantal van de belangrijkste problemen die u mogelijk hebt met de integratie van Microsoft Store for Business and education (MSfB) met Configuration Manager.

Zie voor meer informatie over het gebruik van de Microsoft Store voor bedrijven en onderwijs met Configuration Manager [apps beheren van de Microsoft Store voor bedrijven en onderwijs met Configuration Manager](manage-apps-from-the-windows-store-for-business.md).

## <a name="monitor"></a>Controleren

### <a name="component-status"></a>Onderdeel status

Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **systeem status**uit en selecteer het knoop punt **onderdeel status** . Bewaak de status van de volgende onderdelen:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>Synchronisatie status

Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Microsoft Store voor zakelijk** . Controleer de kolom **laatste synchronisatie status** .

### <a name="view-synchronized-apps"></a>Gesynchroniseerde apps weer geven

Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **licentie gegevens voor Store-apps** .


## <a name="log-files"></a>Logboekbestanden

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker. log

Dit logboek bestand bevindt zich op het service aansluitpunt, onder `\Logs` in de installatiemap van Configuration Manager. Het registreert informatie over de communicatie met de Cloud service. Deze informatie omvat meta gegevens, pictogrammen, pakketten en het ophalen van licentie bestanden.

Als u het logboek niveau wilt wijzigen, `LoggingLevel` wijzigt u `0` de waarde `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` in de register sleutel. Zie [Configure logging Options](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site)(Engelstalig) voor meer informatie.

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION. log

Dit logboek bestand bevindt zich op het service aansluitpunt, onder `\Logs` in de installatiemap van Configuration Manager. Als de WSfBSyncWorker-service niet is gestart of herhaaldelijk wordt gestart en gestopt, controleert u de vermeldingen in dit logboek bestand.

> [!NOTE]
> Dit logboek bestand wordt gedeeld met andere functies.

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker. log

Dit logboek bestand bevindt zich op de site server voor de site op het hoogste niveau in de hiërarchie. Onder `\Logs` in de Configuration Manager installatiemap. Er wordt informatie over de volgende processen vastgelegd:

- De meta gegevens gegevens die zijn gesynchroniseerd met het onderdeel BusinessAppProcessWorker in de data base invoegen
- Bestanden verwerken in`\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER. log

Dit logboek bestand bevindt zich op de site server voor de site op het hoogste niveau in de hiërarchie. Onder `\Logs` in de Configuration Manager installatiemap. Als de BusinessAppProcessWorker-service niet is gestart of herhaaldelijk wordt gestart en gestopt, controleert u de vermeldingen in dit logboek bestand.



## <a name="last-sync-failed"></a>Laatste synchronisatie mislukt

Wanneer de laatste synchronisatie status is *mislukt*, controleert u eerst de volgende [logboek bestanden](#log-files) om het symptoom te identificeren:

- WSfbSyncWorker. log
- SMS_CLOUDCONNECTION. log

Bekijk vervolgens een van de volgende secties voor veelvoorkomende problemen:

- [Autorisatie fout](#bkmk_fail-symptom1)
- [De geheime sleutel is ongeldig](#bkmk_fail-symptom2)
- [Fout bij het ophalen van het toepassings token](#bkmk_fail-symptom3)
- [Locatie van inhoud bestaat niet of heeft onjuiste machtigingen](#bkmk_fail-symptom4)
- [Er is een fout opgetreden tijdens het aanroepen van de HTTP-aanvraag methode GET](#bkmk_fail-symptom5)
- [Kan niet meer bytes schrijven naar de buffer](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a>Autorisatie fout

#### <a name="cause"></a>Oorzaak

Dit probleem kan optreden als de geconfigureerde Azure Active Directory-toepassing (Azure AD) geen machtigingen heeft voor het beheren van de Microsoft Store voor zakelijk en onderwijs voor deze Tenant.

#### <a name="workaround"></a>Tijdelijke oplossing

1. Meld u aan als beheerder voor de portal van Microsoft Store voor bedrijven of onderwijs.
1. Ga naar **instellingen**en selecteer **beheer hulpprogramma's**.
1. Als de toepassing niet wordt weer gegeven, selecteert u **een beheer programma toevoegen**. Zoek vervolgens op naam en selecteer de Azure AD-toepassing die is gekoppeld aan dezelfde ClientID als Configuration Manager.
1. Als de status niet **actief**is, selecteert u **activeren** in het gedeelte **actie** .
1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Microsoft Store voor zakelijk** . Synchroniseer met de Store of wacht tot het volgende synchronisatie-interval plaatsvindt.

> [!Tip]
> De ClientID in Configuration Manager zoeken:
>
> 1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure Active Directory Tennts** .
> 1. Selecteer de Tenant die u gebruikt voor de integratie van de Microsoft Store voor zakelijke en onderwijs.
> 1. Zoek in het resultaten venster de overeenkomende toepassing en kijk naar de kolom **client-id** .

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a>De geheime sleutel is ongeldig

#### <a name="cause"></a>Oorzaak

Dit probleem kan optreden als de geheime sleutel is verlopen voor de Azure AD-App voor de Microsoft Store voor de configuratie van zakelijk en onderwijs.

#### <a name="resolution"></a>Oplossing

Vernieuw de geheime sleutel voor de Azure AD-toepassing. Zie [geheime sleutel vernieuwen](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew)voor meer informatie.

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a>Fout bij het ophalen van het toepassings token

#### <a name="cause"></a>Oorzaak

Dit probleem kan optreden als de verbonden app niet meer bestaat in azure AD.

#### <a name="resolution"></a>Oplossing

De verbinding met de Microsoft Store voor bedrijven en onderwijs verwijderen en opnieuw maken.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Microsoft Store voor zakelijk** .
1. Selecteer de bestaande verbinding.
1. Selecteer **verwijderen** in het lint.

Maak de verbinding vervolgens opnieuw. Raadpleeg voor meer informatie de volgende artikelen:

- [Azure-Services configureren](../../core/servers/deploy/configure/azure-services-wizard.md)
- [Microsoft Store instellen voor het synchroniseren van zakelijke en onderwijs instellingen](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a>Locatie van inhoud bestaat niet of heeft onjuiste machtigingen

#### <a name="cause"></a>Oorzaak

Wanneer u de Microsoft Store voor Business-en Education-verbinding instelt, geeft u een netwerk share op voor het opslaan van gesynchroniseerde inhoud. Dit probleem kan optreden als deze share niet bestaat of onjuiste machtigingen heeft. Het computer account voor het service verbindings punt moet de eigenaar zijn van deze map en eventuele submappen.<!-- memdocs#146 --> Als dat niet het geval is, wordt er een fout melding weer gegeven die vergelijkbaar is met de volgende fout:

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

Als u de locatie wilt zien die u hebt geconfigureerd:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Microsoft Store voor zakelijk** .

1. Selecteer het account en open de **Eigenschappen**ervan.

1. Ga naar het tabblad **configuratie** . De **locatie** -instelling toont het netwerkpad voor het opslaan van toepassings inhoud die is gedownload van de Microsoft Store voor bedrijven en onderwijs.

#### <a name="workaround"></a>Tijdelijke oplossing

1. Als deze nog niet bestaat, maakt u de share.

1. Controleer de NTFS-machtigingen voor de map en de machtigingen op de netwerk share. Verleen het computer account van het service verbindings punt **Lees** -en **Schrijf** machtigingen.

Als u de locatie opnieuw wilt configureren, verwijdert u de verbinding en maakt u deze opnieuw met de nieuwe locatie van de inhoud.

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a>Er is een fout opgetreden tijdens het aanroepen van de HTTP-aanvraag methode GET

#### <a name="cause"></a>Oorzaak

Dit probleem kan zich voordoen als de synchronisatie van toepassingen uit de Store zo lang duurde dat de inhouds-URL is verlopen.

#### <a name="workaround"></a>Tijdelijke oplossing

Het synchronisatie proces opnieuw proberen

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Microsoft Store voor zakelijk** .
1. Selecteer de verbinding. Selecteer in het lint de optie **synchroniseren van Microsoft Store voor bedrijven**.

Bij elke keer moet het worden voortgezet. Het kan enkele nieuwe pogingen duren, afhankelijk van de volgende factoren:

- Het aantal offline toepassingen
- De grootte van de pakketten
- De netwerk snelheid

Bij elke poging zou de fout minder vaak moeten worden weer geven. Als het aantal fouten niet vermindert, is er nog een probleem.

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a>Kan niet meer bytes schrijven naar de buffer

#### <a name="cause"></a>Oorzaak

Dit probleem kan optreden als het pakket van de toepassing groter is dan 500 MB. Configuration Manager ondersteunt alleen automatische synchronisatie van offline toepassingen met pakketten van minder dan 500 MB.

#### <a name="workaround"></a>Tijdelijke oplossing

Deze apps kunnen niet automatisch worden gesynchroniseerd, maar u kunt de inhoud downloaden en de toepassing hand matig maken:

1. Haal de mislukte toepassings-ID op uit de volgende regel in **WSfbSynWorker. log**:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Meld u aan als beheerder voor de portal van Microsoft Store voor bedrijven of onderwijs. Zoek de pagina voor deze toepassing.

    > [!Tip]
    > De URL voor de pagina is vergelijkbaar met:`https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Selecteer **offline**als dit nog niet is geselecteerd. Selecteer vervolgens **beheren**.

    1. Maak een afzonderlijke map in de inhouds share van de toepassing voor alle ondersteunde platforms.

    1. Down load het pakket naar de map package.

    1. Down load het gecodeerde licentie bestand als `.bin` een bestand naar de pakketmap.

    1. Down load alle vereiste Frameworks naar de pakketmap.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **toepassingen** .

1. [Maak een toepassing](create-applications.md)en geef hand matig de toepassings gegevens op.

    1. Maak een implementatie type voor elk ondersteund platform dat u eerder hebt gedownload.

    1. Type: **Windows-app-\*pakket (. \*appx,. appxbundle)**

    1. Geef het appx-appxbundle voor het daad werkelijke app-pakket op, niet een vereiste afhankelijkheids pakket.

Bevestig de volgende gegevens op de pagina **gegevens** van de laatste import:

- **Licentie bestand:** Hiermee geeft `.bin` u het bestand. Dit licentie bestand is vereist voor offline-Apps.
- **Windows-app-afhankelijkheden:** Controleer of alle vereiste afhankelijkheden voor dit pakket zijn gedownload.


## <a name="sync-doesnt-run"></a>Synchronisatie wordt niet uitgevoerd

In deze sectie worden de volgende synchronisatie problemen beschreven:

- U kunt het synchronisatie proces hand matig starten, maar dit wordt niet uitgevoerd
- De site synchroniseert niet elke dag automatisch

Bekijk eerst de volgende [logboek bestanden](#log-files) om het symptoom te identificeren:

- BusinessAppProcessWorker. log
- SMS_BUSINESS_APP_PROCESS_MANAGER. log
- WsfbSyncWorker. log
- SMS_CLOUDCONNECTION. log

Bekijk vervolgens een van de volgende secties voor veelvoorkomende problemen:

- [Hand matige synchronisatie wordt niet gestart](#bkmk_sync-symptom1)
- [Automatische dagelijkse synchronisatie wordt niet uitgevoerd en de fout ' de # Workers worden afgesloten ' in SMS_BUSINESS_APP_PROCESS_MANAGER. log](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a>Hand matige synchronisatie wordt niet gestart

#### <a name="cause"></a>Oorzaak

Dit probleem kan optreden als u een synchronisatie van minder dan 10 minuten na de vorige synchronisatie start. U kunt niet vaker dan elke 10 minuten synchroniseren.

#### <a name="resolution"></a>Oplossing

Wacht mini maal tien minuten voordat u een andere synchronisatie start.

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a>Automatische dagelijkse synchronisatie wordt niet uitgevoerd en de fout ' de # Workers worden afgesloten ' in SMS_BUSINESS_APP_PROCESS_MANAGER. log

#### <a name="cause"></a>Oorzaak

Dit probleem kan optreden als het onderdeel SMS_BUSINESS_APP_PROCESS_MANAGER de WsfbSyncWorker-thread stopt. Bij deze fout kunnen ofwel `2` `4` werk nemers worden opgegeven.

#### <a name="workaround"></a>Tijdelijke oplossing

Start de **SMS_EXECUTIVE** -service opnieuw.

Als u die hoofd service niet kunt starten, stopt u beide onderdelen met MSfB-werk rollen en start u beide:

1. Open het Windows-REGI ster op de server waarop het service verbindings punt wordt uitgevoerd

1. Ga naar `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. De aangevraagde bewerking is ingesteld om te **stoppen**.

    1. Vernieuwen om de huidige status te controleren = **gestopt**.

1. Ga naar `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. De aangevraagde bewerking is ingesteld om te **stoppen**.

    1. Vernieuwen om de huidige status te controleren = **gestopt**.

1. Stel in **SMS_CLOUDCONNECTION**de aangevraagde bewerking in op **starten**.

1. Stel in **SMS_BUSINESS_APP_PROCESS_MANAGER**de aangevraagde bewerking in op **starten**.


## <a name="language-related-issues"></a>Taal problemen

Deze sectie bevat de volgende veelvoorkomende problemen:

- [Wijzigingen in de taal selectie worden niet toegepast](#bkmk_lang-symptom1)
- [Niet alle geselecteerde talen zijn aanwezig voor alle licentie gegevens](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a>Wijzigingen in de taal selectie worden niet toegepast

#### <a name="cause"></a>Oorzaak

Dit probleem kan optreden als de taal selectie in de cache wordt opgeslagen en niet wordt gewist nadat de eigenschapwaarden zijn gewijzigd.

#### <a name="workaround"></a>Tijdelijke oplossing

U kunt dit probleem oplossen door de **SMS_Executive** -service opnieuw te starten.

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a>Niet alle geselecteerde talen zijn aanwezig voor alle licentie gegevens

#### <a name="cause"></a>Oorzaak

Dit probleem kan zich voordoen als de Microsoft Store voor de licentie gegevens van de toepassing voor bedrijven en onderwijs geen gelokaliseerde gegevens voor de opgegeven taal bevatten.

#### <a name="workaround"></a>Tijdelijke oplossing

Voeg hand matig ontbrekende talen toe voor gemaakte toepassingen.


## <a name="offline-applications"></a>Offline toepassingen

Deze sectie bevat de volgende veelvoorkomende problemen:

- [Kan geen offline toepassing maken omdat inhoud niet kan worden geverifieerd](#bkmk_off-symptom1)
- [Kan geen toepassing installeren die is gemaakt op basis van offline licentie gegevens](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a>Kan geen offline toepassing maken omdat inhoud niet kan worden geverifieerd

#### <a name="cause"></a>Oorzaak

Dit probleem kan optreden als de gesynchroniseerde inhoud voor de offline toepassing is beschadigd of gewijzigd.

#### <a name="workaround"></a>Tijdelijke oplossing

Start een nieuwe synchronisatie. Wanneer de synchronisatie is voltooid, moeten er onjuiste inhouds bestanden worden gecontroleerd en gedownload.

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a>Kan geen toepassing installeren die is gemaakt op basis van offline licentie gegevens

#### <a name="cause"></a>Oorzaak

Dit probleem kan optreden als u de toepassing implementeert op een client met een versie van Windows 10 ouder dan versie 1511. Apps met een offline licentie van Microsoft Store voor bedrijven en onderwijs worden alleen ondersteund in Windows 10 versie 1511 en hoger.

#### <a name="resolution"></a>Oplossing

Installeer de nieuwste versie van Windows 10.


## <a name="next-steps"></a>Volgende stappen

Zie [hulp zoeken voor het gebruik van Configuration Manager](../../core/understand/find-help.md)voor meer informatie.

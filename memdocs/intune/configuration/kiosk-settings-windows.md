---
title: Kioskinstellingen voor Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Configureer uw apparaten met Windows 10 (en hoger) als kiosken voor één app en voor meerdere apps, pas het menu Start aan, voeg apps toe, toon de taakbalk en configureer een webbrowser in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a37b94ee0e474e9e3da6aae359ba1b315212910
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911927"
---
# <a name="windows-10-and-later-device-settings-to-run-as-a-kiosk-in-intune"></a>Instellingen voor apparaten met Windows 10 en hoger om ze als kiosk uit te voeren via Intune

Op apparaten met Windows 10 en hoger kunt u configureren dat deze apparaten worden uitgevoerd in de kioskmodus met één app of in de kioskmodus met meerdere apps.

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen die u kunt beheren op apparaten met Windows 10 en hoger. Gebruik deze instellingen voor het configureren van uw apparaten met Windows 10 en hoger, zodat ze in de kioskmodus worden uitgevoerd, als onderdeel van uw MDM-oplossing (Mobile Device Management).

Als Intune-beheerder kunt u deze instellingen maken en toewijzen aan uw apparaten.

Zie voor meer informatie over de Windows-kioskfunctie in Intune [Configure kiosk settings](kiosk-settings.md) (Kioskinstellingen configureren).

## <a name="before-you-begin"></a>Voordat u begint

- [Maak het profiel](kiosk-settings.md#create-the-profile).

- Dit kioskprofiel is direct gerelateerd aan het apparaatbeperkingsprofiel dat u maakt met behulp van de [Windows Edge kioskinstellingen](device-restrictions-windows-10.md#microsoft-edge-browser). Samenvatting:

  1. Maak dit kioskprofiel om het apparaat in de kioskmodus uit te voeren.
  2. Maak het [apparaatbeperkingsprofiel](device-restrictions-windows-10.md#microsoft-edge-browser) en configureer specifieke functies en instellingen die zijn toegestaan in Microsoft Edge.

- Controleer of bestanden, scripts en snelkoppelingen zich in het lokale systeem bevinden. Raadpleeg [Lay-out van het menu Start aanpassen en exporteren](/windows/configuration/customize-and-export-start-layout) voor meer informatie, waaronder andere Windows-vereisten.

> [!IMPORTANT]
> Zorg ervoor dat u dit kioskprofiel toewijst aan de dezelfde apparaten als uw [Microsoft Edge-profiel](device-restrictions-windows-10.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>Kiosk met één app, in volledige schermweergave

Hiermee wordt slechts één app op het apparaat uitgevoerd.

- **Selecteer een kioskmodus**: Kies **Kiosk met één app, in volledige schermweergave**.

- **Aanmeldingstype gebruiker**: Selecteer het accounttype waarmee de app wordt uitgevoerd. Uw opties zijn:

  - **Automatisch aanmelden (Windows 10 versie 1803 en hoger)** : Gebruik dit in kiosken in openbare omgevingen waarbij een gebruiker zich niet hoeft aan te melden, vergelijkbaar met een gastaccount. Deze instelling maakt gebruik van [AssignedAccess CSP](/windows/client-management/mdm/assignedaccess-csp).
  - **Lokaal gebruikersaccount**: Voeg het lokale (op het apparaat) gebruikersaccount toe. Met het account dat u invoert, kunt u zich aanmelden bij de kiosk.

- **Toepassingstype**: Selecteer het toepassingstype. Uw opties zijn:

  - **Microsoft Edge-browser toevoegen**: selecteer **Microsoft Edge-browser** en kies het **Microsoft Edge-kioskmodustype**:

    - **Digitale/interactieve display**: hiermee wordt een volledig URL-scherm geopend, met alleen de inhoud op die website. [Digitale displays instellen](/windows/configuration/setup-digital-signage) biedt meer informatie over deze functie.
    - **Openbaar bladeren (InPrivate)** : Er wordt een beperkte versie met meerdere tabbladen van Microsoft Edge uitgevoerd. Gebruikers kunnen openbaar bladeren of de browsersessie beëindigen.

    Zie [Microsoft Edge-kioskmodus implementeren](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types) voor meer informatie over deze opties.

    > [!NOTE]
    > Via deze instelling schakelt u de Microsoft Edge-browser in op het apparaat. Als u specifieke Microsoft Edge-instellingen wilt configureren, maakt u een apparaatbeperkingsprofiel (**Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **Windows 10** voor platform > **Apparaatbeperkingen** > **Microsoft Edge-browser**). De beschikbare instellingen worden in de [Microsoft Edge-browser](device-restrictions-windows-10.md#microsoft-edge-browser) vermeld en beschreven.

  - **Kiosk-browser toevoegen**: Selecteer **Browserinstellingen voor de kiosk**. Met deze instellingen beheert u een webbrowser-app op de kiosk. Zorg ervoor dat u de [Kioskbrowser-app](https://businessstore.microsoft.com/store/details/kiosk-browser/9NGB5S5XG2KP) uit de Store ophaalt en deze aan Intune toevoegt als een [client-app](../apps/apps-add.md). Wijs vervolgens de app toe aan de kioskapparaten.

    Voer de volgende instellingen in:

    - **Standaard-URL voor de startpagina**: Voer de standaard-URL in die wordt weergegeven als de kioskbrowser wordt geopend of opnieuw wordt gestart. Voer bijvoorbeeld `http://bing.com` of `http://www.contoso.com` in.

    - **Knop Start**: **Toon** of **verberg** de knop Start van de kioskbrowser. Standaard wordt de knop niet weergegeven.

    - **Navigatieknoppen**: **Toon** of **verberg** de knoppen Volgende en Vorige. De navigatieknoppen worden standaard niet weergegeven.

    - **Knop Sessie beëindigen**: **Toon** of **verberg** de knop voor het beëindigen van de sessie. Als deze knop wordt getoond, selecteert de gebruiker de knop en wordt in de app gevraagd om de sessie te beëindigen. Wanneer de actie wordt bevestigd, wist de browser alle browsegegevens (cookies, cache etc.) en wordt de standaard-URL geopend. Standaard wordt de knop niet weergegeven.

    - **De browser vernieuwen na niet-actieve tijd**: Voer de niet-actieve tijd (tussen 1-1440 minuten) in, waarna de kioskbrowser opnieuw wordt gestart en vernieuwd. Niet-actieve tijd is het aantal minuten dat is verstreken sinds de laatste interactie van de gebruiker. De waarde is standaard leeg of blanco, wat inhoudt dat er geen time-out is voor inactiviteit.

    - **Toegestane websites**: Gebruik deze instelling om toe te staan dat bepaalde websites worden geopend. Met andere woorden, gebruik deze functie om het aantal websites dat op het apparaat kan worden geopend, te beperken. U kunt bijvoorbeeld toestaan dat alle websites op `http://contoso.com` kunnen worden geopend. Standaard worden alle websites toegestaan.

      Als u specifieke websites wilt toestaan, moet u een bestand uploaden dat een lijst met toegestane websites op afzonderlijke regels bevat. Als u geen bestand toevoegt, zijn alle websites toegestaan. Standaard worden alle subdomeinen van de website door Intune toegestaan. U kunt bijvoorbeeld het domein `sharepoint.com` opgeven. Intune staat automatisch alle subdomeinen toe, zoals `contoso.sharepoint.com`, `my.sharepoint.com`, enzovoort. Voer geen jokertekens in, zoals het sterretje (`*`).

      Het voorbeeldbestand moeten eruitzien als het volgende lijst:

      `http://bing.com`  
      `https://bing.com`  
      `http://contoso.com`  
      `https://contoso.com`  
      `office.com`

    > [!NOTE]
    > Voor Windows 10-kiosken waarvoor automatische aanmelding is ingeschakeld met Microsoft Kiosk Browser moet u een offline licentie gebruiken uit de Microsoft Store voor bedrijven. Deze vereiste is van toepassing omdat bij de automatische aanmelding gebruik wordt gemaakt van een lokaal gebruikersaccount zonder AD-referenties (Azure Active Directory). Online licenties kunnen daarom niet worden beoordeeld. Zie [Offline apps distribueren](/microsoft-store/distribute-offline-apps) voor meer informatie.

  - **Store-app toevoegen**: selecteer **Een Store-app toevoegen** en kies een app uit de lijst.

    Worden er geen apps in de lijst weergegeven? Voeg er een aantal toe met behulp van de stappen in [Client-apps](../apps/apps-add.md).

- **Onderhoudsvenster opgeven voor opnieuw opstarten van apps**: Voor sommige apps moet de computer opnieuw worden opgestart om de installatie van de app te voltooien of de installatie van updates te voltooien. Met **Vereisen** wordt een onderhoudsvenster gemaakt. Als de app opnieuw moet worden opgestart, wordt deze opnieuw gestart tijdens dit venster.

  Voer ook in:

  - **Begintijd van onderhoudsvenster**: Selecteer de datum en tijd van de dag waarop u clients wilt gaan controleren op app-updates waarvoor opnieuw moet worden gestart. De reguliere begintijd is middernacht, oftewel nul minuten. Als deze leeg is, worden apps op een niet-gepland tijdstip 3 dagen na de installatie van een app-update opnieuw gestart.

  - **Terugkeerpatroon voor onderhoudsvenster**: De standaardinstelling is dagelijks. Selecteer hoe vaak onderhoudsvensters voor app-updates moeten worden uitgevoerd. Om te voorkomen dat apps op een niet-gepland tijdstip opnieuw worden gestart, wordt **Dagelijks** aanbevolen.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="multi-app-kiosk"></a>Kiosk voor meerdere apps

Apps in deze modus zijn beschikbaar in het startmenu. Deze apps zijn de enige apps die de gebruiker kan openen. Als een app een afhankelijkheid van een andere app heeft, moeten beide worden opgenomen in de lijst met toegestane apps. De 64-bits Internet Explorer-versie heeft bijvoorbeeld een afhankelijkheid van de 32-bits Internet Explorer-versie, dus moet u zowel C:\Program Files\internet explorer\iexplore.exe als C:\Program Files (x86)\Internet Explorer\iexplore.exe toestaan. 

- **Selecteer een kioskmodus**: Selecteer **Kiosk voor meerdere apps**.

- **Gericht op Windows 10-apparaten in de S-modus**:
  - **Ja**: hiermee staat u Store-apps en AUMID-apps in het kioskprofiel toe. Win32-apps zijn uitgesloten.
  - **Nee**: hiermee staat u Store-apps, Win32-apps en AUMID-apps in het kioskprofiel toe. Dit kioskprofiel wordt niet geïmplementeerd op apparaten in de S-modus.

- **Aanmeldingstype gebruiker**: selecteer het accounttype waarmee uw apps worden uitgevoerd. Uw opties zijn:

  - **Automatisch aanmelden (Windows 10 versie 1803 en hoger)** : Gebruik dit in kiosken in openbare omgevingen waarbij een gebruiker zich niet hoeft aan te melden, vergelijkbaar met een gastaccount. Deze instelling maakt gebruik van [AssignedAccess CSP](/windows/client-management/mdm/assignedaccess-csp).
  - **Lokaal gebruikersaccount**: **Voeg** het lokale (op het apparaat) gebruikersaccount toe. Met het account dat u invoert, kunt u zich aanmelden bij de kiosk.
  - **Azure AD-gebruiker of -groep (Windows 10, versie 1803 of hoger)** : Selecteer **Toevoegen** en kies Azure AD-gebruikers of -groepen in de lijst. U kunt meerdere gebruikers en groepen selecteren. Kies **Selecteren** om uw wijzigingen op te slaan.
  - **HoloLens-bezoeker**: Het bezoekersaccount is een gastaccount waarvoor geen gebruikersreferenties zijn of verificatie is vereist, zoals wordt beschreven in [Gedeelde pc-modusconcepten](/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Browser en apps**: Voeg de apps toe die u op het apparaat in kioskmodus wilt uitvoeren. U kunt verschillende apps toevoegen.

  :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-add-applications-browser.png" alt-text="Voeg browsers of apps toe aan het kioskprofiel voor meerdere apps in Microsoft Intune.":::  

  - **Browsers**

    - **Microsoft Edge toevoegen**: Microsoft Edge wordt toegevoegd aan het app-raster en alle apps kunnen in deze kiosk worden uitgevoerd. Selecteer het **Microsoft Edge-kioskmodustype**:

      - **Normale modus (volledige versie van Microsoft Edge)** : Er wordt een volledige versies van Microsoft Edge uitgevoerd met alle browserfuncties. Gebruikersgegevens en -statussen worden tussen sessies opgeslagen.
      - **Openbaar bladeren (InPrivate)** : hiermee wordt een versie met meerdere tabbladen van Microsoft Edge InPrivate uitgevoerd met een op maat gemaakte toepassing voor kiosken die in volledige schermweergave worden uitgevoerd.

      Zie [Microsoft Edge-kioskmodus implementeren](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types) voor meer informatie over deze opties.

      > [!NOTE]
      > Via deze instelling schakelt u de Microsoft Edge-browser in op het apparaat. Als u specifieke Microsoft Edge-instellingen wilt configureren, maakt u een apparaatbeperkingsprofiel (**Apparaatconfiguratie** > **Profielen** > **Profiel maken** > > **Windows 10** voor platform > **Apparaatbeperkingen** >  **Microsoft Edge-browser**). De beschikbare instellingen worden in de [Microsoft Edge-browser](device-restrictions-windows-10.md#microsoft-edge-browser) vermeld en beschreven.

    - **Kiosk-browser toevoegen**: Met deze instellingen beheert u een webbrowser-app op de kiosk. Implementeer met [Client-apps](../apps/apps-add.md) een webbrowser-app op de kioskapparaten.

      Voer de volgende instellingen in:

      - **Standaard-URL voor de startpagina**: Voer de standaard-URL in die wordt weergegeven als de kioskbrowser wordt geopend of opnieuw wordt gestart. Voer bijvoorbeeld `http://bing.com` of `http://www.contoso.com` in.

      - **Knop Start**: **Toon** of **verberg** de knop Start van de kioskbrowser. Standaard wordt de knop niet weergegeven.

      - **Navigatieknoppen**: **Toon** of **verberg** de knoppen Volgende en Vorige. De navigatieknoppen worden standaard niet weergegeven.

      - **Knop Sessie beëindigen**: **Toon** of **verberg** de knop voor het beëindigen van de sessie. Als deze knop wordt getoond, selecteert de gebruiker de knop en wordt in de app gevraagd om de sessie te beëindigen. Wanneer de actie wordt bevestigd, wist de browser alle browsegegevens (cookies, cache etc.) en wordt de standaard-URL geopend. Standaard wordt de knop niet weergegeven.

      - **De browser vernieuwen na niet-actieve tijd**: Voer de niet-actieve tijd (1-1440 minuten) in, waarna de kioskbrowser opnieuw wordt gestart en vernieuwd. Niet-actieve tijd is het aantal minuten dat is verstreken sinds de laatste interactie van de gebruiker. De waarde is standaard leeg of blanco, wat inhoudt dat er geen time-out is voor inactiviteit.

      - **Toegestane websites**: Gebruik deze instelling om toe te staan dat bepaalde websites worden geopend. Met andere woorden, gebruik deze functie om het aantal websites dat op het apparaat kan worden geopend, te beperken. U kunt bijvoorbeeld toestaan dat alle websites op `contoso.com*` kunnen worden geopend. Standaard worden alle websites toegestaan.

        Als u alleen bepaalde websites wilt toestaan, moet u een CSV-bestand uploaden dat een lijst met toegestane websites bevat. Als u geen CSV-bestand toevoegt, zijn alle websites toegestaan.

      > [!NOTE]
      > Voor Windows 10-kiosken waarvoor automatische aanmelding is ingeschakeld met Microsoft Kiosk Browser moet u een offline licentie gebruiken uit de Microsoft Store voor Bedrijven. Deze vereiste is van toepassing omdat bij de automatische aanmelding gebruik wordt gemaakt van een lokaal gebruikersaccount zonder AD-referenties (Azure Active Directory). Online licenties kunnen daarom niet worden beoordeeld. Zie [Offline apps distribueren](/microsoft-store/distribute-offline-apps) voor meer informatie.

  - **Toepassingen**

    - **Store-app toevoegen**: Voeg een app toe uit de Microsoft Store voor Bedrijven. Als er geen apps worden weergegeven, kunt u apps aanschaffen en deze [aan Intune toevoegen](../apps/store-apps-windows.md). U kunt bijvoorbeeld Kiosk-Browser, Excel, OneNote en meer toevoegen.

    - **Win32-app toevoegen**: Een Win32-app is een traditionele bureaublad-app, zoals Visual Studio Code of Google Chrome. Voer de volgende eigenschappen in:

      - **Toepassingsnaam**: Vereist. Geef een naam op voor de toepassing.
      - **Lokaal pad naar het uitvoerbare bestand van de app**: Vereist. Voer het pad naar het uitvoerbare bestand in, zoals `C:\Program Files (x86)\Microsoft VS Code\Code.exe` of `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`.
      - **Model-id van toepassingsgebruiker (AUMID) voor de Win32-app**: Voer de AUMID van de Win32-app in. Deze instelling bepaalt de indeling van de tegel na het opstarten op het bureaublad. Raadpleeg [Get-StartApps](/powershell/module/startlayout/get-startapps?view=win10-ps) om deze id op te halen.

    - **Toevoegen via AUMID**: Gebruik deze optie om Postvak IN-apps voor Windows, zoals Kladblok of Calculator toe te voegen. Voer de volgende eigenschappen in:

      - **Toepassingsnaam**: Vereist. Geef een naam op voor de toepassing.
      - **Model-id van toepassingsgebruiker (AUMID)** : Vereist. Voer de AUMID van de Windows-app in. Zie [De model-id van toepassingsgebruiker van een geïnstalleerde app vinden](/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app) als u wilt weten hoe u aan deze id komt.

    - **AutoLaunch**: Optioneel. Nadat u uw apps en browser hebt toegevoegd, selecteert u één app of browser die automatisch moet worden geopend wanneer de gebruiker zich aanmeldt. Er kan slechts één app of browser automatisch worden gestart.
    - **Tegelgrootte**: Vereist. Nadat u uw apps hebt toegevoegd, selecteert u een kleine, middelgrote, brede of grote app-tegelgrootte.

      :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-autolaunch-tiles.png" alt-text="Start de app of browser automatisch en selecteer de tegelgrootte in een kioskprofiel voor meerdere apps in Microsoft Intune.":::

  > [!TIP]
  > Nadat u alle apps hebt toegevoegd, kunt u de volgorde ervan wijzigen door er op te klikken en de apps naar een andere positie op de lijst te slepen.  

- **Alternatieve indeling van het menu Start gebruiken**: Selecteer **Ja** om een XML-bestand op te geven waarin wordt beschreven hoe de apps worden weergegeven in het menu Start, zoals de volgorde van de apps. Gebruik deze optie als u meer aanpassingsmogelijkheden wilt gebruiken in het startmenu. [Indeling Start aanpassen en exporteren](/windows/configuration/customize-and-export-start-layout) biedt een aantal richtlijnen en een XML-voorbeeld.

- **Windows-taakbalk**: Kies of u wilt dat de taakbalk wordt **weergegeven** of **verborgen**. Standaard wordt de taakbalk niet weergegeven. Pictogrammen, zoals het Wi-Fi-pictogram, worden weergegeven, maar de instellingen kunnen niet worden gewijzigd door eindgebruikers.

- **Toegang tot de map Downloads toestaan**: kies **Ja** om gebruikers toegang te verlenen tot de map Downloads in Windows Verkenner. Toegang tot de map Downloads is standaard uitgeschakeld. Deze functie wordt vaak gebruikt voor eindgebruikers om items te openen die zijn gedownload vanuit een browser.

- **Onderhoudsvenster opgeven voor opnieuw opstarten van apps**: Voor sommige apps moet de computer opnieuw worden opgestart om de installatie van de app te voltooien of de installatie van updates te voltooien. Met **Vereisen** wordt een onderhoudsvenster gemaakt. Als apps opnieuw moeten worden gestart, worden deze opnieuw gestart tijdens dit venster.

  Voer ook in:

  - **Begintijd van onderhoudsvenster**: Selecteer de datum en tijd van de dag waarop u clients wilt gaan controleren op app-updates waarvoor opnieuw moet worden gestart. De reguliere begintijd is middernacht, oftewel nul minuten. Als deze leeg is, worden apps op een niet-gepland tijdstip 3 dagen na de installatie van een app-update opnieuw gestart.

  - **Terugkeerpatroon voor onderhoudsvenster**: De standaardinstelling is dagelijks. Selecteer hoe vaak onderhoudsvensters voor app-updates moeten worden uitgevoerd. Om te voorkomen dat apps op een niet-gepland tijdstip opnieuw worden gestart, wordt **Dagelijks** aanbevolen.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook kiosk-profielen maken voor apparaten met [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience) en [Windows Holographic for Business](kiosk-settings-holographic.md).

Zie ook [een kiosk met één app instellen](/windows/configuration/kiosk-single-app) of [een kiosk met meerdere apps instellen](/windows/configuration/lock-down-windows-10-to-specific-apps) in de Windows-richtlijnen.
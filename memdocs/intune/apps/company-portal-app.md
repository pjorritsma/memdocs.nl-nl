---
title: De Intune-bedrijfsportal-apps, de bedrijfsportalwebsite en de Intune-app aanpassen
titleSuffix: Microsoft Intune
description: Lees hoe u de specifieke huisstijl van uw bedrijf kunt toepassen op de Intune-bedrijfsportal-apps, bedrijfsportalwebsite en Intune-app.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/16/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dec6f258-ee1b-4824-bf66-29053051a1ae
ms.reviewer: esthermsft
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6a3152966dee507cde690d9be8f5a7e210c7945
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407756"
---
# <a name="how-to-customize-the-intune-company-portal-apps-company-portal-website-and-intune-app"></a>De Intune-bedrijfsportal-apps, de bedrijfsportalwebsite en de Intune-app aanpassen

Via de bedrijfsportal-apps, de bedrijfsportalwebsite en de Intune-app op Android hebben gebruikers toegang tot bedrijfsgegevens en kunnen ze algemene taken uitvoeren. Algemene taken zijn onder andere apparaten inschrijven, apps installeren en informatie zoeken (zoals hulp van uw IT-afdeling). Daarnaast biedt dit gebruikers een veilige omgeving voor toegang tot bedrijfsresources. De eindgebruikerservaring bevat verschillende pagina's, zoals de startpagina, Apps, App-details, Apparaten en Apparaatdetails. Als u snel apps wilt vinden in de bedrijfsportal, kunt u de apps filteren op de pagina Apps.

## <a name="customizing-the-user-experience"></a>De gebruikerservaring aanpassen

Door de eindgebruikerservaring aan te passen, kunt u uw eindgebruikers een vertrouwde en efficiënte ervaring geven. Ga hiervoor naar het [Beheercentrum voor Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), selecteer **Tenantbeheer** > **Aanpassing** en configureer de vereiste instellingen. Deze instellingen zijn van toepassing op de bedrijfsportal-apps, bedrijfsportalwebsite en Intune-app op Android.

## <a name="branding"></a>Huisstijl

De volgende tabel bevat de gegevens voor huismerkaanpassing voor de eindgebruikerservaring:

| Veldnaam | Meer informatie |
|---|---|---|
| **Organisatienaam** | Deze naam wordt weergegeven in de berichten in de eindgebruikerservaring. Met de instelling **Weergeven in koptekst** kan worden ingesteld dat deze ook wordt weergegeven in kopteksten. De maximale lengte is 40 tekens. |
| **Kleur** | Kies **Standaard** om te kiezen uit vijf standaardkleuren. Kies **Aangepast** om een specifieke kleur te selecteren op basis van een hexadecimale code. |
| **Themakleur** | Stel de kleur van het thema in die u in de eindgebruikerservaring wilt weergeven. De tekstkleur wordt automatisch ingesteld op zwart of wit, zodat deze het best zichtbaar is op de geselecteerde themakleur. |
| **Weergeven in koptekst** | Geef op of de koptekst in de eindgebruikerservaring het **Bedrijfslogo en -naam**, **Alleen bedrijfslogo** of **Alleen bedrijfsnaam** moet bevatten. In de onderstaande voorbeelden worden alleen de logo's weergegeven, niet de naam.  |
| **Logo uploaden voor achtergrondkleur van thema​** | Upload het logo dat u wilt weergeven tegen de achtergrondkleur van het geselecteerde thema. Voor de beste weergave uploadt u een logo met een transparante achtergrond. In het voorbeeldvak onder de instelling kunt u zien hoe dit er uitziet.<p>Maximale afbeeldingsgrootte: 400 x 400 px<br>Maximale bestandsgrootte:   750 KB<br>Bestandstype: PNG, JPG of JPEG |
| **Logo uploaden voor witte of lichte achtergrond​** | Upload het logo dat u wilt weergeven tegen een witte of lichtgekleurde achtergrond. Voor de beste weergave uploadt u een logo met een transparante achtergrond. In het voorbeeldvak onder de instelling kunt u zien hoe dit er uitziet tegen een witte achtergrond.<p>Maximale afbeeldingsgrootte: 400 x 400 px<br>Maximale bestandsgrootte: 750 KB<br>Bestandstype: PNG, JPG of JPEG |
| **Merkafbeelding uploaden​** | Upload een afbeelding die het merk van uw organisatie weergeeft.<p><ul><li>Aanbevolen breedte van afbeelding: Groter dan 1125 pixels (minimaal 650 pixels vereist)</li><li>Maximale afbeeldingsgrootte: 1,3 MB</li><li>Bestandstype: PNG, JPG of JPEG</li><li>Deze wordt weergegeven op de volgende locaties:</li><ul><li>Bedrijfsportal voor iOS/iPadOS: Achtergrondafbeelding op de profielpagina van de gebruiker.</li><li>Bedrijfsportalwebsite:   Achtergrondafbeelding op de profielpagina van de gebruiker.</li><li>Intune-app voor Android: In de lade en als achtergrondafbeelding op de profielpagina van de gebruiker.</li></ul></ul> |

> [!NOTE]
> Wanneer een gebruiker een iOS/iPadOS-toepassing installeert vanuit de bedrijfsportal wordt er een prompt weergegeven. Dit doet zich voor wanneer de iOS/iPadOS-app is gekoppeld aan de App Store, aan een volume-aankoopprogramma (VPP) of aan een Line-Of-Business-app (LOB). Met de prompt kunnen gebruikers de actie accepteren of het beheer van de app toestaan. In de prompt wordt uw bedrijfsnaam weergegeven. Wanneer uw bedrijfsnaam niet beschikbaar is, wordt **Bedrijfsportal** weergegeven.

### <a name="brand-image-best-practices"></a>Best practices voor merkafbeeldingen

Met de juiste merkafbeelding kan het vertrouwen van de gebruiker worden versterkt door een sterke aanwezigheid van het merk van uw organisatie. Hier volgen enkele tips die u kunt gebruiken voor het verkrijgen, kiezen en optimaliseren van de afbeelding voor de weergavelocaties.

- Neem contact op met uw marketing- of huisstijlafdeling. Mogelijk beschikken zij al over een goedgekeurde set afbeeldingen. Wellicht kunnen ze u ook helpen bij het naar behoefte optimaliseren van afbeeldingen.
- Houd rekening met zowel liggende als staande weergave. De afbeelding moet voldoende achtergrond rond het centrale punt hebben. De afbeelding wordt mogelijk verschillend bijgesneden op basis van apparaatgrootte, -oriëntatie en platform.
- Vermijd het gebruik van een standaardafbeelding. De afbeelding moet het merk en de identiteit van uw organisatie uitstralen, zoals de gebruikers dit kennen. Als u geen geschikte afbeelding hebt, kunt u beter helemaal geen afbeelding gebruiken, dan te kiezen voor een afbeelding die voor de gebruiker geen betekenis heeft.
- Verwijder onnodige metagegevens. Afbeeldingsbestanden bevatten soms metagegevens, zoals een cameraprofiel, geografische locatie, titel, bijschrift, enzovoort. Gebruik een hulpprogramma voor afbeeldingoptimalisatie voor het verwijderen van deze gegevens. Zo blijft de kwaliteit behouden en kunt u voldoet aan de maximale bestandsgrootte.

### <a name="brand-image-examples"></a>Voorbeelden van merkafbeeldingen

In de volgende afbeelding ziet u een voorbeeld van de merkafbeelding op een iPhone:

<img alt="Screenshot of example iPhone branding image" src="./media/company-portal-app/company-portal-app-01.png" width="250">

Hieronder ziet u een voorbeeld van de merkafbeelding in de Intune-app voor Android:

<img alt="Screenshot of example #1 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-02.png" width="250">

<img alt="Screenshot of example #2 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-03.png" width="250">

## <a name="support-information"></a>Ondersteuningsinformatie

Voer de ondersteuningsinformatie van uw organisatie in, zodat werknemers voor vragen contact met u kunnen opnemen. Deze ondersteuningsinformatie wordt in de gehele eindgebruikerservaring weergegeven op de pagina's **Ondersteuning**, **Help en ondersteuning** en **Helpdesk**.

| Veldnaam | Maximale lengte | Meer informatie |
|------------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Naam van contactpersoon | 40 | Dit is de naam van de persoon met wie gebruikers contact hebben wanneer ze contact opnemen met Ondersteuning. |
| Telefoonnummer | 20 | Dit nummer kunnen gebruikers bellen om contact op te nemen voor ondersteuning. |
| E-mailadres | 40 | Naar dit e-mailadres kunnen gebruikers e-mailberichten sturen voor ondersteuning. U moet een geldig e-mailadres invoeren in de notatie `alias@domainname.com`. |
| Naam website | 40 | Dit is de beschrijvende naam die op een aantal locaties wordt weergegeven voor de URL naar de ondersteuningswebsite. Als u de URL van een ondersteuningswebsite zonder beschrijvende naam opgeeft, wordt de URL zelf in de eindgebruikerservaring weergegeven.  |
| URL van website | 150 | De ondersteuningswebsite die gebruikers moeten gebruiken. De URL moet in de notatie `https://www.contoso.com` worden opgegeven.  |
| Aanvullende informatie | 120 | Voeg hier aanvullende berichten met betrekking tot ondersteuningsberichten aan gebruikers toe. |

## <a name="configuration"></a>Configuration

De volgende tabel bevat aanvullende configuratiegegevens:

| Veldnaam | Maximale lengte | Meer informatie |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| URL voor de privacyverklaring | 79 | Stel de privacyverklaring van uw organisatie in zodat deze wordt weergegeven wanneer gebruikers op privacykoppelingen klikken. U moet een geldige URL opgeven in de notatie `https://www.contoso.com`. |
| Privacybericht in de bedrijfsportal voor iOS​/iPadOS | 520 | Behoud de standaardinstelling of stel een Aangepast bericht in om de items weer te geven die uw organisatie wel of niet kan zien op beheerde iOS- en iPadOS-apparaten. U kunt Markdown gebruiken om opsommingstekens, vet, cursief en koppelingen toe te voegen. |
| Apparaatinschrijving | N.v.t. | Geef op of en hoe gebruikers moeten worden gevraagd om zich in te schrijven bij Mobile Device Management. Zie hieronder voor meer informatie. |

### <a name="device-enrollment-setting-options"></a>Opties voor het instellen van apparaatinschrijving

> [!NOTE]
> Voor ondersteuning van de instelling voor het inschrijven van apparaten moeten eindgebruikers beschikken over deze bedrijfsportalversies:
> - Bedrijfsportal op iOS/iPadOS: versie 4.4 of hoger
> - Bedrijfsportal op Android: versie 5.0.4715.0 of hoger 

|    Opties voor apparaatinschrijving    |    Beschrijving    |    Controlevragen    |    Melding    |    Status van apparaatgegevens    |    Status van app-details (van een app waarvoor inschrijving is vereist)    |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------|--------------------|-----------------------------|--------------------------------------------------------------------|
|    Beschikbaar, met prompts    |    De standaardervaring met prompts voor inschrijving op alle mogelijke locaties.    |    Ja    |    Ja    |    Ja    |    Ja    |
|    Beschikbaar, geen prompts    |    De gebruiker kan een apparaat inschrijven via de status in Apparaatgegevens voor zijn/haar huidige apparaat of vanuit apps waarvoor inschrijving is vereist.    |    Nee    |    Nee    |    Ja    |    Ja    |
|    Niet beschikbaar    |    Gebruikers kunnen een apparaat niet inschrijven.    |    Nee    |    Nee    |    Nee    |    Nee<sup>(1)</sup>    |

<sup>(1)</sup> **Bekend probleem:** Als u apps zo instelt dat inschrijving voor installatie is vereist en als u eveneens apparaatinschrijving instelt op 'Niet beschikbaar', worden gebruikers in de bedrijfsportal-app op Android alsnog geholpen bij de inschrijving. Dit wordt binnenkort verwijderd.

> [!NOTE]
> Als u gebruikmaakt van Azure Government, worden er app-logboeken aangeboden aan de eindgebruiker zodat deze kan beslissen hoe deze de logboeken graag wil delen wanneer er een probleem moet worden opgelost. Als u geen gebruik maakt van Azure Government, worden app-logboeken rechtstreeks vanuit de bedrijfsportal naar Microsoft verzonden wanneer de gebruiker hulp nodig heeft bij het oplossen van een probleem. Als de app-logboeken naar Microsoft worden verzonden, is het eenvoudiger om problemen op te lossen.

> [!NOTE]
> Conform beleid van Microsoft en Apple verkopen we gegevens die met onze service zijn verzameld om geen enkele reden aan externe partijen.

## <a name="company-portal-derived-credentials-for-iosipados-devices"></a>Van de bedrijfsportal afgeleide referenties voor iOS/iPadOS-apparaten

Intune ondersteunt referenties die zijn afgeleid van Personal Identity Verification (PIV) en Common Access Card (CAC), in samenwerking met de referentieproviders DISA Purebred, Entrust Datacard en Intercede. Eindgebruikers voeren na inschrijving aanvullende stappen uit op hun iOS/iPadOS-apparaat om hun identiteit te verifiëren in de toepassing Bedrijfsportal. Afgeleide referenties worden ingeschakeld voor gebruikers door eerst een referentieprovider voor uw tenant in te stellen en vervolgens een profiel dat gebruikmaakt van afgeleide referenties te richten op gebruikers of apparaten.

> [!NOTE]
> De gebruiker ziet instructies over afgeleide referenties op basis van de koppeling die u via Intune hebt opgegeven.

Zie [Afgeleide referenties gebruiken in Microsoft Intune](../protect/derived-credentials.md) voor meer informatie over afgeleide referenties voor iOS/iPadOS-apparaten.

## <a name="dark-mode-for-iosipados-company-portal"></a>Donkere modus voor iOS/iPadOS-bedrijfsportal

Donkere modus is beschikbaar voor de iOS/iPadOS-bedrijfsportal. Gebruikers kunnen apps downloaden, hun apparaten beheren en IT-ondersteuning krijgen in het gewenste kleurenschema op basis van hun apparaatinstellingen. De iOS/iPadOS-bedrijfsportal wordt automatisch afgestemd op de apparaatinstellingen van de eindgebruiker voor donkere of lichte modus.

## <a name="windows-company-portal-keyboard-shortcuts"></a>Sneltoetsen voor Windows-bedrijfsportal

Eindgebruikers kunnen navigatie-, app- en apparaatacties in de Windows-bedrijfsportal activeren met behulp van sneltoetsen (accelerators).

De volgende sneltoetsen zijn beschikbaar in de Windows-bedrijfsportal-app.

| Gebied | Beschrijving | Sneltoets |
|:------------------:|:--------------:|:-----------------:|
| Navigatiemenu | Navigatie | Alt+M |
|  | Home | Alt+H |
|  | Alle apps | Alt+A |
|  | Geïnstalleerde apps | Alt+I |
|  | Feedback verzenden | Alt+F |
|  | Mijn profiel | Alt+U |
|  | Instellingen | Alt+T |
| Startpagina - Apparaattegel | Naam wijzigen | F2 |
|  | Verwijderen | Ctrl+D of Delete |
|  | Toegang controleren | Ctrl+M of F9 |
| Apparaatgegevens | Naam wijzigen | F2 |
|  | Verwijderen | Ctrl+D of Delete |
|  | Toegang controleren | Ctrl+M of F9 |
| App-details | Installeren | Ctrl+I |
| Apparaten | Beschikbaar | Ctrl+D |

Eindgebruikers zien ook de beschikbare snelkoppelingen in de Bedrijfsportal-app in Windows.

![Schermafbeelding van beschikbare sneltoetsen in de Windows-bedrijfsportal](./media/company-portal-app/company-portal-app-04.png)

## <a name="user-self-service-device-actions-from-the-company-portal"></a>Apparaatacties voor selfservicegebruikers van de bedrijfsportal

Gebruikers kunnen acties uitvoeren op hun lokale of externe apparaten via de bedrijfsportal-app of -website of de Intune-app op Android. De acties die gebruikers kunnen uitvoeren, kunnen per platform en configuratie van het apparaat verschillen. In alle gevallen kunnen de acties van het externe apparaat alleen worden uitgevoerd door de primaire gebruiker van het apparaat.

- **Buiten gebruik stellen**: hiermee wordt het apparaat uit Intune verwijderd. In de app en op de website van de bedrijfsportal wordt dit weergegeven als **Verwijderen**.
- **Wissen**: met deze actie wordt het apparaat opnieuw ingesteld. Op de website van de bedrijfsportal wordt dit weergegeven als **Opnieuw instellen** en als **Fabrieksinstellingen** in de iOS/iPadOS-bedrijfsportal-app.
- **Naam wijzigen**: met deze actie wijzigt u de apparaatnaam die de gebruiker kan zien in de bedrijfsportal. Alleen de vermelding in de bedrijfsportal wordt gewijzigd. De naam van het lokale apparaat wordt niet gewijzigd.
- **Synchroniseren**: met deze actie wordt een apparaat ingecheckt bij de Intune-service. Dit wordt weergegeven als **Status controleren** in de bedrijfsportal.
- **Extern vergrendelen**: hiermee wordt het apparaat vergrendeld en is een pincode vereist om het apparaat weer te ontgrendelen.
- **Wachtwoordcode opnieuw instellen**: deze actie wordt gebruikt om de wachtwoordcode van het apparaat opnieuw in te stellen. Op iOS/iPadOS-apparaten wordt de wachtwoordcode verwijderd en moet de eindgebruiker een nieuwe code invoeren in Instellingen. Op ondersteunde Android-apparaten wordt een nieuwe wachtwoordcode gegenereerd door Intune, die tijdelijk wordt weergegeven in de bedrijfsportal.
- **Sleutelherstel**: deze actie wordt gebruikt om een persoonlijke herstelsleutel te herstellen voor versleutelde macOS-apparaten vanaf de Bedrijfsportal-website. 

### <a name="self-service-actions"></a>Selfserviceacties

Voor sommige platforms en configuraties zijn geen selfserviceacties voor apparaten toegestaan. De onderstaande tabel bevat meer informatie over selfserviceacties:

|  | Windows 10<sup>(3)</sup> | iOS/iPadOS<sup>(3)</sup> | MacOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Buiten gebruik stellen | Beschikbaar<sup>(1)</sup> | Beschikbaar | Beschikbaar | Beschikbaar<sup>(7)</sup> |
| Wissen | Beschikbaar | Beschikbaar<sup>(5)</sup> | NA | Beschikbaar<sup>(7)</sup> |
| Naam wijzigen<sup>(4)</sup> | Beschikbaar | Beschikbaar | Beschikbaar | Beschikbaar |
| Synchroniseren | Beschikbaar | Beschikbaar | Beschikbaar | Beschikbaar |
| Vergrendelen op afstand | Alleen Windows Phone | Beschikbaar | Beschikbaar | Beschikbaar |
| Wachtwoordcode opnieuw instellen | Alleen Windows Phone | Beschikbaar<sup>(8)</sup> | NA | Beschikbaar<sup>(6)</sup> |
| Sleutelherstel | NA | NA | Beschikbaar<sup>(2)</sup> | NA |

<sup>(1)</sup> **Buiten gebruik stellen** wordt altijd geblokkeerd op Windows-apparaten die zijn toegevoegd aan Azure AD.<br>
<sup>(2)</sup> **Sleutelherstel** voor MacOS is alleen beschikbaar via de webportal.<br>
<sup>(3) </sup> Alle externe acties worden uitgeschakeld als u een Apparaatinschrijvingsmanager-inschrijving gebruikt.<br>
<sup>(4)</sup> Met **Naam wijzigen** wordt alleen de apparaatnaam in de app of webportal van de bedrijfsportal gewijzigd, niet op het apparaat zelf.<br>
<sup>(5)</sup> **Wissen** is niet beschikbaar op door de gebruiker ingeschreven iOS/iPadOS-apparaten.<br>
<sup>(6)</sup> **Wachtwoordcode opnieuw instellen** wordt niet ondersteund in bepaalde Android- en Android Enterprise-configuraties. Zie [De wachtwoordcode van een apparaat opnieuw instellen of verwijderen via Intune](../remote-actions/device-passcode-reset.md) voor meer informatie.<br>
<sup>(7)</sup> **Buiten gebruik stellen** en **Wissen** is niet beschikbaar in Android Enterprise-apparaateigenaarscenario's (COPE, COBO, COSU).<br> 
<sup>(8)</sup> **Wachtwoordcode opnieuw instellen** wordt niet ondersteund voor door de gebruiker ingeschreven iOS/iPadOS-apparaten.

## <a name="next-steps"></a>Volgende stappen

- [Apps toevoegen](apps-add.md)

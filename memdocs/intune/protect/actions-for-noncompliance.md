---
title: Melding van niet-compatibele apparaten en acties met Microsoft Intune - Azure | Microsoft Docs
description: Maak een e-mailmelding om te verzenden naar niet-compatibele apparaten. Voeg acties toe om van toepassing te zijn op apparaten die niet voldoen aan uw nalevingsbeleid. Acties kunnen een respijtperiode omvatten om compatibel te zijn, toegang tot netwerkresources te blokkeren of het niet-compatibele apparaat buiten gebruik te stellen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9e5786289e54071d54c11fbb08790e95e54a9377
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461858"
---
# <a name="configure-actions-for-noncompliant-devices-in-intune"></a>Acties configureren voor niet-compatibele apparaten in Intune

Voor apparaten die niet aan uw nalevingsbeleid of -regels voldoen, kunt u **Acties voor niet-naleving** toevoegen. Met deze functie configureert u een reeks chronologische acties, zoals het versturen van e-mailberichten naar eindgebruikers, en meer.

## <a name="overview"></a>Overzicht

Elk nalevingsbeleid bevat standaard de actie voor niet-naleving van **Apparaat als niet-compatibel markeren** met een planning van nul dagen (**0**). Het resultaat van deze standaardactie is dat wanneer Intune een apparaat detecteert dat niet compatibel is, Intune het apparaat onmiddellijk als niet-compatibel markeert. Nadat een apparaat als niet-compatibel is gemarkeerd, kan [Voorwaardelijke toegang](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) van Azure Active Directory (AD) het apparaat vervolgens blokkeren.

Door **acties voor niet-naleving** te configureren, krijgt u meer flexibiliteit om te bepalen wat er moet gebeuren met niet-compatibele apparaten en wanneer u dit moet doen. U kunt er bijvoorbeeld voor kiezen het apparaat niet onmiddellijk te blokkeren en de gebruiker een respijtperiode te bieden om ervoor te zorgen dat het apparaat weer compatibel wordt.

Voor elke actie die u instelt, kunt u een planning configureren die bepaalt wanneer die actie van kracht wordt. De planning neemt een aantal dagen in beslag waarna het apparaat wordt gemarkeerd als niet-compatibel. U kunt ook meerdere exemplaren van een actie configureren. Wanneer u meerdere exemplaren van een actie in een beleid instelt, wordt de actie opnieuw uitgevoerd op die later geplande tijd als het apparaat niet-compatibel blijft.

Niet alle acties zijn beschikbaar voor alle platforms.

## <a name="available-actions-for-noncompliance"></a>Beschikbare acties voor niet-naleving

Hieronder vindt u de beschikbare acties voor niet-naleving. Tenzij anders vermeld, is elke actie beschikbaar voor alle platformen die door Intune worden ondersteund:

- **Apparaat markeren als niet-compatibel**: Deze actie is standaard ingesteld voor elk nalevingsbeleid en heeft een planning van nul (**0**) dagen, waarbij apparaten direct worden gemarkeerd als niet-compatibel.

  Wanneer u de standaardplanning wijzigt, geeft u een respijtperiode op waarin een gebruiker problemen kan oplossen of zorgen dat het apparaat compatibel wordt zonder dat deze als niet-compatibel wordt gemarkeerd.

- **E-mail verzenden naar de eindgebruiker**: Met deze actie wordt een e-mailmelding verzonden naar de gebruiker.
Handel als volgt wanneer u deze actie inschakelt:

  - Selecteer een *sjabloon voor meldingsberichten* die door deze actie wordt verzonden. U moet [Een sjabloon voor een meldingsbericht maken](#create-a-notification-message-template) voordat u er eentje kunt toewijzen aan deze actie. Wanneer u de aangepaste melding maakt, past u het onderwerp en de hoofdtekst van het bericht aan en kunt u het bedrijfslogo, de bedrijfsnaam en aanvullende contactgegevens opnemen.
  - U kunt ervoor kiezen om het bericht naar extra ontvangers te verzenden door een of meer van uw Azure AD-groepen te selecteren.

Wanneer het e-mailbericht wordt verzonden, geeft Intune meer informatie over het apparaat dat niet compatibel is in het e-mailbericht.

- **U kunt het niet-compatibele apparaat als volgt op afstand vergrendelen**: Gebruik deze actie om een externe vergrendeling van een apparaat uit te brengen. De gebruiker wordt vervolgens gevraagd een pincode of wachtwoord in te voeren om het apparaat te ontgrendelen. Meer over de functie [Extern vergrendelen](../remote-actions/device-remote-lock.md).

  Deze actie wordt ondersteund op de volgende platforms:
  - Android:
    - Android-apparaatbeheerder
    - Volledig beheerd, toegewezen Android-werkprofiel in bedrijfseigendom
    - Android Enterprise-werkprofiel
    - Kioskapparaten voor Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 en hoger

- **Het niet-compatibele apparaat buiten gebruik stellen**: Met deze actie verwijdert u alle bedrijfsgegevens van het apparaat en verwijdert u het apparaat uit Intune-beheer. Er wordt een minimale planning van **30** dagen ondersteund om te voorkomen dat u een apparaat per ongeluk wist.

  Deze actie wordt ondersteund op de volgende platforms:
  - Android:
    - Android-apparaatbeheerder
    - Android Enterprise-apparaateigenaar
    - Android Enterprise-werkprofiel
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 en hoger

  Meer informatie over het [buiten gebruik stellen van apparaten](../remote-actions/devices-wipe.md#retire).

- **Pushmelding verzenden naar eindgebruiker**: Configureer deze actie voor het verzenden van een pushmelding over niet-naleving van een apparaat via de bedrijfsportal app of de Intune-app op het apparaat.

  Deze actie wordt ondersteund op de volgende platforms:
  - Android:
    - Android-apparaatbeheerder
    - Android Enterprise-apparaateigenaar
    - Android Enterprise-werkprofiel
  - iOS/iPadOS

  De pushmelding wordt voor het eerst verzonden wanneer een apparaat wordt ingecheckt bij Intune en wanneer is vastgesteld dat het apparaat niet compatibel is met het nalevingsbeleid. Wanneer een gebruiker de melding selecteert, wordt de bedrijfsportal-app of de Intune-app geopend en wordt er informatie weergegeven over waarom ze niet compatibel zijn. De gebruiker kan vervolgens actie ondernemen om het probleem op te lossen. De berichtgegevens over niet-naleving worden gegenereerd door Intune en kunnen niet worden aangepast.

  > [!IMPORTANT]
  > Intune, de bedrijfsportal-app en de Microsoft Intune-app kunnen niet garanderen dat er een pushmelding wordt afgeleverd. Meldingen kunnen na enkele uren vertraging worden weergegeven, of helemaal niet. Dit geldt ook wanneer gebruikers pushmeldingen hebben uitgeschakeld.
  >
  > Vertrouw niet op deze meldingsmethode voor dringende berichten.

  Elk exemplaar van de actie verzendt één keer een melding. Als u dezelfde melding opnieuw wilt verzenden vanuit een beleid, configureert u aanvullende exemplaren van de actie in dat beleid, elk met een andere planning.
  
  U kunt bijvoorbeeld de eerste actie voor nul dagen plannen en vervolgens een tweede exemplaar van de actie toevoegen dat op drie dagen is ingesteld. Door deze vertraging voor de tweede melding krijgt de gebruiker enkele dagen de tijd om het probleem op te lossen en de tweede melding te vermijden.

  Als u wilt voorkomen dat u gebruikers met te veel dubbele berichten spamt, controleert en stroomlijnt u welk nalevingsbeleid een pushmelding voor niet-naleving omvat en bekijkt u de planningen om te voorkomen dat de meldingen voor hetzelfde te vaak worden verzonden.

  Overweeg het volgende:
  - Voor één beleid dat meerdere exemplaren van een pushmelding voor dezelfde dag bevat, wordt slechts één melding voor die dag verzonden.

  - Wanneer meerdere nalevingsbeleidsregels dezelfde nalevingsvoorwaarden en de pushmeldingsactie met dezelfde planning bevatten, verzend Intune er op dezelfde dag meerdere meldingen naar hetzelfde apparaat.

## <a name="before-you-begin"></a>Voordat u begint

U kunt [acties voor niet-naleving toevoegen](#add-actions-for-noncompliance) wanneer u nalevingsbeleid voor apparaten configureert of op een later tijdstip, door het beleid te bewerken. U kunt aan elk beleid extra acties toevoegen om aan uw behoeften te voldoen. Onthoud dat elk nalevingsbeleid automatisch de standaardactie voor niet-naleving bevat waarmee apparaten worden aangemerkt als niet-compatibel, waarbij een planning is ingesteld op nul dagen.

Wanneer u nalevingsbeleid gebruikt om toegang tot bedrijfsresources door apparaten te blokkeren, moet voorwaardelijke toegang voor Azure AD zijn ingesteld. Zie [Voorwaardelijke toegang in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) of [Gebruikelijke manieren om voorwaardelijke toegang met Intune te gebruiken](conditional-access-intune-common-ways-use.md) voor instructies.

Zie de volgende platform-specifieke richtlijnen om een nalevingsbeleid voor apparaten te maken:

- [Android](compliance-policy-create-android.md)
- [Android-werkprofielen](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [macOS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## <a name="create-a-notification-message-template"></a>Een sjabloon voor een meldingsbericht maken

Maak een sjabloon voor berichtmeldingen om een e-mail naar uw gebruikers te versturen. Wanneer een apparaat niet conform is, worden de gegevens die u in de sjabloon invoert, weergegeven in de e-mail die naar uw gebruikers wordt verzonden.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer (**Eindpuntbeveiliging** > **Apparaatnaleving** > **Meldingen** > **Melding maken**).
3. Geef onder *Basisprincipes* de volgende informatie op:

   - **Naam**
   - **Onderwerp**
   - **Bericht**

4. Configureer, ook onder *Basisprincipes*, de volgende opties voor de melding:

   - **E-mailkoptekst - Bedrijfslogo opnemen** (standaardinstelling = *Inschakelen*): het logo dat u uploadt als onderdeel van de huisstijl voor de bedrijfsportal, zal worden gebruikt voor e-mailsjablonen. Zie [Aanpassing bedrijfshuisstijl](../apps/company-portal-app.md#customizing-the-user-experience) voor meer informatie over de huisstijl voor de bedrijfsportal.
   - **E-mailvoettekst - Bedrijfsnaam opnemen** (standaardinstelling = *Inschakelen*)
   - **E-mailvoettekst - Contactgegevens opnemen** (standaardinstelling = *Inschakelen*)
   - **Koppeling naar website van bedrijfsportal** (standaardinstelling = *Uitschakelen*): wanneer deze optie is ingesteld op *Inschakelen*, bevat het e-mailbericht een koppeling naar de Bedrijfsportalwebsite.

   > [!div class="mx-imgBorder"]
   > ![Voorbeeld van een compatibel meldingsbericht in Intune](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Selecteer **Volgende** om door te gaan.

5. Controleer onder **Controleren en maken** de configuraties, zodat u zeker weet dat de sjabloon voor het meldingsbericht gereed is voor gebruik. Selecteer **Maken** om de melding te voltooien.

> [!NOTE]
> U kunt ook een meldingssjabloon selecteren die u eerder hebt gemaakt en de gegevens **bewerken** om de sjabloon bij te werken.

## <a name="add-actions-for-noncompliance"></a>Acties voor niet-naleving toevoegen

Wanneer u een nalevingsbeleid voor apparaten maakt, maakt Intune automatisch een actie voor niet-naleving. Als een apparaat niet voldoet aan uw nalevingsbeleid, markeert deze actie het apparaat als niet-compatibel. U kunt aanpassen hoe lang het apparaat wordt gemarkeerd als niet compatibel. Deze actie kan niet worden verwijderd.

U kunt optionele acties toevoegen wanneer u een nalevingsbeleid maakt of wanneer u een bestaand beleid bijwerkt.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Nalevingsbeleid** > **Beleid**, selecteer een van uw beleidsregels en selecteer **Eigenschappen**.

   Heeft u nog geen beleid? Maak een beleid voor een [Android-](compliance-policy-create-android.md), [iOS-](compliance-policy-create-ios.md), [Windows-](compliance-policy-create-windows.md) platform of een ander platform.

   > [!NOTE]
   > JAMF-apparaten en apparaten die worden toegepast op apparaatgroepen kunnen momenteel geen nalevingsacties ontvangen.

3. Selecteer **Acties voor niet-naleving** > **Toevoegen**.

4. Selecteer uw **actie**:

   - **E-mail verzenden naar eindgebruikers**: Wanneer het apparaat niet compatibel is, kunt u de gebruiker een e-mail sturen. Ook:
     - De **berichtsjabloon** kiezen die u eerder hebt gemaakt
     - Eventuele **extra ontvangers** invoeren door groepen te selecteren

   - **U kunt het niet-compatibele apparaat als volgt op afstand vergrendelen**: Als het apparaat niet compatibel is, vergrendelt u het apparaat. De gebruiker moet een pincode of wachtwoord invoeren om het apparaat te ontgrendelen.

   - **Het niet-compatibele apparaat buiten gebruik stellen**: Wanneer het apparaat niet compatibel is, verwijdert u alle bedrijfsgegevens van het apparaat en verwijdert u het apparaat uit Intune-beheer.

   - **Pushmelding verzenden naar eindgebruiker**: Configureer deze actie voor het verzenden van een pushmelding over niet-naleving van een apparaat via de bedrijfsportal app of de Intune-app op het apparaat.

5. Een **planning** configureren: Voer het aantal dagen (0 tot 365) na niet-naleving in voor het activeren van de actie op apparaten van gebruikers. (*Het niet-compatibele apparaat buiten gebruik stellen* ondersteunt een minimum van 30 dagen.) Na deze respijtperiode kunt u een beleid voor [voorwaardelijke toegang](conditional-access-intune-common-ways-use.md) afdwingen. Als u **0** (nul) dagen invoert, wordt de voorwaardelijke toegang **onmiddellijk** van kracht. Als bijvoorbeeld een apparaat niet-compatibel is, gebruikt u voorwaardelijke toegang om onmiddellijk toegang tot e-mail, SharePoint en andere organisatieresources te blokkeren.

   Wanneer u een compliancebeleid maakt, wordt de actie **Het apparaat als niet-compatibel markeren** automatisch gemaakt en ingesteld op **0** dagen (onmiddellijk). Wanneer het apparaat met deze actie incheckt, wordt het apparaat onmiddellijk gemarkeerd als niet-compatibel. Als u ook voorwaardelijke toegang, wordt voorwaardelijke toegang automatisch geactiveerd. Als u een respijtperiode wilt toestaan, wijzigt u de **Planning** in de actie **Het apparaat als niet-compatibel markeren**.

   In uw compliancebeleid wilt u bijvoorbeeld ook de gebruiker op de hoogte stellen. U kunt de actie **E-mail verzenden naar de eindgebruiker** toevoegen. In de actie **E-mail verzenden** stelt u de **Planning** in op twee dagen. Als het apparaat of de eindgebruiker op de tweede dag nog steeds wordt beoordeeld als niet-compatibel, wordt uw e-mail op de tweede dag verzonden. Als u de gebruiker op de vijfde dag nog een keer wilt mailen over de niet-compatibele status, voegt u nog een actie toe en stelt u de **Planning** in op vijf dagen.

   Voor meer informatie over compliance en de ingebouwde acties, raadpleegt u het [complianceoverzicht](device-compliance-get-started.md).

6. Wanneer u klaart bent, selecteert u **Toevoegen** > **OK** om uw wijzigingen op te slaan.

## <a name="next-steps"></a>Volgende stappen

[Controleer uw beleidsregels](compliance-policy-monitor.md).

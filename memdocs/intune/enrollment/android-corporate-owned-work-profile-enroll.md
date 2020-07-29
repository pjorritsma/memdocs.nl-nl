---
title: Intune-inschrijving instellen voor zakelijke Android Enterprise-apparaten met een werkprofiel
titleSuffix: Microsoft Intune
description: Kom meer te weten over het inschrijven van zakelijke Android Enterprise-apparaten met een werkprofiel in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4934115915c41d696258aa54ee8f4b7c84d1809c
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86464977"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-corporate-owned-devices-with-work-profile"></a>Intune-inschrijving instellen voor zakelijke Android Enterprise-apparaten met een werkprofiel

Zakelijke Android Enterprise-apparaten met een werkprofiel zijn apparaten met één gebruiker die zijn bedoeld voor zakelijk en persoonlijk gebruik.

Eindgebruikers kunnen hun werk- en persoonsgegevens gescheiden houden en er zeker van zijn dat hun persoonlijke gegevens en toepassingen privé blijven. Beheerders kunnen sommige instellingen en functies voor het hele apparaat beheren, waaronder:

- Wachtwoordvereisten instellen voor het apparaat
- Bluetooth en gegevensroaming beheren
- Bescherming voor het opnieuw instellen van fabrieksinstellingen configureren

Intune helpt u met de implementatie van apps en instellingen op zakelijke Android Enterprise-apparaten met een werkprofiel. Zie [Android Enterprise-vereisten](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) voor specifieke informatie over Android Enterprise.

## <a name="device-requirements"></a>Vereisten voor apparaten

Apparaten moeten voldoen aan de volgende vereisten om te worden beheerd als zakelijke Android Enterprise-apparaten met een werkprofiel:

- Android-besturingssysteemversie 8.0 en hoger.
- Op de apparaten moet een verdeling van Android worden uitgevoerd die connectiviteit met GMS (Google Mobile Services) heeft. Op de apparaten moet GMS beschikbaar zijn en de apparaten moeten in staat zijn om verbinding te maken met GMS.

## <a name="set-up-android-enterprise-corporate-owned-work-profile-device-management"></a>Zakelijke Android Enterprise-apparaten met een werkprofiel instellen

Volg deze stappen om zakelijke Android Enterprise-apparaten met een werkprofiel in te stellen:

1. U moet de [MDM-instantie instellen op **Microsoft Intune**](../fundamentals/mdm-authority-set.md) als voorbereiding op het beheer van mobiele apparaten. U stelt de instantie slechts één keer in, wanneer u Intune voor het eerst instelt voor het beheer van mobiele apparaten.
2. [Verbind uw Intune-tenantaccount met uw Beheerde Google Play-account](connect-intune-android-enterprise.md).
3. [Maak een inschrijvingsprofielprofiel](#create-an-enrollment-profile).
4. [Maak een apparaatgroep](#create-a-device-group).
5. [Schrijf de zakelijke apparaten met een werkprofiel in](#enroll-the-corporate-owned-work-profile-devices).

### <a name="create-an-enrollment-profile"></a>Een inschrijvingsprofiel maken

> [!NOTE]
> Tokens voor bedrijfseigendommen met een werkprofiel kunnen niet automatisch verlopen. Als een beheerder besluit een token in te trekken, wordt het profiel dat eraan is gekoppeld niet weergegeven in **Apparaten** > **Android** > **Android-inschrijving** > **Apparaten in bedrijfseigendom met werkprofiel (preview-versie)** . Als u alle profielen wilt zien die zijn gekoppeld aan zowel actieve als niet-actieve tokens, klikt u op **Filteren** en schakelt u de vakjes in voor de beleidsstatussen Actief en Niet-actief. 

U moet een inschrijvingsprofiel maken zodat gebruikers zakelijke apparaten met een werkprofiel kunnen inschrijven. Bij het maken van het profiel ontvangt u een inschrijvingstoken (willekeurige tekenreeks) en een QR-code. Afhankelijk van het Android-besturingssysteem en de versie van het apparaat kunt u het token of de QR-code gebruiken om [het toegewezen apparaat in te schrijven](#enroll-the-corporate-owned-work-profile-devices).

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en kies **Apparaten** > **Android** > **Android-inschrijving** > **Apparaten in bedrijfseigendom met werkprofiel (preview-versie)** .
2. Kies **Profiel maken** en vul de vereiste velden in.
    - **Naam**: Typ een naam die u gebruikt wanneer u het profiel toewijst aan de dynamische apparaatgroep.
    - **Beschrijving**: Voeg een profielbeschrijving toe (optioneel).
3. Kies **Volgende**.
5. Kies op de pagina **Beoordelen en maken** de optie **Maken** om het profiel te maken.

### <a name="create-a-device-group"></a>Een apparaatgroep maken

U kunt apps en beleidsregels zenden naar toegewezen of dynamische apparaatgroepen. U kunt dynamische Azure AD-apparaatgroepen configureren om apparaten die zijn geregistreerd met een bepaald inschrijvingsprofiel automatisch te vullen door deze stappen te volgen:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en kies **Groepen** > **Alle groepen** > **Nieuwe groep**.
2. Vul in de blade **Groep** de vereiste velden als volgt in:
    - **Groepstype**: Beveiliging
    - **Groepsnaam**: Typ een intuïtieve naam (bijvoorbeeld Factory 1-apparaten)
    - **Type lidmaatschap**: Dynamisch apparaat
3. Kies **Dynamische query toevoegen**.
4. Vul in de blade **Dynamisch-lidmaatschapregels** de velden als volgt in:
    - **Regel voor dynamisch lidmaatschap toevoegen**: Eenvoudige regel
    - **Locatie voor het toevoegen van apparaten**: enrollmentProfileName
    - Kies in het middelste vak **Is gelijk aan**.
    - Voer in het laatste veld de naam in van het inschrijvingsprofiel dat u eerder hebt gemaakt.
    Raadpleeg [Dynamische lidmaatschapsregels voor groepen in AAD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership) voor meer informatie over dynamische lidmaatschapsregels. 
5. Kies **Query toevoegen** > **Maken**.

### <a name="revoke-tokens"></a>Tokens intrekken

U kunt het token of de QR-code direct laten verlopen. Vanaf dat moment is het token of de QR-code niet meer bruikbaar. U kunt deze optie bijvoorbeeld gebruiken als u:
  - het token of de QR-code per ongeluk hebt gedeeld met een onbevoegde partij
  - alle inschrijvingen hebt voltooid en het token of de QR-code niet meer nodig hebt

Het vervangen van een token of QR-code heeft geen effect op apparaten die al zijn geregistreerd.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en kies **Apparaten** > **Android** > **Android-inschrijving** > **Apparaten in bedrijfseigendom met werkprofiel (preview-versie)** .
2. Kies het profiel waarmee u wilt werken.
3. Kies **Token**.
5. Kies **Token intrekken** > **Ja** als u het token wilt intrekken.

## <a name="enroll-the-corporate-owned-work-profile-devices"></a>De zakelijke apparaten met een werkprofiel inschrijven

Gebruikers kunnen nu hun [zakelijke apparaat met een werkprofiel inschrijven](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> De **Microsoft Intune**-app wordt automatisch geïnstalleerd als een zakelijk apparaat met werkprofiel wordt ingeschreven.  Deze app is vereist voor inschrijving en kan niet worden verwijderd. 

## <a name="managing-apps-on-android-enterprise-corporate-owned-work-profile-devices"></a>Apps beheren op zakelijke Android Enterprise-apparaten met een werkprofiel

U kunt op zakelijke Android Enterprise-apparaten met een werkprofiel alleen apps installeren waarvoor het toewijzingstype is [ingesteld op Vereist](../apps/apps-deploy.md#assign-an-app). De apps worden geïnstalleerd vanuit de Beheerde Google Play Store op dezelfde manier als op apparaten met een Android Enterprise-werkprofiel.

Apps worden automatisch bijgewerkt op beheerde apparaten zodra de app-ontwikkelaar een update op Google Play publiceert.

Als u een app van zakelijke Android Enterprise-apparaten met een werkprofiel wilt verwijderen, kunt u het volgende doen:
- Verwijder de vereiste app-implementatie.
- Maak een verwijderimplementatie voor de app.

## <a name="next-steps"></a>Volgende stappen
- [Android-apps implementeren](../apps/apps-deploy.md)
- [Configuratiebeleid voor Android toevoegen](../configuration/device-profiles.md)

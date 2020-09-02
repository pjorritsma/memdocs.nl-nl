---
title: Intune-inschrijving voor toegewezen Android Enterprise-apparaten instellen
titleSuffix: Microsoft Intune
description: Meer informatie over het inschrijven van toegewezen Android Enterprise-apparaten in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e151f45f8b65050496504ecdc95c0084b74e7c2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915157"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-dedicated-devices"></a>Intune-inschrijving van toegewezen Android Enterprise-apparaten instellen

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Android Enterprise ondersteunt kioskapparaten in bedrijfseigendom voor eenmalig gebruik waarvoor de oplossing voor toegewezen apparaten is ingesteld. Dergelijke apparaten worden voor een bepaald doel gebruikt, zoals digitale ondertekening, het afdrukken van tickets of voorraadbeheer. Beheerders vergrendelen het gebruik van een apparaat voor een beperkt aantal apps en webkoppelingen. Ook wordt voorkomen dat gebruikers andere apps kunnen toevoegen of andere acties op het apparaat kunnen uitvoeren.

Intune helpt u met de implementatie van apps en instellingen op toegewezen Android Enterprise-apparaten. Zie [Android Enterprise-vereisten](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) voor specifieke informatie over Android Enterprise.

Apparaten die u op deze manier beheert, zijn geregistreerd in Intune zonder een gebruikersaccount en zijn niet gekoppeld aan een eindgebruiker. Ze zijn niet bedoeld voor apps voor persoonlijk gebruik of voor apps met een sterke vereiste voor gebruikersspecifieke accountgegevens, zoals Outlook of Gmail.

## <a name="device-requirements"></a>Vereisten voor apparaten

Apparaten moeten voldoen aan de volgende vereisten om te worden beheerd als een toegewezen Android Enterprise-apparaat:

- Android-besturingssysteemversie 6.0 en hoger.
- Op de apparaten moet een verdeling van Android worden uitgevoerd die connectiviteit met GMS (Google Mobile Services) heeft. Op de apparaten moet GMS beschikbaar zijn en de apparaten moeten in staat zijn om verbinding te maken met GMS.

## <a name="set-up-android-enterprise-dedicated-device-management"></a>Beheer van toegewezen Android Enterprise-apparaat instellen

Volg deze stappen om het beheer van een toegewezen Android Enterprise-apparaat in te stellen:

1. U moet de [MDM-instantie instellen op **Microsoft Intune**](../fundamentals/mdm-authority-set.md) als voorbereiding op het beheer van mobiele apparaten. U stelt de instantie slechts één keer in, wanneer u Intune voor het eerst instelt voor het beheer van mobiele apparaten.
2. [Verbind uw Intune-tenantaccount met uw Beheerde Google Play-account](connect-intune-android-enterprise.md).
3. [Maak een inschrijvingsprofielprofiel](#create-an-enrollment-profile).
4. [Maak een apparaatgroep](#create-a-device-group).
5. [Schrijf de toegewezen apparaten in](#enroll-the-dedicated-devices).

### <a name="create-an-enrollment-profile"></a>Een inschrijvingsprofiel maken

> [!NOTE]
> Als een token is verlopen, wordt het gekoppelde profiel niet weergegeven in **Apparaatinschrijving** > **Android-inschrijving** > **Toegewezen apparaten in bedrijfseigendom**. Als u alle profielen wilt zien die zijn gekoppeld aan zowel actieve als niet-actieve tokens, klikt u op **Filteren** en schakelt u de vakjes in voor de beleidsstatussen Actief en Niet-actief. 

U moet een inschrijvingsprofiel maken, zodat u uw toegewezen apparaten kunt inschrijven. Bij het maken van het profiel ontvangt u een inschrijvingstoken (willekeurige tekenreeks) en een QR-code. Afhankelijk van het Android-besturingssysteem en de versie van het apparaat kunt u het token of de QR-code gebruiken om [het toegewezen apparaat in te schrijven](#enroll-the-dedicated-devices).

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en kies **Apparaten** > **Android** > **Android-inschrijving** > **Toegewezen apparaten in bedrijfseigendom.**
2. Kies **Maken** en vul de vereiste velden in.
    - **Naam**: typ een naam die u gebruikt wanneer u het profiel toewijst aan de dynamische apparaatgroep.
    - **Vervaldatum van token**: de datum waarop het token verloopt. Google dwingt een maximum van 90 dagen af.
3. Kies **Maken** om het profiel op te slaan.

### <a name="create-a-device-group"></a>Een apparaatgroep maken

U kunt apps en beleidsregels zenden naar toegewezen of dynamische apparaatgroepen. U kunt dynamische AAD-apparaatgroepen configureren om apparaten die zijn geregistreerd met een bepaald inschrijvingsprofiel automatisch te vullen door deze stappen te volgen:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en kies **Groepen** > **Alle groepen** > **Nieuwe groep**.
2. Vul in de blade **Groep** de vereiste velden als volgt in:
    - **Groepstype**: Beveiliging
    - **Groepsnaam**: typ een intuïtieve naam (bijvoorbeeld Factory 1-apparaten)
    - **Type lidmaatschap**: Dynamisch apparaat
3. Kies **Dynamische query toevoegen**.
4. Vul in de blade **Dynamisch-lidmaatschapregels** de velden als volgt in:
    - **Regel voor dynamisch lidmaatschap toevoegen**: Eenvoudige regel
    - **Locatie voor het toevoegen van apparaten**: enrollmentProfileName
    - Kies in het middelste vak **Is gelijk aan**.
    - Voer in het laatste veld de naam in van het inschrijvingsprofiel dat u eerder hebt gemaakt.
    Raadpleeg [Dynamische lidmaatschapsregels voor groepen in AAD](/azure/active-directory/users-groups-roles/groups-dynamic-membership) voor meer informatie over dynamische lidmaatschapsregels. 
5. Kies **Query toevoegen** > **Maken**.

### <a name="replace-or-remove-tokens"></a>Tokens vervangen of verwijderen

- **Token vervangen**: met Token vervangen kunt u een nieuw token of nieuwe QR-code genereren wanneer voor een van beide de vervaldatum nadert.
- **Token intrekken**: u kunt het token of de QR-code direct laten verlopen. Vanaf dat moment is het token of de QR-code niet meer bruikbaar. U kunt deze optie bijvoorbeeld gebruiken als u:
  - het token of de QR-code per ongeluk hebt gedeeld met een onbevoegde partij
  - alle inschrijvingen hebt voltooid en het token of de QR-code niet meer nodig hebt

Het vervangen of intrekken van een token of QR-code heeft geen effect op apparaten die al zijn geregistreerd.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en kies **Apparaten** > **Android** > **Android-inschrijving** > **Toegewezen apparaten in bedrijfseigendom.**
2. Kies het profiel waarmee u wilt werken.
3. Kies **Token**.
4. Kies **Token vervangen** als u het token wilt vervangen.
5. Kies **Token intrekken** als u het token wilt intrekken.

## <a name="enroll-the-dedicated-devices"></a>De toegewezen apparaten inschrijven

U kunt nu [uw toegewezen apparaten inschrijven](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> De **Microsoft Intune**-app wordt automatisch geïnstalleerd als een toegewezen apparaat wordt ingeschreven.  Deze app is vereist voor inschrijving en kan niet worden verwijderd. 

## <a name="managing-apps-on-android-enterprise-dedicated-devices"></a>Apps beheren op toegewezen Android Enterprise-apparaten

U kunt op toegewezen Android Enterprise-apparaten alleen apps installeren waarvoor het toewijzingstype is [ingesteld op Vereist](../apps/apps-deploy.md#assign-an-app). De apps worden geïnstalleerd vanuit de Beheerde Google Play Store op dezelfde manier als op apparaten met een Android Enterprise-werkprofiel.

Apps worden automatisch bijgewerkt op beheerde apparaten zodra de app-ontwikkelaar een update op Google Play publiceert.

Als u een app van toegewezen Android Enterprise-apparaten wilt verwijderen, kunt u het volgende doen:
- Verwijder de vereiste app-implementatie.
- Maak een verwijderimplementatie voor de app.

## <a name="next-steps"></a>Volgende stappen
- [Android-apps implementeren](../apps/apps-deploy.md)
- [Configuratiebeleid voor Android toevoegen](../configuration/device-profiles.md)
---
title: Microsoft Edge toevoegen aan macOS-apparaten met behulp van Microsoft Intune
titleSuffix: ''
description: Meer informatie over het toevoegen van Microsoft Edge aan macOS-apparaten met behulp van Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kellieei
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0b9af43c149912d4972e2f79f5e89840823ca94
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914035"
---
# <a name="add-microsoft-edge-to-macos-devices-using-microsoft-intune"></a>Microsoft Edge toevoegen aan macOS-apparaten met behulp van Microsoft Intune

Voordat u apps kunt implementeren, configureren, bewaken of beveiligen, moet u deze aan Intune toevoegen. Een van de beschikbare [app-typen](apps-add.md#app-types-in-microsoft-intune) is Microsoft Edge *versie 77 en later*. Door dit app-type in Intune te selecteren, kunt u Microsoft Edge *versie 77 en later* toewijzen aan en installeren op door u beheerde macOS-apparaten. Met dit app-type kunt u Microsoft Edge eenvoudig toewijzen aan macOS-apparaten zonder dat u gebruik hoeft te maken van de macOS App Wrapping Tool. Deze apps worden geleverd met Microsoft AutoUpdate (MAU) om de apps veiliger te maken en up-to-date te houden.

> [!IMPORTANT]
> Dit app-type is biedt Dev- en Beta-kanalen voor macOS. De implementatie is alleen in het Engels (EN) beschikbaar, maar eindgebruikers kunnen de weergavetaal wijzigen in de browser via **Instellingen** > **Talen**. 

> [!NOTE]
> Microsoft Edge *versie 77 en later* is ook beschikbaar voor Windows 10.

## <a name="prerequisites"></a>Vereisten

- Op het macOS-apparaat moet macOS 10.12 of later worden uitgevoerd voordat u Microsoft Edge installeert.

## <a name="add-microsoft-edge-to-intune"></a>Microsoft Edge toevoegen aan Intune

U kunt Microsoft Edge versie 77 en later toevoegen aan Intune met behulp van de volgende stappen:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Alle apps** > **Toevoegen**.
3. Selecteer in de lijst **App-type** onder **Microsoft Edge, versie 77 en later** de optie **macOS**.

## <a name="configure-app-information"></a>App-gegevens configureren
In deze stap geeft u informatie op over deze app-implementatie. Aan de hand van deze informatie kunt u de app vinden in Intune en kunnen gebruikers de app vinden in de bedrijfsportal.

1. Selecteer de optie **App-gegevens** om het deelvenster **App-gegevens** weer te geven.
2. In het deelvenster **App-gegevens** geeft u informatie op over deze app-implementatie. Aan de hand van deze informatie kunt u de app vinden in Intune en kunnen gebruikers de app vinden in de bedrijfsportal.
    - **Naam**: Voer de naam van de app in zoals deze in de bedrijfsportal zal worden weergegeven. Zorg ervoor dat alle namen uniek zijn. Als dezelfde app-naam twee keer voorkomt, wordt slechts één van de apps weergegeven voor gebruikers in de bedrijfsportal.
    - **Beschrijving**: Voer een beschrijving in voor de app. U kunt bijvoorbeeld de beoogde gebruikers vermelden in de beschrijving.
    - **Uitgever**: Microsoft wordt weergegeven als de uitgever.
    - **Categorie**: selecteer een of meer ingebouwde app-categorieën of een categorie die u hebt gemaakt (optioneel). Met deze instellingen kunnen gebruikers de app gemakkelijker vinden wanneer ze door de bedrijfsportal bladeren.
    - **Deze weergeven als aanbevolen app in de bedrijfsportal**: Selecteer deze optie om de app prominent weer te geven op de hoofdpagina van de bedrijfsportal wanneer gebruikers zoeken naar apps.
    - **Informatie-URL**: Voer de URL in van een website die informatie over deze app bevat (optioneel). De URL wordt weergegeven voor gebruikers in de bedrijfsportal.
    - **Privacy-URL**: (optioneel) Voer de URL in van een website die privacyinformatie over deze app bevat. De URL wordt weergegeven voor gebruikers in de bedrijfsportal.
    - **Ontwikkelaar**: Microsoft wordt weergegeven als de ontwikkelaar.
    - **Eigenaar**: Microsoft wordt weergegeven als de eigenaar.
    - **Opmerkingen**: Voer de opmerkingen in die u aan deze app wilt koppelen (optioneel).
3. Selecteer **OK**.

## <a name="configure-microsoft-edge-settings"></a>Instellingen voor Microsoft Edge configureren
In deze stap configureert u de installatieopties voor de app.

1. Selecteer in het deelvenster **App toevoegen** de optie **App-instellingen**.
2. Selecteer in het deelvenster **App-instellingen** de optie **Stable,** **Beta** of **Dev** in de lijst **Kanaal** om te bepalen vanuit welk Edge-kanaal u de app gaat implementeren.

    - **Stable** is het aanbevolen kanaal voor een brede implementatie in Enterprise-omgevingen. Het wordt elke zes weken bijgewerkt en elke release bevat verbeteringen uit het Beta-kanaal.
    - Het kanaal **Beta** is de stabielste previewervaring van Microsoft Edge en de beste keuze voor een volledige pilot binnen uw organisatie. Met elke zes weken belangrijke updates bevat elke release de vergaarde kennis en verbeteringen van het Dev-kanaal.
    - Het kanaal **Dev** is gereed voor zakelijke feedback over Windows, Windows Server en macOS. Het wordt elke week bijgewerkt en bevat de nieuwste verbeteringen en oplossingen.

    > [!NOTE]
    > Het Microsoft Edge-browserlogo wordt samen met de app weergegeven wanneer gebruikers door de bedrijfsportal bladeren.

3.    Selecteer **OK**.

## <a name="select-scope-tags-optional"></a>Bereiktags selecteren (optioneel)
U kunt bereiktags gebruiken om te bepalen wie er informatie over client-apps mag bekijken in Intune. Zie Op rollen gebaseerd toegangsbeheer en bereiktags gebruiken voor gedistribueerde IT voor uitgebreide informatie over bereiktags.
1.    Selecteer **Bereik (tags)**  > **Toevoegen**.
2.    Gebruik het vak onder **Selecteren** om bereiktags te zoeken.
3.    Schakel het selectievakje in naast de bereiktags die u aan deze app wilt toewijzen.
4.    Klik op **Selecteren** > **OK**.

## <a name="add-the-app"></a>De app toevoegen
Wanneer u klaar bent met configureren, selecteert u **Toevoegen** in het deelvenster **App-app**. 

De app die u hebt gemaakt, wordt weergegeven in de lijst met apps waar u de app kunt toewijzen aan de groepen die u selecteert. 

> [!NOTE]
> Momenteel biedt Apple geen manier om Microsoft Edge via Intune te verwijderen van macOS-apparaten.

## <a name="next-steps"></a>Volgende stappen
- Zie [Microsoft Edge configureren op macOS-apparaten](/deployedge/configure-microsoft-edge-on-mac) voor meer informatie over het configureren van Microsoft Edge op macOS-apparaten.
- Zie voor meer informatie over app-toewijzingen opnemen in of uitsluiten uit groepen gebruikers [App-toewijzingen opnemen en uitsluiten](apps-inc-exl-assignments.md).
- [Apps aan groepen toewijzen](apps-deploy.md)
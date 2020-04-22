---
title: Snelstart - Een groep maken om gebruikers te beheren
titleSuffix: Microsoft Intune
description: In deze snelstart gebruikt u Microsoft Intune om een groep te maken op basis van bestaande gebruikers.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/17/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 723f4b4e-3090-4811-84ff-6af652abea5a
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7adb23f4709bf3ead07a01cb00d1b38fcb23c40
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "79356905"
---
# <a name="quickstart-create-a-group-to-manage-users"></a>Snelstart: een groep maken om gebruikers te beheren

In deze snelstart gebruikt u Intune om een groep te maken op basis van een bestaande gebruiker. Groepen worden gebruikt om uw gebruikers te beheren en de toegang van uw medewerkers tot uw zakelijke resources te regelen. Deze resources kunnen deel uitmaken van het intranet van uw bedrijf, of het kunnen externe resources zijn, zoals SharePoint-sites, SaaS-apps of web-apps.

Als u niet over een Intune-abonnement beschikt, kunt u [zich registreren voor een gratis proefaccount](free-trial-sign-up.md).

>[!NOTE]
>Intune biedt vooraf gemaakte de groepen **Alle gebruikers** en **Alle apparaten** in de console met handige, ingebouwde optimalisaties.

## <a name="prerequisites"></a>Vereisten

- Microsoft Intune-abonnement - [Registreren voor een gratis proefaccount](../fundamentals/free-trial-sign-up.md).
- Als u de stappen in deze snelstart wilt uitvoeren, moet u eerst [een gebruiker maken](quickstart-create-user.md).

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Aanmelden bij Intune in de Microsoft Endpoint Manager

Meld u bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) aan als een [globale beheerder of een Intune-serviceondersteuningsbeheerder](users-add.md#types-of-administrators). Als u een Intune-proefabonnement hebt gemaakt, is het account waarmee u het abonnement hebt gemaakt de globale beheerder.

## <a name="create-a-group"></a>Een groep maken

U maakt een groep die later in deze snelstartreeks wordt gebruikt. Ga als volgt te werk om een groep te maken:

1. Open de **Microsoft Endpoint Manager** en selecteer **Groepen** > **Nieuwe groep**.
2. Selecteer in de vervolgkeuzelijst **Groepstype** de optie **Beveiliging**.
3. Geef in het veld **Groepsnaam** de naam van de nieuwe groep (bijvoorbeeld **Contoso Testers**) op.
4. Voeg een **Groepsbeschrijving** aan de groep toe.
5. Stel **Type lidmaatschap** in op **Toegewezen**. 
6. Selecteer onder **Leden** de koppeling en voeg een of meer leden voor de groep toe vanuit de lijst.

    ![Schermopname van het maken van een groep in Microsoft Intune](./media/quickstart-create-group/quickstart-use-groups-01.png)

7. Klik op **Selecteren** > **maken**.

Als u de groep hebt gemaakt, wordt deze weergegeven in de lijst **Alle groepen**. 

## <a name="next-steps"></a>Volgende stappen

In deze snelstart hebt u Intune gebruikt om een groep te maken op basis van een bestaande gebruiker. Zie [Groepen toevoegen om gebruikers en apparaten te organiseren](groups-add.md) voor meer informatie over het toevoegen van groepen aan Intune.

Ga door naar de volgende snelstartgids om deze serie met snelstartgidsen voor Intune te volgen.

> [!div class="nextstepaction"]
> [Snelstart: Automatische inschrijving voor Windows 10-apparaten instellen](../enrollment/quickstart-setup-auto-enrollment.md)

---
title: De bedrijfsportal-app van Windows 10 toevoegen en toewijzen voor apparaten die met Autopilot zijn ingericht
titleSuffix: Microsoft Intune
description: De bedrijfsportal-app van Windows 10 toevoegen en toewijzen aan Intune voor apparaten die met Autopilot zijn ingericht.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d45d73f9c10c9bf7562def73b005c0dd63c7613
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559518"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>De bedrijfsportal-app van Windows 10 toevoegen en toewijzen voor apparaten die met Autopilot zijn ingericht

Uw gebruikers kunnen de bedrijfsportal-app gebruiken om apparaten te beheren en apps te installeren. U kunt de bedrijfsportal-app van Windows 10 rechtstreeks toewijzen vanuit Intune. 

## <a name="prerequisites"></a>Vereisten

Voor apparaten die met Windows 10 Autopilot zijn ingericht, kunt u het beste uw Microsoft Store voor Business-account koppelen aan Intune. Zie [In volume aangeschafte apps beheren vanuit de Microsoft Store voor Bedrijven met Microsoft Intune](windows-store-for-business.md) voor meer informatie.

U kunt ervoor kiezen om de **Bedrijfsportal (offline)** -app te installeren met behulp van de onderstaande stappen. De bedrijfsportal-app wordt in de apparaatcontext geïnstalleerd wanneer deze aan de Autopilot-groep is toegewezen en wordt op het apparaat geïnstalleerd vóór de gebruiker zich aanmeldt.

## <a name="configure-the-store-settings-to-show-the-offline-app"></a>De store-instellingen configureren om de offline-app weer te geven

1. Meld u met uw beheerdersaccount aan bij [Microsoft Store voor Bedrijven](https://www.microsoft.com/business-store).
2. Selecteer het tabblad **Beheren** boven in het venster.
3. Selecteer **Instellingen** in het linkerdeelvenster.
4. Stel **Offline apps weergeven** onder **Winkelervaring** in op **Aan**.  
   De offline gelicentieerde apps worde weergegeven.

## <a name="get-the-offline-company-portal-app-from-the-store"></a>De offline Bedrijfsportal-app downloaden uit de store

1. Zoek en selecteer de app **Bedrijfsportal**.
2. Stel het**Licentietype** in op **Offline**.
3. Selecteer **De app downloaden** om de offline bedrijfsportal-app te verkrijgen en toe te voegen aan uw inventaris.
   Om de app in de lijst van Intune te krijgen, moet u wachten tot de synchronisatieplanning is voltooid of een handmatige synchronisatie uitvoeren vanuit het Beheercentrum voor Microsoft Eindpuntbeheer.

## <a name="manually-sync-company-portal-app-with-intune"></a>Bedrijfsportal-app handmatig synchroniseren met Intune

1. Meld u met uw beheerdersaccount aan bij het  [Beheercentrum voor Microsoft Eindpuntbeheer](https://go.microsoft.com/fwlink/?linkid=2109431) .
2. Selecteer **Tenantbeheer** > **Connectors en tokens** > **Microsoft Azure Store voor Bedrijven**.
3. Klik op **Inschakelen**.
4. Klik, als u dit nog niet hebt gedaan, op de koppeling om u te registreren bij Microsoft Store voor Bedrijven en uw account te koppelen zoals eerder is beschreven.
5. Kies in de vervolgkeuzelijst **Taal** de taal waarin apps uit Microsoft Store voor Bedrijven moeten worden weergegeven in Azure Portal. Ongeacht de taal waarin deze apps worden weergegeven, worden ze geïnstalleerd in de taal van de eindgebruiker (indien beschikbaar).
6. Klik op **Synchroniseren** om de apps die u hebt aangeschaft in Microsoft Store, op te halen in Intune.

## <a name="assign-the-company-portal-app"></a>De bedrijfsportal-app toewijzen

1. Meld u met uw beheerdersaccount aan bij het  [Beheercentrum voor Microsoft Eindpuntbeheer](https://go.microsoft.com/fwlink/?linkid=2109431) .
2. Selecteer **Apps** > **Windows**.
3. Selecteer in de lijst met Windows-apps **Bedrijfsportal (offline)** .
4. [Wijs](apps-deploy.md) de Bedrijfsportal-app, indien nodig, toe als vereiste app aan geselecteerde groepen met Autopilot-apparaten.

## <a name="next-steps"></a>Volgende stappen

- Zie [Apps aan groepen toewijzen](apps-deploy.md) voor meer informatie over het toewijzen van apps.


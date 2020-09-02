---
title: Aangepaste instellingen toevoegen aan Windows Phone 8.1-apparaten in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Maak een aangepast profiel of voeg dit toe om de OMA-URI-instellingen te gebruiken voor apparaten met Windows Phone 8.1 in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0adb573dbb40f00a1b43b9fb356cdc20b97b669
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910074"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Aangepaste instellingen gebruiken voor Windows Phone 8.1-apparaten in Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Met Microsoft Intune kunt u aangepaste instellingen voor uw Windows Phone 8.1-apparaten toevoegen of maken met behulp van 'aangepaste profielen'. Aangepaste profielen zijn een functie in Intune. Ze zijn ontworpen om apparaatinstellingen en -functies toe te voegen die niet in Intune zijn ingebouwd.

In aangepaste profielen voor Windows Phone 8.1 worden OMA-URI-instellingen (Open Mobile Alliance Uniform Resource Identifier) gebruikt om verschillende functies te configureren. Deze instellingen worden doorgaans gebruikt door fabrikanten van mobiele apparaten om functies op het apparaat te beheren. In [Windows Phone 8.1 MDM-protocoldocumentatie](/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) vindt u een lijst met de instellingen.

In dit artikel wordt beschreven hoe u een aangepast profiel maakt voor Windows Phone 8.1-apparaten. 

## <a name="before-you-begin"></a>Voordat u begint

[Maak een aangepast profiel voor Windows Phone 8.1](custom-settings-configure.md).

## <a name="custom-oma-uri-settings"></a>Aangepaste OMA-URI-instellingen

- **OMA-URI-instellingen**: **Voeg** de volgende instellingen toe:

  - **Naam**: Voer een unieke naam in voor de OMA-URI-instelling waaraan u deze kunt herkennen in de lijst met instellingen.
  - **Beschrijving**: Geef een beschrijving op met een overzicht van de instelling en overige relevante informatie, zodat u het profiel beter kunt vinden.
  - **OMA-URI** (hoofdlettergevoelig): Voer de OMA-URI in die u als instelling wilt gebruiken.
  - **Gegevenstype**: Selecteer het gegevenstype dat u voor deze OMA-URI-instelling gaat gebruiken. Uw opties zijn:

    - Tekenreeks
    - Tekenreeks (XML-bestand)
    - Datum en tijd
    - Geheel getal
    - Drijvende komma
    - Boolean-waarde
    - Base64 (bestand)

  - **Waarde**: Voer de gegevenswaarde in die moet worden gekoppeld aan de OMA-URI die u hebt ingevoerd. De waarde is afhankelijk van het gegevenstype dat u hebt geselecteerd. Als u bijvoorbeeld **Datum en tijd** selecteert, selecteert u de waarde in een datumkiezer.

  Nadat u een aantal instellingen hebt toegevoegd, kunt u **Exporteren** selecteren. Met **Exporteren** maakt u een lijst met alle waarden die u hebt toegevoegd in een bestand met door komma's gescheiden waarden (.csv).

## <a name="example"></a>Voorbeeld

In het volgende voorbeeld kunnen Windows Phone 8.1-apparaten geen mobiele netwerken wijzigen tijdens het reizen buiten het dekkingsgebied van de provider.

- **Naam**: Mobiele dataroaming toestaan
- **Beschrijving**: Mobiele dataroaming toestaan of weigeren
- **OMA-URI** (hoofdlettergevoelig): ./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Gegevenstype**: Geheel getal
- **Waarde**: 0

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

Maak een [aangepast profiel op Windows 10-apparaten](custom-settings-windows-10.md).
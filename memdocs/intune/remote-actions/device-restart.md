---
title: Apparaten opnieuw opstarten met Microsoft Intune - Azure | Microsoft Docs
description: Gebruik de externe actie Opnieuw opstarten om Windows- en iOS-/iPadOS-apparaten opnieuw op te starten met Microsoft Intune in de Azure-portal.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c707e0c4-391a-4bad-9dfd-9a7799c48dd5
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d68f09c6163ff613e5e4387a0e2d09a5eeea56c4
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051686"
---
# <a name="remotely-restart-devices-with-intune"></a>Apparaten extern opnieuw opstarten met Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

De apparaatactie **Opnieuw opstarten** zorgt ervoor dat het apparaat dat kiest, opnieuw wordt opgestart (binnen 5 minuten). De eigenaar van het apparaat wordt niet op de hoogte gesteld dat het apparaat opnieuw wordt opgestart. Hierdoor kan eventueel werk verloren gaan.

## <a name="supported-platforms"></a>Ondersteunde platforms

- Windows: ondersteund op Windows 8.1 en hoger
- Toegewezen Android Enterprise-apparaten - Ondersteund op Android 7.0 en hoger
- Volledig beheerde Android-apparaten - Ondersteund op Android 6.0 en hoger
- Android Enterprise-apparaten in bedrijfseigendom met werkprofiel - Ondersteund op Android 8.0 en hoger
- iOS/iPadOS: ondersteund

    > [!Note]  
    > Voor deze opdracht is een apparaat onder supervisie en het vereist toegangsrecht **Apparaatvergrendeling** vereist. Het apparaat wordt onmiddellijk opnieuw opgestart. iOS-/iPadOS-apparaten die met een wachtwoordcode zijn vergrendeld, worden na het opnieuw opstarten niet aan een Wi-Fi-netwerk toegevoegd. Nadat het apparaat opnieuw is opgestart, kan het mogelijk niet meer communiceren met de server.
- macOS: niet ondersteund
- Android-apparaten en apparaten met Android- werkprofiel - niet ondersteund

## <a name="restart-a-device"></a>Apparaten opnieuw opstarten

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selecteer **Apparaten** > **Alle apparaten**.
4. Kies een apparaat in de lijst met apparaten die u beheert > **Opnieuw opstarten** > **Ja**.

## <a name="next-steps"></a>Volgende stappen

- Selecteer **Apparaten** > **Apparaatacties** om de status van de apparaatactie **Opnieuw opstarten** te bekijken.

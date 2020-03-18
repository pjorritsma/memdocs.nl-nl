---
title: Een gebruiker met Microsoft Intune verwijderen van een iOS-/iPadOS-apparaat
titleSuffix: ''
description: Lees hier meer over het verwijderen van een gebruiker van een gedeeld iOS-/iPadOS-apparaat met Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2ea5941c-a69b-4e1c-b42c-a1fc0c3a7de7
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08a6ccb30d4397ce5d06483556579c32f3eb2819
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348975"
---
# <a name="remove-a-user-from-a-shared-iosipados-device"></a>Een gebruiker verwijderen van een gedeeld iOS-/iPadOS-apparaat


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Met de actie **Gebruiker verwijderen** kunt u een gebruiker verwijderen uit de lokale cache op een gedeeld iPad-apparaat. Het iPad-apparaat moet met behulp van een [iOS-/iPadOS-opleidingsprofiel](../fundamentals/education-settings-configure-ios.md) worden ingesteld voor het beheren van de Klaslokaal-app voor iOS/iPadOS. 

## <a name="supported-platforms"></a>Ondersteunde platforms

- Windows: niet ondersteund
- Windows Phone: niet ondersteund
- iOS/iPadOS: ondersteund op iOS/iPadOS 9.3 en hoger (alleen gedeelde iPads)
- macOS: niet ondersteund
- Android: niet ondersteund

## <a name="remove-a-user"></a>Een gebruiker verwijderen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Alle apparaten**.
3. Selecteer een iOS-/iPadOS-apparaat in de lijst met apparaten die u beheert.
4. Selecteer **Gebruikers** in het deelvenster voor het apparaat.
5. Klik in de lijst met de rechtermuisknop op de gebruiker die u wilt verwijderen en kies vervolgens **Gebruiker verwijderen**.

## <a name="next-steps"></a>Volgende stappen

- Selecteer **Apparaten** > **Apparaatacties** om de status van de apparaatactie **Gebruiker verwijderen** te bekijken.

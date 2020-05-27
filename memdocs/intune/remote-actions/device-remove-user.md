---
title: Een gebruiker met Microsoft Intune verwijderen van een iOS-/iPadOS-apparaat
titleSuffix: ''
description: Lees hier meer over het verwijderen van een gebruiker van een gedeeld iOS-/iPadOS-apparaat met Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2ea5941c-a69b-4e1c-b42c-a1fc0c3a7de7
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed91d31a7085d023ef012e1dd30d86c833819ecc
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983080"
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

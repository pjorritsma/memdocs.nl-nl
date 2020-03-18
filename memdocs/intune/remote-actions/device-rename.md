---
title: Naam van een apparaat wijzigen met Microsoft Intune - Azure | Microsoft Docs
description: Wijzig de naam van een apparaat met behulp van Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bdb5649450703215add20b88c262c0aa27e546e7
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79338055"
---
# <a name="rename-a-device-in-intune"></a>Naam van een apparaat wijzigen in Intune

Met de actie **Naam van apparaat wijzigen** kunt u de naam wijzigen van een apparaat dat is ingeschreven bij Intune. De naam van het apparaat wordt gewijzigd in Intune en op het apparaat.

U kunt de namen van de volgende typen apparaten wijzigen:
- Windows-apparaat in bedrijfseigendom 
- iOS/iPadOS onder supervisie
- MacOS 10-apparaat in bedrijfseigendom

Deze functie biedt momenteel geen ondersteuning voor de naamwijziging van hybride Azure AD Windows-apparaten.

## <a name="rename-a-device"></a>De naam van een apparaat wijzigen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Kies **Apparaten** > **Alle apparaten** > kies een apparaat > **...**  > **Naam van apparaat wijzigen**.
4. Typ op de blade **Naam van apparaat wijzigen** de nieuwe naam in het tekstvak. U kunt letters, cijfers en afbreekstreepjes gebruiken. De naam moet minstens één letter of afbreekstreepje bevatten.
5. Als u het apparaat opnieuw wilt opstarten nadat u de naam ervan hebt gewijzigd, kiest u naast **Opnieuw opstarten na het wijzigen van de naam** de optie **Ja**.
6. Kies **Naam wijzigen**.

## <a name="windows-device-rename-rules"></a>Regels voor het wijzigen van de naam van Windows-apparaten
Bij het wijzigen van de naam van een Windows-apparaat moet de nieuwe naam aan de volgende regels voldoen:
- Maximaal 15 tekens (moet kleiner zijn dan of gelijk zijn aan 63 bytes, exclusief navolgende null-tekens)
- Niet null of een lege tekenreeks
- Toegestane ASCII: Letters (a-z, A-Z), cijfers (0-9) en afbreekstreepjes
- Toegestane Unicode: tekens > = 0x80, moet geldige UTF8 zijn, moet IDN-toewijsbaar zijn (dat wil zeggen dat RtlIdnToNameprepUnicode moet slagen, zie RFC 3492)
- Namen mogen niet alleen cijfers bevatten
- Namen mogen geen spaties bevatten
- Niet-toegestane tekens: { | } ~ [ \ ] ^ ' : ; < = > ? & @ ! " # $ % ` ( ) + / , . _ *)


## <a name="next-steps"></a>Volgende stappen

Ga naar de pagina **Overzicht** voor het apparaat om de status van de actie **Naam wijzigen** te zien.

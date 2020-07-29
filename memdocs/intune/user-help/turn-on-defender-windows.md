---
title: Windows Defender inschakelen | Microsoft Docs
description: Ontdek hoe u Windows Defender kunt inschakelen voor toegang tot bedrijfsresources.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/15/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: shburbid
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 2169abf9955446d6299a64c7ce2ae03723faa792
ms.sourcegitcommit: 5c15b59cde085787b85f032f88add70a11d8e9a2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/17/2020
ms.locfileid: "86447973"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Windows Defender inschakelen voor toegang tot bedrijfsresources

Uw werk of school wilt er zeker van zijn dat apparaten die toegang hebben tot hun resources, beveiligd zijn. Er zijn bepaalde manieren waarop ze [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx), de ingebouwde beveiliging voor schadelijke software in Windows, kunnen gebruiken.

Er zijn enkele instellingen die u mogelijk moet wijzigen in Windows Defender om toegangsproblemen op te lossen. Voor deze stappen moet u mogelijk naar een aantal verschillende plaatsen op uw computer gaan.

## <a name="turn-on-windows-defender"></a>Windows Defender inschakelen

1. Ga naar **Start** en open **Configuratiescherm**.
2. Open **Beheerprogramma's** > **Groepsbeleid bewerken**. Hiermee opent u de **Editor voor lokaal groepsbeleid** in een nieuw venster.
3. Open **Computerconfiguratie** > **Beheersjablonen** > **Windows-onderdelen** > **Windows Defender Antivirus**. De instelling **Windows Defender Antivirus uitschakelen** bevindt zich onder de mappen van andere instellingen. 
4. Open **Windows Defender Antivirus uitschakelen** en zorg ervoor dat deze optie is ingesteld op **Uitgeschakeld** of **Niet geconfigureerd**.

## <a name="turn-on-real-time-protection"></a>Realtime-beveiliging inschakelen

Controleer of realtime-beveiliging is ingeschakeld door naar **Start** te gaan en te zoeken op **Windows-beveiliging**. Selecteer **Virus and threat protection settings** (Virus- en dreigingsinstellingen) en zorg dat zowel **Real-timebeveiliging** als **Cloud-beveiliging** is ingesteld op **Aan** . Als deze opties niet worden niet weergegeven, moet u de volgende stappen uitvoeren:

1. Ga naar **Start** en open **Configuratiescherm**.
2. Open **Beheerprogramma's** > **Groepsbeleid bewerken**. Hiermee opent u de **Editor voor lokaal groepsbeleid** in een nieuw venster.
3. Open **Computerconfiguratie** > **Beheersjablonen** > **Windows-onderdelen** > **Windows-beveiliging** > **Virus- en bedreigingsbeveiliging**.
4. Open de instelling **Virus- en bedreigingsbeveiliging verbergen** en stel deze optie in op **Uitgeschakeld**.

## <a name="update-your-antivirus-definitions"></a>Uw antivirus-definities bijwerken

Controleer of uw antivirus-definities zijn bijgewerkt door te gaan naar **Start** en te zoeken op **Windows Defender Security Center**. Selecteer **Beveiligingsupdates** en **Controleren op updates** om ervoor te zorgen dat uw apparaat is beveiligd tegen virussen. Als deze optie niet wordt weergegeven, volgt u de stappen in [Realtime-beveiliging inschakelen](turn-on-defender-windows.md#turn-on-real-time-protection)

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of hun contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).

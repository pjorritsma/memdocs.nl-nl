---
title: Uitgebreide interoperabiliteit client
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van de uitgebreide samenwerkings client voor lange termijn ondersteuning van een statische Configuration Manager-client met een huidige branch-site.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78e89307e66107b259d818a84fa4dbca878a843c
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590895"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Gebruik de Configuration Manager-client software voor uitgebreide interoperabiliteit met toekomstige versies van een Current Branch site

*Van toepassing op: Configuration Manager (huidige vertakking)*  

Het is mogelijk dat u de Configuration Manager-client niet regel matig op sommige apparaten kunt bijwerken met bedrijfs vereisten. U moet bijvoorbeeld beleids regels voor wijzigings beheer volgen of het apparaat is essentieel voor de hand. Deze behoeften zijn geschikt door een nieuwe client te installeren voor langdurig gebruik, de zogeheten uitgebreide samenwerkings client (EIC). Gebruik alleen de EIC voor specifieke apparaten die niet regel matig kunnen worden bijgewerkt, zoals kiosk of verkooppunt apparaten. Blijf [automatische client upgrade](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) voor de meeste clients gebruiken.

## <a name="how-it-works"></a>Hoe werkt het?

Wanneer u bijvoorbeeld een nieuwe [Update in de console](../servers/manage/install-in-console-updates.md) voor Configuration Manager installeert, updaten clients hun client software automatisch bij, zodat deze de nieuwe functies kunnen gebruiken. Met dit scenario wordt u nog steeds bijgewerkt naar de huidige branch die de nieuwe functies en updates ontvangt. De meeste apparaten updaten de Configuration Manager-client software bij elke versie-update die u installeert. In een subset van kritieke systemen waarvoor u geen updates voor client software wilt ontvangen, installeert u echter de uitgebreide samenwerkings-client. Deze clients installeren pas nieuwe client software als u een nieuwe versie van de client software expliciet implementeert.

## <a name="supported-versions"></a>Ondersteunde versies

De volgende tabel geeft een lijst van de versies van de Configuration Manager-client die worden ondersteund voor dit scenario:

| Versie | Beschikbaarheidsdatum | Einddatum voor ondersteuning |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 27 maart 2019 | Niet eerder dan 27 maart 2021 |
| 1802<br/>5.00.8634 | 1 mei 2018 | Niet eerder dan 1 mei, 2020 |
| 1606<br/>5.00.8412 | 18 november 2016 | 1 mei 2019 |

> [!TIP]  
> De EIC wordt voor ten minste twee jaar na de release datum ondersteund. Zie [ondersteuning voor Configuration Manager huidige branch-versies](../servers/manage/current-branch-versions-supported.md)voor meer informatie over release datums.  

Plan de uitgebreide interoperabiliteits client bij te werken op apparaten die u beheert met de huidige vertakking voordat ondersteuning voor de client verloopt. U kunt dit doen door een nieuwe versie van de client van micro soft te downloaden en vervolgens die bijgewerkte client software te implementeren op uw apparaten die gebruikmaken van de huidige uitgebreide samenwerkings client.

## <a name="how-to-use-the-eic"></a>De EIC gebruiken

1. Voeg deze apparaten toe aan een verzameling en sluit die verzameling uit van automatische Client upgrades. Zie voor meer informatie [clients uitsluiten van upgrade](../clients/manage/upgrade/exclude-clients-windows.md).  

1. Verkrijg een ondersteunde versie van de EIC vanuit de `\SMSSETUP\Client` map van de installatie media van Configuration Manager Update. Zorg ervoor dat u de volledige inhoud van de map kopieert.  

<!--
    > [!TIP]
    > To find Configuration Manager media in the [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC), go to the **Downloads and Keys** tab, and search for **Microsoft Endpoint Configmgr (current branch)**.
-->

1. Installeer de EIC hand matig op deze apparaten. Zie [de client hand matig installeren](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)voor meer informatie.  

    > [!Important]  
    > Gebruik de optie CCMSETUP **/AlwaysExcludeUpgrade: True**bij het upgraden van versie 1606-clients naar versie 1802. Anders kan de client beleid ontvangen van het beheer punt om automatisch bij te werken vóór het uitsluitings beleid.  

## <a name="limitations"></a>Beperkingen

- Updates voor de uitgebreide samenwerkings client software zijn niet beschikbaar met behulp van updates in de console. Voor meer informatie over het bijwerken van de EIC gaat u naar [een upgrade uitvoeren van een uitgesloten client](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override).  

- De EIC ondersteunt alleen de volgende functies:  

  - Software-updates  
  - Hardware- en software-inventaris
  - Pakketten en programma's

## <a name="next-steps"></a>Volgende stappen

[Clients uitsluiten van een upgrade](../clients/manage/upgrade/exclude-clients-windows.md)

Zie [clients controleren](../clients/manage/monitor-clients.md)om ervoor te zorgen dat clients correct zijn geïnstalleerd op de apparaten die u wilt.

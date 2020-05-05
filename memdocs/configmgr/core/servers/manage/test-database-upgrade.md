---
title: Data Base-update testen
titleSuffix: Configuration Manager
description: Voer een upgrade uit van de site database bij het installeren van updates voor Configuration Manager.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56c1422f4157b255f4f7a8624e36d10e01f28fc0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719979"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>De data base-upgrade testen bij het installeren van een update

*Van toepassing op: Configuration Manager (huidige vertakking)*

De informatie in dit onderwerp kan u helpen bij het uitvoeren van een test database-upgrade voordat u een update in de console installeert voor de huidige vertakking van Configuration Manager. De test upgrade is echter niet langer een vereiste of aanbevolen stap, tenzij uw data base verdacht is of wordt gewijzigd door aanpassingen die niet expliciet door Configuration Manager worden ondersteund.

## <a name="do-i-need-to-run-a-test-upgrade"></a>Moet ik een test upgrade uitvoeren?
De afschaffing van deze upgrade test wordt mogelijk gemaakt als gevolg van wijzigingen die zijn geïntroduceerd in Configuration Manager current branch. Deze wijzigingen vereenvoudigen het proces en de snelheid waarmee een productie omgeving kan worden bijgewerkt naar nieuwere versies. Deze nieuwe opzet werd uitgevoerd om klanten te helpen om op de hoogte te blijven van minder Risico's en minder operationele overhead bij het installeren van elke update.

De wijzigingen zijn de manier waarop updates worden geïnstalleerd, met inbegrip van logica waarmee automatisch een mislukte update wordt teruggedraaid zonder dat er een site herstel hoeft te worden uitgevoerd. Met deze wijzigingen wordt het gebruik van de-console voor het beheren van update-installaties ingeschakeld en wordt een optie opgenomen om de [installatie van een mislukte update opnieuw uit te voeren](install-in-console-updates.md#bkmk_retry).

> [!TIP]
> Wanneer u een upgrade uitvoert naar Configuration Manager huidige vertakking van een ouder product, zoals System Center 2012 Configuration Manager, is [het testen van de Data Base een aanbevolen stap](../deploy/install/upgrade-to-configuration-manager.md#bkmk_test).

Als u nog steeds de upgrade van een site database wilt testen wanneer u een update in de console installeert, vormt de volgende informatie een aanvulling [op de richt lijnen voor het installeren van een update in de console](install-in-console-updates.md#bkmk_install).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Voorbereiden op het uitvoeren van een test database-upgrade  
Voordat u een nieuwe update in uw-hiërarchie installeert, zoals update 1702, kunt u de upgrade van uw site database testen.

Als u de upgrade test wilt uitvoeren, gebruikt u de Configuration Manager Setup van de bron bestanden vanaf [de cd. De meest recente map](the-cd.latest-folder.md) van een site waarop de versie van Configuration Manager wordt uitgevoerd die u bijwerkt. Deze vereiste betekent dat de update van de Data Base voor update naar 1702 moet worden getest:
-   U moet ten minste één site hebben met versie 1702 van waaruit u deze CD kunt ophalen. Meest recente map.
-   Als u geen site hebt waarop de vereiste versie wordt uitgevoerd, kunt u overwegen om een site te installeren in een test omgeving en vervolgens die site bij te werken naar de nieuwe versie. Hiermee maakt u de CD. Meest recente map met de juiste versie van de bron bestanden.

De upgrade test wordt uitgevoerd op basis van een back-up van uw site database die u hebt hersteld naar een afzonderlijk exemplaar van SQL Server.  U voert Setup uit vanaf de **cd. De laatste** map met de **testdbupgrade** -opdracht regel optie om de upgrade van de data base te testen. Nadat de test upgrade is voltooid, wordt de bijgewerkte data base verwijderd. Het kan niet worden gebruikt door een Configuration Manager-site.

Als een update niet kan worden geïnstalleerd, hoeft u de site niet te herstellen. In plaats daarvan kunt u de installatie van de update opnieuw uitvoeren vanuit de-console.

##  <a name="run-the-test-upgrade"></a>De test upgrade uitvoeren    
1. Gebruik Configuration Manager Setup en de bron bestanden van de **cd. De meest recente** map van een site waarop de versie wordt uitgevoerd die u wilt bijwerken.  

2. Kopieer de **cd. De meest recente** map naar een locatie op het SQL Server-exemplaar dat u gaat gebruiken om de upgrade van de test database uit te voeren.

3. Maak een back-up van de site database die u wilt testen. Herstel vervolgens een kopie van die Data Base naar een exemplaar van SQL Server dat geen Configuration Manager-site host. Het SQL Server exemplaar moet dezelfde versie van SQL Server gebruiken als uw site database.  

4. Nadat u de kopie van de Data Base hebt hersteld, voert u **Setup** uit vanaf de cd. De meest recente map met de bron bestanden van de versie die u bijwerkt. Wanneer u Setup wilt uitvoeren, gebruikt u de opdrachtregeloptie **/TESTDBUPGRADE**. Als het SQL Server exemplaar dat de database kopie host niet het standaard exemplaar is, geeft u de opdracht regel argumenten op voor het identificeren van het exemplaar dat als host fungeert voor de kopie van de site database.   

   U hebt bijvoorbeeld een site database met de naam van de Data Base *SMS_ABC*. U herstelt een kopie van deze site database naar een ondersteund exemplaar van SQL Server met de instantie naam *DBTest*. Als u een upgrade van deze kopie van de site database wilt testen, gebruikt u de volgende opdracht regel: **Setup. exe/TESTDBUPGRADE DBtest \ CM_ABC**.  

   U vindt Setup. exe op de volgende locatie op de bron media voor Configuration Manager: **SMSSETUP\BIN\X64**.  

5. Op het exemplaar van SQL Server waar u de upgrade test uitvoert, controleert u het *bestand ConfigMgrSetup. log* in de hoofdmap van het systeem station voor voortgang en geslaagde pogingen.  

    Als de test upgrade mislukt, kunt u eventuele problemen met betrekking tot de upgrade fout van de site database oplossen. Vervolgens maakt u een nieuwe back-up van de site database en test u de upgrade van de nieuwe kopie van de data base.  



## <a name="next-steps"></a>Volgende stappen
Nadat de test database is bijgewerkt, verwijdert u de bijgewerkte data base. Het kan niet worden gebruikt door een Configuration Manager-site. U kunt vervolgens terugkeren naar de actieve site en [de installatie van de update starten](install-in-console-updates.md).

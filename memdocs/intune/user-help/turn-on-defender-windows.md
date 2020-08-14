---
title: Windows Defender inschakelen | Microsoft Docs
description: Ontdek hoe u Windows Defender kunt inschakelen voor toegang tot bedrijfsresources.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/07/2020
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
ms.openlocfilehash: a57010a5c8089b0ac979cf43c3706467d83faea2
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110695"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Windows Defender inschakelen voor toegang tot bedrijfsresources

Organisaties willen er zeker van zijn dat apparaten die toegang hebben tot hun resources, veilig zijn. Wellicht moet u daarom [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx) gebruiken. Windows Defender is antivirussoftware die deel uitmaakt van Windows en helpt uw apparaat te beschermen tegen virussen en andere malware en bedreigingen. 

In dit artikel wordt beschreven hoe u uw apparaatinstellingen bijwerkt zodat deze voldoen aan de antivirusvereisten van uw organisatie en om toegangsproblemen op te lossen. 

## <a name="turn-on-windows-defender"></a>Windows Defender inschakelen
Voer de volgende stappen uit om Windows Defender op uw apparaat in te schakelen. 

1. Selecteer het menu **Start**.
2. Typ **groepsbeleid** in de zoekbalk. Selecteer vervolgens **Groepsbeleid bewerken** in de vermelde resultaten. De editor voor lokaal groepsbeleid wordt geopend.
4. Selecteer **Computerconfiguratie** > **Beheersjablonen** > **Windows-onderdelen** > **Windows Defender Antivirus**. 
5. Schuif naar onderaan de lijst en selecteer **Windows Defender antivirus uitschakelen**.  
6. Selecteer **Uitgeschakeld** of **Niet geconfigureerd**. Dit voelt wellicht vreemd aan; door de naamgeving lijkt het nu net of u Windows Defender uitschakelt. Dit is niet het geval, hiermee wordt deze optie wel degelijk ingeschakeld. 
7. Selecteer **Toepassen** > **OK**.  


## <a name="turn-on-real-time-and-cloud-delivered-protection"></a>Realtime-cloudbeveiliging inschakelen

Voer de volgende stappen uit om realtime-cloudbeveiliging in te schakelen. Met deze gezamenlijke antivirusfuncties wordt u beschermd tegen spyware en kunnen oplossingen voor problemen met schadelijke software via de cloud worden geleverd. 

1. Selecteer het menu **Start**.
2. Typ **Windows-beveiliging** in de zoekbalk. Selecteer het overeenkomende resultaat. 
3. Selecteer **Virus- en bedreigingsbeveiliging**.
4. Selecteer onder **Instellingen voor virus- en bedreigingsbeveiliging** de optie **Instellingen beheren**.
5. Zet elke schakelaar onder **Realtime-beveiliging** en **Cloudbeveiliging** om om ze in te schakelen. 

Als u deze opties niet ziet op het scherm, zijn ze mogelijk verborgen. Voer de volgende stappen uit om ze zichtbaar te maken.  

1. Selecteer het menu **Start**.  
2. Typ **groepsbeleid** in de zoekbalk. Selecteer vervolgens **Groepsbeleid bewerken** in de vermelde resultaten. De editor voor lokaal groepsbeleid wordt geopend.
3. Selecteer **Computerconfiguratie** > **Beheersjablonen** > **Windows-onderdelen** > **Windows-beveiliging** > **Virus- en bedreigingsbeveiliging**.
4. Selecteer **Het gebied Virus- en bedreigingsbeveiliging verbergen**.
5. Selecteer **Uitgeschakeld** > **Toepassen** > **OK**.  

## <a name="update-your-antivirus-definitions"></a>Uw antivirus-definities bijwerken
Voer de volgende stappen uit om uw antivirusdefinities bij te werken.  
1. Selecteer het menu **Start**.
2. Typ **Windows-beveiliging** in de zoekbalk. Selecteer het overeenkomende resultaat. 
3. Selecteer **Virus- en bedreigingsbeveiliging**.
4. Selecteer onder **Updates voor virus- en bedreigingsbeveiliging** de optie **Controleren op updates**. Als deze optie niet wordt weergegeven op het scherm, voltooit u de eerste reeks stappen in [Realtime-beveiliging inschakelen](turn-on-defender-windows.md#turn-on-real-time-and-cloud-delivered-protection). Controleer vervolgens opnieuw op updates. 

## <a name="next-steps"></a>Volgende stappen  

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of hun contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).

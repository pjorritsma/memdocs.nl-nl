---
title: Privacyverklaring voor cmdlets
titleSuffix: Configuration Manager
description: Meer informatie over hoe micro soft gegevens verzamelt en gebruikt die betrekking hebben op de Configuration Manager-cmdlets
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714645"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Privacyverklaring van Configuration Manager cmdlet-bibliotheek

*Van toepassing op: Configuration Manager (huidige vertakking)*

Deze privacyverklaring heeft betrekking op de functies voor de Configuration Manager cmdlet-bibliotheek.  

## <a name="usage-data"></a>Gebruiksgegevens  

#### <a name="what-this-feature-does"></a>Wat deze functie doet

Met de cmdlet-bibliotheek van Configuration Manager kunt u een Configuration Manager-hiërarchie beheren met Windows Power shell-cmdlets en-scripts. De cmdlet-bibliotheek verzamelt informatie over hoe u de cmdlets in de bibliotheek gebruikt om trends en gebruiks patronen te identificeren. De cmdlet-bibliotheek verzamelt ook de typen en het aantal fouten dat u ontvangt wanneer u de-cmdlets gebruikt.  

#### <a name="information-collected-processed-or-transmitted"></a>Verzamelde, verwerkte of verzonden gegevens
   
De verzamelde gebruiks gegevens omvatten het starten, stoppen en het beëindigen van cmdlets, het uitvoeren van afgeschafte cmdlets en metrische gegevens van activiteiten voor bewerkingen van SMS-providers die betrekking hebben op de cmdlets. Deze gegevens zijn niet persoonlijk identificeerbaar. Verzamelde fout gegevens bevatten fouten die zijn geretourneerd door cmdlets en fout Details voor uitzonderings fouten. Sommige rapporten met fout details bevatten mogelijk per ongeluk individuele id's, zoals een serie nummer van een apparaat dat op uw computer is aangesloten. De cmdlet-bibliotheek filtert en anoniem gemaakt informatie die in de fout rapporten wordt weer gegeven om afzonderlijke id's te verwijderen voordat ze naar micro soft worden verzonden.  

#### <a name="use-of-information"></a>Gebruik van gegevens
   
Micro soft gebruikt deze informatie voor het verbeteren van de kwaliteit, beveiliging en integriteit van de producten en services die ze aanbieden.  

#### <a name="choicecontrol"></a>Keuze/controle   

Deze functie voor gebruiks gegevens is standaard ingeschakeld. De cmdlet-bibliotheek van Configuration Manager heeft twee register sleutels die deze functionaliteit best uren.  

 Als u zich volledig wilt afmelden, stelt u deze twee register sleutel waarden in. Ze zijn voor elk van de providers van de Event Tracing for Windows (ETW):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider: CeipLevel = 0 (gebruiks gegevens voor de provider van het station worden niet meer gebruikt)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets: CeipLevel = 0 (gebruiks gegevens voor de cmdlets worden niet meer gebruikt)  

  Wijzigingen in de instellingen voor gebruiks gegevens zijn specifiek voor de computer waarop ze worden uitgevoerd.  


## <a name="next-steps"></a>Volgende stappen

[Documentatie over de cmdlet-bibliotheek Configuration Manager](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   

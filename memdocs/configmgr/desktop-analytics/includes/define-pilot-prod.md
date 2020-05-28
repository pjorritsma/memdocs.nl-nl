---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 431c88b07889f7c80d2723425aaef2245c7f06bc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268777"
---
Gebruik de volgende definities om onderscheid te maken tussen pilot en productie:  

- **Pilot**: een subset van uw apparaten die u wilt valideren voordat u deze implementeert in een grotere set. Gebruik Desktop Analytics om apparaten te markeren als een unieke waarde voor de pilotset. Apparaten in de pilot kunnen worden bijgewerkt wanneer er geen assets worden geblokkeerd. Een blokkerende Asset is gemarkeerd als *kritiek* en *kan niet* worden bijgewerkt.  

- **Productie**: alle andere apparaten die zijn Inge schreven bij Desktop Analytics en die zich niet in de pilot bevinden. Productie-apparaten kunnen worden bijgewerkt wanneer alle activa zijn afgemeld. Desktop Analytics meldt automatisch alle niet-essentiële assets af.  

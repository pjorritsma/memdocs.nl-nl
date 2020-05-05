---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 1b4fb4fb087639d1b3c3075339ce890a9c1dbbca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723647"
---
Gebruik de volgende definities om onderscheid te maken tussen pilot en productie:  

- **Pilot**: een subset van uw apparaten die u wilt valideren voordat u deze implementeert in een grotere set. Gebruik Desktop Analytics om apparaten te markeren als een unieke waarde voor de pilotset. Apparaten in de pilot kunnen worden bijgewerkt wanneer er geen assets worden geblokkeerd. Een blokkerende Asset is gemarkeerd als *kritiek* en *kan niet* worden bijgewerkt.  

- **Productie**: alle andere apparaten die zijn Inge schreven bij Desktop Analytics en die zich niet in de pilot bevinden. Productie-apparaten kunnen worden bijgewerkt wanneer alle activa zijn afgemeld. Desktop Analytics meldt automatisch alle niet-essentiële assets af.  


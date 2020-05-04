---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716115"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a>Taken reeksen zijn niet beschikbaar voor PXE of media

<!--5578298-->
Als u een taken reeks implementeert voor PXE of media (USB of DVD), ontvangt de client het beleid niet. Het volgende bericht bevindt zich in **bestand smsts. log**:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Tijdelijke oplossing

Start de taken reeks vanuit software Center.

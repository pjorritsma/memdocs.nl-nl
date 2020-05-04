---
title: Beveiliging en privacy voor energiebeheer
titleSuffix: Configuration Manager
description: Beveiligings-en privacy-informatie ophalen voor energie beheer in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715177"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Beveiliging en privacy voor energie beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Deze sectie bevat beveiligings-en privacy-informatie voor energie beheer in Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Aanbevolen beveiligingsprocedures voor energiebeheer  
 Er zijn geen aanbevolen beveiligingsprocedures voor energiebeheer.  

## <a name="privacy-information-for-power-management"></a>Privacyinformatie voor energiebeheer  
 Energiebeheer maakt gebruik van functies die zijn ingebouwd in Windows om tijdens en buiten kantooruren energieverbruik te controleren en energie-instellingen toe te passen op computers. Configuration Manager verzamelt informatie over het energie verbruik van computers, waaronder gegevens over wanneer een gebruiker een computer gebruikt. Hoewel Configuration Manager energie verbruik voor een verzameling bewaakt in plaats van voor elke computer, kan een verzameling slechts één computer bevatten. Energiebeheer is standaard niet ingeschakeld en moet worden geconfigureerd door een beheerder.  

 De informatie over energie gebruik wordt opgeslagen in de Configuration Manager-Data Base en wordt niet naar micro soft verzonden. Gedetailleerde informatie wordt 31 dagen in de database bewaard en een samenvatting van de gegevens wordt 13 maanden bewaard. U kunt de verwijderingstermijn niet configureren.  

 Voordat u energiebeheer configureert, moet u rekening houden met uw privacyvereisten.  

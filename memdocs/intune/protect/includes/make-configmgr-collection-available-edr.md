---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: 01179c35274ff14d4a91283e9a38aa5e6fee8e03
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823477"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. Klik met de rechtermuisknop vanuit een Configuration Manager-console die is verbonden met uw site op het hoogste niveau op een apparaatverzameling die u met Microsoft Endpoint Manager-beheercentrum synchroniseert, en selecteer **Eigenschappen**.

2. Schakel op het tabblad **Cloud Sync** de optie in om **Deze verzameling beschikbaar te maken om eindpuntbeveiligingsregels toe te wijzen vanuit het Microsoft Endpoint Manager-beheercentrum**.

   - U kunt deze optie niet selecteren als de Configuration Manager-hiërarchie niet is gekoppeld aan een tenant.
   - De verzamelingen die beschikbaar zijn voor deze optie, worden beperkt door het [verzamelingsbereik dat is geselecteerd voor uploaden met tenantkoppeling](../../../configmgr/tenant-attach/device-sync-actions.md#bkmk_edit). <!--CM7423168-->
  
   ![Cloudsynchronisatie configureren](../media/tenant-attach-intune/cloud-sync.png)

3. Selecteer **OK** om de configuratie op te slaan.

   Apparaten in deze verzameling kunnen nu worden gebruikt met Microsoft Defender ATP en bieden ondersteuning voor het gebruik van Intune-eindpuntbeveiligingsbeleid.

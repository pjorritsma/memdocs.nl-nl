---
title: Afgeschaft voor site servers
titleSuffix: Configuration Manager
description: Meer informatie over de producten en besturings systemen die Configuration Manager niet langer worden ondersteund voor site servers.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719475"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Verwijderd en afgeschaft voor Configuration Manager site servers

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel worden de producten en besturings systemen beschreven die worden verwijderd uit ondersteuning voor Configuration Manager-site servers of worden verwijderd in een toekomstige update (afgeschaft). Het bevat een vroegtijdige kennisgeving over toekomstige wijzigingen die van invloed kunnen zijn op uw gebruik van Configuration Manager.  

Deze informatie kan in de toekomst worden gewijzigd. De oplossing bevat mogelijk niet alle afgeschafte functies, producten of besturings systemen.  

## <a name="server-os"></a>Server-besturings systeem  

|Besturingssystemen|Afschaffing eerst aangekondigd|Ondersteuning verwijderd|
|-|-|-|
|Windows Server 2008 R2 met SP1|10 juli 2015| Versie 1702|
|Windows Server 2008 met SP2|10 juli 2015|Versie 1511|

## <a name="sql-server"></a>SQL Server

|SQL Server-versies|Afschaffing eerst aangekondigd|Ondersteuning verwijderd|
|-|-|-|
|SQL Server 2008 R2|10 juli 2015|Versie 1702|
|SQL Server 2008|10 juli 2015|Versie 1511|

Als u uw versie van SQL Server wilt bijwerken, raden we u aan de volgende methoden te volgen, van eenvoudig te complexere:

1. [Upgrade SQL Server ter plekke](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (aanbevolen).  

2. Installeer een nieuwe versie van SQL Server op een nieuwe computer. Ga vervolgens naar de nieuwe SQL Server met [behulp van de optie voor het verplaatsen van de data base](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) van Configuration Manager Setup.  

3. [Back-up en herstel](../../../servers/manage/backup-and-recovery.md)gebruiken.  

## <a name="next-steps"></a>Volgende stappen

Raadpleeg voor meer informatie de volgende artikelen:

- [Verwijderd en afgeschaft](removed-and-deprecated.md)  

- [Microsoft Ondersteuning levenscyclus](https://support.microsoft.com/lifecycle)  

- [Ondersteuning voor huidige branch-versies van Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)  

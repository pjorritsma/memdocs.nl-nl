---
title: Aanbevolen procedures voor software-updates
titleSuffix: Configuration Manager
description: Gebruik deze aanbevolen procedures voor software-updates in Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: dc0d416fdd186dbbeb4c61d48b688072bb830485
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723990"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Aanbevolen procedures voor software-updates in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat aanbevolen procedures voor software-updates in Configuration Manager. De informatie wordt gesorteerd in Aanbevolen procedures voor de eerste installatie en voor lopende bewerkingen.  



## <a name="installation-best-practices"></a><a name="bkmk_install"></a>Best practices voor installatie  

Gebruik de volgende aanbevolen procedures wanneer u software-updates installeert in Configuration Manager.  


### <a name="use-a-shared-wsus-database-for-software-update-points"></a><a name="bkmk_shared-susdb"></a>Een gedeelde WSUS-Data Base voor software-update punten gebruiken  

Wanneer u meer dan één software-updatepunt op een primaire site installeert, gebruikt u dezelfde WSUS-database voor elk software-updatepunt in hetzelfde Active Directory-forest. Als u dezelfde data base deelt, vermindert dit aanzienlijk, maar worden de prestaties van de client en het netwerk die u mogelijk ondervindt wanneer clients overschakelen naar een nieuw software-update punt. Een Delta scan vindt nog steeds plaats wanneer een client overschakelt naar een nieuw software-update punt dat een Data Base deelt met het oude software-update punt, maar de scan is veel kleiner dan wanneer de WSUS-server een eigen data base heeft. Zie [Software-update punt switches](plan-for-software-updates.md#BKMK_SUPSwitching)(Engelstalig) voor meer informatie over het overschakelen van software-update punten.  

> [!IMPORTANT]  
>  U kunt ook de lokale mappen met WSUS-inhoud delen wanneer u een gedeelde WSUS-Data Base voor software-update punten gebruikt.  

Voor meer informatie over het delen van de WSUS-data base raadpleegt u de volgende blog berichten:  

- [Een gedeelde SUSDB implementeren voor Configuration Manager software-update punten](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)  

- [Overwegingen voor meerdere WSUS-instanties die een inhouds database delen wanneer u Configuration Manager gebruikt](https://blogs.technet.microsoft.com/wsus/2014/03/22/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb/)  


### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-to-use-a-named-instance-and-the-other-to-use-the-default-instance"></a><a name="bkmk_sql-instance"></a>Als Configuration Manager en WSUS gebruikmaken van dezelfde SQL Server, configureert u er een om een benoemd exemplaar te gebruiken en de andere voor het gebruik van het standaard exemplaar  

Wanneer de Configuration Manager-en WSUS-data bases hetzelfde exemplaar van SQL Server delen, kunt u het resource gebruik niet eenvoudig bepalen tussen de twee toepassingen. Gebruik verschillende SQL Server exemplaren voor Configuration Manager en WSUS. Deze configuratie maakt het gemakkelijker om problemen met resource gebruik op te lossen en te diagnosticeren die voor elke toepassing kunnen optreden.  


### <a name="specify-the-store-updates-locally-setting"></a><a name="bkmk_store-local"></a>Geef de instelling updates lokaal opslaan op  

Wanneer u WSUS installeert, selecteert u de instelling om **Updates lokaal**op te slaan. Deze instelling zorgt ervoor dat WSUS de licentie voorwaarden downloadt die aan software-updates zijn gekoppeld. De termen worden tijdens het synchronisatie proces gedownload en opgeslagen op de lokale harde schijf voor de WSUS-server. Als u deze instelling niet selecteert, kunnen client computers geen compatibiliteits scans uitvoeren voor software-updates met licentie voorwaarden. Met het onderdeel **WSUS Synchronization Manager** van het software-update punt wordt gecontroleerd of deze instelling standaard elke 60 minuten is ingeschakeld.  



## <a name="operational-best-practices"></a><a name="bkmk_operation"></a>Aanbevolen procedures voor operationeel  

Gebruik de volgende aanbevolen procedures wanneer u software-updates gebruikt:  


### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a><a name="bkmk_object-limit"></a>Beperk software-updates tot 1000 in één software-update-implementatie  

Beperk het aantal software-updates tot 1000 in elke implementatie van software-updates. Wanneer u een regel voor automatische implementatie maakt, moet u controleren of de opgegeven criteria niet resulteren in meer dan 1000 software-updates. Als u software-updates hand matig implementeert, selecteert u niet meer dan 1000 updates.  


### <a name="create-a-new-software-update-group-each-time-an-adr-runs-for-patch-tuesday-and-for-general-deployments"></a><a name="bkmk_new-group"></a>Een nieuwe software-update groep maken telkens wanneer een ADR wordt uitgevoerd voor ' patch dinsdag ' en voor algemene implementaties  

Er is een limiet van 1000 software-updates in een implementatie. Wanneer u een regel voor automatische implementatie (ADR) maakt, geeft u op of u een bestaande update groep wilt gebruiken of een nieuwe update groep wilt maken telkens wanneer de regel wordt uitgevoerd. Als u in een ADR criteria opgeeft die resulteren in meerdere software-updates en de regel wordt uitgevoerd in een terugkerend schema, moet u elke keer dat de regel wordt uitgevoerd, een nieuwe software-update groep maken. Dit gedrag voor komt dat de implementatie de limiet van 1000 software-updates per implementatie overschrijdt.  


### <a name="use-an-existing-software-update-group-for-adrs-for-endpoint-protection-definition-updates"></a><a name="bkmk_same-group"></a>Een bestaande software-update groep gebruiken voor Adr's voor Endpoint Protection definitie-updates  

Gebruik altijd een bestaande software-update groep wanneer u een ADR gebruikt om regel matig Endpoint Protection definitie-updates te implementeren. Anders maakt de ADR mogelijk honderden software-update groepen in de loop van de tijd. Uitgevers van definitie-updates stellen doorgaans definitie-items in op verlopen wanneer ze worden vervangen door vier nieuwere updates. Daarom bevat de software-update groep die is gemaakt door de ADR nooit meer dan vier definitie-updates voor de Uitgever: één actieve en drie vervangen.  



## <a name="see-also"></a>Zie ook  
 [Software-updates plannen](plan-for-software-updates.md)

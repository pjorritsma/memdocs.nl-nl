---
title: Configuration Manager-hulpprogramma's
titleSuffix: Configuration Manager
description: Meer informatie over de hulpprogram ma's die u helpen bij het beheren en oplossen van problemen met uw Configuration Manager-infra structuur.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 06e308a54ee9636a7781667823e7b7f98ae6f25c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718565"
---
# <a name="configuration-manager-tools"></a>Configuration Manager-hulpprogramma's

*Van toepassing op: Configuration Manager (huidige vertakking)*

De Configuration Manager-hulpprogram ma's omvatten [op clients](#client-tools) en [op de server gebaseerde hulpprogram ma's](#server-tools). Gebruik deze hulpprogram ma's om uw Configuration Manager-infra structuur te ondersteunen en problemen op te lossen.

Vanaf Configuration Manager versie 1806 worden deze hulpprogram ma's opgenomen in de `CD.Latest\SMSSETUP\Tools` map op de site server. Er is geen verdere installatie vereist.<!--1357145--> Gebruik deze versies van de hulpprogram ma's met Configuration Manager versie 1806 en hoger.

Alle Windows-besturings systemen die worden vermeld als ondersteunde clients in [ondersteunde besturings systemen voor clients en apparaten](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) , worden ondersteund voor gebruik met deze hulpprogram ma's.

> [!Note]  
> De [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) is nog steeds beschikbaar via het micro soft Download centrum. Gebruik de versies van de hulpprogram ma's op de CD-rom voor Configuration Manager versie 1806 en hoger. Meest recente map op de site server. Sommige hulpprogram ma's waren voorheen aanwezig in de Toolkit, maar zijn niet opgenomen in versie 1806. Deze verouderde hulpprogram ma's worden niet meer ondersteund.


## <a name="client-tools"></a>Client hulpprogramma's

Deze hulpprogram ma's bevinden `ClientTools` zich in de submap:

- [CMTrace](cmtrace.md): Configuration Manager-logboek bestanden weer geven, controleren en analyseren  

- [Client Spy](clispy.md): problemen oplossen met betrekking tot software distributie, inventarisatie en meting

- [Hulp programma voor implementatie bewaking](deployment-monitoring-tool.md): problemen met toepassingen, updates en basislijn implementaties oplossen  

- [Beleids spyware](policy-spy.md): beleids toewijzingen weer geven  

- [Power Viewer-hulp programma](power-viewer-tool.md): de status van de functie voor energie beheer weer geven  

- [Hulp programma voor verzenden van planning](send-schedule-tool.md): trigger planningen en evaluaties van configuratie basislijnen  

> [!Note]  
> De `ClientTools` map bevat ook het bestand micro soft. Diagnostics. tracing. Event source. dll. Deze bibliotheek is vereist voor verschillende client hulpprogramma's. U kunt deze niet rechtstreeks gebruiken.  


## <a name="server-tools"></a>Server hulpprogramma's

Deze hulpprogram ma's bevinden `ServerTools` zich in de submap:

- [DP-taak wachtrij beheer](dp-job-manager.md): problemen met inhouds distributie taken naar distributie punten oplossen  

- [Verzamelings evaluatie-Viewer](ceviewer.md): Details van verzamelings evaluatie weer geven  

- [Inhouds bibliotheek Verkenner](content-library-explorer.md): inhoud van de inhouds bibliotheek Single Instance Store weer geven  

- [Overdracht van inhouds bibliotheek](content-library-transfer.md): inhouds bibliotheek verplaatsen tussen stations  

- [Hulp programma voor eigendom van inhoud](content-ownership-tool.md): wijzigt het eigendom van zwevende pakketten. Deze pakketten bevinden zich op de site zonder eigenaar van de site server.

- [Op rollen gebaseerd beheer en controle programma](rbaviewer.md): helpt beheerders bij het controleren van de configuratie van rollen  

- [Samenvattings programma voor metingen uitvoeren](run-meter-summ.md): taak samen vatting van meting uitvoeren en meet gegevens analyseren

> [!Note]  
> De map server-aan bevat ook de volgende bestanden:
>
> - AdminUI. WqlQueryEngine. dll
> - Microsoft. ConfigurationManagement. ManagementProvider. dll
> - Micro soft. Diagnostics. tracing. Event source. dll
>
> Deze bibliotheken zijn vereist voor verschillende server hulpprogramma's. U kunt ze niet rechtstreeks gebruiken.  

## <a name="other-tools-and-toolkits"></a>Andere hulpprogram ma's en tool kits

- [Ondersteunings centrum](support-center.md): informatie verzamelen van clients voor een eenvoudige analyse bij het oplossen van problemen.

    Vanaf versie 1906 is **OneTrace** een nieuwe logboek weergave met het ondersteunings centrum. Het werkt op dezelfde manier als CMTrace, met verbeteringen. Zie [ondersteunings centrum OneTrace](support-center-onetrace.md)voor meer informatie.

- [On-premises site uitbreiden en migreren naar Microsoft Azure](azure-migration-tool.md): helpt u bij het programmatisch maken van Azure virtual machines (vm's) voor Configuration Manager. <!--3556022--> 

- [Hulp programma voor opruimen van inhouds bibliotheken](../plan-design/hierarchy/content-library-cleanup-tool.md): `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` gebruik **ContentLibraryCleanup. exe** in om zwevende inhoud van een distributie punt te verwijderen.  

- [Hulp programma voor hiërarchie onderhoud](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): gebruik **preinst. exe** in de `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` gedeelde map op de site server om opdrachten door te geven aan het onderdeel hiërarchie beheer.  

- [Hulp programma voor het opnieuw instellen](../servers/manage/update-reset-tool.md)van de update `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` : gebruik **CMUpdateReset. exe** in om problemen op te lossen bij het downloaden of repliceren van updates in de console.  

- [Hulp programma voor service verbindingen](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): gebruik **ServiceConnectionTool. exe** in `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` om uw site up-to-date te houden wanneer uw service verbindings punt offline is.   

- [Micro soft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md): een verzameling hulpprogram ma's, processen en richt lijnen voor het automatiseren van implementaties van Desktop-en Server besturingssystemen.

- [System Center updates Publisher (Scup gemaakt)](../../sum/tools/updates-publisher.md): een zelfstandig hulp programma voor het beheren en importeren van aangepaste software-updates.

- [Pakket conversie beheer](../../apps/pcm/package-conversion-manager.md): Converteer verouderde pakketten naar toepassingen.

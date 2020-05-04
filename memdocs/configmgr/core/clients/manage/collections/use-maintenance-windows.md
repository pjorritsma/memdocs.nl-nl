---
title: Onderhouds Vensters gebruiken
titleSuffix: Configuration Manager
description: Gebruik verzamelingen en onderhouds Vensters om clients effectief te beheren in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c2128c9e26137c268577e68e5ee12e3a71f8513
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714442"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Onderhouds Vensters gebruiken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Onderhouds vensters bieden u de mogelijkheid om een tijd te definiëren waarop Configuration Manager bewerkingen kunnen worden uitgevoerd op een verzameling apparaten. U kunt onderhouds Vensters gebruiken om ervoor te zorgen dat wijzigingen in de client configuratie plaatsvinden tijdens peri Oden die geen invloed hebben op de productiviteit. Vanaf Configuration Manager versie 1806 kunnen uw gebruikers zien wanneer hun volgende onderhouds venster zich bevindt op het tabblad **installatie status** in het **Software Center**. <!--1358131-->

 De volgende bewerkingen ondersteunen onderhouds Vensters:  

- Software-implementatie  

- Software-update-implementaties  

- Implementatie en beoordeling van instellingen voor naleving  

- Implementaties van besturingssystemen  

- Implementaties van takenreeksen  

  Configureer onderhouds Vensters met een begin datum, een begin-en eind tijd en een terugkeer patroon. De maximale duur van een venster moet minder dan 24 uur zijn. Standaard is het opnieuw opstarten van een computer als gevolg van een implementatie niet toegestaan buiten een onderhouds venster, maar u kunt de standaard instelling onderdrukken. Onderhouds Vensters zijn alleen van invloed op het tijdstip waarop het implementatie programma wordt uitgevoerd. toepassingen die zijn geconfigureerd om lokaal te downloaden en uit te voeren, kunnen inhoud buiten het venster downloaden.  

  Wanneer een client computer lid is van een verzameling apparaten met een onderhouds venster, wordt een implementatie programma alleen uitgevoerd als de Maxi maal toegestane uitvoerings tijd de geconfigureerde duur voor het venster niet overschrijdt. Als de uitvoering van het programma mislukt, wordt er een waarschuwing gegenereerd en wordt de implementatie opnieuw uitgevoerd tijdens het volgende geplande onderhoudsvenster dat over voldoende tijd beschikt.  

## <a name="using-multiple-maintenance-windows"></a>Meerdere onderhoudsvensters gebruiken  
 Wanneer een client computer lid is van meerdere verzamelingen apparaten die onderhouds vensters hebben, gelden deze regels:  

- Als de onderhouds vensters elkaar niet overlappen, worden deze behandeld als twee onafhankelijke onderhouds Vensters.  

- Als de onderhouds vensters elkaar overlappen, worden ze behandeld als één onderhouds venster dat de tijds periode benadert die door beide onderhouds Vensters wordt gedekt. Als twee vensters bijvoorbeeld elk uur in de duur 30 minuten overlappen, zou de werkelijke duur van het onderhouds venster 90 minuten zijn.  

  Wanneer een gebruiker een installatie van een toepassing vanuit software Center initieert, wordt de toepassing onmiddellijk geïnstalleerd, ongeacht eventuele onderhouds Vensters.  

  Als de implementatie van een toepassing met het doel **Vereist** buiten kantooruren de installatiedeadline bereikt die door de gebruiker in Software Center is gedefinieerd, wordt de toepassing geïnstalleerd. 

### <a name="how-to-configure-maintenance-windows"></a>Onderhoudsvensters configureren  

1.  Kies in de Configuration Manager-console de optie **activa en naleving**>  van**apparaten**.  

3.  Selecteer een verzameling in de lijst **apparaat Collections** . U kunt geen onderhouds vensters maken voor de verzameling **alle systemen** .  

4.  Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

5.  Kies op het tabblad **onderhouds Vensters** van het ** &lt;dialoog venster Eigenschappen van verzamelings\> naam** het pictogram **Nieuw** .  

6.  Vul het ** &lt;dialoog\> venster nieuwe planning** in.  

7.  Maak een selectie in de vervolg keuzelijst **Dit schema Toep assen op** .  

8.  Kies **OK** en sluit vervolgens het ** &lt;dialoog venster\> eigenschappen van verzamelings naam** .  
 
## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Power shell gebruiken

Power shell kan worden gebruikt voor het configureren van onderhouds Vensters.  Zie voor meer informatie:

* [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow)
* [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow)
* [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow)
* [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow)

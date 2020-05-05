---
title: Mogelijkheden van Technical Preview 1602
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1602.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 64d01598f3d5feb162898761645ac84b1c73b175
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074466"
---
# <a name="capabilities-in-technical-preview-1602-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1602 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1602. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.  

 Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.  

##  <a name="improvements-to-mobile-device-management"></a><a name="BKMK_MDM"></a>Verbeteringen in Mobile Device Management  

### <a name="ios-activation-lock"></a>iOS-Activeringsslot  
 Configuration Manager kan u helpen bij het beheren van iOS-Activeringsslot, een functie van de app zoek mijn iPhone voor iOS 7,1 en hoger. Activeringsvergrendeling is automatisch ingeschakeld wanneer de app Zoek mijn iPhone op een apparaat wordt gebruikt. Nadat de vergrendeling is ingeschakeld, moeten de Apple ID en het wachtwoord van de gebruiker worden ingevoerd voordat een van de volgende handelingen kan worden verricht:  

- Zoek mijn iPhone uitschakelen  

- Het apparaat wissen  

- Het apparaat opnieuw activeren  

  Configuration Manager kunt de Activeringsslot status van apparaten onder Super visie en niet-super visie aanvragen waarop iOS 7,1 of hoger wordt uitgevoerd. Voor apparaten onder supervisie kan met Intune de bypass-code van de activeringsvergrendeling worden opgehaald direct aan het apparaat worden uitgegeven.  

##  <a name="improvements-to-software-center-in-version-1602"></a><a name="BKMK_SC1601"></a>Verbeteringen aan software Center in versie 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>PC-computer-en gebruikers beleid vernieuwen vanuit software Center  
 Er is een nieuwe optie voor het **synchronisatie beleid** toegevoegd aan de pagina **Opties** > **computer onderhoud** van software Center dat ervoor zorgt dat de PC het Configuration Manager computer-en gebruikers beleid vernieuwd.  

##  <a name="improvements-to-windows-10-servicing"></a><a name="BKMK_Win10Servicing"></a>Verbeteringen in Windows 10 Servicing  
 In de 1602 Technical Preview zijn de volgende verbeteringen toegevoegd voor Windows 10-onderhoud:  

-   Nieuwe filter opties voor onderhouds plannen.  U kunt nu filteren op **taal**, **vereist**en **titel**. Alleen de upgrades die voldoen aan de opgegeven criteria worden aan de gekoppelde implementatie toegevoegd.  

-   Wanneer u de classificatie **upgrades** voor software-update synchronisatie selecteert, wordt er een waarschuwings venster weer gegeven waarin u kunt zien dat WSUS [hotfix 3095113](https://support.microsoft.com/kb/3095113) is vereist voor het synchroniseren van software-updates en voor een goede werking van Windows 10-onderhoud.  Vanuit het dialoog venster kunt u naar het Knowledge Base-artikel voor de hotfix gaan.  

-   Beschik bare Windows 10-upgrades worden nu alleen weer gegeven in het knoop punt Windows 10- **onderhoud** \ **alle updates van Windows** 10 van de Configuration Manager-console. Deze updates worden niet meer weer gegeven in het knoop punt **Software** \ -updates**alle software-updates** .  

-   Eind gebruikers die een Windows 10-upgrade pakket starten, wordt gevraagd een dialoog venster op te geven waarmee ze kunnen weten dat ze hun besturings systeem upgraden.  

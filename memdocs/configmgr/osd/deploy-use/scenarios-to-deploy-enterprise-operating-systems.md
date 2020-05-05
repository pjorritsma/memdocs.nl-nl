---
title: Scenario's voor het implementeren van enterprise-besturingssystemen
titleSuffix: Configuration Manager
description: Meer informatie over verschillende scenario's voor het implementeren van ENTER prise-besturings systemen met Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07e8623928cbfe0bcd562d3d6efdf3a9ceee85ae
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723766"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Scenario's voor het implementeren van ENTER prise-besturings systemen met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De volgende implementatie scenario's voor besturings systemen zijn beschikbaar in Configuration Manager:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Windows bijwerken naar de laatste versie
Met dit scenario wordt het besturings systeem bijgewerkt op computers waarop momenteel Windows 7, Windows 8,1 of Windows 10 wordt uitgevoerd. Het upgrade proces houdt de toepassingen, instellingen en gebruikers gegevens op de computer. Er zijn geen externe afhankelijkheden, zoals de Windows ADK. Dit proces kan sneller en flexibeler zijn dan traditionele besturingssysteem implementaties.  

Zie [Windows upgraden naar de nieuwste versie](upgrade-windows-to-the-latest-version.md)voor meer informatie.


#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot implementeren voor bestaande apparaten
<!--3607717, fka 1358333-->
Vanaf versie 1810 is Windows auto pilot voor bestaande apparaten beschikbaar met Windows 10 versie 1809 of hoger. Met deze functie kunt u de installatie kopie van een Windows 7-apparaat voor de door de gebruiker gestuurde Windows-modus voor automatische Piloting en het inrichten met één Configuration Manager taken reeks.

Zie voor meer informatie [Windows auto pilot voor bestaande apparaten](windows-autopilot-for-existing-devices.md).


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Een bestaande computer vernieuwen met een nieuwe versie van Windows
In dit scenario wordt een bestaande computer gepartitioneerd en geformatteerd (gewist) en wordt een nieuw besturings systeem op de computer geïnstalleerd. U kunt instellingen en gebruikers gegevens migreren nadat het besturings systeem is geïnstalleerd.  

Zie [een bestaande computer vernieuwen met een nieuwe versie van Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)voor meer informatie.


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren
In dit scenario wordt een besturings systeem op een nieuwe computer geïnstalleerd. Het is een nieuwe installatie van het besturings systeem en bevat geen migratie van instellingen of gebruikers gegevens.  

Zie [een nieuwe versie van Windows installeren op een nieuwe computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)voor meer informatie.


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Een bestaande computer vervangen en de instellingen overzetten
In dit scenario wordt een besturings systeem op een nieuwe computer geïnstalleerd. U kunt eventueel instellingen en gebruikersgegevens van de oude computer naar de nieuwe computer migreren.  

Zie [een bestaande computer vervangen en de instellingen overzetten](replace-an-existing-computer-and-transfer-settings.md)voor meer informatie.



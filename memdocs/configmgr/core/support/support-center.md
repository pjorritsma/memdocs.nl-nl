---
title: Ondersteuningscentrum
titleSuffix: Configuration Manager
description: Problemen met Configuration Manager-clients oplossen met het ondersteunings centrum.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 788c48599ac8a94b8690f3a88f9761b9ae8ac742
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699429"
---
# <a name="support-center-for-configuration-manager"></a>Ondersteunings centrum voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1357489-->
Vanaf versie 1810, gebruikt u het ondersteunings centrum voor het oplossen van problemen met clients, het weer geven van real-time Logboeken of het vastleggen van de status van een Configuration Manager-client computer voor latere analyse. Ondersteunings centrum is één hulp programma voor het consolideren van veel hulpprogram ma's voor probleem oplossing.


## <a name="about"></a>Over

Het ondersteunings centrum is erop gericht de uitdagingen en frustraties te verminderen bij het oplossen van problemen Configuration Manager-client computers. Als u zich eerder bij het werken met ondersteuning voor het oplossen van een probleem met Configuration Manager-clients, moet u hand matig logboek bestanden en andere informatie verzamelen om het probleem op te lossen. Het was heel gemakkelijk om per ongeluk een cruciaal logboek bestand te verg eten, waardoor er extra pijnen worden veroorzaakt voor u en het ondersteunings personeel waarmee u samenwerkt.

Gebruik het ondersteunings centrum om de ondersteunings ervaring te stroom lijnen. U kunt het volgende doen:

- Maak een bundel voor probleem oplossing (zip-bestand) die de Configuration Manager client logboek bestanden bevat. U hebt dan één bestand dat u kunt verzenden naar ondersteunend personeel.  

- Configuration Manager client logboek bestanden, certificaten, register instellingen, debug dumps, client beleid weer geven.  

- Real-time diagnose van de inventaris (vervangt ContentSpy), beleid (vervangt PolicySpy) en de client cache.  

### <a name="support-center-viewer"></a>Viewer voor ondersteunings centrum

Ondersteunings centrum omvat de viewer voor ondersteunings centrum, een hulp programma dat het personeel ondersteunt om de bundel bestanden te openen die u maakt met ondersteunings centrum. De gegevens verzamelaar van het ondersteunings centrum verzamelt en verpakt Diagnostische logboeken van een lokale of externe Configuration Manager client. Als u gegevens verzamelaarsets wilt weer geven, gebruikt u de Viewer-toepassing.

### <a name="support-center-log-file-viewer"></a>Logboek bestand viewer voor ondersteunings centrum

Ondersteunings centrum bevat een moderne logboek viewer. Dit hulp programma vervangt CMTrace en biedt een aanpas bare interface met ondersteuning voor tabbladen en dockable Windows. De laag heeft een snelle presentatielaag en kan grote logboek bestanden in enkele seconden laden.

### <a name="support-center-onetrace-preview"></a>Ondersteuningscentrum OneTrace (preview)

<!--3555962-->
Vanaf versie 1906 is **OneTrace** een nieuwe logboek weergave met het ondersteunings centrum. Het werkt op dezelfde manier als CMTrace, met verbeteringen. Zie [ondersteunings centrum OneTrace](support-center-onetrace.md)voor meer informatie.

### <a name="powershell-cmdlets"></a>PowerShell-cmdlets

Ondersteunings centrum omvat ook [Power shell-cmdlets](/powershell/sccm/overview?view=sccm-ps). Gebruik deze cmdlets om een externe verbinding met een andere Configuration Manager-client te maken, de opties voor gegevens verzameling te configureren en gegevens verzameling te starten.


## <a name="prerequisites"></a>Vereisten

Installeer de volgende onderdelen op de server of client computer waarop u het ondersteunings centrum installeert:

- Een versie van het besturings systeem die wordt ondersteund door Configuration Manager. Zie [ondersteunde versies van besturings systemen voor clients](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)voor meer informatie. Het ondersteunings centrum biedt geen ondersteuning voor mobiele apparaten.  

- .NET Framework 4.5.2 is vereist op de computer waarop u het ondersteunings centrum en de bijbehorende onderdelen uitvoert.  


## <a name="install"></a>Installeren

Zoek het installatie programma voor het ondersteunings centrum op de site server op het volgende pad: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` .

Nadat u deze hebt geïnstalleerd, gaat u naar de volgende items in het menu Start van de groep **micro soft System Center** :  

- Ondersteunings centrum (ConfigMgrSupportCenter.exe)  
- Logboek bestand viewer voor ondersteunings centrum (CMLogViewer.exe)  
- Viewer voor ondersteunings centrum (ConfigMgrSupportCenterViewer.exe)  


## <a name="known-issues"></a>Bekende problemen

### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>U kunt de nieuwste versie niet installeren als er al een oudere versie is geïnstalleerd

<!--SCCMDocs-pr issue #3090-->
*Van toepassing op versies 1810 en 1902*

Als u al een oudere versie van het ondersteunings centrum hebt geïnstalleerd, mislukt het nieuwe installatie programma. Dit probleem wordt veroorzaakt door de versie van de bestanden tussen de oorspronkelijke versie en de meest recente versie. U kunt dit probleem omzeilen door de oudere versie van het ondersteunings centrum eerst te verwijderen. Installeer vervolgens de nieuwste versie.

### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>Externe verbindingen moeten de computer naam of het domein bevatten als onderdeel van de gebruikers naam

Als u verbinding maakt met een externe client vanuit ondersteunings centrum, moet u de computer naam of de domein naam voor het gebruikers account opgeven bij het tot stand brengen van de verbinding. Als u een steno computer naam of domein naam gebruikt (zoals `.\administrator` ), is de verbinding geslaagd, maar worden er geen gegevens van de client verzameld.

Als u dit probleem wilt voor komen, gebruikt u de volgende indelingen voor gebruikers namen om verbinding te maken met een externe client:

- `ComputerName\UserName`  
- `DomainName\UserName`  

### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>Script server bericht blok verbindingen met externe clients moeten mogelijk worden verwijderd

Wanneer u verbinding maakt met externe clients met behulp van de cmdlet [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) Power shell, maakt het ondersteunings centrum een Server Message Block (SMB)-verbinding met elke externe client. Deze verbindingen blijven behouden nadat u het verzamelen van gegevens hebt voltooid. Om te voor komen dat het maximum aantal externe verbindingen voor Windows wordt overschreden, gebruikt u de `net use` opdracht om de momenteel actieve set met externe verbindingen weer te geven. Schakel vervolgens alle overbodige verbindingen uit met behulp van de volgende opdracht: `net use <connection_name> /d`
waarbij `<connection_name>` de naam is van de externe verbinding.

### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>De aanvraag voor de evaluatie cyclus voor implementatie van de toepassing is niet correct naar externe computers verzonden

<!--2849356-->
*Van toepassing op versie 1810*

Als u in ondersteunings centrum de evaluatie van de **toepassings implementatie** selecteert van de actie **trigger activeren** op het tabblad **inhoud** , wordt met deze actie een taak gestart die geïmplementeerde toepassingen evalueert. Als u bent verbonden met een lokale client, worden de implementaties van computer-en gebruikers toepassingen geëvalueerd. Als u echter bent verbonden met een externe client, worden alleen de implementaties van machine toepassingen geëvalueerd.


## <a name="next-steps"></a>Volgende stappen

[Snelstartgids voor ondersteunings centrum](support-center-quickstart.md)
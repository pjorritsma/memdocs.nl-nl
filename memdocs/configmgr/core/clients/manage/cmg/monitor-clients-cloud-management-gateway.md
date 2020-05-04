---
title: Cloud beheer gateway bewaken
titleSuffix: Configuration Manager
description: Bewaak clients en netwerk verkeer via de Cloud Management Gateway (CMG).
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3233dc2f6bd13e56f7555536c95d42a34e01d5e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714225"
---
# <a name="monitor-cloud-management-gateway"></a>Cloud beheer gateway bewaken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat de Cloud beheer gateway (CMG) wordt uitgevoerd en er clients worden aangesloten, kunt u clients en netwerk verkeer controleren om ervoor te zorgen dat u weet hoe de service wordt uitgevoerd.


## <a name="monitor-clients"></a>Clients bewaken

Clients die zijn verbonden via de CMG, worden op dezelfde manier weer gegeven in de Configuration Manager-console als on-premises clients. Zie [clients controleren](../monitor-clients.md)voor meer informatie.


## <a name="monitor-traffic-in-the-console"></a>Verkeer bewaken in de-console

Verkeer op de CMG bewaken met behulp van de Configuration Manager-console:

1. Ga naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **cloudbeheergateway** .  

2. Selecteer de CMG in het lijst deel venster.  

3. Bekijk de verkeers gegevens in het detail venster voor het CMG-verbindings punt en de site systeem rollen waarmee verbinding wordt gemaakt. Deze statistieken tonen de client aanvragen die worden verzonden naar deze rollen. De aanvragen omvatten beleid, locatie, registratie, inhoud, inventaris en client meldingen.<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>Waarschuwingen voor uitgaand verkeer instellen

Met waarschuwingen voor uitgaand verkeer weet u wanneer het netwerk verkeer een drempel niveau van 14 dagen nadert. Wanneer u de CMG maakt, kunt u waarschuwingen voor verkeer instellen. Als u dat onderdeel hebt overgeslagen, kunt u de waarschuwingen nog steeds instellen nadat de service wordt uitgevoerd. De instellingen voor waarschuwingen op elk gewenst moment aanpassen.

1. Ga naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **cloudbeheergateway** .  

2. Selecteer de CMG in het lijst deel venster en selecteer vervolgens **Eigenschappen** in het lint.  

3. Ga naar het tabblad **waarschuwingen** om de drempel en waarschuwingen in te scha kelen. Geef de drempel waarde voor 14 dagen op in gigabytes (GB). Geef ook het drempel percentage op om de verschillende waarschuwings niveaus te verhogen.  

4. Wanneer u gereed bent, selecteert u **OK**.  


## <a name="monitor-logs"></a>Logboeken bewaken

De CMG genereert vermeldingen in een aantal logboek bestanden. Zie [Configuration Manager-logboeken](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)voor meer informatie.


## <a name="cloud-management-dashboard"></a>Dash board voor Cloud beheer

<!--1358461-->
Vanaf versie 1806 biedt het dash board voor Cloud beheer een gecentraliseerde weer gave voor het gebruik van CMG. Wanneer de site is voor bereid op [Azure-Services](../../../servers/deploy/configure/azure-services-wizard.md) voor Cloud beheer, worden er ook gegevens weer gegeven over Cloud gebruikers en-apparaten.  

De volgende scherm afbeelding is een deel van het dash board voor Cloud beheer met twee van de beschik bare tegels:  
![Cloud beheer dashboard tegels CMG verkeer en huidige online clients](media/1358461-cmg-dashboard.png)

Ga in de Configuration Manager-console naar de werk ruimte **bewaking** . Selecteer het knoop punt voor **Cloud beheer** en Bekijk de dashboard tegels.  


## <a name="connection-analyzer"></a>Connection Analyzer

Vanaf versie 1806, gebruikt u de CMG Connection Analyzer voor realtime verificatie om problemen op te lossen. Het console-hulp programma controleert de huidige status van de service en het communicatie kanaal via het CMG-verbindings punt naar een beheer punt dat CMG-verkeer toestaat.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **Cloud Services** uit en selecteer het knoop punt voor de **Cloud beheer gateway** .  

2. Selecteer de doel-CMG instantie en selecteer vervolgens **verbindings analyse** in het lint.  

3. Selecteer in het venster CMG Connection Analyzer een van de volgende opties om te verifiëren bij de service:  

     1. **Azure AD-gebruiker**: gebruik deze optie om de communicatie te simuleren op dezelfde manier als een cloud-gebaseerde gebruikers-id die is aangemeld bij een Windows 10-apparaat dat is toegevoegd aan Azure AD. Klik op **Aanmelden** om de referenties voor dit Azure AD-gebruikers account veilig in te voeren.  

     2. **Client certificaat**: gebruik deze optie om communicatie te simuleren op dezelfde manier als een Configuration Manager client met een [certificaat voor client verificatie](certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Selecteer **starten** om de analyse te starten. In het venster analyse worden de resultaten weer gegeven. Selecteer een vermelding om meer details te bekijken in het veld Beschrijving.  


## <a name="stop-cmg-when-it-exceeds-threshold"></a><a name="bkmk_stop"></a>CMG stoppen als de drempel waarde wordt overschreden

<!--3735092-->
Vanaf versie 1902 kan Configuration Manager nu een CMG-service stoppen als de totale gegevens overdracht meer dan uw limiet overschrijdt. [Waarschuwingen](#set-up-outbound-traffic-alerts) gebruiken om meldingen te activeren wanneer het gebruik een waarschuwing of kritiek niveau bereikt. Met deze optie wordt de Cloud service uitgeschakeld om eventuele onverwachte Azure-kosten te verminderen vanwege een piek in het gebruik.

> [!Important]  
> Zelfs als de service niet wordt uitgevoerd, zijn er nog steeds kosten verbonden aan de Cloud service. Als u de service stopt, worden niet alle gekoppelde Azure-kosten geëlimineerd. Als u alle kosten voor de Cloud service wilt verwijderen, [verwijdert u de CMG](setup-cloud-management-gateway.md#modify-a-cmg).  
>
> Wanneer de CMG-service wordt gestopt, kunnen clients op internet niet communiceren met Configuration Manager.  

De totale gegevens overdracht (uitgaand verkeer) bevat gegevens uit de Cloud service en het opslag account. Deze gegevens zijn afkomstig van de volgende stromen:

- CMG naar client  
- CMG naar site, inclusief CMG-logboek bestanden  
- Als u CMG inschakelt voor inhoud, opslag account naar client  

Zie [CMG ports and data flow](plan-cloud-management-gateway.md#ports-and-data-flow)(Engelstalig) voor meer informatie over deze gegevens stromen.

De waarschuwings drempel voor opslag is afzonderlijk. Met deze waarschuwing wordt de capaciteit van uw Azure Storage-exemplaar gecontroleerd.

Wanneer u het CMG-exemplaar selecteert in het knoop punt **cloudbeheergateway** in de-console, ziet u de totale gegevens overdracht in het detail venster.

Configuration Manager controleert de drempel waarde elke zes minuten. Als er sprake is van een plotselinge piek in het gebruik, kan het tot zes minuten duren voordat Configuration Manager de drempel waarde heeft overschreden en de service vervolgens stopt.

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>Proces voor het stoppen van de Cloud service wanneer deze de drempel waarde overschrijdt

1. [Waarschuwingen voor uitgaand verkeer instellen](#set-up-outbound-traffic-alerts).  

2. Schakel op het tabblad **waarschuwingen** van het venster Eigenschappen van CMG de optie in om **deze service te stoppen wanneer de kritieke drempel waarde wordt overschreden**.  

Als u deze functie wilt testen, verkleint u tijdelijk een van de volgende waarden:  

- **drempel waarde van 14 dagen voor uitgaande gegevens overdracht (GB)**. De standaardwaarde is `10000`.  

- Het **percentage van de drempel waarde voor het verhogen van de kritieke waarschuwing**. De standaardwaarde is `90`.  

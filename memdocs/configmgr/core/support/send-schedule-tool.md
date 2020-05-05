---
title: Hulpprogramma voor het verzenden van planningen
titleSuffix: Configuration Manager
description: Gebruik het hulp programma planning verzenden om een planning op een Configuration Manager-client te activeren.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78e154c5361063224d9e8c99bc87ba117958edf4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723122"
---
# <a name="send-schedule-tool"></a>Hulpprogramma voor het verzenden van planningen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het hulp programma planning verzenden is een van de [Configuration Manager-hulpprogram ma's](tools.md). Gebruik het om een planning te activeren op een client of de evaluatie van een opgegeven configuratie basislijn te activeren. Het werkt voor de lokale computer of het doel van een externe client.  

Gebruik bijvoorbeeld het hulp programma om een inventaris planning of compatibiliteits evaluatie te activeren. Als een aantal Configuration Manager-clients onlangs geen inventaris-of nalevings status hebben gerapporteerd, voert u het hulp programma uit om de benodigde planning op elke client te initiëren.



## <a name="usage"></a>Gebruik

Voer **SendSchedule. exe** uit als Administrator. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

Nadat u een bericht (GUID) hebt geactiveerd, raadpleegt u **SMSClientMethodProvider. log**. Zie [bericht-id's](#bkmk_sendschedule-guids)voor meer informatie over de beschik bare bericht-guid's.

Nadat u de evaluatie van een configuratie basislijn (DCM UID) hebt geactiveerd, raadpleegt u **DCMAgent. log**.



## <a name="command-line-options"></a>Opdrachtregelopties


### <a name="option-l"></a>Selecteert`/L` 
Alle bericht-GUID of DCM-UID weer geven die beschikbaar is voor verzen ding. De betekenis volle naam van berichten in de gegevens tabel weer geven voor elk item. Als de computer naam ontbreekt, wordt de lokale computer gebruikt. Als u een bericht zonder computer naam opgeeft, wordt het bericht naar de lokale computer verzonden. 



## <a name="examples"></a>Voorbeelden

#### <a name="list-the-available-messages-on-the-local-machine"></a>De beschik bare berichten op de lokale computer weer geven 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>De beschik bare berichten op de client-MyPC lijst weer geven: 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Hardware-inventaris op de lokale computer activeren
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>Hardware-inventaris op MyPC activeren: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>De evaluatie van een specifieke configuratie basislijn op MyPC activeren: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="message-ids"></a><a name="bkmk_sendschedule-guids"></a>Bericht-Id's

|Bericht-ID  |Weergavenaam  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Hardware-inventaris|
|{00000000-0000-0000-0000-000000000002}|Software-inventaris|
|{00000000-0000-0000-0000-000000000003}|Detectie-inventaris|
|{00000000-0000-0000-0000-000000000010}|Bestands verzameling|
|{00000000-0000-0000-0000-000000000011}|IDMIF-verzameling|
|{00000000-0000-0000-0000-000000000021}|Machine toewijzingen aanvragen|
|{00000000-0000-0000-0000-000000000022}|Computer beleid evalueren|
|{00000000-0000-0000-0000-000000000023}|Standaard taak MP vernieuwen|
|{00000000-0000-0000-0000-000000000024}|LS (locatie service) taak voor het vernieuwen van locaties|
|{00000000-0000-0000-0000-000000000025}|Time-out bij het vernieuwen van LS|
|{00000000-0000-0000-0000-000000000026}|Toewijzing van beleids agent aanvragen (gebruiker)|
|{00000000-0000-0000-0000-000000000027}|Toewijzing van beleids agent evalueren (gebruiker)|
|{00000000-0000-0000-0000-000000000031}|Gebruiks rapport van software licentie controle genereren|
|{00000000-0000-0000-0000-000000000032}|Bericht bron update|
|{00000000-0000-0000-0000-000000000037}|Cache met proxy-instellingen wissen|
|{00000000-0000-0000-0000-000000000040}|Opschonen van de machine beleids agent|
|{00000000-0000-0000-0000-000000000041}|Gebruikers beleids agent opschonen|
|{00000000-0000-0000-0000-000000000042}|Beleids agent computer beleid/toewijzing valideren|
|{00000000-0000-0000-0000-000000000043}|Beleids agent gebruikers beleid/toewijzing valideren|
|{00000000-0000-0000-0000-000000000051}|Opnieuw proberen/vernieuwen van certificaten in AD in MP|
|{00000000-0000-0000-0000-000000000061}|Peer DP-status rapportage|
|{00000000-0000-0000-0000-000000000062}|Pakket controle schema peer DP in behandeling|
|{00000000-0000-0000-0000-000000000063}|Planning SUM-updates installeren|
|{00000000-0000-0000-0000-000000000101}|Verzamelings cyclus voor hardware-inventaris|
|{00000000-0000-0000-0000-000000000102}|Verzamelings cyclus van software-inventaris|
|{00000000-0000-0000-0000-000000000103}|Verzamel fase detectie gegevens|
|{00000000-0000-0000-0000-000000000104}|Verzamel fase bestanden|
|{00000000-0000-0000-0000-000000000105}|IDMIF-verzamelings cyclus|
|{00000000-0000-0000-0000-000000000106}|Gebruiks rapport cyclus voor software licentie controle|
|{00000000-0000-0000-0000-000000000107}|Update fase van de bron lijst Windows Installer|
|{00000000-0000-0000-0000-000000000108}|Evaluatie cyclus voor software-update-beleids acties voor software-updates|
|{00000000-0000-0000-0000-000000000109}|Onderhouds taak voor het onderhouds beleid van de vertakkings verdeling|
|{00000000-0000-0000-0000-000000000110}|DCM-beleid|
|{00000000-0000-0000-0000-000000000111}|Bericht over niet-verzonden status verzenden|
|{00000000-0000-0000-0000-000000000112}|Cache cleanout status systeem beleid|
|{00000000-0000-0000-0000-000000000113}|Bron beleid bijwerken|
|{00000000-0000-0000-0000-000000000114}|Archief beleid bijwerken|
|{00000000-0000-0000-0000-000000000115}|Status systeem beleid bulksgewijs verzenden hoog|
|{00000000-0000-0000-0000-000000000116}|Status systeem beleid bulksgewijs verzenden laag|
|{00000000-0000-0000-0000-000000000121}|Beleids actie toepassings beheer|
|{00000000-0000-0000-0000-000000000122}|Actie gebruikers beleid toepassings beheer|
|{00000000-0000-0000-0000-000000000123}|Globale evaluatie actie van toepassings beheer|
|{00000000-0000-0000-0000-000000000131}|Start samenvattings programma voor energie beheer|
|{00000000-0000-0000-0000-000000000221}|Implementatie van eind punten opnieuw evalueren|
|{00000000-0000-0000-0000-000000000222}|Endpoint AM-beleid wordt opnieuw geëvalueerd|
|{00000000-0000-0000-0000-000000000223}|Externe gebeurtenis detectie|




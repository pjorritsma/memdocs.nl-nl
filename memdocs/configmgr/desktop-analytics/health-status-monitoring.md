---
title: Status bewaken
titleSuffix: Configuration Manager
description: Meer informatie over hoe status controle werkt in Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 119f787f15b8c907d0c760a12b973ca984f4348c
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268535"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Controle van de status van de Desktop Analytics

Wanneer u [een update voor productie implementeert](deploy-prod.md), gebruikt u Desktop Analytics om de status van uw apparaten te bewaken. In dit artikel wordt gedetailleerd uitgelegd hoe status controle werkt.

Zie [de status van bijgewerkte apparaten bewaken](deploy-prod.md#bkmk_monitor)voor meer informatie over het gebruik van deze functie.

![Scherm afbeelding van de pagina status controleren van Desktop Analytics](media/monitor-health.png)

> [!NOTE]  
> Desktop Analytics verzamelt alleen status gegevens van apparaten die gebruiks gegevens leveren die kunnen worden gebruikt als noemer. Dit betekent dat er geen apparaten worden geleverd met Windows 7 en Windows 10 die niet zijn ingesteld voor het delen van diagnostische gegevens op het niveau verbeterd (beperkt). Als er meer dan 10% van de apparaten met Windows 10 zijn ingesteld op het delen van diagnostische gegevens op andere niveaus dan uitgebreid (beperkt), wordt op de pagina **status controleren** een waarschuwing weer gegeven in het gebied banner.  

Als u meer informatie over een specifieke app wilt weer geven, selecteert u deze in de lijst.

## <a name="apps"></a>Apps

### <a name="health-status-factors"></a>Status factoren

![Status factoren voor een app in Desktop Analytics](media/monitor-health-status-factors.png)

Met Desktop Analytics worden de volgende status factoren voor apps bewaakt:

- **% Apparaten met crashes**: gedurende de afgelopen twee weken is het aantal apparaten waarop deze specifieke app is gecrasht gedeeld door het aantal apparaten waarop de app is gebruikt. In deze weer gave kunt u zien of de stabiliteit van de app is verg root of verkleind op de nieuwe versie van het besturings systeem. Desktop Analytics berekent dit percentage voor de volgende sets:  

  - **Na update**: apparaten die zijn bijgewerkt naar de doel besturingssysteem versie die is opgegeven in het implementatie plan. Desktop Analytics verzamelt deze gegevens voor al uw bijgewerkte apparaten om het aantal assets met onvoldoende gegevens te verminderen. Deze set bevat de apparaten die niet in het implementatie plan zijn opgenomen.  

  - **Vóór update**: apparaten die zich op een besturingssysteem versie eerder bevinden dan wat is opgegeven in het implementatie plan. Deze lijst bevat geen apparaten met Windows 7.  

  - **Commercieel Gem**: de gemiddelde crash frequentie (gemiddeld) op alle commerciële apparaten. Dit gemiddelde wordt berekend over *alle* versies van de app. Als in uw versie een crash frequentie wordt weer gegeven die hoger is dan het commerciële gemiddelde, is er mogelijk een stabielere versie beschikbaar.  

- **% Sessies met crashes**: vergelijkbaar met de voor gaande, maar telt het percentage sessies met crashes in de afgelopen twee weken.  

Voor het bepalen van de status van een app vereist Desktop Analytics gegevens van ten minste 20 apparaten. Als dat niet het geval is, worden er **onvoldoende gegevens** voor de app gerapporteerd. De service berekent de status op basis van de *crash frequentie* van de sessie van deze apparaten. De crash frequentie van het apparaat wordt alleen ter informatie verstrekt. Deze wordt niet gebruikt in de berekening van de status status.

### <a name="usage"></a>Gebruik

<!-- 5533890 -->

- **Actieve apparaten**: deze waarde is het aantal apparaten waarbij een gebruiker de geselecteerde app in de afgelopen twee weken heeft gestart. Het is gebaseerd op apparaten in het geselecteerde implementatie plan waarop de doel versie van Windows 10 wordt uitgevoerd.

- **Sessies**: deze waarde is het totale aantal keer dat een gebruiker de geselecteerde app heeft gestart op de doel versie van Windows.

### <a name="additional-tabs"></a>Extra tabbladen

Onder aan de pagina app-Details kunt u de volgende drie tabbladen gebruiken om problemen op te lossen:

- **Andere versies**: een lijst met alternatieve versies van deze app. Voor elke versie worden de relatieve wijzigingen in de crash-tarieven binnen uw organisatie en het commerciële gemiddelde weer gegeven. Als u een nieuwere versie van de app met een lagere crash frequentie vindt, kan het bijwerken van de app helpen.  

    Ook wordt aangegeven of de versie geavanceerde inzichten heeft. Zie [Compatibility Assessment](compat-assessment.md)(Engelstalig) voor meer informatie.  

- **Belangrijkste problemen**: een lijst met de meest voorkomende fout-id's per exemplaar aantal. Een fout-ID geeft de stack tracering aan die is gekoppeld aan de crash. U kunt deze ID gebruiken wanneer u de leverancier van de app aanroept voor ondersteuning.  

- **Recente crashes**: een lijst met apparaten waarop de app onlangs is vastgelopen. U kunt filteren op fout-ID en andere criteria. Gebruik deze informatie om het probleem op te lossen door Logboeken te verzamelen of oplossingen te proberen op specifieke apparaten voordat u een bredere implementatie probeert.  

Als u een ernstige gezondheids regressie vindt die u niet kunt oplossen, wijzigt u de **upgrade beslissing** van de app in **niet**. Deze actie voor komt toekomstige implementatie van de update voor apparaten met deze asset.

## <a name="see-also"></a>Zie ook

- [Compatibiliteits evaluatie in Desktop Analytics](compat-assessment.md)  

- [Implementatie in productie met Desktop Analytics](deploy-prod.md)  

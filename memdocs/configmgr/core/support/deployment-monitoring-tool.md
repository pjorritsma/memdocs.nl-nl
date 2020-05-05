---
title: Hulpprogramma voor implementatiebewaking
titleSuffix: Configuration Manager
description: Gebruik het hulp programma voor implementatie bewaking om software-implementaties op een Configuration Manager-client op te lossen.
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723374"
---
# <a name="deployment-monitoring-tool"></a>Hulpprogramma voor implementatiebewaking

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het hulp programma voor implementatie bewaking is een van de [Configuration Manager-hulpprogram ma's](tools.md). Het is een Graphical User Interface die is ontworpen om u te helpen bij het oplossen van problemen met toepassingen, software-updates en configuratie basislijn implementaties op een Configuration Manager-client. Het hulp programma heeft het kenmerk alleen-lezen omdat er geen status op de client wordt gewijzigd. U kunt dit veilig gebruiken om veelvoorkomende implementatie scenario's te diagnosticeren.


## <a name="features"></a>Functies

- Als beheerder uitvoeren om implementaties op een lokale client op te lossen.  

- Problemen met implementaties op een externe client oplossen. Start het hulp programma en maak verbinding met een externe computer als beheerder.  

- Exporteren naar XML alle gegevens die in het hulp programma zijn verzameld. Deel het XML-bestand met anderen en gebruik dit als een algemeen platform voor het bespreken van problemen met de implementatie van het probleem.  

- Importeer eerder geëxporteerde gegevens naar een andere machine en gebruik deze om het hulp programma uit te voeren in de offline modus.   


## <a name="usage"></a>Gebruik

Het hulp programma voor implementatie bewaking ondersteunt alleen Graphical User Interface. Als u het hulp programma wilt starten, voert u **DeploymentMonitoringTool. exe** uit als Administrator. Er zijn drie weer gaven:  

- **Client eigenschappen**: een lijst met nuttige kenmerken over het apparaat en de Configuration Manager-client. Deze weer gave is de standaard instelling.   

- **Implementaties**: Bekijk alle huidige gerichte implementaties. Selecteer een implementatie in het resultaten venster om meer informatie in het detail venster weer te geven.  

- **Alle updates**: Bekijk alle software-updates en hun status.  

Als u gegevens in een weer gave wilt kopiëren, selecteert u een cel en drukt u op **CTRL** + **C**.


### <a name="actions-menu"></a>Menu acties

De volgende acties zijn beschikbaar in het menu **acties** :  

- **Verbinding maken met externe computer**: Selecteer een computer waarmee u verbinding wilt maken. Wanneer u geen gebruikers naam en wacht woord opgeeft, worden de huidige referenties gebruikt. Klik op **Opslaan** om verbinding te maken met een externe computer.  

- **Gegevens exporteren**: Selecteer het bestand waarin u de gegevens wilt schrijven en klik op **Opslaan**. Het geëxporteerde XML-bestand gebruiken voor extern oplossen van problemen op een andere computer.  

- **Gegevens importeren**: Selecteer een bestand dat u wilt importeren in het hulp programma.  

- **Logboek weer geven**: Hiermee opent u een gekoppeld logboek bestand, afhankelijk van de weer gave:  
    - Client eigenschappen:`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Implementaties`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Alle updates:`C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Zie ook

- [Toepassingen implementeren](../../apps/deploy-use/deploy-applications.md)
- [Software-updates implementeren](../../sum/deploy-use/deploy-software-updates.md)
- [Configuratiebasislijnen implementeren](../../compliance/deploy-use/deploy-configuration-baselines.md)

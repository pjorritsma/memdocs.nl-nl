---
title: Een servergroep onderhouden
titleSuffix: Configuration Manager
description: Server groepen zijn vervangen door Orchestration-groepen
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: a5475d2a33ebcf7fb2e1500a8dc6573180b9a70c
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608391"
---
# <a name="service-a-server-group"></a>Een servergroep onderhouden

*Van toepassing op: Configuration Manager (huidige vertakking)*

>[!IMPORTANT]
> - Vanaf Configuration Manager versie 2002 zijn Server groepen vervangen door Orchestration-groepen. Zie [Orchestration-groepen](orchestration-groups.md)voor meer informatie.
> - Functies van de voorlopige versie zijn functies die in de Current Branch voor vroege tests in een productie omgeving. Deze functies worden volledig ondersteund, maar zijn nog steeds actief in ontwikkeling en kunnen wijzigingen ontvangen totdat ze buiten de voorlopige categorie zijn geplaatst. U moet deze functie inschakelen om deze beschikbaar te maken. Zie [Use pre-release features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Functies van evaluatieversies gebruiken) voor meer informatie.

Vanaf Configuration Manager versie 1606 kunt u instellingen voor de Server groep voor een verzameling configureren om te definiëren hoeveel, welk percentage, of in welke volg orde computers in de verzameling software-updates zullen installeren. U kunt ook vooraf-implementatie en Power shell-scripts na implementatie configureren om aangepaste acties uit te voeren.

Wanneer u software-updates implementeert voor een verzameling met geconfigureerde instellingen voor de Server groep, bepaalt Configuration Manager op hoeveel computers in de verzameling de software-updates op een bepaald moment kunnen worden geïnstalleerd en wordt hetzelfde aantal implementatie vergrendelingen beschikbaar gemaakt. Alleen computers die een implementatie vergrendeling downloaden, starten de installatie van software-updates. Wanneer een implementatie vergrendeling beschikbaar is, krijgt de computer de implementatie vergrendeling, worden de software-updates geïnstalleerd en wordt de implementatie vergrendeling vrijgegeven wanneer de installatie van software-updates is voltooid. Vervolgens wordt de implementatie vergrendeling beschikbaar voor andere computers. Als een computer geen implementatie vergrendeling kan vrijgeven, kunt u alle implementatie vergrendelingen van de Server groep hand matig vrijgeven voor de verzameling.

>[!IMPORTANT]
>Alle computers in de verzameling moeten worden toegewezen aan dezelfde site.

#### <a name="to-create-a-collection-for-a-server-group"></a>Een verzameling voor een server groep maken  
De instellingen van de Server groep worden geconfigureerd in de eigenschappen voor een verzameling apparaten. Als u een server groep wilt onderhouden, moeten alle leden in de verzameling worden toegewezen aan dezelfde site. Gebruik de volgende stappen voor het maken van een verzameling en het configureren van de instellingen van de Server groep:
1.  [Maak een verzameling apparaten](../../core/clients/manage/collections/create-collections.md) die de computers in de Server groep bevat.  

2.  Klik in de werk ruimte **activa en naleving** op **apparaten verzamelingen**, klik met de rechter muisknop op de verzameling met de computers in de Server groep en klik vervolgens op **Eigenschappen**.  

3.  Selecteer op het tabblad **Algemeen** de optie **alle apparaten zijn onderdeel van dezelfde server groep**en klik vervolgens op **instellingen**.  

4.  Geef op de pagina **instellingen voor Server groep** een van de volgende instellingen op:  

    -   **Toestaan dat een percentage van de machines tegelijk wordt bijgewerkt**: Hiermee geeft u op dat alleen een bepaald percentage van clients tegelijk wordt bijgewerkt. Als de verzameling bijvoorbeeld 10 clients heeft en de verzameling zodanig is geconfigureerd dat 30% van de clients tegelijkertijd wordt bijgewerkt, worden er door slechts drie clients software-updates op een bepaald moment geïnstalleerd.  

    -   **Toestaan dat een aantal machines tegelijk wordt bijgewerkt**: Hiermee geeft u op dat slechts een bepaald aantal clients tegelijk wordt bijgewerkt.  

    -   **De onderhouds volgorde opgeven**: Hiermee geeft u op dat de clients in de verzameling op één keer worden bijgewerkt in de volg orde die u configureert. Een client installeert alleen software-updates nadat de installatie van de software-updates is voltooid door de client die zich voordoet in de lijst.  

5.  Geef aan of u een script voor het uitvoeren van een voor bereiding (knooppunt afvoer) of na de implementatie (knoop punt voor het hervatten) wilt gebruiken.  

    > [!WARNING]
    > Aangepaste scripts zijn niet ondertekend door micro soft. Het is uw verantwoordelijkheid om de integriteit van deze scripts te hand haven.

    > [!TIP]  
    > Hier volgen enkele voor beelden die u kunt gebruiken bij het testen van scripts voor vóór de implementatie en na de implementatie die de huidige tijd naar een tekst bestand schrijven:  
    >   
    >  **Pre-implementatie**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **Na de implementatie**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Software-updates implementeren in de Server groep en de status van de monitor  
U implementeert software-updates in de verzameling van Server groepen met behulp van het typische implementatie proces. Nadat u de software-updates hebt geïmplementeerd, kunt u de implementatie van software-updates in de Configuration Manager-console bewaken.
1.  [Software-updates implementeren](manually-deploy-software-updates.md) in de verzameling van Server groepen.   

2.  [Controleer de implementatie van de software-update](monitor-software-updates.md). Naast de standaard weergave weergaven voor de implementatie van software-updates, wordt de **wacht tijd voor vergren deling** weer gegeven wanneer een client op zijn beurt wacht om de software-updates te installeren. U kunt het bestand UpdatesDeployment. log controleren voor meer informatie.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>De implementatie vergrendelingen wissen voor computers in een server groep  
Wanneer een computer een implementatie vergrendeling niet kan vrijgeven, kunt u hand matig alle implementatie vergrendelingen van de Server groep voor de verzameling vrijgeven. Schakel de vergren delingen alleen uit wanneer een implementatie is vastgelopen bij het bijwerken van computers in de verzameling en er computers zijn die nog niet compatibel zijn.  
1.  Klik in de werk ruimte **activa en naleving** op **apparaten verzamelingen**en klik op de verzameling om de implementatie vergrendelingen te wissen.  

2.  Klik op het tabblad **Start** , in de groep **implementatie** , op **Server groep implementatie vergrendelingen wissen**. De implementatie vergrendelingen kunnen hand matig worden gewist wanneer clients de software-updates niet hebben geïnstalleerd en de software-updates niet worden geïnstalleerd door andere clients.  

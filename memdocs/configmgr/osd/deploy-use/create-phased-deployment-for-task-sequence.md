---
title: Gefaseerde implementaties maken
titleSuffix: Configuration Manager
description: Gebruik gefaseerde implementaties om de implementatie van software in meerdere verzamelingen te automatiseren.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1845b381d8b37fed3a785475e961cd39c54cf42d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125267"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Gefaseerde implementaties met Configuration Manager maken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met gefaseerde implementaties wordt een gecoördineerde, geordende implementatie van software in meerdere verzamelingen geautomatiseerd. U kunt bijvoorbeeld software implementeren op een pilot verzameling en vervolgens de implementatie automatisch voortzetten op basis van de criteria voor geslaagde pogingen. Maak gefaseerde implementaties met de standaard twee fasen of configureer hand matig meerdere fasen. 

Gefaseerde implementaties maken voor de volgende objecten:
- **Takenreeks**  
    - De gefaseerde implementatie van taken reeksen biedt geen ondersteuning voor de installatie van PXE of media   
- **Toepassing** (vanaf versie 1806) <!--1358147-->  
- **Software-update** (vanaf versie 1810) <!--1358146-->  
    - U kunt geen automatische implementatie regel gebruiken met een gefaseerde implementatie

> [!Tip]  
> De functie gefaseerde implementatie werd voor het eerst in versie 1802 geïntroduceerd als een [voorlopige functie](../../core/servers/manage/pre-release-features.md). Vanaf versie 1806 is het niet langer een functie van de voorlopige versie.<!--1356837-->  



## <a name="prerequisites"></a>Vereisten

#### <a name="security-scope"></a>Beveiligings bereik
Implementaties die zijn gemaakt door gefaseerde implementaties zijn niet zichtbaar voor gebruikers met beheerders rechten die niet over het bereik **alle** beveiliging beschikken. Zie [Beveiligingsbereiken](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)voor meer informatie.

#### <a name="distribute-content"></a>Inhoud distribueren
Voordat u een gefaseerde implementatie maakt, distribueert u de gekoppelde inhoud naar een distributie punt.<!--518293-->  

- **Toepassing**: Selecteer de doel toepassing in de console en gebruik de actie **inhoud distribueren** in het lint. Zie [inhoud implementeren en beheren](../../core/servers/deploy/configure/deploy-and-manage-content.md)voor meer informatie.   

- **Taken reeks**: u moet gerefereerde objecten maken, zoals het upgrade pakket van het besturings systeem voordat u de taken reeks maakt. Distribueer deze objecten voordat u een implementatie maakt. Gebruik de actie voor het **distribueren van inhoud** op elk object of de taken reeks. Als u de status van alle inhoud waarnaar wordt verwezen, wilt weer geven, selecteert u de taken reeks en schakelt u over naar het tabblad **verwijzingen** in het detail venster. Zie voor meer informatie het specifieke object type bij de [voor bereiding van de besturingssysteem implementatie](../get-started/prepare-for-operating-system-deployment.md).   

- **Software-update**: Maak het implementatie pakket en distribueer het. Gebruik de wizard software-updates downloaden. Zie [software-updates downloaden](../../sum/deploy-use/download-software-updates.md)voor meer informatie.  



## <a name="phase-settings"></a><a name="bkmk_settings"></a>Fase-instellingen

Deze instellingen zijn uniek voor gefaseerde implementaties. Configureer deze instellingen bij het maken of bewerken van de fasen om de planning en het gedrag van het gefaseerde implementatie proces te bepalen. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Criteria voor het slagen van de eerste fase  

- **Percentage geslaagde implementaties**: Geef het percentage apparaten op dat de implementatie moet volt ooien voordat de eerste fase slaagt. Deze waarde is standaard 95%. Met andere woorden, de site beschouwt de eerste fase als geslaagd wanneer de nalevings status voor 95% van de apparaten is **geslaagd** voor deze implementatie. De site gaat vervolgens door naar de tweede fase en maakt een implementatie van de software voor de volgende verzameling.  
- **Aantal apparaten dat is geïmplementeerd**: toegevoegd Configuration Manager versie 1902. Geef het aantal apparaten op dat de implementatie moet volt ooien voordat de eerste fase slaagt. Deze optie is handig als de grootte van de verzameling variabel is en u een specifiek aantal apparaten hebt om het succes weer te geven voordat u verdergaat met de volgende fase. <!--3555946-->


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Voor waarden voor het starten van de tweede fase van de implementatie na het Wels lagen van de eerste fase  

- **Deze fase automatisch starten na een uitstel periode (in dagen)**: Kies het aantal dagen dat moet worden gewacht voordat de tweede fase wordt gestart na het slagen van de eerste. Deze waarde is standaard één dag.  

- **De tweede fase van de implementatie hand matig starten**: de tweede fase wordt niet automatisch door de site gestart nadat de eerste fase is geslaagd. Voor deze optie moet u de tweede fase hand matig starten. Zie voor meer informatie naar [de volgende fase gaan](manage-monitor-phased-deployments.md#bkmk_move).  

    > [!Note]  
    > Deze optie is niet beschikbaar voor gefaseerde implementaties van toepassingen.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Deze software geleidelijk beschikbaar maken gedurende deze periode (in dagen)
<!--1358578-->
Vanaf versie 1806 kunt u deze instelling configureren voor de implementatie in elke fase, zodat deze geleidelijk plaatsvindt. Dit gedrag helpt het risico op implementatie problemen te verminderen en vermindert de belasting van het netwerk dat wordt veroorzaakt door de distributie van inhoud naar clients. De site maakt de software geleidelijk beschikbaar, afhankelijk van de configuratie van elke fase. Elke client in een fase heeft een deadline die relatief is ten opzichte van de tijd dat de software beschikbaar is. Het tijd venster tussen de beschik bare tijd en deadline is hetzelfde voor alle clients in een fase. De standaard waarde van deze instelling is nul, dus de implementatie wordt standaard niet beperkt. Stel de waarde niet hoger dan 30 in.<!--SCCMDocs-pr issue 2767--> 

![Gefaseerde implementatie criteria voor geslaagde instellingen](media/phased-deployment-criteria-for-success.png)

#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Het deadline gedrag bepalen ten opzichte van wanneer de software beschikbaar wordt gesteld  

- De **installatie is zo snel mogelijk vereist**: Stel de deadline in voor installatie op het apparaat zodra het apparaat is gericht.  

- De **installatie is na deze periode vereist**: Stel een deadline in voor de installatie van een bepaald aantal dagen nadat het apparaat is benaderd. Deze waarde is standaard zeven dagen.   


<!--### Examples
Include a timeline diagram
-->



## <a name="automatically-create-a-default-two-phase-deployment"></a><a name="bkmk_auto"></a>Automatisch een standaard implementatie met twee fasen maken

1. Start de wizard gefaseerde implementatie maken in de Configuration Manager-console. Deze actie is afhankelijk van het type software dat u implementeert:  

    - **Toepassing** (alleen in versie 1806 of hoger): Ga naar de **software bibliotheek**, vouw **toepassings beheer**uit en selecteer **toepassingen**. Selecteer een bestaande toepassing en kies vervolgens **gefaseerde implementatie maken** op het lint.  

    - **Software-update** (alleen in versie 1810 of hoger): Ga naar **de software bibliotheek**, vouw **software-updates**uit en selecteer **alle software-updates**. Selecteer een of meer updates en kies vervolgens **gefaseerde implementatie maken** op het lint.  

        Deze actie is beschikbaar voor software-updates van de volgende knoop punten:  
        - Software-updates  
            - **Alle software-updates**  
            - **Software-update groepen**   
        - Windows 10-onderhoud, **alle Windows 10-updates**  
        - Office 365-client beheer, **office 365-updates**  

    - **Taken reeks**: Ga naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer **taken reeksen**. Selecteer een bestaande taken reeks en kies vervolgens **gefaseerde implementatie maken** op het lint.  

2. Geef op de pagina **Algemeen** de gefaseerde implementatie een **naam**, **Beschrijving** (optioneel) en selecteer **automatisch een standaard implementatie met twee fasen maken**.  

3. Selecteer **Bladeren** en kies een doel verzameling voor zowel de **eerste verzameling** als de **tweede verzamelings** velden. Voor een taken reeks en software-updates selecteert u uit apparaten verzamelen. Voor een toepassing selecteert u van gebruikers-of apparaat-verzamelingen. Selecteer **Next**.  

    > [!Important]  
    > Met de wizard gefaseerde implementatie wordt u niet op de hoogte gesteld als een implementatie mogelijk een groot risico is. Zie instellingen voor het [beheren van implementaties met een hoog risico](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) en de notitie wanneer u [een taken reeks implementeert](deploy-a-task-sequence.md)voor meer informatie.  

4. Kies op de pagina **instellingen** één optie voor elk van de plannings instellingen. Zie [Phase Settings](#bkmk_settings)(Engelstalig) voor meer informatie. Selecteer **volgende** als u klaar bent.  

5. Bekijk op de pagina **fasen** de twee fasen die de wizard voor de opgegeven verzamelingen maakt. Selecteer **Next**. Deze instructies beslaan de procedure om automatisch een standaard implementatie met twee fasen te maken. Met de wizard kunt u fasen voor een gefaseerde implementatie toevoegen, verwijderen, opnieuw rangschikken, bewerken of weer geven. Zie [een gefaseerde implementatie met hand matig geconfigureerde fasen maken](#bkmk_manual)voor meer informatie over deze aanvullende acties.  

6. Bevestig uw selecties op het tabblad **samen vatting** en selecteer vervolgens **volgende** om de wizard te volt ooien.  

> [!NOTE]
> Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Zie [name wijzigen voor Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change)voor meer informatie. Mogelijk ziet u nog steeds de oude naam in het Configuration Manager product en de documentatie terwijl de-console wordt bijgewerkt.  

## <a name="create-a-phased-deployment-with-manually-configured-phases"></a><a name="bkmk_manual"></a>Een gefaseerde implementatie met hand matig geconfigureerde fasen maken
<!--1358148--> 

Met ingang van versie 1806 maakt u een gefaseerde implementatie met hand matig geconfigureerde fasen voor een taken reeks. Voeg Maxi maal 10 extra fasen toe op het tabblad **fasen** van de wizard gefaseerde implementatie maken. 

> [!Note]  
> U kunt momenteel niet hand matig fasen maken voor een toepassing. De wizard maakt automatisch twee fasen voor toepassings implementaties.


1. Start de wizard gefaseerde implementatie maken voor een taken reeks of software-updates.  

2. Geef op de pagina **Algemeen** van de wizard gefaseerde implementatie maken de gefaseerde implementatie een **naam**, **Beschrijving** (optioneel) en selecteer **alle fasen hand matig configureren**.  

3. Op de pagina **fasen** van de wizard gefaseerde implementatie maken zijn de volgende acties beschikbaar:  

    - De lijst met implementatie fasen **filteren** . Voer een teken reeks in voor een niet-hoofdletter gevoelige overeenkomst van de volg orde, naam of verzamelings kolommen. 

    - Een nieuwe fase **toevoegen** :  

        1. Geef op de pagina **Algemeen** van de wizard fase toevoegen een **naam** op voor de fase en blader vervolgens naar de doel **fase verzameling**. De aanvullende instellingen op deze pagina zijn hetzelfde als wanneer u een taken reeks of software-updates normaal gesp roken implementeert.  

        2. Configureer op de pagina **fase-instellingen** van de wizard fase toevoegen de plannings instellingen en selecteer **volgende** als u klaar bent. Zie [instellingen](#bkmk_settings)voor meer informatie.   

            > [!Note]  
            > U kunt de instellingen van de fase, het percentage van de **implementatie** of het **aantal apparaten dat is geïmplementeerd** (versie 1902 of hoger), in de eerste fase niet bewerken. Deze instelling is alleen van toepassing op fasen die een eerdere fase hebben.  

        3. De instellingen op de pagina's **gebruikers ervaring** en **distributie punten** van de wizard fase toevoegen zijn hetzelfde als wanneer u een taken reeks of software-updates normaal gesp roken implementeert.  

        4. Controleer de instellingen op de pagina **samen vatting** en voltooi vervolgens de wizard fase toevoegen.  

    - **Bewerken**: met deze actie wordt de venster Eigenschappen van de geselecteerde fase geopend. deze heeft dezelfde tabs als de pagina's van de wizard fase toevoegen.  

    - **Verwijderen**: met deze actie wordt de geselecteerde fase verwijderd.  

       > [!Warning]  
       > Er is geen bevestiging en u kunt deze actie niet ongedaan maken.  

    - **Omhoog of** **omlaag**verplaatsen: de wizard rangschikt de fasen door de stappen toe te voegen. De laatst toegevoegde fase staat in de lijst. Als u de volg orde wilt wijzigen, selecteert u een fase en vervolgens gebruikt u deze knoppen om de locatie van de fase in de lijst te verplaatsen.  

       > [!Important]  
       > Controleer de instellingen van de fase nadat u de volg orde hebt gewijzigd. Zorg ervoor dat de volgende instellingen nog steeds consistent zijn met uw vereisten voor deze gefaseerde implementatie:  
       > 
       > - Criteria voor het slagen van de vorige fase  
       > - Voor waarden voor het starten van deze implementatie fase na een geslaagde uitvoering van de vorige fase   

5. Selecteer **Next**. Controleer de instellingen op de pagina **samen vatting** en voltooi vervolgens de wizard gefaseerde implementatie maken.  


Nadat u een gefaseerde implementatie hebt gemaakt, opent u de eigenschappen ervan om wijzigingen aan te brengen:  

- **Voeg** extra fasen toe aan een bestaande gefaseerde implementatie.  

- Als een fase niet actief is, kunt u deze **bewerken**, **verwijderen**of **verplaatsen** . U kunt deze niet voor een actieve fase verplaatsen.  

- Wanneer een fase actief is, is deze alleen-lezen. U kunt deze niet bewerken, verwijderen of de locatie ervan in de lijst verplaatsen. De enige optie is de eigenschappen van de fase **weer te geven** .  

- Een door de toepassing gefaseerde implementatie is altijd alleen-lezen.  



## <a name="next-steps"></a>Volgende stappen

Gefaseerde implementaties beheren en bewaken:
- [Toepassing](manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)
- [Software-update](manage-monitor-phased-deployments.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Takenreeks](manage-monitor-phased-deployments.md)  


---
title: Fouten opsporen in een takenreeks
titleSuffix: Configuration Manager
description: Gebruik het hulp programma voor het opsporen van taken reeksen om een taken reeks op te lossen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99ed8232a74b038b9b1cde4af257353252454c2b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125148"
---
# <a name="debug-a-task-sequence"></a>Fouten opsporen in een takenreeks

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3612274-->

Vanaf versie 1906 is het fout opsporingsprogramma voor taken reeksen een nieuw hulp programma voor probleem oplossing. U implementeert een taken reeks in foutopsporingsmodus naar een kleine verzameling. Zo kunt u de taken reeks op een gecontroleerde manier door lopen om het oplossen van problemen en onderzoek te helpen. Het fout opsporingsprogramma wordt momenteel uitgevoerd op hetzelfde apparaat als de taken reeks engine, maar dit is geen externe fout opsporing.

> [!Note]  
> In deze versie van Configuration Manager is het fout opsporingsprogramma voor taken reeksen een functie van de voorlopige versie. Zie [functies van voorlopige versies](../../core/servers/manage/pre-release-features.md)om deze functie in te scha kelen.  


## <a name="prerequisites"></a>Vereisten

- De Configuration Manager-client op het doel apparaat bijwerken

- Meld u aan bij het doel apparaat als een gebruiker in de lokale groep **Administrators** . Het fout opsporingsprogramma wordt alleen uitgevoerd voor beheerders.

- Werk de opstart installatie kopie die is gekoppeld aan de taken reeks bij om er zeker van te zijn dat deze de meest recente client versie heeft


## <a name="start-the-tool"></a>Het hulp programma starten

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer **taken reeksen**.

1. Selecteer een taken reeks. Selecteer in de implementatie groep van het lint **fout opsporing**.

    > [!Tip]  
    > U kunt ook de variabele **TSDebugMode** instellen op `TRUE` een verzameling of computer object waarop de taken reeks wordt geïmplementeerd. Op elk apparaat waarop deze variabele is ingesteld, wordt elke taken reeks geïmplementeerd in de foutopsporingsmodus.

1. Maak een implementatie voor fout opsporing. De implementatie-instellingen zijn hetzelfde als een normale implementatie van een taken reeks. Zie [Een takenreeks implementeren](deploy-a-task-sequence.md#process)voor meer informatie.

    > [!Note]  
    > U kunt alleen een kleine verzameling selecteren voor een debug-implementatie. Er worden alleen verzamelingen weer gegeven met tien of minder leden.

Vanaf versie 1910 gebruikt u de nieuwe taken reeks variabele **TSDebugOnError** om automatisch het fout opsporingsprogramma te starten als er een fout wordt geretourneerd door de taken reeks.<!-- 5012536 --> Zie [taken reeks variabelen-TSDebugOnError](../understand/task-sequence-variables.md#TSDebugOnError)voor meer informatie.

## <a name="use-the-tool"></a>Het hulp programma gebruiken

Wanneer de taken reeks op het apparaat wordt uitgevoerd, wordt het venster fout opsporing voor taken reeksen geopend zoals in de volgende scherm afbeelding:

![Scherm afbeelding van het fout opsporingsprogramma voor taken reeksen](media/3612274-tsdebug.png)

Het fout opsporingsprogramma bevat de volgende besturings elementen:

- **Stap**: Voer vanaf de *huidige* positie alleen de volgende stap in de taken reeks uit.  

    > [!Note]  
    > Als de taken reeks zich in de foutopsporingsmodus bevindt en een stap een fatale fout retourneert, mislukt de taken reeks normaal. Dit gedrag geeft u de mogelijkheid om een stap opnieuw uit te voeren nadat u een externe wijziging hebt aangebracht.

- **Uitvoeren**: vanaf de *huidige* positie voert u de taken reeks normaal tot het einde, het volgende *einde* punt of als een stap mislukt. Voordat u deze actie gebruikt, moet u een wille keurige afbreek punt instellen met de actie voor het instellen van een **afbreek** bewerking.

- **Set current**: Selecteer een stap in het fout opsporingsprogramma en selecteer vervolgens **huidige instellen**. Met deze actie wordt de *huidige* verwijzing naar die stap verplaatst. Met deze actie kunt u stappen overs Laan of achterwaarts verplaatsen.  

    > [!Warning]  
    > Het fout opsporingsprogramma beschouwt niet het type stap wanneer u de huidige positie in de reeks wijzigt. In sommige stappen kunnen taken reeks variabelen worden ingesteld die vereist zijn voor de evaluatie van voor waarden door latere stappen. Als de bewerking niet in orde is, kunnen bepaalde stappen mislukken of aanzienlijke schade aan een apparaat veroorzaken. Gebruik deze optie voor uw eigen risico.  

- **Stel breek**punt in: Selecteer een stap in het fout opsporingsprogramma en selecteer vervolgens **kraken instellen**. Met deze actie wordt een *onderbreek* punt toegevoegd in het fout opsporingsprogramma. Wanneer u de taken reeks **uitvoert** , stopt deze bij een *onderbreking*.  

    - Voordat u de actie **uitvoeren** gebruikt, stelt u breek punten in.

    - Vanaf versie 1910, als u een breek punt in het fout opsporingsprogramma maakt en vervolgens de computer opnieuw opstart, worden de verbreken na het opnieuw opstarten door de taken reeks bewaard.<!-- 5012509 -->

    - In versie 1906 worden breek punten niet opgeslagen nadat de computer opnieuw is opgestart, zoals bij de stap [computer opnieuw opstarten](../understand/task-sequence-steps.md#BKMK_RestartComputer) . Als u bijvoorbeeld het fout opsporingsprogramma start vanuit software Center voor een taken reeks voor het uitvoeren van een installatie kopie, stelt u geen onderbrekingen in de Windows PE-fase in. Wanneer de computer opnieuw wordt opgestart in Windows PE, wordt de taken reeks onderbroken door het fout opsporingsprogramma, zodat u onderbrekingen kunt instellen.

- **Alle einde markeringen wissen**: Verwijder alle onderbrekings punten.

- **Logboek bestand**: Hiermee opent u het huidige logboek bestand van de taken reeks, **bestand smsts. log**, met [CMTrace](../../core/support/cmtrace.md). U kunt logboek vermeldingen zien wanneer de taken reeks Engine wacht op het fout opsporingsprogramma.

- **Cmd prompt**: in Windows PE wordt een opdracht prompt geopend.

- **Annuleren**: Sluit het fout opsporingsprogramma en de taken reeks mislukt.

- **Afsluiten**: de debugger loskoppelen en sluiten, maar de taken reeks blijft normaal uitgevoerd.

In het venster **taken reeks variabelen** worden de huidige waarden weer gegeven voor alle variabelen in de taken reeks omgeving. Zie [taken reeks variabelen](../understand/task-sequence-variables.md)voor meer informatie. Als u de stap [taken reeks variabele instellen](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) gebruikt met de optie om **deze waarde niet weer te geven**, wordt de waarde van de variabele niet weer gegeven door het fout opsporingsprogramma. U kunt de variabelen waarden in het fout opsporingsprogramma niet bewerken.

> [!Note]
> Sommige taken reeks variabelen zijn alleen bedoeld voor intern gebruik en worden niet vermeld in de referentie documentatie.

Het fout opsporingsprogramma voor taken reeksen blijft actief na een stap voor het [opnieuw opstarten](../understand/task-sequence-steps.md#BKMK_RestartComputer) van de computer, maar u moet alle breek punten opnieuw maken. Hoewel de taken reeks dit mogelijk niet vereist, omdat het fout opsporingsprogramma gebruikers interactie vereist, moet u zich aanmelden bij Windows om door te gaan. Als u zich niet aanmeldt na een uur om de fout opsporing voort te zetten, mislukt de taken reeks.

Er wordt ook een onderliggende taken reeks uitgevoerd met de stap [taken reeks uitvoeren](../understand/task-sequence-steps.md#child-task-sequence) . In het venster fout opsporing worden de stappen van de onderliggende taken reeks weer gegeven samen met de hoofd taken reeks.


## <a name="known-issues"></a>Bekende problemen

Als u de implementatie van een normale implementatie en het opsporen van fouten op hetzelfde apparaat bedoelt via meerdere implementaties, wordt het fout opsporingsprogramma voor de taken reeks mogelijk niet gestart.


## <a name="see-also"></a>Zie ook

- [Stappen voor takenreeksen](../understand/task-sequence-steps.md)
- [Takenreeksvariabelen](../understand/task-sequence-variables.md)
- [Takenreeksvariabelen gebruiken](../understand/using-task-sequence-variables.md)
- [Een takenreeks implementeren](deploy-a-task-sequence.md)

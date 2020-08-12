---
title: Gebruikers status vastleggen en herstellen
titleSuffix: Configuration Manager
description: Gebruik Configuration Manager taken reeksen om de gegevens van de gebruikers status vast te leggen en te herstellen in implementatie scenario's voor besturings systemen.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a1f11c46689b213b795c0d71221728f916a68bb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125488"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Een taken reeks maken voor het vastleggen en herstellen van de gebruikers status in Configuration Manager

 *Van toepassing op: Configuration Manager (huidige vertakking)*

 Gebruik Configuration Manager taken reeksen om de gegevens van de gebruikers status vast te leggen en te herstellen in implementatie scenario's voor besturings systemen. In deze scenario's wilt u de gebruikers status van het huidige besturings systeem behouden. Afhankelijk van het type takenreeks dat u wilt maken, worden de stappen voor het vastleggen en terugzetten automatisch toegevoegd als onderdeel van de takenreeks. In andere situaties moet u de stappen voor het vastleggen en terugzetten misschien handmatig toevoegen. In dit artikel worden de stappen beschreven die u aan een bestaande taken reeks moet toevoegen om gebruikers status gegevens vast te leggen en te herstellen.  



## <a name="task-sequence-steps"></a>Stappen voor takenreeksen  

Als u de gebruikers status wilt vastleggen en herstellen, voegt u de volgende stappen toe aan de taken reeks:  

- [Status opslag opvragen](../understand/task-sequence-steps.md#BKMK_RequestStateStore): als u de gebruikers status opslaat op het status migratie punt, hebt u deze stap nodig.  

- [Gebruikers status vastleggen](../understand/task-sequence-steps.md#BKMK_CaptureUserState): deze stap legt de gebruikers status gegevens vast. Vervolgens worden de gegevens opgeslagen op het status migratie punt of de lokale schijf met behulp van hardlinks.  

- [Gebruikersstatus herstellen](../understand/task-sequence-steps.md#BKMK_RestoreUserState): deze stap herstelt de gebruikersstatusgegevens op de doelcomputer. Het kan de gegevens ophalen van een status migratie punt of als hardlinked op de lokale schijf.  

- [Status opslag vrijgeven](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore): als u de gebruikers status opslaat op het status migratie punt, hebt u deze stap nodig. Met deze stap worden de gegevens van het status migratie punt verwijderd.  


 Gebruik de volgende procedures om de taken reeks stappen toe te voegen die nodig zijn om de gebruikers status vast te leggen en te herstellen. Raadpleeg taken [reeksen beheren om taken te automatiseren](manage-task-sequences-to-automate-tasks.md)voor meer informatie over het maken van een taken reeks.  



## <a name="capture-the-user-state"></a>De gebruikers status vastleggen  

 Gebruik de volgende stappen om taken reeks stappen toe te voegen om de gebruikers status vast te leggen:

1.  Selecteer een takenreeks uit de lijst **Takenreeks** en klik vervolgens op **Bewerken**.  

2.  Als u een status migratie punt gebruikt om de gebruikers status op te slaan, voegt u de stap **status opslag opvragen** toe aan de taken reeks. Klik in de **taken reeks editor**op **toevoegen**. Wijs **gebruikers status**aan en klik vervolgens op **status opslag opvragen**. Configureer de eigenschappen en opties voor deze stap en klik vervolgens op **Toep assen**. Zie [status opslag aanvragen](../understand/task-sequence-steps.md#BKMK_RequestStateStore)voor meer informatie over de beschik bare instellingen.  

3.  Voeg de stap **Gebruikersstatus vastleggen** toe aan de takenreeks. Klik in de **taken reeks editor**op **toevoegen**. Wijs **gebruikers status**aan en klik vervolgens op **gebruikers status vastleggen**. Configureer de eigenschappen en opties voor deze stap en klik vervolgens op **Toep assen**. Zie [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState)voor meer informatie over de beschik bare instellingen.  

    > [!IMPORTANT]  
    >  Wanneer u deze stap aan uw taken reeks toevoegt, stelt u ook de taken reeks variabele **osdstatestorepath in** in om op te geven waar de gebruikers status gegevens moeten worden opgeslagen. Als u de gebruikers status lokaal opslaat, dient u geen hoofdmap op te geven, aangezien dat ertoe kan leiden dat de taken reeks mislukt. Gebruik altijd een map of submap wanneer u de gebruikersgegevens lokaal opslaat. Zie [taken reeks variabelen](../understand/task-sequence-variables.md#OSDStateStorePath)voor meer informatie over deze variabele.  

4.  Als u een status migratie punt gebruikt, voegt u de stap **status opslag vrijgeven** toe aan de taken reeks. Klik in de **taken reeks editor**op **toevoegen**. Wijs **gebruikers status**aan en klik vervolgens op **status opslag vrijgeven**. Configureer de eigenschappen en opties voor deze stap en klik vervolgens op **Toep assen**. Zie [release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)voor meer informatie over de beschik bare instellingen.  

    > [!IMPORTANT]  
    >  De taken reeks actie die wordt uitgevoerd voordat de stap **status opslag vrijgeven** moet slagen voordat de stap **status opslag vrijgeven** wordt gestart.  


 Implementeer deze takenreeks om de gebruikersstatus op een doelcomputer vast te leggen. Zie [Deploy a task sequence](deploy-a-task-sequence.md)voor meer informatie over het implementeren van takenreeksen.  



## <a name="restore-the-user-state"></a>De gebruikers status herstellen  

 Als u taken reeks stappen wilt toevoegen om de gebruikers status te herstellen, gebruikt u de volgende stappen:

1. Selecteer een takenreeks uit de lijst **Takenreeks** en klik vervolgens op **Bewerken**.  

2. Voeg de stap **Restore User State** toe aan de takenreeks. Klik in de **taken reeks editor**op **toevoegen**. Wijs **gebruikers status**aan en klik vervolgens op **gebruikers status herstellen**. Deze stap brengt zo nodig een verbinding tot stand met het status migratie punt. Configureer de eigenschappen en opties voor deze stap en klik vervolgens op **Toep assen**. Zie [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState)voor meer informatie over de beschik bare instellingen.  

   > [!Important]  
   >  Wanneer u de stap [gebruikers status vastleggen](../understand/task-sequence-steps.md#BKMK_CaptureUserState) gebruikt met de optie voor **het vastleggen van alle gebruikers profielen met standaard opties**, moet u de instelling **gebruikers profielen voor lokale computers herstellen** selecteren in de stap **gebruikers status herstellen** . Anders mislukt de taken reeks.  

   > [!Note]  
   > Als u de gebruikers status opslaat met behulp van lokale hardlinks en de herstel bewerking is mislukt, kunt u hand matig de hardlinks verwijderen die zijn gemaakt om de gegevens op te slaan. Met de taken reeks kan het hulp programma USMTUtils worden uitgevoerd om deze actie te automatiseren met de stap [opdracht regel uitvoeren](../understand/task-sequence-steps.md#BKMK_RunCommandLine) . Als u USMTUtils gebruikt om de hard link te verwijderen, voegt u een stap [computer opnieuw opstarten](../understand/task-sequence-steps.md#BKMK_RestartComputer) toe nadat u USMTUtils hebt uitgevoerd.  

3. Als u een status migratie punt gebruikt om de gebruikers status op te slaan, voegt u de stap **status opslag vrijgeven** toe aan de taken reeks. Klik in de **taken reeks editor**op **toevoegen**. Wijs **gebruikers status**aan en klik vervolgens op **status opslag vrijgeven**. Configureer de eigenschappen en opties voor deze stap en klik vervolgens op **Toep assen**. Zie [release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)voor meer informatie over de beschik bare instellingen.  

   > [!IMPORTANT]  
   >  De taken reeks actie die wordt uitgevoerd voordat de stap **status opslag vrijgeven** moet slagen voordat de stap **status opslag vrijgeven** wordt gestart.  


 Implementeer deze takenreeks om de gebruikersstatus op de doelcomputer te herstellen. Zie [Deploy a task sequence](deploy-a-task-sequence.md)voor meer informatie over het implementeren van takenreeksen.  



## <a name="next-steps"></a>Volgende stappen

[De takenreeksimplementatie controleren](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)

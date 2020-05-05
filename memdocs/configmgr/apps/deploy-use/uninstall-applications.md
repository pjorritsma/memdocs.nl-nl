---
title: Toepassingen verwijderen
titleSuffix: Configuration Manager
description: Een toepassing verwijderen met behulp van Configuration Manager
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d9b5152c094ecc1470f748c57f2831cfdd66474
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075843"
---
# <a name="uninstall-applications-with-configuration-manager"></a>Toepassingen verwijderen met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*


Voer de volgende acties uit om een toepassing die u eerder hebt geïmplementeerd, te verwijderen.

-   Geef de opdracht regel op voor het verwijderen van de implementatie type-inhoud op de pagina **inhoud** van de wizard implementatie type maken.  

-   Implementeer de toepassing met behulp van een implementatieactie **Verwijderen**.  

> [!IMPORTANT]  
> Sommige toepassingtypen bieden geen ondersteuning voor verwijdering.  

 In deze lijst vindt u meer informatie over de werking van het verwijderen van toepassingen:  

-   Wanneer u een Configuration Manager-toepassing (Configuration Manager) verwijdert, worden alle afhankelijke toepassingen niet automatisch verwijderd.  

-   Als u een toepassing implementeert die gebruikmaakt van een actie van het **verwijderen** van een gebruiker en de toepassing is geïnstalleerd voor alle gebruikers van de computer, mislukt de verwijdering mogelijk als het account van de gebruiker niet gemachtigd is om de toepassing te verwijderen.  

-   Als u een gebruiker of een apparaat verwijdert uit een verzameling waarin een toepassing is geïmplementeerd, wordt de toepassing niet automatisch van het apparaat verwijderd.  

-   Bij een implementatie met het implementatiedoel **Verwijderen** , worden de regels voor vereisten niet gecontroleerd. Als de toepassing wordt geïnstalleerd op de computer waarop de implementatie wordt uitgevoerd, wordt deze verwijderd.  

> [!IMPORTANT]  
> Als u de toepassing wilt implementeren met de actie verwijderen, moet u eerst bestaande toepassings implementaties, gesimuleerde implementaties of taken reeks implementaties die deze toepassing bevatten, verwijderen. 

 Zie [toepassingen maken](../../apps/deploy-use/create-applications.md)voor meer informatie over het maken van een implementatie type.  

 Zie [toepassingen implementeren](../../apps/deploy-use/deploy-applications.md)voor meer informatie over het implementeren van een toepassing.  

## <a name="uninstall-an-application"></a>Een toepassing verwijderen  

1.  Gebruik een van de volgende methoden om het implementatietype van de toepassing te configureren met de opdrachtregel voor verwijdering:  

    -   Selecteer op de pagina **Algemeen** van de wizard implementatie maken de optie **automatisch informatie identificeren over dit implementatie type vanuit installatie bestanden**. Als de informatie beschikbaar is in de installatiebestanden, wordt de opdrachtregel voor verwijdering automatisch toegevoegd aan de eigenschappen van het implementatietype.  

    -   Geef op de pagina **inhoud** van de wizard implementatie type maken in het veld **programma voor verwijderen** de opdracht regel op om de toepassing te verwijderen.  

        > [!NOTE]  
        >  De pagina **inhoud** wordt alleen weer gegeven als u de optie **hand matig de implementatie type-informatie opgeven** op de pagina **Algemeen** van de wizard implementatie type maken.  

    -   Geef op het tabblad **Program ma's** in het ** <dialoog venster *naam van implementatie type*> eigenschappen** de opdracht regel op om de toepassing te verwijderen in het veld **programma verwijderen** .  

2.  Implementeer de toepassing en selecteer vervolgens de implementatie actie **verwijderen** op de pagina **implementatie-instellingen** van de wizard software implementeren.  

    > [!NOTE]  
    >  Wanneer u de implementatieactie **Verwijderen**selecteert, wordt het implementatiedoel automatisch geconfigureerd als **Vereist**.  

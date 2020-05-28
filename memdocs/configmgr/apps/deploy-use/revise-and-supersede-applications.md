---
title: Toepassingen herzien en vervangen
titleSuffix: Configuration Manager
description: Meer informatie over het werken met Configuration Manager toepassings versies en het vervangen van toepassingen.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 6afed00b8207edb338b2a6dc62e083a5267fa47e
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343130"
---
# <a name="revise-and-supersede-applications-in-configuration-manager"></a>Toepassingen herzien en vervangen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit onderwerp leert u hoe u kunt werken met Configuration Manager-toepassings versies en hoe u toepassingen vervangt door een nieuwe versie.  

##  <a name="application-revisions"></a> Revisies van toepassing  
 Wanneer u wijzigingen aanbrengt in een toepassing of een implementatie type dat is opgenomen in een toepassing, wordt in Configuration Manager een nieuwe revisie van de toepassing gemaakt. U kunt de geschiedenis van elke toepassingsrevisie weergeven. Daarnaast kunt u de eigenschappen weergeven, een eerdere revisie van een toepassing herstellen of een oude revisie verwijderen.  

### <a name="to-display-an-application-revision-history"></a>De revisiegeschiedenis voor een toepassing weergeven  

1.  Kies in de Configuration Manager-console **software bibliotheek**toepassingen voor  >  **toepassings beheer**  >  **Applications**en kies vervolgens de gewenste toepassing.  

3.  Klik op het tabblad **Start** in de groep **toepassing** op **overzicht van wijzigingen** om het dialoog venster **overzicht van toepassings revisies** te openen.  

### <a name="to-view-an-application-revision"></a>Een toepassingsrevisie weergeven  

1.  Selecteer een toepassings revisie in het dialoog venster **overzicht van toepassings revisies** en kies vervolgens **weer gave**.  

2.  In het dialoogvenster **Eigenschappen** controleert u de eigenschappen van de geselecteerde toepassing.  

    > [!NOTE]  
    >  De toepassingseigenschappen die worden weergegeven, zijn alleen-lezen.  

3.  Sluit het dialoogvenster **Eigenschappen** .  

### <a name="to-restore-an-application-revision"></a>Een toepassingsrevisie herstellen  

1.  Selecteer een toepassings revisie in het dialoog venster **overzicht van toepassings revisies** en kies vervolgens **herstellen**.  

2.  Kies in het dialoog venster **Restore revisies bevestigen** **Ja** om de geselecteerde toepassings revisie te herstellen.  

### <a name="to-delete-an-application-revision"></a>Een toepassingsrevisie verwijderen  

1.  Selecteer een toepassings revisie in het dialoog venster **overzicht van toepassings revisies** en kies vervolgens **verwijderen**.  

2.  Klik in het dialoog venster **toepassings revisie verwijderen** op **Ja**.  

> [!IMPORTANT]  
>  U kunt de huidige toepassings revisie alleen verwijderen als de toepassing buiten gebruik is gesteld en geen verwijzingen bevat.  

##  <a name="application-supersedence"></a> Vervanging van toepassing  
 Met toepassings beheer in Configuration Manager kunt u bestaande toepassingen bijwerken of vervangen door gebruik te maken van een vervangings relatie. Wanneer u een toepassing vervangt, kunt u een nieuw implementatie type opgeven om het implementatie type van de vervangen toepassing te vervangen en ook bepalen of u de vervangen toepassing wilt upgraden of verwijderen voordat de vervangende toepassing wordt geïnstalleerd. Over het algemeen is het raadzaam om vervangings ketens te beperken tot vijf niveaus diep.
 
> [!IMPORTANT]  
>  Wanneer u de optie voor het verwijderen van het vervangen implementatietype selecteert, kunt u dit implementatietype niet vervangen door een implementatietype dat is toegepast op een ander type verzameling.  Als u de optie voor het verwijderen van het vervangen implementatietype hebt geselecteerd, kunt u een implementatietype dat op een apparaatverzameling is geïmplementeerd bijvoorbeeld niet vervangen door een implementatietype dat op een gebruikersverzameling is geïmplementeerd.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Bepalen of u een toepassing wilt bijwerken of vervangen  
 In het dialoogvenster met toepassingseigenschappen kunt u in het dialoogvenster **Geef vervangingsrelatie op** aangeven of u een app wilt vervangen of bijwerken. Het type vervanging is afhankelijk van of de optie **Verwijderen** is ingeschakeld in dit dialoogvenster:  

-   Als u wilt bijwerken naar een nieuwere versie van dezelfde toepassing (met dezelfde toepassings-ID), moet u de **installatie** **niet** controleren.  

-   Als u een andere toepassing wilt gebruiken (met een andere toepassings-id), schakelt u **Verwijderen**in. U moet de vervangen versie van de toepassing verwijderen.  

### <a name="supersede-dependent-applications"></a>Afhankelijke toepassingen vervangen  
 In dit voor beeld verwijst **hoofd toepassing** naar de app die u implementeert die de afhankelijkheden heeft.  

 U kunt een vervangingsrelatie maken die de afhankelijke toepassing bijwerkt naar een nieuwe versie.  

1. Zorg ervoor dat de nieuwe afhankelijke toepassing en de oorspronkelijke afhankelijke toepassing zich in dezelfde afhankelijkheidsgroep bevinden als de hoofdtoepassing.  

2. Maak een vervangingsrelatie waarbij de oorspronkelijke afhankelijke toepassing wordt vervangen door de nieuwe afhankelijke toepassing.  

   Tijdens nieuwe installaties van de hoofd toepassing wordt de nieuwe afhankelijke toepassing geïnstalleerd. Bestaande installaties van de hoofd toepassing worden bijgewerkt met de nieuwe afhankelijke toepassing.  

   Het eind resultaat is dat alle implementaties van de hoofd toepassing de nieuwe afhankelijke toepassing gebruiken.  

### <a name="further-considerations"></a>Verdere overwegingen  

-   U kunt meerdere vervangingsrelaties opgeven voor afhankelijke toepassingen. De hoogste afhankelijke toepassing in de vervangingsketen wordt geïnstalleerd.  

-   Afhankelijke toepassingen moeten worden geïmplementeerd op het apparaat waarop de hoofd toepassing is geïnstalleerd, anders wordt de afhankelijke toepassing niet geïnstalleerd.  

-   Als u meerdere afhankelijkheden hebt, bepaalt de afhankelijkheidsvolgorde welke versie van de afhankelijke toepassing voor nieuwe installaties van de hoofdtoepassing wordt geïnstalleerd.  

### <a name="to-specify-a-supersedence-relationship"></a>Een vervangingsrelatie opgeven  

1.  Kies in de Configuration Manager-console **software bibliotheek**toepassingen voor  >  **toepassings beheer**  >  **Applications**en kies vervolgens de toepassing die een andere toepassing vervangt.  

3.  Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen** om het dialoog venster **Eigenschappen** van toepassings naam te openen.  

4.  Kies op het tabblad **vervanging** van het dialoog venster **Eigenschappen** van *<\> toepassings naam* de optie **toevoegen**.  

5.  Klik in het dialoogvenster **Geef vervangingsrelatie op** op **Bladeren**.  

6.  Kies in het dialoog venster **toepassing kiezen** de toepassing die u wilt vervangen en klik vervolgens op **OK**.  

7.  Selecteer in het dialoog venster **Geef vervangings relatie** op het implementatie type dat het implementatie type van de vervangen toepassing vervangt.  

    > [!NOTE]  
    >  Standaard wordt het implementatie type van de vervangen toepassing niet verwijderd door het nieuwe implementatie type. Dit scenario wordt doorgaans gebruikt om een upgrade voor een bestaande toepassing te implementeren. Selecteer **Verwijderen** als u het bestaande implementatietype wilt verwijderen voordat het nieuwe implementatietype wordt geïnstalleerd. Als u een toepassing wilt upgraden, kunt u dit het beste eerst testen in een testomgeving.  

8.  Klik op **OK** om het dialoog venster **Geef vervangings relatie** op te sluiten.  

9. Klik op **OK** om het dialoog venster **Eigenschappen** van *<toepassings \> naam* te sluiten.  

### <a name="to-display-applications-that-supersede-the-current-application"></a>Toepassingen weergeven die de huidige toepassing vervangen  

1.  Kies in de Configuration Manager-console de optie **software bibliotheek**.  

2.  Vouw in de werk ruimte **software bibliotheek** het knoop punt **toepassings beheer**uit, kies **toepassingen**en kies vervolgens de gewenste toepassing.  

3.  Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen** om het dialoog venster **Eigenschappen** van *<\> toepassing* te openen.  

4.  Kies op het tabblad **verwijzingen** van het dialoog venster **Eigenschappen** van *<toepassings \> naam* de optie **toepassingen die deze toepassing vervangen** in de vervolg keuzelijst **Relatie type** .  

5.  Bekijk de lijst met toepassingen die de geselecteerde toepassing vervangen en klik vervolgens op **OK** om het dialoog venster **Eigenschappen** van *<\> toepassings naam* te sluiten.  

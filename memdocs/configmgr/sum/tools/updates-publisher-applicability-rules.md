---
title: Toepasselijkheidsregels
titleSuffix: Configuration Manager
description: Toepasings regels voor System Center Updates Publisher beheren
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53a3aabfe65449723bdb6076486128b76a1a830c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078427"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Regels voor toepasselijkheid beheren in updates Publisher

*Van toepassing op: System Center Updates Publisher*

Met updates Publisher definiëren de regels voor toepasselijkheid vereisten waaraan moet worden voldaan voordat een apparaat een update kan installeren. De regels worden ook gebruikt om te bepalen of er een update is geïnstalleerd op de computer. Een regel voor toepas baarheid die complex is met meerdere onderdelen wordt een regelset genoemd.

Update bundels gebruiken geen toepas baarheids regels.

## <a name="overview-of-applicability-rules"></a>Overzicht van regels voor toepasselijkheid
U beheert toepas baarheids regels vanuit de **werk ruimte regels**. Wanneer u een regel maakt, kunt u een of meer voor waarden opgeven. Wanneer er meerdere voor waarden zijn opgegeven, kunt u relaties tussen de voor waarden configureren zodat ze opeenvolgend worden geëvalueerd of worden gecombineerd in logische **en** of **or** -instructies.

In het volgende voor beeld ziet u een regel reeks die drie regels bevat. Met de eerste regel wordt gecontroleerd of het bestand *Mijnbestand* bestaat en de tweede en derde regel controleren of de taal van het Windows-besturings systeem Engels of Japans is.

``` Example
And  
  File '\[PROGRAM\_FILES\] \\Microsoft\\MyFile' exists  
  Or  
    Windows Language is English
    Windows Language is Japanese
```

Voor alle updates is ten minste één toepas baarheids regel vereist. Voor updates die u importeert, zijn al toepasselijkheid regels toegepast en wanneer u uw eigen updates maakt, moet u er een of meer regels aan toevoegen. U kunt de regels voor elke update in updates Publisher wijzigen en uitvouwen.

Als u de regels die u hebt gemaakt, wilt weer geven, selecteert u in de **werk ruimte regels**een regel in de lijst **Mijn opgeslagen regels** . De afzonderlijke voor waarden en logische bewerkingen voor die regel worden weer gegeven in het deel venster **regels toepasselijkheid** van de-console. Regels voor updates die u importeert, kunnen alleen worden weer gegeven en gewijzigd wanneer u die update bewerkt.

U kunt op twee locaties regels maken in updates Publisher:

-   In de **werk ruimte regels** maakt en **slaat** u regel sets op die u later kunt gebruiken. Wanneer u een update bewerkt of maakt, kunt u **opgeslagen regel** als het **regel type**selecteren en vervolgens in een lijst met uw vooraf gemaakte regel sets selecteren.

-   U kunt ook nieuwe regels maken op het moment dat u een update maakt of bewerkt. De regels die u op deze manier maakt, worden niet opgeslagen voor toekomstig gebruik.

## <a name="create-applicability-rule"></a>Regel voor toepas baarheid maken
De volgende informatie is vergelijkbaar met hoe u regels maakt in de [wizard Update maken](create-updates-with-updates-publisher.md#use-the-create-update-wizard). Maar in tegens telling tot de wizard hebt u de optie om uw regel sets op te slaan voor toekomstig gebruik.

1. Kies in de **werk ruimte regels**de optie **maken** om de wizard **regel maken** te openen.

2. Geef een naam op voor de regel en klik vervolgens ![op nieuwe](media/newrule.png)regel. Hiermee opent u de pagina **toepasselijkheid regel** waar u regels kunt configureren.

3. Selecteer bij **regel type** een van de volgende. De opties die u moet configureren, zijn afhankelijk van elk type:

   - **Bestand** : gebruik deze regel om te vereisen dat een apparaat een bestand heeft met eigenschappen die voldoen aan een of meer criteria die u opgeeft voordat deze update kan worden toegepast.

   - **REGI ster –** Gebruik dit type om register Details op te geven die aanwezig moeten zijn voordat een apparaat in aanmerking komt voor het installeren van deze update.

   - **Systeem:** Deze regel gebruikt systeem gegevens om de toepas baarheid te bepalen. U kunt kiezen tussen het definiëren van een Windows-versie, een Windows-taal, een processor architectuur of het opgeven van een WMI-query voor het identificeren van het besturings systeem van het apparaat.

   - **Windows Installer –** Gebruik dit regel type om toepas baarheid te bepalen op basis van een geïnstalleerd. MSI-of Windows Installer-patch (. MSP). U kunt ook bepalen of specifieke onderdelen of onderdelen worden geïnstalleerd als onderdeel van de vereiste.

     > [!IMPORTANT]   
     > In beheerde deices kan de Windows Update-agent geen Windows-installatie pakketten detecteren die per gebruiker zijn geïnstalleerd. Wanneer u dit regel type gebruikt, configureert u aanvullende regels voor toepasselijkheid, zoals bestands versies of register sleutel waarden, zodat het Windows Installer-pakket correct kan worden gedetecteerd, ongeacht de basis van een gebruiker of per systeem.

   - **Opgeslagen regel –** Met deze optie kunt u regels vinden en gebruiken die u eerder hebt geconfigureerd en opgeslagen.

4. Ga verder met het toevoegen en configureren van aanvullende regels naar wens.

5. Gebruik de knoppen logische bewerking om verschillende regels te rangschikken en groeperen om complexere controles voor vereisten te maken.

6. Wanneer de regel is ingesteld, klikt u op **OK** om deze op te slaan. De regel instellingen worden nu weer gegeven in de lijst **Mijn opgeslagen regels** .

## <a name="edit-applicability-rule-sets"></a>Regel sets voor toepas baarheid bewerken
Als u een toepas baarheids regel wilt bewerken, selecteert u in de **werk ruimte regels** een regel die is opgeslagen in de lijst **Mijn opgeslagen regels** en kiest u vervolgens **bewerken** in het lint. Hiermee opent u de wizard **regel bewerken** .

Met de wizard **regel bewerken** worden de huidige regels voor de regel instellingen weer gegeven. U kunt regels op dezelfde manier bewerken als met de wizard **regel maken** om nieuwe regels te maken. U kunt deze wizard gebruiken om de naam van de regelset, regels verwijderen, regels en relaties opnieuw te rangschikken of nieuwe regels toe te voegen.

Nadat u wijzigingen hebt aangebracht, klikt u op **OK** om de wijzigingen op te slaan en de wizard te sluiten.

Zie voor meer informatie over het gebruik van de wizard regel **stap 7**, de pagina toepas baarheid, van de [wizard Update maken](create-updates-with-updates-publisher.md#use-the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Regels voor toepasselijkheid verwijderen
Als u een opgeslagen toepas baarheids regel wilt verwijderen, selecteert u in de **werk ruimte regels** de regel of regelset in de lijst **Mijn opgeslagen regels** en kiest u vervolgens **verwijderen** in het lint. Hiermee verwijdert u de opgeslagen regel of regelset van updates Publisher.

Als u een regel uit een specifieke update wilt verwijderen, moet u [de update bewerken](manage-updates-with-updates-publisher.md#edit-updates-and-bundles).

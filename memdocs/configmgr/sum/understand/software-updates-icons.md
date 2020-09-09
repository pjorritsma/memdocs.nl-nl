---
title: Gebruikte pictogrammen voor software-updates
titleSuffix: Configuration Manager
description: De Configuration Manager-console bevat pictogrammen die een status voor de gesynchroniseerde update of software-update groep aangeven.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0ca0509893ecadc4c54d06ca98c18531959fb941
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608411"
---
# <a name="icons-used-for-software-updates-in-configuration-manager"></a>Pictogrammen die worden gebruikt voor software-updates in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gesynchroniseerde software-updates worden weer gegeven in de Configuration Manager-console en de eerste kolom voor elke software-update bevat een pictogram dat een specifieke status aangeeft. Software-updategroepen worden ook weergegeven met een pictogram dat informatie verschaft over de status van de software-updates in de groep. Deze sectie bevat informatie over de software-updatepictogrammen en de betekenis van elk pictogram.  

## <a name="icons-for-software-updates"></a>Pictogrammen voor software-updates  
 Gesynchroniseerde software-updates worden aangeduid met een van de volgende pictogrammen.  

### <a name="normal-icon"></a>Pictogram Normaal  
 ![Pictogram normaal](../media/Normal.jpg) Het pictogram met de groene pijl duidt op een normale software-update.  

 **Beschrijving:**  

 Normale software-updates zijn gesynchroniseerd en zijn beschikbaar voor software-implementatie.  

 **Operationele problemen:**  

 Er zijn geen operationele problemen.  

### <a name="expired-icon"></a>Pictogram Verlopen  
 ![Pictogram verlopen ](../media/Expired.jpg) het pictogram met de zwarte X duidt op een verlopen software-update. U kunt verlopen software-updates ook identificeren aan de hand van de kolom **verlopen** voor de software-update wanneer deze wordt weer gegeven in de Configuration Manager-console.  

 **Beschrijving:**  

 Verlopen software-updates konden voorheen worden geïmplementeerd op clientcomputers, maar zodra een software-update is verlopen, kunnen er geen nieuwe implementaties meer worden gemaakt voor de software-updates. Verlopen software-updates worden verwijderd uit actieve implementaties en worden niet langer beschikbaar gemaakt voor clients.  

 **Operationele problemen:**  

 Er zijn geen operationele problemen.

### <a name="superseded-icon"></a>Pictogram Vervangen  
 ![Vervangend pictogram ](../media/Superseded.jpg) het pictogram met de gele ster vertegenwoordigt een vervangen software-update. U kunt vervangen software-updates ook identificeren door de **vervangen** kolom te bekijken voor de software-update wanneer deze wordt weer gegeven in de Configuration Manager-console.  

 **Beschrijving:**  

 Vervangen software-updates zijn vervangen door de nieuwere versies van de software-update. Normaal gesp roken voert een software-update die een andere software-update vervangt, een of meer van de volgende handelingen uit:  

- Bevordert, verbetert of voegt iets toe aan de oplossing die werd geleverd door een of meer eerder uitgebrachte software-updates.  

- Verbetert de efficiëntie van het bestandspakket van de software-update, dat clients installeren wanneer de software-update is goedgekeurd voor installatie. Bijvoorbeeld, de vervangen software-update kan bestanden bevatten die niet langer relevant zijn voor de oplossing of voor de besturings systemen die nu door de nieuwe software-update worden ondersteund, zodat deze bestanden niet zijn opgenomen in het vervangende bestands pakket van de software-update.  

- Werkt nieuwere versies van een product bij, of met andere woorden, is niet langer van toepassing op oudere versies of configuraties van een product. Software-updates kunnen ook andere software-updates vervangen als er wijzigingen zijn aangebracht om de taalondersteuning uit te breiden. Een latere revisie van een product update voor Microsoft 365-apps kan bijvoorbeeld ondersteuning voor een ouder besturings systeem verwijderen, maar extra ondersteuning toevoegen voor nieuwe talen in de oorspronkelijke software-update release.  

  Op het tabblad Vervangingsregels van het dialoogvenster Eigenschappen van software-updatepuntcomponent, kunt u aangeven hoe u vervangen software-updates wilt beheren. Zie [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules)voor meer informatie.  

  **Operationele problemen:**  

  Indien mogelijk moet u in plaats van de vervangen software-update de vervangende software-update implementeren op clientcomputers. U kunt op het tabblad **Vervangingsinformatie** in de eigenschappen van de software-update een lijst weergeven van de software-updates die de software-update vervangen.  

### <a name="invalid-icon"></a>Pictogram Ongeldig  
 ![Ongeldig pictogram](../media/Invalid.jpg) Het pictogram met de rode X duidt op een ongeldige software-update.  

 **Beschrijving:**  

 Ongeldige software-updates bevinden zich in een actieve implementatie, maar om de een of andere reden is de inhoud (software-update bestanden) niet beschikbaar. Hier volgen enkele scenario's waarin deze status kan zich voordoen:  

- U kunt de software-update implementeren, maar het software-updatebestand wordt verwijderd uit het implementatiepakket en is niet meer beschikbaar.  

- U maakt een implementatie van een software-update op een site en het implementatie object wordt gerepliceerd naar een onderliggende site, maar het implementatie pakket is niet met succes gerepliceerd naar de onderliggende site.  

  **Operationele problemen:**  

  Als de inhoud voor een software-update ontbreekt, kunnen clients de software-update niet installeren totdat de inhoud beschikbaar is op een distributiepunt. U kunt de inhoud opnieuw naar distributiepunten distribueren met behulp van de actie **Opnieuw distribueren** . Als er inhoud ontbreekt voor een software-update in een implementatie die is gemaakt op een bovenliggende site, moet de software-update worden gerepliceerd of opnieuw worden gedistribueerd naar de onderliggende site. Zie [de inhoud beheren die u hebt gedistribueerd](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage)voor meer informatie over het opnieuw distribueren van inhoud.  

### <a name="metadata-only-icon"></a>Pictogram Alleen metagegevens
 ![Pictogram alleen meta gegevens](../media/MetadataOnly.png) Het pictogram met de blauwe pijl duidt op een software-update waarbij alleen de metagegevens worden bijgewerkt.

 **Beschrijving:**  

 Software-updates met alleen meta gegevens zijn beschikbaar in de Configuration Manager-console voor rapportage. U kunt software-updates met alleen meta gegevens niet implementeren of downloaden omdat er geen software-update bestand is gekoppeld aan de meta gegevens van software-updates.  

 **Operationele problemen:**  

 Software-updates met alleen meta gegevens zijn beschikbaar voor rapportage doeleinden en zijn niet bedoeld voor de implementatie van software-updates.  

## <a name="icons-for-software-update-groups"></a>Pictogrammen voor software-updategroepen  
 Software-updategroepen worden aangeduid met een van de volgende pictogrammen.  

### <a name="normal-icon"></a>Pictogram Normaal  
 ![Software-update groepen-pictogram normaal](../media/Normal.jpg) Het pictogram met de groene pijl duidt op een software-updategroep die alleen normale software-updates bevat.  

 **Operationele problemen:**  

 Er zijn geen operationele problemen.  

### <a name="expired-icon"></a>Pictogram Verlopen  
 ![Software-update groepen-pictogram verlopen](../media/Expired.jpg) Het pictogram met de zwarte X duidt op een software-updategroep die een of meer verlopen software-updates bevat.  

 **Operationele problemen:**  

 Indien mogelijk moeten de verlopen software-updates in de software-updategroep worden verwijderd of vervangen.  

### <a name="superseded-icon"></a>Pictogram Vervangen  
 ![Software-update groepen-vervangen pictogram](../media/Superseded.jpg) Het pictogram met de gele ster duidt op een software-updategroep die een of meer vervangen software-updates bevat.  

 **Operationele problemen:**  

 Indien mogelijk moet de vervangen software-update in de software-updategroep worden vervangen door de vervangende software-update.  

### <a name="invalid-icon"></a>Pictogram Ongeldig  
 ![Software-update groepen-ongeldig pictogram](../media/Invalid.jpg) Het pictogram met de rode X duidt op een software-updategroep die een of meer ongeldige software-updates bevat.  

 **Operationele problemen:**  

 Als de inhoud voor een software-update ontbreekt, kunnen clients de software-update niet installeren totdat de inhoud beschikbaar is op een distributiepunt. U kunt de inhoud opnieuw naar distributiepunten distribueren met behulp van de actie **Opnieuw distribueren** . Als er inhoud ontbreekt voor een software-update in een implementatie die is gemaakt op een bovenliggende site, moet de software-update worden gerepliceerd of opnieuw worden gedistribueerd naar de onderliggende site. Zie [de inhoud beheren die u hebt gedistribueerd](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage)voor meer informatie over het opnieuw distribueren van inhoud.  


## <a name="next-steps"></a>Volgende stappen 

[Software-updates plannen](../plan-design/plan-for-software-updates.md)
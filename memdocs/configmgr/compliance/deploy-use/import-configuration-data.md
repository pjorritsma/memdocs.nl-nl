---
title: Configuratiegegevens importeren
titleSuffix: Configuration Manager
description: Importeer configuratie gegevens als deze zijn opgenomen in een cab-bestands indeling en voldoen aan het ondersteunde taal schema voor service modellering.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 3c31f97e2a494fa4b0d3e9e825a81b562859e5dd
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240351"
---
# <a name="import-configuration-data-with-configuration-manager"></a>Configuratie gegevens importeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Naast het maken van configuratie basislijnen en configuratie-items in de Configuration Manager-console, kunt u configuratie gegevens importeren als deze zijn opgenomen in een cab-bestands indeling en voldoen aan het ondersteunde SML-schema (Service Modeling Language). U kunt configuratie gegevens importeren uit:  

- Aanbevolen configuratiegegevens (configuratiepakketten) die zijn gedownload van Microsoft of van andere sites van softwareleveranciers.  

- Configuratie gegevens die zijn geëxporteerd uit System Center 2012 Configuration Manager en hoger.  

- Configuratie gegevens die extern zijn gemaakt en die voldoen aan het SML-schema.  

  Zie [System Center 2012 Configuration Manager Configuration Pack](https://www.microsoft.com/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all)(Engelstalig) voor een voorbeeld van een configuratiepakket waarmee u compliantie beheert voor System Center 2012 Configuration Manager-siteserverrollen.  

Wanneer u een configuratiebasislijn importeert, kunnen enkele of alle van de configuratie-items waarnaar wordt verwezen in de configuratiebasislijn ook worden opgenomen in het CAB-bestand. Tijdens het import proces wordt in Configuration Manager gecontroleerd of alle configuratie-items waarnaar wordt verwezen in de configuratie basislijn ook zijn opgenomen in het CAB-bestand of al aanwezig zijn in de Configuration Manager-site. Het import proces mislukt als u een configuratie basislijn probeert te importeren die verwijst naar de configuratie gegevens die Configuration Manager niet kan worden gevonden.  

Hieronder worden enkele andere scenario's beschreven waarin het importproces kan mislukken:  

-   De configuratie gegevens verwijzen naar configuratie gegevens die Configuration Manager niet in de data base of in het CAB-bestand zelf kunnen worden gevonden.  

-   De configuratie gegevens zijn al aanwezig in de Configuration Manager-Data Base met dezelfde naam en versie van de configuratie gegevens, maar de inhouds versie wijkt af.  

-   De configuratie gegevens zijn al aanwezig in de Configuration Manager-Data Base met dezelfde inhouds versie, maar de hash-berekening identificeert deze als andere.  

-   Een nieuwere versie van de configuratie gegevens met dezelfde naam is al aanwezig of is onlangs verwijderd uit de Configuration Manager-Data Base.  

-   In een Configuration Manager hiërarchie met meerdere sites zijn de configuratie gegevens oorspronkelijk geïmporteerd van een bovenliggende site. U moet deze bijwerken van dezelfde site, niet een onderliggende site.  

### <a name="import-configuration-data"></a>Configuratiegegevens importeren  

1.  Klik in de Configuration Manager-console op **activa en nalevings**  >  **configuratie-items** of **configuratie basislijnen**
2.  Klik op het tabblad **Start** in de groep **maken** op **configuratie gegevens importeren**.  
3.  Klik op de pagina **Bestanden selecteren** van de wizard **Configuratiegegevens importeren**op **Toevoegen**en selecteer in het dialoogvenster **Openen** de CAB-bestanden die u wilt importeren.  
4.  Schakel het selectie vakje **een nieuwe kopie maken van de geïmporteerde configuratie basislijnen en configuratie-items** in als u wilt dat de geïmporteerde configuratie gegevens kunnen worden bewerkt in de Configuration Manager-console.  
5.  Controleer op de pagina **samen vatting** de acties die zullen worden uitgevoerd en voltooi vervolgens de wizard.  

De geïmporteerde configuratie gegevens worden weer gegeven in het knoop punt **instellingen voor naleving** van de werk ruimte **activa en naleving** .  

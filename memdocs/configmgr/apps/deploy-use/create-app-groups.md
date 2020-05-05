---
title: Toepassingsgroepen maken
titleSuffix: Configuration Manager
description: Een groep toepassingen maken die u kunt verzenden naar een gebruiker of apparaat als één implementatie in Configuration Manager.
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f63c52fcd2aaccbfbe04160581318126bc53db12
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643119"
---
# <a name="create-application-groups"></a>Toepassingsgroepen maken

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3555907-->

Met ingang van versie 1906 maakt u een groep toepassingen die u kunt verzenden naar een gebruiker of een apparaat-verzameling als één implementatie. De meta gegevens die u opgeeft over de app-groep worden gezien in Software Center als één entiteit. U kunt de apps in de groep ordenen, zodat de client deze in een specifieke volg orde installeert.

> [!Note]  
> In deze versie van Configuration Manager zijn app-groepen een functie van de voorlopige versie. Zie [functies van voorlopige versies](../../core/servers/manage/pre-release-features.md)om deze functie in te scha kelen.  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **toepassings beheer** uit en selecteer het knoop punt **toepassings groep** .  

1. Selecteer **toepassings groep maken**in de groep maken op het lint.

1. Op de pagina **algemene informatie** geeft u informatie op over de app-groep.  

1. Op de pagina **Software Center** neemt u informatie op die wordt weer gegeven in Software Center.  

1. Selecteer op de pagina **groep van toepassingen** de optie **toevoegen**. Selecteer een of meer apps voor deze groep. Volg deze opnieuw met behulp van de acties **omhoog** en **omlaag** .  

1. Voltooi de wizard.  

Implementeer de app-groep met hetzelfde proces als voor een toepassing. Zie [toepassingen implementeren](deploy-applications.md)voor meer informatie. Vanaf versie 1910 kunt u een app-groep implementeren op apparaat-of gebruikers verzamelingen.

Nadat u de groep hebt geïmplementeerd:

- Als u een nieuwe app toevoegt aan de groep, moet u de nieuwe app-inhoud afzonderlijk distribueren naar distributie punten.

- Als u een app in de app-groep wijzigt, distribueert u de inhoud opnieuw.

Als u problemen met de implementatie van een app-groep wilt oplossen, gebruikt u de volgende logboek bestanden op de client:

- **AppGroupHandler. log**
- **AppEnforce.log**
- **SettingsAgent. log**

> [!Important]  
> Maak of implementeer geen app-groep totdat u de gehele hiërarchie en de beoogde clients bijwerkt naar ten minste versie 1906.

### <a name="known-issues"></a>Bekende problemen

- *Versie 1906*: apps in de groep kunnen alleen **Windows Installer** -of **script** implementatie typen bevatten.
  - *Versie 1906*: Stel het installatie gedrag van het implementatie type in om **voor het systeem te installeren**.
- De volgende implementatie opties werken mogelijk niet: waarschuwingen, goed keuring, gefaseerde implementatie, herstellen.
- U kunt geen app-groepen exporteren of importeren.
- Neem in de groep geen apps op die opnieuw moeten worden opgestart of de groeps implementatie kan mislukken.
- *Versie 1906*: u kunt de app-groep niet implementeren in een gebruikers verzameling.
- *Versie 1906*: gebruikers kunnen de app-groep niet **verwijderen** in Software Center.
- Als u een app verwijdert die deel uitmaakt van een app-groep, wordt de volgende waarschuwing weer gegeven wanneer u de eigenschappen van de app-groep weer geven: ' kan geen informatie laden over alle toepassingen in de groep '. Breng een eenvoudige wijziging aan in de app-groep en sla deze op. Voeg bijvoorbeeld een ruimte toe aan de opmerkingen van de **beheerder**. Wanneer u de wijziging opslaat, wordt de verwijderde app uit de groep verwijderd.<!-- 7099542 -->

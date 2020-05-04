---
title: Windows Embedded-toepassingen maken
titleSuffix: Configuration Manager
description: Bekijk welke overwegingen u moet meenemen wanneer u toepassingen voor Windows Embedded-apparaten maakt en implementeert.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bec9765e5152863bb8b55a0b75f1e5c2fc580550
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710494"
---
# <a name="create-windows-embedded-applications-with-configuration-manager"></a>Windows Embedded-toepassingen maken met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Naast de andere Configuration Manager-vereisten en-procedures voor het maken van een toepassing, moet u ook rekening houden met de volgende overwegingen wanneer u toepassingen voor Windows Embedded-apparaten maakt en implementeert.  

## <a name="general-considerations"></a>Algemene overwegingen  

-   Wanneer u toepassingen implementeert op Windows Embedded-apparaten waarvoor schrijf filters zijn ingeschakeld, kunt u opgeven of het schrijf filter op het apparaat moet worden uitgeschakeld tijdens de implementatie van de app. Daarna kunt u ervoor kiezen om de schrijf filter opnieuw te starten na de implementatie van de app. Als het schrijf filter niet is uitgeschakeld, wordt de software geïmplementeerd op een tijdelijke overlay. Dit betekent dat de software niet meer wordt geïnstalleerd wanneer het apparaat opnieuw wordt opgestart, tenzij een andere implementatie afdwingt dat wijzigingen blijven bestaan.  

-   Wanneer u een toepassing implementeert op een Windows Embedded-apparaat, moet u ervoor zorgen dat het apparaat lid is van een verzameling met een geconfigureerd onderhoudsvenster. U kunt op deze manier beheren wanneer het schrijffilter is uitgeschakeld en ingeschakeld en wanneer het apparaat opnieuw wordt gestart.  

-   De instelling die het gedrag van schrijf filters bepaalt, is een selectie vakje met de naam **wijzigingen door voeren bij deadline of tijdens een onderhouds venster (opnieuw opstarten nood zakelijk)**.  

## <a name="tips-for-deploying-applications"></a>Tips voor het implementeren van toepassingen  

**Gebruik vereiste toepassingen in plaats van beschik bare toepassingen voor Windows Embedded-apparaten waarvoor schrijf filters zijn ingeschakeld.** Omdat gebruikers geen apps kunnen installeren vanuit software Center op een Windows Embedded-apparaat waarop schrijf filters zijn ingeschakeld, moet u toepassingen altijd implementeren met het implementatie doel **vereist** en niet **beschikbaar zijn** voor deze apparaten. Doorgaans is dit geen probleem omdat op computers waarop een Windows Embedded-besturings systeem wordt uitgevoerd, vaak een enkele toepassing wordt uitgevoerd die op dezelfde manier moet worden uitgevoerd voor meerdere gebruikers. Daarom worden deze apparaten in hoge mate beheerd en vergrendeld door de IT-afdeling. Vereiste toepassingen zijn geschikt voor dit scenario.

 Als gebruikers echter wel meer dan één toepassing uitvoeren op Embedded-apparaten wanneer schrijffilters zijn ingeschakeld, moet u deze gebruikers informeren over de volgende beperkingen:  

-   Gebruikers kunnen geen vereiste software installeren vanuit Software Center.  

-   Gebruikers kunnen hun kantooruren niet wijzigen op het tabblad Opties van Software Center.  

-   Gebruikers kunnen de installatie van een vereiste toepassing niet uitstellen.  

Bovendien kunnen gebruikers met beperkte rechten zich niet aanmelden tijdens een onderhouds periode als Configuration Manager wijzigingen doorvoert voor software-installaties en-updates. Gedurende deze periode krijgen gebruikers een bericht te zien met de melding dat het apparaat niet beschikbaar is omdat het wordt onderhouden.  

**Implementeer geen toepassingen op Windows Embedded-apparaten waarvoor schrijf filters zijn ingeschakeld als de gebruiker de licentie voorwaarden moet accepteren voor de toepassingen.** Wanneer schrijf filters zijn uitgeschakeld, zodat Configuration Manager software op Inge sloten apparaten kan installeren, kunnen gebruikers met beperkte rechten zich niet aanmelden bij het apparaat. Als het voor de installatie vereist is dat de gebruiker de licentievoorwaarden accepteert, is dit niet mogelijk en zal de installatie dus mislukken. Zorg dat u geen software op Windows Embedded-apparaten implementeert als voor de installatie gebruikersinteractie vereist is. U kun de lijst Toepasselijke platforms gebruiken om deze besturingssystemen te filteren.  

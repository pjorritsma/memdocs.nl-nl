---
title: Implementatie plannen in Desktop Analytics
titleSuffix: Configuration Manager
description: Meer informatie over implementatie plannen in Desktop Analytics.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ccc325ac4b8e02142a1442862ad661a77b0561f2
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268484"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Implementatie plannen in Desktop Analytics

Desktop Analytics verzamelt en analyseert gegevens van apparaten, toepassingen en stuur Programma's in uw organisatie. Op basis van deze analyse en uw invoer kunt u de service gebruiken om implementatie plannen voor Windows 10 te maken. Implementatie plannen hebben de volgende kenmerken:  

- Automatisch aanbevelen welke apparaten moeten worden meegenomen in pilots  

- Compatibiliteits problemen identificeren en oplossingen Voorst Ellen  

- De status van de implementatie evalueren vóór, tijdens en na de updates  

- De voortgang van uw implementatie volgen  

Als onderdeel van uw implementatie plan voert u de volgende acties uit:  

- Bepalen welke versies van Windows 10 u wilt implementeren  

- Kies welke groepen apparaten u wilt implementeren  

- Gereedheids regels maken voor de implementatie  

- Het belang van uw apps bepalen  

- Test apparaten kiezen op basis van Automatische aanbevelingen  

- Bepalen hoe u problemen met apps kunt oplossen op basis van aanbevelingen van Desktop Analytics  

Standaard worden de gegevens van het implementatie plan door Desktop Analytics dagelijks vernieuwd. Alle wijzigingen die u aanbrengt in een implementatie plan, zoals het toewijzen van belang aan een app of het kiezen van een apparaat dat in een pilot moet worden meegenomen, duurt Maxi maal 24 uur om te verwerken. U kunt dit proces versnellen door een gegevens vernieuwing op aanvraag in te dienen. Zie [Veelgestelde vragen over desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)voor meer informatie.  

Nadat u de verbinding met Desktop Analytics hebt gemaakt met Configuration Manager, selecteert u uw verzamelingen in de implementatie plannen. Met deze integratie kunt u Windows vervolgens implementeren op een verzameling op basis van de gegevens van de Desktop Analytics.

## <a name="readiness-rules"></a>Gereedheids regels

De volgende gereedheids regels zijn beschikbaar in implementatie plannen:

- Hiermee wordt aangegeven of uw apparaten automatisch Stuur Programma's ontvangen van Windows Update. Als apparaten het stuur programma-updates van Windows Update ontvangen, worden de problemen met stuur Programma's die zijn geïdentificeerd als onderdeel van de gereedheids beoordeling automatisch gemarkeerd als **gereed**.  

- Drempel waarde voor aantal geïnstalleerde installaties voor Windows-apps. **Als een**app wordt geïnstalleerd op een hoger percentage computers dan deze drempel waarde, markeert het implementatie plan de app als een afdoende. Deze tag betekent dat u kunt bepalen hoe belang rijk de app moet testen tijdens de test fase.  

## <a name="plan-assets"></a>Activa plannen

<!-- 4670224 -->

Hoewel in het gebied [activa](about-assets.md) ook apparaten en apps worden weer gegeven, bevat het gedeelte **plan assets** onder een specifiek implementatie plan aanvullende informatie.

### <a name="devices"></a>Apparaten

Zie de **Windows-upgrade beslissing** voor elk apparaat in het implementatie plan.

Het Windows-upgrade besluit om het **apparaat te vervangen** , kan een van de volgende oorzaken hebben:

- Er is een Windows 10-vereiste processor controle mislukt. Zie [minimale hardwarevereisten](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor)voor meer informatie.
- Er is een BIOS-blok
- Er is onvoldoende geheugen beschikbaar
- Een essentieel onderdeel van het opstarten van het systeem heeft een geblokkeerd stuur programma
- Het specifieke merk en model kunnen niet worden bijgewerkt
- Er is een onderdeel van een weer gave met een stuur programma dat alle volgende kenmerken heeft:
  - U niet overschrijft
  - Er is geen stuur programma in de nieuwe versie van het besturings systeem
  - Het is nog niet aanwezig Windows Update
- Er is een ander Plug en Play-onderdeel op het systeem dat de upgrade blokkeert
- Er is een draadloos onderdeel dat gebruikmaakt van een XP-geëmuleerd stuur programma
- Een netwerk onderdeel met een actieve verbinding zal het stuur programma kwijt raken. Met andere woorden, na een upgrade kan de verbinding met het netwerk verloren gaan.

De Windows-upgrade beslissing om **opnieuw te installeren** geeft aan dat voor de upgrade een installatie moet worden uitgevoerd, in tegens telling tot een in-place upgrade.

Een **geblokkeerd** Windows-upgrade besluit kan worden veroorzaakt door de volgende redenen:

- U stelt de upgrade beslissing van een of meer assets in op **geen**.

- De inventarisatie gegevens voor dat apparaat zijn onvolledig en desktop Analytics kan geen volledige compatibiliteits beoordeling uitvoeren.

### <a name="apps"></a>Apps

Stel de **beslissing** voor de upgrade en het **belang** van deze app in dit implementatie plan in. Zie [implementatie plannen maken](create-deployment-plans.md)voor meer informatie.

In de details van de app kunt u ook de volgende informatie zien: aanbevelingen, compatibiliteits risico factoren en bekende problemen met micro soft. Gebruik deze informatie om de beslissing over de **upgrade**te kunnen instellen. Zie [Compatibility Assessment](compat-assessment.md)(Engelstalig) voor meer informatie.

De apps die door Desktop *Analytics worden weer gegeven, zijn gebaseerd* op de drempel waarde voor laag aantal installaties voor de gereedheids regels van het implementatie plan. Zie [gereedheids regels](create-deployment-plans.md#readiness-rules)voor meer informatie.

   > [!Tip]
   > Zie voor meer informatie over de app-categorie ' niet belang rijk ' [automatische upgrade besluit van systeem-en Store-apps](about-assets.md#bkmk_plan-autoapp). <!-- 3587232 -->

De instelling Details van de **App-versies** is standaard uitgeschakeld. op dit tabblad worden alle versies van apps met dezelfde naam en uitgever gecombineerd.<!-- 5542186 --> Het standaard gedrag helpt bij het verminderen van het totale aantal apps dat u ziet, waardoor u minder inspanningen krijgt om aantekeningen aan de apps te maken. Het aantal apps in de tegel **apps** op de achtergrond is ook gelijk aan deze instelling. In plaats van honderden exemplaren van micro soft Edge te vermelden, is er bijvoorbeeld één exemplaar voor alle versies. U kunt beslissingen voor alle versies eenmaal maken. Als u beslissingen moet nemen over specifieke versies van een app, schakelt u deze instelling in. U kunt deze instelling ook configureren wanneer u werkt op het niveau van globale activa. Zie [about assets-apps (](about-assets.md#apps)Engelstalig) voor meer informatie.

Wanneer de instelling Details van de **App-versie** is uitgeschakeld, wordt in het deel venster app-Details het aantal versies en talen van de app weer gegeven dat wordt gecombineerd. Als u wijzigingen in de app-details opslaat, geldt dit voor alle versies. Stel bijvoorbeeld de beslissing van de **upgrade** of het **belang**in. Bij sommige waarden wordt ' multiple ' weer gegeven, wat betekent dat er niet één consistente waarde in alle versies is. De service maakt nog steeds compatibiliteits risico Beoordelingen voor elke versie. Schakel Details van de **App-versies** in om de compatibiliteits risico beoordeling voor een specifieke app-versie te bekijken.

### <a name="drivers"></a>Stuurprogramma's

Zie de lijst met stuur Programma's die zijn opgenomen in dit implementatie plan. Stel de **beslissing**van de upgrade in, lees de aanbeveling van micro soft en zie risico factoren voor compatibiliteit.

## <a name="importance"></a>Urgentie

Als onderdeel van het implementatie plan stelt u het *belang* van de apps in. Desktop Analytics detecteert deze apps zoals geïnstalleerd op de doel apparaten. Met deze instelling kan Desktop Analytics bepalen welke apparaten worden opgenomen in de test fase van de implementatie.

Als een app wordt geïnstalleerd op minder dan 2% van de doel apparaten, is het gemarkeerd als **laag aantal installaties**. Twee procent is de standaard waarde. U kunt de drempel waarde voor de gereedheids instellingen aanpassen van 0% tot 10%. Met Desktop Analytics worden deze apps automatisch gemarkeerd als **gereed voor de upgrade**.  

Kies voor apps het belang van **kritiek**, **belang rijk**of **niet belang rijk**. Als u één als kritiek of belang rijk markeert, biedt Desktop Analytics in de pilot implementatie enkele apparaten met die app. De service omvat de pilot meer exemplaren van een kritieke app. Als u een app markeert als niet belang rijk, stelt Desktop Analytics deze automatisch in op **gereed voor de upgrade**.

## <a name="pilot-devices"></a>Pilot-apparaten

Desktop Analytics combineert de belang rijke informatie met de globale pilot instellingen. Vervolgens wordt er een aanbeveling gemaakt waarvoor apparaten deel moeten uitmaken van de proef implementatie. De aanbevolen pilot implementatie omvat apparaten met verschillende hardwareconfiguraties en een of meer exemplaren van alle essentiële en belang rijke apps. Als een app als kritiek is gemarkeerd, raadt de service meer apparaten aan met die app in de pilot.

## <a name="deployment-plans-in-configuration-manager"></a>Implementatie plannen in Configuration Manager

Nadat u een implementatie plan hebt gemaakt, gebruikt u Configuration Manager om de producten te implementeren. Zodra de implementatie is gestart, controleert Desktop Analytics de implementatie op basis van de instellingen in het plan.

## <a name="next-steps"></a>Volgende stappen

- [Meer informatie over desktop Analytics-assets](about-assets.md): apparaten, stuur Programma's en apps  

- [Meer informatie over beveiliging en functie-updates](about-updates.md)  

- [Een implementatie plan maken](create-deployment-plans.md)  

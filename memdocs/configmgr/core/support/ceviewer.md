---
title: Viewer voor collectie-evaluatie
titleSuffix: Configuration Manager
description: Gebruik de verzamelings evaluatie-viewer voor het bekijken en oplossen van problemen met het verzamelings evaluatie proces in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9ab75238e5dd26872847e68863ef603d3ac22671
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723416"
---
# <a name="collection-evaluation-viewer"></a>Viewer voor collectie-evaluatie

*Van toepassing op: Configuration Manager (huidige vertakking)*

Verzamelings evaluatie Viewer is een van de [Configuration Manager-hulpprogram ma's](tools.md). Gebruik het om het verzamelings evaluatie proces op de primaire site server te bekijken en problemen op te lossen.

Het hulp programma geeft de volgende informatie weer:  

- Zowel historische als actuele gegevens voor volledige en incrementele verzamelings evaluaties  

- De status van de evaluatie wachtrij  

- De tijd voor het volt ooien van de verzamelings evaluaties  

- Welke verzamelingen momenteel worden geëvalueerd  

- De geschatte tijd voor het starten en volt ooien van een verzamelings evaluatie  



## <a name="about-collection-evaluation"></a>Over verzamelings evaluatie

Het verzamelings evaluatie proces wordt uitgevoerd door de lidmaatschaps regels van een verzameling te evalueren om de leden bij te werken. De site plaatst een verzameling die in een van vier verschillende wacht rijen wordt geëvalueerd:  

- **Hand matige wachtrij**: voor verzamelingen die een beheerder hand matig heeft geselecteerd voor evaluatie vanaf de-console  

- **Nieuwe wachtrij**: voor nieuw gemaakte verzamelingen  

- **Volledige wachtrij**: voor verzamelingen die moeten worden voltooid voor volledige evaluatie  

- **Incrementele wachtrij**: voor verzamelingen met incrementele evaluatie  

Er zijn vier threads die worden uitgevoerd om de verzamelingen in de bovenstaande wacht rijen te evalueren. Elke wachtrij bevat een reeks matrices en elke matrix bevat de verzamelingen die moeten worden geëvalueerd. De thread die wordt uitgevoerd voor de wachtrij selecteert een verzameling uit de matrix en voert de evaluatie uit. De lengte van de wachtrij geeft het aantal matrixen in de wachtrij aan.



## <a name="requirements"></a>Vereisten

- Het hulp programma uitvoeren op de site server  

- Voer het hulp programma uit met een gebruiker met beheerders rechten met ten minste de rol **alleen-lezen analist**  

- Voor de gebruiker is ook de machtiging **lezen** vereist voor de site database in SQL



## <a name="usage"></a>Gebruik

Voer **CEViewer. exe**uit. Het hoofd menu van het hulp programma bevat de volgende tabbladen: 

- [Verbinding maken](#bkmk_connect): de eerste verbinding met de primaire site server en SQL Server tot stand brengen  

- [Volledige evaluatie](#bkmk_full-eval): Hier vindt u gedetailleerde informatie over alle eerdere volledige evaluaties   

- [Incrementele evaluatie](#bkmk_incremental-eval): Hier vindt u gedetailleerde informatie over alle vorige incrementele evaluaties  

- [Alle wacht rijen](#bkmk_all-q): Hiermee wordt een overzicht gegeven van de huidige verzamelings evaluaties voor alle vier wacht rijen  

- [Hand matige wachtrij](#bkmk_manual-q): bevat gedetailleerde informatie over de evaluatie van de huidige verzameling in de hand matige wachtrij  

- [Nieuwe wachtrij](#bkmk_new-q): bevat gedetailleerde informatie over de evaluatie van de huidige verzameling in de nieuwe wachtrij  

- [Volledige wachtrij](#bkmk_full-q): bevat gedetailleerde informatie over de huidige verzamelings evaluatie in de volledige wachtrij  

- [Incrementele wachtrij](#bkmk_incremental-q): bevat gedetailleerde informatie over de evaluatie van de huidige verzameling in de incrementele wachtrij  


### <a name="connect-tab"></a><a name="bkmk_connect"></a>Tabblad verbinden

Op dit tabblad kunt u de eerste verbinding met de primaire site server tot stand brengen. Het hulp programma brengt ook een verbinding tot stand met de SQL Server die de site database host.

De verbindingen met de primaire site server en SQL-servers gebruiken de huidige aanmeldings referenties van de gebruiker. Verbindingen met de centrale beheer site of een secundaire site worden niet ondersteund. Er wordt geen evaluatie proces verzameld op deze sites.

Wanneer het hulp programma een verbinding tot stand heeft gebracht, ziet u een melding aan de onderkant van de verzamelings evaluatie viewer waarmee de verbinding van het hulp programma met de SQL-Server wordt bevestigd. 


### <a name="full-evaluation-tab"></a><a name="bkmk_full-eval"></a>Tabblad volledige evaluatie

Bevat gedetailleerde informatie over eerdere volledige verzamelings evaluaties. Er zijn acht kolommen:  

- **Naam verzameling**: naam van de verzameling  

- **Site-id**: site-id van de verzameling   

- **Uitvoerings tijd**: hoelang de laatste evaluatie van de verzameling is uitgevoerd, in seconden  

- **Laatste keer**dat de evaluatie is voltooid: wanneer de laatste verzamelings evaluatie is voltooid  

- **Volgende evaluatie tijd**: wanneer de volgende volledige evaluatie wordt gestart  

- **Wijzigingen**in het lid: het lid verandert in de laatste verzamelings evaluatie. Deze wijzigingen zijn plus (toegevoegde leden) of minknop (leden worden verwijderd).  

- **Laatste wijzigings tijd van lid**: de meest recente keer dat er een lidmaatschaps wijziging is opgetreden in de verzamelings evaluatie  

- **Percentage**: het percentage van de evaluatie tijd voor deze verzameling gedurende de evaluatie tijd van het totaal (alle verzamelingen)  


### <a name="incremental-evaluation-tab"></a><a name="bkmk_incremental-eval"></a>Tabblad incrementele evaluatie

Geeft gedetailleerde informatie weer over evaluaties van afgelopen incrementele verzamelingen. Er zijn zeven kolommen:  

- **Naam verzameling**: naam van de verzameling  

- **Site-id**: site-id van de verzameling   

- **Uitvoerings tijd**: hoelang de laatste evaluatie van de verzameling is uitgevoerd, in seconden  

- **Laatste keer**dat de evaluatie is voltooid: wanneer de laatste verzamelings evaluatie is voltooid  

- **Wijzigingen**in het lid: het lid verandert in de laatste verzamelings evaluatie. Deze wijzigingen zijn plus (toegevoegde leden) of minknop (leden worden verwijderd).  

- **Laatste wijzigings tijd van lid**: de meest recente keer dat er een lidmaatschaps wijziging is opgetreden in de verzamelings evaluatie  

- **Percentage**: het percentage van de evaluatie tijd voor deze verzameling gedurende de evaluatie tijd van het totaal (alle verzamelingen)  


### <a name="all-queues-tab"></a><a name="bkmk_all-q"></a>Het tabblad alle wacht rijen

Overzicht van de evaluaties van Live verzamelingen voor alle vier de wacht rijen. Er zijn zes secties:  

- **Samen vatting**: hier worden het totale verzamelings nummer en de lengte van de wachtrij voor alle verzamelingen in alle vier wacht rijen weer gegeven  

- **Evaluatie uitvoeren**: een lijst met de verzamelingen die momenteel worden geëvalueerd in elke wachtrij, en hoelang deze actief is  

- **Hand matig bijwerken**: toont een korte samen vatting van de verzamelingen die worden geëvalueerd, de geschatte voltooiings tijd en de volg orde van de evaluatie in de hand matige wachtrij  

- **Nieuwe verzameling**: toont een korte samen vatting van de verzamelingen die worden geëvalueerd, de geschatte voltooiings tijd en de volg orde van de evaluatie in de nieuwe verzamelings wachtrij  

- **Volledige evaluatie**: toont een korte samen vatting van de verzamelingen die worden geëvalueerd, de geschatte voltooiings tijd en de volg orde van de evaluatie in de volledige evaluatie wachtrij  

- **Incrementele evaluatie**: toont een korte samen vatting van de verzamelingen die worden geëvalueerd, de geschatte voltooiings tijd en de volg orde van de evaluatie in de incrementele evaluatie wachtrij  


### <a name="manual-queue-tab"></a><a name="bkmk_manual-q"></a>Tabblad hand matige wachtrij

Toont informatie over de hand matige verzamelings evaluatie die momenteel wordt geëvalueerd. De volg orde in de lijst is de volg orde waarin de verzameling wordt geëvalueerd. Er zijn vier kolommen:  

- **Naam verzameling**: naam van de verzameling  

- **Site-id**: site-id van de verzameling   

- **Geschatte voltooiings tijd**: wanneer de evaluatie van de schatting moet worden voltooid  

- **Geschatte uitvoerings tijd**: hoe lang de evaluatie moet worden uitgevoerd, in dag: uur: minuut: tweede notatie  


### <a name="new-queue-tab"></a><a name="bkmk_new-q"></a>Tabblad nieuwe wachtrij

Toont de live informatie over de evaluatie van de nieuwe verzameling die wordt geëvalueerd. De volg orde in de lijst is de volg orde waarin de verzameling wordt geëvalueerd. Er zijn vier kolommen:  

- **Naam verzameling**: naam van de verzameling  

- **Site-id**: site-id van de verzameling   

- **Geschatte voltooiings tijd**: wanneer de evaluatie van de schatting moet worden voltooid  

- **Geschatte uitvoerings tijd**: hoe lang de evaluatie moet worden uitgevoerd, in dag: uur: minuut: tweede notatie  


### <a name="full-queue-tab"></a><a name="bkmk_full-q"></a>Tabblad volledige wachtrij

Toont informatie over de volledige verzamelings evaluatie die momenteel wordt geëvalueerd. De volg orde in de lijst is de volg orde waarin de verzameling wordt geëvalueerd. Er zijn vier kolommen:  

- **Naam verzameling**: naam van de verzameling  

- **Site-id**: site-id van de verzameling   

- **Geschatte voltooiings tijd**: wanneer de evaluatie van de schatting moet worden voltooid  

- **Geschatte uitvoerings tijd**: hoe lang de evaluatie moet worden uitgevoerd, in dag: uur: minuut: tweede notatie  


### <a name="incremental-queue-tab"></a><a name="bkmk_incremental-q"></a>Tabblad incrementele wachtrij

Geeft informatie weer over de evaluatie van de incrementele verzameling die momenteel wordt geëvalueerd. De volg orde in de lijst is de volg orde waarin de verzameling wordt geëvalueerd. Er zijn vier kolommen:  

- **Naam verzameling**: naam van de verzameling  

- **Site-id**: site-id van de verzameling   

- **Geschatte voltooiings tijd**: wanneer de evaluatie van de schatting moet worden voltooid  

- **Geschatte uitvoerings tijd**: hoe lang de evaluatie moet worden uitgevoerd, in dag: uur: minuut: tweede notatie  




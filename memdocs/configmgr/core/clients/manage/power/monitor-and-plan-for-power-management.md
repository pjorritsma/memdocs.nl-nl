---
title: Energie beheer bewaken en plannen
titleSuffix: Configuration Manager
description: Meer informatie over het bewaken en plannen van energie beheer in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 507bf676-2679-4e4d-8831-3ffc9cf8557e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a4e5ee9c35dd96f79ea1a88ab09200d4386a7535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715212"
---
# <a name="how-to-monitor-and-plan-for-power-management-in-configuration-manager"></a>Energie beheer bewaken en plannen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de volgende informatie om energie beheer in Configuration Manager te controleren en te plannen.  

##  <a name="how-to-use-reports-for-power-management"></a><a name="BKMK_How_to_use_reports"></a> Rapporten voor energiebeheer gebruiken  
 Energie beheer in Configuration Manager bevat verschillende rapporten waarmee u het energie verbruik en de energie-instellingen van computers in uw organisatie kunt analyseren. De rapporten kunnen ook worden gebruikt bij het oplossen van problemen.  

 Voordat u de energiebeheerrapporten kunt gebruiken, moet u de rapportage voor uw hiërarchie configureren. Zie [Introduction to Reporting](../../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over rapportage in Configuration Manager.  

> [!NOTE]  
>  Informatie over energie beheer die dagelijks rapporten worden gebruikt, wordt gedurende 31 dagen in de site database van Configuration Manager bewaard.  
>           Informatie over energie beheer die wordt gebruikt door maandelijkse rapporten, wordt gedurende 13 maanden in de site database van Configuration Manager bewaard.  
>   
>  Wanneer u rapporten uitvoert tijdens de bewakings-en plannings-en nalevings fase van energie beheer, moet u de resultaten opslaan of exporteren uit alle rapporten waarvoor u de gegevens wilt bewaren om deze later te vergelijken als ze later worden verwijderd door Configuration Manager.  

## <a name="list-of-power-management-reports"></a>Lijst met energiebeheerrapporten  
 In de volgende lijsten vindt u informatie over de energiebeheer rapporten die beschikbaar zijn in Configuration Manager.  

> [!NOTE]  
>  Energiebeheerrapporten geven het aantal fysieke computers en het aantal virtuele computers in een geselecteerde verzameling weer. Er wordt echter alleen energiebeheer-informatie van fysieke computers weergegeven in energiebeheerrapporten.  

###  <a name="computer-activity-report"></a><a name="BKMK_Activity"></a> Het rapport Computeractiviteit  
 Het rapport **Computeractiviteit** geeft een grafiek weer met de volgende activiteit voor een opgegeven verzameling gedurende een bepaalde periode:  

- **Computer aan** : de computer is ingeschakeld.  

- **Bewaking aan** : de bewaking is ingeschakeld.  

- **Gebruiker actief** : er is activiteit gedetecteerd van de computer muis, het toetsen bord of van een extern bureaublad verbinding met de computer  

  Dit rapport wordt gebruikt tijdens de bewaking-, planning- en afdwingingsfase, zodat u inzicht krijgt in het samenspel van computeractiviteiten, bewakingsactiviteiten en gebruikersactiviteiten gedurende een periode van 24 uur. Als u het rapport gedurende een aantal dagen uitvoert, worden de gegevens tijdens deze periode geaggregeerd. Aan de hand van dit rapport kunt u activiteiten tijdens kantooruren (piekuren) en buiten kantooruren (niet-piekuren) achterhalen voor een geselecteerde verzameling, zodat u kunt bepalen wanneer geconfigureerde energieschemaplannen moeten worden toegepast.  

  De grafiek toont perioden waarin computers worden ingeschakeld, maar er geen gebruikersactiviteit is. Overweeg of u beperkende energie-instellingen wilt toepassen tijdens deze perioden om energiekosten te besparen van computers die wel zijn ingeschakeld maar niet worden gebruikt. Een computer wordt beschouwd als actief als er gedurende een minuut of langer sprake is van computer-, gebruiker- of beeldschermactiviteit tijdens een uur die in de grafiek wordt weergegeven. Als een computer geen energiebeheergegevens rapporteert, wordt deze computer niet opgenomen in het rapport **Computeractiviteit** .  

  Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Begindatum**|Selecteer de begindatum voor dit rapport in de vervolgkeuzelijst.|  
|**Eind datum (optioneel)**|Selecteer een optionele einddatum voor dit rapport in de vervolgkeuzelijst.|  
|**Naam van verzameling**|Selecteer een verzameling die moet worden gebruikt voor dit rapport in de vervolgkeuzelijst.|  
|**Apparaattype**|Selecteer het type computer waarvoor u een rapport wilt maken in de vervolgkeuzelijst. Geldige waarden zijn **alle** (zowel bureau blad als draag bare computers), **Desktop** (alleen desktop computers) en **laptop** (alleen draag bare computers).|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 Dit rapport heeft geen verborgen parameters die u kunt instellen.  

#### <a name="report-links"></a>Rapportkoppelingen  
 Als er geen waarde wordt opgegeven voor **Einddatum (optioneel)** , bevat dit rapport een koppeling naar het volgende rapport met meer informatie.  

|Rapportnaam|Details|  
|-----------------|-------------|  
|**Details van computeractiviteit**|Klik op de koppeling **Klik voor gedetailleerde informatie** voor een overzicht van actieve computers, niet-actieve computers en computers waarvoor geen rapporten zijn gemaakt voor de opgegeven datum.<br /><br /> Zie [Computer Activity Details Report](#BKMK_Activity_Details) in dit onderwerp voor meer informatie.|  

###  <a name="computer-activity-by-computer-report"></a><a name="BKMK_Comp_Activity_by_computer"></a> Het rapport Computeractiviteit per computer  
 Het rapport **Computeractiviteit per computer** geeft een grafiek weer met de volgende activiteit voor een opgegeven computer op een opgegeven datum:  

- **Computer aan** : de computer is ingeschakeld.  

- **Bewaking aan** : de bewaking is ingeschakeld.  

- **Gebruiker actief** : er is activiteit gedetecteerd van de muis, het toetsenbord, of van een extern-bureaubladverbinding met de computer.  

  Dit rapport kan onafhankelijk worden uitgevoerd of worden aangeroepen door het rapport **Details van computeractiviteit** .  

> [!NOTE]  
>  Tijdens de hardware-inventarisatie wordt er informatie over computeractiviteiten verzameld bij clientcomputers. Afhankelijk van het tijdstip waarop de hardware-inventarisatie wordt uitgevoerd, wordt er mogelijk activiteit verzameld tijdens een toegepast energiebeheerschema voor piekuren of niet-piekuren.  

 Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Rapportdatum**|Selecteer een datum voor dit rapport in de vervolgkeuzelijst.|  
|**Computer naam**|Voer de naam van de computer in waarvoor u een rapport wilt.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 Dit rapport heeft geen verborgen parameters die u kunt instellen.  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport bevat koppelingen naar het volgende rapport met meer informatie over het geselecteerde item.  

|Rapportnaam|Details|  
|-----------------|-------------|  
|**Computerdetails**|Klik op de koppeling **Klik voor gedetailleerde informatie** om de energiemogelijkheden, energie-instellingen en toegepaste energiebeheerschema's voor de geselecteerde computer te zien.|  

###  <a name="computer-activity-details-report"></a><a name="BKMK_Activity_Details"></a> Computer Activity Details report  
 Het rapport **Details van computeractiviteit** geeft een lijst met actieve of niet-actieve computers en hun slaap- en waakstandmogelijkheden weer. Dit rapport wordt aangeroepen door het [Computer Activity Report](#BKMK_Activity) en is niet ontworpen om rechtstreeks door de sitebeheerder te worden uitgevoerd.  

 Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Naam van verzameling**|Selecteer een verzameling die moet worden gebruikt voor dit rapport in de vervolgkeuzelijst.|  
|**Rapportdatum**|Selecteer een datum voor dit rapport in de vervolgkeuzelijst.|  
|**Rapportage-uur**|Selecteer een uur in de vervolgkeuzelijst voor de opgegeven datum waarop dit rapport wordt uitgevoerd. Geldige waarden liggen tussen **00:00 uur** en **23:00 uur**.|  
|**Computerstatus**|Selecteer de computerstatus in de vervolgkeuzelijst waarvoor dit rapport wordt uitgevoerd. Geldige waarden zijn **alle** (computers die zijn ingeschakeld of uitgeschakeld), **op** (computers die zijn ingeschakeld) en **uit** (computers die zijn uitgeschakeld, in de slaap stand of in de sluimer stand). Deze waarden worden alleen geretourneerd voor de gekozen rapportage periode.|  
|**Apparaattype**|Selecteer het type computer waarvoor u een rapport wilt maken in de vervolgkeuzelijst. Geldige waarden zijn **alle** (zowel bureau blad als draag bare computers), **Desktop** (alleen desktop computers) en **laptop** (alleen draag bare computers). Deze waarden worden alleen geretourneerd voor de gekozen rapportage periode.|  
|**Slaapstand mogelijk**|Selecteer in de vervolgkeuzelijst of u computers die naar de slaapstand kunnen overschakelen, in het rapport weergegeven wilt hebben. Geldige waarden zijn **allemaal** (zowel computers die in de slaap stand kunnen worden gezet), Nee (computers die **niet** geschikt zijn voor de slaap stand) en **Ja** (computers die in de slaap stand kunnen worden gezet).|  
|**Ontwaken uit slaapstand mogelijk**|Selecteer in de vervolgkeuzelijst of u computers in het rapport wilt weergeven die uit de slaapstand kunnen ontwaken. Geldige waarden zijn **allemaal** (zowel computers die in de slaap stand kunnen vallen), **Nee** (computers die niet kunnen worden ontwaakt uit de slaap stand) en **Ja** (computers die in de slaap stand kunnen ontwaken).|  
|**Energiebeheerschema**|Selecteer de typen energiebeheerplannen in de vervolgkeuzelijst die u wilt weergeven in het rapport. Geldige waarden zijn **alle** (computers waarop geen energiebeheer schema's zijn toegepast; computers waarop een energiebeheer schema is toegepast; computers die zijn uitgesloten van energie beheer), **niet opgegeven** (computers waarop een energiebeheer schema is toegepast), **gedefinieerd** (computers waarop een energiebeheer schema is toegepast), en **uitgesloten** (computers die zijn uitgesloten van energie beheer).|  
|**Besturingssysteem**|Selecteer in de vervolgkeuzelijst de besturingssystemen die u in het rapport wilt weergeven of selecteer **Alles** om alle besturingssystemen weer te geven.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 Dit rapport heeft geen verborgen parameters die u kunt instellen.  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport bevat koppelingen naar het volgende rapport met meer informatie over het geselecteerde item.  

|Rapportnaam|Details|  
|-----------------|-------------|  
|**Computeractiviteit per computer**|Klik op de naam van een computer om de specifieke activiteit voor die computer te bekijken gedurende een gekozen rapportage periode. Deze activiteiten zijn onder andere **computer aan** (de computer is ingeschakeld?), de **monitor** ingeschakeld (heeft de monitor ingeschakeld?) en de **gebruiker actief** (er is activiteit gedetecteerd van de muis, het toetsen bord of een verbinding met een extern bureau blad van de computer).<br /><br /> Zie [Computer Activity by Computer Report](#BKMK_Comp_Activity_by_computer) in dit onderwerp voor meer informatie.|  

###  <a name="computer-details-report"></a><a name="BKMK_Computer_Details"></a> Rapport Computerdetails  
 Het rapport **Computerdetails** geeft gedetailleerde informatie weer over de energiemogelijkheden, energie-instellingen en energiebeheerschema's die worden toegepast op een opgegeven computer. Dit rapport wordt aangeroepen door het rapport **Computeractiviteit per Computer** , het rapport **Computers met meerdere energiebeheerschema's** , het rapport **Energiemogelijkheden** en het rapport **Details van energie-instellingen** . Het is niet ontworpen om rechtstreeks door de beheerder van de site te worden uitgevoerd.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Computer naam**|Voer de naam van de computer in waarvoor u een rapport wilt.|  
|**Energiemodus**|Selecteer in de vervolgkeuzelijst het type energie-instellingen dat u wilt weergeven in de rapportresultaten. Selecteer **Netstroom** om de energie-instellingen weer te geven die zijn geconfigureerd voor wanneer de computer is aangesloten op netstroom, en **Op accu** om de energie-instellingen weer te geven die zijn geconfigureerd voor wanneer de computer op de accu werkt.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 Dit rapport heeft geen verborgen parameters die u kunt instellen.  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport is niet gekoppeld aan andere energiebeheerrapporten.  

###  <a name="computer-not-reporting-details-report"></a><a name="BKMK_Not_Reporting"></a> Het rapport Computer geeft geen details  
 Het rapport **Computer geeft geen details** geeft een lijst weer met computers in een opgegeven verzameling die geen energieactivititeiten op een opgegeven datum en tijd hebben gerapporteerd. Dit rapport wordt aangeroepen door het **Computer Activity Report** en is niet ontworpen om rechtstreeks door de sitebeheerder te worden uitgevoerd.  

> [!NOTE]  
>  Computers melden energiebeheerinformatie als onderdeel van hun hardware-inventarisatieplanning. Als u denkt dat een computer geen rapporten maakt, dient u eerst te controleren of de computer zijn hardware-inventaris heeft gerapporteerd.  

 Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Naam van verzameling**|Selecteer een verzameling die moet worden gebruikt voor dit rapport in de vervolgkeuzelijst.|  
|**Rapportdatum**|Selecteer een datum voor dit rapport in de vervolgkeuzelijst.|  
|**Rapportage-uur**|Selecteer een uur in de vervolgkeuzelijst voor de opgegeven datum waarop dit rapport wordt uitgevoerd. Geldige waarden liggen tussen **00:00 uur** en **23:00 uur**.|  
|**Apparaattype**|Selecteer het type computer waarvoor u een rapport wilt maken in de vervolgkeuzelijst. Geldige waarden zijn **alle** (zowel bureau blad als draag bare computers), **Desktop** (alleen desktop computers) en **laptop** (alleen draag bare computers). Deze waarden worden alleen geretourneerd voor de gekozen rapportage periode.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 Dit rapport heeft geen verborgen parameters die u kunt instellen.  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport is niet gekoppeld aan andere energiebeheerrapporten.  

###  <a name="computers-excluded"></a><a name="BKMK_Excluded"></a> Computers die zijn uitgesloten  
 Het rapport **uitgesloten computers** geeft een lijst weer van computers in een opgegeven verzameling die zijn uitgesloten van Configuration Manager energie beheer.  

 Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Verzameling**|Selecteer een verzameling voor dit rapport in de vervolgkeuzelijst.|  
|**Reden**|Selecteer in de vervolgkeuzelijst de reden waarom de computers zijn uitgesloten van energiebeheer. U kunt **alle** (alle uitgesloten computers), **uitgesloten door de beheerder** (alleen computers die zijn uitgesloten door een gebruiker met beheerders rechten), en **uitgesloten door gebruiker** (alleen computers die zijn uitgesloten door een gebruiker van software Center) weer geven.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 Dit rapport heeft geen verborgen parameters die u kunt instellen.  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport bevat koppelingen naar het volgende rapport met meer informatie over het geselecteerde item.  

|Rapportnaam|Details|  
|-----------------|-------------|  
|**Energiedetails van een computer**|Klik op de naam van een computer om de energiemogelijkheden, energie-instellingen en toegepaste energiebeheerschema's voor de geselecteerde computer te zien.<br /><br /> Zie [Computer Details Report](#BKMK_Computer_Details) in dit onderwerp voor meer informatie.|  

###  <a name="computers-with-multiple-power-plans"></a><a name="BKMK_Multiple"></a> Computers met meerdere energiebeheerschema's  
 Het rapport **Computers met meerdere energiebeheerschema's** geeft een lijst weer met computers die lid zijn van meerdere verzamelingen, die elk verschillende energiebeheerschema's toepassen. Voor elke computer met mogelijk conflicterende energie-instellingen geeft het rapport de computernaam en energiebeheerschema's weer die voor elke verzameling worden toegepast waarvan de computer lid is.  

> [!IMPORTANT]  
>  Als een computer lid is van meerdere verzamelingen, waarbij elke verzameling verschillende energiebeheer schema's heeft, wordt het minst beperkende energiebeheer schema toegepast.  
>   
>  Als een computer lid is van meerdere verzamelingen, waarbij elke verzameling verschillende Ontwaak tijden heeft, wordt de tijd gebruikt die het dichtst bij middernacht ligt.  

 Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Naam van verzameling**|Selecteer een verzameling voor dit rapport in de vervolgkeuzelijst.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 Dit rapport heeft geen verborgen parameters die u kunt instellen.  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport bevat koppelingen naar het volgende rapport met meer informatie over het geselecteerde item.  

|Rapportnaam|Details|  
|-----------------|-------------|  
|**Energiedetails van een computer**|Klik op de naam van een computer om de energiemogelijkheden, energie-instellingen en toegepaste energiebeheerschema's voor de geselecteerde computer te zien.<br /><br /> Zie [Computer Details Report](#BKMK_Computer_Details) in dit onderwerp voor meer informatie.|  

###  <a name="energy-consumption-report"></a><a name="BKMK_Consumption"></a> Het rapport Energieverbruik  
 Het rapport **Energieverbruik** geeft de volgende informatie weer:  

- Een grafiek met het totale maandelijkse energieverbruik van computers in kilowatt per uur (kWh) in de opgegeven verzameling voor de opgegeven periode.  

- Een grafiek met het gemiddelde energieverbruik in kilowatt per uur (kWh) van elke computer in de opgegeven verzameling voor de opgegeven periode.  

- Een tabel met het totale maandelijkse energieverbruik in kilowatt per uur (kWh) en het gemiddelde energieverbruik van computers in de opgegeven verzameling voor de opgegeven periode.  

  Aan de hand van deze informatie kunt u inzicht krijgen in de energieverbruiktrends in uw omgeving. Na het toepassen van een energiebeheerschema op computers in de geselecteerde verzameling, zou het energieverbruik van computers moeten afnemen.  

> [!NOTE]  
>  Als u leden aan de verzameling toevoegt of eruit verwijdert nadat u een energiebeheerschema hebt toegepast, heeft dit invloed op de resultaten in het rapport **Energieverbruik** en kan het lastiger zijn de resultaten van de bewaking- en planningfase te vergelijken met de afdwingingsfase.  

 Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Begindatum**|Selecteer een begindatum voor dit rapport in de vervolgkeuzelijst.|  
|**Eind datum**|Selecteer een einddatum voor dit rapport in de vervolgkeuzelijst.|  
|**Naam van verzameling**|Selecteer een verzameling voor dit rapport in de vervolgkeuzelijst.|  
|**Apparaattype**|Selecteer het type computer waarvoor u een rapport wilt maken in de vervolgkeuzelijst. Geldige waarden zijn **alle** (zowel bureau blad als draag bare computers), **Desktop** (alleen desktop computers) en **laptop** (alleen draag bare computers). Deze waarden worden alleen geretourneerd voor de gekozen rapportage periode.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 De volgende verborgen parameters kunnen eventueel worden opgegeven om het gedrag van dit rapport te wijzigen.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Desktopcomputer aan**|Geef het energieverbruik van een desktopcomputer op wanneer deze is ingeschakeld. De standaardwaarde is **0,07** kW per uur.|  
|**Laptopcomputer aan**|Geef het energieverbruik van een draagbare computer op wanneer deze is ingeschakeld. De standaardwaarde is **0,02** kW per uur.|  
|**Desktopcomputer slaapstand**|Geef het energieverbruik van een desktopcomputer op die zich in de slaapstand bevindt. De standaardwaarde is **0,003** kW per uur.|  
|**Laptopcomputer slaapstand**|Geef het energieverbruik van een draagbare computer op die zich in de slaapstand bevindt. De standaardwaarde is **0,001** kW per uur.|  
|**Desktopcomputer uit**|Geef het energieverbruik van een desktopcomputer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Laptopcomputer uit**|Geef het energieverbruik van een draagbare computer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Desktopbeeldscherm aan**|Geef het energieverbruik van een desktopbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0,028** kW per uur.|  
|**Laptopbeeldscherm aan**|Geef het energieverbruik van een draagbaar computerbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0** kW per uur.|  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport is niet gekoppeld aan andere energiebeheerrapporten.  

###  <a name="energy-consumption-by-day-report"></a><a name="BKMK_Consumption_by_Day"></a> Het rapport Energieverbruik per dag  
 Het rapport **Energieverbruik per dag** geeft de volgende informatie weer:  

- Een grafiek met het totale dagelijkse energieverbruik van computers in kilowatt per uur (kWh) in de opgegeven verzameling voor de afgelopen 31 dagen.  

- Een grafiek met het gemiddelde dagelijkse energieverbruik in kilowatt per uur (kWh) van elke computer in de opgegeven verzameling voor de afgelopen 31 dagen.  

- Een tabel met het totale dagelijkse energieverbruik in kilowatt per uur (kWh) en het gemiddelde dagelijkse energieverbruik van computers in de opgegeven verzameling voor de afgelopen 31 dagen.  

  Aan de hand van deze informatie kunt u inzicht krijgen in de energieverbruiktrends in uw omgeving. Na het toepassen van een energiebeheerschema op computers in de geselecteerde verzameling, zou het energieverbruik van computers moeten afnemen.  

> [!NOTE]  
>  Als u leden aan de verzameling toevoegt of eruit verwijdert nadat u een energiebeheerschema hebt toegepast, heeft dit invloed op de resultaten in het rapport **Energieverbruik** en kan het lastiger zijn de resultaten van de bewaking- en planningfase te vergelijken met de afdwingingsfase.  

 Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Verzameling**|Selecteer een verzameling voor dit rapport in de vervolgkeuzelijst.|  
|**Apparaattype**|Selecteer het type computer waarvoor u een rapport wilt maken in de vervolgkeuzelijst. Geldige waarden zijn **alle** (zowel bureau blad als draag bare computers), **Desktop** (alleen desktop computers) en **laptop** (alleen draag bare computers). Deze waarden worden alleen geretourneerd voor de gekozen rapportage periode.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 De volgende verborgen parameters kunnen eventueel worden opgegeven om het gedrag van dit rapport te wijzigen.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Desktopcomputer aan**|Geef het energieverbruik van een desktopcomputer op wanneer deze is ingeschakeld. De standaardwaarde is **0,07** kW per uur.|  
|**Laptopcomputer aan**|Geef het energieverbruik van een draagbare computer op wanneer deze is ingeschakeld. De standaardwaarde is **0,02** kW per uur.|  
|**Desktopcomputer slaapstand**|Geef het energieverbruik van een desktopcomputer op die zich in de slaapstand bevindt. De standaardwaarde is **0,003** kW per uur.|  
|**Laptopcomputer slaapstand**|Geef het energieverbruik van een draagbare computer op die zich in de slaapstand bevindt. De standaardwaarde is **0,001** kW per uur.|  
|**Desktopcomputer uit**|Geef het energieverbruik van een desktopcomputer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Laptopcomputer uit**|Geef het energieverbruik van een draagbare computer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Desktopbeeldscherm aan**|Geef het energieverbruik van een desktopbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0,028** kW per uur.|  
|**Laptopbeeldscherm aan**|Geef het energieverbruik van een draagbaar computerbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0** kW per uur.|  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport is niet gekoppeld aan andere energiebeheerrapporten.  

###  <a name="energy-cost-report"></a><a name="BKMK_Cost"></a> Het rapport Energiekosten  
 Het rapport **Energiekosten** geeft de volgende informatie weer:  

- Een grafiek met de totale maandelijkse energiekosten voor computers in de opgegeven verzameling voor een opgegeven periode.  

- Een grafiek met de gemiddelde maandelijkse energiekosten per computer in de opgegeven verzameling voor de opgegeven periode.  

- Een tabel waarin de totale maandelijkse energiekosten en de gemiddelde maandelijkse energiekosten voor computers in de opgegeven verzameling voor de afgelopen 31 dagen.  

  Aan de hand van deze informatie kunt u inzicht krijgen in de energiekostentrends in uw omgeving. Na het toepassen van een energiebeheerschema op computers in de geselecteerde verzameling, zouden de energiekosten van computers moeten afnemen.  

  Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Begindatum**|Selecteer een begindatum voor dit rapport in de vervolgkeuzelijst.|  
|**Eind datum**|Selecteer een einddatum voor dit rapport in de vervolgkeuzelijst.|  
|**Kosten van kWh**|Geef de kosten per kWh elektriciteit op. De standaardwaarde is **0,09**.<br /><br /> U kunt de valuta-eenheid die in dit rapport wordt gebruikt aanpassen in de sectie met verborgen parameters.|  
|**Naam van verzameling**|Selecteer een verzameling die moet worden gebruikt voor dit rapport in de vervolgkeuzelijst.|  
|**Apparaattype**|Selecteer het type computer waarvoor u een rapport wilt maken in de vervolgkeuzelijst. Geldige waarden zijn **alle** (zowel bureau blad als draag bare computers), **Desktop** (alleen desktop computers) en **laptop** (alleen draag bare computers). Deze waarden worden alleen geretourneerd voor de gekozen rapportage periode.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 De volgende verborgen parameters kunnen eventueel worden opgegeven om het gedrag van dit rapport te wijzigen.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Desktopcomputer aan**|Geef het energieverbruik van een desktopcomputer op wanneer deze is ingeschakeld. De standaardwaarde is **0,07** kW per uur.|  
|**Laptopcomputer aan**|Geef het energieverbruik van een draagbare computer op wanneer deze is ingeschakeld. De standaardwaarde is **0,02** kW per uur.|  
|**Desktopcomputer slaapstand**|Geef het energieverbruik van een desktopcomputer op die zich in de slaapstand bevindt. De standaardwaarde is **0,003** kW per uur.|  
|**Laptopcomputer slaapstand**|Geef het energieverbruik van een draagbare computer op die zich in de slaapstand bevindt. De standaardwaarde is **0,001** kW per uur.|  
|**Desktopcomputer uit**|Geef het energieverbruik van een desktopcomputer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Laptopcomputer uit**|Geef het energieverbruik van een draagbare computer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Desktopbeeldscherm aan**|Geef het energieverbruik van een desktopbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0,028** kW per uur.|  
|**Laptopbeeldscherm aan**|Geef het energieverbruik van een draagbaar computerbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Valuta**|Geef het valutalabel op dat voor dit rapport moet worden gebruikt. De standaardwaarde is **USD ($)**.|  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport is niet gekoppeld aan andere energiebeheerrapporten.  

###  <a name="energy-cost-by-day-report"></a><a name="BKMK_Cost_by_Day"></a> Het rapport Energiekosten per dag  
 Het rapport **Energiekosten per dag** geeft de volgende informatie weer:  

- Een grafiek met de totale dagelijkse energiekosten voor computers in de opgegeven verzameling voor de afgelopen 31 dagen.  

- Een grafiek met de gemiddelde dagelijkse energiekosten per computer in de opgegeven verzameling voor de afgelopen 31 dagen.  

- Een tabel met de totale dagelijkse energiekosten en de gemiddelde dagelijkse energiekosten voor computers in de opgegeven verzameling voor de afgelopen 31 dagen.  

  Aan de hand van deze informatie kunt u inzicht krijgen in de energiekostentrends in uw omgeving. Na het toepassen van een energiebeheerschema op computers in de geselecteerde verzameling, zouden de energiekosten van computers moeten afnemen.  

  Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Naam van verzameling**|Selecteer een verzameling die moet worden gebruikt voor dit rapport in de vervolgkeuzelijst.|  
|**Apparaattype**|Selecteer het type computer waarvoor u een rapport wilt maken in de vervolgkeuzelijst. Geldige waarden zijn **alle** (zowel bureau blad als draag bare computers), **Desktop** (alleen desktop computers) en **laptop** (alleen draag bare computers). Deze waarden worden alleen geretourneerd voor de gekozen rapportage periode.|  
|**Kosten van kWh**|Geef de kosten per kWh elektriciteit op. De standaardwaarde is **0,09**.<br /><br /> U kunt de valuta-eenheid die in dit rapport wordt gebruikt aanpassen in de sectie met verborgen parameters.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 De volgende verborgen parameters kunnen eventueel worden opgegeven om het gedrag van dit rapport te wijzigen.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Desktopcomputer aan**|Geef het energieverbruik van een desktopcomputer op wanneer deze is ingeschakeld. De standaardwaarde is **0,07** kW per uur.|  
|**Laptopcomputer aan**|Geef het energieverbruik van een draagbare computer op wanneer deze is ingeschakeld. De standaardwaarde is **0,02** kW per uur.|  
|**Desktopcomputer slaapstand**|Geef het energieverbruik van een desktopcomputer op die zich in de slaapstand bevindt. De standaardwaarde is **0,003** kW per uur.|  
|**Laptopcomputer slaapstand**|Geef het energieverbruik van een draagbare computer op die zich in de slaapstand bevindt. De standaardwaarde is **0,001** kW per uur.|  
|**Desktopcomputer uit**|Geef het energieverbruik van een desktopcomputer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Laptopcomputer uit**|Geef het energieverbruik van een draagbare computer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Desktopbeeldscherm aan**|Geef het energieverbruik van een desktopbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0,028** kW per uur.|  
|**Laptopbeeldscherm aan**|Geef het energieverbruik van een draagbaar computerbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Valuta**|Geef het valutalabel op dat voor dit rapport moet worden gebruikt. De standaardwaarde is **USD ($)**.|  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport is niet gekoppeld aan andere energiebeheerrapporten.  

###  <a name="environmental-impact-report"></a><a name="BKMK_Environmental_Impact"></a> Het rapport Uitwerking op het milieu  
 Het rapport **Uitwerking op het milieu** geeft de volgende informatie weer:  

- Een grafiek met de totale maandelijkse CO2 gegenereerd (in ton) voor computers in de opgegeven verzameling voor de opgegeven tijds periode.  

- Een grafiek met de gemiddelde maandelijkse CO2 gegenereerd (in ton) voor elke computer in de opgegeven verzameling voor de opgegeven tijds periode.  

- Een tabel met de totale maandelijkse CO2 gegenereerd en de gemiddelde maandelijkse CO2 gegenereerd voor computers in de opgegeven verzameling voor een opgegeven periode.  

  Het rapport **milieu-impact** berekent de hoeveelheid CO2 die is gegenereerd (in ton) door gebruik te maken van de tijd dat een computer of monitor is ingeschakeld in een periode van 24 uur.  

  Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Begindatum van rapport**|Selecteer een begindatum voor dit rapport in de vervolgkeuzelijst.|  
|**Einddatum van rapport**|Selecteer een einddatum voor dit rapport in de vervolgkeuzelijst.|  
|**Naam van verzameling**|Selecteer een verzameling voor dit rapport in de vervolgkeuzelijst.|  
|**Apparaattype**|Selecteer het type computer waarvoor u een rapport wilt maken in de vervolgkeuzelijst. Geldige waarden zijn **alle** (zowel bureau blad als draag bare computers), **Desktop** (alleen desktop computers) en **laptop** (alleen draag bare computers). Deze waarden worden alleen geretourneerd voor de gekozen rapportage periode.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 De volgende verborgen parameters kunnen eventueel worden opgegeven om het gedrag van dit rapport te wijzigen.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Desktopcomputer aan**|Geef het energieverbruik van een desktopcomputer op wanneer deze is ingeschakeld. De standaardwaarde is **0,07** kW per uur.|  
|**Laptopcomputer aan**|Geef het energieverbruik van een draagbare computer op wanneer deze is ingeschakeld. De standaardwaarde is **0,02** kW per uur.|  
|**Desktopcomputer slaapstand**|Geef het energieverbruik van een desktopcomputer op die zich in de slaapstand bevindt. De standaardwaarde is **0,003** kW per uur.|  
|**Laptopcomputer slaapstand**|Geef het energieverbruik van een draagbare computer op die zich in de slaapstand bevindt. De standaardwaarde is **0,001** kW per uur.|  
|**Desktopcomputer uit**|Geef het energieverbruik van een desktopcomputer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Laptopcomputer uit**|Geef het energieverbruik van een draagbare computer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Desktopbeeldscherm aan**|Geef het energieverbruik van een desktopbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0,028** kW per uur.|  
|**Laptopbeeldscherm aan**|Geef het energieverbruik van een draagbaar computerbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0** kW per uur.|  
|**Koolstoffactor (ton/kWh)** (CO2-mix)|Geef de koolstoffactorwaarde (in ton/kWh) op die u doorgaans bij uw energiebedrijf kunt aanvragen. De standaardwaarde is **0,0015** ton per kWh.|  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport is niet gekoppeld aan andere energiebeheerrapporten.  

###  <a name="environmental-impact-by-day-report"></a><a name="BKMK_Environmental_Impact_by_Day"></a> Het rapport Uitwerking op het milieu op dag  
 Het rapport **Uitwerking op het milieu op dag** geeft de volgende informatie weer:  

- Een grafiek met de totale dagelijkse CO2 die is gegenereerd (in ton) voor computers in de opgegeven verzameling voor de afgelopen 31 dagen.  

- Een grafiek met de gemiddelde dagelijkse gegenereerde CO2 (in ton) voor elke computer in de opgegeven verzameling voor de afgelopen 31 dagen.  

- Een tabel met de totale dagelijkse CO2 gegenereerd en de gemiddelde dagelijkse CO2 gegenereerd voor computers in de opgegeven verzameling voor de afgelopen 31 dagen.  

  Het rapport **milieu-impact per dag** berekent de hoeveelheid CO2 die is gegenereerd (in ton) door gebruik te maken van de tijd dat een computer of monitor is ingeschakeld in een periode van 24 uur.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Naam van verzameling**|Selecteer een verzameling voor dit rapport in de vervolgkeuzelijst.|  
|**Apparaattype**|Selecteer het type computer waarvoor u een rapport wilt maken in de vervolgkeuzelijst. Geldige waarden zijn **alle** (zowel bureau blad als draag bare computers), **Desktop** (alleen desktop computers) en **laptop** (alleen draag bare computers). Deze waarden worden alleen geretourneerd voor de gekozen rapportage periode.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 De volgende verborgen parameters kunnen eventueel worden opgegeven om het gedrag van dit rapport te wijzigen.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Desktopcomputer aan**|Geef het energieverbruik van een desktopcomputer op wanneer deze is ingeschakeld. De standaardwaarde is **0,07** .|  
|**Laptopcomputer aan**|Geef het energieverbruik van een draagbare computer op wanneer deze is ingeschakeld. De standaardwaarde is **0,02** kWh.|  
|**Desktopcomputer uit**|Geef het energieverbruik van een desktopcomputer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kWh.|  
|**Laptopcomputer uit**|Geef het energieverbruik van een draagbare computer op wanneer deze is uitgeschakeld. De standaardwaarde is **0** kWh.|  
|**Desktopcomputer slaapstand**|Geef het energieverbruik van een desktopcomputer op die zich in de slaapstand bevindt. De standaardwaarde is **0,003** kWh.|  
|**Laptopcomputer slaapstand**|Geef het energieverbruik van een draagbare computer op die zich in de slaapstand bevindt. De standaardwaarde is **0,001** kWh.|  
|**Desktopbeeldscherm aan**|Geef het energieverbruik van een desktopbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0,028** kWh.|  
|**Laptopbeeldscherm aan**|Geef het energieverbruik van een draagbaar computerbeeldscherm op wanneer dit is ingeschakeld. De standaardwaarde is **0** kWh.|  
|**Koolstoffactor (ton/kWh)** (CO2-mix)|Geef een kooldioxidefactorwaarde (in ton/kWh) op die u doorgaans bij uw energiebedrijf kunt aanvragen. De standaardwaarde is **0,0015** ton per kWh.|  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport is niet gekoppeld aan andere energiebeheerrapporten.  

###  <a name="insomnia-computer-details-report"></a><a name="BKMK_Insomnia_Computer_Details"></a> Rapport Details van slapeloosheid computer  
 Het rapport **Details van slapeloosheid computer** geeft een lijst met computers weer die om een bepaalde reden niet binnen een opgegeven periode in de slaapstand of sluimerstand zijn gegaan. Dit rapport wordt aangeroepen door het **slapeloosheidsrapport** en is niet ontworpen om rechtstreeks door de sitebeheerder te worden uitgevoerd.  

 Het **slapeloosheidsrapport** geeft voor computers **Slaapstand niet mogelijk** weer wanneer deze computers niet kunnen overgaan op de slaapstand en tijdens het gehele opgegeven rapportinterval ingeschakeld zijn geweest. Het rapport geeft voor computers **Sluimerstand niet mogelijk** weer wanneer deze computers niet kunnen overgaan op de sluimerstand en tijdens het gehele opgegeven rapportinterval ingeschakeld zijn geweest.  

> [!NOTE]  
>  Energiebeheer kan alleen oorzaken verzamelen die hebben voorkomen dat computers met Windows 7 of Windows Server 2008 R2 naar de slaapstand of sluimerstand zijn overgeschakeld.  

 Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Naam van verzameling**|Selecteer een verzameling die moet worden gebruikt voor dit rapport in de vervolgkeuzelijst.|  
|**Rapportinterval (dagen)**|Geef het aantal dagen aan waarover moet worden gerapporteerd. De standaardwaarde is **7** dagen.|  
|**Oorzaak van slapeloosheid**|Selecteer in de vervolgkeuzelijst een van de oorzaken die kunnen voorkomen dat computers overschakelen naar de slaapstand of sluimerstand.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 Dit rapport heeft geen verborgen parameters die u kunt instellen.  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport bevat koppelingen naar het volgende rapport met meer informatie over het geselecteerde item.  

|Rapportnaam|Details|  
|-----------------|-------------|  
|**Computerdetails**|Klik op de koppeling **Klik voor gedetailleerde informatie** om de energiemogelijkheden, energie-instellingen en toegepaste energiebeheerschema's voor de geselecteerde computer te zien.<br /><br /> Zie [Computer Details Report](#BKMK_Computer_Details) in dit onderwerp voor meer informatie.|  

###  <a name="insomnia-report"></a><a name="BKMK_Insomnia"></a> Insomnia report  
 Het **Slapeloosheidsrapport** geeft een lijst met algemene oorzaken weer die voorkomen dat computers overschakelen naar de slaapstand of sluimerstand, evenals het aantal computers dat hierdoor gedurende een bepaalde periode is getroffen. Er zijn enkele oorzaken die mogelijk voorkomen dat een computer overschakelt naar de slaapstand of sluimerstand, zoals een proces dat wordt uitgevoerd op de computer, een geopende extern-bureaubladsessie of het feit dat een computer niet in staat is over te schakelen naar de slaapstand of sluimerstand. U kunt vanuit dit rapport het rapport **Details van slapeloosheid computer** openen. Dit geeft een lijst met computers weer die gedurende een bepaalde periode zijn getroffen door een oorzaak die overschakelen naar de slaap- of sluimerstand heeft verhinderd.  

 Het slapeloosheidsrapport geeft voor computers **Slaapstand niet mogelijk** weer wanneer deze computers niet kunnen overschakelen naar de slaapstand en tijdens het gehele opgegeven rapportinterval ingeschakeld zijn geweest. Het rapport geeft voor computers **Sluimerstand niet mogelijk** weer wanneer deze computers niet kunnen overgaan op de sluimerstand en tijdens het gehele opgegeven rapportinterval ingeschakeld zijn geweest.  

> [!NOTE]  
>  Energiebeheer kan alleen oorzaken verzamelen die hebben voorkomen dat computers met Windows 7 of Windows Server 2008 R2 naar de slaapstand of sluimerstand zijn overgeschakeld.  

 Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Naam van verzameling**|Selecteer een verzameling die moet worden gebruikt voor dit rapport in de vervolgkeuzelijst.|  
|**Rapportinterval (dagen)**|Geef het aantal dagen aan waarover moet worden gerapporteerd. De standaardwaarde is **7** dagen. De maximumwaarde is **365** dagen. Geef **0** op om het rapport voor vandaag uit te voeren.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 Dit rapport heeft geen verborgen parameters die u kunt instellen.  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport bevat koppelingen naar het volgende rapport met meer informatie over het geselecteerde item.  

|Rapportnaam|Details|  
|-----------------|-------------|  
|**Details van slapeloosheid computer**|Klik op een getal in de kolom **Betreffende computers** voor een lijst met computers die vanwege de geselecteerde oorzaak niet naar de slaapstand of sluimerstand konden overschakelen.<br /><br /> Zie [Insomnia Computer Details Report](#BKMK_Insomnia_Computer_Details) in dit onderwerp voor meer informatie.|  

###  <a name="power-capabilities-report"></a><a name="BKMK_Capabilites"></a> Het rapport Stroomvoorzieningsmogelijkheden  
 Het rapport **Stroomvoorzieningsmogelijkheden** geeft de hardwaremogelijkheden voor energiebeheer van computers in de opgegeven verzameling weer. Dit rapport wordt doorgaans gebruikt in de bewakingsfase van energiebeheer om te bepalen wat de mogelijkheden voor energiebeheer van computers in uw organisatie zijn. De informatie die wordt weergegeven in het rapport kan vervolgens worden gebruikt om verzamelingen computers te maken en energiebeheerschema's toe te passen, of om computers van energiebeheer uit te sluiten. De mogelijkheden voor energiebeheer die in dit rapport worden weergegeven, zijn:  

- **Slaapstand mogelijk** : geeft aan of de computer de mogelijkheid heeft over te schakelen naar de slaapstand als deze hiervoor is geconfigureerd.  

- **Sluimerstand mogelijk** : geeft aan of de computer de mogelijkheid heeft om over te schakelen naar de sluimerstand als deze hiervoor is geconfigureerd.  

- **Ontwaken uit slaapstand** : geeft aan of de computer uit de slaapstand kan ontwaken als de computer hiervoor is geconfigureerd.  

- **Ontwaken uit sluimerstand** : geeft aan of de computer uit de sluimerstand kan ontwaken als de computer hiervoor is geconfigureerd.  

  De waarden die worden gemeld door het rapport **Stroomvoorzieningsmogelijkheden** geven de slaapstand- en sluimerstandmogelijkheden weer van computers, zoals gemeld door Windows. De gerapporteerde waarden geven echter geen gevallen weer waarin Windows- of BIOS-instellingen hebben voorkomen dat deze functies werken.  

  Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Verzameling**|Selecteer een verzameling voor dit rapport in de vervolgkeuzelijst.|  
|**Filter weergeven**|Selecteer in de vervolg keuzelijst **niet ondersteund** om alleen computers in de opgegeven verzameling weer te geven die niet geschikt zijn voor de slaap stand, sluimer stand, ontwaken uit slaap stand of ontwaken uit sluimer stand. Selecteer **alles weer geven** om alle computers in de opgegeven verzameling weer te geven.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 Dit rapport heeft geen verborgen parameters die u kunt instellen.  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport bevat koppelingen naar het volgende rapport met meer informatie over het geselecteerde item.  

|Rapportnaam|Details|  
|-----------------|-------------|  
|**Computerdetails**|Klik op de naam van een computer om de energiemogelijkheden, energie-instellingen en toegepaste energiebeheerschema's voor de geselecteerde computer te zien.<br /><br /> Zie [Computer Details Report](#BKMK_Computer_Details) in dit onderwerp voor meer informatie.|  

###  <a name="power-settings-report"></a><a name="BKMK_Settings"></a> Het rapport Energie-instellingen  
 Het rapport **Energie-instellingen** bevat een samengevoegde lijst met energie-instellingen die door computers in de opgegeven verzameling worden gebruikt. Voor elke energie-instelling worden de mogelijke energiemodi, -waarden en -eenheden weergegeven, samen met een telling van het aantal computers dat deze waarden gebruikt. Dit rapport kan worden gebruikt tijdens de bewakingsfase van energiebeheer om de beheerder beter inzicht te geven in de bestaande energie-instellingen die door computers op de locatie worden gebruikt en om te helpen bij het plannen van optimale energie-instellingen die in een energiebeheerschema kunnen worden toegepast. Het rapport is ook nuttig bij het oplossen van problemen en om te controleren of de energie-instellingen juist zijn toegepast.  

> [!NOTE]  
>  De instellingen die worden weergegeven, zijn tijdens een hardware-inventarisatie bij clientcomputers verzameld. Afhankelijk van het tijdstip waarop de hardware-inventarisatie wordt uitgevoerd, worden er mogelijk instellingen van een toegepast energiebeheerschema voor piekuren of niet-piekuren verzameld.  

 Gebruik de volgende parameters voor het configureren van dit rapport.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Naam van verzameling**|Selecteer een verzameling voor dit rapport in de vervolgkeuzelijst.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 De volgende verborgen parameters kunnen eventueel worden opgegeven om het gedrag van dit rapport te wijzigen.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Geef het aantal talen op waarin u namen van energie-instellingen weergeven wilt hebben die door de clientcomputers worden gerapporteerd. Als u alleen informatie in de populairste taal weergegeven wilt hebben, laat de standaardwaarde **1**dan ongewijzigd staan. Als u alle talen wilt weergeven, stelt u deze waarde in op **0**.|  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport bevat koppelingen naar het volgende rapport met meer informatie over het geselecteerde item.  

|Rapportnaam|Details|  
|-----------------|-------------|  
|**Details van energie-instellingen**|Klik op het aantal computers in de kolom **Computers** voor een overzicht van alle computers die gebruikmaken van de instellingen voor energiebeheer in die rij.<br /><br /> Zie [Power Settings Details Report](#BKMK_Settings_Details) in dit onderwerp voor meer informatie.|  

###  <a name="power-settings-details-report"></a><a name="BKMK_Settings_Details"></a> Power Settings Details report  
 Het rapport **Details van energie-instellingen** bevat meer informatie over computers die zijn geselecteerd in het rapport **Energie-instellingen** . Dit rapport wordt aangeroepen door het rapport **Energie-instellingen** en is niet ontworpen om rechtstreeks door de sitebeheerder te worden uitgevoerd.  

#### <a name="required-report-parameters"></a>Vereiste rapportparameters  
 De volgende parameters moeten worden opgegeven om dit rapport uit te voeren.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**Verzameling**|Selecteer een verzameling die moet worden gebruikt voor dit rapport in de vervolgkeuzelijst.|  
|**GUID van energie-instelling**|Selecteer in de vervolgkeuzelijst de GUID van de energie-instelling waarover u een rapport wilt ontvangen. Zie [beschik bare energiebeheer schema-instellingen](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) in het onderwerp [procedures voor het maken en Toep assen van energie schema's](../../../../core/clients/manage/power/create-and-apply-power-plans.md)voor een lijst met alle energie-instellingen en het gebruik ervan.|  
|**Energie modus**|Selecteer in de vervolgkeuzelijst het type energie-instellingen dat u wilt weergeven in de rapportresultaten. Selecteer **Netstroom** om de energie-instellingen weer te geven die zijn geconfigureerd voor wanneer de computer is aangesloten op netstroom, en **Op accu** om de energie-instellingen weer te geven die zijn geconfigureerd voor wanneer de computer op de accu werkt.|  
|**Instellingenindex**|Selecteer in de vervolgkeuzelijst de waarde voor de naam van de geselecteerde energie-instelling waarover u een rapport wilt ontvangen. Bijvoorbeeld, als u alle computers wilt weergeven waarvoor de instelling **Vaste schijf uitschakelen na** is ingesteld op **10** minuten, selecteert u **Vaste schijf uitschakelen na** voor **Naam energie-instelling** en **10** voor **Instellingenindex**.|  

#### <a name="hidden-report-parameters"></a>Verborgen rapportparameters  
 De volgende verborgen parameters kunnen eventueel worden opgegeven om het gedrag van dit rapport te wijzigen.  

|Parameternaam|Beschrijving|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Geef het aantal talen op waarin u namen van energie-instellingen weergeven wilt hebben die door de clientcomputers worden gerapporteerd. Als u alleen informatie in de populairste taal weergegeven wilt hebben, laat de standaardwaarde **1**dan ongewijzigd staan. Als u alle talen wilt weergeven, stelt u deze waarde in op **0**.|  

#### <a name="report-links"></a>Rapportkoppelingen  
 Dit rapport bevat koppelingen naar het volgende rapport met meer informatie over het geselecteerde item.  

|Rapportnaam|Details|  
|-----------------|-------------|  
|**Computerdetails**|Klik op de naam van een computer om de energiemogelijkheden, energie-instellingen en toegepaste energiebeheerschema's voor de geselecteerde computer te zien.<br /><br /> Zie [Computer Details Report](#BKMK_Computer_Details) in dit onderwerp voor meer informatie.|  

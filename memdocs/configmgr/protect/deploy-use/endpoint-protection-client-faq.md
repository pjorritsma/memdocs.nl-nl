---
title: Veelgestelde vragen over Endpoint Protection-client
titleSuffix: Configuration Manager
description: Krijg antwoorden op veelgestelde vragen over Windows Defender en Endpoint Protection.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3b206c1556c2e9550ade5c2322acd65ad2b19412
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906834"
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Veelgestelde vragen over Endpoint Protection-client

*Van toepassing op: Configuration Manager (huidige vertakking)*


Deze veelgestelde vragen zijn voor computergebruikers waarvan de IT-beheerder Windows Defender of Endpoint Protection heeft geïmplementeerd op de beheerde computer. De inhoud is mogelijk niet van toepassing op andere antimalware-software. Micro soft System Center Endpoint Protection beheert Windows Defender in Windows 10. Het kan ook de Endpoint Protection-client implementeren en beheren op computers vóór Windows 10. In dit artikel wordt Windows Defender beschreven, maar de informatie is ook van toepassing op Endpoint Protection.  

-   [Waarom heb ik software tegen virussen en spyware nodig?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [Hoe weet ik of mijn computer is geïnfecteerd met schadelijke software?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [Hoe kan ik de versie van Windows Defender vinden?](#how-can-i-find-the-version-of-windows-defender)
-   [Wat moet ik doen als schadelijke software op mijn computer wordt gedetecteerd door Windows Defender of Endpoint Protection?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer)  
-   [Wat is een virus?](#what-is-a-virus)  
-   [Wat is spyware?](#what-is-spyware)  
-   [Wat is het verschil tussen virussen, spyware en andere mogelijk schadelijke software?](#whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [Waar komen virussen, spyware en andere mogelijk ongewenste software vandaan?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [Kan ik schadelijke software krijgen zonder het te weten?](#can-i-get-malicious-software-without-knowing-it)  
-   [Waarom is het belangrijk om licentieovereenkomsten te lezen voordat u software installeert?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [Wat is het verschil tussen Endpoint Protection en Windows Defender?](#whats-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Waarom detecteert Windows Defender geen cookies?](#why-doesnt-windows-defender-detect-cookies)  
-   [Hoe voorkom ik dat schadelijke software wordt geïnstalleerd?](#how-can-i-prevent-malware)  
-   [Wat zijn virus- en spywaredefinities?](#what-are-virus-and-spyware-definitions)  
-   [Hoe houd ik virus-en spywaredefinities up-to-date?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [Hoe kan ik items verwijderen of herstellen die door Windows Defender of Endpoint Protection in quarantaine zijn geplaatst?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [Wat is realtime-beveiliging?](#what-is-real-time-protection)  
-   [Hoe weet ik of Windows Defender of Endpoint Protection op mijn computer wordt uitgevoerd?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [Hoe kan ik waarschuwingen door Windows Defender of Endpoint Protection instellen?](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a>Waarom heb ik software tegen virussen en spyware nodig?  

 Het is essentieel dat u ervoor zorgt dat op uw computer software wordt uitgevoerd die beschermt tegen schadelijke software. Schadelijke software, inclusief virussen, spyware of andere mogelijk ongewenste software, kan op elk moment dat u verbinding hebt met internet proberen zich op uw computer te installeren. Uw computer kan ook worden geïnfecteerd wanneer u een programma installeert vanaf een cd, dvd of andere verwisselbare media. Schadelijke software kan ook zo worden geprogrammeerd dat deze niet tijdens de installatie, maar op een onverwacht moment daarna wordt uitgevoerd.  

 Windows Defender of Endpoint Protection biedt drie manieren om te voorkomen dat schadelijke software de computer infecteert:  

-   **Met realtime** -beveiliging-real-time beveiliging kan Windows Defender de computer altijd controleren en wordt u gewaarschuwd wanneer schadelijke software, inclusief virussen, spyware of andere mogelijk ongewenste software, probeert zichzelf te installeren of uit te voeren op uw computer. Windows Defender onderbreekt vervolgens de software, zodat u de aanbeveling met betrekking tot de software kunt volgen of alternatieve actie kunt ondernemen.

-   **Scan opties** : u kunt Windows Defender gebruiken om te scannen op mogelijke bedreigingen, zoals virussen, spyware en andere schadelijke software waarmee uw computer risico loopt. U kunt ook regelmatige scans plannen en schadelijke software verwijderen die tijdens een scan wordt gedetecteerd.  

-   **Microsoft Active Protection Service Community** : in de online Microsoft Active Protection Service-community kunt u zien hoe anderen reageren op software die nog niet is geclassificeerd voor Risico's. U kunt deze informatie gebruiken om te bepalen of u wilt toestaan dat deze software op uw computer wordt uitgevoerd. Als u deelneemt, worden uw keuzes toegevoegd aan de classificaties van de community om andere te helpen bepalen wat ze moeten doen.  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>Hoe weet ik of mijn computer is geïnfecteerd met schadelijke software?  

 Mogelijk hebt u een vorm van schadelijke software, inclusief virussen, spyware of andere mogelijk ongewenste software op uw computer als:  

-   U nieuwe werkbalken, koppelingen of favorieten opmerkt die u niet bewust aan uw webbrowser hebt toegevoegd.  

-   Uw startpagina, muisaanwijzer of zoekprogramma onverwacht verandert.  

-   U het adres typt voor een bepaalde website, zoals een zoekmachine, maar zonder voorafgaande kennisgeving naar een andere website wordt doorgestuurd.  

-   Bestanden automatisch van uw computer worden verwijderd.  

-   Uw computer wordt gebruikt voor aanvallen op andere computers.  

-   U pop-ups ziet, ook als u geen gebruikmaakt van internet.  

-   Uw computer begint plotseling langzamer is dan normaal. Niet alle computerprestatieproblemen worden veroorzaakt door schadelijke software, maar schadelijke software, vooral spyware, kan merkbare veranderingen veroorzaken.  

Het is ook mogelijk dat zich op uw computer schadelijke software bevindt, zelfs als u hiervan geen symptomen opmerkt. Met dit type software kan zonder uw medeweten of toestemming informatie over u en uw computer worden verzameld. Ter bescherming van uw privacy en uw computer, moet u altijd Windows Defender of Endpoint Protection uitvoeren.  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>Hoe kan ik de versie van Windows Defender vinden?
 Als u wilt weer geven welke versie van Windows Defender op uw computer wordt uitgevoerd, opent u Windows Defender (Klik op **Start** en vervolgens op zoeken naar **Windows Defender**), klikt u op **instellingen**en schuift u naar de onderkant van de Windows Defender-instellingen om **versie gegevens**te vinden.

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>Wat moet ik doen als schadelijke software op mijn computer wordt gedetecteerd door Windows Defender of Endpoint Protection?  

 Als Windows Defender schadelijke of mogelijk ongewenste software detecteert op de computer (bij controles van de realtime-beschermingsfunctie of na het uitvoeren van een scan), wordt rechtsonder in het scherm een waarschuwingsbericht weergegeven over het gedetecteerde item.  

 In dit waarschuwingsbericht bevindt zich een knop **Computer opschonen** en een koppeling **Details weergeven** waarmee meer informatie over het gedetecteerde item kan worden geraadpleegd. Klik op de koppeling **Details weergeven** om het venster **Details over de mogelijke dreiging** te openen. Dit venster bevat aanvullende informatie over het gedetecteerde item. Kies nu welke actie op het item moet worden toegepast of klik op **Computer opschonen**. Bij twijfel over de op het gedetecteerde item toe te passen actie is het aanbevolen het door Windows Defender toegewezen waarschuwingsniveau als uitgangspunt te gebruiken (zie Meer informatie over waarschuwingsniveaus voor meer informatie).  

 Waarschuwingsniveaus helpen bij de beslissing hoe gereageerd moet worden op virussen, spyware en andere mogelijk ongewenste software. Windows Defender beveelt aan dat alle virussen en spyware worden verwijderd, maar soms wordt gewaarschuwd voor software die niet werkelijk kwaadaardig of ongewenst is. Met behulp van de volgende informatie kan worden bepaald wat er gedaan moet worden als Windows Defender mogelijk ongewenste software op de computer detecteert.  

 U kunt een van de volgende acties kiezen om op het gedetecteerde item toe te passen, afhankelijk van het waarschuwingsniveau:  

- **Verwijderen** : met deze actie wordt de software permanent van de computer verwijderd.  

- **Quarantaine** : met deze actie wordt de software in quarantaine geplaatst, zodat deze niet kan worden uitgevoerd. Als Windows Defender software in quarantaine plaatst, wordt deze software verplaatst naar een andere locatie. Er wordt voorkomen dat de software wordt uitgevoerd totdat de software wordt teruggezet of van de computer wordt verwijderd.  

- **Toestaan** : met deze actie wordt de software toegevoegd aan de lijst met toegestane Windows Defender en kan deze worden uitgevoerd op uw computer. U wordt niet meer door Windows Defender gewaarschuwd over mogelijke risico's waaraan de software uw privacy of de computer kan blootstellen.  

  Als u **Toestaan** kiest voor een item, bijvoorbeeld software, krijgt u geen waarschuwingen van Windows Defender meer over de risico's die de software oplevert voor uw privacy of de computer. Voeg software alleen aan de lijst met toegestane items toe als de software vertrouwd is en afkomstig is van een vertrouwde uitgever.  

### <a name="how-to-remove-potentially-harmful-software"></a>Mogelijk schadelijke software verwijderen

U kunt alle ongewenste of mogelijk schadelijke items die Windows Defender detecteert snel en eenvoudig verwijderen met de optie **Computer opschonen** .  

1.  Als u de melding ziet die wordt weergegeven in het systeemvak nadat mogelijke bedreigingen zijn gedetecteerd, klikt u op **Computer opschonen**.  

2.  Windows Defender verwijdert de mogelijke bedreiging (of bedreigingen) en geeft een melding wanneer het opschonen van de computer is voltooid.  

3.  Als u meer informatie wilt over de gedetecteerde bedreigingen, klikt u op het tabblad **Geschiedenis** en selecteert u vervolgens **Alle gedetecteerde items**.  

4.  Als u niet alle gedetecteerde items ziet, klikt u op **details weergeven**. Als u wordt gevraagd om een beheerderswachtwoord of een bevestiging, typt u het wachtwoord of bevestigt u de actie.

> [!NOTE]  
>  Indien mogelijk verwijdert Windows Defender tijdens het opschonen van de computer alleen het geïnfecteerde deel van een bestand, niet het volledige bestand.  

##  <a name="what-is-a-virus"></a>Wat is een virus?  
 Computervirussen zijn softwareprogramma's die zijn ontworpen om de werking van een computer te verstoren, om gegevens op te slaan, beschadigen of verwijderen, of om via internet andere computers te infecteren. Virussen zorgen vaak voor vertraging en veroorzaken ondertussen andere problemen.  

##  <a name="what-is-spyware"></a> Wat is spyware?  
 Spyware is software die zichzelf zonder uw toestemming, of zonder u hiervan op de hoogte te stellen of hierover controle te geven, op uw computer kan installeren of uitvoeren. Spyware veroorzaakt mogelijk geen symptomen nadat uw computer is geïnfecteerd, maar veel schadelijke of ongewenste programma's kunnen invloed hebben op de werking van uw computer. Spyware kan bijvoorbeeld uw onlinegedrag volgen of informatie over u verzamelen (met inbegrip van gegevens waarmee u kunt worden geïdentificeerd en andere gevoelige gegevens), instellingen wijzigen op uw computer of ervoor zorgen dat uw computer traag wordt.  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a>Wat is het verschil tussen virussen, spyware en andere mogelijk schadelijke software?  
 Zowel virussen als spyware worden zonder uw medeweten geïnstalleerd op uw computer en beide kunnen destructieve gevolgen hebben. Ze hebben ook de mogelijkheid informatie op uw computer vast te leggen en deze informatie te beschadigen of verwijderen. Ze kunnen beide de prestaties van uw computer negatief beïnvloeden.  

 Het belangrijkste verschil tussen virussen en spyware is hoe ze zich gedragen op uw computer. Virussen willen, net zoals levende organismen, een computer infecteren, repliceren en zich vervolgens naar zo veel mogelijk andere computers verspreiden. Spyware is echter meer hetzelfde als een Mole-IT-afdeling wil de computer verplaatsen naar en zo lang mogelijk blijven, zodat er waardevolle informatie over uw computer naar een externe bron kan worden verzonden.  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>Waar komen virussen, spyware en andere mogelijk ongewenste software vandaan?  
 Ongewenste software zoals virussen, kan worden geïnstalleerd door websites of door programma's die u hebt gedownload of die u hebt geïnstalleerd met een cd, dvd, externe vaste schijf of apparaat. Spyware wordt meestal geïnstalleerd door gratis software, zoals delen van bestanden, schermbeveiligingen of zoekwerkbalken.  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a> Kan er ongemerkt schadelijke software worden geïnstalleerd?  
 Ja, bepaalde schadelijke software kan worden geïnstalleerd vanaf een website via een Inge sloten script of programma op een webpagina. Voor de installatie van andere schadelijke software is uw hulp vereist. Deze software maakt gebruik van pop-ups in uw browser of gratis software waarvoor u een downloadbaar bestand accepteert. Als u Microsoft Windows ® up-to-date te houdt en de beveiligingsinstellingen niet verlaagt, kunt u de kans op een infectie minimaliseren.  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>Waarom is het belangrijk om licentieovereenkomsten te lezen voordat u software installeert?  
 Wanneer u websites bezoekt, ga dan niet automatisch akkoord met het downloaden van alle aanbiedingen van de site. Lees zorgvuldig de gebruiksrechtovereenkomst van gratis software, zoals programma's voor het delen van bestanden of schermbeveiligers. Wees bedacht op zinnen waarin u wordt verplicht advertenties en pop-ups van het bedrijf te accepteren of waarin wordt aangegeven dat de software bepaalde gegevens verzendt naar de software-uitgever.  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>Wat is het verschil tussen Endpoint Protection en Windows Defender?  
 Endpoint Protection is antimalwaresoftware. Dit betekent dat de software is ontworpen om een breed scala aan schadelijke software, inclusief virussen, spyware en andere mogelijk ongewenste software te detecteren en uw computer hiertegen te beschermen. Windows Defender wordt automatisch samen met uw Windows-besturingssysteem geïnstalleerd en is software die spyware detecteert en stopt.  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a>Waarom detecteert Windows Defender geen cookies?  
 Cookies zijn kleine tekst bestanden die door websites op uw computer worden geplaatst om informatie over u en uw voor keuren op te slaan. Websites gebruiken cookies om u een persoonlijke ervaring te bieden en om informatie over het gebruik van de website te verzamelen. Windows Defender detecteert geen cookies omdat deze niet worden beschouwd als een bedreiging voor uw privacy of voor de beveiliging van uw computer. Met de meeste Internet browsers kunt u cookies blok keren.  

##  <a name="how-can-i-prevent-malware"></a>Hoe voorkom ik dat schadelijke software wordt geïnstalleerd?  
 Twee van de belangrijkste zorgen voor computergebruikers zijn tegenwoordig virussen en spyware. Hoewel beide een probleem kunnen vormen, kunt u zich hier door te plannen vrij eenvoudig tegen verdedigen:  

-   Houd de software van uw computer up-to-date en vergeet niet alle patches te installeren. Werk uw besturingssysteem regelmatig bij.  

-   Zorg ervoor dat uw antivirus- en antispywaresoftware, Windows Defender, de meest recente updates gebruikt tegen mogelijke bedreigingen (zie Hoe houd ik virus-en spywaredefinities up-to-date?). Zorg er ook voor dat u altijd de meest recente versie van Windows Defender gebruikt.  

-   Download updates alleen van betrouwbare bronnen. Ga voor Windows-besturings systemen altijd naar de [catalogus Microsoft Update](https://catalog.update.microsoft.com).  Gebruik altijd de legitieme websites van het bedrijf of de persoon die de software produceert.

-   Als u een e-mailbericht met een bijlage ontvangt en de bron niet vertrouwt, verwijdert u dit onmiddellijk. Down load geen toepassingen of bestanden van onbekende bronnen en wees voorzichtig wanneer u bestanden verhandelt met andere gebruikers.  

-   Installeer en gebruik een firewall. Het wordt aanbevolen Windows Firewall in te schakelen.  

##  <a name="what-are-virus-and-spyware-definitions"></a>Wat zijn virus- en spywaredefinities?  
 Wanneer u Windows Defender of Endpoint Protection gebruikt, is het belangrijk ervoor te zorgen dat de virus- en spywaredefinities zijn bijgewerkt. Definities zijn bestanden die fungeren als een voortdurend groeiende encyclopedie met mogelijke softwarebedreigingen. Windows Defender of Endpoint Protection gebruikt definities om te bepalen of gedetecteerde software een virus, spyware of andere mogelijk ongewenste software is, en om u vervolgens te waarschuwen voor mogelijke risico's. Om ervoor te zorgen dat uw definities altijd zijn bijgewerkt, werkt Windows Defender of Endpoint Protection samen met Microsoft Update om nieuwe definities automatisch te installeren zodra ze worden vrijgegeven. Voordat u gaat scannen, kunt u ook met Windows Defender of Endpoint Protection online controleren of er bijgewerkte definities zijn.  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a>Hoe houd ik virus-en spywaredefinities up-to-date?  
 Virus- en spywaredefinities zijn bestanden die fungeren als een encyclopedie van bekende schadelijke software, inclusief virussen, spyware en andere mogelijk ongewenste software. Omdat schadelijke software voortdurend wordt ontwikkeld, is Windows Defender of Endpoint Protection afhankelijk van bijgewerkte definities om te bepalen of software die wordt geïnstalleerd of uitgevoerd, of waarmee wordt geprobeerd instellingen op uw computer te wijzigen, een virus, spyware of andere mogelijk ongewenste software is.  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>Voor een geplande scan automatisch controleren op nieuwe definities (aanbevolen)  

1.  Open de Windows Defender- of Endpoint Protection-client door op het pictogram in het systeemvak te klikken, of start de client vanuit het menu **Start** .  

2.  Klik op **Instellingen**en klik vervolgens op **Geplande scan**.  

3.  Controleer of het selectievakje **Zoeken naar de meest recente definities van virussen en spyware voordat een geplande scan wordt uitgevoerd** is ingeschakeld en klik vervolgens op **Wijzigingen opslaan**. Als u wordt gevraagd om een beheerderswachtwoord of een bevestiging, typt u het wachtwoord of bevestigt u de actie.  

### <a name="to-check-for-new-definitions-manually"></a>Handmatig controleren of er nieuwe definities zijn

 Windows Defender of Endpoint Protection werkt automatisch de virus- en spywaredefinities op uw computer bij. Als de definities meer dan zeven dagen niet zijn bijgewerkt (bijvoorbeeld als u de computer gedurende een week niet hebt ingeschakeld), geeft Windows Defender of Endpoint Protection u een melding dat de definities verouderd zijn.  

1.  Open de Windows Defender- of Endpoint Protection-client door op het pictogram in het systeemvak te klikken, of start de client vanuit het menu **Start** .  

2.  Als u handmatig wilt controleren of er nieuwe definities zijn, klikt u op het tabblad **Bijwerken** en klikt u vervolgens op **Definities bijwerken**.  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Hoe kan ik items verwijderen of herstellen die door Windows Defender of Endpoint Protection in quarantaine zijn geplaatst?  

 Als Windows Defender of Endpoint Protection software in quarantaine plaatst, wordt de software verplaatst naar een andere locatie. Er wordt voorkomen dat de software wordt uitgevoerd totdat de software wordt teruggezet of van de computer wordt verwijderd.  

 Voor alle stappen in deze procedure geldt het volgende: als u gevraagd om een beheerderswachtwoord of een bevestiging, typt u het wachtwoord of geeft u de bevestiging.  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Items verwijderen of herstellen die door Windows Defender of Endpoint Protection in quarantaine zijn geplaatst


1.  Klik op het tabblad **Geschiedenis** , selecteer **Items in quarantaine**en selecteer vervolgens de optie **Items in quarantaine** .  

2.  Klik op **Details weergeven** om alle items te bekijken.  

3.  Bekijk elk item en klik voor elk item of u dit wilt **Verwijderen** of **Herstellen**. Als u alle items in quarantaine van uw computer wilt verwijderen, klikt u op **Alles verwijderen**.  

##  <a name="what-is-real-time-protection"></a>Wat is realtime-beveiliging?  

 Realtime-beveiliging zorgt ervoor dat Windows Defender de computer continu bewaakt en waarschuwt u wanneer mogelijke bedreigingen zoals virussen en spyware, probeert zichzelf te installeren of uit te voeren op uw computer. Omdat deze functie een belangrijk aspect vormt van de manier waarop Windows Defender uw computer beschermt, moet u ervoor zorgen dat realtime-beveiliging altijd is ingeschakeld. Als realtime-beveiliging is uitgeschakeld, ontvangt u een melding van Windows Defender en wordt de status van de computer gewijzigd in **risico**.  

 Wanneer met realtime-beveiliging een dreiging of mogelijke bedreiging wordt gedetecteerd, wordt door Windows Defender een melding weergegeven. U kunt nu kiezen uit de volgende opties:  

- Klik op **Computer opschonen** om het gedetecteerde item te verwijderen. Windows Defender verwijdert het item automatisch van uw computer.  

- Klik op de koppeling **Details weergeven** om het venster Details over de mogelijke dreiging weer te geven en kies vervolgens welke actie moeten worden uitgevoerd op het gedetecteerde item.  

  U kunt kiezen welke software en instellingen Windows Defender moet bewaken, maar het wordt aangeraden om realtime-beveiliging en alle opties voor realtime-beveiliging in te schakelen. In de volgende tabel worden de beschikbare opties verklaard.  

|||  
|-|-|  
|**Optie realtime-beveiliging**|**Doel**|  
|Alle downloads scannen|Deze optie controleert bestanden en programma's die worden gedownload, inclusief bestanden die automatisch worden gedownload via Windows Internet Explorer en Microsoft Outlook Express ®, zoals ® ActiveX-besturingselementen en software-installatieprogramma's. Deze bestanden kunnen door de browser worden gedownload, geïnstalleerd of uitgevoerd. Schadelijke software, inclusief virussen, spyware en andere mogelijk ongewenste software, kan worden opgenomen in deze bestanden en zonder uw medeweten worden geïnstalleerd.<br /><br /> Met de optie realtime-beveiliging bewaakt Windows Defender voortdurend de computer en controleert deze op mogelijke schadelijke bestanden of programma's die u hebt gedownload. Dankzij deze bewakingsfunctie hoeft Windows Defender uw browser- of e-mailervaring niet te vertragen om bestanden of programma's die u wilt downloaden te controleren.|  
|De activiteit van bestanden en programma's op de computer controleren|Deze optie houdt in de gaten wanneer bestanden en programma's op uw computer worden gestart en waarschuwt u over de acties die ze uitvoeren en over de acties die erop worden uitgevoerd. Dit is belangrijk, omdat schadelijke software gebruik kan maken van beveiligingslekken in programma's die u hebt geïnstalleerd om buiten uw medeweten schadelijke of ongewenste software uit te voeren. Spyware zichzelf bijvoorbeeld op de achtergrond uitvoeren wanneer u een programma start dat u vaak gebruikt. Windows Defender controleert uw programma's en waarschuwt u als er verdachte activiteiten worden gedetecteerd.|  
|Gedragscontrole inschakelen|Met deze optie controleert u verzamelingen gedragingen op verdachte patronen die door traditionele methoden voor antivirusdetectie niet zouden worden gedetecteerd.|  
|Systeem voor netwerkinspectie inschakelen|Deze optie helpt u uw computer te beschermen tegen aanvallen met een zwakke dag van bekende beveiligings problemen, waardoor de periode tussen het moment dat een beveiligings probleem wordt gedetecteerd en een update wordt toegepast.|  

### <a name="to-turn-off-real-time-protection"></a>Realtime-beveiliging uitschakelen  

1.  Klik op **Instellingen**en klik vervolgens op **Realtime-beveiliging.**  

2.  Wis de opties voor realtime-beveiliging die u wilt uitschakelen en klik vervolgens op **Wijzigingen opslaan**. Als u wordt gevraagd om een beheerderswachtwoord of een bevestiging, typt u het wachtwoord of bevestigt u de actie.  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a>Hoe weet ik of Windows Defender of Endpoint Protection op mijn computer wordt uitgevoerd?  

 Nadat u Windows Defender op uw computer hebt geïnstalleerd, kunt u het hoofdvenster sluiten en Windows Defender op de achtergrond uitvoeren. Windows Defender wordt voortdurend op uw computer uitgevoerd om deze te beveiligen tegen bedreigingen.  

 U weet natuurlijk ook dat Windows Defender wordt uitgevoerd wanneer hierdoor in het systeemvak meldingen worden weergegeven. Met deze meldingen wordt u geattendeerd op mogelijke bedreigingen die door Windows Defender zijn gedetecteerd.  

 U ontvangt ook andere waarschuwingsmeldingen, bijvoorbeeld wanneer u realtime-beveiliging hebt uitgeschakeld, wanneer u de virus- en spywaredefinities een aantal dagen niet hebt bijgewerkt of wanneer er updates voor het programma beschikbaar zijn. Windows Defender geeft ook kort een melding weer om u erop te attenderen dat de computer wordt gescand.  

> [!TIP]
> 
> Als u het pictogram Windows Defender niet in het systeemvak ziet, klikt u op de pijl in het systeemvak om verborgen pictogrammen weer te geven, met inbegrip van het pictogram van Windows Defender.  


 De kleur van het pictogram is afhankelijk van de huidige status van uw computer:  

-   Groen geeft aan dat de computerstatus Beschermd is.  

-   Geel geeft aan dat de computerstatus Mogelijk niet beschermd is.  

-   Groen geeft aan dat de computerstatus Risico is.  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>Hoe kan ik waarschuwingen door Windows Defender of Endpoint Protection instellen?  
 Wanneer Windows Defender op uw computer wordt uitgevoerd, wordt u automatisch gewaarschuwd als er een virus, spyware of andere mogelijk ongewenste software wordt gedetecteerd. U kunt Windows Defender ook zo instellen dat u wordt gewaarschuwd als u software uitvoert die nog niet is geanalyseerd en u kunt ervoor kiezen om te worden gewaarschuwd wanneer door software wijzigingen aan uw computer worden aangebracht.  

### <a name="to-set-up-alerts"></a>Waarschuwingen instellen  

1.  Klik op **Instellingen**en klik vervolgens op **Realtime-beveiliging.**  

2.  Zorg ervoor dat het selectievakje **Realtime-beveiliging inschakelen (aanbevolen)** is ingeschakeld.  

3.  Schakel de selectievakjes in naast de opties voor real-timebeveiliging die u wilt uitvoeren en klik vervolgens op **Wijzigingen opslaan**. Als u wordt gevraagd om een beheerderswachtwoord of een bevestiging, typt u het wachtwoord of bevestigt u de actie.  

### <a name="see-also"></a>Zie ook  
 [Problemen met Windows Defender of Endpoint Protection-client oplossen](troubleshoot-endpoint-client.md)   

 [Help bij Endpoint Protection-client](endpoint-protection-client-help.md)

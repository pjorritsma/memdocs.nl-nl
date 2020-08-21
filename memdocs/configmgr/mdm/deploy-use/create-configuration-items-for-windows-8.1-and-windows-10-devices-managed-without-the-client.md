---
title: Configuratie-items voor Windows maken
titleSuffix: Configuration Manager
description: Configuratie-items maken voor het beheren van instellingen voor Windows 10-computers met on-premises Mobile Device Management (MDM) in Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 26846066aa713d40fdacfe75810d43cafd1c3f04
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693672"
---
# <a name="create-configuration-items-for-windows-devices-with-on-premises-mdm-in-configuration-manager"></a>Configuratie-items maken voor Windows-apparaten met on-premises MDM in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik het configuratie-item Configuration Manager **windows 8,1 en Windows 10** om instellingen te beheren voor Windows-apparaten die u beheert met on-premises Mobile Device Management (MDM).

Raadpleeg de volgende artikelen voor meer algemene informatie over de instellingen voor naleving in Configuration Manager:

- [Aan de slag met instellingen voor naleving](../../compliance/get-started/get-started-with-compliance-settings.md)

- [Nalevings instellingen plannen en configureren](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)

## <a name="create-a-configuration-item"></a>Een configuratie-item maken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit en selecteer vervolgens het knoop punt configuratie- **items** .

1. Selecteer **configuratie-item maken**op het tabblad **Start** van het lint in de groep **maken** .

1. Geef op de pagina **Algemeen** van de **wizard Configuratie-item maken**de volgende informatie op:

    - **Naam**: een unieke naam voor het identificeren van dit configuratie-item.

    - **Beschrijving**: een optionele beschrijving voor meer informatie over het gebruik ervan.

    - Onder **instellingen voor apparaten die worden beheerd *zonder* de Configuration Manager-client**, selecteert u **Windows 8,1 en Windows 10**.

    - **Categorieën**: u kunt categorieën maken en toewijzen om u te helpen bij het zoeken en filteren van configuratie-items in de Configuration Manager-console.

1. Selecteer op de pagina **ondersteunde platforms** van de wizard de specifieke Windows-platforms om dit configuratie-item te evalueren.

1. Selecteer op de pagina **Apparaatinstellingen** de instellingen groepen die u wilt configureren. Zie voor meer informatie over de beschik bare instellingen [referentie-instellingen](#bkmk_setref).

    > [!TIP]
    > Als de instelling die u wilt, niet wordt weer gegeven, selecteert u de optie voor het **configureren van extra instellingen die niet in de standaard instellings groepen staan**. Met deze optie wordt de pagina **extra instellingen** toegevoegd aan de wizard.

1. Configureer op elke pagina instellingen de vereiste instellingen. Wanneer de instellingen deze ondersteunen, kunt u ook niet- **compatibele instellingen herstellen**. Als een apparaat de instelling evalueert als niet compatibel met dit configuratie-item, wordt de instelling hersteld zodat deze compatibel is.

    U kunt voor elke instellingen groep ook de ernst configureren die wordt gerapporteerd wanneer de instelling niet aan het beleid voldoet. Kies een van de volgende waarden voor de optie **ernst van niet-compliantie voor rapporten** :

    - **Geen**: voor apparaten die niet voldoen aan deze nalevings regel wordt geen fout Ernst gerapporteerd voor Configuration Manager-rapporten.

    - **Informatie**

    - **Waarschuwing**

    - **Kritiek**

    - **Kritiek met gebeurtenis**: voor apparaten die niet voldoen aan deze compliantie regel wordt de fout Ernst **kritiek** gerapporteerd voor Configuration Manager-rapporten. Ook wordt de niet-compatibele status geregistreerd als een Windows-gebeurtenis in het logboek voor toepassings gebeurtenissen.

1. Op de pagina **platform toepas baarheid** van de wizard controleert u alle instellingen die niet compatibel zijn met de geselecteerde ondersteunde platforms. Ga terug en verwijder deze instellingen, wijzig de ondersteunings platforms of ga door.

    > [!IMPORTANT]
    > Apparaten beoordelen niet de naleving van niet-ondersteunde instellingen.

1. Voltooi de wizard.

U kunt het nieuwe configuratie-item weergeven in het knooppunt **Configuratie-items** van de werkruimte **Activa en naleving** .

## <a name="settings-reference"></a><a name="bkmk_setref"></a> Verwijzing naar instellingen  

In de volgende secties worden de specifieke instellingen beschreven die beschikbaar zijn in elke groep. Configureer deze instellingen op de pagina **Apparaatinstellingen** van de **wizard Configuratie-item maken** voor **Windows 8,1-en Windows 10** -apparaten die worden beheerd *zonder* de Configuration Manager-client.

### <a name="password"></a>Wachtwoord

Deze instellingen zijn alleen voor apparaten met Windows 10 of hoger.

- **Wachtwoord instellingen vereisen op apparaten**: een wacht woord vereisen op ondersteunde apparaten.
- **Minimale wachtwoord lengte (tekens)**: de minimale lengte voor het wacht woord.
- **Wacht woord verloopt over dagen**: het aantal dagen waarna de gebruiker het wacht woord moet wijzigen.
- **Aantal onthouden wacht woorden**: hiermee voor komt u dat eerder gebruikte wacht woorden opnieuw worden gebruikt.
- **Aantal mislukte aanmeldings pogingen voordat het apparaat wordt gewist**: als dit aantal aanmeldings pogingen mislukt, wordt het apparaat gewist door MDM
- **Niet-actieve periode voordat het apparaat wordt vergrendeld**: Hiermee geeft u de hoeveelheid tijd op die een apparaat inactief kan zijn voordat het wordt vergrendeld. Het apparaat is niet actief wanneer er geen gebruikers invoer is.
- **Wachtwoord complexiteit**: Kies of u een numerieke pincode wilt opgeven, bijvoorbeeld `1234` of of u een sterk wacht woord moet invoeren.
  - **Aantal complexe teken sets dat is vereist in het wacht woord**: als de complexiteit van het wacht woord **sterk**is, selecteert u hoeveel typen tekens het wacht woord vereist: hoofd letters, kleine letters, cijfers en symbolen. Deze waarde is standaard ingesteld op `2` .
- **Pincode voor wachtwoordherstel verzenden naar Exchange Server**

### <a name="device"></a>Apparaat

- **Scherm opname**: Schakel deze instelling in om de gebruiker toe te staan een scherm opname van de weer gave van het apparaat te maken. (Alleen Windows 10)
- **Verzen ding van diagnostische gegevens**: Schakel deze instelling in om Windows diagnostische gegevens toe te staan voor analyse. (Alleen Windows 8.1)
- **Verzen ding van diagnostische gegevens toestaan (Windows 10)**: Stel het niveau van Windows diagnostische gegevens in voor analyse: uitschakelen, basis, uitgebreid of volledig. (Alleen Windows 10)
- **Geolocatie**: Schakel deze instelling in om het apparaat in staat te stellen locatie service gegevens te gebruiken. (Alleen Windows 10)
- **Kopiëren en plakken**: Schakel deze instelling in als u kopiëren en plakken wilt gebruiken om gegevens over te dragen tussen apps. (Alleen Windows 10)
- **Fabrieks instellingen terugzetten**: Schakel deze instelling in om de gebruiker toe te staan om het apparaat opnieuw in te stellen op de begin waarden. (Alleen Windows 10)
- **Bluetooth**: het gebruik van de Bluetooth-functionaliteit van het apparaat toestaan of verbieden.
- **Modus voor Bluetooth-detectie**: toestaan of voor komen dat het apparaat door andere Bluetooth-apparaten wordt gedetecteerd. (Alleen Windows 10)
- **Bluetooth-reclame**: het gebruik van Bluetooth-reclame toestaan of verbieden. (Alleen Windows 10)
- **Spraak opname**: het gebruik van de spraak opname functies van het apparaat toestaan of verbieden. (Alleen Windows 10)
- **Cortana**: het gebruik van de Cortana-spraak assistent toestaan of verbieden. (Alleen Windows 10)
- **Meldingen in onderhouds centrum**: in-of uitschakelen van het meldings venster in Windows 10. (Alleen Windows 10)
- **Regio-instellingen wijzigen (alleen Desktop)**: Hiermee staat u toe of voor komt u dat de gebruiker de regionale instellingen op het apparaat kan wijzigen.
- **Instellingen voor in-/uitschakelen en slaap stand wijzigen (alleen Desktop)**: Hiermee staat u toe dat de gebruiker de instellingen voor energie en slaap stand kan wijzigen op het apparaat.
- **Taal instellingen wijzigen (alleen Desktop)**: toestaan of voor komen dat de gebruiker de taal instellingen op het apparaat wijzigt.
- **Systeem tijd wijzigen**: de datum en tijd van het apparaat kunnen worden gewijzigd door de gebruiker.
- **Apparaatnaam wijzigen**: toestaan of verhinderen dat de gebruiker de naam van het apparaat wijzigt.

### <a name="email-management"></a>E-mailbeheer

Deze instellingen zijn voor apparaten met Windows 8.1 en Windows 10.  

- **Pop-en IMAP-e-mail**: verbindingen toestaan of verbieden voor e-mail accounts die gebruikmaken van de pop-en IMAP-standaarden.
- **Maximale tijd voor het opslaan van e-mail**: hoe lang e-mail moet worden bewaard voordat de server deze verwijdert.
- **Toegestane bericht indelingen**: Hiermee geeft u op of E-mails **tekst zonder opmaak** of **HTML en tekst zonder opmaak**zijn.
- **Maximale grootte voor e-mail met tekst zonder opmaak (automatisch gedownload)**: Stel de maximale grootte van e-mails met tekst zonder opmaak in wanneer deze automatisch worden gedownload.
- **Maximum grootte voor HTML-e-mail (automatisch gedownload)**: Stel de maximale grootte van HTML-e-mails in wanneer deze automatisch worden gedownload.
- **Maximale grootte van een bijlage (automatisch gedownload)**: Stel de maximale grootte van e-mail bijlagen in die automatisch worden gedownload.
- **Agenda synchronisatie**: synchronisatie van agenda's op het apparaat toestaan of verbieden.
- **Aangepast e-mail account**: het gebruik van een niet-organisatie-e-mail account op het apparaat toestaan of verbieden.
- **Micro soft-account optioneel maken in Windows Mail-app**: Schakel deze optie in als u geen Microsoft-account nodig hebt in Windows Mail.

### <a name="store"></a>Opslaan

Deze instellingen zijn alleen voor apparaten met Windows 10 of hoger.

- **Toepassings archief**: toegang tot de Microsoft Store op het apparaat toestaan of verbieden.
- **Voer een wacht woord in om toegang te krijgen tot het toepassings archief**: Schakel deze optie in als u wilt dat gebruikers een wacht woord invoeren om toegang te krijgen tot de app Microsoft Store.
- **Aankopen in app**: Hiermee staat u gebruikers toe om in-app-aankopen te maken.
- Door **Store afkomstige app starten**: alle apps uitschakelen die vooraf zijn geïnstalleerd op het apparaat of die zijn geïnstalleerd vanaf de Microsoft Store.
- **Apps uit de Store automatisch bijwerken**: toestaan of verhinderen dat apps die zijn geïnstalleerd van de Microsoft Store automatisch worden bijgewerkt.
- **Apps installeren op Systeem station**: Hiermee staat u toe dat het apparaat apps op het systeem station installeert. Dit is meestal het `C:` station.
- **App-gegevens installeren op systeem volume**: Schakel deze optie in om apps in staat te stellen gegevens op te slaan op het systeem station.
- **Alleen persoonlijke Store gebruiken**: gebruikers moeten apps uit uw privé-archief downloaden.
- **Game DVR**: Windows Game-opname en-uitzending uitschakelen

### <a name="browser"></a>Browser

Deze instellingen zijn voor apparaten met Windows 8.1 en Windows 10.

- **Webbrowser toestaan**: het gebruik van de webbrowser op het apparaat toestaan of verbieden.
- **Automatisch door voeren**: het wijzigen van de instellingen voor automatisch aanvullen in de browser toestaan of verbieden.
- **Actieve scripting**: toestaan of verbieden of de browser scripts kan uitvoeren, zoals ActiveX-scripts.
- Invoeg **toepassingen**: het toevoegen of verbieden van invoeg toepassingen aan Internet Explorer toestaan.
- **Pop-upblokkering**: de pop-upblokkering van de browser toestaan of verbieden.
- **Cookies**: toestaan of verhinderen dat cookies op het apparaat worden opgeslagen.
- **Fraude waarschuwing**: waarschuwingen voor mogelijke frauduleuze websites toestaan of weigeren.

### <a name="internet-explorer"></a>Internet Explorer

Deze instellingen zijn voor apparaten met Windows 8.1 en Windows 10.

- **Altijd do not track-header verzenden**: het verzenden van Browse gegevens naar sites van derden toestaan of verbieden.
- **Beveiligings zone Intranet**: toewijzing van een beveiligings niveau aan de beveiligings zone Intranet toestaan of verbieden.
- **Beveiligings niveau voor Internet zone**: Stel het beveiligings niveau in voor de zone Internet: hoog, gemiddeld-hoog of gemiddeld.
- **Beveiligings niveau voor intranet zone**: Stel het beveiligings niveau voor de intranet zone in: hoog, gemiddeld-hoog, gemiddeld, middel groot laag of laag.
- **Beveiligings niveau voor zone met vertrouwde sites**: Stel het beveiligings niveau in voor de zone met vertrouwde sites: hoog, gemiddeld-hoog, gemiddeld, middel groot laag of laag.
- **Beveiligings niveau voor zone Websites met beperkte toegang**: Stel het beveiligings niveau in voor de zone met sites met beperkte toegang: hoog.
- **Naam ruimten voor intranet zone**: Configureer websites om toe te voegen aan of te verwijderen uit de intranet zone.
- **Ga naar intranet site voor invoer van één woord**: toestaan of verbieden dat Internet Explorer automatisch naar een intranet site gaat als de gebruiker een geldige site naam invoert zonder hiervoor een voor gaande protocol `https://` .
- **Menu optie bedrijfs modus**: Hiermee stelt u gebruikers in staat om bedrijfs modus te activeren en deactiveren vanuit het menu **extra** in Internet Explorer.
  - **Locatie van registratie rapport (URL)**: als bedrijfs modus actief is, geeft u een URL op voor het registreren van bezochte websites.
- Locatie van de lijst met websites van **bedrijfs modus (URL)**: als de ondernemings modus actief is, geeft u de lijst met sites op die deze gebruikt.

### <a name="cloud"></a>Cloud

Deze instellingen zijn voor apparaten met Windows 8.1 en Windows 10.

- **Synchronisatie van instellingen**: het synchroniseren van instellingen tussen apparaten toestaan of verbieden.
- **Synchronisatie van referenties**: referenties toestaan of verbieden voor synchronisatie tussen apparaten.
- **Micro soft-account**: Schakel deze instelling in om het gebruik van een Microsoft-account op het apparaat toe te staan.
- **Synchronisatie van instellingen via verbindingen met een Data limiet**: toestaan of verbieden dat instellingen worden gesynchroniseerd wanneer de netwerk verbinding wordt gemeten.

### <a name="security"></a>Beveiliging

- **Installatie van niet-ondertekend bestand**: Hiermee staat u toe dat een niet-ondertekend bestand kan worden geïnstalleerd. (Alleen Windows 10)
- Niet- **ondertekende toepassingen**: het installeren van niet-ondertekende apps toestaan of verbieden. (Alleen Windows 10)
- **SMS-en MMS-berichten**: protocol voor tekst berichten op het apparaat toestaan of verbieden. (Alleen Windows 10)
- **Verwissel bare opslag**: het gebruik van Verwissel bare opslag, zoals een SD-kaart, toestaan of verbieden. (Alleen Windows 10)
- **Camera**: het gebruik van de camera van het apparaat toestaan of verbieden. (Alleen Windows 10)
- **Near Field Communication (NFC)**: communicatie via NFC toestaan of verbieden. (Alleen Windows 10)
- **Anti diefstal modus**: het gebruik van de anti diefstal-modus van Windows 10 toestaan of verbieden. (Alleen Windows 10)
- **USB-verbinding toestaan**: andere apparaten kunnen toestaan of verbieden dat er verbinding wordt gemaakt met dit apparaat via een USB-verbinding. (Alleen Windows 10)
- **Windows RT VPN-profiel**: een VPN-profiel voor Windows RT-apparaten inrichten (alleen Windows 8,1)

### <a name="peak-synchronization"></a>Pieksynchronisatie

Deze instellingen zijn alleen voor apparaten met Windows 10 of hoger.

- **Piek tijd opgeven**: Stel de piek tijd en dagen van de week in voor synchronisatie van mobiele apparaten.
- **Synchronisatiefrequentie binnen piektijden**: Configureer Hoe vaak synchronisatie plaatsvindt tijdens de piek uren.
- **Synchronisatiefrequentie buiten piektijden**: Configureer Hoe vaak synchronisatie plaatsvindt buiten de piek uren.

### <a name="roaming"></a>Roaming

- **Apparaatbeheer tijdens roaming**: toestaan of verhinderen dat Configuration Manager het apparaat beheert tijdens roaming. (Alleen Windows 10)
- **Software downloaden tijdens roaming: het**downloaden van apps en software tijdens het roamen toestaan of verbieden. (Alleen Windows 10)
- **E-mail downloaden tijdens roaming**: e-mail downloads toestaan of verbieden tijdens roaming. (Alleen Windows 10)
- **Gegevens roaming**: roaming tussen netwerken toestaan of verbieden bij het openen van gegevens.
- **VPN via mobiel**: toestaan of voor komen dat het apparaat een VPN-verbinding gebruikt tijdens de verbinding met een mobiel netwerk. (Alleen Windows 10)
- **VPN-roaming via mobiel**: toestaan of voor komen dat het apparaat een VPN-verbinding gebruikt tijdens roaming op een mobiel netwerk. (Alleen Windows 10)

### <a name="encryption"></a>Versleuteling

- **Versleuteling van opslag kaart**: Stel deze in op om te vereisen dat de gebruiker opslag kaarten versleutelt die op het apparaat worden gebruikt. (Alleen Windows 10)
- **Bestands versleuteling op apparaat**: ingesteld op om bestanden te versleutelen die zijn opgeslagen op het apparaat.
- **Ondertekening van E-mail vereisen**: de gebruiker moet e-mail berichten digitaal ondertekenen voordat ze worden verzonden.
  - **Handtekening algoritme**: Selecteer het algoritme voor het ondertekenen van e-mail berichten: standaard, SHA of MD5
- **E-mail versleuteling vereisen**: de gebruiker moet e-mails versleutelen voordat ze worden verzonden.
  - **Versleutelings algoritme**: Selecteer het algoritme voor het versleutelen van e-mail berichten: standaard, Triple DES, des, RC2 128-bits, RC2 64-bits, RC2 40-bits

### <a name="wireless-communications"></a>Draadloze communicatie

Deze instellingen zijn alleen voor apparaten met Windows 10 of hoger.

- **Draadloze netwerk verbinding**: de Wi-Fi-mogelijkheid van het apparaat toestaan of verbieden.
- **Wi-Fi-Tethering**: Hiermee stelt u de gebruiker in staat om het apparaat te gebruiken als een mobiele hotspot.
- **Gegevens naar Wi-Fi offloaden**: Schakel het apparaat zo veel mogelijk in voor gebruik van de Wi-Fi-verbinding.
- **Wi-Fi-HOTS pots melden**: Hiermee kan het apparaat informatie over Wi-Fi-verbindingen verzenden om de gebruiker te helpen verbindingen in de buurt te detecteren.
- **Hand matige Wi-Fi-configuratie**: Hiermee staat u de gebruiker toe om hand matig draadloze verbindingen te configureren.

#### <a name="configured-wireless-network-connections"></a>Geconfigureerde draadloze netwerk verbindingen

1. Selecteer **toevoegen**op de pagina **instellingen voor draadloze communicatie voor mobiele apparaten configureren** .

1. Geef in het venster **draadloze netwerk verbinding** de volgende informatie op over de draadloze verbinding die moet worden ingericht op mobiele apparaten:

    - **Netwerk naam (SSID)**: Voer de naam in van het Wi-Fi-netwerk.
    - **Netwerk verbinding**: Kies **Internet** of **werk**.
    - **Verificatie**: Kies de verificatie methode voor de draadloze verbinding:
        - **Openen**
        - **Gedeeld**
        - **WPA**
        - **WPA-PSK**
        - **WPA2**
        - **WPA2-PSK**
    - **Gegevens versleuteling**: Kies de versleutelings methode die door deze verbinding wordt gebruikt. De beschik bare waarden worden gewijzigd op basis van de **verificatie** methode die u selecteert:
        - **Uitgeschakeld**
        - **WEP**
        - **TKIP**
        - **KIEST**
    - **Sleutel index**: wanneer u **gegevens versleuteling** instelt op **WEP**, selecteert u een sleutel index van **1** tot **4**.
    - **Dit netwerk maakt verbinding met Internet**: Geef proxy instellingen op zodat mobiele apparaten in een draadloos netwerk verbinding kunnen maken met internet.
        - **Instellingen voor proxy server**: Configureer uw **Server** -en **poort** instellingen voor http-, **WAP**-en **socket** **-** proxy's.
    - **802.1 x-instellingen**:
        - **802.1 x-netwerk toegang inschakelen**: de verbinding beveiligen door een EAP-type op te geven.
        - **EAP-type**: Kies een van de volgende verificatie protocollen:
            - **PEAP**
            - **Smartcard of certificaat**

### <a name="certificates"></a>Certificaten

Importeer certificaten om te installeren op mobiele apparaten.

Selecteer **importeren**en geef vervolgens de volgende waarden op:

- **Certificaat bestand**: Blader naar en selecteer een certificaat bestand (**. CER**) dat u wilt importeren.
- **Doel archief**: Kies een of meer van de volgende certificaat archieven:
  - **Basis**
  - **CA (consistentie en beschikbaarheid)**
  - **Normaal**
  - **Gemachtigd**
  - **SPC**
  - **Peer**
- **Rol**: als u het certificaat archief **SPC** (software-uitgever certificaat) kiest, kiest u de rol die u aan het certificaat wilt koppelen:
  - **Mobiele operator**
  - **Manager**
  - **Door gebruiker geverifieerd**
  - **IT-administrator**
  - **Niet door gebruiker geverifieerd 	S**
  - **Vertrouwde inrichtingsserver**

### <a name="system-security"></a>Systeembeveiliging

- **Gebruikersaccountbeheer: Hiermee**configureert u het gedrag van Windows Gebruikersaccountbeheer op het apparaat.
- **Netwerk firewall**: vereist dat Windows de ingebouwde firewall inschakelt. (Windows 8,1)
- **Updates**: Hiermee configureert u het gedrag van Windows-software-updates. (Windows 8,1)
  - **Minimale classificatie van updates**: Kies de minimale classificatie van updates die u wilt downloaden en installeren: **geen**, **belang rijk**of **Aanbevolen**.
- **Updates (Windows 10)**: Configureer het gedrag Windows-software-updates. (Alleen Windows 10)
  - **Dag van installatie**: Kies de geplande dag wanneer het apparaat automatisch updates installeert en opnieuw opstart. (Alleen Windows 10)
  - **Installatie tijd**: Kies het geplande tijdstip waarop het apparaat automatisch updates installeert en opnieuw opstart. (Alleen Windows 10)
- **SmartScreen**: Windows Smart Screen in-of uitschakelen.
- **Virus beveiliging**: vereist dat Windows Antivirus software heeft.
- **Hand tekeningen voor virus beveiliging zijn bijgewerkt**: vereisen dat de virus handtekeningen bestanden up-to-date zijn.
- **Meldings weergave voor het vergrendelings scherm**: meldingen in-of uitschakelen om weer te geven op het vergrendelings scherm.
- **Functies van de voorlopige versie**: Configureer of het apparaat instellingen en functies van de voorlopige versie accepteert. (Alleen Windows 10)
- **Hand matige installatie van het basis certificaat**: in-of uitschakelen dat de gebruiker hand matig een basis certificaat kan installeren. Dit maakt het mogelijk om een certificaat te vertrouwen dat is uitgegeven door de hoofdmap. (Alleen Windows 10)
- **Hand matige uitschrijving toestaan**: toestaan of voor komen dat de gebruiker de registratie van het apparaat bij on-premises Mobile Device Management met Configuration Manager ongedaan maakt.

### <a name="windows-server-work-folders"></a>Windows Server-werkmappen

Deze instellingen zijn voor apparaten met Windows 8.1 en Windows 10.

- **URL voor werkmappen**: Geef de locatie op van een Windows Server-werkmap waarmee gebruikers vanaf hun apparaat verbinding kunnen maken.

### <a name="allowed-and-blocked-apps-list"></a>Lijst met toegestane en geblokkeerde apps

Deze instellingen zijn alleen voor apparaten met Windows Phone, die Configuration Manager on-premises MDM niet worden ondersteund. Zie [Wat is er gebeurd met hybride?](../understand/what-happened-to-hybrid.md)voor meer informatie.

### <a name="windows-10-team"></a>Windows 10 Team

Deze instellingen zijn alleen voor apparaten met Windows 10 team.

- **Toestaan dat het scherm automatisch wordt geactiveerd wanneer Sens oren iemand in de ruimte detecteren**: toestaan of voor komen dat het apparaat automatisch wordt geactiveerd wanneer de sensor iemand in de ruimte detecteert.
- **Pincode vereisen voor draadloze projectie**: Schakel deze optie in of uit of u een pincode moet invoeren voordat een ander apparaat draadloos verbinding kan maken voor projectie.
- **Onderhouds venster**: Schakel deze instelling in om het venster te configureren wanneer het apparaat door updates kan worden geïnstalleerd en opnieuw moet worden gestart.
  - **Begin tijd**: Stel de begin tijd in voor het onderhouds venster.
  - **Duur (uren)**: Stel de lengte in uren in van het onderhouds venster.
- **Azure Operational Insights**: [Azure Operational Insights](https://azure.microsoft.com/resources/videos/azure-operational-insights-overview/) toestaan om logboek bestand gegevens van Windows 10 team-apparaten te verzamelen, op te slaan en te analyseren.
  - **Werk ruimte-id**: Voer een geldige werk ruimte-id in
  - **Werkruimte sleutel**: Voer de sleutel in voor de gekoppelde werk ruimte
- **Draadloze miracast-projectie**: Hiermee staat u toe dat apparaten met miracast kunnen projecteren op dit Windows 10 team-apparaat.
  - **Miracast-kanaal**: Selecteer een miracast-kanaal om inhoud te projecteren.
- **Informatie over de vergadering die wordt weer gegeven op het welkomst scherm**: Kies het type informatie dat op het apparaat wordt weer gegeven op de tegel **vergaderingen** van het **welkomst** scherm:
  - **Alleen de organisator en tijd weergeven**
  - **Organisator, tijd en onderwerp weergeven (onderwerp verborgen bij privévergaderingen)**
- **URL voor achtergrond afbeelding voor scherm vergrendeling**: Geef een URL op om een aangepaste achtergrond weer te geven op het **welkomst** scherm van een apparaat met Windows 10 team. Start de URL met `https://` en gebruik de PNG-indeling.

### <a name="windows-information-protection"></a>Windows Information Protection  

Zie [uw ondernemings gegevens beveiligen met behulp van Windows Information Protection (WIP)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)voor meer informatie over het configureren van ondernemings gegevens beveiliging met Configuration Manager.

### <a name="microsoft-edge-legacy"></a>Micro soft Edge verouderd

Deze instellingen zijn alleen voor apparaten met Windows 10 of hoger.  

- **Zoek suggesties in de adres balk toestaan**: laat de zoek machine sites Voorst Ellen terwijl u zoek termen typt.
- **Do not track toestaan: laat**websites weten dat u niet wilt dat ze uw bezoek volgen.
- **SmartScreen inschakelen**: Controleer of gedownloade bestanden geen schadelijke code bevatten.
- **Pop-ups toestaan**: pop-ups van de browser configureren.
- **Cookies toestaan**: Configureer het gebruik van cookies.
- Automatisch door **voeren toestaan**: laat de browser formulieren automatisch invullen met opgeslagen gegevens zoals naam, adres en telefoon nummer.
- **Wachtwoord beheer toestaan**: Hiermee kunt u de wacht woorden voor websites opslaan en beheren in de browser.
- **Ontwikkelhulpprogramma's**: de functie voor ontwikkel Hulpprogramma's van Edge toestaan of verbieden.
- **Extensies**: Edge-extensies toestaan of verbieden.
- **InPrivate-Browsing**: InPrivate-Browsing toestaan of verbieden, wat geen geschiedenis of cookies opslaat.
- **WebRTC localhost IP-adres**: Hiermee staat u toe dat het localhost IP-adres van het apparaat wordt weer gegeven wanneer de gebruiker telefoon gesprekken maakt met het web RTC-protocol.
- **Toegang tot about: Flags blok keren**: Hiermee staat u toe dat de gebruiker toegang heeft tot de `about:flags` pagina, die ontwikkel-en experimentele instellingen bevat.
- **SmartScreen-prompt negeren voor bestanden**: Hiermee staat u toe dat de gebruiker de waarschuwingen van het SmartScreen-filter overs Laan over het downloaden van mogelijk schadelijke bestanden.
- **SmartScreen-prompt negeren**: Hiermee staat u toe dat de gebruiker de waarschuwingen van het SmartScreen-filter over mogelijk schadelijke websites kan overs Laan.
- **URL voor eerste uitvoering**: Geef een website op die moet worden weer gegeven wanneer een gebruiker de eerste keer een rand opent.

### <a name="windows-defender-antivirus"></a>Windows Defender Antivirus

Deze instellingen zijn alleen voor apparaten met Windows 10 of hoger.

- **Real-time bewaking toestaan**: Schakel realtime scannen in voor malware, spyware en andere ongewenste software.
- **Gedrags controle toestaan**: Defender controleert op bepaalde bekende patronen van verdachte activiteiten op apparaten.
- **Netwerkinspectiesysteem inschakelen**: de NETWERKINSPECTIESYSTEEM (NIS) helpt bij het beveiligen van apparaten tegen netwerk aanvallen. NIS maakt gebruik van handtekeningen van bekende beveiligingsproblemen uit het Microsoft Endpoint Protection Center om schadelijk netwerkverkeer te detecteren en blokkeren.
- **Alle down loads scannen**: Defender scant alle bestanden die u downloadt van Internet.
- **Scannen van scripts toestaan**: Defender scant de scripts die worden gebruikt in Internet Explorer.
- **Activiteiten van bestanden en Program ma's bewaken**: Defender controleert bestands-en programma-activiteit op apparaten.
  - **Bewaakte bestanden**: Kies het type bestanden dat u wilt bewaken: alle, inkomend of uitgaand.
- **Dagen voor het bijhouden van opgeloste malware**: Defender blijft opgeloste schadelijke software volgen gedurende het aantal dagen dat u opgeeft. Vervolgens kunt u eerder betroffen apparaten hand matig controleren. Als u het aantal dagen instelt op 0, blijft malware in de map quarantaine en wordt niet automatisch verwijderd. De maximum waarde is 90.
- **Toegang tot client gebruikersinterface toestaan**: Hiermee bepaalt u of de gebruikers interface van Defender moet worden verborgen voor gebruikers. Wanneer u deze instelling wijzigt, wordt deze van kracht wanneer het apparaat de volgende keer opnieuw wordt opgestart.
- **Een systeem scan plannen**: Kies een volledige of snelle scan die regel matig wordt uitgevoerd op de dag en tijd die u selecteert:
  - **Geplande dag**: Kies de geplande dag waarop de scan door Defender wordt uitgevoerd.
  - **Geplande tijd**: Kies het geplande tijdstip waarop de scan door Defender wordt uitgevoerd.
- **Een dagelijkse snelle scan plannen**: Kies het geplande tijdstip waarop Defender elke dag een snelle scan uitvoert.
- Het **CPU-gebruik tijdens het scannen beperken**: Stel het percentage van de processor in dat door Defender kan worden gebruikt wanneer er een scan wordt uitgevoerd. Voer een waarde in van 1 tot en met 100.
- **Archief bestanden scannen**: Defender scant gecomprimeerde archieven, zoals zip-of CAB-bestanden.
- **E-mail berichten scannen**: Defender scant e-mail berichten wanneer deze op het apparaat binnenkomen.
- **Verwissel bare stations scannen**: Defender scant Verwissel bare stations, zoals USB-sticks.
- **Toegewezen stations scannen**: met Defender worden de stations gescand die zijn toegewezen aan netwerk shares. `H:`Is bijvoorbeeld toegewezen aan het persoonlijke station van een gebruiker. Als de bestanden op de schijf het kenmerk alleen-lezen hebben, kan Defender de gevonden malware niet verwijderen.
- **Bestanden die zijn geopend vanuit gedeelde mappen op het netwerk scannen**: met Defender worden bestanden gescand wanneer een gebruiker deze opent vanuit een gedeeld netwerkpad. Bijvoorbeeld `\\server\share\file.doc`. Als het bestand op de share alleen-lezen is, kunnen er door Defender gevonden malware niet worden verwijderd.
- **Interval voor handtekening updates**: Kies het tijds interval wanneer Defender op nieuwe handtekening bestanden controleert.
- **Cloud beveiliging toestaan**: Defender gebruikt de micro soft Cloud om informatie over malware-activiteiten te ontvangen en functies zoals blok keren op het eerste gezicht in te scha kelen.
- **Gebruikers vragen voor beelden te verzenden**: Kies het gedrag voor Defender wanneer bestanden mogelijk verdere analyse vereisen. Defender kan bijvoorbeeld automatisch bestanden naar micro soft verzenden om te bepalen of ze schadelijk zijn.
- **Detectie van mogelijk ongewenste toepassingen**: Hiermee wordt het apparaat beschermd tegen het uitvoeren van software die door Defender als mogelijk ongewenst is geclassificeerd. U kunt beveiligen tegen deze toepassingen of de controle modus gebruiken om te rapporteren wanneer een gebruiker een mogelijk ongewenste toepassing installeert.
- **Uitsluitingen van bestanden en**mappen: Voeg een of meer bestanden en mappen toe aan de uitsluitings lijst. Bijvoorbeeld `C:\Path` of `%ProgramFiles%\Path\filename.exe`. Defender bevat deze bestanden en mappen niet in realtime of geplande scans.
- **Uitsluitingen van bestands extensies**: Voeg een of meer bestands extensies toe aan de uitsluitings lijst. Bijvoorbeeld `java` of `exe`. Defender bevat geen bestanden met deze uitbrei dingen in real-time of geplande scans.
- **Uitsluitingen van processen**: Voeg specifieke processen toe aan de uitsluitings lijst. Bijvoorbeeld `C:\path\myproc.exe`. Dit type uitsluiting ondersteunt alleen de volgende extensies: `exe` , `com` of `scr` . Defender bevat deze processen niet in realtime of geplande scans.

### <a name="additional-settings"></a>Aanvullende instellingen

Als u op de pagina **Apparaatinstellingen** van de wizard de optie selecteert voor het **configureren van extra instellingen die niet voor komen in de standaard instellings groepen**, gebruikt u deze **extra instellingen** pagina om deze instellingen te configureren. Selecteer **toevoegen** en kies vervolgens in de lijst met beschik bare mobiele instellingen. Kies **selecteren** om de ingebouwde instelling te wijzigen of maak een **instelling** voor het maken van een aangepaste register waarde of een oma-URI-instellings type.

## <a name="next-steps"></a>Volgende stappen

[Instellingen voor naleving bewaken](../../compliance/deploy-use/monitor-compliance-settings.md)
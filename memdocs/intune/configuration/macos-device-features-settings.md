---
title: Instellingen van apparaatfuncties voor macOS in Microsoft Intune - Azure | Microsoft Docs
description: Zie de instellingen om macOS-apparaten te configureren voor AirPrint en om energie-instellingen op het aanmeldingsvenster van Microsoft Intune weer te geven of te verbergen. Raadpleeg de stappen om het IP-adres, het pad en de poortinstellingen van een AirPrint-server in uw netwerk op te halen. Gebruik deze instellingen in een apparaatconfiguratieprofiel om functies voor macOS-apparaten te configureren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e70952b0d90222bd31a4e9df997d70e9d528ef24
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194195"
---
# <a name="macos-device-feature-settings-in-intune"></a>Instellingen van apparaatfuncties voor macOS in Intune

Intune bevat ingebouwde instellingen om functies op uw macOS-apparaten aan te passen. Zo kunnen beheerders onder meer AirPrint-printers toevoegen, kiezen hoe gebruikers zich aanmelden, de energiebeheerfuncties configureren, verificatie voor eenmalige aanmelding gebruiken.

Gebruik deze functies om macOS-apparaten te beheren als onderdeel van uw Mobile Device Management-oplossing (MDM).

Dit artikel beschrijft deze instellingen en wat elke instelling doet. Het beschrijft tevens de stappen voor het ophalen van het IP-adres, het pad en de poort van AirPrint-printers via de Terminal-app (emulator). Ga voor meer informatie over de functies van het apparaat naar [Instellingen voor iOS-/iPadOS- of macOS-apparaatfuncties toevoegen](device-features-configure.md).

> [!NOTE]
> De gebruikersinterface komt mogelijk niet overeen met de inschrijvingstypen in dit artikel. De informatie in dit artikel is juist. De gebruikersinterface wordt bijgewerkt in een aanstaande release.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een profiel voor macOS-apparaatfuncties](device-features-configure.md).

> [!NOTE]
> Deze instellingen zijn van toepassing op verschillende inschrijvingstypen, waarbij sommige instellingen van toepassing zijn op alle inschrijvingsopties. Zie [macOS-inschrijving](../enrollment/macos-enroll.md) voor meer informatie over de verschillende inschrijvingstypen.

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **AirPrint-doelen**: **Voeg** een of meer AirPrint-printers toe waarmee gebruikers kunnen afdrukken vanaf hun apparaten. Voer ook in:
  - **Poort** (iOS 11.0+, iPadOS 13.0+): Voer de luisterpoort van de AirPrint-bestemming in. Als u deze eigenschap leeg laat, maakt AirPrint gebruik van de standaardpoort.
  - **IP-adres**: voer het IPv4- of IPv6-adres van de printer in. Voer bijvoorbeeld `10.0.0.1` in. Als u hostnamen gebruikt om printers te identificeren, haalt u het IP-adres op door de printer in de Terminal-app te pingen. In [IP-adres en pad ophalen](#get-the-ip-address-and-path) (in dit artikel) vindt u meer informatie.
  - **Pad**: Voer het bronpad van de printer in. Het pad is doorgaans `ipp/print` voor printers in uw netwerk. In [IP-adres en pad ophalen](#get-the-ip-address-and-path) (in dit artikel) vindt u meer informatie.
  - **TLS** (iOS 11.0+, iPadOS 13.0+): Uw opties zijn:
    - **Nee** (standaard): Transport Layer Security (TLS) wordt niet afgedwongen wanneer verbinding wordt gemaakt met AirPrint-printers.
    - **Ja**: AirPrint-verbindingen worden beveiligd met TLS (Transport Layer Security).

- **Importeer** een door komma's gescheiden bestand (.csv) met een lijst van AirPrint-printers. Nadat u AirPrint-printers aan Intune hebt toegevoegd, kunt u bovendien deze lijst **exporteren**.

### <a name="get-the-ip-address-and-path"></a>IP-adres en pad ophalen

Om AirPrinter-servers toe te voegen, hebt u het IP-adres van de printer, het bronpad en de poort nodig. De volgende stappen laten zien hoe u aan deze informatie komt.

1. Open op een Mac die verbonden is met hetzelfde lokale netwerk (subnet) als de AirPrint-printers de **terminal** (via **/Programma's/Hulpprogramma's**).
2. Typ in de Terminal-app `ippfind` en selecteer Enter.

    Noteer de printergegevens. Er wordt bijvoorbeeld iets in de trant van `ipp://myprinter.local.:631/ipp/port1` geretourneerd. Het eerste deel is de naam van de printer. Het laatste deel (`ipp/port1`) is het bronpad.

3. Typ in de terminal `ping myprinter.local` en selecteer Enter.

   Noteer het IP-adres. Er wordt bijvoorbeeld iets in de trant van `PING myprinter.local (10.50.25.21)` geretourneerd.

4. Gebruik de waarden van het IP-adres en het bronpad. In dit voorbeeld is het IP-adres `10.50.25.21` en het bronpad `/ipp/port1`.

## <a name="associated-domains"></a>Gekoppelde domeinen

In Intune kunt u het volgende doen:

- Een groot aantal app-naar-domein-koppelingen toevoegen.
- Een groot aantal domeinen koppelen aan dezelfde app.

Deze functie is van toepassing op:

- macOS 10.15 of hoger

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Door de gebruiker goedgekeurde apparaatinschrijving en automatische apparaatregistratie

- **Gekoppelde domeinen**: **Voeg een koppeling toe** tussen uw domein en een app. Door deze functie worden aanmeldingsreferenties tussen een contoso-app en een contoso-website gedeeld. Voer ook in:

  - **App-id**: voer de app-id in van de app die u aan een website wilt koppelen. De app-id bevat de team-id en een bundel-id: `TeamID.BundleID`.

    De team-id is een alfanumerieke tekenreeks van 10 tekens (letters en cijfers) die door Apple wordt gegenereerd voor uw app-ontwikkelaars, zoals `ABCDE12345`. [Zoek uw team-id](https://help.apple.com/developer-account/#/dev55c3c710c) : (opent de website van Apple) biedt meer informatie.

    De bundel-id is een unieke identificatie van de app en heeft doorgaans de omgekeerde notatie van de domeinnaam. De bundel-id van Finder is bijvoorbeeld `com.apple.finder`. Gebruik het AppleScript in Terminal om de bundel-id te vinden:

    `osascript -e 'id of app "ExampleApp"'`

  - **Domein**: voer het websitedomein in dat u aan een app wilt koppelen. Het domein bevat een servicetype en een volledig gekwalificeerde hostnaam, zoals `webcredentials:www.contoso.com`.

    U kunt alle subdomeinen van een gekoppeld domein vergelijken door `*.` (een asterisk-jokerteken en een punt) vóór het domein in te voeren. De punt is vereist. Exacte domeinen hebben een hogere prioriteit dan domeinen met een jokerteken. Patronen van bovenliggende domeinen worden vergeleken *als* er geen overeenkomst wordt gevonden in het volledig gekwalificeerde subdomein.

    Mogelijke servicetypen zijn:

    - **authsrv**: App-extensie voor eenmalige aanmelding
    - **applink**: Universele koppeling
    - **webcredentials**: Automatisch invullen van wachtwoorden

> [!TIP]
> Als u problemen wilt oplossen, opent u **Systeemvoorkeuren** > **Profielen** op uw macOS-apparaat. Controleer of het profiel dat u hebt gemaakt, voorkomt in de lijst met apparaatprofielen. Zo ja, dan controleert u of de **configuratie voor gekoppelde domeinen** in het profiel voorkomt en de juiste app-id en domeinen bevat.

## <a name="content-caching"></a>Cacheopslag van inhoud

In cacheopslag van inhoud wordt een lokale kopie van de inhoud bewaard. Deze informatie kan worden opgehaald door andere Apple-apparaten zonder verbinding te maken met internet. Met dit opslaan in cache worden downloads versneld doordat software-updates, apps, foto's en andere inhoud de eerste keer dat ze worden gedownload, worden opgeslagen. Omdat apps eenmaal worden gedownload en gedeeld met andere apparaten, besparen scholen en organisaties met veel apparaten bandbreedte.

> [!NOTE]
> Gebruik slechts één profiel voor deze instellingen. Als u meerdere profielen met deze instellingen toewijst, treedt er een fout op.
>
> Zie [Logboeken en statistieken over cacheopslag van inhoud weergeven](https://support.apple.com/guide/mac-help/view-content-caching-logs-statistics-mac-mchl0d8533cd/10.15/mac/10.15) (opent de website van Apple) voor meer informatie over het bewaken van cacheopslag van inhoud.

Deze functie is van toepassing op:

- macOS 10.13.4 en hoger

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

Raadpleeg [Nettoladinginstellingen voor cacheopslag van inhoud](https://support.apple.com/guide/mdm/content-caching-mdm163612d39/1/web/1) (hiermee opent u de website van Apple) voor meer informatie over deze instellingen.

**Cacheopslag van inhoud inschakelen**: Met **Ja** wordt cacheopslag van inhoud ingeschakeld; gebruikers kunnen dit niet uitschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem dit uitschakelen.

- **Type inhoud dat moet worden opgeslagen in de cache**: Uw opties zijn:
  - **Alle inhoud**: Slaat iCloud-inhoud en gedeelde inhoud op in de cache.
  - **Allen gebruikersinhoud**: Slaat iCloud-inhoud, waaronder foto's en documenten, op in de cache.
  - **Alleen gedeelde inhoud**: Slaat apps en software-updates op in de cache.

- **Maximumcachegrootte**: Voer de maximale hoeveelheid schijfruimte (in bytes) in die wordt gebruikt voor het opslaan van inhoud in de cache. Als u dit leeg laat (standaard), wordt deze instelling niet gewijzigd of bijgewerkt door Intune. Standaard kan het besturingssysteem deze waarde instellen op nul (`0`) bytes, wat leidt tot onbeperkte schijfruimte voor de cache.

  Zorg ervoor dat u de beschikbare ruimte op de apparaten niet overschrijdt. Zie [Hoe iOS en macOS de opslagcapaciteit rapporteren](https://support.apple.com/HT201402) (opent de website van Apple) voor meer informatie over de opslagcapaciteit van het apparaat.

- **Locatie van cache**: Geef het pad op waarin u de inhoud in de cache wilt opslaan. De standaardlocatie is `/Library/Application Support/Apple/AssetCache/Data`. Het wordt aangeraden deze locatie niet te wijzigen.

  Als u deze instelling wijzigt, wordt de inhoud in de cache niet verplaatst naar de nieuwe locatie. Gebruikers moeten de locatie op het apparaat wijzigen (**Systeemvoorkeuren** > **Delen** > **Cacheopslag van inhoud**) om het automatisch te verplaatsen.

- **Poort**: Voer het TCP-poortnummer in op apparaten voor de cache om aanvragen voor downloaden en uploaden te accepteren, van 0-65535. Geef nul (`0`) (standaard) op om een willekeurige, beschikbare poort te gebruiken.
- **Internetverbinding en delen van inhoud in cache blokkeren**: Dit wordt ook 'getethered opslaan in cache' genoemd. **Ja** verhindert delen van de internetverbinding en voorkomt dat inhoud in de cache wordt gedeeld met iOS/iPadOS-apparaten die via USB zijn verbonden met hun Mac. Gebruikers kunnen deze functie niet inschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

- **Het delen van een internetverbinding inschakelen**: Dit wordt ook 'getethered opslaan in cache' genoemd. Met **Ja** staat u delen van de internetverbinding toe en staat u toe dat inhoud in de cache wordt gedeeld met iOS/iPadOS-apparaten die via USB zijn verbonden met hun Mac. Gebruikers kunnen deze functie niet uitschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem dit uitschakelen.

  Deze functie is van toepassing op:

  - macOS 10.15.4 en hoger

- **Cache inschakelen voor het registreren van clientgegevens**: Met **Ja** registreert u het IP-adres en het poortnummer van de apparaten waarvandaan inhoud wordt opgevraagd. Als u problemen met het apparaat wilt oplossen, kan dit logboekbestand helpen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het kan zijn dat het besturingssysteem standaard deze informatie niet weergeeft op de menubalk.

- **Inhoud van de cache altijd behouden, zelfs wanneer het systeem schijfruimte nodig heeft voor andere apps**: Met **Ja** bewaart u de cache-inhoud en zorgt u ervoor dat er niets wordt verwijderd, zelfs niet wanneer er weinig schijfruimte is. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem inhoud van de cache automatisch leegmaken wanneer er opslagruimte nodig is voor andere apps.

  Deze functie is van toepassing op:

  - macOS 10.15 of hoger

- **Statuswaarschuwingen weergeven**: Met **Ja** worden waarschuwingen als systeemmeldingen weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard worden deze waarschuwingen in het besturingssysteem mogelijk niet weergegeven als systeemmeldingen.

  Deze functie is van toepassing op:

  - macOS 10.15 of hoger

- **Voorkomen dat het apparaat naar slaapstand schakelt terwijl caching is ingeschakeld**: Met **Ja** voorkomt u dat de computer in de slaapstand gaat wanneer opslaan in cache is ingeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat het apparaat in de slaapstand gaat.

  Deze functie is van toepassing op:

  - macOS 10.15 of hoger

- **Apparaten die in de cache moeten worden opgeslagen**: Kies de apparaten die inhoud kunnen opslaan in de cache. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. 
  - **Apparaten die gebruikmaken van hetzelfde lokale netwerk**: De inhoudscache biedt inhoud aan apparaten in hetzelfde directe lokale netwerk. Er wordt geen inhoud aangeboden aan apparaten op andere netwerken, inclusief apparaten die bereikbaar zijn voor de inhoudscache.
  - **Apparaten die gebruikmaken van hetzelfde openbare IP**: De inhoudscache biedt inhoud aan apparaten die gebruikmaken van hetzelfde openbare IP. Er wordt geen inhoud aangeboden aan apparaten op andere netwerken, inclusief apparaten die bereikbaar zijn voor de inhoudscache.
  - **Apparaten die aangepaste lokale netwerken gebruiken**: De inhoudscache biedt inhoud aan apparaten in de IP-bereiken die u invoert.
    - **Luisterbereiken van clients**: Voer het bereik in van IP-adressen die de inhoudscache kunnen ontvangen.
  - **Apparaten die aangepaste lokale netwerken gebruiken met terugval**: De inhoudscache biedt inhoud aan apparaten in de luisterbereiken, de luisterbereiken van de peer en bovenliggende IP-adressen.
    - **Luisterbereiken van clients**: Voer het bereik in van IP-adressen die de inhoudscache kunnen ontvangen.

- **Aangepaste openbare IP-adressen**: Voer een bereik van openbare IP-adressen in. De cloudservers gebruiken dit bereik om clientapparaten te koppelen aan caches.

- **Inhoud delen met andere caches**: Wanneer uw netwerk meer dan één inhoudscache heeft, worden de inhoudscaches op andere apparaten automatisch peers. Deze apparaten kunnen software in de cache raadplegen en delen. 

  Wanneer een aangevraagd item niet beschikbaar is in een inhoudscache, worden de peers gecontroleerd op het item. Als het item beschikbaar is, wordt het gedownload uit de inhoudscache op het peer-apparaat. Als het nog steeds niet beschikbaar is, downloadt de inhoudscache het item van:

  - Een bovenliggend IP-adres, indien een is geconfigureerd
  
    OF
    
  - van Apple via internet

  Wanneer er meer dan één inhoudscache beschikbaar is, selecteren apparaten automatisch de juiste inhoudscache. 

  Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Inhoudscaches die gebruikmaken van hetzelfde lokale netwerk**: Inhoudscache maakt alleen een peer-verbinding met andere inhoudscaches op hetzelfde lokale netwerk.
  - **Inhoudscaches die gebruikmaken van hetzelfde openbare IP**: Inhoudscache maakt alleen een peer-verbinding met andere inhoudscaches op hetzelfde openbare IP.
  - **Inhoudscaches die aangepaste lokale netwerken gebruiken**: Inhoudscache maakt alleen een peer-verbinding met andere inhoudscaches in het luisterbereik van het IP-adres dat u invoert:

    - **Luisterbereiken van peers**: Voer de begin- en eind-IP-adressen van IPv4 of IPv6 in voor uw bereik. De inhoudscache reageert alleen op cacheaanvragen van peers van inhoudscaches in de IP-adresbereiken die u invoert.
    - **Filterbereiken van peers**: Voer de begin- en eind-IP-adressen van IPv4 of IPv6 in voor uw bereik. De inhoudscache filtert de lijst met peers op basis van de IP-adresbereiken die u invoert.

- **Bovenliggende IP-adressen**: Voer het lokale IP-adres van een andere inhoudscache in om toe te voegen als een bovenliggende cache. Uw cache uploadt en downloadt inhoud naar deze caches, in plaats van ze rechtstreeks met Apple te uploaden/downloaden. Voeg maar eenmaal een bovenliggend IP-adres toe.
- **Selectiebeleid bovenliggende cache**: Wanneer er veel bovenliggende caches zijn, selecteert u hoe het bovenliggende IP-adres wordt gekozen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Round robin**: Gebruik de bovenliggende IP-adressen op volgorde. Deze optie is geschikt voor scenario's met taakverdeling.
  - **Eerst beschikbare**: Gebruik altijd het eerste beschikbare IP-adres in de lijst.
  - **Hash**: Hiermee maakt u een hash-waarde voor het padgedeelte van de aangevraagde URL. Deze optie zorgt ervoor dat hetzelfde bovenliggende IP-adres altijd wordt gebruikt voor dezelfde URL.
  - **Willekeurig**: Willekeurig een IP-adres in de lijst gebruiken. Deze optie is geschikt voor scenario's met taakverdeling.
  - **Plaknotitie beschikbaar**: Gebruik altijd het eerste IP-adres in de lijst. Als deze niet beschikbaar is, gebruikt u het tweede IP-adres in de lijst. Ga verder met het tweede IP-adres totdat het niet beschikbaar is, enzovoort.

## <a name="login-items"></a>Aanmeldingsitems

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **De bestanden, mappen en aangepaste apps toevoegen die worden gestart bij het aanmelden**: U kunt het pad van een bestand, map, aangepaste app of systeem-app **toevoegen**  dat u wilt openen wanneer gebruikers zich aanmelden bij hun apparaten. Voer ook in:

  - **Pad van item**: Voer het pad naar het bestand, de map of de app in. Systeem-apps of apps die zijn gebouwd of aangepast voor uw organisatie, bevinden zich doorgaans in de map `Applications` en hebben een pad dat er als volgt uitziet: `/Applications/AppName.app`.

    U kunt een groot aantal bestanden, mappen en apps toevoegen. Voer bijvoorbeeld het volgende in:  
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    Let erop dat u het juiste pad opgeeft bij het toevoegen van een app, map of bestand. Niet alle items bevinden zich in de map `Applications`. Als gebruikers een item naar een andere locatie verplaatsen, verandert het pad. Dit verplaatste item wordt niet geopend wanneer de gebruiker zich aanmeldt.

  - **Verbergen**: Kies of u wilt dat de app wordt weergegeven of verborgen. Uw opties zijn:
    - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Het besturingssysteem kant standaard items weergeven in de lijst met aanmeldingsitems voor gebruikers en groepen wanneer de optie voor verbergen is uitgeschakeld.
    - **Ja**: De app wordt niet weergegeven in de lijst met aanmeldingsitems voor gebruikers en groepen.

## <a name="login-window"></a>Aanmeldingsvenster

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Aanvullende informatie op de menubalk weergeven**: Wanneer het tijdgebied op de menubalk wordt geselecteerd, worden met **Ja** de hostnaam en macOS-versie getoond. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het kan zijn dat het besturingssysteem standaard deze informatie niet weergeeft op de menubalk.
- **Banner**: Voer een bericht in dat op het aanmeldingsscherm van apparaten wordt weergegeven. Voer bijvoorbeeld gegevens over uw organisatie, een welkomstbericht, informatie over gevonden voorwerpen, enzovoort in.
- **Tekstvelden voor gebruikersnaam en wachtwoord vereisen**: kies hoe gebruikers zich aanmelden op apparaten. Met **Ja** vereist u dat gebruikers een gebruikersnaam en wachtwoord invoeren. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard vereist het besturingssysteem mogelijk dat gebruikers hun gebruikersnaam selecteren in een lijst en vervolgens hun wachtwoord typen.

  Voer ook in:

  - **Lokale gebruikers verbergen**: Met **Ja** worden de lokale gebruikersaccounts niet weergegeven in de lijst met gebruikers, waaronder mogelijk de standaard- en beheerdersaccounts. Alleen de netwerk- en systeemgebruikersaccounts worden weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard de lokale gebruikersaccounts weergeven in de lijst met gebruikers.
  - **Mobiele accounts verbergen**: Met **Ja** worden mobiele accounts niet weergegeven in de lijst met gebruikers. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard de mobiele accounts weergeven in de lijst met gebruikers. Sommige mobiele accounts worden mogelijk weergegeven als netwerkgebruikers.
  - **Netwerkgebruikers weergeven**: Selecteer **Ja** om de netwerkgebruikers in de lijst met gebruikers weer te geven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het kan zijn dat het besturingssysteem standaard de netwerkgebruikersaccounts niet weergeeft in de lijst met gebruikers.
  - **Beheerders van de computer verbergen**: Met **Ja** worden de gebruikersaccounts met beheerdersrechten niet weergegeven in de lijst met gebruikers. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard de gebruikersaccounts met beheerdersrechten weergeven in de lijst met gebruikers.
  - **Alle andere gebruikers weergeven**: Selecteer **Ja** om de **Andere...** gebruikers weer te geven in de lijst met gebruikers. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem geeft mogelijk standaard de andere gebruikersaccounts niet weer in de lijst met gebruikers.

- **De knop Afsluiten verbergen**: Met **Ja** wordt de knop Afsluiten niet weergegeven op het aanmeldingsscherm. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard de knop Afsluiten weergeven.
- **De knop Opnieuw opstarten verbergen**: Met **Ja** wordt de knop Opnieuw opstarten niet weergegeven op het aanmeldingsscherm. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard de knop Opnieuw opstarten weergeven.
- **De slaapstandknop verbergen**: Met **Ja** wordt de knop Slaapstand niet weergegeven op het aanmeldingsscherm. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard de knop Slaapstand weergeven.
- **Gebruikersaanmelding via console uitschakelen**: Met **Ja** wordt de macOS-opdrachtregel verborgen die wordt gebruikt voor aanmelding. Voor standaardgebruikers kunt u deze instelling het beste op **Ja** instellen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat geavanceerde gebruikers zich aanmelden via de macOS-opdrachtregel. Om de consolemodus in te schakelen moeten gebruikers `>console` invoeren in het veld Gebruikersnaam en zich verifiëren in het consolevenster.
- **Afsluiten actieve aanmelding uitschakelen**: Met **Ja** wordt voorkomen dat gebruikers na aanmelding de optie **Afsluiten** selecteren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers de menuopdracht **Afsluiten** selecteren op apparaten.
- **Opnieuw opstarten tijdens actieve aanmelding uitschakelen**: Met **Ja** wordt voorkomen dat gebruikers na aanmelding de optie **Opnieuw opstarten** selecteren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers de menuopdracht **Opnieuw opstarten** selecteren op apparaten.
- **Uitschakelen tijdens actieve aanmelding uitschakelen**: Met **Ja** wordt voorkomen dat gebruikers na aanmelding de optie **Uitschakelen** selecteren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers de menuopdracht **Uitschakelen** selecteren op apparaten.
- **Afmelden tijdens actieve aanmelding uitschakelen** (macOS 10.13 of hoger): Met **Ja** wordt voorkomen dat gebruikers na aanmelding de optie **Afmelden** selecteren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers de menuopdracht **Afmelden** selecteren op apparaten.
- **Vergrendelingsscherm tijdens actieve aanmelding uitschakelen** (macOS 10.13 of hoger): Met **Ja** wordt voorkomen dat gebruikers na aanmelding de optie **Vergrendelingsscherm** selecteren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers de menuopdracht **Vergrendelingsscherm** selecteren op apparaten.

## <a name="single-sign-on-app-extension"></a>App-extensie voor eenmalige aanmelding

Deze functie is van toepassing op:

- macOS 10.15 of hoger

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Door de gebruiker goedgekeurde apparaatinschrijving en automatische apparaatregistratie

- **Type app-extensie voor eenmalige aanmelding**: Kies het type app-extensie voor eenmalige aanmelding. Uw opties zijn:

  - **Niet geconfigureerd**: er worden geen app-extensies gebruikt. Als u een app-extensie wilt uitschakelen, stelt u het type app-extensie voor SSO in op **Niet geconfigureerd**.
  - **Microsoft Azure AD**: 

    > [!IMPORTANT]
    > De Microsoft Azure AD-extensie voor eenmalige aanmelding is nog steeds in ontwikkeling. De extensie wordt vermeld in de Intune-gebruikersinterface, maar werkt niet zoals verwacht. Gebruik **Microsoft Azure AD** niet voor het type app-extensie voor eenmalige aanmelding.

    Maakt gebruik van de SSO-invoegtoepassing van Microsoft Enterprise. Dat is een omleidingstype-SSO-app-extensie. Deze invoegtoepassing biedt SSO voor Active Directory-accounts voor alle macOS-toepassingen die ondersteuning bieden voor de functie [Enterprise Single Sign-On van Apple](https://developer.apple.com/documentation/authenticationservices). Gebruik dit SSO-app-extensietype om SSO in te schakelen voor Microsoft-apps, organisatie-apps en websites die worden geverifieerd met behulp van Azure AD.

    De Azure AD-invoegtoepassing fungeert als een geavanceerde broker voor verificatie die verbeteringen in de beveiliging en de gebruikerservaring biedt.

    > [!IMPORTANT]
    > Installeer de macOS-bedrijfsportal-app op apparaten om eenmalige aanmelding te verkrijgen met het SSO-app-extensietype van Microsoft Azure AD. De bedrijfsportal-app levert de Microsoft Enterprise invoegtoepassing voor eenmalige aanmelding op apparaten. De instellingen van de MDM app-extensie voor eenmalige aanmelding activeren de invoegtoepassing. Zodra de bedrijfsportal-app en het profiel van de app-extensie voor eenmalige aanmelding op apparaten zijn geïnstalleerd, melden gebruikers zich aan met hun referenties en maken een sessie op hun apparaat. Deze sessie wordt voor verschillende toepassingen gebruikt, zonder dat gebruikers opnieuw moeten worden geverifieerd.
    >
    > Zie [Wat gebeurt er wanneer ik de bedrijfsportal-app installeer en mijn macOS-apparaat registreer bij Intune?](../user-help/what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md) voor meer informatie over de bedrijfsportal-app. De bedrijfsportal-app [downloaden](https://go.microsoft.com/fwlink/?linkid=853070).

  - **Omleiding**: Gebruik een algemene, aanpasbare app-extensie van het type Omleiding om eenmalige aanmelding te gebruiken met moderne verificatiestromen. Zorg ervoor dat u de extensie- en team-id van de app-extensie van uw organisatie kent.
  - **Referentie**: Gebruik een algemene, aanpasbare app-extensie van het type Referentie om eenmalige aanmelding te gebruiken met verificatiestromen met vraag en antwoord. Zorg ervoor dat u de extensie-id en de team-id van de app-extensie van uw organisatie kent.  
  - **Kerberos**: gebruik de ingebouwde Kerberos-extensie van Apple, die is opgenomen in macOS Catalina 10.15 en hoger. Deze optie is een Kerberos-versie van de app-extensie **Referentie**.

  > [!TIP]
  > Met de typen **Omleiding** en **Referentie** voegt u uw eigen configuratiewaarden toe om door te geven aan de extensie. Als u het type **Referentie** gebruikt, kunt u overwegen om de ingebouwde configuratie-instellingen te gebruiken die Apple heeft opgenomen in het type **Kerberos**.

- **Extensie-id** (omleiding, referentie): voer de bundel-id in waarmee de app-extensie voor eenmalige aanmelding wordt aangeduid, zoals `com.apple.ssoexample`.
- **Team-id** (omleiding, referentie): voer de team-id in van uw app-extensie voor eenmalige aanmelding. Een team-id is een alfanumerieke tekenreeks van 10 tekens (cijfers en letters) die wordt gegenereerd met Apple, zoals `ABCDE12345`. 

  [Zoek uw team-id](https://help.apple.com/developer-account/#/dev55c3c710c): (hiermee wordt de website van Apple geopend) biedt meer informatie.

- **Realm** (referentie, Kerberos): Voer de naam van uw verificatierealm in. De realmnaam moet in hoofdletters zijn, zoals `CONTOSO.COM`. Uw realmnaam is meestal gelijk aan uw DNS-domeinnaam, maar dan met alleen hoofdletters.

- **Domeinen** (referentie, Kerberos): voer de domein- of hostnamen in van de sites die via eenmalige aanmelding kunnen worden geverifieerd. Als bijvoorbeeld `mysite.contoso.com` uw website is, is `mysite` de hostnaam en is `contoso.com` de domeinnaam. Wanneer gebruikers verbinding maken met een van deze sites, wordt de verificatie-uitdaging afgehandeld via de app-extensie. Met deze verificatie kunnen gebruikers Face ID, Touch ID of de pincode/wachtwoordcode van Apple gebruiken om zich aan te melden.

  - Alle domeinen in uw app-extensie voor eenmalige aanmelding bij Intune-profielen moeten uniek zijn. U kunt een domein niet herhalen in een app-extensieprofiel voor eenmalige aanmelding, zelfs niet als u verschillende typen app-extensie voor SSO gebruikt.
  - Deze domeinen zijn niet hoofdlettergevoelig.

- **URL's** (alleen omleiden): Voer de URL-voorvoegsels van uw id-providers in namens wie de eenmalige aanmelding de app-extensie van het type Omleiding gebruikt. Wanneer gebruikers worden omgeleid naar deze URL's, grijpt de app-extensie voor eenmalige aanmelding in en wordt er om eenmalige aanmelding gevraagd.

  - Alle URL's in uw app-extensie voor SSO bij Intune-profielen moeten uniek zijn. U kunt een domein niet herhalen in een app-extensieprofiel voor eenmalige aanmelding, zelfs niet als u verschillende typen app-extensies voor eenmalige aanmelding gebruikt.
  - De URL's moeten beginnen met `http://` of `https://`.

- **Aanvullende configuratie** (Microsoft Azure AD, omleiding, referentie): Voer aanvullende extensiegegevens in die moeten worden doorgegeven aan de app-extensie voor eenmalige aanmelding:
  - **Sleutel**: voer de naam in van het item dat u wilt toevoegen, zoals `user name`.
  - **Type**: voer het gegevenstype in. Uw opties zijn:

    - Tekenreeks
    - Booleaanse waarde: voer `True` of `False` in bij **Configuratiewaarde**.
    - Geheel getal: voer een getal in bij **Configuratiewaarde**.

  - **Waarde**: voer de gegevens in.
  
  - **Toevoegen**: selecteer deze optie om uw configuratiesleutels toe te voegen.

- **Gebruik van sleutelhanger** (alleen Kerberos): kies **Blokkeren** om te voorkomen dat wachtwoorden worden opgeslagen in de sleutelhanger. Als deze optie is geblokkeerd, wordt gebruikers niet gevraagd om het wachtwoord op te slaan. Het wachtwoord moet opnieuw worden ingevoerd wanneer het Kerberos-ticket verloopt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat wachtwoorden worden opgeslagen in de sleutelketen. Gebruikers worden niet gevraagd om hun wachtwoord opnieuw in te voeren wanneer het ticket verloopt.
- **Face ID, Touch ID of wachtwoordcode** (alleen Kerberos): **Vereisen**: gebruikers moeten hun Face ID, Touch ID of de wachtwoordcode van het apparaat invoeren wanneer de referentie nodig is om het Kerberos-ticket te vernieuwen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het kan zijn dat het besturingssysteem standaard niet vereist dat gebruikers biometrische gegevens of wachtwoordcode gebruiken om het Kerberos-ticket te vernieuwen. Als **Gebruik van sleutelhanger** is geblokkeerd, is deze instelling niet van toepassing.
- **Standaardrealm** (alleen Kerberos): kies **Inschakelen** om de waarde voor **Realm** in te stellen die u hebt ingevoerd als de standaardrealm. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het kan zijn dat het besturingssysteem standaard geen realm instelt.

  > [!TIP]
  > - U moet deze instelling **inschakelen** als u meerdere app-extensies voor SSO bij Kerberos configureert in uw organisatie.
  > - U kunt deze instelling **inschakelen** als u meerdere realms gebruikt. Hiermee stelt u de waarde voor **Realm** in die u hebt ingevoerd als de standaardrealm.
  > - Als u slechts één realm hebt, laat u deze ingesteld op **Niet geconfigureerd** (standaard).

- **Automatische detectie** (alleen Kerberos): als deze optie is ingesteld op **Blokkeren**, maakt de Kerberos-extensie niet automatisch gebruik van LDAP en DNS om de Active Directory-sitenaam te bepalen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat de extensie automatisch naar de Active Directory-sitenaam zoekt.
- **Wachtwoordwijzigingen** (alleen Kerberos): **Blokkeren** voorkomt dat gebruikers de wachtwoorden kunnen wijzigen waarmee ze zich aanmelden bij de door u ingevoerde domeinen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard wachtwoordwijzigingen toestaan.  
- **Wachtwoordsynchronisatie** (alleen Kerberos): kies **Inschakelen** om de lokale wachtwoorden van de gebruikers te synchroniseren met Azure AD. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard wachtwoordsynchronisatie met Azure AD uitschakelen. Gebruik deze instelling als alternatief of als back-up voor SSO. Deze instelling werkt niet als gebruikers zijn aangemeld met een mobiel Apple-account.
- **Active Directory-wachtwoordcomplexiteit van Windows Server** (alleen Kerberos): Kies **Vereisen** zodat gebruikerswachtwoorden moeten voldoen aan de vereisten voor wachtwoordcomplexiteit van Active Directory. Zie [Wachtwoorden moeten voldoen aan complexiteitsvereisten](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements) voor meer informatie. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het kan zijn dat het besturingssysteem standaard niet vereist dat gebruikers moeten voldoen aan de wachtwoordvereisten van Active Directory.
- **Minimale wachtwoordlengte** (alleen Kerberos): Voer het minimum aantal tekens in dat wachtwoorden van gebruikers moeten bevatten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het kan zijn dat het besturingssysteem standaard geen minimumwachtwoordlengte afdwingt voor de gebruikers.
- **Limiet voor het opnieuw gebruiken van een wachtwoord** (alleen Kerberos): Voer het aantal nieuwe wachtwoorden in, van 1 tot 24, die worden gebruikt voordat een eerder gebruikt wachtwoord opnieuw kan worden gebruikt in het domein. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het kan zijn dat het besturingssysteem standaard geen limiet voor het opnieuw gebruiken van wachtwoorden afdwingt.
- **Minimale gebruiksduur wachtwoord** (alleen Kerberos): Voer het aantal dagen in dat een wachtwoord wordt gebruikt in het domein voordat gebruikers dit kunnen wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het kan zijn dat het besturingssysteem standaard geen minimumduur voor wachtwoorden afdwingt waarna deze kunnen worden gewijzigd.
- **Melding voor verlopen van wachtwoord** (alleen Kerberos): voer het aantal dagen vóór het verlopen van een wachtwoord in wanneer gebruikers op de hoogte worden gesteld dat hun wachtwoord zal verlopen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard `15` dagen gebruiken.
- **Wachtwoordverlooptijd** (alleen Kerberos): Geef op na hoeveel dagen het wachtwoord voor het apparaat moet veranderen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het kan zijn dat het besturingssysteem standaard nooit wachtwoorden laat verlopen.
- **URL voor het wijzigen van het wachtwoord** (alleen Kerberos): Voer de URL in die wordt geopend wanneer gebruikers een Kerberos-wachtwoord willen wijzigen.
- **Principal-naam** (alleen Kerberos): voer de gebruikersnaam in van de Kerberos-principal. U hoeft de realmnaam niet op te nemen. In `user@contoso.com` is `user` bijvoorbeeld de principal-naam en `contoso.com` de realmnaam.

  > [!TIP]
  > - U kunt ook variabelen gebruiken in de principal-naam door accolades `{{ }}` in te voeren. Voer bijvoorbeeld `Username: {{username}}` in om de gebruikersnaam weer te geven. 
  > - Wees echter voorzichtig met het vervangen van variabelen, want variabelen worden niet gevalideerd in de UI en zijn hoofdlettergevoelig. Zorg dat u de juiste informatie invoert.
  
- **Active Directory-sitecode** (alleen Kerberos): voer de naam in van de Active Directory-site die door de Kerberos-extensie moet worden gebruikt. Waarschijnlijk hoeft u deze waarde niet te wijzigen, omdat de Kerberos-extensie de Active Directory-sitecode mogelijk automatisch kan vinden.
- **Cachenaam** (alleen Kerberos): voer de naam in van de generieke beveiligingsservices (Generic Security Services of GSS) van de Kerberos-cache. Waarschijnlijk hoeft u deze waarde niet in te stellen.  
- **Bericht voor wachtwoordvereisten** (alleen Kerberos): voer een tekstversie in van de wachtwoordvereisten van uw organisatie die voor gebruikers worden weergegeven. Het bericht wordt weergegeven als u geen vereisten voor wachtwoordcomplexiteit van Active Directory nodig hebt of geen minimale wachtwoordlengte opgeeft.  
- **Modus Gedeeld apparaat** inschakelen (alleen Microsoft Azure AD): Selecteer **Ja** als u de SSO-invoegtoepassing van Microsoft Enterprise implementeert op macOS-apparaten die zijn geconfigureerd voor de modus Gedeeld apparaat van Azure AD. Met apparaten in de gedeelde modus kunnen veel gebruikers zich globaal aan- en afmelden bij toepassingen die de modus Gedeeld apparaat ondersteunen. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt. 

  Als dit is ingesteld op **Ja**, dan worden alle bestaande gebruikersaccounts van de apparaten gewist. Als u gegevensverlies of het herstellen van fabrieksinstellingen wilt voorkomen, moet u weten hoe deze instelling uw apparaten wijzigt.

  Zie [Overzicht van de modus voor gedeelde apparaten](/azure/active-directory/develop/msal-shared-devices) voor meer informatie over de modus gedeeld apparaat.

- **Bundel-id’s van app** (Microsoft Azure AD, Kerberos): **voeg de app-bundel-id's toe** die moeten gebruikmaken van eenmalige aanmelding op uw apparaten. Aan deze apps wordt toegang verleend tot Kerberos Ticket Granting Ticket en het verificatieticket. De apps verifiëren gebruikers ook voor services waarvoor ze gemachtigd zijn.
- **Toewijzing aan domeinrealm** (alleen Kerberos): **voeg de DNS-achtervoegsels voor het domein toe** die moeten worden toegewezen aan uw realm. Gebruik deze instelling als de DNS-namen van de hosts niet overeenkomen met de realmnaam. Waarschijnlijk hoeft u deze aangepaste domein-naar-realm-toewijzing niet te maken.
- **PKINIT-certificaat** (alleen Kerberos): **selecteer** het PIKNIT-certificaat (Public Key Cryptography for Initial Authentication) dat kan worden gebruikt voor Kerberos-verificatie. U kunt kiezen uit een [PKCS](../protect/certficates-pfx-configure.md)- of [SCEP](../protect/certificates-scep-configure.md)-certificaat dat u hebt toegevoegd in Intune. Raadpleeg [Certificaten gebruiken voor verificatie in Microsoft Intune](../protect/certificates-configure.md) voor meer informatie over certificaten.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook apparaatfuncties configureren in [iOS/iPadOS](ios-device-features-settings.md).
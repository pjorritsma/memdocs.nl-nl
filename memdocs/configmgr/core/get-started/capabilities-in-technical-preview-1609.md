---
title: Mogelijkheden van Technical Preview 1609
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1609.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 9d58ffee30986efeda1716358ab7aa6c1d36cbf5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695678"
---
# <a name="capabilities-in-technical-preview-1609-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1609 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*



Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1609. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site.      Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    

**Bekende problemen in deze technische preview:**  
*  Wanneer u bijwerkt naar de Configuration Manager 1609 Technical Preview, worden de editie-upgrade beleid verwijderd die u hebt geïmplementeerd. Als u deze beleids regels wilt blijven gebruiken, moet u ze opnieuw maken en implementeren.


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

## <a name="improvements-to-endpoint-protection"></a>Verbeteringen in Endpoint Protection
Verbetering van Endpoint Protection antimalware-beleids instellingen: u kunt nu het niveau opgeven waarop de Endpoint Protection Cloud Protection-Service verdachte bestanden blokkeert. Met een nieuwe instelling kunnen beheerders "Risk ante" computers opgeven op basis van de grote aantallen malware die ze tegen komen.

## <a name="increased-number-of-enrolled-devices"></a>Uitgebreid aantal geregistreerde apparaten
Beheerders kunnen gebruikers nu in staat stellen om Maxi maal 15 apparaten in te schrijven in hybride Mobile Device Management met intune. De limiet is vijf apparaten per gebruiker eerder.

## <a name="additional-apple-dep-settings"></a>Aanvullende Apple DEP-instellingen

Beheerders kunnen nu de volgende instellingen voor Apple Device Enrollment Program (DEP) configureren in het DEP-profiel voor iOS-en Mac-apparaten:
- **Touch-id**
- **In- en uitzoomen**
- **Siri**

Als deze functie is ingeschakeld, wordt door de Configuratieassistent van Apple om deze service gevraagd tijdens het activeren van het apparaat.

## <a name="integration-with-upgrade-analytics"></a>Integratie met Upgrade Analytics

Met upgrade Analytics kunt u de gereedheids gegevens en compatibiliteit van apparaten beoordelen en analyseren met Windows 10, zodat u gemakkelijker en vloeiendere upgrades kunt uitvoeren. Met de integratie van Upgrade Analytics met Configuration Manager, hebt u toegang tot de compatibiliteits gegevens voor upgrades in de Configuration Manager-beheer console en vervolgens, vanuit de apparaten lijst, doel apparaten voor upgrade of herstel.


## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Systeem eigen verbindings typen voor hybride profielen voor Windows 10 VPN

Wanneer u Configuration Manager met intune gebruikt, kunt u nu Windows 10 VPN-profielen maken met de verbindings typen micro soft Automatic, IKEv2, PPTP en L2TP in de Configuration Manager-console zonder OMA-URI te gebruiken.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Verbeteringen in de integratie van Windows Store voor bedrijven met Configuration Manager

In deze release hebben we de [integratie van Windows Store voor bedrijven](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) met de volgende nieuwe functies bijgewerkt:

**Update:** In de huidige Technical Preview-versie is de functie directe synchronisatie niet functioneel.

- Voorheen kon u alleen gratis apps implementeren vanuit Windows Store voor bedrijven. Configuration Manager biedt nu ook ondersteuning voor de implementatie van betaalde online gelicentieerde apps (alleen voor intune Inge schreven apparaten).
- U kunt nu een onmiddellijke synchronisatie initiëren tussen Windows Store voor bedrijven en Configuration Manager.
- U kunt nu de geheime sleutel van de client wijzigen die u hebt verkregen via Azure Active Directory

### <a name="try-it-out"></a>Probeer het nu!

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Een betaalde online gelicentieerde app kopen en synchroniseren

1. Koop een betaalde online gelicentieerde app vanuit Windows Store voor bedrijven.
2. Klik in de werk ruimte **beheer** van de Configuration Manager-console op **Cloud Services**  >  **updates en onderhoud**van  >  **Windows Store voor bedrijven**.
3. Klik op het tabblad **Start** in de groep **synchroniseren** op **Nu synchroniseren**.
4. Binnenkort wordt de app die u hebt aangeschaft, weer gegeven in het knoop punt **licentie gegevens voor Store-apps** van de werk ruimte **toepassings beheer** .

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Een Configuration Manager-toepassing maken en implementeren vanuit de gesynchroniseerde app-gegevens

De procedure voor het maken en implementeren van een Configuration Manager toepassing vanuit een betaalde Store-app is hetzelfde als voor het maken van een toepassing vanuit een gratis app. Zie de sectie **een Configuration Manager-toepassing maken en implementeren vanuit een Windows Store voor bedrijven-app** in [apps beheren vanuit Windows Store voor bedrijven met Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Wijzig de client geheime sleutel van Azure Active Directory

1. Klik in de werk ruimte **beheer** van de Configuration Manager-console op **Cloud Services**  >  **updates en onderhoud**van  >  **Windows Store voor bedrijven**.
2. Selecteer uw Windows Store voor bedrijven-account en klik vervolgens op **Eigenschappen**.
3. Voer in het dialoog venster **Eigenschappen van Windows Store voor bedrijven-account** een nieuwe sleutel in het veld **geheime sleutel** van de client in en klik vervolgens op **verifiëren**. Nadat de verificatie is uitgevoerd, klikt u op **Toep assen**en sluit u het dialoog venster.


## <a name="new-compliance-settings-for-configuration-items"></a>Nieuwe instellingen voor naleving voor configuratie-items

Er zijn veel nieuwe instellingen toegevoegd die u kunt gebruiken in uw configuratie-items voor verschillende platformen.
Dit zijn instellingen die voorheen aanwezig waren in Microsoft Intune in een zelfstandige configuratie en zijn nu beschikbaar wanneer u intune gebruikt met Configuration Manager.
Als u hulp nodig hebt bij een van deze instellingen, opent u [instellingen en functies op uw apparaten beheren met Microsoft intune beleid](../../../intune/configuration/device-profiles.md) en selecteert u vervolgens het subonderwerp instellingen voor het platform dat u wilt.


### <a name="new-settings-for-android-devices"></a>Nieuwe instellingen voor Android-apparaten

#### <a name="password-settings"></a>Wachtwoordinstellingen

- **Wachtwoordgeschiedenis onthouden**
- **Vingerafdruk voor ontgrendelen toestaan**

#### <a name="security-settings"></a>Beveiligingsinstellingen

- **Versleuteling vereisen op opslagkaarten**
- **Schermafbeelding toestaan**
- **Verzending van diagnostische gegevens toestaan**

#### <a name="browser-settings"></a>Browserinstellingen

- **Webbrowser toestaan**
- **Automatisch invullen toestaan**
- **Pop-upblokkering toestaan**
- **Cookies toestaan**
- **Active Scripting toestaan**

#### <a name="app-settings"></a>App-instellingen

- **Google Play Store toestaan**

#### <a name="device-capability-settings"></a>Instellingen voor apparaatfuncties

- **Verwisselbare opslag toestaan**
- **Wi-Fi-tethering toestaan**
- **Geolocatie toestaan**
- **NFC toestaan**
- **Bluetooth toestaan**
- **Spraakroaming toestaan**
- **Gegevensroaming toestaan**
- **Sms-/mms-berichten toestaan**
- **Spraakassistent toestaan**
- **Nummer inspreken toestaan**
- **Kopiëren en plakken toestaan**


### <a name="new-settings-for-ios-devices"></a>Nieuwe instellingen voor iOS-apparaten

#### <a name="password-settings"></a>Wachtwoordinstellingen

- **Aantal complexe tekens dat is vereist in wachtwoord**
- **Eenvoudige wachtwoorden toestaan**
- **Minuten inactief voordat wachtwoord is vereist**
- **Wachtwoordgeschiedenis onthouden**

### <a name="new-settings-for-mac-os-x-devices"></a>Nieuwe instellingen voor Mac OS X-apparaten

#### <a name="password-settings"></a>Wachtwoordinstellingen

- **Aantal complexe tekens dat is vereist in wachtwoord**
- **Eenvoudige wachtwoorden toestaan**
- **Wachtwoordgeschiedenis onthouden**
- **Minuten van inactiviteit voordat de schermbeveiliging wordt geactiveerd**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nieuwe instellingen voor Windows 10 Desktop-en Mobile-apparaten

#### <a name="password-settings"></a>Wachtwoordinstellingen

- **Minimum aantal tekensets**
- **Wachtwoordgeschiedenis onthouden**
- **Wacht woord vereisen wanneer het apparaat wordt geactiveerd vanuit een niet-actieve status**

#### <a name="security-settings"></a>Beveiligingsinstellingen

- **Versleuteling vereisen voor mobiel apparaat**
- **Handmatige uitschrijving toestaan**

#### <a name="device-capability-settings"></a>Instellingen voor apparaatfuncties

- **VPN via mobiele verbinding toestaan**
- **VPN-roaming via mobiele verbinding toestaan**
- **Opnieuw instellen van telefoon toestaan**
- **USB-verbinding toestaan**
- **Cortana toestaan**
- **Meldingen van onderhoudscentrum toestaan**

### <a name="new-settings-for-windows-10-team-devices"></a>Nieuwe instellingen voor Windows 10 team-apparaten

#### <a name="device-settings"></a>Apparaatinstellingen

- **Operational Insights van Azure inschakelen**
- **Draadloze Miracast-projectie inschakelen**
- **Kiezen welke vergaderingsinformatie wordt weergegeven op het welkomstscherm**
- **URL naar de achtergrondafbeelding van het vergrendelingsscherm**


### <a name="new-settings-for-windows-81-devices"></a>Nieuwe instellingen voor Windows 8,1-apparaten

#### <a name="applicability-settings"></a>Toepasselijkheidsinstellingen

- **Alle configuraties toepassen op Windows 10**

#### <a name="password-settings"></a>Wachtwoordinstellingen

- **Vereist wachtwoordtype**
- **Minimum aantal tekensets**
- **Minimale wachtwoordlengte**
- **Aantal mislukte aanmeldingen dat is toegestaan voordat het apparaat wordt gewist**
- **Minuten van inactiviteit voordat het scherm wordt uitgeschakeld**
- **Dagen tot wachtwoord verloopt**
- **Wachtwoordgeschiedenis onthouden**
- **Wachtwoorden niet opnieuw gebruiken**
- **Afbeeldingswachtwoord en PIN toestaan**

#### <a name="browser-settings"></a>Browserinstellingen

- **Automatische detectie van een intranetnetwerk toestaan**


### <a name="new-settings-for-windows-phone-81-devices"></a>Nieuwe instellingen voor Windows Phone 8,1-apparaten

#### <a name="applicability-settings"></a>Toepasselijkheidsinstellingen

- **Alle configuraties toepassen op Windows 10**

#### <a name="password-settings"></a>Wachtwoordinstellingen

- **Minimum aantal tekensets**
- **Eenvoudige wachtwoorden toestaan**
- **Wachtwoordgeschiedenis onthouden**

#### <a name="device-capability-settings"></a>Instellingen voor apparaatfuncties

- **Automatische verbinding met gratis Wi-Fi-hotspots toestaan**


## <a name="improvements-for-boundary-groups"></a>Verbeteringen voor grens groepen
Deze preview introduceert belang rijke wijzigingen in grens groepen en hoe deze werken met distributie punten. Deze wijzigingen helpen het ontwerp van uw inhouds infrastructuur te vereenvoudigen, terwijl u meer controle hebt over hoe en wanneer clients terugvallen op het zoeken naar extra distributie punten als inhouds bron locaties. Dit geldt zowel voor on-premises als in de cloud gebaseerde distributie punten.

Deze verbeteringen vervangen de concepten en gedragingen die u mogelijk al kent, zoals het configureren van distributie punten die snel of traag zijn. deze worden vervangen door een nieuw model dat eenvoudiger kan worden geconfigureerd en onderhouden. Deze wijzigingen zijn ook basis voor toekomstige wijzigingen waarmee andere site systeem rollen die u koppelt aan grens groepen worden verbeterd.  

Tijdens de upgrade naar 1609 worden uw huidige grenzen van de grens groep zodanig geconverteerd dat deze aan het nieuwe model voldoen, zodat deze wijzigingen de configuraties van de inhouds distributie niet storen (Zie [bestaande grens groepen bijwerken naar het nieuwe model](capabilities-in-technical-preview-1609.md#bkmk_update)).

In de volgende secties worden de wijzigingen beschreven die in deze preview-versie zijn geïntroduceerd, de werking van het nieuwe model en wat u kunt verwachten bij het upgraden van een site waarop al grens groepen zijn geconfigureerd.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Wijzigingen in de gebruikers interface en het gedrag voor grens groepen en inhouds locaties
Hieronder vindt u belang rijke wijzigingen in grens groepen en hoe clients inhoud vinden. Veel van deze wijzigingen en concepten werken samen.
- **Configuraties voor snelle of trage verbindingen worden verwijderd:** U kunt afzonderlijke distributie punten niet meer configureren om snel of traag te zijn.  In plaats daarvan wordt elk site systeem dat is gekoppeld aan een grens groep, op dezelfde manier behandeld. Als gevolg van deze wijziging wordt het tabblad **verwijzingen** van de eigenschappen van de grens groep niet meer ondersteund voor snelle of langzame configuratie.
- **Nieuwe standaard grens groep op elke site:**  Elke primaire site heeft een nieuwe standaard grens groep met de naam ***standaard-site-grens \<sitecode> -groep***.  Wanneer een client zich niet op een netwerk locatie bevindt die is toegewezen aan een grens groep, zal die client de site systemen gebruiken die zijn gekoppeld aan de standaard groep van de toegewezen site. Plan het gebruik van deze grens groep als een vervanging van de locatie van de tijdelijke inhoud van het concept.    
  -  **' Terugval bron locaties voor inhoud toestaan '** wordt verwijderd: u hoeft niet langer expliciet een distributie punt te configureren dat moet worden gebruikt voor terugval en de opties die u kunt instellen, worden verwijderd uit de gebruikers interface.

  Daarnaast is het resultaat van de instelling **clients toestaan een terugval bron locatie te gebruiken voor inhoud** van een implementatie type voor toepassingen is gewijzigd. Met deze instelling voor een implementatie type kan een client de standaard site grens groep gebruiken als de locatie van de inhouds bron.

  -  **Relaties grens groepen:** Elke grens groep kan worden gekoppeld aan een of meer extra grens groepen. Deze koppelingen vormen formulier relaties die zijn geconfigureerd op het tabblad Eigenschappen van nieuwe grens groep, met de naam **relaties**:
  -   Elke grens groep waaraan een client rechtstreeks is gekoppeld, wordt een **huidige** grens groep genoemd.  
  -   Een grens groep die een client kan gebruiken vanwege een koppeling tussen de *huidige* grens groep van die client en een andere groep wordt een grens groep in de vorm van een **buur** genoemd.
  -  Het bevindt zich op het tabblad **relaties** waarmee u grens groepen kunt toevoegen die kunnen worden gebruikt *als een grens groep in de* nabijheid. U kunt ook een tijd in minuten configureren die bepaalt wanneer een client die de inhoud niet kan vinden van een distributie punt in de *huidige* groep, begint met het zoeken naar inhouds locaties vanuit die *naburige* grens groepen.

      Wanneer u de configuratie van een grens groep toevoegt of wijzigt, hebt u de mogelijkheid om terugval te blok keren op die specifieke grens groep van de huidige groep die u configureert.

  Als u de nieuwe configuratie wilt gebruiken, definieert u expliciete koppelingen (koppelingen) van de ene grens groep naar een andere en configureert u alle distributie punten in die gekoppelde groep met dezelfde tijd in minuten. De tijd die u configureert bepaalt wanneer een client die geen inhouds bron kan vinden op basis van de *huidige* grens groep, kan beginnen met zoeken naar inhouds bronnen vanuit die grens groep in de neighbor.

  Naast de grens groepen die u expliciet configureert, heeft elke grens groep een geïmpliceerde koppeling naar de standaard site grens groep. Deze koppeling wordt na 120 minuten actief wanneer de standaard site grens groep een naburig grens groep wordt, waarmee de clients de distributie punten kunnen gebruiken die zijn gekoppeld aan die grens groep als locatie van de inhouds bron.

  Dit gedrag vervangt wat eerder als terugval voor inhoud werd genoemd.  U kunt dit standaard gedrag van 120 minuten onderdrukken door de standaard site grens groep expliciet te koppelen aan een *huidige* groep, een specifieke tijd in minuten in te stellen of terugval volledig te blok keren om te voor komen dat ze worden gebruikt.


- **Clients proberen inhoud van elk distributie punt Maxi maal twee minuten op te halen:** Wanneer een client zoekt naar een locatie van de inhouds bron, probeert het elk distributie punt twee minuten te benaderen voordat vervolgens een ander distributie punt wordt uitgevoerd. Dit is een wijziging ten opzichte van vorige versies waar clients tot Maxi maal twee uur verbinding hebben gemaakt met een distributie punt.

  - Het eerste distributie punt dat een client probeert te gebruiken, is wille keurig geselecteerd uit de groep beschik bare distributie punten in de *huidige* grens groep (of groepen) van de client.

  - Als de client de inhoud na twee minuten niet heeft gevonden, wordt deze overgeschakeld naar een nieuw distributie punt en wordt geprobeerd om inhoud op te halen van de server. Dit proces wordt elke twee minuten herhaald totdat de client de inhoud heeft gevonden of de laatste server in de groep heeft bereikt.

  - Als een client geen geldige locatie van de inhouds bron van de *huidige* groep kan vinden voordat de periode voor terugval naar *een grens groep in de* nabijheid is bereikt, voegt de client de distributie punten van die groep van de *neighbor* toe aan het einde van de huidige lijst en zoekt vervolgens de uitgevouwen groep van bron locaties die de distributie punten van beide grens groepen bevatten.

      > [!TIP]  
      > Wanneer u een expliciete koppeling van de huidige grens groep naar de standaard site grens groep maakt en een terugval tijd definieert die kleiner is dan de terugval tijd voor een koppeling naar een grens groep in de nabijheid, zullen clients vanaf de standaard site grens groep zoeken naar bron locaties voordat ze de groep neighbor opnemen.

  - Wanneer de client geen inhoud kan ophalen van de laatste server in de groep, wordt het proces opnieuw gestart.


### <a name="how-the-new-model-works"></a>Hoe het nieuwe model werkt
Wanneer u grens groepen configureert, koppelt u grenzen (netwerk locaties) en site systeem rollen, zoals distributie punten, aan de grens groep. Dit helpt clients te koppelen aan site systeem servers zoals distributie punten die zich in de buurt van de clients op het netwerk bevinden.   
- U kunt dezelfde grens toewijzen aan meerdere grens groepen
- Site systeem servers, zoals distributie punten, kunnen worden gekoppeld aan meerdere grens groepen, zodat ze beschikbaar zijn voor een groter aantal netwerk locaties
- Als een distributie punt niet is gekoppeld aan een grens groep, kunnen clients dat distributie punt niet gebruiken als de locatie van de inhouds bron.

Vanaf deze Technical Preview definieert u grens groeps relaties voor het configureren van terugval gedrag voor inhouds bron locaties. Dit nieuwe gedrag wordt geconfigureerd op het tabblad nieuwe **relaties** van de eigenschappen van de grens groep en vervangt het configureren van site systemen op langzame of snelle wijze, en het configureren van een grens groep voor het toestaan van terugval bron locatie voor inhoud.

Op het tabblad relaties voegt u andere grens groepen toe om een relatie met die groepen te configureren. Elke relatie is een eenrichtings koppeling van de **huidige** grens groep naar de grens groep die u toevoegt, die een **neighbor**wordt genoemd. Voor elke koppeling die u maakt, kunt u binnen enkele minuten distributie punten configureren met een terugval tijd. Deze tijd wordt gebruikt om te bepalen hoe lang clients in de *huidige* grens groep met behulp van distributie punten in *de grens groep grenzen kunnen* beginnen als ze geen geldige inhouds bron locatie van de huidige grens groep vinden.

Wanneer een client geen inhoud kan vinden en locaties kan zoeken vanuit grens groepen in de buur, wordt de groep beschik bare distributie punten voor die client op een gecontroleerde manier verg root.  

- Een grens groep kan meer dan één relatie hebben. Zo kunt u terugvallen instellen op verschillende neighbors na verschillende Peri Oden.
- Clients worden alleen teruggevallen op een grens groep die een directe buur is van de huidige grens groep.
- Wanneer een client lid is van meerdere grens groepen, wordt de huidige grens groep gedefinieerd als een samen voeging van alle grens groepen van die client.  Die client kan vervolgens worden teruggevallen naar een neighbor van een van deze oorspronkelijke grens groepen.

Naast de koppelingen die u definieert, is er een impliciete koppeling die automatisch wordt gemaakt tussen de grens groepen die u maakt en de standaard grens groep die automatisch voor elke site wordt gemaakt. Deze automatische koppeling:
- Wordt gebruikt door clients die zich niet in een grens bevinden die is gekoppeld aan een grens groep in uw hiërarchie, gebruikt automatisch de standaard grens groep van de toegewezen site om geldige inhouds bron locaties te identificeren.   
-  Is een standaard terugval optie van de huidige grens groep tot de standaard grens groep voor sites die na 120 minuten wordt gebruikt.

**Voor beeld van het gebruik van het nieuwe model:** U maakt drie grens groepen die geen grenzen of site systeem servers delen:
- Groeps BG_A met distributie punten DP_A1 en DP_A2 die zijn gekoppeld aan de groep
- Groeps BG_B met distributie punten DP_B1 en DP_B2 die zijn gekoppeld aan de groep
- Groeps BG_C met distributie punten DP_C1 en DP_C2 die zijn gekoppeld aan de groep

U voegt de netwerk locaties van uw clients alleen toe aan de grens groep BG_A en u configureert vervolgens relaties van die grens groep naar de andere twee grens groepen:
- U kunt distributie punten configureren voor de eerste *neighbor* -groep (BG_B) die na 10 minuten moet worden gebruikt. Deze groep bevat distributie punten DP_B1 en DP_B2. Beide zijn goed verbonden met de eerste groepen grens locaties.
- U configureert de tweede *neighbor* -groep (BG_C) die na 20 minuten moet worden gebruikt. Deze groep bevat distributie punten DP_C1 en DP_C2. Beide bevinden zich in een WAN van de andere twee grens groepen.
- U voegt ook een extra distributie punt dat zich op de site server bevindt, toe aan de standaard site grens groep. Dit is uw minimale locatie voor de inhouds bron, maar deze bevindt zich centraal in alle grens groepen.

  Voor beeld van grens groepen en terugval tijden:

  ![BG_Fallack](media/BG_Fallback.png)


Met deze configuratie:
- De client begint met het zoeken naar inhoud vanaf distributie punten in de *huidige* grens groep (BG_A), waarbij op elk distributie punt twee minuten wordt gezocht voordat wordt overgeschakeld naar het volgende distributie punt in de grens groep. De groep clients met geldige inhouds bron locaties bevat DP_A1 en DP_A2.
- Als de client na tien minuten geen inhoud van de *huidige* grens groep kan vinden, voegt deze de distributie punten van de BG_B grens groep toe aan de zoek opdracht. Vervolgens wordt gezocht naar inhoud van een distributie punt in de gecombineerde groep distributie punten die nu uit zowel de BG_A als BG_B grens groepen bestaan. De client blijft binnen twee minuten contact opnemen met elk distributie punt voordat naar het volgende distributie punt van de groep wordt overgeschakeld. De groep clients met geldige inhouds bron locaties bevat DP_A1, DP_A2, DP_B1 en DP_B2.
- Na een extra periode van tien minuten (totaal van 20 minuten) als de client nog geen distributie punt met inhoud heeft gevonden, wordt de groep beschik bare distributie punten uitgevouwen om deze op te halen uit de tweede *neighbor* -groep, grens groep BG_C. De client heeft nu 6 distributie punten die moeten worden doorzocht (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 en DP_C2) en blijven elke twee minuten overschakelen naar een nieuw distributie punt totdat de inhoud is gevonden.
- Als de client na een totaal van 120 minuten geen inhoud heeft gevonden, wordt de *standaard site grens groep* opgenomen als onderdeel van de voortgezette zoek opdracht. De groep distributie punten bevat nu alle distributie punten van de drie geconfigureerde grens groepen en het laatste distributie punt dat zich op de site Server computer bevindt.  De client gaat vervolgens door met zoeken naar inhoud, waarbij distributie punten elke twee minuten worden gewijzigd totdat de inhoud is gevonden.

Door de verschillende groepen van de neighbor zo te configureren dat deze op verschillende tijdstippen beschikbaar zijn, kunt u bepalen wanneer specifieke distributie punten worden toegevoegd als de locatie van de inhouds bron, en wanneer, of als de client terugvallen op de standaard site grens groep als een veiligheids-net voor inhoud die niet beschikbaar is op een andere locatie.


### <a name="update-existing-boundary-groups-to-the-new-model"></a><a name="bkmk_update"></a>Bestaande grens groepen bijwerken naar het nieuwe model
Wanneer u versie 1609 installeert en uw site bijwerkt, worden de volgende configuraties automatisch gemaakt. Deze zijn bedoeld om ervoor te zorgen dat uw huidige terugval gedrag beschikbaar blijft, totdat u nieuwe grens groepen en relaties configureert.  
- Niet-beveiligde distributie punten op een site worden toegevoegd aan de *standaard-site-boundary-groep \<sitecode> * grens groep van die site.
- Er wordt een kopie gemaakt van elke bestaande grens groep die een site server bevat die is geconfigureerd met een trage verbinding. De naam van de nieuwe groep is *** \<original boundary group name> langzaam tmp***:  
  -   Site systemen met een snelle verbinding blijven in de oorspronkelijke grens groep.
  -   Een kopie van site systemen met een trage verbinding wordt toegevoegd aan de kopie van de grens groep. De oorspronkelijke site systemen die als langzaam zijn geconfigureerd, blijven in de oorspronkelijke grens groep voor compatibiliteit met eerdere versies, maar worden niet gebruikt vanuit die grens groep.
  -   Er zijn geen grenzen gekoppeld aan de kopie van deze grens groep. Er wordt echter een terugval koppeling gemaakt tussen de oorspronkelijke groep en de nieuwe kopie van de grens groep waarvan de terugval tijd is ingesteld op nul.

  De volgende tabel bevat het nieuwe terugval gedrag dat u kunt verwachten van de combi natie van de oorspronkelijke implementatie-instellingen en distributiepunt configuraties:

Oorspronkelijke implementatie configuratie voor Program ma's niet uitvoeren in langzaam netwerk  |Oorspronkelijke distributiepunt configuratie voor de ' client toestaan een terugval bron locatie voor inhoud te gebruiken '  |Nieuw terugval gedrag  
---------|---------|---------
Geselecteerd     |  Geselecteerd    |  **Geen terugval** : gebruik alleen de distributie punten in de huidige grens groep       
Geselecteerd     |  Niet geselecteerd|  **Geen terugval** : gebruik alleen de distributie punten in de huidige grens groep       
Niet geselecteerd |  Niet geselecteerd|  **Terugval naar neighbor** : gebruik de distributie punten in de huidige grens groep en voeg vervolgens de distributie punten toe vanuit de grens groep van de neighbor. Tenzij een expliciete koppeling naar de standaard site grens groep is geconfigureerd, kunnen clients niet terugvallen op die groep.    
Niet geselecteerd | Geselecteerd |   **Normale terugval** : distributie punten in de huidige grens groep gebruiken, vervolgens de standaard grens groepen van de neighbor en de site

 Alle andere implementatie configuraties resulteren in **normale terugval**.  



## <a name="office-365-client-management-dashboard"></a>Office 365-dash board voor client beheer  
De technische preview van Configuration Manager 1609 introduceert een nieuw dash board. Als u het dash board wilt weer geven, gaat u in de Configuration Manager-console naar **software bibliotheek**  >  **Overview**  >  **Office 365 client management**.
>[!NOTE]
>In de werk ruimte wat is er **Nieuw** in de Configuration Manager-console, heeft het nieuwe dash board een onjuiste naam **Office 365-onderhouds dashboard**.

In het dash board worden grafieken weer gegeven voor het volgende:

- Aantal Office 365-clients
- Office 365-client versies
- Office 365-client talen
- Office 365-client kanalen     
Zie [Overzicht van updatekanalen voor Office 365 ProPlus](/deployoffice/overview-update-channels) voor meer informatie.
- Automatische implementatie regels waarbij Office 365-client is geselecteerd in de set beschik bare producten.

U kunt de volgende acties uitvoeren op het dash board:
- Aan de bovenkant van het dash board gebruikt u de vervolg keuzelijst **verzameling** om de dashboard gegevens te filteren op leden van een bepaalde verzameling.
- Klik in de rechter bovenhoek van het dash board op **office 365 Installer** om de Wizard Office 365-client installatie te starten om Office 365-apps te implementeren op clients. Zie [Office 365-Apps implementeren op clients](#deploy-office-365-apps-to-clients)voor meer informatie.
- Klik aan de rechter kant van het dash board op **een ADR maken** om de wizard regel voor automatische implementatie te openen en een nieuwe regel voor automatische implementatie (ADR) te maken. Als u een ADR voor Office 365-Apps wilt maken, selecteert u **Office 365-client** wanneer u het product kiest. Zie [software-updates automatisch implementeren](../../sum/deploy-use/automatically-deploy-software-updates.md)voor meer informatie.
- Klik in de rechter benedenhoek van het dash board op **client agent instellingen maken** om instellingen voor client agent te openen. Zie [over client instellingen](../clients/deploy/about-client-settings.md)voor meer informatie.



Zie [office 365 ProPlus-updates beheren met Configuration Manager](../../sum/deploy-use/manage-office-365-proplus-updates.md)voor meer informatie over updates voor Office 365 ProPlus.

## <a name="deploy-office-365-apps-to-clients"></a>Office 365-Apps implementeren op clients
In deze versie van het Office 365-dash board voor client beheer kunt u het installatie programma van Office 365 starten, waarmee u installatie-instellingen voor Office 365 kunt configureren, bestanden van Office Content Delivery Networks (Cdn's) downloadt en de bestanden als een toepassing implementeert in Configuration Manager.

### <a name="limitations-of-office-365-deployment"></a>Beperkingen van Office 365-implementatie
- U kunt problemen ondervinden bij het importeren van bestaande client instellingen (XML) in de wizard Office 365-app installeren. U kunt de client instellingen hand matig configureren zonder een probleem.

#### <a name="to-deploy-office-365-apps-to-clients"></a>Office 365-Apps implementeren op clients
1. Navigeer in de Configuration Manager-console naar **software bibliotheek**  >  **Overview**  >  **Office 365 client management**.
2. Klik in het rechterdeel venster op **Office 365 Installer** . De Office 365-client installatie wizard wordt geopend.
3. Geef op de pagina **Toepassings instellingen** een naam en beschrijving voor de app op, voer de download locatie voor de bestanden in en klik op **volgende**. Houd er rekening mee dat de locatie moet worden opgegeven in de vorm &#92;&#92;*server*&#92;*share*.
4. Kies op de pagina **client instellingen importeren** of u de Office 365-client instellingen wilt importeren uit een bestaand XML-configuratie bestand of hand matig de instellingen wilt opgeven en klik vervolgens op **volgende**.
Wanneer u een bestaand configuratie bestand hebt, voert u de locatie voor het bestand in en gaat u verder met stap 7. Houd er rekening mee dat de locatie moet worden opgegeven in de vorm &#92;&#92;*server*&#92;*share*&#92;*Bestands naam*. Indeling.

    > [!IMPORTANT]
    >U kunt problemen ondervinden bij het importeren van bestaande client instellingen (XML) in deze Technical Preview.

5. Op de **client producten** pagina selecteert u het Office 365-pakket dat u gebruikt, selecteert u de toepassingen die u wilt opnemen, selecteert u eventuele extra Office-producten die moeten worden opgenomen en klikt u vervolgens op **volgende**.
6. Kies op de pagina **client instellingen** de instellingen die u wilt toevoegen en klik vervolgens op **volgende**.
7. Kies op de pagina **implementatie** of u de toepassing wilt implementeren en klik vervolgens op **volgende**.
Als u ervoor kiest om het pakket niet in de wizard te implementeren, gaat u naar stap 9.
8. Configureer de overige pagina's van de wizard op dezelfde manier als bij een typische toepassings implementatie. Zie [een toepassing maken en implementeren](../../apps/get-started/create-and-deploy-an-application.md)voor meer informatie.
9. Voltooi de wizard.
10. U kunt de toepassing implementeren of bewerken op dezelfde manier als andere toepassingen in Configuration Manager vanuit **software bibliotheek**  >  **overzicht**toepassingen voor  >  **toepassings beheer**  >  **Applications**.

>[!NOTE]
>Nadat u Office 365-apps hebt geïmplementeerd, kunt u regels voor automatische implementatie maken om de apps te onderhouden. Als u een ADR voor Office 365-Apps wilt maken, klikt u op **een ADR maken**en selecteert u **Office 365-client** wanneer u het product kiest. Zie [software-updates automatisch implementeren](../../sum/deploy-use/automatically-deploy-software-updates.md)voor meer informatie.

## <a name="improvements-for-bios-to-uefi-conversion"></a><a name="BKMK_UEFIConversion"></a>Verbeteringen voor de conversie van BIOS naar UEFI
U kunt nu een taken reeks met een implementatie van een besturings systeem aanpassen met een nieuwe variabele, TSUEFIDrive, zodat de stap computer opnieuw opstarten een FAT32-partitie op de harde schijf voorbereidt voor overgang naar UEFI. De volgende procedure bevat een voor beeld van hoe u taken reeks stappen kunt maken om de harde schijf voor te bereiden voor de conversie van BIOS naar UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Voor bereiding van de FAT32-partitie voor de conversie naar UEFI:
In een bestaande taken reeks om een besturings systeem te installeren, voegt u een nieuwe groep toe met stappen om de conversie van het BIOS naar UEFI uit te voeren.

1. Maak een nieuwe taken reeks groep na de stappen voor het vastleggen van bestanden en instellingen en vóór de stappen voor het installeren van het besturings systeem. U kunt bijvoorbeeld een groep maken na de **opname bestanden en instellingen groep met** de naam **BIOS-naar-UEFI**.
2. Voeg op het tabblad **Opties** van de nieuwe groep een nieuwe taken reeks variabele toe als een voor waarde **_SMSTSBootUEFI** waarbij _SMSTSBootUEFI **niet gelijk** is aan **waar**. Zo voor komt u dat de stappen in de groep worden uitgevoerd wanneer een computer zich al in de UEFI-modus bevindt.
![Groep BIOS naar UEFI](media/BIOS-to-UEFI-group.png)
3. Voeg onder de nieuwe groep de taken reeks stap **computer opnieuw opstarten** toe. In **opgeven wat moet worden uitgevoerd na het opnieuw opstarten**, selecteert u **de opstart installatie kopie die is toegewezen aan deze taken reeks wordt geselecteerd** om de computer te starten in Windows PE.  
4. Voeg op het tabblad **Opties** een taken reeks variabele toe als een voor waarde waarbij **_SMSTSInWinPE gelijk is aan False**. Dit voor komt dat deze stap wordt uitgevoerd als de computer al aanwezig is in Windows PE.

    ![Computer stap opnieuw opstarten](media/Restart-in-Windows-PE.png)
5. Voeg een stap toe om het OEM-hulp programma te starten waarmee de firmware wordt geconverteerd van BIOS naar UEFI. Dit is doorgaans een taken reeks stap **opdracht regel uitvoeren** met een opdracht regel om het OEM-hulp programma te starten.
5. Voeg de taken reeks stap schijf Format teren en partitioneren toe voor het partitioneren en Format teren van de harde schijf. In de stap gaat u als volgt te werk:
    1. Maak de FAT32-partitie die wordt geconverteerd naar UEFI voordat het besturings systeem wordt geïnstalleerd. Kies **GPT** voor het **schijf type**.
    ![Schijf stap Format teren en partitioneren](media/Format-and-partition-disk.png)
    2. Ga naar de eigenschappen van de FAT32-partitie. Voer **TSUEFIDrive** in het veld **variabele** in. Wanneer de taken reeks deze variabele detecteert, wordt de UEFI-overgang voor bereid voordat de computer opnieuw wordt opgestart.
    ![Partitie-eigenschappen](media/Partition-properties.png)
    3. Maak een NTFS-partitie die wordt gebruikt door de taken reeks Engine om de status op te slaan en logboek bestanden op te slaan.
6. Voeg de taken reeks stap **computer opnieuw opstarten** toe. In **opgeven wat moet worden uitgevoerd na het opnieuw opstarten**, selecteert u **de opstart installatie kopie die is toegewezen aan deze taken reeks wordt geselecteerd** om de computer te starten in Windows PE.  




## <a name="intune-compliance-charts"></a>InTune-compatibiliteits grafieken
In deze release kunt u een snel overzicht krijgen van de algemene compatibiliteit voor apparaten en de belangrijkste redenen voor niet-naleving met behulp van nieuwe grafieken onder **bewaking werk ruimte** in de Configuration Manager-console.

#### <a name="to-view-the-intune-compliance-charts"></a>De intune-compatibiliteits grafieken weer geven
1. Ga in de Configuration Manager-console naar **controle**-  >  **overzicht**  >  **instellingen voor naleving**.
2. De **algemene nalevings** grafiek van het apparaat wordt weer gegeven.
3. Klik op het knoop punt **nalevings beleid** om de grafieken over de **algehele naleving** van het apparaat en de **belangrijkste niet-nalevings redenen** weer te geven.

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Beperkingen van de intune-compatibiliteits grafieken in TP 1609
- Er wordt momenteel een fout gegenereerd door het inzoomen voor de **algemene nalevings** grafiek voor apparaten.
- In de grafiek **best mogelijke redenen voor niet-naleving** worden de beleids naam en niet de afzonderlijke redenen voor niet-naleving vermeld. U kunt op het beleid klikken om in te zoomen op de apparaten die niet compatibel zijn voor dat beleid.

### <a name="try-it-out"></a>Probeer het eens
Voer de volgende secties in de aangegeven volg orde uit:

#### <a name="check-overall-compliance-chart"></a>Algemene nalevings grafiek controleren
1. Voeg in Configuration Manager twee beleids regels voor naleving van iOS toe. Eén beleid moet één set instellingen voor apparaten hebben (Stel bijvoorbeeld de lengte van de pincode in op 6). Het andere beleid moet een andere set instellingen hebben (bijvoorbeeld complexiteit van de pincode). De beleids instellingen mogen niet overlappen of conflicteren.
2. Implementeer de twee beleids regels voor een groep gebruikers.
3. Registreer twee iOS-apparaten in intune met hetzelfde gebruikers account en een account dat het beleid in de vorige stap heeft ontvangen. De apparaten mogen niet voldoen aan de criteria van het nalevings beleid.
4. In Configuration Manager raadpleegt u de **algemene compliance** -grafiek van het apparaat. Beide apparaten moeten rapporteren als niet-compatibel.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Controleer de grafiek met de belangrijkste redenen voor niet-naleving
5. Controleer de grafiek **best mogelijke redenen voor niet-naleving** . In dit diagram worden de belangrijkste vijf redenen voor niet-naleving vermeld, maar wanneer er slechts twee nalevings instellingen zijn ingesteld voor het beleid, worden alleen de bovenste twee redenen voor naleving weer gegeven.
6. Klik op een van de secties in de grafiek. Beide apparaten moeten worden weer gegeven in de gefilterde weer gave onder **activa en naleving**  >  **overzicht**  >  **apparaat**.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Apparaten compatibel maken en de grafieken controleren
7. Maak een van de apparaten die voldoen aan een van de beleids regels. Controleer de **volledige compliance** -grafiek van het apparaat. In de grafiek moet één compatibel apparaat en één niet-compatibel apparaat worden weer gegeven.
8. Zorg ervoor dat het andere apparaat compatibel is met hetzelfde beleid. Dit zorgt ervoor dat één apparaat compatibel is met beide beleids regels en één apparaat dat voldoet aan één van de beleids regels.
9. Controleer de grafiek **best mogelijke redenen voor niet-naleving** . Er mag slechts één niet-nalevings reden worden vermeld.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Zie ook
[Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md)
---
title: Technical Preview 1706
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview-versie 1706 voor Configuration Manager.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 79258786b56cc3e7fe4971391903772700768a89
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126753"
---
# <a name="capabilities-in-technical-preview-1706-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1706 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1706. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md) om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
- **Issue Name**. Details
    Workaround details.
-->
**Bekende problemen in deze technische preview:**

- **Distributie punt verplaatsen** : de opties in de console om een distributie punt tussen sites te verplaatsen, kunnen niet met deze release worden gebruikt vanwege de technische preview-limiet van één primaire site.

- **Instellingen voor naleving van apparaten** : u kunt een tegenovergesteld gedrag ondervinden bij het gebruik van de twee nieuwe instellingen voor naleving van apparaten:
  - **USB-foutopsporing op apparaat blokkeren**
  - **Apps van onbekende bronnen blokkeren**

    Als beheerders bijvoorbeeld **blok-USB-fout opsporing op apparaat** instellen op **True**, worden alle apparaten waarvoor geen USB-fout opsporing is ingeschakeld, gemarkeerd als niet-compatibel.

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Verbeterde grens groepen voor software-update punten
<!-- 1324591 -->
Deze release bevat verbeteringen voor de werking van software-update punten met grens groepen. Hieronder vindt u een overzicht van het nieuwe terugval gedrag:
- Terugval voor software-update punten maakt nu gebruik van een Configureer bare tijd voor terugval voor grens groepen in de buur, met een minimum tijd van 120 minuten.

- Onafhankelijk van de terugval configuratie probeert een client het laatste software-update punt te bereiken dat gedurende 120 minuten wordt gebruikt. Wanneer de server gedurende 120 minuten niet kan worden bereikt, controleert de client de groep beschik bare software-update punten, zodat er een nieuwe kan worden gevonden.

  - Alle software-update punten in de huidige grens groep van de client worden direct toegevoegd aan de groep van de client.

  - Omdat een client de oorspronkelijke server gedurende 120 minuten probeert te gebruiken voordat een nieuwe wordt gezocht, worden er pas na twee uur verbinding gemaakt met extra servers.

  - Als terugval naar een neighbor-groep is geconfigureerd voor het minimum van 120 minuten, zullen software-update punten van die grens groep van die neighbor deel uitmaken van de groep beschik bare servers van de client.

- Als de oorspronkelijke server gedurende twee uur niet kan worden bereikt, schakelt de client over naar een kortere cyclus voor het maken van contact met een nieuw software-update punt.

  Dit betekent dat als een client geen verbinding kan maken met een nieuwe server, de volgende server snel wordt geselecteerd uit de groep beschik bare servers en er wordt geprobeerd contact op te nemen.

  - Deze cyclus wordt vervolgd totdat de client verbinding maakt met een software-update punt dat kan worden gebruikt.
  - Totdat de client een software-update punt vindt, worden er extra servers toegevoegd aan de groep beschik bare servers wanneer aan de terugval tijd voor elke grens groep van de neighbor wordt voldaan.

Zie [Software-update punten](../servers/deploy/configure/boundary-groups.md#bkmk_sup) in het onderwerp grens groepen voor de current branch voor meer informatie.


## <a name="site-server-role-high-availability"></a>Site serverrol hoge Beschik baarheid
<!-- 1128774 -->
Hoge Beschik baarheid voor de site serverrol is een op Configuration Manager gebaseerde oplossing voor het installeren van een extra primaire site server in de *passieve* modus. De site server in de passieve modus is een aanvulling op de bestaande primaire site server in de *actieve* modus. Een passieve-modus site server is beschikbaar voor onmiddellijk gebruik, indien nodig.

Een primaire site server in de passieve modus:
- Maakt gebruik van dezelfde site database als uw actieve site server.
- Hiermee ontvangt u een kopie van de inhouds bibliotheek van de actieve site servers, die vervolgens in synch wordt bewaard.
- Schrijft geen gegevens naar de site database, zolang deze zich in de passieve modus bevindt.
- Biedt geen ondersteuning voor het installeren of verwijderen van optionele site systeem rollen, zolang deze zich in de passieve modus bevindt.

Als u de site server van de passieve modus wilt maken op de site server in de actieve modus, moet u deze hand matig promo veren. Hiermee wordt de actieve site server overgeschakeld naar de passieve site server. De site systeem rollen die beschikbaar zijn op de oorspronkelijke actieve modus server blijven beschikbaar zolang die computer toegankelijk is. Alleen de site serverrol wordt overgeschakeld tussen de actieve en passieve modus.

Als u een site server in de passieve modus wilt installeren, gebruikt u de **wizard site systeem server maken** om een nieuwe site server te configureren met een type **primaire site server** en een **passieve**modus. De wizard voert Configuration Manager Setup uit op de opgegeven server om de nieuwe site server in de passieve modus te installeren. Nadat de installatie is voltooid, wordt de site server van de passieve modus en de inhouds bibliotheek van de site server in de actieve modus gesynchroniseerd met wijzigingen of configuraties die u naar de actieve site server hebt gemaakt.

### <a name="prerequisites-and-limitations"></a>Vereisten en beperkingen
- Één site server in de passieve modus wordt ondersteund op elke primaire site.

- De site server in de passieve modus kan on-premises of in de cloud worden uitgevoerd in Azure.

- De actieve modus en site servers in de passieve modus moeten zich in hetzelfde domein bevindt.

- Zowel de actieve modus als de passieve modus site servers moeten gebruikmaken van dezelfde site database, die extern moet zijn van de computers van elke site server.

    - De SQL Server die als host fungeert voor de-data base, kan gebruikmaken van een standaard exemplaar, een benoemd exemplaar, een SQL Server cluster of een AlwaysOn-beschikbaarheids groep.

    - De site server in de passieve modus is geconfigureerd voor gebruik van dezelfde site database als de actieve modus site server. De site server in de passieve modus gebruikt deze data base echter pas nadat deze is gepromoveerd tot de actieve modus.

- De computer waarop de site server van de passieve modus wordt uitgevoerd:

    - Moet voldoen aan de [vereisten voor het installeren van een primaire site](https://docs.microsoft.com/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    - Wordt geïnstalleerd met behulp van bron bestanden die overeenkomen met de versie van de actieve modus site server.

    - U kunt geen site systeemrol van een site hebben voordat u de site passieve modus installeert.

- Op de site Server computers actief en passieve modus kunnen verschillende besturings systemen of Service Pack versies worden uitgevoerd, zolang deze beide niet worden ondersteund door uw versie van Configuration Manager.

- De promotie van de site server passieve modus naar de actieve modus server is hand matig. Er is geen automatische failover.

- Site systeem rollen kunnen alleen worden geïnstalleerd op de site server die zich in de actieve modus bevindt.

    - Een site server in de actieve modus ondersteunt alle site systeem rollen. U kunt geen site systeem rollen installeren op de server wanneer deze zich in de passieve modus bevindt.

    - Site systeem rollen die gebruikmaken van een Data Base (zoals het rapportage punt), moeten die data base hebben op een server die extern is van zowel de actieve modus als de passieve modus site servers.

    - De SMS_Provider wordt niet geïnstalleerd op de site server in de passieve modus. Omdat u verbinding moet maken met een SMS_Provider voor de site om de site server van de passieve modus hand matig te promo veren naar de actieve modus, raden we u [aan ten minste één extra exemplaar van de provider](../plan-design/hierarchy/plan-for-the-sms-provider.md) op een extra computer te installeren.

**Bekend probleem**:   
In deze release worden de **status** voor de volgende voor waarden in de-console weer gegeven als numerieke waarden in plaats van Lees bare tekst:
- 131071-installatie van site server is mislukt
- 720895-het verwijderen van de site server functie is mislukt
- 851967 – failover is mislukt

### <a name="add-a-site-server-in-passive-mode"></a>Een site server toevoegen in de passieve modus
1. Ga in de-console naar **beheer**  >  **site configuratie**  >  **sites** en start de [wizard site systeem rollen toevoegen](../servers/deploy/configure/install-site-system-roles.md). U kunt ook de **wizard site systeem server maken**gebruiken.

2. Geef op de pagina **Algemeen** de server op die als host moet fungeren voor de site server in de passieve modus. De server die u opgeeft, kan geen site systeem rollen hosten voordat een site server in de passieve modus wordt geïnstalleerd.

3. Selecteer op de pagina **selectie van systeem functie** alleen **primaire site server in de passieve modus**.

4. Als u de wizard wilt volt ooien, moet u de volgende informatie opgeven die wordt gebruikt om Setup uit te voeren en de site serverrol op de opgegeven server te installeren:
    - Kies of u de installatie bestanden van de actieve site server wilt kopiëren naar de nieuwe site server in de passieve modus of geef een pad op naar een locatie met de inhoud van de cd van de actieve site server **. Meest recente** map.

    - Geef dezelfde naam op voor de site database server en de data base die wordt gebruikt door de site server in de actieve modus.

5. Configuration Manager wordt de site server vervolgens in de passieve modus geïnstalleerd op de opgegeven server.

Ga voor gedetailleerde installatie status naar **beheer**  >  **site configuratie**  >  **sites**.
- De status van de site server in de passieve modus wordt weer gegeven als **installatie**.

- Selecteer de server en klik vervolgens op **status weer geven** om de **installatie status van de site server** te openen voor meer gedetailleerde informatie.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>De site server in de passieve modus promo veren naar de actieve modus
Wanneer u de site server van de passieve modus wilt wijzigen in de actieve modus, doet u dat in het deel venster **knoop punten** in de **beheer**  >  **site configuratie**  >  **sites**. Zolang u toegang hebt tot een exemplaar van de SMS_Provider, kunt u de site openen om deze wijziging door te voeren.
1. Selecteer in het deel venster **knoop punten** van de Configuration Manager-console de site server in de passieve modus en kies vervolgens **niveau verhogen naar actief**in het lint.

2. De eenvoudige **status** van de **server die u**wilt promo veren wordt weer gegeven in het deel venster **knoop punten** .

3. Nadat de promotie is voltooid, wordt in de kolom **status** **OK** weer gegeven voor de nieuwe site server in de *actieve* modus en voor de nieuwe site server in de *passieve* modus.

4. In de **beheer**  >  **site configuratie**  >  **sites**, de naam van de primaire site server, wordt nu de naam van de nieuwe site server in de *actieve* modus weer gegeven.
Ga voor gedetailleerde status naar **monitoring**  >  **site server status**.
    - In de kolom **modus** wordt aangegeven welke server *actief* of *passief*is.

    - Bij het promo veren van een server van de passieve modus naar de actieve modus, selecteert u de site server die u promoveert naar actief en kiest u **status weer geven** op het lint. Hiermee opent u het venster **status van site server promotie** waarin extra details over het proces worden weer gegeven.

Wanneer een site server in de actieve modus overschakelt naar de passieve modus, wordt alleen de site systeemrol passief gemaakt. Alle andere site systeem rollen die op die computer zijn geïnstalleerd, blijven actief en toegankelijk voor clients.


### <a name="daily-monitoring"></a>Dagelijkse bewaking
Wanneer u een primaire site in de passieve modus hebt, controleert u deze dagelijks zodat deze synchroon blijft met de actieve modus site server en klaar voor gebruik. Als u dit wilt doen, gaat u naar **monitoring**  >  **site server status**. Hier kunt u de site servers van de actieve modus en de passieve modus weer geven.

Het tabblad **samen vatting** :
- In de kolom **modus** wordt aangegeven welke server actief of passief is.
- In de kolom **status** wordt **OK** weer gegeven wanneer de server van de passieve modus is gesynchroniseerd met de server in de actieve modus.
- Als u meer informatie wilt weer geven over de status van inhouds synchronisatie, klikt u op **status weer geven** van de status van de synchronisatie van inhoud. Hiermee opent u het tabblad inhouds bibliotheek waar u problemen met de synchronisatie van inhoud kunt oplossen.

Het tabblad **inhouds bibliotheek** :
- Bekijk de **status** voor inhoud die synchroniseert van de actieve site server naar de site server in de passieve modus.
- U kunt inhoud met de status **mislukt**selecteren en vervolgens **geselecteerde items** vanuit het lint synchroniseren selecteren. Met deze actie wordt geprobeerd deze inhoud opnieuw te synchroniseren van de bron van de inhoud naar de site server van de passieve modus. Tijdens het herstel wordt de status weer gegeven als **actief**en wanneer deze is gesynchroniseerd, wordt deze weer gegeven als **geslaagd**.

### <a name="try-it-out"></a>Probeer het nu!
Voer de volgende taken uit en stuur ons **feedback** via het tabblad **Start** van het lint om ons te laten weten hoe het werkt:
- Ik kan een primaire site installeren in de passieve modus.
- Ik kan de-console gebruiken om de site server van de passieve modus te promo veren om deze de actieve modus site server te maken en de status wijziging voor beide site servers te bevestigen.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Vertrouwens relatie voor specifieke bestanden en mappen in een Device Guard-beleid toevoegen
<!-- 1324676 -->
In deze release hebben we meer mogelijkheden toegevoegd aan het [device Guard](../../protect/deploy-use/use-device-guard-with-configuration-manager.md) -beleids beheer

U kunt nu desgewenst vertrouwen toevoegen voor specifieke bestanden voor mappen in een Device Guard-beleid. Hiermee kunt u het volgende doen:

1. Problemen oplossen met het gedrag van beheerde installatie Programma's
2. Regel-of-Business-Apps vertrouwen die niet met Configuration Manager kunnen worden geïmplementeerd
3. Vertrouw apps die zijn opgenomen in een installatie kopie van een besturings systeem.

### <a name="try-it-out"></a>Probeer het nu!

1. Wanneer u een Device Guard-beleid maakt, klikt u op het tabblad insluitingen van de wizard Device Guard-beleid maken op **toevoegen**.
2. Geef in het dialoog venster **vertrouwd bestand of map toevoegen** informatie op over het bestand of de map die u wilt vertrouwen. U kunt een lokaal bestand of mappad opgeven of verbinding maken met een extern apparaat waarvoor u gemachtigd bent om verbinding te maken en een pad naar een bestand of map op dat apparaat op te geven.
3. Voltooi de wizard.


## <a name="hide-task-sequence-progress"></a>Voortgang van taken reeks verbergen
<!-- 1354291 -->
In deze release kunt u bepalen wanneer de voortgang van taken reeksen wordt weer gegeven voor eind gebruikers met behulp van een nieuwe variabele. Gebruik in uw taken reeks de stap **taken reeks variabele instellen** om de waarde in te stellen voor de variabele **TSDisableProgressUI** om de voortgang van taken reeksen te verbergen of weer te geven. U kunt de stap taken reeks variabele instellen meerdere keren in een taken reeks gebruiken om de waarde voor de variabele te wijzigen. Hiermee kunt u de voortgang van taken reeksen in verschillende secties van de taken reeks verbergen of weer geven.

#### <a name="to-hide-task-sequence-progress"></a>Voortgang van taken reeks verbergen
Gebruik in de taken reeks editor de stap [taken reeks variabele instellen](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) om de waarde van de variabele **TSDisableProgressUI** in te stellen op **True** om de voortgang van de taken reeks te verbergen.

#### <a name="to-display-task-sequence-progress"></a>Voortgang van taken reeks weer geven
Gebruik in de taken reeks editor de stap [taken reeks variabele instellen](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) om de waarde van de variabele **TSDisableProgressUI** in te stellen op **False** om de voortgang van de taken reeks weer te geven.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Een andere inhouds locatie voor installatie-inhoud opgeven en inhoud verwijderen
<!-- 1097546 -->
In Configuration Manager vandaag geeft u de installatie locatie op die de Setup-bestanden voor een app bevat. Wanneer u een installatie locatie opgeeft, wordt dit ook gebruikt als de verwijderings locatie voor de toepassings inhoud.
Op basis van uw feedback, wanneer u een geïmplementeerde toepassing wilt verwijderen en de inhoud van de app bevindt zich niet op de client computer, zal de client alle installatie bestanden van de app opnieuw downloaden voordat de toepassing wordt verwijderd.
Als u dit probleem wilt oplossen, kunt u nu zowel de locatie van de installatie-inhoud als een optionele locatie voor het verwijderen van inhoud opgeven. U kunt er ook voor kiezen om een locatie voor de installatie van inhoud niet op te geven.

### <a name="try-it-out"></a>Probeer het eens!

1. Klik in de eigenschappen van het implementatie type van een toepassing op het tabblad **inhoud** .
2. Configureer de **locatie** van de installatie-inhoud als normaal.
3. Kies een van de volgende opties voor het **verwijderen van inhouds instellingen**:
   - **Hetzelfde als de installatie-inhoud** : dezelfde inhouds locatie wordt gebruikt ongeacht of u de toepassing installeert of verwijdert.
   - **Geen inhoud voor verwijderen** : Kies deze optie als u geen locatie voor het verwijderen van inhoud wilt opgeven voor de toepassing.
   - **Afwijkend van installatie-inhoud** : Kies deze optie als u een andere locatie voor installatie-inhoud wilt opgeven dan de locatie van de installatie-inhoud.
5. Als u hebt gekozen voor **inhoud installeren**, bladert u naar of voert u de locatie in van de toepassings inhoud die wordt gebruikt om de toepassing te verwijderen.
6. Klik op **OK** om het dialoog venster Eigenschappen van implementatie type te sluiten.


## <a name="accessibility-improvements"></a>Verbeterde toegankelijkheid  
<!--1253000 -->
In deze preview worden verschillende verbeteringen geïntroduceerd in de [toegankelijkheids functies](../understand/accessibility-features.md) in de Configuration Manager-console. Deze omvatten:     

**Nieuwe sneltoetsen om de console te verplaatsen:**
- CTRL + M: Hiermee stelt u de focus in op het hoofd venster (centraal).
- CTRL + T: Hiermee wordt de focus ingesteld op het bovenste knoop punt in het navigatie deel venster. Als de focus zich al in dat deel venster bevindt, wordt de focus ingesteld op het laatste knoop punt dat u hebt bezocht.
- CTRL + I: Hiermee stelt u de focus in op de breadcrumb-balk onder het lint.
- CTRL + L: Hiermee stelt u de focus naar het **Zoek** veld in, indien beschikbaar.
- CTRL + D: Hiermee stelt u de focus in op het detail venster, indien beschikbaar.
- Alt: verandert de focus in en uit het lint.

**Algemene verbeteringen:**
- Verbeterde navigatie in het navigatie deel venster wanneer u de letters van een naam van een knoop punt typt.
- Toetsenbord navigatie via de hoofd weergave en het lint is nu circulair.
- Toetsenbord navigatie in het detail venster is nu circulair. Als u wilt terugkeren naar het vorige object of deel venster, gebruikt u CTRL + D en vervolgens SHIFT + TAB.
- Nadat u een werkruimte weergave hebt vernieuwd, wordt de focus ingesteld op het hoofd venster van die werk ruimte.
- Er is een probleem opgelost waardoor scherm lezers de namen van lijst items kunnen aankondigen.
- Er zijn toegankelijke namen toegevoegd voor meerdere besturings elementen op de pagina waarmee scherm lezers belang rijke informatie kunnen aankondigen.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Wijzigingen in de wizard Azure-Services ter ondersteuning van Upgradegereedheid
<!-- 1353331 -->
Vanaf deze release gebruikt u de wizard Azure-Services om een verbinding te configureren van Configuration Manager naar Upgradegereedheid. Het gebruik van de wizard vereenvoudigt de configuratie van de connector met behulp van een algemene wizard voor gerelateerde Azure-Services.   

Hoewel de methode voor het configureren van de verbinding is gewijzigd, worden de vereisten voor de verbinding en het gebruik van Upgradegereedheid ongewijzigd blijven.   

### <a name="prerequisites-for-upgrade-readiness"></a>Vereisten voor Upgradegereedheid
De vereisten voor een verbinding met Upgradegereedheid zijn niet gewijzigd ten opzichte van die voor de Current Branch van Configuration Manager. Ze worden hier voor het gemak herhaald:  

**Vereisten**
- Om de verbinding toe te voegen, moet uw Configuration Manager-omgeving eerst een [service aansluitpunt](../servers/deploy/configure/about-the-service-connection-point.md) in een [online modus](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)configureren. Wanneer u de verbinding aan uw omgeving toevoegt, wordt de micro soft monitoring agent ook geïnstalleerd op de computer waarop deze site systeemrol wordt uitgevoerd.
- Registreer Configuration Manager als een hulp programma voor het beheer van webtoepassingen en/of Web-API en haal de [client-id op uit deze registratie](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Maak een client sleutel voor het geregistreerde beheer programma in Azure Active Directory.
- Geef in de Azure Portal de geregistreerde Web-app met toestemming voor toegang tot OMS.

> [!IMPORTANT]       
> Wanneer u machtigingen voor toegang tot OMS configureert, moet u de rol **Inzender** kiezen en de machtigingen toewijzen aan de resource groep van de geregistreerde app.

Nadat de vereisten zijn geconfigureerd, kunt u de wizard gebruiken om de verbinding te maken.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Gebruik de wizard Azure-Services om Upgradegereedheid te configureren
1. Ga in de-console naar **beheer**  >  **overzicht**  >  **Cloud Services**  >  **Azure-Services**en kies vervolgens **Azure-Services configureren** op het tabblad **Start** van het lint om de **wizard Azure-Services**te starten.

2. Selecteer op de pagina **Azure-Services** de **Upgradegereedheid-connector**en klik vervolgens op **volgende**.

3. Geef uw **Azure-omgeving** op de pagina **app** op (de Technical Preview ondersteunt alleen de open bare Cloud). Klik vervolgens op **importeren** om het venster **apps importeren** te openen.

4. Geef in het venster **apps importeren** Details op voor een web-app die al in uw Azure AD voor komt.
    - Geef een beschrijvende naam op voor de naam van de Azure AD-Tenant. Geef vervolgens de Tenant-ID, toepassings naam, client-ID, geheime sleutel voor de Azure-web-app en de App-ID-URI op.
    - Klik op **controleren**en klik op **OK** om door te gaan.

5.  Geef op de pagina **configuratie** het abonnement, de resource groep en de Windows Analytics-werk ruimte op die u met deze verbinding wilt gebruiken om Upgradegereedheid.  

6. Klik op **volgende** om naar de pagina **samen vatting** te gaan en voltooi vervolgens de wizard om de verbinding te maken.


## <a name="new-client-settings-for-cloud-services"></a>Nieuwe client instellingen voor Cloud Services
<!-- 1319883 -->

In deze release hebben we twee nieuwe client instellingen toegevoegd aan Configuration Manager. Deze vindt u in de sectie **Cloud Services** .  Deze instellingen bieden u de volgende mogelijkheden:

- Bepaal welke Configuration Manager-clients toegang hebben tot een geconfigureerde Cloud beheer gateway.
- Windows 10-domein-gekoppelde Configuration Manager-clients automatisch registreren bij Azure Active Directory.

Deze nieuwe instellingen helpen u bij het uitvoeren van de mogelijkheden die worden beschreven in de [Configuration Manager 1705 Technical Preview](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management).

### <a name="before-you-start"></a>Voordat u begint

U moet Azure AD Connect hebben geïnstalleerd en geconfigureerd tussen uw on-premises Active Directory en uw Azure AD-Tenant.

Als u de verbinding verwijdert, worden apparaten niet ongedaan gemaakt, maar worden er geen nieuwe apparaten geregistreerd.

### <a name="try-it-out"></a>Probeer het nu!

1. De volgende client instellingen (gevonden in de Cloud Services) configureren met behulp van de informatie in het [configureren van client instellingen](../clients/deploy/configure-client-settings.md).
   - **Nieuwe Windows 10-apparaten die lid zijn van een domein automatisch registreren bij Azure Active Directory** : ingesteld op **Ja** (standaard) of **Nee**.
   - **Clients inschakelen om een Cloud beheer gateway te gebruiken** : ingesteld op **Ja** (standaard) of **Nee**.
2. Implementeer de client instellingen op de vereiste verzameling apparaten.

Als u wilt controleren of het apparaat is gekoppeld aan Azure AD, voert u de opdracht uit **dsregcmd.exe/status** in een opdracht prompt venster. In het veld **AzureAdjoined** in de resultaten wordt **Ja** weer gegeven als het apparaat is toegevoegd aan Azure AD.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Power shell-scripts maken en uitvoeren vanuit de Configuration Manager-console
<!-- 1236459 -->

In Configuration Manager kunt u scripts implementeren op client apparaten met behulp van pakketten en Program ma's. In deze Technical Preview hebt u nieuwe functionaliteit toegevoegd waarmee u de volgende acties kunt uitvoeren:

- Power shell-scripts importeren in Configuration Manager
- De scripts bewerken vanuit de Configuration Manager-console (alleen voor niet-ondertekende scripts)
- Scripts markeren als goedgekeurd of geweigerd, ter verbetering van de beveiliging
- Scripts uitvoeren op verzamelingen van Windows-client-Pc's en on-premises beheerde Windows-Pc's. U kunt in plaats daarvan geen scripts implementeren. deze worden in bijna realtime uitgevoerd op client apparaten.
- Bekijk de resultaten die door het script worden geretourneerd in de Configuration Manager-console.


### <a name="prerequisites"></a>Vereisten

Als u scripts wilt gebruiken, moet u lid zijn van de juiste Configuration Manager beveiligingsrol.

- **Als u scripts wilt importeren en schrijven,** moet uw account beschikken over **Create** -machtigingen voor **SMS-scripts** in de beveiligingsrol **volledige beheerder** .
- **Als u scripts wilt goed keuren of weigeren,** moet uw account beschikken over **goedkeurings** machtigingen voor **SMS-scripts** in de beveiligingsrol **volledige beheerder** .
- **Als u scripts wilt uitvoeren** , moet uw account beschikken over de machtigingen voor het **uitvoeren van scripts** voor **verzamelingen** in de beveiligingsrol **nalevings instellingen Manager** .

Zie de [basis principes van beheer op basis van rollen](../understand/fundamentals-of-role-based-administration.md)voor meer informatie over Configuration Manager beveiligings rollen.

Standaard kunnen gebruikers geen script goed keuren dat ze hebben gemaakt. Omdat scripts krachtig, veelzijdig en kunnen worden geïmplementeerd op veel apparaten, hebben we een nieuw concept geïntroduceerd van de mogelijkheid om de rollen te scheiden tussen de persoon die het script en de persoon die het script goedkeurt. Dit biedt een extra beveiligings niveau voor het uitvoeren van een script zonder toezicht. U kunt deze secundaire goed keuring uitschakelen voor het gemak van de tests, met name tijdens de Technical Preview-versie.

Gebruikers toestaan hun eigen scripts goed te keuren:

1. Klik op **Beheer**in de Configuration Manager-console.
2. Vouw in de werkruimte **Beheer****Siteconfiguratie**uit en klik vervolgens op **Sites**.
3. Kies uw site in de lijst met sites en klik vervolgens op het tabblad **Start** in de groep **sites** op **hiërarchie-instellingen**.
4. Schakel op het tabblad **Algemeen** van het dialoog venster **Eigenschappen van hiërarchie-instellingen** het selectie vakje **niet toe dat auteurs van scripts hun eigen scripts goed keuren**.


### <a name="try-it-out"></a>Probeer het nu!

#### <a name="import-and-edit-a-script"></a>Een script importeren en bewerken

1. Klik in de Configuration Manager-console op **Softwarebibliotheek**.
2. Klik in de werk ruimte **software bibliotheek** op **scripts**.
3. Klik op het tabblad **Start** in de groep **maken** op **script maken**.
4. Configureer op de pagina **script** van de wizard **script maken** het volgende:
   - **Script naam** : Voer een naam in voor het script. Hoewel u meerdere scripts met dezelfde naam kunt maken, is het voor u moeilijker om het script te vinden dat u nodig hebt in de Configuration Manager-console.
   - **Script taal** -momenteel worden alleen **Power shell** -scripts ondersteund.
   - **Importeer** een Power shell-script in de-console. Het script wordt weer gegeven in het veld **script** .
   - **Clear** : Hiermee verwijdert u het huidige script uit het veld **script** .
   - **Script** : het momenteel geïmporteerde script wordt weer gegeven. U kunt het script in dit veld indien nodig bewerken.
5. Voltooi de wizard. Het nieuwe script wordt weer gegeven in **de lijst met de status** van **wachten op goed keuring**. Voordat u dit script op client apparaten kunt uitvoeren, moet u het goed keuren.


#### <a name="approve-or-deny-a-script"></a>Een script goed keuren of weigeren



Voordat u een script kunt uitvoeren, moet dit worden goedgekeurd. Een script goed keuren:

1. Klik in de Configuration Manager-console op **Softwarebibliotheek**.
2. Klik in de werk ruimte **software bibliotheek** op **scripts**.
3. Kies in de lijst **script** het script dat u wilt goed keuren of weigeren, en klik vervolgens op het tabblad **Start** in de groep **script** op **goed keuren/weigeren**.
4. In het dialoog venster **script goed keuren of** weigeren kunt u het script **goed keuren**of **weigeren** en eventueel een opmerking over uw beslissing invoeren. Als u een script weigert, kan het niet worden uitgevoerd op client apparaten.
5. Voltooi de wizard. In de lijst met **scripts** ziet u de kolom wijziging **goedkeurings status** , afhankelijk van de actie die u hebt ondernomen.

#### <a name="run-a-script"></a>Een script uitvoeren

Zodra een script is goedgekeurd, kan dit worden uitgevoerd op basis van een verzameling die u kiest.

1. Klik op **Activa en naleving**op de Configuration Manager-console.
2. Klik op **Apparaatverzamelingen** in de werkruimte **Activa en naleving**.
3. Klik in de lijst **apparaat Collections** op de verzameling apparaten waarop u het script wilt uitvoeren.
3. Klik op het tabblad **Start** in de groep **alle systemen** op **script uitvoeren**.
4. Kies op de pagina **script** van de wizard **script uitvoeren** een script uit de lijst. Alleen goedgekeurde scripts worden weer gegeven. Klik op **volgende**en voltooi de wizard.

#### <a name="monitor-a-script"></a>Een script bewaken

Nadat u een script hebt uitgevoerd op client apparaten, gebruikt u deze procedure om het succes van de bewerking te controleren.

1. Klik in de Configuration Manager-console op **bewaking**.
2. Klik in de werk ruimte **bewaking** op **script resultaten**.
3. In de lijst met **script resultaten** bekijkt u de resultaten voor elk script dat u hebt uitgevoerd op client apparaten. De afsluit code van het script van **0**geeft doorgaans aan dat het script is uitgevoerd.

## <a name="pxe-network-boot-support-for-ipv6"></a>PXE-netwerk opstart ondersteuning voor IPv6
<!-- 1269793 -->
U kunt nu PXE-netwerk opstart ondersteuning inschakelen voor IPv6 om een implementatie van een taken reeks besturings systeem te starten. Wanneer u deze instelling gebruikt, ondersteunen distributie punten met PXE-functionaliteit zowel IPv4 als IPv6. Voor deze optie is WDS niet vereist en wordt WDS gestopt als deze aanwezig is.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>PXE-opstart ondersteuning inschakelen voor IPv6
Gebruik de volgende procedure om de optie voor IPv6-ondersteuning voor PXE in te scha kelen.

1. Ga in de Configuration Manager-console naar **beheer**  >  **overzicht**  >  **distributie punten**en klik op **Eigenschappen** voor distributie punten met PXE-functionaliteit.
2. Op het tabblad **PXE** selecteert u **IPv6 ondersteunen** om IPv6-ondersteuning voor PXE in te scha kelen.

## <a name="manage-microsoft-surface-driver-updates"></a>Updates voor micro soft Surface drivers beheren
<!-- 1098490 -->
U kunt nu Configuration Manager gebruiken om updates van micro soft Surface-Stuur Programma's te beheren.

### <a name="prerequisites"></a>Vereisten
Alle software-update punten moeten Windows Server 2016 uitvoeren.

### <a name="try-it-out"></a>Probeer het nu!
Voer de volgende taken uit en stuur ons **feedback** via het tabblad **Start** van het lint om ons te laten weten hoe het werkt:
1. Synchronisatie inschakelen voor micro soft Surface-Stuur Programma's. Gebruik de procedure in [classificatie en producten configureren](../../sum/get-started/configure-classifications-and-products.md) en selecteer **micro soft Surface-Stuur Programma's en firmware-updates** op het tabblad **classificaties** om Surface-Stuur Programma's in te scha kelen.
2. [Synchroniseer de micro soft Surface-Stuur Programma's](../../sum/get-started/synchronize-software-updates.md).
3. [Gesynchroniseerde Stuur Programma's van micro soft Surface implementeren](../../sum/deploy-use/deploy-software-updates.md)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Windows Update voor beleid voor bedrijfs uitstel configureren
<!-- 1290890 -->
U kunt nu uitstel beleid configureren voor Windows 10-onderdelen updates of kwaliteits updates voor Windows 10-apparaten die rechtstreeks worden beheerd door Windows Update voor bedrijven. U kunt het uitstel beleid beheren in het knoop punt nieuwe **Windows Update voor bedrijfs beleid** onder **software bibliotheek**  >  **Windows 10 Servicing**.

### <a name="prerequisites"></a>Vereisten
Windows 10-apparaten die worden beheerd door Windows Update voor bedrijven, moeten verbinding hebben met internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Een Windows Update voor beleid voor bedrijfs uitstel maken
1. In **software bibliotheek**  >  **Windows 10-onderhouds**  >  **Windows Update voor bedrijfs beleid**
2. Selecteer op het tabblad **Start** in de groep **maken** de optie **Windows Update maken voor bedrijfs beleid** om de wizard Windows Update voor bedrijven-beleid maken te openen.
3. Geef op de pagina **Algemeen** een naam en beschrijving voor het beleid op.
4. Configureer op de pagina **uitstel beleid** of functie-updates moeten worden uitstellen of onderbroken.    
    Upgrades van onderdelen zijn over het algemeen nieuwe functies van Windows. Nadat u de instelling voor het niveau van de **Branch-gereedheid** hebt geconfigureerd, kunt u opgeven of en hoe lang u de ontvangst van onderdelen wilt uitstellen na hun Beschik baarheid van micro soft.
    - **Branch-gereedheids niveau**: Stel de vertakking in waarvoor het apparaat Windows-updates (Current Branch of current branch for Business) zal ontvangen.
    - **Uitstel periode (dagen)**: Geef het aantal dagen op waarvoor updates van onderdelen worden uitgesteld. U kunt deze upgrades van onderdelen uitstellen gedurende een periode van 180 dagen vanaf de release.
    - **Onderbreken van onderdelen updates starten**: Selecteer of u wilt dat apparaten de updates van onderdelen gedurende een periode van maxi maal 60 dagen ontvangen vanaf het moment dat u de updates onderbreekt. Als het maximum aantal dagen is verstreken, verloopt de functionaliteit voor onderbreken automatisch en zoekt het apparaat in Windows-Updates naar toepasselijke updates. Na deze scan kunt u de updates opnieuw onderbreken. U kunt de onderbreking van de functie-updates uitschakelen door het selectie vakje uit te scha kelen.   
5. Kies of u kwaliteits updates wilt uitstellen of onderbreken.     
    Kwaliteitsupdates zijn doorgaans oplossingen en verbeteringen in de bestaande Windows-functionaliteit. Deze worden normaal gesproken op de eerste dinsdag van elke maand gepubliceerd, maar kunnen op elk gewenst moment door Microsoft worden vrijgegeven. U kunt opgeven of, en hoe u de installatie van kwaliteitsupdates wilt uitstellen na hun beschikbaarheid.
    - **Uitstel periode (dagen)**: Geef het aantal dagen op waarvoor updates van onderdelen worden uitgesteld. U kunt deze upgrades van onderdelen uitstellen gedurende een periode van 180 dagen vanaf de release.
    - Het **starten van kwaliteits updates onderbreken**: Selecteer of u wilt onderbreken dat apparaten een periode van maxi maal 35 dagen ontvangen van de tijd dat u de updates hebt onderbroken. Als het maximum aantal dagen is verstreken, verloopt de functionaliteit voor onderbreken automatisch en zoekt het apparaat in Windows-Updates naar toepasselijke updates. Na deze scan kunt u de updates opnieuw onderbreken. U kunt de kwaliteit van de kwaliteits updates verwijderen door het selectie vakje uit te scha kelen.
6. Selecteer **updates van andere micro soft-producten installeren** om de groeps beleids instelling in te scha kelen waarmee uitstel instellingen worden ingesteld die van toepassing zijn op Microsoft Update, evenals Windows-updates.
7. Selecteer **Stuur Programma's insluiten met Windows Update** om stuur Programma's automatisch bij te werken van Windows-updates. Als u deze instelling uitschakelt, worden stuur programma-updates niet gedownload van Windows-updates.
8. Voltooi de wizard om het nieuwe uitstel beleid te maken.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Een Windows Update voor beleid voor bedrijfs uitstel implementeren
1. In **software bibliotheek**  >  **Windows 10-onderhouds**  >  **Windows Update voor bedrijfs beleid**
2. Selecteer op het tabblad **Start** in de groep **implementatie** de optie **Windows Update implementeren voor bedrijfs beleid**.
3. Configureer de volgende instellingen:
    - **Te implementeren configuratie beleid**: selecteer de Windows Update voor bedrijfs beleid dat u wilt implementeren.
    - **Verzameling**: Klik op **Bladeren** om de verzameling te selecteren waarvoor u het beleid wilt implementeren.
    - **Regels die niet compliant zijn herstellen, indien ondersteund**: Schakel deze optie in om automatisch regels te herstellen die niet compatibel zijn voor Windows Management INSTRUMENTATION (WMI), het REGI ster, scripts en alle instellingen voor mobiele apparaten die zijn geregistreerd door Configuration Manager.
    - **Herstel toestaan buiten het onderhouds venster**: als er een onderhouds venster is geconfigureerd voor de verzameling waarnaar u het beleid implementeert, schakelt u deze optie in om de waarde buiten het onderhouds venster te laten herstellen met de instellingen voor naleving. Zie [onderhouds Vensters gebruiken](../clients/manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.
    - **Waarschuwing genereren**: Hiermee configureert u een waarschuwing die wordt gegenereerd als de naleving van de configuratie basislijn op een opgegeven datum en tijd minder is dan een opgegeven percentage. U kunt tevens opgeven of u een melding naar System Center Operations Manager wilt verzenden.
    - **Wille keurige vertraging (uren)**: Hiermee geeft u een vertragings venster op om overmatige verwerking van de registratie service voor netwerk apparaten te voor komen. De standaardwaarde is 64 uur.
    - **Planning**: Geef het evaluatie schema voor naleving op waarmee het geïmplementeerde profiel wordt geëvalueerd op client computers. U kunt een eenvoudig of aangepast schema opgeven. Het profiel wordt door de clientcomputers beoordeeld wanneer de gebruiker zich aanmeldt.
4.  Voltooi de wizard om het profiel te implementeren.



## <a name="support-for-entrust-certification-authorities"></a>Ondersteuning voor vertrouwde certificerings instanties
<!-- 1350740 -->
Configuration Manager ondersteunt nu het vertrouwen van certificerings instanties; Hiermee wordt de levering van PFX-certificaten op apparaten die zijn Inge schreven bij Microsoft Intune.

U kunt de verantwoordelijkheid configureren als de certificerings instantie bij het toevoegen van een rol voor een certificaat registratiepunt in Configuration Manager. Bij het toevoegen van een nieuw certificaat profiel dat PFX-certificaten uitgeeft, kunt u een micro soft-of reactieve certificerings instantie selecteren.

**Bekend probleem**: In de 1706 Technical Preview worden geen pfx-certificaten uitgegeven voor micro soft-certificerings instanties. Dit heeft geen invloed op geïmporteerde PFX-certificaten of SCEP-profielen.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Cisco-ondersteuning (IPsec) voor iOS VPN-profielen
<!-- 1321367 -->

U kunt een iOS VPN-profiel maken met Cisco (IPsec) als het verbindings type. Zie [VPN-profielen maken](../../protect/deploy-use/create-vpn-profiles.md#create-a-vpn-profile)voor meer informatie.


## <a name="new-windows-configuration-item-settings"></a>Instellingen voor nieuwe Windows-configuratie-items
<!-- 1354715 -->

In deze release hebben we de volgende nieuwe instellingen toegevoegd die u kunt gebruiken in Windows-configuratie-items:

### <a name="password"></a>Wachtwoord

- **Apparaatversleuteling**

### <a name="device"></a>Apparaat

- **Regio-instellingen aanpassen (alleen Desktop)**
- **Instellingen voor in-/uitschakelen en slaap stand wijzigen**
- **Taal instellingen wijzigen**
- **Systeem tijd wijzigen**
- **Apparaatnaam wijzigen**

### <a name="store"></a>Opslaan

- **Apps uit de Store automatisch bijwerken**
- **Alleen persoonlijke Store gebruiken**
- **Door store afkomstige app starten**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Toegang tot about: Flags blok keren**
- **SmartScreen-prompt negeren**
- **SmartScreen-prompt voor bestanden negeren**
- **WebRTC localhost IP-adres**
- **Standaard zoekmachine**
- **URL van OpenSearch XML**
- **Start pagina's (alleen Desktop)**

Zie apparaatcompatibiliteit [controleren](../../compliance/understand/ensure-device-compliance.md)voor meer informatie over nalevings instellingen.


## <a name="new-device-compliance-policy-rules"></a>Nieuwe regels voor nalevings beleid voor apparaten

* **Vereist wachtwoord type**. Geef op of de gebruiker een alfanumeriek wacht woord of een numeriek wacht woord moet maken. Voor alfanumerieke wacht woorden geeft u ook het minimum aantal teken sets op waaruit het wacht woord moet bestaan. De vier teken sets zijn: hoofd letters, kleine letters, symbolen en cijfers.

  **Ondersteund in:**
  * Windows Phone 8+
  * Windows 8.1 +
  * iOS 6+
<br></br>
* **USB-fout opsporing blok keren op apparaat**. U hoeft deze instellingen niet te configureren, omdat USB-fout opsporing al is uitgeschakeld op Android for work-apparaten.

  **Ondersteund in:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Apps van onbekende bronnen blok keren**. Vereisen dat de installatie van apps van onbekende bronnen wordt voor komen. U hoeft deze instelling niet te configureren, omdat de installatie van onbekende bronnen altijd wordt beperkt door Android for work-apparaten.

  **Ondersteund in:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Dreigingen moeten worden gescand op apps**. Met deze instelling geeft u op dat de functie apps controleren is ingeschakeld op het apparaat.

  **Ondersteund in:**
  * Android 4,2 tot en met 4,4
  * Samsung KNOX Standard 4.0+


## <a name="new-mobile-application-management-policy-settings"></a>Nieuwe Mobile Application Management-beleids instellingen
Vanaf deze release kunt u drie nieuwe Mobile Application Management-beleids instellingen (MAM) gebruiken:

- **Scherm opname blok keren (alleen Android-apparaten):** Hiermee geeft u op dat de mogelijkheden voor scherm opname van het apparaat worden geblokkeerd wanneer deze app wordt gebruikt.

- **Synchronisatie van contact personen uitschakelen:** Hiermee voor komt u dat de app gegevens opslaat in de systeem eigen contact personen-app op het apparaat.

- **Afdrukken uitschakelen:** Hiermee voor komt u dat de app werk-of school gegevens afdrukt.

## <a name="android-and-ios-enrollment-restrictions"></a>Inschrijvings beperkingen voor Android-en iOS-apparaten
<!-- 1290826 -->
Vanaf deze release kunnen beheerders nu opgeven dat gebruikers geen persoonlijke Android-of iOS-apparaten kunnen inschrijven in hun hybride omgeving. Hierdoor kunt u geregistreerde apparaten beperken tot vooraf gedeclareerde apparaten die eigendom zijn van het bedrijf of iOS-apparaten die zijn Inge schreven met Device Enrollment Program.

### <a name="try-it-out"></a>Probeer het eens
1. Ga in de Configuration Management-console in de werkruimte **Beheer** naar **Cloudservices** > **Microsoft Intune-abonnement**.
2. Klik op het tabblad **Start** in de groep **abonnement** op **platforms configureren** en selecteer vervolgens **Android** of **IOS**.
3. Selecteer **apparaten met persoonlijke eigendom blok keren**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Beleid voor het beheer van Android for work-toepassingen voor kopiëren en plakken
We hebben de instellings beschrijvingen voor Android for work-configuratie-items bijgewerkt voor het **delen van gegevens tussen werk en persoonlijk profiel toestaan**.

|Voor 1706 Technical Preview | Nieuwe optie naam | Gedrag|
|-|-|-|
|Delen buiten grenzen voorkomen| Standaard beperkingen voor delen| Werk-naar-persoonlijk: standaard (wordt naar verwachting geblokkeerd voor alle versies) <br>Persoonlijk-op-werk: standaard (toegestaan op 6. x +, geblokkeerd op 5. x)|
|Geen beperkingen| Apps in persoonlijk profiel kunnen aanvragen voor delen van het werk profiel verwerken| Voor persoonlijk gebruik: toegestaan  <br>Persoonlijk-op-werk: toegestaan|
|Met apps in het werk profiel kunnen aanvragen voor delen van het persoonlijke profiel worden verwerkt |Met apps in het werk profiel kunnen aanvragen voor delen van het persoonlijke profiel worden verwerkt |Werk-naar-persoonlijk: standaard<br>Persoonlijk-op-werk: toegestaan<br>(Alleen nuttig op 5. x waar persoonlijk werk wordt geblokkeerd)|

Geen van deze opties voor komt dat het gedrag kopiëren en plakken wordt voor komen. Er is een aangepaste instelling toegevoegd aan de service en Bedrijfsportal app in 1704 die kan worden geconfigureerd om kopiëren-plakken te voor komen. Dit kan worden ingesteld via een aangepaste URI.

- OMA-URI:./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Waardetype: Booleaans

Als u DisallowCrossProfileCopyPaste instelt op True, wordt het gedrag van kopiëren en plakken tussen Android for work-persoonlijke en werk profielen voor komen.

### <a name="try-it-out"></a>Probeer het eens
1. Selecteer in de Configuration Manager-console **activa en naleving**  >  **overzicht**  >  configuratie-items voor**compatibiliteits instellingen**  >  **Configuration items**.
2. Kies **maken** om een nieuw configuratie-item te maken en geef **naam** en **Android for work**op.
3. In de instellings groepen voor apparaten die u wilt configureren, selecteert u **werk profiel**en klikt u op **volgende**.
4. Selecteer de waarde voor het **delen van gegevens tussen werk en persoonlijke profielen toestaan**en voltooi vervolgens de wizard.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Apparaatstatusverklaring beoordeling voor nalevings beleid voor voorwaardelijke toegang
<!-- 1097546 -->
Vanaf deze release kunt u Apparaatstatusverklaring status gebruiken als nalevings beleids regel voor voorwaardelijke toegang tot bedrijfs resources.

### <a name="try-it-out"></a>Probeer het eens
Selecteer een Apparaatstatusverklaring regel als onderdeel van een beoordeling van het nalevings beleid.

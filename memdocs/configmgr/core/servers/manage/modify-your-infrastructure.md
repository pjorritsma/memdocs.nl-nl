---
title: Infrastructuur wijzigen
titleSuffix: Configuration Manager
description: Breng wijzigingen aan of onderneem acties die van invloed zijn op uw Configuration Manager-infra structuur.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713672"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>Uw Configuration Manager-infra structuur wijzigen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u een of meer sites hebt geïnstalleerd, moet u mogelijk configuraties wijzigen of acties ondernemen die van invloed zijn op uw infra structuur.

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a>De SMS-provider beheren

De SMS-provider biedt het punt van beheer contact voor een of meer Configuration Manager-consoles. Wanneer u meerdere SMS-providers installeert, kunt u redundantie bieden voor contact punten om uw site en hiërarchie te beheren.

Op elke Configuration Manager-site kunt u de installatie opnieuw uitvoeren om de volgende handelingen uit te voeren:

- Een extra exemplaar van de SMS-provider toevoegen. Elk extra exemplaar van de SMS-provider moet zich op een afzonderlijke computer bevindt.

- Verwijder een exemplaar van de SMS-provider. Als u de laatste SMS-provider voor een site wilt verwijderen, moet u de site verwijderen.

Controleer de installatie of verwijdering van de SMS-provider door de map **ConfigMgrSetup. log** in de hoofdmap van de site server waarop u Setup uitvoert, te bekijken.

Zie [de SMS-provider plannen](../../plan-design/hierarchy/plan-for-the-sms-provider.md)voordat u de SMS-provider op een site wijzigt.

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>De configuratie van de SMS-provider voor een site beheren  

1. Voer **Configuration Manager Setup** uit `\BIN\X64\setup.exe` vanuit de installatiemap van de Configuration Manager-site.

1. Selecteer op de pagina **aan de slag** de optie **site onderhoud uitvoeren of deze site opnieuw instellen**.

1. Op de pagina **site onderhoud** selecteert u **configuratie van de SMS-provider wijzigen**.

1. Selecteer op de pagina **SMS-providers beheren** een van de volgende opties:

    - **Een nieuwe SMS-provider toevoegen**: Geef de FQDN op van een computer die als host moet fungeren voor de SMS-provider die dit momenteel niet host.

    - **De opgegeven SMS-provider verwijderen**: Selecteer de naam van de computer waarvan u de SMS-provider wilt verwijderen.

    > [!TIP]  
    > Als u de SMS-provider tussen twee computers wilt verplaatsen, installeert u deze eerst op de nieuwe computer. Verwijder deze vervolgens van de oorspronkelijke locatie. Er is geen optie om de SMS-provider te verplaatsen tussen computers.

Nadat de installatie wizard is voltooid, is de configuratie van de SMS-provider voltooid. Controleer in de site- **Eigenschappen**, op het tabblad **Algemeen** , de computers die een SMS-provider hebben geïnstalleerd voor een site.

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a>De Configuration Manager-console beheren

De volgende taken helpen u bij het beheren van de Configuration Manager-console:

- Als u de taal wilt wijzigen die wordt weer gegeven in de Configuration Manager-console, raadpleegt u de sectie [Configuration Manager console taal beheren](#BKMK_ManageConsoleLanguages) .

- Zie [Configuration Manager-consoles installeren](../deploy/install/install-consoles.md)voor meer informatie over het installeren van extra consoles.

- Zie de sectie [DCOM-machtigingen configureren voor externe Configuration Manager-consoles](#BKMK_ConfigDCOMforRemoteConsole) voor informatie over het configureren van DCOM-machtigingen voor het inschakelen van consoles die zich op afstand van de site server bevinden.

- Zie [het beheer bereik van een gebruiker met beheerders](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)rechten aanpassen als u beheerders machtigingen wilt wijzigen om te beperken wat gebruikers in de console kunnen zien en doen.

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a>De taal van de Configuration Manager-console beheren

Tijdens de installatie van de site server worden de installatie bestanden van de Configuration Manager-console en ondersteunde taal pakketten voor `\Tools\ConsoleSetup` de site gekopieerd naar de submap van het installatiepad van Configuration Manager op de site server.

- Wanneer u de installatie van de Configuration Manager-console start vanuit deze map op de site server, worden de Configuration Manager-console en ondersteunde taal pakket bestanden naar de computer gekopieerd.

- Wanneer er een taal pakket beschikbaar is voor de huidige taal instelling op de computer, wordt de Configuration Manager-console in die taal geopend.

- Als het gekoppelde taal pakket niet beschikbaar is voor de Configuration Manager-console, wordt de console geopend in het Engels (Verenigde Staten).

U kunt bijvoorbeeld de Configuration Manager-console installeren vanaf een site server die Engels, Duits en Frans ondersteunt. Als u de Configuration Manager-console opent op een computer met een geconfigureerde taal instelling van het Frans, wordt de console geopend in het Frans. Als u de Configuration Manager-console opent op een computer met een geconfigureerde taal van Japans, wordt de console in het Engels geopend, omdat het Japanse taal pakket niet beschikbaar is.  

Telkens wanneer de Configuration Manager-console wordt geopend:

- TT bepaalt de geconfigureerde taal instellingen voor de computer
- Verifieert of een gekoppeld taal pakket beschikbaar is voor de Configuration Manager-console
- Hiermee opent u de-console met behulp van het juiste taal pakket

Als u de Configuration Manager-console in het Engels wilt openen, ongeacht de geconfigureerde taal instellingen op de computer, verwijdert of wijzigt u de naam van de taal pakket bestanden op de computer.

Gebruik de volgende procedures om de Configuration Manager-console in het Engels te starten, ongeacht de geconfigureerde land instelling op de computer.  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Een alleen-Engelse versie van de Configuration Manager-console installeren op computers  

1. Blader in Windows Verkenner naar `\Tools\ConsoleSetup\LanguagePack` het installatiepad van Configuration Manager.

1. Wijzig de namen van de **MSP**- en **MST**-bestanden. U kunt bijvoorbeeld de ** &lt;bestands naam\>wijzigen. MSP** naar ** &lt;de bestands\>naam. MSP. disabled**.

1. Installeer de Configuration Manager-console op de computer.

    > [!IMPORTANT]
    > Wanneer er nieuwe server talen voor de site server zijn geconfigureerd, worden de MSP-en mst-bestanden opnieuw naar de map **language pack** gekopieerd en moet u deze procedure herhalen om nieuwe Configuration Manager-consoles alleen in het Engels te installeren.  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Een console taal voor een bestaande installatie van de Configuration Manager-console tijdelijk uitschakelen

1. Sluit de Configuration Manager-console op de computer waarop de Configuration Manager-console wordt uitgevoerd.

1. Blader in Windows Verkenner naar &lt; *ConsoleInstallationPath*> \bin\ op de computer met de Configuration Manager-console.  

1. Wijzig de naam van de toepasselijke taalmap voor de taal die op de computer is geconfigureerd. Als de taalinstellingen voor de computer zijn ingesteld op Duits, kunt de naam van de map **de** wijzigen in **de.disabled**.  

1. Als u de Configuration Manager-console wilt openen in de taal die voor de computer is geconfigureerd, wijzigt u de naam van de map in de oorspronkelijke namen. Wijzig bijvoorbeeld de naam **de.disabled** in **de**.  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a>DCOM-machtigingen configureren voor externe consoles

Het gebruikers account waarmee de Configuration Manager-console wordt uitgevoerd, heeft toestemming nodig voor toegang tot de site database met behulp van de SMS-provider. Een gebruiker met beheerders rechten die gebruikmaakt van een externe Configuration Manager-console, moet ook DCOM-machtigingen voor **externe activering** hebben op:

- De siteservercomputer

- Elke computer die als host fungeert voor een exemplaar van de SMS-provider

De beveiligings groep **SMS-beheerders** verleent toegang tot de SMS-provider op een computer en kan ook worden gebruikt om de vereiste DCOM-machtigingen te verlenen. Deze groep is lokaal op de computer wanneer de SMS-provider wordt uitgevoerd op een lidserver. Het is een domeingebonden groep wanneer de SMS-provider wordt uitgevoerd op een domein controller.

> [!IMPORTANT]
> De Configuration Manager-console maakt gebruik van WMI om verbinding te maken met de SMS-provider en WMI gebruikt intern DCOM. Als de Configuration Manager-console wordt uitgevoerd op een andere computer dan de computer van de SMS-provider, hebt u machtigingen nodig om een DCOM-Server te activeren op de computer van de SMS-provider. Externe activering wordt standaard alleen verleend aan de leden van de ingebouwde groep Administrators.
>
> Als u de SMS admins-groep toestaat toestemming te geven voor externe activering, zou een lid van deze groep DCOM-aanvallen kunnen uitvoeren op de computer van de SMS-provider. Deze configuratie verhoogt ook de kwetsbaarheid van de computer. Controleer de leden van de SMS-beheerdersgroep zorgvuldig om deze dreiging te verminderen.

Gebruik de volgende procedure voor het configureren van elke centrale beheer site (CAS), primaire site server en elke computer waarop de SMS-provider is geïnstalleerd om externe toegang tot Configuration Manager console te verlenen voor gebruikers met beheerders rechten.

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>DCOM-machtigingen configureren voor verbindingen met externe Configuration Manager-console

1. Als beheerder op de doel computer voert u uit `Dcomcnfg.exe` om **Component Services**te openen.

1. Vouw **Component Services**uit, vouw **computers**uit en selecteer vervolgens **mijn computer**. Selecteer **Eigenschappen**in het menu **actie** .

1. Ga in het venster **Eigenschappen van mijn computer** naar het tabblad **COM-beveiliging** . Selecteer in de sectie **machtigingen voor starten en activeren** de optie **limieten bewerken**.

1. Selecteer in het venster **machtigingen voor starten en activeren** de optie **toevoegen**.

1. Typ `SMS Admins`in het venster **gebruikers, computers, service accounts of groepen selecteren** in het veld **Geef de object namen op** en selecteer vervolgens **OK**.

   > [!TIP]
   > Als u de SMS admins-groep wilt zoeken, moet u mogelijk de instelling wijzigen: **van deze locatie**. Deze groep is lokaal op de computer wanneer de SMS-provider wordt uitgevoerd op een lidserver en is een domeingebonden groep wanneer de SMS-provider wordt uitgevoerd op een domein controller.

1. Selecteer in de sectie **machtigingen voor SMS admins** de optie **toestaan** om **externe activering toe** te staan.

1. Selecteer **OK** om de wijzigingen op te slaan en alle vensters te sluiten.

Uw computer is nu geconfigureerd om externe Configuration Manager-console toegang toe te staan voor leden van de SMS admins-groep.

Herhaal deze procedure op elke computer van de SMS-provider die externe Configuration Manager-consoles ondersteunt.

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a>De configuratie van de site database wijzigen

Nadat u een site hebt geïnstalleerd, kunt u de configuratie van de site database en site database server wijzigen. Voer Configuration Manager Setup uit op een CAS-server of primaire site server om wijzigingen aan te brengen. U kunt de sitedatabase verplaatsen naar een nieuw exemplaar van SQL Server op dezelfde computer, of naar een andere computer die een ondersteunde versie van SQL Server uitvoert. Deze wijzigingen worden niet ondersteund voor de database configuratie op secundaire sites.

Zie [Support policy for manual database changes in a Configuration Manager environment](https://support.microsoft.com/kb/3106512) (Ondersteungingsbeleid voor handmatig databasewijzigingen een Configuration Manager-omgeving) voor meer informatie over de beperkingen van de ondersteuning.  

> [!NOTE]
> Wanneer u de database configuratie voor een site wijzigt, worden Configuration Manager services op de site server en externe site systeem servers die met de data base communiceren, Configuration Manager opnieuw opgestart of geïnstalleerd.

### <a name="modify-the-database-configuration"></a>De database configuratie wijzigen

Voer Configuration Manager Setup uit op de site server en selecteer de optie **site onderhoud uitvoeren of deze site opnieuw instellen**. Selecteer vervolgens de optie **SQL Server configuratie wijzigen** . U kunt de volgende configuraties van de sitedatabase wijzigen:

- De Windows-Server die als host fungeert voor de-data base.

- Het exemplaar van SQL Server dat wordt gebruikt op een server die de SQL Server-database host.

- De naam van de database.

- SQL Server poort wordt gebruikt door Configuration Manager.

- SQL Server Service Broker poort wordt gebruikt door Configuration Manager.

### <a name="move-the-site-database"></a>De site database verplaatsen

Als u de site database verplaatst, moet u ook de volgende configuraties bekijken:

- Wanneer u de site database naar een nieuwe computer verplaatst, voegt u het computer account van de site server toe aan de lokale groep **Administrators** op de computer waarop SQL Server wordt uitgevoerd. Als u een SQL Server cluster gebruikt voor de site database, voegt u het computer account toe aan de groep lokale **beheerders** van elke Windows Server-cluster knooppunt computer.

- Wanneer u de data base verplaatst naar een nieuw exemplaar op SQL Server, of naar een nieuwe SQL Server computer, schakelt u de integratie van Common Language Runtime (CLR) in. Gebruik **SQL Server Management Studio** om verbinding te maken met het exemplaar van SQL Server dat als host fungeert voor de site database. Voer vervolgens de volgende opgeslagen procedure uit als een query:`sp_configure 'clr enabled',1; reconfigure`

- Zorg ervoor dat de nieuwe SQL Server toegang tot de back-uplocatie heeft. Wanneer u een UNC gebruikt voor het opslaan van de back-up van uw site database, moet u nadat u de Data Base naar een nieuwe server hebt verplaatst, ervoor zorgen dat het computer account van de nieuwe SQL Server **Schrijf** machtigingen heeft voor de UNC-locatie. Deze configuratie omvat wanneer u overstapt naar een SQL Server AlwaysOn-beschikbaarheids groep of een SQL Server-cluster.

> [!IMPORTANT]
> Voordat u een Data Base verplaatst die een of meer database replica's voor beheer punten heeft, moet u eerst de database replica's verwijderen. Nadat u de database verplaatst hebt, kunt u databasereplica's opnieuw configureren. Zie [database replica's voor beheer punten](../deploy/configure/database-replicas-for-management-points.md)voor meer informatie.

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a>De SPN voor de site database server beheren

U kunt het account kiezen waarmee SQL-services voor de site database worden uitgevoerd:

- Wanneer de services worden uitgevoerd met het systeem account van de computer, registreert deze automatisch de Service Principal Name (SPN) voor u.

- Wanneer de services worden uitgevoerd met een domeingebonden gebruikers account, moet u de SPN hand matig registreren. Met de SPN kunnen SQL-clients en andere site systemen worden geverifieerd met Kerberos. Zonder Kerberos-verificatie, is het mogelijk dat de communicatie met de database mislukt.

Zie [een service principal name voor Kerberos-verbindingen registreren](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections)voor meer informatie over Spn's en Kerberos-verbindingen.

Registreer een SPN voor de SQL Server-service account van de site database server met behulp van het **Setspn** -hulp programma. Voer SETSPN als een domein beheerder uit op een computer in hetzelfde domein als de SQL Server.

De volgende procedures zijn voor beelden van het beheren van de SPN voor de SQL Server-service account. Zie [overzicht van Setspn](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\))voor meer informatie over Setspn.

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>Hand matig een SPN voor de domein gebruiker maken voor het SQL Server-service account

1. Open een opdrachtprompt als beheerder.

1. Voer een geldige opdracht in om de SPN te maken voor zowel de NetBIOS-naam als de FQDN:

    > [!IMPORTANT]
    > Wanneer u een SPN voor een geclusterde SQL Server maakt, geeft u de virtuele naam van het SQL Server cluster op als de SQL Server computer naam.

    - NetBIOS-naam:`setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        Bijvoorbeeld: `setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - QUALIFIED`setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        Bijvoorbeeld: `setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > De opdracht voor het registreren van een SPN voor een SQL Server benoemd exemplaar is hetzelfde als die u gebruikt wanneer u een SPN voor een standaard exemplaar registreert. De enige uitzonde ring hierop is dat het poort nummer moet overeenkomen met de poort die wordt gebruikt door het benoemde exemplaar.

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>Controleren of de SPN van de domein gebruiker correct is geregistreerd

1. Open een opdrachtprompt als beheerder.

1. Voer de volgende opdracht in:`setspn -L <domain\SQL service account>`

    Bijvoorbeeld: `setspn -L contoso\sqlservice`

1. Bekijk de geregistreerde **ServicePrincipalName**. Zorg ervoor dat u een geldige SPN hebt gemaakt voor de SQL Server.

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Wijzig de SQL Server-service account van het lokale systeem in een domein gebruikers account

1. Maak een gebruikersaccount van het domein of lokale systeem of selecteer deze account die u wilt gebruiken als de SQL Server-serviceaccount.

1. Open **SQL Server Configuration Manager**.

1. Selecteer **SQL Server services**en open vervolgens **SQL Server&lt;\>exemplaar naam**.

1. Ga naar het tabblad **Aanmelden** . Selecteer **dit account**en voer vervolgens de gebruikers naam en het wacht woord voor het domein gebruikers account uit stap 1 in.

1. Bevestig de wijziging van het service account en start de SQL Server-service opnieuw.

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a>Een site opnieuw instellen

Wanneer een site opnieuw wordt ingesteld op een CAS of primaire site, de site:

- Hiermee worden de standaard Configuration Manager bestands-en register machtigingen opnieuw toegepast

- Hiermee worden alle site onderdelen en alle site systeem rollen opnieuw geïnstalleerd

Secundaire sites bieden geen ondersteuning voor het opnieuw instellen van sites.

U kunt een site hand matig opnieuw instellen. Ze kunnen ook automatisch worden uitgevoerd nadat u de site configuratie hebt gewijzigd. Bijvoorbeeld:

- Als er een wijziging is aangebracht in de accounts die door Configuration Manager onderdelen worden gebruikt, kunt u een hand matige reset van de site overwegen. Met deze actie wordt gecontroleerd of de site onderdelen worden bijgewerkt om de nieuwe account gegevens te gebruiken.

- Als u de client-of server talen op een site wijzigt, wordt Configuration Manager automatisch opnieuw ingesteld op de site. De site moet opnieuw worden ingesteld voor het gebruik van de nieuwe talen.

> [!NOTE]
> Wanneer een site opnieuw wordt ingesteld, worden de toegangs machtigingen voor niet-Configuration Manager objecten niet opnieuw ingesteld.

### <a name="what-happens-during-a-site-reset"></a>Wat er gebeurt tijdens het opnieuw instellen van een site

Tijdens een sitereset:

1. Setup stopt en start de **SMS_SITE_COMPONENT_MANAGER** -service en de thread onderdelen van de **SMS_EXECUTIVE** -service.

1. Setup verwijdert en maakt de map site systeem share en het onderdeel **SMS Executive** op de lokale computer en op externe site systeem computers.

1. Setup start de **SMS_SITE_COMPONENT_MANAGER** -service opnieuw op, waarmee de **SMS_EXECUTIVE** en de **SMS_SQL_MONITOR** services worden geïnstalleerd.

Met site reset worden de volgende objecten hersteld:

- De **SMS**- of **NAL**-registersleutels, en enige standaard subsleutels onder deze sleutels.

- De mapstructuur van Configuration Manager bestanden en alle standaard bestanden of submappen in deze mapstructuur.

### <a name="prerequisites-for-site-reset"></a>Vereisten voor het opnieuw instellen van de site

Het account dat u gebruikt om een site opnieuw in te stellen, moet de volgende machtigingen hebben:

- De CA'S opnieuw instellen:

  - Een lokale **beheerder** op de CAS-server

  - Bevoegdheden die gelijk zijn aan de beveiligingsrol **volledige beheerder** op basis van rollen

- Een primaire site opnieuw instellen:

  - Een lokale **beheerder** op de primaire site server

  - Bevoegdheden die gelijk zijn aan de beveiligingsrol **volledige beheerder** op basis van rollen
  
  - Als de primaire site zich in een hiërarchie met een certificerings instantie bevindt, moet dit account ook een lokale **beheerder** zijn op de CAS-server.

### <a name="limitations-for-a-site-reset"></a>Beperkingen voor het opnieuw instellen van een site

Als de hiërarchie is geconfigureerd voor de ondersteuning [van client upgrades testen in een pre-productie verzameling](../../clients/manage/upgrade/test-client-upgrades.md), kunt u geen site reset gebruiken om de server-of client taal pakketten op sites te wijzigen.

### <a name="run-a-site-reset"></a>Een site resetten

1. Start Configuration Manager Setup op de site server met behulp van een van de volgende methoden:

    - Selecteer **Configuration Manager Setup**in het menu **Start** .

    - Open `\SMSSETUP\BIN\X64\setup.exe`in de map voor de Configuration Manager- *installatie media*. Zorg ervoor dat deze versie hetzelfde is als de site versie.

    - Open `\BIN\X64\setup.exe`in de map waar Configuration Manager is *geïnstalleerd*.

1. Selecteer op de pagina **aan de slag** de optie **site onderhoud uitvoeren of deze site opnieuw instellen**.

1. Selecteer op de pagina **site onderhoud** de optie **site opnieuw instellen zonder configuratie wijzigingen**.

1. Selecteer **Ja** om te beginnen met het opnieuw instellen van de site.

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a>Taal pakketten op een site beheren

Nadat een site is geïnstalleerd, kunt u de taal pakketten van de server en de client die in gebruik zijn, wijzigen.

### <a name="server-language-packs"></a>Taal pakketten voor Server

*Van toepassing op: Configuration Manager-console-installaties, nieuwe installaties van toepasselijke site systeem rollen*

Nadat u de taal pakketten voor de server op een site hebt bijgewerkt, kunt u ondersteuning voor de taal pakketten toevoegen aan Configuration Manager-consoles.

Als u ondersteuning voor een taal pakket voor de server wilt toevoegen aan een Configuration Manager-console, installeert u de Configuration Manager-console vanuit de map **ConsoleSetup** op een site server die het taal pakket bevat dat u wilt gebruiken. Als de Configuration Manager-console al is geïnstalleerd, moet u deze eerst verwijderen om de nieuwe installatie in te scha kelen om de huidige lijst met ondersteunde taal pakketten te identificeren.

### <a name="client-language-packs"></a>Taal pakketten voor client

Wijzigingen in de client taal pakketten worden de bron bestanden van de client installatie bijgewerkt. Nieuwe client installaties en upgrades voegen ondersteuning toe voor de bijgewerkte lijst met client talen.

Nadat u de client taal pakketten op een site hebt bijgewerkt, installeert u elke client die de taal pakketten gaat gebruiken met behulp van bron bestanden die de client taal pakketten bevatten.

Zie [taal pakketten](../deploy/install/language-packs.md)voor meer informatie over de client-en server talen die door Configuration Manager worden ondersteund.

### <a name="modify-the-supported-language-packs-at-a-site"></a>De ondersteunde taal pakketten op een site wijzigen

1. Start Configuration Manager Setup op de site server met behulp van een van de volgende methoden:

    - Selecteer **Configuration Manager Setup**in het menu **Start** .

    - Open `\SMSSETUP\BIN\X64\setup.exe`in de map voor de Configuration Manager- *installatie media*. Zorg ervoor dat deze versie hetzelfde is als de site versie.

    - Open `\BIN\X64\setup.exe`in de map waar Configuration Manager is *geïnstalleerd*.

1. Selecteer op de pagina **aan de slag** de optie **site onderhoud uitvoeren of deze site opnieuw instellen**.

1. Selecteer op de pagina **site onderhoud** de optie **taal configuratie wijzigen**.

1. Selecteer op de pagina **vereiste onderdelen downloaden** een van de volgende opties:

    - **Vereiste bestanden downloaden**: updates voor taal pakketten ophalen.

    - **Eerder gedownloade bestanden gebruiken**: eerder gedownloade bestanden gebruiken die de taal pakketten bevatten die u aan de site wilt toevoegen.

1. Selecteer op de pagina **selectie van server taal** de server talen die door deze site worden ondersteund.

1. Selecteer op de pagina **selectie van client taal** de client talen die door deze site worden ondersteund.

1. Voltooi de wizard om de taal ondersteuning op de site te wijzigen.

    > [!NOTE]
    > Configuration Manager initieert een site reset, waarbij ook alle site systeem rollen op de site opnieuw worden geïnstalleerd.

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a>De waarschuwings drempel van de database server wijzigen

Configuration Manager genereert standaard waarschuwingen wanneer de vrije schijf ruimte op een site database server laag is:

- Een waarschuwing genereren wanneer er 10 GB of minder vrije schijf ruimte beschikbaar is
- Een kritieke waarschuwing genereren wanneer er 5 GB of minder vrije schijf ruimte beschikbaar is

U kunt deze waarden wijzigen of waarschuwingen uitschakelen voor elke site:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .

1. Selecteer de site die u wilt configureren. Selecteer **Eigenschappen**in het lint.

1. Ga naar het tabblad **waarschuwing** en bewerk vervolgens de instellingen.

## <a name="uninstall-sites-and-hierarchies"></a>Sites en hiërarchieën verwijderen

Mogelijk moet u een Configuration Manager site systeemrol,-site of-hiërarchie verwijderen. Zie [rollen, sites en hiërarchieën verwijderen](../deploy/install/uninstall-sites-and-hierarchies.md)voor meer informatie.

Vanaf versie 2002 kunt u de certificerings instanties ook uit een hiërarchie verwijderen, maar de primaire site blijven gebruiken. Zie [de certificerings instanties verwijderen](../deploy/install/remove-central-administration-site.md)voor meer informatie.

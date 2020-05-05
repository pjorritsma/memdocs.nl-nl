---
title: Rapportage configureren
titleSuffix: Configuration Manager
description: Rapportage instellen in uw Configuration Manager-hiërarchie, met inbegrip van informatie over SQL Server Reporting Services.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ba67fee260867494302e49b7c9d3a97480e236b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723759"
---
# <a name="configure-reporting-in-configuration-manager"></a>Rapportage in Configuration Manager configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u rapporten kunt maken, wijzigen en uitvoeren in de Configuration Manager-console, moeten er verschillende configuratie taken worden uitgevoerd. Gebruik dit artikel voor informatie over het configureren van rapportage in uw Configuration Manager-hiërarchie.  

Voordat u SQL Server Reporting Services in uw hiërarchie installeert en configureert, raadpleegt u de volgende Configuration Manager Reporting-artikelen:  

- [Inleiding op rapportage](introduction-to-reporting.md)  

- [Rapportage plannen](planning-for-reporting.md)  

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services is een op een server gebaseerd rapportage platform dat uitgebreide rapportage functionaliteit biedt voor verschillende soorten gegevens bronnen. Het Reporting Services-punt in Configuration Manager communiceert met SQL Server Reporting Services tot:

- Configuration Manager-rapporten naar een opgegeven rapportmap kopiëren
- Reporting Services-instellingen configureren
- Beveiligings instellingen voor Reporting Services configureren

Wanneer u een rapport uitvoert, maakt het Reporting Services-onderdeel verbinding met de Configuration Manager-site database om gegevens op te halen.  

Voordat u het Reporting Services-punt op een Configuration Manager-site kunt installeren, moet u SQL Server Reporting Services op het doel site systeem installeren en configureren. Zie [Install SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services)(Engelstalig) voor meer informatie.  

### <a name="verify-sql-server-reporting-services-installation"></a>De SQL Server Reporting Services-installatie controleren

Gebruik de volgende procedure om te controleren of SQL Server Reporting Services is geïnstalleerd en normaal wordt uitgevoerd.

1. Ga naar het menu **Start** op het site systeem en open **Reporting Services Configuration Manager**. U kunt dit vinden in de sectie **Configuratiehulpprogramma's** van de **Microsoft SQL Server** groep.

2. Voer in het venster **Reporting Services-configuratie verbinding** de naam in van de server die als host fungeert voor SQL Server Reporting Services. Selecteer het exemplaar van SQL Server waarop u SQL Reporting Services hebt geïnstalleerd. Selecteer vervolgens **verbinding maken** om Reporting Services te openen Configuration Manager.  

3. Controleer op de pagina **rapport server status** of de **status van de rapport service** is **gestart**. Als dit niet het geval is, selecteert u **starten**.  

4. Selecteer op de pagina **webservice-URL** de URL in webservice- **Url's van Report Service**. Met deze actie wordt de verbinding met de rapportmap getest. Mogelijk wordt u door de browser gevraagd om referenties. Controleer of de webpagina is geopend.

5. Controleer op de pagina **Data Base** of de **rapport server modus** is ingesteld op **systeem eigen**.  

6. Selecteer op de pagina **Report Manager URL** de url in **Report Manager site-identificatie**. Met deze actie wordt de verbinding met de virtuele map voor Report Manager getest. Mogelijk wordt u door de browser gevraagd om referenties. Controleer of de webpagina is geopend.

    > [!NOTE]  
    > Reporting Services-Report Manager is niet vereist voor rapportage in Configuration Manager. U hebt deze alleen nodig als u rapporten wilt uitvoeren in de browser of rapporten wilt beheren met behulp van Report Manager.  

7. Selecteer **Afsluiten** om Reporting Services te sluiten Configuration Manager.  

## <a name="configure-reporting-to-use-report-builder-30"></a>Rapportage configureren voor gebruik van Report Builder 3,0

1. Open de REGI ster-editor van Windows op de computer waarop de Configuration Manager-console wordt uitgevoerd.  

2. Blader naar `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ConfigMgr10\AdminUI\Reporting`.

3. Open de **sleutel reportbuilderapplicationmanifestname** -sleutel om de waardegegevens te bewerken.  

4. Wijzig de waarde in `ReportBuilder_3_0_0_0.application`en selecteer **OK** om op te slaan.

5. Sluit de Register-editor van Windows.  

## <a name="install-a-reporting-services-point"></a>Een Reporting Services-punt installeren

Installeer het Reporting Services-punt om rapporten op de site te beheren. Het Reporting Services-punt:

- Hiermee worden rapport mappen en-rapporten naar SQL Server Reporting Services gekopieerd
- Hiermee wordt het beveiligings beleid voor de rapporten en mappen toegepast
- Stelt configuratie-instellingen in Reporting Services in

### <a name="requirements-and-limitations"></a>Vereisten en beperkingen

Voordat u rapporten kunt weer geven of beheren in de Configuration Manager-console, hebt u een Reporting Services-punt nodig. Deze site systeemrol configureren op een server met Microsoft SQL Server Reporting Services. Zie [vereisten voor rapportage](prerequisites-for-reporting.md)voor meer informatie.  

- Wanneer u een site selecteert voor het installeren van het Reporting Services-punt, moeten gebruikers die de rapporten openen zich in hetzelfde beveiligings bereik bevinden als de site waarop u de rol installeert.  

- Wijzig nadat u een Reporting Services-punt op een site systeem hebt geïnstalleerd niet de URL voor de rapport server.

    U maakt bijvoorbeeld het Reporting Services-punt. Vervolgens wijzigt u de URL voor de rapport server in Reporting Services Configuration Manager. De Configuration Manager-console blijft de oude URL gebruiken. U kunt geen rapporten uitvoeren, bewerken of maken vanuit de-console.

    Als u de URL van de rapport server moet wijzigen, verwijdert u eerst het bestaande Reporting Services-punt. Wijzig de URL en installeer het Reporting Services-punt opnieuw.  

- Wanneer u een Reporting Services-punt installeert, geeft u een account van het [Reporting Services-punt](../../plan-design/hierarchy/accounts.md#reporting-services-point-account)op. Voor gebruikers van een ander domein voor het uitvoeren van een rapport, maakt u een twee richtings vertrouwensrelatie tussen domeinen. Anders kan het rapport niet worden uitgevoerd.

### <a name="install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" />Het Reporting Services-punt op een site systeem installeren  

Zie [site systeem rollen installeren](../deploy/configure/install-site-system-roles.md)voor meer informatie over het configureren van site systemen.  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer vervolgens het knoop punt **servers en site systeem rollen** .  

1. Voeg het Reporting Services-punt toe aan een nieuwe of bestaande site systeem server:  

    - *Nieuw site systeem*: Selecteer op het tabblad **Start** van het lint in de groep **maken** de optie **site systeem server maken**. De **wizard Sitesysteemserver maken** wordt geopend.  

    - *Bestaand site systeem*: Selecteer de doel server. Selecteer op het tabblad **Start** van het lint in de **Server** groep de optie **site systeemrol toevoegen**. De **wizard site systeem rollen toevoegen** wordt geopend.  

1. Op de pagina **Algemeen** specificeert u de algemene instellingen voor de sitesysteemserver. Wanneer u het Reporting Services-punt aan een bestaande server toevoegt, controleert u de waarden die u eerder hebt geconfigureerd.  

1. Selecteer op de pagina **selectie van systeem rollen** **Reporting Services-punt** in de lijst met beschik bare rollen en selecteer vervolgens **volgende**.  

1. Configureer op de pagina **Reporting Services-punt** de volgende instellingen:  

    - **Naam site database server**: Geef de naam op van de server die als host fungeert voor de Configuration Manager-site database. De wizard haalt doorgaans de Fully Qualified Domain Name (FQDN) voor de server op. Als u een Data Base-exemplaar wilt opgeven &lt;, gebruikt u de indeling *Server naam*>\&lt; *exemplaar naam*>. Bijvoorbeeld `sqlserver\named1`.

    - **Database naam**: Geef de naam op van de Configuration Manager-site database. Selecteer **verifiëren** om te bevestigen dat de wizard toegang heeft tot de site database.  

        > [!IMPORTANT]  
        > Het gebruikers account dat u gebruikt om het Reporting Services-punt te maken, moet **Lees** toegang hebben tot de site database. Als de verbindingstest niet slaagt, wordt een rood waarschuwingspictogram weergegeven. De contextuele tekst van de aanwijzing op het pictogram bevat de details van de fout. Corrigeer de fout en selecteer vervolgens opnieuw **testen** .  

    - **Mapnaam**: Geef de naam op van de map die u wilt maken en gebruiken voor Configuration Manager rapporten in Reporting Services.  

    - **Reporting Services-server instantie**: Selecteer het exemplaar van SQL Server voor Reporting Services. Als op deze pagina geen exemplaren worden weer geven, controleert u of SQL Server Reporting Services is geïnstalleerd, geconfigureerd en gestart.  

        > [!IMPORTANT]  
        > Configuration Manager maakt een verbinding in de context van de huidige gebruiker naar WMI op het geselecteerde site systeem. Deze verbinding wordt gebruikt om het exemplaar van SQL Server voor Reporting Services op te halen. De huidige gebruiker moet **Lees** toegang hebben tot WMI op het site systeem, of de wizard kan de Reporting Services-instanties niet ophalen.  

    - **Account van Reporting Services-punt**: Selecteer **instellen**en selecteer vervolgens een account om te gebruiken. SQL Server Reporting Services op het Reporting Services-punt gebruikt dit account om verbinding te maken met de Configuration Manager-site database. Deze verbinding is om de gegevens voor een rapport op te halen. Selecteer **bestaand account** om een Windows-gebruikers account op te geven dat u eerder hebt geconfigureerd als een Configuration Manager-account. Selecteer **Nieuw account** om een Windows-gebruikers account op te geven dat momenteel niet is geconfigureerd voor gebruik. Configuration Manager verleent de opgegeven gebruiker automatisch toegang tot de site database.  

        Het account waarmee Reporting Services wordt uitgevoerd, moet behoren tot de lokale beveiligings groep van het domein **Windows-autorisatie toegangs groep**. Ook moet de machtiging voor het **lezen van tokenGroupsGlobalAndUniversal** zijn ingesteld op **toestaan**. Gebruikers in een ander domein dan het Reporting Services-punt account hebben een twee richtings vertrouwensrelatie nodig tussen de domeinen om rapporten uit te voeren.

        Het opgegeven Windows-gebruikersaccount en wachtwoord zijn versleuteld en opgeslagen in de Reporting Services-database. Reporting Services haalt de gegevens op voor rapporten van de sitedatabase met dit account en wachtwoord.  

        > [!IMPORTANT]  
        > Het account dat u opgeeft moet de machtiging **lokaal aanmelden** hebben op de server die als host fungeert voor de Reporting Services-Data Base.  

1. Voltooi de wizard.

Nadat de wizard is voltooid, maakt Configuration Manager de rapport mappen in Reporting Services. Vervolgens worden de rapporten gekopieerd naar de opgegeven rapport mappen.  

> [!TIP]  
> Als u alleen site systemen wilt weer geven die de siterol van het Reporting Services-punt hosten, klikt u met de rechter muisknop op **servers en site systeem rollen**en selecteert u **Reporting Services-punt**.  

### <a name="languages-for-reports"></a><a name="bkmk_languages" />Talen voor rapporten

<!-- SCCMDocs#1067 -->

Als Configuration Manager rapport mappen maakt en rapporten naar de rapport Server kopieert, wordt de juiste taal voor de objecten bepaald.

- Rapport mappen maken, rapporten kopiëren

  - Objecten maken met behulp van de land instelling van het besturings systeem van de site server

  - Als het specifieke taal pakket niet beschikbaar is, standaard ingesteld op Engels (Nederlands)

- Rapporten weer geven in een webbrowser

  - Map-en rapport namen: dezelfde land instelling als de site server
  
  - Inhoud van rapport: dynamisch op basis van de land instellingen van de browser

- Rapporten weer geven in de Configuration Manager-console

  - Namen van mappen en rapporten: dynamisch op basis van de land instellingen van de console
  
  - Inhoud van rapport: dynamisch op basis van de land instellingen van de console

Als u een Reporting Services-punt installeert op een site zonder taalpakketten, worden de rapporten in het Engels geïnstalleerd. Als u een taalpakket installeert nadat u het Reporting Services-punt hebt geïnstalleerd, moet u het Reporting Services-punt verwijderen en opnieuw installeren zodat de rapporten worden weergegeven in de juiste taal van het taalpakket.  

Zie [taal pakketten](../deploy/install/language-packs.md)voor meer informatie.

### <a name="file-installation-and-report-folder-security-rights"></a> Bestandsinstallatie en de beveiligingsrechten van rapportmappen

Configuration Manager voert de volgende acties uit om het Reporting Services-punt te installeren en Reporting Services te configureren:  

> [!IMPORTANT]  
> De site voert deze acties uit in de context van het account dat is geconfigureerd voor de SMS_Executive-service. Normaal gesp roken is dit account het lokale systeem account van de site server.  

- Installeer de siterol van het Reporting Services-punt.  

- Maak de gegevens bron in Reporting Services met de opgeslagen referenties die u in de wizard hebt opgegeven. Dit account is het Windows-gebruikers account en wacht woord dat Reporting Services gebruikt om verbinding te maken met de site database wanneer u rapporten uitvoert.  

- Maak de basismap van de Configuration Manager in Reporting Services.  

- Voeg de **Configuration Manager-rapport gebruikers** en beveiligings rollen van **ConfigMgr-rapport beheerders** toe in Reporting Services.  

- Maak submappen en implementeer vervolgens Configuration Manager rapporten van `%ProgramFiles%\SMS_SRSRP` op de site server naar Reporting Services.  

- Voeg de rol **ConfigMgr-rapport gebruikers** in Reporting Services toe aan de hoofd mappen voor alle gebruikers accounts in Configuration Manager waarvoor **site Lees** rechten gelden.  

- Voeg de rol **ConfigMgr-rapport beheerders** in Reporting Services toe aan de hoofd mappen voor alle gebruikers accounts in Configuration Manager die machtigingen voor het wijzigen van de **site** hebben.  

- De toewijzing tussen rapport mappen en Configuration Manager beveiligde object typen ophalen. Configuration Manager onderhoudt deze kaart in de site database.  

- Configureer de volgende machtigingen voor gebruikers met beheerders rechten in Configuration Manager voor specifieke rapport mappen in Reporting Services:  

  - Voeg gebruikers toe en wijs de rol **ConfigMgr-rapport gebruikers** toe aan de bijbehorende rapportmap voor gebruikers met beheerders rechten die **rapport** machtigingen hebben voor het Configuration Manager-object.  

  - Voeg gebruikers toe en wijs de rol **ConfigMgr-rapport beheerders** toe aan de bijbehorende rapportmap voor gebruikers met beheerders rechten die machtigingen voor het **wijzigen van rapporten** hebben voor het Configuration Manager-object.  

Configuration Manager maakt verbinding met Reporting Services en stelt de machtigingen voor gebruikers in op de Configuration Manager-en Reporting Services-hoofd mappen en specifieke rapport mappen. Na de eerste installatie van het Reporting Services-punt maakt Configuration Manager elke 10 minuten verbinding met Reporting Services om te controleren of de gebruikers rechten die op de rapport mappen zijn geconfigureerd, de gekoppelde rechten zijn die zijn ingesteld voor Configuration Manager gebruikers. Wanneer gebruikers worden toegevoegd of gebruikers rechten worden gewijzigd op de rapportmap met behulp van Reporting Services Report Manager, Configuration Manager deze wijzigingen overschrijft met behulp van de op rollen gebaseerde toewijzingen die zijn opgeslagen in de site database. Configuration Manager verwijdert ook gebruikers die geen rapportage rechten hebben in Configuration Manager.  

### <a name="reporting-services-security-roles"></a>Reporting Services-beveiligings rollen

Wanneer Configuration Manager het Reporting Services-punt installeert, worden de volgende beveiligings rollen toegevoegd in Reporting Services:  

- **ConfigMgr-rapport gebruikers**: gebruikers die zijn toegewezen aan deze beveiligingsrol, kunnen alleen Configuration Manager-rapporten uitvoeren.  

- **ConfigMgr-rapport beheerders**: gebruikers die zijn toegewezen aan deze beveiligingsrol, kunnen alle taken in verband met rapportage in Configuration Manager uitvoeren.  

## <a name="verify-installation"></a><a name="bkmk_verify"></a>Installatie controleren

Controleer de installatie van het Reporting Services-punt door te kijken naar specifieke status berichten en vermeldingen in logboek bestanden. Gebruik de volgende procedure om te controleren of de installatie van het Reporting Services-punt geslaagd is.  

> [!Note]  
> Als er rapporten worden weer gegeven in de submap **rapporten** van het knoop punt **rapportage** in de werk ruimte **bewaking** in de Configuration Manager-console, kunt u deze procedure overs Laan.

### <a name="verify-installation-by-status-message"></a>Installatie controleren op status bericht

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **systeem status**uit en selecteer het knoop punt **onderdeel status** .  

1. Selecteer het onderdeel **SMS_SRS_REPORTING_POINT** .  

1. Selecteer **berichten weer geven**op het tabblad **Start** van het lint in de groep **onderdeel** en kies **alle**.  

1. Geef een datum en tijd op voor een periode voordat u het Reporting Services-punt hebt geïnstalleerd en selecteer vervolgens **OK**.  

1. Controleer status bericht-ID **1015**. Dit status bericht geeft aan dat het Reporting Services-punt is geïnstalleerd.

### <a name="verify-installation-by-log-file"></a>Installatie controleren op logboek bestand

Open het bestand **Srsrp. log** , dat zich bevindt in de map **Logs** van het Configuration Manager installatiepad. Zoek naar de teken `Installation was successful`reeks.

Door lopen dit logboek bestand vanaf het tijdstip waarop het Reporting Services-punt is geïnstalleerd. Controleer of de rapportmappen gemaakt zijn, of de rapporten geïmplementeerd zijn en of het beveiligingsbeleid op elke map bevestigd is. Zoek na de laatste regel van beveiligings beleids bevestigingen naar de teken `Successfully checked that the SRS web service is healthy on server`reeks.  

## <a name="configure-a-certificate-to-author-reports"></a>Een certificaat voor het ontwerpen van rapporten configureren

Er zijn veel opties waarmee u rapporten in SQL Server Reporting Services kunt ontwerpen. Wanneer u rapporten in de Configuration Manager-console maakt of bewerkt, opent Configuration Manager Report Builder om te gebruiken als de ontwerp omgeving. Ongeacht de manier waarop u uw Configuration Manager-rapporten ontwerpt, hebt u een zelfondertekend certificaat voor Server verificatie nodig voor de site database server.

> [!NOTE]  
> Zie [Report Builder authoring Environment](https://docs.microsoft.com/sql/reporting-services/tools/report-builder-authoring-environment-ssrs)(Engelstalig) voor meer informatie over het ontwerpen van rapporten met SQL Server Reporting Services.  

Configuration Manager installeert automatisch het certificaat op de site server en eventuele SMS-provider rollen. U kunt rapporten maken of bewerken vanuit de Configuration Manager-console wanneer u deze uitvoert vanaf een van deze servers.

Wanneer u rapporten maakt of wijzigt vanuit een Configuration Manager-console op een andere computer, exporteert u het certificaat van de site server. De beschrijvende naam van het specifieke certificaat is de FQDN van de site server in het certificaat archief **vertrouwde personen** voor de lokale computer. Voeg dit certificaat toe aan het certificaat archief **vertrouwde personen** op de computer waarop de Configuration Manager-console wordt uitgevoerd.  

## <a name="modify-reporting-services-point-settings"></a>Instellingen van Reporting Services-punt wijzigen

Nadat u deze rol hebt geïnstalleerd, kunt u de site database verbinding en verificatie-instellingen wijzigen in de eigenschappen van het Reporting Services-punt.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer vervolgens het knoop punt **servers en site systeem rollen** .  

    > [!TIP]  
    > Als u alleen site systemen wilt weer geven die het Reporting Services-punt hosten, klikt u met de rechter muisknop op het knoop punt **servers en site systeem rollen** en selecteert u **Reporting Services-punt**.  

1. Selecteer het site systeem dat als host fungeert voor het Reporting Services-punt. Selecteer vervolgens de site systeem rollen van het **rapportage service punt** in het detail venster.

1. Klik op het tabblad **siterol** van het lint in de groep **Eigenschappen** op **Eigenschappen**.  

1. U kunt de volgende instellingen wijzigen in de **Eigenschappen van het Reporting Services-punt**:  

    - **Naam van site database server**

    - **Database naam**

    - **Gebruikers account**

1. Selecteer **OK** om de wijzigingen op te slaan en de eigenschappen te sluiten.  

Zie de beschrijvingen in de sectie voor [het installeren van het Reporting Services-punt op een site systeem](#bkmk_install)voor meer informatie over deze instellingen.

## <a name="power-bi-report-server"></a>Power BI Report Server

Vanaf versie 2002 kunt u de rapportage met Power BI Report Server integreren. Zie [integreren met Power bi Report Server](powerbi-report-server.md)voor meer informatie over het configureren ervan.

## <a name="upgrade-sql-server"></a>SQL Server bijwerken

Als u SQL Server en SQL Server Reporting Services wilt bijwerken, verwijdert u eerst het Reporting Services-punt van de site. Nadat u SQL Server hebt bijgewerkt, installeert u het Reporting Services-punt opnieuw in Configuration Manager.

Als u dit proces niet volgt, worden er fouten weer gegeven wanneer u rapporten uitvoert of bewerkt vanuit de Configuration Manager-console. U kunt rapporten blijven uitvoeren en bewerken vanuit een webbrowser.  

## <a name="configure-report-options"></a> Rapportopties configureren

U kunt het standaard Reporting Services-punt selecteren dat u gebruikt voor het beheren van rapporten. De site kan meer dan één Reporting Services-punt hebben, maar deze gebruikt alleen de standaard server voor het beheren van rapporten. Gebruik de volgende procedure om rapportopties voor uw site te configureren.  

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **rapportage**uit en selecteer vervolgens het knoop punt **rapporten** .  

1. Selecteer op het tabblad **Start** van het lint in de groep **instellingen** de optie **rapport opties**.  

1. Selecteer de standaard rapport server in de lijst en selecteer vervolgens **OK**.

Als er geen servers worden weer gegeven, controleert u of u een Reporting Services-punt op de site hebt geïnstalleerd en geconfigureerd. Zie [installatie controleren](#bkmk_verify)voor meer informatie.

Zorg ervoor dat op uw computer een versie van SQL Server Report Builder wordt uitgevoerd die overeenkomt met de versie van SQL Server die u voor de rapport server gebruikt. Anders wordt er een fout bericht weer gegeven, de standaard rapport server wordt niet opgeslagen en u kunt geen rapporten maken of bewerken.<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>Volgende stappen

[Bewerkingen en onderhoud voor rapportage](operations-and-maintenance-for-reporting.md)

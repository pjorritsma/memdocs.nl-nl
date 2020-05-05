---
title: Upgrade uitvoeren naar huidige vertakking
titleSuffix: Configuration Manager
description: Meer informatie over de stappen voor het uitvoeren van een geslaagde in-place upgrade van een site en hiërarchie waarop System Center 2012 Configuration Manager wordt uitgevoerd.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a2a803a62f2b42c3b62a09e710a3ca74110a4257
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717963"
---
# <a name="upgrade-to-configuration-manager-current-branch"></a>Upgrade uitvoeren naar Configuration Manager current branch

*Van toepassing op: Configuration Manager (huidige vertakking)*

Een in-place upgrade om de huidige vertakking te Configuration Manager van een site en hiërarchie die System Center 2012 Configuration Manager uitvoert. Voordat u een upgrade uitvoert van System Center 2012 Configuration Manager, moet u de sites voorbereiden. Deze voor bereiding vereist dat u specifieke configuraties verwijdert die een geslaagde upgrade kunnen voor komen. Volg vervolgens de upgrade volgorde wanneer er meer dan één site betrokken is.  

> [!TIP]  
> Bij het beheren van Configuration Manager site-en hiërarchie-infra structuur, worden de voor waarden *bijgewerkt*, *bijgewerkt*en *installeren* gebruikt om drie afzonderlijke concepten te beschrijven. Zie voor meer informatie over het gebruik van elke term [over upgrade, update en installatie](../../../understand/upgrade-update-install.md).

## <a name="in-place-upgrade-paths"></a><a name="bkmk_path"></a>In-place upgrade paden  

De volgende opties zijn de momenteel ondersteunde in-place upgrade paden:

### <a name="upgrade-to-version-2002"></a>Upgrade naar versie 2002

U kunt de volgende producten bijwerken naar een *volledig gelicentieerde* versie van Configuration Manager, huidige branch-versie 2002:

- Een *evaluatie* -installatie van Configuration Manager, huidige branch-versie 2002
- System Center 2012 Configuration Manager met Service Pack 1
- System Center 2012 Configuration Manager met Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager met Service Pack 1

Zie [Veelgestelde vragen over Configuration Manager branches en licenties](../../../understand/product-and-licensing-faq.md)voor meer informatie.

> [!TIP]  
> Wanneer u een upgrade uitvoert van een System Center 2012 Configuration Manager-versie naar de huidige vertakking, kunt u uw upgrade proces stroom lijnen. Raadpleeg de volgende artikelen voor meer informatie:  
>
> - [Basis lijn-en update versies](../../manage/updates.md#bkmk_Baselines)  
> - [De map CD.Latest](../../manage/the-cd.latest-folder.md)  

### <a name="unsupported-paths"></a>Niet-ondersteunde paden

De volgende paden worden niet ondersteund:

- Het is niet mogelijk om een upgrade van een Technical Preview-vertakking naar een volledig gelicentieerde installatie uit te kunnen werken. Een technische preview-versie kan alleen worden bijgewerkt naar een nieuwere versie van de Technical Preview.  

- Migratie van een Technical Preview naar een volledig gelicentieerde versie wordt niet ondersteund.  

## <a name="upgrade-checklists"></a><a name="bkmk_checklist"></a>Controle lijsten voor bijwerken  

De volgende controle lijsten kunnen u helpen een geslaagde upgrade naar Configuration Manager te plannen.  

### <a name="before-you-upgrade"></a>Voordat u een upgrade uitvoert  

Neem deze stappen door voordat u een upgrade uitvoert naar Configuration Manager.

#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>Uw System Center 2012 Configuration Manager-omgeving controleren

Los de problemen op die in het volgende Microsoft Ondersteuning artikel worden beschreven: [Configuration Manager-clients worden elke vijf uur opnieuw geïnstalleerd, omdat een terugkerende taak opnieuw wordt uitgevoerd en een onbedoelde client upgrade kan veroorzaken](https://support.microsoft.com/help/4018655).

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>Controleren of uw omgeving voldoet aan de ondersteunde configuraties

- Controleer de versie van het besturings systeem van de server in gebruik om site systeem rollen te hosten:  

  - Sommige oudere besturings systemen die worden ondersteund door System Center 2012 Configuration Manager worden niet ondersteund door Configuration Manager current branch. Voor de upgrade verwijdert u site systeem rollen voor die versies van het besturings systeem. Zie [ondersteunde besturings systemen voor site systeem servers](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)voor meer informatie.

  - De prerequisite Checker voor Configuration Manager controleert niet de vereisten voor site systeem rollen op de site server of op externe site systemen  

- Controleer de vereiste onderdelen voor elke computer die als host fungeert voor een site systeemrol. Als u bijvoorbeeld een besturings systeem wilt implementeren, maakt Configuration Manager gebruik van de Windows 10 Assessment and Deployment Kit (Windows ADK). Voordat u het installatieprogramma uitvoert, moet u Windows 10 ADK downloaden en installeren op de siteserver en op elke computer waarop een exemplaar van de SMS-provider wordt uitgevoerd.  

Zie [ondersteunde configuraties](../../../plan-design/configs/supported-configurations.md)voor meer informatie over ondersteunde platforms en vereiste configuraties.  

Zie [vereisten voor de infra structuur voor implementatie van het besturings systeem](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)voor meer informatie over het gebruik van Windows ADK met Configuration Manager.  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>Controleer de site-en hiërarchie status en controleer of er geen onopgeloste problemen zijn

Voordat u een site upgradet, moet u alle operationele problemen voor de siteserver, de sitedatabaseserver, en sitesysteemrollen die op externe computers zijn geïnstalleerd, oplossen. Een site-upgrade kan mislukken door bestaande operationele problemen.  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>Alle toepasselijke essentiële updates installeren voor besturings systemen op computers die de site, de site database server en externe site systeem rollen hosten

Vóór de upgrade van een site installeert u alle kritieke updates voor elk toepasselijk sitesysteem. Als u voor een te installeren update computers opnieuw moet opstarten, start de desbetreffende computers dan opnieuw op voordat u de upgrade van het service pack start.  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>De site systeem rollen verwijderen die niet worden ondersteund door Configuration Manager

De volgende site systeem rollen worden niet meer gebruikt in Configuration Manager. Verwijder deze voordat u een upgrade uitvoert van System Center 2012 Configuration Manager:  

- Buiten-bandbeheerpunt  

- Systeemstatuscontrolepunt  

- Application catalog-website punt en-webservicepunt

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Database replica's voor beheer punten op primaire sites uitschakelen

Configuration Manager kan geen primaire site upgraden die een database replica voor beheer punten heeft. Schakel databasereplicatie uit voordat u:  

- Een back-up van de sitedatabase maakt om de database-upgrade te testen  

- De productie site upgraden naar Configuration Manager huidige branch  

Raadpleeg voor meer informatie de volgende artikelen:  

- System Center 2012 Configuration Manager: [database replica's voor beheer punten configureren](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config)  

- Configuration Manager, current branch: [database replica's voor beheer punten](../configure/database-replicas-for-management-points.md)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>Software-update punten die gebruikmaken van NLB opnieuw configureren

Configuration Manager kan geen site upgraden die een NLB-cluster (Network Load Balancing) gebruikt om software-update punten te hosten.  

Als u NLB-clusters voor software-updatepunten gebruikt, gebruik dan PowerShell om de NLB-cluster te verwijderen. (Vanaf System Center 2012 Configuration Manager SP1, is er geen optie in de Configuration Manager-console om een NLB-cluster te configureren.)  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>Alle site-onderhouds taken op elke site uitschakelen gedurende de duur van de upgrade van die site

Voordat u een upgrade uitvoert naar Configuration Manager, schakelt u site-onderhouds taken uit die mogelijk worden uitgevoerd op het moment dat het upgrade proces actief is. Deze lijst bevat, maar is niet beperkt tot de volgende taken:  

- Back-upserver van site  
- Verouderde clientbewerkingen verwijderen  
- Verouderde detectiegegevens verwijderen  

Als een onderhouds taak van de site database wordt uitgevoerd tijdens het upgrade proces, kan de site-upgrade mislukken.  

Voordat u een taak uitschakelt, registreert u het schema van de taak zodat u de configuratie ervan kunt herstellen nadat de site-upgrade voltooid is.

Zie de volgende artikelen voor meer informatie over site-onderhouds taken:  

- System Center 2012 Configuration Manager: [planning voor site bewerkingen](../../../plan-design/hierarchy/plan-for-the-site-database.md)  

- Configuration Manager, current branch: [naslag voor onderhouds taken](../../manage/reference-for-maintenance-tasks.md)  

#### <a name="run-setup-prerequisite-checker"></a>Prerequisite Checker uitvoeren

Voordat u een site bijwerkt, moet u de **prerequisite Checker** onafhankelijk van Setup uitvoeren om te valideren dat uw site aan de vereisten voldoet. Wanneer u later de site bijwerkt, wordt prerequisite Checker opnieuw uitgevoerd.  

De onafhankelijke controle van vereisten evalueert de site voor de upgrade naar de huidige vertakking en de Long-term Servicing Branch (LTSB) van Configuration Manager. Omdat sommige functies niet worden ondersteund door de LTSB, ziet u mogelijk vermeldingen in het **bestand ConfigMgrPrereq. log** , zoals in de volgende voor beelden:

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Als u van plan bent om bij te werken naar de huidige vertakking, kunnen fouten voor de LTSB-editie veilig worden genegeerd. Ze zijn alleen van toepassing als u van plan bent om bij te werken naar de LTSB.

Wanneer u later Configuration Manager Setup uitvoert om de upgrade uit te voeren, wordt de controle van vereisten opnieuw uitgevoerd. Hiermee wordt uw site geëvalueerd op basis van de vertakking van Configuration Manager die u wilt installeren (current branch of LTSB). Als u ervoor kiest om een upgrade uit te voeren naar de huidige vertakking, wordt de controle niet uitgevoerd voor functies die niet worden ondersteund door de LTSB.

Zie voor meer informatie de [prerequisite Checker](prerequisite-checker.md) en [lijst met vereisten controles](list-of-prerequisite-checks.md).  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Vereiste bestanden en herdistribueerbare bestanden voor Configuration Manager downloaden

Gebruik het Download **programma** om de vereiste herdistribueerbare bestanden, taal pakketten en de meest recente product updates voor Configuration Manager te downloaden.  

Zie het [Download programma](setup-downloader.md)voor meer informatie.  

#### <a name="plan-to-manage-server-and-client-languages"></a>Beheer van server-en client talen plannen

Wanneer u een site bijwerkt, installeert de site-upgrade alleen de taalpakketversies die u tijdens de upgrade selecteert.  

- Setup controleert de huidige taal configuratie van uw site. Vervolgens worden de taal pakketten geïdentificeerd die beschikbaar zijn in de map waar u eerder gedownloade vereiste bestanden opslaat.  

- U kunt de selectie van de huidige server-en client taal pakketten bevestigen, of de selecties wijzigen om ondersteuning voor talen toe te voegen of te verwijderen.  

- U kunt alleen taal pakketten selecteren die beschikbaar zijn wanneer u het installatie programma uitvoert.  

> [!NOTE]  
> U kunt de taal pakketten van System Center 2012 Configuration Manager niet gebruiken om talen in te scha kelen voor een Configuration Manager huidige branch-site.  

Zie [taal pakketten](language-packs.md)voor meer informatie over taal pakketten.  

#### <a name="review-considerations-for-site-upgrades"></a>Aandachtspunten voor site-upgrades controleren

Wanneer u een site upgradet, worden bepaalde functies en configuraties opnieuw ingesteld op een standaardconfiguratie. Zie [overwegingen voor het uitvoeren van upgrades](#bkmk_considerations)voor informatie over het voorbereiden van deze en gerelateerde wijzigingen.  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>Maak een back-up van de site database op de centrale beheer site en primaire sites

Voordat u een site bijwerkt, maakt u een back-up van de site database om ervoor te zorgen dat u over een geslaagde back-up beschikt voor herstel na nood gevallen.  

Zie [back-up en herstel](../../manage/backup-and-recovery.md)voor meer informatie.  

#### <a name="back-up-a-customized-configurationmof-file"></a>Maak een back-up van een aangepast Configuration. MOF-bestand

Als u een aangepast configuratie. MOF-bestand gebruikt voor het definiëren van gegevens klassen die u gebruikt met hardware-inventaris, maakt u een back-up van dit bestand. Nadat de upgrade is uitgevoerd, herstelt u dit bestand naar uw site. Zie [Hardware-inventarisatie uitbreiden](../../../clients/manage/inventory/extend-hardware-inventory.md)voor meer informatie.  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>Het upgrade proces van de data base testen op een kopie van de meest recente back-up van de site database

Voordat u een centrale beheersite of primaire site van Configuration Manager bijwerkt, moet u het upgradeproces van de sitedatabase eerst testen op een kopie van de sitedatabase.  

- Test het upgrade proces van de site database. Wanneer u een site bijwerkt, kan de site database worden gewijzigd.  

- Hoewel het testen van de data base-upgrade niet vereist is, kunnen er problemen voor de upgrade worden geïdentificeerd voordat de productie database wordt beïnvloed  

- Een mislukte upgrade van de sitedatabase kan leiden tot een onbruikbare sitedatabase, waardoor u mogelijk een site recovery moet uitvoeren om de functionaliteit te herstellen  

- Hoewel de sitedatabase door verschillende sites in een hiërarchie wordt gedeeld, moet u de database op elke site testen voordat u die site bijwerkt.  

- Als u databasereplica's gebruikt voor beheerpunten op een primaire site, schakelt u replicatie uit voordat u de back-up van de sitedatabase maakt.  

Configuration Manager biedt geen ondersteuning voor back-ups van secundaire sites of de test upgrade van een secundaire site database.  

Het is niet mogelijk om een test database-upgrade uit te voeren op de data base van de productie site. Dit leidt tot een upgrade van de sitedatabase en kan tot gevolg hebben dat uw site onbruikbaar wordt.  

Zie [Test the site database upgrade](#bkmk_test)(Upgrade van de sitedatabase testen) voor meer informatie.  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>Start de site server en elke computer die als host fungeert voor een site systeemrol

Voer deze actie uit om ervoor te zorgen dat er geen acties in behandeling zijn van een recente installatie van updates of van vereisten.  

#### <a name="upgrade-sites"></a>Upgrade van sites uitvoeren

Start op de site op het hoogste niveau in de hiërarchie, voer Setup. exe uit vanaf de Configuration Manager-bron media.  

Nadat de site op het hoogste niveau is bijgewerkt, kunt u beginnen met de upgrade van elke onderliggende site. Voltooi de upgrade van elke site voordat u begint met het upgraden van de volgende site.  

Totdat alle sites in uw hiërarchie zijn bijgewerkt naar Configuration Manager, werkt uw hiërarchie in een gemengde-versie modus.  

Voor informatie over het uitvoeren van een upgrade, raadpleegt u [sites bijwerken](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Nadat u een upgrade hebt uitgevoerd  

Bekijk deze stappen nadat u een upgrade hebt uitgevoerd naar Configuration Manager.

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>Zelfstandige Configuration Manager-consoles upgraden

Wanneer u een centrale beheer site of primaire site bijwerkt, wordt de Configuration Manager-console die op de site server is geïnstalleerd, standaard bijgewerkt met de installatie. Voer hand matig een upgrade uit voor elke console die is geïnstalleerd op een andere computer dan de site server.  

> [!TIP]  
> Sluit alle geopende consoles voordat u de upgrade uitvoert.  

Zie [Configuration Manager-consoles installeren](install-consoles.md)voor meer informatie.  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>Database replica's voor beheer punten op primaire sites opnieuw configureren

Als u database replica's gebruikt voor beheer punten op primaire sites, moet u de database replica's verwijderen voordat u de site bijwerkt. Na de upgrade van een primaire site configureert u de databasereplica voor beheerpunten opnieuw.

Zie [database replica's voor beheer punten](../configure/database-replicas-for-management-points.md)voor meer informatie.  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>Alle onderhouds taken voor de data base die u voor de upgrade hebt uitgeschakeld, opnieuw configureren

Als u de Data Base- [onderhouds taken](../../manage/reference-for-maintenance-tasks.md) op een site vóór de upgrade hebt uitgeschakeld, moet u deze taken op de site opnieuw configureren met dezelfde instellingen die vóór de upgrade aanwezig waren.  

#### <a name="upgrade-clients"></a>Clients bijwerken

Nadat alle sites zijn bijgewerkt naar Configuration Manager, moet u de upgrade van clients plannen.  

Bij de upgrade van een client wordt de huidige clientsoftware verwijderd en wordt de nieuwe clientsoftwareversie geïnstalleerd. Als u clients wilt upgraden, kunt elke methode gebruiken die door Configuration Manager wordt ondersteund.  

> [!TIP]  
> Wanneer u de site op het hoogste niveau van een hiërarchie bijwerkt, wordt het clientinstallatiepakket op elk distributiepunt in de hiërarchie ook bijgewerkt. Wanneer u een primaire site bijwerkt, wordt het client upgrade pakket dat beschikbaar is van die primaire site, bijgewerkt.  

Zie [clients voor Windows-computers bijwerken voor](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)meer informatie.  

## <a name="considerations-for-upgrading"></a><a name="bkmk_considerations"></a>Overwegingen bij het upgraden  

### <a name="automatic-actions"></a>Automatische acties

Wanneer u een upgrade uitvoert naar Configuration Manager, worden de volgende acties automatisch uitgevoerd:  

- Een site wordt opnieuw ingesteld. Deze actie omvat een herinstallatie van alle site systeem rollen.  

- Als de site een site op het hoogste niveau van een hiërarchie is, wordt het clientinstallatiepakket op elk distributiepunt in de hiërarchie bijgewerkt. De site werkt ook de standaard opstart installatie kopieën bij om de nieuwe Windows PE-versie te gebruiken die is opgenomen in de Windows Assessment and Deployment Kit 10. Tijdens de upgrade worden bestaande media echter niet bijgewerkt voor gebruik met implementatie van de installatie kopie.  

- Als de site een primaire site is, wordt het clientupgradepakket voor die site bijgewerkt.  

### <a name="manual-actions-after-an-upgrade"></a>Hand matige acties na een upgrade

Nadat u een site hebt bijgewerkt, moet u de volgende acties uitvoeren:  

- Zorg ervoor dat clients die aan elke primaire site zijn toegewezen, de nieuwe client versie upgraden en installeren.  

- Een upgrade uitvoeren van elke Configuration Manager-console die verbinding maakt met de site en die wordt uitgevoerd op een computer die zich op afstand van de site server bevindt  

- Op primaire sites waar u databasereplica's voor beheerpunten gebruikt, configureert u de databasereplica's opnieuw.  

- Nadat de site is bijgewerkt, moet u hand matig fysieke media bijwerken zoals ISO-bestanden voor cd's, Dvd's of USB-flash stations. Het bevat ook voor bereide media die aan hardwareleveranciers zijn geleverd. Bij de upgrade van de site worden de standaard installatie kopieën bijgewerkt, maar kunnen deze media bestanden of apparaten die buiten worden gebruikt, niet worden bijgewerkt naar Configuration Manager.  

- Plan het bijwerken van aangepaste opstart installatie kopieën wanneer u de oudere versie van Windows PE niet nodig hebt.  

### <a name="actions-that-affect-configurations-and-settings"></a>Acties die van invloed zijn op configuraties en instellingen

Wanneer een site wordt bijgewerkt naar Configuration Manager, blijven bepaalde configuraties en instellingen na de upgrade niet behouden. Sommige configuraties worden ingesteld op een nieuwe standaard waarde. De volgende lijst bevat enkele instellingen die niet behouden blijven of die veranderen:  

- **Software Center**  
    De volgende Software Center-items worden opnieuw ingesteld op hun standaardwaarden:  

  - **Werk gegevens** worden opnieuw ingesteld op kantoor uren van **5: am** tot **10:13:00** maandag t/m vrijdag.  

  - De waarde voor **Computeronderhoud** wordt ingesteld op **Software Center-activiteiten onderbreken wanneer mijn computer zich in de presentatiemodus bevindt**.  

  - De waarde voor **Extern beheer** wordt ingesteld op de waarde in de clientinstellingen die aan de computer zijn toegewezen.  

- **Planningen overzicht software-updates**: aangepaste planningen voor samen vattingen voor software-updates of software-update groepen worden opnieuw ingesteld op de standaard waarde van 1 uur. Nadat de upgrade is voltooid, stelt u de aangepaste overzichtswaarden opnieuw in op de vereiste frequentie.  

## <a name="test-the-site-database-upgrade"></a><a name="bkmk_test"></a>De upgrade van de site database testen  

De volgende informatie is alleen van toepassing wanneer u een eerdere versie bijwerkt, zoals System Center 2012 Configuration Manager op Configuration Manager huidige branch.

Test voordat u een site bijwerkt een kopie van de data base van die site voor de upgrade.  

Als u de Data Base voor een upgrade wilt testen, herstelt u eerst een kopie van de site database naar een exemplaar van SQL Server dat geen Configuration Manager-site host. De versie van SQL Server die u gebruikt om de database kopie te hosten, moet een versie zijn van SQL Server die Configuration Manager ondersteunt.  

Nadat u de site database hebt hersteld, voert u op de SQL Server computer Configuration Manager Setup uit vanuit de map bron media voor Configuration Manager. Gebruik de `/TESTDBUPGRADE` opdracht regel optie.  

Raadpleeg voor meer informatie de volgende artikelen:

- [Een back-up maken van een Configuration Manager-site](../../manage/backup-and-recovery.md)  

- [Opdracht regel opties voor installatie](command-line-options-for-setup.md#bkmk_setup)  

- [Ondersteuning voor SQL Server-versies](../../../plan-design/configs/support-for-sql-server-versions.md)  

> [!TIP]  
> Als u Microsoft Intune integreert met Configuration Manager:  
>
> Wanneer u een testdatabase-upgrade uitvoert op en kopie van de sitedatabase die meer dan vijf dagen oud is, kunt u een van de volgende berichten ontvangen:  
>
> - WAARSCHUWING: de upgrade forceert een volledige synchronisatie naar de cloud.  
> - FOUT: de database-upgrade forceert een volledige synchronisatie naar de cloud.  
>
> Beide kunnen veilig worden genegeerd tijdens het testen van een Data Base-upgrade. Ze geven geen fout of probleem met de test upgrade aan. In plaats daarvan geven ze aan dat tijdens de daad werkelijke upgrade gegevens uit de replicatie groep van de **Cloud** database kunnen worden gesynchroniseerd met Microsoft intune.  

### <a name="test-a-site-database-for-upgrade"></a>Een site database testen voor een upgrade  

Gebruik de volgende procedure op elke centrale beheer site en de primaire site die u wilt upgraden:  

1. Maak een kopie van de site database. Herstel die kopie vervolgens naar een exemplaar van SQL Server dat dezelfde editie als uw site database gebruikt en die geen Configuration Manager-site host. Als de sitedatabase wordt uitgevoerd op een exemplaar van de Enterprise-editie van SQL Server, dient u de database dus te herstellen op een SQL Server-exemplaar waarop de Enterprise-editie van SQL Server wordt uitgevoerd.  

2. Nadat u de kopie van de Data Base hebt hersteld, voert u Setup uit vanaf de bron media voor Configuration Manager huidige vertakking. Wanneer u Setup uitvoert, gebruikt u `/TESTDBUPGRADE` de opdracht regel optie. Als het SQL Server-exemplaar dat de database kopie host niet het standaard exemplaar is, moet u ook de opdracht regel argumenten opgeven om het exemplaar te identificeren dat als host fungeert voor de kopie van de site database.  

    Stel dat u van plan bent om een sitedatabase met de databasenaam SMS_ABC bij te werken. U herstelt een kopie van deze sitedatabase naar een ondersteund exemplaar van SQL Server met de exemplaarnaam DBTest. Als u een upgrade van deze kopie van de site database wilt testen, gebruikt u de volgende opdracht regel:`Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Setup. exe bevindt zich op de volgende locatie op de Configuration Manager-bron media:`SMSSETUP\BIN\X64`  

3. Op het exemplaar van SQL Server waarop u de database-upgrade test, bevat ConfigMgrSetup.log in de hoofdmap van het systeemstation informatie over de voortgang van de bewerking:  

    - Als de test upgrade mislukt, lost u de problemen op die zijn gerelateerd aan de upgrade fout van de site database. Vervolgens maakt u een nieuwe back-up van de site database en test u de upgrade van de nieuwe kopie van de site database.  

    - Wanneer de upgrade lukt, kunt u de databasekopie verwijderen.  

        > [!NOTE]  
        > Het is niet mogelijk om de kopie van de site database te herstellen die u gebruikt voor de test upgrade voor gebruik als een site database op een wille keurige site.  

Nadat u een kopie van de site database hebt bijgewerkt, gaat u verder met de upgrade van de Configuration Manager-site en de site database.  

## <a name="upgrade-sites"></a><a name="bkmk_upgrade"></a>Upgrade van sites  

U bent klaar om uw Configuration Manager-site bij te werken nadat u de volgende taken hebt voltooid:

- Configuraties vóór de upgrade voor uw site
- De upgrade van de site database op een database kopie testen
- Down load vereiste bestanden en taal pakketten voor de versie die u wilt installeren

Wanneer u een site in een hiërarchie wilt bijwerken, moet u eerst de site op het hoogste niveau van de hiërarchie bijwerken. Deze site op het hoogste niveau is een centrale beheersite of een zelfstandige primaire site. Nadat u de upgrade van een centrale beheer site hebt voltooid, kunt u onderliggende primaire sites in elke gewenste volg orde bijwerken. Nadat u een primaire site hebt bijgewerkt, kunt u de onderliggende secundaire sites van die site upgraden of extra primaire sites upgraden voordat u secundaire sites bijwerkt.  

Als u een centrale beheer site of primaire site wilt bijwerken, voert u Setup uit vanaf de Configuration Manager-bron media. Voer Setup niet uit om secundaire sites bij te werken. In plaats daarvan gebruikt u de Configuration Manager-console om een secundaire site bij te werken nadat u de upgrade van de primaire bovenliggende site hebt voltooid.  

Voordat u een site bijwerkt, sluit u de Configuration Manager-console op de site server totdat de upgrade van de site is voltooid. Sluit ook elke Configuration Manager-console die wordt uitgevoerd op andere computers dan de site server. U kunt de console weer verbinden als de site is bijgewerkt. Totdat u echter een Configuration Manager-console naar de nieuwe versie van Configuration Manager bijwerkt, kan die console sommige objecten en informatie die beschikbaar zijn in de nieuwe versie van Configuration Manager niet weer geven.  

### <a name="upgrade-a-central-administration-site-or-primary-site"></a>Een centrale beheer site of primaire site bijwerken  

1. Controleer of de gebruiker die Setup uitvoert over de volgende beveiligingsrechten beschikt:  

    - Lokale **beheerders** rechten op de site server  

    - Als de site database server extern is van de site server, lokale **beheerders** rechten.  

2. Open het volgende programma op de site server: `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`. Met deze actie wordt de wizard Configuration Manager installatie geopend.  

3. Lees de informatie op de pagina **voordat u begint** en selecteer **volgende**.  

4. Selecteer op de pagina **aan de slag** de optie **deze Configuration Manager site bijwerken**en selecteer **volgende**.  

5. Op de pagina **product code** :  

    Als u Configuration Manager evaluatie eerder hebt geïnstalleerd, kunt u **de gelicentieerde versie van dit product installeren**selecteren. Voer vervolgens uw product code in voor de volledige installatie van Configuration Manager. Met deze actie wordt de site geconverteerd naar de volledige versie.  

    U kunt ook de **verval datum van de Software Assurance** van uw gebruiksrecht overeenkomst opgeven als een handige herinnering voor die datum. Als u deze waarde niet invoert tijdens de installatie, kunt u deze later opgeven in de Configuration Manager-console.  

    > [!NOTE]  
    > Micro soft valideert niet de verval datum die u hebt ingevoerd, en gebruikt deze datum niet voor validatie van licenties. U kunt deze gebruiken als herinnering voor uw verval datum. Configuration Manager regel matig controleren of nieuwe software-updates online worden aangeboden en dat de licentie status van uw Software Assurance actueel moet zijn om deze aanvullende updates te kunnen gebruiken.

    Zie [Licentiëring en vertakkingen](../../../understand/learn-more-editions.md)voor meer informatie.

6. Lees en accepteer de licentie voorwaarden op de pagina **licentie voorwaarden voor micro soft-software** en selecteer **volgende**.  

7. Lees en accepteer de licentie voorwaarden voor de vereiste software op de pagina **vereiste licenties** en selecteer **volgende**. Setup downloadt en installeert de software automatisch op site systemen of clients wanneer deze vereist is. Voordat u kunt door gaan met de volgende pagina, gaat u akkoord met alle voor waarden.  

8. Geef op de pagina **vereiste down loads** op of het installatie programma de nieuwste inhoud downloadt van Internet of eerder gedownloade bestanden gebruikt. Deze inhoud bevat de vereiste herdistribueerbare bestanden, taal pakketten en de meest recente product updates. Als u eerder de bestanden had gedownload met behulp van de Setup Downloader, selecteert u **Eerder gedownloade bestanden gebruiken** en specificeert u de downloadmap. Zie het [Download programma](setup-downloader.md)voor meer informatie.  

    > [!NOTE]  
    > Als u eerder gedownloade bestanden gebruikt, controleert u of het pad naar de downloadmap de recentste versie van de bestanden bevat.  

9. Bekijk op de pagina **Selectie van servertaal** welke talen momenteel zijn geïnstalleerd voor de site. Selecteer extra talen die op deze site beschikbaar zijn voor de Configuration Manager-console en voor rapporten. U kunt ook talen wissen die u niet meer wilt ondersteunen op deze site. Standaard is Engels geselecteerd en kan niet worden verwijderd.  

    > [!IMPORTANT]  
    > Elke versie van Configuration Manager kan geen taal pakketten van een eerdere versie van Configuration Manager gebruiken. Als u ondersteuning wilt inschakelen voor een taal op een Configuration Manager-site die u bijwerkt, moet u de versie van het taal pakket voor die nieuwe versie gebruiken. Als de huidige branch-versie van een taal pakket niet beschikbaar is in de vereiste bestanden die u hebt gedownload, kunt u tijdens de upgrade van System Center 2012 Configuration Manager naar Configuration Manager current branch geen ondersteuning voor die taal installeren.  

10. Bekijk op de pagina **Selectie van clienttaal** welke talen momenteel zijn geïnstalleerd voor de site. Selecteer extra talen die op deze site beschikbaar zijn voor clientcomputers. U kunt ook talen wissen die u niet meer wilt ondersteunen op deze site. Geef op of alle clienttalen moeten worden ingeschakeld voor clients voor mobiele apparaten en klik vervolgens op **Volgende**. Standaard is Engels geselecteerd en kan niet worden verwijderd.  

11. Controleer de configuratie op de pagina **samen vatting van instellingen** . Wanneer u klaar bent, selecteert u **volgende** om prerequisite Checker te starten om de gereedheid van de server voor de upgrade van de site te controleren.  

12. Als er geen problemen worden weer gegeven, selecteert u op de pagina **controle van vereisten voor installatie** de optie **volgende** om de site en de site systeem rollen bij te werken.

    Als prerequisite Checker een probleem vindt, selecteert u een item in de lijst voor meer informatie over het oplossen van het probleem. Alle items met de status **Fout** in de lijst moeten worden opgelost voordat u de installatie kunt voortzetten. Klik na het oplossen van het probleem op **Controle uitvoeren** om de controle van vereiste software opnieuw te starten. U kunt ook het bestand ConfigMgrPrereq.log openen in de systeemhoofdmap om de resultaten van Prerequisite Checker te controleren. Het logboek bestand kan aanvullende informatie bevatten die niet wordt weer gegeven in de gebruikers interface. Zie [prerequisite Checker](list-of-prerequisite-checks.md)voor een lijst met de vereiste regels en beschrijvingen voor de installatie.

Op de pagina **Upgrade uitvoeren** wordt de algehele voortgang weergegeven. Wanneer het installatieprogramma de installatie van de hoofdsiteserver en het sitesysteem voltooit, kunt u de wizard sluiten. Siteconfiguratie gaat door op de achtergrond.  

### <a name="upgrade-a-secondary-site"></a>Een secundaire site bijwerken  

1. Controleer of de gebruiker met beheerdersrechten die het installatieprogramma uitvoert beschikt over de volgende beveiligingsrechten:  

    - Lokale **beheerders** rechten op de secundaire site server  

    - De beveiligingsrol **infrastructuur beheerder** of **volledige beheerder** op de bovenliggende primaire site  

    - Systeembeheerders**SA**rechten voor de site database van de secundaire site  

2. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer vervolgens het knoop punt **sites** .  

3. Selecteer de secundaire site die u wilt bijwerken. Selecteer op het tabblad **Start** van het lint in de groep **site** de optie **upgrade**.  

4. Selecteer **Ja** om de beslissing te bevestigen en om de upgrade van de secundaire site te starten.  

De upgrade van de secundaire site wordt op de achtergrond uitgevoerd. Nadat de upgrade is voltooid, controleert u de status in de Configuration Manager-console. Selecteer de secundaire site server en selecteer op het tabblad **Start** van het lint in de **site** groep de optie **installatie status weer geven**.  

## <a name="post-upgrade-tasks"></a><a name="BKMK_PostUpgrade"></a>Taken na de upgrade  

Nadat u een site hebt bijgewerkt, moet u mogelijk aanvullende taken uitvoeren om de upgrade te volt ooien of de site opnieuw te configureren. Deze taken kunnen de volgende items bevatten:

- Configuration Manager-clients upgraden
- Configuration Manager-consoles bijwerken
- Database replica's voor beheer punten opnieuw inschakelen
- Instellingen herstellen voor Configuration Manager functionaliteit die u gebruikt en die niet behouden blijft na de upgrade  

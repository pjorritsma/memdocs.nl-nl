---
title: Controle lijst voor 2006
titleSuffix: Configuration Manager
description: Meer informatie over de acties die u moet uitvoeren voordat u bijwerkt naar Configuration Manager versie 2006.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6d359306-69ae-4873-ba90-964b6ae51d79
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7a3c66863e7768c5ca90151bf85d61aa1e3a0e17
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129643"
---
# <a name="checklist-for-installing-update-2006-for-configuration-manager"></a>Controle lijst voor het installeren van update 2006 voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u de huidige vertakking van Configuration Manager gebruikt, kunt u de update voor de console van versie 2006 installeren om uw hiërarchie van een vorige versie bij te werken. <!-- baseline only statement:Version 2006 is also available as [baseline media](updates.md#bkmk_Baselines), so you can use the installation media to install the first site of a new hierarchy.-->

Als u de update voor versie 2006 wilt downloaden, moet u een service verbindings punt gebruiken op de site op het hoogste niveau van uw hiërarchie. Deze site systeemrol kan zich in de online-of offline modus bevindt. [Gebruik het hulp programma voor service verbindingen](use-the-service-connection-tool.md)om de update te downloaden wanneer uw service verbindings punt offline is.<!-- SCCMDocs#1946 -->

Nadat uw hiërarchie het update pakket van micro soft heeft gedownload, kunt u het vinden in de-console. Selecteer in de werk ruimte **beheer** het knoop punt **updates en onderhoud** .

- Wanneer de update wordt weer gegeven als **beschikbaar**, is de update gereed voor installatie. Voordat u versie 2006 installeert, raadpleegt u de volgende informatie [over het installeren van update 2006](#about-installing-update-2006) en de [controle lijst](#checklist) voor configuraties die moeten worden gemaakt voordat de update wordt gestart.

- Als de update wordt weer gegeven als **downloaden** en niet wordt gewijzigd, raadpleegt u de **hman. log** en **dmpdownloader. log** op fouten.

  - In het dmpdownloader. log kan worden aangegeven dat het dmpdownloader-proces wacht op een interval voordat op updates wordt gecontroleerd. Als u het downloaden van de herdistributie bestanden van de update opnieuw wilt starten, start u de **SMS_Executive** -service opnieuw op de site server.

  - Een ander algemeen Download probleem treedt op wanneer de instellingen van de proxy server downloaden van `silverlight.dlservice.microsoft.com` , en niet verhinderen `download.microsoft.com` `go.microsoft.com` .

Zie [updates en onderhoud in de console](updates.md#bkmk_inconsole)voor meer informatie over het installeren van updates.

Zie [basis lijn-en update versies](updates.md#bkmk_Baselines)voor meer informatie over huidige branch-versies.

## <a name="about-installing-update-2006"></a>Over het installeren van update 2006

### <a name="sites"></a>Sites

Installeer update 2006 op de site op het hoogste niveau van uw hiërarchie. Start de installatie vanaf uw centrale beheer site (CAS) of vanaf uw zelfstandige primaire site. Nadat de update is geïnstalleerd op de site op het hoogste niveau, hebben onderliggende sites het volgende gedrag van de update:

- De update wordt automatisch geïnstalleerd op onderliggende primaire sites nadat de certificerings instantie de installatie van de update heeft voltooid. U kunt service Windows gebruiken om te bepalen wanneer een site de update installeert. Zie [service Windows for site servers](service-windows.md)(Engelstalig) voor meer informatie.

- Werk elke secundaire site hand matig bij vanuit de Configuration Manager-console nadat de primaire bovenliggende site de installatie van de update heeft voltooid. Het automatisch bijwerken van secundaire site servers wordt niet ondersteund.

### <a name="site-system-roles"></a>Sitesysteemrollen

Wanneer een site server de update installeert, worden automatisch alle site systeem rollen bijgewerkt. Deze rollen bevinden zich op de site server of zijn geïnstalleerd op externe servers. Voordat u de update installeert, moet u ervoor zorgen dat elke site systeem server voldoet aan de huidige vereisten voor de nieuwe update versie.

### <a name="configuration-manager-consoles"></a>Configuration Manager-consoles

De eerste keer dat u een Configuration Manager-console gebruikt nadat de update is voltooid, wordt u gevraagd die console bij te werken. U kunt ook de Configuration Manager Setup uitvoeren op de computer die als host fungeert voor de-console en de optie kiezen om de-console bij te werken. Installeer de update zo snel mogelijk naar de-console. Zie [de Configuration Manager-console installeren](../deploy/install/install-consoles.md)voor meer informatie.

> [!IMPORTANT]  
> Wanneer u een update installeert op de certificerings instantie, moet u rekening houden met de volgende beperkingen en vertragingen die bestaan totdat alle onderliggende primaire sites de update-installatie ook volt ooien:
>
> - **Client upgrades** worden niet gestart. Dit omvat automatische updates van clients en pre-productie clients. Daarnaast kunt u pas productie clients promo veren naar productie als de laatste site de installatie van de update heeft voltooid. Nadat de installatie van de update is voltooid op de laatste site, worden de client updates gestart op basis van uw configuratie keuzes.
> - **Nieuwe functies** die u met de update inschakelt, zijn niet beschikbaar. Dit gedrag is om te voor komen dat de certificerings instanties gegevens repliceren die zijn gerelateerd aan die functie naar een site die nog geen ondersteuning voor die functie heeft geïnstalleerd. Nadat alle primaire sites de update hebben geïnstalleerd, is de functie beschikbaar voor gebruik.
> - **Replicatie koppelingen** tussen de ca's en onderliggende primaire sites worden weer gegeven als niet-bijgewerkt. Deze status wordt weer gegeven in de update-installatie status *voltooid met waarschuwing* voor het controleren van de replicatie-initialisatie. In de werk ruimte **bewaking** van de-console wordt deze status weer gegeven als *koppeling wordt geconfigureerd*.

### <a name="early-update-ring"></a>Eerste update ring

<!-- SCCMDocs#1397 -->

<!-- As of May 11, 2020, version 2006 is globally available for all customers to install. If you previously opted in to the early update ring, watch for an update to this current branch version. -->

Op dit moment wordt versie 2006 uitgebracht voor de vroege update ring. Als u deze update wilt installeren, moet u zich aanmelden. Met het volgende Power shell-script wordt uw hiërarchie of zelfstandige primaire site toegevoegd aan de vroege update ring voor versie 2006:

[Script voor versie 2006 opt-in](https://go.microsoft.com/fwlink/?linkid=2099733) <!-- This fwlink points to the script package on the Download Center, don't change the link here! Make any changes to the fwlink target -->

Micro soft ondertekent het script digitaal en bundelt dit in een ondertekend zelfuitpakkend uitvoerbaar bestand.

> [!NOTE]
> Update versie 2006 is alleen van toepassing op sites waarop versie 1810 of hoger wordt uitgevoerd.

Om u aan te melden voor de eerste update ring:

1. Open Windows Power shell en **Voer als Administrator uit**
1. Voer het **EnableEarlyUpdateRing2006.ps1** script uit met de volgende syntaxis:

    `EnableEarlyUpdateRing2006.ps1 <SiteServer_Name> | SiteServer_IP>`

    Waar `SiteServer` verwijst naar de centrale beheer site of de zelfstandige primaire site server. Bijvoorbeeld: `EnableEarlyUpdateRing2006.ps1 cmprimary01`

1. Controleren op updates. Zie [beschik bare updates ophalen](install-in-console-updates.md#get-available-updates)voor meer informatie.

De update versie 2006 is nu beschikbaar in de-console.

> [!IMPORTANT]
> Met dit script wordt de site alleen toegevoegd aan de vroege update ring voor versie 2006. Het is geen permanente wijziging.

## <a name="checklist"></a>Controlelijst

### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>Alle sites voeren een ondersteunde versie van Configuration Manager

Op elke site server in de hiërarchie moet dezelfde versie van Configuration Manager worden uitgevoerd voordat u de installatie van update 2006 kunt starten. Als u wilt bijwerken naar 2006, moet u versie 1810 of hoger gebruiken.

### <a name="review-the-status-of-your-product-licensing"></a>Bekijk de status van uw product licenties

U moet over een actieve Software Assurance (SA)-overeenkomst of gelijkwaardige abonnements rechten beschikken om deze update te kunnen installeren. Wanneer u de site bijwerkt, biedt de pagina **licentie** de optie om de **verval datum van uw Software Assurance**te bevestigen.

Deze waarde is optioneel. U kunt opgeven als een handige herinnering voor de verval datum van uw licentie. Deze datum is zichtbaar wanneer u toekomstige updates installeert. Mogelijk hebt u deze waarde eerder opgegeven tijdens de installatie of installatie van een update. U kunt deze waarde ook opgeven in de Configuration Manager-console. Vouw **site configuratie**uit in de werk ruimte **beheer** en selecteer **sites**. Selecteer **hiërarchie-instellingen** in het lint en schakel over naar het tabblad **licenties** .

Zie [Licentiëring en vertakkingen](../../understand/learn-more-editions.md)voor meer informatie.

### <a name="review-microsoft-net-versions"></a>Microsoft .NET versies controleren

Wanneer een site deze update installeert en de minimale vereiste van .NET Framework 4,5 niet is geïnstalleerd Configuration Manager, wordt .NET Framework 4.5.2 automatisch geïnstalleerd. Wanneer deze vereiste nog niet is geïnstalleerd, installeert de site deze op elke server die als host fungeert voor een van de volgende site systeem rollen:

- Beheerpunt
- Serviceverbindingspunt
- Proxypunt voor inschrijving
- Inschrijvingspunt

Met deze installatie kan de site systeem server de status opnieuw opstarten in behandeling hebben en fouten melden aan de Configuration Manager onderdeel status viewer. Daarnaast kunnen de .NET-toepassingen op de server wille keurige fouten ondervinden totdat u de server opnieuw opstart.

Zie [site-en site systeem vereisten](../../plan-design/configs/site-and-site-system-prerequisites.md)voor meer informatie.

### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Controleer de versie van Windows ADK voor Windows 10

De versie van de Windows 10 Assessment and Deployment Kit (ADK) moet worden ondersteund voor Configuration Manager versie 2006. Zie [Windows 10 ADk](../../plan-design/configs/support-for-windows-10.md#windows-10-adk)voor meer informatie over ondersteunde versies van Windows ADk. Als u de Windows ADK wilt bijwerken, moet u dit doen voordat u begint met het bijwerken van Configuration Manager. Deze volg orde zorgt ervoor dat de standaard installatie kopieën automatisch worden bijgewerkt naar de meest recente versie van Windows PE. Aangepaste opstart installatie kopieën hand matig bijwerken na het bijwerken van de site.

Als u de site bijwerkt voordat u de Windows ADK bijwerkt, raadpleegt u [distributie punten bijwerken met de opstart installatie kopie](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

### <a name="review-sql-server-native-client-version"></a>SQL Server Native Client versie controleren

Installeer een minimale versie van SQL Server 2012 Native Client, die ondersteuning biedt voor TLS 1,2. Zie de [lijst met vereisten controles](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.

### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>De site-en hiërarchie status controleren op onopgeloste problemen

Het bijwerken van een site kan mislukken vanwege bestaande operationele problemen. Voordat u een site bijwerkt, moet u alle operationele problemen voor de volgende systemen oplossen:  

- De site server  
- De site database server  
- Externe site systeem rollen op andere servers

Zie [waarschuwingen en het status systeem gebruiken](use-alerts-and-the-status-system.md)voor meer informatie.

### <a name="review-file-and-data-replication-between-sites"></a>Bestands-en gegevens replicatie tussen sites controleren

Zorg ervoor dat bestands-en database replicatie tussen sites operationeel en actueel is. Vertragingen of achterstanden in een van beide kunnen een geslaagde update verhinderen.

#### <a name="database-replication"></a>Databasereplicatie

Voor [database replicatie](../../plan-design/hierarchy/database-replication.md)kunt u problemen oplossen voordat u de update start met behulp van de **Replication link Analyzer** (RLA). Zie [Data Base-replicatie bewaken](monitor-replication.md)voor meer informatie.

Gebruik RLA om de volgende vragen te beantwoorden:

- Is replicatie per groep in goede staat?
- Zijn er koppelingen gedegradeerd?
- Zijn er fouten opgetreden?

Als er een achterstand is, wacht u totdat deze is gewist. Als de achterstand groot is, zoals miljoenen records, heeft de koppeling een ongeldige status. Los het replicatie probleem op voordat u de site bijwerkt. Als u meer hulp nodig hebt, neemt u contact op met Microsoft Ondersteuning.<!-- 2838129 -->

#### <a name="file-based-replication"></a>Replicatie op basis van een bestand

Voor [replicatie op basis](../../plan-design/hierarchy/file-based-replication.md)van een bestand controleert u alle post vakken voor een achterstand op zowel verzendende als ontvangende sites. Als er veel vastgelopen of wachtende replicatie taken zijn, wacht u totdat ze zijn uitgeschakeld.<!-- SCCMDocs#1792 -->

- Controleer op de verzendende site de **afzender. log**.
- Controleer het logboek van de **wachtrij**op de ontvangende site.

### <a name="install-all-applicable-critical-windows-updates"></a>Alle toepasselijke essentiële Windows-updates installeren

Voordat u een update voor Configuration Manager installeert, moet u essentiële besturingssysteem updates voor elk toepasselijk site systeem installeren. Deze servers omvatten de site server, site database server en externe site systeem rollen. Als voor een update die u installeert, opnieuw moet worden opgestart, start u de desbetreffende servers opnieuw op voordat u de upgrade start.

### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Database replica's voor beheer punten op primaire sites uitschakelen

Configuration Manager kan een primaire site met een database replica voor beheer punten niet bijwerken. Schakel database replicatie uit voordat u een update voor Configuration Manager installeert.

Zie [database replica's voor beheer punten](../deploy/configure/database-replicas-for-management-points.md)voor meer informatie.

### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>SQL Server AlwaysOn-beschikbaarheids groepen instellen op hand matige failover

Als u een beschikbaarheids groep gebruikt, moet u ervoor zorgen dat de beschikbaarheids groep is ingesteld op hand matige failover voordat u de installatie van de update start. Nadat de site is bijgewerkt, kunt u de failover herstellen naar automatisch. Zie [SQL Server AlwaysOn voor een site database](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)voor meer informatie.

### <a name="disable-site-maintenance-tasks-at-each-site"></a>Site-onderhouds taken op elke site uitschakelen

Voordat u de update installeert, moet u de onderhouds taak van de site uitschakelen die kan worden uitgevoerd op het moment dat het update proces actief is. Bijvoorbeeld, maar niet beperkt tot:

- Back-upserver van site
- Verouderde clientbewerkingen verwijderen
- Verouderde detectiegegevens verwijderen

Wanneer een onderhoudstaak van de sitedatabase wordt uitgevoerd tijdens de installatie van updates, kan de installatie van de update mislukken. Voordat u een taak uitschakelt, registreert u het schema van de taak zodat u de configuratie ervan kunt herstellen nadat de update is geïnstalleerd.

Zie [onderhouds taken](maintenance-tasks.md)   en [naslag voor onderhouds taken](reference-for-maintenance-tasks.md)voor meer informatie.

### <a name="temporarily-stop-any-antivirus-software"></a>Antivirus software tijdelijk stoppen

Stop de antivirus software op de Configuration Manager-servers voordat u een site bijwerkt. De antivirus software kan sommige bestanden die moeten worden bijgewerkt, vergren delen, waardoor de update mislukt. <!--SMS.503481-->

### <a name="create-a-backup-of-the-site-database"></a>Maak een back-up van de site database

Maak een back-up van de site database op de CA'S en primaire sites voordat u een site bijwerkt. Met deze back-up wordt gecontroleerd of u een geslaagde back-up hebt voor herstel na nood gevallen.

Zie [back-up en herstel](backup-and-recovery.md)voor meer informatie.

### <a name="back-up-customized-files"></a>Maak een back-up van aangepaste bestanden

Als u of een product van derden een Configuration Manager configuratie bestanden bijpast, moet u een kopie van uw aanpassingen opslaan.

U kunt bijvoorbeeld aangepaste vermeldingen toevoegen aan het **osdinjection.xml** -bestand in de `bin\X64` map van uw Configuration Manager installatiemap. Na het bijwerken van Configuration Manager zijn deze aanpassingen niet behouden. U moet uw aanpassingen opnieuw Toep assen.

### <a name="plan-for-client-piloting"></a>Plannen voor client Piloting

Wanneer u een site-update installeert waarmee de client ook wordt bijgewerkt, test u die nieuwe client update in de pre-productie voordat u alle productie-clients bijwerkt. Als u deze optie wilt gebruiken, moet u uw site configureren voor ondersteuning van automatische upgrades voor pre-productie voordat u begint met de installatie van de update.

Zie [clients bijwerken](../../clients/manage/upgrade/upgrade-clients.md)   en [Client upgrades testen in een pre-productie verzameling](../../clients/manage/upgrade/test-client-upgrades.md)voor meer informatie.

### <a name="plan-to-use-service-windows"></a>Het gebruik van service vensters plannen

Als u een periode wilt definiëren waarin updates naar een site server kunnen worden geïnstalleerd, gebruikt u service Windows. Ze kunnen u helpen te bepalen wanneer sites in uw hiërarchie de update installeren. Zie [service Windows for site servers](service-windows.md)(Engelstalig) voor meer informatie.

### <a name="review-supported-extensions"></a>Ondersteunde uitbrei dingen controleren

<!--SCCMdocs#587-->
Als u Configuration Manager uitbreidt met andere producten van micro soft of micro soft-partners, controleert u of deze producten versie 2006 ondersteunen. Neem contact op met de leverancier van het product voor deze informatie. Zie de [release opmerkingen](../../../mdt/release-notes.md)voor de micro soft Deployment Toolkit voor meer informatie.

### <a name="remove-intune-subscription-hybrid-mdm"></a>InTune-abonnement verwijderen (hybride MDM)

<!-- SCCMDocs-pr#4253 -->
Het Hybrid MDM-service aanbod wordt vanaf 1 september 2019 buiten gebruik gesteld. Als uw Configuration Manager-site een Microsoft Intune-abonnement had, moet u het verwijderen. Zie [Hybrid MDM verwijderen](../../../mdm/understand/what-happened-to-hybrid.md#remove-hybrid-mdm)voor meer informatie.

### <a name="run-the-setup-prerequisite-checker"></a>De prerequisite Checker van Setup uitvoeren

Als de-console de update als **beschikbaar**bevat, kunt u de prerequisite Checker uitvoeren voordat u de update installeert. (Wanneer u de update op de site installeert, wordt prerequisite Checker opnieuw uitgevoerd.)

Als u een controle op vereisten wilt uitvoeren vanuit de-console, gaat u naar de werk ruimte **beheer** en selecteert u **updates en onderhoud**. Selecteer het update pakket voor **Configuration Manager 2006** en selecteer **controle van vereisten uitvoeren** op het lint.

Zie voor meer informatie de sectie de **prerequisite Checker uitvoeren voordat u een update installeert** in [voordat u een update in de console installeert](install-in-console-updates.md#bkmk_beforeinstall).

> [!IMPORTANT]  
> Wanneer de prerequisite checker wordt uitgevoerd, werkt het proces enkele product bron bestanden bij die worden gebruikt voor site-onderhouds taken. Na het uitvoeren van de prerequisite Checker, maar voordat u de update installeert, moet u, als u een onderhouds taak voor de site wilt uitvoeren, **Setupwpf.exe**   (Configuration Manager Setup) uitvoeren vanaf de cd. Meest recente map op de site server.

### <a name="update-sites"></a>Sites bijwerken

U bent nu klaar om de installatie van de update voor uw hiërarchie te starten. Zie [updates in de console installeren](install-in-console-updates.md#bkmk_install)voor meer informatie over het installeren van de update.

U kunt plannen dat de update wordt geïnstalleerd buiten de normale kantoor uren. Bepaal wanneer het proces het minste effect heeft op uw zakelijke activiteiten. Bij de installatie van de update en de bijbehorende acties worden site onderdelen en site systeem rollen opnieuw geïnstalleerd.

Zie [updates voor Configuration Manager](updates.md)voor meer informatie.

## <a name="post-update-checklist"></a>Controle lijst na de update

Nadat de site is bijgewerkt, gebruikt u de volgende controle lijst om algemene taken en configuraties uit te voeren.

### <a name="confirm-version-and-restart-if-necessary"></a>Versie bevestigen en opnieuw opstarten (indien nodig)

Zorg ervoor dat de site server en site systeemrol zijn bijgewerkt naar versie 2006. Voeg in de-console de kolom **versie** toe aan de knoop punten **sites** en **distributie punten** in de werk ruimte **beheer** . Als dat nodig is, installeert een site systeemrol automatisch opnieuw om bij te werken naar de nieuwe versie.

Overweeg om externe site systemen opnieuw te starten die op het eerste niet met succes zijn bijgewerkt. Controleer uw site-infra structuur en zorg ervoor dat toepasselijke site servers en externe site systeem servers opnieuw zijn opgestart. Site servers worden normaal gesp roken alleen opnieuw opgestart wanneer Configuration Manager .NET installeert als een vereiste voor een site systeemrol.

### <a name="confirm-site-to-site-replication-is-active"></a>Controleren of site-to-site-replicatie actief is

Ga in de Configuration Manager-console naar de volgende locaties om de status weer te geven en zorg ervoor dat de replicatie actief is:  

- **Bewakings** werkruimte, knoop punt **site hiërarchie**  

- **Bewakings** werkruimte, knoop punt voor **database replicatie**  

Raadpleeg voor meer informatie de volgende artikelen:  

- [Hiërarchie- en replicatie-infrastructuur bewaken](monitor-hierarchy.md)
- [Over de Replication Link Analyzer](monitor-replication.md#BKMK_RLA)  

### <a name="update-configuration-manager-consoles"></a>Configuration Manager-consoles bijwerken

Werk alle externe Configuration Manager-consoles bij naar dezelfde versie. U wordt gevraagd de console bij te werken wanneer:  

- U opent de-console.  

- U gaat naar een nieuw knoop punt in de-console.  

### <a name="reconfigure-database-replicas-for-management-points"></a>Database replica's voor beheer punten opnieuw configureren

Nadat u een primaire site hebt bijgewerkt, configureert u de database replica voor beheer punten die u hebt verwijderd voordat u de site hebt bijgewerkt. Zie [database replica's voor beheer punten](../deploy/configure/database-replicas-for-management-points.md)voor meer informatie.  

### <a name="reconfigure-sql-server-alwayson-availability-groups"></a>SQL Server AlwaysOn-beschikbaarheids groepen opnieuw configureren

Als u een beschikbaarheids groep gebruikt, stelt u de configuratie van de failover opnieuw in op automatisch. Zie [SQL Server AlwaysOn voor een site database](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)voor meer informatie.<!-- SCCMDocs #1366 -->

### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Uitgeschakelde onderhouds taken opnieuw configureren

Als u Data Base- [onderhouds taken](maintenance-tasks.md) op een site hebt uitgeschakeld voordat u de update installeert, moet u deze taken opnieuw configureren. Gebruik dezelfde instellingen die vóór de update aanwezig waren.  

### <a name="update-clients"></a>Clients bijwerken

Werk clients bij volgens het plan dat u hebt gemaakt, met name als u client Piloting hebt geconfigureerd voordat u de update installeert. Zie [clients voor Windows-computers bijwerken voor](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)meer informatie.  

### <a name="third-party-extensions"></a>Extensies van derden

Als u uitbrei dingen voor Configuration Manager gebruikt, moet u deze bijwerken naar de meest recente versie ter ondersteuning van Configuration Manager versie 2006.

### <a name="update-custom-boot-images-and-media"></a>Aangepaste opstart installatie kopieën en media bijwerken

<!--SCCMDocs issue 775-->

Gebruik de actie **distributie punten bijwerken** voor elke opstart installatie kopie die u gebruikt, of het nu een standaard-of aangepaste opstart installatie kopie is. Met deze actie zorgt u ervoor dat clients de nieuwste versie kunnen gebruiken. Zelfs als er geen nieuwe versie van Windows ADK is, kunnen de Configuration Manager-client onderdelen worden gewijzigd met een update. Als u geen opstart installatie kopieën en media bijwerkt, kunnen implementaties van taken reeksen mislukken op apparaten.

Wanneer u de site bijwerkt, Configuration Manager de *standaard* installatie kopieën automatisch bijgewerkt. De bijgewerkte inhoud wordt niet automatisch naar distributie punten gedistribueerd. Gebruik de actie **distributie punten bijwerken** op specifieke opstart installatie kopieën wanneer u klaar bent voor het distribueren van deze inhoud in uw netwerk.

Nadat u de site hebt bijgewerkt, werkt u de *aangepaste* opstart installatie kopieën hand matig bij. Met deze actie wordt de opstart installatie kopie zo nodig bijgewerkt met de nieuwste client onderdelen, eventueel opnieuw geladen met de huidige Windows PE-versie en de inhoud wordt opnieuw gedistribueerd naar de distributie punten.

Zie [distributie punten bijwerken met de opstart installatie kopie](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image)voor meer informatie.

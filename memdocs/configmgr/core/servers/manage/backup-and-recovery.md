---
title: Back-upsites
titleSuffix: Configuration Manager
description: Meer informatie over het maken van een back-up van uw sites vóór het mislukken of gegevens verlies in Configuration Manager.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8d766a172f934e27398ec2633ef0ec23ba4ade5e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700681"
---
# <a name="back-up-a-configuration-manager-site"></a>Back-up van een Configuration Manager-site

*Van toepassing op: Configuration Manager (huidige vertakking)*

Bereid methoden voor het maken van back-ups en herstel om gegevens verlies te voor komen. Voor Configuration Manager-sites kan een back-up-en herstel benadering u helpen om sneller sites en hiërarchieën te herstellen en met het minste gegevens verlies.  

De secties in dit artikel kunnen u helpen bij het maken van een back-up van uw sites. Zie [Recovery for Configuration Manager](recover-sites.md)als u een site wilt herstellen.  

<!--/SCCMdocs/issues/2108-->
>[!WARNING]
> De twee back-upmethoden die worden ondersteund voor Configuration Manager site Recovery zijn:
>
> - Een geslaagde back-up op de onderhouds taak van de **back-upserver**
> - Een hand matig herstelde back-up van de site database


## <a name="considerations-before-creating-a-backup"></a>Overwegingen voor het maken van een back-up  

-   Als u een SQL Server AlwaysOn-beschikbaarheids groep gebruikt om de site database te hosten: Wijzig uw back-up-en herstel plannen, zoals wordt beschreven in [voor bereiding voor het gebruik van SQL Server always on](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup).  

-   Configuration Manager kunt de site database herstellen vanaf de Configuration Manager back-uptaak. Het kan ook een back-up van de site database gebruiken die u met een ander proces maakt.   

     U kunt de site database bijvoorbeeld herstellen vanaf een back-up die is gemaakt als onderdeel van een onderhouds plan van Microsoft SQL Server. U kunt ook een back-up die is gemaakt met behulp van Data Protection Manager gebruiken om een back-up te maken van uw site database.  

-   Installeer vanaf versie 1806 een extra site server in de *passieve* modus. De site server in de passieve modus is naast uw bestaande site server in de *actieve* modus. Een site server in de passieve modus is beschikbaar voor onmiddellijk gebruik, indien nodig. Zie [hoge Beschik baarheid van site server](../deploy/configure/site-server-high-availability.md)voor meer informatie. Hoewel deze rol de nood zaak om back-up-en herstel bewerkingen te plannen niet heeft verwijderd, vermindert het de moeite om zo nodig een site te herstellen.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Data Protection Manager gebruiken om een back-up te maken van uw sitedatabase
U kunt System Center Data Protection Manager (DPM) gebruiken om een back-up te maken van uw Configuration Manager-site database.

Maak een nieuwe beveiligings groep in DPM voor de site database computer. Selecteer op de pagina **groeps leden selecteren** van de wizard nieuwe beveiligingsgroep maken de SMS Writer-service uit de lijst met gegevens bronnen. Selecteer vervolgens de site database als een geschikt lid. Zie de documentatie bibliotheek van [Data Protection Manager](/system-center/dpm) voor meer informatie over het gebruik van DPM.  

> [!IMPORTANT]  
>  Configuration Manager ondersteunt geen DPM-back-up voor een SQL Server cluster dat een benoemd exemplaar gebruikt. Het biedt ondersteuning voor DPM-back-up op een SQL Server-cluster dat gebruikmaakt van het standaard exemplaar van SQL Server.  

Nadat u de site database hebt hersteld, volgt u de stappen in Setup om de site te herstellen. Als u de site database waarvan u een back-up hebt gemaakt met Data Protection Manager wilt gebruiken, selecteert u de herstel optie om **een site database te gebruiken die hand matig is hersteld**.  



## <a name="backup-maintenance-task"></a>Back-uponderhoudstaak
U kunt back-up voor Configuration Manager-sites automatiseren door de vooraf gedefinieerde onderhouds taak van de back-upserver te plannen. Deze taak heeft de volgende functies:

-   Volgens een planning wordt uitgevoerd
-   Een back-up maakt van de sitedatabase
-   Een back-up maakt van specifieke registersleutels
-   Een back-up maakt van specifieke mappen en bestanden
-   Maakt een back-up van de [cd. Meest recente map](the-cd.latest-folder.md)   

Plan om de standaard back-uptaak voor de site mini maal elke vijf dagen uit te voeren. Dit schema is omdat Configuration Manager een Bewaar periode van vijf dagen gebruikt voor het *bijhouden van SQL Server wijzigingen* . Zie [SQL Server Bewaar periode](recover-sites.md#sql-server-change-tracking-retention-period)voor het bijhouden van wijzigingen voor meer informatie.

Als u het back-upproces wilt vereenvoudigen, kunt u een **AfterBackup.bat** bestand maken. Met dit script worden acties na de back-up automatisch uitgevoerd nadat de back-uptaak is voltooid. Gebruik het AfterBackup.bat-bestand om de moment opname van de back-up op een veilige locatie te archiveren. U kunt ook het AfterBackup.bat-bestand gebruiken om bestanden te kopiëren naar de map met back-ups of om andere back-uptaken te starten.  

U kunt een back-up maken van een centrale beheer site en primaire site. Secundaire sites of site systeem servers hebben geen back-uptaken.

Wanneer de Configuration Manager backup-service wordt uitgevoerd, worden de instructies gevolgd die zijn gedefinieerd in het back-upbesturingsbestand: `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl` . U kunt het back-upcontrolebestand aanpassen om het gedrag van de back-upservice te wijzigen.  
> [!NOTE]
> Wijzigingen van **Smsbkup. ctl** worden toegepast na het opnieuw opstarten van de service SMS_SITE_VSS_WRITER op de site server.

Informatie voor siteback-upstatus wordt geschreven naar het bestand **Smsbkup.log** . Dit bestand wordt gemaakt in de doelmap die u opgeeft in de eigenschappen van de onderhouds taak van de back-upserver van site.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>De onderhoudstaak van de back-upserver van site inschakelen  
1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2.  Selecteer de site waarvoor u de onderhouds taak voor site back-ups wilt inschakelen.  

3.  Klik op **site-onderhouds taken** op het lint.  

4.  Selecteer de taak **back-upserver van site** en klik op **bewerken**.  

5.  Selecteer de optie om **deze taak in te scha kelen**. Klik op **paden instellen** om de back-upbestemming op te geven. U hebt de volgende opties:  

    > [!IMPORTANT]  
    >  Sla ter voorkoming van knoeien met de back-upbestanden deze op een veilige locatie op. Het veiligste back-uppad is naar een lokaal station, zodat u NTFS-bestands machtigingen voor de map kunt instellen. Configuration Manager de back-upgegevens die zijn opgeslagen in het back-uppad, worden niet versleuteld.  

    -   **Lokaal station op site server voor site gegevens en-data base**: Hiermee geeft u op dat de taak de back-upbestanden voor de site en site database opslaat in het opgegeven pad op het lokale schijf station van de site server. Maak de lokale map voordat de back-uptaak wordt uitgevoerd. Het lokale systeem account op de site server moet **Schrijf** machtigingen hebben voor het NTFS-bestands beheer voor de lokale map voor de back-up van de site server. Het lokale systeem account op de computer waarop SQL Server worden uitgevoerd, moet **Schrijf** machtigingen hebben voor NTFS naar de map voor de back-up van de site database.  

    -   Netwerkpad **(UNC-naam) voor site gegevens en-data base**: Hiermee geeft u op dat de back-upbestanden voor de site en site database worden opgeslagen in het opgegeven netwerkpad. Maak de share voordat de back-uptaak wordt uitgevoerd. Het computer account van de site server moet **Schrijf** -NTFS-en share machtigingen hebben voor de gedeelde netwerkmap. Als SQL Server op een andere computer is geïnstalleerd, moet het computer account van de SQL Server dezelfde machtigingen hebben.  

    -   **Lokale stations op site server en SQL Server**: Hiermee geeft u op dat de taak de back-upbestanden voor de site opslaat in het opgegeven pad op het lokale station van de site server. De taak slaat de back-upbestanden voor de site database op in het opgegeven pad op het lokale station van de site database server. De lokale mappen maken voordat de back-uptaak wordt uitgevoerd. Het computeraccount van de siteserver moet **schrijf** machtigingen hebben voor NTFS naar de map die u maakt op de siteserver. Het computeraccount van de SQL Server moet **schrijf** machtigingen hebben voor NTFS naar de map die u maakt op de sitedatabaseserver. Deze optie is alleen beschikbaar wanneer de site database niet is geïnstalleerd op de site server.  

    > [!NOTE]  
    > De optie om naar het back-updoel te bladeren, is alleen beschikbaar wanneer u het netwerkpad opgeeft van de back-upbestemming.  
    >  
    > De mapnaam of share naam die wordt gebruikt voor de back-updoel, biedt geen ondersteuning voor het gebruik van Unicode-tekens.  

6.  Configureer een planning voor de back-uptaak van de site. Denk na over een back-upschema dat zich buiten actieve werk uren bevindt. Als u een hiërarchie hebt, overweeg dan een planning die ten minste twee keer per week wordt uitgevoerd. Als de site uitvalt, zorgt dit schema voor maximale gegevens retentie.  

    Wanneer u de Configuration Manager-console uitvoert op dezelfde site server die u configureert voor back-up, gebruikt de back-uptaak de lokale tijd voor de planning. Wanneer u de Configuration Manager-console uitvoert vanaf een andere computer, gebruikt de back-uptaak Coordinated Universal Time (UTC) voor het schema.  

7.  Kies of u een waarschuwing wilt maken als de back-uptaak van de site mislukt. Als deze functie is ingeschakeld, wordt door Configuration Manager een kritieke waarschuwing voor de back-upfout gemaakt. U kunt deze waarschuwingen bekijken in het knoop punt **waarschuwingen** van de werk ruimte **bewaking** .  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Controleer of de onderhouds taak van de back-upserver van site wordt uitgevoerd  

-   Controleer de tijds tempel op de bestanden in de doelmap van de back-up die de taak heeft gemaakt. Controleer of de tijds tempel is bijgewerkt naar het tijdstip waarop de taak voor het laatst is ingepland om te worden uitgevoerd.  

-   Ga naar het knoop punt **onderdeel status** van de werk ruimte **bewaking** . Controleer de status berichten voor **SMS_SITE_BACKUP**. Wanneer site back-up is voltooid, ziet u bericht-ID **5035**. Dit bericht geeft aan dat de back-up van de site zonder fouten is voltooid.  

-   Wanneer u de back-uptaak configureert om een waarschuwing te maken wanneer deze mislukt, zoekt u naar back-upfouten in het knoop punt **waarschuwingen** van de werk ruimte **bewaking** .  

-   Open Windows Verkenner op de site server en blader naar `<ConfigMgrInstallationFolder>\Logs` . Controleer **Smsbkup. log** op waarschuwingen en fouten. Wanneer site back-up is voltooid, wordt het logboek weer gegeven `Backup completed` met de bericht-id `STATMSG: ID=5035` .  

    > [!TIP]  
    >  Wanneer de onderhouds taak van de back-up mislukt, start u de back-uptaak opnieuw door de **SMS_SITE_BACKUP** Windows-service te stoppen en opnieuw te starten.  



## <a name="archive-the-backup-snapshot"></a>De moment opname van de back-up archiveren  
De back-uptaak maakt de moment opname van de back-up de eerste keer dat deze wordt uitgevoerd. U kunt deze moment opname gebruiken om uw site server te herstellen als deze mislukt. Wanneer de back-uptaak opnieuw op schema wordt uitgevoerd, wordt er een nieuwe back-upmomentopname gemaakt waarmee de vorige moment opname wordt overschreven. Als gevolg hiervan heeft de site slechts één moment opname van back-ups en u hebt geen manier om een eerdere moment opname van de back-up op te halen.  

Bewaar meerdere archieven van de back-upmomentopname om de volgende redenen:  

-   Het is gebruikelijk dat back-upmedia mislukken, vastlopen of alleen een gedeeltelijke back-up bevatten. Een mislukte zelfstandige primaire site op basis van een oudere back-up herstellen is beter dan deze zonder back-up te herstellen. Voor een site server in een hiërarchie moet de back-up zich in de SQL Server Bewaar periode voor het bijhouden van wijzigingen bevindt, of de back-up is niet vereist.  

-   Een beschadiging in de site kan gedurende verschillende back-upcycli ongedetecteerd blijven. Mogelijk moet u een moment opname van de back-up gebruiken voordat de site was beschadigd. Deze reden is van toepassing op een zelfstandige primaire site en op sites in een hiërarchie waar de back-up zich bevindt in de SQL Server Bewaar periode voor het bijhouden van wijzigingen.  

-   De site heeft mogelijk helemaal geen back-upmomentopname. Bijvoorbeeld, als de onderhouds taak van de back-upserver van site mislukt. Omdat de back-uptaak de vorige back-upmomentopname verwijdert voordat het een back-up begint te maken van de huidige gegevens, is er geen geldige back-upmomentopname.  



## <a name="using-the-afterbackupbat-file"></a>Het bestand AfterBackup.bat gebruiken  
Nadat er een back-up van de site is gemaakt, probeert de back-uptaak automatisch een script uit te voeren met de naam **AfterBackup.bat**. Maak het AfterBackup.bat-bestand hand matig op de site server in `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box` . Als er een AfterBackup.bat bestand in de juiste map bestaat, wordt dit automatisch uitgevoerd nadat de back-uptaak is voltooid.

Met het AfterBackup.bat bestand kunt u de moment opname van de back-up archiveren aan het einde van elke back-upbewerking. Er kunnen automatisch andere taken na back-ups worden uitgevoerd die geen deel uitmaken van de onderhouds taak van de back-upserver van site. Het AfterBackup.bat-bestand integreert het archief en de back-upbewerkingen, waardoor elke nieuwe back-upmomentopname wordt gearchiveerd.

Als het AfterBackup.bat bestand niet aanwezig is, slaat de back-uptaak het over zonder dat dit van invloed is op de back-upbewerking. Als u wilt controleren of de back-uptaak dit script heeft uitgevoerd, gaat u naar het knoop punt **onderdeel status** in de werk ruimte **bewaking** en bekijkt u de status berichten voor **SMS_SITE_BACKUP**. Wanneer de taak het AfterBackup.bat-opdracht bestand heeft gestart, ziet u bericht-ID **5040**.  

> [!TIP]  
>  Als u de back-upbestanden van de site server met AfterBackup.bat wilt archiveren, moet u een Kopieer opdracht gebruiken in het batch-bestand. Een dergelijk hulp programma is [Robocopy](/windows-server/administration/windows-commands/robocopy) in Windows Server. Maak bijvoorbeeld het AfterBackup.bat bestand met de volgende opdracht: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

Hoewel het beoogde gebruik van de AfterBackup.bat het archiveren van back-upmomentopnamen is, kunt u een AfterBackup.bat bestand maken om extra taken aan het einde van elke back-upbewerking uit te voeren.  



##  <a name="supplemental-backup-tasks"></a>Aanvullende back-uptaken  
De onderhouds taak back-upserver van site biedt een back-upmomentopname voor de site server bestanden en de site database. Er zijn andere items waarvan geen back-up is gemaakt, die u moet overwegen wanneer u uw back-upstrategie maakt. Gebruik deze secties om u te helpen bij het volt ooien van uw Configuration Manager-back-upstrategie.  

### <a name="back-up-custom-reports"></a>Back-ups maken van aangepaste rapporten   
Als u in SQL Server Reporting Services vooraf gedefinieerde of gemaakte aangepaste rapporten wijzigt, maakt u een back-up voor de database bestanden van de rapport server. De back-up van de rapport server moet de volgende onderdelen bevatten:
- De bron bestanden voor rapporten en modellen
- Versleutelingssleutels
- Aangepaste assembly's of extensies
- Configuratie bestanden
- Aangepaste SQL Server weer gaven die in aangepaste rapporten worden gebruikt
- Aangepaste opgeslagen procedures  

> [!IMPORTANT]  
>  Wanneer Configuration Manager bijgewerkt naar een nieuwere versie, worden de vooraf gedefinieerde rapporten mogelijk overschreven door nieuwe rapporten. Als u een vooraf gedefinieerd rapport wijzigt, zorg er dan voor dat u een back-up maakt van het rapport en dit vervolgens herstelt in Reporting Services.  

Zie [back-up-en herstel bewerkingen voor Reporting Services](/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services)voor meer informatie over het maken van een back-up van uw aangepaste rapporten in Reporting Services.  

### <a name="back-up-content-files"></a>Back-up maken van inhouds bestanden  
De inhouds bibliotheek in Configuration Manager is de locatie waar alle inhouds bestanden worden opgeslagen voor alle software-implementaties. De inhouds bibliotheek bevindt zich op de site server en op elk distributie punt. De onderhouds taak van de back-upserver van de site maakt geen back-up van de inhouds bibliotheek of pakket bron bestanden. Wanneer een site server uitvalt, wordt de informatie over de inhouds bibliotheek teruggezet naar de site database, maar moet u de inhouds bibliotheek en pakket bron bestanden herstellen.  

-   De inhouds bibliotheek moet worden hersteld voordat u inhoud opnieuw kunt distribueren naar distributie punten. Wanneer u de herdistributie van inhoud start, Configuration Manager kopieert de bestanden uit de inhouds bibliotheek van de site server naar de distributie punten. Zie [de inhouds bibliotheek](../../plan-design/hierarchy/the-content-library.md)voor meer informatie.  

-   De bron bestanden van het pakket moeten worden hersteld voordat u inhoud op distributie punten kunt bijwerken. Wanneer u een update van de inhoud start, kopieert Configuration Manager nieuwe of gewijzigde bestanden van de pakket bron naar de inhouds bibliotheek. Vervolgens worden de bestanden gekopieerd naar de gekoppelde distributie punten. Voer de volgende SQL Server query uit op de site database om de bron locatie van het pakket voor alle pakketten en toepassingen te vinden: `SELECT * FROM v_Package` . U kunt de locatie van de pakketbron vinden door de eerste drie tekens van de pakket-id te bekijken. Als de pakket-id bijvoorbeeld CEN00001 is, is de sitecode van de bronsite CEN. Wanneer u de pakket bron bestanden herstelt, moeten deze worden hersteld naar dezelfde locatie waar deze zich vóór de fout bevonden.  

Controleer of u zowel de inhouds bibliotheek als pakket bron bestanden in de back-up van het bestands systeem voor de site server opneemt.  

### <a name="back-up-custom-software-updates"></a>Back-up maken van aangepaste software-updates  
System Center Updates Publisher is een zelfstandig hulp programma waarmee u aangepaste software-updates kunt beheren. Updates Publisher gebruikt een lokale Data Base voor de software-update opslagplaats. Wanneer u updates Publisher gebruikt voor het beheren van aangepaste software-updates, bepaalt u of u de updates Publisher-data base in uw back-upplan moet bevatten. Zie [System Center updates Publisher](../../../sum/tools/updates-publisher.md)voor meer informatie.  

Gebruik de volgende procedure om een back-up te maken van de update Publisher-data base.  

#### <a name="back-up-the-updates-publisher-database"></a>Back-up maken van de updates Publisher-data base  

1.  Op de computer waarop updates Publisher wordt uitgevoerd, bladert u naar de updates Publisher-database bestand **Scupdb. sdf** in `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` . Er is een ander database bestand voor elke gebruiker die updates Publisher uitvoert.  

2.  Kopieer het databasebestand naar uw back-upbestemming. Als uw back-upbestemming bijvoorbeeld is `E:\ConfigMgr_Backup` , kunt u de updates Publisher-database bestand naar kopiëren `E:\ConfigMgr_Backup\SCUP` .  

    > [!TIP]  
    >  Wanneer er meer dan één database bestand op een computer staat, overweeg dan het bestand in een submap op te slaan die het gebruikers profiel aangeeft dat aan het database bestand is gekoppeld. U kunt bijvoorbeeld één database bestand hebben in `E:\ConfigMgr_Backup\SCUP\User1` en een ander database bestand in `E:\ConfigMgr_Backup\SCUP\User2` .  



## <a name="user-state-migration-data"></a>Migratiegegevens van de gebruikersstatus  
U kunt Configuration Manager taken reeksen gebruiken om de gebruikers status gegevens vast te leggen en te herstellen in implementatie scenario's voor besturings systemen. De eigenschappen van het status migratie punt vermelden de mappen waarin de gebruikers status gegevens worden opgeslagen. Voor deze gegevens wordt geen back-up gemaakt als onderdeel van de onderhouds taak voor back-up van site server. Als deel van uw back-upplan moet u handmatig een back-up maken van de mappen die u specificeert om de migratiegegevens van de gebruikersstatus op te slaan.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>De mappen bepalen die worden gebruikt om de migratie gegevens van de gebruikers status op te slaan  

1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **servers en site systeem rollen** .  

2.  Selecteer het site systeem dat als host fungeert voor de rol van de status migratie. Selecteer vervolgens **status migratie punt** in het deel venster **site systeem rollen** .  

3.  Klik op **Eigenschappen** in het lint.  

4.  De mappen waar de migratiegegevens van de gebruikersstatus worden opgeslagen, staan in de sectie **Mapdetails** op het tabblad **Algemeen** .  



## <a name="about-the-sms-writer-service"></a>Over de SMS Writer-Service  
De SMS Writer is een service die communiceert met de Windows-Volume Shadow Copy Service (VSS) tijdens het back-upproces. De SMS Writer-service moet worden uitgevoerd om een back-up te kunnen maken van de Configuration Manager-site.  

### <a name="process"></a>Proces  
1. SMS Writer registreert bij de VSS-service en wordt gekoppeld aan de betreffende interfaces en gebeurtenissen. 
2. Wanneer VSS gebeurtenissen uitzendt, of specifieke berichten naar de SMS Writer verstuurt, reageert de SMS Writer op het bericht en neemt de nodige actie. 
3. De SMS Writer leest het back-upcontrolebestand **smsbkup. ctl** in en `<ConfigMgrInstallationPath>\inboxes\smsbkup.box` bepaalt de bestanden en gegevens waarvan een back-up moet worden gemaakt. 
4. De SMS Writer bouwt meta gegevens op, die bestaan uit verschillende onderdelen, waaronder specifieke gegevens van de SMS-register sleutel en subsleutels. 
    a. De meta gegevens worden verzonden naar VSS wanneer deze wordt aangevraagd. 
    b. VSS verzendt de meta gegevens vervolgens naar de aanvragende toepassing, de Configuration Manager back-upbeheer. 
5. Backup Manager selecteert de gegevens waarvan een back-up moet worden gemaakt en verzendt deze gegevens naar de SMS Writer via VSS. 
6. De SMS Writer neemt de nodige stappen om de back-up voor te bereiden. 
7. Later, wanneer VSS klaar is om de moment opname te maken: a. Er wordt een gebeurtenis b verzonden. De SMS Writer stopt alle Configuration Manager services c. Het zorgt ervoor dat de Configuration Manager activiteiten worden bevroren terwijl de moment opname wordt gemaakt. 
8. Na voltooiing van de momentopname start de SMS Writer services en activiteiten opnieuw op.

De SMS Writer-service wordt automatisch geïnstalleerd. De service moet actief zijn wanneer de VSS-toepassing een back-up of herstel aanvraagt.  

### <a name="writer-id"></a>Schrijver-id  
De schrijver-ID voor de SMS Writer is **03ba67dd-dc6d-4729-a038-251f7018463b**.  

### <a name="permissions"></a>Machtigingen  
De SMS Writer-service moet onder het lokale systeemaccount worden uitgevoerd.  

### <a name="volume-shadow-copy-service"></a>Volume Shadow Copy-service  
De VSS is een set van COM API's die een kader implementeert voor het maken van volume back-ups terwijl toepassingen op het systeem doorgaan met het schrijven naar de volumes. De VSS biedt een consistente interface die coördinatie toestaat tussen toepassingen die gegevens op schijf bijwerken (de SMS Writer-service) en toepassingen die back-ups maken van toepassingen (de Backup Manager-service). Zie de [Volume Shadow Copy service](/windows-server/storage/file-server/volume-shadow-copy-service)voor meer informatie.  



## <a name="next-steps"></a>Volgende stappen
Nadat u een back-up hebt gemaakt, moet u de [site herstellen](recover-sites.md) met die back-up. Aan de hand van deze procedure kunt u vertrouwd raken met het herstel proces voordat u erop moet vertrouwen. Het kan ook helpen te controleren of de back-up is geslaagd voor het beoogde doel.
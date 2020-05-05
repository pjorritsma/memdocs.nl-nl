---
title: Siteserver met hoge beschikbaarheid
titleSuffix: Configuration Manager
description: Hoge Beschik baarheid configureren voor de Configuration Manager-site server door een site server in de passieve modus toe te voegen.
ms.date: 02/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 395504f5ccc3635f580bca739f1c4b7273861123
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718306"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Hoge Beschik baarheid van site server in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1128774-->

In het verleden kunt u redundantie toevoegen aan de meeste rollen in Configuration Manager door meerdere exemplaren van deze rollen te hebben in uw omgeving. Behalve voor de site server zelf. Hoge Beschik baarheid voor de site serverrol is een op Configuration Manager gebaseerde oplossing voor het installeren van een extra site server in de *passieve* modus. De centrale beheer site en de onderliggende primaire sites kunnen een extra site server in de passieve modus hebben. De site server in de passieve modus kan on-premises of in de cloud worden uitgevoerd in Azure.

Deze functie biedt de volgende voor delen

- Redundantie en hoge Beschik baarheid voor de site serverrol  
- Het is eenvoudiger om de hardware of het besturings systeem van de site server te wijzigen  
- Uw site server eenvoudiger verplaatsen naar Azure IaaS  

De site server in de passieve modus is een aanvulling op uw bestaande site server in de *actieve* modus. Een site server in de passieve modus is beschikbaar voor onmiddellijk gebruik, indien nodig. Neem deze extra site server op als onderdeel van het algehele ontwerp om de Configuration Manager-service [Maxi maal beschikbaar](high-availability-options.md)te maken.  

Een site server in de passieve modus:

- Maakt gebruik van dezelfde site database als uw site server in de actieve modus.
- Schrijft geen gegevens naar de site database in de passieve modus.
- Maakt gebruik van dezelfde inhouds bibliotheek als uw site server in de actieve modus.

Als u de site server in de passieve modus actief wilt maken, moet u deze hand matig *promo veren* . Met deze actie wordt de site server in de actieve modus overgeschakeld naar de site server in de passieve modus. De site systeem rollen die beschikbaar zijn op de oorspronkelijke actieve modus server blijven beschikbaar zolang die computer toegankelijk is. Alleen de site serverrol is overgeschakeld tussen de actieve en passieve modus.

Micro soft Core Services-Engineering en-bewerkingen gebruiken deze functie om hun centrale beheer site te migreren naar Microsoft Azure. Zie het [artikel micro soft it show case](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure)voor meer informatie.

## <a name="prerequisites"></a>Vereisten

- De inhouds bibliotheek van de site moet zich op een externe netwerk share bestaan. Beide site servers hebben machtigingen voor volledig beheer voor de share en de inhoud. Zie [inhouds bibliotheek beheren](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote)voor meer informatie.<!--1357525-->  

  - Het computer account van de site server moet machtigingen voor **volledig beheer** hebben voor het netwerkpad waarnaar u de inhouds bibliotheek verplaatst. Deze machtiging is van toepassing op zowel de share als het bestands systeem. Er zijn geen onderdelen geïnstalleerd op het externe systeem.

  - De-site server kan geen rol voor distributie punt hebben. Het distributie punt gebruikt ook de inhouds bibliotheek en deze rol biedt geen ondersteuning voor een externe inhouds bibliotheek. Nadat u de inhouds bibliotheek hebt verplaatst, kunt u de distributiepuntrol niet toevoegen aan de site server.  

- De site server in de passieve modus kan on-premises of in de cloud worden uitgevoerd in Azure.  

    > [!NOTE]
    > Een cloud-gebaseerde site server in de passieve modus maakt gebruik van Azure Infrastructure as a Service (IaaS). Raadpleeg voor meer informatie de volgende artikelen:
    >
    >   - [Virtuele Azure-machines (voor Cloud infrastructuur)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    >   - [Veelgestelde vragen over Configuration Manager in azure](../../../understand/configuration-manager-on-azure.md)  

- Beide site servers moeten lid zijn van hetzelfde Active Directory domein.  

- Configuration Manager ondersteunt site servers in de passieve modus in een-hiërarchie. De centrale beheer site en de onderliggende primaire sites kunnen een extra site server in de passieve modus hebben.<!-- 3607755 -->  

- Beide site servers moeten dezelfde site database gebruiken.  

  - De data base kan extern van elke site server zijn. Vanaf versie 1810 wordt de installatie van de site serverrol op een computer met de Windows-functie voor failover clustering niet meer geblokkeerd door het installatie proces Configuration Manager. Voor SQL always on is deze rol vereist, zodat u de site database niet kunt vinden op de site server. Met deze wijziging kunt u een Maxi maal beschik bare site met minder servers maken met behulp van SQL always on en een site server in de passieve modus.<!-- SCCMDocs issue 1074 -->  

  - De SQL Server die als host fungeert voor de site database kan gebruikmaken van een standaard exemplaar, een benoemd exemplaar, een [SQL Server cluster](use-a-sql-server-cluster-for-the-site-database.md)of een SQL Server AlwaysOn- [beschikbaarheids groep](sql-server-alwayson-for-a-highly-available-site-database.md).  

  - Beide site servers hebben de beveiligingsrol **sysadmin** nodig op het exemplaar van SQL Server dat als host fungeert voor de site database. De oorspronkelijke site server moet deze rollen al hebben, dus voeg deze toe voor de nieuwe site server. Het volgende SQL-script voegt bijvoorbeeld deze rollen toe voor de nieuwe site server **VM2** in het contoso-domein:  

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

  - Beide site servers moeten toegang hebben tot de site database op het exemplaar van SQL Server. De oorspronkelijke site server moet deze toegang al hebben, dus voeg deze toe voor de nieuwe site server. Met het volgende SQL-script wordt bijvoorbeeld een aanmelding toegevoegd aan de **CM_ABC** -Data Base voor de nieuwe site server **VM2** in het contoso-domein:  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

  - De site server in de passieve modus is geconfigureerd voor gebruik van dezelfde site database als de site server in de actieve modus. De site server in de passieve modus leest alleen uit de-data base. Er wordt pas naar de data base geschreven nadat deze in de actieve modus is gepromoveerd.  

- De site server in de passieve modus:  

  - Moet voldoen aan de vereisten voor het installeren van een primaire site. Bijvoorbeeld .NET Framework, externe differentiële compressie en de Windows ADK. Zie [site-en site systeem vereisten](../../../plan-design/configs/site-and-site-system-prerequisites.md)voor de volledige lijst.<!-- SCCMDocs issue 765 -->  

    > [!NOTE]
    > Zorg ervoor dat u de SQL Server Native Client installeert. Als u deze niet installeert, wordt Configuration Manager tijdens de installatie van de vereiste controle een fout gerapporteerd over ontbrekende SQL Server machtigingen.<!-- SCCMDocs#2290 -->

  - Moet het computer account in de lokale groep Administrators op de site server in de actieve modus hebben.<!--516036-->

  - Moet worden geïnstalleerd met behulp van bron bestanden die overeenkomen met de versie van de site server in de actieve modus.  

  - Er kan geen site systeemrol van een site worden geïnstalleerd voordat u de site server installeert in de passieve modus rol.  

- Op beide site servers kunnen verschillende versies van besturings systemen of service packs worden uitgevoerd, mits beide [door Configuration Manager worden ondersteund](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

- Host niet de rol service aansluitpunt op de site server die is geconfigureerd voor hoge Beschik baarheid. Als het momenteel op de oorspronkelijke site server staat, verwijdert u deze en installeert u deze op een andere site systeem server. Zie [about the Service Connection Point](about-the-service-connection-point.md)(Engelstalig) voor meer informatie.  

- Machtigingen voor het [installatie account van het site systeem](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)  

  - Standaard gebruiken veel klanten het computer account van de site server om nieuwe site systemen te installeren. De vereiste is om het computer account van de site server toe te voegen aan de lokale groep **Administrators** op het externe site systeem. Als uw omgeving gebruikmaakt van deze configuratie, moet u ervoor zorgen dat u het computer account van de nieuwe site server toevoegt aan deze lokale groep op alle externe site systemen. Bijvoorbeeld alle externe distributie punten.  

  - De veiligere en aanbevolen configuratie is het gebruik van een service account voor het installeren van het site systeem. De veiligste configuratie is het gebruik van een lokaal service account. Als uw omgeving gebruikmaakt van deze configuratie, is er geen wijziging nodig.  

## <a name="limitations"></a>Beperkingen

- Op elke site wordt slechts één site server in de passieve modus ondersteund.  

- Een site server in de passieve modus wordt niet ondersteund op een secundaire site.<!--SCCMDocs issue 680-->  

    > [!NOTE]  
    > Secundaire sites worden nog steeds ondersteund onder een primaire site met Maxi maal beschik bare site servers.

- De promotie van de site server in de passieve modus naar de actieve modus is hand matig. Er is geen automatische failover.  

- Site systeem rollen kunnen niet op de nieuwe server worden geïnstalleerd voordat u de site server in de passieve modus toevoegt.  

    > [!NOTE]
    > Nadat de site server in de passieve modus is geïnstalleerd, kunt u indien nodig aanvullende rollen toevoegen. Bijvoorbeeld een beheer punt op een primaire site.

- Voor rollen zoals het rapportage punt dat gebruikmaakt van een-Data Base, moet u de data base hosten op een server die extern is van beide site servers.  

- De Configuration Manager-console wordt niet automatisch geïnstalleerd op de site server in de passieve modus.  

## <a name="add-a-site-server-in-passive-mode"></a>Een site server toevoegen in de passieve modus

Zie [site systeem rollen installeren](install-site-system-roles.md)voor meer informatie over het algemene proces voor het toevoegen van rollen.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit, selecteer het knoop punt **sites** en klik op **site systeem server maken** in het lint.

2. Geef op de pagina **Algemeen** van de wizard site systeem server maken de server op waarop de site server moet worden gehost in de passieve modus. De server die u opgeeft, kan geen site systeem rollen hosten voordat een site server in de passieve modus wordt geïnstalleerd.  

3. Selecteer op de pagina **selectie van systeem functie** alleen **site server in de passieve modus**.  

    > [!NOTE]  
    > De wizard voert de volgende controles van de eerste vereisten op deze pagina uit:
    >
    > - De geselecteerde server is geen secundaire site server
    > - De geselecteerde server is niet al een site server in de passieve modus
    > - De inhouds bibliotheek van de site bevindt zich op een externe locatie  
    >  
    > Als deze eerste controles zijn mislukt, kunt u niet door gaan met de volgende pagina van de wizard.  

4. Geef op de pagina **site server op passieve modus** de volgende informatie op die wordt gebruikt om Setup uit te voeren en de site serverrol op de opgegeven server te installeren:

     - Kies een van de volgende opties:  

         - **Bron bestanden voor de installatie via het netwerk kopiëren van de site server in de actieve modus: met**deze optie wordt een gecomprimeerd pakket gemaakt en verzonden naar de nieuwe site server.  

         - **Gebruik de bron bestanden op de volgende locatie op de site server in de passieve modus**: bijvoorbeeld een lokaal pad waarnaar u de bron bestanden al hebt gekopieerd. Zorg ervoor dat deze inhoud dezelfde versie heeft als de site server in de actieve modus.  

         - (*Aanbevolen*) **De bron bestanden op de volgende netwerk locatie gebruiken**: Geef het pad rechtstreeks op naar de inhoud van de **cd. Meest recente** map van de site server in de actieve modus. Bijvoorbeeld: `\\Server\SMS_ABC\CD.Latest` '*Server*' is de naam van de site server in de actieve modus en '*ABC*' is de site code.  

     - Geef het lokale pad op waarop Configuration Manager op de nieuwe site server wilt installeren. Bijvoorbeeld: `C:\Program Files\Configuration Manager`  

5. Voltooi de wizard. Configuration Manager wordt de site server vervolgens in de passieve modus geïnstalleerd op de opgegeven server.

Voor een gedetailleerde installatie status gaat u in de-console naar de werk ruimte **bewaking** en selecteert u het knoop punt **status van site server** . De status van de site server in de passieve modus wordt weer gegeven als **installatie**. Selecteer de server en klik op **status weer geven**voor meer gedetailleerde informatie. Met deze actie wordt het venster installatie status van de site server geopend. Wanneer het proces is voltooid, ziet u de status **OK** voor beide servers.

Zie voor meer informatie over het installatie proces [stroom diagram: een site server instellen in de passieve modus](passive-site-server-flowchart.md).

Nadat u een site server in de passieve modus hebt toegevoegd, ziet u beide site servers op het tabblad **knoop punten** in het knoop punt **sites** van de-console.

Alle Configuration Manager site Server onderdelen bevinden zich in de stand-bymodus op de site server in de passieve modus. De Windows-Services worden nog uitgevoerd.

## <a name="site-server-promotion"></a>Promotie van site server  

Op dezelfde manier als met back-up en herstel kunt u het proces plannen en gebruiken om site servers te wijzigen. Houd rekening met de volgende punten in uw promotie plan:  

- Oefen een geplande promotie uit, waarbij beide site servers online zijn. U kunt ook een niet-geplande failover gebruiken door de verbinding met de site server in de actieve modus geforceerd te verbreken of af te sluiten.  

- Bepaal uw operationele processen tijdens de failover en wat u kunt communiceren met andere Configuration Manager-beheerders.  

- Voor een geplande promotie:  

  - Controleer de algemene status van de site-en site onderdelen. Zorg ervoor dat alles in orde is als normaal voor uw omgeving.  

  - Controleer de status van de inhoud voor alle pakketten die actief worden gerepliceerd tussen sites.  

  - Controleer de status van de secundaire site en de replicatie van de site.

  - Start geen nieuwe inhouds distributie taken of onderhoud op onderliggende of secundaire site servers.

    > [!NOTE]
    > Als er tijdens de failover een bestands-of database replicatie tussen sites wordt uitgevoerd, wordt de gerepliceerde inhoud mogelijk niet door de nieuwe site server ontvangen. Als dit het geval is, distribueert u de software-inhoud opnieuw nadat de nieuwe site server actief is.<!--515436--> Voor database replicatie moet u mogelijk een secundaire site opnieuw initialiseren na een failover.<!-- SCCMDocs issue 808 -->

  - Andere geplande activiteiten op hetzelfde moment verminderen of verwijderen. U kunt bijvoorbeeld geen site server promo veren direct na het bijwerken van de site naar een nieuwe versie. Site-update bevat andere taken die mogelijk conflicteren met de promotie van de site server.

    > [!TIP]
    > Hier volgt een voor beeld van hoe andere activiteiten kunnen conflicteren met de promotie van de site server:
    >
    > - Maandag: werk de site bij naar de nieuwste versie. Schakel automatische client upgrade met client Piloting in.
    > - Dinsdag: promoot de site server in de passieve modus als de actieve site server.
    >
    > Op woensdag of donderdag kan deze actie ertoe leiden dat *alle* clients worden bijgewerkt, niet alleen de pilot verzameling. Dit gedrag kan leiden tot aanzienlijk netwerk gebruik en onverwachte belasting op de distributie punten.<!-- SCCMDocs-pr#4794 -->

### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Proces voor het promo veren van de site server in de passieve modus naar de actieve modus

In deze sectie wordt beschreven hoe u de site server in de passieve modus wijzigt in de actieve modus. Als u toegang wilt krijgen tot de site en deze wijziging wilt aanbrengen, moet u toegang hebben tot een exemplaar van de SMS-provider. Zie [meerdere SMS-providers gebruiken](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#BKMK_MultiSMSProv)voor meer informatie.  

> [!IMPORTANT]  
> Als alle exemplaren van de SMS-provider offline zijn, kunt u geen verbinding maken met de site omdat er geen provider beschikbaar is. Wanneer u de site server in de passieve modus toevoegt, installeert Setup een exemplaar van de SMS-provider op deze server.<!-- SCCMDocs#1613 -->
>
> De Configuration Manager-console vraagt de lijst met beschik bare SMS-providers van WMI op de site server. Wanneer u meerdere SMS-providers op een site installeert, wijst de site elke nieuwe verbindings aanvraag wille keurig toe om een geïnstalleerde SMS-provider te gebruiken. U kunt de locatie van de SMS-provider niet opgeven voor gebruik met een specifieke verbindings sessie. Als uw console geen verbinding kan maken met de site omdat de huidige site server offline is, geeft u de andere site server op in het venster site verbinding.  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** . Selecteer de site en schakel over naar het tabblad **knoop punten** . Selecteer de site server in de passieve modus en klik vervolgens op **promo veren naar actief** in het lint. Klik op **Ja** om te bevestigen en door te gaan.
  
2. Vernieuw het console knooppunt. De kolom **status** voor de server die u wilt promo veren wordt weer gegeven op het tabblad **knoop punten** als **promo veren**.  

3. Nadat de promotie is voltooid, ziet u in de kolom **status** **OK** voor zowel de nieuwe site server in de actieve modus als voor de nieuwe site server in de passieve modus. In de kolom **Server naam** voor de site wordt nu de naam van de nieuwe site server in de actieve modus weer gegeven.

Voor gedetailleerde status, gaat u naar de werk ruimte **bewaking** en selecteert u het knoop punt **status van site server** . In de kolom **modus** wordt aangegeven welke server *actief* of *passief*is. Wanneer u een server van de passieve modus naar de actieve modus promo veren, selecteert u de site server die u wilt promo veren naar actief en kiest u **status weer geven** op het lint. Met deze actie opent u het venster promotie status van site server waarin extra informatie over het proces wordt weer gegeven.

Wanneer een site server in de actieve modus overschakelt naar de passieve modus, wordt alleen de site systeemrol passief gemaakt. Alle andere site systeem rollen die op die computer zijn geïnstalleerd, blijven actief en toegankelijk voor clients.

Zie voor meer informatie over het *geplande* promotie proces [stroom diagram niveau site server (gepland)](promote-site-server-flowchart.md).

### <a name="unplanned-failover"></a>Niet-geplande failover

Als de huidige site server in de actieve modus offline is, probeert de site server voor promotie 30 minuten verbinding te maken met de huidige site server in de actieve modus. Als de offline server voor deze periode terugkomt, wordt er een melding weer gegeven en wordt de wijziging correct doorgevoerd. Anders wordt de site server voor promotie geforceerd bijgewerkt, zodat deze actief is. Als de offline server na deze tijd wordt weer gegeven, controleert deze eerst de huidige status in de site database. Vervolgens wordt het niveau van de site server in de passieve modus gedegradeerd.

Tijdens deze wacht tijd van 30 minuten heeft de site geen site server in de actieve modus. Clients communiceren nog steeds met client gerichte rollen, zoals beheer punten, software-update punten en distributie punten. Gebruikers kunnen software installeren die al is geïmplementeerd. Er is in deze tijds periode geen site beheer mogelijk. Zie voor meer informatie [site fout effecten](../../manage/site-failure-impacts.md).  

Als de offline server zodanig is beschadigd dat deze niet kan worden geretourneerd, verwijdert u deze site server uit de-console. Maak vervolgens een nieuwe site server in de passieve modus om een Maxi maal beschik bare service te herstellen.

Zie voor meer informatie over het niet- *geplande* failover [-proces stroom diagram site server (niet gepland)](promote-site-server-unplanned-flowchart.md).

### <a name="additional-tasks-after-site-server-promotion"></a>Aanvullende taken na de promotie van de site server  

Na het overschakelen van site servers hoeft u de meeste andere taken niet uit te voeren wanneer u [een site herstelt](../../manage/recover-sites.md#post-recovery-tasks). U hoeft bijvoorbeeld geen wacht woorden opnieuw in te stellen of uw Microsoft Intune-abonnement opnieuw te verbinden.

De volgende stappen kunnen vereist zijn indien nodig in uw omgeving:  

- Als u PKI-certificaten voor distributie punten importeert, moet u het certificaat voor de betrokken servers opnieuw importeren. Zie [de certificaten voor distributie punten opnieuw genereren](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points)voor meer informatie.  

- Als u Configuration Manager integreert met de Microsoft Store voor bedrijven, moet u die verbinding opnieuw configureren. Zie [apps beheren vanuit de Microsoft Store voor bedrijven](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)voor meer informatie.  

## <a name="daily-monitoring"></a>Dagelijkse bewaking

Wanneer u een site server in de passieve modus hebt, controleert u deze per dag. Zorg ervoor dat de status ervan ongewijzigd blijft en klaar is voor gebruik. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** en selecteer het knoop punt **status van site server** . Zowel site servers als hun huidige status weer geven. Bekijk ook de status in de werk ruimte **beheer** . Vouw **site configuratie**uit en selecteer het knoop punt **sites** . Selecteer de site en schakel over naar het tabblad **knoop punten** .

> [!NOTE]
> Wanneer u de site bijwerkt naar een nieuwe versie van Configuration Manager, werkt de site server ook bij in de passieve modus. <!-- SCCMDocs-pr#4293 -->
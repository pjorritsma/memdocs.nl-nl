---
title: Inhoud migreren
titleSuffix: Configuration Manager
description: Gebruik distributie punten om inhoud te beheren wanneer u gegevens migreert naar een Configuration Manager huidige vertakkings doel hiërarchie.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: afb39af5087daaca3b2bb6eb15f33d81d959beec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719685"
---
# <a name="plan-a-content-deployment-migration-strategy-in-configuration-manager"></a>Een strategie voor de migratie van een inhouds implementatie plannen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Terwijl u actief gegevens migreert naar een Configuration Manager huidige vertakkings doel hiërarchie, kunnen Configuration Manager-clients in zowel de bron-als de doel hiërarchie de toegang tot inhoud onderhouden die u in de bron hiërarchie hebt geïmplementeerd. U kunt ook migratie gebruiken om distributie punten van de bron hiërarchie bij te werken of opnieuw toe te wijzen om distributie punten in de doel hiërarchie te worden. Wanneer u distributiepunten deelt of opnieuw toewijst, kan deze strategie u helpen om te vermijden dat u inhouden opnieuw implementeert op nieuwe servers in de doelhiërarchie voor de clients die u migreert.  

Hoewel u inhoud opnieuw kunt creëren en verdelen in de doelhiërarchie, kunt u ook de volgende punten gebruiken om deze inhoud te beheren:  

-   Deel distributiepunten in de doelhiërarchie met clients in de doelhiërarchie.  

-   Upgrade zelfstandige Configuration Manager 2007-distributie punten of Configuration Manager 2007 secundaire sites in de bron hiërarchie om distributie punten in de doel hiërarchie te worden.  

-   Distributie punten van een Configuration Manager-bron hiërarchie opnieuw toewijzen aan een site in de doel hiërarchie.  

##  <a name="share-distribution-points-between-source-and-destination-hierarchies"></a><a name="About_Shared_DPs_in_Migration"></a> Distributiepunten delen tussen de bron- en doelhiërarchieën  
Tijdens migratie kunt u distributiepunten delen van een bronhiërarchie met de doelhiërarchie. U kunt gedeelde distributiepunten gebruiken om inhoud, die u gemigreerd hebt van een bronhiärarchie, onmiddellijk beschikbaar te maken voor klanten in de doelhiërarchie zonder dat u opnieuw inhoud moet creëren, en hem dan verdelen naar nieuwe distributiepunten in de doelhiërarchie. Wanneer clients in de doelhiërarchie inhoud opvragen die geïmplementeerd is naar distributiepunten die u gedeeld hebt, kunnen de distributiepunten als geldige locaties van inhoud aangeboden worden aan de clients.  

 Naast een geldige inhouds locatie voor clients in de doel hiërarchie terwijl de migratie van de bron hiërarchie actief blijft, is het mogelijk om een distributie punt te upgraden of opnieuw toe te wijzen aan de doel hiërarchie. U kunt Configuration Manager 2007 gedeelde distributie punten upgraden en System Center 2012 Configuration Manager gedeelde distributie punten opnieuw toewijzen. Als u een gedeeld distributiepunt updatet of opnieuw toewijst, wordt het distributiepunt verwijderd van de bronhiërarchie en wordt het een distributiepunt in de doelhiërarchie. Nadat u een gedeeld distributiepunt updatet of opnieuw toewijst, kunt u het distributiepunt in de doelhiërarchie blijven gebruiken nadat de migratie vanaf de bronhiërarchie beëindigd is. Zie voor meer informatie over het bijwerken van een gedeeld distributie punt [plannen voor het upgraden van Configuration Manager 2007 gedeelde distributie punten](#Planning_to_Upgrade_DPs). Zie voor meer informatie over het opnieuw toewijzen van een gedeeld distributie punt [plannen om Configuration Manager distributie punten opnieuw toe te wijzen](#BKMK_ReassignDistPoint).  

 U kunt ervoor kiezen om distributiepunten te delen vanaf om het even welke bronsite in uw bronhiërarchie. Wanneer u distributie punten voor een bron site deelt, worden onderliggende secundaire sites gedeeld op elk in aanmerking komend distributie punt op die primaire site en op elk van de primaire sites. Om te kwalificeren om een gedeeld distributie punt te zijn, moet de site systeem server die het distributie punt host, worden ingesteld met een Fully Qualified Domain Name (FQDN). Distributie punten die zijn ingesteld met een NetBIOS-naam, worden genegeerd.  

> [!TIP]  
>  Voor Configuration Manager 2007 is het niet vereist dat u een FQDN-naam voor site systeem servers instelt.  

Gebruik de volgende informatie om u te helpen bij het plannen van gedeelde distributiepunten:  

-   Distributiepunten die u deelt, moeten voldoen aan de vereisten voor gedeelde distributiepunten. Zie [vereiste configuraties voor migratie](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) in [vereisten voor migratie](../../core/migration/prerequisites-for-migration.md)voor meer informatie over deze vereisten.  

-   De gedeelde distributiepunt-actie is een instelling die draagt over de hele site, die alle gekwalificeerde distributiepunten delen op een bronsite en op alle rechtstreeks onderliggende, secundaire sites. U kunt geen individuele distributiepunten selecteren voor het delen als u delen van distributiepunten inschakelt.  

-   Clients in de doelhiërarchie kunnen informatie over plaats van inhoud ontvangen voor pakketten die gedistribueerd zijn naar distributiepunten die gedeeld zijn vanaf de doelhiërarchie. Voor distributie punten van een Configuration Manager 2007-bron hiërarchie, waaronder vertakkings distributiepunten, distributie punten op server shares en standaard distributie punten.  

    > [!WARNING]  
    >  Indien u de bronhiërarchie wijzigt, zijn gedeelde distributiepunten van de originele bronhiërarchie niet langer beschikbaar en kunnen ze niet aangeboden worden als locatie van inhoud voor clients in de doelhiërarchie. Indien u de migratie herconfigureert om de oorspronkelijke bronhiërarchie te gebruiken, worden de voordien gedeelde distributiepunten gedeeld als geldige servers van locatie van inhoud.  

-   Wanneer u een pakket migreert dat gehost is op een gedeeld distributiepunt, moet de versie van het pakket dezelfde blijven in de bron- en doelhiërarchieën. Wanneer een pakketversie niet dezelfde is in de bron- en doelhiërarchie, kunnen clients in de doelhiërarchie deze inhoud niet ophalen van het gedeelde distributiepunt. Daarom moet u, indien u een pakket updatet in de doelhiërarchie, de pakketgegevens opnieuw migreren vóór clients in de doelhiërarchie deze inhoud ophalen van een gedeeld distributiepunt.  

    > [!NOTE]  
    >  Wanneer u details bekijkt voor een pakket dat wordt gehost op een gedeeld distributie punt, wordt het aantal pakketten dat wordt weer gegeven als **gehoste gemigreerde pakketten** op het tabblad **gedeelde distributie punten** van de bron site pas bijgewerkt als de volgende cyclus voor het verzamelen van gegevens is voltooid.  

-   U kunt gedeelde distributie punten en hun eigenschappen weer geven in het knoop punt **bron hiërarchie** van de werk ruimte **beheer** in de Configuration Manager-console die verbinding maakt met de doel hiërarchie.  

-   U kunt geen gedeeld distributie punt van een Configuration Manager 2007-bron hiërarchie gebruiken om pakketten te hosten voor micro soft Application Virtualization (app-V). App-V pakketen moeten migreren en geconverteerd worden om te kunnen gebruikt worden door clients in de doelhiërarchie. U kunt echter een gedeeld distributie punt van een System Center 2012-Configuration Manager of Configuration Manager huidige branch-bron hiërarchie gebruiken om app-V-pakketten te hosten voor clients in een doel hiërarchie.  

-   Wanneer u een beveiligd distributie punt deelt vanuit een Configuration Manager 2007-bron hiërarchie, maakt de doel hiërarchie een grens groep die de beveiligde netwerk locaties van dat distributie punt bevat. U kunt deze grens groep in de doel hiërarchie niet wijzigen. Als u echter de beveiligde grens gegevens voor het distributie punt in de bron hiërarchie van Configuration Manager 2007 wijzigt, wordt die wijziging weer gegeven in de doel hiërarchie nadat de volgende cyclus voor het verzamelen van gegevens is voltooid.  

    > [!NOTE]  
    >  System Center 2012 Configuration Manager en Configuration Manager huidige branch-sites gebruiken het concept van voorkeurs distributiepunten in plaats van beveiligde distributie punten. Deze voor waarde is alleen van toepassing op distributie punten die worden gedeeld via Configuration Manager 2007-bron sites.  

De in aanmerking komende distributie punten zijn niet zichtbaar in de Configuration Manager-console voordat u distributie punten van een bron site deelt. Nadat u distributiepunten deelt, worden enkel de distributiepunten getoond die effectief gedeeld worden.  

Nadat u de distributiepunten hebt gedeeld, kunt u de configuratie van een gedeeld distributiepunt wijzigen in de bronhiërarchie. Wijzigingen die u maakt aan de configuratie van een distributiepunt worden weerspiegeld in de doelhiërarchie na de volgende cyclus van gegevensgaring, Distributiepunten die u updatet om ze in aanmerking te laten komen voor delen, worden automatisch gedeeld, terwijl deze die niet langer in aanmerking komen, niet langer gedeeld worden. U kunt bijvoorbeeld een distributie punt hebben dat niet is ingesteld met een intranet-FQDN en niet oorspronkelijk is gedeeld met de doel hiërarchie. Nadat u de FQDN voor dat distributie punt hebt ingesteld, identificeert de volgende gegevens verzamelings cyclus deze configuratie. het distributie punt wordt vervolgens gedeeld met de doel hiërarchie.  

##  <a name="plan-to-upgrade-configuration-manager-2007-shared-distribution-points"></a><a name="Planning_to_Upgrade_DPs"></a>Upgrade van Configuration Manager 2007 gedeelde distributie punten plannen  
Wanneer u migreert vanaf een Configuration Manager 2007-bron hiërarchie, kunt u een gedeeld distributie punt bijwerken om er een Configuration Manager het huidige vertakkings distributiepunt van te maken. U kunt distributie punten bijwerken op primaire sites en secundaire sites. Het upgrade proces verwijdert het distributie punt uit de hiërarchie Configuration Manager 2007 en maakt er een site systeem server in de doel hiërarchie. Dit proces kopieert ook de bestaande inhoud op het distributie punt naar een nieuwe locatie op de distributiepunt computer. Het updateproces wijzigt dan de kopie van de inhoud om de single instance store te creëren voor gebruik met inhoudimplementatie in de doelhiërarchie. Wanneer u een upgrade uitvoert voor een distributie punt, moet u daarom gemigreerde inhoud die op het Configuration Manager 2007-distributie punt is gehost, niet opnieuw distribueren.  

Nadat Configuration Manager de inhoud naar de Single Instance Store hebt geconverteerd, Configuration Manager de oorspronkelijke bron inhoud op de distributiepunt computer verwijderen om schijf ruimte vrij te maken. Configuration Manager maakt geen gebruik van de oorspronkelijke locatie van de inhoud van de bron.  

Niet alle Configuration Manager 2007-distributie punten die u kunt delen, komen in aanmerking voor een upgrade naar Configuration Manager current branch. Om in aanmerking te komen voor een upgrade, moet een Configuration Manager 2007-distributie punt voldoen aan de voor waarden voor de upgrade. Deze voor waarden omvatten de site systeem server waarop het distributie punt is geïnstalleerd en het type Configuration Manager 2007-distributie punt dat is geïnstalleerd. U kunt bijvoorbeeld geen enkel type distributiepunt updaten dat geïnstalleerd is op de servercomputer van de primaire site, maar u kunt een standaard distributiepunt updaten dat geïnstalleerd is op de servercomputer van de site op een secundaire site.  

> [!NOTE]  
>  U kunt alleen die Configuration Manager 2007 gedeelde distributie punten bijwerken die zich op een computer bevinden waarop een versie van het besturings systeem wordt uitgevoerd die wordt ondersteund voor distributie punten in de doel hiërarchie. Hoewel u bijvoorbeeld een Configuration Manager 2007-distributie punt kunt delen dat zich op een computer met Windows Vista bevindt, kunt u dit gedeelde distributie punt niet bijwerken omdat het besturings systeem niet wordt ondersteund door Configuration Manager huidige vertakking voor gebruik als een distributie punt.  

De volgende tabel bevat de ondersteunde locaties voor elk type Configuration Manager 2007-distributie punt dat u kunt upgraden.  

|Type distributiepunt|Distributiepunt op een sitesysteemcomputer die niet de siteserver is|Distributiepunt op een sitesysteemcomputer die niet de siteserver is en die andere systeemfuncties voor de site host|Distributiepunt op een secundaire siteserver|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Standaard distributiepunt|Ja|Nee|Ja|  
|Distributiepunt op server deelt<sup>1</sup>|Ja|Nee|Nee|  
|Vertakkingsdistributiepunt|Ja|Nee|Nee|  

 <sup>1</sup> Configuration Manager huidige vertakking biedt geen ondersteuning voor Server shares voor site systemen, maar ondersteunt wel de upgrade van een Configuration Manager 2007-distributie punt dat zich op een server share bevindt. Wanneer u een upgrade uitvoert voor een Configuration Manager 2007-distributie punt dat zich op een server share bevindt, wordt het type distributie punt automatisch geconverteerd naar een server en moet u het station op de distributiepunt computer selecteren waarop de single instance Content Store wordt opgeslagen.  

> [!WARNING]  
>  Voordat u een vertakkings distributiepunt bijwerkt, moet u de Configuration Manager 2007-client software verwijderen. Wanneer u een vertakkings distributiepunt bijwerkt waarop de Configuration Manager 2007-client software is geïnstalleerd, wordt de inhoud die eerder op de computer is geïmplementeerd, verwijderd van de computer en mislukt de upgrade van het distributie punt.  

Als u distributie punten wilt identificeren die in aanmerking komen voor een upgrade in de Configuration Manager-console in het knoop punt **bron hiërarchie** , selecteert u een bron site en selecteert u vervolgens het tabblad **gedeelde distributie punten** . in aanmerking komende distributie punten worden **Ja** weer gegeven in de kolom **in aanmerking voor upgrade** .  

Wanneer u een upgrade uitvoert voor een distributie punt dat is geïnstalleerd op een Configuration Manager 2007 secundaire site server, wordt de secundaire site verwijderd uit de bron hiërarchie. Hoewel dit scenario een secundaire site-upgrade wordt genoemd, is dit alleen van toepassing op de sitesysteemrol voor distributiepunten. Het resultaat is dat de secundaire site niet wordt bijgewerkt en dat deze in plaats daarvan wordt verwijderd. Hiermee verlaat u een distributie punt uit de doel hiërarchie op de computer die de secundaire site server was. Als u van plan bent om het distributie punt op een secundaire site bij te werken, raadpleegt u een [upgrade plannen Configuration Manager 2007 secundaire sites](#BKMK_UpgradeSS) in dit onderwerp.  

###  <a name="distribution-point-upgrade-process"></a><a name="BKIMK_UpgradeProcess"></a> Het upgradeproces voor distributiepunten  
U kunt de Configuration Manager-console gebruiken om een upgrade uit te Configuration Manager 2007-distributie punten die u met de doel hiërarchie hebt gedeeld. Wanneer u een upgrade uitvoert voor een gedeeld distributie punt, wordt het distributie punt verwijderd van de Configuration Manager 2007-site. Deze wordt vervolgens geïnstalleerd als een distributie punt dat is gekoppeld aan een primaire of secundaire site die u opgeeft in de doel hiërarchie. Het upgradeproces maakt een kopie van de gemigreerde inhoud die op het distributiepunt is opgeslagen en converteert deze kopie vervolgens naar de Single Instance Store voor inhoud. Wanneer Configuration Manager een pakket converteert naar de single instance Content Store, wordt dat pakket verwijderd uit de SMSPKG-share op de distributiepunt computer, tenzij het pakket een of meer aankondigingen heeft die zijn ingesteld op **programma uitvoeren vanaf distributie punt**.  

Als u het distributie punt wilt bijwerken, gebruikt Configuration Manager het **toegangs account voor de bron site** dat is ingesteld voor het verzamelen van gegevens van de SMS-provider van de bron site. Hoewel dit account alleen de machtiging **lezen** nodig heeft voor site objecten voor het verzamelen van gegevens van de bron site, moet het ook de machtiging **verwijderen** en **wijzigen** hebben voor de klasse **site** om het distributie punt van de Configuration Manager 2007-site tijdens de upgrade te kunnen verwijderen.  

> [!NOTE]  
>  Configuration Manager kunt inhoud op slechts één distributie punt tegelijk naar de Single Instance Store converteren. Wanneer u meerdere distributiepunt upgrades instelt, worden de distributie punten in de wachtrij geplaatst voor een upgrade en kunnen ze een voor een verwerken.  

Voordat u een upgrade van een gedeeld distributiepunt uitvoert, moet u ervoor zorgen dat alle inhoud die voor het distributiepunt is geïmplementeerd, wordt gemigreerd. Inhoud die u niet migreert voordat u een upgrade van het distributiepunt uitvoert, is na de upgrade niet beschikbaar in de doelhiërarchie. Wanneer u een upgrade van een distributiepunt uitvoert, wordt de inhoud in de gemigreerde pakketten geconverteerd naar een indeling die compatibel is met Single Instance Store in de doelhiërarchie.  

Als u een upgrade wilt uitvoeren van een distributie punt vanuit de Configuration Manager-console, moet de Configuration Manager 2007-site systeem server voldoen aan de volgende voor waarden:  

-   De configuratie en locatie van het distributiepunt moeten in aanmerking komen voor het uitvoeren van een upgrade.  

-   De distributiepunt computer moet over voldoende schijf ruimte beschikken om de inhoud te converteren van de opslag indeling Configuration Manager 2007-inhoud naar de Single Instance Store-indeling. Voor deze conversie is een hoeveelheid beschikbare schijfruimte vereist die gelijk is aan de grootte van het grootste pakket dat op het distributiepunt is opgeslagen.  

-   Op de distributiepuntcomputer moet een besturingssysteemversie worden uitgevoerd die wordt ondersteund als een distributiepunt in de doelhiërarchie.  

    > [!NOTE]  
    >  Als Configuration Manager controleert op het Beschik baarheid van een distributie punt voor een upgrade, wordt de besturingssysteem versie van de distributiepunt computer niet gevalideerd.  

Als u een upgrade wilt uitvoeren voor een distributie punt, vouwt u in de werk ruimte **beheer** de optie **migratie**uit, vouwt u het knoop punt **bron hiërarchie** uit en selecteert u de site die het distributie punt bevat dat u wilt bijwerken. Selecteer vervolgens in het detailvenster op het tabblad **Gedeelde distributiepunten** het distributiepunt waarvoor u een upgrade wilt uitvoeren.  

U kunt controleren of het distributiepunt klaar is voor een upgrade door de status te bekijken in de kolom **Eligible for Reassignment (Kan opnieuw worden toegewezen)** .  Selecteer vervolgens op het lint Configuration Manager console op het tabblad **distributie punten** in de groep **distributie punt** de optie **opnieuw toewijzen**. Hiermee opent u een wizard die u gebruikt om de upgrade van het distributie punt te volt ooien.  

Wanneer u een upgrade uitvoert voor een gedeeld distributiepunt, moet u het distributiepunt toewijzen aan een primaire of secundaire site van uw keuze in de doelhiërarchie. Nadat het distributie punt is bijgewerkt, beheert u het distributie punt als een distributie punt in de doel hiërarchie, zoals elk ander distributie punt.  

U kunt de voortgang van een distributiepunt upgrade in de Configuration Manager-console bewaken door het knoop punt **migratie van distributie punt** te selecteren onder het knoop punt **migratie** van de werk ruimte **beheer** . U kunt ook informatie weergegeven via het bestand **Migmctrl.log** op de server van de centrale beheersite van de doelhiërarchie of in het bestand **distmgr.log** op de siteserver in de doelhiërarchie die het bijgewerkte distributiepunt beheert.  

> [!NOTE]  
>  Wanneer u een upgrade uitvoert voor een distributie punt naar de doel hiërarchie, wordt de site systeemrol van het distributie punt verwijderd van de Configuration Manager 2007-bron site. Pakketten die naar het distributie punt zijn verzonden, worden echter niet bijgewerkt in de Configuration Manager 2007-hiërarchie. In de Configuration Manager 2007-console worden pakketten die naar het distributie punt zijn verzonden, door gaan met het weer geven van de site systeem computer als een distributie punt met een **onbekend** **type** . Volgende updates van het pakket in Configuration Manager 2007 resulteren in Distribution Manager-rapportage fouten in het distmgr. log voor die site wanneer de site probeert het pakket op het onbekende site systeem bij te werken.  

Als u geen upgrade van een gedeeld distributie punt wilt uitvoeren, kunt u nog steeds een distributie punt installeren vanuit de doel hiërarchie op een voormalige Configuration Manager 2007-distributie punt. Voordat u het nieuwe distributie punt kunt installeren, moet u eerst alle Configuration Manager 2007-site systeem rollen van de distributiepunt computer verwijderen. Dit geldt ook voor de Configuration Manager 2007-site als dit de site Server computer is. Wanneer u een Configuration Manager 2007-distributie punt verwijdert, wordt inhoud die op het distributie punt is geïmplementeerd, niet van de computer verwijderd.  

###  <a name="plan-to-upgrade-configuration-manager-2007-secondary-sites"></a><a name="BKMK_UpgradeSS"></a>Upgrade van Configuration Manager 2007 secundaire sites plannen  
 Wanneer u migratie gebruikt om een gedeeld distributie punt dat wordt gehost op een Configuration Manager 2007 secundaire site server, Configuration Manager de site systeemrol van het distributie punt bij te werken naar een distributie punt in de doel hiërarchie. Ook wordt de secundaire site uit de bron hiërarchie verwijderd. Het resultaat is een Configuration Manager huidige Branch-distributie punt, maar geen secundaire site.  

 Configuration Manager moet de secundaire site en alle site systeem rollen op die computer kunnen verwijderen voor een distributie punt op de site Server computer die in aanmerking komt voor upgrade. Normaal gesp roken komt een gedeeld distributie punt op een Configuration Manager 2007-server share in aanmerking voor een upgrade. Wanneer er echter sprake is van een servershare op een secundaire siteserver, komen de secundaire site en eventuele gedeelde distributiepunten op de desbetreffende computer niet aanmerking voor het uitvoeren van een upgrade. Dit komt doordat de server share wordt behandeld als een aanvullend site systeem object wanneer het proces probeert om de secundaire site te verwijderen en dit proces kan dit object niet verwijderen. In dit scenario kunt u een standaarddistributiepunt op de secundaire siteserver inschakelen en vervolgens de inhoud distribueren naar dit standaarddistributiepunt. Dit proces maakt geen gebruik van netwerk bandbreedte en wanneer dit is voltooid, kunt u het distributie punt verwijderen van de server share, de server share verwijderen en vervolgens een upgrade uitvoeren van het distributie punt en de secundaire site.  

 Voordat u een upgrade van een gedeeld distributie punt uitvoert, controleert u de distributiepunt configuratie in Configuration Manager 2007 om te voor komen dat u een distributie punt op een secundaire site wilt upgraden dat u nog steeds wilt gebruiken met Configuration Manager 2007. Dit is een goede gewoonte, omdat na het upgraden van een gedeeld distributie punt dat zich op een secundaire site server bevindt, de site systeem server wordt verwijderd uit de hiërarchie Configuration Manager 2007 en niet langer beschikbaar is voor gebruik met die hiërarchie. Wanneer de secundaire site wordt verwijderd, worden eventueel resterende distributiepunten op deze secundaire site zwevende distributiepunten. Dit betekent dat ze niet meer worden beheerd vanaf Configuration Manager 2007 en niet langer worden gedeeld of in aanmerking komen voor een upgrade.  

> [!WARNING]  
>  Wanneer u gedeelde distributie punten weergeeft in de Configuration Manager-console, is er geen zicht bare indicatie dat een gedeeld distributie punt zich op een externe site systeem server bevindt of op de secundaire site server.  

 Wanneer u een secundaire site hebt op een externe netwerk locatie die voornamelijk wordt gebruikt voor het beheren van de implementatie van inhoud op die externe locatie, kunt u overwegen secundaire sites met een gedeeld distributie punt bij te werken. Omdat u het beheer van de band breedte kunt instellen voor wanneer u inhoud distribueert naar een Configuration Manager huidige vertakkings distributiepunt, kunt u een secundaire site vaak upgraden naar een distributie punt, het distributie punt voor bandbreedte regeling instellen en voor komen dat u een secundaire site installeert op die netwerk locatie in de doel hiërarchie.  

 Het proces voor het uitvoeren van een upgrade van een gedeeld distributie punt op een secundaire site server is hetzelfde als een andere upgrade van een gedeeld distributie punt. Inhoud wordt gekopieerd en geconverteerd naar de Single Instance Store die wordt gebruikt door de doel hiërarchie. Wanneer u echter een upgrade uitvoert van een gedeeld distributie punt dat zich op een secundaire site server bevindt, verwijdert het upgrade proces ook het beheer punt (indien aanwezig) en wordt vervolgens de secundaire site van de server verwijderd. Het resultaat is dat de secundaire site wordt verwijderd uit de hiërarchie Configuration Manager 2007. Als u de secundaire site wilt verwijderen, maakt Configuration Manager gebruik van het account dat is ingesteld voor het verzamelen van gegevens van de bron site.  

 Tijdens de upgrade is er sprake van een vertraging tussen het moment waarop de secundaire site van Configuration Manager 2007 wordt verwijderd en het moment waarop de installatie van het distributie punt in de doel hiërarchie begint. De cyclus voor het verzamelen van gegevens bepaalt deze vertraging van Maxi maal vier uur. De vertraging is bedoeld om ervoor te zorgen dat de secundaire site wordt verwijderd voordat de installatie van het nieuwe distributie punt begint.  

 Zie voor meer informatie over het bijwerken van een gedeeld distributie punt [plannen voor het upgraden van Configuration Manager 2007 gedeelde distributie punten](#Planning_to_Upgrade_DPs).  

##  <a name="plan-to-reassign-configuration-manager-distribution-points"></a><a name="BKMK_ReassignDistPoint"></a>Plannen om Configuration Manager distributie punten opnieuw toe te wijzen  
 Wanneer u migreert van een ondersteunde versie van System Center 2012 Configuration Manager naar een hiërarchie met dezelfde versie, kunt u een gedeeld distributie punt van de bron hiërarchie opnieuw toewijzen aan een site in de doel hiërarchie. Dit is vergelijkbaar met het concept van het upgraden van een Configuration Manager 2007-distributie punt om een distributie punt in de doel hiërarchie te worden. U kunt distributie punten van primaire sites en secundaire sites opnieuw toewijzen. De actie voor het opnieuw toewijzen van een distributie punt verwijdert het distributie punt uit de bron hiërarchie en maakt de computer en het distributie punt een site systeem server van de site die u in de doel hiërarchie selecteert.  

 Wanneer u een distributiepunt opnieuw toewijst, hoeft u gemigreerde inhoud die op het bronsitedistributiepunt werd gehost, niet opnieuw te distribueren. Daarnaast is er voor het opnieuw toewijzen van een distributie punt, in tegens telling tot de upgrade van een Configuration Manager 2007-distributie punt, geen extra schijf ruimte nodig op de distributiepunt computer. Dit komt doordat vanaf System Center 2012-Configuration Manager, distributie punten de Single Instance Store-indeling voor inhoud gebruiken. De inhoud op de distributiepunt computer hoeft niet te worden geconverteerd wanneer het distributie punt tussen hiërarchieën opnieuw wordt toegewezen.  

 Voor een System Center 2012 Configuration Manager distributie punt in aanmerking komen voor opnieuw toewijzen, moet het voldoen aan de volgende criteria:  

-   Een gedeeld distributiepunt moet op een andere computer dan de siteserver zijn geïnstalleerd.  

-   Een gedeeld distributiepunt mag zich niet op dezelfde locatie bevinden als eventuele aanvullende sitesysteemrollen.  

Als u distributie punten wilt identificeren die in aanmerking komen voor opnieuw toewijzen in de Configuration Manager-console in het knoop punt **bron hiërarchie** , selecteert u een bron site en selecteert u vervolgens het tabblad **gedeelde distributie punten** . in aanmerking komende distributie punten worden **Ja** weer gegeven in de kolom komt in aanmerking voor een nieuwe **toewijzing** (deze kolom is een naam die **in aanmerking komt voor upgrade** vóór System Center 2012 R2 Configuration Manager).  

###  <a name="distribution-point-reassignment-process"></a><a name="BKMK_ReassignProcess"></a> Het opnieuw toewijzen van distributiepunten  
 U kunt de Configuration Manager-console gebruiken voor het opnieuw toewijzen van distributie punten die u hebt gedeeld vanuit een actieve bron hiërarchie. Wanneer u een gedeeld distributie punt opnieuw toewijst, wordt het distributie punt verwijderd van de bron site en vervolgens geïnstalleerd als een distributie punt dat is gekoppeld aan een primaire of secundaire site die u opgeeft in de doel hiërarchie.  

 Als u het distributie punt opnieuw wilt toewijzen, gebruikt de doel hiërarchie het toegangs account voor de bron site dat is ingesteld voor het verzamelen van gegevens van de SMS-provider van de bron site. Zie [vereisten voor migratie](../../core/migration/prerequisites-for-migration.md)voor meer informatie over de vereiste machtigingen en aanvullende vereisten.  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Meerdere gedeelde distributie punten tegelijk migreren
Vanaf versie 1610 kunt u het **distributie punt opnieuw toewijzen** gebruiken om Configuration Manager proces parallel de hertoewijzing van maxi maal 50 gedeelde distributie punten tegelijk. Dit omvat gedeelde distributie punten van ondersteunde bron sites waarop wordt uitgevoerd:  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- System Center 2012 R2 Configuration Manager
- Configuration Manager (huidige vertakking)

Wanneer u distributie punten opnieuw toewijst, moet elk distributie punt in aanmerking komen voor een upgrade of een nieuwe toewijzing. De naam van de betreffende actie en het proces (bijwerken of opnieuw toewijzen) is afhankelijk van de versie van Configuration Manager de bron site wordt uitgevoerd. De eind resultaten voor beide acties zijn hetzelfde: het distributie punt is toegewezen aan een van uw Current Branch sites met de inhoud ervan.

Vóór versie 1610 kan Configuration Manager slechts één distributie punt tegelijk verwerken. U kunt nu zo veel distributie punten opnieuw toewijzen als u wilt met het volgende voor behoud:  
- Hoewel u niet meerdere distributie punten kunt selecteren die opnieuw moeten worden toegewezen en u in de wachtrij meer dan één hebt geplaatst, worden ze door Configuration Manager parallel verwerkt in plaats van te wachten totdat de volgende stap wordt uitgevoerd.  
- Standaard worden Maxi maal 50 distributie punten gelijktijdig verwerkt. Nadat de hertoewijzing van het eerste distributie punt is voltooid, begint Configuration Manager de 51st te verwerken, enzovoort.  
- Wanneer u de Configuration Manager SDK gebruikt, kunt u **SharedDPImportThreadLimit** wijzigen om het aantal opnieuw toegewezen distributie punten aan te passen dat Configuration Manager parallel kan worden uitgevoerd.


##  <a name="assign-content-ownership-when-migrating-content"></a><a name="About_Migrating_Content"></a>Eigendom van inhoud toewijzen bij het migreren van inhoud  
 Wanneer u inhoud voor implementaties migreert, moet u het inhoudsobject toewijzen aan een site in de doelhiërarchie. Deze site wordt vervolgens de eigenaar van de desbetreffende inhoud in de doelhiërarchie. Hoewel de site op het hoogste niveau van uw doel hiërarchie de site is die de meta gegevens voor inhoud migreert, is het de toegewezen site die de oorspronkelijke bron bestanden voor de inhoud via het netwerk gebruikt.  

 U kunt overwegen om het eigendom van de inhoud over te dragen aan een site in de doelhiërarchie die zich op het netwerk dicht in de buurt van de inhoudslocatie in de bronhiërarchie bevindt om de bandbreedte te minimaliseren die wordt gebruikt wanneer u inhoud migreert. Omdat informatie over de inhoud in de doelhiërarchie globaal wordt gedeeld, is deze beschikbaar op elke site.  

 Hoewel informatie over inhoud via database replicatie met alle sites wordt gedeeld, wordt inhoud die u toewijst aan een primaire site en die u vervolgens implementeert op distributie punten op andere primaire sites, overgedragen door replicatie op basis van een bestand. Deze overdracht verloopt via de centrale beheersite en vervolgens via de aanvullende primaire site. U kunt gegevens overdrachten over netwerken met een lage band breedte reduceren door de pakketten die u wilt distribueren naar meerdere primaire sites vóór of tijdens de migratie, te centraliseren wanneer u een site toewijst als eigenaar van de inhoud.

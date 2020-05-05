---
title: Herstel zonder toezicht
titleSuffix: Configuration Manager
description: Gebruik een script om uw sites in Configuration Manager te herstellen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a12de673776817330a80cb68588faf225922e241
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720798"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Site Recovery zonder toezicht voor Configuration Manager   

*Van toepassing op: Configuration Manager (huidige vertakking)*

 Als u een [herstel zonder toezicht](recover-sites.md#site-recovery-procedures) van een Configuration Manager centrale beheer site of primaire site wilt uitvoeren, kunt u een script voor installatie zonder toezicht maken en vervolgens Setup gebruiken met de opdracht optie **/script** . Het script geeft hetzelfde type informatie aan dat door de installatie wizard wordt gevraagd, behalve dat er geen standaard instellingen zijn. Alle waarden moeten worden gespecificeerd voor de installatiesleutels die van toepassing zijn op het type herstel dat u gebruikt.

 Als u de opdracht regel optie voor de installatie van/script wilt gebruiken, moet u een initialisatie bestand maken. Geef deze bestands naam vervolgens op na de optie/script. De naam van het bestand is niet belang rijk, zolang het de bestandsnaam extensie **. ini** heeft. Wanneer u verwijst naar het installatie-initialisatiebestand van de opdrachtregel, moet u het volledige pad naar het bestand geven. Als uw installatie-initialisatie bestand bijvoorbeeld *Setup. ini*heet en het is opgeslagen in de *map C:\setup*, is de opdracht regel:

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  U moet over beheerders rechten beschikken om Setup uit te voeren. Wanneer u het installatie programma uitvoert met het script zonder toezicht, start u de opdracht prompt in een beheerders context met behulp van **uitvoeren als Administrator**.

 Het script bevat sectienamen, sleutelnamen en waarden. Vereiste sectiesleutelnamen variëren afhankelijk van het hersteltype waarvoor u een script schrijft. De volgorde van de sleutels binnen secties en de volgorde van secties binnen het bestand zijn niet belangrijk. De sleutels zijn niet hoofdletter gevoelig. Wanneer u waarden voor sleutels opgeeft, moet de naam van de sleutel worden gevolgd door een gelijkteken (=) en de waarde voor de sleutel.

 Gebruik de volgende secties om u te helpen uw script te maken voor herstel van sites zonder toezicht. De tabellen geven een lijst van de beschikbare installatiescriptsleutels, de overeenkomstige waarden ervan, of ze al dan niet vereist zijn, voor welk type installatie ze worden gebruikt en een korte beschrijving voor de sleutel.

## <a name="recover-a-central-administration-site-unattended"></a>Herstellen van een centrale beheersite zonder toezicht
 Gebruik de volgende informatie om een script bestand voor installatie zonder toezicht te configureren voor het herstellen van een centrale beheer site.

 **Aanduiding**

-   **Naam sleutel:** Action

    -   **Vereist:** ja
    -   **Waarden:** RecoverCCAR
    -   **Details:** hiermee herstelt u een centrale beheersite


-   **Sleutel naam:** CDLatest

    -   **Vereist:** Ja: alleen wanneer media vanaf de CD worden gebruikt. Meest recente map.
    -   **Waarden:** 1 een andere waarde dan 1 wordt gezien als niet het gebruik van de cd. Jongste.
    -   **Details:** Uw script moet deze sleutel en waarde bevatten wanneer u Setup uitvoert vanaf media in een CD. Meest recente map voor het installeren van een primaire of centrale beheer site of het herstellen van een primaire of centrale beheer site. Met deze waarde wordt de installatie van media formulier-CD omgevormd. Meest recente wordt gebruikt.

**RecoveryOptions**   
-   **Sleutelnaam:** ServerRecoveryOptions   

    -   **Vereist:** ja
    -   **Waarden:** 1, 2 of 4  
         1 = Siteserver en SQL-server herstellen.   
         2 = Alleen siteserver herstellen.  
         4 = Alleen SQL Server herstellen.
    -   **Details:** Hiermee geeft u op of het installatie programma de site server, SQL Server of beide moet herstellen. De gekoppelde sleutels zijn vereist wanneer u de volgende waarde instelt voor de instelling ServerRecoveryOptions:  
        -   **Waarde = 1** u hebt de mogelijkheid een waarde op te geven voor de sleutel **SiteServerBackupLocation** om de site te herstellen met een siteback-up. Als u geen waarde opgeeft, wordt de site opnieuw geïnstalleerd zonder dat deze wordt hersteld uit een back-upset.

             De sleutel **BackupLocation** is vereist wanneer u een waarde van **10** configureert voor de sleutel **DatabaseRecoveryOptions** . Hiermee wordt de sitedatabase uit de back-up hersteld.

        -   **Waarde = 2** u hebt de mogelijkheid een waarde op te geven voor de sleutel **SiteServerBackupLocation** om de site te herstellen met een siteback-up. Als u geen waarde opgeeft, wordt de site opnieuw geïnstalleerd zonder dat deze wordt hersteld uit een back-upset.

        -   **Waarde = 4** de sleutel **BackupLocation** is vereist wanneer u een waarde van **10** configureert voor de sleutel **DatabaseRecoveryOptions** . Hiermee wordt de sitedatabase uit de back-up hersteld.

-   **Sleutelnaam:** DatabaseRecoveryOptions

    -   **Vereist:** mogelijk
    -   **Gegevens**   
         - **10** = de site database herstellen vanuit een back-up.  
         - **20** = een site database gebruiken die hand matig is hersteld met behulp van een andere methode.   
         - **40** = een nieuwe data base maken voor de site. Gebruik deze optie wanneer er geen back-up van de sitedatabase beschikbaar is. Globale en sitegegevens worden hersteld via replicatie vanaf andere sites.  
         - **80** = database herstel overs Laan.
    -   **Details:** Hiermee geeft u op hoe de site database in SQL Server wordt hersteld door Setup. Deze sleutel is vereist wanneer de instelling **ServerRecoveryOptions** een waarde heeft van **1** of **4**.


-   **Sleutelnaam:** ReferenceSite  

    -   **Vereist:** mogelijk
    -   **Waarden:** &lt;ReferenceSiteFQDN\>
    -   **Details:** Hiermee geeft u de primaire referentie site. Als de back-up van de data base ouder is dan de Bewaar periode voor het bijhouden van wijzigingen of als u de site herstelt zonder een back-up te maken, gebruikt de centrale beheer site de referentie site om globale gegevens te herstellen.

         Wanneer u geen referentie site opgeeft en de back-up ouder is dan de Bewaar periode voor het bijhouden van wijzigingen, worden alle primaire sites opnieuw geïnitialiseerd met de herstelde gegevens van de centrale beheer site.

         Wanneer u geen referentie site opgeeft en de back-up valt binnen de Bewaar periode voor het bijhouden van wijzigingen, worden alleen de wijzigingen sinds de back-up gerepliceerd van primaire sites. Wanneer er conflicterende wijzigingen van verschillende primaire sites zijn, gebruikt de centrale beheersite de eerste die het ontvangt.

         Deze sleutel is vereist wanneer de instelling **DatabaseRecoveryOptions** een waarde heeft van **40**.

-   **Sleutelnaam:** SiteServerBackupLocation

    -   **Vereist:** nee
    -   **Waarden:** &lt;PathToSiteServerBackupSet\>
    -   **Details:** hiermee geeft u het pad op naar de back-upset van de siteserver. Deze sleutel is optioneel wanneer de instelling **ServerRecoveryOptions** een waarde heeft van **1** of **2**. Geef een waarde op voor de sleutel **SiteServerBackupLocation** om de site te herstellen met behulp van een siteback-up. Als u geen waarde opgeeft, wordt de site opnieuw geïnstalleerd zonder dat deze wordt hersteld uit een back-upset.


-   **Sleutelnaam:** BackupLocation

    -   **Vereist:** mogelijk
    -   **Waarden:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Details:** hiermee geeft u het pad op naar de back-upset van de sitedatabase. De sleutel **BackupLocation** is vereist wanneer u een waarde van **1** of **4** configureert voor de sleutel **ServerRecoveryOptions** en een waarde van **10** configureert voor de sleutel **DatabaseRecoveryOptions**.


**Opties**

- **Sleutelnaam:** ProductID
  -   **Vereist:** ja
  -   **Gegevens**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - Eval
  -   **Details:** De product code voor de Configuration Manager-installatie, inclusief de streepjes. Voer **Eval** in om de evaluatie versie van Configuration Manager te installeren.  


- **Sleutelnaam:** SiteCode

  -   **Vereist:** ja
  -   **Waarden:** &lt;site code\>
  -   **Details:** Drie alfanumerieke tekens die de site in uw hiërarchie op unieke wijze identificeren. Geef de site code op die door de site is gebruikt vóór de fout.


- **Sleutelnaam:** SiteName

  -   **Vereist:** ja
  -   **Waarden:** SiteName
  -   **Details:** beschrijving voor deze site.


- **Sleutelnaam:** SMSInstallDir

  - **Vereist:** ja
  - **Waarden:** &lt; *ConfigMgrInstallationPath*>
  - **Details:** Hiermee geeft u de installatiemap op voor de Configuration Manager-programma bestanden.
    > [!NOTE]   
    >  U kunt het oorspronkelijke pad of een nieuw pad opgeven dat moet worden gebruikt voor de installatie van de Configuration Manager.

- **Sleutelnaam:** SDKServer

  -   **Vereist:** ja
  -   **Waarden:** &lt;*FQDN van de SMS-provider*>
  -   **Details:** Hiermee geeft u de FQDN-naam op van de server die als host fungeert voor de SMS-provider. Geef de server op die de SMS-provider heeft gehost vóór de fout.

       U kunt bijkomende SMS-providers voor de site configureren na de eerste installatie.

- **Sleutelnaam:** PrerequisiteComp

  -   **Vereist:** ja
  -   **Waarden:** 0 of 1  
       0 = downloaden   
       1 = reeds gedownload
  -   **Details:** Hiermee geeft u op of de vereiste bestanden voor de installatie al zijn gedownload. Als u bijvoorbeeld de waarde 0 gebruikt, downloadt Setup de bestanden.  


- **Sleutelnaam:** PrerequisitePath

  -   **Vereist:** ja
  -   **Waarden:** &lt;*PathToSetupPrerequisiteFiles*>
  -   **Details:** Hiermee geeft u het pad op naar de vereiste bestanden voor de installatie. Afhankelijk van de waarde van **PrerequisiteComp** , gebruikt Setup dit pad om gedownloade bestanden op te slaan of om eerder gedownloade bestanden te zoeken.

- **Sleutelnaam:** AdminConsole

  -   **Vereist:** mogelijk
  -   **Waarden:** 0 of 1 0 = niet installeren   
       1 = installeren
  -   **Details:** Hiermee geeft u op of de Configuration Manager-console moet worden geïnstalleerd. Deze sleutel is vereist, behalve wanneer de instelling **ServerRecoveryOptions** een waarde heeft van **4**.


- **Sleutelnaam:** JoinCEIP   
  > [!Note]  
  > Vanaf Configuration Manager versie 1802 wordt de functie CEIP verwijderd uit het product.

  -   **Vereist:** ja
  -   **Waarden:** 0 of 1  
       0 = niet aanmelden  
       1 = aanmelden
  -   **Details:** hiermee geeft u op of u deelneemt aan het programma voor kwaliteitsverbetering.

**SQLConfigOptions**

-   **Sleutelnaam:** SQLServerName

    -   **Vereist:** ja
    -   **Waarden:** * &lt;SQL-\>*
    -   **Details:** De naam van de server of de naam van de geclusterde instantie met SQL Server die als host fungeert voor de site database. Geef de server op die de site database heeft gehost vóór de fout.


-   **Sleutelnaam:** DatabaseName

    -   **Vereist:** ja
    -   **Waarden:** * &lt;SiteDatabaseName\> * \\of * &lt;INSTANCENAME\>**SiteDatabaseName&lt;\> *
    -   **Details:** hiermee geeft u de naam op van de SQL Server-database die moet worden gemaakt of gebruikt voor het installeren van de database van de centrale beheersite. Geef dezelfde database naam op die werd gebruikt vóór de fout.

        > [!IMPORTANT]  
        >  Als u het standaard exemplaar niet gebruikt, moet u de exemplaar naam en de naam van de site database opgeven.

-   **Sleutelnaam:** SQLSSBPort

    -   **Vereist:** nee
    -   **Waarden:** &lt;*SSBPortNumber*>
    -   **Details:** hiermee geeft u de SQL SSB-poort (SQL Server Service Broker) op die door de SQL Server wordt gebruikt. Doorgaans is SSB geconfigureerd om TCP-poort 4022 te gebruiken, maar andere poorten worden ondersteund. Geef dezelfde SSB-poort op die voor de fout is gebruikt.

## <a name="recover-a-primary-site-unattended"></a>Herstellen van een primaire site zonder toezicht
 Gebruik de volgende informatie om een script bestand voor installatie zonder toezicht te configureren voor het herstellen van een centrale beheer site.

 **Aanduiding**

-   **Naam sleutel:** Action

    -   **Vereist:** ja
    -   **Waarden:** RecoverPrimarySite
    -   **Details:** hiermee herstelt u een primaire site.


-   **Sleutel naam:** CDLatest

    -   **Vereist:** Ja: alleen wanneer media vanaf de CD worden gebruikt. Meest recente map.
    -   **Waarden:** 1 een andere waarde dan 1 wordt gezien als niet het gebruik van de cd. Jongste.
    -   **Details:** Uw script moet deze sleutel en waarde bevatten wanneer u Setup uitvoert vanaf media in een CD. Meest recente map voor het installeren van een primaire of centrale beheer site of het herstellen van een primaire of centrale beheer site. Met deze waarde wordt de installatie van media formulier-CD omgevormd. Meest recente wordt gebruikt.

**RecoveryOptions**

-   **Sleutelnaam:** ServerRecoveryOptions

    -   **Vereist:** ja
    -   **Waarden:** 1, 2 of 4    
         1 = Siteserver en SQL-server herstellen.   
         2 = Alleen siteserver herstellen.  
         4 = Alleen SQL Server herstellen.
    -   **Details:** Hiermee geeft u op of het installatie programma de site server, SQL Server of beide moet herstellen. De gekoppelde sleutels zijn vereist wanneer u de volgende waarde instelt voor de instelling ServerRecoveryOptions:

        -   **Waarde = 1** u hebt de mogelijkheid een waarde op te geven voor de sleutel **SiteServerBackupLocation** om de site te herstellen met een siteback-up. Als u geen waarde opgeeft, wordt de site opnieuw geïnstalleerd zonder dat deze wordt hersteld uit een back-upset.

             De sleutel **BackupLocation** is vereist wanneer u een waarde van **10** configureert voor de sleutel **DatabaseRecoveryOptions** . Hiermee wordt de sitedatabase uit de back-up hersteld.

        -   **Waarde = 2** u hebt de mogelijkheid een waarde op te geven voor de sleutel **SiteServerBackupLocation** om de site te herstellen met een siteback-up. Als u geen waarde opgeeft, wordt de site opnieuw geïnstalleerd zonder dat deze wordt hersteld uit een back-upset.

        -   **Waarde = 4** de sleutel **BackupLocation** is vereist wanneer u een waarde van **10** configureert voor de sleutel **DatabaseRecoveryOptions** . Hiermee wordt de sitedatabase uit de back-up hersteld.

-   **Sleutelnaam:** DatabaseRecoveryOptions

    -   **Vereist:** mogelijk
    -   **Gegevens**   
         - **10** = de site database herstellen vanuit een back-up.  
         - **20** = een site database gebruiken die hand matig is hersteld met behulp van een andere methode.     
         - **40** = een nieuwe data base maken voor de site. Gebruik deze optie wanneer er geen back-up van de sitedatabase beschikbaar is. Globale en sitegegevens worden hersteld via replicatie vanaf andere sites.  
         - **80** = database herstel overs Laan.
    -   **Details:** Hiermee geeft u op hoe de site database in SQL Server wordt hersteld door Setup. Deze sleutel is vereist wanneer de instelling **ServerRecoveryOptions** een waarde heeft van **1** of **4**.


-   **Sleutelnaam:** SiteServerBackupLocation

    -   **Vereist:** nee
    -   **Waarden:** &lt;PathToSiteServerBackupSet\>
    -   **Details:** hiermee geeft u het pad op naar de back-upset van de siteserver. Deze sleutel is optioneel wanneer de instelling **ServerRecoveryOptions** een waarde heeft van **1** of **2**. Geef een waarde op voor de sleutel **SiteServerBackupLocation** om de site te herstellen met behulp van een siteback-up. Als u geen waarde opgeeft, wordt de site opnieuw geïnstalleerd zonder dat deze wordt hersteld uit een back-upset.     


-   **Sleutelnaam:** BackupLocation

    -   **Vereist:** mogelijk
    -   **Waarden:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Details:** hiermee geeft u het pad op naar de back-upset van de sitedatabase. De sleutel **BackupLocation** is vereist wanneer u een waarde van **1** of **4** configureert voor de sleutel **ServerRecoveryOptions** en een waarde van **10** configureert voor de sleutel **DatabaseRecoveryOptions**.

**Opties**

-   **Sleutelnaam:** ProductID

    -   **Vereist:** ja
    -   **Gegevens**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Eval     
    -   **Details:** De product code voor de Configuration Manager-installatie, inclusief de streepjes. Voer **Eval** in om de evaluatie versie van Configuration Manager te installeren.  


-   **Sleutelnaam:** SiteCode

    -   **Vereist:** ja
    -   **Waarden:** &lt;site code\>
    -   **Details:** Drie alfanumerieke tekens die de site in uw hiërarchie op unieke wijze identificeren. Geef de site code op die door de site is gebruikt vóór de fout.


-   **Sleutelnaam:** SiteName

    -   **Vereist:** ja
    -   **Waarden:** SiteName
    -   **Details:** beschrijving voor deze site.


-   **Sleutelnaam:** SMSInstallDir

    -   **Vereist:** ja
    -   **Waarden:** &lt; *ConfigMgrInstallationPath*>
    -   **Details:** Hiermee geeft u de installatiemap op voor de Configuration Manager-programma bestanden.

        > [!NOTE]   
        >  U kunt het oorspronkelijke pad of een nieuw pad opgeven dat moet worden gebruikt voor de installatie van de Configuration Manager.

-   **Sleutelnaam:** SDKServer

    -   **Vereist:** ja
    -   **Waarden:** &lt;*FQDN van de SMS-provider*>
    -   **Details:** Hiermee geeft u de FQDN-naam op van de server die als host fungeert voor de SMS-provider. Geef de server op die de SMS-provider heeft gehost vóór de fout.

         U kunt bijkomende SMS-providers voor de site configureren na de eerste installatie.

-   **Sleutelnaam:** PrerequisiteComp

    -   **Vereist:** ja
    -   **Waarden:** 0 of 1    
         0 = downloaden   
         1 = reeds gedownload   
    -   **Details:** Hiermee geeft u op of de vereiste bestanden voor de installatie al zijn gedownload. Als u bijvoorbeeld de waarde 0 gebruikt, downloadt Setup de bestanden.


-   **Sleutelnaam:** PrerequisitePath

    -   **Vereist:** ja
    -   **Waarden:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Details:** Hiermee geeft u het pad op naar de vereiste bestanden voor de installatie. Afhankelijk van de waarde van **PrerequisiteComp** , gebruikt Setup dit pad om gedownloade bestanden op te slaan of om eerder gedownloade bestanden te zoeken.


-   **Sleutelnaam:** AdminConsole

    -   **Vereist:** mogelijk
    -   **Waarden:** 0 of 1  
         0 = niet installeren   
         1 = installeren  
    -   **Details:** Hiermee geeft u op of de Configuration Manager-console moet worden geïnstalleerd. Deze sleutel is vereist, behalve wanneer de instelling **ServerRecoveryOptions** een waarde heeft van **4**.

-   **Sleutelnaam:** JoinCEIP  
    > [!Note]  
    > Vanaf Configuration Manager versie 1802 wordt de functie CEIP verwijderd uit het product.

    -   **Vereist:** ja
    -   **Waarden:** 0 of 1    
         0 = niet aanmelden  
         1 = aanmelden
    -   **Details:** hiermee geeft u op of u deelneemt aan het programma voor kwaliteitsverbetering.


**SQLConfigOptions**

-   **Sleutelnaam:** SQLServerName

    -   **Vereist:** ja
    -   **Waarden:** * &lt;SQL-\>*
    -   **Details:** De naam van de server of de naam van de geclusterde instantie met SQL Server die als host fungeert voor de site database. Geef de server op die de site database heeft gehost vóór de fout.


-   **Sleutelnaam:** DatabaseName

    -   **Vereist:** ja
    -   **Waarden:** * &lt;SiteDatabaseName\> * \\of * &lt;INSTANCENAME\>**SiteDatabaseName&lt;\> *
    -   **Details:** hiermee geeft u de naam op van de SQL Server-database die moet worden gemaakt of gebruikt voor het installeren van de database van de centrale beheersite. Geef dezelfde database naam op die werd gebruikt vóór de fout.

        > [!IMPORTANT]    
        >  Als u het standaard exemplaar niet gebruikt, moet u de exemplaar naam en de naam van de site database opgeven.

-   **Sleutelnaam:** SQLSSBPort

    -   **Vereist:** nee
    -   **Waarden:** &lt;*SSBPortNumber*>
    -   **Details:** hiermee geeft u de SQL SSB-poort (SQL Server Service Broker) op die door de SQL Server wordt gebruikt. Doorgaans is SSB geconfigureerd om TCP-poort 4022 te gebruiken, maar andere poorten worden ondersteund. Geef dezelfde SSB-poort op die voor de fout is gebruikt.

**Optie voor hiërarchie-uitbreiding**

-   **Sleutelnaam:** CCARSiteServer

    -   **Vereist:** mogelijk
    -   **Waarden:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Details:** Hiermee geeft u de centrale beheer site op waaraan een primaire site wordt gekoppeld wanneer deze lid wordt van de Configuration Manager-hiërarchie. Deze instelling is vereist als de primaire site was gekoppeld aan een centrale beheersite vóór de fout. Geef de site code op die voor de centrale beheer site is gebruikt vóór de fout.

-   **Sleutelnaam:** CASRetryInterval

    -   **Vereist:** nee
    -   **Waarden:** &lt; *interval*>
    -   **Details:** hiermee geeft u de interval (in minuten) op waarna wordt geprobeerd verbinding te maken met de centrale beheersite nadat de verbinding is verbroken. Als de verbinding met de centrale beheer site mislukt, wacht de primaire site bijvoorbeeld het aantal minuten dat u opgeeft voor CASRetryInterval, en wordt vervolgens opnieuw geprobeerd de verbinding te verbreken.


-   **Sleutelnaam:** WaitForCASTimeout

    -   **Vereist:** nee
    -   **Waarden:** &lt;*Time-out*>
    -   **Details:** hiermee geeft u de maximum time-outwaarde (in minuten) op voor een primaire site om verbinding te maken met de centrale beheersite. Als een primaire site bijvoorbeeld geen verbinding kan maken met een centrale beheersite, probeert de primaire site opnieuw de verbinding met de centrale beheersite te maken op basis van het CASRetryInterval tot de WaitForCASTTimeout-periode is bereikt. U kunt een waarde opgeven van 0 tot 100.

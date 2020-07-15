---
title: Datawarehouse
titleSuffix: Configuration Manager
description: Data Warehouse-service punt en-Data Base voor Configuration Manager
ms.date: 07/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d5ff011c0d25e601ff6605edb49383e58f949203
ms.sourcegitcommit: 1edcfb3ce4350ba1a6f36a6150e86301d35c631b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/15/2020
ms.locfileid: "86390888"
---
# <a name="the-data-warehouse-service-point-for-configuration-manager"></a>Het Data Warehouse-service punt voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1277922-->
Gebruik het Data Warehouse-service punt om historische gegevens over lange termijn voor uw Configuration Manager-implementatie op te slaan en te rapporteren.

> [!NOTE]
> In versie 1910 Configuration Manager deze functie standaard ingeschakeld. In versie 1906 of eerder is Configuration Manager deze optionele functie standaard niet ingeschakeld. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](install-in-console-updates.md#bkmk_options).<!--505213-->

Het Data Warehouse ondersteunt Maxi maal 2 TB aan gegevens, met tijds tempels voor het bijhouden van wijzigingen. In het Data Warehouse worden gegevens opgeslagen door automatisch gegevens te synchroniseren van de Configuration Manager-site database naar de Data Warehouse-data base. Deze informatie is vervolgens toegankelijk vanaf uw Reporting service-punt. De gegevens die naar de Data Warehouse database worden gesynchroniseerd, worden drie jaar bewaard. Regel matig verwijdert een ingebouwde taak gegevens die ouder zijn dan drie jaar.

Gegevens die worden gesynchroniseerd, bevatten het volgende uit de globale gegevens en site gegevens groepen:

- Status van infra structuur
- Beveiliging
- Naleving
- Malware
- Software-implementatie
- Inventaris gegevens (de inventarisatie geschiedenis wordt echter niet gesynchroniseerd)

Wanneer de site systeemrol wordt geïnstalleerd, wordt de Data Warehouse database geïnstalleerd en geconfigureerd. Er worden ook verschillende rapporten geïnstalleerd zodat u deze gegevens eenvoudig kunt zoeken en rapporteren.

## <a name="prerequisites"></a>Vereisten

- De site systeemrol van het Data Warehouse wordt alleen ondersteund op de site op het hoogste niveau van uw hiërarchie. Een voor beeld: een centrale beheer site (CAS) of zelfstandige primaire site.

- De computer waarop u de site systeemrol installeert, vereist .NET Framework 4.5.2 of hoger.

- Verleen het **Reporting Services-punt account** de **db_datareader** machtiging voor de Data Warehouse-data base.

- Configuration Manager maakt gebruik van het computer account van de site systeemrol om gegevens te synchroniseren met de Data Warehouse database. Voor dit account zijn de volgende machtigingen vereist:

  - **Beheerder** op de computer die als host fungeert voor de Data Warehouse-data base.

  - **DB_Creator** machtiging voor de Data Warehouse-data base.

  - **DB_owner** of **DB_reader** met machtigingen voor **uitvoeren** voor de data base van de site op het hoogste niveau.

- Het gebruik van SQL Server 2012 of hoger is vereist voor de Data Warehouse-data base. De editie kan Standard, Enter prise of Data Center zijn. De SQL Server-versie voor het Data Warehouse hoeft niet hetzelfde te zijn als de site database server.<!--SCCMDocs issue 662-->

- De Warehouse-data base ondersteunt de volgende SQL Server configuraties:

  - Een standaard-of benoemd exemplaar

  - SQL Server AlwaysOn-beschikbaarheids groep

  - SQL Server-failovercluster

- Als u [gedistribueerde weer gaven](../../plan-design/hierarchy/database-replication.md#bkmk_distviews)gebruikt, installeert u het Data Warehouse-service punt op dezelfde server die als host fungeert voor de data base van de certificerings instantie.

Zie de [Veelgestelde vragen over product en licenties](../../understand/product-and-licensing-faq.md)voor meer informatie over SQL Server-licenties.<!-- sms500967 -->

Het formaat van de Data Warehouse database op dezelfde grootte als uw site database. Hoewel het Data Warehouse op het eerst kleiner is, zal het in de loop van de tijd groeien. <!--SCCMDocs issue 756-->

## <a name="install"></a>Installeren

Elke hiërarchie ondersteunt één exemplaar van deze rol, op elk site systeem van de site op het hoogste niveau. De SQL Server die als host fungeert voor de Data Base voor het magazijn, kan lokaal zijn voor de site systeemrol of extern. Het Data Warehouse werkt met het Reporting Services-punt dat is geïnstalleerd op dezelfde site. U hoeft de twee site systeem rollen niet op dezelfde server te installeren.

Als u de functie wilt installeren, gebruikt u de **wizard site systeem rollen toevoegen** of de **wizard site systeem server maken**. Zie [site systeem rollen installeren](../deploy/configure/install-site-system-roles.md)voor meer informatie. Selecteer de rol **Data Warehouse-service punt** op de pagina **selectie van systeem rollen** van de wizard.

Wanneer u de functie installeert, maakt Configuration Manager de Data Warehouse database voor u op het door u opgegeven exemplaar van SQL Server. Als u de naam van een bestaande data base opgeeft, maakt Configuration Manager geen nieuwe data base. In plaats daarvan wordt de methode gebruikt die u opgeeft. Dit proces is hetzelfde als wanneer u [de Data Warehouse-data base verplaatst naar een nieuwe SQL Server](#move-the-database).

### <a name="configure-properties"></a>Eigenschappen configureren

#### <a name="general-page"></a>Pagina Algemeen

- **SQL Server Fully Qualified Domain name**: Geef de FQDN-naam (Fully Qualified Domain Name) op van de server die als host fungeert voor de Data Warehouse-service punt database.

- **SQL Server exemplaar naam, indien van toepassing**: als u geen standaard exemplaar van SQL Server gebruikt, geeft u het benoemde exemplaar op.

- **Database naam**: Geef een naam op voor de Data Warehouse-data base. Configuration Manager maakt de Data Warehouse-data base met deze naam. Als u een database naam opgeeft die al bestaat op het exemplaar van SQL Server, gebruikt Configuration Manager die data base.

- **SQL Server poort die wordt gebruikt voor de verbinding**: Geef het TCP/IP-poort nummer op dat wordt gebruikt door de SQL Server die als host fungeert voor de Data Warehouse-data base. De Data Warehouse-synchronisatie service gebruikt deze poort om verbinding te maken met de Data Warehouse-data base. SQL Server poort **1433** wordt standaard gebruikt voor communicatie.

- **Account voor Data Warehouse-service punt**: Stel de **gebruikers naam** in die SQL Server Reporting Services gebruikt wanneer verbinding wordt gemaakt met de Data Warehouse database.

#### <a name="synchronization-settings-page"></a>Pagina synchronisatie-instellingen

- **Aangepaste instelling voor gegevens synchronisatie**: Kies de optie voor het **selecteren van tabellen**. Selecteer in het venster database tabellen de tabel namen om te synchroniseren met de Data Warehouse-data base. Gebruik het filter om op naam te zoeken of selecteer de vervolg keuzelijst om specifieke groepen te kiezen. Selecteer **OK** wanneer u klaar bent om op te slaan.

    > [!NOTE]
    > U kunt geen tabellen verwijderen die de rol standaard selecteert.

- **Begin tijd**: Geef het tijdstip op waarop u wilt dat de Data Warehouse-synchronisatie wordt gestart.

- **Terugkeer patroon**

  - **Dagelijks**: Geef op dat synchronisatie elke dag wordt uitgevoerd.

  - **Wekelijks**: Geef één dag per week op en wekelijks terugkeer patroon voor synchronisatie.

## <a name="reporting"></a>Rapportage

Nadat u een Data Warehouse-service punt hebt geïnstalleerd, worden er verschillende rapporten beschikbaar op het Reporting Services-punt voor de site. Als u het Data Warehouse-service punt installeert voordat u een Reporting Services-punt installeert, worden de rapporten automatisch toegevoegd wanneer u later het Reporting Services-punt installeert.

> [!NOTE]
> Het Data Warehouse-punt ondersteunt alternatieve referenties.<!--507334--> Geef referenties op die SQL Server Reporting Services gebruikt om verbinding te maken met de Data Warehouse-data base. Data Warehouse-rapporten worden pas geopend als u referenties hebt toegevoegd.
>
> Als u een account wilt opgeven, stelt u de **gebruikers naam** voor het Data Warehouse-service punt account in de rol eigenschappen in. Zie [eigenschappen configureren](#configure-properties)voor meer informatie.

De Data Warehouse-site systeemrol bevat de volgende rapporten, onder de categorie **Data Warehouse** :

- **Toepassings implementatie-historisch**: Details voor toepassings implementaties voor een specifieke toepassing en computer weer geven.

- **Endpoint Protection en Software Updatenaleving-historisch**: Bekijk computers waarop software-updates ontbreken.

- **Algemene hardware-inventaris: historisch**overzicht van de hardware-inventaris voor een specifieke computer.

- **Algemene software-inventaris-historisch**: alle software-inventaris weer geven voor een specifieke computer.

- **Overzicht van infrastructuur status-historisch**: hier wordt een overzicht weer gegeven van de status van uw Configuration Manager-infra structuur.

- **Lijst met gedetecteerde malware-historisch**: schadelijke software weer geven die in de organisatie is gedetecteerd.

- **Samen vatting van software distributie-historisch**: een samen vatting van software distributie voor een specifieke advertentie en computer.

## <a name="site-expansion"></a>Site-uitbrei ding

Voordat u een certificerings instantie kunt installeren om een bestaande zelfstandige primaire site uit te breiden, moet u eerst de functie Data Warehouse-service punt verwijderen. Nadat u de certificerings instantie hebt geïnstalleerd, kunt u de site systeemrol installeren op de CAS.

In tegens telling tot een verplaatsing van de Data Warehouse-data base resulteert deze wijziging in verlies van de historische gegevens die u eerder hebt gesynchroniseerd op de primaire site. Het wordt niet ondersteund om een back-up van de data base van de primaire site te maken en deze op de CAS te herstellen.

## <a name="move-the-database"></a>De data base verplaatsen

Gebruik de volgende stappen om de Data Warehouse-data base te verplaatsen naar een nieuwe SQL Server:

1. Gebruik SQL Server Management Studio om een back-up te maken van de Data Warehouse-data base. Herstel vervolgens die Data Base naar een SQL Server op de nieuwe computer die als host fungeert voor het Data Warehouse.

    > [!NOTE]
    > Nadat u de Data Base naar de nieuwe server hebt hersteld, moet u ervoor zorgen dat de toegangs machtigingen voor de data base in de nieuwe Data Warehouse-data base gelijk zijn aan die van de oorspronkelijke Data Warehouse-data base.

2. Gebruik de Configuration Manager-console om de rol van het Data Warehouse-service punt te verwijderen van de huidige server.

3. Installeer het Data Warehouse-service punt opnieuw. Geef de naam op van de nieuwe SQL Server en het exemplaar dat als host fungeert voor de herstelde data warehouse-data base.

4. Wanneer de site systeemrol wordt geïnstalleerd, is de verplaatsing voltooid.

## <a name="troubleshoot"></a>Problemen oplossen

### <a name="log-files"></a>Logboekbestanden

Gebruik de volgende logboeken om problemen met de installatie van het Data Warehouse-service punt of de synchronisatie van gegevens te onderzoeken:

- **DWSSMSI. log** en **DWSSSetup. log**: gebruik deze logboeken om fouten te onderzoeken bij het installeren van het Data Warehouse-service punt.

- **Microsoft.ConfigMgrDataWarehouse. log**: dit logboek gebruiken om de gegevens synchronisatie tussen de site database naar de Data Warehouse-data base te onderzoeken.

### <a name="set-up-failure"></a>Fout instellen

Wanneer de rol van het Data Warehouse-service punt de eerste is die u op een externe server installeert, mislukt de installatie voor het Data Warehouse.  

U kunt dit probleem omzeilen door ervoor te zorgen dat de computer waarop u het Data Warehouse-service punt installeert, al als host fungeert voor ten minste één andere rol.

### <a name="synchronization-failed-to-populate-schema-objects"></a>De synchronisatie van schema objecten kan niet worden gevuld

Synchronisatie mislukt met het volgende bericht in **Microsoft.ConfigMgrDataWarehouse. log**:`failed to populate schema objects`

U kunt dit probleem omzeilen door ervoor te zorgen dat het computer account van de site systeemrol een **db_owner** is in de Data Warehouse-data base.

### <a name="reports-fail-to-open"></a>Rapporten kunnen niet worden geopend

Data Warehouse-rapporten kunnen niet worden geopend wanneer de Data Warehouse-data base en het rapportage service punt zich op verschillende site systemen bevinden.

U kunt dit probleem omzeilen door het **account van het Reporting Services-punt** toe te kennen de **db_datareader** machtiging voor de Data Warehouse-data base.

### <a name="error-opening-reports"></a>Fout bij het openen van rapporten

Wanneer u een Data Warehouse-rapport opent, wordt de volgende fout geretourneerd:

``` Output
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

U kunt dit probleem omzeilen door de volgende stappen uit te voeren om certificaten te configureren:

1. Op de server die als host fungeert voor de Data Warehouse-Data Base:

    1. Maak een zelfondertekend certificaat. Open IIS, selecteer **server certificaten**en selecteer vervolgens de actie **zelf ondertekend certificaat maken** . Geef de beschrijvende naam van de certificaat naam op als **Data Warehouse-SQL Server-identificatie certificaat**. Selecteer het certificaat archief als **persoonlijk**.

      > [!TIP]
      > Als deze server nog geen IIS heeft, installeert u deze eerst.

    1. Het certificaat beheren. Open de micro soft Management Console (MMC) en voeg de module **certificaten** toe. Selecteer **computer account** van de lokale machine. Vouw de map **persoonlijk** uit en selecteer **certificaten**.

        1. Geef het SQL Server-service account lees machtigingen voor het certificaat. Selecteer het **Data Warehouse-SQL Server identificatie certificaat** certificaat, ga naar het menu **actie** , selecteer **alle taken**en selecteer **persoonlijke sleutels beheren**. Voeg het SQL Server-service account toe en sta **Lees** toestemming toe.<!-- SCCMDocs#1805 -->

        1. Exporteer het **Data Warehouse-SQL Server identificatie certificaat** als een **der Encoded Binary X. 509 (. CER)-** bestand.

    1. Configureer SQL opnieuw. Open **SQL Server Configuration Manager**.

        1. Klik onder **SQL Server netwerk configuratie**met de rechter muisknop om **Eigenschappen** te selecteren onder **protocollen voor MSSQLSERVER**. Ga naar het tabblad **certificaat** , selecteer **Data Warehouse SQL Server identificatie certificaat** als het certificaat en sla de wijzigingen op.

        1. Start de **SQL Server-service**onder **SQL Server services**opnieuw. Als SQL Reporting Services ook is geïnstalleerd op de server die als host fungeert voor de Data Warehouse-data base, moet u ook **Reporting service** services opnieuw starten.

1. Open de MMC op de server die als host fungeert voor SQL Server Reporting Services en voeg de module **certificaten** toe. Selecteer **computer account**. Importeer in de map **vertrouwde basis certificerings instanties** het **Data Warehouse SQL Server-identificatie certificaat**.

## <a name="data-flow"></a>Gegevensstroom

:::image type="content" source="media/datawarehouse.png" alt-text="Diagram van de logische gegevens stroom tussen site onderdelen voor het Data Warehouse" lightbox="media/datawarehouse.png":::

### <a name="data-storage-and-synchronization"></a>Gegevens opslag en-synchronisatie

| Stap   | Details  |
|--------|----------|
| **1**  | De site server verzendt en slaat gegevens op in de site database. |
| **2**  | Op basis van het schema en de configuratie haalt het Data Warehouse-service punt gegevens op uit de site database. |
| **3**  | Het Data Warehouse-service punt brengt een kopie van de gesynchroniseerde gegevens in de Data Warehouse-Data Base over en slaat deze op. |

### <a name="reporting-flow"></a>Rapport stroom

| Stap   | Details  |
|--------|----------|
| **A**  | Met behulp van ingebouwde rapporten wordt een gebruiker gevraagd om gegevens op te vragen. Deze aanvraag wordt door gegeven aan het Reporting service-punt met behulp van SQL Server Reporting Services. |
| **B**  | De meeste rapporten zijn voor actuele informatie en deze aanvragen worden uitgevoerd op basis van de site database. |
| **C**  | Wanneer een rapport historische gegevens opvraagt met behulp van een van de rapporten met een *categorie* van **Data Warehouse**, wordt de aanvraag uitgevoerd op basis van de Data Warehouse database. |

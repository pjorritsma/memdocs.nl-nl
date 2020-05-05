---
title: SQL Server cluster
titleSuffix: Configuration Manager
description: Een SQL Server-cluster gebruiken om de Configuration Manager-site database te hosten
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d035e6fbd776a03ce38a4cd0fc12755100b60c91
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643253"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Een SQL Server cluster gebruiken voor de site database

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt een SQL Server-failovercluster gebruiken om de Configuration Manager-site database te hosten. Een cluster biedt failover-ondersteuning en verbetert de betrouw baarheid van de site database. Het biedt echter geen aanvullende voor delen voor verwerking of taak verdeling. Daarnaast gebruikt een SQL Server-failovercluster gedeelde opslag en introduceert een Single Point of Failure. Prestatie vermindering kan optreden omdat de site server het actieve knoop punt van het SQL Server cluster moet vinden voordat deze verbinding maakt met de site database.  

> [!IMPORTANT]  
> Geslaagde installatie van SQL Server clusters is afhankelijk van de documentatie en procedures in de documentatie bibliotheek van SQL Server.  


Voordat u Configuration Manager installeert, moet u het SQL Server cluster voorbereiden voor de ondersteuning van Configuration Manager. Zie [een geclusterde SQL Server-instantie voorbereiden](#bkmk_prepare)voor meer informatie.

Tijdens Configuration Manager installatie wordt de Windows Volume Shadow Copy Service Writer geïnstalleerd op elk fysiek computer knooppunt van de micro soft Windows Server-cluster. Deze service biedt ondersteuning voor de onderhouds taak van de **back-upserver van site** .  

Nadat de site is geïnstalleerd, controleert Configuration Manager elk uur op wijzigingen in het cluster knooppunt. Configuration Manager beheert automatisch alle wijzigingen die van invloed zijn op de installatie van de onderdelen. Bijvoorbeeld een failover van een knoop punt of de toevoeging van een nieuw knoop punt aan het SQL Server cluster.  



## <a name="supported-options"></a>Ondersteunde opties

De volgende opties worden ondersteund voor SQL Server-failoverclusters die worden gebruikt als de site database:

- Een cluster met één exemplaar  

- Configuraties met meerdere exemplaren  

- Meerdere actieve knooppunten  

- Zowel een benoemd als een standaard exemplaar  



## <a name="prerequisites"></a>Vereisten

Houd rekening met de volgende vereisten:  

- De sitedatabase mag niet op de siteserver staan. De site systeem server kan niet worden toegevoegd aan het cluster.  

    > [!Note]  
    > Vanaf versie 1810 wordt de installatie van de site serverrol op een computer met de Windows-functie voor failover clustering niet meer geblokkeerd door het installatie proces Configuration Manager. Voorheen kon u de site database op de site server niet vinden. Met deze wijziging kunt u een Maxi maal beschik bare site met minder servers maken met behulp van een SQL-cluster en een site server in de passieve modus. Zie [Opties voor hoge Beschik baarheid](high-availability-options.md)voor meer informatie. <!--3607761, fka 1359132-->  

- Voeg het computer account van de site server toe aan de groep lokale **beheerders** van elke server in het cluster.  

- Als u Kerberos-verificatie wilt ondersteunen, schakelt u het **TCP/IP-** netwerk communicatie protocol in voor de netwerk verbinding van elk SQL Server cluster knooppunt. Het protocol **named pipes** is niet vereist, maar kan worden gebruikt om problemen met Kerberos-verificatie op te lossen. De instellingen voor het netwerk protocol worden geconfigureerd in **SQL Server Configuration Manager**, onder **SQL Server netwerk configuratie**.  

- Er zijn specifieke certificaat vereisten wanneer u een SQL Server cluster gebruikt voor de site database. Raadpleeg voor meer informatie de volgende artikelen:
  - [Een certificaat installeren in een configuratie van een SQL-failovercluster](https://docs.microsoft.com/sql/database-engine/configure-windows/manage-certificates?view=sql-server-ver15#provision-failover-cluster-cert)
  - [PKI-certificaatvereisten voor Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md#BKMK_PKIcertificates_for_servers)

  > [!NOTE]
  > Als u geen certificaat vooraf inricht in SQL, Configuration Manager maakt en richt u een zelfondertekend certificaat voor SQL.<!-- 7099499 -->

## <a name="limitations"></a>Beperkingen

Houd rekening met de volgende beperkingen:  


### <a name="installation-and-configuration"></a>Installatie en configuratie

- Secundaire sites kunnen geen SQL Server cluster gebruiken.  

- Wanneer u een SQL Server cluster opgeeft, is de optie voor het opgeven van niet-standaard bestands locaties voor de site database niet beschikbaar.  


### <a name="sms-provider"></a>SMS-provider

U kunt geen exemplaar van de SMS-provider installeren op een SQL Server-cluster. Het wordt ook niet ondersteund op een computer die wordt uitgevoerd als een geclusterde SQL Server knoop punt.  


### <a name="data-replication-options"></a>Opties voor gegevens replicatie

Als u **gedistribueerde weer gaven**gebruikt, kunt u geen SQL Server-cluster gebruiken om de site database te hosten.  


### <a name="backup-and-recovery"></a>Back-ups maken en herstellen

Configuration Manager biedt geen ondersteuning voor Data Protection Manager (DPM)-back-ups voor een SQL Server cluster dat een benoemd exemplaar gebruikt. Het biedt ondersteuning voor DPM-back-up op een SQL Server-cluster dat gebruikmaakt van het standaard exemplaar van SQL Server.  



## <a name="prepare-a-clustered-sql-server-instance"></a><a name="bkmk_prepare"></a>Een geclusterde SQL Server-instantie voorbereiden  

Hier volgen de belangrijkste taken die u moet uitvoeren om de site database voor te bereiden:

- Maak de virtuele SQL Server-cluster om de sitedatabase te hosten in een bestaande Windows Server-clusteromgeving. Zie de documentatie die specifiek is voor uw versie van SQL Server voor specifieke stappen voor het installeren en instellen van een SQL Server cluster. Zie [een nieuw SQL Server-failovercluster maken](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017)voor meer informatie.  

- Plaats op elke computer in het SQL Server cluster een bestand in de hoofdmap van elk station waar u niet wilt dat Configuration Manager site-onderdelen installeert. Noem het bestand `NO_SMS_ON_DRIVE.SMS`. Configuration Manager installeert standaard sommige onderdelen op elk fysiek knoop punt om bewerkingen zoals back-ups te ondersteunen.  

- Voeg het computer account van de site server toe aan de groep lokale **beheerders** van elke Windows Server-cluster knooppunt computer.  

- Wijs in het virtuele SQL Server-exemplaar de **sysadmin** -SQL Server rol toe aan het gebruikers account dat Configuration Manager Setup uitvoert.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Een nieuwe site installeren met een geclusterde SQL Server  

Als u een site wilt installeren die gebruikmaakt van een geclusterde site database, voert u Configuration Manager Setup uit volgens uw normale proces voor het installeren van een site, met de volgende wijziging:  

- Geef op de pagina **Databasegegevens** de naam op van het virtuele SQL Server-clusterexemplaar waarop de sitedatabase wordt gehost. De naam van de computer waarop SQL Server wordt uitgevoerd, wordt vervangen door het virtuele exemplaar.  

    > [!IMPORTANT]  
    > Wanneer u de naam van de virtuele-SQL Server cluster instantie opgeeft, voert u niet de naam van de virtuele Windows-Server in die is gemaakt door de Windows Server-cluster. Als u de naam van de virtuele Windows-Server gebruikt, wordt de site database geïnstalleerd op de lokale vaste schijf van het actieve Windows Server-cluster knooppunt. Dit heeft tot gevolg dat er geen juiste failover plaatsvindt, als dit knooppunt uitvalt.  

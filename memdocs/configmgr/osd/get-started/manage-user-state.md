---
title: 'De gebruikersstatus beheren '
titleSuffix: Configuration Manager
description: Configuration Manager gebruikt de Hulpprogramma voor migratie van gebruikersstatus om gebruikers status gegevens vast te leggen en te herstellen in implementatie scenario's voor besturings systemen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 70c15fb3a108b22ffacad69d6a67bef3b2d29952
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724074"
---
# <a name="manage-user-state-in-configuration-manager"></a>Gebruikers status beheren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt Configuration Manager taken reeksen gebruiken om de gebruikers status gegevens vast te leggen en te herstellen in implementatie scenario's voor besturings systemen waarin u de gebruikers status van het huidige besturings systeem wilt bewaren. Bijvoorbeeld:  

- Implementaties waarbij u de gebruikersstatus wilt vastleggen van één computer om deze terug te zetten op een andere computer.  

- Werk implementaties bij waarvan u de gebruikersstatus op dezelfde computer wilt vastleggen en herstellen.  

Configuration Manager maakt gebruik van de Hulpprogramma voor migratie van gebruikersstatus (USMT) 10,0 voor het beheren van de migratie van gebruikers status gegevens van een bron computer naar een doel computer nadat de installatie van het besturings systeem is voltooid. Zie  [Algemene migratiescenario's](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios)voor meer informatie over algemene migratiescenario's voor USMT 10.0.

Gebruik de volgende secties om u te helpen bij het vastleggen en herstellen van gebruikers gegevens.

## <a name="store-user-state-data"></a><a name="BKMK_StoringUserData"></a>Gebruikers status gegevens opslaan

 Wanneer u de gebruikersstatus vastlegt, kunt u de gebruikersstatusgegevens opslaan op de doelcomputer of op een statusmigratiepunt. Als u de gebruikers status wilt opslaan op een gebruikers status migratie punt, moet u een Configuration Manager-site systeem server gebruiken die de site systeemrol van het status migratie punt host. U moet, om de gebruikersstatus op de doelcomputer op te slaan, uw takenreeks configureren om de gegevens lokaal op te slaan met behulp van koppelingen.

> [!NOTE]
> De koppelingen die worden gebruikt om de gebruikersstatus lokaal op te slaan, worden vaste koppelingen genoemd. Vaste koppelingen zijn een optie van USMT 10.0 waarmee er op de computer wordt gescand naar gebruikersbestanden en -instellingen en er vervolgens een directory van vaste koppelingen naar die bestanden wordt gemaakt. De vaste koppelingen worden vervolgens gebruikt om de gebruikersgegevens te herstellen na implementatie van het nieuwe besturingssysteem.

> [!IMPORTANT]
> U kunt geen statusmigratie gebruiken en wel vaste koppelingen om de gebruikersstatusgegevens op hetzelfde moment op te slaan.

Als de gebruikersstatusinformatie wordt vastgelegd, kan de informatie op een van de volgende manieren worden opgeslagen:  

- U kunt de gebruikersstatusgegevens extern opslaan door een statusmigratiepunt te configureren. De taken reeks **vastleggen** verzendt de gegevens naar het status migratie punt. Nadat het besturings systeem is geïmplementeerd, haalt de taken reeks **herstellen** de gegevens op en wordt de gebruikers status op de doel computer hersteld.  

- U kunt de gebruikersstatusgegevens lokaal opslaan op een specifieke locatie. In dit scenario kopieert de taken reeks **vastleggen** de gebruikers gegevens naar een specifieke locatie op de doel computer. Nadat het besturings systeem is geïmplementeerd, haalt de taken reeks **herstellen** de gebruikers gegevens op van die locatie.  

- U kunt vaste koppelingen opgeven die kunnen worden gebruikt om de gebruikersgegevens naar de oorspronkelijke locatie te herstellen. In dit scenario blijven de gebruikersstatusgegevens aanwezig op de schijf wanneer het oude besturingssysteem wordt verwijderd. Nadat het nieuwe besturingssysteem vervolgens is geïmplementeerd, worden via de takenreeks **Terugzetten** met de vaste koppelingen de gebruikersstatusgegevens teruggezet op de oorspronkelijke locatie.  

### <a name="store-user-data-on-a-state-migration-point"></a><a name="BKMK_UserDataSMP"></a>Gebruikers gegevens opslaan op een status migratie punt

 Als u de gebruikersstatusgegevens op een statusmigratiepunt wilt opslaan, gaat u als volgt te werk:  

1. [Configure a state migration point](#BKMK_StateMigrationPoint) om de gebruikersstatusgegevens op te slaan.  

1. [Create a computer association](#BKMK_ComputerAssociation) tussen de broncomputer en de doelcomputer. U moet deze koppeling maken voordat u de gebruikersstatus op de broncomputer vastlegt.  

1. [Maak een taken reeks om de gebruikers status vast te leggen en te herstellen](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). U moet met name de volgende taken reeks stappen toevoegen om gebruikers gegevens van een computer vast te leggen, de gebruikers datum op een status migratie punt op te slaan en de gebruikers gegevens op een computer terug te zetten:  

    - [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore) om toegang aan te vragen tot een statusmigratiepunt wanneer u de status van een computer vastlegt of de status terugzet op een computer.  

    - [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) om de gebruiksstatusgegevens vast te leggen en op het statusmigratiepunt op te slaan.  

    - [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) om de gebruiksstatus op de doelcomputer terug te zetten door de gegevens van een gebruikersstatusmigratiepunt op te halen.  

    - [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) om aan het statusmigratiepunt te melden dat het vastleggen of terugzetten is voltooid.  

### <a name="store-user-data-locally"></a><a name="BKMK_UserDataDestination"></a>Gebruikers gegevens lokaal opslaan

 U kunt de gebruikersstatusgegevens als volgt lokaal opslaan:  

- [Maak een taken reeks om de gebruikers status vast te leggen en te herstellen](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). U moet met name de volgende taken reeks stappen toevoegen om gebruikers gegevens van een computer vast te leggen en de gebruikers gegevens op een computer terug te zetten met behulp van vaste koppelingen.

  - [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) om de gebruikersstatusgegevens via vaste koppelingen vast te leggen en op te slaan in een lokale map .  

  - [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) om de gebruiksstatus op de doelcomputer terug te zetten door de gegevens via vaste koppelingen op te halen.  

    > [!NOTE]
    > De gebruikersstatusgegevens waarnaar de vaste koppelingen verwijzen, blijven op de computer nadat de takenreeks het oude besturingssysteem verwijdert. Dit zijn de gegevens die worden gebruikt om de gebruikersstatus op te slaan wanneer het nieuwe besturingssysteem wordt geïmplementeerd.  

## <a name="configure-a-state-migration-point"></a><a name="BKMK_StateMigrationPoint"></a>Een status migratie punt configureren

Op het statusmigratiepunt worden gebruikersstatusgegevens opgeslagen die op de ene computer worden vastgelegd en vervolgens op een andere computer worden hersteld. Wanneer u echter gebruikersinstellingen voor een besturingssysteemimplementatie op dezelfde computer vastlegt, zoals een implementatie waarbij u het besturingssysteem op de doelcomputer vernieuwt, kunt u de gegevens opslaan op dezelfde computer via vaste koppelingen of op een statusmigratiepunt. Bij sommige computer implementaties maakt Configuration Manager automatisch een koppeling tussen het status archief en de doel computer wanneer u de status opslag maakt. U kunt de volgende methoden gebruiken om een statusmigratiepunt te configureren om de gebruikersstatusgegevens op te slaan:  

- Gebruik de **wizard Sitesysteemserver maken** om een nieuwe sitesysteemserver te maken voor het statusmigratiepunt.  

- Gebruik de **wizard Sitesysteemrollen toevoegen** om een statusmigratiepunt toe te voegen aan een bestaande server.  

  Als u deze wizards gebruikt, wordt u gevraagd om de volgende informatie op te geven voor het statusmigratiepunt:  

- De mappen voor het opslaan van de gebruikersstatusgegevens.  

- Het maximum aantal clients die gegevens op het statusmigratiepunt kunnen opslaan.  

- De minimale hoeveelheid vrije schijfruimte voor het statusmigratiepunt om gebruikersstatusgegevens op te slaan.  

- Het verwijderingsbeleid voor de rol. U kunt opgeven dat de gebruikersstatusgegevens onmiddellijk worden verwijderd nadat ze op een computer zijn hersteld, of na een specifiek aantal dagen nadat de gebruikersgegevens op een computer worden hersteld.  

- Of het statusmigratiepunt alleen moet reageren op aanvragen om gebruikersstatusgegevens terug te zetten. Wanneer u deze optie inschakelt, kunt het statusmigratiepunt niet gebruiken om de gebruikersstatusgegevens op te slaan.  

  Zie [State migration point](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)voor meer informatie over het statusmigratiepunt en de stappen om dit te configureren.  

## <a name="create-a-computer-association"></a><a name="BKMK_ComputerAssociation"></a> Create a computer association

Maak een computerkoppeling om een relatie te definiëren tussen een broncomputer en een doelcomputer wanneer u een besturingssysteem op nieuwe hardware installeert en gebruikersgegevensinstellingen wilt vastleggen en terugzetten. De bron computer is een bestaande computer die Configuration Manager beheerd. Wanneer u het nieuwe besturingssysteem implementeert op de doelcomputer, bevat de broncomputer de gebruikersstatus die is gemigreerd naar de doelcomputer.  

> [!NOTE]  
> Het is niet mogelijk om een computer koppeling te maken tussen computers die zich in een Configuration Manager bovenliggende site bevinden met computers die zich in een onderliggende site bevinden. Computer koppelingen zijn site-specifiek en worden niet gerepliceerd.  

### <a name="to-create-a-computer-association"></a>Een computerkoppeling maken

1. Klik op **Activa en naleving**op de Configuration Manager-console.  

1. Klik op **Gebruikersstatusmigratie** in de werkruimte **Activa en naleving**.  

1. Klik op **Computerkoppeling maken** in het tabblad **Start** in de groep **Maken**.  

1. Geef, op het tabblad **Computerkoppeling** van het dialoogvenster **Eigenschappen computerkoppeling** de broncomputer op met de te vastleggen gebruikersstatus; geef ook de doelcomputer op waarop de gebruikersstatusgegevens moeten worden hersteld.  

1. Geef, op het tabblad **Gebruikersaccounts** , de gebruikersaccounts op die moeten worden gemigreerd naar de doelcomputer. Geef een van de volgende instellingen op:  

    - **Alle gebruikersaccounts vastleggen en herstellen**: met deze instelling worden alle gebruikersaccount vastgelegd en hersteld. Gebruik deze instelling om meerdere koppelingen te maken op dezelfde broncomputer.  

    - **Alle gebruikersaccounts vastleggen en opgegeven accounts herstellen**: met deze instelling worden alle gebruikersaccounts op de broncomputer vastgelegd en worden alleen de door u opgegeven accounts op de doelcomputer hersteld. Bovendien kunt u deze instelling gebruiken wanneer u meervoudige koppelingen op dezelfde broncomputer wilt maken.  

    - **Opgegeven gebruikersaccounts vastleggen en herstellen**: met deze instelling worden alleen de accounts die u opgeeft, vastgelegd en hersteld. U kunt geen meervoudige koppelingen naar dezelfde broncomputer maken wanneer u deze instelling selecteert.  

## <a name="restore-user-state-data-when-an-operating-system-deployment-fails"></a><a name="BKMK_MigrationFails"></a> Gebruikersstatusgegevens terugzetten wanneer een besturingssysteemimplementatie mislukt

Als de implementatie van het besturingssysteem mislukt, kunt u met de functie USMT 10.0 LoadState de gebruikersstatusgegevens ophalen die zijn vastgelegd tijdens de implementatie. Hiertoe behoren ook gegevens die op een statusmigratiepunt zijn opgeslagen en gegevens die lokaal op de doelcomputer zijn opgeslagen. Zie [LoadState Syntax (LoadState-syntax)](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax)voor meer informatie over deze USMT-functie.

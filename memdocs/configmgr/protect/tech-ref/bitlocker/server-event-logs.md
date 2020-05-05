---
title: Servergebeurtenislogboeken
titleSuffix: Configuration Manager
description: Technische Naslag informatie over de mogelijke BitLocker (MBAM)-server vermeldingen in het Windows-gebeurtenis logboek
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d49a24b6fea08f12d1fe70c1e0b7415adf98719
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074806"
---
# <a name="server-event-logs"></a>Servergebeurtenislogboeken

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3601034-->

Gebruik de Windows-Logboeken om gebeurtenis logboeken weer te geven voor de volgende onderdelen van de BitLocker-beheer server in Configuration Manager:

- Herstel service op het beheer punt
- Selfservice portal
- Website voor beheer en controle

Open de Logboeken op een server die als host fungeert voor een of meer van deze onderdelen. Ga vervolgens naar **Logboeken voor toepassingen en services**, **micro soft**, **Windows**en vouw **MBAM-Web**uit. Standaard zijn er [beheer](#admin) -en [operationele](#operational) gebeurtenis Logboeken.

De volgende secties bevatten berichten en informatie voor het oplossen van problemen met gebeurtenis-Id's die kunnen optreden met de onderdelen van de BitLocker-beheer server.

## <a name="admin"></a>Beheerder

### <a name="1-webappspnerror"></a>1: WebAppSpnError

Voor de toepassing {VirtualDirectory} ontbreken de volgende Spn's (Service Principal Names): {ListOfSpns} Registreer de vereiste Spn's voor het account: {ExecutionAccount}.

Geïntegreerde Windows-verificatie is alleen mogelijk als de benodigde Spn's aanwezig zijn. Dit bericht geeft aan dat de SPN die vereist is voor de toepassing, niet juist is geconfigureerd. In deze gebeurtenis vindt u meer informatie over de details.

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100: AdminServiceRecoveryDbError

Mogelijke fout berichten:

- GetMachineUsers: er is een fout opgetreden tijdens het ophalen van gebruikers informatie uit de data base.
- GetRecoveryKey: er is een fout opgetreden tijdens het ophalen van de herstel sleutel van de data base.
- GetRecoveryKey: er is een fout opgetreden tijdens het ophalen van gebruikers informatie uit de data base.
- GetRecoveryKeyIds: er is een fout opgetreden tijdens het ophalen van herstel sleutel-Id's uit de data base.
- GetTpmHashForUser: er is een fout opgetreden tijdens het ophalen van TPM-hash-gegevens uit de herstel database.
- GetTpmHashForUser: er is een fout opgetreden tijdens het ophalen van TPM-hash-gegevens uit de herstel database.
- QueryDriveRecoveryData: er is een fout opgetreden tijdens het ophalen van gegevens voor het herstel van stations vanuit de data base.
- QueryRecoveryKeyIdsForUser: er is een fout opgetreden tijdens het ophalen van herstel sleutel-Id's uit de data base.
- QueryVolumeUsers: er is een fout opgetreden tijdens het ophalen van gebruikers informatie uit de data base.

Dit bericht wordt geregistreerd wanneer er een uitzonde ring is opgetreden tijdens de communicatie met de herstel database. Lees de informatie in de tracering om specifieke informatie over de uitzonde ring op te halen.

### <a name="101-adminservicecompliancedberror"></a>101: AdminServiceComplianceDbError

Mogelijke fout berichten:

- GetRecoveryKey: er is een fout opgetreden tijdens het vastleggen van een controle gebeurtenis aan de nalevings database.
- GetRecoveryKeyIds: er is een fout opgetreden tijdens het vastleggen van een controle gebeurtenis aan de nalevings database.
- GetTpmHashForUser: er is een fout opgetreden tijdens het vastleggen van een controle gebeurtenis aan de nalevings database.
- QueryRecoveryKeyIdsForUser: er is een fout opgetreden tijdens het vastleggen van een controle gebeurtenis aan de nalevings database.
- QueryDriveRecoveryData: er is een fout opgetreden tijdens het vastleggen van een controle gebeurtenis aan de nalevings database.

Dit bericht wordt geregistreerd wanneer er een uitzonde ring is opgetreden tijdens de communicatie met de nalevings database. Lees de informatie in de tracering om specifieke informatie over de uitzonde ring op te halen.

### <a name="102-agentservicerecoverydberror"></a>102: AgentServiceRecoveryDbError

Dit bericht geeft een uitzonde ring aan wanneer de service probeert te communiceren met de herstel database. Lees het bericht dat in de gebeurtenis is opgenomen om specifieke informatie over de uitzonde ring op te halen.

Controleer of het MBAM-account van de app-groep de vereiste machtigingen heeft om verbinding te maken met de herstel database.

### <a name="103-agentserviceerror"></a>103: AgentServiceError

Mogelijke fout berichten:

- Kan het gebruikers account voor de client computer of de gegevens migratie niet detecteren.

    Wanneer een aanroep wordt gedaan aan de `PostKeyRecoveryInfo`- `IsRecoveryKeyResetRequired` `CommitRecoveryKeyRest`,-of `GetTpmHash` -webmethode, wordt de context van de aanroeper opgehaald om de aanroeper-referenties te verkrijgen. Als de aanroeper-context null of leeg is, wordt dit bericht door de service geregistreerd.

- Account verificatie is mislukt voor de identiteit van de aanroeper.

    Dit bericht wordt vastgelegd als de webmethode verwacht dat de aanroeper een computer account is en dat niet. Dit kan ook worden veroorzaakt als de webmethode verwacht dat de beller een gebruikers account is en het geen gebruikers account of een lid van een groeps account voor gegevens migratie is.

### <a name="104-statusservicecompliancedbconfigerror"></a>104: StatusServiceComplianceDbConfigError

De connection string van de nalevings database in het REGI ster is leeg.

Dit bericht wordt vastgelegd wanneer het connection string van de nalevings database ongeldig is. Controleer de waarde bij de register sleutel `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`.

### <a name="105-statusservicecompliancedberror"></a>105: StatusServiceComplianceDbError

Deze fout geeft aan dat de websites of webservices geen verbinding kunnen maken met de nalevings database. Controleer of het IIS-app-groeps account verbinding kan maken met de data base.

### <a name="106-helpdeskerror"></a>106: HelpdeskError

Bekende fouten en mogelijke oorzaken:

- De aanvraag voor de URL heeft een interne fout veroorzaakt.

    Er is een onverwerkte uitzonde ring opgetreden in de toepassing voor de beheer-en bewakings website (helpdesk). Controleer de logboek vermeldingen in het gebeurtenis logboek van de **beheerder** om de specifieke uitzonde ring te vinden.

- Er is een fout opgetreden tijdens het ophalen van de uitvoerings context gegevens. Kan de registratie van de service principal name (SPN) niet controleren.

    Tijdens de eerste laad bewerking van de helpdesk website wordt de SPN gecontroleerd. Als u de SPN wilt controleren, hebt u account gegevens, IIS-site naam en ApplicationVirtualPath nodig die overeenkomen met de Help Desk-website. Dit fout bericht wordt geregistreerd wanneer een of meer van deze kenmerken ongeldig of ontbreken.

- Er is een fout opgetreden tijdens het controleren van de registratie van de SPN (Service Principal Name).

    Dit bericht geeft aan dat er een beveiligings uitzondering wordt gegenereerd bij het controleren van de SPN. Raadpleeg de uitzonde ring die is opgenomen in de details van de gebeurtenis.

### <a name="107-selfserviceportalerror"></a>107: SelfServicePortalError

Bekende fouten en mogelijke oorzaken:

- Er is een fout opgetreden tijdens het ophalen van de herstel sleutel voor een gebruiker

    Geeft aan dat er een onverwachte uitzonde ring is opgetreden tijdens het ophalen van een herstel sleutel. Raadpleeg het uitzonderings bericht in de gebeurtenis Details. Als tracering is ingeschakeld voor de Help Desk-app, raadpleegt u tracerings gegevens om gedetailleerde uitzonderings berichten te verkrijgen.

- Er is een fout opgetreden tijdens het ophalen van de uitvoerings context gegevens. Kan de registratie van de service principal name (SPN) niet verifiëren

    Tijdens een initiële laad bewerking haalt de Self-Service Portal account gegevens, IIS-site naam en ApplicationVirtualPath op voor de selfservice website om de SPN te verifiëren. Dit fout bericht wordt geregistreerd wanneer een of meer van deze kenmerken ongeldig zijn.

- Er is een fout opgetreden tijdens het controleren van de registratie van de SPN (Service Principal Name). EventDetails: {ExceptionMessage}

    Dit bericht geeft aan dat er een beveiligings uitzondering is opgetreden tijdens het controleren van de SPN. Raadpleeg de uitzonde ring die is opgenomen in de details van de gebeurtenis.

### <a name="108-domaincontrollererror"></a>108: DomainControllerError

Bekende fouten en mogelijke oorzaken:

- Er is een fout opgetreden tijdens het omzetten van de domein naam {DomainName}. er is een geheugen toewijzings fout opgetreden.

    De Windows-API wordt aangeroepen om de `DsGetDcName` domein naam op te lossen. Dit bericht wordt geregistreerd wanneer deze API retourneert `ERROR_NOT_ENOUGH_MEMORY`, wat aangeeft dat er een geheugen toewijzing is mislukt.

- Kan de DsGetDcName-methode niet aanroepen

    Dit bericht geeft aan dat `DsGetDcName` de API niet beschikbaar is op de host.

### <a name="109-webapprecoverydberror"></a>109: WebAppRecoveryDbError

Bekende fouten en mogelijke oorzaken:

- Er is een fout opgetreden tijdens het lezen van de configuratie van de herstel database. Het connection string naar de herstel database is niet geconfigureerd.

    Dit bericht geeft aan dat de gegevens van de `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` herstel database connection string op ongeldig zijn. Controleer de opgegeven register sleutel waarde.

Als u een van de volgende berichten ziet, controleert u of de referenties van de groep van toepassingen van de IIS-server verbinding kunnen maken met de herstel database:

- DoesUserHaveMatchingRecoveryKey: er is een fout opgetreden tijdens het ophalen van de herstel sleutel-Id's voor een gebruiker.
- QueryDriveRecoveryData: er is een fout opgetreden tijdens het ophalen van gegevens voor station Recovery.
- QueryRecoveryKeyIdsForUser: er is een fout opgetreden tijdens het ophalen van de herstel sleutel-Id's voor een gebruiker.
- Er is een fout opgetreden tijdens het ophalen van de TPM-wachtwoord-hash van de herstel database.

### <a name="110-webappcompliancedberror"></a>110: WebAppComplianceDbError

Bekende fouten en mogelijke oorzaken:

- Er is een fout opgetreden tijdens het lezen van de configuratie van de nalevings database. De connection string voor de nalevings database is niet geconfigureerd.

    Dit bericht geeft aan dat de gegevens van de `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` nalevings database connection string op ongeldig zijn. Controleer de waarde van deze register sleutel.

Als u een van de volgende berichten ziet, controleert u of de referenties van de groep van toepassingen van de IIS-server verbinding kunnen maken met de nalevings database:

- GetRecoveryKeyForCurrentUser: er is een fout opgetreden tijdens het vastleggen van een controle gebeurtenis aan de nalevings database.
- QueryRecoveryKeyIdsForUser: er is een fout opgetreden tijdens het vastleggen van een controle gebeurtenis aan de nalevings database.
- QueryRecoveryKeyIdsForUser: er is een fout opgetreden tijdens het vastleggen van een controle gebeurtenis aan de nalevings database.

### <a name="111-webappdberror"></a>111: WebAppDbError

Deze fouten duiden op een van de volgende twee voor waarden

- MBAM websites/webservices kunnen geen verbinding maken met de compatibiliteits-of herstel database
- MBAM websites/webservices-uitvoerings account (account voor de groep van toepassingen `GetVersion` ) kan de opgeslagen procedure niet uitvoeren voor de nalevings-of herstel database

In het bericht dat in de gebeurtenis is opgenomen, vindt u meer informatie over de uitzonde ring.

Controleer of het groeps account van de app verbinding kan maken met de data bases voor naleving of herstel. Controleer of het machtigingen heeft om de `GetVersion` opgeslagen procedure uit te voeren.

### <a name="112-webapperror"></a>112: WebAppError

Er is een fout opgetreden tijdens het controleren van de registratie van de SPN (Service Principal Name).

Om de SPN te verifiëren, vraagt de IT Active Directory om een lijst op te halen met het uitvoerings account voor Spn's toegewezen. Er wordt ook een `ApplicationHost.config` query uitgevoerd op de om de website bindingen op te halen. Dit fout bericht geeft aan dat er niet kan worden gecommuniceerd met Active Directory of `ApplicationHost.config` dat het bestand niet kan worden geladen.

Controleer of het app-groeps account machtigingen heeft om Active Directory of `ApplicationHost.config` het bestand te zoeken. Controleer ook de vermeldingen van de site binding `ApplicationHost.config` in het bestand.

## <a name="operational"></a>Functioneren

### <a name="4-performancecountererror"></a>4: PerformanceCounterError

Er is een fout opgetreden tijdens het ophalen van een prestatie meter item.

Het tracerings bericht bevat het werkelijke uitzonderings bericht, sommige worden hier weer gegeven:

- ArgumentNullException: Deze uitzonde ring wordt gegenereerd als de categorie, teller of exemplaar van het aangevraagde prestatie meter item ongeldig is.
- System. InvalidOperationException: categoryName is een lege teken reeks (""). CounterName is een lege teken reeks ("").
- De aangevraagde lees-/schrijfmachtigingen is ongeldig voor deze teller.
- De opgegeven categorie bestaat niet (als alleen-lezen is ingesteld op True).
- De opgegeven categorie is geen .NET Framework aangepaste categorie (als alleen-lezen is ingesteld op false).
- De opgegeven categorie is gemarkeerd als meerdere exemplaren en vereist dat het prestatie meter item wordt gemaakt met een exemplaar naam.
- INSTANCENAME is langer dan 127 tekens.
- categoryName en CounterName zijn gelokaliseerd in verschillende talen.
- System. ComponentModel. Win32Exception: er is een fout opgetreden bij het openen van een systeem-API.
- System. UnauthorizedAccessException: code die wordt uitgevoerd zonder beheerders bevoegdheden heeft geprobeerd een prestatie meter item te lezen.

In het bericht in de gebeurtenis vindt u meer informatie over de uitzonde ring.

Controleer voor `System.UnauthorizedAccessException`de of het app-groeps account toegang heeft tot api's voor prestatie meter items.

### <a name="200-helpdeskinformation"></a>200: HelpDeskInformation

De beheer website toepassing is gevonden en verbonden met een ondersteunde versie van de Data Base voor herstel/naleving.

Geeft een geslaagde verbinding tot stand met de herstel-of nalevings database van de Help Desk-website.

### <a name="201-selfserviceportalinformation"></a>201: SelfServicePortalInformation

De Self-Service Portal-toepassing is gevonden en verbonden met een ondersteunde versie van de Data Base voor herstel/naleving.

Geeft een geslaagde verbinding tot stand met de herstel-of nalevings database van de selfservice Portal.

### <a name="202-webappinformation"></a>202: WebAppInformation

De Spn's van de toepassing zijn op de juiste manier geregistreerd.

Geeft aan dat de Spn's die vereist zijn voor de Help Desk-website correct zijn geregistreerd voor het account dat wordt uitgevoerd.

## <a name="see-also"></a>Zie ook

Zie [BitLocker-gebeurtenis logboeken](about-event-logs.md)voor meer informatie over het gebruik van deze logboeken.

Zie [problemen met BitLocker oplossen](troubleshoot.md)voor meer informatie over probleem oplossing.

Zie [BitLocker-rapporten en-portals instellen](../../deploy-use/bitlocker/setup-websites.md)voor meer informatie over het installeren van deze websites.

---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/13/2020
ms.openlocfilehash: 8e95fce122a3e153f2aa391dcd5e40439f8e5820
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88702967"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>Query's

Query's kunnen worden gebruikt om termen te zoeken, trends te identificeren, patronen te analyseren en veel andere inzichten te bieden op basis van uw gegevens. CMPivot maakt gebruik van een subset van het [Azure log Analytics](/azure/kusto/query) -gegevens stroom model voor de tabellaire expressie-instructie. De typische structuur van een tabellaire expressie-instructie is een samen stelling van client entiteiten en tabellaire gegevens operators (zoals filters en projecties). De samen stelling wordt vertegenwoordigd door het sluis teken (|), waarbij de instructie een gewone vorm heeft die de stroom van gegevens in tabel vorm visueel van links naar rechts vertegenwoordigt. Elke operator accepteert een tabellaire gegevensset van de pipe en extra invoer (inclusief andere tabellaire gegevens sets) van de hoofd tekst van de operator. vervolgens wordt er een tabellaire gegevensset met de volgende-operator ingesteld die volgt: `entity | operator1 | operator2 | ...`

In het volgende voor beeld is de entiteit `CCMRecentlyUsedApplications` (een verwijzing naar de recent gebruikte toepassingen) en de operator is waar (die records uit de invoer uitfiltert op basis van een predikaat per record):

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%' | project CompanyName, ExplorerFileName, LastUsedTime, LaunchCount, FolderPath
```

## <a name="entities"></a>Entiteiten

Entiteiten zijn objecten die kunnen worden opgevraagd van de client. Momenteel worden de volgende entiteiten ondersteund:


|Entiteit|Beschrijving|
|---|---|
|AadStatus|Status van Azure Active Directory|
|Beheerders|Leden van de lokale groep Administrators|
|AppCrash|Recente toepassings crash rapporten|
|AppVClientApplication|AppV-client toepassing|
|AppVClientPackage|AppV-client pakket|
|AutoStartSoftware|Software die automatisch wordt gestart met of direct na het besturings systeem|
|Kaart|Kaart|
|Accu|Accu|
|Beschikt|Informatie over het systeem-BIOS|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|BitLocker-versleutelings Details|
|BitLockerPolicy|BitLocker-beleid|
|BootConfiguration|Opstart configuratie|
|BrowserHelperObject|Browser helper-object|
|BrowserUsage|Browser gebruik|
|CcmLog()|Regels binnen 24 uur (standaard) vanuit een CCM-logboek bestand|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|Recent gebruikte toepassingen|
|CCMWebAppInstallInfo|Webtoepassingen|
|STATION|CD-romstation|
|ClientEvents|Client gebeurtenissen|
|Computer System|Computersysteem|
|ComputerSystemEx|Computer systeem ex|
|ComputerSystemProduct|Computer systeem product|
|ConnectedDevice|Verbonden apparaat|
|Verbinding|Een actieve TCP-verbinding in of uit het apparaat|
|Desktop|Desktop|
|DesktopMonitor|Bureaublad monitor|
|Apparaat|Algemene informatie over het apparaat|
|Schijf|Gegevens van het lokale opslag apparaat op een computer waarop Windows wordt uitgevoerd|
|DMA|DMA|
|DMAChannel|DMA-kanaal|
|DriverVxD|Stuur programma-VxD|
|EmbeddedDeviceInformation|Informatie over Inge sloten apparaat|
|Omgeving|Omgeving|
|EPStatus|Status van de antimalware-software op de computer|
|EventLog ()|Gebeurtenissen binnen 24 uur (standaard) vanuit een gebeurtenis logboek|
|Bestand ()|Informatie over een specifiek bestand|
|Bestandsshare|Informatie over de actieve bestands share|
|Firmware|Firmware|
|IDEController|IDE-controller|
|InstalledExecutable|Geïnstalleerd uitvoerbaar bestand|
|InstalledSoftware|Een toepassing die op het apparaat is geïnstalleerd|
|IP|Hiermee wordt de netwerk configuratie opgehaald, met inbegrip van bruikbare interfaces, IP-adressen en DNS-servers|
|IRQTable|IRQ-tabel|
|Toetsenbord|Toetsenbord|
|LoadOrderGroup|Volgorde groep laden|
|LogicalDisk|Logische schijf|
|MDMDevDetail|Apparaatgegevens|
|Geheugen|Geheugen|
|Nulmodem|Nulmodem|
|Beschikt|Beschikt|
|Netwerk adapter|Netwerk adapter|
|NetworkAdapterConfiguration|Configuratie van netwerk adapter|
|NetworkClient|Netwerkclient|
|NetworkLoginProfile|Aanmeldings profiel voor netwerk|
|NTEventlogFile|NT-gebeurtenis logboek bestand|
|Office365ProPlusConfigurations|Office 365 ProPlus-configuraties|
|OfficeAddin|Office-invoeg toepassingen|
|OfficeClientMetric|Metrische Office-client|
|OfficeDeviceSummary|Overzicht van Office-apparaten|
|OfficeDocumentMetric|Metrische gegevens van Office-document|
|OfficeDocumentSolution|Office-document oplossing|
|OfficeMacroError|Office-macro fout|
|OfficeProductInfo|Office-product informatie|
|OfficeVbaRuleViolation|Schending Office VBA-regel|
|OfficeVbaSummary|Overzicht van Office VBA-scans|
|OperatingSystem|Besturingssysteem|
|OperatingSystemEx|Besturings systeem ex|
|OperatingSystemRecoveryConfiguration|Configuratie van het besturings systeem herstellen|
|OptionalFeature|Optionele functie|
|Besturingssysteem|Basis informatie over het besturings systeem|
|PageFileSetting|Instelling voor pagina bestand|
|ParallelPort|Parallelle poort|
|Partitie|Schijf partities|
|PCMCIAController|PCMCIA-controller|
|PhysicalDisk|PhysicalDisk|
|PhysicalMemory|Fysiek geheugen|
|PNPDEVICEDRIVER|PNP-apparaatstuurprogramma|
|PointingDevice|Aanwijs apparaat|
|PortableBattery|Draag bare batterij|
|Poorten|Poorten|
|PowerCapabilities|Energie mogelijkheden|
|PowerClientOptOutSettings|Instellingen voor uitzonde ring energie beheer|
|PowerConfigurations|Energie configuratie|
|PowerManagementDaily|Dagelijkse gegevens energie beheer|
|PowerManagementInsomniaReasons|Redenen voor energie slapeloosheid|
|PowerManagementMonthly|Maandelijkse gegevens voor energie beheer|
|PowerSettings|Energie-instellingen|
|PrinterConfiguration|Printer configuratie|
|PrinterDevice|Printer apparaat|
|PrintJobs|Afdruk taken|
|Proces|Een proces op een besturings systeem|
|ProcessModule()|Modules geladen door opgegeven processen|
|Processor|Processor|
|ProtectedVolumeInformation|Gegevens van beveiligd volume|
|Protocol|Protocol|
|QuickFixEngineering|Quick Fix Engineering|
|SCSIController|SCSI-controller|
|SerialPortConfiguration|Configuratie van seriële poort|
|SerialPorts|Seriële poorten|
|ServerFeature|Serverfunctie|
|Service|Een service op een computer waarop Windows wordt uitgevoerd|
|Services|Services|
|Shares|Shares|
|SMBConfig|SMB-configuratie van een apparaat|
|SMSAdvancedClientPorts|Client poorten Configuration Manager|
|SMSAdvancedClientSSLConfigurations|SSL-configuraties van Configuration Manager-client|
|SMSAdvancedClientState|Status van Configuration Manager-client|
|SMSDefaultBrowser|Standaard browser|
|SMSSoftwareTag|Software label|
|SMSWindows8Application|Windows-app|
|SMSWindows8ApplicationUserInfo|Gebruikers gegevens voor Windows-apps|
|SoftwareShortcut|Software snelkoppeling|
|SoftwareUpdate|Een software-update die van toepassing is op het apparaat, maar niet is geïnstalleerd|
|SoundDevices|Geluids apparaten|
|SWLicensingProduct|Software licentie product|
|SWLicensingService|Software Licensing-service|
|SystemAccount|Systeemaccount|
|SystemBootData|Opstart gegevens van het systeem|
|SystemBootSummary|Samen vatting van systeem opstarten|
|SystemConsoleUsage|Gebruik van systeem console|
|SystemConsoleUser|Gebruiker van systeem console|
|SystemDevices|Systeem apparaten|
|Systeem eigen|Systeem Stuur Programma's|
|SystemEnclosure|Systeembehuizing|
|TapeDrive|Tape station|
|Tijdzone|Tijdzone|
|TPM|TPM|
|TPMStatus|TPM-status|
|TSIssuedLicense|Uitgegeven TS-licentie|
|TSLicenseKeyPack|TS-licentie sleutel pakket|
|UninterruptiblePowerSupply|Uninterruptible Power Supply|
|USBController|USB-controller|
|USBDevice|USB-apparaat|
|Gebruiker|Een gebruikers account met een actieve verbinding met het apparaat|
|USMFolderRedirectionHealth|Status Mapomleiding|
|USMUserProfile|Status van gebruikers profiel|
|VideoController|Video controller|
|VirtualMachine|Virtuele machine|
|VirtualMachine64|Virtuele machine (64)|
|Volume|Volume|
|WindowsUpdate|Windows Update|
|WindowsUpdateAgentVersion|Versie van Windows Update Agent|
|Wine vent ()|Gebeurtenissen binnen 24 uur (standaard) van een Windows-gebeurtenis logboek|
|WriteFilterState|Status van schrijf filter|

## <a name="table-operators"></a>Tabel operators

U kunt tabel operators gebruiken om gegevens stromen te filteren, samen te vatten en te transformeren. Momenteel worden de volgende Opera tors ondersteund:

|Tabel operators|Beschrijving|
|---|---|
|count|Retourneert een tabel met één record die het aantal records bevat|
|distinct|Produceert een tabel met de unieke combi natie van de opgegeven kolommen van de invoer tabel|
|join|De rijen van twee tabellen samen voegen om een nieuwe tabel te vormen door overeenkomende rij voor hetzelfde apparaat te zoeken|
|sorteren op|Sorteer de rijen van de invoer tabel in volg orde van een of meer kolommen|
|project|De kolommen selecteren die u wilt opnemen, de naam ervan wijzigen of verwijderen, en nieuwe berekende kolommen invoegen|
|samenvatten|Hiermee wordt een tabel gegenereerd waarin de inhoud van de invoer tabel wordt geaggregeerd|
|take|Naar het opgegeven aantal rijen retour neren|
|top|Retourneert de eerste N records gesorteerd op de opgegeven kolommen|
|waar|Hiermee wordt een tabel gefilterd op de subset rijen die voldoen aan een predikaat|

## <a name="scalar-operators"></a>Scalaire Opera tors

De volgende tabel bevat een overzicht van Opera tors:

|Operators|Beschrijving|Voorbeeld
|---|---|---|
|==|Is gelijk aan|`1 == 1, 'aBc' == 'AbC'`|
|!=|Niet gelijk aan|`1 != 2, 'abc' != 'abcd'`|
|< |Jonge|`1 < 2, 'abc' < 'DEF'`|
|> |Groter|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Kleiner of gelijk aan|`1 <= 2, 'abc' <= 'abc'`|
|>=|Groter of gelijk aan|`2 >= 1, 'abc' >= 'ABC'`|
|+|Toevoegen|`2 + 1, now() + 1d`|
|-|Aftrekken|`2 - 1, now() - 1h`|
|*|Vermenigvuldigen|`2 * 2`|
|/|Delen|`2 / 1`|
|%|Modulo|`2 % 1`|
|zo|Aan de linkerkant (LHS) bevat een overeenkomst voor de rechter kant (RHS)|`'abc' like '%B%'`|
|! like|LHS bevat geen overeenkomst voor RHS|`'abc' !like '_d_'`|
|contains|RHS treedt op als een subreeks van LHS|`'abc' contains 'b'`|
|! bevat|RHS vindt niet plaats in LHS|`'team' !contains 'i'`|
|startsWith|RHS is een initiële subreeks van LHS|`'team' startswith 'tea'`|
|! startsWith|RHS is geen initiële subreeks van LHS|`'abc' !startswith 'bc'`|
|endswith|RHS is een subreeks van LHS|`'abc' endswith 'bc'`|
|! endswith|RHS is geen afsluitende subreeks van LHS|`'abc' !endswith 'a'`|
|en|Waar als en alleen als RHS en LHS True zijn|`(1 == 1) and (2 == 2)`|
|of|Waar als en alleen als RHS of LHS True is|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>Aggregatiefuncties

Aggregatie functies kunnen met de operator tabel samenvatten worden gebruikt voor berekende samenvattings waarden. Momenteel worden de volgende aggregatie functies ondersteund:

|Functie|Beschrijving|
|---|---|
|avg()|Hiermee wordt het gemiddelde van de waarden in de groep geretourneerd|
|count()|Hiermee wordt het aantal records per samenvattings groep geretourneerd|
|countif()|Retourneert het aantal rijen waarvoor het predicaat resulteert in waar|
|dcount()|Hiermee wordt het aantal afzonderlijke waarden in de groep geretourneerd|
|max()|Retourneert de maximum waarde voor de hele groep|
|min()|Retourneert de minimum waarde voor de hele groep|
|percentiel ()|Retourneert een schatting voor het opgegeven dichtstbijzijnde-positie percentiel van de populatie die is gedefinieerd met expr|
|sum()|Retourneert de som van de waarden in de groep|
|sumif()|Retourneert een som van de expr waarvoor het predicaat resulteert in waar|

## <a name="scalar-functions"></a>Scalaire functies

Scalaire functies kunnen worden gebruikt in expressies. Momenteel worden de volgende scalaire functies ondersteund:

|Functie|Beschrijving|
|---|---|
|ago()|Trekt de opgegeven time span af van de huidige UTC-klok tijd|
|bin()|Rondt waarden af naar een aantal datetime-veelvoud van een bepaalde opslaglocatie grootte|
|case()|Evalueert een lijst met predikaten en retourneert de eerste resultaat expressie waarvan het predicaat is voldaan|
|datetime_add()|Hiermee wordt een nieuwe datum/tijd berekend op basis van een opgegeven date Part vermenigvuldigd met een opgegeven aantal, toegevoegd aan een opgegeven datum/tijd|
|datetime_diff()|Hiermee wordt het verschil tussen twee datum tijd waarden berekend|
|iif()|Evalueert het eerste argument en retourneert de waarde van de tweede of derde argumenten, afhankelijk van het feit of het predicaat is geëvalueerd als waar (seconde) of ONWAAR (derde)|
|indexof()|Functie rapporteert de op nul gebaseerde index van het eerste exemplaar van een opgegeven teken reeks in de invoer teken reeks|
|isnotnull()|Hiermee wordt het enige argument geëvalueerd en wordt een Booleaanse waarde geretourneerd die aangeeft of het argument resulteert in een waarde die niet null is|
|isnull()|Hiermee wordt het enige argument geëvalueerd en wordt een Booleaanse waarde geretourneerd die aangeeft of het argument resulteert in een null-waarde|
|now()|Retourneert de huidige UTC-klok tijd|
|strcat()|Voegt de argumenten tussen 1 en 64|
|strlen()|Retourneert de lengte in tekens van de invoer teken reeks|
|substring()|Hiermee wordt een subtekenreeks geëxtraheerd van een bron teken reeks, beginnend bij een index naar het einde van de teken reeks|
|tostring()|Converteert invoer naar een teken reeks representatie|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a> Aanvullende entiteiten, Opera tors en functies voor CMPivot van Configuration Manager

> [!Important]
> Deze items worden niet ondersteund wanneer u CMPivot uitvoert vanuit het micro soft Endpoint Manager-beheer centrum.

|Type|Item|Beschrijving|
|--|--|---|
|Entiteit|AccountSID|Account-SID|
|Entiteit|FileContent()|Inhoud van een specifiek bestand|
|Entiteit|NAPClient|NAP-client|
|Entiteit|NAPSystemHealthAgent|NAP-systeem status agent|
|Entiteit|REGI ster ()|Alle waarden voor een specifieke register sleutel<!--7371183-->|
|Tabel operator|waardoor|Hiermee worden resultaten weer gegeven als grafische uitvoer|
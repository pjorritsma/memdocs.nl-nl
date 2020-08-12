---
title: Referentie voor takenreeksvariabelen
titleSuffix: Configuration Manager
description: Meer informatie over de variabelen voor het beheren en aanpassen van een Configuration Manager taken reeks.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 667d7451f467592bd0645b54d7068a20628ec98e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124138"
---
# <a name="task-sequence-variables"></a>Takenreeksvariabelen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat een verwijzing voor alle beschik bare variabelen in alfabetische volg orde. Gebruik de functie **zoeken** in browser (doorgaans **CTRL**  +  **F**) om een specifieke variabele te vinden. De variabele opmerkingen als deze specifiek zijn voor een bepaalde stap. Het artikel over [taken reeks stappen](task-sequence-steps.md) bevat de lijst met variabelen die specifiek zijn voor elke stap.

Zie [using Task sequence Varia bles](using-task-sequence-variables.md)(Engelstalig) voor meer informatie.

## <a name="task-sequence-variable-reference"></a><a name="bkmk_tsvar"></a>Naslag informatie over taken reeks variabelen

### <a name="_osddetectedwindir"></a><a name="OSDDetectedWinDir"></a>_OSDDetectedWinDir

De taken reeks scant de harde schijven van de computer op een eerdere installatie van het besturings systeem wanneer Windows PE wordt gestart. De locatie van de Windows-map wordt opgeslagen in deze variabele. U kunt de takenreeks zo configureren dat deze waarde wordt opgehaald uit de omgeving en wordt gebruikt om dezelfde locatie van de Windows-map op te geven voor de installatie van het nieuwe besturingssysteem.

### <a name="_osddetectedwindrive"></a><a name="OSDDetectedWinDrive"></a>_OSDDetectedWinDrive

De taken reeks scant de harde schijven van de computer op een eerdere installatie van het besturings systeem wanneer Windows PE wordt gestart. De locatie van de vaste schijf voor de installatie van het besturingssysteem wordt opgeslagen in deze variabele. U kunt de takenreeks zo configureren dat deze waarde wordt opgehaald uit de omgeving en wordt gebruikt om dezelfde locatie van de harde schijf op te geven voor het nieuwe besturingssysteem.

### <a name="_osdmigrateusmtpackageid"></a><a name="OSDMigrateUsmtPackageID"></a>_OSDMigrateUsmtPackageID

*Is van toepassing op de stap [gebruikers status vastleggen](task-sequence-steps.md#BKMK_CaptureUserState) .*

(invoer)

Hiermee geeft u de pakket-ID op van het Configuration Manager-pakket dat de USMT-bestanden bevat. Deze variabele is vereist.

### <a name="_osdmigrateusmtrestorepackageid"></a><a name="OSDMigrateUsmtRestorePackageID"></a>_OSDMigrateUsmtRestorePackageID

*Is van toepassing op de stap [gebruikers status herstellen](task-sequence-steps.md#BKMK_RestoreUserState) .*

(invoer)

Hiermee geeft u de pakket-ID op van het Configuration Manager-pakket dat de USMT-bestanden bevat. Deze variabele is vereist.

### <a name="_smstsadvertid"></a><a name="SMSTSAdvertID"></a>_SMSTSAdvertID

Slaat de unieke id van de huidige actieve takenreeksimplementatie op. Er wordt dezelfde indeling gebruikt als voor de implementatie-ID van een Configuration Manager software distributie. Deze variabele is niet gedefinieerd, als de takenreeks wordt uitgevoerd op zelfstandige media.

#### <a name="example"></a>Voorbeeld

`ABC20001`

### <a name="_smstsassettag"></a><a name="SMSTSAssetTag"></a>_SMSTSAssetTag

*Is van toepassing op de stap [dynamische variabelen instellen](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Geeft de inventaristag voor de computer aan.

### <a name="_smstsbootimageid"></a><a name="SMSTSBootImageID"></a>_SMSTSBootImageID

Als de huidige actieve taken reeks naar een installatie kopie pakket verwijst, slaat deze variabele de pakket-ID van de opstart installatie kopie op. Als de taken reeks niet verwijst naar een installatie kopie pakket, wordt deze variabele niet ingesteld.

#### <a name="example"></a>Voorbeeld

`ABC00001`  

### <a name="_smstsbootuefi"></a><a name="SMSTSBootUEFI"></a>_SMSTSBootUEFI

De taken reeks stelt deze variabele in wanneer een computer in de UEFI-modus wordt gedetecteerd.

### <a name="_smstsclientcache"></a><a name="SMSTSClientCache"></a>_SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
De taken reeks stelt deze variabele in als de inhoud op het lokale station wordt opgeslagen in de cache. De variabele bevat het pad naar de cache. Als deze variabele niet bestaat, is er geen cache.

### <a name="_smstsclientguid"></a><a name="SMSTSClientGUID"></a>_SMSTSClientGUID

Slaat de waarde op van Configuration Manager client-GUID. Als de taken reeks wordt uitgevoerd vanaf zelfstandige media, wordt deze variabele niet ingesteld.

#### <a name="example"></a>Voorbeeld

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="_smstscurrentactionname"></a><a name="SMSTSCurrentActionName"></a>_SMSTSCurrentActionName

Hiermee geeft u de naam op van de huidige actieve stap van de takenreeks. Deze variabele wordt ingesteld voordat takenreeksbeheer elke afzonderlijke stap uitvoert.

#### <a name="example"></a>Voorbeeld

`run command line`

### <a name="_smstsdefaultgateways"></a><a name="SMSTSDefaultGateways"></a>_SMSTSDefaultGateways

*Is van toepassing op de stap [dynamische variabelen instellen](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Geeft de standaardgateways aan die worden gebruikt door de computer.

### <a name="_smstsdownloadondemand"></a><a name="SMSTSDownloadOnDemand"></a>_SMSTSDownloadOnDemand

Als de huidige taken reeks wordt uitgevoerd in de modus voor downloaden op aanvraag, is deze variabele `true` . Down load-on-demand modus betekent dat taken reeks beheer alleen lokaal inhoud downloadt wanneer het toegang heeft tot de inhoud.

### <a name="_smstsinwinpe"></a><a name="SMSTSInWinPE"></a>_SMSTSInWinPE

Wanneer de huidige taken reeks stap wordt uitgevoerd in Windows PE, is deze variabele `true` . Test deze taken reeks variabele om de huidige besturingssysteem omgeving te bepalen.

### <a name="_smstsipaddresses"></a><a name="SMSTSIPAddresses"></a>_SMSTSIPAddresses

*Is van toepassing op de stap [dynamische variabelen instellen](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Geeft de IP-adressen aan die door de computer worden gebruikt.

### <a name="_smstslastactionname"></a><a name="SMSTSLastActionName"></a>_SMSTSLastActionName

Slaat de naam op van de laatste actie die is uitgevoerd. Deze variabele is gekoppeld aan **_SMSTSLastActionRetCode**. De taken reeks registreert deze waarden in het bestand bestand smsts. log. Deze variabele is handig bij het oplossen van problemen met een taken reeks. Wanneer een stap mislukt, kan een aangepast script de naam van de stap en de retour code bevatten.

### <a name="_smstslastactionretcode"></a><a name="SMSTSLastActionRetCode"></a>_SMSTSLastActionRetCode

Slaat de retour code op van de laatste actie die is uitgevoerd. Deze variabele kan worden gebruikt als een voorwaarde om te bepalen of de volgende stap wordt uitgevoerd.

#### <a name="example"></a>Voorbeeld

`0`

### <a name="_smstslastactionsucceeded"></a><a name="SMSTSLastActionSucceeded"></a>_SMSTSLastActionSucceeded

- Als de laatste stap is voltooid, is deze variabele `true` .  

- Als de laatste stap is mislukt, is dat `false` .  

- Als de taken reeks de laatste actie heeft overgeslagen, omdat de stap is uitgeschakeld of de gekoppelde voor waarde is geëvalueerd als **Onwaar**, wordt deze variabele niet opnieuw ingesteld. Het bevat nog steeds de waarde voor de vorige actie.  

### <a name="_smstslastcontentdownloadlocation"></a><a name="SMSTSLastContentDownloadLocation"></a>_SMSTSLastContentDownloadLocation

<!-- 2840337 -->
Vanaf versie 1906 bevat deze variabele de laatste locatie waar de taken reeks is gedownload of geprobeerd inhoud te downloaden. Inspecteer deze variabele in plaats van de client logboeken voor deze inhouds locatie te parseren.

### <a name="_smstslaunchmode"></a><a name="SMSTSLaunchMode"></a>_SMSTSLaunchMode

Specificeert dat de taken reeks is gestart via een van de volgende methoden:  

- **SMS**: de Configuration Manager-client, bijvoorbeeld wanneer een gebruiker deze start vanuit software Center
- **UFD**: verouderde USB-media
- **UFD + Format**: nieuwere USB-media
- **Cd**: een opstart bare cd
- **DVD**: een opstart bare DVD
- **PXE**: opstarten via het netwerk met PXE
- **HD**: voor bereide media op een harde schijf

### <a name="_smstslogpath"></a><a name="SMSTSLogPath"></a>_SMSTSLogPath

Slaat het volledige pad op van de logboekmap. Gebruik deze waarde om te bepalen waar de stappen van de taken reeks de acties registreren. Deze waarde wordt niet ingesteld als er geen vaste schijf beschikbaar is.

### <a name="_smstsmacaddresses"></a><a name="SMSTSMacAddresses"></a>_SMSTSMacAddresses

*Is van toepassing op de stap [dynamische variabelen instellen](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Geeft de MAC-adressen aan die door de computer worden gebruikt.

### <a name="_smstsmachinename"></a><a name="SMSTSMachineName"></a>_SMSTSMachineName

Slaat de computernaam op en specificeert deze. Slaat de naam op van de computer die door de taken reeks wordt gebruikt om alle status berichten te registreren. Als u de naam van de computer in het nieuwe besturings systeem wilt wijzigen, gebruikt u de variabele [OSDComputerName](#OSDComputerName-input) .

### <a name="_smstsmake"></a><a name="SMSTSMake"></a>_SMSTSMake

*Is van toepassing op de stap [dynamische variabelen instellen](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Geeft het merk van de computer aan.

### <a name="_smstsmdatapath"></a><a name="SMSTSMDataPath"></a>_SMSTSMDataPath

Hiermee geeft u het pad op dat wordt gedefinieerd door de variabele [SMSTSLocalDataDrive](#SMSTSLocalDataDrive) . Dit pad geeft aan waar de taken reeks tijdelijke cache bestanden opslaat op de doel computer terwijl deze wordt uitgevoerd. Wanneer u SMSTSLocalDataDrive definieert voordat de taken reeks wordt gestart, bijvoorbeeld door een verzamelings variabele in te stellen, definieert Configuration Manager de _SMSTSMDataPath variabele zodra de taken reeks wordt gestart.

### <a name="_smstsmediatype"></a><a name="SMSTSMediaType"></a>_SMSTSMediaType

Hiermee geeft u het type media op dat wordt gebruikt om de installatie te initiëren. Voorbeelden van typen media zijn opstartmedia, volledige media, PXE en voorgefaseerde media.

### <a name="_smstsmodel"></a><a name="SMSTSModel"></a>_SMSTSModel

*Is van toepassing op de stap [dynamische variabelen instellen](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Geeft het model van de computer aan.

### <a name="_smstsmp"></a><a name="SMSTSMP"></a>_SMSTSMP

Hiermee wordt de URL of het IP-adres van een Configuration Manager beheer punt opgeslagen.

### <a name="_smstsmpport"></a><a name="SMSTSMPPort"></a>_SMSTSMPPort

Hiermee wordt het poort nummer van een Configuration Manager beheer punt opgeslagen.

### <a name="_smstsorgname"></a><a name="SMSTSOrgName"></a>_SMSTSOrgName

Slaat de naam op van de titel van de brander die de taken reeks weergeeft in het voortgangs venster.

### <a name="_smstsosupgradeactionreturncode"></a><a name="SMSTSOSUpgradeActionReturnCode"></a>_SMSTSOSUpgradeActionReturnCode

*Is van toepassing op de stap [besturings systeem bijwerken](task-sequence-steps.md#BKMK_UpgradeOS) .*

Slaat de afsluit code waarde op die Windows Setup wordt geretourneerd om aan te geven of de bewerking is geslaagd of mislukt. Deze variabele is handig bij de `/Compat` opdracht regel optie.

#### <a name="example"></a>Voorbeeld

Na het volt ooien van een compatibiliteits scan moet u in latere stappen actie ondernemen, afhankelijk van de afsluit code van de fout of het succes. Begin met het uitvoeren van de upgrade. U kunt ook een markering in de omgeving instellen om te verzamelen met de hardware-inventarisatie. U kunt bijvoorbeeld een bestand toevoegen of een register sleutel instellen. Gebruik deze markering om een verzameling computers te maken die kunnen worden bijgewerkt of waarvoor actie moet worden uitgevoerd voordat de upgrade kan worden uitgevoerd.

### <a name="_smstspackageid"></a><a name="SMSTSPackageID"></a>_SMSTSPackageID

Slaat de id van de huidige actieve takenreeks op. Deze ID maakt gebruik van dezelfde indeling als een Configuration Manager pakket-ID.

#### <a name="example"></a>Voorbeeld

`HJT00001`

### <a name="_smstspackagename"></a><a name="SMSTSPackageName"></a>_SMSTSPackageName

Slaat de naam op van de huidige actieve taken reeks. Een Configuration Manager beheerder geeft deze naam aan bij het maken van de taken reeks.

#### <a name="example"></a>Voorbeeld

`Deploy Windows 10 task sequence`

### <a name="_smstsrunfromdp"></a><a name="SMSTSRunFromDP"></a>_SMSTSRunFromDP

Ingesteld op `true` als de huidige taken reeks wordt uitgevoerd in de modus uitvoeren vanaf distributie punt. Deze modus geeft aan dat de taken reeks Manager vereiste pakket shares verkrijgt van het distributie punt.

### <a name="_smstsserialnumber"></a><a name="SMSTSSerialNumber"></a>_SMSTSSerialNumber

*Is van toepassing op de stap [dynamische variabelen instellen](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Geeft het serienummer van de computer aan.

### <a name="_smstssetuprollback"></a><a name="SMSTSSetupRollback"></a>_SMSTSSetupRollback

Hiermee geeft u op of Windows Setup een terugdraai bewerking hebt uitgevoerd tijdens een in-place upgrade. De waarden van de variabele kunnen `true` of zijn `false` .

### <a name="_smstssitecode"></a><a name="SMSTSSiteCode"></a>_SMSTSSiteCode

Slaat de site code op van de Configuration Manager-site.

#### <a name="example"></a>Voorbeeld

`ABC`

### <a name="_smststimezone"></a><a name="SMSTSTimezone"></a>_SMSTSTimezone

Deze variabele slaat de tijdzone gegevens op in de volgende indeling:

`Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName`

#### <a name="example"></a>Voorbeeld

Voor de tijd zone **Eastern Time (VS en Canada)**:

`300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time`

### <a name="_smststype"></a><a name="SMSTSType"></a>_SMSTSType

Hiermee geeft u het type op van de huidige actieve takenreeks. Dit kan een van de volgende waarden hebben:  

- **1**: een algemene taken reeks
- **2**: een taken reeks voor de implementatie van een besturings systeem

### <a name="_smstsusecrl"></a><a name="SMSTSUseCRL"></a>_SMSTSUseCRL

Wanneer de taken reeks gebruikmaakt van HTTPS om te communiceren met het beheer punt, wordt met deze variabele opgegeven of de certificaatintrekkingslijst (CRL) wordt gebruikt.

### <a name="_smstsuserstarted"></a><a name="SMSTSUserStarted"></a>_SMSTSUserStarted

Hiermee wordt aangegeven of een gebruiker de taken reeks heeft gestart. Deze variabele wordt alleen ingesteld als de taken reeks wordt gestart vanuit software Center. Als [_SMSTSLaunchMode](#SMSTSLaunchMode) bijvoorbeeld is ingesteld op `SMS` .

Deze variabele kan de volgende waarden hebben:  

- `true`: Hiermee geeft u op dat de taken reeks hand matig wordt gestart door een gebruiker vanuit software Center.  

- `false`: Hiermee geeft u op dat de taken reeks automatisch wordt geïnitieerd door de Configuration Manager scheduler.

### <a name="_smstsusessl"></a><a name="SMSTSUseSSL"></a>_SMSTSUseSSL

Hiermee geeft u op of de taken reeks SSL gebruikt om te communiceren met het Configuration Manager beheer punt. Als u uw site systemen voor HTTPS configureert, wordt de waarde ingesteld op `true` .

### <a name="_smstsuuid"></a><a name="SMSTSUUID"></a>_SMSTSUUID

*Is van toepassing op de stap [dynamische variabelen instellen](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Geeft de UUID van de computer aan.

### <a name="_smstswtg"></a><a name="SMSTSWTG"></a>_SMSTSWTG

De variabele specificeert of de computer wordt gebruikt als een Windows To Go-apparaat.

### <a name="_ts_crmemory"></a><a name="TSCRMEMORY"></a>_TS_CRMEMORY

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de controle van het **minimale geheugen (MB)** de waarde True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_crspeed"></a><a name="TSCRSPEED"></a>_TS_CRSPEED

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de **minimale processor snelheid (MHz)** controleren True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_crdisk"></a><a name="TSCRDISK"></a>_TS_CRDISK

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de controle **minimale beschik bare schijf ruimte (MB)** de waarde True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_crostype"></a><a name="TSCROSTYPE"></a>_TS_CROSTYPE

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of het **huidige besturings systeem dat moet worden vernieuwd, wordt geretourneerd als** True ( `1` ) of False ( `0` ). Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_crarch"></a><a name="TSCRARCH"></a>_TS_CRARCH

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de **architectuur van de huidige controle van het besturings systeem** True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_crminosver"></a><a name="TSCRMINOSVER"></a>_TS_CRMINOSVER

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de minimale controle van de versie van het **besturings systeem** True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_crmaxosver"></a><a name="TSCRMAXOSVER"></a>_TS_CRMAXOSVER

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de maximale controle van de versie van het **besturings systeem** True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_crclientminver"></a><a name="TSCRCLIENTMINVER"></a>_TS_CRCLIENTMINVER

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de controle van de **minimale client versie** True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_croslanguage"></a><a name="TSCROSLANGUAGE"></a>_TS_CROSLANGUAGE

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de **taal van de huidige controle van het besturings systeem** True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_cracpower"></a><a name="TSCRACPOWER"></a>_TS_CRACPOWER

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de **netstroom die is aangesloten op het stop** contact, True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_crnetwork"></a><a name="TSCRNETWORK"></a>_TS_CRNETWORK

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de controle van de **netwerk adapter die is verbonden** , True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_cruefi"></a><a name="TSCRUEFI"></a>_TS_CRUEFI

*Vanaf versie 2006* <!--6452769-->
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de **computer zich in de UEFI-modus bevindt** BIOS ( `0` ) of UEFI ( `1` ). Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_ts_crwired"></a><a name="TSCRWIRED"></a>_TS_CRWIRED

*Vanaf versie 2002* <!--6005561-->  
*Is van toepassing op de stap [gereedheid controleren](task-sequence-steps.md#BKMK_CheckReadiness) .*

Een alleen-lezen variabele voor of de **netwerk adapter niet draadloze** controle de waarde True ( `1` ) of False ( `0` ) retourneert. Als u de controle niet inschakelt, is de waarde van deze alleen-lezen variabele leeg.

### <a name="_tsappinstallstatus"></a><a name="TSAppInstallStatus"></a>_TSAppInstallStatus

De taken reeks stelt deze variabele in met de installatie status voor de toepassing tijdens de stap [toepassing installeren](task-sequence-steps.md#BKMK_InstallApplication) . Hiermee wordt een van de volgende waarden ingesteld:  

- Niet **gedefinieerd**: de stap toepassing installeren wordt niet uitgevoerd.  

- **Fout**: ten minste één toepassing is mislukt vanwege een fout tijdens de stap toepassing installeren.  

- **Waarschuwing**: er zijn geen fouten opgetreden tijdens de stap toepassing installeren. Een of meer toepassingen, of een vereiste afhankelijkheid, niet zijn geïnstalleerd omdat niet is voldaan aan een vereiste.  

- **Geslaagd**: er zijn geen fouten of waarschuwingen gedetecteerd tijdens de stap toepassing installeren.  

### <a name="_tssecureboot"></a><a name="TSSecureBoot"></a>_TSSecureBoot

*Vanaf versie 2002* <!--5842295-->  

Gebruik deze variabele om de status van beveiligd opstarten op een apparaat met UEFI-functionaliteit te bepalen. De variabele kan een van de volgende waarden hebben:

- `NA`: De bijbehorende register waarde bestaat niet. Dit betekent dat het apparaat beveiligd opstarten niet ondersteunt.
- `Enabled`: Beveiligd opstarten is ingeschakeld op het apparaat.
- `Disabled`: Beveiligd opstarten is uitgeschakeld op het apparaat.

### <a name="osdadapter"></a><a name="OSDAdapter"></a>OSDAdapter

*Is van toepassing op de stap [netwerk instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(invoer)

Deze taken reeks variabele is een *matrix* variabele. Elk element in de matrix staat voor de instellingen voor één netwerkadapter op de computer. Toegang tot de instellingen voor elke adapter door de naam van de matrix variabele te combi neren met de op nul gebaseerde netwerk adapter index en de naam van de eigenschap.

Als met de stap netwerk instellingen Toep assen meerdere netwerk adapters worden geconfigureerd, worden de eigenschappen voor de *tweede* netwerk adapter gedefinieerd met behulp van de index **1** in de naam van de variabele. Bijvoorbeeld: OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList en OSDAdapter1DNSDomain.

Gebruik de volgende namen van variabelen om de eigenschappen van de *eerste* netwerk adapter te definiëren voor de te configureren stap:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

Deze instelling is vereist. Mogelijke waarden zijn `True` en `False`. Bijvoorbeeld:

`true`: Enable Dynamic Host Configuration Protocol (DHCP) voor de adapter

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList

Een door komma's gescheiden lijst met IP-adressen voor de adapter. Deze eigenschap wordt genegeerd, tenzij **EnableDHCP** is ingesteld op `false` . Deze instelling is vereist.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

Een door komma's gescheiden lijst met subnetmaskers. Deze eigenschap wordt genegeerd, tenzij **EnableDHCP** is ingesteld op `false` . Deze instelling is vereist.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

Een door komma's gescheiden lijst met IP-gateway adressen. Deze eigenschap wordt genegeerd, tenzij **EnableDHCP** is ingesteld op `false` . Deze instelling is vereist.

#### <a name="osdadapter0dnsdomain"></a>Osdadapter0dnsdomain – DNS

Domain Name System-domein (DNS) voor de adapter.

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList

Een door komma's gescheiden lijst met DNS-servers voor de adapter. Deze instelling is vereist.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration

Stel in om `true` het IP-adres voor de adapter in DNS te registreren.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

Stel `true` dit in om het IP-adres voor de adapter in DNS te registreren onder de volledige DNS-naam voor de computer.

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering

Stel `true` deze optie in om IP-protocol filtering op de adapter in te scha kelen.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList

Een door komma's gescheiden lijst met protocollen die over IP mogen worden uitgevoerd. Deze eigenschap wordt genegeerd als **EnableIPProtocolFiltering** is ingesteld op `false` .

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering

Instellen op `true` om TCP-poort filtering voor de adapter in te scha kelen.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList

Een door komma's gescheiden lijst met poorten waaraan toegangs machtigingen voor TCP worden toegekend. Deze eigenschap wordt genegeerd als **EnableTCPFiltering** is ingesteld op `false` .

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

Opties voor NetBIOS via TCP/IP. Mogelijke waarden zijn als volgt:  

- `0`: NetBIOS-instellingen van DHCP-server gebruiken  
- `1`: NetBIOS via TCP/IP inschakelen  
- `2`: NetBIOS via TCP/IP uitschakelen  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS

Stel in `true` om WINS te gebruiken voor naam omzetting.

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList

Een door komma's gescheiden lijst met IP-adressen van WINS-servers. Deze eigenschap wordt genegeerd, tenzij **EnableWINS** is ingesteld op `true` .

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

MAC-adres dat wordt gebruikt om instellingen overeen te laten komen met de fysieke netwerk adapter.

#### <a name="osdadapter0name"></a>OSDAdapter0Name

De naam van de netwerk verbinding zoals deze wordt weer gegeven in het programma netwerk verbindingen van het configuratie scherm. De naam ligt tussen 0 en 255 tekens lang.

#### <a name="osdadapter0index"></a>OSDAdapter0Index

Index van de instellingen van de netwerk adapter in de matrix met instellingen.

#### <a name="example"></a>Voorbeeld

- **OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="osdadaptercount"></a><a name="OSDAdapterCount"></a>OSDAdapterCount

*Is van toepassing op de stap [netwerk instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(invoer)

Hiermee geeft u het aantal netwerkadapters op dat op de doelcomputer is geïnstalleerd. Wanneer u de waarde **OSDAdapterCount** instelt, stelt u ook alle configuratie opties voor elke adapter in.

Als u bijvoorbeeld de waarde **OSDAdapter0TCPIPNetbiosOptions** voor de eerste adapter instelt, moet u alle waarden voor die adapter configureren.

Als u deze waarde niet opgeeft, negeert de taken reeks alle **OSDAdapter** -waarden.

### <a name="osdapplydriverbootcriticalcontentuniqueid"></a><a name="OSDApplyDriverBootCriticalContentUniqueID"></a>OSDApplyDriverBootCriticalContentUniqueID

*Is van toepassing op de stap [Stuur programmapakket Toep assen](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(invoer)

Hiermee geeft u de inhoud-id op van het te installeren stuurprogramma voor massaopslagapparaten uit het stuurprogrammapakket. Als deze variabele niet is opgegeven, wordt er geen stuur programma voor massa opslag geïnstalleerd.

### <a name="osdapplydriverbootcriticalhardwarecomponent"></a><a name="OSDApplyDriverBootCriticalHardwareComponent"></a>OSDApplyDriverBootCriticalHardwareComponent

*Is van toepassing op de stap [Stuur programmapakket Toep assen](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(invoer)

Hiermee geeft u op of een stuur programma voor massaopslagapparaten wordt geïnstalleerd. deze variabele moet **SCSI**zijn.

Als [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) is ingesteld, is deze variabele vereist.

### <a name="osdapplydriverbootcriticalid"></a><a name="OSDApplyDriverBootCriticalID"></a>OSDApplyDriverBootCriticalID

*Is van toepassing op de stap [Stuur programmapakket Toep assen](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(invoer)

Hiermee geeft u de essentiële opstart-id op van het te installeren stuurprogramma voor massaopslagapparaten. Deze ID wordt weer gegeven in de sectie **SCSI** van het bestand Txtsetup. OEM van het apparaatstuurprogramma.

Als [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) is ingesteld, is deze variabele vereist.

### <a name="osdapplydriverbootcriticalinffile"></a><a name="OSDApplyDriverBootCriticalINFFile"></a>OSDApplyDriverBootCriticalINFFile

*Is van toepassing op de stap [Stuur programmapakket Toep assen](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(invoer)

Hiermee geeft u het INF-bestand op van het te installeren stuurprogramma voor massaopslag.

Als [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) is ingesteld, is deze variabele vereist.

### <a name="osdautoapplydriverbestmatch"></a><a name="OSDAutoApplyDriverBestMatch"></a>OSDAutoApplyDriverBestMatch

*Is van toepassing op de stap [Stuur Programma's automatisch Toep assen](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

(invoer)

Als er meerdere apparaatstuurprogramma's in de stuurprogrammacatalogus zijn die compatibel zijn met een hardwareapparaat, bepaalt deze variabele de actie van de stap.

#### <a name="valid-values"></a>Geldige waarden

- `true`(standaard): Installeer alleen het beste apparaatstuurprogramma  

- `false`: Hiermee worden alle compatibele apparaatstuurprogramma's geïnstalleerd en kiest Windows het beste stuur programma dat moet worden gebruikt  

### <a name="osdautoapplydrivercategorylist"></a><a name="OSDAutoApplyDriverCategoryList"></a>OSDAutoApplyDriverCategoryList

*Is van toepassing op de stap [Stuur Programma's automatisch Toep assen](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

(invoer)

Een door komma's gescheiden lijst van unieke categorie-id's uit de stuurprogrammacatalogus. Met de stap **stuur programma automatisch Toep assen** worden alleen de Stuur Programma's in ten minste één van de opgegeven categorieën beschouwd. Deze waarde is optioneel en is niet standaard ingesteld. Haal de beschik bare categorie-Id's op door de lijst met **SMS_CategoryInstance** objecten op de site te inventariseren.

### <a name="osdbitlockerrebootcount"></a><a name="OSDBitLockerRebootCount"></a>OSDBitLockerRebootCount

*Is van toepassing op de stap [BitLocker uitschakelen](task-sequence-steps.md#BKMK_DisableBitLocker) .*

<!-- 4512937 -->
Met ingang van versie 1906 gebruikt u deze variabele om het aantal keer opnieuw opstarten in te stellen waarna de beveiliging wordt hervat.

#### <a name="valid-values"></a>Geldige waarden

Een geheel getal van `1` tot `15` .

### <a name="osdbitlockerrebootcountoverride"></a><a name="OSDBitLockerRebootCountOverride"></a>OSDBitLockerRebootCountOverride

*Is van toepassing op de stap [BitLocker uitschakelen](task-sequence-steps.md#BKMK_DisableBitLocker) .*

<!-- 4512937 -->
Met ingang van versie 1906 stelt u deze waarde in om het aantal te overschrijven dat is ingesteld met de stap of de variabele [OSDBitLockerRebootCount](#OSDBitLockerRebootCount) . Hoewel de andere methoden alleen waarden 1 tot en met 15 accepteren, blijft BitLocker voor onbepaalde tijd ingeschakeld als u deze variabele instelt op 0. Deze variabele is handig wanneer de taken reeks één waarde instelt, maar u een afzonderlijke waarde per apparaat of per verzameling wilt instellen.

#### <a name="valid-values"></a>Geldige waarden

Een geheel getal van `0` tot `15` .

### <a name="osdbitlockerrecoverypassword"></a><a name="OSDBitLockerRecoveryPassword"></a>OSDBitLockerRecoveryPassword

*Is van toepassing op de stap [BitLocker inschakelen](task-sequence-steps.md#BKMK_EnableBitLocker) .*

(invoer)

In plaats van een wille keurig herstel wachtwoord te genereren, gebruikt de stap **BitLocker inschakelen** de opgegeven waarde als het herstel wachtwoord. De waarde moet een geldig numeriek BitLocker-herstelwachtwoord zijn.

### <a name="osdbitlockerstartupkey"></a><a name="OSDBitLockerStartupKey"></a>OSDBitLockerStartupKey

*Is van toepassing op de stap [BitLocker inschakelen](task-sequence-steps.md#BKMK_EnableBitLocker) .*

(invoer)

In plaats van een wille keurige opstart sleutel te genereren voor de sleutel beheer optie **opstart sleutel op USB,** wordt met de stap **BitLocker inschakelen** de Trusted Platform Module (TPM) gebruikt als opstart sleutel. De waarde moet een geldige, 256-bits BitLocker-opstartsleutel met Base64-codering zijn.

### <a name="osdcaptureaccount"></a><a name="OSDCaptureAccount"></a>OSDCaptureAccount

*Is van toepassing op de stap voor het [vastleggen van installatie kopieën van besturings systemen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(invoer)

Hiermee geeft u een Windows-account naam op die machtigingen heeft voor het opslaan van de vastgelegde installatie kopie op een netwerk share ([OSDCaptureDestination](#OSDCaptureDestination)). Geef ook de [OSDCaptureAccountPassword](#OSDCaptureAccountPassword)op.

Zie [accounts](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account)voor meer informatie over de installatie kopie van het besturings systeem.

### <a name="osdcaptureaccountpassword"></a><a name="OSDCaptureAccountPassword"></a>OSDCaptureAccountPassword

*Is van toepassing op de stap voor het [vastleggen van installatie kopieën van besturings systemen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(invoer)

Hiermee geeft u het wacht woord op voor het Windows-account ([OSDCaptureAccount](#OSDCaptureAccount)) dat wordt gebruikt voor het opslaan van de vastgelegde installatie kopie op een netwerk share ([OSDCaptureDestination](#OSDCaptureDestination)).

### <a name="osdcapturedestination"></a><a name="OSDCaptureDestination"></a>OSDCaptureDestination

*Is van toepassing op de stap voor het [vastleggen van installatie kopieën van besturings systemen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(invoer)

Hiermee geeft u de locatie op waar de vastgelegde installatie kopie van het besturings systeem wordt opgeslagen in de taken reeks. De maximale lengte van de mapnaam is 255 tekens. Als de netwerk share verificatie vereist, geeft u de variabelen [OSDCaptureAccount](#OSDCaptureAccount) en [OSDCaptureAccountPassword](#OSDCaptureAccountPassword) op.

### <a name="osdcomputername-input"></a><a name="OSDComputerName-input"></a>OSDComputerName (invoer)

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Geeft de naam van de doelcomputer op.

#### <a name="example"></a>Voorbeeld

`%_SMSTSMachineName%`prijs

### <a name="osdcomputername-output"></a><a name="OSDComputerName-output"></a>OSDComputerName (uitvoer)

*Is van toepassing op de stap [Windows-instellingen vastleggen](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

Ingesteld op de NetBIOS-naam van de computer. De waarde wordt alleen ingesteld als de variabele [OSDMigrateComputerName](#OSDMigrateComputerName) is ingesteld op `true` .

### <a name="osdconfigfilename"></a><a name="OSDConfigFileName"></a>OSDConfigFileName

*Is van toepassing op de stap [installatie kopie van besturings systeem Toep assen](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) .*

(invoer)

Hiermee geeft u de bestands naam op van het antwoord bestand voor de besturingssysteem implementatie dat is gekoppeld aan het installatie kopie pakket van de besturingssysteem implementatie.  

### <a name="osddataimageindex"></a><a name="OSDDataImageIndex"></a>OSDDataImageIndex

*Is van toepassing op de stap afbeelding van het [Toep assen van gegevens](task-sequence-steps.md#BKMK_ApplyDataImage) .*

(invoer)

Hiermee geeft u de index waarde op van de installatie kopie die wordt toegepast op de doel computer.

### <a name="osddiskindex"></a><a name="OSDDiskIndex"></a>OSDDiskIndex

*Is van toepassing op de stap [schijf Format teren en partitioneren](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(invoer)

Hiermee geeft u het nummer van de te partitioneren fysieke schijf op.

### <a name="osddnsdomain"></a><a name="OSDDNSDomain"></a>OSDDNSDomain

*Is van toepassing op de stap [netwerk instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(invoer)

Hiermee geeft u de primaire DNS-server op die op de doel computer wordt gebruikt.

### <a name="osddnssuffixsearchorder"></a><a name="OSDDNSSuffixSearchOrder"></a>OSDDNSSuffixSearchOrder

*Is van toepassing op de stap [netwerk instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(invoer)

Hiermee geeft u de DNS-zoekvolgorde op voor de doelcomputer.

### <a name="osddomainname"></a><a name="OSDDomainName"></a>Osddomainname opgeven

*Is van toepassing op de stap [netwerk instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(invoer)

Hiermee geeft u de naam op van het Active Directory domein waarvan de doel computer lid wordt. De opgegeven waarde moet een geldige domeinnaam van Active Directory Domain Services zijn.

### <a name="osddomainouname"></a><a name="OSDDomainOUName"></a>OSDDomainOUName

*Is van toepassing op de stap [netwerk instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(invoer)

Hiermee geeft u de naam in RFC 1779-indeling op van de organisatie-eenheid (OE) waarvan de doelcomputer lid wordt. Als u deze optie opgeeft, moet de waarde het volledige pad bevatten.

#### <a name="example"></a>Voorbeeld

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="osddonotlogcommand"></a><a name="OSDDoNotLogCommand"></a>OSDDoNotLogCommand

<!--1358493-->
*Is van toepassing op de stap [pakket installeren](task-sequence-steps.md#BKMK_InstallPackage) .*

*Vanaf versie 1902*  
*Is van toepassing op de stap [opdracht regel uitvoeren](task-sequence-steps.md#BKMK_RunCommandLine) .*

(invoer)

Als u wilt voor komen dat mogelijk gevoelige gegevens worden weer gegeven of geregistreerd, stelt u deze variabele in op `TRUE` . Deze variabele maskeert de programma naam in de **bestand smsts. log** tijdens de stap **pakket installeren** .

Vanaf versie 1902, wanneer u deze variabele instelt op `TRUE` , wordt de opdracht regel ook verborgen met de stap **opdracht regel uitvoeren** in het logboek bestand.<!--3654172-->

### <a name="osdenabletcpipfiltering"></a><a name="OSDEnableTCPIPFiltering"></a>OSDEnableTCPIPFiltering

*Is van toepassing op de stap [netwerk instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(invoer)

Hiermee geeft u aan of TCP/IP-filtering is ingeschakeld.

#### <a name="valid-values"></a>Geldige waarden

- `true`  
- `false`prijs  

### <a name="osdgptbootdisk"></a><a name="OSDGPTBootDisk"></a>OSDGPTBootDisk

*Is van toepassing op de stap [schijf Format teren en partitioneren](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(invoer)

Hiermee geeft u op of u een EFI-partitie op een GPT-vaste schijf wilt maken. EFI-computers gebruiken deze partitie als opstart schijf.

#### <a name="valid-values"></a>Geldige waarden

- `true`  
- `false`prijs

### <a name="osdimagecreator"></a><a name="OSDImageCreator"></a>OSDImageCreator

*Is van toepassing op de stap voor het [vastleggen van installatie kopieën van besturings systemen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(invoer)

Optioneel. De naam van de gebruiker die de installatiekopie heeft gemaakt. Deze naam wordt opgeslagen in het WIM-bestand. De maximale lengte van de gebruikersnaam is 255 tekens.

### <a name="osdimagedescription"></a><a name="OSDImageDescription"></a>OSDImageDescription

*Is van toepassing op de stap voor het [vastleggen van installatie kopieën van besturings systemen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(invoer)

Een optionele, door de gebruiker gedefinieerde beschrijving van de vastgelegde installatie kopie van het besturings systeem. Deze beschrijving wordt opgeslagen in het WIM-bestand. De maximale lengte van de beschrijving is 255 tekens.

### <a name="osdimageindex"></a><a name="OSDImageIndex"></a>OSDImageIndex

*Is van toepassing op de stap [installatie kopie van besturings systeem Toep assen](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) .*

(invoer)

Hiermee geeft u de waarde van de installatie kopie-index van het WIM-bestand dat wordt toegepast op de doel computer.

### <a name="osdimageversion"></a><a name="OSDImageVersion"></a>OSDImageVersion

*Is van toepassing op de stap voor het [vastleggen van installatie kopieën van besturings systemen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(invoer)

Een optioneel, door de gebruiker gedefinieerd versie nummer om toe te wijzen aan de vastgelegde installatie kopie van het besturings systeem. Dit versienummer wordt opgeslagen in het WIM-bestand. Deze waarde kan een combi natie van alfanumerieke tekens zijn met een maximale lengte van 32.

### <a name="osdinstalldriversadditionaloptions"></a><a name="OSDInstallDriversAdditionalOptions"></a>OSDInstallDriversAdditionalOptions

<!--516679/2840016-->
*Is van toepassing op de stap [Stuur programmapakket Toep assen](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(invoer)

Hiermee geeft u aanvullende opties op die u wilt toevoegen aan de DISM-opdracht regel bij het Toep assen van een stuur programmapakket. De taken reeks verifieert de opdracht regel opties niet.

Als u deze variabele wilt gebruiken, schakelt u de instelling in, installeert u het **Stuur programmapakket via DISM met de optie recursief met**behulp van de stap **Stuur programmapakket Toep assen** .

Zie [opdracht regel opties voor Windows 10 DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options)voor meer informatie.

### <a name="osdjoinaccount"></a><a name="OSDJoinAccount"></a>OSDJoinAccount

*Is van toepassing op de volgende stappen:*  

- [Netwerkinstellingen toepassen](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Lid worden van domein of werkgroep](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(invoer)

Hiermee geeft u het domein gebruikers account op dat wordt gebruikt om de doel computer toe te voegen aan het domein. Deze variabele is vereist voor domeinlidmaatschap.

Zie [accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)voor meer informatie over het domein voor het samen voegen van taken reeksen.

### <a name="osdjoindomainname"></a><a name="OSDJoinDomainName"></a>OSDJoinDomainName

*Is van toepassing op de stap [lid worden van domein of werk groep](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(invoer)

Hiermee geeft u de naam op van een Active Directory domein waarvan de doel computer lid wordt. De domein naam moet tussen 1 en 255 tekens lang zijn.

### <a name="osdjoindomainouname"></a><a name="OSDJoinDomainOUName"></a>OSDJoinDomainOUName

*Is van toepassing op de stap [lid worden van domein of werk groep](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(invoer)

Hiermee geeft u de naam in RFC 1779-indeling op van de organisatie-eenheid (OE) waarvan de doelcomputer lid wordt. Als u deze optie opgeeft, moet de waarde het volledige pad bevatten. De lengte van de OE-naam moet tussen 0 en 32.767 tekens lang zijn. Deze waarde wordt niet ingesteld als de variabele [OSDJoinType](#OSDJoinType) is ingesteld op `1` (lid worden van werk groep).

#### <a name="example"></a>Voorbeeld

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="osdjoinpassword"></a><a name="OSDJoinPassword"></a>OSDJoinPassword

*Is van toepassing op de volgende stappen:*  

- [Netwerkinstellingen toepassen](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Lid worden van domein of werkgroep](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(invoer)

Hiermee geeft u het wacht woord op voor de [OSDJoinAccount](#OSDJoinAccount) die de doel computer gebruikt om lid te worden van het Active Directory domein. Als de taken reeks omgeving deze variabele niet bevat, probeert Windows Setup een leeg wacht woord. Als de variabele [OSDJoinType](#OSDJoinType) is ingesteld op `0` (lid worden van domein), is deze waarde vereist.

### <a name="osdjoinskipreboot"></a><a name="OSDJoinSkipReboot"></a>OSDJoinSkipReboot

*Is van toepassing op de stap [lid worden van domein of werk groep](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(invoer)

Hiermee geeft u aan of het opnieuw opstarten van de doelcomputer wordt overgeslagen nadat deze lid is geworden van het domein of de werkgroep.

#### <a name="valid-values"></a>Geldige waarden

- `true`  
- `false`  

### <a name="osdjointype"></a><a name="OSDJoinType"></a>OSDJoinType

*Is van toepassing op de stap [lid worden van domein of werk groep](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(invoer)

Hiermee geeft u aan of de doelcomputer lid wordt van een Windows-domein of een werkgroep.

#### <a name="valid-values"></a>Geldige waarden

- `0`: De doel computer toevoegen aan een Windows-domein  
- `1`: De doel computer toevoegen aan een werk groep  

### <a name="osdjoinworkgroupname"></a><a name="OSDJoinWorkgroupName"></a>OSDJoinWorkgroupName

*Is van toepassing op de stap [lid worden van domein of werk groep](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(invoer)

Hiermee geeft u de naam van een werkgroep waarvan de doelcomputer lid wordt. De lengte van de werkgroepnaam moet liggen tussen 1 en 32 tekens.

### <a name="osdkeepactivation"></a><a name="OSDKeepActivation"></a>OSDKeepActivation

*Is van toepassing op de stap [Windows voorbereiden voor vastleggen](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) .*

(invoer)

Hiermee geeft u op of Sysprep de markering voor product activering onderhoudt of herstelt.

#### <a name="valid-values"></a>Geldige waarden

- `true`: behoud de activerings vlag
- `false`(standaard): de activerings vlag opnieuw instellen

### <a name="osdlocaladminpassword"></a><a name="OSDLocalAdminPassword"></a>OSDLocalAdminPassword

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(invoer)

Hiermee geeft u het wacht woord van de lokale beheerders account op. Als u de optie inschakelt om **het lokale beheerders wachtwoord wille keurig te genereren en het account op alle ondersteunde platforms uit te scha kelen**, wordt deze variabele door de stap genegeerd. De opgegeven waarde moet tussen 1 en 255 tekens lang zijn.

### <a name="osdlogpowershellparameters"></a><a name="OSDLogPowerShellParameters"></a>OSDLogPowerShellParameters

<!--3556028-->
*Vanaf versie 1902*  
*Is van toepassing op de stap [Power shell-script uitvoeren](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

(invoer)

Om te voor komen dat mogelijk gevoelige gegevens worden geregistreerd, worden script parameters in het bestand **bestand smsts. log** niet door de stap **Power shell-script uitvoeren** geregistreerd. Als u de script parameters in het taken reeks logboek wilt toevoegen, stelt u deze variabele in op **True**.

### <a name="osdmigrateadaptersettings"></a><a name="OSDMigrateAdapterSettings"></a>OSDMigrateAdapterSettings

*Is van toepassing op de stap [netwerk instellingen vastleggen](task-sequence-steps.md#BKMK_CaptureNetworkSettings) .*

(invoer)

Hiermee geeft u op of de taken reeks de gegevens van de netwerk adapter vastlegt. Deze informatie bevat configuratie-instellingen voor TCP/IP, DNS en WINS.

#### <a name="valid-values"></a>Geldige waarden

- `true`prijs
- `false`

### <a name="osdmigrateadditionalcaptureoptions"></a><a name="OSDMigrateAdditionalCaptureOptions"></a>Taken osdmigrateadditionalcaptureoptions

*Is van toepassing op de stap [gebruikers status vastleggen](task-sequence-steps.md#BKMK_CaptureUserState) .*

(invoer)

Geef aanvullende opdracht regel opties op voor het hulp programma voor migratie van gebruikers status (USMT) dat de taken reeks gebruikt om de gebruikers status vast te leggen. Deze instellingen worden niet door de stap zichtbaar in de taken reeks editor. Geef deze opties op als teken reeks, die door de taken reeks wordt toegevoegd aan de automatisch gegenereerde USMT-opdracht regel voor scan State.

De USMT-opties die zijn opgegeven met deze taken reeks variabele worden niet gevalideerd op nauw keurigheid voordat de taken reeks wordt uitgevoerd.

Zie [Scan State-syntaxis](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax)voor meer informatie over de beschik bare opties.

### <a name="osdmigrateadditionalrestoreoptions"></a><a name="OSDMigrateAdditionalRestoreOptions"></a>Taken osdmigrateadditionalrestoreoptions

*Is van toepassing op de stap [gebruikers status herstellen](task-sequence-steps.md#BKMK_RestoreUserState) .*

(invoer)

Hiermee geeft u aanvullende opdracht regel opties voor het hulp programma voor migratie van gebruikers status (USMT) op dat de taken reeks gebruikt voor het herstellen van de gebruikers status. Geef de extra opties op als een teken reeks, die de taken reeks toevoegt aan de automatisch gegenereerde USMT-opdracht regel voor load State.

De USMT-opties die zijn opgegeven met deze taken reeks variabele worden niet gevalideerd op nauw keurigheid voordat de taken reeks wordt uitgevoerd.

Zie [Load State-syntaxis](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax)voor meer informatie over de beschik bare opties.

### <a name="osdmigratecomputername"></a><a name="OSDMigrateComputerName"></a>OSDMigrateComputerName

*Is van toepassing op de stap [Windows-instellingen vastleggen](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

(invoer)

Hiermee geeft u op of de naam van de computer wordt gemigreerd.

#### <a name="valid-values"></a>Geldige waarden

- `true`(standaard). De variabele [OSDComputerName (output)](#OSDComputerName-output) is ingesteld op de NetBIOS-naam van de computer.  
- `false`  

### <a name="osdmigrateconfigfiles"></a><a name="OSDMigrateConfigFiles"></a>OSDMigrateConfigFiles

*Is van toepassing op de stap [gebruikers status vastleggen](task-sequence-steps.md#BKMK_CaptureUserState) .*

(invoer)

Hiermee geeft u de configuratiebestanden op waarmee het vastleggen van gebruikersprofielen wordt beheerd. Deze variabele wordt alleen gebruikt als [OSDMigrateMode](#OSDMigrateMode) is ingesteld op `Advanced` . Deze door komma's gescheiden lijstwaarde wordt ingesteld om aangepaste gebruikersprofielmigratie uit te voeren.

#### <a name="example"></a>Voorbeeld

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="osdmigratecontinueonlockedfiles"></a><a name="OSDMigrateContinueOnLockedFiles"></a>OSDMigrateContinueOnLockedFiles

*Is van toepassing op de stap [gebruikers status vastleggen](task-sequence-steps.md#BKMK_CaptureUserState) .*

(invoer)

Als USMT sommige bestanden niet kan vastleggen, kan met deze variabele het vastleggen van de gebruikers status worden voortgezet.

#### <a name="valid-values"></a>Geldige waarden

- `true`prijs  
- `false`  

### <a name="osdmigratecontinueonrestore"></a><a name="OSDMigrateContinueOnRestore"></a>OSDMigrateContinueOnRestore

*Is van toepassing op de stap [gebruikers status herstellen](task-sequence-steps.md#BKMK_RestoreUserState) .*

(invoer)

Ga verder met het proces, zelfs als USMT sommige bestanden niet kan herstellen.

#### <a name="valid-values"></a>Geldige waarden

- `true`prijs  
- `false`  

### <a name="osdmigrateenableverboselogging"></a><a name="OSDMigrateEnableVerboseLogging"></a>OSDMigrateEnableVerboseLogging

*Is van toepassing op de volgende stappen:*  

- [Gebruikersstatus vastleggen](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Gebruikersstatus herstellen](task-sequence-steps.md#BKMK_RestoreUserState)  

(invoer)

Hiermee schakelt u uitgebreide logboek registratie in voor USMT. Deze waarde is vereist voor de stap.

#### <a name="valid-values"></a>Geldige waarden

- `true`  
- `false`prijs  

### <a name="osdmigratelocalaccounts"></a><a name="OSDMigrateLocalAccounts"></a>OSDMigrateLocalAccounts

*Is van toepassing op de stap [gebruikers status herstellen](task-sequence-steps.md#BKMK_RestoreUserState) .*

(invoer)

Hiermee geeft u op of het lokale computeraccount wordt hersteld.

#### <a name="valid-values"></a>Geldige waarden

- `true`  
- `false`prijs  

### <a name="osdmigratelocalaccountpassword"></a><a name="OSDMigrateLocalAccountPassword"></a>OSDMigrateLocalAccountPassword

*Is van toepassing op de stap [gebruikers status herstellen](task-sequence-steps.md#BKMK_RestoreUserState) .*

(invoer)

Als de variabele [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) is `true` , moet deze variabele het wacht woord bevatten dat is toegewezen aan *alle* gemigreerde lokale accounts. USMT wijst hetzelfde wacht woord toe aan alle gemigreerde lokale accounts. Beschouw dit wacht woord als tijdelijk en wijzig het later op een andere manier.

### <a name="osdmigratemode"></a><a name="OSDMigrateMode"></a>OSDMigrateMode

*Is van toepassing op de stap [gebruikers status vastleggen](task-sequence-steps.md#BKMK_CaptureUserState) .*

(invoer)

Hiermee kunt u de bestanden aanpassen die worden vastgelegd door USMT.

#### <a name="valid-values"></a>Geldige waarden

- `Simple`: In de taken reeks worden alleen de standaard USMT-configuratie bestanden gebruikt  

- `Advanced`: Met de taken reeks variabele [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) worden de configuratie bestanden opgegeven die USMT gebruikt  

### <a name="osdmigratenetworkmembership"></a><a name="OSDMigrateNetworkMembership"></a>OSDMigrateNetworkMembership

*Is van toepassing op de stap [netwerk instellingen vastleggen](task-sequence-steps.md#BKMK_CaptureNetworkSettings) .*

(invoer)

Hiermee geeft u op of de taken reeks de werk groep-of domein lidmaatschaps gegevens migreert.

#### <a name="valid-values"></a>Geldige waarden

- `true`prijs
- `false`

### <a name="osdmigrateregistrationinfo"></a><a name="OSDMigrateRegistrationInfo"></a>OSDMigrateRegistrationInfo

*Is van toepassing op de stap [Windows-instellingen vastleggen](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

(invoer)

Hiermee wordt aangegeven of de stap gebruikers-en organisatie gegevens migreert.

#### <a name="valid-values"></a>Geldige waarden

- `true`(standaard). De [OSDRegisteredOrgName-variabele (uitvoer)](#OSDRegisteredOrgName-output) wordt ingesteld op de geregistreerde organisatie naam van de computer.  
- `false`  

### <a name="osdmigrateskipencryptedfiles"></a><a name="OSDMigrateSkipEncryptedFiles"></a>OSDMigrateSkipEncryptedFiles

*Is van toepassing op de stap [gebruikers status vastleggen](task-sequence-steps.md#BKMK_CaptureUserState) .*

(invoer)

Hiermee geeft u op of versleutelde bestanden worden vastgelegd.

#### <a name="valid-values"></a>Geldige waarden

- `true`  
- `false`prijs  

### <a name="osdmigratetimezone"></a><a name="OSDMigrateTimeZone"></a>OSDMigrateTimeZone

*Is van toepassing op de stap [Windows-instellingen vastleggen](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

(invoer)

Hiermee geeft u op of de tijdzone van de computer wordt gemigreerd.

#### <a name="valid-values"></a>Geldige waarden

- `true`(standaard). De variabele [OSDTimeZone (uitvoer)](#OSDTimeZone-output) is ingesteld op de tijd zone van de computer.  
- `false`  

### <a name="osdnetworkjointype"></a><a name="OSDNetworkJoinType"></a>OSDNetworkJoinType

*Is van toepassing op de stap [netwerk instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(invoer)

Hiermee geeft u op of de doel computer lid wordt van een Active Directory domein of werk groep.

#### <a name="value-values"></a>Waarde waarden

- `0`: Lid worden van een Active Directory domein  
- `1`: Lid worden van een werk groep

### <a name="osdpartitions"></a><a name="OSDPartitions"></a>OSDPartitions

*Is van toepassing op de stap [schijf Format teren en partitioneren](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(invoer)

Deze taken reeks variabele is een matrix variabele van partitie-instellingen. Elk element in de matrix staat voor de instellingen voor één partitie op de harde schijf. Toegang tot de instellingen die zijn gedefinieerd voor elke partitie door de naam van de matrix variabele te combi neren met het schijf partitie nummer op basis van nul en de naam van de eigenschap.

Gebruik de volgende namen van variabelen om de eigenschappen te definiëren voor de *eerste* partitie die door deze stap op de harde schijf wordt gemaakt:

#### <a name="osdpartitions0type"></a>Osdpartitions0type –

Hiermee geeft u het type partitie. Deze eigenschap is vereist. Geldige waarden zijn `Primary` ,, en `Extended` `Logical` `Hidden` .

#### <a name="osdpartitions0filesystem"></a>Osdpartitions0filesystem – dit

Hiermee geeft u het type bestands systeem op dat moet worden gebruikt bij het format teren van de partitie. Deze eigenschap is optioneel. Als u geen bestands systeem opgeeft, wordt de partitie niet geformatteerd met de stap. Geldige waarden zijn `FAT32` en `NTFS` .

#### <a name="osdpartitions0bootable"></a>Osdpartitions0bootable –

Hiermee geeft u op of de partitie kan worden opgestart. Deze eigenschap is vereist. Als deze waarde is ingesteld op `TRUE` voor MBR-schijven, markeert de stap deze partitie als actief.

#### <a name="osdpartitions0quickformat"></a>Osdpartitions0quickformat –

Hiermee geeft u het type notatie op dat wordt gebruikt. Deze eigenschap is vereist. Als deze waarde is ingesteld op `TRUE` , wordt door de stap een snelle indeling uitgevoerd. Anders voert de stap een volledige indeling uit.

#### <a name="osdpartitions0volumename"></a>Osdpartitions0volumename –

Hiermee geeft u de naam op die wordt toegewezen aan het volume wanneer deze is geformatteerd. Deze eigenschap is optioneel.

#### <a name="osdpartitions0size"></a>OSDPartitions0Size

Hiermee geeft u de grootte van de partitie. Deze eigenschap is optioneel. Als deze eigenschap niet is opgegeven, wordt de partitie gemaakt met alle resterende vrije ruimte. Eenheden worden opgegeven met de variabele **OSDPartitions0SizeUnits** .

#### <a name="osdpartitions0sizeunits"></a>Osdpartitions0sizeunits –

In de stap worden deze eenheden gebruikt voor het interpreteren van de variabele **OSDPartitions0Size** . Deze eigenschap is optioneel. Geldige waarden zijn `MB` (standaard), `GB` en `Percent` .

#### <a name="osdpartitions0volumelettervariable"></a>Osdpartitions0volumelettervariable –

Wanneer deze stap partities maakt, wordt altijd de eerstvolgende beschik bare stationsletter gebruikt in Windows PE. Gebruik deze optionele eigenschap om de naam van een andere taken reeks variabele op te geven. In de stap wordt deze variabele gebruikt om de nieuwe stationsletter op te slaan voor toekomstige referentie.

Als u meerdere partities met deze taken reeks stap definieert, worden de eigenschappen voor de *tweede* partitie gedefinieerd door gebruik te maken van de **1** index in de naam van de variabele. Bijvoorbeeld: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**en **OSDPartitions1VolumeName**.

### <a name="osdpartitionstyle"></a><a name="OSDPartitionStyle"></a>OSDPartitionStyle

*Is van toepassing op de stap [schijf Format teren en partitioneren](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(invoer)

Hiermee geeft u de partitiestijl op die moet worden gebruikt bij het partitioneren van de schijf.

#### <a name="valid-values"></a>Geldige waarden

- `GPT`: Gebruik de GUID-partitie tabel stijl
- `MBR`: De partitie stijl Master Boot Record gebruiken

### <a name="osdproductkey"></a><a name="OSDProductKey"></a>OSDProductKey

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(invoer)

Geeft de Windows-productcode op. De opgegeven waarde moet tussen 1 en 255 tekens lang zijn.

### <a name="osdrandomadminpassword"></a><a name="OSDRandomAdminPassword"></a>OSDRandomAdminPassword

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(invoer)

Hiermee geeft u een wille keurig gegenereerd wacht woord op voor het lokale beheerders account in het nieuwe besturings systeem.

#### <a name="valid-values"></a>Geldige waarden

- `true`(standaard): Windows Setup schakelt het lokale beheerders account op de doel computer uit  

- `false`: Windows Setup maakt het lokale Administrator-account op de doel computer en stelt het account wachtwoord in op de waarde van [OSDLocalAdminPassword](#OSDLocalAdminPassword)  

### <a name="osdregisteredorgname-input"></a><a name="OSDRegisteredOrgName-input"></a>OSDRegisteredOrgName (invoer)

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Hiermee geeft u de standaard geregistreerde organisatie naam in het nieuwe besturings systeem op. De opgegeven waarde moet tussen 1 en 255 tekens lang zijn.

### <a name="osdregisteredorgname-output"></a><a name="OSDRegisteredOrgName-output"></a>OSDRegisteredOrgName (uitvoer)

*Is van toepassing op de stap [Windows-instellingen vastleggen](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

Ingesteld op de geregistreerde organisatienaam van de computer. De waarde wordt alleen ingesteld als de variabele [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) is ingesteld op `true` .

### <a name="osdregisteredusername"></a><a name="OSDRegisteredUserName"></a>OSDRegisteredUserName

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(invoer)

Hiermee geeft u de standaard geregistreerde gebruikers naam in het nieuwe besturings systeem op. De opgegeven waarde moet tussen 1 en 255 tekens lang zijn.

### <a name="osdserverlicenseconnectionlimit"></a><a name="OSDServerLicenseConnectionLimit"></a>OSDServerLicenseConnectionLimit

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(invoer)

Hiermee geeft u het maximumaantal toegestane verbindingen op. Het opgegeven getal moet liggen tussen 5 en 9999 verbindingen.

### <a name="osdserverlicensemode"></a><a name="OSDServerLicenseMode"></a>OSDServerLicenseMode

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(invoer)

Hiermee geeft u de Windows Server-licentie modus op die wordt gebruikt.

#### <a name="valid-values"></a>Geldige waarden

- `PerSeat`
- `PerServer`

### <a name="osdsetupadditionalupgradeoptions"></a><a name="OSDSetupAdditionalUpgradeOptions"></a>OSDSetupAdditionalUpgradeOptions

*Is van toepassing op de stap [besturings systeem bijwerken](task-sequence-steps.md#BKMK_UpgradeOS) .*

(invoer)

Hiermee geeft u de aanvullende opdracht regel opties op die worden toegevoegd aan Windows Setup tijdens een upgrade van Windows 10. De taken reeks verifieert de opdracht regel opties niet.

Zie [Windows Setup-opdrachtregelopties)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)voor meer informatie.

### <a name="osdstatefallbacktonaa"></a><a name="OSDStateFallbackToNAA"></a>OSDStateFallbackToNAA

*Is van toepassing op de stap [status opslag opvragen](task-sequence-steps.md#BKMK_RequestStateStore) .*

(invoer)

Wanneer het computer account geen verbinding kan maken met het status migratie punt, geeft deze variabele aan of de taken reeks terugvalt op het gebruik van het netwerk toegangs account (NAA).

Zie [accounts](../../core/plan-design/hierarchy/accounts.md#network-access-account)voor meer informatie over het netwerk toegangs account.

#### <a name="valid-values"></a>Geldige waarden

- `true`  
- `false`prijs  

### <a name="osdstatesmpretrycount"></a><a name="OSDStateSMPRetryCount"></a>OSDStateSMPRetryCount

*Is van toepassing op de stap [status opslag opvragen](task-sequence-steps.md#BKMK_RequestStateStore) .*

(invoer)

Hiermee wordt het aantal pogingen opgegeven dat met deze takenreeksstap wordt uitgevoerd om een statusmigratiepunt te zoeken voordat de stap mislukt. Het opgegeven aantal moet tussen 0 en 600 liggen.

### <a name="osdstatesmpretrytime"></a><a name="OSDStateSMPRetryTime"></a>OSDStateSMPRetryTime

*Is van toepassing op de stap [status opslag opvragen](task-sequence-steps.md#BKMK_RequestStateStore) .*

(invoer)

Hiermee geeft u het aantal seconden op dat de takenreeksstap moet wachten tussen nieuwe pogingen. Het aantal seconden mag maximaal 30 tekens zijn.

### <a name="osdstatestorepath"></a><a name="OSDStateStorePath"></a>Osdstatestorepath in

*Is van toepassing op de volgende stappen:*  

- [Gebruikersstatus vastleggen](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Statusopslag vrijgeven](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [Statusopslag opvragen](task-sequence-steps.md#BKMK_RequestStateStore)  
- [Gebruikersstatus herstellen](task-sequence-steps.md#BKMK_RestoreUserState)  

(invoer)

De netwerk share of lokale padnaam van de map waarin de taken reeks de gebruikers status opslaat of herstelt. Er is geen standaard waarde.

### <a name="osdtargetsystemdrive"></a><a name="OSDTargetSystemDrive"></a>OSDTargetSystemDrive

*Is van toepassing op de stap [installatie kopie van besturings systeem Toep assen](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) .*

(uitvoer)

Hiermee geeft u de stationsletter van de partitie die de besturingssysteem bestanden bevat nadat de installatie kopie is toegepast.

### <a name="osdtargetsystemroot-input"></a><a name="OSDTargetSystemRoot-input"></a>OSDTargetSystemRoot (invoer)

*Is van toepassing op de stap voor het [vastleggen van installatie kopieën van besturings systemen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

Hiermee geeft u het pad op naar de Windows-map van het geïnstalleerde besturings systeem op de referentie computer. De taken reeks verifieert deze als een ondersteund besturings systeem voor vastleggen door Configuration Manager.

### <a name="osdtargetsystemroot-output"></a><a name="OSDTargetSystemRoot-output"></a>OSDTargetSystemRoot (uitvoer)

*Is van toepassing op de stap [Windows voorbereiden voor vastleggen](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) .*

Hiermee geeft u het pad op naar de Windows-map van het geïnstalleerde besturings systeem op de referentie computer. De taken reeks verifieert deze als een ondersteund besturings systeem voor vastleggen door Configuration Manager.

### <a name="osdtimezone-input"></a><a name="OSDTimeZone-input"></a>OSDTimeZone (invoer)

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Hiermee geeft u de standaard instelling voor de tijd zone op die wordt gebruikt in het nieuwe besturings systeem.

Stel de waarde van deze variabele in op de taal invariante naam van de tijd zone. Gebruik bijvoorbeeld de teken reeks in de `Std` waarde voor een tijd zone onder de volgende register sleutel: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones` .

### <a name="osdtimezone-output"></a><a name="OSDTimeZone-output"></a>OSDTimeZone (uitvoer)

*Is van toepassing op de stap [Windows-instellingen vastleggen](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

Ingesteld op de tijdzone van de computer. De waarde wordt alleen ingesteld als de variabele [OSDMigrateTimeZone](#OSDMigrateTimeZone) is ingesteld op `true` .

### <a name="osdwindowssettingsinputlocale"></a><a name="OSDWindowsSettingsInputLocale"></a>OSDWindowsSettingsInputLocale

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Hiermee geeft u de standaard land instelling voor invoer die wordt gebruikt in het nieuwe besturings systeem.

Zie [micro soft-Windows-International-core-InputLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-inputlocale)voor meer informatie over de waarde van het Windows Setup-antwoord bestand.

### <a name="osdwindowssettingssystemlocale"></a><a name="OSDWindowsSettingsSystemLocale"></a>OSDWindowsSettingsSystemLocale

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Hiermee geeft u de standaard land instelling voor het systeem op die wordt gebruikt in het nieuwe besturings systeem.

Zie [micro soft-Windows-International-core-SystemLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-systemlocale)voor meer informatie over de waarde van het Windows Setup-antwoord bestand.

### <a name="osdwindowssettingsuilanguage"></a><a name="OSDWindowsSettingsUILanguage"></a>OSDWindowsSettingsUILanguage

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Hiermee geeft u de standaard taal instelling voor de gebruikers interface op die wordt gebruikt in het nieuwe besturings systeem.

Zie [micro soft-Windows-International-core-UILanguage](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguage)voor meer informatie over de waarde van het Windows Setup-antwoord bestand.

### <a name="osdwindowssettingsuilanguagefallback"></a><a name="OSDWindowsSettingsUILanguageFallback"></a>OSDWindowsSettingsUILanguageFallback

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Hiermee geeft u de terugval taal instelling van de gebruikers interface op die wordt gebruikt in het nieuwe besturings systeem.

Zie [micro soft-Windows-International-core-UILanguageFallback](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguagefallback)voor meer informatie over de waarde van het Windows Setup-antwoord bestand.

### <a name="osdwindowssettingsuserlocale"></a><a name="OSDWindowsSettingsUserLocale"></a>OSDWindowsSettingsUserLocale

*Is van toepassing op de stap [Windows-instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Hiermee geeft u de standaard land instelling voor gebruikers die wordt gebruikt in het nieuwe besturings systeem.

Zie [micro soft-Windows-International-core-UserLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-userlocale)voor meer informatie over de waarde van het Windows Setup-antwoord bestand.

### <a name="osdwipedestinationpartition"></a><a name="OSDWipeDestinationPartition"></a>OSDWipeDestinationPartition

*Is van toepassing op de stap afbeelding van het [Toep assen van gegevens](task-sequence-steps.md#BKMK_ApplyDataImage) .*

(invoer)

Hiermee geeft u op of de bestanden op de doelpartitie worden verwijderd.

#### <a name="valid-values"></a>Geldige waarden

- `true`prijs
- `false`

### <a name="osdworkgroupname"></a><a name="OSDWorkgroupName"></a>OSDWorkgroupName

*Is van toepassing op de stap [netwerk instellingen Toep assen](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(invoer)

Hiermee geeft u de naam op van de werkgroep waarvan de doelcomputer lid wordt.

Geef deze variabele of de variabele [osddomainname opgeven](#OSDDomainName) op. De werkgroepnaam mag maximaal 32 tekens lang zijn.

### <a name="setupcompletepause"></a><a name="SetupCompletePause"></a>SetupCompletePause

*Is van toepassing op de stap [besturings systeem bijwerken](task-sequence-steps.md#BKMK_UpgradeOS) .*

<!-- 4680263 -->

Met ingang van versie 1910 kunt u met deze variabele timing problemen oplossen met het venster 10 in-place upgrade taken reeks op apparaten met hoge prestaties wanneer Windows Setup is voltooid. Wanneer u een waarde in seconden aan deze variabele toewijst, wordt de hoeveelheid tijd voordat de taken reeks wordt gestart door het Windows-installatie proces vertraagd. Deze time-out zorgt voor de Configuration Manager-client meer tijd om te initialiseren.

De volgende logboek vermeldingen zijn veelvoorkomende voor beelden van dit probleem, dat u kunt herstellen met deze variabele:

- De service tsmanager-component registreert vermeldingen die vergelijkbaar zijn met de volgende fouten in het **bestand smsts. log**:

    ``` log
    Failed to initate policy evaluation for namespace 'root\ccm\policy\machine', hr=0x80041010
    Error compiling client config policies. code 80041010
    Task Sequence Manager could not initialize Task Sequence Environment. code 80041010
    ```

- Windows Setup registreert vermeldingen die vergelijkbaar zijn met de volgende fouten in het **bestand setupcomplete. log**:

    ``` log
    Running C:\windows\CCM\\TSMBootstrap.exe to resume task sequence
    ERRORLEVEL = -1073741701
    TSMBootstrap did not request reboot, resetting registry
    Exiting setupcomplete.cmd
    ```

### <a name="smsclientinstallproperties"></a><a name="SMSClientInstallProperties"></a>SMSClientInstallProperties

*Is van toepassing op de stap [Windows en ConfigMgr installeren](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) .*

(invoer)

Hiermee geeft u de client installatie-eigenschappen op die de taken reeks gebruikt voor het installeren van de Configuration Manager-client.

Zie [over para meters en eigenschappen van client installatie](../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie.

### <a name="smsconnectnetworkfolderaccount"></a><a name="SMSConnectNetworkFolderAccount"></a>SMSConnectNetworkFolderAccount

*Is van toepassing op de stap [verbinding maken met](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) netwerkmap.*

(invoer)

Hiermee geeft u het gebruikers account op dat wordt gebruikt om verbinding te maken met de netwerk share in [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Geef het wacht woord voor het account op met de waarde [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword) .

Zie [accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account)voor meer informatie over het verbindings account voor de taken reeks netwerkmap.

### <a name="smsconnectnetworkfolderdriveletter"></a><a name="SMSConnectNetworkFolderDriveLetter"></a>SMSConnectNetworkFolderDriveLetter

*Is van toepassing op de stap [verbinding maken met](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) netwerkmap.*

(invoer)

Hiermee geeft u de netwerkstationsletter op waarmee verbinding wordt gemaakt. Deze waarde is optioneel. Als deze niet is opgegeven, wordt de netwerk verbinding niet toegewezen aan een stationsletter. Als deze waarde is opgegeven, moet de waarde binnen het bereik van D tot Z liggen. gebruik X niet. Dit is de stationsletter die door Windows PE wordt gebruikt tijdens de Windows PE-fase.

#### <a name="examples"></a>Voorbeelden

- `D:`  
- `E:`  

### <a name="smsconnectnetworkfolderpassword"></a><a name="SMSConnectNetworkFolderPassword"></a>SMSConnectNetworkFolderPassword

*Is van toepassing op de stap [verbinding maken met](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) netwerkmap.*

(invoer)

Hiermee geeft u het wacht woord op voor de [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) die wordt gebruikt om verbinding te maken met de netwerk share in [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath).

### <a name="smsconnectnetworkfolderpath"></a><a name="SMSConnectNetworkFolderPath"></a>SMSConnectNetworkFolderPath

*Is van toepassing op de stap [verbinding maken met](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) netwerkmap.*

(invoer)

Hiermee geeft u het netwerkpad voor de verbinding op. Als u dit pad moet toewijzen aan een stationsletter, gebruikt u de waarde [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter) .

#### <a name="example"></a>Voorbeeld

`\\server\share`

### <a name="smsinstallupdatetarget"></a><a name="SMSInstallUpdateTarget"></a>SMSInstallUpdateTarget

*Is van toepassing op de stap [software-updates installeren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) .*

(invoer)

Hiermee geeft u op of alle updates of alleen verplichte updates worden geïnstalleerd.

#### <a name="valid-values"></a>Geldige waarden

- `All`  
- `Mandatory`  

### <a name="smsrebootmessage"></a><a name="SMSRebootMessage"></a>SMSRebootMessage

*Is van toepassing op de stap [computer opnieuw opstarten](task-sequence-steps.md#BKMK_RestartComputer) .*

(invoer)

Hiermee geeft u het bericht op dat moet worden weergegeven voor gebruikers voordat de doelcomputer opnieuw wordt opgestart. Als deze variabele niet is ingesteld, wordt de standaard bericht tekst weer gegeven. Het opgegeven bericht mag niet langer zijn dan 512 tekens.

#### <a name="example"></a>Voorbeeld

`Save your work before the computer restarts.`  

### <a name="smsreboottimeout"></a><a name="SMSRebootTimeout"></a>SMSRebootTimeout

*Is van toepassing op de stap [computer opnieuw opstarten](task-sequence-steps.md#BKMK_RestartComputer) .*

(invoer)

Hiermee geeft u het aantal seconden op dat de waarschuwing wordt weergegeven aan de gebruiker voordat de computer opnieuw wordt opgestart.

#### <a name="examples"></a>Voorbeelden

- `0`(standaard): geen opnieuw opstarten bericht weer geven  
- `60`: De waarschuwing voor één minuut weer geven  

### <a name="smstsassignmentsdownloadinterval"></a><a name="SMSTSAssignmentsDownloadInterval"></a>SMSTSAssignmentsDownloadInterval

Het aantal seconden dat moet worden gewacht voordat de client het beleid probeert te downloaden sinds de laatste poging die geen beleid heeft geretourneerd. De client wacht standaard **0** seconden alvorens het opnieuw te proberen.

U kunt deze variabele instellen door een prestart-opdracht te gebruiken vanaf media of PXE.

### <a name="smstsassignmentsdownloadretry"></a><a name="SMSTSAssignmentsDownloadRetry"></a>SMSTSAssignmentsDownloadRetry

Het aantal keren dat een client het beleid probeert te downloaden nadat er bij de eerste poging geen beleid is gevonden. De client probeert standaard **0** keer opnieuw te proberen.

U kunt deze variabele instellen door een prestart-opdracht te gebruiken vanaf media of PXE.

### <a name="smstsassignusersmode"></a><a name="SMSTSAssignUsersMode"></a>SMSTSAssignUsersMode

Hiermee geeft u op hoe een takenreeks gebruikers koppelt aan de doelcomputer. Stel de variabele in op een van de volgende waarden:  

- **Automatisch**: wanneer de taken reeks het besturings systeem implementeert op de doel computer, maakt het een relatie tussen de opgegeven gebruikers en de doel computer.  

- **In behandeling**: de taken reeks maakt een relatie tussen de opgegeven gebruikers en de doel computer. Een beheerder moet de relatie goed keuren om deze in te stellen.  

- **Uitgeschakeld**: de taken reeks koppelt geen gebruikers aan de doel computer wanneer het besturings systeem wordt geïmplementeerd.

### <a name="smstsdisablestatusretry"></a><a name="SMSTSDisableStatusRetry"></a>SMSTSDisableStatusRetry

<!--512358-->
In scenario's zonder verbinding probeert de taken reeks engine herhaaldelijk status berichten naar het beheer punt te verzenden. Dit gedrag in dit scenario veroorzaakt vertragingen bij het verwerken van taken reeksen.

Stel deze variabele in op `true` en de taken reeks engine probeert geen status berichten te verzenden nadat het eerste bericht niet kan worden verzonden. In deze eerste poging zijn meerdere nieuwe pogingen opgenomen.

Wanneer de taken reeks opnieuw wordt gestart, blijft de waarde van deze variabele behouden. De taken reeks probeert echter een oorspronkelijk status bericht te verzenden. In deze eerste poging zijn meerdere nieuwe pogingen opgenomen. Als dit lukt, wordt de status van de taken reeks verder verzonden, ongeacht de waarde van deze variabele. Als de status niet kan worden verzonden, gebruikt de taken reeks de waarde van deze variabele.

> [!NOTE]  
> De rapportage van de [taken reeks status](../../core/servers/manage/list-of-reports.md#task-sequence---deployment-status) vertrouwt op deze status berichten om de voortgang, geschiedenis en Details van elke stap weer te geven. Als status berichten niet kunnen worden verzonden, worden ze niet in de wachtrij geplaatst. Wanneer de verbinding met het beheer punt wordt hersteld, worden deze niet op een later tijdstip verzonden. Dit gedrag resulteert in het rapporteren van taken reeks status om onvolledige en ontbrekende items te zijn.

### <a name="smstsdisablewow64redirection"></a><a name="SMSTSDisableWow64Redirection"></a>SMSTSDisableWow64Redirection

*Is van toepassing op de stap [opdracht regel uitvoeren](task-sequence-steps.md#BKMK_RunCommandLine) .*

(invoer)

Standaard in een 64-bits besturings systeem zoekt en voert de taken reeks het programma uit op de opdracht regel met behulp van de WOW64-bestands systeem-redirector. Dit gedrag zorgt ervoor dat de opdracht 32-bits versies van OS-Program ma's en-Dll's kan zoeken. Als u deze variabele instelt, wordt `true` het gebruik van de WOW64-bestands systeem-redirector uitgeschakeld. De opdracht vindt systeem eigen 64-bits versies van OS-Program ma's en dll-bestanden. Deze variabele heeft geen effect als deze wordt uitgevoerd op een 32-bits besturings systeem.

### <a name="smstsdownloadabortcode"></a><a name="SMSTSDownloadAbortCode"></a>SMSTSDownloadAbortCode

Deze variabele bevat de afbreek code waarde voor het download programma voor externe Program ma's. Dit programma is opgegeven in de variabele [SMSTSDownloadProgram](#SMSTSDownloadProgram) . Als het programma een fout code retourneert die gelijk is aan de waarde van de variabele SMSTSDownloadAbortCode, mislukt het downloaden van de inhoud en wordt er geen andere download methode geprobeerd.

### <a name="smstsdownloadprogram"></a><a name="SMSTSDownloadProgram"></a>SMSTSDownloadProgram

Gebruik deze variabele om een alternatieve inhouds provider (ACS) op te geven. Een ACS is een Downloader-programma dat wordt gebruikt om inhoud te downloaden. De taken reeks gebruikt de ACS in plaats van de standaard Configuration Manager Downloader. Als onderdeel van het proces voor het downloaden van inhoud, controleert de taken reeks deze variabele. Indien opgegeven, voert de taken reeks het programma uit om de inhoud te downloaden.

### <a name="smstsdownloadretrycount"></a><a name="SMSTSDownloadRetryCount"></a>SMSTSDownloadRetryCount

Het aantal keren dat Configuration Manager probeert inhoud te downloaden vanaf een distributie punt. De client probeert standaard **twee** maal opnieuw te proberen.

### <a name="smstsdownloadretrydelay"></a><a name="SMSTSDownloadRetryDelay"></a>SMSTSDownloadRetryDelay

Het aantal seconden dat Configuration Manager wacht voordat het opnieuw probeert inhoud te downloaden vanaf een distributie punt. De client wacht standaard **15** seconden alvorens het opnieuw te proberen.

### <a name="smstsdriverrequestconnecttimeout"></a><a name="SMSTSDriverRequestConnectTimeOut"></a>SMSTSDriverRequestConnectTimeOut

*Is van toepassing op de stap [Stuur Programma's automatisch Toep assen](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

Bij het aanvragen van de stuurprogrammacatalogus, is deze variabele het aantal seconden dat de taken reeks wacht op de HTTP-server verbinding. Als de verbinding langer duurt dan de time-outinstelling, annuleert de taken reeks de aanvraag. De time-out is standaard ingesteld op **60** seconden.

### <a name="smstsdriverrequestreceivetimeout"></a><a name="SMSTSDriverRequestReceiveTimeOut"></a>SMSTSDriverRequestReceiveTimeOut

*Is van toepassing op de stap [Stuur Programma's automatisch Toep assen](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

Bij het aanvragen van de stuurprogrammacatalogus, is deze variabele het aantal seconden dat de taken reeks wacht op een antwoord. Als de verbinding langer duurt dan de time-outinstelling, annuleert de taken reeks de aanvraag. De time-out is standaard ingesteld op **480** seconden.

### <a name="smstsdriverrequestresolvetimeout"></a><a name="SMSTSDriverRequestResolveTimeOut"></a>SMSTSDriverRequestResolveTimeOut

*Is van toepassing op de stap [Stuur Programma's automatisch Toep assen](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

Bij het aanvragen van de stuurprogrammacatalogus, is deze variabele het aantal seconden dat de taken reeks wacht op HTTP-naam omzetting. Als de verbinding langer duurt dan de time-outinstelling, annuleert de taken reeks de aanvraag. De time-out is standaard ingesteld op **60** seconden.

### <a name="smstsdriverrequestsendtimeout"></a><a name="SMSTSDriverRequestSendTimeOut"></a>SMSTSDriverRequestSendTimeOut

*Is van toepassing op de stap [Stuur Programma's automatisch Toep assen](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

Bij het verzenden van een aanvraag voor de stuurprogrammacatalogus, is deze variabele het aantal seconden dat de taken reeks wacht op het verzenden van de aanvraag. Als de aanvraag langer duurt dan de time-outinstelling, annuleert de taken reeks de aanvraag. De time-out is standaard ingesteld op **60** seconden.

### <a name="smstserrordialogtimeout"></a><a name="SMSTSErrorDialogTimeout"></a>SMSTSErrorDialogTimeout

Als er een fout optreedt in een taken reeks, wordt er een dialoog venster met de fout weer gegeven. De taken reeks wordt automatisch gesloten na het aantal seconden dat door deze variabele is opgegeven. Deze waarde is standaard **900** seconden (15 minuten).

### <a name="smstslanguagefolder"></a><a name="SMSTSLanguageFolder"></a>SMSTSLanguageFolder

Gebruik deze variabele als u de weergavetaal wilt wijzigen van een taalonafhankelijke installatiekopie.

### <a name="smstslocaldatadrive"></a><a name="SMSTSLocalDataDrive"></a>SMSTSLocalDataDrive

Hiermee geeft u op waar de taken reeks tijdelijke cache bestanden opslaat op de doel computer terwijl deze wordt uitgevoerd.

Stel deze variabele in voordat de taken reeks wordt gestart, bijvoorbeeld door een verzamelings variabele in te stellen. Zodra de taken reeks is gestart, definieert Configuration Manager de [_SMSTSMDataPath](#SMSTSMDataPath) variabele op basis van de definitie van de variabele SMSTSLocalDataDrive.

### <a name="smstsmp"></a><a name="SMSTSMP"></a>SMSTSMP

Gebruik deze variabele om de URL of het IP-adres van het Configuration Manager beheer punt op te geven.

### <a name="smstsmplistrequesttimeoutenabled"></a><a name="SMSTSMPListRequestTimeoutEnabled"></a>SMSTSMPListRequestTimeoutEnabled

*Is van toepassing op de volgende stappen:*  

- [Toepassing installeren](task-sequence-steps.md#BKMK_InstallApplication)  
- [Software-updates installeren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(invoer)

Als de client zich niet op het intranet bevindt, gebruikt u deze variabele om herhaalde MPList-aanvragen voor het vernieuwen van de client in te scha kelen. Deze variabele is standaard ingesteld op `True` .

Wanneer clients zich op het Internet bevinden, stelt u deze variabele in op `False` om onnodige vertragingen te voor komen.

### <a name="smstsmplistrequesttimeout"></a><a name="SMSTSMPListRequestTimeout"></a>SMSTSMPListRequestTimeout

*Is van toepassing op de volgende stappen:*  

- [Toepassing installeren](task-sequence-steps.md#BKMK_InstallApplication)  
- [Software-updates installeren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(invoer)

Als de taken reeks de lijst met beheer punten (MPList) niet kan ophalen van locatie Services, geeft deze variabele aan hoeveel milliseconden er moet worden gewacht voordat de stap opnieuw wordt geprobeerd. Standaard wacht de taken reeks op `60000` milliseconden (60 seconden) voordat deze opnieuw probeert. Het probeert Maxi maal drie keer.

### <a name="smstspeerdownload"></a><a name="SMSTSPeerDownload"></a>SMSTSPeerDownload

Gebruik deze variabele om de client in staat te stellen Windows PE-peer-cache te gebruiken. Als u deze variabele instelt, wordt `true` deze functionaliteit ingeschakeld.

### <a name="smstspeerrequestport"></a><a name="SMSTSPeerRequestPort"></a>SMSTSPeerRequestPort

Een aangepaste netwerk poort die door Windows PE-peer-cache wordt gebruikt voor de eerste uitzending. De standaard poort die in de client instellingen is geconfigureerd, is **8004**.

### <a name="smstspersistcontent"></a><a name="SMSTSPersistContent"></a>Smstspersiscontent

Gebruik deze variabele als u inhoud tijdelijk in de takenreekscache wilt houden. Deze variabele wijkt af van [SMSTSPreserveContent](#SMSTSPreserveContent), die inhoud in de Configuration Manager-client cache houdt nadat de taken reeks is voltooid. Smstspersiscontent maakt gebruik van de taken reeks cache, SMSTSPreserveContent maakt gebruik van de Configuration Manager-client cache.

### <a name="smstspostaction"></a><a name="SMSTSPostAction"></a>SMSTSPostAction

Hiermee geeft u een opdracht op die wordt uitgevoerd nadat de taken reeks is voltooid. Geef bijvoorbeeld `shutdown.exe /r /t 30 /f` op dat de computer 30 seconden nadat de taken reeks is voltooid, opnieuw moet worden opgestart.

### <a name="smstspreferredadvertid"></a><a name="SMSTSPreferredAdvertID"></a>SMSTSPreferredAdvertID

Hiermee wordt de taken reeks gedwongen een specifieke gerichte implementatie uit te voeren op de doel computer. Stel deze variabele in via een prestart-opdracht vanaf media of PXE. Als deze variabele is ingesteld, overschrijft de takenreeks alle vereiste implementaties.

### <a name="smstspreservecontent"></a><a name="SMSTSPreserveContent"></a>SMSTSPreserveContent

Met deze variabele wordt de inhoud in de taken reeks gemarkeerd die na de implementatie moet worden bewaard in de Configuration Manager-client cache. Deze variabele wijkt af van de [smstspersiscontent](#SMSTSPersistContent), waarbij alleen de inhoud voor de duur van de taken reeks wordt bewaard. Smstspersiscontent maakt gebruik van de taken reeks cache, SMSTSPreserveContent maakt gebruik van de Configuration Manager-client cache. Stel SMSTSPreserveContent in om `true` deze functionaliteit in te scha kelen.

### <a name="smstsrebootdelay"></a><a name="SMSTSRebootDelay"></a>SMSTSRebootDelay

Hiermee wordt opgegeven hoeveel seconden er wordt gewacht voordat de computer opnieuw wordt opgestart. Als deze variabele nul (0) is, wordt in het taken reeks beheer geen meldings dialoogvenster weer gegeven voordat de computer opnieuw wordt opgestart.

#### <a name="example"></a>Voorbeeld

- `0`: geen melding weer geven  

- `60`: een melding voor één minuut weer geven  

### <a name="smstsrebootdelaynext"></a><a name="SMSTSRebootDelayNext"></a>SMSTSRebootDelayNext

<!--4447680-->
Vanaf versie 1906 gebruikt u deze variabele met de bestaande [SMSTSRebootDelay](task-sequence-variables.md#SMSTSRebootDelay) -variabele. Als u later opnieuw wilt opstarten met een andere time-out dan de eerste, stelt u SMSTSRebootDelayNext in op een andere waarde in seconden.

#### <a name="example"></a>Voorbeeld

U wilt gebruikers een melding van 60 minuten opnieuw opstarten aan het begin van de taken reeks van Windows 10 in-place upgrade geven. Na deze eerste lange time-out wilt u extra time-outs tot 60 seconden. Stel SMSTSRebootDelay in op `3600` en SMSTSRebootDelayNext naar `60` .  


### <a name="smstsrebootmessage"></a><a name="SMSTSRebootMessage"></a>SMSTSRebootMessage

Hiermee geeft u het bericht op dat moet worden weer gegeven in het dialoog venster melding over opnieuw opstarten. Als deze variabele niet is ingesteld, wordt een standaard bericht weer gegeven.

#### <a name="example"></a>Voorbeeld

`The task sequence is restarting this computer`

### <a name="smstsrebootrequested"></a><a name="SMSTSRebootRequested"></a>SMSTSRebootRequested

Geeft aan dat opnieuw opstarten is aangevraagd nadat de huidige takenreeks is voltooid. Als voor de taken reeks stap opnieuw opstarten nodig is om de actie te volt ooien, stelt u deze variabele in. Nadat de computer opnieuw is opgestart, wordt de taken reeks nog steeds uitgevoerd vanaf de volgende taken reeks stap.

- `HD`: Opnieuw opstarten naar het geïnstalleerde besturings systeem
- `WinPE`: Opnieuw opstarten naar de gekoppelde opstart installatie kopie

### <a name="smstsretryrequested"></a><a name="SMSTSRetryRequested"></a>SMSTSRetryRequested

Hiermee wordt een nieuwe poging aangevraagd nadat de huidige takenreeksstap is voltooid. Als deze taken reeks variabele is ingesteld, stelt u ook de variabele [SMSTSRebootRequested](#SMSTSRebootRequested) in op `true` . Nadat de computer opnieuw is opgestart, voert het taken reeks beheer dezelfde taken reeks stap opnieuw uit.

### <a name="smstsruncommandlineasuser"></a><a name="SMSTSRunCommandLineAsUser"></a>SMSTSRunCommandLineAsUser

*Vanaf versie 2002* <!-- 5573175 -->  
*Is van toepassing op de stap [opdracht regel uitvoeren](task-sequence-steps.md#BKMK_RunCommandLine) .*

Gebruik taken reeks variabelen voor het configureren van de gebruikers context voor de stap **opdracht regel uitvoeren** . U hoeft de stap **opdracht regel uitvoeren** niet te configureren met een tijdelijke account voor het gebruik van de variabelen [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName) en [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword) .

Configureer `SMSTSRunCommandLineAsUser` met een van de volgende waarden:

- `true`: Alle verdere **Uitvoeren opdracht regel** stappen worden uitgevoerd in de context van de gebruiker die is opgegeven in `SMSTSRunCommandLineUserName` .

- `false`: Alle verdere **Uitvoeren opdracht regel** stappen worden uitgevoerd in de context die u in de stap hebt geconfigureerd.

### <a name="smstsruncommandlineusername"></a><a name="SMSTSRunCommandLineUserName"></a>SMSTSRunCommandLineUserName

*Is van toepassing op de stap [opdracht regel uitvoeren](task-sequence-steps.md#BKMK_RunCommandLine) .*

(invoer)

Hiermee geeft u het account op waarmee de opdrachtregel wordt uitgevoerd. De waarde is een tekenreeks in de indeling gebruikersnaam of domein\gebruikersnaam. Geef het wacht woord voor het account op met de variabele [SMSTSRunCommandLineUserPassword](#SMSTSRunCommandLineUserPassword) .

> [!NOTE]
> Vanaf versie 2002 gebruikt u de variabele [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) met deze variabele om de gebruikers context voor deze stap te configureren.
>
> In versie 1910 en eerder configureert u de stap **opdracht regel uitvoeren** met de instelling om **deze stap uit te voeren als het volgende account**. Als u deze optie inschakelt en u de gebruikers naam en het wacht woord instelt met behulp van variabelen, geeft u een waarde op voor het account.

Zie [accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)voor meer informatie over het run as-account van de taken reeks.

### <a name="smstsruncommandlineuserpassword"></a><a name="SMSTSRunCommandLineUserPassword"></a>SMSTSRunCommandLineUserPassword

*Is van toepassing op de stap [opdracht regel uitvoeren](task-sequence-steps.md#BKMK_RunCommandLine) .*

(invoer)

Hiermee geeft u het wacht woord op voor het account dat is opgegeven door de variabele [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName) .

### <a name="smstsrunpowershellasuser"></a><a name="SMSTSRunPowerShellAsUser"></a>SMSTSRunPowerShellAsUser

*Vanaf versie 2002* <!-- 5573175 -->  
*Is van toepassing op de stap [Power shell-script uitvoeren](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

Gebruik taken reeks variabelen voor het configureren van de gebruikers context voor de stap **Power shell-script uitvoeren** . U hoeft de stap **Power shell-script uitvoeren** niet te configureren met een tijdelijke aanduiding voor het gebruik van de variabelen [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName) en [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword) .

Configureer `SMSTSRunPowerShellAsUser` met een van de volgende waarden:

- `true`: Eventuele verdere **uitvoer Power shell-script** stappen worden uitgevoerd in de context van de gebruiker die is opgegeven in `SMSTSRunPowerShellUserName` .

- `false`: Alle verdere **Power shell-script** stappen die worden uitgevoerd in de context die u hebt geconfigureerd in de stap.

### <a name="smstsrunpowershellusername"></a><a name="SMSTSRunPowerShellUserName"></a>SMSTSRunPowerShellUserName

*Is van toepassing op de stap [Power shell-script uitvoeren](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

(invoer)

Hiermee geeft u het account op waarmee het Power shell-script wordt uitgevoerd. De waarde is een tekenreeks in de indeling gebruikersnaam of domein\gebruikersnaam. Geef het wacht woord voor het account op met de variabele [SMSTSRunPowerShellUserPassword](#SMSTSRunPowerShellUserPassword) .

> [!NOTE]
> Als u deze variabelen wilt gebruiken, configureert u de stap **Power shell-script uitvoeren** met de instelling om **deze stap uit te voeren als het volgende account**. Als u deze optie inschakelt en u de gebruikers naam en het wacht woord instelt met behulp van variabelen, geeft u een waarde op voor het account.

Zie [accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)voor meer informatie over het run as-account van de taken reeks.

### <a name="smstsrunpowershelluserpassword"></a><a name="SMSTSRunPowerShellUserPassword"></a>SMSTSRunPowerShellUserPassword

*Is van toepassing op de stap [Power shell-script uitvoeren](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

(invoer)

Hiermee geeft u het wacht woord op voor het account dat is opgegeven door de variabele [SMSTSRunPowerShellUserName](#SMSTSRunPowerShellUserName) .

### <a name="smstssoftwareupdatescantimeout"></a><a name="SMSTSSoftwareUpdateScanTimeout"></a>SMSTSSoftwareUpdateScanTimeout

*Is van toepassing op de stap [software-updates installeren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) .*

(invoer)

Bepaal de time-out voor het scannen van software-updates tijdens deze stap. Als u bijvoorbeeld talloze updates verwacht tijdens de scan, verhoogt u de waarde. De standaard waarde is `3600` seconden (60 minuten). De waarde van de variabele wordt in seconden ingesteld.

### <a name="smstsudausers"></a><a name="SMSTSUDAUsers"></a>SMSTSUDAUsers

Hiermee geeft u de primaire gebruikers van de doel computer op met de volgende indeling: `<DomainName>\<UserName>` . Scheid meerdere gebruikers met behulp van een komma ( `,` ). Zie [gebruikers koppelen aan een doel computer](../get-started/associate-users-with-a-destination-computer.md)voor meer informatie.

#### <a name="example"></a>Voorbeeld

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="smstswaitforsecondreboot"></a><a name="SMSTSWaitForSecondReboot"></a>SMSTSWaitForSecondReboot

*Is van toepassing op de stap [software-updates installeren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) .*

(invoer)

Deze optionele taken reeks variabele bepaalt het client gedrag wanneer de installatie van een software-update twee maal opnieuw moet worden opgestart. Stel deze variabele in voor deze stap om te voor komen dat een taken reeks mislukt omdat de installatie van de software-update een tweede keer opnieuw moet worden opgestart.

Stel de waarde voor SMSTSWaitForSecondReboot in seconden in om op te geven hoelang de taken reeks tijdens deze stap wordt onderbroken terwijl de computer opnieuw wordt opgestart. Laat voldoende tijd voor het geval er een tweede keer opnieuw wordt opgestart.

Als u bijvoorbeeld SMSTSWaitForSecondReboot instelt op, wordt `600` de taken reeks gedurende tien minuten na het opnieuw opstarten onderbroken voordat extra stappen worden uitgevoerd. Deze variabele is handig wanneer een enkele taken reeks stap software-updates installeren honderden software-updates installeert.

> [!Note]
> Deze variabele is alleen van toepassing op een taken reeks die een besturings systeem implementeert. Het werkt niet in een aangepaste taken reeks. <!-- 2839998 -->

### <a name="tsdebugmode"></a><a name="TSDebugMode"></a>TSDebugMode

<!--3612274-->
Met ingang van versie 1906 stelt u deze variabele in `TRUE` op een verzameling of computer object waarop de taken reeks wordt geïmplementeerd. Op elk apparaat waarop deze variabele is ingesteld, wordt elke taken reeks geïmplementeerd in de foutopsporingsmodus.

Zie [debug a task sequence](../deploy-use/debug-task-sequence.md)voor meer informatie.

### <a name="tsdebugonerror"></a><a name="TSDebugOnError"></a>TSDebugOnError

<!-- 5012536 -->
Met ingang van versie 1910 stelt u deze variabele in op `TRUE` automatisch starten van het [fout opsporingsprogramma voor de taken reeks](../deploy-use/debug-task-sequence.md) wanneer de taken reeks een fout retourneert.

Stel deze variabele in op:

- De stap [taken reeks variabele instellen](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)

- Een verzamelings variabele. Zie [variabelen instellen](using-task-sequence-variables.md#bkmk_set)voor meer informatie.

### <a name="tsdisableprogressui"></a><a name="TSDisableProgressUI"></a>TSDisableProgressUI

<!-- 1354291 -->
Gebruik deze variabele om te bepalen wanneer de taken reeks voortgang weergeeft aan eind gebruikers. Als u de voortgang op verschillende tijdstippen wilt verbergen of weer geven, stelt u deze variabele meermaals in een taken reeks in.  

- `true`: Voortgang van taken reeks verbergen  

- `false`: Voortgang van taken reeks weer geven  

### <a name="tserroronwarning"></a><a name="TSErrorOnWarning"></a>Tserroronwarning instelt

*Is van toepassing op de stap [toepassing installeren](task-sequence-steps.md#BKMK_InstallApplication) .*

(invoer)

Geef op of de taken reeks engine een gedetecteerde waarschuwing beschouwt als een fout tijdens deze stap. De taken reeks stelt de [_TSAppInstallStatus](#TSAppInstallStatus) variabele in op `Warning` Wanneer een of meer toepassingen, of een vereiste afhankelijkheid, niet zijn geïnstalleerd omdat deze niet aan een vereiste voldoet. Wanneer u deze variabele instelt op `True` , en de taken reeks **_TSAppInstallStatus** op `Warning` , is het resultaat een fout. Een waarde van `False` is het standaard gedrag.

### <a name="tsprogressinfolevel"></a><a name="TSProgressInfoLevel"></a>TSProgressInfoLevel

*Vanaf versie 2002*<!--5932692-->  

Geef deze variabele op om te bepalen welk type informatie wordt weer gegeven in het venster voortgang van taken reeks. Gebruik de volgende waarden voor deze variabele:

- `1`: Voeg de huidige stap en het totale aantal stappen toe aan de voortgangs tekst. Bijvoorbeeld **2 van 10**.
- `2`: Voeg de huidige stap, het totale aantal stappen en het percentage voltooid toe. Bijvoorbeeld **2 van 10 (20% voltooid)**.
- `3`: Geef het percentage voltooid op. Bijvoorbeeld **(20% voltooid)**.

### <a name="tsuefidrive"></a><a name="TSUEFIDrive"></a>TSUEFIDrive

Gebruik de eigenschappen van een FAT32-partitie in het veld **variabele** . Wanneer de taken reeks deze variabele detecteert, bereidt deze de schijf voor op de overgang naar UEFI voordat de computer opnieuw wordt opgestart. Zie [taken reeks stappen voor het beheren van de conversie van BIOS naar UEFI](../deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md)voor meer informatie.

### <a name="workingdirectory"></a><a name="WorkingDirectory"></a>Variabele workingdirectory

*Is van toepassing op de stap [opdracht regel uitvoeren](task-sequence-steps.md#BKMK_RunCommandLine) .*

(invoer)

Hiermee geeft u de beginmap voor een opdrachtregelactie op. De opgegeven mapnaam mag niet langer zijn dan 255 tekens.

#### <a name="examples"></a>Voorbeelden

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>Afgeschafte variabelen

De volgende variabelen zijn afgeschaft:

- **OSDAllowUnsignedDriver**: wordt niet gebruikt bij het implementeren van Windows Vista en latere besturings systemen
- **OSDBuildStorageDriverList**: alleen van toepassing op Windows XP en windows server 2003
- **OSDDiskpartBiosCompatibilityMode**: alleen nodig bij het implementeren van Windows XP of Windows Server 2003
- **OSDInstallEditionIndex**: niet nodig na Windows Vista
- **OSDPreserveDriveLetter**: Zie [OSDPreserveDriveLetter](#osdpreservedriveletter) voor meer informatie.

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> Deze taken reeks variabele is afgeschaft.
>
> Tijdens de implementatie van een besturings systeem bepaalt Windows Setup standaard de beste stationsletter die moet worden gebruikt (meestal C:).

*Vorig gedrag*: wanneer u een installatie kopie toepast, bepaalt de variabele OSDPreverveDriveLetter of de taken reeks de stationsletter gebruikt die is vastgelegd in het installatie kopie bestand (Wim). Stel de waarde voor deze variabele in op het `false` gebruik van de locatie die u opgeeft voor de **doel** instelling in de taken reeks stap **besturings systeem Toep assen** . Zie installatie kopie van het [besturings systeem Toep assen](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)voor meer informatie.


## <a name="see-also"></a>Zie ook

- [Stappen voor takenreeksen](task-sequence-steps.md)
- [Taken reeks variabelen gebruiken](using-task-sequence-variables.md)
- [Planningsoverwegingen voor het automatiseren van taken](../plan-design/planning-considerations-for-automating-tasks.md)

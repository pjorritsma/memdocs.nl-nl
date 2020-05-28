---
title: Logboekbestanden
titleSuffix: Configuration Manager
description: Logboek bestanden gebruiken om problemen met Configuration Manager-clients en-site systemen op te lossen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 588bccc533909f2438dc61d6f25b39c3a582c71b
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879013"
---
# <a name="about-log-files-in-configuration-manager"></a>Over logboek bestanden in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In Configuration Manager worden proces gegevens in afzonderlijke logboek bestanden vastgelegd in de client-en Site Server onderdelen. U kunt de informatie in deze logboek bestanden gebruiken om problemen op te lossen die zich kunnen voordoen. Configuration Manager maakt logboek registratie voor client-en Server onderdelen standaard mogelijk.

Dit artikel bevat algemene informatie over de Configuration Manager-logboek bestanden. Het bevat hulpprogram ma's voor gebruik, het configureren van de logboeken en waar u ze kunt vinden. Zie voor meer informatie over specifieke logboek bestanden [referentie logboek bestanden](log-files.md).


## <a name="how-it-works"></a><a name="BKMK_AboutLogs"></a>Hoe werkt het?

De meeste processen in Configuration Manager operationele gegevens schrijven naar een logboek bestand dat is toegewezen aan dat proces. De logboek bestanden worden geïdentificeerd door **. log** of **. lo_** bestands extensies. Configuration Manager schrijft naar een log-bestand totdat het logboek de maximum grootte heeft bereikt. Wanneer het logboek vol is, wordt het. log-bestand gekopieerd naar een bestand met dezelfde naam, maar met de extensie. lo_ en het proces of onderdeel blijft naar het. log-bestand schrijven. Wanneer het. log-bestand de maximale grootte heeft bereikt, wordt het. lo_-bestand overschreven en wordt het proces herhaald. Sommige onderdelen maken een logboek bestand geschiedenis door een datum en tijds tempel toe te voegen aan de naam van het logboek bestand en door de. log-extensie te behouden.


## <a name="log-viewer-tools"></a><a name="bkmk_tools"></a>Hulpprogram ma's voor logboek weergave

Alle Configuration Manager-logboek bestanden zijn tekst zonder opmaak, zodat u ze kunt weer geven met een wille keurige tekst lezer als klad blok. De Logboeken gebruiken unieke opmaak die het beste kan worden weer gegeven met een van de volgende gespecialiseerde hulpprogram ma's:

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [Logboek viewer voor ondersteunings centrum](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

Als u de logboeken wilt weer geven, gebruikt u het hulp programma Configuration Manager log viewer **CMTrace**. Deze bevindt zich in de `\SMSSetup\Tools` map van de Configuration Manager-bron media. Het hulp programma CMTrace wordt toegevoegd aan alle opstart installatie kopieën die worden toegevoegd aan de software bibliotheek. Het CMTrace-hulp programma voor logboek weergave wordt samen met de Configuration Manager-client automatisch geïnstalleerd.<!--1357971--> Zie [CMTrace](../../support/cmtrace.md) voor meer informatie.

### <a name="onetrace"></a>OneTrace

Vanaf versie 1906 is **OneTrace** een nieuwe logboek weergave met het ondersteunings centrum. Het werkt op dezelfde manier als CMTrace, met verbeteringen. Zie [ondersteunings centrum OneTrace](../../support/support-center-onetrace.md)voor meer informatie.

### <a name="support-center-log-viewer"></a>Logboek viewer voor ondersteunings centrum

**Ondersteunings centrum** bevat een moderne logboek viewer. Dit hulp programma vervangt CMTrace en biedt een aanpas bare interface met ondersteuning voor tabbladen en dockable Windows. De laag heeft een snelle presentatielaag en kan grote logboek bestanden in enkele seconden laden. Zie de [Naslag Gids voor logboeken in ondersteunings centrum](../../support/support-center-ui-reference.md#bkmk_log-viewer)voor meer informatie.

> [!Note]  
> Het ondersteunings centrum en OneTrace gebruiken Windows Presentation Foundation (WPF). Dit onderdeel is niet beschikbaar in Windows PE. Ga door met het gebruik van CMTrace in opstart installatie kopieën met taken reeks implementaties.


## <a name="configure-logging-options"></a><a name="bkmk_logoptions"></a>Opties voor logboek registratie configureren

U kunt de configuratie van de logboek bestanden, zoals het uitgebreide niveau, de grootte en de geschiedenis, wijzigen. Er zijn verschillende manieren om deze instellingen te wijzigen:

- [Tijdens client installatie](#bkmk_logoptions-clientprop)
- [Configuration Manager Service Manager gebruiken](#bkmk_logoptions-sm)
- [Het Windows-REGI ster gebruiken](#bkmk_logoptions-registry)
- [In de Configuration Manager-console](#bkmk_logoptions-console)

### <a name="configure-logging-options-during-client-installation"></a><a name="bkmk_logoptions-clientprop"></a>Opties voor logboek registratie configureren tijdens client installatie

U kunt de configuratie van de client logboek bestanden instellen tijdens de installatie. Gebruik de volgende eigenschappen:

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

Zie [Eigenschappen van client installatie](../../clients/deploy/about-client-installation-properties.md#clientMsiProps)voor meer informatie.

### <a name="configure-logging-options-by-using-configuration-manager-service-manager"></a><a name="bkmk_logoptions-sm"></a>Configureer opties voor logboek registratie met behulp van Configuration Manager Service Manager

U kunt wijzigen waar Configuration Manager de logboek bestanden opslaat, en hun grootte.  

Als u de grootte van de logboek bestanden wilt wijzigen, de naam en locatie van het logboek bestand wilt wijzigen of als u wilt afdwingen dat meerdere onderdelen naar één logboek bestand schrijven, voert u de volgende stappen uit:  

#### <a name="modify-logging-for-a-component"></a>Logboek registratie voor een onderdeel wijzigen  

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw de **systeem status**uit en selecteer het knoop punt **site status** of **onderdeel status** .  

2. Selecteer in het lint **Start**en selecteer vervolgens **Configuration Manager Service Manager**.  

3. Als Configuration Manager Service Manager wordt geopend, maakt u verbinding met de site die u wilt beheren. Als de site die u wilt beheren niet wordt weer gegeven, selecteert u **site**, selecteert u **verbinden**en voert u de naam van de site server voor de juiste site in.  

4. Vouw de site uit en ga naar **onderdelen** of **servers**, afhankelijk van waar de onderdelen die u wilt beheren zich bevinden.  

5. Selecteer één of meer onderdelen in het rechterpaneel.  

6. Selecteer in het menu **onderdeel** **logboek registratie**.  

7. Voltooi in het dialoogvenster **Logboekregistratie Configuration Manager-onderdeel** de beschikbare configuratieopties voor uw selectie.  

8. Selecteer **OK** om de configuratie op te slaan.  

### <a name="configure-logging-options-by-using-the-windows-registry"></a><a name="bkmk_logoptions-registry"></a>Opties voor logboek registratie configureren met het Windows-REGI ster

<!-- SCCMDocs#992 -->
Gebruik het Windows-REGI ster op de servers of clients om de volgende opties voor logboek registratie te wijzigen:

- Niveau uitgebreid
- Maximum geschiedenis
- Maximumgrootte

Bij het oplossen van problemen kunt u uitgebreide logboek registratie inschakelen voor Configuration Manager om aanvullende details in de logboek bestanden te schrijven.

> [!Warning]
> Een onjuiste configuratie van deze instellingen kan ertoe leiden dat Configuration Manager grote hoeveel heden gegevens registreert, of helemaal niets. Hoewel deze gegevens handig kunnen zijn voor het oplossen van problemen, wees dan voorzichtig bij het wijzigen van deze waarden in productie sites. Test deze wijzigingen altijd eerst in een test omgeving. Overmatige logboek registratie kan optreden, waardoor het lastig is om relevante informatie te vinden in de logboek bestanden.

Nadat u wijzigingen in deze register instellingen hebt aangebracht, start u het onderdeel opnieuw:

- Als u de client instellingen wijzigt, start u de **SMS agent host** -service (CcmExec) opnieuw.
- Als u de server instellingen wijzigt, start u de **SMS Executive** -service opnieuw.

De Register instellingen variëren afhankelijk van het onderdeel:

- [Client en beheer punt](#bkmk_reg-client)
- [Site Server](#bkmk_reg-site)
- [Sitesysteemrol](#bkmk_reg-role)
- [Configuration Manager-console](#bkmk_reg-console)

#### <a name="client-and-management-point-logging-options"></a><a name="bkmk_reg-client"></a>Opties voor logboek registratie van client en beheer punt

Als u de opties voor logboek registratie wilt configureren voor alle onderdelen op een client-of beheer punt-site systeem, configureert u deze **REG_DWORD** waarden onder de volgende Windows-register sleutel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|Naam  |Waarden  |Beschrijving  |
|---------|---------|---------|
|Logniveau|`0`: Uitgebreid<br>`1`: Standaard<br>`2`: Waarschuwingen en fouten<br>`3`: Alleen fouten|Het detail niveau dat naar de logboek bestanden moet worden geschreven.|
|LogMaxHistory|Een geheel getal dat groter is dan of gelijk is aan nul, bijvoorbeeld:<br>`0`: Geen geschiedenis<br>`1`: Standaard|Wanneer een logboek bestand de maximum grootte bereikt, wordt de naam van de client gewijzigd als back-up en wordt er een nieuw logboek bestand gemaakt. Geef op hoeveel vorige versies moeten worden bewaard.|
|LogMaxSize|Een geheel getal dat groter is dan of gelijk is aan 10.000, bijvoorbeeld:<br>250000|De maximale grootte van het logboek bestand in bytes. Wanneer een logboek groter wordt dan de opgegeven grootte, wordt de naam van de client gewijzigd als een geschiedenis bestand en wordt er een nieuw bestand gemaakt. De standaard waarde is 250.000 bytes.|

> [!Note]  
> Wijzig geen andere waarden die mogelijk voor komen in deze register sleutel.

Voor geavanceerde fout opsporing kunt u deze **REG_SZ** waarde ook toevoegen onder de volgende Windows-register sleutel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|Naam  |Waarden  |Beschrijving  |
|---------|---------|---------|
|Ingeschakeld | `True`: Logboeken voor fout opsporing inschakelen<br>`False`: Logboeken voor fout opsporing uitschakelen |Schakelt logboek registratie voor fout opsporing in voor het oplossen van problemen.|

Deze instelling zorgt ervoor dat de client informatie op laag niveau registreert voor het oplossen van problemen. Vermijd het gebruik van deze instelling in productie sites. Overmatige logboek registratie kan optreden, waardoor het lastig is om relevante informatie te vinden in de logboek bestanden. Zorg ervoor dat u deze instelling uitschakelt nadat u het probleem hebt opgelost.

#### <a name="site-server-logging-options"></a><a name="bkmk_reg-site"></a>Opties voor logboek registratie van de site server

U kunt instellingen globaal configureren of voor een specifiek onderdeel op de Configuration Manager-site server.

Configureer deze waarden onder de volgende Windows-register sleutel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|Naam  |Waarden  |Type  |Beschrijving
|---------|---------|---------|---------|
|SqlEnabled| `1`: SQL-tracering inschakelen<br> `0`: SQL-tracering uitschakelen |REG_DWORD|SQL Trace-logboek registratie toevoegen aan alle logboeken van de site server.|
|ArchiveEnabled| `1`: logboek archieven inschakelen<br> `0`: logboek archieven uitschakelen | REG_DWORD |Archiveert site server logboeken op een afzonderlijke locatie voor historische behoud.|
|ArchivePath| Een geldig mappad, bijvoorbeeld`C:\Logs\Archive` | REG_SZ |Het pad voor het archiveren van de logboeken van de site server.|

Schakel SQL-tracering alleen in voor het oplossen van problemen. Vermijd het gebruik ervan in productie sites. Overmatige logboek registratie kan optreden, waardoor het lastig is om relevante informatie te vinden in de logboek bestanden. Zorg ervoor dat u deze instelling uitschakelt nadat u het probleem hebt opgelost.

> [!Note]  
> Wijzig geen andere waarden die mogelijk voor komen in deze register sleutel.

Als u opties voor logboek registratie wilt configureren voor een specifiek Server onderdeel, configureert u deze **REG_DWORD** waarden onder de volgende Windows-register sleutel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|Naam  |Waarden  |Beschrijving  |
|---------|---------|---------|
|LoggingLevel|`0`: Uitgebreid<br>`1`: Standaard<br>`2`: Waarschuwingen en fouten<br>`3`: Alleen fouten|Het detail niveau dat naar de logboek bestanden moet worden geschreven.|
|LogMaxHistory|Een geheel getal dat groter is dan of gelijk is aan nul, bijvoorbeeld:<br>`0`: Geen geschiedenis<br>`1`: Standaard|Wanneer een logboek bestand de maximum grootte bereikt, wordt de naam van de server gewijzigd als back-up en wordt er een nieuw logboek bestand gemaakt. Geef op hoeveel vorige versies moeten worden bewaard.|
|MaxFileSize|Een geheel getal dat groter is dan of gelijk is aan 10.000, bijvoorbeeld:<br>250000|De maximale grootte van het logboek bestand in bytes. Wanneer een logboek groter wordt dan de opgegeven grootte, wordt de naam van de client gewijzigd als een geschiedenis bestand en wordt er een nieuw bestand gemaakt. De standaard waarde is 250.000 bytes.|
|DebugLogging| `1`: Logboeken voor fout opsporing inschakelen<br>`0`: Logboeken voor fout opsporing uitschakelen |Schakelt logboek registratie voor fout opsporing in voor het oplossen van problemen.|

De instelling DebugLogging zorgt ervoor dat de server gegevens op laag niveau registreert voor het oplossen van problemen. Vermijd het gebruik van deze instelling in productie sites. Overmatige logboek registratie kan optreden, waardoor het lastig is om relevante informatie te vinden in de logboek bestanden. Zorg ervoor dat u deze instelling uitschakelt nadat u het probleem hebt opgelost.

> [!Note]  
> Wijzig geen andere waarden die mogelijk voor komen in deze register sleutel.

#### <a name="site-system-role-logging-options"></a><a name="bkmk_reg-role"></a>Opties voor logboek registratie van site systeem rollen

U kunt instellingen globaal configureren of voor een specifiek onderdeel op een site systeem dat als host fungeert voor een Configuration Manager serverrol.

Als u opties voor logboek registratie wilt configureren voor een specifiek Server onderdeel, configureert u deze **REG_DWORD** waarden onder de volgende Windows-register sleutel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

Voor de rol van distributie punt bijvoorbeeld:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|Naam  |Waarden  |Beschrijving  |
|---------|---------|---------|
|Logniveau|`0`: Uitgebreid<br>`1`: Standaard<br>`2`: Waarschuwingen en fouten<br>`3`: Alleen fouten|Het detail niveau dat naar de logboek bestanden moet worden geschreven.|
|LogMaxHistory|Een geheel getal dat groter is dan of gelijk is aan nul, bijvoorbeeld:<br>`0`: Geen geschiedenis<br>`1`: Standaard|Wanneer een logboek bestand de maximum grootte bereikt, wordt de naam van de server gewijzigd als back-up en wordt er een nieuw logboek bestand gemaakt. Geef op hoeveel vorige versies moeten worden bewaard.|
|LogMaxSize|Een geheel getal dat groter is dan of gelijk is aan 10.000, bijvoorbeeld:<br>250000|De maximale grootte van het logboek bestand in bytes. Wanneer een logboek groter wordt dan de opgegeven grootte, wordt de naam van de server gewijzigd als een geschiedenis bestand en wordt er een nieuw bestand gemaakt. De standaard waarde is 250.000 bytes.|

> [!Note]  
> Wijzig geen andere waarden die mogelijk voor komen in deze register sleutel.

#### <a name="configuration-manager-console-logging-options"></a><a name="bkmk_reg-console"></a>Opties voor logboek registratie van Configuration Manager-console

Gebruik de volgende procedure om het uitgebreide niveau van het AdminUI. log voor de Configuration Manager-console te wijzigen:

1. Open het console configuratie bestand **micro soft. ConfigurationManagement. exe. config**in een XML-editor, zoals Klad blok. Het standaard configuratie bestand bevindt zich op de volgende locatie:`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

    > [!IMPORTANT]
    > Vanaf versie 1910 is dit pad gewijzigd om de map te gebruiken `Microsoft Endpoint Manager` . Zorg ervoor dat u geen oudere versie van het bestand gebruikt dat in een andere map kan voor komen.

1. **system.diagnostics**  >  **sources**  >  Wijzig het kenmerk **switchValue** onder het**bron** element System. Diagnostics sources `Error` `Verbose` . Bijvoorbeeld:

    Origineel: `<source name="SmsAdminUISnapIn" switchValue="Error">` Nieuw:`<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. Sla het bestand op en start de console opnieuw.

### <a name="configure-logging-options-in-the-configuration-manager-console"></a><a name="bkmk_logoptions-console"></a>Opties voor logboek registratie configureren in de Configuration Manager-console

<!-- 4433455 -->

Vanaf versie 1910 kunt u uitgebreide logboek registratie in-of uitschakelen op een client of verzameling van de-console:

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , selecteer het knoop punt **apparaten** en kies een doel apparaat.

1. Selecteer in het lint op het tabblad **Start** in de groep **apparaat** de optie **client diagnostiek**. Kies een van de beschik bare acties.

Zie [client Diagnostics](../../clients/manage/client-notification.md#client-diagnostics)(Engelstalig) voor meer informatie.

## <a name="locating-log-files"></a><a name="BKMK_LogLocation"></a>Zoeken naar logboek bestanden

Met Configuration Manager-en afhankelijke onderdelen worden logboek bestanden op verschillende locaties opgeslagen. Deze locaties zijn afhankelijk van het proces dat het logboek bestand maakt en de configuratie van uw omgeving.

De volgende locaties zijn de standaard waarden. Als u de installatie mappen in uw omgeving hebt aangepast, kunnen de daad werkelijke paden verschillen.

- Serviceclient`C:\Windows\CCM\logs`
- Naam`C:\Program Files\Microsoft Configuration Manager\Logs`
- Beheer punt:`C:\SMS_CCM\Logs`
- Configuration Manager-console:`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog`
- ADSI`C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>Locaties van taken reeks logboeken

De locatie van het logboek bestand **bestand smsts. log** van de taken reeks varieert, afhankelijk van de fase van de taken reeks:

- In Windows PE voor [Format teren en partitioneren schijf](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) stap: `X:\Windows\temp\smstslog\smsts.log` (X is het Windows PE RAM-station)
- In Windows PE na **Format teren en partitioneren schijf** : `X:\smstslog\smsts.log` en vervolgens gekopieerd naar `C:\_SMSTaskSequence\Logs\smstslog\smsts.log` wanneer het station gereed is
- In het nieuwe Windows-besturings systeem voordat de-client is geïnstalleerd:`C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- In Windows nadat de client is geïnstalleerd:`C:\Windows\CCM\Logs\smstslog\smsts.log`
- In Windows nadat de taken reeks is voltooid:`C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> De alleen-lezen taken reeks variabele [_SMSTSLogPath](../../../osd/understand/task-sequence-variables.md#SMSTSLogPath) bevat altijd het pad van het huidige logboek bestand.


## <a name="see-also"></a>Zie ook

- [Naslag informatie over logboek bestanden](log-files.md)

- [Ondersteunings centrum OneTrace](../../support/support-center-onetrace.md)

- [Logboek bestand viewer voor ondersteunings centrum](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)

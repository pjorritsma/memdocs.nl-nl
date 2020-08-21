---
title: Status van de verbinding bewaken
titleSuffix: Configuration Manager
description: Meer informatie over het controleren van de verbindings status en de status van de apparaten voor desktop Analytics in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ecd8b83224cbcbfe367a3b1db160d680952a4407
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700834"
---
# <a name="monitor-connection-health"></a>Status van de verbinding bewaken

Gebruik het dash board **verbindings status** in Configuration Manager om in categorieën in te zoomen op de status van apparaten. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw het knoop punt **Desktop Analytics Servicing** uit en selecteer het dash board **verbindings status** .  

[![Scherm afbeelding van het dash board voor de Configuration Manager verbindings status](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

Wanneer u Desktop Analytics voor het eerst instelt, worden in deze grafieken mogelijk geen volledige gegevens weer gegeven. Het kan 2-3 dagen duren voordat actieve apparaten diagnostische gegevens verzenden naar de Desktop Analytics-service, de service voor het verwerken van de gegevens en vervolgens synchroniseren met uw Configuration Manager-site.<!-- 4098037 -->

## <a name="connection-details"></a>Verbindingsdetails

Deze tegel toont de volgende basis informatie over de verbinding van Configuration Manager naar Desktop Analytics:

- **Tenant naam**: de naam van de verbinding met de bureau blad Analytics in het knoop punt **Azure-Services**

- **Doel verzameling**: dezelfde *doel verzameling* die u hebt opgegeven bij het verbinden van Configuration Manager op Desktop Analytics. Deze verzameling bevat alle apparaten die Configuration Manager configureert met de instellingen voor uw commerciële ID en diagnostische gegevens. Het is de volledige set apparaten waarmee Configuration Manager verbinding maakt met de Desktop Analytics-service.

- **Doel apparaten**: alle apparaten in de doel verzameling, min de volgende typen apparaten:

  - Gesteld
  - Verouderd
  - Niet-actief
  - Niet-beheerd
  - Apparaten met LTSC-versies (Long term Servicing Channel) van Windows 10
  - Apparaten met Windows Server

    Zie [about client status](../core/clients/manage/monitor-clients.md#bkmk_about)(Engelstalig) voor meer informatie over deze Apparaatstatus.

    > [!Note]  
    > Configuration Manager uploads naar Desktop Analytics alle apparaten in de doel verzameling min buiten gebruik gesteld en verouderde clients.

- **Apparaten die in aanmerking komen voor da**: het aantal apparaten met het doel minus apparaten dat niet in aanmerking komt voor desktop Analytics. Bijvoorbeeld: apparaten in de doel verzameling met Windows Server of Windows 10-onderhouds kanaal voor lange termijn verwerking (LTSC).

## <a name="last-sync-details"></a>Details van de laatste synchronisatie

In deze tegel wordt weer gegeven wanneer Configuration Manager synchroniseert met de Cloud service van Desktop Analytics en hoeveel apparaten er worden gesynchroniseerd.

- **Gesynchroniseerde apparaten**: het aantal in aanmerking komende apparaten dat Configuration Manager verzonden naar Desktop Analytics. De service bevat deze apparaten in de huidige zicht bare moment opname.

- **Laatste service synchronisatie**: hetzelfde als het tijdstip waarop de update voor het **laatst is bijgewerkt** in de Desktop Analytics-Portal.

- **Volgende service Sync**: wanneer u de volgende dagelijkse moment opname in Desktop Analytics kunt verwachten.

> [!Note]  
> Wanneer u apparaten voor het eerst registreert bij Desktop Analytics, kan het enkele dagen duren voordat gegevens worden geüpload en verwerkt. Gedurende deze tijd kan de tegel **laatste synchronisatie Details** leeg zijn.
> Daarnaast worden geen van de waarden in deze tegel automatisch bijgewerkt wanneer u een moment opname op aanvraag aanvraagt. Zie [Data latentie](troubleshooting.md#data-latency)voor meer informatie.

Als u denkt dat sommige apparaten niet in Desktop Analytics worden weer gegeven, controleert u of de apparaten door Desktop Analytics worden ondersteund. Zie [vereisten](overview.md#prerequisites)voor meer informatie.

## <a name="connection-health"></a>Verbindings status

In het diagram **verbindings status** wordt het aantal apparaten in de volgende statussen weer gegeven:  

- [Correct Inge schreven](#properly-enrolled): het apparaat wordt weer gegeven in Desktop Analytics met een volledige inventarisatie
- [Kan niet inschrijven](#unable-to-enroll): er is een probleem met het blok keren waardoor de registratie van het apparaat wordt voor komen
- [Configuratie waarschuwing](#configuration-alert): het apparaat wordt niet weer gegeven in Desktop Analytics of wordt weer gegeven met een onvolledige inventarisatie. Configuration Manager heeft ook een probleem met de registratie van het apparaat geïdentificeerd.
- [Wachten op inschrijving](#awaiting-enrollment): Configuration Manager het apparaat niet geconfigureerd, maar het is nog niet weer gegeven in Desktop Analytics
- [Status in behandeling](#status-pending): Configuration Manager is nog bezig met het configureren van dit apparaat of heeft onvoldoende gegevens van het apparaat om de status te bepalen
- [Ontbrekende gegevens](#missing-data): Configuration Manager het apparaat geconfigureerd, maar Desktop Analytics heeft alleen gedeeltelijke gegevens

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

Het totale aantal apparaten in dit diagram moet hetzelfde zijn als de apparaten die in **aanmerking komen voor de da** -waarde in de tegel verbindings Details.

Selecteer het segment in het diagram om in te zoomen op een lijst met apparaten met die status. Zie [apparaten lijst](#device-list)voor meer informatie.

Selecteer de categorie naam in de legenda om deze uit de grafiek te verwijderen of toe te voegen. Met deze actie kunt u de grafiek in-en uitzoomen zodat u de relatieve grootten van kleinere segmenten ziet.

### <a name="properly-enrolled"></a>Goed Inge schreven

Het apparaat heeft de volgende kenmerken:

- Een Configuration Manager-client versie 1902 of hoger  
- Er zijn geen configuratie fouten  
- Desktop Analytics heeft de afgelopen 28 dagen volledige diagnostische gegevens ontvangen van dit apparaat  
- Desktop Analytics bevat een volledige inventarisatie van de configuratie van het apparaat en de geïnstalleerde apps  

### <a name="unable-to-enroll"></a>Kan niet registreren

Configuration Manager detecteert een of meer blokkerende problemen die de registratie van het apparaat verhinderen. Zie de lijst met eigenschappen van het [bureau blad Analytics in Configuration Manager](#bkmk_config-issues)voor meer informatie.  

Zo is de Configuration Manager-client niet ten minste versie 1902 (5.0.8790). Werk de client bij naar de nieuwste versie. Overweeg automatische client upgrade voor de Configuration Manager-site in te scha kelen. Zie [upgrade-clients](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)voor meer informatie.  

> [!TIP]
> Er is een bekend probleem met de Extended Security Update (ESU) van april 2020 voor Windows 7 waardoor apparaten deze fout niet kunnen rapporteren. Zie [release opmerkingen](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack)voor meer informatie.<!-- 7283186 -->

Vanaf versie 2002 kunt u problemen met de configuratie van de client proxy op twee gebieden gemakkelijker identificeren:

- **Controle van eind punten**: als clients geen vereist eind punt kunnen bereiken, ziet u een configuratie waarschuwing in het dash board. Inzoomen op clients die niet kunnen worden inge schreven om de eind punten te zien waarmee clients geen verbinding kunnen maken vanwege problemen met de proxy configuratie. Zie [controle van eind punten](#endpoint-connectivity-checks)voor meer informatie.<!-- 4963230 -->

- **Connectiviteits status**: als uw clients een proxy server gebruiken voor toegang tot Desktop Analytics, worden er Configuration Manager problemen met de proxy verificatie van clients weer gegeven. Inzoomen om te zien welke clients niet kunnen worden inge schreven vanwege problemen met de proxy verificatie. Zie [connectiviteits status](#connectivity-status)voor meer informatie.<!-- 4963383 -->

### <a name="configuration-alert"></a>Configuratie waarschuwing

Het apparaat wordt niet weer gegeven in Desktop Analytics of wordt weer gegeven met een onvolledige inventarisatie. Configuration Manager heeft ook een probleem met de registratie van het apparaat geïdentificeerd. Zie de lijst met eigenschappen van het [bureau blad Analytics in Configuration Manager](#bkmk_config-issues)voor meer informatie.

Het apparaat heeft bijvoorbeeld geen verbinding met de service. Zie [connectiviteit van Windows diagnostische eind punten](#windows-diagnostic-endpoint-connectivity)voor meer informatie.

### <a name="awaiting-enrollment"></a>Wachten op inschrijving

Desktop Analytics heeft geen diagnostische gegevens voor dit apparaat. Dit probleem kan worden veroorzaakt doordat u het apparaat onlangs hebt toegevoegd aan de doel verzameling en er nog geen gegevens zijn verzonden. Het kan ook betekenen dat het apparaat niet goed communiceert met de service en dat de meest recente diagnostische gegevens meer dan 28 dagen oud zijn.

Zorg ervoor dat het apparaat kan communiceren met de service. Zie [eind punten](enable-data-sharing.md#endpoints)voor meer informatie.  

### <a name="status-pending"></a>Status in behandeling

Configuration Manager is nog bezig met het configureren van dit apparaat of heeft onvoldoende gegevens van het apparaat om de status te bepalen.

### <a name="missing-data"></a>Ontbrekende gegevens

Configuration Manager het apparaat is geconfigureerd, maar er kan geen compatibiliteits beoordeling worden gemaakt met Desktop Analytics. Er is geen volledige gegevensset voor de configuratie van het apparaat (telling) of geïnstalleerde apps (inventarisatie).

Dit probleem wordt vaak automatisch opgelost wanneer het apparaat opnieuw probeert. Als dat het geval is, moet u controleren of het apparaat kan communiceren met de service. Zie [eind punten](enable-data-sharing.md#endpoints)voor meer informatie.  

## <a name="device-list"></a>Lijst met apparaten

Als u een specifieke lijst met apparaten op status wilt zien, begint u met het dash board **verbindings status** . Selecteer een van de segmenten van de tegel **verbindings status** en zoom in op een lijst met apparaten met deze status. In deze weer gave voor aangepaste apparaten wordt standaard de volgende Desktop Analytics-kolommen weer gegeven:

- Commerciële ID-configuratie
- Minimale compatibiliteits update
- Opt-in voor Windows diagnostische gegevens
- Windows Commercial data opt-in
- Windows diagnostische endpoint-connectiviteit
- Connectiviteits status (vanaf versie 2002)
- Controle van eind punten (vanaf versie 2002)

Deze kolommen komen overeen met de belangrijkste [vereisten](overview.md#prerequisites) voor apparaten die kunnen communiceren met Desktop Analytics.

[![Scherm opname van de apparaten lijst kan niet worden inge schreven](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

Selecteer een apparaat om de volledige lijst met beschik bare eigenschappen weer te geven in het detail venster. U kunt ook een van deze eigenschappen als kolommen toevoegen aan de lijst met apparaten.

## <a name="device-properties"></a><a name="bkmk_config-issues"></a> Apparaateigenschappen

De volgende eigenschappen van het bureau blad Analytics-apparaat zijn beschikbaar als kolommen in de lijst met apparaten van Configuration Manager:

- [Controle van eind punten](#endpoint-connectivity-checks) (vanaf versie 2002)
- [Connectiviteits status](#connectivity-status) (vanaf versie 2002)
- [Configuratie van de beoordeling](#appraiser-configuration)  
- [Minimale compatibiliteits update](#minimum-compatibility-update)  
- [Versie van de beoordeling](#appraiser-version)  
- [Laatste geslaagde volledige uitvoering van de beoordelings programma](#last-successful-full-run-of-appraiser)  
- [Gegevens verzameling van de beoordeling](#appraiser-data-collection)  
- [Laatste geslaagde volledige uitvoering van telling](#last-successful-full-run-of-census)  
- [Gegevens verzameling met tellingen](#census-data-collection)  
- [Windows diagnostische endpoint-connectiviteit](#windows-diagnostic-endpoint-connectivity)  
- [Diagnostische gegevens voor eind gebruikers controleren](#check-end-user-diagnostic-data)  
- [Gebruikers proxy controleren](#check-user-proxy)  
- [Commerciële ID-configuratie](#commercial-id-configuration)  
- [Windows Commercial data opt-in](#windows-commercial-data-opt-in)  
- [Controleer de naam van de apparaat in diagnostische gegevens](#check-device-name-in-diagnostic-data)  
- [Configuratie van DiagTrack-service](#diagtrack-service-configuration)  
- [DiagTrack-versie](#diagtrack-version)  
- [SQM-ID ophalen](#sqm-id-retrieval)  
- [Unieke apparaat-id ophalen](#unique-device-identifier-retrieval)  
- [Opt-in voor Windows diagnostische gegevens](#windows-diagnostic-data-opt-in)  

De tegel **inschrijvings blokkeringen en configuratie waarschuwingen** in het dash board status van de verbinding geeft de eigenschappen weer die apparaten het meest als een probleem rapporteren.

### <a name="endpoint-connectivity-checks"></a>Controle van eindpunt connectiviteit

Vanaf versie 2002,<!-- 4963230 --> voor het detecteren van problemen met proxy verificatie voeren clients connectiviteits controles uit op vereiste eind punten. Als een client een vereist eind punt niet kan bereiken, wordt met deze eigenschap een genummerde lijst met eind punten weer gegeven die geen verbinding kunnen maken vanwege problemen met de proxy configuratie. Vergelijk deze lijst met de gepubliceerde lijst met [vereiste eind punten](enable-data-sharing.md#endpoints).

### <a name="connectivity-status"></a>Connectiviteits status

Vanaf versie 2002,<!-- 4963383 --> Als uw clients een proxy server gebruiken voor toegang tot Desktop Analytics, toont deze eigenschap problemen met de proxy-verificatie. Het bevat de volgende gegevens met betrekking tot proxy verificatie:

- Statuscode
- Retourcode

Er worden fouten weer gegeven die vergelijkbaar zijn met het volgende in het logboek bestand:

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

Waarbij `%s` de URL is van een vereist eind punt.

Mogelijk ziet u ook niet-deterministische fout berichten die geen aandacht nodig hebben totdat apparaten registratie problemen ondervinden. Bijvoorbeeld:

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

Zie voor meer informatie over het configureren van proxy servers voor gebruik met Desktop Analytics verificatie van de [proxy server](enable-data-sharing.md#proxy-server-authentication).

### <a name="appraiser-configuration"></a>Configuratie van de beoordeling

<!--20,21-->
Beoordeling is het Windows-onderdeel dat overeenkomt met de [compatibiliteits updates](enroll-devices.md#update-devices). Hiermee worden de apps en stuur Programma's op het apparaat beoordeeld op compatibiliteit met de nieuwste versie van Windows.

Als deze controle is geslaagd, is het onderdeel van de beoordelings functie op de juiste wijze geconfigureerd op het apparaat.

Anders kan een van de volgende fouten worden weer gegeven:

- Kan de compatibiliteits gegevens verzameling voor de apparaat-app niet configureren (SetRequestAllAppraiserVersions). Raadpleeg de logboeken voor de uitzonderings Details  

- Kan de compatibiliteits gegevens verzameling voor de apparaat-app niet configureren (SetRequestAllAppraiserVersions). Raadpleeg de logboeken voor de uitzonderings Details  

- Kan de RequestAllAppraiserVersions niet naar de register sleutel schrijven `HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Appraiser` . Machtigingen controleren  

Controleer de machtigingen voor deze register sleutel. Zorg ervoor dat het lokale systeem account toegang heeft tot deze sleutel om de Configuration Manager-client in te stellen.  

Raadpleeg M365AHandler. log op de client voor meer informatie.  

### <a name="minimum-compatibility-update"></a>Minimale compatibiliteits update

<!--18,19,32-->
De compatibiliteits update (appraiser.dll) is niet geïnstalleerd of verouderd op het apparaat. Het is ouder dan de minimum vereiste voor desktop Analytics, 10.0.17763.

Installeer de meest recente compatibiliteits update. Zie [Compatibility updates](enroll-devices.md#update-devices)(Engelstalig) voor meer informatie.

### <a name="appraiser-version"></a>Versie van de beoordeling

Met deze eigenschap wordt de huidige versie van het onderdeel van de component beoordeling op het apparaat weer gegeven. Het bevat de bestands versie op `%windir%\System32\appraiser.dll` , zonder de decimale punten. Bestands versie 10.0.17763 wordt bijvoorbeeld weer gegeven als 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Laatste geslaagde volledige uitvoering van de beoordelings programma

Met deze eigenschap worden de datum en tijd weer gegeven waarop het apparaat de laatste keer is uitgevoerd.

### <a name="appraiser-data-collection"></a>Gegevens verzameling van de beoordeling

<!--Appraiser run status-->
<!--22,33-->
Met deze eigenschap wordt het laatste resultaat weer gegeven van Windows waarop het onderdeel van de beoordeling wordt uitgevoerd.

Als dat niet lukt, kan er een van de volgende fouten worden weer gegeven:

- Kan geen app-compatibiliteits gegevens verzamelen (RunAppraiser). Raadpleeg de logboeken voor meer informatie  

- App Compatibility Data Collection (CompatTelRunner.exe) is beëindigd met een fout code  

Raadpleeg M365AHandler. log op de client voor meer informatie.

Controleer het volgende bestand: `%windir%\System32\CompatTelRunner.exe` . Als deze niet bestaat, installeert u de vereiste [compatibiliteits updates](enroll-devices.md#update-devices)opnieuw. Zorg ervoor dat er geen ander systeem onderdeel is om dit bestand te verwijderen, zoals groeps beleid of een antimalware-service.

Als het bestand M365AHandler. log op de client een van de volgende fouten bevat:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Voer de volgende opdrachten uit vanuit een Windows Power shell-console met verhoogde bevoegdheden op de betreffende client om deze fouten te herstellen:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Laatste geslaagde volledige uitvoering van telling

Met deze eigenschap worden de datum en tijd weer gegeven waarop het apparaat voor het laatst een inventarisatie heeft uitgevoerd.

### <a name="census-data-collection"></a>Gegevens verzameling met tellingen

<!-- Census run status -->
<!--51,52-->
Tellingen is het Windows-onderdeel dat het apparaat inventariseert. Deze inventarisatie gegevens worden gebruikt om inzicht te krijgen in het apparaat en de configuratie.

Deze eigenschap toont het laatste resultaat van Windows waarop het onderdeel voor de telling wordt uitgevoerd.

Als dat niet lukt, kan er een van de volgende fouten worden weer gegeven:

- Kan geen gegevens verzamelen over het apparaat en de configuratie (RunCensus). Raadpleeg de logboeken voor de uitzonderings Details  

- Het hulp programma voor het verzamelen van apparaat-en configuratie gegevens (devicecensus.exe) is niet gevonden  

Raadpleeg M365AHandler. log op de client voor meer informatie.

Controleer het volgende bestand: `%windir%\System32\DeviceCensus.exe` . Als deze niet bestaat, installeert u de vereiste [compatibiliteits updates](enroll-devices.md#update-devices)opnieuw. Zorg ervoor dat er geen ander systeem onderdeel is om dit bestand te verwijderen, zoals groeps beleid of een antimalware-service.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Windows diagnostische endpoint-connectiviteit

<!--12,15-->
Als deze controle is geslaagd, kan het apparaat verbinding maken met de verbonden gebruikers ervaring en het telemetrie-eind punt (Vortex).

Anders kan een van de volgende fouten worden weer gegeven:  

- Kan geen verbinding maken met de verbonden gebruikers ervaring en het telemetrie-eind punt (Vortex). Controleer uw netwerk/proxy-instellingen  

- Kan geen verbinding controleren met de verbonden gebruikers ervaring en het telemetrie-eind punt (CheckVortexConnectivity). Raadpleeg de logboeken voor de uitzonderings Details  

Apparaten verifiëren de connectiviteit met een GET-aanvraag voor het volgende eind punt op basis van de versie van het besturings systeem:

| Besturingssysteemversie | Eindpunt |
|------------|----------|
| -Windows 10, versie 1809 of hoger<br/>-Windows 10, versie 1803 met de cumulatieve update van 2018-09 of hoger | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, versie 1803 *zonder* de cumulatieve update van 2018-09 of hoger | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versie 1709 of lager | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 of Windows 8,1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Zorg ervoor dat het apparaat kan communiceren met de service. Met deze controle worden enkele, maar niet alle vereiste eind punten gevalideerd. Zie [eind punten](enable-data-sharing.md#endpoints)voor meer informatie.  

Raadpleeg M365AHandler. log op de client voor meer informatie.  

### <a name="check-end-user-diagnostic-data"></a>Diagnostische gegevens voor eind gebruikers controleren

<!--1004-->
Als deze controle mislukt, een gebruiker heeft een lagere diagnostische gegevens van Windows op het apparaat geselecteerd. Dit kan ook worden veroorzaakt door een conflicterende groeps beleidsobject. Zie [Windows-instellingen](enroll-devices.md#windows-settings)voor meer informatie.

Afhankelijk van uw bedrijfs vereisten kunt u de gebruikers keuze uitschakelen via groeps beleid. Gebruik de instelling voor het **configureren van de aanmeldings instellingen voor telemetrie voor het instellen van de gebruikers interface**. Zie [Diagnostische gegevens van Windows in uw organisatie configureren](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management) voor meer informatie.

### <a name="check-user-proxy"></a>Gebruikers proxy controleren

<!--30,35-->
De instelling DisableEnterpriseAuthProxy is standaard ingeschakeld voor Windows 7. Voor Windows 8,1-computers stelt Configuration Manager de instelling DisableEnterpriseAuthProxy in op 0 (niet uitgeschakeld).

Met deze eigenschap kunnen de volgende fouten worden weer gegeven:

- Verificatie proxy is ingeschakeld. Stel DisableEnterpriseAuthProxy in op 0 in `HKLM:\Software\Policies\Microsoft\Windows\DataCollection`

- Kan niet controleren op de status van de verificatie proxy. Raadpleeg de logboeken voor de uitzonderings Details

Raadpleeg M365AHandler. log op de client voor meer informatie.  

Controleer de machtigingen voor deze register sleutel. Zorg ervoor dat het lokale systeem account toegang heeft tot deze sleutel om de Configuration Manager-client in te stellen. Dit kan ook worden veroorzaakt door een conflicterende groeps beleidsobject. Zie [Windows-instellingen](enroll-devices.md#windows-settings)voor meer informatie.  

### <a name="commercial-id-configuration"></a>Commerciële ID-configuratie

<!--9, 11, 53-->
Micro soft gebruikt een unieke commerciële ID om gegevens van apparaten toe te wijzen aan de werk ruimte van uw bureau blad Analytics. Wanneer u Configuration Manager integreert met Desktop Analytics, wordt de service automatisch voor deze ID opgevraagd. Configuration Manager moet deze ID automatisch Toep assen op clients waarop u de instellingen voor desktop Analytics hebt ingesteld.

Als deze controle is geslaagd, is het apparaat op de juiste wijze geconfigureerd met een commerciële ID.

Anders kan een van de volgende fouten worden weer gegeven:

- Kan de CommercialId niet naar de register sleutel schrijven `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` . Machtigingen controleren  

- Kan de CommercialId in de register sleutel niet bijwerken `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` . Raadpleeg de logboeken voor de uitzonderings Details  

- Geef de juiste CommercialId-waarde op `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Raadpleeg M365AHandler. log op de client voor meer informatie.  

Controleer de machtigingen voor deze register sleutel. Zorg ervoor dat het lokale systeem account toegang heeft tot deze sleutel om de Configuration Manager-client in te stellen. Dit kan ook worden veroorzaakt door een conflicterende groeps beleidsobject. Zie [Windows-instellingen](enroll-devices.md#windows-settings)voor meer informatie.  

Er is een andere ID voor het apparaat. Deze register sleutel wordt gebruikt door groeps beleid. Het heeft voor rang op de ID van Configuration Manager.  

<a name="bkmk_ViewCommercialID"></a> Gebruik de volgende procedure om de commerciële ID in de Desktop Analytics-portal weer te geven:

1. Ga naar de Desktop Analytics-Portal en selecteer **verbonden services** in de groep globale instellingen.  

2. In het deel venster **verbonden services** is het deel venster **apparaten inschrijven** standaard geselecteerd. In het deel venster apparaten inschrijven wordt in de sectie informatie uw commerciële ID-sleutel weer gegeven.  

[![Scherm opname van commerciële ID in de Desktop Analytics-Portal](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> Haal alleen een **nieuwe ID-sleutel** op wanneer u de huidige niet kunt gebruiken. Als u de commerciële ID opnieuw genereert, moet u [uw apparaten opnieuw inschrijven met de nieuwe id](enroll-devices.md#device-enrollment). Dit proces kan leiden tot verlies van diagnostische gegevens tijdens de overgang.  

### <a name="windows-commercial-data-opt-in"></a>Windows Commercial data opt-in

<!--64-->
Deze eigenschap is specifiek voor apparaten met Windows 7 of Windows 8,1. Dit voert soort gelijke tests [uit als opt-in voor Windows diagnostische gegevens](#windows-diagnostic-data-opt-in), met uitzonde ring van de waarde CommercialDataOptIn.

### <a name="check-device-name-in-diagnostic-data"></a>Controleer de naam van de apparaat in diagnostische gegevens

<!--56,58-->
Als deze controle is geslaagd, is het apparaat op de juiste wijze geconfigureerd voor het delen van de apparaatnaam.

Anders kan een van de volgende fouten worden weer gegeven:

- Kan niet controleren of de apparaatnaam naar micro soft moet worden verzonden als onderdeel van de diagnostische gegevens van Windows. Raadpleeg de logboeken voor de uitzonderings Details  

- Kan AllowDeviceNameInTelemetry niet naar de register sleutel schrijven `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection` . Machtigingen controleren  

Raadpleeg M365AHandler. log op de client voor meer informatie.  

Controleer de machtigingen voor deze register sleutel. Zorg ervoor dat het lokale systeem account toegang heeft tot deze sleutel om de Configuration Manager-client in te stellen. Dit kan ook worden veroorzaakt door een conflicterende groeps beleidsobject. Zie [Windows-instellingen](enroll-devices.md#windows-settings)voor meer informatie.  

Zorg ervoor dat een ander beleids mechanisme, zoals groeps beleid, de instelling niet uitschakelt.

### <a name="diagtrack-service-configuration"></a>Configuratie van DiagTrack-service

<!--44,45,50-->
Als deze controle is geslaagd, is het DiagTrack-onderdeel op de juiste wijze geconfigureerd op het apparaat. De mini maal vereiste versie van Desktop Analytics is 10010586 (10.0.10586).

Anders kan een van de volgende fouten worden weer gegeven:

- Het onderdeel verbonden gebruikers ervaring en telemetrie (diagtrack.dll) is verouderd. Vereisten controleren  

    > [!TIP]
    > Er is een bekend probleem met de Extended Security Update (ESU) van april 2020 voor Windows 7 waardoor apparaten deze fout niet kunnen rapporteren. Zie [release opmerkingen](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack)voor meer informatie.<!-- 7283186 -->

- Kan het onderdeel verbonden gebruikers ervaring en telemetrie (diagtrack.dll) niet vinden. Vereisten controleren  

- De verbonden gebruikers ervaringen en telemetrie-service inschakelen en starten om gegevens te verzenden naar micro soft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Installeer de laatste updates. Zie [updates voor apparaten](enroll-devices.md#update-devices)voor meer informatie.

Zorg ervoor dat de **verbonden gebruikers ervaring en telemetrie** -service op het apparaat wordt uitgevoerd.

### <a name="diagtrack-version"></a>DiagTrack-versie

Met deze eigenschap wordt de huidige versie van de verbonden gebruikers ervaring en het telemetrie-onderdeel op het apparaat weer gegeven. Het bevat de bestands versie op `%windir%\System32\diagtrack.dll` , zonder de decimale punten. Bestands versie 10.0.10586 wordt bijvoorbeeld weer gegeven als 10010586.

### <a name="sqm-id-retrieval"></a>SQM-ID ophalen

<!--38-->
Deze eigenschap is voornamelijk bedoeld voor Windows 7-apparaten. Deze kan worden gebruikt door latere versies van het besturings systeem als een terugval-id voor het apparaat.

Als dat niet lukt, wordt mogelijk de volgende fout weer gegeven:

- Kan de verouderde telemetrie-id van het apparaat niet ophalen (SQM-ID)

Raadpleeg M365AHandler. log op de client voor meer informatie.  

Zorg ervoor dat u geen dubbele Id's in uw omgeving hebt. Als er bijvoorbeeld apparaten zijn geïmplementeerd met een installatie kopie van het besturings systeem die niet is gegeneraliseerd.

### <a name="unique-device-identifier-retrieval"></a>Unieke apparaat-id ophalen

<!--54-->
Desktop Analytics maakt gebruik van de micro soft-account service voor een betrouwbaardere apparaat-id.

Zorg ervoor dat de service **micro soft-account aanmeld hulp** niet is uitgeschakeld. Het opstart type moet **hand matig zijn (start activeren)**.

Als u Microsoft-account toegang door eind gebruikers wilt uitschakelen, gebruikt u de beleids instellingen in plaats van dit eind punt te blok keren. Zie [de Microsoft-account in de onderneming](/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)voor meer informatie.

### <a name="windows-diagnostic-data-opt-in"></a>Opt-in voor Windows diagnostische gegevens

<!--8,40,55,62-->
Met deze eigenschap wordt gecontroleerd of Windows correct is geconfigureerd om diagnostische gegevens toe te staan. Hiermee wordt de AllowTelemetry-waarde in de volgende register sleutels gecontroleerd:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Controleer de machtigingen voor deze register sleutels. Zorg ervoor dat het lokale systeem account toegang heeft tot deze sleutels om de Configuration Manager-client in te stellen. Dit kan ook worden veroorzaakt door een conflicterende groeps beleidsobject. Zie [Windows-instellingen](enroll-devices.md#windows-settings)voor meer informatie.  

Raadpleeg M365AHandler. log op de client voor meer informatie.  

## <a name="see-also"></a>Zie ook

[Problemen met Desktop Analytics oplossen](troubleshooting.md)
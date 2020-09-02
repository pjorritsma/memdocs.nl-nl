---
title: Instellingen van het Antivirus-beleid voor Windows 10 van Microsoft Defender Antivirus voor apparaten met tenantkoppeling | Microsoft Docs
description: Bekijk een lijst met de instellingen in het Microsoft Defender Antivirus-profiel voor Windows 10-apparaten beheerd door Configuration Manager. U kunt deze instellingen configureren als onderdeel van het antivirusbeleid voor eindpuntbeveiliging in Microsoft Intune nadat u tenantkoppeling configureert voor Configuration Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 3bb1d4806271ab40c60f0ad419e4e708d36bbc97
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194120"
---
# <a name="settings-for-microsoft-defender-antivirus-policy-for-tenant-attached-devices-in-microsoft-intune"></a>Instellingen voor het Antivirus-beleid van Microsoft Defender voor apparaten met tenantkoppeling in Microsoft Intune

Bekijk de instellingen van Microsoft Defender Antivirus die u kunt beheren met het **Microsoft Defender Antivirus-beleid (ConfigMgr)** -profiel van Intune. Het profiel is beschikbaar wanneer u het [Antivirus-beleid voor eindpuntbeveiliging](../protect/endpoint-security-antivirus-policy.md) configureert in Intune en het beleid wordt geïmplementeerd op apparaten die u beheert met Configuration Manager wanneer u het scenario [tenantkoppeling](../protect/tenant-attach-intune.md) hebt geconfigureerd.

## <a name="cloud-protection"></a>Cloudbeveiliging

- **Cloudbeveiliging inschakelen**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Standaard stuurt Defender op desktopapparaten met Windows 10 informatie naar Microsoft over eventuele gevonden problemen. Microsoft analyseert die gegevens om meer te weten te komen over problemen die u en andere klanten ondervinden, om verbeterde oplossingen te kunnen bieden.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Niet toegestaan.** Hiermee wordt de Microsoft Active Protection Service uitgeschakeld.
  - **Toegestaan.**  Hiermee wordt de Microsoft Active Protection Service ingeschakeld.

- **Cloudbeveiligingsniveau**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configureer hoe strikt Defender Antivirus te werk gaat bij het blokkeren en scannen van verdachte bestanden.
  - **Niet geconfigureerd** (*standaard*): standaardblokkeringsniveau van Defender.
  - **Hoog**: onbekende bestanden wordt strikt geblokkeerd met optimalisatie van clientprestaties. Dit kan leiden tot meer onterechte positieven.
  - **Hoog plus**: onbekende bestanden wordt strikt geblokkeerd met toepassing van aanvullende beveiligingsmaatregelen die invloed kunnen hebben op clientprestaties.
  - **Zero tolerance**: alle onbekende uitvoerbare bestanden worden geblokkeerd.

- **Verlengde time-out van Windows Defender-cloud in seconden**  
  CSP: [CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus blokkeert automatisch verdachte bestanden gedurende tien seconden, zodat de bestanden in de cloud kunnen worden gescand om er zeker van te zijn dat ze veilig zijn. Met deze instelling kunt u maximaal 50 seconden extra toevoegen aan deze time-out.

## <a name="microsoft-defender-antivirus-exclusions"></a>Uitsluitingen voor Microsoft Defender Antivirus

Voor elke instelling in deze groep kunt u de instelling uitvouwen, **Toevoegen** selecteren en vervolgens een waarde voor de uitsluiting opgeven.

- **Defender-processen die moeten worden uitgesloten**  
  CSP: [ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Geef een lijst op met bestanden die door processen worden geopend en die u wilt negeren tijdens een scan. Het proces zelf wordt niet uitgesloten van de scan.

- **Bestandsextensies die moeten worden uitgesloten van scans en de realtime-beveiliging**  
  CSP: [ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Geef een lijst op met bestandsextensies die moeten worden genegeerd tijdens een scan.

- **Defender-bestanden en -mappen die moeten worden uitgesloten**  
  CSP: [ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Geef een lijst op met bestanden en mappaden die tijdens een scan moeten worden genegeerd.

## <a name="real-time-protection"></a>Realtime-beveiliging

- **Realtime-beveiliging inschakelen**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Vereis dat Defender op Windows 10-desktopapparaten gebruikmaakt van de realtime-bewakingsfunctionaliteit.
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Niet toegestaan.** Hiermee wordt de realtimebewakingsservice uitgeschakeld.
  - **Toegestaan.** Hiermee wordt de realtimebewakingsservice ingeschakeld en uitgevoerd.

- **Beveiliging bij toegang inschakelen**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Configureer virusbeveiliging die voortdurend actief is, in plaats van op aanvraag.

  - **Niet geconfigureerd** (*standaard*): dit beleid verandert niet de status van deze instelling op een apparaat. De bestaande status op het apparaat verandert niet.
  - **Niet toegestaan.** Hiermee wordt de realtimebewakingsservice uitgeschakeld.
  - **Toegestaan.**

- **Controleren op inkomende en uitgaande bestanden**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Configureer deze instelling om te bepalen welk NTFS-bestand en welke programma-activiteit wordt gecontroleerd.
  - **Alle bestanden controleren (in twee richtingen).** (*standaard*)
  - **Binnenkomende bestanden controleren.**
  - **Uitgaande bestanden controleren.**

- **Gedragscontrole inschakelen**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Standaard maakt Defender op desktopapparaten met Windows 10 gebruik van Gedragscontrole.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Niet toegestaan.** Hiermee wordt gedragscontrole uitgeschakeld.
  - **Toegestaan.** Hiermee wordt de bewaking van realtimegedrag ingeschakeld.

- **Inbraakpreventiesysteem toestaan**  
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Niet toegestaan.**
  - **Toegestaan.**

- **Alle gedownloade bestanden en bijlagen scannen**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Configureer Defender zo dat alle gedownloade bestanden en bijlagen worden gescand.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Niet toegestaan.**
  - **Toegestaan.**

- **Scripts scannen die in Microsoft-browsers worden gebruikt**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Configureer Defender voor het scannen van scripts.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Niet toegestaan.**
  - **Toegestaan.**

- **Netwerkbestanden scannen**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Configureer Defender voor het scannen van netwerkbestanden.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Niet toegestaan.** Hiermee wordt scannen van netwerkbestanden uitgeschakeld.
  - **Toegestaan.** Scant netwerkbestanden.

- **E-mails scannen**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Configureer Defender voor het scannen van inkomende e-mail.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Niet toegestaan.** Hiermee wordt scannen van e-mail uitgeschakeld.
  - **Toegestaan.** Hiermee wordt scannen van e-mail ingeschakeld.

## <a name="remediation"></a>Herstel

- **Aantal dagen (0-90) voor het bewaren van schadelijke software in quarantaine**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Geef een aantal dagen op van nul tot 90, gedurende welke het systeem in quarantaine geplaatste items bewaart voordat ze automatisch worden verwijderd. Met de waarde nul blijven items in quarantaine staan en worden ze niet automatisch verwijderd.

- **Toestemming voor voorbeelden verzenden**  

  - **Niet geconfigureerd** (*standaard*)
  - **Altijd vragen.**
  - **Veilige voorbeelden automatisch verzenden.**
  - **Nooit verzenden.**
  - **Alle voorbeelden automatisch verzenden.**

- **Uit te voeren actie tegen mogelijk ongewenste apps**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Geef het detectieniveau op voor mogelijk ongewenste toepassingen (PUA's). Defender waarschuwt gebruikers wanneer mogelijk ongewenste software wordt gedownload of op een apparaat wordt geïnstalleerd.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard. Dat wil zeggen dat PUA-beveiliging is uitgeschakeld.
  - **PUA-beveiliging uit.** Windows Defender biedt geen beveiliging tegen mogelijk ongewenste toepassingen.
  - **PUA-beveiliging aan.** Gedetecteerde items worden geblokkeerd. Deze worden weergegeven in de geschiedenis, samen met andere dreigingen.
  - **Controlemodus.** Defender detecteert mogelijk ongewenste toepassingen, maar neemt geen verdere acties. U kunt informatie nalezen over de toepassingen waartegen Windows Defender actie zou hebben ondernomen, door te zoeken naar gebeurtenissen die door Windows Defender in Logboeken zijn gemaakt.

- **Een systeemherstelpunt maken voordat de computers worden opgeschoond**  
  - **Ja** (*standaard*)
  - **Nee**
  - **Niet geconfigureerd**

- **Acties voor gedetecteerde bedreigingen**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Geef de actie op die door Microsoft Defender moeten worden uitgevoerd voor gedetecteerde schadelijke software op basis van het bedreigingsniveau van de malware.
  
  Defender classificeert gedetecteerde malware volgens een van de volgende ernstniveaus:
  - **Weinig bedreiging**
  - **Gemiddelde bedreiging**
  - **Grote bedreiging**
  - **Ernstige bedreiging**

  Voor elk niveau geeft u de actie op die moet worden uitgevoerd. De standaardinstelling voor elk ernstniveau is *Niet geconfigureerd*.

  - **Niet geconfigureerd** (*standaard*)
  - **Opschonen**: de service probeert bestanden te herstellen en te desinfecteren.
  - **Quarantaine**: bestanden worden verplaatst naar quarantaine.
  - **Verwijderen**: bestanden worden van het apparaat verwijderd.
  - **Toestaan**: hiermee staat u het bestand toe en worden er geen andere acties uitgevoerd.
  - **Door gebruiker gedefinieerd**: de apparaatgebruiker beslist welke actie er moet worden ondernomen.
  - **Blokkeren**: de uitvoering van bestanden wordt geblokkeerd.

## <a name="scan"></a>Scannen

- **Archiefbestanden scannen**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Configureer Defender om archiefbestanden, zoals ZIP- of CAB-bestanden, te scannen.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardwaarde van de client, namelijk het scannen van gearchiveerde bestanden. De gebruiker kan de scan echter uitschakelen.
Meer informatie
  - **Niet toegestaan** Hiermee wordt het scannen van gearchiveerde bestanden uitgeschakeld.
  - **Toegestaan.** Hiermee worden de archiefbestanden gescand.

- **Lage CPU-prioriteit inschakelen voor geplande scans**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Configureer CPU-prioriteit voor geplande scans.
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard. Dat betekent dat er geen wijzigingen in de CPU-prioriteit worden aangebracht.
  - **Uitgeschakeld**
  - **Ingeschakeld**

- **Volledige inhaalscan uitschakelen**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Configureer inhaalscans voor geplande volledige scans. Een inhaalscan is een scan die wordt gestart omdat een regelmatig geplande scan is gemist. Normaal gesproken zijn deze geplande scans niet uitgevoerd omdat de computer op het geplande tijdstip was uitgeschakeld.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client. Dat betekent dat inhaalscans voor volledige scans zijn ingeschakeld. De gebruiker kan deze echter uitschakelen.
  - **Uitgeschakeld**
  - **Ingeschakeld**

- **Snelle inhaalscan uitschakelen**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Configureer inhaalscans voor geplande snelle scans. Een inhaalscan is een scan die wordt gestart omdat een regelmatig geplande scan is gemist. Normaal gesproken zijn deze geplande scans niet uitgevoerd omdat de computer op het geplande tijdstip was uitgeschakeld.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client. Dat betekent dat snelle inhaalscans zijn ingeschakeld. De gebruiker kan deze echter uitschakelen.
  - **Uitgeschakeld**
  - **Ingeschakeld**

- **Limiet voor CPU-gebruik (0-100 procent) per scan**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Geef de limiet op als een percentage tussen nul en 100, de gemiddelde CPU-belastingsfactor voor de Defender-scan.

- **Inschakelen dat toegewezen netwerkschijven worden gescand tijdens een volledige scan**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Configureer Defender voor het scannen van toegewezen netwerkstations.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard. Dat wil zeggen dat het scannen van toegewezen netwerkstations is uitgeschakeld.
  - **Niet toegestaan.** Scannen uitschakelen op toegewezen netwerkstations.
  - **Toegestaan.** Scant toegewezen netwerkstations.

- **Dagelijkse snelle scan uitvoeren om**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Selecteer het tijdstip waarop Defender snelle scans moet uitvoeren.
  Deze optie is standaard **Niet geconfigureerd**

- **Type scan**  
  CSP: [ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  Selecteer het type scan dat Defender moet uitvoeren.

  - **Niet geconfigureerd** (*standaard*)
  - **Snelle scan**
  - **Volledige scan**

- **Dag van de week waarop een geplande scan moet worden uitgevoerd**  
  - **Niet geconfigureerd** (*standaard*)

- **Tijdstip waarop een geplande scan moet worden uitgevoerd**  
  - **Niet geconfigureerd** (*standaard*)

- **Controleren op handtekeningen voordat de scan wordt uitgevoerd**  
  - **Niet geconfigureerd** (*standaard*)
  - **Uitgeschakeld**
  - **Ingeschakeld**

- **Begintijden van geplande update van scan- en beveiligingsintelligentie randomiseren**  
  -**Niet geconfigureerd** (*standaard*) -**Ja**
  -**Nee**

- **Verwijderbare stations scannen tijdens een volledige scan**
  - **Niet geconfigureerd** (*standaard*)
  - **Niet toegestaan.** Hiermee wordt het scannen van verwisselbare stations uitgeschakeld.
  - **Toegestaan.** Scant verwisselbare stations.

## <a name="updates"></a>Updates

- **Voer in hoe vaak (0-24 uur) er moet worden gecontroleerd op updates van de beveiligingsinformatie**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Geef een interval van nul tot 24 (in uren) op dat wordt gebruikt om op handtekeningen te controleren. De waarde nul betekent dat er niet wordt gecontroleerd op nieuwe handtekeningen. Met de waarde 2 wordt elke twee uur gecontroleerd, enzovoort.

- **Volgorde van terugval voor handtekeningupdates (apparaat)**

- **Bronnen voor bestandsshares voor handtekeningupdates (apparaat)**

- **Locatie van beveiligingsintelligentie (apparaat)**  

## <a name="user-experience"></a>Gebruikerservaring

- **Gebruikerstoegang tot de Microsoft Defender-app blokkeren**  
  - **Niet geconfigureerd** (*standaard*)
  - **Niet toegestaan.** Voorkomt dat gebruikers toegang hebben tot de gebruikersinterface.
  - **Toegestaan.** Hiermee krijgen gebruikers toegang tot de gebruikersinterface.

- **Meldingen op de clientcomputer weergeven wanneer de gebruiker een volledige scan moet uitvoeren, de beveiligingsintelligentie moet bijwerken of Windows Defender Offline moet uitvoeren**  
  - **Niet geconfigureerd** (*standaard*)
  - **Ja**
  - **Nee**

- **De clientgebruikersinterface uitschakelen**  
  - **Niet geconfigureerd** (*standaard*)
  - **Ja**
  - **Nee**

- **Alle gebruikers toestaan de volledige geschiedenisresultaten weer te geven**
  - **Niet geconfigureerd** (*standaard*)
  - **Ja**
  - **Nee**
---
title: Instellingen van het Antivirus-beleid voor Windows 10 voor Microsoft Defender Antivirus voor Intune | Microsoft Docs
description: Bekijk een lijst met de instellingen in het Microsoft Defender Antivirus-profiel voor Windows 10. U kunt deze instellingen configureren als onderdeel van het antivirusbeleid voor eindpuntbeveiliging in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
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
ms.openlocfilehash: 554bc09aa57306010069df4a85baa70fafdc41a6
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086673"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Instellingen voor het Microsoft Defender Antivirus-beleid voor Windows 10 in Microsoft Intune

Bekijk de instellingen voor het Antivirus-profiel die u kunt configureren voor het Microsoft Defender Antivirus-profiel voor Windows 10 in Microsoft Intune.

## <a name="cloud-protection"></a>Cloudbeveiliging

- **Cloudbeveiliging inschakelen**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Standaard stuurt Defender op desktopapparaten met Windows 10 informatie naar Microsoft over eventuele gevonden problemen. Microsoft analyseert die gegevens om meer te weten te komen over problemen die u en andere klanten ondervinden, om verbeterde oplossingen te kunnen bieden.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: cloudbeveiliging is ingeschakeld.  Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Cloudbeveiligingsniveau**  
  CSP: [CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configureer hoe strikt Defender Antivirus te werk gaat bij het blokkeren en scannen van verdachte bestanden.
  - **Niet geconfigureerd** (*standaard*): standaardblokkeringsniveau van Defender.
  - **Hoog**: onbekende bestanden wordt strikt geblokkeerd met optimalisatie van clientprestaties. Dit kan leiden tot meer onterechte positieven.
  - **Hoog plus**: onbekende bestanden wordt strikt geblokkeerd met toepassing van aanvullende beveiligingsmaatregelen die invloed kunnen hebben op clientprestaties.
  - **Zero tolerance**: alle onbekende uitvoerbare bestanden worden geblokkeerd.

- **Verlengde time-out van Windows Defender-cloud in seconden**  
  CSP: [CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus blokkeert automatisch verdachte bestanden gedurende tien seconden, zodat de bestanden in de cloud kunnen worden gescand om er zeker van te zijn dat ze veilig zijn. Met deze instelling kunt u maximaal 50 seconden extra toevoegen aan deze time-out.

## <a name="microsoft-defender-antivirus-exclusions"></a>Uitsluitingen voor Microsoft Defender Antivirus

Voor elke instelling in deze groep kunt u de instelling uitvouwen, **Toevoegen** selecteren en vervolgens een waarde voor de uitsluiting opgeven.

- **Defender-processen die moeten worden uitgesloten**  
  CSP: [ExcludedProcesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Geef een lijst op met bestanden die door processen worden geopend en die u wilt negeren tijdens een scan. Het proces zelf wordt niet uitgesloten van de scan.

- **Bestandsextensies die moeten worden uitgesloten van scans en de realtime-beveiliging**  
  CSP: [ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Geef een lijst op met bestandsextensies die moeten worden genegeerd tijdens een scan.

- **Defender-bestanden en -mappen die moeten worden uitgesloten**  
  CSP: [ExcludedPaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Geef een lijst op met bestanden en mappaden die tijdens een scan moeten worden genegeerd.

## <a name="real-time-protection"></a>Realtime-beveiliging

- **Realtime-beveiliging inschakelen**  
  CSP: [AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Vereis dat Defender op Windows 10-desktopapparaten gebruikmaakt van de realtime-bewakingsfunctionaliteit.
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het gebruik van realtime-bewaking wordt afgedwongen. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Beveiliging bij toegang inschakelen**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  Configureer virusbeveiliging die voortdurend actief is, in plaats van op aanvraag.

  - **Niet geconfigureerd** (*standaard*): dit beleid verandert niet de status van deze instelling op een apparaat. De bestaande status op het apparaat verandert niet.
  - **Nee**: beveiliging bij toegang blokkeren op apparaten. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: beveiliging bij toegang is actief op apparaten.

- **Gedragscontrole inschakelen**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  Standaard maakt Defender op desktopapparaten met Windows 10 gebruik van Gedragscontrole.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het gebruik van realtime-gedragscontrole wordt afgedwongen. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Netwerkbeveiliging inschakelen**  
  CSP: [EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Bescherm apparaatgebruikers die gebruikmaken van een app tegen het openen van phishing-praktijken, sites die schadelijke software hosten en schadelijke inhoud op internet. Beveiliging omvat het voorkomen dat browsers van derden verbinding maken met gevaarlijke websites.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: netwerkbeveiliging is ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Alle gedownloade bestanden en bijlagen scannen**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)

  Configureer Defender zo dat alle gedownloade bestanden en bijlagen worden gescand.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: Defender scant alle gedownloade bestanden en bijlagen. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Scripts scannen die in Microsoft-browsers worden gebruikt**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  Configureer Defender voor het scannen van scripts.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: Defender scant scripts. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Netwerkbestanden scannen**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  Configureer Defender voor het scannen van netwerkbestanden.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het scannen van netwerkbestanden is ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **E-mails scannen**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  Configureer Defender voor het scannen van inkomende e-mail.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het scannen van e-mail is ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

## <a name="remediation"></a>Herstel

- **Aantal dagen (0-90) voor het bewaren van schadelijke software in quarantaine**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  Geef een aantal dagen op van nul tot 90, gedurende welke het systeem in quarantaine geplaatste items bewaart voordat ze automatisch worden verwijderd. Met de waarde nul blijven items in quarantaine staan en worden ze niet automatisch verwijderd.

- **Toestemming voor voorbeelden verzenden**  

  - **Niet geconfigureerd** (*standaard*)
  - **Veilige voorbeelden automatisch verzenden**
  - **Altijd vragen**
  - **Nooit verzenden**
  - **Alle voorbeelden automatisch verzenden**

- **Uit te voeren actie tegen mogelijk ongewenste apps**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051&clcid=0x409)

  Geef het detectieniveau op voor mogelijk ongewenste toepassingen (PUA's). Defender waarschuwt gebruikers wanneer mogelijk ongewenste software wordt gedownload of op een apparaat wordt geïnstalleerd.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard. Dat wil zeggen dat PUA-beveiliging is uitgeschakeld.
  - **Uitschakelen**
  - **Inschakelen**: Gedetecteerde items worden geblokkeerd en worden samen met andere bedreigingen in de geschiedenis weergegeven.
  - **Auditmodus**: Microsoft Defender detecteert mogelijk ongewenste toepassingen, maar neemt geen verdere acties. U kunt informatie nalezen over de toepassingen waartegen Windows Defender actie zou hebben ondernomen, door te zoeken naar gebeurtenissen die door Windows Defender in Logboeken zijn gemaakt.

- **Acties voor gedetecteerde bedreigingen**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938&clcid=0x409)

  Geef de actie op die door Microsoft Defender moeten worden uitgevoerd voor gedetecteerde schadelijke software op basis van het bedreigingsniveau van de malware.
  
  Defender classificeert gedetecteerde malware volgens een van de volgende ernstniveaus:
  - **Lage ernst**
  - **Gemiddelde ernst**
  - **Hoge ernst**
  - **Zeer hoge ernst**

  Voor elk niveau geeft u de actie op die moet worden uitgevoerd. De standaardinstelling voor elk ernstniveau is *Niet geconfigureerd*.

  - **Niet geconfigureerd**
  - **Opschonen**: de service probeert bestanden te herstellen en te desinfecteren.
  - **Quarantaine**: bestanden worden verplaatst naar quarantaine.
  - **Verwijderen**: bestanden worden van het apparaat verwijderd.
  - **Toestaan**: hiermee staat u het bestand toe en worden er geen andere acties uitgevoerd.
  - **Door gebruiker gedefinieerd**: de apparaatgebruiker beslist welke actie er moet worden ondernomen.
  - **Blokkeren**: de uitvoering van bestanden wordt geblokkeerd.

## <a name="scan"></a>Scannen

- **Archiefbestanden scannen**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  Configureer Defender om archiefbestanden, zoals ZIP- of CAB-bestanden, te scannen.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardwaarde van de client, namelijk het scannen van gearchiveerde bestanden. De gebruiker kan dit echter uitschakelen.
Meer informatie
  - **Nee**: bestandsarchieven worden niet gescand. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het scannen van archiefbestanden wordt ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Lage CPU-prioriteit inschakelen voor geplande scans**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944&clcid=0x409)

  Configureer CPU-prioriteit voor geplande scans.
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard. Dat betekent dat er geen wijzigingen in de CPU-prioriteit worden aangebracht.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: tijdens geplande scans wordt lage CPU-prioriteit gebruikt. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Volledige inhaalscan uitschakelen**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042&clcid=0x409)

  Configureer inhaalscans voor geplande volledige scans. Een inhaalscan is een scan die wordt gestart omdat een regelmatig geplande scan is gemist. Normaal gesproken zijn deze geplande scans niet uitgevoerd omdat de computer op het geplande tijdstip was uitgeschakeld.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client. Dat betekent dat inhaalscans voor volledige scans zijn ingeschakeld. De gebruiker kan deze echter uitschakelen.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: inhaalscans voor geplande volledige scans worden afgedwongen en de gebruiker kan ze niet uitschakelen. Als een computer offline is gedurende twee opeenvolgende geplande scans, wordt een inhaalscan gestart wanneer iemand zich de volgende keer aanmeldt bij de computer. Als er geen geplande scan is geconfigureerd, wordt er geen inhaalscan uitgevoerd. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Snelle inhaalscan uitschakelen**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941&clcid=0x409)

  Configureer inhaalscans voor geplande snelle scans. Een inhaalscan is een scan die wordt gestart omdat een regelmatig geplande scan is gemist. Normaal gesproken zijn deze geplande scans niet uitgevoerd omdat de computer op het geplande tijdstip was uitgeschakeld.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client. Dat betekent dat snelle inhaalscans zijn ingeschakeld. De gebruiker kan deze echter uitschakelen.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: inhaalscans voor geplande snelle scans worden afgedwongen en de gebruiker kan ze niet uitschakelen. Als een computer offline is gedurende twee opeenvolgende geplande scans, wordt een inhaalscan gestart wanneer iemand zich de volgende keer aanmeldt bij de computer. Als er geen geplande scan is geconfigureerd, wordt er geen inhaalscan uitgevoerd. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Limiet voor het CPU-gebruik per scan**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  Geef de limiet op als een percentage tussen nul en 100, de gemiddelde CPU-belastingsfactor voor de Defender-scan.

- **Toegewezen netwerkschijven scannen tijdens een volledige scan**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  Configureer Defender voor het scannen van toegewezen netwerkstations.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard. Dat wil zeggen dat het scannen van toegewezen netwerkstations is uitgeschakeld.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het scannen van toegewezen netwerkstations is ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Dagelijkse snelle scan uitvoeren om**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)

  Selecteer het tijdstip waarop Defender snelle scans moet uitvoeren.
  Standaard is dit **niet geconfigureerd**

- **Type scan**  
  CSP: [ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

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
  - **Nee**
  - **Ja**

## <a name="updates"></a>Updates

- **Voer in hoe vaak (0-24 uur) er moet worden gecontroleerd op updates van de beveiligingsinformatie**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  Geef een interval van nul tot 24 (in uren) op dat wordt gebruikt om op handtekeningen te controleren. De waarde nul betekent dat er niet wordt gecontroleerd op nieuwe handtekeningen. Met de waarde 2 wordt elke twee uur gecontroleerd, enzovoort.

## <a name="user-experience"></a>Gebruikerservaring

- **Gebruikerstoegang tot de app Microsoft Defender toestaan**  
  CSP: [AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)  

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij interface en meldingen zijn toegestaan.
  - **Nee**: de gebruikersinterface (UI) van Defender is niet toegankelijk en meldingen worden onderdrukt.
  - **Ja**


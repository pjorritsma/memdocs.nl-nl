---
title: Instellingen van het Antivirus-beleid voor Windows 10 voor Microsoft Defender Antivirus voor Intune | Microsoft Docs
description: Bekijk een lijst met de instellingen in het Microsoft Defender Antivirus-profiel voor Windows 10. U kunt deze instellingen configureren als onderdeel van het antivirusbeleid voor eindpuntbeveiliging in Microsoft Intune.
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
ms.openlocfilehash: ff5c8208cb1ee9357c501a3c457bc346879b241d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88906698"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Instellingen voor het Microsoft Defender Antivirus-beleid voor Windows 10 in Microsoft Intune

Bekijk het eindpuntbeveiligingsbeleid voor antivirus dat u kunt configureren voor het profiel Microsoft Defender Antivirus voor Windows 10 in Microsoft Intune als onderdeel van een [eindpuntbeveiligingsbeleid](../protect/endpoint-security-policy.md).

## <a name="cloud-protection"></a>Cloudbeveiliging

Deze instellingen zijn beschikbaar in de volgende profielen:

- Microsoft Defender Antivirus

**Instellingen**:

- **Cloudbeveiliging inschakelen**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Standaard stuurt Defender op desktopapparaten met Windows 10 informatie naar Microsoft over eventuele gevonden problemen. Microsoft analyseert die gegevens om meer te weten te komen over problemen die u en andere klanten ondervinden, om verbeterde oplossingen te kunnen bieden.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: cloudbeveiliging is ingeschakeld.  Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Cloudbeveiligingsniveau**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configureer hoe strikt Defender Antivirus te werk gaat bij het blokkeren en scannen van verdachte bestanden.
  - **Niet geconfigureerd** (*standaard*): standaardblokkeringsniveau van Defender.
  - **Hoog**: onbekende bestanden wordt strikt geblokkeerd met optimalisatie van clientprestaties. Dit kan leiden tot meer onterechte positieven.
  - **Hoog plus**: onbekende bestanden wordt strikt geblokkeerd met toepassing van aanvullende beveiligingsmaatregelen die invloed kunnen hebben op clientprestaties.
  - **Zero tolerance**: alle onbekende uitvoerbare bestanden worden geblokkeerd.

- **Verlengde time-out van Windows Defender-cloud in seconden**  
  CSP: [CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus blokkeert automatisch verdachte bestanden gedurende tien seconden, terwijl het de bestanden in de cloud scant om er zeker van te zijn dat deze veilig zijn. U kunt maximaal 50 seconden extra toevoegen aan deze time-out.

## <a name="microsoft-defender-antivirus-exclusions"></a>Uitsluitingen voor Microsoft Defender Antivirus

Deze instellingen zijn beschikbaar in de volgende profielen:

- Microsoft Defender Antivirus
- Uitsluitingen voor Microsoft Defender Antivirus

**Instellingen**:

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

Deze instellingen zijn beschikbaar in de volgende profielen:

- Microsoft Defender Antivirus

**Instellingen**:

- **Realtime-beveiliging inschakelen**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Vereis dat Defender op Windows 10-desktopapparaten gebruikmaakt van de realtime-bewakingsfunctionaliteit.
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het gebruik van realtime-bewaking wordt afgedwongen. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Beveiliging bij toegang inschakelen**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Configureer virusbeveiliging die voortdurend actief is, in plaats van op aanvraag.

  - **Niet geconfigureerd** (*standaard*): dit beleid verandert niet de status van deze instelling op een apparaat. De bestaande status op het apparaat verandert niet.
  - **Nee**: beveiliging bij toegang blokkeren op apparaten. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: beveiliging bij toegang is actief op apparaten.

- **Controleren op inkomende en uitgaande bestanden**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Configureer deze instelling om te bepalen welk NTFS-bestand en welke programma-activiteit wordt gecontroleerd.
  - **Alle bestanden bewaken** (*standaard*)
  - **Alleen inkomende bestanden controleren**
  - **Alleen uitgaande bestanden controleren**

- **Gedragscontrole inschakelen**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Standaard maakt Defender op desktopapparaten met Windows 10 gebruik van Gedragscontrole.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het gebruik van realtime-gedragscontrole wordt afgedwongen. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Netwerkbeveiliging inschakelen**  
  CSP: [EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Bescherm apparaatgebruikers die gebruikmaken van een app tegen het openen van phishing-praktijken, sites die schadelijke software hosten en schadelijke inhoud op internet. Beveiliging omvat het voorkomen dat browsers van derden verbinding maken met gevaarlijke websites.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: netwerkbeveiliging is ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Alle gedownloade bestanden en bijlagen scannen**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Configureer Defender zo dat alle gedownloade bestanden en bijlagen worden gescand.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: Defender scant alle gedownloade bestanden en bijlagen. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Scripts scannen die in Microsoft-browsers worden gebruikt**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Configureer Defender voor het scannen van scripts.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: Defender scant scripts. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Netwerkbestanden scannen**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Configureer Defender voor het scannen van netwerkbestanden.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het scannen van netwerkbestanden is ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **E-mails scannen**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Configureer Defender voor het scannen van inkomende e-mail.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het scannen van e-mail is ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

## <a name="remediation"></a>Herstel

Deze instellingen zijn beschikbaar in de volgende profielen:

- Microsoft Defender Antivirus

**Instellingen**:

- **Aantal dagen (0-90) voor het bewaren van schadelijke software in quarantaine**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Geef een aantal dagen op van nul tot 90, gedurende welke het systeem in quarantaine geplaatste items bewaart voordat ze automatisch worden verwijderd. Met de waarde nul blijven items in quarantaine staan en worden ze niet automatisch verwijderd.

- **Toestemming voor voorbeelden verzenden**  

  - **Niet geconfigureerd** (*standaard*)
  - **Veilige voorbeelden automatisch verzenden**
  - **Altijd vragen**
  - **Nooit verzenden**
  - **Alle voorbeelden automatisch verzenden**

- **Uit te voeren actie tegen mogelijk ongewenste apps**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Geef het detectieniveau op voor mogelijk ongewenste toepassingen (PUA's). Defender waarschuwt gebruikers wanneer mogelijk ongewenste software wordt gedownload of op een apparaat wordt geïnstalleerd.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard. Dat wil zeggen dat PUA-beveiliging is uitgeschakeld.
  - **Uitschakelen**
  - **Inschakelen**: Gedetecteerde items worden geblokkeerd en worden samen met andere bedreigingen in de geschiedenis weergegeven.
  - **Auditmodus**: Microsoft Defender detecteert mogelijk ongewenste toepassingen, maar neemt geen verdere acties. U kunt informatie nalezen over de toepassingen waartegen Windows Defender actie zou hebben ondernomen, door te zoeken naar gebeurtenissen die door Windows Defender in Logboeken zijn gemaakt.

- **Acties voor gedetecteerde bedreigingen**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

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

Deze instellingen zijn beschikbaar in de volgende profielen:

- Microsoft Defender Antivirus

**Instellingen**:

- **Archiefbestanden scannen**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Configureer Defender om archiefbestanden, zoals ZIP- of CAB-bestanden, te scannen.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardwaarde van de client, namelijk het scannen van gearchiveerde bestanden. De gebruiker kan deze instelling echter uitschakelen.
Meer informatie
  - **Nee**: bestandsarchieven worden niet gescand. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: het scannen van archiefbestanden wordt ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Lage CPU-prioriteit inschakelen voor geplande scans**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Configureer CPU-prioriteit voor geplande scans.
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard. Dat betekent dat er geen wijzigingen in de CPU-prioriteit worden aangebracht.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: tijdens geplande scans wordt lage CPU-prioriteit gebruikt. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Volledige inhaalscan uitschakelen**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Configureer inhaalscans voor geplande volledige scans. Een inhaalscan is een scan die wordt gestart omdat een regelmatig geplande scan is gemist. Normaal gesproken zijn deze geplande scans niet uitgevoerd omdat de computer op het geplande tijdstip was uitgeschakeld.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client. Dat betekent dat inhaalscans voor volledige scans zijn ingeschakeld. De gebruiker kan deze echter uitschakelen.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: inhaalscans voor geplande volledige scans worden afgedwongen en de gebruiker kan ze niet uitschakelen. Als een computer offline is gedurende twee opeenvolgende geplande scans, wordt een inhaalscan gestart wanneer iemand zich de volgende keer aanmeldt bij de computer. Als er geen geplande scan is geconfigureerd, wordt er geen inhaalscan uitgevoerd. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Snelle inhaalscan uitschakelen**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Configureer inhaalscans voor geplande snelle scans. Een inhaalscan is een scan die wordt gestart omdat een regelmatig geplande scan is gemist. Normaal gesproken zijn deze geplande scans niet uitgevoerd omdat de computer op het geplande tijdstip was uitgeschakeld.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client. Dat betekent dat snelle inhaalscans zijn ingeschakeld. De gebruiker kan deze echter uitschakelen.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Ja**: inhaalscans voor geplande snelle scans worden afgedwongen en de gebruiker kan ze niet uitschakelen. Als een computer offline is gedurende twee opeenvolgende geplande scans, wordt een inhaalscan gestart wanneer iemand zich de volgende keer aanmeldt bij de computer. Als er geen geplande scan is geconfigureerd, wordt er geen inhaalscan uitgevoerd. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Limiet voor het CPU-gebruik per scan**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Geef de limiet op als een percentage tussen nul en 100, de gemiddelde CPU-belastingsfactor voor de Defender-scan.

- **Toegewezen netwerkschijven scannen tijdens een volledige scan**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Configureer Defender voor het scannen van toegewezen netwerkstations.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard. Dat wil zeggen dat het scannen van toegewezen netwerkstations is uitgeschakeld.
  - **Nee**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen de instelling niet wijzigen.
  - **Ja**: het scannen van toegewezen netwerkstations is ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Dagelijkse snelle scan uitvoeren om**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Selecteer het tijdstip waarop Defender snelle scans moet uitvoeren.
  Deze instelling is standaard **Niet geconfigureerd**

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
  - **Nee**
  - **Ja**

## <a name="updates"></a>Updates

Deze instellingen zijn beschikbaar in de volgende profielen:

- Microsoft Defender Antivirus

**Instellingen**:

- **Voer in hoe vaak (0-24 uur) er moet worden gecontroleerd op updates van de beveiligingsinformatie**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Geef een interval van nul tot 24 (in uren) op dat wordt gebruikt om op handtekeningen te controleren. De waarde nul betekent dat er niet wordt gecontroleerd op nieuwe handtekeningen. Met de waarde 2 wordt elke twee uur gecontroleerd, enzovoort.

- **De bestandsshares voor het downloaden van definitie-updates definiëren**  
  CSP: [SignatureUpdateFallbackOrder](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

  Beheer locaties, zoals een UNC-bestandsshare, als bronlocatie voor het downloaden om definitie-updates op te halen. Zodra de definitie-updates van een opgegeven bron zijn gedownload, wordt er geen contact meer gemaakt met de resterende bronnen in de lijst.

  U kunt afzonderlijke locaties **toevoegen** of een lijst met locaties als een CSV-bestand **importeren**.

- **De volgorde definiëren van de bronnen voor het downloaden van definitie-updates**  
  CSP: [SignatureUpdateFileSharesSources](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)

  Geef op in welke volgorde contact moet worden opgenomen met de bronlocaties die u hebt opgegeven om definitie-updates op te halen. Nadat de definitie-updates van een opgegeven bron zijn gedownload, wordt er geen contact meer gemaakt met de resterende bronnen in de lijst.

## <a name="user-experience"></a>Gebruikerservaring

Deze instellingen zijn beschikbaar in de volgende profielen:

- Microsoft Defender Antivirus

**Instellingen**:

- **Gebruikerstoegang tot de app Microsoft Defender toestaan**  
  CSP: [AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043)  

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij interface en meldingen zijn toegestaan.
  - **Nee**: de gebruikersinterface (UI) van Defender is niet toegankelijk en meldingen worden onderdrukt.
  - **Ja**
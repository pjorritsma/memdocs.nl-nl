---
title: UUP preview
titleSuffix: Configuration Manager
description: Instructies voor de preview-versie van UUP-integratie
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c37fab775cdb90667ff1bc9f77dbbcaa1864b6f0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696783"
---
# <a name="uup-private-preview-instructions"></a>UUP persoonlijke preview-instructies

> [!Note]  
> Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.  

## <a name="introduction"></a>Inleiding

Het Unified update platform (UUP) is het verpakkings-en publicatie platform dat door consumenten-en Bedrijfs apparaten wordt gebruikt voor het ontvangen van updates van Windows Update voor bedrijven. Het UUP private preview-programma is voor klanten die zijn overeengekomen micro soft te helpen bij het valideren van het gebruik van UUP-updates in Configuration Manager om problemen op te lossen die klanten rapporteren met onderhouds werkzaamheden van Windows. Deze updates zijn momenteel niet openbaar beschikbaar.

Voor meer informatie over UUP raadpleegt u de volgende Windows blog post: [een update op ons Unified update platform (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/).

## <a name="benefits"></a>Voordelen

Met de UUP-functie en cumulatieve updates van Windows 10 kunt u meerdere problemen oplossen die klanten rapporteren met onderhouds Vensters.

### <a name="feature-updates"></a>Onderdelenupdates

- Met een update van UUP-onderdelen behoudt het Windows Update-proces functies op aanvraag (DOM) en taal pakketten.

- Update recht op het meest recente beveiligings nalevings niveau. U hoeft geen beveiligings updates onmiddellijk te installeren na het bijwerken van de onderdelen. Micro soft publiceert elke maand een nieuwe functie-update met de meest recente cumulatieve beveiligings update. U hoeft de inhoud van de functie-update niet elke maand te downloaden of te distribueren. U downloadt alleen de beveiligings update, die UUP deelt met de cumulatieve update.

### <a name="cumulative-updates"></a>Cumulatieve updates

- Cumulatieve updates met UUP bevatten onderhouds stack-updates (SSU) met maandelijkse cumulatieve beveiligings updates. Dit gedrag lost problemen op met het organiseren van deze twee updates. Het zorgt ervoor dat de onderhouds stack-updates worden uitgevoerd om cumulatieve updates te installeren. U hoeft deze relaties niet te beheren en te organiseren.

- Cumulatieve updates met UUP bieden u de mogelijkheid om de inhoud van de dom en het taal pakket offline te distribueren. Dit gedrag stelt gebruikers in staat om ze op aanvraag toe te voegen. Gebruikers hoeven niet te downloaden van Internet en u hoeft niet te weten hoe u deze inhoud voorbereidt.

## <a name="set-up"></a>Instellen

### <a name="1-send-your-wsus-id-to-microsoft"></a>1. uw WSUS-ID naar micro soft verzenden

Als u wilt deel nemen aan de UUP-persoonlijke preview, deelt u uw WSUS-ID met uw contact persoon voor UUP-voor beeld. Micro soft keurt uw WSUS-omgeving goed in het UUP preview-programma. Zonder deze ID kunt u geen UUP-updates zien totdat de preview-versie openbaar is.

Voer het volgende Power shell-script uit om uw WSUS-ID op te halen:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

De eigenschap **MUUrl** moet zijn `https://sws.update.microsoft.com` . Als u deze wilt wijzigen, raadpleegt u de oplossing in het volgende ondersteunings artikel: [WSUS-synchronisatie mislukt met SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception).

### <a name="2-update-configuration-manager"></a>2. Configuration Manager bijwerken

Breng de volgende wijzigingen aan op uw Configuration Manager-site ter ondersteuning van deze UUP-Preview:

#### <a name="diagnostics-and-usage-data-level"></a>Niveau van diagnose-en gebruiks gegevens

Overweeg het Configuration Manager niveau voor diagnose en gegevens gebruik te verhogen tijdens deze preview. Het **volledige** niveau helpt micro soft bij het analyseren en oplossen van problemen met deze nieuwe functie. Zie niveaus voor het [verzamelen van diagnostische gebruiks gegevens voor versie 1906](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md)voor meer informatie.

#### <a name="install-the-latest-update"></a>De meest recente update installeren

1. Werk de site bij met een van de volgende updates:

    - Versie 1902 met het [Update pakket](https://support.microsoft.com/help/4500571)
    - [Versie 1906](../../core/servers/manage/checklist-for-installing-update-1906.md)

    Zie [updates binnen de console installeren](../../core/servers/manage/install-in-console-updates.md)voor meer informatie.

2. Clients bijwerken.  

    - U kunt dit proces vereenvoudigen door gebruik te maken van automatische client upgrade. Zie [upgrade-clients](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)voor meer informatie.  

    - Als u wilt voor komen dat er *altijd 6 GB* ongebruikte inhoud naar de client wordt gedownload, werkt u alle clients waarop u UUP-updates hebt gericht, bij.

### <a name="3-update-windows-clients-to-a-supported-version"></a>3. Windows-clients bijwerken naar een ondersteunde versie

Installeer de volgende updates om de installatie van UUP-updates te kunnen installeren:

1. Een specifiek mini maal cumulatief maandelijks compatibiliteits niveau.

2. Een specifieke niet-cumulatieve, niet-beveiligings update van de Microsoft Update catalogus. Als u de update wilt importeren in Configuration Manager voor implementatie, raadpleegt u [updates importeren uit de Microsoft Update catalogus](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog).

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>Ondersteunde versies van Windows 10 en vereiste updates

| Windows 10-versie | Minimale compatibiliteits niveau | Aanvullende catalogus update |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10, versie 1903** | RTM | 7 november 2019, [KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10, versie 1809** | 2019 augustus, [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 7 november 2019, [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10, versie 1803** | 2019 april, [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 7 november 2019, [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10, versie 1709** | 2019 april, [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 7 november 2019, [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - Als u de updates van 12 november 2019 toepast op de client voordat u de nieuwe catalogus update van 7 november 2019 toepast, worden de Windows Update agent wijzigingen die nodig zijn om UUP te ondersteunen, overschreven. Als u clients in dat scenario wilt herstellen, moet u na de 12 november 2019 updates de extra catalogus update Toep assen.
> - Als u een onderdeel Update op de client toepast, moet u de aanvullende catalogus update opnieuw installeren nadat de upgrade is voltooid.
> - Importeer de updates in Configuration Manager om het gemakkelijker te maken om onderdelen updates te testen. Zie [updates importeren uit de catalogus met Microsoft Update](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog)voor meer informatie. Nadat de functie-update is voltooid, wordt de extra catalogus update weer gegeven als **vereist**, waardoor automatische implementatie naar de versie van het besturings systeem op het hoogste niveau wordt toegestaan.

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4. clients toestaan om Delta-inhoud te downloaden wanneer deze beschikbaar is

Als u wilt dat UUP-updates correct worden gedownload, schakelt u de client instelling in zodat **clients Delta-inhoud kunnen downloaden wanneer deze beschikbaar zijn**. Met deze instelling kunt Configuration Manager de Windows Update Agent (WUA) de benodigde inhoud laten bepalen om te downloaden naar clients. Dit gedrag is in plaats van de standaard instelling, waarbij de Configuration Manager-client alle inhoud downloadt die is gekoppeld aan de UUP-update. Wanneer u deze instelling inschakelt, bepaalt WUA de extra inhoud die vereist is voor elke UUP-update. Bijvoorbeeld alleen de vereiste dom en taal pakketten.

Wanneer u deze instelling inschakelt, heeft dit geen invloed op het downloaden van server inhoud via internet. Dit is alleen van toepassing op client downloads. Voordat u UUP-updates op clients implementeert, moet u deze instelling Toep assen op clients die voldoen aan de ondersteunde versies voor UUP. De vereiste client updates verhelpen compatibiliteits problemen voor UUP-updates in WSUS en Configuration Manager.

Zie [client instellingen-software-updates](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) voor meer informatie over deze client instelling.

### <a name="5-review-your-software-update-infrastructure"></a>5. Controleer de software-update-infra structuur

Controleer uw regels voor automatische implementatie (ADR) en onderhouds plannen voordat u UUP-updates synchroniseert. Als u niet wilt dat deze updates automatisch worden geïmplementeerd, controleert u uw Adr's om deze te filteren. Zie [synced UUP updates](#how-to-find-synced-uup-updates)(Engelstalig) voor meer informatie. Bestaande onderhouds plannen implementeren standaard alleen niet-UUP-updates. U kunt de onderhouds plannen wijzigen om dit gedrag te wijzigen.

Controleer uw nalevings rapporten en wijzig deze indien nodig. Als u bijvoorbeeld de naleving voor alle producten meet, ziet u nu de cumulatieve updates UUP en niet-UUP. Aan apparaten wordt de naleving van beide typen updates gerapporteerd. Zorg ervoor dat uw nalevings rapporten deze wijziging aanpakken.

## <a name="enable-uup-and-start-testing"></a>UUP inschakelen en testen starten

### <a name="select-products-and-classifications-to-sync"></a>Selecteer de producten en classificaties die u wilt synchroniseren

Wanneer u klaar bent om te beginnen met het synchroniseren van UUP-updates, en micro soft uw WSUS-ID heeft goedgekeurd, schakelt u de nieuwe producten in:

1. [Synchroniseer software-updates](../get-started/synchronize-software-updates.md) om de nieuwe producten te vullen.  

2. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .

3. Selecteer de site op het hoogste niveau. Dit is een centrale beheer site (CAS) of een zelfstandige primaire site.

4. Selecteer in het lint **site onderdelen configureren**en kies software- **Update punt**.

5. Ga naar het tabblad **Products** en selecteer een of meer van de volgende producten: 

    - **Windows 10 UUP preview**
    - **Windows Server UUP preview**

6. Ga naar het tabblad **classificaties** en selecteer de volgende opties:  

    - **Beveiligings updates**: de cumulatieve UUP-updates weer geven  
    - **Upgrades**: voor een overzicht van de updates van de UUP-onderdelen  

7. Synchroniseer opnieuw om software-updates te synchroniseren om de nieuwe UUP-updates te bekijken.

### <a name="how-to-find-synced-uup-updates"></a>Gesynchroniseerde UUP-updates zoeken

Nadat u de UUP-updates in uw omgeving hebt gesynchroniseerd, kunt u deze vinden in de Configuration Manager-console om te testen. Er zijn twee manieren om de preview-updates te vinden:

- Omdat deze updates in een afzonderlijk product worden weer gegeven, gebruikt u het product om deze updates te filteren. Gebruik het product filter van het onderhouds plan om UUP of niet-UUP onderdeel updates te implementeren.  

- In de knoop punten **alle software-updates** en **alle Windows 10-updates** van **software bibliotheek**is er een nieuwe optionele kolom **Label**. Deze eigenschap is ook beschikbaar als een filter in Adr's. Zoek in dit veld naar voor UUP-updates `UUP` . Het is leeg voor niet-UUP-updates.  

### <a name="updates-available-during-preview"></a>Er zijn updates beschikbaar tijdens de preview-versie

Zie [release-informatie voor Windows 10](/windows/release-information/)voor meer informatie over alle Windows 10-updates die door micro soft worden uitgebracht.

#### <a name="cumulative-updates-to-test"></a>Cumulatieve updates die moeten worden getest

Hoewel u mogelijk meerdere UUP-beschik bare updates ziet, begint u met de update van **September 2019** (2019-09) of een latere versie. Bijvoorbeeld:

- 2019-09 cumulatieve update voor Windows 10 versie 1809 voor x64-systemen (KB4512578)
- 2019-09 cumulatieve update voor Windows 10 versie 1803 voor x64-systemen (KB4516058)
- 2019-09 cumulatieve update voor Windows 10 versie 1709 voor x64-systemen (KB4516066)

#### <a name="feature-updates-to-test"></a>Te testen functie-updates

Hoewel u mogelijk meerdere UUP-beschik bare updates ziet, begint u met de update van **September 2019** (2019-09B) of een latere versie. Bijvoorbeeld:

- Onderdeel Update voor Windows 10, versie 1809 x64 2019-09B
- Onderdeel Update voor Windows 10, versie 1803 x64 2019-09B

## <a name="scenarios-to-test"></a>Te testen scenario's

### <a name="test-feature-updates"></a>Functie-updates testen

- Direct bijwerken naar uw gekozen beveiligings nalevings niveau  

- Installeer FODs en taal pakketten vóór de update. Zorg ervoor dat de update deze onderdelen behoudt.  

### <a name="test-cumulative-updates"></a>Cumulatieve updates testen

Zorg er tijdens de preview voor dat clients compatibel blijven maken met het UUP-type update voor meerdere opeenvolgende updates. Deze test helpt u bij het herkennen van het doorlopende gedrag.

### <a name="test-content"></a>Inhoud testen

De eerste update voor elke primaire versie (1809, 1803, 1709), architectuur en taal combinatie lijkt groot te zijn. Deze grootte is beide in aantal bestanden en schijf ruimte, vergeleken met wat u eerder hebt gezien met niet-UUP-updates. Deze extra inhoud is hoofd zakelijk voor alle dom-en taal pakketten voor cumulatieve updates. Voor functie-updates is er extra grote inhoud voor die eerste update.

Voor toekomstige cumulatieve en functie-updates is de hoeveelheid nieuwe inhoud die de site downloadt en distribueert veel kleiner. UUP deelt alle dom-en taal pakket inhoud op intelligente wijze over van updates. Deze gedeelde inhoud hoeft niet opnieuw te worden gedownload of gedistribueerd. Tijdens de preview-versie van Windows 10 versies 1709 en 1803 is deze maand down load ongeveer hetzelfde als de grootte van de cumulatieve updates in niet-UUP scenario's. In Windows 10 versie 1809 en hoger is de incrementele down load van de cumulatieve update veel kleiner dan elke maand.

Wanneer u de totale inhoud bekijkt die wordt gedownload en gedistribueerd gedurende een periode van 12 maanden voor *niet-Express*, Windows 10 versie 1803 zonder UUP moet ongeveer gelijk zijn aan die van versie 1809 met UUP. De totale inhoud die is gedownload en gedistribueerd over de gehele levens duur van de release, is kleiner in versie 1809 met UUP.

### <a name="supported-content-channels"></a>Ondersteunde inhouds kanalen

Test uw typische praktijk scenario's voor de preview-versie. UUP ondersteunt alle inhouds kanalen, waaronder:

- Windows Delivery Optimization (DO)
  - Wanneer u dit doet, moet u ervoor zorgen dat deze correct is geconfigureerd. Zie [Windows 10 update delivery](optimize-windows-10-update-delivery.md)voor meer informatie.
- Peer-cache Configuration Manager
- Windows BranchCache
- Gebruik de optie **geen implementatie pakket** en clients downloaden recht van Microsoft Update. Gebruik deze optie met Delivery Optimization.
- Alternatieve inhouds providers van derden

Zie [Windows 10-bezorgings bezorging optimaliseren](optimize-windows-10-update-delivery.md)voor meer informatie over inhouds kanalen.

<!-- TODO: Addlink to WSUS Perf documentation-->
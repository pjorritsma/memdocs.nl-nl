---
title: Instellingen voor antivirus tegen aanvallen beheren met eindpuntbeveiligingsbeleid in Microsoft Intune | Microsoft Docs
description: Configureer en implementeer beleidsregels en gebruik rapporten voor apparaten die u beheert met eindpuntbeveiligingsinstellingen voor antivirusbeleid in Microsoft Endpoint Manager.
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
ms.openlocfilehash: 63400c81ee678a98a83ed17cf192335acf9c047b
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820290"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Antivirusbeleid voor eindpuntbeveiliging in Intune

Het antivirusbeleid van de Intune-eindpuntbeveiliging kan beveiligingsbeheerders helpen om zich te richten op het beheren van de afzonderlijke groep antivirusinstellingen voor beheerde apparaten. U kunt Intune integreren met Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) als Mobile Threat Defense-oplossing om een antivirusbeleid te gebruiken.

Antivirusbeleid bevat verschillende profielen. Elk profiel bevat alleen de instellingen die relevant zijn voor Microsoft Defender ATP-antivirus voor macOS, Windows 10 of voor de gebruikerservaring in de Windows-beveiligingstoepassing op Windows 10-apparaten.

U vindt dit antivirusbeleid vinden onder **Beheren** in het knooppunt Eindpuntbeveiliging van het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

Het antivirusbeleid bevat dezelfde instellingen als bij *eindpuntbescherming* of *apparaatbeperkingsprofielen* voor [apparaatconfiguratiebeleid](../configuration/device-profile-create.md) en zijn hetzelfde als de instellingen voor [apparaatcompliancebeleid](../protect/device-compliance-get-started.md). Deze beleidstypen bevatten echter aanvullende categorieën instellingen die geen betrekking hebben op antivirus. De extra instellingen kunnen de taak voor het configureren van antivirus bemoeilijken. Daarnaast zijn de instellingen die worden gevonden in het antivirusbeleid voor macOS niet beschikbaar via de andere beleidstypen. Het antivirusprofiel van macOS vervangt de noodzaak om de instellingen te configureren met behulp van `.plist` bestanden.

## <a name="prerequisites-for-antivirus-policy"></a>Vereisten voor antivirusbeleid

**Algemeen**:

- **macOS**
  - Een ondersteunde versie van macOS
  - Microsoft Defender ATP moet op een apparaat zijn geïnstalleerd om de antivirus-instellingen op dat apparaat te beheren met Intune. Zie. [Microsoft Defender ATP voor macOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (in de documentatie van Microsoft Defender ATP)

- **Windows 10 en hoger**
  - Er zijn geen aanvullende voorwaarden vereist.

**Ondersteuning voor Configuration Manager-clients** (*voorbeeld*)

*Dit scenario vindt plaats in Preview en vereist het gebruik van Configuration Manager versie 2006 of hoger van de huidige vertakking*.
<!--*This scenario is in preview and requires use of Configuration Manager Technical Preview version 2007 or later*.-->

- **Tenantkoppeling instellen voor Configuration Manager-apparaten**: ter ondersteuning van het implementeren van antivirusbeleid op apparaten die worden beheerd door Configuration Manager, configureert u *Tenantkoppeling*. Het instellen van een tenantkoppeling omvat het configureren van Configuration Manager-apparaatverzamelingen om beveiligingsbeleid voor eindpunten van Intune te ondersteunen.

  Zie [Tenantkoppeling configureren ter ondersteuning van eindpuntbeschermingsbeleid](../protect/tenant-attach-intune.md) om een tenantkoppeling in te stellen.

## <a name="antivirus-profiles"></a>Antivirus-profielen

### <a name="devices-managed-by-intune"></a>Apparaten die worden beheerd met Intune

De onderstaande profielen worden ondersteund voor apparaten die u met Intune beheert:

**macOS**:

- **Platform**: macOS

  - Profiel: **Antivirus**: [Instellingen voor antivirusbeleid beheren](../protect/antivirus-microsoft-defender-settings-macos.md) voor macOS.

    Wanneer u [Microsoft Defender ATP voor Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) gebruikt, kunt u antivirus-instellingen configureren en implementeren op uw beheerde macOS-apparaten via Intune in plaats van deze instellingen te configureren met behulp van `.plist` bestanden.

**Windows 10**:

- Platform: **Windows 10-profielen**

  - Profiel: **Microsoft Defender Antivirus**: beheer de instellingen van het [Antivirus-beleid](../protect/antivirus-microsoft-defender-settings-windows.md) voor Windows 10.

    Defender Antivirus is de volgende generatie van beveiligingsonderdelen van Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). De volgende generatie beveiliging combineert technologieën zoals machine learning en cloudinfrastructuur om apparaten in uw bedrijfsorganisatie te beschermen.

    Het *Microsoft Defender Antivirus*-profiel is een afzonderlijk exemplaar van de antivirusinstellingen die worden gevonden in het *Beperkingsprofiel voor apparaten* voor het configuratiebeleid voor apparaten.
  
    In tegenstelling tot de antivirus-instellingen in een *Restrictieprofiel voor apparaten*, kunt u deze instellingen gebruiken voor apparaten die gezamenlijk worden beheerd. Als u deze instellingen wilt gebruiken, moet u de [schuifregelaar voor cobeheerworkload](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) voor Endpoint Protection instellen op Intune.

  - Profiel: **Microsoft Defender Antivirus-uitsluitingen** - Beheer beleidsinstellingen alleen voor [antivirusuitsluitingen](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions).
  
    Met dit beleid kunt u instellingen beheren voor de volgende Microsoft Defender Antivirus Configuration Service Providers (CSP's) die antivirusuitsluitingen definiëren:

    - Defender/ExcludedPaths
    - Defender/ExcludedExtensions
    - Defender/ExcludedProcesses

    Deze CSP's voor antivirusuitsluiting worden ook beheerd door het *Microsoft Defender Antivirus*-beleid dat identieke instellingen voor uitsluitingen bevat. Instellingen van beide beleidstypen (*antivirus* en *anti virus-uitsluitingen*) zijn onderworpen aan [beleidsamenvoeging](#policy-merge-for-settings) en maken een superset van uitsluitingen voor toepasselijke apparaten en gebruikers.

  - Profiel: **Windows Security-ervaring**: beheer welke [app-instellingen van Windows Security](../protect/antivirus-security-experience-windows-settings.md) eindgebruikers kunnen bekijken in het Microsoft Defender-beveiligingscentrum en welke meldingen ze ontvangen.

    De Windows-beveiligingsapp wordt gebruikt door een aantal Windows-beveiligingsfuncties om meldingen over de status en beveiliging van de machine te geven. Meldingen over beveiligingsapps zijn onder andere firewalls, antivirusproducten, Windows Defender SmartScreen en anderen.

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Apparaten beheerd door Configuration Manager *(In preview)*

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](includes/configmgr-antivirus-profiles.md)]

## <a name="policy-merge-for-settings"></a>Beleidsamenvoeging voor instellingen

Sommige instellingen voor antivirusbeleid ondersteunen *beleidsamenvoeging*. Beleidsamenvoeging helpt conflicten te voorkomen als er meerdere beleidsregels op dezelfde apparaten van toepassing zijn en dezelfde instelling configureren. Intune evalueert de instellingen die door de beleidsamenvoeging worden ondersteund, voor elke gebruiker of elk apparaat dat wordt uitgevoerd vanuit alle toepasselijke beleidsregels. Deze instellingen worden vervolgens samengevoegd tot één hoofdverzameling beleidsregels.

U maakt bijvoorbeeld drie afzonderlijke antivirusbeleidsregels die verschillende uitsluitingen voor de bestandspaden van virussen definiëren. Uiteindelijk worden alle drie de beleidsregels aan dezelfde gebruiker toegewezen. Omdat de Microsoft Defender-bestandspaduitsluiting CSP ondersteuning biedt voor beleidsamenvoeging, evalueert en combineert Intune de bestandsuitsluitingen van alle toepasselijke beleidsregels voor de gebruiker. De uitsluitingen worden toegevoegd aan een superset en de afzonderlijke lijst met uitsluitingen wordt aan het apparaat van de gebruiker geleverd.

Als beleidsamenvoeging niet wordt ondersteund voor een instelling, kan een conflict optreden. Conflicten kunnen ertoe leiden dat de gebruiker of het apparaat geen beleid voor de instelling ontvangt. Zo biedt beleidsamenvoeging geen ondersteuning aan de CSP om te voorkomen dat overeenkomende apparaat-id's worden geïnstalleerd (*PreventInstallationOfMatchingDeviceIDs*). Configuraties voor deze CSP worden niet samengevoegd en worden afzonderlijk verwerkt.

Als configuraties afzonderlijk worden verwerkt, worden beleidsconflicten als volgt opgelost:

1. Het veiligste beleid is van toepassing.
2. Als twee beleidsregels even veilig zijn, is het laatst gewijzigde beleid van toepassing.
3. Als het laatst gewijzigde beleid het conflict niet kan oplossen, wordt er geen beleid aan het apparaat geleverd.

### <a name="settings-and-csps-that-support-policy-merge"></a>Instellingen en CSP's die ondersteuning bieden voor het samenvoegen van beleid

De volgende instellingen ondersteunen het samenvoegen van beleid:

[Microsoft Defender Antivirus-beleid](../protect/antivirus-microsoft-defender-settings-windows.md)

- **Defender-processen die moeten worden uitgesloten** - CSP: [Defender/ExcludedProcesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)
- **Bestandsextensies die moeten worden uitgesloten van scans en de realtime-beveiliging** - CSP: [Defender/ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)
- **Defender-bestanden en -mappen die moeten worden uitgesloten** - CSP: [Defender/ExcludedPaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

## <a name="antivirus-policy-reports"></a>Beleidsrapporten voor antivirus

In rapporten van het antivirusbeleid worden statusgegevens weergegeven over het antivirusbeleid van eindpuntbeveiliging en de apparaatstatus. Deze rapporten zijn te vinden in het knooppunt eindpuntbeveiliging van het Beheercentrum voor Microsoft Endpoint Manager.

Als u de rapporten wilt weergeven, gaat u in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) naar eindpuntbeveiliging en selecteert u **Antivirus**. Als u antivirus selecteert, wordt de Overzichtspagina geopend. Aanvullende rapporten en statusweergaven zijn beschikbaar als extra pagina's.

### <a name="summary"></a>Samenvatting

Op de **Overzichtspagina** kunt u [nieuwe beleidsregels maken](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) en een lijst met de eerder gemaakte beleidsregels weergeven. De lijst bevat details op hoog niveau over het profiel dat door dat beleid wordt opgenomen (beleidstype), en als het beleid is toegewezen.

![Overzichtspagina van antivirusbeleid](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Wanneer u een beleid selecteert in de lijst, wordt de *Overzichtspagina* voor dat beleidsexemplaar geopend en wordt er meer informatie weergegeven. Nadat u een tegel in deze weergave hebt geselecteerd, geeft Intune extra informatie weer voor dat profiel als dit beschikbaar is.

![Overzichtspagina van antivirusbeleid](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Beschadigde eindpunten voor Windows 10

U kunt op de pagina **Beschadigde eindpunten voor Windows 10** de informatie bekijken over de antivirusstatus van uw door MDM beheerde Windows 10-apparaten. Deze informatie wordt geretourneerd door Windows Defender Antivirus dat op het apparaat wordt uitgevoerd, zoals *status van de bedreigingsagent*.

In deze weergave worden alleen apparaten met gedetecteerde problemen weergegeven. In deze weergave worden geen details weergegeven voor apparaten die als veilig worden geïdentificeerd.

![Pagina met beschadigde eindpunten van antivirusbeleid](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Volgende stappen

[Eindpuntbeveiligingsbeleid configureren](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)

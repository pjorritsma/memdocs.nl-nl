---
title: Instellingen voor groepsbeleid
titleSuffix: Configuration Manager
description: Informatie over de instellingen voor lokaal en groeps beleid in Windows die worden gebruikt door Configuration Manager en desktop Analytics
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0224d9faecb9ff17afc2af3a57ba222023b5a3d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718894"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>Groeps beleids instellingen voor desktop Analytics

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u een overzicht van de instellingen voor lokale en groeps beleid in Windows die Configuration Manager en het gebruik van Desktop Analytics.

Wanneer Configuration Manager apparaten registreert bij Desktop Analytics, wordt het Windows-beleid ingesteld voor het configureren van het apparaat. In de meeste gevallen gebruikt u Configuration Manager voor het configureren van deze instellingen.

## <a name="windows-settings"></a>Windows-instellingen

Configuration Manager stelt Windows-beleid in een of beide van de volgende register sleutels in:

- Groeps beleidsobject (**GPO**):`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- **Lokale** beleids voorkeur:`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Beleid | Pad | Van toepassing op | Waarde |
|--------|------|------------|-------|
| **CommercialId** | Lokaal | Alle Windows-versies | Als u een apparaat wilt weer geven in Desktop Analytics, configureert u dit met de commerciële ID van uw organisatie. |
| **AllowTelemetry**  | GPO | Windows 10 | Instellen `1` voor **Basic**, `2` voor **uitgebreid**of `3` voor **volledige** diagnostische gegevens. Voor desktop Analytics zijn ten minste eenvoudige diagnostische gegevens vereist. Micro soft raadt u aan het verbeterde niveau (beperkt) te gebruiken met Desktop Analytics. Zie [Diagnostische gegevens van Windows in uw organisatie configureren](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization) voor meer informatie. |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10, versie 1803 en hoger | Deze instelling is alleen van toepassing wanneer de AllowTelemetry `2`-instelling is. Hiermee worden de uitgebreide diagnostische gegevens gebeurtenissen die naar micro soft worden verzonden, beperkt tot alleen die gebeurtenissen die nodig zijn voor desktop Analytics. Zie voor meer informatie [gebeurtenissen van Windows 10 diagnostische gegevens en velden die zijn verzameld via het beleid uitgebreide diagnostische gegevens beperken](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields). |
| **AllowDeviceNameInTelemetry** | GPO | Windows 10, versie 1803 en hoger | Apparaten kunnen de naam van het apparaat verzenden. De naam van het apparaat wordt niet standaard naar micro soft verzonden. Als u de apparaatnaam niet verzendt, wordt deze in Desktop Analytics weer gegeven als ' onbekend '. Zie [device name (apparaatnaam](enroll-devices.md#device-name)) voor meer informatie. |
| **CommercialDataOptIn** | Lokaal | Windows 8,1 en eerder | Desktop Analytics vereist een waarde van `1`. Zie voor meer informatie [commerciële gegevens opt-in Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **RequestAllAppraiserVersions** | Beide | Windows 8,1 en eerder | `1` Voor desktop Analytics moet de waarde voor het verzamelen van gegevens correct zijn. |
| **DisableEnterpriseAuthProxy** | GPO | Alle Windows-versies | Als uw omgeving een door een gebruiker geverifieerde proxy met geïntegreerde Windows-verificatie voor Internet toegang vereist, moet `0` voor desktop Analytics de waarde voor het verzamelen van gegevens correct worden gebruikt. Zie verificatie van de [proxy server](enable-data-sharing.md#proxy-server-authentication)voor meer informatie. |

> [!IMPORTANT]
> In de meeste gevallen gebruikt u Configuration Manager voor het configureren van deze instellingen. Deze instellingen zijn niet ook van toepassing op domein groeps beleidsobjecten. Zie [conflict oplossing](enroll-devices.md#conflict-resolution)voor meer informatie.

### <a name="settings-from-upgrade-readiness"></a>Instellingen van Upgradegereedheid

Windows Analytics stelt ook de volgende beleids regels in via het Upgradegereedheid script:

- CommercialId
- AllowDeviceNameInTelemetry
- CommercialDataOptIn
- RequestAllAppraiserVersions

Als u het Upgradegereedheid onboarding-script op een apparaat hebt uitgevoerd, kunnen deze beleids instellingen nog bestaan. Gebruik het verouderde script niet. Voordat u het apparaat registreert bij Desktop Analytics, verwijdert u deze vorige beleids instellingen.

## <a name="group-policy-settings"></a>Instellingen voor groepsbeleid

In het algemeen gebruikt u Configuration Manager verzamelingen om instellingen en registraties voor desktop Analytics te richten. Gebruik direct lidmaatschap of query's om apparaten op te nemen of uit te sluiten van de verzameling. Zie [verzamelingen maken](../core/clients/manage/collections/create-collections.md)voor meer informatie.

Configuration Manager configureert de instellingen voor commerciële ID en diagnostische gegevens in uw doel verzameling. Als u verschillende instellingen voor diagnostische gegevens wilt configureren voor een andere groep apparaten, gebruikt u instellingen voor groeps beleid om Configuration Manager instellingen te overschrijven. U moet bijvoorbeeld een **verbeterd (beperkt)** niveau instellen voor sommige apparaten en **basis** voor anderen. Sommige apparaten hebben mogelijk verschillende verificatie-instellingen voor de [proxy server](enable-data-sharing.md#proxy-server-authentication) .

De relevante groeps beleids instellingen bevinden zich op het volgende pad: **computer configuratie** > **Beheersjablonen** > **Windows Components** > **gegevens verzameling en Preview-versies**van Windows-onderdelen.

Groeps beleids instellingen wijzigen alleen register instellingen in de volgende sleutel:`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> Wanneer u instellingen voor groeps beleid gebruikt om complexe scenario's in te scha kelen, moet u speciale aandacht schenken aan beleids instellingen die configuratie conflicten kunnen veroorzaken. Configuration Manager configureert alleen [Windows-instellingen](#windows-settings) *als de waarde nog niet bestaat*. Groeps beleids instellingen hebben voor rang op Configuration Manager instellingen, waardoor bepaalde groeps beleids configuraties problemen kunnen veroorzaken met Desktop Analytics.

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>Groeps beleids instellingen die conflicteren met Configuration Manager instellingen voor desktop Analytics

De instellingen voor groeps beleid in de volgende tabel hebben de grootste kans om conflicten te veroorzaken met de Windows-instellingen die door Configuration Manager worden ingesteld op apparaten die worden inge schreven bij Desktop Analytics:

| Weergavenaam | Registerwaarde | Effect op apparaten die zijn Inge schreven in Desktop Analytics |
|--------------|----------------|-------------------------------------------------|
| **De commerciële ID configureren** | CommercialId | Als u dit beleid instelt op een andere waarde, wordt de commerciële ID die is ingesteld door Configuration Manager overschreven. Als dit niet dezelfde ID is, worden geconfigureerde apparaten mogelijk niet weer gegeven in Desktop Analytics. |
| **Telemetrie toestaan** | AllowTelemetry | Als u dit beleid instelt op een andere waarde, overschrijft het het globale diagnostische gegevens niveau dat u hebt ingesteld in Configuration Manager voor de doel verzameling. |
| **Uitgebreide diagnostische gegevens beperken tot de minimale vereisten van Windows Analytics** | LimitEnhancedDiagnosticDataWindowsAnalytics | Dit beleid is afhankelijk van de vorige AllowTelemetry-instelling. Afhankelijk van het niveau dat u hebt ingesteld in Configuration Manager of met groeps beleid, kan dit beleid het niveau van diagnostische gegevens op het apparaat wijzigen in **uitgebreid** of **uitgebreid (beperkt)**. Dit beleid is alleen van toepassing als AllowTelemetry is `2` ingesteld op (**uitgebreid**). |
| **Toestaan dat de apparaatnaam wordt verzonden in diagnostische gegevens van Windows** | AllowDeviceNameInTelemetry | Als u ervoor kiest om apparaatnamen te verzenden in Configuration Manager, kunt u deze vervangen door de configuratie van dit beleid in te scha kelen. Wanneer u deze instelling uitschakelt, worden apparaatnamen in Desktop Analytics weer gegeven als ' onbekend '. Zie [device name (apparaatnaam](enroll-devices.md#device-name)) voor meer informatie. |
| **Geauthenticeerd proxy gebruik configureren voor de verbonden gebruikers ervaring en telemetrie-service** | DisableEnterpriseAuthProxy | Als u Configuration Manager apparaten configureert voor het gebruik van door de gebruiker`0`geverifieerde proxy (), als u dit beleid vervolgens configureert om het`1` **gebruik van geverifieerde proxy's () uit te scha kelen** , verzendt het apparaat diagnostische gegevens in de systeem context in plaats van de context van de gebruiker. Als u het apparaat niet configureert met een proxy in de systeem context of als het apparaat niet kan worden geverifieerd bij de proxy, kan Windows geen diagnostische gegevens naar Desktop Analytics verzenden. |

> [!NOTE]
> Met het verouderde beleid worden **Connected user experiences en telemetrie** (TelemetryProxy) geconfigureerd, kan Windows diagnostische gegevens naar een specifieke proxy door sturen in plaats van de gebruiker (WinINET) of de Device (WinHTTP)-proxy. Sommige Windows-onderdelen bieden geen ondersteuning voor dit beleid. Als u dit beleid gebruikt, kan dit leiden tot problemen met de gegevens kwaliteit in Desktop Analytics.

#### <a name="behavior-of-disabled-settings"></a>Gedrag bij uitgeschakelde instellingen

Als u deze groeps beleids instellingen configureert op **uitgeschakeld**, heeft dit verschillende gevolgen voor het gedrag van het systeem.

- Wanneer u het **CommercialId** -beleid uitschakelt, wordt de register waarde door Windows verwijderd. De instelling Configuration Manager voor de commerciële ID, die wordt ingesteld in het registerpad van het lokale beleid, is van toepassing op het apparaat.

- Wanneer u de instelling in groeps beleid inschakelt, wordt de register waarde door Windows verwijderd voor beleids regels die in dezelfde register locatie als groeps beleid worden Configuration Manager. Configuration Manager wordt het opnieuw ingesteld op de volgende beleids verwerkings cyclus en vervolgens wordt dit door Windows verwijderd bij de volgende vernieuwing van groeps beleid. Deze constante wijziging in configuratie kan leiden tot ongewenste gedrag met Desktop Analytics.

  - Als u instelt dat deze groeps beleids instellingen **niet zijn geconfigureerd**, wordt de waarde eenmaal door Windows verwijderd, maar blijft deze onverwijderd. Met deze configuratie kunnen de waarden van Configuration Manager worden toegepast zoals verwacht.

### <a name="group-policy-settings-to-customize-the-user-experience"></a>Groeps beleids instellingen voor het aanpassen van de gebruikers ervaring

Deze groeps beleids instellingen zijn niet vereist voor Configuration Manager of desktop Analytics. U kunt deze configureren in groeps beleid voor het configureren van de gebruikers ervaring met diagnostische gegevens van Windows.

| Weergavenaam | Registerwaarde | Effect op apparaten die zijn Inge schreven in Desktop Analytics |
|--------------|----------------|-------------------------------------------------|
| **Wijzigings meldingen voor het inschakelen van telemetrie configureren** | DisableTelemetryOptInChangeNotification | Vanaf Windows 10, versie 1803, ontvangt u een melding van gebruikers wanneer het niveau van diagnostische gegevens wordt gewijzigd. Gebruik dit beleid om meldingen uit te scha kelen. |
| **Gebruikers interface voor het instellen van de telemetrie-instelling configureren** | DisableTelemetryOptInSettingsUx | Wanneer u het niveau van de diagnostische gegevens configureert, stelt u de bovenste grens voor het apparaat in. Met ingang van Windows 10 versie 1803 kunnen gebruikers een lager niveau instellen. Gebruik dit beleid om te voor komen dat gebruikers het diagnose niveau wijzigen. Zie [Diagnostische gegevens van Windows in uw organisatie configureren](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management) voor meer informatie. |
| **Het verwijderen van diagnostische gegevens uitschakelen** | DisableDeviceDelete | Vanaf Windows 10 versie 1809 kunnen gebruikers diagnostische gegevens verwijderen van de pagina met instellingen voor **diagnostische &-feedback** . Gebruik dit beleid om te voor komen dat diagnostische gegevens die micro soft verzamelt van het apparaat worden verwijderd. |
| **Diagnostische data viewer uitschakelen** | DisableDiagnosticDataViewer | Vanaf Windows 10 versie 1809 kunnen gebruikers de viewer voor diagnostische gegevens inschakelen en openen via de pagina met instellingen voor **diagnostische & feedback** . Gebruik dit beleid om de viewer voor diagnostische gegevens in Windows-instellingen uit te scha kelen en te voor komen dat diagnostische gegevens worden weer gegeven die micro soft verzamelt van het apparaat.|

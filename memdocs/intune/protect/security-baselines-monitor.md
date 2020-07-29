---
title: Controleer het succes of falen van beveiligingsbasislijnen in Microsoft Intune - Azure | Microsoft Docs
description: Controleer de fout-, conflict- en successtatus bij het implementeren van beveiligingsbasislijnen voor gebruikers en apparaten in Microsoft Intune MDM. Leer hoe u problemen oplost met clientlogboeken en bekijk de rapportagefuncties in Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cecd39bcba7e16cc933086c99bbc0b403381d75d
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461790"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>De beveiligingsbasislijnen en beveiligingsprofielen controleren in Microsoft Intune

Intune biedt verschillende opties om uw beveiligingsbasislijnen te bewaken. U kunt het volgende doen:

- Controleer een beveiligingsbasislijn, evenals apparaten die (al dan niet) overeenkomen met de aanbevolen waarden.
- Controleer het beveiligingsbasislijnprofiel dat op uw gebruikers en apparaten van toepassing is.
- Bekijk hoe de instellingen van een geselecteerd profiel worden ingesteld op een geselecteerd apparaat.

U kunt ook de *configuraties voor Eindpuntbeveiliging* bekijken die van toepassing zijn op afzonderlijke apparaten, waaronder beveiligingsbasislijnen.

In dit artikel worden beide controleopties besproken.

In [Security baselines in Intune](security-baselines.md) (Beveiligingsbasislijnen in Intune) vindt u meer informatie over de basislijnbeveiligingsfunctie in Microsoft Intune.

## <a name="monitor-the-baseline-and-your-devices"></a>Bewaak de basislijn en uw apparaten

Als u een basislijn controleert, krijgt u inzicht in de beveiligingsstatus van uw apparaten op basis van de aanbevelingen van Microsoft. Als u deze inzichten wilt bekijken, meldt u zich aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431), gaat u naar **Eindpuntbeveiliging** > **Beveiligingsbasislijnen** en selecteert u een type beveiligingsbasislijn, zoals de *MDM-beveiligingsbasislijn*. Selecteer vervolgens in het deelvenster *Profiel* het profielexemplaar waarvan u de details wilt weergeven. Hiermee opent u het deelvenster *Eigenschappen* van het profiel, waarin u vervolgens een van de profielrapporten kunt selecteren in de sectie *Controleren*. 

Het kan tot 24 uur na de eerste toewijzing van een basislijn duren voordat gegevens worden weergegeven. Latere wijzigingen worden na maximaal zes uur weergegeven.

Bij het inzoomen op rapporten en apparaten zijn er verschillende details beschikbaar.

<!-- UI is changing, unclear how yet: 


- **Device view** – A summary of how many devices are in each status category for the baseline.
- **Per-category** - A view that displays each category in the baseline and includes the percentage of devices for each status group for each baseline category.

Each device is represented by one of the following statuses (used in the *device* view and also the *per-category* views):

- **Matches baseline** - All the settings in the baseline match the recommended settings.
- **Does not match baseline** - One or more settings in the baseline were modified from their default values in the original baseline. The default values in each security baseline are the recommended values for that baseline.

  > [!NOTE]
  > When you create or edit a baseline profile, any change that is made to a default value or configuration setting causes a *Does not match baseline* status to occur. For help to determine the settings that were changed, contact Microsoft Support. 

- **Misconfigured** - At least one setting isn't correctly configured. This status means that the setting is in a conflict, error, or pending state.
- **Not applicable** - At least one setting isn't applicable and isn't applied.

### Device view

The Overview pane displays a chart-based summary of how many devices have a specific status for the baseline; **Security baseline posture for assigned Windows 10 devices**.

![Check the status of the devices](./media/security-baselines-monitor/overview.png)

When a device has different status from different categories in the baseline, the device is represented by a single status. The status that represents the device is taken from the following order of precedence: **Misconfigured**, **Does not match baseline**, **Not applicable**, **Matches baseline**.

For example, if a device has a setting that's classified as *misconfigured* and one or more settings that are classified as *Does not match baseline*, the device is classified as *Misconfigured*.

You can click on the chart to drill through and view a list of devices with various statuses. You can then select individual devices from that list to view details about individual devices. For example:

- Select **Device configuration** > Select the profile with an Error state:

  ![View the status of a profile](./media/security-baselines-monitor/device-configuration-profile-list.png)

- Select the Error profile. A list of all settings in the profile, and their state is shown. Now, you can scroll to find the setting causing the error:

  ![See the setting causing the error](./media/security-baselines-monitor/profile-with-error-status.png)

Use this reporting to see any settings in a profile that are causing an issue. Also get more details of policies and profiles deployed to devices.

> [!NOTE]
> When a property is set to **Not configured** in the baseline, the setting is ignored, and no restrictions are enforced. The property isn't shown in any reporting.

### Per category view

The Overview pane displays a per-category chart for the baseline named **Security baseline posture by category**.  This view displays each category from the baseline, and identifies the percentage of devices that fall into a status classification for each of those categories.

![Per-Category view of status](./media/security-baselines-monitor/monitor-baseline-per-category.png)

Status for **Matches baseline** doesn't display until 100% of devices report that status for the category.

You can sort the by-category view by each column, by selecting up-down arrow icon at the top of the column.
-->

## <a name="monitor-the-profile"></a>Bewaak het profiel

Het bewaken van het profiel geeft inzicht in de implementatiestatus van uw apparaten, maar niet in de beveiligingsstatus op basis van de aanbevelingen uit de basislijn.

1. Selecteer in Intune **Beveiligingsbasislijnen** > selecteer een basislijn om het bijbehorende deelvenster *Profielen* te openen.

<!-- More churn  
2. Select a profile. In **Overview**, the image shows how many devices and users have this profile assigned:

   ![See how many devices and users are assigned the security baselines profile](./media/security-baselines-monitor/existing-profile-overview.png)
--> 
3. Onder **Eigenschappen** > **beheren** staat een overzicht van alle instellingen in de basislijn. U kunt deze instellingen eveneens wijzigen:

   ![Bekijk en update instellingen in het beveiligingsbasislijnprofiel](./media/security-baselines-monitor/manage-settings.png)

4. In **Bewaken** ziet u de implementatiestatus van het profiel op afzonderlijke apparaten, de status voor elke gebruiker en de status voor elke instelling in de basislijn:

   ![Bekijk de verschillende controleopties voor een beveiligingsbasislijnprofiel](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>Instellingen weergeven van profielen die van toepassing zijn op een apparaat

U kunt een profiel voor een beveiligingsbasislijn selecteren en inzoomen om een lijst met instellingen van dat profiel te bekijken, aangezien deze van toepassing zijn op een afzonderlijk apparaat.  Als u deze lijst wilt bekijken, zoomt u in op **Eindpuntbeveiliging** > **Beveiligingsbasislijnen** >  *, selecteert u het type beveiligingsbasislijn*  >  *en het profiel dat u wilt bekijken* > **Apparaatstatus**. U kunt de lijst ook weergeven door naar **Eindpuntbeveiliging** > **Alle apparaten** > *Een apparaat selecteren* > **Configuratie eindpuntbeveiliging** > *Een basislijnversie selecteren* te gaan.

Nadat u een apparaat hebt geselecteerd, wordt in het Microsoft Endpoint Manager-beheercentrum een lijst weergegeven met de instellingen van dat profiel, met inbegrip van de categorie waarvan de instelling afkomstig is en de configuratiestatus op het apparaat. Configuratiestatussen zijn onder andere de volgende waarden:

- **Geslaagd**: de instelling op het apparaat komt overeen met de waarde die is geconfigureerd in het profiel. Dit is de aanbevolen standaardwaarde voor basislijnen of een aangepaste waarde die door een beheerder is opgegeven toen het profiel werd geconfigureerd.
- **Conflict**: de instelling is in conflict met een ander beleid, bevat een fout of is in afwachting van een update.
- **Niet van toepassing**: de instelling wordt niet toegepast door het profiel.

> [!NOTE]
> De statuswaarden voor instellingen worden in een toekomstige versie bijgewerkt en bieden meer gedetailleerde informatie.

## <a name="view-endpoint-security-configurations-per-device"></a>Configuratie van eindpuntbeveiliging per apparaat weergeven

Bekijk details over de beveiligingsconfiguraties die van toepassing zijn op afzonderlijke apparaten voor hulp bij het isoleren van instellingen die niet goed zijn geconfigureerd.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Ga naar **Apparaten** > **Alle apparaten** en selecteer het apparaat dat u wilt weergeven.

3. Selecteer in de categorie *Bewaking* de optie **Beveiligingsconfiguratie van eindpunt** om de lijst weer te geven met beveiligingsconfiguraties die op dat apparaat van toepassing zijn.

4. U kunt de beveiligingsconfiguratie van een eindpunt gebruiken om dieper in te gaan op extra details over de evaluatie van die beveiligingsconfiguratie op het apparaat.

## <a name="troubleshoot-using-per-setting-status"></a>Los problemen op met de status per instelling

U hebt een beveiligingsbasislijn geïmplementeerd, maar de implementatiestatus bevat een fout. De volgende stappen leggen uit hoe u de fout oplost.

1. Selecteer in Intune **Beveiligingsbasislijnen** > selecteer een basislijn > **Profielen**.

2. Selecteer een profiel > onder **Bewaken** > **Status per instelling**.

3. De tabel toont alle instellingen en hun status. Selecteer de kolom **Fout** of **Conflict** om te zien welke instelling de fout veroorzaakt.

### <a name="mdm-diagnostic-information"></a>Diagnostische gegevens over MDM

Nu weet u welke instelling de boosdoener is. De volgende stap is om erachter te komen waarom deze instelling een fout of een conflict veroorzaakt.

Op Windows 10-apparaten is er een ingebouwd rapport met diagnostische gegevens over MDM. Dit rapport bevat standaardwaarden en huidige waarden, benoemt de beleidsregels, geeft aan of het op het apparaat of de gebruiker is geïmplementeerd en meer. Gebruik dit rapport om te bepalen waarom de instelling een conflict of fout veroorzaakt.

1. Ga op het apparaat naar **Instellingen** > **Accounts** > **Toegang tot werk of school**.

2. Selecteer het account > **Info** > **Geavanceerd diagnostisch rapport** > **Rapport maken**.

3. Kies **Exporteren** en open het gegenereerde bestand.

4. Zoek in de verschillende onderdelen van het rapport naar de instelling met de fout of het conflict.

  Zoek bijvoorbeeld in het gedeelte **Ingeschreven configuratiebronnen en doelbronnen** of **Onbeheerd beleid**. Mogelijk komt u erachter waarom deze instelling een fout of conflict veroorzaakt.

[Diagnose MDM failures in Windows 10](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) (MDM-Fouten diagnosticeren in Windows 10) bevat meer informatie over dit ingebouwde rapport.

> [!TIP]
>
> - Sommige instellingen vermelden tevens de GUID. U kunt deze GUID in het lokale register (regedit) zoeken voor eventuele ingestelde waarden.
> - De Event Viewer-logboeken kunnen ook bepaalde foutinformatie over de problematische instelling bevatten (**Event viewer** > **Logboeken van toepassingen en services** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider** > **Beheerder**).

## <a name="next-steps"></a>Volgende stappen

- [Meer informatie over beveiligingsbasislijnen](security-baselines.md)
- [Conflicten voorkomen](security-baselines.md#avoid-conflicts)
- [Apparaatprofielen bewaken](../configuration/device-profile-monitor.md) 
- [Veelvoorkomende problemen en oplossingen](../configuration/device-profile-troubleshoot.md).
- [Beleidsregels en profielen voor het oplossen van problemen in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
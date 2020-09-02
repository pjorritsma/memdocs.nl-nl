---
title: Instellingen voor eindpuntdetectie en -respons beheren in eindpuntbeveiligingsbeleid in Microsoft Intune | Microsoft Docs
description: Configureer en implementeer beleidsregels voor apparaten die u beheert met eindpuntdetectie- en eindpuntresponsbeleid voor eindpuntbeveiliging in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: ff880b564562b3e6d67dc852f97ef7a9f5d6b814
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915038"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Eindpuntdetectie- en eindpuntresponsbeleid voor eindpuntbeveiliging in Intune

Wanneer u Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) integreert met Intune, kunt u eindpuntbeveiligingsbeleid gebruiken voor eindpuntdetectie en -respons (EDR) voor het beheren van de EDR-instellingen en de onboarding van apparaten naar Microsoft Defender ATP.

De functionaliteit van de Microsoft Defender ATP-eindpuntdetectie en -respons biedt geavanceerde aanvalsdetecties die bijna in realtime en praktisch kunnen worden uitgevoerd. Beveiligingsanalisten kunnen waarschuwingen effectief prioriteren, inzicht krijgen in de volledige reikwijdte van een inbreuk en responsacties ondernemen om bedreigingen te verhelpen.

EDR-beleid bevat platformspecifieke profielen voor het beheren van instellingen voor EDR. De profielen bevatten automatisch een *onboardingpakket* voor Microsoft Defender ATP. Onboardingpakketten geven aan hoe apparaten moeten worden geconfigureerd voor gebruik met Microsoft Defender ATP. Nadat voor een apparaat onboarding is uitgevoerd, kunt u gebruik gaan maken van bedreigingsgegevens van dat apparaat.

Er wordt EDR-beleid geïmplementeerd op groepen apparaten in Azure Active Directory (Azure AD) die u beheert met Intune en op verzamelingen on-premises apparaten die u beheert met Configuration Manager, waaronder Windows-servers. Voor het EDR-beleid zijn voor de verschillende beheerpaden verschillende onboardingpakketten vereist. Daarom maakt u afzonderlijke EDR-beleidsregels voor de verschillende typen apparaten die u beheert.

U kunt het eindpuntbeveiligingsbeleid voor EDR vinden onder *Beheren* in het knooppunt **Eindpuntbeveiliging** van het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

Bekijk [Profielinstellingen voor eindpuntdetectie en -respons](endpoint-security-edr-profile-settings.md).

## <a name="prerequisites-for-edr-policies"></a>Vereisten voor EDR-beleid

**Algemeen**:

- **Tenant voor Microsoft Defender Advanced Threat Protection**: uw Microsoft Defender ATP-tenant moet worden geïntegreerd met uw Microsoft Endpoint Manager-tenant (Intune-abonnement) voordat u een EDR-beleid kunt maken. Zie [Microsoft Defender ATP gebruiken](advanced-threat-protection.md) in de Intune-documentatie.

**Ondersteuning voor Configuration Manager-clients**:

- **Tenantkoppeling instellen voor Configuration Manager-apparaten**: ter ondersteuning van het implementeren van EDR-beleid op apparaten die worden beheerd door Configuration Manager, configureert u *tenantkoppeling*. Dit omvat het configureren van Configuration Manager-apparaatverzamelingen om beveiligingsbeleid voor eindpunten van Intune te ondersteunen.

  Als u tenantkoppeling wilt instellen, inclusief de synchronisatie van Configuration Manager-verzamelingen met het beheercentrum van Microsoft Endpoint Manager en het mogelijk wilt maken dat zij met eindpuntbeveiligingsbeleid werken, raadpleegt u [Tenantkoppeling toevoegen ter ondersteuning van eindpuntbeschermingsbeleid](../protect/tenant-attach-intune.md).

## <a name="edr-profiles"></a>EDR-profielen

[Bekijk de instellingen](endpoint-security-edr-profile-settings.md) die u voor de volgende platforms en profielen kunt configureren.

**Intune**: het onderstaande wordt ondersteund voor apparaten die u met Intune beheert:

- Platform: **Windows 10 en hoger**: Intune implementeert het beleid op apparaten in uw Azure AD-groepen.
- Profiel: **Eindpuntdetectie en -respons (MDM)**

**Configuration Manager**: De volgende instellingen worden ondersteund voor apparaten die u beheert met Configuratiebeheer:

- Platform: **Windows 10- en Windows Server (ConfigMgr)** : Configuration Manager implementeert het beleid op apparaten in uw Configuration Manager-verzamelingen.
- Profiel: **Eindpuntdetectie en -respons (ConfigMgr)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Configuration Manager instellen om het EDR-beleid te ondersteunen

Voordat u EDR-beleid kunt implementeren voor Configuration Manager-apparaten, moet u de configuraties uitvoeren die in de volgende secties worden beschreven.

Deze configuraties worden gemaakt in de Configuration Manager-console en op uw Configuration Manager-implementatie. Als u niet bekend bent met Configuration Manager, kunt u in samenwerking met een Configuration Manager-beheerder stappen ondernemen om deze taken uit te voeren.  

In de volgende secties worden de vereiste taken behandeld:

1. [De update voor Configuration Manager installeren](#task-1-install-the-update-for-configuration-manager)
2. [Tenantkoppeling inschakelen](#task-2-configure-tenant-attach-and-synchronize-collections)  

> [!TIP]
> Voor meer informatie over het gebruik van Microsoft Defender ATP met Configuration Manager raadpleegt u de volgende artikelen in de Configuration Manager-inhoud:
>
> - [Configuration Manager-clients onboarden naar Microsoft Defender ATP via het Microsoft Endpoint Manager-beheercentrum](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft Endpoint Manager-tenant koppelen: Synchronisatie van apparaten en apparaatacties](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Taak 1: De update voor Configuration Manager installeren

Voor Configuration Manager versie 2002 is een update vereist die ondersteuning biedt voor het gebruik van het eindpuntdetectie- en eindpuntresponsbeleid dat u implementeert vanuit het Microsoft Endpoint Manager-beheercentrum.

**Updatedetails**:

- **Hotfix (KB4563473) Configuration Manager 2002**

Deze update is te vinden als *console-update* voor Configuration Manager 2002.

Als u deze update wilt installeren, volgt u de richtlijnen in [Console-updates installeren](../../configmgr/core/servers/manage/install-in-console-updates.md) in de Configuration Manager-documentatie.

Nadat u de update hebt geïnstalleerd, keert u terug om uw omgeving verder te configureren ter ondersteuning van het EDR-beleid van het Microsoft Endpoint Manager-beheercentrum.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Taak 2: Tenantkoppeling configureren en verzamelingen synchroniseren

Met tenantkoppeling kunt u verzamelingen apparaten van uw Configuration Manager-implementatie synchroniseren met het Microsoft Endpoint Manager-beheercentrum. Na de synchronisatie van verzamelingen kunt u in het beheercentrum informatie over die apparaten bekijken en EDR-beleid van Intune erop implementeren.  

Voor meer informatie over het tenantkoppelingsscenario raadpleegt u [Tenantkoppeling inschakelen](../../configmgr/tenant-attach/device-sync-actions.md) in de Configuration Manager-inhoud.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Tenantkoppeling inschakelen als co-beheer niet is ingeschakeld

> [!TIP]
> U gebruikt de wizard **Configuratie van co-beheer** in de Configuration Manager-console om tenantkoppeling in te schakelen, maar u hoeft geen co-beheer in te schakelen.

Als u van plan bent om co-beheer in te schakelen, moet u bekend zijn met co-beheer, de bijbehorende vereisten en hoe u workloads beheert voordat u doorgaat. Zie [Wat is co-beheer?](../../configmgr/comanage/overview.md) in de Configuration Manager documentatie.

1. Ga in de Configuration Manager-beheerconsole naar **Beheer** > **Overzicht** > **Cloudservices** > **Co-beheer**.
2. Klik in het lint op **Co-beheer configureren** om de wizard te openen.
3. Selecteer op de pagina **Tenant-onboarding** de optie **AzurePublicCloud** voor uw omgeving. Azure Government-cloud wordt niet ondersteund.
   1. Klik op **Aanmelden**. Gebruik uw *globale beheerder*-account om u aan te melden.

Het onderstaande wordt ondersteund voor apparaten die u met Intune beheert:

- Platform: **Windows 10 en hoger**: Intune implementeert het beleid op apparaten in uw Azure AD-groepen.
  - Profiel: **Eindpuntdetectie en -respons (MDM)**

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Apparaten beheerd door Configuration Manager *(In preview)*

Het volgende wordt ondersteund voor apparaten die u beheert met Configuration Manager via het scenario voor *tenantkoppeling*:

- Platform: **Windows 10- en Windows Server (ConfigMgr)** : Configuration Manager implementeert het beleid op apparaten in uw Configuration Manager-verzamelingen.
  - Profiel: **Eindpuntdetectie en -respons (ConfigMgr) (preview-versie)**

## <a name="create-and-deploy-edr-policies"></a>EDR-beleid maken en implementeren

Wanneer u uw Microsoft Defender ATP-abonnement integreert met Intune, kunt u een EDR-beleid maken en implementeren. Er zijn twee verschillende typen EDR-beleid die u kunt maken. Eén beleidstype voor apparaten die u met Intune beheert via MDM. Het tweede type is voor apparaten die u beheert met Configuration Manager.

U kiest het type beleid dat u wilt maken tijdens het configureren van een nieuw EDR-beleid door een platform voor het beleid te kiezen.

Voordat u beleid kunt implementeren op apparaten die worden beheerd door Configuration Manager, stelt u Configuration Manager in ter ondersteuning van het EDR-beleid vanuit het Microsoft Endpoint Manager-beheercentrum. Zie [Tenantkoppeling configureren ter ondersteuning van eindpuntbeschermingsbeleid](../protect/tenant-attach-intune.md).


### <a name="create-edr-policies"></a>EDR-beleid maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Eindpuntbeveiliging** > **Eindpuntdetectie en -respons** > **Beleid maken**.

3. Selecteer het platform en het profiel voor uw beleid. De volgende informatie bepaalt uw opties:

   - Intune: Intune implementeert het beleid op apparaten in uw Azure AD-groepen. Wanneer u het beleid maakt, selecteert u:
     - Platform: **Windows 10 en hoger**
     - Profiel: **Eindpuntdetectie en -respons (MDM)**

   - Configuration Manager: Configuration Manager implementeert het beleid op apparaten in uw Configuration Manager-verzamelingen. Wanneer u het beleid maakt, selecteert u:
     - Platform: **Windows 10 en Windows Server (ConfigMgr)**
     - Profiel: **Eindpuntdetectie en -respons (ConfigMgr)**

4. Selecteer **Maken**.

5. Voer op de pagina **Basisinformatie** een naam en een beschrijving in voor het profiel en selecteer dan **Volgende**.

6. Configureer op de pagina **Configuratie-instellingen** de instellingen die u met dit profiel wilt beheren. Het onboardingpakket wordt automatisch opgenomen en kan niet worden geconfigureerd.

   Wanneer u klaar bent met het configureren van instellingen, selecteert u **Volgende**.

7. *Deze stap is alleen van toepassing op het profiel **Eindpuntdetectie en -respons (MDM)***:  

   Selecteer op de pagina **Bereiktags** de optie **Bereiktags selecteren** om het deelvenster *Tags selecteren* te openen en bereiktags aan het profiel toe te wijzen.
  
   Selecteer **Volgende** om door te gaan.

8. Selecteer op de pagina **Toewijzingen** de groepen of verzamelingen die dit beleid zullen ontvangen. De keuze is afhankelijk van het platform en het profiel dat u hebt geselecteerd:

   - Voor Intune selecteert u groepen uit Azure AD.
   - Voor Configuration Manager selecteert u verzamelingen in Configuration Manager die u hebt gesynchroniseerd met Microsoft Endpoint Manager-beheercentrum en zijn ingeschakeld voor Microsoft Defender ATP-beleid.

   U kunt ervoor kiezen om op dit moment geen groepen of verzamelingen toe te wijzen en het beleid later te bewerken voor het toevoegen van een toewijzing.

   Wanneer u klaar bent om verder te gaan, selecteert u **Volgende**.

9. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent.

   Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

## <a name="edr-policy-reports"></a>EDR-beleidsrapporten

U kunt uitgebreide informatie bekijken over de EDR-beleidsregels die u in het beheercentrum voor Microsoft Endpoint Manager implementeert. Als u de informatie wilt weergeven, gaat u naar **Eindpuntbeveiliging** > **Eindpuntimplementatie en -respons** en selecteert u een beleid waarvan u de nalevingsgegevens wilt bekijken:

- Voor beleidsregels die zijn gericht op het platform **Windows 10 en hoger** (Intune), ziet u een overzicht van de naleving van het beleid. U kunt ook de grafiek selecteren om een lijst weer te geven met apparaten waarvoor het beleid is ontvangen en inzoomen op afzonderlijke apparaten voor meer informatie.

  De grafiek voor **apparaten met ATP-sensor** geeft alleen apparaten weer die naar Microsoft Defender ATP onboarden door het profiel voor **Windows 10 en hoger** te gebruiken. Om ervoor te zorgen dat al uw apparaten in deze grafiek worden weergeven, implementeert u het onboarding-profiel op al uw apparaten. Apparaten die op externe wijze, bijv. via groepsbeleid of PowerShell, op Microsoft Defender ATP worden uitgevoerd, behoren tot de **apparaten zonder ATP-sensor**.

- Voor beleid dat is gericht op het **Windows 10- en Windows Server (ConfigMgr)** -platform (Configuration Manager), ziet u een overzicht van de naleving van het beleid, maar u kunt niet inzoomen om aanvullende informatie te bekijken. De weergave is beperkt omdat het beheercentrum gegevens met een beperkte status ontvangt van Configuration Manager, waarmee de implementatie van het beleid op Configuration Manager apparaten wordt beheerd.

[Bekijk de instellingen](endpoint-security-edr-profile-settings.md) die u voor de platformen en profielen kunt configureren.

## <a name="next-steps"></a>Volgende stappen

- [Eindpuntbeveiligingsbeleid configureren](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Meer informatie over [eindpuntdetectie en -respons](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) vindt u in de Microsoft Defender ATP-documentatie.
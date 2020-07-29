---
title: Instellingen voor eindpuntdetectie en -respons beheren in eindpuntbeveiligingsbeleid in Microsoft Intune | Microsoft Docs
description: Configureer en implementeer beleidsregels voor apparaten die u beheert met eindpuntdetectie- en eindpuntresponsbeleid voor eindpuntbeveiliging in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: b1711dad8163409d05c5299e8d3b54ad619b48ec
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462062"
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

**Apparaten vanuit Configuration Manager ondersteunen**:

Voor ondersteuning bij het gebruik van een EDR-beleid bij Configuration Manager-apparaten zijn voor uw Configuration Manager-omgeving de volgende aanvullende configuraties vereist. In dit artikel vindt u [richtlijnen voor de configuratie](#set-up-configuration-manager-to-support-edr-policy):

- **Configuration Manager met versie 2002 of hoger**: op uw site moet u Configuration Manager 2002 of hoger gebruiken.

- **De Configuration Manager-update installeren**: installeer de volgende update vanuit de Configuration Manager-console om ondersteuning in Configuration Manager 2002 mogelijk te maken voor het gebruik van het EDR-beleid dat u in het Microsoft Endpoint Manager-beheercentrum maakt:
  - **Hotfix (KB4563473) Configuration Manager 2002**

- **Tenantkoppeling configureren**: met tenantkoppeling kunt u verzamelingen apparaten van Configuration Manager synchroniseren met het Microsoft Configuration Manager-beheercentrum. Vervolgens kunt u het beheercentrum gebruiken voor het implementeren van EDR-beleid voor deze verzamelingen.

  Tenantkoppeling wordt vaak geconfigureerd met co-beheer, maar u kunt ook een zelfstandige tenantkoppeling configureren.

- **Configuration Manager-verzamelingen synchroniseren**: wanneer u een tenantkoppeling configureert, kunt u de Configuration Manager-apparaatverzamelingen selecteren om te synchroniseren met Microsoft Endpoint Manager-beheercentrum. U kunt ook later terugkeren om de apparaatverzamelingen te wijzigen die u synchroniseert. Het EDR-beleid voor Configuration Manager-apparaten kan alleen worden toegewezen aan verzamelingen die u hebt gesynchroniseerd.

  Nadat u de verzamelingen hebt geselecteerd die u wilt synchroniseren, moet u deze inschakelen voor gebruik met Microsoft Defender ATP.

- **Machtigingen voor Azure AD**: als u de installatie van de tenantkoppeling wilt uitvoeren en de Configuration Manager-verzamelingen wilt configureren die u wilt synchroniseren met Microsoft Endpoint Manager-beheercentrum, hebt u een account met globale beheerdersmachtigingen voor uw Azure-abonnement nodig.

## <a name="edr-profiles"></a>EDR-profielen

[Bekijk de instellingen](endpoint-security-edr-profile-settings.md) die u voor de volgende platforms en profielen kunt configureren.

**Intune**: het onderstaande wordt ondersteund voor apparaten die u met Intune beheert:

- Platform: **Windows 10 en hoger**: Intune implementeert het beleid op apparaten in uw Azure AD-groepen.
- Profiel: **Eindpuntdetectie en -respons (MDM)**

**Configuration Manager**: De volgende instellingen worden ondersteund voor apparaten die u beheert met Configuratiebeheer:

- Platform: **Windows 10- en Windows Server**: Configuration Manager implementeert het beleid op apparaten in uw Configuration Manager-verzamelingen.
- Profiel: **Eindpuntdetectie en -respons (ConfigMgr)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Configuration Manager instellen om het EDR-beleid te ondersteunen

Voordat u EDR-beleid kunt implementeren voor Configuration Manager-apparaten, moet u de configuraties uitvoeren die in de volgende secties worden beschreven.

Deze configuraties worden gemaakt in de Configuration Manager-console en op uw Configuration Manager-implementatie. Als u niet bekend bent met Configuration Manager, kunt u in samenwerking met een Configuration Manager-beheerder stappen ondernemen om deze taken uit te voeren.  

In de volgende secties worden de vereiste taken behandeld:

1. [De update voor Configuration Manager installeren](#task-1-install-the-update-for-configuration-manager)
2. [Tenantkoppeling inschakelen](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Verzamelingen selecteren die u wilt synchroniseren](#task-3-select-collections-to-synchronize)
4. [Verzamelingen inschakelen voor Microsoft Defender ATP](#task-4-enable-collections-for-microsoft-defender-atp)

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

Als co-beheer eerder was ingeschakeld, is de tenantkoppeling al ingesteld en kunt u dit overslaan en naar [taak 3](#task-3-select-collections-to-synchronize) gaan.

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

   2. Zorg ervoor dat de optie **Uploaden naar het Microsoft Endpoint Manager-beheercentrum** is ingeschakeld op de pagina **Tenant-onboarding**.

   3. Verwijder het vinkje van **Automatische clientinschrijving voor co-beheer inschakelen**.

      Wanneer deze optie is geselecteerd, biedt de wizard extra pagina's om de installatie van co-beheer uit te voeren. Zie [Co-beheer inschakelen](../../configmgr/comanage/how-to-enable.md) in de Configuration Manager-inhoud voor meer informatie.

     ![Tenantkoppeling configureren](media/endpoint-security-edr-policy/tenant-onboarding.png)

4. Klik op **Volgende** en daarna op **Ja** om de melding **Een AAD-toepassing maken** te accepteren. Met deze actie wordt een service-principal ingericht en wordt een Azure AD-toepassingsregistratie gemaakt om de synchronisatie van verzamelingen met het Microsoft Endpoint Manager-beheercentrum te vergemakkelijken.

5. Configureer op de pagina **Upload configureren** de verzamelingen die u wilt synchroniseren. U kunt uw configuratie beperken tot een of enkele verzamelingen of door de aanbevolen instelling voor het uploaden van apparaten te gebruiken voor **alle apparaten die worden beheerd door Microsoft Endpoint Configuration Manager**.

6. Klik op **Samenvatting** om uw selectie te controleren en klik vervolgens op **Volgende**.

7. Klik op **Sluiten** als de wizard is voltooid.

   De tenantkoppeling is nu geconfigureerd en de geselecteerde verzamelingen worden gesynchroniseerd met het Microsoft Endpoint Manager-beheercentrum.

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>Tenantkoppeling inschakelen wanneer u co-beheer gebruikt

1. Ga in de Configuration Manager-beheerconsole naar **Beheer** > **Overzicht** > **Cloudservices** > **Co-beheer**.

2. Klik met de rechtermuisknop op uw instellingen voor co-beheer en selecteer **Eigenschappen**.

3. Selecteer **Uploaden naar Microsoft Endpoint Manager-beheercentrum** in het tabblad **Upload configureren**. Klik op **Toepassen**.
   - De standaardinstelling voor het uploaden van apparaten is **Alle apparaten die worden beheerd door Microsoft Endpoint Configuration Manager**. U kunt er ook voor kiezen om uw configuratie te beperken tot een of enkele verzamelingen apparaten.

     ![Het tabblad Eigenschappen voor co-beheer bekijken](media/endpoint-security-edr-policy/configure-upload.png)

4. Meld u aan met uw *globale beheerder*-account wanneer u hierom wordt gevraagd.

5. Klik op **Ja** om de melding **AAD-toepassing maken** te accepteren. Met deze actie wordt een service-principal ingericht en wordt een Azure AD-toepassingsregistratie gemaakt om de synchronisatie te vergemakkelijken.

6. Klik op **OK** om de eigenschappen voor co-beheer af te sluiten nadat u de wijzigingen hebt aangebracht.

   De tenantkoppeling is nu geconfigureerd en de geselecteerde verzamelingen worden gesynchroniseerd met het Microsoft Endpoint Manager-beheercentrum.

### <a name="task-3-select-collections-to-synchronize"></a>Taak 3: Verzamelingen selecteren die u wilt synchroniseren

Wanneer de tenantkoppeling is geconfigureerd, kunt u verzamelingen selecteren die u wilt synchroniseren. Als u nog geen verzamelingen hebt gesynchroniseerd of de verzamelingen die u wel wilt synchroniseren opnieuw wilt configureren, kunt u hiervoor de eigenschappen van co-beheer in de Configuration Manager-console bewerken.

#### <a name="select-collections"></a>Verzamelingen selecteren

1. Ga in de Configuration Manager-beheerconsole naar **Beheer** > **Overzicht** > **Cloudservices** > **Co-beheer**.

2. Klik met de rechtermuisknop op uw instellingen voor co-beheer en selecteer **Eigenschappen**.

3. Selecteer **Uploaden naar Microsoft Endpoint Manager-beheercentrum** in het tabblad **Upload configureren**. Klik op **Toepassen**.

   De standaardinstelling voor het uploaden van apparaten is **Alle apparaten die worden beheerd door Microsoft Endpoint Configuration Manager**. U kunt er ook voor kiezen om uw configuratie te beperken tot een of enkele verzamelingen apparaten.

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>Taak 4: Verzamelingen inschakelen voor Microsoft Defender ATP

Nadat u verzamelingen hebt geconfigureerd die u wilt synchroniseren met Microsoft Endpoint Manager-beheercentrum, moet u deze verzamelingen alsnog inschakelen om deze geschikt te maken voor onboarding en Microsoft Defender ATP-beleid.  Hiervoor bewerkt u de eigenschappen van elke verzameling in de Configuration Manager-console.

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>Verzamelingen inschakelen voor gebruik met Advanced Threat Protection

1. Klik met de rechtermuisknop vanuit een Configuration Manager-console die is verbonden met uw site op het hoogste niveau op een apparaatverzameling die u met Microsoft Endpoint Manager-beheercentrum synchroniseert, en selecteer **Eigenschappen**.

2. Schakel op het tabblad **Cloudsynchronisatie** de optie in om **deze verzameling beschikbaar te maken voor het toewijzen van Microsoft Defender ATP-beleid in Intune**.

   - U kunt deze optie niet selecteren als de Configuration Manager-hiërarchie niet is gekoppeld aan een tenant.
  
   ![Cloudsynchronisatie configureren](media/endpoint-security-edr-policy/cloud-sync.png)

3. Selecteer **OK** om de configuratie op te slaan.

   U kunt nu voor apparaten in deze verzameling Microsoft Defender ATP-beleid ontvangen.

## <a name="create-and-deploy-edr-policies"></a>EDR-beleid maken en implementeren

Wanneer uw Microsoft Defender ATP-abonnement is geïntegreerd met Intune, kunt u een EDR-beleid maken en implementeren. Er zijn twee verschillende typen EDR-beleid die u kunt maken. Eén beleidstype voor apparaten die u met Intune beheert via MDM. Het tweede type is voor apparaten die u beheert met Configuration Manager.

U kiest het type beleid dat u wilt maken tijdens het maken van een nieuw EDR-beleid wanneer u het platform voor het beleid kiest.

Voordat u beleid kunt implementeren op apparaten die worden beheerd door Configuration Manager, [stelt u Configuration Manager in ter ondersteuning van het EDR-beleid](#set-up-configuration-manager-to-support-edr-policy) vanuit het Microsoft Endpoint Manager-beheercentrum.

### <a name="create-edr-policies"></a>EDR-beleid maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Eindpuntbeveiliging** > **Eindpuntdetectie en -respons** > **Beleid maken**.

3. Selecteer het platform en het profiel voor uw beleid. De volgende informatie bepaalt uw opties:

   - Intune: Intune implementeert het beleid op apparaten in uw Azure AD-groepen. Wanneer u het beleid maakt, selecteert u:
     - Platform: **Windows 10 en hoger**
     - Profiel: **Eindpuntdetectie en -respons (MDM)**

   - Configuration Manager: Configuration Manager implementeert het beleid op apparaten in uw Configuration Manager-verzamelingen. Wanneer u het beleid maakt, selecteert u:
     - Platform: **Windows 10 en Windows Server**
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

- Voor beleidsregels die zijn gericht op het **Windows 10- en Windows Server**-platform (Configuration Manager), ziet u een overzicht van de naleving van het beleid, maar u kunt niet inzoomen om aanvullende informatie te bekijken. De weergave is beperkt omdat het beheercentrum gegevens met een beperkte status ontvangt van Configuration Manager, waarmee de implementatie van het beleid op Configuration Manager apparaten wordt beheerd.


[Bekijk de instellingen](endpoint-security-edr-profile-settings.md) die u voor de platformen en profielen kunt configureren.

## <a name="next-steps"></a>Volgende stappen

- [Eindpuntbeveiligingsbeleid configureren](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Meer informatie over [eindpuntdetectie en -respons](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) vindt u in de Microsoft Defender ATP-documentatie.

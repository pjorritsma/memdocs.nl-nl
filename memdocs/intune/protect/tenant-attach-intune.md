---
title: Gebruik Intune-beleidsregels met tenantgekoppelde Configuration Manager-apparaten | Microsoft Docs
description: Configureer de tenantkoppeling van Configuration Manager-apparaten in het Microsoft Endpoint Manager-beheercentrum, zodat u ondersteund beleid van Microsoft Intune op die apparaten kunt implementeren.
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
ms.openlocfilehash: d56b06b49846201d6198c1abc81185bf74765ae3
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823478"
---
# <a name="configure-tenant-attach-to-support-endpoint-security-policies-from-intune"></a>Tenantkoppeling configureren ter ondersteuning van Intune-eindpuntbeschermingsbeleid

Als u het scenario tenantkoppeling Configuration Manager gebruikt, kunt u de eindpuntbeveiligingsbeleidsregels van Intune implementeren op apparaten die u beheert met Configuration Manager. Als u dit scenario wilt gebruiken, moet u eerst tenantkoppeling configureren voor Configuration Manager en verzamelingen apparaten van Configuration Manager zo instellen dat deze met Intune kunnen worden gebruikt. Nadat verzamelingen zijn ingeschakeld voor gebruik, gebruikt u het Microsoft Endpoint Manager-beheercentrum voor het maken en implementeren van beleid.

De volgende beleidstypen worden ondersteund door Configuration Manager-apparaten die aan een tenant zijn gekoppeld:

- Antivirusbeleid voor eindpuntbeveiliging
- Eindpuntbeveiliging, -detectie en -responsbeleid

## <a name="requirements-to-use-intune-policy-for-tenant-attach"></a>Vereisten voor het gebruik van Intune-beleid voor tenantkoppeling

Om het gebruik van Intune-eindpuntbeveiligingsbeleidregels met Configuration Manager-apparaten te ondersteunen, heeft uw Configuration Manager-omgeving de volgende aanvullende configuraties nodig. In dit artikel vindt u [richtlijnen voor de configuratie](#set-up-configuration-manager-to-support-intune-policies):

### <a name="general-requirements-for-tenant-attach"></a>Algemene vereisten voor tenantkoppeling

- **Tenantkoppeling configureren**: met het *tenantkoppelingsscenario* kunt u verzamelingen apparaten van Configuration Manager synchroniseren met het Microsoft Configuration Manager-beheercentrum. Vervolgens kunt u het beheercentrum gebruiken voor het implementeren van ondersteund beleid voor deze verzamelingen.

  Tenantkoppeling wordt vaak geconfigureerd met co-beheer, maar u kunt ook een zelfstandige tenantkoppeling configureren.

- **Configuration Manager-verzamelingen synchroniseren**: wanneer u een tenantkoppeling configureert, kunt u de Configuration Manager-apparaatverzamelingen selecteren om te synchroniseren met Microsoft Endpoint Manager-beheercentrum. U kunt ook later terugkeren om de apparaatverzamelingen te wijzigen die u synchroniseert. Het ondersteunde beleid voor Configuration Manager-apparaten kan alleen worden toegewezen aan verzamelingen die u hebt gesynchroniseerd.

  Nadat u de verzamelingen hebt geselecteerd die u wilt synchroniseren, moet u deze inschakelen voor gebruik met eindpuntbeveiligingsbeleid van Intune.

- **Machtigingen voor Azure AD** - als u het instellen van een tenantkoppeling wilt voltooien, hebt u een account met globale beheerdersmachtigingen voor uw Azure-abonnement nodig.

### <a name="specific-requirements-for-intune-endpoint-security-policies"></a>Specifieke vereisten voor Intune-eindpuntbeveiligingsbeleidsregels

- **Antivirusbeleid**  (*voorbeeld*):

  - **Configuration Manager** - De volgende omgevingen worden ondersteund:

    - **Configuration Manager huidige branchversie 2006 of hoger** - ondersteuning voor het Intune-antivirusbeleid is toegevoegd met deze huidige branchversie.
    <!--
    - **Configuration Manager technical preview 2007 or later** - Support for Intune antivirus policies was added with this technical preview version. -->

  - **Tenant voor Microsoft Defender Advanced Threat Protection**: uw Microsoft Defender ATP-tenant moet worden geïntegreerd met uw Microsoft Endpoint Manager-tenant (Intune-abonnement).  Zie [Microsoft Defender ATP gebruiken](advanced-threat-protection.md) in de Intune-documentatie.

- **Eindpuntdetectie en -responsbeleid**:

  - **Configuration Manager** - De volgende omgevingen worden ondersteund:

    - **Configuration Manager technische preview 2003 of hoger** - ondersteuning voor Intune-eindpuntdetectie en -responsbeleid is toegevoegd met de technische previewversie 2003.

    - **Configuration Manager huidige branchversie 2002 of hoger** - als u Configuration Manager gebruikt met versie 2002, moet u de update in de console **Configuration Manager 2002 hotfix (KB4563473)** installeren. Met deze update schakelt u ondersteuning in Configuration Manager 2002 in voor het gebruik van eindpuntbeveiligingsbeleid.

  - **Tenant voor Microsoft Defender Advanced Threat Protection**: uw Microsoft Defender ATP-tenant moet worden geïntegreerd met uw Microsoft Endpoint Manager-tenant (Intune-abonnement).  Zie [Microsoft Defender ATP gebruiken](advanced-threat-protection.md) in de Intune-documentatie.

## <a name="set-up-configuration-manager-to-support-intune-policies"></a>Configuration Manager instellen om Intune-beleidsregels te ondersteunen

Voordat u Intune-beleid implementeert voor Configuration Manager-apparaten, moet u de configuraties uitvoeren die in de volgende secties worden beschreven. Met deze configuraties worden uw Configuration Manager-apparaten opgenomen met Microsoft Defender ATP en kunnen ze met Intune-beleidsregels werken.

De volgende taken worden uitgevoerd in de Configuration Manager-console. Als u niet bekend bent met Configuration Manager, kunt u in samenwerking met een Configuration Manager-beheerder deze taken uit te voeren.

1. [De update voor Configuration Manager installeren](#task-1-install-the-update-for-configuration-manager)
2. [Tenantkoppeling inschakelen](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Verzamelingen selecteren die u wilt synchroniseren](#task-3-select-collections-to-synchronize)
4. [Stel verzamelingen in staat om Intune-beleidsregels te ondersteunen](#task-4-enable-collections-for-endpoint-security-policies)

> [!TIP]
> Voor meer informatie over het gebruik van Microsoft Defender ATP met Configuration Manager raadpleegt u de volgende artikelen in de Configuration Manager-inhoud:
>
> - [Configuration Manager-clients onboarden naar Microsoft Defender ATP via het Microsoft Endpoint Manager-beheercentrum](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft Endpoint Manager-tenant koppelen: Synchronisatie van apparaten en apparaatacties](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Taak 1: De update voor Configuration Manager installeren

Als u de huidige branchversie 2002 van Configuration Manager gebruikt, moet u de volgende update in de console installeren die ondersteuning toevoegt voor de eindpuntbeveiligingsbeleidsregels die u implementeert vanuit het Microsoft Endpoint Manager-beheercentrum.

**Updatedetails**:

- **Hotfix (KB4563473) Configuration Manager 2002**

Als u deze update wilt installeren, volgt u de richtlijnen in [Console-updates installeren](../../configmgr/core/servers/manage/install-in-console-updates.md) in de Configuration Manager-documentatie.

Nadat u de update hebt geïnstalleerd, keert u terug om uw omgeving verder te configureren ter ondersteuning van het eindpuntbeveiligingsbeleid van het Microsoft Endpoint Manager-beheercentrum.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Taak 2: Tenantkoppeling configureren en verzamelingen synchroniseren

Met tenantkoppeling kunt u verzamelingen apparaten van uw Configuration Manager-implementatie synchroniseren met het Microsoft Endpoint Manager-beheercentrum. Na de synchronisatie van verzamelingen kunt u in het beheercentrum informatie over die apparaten bekijken en het eindpuntbeveiligingsbeleid van Intune erop implementeren.

Voor meer informatie over het tenantkoppelingsscenario raadpleegt u [Tenantkoppeling inschakelen](../../configmgr/tenant-attach/device-sync-actions.md) in de Configuration Manager-inhoud.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Tenantkoppeling inschakelen als co-beheer niet is ingeschakeld

> [!TIP]
> U gebruikt de wizard **Configuratie van co-beheer** in de Configuration Manager-console om tenantkoppeling in te schakelen, maar u hoeft geen co-beheer in te schakelen.
>
> Als u van plan bent om co-beheer in te schakelen, moet u bekend zijn met co-beheer, de bijbehorende vereisten en hoe u workloads beheert voordat u doorgaat. Zie [Wat is co-beheer?](../../configmgr/comanage/overview.md) in de Configuration Manager documentatie.

1. Ga in de Configuration Manager-beheerconsole naar **Beheer** > **Overzicht** > **Cloudservices** > **Co-beheer**.
2. Klik in het lint op **Co-beheer configureren** om de wizard te openen.
3. Selecteer op de pagina **Tenant-onboarding** de optie **AzurePublicCloud** voor uw omgeving. Azure Government-cloud wordt niet ondersteund.
   1. Klik op **Aanmelden**. Gebruik uw *globale beheerder*-account om u aan te melden.

   2. Zorg ervoor dat de optie **Uploaden naar het Microsoft Endpoint Manager-beheercentrum** is ingeschakeld op de pagina **Tenant-onboarding**.

   3. Verwijder het vinkje van **Automatische clientinschrijving voor co-beheer inschakelen**.

      Wanneer deze optie is geselecteerd, biedt de wizard extra pagina's om de installatie van co-beheer uit te voeren. Zie [Co-beheer inschakelen](../../configmgr/comanage/how-to-enable.md) in de Configuration Manager-inhoud voor meer informatie.

     ![Tenantkoppeling configureren](./media/tenant-attach-intune/tenant-onboarding.png)

4. Klik op **Volgende** en daarna op **Ja** om de melding **Een AAD-toepassing maken** te accepteren. Met deze actie wordt een service-principal ingericht en wordt een Azure AD-toepassingsregistratie gemaakt om de synchronisatie van verzamelingen met het Microsoft Endpoint Manager-beheercentrum te vergemakkelijken.

5. Configureer op de pagina **Upload configureren** de verzamelingen die u wilt synchroniseren. U kunt uw configuratie beperken tot een of enkele verzamelingen of door de aanbevolen instelling voor het uploaden van apparaten te gebruiken voor **alle apparaten die worden beheerd door Microsoft Endpoint Configuration Manager**.

   > [!TIP]
   > U kunt het selecteren van verzamelingen nu overslaan en later de informatie in de volgende taak (taak 3) gebruiken om te configureren welke verzamelingen moeten worden gesynchroniseerd met het Microsoft Endpoint Manager-beheercentrum.

6. Klik op **Samenvatting** om uw selectie te controleren en klik vervolgens op **Volgende**.

7. Klik op **Sluiten** als de wizard is voltooid.

   De tenantkoppeling is nu geconfigureerd en de geselecteerde verzamelingen worden gesynchroniseerd met het Microsoft Endpoint Manager-beheercentrum.

#### <a name="enable-tenant-attach-when-you-already-use-co-management"></a>Tenantkoppeling inschakelen wanneer u al co-beheer gebruikt

1. Ga in de Configuration Manager-beheerconsole naar **Beheer** > **Overzicht** > **Cloudservices** > **Co-beheer**.

2. Klik met de rechtermuisknop op uw instellingen voor co-beheer en selecteer **Eigenschappen**.

3. Selecteer **Uploaden naar Microsoft Endpoint Manager-beheercentrum** in het tabblad **Upload configureren**. Klik op **Toepassen**.

   De standaardinstelling voor het uploaden van apparaten is **Alle apparaten die worden beheerd door Microsoft Endpoint Configuration Manager**. U kunt er ook voor kiezen om uw configuratie te beperken tot een of enkele verzamelingen apparaten.

   ![Het tabblad Eigenschappen voor co-beheer bekijken](./media/tenant-attach-intune/configure-upload.png)

   > [!TIP]
   > U kunt het selecteren van verzamelingen nu overslaan en later de informatie in de volgende taak (taak 3) gebruiken om te configureren welke verzamelingen moeten worden gesynchroniseerd met het Microsoft Endpoint Manager-beheercentrum.

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

### <a name="task-4-enable-collections-for-endpoint-security-policies"></a>Taak 4: Verzamelingen inschakelen voor eindpuntbeveiligingsbeleid

Nadat u verzamelingen hebt geconfigureerd om te synchroniseren met het Microsoft Endpoint Manager-beheercentrum, kunt u deze verzamelingen gebruiken met eindpuntbeveiligingsbeleid. Als u verzamelingen van apparaten in Intune in staat stelt om met eindpuntbeveiligingsbeleid Intune te werken, configureert u apparaten in die verzamelingen voor onboarding met Microsoft Defender ATP.

#### <a name="enable-collections-for-use-with-endpoint-security-policies"></a>Stel verzamelingen in staat om met eindpuntbeveiligingsbeleid te werken

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](includes/make-configmgr-collection-available-edr.md)]

## <a name="next-steps"></a>Volgende stappen

- [Configureer eindpuntbeveiligingsbeleid](endpoint-security-policy.md#create-an-endpoint-security-policy) voor *antivirus* en *eindpuntdetectie en -respons*.

- Meer informatie over [eindpuntdetectie en -respons](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) vindt u in de Microsoft Defender ATP-documentatie.

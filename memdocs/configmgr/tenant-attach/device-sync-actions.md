---
title: Microsoft Endpoint Manager-tenant koppelen
titleSuffix: Configuration Manager
description: Upload uw Configuration Manager-apparaten naar de Cloud service en onderneem acties vanuit het beheer centrum.
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: be1c938cfcf332edb37e24e4094567f88f363560
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795615"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Micro soft Endpoint Manager-Tenant bijvoegen: synchronisatie van apparaten en acties van apparaten
<!--3555758 live 3/4/2020-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Micro soft Endpoint Manager is een geïntegreerde oplossing voor het beheer van al uw apparaten. Micro soft brengt Configuration Manager en intune samen in één console met de naam **micro soft Endpoint Manager-beheer centrum**.

Vanaf Configuration Manager versie 2002 kunt u uw Configuration Manager-apparaten uploaden naar de Cloud service en acties uitvoeren op de Blade **apparaten** in het beheer centrum.

## <a name="prerequisites"></a>Vereisten

- Een account dat een *globale beheerder* is voor het aanmelden bij het Toep assen van deze wijziging. Zie [Azure Active Directory (Azure AD)-beheerders rollen](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles)voor meer informatie.
   - Bij de voor bereiding wordt een app van derden en een service-principal voor de eerste partij gemaakt in uw Azure AD-Tenant.
- Een open bare Azure-cloud omgeving.
- De gebruikers accounts die acties voor apparaten activeren, hebben de volgende vereisten:
   - Is gedetecteerd met Azure Active Directory detectie van [gebruikers](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) en [Active Directory gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
      - Dit betekent dat het gebruikers account een gesynchroniseerd gebruikers object moet zijn in azure AD.
   - De machtiging **Configuration Manager actie initiëren** onder **externe taken** in het micro soft Endpoint Manager-beheer centrum.


## <a name="internet-endpoints"></a>Internet-eind punten

- `https://aka.ms/configmgrgateway`
- `https://*.manage.microsoft.com` <!--7424742-->

## <a name="enable-device-upload"></a>Apparaat uploaden inschakelen

- Als u co-beheer momenteel hebt ingeschakeld, [bewerkt u de eigenschappen voor co-beheer](#bkmk_edit) om het uploaden van apparaten in te scha kelen.
- Als er geen co-beheer is ingeschakeld, [gebruikt u de wizard voor het **configureren van co-beheer** om het](#bkmk_config) uploaden van apparaten in te scha kelen.
   - U kunt uw apparaten uploaden zonder automatische inschrijving in te scha kelen voor co-beheer of switch-workloads naar intune.
- Alle apparaten die worden beheerd door Configuration Manager die **Ja** in de kolom **client** bevatten, worden geüpload. Als dat nodig is, kunt u het uploaden beperken tot één verzameling apparaten.

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>Eigenschappen voor co-beheer bewerken om het uploaden van apparaten in te scha kelen

Als u co-beheer momenteel hebt ingeschakeld, bewerkt u de eigenschappen voor co-beheer om het uploaden van apparaten in te scha kelen met behulp van de onderstaande instructies:

1. Ga in de Configuration Manager-beheerconsole naar **Beheer** > **Overzicht** > **Cloudservices** > **Co-beheer**.
1. Klik met de rechtermuisknop op uw instellingen voor co-beheer en selecteer **Eigenschappen**.
1. Selecteer **Uploaden naar Microsoft Endpoint Manager-beheercentrum** in het tabblad **Upload configureren**. Klik op **Toepassen**.
   - De standaardinstelling voor het uploaden van apparaten is **Alle apparaten die worden beheerd door Microsoft Endpoint Configuration Manager**. Als dat nodig is, kunt u het uploaden beperken tot één verzameling apparaten.

   [![Wizard Configuratie van co-beheer](./media/3555758-configure-upload.png)](./media/3555758-configure-upload.png#lightbox)
1. Meld u aan met uw *globale beheerder*-account wanneer u hierom wordt gevraagd.
1. Klik op **Ja** om de melding **AAD-toepassing maken** te accepteren. Met deze actie wordt een service-principal ingericht en wordt een Azure AD-toepassingsregistratie gemaakt om de synchronisatie te vergemakkelijken.
1. Klik op **OK** om de eigenschappen voor co-beheer af te sluiten nadat u de wijzigingen hebt aangebracht.


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>Gebruik de wizard voor co-beheer configureren om het uploaden van apparaten in te scha kelen
Als er geen co-beheer is ingeschakeld, gebruikt u de wizard voor het **configureren van co-beheer** om het uploaden van apparaten in te scha kelen. U kunt uw apparaten uploaden zonder automatische inschrijving in te scha kelen voor co-beheer of switch-workloads naar intune. Schakel het uploaden van apparaten in met behulp van de onderstaande instructies:

1. Ga in de Configuration Manager-beheerconsole naar **Beheer** > **Overzicht** > **Cloudservices** > **Co-beheer**.
1. Klik in het lint op **Co-beheer configureren** om de wizard te openen.
1. Selecteer op de pagina **Tenant-onboarding** de optie **AzurePublicCloud** voor uw omgeving. Azure Government-cloud wordt niet ondersteund.
1. Klik op **Aanmelden**. Gebruik uw *globale beheerder*-account om u aan te melden.
1. Zorg ervoor dat de optie **uploaden naar micro soft Endpoint Manager-beheer centrum** is geselecteerd op de pagina voor **onboarding** van de Tenant.
   - Zorg ervoor dat de optie **automatische client registratie voor co-beheer inschakelen** niet is ingeschakeld als u co-beheer nu niet wilt inschakelen. Als u co-beheer wilt inschakelen, selecteert u de optie.
   - Als u co-beheer samen met het uploaden van het apparaat inschakelt, krijgt u extra pagina's in de wizard om te volt ooien. Zie [co-beheer inschakelen](../comanage/how-to-enable.md)voor meer informatie.

   [![Wizard Configuratie van co-beheer](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Klik op **Volgende** en daarna op **Ja** om de melding **Een AAD-toepassing maken** te accepteren. Met deze actie wordt een service-principal ingericht en wordt een Azure AD-toepassingsregistratie gemaakt om de synchronisatie te vergemakkelijken.
1. Selecteer op de pagina **Upload configureren** de aanbevolen instelling voor het uploaden van apparaten voor **alle apparaten die door micro soft endpoint Configuration Manager worden beheerd**. Als dat nodig is, kunt u het uploaden beperken tot één verzameling apparaten.
1. Klik op **Samenvatting** om uw selectie te controleren en klik vervolgens op **Volgende**.
1. Klik op **Sluiten** als de wizard is voltooid.  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>Uw uploads controleren

1. Open **CMGatewaySyncUploadWorker. log** van de ConfigMgr-installatiemap &lt;> \logs.
1. De volgende synchronisatie tijd wordt aangegeven door logboek vermeldingen die vergelijkbaar zijn met `Next run time will be at approximately: 02/28/2020 16:35:31` .
1. Voor het uploaden van apparaten zoekt u naar logboek vermeldingen die vergelijkbaar zijn met `Batching N records` . **N** is het aantal apparaten dat is geüpload naar de Cloud. 
1. De upload vindt elke 15 minuten plaats voor wijzigingen. Zodra de wijzigingen zijn geüpload, kan het vijf tot tien minuten duren voordat client wijzigingen worden weer gegeven in het **micro soft Endpoint Manager-beheer centrum**.

## <a name="perform-device-actions"></a>Acties op het apparaat uitvoeren

1. Ga in een browser naar`endpoint.microsoft.com`
1. Selecteer **apparaten** en vervolgens **alle apparaten** om de geüploade apparaten weer te geven. **ConfigMgr** wordt weer geven in de kolom **beheerd door** voor geüploade apparaten.
   [![Alle apparaten in het micro soft Endpoint Manager-beheer centrum](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Klik op een apparaat om de pagina **overzicht** te laden.
1. Klik op een van de volgende acties:
   - **Computerbeleid synchroniseren**
   - **Gebruikersbeleid synchroniseren**
   - **App-evaluatiecyclus**

   [![Overzicht van apparaten in het beheer centrum van micro soft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>Bekende problemen

### <a name="specific-devices-dont-synchronize"></a>Specifieke apparaten worden niet gesynchroniseerd

<!--7099564-->
Het is mogelijk dat bepaalde apparaten, die Configuration Manager-clients zijn, niet worden geüpload naar de service.

**Beïnvloede apparaten:** Als een apparaat een distributie punt is dat hetzelfde PKI-certificaat gebruikt voor de functionaliteit van het distributie punt en de client agent, wordt het apparaat niet opgenomen in de synchronisatie van het apparaat koppelen aan de Tenant.

**Gedrag:** Wanneer u een Tenant bijvoegt tijdens de on-board fase, wordt de eerste keer een volledige synchronisatie uitgevoerd. Volgende synchronisatie cycli zijn Delta synchronisaties. Een update van de betrokken apparaten zorgt ervoor dat het apparaat wordt verwijderd uit de synchronisatie.

## <a name="log-files"></a>Logboekbestanden
Gebruik de volgende logboeken die zich op het service verbindings punt bevinden:

- **CMGatewaySyncUploadWorker. log**
- **CMGatewayNotificationWorker. log**

## <a name="next-steps"></a>Volgende stappen

Zie [problemen met Tenant koppeling oplossen](technical-reference.md)voor meer informatie over het toevoegen van logboek bestanden voor de Tenant.

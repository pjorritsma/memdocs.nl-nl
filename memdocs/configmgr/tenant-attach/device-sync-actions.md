---
title: Microsoft Endpoint Manager-tenant koppelen
titleSuffix: Configuration Manager
description: Upload uw Configuration Manager-apparaten naar de Cloud service en onderneem acties vanuit het beheer centrum.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 676ae288003b257802eea495c4101a95129eaf34
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251861"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a> Micro soft Endpoint Manager-Tenant bijvoegen: synchronisatie van apparaten en acties van apparaten
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
- Als uw centrale beheer site een [externe provider](../core/plan-design/hierarchy/plan-for-the-sms-provider.md)heeft, volgt u de instructies voor de [CAS bevat een scenario voor externe provider](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) in het CMPivot-artikel. <!--7796824-->

## <a name="internet-endpoints"></a>Internet-eind punten

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

## <a name="enable-device-upload-when-co-management-is-already-enabled"></a><a name="bkmk_edit"></a> Het uploaden van apparaten inschakelen als co-beheer al is ingeschakeld

Als u co-beheer momenteel hebt ingeschakeld, gebruikt u de co-beheer eigenschappen om het uploaden van apparaten in te scha kelen. Als co-beheer nog niet is ingeschakeld, [gebruikt u de wizard voor **co-beheer configureren** ](#bkmk_config) om het uploaden van apparaten in te scha kelen.

Als co-beheer al is ingeschakeld, bewerkt u de eigenschappen voor co-beheer om het uploaden van apparaten in te scha kelen met behulp van de onderstaande instructies:

1. Ga in de Configuration Manager-beheerconsole naar **Beheer** > **Overzicht** > **Cloudservices** > **Co-beheer**.
1. Selecteer in het lint **Eigenschappen** voor het productie beleid voor co-beheer.
1. Selecteer **Uploaden naar Microsoft Endpoint Manager-beheercentrum** in het tabblad **Upload configureren**. Selecteer **Toepassen**.
   - De standaardinstelling voor het uploaden van apparaten is **Alle apparaten die worden beheerd door Microsoft Endpoint Configuration Manager**. Als dat nodig is, kunt u het uploaden beperken tot één verzameling apparaten.
1. Schakel de optie in om **endpoint Analytics in te scha kelen voor apparaten die zijn geüpload naar micro soft Endpoint Manager** als u ook inzicht wilt krijgen in het optimaliseren van de eindgebruikers ervaring in [endpoint Analytics](../../analytics/overview.md).

   [![Apparaten uploaden naar het beheer centrum van micro soft Endpoint Manager](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. Meld u aan met uw *globale beheerder*-account wanneer u hierom wordt gevraagd.
1. Selecteer **Ja** om de melding voor **Aad-toepassingen maken** te accepteren. Met deze actie wordt een service-principal ingericht en wordt een Azure AD-toepassingsregistratie gemaakt om de synchronisatie te vergemakkelijken.
1. Kies **OK** om de eigenschappen voor co-beheer af te sluiten nadat u de wijzigingen hebt aangebracht.


## <a name="enable-device-upload-when-co-management-isnt-enabled"></a><a name="bkmk_config"></a> Het uploaden van apparaten inschakelen als co-beheer niet is ingeschakeld

Als co-beheer niet is ingeschakeld, gebruikt u de wizard voor het **configureren van co-beheer** om het uploaden van apparaten in te scha kelen. U kunt uw apparaten uploaden zonder automatische inschrijving in te scha kelen voor co-beheer of switch-workloads naar intune. Alle apparaten die worden beheerd door Configuration Manager die **Ja** in de kolom **client** bevatten, worden geüpload. Als dat nodig is, kunt u het uploaden beperken tot één verzameling apparaten. Als co-beheer al is ingeschakeld in uw omgeving, [bewerkt u de eigenschappen voor co-beheer](#bkmk_edit) om het uploaden van apparaten in te scha kelen.

Als co-beheer niet is ingeschakeld, gebruikt u de onderstaande instructies om het uploaden van apparaten in te scha kelen:

1. Ga in de Configuration Manager-beheerconsole naar **Beheer** > **Overzicht** > **Cloudservices** > **Co-beheer**.
1. Selecteer in het lint **co-beheer configureren** om de wizard te openen.
1. Selecteer op de pagina **Tenant-onboarding** de optie **AzurePublicCloud** voor uw omgeving. Azure Government Cloud en Azure China 21Vianet worden niet ondersteund.
1. Selecteer **Aanmelden.** Gebruik uw *globale beheerder*-account om u aan te melden.
1. Zorg ervoor dat de optie **uploaden naar micro soft Endpoint Manager-beheer centrum** is geselecteerd op de pagina voor **onboarding** van de Tenant.
   - Zorg ervoor dat de optie **automatische client registratie voor co-beheer inschakelen** niet is ingeschakeld als u co-beheer nu niet wilt inschakelen. Als u co-beheer wilt inschakelen, selecteert u de optie.
   - Als u co-beheer samen met het uploaden van het apparaat inschakelt, krijgt u extra pagina's in de wizard om te volt ooien. Zie [co-beheer inschakelen](../comanage/how-to-enable.md)voor meer informatie.

   [![Wizard Configuratie van co-beheer](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Klik op **volgende** en vervolgens op **Ja** om de melding voor **Aad-toepassingen maken** te accepteren. Met deze actie wordt een service-principal ingericht en wordt een Azure AD-toepassingsregistratie gemaakt om de synchronisatie te vergemakkelijken.
     - U kunt eventueel een eerder gemaakte Azure AD-toepassing importeren tijdens het voorbereiden van het toevoegen van een Tenant (vanaf versie 2006). Zie de sectie [een eerder gemaakte Azure AD-toepassing importeren](#bkmk_aad_app) voor meer informatie.
1. Selecteer op de pagina **Upload configureren** de aanbevolen instelling voor het uploaden van apparaten voor **alle apparaten die door micro soft endpoint Configuration Manager worden beheerd**. Als dat nodig is, kunt u het uploaden beperken tot één verzameling apparaten.
1. Schakel de optie in om **endpoint Analytics in te scha kelen voor apparaten die zijn geüpload naar micro soft Endpoint Manager** als u ook inzicht wilt krijgen in het optimaliseren van de ervaring van de eind gebruiker in [endpoint Analytics](../../analytics/overview.md)
1. Selecteer **samen vatting** om uw selectie te controleren en klik vervolgens op **volgende**.
1. Wanneer de wizard is voltooid, selecteert u **sluiten**.  

## <a name="perform-device-actions"></a>Acties op het apparaat uitvoeren

1. Ga in een browser naar `endpoint.microsoft.com`
1. Selecteer **apparaten** en vervolgens **alle apparaten** om de geüploade apparaten weer te geven. **ConfigMgr** wordt weer geven in de kolom **beheerd door** voor geüploade apparaten.
   [![Alle apparaten in het micro soft Endpoint Manager-beheer centrum](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Selecteer een apparaat om de **overzichts** pagina te laden.
1. Kies een van de volgende acties:
   - **Computerbeleid synchroniseren**
   - **Gebruikersbeleid synchroniseren**
   - **App-evaluatiecyclus**

   [![Overzicht van apparaten in het beheer centrum van micro soft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="import-a-previously-created-azure-ad-application-optional"></a><a name="bkmk_aad_app"></a> Een eerder gemaakte Azure AD-toepassing importeren (optioneel)
<!--6479246-->
*(Geïntroduceerd in versie 2006)*

Tijdens een [nieuwe onboarding](#bkmk_config)kan een beheerder een eerder gemaakte toepassing opgeven tijdens het voorbereiden op het koppelen van de Tenant. Deel of gebruik Azure AD-toepassingen niet over meerdere hiërarchieën. Als u meerdere hiërarchieën hebt, maakt u afzonderlijke Azure AD-toepassingen voor elk.

Selecteer **optioneel een afzonderlijke web-app voor het synchroniseren van Configuration Manager-client gegevens naar het micro soft Endpoint Manager-beheer centrum**op de pagina voor **onboarding van tenants** in de wizard voor het **configureren van co-beheer**. Met deze optie wordt u gevraagd om de volgende informatie op te geven voor uw Azure AD-App:

- Naam van Azure AD-Tenant
- Azure AD-tenant-id
- De naam van de toepassing
- Client-id
- Geheime sleutel
- Verval datum van geheime sleutel
- App-id-URI

### <a name="azure-ad-application-permissions-and-configuration"></a>Machtigingen en configuratie van Azure AD-toepassing

Voor het gebruik van een eerder gemaakte toepassing tijdens het voorbereiden op een Tenant moet u de volgende machtigingen hebben:

- Configuration Manager micro service-machtigingen:
   - CmCollectionData. Read
   - CmCollectionData. write

- Microsoft Graph machtigingen:
   - Directory. Read. alle [toepassingen, machtiging](https://docs.microsoft.com/graph/permissions-reference#application-permissions)
   - Directory. Read. alle [gemachtigde Directory-machtigingen](https://docs.microsoft.com/graph/permissions-reference#directory-permissions)

- Zorg ervoor dat de **beheerder toestemming geven voor de Tenant** is geselecteerd voor de Azure AD-toepassing. Zie [toestemming geven voor beheerders in app-registraties](https://docs.microsoft.com/azure/active-directory/manage-apps/grant-admin-consent)voor meer informatie.

- De geïmporteerde toepassing moet als volgt worden geconfigureerd:
   - Alleen geregistreerd voor **accounts in deze organisatie Directory**. Zie [wijzigen wie toegang heeft tot uw toepassing](https://docs.microsoft.com/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application)voor meer informatie.
   -  Heeft een geldige URI voor de toepassings-ID en een geheim



## <a name="next-steps"></a>Volgende stappen

- [Configuration Manager apparaten inschrijven bij Endpoint Analytics](../../analytics/enroll-configmgr.md#bkmk_cm_enroll)
- Zie [problemen met Tenant koppeling oplossen](troubleshoot.md)voor meer informatie over het toevoegen van logboek bestanden voor de Tenant.

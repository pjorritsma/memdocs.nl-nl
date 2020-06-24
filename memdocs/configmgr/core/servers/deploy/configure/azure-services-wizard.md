---
title: Azure-services configureren
titleSuffix: Configuration Manager
description: Verbind uw Configuration Manager-omgeving met Azure-Services voor Cloud beheer, Microsoft Store voor bedrijven en Log Analytics.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6ca5307de5c7df54c3cf7924bc91b0175b1bfa39
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715319"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Azure-Services configureren voor gebruik met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de **wizard Azure-Services** om het proces te vereenvoudigen van het configureren van de Azure-Cloud Services die u gebruikt met Configuration Manager. Deze wizard biedt een algemene configuratie-ervaring met behulp van de web-app-registraties van Azure Active Directory (Azure AD). Deze apps bieden abonnements-en configuratie gegevens en verifiëren communicatie met Azure AD. De app vervangt elke keer dat u een nieuw Configuration Manager onderdeel of service met Azure instelt, dezelfde informatie.

## <a name="available-services"></a>Beschik bare Services

Configureer de volgende Azure-Services met behulp van deze wizard:  

- **Cloud beheer**: met deze service kunnen de site en clients worden geverifieerd met behulp van Azure AD. Deze verificatie maakt andere scenario's mogelijk, zoals:  

  - [Configuration Manager Windows 10-clients installeren en toewijzen met behulp van Azure AD voor verificatie](../../../clients/deploy/deploy-clients-cmg-azure.md)  

  - [Azure AD-gebruikers detectie configureren](configure-discovery-methods.md#azureaadisc)  

  - [Detectie van Azure AD-gebruikers groepen configureren](configure-discovery-methods.md#bkmk_azuregroupdisco)

  - Ondersteuning voor bepaalde [scenario's voor Cloud beheer gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

  - [E-mail meldingen voor app-goed keuring](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Log Analytics connector**: [Maak verbinding met Azure log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm). Verzamelings gegevens synchroniseren met Log Analytics.  

    > [!Note]  
    > In dit artikel wordt verwezen naar de *log Analytics-connector*, voorheen de *OMS-connector*genoemd. Er is geen functioneel verschil. Zie [Azure Management-monitoring](https://docs.microsoft.com/azure/azure-monitor/terminology#log-analytics)voor meer informatie.  

- **Microsoft Store voor bedrijven**: Maak verbinding met de [Microsoft Store voor bedrijven](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md). Ontvang Store-apps voor uw organisatie die u kunt implementeren met Configuration Manager.  

### <a name="service-details"></a>Service Details

De volgende tabel bevat informatie over elk van de services.  

- **Tenants**: het aantal service-exemplaren dat u kunt configureren. Elk exemplaar moet een afzonderlijke Azure AD-Tenant zijn.  

- **Clouds**: alle services ondersteunen de wereld wijde Azure-Cloud, maar niet alle services ondersteunen persoonlijke Clouds, zoals de Azure US Government-Cloud.  

- **Web-app**: of de service gebruikmaakt van een Azure AD-App van het type *Web app/API*, ook wel een server-app genoemd in Configuration Manager.  

- **Systeem eigen app**: of de service gebruikmaakt van een Azure AD-App van het type *native*, ook wel een client-app genoemd in Configuration Manager.  

- **Acties**: of u deze apps kunt importeren of maken in de Configuration Manager wizard Azure-Services.  

|Service  |Tenants  |Clouds  |Web-app  |Systeemeigen app  |Acties  |
|---------|---------|---------|---------|---------|---------|
|Cloud beheer met<br>Azure AD-detectie | Meerdere | Openbaar, privé | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | Importeren, maken |
|Log Analytics-connector | Eén | Openbaar, privé | ![Ondersteund](media/green_check.png) | ![Niet ondersteund](media/Red_X.png) | Importeren |
|Microsoft Store voor<br>Business | Eén | Public | ![Ondersteund](media/green_check.png) | ![Niet ondersteund](media/Red_X.png) | Importeren, maken |

### <a name="about-azure-ad-apps"></a>Over Azure AD-apps

Voor verschillende Azure-Services zijn verschillende configuraties vereist, die u aanbrengt in de Azure Portal. Daarnaast kunnen de apps voor elke service afzonderlijke machtigingen voor Azure-resources vereisen.  

U kunt één app gebruiken voor meer dan één service. Er is slechts één object om te beheren in Configuration Manager en Azure AD. Wanneer de beveiligings sleutel op de app verloopt, hoeft u slechts één sleutel te vernieuwen.

Wanneer u aanvullende Azure-Services in de wizard maakt, is Configuration Manager ontworpen om gegevens te hergebruiken die gemeen schappelijk zijn tussen services. Dit gedrag zorgt ervoor dat u niet meer dan één keer dezelfde informatie hoeft in te voeren.

Zie het betreffende Configuration Manager-artikel in de [beschik bare Services](#available-services)voor meer informatie over de vereiste app-machtigingen en configuraties voor elke service.

Voor meer informatie over Azure-apps begint u met de volgende artikelen:

- [Verificatie en autorisatie in Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)
- [Overzicht van Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)
- [Basis beginselen van het registreren van een toepassing in azure AD](/azure/active-directory/develop/authentication-scenarios)  
- [Uw toepassing registreren bij uw Azure Active Directory-Tenant](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)

## <a name="before-you-begin"></a>Voordat u begint

Nadat u hebt bepaald welke service u wilt verbinden, raadpleegt u de tabel in [service Details](#service-details). Deze tabel bevat informatie die u nodig hebt om de wizard Azure-service te volt ooien. Een bespreking van uw Azure AD-beheerder hebben. Bepaal welke van de volgende acties moeten worden uitgevoerd:

- Maak de apps hand matig vooraf in de Azure Portal. Importeer vervolgens de app-Details in Configuration Manager.  

- Gebruik Configuration Manager om de apps rechtstreeks in azure AD te maken. Lees de informatie in de andere secties van dit artikel om de benodigde gegevens te verzamelen uit Azure AD.  

Voor sommige services moet de Azure AD-app specifieke machtigingen hebben. Controleer de informatie voor elke service om de vereiste machtigingen te bepalen. Voordat u bijvoorbeeld een web-app kunt importeren, moet een Azure-beheerder deze eerst maken in de [Azure Portal](https://portal.azure.com).

Wanneer u de Log Analytics-connector configureert, geeft u uw nieuw geregistreerde *Web app-* machtigings rechten voor de resource groep die de relevante werk ruimte bevat. Met deze machtiging kunnen Configuration Manager toegang krijgen tot die werk ruimte. Wanneer u de machtiging toewijst, zoekt u naar de naam van de app-registratie in het gedeelte **gebruikers toevoegen** van de Azure Portal. Dit proces is hetzelfde als bij het [leveren van Configuration Manager met machtigingen voor log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). Een Azure-beheerder moet deze machtigingen toewijzen voordat u de app in Configuration Manager importeert.

## <a name="start-the-azure-services-wizard"></a>De wizard Azure-Services starten

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure-Services** .  

2. Selecteer op het tabblad **Start** van het lint in de groep **Azure-Services** Azure- **Services configureren**.  

3. Op de pagina **Azure-Services** van de wizard Azure-Services:  

    1. Geef een **naam** op voor het object in Configuration Manager.  

    2. Geef een optionele **Beschrijving** op die u kan helpen bij het identificeren van de service.  

    3. Selecteer de Azure-service die u wilt verbinden met Configuration Manager.  

4. Selecteer **volgende** om door te gaan naar de pagina met [Eigenschappen van Azure app](#azure-app-properties) van de wizard Azure-Services.  

## <a name="azure-app-properties"></a>Eigenschappen van Azure-app

Selecteer op de pagina **app** van de wizard Azure-Services eerst de **Azure-omgeving** in de lijst. Raadpleeg de tabel in [service Details](#service-details) waarvoor de omgeving momenteel beschikbaar is voor de service.

De rest van de app-pagina varieert afhankelijk van de specifieke service. Raadpleeg de tabel in [service Details](#service-details) voor welk type app door de service wordt gebruikt en welke actie u kunt gebruiken.

- Als de app zowel importeren als acties maken ondersteunt, selecteert u **Bladeren**. Met deze actie wordt het [dialoog venster server-app](#server-app-dialog) of het [dialoog venster Client-App](#client-app-dialog)geopend.  

- Als de app de import actie alleen ondersteunt, selecteert u **importeren**. Met deze actie wordt het [dialoog venster apps importeren (Server)](#import-apps-dialog-server) of het [dialoog venster apps importeren (client)](#import-apps-dialog-client)geopend.

Nadat u de apps op deze pagina hebt opgegeven, selecteert u **volgende** om door te gaan naar de pagina [configuratie of detectie](#configuration-or-discovery) van de wizard Azure-Services.

### <a name="web-app"></a>Web-app

Deze app is de Azure AD *-type Web-app/-API*, ook wel een server-app genoemd in Configuration Manager.

#### <a name="server-app-dialog"></a>Dialoog venster server-app

Wanneer u **Bladeren** voor de **Web-app** selecteert op de pagina app van de wizard Azure-Services, wordt het dialoog venster Server-App geopend. Er wordt een lijst weer gegeven met de volgende eigenschappen van alle bestaande web-apps:

- Beschrijvende naam voor Tenant
- Beschrijvende naam van app
- Servicetype

Er zijn drie acties die u kunt uitvoeren in het dialoog venster van de server-app:

- Als u een bestaande web-app opnieuw wilt gebruiken, selecteert u deze in de lijst.
- Selecteer **importeren** om het [dialoog venster apps importeren](#import-apps-dialog-server)te openen.
- Selecteer **maken** om het [dialoog venster Server toepassing maken](#create-server-application-dialog)te openen.

Nadat u een web-app hebt geselecteerd, geïmporteerd of gemaakt, selecteert u **OK** om het dialoog venster server-app te sluiten. Met deze actie keert u terug naar de [app-pagina](#azure-app-properties) van de wizard Azure-Services.

#### <a name="import-apps-dialog-server"></a>Dialoog venster apps importeren (Server)

Wanneer u **importeren** selecteert in het dialoog venster van de server-app of de app-pagina van de wizard Azure-Services, wordt het dialoog venster apps importeren geopend. Op deze pagina kunt u informatie invoeren over een Azure AD-web-app die al is gemaakt in de Azure Portal. Meta gegevens over die web-app worden geïmporteerd in Configuration Manager. Geef de volgende informatie op:

- **Azure AD-Tenant naam**: de naam van uw Azure AD-Tenant.
- **Azure AD-Tenant-id**: de GUID van uw Azure AD-Tenant.
- **Toepassings naam**: een beschrijvende naam voor de app, de weergave naam in de app-registratie.
- **Client-id**: de waarde van de **toepassings-id (client)** van de app-registratie. De indeling is een standaard-GUID.
- **Geheime sleutel**: u moet de geheime sleutel kopiëren wanneer u de app registreert in azure AD.
- **Verloop van geheime sleutel**: Selecteer een datum in de toekomst in de agenda.
- **App-ID-URI**: deze waarde moet uniek zijn in uw Azure AD-Tenant. Het is in het toegangs token dat door de Configuration Manager-client wordt gebruikt om toegang tot de service aan te vragen. De waarde is de **URI van de toepassings-id** van de app-registratie vermelding in de Azure AD-Portal. De indeling is vergelijkbaar met `https://ConfigMgrService` .

Nadat u de gegevens hebt ingevoerd, selecteert u **verifiëren**. Selecteer **OK** om het dialoog venster apps importeren te sluiten. Met deze actie keert u terug naar de [app-pagina](#azure-app-properties) van de wizard Azure-Services of het dialoog venster voor de [Server toepassing](#server-app-dialog).

> [!TIP]
> Wanneer u de app registreert in azure AD, moet u de volgende **omleidings-URI**mogelijk hand matig opgeven: `ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>` . Geef de client-ID-GUID van de app op, bijvoorbeeld: `ms-appx-web://Microsoft.AAD.BrokerPlugin/a26a653e-17aa-43eb-ab36-0e36c7d29f49` .<!-- SCCMDocs#1135 -->

#### <a name="create-server-application-dialog"></a>Dialoog venster Server toepassing maken

Wanneer u **maken** selecteert in het dialoog venster server-app, wordt het dialoog venster Server toepassing maken geopend. Op deze pagina wordt het maken van een web-app in azure AD geautomatiseerd. Geef de volgende informatie op:

- **Toepassings naam**: een beschrijvende naam voor de app.
- **URL van start pagina**: deze waarde wordt niet gebruikt door Configuration Manager, maar is vereist voor Azure AD. Standaard is deze waarde ingesteld op `https://ConfigMgrService`.  
- **App-ID-URI**: deze waarde moet uniek zijn in uw Azure AD-Tenant. Het is in het toegangs token dat door de Configuration Manager-client wordt gebruikt om toegang tot de service aan te vragen. Standaard is deze waarde ingesteld op `https://ConfigMgrService`.  
- **Geldigheids duur van geheime sleutel**: Kies **1 jaar** of **2 jaar** in de vervolg keuzelijst. Een jaar is de standaard waarde.

Selecteer **Aanmelden** om te verifiëren bij Azure als gebruiker met beheerders rechten. Deze referenties worden niet opgeslagen door Configuration Manager. Deze persoon heeft geen machtigingen nodig in Configuration Manager en hoeft niet hetzelfde account te zijn dat de wizard Azure-Services uitvoert. Nadat de verificatie naar Azure is geslaagd, wordt op de pagina de naam van de **Azure AD-Tenant** voor referentie weer gegeven.

Selecteer **OK** om de web-app te maken in azure AD en sluit het dialoog venster Server toepassing maken. Met deze actie keert u terug naar het [dialoog venster van de server toepassing](#server-app-dialog).

> [!NOTE]
> Als u een beleid voor voorwaardelijke toegang voor Azure AD hebt gedefinieerd en dit geldt voor **alle Cloud-apps** , moet u de gemaakte server toepassing uitsluiten van dit beleid. Zie de [documentatie voor voorwaardelijke toegang van Azure AD](https://docs.microsoft.com/azure/active-directory/conditional-access/)voor meer informatie over het uitsluiten van specifieke apps.

### <a name="native-client-app"></a>Systeem eigen client-app

Deze app is de Azure AD-type *systeem eigen*, ook wel een client-app genoemd in Configuration Manager.

#### <a name="client-app-dialog"></a>Dialoog venster Client-App

Wanneer u **Bladeren** selecteert voor de **systeem eigen client-app** op de pagina app van de wizard Azure-Services, wordt het dialoog venster van de client-App geopend. Er wordt een lijst weer gegeven met de volgende eigenschappen van alle bestaande systeem eigen apps:

- Beschrijvende naam voor Tenant
- Beschrijvende naam van app
- Servicetype

Er zijn drie acties die u kunt uitvoeren in het dialoog venster Client-App:

- Als u een bestaande systeem eigen app opnieuw wilt gebruiken, selecteert u deze in de lijst. 
- Selecteer **importeren** om het [dialoog venster apps importeren](#import-apps-dialog-client)te openen.
- Selecteer **maken** om het [dialoog venster client toepassing maken](#create-client-application-dialog)te openen.

Nadat u een systeem eigen app hebt geselecteerd, geïmporteerd of gemaakt, kiest u **OK** om het dialoog venster client-app te sluiten. Met deze actie keert u terug naar de [app-pagina](#azure-app-properties) van de wizard Azure-Services.

#### <a name="import-apps-dialog-client"></a>Dialoog venster apps importeren (client)

Wanneer u **importeren** selecteert in het dialoog venster client-app, wordt het dialoog venster apps importeren geopend. Op deze pagina kunt u informatie invoeren over een systeem eigen Azure AD-app die al is gemaakt in de Azure Portal. Meta gegevens over die systeem eigen app worden geïmporteerd in Configuration Manager. Geef de volgende informatie op:

- **Toepassings naam**: een beschrijvende naam voor de app.
- **Client-id**: de waarde van de **toepassings-id (client)** van de app-registratie. De indeling is een standaard-GUID.

Nadat u de gegevens hebt ingevoerd, selecteert u **verifiëren**. Selecteer **OK** om het dialoog venster apps importeren te sluiten. Met deze actie keert u terug naar het [dialoog venster Client-App](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Dialoog venster client toepassing maken

Wanneer u **maken** selecteert in het dialoog venster client-app, wordt het dialoog venster client toepassing maken geopend. Op deze pagina wordt het maken van een systeem eigen app in azure AD geautomatiseerd. Geef de volgende informatie op:

- **Toepassings naam**: een beschrijvende naam voor de app.
- **Antwoord-URL**: deze waarde wordt niet gebruikt door Configuration Manager, maar is vereist voor Azure AD. Standaard is deze waarde ingesteld op `https://ConfigMgrService`.

Selecteer **Aanmelden** om te verifiëren bij Azure als gebruiker met beheerders rechten. Deze referenties worden niet opgeslagen door Configuration Manager. Deze persoon heeft geen machtigingen nodig in Configuration Manager en hoeft niet hetzelfde account te zijn dat de wizard Azure-Services uitvoert. Nadat de verificatie naar Azure is geslaagd, wordt op de pagina de naam van de **Azure AD-Tenant** voor referentie weer gegeven.

Selecteer **OK** om de systeem eigen app in azure ad te maken en sluit het dialoog venster client toepassing maken. Met deze actie keert u terug naar het [dialoog venster Client-App](#client-app-dialog).

## <a name="configuration-or-discovery"></a>Configuratie of detectie

Nadat u de web-en systeem eigen apps op de pagina apps hebt opgegeven, gaat de wizard Azure-Services naar een **configuratie** -of **detectie** pagina, afhankelijk van de service waarmee u verbinding maakt. De details van deze pagina variëren van service naar service. Zie een van de volgende artikelen voor meer informatie:  

- **Cloud Management** service, **detectie** pagina: [Azure AD-gebruikers detectie configureren](configure-discovery-methods.md#azureaadisc)  

- **Log Analytics-connector** service, **configuratie** pagina: [de verbinding met log Analytics configureren](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- Pagina **configuraties** **van Microsoft Store for Business** -service: [Microsoft Store voor zakelijke synchronisatie configureren](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

Ten slotte voltooit u de wizard Azure-Services via de pagina's samen vatting, voortgang en voltooiing. U hebt de configuratie van een Azure-service in Configuration Manager voltooid. Herhaal dit proces om andere Azure-Services te configureren.

## <a name="renew-secret-key"></a><a name="bkmk_renew"></a>Geheime sleutel vernieuwen

### <a name="renew-key-for-created-app"></a>Sleutel voor gemaakte app vernieuwen

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure Active Directory tenants** .

1. Selecteer in het detail venster de Azure AD-Tenant voor de app.

1. Selecteer in het lint de optie **geheime sleutel vernieuwen**. Geef de referenties op van de eigenaar van de app of een Azure AD-beheerder.

### <a name="renew-key-for-imported-app"></a>Sleutel voor geïmporteerde app vernieuwen

Als u de Azure-app in Configuration Manager hebt geïmporteerd, gebruikt u de Azure Portal om te verlengen. Noteer de nieuwe geheime sleutel en de verval datum. Voeg deze informatie toe aan de wizard **geheime sleutel vernieuwen** .  

> [!NOTE]
> Sla de geheime sleutel op voordat u de Azure Application eigenschappen- **sleutel** pagina sluit. Deze informatie wordt verwijderd wanneer u de pagina sluit.

## <a name="view-the-configuration-of-an-azure-service"></a>De configuratie van een Azure-service weer geven

Bekijk de eigenschappen van een Azure-service die u hebt geconfigureerd voor gebruik. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer **Azure-Services**. Selecteer de service die u wilt weer geven of bewerken en selecteer vervolgens **Eigenschappen**.

Als u een service selecteert en vervolgens **verwijderen** kiest in het lint, wordt met deze actie de verbinding in Configuration Manager verwijderd. De app wordt niet verwijderd uit Azure AD. Vraag uw Azure-beheerder om de app te verwijderen wanneer deze niet meer nodig is. Of voer de wizard Azure-service uit om de app te importeren.<!--483440-->

## <a name="cloud-management-data-flow"></a>Gegevens stroom voor Cloud beheer

Het volgende diagram is een conceptuele gegevens stroom voor de interactie tussen Configuration Manager, Azure AD en verbonden Cloud Services. Dit specifieke voor beeld maakt gebruik van de **Cloud Management** -service, die een Windows 10-client bevat en zowel server-als client-apps. De stromen voor andere services zijn vergelijkbaar.

![Gegevens stroom diagram voor Configuration Manager met Azure AD en Cloud Management](media/aad-auth.png)

1. De Configuration Manager-beheerder importeert of maakt de client-en server-apps in azure AD.  

2. Configuration Manager Azure AD-gebruikers detectie methode wordt uitgevoerd. De site gebruikt het Azure AD server-app-token om Microsoft Graph voor gebruikers objecten op te vragen.  

3. Op de site worden gegevens over de gebruikers objecten opgeslagen. Zie [Azure AD-gebruikers detectie](about-discovery-methods.md#azureaddisc)voor meer informatie.  

4. De Configuration Manager-client vraagt het Azure AD-gebruikers token op. De client maakt de claim met behulp van de toepassings-ID van de Azure AD-client-app en de server-app als de doel groep. Zie [claims in azure AD-beveiligings tokens](/azure/active-directory/develop/authentication-scenarios#security-tokens)voor meer informatie.  

5. De client wordt geverifieerd met de-site door het Azure AD-token te presen teren aan de Cloud beheer gateway en het on-premises HTTPS-ingeschakelde beheer punt.  

Zie [Azure AD-verificatie werk stroom](../../../clients/manage/azure-ccmsetup.md)voor meer gedetailleerde informatie.

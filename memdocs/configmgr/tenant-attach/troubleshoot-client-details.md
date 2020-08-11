---
title: Problemen met client Details oplossen
titleSuffix: Configuration Manager
description: Client Details voor het koppelen van Configuration Manager tenants oplossen
ms.date: 07/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d983e0c3d84f5bcbf411af1243ddc045d66d9199
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051581"
---
# <a name="troubleshoot-configmgr-client-details-in-the-admin-center-preview"></a>Problemen met ConfigMgr-client Details in het beheer centrum oplossen (preview-versie)
<!--6374854, 6521921-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik het volgende om de details van ConfigMgr-clients in het beheer centrum van micro soft Endpoint Manager op te lossen:

> [!Important]
> Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Veelvoorkomende fouten in het beheer centrum van micro soft Endpoint Manager

Wanneer u de details van de ConfigMgr-client bekijkt, kunt u een van deze fouten uitvoeren.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a>De benodigde configuratie ontbreekt in Azure Active Directory

**Fout bericht:** De benodigde configuratie ontbreekt in Azure Active Directory. Zorg ervoor dat u de Configuration Manager-site koppelt aan uw Azure-Tenant en wijs de juiste gebruikersrol toe in azure AD.

**Mogelijke oorzaak:** In het gebruikers account ontbreekt waarschijnlijk de gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD. Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt. Het kan tot een uur duren voordat wijzigingen in deze machtiging van kracht worden.

### <a name="unable-to-get-device-or-collection-information"></a><a name="bkmk_noinfo"></a>Kan geen apparaat-of verzamelings gegevens ophalen

**Fout bericht 1:** Kan geen gegevens over client Details (of verzameling) ophalen. Zorg ervoor dat Azure AD en AD-gebruikers detectie zijn geconfigureerd en dat de gebruiker wordt gedetecteerd door beide. Controleer of de gebruiker de juiste machtigingen heeft in Configuration Manager.

**Mogelijke oorzaken:** Deze fout wordt meestal veroorzaakt door een probleem met het beheerders account. Hieronder vindt u de meest voorkomende problemen met het gebruikers account met beheerders rechten:

1. Gebruik hetzelfde account om u aan te melden bij het beheer centrum. De on-premises identiteit moet worden gesynchroniseerd met en overeenkomen met de Cloud identiteit.
1. Controleer of het account de machtiging **lezen** heeft voor de **verzameling** van het apparaat in Configuration Manager.
1. Zorg ervoor dat Configuration Manager het gebruikers account met beheerders ervaring heeft gedetecteerd dat u gebruikt. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Selecteer het knoop punt **gebruikers** en zoek uw gebruikers account.

    Als uw account niet wordt weer gegeven in het knoop punt **gebruikers** , controleert u de configuratie van de [Active Directory gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)van de site.

1. Controleer de detectie gegevens. Selecteer uw gebruikersaccount. Selecteer in het lint op het tabblad **Start** de optie **Eigenschappen**. Bevestig in het venster Eigenschappen de volgende detectie gegevens:

    - **Azure Active Directory Tenant-id**: deze waarde moet een GUID zijn voor de Azure AD-Tenant.
    - **Azure Active Directory gebruikers-id**: deze waarde moet een GUID zijn voor dit account in azure AD.
    - **Principal-naam van gebruiker**: de indeling van deze waarde is user@domain . Bijvoorbeeld `jqpublic@contoso.com`.

    Als de Azure AD-eigenschappen leeg zijn, controleert u de configuratie van de [Azure AD-gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)van de site.


### <a name="unexpected-error-occurred"></a><a name="bkmk_1603"></a>Er is een onverwachte fout opgetreden

**Fout bericht:** Er is een onverwachte fout opgetreden

**Mogelijke oorzaken:** Onverwachte fouten worden meestal veroorzaakt door een [service aansluitpunt](../core/servers/deploy/configure/about-the-service-connection-point.md), een [beheer service](../develop/adminservice/overview.md)of verbindings problemen.

1. Controleer of het service verbindings punt verbinding heeft met de Cloud met behulp van **CMGatewayNotificationWorker. log**.
1. Controleer of de beheer service in orde is door het SMS_REST_PROVIDER onderdeel van de bewaking van site componenten op de centrale site te controleren.
1. IIS moet zijn geïnstalleerd op de provider computer. Zie [vereisten voor de beheer service](../develop/adminservice/overview.md#prerequisites)voor meer informatie.
1. Controleer of de klok op het service verbindings punt synchroon is. Als de klok van het service aansluitpunt zich iets achter bevindt, past u [KB4563473-Update Rollup toe voor Configuration Manager versie 2002-Tenant problemen toevoegen](https://support.microsoft.com/help/4563473). Controleer **AdminService. log** op de provider computer op fouten.

## <a name="known-issues"></a>Bekende problemen

### <a name="gettingresultstimedout"></a>Time-out tijdens ophalen van resultaten

**Scenario:** Als u een extern service verbindings punt hebt en u 2002 vroege update ring hebt geïnstalleerd vóór 30 maart 2020, ziet u een time-outfout in het beheer centrum.

**Fout bericht:** Time-out tijdens ophalen van resultaten. Zorg ervoor dat het Configuration Manager service-verbindings punt operationeel is en een verbinding heeft met de Cloud.

**Tijdelijke oplossing:** Kopieer de `Microsoft.ConfigurationManagement.ManagementProvider.dll` map van de site server `bin\x64` naar de map van het externe service-verbindings punt `bin\x64` .  Start de `SMS_EXECUTIVE` service op de Service Connection Point-server opnieuw.

### <a name="boundary-groups-list-is-empty"></a>Lijst met grens groepen is leeg

**Fout bericht**: er zijn geen grens groepen gevonden of de gebruiker is niet gemachtigd om informatie over de grens groep weer te geven.

De lege lijst is een bekend probleem voor Configuration Manager versie 2002 wanneer u een hiërarchie van Configuration Manager sites hebt.

:::image type="content" source="media/6024387-known-issue-device-details.png" alt-text="Lijst met grens groepen is leeg" lightbox="media/6024387-known-issue-device-details.png":::

## <a name="next-steps"></a>Volgende stappen

[Problemen met tenantkoppeling oplossen](troubleshoot.md)

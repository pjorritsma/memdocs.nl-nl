---
title: Problemen oplossen met scripts voor apparaten die zijn geüpload naar het beheer centrum
titleSuffix: Configuration Manager
description: Probleemoplossings scripts voor het koppelen van Configuration Manager tenants
ms.date: 09/18/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: a0eb1e8f-2c85-4f48-a0b5-945b3e5f63f3
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: b42663e649f50d1a785bf929d0b03fb4d2eb0632
ms.sourcegitcommit: af4fc4f928203c1bfdb27499a56c91fe0ebae854
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/18/2020
ms.locfileid: "90803279"
---
# <a name="troubleshoot-scripts-preview-for-devices-uploaded-to-the-admin-center"></a>Problemen oplossen met scripts (preview) voor apparaten die zijn geüpload naar het beheer centrum
<!--6024392-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik het volgende om problemen met scripts in het beheer centrum van micro soft Endpoint Manager op te lossen:

> [!Important]
> Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

## <a name="common-issues"></a>Algemene problemen

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> De benodigde configuratie ontbreekt in Azure Active Directory

**Fout bericht:** De benodigde configuratie ontbreekt in Azure Active Directory. Zorg ervoor dat u de Configuration Manager-site koppelt aan uw Azure-Tenant en wijs de juiste gebruikersrol toe in azure AD.

**Mogelijke oorzaak:** In het gebruikers account ontbreekt waarschijnlijk de gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD. Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt. Het kan tot een uur duren voordat wijzigingen in deze machtiging van kracht worden.

### <a name="configuration-manager-doesnt-meet-the-minimum-version-prerequisite"></a><a name="bkmk_version"></a> Configuration Manager voldoet niet aan de vereiste voor de minimum versie

**Fout bericht:** Configuration Manager voldoet niet aan de vereiste voor de minimum versie.

**Mogelijke oorzaken:** Op uw Configuration Manager-sites wordt niet de minimale versie van Configuration Manager 2006 met [KB4580678-Tenant attached Rollup voor Configuration Manager current branch, versie 2006](https://support.microsoft.com/help/4580678) geïnstalleerd. Controleer het volgende:
 - Configuration Manager versie 2006 of hoger is geïnstalleerd.
 - Die [KB4580678](https://support.microsoft.com/help/4580678) op sites met Configuration Manager versie 2006.
 - Elke site in de hiërarchie voldoet aan de minimum vereisten die hierboven worden vermeld.

### <a name="unable-to-get-scripts-information"></a><a name="bkmk_403"></a> Kan geen informatie over de scripts ophalen

**Fout bericht:** Kan geen informatie over de scripts ophalen. Zorg ervoor dat Azure AD en AD-gebruikers detectie zijn geconfigureerd en dat het gebruikers account dat toegang heeft tot de Tenant functies van het micro soft Endpoint Manager-beheer centrum wordt gedetecteerd door beide. Controleer of de gebruiker de juiste machtigingen heeft in Configuration Manager.

**Mogelijke oorzaken:** Deze fout wordt meestal veroorzaakt door een probleem met het beheerders account. Hieronder vindt u de meest voorkomende problemen met het gebruikers account met beheerders rechten:

1. Gebruik hetzelfde account om u aan te melden bij het beheer centrum. De on-premises identiteit moet worden gesynchroniseerd met en overeenkomen met de Cloud identiteit.
1. Controleer of het account de machtiging **lezen** heeft voor de **verzameling** van het apparaat in Configuration Manager.
1. Controleer of het account de machtiging **resource lezen** heeft voor de **verzameling** van het apparaat in Configuration Manager.
1. Zorg ervoor dat Configuration Manager het gebruikers account met beheerders rechten heeft gedetecteerd dat u gebruikt voor toegang tot de functies voor het koppelen van tenants in het micro soft Endpoint Manager-beheer centrum. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Selecteer het knoop punt **gebruikers** en zoek uw gebruikers account.

    Als uw account niet wordt weer gegeven in het knoop punt **gebruikers** , controleert u de configuratie van de [Active Directory gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)van de site.

1. Controleer de detectie gegevens. Selecteer uw gebruikersaccount. Selecteer in het lint op het tabblad **Start** de optie **Eigenschappen**. Bevestig in het venster Eigenschappen de volgende detectie gegevens:

    - **Azure Active Directory Tenant-id**: deze waarde moet een GUID zijn voor de Azure AD-Tenant.
    - **Azure Active Directory gebruikers-id**: deze waarde moet een GUID zijn voor dit account in azure AD.
    - **Principal-naam van gebruiker**: de indeling van deze waarde is user@domain . Bijvoorbeeld `jqpublic@contoso.com`.

    Als de Azure AD-eigenschappen leeg zijn, controleert u de configuratie van de [Azure AD-gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)van de site.


### <a name="unable-to-get-device-information"></a><a name="bkmk_noinfo"></a> Kan de apparaatgegevens niet ophalen

**Fout bericht:** Kan geen apparaatgegevens ophalen. Zorg ervoor dat Azure AD en AD-gebruikers detectie zijn geconfigureerd en dat de gebruiker wordt gedetecteerd door beide. Controleer of de gebruiker de juiste machtigingen heeft in Configuration Manager.

**Mogelijke oorzaak:** Zorg ervoor dat Configuration Manager het gebruikers account met beheerders rechten heeft gedetecteerd dat u gebruikt voor toegang tot de functies voor het koppelen van tenants in het micro soft Endpoint Manager-beheer centrum. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Selecteer het knoop punt **gebruikers** en zoek uw gebruikers account.

   Als uw account niet wordt weer gegeven in het knoop punt **gebruikers** , controleert u de configuratie van de [Active Directory gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)van de site.

1. Controleer de detectie gegevens. Selecteer uw gebruikersaccount. Selecteer in het lint op het tabblad **Start** de optie **Eigenschappen**. Bevestig in het venster Eigenschappen de volgende detectie gegevens:

    - **Azure Active Directory Tenant-id**: deze waarde moet een GUID zijn voor de Azure AD-Tenant.
    - **Azure Active Directory gebruikers-id**: deze waarde moet een GUID zijn voor dit account in azure AD.
    - **Principal-naam van gebruiker**: de indeling van deze waarde is user@domain . Bijvoorbeeld `jqpublic@contoso.com`.

    Als de Azure AD-eigenschappen leeg zijn, controleert u de configuratie van de [Azure AD-gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)van de site.


### <a name="unexpected-error-occurred"></a><a name="bkmk_1603"></a> Er is een onverwachte fout opgetreden

**Fout bericht:** Er is een onverwachte fout opgetreden

#### <a name="possible-cause"></a>Mogelijke oorzaak

Controleer of het account de machtiging **resource lezen** heeft voor de **verzameling** van het apparaat in Configuration Manager.

#### <a name="error-code-500-with-an-unexpected-error-occurred-message"></a>Fout code 500 met een onverwachte fout opgetreden bericht

Als u `System.Security.SecurityException` in het **AdminService. log**ziet, controleert u of uw User Principal Name (UPN) die door [Active Directory gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) is gedetecteerd, niet is ingesteld op een Cloud-UPN in plaats van een lokale UPN. Een lege UPN-waarde is ook acceptabel omdat de naam van het Active Directory gedetecteerde domein wordt gebruikt. Als u alleen Cloud-UPN (voor beeld: onmicrosoft.com) ziet die geen geldig domein UPN (contoso.com) is, hebt u een probleem en moet u [het UPN-achtervoegsel instellen in Active Directory](/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization#add-upn-suffixes-and-update-your-users-to-them).


#### <a name="other-possible-causes-of-unexpected-errors"></a>Andere mogelijke oorzaken van onverwachte fouten

Onverwachte fouten worden meestal veroorzaakt door een [service aansluitpunt](../core/servers/deploy/configure/about-the-service-connection-point.md), een [beheer service](../develop/adminservice/overview.md)of verbindings problemen.

1. Controleer of het service verbindings punt verbinding heeft met de Cloud met behulp van **CMGatewayNotificationWorker. log**.
1. Controleer of de beheer service in orde is door het SMS_REST_PROVIDER onderdeel van de bewaking van site componenten op de centrale site te controleren.
1. IIS moet zijn geïnstalleerd op de provider computer. Zie [vereisten voor de beheer service](../develop/adminservice/overview.md#prerequisites)voor meer informatie.

## <a name="known-issues"></a>Bekende problemen

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

---
title: Problemen met resource Explorer oplossen
titleSuffix: Configuration Manager
description: Problemen met resource Explorer oplossen voor het koppelen van Configuration Manager tenants
ms.date: 09/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 05829d36-2cbf-4921-bf4b-cfcdef4cfcc1
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 013bbb631b62a46927d9430751ac796237bfcefc
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643569"
---
# <a name="troubleshoot-resource-explorer-for-devices-uploaded-to-the-admin-center-preview"></a>Problemen met resource Explorer oplossen voor apparaten die zijn geüpload naar het beheer centrum (preview)
<!--6479284-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik het volgende om problemen met resource Explorer voor ConfigMgr-apparaten in het micro soft Endpoint Manager-beheer centrum op te lossen:

> [!Important]
> Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Veelvoorkomende fouten in het beheer centrum van micro soft Endpoint Manager

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> De benodigde configuratie ontbreekt in Azure Active Directory

**Fout bericht:** De benodigde configuratie ontbreekt in Azure Active Directory. Zorg ervoor dat u de Configuration Manager-site koppelt aan uw Azure-Tenant en wijs de juiste gebruikersrol toe in azure AD.

**Mogelijke oorzaak:** In het gebruikers account ontbreekt waarschijnlijk de gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD. Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt. Het kan tot een uur duren voordat wijzigingen in deze machtiging van kracht worden.

### <a name="unable-to-get-resource-information"></a><a name="bkmk_noinfo"></a> Kan geen resource gegevens ophalen

**Fout bericht 1:** Kan geen resource gegevens ophalen. Zorg ervoor dat Azure AD en AD-gebruikers detectie zijn geconfigureerd en dat de gebruiker wordt gedetecteerd door beide. Controleer of de gebruiker de juiste machtigingen heeft in Configuration Manager.

**Mogelijke oorzaken:** Deze fout wordt meestal veroorzaakt door een probleem met het beheerders account. Hieronder vindt u de meest voorkomende problemen met het gebruikers account met beheerders rechten:

1. Gebruik hetzelfde account om u aan te melden bij het beheer centrum. De on-premises identiteit moet worden gesynchroniseerd met en overeenkomen met de Cloud identiteit.
1. Controleer of het account de machtiging **lezen** heeft voor de **verzameling** van het apparaat in Configuration Manager.
1. Zorg ervoor dat Configuration Manager het gebruikers account met beheerders rechten heeft gedetecteerd dat u gebruikt voor toegang tot de functies voor het koppelen van tenants in het micro soft Endpoint Manager-beheer centrum. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Selecteer het knoop punt **gebruikers** en zoek uw gebruikers account.

    Als uw account niet wordt weer gegeven in het knoop punt **gebruikers** , controleert u de configuratie van de [Active Directory gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)van de site.

1. Controleer de detectie gegevens. Selecteer uw gebruikersaccount. Selecteer in het lint op het tabblad **Start** de optie **Eigenschappen**. Bevestig in het venster Eigenschappen de volgende detectie gegevens:

    - **Azure Active Directory Tenant-id**: deze waarde moet een GUID zijn voor de Azure AD-Tenant.
    - **Azure Active Directory gebruikers-id**: deze waarde moet een GUID zijn voor dit account in azure AD.
    - **Principal-naam van gebruiker**: de indeling van deze waarde is user@domain . Bijvoorbeeld `jqpublic@contoso.com`.

    Als de Azure AD-eigenschappen leeg zijn, controleert u de configuratie van de [Azure AD-gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)van de site.

### <a name="the-site-information-hasnt-yet-synchronized"></a><a name="bkmk_sync"></a> De site gegevens zijn nog niet gesynchroniseerd

**Fout bericht:** De site-informatie is nog niet gesynchroniseerd van Configuration Manager naar het micro soft Endpoint Manager-beheer centrum. 

**Mogelijke oorzaken:**
- Deze fout treedt doorgaans op wanneer nieuw onboarding wordt toegevoegd aan de Tenant. Wacht een uur tot de gegevens zijn gesynchroniseerd.
- Deze fout kan ook optreden als de centrale beheer site is bijgewerkt naar een nieuwe versie van Configuration Manager, maar er nog geen upgrade is uitgevoerd voor sommige onderliggende primaire sites.

### <a name="unable-to-load-inventory-classes"></a><a name="bkmk_load"></a> Kan inventaris klassen niet laden

**Fout bericht:** Kan geen inventaris klassen laden voor uw omgeving.

**Mogelijke oorzaken:**

- De lijst met entiteiten is mogelijk niet van on-premises geüpload. Wacht een uur en kijk of de fout zich blijft voordoen.
- Er is mogelijk een ongeldige **Tenant-id** of **hiërarchie-id** opgegeven. Controleer het service aansluitpunt en controleer of het werkt.
- Kan de query niet uitvoeren om klassen op te halen. Wacht 15 minuten om te controleren of de fout zich blijft voordoen.

### <a name="failed-to-get-inventory-classes-with-data"></a><a name="bkmk_get"></a> Kan geen inventaris klassen met gegevens ophalen

**Fout bericht:** Kan geen inventaris klassen met gegevens ophalen. On-premises fout 500.

**Mogelijke oorzaken:** Onverwachte fouten worden meestal veroorzaakt door een [service aansluitpunt](../core/servers/deploy/configure/about-the-service-connection-point.md), een [beheer service](../develop/adminservice/overview.md)of verbindings problemen.

1. Controleer of het service verbindings punt verbinding heeft met de Cloud met behulp van **CMGatewayNotificationWorker. log**.
1. Controleer of de beheer service in orde is door het SMS_REST_PROVIDER onderdeel van de bewaking van site componenten op de centrale site te controleren.
1. IIS moet zijn geïnstalleerd op de provider computer. Zie [vereisten voor de beheer service](../develop/adminservice/overview.md#prerequisites)voor meer informatie.

### <a name="the-user-does-not-have-permissions"></a><a name="bkmk_user"></a> De gebruiker heeft geen machtigingen

**Fout bericht:** Kan geen inventaris klassen met gegevens ophalen. De gebruiker heeft geen machtigingen.

**Mogelijke oorzaken:** De gebruiker heeft mogelijk geen toegang tot de verzameling waarvan het apparaat deel uitmaakt. Controleer de volgende items:

1. Gebruik hetzelfde account om u aan te melden bij het beheer centrum. De on-premises identiteit moet worden gesynchroniseerd met en overeenkomen met de Cloud identiteit.
1. Controleer of het account de machtiging **lezen** heeft voor de **verzameling** van het apparaat in Configuration Manager.
1. Zorg ervoor dat Configuration Manager het gebruikers account met beheerders ervaring heeft gedetecteerd dat u gebruikt. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Selecteer het knoop punt **gebruikers** en zoek uw gebruikers account.

    Als uw account niet wordt weer gegeven in het knoop punt **gebruikers** , controleert u de configuratie van de [Active Directory gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)van de site.

## <a name="known-issues"></a>Bekende problemen

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Volgende stappen

[Problemen met tenantkoppeling oplossen](troubleshoot.md)
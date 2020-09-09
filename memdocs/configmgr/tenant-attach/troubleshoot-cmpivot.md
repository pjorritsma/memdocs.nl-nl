---
title: Problemen oplossen met CMPivot voor apparaten die zijn geüpload naar het beheer centrum
titleSuffix: Configuration Manager
description: Problemen met CMPivot voor Configuration Manager Tenant toevoegen
ms.date: 09/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 86f97154-c9fc-4efd-9d49-4a253cef5953
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d1ca270bc1095e1596f5e725c16a97f4e42e4411
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564303"
---
# <a name="troubleshoot-cmpivot-preview-for-devices-uploaded-to-the-admin-center"></a>Problemen oplossen met CMPivot (preview) voor apparaten die zijn geüpload naar het beheer centrum
<!--6024392-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik het volgende om problemen met CMPivot in het beheer centrum van micro soft Endpoint Manager op te lossen:

> [!Important]
> Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

## <a name="common-issues"></a>Algemene problemen

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> De benodigde configuratie ontbreekt in Azure Active Directory

**Fout bericht:** De benodigde configuratie ontbreekt in Azure Active Directory. Zorg ervoor dat u de Configuration Manager-site koppelt aan uw Azure-Tenant en wijs de juiste gebruikersrol toe in azure AD.

**Mogelijke oorzaak:** In het gebruikers account ontbreekt waarschijnlijk de gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD. Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt. Het kan tot een uur duren voordat wijzigingen in deze machtiging van kracht worden.

### <a name="unable-to-get-device-information"></a><a name="bkmk_noinfo"></a> Kan de apparaatgegevens niet ophalen

**Fout bericht 1:** Kan geen apparaatgegevens ophalen. Zorg ervoor dat Azure AD en AD-gebruikers detectie zijn geconfigureerd en dat de gebruiker wordt gedetecteerd door beide. Controleer of de gebruiker de juiste machtigingen heeft in Configuration Manager.

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


### <a name="not-authorized-to-view-query-results"></a><a name="bkmk_rbac"></a> Niet gemachtigd om query resultaten weer te geven

**Fout bericht:** Niet gemachtigd om query resultaten weer te geven. Controleer of u machtigingen hebt gekregen voor CMPivot in Configuration Manager

**Mogelijke oorzaken:** Controleer of het gebruikers account machtigingen heeft voor CMPivot. Zie [machtigingen voor CMPivot](cmpivot-start.md#permissions)voor meer informatie.

#### <a name="other-possible-causes-of-unexpected-errors"></a><a name="bkmk_other"></a> Andere mogelijke oorzaken van onverwachte fouten

Onverwachte fouten worden meestal veroorzaakt door een [service aansluitpunt](../core/servers/deploy/configure/about-the-service-connection-point.md), een [beheer service](../develop/adminservice/overview.md)of verbindings problemen.

1. Controleer of het service verbindings punt verbinding heeft met de Cloud met behulp van **CMGatewayNotificationWorker. log**.
1. Controleer of de beheer service in orde is door het SMS_REST_PROVIDER onderdeel van de bewaking van site componenten op de centrale site te controleren.
1. IIS moet zijn geïnstalleerd op de provider computer. Zie [vereisten voor de beheer service](../develop/adminservice/overview.md#prerequisites)voor meer informatie.

## <a name="known-issues"></a>Bekende problemen

### <a name="inconsistent-results-for-some-operators-with-configuration-manager-version-2002"></a>Inconsistente resultaten voor sommige Opera tors met Configuration Manager versie 2002
<!--7784718, 7884272-->
Wanneer u CMPivot gebruikt vanuit het micro soft Endpoint Manager-beheer centrum met Configuration Manager versie 2002, krijgt u mogelijk inconsistente resultaten voor de volgende Opera tors:

- Samenvatten op
- Houd
- Sorteren op
- Boven
- Aantal
- Distinct

**Oplossing**: [Als u KB4578123-CMPivot-query's installeert, worden onverwachte resultaten geretourneerd in Configuration Manager huidige vertakking versie 2002](https://support.microsoft.com/help/4578123).

### <a name="when-the-sms-provider-is-remote-from-the-cas-you-may-encounter-an-internal-server-error-from-the-admin-console"></a><a name="bkmk_dblhop"></a> Wanneer de SMS-provider extern van de certificerings instantie is, kan er een interne server fout optreden in de beheer console

**Fout bericht:** On-premises fout code: 500 interne server fout

**Scenario 1:** Bij het uitvoeren van Configuration Manager versie 2002 en er een externe provider voor de certificerings instantie is, kan er een interne server fout optreden in de beheer console.

**Scenario 2:** Als Configuration Manager versie 2006 wordt uitgevoerd, kan deze fout ook optreden als het service verbindings punt geen verbinding kan maken met de provider op de primaire site en terugvalt op de provider voor de CAS. 

**Scenario 3:** Als de CAS is bijgewerkt naar versie 2006, maar de primaire site nog niet is bijgewerkt, worden de aanvragen doorgestuurd via de CAS-provider. Als de provider extern is, kan er een interne server fout optreden in de beheer console. 

**Tijdelijke oplossing:** Volg de instructies voor de [CAS bevat een scenario voor een externe provider](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) in het CMPivot-artikel om dit "dubbele hop"-scenario te omzeilen.


[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Volgende stappen

[Problemen met tenantkoppeling oplossen](troubleshoot.md)

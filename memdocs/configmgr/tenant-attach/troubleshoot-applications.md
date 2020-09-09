---
title: Problemen met de installatie van toepassingen oplossen
titleSuffix: Configuration Manager
description: Problemen met de installatie van een toepassing voor Configuration Manager Tenant koppelen
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 75f47456-cd8d-4c83-8dc5-98b336a7c6c8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 7e02c642c95952c8751f03a8e1cb8838feff1155
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564040"
---
# <a name="troubleshoot-application-installation-for-devices-uploaded-to-the-admin-center-preview"></a>Problemen met de installatie van een toepassing oplossen voor apparaten die zijn geüpload naar het beheer centrum (preview-versie)
<!--6374854, 6521921-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik het volgende om problemen met Configuration Manager-toepassingen in het micro soft Endpoint Manager-beheer centrum op te lossen:

> [!Important]
> Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Veelvoorkomende fouten in het beheer centrum van micro soft Endpoint Manager

Wanneer u toepassingen weergeeft of installeert vanuit het micro soft-beheer centrum voor eind punten, kunt u een van deze fouten uitvoeren.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> De benodigde configuratie ontbreekt in Azure Active Directory

**Fout bericht:** De benodigde configuratie ontbreekt in Azure Active Directory. Zorg ervoor dat u de Configuration Manager-site koppelt aan uw Azure-Tenant en wijs de juiste gebruikersrol toe in azure AD.

**Mogelijke oorzaak:** In het gebruikers account ontbreekt waarschijnlijk de gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD. Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt. Het kan tot een uur duren voordat wijzigingen in deze machtiging van kracht worden.

### <a name="unable-to-get-application-information"></a><a name="bkmk_noinfo"></a> Kan geen toepassings gegevens ophalen

**Fout bericht 1:** Kan geen toepassings gegevens ophalen. Zorg ervoor dat Azure AD en AD-gebruikers detectie zijn geconfigureerd en dat de gebruiker wordt gedetecteerd door beide. Controleer of de gebruiker de juiste machtigingen heeft in Configuration Manager.

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

### <a name="unexpected-error-occurred"></a><a name="bkmk_1603"></a> Er is een onverwachte fout opgetreden

**Fout bericht:** Er is een onverwachte fout opgetreden

#### <a name="error-code-500-with-an-unexpected-error-occurred-message"></a>Fout code 500 met een onverwachte fout opgetreden bericht

1. Als u `System.Security.SecurityException` in het **AdminService. log**ziet, controleert u of uw User Principal Name (UPN) die door [Active Directory gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) is gedetecteerd, niet is ingesteld op een Cloud-UPN in plaats van een lokale UPN. Een lege UPN-waarde is ook acceptabel omdat de naam van het Active Directory gedetecteerde domein wordt gebruikt. Als u alleen Cloud-UPN (voor beeld: onmicrosoft.com) ziet die geen geldig domein UPN (contoso.com) is, hebt u een probleem en moet u [het UPN-achtervoegsel instellen in Active Directory](/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization#add-upn-suffixes-and-update-your-users-to-them).
1. [KB4576782-invoeg toepassingen in het micro soft Endpoint Manager-beheer centrum](https://support.microsoft.com/help/4576782) installeren als de onderstaande fout wordt weer gegeven in de **AdminService. log**:
   ```log 
   System.Data.Entity.Core.EntityCommandExecutionException: An error occurred while executing the command definition. See the inner exception for details.
   System.Data.SqlClient.SqlException: Execution Timeout Expired.  The timeout period elapsed prior to completion of the operation or the server is not responding.
   System.ComponentModel.Win32Exception: The wait operation timed out
   ```

#### <a name="error-code-3-with-an-unexpected-error-occurred-message"></a>Fout code 3 met een onverwachte fout opgetreden bericht

De beheer service is niet actief of IIS is niet geïnstalleerd. IIS moet zijn geïnstalleerd op de provider computer. Zie [vereisten voor de beheer service](../develop/adminservice/overview.md#prerequisites)voor meer informatie.

#### <a name="other-possible-causes-of-unexpected-errors"></a>Andere mogelijke oorzaken van onverwachte fouten

Onverwachte fouten worden meestal veroorzaakt door een [service aansluitpunt](../core/servers/deploy/configure/about-the-service-connection-point.md), een [beheer service](../develop/adminservice/overview.md)of verbindings problemen.

1. Controleer of het service verbindings punt verbinding heeft met de Cloud met behulp van **CMGatewayNotificationWorker. log**.
1. Controleer of de beheer service in orde is door het SMS_REST_PROVIDER onderdeel van de bewaking van site componenten op de centrale site te controleren.
1. IIS moet zijn geïnstalleerd op de provider computer. Zie [vereisten voor de beheer service](../develop/adminservice/overview.md#prerequisites)voor meer informatie.


### <a name="the-site-information-hasnt-yet-synchronized"></a><a name="bkmk_sync"></a> De site gegevens zijn nog niet gesynchroniseerd

**Fout bericht:** De site-informatie is nog niet gesynchroniseerd van Configuration Manager naar het micro soft Endpoint Manager-beheer centrum. Wacht tot 15 minuten nadat u de site hebt gekoppeld aan uw Azure-Tenant.

**Mogelijke oorzaken:**
- Deze fout treedt doorgaans op wanneer nieuw onboarding wordt toegevoegd aan de Tenant. Wacht tot een uur voordat de gegevens worden gesynchroniseerd.
- Deze fout kan ook optreden als de centrale beheer site is bijgewerkt naar een nieuwe versie van Configuration Manager, maar er nog geen upgrade is uitgevoerd voor sommige onderliggende primaire sites.

### <a name="application-shows-as-installed-after-creating-a-new-deployment"></a><a name="bkmk_installed"></a> De toepassing wordt weer gegeven als geïnstalleerd na het maken van een nieuwe implementatie

**Symptoom:** Een toepassing wordt weer gegeven als geïnstalleerd in het beheer centrum van micro soft Endpoint Manager na het maken van een nieuw apparaat vereist goedkeurings implementatie of een beschik bare implementatie van een gebruiker.

**Mogelijke oorzaak:** De toepassings status die voor dat apparaat wordt weer gegeven, is van een andere actieve of eerdere implementatie.

### <a name="errors-when-searching-or-retrying-an-installation"></a><a name="bkmk_hfru"></a> Fouten bij het zoeken of opnieuw proberen van een installatie

**Symptoom:** Er treden fouten op bij het uitvoeren van de volgende acties:
- De zoekfunctie gebruiken
- Selecteer **installatie opnieuw uitvoeren**

**Mogelijke oorzaak:**  Zorg ervoor dat [Update pakket voor micro soft Endpoint Configuration Manager versie 2002](https://support.microsoft.com/help/4560496/) en de bijbehorende versie van de-console is geïnstalleerd. Zie [vereisten voor het installeren van een toepassing vanuit het beheer centrum](applications.md#prerequisites)voor meer informatie.

## <a name="known-issues"></a>Bekende problemen

### <a name="application-installation-times-out-if-application-requires-restart"></a>Er is een time-out opgeassen tijdens de installatie van de toepassing

**Scenario:** Als u Configuration Manager versie 2002 en een toepassing moet opnieuw worden opgestart om het installatie proces te volt ooien, is er mogelijk een time-out opgetreden tijdens de installatie.

**Symptomen:** De gebruiker ziet `restart pending` meldingen en in Software Center. In het beheer centrum van micro soft Endpoint Manager blijft de toepassing in de `Installing` status.  

**Tijdelijke oplossing:** Zodra de gebruiker het apparaat opnieuw opstart, wordt de juiste status weer gegeven in het beheer centrum.

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]


## <a name="next-steps"></a>Volgende stappen

[Problemen met tenantkoppeling oplossen](troubleshoot.md)
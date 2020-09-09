---
title: Problemen met de tijd lijn van het apparaat oplossen
titleSuffix: Configuration Manager
description: Problemen oplossen met de tijd lijn van het apparaat voor het koppelen van Configuration Manager Tenant
ms.date: 09/8/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 54a58548-45f3-4f75-93d6-d2fd96227e6a
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 979ec6f081a318886eda9eeac91c16adc635701d
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564306"
---
# <a name="troubleshoot-the-timeline-for-devices-uploaded-to-the-admin-center-preview"></a><a name="bkmk_timeline"></a> Problemen met de tijd lijn oplossen voor apparaten die zijn geüpload naar het beheer centrum (preview-versie)
<!--CM7141381, IN7552762 pubpreview Sept8, 2020 -->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik het volgende om problemen met de tijd lijn van het apparaat in het beheer centrum van micro soft Endpoint Manager op te lossen:

> [!Important]
> Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.


## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_common"></a> Veelvoorkomende fouten in het beheer centrum van micro soft Endpoint Manager

Wanneer u de tijd lijn vanuit het micro soft-beheer centrum voor eind punten bekijkt of wilt synchroniseren, kunt u een van deze fouten uitvoeren.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_401"></a> De benodigde configuratie ontbreekt in Azure Active Directory

**Fout bericht:** De benodigde configuratie ontbreekt in Azure Active Directory. Zorg ervoor dat u de Configuration Manager-site koppelt aan uw Azure-Tenant en wijs de juiste gebruikersrol toe in azure AD.

**Mogelijke oorzaken:**

- Zorg ervoor dat [Azure AD-gebruikers](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) detectie en [Active Directory gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) zijn geconfigureerd en dat de gebruiker wordt gedetecteerd door beide.
- In het gebruikers account ontbreekt mogelijk de gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD. Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt. Het kan tot een uur duren voordat wijzigingen in deze machtiging van kracht worden.

### <a name="unable-to-get-timeline-information"></a><a name="bkmk_403"></a> Kan geen tijdlijn gegevens ophalen

**Fout bericht:** Kan geen tijdlijn gegevens ophalen. Zorg ervoor dat de Azure AD-en AD-gebruikers detectie zijn geconfigureerd en dat de gebruiker wordt gedetecteerd door beide. Controleer of de gebruiker de juiste machtigingen heeft in Configuration Manager.

**Mogelijke oorzaken:**

Controleer of het account de volgende machtigingen heeft:
- De **Lees** machtiging voor de **verzameling** van het apparaat in Configuration Manager.
- De machtiging **resource lezen** onder **verzameling** in Configuration Manager.
- De machtiging voor het **melden van resources** onder **verzameling** in Configuration Manager.
   - Deze machtiging is nodig om de meest recente gebeurtenissen te kunnen synchroniseren.

### <a name="unable-to-get-timeline-information"></a><a name="bkmk_404"></a> Kan geen tijdlijn gegevens ophalen

**Fout bericht:** De apparaatgegevens zijn nog niet gesynchroniseerd van Configuration Manager naar het micro soft Endpoint Manager-beheer centrum. Wacht tot 15 minuten nadat u de site hebt gekoppeld aan uw Azure-Tenant.

**Mogelijke oplossing:** Wacht ongeveer 15 minuten en het probleem moet automatisch worden opgelost.

### <a name="unexpected-error-occurred"></a><a name="bkmk_500"></a> Er is een onverwachte fout opgetreden

**Fout bericht:** Er is een onverwachte fout opgetreden

**Mogelijke oorzaken:**

- Controleer of er mini maal Configuration Manager versie 2002 met het [Update pakket](https://support.microsoft.com/help/4560496/) en de bijbehorende versie van de console zijn geïnstalleerd.
- Als er sprake is van een groot aantal gebeurtenissen (meer dan 10.000, ongeveer) en er snel meerdere zoek opdrachten worden aangevraagd, is het mogelijk om een onverwachte fout te ontvangen. U ziet mogelijk ook de [time-out voor](#bkmk_timeout)de zoek resultaten.

### <a name="getting-results-timed-out"></a><a name="bkmk_timeout"></a> Time-out tijdens ophalen van resultaten

**Fout bericht:** Time-out tijdens ophalen van resultaten. Zorg ervoor dat het Configuration Manager service-verbindings punt operationeel is en een verbinding heeft met de Cloud.

**Mogelijke oorzaak:** Als er sprake is van een groot aantal gebeurtenissen (meer dan 10.000, ongeveer), en er snel meerdere zoek opdrachten worden aangevraagd, is het mogelijk om een time-out te zien. Mogelijk ziet u ook een [onverwachte fout](#bkmk_500).

## <a name="known-issues"></a>Bekende problemen

### <a name="boundary-group-id-is-used-rather-than-the-name"></a>Grens groep-ID wordt gebruikt in plaats van de naam

**Scenario:** Als u Configuration Manager versie 2002 en de grens groepen van een apparaat wijzigt, ziet u mogelijk het gebeurtenis bericht de grens groep-ID in plaats van de naam.

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Volgende stappen

[Problemen met tenantkoppeling oplossen](troubleshoot.md)
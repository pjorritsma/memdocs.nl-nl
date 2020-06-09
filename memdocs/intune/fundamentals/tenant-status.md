---
title: Tenantstatuspagina in Microsoft Intune
titleSuffix: Microsoft Intune
description: Gebruik de tenantstatuspagina van Intune om belangrijke tenantgegevens te bekijken zonder daarvoor de Intune-portal te hoeven verlaten
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 7954a686-25dc-4fce-b395-324816f46d3b
ms.reviewer: crisk
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4d747a38dd8e2f95cafb25ec5705f83199f4c54
ms.sourcegitcommit: 5dc3545d7f76ce81598f6b1c9734b0ac0a3e9722
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/20/2020
ms.locfileid: "83690687"
---
# <a name="use-the-intune-tenant-status-page"></a>De tenantstatuspagina in Intune gebruiken

De Tenantstatuspagina in Microsoft Intune is een gecentraliseerde hub met de huidige en belangrijke details over uw tenant. Dit zijn onder andere details over de beschikbaarheid en het gebruik van licenties, de status van de connector en belangrijke communicatie over de Intune-service.

> [!TIP]
> Een tenant is een instantie van Azure Active Directory (Azure AD). Uw abonnement op Intune wordt gehost door een Azure AD-tenant. Zie [Een tenant instellen](https://docs.microsoft.com/azure/active-directory/develop/quickstart-create-new-tenant) in de Azure AD-documentatie voor meer informatie.

Als u het dashboard wilt bekijken, meldt u zich aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431), gaat u naar **Tenantbeheer** en selecteert u vervolgens **Tenantstatus**.

De pagina is onderverdeeld in drie tabbladen:

## <a name="tenant-details"></a>Tenantgegevens
Tenantgegevens biedt overzichtelijke informatie over uw tenant. U ziet hier informatie zoals de naam van de tenant, de locatie ervan, uw MDM-instantie en het versienummer van de tenant. Het versienummer van de service is een koppeling waarmee u het artikel *Nieuwe functies in Intune* opent in de Microsoft-documentatie. In *Nieuwe functies* leest u meer over de nieuwste functies en updates voor de Intune-service.  

Dit tabblad biedt ook basisinformatie over welke licenties beschikbaar zijn en hoeveel er zijn toegewezen aan gebruikers. De licenties voor apparaten worden niet weergegeven.

## <a name="connector-status"></a>Connectorstatus
In Connectorstatus kunt u de status van alle connectors bekijken die beschikbaar zijn voor Intune.  

Connectors zijn:
- **Door u geconfigureerde verbindingen met externe services**. Dit kan bijvoorbeeld de *Apple Volume Purchase Program*-service of de *Windows Autopilot*-service zijn.  De status van dit type connector wordt gebaseerd op het tijdstip van de laatste geslaagde synchronisatie.
- **Certificaten of referenties die nodig zijn voor het verbinden met een externe, niet-beheerde service**, zoals *Apple Push Notification Services*-certificaten (APNS). De status van dit type connector wordt gebaseerd op de verlooptijdstempel van het certificaat of de referentie.  

Wanneer u het tabblad *Connectorstatus* opent, worden connectors die niet in orde zijn boven aan de lijst weergegeven. Daarna komen de connectors met waarschuwingen en daarna de connectors die in orde zijn. De connectors die nog niet zijn geconfigureerd, worden als laatste weergegeven, met de status *Niet ingeschakeld*.

Als er meer dan één connector van een bepaald type is, is de status een overzicht van alle connectors van hetzelfde type. De slechtste status van alle connectors in een groep wordt gebruikt als de status van de gehele groep.  

**Connectorstatus:**
- **Niet in orde:**
  - Het certificaat of de referentie is verlopen
  - De laatste synchronisatie is drie of meer dagen geleden
- **Waarschuwing:**
  - Het certificaat of de referentie verloopt binnen zeven dagen
  - De laatste synchronisatie is meer dan een dag geleden
- **In orde:**
  - Het certificaat of de referentie verloopt niet binnen zeven dagen
  - De laatste synchronisatie is minder dan een dag geleden  

Als u een connector uit de lijst selecteert, wordt in de portal de pagina weergegeven die relevant is voor die connector. Op de connectorpagina kunt u de status van eerder geconfigureerde connectors bekijken of opties selecteren om een nieuwe connector van dat type toe te voegen of te maken.

Als u bijvoorbeeld de connector **VVP Expiry Date** selecteert, wordt de pagina **iOS Volume-Purchased Program Tokens** geopend. Hier kunt u meer informatie over de connector bekijken. U kunt ook een nieuwe configuratie maken, een bewerking doorvoeren of problemen met een bestaande configuratie oplossen.

## <a name="service-health-dashboard"></a>Statusdashboard van de service  
Op het Statusdashboard van de service kunt u details weergeven voor *service-incidenten* die van invloed zijn op uw Tenant, en *Intune-nieuws* met informatie over updates en geplande wijzigingen.

### <a name="intune-service-health-and-message-center"></a>Servicestatus en berichtencentrum van Intune
U kunt gegevens over actieve incidenten en advies bekijken zonder dat u naar het Microsoft 365 Service Health-dashboard of het berichtencentrum hoeft te gaan. Beide zijn in het [Microsoft 365-beheercentrum](https://admin.microsoft.com) te vinden. Alleen incidenten die van invloed zijn op uw tenant worden weergegeven.  

Wanneer u een incident selecteert, worden de incidentgegevens rechtstreeks op de tenantstatuspagina weergegeven. Als u advies en incidenten uit het verleden wilt bekijken, selecteert u **Incidenten/advies uit het verleden bekijken**. Het Microsoft 365-beheercentrum wordt geopend. U kunt dan voor uw tenant advies en incidenten uit de afgelopen 30 dagen bekijken.  

Als u informatie over *Intune Service Health* wilt bekijken, moet uw account beschikken over de rol **Globale beheerder** of **Serviceondersteuningsbeheerder** in Azure Active Directory of het Microsoft 365-beheercentrum. Als u deze machtigingen wilt toewijzen, meldt u zich aan bij het [Microsoft 365-beheercentrum](https://admin.microsoft.com) met globale-beheerdersmachtigingen. Selecteer **Gebruikers > Actieve gebruikers** en selecteer vervolgens het account waarvoor toegang is vereist. Selecteer **Bewerken** voor rollen, selecteer *Serviceondersteuningsbeheerder* of *Globale beheerder* en selecteer vervolgens **Opslaan** voor uw bewerking om de machtigingen toe te wijzen.  

U kunt uw communicatievoorkeuren voor Intune Service Health alleen instellen via het Microsoft 365-beheercentrum.

### <a name="intune-message-center"></a>Intune-berichtencentrum  
U kunt informatieve communicatie van het Intune-serviceteam bekijken zonder naar het Office-berichtencentrum te gaan. De communicatie omvat berichten over wijzigingen die recent zijn aangebracht aan de Intune-service en wijzigingen die binnenkort worden doorgevoerd voor uw tenant.  

Standaard worden de tien meest recente en actieve berichten weergegeven. Als u oudere berichten wilt weergeven, klikt u op **Oudere berichten weergeven** om het *berichtencentrum* te openen in het Microsoft 365-beheercentrum.  

Als u informatie over Intune-nieuws wilt bekijken, moet uw account beschikken over de rol **Globale beheerder** of **Serviceondersteuningsbeheerder** in Azure Active Directory, of de rol **Berichtencentrum-lezer** in het Microsoft 365-beheercentrum.  Als u deze machtiging wilt toewijzen, meldt u zich aan bij het [Microsoft 365-beheercentrum](https://admin.microsoft.com) met beheerdersmachtigingen. Selecteer **Gebruikers > Actieve gebruikers** en selecteer vervolgens het account waarvoor toegang is vereist. Selecteer **Bewerken** voor *Rollen*, selecteer *Teams-communicatiebeheerder* en **sla vervolgens uw bewerking op** om de machtigingen toe te wijzen.  

U kunt uw communicatievoorkeuren voor het Intune-berichtencentrum alleen instellen via het Microsoft 365-beheercentrum.

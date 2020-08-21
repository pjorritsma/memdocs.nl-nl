---
title: Tenant koppeling-toepassingen (preview) in het beheer centrum
titleSuffix: Configuration Manager
description: Toepassingen voor het uploaden van Configuration Manager-apparaten installeren vanuit het beheer centrum.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 963dda08-87b8-4e80-90a7-25625efe8861
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 4c535cc41e1351b334e8eb7bb942de04ebbd00a2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700433"
---
# <a name="tenant-attach-install-an-application-from-the-admin-center-preview"></a><a name="bkmk_apps"></a> Tenant bijvoegen: een toepassing installeren vanuit het beheer centrum (preview-versie)
<!--cm 6024389, in 7220536 pubpreview Aug 10, 2020-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]
> - Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

Micro soft Endpoint Manager is een geïntegreerde oplossing voor het beheer van al uw apparaten. Micro soft brengt Configuration Manager en intune samen in één console met de naam **micro soft Endpoint Manager-beheer centrum**. Vanuit het micro soft endpoint management-beheer centrum kunt u een installatie van een toepassing in realtime initiëren voor een apparaat dat aan een Tenant is gekoppeld.

   :::image type="content" source="media/6024389-tenant-attach-application-list.png" alt-text="Toepassingen in het beheer centrum van micro soft Endpoint Manager" lightbox="media/6024389-tenant-attach-application-list.png":::

## <a name="prerequisites"></a>Vereisten

- Alle vereisten voor [Tenant koppeling: client Details ConfigMgr](client-details.md#prerequisites).
- [Update pakket voor micro soft Endpoint Configuration Manager versie 2002](https://support.microsoft.com/help/4560496/) en de bijbehorende versie van de geïnstalleerde console
- De optionele functie **voor het goed keuren van toepassings aanvragen voor gebruikers per apparaat**inschakelen. Zie voor meer informatie [Enable optional features from updates](../core/servers/manage/install-in-console-updates.md#bkmk_options).
- Ten minste één toepassing die is geïmplementeerd op een verzameling apparaten met de **beheerder moet een aanvraag voor deze toepassing goed keuren op de apparaat** -optie die is ingesteld op de implementatie. Zie [toepassingen goed keuren](../apps/deploy-use/app-approval.md#bkmk_opt)voor meer informatie.
   - Gebruikers gerichte toepassingen of toepassingen zonder de optie set goed keuring worden niet weer gegeven in de lijst met toepassingen wanneer u Configuration Manager versie 2002.

Daarnaast hebt u het volgende nodig voor het installeren van [gebruikers gerichte toepassingen](#bkmk_user):<!--7518897-->

- Configuration Manager versie 2006 en de bijbehorende versie van de console zijn geïnstalleerd.


## <a name="permissions"></a>Machtigingen

Het gebruikers account heeft de volgende machtigingen nodig:

- De **Lees** machtiging voor de **verzameling** van het apparaat in Configuration Manager.
- De **Lees** machtiging voor de **toepassing** in Configuration Manager.
- De machtiging **goed keuren** voor de **toepassing** in Configuration Manager.
- De gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD. 
  - Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt.
   > [!TIP]
   > De [rol toepassings beheerder in azure AD](/azure/active-directory/users-groups-roles/directory-assign-admin-roles) beschikt over voldoende machtigingen om een gebruiker toe te voegen aan de gebruikersrol **admin** van de toepassing.

## <a name="deploy-an-application-to-a-device"></a><a name="bkmk_deploy"></a> Een toepassing implementeren op een apparaat

1. Ga in een browser naar [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Selecteer **apparaten** en vervolgens **alle apparaten**.
1. Selecteer een apparaat dat is gesynchroniseerd vanuit Configuration Manager via [Tenant attach](device-sync-actions.md).
1. Selecteer **toepassingen**.
1. Selecteer de toepassing en klik op **installeren**.

   :::image type="content" source="media/6024389-tenant-attach-application-install.png" alt-text="Installatie van de toepassing vanuit het micro soft Endpoint Manager-beheer centrum" lightbox="media/6024389-tenant-attach-application-install.png":::

U kunt alle gegevens die momenteel in de weer gave zijn, naar een. CSV-bestand exporteren. Selecteer boven aan de pagina de optie **exporteren** om het bestand te maken. Als de weer gave groter is dan 500 rijen, worden alleen de eerste 500 geëxporteerd.

## <a name="application-status"></a>Toepassings status

U kunt de lijst met toepassingen filteren op basis van de status. De toepassings status kan een van de volgende zijn:

- **Beschikbaar**: de toepassing is nooit op het apparaat geïnstalleerd.
- **Geïnstalleerd**: de toepassing is geïnstalleerd op het apparaat.
- **Installeren**: de toepassing wordt momenteel geïnstalleerd.
- **Installatie aangevraagd**: de installatie is aangevraagd, maar de client heeft de aanvraag nog niet bevestigd.
   - Als het apparaat offline is, wordt de installatie aanvraag bevestigd zodra deze weer online is en het beleid ontvangt.  
- **Mislukt**: de installatie van de toepassing is mislukt.
- **Niet voldaan aan vereisten**: er is niet voldaan aan de vereisten van de toepassing.
- **Niet geïnstalleerd**: de toepassing is momenteel niet geïnstalleerd. Deze status wordt doorgaans gezien als een andere implementatie of een gebruiker de toepassing heeft verwijderd.
- **Opnieuw opstarten in behandeling**: de toepassing is geïnstalleerd, maar moet opnieuw worden opgestart om te volt ooien (vanaf versie 2006).

## <a name="deploy-an-application-to-a-user"></a><a name="bkmk_user"></a> Een toepassing implementeren voor een gebruiker
<!--7518897-->
Vanaf Configuration Manager versie 2006 worden toepassingen die beschikbaar zijn, weer gegeven in het knoop punt **toepassingen** voor een ConfigMgr-apparaat. De lijst met toepassingen die beschikbaar zijn voor het apparaat omvat ook toepassingen die zijn geïmplementeerd op de momenteel aangemelde gebruiker van het apparaat.

Voor het implementeren van toepassingen voor een gebruiker gelden de volgende beperkingen:
- Scenario's voor sessie met meerdere gebruikers worden niet ondersteund.
- Apparaten die zijn toegevoegd aan Azure AD, worden momenteel niet ondersteund.
   - Apparaten die deel uitmaken van een domein en Azure AD zijn toegevoegd, worden ondersteund.

## <a name="next-steps"></a>Volgende stappen

[Problemen met toepassingen oplossen](troubleshoot-applications.md)
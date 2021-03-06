---
title: 'Tenant koppelen: ConfigMgr-client Details (preview) in het beheer centrum'
titleSuffix: Configuration Manager
description: Details van de client voor Configuration Manager apparaten weer geven vanuit het beheer centrum.
ms.date: 09/09/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: fbe75e34465335450f3a09680b68a78520451bd1
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643391"
---
# <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview"></a><a name="bkmk_mem"></a> Tenant bijvoegen: client Details ConfigMgr in het beheer centrum (preview-versie)
<!--6024387, 6374854, 6521921, intune 7552762 pubpreview July 7, 2020-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Micro soft Endpoint Manager is een geïntegreerde oplossing voor het beheer van al uw apparaten. Micro soft brengt Configuration Manager en intune samen in één console met de naam **micro soft Endpoint Manager-beheer centrum**. U kunt ConfigMgr-client gegevens weer geven, inclusief verzamelingen, lidmaatschap van grens groepen en real-time client informatie voor een specifiek apparaat in het beheer centrum.

> [!Important]
> - Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.
> - Het tabblad grens groepen werkt alleen voor zelfstandige sites. Het tabblad is leeg in het beheer centrum voor alle andere dan een zelfstandige primaire site.

## <a name="prerequisites"></a>Vereisten

- Een omgeving waaraan een [Tenant is gekoppeld met geüploade apparaten](device-sync-actions.md).
- Een van de volgende browsers:
  - Micro soft Edge, versie 77 en hoger
  - Google Chrome
- Het gebruikers account voor het koppelen van functies voor Tenant koppeling in het **micro soft Endpoint Manager-beheer centrum** moet zijn gedetecteerd met [Azure Active Directory (Azure AD) gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) en [Active Directory gebruikers detectie](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
  - Dit betekent dat het gebruikers account een gesynchroniseerd gebruikers object moet zijn in Azure.

## <a name="permissions"></a>Machtigingen

De gebruikers account voor het koppelen van functies voor Tenant koppeling in het micro soft Endpoint Manager-beheer centrum heeft de volgende machtigingen nodig:

- De **Lees** machtiging voor de **verzameling** van het apparaat in Configuration Manager.
- De gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD.
  - Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt.
   > [!TIP]
   > De [rol toepassings beheerder in azure AD](/azure/active-directory/users-groups-roles/directory-assign-admin-roles) beschikt over voldoende machtigingen om een gebruiker toe te voegen aan de gebruikersrol **admin** van de toepassing.

## <a name="view-configmgr-client-details"></a>Details van ConfigMgr-client weer geven

1. Ga in een browser naar [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Selecteer **apparaten** en vervolgens **alle apparaten**.
1. Selecteer een apparaat dat is gesynchroniseerd vanuit Configuration Manager via [Tenant attach](device-sync-actions.md).
1. Selecteer de **client Details (preview-versie)**.
   - De primaire site werkt de volgende velden eenmaal per uur bij:
      - **Laatste beleids aanvraag**
      - **Laatste actieve tijd**
      - **Laatste beheer punt**.

   :::image type="content" source="media/6024387-device-details.png" alt-text="Client Details in het micro soft Endpoint Manager-beheer centrum" lightbox="media/6024387-device-details.png":::

1. Selecteer de **verzamelingen (preview)** om de verzamelingen van de client weer te geven. <!--6024390-->

   :::image type="content" source="media/6024387-device-collections.png" alt-text="Client verzamelingen in het micro soft Endpoint Manager-beheer centrum" lightbox="media/6024387-device-collections.png":::

## <a name="next-steps"></a>Volgende stappen

[Problemen met client Details oplossen](troubleshoot-client-details.md)

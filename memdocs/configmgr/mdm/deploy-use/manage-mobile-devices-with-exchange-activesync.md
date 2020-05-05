---
title: Apparaatbeheer met Exchange
titleSuffix: Configuration Manager
description: Mobiele apparaten beheren met de Exchange Server-connector in Configuration Manager.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721925"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>Apparaatbeheer met Exchange en Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u mobiele apparaten hebt die u via het ActiveSync-protocol met Exchange Server maakt, kunt u de Exchange Server-connector in Configuration Manager gebruiken om deze apparaten te beheren. De connector werkt met on-premises Exchange Server of Exchange Online. Gebruik de Configuration Manager-console om Exchange Mobile Device Management-functies te configureren. Bijvoorbeeld, besturings element voor het wissen van externe apparaten en instellingen voor meerdere Exchange-servers.

![Logisch diagram van Exchange Server-connector met Configuration Manager](media/configmgr-with-exchange.png)  

Wanneer u mobiele apparaten beheert met deze connector, wordt de Configuration Manager-client niet geïnstalleerd of worden de apparaten Inge schreven via MDM. De beheer functies van Exchange Server zijn beperkt in vergelijking met deze andere opties. U kunt bijvoorbeeld geen software installeren of configuratie-items gebruiken om deze apparaten te configureren. Zie [een oplossing voor het beheer van apparaten kiezen voor Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)voor meer informatie.  

## <a name="policies"></a>Beleidsregels

Wanneer u de-connector gebruikt, configureert Configuration Manager instellingen op de mobiele apparaten. De apparaten gebruiken niet het standaard beleid voor Exchange ActiveSync-post vakken. Definieer de instellingen die u wilt gebruiken in de volgende groepen:

- **Algemeen**
- **Wachtwoord**
- **E-mail beheer**
- **Beveiliging**
- **Toepassing**

U kunt bijvoorbeeld in de groep **wacht woord** de volgende instellingen configureren:

- Of mobiele apparaten een wacht woord vereisen
- De minimale wachtwoord lengte
- Wachtwoordcomplexiteit
- Of wachtwoord herstel is toegestaan

Wanneer u ten minste één instelling in de groep configureert, beheert Configuration Manager alle instellingen in de groep voor mobiele apparaten. Als u geen instellingen in een groep configureert, blijft Exchange die instellingen voor de mobiele apparaten beheren. Elk Exchange ActiveSync-postvak beleid dat u op de Exchange-server configureert en aan gebruikers toewijst, wordt nog steeds toegepast.

## <a name="access-rules-and-remote-actions"></a>Toegangs regels en externe acties

U kunt de Exchange Server-connector ook configureren om de toegangs regels voor Exchange te beheren. Deze toegangs regels omvatten het toestaan, blok keren of in quarantaine plaatsen van mobiele apparaten. U kunt mobiele apparaten op afstand wissen met behulp van de Configuration Manager-console. gebruikers kunnen hun mobiele apparaten op afstand wissen met behulp van de Application Catalog.

Het mobiele apparaat van een gebruiker wordt automatisch in de toepassings catalogus weer gegeven wanneer u het beheert en de Exchange-Server is on-premises. Als u wilt dat het mobiele apparaat wordt weer gegeven in de toepassings catalogus wanneer u Exchange Online gebruikt, moet u de gebruikers affiniteit van het apparaat hand matig configureren. Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie.

> [!TIP]  
> Wanneer een mobiel apparaat wordt overgedragen aan een andere gebruiker, verwijdert u het mobiele apparaat uit de Configuration Manager-console voordat de nieuwe eigenaar zijn of haar Exchange-account configureert op het apparaat.

## <a name="prerequisites"></a>Vereisten

> [!IMPORTANT]  
> Controleer voordat u deze connector installeert of Configuration Manager uw versie van Exchange ondersteunt. Zie [ondersteunde configuraties-Exchange Server-connector](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS)voor meer informatie.  

### <a name="permissions-to-configure-the-connector"></a>Machtigingen voor het configureren van de connector

U hebt de volgende beveiligings machtigingen nodig om de Exchange Server-connector te configureren in Configuration Manager:

- Als u de Exchange Server-connector wilt toevoegen, wijzigen of verwijderen: machtiging **Wijzigen** voor het object **Site** .  

- Als u de instellingen voor mobiele apparaten wilt configureren: machtiging **ModifyConnectorPolicy** voor het object **Site** .  

De ingebouwde rol **volledige beheerder** bevat bijvoorbeeld deze vereiste machtigingen.  

### <a name="permissions-to-manage-mobile-devices"></a>Machtigingen voor het beheren van mobiele apparaten

U hebt de volgende beveiligings machtigingen nodig voor het beheren van mobiele apparaten:  

- Als u een mobiel apparaat wilt wissen: **Resource verwijderen** voor het object **Verzameling** .  

- Als u een wisopdracht wilt annuleren: **Resource wijzigen** voor het object **Verzameling** .  

- Mobiele apparaat toestaan en blokkeren: **resource wijzigen** voor het **verzamelings**object.  

De ingebouwde rol van **Operations-beheerder** bevat bijvoorbeeld deze vereiste machtigingen.

Zie [op rollen gebaseerd beheer configureren](../../core/servers/deploy/configure/configure-role-based-administration.md)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [De Exchange-connector installeren en configureren](install-configure-exchange-connector.md)

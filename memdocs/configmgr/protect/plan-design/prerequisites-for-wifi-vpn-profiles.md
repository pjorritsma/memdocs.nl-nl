---
title: Vereisten voor Wi-Fi- en VPN-profielen
titleSuffix: Configuration Manager
description: Meer informatie over de vereisten voor het beheren van Wi-Fi-profielen en VPN-profielen in Configuration Manager
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722128"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Vereisten voor Wi-Fi-en VPN-profielen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wi-Fi-en VPN-profielen in Configuration Manager hebben alleen afhankelijkheden binnen het product.

U hebt de volgende beveiligings machtigingen nodig voor het beheren van toegangs instellingen voor bedrijfs bronnen, zoals certificaat profielen, Wi-Fi-profielen en VPN-profielen:  

- Waarschuwingen en rapporten voor Wi-Fi en profielen weer geven en beheren: **maken**, **verwijderen**, **wijzigen**, **rapport wijzigen**, **lezen**en **rapport uitvoeren** voor het object **waarschuwingen** .  

- Certificaatprofielen maken en beheren: **Auteursbeleid**, **Rapport wijzigen**, **Lezen** en **Rapport uitvoeren** voor het object **Certificaatprofiel**.  

- Wi-Fi-, certificaat- en VPN-profielimplementaties beheren: **Configuratiebeleid toepassen**, **Waarschuwing voor wijzigen clientstatus**, **Lezen** en **Resource lezen** voor het object **Verzameling**.  

- Alle configuratiebeleidsregels beheren: **Maken**, **Verwijderen**, **Wijzigen**, **Lezen** en **Beveiligingsbereik instellen** voor het object **Configuratiebeleid**.  

- Query's uitvoeren die gerelateerd zijn aan Wi-Fi-en VPN-profielen: machtiging voor **lezen** voor het object **query** .  

- Wi-Fi-en VPN-profiel gegevens weer geven in de Configuration Manager-console: machtiging voor **lezen** voor het object **site** .  

- Status berichten weer geven voor Wi-Fi-en VPN-profielen: machtiging voor **lezen** voor het object **status berichten** .  

- Profiel voor vertrouwd CA-certificaat maken en beheren: **Auteursbeleid**, **Rapport wijzigen**, **Lezen** en **Rapport uitvoeren** voor het object **Profiel voor vertrouwd CA-certificaat**.  

- VPN-profielen maken en beheren: **Auteursbeleid**, **Rapport wijzigen**, **Lezen** en **Rapport uitvoeren** voor het object **VPN-profiel**.  

- Wi-Fi-profielen maken en beheren: **Auteursbeleid**, **Rapport wijzigen**, **Lezen** en **Rapport uitvoeren** voor het object **Wi-Fi-profiel**.  

De ingebouwde beveiligingsrol **bedrijfs resource Access Manager** bevat de machtigingen die nodig zijn voor het beheren van Wi-Fi-profielen in Configuration Manager. Zie [Configure Security](../../core/plan-design/security/configure-security.md)(Engelstalig) voor meer informatie.

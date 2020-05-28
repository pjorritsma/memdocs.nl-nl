---
title: Mogelijkheden van Technical Preview 1607
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1607.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 73aac9e1bfb7b902a7db28ba4be00a2a02277324
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905685"
---
# <a name="capabilities-in-technical-preview-1607-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1607 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1607. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site.      Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a><a name="dmp_edition"></a>Verbeteringen in het upgradebeleid van de Windows 10-editie

In deze release zijn de volgende verbeteringen aangebracht in dit beleid:

* U kunt nu het beleid voor editie-upgrades gebruiken met Windows 10-Pc's waarop de Configuration Manager-client wordt uitgevoerd, naast de Windows 10-computers die zijn Inge schreven bij Microsoft Intune.
* U kunt een upgrade uitvoeren van Windows 10 Professional naar een van de platformen in de wizard die compatibel zijn met uw hardware.

[Meer informatie over het beleid voor editie-upgrades voor Windows 10](../../compliance/deploy-use/upgrade-windows-version.md)

### <a name="try-it-out"></a>Probeer het nu!

1. Gebruik de informatie in het [onderwerp over het huidige beleid voor editie-upgrades](../../compliance/deploy-use/upgrade-windows-version.md) om een beleid voor editie-upgrades te maken.
2. Implementeer dit beleid op een Windows 10-PC waarop de Configuration Manager-client wordt uitgevoerd.
Als het beleid een bepaalde Windows-computer bereikt, wordt de computer binnen twee uur opnieuw opgestart om de upgrade toe te passen. U kunt deze opnieuw opstarten momenteel niet onderdrukken. Zorg ervoor dat u alle gebruikers op de hoogte stelt waarvoor u het beleid implementeert of plan het beleid om buiten de werk uren van de gebruiker te worden uitgevoerd.

### <a name="known-issue-with-this-release"></a>Bekend probleem met deze release
In Configuration Manager-client instellingen ziet u mogelijk instellingen voor **editie-upgrade**. In deze release zijn deze instellingen niet functioneel. Volg de bovenstaande instructies om Windows 10 bij te werken naar een nieuwere versie.

## <a name="customizable-branding-for-software-center-dialogs"></a>Aanpasbare huisstijl voor Software Center-dialoogvensters

Aangepaste huis stijl voor het Software Center werd geïntroduceerd in Configuration Manager versie 1602. In Technical Preview versie 1607 is die branding nu uitgebreid naar alle bijbehorende dialoog vensters en taak balk meldingen om gebruikers van het Software Center een consistenter ervaring te bieden.

### <a name="try-it-out"></a>Probeer het nu!

Aangepaste huis stijl voor het Software Center wordt toegepast volgens de volgende regels:

1. Als de site serverrol toepassingscatalogus website punt niet is geïnstalleerd, wordt in Software Center de naam van de organisatie weer gegeven die is opgegeven in de **computer agent** -client instelling **organisatie naam weer gegeven in Software Center**. Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor instructies.

2. Als de site serverrol toepassingscatalogus website punt is geïnstalleerd, worden in Software Center de naam en kleur van de organisatie weer gegeven die zijn opgegeven in de eigenschappen van de site server functie toepassingscatalogus website punt. Zie [configuratie opties voor toepassingscatalogus website punt](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)voor meer informatie.

3. Als een Microsoft Intune-abonnement is geconfigureerd en verbonden met de Configuration Manager omgeving, worden in Software Center de naam van de organisatie, de kleur en het bedrijfs logo weer gegeven die zijn opgegeven in de eigenschappen van het intune-abonnement.

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Dezelfde netwerk adapter gebruiken voor meerdere door PXE geïnitieerde implementaties
In Technical Preview versie 1607, wanneer u een Ethernet-adapter gebruikt om meerdere apparaten te installeren (zoals een USB-Ethernet adapter die u op meerdere apparaten gebruikt), kunt u een nieuwe instelling inschakelen waarmee u hardware-id's voor de Ethernet-adapters opgeeft. Configuration Manager negeert de hardware-id's in de lijst tijdens het uitvoeren van een PXE-installatie en voor registratie van de client.

Voor meer informatie over dit probleem raadpleegt u de blog van het [Configuration Manager OSD-ondersteunings team](https://techcommunity.microsoft.com/t5/configuration-manager-archive/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in/ba-p/273721).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>De functie inschakelen voor het beheren van dubbele hardware-id's  
1. Ga in de Configuration Manager-console naar **beheer**  >  **overzicht**  >  **Cloud Services**  >  **updates en onderhouds**  >  **functies**.
2. Selecteer in het weergave paneel **dubbele hardware-Id's beheren**.
3. Klik op het tabblad **Start** in de groep **functies** op **inschakelen**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Hardware-id's voor Configuration Manager voor negeren toevoegen  
1. Ga in de Configuration Manager-console naar **beheer**  >  **overzicht**  >  **site configuratie**  >  **sites**.
2. Klik op **Hiërarchie-instellingen** op het tabblad **Start** , in de groep **Sites**.
3. Ga naar het tabblad **goed keuring van client en conflicterende records** .
4. Klik op **toevoegen** in de sectie **dubbele hardware-id's** om nieuwe hardware-id's toe te voegen.

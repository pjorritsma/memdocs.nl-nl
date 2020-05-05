---
title: Grenzen definiëren
titleSuffix: Configuration Manager
description: Meer informatie over het definiëren van netwerk locaties op uw intranet die apparaten kunnen bevatten die u wilt beheren.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f53088843e0bf42a93c1d959255c7885b07dfe35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721113"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Netwerk locaties definiëren als grenzen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager grenzen zijn locaties in uw netwerk die apparaten bevatten die u wilt beheren. De grens van een apparaat is gelijk aan de Active Directory-site of het netwerk-IP-adres dat wordt geïdentificeerd door de Configuration Manager-client die op het apparaat is geïnstalleerd.
- U kunt handmatig afzonderlijke grenzen maken. Configuration Manager biedt echter geen ondersteuning voor de rechtstreekse invoer van een supernet als grens. Gebruik in plaats daarvan het grenstype IP-adresbereik.
- U kunt de [Active Directory forest-detectie](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) methode configureren om automatisch te detecteren en grenzen te maken voor elk IP-Subnet en Active Directory site die wordt gedetecteerd. Wanneer Active Directory forest-detectie een supernet identificeert dat is toegewezen aan een Active Directory-site, Configuration Manager converteert de supernet naar een IP-adres bereik grens.  

Het is niet ongebruikelijk dat een apparaat een IP-adres gebruikt waarvan de Configuration Manager beheerder niet op de hoogte is. Wanneer de netwerk locatie van een apparaat onzeker is, controleert u wat het apparaat rapporteert als locatie met behulp van de opdracht **ipconfig** op het apparaat.  

Wanneer u een grens maakt, krijgt deze automatisch een naam die is gebaseerd op het type en bereik van de grens. U kunt deze naam niet wijzigen. In plaats daarvan kunt u een beschrijving opgeven om de grens te identificeren in de Configuration Manager-console.  

Elke grens is beschikbaar voor gebruik door elke site in uw hiërarchie. Nadat u een grens hebt gemaakt, kunt u de eigenschappen wijzigen om het volgende te doen:  
- De grens toevoegen aan een of meer grensgroepen.  
- Het type of bereik van de grens wijzigen.  
- Ga naar het tabblad **Sitesystemen** voor de grenzen om te zien welke sitesysteemservers (distributiepunten, statusmigratiepunten en beheerpunten) aan de grens zijn gekoppeld.  

## <a name="to-create-a-boundary"></a>Een grens maken  

1.  Klik in de Configuration Manager-console op **beheer** > **hiërarchie configuratie** > **grenzen**  

2.  Klik op het tabblad **Start** in de groep **Maken** op **Maken Boundary**.  

3.  Op het tabblad **Algemeen** van het dialoogvenster Grens maken kunt u bij **Beschrijving** een beschrijving opgeven om de grens aan te duiden met een beschrijvende naam of verwijzing.  

4.  Selecteer een **type** voor deze grens:  

    - Als u **IP-subnet**selecteert, moet u bij **Subnet-id** een subnet-id voor deze grens opgeven.  
      > [!TIP]  
      > Als u het **netwerk** en **subnetmasker** opgeeft, wordt de **subnet-id** automatisch opgegeven. Wanneer u de grens opslaat, wordt alleen de subnet-id opgeslagen.  

    - Als u **Active Directory-site**selecteert, moet u een Active Directory-site in het lokale forest van de siteserver opgeven of **Bladeren** selecteren.  
        
      - Wanneer u een Active Directory-site voor een grens opgeeft, bevat de grens alle IP-subnetten die lid zijn van die Active Directory-site. Als de configuratie van de Active Directory-site wordt gewijzigd in Active Directory, worden de netwerklocaties die zijn opgenomen in deze grens ook gewijzigd.  

      - Active Directory site grenzen werken niet voor zuivere AzureAD-clients. Als ze on-premises zwerven, vallen ze niet onder een grens als ze alleen worden gedefinieerd met behulp van AD-sites.

    - Als u **IPv6-voorvoegsel**selecteert, moet u een **voorvoegsel** in de IPv6-voorvoegselindeling opgeven.  

    - Als u **IP-adresbereik**selecteert, moet u een **IP-beginadres** en **IP-eindadres** opgeven die een deel van een IP-subnet of meerdere IP-subnetten bevatten.    

5.  Klik op **OK** om de nieuwe grens op te slaan.  

## <a name="to-configure-a-boundary"></a>Een grens configureren  

1.  Klik in de Configuration Manager-console op **beheer** > **hiërarchie configuratie** > **grenzen**  

2.  Selecteer de grens die u wilt wijzigen.  

3.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

4.  Selecteer in het dialoogvenster **Eigenschappen** voor de grens het tabblad **Algemeen** om de **beschrijving** of het **type** voor de grens te bewerken. U kunt ook het bereik van een grens wijzigen door de netwerklocaties voor de grens te bewerken. Voor een grens van het type Active Directory-site kunt u bijvoorbeeld een nieuwe naam opgeven.  

5.  Selecteer het tabblad **Sitesystemen** om de sitesystemen weer te geven die zijn gekoppeld aan deze grens. U kunt deze configuratie niet wijzigen vanuit de eigenschappen van een grens.  

    > [!TIP]  
    > Een sitesysteemserver wordt als een sitesysteem voor een grens weergegeven als de sitesysteemserver is gekoppeld aan een sitesysteemserver voor minstens één grensgroep waarin deze grens is opgenomen. Deze wordt geconfigureerd op het tabblad **Verwijzingen** van een grensgroep.  

6.  Selecteer het tabblad **Grensgroepen** om het lidmaatschap van grensgroepen voor deze grens te wijzigen:  

    - Als u deze grens aan een of meer grensgroepen wilt toevoegen, klikt u op **Toevoegen**, schakelt u het selectievakje voor een of meer grensgroepen in en klikt u op **OK**.  

    - Als u deze grens uit een grensgroep wilt verwijderen, selecteert u de grensgroep en klikt u op **Verwijderen**.  

7.  Klik op **OK** om de grenseigenschappen te sluiten en de configuratie op te slaan.  

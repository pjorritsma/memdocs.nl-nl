---
title: Grenzen definiëren
titleSuffix: Configuration Manager
description: Meer informatie over het definiëren van netwerk locaties op uw intranet die apparaten kunnen bevatten die u wilt beheren.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13312c20edbda290daaa0d51908adeb7ab4a6860
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700058"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Netwerk locaties definiëren als grenzen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager grenzen zijn locaties in uw netwerk die apparaten bevatten die u wilt beheren. U kunt verschillende typen grenzen maken, bijvoorbeeld een Active Directory site of netwerk-IP-adres. Wanneer de Configuration Manager-client een vergelijk bare netwerk locatie identificeert, maakt dat apparaat deel uit van de grens.

Configuration Manager ondersteunt de volgende grens typen:

- IP-subnet
- Active Directory-site
- IPv6-voor voegsel
- IP-adresbereik
- VPN (vanaf versie 2006)

U kunt hand matig afzonderlijke grenzen maken of [Active Directory forest-detectie](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)gebruiken. Deze detectie methode zoekt en maakt automatisch grenzen voor IP-subnetten en Active Directory-sites. Wanneer Active Directory forest-detectie een supernet identificeert voor een Active Directory site, Configuration Manager zet de supernet om in een IP-adres bereik grens.

Als een apparaat zich niet in de door u verwachte grens bevindt, kan het zijn dat u de netwerk locatie niet hebt gedefinieerd als een grens. Wanneer de netwerk locatie van een apparaat onzeker is, gebruikt u de volgende Windows-opdrachten op het apparaat om te bevestigen:

- IP-adres: `ipconfig`
- Active Directory-site: `nltest /dsgetsite`
- VPN `ipconfig /all`

## <a name="boundary-types"></a>Grens typen

### <a name="ip-subnet"></a>IP-subnet

Voor het grens type van het IP-subnet is een **subnet-id**vereist. Bijvoorbeeld `169.254.0.0`. Als u het **netwerk** (standaard gateway) en **subnetmask** waarden opgeeft, wordt Configuration Manager de **subnet-id**automatisch berekend. Wanneer u de grens opslaat, slaat Configuration Manager alleen de subnet-ID op.

> [!NOTE]
> Configuration Manager biedt geen ondersteuning voor de directe invoer van een supernet als grens. Gebruik in plaats daarvan het grenstype IP-adresbereik.

### <a name="active-directory-site"></a>Active Directory-site

Voor het **site** grens type Active Directory, geeft u de naam van de site op. U kunt de naam typen of door het lokale forest van de site server bladeren.

Wanneer u een Active Directory site voor een grens opgeeft, bevat de grens alle IP-subnetten die lid zijn van die Active Directory site. Als de configuratie van de Active Directory-site wordt gewijzigd in Active Directory, worden de netwerklocaties die zijn opgenomen in deze grens ook gewijzigd.  

Active Directory site grenzen werken niet voor zuivere Azure Active Directory-apparaten (Azure AD), ook wel apparaten die lid zijn van het Cloud domein. Als ze on-premises zwerven en u alleen Active Directory site type grenzen maakt, bevinden deze apparaten zich niet in een grens.

> [!TIP]
> Gebruik de volgende Windows-opdracht om de huidige Active Directory-site van een apparaat weer te geven: `nltest /dsgetsite` .
>
> Gebruik de volgende Windows-opdracht om te bepalen of een client lid is van een Cloud domein: `dsregcmd /status` . Zie [dsregcmd Command-Apparaatstatus](/azure/active-directory/devices/troubleshoot-device-dsregcmd)voor meer informatie.

### <a name="ipv6-prefix"></a>IPv6-voor voegsel

Voor het grens type van het **IPv6-voor voegsel** geeft u een **voor voegsel**op. Bijvoorbeeld `2001:1111:2222:3333`.

### <a name="ip-address-range"></a>IP-adresbereik

Geef voor het grens type **IP-adres bereik** het **begin-IP-adres** en het **laatste IP-adres** voor het bereik op. Het bereik kan een deel van een IP-subnet of meerdere IP-subnetten bevatten. Gebruik een grens type voor IP-adres bereik om een supernet te ondersteunen.

U kunt dit type ook gebruiken om een grens te definiëren voor één IP-adres. Stel zowel het eerste als laatste IP-adres in als dezelfde waarde. Deze configuratie kan handig zijn voor unieke apparaten of test omgevingen.

### <a name="vpn"></a>VPN

<!--7020519-->

Vanaf versie 2006 kunt u het beheer van externe clients vereenvoudigen door een grens type voor Vpn's te maken. Wanneer een client een locatie aanvraag verstuurt, bevat deze aanvullende informatie over de netwerk configuratie. Op basis van deze informatie bepaalt de server of de client zich op een VPN bevindt. Verbind het apparaat met de VPN-verbinding om Configuration Manager de client aan de grens te koppelen.

U kunt op verschillende manieren een VPN-grens configureren:

- **Automatische detectie VPN**: Configuration Manager detecteert alle VPN-oplossingen die gebruikmaken van het Point-to-Point Tunneling Protocol (PPTP). Als uw VPN niet wordt gedetecteerd, gebruikt u een van de andere opties. De grens waarde in de console lijst is `Auto:On` .

- **Verbindings naam**: Geef de naam op van de VPN-verbinding op het apparaat. Het is de naam van de netwerk adapter in Windows voor de VPN-verbinding. Configuration Manager komt overeen met de eerste 250 tekens van de teken reeks, maar ondersteunt geen joker tekens of gedeeltelijke teken reeksen. De grens waarde in de lijst met-consoles is `Name:<name>` , waarbij `<name>` de naam van de verbinding die u opgeeft.

  U kunt bijvoorbeeld de opdracht uitvoeren `ipconfig` op het apparaat en een van de secties begint met: `PPP adapter ContosoVPN:` . Gebruik de teken reeks `ContosoVPN` als de naam van de **verbinding**. De lijst wordt weer gegeven als `Name:CONTOSOVPN` .

- **Verbindings beschrijving**: Geef de beschrijving van de VPN-verbinding op. Configuration Manager komt overeen met de eerste 243 tekens van de teken reeks, maar ondersteunt geen joker tekens of gedeeltelijke teken reeksen. De grens waarde in de lijst met-consoles is `Description:<description>` `<description>` de verbindings beschrijving die u opgeeft.

  U kunt bijvoorbeeld de opdracht uitvoeren `ipconfig /all` op het apparaat en een van de verbindingen bevat de volgende regel: `Description . . . . . . . . . . . : ContosoMainVPN` . Gebruik de teken reeks `ContosoMainVPN` als de beschrijving van de **verbinding**. De lijst wordt weer gegeven als `Description:CONTOSOMAINVPN` .

> [!IMPORTANT]
> Als u deze functie optimaal wilt benutten, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Er wordt een nieuwe functionaliteit weer gegeven in de Configuration Manager-console wanneer u de-site en-console bijwerkt. Het volledige scenario werkt pas als de client versie ook het meest recent is.
>
> Als u deze VPN-grens wilt gebruiken tijdens de implementatie van een besturings systeem, moet u de opstart installatie kopie ook bijwerken om de nieuwste binaire client bestanden op te nemen.

## <a name="create-a-boundary"></a>Een grens maken

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **hiërarchie configuratie**uit en selecteer het knoop punt **grenzen** .

1. Selecteer **grens maken**op het tabblad **Start** van het lint in de groep **maken** .

1. Geef op het tabblad **Algemeen** van het venster **grens maken** de volgende gegevens op:

    - **Beschrijving**: Identificeer de grens met een beschrijvende naam of verwijzing.

        > [!NOTE]
        > Configuration Manager noemt de grens automatisch op basis van het type en bereik. U kunt de naam niet wijzigen.

    - **Type**: Selecteer het type grens dat u wilt maken. Geef vervolgens de aanvullende informatie op die voor het type nodig is. Zie [grens typen](#boundary-types)voor meer informatie.

1. Schakel over naar het tabblad **grens groepen** . Als u al grens groepen op de site hebt, kunt u deze nieuwe grens onmiddellijk aan een of meer groepen toevoegen.

1. Selecteer **OK** om de nieuwe grens op te slaan.

## <a name="configure-a-boundary"></a>Een grens configureren

> [!TIP]
> Wanneer u een grens maakt, wordt deze door Configuration Manager automatisch op basis van het type en het bereik van de grens. U kunt deze naam niet wijzigen. Geef een beschrijving op om de grens te identificeren in de Configuration Manager-console.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **hiërarchie configuratie**uit en selecteer het knoop punt **grenzen** .

1. Selecteer de grens die u wilt wijzigen. Klik op het tabblad **Start** van het lint in de groep **Eigenschappen** op **Eigenschappen**.

1. In het venster **Eigenschappen** voor de grens op het tabblad **Algemeen** kunt u de volgende instellingen configureren:

    - De **Beschrijving** bewerken
    - Het **type** voor de grens wijzigen
    - Het bereik van een grens wijzigen door de netwerk locaties ervan te bewerken. Voor een grens van het type Active Directory-site kunt u bijvoorbeeld een nieuwe naam opgeven.

1. Schakel over naar het tabblad **site systemen** om de site systemen weer te geven die zijn gekoppeld aan deze grens. U kunt deze configuratie niet wijzigen vanuit de eigenschappen van een grens.

    > [!TIP]
    > Als een server als een site systeem voor een grens moet worden weer gegeven, koppelt u deze als een site systeem server voor ten minste één grens groep die deze grens bevat. Maak deze configuratie op het tabblad **verwijzingen** van een grens groep. Zie [Configure site Assignment en select site System servers](boundary-group-procedures.md#bkmk_references)voor meer informatie.

1. Als u het lidmaatschap van de grens groep voor deze grens wilt wijzigen, selecteert u het tabblad **grens groepen** :

    - Als u deze grens aan een of meer grens groepen wilt toevoegen, selecteert u **toevoegen**. Selecteer een of meer grens groepen en selecteer vervolgens **OK**.

    - Als u deze grens uit een grens groep wilt verwijderen, kiest u de grens groep en selecteert u vervolgens **verwijderen**.

1. Selecteer **OK** om de grens eigenschappen te sluiten en de configuratie op te slaan.

## <a name="next-steps"></a>Volgende stappen

Elke grens is beschikbaar voor gebruik door elke site in uw hiërarchie. Nadat u een grens hebt gemaakt, voegt u de grens toe aan een of meer [grens groepen](boundary-groups.md).
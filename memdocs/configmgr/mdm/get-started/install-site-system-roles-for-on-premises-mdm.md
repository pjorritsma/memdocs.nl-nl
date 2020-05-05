---
title: Rollen installeren voor on-premises MDM
titleSuffix: Configuration Manager
description: Installeer de vereiste site systeem rollen voor on-premises Mobile Device Management (MDM) in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721855"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>Site systeem rollen installeren voor on-premises MDM in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voor Configuration Manager on-premises Mobile Device Management (MDM) zijn de volgende site systeem rollen op uw Configuration Manager-site vereist:

- Inschrijvingspunt

- Proxypunt voor inschrijving

- Distributiepunt

- Apparaatbeheerpunt, een beheer punt dat u toestaat voor mobiele apparaten

## <a name="requirements-and-limitations"></a>Vereisten en beperkingen

- Voor on-premises MDM moet u site systeem rollen inschakelen voor HTTPS-communicatie. Zie [certificaten voor vertrouwde communicatie instellen in on-premises MDM](set-up-certificates-on-premises-mdm.md)voor meer informatie.

- De huidige vertakking van Configuration Manager ondersteunt alleen *intranet* verbindingen van apparaten naar de distributie punten en Apparaatbeheer punten voor on-premises MDM. Als u echter ook macOS-computers beheert, hebben deze clients *Internet* verbindingen met dezelfde rollen nodig. Wanneer u het distributie punt en het apparaatbeheerpunt configureert, gebruikt u de optie voor het **toestaan van intranet-en Internet verbindingen**.

- Voor distributie punten die u configureert voor intranet verbindingen, moet u de site grenzen voor hen configureren. Configuration Manager ondersteunt alleen grenzen van IPv4-bereik voor on-premises MDM. Zie [site grenzen en grens groepen definiëren](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)voor meer informatie.

- Als u [database replica's](../../core/servers/deploy/configure/database-replicas-for-management-points.md) gebruikt met het apparaatbeheerpunt, zullen nieuwe geregistreerde apparaten in eerste instantie geen verbinding kunnen maken. Deze verbindings fout treedt op omdat de database replica niet over de informatie beschikt over het nieuwe geregistreerde apparaat dat nodig is voor een geslaagde verbinding. Replica's worden elke vijf minuten gesynchroniseerd. Apparaten kunnen de eerste vijf minuten na de inschrijving geen verbinding maken, wat meestal twee Verbindings pogingen zijn. Vervolgens kunnen apparaten verbinding maken.

## <a name="add-roles"></a>Functies toevoegen

Als u een on-premises MDM toevoegt aan een site met de meeste apparaten die worden beheerd met de Configuration Manager-client, is het mogelijk dat er al een aantal van deze rollen op de site is geïnstalleerd. Het distributie punt is bijvoorbeeld een gemeen schappelijke rol en het apparaatbeheerpunt is vereist voor het beheren van macOS-apparaten.

Zie [site systeem rollen toevoegen](../../core/servers/deploy/configure/install-site-system-roles.md)voor meer informatie over het toevoegen van functies aan uw site.

## <a name="configure-roles"></a>Rollen configureren

Nieuwe of bestaande rollen configureren om mobiele apparaten te beheren. Volg de onderstaande stappen om het distributie punt en het apparaatbeheerpunt zodanig te configureren dat het correct werkt voor on-premises MDM:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **servers en site systeem rollen** .

1. Selecteer de site systeem server met het distributie punt of het apparaatbeheerpunt dat u wilt configureren. Selecteer de server in de lijst en selecteer vervolgens de **site systeemrol** in het detail venster site systeem rollen. Selecteer in het lint op het tabblad **siterol** de optie **Eigenschappen**.

    > [!TIP]
    > In een grote site kunt u de weer gave zodanig beperken dat alleen servers met specifieke rollen worden weer gegeven. Wanneer u het knoop punt **servers en site systeem rollen** selecteert, selecteert u in het lint op het label Start de optie **servers met rol**. Selecteer vervolgens de gewenste rol in de lijst met functies die momenteel beschikbaar zijn op de site.

    Controleer op het tabblad **Algemeen** van de eigenschappen van het **site systeem**of de **naam** een Fully Qualified Domain Name (FQDN) is. Sluit de eigenschappen.

1. Selecteer in de lijst-console een server met een rol op een on-premises distributie punt. Selecteer de rol **distributie punt** in het deel venster Details van site systeem rollen. Selecteer in het lint op het tabblad **siterol** de optie **Eigenschappen**. Op het tabblad **communicatie** van de **Eigenschappen van het distributie punt**:

    1. Selecteer **https**en selecteer **alleen intranet verbindingen toestaan**.

        > [!IMPORTANT]
        > Als u Mac OS-computers ook beheert met de Configuration Manager-client, gebruikt u in plaats daarvan **intranet-en Internet verbindingen toestaan** .

    1. Schakel de optie in om **mobiele apparaten toe te staan verbinding te maken met dit distributie punt**en sluit vervolgens de eigenschappen.

1. Open de eigenschappen voor de site systeemrol van het **beheer punt** .

    1. Selecteer op het tabblad **Algemeen** de optie **https**en selecteer **alleen intranet verbindingen toestaan**.

        > [!IMPORTANT]
        > Als u Mac OS-computers ook beheert met de Configuration Manager-client, gebruikt u in plaats daarvan **intranet-en Internet verbindingen toestaan** .

    1. Schakel de optie in zodat **mobiele apparaten en Mac-computers dit beheer punt kunnen gebruiken**. Sluit vervolgens de eigenschappen.

        > [!NOTE]
        > Met deze optie wordt het beheer punt effectief omgezet in een *apparaatbeheerpunt* .  

## <a name="next-step"></a>Volgende stap

Nadat u de functies voor het beheren van mobiele apparaten hebt toegevoegd en geconfigureerd, moet u de servers als vertrouwde eind punten configureren. Met deze vertrouwens relatie kunnen rollen communiceren met en registratie van beheerde apparaten.

> [!div class="nextstepaction"]
> [Certificaten voor vertrouwde communicatie instellen](set-up-certificates-on-premises-mdm.md)

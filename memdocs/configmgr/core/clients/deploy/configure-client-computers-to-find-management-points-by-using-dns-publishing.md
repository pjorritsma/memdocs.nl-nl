---
title: Clients configureren voor het gebruik van DNS-publishing
titleSuffix: Configuration Manager
description: Configureer Configuration Manager-client computers om beheer punten te vinden met behulp van DNS-publishing.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d28a8a35f711dcef7e3f9adb6dccbabc4082ab28
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713098"
---
# <a name="configure-client-computers-to-find-management-points-by-using-dns-publishing"></a>Client computers configureren om beheer punten te vinden met DNS-publishing

*Van toepassing op: Configuration Manager (huidige vertakking)*

Clients in Configuration Manager moeten een beheer punt vinden om de site toewijzing te volt ooien en als een continu proces om beheerd te blijven. Active Directory Domain Services is de veiligste methode om clients op het intranet beheerpunten te laten vinden. Als clients deze servicelocatiemethode echter niet kunnen gebruiken (bijvoorbeeld als u het Active Directory-schema niet hebt uitgebreid of clients deel uitmaken van een werkgroep), gebruikt u DNS-publicatie als voorkeursalternatief voor de servicelocatiemethode.  

> [!NOTE]  
>  Wanneer u de client voor Linux en UNIX installeert, moet u een beheerpunt opgeven dat moet worden gebruikt als eerste contactpunt. Zie [clients implementeren op UNIX-en Linux-servers](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)voor meer informatie over het installeren van de-client voor Linux en UNIX.  

 Voordat u DNS-publicatie gebruikt voor beheerpunten, moet u ervoor zorgen dat DNS-servers op intranet servicelocatiebronrecords (SRV RR) en bijbehorende hostbronrecords (A of AAA) hebben voor de beheerpunten van de site. De service locatie bron records kunnen automatisch door Configuration Manager of hand matig worden gemaakt door de DNS-beheerder die de records in DNS maakt.  

 Zie [begrijpen hoe clients site resources en-services vinden voor Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)voor meer informatie over DNS-publicatie als een service locatie methode voor Configuration Manager-clients.  

 Clients zoeken standaard in DNS naar beheerpunten in hun DNS-domein. Als er echter geen beheer punten zijn gepubliceerd in het domein van de client, moet u clients hand matig configureren met een DNS-achtervoegsel van het beheer punt. U kunt dit DNS-achtervoegsel op clients configureren tijdens of na de clientinstallatie:  

-   Als u clients tijdens de clientinstallatie wilt configureren voor het achtervoegsel van een beheerpunt, configureert u de Client.msi-eigenschappen van CCMSetup.  

-   Als u clients na de clientinstallatie wilt configureren voor het achtervoegsel van een beheerpunt, configureert u de **Eigenschappen van Configuration Manager**.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Clients configureren voor een achtervoegsel van een beheerpunt tijdens de clientinstallatie  

- Installeer de client met de volgende Client.msi-eigenschap van CCMSetup:  

  - **DNSSUFFIX =** * &lt;beheer punt domein\>*  

     Als de site meer dan één beheerpunt heeft en deze zich in meer dan één domein bevinden, geeft u slechts één domein op. Wanneer clients verbinding maken met een beheerpunt in dit domein, downloaden ze een lijst met beschikbare beheerpunten, inclusief de beheerpunten van de andere domeinen.  

    Zie [over eigenschappen van client installatie](../../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie over de CCMSetup-opdracht regel eigenschappen.  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Clients configureren voor een achtervoegsel van een beheerpunt na de clientinstallatie  

1.  Navigeer in het Configuratiescherm van de clientcomputer naar **Configuration Manager**en dubbelklik vervolgens op **Eigenschappen**.  

2.  Geef op het tabblad **Site** het DNS-achtervoegsel van een beheerpunt op en klik vervolgens op **OK**.  

     Als de site meer dan één beheerpunt heeft en deze zich in meer dan één domein bevinden, geeft u slechts één domein op. Wanneer clients verbinding maken met een beheerpunt in dit domein, downloaden ze een lijst met beschikbare beheerpunten, inclusief de beheerpunten van de andere domeinen.

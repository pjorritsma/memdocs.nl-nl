---
title: " Ondersteunde sitesysteemservers"
titleSuffix: Configuration Manager
description: Ontdek welke Windows-versies u kunt gebruiken om een Configuration Manager site of site systeemrol te hosten.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc58ae7f7b5629319d239f9c48b5c6572fb28116
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711586"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Ondersteunde besturings systemen voor Configuration Manager-site systeem servers

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel worden de Windows-versies beschreven die u kunt gebruiken om een Configuration Manager site of site systeemrol te hosten.

Gebruik de informatie in dit artikel met de informatie in de volgende artikelen:

- [Aanbevolen hardware voor Configuration Manager](recommended-hardware.md)
- [Site-en site systeem vereisten voor Configuration Manager](site-and-site-system-prerequisites.md)
- [Grootte en schaalgrootte voor Configuration Manager](size-and-scale-numbers.md)

## <a name="windows-server-2019"></a><a name="bkmk_2019"></a>Windows Server 2019

*Van toepassing op Windows Server 2019: Standard en Data Center* 

Vanaf versie 1810 wordt deze versie van het besturings systeem ondersteund voor de volgende rollen:

#### <a name="site-servers"></a>Siteservers

- Centrale beheersite  
- Primaire site  
- Secundaire site  

#### <a name="site-system-servers"></a>Sitesysteemservers

- Application Catalog-webservicepunt  
- Application Catalog-websitepunt  
- Asset Intelligence-synchronisatiepunt  
- Certificaatregistratiepunt  
- Verbindings punt van de Cloud beheer gateway  
- Data Warehouse-service punt  
- Distributie punt <sup> [Opmerking 1](#bkmk_note1)</sup>  
- Endpoint Protection-punt  
- Inschrijvingspunt  
- Proxypunt voor inschrijving  
- Terugvalstatuspunt  
- Beheerpunt
- Reporting Services-punt  
- Serviceverbindingspunt  
- Site database server <sup> [Opmerking 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Software-updatepunt  
- Statusmigratiepunt

## <a name="windows-server-2016"></a><a name="bkmk_2016"></a>Windows Server 2016

*Van toepassing op Windows Server 2016: Standard en Data Center*

Deze versie van het besturings systeem wordt ondersteund voor de volgende rollen:

#### <a name="site-servers"></a>Siteservers

- Centrale beheersite  
- Primaire site  
- Secundaire site  

#### <a name="site-system-servers"></a>Sitesysteemservers

- Application Catalog-webservicepunt  
- Application Catalog-websitepunt  
- Asset Intelligence-synchronisatiepunt  
- Certificaatregistratiepunt  
- Verbindings punt van de Cloud beheer gateway  
- Data Warehouse-service punt  
- Distributie punt <sup> [Opmerking 1](#bkmk_note1)</sup>  
- Endpoint Protection-punt  
- Inschrijvingspunt  
- Proxypunt voor inschrijving  
- Terugvalstatuspunt  
- Beheerpunt
- Reporting Services-punt  
- Serviceverbindingspunt  
- Site database server <sup> [Opmerking 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Software-updatepunt  
- Statusmigratiepunt

## <a name="windows-storage-server-2016"></a><a name="bkmk_stor2016"></a>Windows Storage Server 2016

#### <a name="site-system-server"></a>Sitesysteemserver

- Distributie punt <sup> [Opmerking 1](#bkmk_note1)</sup>  

## <a name="windows-server-2012-r2"></a><a name="bkmk_2012r2"></a>Windows Server 2012 R2

*Van toepassing op Windows Server 2012 R2: Standard en Data Center*

#### <a name="site-servers"></a>Siteservers

- Centrale beheersite  
- Primaire site  
- Secundaire site  

#### <a name="site-system-servers"></a>Sitesysteemservers

- Application Catalog-webservicepunt  
- Application Catalog-websitepunt  
- Asset Intelligence-synchronisatiepunt  
- Certificaatregistratiepunt  
- Verbindings punt van de Cloud beheer gateway  
- Data Warehouse-service punt  
- Distributie punt <sup> [Opmerking 1](#bkmk_note1)</sup>  
- Endpoint Protection-punt  
- Inschrijvingspunt  
- Proxypunt voor inschrijving  
- Terugvalstatuspunt  
- Beheerpunt
- Reporting Services-punt  
- Serviceverbindingspunt  
- Site database server <sup> [Opmerking 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Software-updatepunt  
- Statusmigratiepunt  

## <a name="windows-server-2012"></a><a name="bkmk_2012"></a>Windows Server 2012  

*Van toepassing op Windows Server 2012: Standard en Data Center*

#### <a name="site-servers"></a>Siteservers

- Centrale beheersite  
- Primaire site  
- Secundaire site  

#### <a name="site-system-servers"></a>Sitesysteemservers

- Application Catalog-webservicepunt  
- Application Catalog-websitepunt  
- Asset Intelligence-synchronisatiepunt  
- Certificaatregistratiepunt  
- Verbindings punt van de Cloud beheer gateway  
- Data Warehouse-service punt  
- Distributie punt <sup> [Opmerking 1](#bkmk_note1)</sup>  
- Endpoint Protection-punt  
- Inschrijvingspunt  
- Proxypunt voor inschrijving  
- Terugvalstatuspunt  
- Beheerpunt
- Reporting Services-punt  
- Serviceverbindingspunt  
- Site database server <sup> [Opmerking 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Software-updatepunt  
- Statusmigratiepunt  

## <a name="client-os-versions"></a><a name="bkmk_client"></a>Versies van client besturingssysteem

De volgende versies van client besturingssystemen worden ondersteund voor gebruik als een **distributie punt** <sup>[Opmerking 1](#bkmk_note1)</sup>:  

- Windows 10 (x86, x64): Pro en Enter prise

    Zie [ondersteuning voor Windows 10](support-for-windows-10.md)voor meer informatie over ondersteunde versies van builds.

- Windows 8,1 (x86, x64): Professional en Enter prise

Deze ondersteuning heeft de volgende beperking:  

- Distributie punten op dit besturings systeem bieden geen ondersteuning voor PXE of multi cast met de standaard Windows Deployment Services. Vanaf versie 1806 kunt u een distributie punt op dit besturings systeem PXE inschakelen met de optie om **een PXE-responder in te scha kelen zonder Windows Deployment service**. Zie [distributie punten installeren en configureren](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)voor meer informatie.  

## <a name="server-core-installations"></a><a name="bkmk_core"></a>Server Core-installaties

De Server Core-installatie van de volgende versies van het besturings systeem van de server wordt ondersteund voor gebruik als een **distributie punt**:

- Windows Server 2019 (vanaf Configuration Manager, versie 1810)  
- Windows Server, versie 1809 (vanaf Configuration Manager, versie 1810)  
- Windows Server, versie 1803 (vanaf Configuration Manager, versie 1802)  
- Windows Server, versie 1709 (vanaf Configuration Manager, versie 1710)  
- Windows Server 2016  
- Windows Server 2012 R2  
- Windows Server 2012  

Deze ondersteuning heeft de volgende beperking:  

- Distributie punten op dit besturings systeem bieden geen ondersteuning voor PXE of multi cast met de standaard Windows Deployment Services. Vanaf versie 1806 kunt u een distributie punt op dit besturings systeem PXE inschakelen met de optie om **een PXE-responder in te scha kelen zonder Windows Deployment service**. Zie [distributie punten installeren en configureren](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)voor meer informatie.  

## <a name="general-notes"></a>Algemene opmerkingen

### <a name="note-1-distribution-points"></a><a name="bkmk_note1"></a>Opmerking 1: distributie punten

Distributie punten bieden ondersteuning voor verschillende configuraties waarvoor verschillende vereisten gelden. In sommige gevallen ondersteunen deze configuraties niet alleen op servers, maar op client besturingssystemen. Zie [inhoud en infra structuur voor inhoud beheren](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)voor meer informatie.  

### <a name="note-2-site-database-servers"></a><a name="bkmk_note2"></a>Opmerking 2: site database servers

Site database servers worden niet ondersteund op een alleen-lezen domein controller (RODC). Zie voor meer informatie het Microsoft Ondersteuning artikel: [u kunt problemen ondervinden bij het installeren van SQL Server op een domein controller](https://support.microsoft.com/help/2032911). 

Bovendien worden secundaire site servers niet ondersteund op een domein controller.  

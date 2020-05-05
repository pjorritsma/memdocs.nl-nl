---
title: Grondbeginselen van het beheer van apparaten
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van Configuration Manager voor het beheren van apparaten.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bbe7f3a69694395f95596f7f1497c7356b33715f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722842"
---
# <a name="fundamentals-of-managing-devices-with-configuration-manager"></a>Grond beginselen van het beheer van apparaten met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager kunt twee grote categorieën apparaten beheren:

- *Clients* zijn apparaten als werk stations, laptops, servers en mobiele apparaten waarop u de Configuration Manager-client software installeert. Voor sommige beheer functies, zoals hardware-inventaris, is deze client software vereist.  

- *Beheerde apparaten* kunnen *clients*omvatten, maar dit is meestal een mobiel apparaat waarop de Configuration Manager-client software niet is geïnstalleerd. Op dit type apparaat beheert u met behulp van de ingebouwde on-premises Mobile Device Management in Configuration Manager.

U kunt apparaten ook groeperen en identificeren op basis van de gebruiker, niet alleen het client type.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Apparaten met de Configuration Manager-client beheren

Er zijn twee manieren om de Configuration Manager-client software te gebruiken voor het beheren van een apparaat. De eerste manier is om het apparaat op uw netwerk te detecteren en vervolgens de client software op dat apparaat te implementeren. De andere manier is om de-client software hand matig te installeren op een nieuwe computer en vervolgens de computer aan uw-site toe te voegen wanneer deze lid wordt van uw netwerk. Als u apparaten wilt detecteren waarop de client software niet is geïnstalleerd, voert u een of meer van de ingebouwde detectie methoden uit. Nadat een apparaat is gedetecteerd, kunt u een van de volgende methoden gebruiken om de-client software te installeren. Zie [detectie uitvoeren voor Configuration Manager](../servers/deploy/configure/run-discovery.md)voor meer informatie over het gebruik van detectie.  

Nadat u de apparaten hebt gedetecteerd die worden ondersteund om de Configuration Manager-client software uit te voeren, kunt u een van de volgende methoden gebruiken om de software te installeren. Nadat de software is geïnstalleerd en de client is toegewezen aan een primaire site, kunt u beginnen het apparaat te beheren. Veelvoorkomende installatie methoden zijn:

- Clientpushinstallatie

- Installatie op basis van software-updates

- Groeps beleid

- Hand matige installatie op een computer

- De client opnemen als onderdeel van een installatie kopie van het besturings systeem die u implementeert  

Nadat de client is geïnstalleerd, kunt u de taken voor het beheer van apparaten vereenvoudigen met behulp van verzamelingen. Verzamelingen zijn groepen van apparaten of gebruikers die u maakt, zodat u ze als groep kunt beheren. U wilt bijvoorbeeld een toepassing voor mobiele apparaten installeren op alle mobiele apparaten die Configuration Manager registreren. Als dit het geval is, kunt u de verzameling alle mobiele apparaten gebruiken.  

Raadpleeg voor meer informatie de volgende artikelen:  

- [Een oplossing voor apparaatbeheer kiezen](../plan-design/choose-a-device-management-solution.md)  

- [Clientinstallatiemethoden](../clients/deploy/plan/client-installation-methods.md)  

- [Inleiding op verzamelingen](../clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Clientinstellingen

Wanneer u Configuration Manager voor het eerst installeert, worden alle clients in de hiërarchie geconfigureerd met behulp van de standaard client instellingen die u kunt wijzigen. De client instellingen omvatten de volgende configuratie opties:

- Hoe vaak de apparaten communiceren met de site.

- Of de client is ingesteld voor software-updates en andere beheer bewerkingen.

- Hiermee wordt aangegeven of gebruikers hun mobiele apparaten kunnen inschrijven, zodat ze door Configuration Manager worden beheerd.  

U kunt aangepaste client instellingen maken en deze vervolgens toewijzen aan verzamelingen. Leden van de verzameling zijn geconfigureerd voor de aangepaste instellingen en u kunt meerdere aangepaste client instellingen maken die worden toegepast in de volg orde die u opgeeft (op numerieke volg orde). Als er sprake is van conflicterende instellingen, overschrijft de instelling met het laagste volgordenummer de andere stellingen.  

Het volgende diagram toont een voor beeld van hoe u aangepaste client instellingen kunt maken en Toep assen.  

![Clientinstellingen](media/ClientSettings.gif)  

Raadpleeg de volgende artikelen voor meer informatie over client instellingen:

- [Clientinstellingen configureren](../clients/deploy/configure-client-settings.md)
- [Clientinstellingen](../clients/deploy/about-client-settings.md)


## <a name="managing-devices-without-the-configuration-manager-client"></a>Apparaten zonder de Configuration Manager-client beheren

Configuration Manager ondersteunt het beheer van sommige apparaten waarop de client software niet is geïnstalleerd en die niet worden beheerd door intune. Zie [mobiele apparaten met on-premises infra structuur beheren in Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) en [mobiele apparaten beheren met Configuration Manager en Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)voor meer informatie.  

## <a name="user-based-management"></a>Beheer op basis van gebruikers

Configuration Manager ondersteunt verzamelingen van Azure Active Directory en Active Directory Domain Services gebruikers. Wanneer u een gebruikers verzameling gebruikt, kunt u software installeren op alle computers die deel uitmaken van de verzameling. Als u er zeker van wilt zijn dat de software die u implementeert alleen installaties installeert op de apparaten die zijn opgegeven als primair apparaat van een gebruiker, stelt u de gebruikers affiniteit apparaat in. Een gebruiker kan één of meer primaire apparaten hebben.  

Een van de manieren waarop gebruikers hun software-implementatie kunnen beheren, is om de **Software Center** -client interface te gebruiken. Het **Software Center** wordt automatisch geïnstalleerd op client computers en wordt uitgevoerd vanuit het menu **Start** van Windows. Met het **Software Center** kunnen gebruikers hun eigen software beheren en de volgende taken uitvoeren:  

- Software installeren  

- Een planning maken om automatisch software te installeren buiten kantooruren  

- Configureren wanneer Configuration Manager software op een apparaat kan installeren  

- De toegangs instellingen configureren voor extern beheer, als extern beheer is ingesteld in Configuration Manager  

- Opties configureren voor energie beheer als een beheerder deze optie instelt  

- Software zoeken, installeren en aanvragen

- Voorkeurs instellingen configureren

- Wanneer het is ingesteld, geeft u een primair apparaat op voor de gebruikers affiniteit apparaat

Raadpleeg voor meer informatie de volgende artikelen:

- [Software Center plannen](../../apps/plan-design/plan-for-software-center.md)
- [Gebruikers en apparaten koppelen met affiniteit met apparaat van gebruiker](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)
- [Gebruikershandleiding van Software Center](software-center.md)

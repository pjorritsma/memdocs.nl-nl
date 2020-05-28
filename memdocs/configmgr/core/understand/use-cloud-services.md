---
title: Cloudservices gebruiken
titleSuffix: Configuration Manager
description: Richt cloud resources in voor Configuration Manager om uw on-premises infra structuur aan te vullen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84cb878de3eea56dc68180a83fd4b6a32b2d1073
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906427"
---
# <a name="use-cloud-services-with-configuration-manager"></a>Cloudservices met Configuration Manager gebruiken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager ondersteunt verschillende Cloud opties. Deze kunnen een aanvulling vormen op uw on-premises infra structuur en kunnen helpen bij het oplossen van bedrijfs problemen, zoals:  

-   BYOD beheren (met intune voor Mobile Device Management).  

-   Inhouds bronnen aanbieden aan geïsoleerde clients of bronnen op het intranet buiten uw bedrijfs firewall (met behulp van distributie punten in de Cloud).  

-   De infra structuur uitschalen wanneer er geen fysieke hardware beschikbaar is of niet logisch is geplaatst ter ondersteuning van uw behoeften (door gebruik te maken van Microsoft Azure virtuele machines).  

Hoewel het inrichten van cloud resources niet iets hoeft te doen voordat u Configuration Manager implementeert, kan het nuttig zijn om deze opties te begrijpen voordat ze te ver in het ontwerp plan voor een hiërarchie worden uitgevoerd. Het gebruik van Cloud bronnen bespaart u geld en tijd, terwijl u zakelijke problemen kunt oplossen die on-premises infra structuur niet kunnen.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Cloud resources die u kunt gebruiken met Configuration Manager  
 Omdat er voor elke optie verschillende vereisten gelden, is het zinvol om u hierin te verdiepen zodat u bekend raakt met de unieke vereisten, beperkingen en mogelijkheden voor extra kosten op basis van het gebruik.  

-   Zie [cloud-gebaseerde distributie punten installeren](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)voor meer informatie over distributie punten in de Cloud.

-   Zie [Wat is Azure?](https://azure.microsoft.com/overview/what-is-azure/) voor meer informatie over Azure.

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Virtuele Azure-machines (voor Cloud infrastructuur)  
 Configuration Manager ondersteunt het gebruik van computers die worden uitgevoerd op virtuele machines in azure, net zoals wanneer de on-premises in uw fysieke bedrijfs netwerk worden uitgevoerd. U kunt in de volgende scenario's kunt virtuele Azure-machines gebruiken:  

-   **Scenario 1:** U kunt Configuration Manager uitvoeren op een virtuele machine en deze gebruiken om clients te beheren die zijn geïnstalleerd op andere virtuele machines.  

-   **Scenario 2:** U kunt Configuration Manager uitvoeren op een virtuele machine en gebruiken om clients te beheren die niet worden uitgevoerd in Azure.  

-   **Scenario 3:** U kunt verschillende Configuration Manager-site systeem rollen uitvoeren op virtuele machines en tegelijkertijd andere rollen uitvoeren in uw fysieke bedrijfs netwerk (met de juiste netwerk verbinding voor communicatie).  

Dezelfde vereisten voor netwerken, besturings systemen en hardware-vereisten die van toepassing zijn op het installeren van de Configuration Manager op uw fysieke bedrijfs netwerk, zijn ook van toepassing op de installatie van Configuration Manager in Azure.  

Een Azure-abonnement is vereist voor het gebruik van Azure virtual machines. Er worden kosten in rekening gebracht op basis van het aantal virtuele machines dat u gebruikt, de configuratie en het gebruik van cloud resources.  

Daarnaast gelden voor Configuration Manager-sites en-clients die worden uitgevoerd op virtuele Azure-machines dezelfde licentie vereisten als voor on-premises installaties.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Azure-Services (voor distributie punten in de Cloud)  
 U kunt een Azure-service gebruiken om een Configuration Manager distributie punt te hosten. dit wordt ook wel een distributie punt in de Cloud genoemd. U kunt [een distributie punt in de Cloud gebruiken met Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) naast on-premises distributie punten en distributie punten die zijn geïmplementeerd in azure virtual machines.  

 Dit verschilt van het gebruik van een virtuele Azure-machine, waarop u een sitesysteemrol implementeert. Distributie punten in de Cloud:  

-   Als service uitvoeren in azure, en niet op een virtuele machine.  

-   Automatisch schalen om te voldoen aan verhoogde inhouds aanvragen van clients.  

-   Ondersteunings-clients op internet en het intranet.  

Een Azure-abonnement is vereist voor het gebruik van Azure om distributie punten te hosten. Er worden kosten in rekening gebracht op basis van de hoeveelheid gegevens die worden overgedragen van en naar de service.  

### <a name="additional-configuration-manager-capabilities"></a>Aanvullende Configuration Manager-functies  
 Sommige Configuration Manager mogelijkheden kunnen verbinding maken met Cloud Services, zoals:  

-   Windows Server Update Services (WSUS).  

-   De Configuration Manager Service Cloud, om updates te downloaden voor Configuration Manager.  

Voor deze aanvullende mogelijkheden hebt u geen Azure-abonnement nodig. U hoeft geen specifieke verbindingen, certificaten of services in te stellen in de Cloud. In plaats daarvan worden ze automatisch door Configuration Manager voor u beheerd. Het enige wat u hoeft te doen, is ervoor te zorgen dat toepasselijke site systemen en apparaten toegang hebben tot de Url's op internet.  

##  <a name="security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a>Beveiliging voor Cloud Services  
 Configuration Manager gebruikt certificaten voor het inrichten en openen van uw inhoud in azure, en voor het beheren van de services die u gebruikt. Configuration Manager versleutelt de gegevens die u in azure opslaat, maar brengt geen aanvullende beveiligings-of gegevens controles meer uit dan die die Azure biedt.  

 Zie de Details voor de verschillende Cloud resource scenario's voor meer informatie. Zie ook een [Inleiding tot Azure-beveiliging](https://docs.microsoft.com/azure/security/fundamentals/overview).

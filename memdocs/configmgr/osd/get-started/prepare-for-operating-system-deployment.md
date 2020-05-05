---
title: Voorbereidingen voor besturingssysteemimplementatie
titleSuffix: Configuration Manager
description: Meer informatie over het voorbereiden van implementaties van besturings systemen in Configuration Manager
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bdd8cd61aedb06fe35a4ba268806f64cc18bf85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724081"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>De implementatie van het besturings systeem voorbereiden in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Er zijn verschillende dingen die u moet doen in Configuration Manager voordat u besturings systemen kunt implementeren. Gebruik de volgende artikelen om de implementatie van het besturings systeem voor te bereiden:  

-   [Opstartinstallatiekopieën beheren](manage-boot-images.md)  

-   [Installatiekopieën van besturingssysteem beheren](manage-operating-system-images.md)  

-   [Upgradepakketten voor besturingssysteem beheren](manage-operating-system-upgrade-packages.md)  

-   [Stuurprogramma's beheren](manage-drivers.md)  

-   [De gebruikersstatus beheren](manage-user-state.md)  

-   [Voorbereiden op onbekende computerimplementaties](prepare-for-unknown-computer-deployments.md)  

-   [Gebruikers koppelen aan een doelcomputer](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>Grootte van installatie kopie van besturings systeem  

Installatie kopieën van het besturings systeem hebben een grote grootte. De grootte van de installatie kopie voor Windows 7 is bijvoorbeeld 3 GB of meer. De grootte van de installatie kopie en het aantal computers waarop u het besturings systeem tegelijkertijd implementeert, is van invloed op de netwerk prestaties en de beschik bare band breedte. Zorg ervoor dat u de netwerk prestaties test. Testen van de impact betere meters het effect dat de implementatie van de installatie kopie kan hebben en de tijd die nodig is om de implementatie te volt ooien. Configuration Manager activiteiten die van invloed zijn op de netwerk prestaties, zijn het distribueren van de installatie kopie naar een distributie punt, het distribueren van de installatie kopie van de ene site naar de andere en het downloaden van de installatie kopie naar de client.  

Zorg er ook voor dat u voldoende schijf ruimte plant op de distributie punten die de installatie kopieën van het besturings systeem hosten.  

Zie [aanvullende plannings overwegingen voor distributie punten](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_AdditionalPlanning)voor meer informatie.


### <a name="client-cache-size"></a>Clientcachegrootte  

Wanneer Configuration Manager-clients inhoud downloaden, gebruiken ze automatisch Background Intelligent Transfer Service (BITS), als deze beschikbaar zijn. Wanneer u een taken reeks implementeert waarmee een besturings systeem wordt geïnstalleerd, kunt u een optie instellen op de implementatie zodat Configuration Manager-clients de volledige installatie kopie downloaden naar een lokale cache voordat de taken reeks wordt uitgevoerd.  

Wanneer een Configuration Manager-client een installatie kopie van het besturings systeem moet downloaden, maar er onvoldoende ruimte is in de cache, kan de client ruimte in de cache verwijderen. De andere pakketten in de cache worden gecontroleerd om te bepalen of het verwijderen van de oudste pakketten voldoende schijf ruimte vrijmaakt voor de installatie kopie. Als het verwijderen van pakketten niet voldoende ruimte vrijmaakt, wordt de installatie kopie niet door de client gedownload en mislukt de implementatie. Dit gedrag kan optreden als het cache geheugen een groot pakket heeft dat u configureert voor persistent in de cache. Als er met het verwijderen van pakketten voldoende geheugen wordt vrijgemaakt in de cache, worden ze verwijderd en downloadt de client de installatiekopie naar het cachegeheugen.  

De standaard cache grootte op Configuration Manager-clients is mogelijk niet groot genoeg voor de meeste implementaties van installatie kopieën van besturings systemen. Als u van plan bent de volledige installatie kopie te downloaden naar de client cache, past u de cache grootte van de client aan op de doel computers om de grootte van de installatie kopie die u implementeert toe te passen.  

Zie [de client cache configureren](../../core/clients/manage/manage-clients.md#BKMK_ClientCache)voor meer informatie.  



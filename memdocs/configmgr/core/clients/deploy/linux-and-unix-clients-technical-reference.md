---
title: UNIX/Linux-client onderdeel Services en opdrachten
titleSuffix: Configuration Manager
description: Meer informatie over onderdeel Services en opdrachten op Linux-en UNIX-clients in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de564595ce51a336b5f11d4050928fa812269601
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713343"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Linux-en UNIX-clients onderdeel Services en opdrachten voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> Vanaf versie 1902 biedt Configuration Manager geen ondersteuning voor Linux-of UNIX-clients. 
> 
> Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.


 De volgende tabel bevat de client Component Services van de Configuration Manager-client voor Linux en UNIX.  

|Bestandsnaam|Meer informatie|  
|---------------|----------------------|  
|ccmexec.bin|Deze service is vergelijkbaar met de ccmexc-service op een Windows-client. Het is verantwoordelijk voor alle communicatie met Configuration Manager-site systeem rollen en communiceert tevens met de service omiserver. bin voor het verzamelen van hardware-inventaris van de lokale computer.<br /><br /> Voer uit voor een lijst met ondersteunde opdracht regel argumenten`ccmexec -h`|  
|omiserver.bin|Deze service is de CIM-server. De CIM-server biedt een raamwerk voor pluggable softwaremodules, die providers worden genoemd. Providers communiceren met Linux en UNIX computerresources en verzamelen de hardware-inventarisgegevens. De **proces-provider** voor een Linux-computer verzamelt bijvoorbeeld gegevens die zijn gekoppeld aan de processen van het Linux-besturingssysteem.|  

 De volgende tabellen bevatten opdrachten die u kunt gebruiken om de clientservices (ccmexec.bin en omiserver.bin) op elke versie van Linux of UNIX te starten, te stoppen of opnieuw op te starten. Bij het starten of stoppen van de service ccmexec, wordt de service omniserver ook wordt gestart of gestopt.  

|Besturingssysteem|Opdrachten|  
|----------------------|--------------|  
|Universele Agent<br /><br /> RHEL 4 en SLES 9|Starten`/etc/init d/ccmexecd start`<br /><br /> Tab`/etc/init d/ccmexecd stop`<br /><br /> Opnieuw`/etc/init d/ccmexecd restart`|  
|Solaris 9|Starten`/etc/init d/ccmexecd start`<br /><br /> Tab`/etc/init d/ccmexecd stop`<br /><br /> Opnieuw`/etc/init d/ccmexecd restart`|  
|Solaris 10|Starten:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Stoppen:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|Starten:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Stoppen:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|Starten:<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> Stoppen:<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|Starten`/sbin/init.d/ccmexecd start`<br /><br /> Tab`/sbin/init.d/ccmexecd stop`<br /><br /> Opnieuw`/sbin/init.d/ccmexecd restart`|  

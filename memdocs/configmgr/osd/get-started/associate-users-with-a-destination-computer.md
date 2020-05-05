---
title: " Gebruikers koppelen aan een computer"
titleSuffix: Configuration Manager
description: Configureer Configuration Manager om gebruikers te koppelen aan doel computers bij het implementeren van besturings systemen.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3a77e06dd2502b9007244ff9a3c9c9922fea592
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724200"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Gebruikers koppelen aan een doel computer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u Configuration Manager gebruikt om besturings systemen te implementeren, kunt u gebruikers koppelen aan de doel computer. Deze optie werkt op basis van het feit of een of meer gebruikers de primaire gebruikers van de doel computer zijn.  

De gebruikersaffiniteit van apparaten biedt ondersteuning voor op de gebruiker gericht beheer wanneer u toepassingen implementeert. Wanneer u een gebruiker koppelt aan de doel computer waarop een besturings systeem moet worden geïnstalleerd, kunt u later toepassingen voor die gebruiker implementeren en worden de toepassingen automatisch op de doel computer geïnstalleerd. Hoewel u tijdens de implementatie van het besturings systeem ondersteuning voor de gebruikers affiniteit van apparaten kunt configureren, kunt u de gebruikers affiniteit van het apparaat niet gebruiken om het besturings systeem te implementeren.  

Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie over gebruikers affiniteit met apparaat.  

Er zijn verschillende methoden waarmee u de affiniteit tussen gebruikers en apparaten in uw besturingssysteem implementaties kunt integreren. U kunt de gebruikersaffiniteit van apparaten integreren in PXE-implementaties, implementaties met opstartbare media en implementaties met voorgefaseerde media.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>Een takenreeks maken die de variabele **SMSTSAssignUsersMode** bevat

Voeg de variabele **SMSTSAssignUsersMode** toe aan het begin van de taken reeks met behulp van de stap [taken reeks variabele instellen](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) . Met deze variabele geeft u op hoe de takenreeks omgaat met de gebruikersinformatie.

Zie [taken reeks variabelen](../understand/task-sequence-variables.md#SMSTSAssignUsersMode)voor meer informatie.


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Een prestart-opdracht maken waarmee de gebruikersinformatie worden verzameld

De prestart-opdracht kan een VBScript zijn met een invoervak. Het kan ook een HTML-toepassing (HTA) zijn waarmee de door u ingevoerde gebruikers gegevens worden gevalideerd. 

Met deze prestart-opdracht moet de **SMSTSUDAUsers** -variabele worden ingesteld die wordt gebruikt wanneer de taken reeks wordt uitgevoerd. Deze variabele kan worden ingesteld voor een computer, een verzameling of een variabele in een takenreeks.

Zie [taken reeks variabelen](../understand/task-sequence-variables.md#SMSTSUDAUsers)voor meer informatie.


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Configureren hoe distributiepunten en media de gebruiker koppelen aan de doelcomputer

Het distributie punt of de media ondersteunt het koppelen van gebruikers aan de doel computer waarop het besturings systeem wordt geïmplementeerd. Gebruik een van de volgende methoden: 

- [Een distributie punt configureren om PXE-opstart aanvragen te accepteren](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)  
- [Opstartbare media maken](../deploy-use/create-bootable-media.md)  
- [Voor bereide media maken](../deploy-use/create-prestaged-media.md)  


Het configureren van de ondersteuning voor affiniteit tussen gebruikers en apparaten heeft geen ingebouwde methode om de gebruikers identiteit te valideren. Dit gedrag is belang rijk wanneer een technicus de computer inricht en de informatie namens de gebruiker invoert. Naast het instellen van de manier waarop de taken reeks de gebruikers gegevens verwerkt, is het configureren van deze opties op het distributie punt en de media de mogelijkheid om de implementaties te beperken die worden gestart via een PXE-opstart bewerking of vanaf een specifiek type media.

---
title: Linux- en UNIX-clients upgraden
titleSuffix: Configuration Manager
description: Een upgrade uitvoeren van een client op een Linux-of UNIX-server in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f71a36dff92f888d595538ff2fd483d7c212358f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715394"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Clients voor Linux-en UNIX-servers bijwerken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> Vanaf versie 1902 biedt Configuration Manager geen ondersteuning voor Linux-of UNIX-clients. 
> 
> Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.

U kunt de versie van de client voor Linux en UNIX op een computer bijwerken naar een nieuwere clientversie zonder dat u de huidige client eerst hoeft te verwijderen. U doet dit door het nieuwe client installatie pakket op de computer te installeren terwijl u de opdracht regel eigenschap **-keepdb** gebruikt. Wanneer de client voor Linux en UNIX wordt geïnstalleerd, worden de bestaande clientgegevens overschreven met de nieuwe clientbestanden. De opdracht regel eigenschap **-keepdb** leidt echter het installatie proces om de unieke ID'S (GUID), de lokale data base van de gegevens en het certificaat archief van de clients te bewaren. Deze informatie wordt vervolgens gebruikt door de nieuwe clientinstallatie.  

 Als u bijvoorbeeld een RHEL5 x64-computer hebt waarop de client uit de oorspronkelijke release van de Configuration Manager-client voor Linux en UNIX wordt uitgevoerd. Als u deze client wilt bijwerken naar de client versie uit cumulatieve update 1, voert u hand matig het **installatie** script uit om het toepasselijke client pakket te installeren op basis van cumulatieve update 1, met de toevoeging van de opdracht regel optie **-keepdb** . Raadpleeg het volgende voor beeld van de opdracht regel:  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Een software-implementatie gebruiken om de client op Linux- en UNIX-servers bij te werken  
 Een software-implementatie gebruiken om de client op Linux- en UNIX-servers bij te werken De Configuration Manager-client kan het installatie script echter niet rechtstreeks uitvoeren om de nieuwe client te installeren, omdat voor de installatie van een nieuwe client eerst de huidige client moet worden verwijderd. Met deze actie wordt het Configuration Manager-client proces dat het installatie script uitvoert, beëindigd voordat de installatie van de nieuwe client wordt gestart. Als u een software-implementatie wilt gebruiken om de nieuwe client te installeren, moet u de installatie zodanig plannen dat deze op een later tijdstip wordt gestart en wordt uitgevoerd door de ingebouwde plannings mogelijkheden van het besturings systeem.  

 Gebruik een software-implementatie om eerst de bestanden voor het nieuwe client installatie pakket naar de client computer te kopiëren. Implementeer en voer vervolgens een script uit om het client installatie proces te plannen. Het script maakt gebruik van de ingebouwde **at** -opdracht van het besturings systeem om de start uit te stellen. Wanneer het script wordt uitgevoerd, wordt de bewerking beheerd door het besturings systeem van de client en niet door de Configuration Manager-client op de computer. Met dit gedrag kan de opdracht regel die door het script wordt aangeroepen, eerst de Configuration Manager-client verwijderen en vervolgens de nieuwe client installeren. Deze acties volt ooien het proces van client upgrade op de Linux-of UNIX-computer. Nadat de upgrade is voltooid, blijft de bijgewerkte client beheerd door Configuration Manager.  

 Gebruik de volgende procedure om een software-implementatie te configureren waarmee de client voor Linux en UNIX kan worden bijgewerkt. Met de volgende stappen en voorbeelden wordt een RHEL5 x64-computer waarop de initiële release van de client wordt uitgevoerd, bijgewerkt naar de clientversie van de cumulatieve update 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Een software-implementatie gebruiken om de client op Linux- en UNIX-servers bij te werken  

1. Kopieer het nieuwe client installatie pakket naar de computer waarop de Configuration Manager-client wordt uitgevoerd om een upgrade uit te voeren.  

    Plaats bijvoorbeeld het client installatie pakket en installeer script voor cumulatieve update 1 op de volgende locatie op de client computer: **/tmp/patch**  

2. Maak een script om de upgrade van de Configuration Manager-client te beheren. Plaats vervolgens een kopie van het script in dezelfde map op de client computer als de client installatie bestanden uit stap 1.  

    Het script vereist geen specifieke naam. Het moet opdracht regels bevatten die voldoende zijn voor het gebruik van de client installatie bestanden uit een lokale map op de client computer en het installeren van het client installatie pakket met behulp van de opdracht regel eigenschap **-keepdb** . Gebruik de opdracht regel eigenschap **-keepdb** om de unieke id van de huidige client bij te houden voor gebruik door de nieuwe client die u installeert.  

    Maak bijvoorbeeld een script met de naam **upgrade.sh** dat de volgende regels bevat:  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    Kopieer deze vervolgens naar de map **/tmp/patch** op de client computer.

3. Gebruik software-implementatie om ervoor te zorgen dat elke client de ingebouwde **at** -opdracht van de computer gebruikt om het script **upgrade.sh** met een korte vertraging uit te voeren voordat het script wordt uitgevoerd.  

    Gebruik bijvoorbeeld de volgende opdracht regel om het script uit te voeren: **at-f/tmp/upgrade.sh-m nu + 5 minuten**  

   Nadat de client de uitvoering van het script **upgrade.sh** heeft gepland, wordt er een statusbericht door de client verzonden dat de software-implementatie is voltooid. De werkelijke clientinstallatie wordt na de vertraging vervolgens beheerd door de computer. Nadat de clientupgrade is voltooid, valideert u de installatie door het bestand **/var/opt/microsoft/scxcm.log** op clientcomputer te controleren. Controleer of de client is geïnstalleerd en communiceert met de site door Details voor de client te bekijken in het knoop punt **apparaten** van de werk ruimte **activa en naleving** in de Configuration Manager-console.  

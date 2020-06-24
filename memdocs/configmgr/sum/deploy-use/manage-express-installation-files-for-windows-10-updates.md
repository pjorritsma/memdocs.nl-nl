---
title: Updates voor Windows 10 Express beheren
titleSuffix: Configuration Manager
description: Configuration Manager ondersteunt bestanden voor snelle installatie van Windows 10, die kleinere down loads en snellere installatie tijden bieden op clients.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/02/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: ff018bc81ecdb3d11ebb71f1850804a5679c67f7
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746575"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Bestanden voor snelle installatie voor Windows 10-updates beheren

Configuration Manager ondersteunt bestanden voor snelle installatie voor Windows 10-updates. Configureer de client zo dat alleen de wijzigingen worden gedownload tussen de cumulatieve kwaliteits update voor Windows 10 van de huidige maand en de update van de vorige maand. Zonder bestanden voor snelle installatie, downloaden Configuration Manager-clients elke maand de volledige cumulatieve update van Windows 10, inclusief alle updates van de vorige maanden. Het gebruik van bestanden voor snelle installatie biedt kleinere down loads en snellere installatie tijden op clients.

Zie [Windows 10-update levering optimaliseren](optimize-windows-10-update-delivery.md)voor meer informatie over het gebruik van Configuration Manager voor het beheren van update-inhoud om actueel te blijven met Windows 10.  


> [!IMPORTANT]  
> De OS-client ondersteuning is beschikbaar in Windows 10, versie 1607, met een update voor de Windows Update-Agent. Deze update is opgenomen in de updates die zijn uitgebracht op 11 april 2017. Zie [ondersteuning voor artikel 4015217](https://support.microsoft.com/kb/4015217)voor meer informatie over deze updates. Toekomstige updates worden gebruikt voor kleinere down loads. Eerdere versies van Windows 10 en Windows 10 versie 1607 zonder deze update ondersteunen geen snelle installatie bestanden.  


## <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>De site inschakelen voor het downloaden van bestanden voor snelle installatie voor Windows 10-updates
Als u wilt beginnen met het synchroniseren van de meta gegevens voor Windows 10 Express-installatie bestanden, schakelt u deze in de eigenschappen van het software-update punt in.  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Selecteer de centrale beheer site of de zelfstandige primaire site.  

3. Klik in het lint op **site onderdelen configureren**en klik vervolgens op **Software-update punt**. Ga naar het tabblad **Update bestanden** en selecteer **beide volledige bestanden downloaden voor alle goedgekeurde updates en bestanden voor snelle installatie voor Windows 10**.

> [!NOTE]    
> U kunt het onderdeel Software-update punt niet configureren om *alleen* snelle updates te downloaden.  De site downloadt de bestanden voor snelle installatie naast de volledige bestanden. Dit verhoogt de hoeveelheid inhoud die is opgeslagen in de inhouds bibliotheek en wordt gedistribueerd naar en opgeslagen op uw distributie punten.

> [!Tip]  
> Controleer de eigenschap **grootte op schijf** van het bestand om na te gaan welke ruimte op de schijf door het bestand wordt gebruikt. De eigenschap grootte op schijf moet aanzienlijk kleiner zijn dan de grootte waarde. Zie [Veelgestelde vragen voor het optimaliseren van Windows 10 update delivery](optimize-windows-10-update-delivery.md#bkmk_faq)voor meer informatie.  


## <a name="enable-clients-to-download-and-install-express-installation-files"></a>Clients inschakelen voor het downloaden en installeren van bestanden voor snelle installatie
Als u ondersteuning voor bestanden voor snelle installatie op clients wilt inschakelen, schakelt u bestanden voor snelle installatie in de **Software-update** groep van client instellingen in. Met deze instelling wordt een nieuwe HTTP-listener gemaakt waarmee wordt geluisterd naar aanvragen voor het downloaden van snelle installatie bestanden op de poort die u opgeeft.

> [!NOTE]    
> Dit is een lokale poort die door clients wordt gebruikt om te Luis teren naar aanvragen van Delivery Optimization of Background Intelligent Transfer Service (BITS) om snelle inhoud vanaf het distributie punt te downloaden. U hoeft deze poort niet te openen op firewalls, omdat al het verkeer op de lokale computer.  

Zodra u client instellingen hebt geïmplementeerd om deze functionaliteit op de client in te scha kelen, wordt geprobeerd de verschillen te downloaden tussen de cumulatieve update voor Windows 10 van de huidige maand en de update van de vorige maand. Clients moeten een versie van Windows 10 uitvoeren die bestanden voor snelle installatie ondersteunt.  

1. Schakel ondersteuning voor bestanden voor snelle installatie in via de eigenschappen van het onderdeel Software-update punt (vorige procedure).  

2. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer **client instellingen**.  

3. Selecteer de juiste client instellingen en klik op **Eigenschappen** op het lint.  

4. Selecteer de groep met **software-updates** . Stel deze optie in op **Ja** om de **installatie van snelle updates op clients in te scha kelen**. Configureer de **poort die wordt gebruikt voor het downloaden van inhoud voor snelle updates** met de poort die wordt gebruikt door de HTTP-listener op de client.
    - In versie 1902 is de **installatie van snelle updates op clients** zodanig gewijzigd dat **clients Delta-inhoud kunnen downloaden wanneer deze beschikbaar zijn**.
    - In versie 1902, **poort die wordt gebruikt voor het downloaden van inhoud voor snelle updates** is gewijzigd in **poort die door clients wordt gebruikt om aanvragen voor Delta-inhoud te ontvangen**.
    

## <a name="next-steps"></a>Volgende stappen

[Software-updates implementeren](deploy-software-updates.md)

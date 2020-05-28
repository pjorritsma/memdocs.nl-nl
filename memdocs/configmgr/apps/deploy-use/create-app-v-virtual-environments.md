---
title: Virtuele app-V-omgevingen maken
titleSuffix: Configuration Manager
description: Maak virtuele omgevingen met micro soft Application Virtualization zodat apps gegevens met elkaar kunnen delen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2280218d3d237f91f0db3150dbc2031bad3e1816
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710417"
---
# <a name="create-app-v-virtual-environments-in-configuration-manager"></a>Virtuele app-V-omgevingen maken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In een virtuele omgeving van micro soft Application Virtualization (app-V) in Configuration Manager kunnen geïmplementeerde virtuele toepassingen hetzelfde bestands systeem en REGI ster delen op client Windows-Pc's. In tegens telling tot standaard virtuele toepassingen kunnen deze toepassingen gegevens met elkaar delen. Virtuele omgevingen worden op client computers gemaakt of gewijzigd wanneer de toepassing wordt geïnstalleerd of wanneer clients vervolgens hun geïnstalleerde toepassingen evalueren. U kunt deze toepassingen zodanig rangschikken dat wanneer meerdere toepassingen proberen een bestandssysteem of registerwaarde te wijzigen, de toepassing met het hoogste rangnummer prioriteit krijgt.  

> [!IMPORTANT]  
>  Vertrouw niet op virtuele app-V-omgevingen om beveiligings beveiliging te bieden, zoals schadelijke software.  

 Gebruik de volgende procedure om een virtuele app-V-omgeving te maken in Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Een virtuele app-V-omgeving maken  

1.  Kies in de Configuration Manager-console **software bibliotheek**  >  **toepassings beheer**  >  **App-V virtuele omgevingen**.  

3.  Klik op het tabblad **Start** in de groep **maken** op **virtuele omgeving maken**.  

4.  Voer in het dialoog venster **virtuele omgeving maken** de volgende gegevens in:  

    -   **Naam**.  Voer een unieke naam in voor de virtuele omgeving (Maxi maal 128 tekens).  

    -   **Beschrijving**. Beschrijving Voer een beschrijving in voor de virtuele omgeving.  

5.  Kies **toevoegen**om een nieuw implementatie type toe te voegen aan de virtuele omgeving. U moet minstens één implementatietype toevoegen.  

6.  Geef in het dialoog venster **toepassingen toevoegen** een **groeps naam** op (Maxi maal 128 tekens). U gebruikt deze naam om te verwijzen naar de groep toepassingen die u toevoegt aan de virtuele omgeving.  

7.  Kies **toevoegen**, selecteer de app-V 5-toepassingen en implementatie typen die u wilt toevoegen aan de groep en kies vervolgens **OK**.  

8.  In het dialoog venster **toepassingen toevoegen** kunt u **volg orde verhogen** of **volg orde verlagen** om de toepassing in te stellen die prioriteit krijgt als meerdere toepassingen het bestands systeem of register instellingen in dezelfde virtuele omgeving proberen te wijzigen.  

9. Klik op **OK**om terug te keren naar het dialoog venster **virtuele omgeving maken** .  

10. Wanneer u klaar bent met het toevoegen van groepen, kiest u **OK** om de virtuele omgeving te maken. De nieuwe virtuele omgeving wordt weer gegeven in het knoop punt **virtuele omgevingen van app-V** van de Configuration Manager-console. U kunt de status van uw virtuele omgevingen bewaken met behulp van het status rapport van de virtuele omgeving van app-V.  

    > [!NOTE]  
    >  De virtuele omgeving wordt op client-Pc's toegevoegd of gewijzigd wanneer de toepassing wordt geïnstalleerd of wanneer de geïnstalleerde toepassingen door de client worden geëvalueerd.  

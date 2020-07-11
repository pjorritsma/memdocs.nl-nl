---
title: Configuratiebasislijnen implementeren
titleSuffix: Configuration Manager
description: Implementeer configuratie basislijnen voor het definiëren van implementaties van configuratie basislijn en het toevoegen of verwijderen van configuratie basislijnen uit implementaties.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 94a5d0af5636236ffba3f15c05823ead083f2948
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240266"
---
# <a name="how-to-deploy-configuration-baselines-in-configuration-manager"></a>Configuratie basislijnen implementeren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuratie basislijnen in Configuration Manager moeten worden geïmplementeerd voor een of meer verzamelingen van gebruikers of apparaten voordat client apparaten in deze verzamelingen hun compatibiliteit met de configuratie basislijn kunnen beoordelen.  

Gebruik de **Configuratiebasislijnen implementeren** in het dialoogvenster voor het definiëren van implementaties van configuratiebasislijnen, waaronder het toevoegen aan of verwijderen van configuratiebasislijnen uit implementaties naast het opgeven van het evaluatieschema.  

## <a name="deploy-a-configuration-baseline"></a>Een configuratiebasislijn implementeren  

1.  Klik in de Configuration Manager-console op **activa en naleving**  >  **instellingen**  >  **configuratie basislijnen**.  

3.  Selecteer in de lijst **Configuratiebasislijnen** de configuratiebasislijn die u wilt implementeren en klik vervolgens op het tabblad **Start** in de groep **Implementatie** op **Implementeren**.  

4.  Selecteer in het dialoogvenster **Configuratiebasislijnen implementeren** de configuratiebasislijnen die u wilt implementeren in de lijst **Beschikbare configuratiebasislijnen** . Klik op **Toevoegen** om ze toe te voegen aan de lijst **Geselecteerde configuratiebasislijnen** .  

    > [!IMPORTANT]  
    >  Als u een configuratie-item wijzigt dat is toegevoegd aan een geïmplementeerde configuratiebasislijn, wordt het gewijzigde configuratie-item pas op de volgende geplande evaluatietijd op compatibiliteit geëvalueerd.  

5.  Geef de volgende aanvullende informatie op:  

    -   **Regels** die niet compliant zijn herstellen, worden automatisch hersteld. alle regels die niet compatibel zijn voor Windows Management INSTRUMENTATION (WMI), het REGI ster, scripts en alle instellingen voor mobiele apparaten die zijn Inge schreven door Configuration Manager, worden door.  

    -   **Herstel toestaan buiten het onderhoudsvenster** : Als er een onderhoudsvenster is geconfigureerd voor de verzameling waarnaar u de configuratiebasislijn implementeert, schakelt u deze optie in om de waarde buiten het onderhoudsvenster te laten herstellen met de instellingen voor naleving. Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.  

6.  **Waarschuwing genereren** : Hiermee configureert u een waarschuwing die wordt gegenereerd als de naleving van de configuratie basislijn op een opgegeven datum en tijd minder is dan een opgegeven percentage. U kunt tevens opgeven of u een melding naar System Center Operations Manager wilt verzenden.  

7.  **Verzameling** : klik op **Bladeren** om de verzameling te selecteren waarvoor u de configuratiebasislijn wilt implementeren.  

8.  **Geef het evaluatie schema voor compatibiliteit op voor deze configuratie basislijn** Hiermee geeft u het schema op waarmee de geïmplementeerde configuratie basislijn wordt geëvalueerd op client computers. U kunt een eenvoudige of een aangepaste planning opgeven.  

    > [!NOTE]  
    >  Als de configuratiebasislijn wordt geïmplementeerd op een computer, wordt deze voor naleving binnen twee uur na het begintijdstip dat u plant geëvalueerd. Als de configuratiebasislijn wordt geïmplementeerd voor een gebruiker, wordt de naleving geëvalueerd wanneer de gebruiker zich aanmeldt.  

9. Klik op **OK** om het dialoogvenster **Configuratiebasislijnen implementeren** te sluiten en de implementatie te maken. Zie [nalevings instellingen controleren](monitor-compliance-settings.md)voor meer informatie over het bewaken van de implementatie.  

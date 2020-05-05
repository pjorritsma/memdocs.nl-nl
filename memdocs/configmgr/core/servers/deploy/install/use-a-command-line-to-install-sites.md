---
title: Installatie vanaf de opdracht regel
titleSuffix: Configuration Manager
description: Meer informatie over het uitvoeren van Configuration Manager Setup vanaf een opdracht prompt voor een groot aantal site-installaties.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c46e7f4dde0fb4719daf0f5c1f1293f627063f2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717956"
---
# <a name="use-a-command-line-to-install-configuration-manager-sites"></a>Een opdracht regel gebruiken om Configuration Manager-sites te installeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

 U kunt Configuration Manager Setup uitvoeren vanaf een opdracht prompt om diverse site typen te installeren.

## <a name="supported-tasks-for-command-line-installations"></a>Ondersteunde taken voor opdracht regel installaties
 Deze methode voor het uitvoeren van Setup ondersteunt de volgende site-installatie-en site-onderhouds taken:

- **Een centrale beheer site of primaire site installeren vanaf een opdracht prompt**  
  [Opdracht regel opties voor Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md) weer geven

- **De talen wijzigen die worden gebruikt op een centrale beheer site of primaire site**  
   Als u de talen die op een site zijn geïnstalleerd, wilt wijzigen vanaf een opdracht prompt (inclusief talen voor mobiele apparaten), moet u het volgende doen:  

  - Voer Setup uit ** &lt;vanuit\>ConfigMgrInstallationPath \Bin\X64** op de site server,
  - Gebruik de opdracht regel optie **/MANAGELANGS**
  - Geef een taal script bestand op dat de talen specificeert die u wilt toevoegen of verwijderen,  

    Gebruik bijvoorbeeld de volgende opdracht syntaxis: **setupwpf. exe/MANAGELANGS &lt;taal script bestand\> **  

    Als u het taal script bestand wilt maken, gebruikt u de informatie in de [opdracht regel opties voor het beheren van talen](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

- **Een installatiescriptbestand gebruiken voor site-installaties of site recovery zonder toezicht**  
   U kunt het installatie programma uitvoeren vanaf een opdracht prompt met behulp van een installatie script en u een installatie zonder toezicht van de site uitvoert. U kunt deze optie ook gebruiken om een site te herstellen.    

   Een script gebruiken met Setup:  

  - Voer Setup uit met de opdracht regel optie **/script** en geef een script bestand op.  

  - Het script bestand moet worden geconfigureerd met de vereiste sleutels en waarden.  

    Voor een installatie zonder toezicht van een centrale beheer site of primaire site, moet het script bestand de volgende secties bevatten:  

  - Identificatie    
  - Opties    
  - SQLConfigOptions    
    -   HierarchyOptions    
  - Hierarchyoptions   

    Als u een site wilt herstellen, moet u ook de volgende secties van het script bestand toevoegen:  

  - Identificatie  
  - Herstel

Zie [site Recovery zonder toezicht voor Configuration Manager](../../manage/unattended-recovery.md)voor meer informatie.  

Zie [script bestand sleutels voor installatie zonder](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended)toezicht voor een lijst met sleutels en waarden die moeten worden gebruikt in een script bestand voor installatie zonder toezicht.  

## <a name="about-the-command-line-script-file"></a>Over het opdracht regel script bestand  
 Voor installaties zonder toezicht van Configuration Manager kunt u het installatie programma uitvoeren met de opdracht regel optie **/script**en een script bestand opgeven dat installatie opties bevat. De volgende taken worden ondersteund met behulp van deze methode:  

-   Een centrale beheer site installeren  
-   Een primaire site installeren  
-   Een Configuration Manager-console installeren  
-   Een site herstellen  

> [!NOTE]  
>  U kunt het script bestand voor installatie zonder toezicht niet gebruiken om een evaluatie site bij te werken naar een gelicentieerde installatie van Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>De naam van de CDLatest-sleutel
Wanneer u media gebruikt vanaf de CD. Meest recente map voor het uitvoeren van een script installatie van de volgende vier installatie opties moet uw script de sleutel **CDLatest** bevatten met de waarde **1**:
- Een nieuwe centrale beheer site installeren
- Een nieuwe primaire site installeren
- Een centrale beheer site herstellen
- Een primaire site herstellen

Deze waarde wordt niet ondersteund voor gebruik met installatie media die u van de micro soft Volume License-site ontvangt.
Zie [opdracht regel opties](command-line-options-for-setup.md) voor informatie over het gebruik van deze sleutel naam in het script bestand.



### <a name="create-the-script"></a>Het script maken
Het installatie script wordt automatisch gemaakt wanneer u [Setup uitvoert om een site te installeren met behulp van de gebruikers interface](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Wanneer u de instellingen op de pagina **samen vatting** van de wizard bevestigt, gebeurt het volgende:  

-   Het installatie programma maakt het script **%temp%\ConfigMgrAutoSave.ini**.  U kunt de naam van dit bestand wijzigen voordat u het gebruikt, maar het moet de bestands extensie. ini behouden.  
-   Het script voor installatie zonder toezicht bevat de instellingen die u hebt geselecteerd in de wizard.  
-   Nadat het script is gemaakt, kunt u het script wijzigen om andere sites in uw hiërarchie te installeren.  
-   U kunt dit script vervolgens gebruiken voor het uitvoeren van een installatie zonder toezicht van Configuration Manager.  

Dit script bestand bevat dezelfde informatie die wordt gevraagd door de installatie wizard, behalve dat er geen standaard instellingen zijn.   
U moet alle waarden opgeven voor de installatie sleutels die van toepassing zijn op het type installatie dat u gebruikt.   

Wanneer het script voor installatie zonder toezicht wordt gemaakt, wordt de waarde van de product code ingevuld die u tijdens de installatie opgeeft. Dit kan een geldige product code zijn of een **Eval** wanneer u een evaluatie versie van Configuration Manager installeert. De waarde van de product sleutel in het script wordt ingevuld, zodat de controle van vereisten kan worden voltooid.   

Wanneer het installatie programma de daad werkelijke installatie van de site start, wordt het automatisch gemaakte script opnieuw geschreven om de waarde van de product code te wissen in het script dat wordt gemaakt. Voordat u het script gebruikt voor een installatie zonder toezicht van een nieuwe site, kunt u het script bewerken om een geldige product code op te geven of om een evaluatie-installatie van Configuration Manager op te geven.  

### <a name="section-names-key-names-and-values"></a>Sectie namen, sleutel namen en waarden
Het script bevat sectienamen, sleutelnamen en waarden. Let op de volgende informatie:
-   De vereiste sectie sleutel namen variëren afhankelijk van het installatie type dat u wilt uitvoeren van scripts.
-   De volg orde van de sleutels binnen secties en de volg orde van de secties in het bestand is niet belang rijk.     
-   De sleutels zijn niet hoofdletter gevoelig.  
-   Wanneer u waarden voor sleutels opgeeft, moet de naam van de sleutel worden gevolgd door een gelijkteken (=) en de waarde voor de sleutel.    

> [!TIP]  
>  Zie [opdracht regel opties voor installatie en scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md)voor een overzicht van de volledige set opties.  

## <a name="use-the-script-setup-command-line-option"></a>De opdracht regel optie voor de installatie van/SCRIPT gebruiken

-   U moet een installatie script bestand gebruiken en de bestands naam opgeven na de opdracht regel optie voor de installatie van **/script** . Let op de volgende informatie:   
    -   De naam van het bestand moet de bestandsnaam extensie **. ini** hebben.  
    -   Wanneer u verwijst naar het installatie script bestand op de opdracht regel, moet u het volledige pad naar het bestand opgeven. Als uw installatie-initialisatie bestand bijvoorbeeld Setup. ini heet en het is opgeslagen in de map C:\Setup, typt u het volgende achter de opdracht prompt: **Setup/script c:\setup\setup.ini**.  

-   Het account waarmee de installatie wordt uitgevoerd, moet **beheerders** rechten op de computer hebben. Wanneer u het installatie programma uitvoert met het script zonder toezicht, opent u het opdracht prompt venster met de optie **als administrator uitvoeren** .   

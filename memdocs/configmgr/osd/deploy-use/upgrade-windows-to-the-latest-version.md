---
title: Een upgrade uitvoeren naar Windows 10
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van Configuration Manager om een besturings systeem te upgraden van Windows 7 of hoger naar Windows 10.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a9ed8e1ece27117993761a3ce52c462e94e9f79a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124770"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>Windows upgraden naar de nieuwste versie met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel worden de stappen beschreven in Configuration Manager het besturings systeem op een computer te upgraden. U kunt kiezen uit verschillende implementatiemethoden, zoals zelfstandige media of Software Center. Het in-place upgrade scenario heeft de volgende functies:  

- Voert een upgrade van het besturings systeem uit naar Windows 10 of Windows Server 2016 en hoger

- Hiermee blijven de toepassingen, instellingen en gebruikers gegevens op de computer behouden

- Heeft geen externe afhankelijkheden, zoals de Windows ADK

- Is sneller en flexibeler dan traditionele besturingssysteem implementaties

> [!Note]  
> De taken reeks Windows 10 in-place upgrade ondersteunt de implementatie voor clients op Internet die worden beheerd via de [Cloud beheer gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md). Met deze mogelijkheid kunnen externe gebruikers eenvoudiger een upgrade uitvoeren naar Windows 10 zonder dat ze verbinding hoeven te maken met het intranet. Zie [Deploying Windows 10 in-place upgrade via CMG](deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)voor meer informatie. <!-- 1357149 -->


## <a name="supported-versions"></a>Ondersteunde versies

### <a name="upgrade-version"></a>Upgrade versie

Alleen OS-upgrade pakketten maken om te upgraden naar de volgende versies van het besturings systeem:

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>Oorspronkelijke versie

Op apparaten moet een van de volgende versies van het besturings systeem worden uitgevoerd om een upgrade uit te voeren voor een besturingssysteem update:

#### <a name="windows-client"></a>Windows-client

- Windows 7
- Windows 8.1
- Een eerdere versie van Windows 10. U kunt bijvoorbeeld Windows 10 versie 1809 bijwerken naar Windows 10, versie 1903.  

Zie [upgrade paden voor Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-upgrade-paths)voor meer informatie.

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- Een eerdere versie van Windows Server 2016
- Een eerdere versie van Windows Server 2019

Zie [Windows server 2016 ondersteunde upgrade paden](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016) en [Windows Server Upgrade Center](https://aka.ms/upgradecenter)voor meer informatie over ondersteunde upgrade paden voor Windows Server.


## <a name="plan"></a><a name="BKMK_Plan"></a>Fonds  

### <a name="task-sequence-requirements-and-limitations"></a>Vereisten en beperkingen voor taken reeksen

Bekijk de volgende vereisten en beperkingen voor de taken reeks om een besturings systeem bij te werken, zodat u zeker weet dat het voldoet aan uw behoeften:  

- Voeg alleen taken reeks stappen toe die betrekking hebben op de kern taak van het bijwerken van het besturings systeem. Deze stappen omvatten voornamelijk het installeren van pakketten, toepassingen of updates. Gebruik ook stappen die opdracht regels uitvoeren, Power shell of dynamische variabelen instellen.  

- Controleer Stuur Programma's en toepassingen die op computers zijn geïnstalleerd. Zorg ervoor dat de Stuur Programma's compatibel zijn met Windows 10 voordat u de upgrade taken reeks implementeert.  

De volgende taken zijn niet compatibel met de in-place upgrade. Hiervoor moet u traditionele besturingssysteem implementaties gebruiken:  

- Het domein lidmaatschap van de computer wijzigen of de lokale groep Administrators bijwerken.  

- Implementatie van een fundamentele wijziging op de computer, zoals:

  - Schijf partities wijzigen
  - De systeem architectuur van x86 naar x64 wijzigen
  - UEFI implementeren. (Zie voor meer informatie over een mogelijke optie [converteren van BIOS naar UEFI tijdens een in-place upgrade](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).)
  - De taal van het basis besturingssysteem wijzigen  

- U hebt aangepaste vereisten, waaronder het gebruik van een aangepaste basis installatie kopie, het gebruik van schijf versleuteling van derden of het vereisen van WinPE offline bewerkingen.  

### <a name="infrastructure-requirements"></a>Vereisten voor de infrastructuur  

De enige vereiste voor het upgrade scenario is dat er een distributie punt beschikbaar is. Distribueer het upgrade pakket van het besturings systeem en eventuele andere pakketten die u in de taken reeks opneemt. Zie voor meer informatie [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).


## <a name="configure"></a><a name="BKMK_Configure"></a>Geconfigureerd  

### <a name="prepare-the-os-upgrade-package"></a>Het upgrade pakket voor het besturings systeem voorbereiden  

Het Windows 10-upgrade pakket bevat de bron bestanden die nodig zijn om het besturings systeem op de doel computer te upgraden. Het upgrade pakket moet dezelfde editie, architectuur en taal zijn als de clients die u bijwerkt. Zie [upgrade pakketten voor besturings systemen beheren](../get-started/manage-operating-system-upgrade-packages.md)voor meer informatie.  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Een taken reeks maken om het besturings systeem bij te werken  

Volg de stappen in [een taken reeks maken om een besturings systeem](create-a-task-sequence-to-upgrade-an-operating-system.md) bij te werken om de upgrade van het besturings systeem te automatiseren.  

> [!NOTE]  
> Voor het maken van een taken reeks om een besturings systeem te upgraden naar Windows 10, gebruikt u doorgaans de stappen in [een taken reeks maken om een besturings systeem bij te werken](create-a-task-sequence-to-upgrade-an-operating-system.md). De taken reeks bevat de stap **besturings systeem bijwerken** , evenals aanvullende aanbevolen stappen en groepen om het end-to-end upgrade proces af te handelen.
>
> U kunt een aangepaste taken reeks maken en de stap [besturings systeem bijwerken](../understand/task-sequence-steps.md#BKMK_UpgradeOS) toevoegen. Dit is de enige stap die is vereist om het besturings systeem te upgraden naar Windows 10. Als u deze methode kiest om de upgrade te volt ooien, voegt u ook de stap [computer opnieuw opstarten](../understand/task-sequence-steps.md#BKMK_RestartComputer) toe na de stap **besturings systeem bijwerken** . Zorg ervoor dat u de **standaard besturingssysteem** instelling gebruikt om de computer opnieuw op te starten in het geïnstalleerde besturings systeem en niet met Windows PE.  


## <a name="deploy"></a><a name="BKMK_Deploy"></a>Zetten  

Gebruik een van de volgende implementatie methoden om het besturings systeem te implementeren:  

- [Windows met Software Center via het netwerk implementeren](use-software-center-to-deploy-windows-over-the-network.md)  

- [Zelfstandige media gebruiken om Windows te implementeren zonder gebruik van het netwerk](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  > [!IMPORTANT]  
  > Wanneer u zelfstandige media gebruikt, moet u een opstart installatie kopie in de taken reeks toevoegen. Deze configuratie zorgt ervoor dat de taken reeks beschikbaar is in de wizard taken reeks media.


## <a name="monitor"></a>Controleren  

Zie [implementaties van besturings systemen bewaken](monitor-operating-system-deployments.md)voor het controleren van de taken reeks implementatie om het besturings systeem bij te werken.  

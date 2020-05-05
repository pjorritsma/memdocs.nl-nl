---
title: Inleiding tot besturingssysteemimplementaties
titleSuffix: Configuration Manager
description: Inzicht in de concepten voordat u besturings systemen in uw Configuration Manager omgeving implementeert.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d53ab2221e3ee936f9b09592a7c7b383b200c928
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720385"
---
# <a name="introduction-to-operating-system-deployment-in-configuration-manager"></a>Inleiding tot implementatie van besturings systemen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt Configuration Manager gebruiken om besturings systemen op een aantal verschillende manieren te implementeren. Gebruik de informatie in deze sectie om inzicht te krijgen in het implementeren van besturings systemen en het automatiseren van taken. 

##  <a name="the-operating-system-deployment-process"></a><a name="BKMK_OSDeploymentProcess"></a> Het proces van de besturingssysteemimplementatie  
 Configuration Manager biedt verschillende methoden die u kunt gebruiken om een besturings systeem te implementeren. Ongeacht de implementatiemethode die u gebruikt, zijn er verschillende acties die u moet uitvoeren.  

-   Stel vast welke Windows-apparaatstuurprogramma's vereist zijn om de opstartinstallatiekopie op te starten en de installatiekopie van het besturingssysteem te installeren die u moet implementeren.  

-   Kies de opstartinstallatiekopie die u wilt gebruiken om de doelcomputer te starten.  

-   Gebruik een takenreeks om een installatiekopie van het besturingssysteem vast te leggen dat u wilt implementeren. U kunt ook een standaardinstallatiekopie van het besturingssysteem gebruiken.  

-   Distribueer de opstartinstallatiekopie, de installatiekopie van het besturingssysteem en eventueel gerelateerde inhoud naar een distributiepunt.  

-   Maak een takenreeks met de stappen voor het implementeren van de opstartinstallatiekopie en de installatiekopie van het besturingssysteem.  

-   Implementeer de takenreeks voor een verzameling computers  

-   Controleer de implementatie.  

##  <a name="operating-system-deployment-scenarios"></a><a name="BKMK_OSDScenarios"></a> Implementatiescenario's voor het besturingssysteem  
 Er zijn veel implementatie scenario's voor besturings systemen in Configuration Manager die u kunt kiezen, afhankelijk van uw omgeving en het doel van de installatie van het besturings systeem.  U kunt bijvoorbeeld de harde schijf van een bestaande computer in partities indelen en formatteren met een nieuwe versie van Windows of voor Windows een upgrade uitvoeren naar de nieuwste versie. Bekijk [scenario's voor het implementeren van ENTER prise-besturings systemen](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)om u te helpen bij het bepalen van de implementatie methode die aan uw behoeften voldoet.  U kunt kiezen uit de volgende implementatiescenario's voor besturingssystemen:  

-   [Windows bijwerken naar de laatste versie](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Een bestaande computer vernieuwen met een nieuwe versie van Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Een bestaande computer vervangen en de instellingen overzetten](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="methods-to-deploy-operating-systems"></a><a name="BKMK_OSDMethods"></a> Methoden voor het implementeren van besturingssystemen  
 Er zijn verschillende methoden die u kunt gebruiken om besturings systemen te implementeren op Configuration Manager-client computers.  

- **Implementaties met gebruik van PXE**: bij implementaties waarbij gebruik wordt gemaakt van PXE kunnen clientcomputers een implementatie via het netwerk aanvragen. In deze implementatiemethode worden de installatiekopie van het besturingssysteem en een opstartinstallatiekopie van Windows PE verzonden naar een distributiepunt dat is geconfigureerd om PXE-opstartaanvragen te accepteren. Zie [PXE gebruiken om Windows via het netwerk te implementeren met Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie.  

- **Besturingssystemen beschikbaar maken in Software Center**: u kunt een besturingssysteem implementeren en beschikbaar maken in Software Center. Configuration Manager-clients kunnen de installatie van het besturings systeem initiëren vanuit software Center. Zie [een bestaande computer vervangen en de instellingen overzetten](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)voor meer informatie.  

- **Multicast-implementaties**: met multicast-implementaties wordt het gebruik van netwerkbandbreedte beperkt door gegevens gelijktijdig te verzenden naar meerdere clients in plaats van een kopie van de gegevens naar elke client via een afzonderlijke verbinding te verzenden. In deze implementatiemethode wordt de installatiekopie van het besturingssysteem verzonden naar een distributiepunt. Dit implementeert op zijn beurt de installatiekopie wanneer clientcomputers de implementatie aanvragen. Zie [multi cast gebruiken om Windows via het netwerk te implementeren](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)voor meer informatie.  

- **Implementaties met opstartbare media**: bij implementaties met opstartbare media kunt u het besturingssysteem implementeren wanneer de doelcomputer wordt opgestart. De doelcomputer haalt de takenreeks, de installatiekopie van het besturingssysteem en alle andere vereiste inhoud van het netwerk op tijdens het opstarten. Omdat die inhoud zich niet op de media bevindt, kunt u de inhoud bijwerken zonder de media opnieuw te moeten maken. Zie [opstart bare media maken](../deploy-use/create-bootable-media.md)voor meer informatie.  

- **Implementaties met zelfstandige media**: bij implementaties met zelfstandige media kunt u besturingssystemen implementeren in de volgende situaties:  

  - In omgevingen waar het niet praktisch is om een installatiekopie van een besturingssysteem of andere grote pakketten over het netwerk te kopiëren.  

  - In omgevingen zonder netwerkverbinding of de met lage netwerkbandbreedte.  

    Zie voor meer informatie [maken van zelfstandige media](../deploy-use/create-stand-alone-media.md).  

- **Implementaties met vooraf geplaatste media**: bij implementaties met vooraf geplaatste media kunt u een besturingssysteem implementeren op een computer die nog niet volledig is ingericht. De vooraf geplaatste media is een WIM-bestand (Windows Imaging Format) dat door de fabrikant kan worden geïnstalleerd op een bare-metal computer of in een Enter prise staging Center dat geen verbinding heeft met de Configuration Manager omgeving.  

   Later in de Configuration Manager omgeving wordt de computer opgestart met behulp van de opstart installatie kopie van de media en vervolgens verbinding maken met het site beheer punt voor beschik bare taken reeksen die het download proces volt ooien. Deze implementatiemethode kan het netwerkverkeer verminderen omdat de opstartinstallatiekopie en de installatiekopie van het besturingssysteem zich al op de doelcomputer bevinden. U kunt toepassingen, pakketten en stuurprogrammapakketten opgeven die in de voorbereide media moeten worden opgenomen. Zie voor [bereide media maken](../deploy-use/create-prestaged-media.md)voor meer informatie.  

##  <a name="boot-images"></a><a name="BKMK_BootImages"></a>Installatie kopieën  
 Een opstart installatie kopie in Configuration Manager is een Windows PE-installatie kopie (WinPE) die wordt gebruikt tijdens de implementatie van een besturings systeem. Opstartinstallatiekopieën worden gebruikt om een computer op te starten in WinPE. Dit is een minimaal besturingssysteem met beperkte onderdelen en services dat de doelcomputer voorbereidt voor een Windows-installatie. Configuration Manager biedt twee opstart installatie kopieën: één ter ondersteuning van x86-platformen en één ter ondersteuning van x64-platformen. Deze worden beschouwd als de standaardopstartinstallatiekopieën. Opstart installatie kopieën die u maakt en toevoegt aan Configuration Manager worden beschouwd als aangepaste installatie kopieën. Standaard installatie kopieën kunnen automatisch worden vervangen wanneer u Configuration Manager bijwerkt. Zie [Opstartinstallatiekopieën beheren met System Center Configuration Manager](../get-started/manage-boot-images.md) voor meer informatie over opstartinstallatiekopieën.  

##  <a name="operating--system-images"></a><a name="BKMK_OSImages"></a> Installatiekopieën van besturingssystemen:  
 Installatiekopieën van besturingssystemen in Configuration Manager worden opgeslagen met de WIM-bestandsindeling (Windows Imaging). Ze omvatten een gecomprimeerde verzameling referentiebestanden en -mappen die zijn vereist om een besturingssysteem correct te installeren en te configureren op een computer. Alle implementatiescenario's voor besturingssystemen vereisen dat u een installatiekopie van een besturingssysteem selecteert. U kunt de standaardinstallatiekopie van een besturingssysteem gebruiken of een installatiekopie van het besturingssysteem maken van een referentiecomputer die u configureert. Zie [installatie kopieën van besturings systemen beheren](../get-started/manage-operating-system-images.md)voor meer informatie.  

##  <a name="operating-system-upgrade-packages"></a><a name="BKMK_OSUpgradePackages"></a> Upgradepakketten voor besturingssysteem  
 Upgradepakketten voor besturingssystemen worden gebruikt om een upgrade uit te voeren voor een besturingssysteem en zijn besturingssysteemimplementaties die met een installatieprogramma worden gestart. U importeert upgrade pakketten voor het besturings systeem naar Configuration Manager vanaf een DVD of een gekoppeld ISO-bestand. Zie [upgrade pakketten voor besturings systemen beheren](../get-started/manage-operating-system-upgrade-packages.md)voor meer informatie.  

##  <a name="media-to-deploy-operating-systems"></a><a name="BKMK_OSDMedia"></a> Media voor het implementeren van besturingssystemen  
 U kunt verschillende soorten media maken die kunnen worden gebruikt om besturingssystemen te implementeren. Dit omvat vastlegmedia die wordt gebruikt voor het vastleggen van installatiekopieën van een besturingssysteem en van zelfstandige, voorbereide en opstartbare media die wordt gebruikt om een besturingssysteem te implementeren. Door media te gebruiken, kunt u besturings systemen implementeren op computers die geen netwerk verbinding hebben of die een lage bandbreedte verbinding met uw Configuration Manager-site hebben. Zie [taken reeks media maken](../deploy-use/create-task-sequence-media.md)voor meer informatie over het gebruik van media.  

##  <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a>Apparaatstuurprogramma's  
 U kunt apparaatstuurprogramma's installeren op doelcomputers zonder ze op te nemen in de installatiekopie van het besturingssysteem die wordt geïmplementeerd. Configuration Manager biedt een stuurprogrammacatalogus die verwijzingen bevat naar alle apparaatstuurprogramma's die u in Configuration Manager importeert. De stuurprogrammacatalogus bevindt zich in de werkruimte **Softwarebibliotheek** en bestaat uit twee knooppunten: **Stuurprogramma's** en **Stuurprogrammapakketten**. Het knooppunt **Stuurprogramma's** geeft alle stuurprogramma's weer die u in de stuurprogrammacatalogus hebt geïmporteerd. U kunt dit knooppunt gebruiken om de details over elk geïmporteerd stuurprogramma te detecteren, om het stuurprogrammapakket of de opstartinstallatiekopie van een stuurprogramma te wijzigen, om een stuurprogramma in of uit te schakelen, en meer. Zie [Stuur Programma's beheren](../get-started/manage-drivers.md)voor meer informatie.  

##  <a name="save-and-restore-user-state"></a><a name="BKMK_OSDUserState"></a> De gebruikersstatus opslaan en terugzetten  
 Tijdens het implementeren van besturingssystemen kunt u de gebruikersstatus van de doelcomputer opslaan, het besturingssysteem implementeren en vervolgens de gebruikersstatus herstellen na de implementatie van de besturingssystemen. Dit proces wordt doorgaans gebruikt wanneer u het besturings systeem installeert op een Configuration Manager-client computer.  

 De gebruikersstatusinformatie wordt vastgelegd en hersteld met takenreeksen. Als de gebruikersstatusinformatie wordt vastgelegd, kan de informatie op een van de volgende manieren worden opgeslagen:  

- U kunt de gebruikersstatusgegevens extern opslaan door een statusmigratiepunt te configureren. De takenreeks Vastleggen verzendt de gegevens naar het statusmigratiepunt. Nadat het besturingssysteem is geïmplementeerd, haalt de takenreeks Herstellen de gegevens op en wordt de gebruikersstatus op de doelcomputer hersteld.  

- U kunt de gebruikersstatusgegevens lokaal opslaan op een specifieke locatie. In dit scenario kopieert de takenreeks Vastleggen de gebruikersgegevens naar een specifieke locatie op de doelcomputer. Na de implementatie van het besturingssysteem haalt de takenreeks Herstellen de gebruikersgegevens op van die locatie.  

- U kunt vaste koppelingen opgeven die kunnen worden gebruikt om de gebruikersgegevens naar de oorspronkelijke locatie te herstellen. In dit scenario blijven de gebruikersstatusgegevens aanwezig op de schijf wanneer het oude besturingssysteem wordt verwijderd. Na de implementatie van het besturingssysteem gebruikt de takenreeks Herstellen de vaste koppelingen om de gebruikersstatusgegevens te herstellen naar hun oorspronkelijke locatie.  

  Voor meer informatie [beheert u de gebruikers status](../get-started/manage-user-state.md).  

##  <a name="deploy-to-unknown-computers"></a><a name="BKMK_UnknownComputer"></a> Naar onbekende computers implementeren  
 U kunt een besturings systeem implementeren op computers die niet worden beheerd door Configuration Manager. Er is geen record van deze computers in de Configuration Manager-Data Base. Deze computers worden onbekende computers genoemd. Onbekende computers omvatten het volgende:  

- Een computer waarop de Configuration Manager-client niet is geïnstalleerd  

- Een computer die niet is geïmporteerd in Configuration Manager  

- Een computer die niet is gedetecteerd door Configuration Manager  

  Zie [voor bereidingen voor onbekende computer implementaties](../get-started/prepare-for-unknown-computer-deployments.md)voor meer informatie.  

##  <a name="associate-users-with-a-computer"></a><a name="BKMK_UDA"></a> Gebruikers koppelen aan een computer  
 Als u een besturingssysteem implementeert, kunt u gebruikers koppelen met de doelcomputer om acties voor gebruikersaffiniteit apparaat te ondersteunen. Als u een gebruiker met de doelcomputer koppelt, kan de gebruiker met beheerdersrechten later acties uitvoeren op eender welke computer die met die gebruiker is gekoppeld, zoals het implementeren van een toepassing naar de computer van een specifieke gebruiker. Wanneer u echter een besturingssysteem implementeert, kunt u dit besturingssysteem niet implementeren op de computer van een specifieke gebruiker. Zie [gebruikers koppelen aan een doel computer](../get-started/associate-users-with-a-destination-computer.md)voor meer informatie.  

##  <a name="use-task-sequences-to-automate-steps"></a><a name="BKMK_TaskSequences"></a> Stappen automatiseren met takenreeksen  
 U kunt taken reeksen maken om verschillende taken in uw Configuration Manager omgeving uit te voeren. De bewerkingen van de takenreeks worden gedefinieerd in de individuele stappen van de reeks. Als de takenreeks wordt uitgevoerd, worden de bewerkingen van elke stap uitgevoerd op het niveau van de opdrachtregel zonder dat er een interventie van de gebruiker is vereist. U kunt takenreeksen gebruiken voor het volgende:  

-   [Een taken reeks maken om een besturings systeem te installeren](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Een takenreeks maken voor niet-besturingssysteemimplementaties](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Een takenreeks maken voor het vastleggen van een besturingssysteem](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Een takenreeks maken voor het registreren en herstellen van de gebruikersstatus](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Een aangepaste takenreeks maken](../deploy-use/create-a-custom-task-sequence.md)  

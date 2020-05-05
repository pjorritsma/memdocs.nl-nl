---
title: 'Installatiekopieën van het besturingssysteem aanpassen '
titleSuffix: Configuration Manager
description: Gebruik taken reeksen voor vastleggen en bouwen, hand matige configuratie of een combi natie van beide om een installatie kopie van een besturings systeem aan te passen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a1dcd3528f4dbaacec81837150d6f8a1ad6c455
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724165"
---
# <a name="customize-operating-system-images-with-configuration-manager"></a>Installatie kopieën van een besturings systeem aanpassen met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Installatie kopieën van besturings systemen in Configuration Manager zijn WIM-bestanden en vertegenwoordigen een gecomprimeerde verzameling referentie bestanden en-mappen die zijn vereist om een besturings systeem correct te installeren en te configureren op een computer. Een installatiekopie van een besturingssysteem wordt samengesteld en vastgelegd vanaf een referentiecomputer die u configureert met alle vereiste besturingssysteembestanden, ondersteuningsbestanden, software-updates, hulpprogramma's en andere softwaretoepassingen. U bepaalt zelf de mate waarin u de referentiecomputer handmatig configureert. U kunt de configuratie van de referentiecomputer volledig automatiseren door een takenreeks samen te stellen en vast te leggen, u kunt een aantal aspecten van de referentiecomputer handmatig configureren en vervolgens de rest automatiseren met behulp takenreeksen of u kunt de referentiecomputer handmatig configureren zonder gebruik te maken van takenreeksen. Gebruik de volgende secties om een besturings systeem aan te passen.

##  <a name="prepare-for-the--reference-computer"></a><a name="BKMK_PrepareReferenceComputer"></a>De referentie computer voorbereiden  
 Voordat u een installatiekopie van besturingssysteem van een referentiecomputer vastlegt, moet u rekening houden met verschillende aspecten.  

###  <a name="decide-between-an-automated-or-manual-configuration"></a><a name="BKMK_RefComputerDecide"></a>Kiezen tussen een automatische of hand matige configuratie  
 Verderop vindt u informatie over de voordelen en nadelen van een automatische en handmatige configuratie van de referentiecomputer.  

#### <a name="automated-configuration"></a>Automatische configuratie  
 **Voordelen**  

- De configuratie kan volledig zonder toezicht gebeuren, wat de noodzaak van de aanwezigheid van een beheerder of gebruiker elimineert.  

- U kunt de takenreeks opnieuw gebruiken om de configuratie van bijkomende referentiecomputers te herhalen met een hoger vertrouwensniveau.  

- U kunt de takenreeks wijzigen om de verschillen in referentiecomputers op te vangen zonder dat de volledige takenreeks opnieuw moet gecreëerd worden.  

  **Nadelen**  

- De initiële actie om een takenreeks te bouwen, kan een lange tijd vergen voor de creatie en het testen.  

- Indien de vereisten voor referentiecomputers significant veranderen, kan het lange tijd duren om de takenreeks opnieuw te bouwen en opnieuw te testen.  

#### <a name="manual-configuration"></a>Handmatige configuratie  
 **Voordelen**  

- U moet de takenreeks niet creëren of de tijd nemen om de takenreeks te testen en er de fouten van op te sporen en te herstellen.  

- U kunt rechtstreeks vanaf cd's installeren zonder alle software pakketten (inclusief Windows zelf) in een Configuration Manager-pakket te plaatsen.  

  **Nadelen**  

- De nauwkeurigheid van de computerconfiguratie hangt af van de beheerder of de gebruiker die de computer configureert.  

- U moet nog altijd verifiëren dat de referentiecomputer juist geconfigureerd is.  

- U kunt de configuratiemethode niet opnieuw gebruiken.  

- Vereist een persoon die actief betrokken wordt tijdens het proces.  

###  <a name="considerations-for-the-reference-computer"></a><a name="BKMK_RefComputerConsiderations"></a>Overwegingen voor de referentie computer  
 Verderop staat de lijst van basiselementen waarmee u rekening moet houden bij de configuratie van een referentiecomputer.  

-   **Te implementeren besturingssysteem**  

     De referentiecomputer moet geïnstalleerd worden met het besturingssysteem dat u van plan bent te gebruiken op uw doelcomputers. Zie [vereisten voor de infra structuur voor besturingssysteem implementatie](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)voor meer informatie over de besturings systemen die u kunt implementeren.  

-   **Juist servicepack**  

     De referentiecomputer moet geïnstalleerd worden met het besturingssysteem dat u van plan bent te gebruiken op uw doelcomputers.  

-   **Juiste software-updates**  

     Installeer alle softwaretoepassingen die u wenst op te nemen in de installatiekopie van het besturingssysteem die u vastlegt van de referentiecomputer. U kunt ook softwaretoepassingen installeren als u de geregistreerde installatiekopie van het besturingssysteem op de doelcomputers implementeert.  

-   **Lidmaatschap van een werkgroep**  

     De referentiecomputer moet geconfigureerd zijn als een lid van een werkgroep.  

-   **Sysprep**  

     Het hulpprogramma voor systeemvoorbereiding (Sysprep) is een technologie die u kunt gebruiken met andere implementatiehulpprogramma's om Windows besturingssystemen te installeren op nieuwe hardware. Sysprep bereidt een computer voor op het nemen van een installatiekopie op harde schijf of voor levering aan een gebruiker door de computer te configureren zodat een nieuwe beveiligings-ID (SID) wordt gecreëerd bij het opnieuw opstarten van de computer. Bovendien ruimt Sysprep gebruikers- en computerspecifieke instellingen en gegevens op die niet moeten worden gekopieerd naar een doelcomputer.  

     U kunt handmatig de systeemvoorbereiding (Sysprep) van de referentiecomputer uitvoeren door de volgende opdracht uit te voeren:  

     `Sysprep /quiet /generalize /reboot`  

     De optie /generalize geeft Sysprep de opdracht systeemspecifieke gegevens uit de Windows-installatie te verwijderen. Systeemspecifieke informatie bevat gebeurtenislogboeken, unieke beveiligings-id (SID's) en andere unieke informatie. Nadat de unieke systeeminformatie is verwijderd, wordt de computer opnieuw opgestart.  

     U kunt Sysprep automatiseren door gebruik te maken van de [Windows voorbereiden voor vastleggen](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) takenreeks of van registratiemedia.  

    > [!IMPORTANT]  
    >  De [Windows voorbereiden voor vastleggen](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) takenreeks tracht het lokale beheerderswachtwoord op de referentiecomputer opnieuw in te stellen op een lege waarde voordat Sysprep draait. Indien het lokale beveiligingsbeleid **Het wachtwoord moet aan de complexiteitsvereisten voldoen** ingeschakeld is, slaagt deze takenreeksstap er niet in om het beheerderswachtwoord opnieuw in te stellen. Schakel in dit geval het beleid uit indien u de takenreeks uitvoert.  

     Zie [Technische naslaginformatie over systeemvoorbereiding (Sysprep)](https://go.microsoft.com/fwlink/?LinkId=280286) voor meer informatie over Sysprep.  

-   **Juiste hulpprogramma's en scripts die zijn vereist om installatie-scenario's in te perken**  

     Juiste hulpprogramma's en scripts die zijn vereist om installatie-scenario's in te perken  

-   **Juiste bureaubladaanpassing, zoals achtergrond, huisstijl en standaard gebruikersprofiel**  

     U kunt de referentiecomputer configureren met de aanpassingskenmerken voor het bureaublad die u wenst over te nemen wanneer u de installatiekopie van het besturingssysteem van de referentiecomputer vastlegt. Bureaubladkenmerken omvatten achtergrond, huisstijl van de organisatie en een standaardgebruikersprofiel.  

##  <a name="manually-build-a-reference-computer"></a><a name="BKMK_ManuallyBuildReference"></a>Hand matig een referentie computer bouwen  
 Gebruik de volgende procedure om handmatig een referentiecomputer te bouwen.  

> [!NOTE]  
>  Als u de referentiecomputer handmatig bouwt, kunt u de installatiekopie van het besturingssysteem vastleggen met vastlegmedia. Zie [Capture-media maken](../deploy-use/create-capture-media.md)voor meer informatie.  

#### <a name="to-manually-build-the-reference-computer"></a>De referentiecomputer handmatig bouwen  

1. Identificeer de te gebruiken computer als de referentiecomputer.  

2. Configureer de referentiecomputer met het juiste besturingssysteem en andere software die nodig is om de installatiekopie van het besturingssysteem te maken dat u wenst te implementeren.  

   > [!WARNING]  
   >  Installeer minimaal het juiste besturingssysteem en servicepack, de juiste stuurprogramma's voor ondersteuning en de vereiste software-updates.  

3. Configureer de referentiecomputer als een lid van een werkgroep.  

4. Zet het beheerderwachtwoord terug op de referentiecomputer zodat de waarde van het wachtwoord leeg is.  

5. Voer Sysprep uit met de opdracht: **sysprep /quiet /generalize /reboot**. De optie /generalize geeft Sysprep de opdracht systeemspecifieke gegevens uit de Windows-installatie te verwijderen. Systeemspecifieke informatie bevat gebeurtenislogboeken, unieke beveiligings-id (SID's) en andere unieke informatie. Nadat de unieke systeeminformatie is verwijderd, wordt de computer opnieuw opgestart.  

   Zodra de referentiecomputer klaar is, gebruikt u een takenreeks om de installatiekopie van het besturingssysteem van de referentiecomputer vast te leggen.  Zie [Een installatiekopie van een besturingssysteem vastleggen vanaf een bestaande referentiecomputer](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer) voor gedetailleerde stappen.  

##  <a name="use-a-task-sequence-to-build-a-reference-computer"></a><a name="BKMK_UseTSToBuildReference"></a>Een referentie computer bouwen met een taken reeks  
 U kunt het proces voor het maken van een referentiecomputer automatiseren door een takenreeks te gebruiken waarmee u het besturingsysteem, de stuurprogramma's, de toepassingen, enzovoort implementeert.  Voer de volgende stappen uit om de referentiecomputer te bouwen en vervolgens de installatiekopie van het besturingssysteem vanaf de referentiecomputer vast te leggen.  

-   Gebruik een takenreeks om de installatiekopie van het referentiebesturingssysteem te maken en vast te leggen.  Zie [Een referentiecomputer bouwen en vastleggen met behulp van een takenreeks](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS) voor gedetailleerde stappen.  

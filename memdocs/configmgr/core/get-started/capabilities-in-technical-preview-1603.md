---
title: Mogelijkheden van Technical Preview 1603
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1603.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73e3e19df4ce545e4cbb36109da2710e848f1159
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076217"
---
# <a name="capabilities-in-technical-preview-1603-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1603 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1603. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Als u System Center Technical Preview 5 gebruikt, wordt deze versie ook geïnstalleerd als een basislijn versie van de Configuration Manager Technical Preview. Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.  

 **Bekende problemen met deze technische preview:**  

- Deze release bevat updates voor eerder uitgebrachte functies, maar er worden geen nieuwe functies geïntroduceerd. Daarom is de pagina functies van de wizard Update leeg als u eerder een upgrade hebt uitgevoerd naar 1602 en alle functies hebt ingeschakeld die zijn opgenomen in 1602.  

- Nadat de site server is bijgewerkt naar Technical Preview 1603, kunnen clients geen functies voor beheer op afstand gebruiken totdat ze ook zijn bijgewerkt naar versie 1603.  

  **Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

##  <a name="improvements-to-software-center"></a><a name="BKMK_SC1603"></a>Verbeteringen in Software Center  

### <a name="new-tiled-view-for-apps"></a>Nieuwe tegel weergave voor apps  
 Eind gebruikers kunnen nu kiezen uit een lijst met apps of een tegel weergave van apps op het tabblad **toepassingen** van software Center.  

### <a name="select-multiple-updates-in-software-center"></a>Meerdere updates selecteren in Software Center  
 Op het tabblad **updates** van software Center kunt u nu meerdere updates selecteren of **Alles bijwerken** selecteren om meerdere updates tegelijk te installeren.  

##  <a name="improvements-to-remote-control"></a><a name="BKMK_RC1603"></a>Verbeteringen aan beheer op afstand  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Toegang tot gedeelde klem bord beperken in een sessie voor beheer op afstand  
 U kunt nu de nieuwe client instelling voor externe hulpprogram ma's **vragen de gebruiker wordt gevraagd** om de toegang tot het gedeelde klem bord te beperken in een sessie voor beheer op afstand.  

 Wanneer deze optie is ingeschakeld, moet de eind gebruiker die een externe sessie deelt, machtigingen verlenen voor de viewer van die sessie voordat de viewer bestanden van de sessie naar hun lokale machine kan overdragen via het gedeelde klem bord.  

 Hiermee wordt een beveiligingslaag voor de eind gebruiker toegevoegd als voorheen, als de viewer volledig beheer van de computer van de eind gebruiker heeft gekregen, kunnen ze het gedeelde klem bord gebruiken om bestanden van de sessie over te brengen naar hun lokale computer, op een manier die volledig transparant was voor de eind gebruiker.  

##  <a name="customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> De RamDisk TFTP-blokgrootte en de -venstergrootte aanpassen op het distributiepunt met PXE-functionaliteit  
 In de 1603 Technical Preview kunt u de RamDisk TFTP-blok grootte en de venster grootte aanpassen voor distributie punten met PXE-functionaliteit. Als u uw netwerk hebt aangepast, kan dit ertoe leiden dat het downloaden van de opstartinstallatiekopie mislukt met een time-outfout omdat het blok of het venster te groot is. Met RamDisk TFTP-blok- en venstergrootteaanpassing kunt u het TFTP-verkeer optimaliseren als u PXE gebruikt om te voldoen aan uw specifieke netwerkvereisten.   
U moet de aangepaste instellingen in uw omgeving testen om te bepalen het meest efficiënt is.  

-   **TFTP-blokgrootte**: de blokgrootte is de grootte van de gegevenspakketten die door de server worden verzonden naar de client die het bestand downloadt (zoals beschreven in de RFC 2347). Met een groter blok kan de server minder pakketten verzenden, waardoor er minder trajectvertraging optreedt tussen de server en de client. Met grotere blokken kan er echter sprake zijn van gefragmenteerde pakketten, waar de meeste PXE-clientimplementaties geen ondersteuning voor bieden.  

-   **TFTP-venstergrootte**: TFTP vereist een bevestigingspakket (ACK) voor elk gegevensblok dat wordt verzonden. De server verzendt het volgende blok in de reeks pas wanneer het ACK-pakket van het vorige blok is ontvangen. TFTP-vensterbewerking is een functie in Windows Deployment Services waarmee u kunt instellen hoeveel gegevensblokken er in een venster passen. De server verzendt de gegevensblokken achter elkaar door tot het venster is gevuld. Daarna verzendt de client een ACK-pakket. Als u het venster vergroot, treedt er minder trajectvertraging op tussen de client en de server en is er minder tijd nodig om een opstartinstallatiekopie te downloaden.  

### <a name="try-it-out"></a>Probeer het nu!  
 Voer de volgende taken uit en gebruik daarna de feedback informatie boven aan dit onderwerp om ons te laten weten hoe het werkt:  

-   Ik kan de RamDisk TFTP-venster grootte aanpassen op het distributie punt met PXE-functionaliteit.  

-   Ik kan de RamDisk TFTP-blok grootte aanpassen op het distributie punt met PXE-functionaliteit.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>De grootte van het RamDisk TFTP-venster wijzigen  

- Voeg de volgende registersleutel toe aan de distributiepunten met PXE-functionaliteit om de RamDisk TFTP-venstergrootte aan te passen:  

   **Locatie**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Naam: RamDiskTFTPWindowSize  

   **Type**: REG_DWORD  

   **Waarde**: &lt;aangepaste venster grootte\>  

  De standaardwaarde is 1 (het venster bestaat uit één gegevensblok)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>De grootte van het RamDisk TFTP-blok wijzigen  

- Voeg de volgende registersleutel toe aan de distributiepunten met PXE-functionaliteit om de RamDisk TFTP-venstergrootte aan te passen:  

   **Locatie**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Naam: RamDiskTFTPBlockSize  

   **Type**: REG_DWORD  

   **Waarde**: &lt;aangepaste blok grootte\>  

  De standaardwaarde is 4096 (4k).  

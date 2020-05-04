---
title: Client implementatie op Mac-computers plannen
titleSuffix: Configuration Manager
description: Plan voor client implementatie naar Mac-computers in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f231e0681b2a202696b6c719966abf818a9c8e27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713224"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-configuration-manager"></a>Het plannen van client implementatie op Mac-computers in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt de Configuration Manager-client installeren op Mac-computers waarop het Mac OS X-besturings systeem wordt uitgevoerd en de volgende beheer mogelijkheden gebruiken:  

- **Hardware-inventaris**  

   U kunt Configuration Manager hardware-inventaris gebruiken om informatie te verzamelen over de hardware en geïnstalleerde toepassingen op Mac-computers. Deze informatie kan vervolgens worden weer gegeven in resource Explorer in de Configuration Manager-console en worden gebruikt om verzamelingen, query's en rapporten te maken. Zie [resource Explorer gebruiken om de hardware-inventaris te bekijken](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)voor meer informatie.  

   Configuration Manager verzamelt de volgende hardware-informatie van Mac-computers:  

  -   Processor  

  -   Computersysteem  

  -   Schijf station  

  -   Schijf partitie  

  -   Netwerk adapter  

  -   Besturingssysteem  

  -   Service  

  -   Proces  

  -   Geïnstalleerde software  

  -   Computer systeem product  

  -   USB-controller  

  -   USB-apparaat  

  -   CD-romstation  

  -   Video controller  

  -   Bureaublad monitor  

  -   Draag bare batterij  

  -   Fysiek geheugen  

  -   Printer  

  > [!IMPORTANT]  
  >  U kunt de hardware-informatie die tijdens de hardware-inventaris wordt verzameld van Mac-computers, niet uitbreiden.  

- **Instellingen voor naleving**  

   U kunt Configuration Manager instellingen voor naleving gebruiken om de compatibiliteit van Mac OS X-voor keur instellingen (. plist) weer te geven en te herstellen. U kunt bijvoorbeeld instellingen afdwingen voor de start pagina in de Safari-webbrowser of ervoor zorgen dat Apple firewall is ingeschakeld. U kunt ook shell scripts gebruiken om instellingen in MAC OS X te controleren en te herstellen.  

- **Toepassingsbeheer**  

   Configuration Manager kunt software implementeren op Mac-computers. U kunt de volgende software-indelingen implementeren op Mac-computers:  

  -   Apple-schijf image (. DMG  

  -   Meta pakket bestand (. MPKG  

  -   Mac OS X Installer-pakket (. PKG  

  -   Mac OS X-toepassing (. APP  

  Wanneer u de Configuration Manager-client op Mac-computers installeert, kunt u de volgende beheer mogelijkheden niet gebruiken die worden ondersteund door de Configuration Manager-client op Windows-computers:  

- Clientpushinstallatie  

- Implementatie van besturingssystemen  

- Software-updates  

  > [!NOTE]  
  >  U kunt Configuration Manager toepassings beheer gebruiken om vereiste Mac OS X-software-updates te implementeren op Mac-computers. Daarnaast kunt u nalevings instellingen gebruiken om ervoor te zorgen dat computers de vereiste software-updates hebben.  

- Onderhoudsvensters  

- Extern beheer  

- Energiebeheer  

- Clientcontrole en herstel van de clientstatus  

  Zie [clients implementeren op Macs](../../../../core/clients/deploy/deploy-clients-to-macs.md)voor meer informatie over het installeren en configureren van de Configuration Manager Mac-client.

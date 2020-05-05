---
title: Clients bijwerken
titleSuffix: Configuration Manager
description: Informatie over het bijwerken van clients in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95e6ebf1544951b71ca2b60615e3e01b27cc0f3b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076676"
---
# <a name="upgrade-clients-in-configuration-manager"></a>Clients bijwerken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt verschillende methoden gebruiken om de Configuration Manager-client software op Windows-computers, UNIX-en Linux-servers en Mac-computers bij te werken. Dit zijn de voor-en nadelen van elke methode.  

> [!TIP]  
>  Als u een upgrade van uw serverinfrastructuur uitvoert vanaf een eerdere versie van Configuration Manager \(zoals Configuration Manager 2007 of System Center 2012 Configuration Manager\), wordt u aangeraden de serverupgrades, inclusief alle updates van Current Branch, uit te voeren voordat u een upgrade uitvoert van de Configuration Manager-clients. Op deze manier hebt u ook de meest recente versie van de-client software.  

## <a name="group-policy-installation"></a>Installatie van Groepsbeleid  
 **Ondersteund clientplatform:** Windows  

#### <a name="advantages"></a>Voordelen  

- Vereist niet dat computers moeten worden gedetecteerd voordat de client kan worden bijgewerkt.  

- Kan worden gebruikt voor de nieuwe clientinstallaties of voor upgrades.  

- Computers kunnen clientinstallatie-eigenschappen lezen die gepubliceerd werden op Active Directory Domain Services.  

- Vereist niet dat u een installatie-account configureert en onderhoudt voor de bedoelde clientcomputer.  

#### <a name="disadvantages"></a>Nadelen  

- Kan hoog netwerk verkeer veroorzaken als u een groot aantal clients bijwerkt.  

- Als het Active Directory schema niet is uitgebreid voor Configuration Manager, moet u [Groepsbeleid instellingen](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) gebruiken om client installatie-eigenschappen toe te voegen aan computers in uw site.  


## <a name="logon-script-installation"></a>Aanmeldingscriptinstallatie  
 **Ondersteund clientplatform:** Windows  

#### <a name="advantages"></a>Voordelen  

- Vereist niet dat computers moeten worden gedetecteerd voordat de client kan worden geïnstalleerd.  

- Kan worden gebruikt voor de nieuwe clientinstallaties of voor upgrades.  

- Ondersteunt opdrachtregeleigenschappen voor CCMSetup.  

#### <a name="disadvantages"></a>Nadelen  

- Kan veel netwerk verkeer veroorzaken als u een groot aantal clients in een korte periode bijwerkt.  

- Het kan lang duren om alle client computers bij te werken als gebruikers zich niet vaak aanmelden op het netwerk.  

  Zie [Configuration Manager-clients met behulp van aanmeldingsscripts installeren](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript)voor meer informatie.  

## <a name="manual-installation"></a>Handmatige installatie  
 **Ondersteund clientplatform**: Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Voordelen  

- Vereist niet dat computers moeten worden gedetecteerd voordat de client kan worden bijgewerkt.  

- Kan handig zijn voor testdoeleinden.  

- Ondersteunt opdrachtregeleigenschappen voor CCMSetup.  

#### <a name="disadvantages"></a>Nadelen  

- Er is geen automatisering, dus tijdrovend.  

  Zie de volgende onderwerpen voor meer informatie:  

- [Het handmatig Configuration Manager-Clients installeren](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [Clients voor Linux-en UNIX-servers bijwerken](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [Clients op Mac-computers bijwerken](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Installatie-upgrade (toepassingsbeheer)  
 **Ondersteund clientplatform:** Windows  

> [!NOTE]  
>  U kunt Configuration Manager 2007-clients niet bijwerken met deze methode. In dit scenario kunt u de Configuration Manager-client implementeren als een pakket vanaf de Configuration Manager 2007-site, of u kunt automatische client upgrade gebruiken die automatisch een pakket maakt en implementeert dat de nieuwste versie van de client bevat.  

#### <a name="advantages"></a>Voordelen  

- Ondersteunt opdrachtregeleigenschappen voor CCMSetup.  

#### <a name="disadvantages"></a>Nadelen  

- Kan hoog netwerk verkeer veroorzaken als u de client distribueert naar grote verzamelingen.  

- Kan enkel gebruikt worden om clientsoftware up te daten op computers die werden gedetecteerd en toegewezen aan de site.  

  Zie [Configuration Manager-clients met behulp van aanmeldingsscripts installeren](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp)voor meer informatie.  

## <a name="automatic-client-upgrade"></a>Automatische clientupgrade  

> [!NOTE]  
> Kan worden gebruikt om Configuration Manager 2007-clients te upgraden naar Configuration Manager van de huidige branch-clients. Een Configuration Manager 2007-client kan worden toegewezen aan een Configuration Manager-site, maar kan geen acties uitvoeren behalve een automatische client upgrade.  

 **Ondersteund clientplatform:** Windows  

#### <a name="advantages"></a>Voordelen  

- Als gevolg van de wille keurige voor de opgegeven periode, is alleen een automatische upgrade geschikt voor grootschalige Client upgrades. Andere methoden zijn te langzaam op grote schaal of ze hebben geen wille keurige waarde. 

    > [!Note]
    > Het testen van de client is niet geschikt voor grote schaal, omdat deze helemaal geen enkele waarde bevat.  
- Kan gebruikt worden om automatisch clients in uw site up to date te laten zijn met de laatste versie.  

- Vereist mini maal beheer.  

#### <a name="disadvantages"></a>Nadelen  

- Kan enkel gebruikt worden om de clientsoftware up te daten en kan niet gebruikt worden om een nieuwe client te installeren.  

- Is van toepassing op alle clients in de hiërarchie die toegewezen zijn aan een site. Kan niet worden ingedeeld per verzameling.  

- Beperkte opties voor het plannen.  

  Zie [clients voor Windows-computers bijwerken voor](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)meer informatie.  

## <a name="client-testing"></a>Client testen  
 **Ondersteund clientplatform:** Windows  

#### <a name="advantages"></a>Voordelen  

- Kan worden gebruikt om nieuwe client versies in een kleinere pre-productie verzameling te testen.  

- Wanneer het testen is voltooid, worden de clients in de pre-productie gepromoveerd tot productie en automatisch bijgewerkt op de Configuration Manager-site.  

#### <a name="disadvantages"></a>Nadelen  

- Kan enkel gebruikt worden om de clientsoftware up te daten en kan niet gebruikt worden om een nieuwe client te installeren.  

  [Client upgrades testen in een pre-productie verzameling](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  

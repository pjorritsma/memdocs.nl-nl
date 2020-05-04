---
title: Clientinstallatiemethoden
titleSuffix: Configuration Manager
description: Meer informatie over de methoden voor het installeren van de Configuration Manager-client.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d5f238ddb0e2c28a51cdad8dc7347f872227535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713308"
---
# <a name="client-installation-methods-in-configuration-manager"></a>Client installatie methoden in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt verschillende methoden gebruiken om de Configuration Manager-client software te installeren. Gebruik één methode of een combi natie van methoden. In dit artikel worden de verschillende methoden beschreven, zodat u kunt zien welke methode het beste werkt voor uw organisatie.  

## <a name="client-push-installation"></a>Clientpushinstallatie  

**Ondersteund client platform**: Windows  

#### <a name="advantages"></a>Voordelen  

-   Kan gebruikt worden om de client te installeren op één computer, een verzameling van computers of voor de resultaten van een query.  

-   Kan gebruikt worden om automatisch de client te installeren op alle gedetecteerde computers.  

-   Gebruikt automatisch clientinstallatie-eigenschappen die zijn gedefinieerd op het tabblad **Client** in het dialoogvenster **Clientpushinstallatie-eigenschappen**.  

#### <a name="disadvantages"></a>Nadelen  

-   Kan hoog netwerkverkeer veroorzaken wanneer te grote verzamelingen worden gepusht.  

-   Kan alleen worden gebruikt op computers die zijn gedetecteerd door Configuration Manager.  

-   Kan niet worden gebruikt voor het installeren van clients in een werk groep.  

-   Er moet een clientpushinstallatie-account opgegeven worden die beheerdersrechten heeft voor de bedoelde clientcomputer.  

-   Windows Firewall moet worden geconfigureerd met uitzonde ringen op client computers.   

-   U kunt client push installatie niet annuleren. Configuration Manager probeert de client te installeren op alle gedetecteerde bronnen. Er worden Maxi maal zeven dagen fouten opnieuw geprobeerd.  

Zie [clients installeren met client push](../deploy-clients-to-windows-computers.md#BKMK_ClientPush)voor meer informatie.  



## <a name="software-update-point-based-installation"></a>Installatie op basis van software-updatepunten  

**Ondersteund client platform**: Windows  

#### <a name="advantages"></a>Voordelen  

-   Kan uw bestaande software-update-infrastructuur gebruiken om de clientsoftware te beheren.  

-   Als Windows Server Update Services (WSUS) en instellingen voor groeps beleid in Active Directory Domain Services op de juiste wijze zijn geconfigureerd, kan de client software automatisch op nieuwe computers worden geïnstalleerd.  

-   Vereist niet dat computers worden gedetecteerd voordat de client kan worden geïnstalleerd.  

-   Computers kunnen clientinstallatie-eigenschappen lezen die gepubliceerd werden op Active Directory Domain Services.  

-   Als de client wordt verwijderd, wordt deze door deze methode opnieuw geïnstalleerd.  

-   Vereist niet dat u een installatie account configureert en onderhoudt voor de bedoelde client computer.  

#### <a name="disadvantages"></a>Nadelen  

-   Vereist een werkende software-update-infrastructuur als een vereist onderdeel.  

-   Moet dezelfde server gebruiken voor client installatie en software-updates. Deze server moet zich bevinden op een primaire site.  

-   Als u nieuwe clients wilt installeren, moet u een groeps beleidsobject in Active Directory Domain Services configureren met het actieve software-update punt en de huidige poort van de client.  

-   Als het Active Directory schema niet is uitgebreid voor Configuration Manager, moet u instellingen voor groeps beleid gebruiken om computers in te richten met client installatie-eigenschappen.  

Zie [clients installeren met installatie op basis van software-updates](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP)voor meer informatie.  



## <a name="group-policy-installation"></a>Installatie van Groepsbeleid  

**Ondersteund client platform**: Windows  

#### <a name="advantages"></a>Voordelen  

-   Vereist niet dat computers worden gedetecteerd voordat de client kan worden geïnstalleerd.  

-   Kan worden gebruikt voor de nieuwe clientinstallaties of voor upgrades.  

-   Computers kunnen clientinstallatie-eigenschappen lezen die gepubliceerd werden op Active Directory Domain Services.  

-   Vereist niet dat u een installatie account configureert en onderhoudt voor de bedoelde client computer.  

#### <a name="disadvantages"></a>Nadelen  

-   Als er een groot aantal clients wordt geïnstalleerd, kan dit veel netwerk verkeer veroorzaken.  

-   Als het Active Directory schema niet is uitgebreid voor Configuration Manager, moet u instellingen voor groeps beleid gebruiken om client installatie-eigenschappen toe te voegen aan computers in uw site.  

Zie [clients installeren met groeps beleid](../deploy-clients-to-windows-computers.md#BKMK_ClientGP)voor meer informatie.  



## <a name="logon-script-installation"></a>Aanmeldingscriptinstallatie  

**Ondersteund client platform**: Windows  

#### <a name="advantages"></a>Voordelen  

-   Vereist niet dat computers worden gedetecteerd voordat de client kan worden geïnstalleerd.  

-   Ondersteunt opdrachtregeleigenschappen voor CCMSetup.  

#### <a name="disadvantages"></a>Nadelen  

-   Als een groot aantal clients gedurende een korte periode wordt geïnstalleerd, kan dit veel netwerk verkeer veroorzaken.  

-   Als gebruikers zich niet regel matig aanmelden bij het netwerk, kan het lang duren om te installeren op alle client computers.  

Zie [clients met aanmeldings scripts installeren](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript)voor meer informatie.  



## <a name="manual-installation"></a>Handmatige installatie  

**Ondersteund client platform**: Windows, Unix/Linux, Mac OS X  

#### <a name="advantages"></a>Voordelen  

-   Vereist niet dat computers worden gedetecteerd voordat de client kan worden geïnstalleerd.  

-   Kan handig zijn voor testdoeleinden.  

-   Ondersteunt opdrachtregeleigenschappen voor CCMSetup.  

#### <a name="disadvantages"></a>Nadelen  

-   Er is geen automatisering, dus tijdrovend.  

Raadpleeg de volgende artikelen voor meer informatie over het hand matig installeren van de client op elk platform:  

-   [Clients implementeren op Windows-computers](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [Clients implementeren op UNIX- en Linux-servers](../deploy-clients-to-unix-and-linux-servers.md)  

-   [Clients op Macs implementeren](../deploy-clients-to-macs.md)  



## <a name="microsoft-intune-mdm-installation"></a>Installatie van Microsoft Intune MDM

**Ondersteunde client platforms**: Windows 10

#### <a name="advantages"></a>Voordelen  

-   Vereist niet dat computers worden gedetecteerd voordat de client kan worden geïnstalleerd.  

-   Vereist niet dat u een installatie account configureert en onderhoudt voor de bedoelde client computer.  

-   Kan moderne verificatie gebruiken met Azure Active Directory.  

-   Kan computers op het Internet installeren en toewijzen.  

-   Kan automatiseren met Windows auto pilot en Microsoft Intune voor co-beheer.  

#### <a name="disadvantages"></a>Nadelen  

-   Vereist extra technologieën buiten Configuration Manager.  

-   Vereist dat het apparaat toegang heeft tot internet, zelfs als dit niet op internet is gebaseerd.  

Raadpleeg voor meer informatie de volgende artikelen:  

-   [Hoe kan ik clients installeren op door Intune MDM beheerde Windows-apparaten](../deploy-clients-to-windows-computers.md#bkmk_mdm)  

-   [Configuration Manager Windows 10-clients installeren en toewijzen met behulp van Azure AD voor verificatie](../deploy-clients-cmg-azure.md)  


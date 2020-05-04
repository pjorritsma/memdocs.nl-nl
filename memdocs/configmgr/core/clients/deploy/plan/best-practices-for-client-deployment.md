---
title: Aanbevolen procedures voor client implementatie
titleSuffix: Configuration Manager
description: Aanbevolen procedures voor client implementatie in Configuration Manager ophalen.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28f8bfb2ef012fcd4f19835190b7c042d38fd9e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713336"
---
# <a name="best-practices-for-client-deployment-in-configuration-manager"></a>Aanbevolen procedures voor de implementatie van clients in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Gebruik software-update-gebaseerde clientinstallatie voor Active Directory-computers  
 Deze client implementatie methode maakt gebruik van bestaande Windows-technologieën, integreert met uw Active Directory-infra structuur, vereist de minste configuratie in Configuration Manager, is het eenvoudigst te configureren voor firewalls en is het veiligst. Als u beveiligings groepen en WMI-filtering voor de groepsbeleid configuratie gebruikt, hebt u ook veel flexibiliteit om te bepalen welke computers de Configuration Manager-client installeren.  

 Zie [Configuration Manager-clients installeren met behulp van installatie op basis van software-updates](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP)voor meer informatie.  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Breid het Active Directory-schema uit en publiceer de site zodat u CCMSetup kunt uitvoeren zonder opdrachtregelopties  
 Wanneer u het Active Directory schema voor Configuration Manager uitbreidt en de site wordt gepubliceerd naar Active Directory Domain Services, worden veel client installatie-eigenschappen gepubliceerd naar Active Directory Domain Services. Als een computer deze client installatie-eigenschappen kan vinden, kan deze worden gebruikt tijdens de implementatie van Configuration Manager-client. Omdat deze informatie automatisch gegenereerd wordt, wordt het risico van menselijke fout, gekoppeld met het handmatig invoeren van installatie-eigenschappen, geëlimineerd.  

 Zie [over client installatie-eigenschappen die zijn gepubliceerd op Active Directory Domain Services](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)voor meer informatie.  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>Een gefaseerde implementatie gebruiken om het CPU-gebruik te beheren  
 Minimaliseer het effect van de CPU-verwerkings vereisten op de site server met behulp van een gefaseerde implementatie van clients. Implementeer clients buiten kantoor uren zodat andere services meer beschik bare band breedte hebben tijdens de dag en gebruikers niet worden onderbroken als hun computer trager wordt of opnieuw moet worden opgestart.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Automatische upgrade inschakelen nadat de belangrijkste clientimplementatie is voltooid  
 [Automatische Client upgrades](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) zijn handig wanneer u een upgrade wilt uitvoeren van een klein aantal client computers dat mogelijk is gemist door de hoofd installatie methode van de client, mogelijk omdat ze offline zijn. 

> [!NOTE]  
>  Dankzij de prestatie verbeteringen in Configuration Manager kunt u automatische upgrades gebruiken als primaire client upgrade methode. Prestatie zal evenwel afhangen van uw hiërarchie-infrastructuur, zoals het aantal clients.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Gebruik SMSMP en FSP als u de client installeert met client.msi-eigenschappen.  
 De SMSMP-eigenschap specificeert het initiële beheerpunt waarmee de client dient te communiceren en elimineert de afhankelijkheid van plaats in oplossingen zoals Active Directory Domain Services, DNS en WINS.  

 Gebruik de FSP-eigenschap en installeer een terugvalstatuspunt zodat u clientinstallatie en -toewijzing kunt controleren en identificeer communicatieproblemen.  

 Zie [over de eigenschappen van client installatie](../../../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie over deze opties.  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>Taal pakketten voor de client installeren voordat u de clients installeert  
U wordt aangeraden client taal pakketten te installeren voordat u de-client implementeert. Als u [client taal pakketten](../../../../core/servers/deploy/install/language-packs.md) installeert (om extra talen in te scha kelen) op een site nadat u clients hebt geïnstalleerd, moet u de clients opnieuw installeren voordat ze deze talen kunnen gebruiken. Voor mobiele apparaatclients moet u het mobiele apparaat wissen en het opnieuw registreren.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Vereiste PKI-certificaten vooraf voorbereiden  
 Om apparaten op het internet, geregistreerde mobiele apparaten en Mac-computers te beheren, moet u PKI-certificaten hebben op sitesystemen (beheerpunten en distributiepunten) en de clientapparaten. U kunt op productienetwerken goedkeuring nodig hebben om nieuwe certificaten te gebruiken, systeemservers van de site te herstarten of gebruikers kunnen zich moeten afmelden en aanmelden voor nieuw groepslidmaatschap. Bovendien kan het zijn dat u voldoende replicatietijd voor de beveiligingsmachtigingen en voor alle nieuwe certificaatsjablonen moet voorzien.  

 Zie [PKI-certificaat vereisten voor Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md)voor meer informatie over vereiste PKI-certificaten.  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Configureer, vóór u clients installeert, nodige clientinstellingen en onderhoudsvensters.  
 Hoewel u [client instellingen](../../../../core/clients/deploy/configure-client-settings.md) en onderhouds Vensters kunt configureren voor-of nadat clients zijn geïnstalleerd, is het beter om de vereiste instellingen te configureren voordat u clients installeert, zodat deze worden gebruikt zodra de-client is geïnstalleerd. 

 Configureer onderhouds Vensters voor servers en voor Windows Embedded-apparaten om te zorgen voor bedrijfs continuïteit voor kritieke apparaten. Onderhouds vensters zorgen ervoor dat vereiste software-updates en antimalware-software de computer niet opnieuw opstarten tijdens kantoor uren.  

> [!IMPORTANT]  
>  Voor Windows 10-computers die u wilt beveiligen met Unified Write Filter (UWF), moet u het apparaat voor UWF configureren voordat u de client installeert. Hiermee kan Configuration Manager de client installeren met een aangepaste referentie provider die gebruikers met beperkte rechten blokkeert om zich tijdens de onderhouds modus aan te melden bij het apparaat.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>De gebruikers registratie voor Mac-computers en mobiele apparaten plannen   
 Als gebruikers hun eigen Mac-computers en mobiele apparaten bij Configuration Manager registreren, moet u de gebruikers ervaring plannen. U kunt bijvoorbeeld een script uitvoeren voor het installatie-en registratie proces door gebruik te maken van een webpagina, zodat gebruikers de minimale hoeveelheid benodigde gegevens invoeren en instructies verzenden via e-mail.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Op bestanden gebaseerde schrijf filters gebruiken voor Windows Embedded-apparaten 
 Ingesloten apparaten die Verbeterde schrijffilters (EWF) gebruiken, hebben grote kans om Hersynchronisaties te ondergaan van de statusmelding. Indien u slechts enkele ingesloten apparaten hebt, die Verbeterde schrijffilters gebruiken, kan het zijn dat u daar niets van merkt. Indien u daarentegen veel ingesloten apparaten hebt die hun informatie hersynchroniseren, zoals het zenden van een volledige inventaris in plaats van een inventaris voor verschillen, kan dit een merkbare toename genereren van netwerkpakketten en een grotere CPU-verwerking op de siteserver.  

 Wanneer u een keuze hebt van het type schrijf filter dat u wilt inschakelen, kies dan op bestand gebaseerde schrijf filters en configureer uitzonde ringen om client status en inventaris gegevens te behouden tussen het opnieuw opstarten van het apparaat voor netwerk-en CPU-efficiëntie op de Configuration Manager-client. Zie [planning voor client implementatie op Windows Embedded-apparaten](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)voor meer informatie over schrijf filters.  

 Zie [Ondersteunde besturingssystemen voor clients en apparaten](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)voor meer informatie over het maximum aantal Windows Embedded-clients dat een primaire site kan ondersteunen.  

---
title: Client implementatie op Windows Embedded-apparaten plannen
titleSuffix: Configuration Manager
description: Plan voor client implementatie op Windows Embedded-apparaten in Configuration Manager.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7848e3c0c38391ab61d10ad46cbb772c812539c7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906641"
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-configuration-manager"></a>Het plannen van client implementatie op Windows Embedded-apparaten in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<a name="BKMK_DeployClientEmbedded"></a>Als uw Windows Embedded-apparaat de Configuration Manager-client niet bevat, kunt u een van de client installatie methoden gebruiken als het apparaat voldoet aan de vereiste afhankelijkheden. Als het Embedded-apparaat schrijffilters ondersteunt, moet u deze filters uitschakelen voordat u de client installeert, en de filters vervolgens opnieuw inschakelen nadat de client is geïnstalleerd en is toegewezen aan een site.  

 Wanneer u de filters uitschakelt, moet u ervoor zorgen dat u niet de stuurprogramma's voor het filter uitschakelt. Deze stuurprogramma's worden doorgaans automatisch gestart wanneer de computer wordt gestart. Als u de stuurprogramma's uitschakelt, wordt de installatie van de client verhinderd of wordt de indelingstaak voor schrijffilters verstoord, waardoor de clientbewerkingen mislukken. Hieronder ziet u de services die zijn gekoppeld aan elk type schrijffilter dat actief moet blijven:  

|Type schrijffilter|Stuurprogramma|Type|Beschrijving|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|Kernel|Implementeert I/O-omleiding op sectorniveau op beveiligde volumes.|  
|FBWF|FBWF|Bestandssysteem|Implementeert I/O-omleiding op bestandsniveau op beveiligde volumes.|  
|UWF|uwfreg|Kernel|Redirector UWF-register|  
|UWF|uwfs|Bestandssysteem|Redirector UWF-bestand|  
|UWF|uwfvol|Kernel|UWF-volumebeheer|  

 Schrijffilters beheren hoe het besturingssysteem op het Embedded-apparaat wordt bijgewerkt wanneer u wijzigingen aanbrengt, zoals wanneer u software installeert. Wanneer schrijffilters zijn ingeschakeld, worden de wijzigingen niet rechtstreeks in het besturingssysteem aangebracht, maar worden ze in plaats daarvan doorgestuurd naar een tijdelijke overlay. Als de wijzigingen enkel naar de overlay worden geschreven, gaan ze verloren wanneer het Embedded-apparaat wordt uitgeschakeld. Als de schrijffilters echter tijdelijk worden uitgeschakeld, kunnen de wijzigingen permanent gemaakt worden zodat u de wijzigingen niet opnieuw moet aanbrengen (of de software niet opnieuw moet installeren) telkens het Embedded-apparaat opnieuw wordt opgestart. Het tijdelijk uitschakelen en vervolgens opnieuw inschakelen van de schrijffilters vereist echter dat de computer een of meerdere keren opnieuw wordt opgestart; u beheert dit daarom best wanneer het gebeurt door onderhoudsvensters te configureren zodat de computer opnieuw wordt opgestart buiten de werkuren.  

 U kunt opties configureren om de schrijffilters automatisch uit te schakelen en opnieuw in te schakelen wanneer u software implementeert zoals toepassingen, takenreeksen, software-updates en de Endpoint Protection-client. De uitzondering is voor configuratiebasislijnen met configuratie-items die automatisch herstel gebruiken. In dit scenario vindt het herstel steeds plaats in de overlay zodat het enkel beschikbaar is wanneer het apparaat opnieuw wordt opgestart. Het herstel wordt opnieuw toegepast bij de volgende evaluatiecyclus, maar enkel op de overlay, die wordt gewist bij het opnieuw opstarten. Als u wilt afdwingen dat Configuration Manager de herstel wijzigingen doorvoert, kunt u de configuratie basislijn implementeren en vervolgens een andere software-implementatie die de wijziging zo snel mogelijk ondersteunt.  

 Als de schrijffilters zijn uitgeschakeld, kunt u software op Windows Embedded-apparaten installeren met behulp van Software Center. Als de schrijf filters zijn ingeschakeld, mislukt de installatie echter en Configuration Manager een fout bericht weer gegeven dat u onvoldoende machtigingen hebt om de toepassing te installeren.  

> [!WARNING]  
>  Zelfs als u niet de Configuration Manager opties selecteert om de wijzigingen door te voeren, kunnen de wijzigingen worden doorgevoerd als er een andere software-installatie of wijziging wordt aangebracht die wijzigingen doorvoert. In dit scenario zullen de oorspronkelijke wijzigingen worden toegepast naast de nieuwe wijzigingen.  

 Als Configuration Manager de schrijf filters uitschakelt om wijzigingen permanent te maken, kunnen alleen gebruikers die lokale beheerders rechten hebben zich aanmelden en het embedded-apparaat gebruiken. Tijdens deze periode worden gebruikers met weinig rechten vergrendeld en zien ze een boodschap dat de computer niet beschikbaar is omdat hij wordt onderhouden. Dit helpt het apparaat te beschermen terwijl het in een status is waarin wijzigingen permanent kunnen worden toegepast, en dit vergrendelgedrag in de onderhoudsmodus is een andere reden om een onderhoudsvenster te configureren op een moment waarop gebruikers zich niet kunnen aanmelden op deze apparaten.  

 Configuration Manager biedt ondersteuning voor het beheren van de volgende typen schrijf filters:  

- Op bestand gebaseerd schrijf filter (FBWF): Zie [op bestanden gebaseerde schrijf filter](https://docs.microsoft.com/previous-versions/windows/embedded/aa940926(v=winembedded.5))voor meer informatie.  

- Enhanced Write Filter-RAM-geheugen (EWF): Zie [Enhanced Write Filter](https://docs.microsoft.com/previous-versions/windows/embedded/ms912906(v=winembedded.5))voor meer informatie.  

- Gecombineerd schrijf filter (UWF): Zie [Unified Write Filter](https://docs.microsoft.com/windows-hardware/customize/enterprise/unified-write-filter)(Engelstalig) voor meer informatie.  

  Configuration Manager ondersteunt geen schrijf filter bewerkingen wanneer het Windows Embedded-apparaat zich in de EWF RAM reg-modus bevindt.  

> [!IMPORTANT]
>  Als u de keuze hebt, kunt u op bestanden gebaseerde schrijf filters (FBWF) gebruiken met Configuration Manager voor een verhoogde efficiëntie en een hogere schaal baarheid.
> 
> **Voor apparaten die alleen gebruikmaken van FBWF:** Configureer de volgende uitzonde ringen om client status en inventaris gegevens te behouden tussen het opnieuw opstarten van het apparaat:  
> 
> - CCMINSTALLDIR \\ *. sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
>   Apparaten waarop Windows Embedded 8.0 of hoger wordt uitgevoerd, bieden geen ondersteuning voor uitsluitingen die jokertekens bevatten. Op deze apparaten moet u de volgende uitsluitingen afzonderlijk configureren:  
> 
> - Alle bestanden in CCMINSTALLDIR met de extensie .sdf. Doorgaans zijn dit:  
> 
>   -   UserAffinityStore.sdf  
>   -   InventoryStore.sdf  
>   -   CcmStore.sdf  
>   -   StateMessageStore.sdf  
>   -   CertEnrollmentStore.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
> **Voor apparaten met alleen FBWF en UWF:** Wanneer clients in een werk groep certificaten voor authenticatie op beheer punten gebruiken, moet u ook de persoonlijke sleutel uitsluiten om ervoor te zorgen dat de client blijft communiceren met het beheer punt. Configureer de volgende uitzonderingen op deze apparaten:  
> 
> - c:\Windows\System32\Microsoft\Protect  
>   -   c:\ProgramData\Microsoft\Crypto  
>   -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

> [!NOTE]
> Er zijn geen extra uitzonde ringen vereist voor de Configuration Manager-client, behalve die die is beschreven in het bovenstaande **belang rijke** vak. Het toevoegen van aanvullende Configuration Manager-of WMI (WBEM) gerelateerde uitzonde ringen kan leiden tot storingen van de Configuration Manager, inclusief apparaten die vastzitten in de onderhouds modus of op apparaten die bezig zijn met het opnieuw opstarten van lussen. Onnodige uitzonde ringen zijn onder andere de Configuration Manager client Directory, de map CCMcache, de CCMSetup-map, de taken reeks cache directory, de map WBEM en Configuration Manager gerelateerde register sleutels.

 Voor een voorbeeld scenario voor het implementeren en beheren van Windows Embedded-apparaten met schrijf filter ingeschakeld in Configuration Manager Zie [voorbeeld scenario voor het implementeren en beheren van Configuration Manager-clients op Windows Embedded-apparaten](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md).  

 Voor meer informatie over het maken van installatiekopieën voor Windows Embedded-apparaten en het configureren van schrijffilters, zie uw Windows Embedded-documentatie, of neem contact op met uw OEM.  

> [!NOTE]
>  Wanneer u de toepasselijke platforms voor software-implementaties en configuratie-items selecteert, tonen deze de Windows Embedded-families eerder dan specifieke versies. Gebruik de volgende lijst om de specifieke versie van Windows Embedded toe te wijzen aan de opties in het lijstvak:  
> 
> - **Embedded-besturingssystemen op basis van Windows XP (32-bit)** omvat het volgende:  
> 
>   -   Windows XP Embedded  
>   -   Windows Embedded voor point-of-service  
>   -   Windows Embedded Standard 2009  
>   -   Windows Embedded POSReady 2009  
>   -   **Embedded-besturingssystemen op basis van Windows 7 (32-bit)** omvat het volgende:  
> 
>   -   Windows Embedded Standard 7 (32-bit)  
>   -   Windows Embedded POSReady 7 (32-bit)  
>   -   Windows ThinPC  
>   -   **Embedded-besturingssystemen op basis van Windows 7 (64-bit)** omvat het volgende:  
> 
>   -   Windows Embedded Standard 7 (64-bit)  
>   -   Windows Embedded POSReady 7 (64-bit)

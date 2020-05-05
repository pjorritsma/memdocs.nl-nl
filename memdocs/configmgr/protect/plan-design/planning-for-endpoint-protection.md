---
title: Endpoint Protection plannen
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 720b5060c913ff3157624c4b6060802af396d221
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722170"
---
# <a name="planning-for-endpoint-protection-in-configuration-manager"></a>Endpoint Protection plannen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*


Met Endpoint Protection in Configuration Manager kunt u het antimalwarebeleid en Windows Firewall beveiliging voor client computers in uw Configuration Manager-hiërarchie beheren.  

> [!IMPORTANT]  
>  U moet een licentie hebben om Endpoint Protection te gebruiken voor het beheren van clients in uw Configuration Manager hiërarchie.  

Wanneer u Endpoint Protection gebruikt met Configuration Manager, hebt u de volgende voor delen:  

-   Antimalwarebeleid, Windows Firewall-instellingen en het beheren van micro soft Defender Advanced Threat Protection op geselecteerde groepen computers configureren  

-   Gebruik Configuration Manager software-updates om de meest recente definitie bestanden voor antimalware te downloaden om client computers up-to-date te houden  

-   Verzend e-mailmeldingen, gebruik in-console bewaking en geef rapporten weer om gebruikers met beheerdersrechten op de hoogte te houden wanneer er malware op clientcomputers is gedetecteerd.  

Voor Windows 10-computers is geen aanvullende client vereist voor Endpoint Protection-beheer. Op Windows 8,1 en eerdere computers installeert Endpoint Protection naast de Configuration Manager-client een eigen client. De Endpoint Protection-client biedt de volgende mogelijkheden:  

-   Detecteren en herstellen van malware en spyware  

-   Rootkitdetectie en herstel  

-   Evalueren van kritieke beveiligingsproblemen en automatische definitie en engine-updates  

-   Detecteren van kwetsbare plekken in het netwerk via het netwerkinspectiesysteem  

-   Integratie met Cloud Protection Service om malware aan micro soft te melden. Wanneer u deelneemt aan deze service, kan Windows Defender of de Endpoint Protection-client de meest recente definities downloaden van het Malware Protection Center wanneer onbekende malware op een computer wordt gedetecteerd.  

> [!NOTE]  
>  De Endpoint Protection-client kan worden geïnstalleerd op een server waarop Hyper-V en op virtuele gast machines met ondersteunde besturings systemen worden uitgevoerd. Endpoint Protection acties hebben een ingebouwde, wille keurige vertraging, zodat de services niet tegelijkertijd worden uitgevoerd om buitensporig CPU-gebruik te voor komen.  

  Daarnaast kunt u met Endpoint Protection in Configuration Manager Windows Firewall-instellingen beheren in de Configuration Manager-console.  

 [Voorbeeld scenario: het gebruik van System Center Endpoint Protection om computers te beveiligen tegen malware](../deploy-use/scenarios-endpoint-protection.md) laat zien hoe u Endpoint Protection en de Windows Firewall kunt configureren en beheren.  

## <a name="managing-malware-with-endpoint-protection"></a>Malware beheren met Endpoint Protection  

Met Endpoint Protection in Configuration Manager kunt u een antimalwarebeleid maken dat instellingen bevat voor Endpoint Protection client configuraties. U kunt deze antimalwarebeleid vervolgens implementeren op client computers en deze controleren in het knoop punt **Endpoint Protection status** in de werk ruimte **bewaking** of door gebruik te maken van Configuration Manager-rapporten.  

 Extra informatie:  

-   [Antimalwarebeleid voor Endpoint Protection maken en implementeren](../deploy-use/endpoint-antimalware-policies.md) : antimalwarebeleid maken, implementeren en bewaken met een lijst met instellingen die u kunt configureren  

-   [Bewaak Endpoint Protection](../deploy-use/monitor-endpoint-protection.md) bewakings activiteiten rapporten, geïnfecteerde client computers en meer.   

-   [Antimalwarebeleid en Firewall instellingen voor Endpoint Protection beheren](../deploy-use/endpoint-antimalware-firewall.md) : u kunt de beleids prioriteit voor [antimalware](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) of [firewall](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies)wijzigen, [malware herstellen die op client computers](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware)en andere taken is gevonden

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Windows Firewall beheren met Endpoint Protection  
 Endpoint Protection in Configuration Manager biedt basis beheer van de Windows Firewall op client computers. Voor elk netwerkprofiel kunt u de volgende instellingen configureren:  

-   Windows Firewall in- of uitschakelen.  

-   Blokkeer binnenkomende verbindingen, inclusief verbindingen in de lijst met toegestane programma's.  

-   Waarschuw de gebruiker wanneer een nieuw programma door Windows Firewall wordt geblokkeerd.  

> [!NOTE]  
>  Endpoint Protection biedt alleen ondersteuning voor het beheren van Windows Firewall.  

  Zie voor meer informatie over het maken en implementeren van Windows Firewall beleid voor Endpoint Protection [het maken en implementeren van Windows Firewall beleid voor Endpoint Protection](../deploy-use/create-windows-firewall-policies.md).  

## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Vanaf versie 1606 van Configuration Manager (current branch) kan Endpoint Protection helpen bij het beheren en bewaken van micro soft Defender Advanced Threat Protection (ATP), voorheen bekend als Windows Defender ATP. Micro soft Defender ATP is een service waarmee bedrijven geavanceerde aanvallen op hun netwerken kunnen detecteren, onderzoeken en hierop reageren. Zie [micro soft Defender Advanced Threat Protection](../deploy-use/windows-defender-advanced-threat-protection.md)(Engelstalig).

## <a name="endpoint-protection-workflow"></a>Endpoint Protection-werkstroom  
 Gebruik het volgende diagram om inzicht te krijgen in de werk stroom voor het implementeren van Endpoint Protection in uw Configuration Manager-hiërarchie.  

 ![Endpoint Protection-werkstroom](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Endpoint Protection-client voor Mac-computers en Linux-servers  
 System Center bevat een Endpoint Protection-client voor Linux en voor Mac-computers. Deze clients worden niet geleverd met Configuration Manager; in plaats daarvan moet u de volgende producten downloaden van de [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  U moet klant van Microsoft Volume License zijn om de Endpoint Protection-installatiebestanden voor Linux en de Mac te kunnen downloaden.  

 Deze producten kunnen niet worden beheerd vanuit de Configuration Manager-console. Er wordt echter System Center Operations Manager-beheerpakket ij de installatiebestanden geleverd waarmee u de client voor Linux kunt beheren met Operations Manager.  

 Voor meer informatie over het installeren en beheren van Endpoint Protection-clients voor Linux- en Mac-computers gebruikt u de documentatie bij deze producten. De documentatie bevindt zich in de map **Documentatie** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Aanbevolen procedures voor Endpoint Protection in Configuration Manager  
 Gebruik de volgende aanbevolen procedures voor Endpoint Protection in System Center 2012 Configuration Manager.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Aangepaste clientinstellingen configureren voor Endpoint Protection  
 Wanneer u client instellingen voor Endpoint Protection configureert, moet u niet de standaard client instellingen gebruiken omdat deze instellingen Toep assen op alle computers in uw hiërarchie. Configureer in plaats daarvan aangepaste clientinstellingen en wijs deze instellingen toe aan verzamelingen computers in uw hiërarchie.  

 Als u aangepaste clientinstellingen configureert, kunt u het volgende doen:  

-   Antimalware- en beveiligingsinstellingen aanpassen voor verschillende onderdelen van uw organisatie.  
-   Test de effecten van het uitvoeren van Endpoint Protection op een kleine groep computers voordat u deze implementeert in de gehele hiërarchie.  
-   Voeg na verloop van tijd meer clients toe aan de verzameling om uw implementatie van de Endpoint Protection-client te faseren.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Definitie-updates distribueren via software-updates  
 Als u Configuration Manager software-updates gebruikt om definitie-updates te distribueren, kunt u overwegen om definitie-updates te plaatsen in een pakket dat geen andere software-updates bevat. Zodoende houdt u de grootte van het definitie-updatepakket beperkt, waardoor ze sneller naar distributiepunten worden gerepliceerd.

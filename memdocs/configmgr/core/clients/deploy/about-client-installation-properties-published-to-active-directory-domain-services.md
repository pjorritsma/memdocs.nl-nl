---
title: Eigenschappen van client installatie in Active Directory
titleSuffix: Configuration Manager
description: Configuration Manager client installatie-eigenschappen publiceren naar Active Directory Domain Services.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49b2edf7234e53c3fc03542f803933463190e8c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712069"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Over eigenschappen van client installatie gepubliceerd op Active Directory Domain Services

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u het Active Directory schema voor Configuration Manager uitbreidt en de site wordt gepubliceerd op Active Directory Domain Services, worden veel client installatie-eigenschappen gepubliceerd naar Active Directory Domain Services. Als een computer deze client installatie-eigenschappen kan vinden, kan deze worden gebruikt tijdens de implementatie van Configuration Manager-client.  

 De voordelen van het gebruik van Active Directory Domain Services om eigenschappen van clientinstallatie te publiceren omvatten het volgende:  

-   Voor client installaties op basis van software-update punten en groepsbeleid-client installaties hoeven geen installatie parameters te worden ingesteld op elke computer.  

-   Omdat deze informatie automatisch gegenereerd wordt, wordt het risico van menselijke fout, gekoppeld met het handmatig invoeren van installatie-eigenschappen, geëlimineerd.  

> [!NOTE]  
>  Zie [schema-uitbrei dingen voor Configuration Manager](../../plan-design/network/schema-extensions.md)voor meer informatie over het uitbreiden van het Active Directory schema voor Configuration Manager en het publiceren van een site.  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Eigenschappen van client installatie gepubliceerd op Active Directory Domain Services  
Hier volgt een lijst met eigenschappen van client installatie. Zie [over de eigenschappen van client installatie](../../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie over elk item dat hieronder wordt vermeld.  

- De Configuration Manager site code.  

- Het server handtekeningcertificaat van de siteserver.  

- De vertrouwde basissleutel.  

- De client-communicatiepoorten voor HTTP en HTTPS.  

- Het terugvalstatuspunt. Als de site meerdere terugval status punten heeft, wordt alleen de eerste versie die is geïnstalleerd, gepubliceerd naar Active Directory Domain Services.  

- Een instelling om aan te geven dat de client moet communiceren door enkel HTTPS te gebruiken.  

- Instellingen voor PKI-certificaten:  

  -   Of u moet een PKI-clientcertificaat gebruiken.  

  -   De selectie criteria voor certificaat selectie. Dit kan vereist zijn omdat de client meer dan één geldig PKI-certificaat heeft dat kan worden gebruikt voor Configuration Manager.  

  -   Een instelling om te bepalen welk certificaat dient gebruikt te worden als de client meerdere geldige certificaten heeft na het proces van certificaatselectie.  

  -   De lijst van uitgevers van certificaten die een lijst bevat van vertrouwde CA basiscertificaten.  

- Client.msi installatie-eigenschappen die gespecificeerd zijn in het tabblad **Client** van het dialoogvenster **Clientpushinstallatie-eigenschappen** .

Client installatie (CCMSetup) gebruikt de eigenschappen die worden gepubliceerd naar Active Directory Domain Services alleen als er geen andere eigenschappen zijn opgegeven met behulp van een van de volgende:  

-   De hand matige installatie methode (verderop in dit artikel beschreven)

-   De groepsbeleid-installatie methode (verderop in dit artikel beschreven)

> [!NOTE]  
>  De eigenschappen van de client installatie worden gebruikt om de-client te installeren. Deze eigenschappen kunnen worden overschreven door nieuwe instellingen van de toegewezen site nadat de client is geïnstalleerd en is toegewezen aan een Configuration Manager-site.  

 Gebruik de details in de volgende secties om te bepalen welke Configuration Manager client installatie methoden Active Directory Domain Services gebruiken om eigenschappen van client installatie te verkrijgen.  

## <a name="client-push-installation"></a>Clientpushinstallatie  
 Clientpushinstallatie gebruikt geen Active Directory Domain Services om installatie-eigenschappen te verkrijgen.  

 In plaats daarvan kunt u de eigenschappen van de client installatie opgeven op het tabblad **installatie-eigenschappen** van het dialoog venster **Eigenschappen van client push installatie** . Deze opties en client-gerelateerde site-instellingen worden opgeslagen in een bestand dat de client leest tijdens clientinstallatie.  

> [!NOTE]  
>  U moet geen CCMSetup-eigenschappen opgeven voor client push installatie, of het terugval status punt, of de vertrouwde basis sleutel in het tabblad **installatie-eigenschappen** . Deze instellingen worden automatisch aan clients geleverd wanneer ze worden geïnstalleerd door gebruik te maken van client push installatie.
CCMSetup ondersteunt naast client. msi-eigenschappen de volgende para meters:/ForceReboot,/skipprereq,/Logon,/BITSPriority,/downloadtimeout,/forceinstall

 Alle eigenschappen die u opgeeft op het tabblad **installatie-eigenschappen** , worden gepubliceerd naar Active Directory Domain Services als de site wordt gepubliceerd op Active Directory Domain Services. Deze instellingen worden gelezen door clientinstallaties waar CCMSetup uitgevoerd wordt zonder installatie-eigenschappen.  

## <a name="software-update-point-based-installation"></a>Installatie op basis van software-updatepunten  
 De installatiemethode op basis van software-updatepunten ondersteunt niet de toevoeging van installatie-eigenschappen aan de CCMSetup-opdrachtregel.  

 Indien er geen opdrachtregels werden ingesteld op de clientcomputer door gebruik te maken van groepsbeleid, zoekt CCMSetup op Active Directory Services naar installatie-eigenschappen.  

## <a name="group-policy-installation"></a>Installatie van Groepsbeleid  
 De groepsbeleid-installatiemethode ondersteunt niet de toevoeging van installatie-eigenschappen aan de CCMSetup-opdrachtregel.  

 Indien er geen opdrachtregels werden ingesteld op de clientcomputer, zoekt CCMSetup op Active Directory Services naar installatie-eigenschappen.  

## <a name="manual-installation"></a>Handmatige installatie  
 CCMSetup zoekt onder de volgende omstandigheden in Active Directory Domain Services naar installatie-eigenschappen:  

-   Er zijn na de opdracht CCMSetup.exe geen eigenschappen vanaf de opdrachtregel opgegeven.  

-   De computer is niet via Groepsbeleid ingericht met installatie-eigenschappen.  

## <a name="logon-script-installation"></a>Aanmeldingscriptinstallatie  
 CCMSetup zoekt onder de volgende omstandigheden in Active Directory Domain Services naar installatie-eigenschappen:  

-   Er zijn na de opdracht CCMSetup.exe geen eigenschappen vanaf de opdrachtregel opgegeven.  

-   De computer is niet via Groepsbeleid ingericht met installatie-eigenschappen.  

## <a name="software-distribution-installation"></a>Installatie van softwaredistributie  
 CCMSetup zoekt onder de volgende omstandigheden in Active Directory Domain Services naar installatie-eigenschappen:  

-   Er zijn na de opdracht CCMSetup.exe geen eigenschappen vanaf de opdrachtregel opgegeven.  

-   De computer is niet via Groepsbeleid ingericht met installatie-eigenschappen.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Installaties voor clients die geen toegang hebben tot Active Directory Domain Services  
Deze client computers kunnen de gepubliceerde installatie-eigenschappen niet lezen of openen vanuit Active Directory Domain Services.

 Deze clients omvatten:  

-   Computers in werk groepen.  

-   Clients die zijn toegewezen aan een Configuration Manager-site die niet is gepubliceerd in Active Directory Domain Services.  

-   Clients die worden geïnstalleerd wanneer ze zich op internet bevinden.  

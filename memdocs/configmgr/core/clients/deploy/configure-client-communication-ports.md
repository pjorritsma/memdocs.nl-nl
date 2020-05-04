---
title: Client communicatie poorten configureren
titleSuffix: Configuration Manager
description: Client communicatie poorten instellen in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30b553bbe2a68ec97e4d5200644a88d09ee5967d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713112"
---
# <a name="how-to-configure-client-communication-ports-in-configuration-manager"></a>Client communicatie poorten configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt de aanvraag poort nummers wijzigen die Configuration Manager clients gebruiken om te communiceren met site systemen die gebruikmaken van HTTP en HTTPS voor communicatie. Hoewel HTTP of HTTPS waarschijnlijk al is geconfigureerd voor firewalls, vereist client meldingen die gebruikmaken van HTTP of HTTPS meer CPU-gebruik en geheugen op de beheer punt computer dan als u een aangepast poort nummer gebruikt. U kunt ook het poort nummer van de site opgeven dat moet worden gebruikt als u clients activeert met behulp van traditionele Ontwaak pakketten.  

 Wanneer u HTTP-en HTTPS-aanvraag poorten opgeeft, kunt u een standaard poort nummer en een alternatief poort nummer opgeven. Clients proberen automatisch de alternatieve poort nadat de communicatie met de standaard poort is mislukt. U kunt instellingen opgeven voor HTTP-en HTTPS-gegevens communicatie.  

 De standaard waarden voor client aanvraag poorten zijn **80** voor http-verkeer en **443** voor HTTPS-verkeer. Wijzig ze alleen als u deze standaard waarden niet wilt gebruiken. Een typisch scenario voor het gebruik van aangepaste poorten is wanneer u een aangepaste website in IIS gebruikt in plaats van de standaard website. Als u de standaard poort nummers voor de standaard website in IIS wijzigt en andere toepassingen ook de standaard website gebruiken, kunnen ze waarschijnlijk niet worden uitgevoerd.  

> [!IMPORTANT]
>  Wijzig de poort nummers in Configuration Manager niet zonder de gevolgen ervan te kennen. Voorbeelden:  
> 
> - Als u de poort nummers voor de client aanvraag Services wijzigt als een site configuratie en bestaande clients niet opnieuw worden geconfigureerd voor het gebruik van de nieuwe poort nummers, worden deze clients onbeheerd.  
>   -   Voordat u een niet-standaard poort nummer configureert, moet u ervoor zorgen dat firewalls en alle tussenliggende netwerk apparaten deze configuratie kunnen ondersteunen en indien nodig opnieuw moeten configureren. Als u clients op Internet gaat beheren en het standaard HTTPS-poort nummer van 443, kunnen routers en firewalls op internet deze communicatie blok keren.  

 Om ervoor te zorgen dat clients niet onbeheerd worden nadat u de poort nummers van de aanvraag hebt gewijzigd, moeten clients worden geconfigureerd voor het gebruik van de nieuwe poort nummers van aanvragen. Wanneer u de aanvraag poorten op een primaire site wijzigt, nemen alle gekoppelde secundaire sites automatisch dezelfde poort configuratie over. Gebruik de procedure in dit onderwerp om de aanvraag poorten op de primaire site te configureren.  

> [!NOTE]  
>  Zie [aanvraag poorten configureren voor de client voor Linux en UNIX](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations)voor informatie over het configureren van de aanvraag poorten voor clients op computers met Linux en UNIX.  

 Wanneer de Configuration Manager-site wordt gepubliceerd naar Active Directory Domain Services, worden nieuwe en bestaande clients die toegang hebben tot deze gegevens, automatisch geconfigureerd met hun site poort instellingen en hoeft u geen verdere actie te ondernemen. Clients die geen toegang hebben tot deze informatie die is gepubliceerd op Active Directory Domain Services zijn onder andere werkgroepcomputers, clients van een andere Active Directory forest, clients die zijn geconfigureerd voor alleen Internet en clients die zich op het Internet bevinden. Als u de standaard poort nummers wijzigt nadat deze clients zijn geïnstalleerd, installeert u deze opnieuw en installeert u nieuwe clients met behulp van een van de volgende methoden:  

- Installeer de clients opnieuw met behulp van de wizard Push-client installatie. Bij client push installatie worden clients automatisch geconfigureerd met de huidige site poort configuratie. Zie [Configuration Manager-clients installeren met behulp van client push](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)voor meer informatie over het gebruik van de wizard Push-client installatie.  

- Installeer de clients opnieuw met behulp van CCMSetup. exe en de client. msi-installatie-eigenschappen van CCMHTTPPORT en CCMHTTPSPORT. Zie [over eigenschappen van client installatie](../../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie over deze eigenschappen.  

- Installeer de clients opnieuw met behulp van een methode die Active Directory Domain Services voor Configuration Manager client installatie-eigenschappen zoekt. Zie [over client installatie-eigenschappen die zijn gepubliceerd op Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)voor meer informatie.  

  Als u de poort nummers voor bestaande clients opnieuw wilt configureren, kunt u ook het script PORTSWITCH gebruiken. VBS dat wordt meegeleverd met de installatie media in de map SMSSETUP\Tools\PortConfiguration.  

> [!IMPORTANT]  
>  Voor bestaande en nieuwe clients die zich momenteel op het Internet bevinden, moet u de niet-standaard poort nummers configureren met behulp van de CCMSetup. exe client. msi-eigenschappen van CCMHTTPPORT en CCMHTTPSPORT.  

 Nadat de aanvraag poorten op de site heeft gewijzigd, worden nieuwe clients die zijn geïnstalleerd met behulp van de Push-client installatie methode voor de gehele site automatisch geconfigureerd met de huidige poort nummers voor de site.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>De poort nummers voor client communicatie voor een site configureren  

1. Klik op **Beheer**in de Configuration Manager-console.  

2. Vouw **site configuratie**uit in de werk ruimte **beheer** , klik op **sites**en selecteer de primaire site die u wilt configureren.  

3. Klik op het tabblad **Start** op **Eigenschappen**en klik vervolgens op het tabblad **poorten** .  

4. Selecteer een van de items en klik op het pictogram Eigenschappen om het dialoog venster **poort Details** weer te geven.  

5. Geef in het dialoog venster **poort Details** het poort nummer en de beschrijving voor het item op en klik vervolgens op **OK**.  

6. Selecteer **aangepaste website gebruiken** als u de aangepaste website naam **SMSWeb** wilt gebruiken voor site systemen die IIS uitvoeren.  

7. Klik op **OK** om het dialoogvenster met eigenschappen voor de site.  

   Herhaal deze procedure voor alle primaire sites in de hiërarchie.

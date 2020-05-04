---
title: Inleiding tot verzamelingen
titleSuffix: Configuration Manager
description: Krijg een inleiding tot het gebruik van verzamelingen in Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0665c6378ac81d6f6f254501760647048ce66b0b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714351"
---
# <a name="introduction-to-collections-in-configuration-manager"></a>Inleiding tot verzamelingen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Verzamelingen helpen u resources te organiseren in beheer bare eenheden. U kunt verzamelingen maken die overeenkomen met de behoeften van uw client beheer en om bewerkingen op meerdere resources tegelijk uit te voeren. 

De meeste beheer taken zijn afhankelijk van of vereisen het gebruik van een of meer verzamelingen. Hoewel u de ingebouwde verzameling van alle systemen kunt gebruiken, is het gebruik ervan voor beheer taken geen best practice. Maak aangepaste verzamelingen om specifieke apparaten of gebruikers voor een taak te identificeren.  

 Ingebouwde en aangepaste verzamelingen worden weer gegeven in de knoop punten **gebruikers verzamelingen** en **apparaten** in de werk ruimte **activa en naleving** in de Configuration Manager-console.  

 Verzamelingen die u onlangs hebt bekeken, worden weer gegeven in het knoop punt **gebruikers** en in het knoop punt **apparaten** in de werk ruimte **activa en naleving** .  

Hier volgen enkele voor beelden van het gebruik van de verzameling:  

|Bewerking|Voorbeeld|  
|---------|-------|  
|Groeperen van resources|U kunt verzamelingen maken waarmee resources worden gegroepeerd op basis van de hiërarchie van uw organisatie.<br /><br /> U kunt bijvoorbeeld een verzameling maken van alle computers in het hoofd kantoor Amsterdam Active Directory organisatie-eenheid (OE). Zie [verzamelingen maken](../../../../core/clients/manage/collections/create-collections.md)voor meer informatie over het maken van dit type verzameling.<br /><br /> U kunt deze verzameling gebruiken voor bewerkingen, zoals het configureren van Endpoint Protection instellingen, het configureren van energiebeheer instellingen voor apparaten of het installeren van de Configuration Manager-client.|  
|Toepassingsimplementatie|U kunt een verzameling maken van alle computers waarop geen Microsoft Office 2013 is geïnstalleerd en deze vervolgens implementeren op alle computers in die verzameling.<br /><br /> U kunt ook toepassingsvereisten gebruiken om deze taak uit te voeren. Zie [toepassingen maken met Configuration Manager](../../../../apps/deploy-use/create-applications.md)voor meer informatie.|  
|[Clientinstellingen beheren](../../../../core/clients/deploy/about-client-settings.md)|Hoewel de standaardclientinstellingen in Configuration Manager van toepassing zijn op alle apparaten en gebruikers, kunt u aangepaste clientinstellingen maken die van toepassing zijn op een verzameling apparaten of een verzameling gebruikers.<br /><br /> Als u bijvoorbeeld wilt dat extern beheer op alle apparaten beschikbaar is, configureert u de standaard client instellingen zodanig dat extern beheer is toegestaan en configureert u vervolgens aangepaste client instellingen die geen beheer op afstand toestaan en implementeert u deze voor de verzameling van buitengewone clients. |  
|[Energiebeheer](../power/introduction-to-power-management.md)|U kunt specifieke energie-instellingen per verzameling configureren.|  
|[Op rollen gebaseerd beheer](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Gebruik verzamelingen om te bepalen welke groepen gebruikers toegang hebben tot verschillende functies in de Configuration Manager-console.|  
|[Onderhouds Vensters](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Met onderhouds Vensters kunt u een periode definiëren waarin verschillende Configuration Manager bewerkingen kunnen worden uitgevoerd op leden van een apparaten verzameling. |  


## <a name="collection-types-in-configuration-manager"></a>Verzamelingtypen in Configuration Manager  
 Configuration Manager heeft ingebouwde verzamelingen voor algemene bewerkingen en u kunt ook aangepaste verzamelingen maken.   

### <a name="built-in-collections"></a>Ingebouwde verzamelingen  
 Configuration Manager bevat standaard de volgende verzamelingen die niet kunnen worden gewijzigd.  

|**Naam van verzameling**|Beschrijving|  
|-------------------------|-----------------|  
|**Alle gebruikersgroepen**|Bevat de gebruikersgroepen die zijn gedetecteerd via detectie van Active Directory-beveiligingsgroepen.|  
|**Alle gebruikers**|Bevat de gebruikers die zijn gedetecteerd via detectie van Active Directory-gebruikers.|  
|**Alle gebruikers en gebruikersgroepen**|Bevat de verzamelingen Alle gebruikers en Alle gebruikersgroepen. Deze verzameling bevat het grootste bereik van resources van de gebruiker en de gebruikers groep.|  
|**Alle Desktop- en Serverclients**|Bevat de server-en desktop apparaten waarop de Configuration Manager-client is geïnstalleerd. Het lidmaatschap wordt beheerd door Heartbeat-detectie.|  
|**Alle mobiele apparaten**|Bevat de mobiele apparaten die worden beheerd door Configuration Manager. Het lidmaatschap is beperkt tot de mobiele apparaten die zijn toegewezen aan een site of die zijn gedetecteerd door de Exchange Server-connector.|  
|**Alle systemen**|Bevat de alle bureau blad-en Server-clients, alle mobiele apparaten en de verzamelingen van alle onbekende computers, en alle mobiele apparaten die zijn Inge schreven door Microsoft Intune. Deze verzameling bevat het grootste bereik van bronnen voor apparaten.|  
|**Alle onbekende computers**|Bevat algemene computerrecords voor meerdere computerplatforms. U kunt deze verzameling gebruiken voor het implementeren van een besturingssysteem met behulp van een takenreeks en PXE-opstartbewerking, opstartbare media of voorbereide media.|  

### <a name="custom-collections"></a>Aangepaste verzamelingen  
 Wanneer u een aangepaste verzameling maakt in Configuration Manager, wordt het lidmaatschap van deze verzameling bepaald door een of meer verzamelings regels, zoals beschreven in [verzamelingen maken](../../../../core/clients/manage/collections/create-collections.md). 


---
title: Updates installeren Publisher
titleSuffix: Configuration Manager
description: System Center Updates Publisher installeren in uw omgeving
ms.date: 08/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f83e7207207496d69342a2322909e972ada5676
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720371"
---
# <a name="install-updates-publisher"></a>Updates installeren Publisher

*Van toepassing op: System Center Updates Publisher*

De informatie in deze artikelen kan u helpen updates Publisher te downloaden, te installeren en in te stellen voor gebruik met uw Configuration Manager-omgeving.

## <a name="prerequisites-and-limitations"></a>Vereisten en beperkingen
System Center Updates Publisher kan alleen worden gebruikt met Configuration Manager. Het is niet bedoeld voor gebruik met zelfstandige WSUS-hiërarchieën.

In de volgende secties worden de vereisten beschreven voor het installeren en gebruiken van updates Publisher, en beperkingen of bekende problemen met betrekking tot het gebruik.  

### <a name="operating-systems"></a>Besturingssystemen
Updates Publisher installeren en uitvoeren op een 64-bits versie van de volgende besturings systemen. Er zijn geen minimale cumulatieve updates of vereisten voor service packs.

-   Windows Server 2016 (Standard, Data Center)
-   Windows Server 2012 R2 (Standard, Data Center)
-   Windows 10 (Pro, education, Pro education, Enter prise)
-   Windows 8,1 (Professional, Enter prise)

### <a name="prerequisites"></a>Vereisten
Het volgende is vereist op de computer waarop updates Publisher wordt uitgevoerd.

-   **64-bits besturings systeem**: de computer waarop u updates installeert Publisher moet een 64-bits besturings systeem uitvoeren.
-   **WSUS 6,2 of hoger**:
    -   Installeer de standaard beheer console op Windows Server om aan deze vereiste te voldoen.
    -   Installeer de [Remote Server Administration Tools (RSAT) voor Windows-besturings systemen](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)voor Windows 10 en Windows 8,1. Hiermee wordt de benodigde ondersteuning voor het gebruik van updates Publisher (*API-en Power shell-cmdlets*en de *beheer console van de gebruikers interface*) geïnstalleerd.
-   **Machtigingen**:
    -   Installatie: lokale beheerder
    -   De meeste bewerkingen: lokale gebruiker
    -   Publiceren of bewerkingen waarbij WSUS: lid is van de groep WSUS-Administrators op de WSUS-server.

### <a name="supported-languages"></a>Ondersteunde talen
Updates Publisher is alleen beschikbaar in het Engels, maar kan updates voor andere talen beheren. De taal ondersteuning is afhankelijk van de taak, zoals het publiceren, maken of bewerken van updates.

Bij het exporteren of publiceren van updates, worden in updates Publisher de titel en beschrijving van de software-update weer gegeven op basis van de land instellingen van de computer waarop updates Publisher is geïnstalleerd.

U maakt bijvoorbeeld een software-update met een Engelse en Spaanse titel.

-   Als u de update maakt op een computer waarvan de land instelling Engels is, worden de titel en beschrijving in het Engels standaard weer geven.
-   Als u deze update vervolgens exporteert of publiceert naar een computer met een Spaanse land instelling, ziet u op die computer de titel en beschrijving in het Spaans.

### <a name="publishing"></a>Publiceren
Wanneer u software-updates publiceert, kunt u de taal van het binaire bestand van de software-update opgeven. U kunt ook opgeven dat het binaire bestand een taal onafhankelijk is. De volgende talen worden ondersteund:

-   Arabisch
-   Chinees (Hong Kong SAR)
-   Chinees (Traditioneel)
-   Chinees (Vereenvoudigd)
-   Tsjechisch
-   Deens
-   Nederlands
-   Engels
-   Fins
-   Frans
-   Duits
-   Grieks
-   Hebreeuws
-   Hongaars
-   Italiaans
-   Japans
-   Koreaans
-   Norwegian
-   Pools
-   Portugees
-   Portugees (Brazilië)
-   Russisch
-   Spaans
-   Zweeds
-   Turks

### <a name="software-update-titles-and-descriptions"></a>Titels en beschrijvingen van software-updates
De volgende talen worden ondersteund voor titels en beschrijvingen van software-updates.

-   Chinees (Traditioneel)
-   Chinees (Vereenvoudigd)
-   Engels
-   Frans
-   Duits
-   Italiaans
-   Japans
-   Koreaans
-   Portugees (Brazilië)
-   Russisch
-   Spaans

## <a name="install-updates-publisher"></a>Updates installeren Publisher
Down load **UpdatesPubliser. msi** voor het installeren van System Center updates Publisher via het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=55543).

Als u updates Publisher wilt installeren, voert u **UpdatesPublisher. msi** uit op een computer die voldoet aan de *vereisten*. Het installatie programma maakt de volgende map voor de bestanden die nodig zijn voor het uitvoeren van updates Publisher:%PROGRAMFILES%\Microsoft\UpdatesPublisher *.

Omdat deze map alle bestanden bevat die nodig zijn om updates Publisher te gebruiken, kunt u de map en de inhoud naar een nieuwe locatie of computer kopiëren en vervolgens updates Publisher vanaf die locatie gebruiken. De nieuwe locatie of computer moet echter voldoen aan de vereisten voor het uitvoeren van updates Publisher.

Nadat de installatie is voltooid, voert u **UpdatesPublisher. exe** uit vanuit de map *UpdatesPublisher* om updates Publisher te starten.

## <a name="next-steps"></a>Volgende stappen
 Na de installatie van updates Publisher wordt u aangeraden [de opties](updates-publisher-options.md) voor updates Publisher te configureren. U moet enkele opties configureren voordat u sommige functies van updates Publisher kunt gebruiken.

 Als u echter de standaard instellingen wilt gebruiken en niet wilt plannen voor het implementeren van updates op een update server of op beheerde apparaten, kunt u meteen aan de slag met het [beheer van software-update catalogi](updates-publisher-catalogs.md)of [software-updates maken](create-updates-with-updates-publisher.md) en zelf update-catalogi maken.

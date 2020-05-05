---
title: Naslaginformatie voor Setup
titleSuffix: Configuration Manager
description: Bekijk deze Naslag informatie om u te helpen bij het voorbereiden van de installatie van een Configuration Manager-site of-hiërarchie.
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d948452da54a41e35095b01cb0e942e02a7a597f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718068"
---
# <a name="reference-for-configuration-manager-setup"></a>Naslag informatie voor het instellen van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager-installatie biedt koppelingen naar verschillende onderwerpen die in de volgende secties worden beschreven. De informatie die hier wordt weer gegeven, kan u helpen bij het voorbereiden van de installatie van een Configuration Manager site of hiërarchie en helpt u bij het voorbereiden van de beslissingen die u moet nemen tijdens de installatie.  


##  <a name="before-you-begin"></a><a name="bkmk_start"></a>Voordat u begint  
Voordat u nieuwe Configuration Manager-sites installeert, moet u ervoor zorgen dat u de volgende informatie hebt bekeken, waarmee u de fase kunt instellen voor een succesvol implementatie ontwerp:  

-   [De grondbeginselen van Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Configuration Manager-infra structuur plannen](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Voorbereiden om Configuration Manager-sites te installeren](prepare-to-install-sites.md)  

##  <a name="assess-server-readiness"></a><a name="bkmk_assess"></a>Gereedheid van de server bepalen  
Voordat u met de installatie van een nieuwe site begint, moet u ervoor zorgen dat de site server en de externe site systeem servers die u wilt gebruiken voor de site (bijvoorbeeld de server die als host fungeert voor de site database) voldoen aan alle vereiste configuraties. Deze onderwerpen in de documentatie bibliotheek kunnen helpen:  

-   [Ondersteunde configuraties voor Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Prerequisite Checker](prerequisite-checker.md)  

##  <a name="clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a>Clients voor aanvullende besturings systemen  
U kunt client software voor Configuration Manager downloaden via het micro soft Download centrum voor de volgende besturings systemen:  

- macOS (Apple)
- UNIX
- Linux

Gebruik de volgende koppelingen voor het downloaden van clients voor de versie van Configuration Manager die u gebruikt:  

- [Micro soft endpoint Configuration Manager-macOS-client (64-bits)](https://www.microsoft.com/download/details.aspx?id=100850)

- [Micro soft Configuration Manager-clients voor aanvullende besturings systemen](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Gebruiksgegevensniveaus en instellingen  
Wanneer u uw eerste Configuration Manager-site installeert, installeert en configureert Configuration Manager automatisch een nieuwe site systeemrol, het **service aansluitpunt**op de site server. Het service verbindings punt heeft deze standaard instellingen:  

-   **Online** modus (de offline modus is ook beschikbaar)  
-   **Verbeterd** gegevensverzamelings niveau (twee andere gegevensverzamelings niveaus, basis en volledig, ook beschikbaar)  

Wanneer de site systeemrol van het service aansluitpunt online is, kan micro soft automatisch diagnostische gegevens en gebruiks informatie verzamelen via internet. Met de gegevens die worden verzameld kunnen we:  

-   Problemen vaststellen en oplossen  
-   Onze producten en de service verbeteren  
-   Updates herkennen voor Configuration Manager die betrekking hebben op de versie van Configuration Manager die u gebruikt  

### <a name="levels-of-data-collection"></a>Niveaus van gegevens verzameling  
Gegevens verzameling bevat deze drie niveaus:

-   **Basis** bevat gegevens over de installatie en upgrade, zoals het aantal sites en welke Configuration Manager functies zijn ingeschakeld. Er wordt geen persoons gegevens verzonden.  

-   **Uitgebreid** bevat de gegevens in de instelling basis niveau en verzendt gegevens over de hiërarchie, hoe elke functie wordt gebruikt (frequentie en duur) en uitgebreide diagnostische informatie, zoals de geheugen status van uw server wanneer er een systeem-of app-crash plaatsvindt. Er worden geen persoons gegevens verzonden.  

-   **Volledig** bevat de gegevens uit de instellingen basis en uitgebreid, en verzendt ook geavanceerde diagnostische informatie, zoals systeem bestanden en moment opnamen van het geheugen. Deze optie kan persoons gegevens bevatten, maar we gebruiken deze informatie niet om u te identificeren of contact met u op te nemen, of om reclame aan u te richten.  

Zie voor meer informatie, inclusief de openbaar making van de gegevens die worden verzameld door elk niveau, [Diagnostische en gebruiks gegevens voor Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Ga naar om de privacyverklaring van Configuration Manager Online weer te geven [https://go.microsoft.com/fwlink/?LinkID=626527](https://go.microsoft.com/fwlink/?LinkID=626527).

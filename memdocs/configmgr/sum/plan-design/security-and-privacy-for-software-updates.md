---
title: Beveiliging en privacy voor software-updates
titleSuffix: Configuration Manager
description: Volg deze aanbevolen procedures voor de beveiliging van software-updates en informatie over de manier waarop Configuration Manager privacy-informatie verwerkt.
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0838f43abf7ff972ac3f6ca2cdf44dcafda323ca
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718719"
---
# <a name="security-and-privacy-for-software-updates-in-configuration-manager"></a>Beveiliging en privacy voor software-updates in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit onderwerp bevat beveiligings-en privacy-informatie voor software-updates in Configuration Manager.  

##  <a name="security-best-practices-for-software-updates"></a><a name="BKMK_Security_HardwareInventory"></a> Aanbevolen beveiligingsprocedures voor software-updates  
 Gebruik de volgende aanbevolen beveiligingsprocedures wanneer u software-updates implementeert op clients:  

-   Zorg dat u de standaardmachtigingen voor software-updatepakketten niet wijzigt.  

     Software-updatepakketten worden standaard zodanig ingesteld dat beheerders **Volledig beheer** hebben en gebruikers de toegang **Lezen** hebben. Als u deze machtigingen wijzigt, kunnen kwaadwillende personen hierdoor mogelijk software-updates toevoegen of verwijderen.  

-   Beheer de toegang tot de downloadlocatie voor software-updates.  

     De computeraccounts voor de SMS-provider, de siteserver en de gebruiker met beheerdersrechten die de software-updates daadwerkelijk downloadt naar de downloadlocatie, hebben de toegang **Schrijven** nodig voor de downloadlocatie. Beperk de toegang tot de downloadlocatie om het risico te beperken dat kwaadwillende personen knoeien met de bronbestanden van software-updates op de downloadlocatie.  

     Als u bovendien een UNC-share gebruikt voor de downloadlocatie, beveiligt u het netwerkkanaal door IPsec of SMB-ondertekening te gebruiken om te voorkomen dat er wordt geknoeid met de bronbestanden van software-updates wanneer deze via het netwerk worden overgedragen.  

-   Gebruik UTC om implementatietijden te evalueren.  

     Als u de lokale tijd gebruikt in plaats van UTC, kunnen gebruikers mogelijk de installatie van software-updates vertragen door de tijdzone op hun computers te wijzigen.  

-   Schakel SSL op Windows Server Update Services (WSUS) in en volg de aanbevolen procedures om WSUS te beveiligen.  

     Bepaal en volg de aanbevolen beveiligings procedures voor de WSUS-versie die u gebruikt met Configuration Manager. 

     Voor meer informatie over het inschakelen van SSL raadpleegt [u de zelf studie een software-update punt configureren voor het gebruik van TLS/SSL met een PKI-certificaat](../get-started/software-update-point-ssl.md). 

    > [!IMPORTANT]  
    >  Als u het software-updatepunt zodanig configureert dat SSL-communicatie voor de WSUS-server wordt ingeschakeld, moet u virtuele roots voor SSL configureren op de WSUS-server.  

-   Schakel CRL-controle in.  

     Configuration Manager controleert standaard niet de certificaatintrekkingslijst (CRL) om de hand tekening van software-updates te controleren voordat deze op computers worden geïmplementeerd. Door de CRL te raadplegen elke keer dat er een certificaat wordt gebruikt, bent u beter beschermd tegen het gebruik van een ingetrokken certificaat. Hierdoor ontstaat echter ook een vertraging in de verbinding en vinden er extra verwerkingsactiviteiten plaats op de computer die de CRL-controle uitvoert.  

     Zie [CRL-controle inschakelen voor software-updates](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates)voor meer informatie over het inschakelen van CRL-controle voor software-updates.  

-   Configureer WSUS voor het gebruik van een aangepaste website.  

     Wanneer u WSUS installeert op het software-updatepunt, kunt u kiezen of u de bestaande standaardwebsite van IIS wilt gebruiken of een aangepaste WSUS-website wilt maken. Maak een aangepaste website voor WSUS, zodat IIS de WSUS-Services host op een speciale virtuele website in plaats van dezelfde website te delen die wordt gebruikt door de andere Configuration Manager-site systemen of andere toepassingen.  

     Zie [Configure WSUS to use a custom web site](plan-for-software-updates.md#BKMK_CustomWebSite)voor meer informatie.  

##  <a name="privacy-information-for-software-updates"></a><a name="BKMK_Privacy_HardwareInventory"></a> Privacy-informatie voor software-updates  
 Bij software-updates worden uw clientcomputers gescand om te bepalen welke updates u nodig hebt. Vervolgens wordt die informatie teruggestuurd naar de sitedatabase. Tijdens het software-update proces kan Configuration Manager informatie verzenden tussen clients en servers die de computer en aanmeldings accounts identificeren.  

 Configuration Manager houdt informatie over de status van het software-implementatie proces. Statusinformatie wordt niet versleuteld tijdens de overdracht of opslag. Status informatie wordt opgeslagen in de Configuration Manager-Data Base en wordt verwijderd door de onderhouds taken van de data base. Er wordt geen statusinformatie verzonden naar Microsoft.  

 Het gebruik van Configuration Manager software-updates om software-updates te installeren op client computers is mogelijk onderhevig aan licentie voorwaarden voor software voor deze updates, die los zijn van de Software licentievoorwaarden voor Configuration Manager. Controleer en ga altijd akkoord met de licentie voorwaarden voor software voordat u de software-updates installeert met behulp van Configuration Manager.  

 Configuration Manager implementeert standaard software-updates niet en vereist verschillende configuratie stappen voordat informatie wordt verzameld.  

 Voordat u software-updates configureert, moet u nadenken over uw privacyvereisten.  

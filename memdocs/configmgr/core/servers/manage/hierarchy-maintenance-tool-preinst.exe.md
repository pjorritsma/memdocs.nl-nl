---
title: Hulp programma voor hiërarchie onderhoud
titleSuffix: Configuration Manager
description: Meer informatie over het hulp programma voor hiërarchie onderhoud en waarom u het kunt gebruiken. Bevat informatie over opdracht regel opties.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b564575dfc135a9c82c7e102a02d70f1b6dbf6eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712440"
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-configuration-manager"></a>Hulp programma voor hiërarchie-onderhoud (preinst. exe) voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het hulp programma voor hiërarchie-onderhoud (preinst. exe) geeft opdrachten door aan de Configuration Manager hiërarchie beheerder terwijl de hiërarchie Manager-service wordt uitgevoerd. Het hiërarchie onderhoud-hulp programma wordt automatisch geïnstalleerd wanneer u een Configuration Manager-site installeert. U kunt preinst. exe vinden in de \\ &lt;gedeelde map *SiteServerName*>&lt;\ SMS_*site*code \bin\x64\00000409. op de site server.  

 U kan het hiërarchieonderhoud-hulpprogramma gebruiken in de volgende scenario's:  

-   Wanneer uitwisseling van een beveiligde sleutel vereist is, zijn er situaties waarin u handmatig de initiële uitwisseling van de openbare sleutel tussen sites moet uitvoeren. Zie [Handmatig uitwisselen van openbare sleutels tussen sites](#BKMK_ManuallyExchangeKeys) in dit onderwerp voor meer informatie.  

-   Om actieve jobs te verwijderen die voor een doelsite zijn die niet langer beschikbaar is.  

-   Een site server verwijderen uit de Configuration Manager-console wanneer u de site niet kunt verwijderen met behulp van Setup. Als u bijvoorbeeld een Configuration Manager site fysiek verwijdert zonder eerst Setup uit te voeren om de site te verwijderen, blijft de site-informatie bestaan in de data base van de bovenliggende site en blijft de bovenliggende site proberen te communiceren met de onderliggende site. Om dit probleem op te lossen, moet u het hulp programma voor hiërarchie onderhoud uitvoeren en hand matig de onderliggende site verwijderen uit de data base van de bovenliggende site.  

-   Om alle Configuration Manager services te stoppen op een site zonder de services afzonderlijk te hoeven stoppen.  

-   Wanneer u een site herstelt, kunt u de CHILDKEYS-optie gebruiken om de openbare sleutels te verdelen van meerdere onderliggende site naar de herstellende site.  

Om het hiërarchieonderhoud-hulpprogramma uit te voeren, moet de huidige gebruiker beheerderrechten hebben op de lokale computer. De gebruiker moet ook expliciet het sitebeheerderrecht hebben; het is niet voldoende dat de gebruiker dit recht erft door een lid te zijn van een groep die deze machtiging heeft.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Opdrachtregelopties voor het hiërarchieonderhoud-hulpprogramma  
Wanneer u het hiërarchieonderhoud-hulpprogramma gebruikt, moet u het lokaal uitvoeren op de centrale beheersite, de primaire site of de secundaire siteserver.  

Wanneer u het hiërarchie onderhoud-hulp programma uitvoert, moet u de volgende syntaxis gebruiken: preinst.&lt;exe\>/Option. Hieronder vindt u de opdrachtregelopties.  

 **> /DELJOB &lt; *site* ** code: gebruik deze optie op een site om alle taken of opdrachten van de huidige site naar de opgegeven doel site te verwijderen.  

 **> /DELSITE &lt; *ChildSiteCodeToRemove* ** : gebruik deze optie op een bovenliggende site om de gegevens voor onderliggende sites te verwijderen uit de site database van de bovenliggende site. U gebruikt deze optie typisch als een siteservercomputer buiten bedrijf gesteld wordt vóór u de site ervan verwijdert.  

> [!NOTE]  
>  De /DELSITE-optie maakt de installatie van de site op de computer, opgegeven door de ChildSiteCodeToRemove-parameter, niet ongedaan. Met deze optie worden alleen de site gegevens uit de Configuration Manager-site database verwijderd.  

/DUMP site code: gebruik deze optie op de lokale site server om de installatie kopieën van sites te schrijven naar de hoofdmap van het station waarop de site is geïnstalleerd. ** &lt; *SiteCode* > ** U kunt een specifieke sitebeheerinstallatiekopie schrijven naar de map of naar alle sitebeheerbestanden in de hiërarchie schrijven.  

-   /DUMP &lt; *site* code> schrijft alleen voor de opgegeven site de installatie kopie van het besturings element.  

-   /DUMP schrijft de sitebesturingsbestanden voor alle sites.  

Een afbeelding is een binaire weer gave van het site besturings bestand, dat is opgeslagen in de Configuration Manager-site database. De gedumpte installatiekopie van het sitebeheerbestand is een som van de basisinstallatiekopie plus de hangende installatiekopieën van de verschillen.  

Na het dumpen van een installatie kopie van een site besturings bestand met het hiërarchie onderhoud-hulp programma, is&lt;de bestands naam in de indeling sitectrl_*site* code>. ct0.  

**/STOPSITE** : gebruik deze optie op de lokale site server om een afsluit cyclus te initiëren voor de Configuration Manager site Component Manager-service, die de site gedeeltelijk opnieuw instelt. Wanneer deze afsluit cyclus wordt uitgevoerd, worden sommige Configuration Manager-services op een site server en de externe site systemen gestopt. Deze services zijn gemarkeerd voor opnieuw installeren. Tengevolge van deze afsluitcyclus, worden sommige wachtwoorden automatisch gewijzigd wanneer de services worden geïnstalleerd.  

> [!NOTE]  
>  Indien u een registratie wilt zien van afsluiten, herinstallatie en wachtwoordwijzigingen voor beheer van siteonderdelen, schakel dan de logboekregistratie in voor dit onderdeel door deze opdrachtregeloptie te gebruiken.  

Nadat de afsluitcyclus gestart is, loopt hij automatisch, waarbij hij niet-reagerende componenten of computers overslaat. Als de Beheer-van-siteonderdelen-service evenwel geen toegang kan krijgen tot een extern sitesysteem tijdens de afsluitcyclus, worden de onderdelen die zijn geïnstalleerd op het externe sitesysteem opnieuw geïnstalleerd wanneer de Beheer-van-de-siteonderdelen-service is gestart. Wanneer hij gestart is, probeert de Beheer-van-siteonderdelen-service herhaaldelijk de herinstallatie van alle services die gemarkeerd zijn voor herinstallatie, totdat hij erin slaagt.  

U kunt de Beheer-van-siteonderdelen-service opnieuw starten door gebruik te maken van sitebeheer. Nadat hij opnieuw gestart is, worden alle beïnvloede services verwijderd, opnieuw geïnstalleerd en opnieuw opgestart. Nadat u de /STOPSITE-optie gebruikt om de afsluitcyclus te initiëren, kunt u de cycli voor herinstallatie niet vermijden nadat de Beheer-van-siteonderdelen-service opnieuw gestart is.  

**/KEYFORPARENT**: gebruik deze optie op een site om de openbare sleutel van de site te distribueren naar een bovenliggende site.  

De optie/KEYFORPARENT plaatst de open bare sleutel van de site in het &lt;bestand *site* code>. CT4 in de hoofdmap van het station voor programma bestanden. Nadat u preinst. exe hebt uitgevoerd met deze optie, kopieert u &lt;de *site* code> hand matig. CT4-bestand naar de map. ..\Inboxes\hman.Box van de bovenliggende site (niet hman. box\pubkey).  

**/KEYFORCHILD**: gebruik deze optie op een site om de openbare sleutel van de site te verdelen naar een onderliggende site.  

De optie/KEYFORCHILD plaatst de open bare sleutel van de site in het &lt;bestand *site* code>. CT5 in de hoofdmap van het station voor programma bestanden. Nadat u preinst. exe hebt uitgevoerd met deze optie, kopieert u &lt;de *site* code> hand matig. CT5-bestand naar de map. ..\Inboxes\hman.Box van de onderliggende site (niet hman. box\pubkey).  

**/CHILDKEYS**: u kunt deze optie gebruiken op de onderliggende sites van een site die u herstelt. Gebruik deze optie om publieke sleutels te verdelen van meerdere onderliggende sites naar de herstellende site.  

De optie/CHILDKEYS plaatst de sleutel van de site waar u de optie uitvoert en alle open bare sleutels van de onderliggende sites van die sites in &lt;het bestand *site* code>. CT6.  

Nadat u preinst. exe hebt uitgevoerd met deze optie, kopieert u &lt;de *site* code> hand matig. CT6-bestand naar de map. ..\Inboxes\hman.Box van de site herstellen (niet hman. box\pubkey).  

**/PARENTKEYS**: u kunt deze optie gebruiken op de bovenliggende sites van een site die u herstelt. Gebruik deze optie om publieke sleutels te verdelen van meerdere bovenliggende sites naar de herstellende site.  

Met de optie/PARENTKEYS wordt de sleutel van de site waar u de optie uitvoert, en de sleutels van elke bovenliggende site boven die site in het &lt;bestand\>site code geplaatst. CT7.  

Nadat u preinst. exe hebt uitgevoerd met deze optie, kopieert u &lt;de *site* code> hand matig. CT7-bestand naar de map. ..\Inboxes\hman.Box van de site herstellen (niet hman. box\pubkey).  

##  <a name="manually-exchange-public-keys-between-sites"></a><a name="BKMK_ManuallyExchangeKeys"></a>Hand matig uitwisselen van open bare sleutels tussen sites  
Standaard is de optie **beveiligde sleutel uitwisseling vereisen** ingeschakeld voor Configuration Manager-sites. Wanneer uitwisseling van een beveiligde sleutel vereist is, zijn er twee situaties waarin u handmatig de initiële uitwisseling van de openbare sleutel tussen sites moet uitvoeren:  

-   Als het Active Directory schema niet is uitgebreid voor Configuration Manager  

-   Configuration Manager-sites publiceren geen site gegevens naar Active Directory  

U kunt het hiërarchieonderhoud-hulpprogramma gebruiken om de openbare sleutels te exporteren voor elke site. Eenmaal ze geëxporteerd werden, moet u handmatig de sleutels tussen de sites uitwisselen.  

> [!NOTE]  
>  Nadat de openbare sleutels handmatig zijn uitgewisseld, kunt u het logboekbestand **hman.log** controleren, dat siteconfiguratiewijzigingen registreert en sitegegevens publiceert naar Active Directory Domain Services, op de bovenliggende siteserver om te controleren of de primaire site de nieuwe openbare sleutel heeft verwerkt.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>Handmatig de openbare sleutel van de onderliggende site overdragen naar de bovenliggende site  

1.  Zorg dat u bent aangemeld bij de onderliggende site, open een opdrachtregel en navigeer naar de locatie van **Preinst.exe**.  

2.  Typ het volgende om de open bare sleutel van de onderliggende site te exporteren: **preinst/keyforparent**  

3.  De/keyforparent optie plaatst de open bare sleutel van de onderliggende site in de ** &lt;site\>code. Het CT4** -bestand bevindt zich in de hoofdmap van het systeem station.  

4.  De ** &lt;site code\>verplaatsen. CT4** -bestand naar de map ** &lt;\>\inboxes\hman.Box** van de bovenliggende site.  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>Handmatig de openbare sleutel van de bovenliggende site overdragen naar de onderliggende site  

1.  Zorg dat u bent aangemeld bij de bovenliggende site, open een opdrachtregel en navigeer naar de locatie van **Preinst.exe**.  

2.  Typ het volgende om de open bare sleutel van de bovenliggende site te exporteren: **preinst/keyforchild**.  

3.  De optie/keyforchild plaatst de open bare sleutel van de bovenliggende site in de ** &lt;site\>code. Het CT5** -bestand bevindt zich in de hoofdmap van het systeem station.  

4.  De ** &lt;site code\>verplaatsen. CT5** -bestand naar de ** &lt;map\>\inboxes\hman.Box installeren** op de onderliggende site.  

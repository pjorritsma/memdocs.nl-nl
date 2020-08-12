---
title: Updates en onderhoud
titleSuffix: Configuration Manager
description: Meer informatie over de service methode in de console, met de naam updates en onderhoud waarmee u gemakkelijk aanbevolen updates kunt zoeken en installeren.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3d8d9097b95a5daf06dc0260173e616fa2f88eb4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126134"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Updates en onderhoud voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager maakt gebruik van een in-console service methode met de naam **updates en onderhoud**. Met deze console methode kunt u eenvoudig aanbevolen updates voor uw Configuration Manager-infra structuur zoeken en installeren. Onderhoud in de console wordt aangevuld door out-of-band-updates, zoals hotfixes. De out-of-band-updates zijn bedoeld voor klanten die problemen moeten oplossen die mogelijk specifiek zijn voor hun omgeving.  

> [!TIP]  
> De voor waarden voor de *upgrade*, *Update*en *installatie* worden gebruikt om drie afzonderlijke concepten in Configuration Manager te beschrijven. Zie voor meer informatie over het gebruik van elke term [over upgrade, update en installatie](../../understand/upgrade-update-install.md).  

## <a name="baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Basislijn- en updateversies  

Gebruik de meest recente versie van de basislijn wanneer u een nieuwe site in een nieuwe hiërarchie installeert.

- Gebruik ook een basislijn versie voor een upgrade van System Center 2012 Configuration Manager.  

- Nadat u een upgrade hebt uitgevoerd naar Configuration Manager current branch, gebruikt u geen basislijn versies om actueel te blijven. In plaats daarvan gebruikt u alleen [updates in de console](install-in-console-updates.md) om naar de nieuwste versie bij te werken.  

- Er worden regel matig extra basislijn versies uitgebracht. Wanneer u de meest recente basislijn versie gebruikt om een nieuwe hiërarchie te installeren, voor komt u dat u een verouderde of niet-ondersteunde versie van Configuration Manager installeert, gevolgd door een extra upgrade van uw infra structuur om deze up-to-date te brengen.  

Nadat u een basislijnversie hebt geïnstalleerd, zijn aanvullende versies van Configuration Manager als updates beschikbaar in de console. Met de updates in de console wordt uw infrastructuur bijgewerkt naar de nieuwste versie van Configuration Manager.  

- U installeert de updates in de console om de versie van uw site op het hoogste niveau bij te werken.  

- Updates die u op de centrale beheer site installeert, worden automatisch geïnstalleerd op onderliggende primaire sites. Deze timing beheren door middel van een service venster op de primaire site. Zie [service Windows](service-windows.md)voor meer informatie.  

- Secundaire sites hand matig bijwerken naar een nieuwe update versie vanuit de-console.  

Wanneer u een update installeert, slaat de update installatie bestanden voor die versie op de site server op in een map met de naam **cd. Meest recente**. Zie de CD voor meer informatie over deze bestanden [. Meest recente map](the-cd.latest-folder.md).  

- Gebruik de bestanden in de CD. De meest recente map tijdens het herstel van de site. Wanneer uw hiërarchie geen basislijn versie meer uitvoert, kunt u ook deze bestanden gebruiken om extra sites te installeren.  

- U kunt geen installatie bestanden van CD gebruiken. Meest recente installatie van de eerste site van een nieuwe hiërarchie, of voor het upgraden van een site van System Center 2012 Configuration Manager.  

### <a name="version-details"></a>Details van versie

Sommige updates voor Configuration Manager zijn beschikbaar als updateversie in de console voor de bestaande infrastructuur en als nieuwe basislijnversie.  

#### <a name="supported-versions"></a>Ondersteunde versies

De volgende ondersteunde versies van Configuration Manager zijn momenteel beschikbaar als basis lijn, een update of beide:  

| Versie | Beschikbaarheidsdatum | [Einddatum voor de ondersteuning](current-branch-versions-supported.md) | Basislijn | Update in de console |  
|-------------|-----------|------------|--------------|------------------------|  
| [**2006**](../../plan-design/changes/whats-new-in-version-2006.md)<br /> (5.00.9012) | 11 augustus 2020 | 11 februari 2022 | Nee | Ja |
| [**2002**](../../plan-design/changes/whats-new-in-version-2002.md)<br /> (5.00.8968) | 1 april 2020 | 1 oktober 2021 | Ja,<sup>[Opmerking 1](#bkmk_note1)</sup> | Ja |
| [**1910**](../../plan-design/changes/whats-new-in-version-1910.md)<br /> (5.00.8913) | 29 november 2019 | 29 mei 2021 | Nee | Ja |
| [**1906**](../../plan-design/changes/whats-new-in-version-1906.md)<br /> (5.00.8853) | 26 juli 2019 | 26 januari 2021 | Nee | Ja |
| [**1902**](../../plan-design/changes/whats-new-in-version-1902.md)<br /> (5.00.8790) | 27 maart 2019 | 27 september 2020 | Ja | Ja |
| [**1810**](../../plan-design/changes/whats-new-in-version-1810.md)<br /> (5.00.8740) | 27 november 2018 | 1 december 2020 | Nee | Ja |

De **beschikbaarheids datum** is het moment waarop de [eerste update ring](checklist-for-installing-update-2006.md#early-update-ring) wordt uitgebracht. De basis lijn is beschikbaar op het Volume License Service Center nadat de update wereld wijd beschikbaar is.

<a name="bkmk_note1"></a>

> [!Note]  
> <sup>**Opmerking 1:**</sup> De basislijn media zijn beschikbaar als onderdeel van de volgende releases op het [Volume License Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC):
>
> - Micro soft endpoint ConfigMgr (huidige vertakking)
> - System Center Data Center
> - System Center Standard  
>
> Zoek bijvoorbeeld naar de VLSC voor `Microsoft Endpoint Configmgr (current branch)` . Zoek de basislijn media in de lijst met bestanden en down load voor die release.  

#### <a name="historical-versions"></a>Historische versies

De volgende tabel bevat historische versies van Configuration Manager huidige vertakking die niet meer worden ondersteund:

| Versie | Beschikbaarheidsdatum | Einddatum voor ondersteuning | Basislijn | Update in de console |  
|-------------|-----------|------------|--------------|------------------------|  
| **1806** <br /> (5.00.8692) | 31 juli 2018 | 31 januari 2020 | Nee | Ja |
| **1802** <br /> (5.00.8634) | 22 maart 2018 | 22 september 2019 | Ja | Ja |
| **1710** <br /> (5.00.8577) | 20 november 2017 | 20 mei 2019 | Nee | Ja |
| **1706** <br /> (5.00.8540) | 31 juli 2017 | 31 juli 2018 | Nee | Ja |
| **1702** <br /> (5.00.8498) | 27 maart 2017 | 27 maart 2018 | Ja | Ja |
| **1610** <br /> (5.00.8458) | 18 november 2016 | 18 november 2017 | Nee | Ja |
| **1606** <br /> (5.00.8412.1000) | 22 juli 2016 | 22 juli 2017 | Nee | Ja |
| **1606 met KB3186654** <br />5.00.8412.1307) | 12 oktober 2016 | 12 oktober 2017 | Ja | Nee |
| **1602** <br /> (5.00.8355) | 11 maart 2016 | 11 maart 2017 | Nee | Ja |
| **1511** <br /> (5.00.8325) | 8 december 2015 | 8 december 2016 | Ja | Nee |  

#### <a name="how-to-check-the-version"></a>De versie controleren

Als u de versie van uw Configuration Manager-site wilt controleren, gaat u in de-console naar de pagina **over Configuration Manager** in de linkerbovenhoek van de console. In dit dialoog venster worden de site-en console versies weer gegeven.  

> [!Note]  
> De console versie wijkt enigszins af van de versie van de site. De secundaire versie van de console komt overeen met de Configuration Manager Release versie. In Configuration Manager versie 1802 is de eerste site versie bijvoorbeeld 5.0.8634.1000 en is de oorspronkelijke console versie 5. **1802**. 1082,1700. De buildnummers (1082) en revisie (1700) kan veranderen met toekomstige hotfixes.

## <a name="in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Updates en onderhoud in de console  

Wanneer u een installatie van Configuration Manager current branch gebruikt die gereed is voor productie, zijn de meeste updates beschikbaar via het kanaal **updates en onderhoud** . Met deze methode worden de updates die van toepassing zijn op uw huidige infrastructuur versie en-configuratie geïdentificeerd, gedownload en beschikbaar gemaakt. Het bevat alleen updates die door micro soft worden aanbevolen voor alle klanten.

Deze updates zijn onder andere:  

- Nieuwe versies, zoals versie 1910, 2002 en 2006.

- Updates die nieuwe functies voor uw huidige versie bevatten.

- Hotfixes voor uw versie van Configuration Manager en die alle klanten moeten installeren.

    > [!Note]  
    > Vanaf versie 1902 hebben hotfixes in de console nu vervangings relaties. Zie [vervanging voor hotfixes in de console](#bkmk_supersede)voor meer informatie.

De updates in de console bieden een verbeterde stabiliteit en oplossingen voor algemene problemen. Ze vervangen de update typen voor eerdere product versies, zoals service packs, cumulatieve updates, hotfixes die van toepassing zijn op alle klanten en de uitbrei ding voor Microsoft Intune.

De updates in de console kunnen van toepassing zijn op een of meer van de volgende systemen:  

- Primaire en centrale beheersiteservers  

- Sitesysteemrollen en sitesysteemservers  

- Exemplaren van de SMS-provider  

- Configuration Manager-consoles  

- Configuration Manager-clients  

Configuration Manager detecteert nieuwe updates voor u. Synchroniseer uw Configuration Manager service-verbindings punt met de micro soft-Cloud service, waarbij u het volgende gedrag doet:  

- Wanneer uw service aansluitpunt zich in de online modus bevindt, synchroniseert uw site elke dag met micro soft. Er worden automatisch nieuwe updates geïdentificeerd die van toepassing zijn op uw infra structuur. Als u updates en herdistribueerbare bestanden wilt downloaden, gebruikt de computer die als host fungeert voor de site systeemrol van het service aansluitpunt de **systeem** context om toegang te krijgen tot de volgende Internet locaties: go.microsoft.com en download.Microsoft.com. Zie [vereisten voor Internet toegang](../deploy/configure/about-the-service-connection-point.md#bkmk_urls)voor meer informatie over aanvullende locaties die worden gebruikt door het service aansluitpunt.  

- Wanneer het service verbindings punt zich in de offline modus bevindt, gebruikt u het hulp programma voor service verbindingen om hand matig te synchroniseren met de micro soft-Cloud. Zie [het hulp programma voor service verbindingen gebruiken](use-the-service-connection-tool.md)voor meer informatie.  

- Dankzij de updates in de console is het niet meer nodig om individuele updates, servicepacks en nieuwe functies onafhankelijk van elkaar te zoeken en installeren.  

- Installeer alleen de console-updates die u hebt gekozen. Bij het installeren van sommige updates kunt u afzonderlijke functies selecteren om in te scha kelen en te gebruiken. Zie voor meer informatie [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

Wanneer u een update in de console installeert, wordt het volgende proces uitgevoerd:  

- De vereisten worden automatisch gecontroleerd. U kunt deze controle ook hand matig uitvoeren voordat u de installatie start.  

- Het wordt geïnstalleerd op de site op het hoogste niveau in uw omgeving. Deze site is de centrale beheer site als u er een hebt. In een hiërarchie wordt de update automatisch geïnstalleerd op primaire sites. Bepaal wanneer elke primaire site server mag bijwerken met behulp van [service Windows voor site servers](service-windows.md).  

- Nadat een site server is bijgewerkt, worden alle betrokken site systeem rollen automatisch bijgewerkt. Deze functies omvatten exemplaren van de SMS-provider. Nadat de update is geïnstalleerd, wordt de console gebruiker door Configuration Manager-consoles gevraagd de console bij te werken.  

- Als een update de Configuration Manager-client bevat, krijgt u de optie om de update in de pre-productie te testen of om de update onmiddellijk op alle clients toe te passen.  

- Nadat een primaire site is bijgewerkt, worden secundaire sites niet automatisch bijgewerkt. In plaats daarvan moet u de update van de secundaire site hand matig starten.  

> [!NOTE]  
> De Configuration Manager current branch, de Long-term Servicing Branch en de Technical Preview-vertakking zijn verschillende releases. Updates die van toepassing zijn op één vertakking zijn niet beschikbaar als updates in de console voor de andere branches. Zie voor meer informatie over beschik bare branches [welke vertakking van Configuration Manager moet ik gebruiken?](../../understand/which-branch-should-i-use.md).

### <a name="supersedence-for-in-console-hotfixes"></a><a name="bkmk_supersede"></a>Vervanging voor hotfixes in de console

<!-- 3229613 -->
Vanaf versie 1902 hebben hotfixes in de console nu vervangings relaties. Wanneer micro soft een nieuwe Configuration Manager hotfix publiceert, worden in de console geen hotfixes weer gegeven die door deze nieuwe hotfix worden vervangen. Met dit nieuwe gedrag kunt u beter bepalen welke hotfixes u wilt installeren.

### <a name="supersedence-example"></a>Vervangings voorbeeld

Er zijn drie hotfixes beschikbaar: hotfix-A, hotfix-B en hotfix-C. Hotfix-A wordt vervangen door hotfix-B en hotfix-B is vervangen door hotfix-C.

|Hotfix-A|Hotfix-B|Hotfix-C|Weer gave in console|
|--------|--------|--------|---------------|
|Niet geïnstalleerd|Niet geïnstalleerd|Niet geïnstalleerd|Alle drie hotfixes weer geven|
|Geïnstalleerd|Geïnstalleerd|Niet geïnstalleerd|Hotfix-B wordt weer gegeven als geïnstalleerd<br/>Hotfix-C wordt weer gegeven als gereed voor installatie|
|Niet geïnstalleerd|Niet geïnstalleerd|Geïnstalleerd|Hotfix-C wordt weer gegeven als geïnstalleerd|

## <a name="out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Out-of-band-hotfixes  

Sommige hotfixes worden uitgebracht met beperkte Beschik baarheid om specifieke problemen op te lossen. Andere hotfixes zijn van toepassing op alle klanten, maar kunnen niet worden geïnstalleerd met behulp van de console. Deze oplossingen worden out-of-band geleverd en worden niet gedetecteerd via de Microsoft-cloudservice.  

Wanneer u een probleem met uw implementatie van Configuration Manager wilt verhelpen of oplossen, kunt u informatie vinden over out-of-band-hotfixes van micro soft Customer Support Services, een micro soft Support Knowledge Base-artikel of [het Configuration Manager team blog](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog).

Installeer deze oplossingen hand matig met een van de volgende twee methoden:  

### <a name="update-registration-tool"></a>Hulp programma Registratie bijwerken

Met dit hulp programma wordt de hotfix hand matig in uw Configuration Manager-console geïmporteerd. Installeer vervolgens de update op dezelfde manier als in de console-updates die automatisch worden gedetecteerd.  

Deze methode wordt gebruikt voor hotfixes die gebruikmaken van de volgende bestandsnaam structuur:  
    `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

Zie [het hulp programma Registratie bijwerken gebruiken om hotfixes te importeren](use-the-update-registration-tool-to-import-hotfixes.md)voor meer informatie.  

### <a name="hotfix-installer"></a>Hotfix-installatie programma

Gebruik dit hulp programma om hand matig een hotfix te installeren die niet kan worden geïnstalleerd met behulp van de console.  

Deze methode wordt gebruikt voor oplossingen die gebruikmaken van de volgende bestandsnaam structuur:  
    `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

Zie het installatie programma voor [hotfixes gebruiken om updates te installeren](use-the-hotfix-installer-to-install-updates.md)voor meer informatie.  

## <a name="next-steps"></a>Volgende stappen

Aan de hand van de volgende artikelen wordt uitgelegd hoe u de verschillende update typen voor Configuration Manager kunt zoeken en installeren:  

- [Updates binnen de console installeren](install-in-console-updates.md)  

- [Het hulpprogramma voor serviceverbindingen gebruiken](use-the-service-connection-tool.md)  

- [Het hulp programma Registratie bijwerken gebruiken om hotfixes te importeren](use-the-update-registration-tool-to-import-hotfixes.md)  

- [Het installatie programma voor hotfixes gebruiken om updates te installeren](use-the-hotfix-installer-to-install-updates.md)  

Zie [Technical Preview](../../get-started/technical-preview.md)voor meer informatie over de vertakking Technical Preview.

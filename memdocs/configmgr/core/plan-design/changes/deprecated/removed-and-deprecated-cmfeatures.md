---
title: 'Verouderde functies:'
titleSuffix: Configuration Manager
description: Meer informatie over de functies die Configuration Manager niet meer wordt ondersteund.
ms.date: 08/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: aca9dc5c2ff2d88155ab19656f391cf87a4e977f
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068086"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Verwijderde en afgeschafte functies voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat een overzicht van de functies die zijn afgeschaft of verwijderd uit ondersteuning voor Configuration Manager. Afgeschafte functies worden verwijderd in een toekomstige update. Deze toekomstige wijzigingen kunnen van invloed zijn op uw gebruik van Configuration Manager.  

Deze informatie kan worden gewijzigd in toekomstige releases. De functie bevat mogelijk niet alle afgeschafte Configuration Manager-functies.

## <a name="deprecated-features"></a>Verouderde functies:

De volgende functies zijn afgeschaft. U kunt ze nu nog steeds gebruiken, maar micro soft wil de ondersteuning in de toekomst beëindigen.

|Functie|Afschaffing eerst aangekondigd|Ondersteuning &nbsp; verwijderd|
|-----------|---|--------------|
|De geografische weer gave in het knoop punt **site hiërarchie** van de werk ruimte **bewaking** in de Configuration Manager-console.<!--8116777-->|Augustus 2020|NOG TE BEPALEN|
|De implementatie voor het delen van inhoud van Azure is gewijzigd. Gebruik een Cloud beheer gateway die is ingeschakeld voor inhoud. U kunt in de toekomst geen traditioneel Cloud distributiepunt maken.|Februari 2019|TBD<sup>[Opmerking 1](#bkmk_note1)</sup>|
|Implementatie van de klassieke service naar Azure voor de Cloud beheer gateway en het Cloud distributiepunt. Zie [plan for CMG](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)voor meer informatie.|November 2018|TBD<sup>[Opmerking 1](#bkmk_note1)</sup>|

### <a name="note-1-support-removed-tbd"></a><a name="bkmk_note1"></a> Opmerking 1: ondersteuning verwijderd TBD

De specifieke periode moet worden bepaald (TBD). Micro soft raadt u aan het nieuwe proces of onderdeel te wijzigen, maar u kunt het afgeschafte proces of de verouderde functie voor de nabije toekomst blijven gebruiken.

## <a name="unsupported-and-removed-features"></a>Niet-ondersteunde en verwijderde functies

De volgende functies worden niet meer ondersteund. In sommige gevallen bevinden ze zich niet meer in het product.

|Functie|Afschaffing eerst aangekondigd|Ondersteuning &nbsp; verwijderd|  
|-----------|---|--------------|  
| Optie Desktop Analytics om **recente gegevens weer te geven** voor apparaatregistratie en beveiligings updates.<!-- 7080949 --> Zie [Data latentie](../../../../desktop-analytics/troubleshooting.md#data-latency)voor meer informatie.|Mei 2020|Juli 2020|
| Integratie van Windows Analytics en Upgradegereedheid. Zie [KB 4521815: Windows Analytics is buiten gebruik gesteld op 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement)voor meer informatie. | 14 oktober 2019 | 31 januari 2020 |
| Evaluatie van apparaatstatusverklaring voor nalevings beleid voor voorwaardelijke toegang <!--1235616 aka 3608202--> Zie [Wat is er gebeurd met hybride MDM](../../../../mdm/understand/what-happened-to-hybrid.md)voor meer informatie.| 3 juli 2019 | Versie 1910 |
| De app Configuration Manager Bedrijfsportal | 21 mei 2019 | Versie 1910 |
| De toepassings catalogus, met inbegrip van beide site systeem rollen: het Application catalog-website punt en het webservicepunt. Zie [de Application Catalog verwijderen](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)voor meer informatie. | 21 mei 2019 | Versie 1910 |
|Verificatie op basis van certificaten met instellingen voor Windows hello voor bedrijven in Configuration Manager<br>Zie [Windows hello voor bedrijven-instellingen](../../../../protect/deploy-use/windows-hello-for-business-settings.md)voor meer informatie.|December 2017|Versie 1910|
|System Center-Endpoint Protection voor Mac en Linux<br>Zie [End of support blog post](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257)voor meer informatie.|Oktober 2018|31 december 2018|
|On-premises voorwaardelijke toegang<br>Zie [Wat is er gebeurd met hybride MDM](../../../../mdm/understand/what-happened-to-hybrid.md)voor meer informatie.|30 januari 2019|1 september 2019|
|Hybrid Mobile Device Management (MDM)<br>Zie [Wat is er gebeurd met hybride MDM](../../../../mdm/understand/what-happened-to-hybrid.md)voor meer informatie.<br><br>Vanaf de 1902-release van de intune-service, die aan het einde van februari 2019 werd verwacht, kunnen nieuwe klanten geen nieuwe hybride verbinding maken.<!--Intune feature 2683117-->|14 augustus 2018|1 september 2019|
|SCAP-extensies (Security content Automation Protocol). <!--3607889--><br>De vorige gecertificeerde versie is nog steeds beschikbaar in het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=48741).|September 2018|Versie 1810|
|De **Silverlight-gebruikers ervaring** voor het Application catalog-website punt wordt niet meer ondersteund. Gebruikers moeten het nieuwe software Center gebruiken. Zie [Software Center configureren](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)voor meer informatie.<!--1358309-->|11 augustus 2017| Versie 1806|
|De vorige versie van software Center.<br><br>Zie [toepassings beheer plannen en configureren](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex)voor meer informatie over het nieuwe software Center.|13 december 2016|Versie 1802|
|Beheer van virtuele harde schijven (Vhd's) met Configuration Manager. <br><br>Deze afschaffing omvat het verwijderen van opties voor het maken van een nieuwe VHD of het beheren van een VHD met behulp van een taken reeks en het verwijderen van het knoop punt virtuele harde schijven van de Configuration Manager-console. <br><br>Bestaande Vhd's worden niet verwijderd, maar zijn niet langer toegankelijk vanuit de Configuration Manager-console.  |6 januari 2017 |Versie 1710|
|Taken reeksen: <br /> -Schijf naar dynamisch converteren <br /> -Implementatie Hulpprogramma's installeren |18 november 2016|Versie 1710|
|Upgrade beoordelings programma<br><br>Het hulp programma upgrade beoordeling is afhankelijk van Configuration Manager en de Application Compatibility Toolkit (ACT) 6. x. De definitieve versie van ACT werd geleverd in Windows 10 v1511 ADK. Omdat er geen verdere updates zijn om te handelen, wordt de ondersteuning voor het hulp programma upgrade beoordeling stopgezet. De aankondiging van de afschaffing is op 12 september 2016 toegevoegd aan de [Download pagina voor bedoeld](https://www.microsoft.com/software-download/windows10) . | 12 september 2016  | 11 juli 2017 |
|Software-update punten met een NLB-cluster (Network Load Balancing) | 27 februari 2016 | Versie 1702 |
|Taken reeksen: <br /> - OSDPreserveDriveLetter  <br /><br /> Tijdens de implementatie van een besturings systeem bepaalt Windows Setup nu de beste stationsletter die moet worden gebruikt (meestal C:). Als u een ander station wilt opgeven, kunt u de locatie wijzigen in de taken reeks stap besturings systeem Toep assen. Ga naar de **locatie selecteren waar u dit besturings systeem wilt Toep assen** . Selecteer een **specifieke logische stationsletter** en kies het station dat u wilt gebruiken. |20 juni 2016 |Versie 1606 |
|Netwerk toegangs beveiliging (NAP): zoals gevonden in System Center 2012 Configuration Manager|10 juli 2015|Versie 1511|  
|Buiten-band beheer-zoals gevonden in System Center 2012 Configuration Manager|16 oktober 2015|Versie 1511|

### <a name="features-removed-in-version-1511"></a>Verwijderde onderdelen in versie 1511

De volgende secties bevatten aanvullende informatie over functies die zijn verwijderd met versie 1511:

#### <a name="out-of-band-management"></a><a name="bkmk_amt"></a> Out-of-band-beheer  

Met Configuration Manager is systeem eigen ondersteuning voor op AMT gebaseerde computers vanuit de Configuration Manager-console verwijderd.  

- Op AMT gebaseerde computers blijven volledig beheerd wanneer u de [Intel SCS-invoeg toepassing voor Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html)gebruikt. De invoeg toepassing biedt u toegang tot de nieuwste mogelijkheden voor het beheren van AMT, terwijl het verwijderen van de beperkingen die zijn geïntroduceerd totdat Configuration Manager deze wijzigingen kan opnemen.  

- Buiten-band beheer in System Center 2012 Configuration Manager wordt niet beïnvloed door deze wijziging.  

#### <a name="network-access-protection"></a><a name="bkmk_nap"></a> Netwerk toegangs beveiliging

Configuration Manager heeft ondersteuning voor netwerk toegangs beveiliging verwijderd. De functie is afgeschaft in Windows Server 2012 R2 en wordt uit Windows 10 verwijderd.  

Bekijk het gedeelte *Afgeschafte functionaliteit* van [Overzicht van Services voor netwerkbeleid en -toegang](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11)) voor informatie over alternatieven voor netwerktoegangsbeveiliging.

## <a name="see-also"></a>Zie ook

- [Verwijderd en afgeschaft](removed-and-deprecated.md)
- [Microsoft Ondersteuning levenscyclus](https://support.microsoft.com/lifecycle)
- [Ondersteuning voor huidige branch-versies van Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)
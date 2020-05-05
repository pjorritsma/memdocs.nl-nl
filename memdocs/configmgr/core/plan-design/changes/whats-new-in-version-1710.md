---
title: Nieuwe versie 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1710 van Configuration Manager.
ms.date: 01/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 15735b015796d2cccfa9b0a24afc8f6eb0573df1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073616"
---
# <a name="what39s-new-in-version-1710-of-configuration-manager"></a>Wat&#39;s nieuw in versie 1710 van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1710 voor Configuration Manager current branch is beschikbaar als een update in de console voor eerder geïnstalleerde sites waarop versie 1610, 1702 of 1706 wordt uitgevoerd.

Afgezien van nieuwe functies bevat deze release ook aanvullende wijzigingen, zoals oplossingen voor problemen. Zie [overzicht van wijzigingen in Configuration Manager current branch, versie 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran)voor meer informatie.

De volgende aanvullende updates voor deze versie zijn nu ook beschikbaar:
- [Update pakket voor Configuration Manager current branch, versie 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Update pakket 2 voor Configuration Manager current branch versie 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Als u een nieuwe site wilt installeren, moet u een basislijn versie van Configuration Manager gebruiken.  
>
> Meer informatie over:    
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)  
> - [Updates installeren op sites](../../servers/manage/updates.md)  
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)

De volgende secties bevatten informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1710 van Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Site-infra structuur

### <a name="updates-for-peer-cache-----sms500850---"></a>Updates voor peer-cache  <!-- sms500850 -->
Vanaf deze release is peer-cache geen functie meer van de voorlopige versie.  Er zijn geen andere wijzigingen voor peer-cache geïntroduceerd in deze release. Zie [peer-cache voor Configuration Manager-clients](../hierarchy/client-peer-cache.md)voor meer informatie.

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Ondersteuning voor Cloud distributiepunt voor Azure Government Cloud   <!-- sms491428 -->
U kunt nu [cloud-gebaseerde distributie punten](../hierarchy/use-a-cloud-based-distribution-point.md) gebruiken in de Azure Government Cloud.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Revisie standaard eenheid inventaris <!-- sms503697 -->
Als apparaten nu harde schijven bevatten met een grootte van Gigabyte (GB), terabyte (TB) en grotere schalen, wijzigt deze release de standaard eenheid (SMS_Units) die in veel weer gaven wordt gebruikt van mega bytes (MB) tot GB. Bijvoorbeeld, de v_gs_LogicalDisk. vrije ruimte-waarde rapporteert nu GB-eenheden.


<!-- ## Migration  -->


## <a name="client-management"></a>Clientbeheer

### <a name="co-management-for-windows-10-devices"></a>Co-beheer voor Windows 10-apparaten    
<!-- 1350871 -->
In de vorige Windows 10-updates kunt u al een Windows 10-apparaat samen voegen met on-premises Active Directory (AD) en op de cloud gebaseerde Azure AD op hetzelfde moment (hybride Azure AD). Met ingang van Configuration Manager versie 1710 maakt co-beheer gebruik van deze verbetering en kunt u gelijktijdig Windows 10, versie 1709 (ook wel de update van de herfst-makers) beheren met zowel Configuration Manager als intune. Het is een oplossing die een brug biedt van traditioneel naar modern beheer en biedt u een pad om de overgang te maken met behulp van een gefaseerde benadering. Zie voor meer informatie [co-beheer voor Windows 10-apparaten](../../../comanage/overview.md).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Computers opnieuw opstarten via de Configuration Manager-console  <!-- 1356283 -->
Vanaf deze release kunt u de Configuration Manager-console gebruiken om client apparaten te identificeren waarvoor opnieuw moet worden opgestart en vervolgens een client meldings actie te gebruiken om ze opnieuw te starten.

Zie [clients beheren](../../clients/manage/manage-clients.md#restart-clients)


<!-- ## Compliance settings -->


## <a name="application-management"></a>Beheer van toepassingen
### <a name="improvements-for-run-scripts------1236459---"></a>Verbeteringen voor het uitvoeren van scripts   <!-- 1236459 -->
Deze release brengt diverse verbeteringen aan in de functie **scripts uitvoeren** , waarmee u Power shell-scripts kunt implementeren voor uitvoering op beheerde apparaten. Deze functie werd voor het eerst geïntroduceerd in versie 1706.

De verbeteringen zijn onder andere:
- Beveiligingsbereiken gebruiken om te bepalen wie run scripts mag gebruiken
- Real-time bewaking van de scripts die u uitvoert
- Para meters voor de script weer geven in de wizard script maken, ondersteuning voor validatie en worden aangeduid als verplicht of optioneel.

Zie [scripts maken en uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md)voor meer informatie over het gebruik van scripts uitvoeren.

### <a name="new-mobile-application-management-policy-settings"></a>Nieuwe Mobile Application Management-beleids instellingen
<!-- 1324760 -->
De volgende instellingen zijn toegevoegd aan de Mobile Application Management-beleids instellingen:
- **Synchronisatie van contact personen uitschakelen**: hiermee voor komt u dat de app gegevens opslaat in de systeem eigen contact personen-app op het apparaat.
- **Afdrukken uitschakelen**: hiermee voor komt u dat de app werk-of school gegevens afdrukt.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Met Software Center worden pictogrammen die groter zijn dan 250x250 niet meer vervormd  
<!-- 1356194 -->

Met deze versie vervormt Software Center niet langer pictogrammen die groter zijn dan 250x250. Met Software Center worden dergelijke pictogrammen wazig weer gegeven. U kunt nu een pictogram met een pixel afmetingen van Maxi maal 512 x 512 instellen en het wordt zonder vervorming weer gegeven.

Zie [toepassingen maken](../../../apps/deploy-use/create-applications.md)voor informatie over het toevoegen van een pictogram voor uw app in Software Center.

## <a name="operating-system-deployment"></a>Implementatie van besturingssystemen
 > [!TIP]   
 > <!-- 1354281 -->
 > Vanaf de release van Windows 10, versie 1709 (ook wel bekend als de update voor het najaar van makers), bevat Windows Media meerdere edities. Bij het configureren van een taken reeks voor het gebruik van een upgrade pakket voor een besturings systeem of een installatie kopie van een besturings systeem, moet u ervoor zorgen dat u een [editie selecteert die wordt ondersteund voor gebruik door Configuration Manager](../configs/support-for-windows-10.md#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Onderliggende taken reeksen toevoegen aan een taken reeks
<!-- 1261338 -->

U kunt een nieuwe taken reeks stap toevoegen die een andere taken reeks uitvoert, waarmee een bovenliggende/onderliggende relatie tussen de taken reeksen wordt gemaakt. Zo kunt u meer modulaire taken reeksen maken die u opnieuw kunt gebruiken.  

Zie voor meer informatie over de onderliggende taken reeks [onderliggende taken reeks](../../../osd/understand/task-sequence-steps.md#child-task-sequence).

## <a name="software-center-customization"></a>Aanpassing van software Center
<!-- 1351224 -->
U kunt huisstijl elementen voor ondernemingen toevoegen en de zicht baarheid van tabbladen in Software Center opgeven. U kunt uw specifieke bedrijfs naam voor Software Center toevoegen, een kleuren thema voor het configureren van software Centers instellen, een bedrijfs logo instellen en de zicht bare tabbladen voor client apparaten instellen.

Zie [toepassings beheer plannen en configureren](../../../apps/plan-design/plan-for-and-configure-application-management.md)voor meer informatie.

## <a name="software-updates"></a>Software-updates

### <a name="surface-driver-updates-----1098490---"></a>Updates van Surface-Stuur Programma's  <!-- 1098490 -->
Vanaf deze release is het beheer van updates voor het oppervlakte stuur programma niet langer een functie van de voorlopige versie.  


## <a name="reporting"></a>Rapporten

### <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Beperk de uitgebreide Windows 10-gegevens zodat alleen gegevens worden verzonden die relevant zijn voor Windows Analytics Apparaatstatus
<!-- 1356148 -->

U kunt nu het verzamelings niveau voor het verzamelen van diagnostische gegevens van Windows 10 instellen op **uitgebreid (beperkt)**. Met deze instelling kunt u geavanceerde inzichten krijgen over apparaten in uw omgeving zonder dat apparaten alle gegevens in het **verbeterde** niveau rapporteren met Windows 10 versie 1709 of hoger.

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Beheer van mobiele apparaten

### <a name="actions-for-non-compliance"></a>Acties voor niet-naleving 
<!--1321366 -->    
U kunt nu een op tijd geordende reeks acties configureren die worden toegepast op apparaten die niet meer compatibel zijn. U kunt bijvoorbeeld gebruikers op de hoogte stellen van niet-compatibele apparaten via e-mail of deze apparaten markeren als niet-compatibel.

### <a name="windows-10-arm64-device-support"></a>Ondersteuning voor Windows 10 ARM64-apparaten
<!-- 1355000 -->

Hybride Mobile Device Management-scenario's (MDM) worden ondersteund op ARM64-apparaten met Windows 10 wanneer deze apparaten beschikbaar zijn.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Verbeterde VPN-profiel ervaring in Configuration Manager-console 
<!-- 1318232 -->

In deze release hebben we de wizard VPN-profiel en eigenschappen bijgewerkt om de instellingen weer te geven die geschikt zijn voor het geselecteerde platform:


- Elk platform heeft zijn eigen werk stroom, wat betekent dat nieuwe VPN-profielen alleen de instelling bevatten die door het platform wordt ondersteund.
- De pagina **ondersteunde platforms** wordt nu weer gegeven na de pagina **Algemeen** .  U kiest nu het platform voordat u eigenschaps waarden instelt.
- Wanneer het platform is ingesteld op **Android**, **Android for Work**of **Windows Phone 8,1**, is de pagina met **ondersteunde platforms** niet nodig en wordt deze niet weer gegeven.
- De Configuration Manager werk stroom op de client is gecombineerd met de op clients gebaseerde Windows 10-werk stromen op basis van het Hybrid Mobile Device (MDM). ze ondersteunen dezelfde instellingen.
- Elke werk stroom van het platform bevat alleen de instellingen die geschikt zijn voor die werk stroom.  De Android-werk stroom bevat bijvoorbeeld instellingen die geschikt zijn voor Android. de juiste instellingen voor iOS of Windows 10 Mobile worden niet meer weer gegeven in de Android-werk stroom.
- De automatische VPN-pagina is verouderd en is verwijderd.

Deze wijzigingen zijn van toepassing op nieuwe VPN-profielen.  

Bestaande VPN-profielen worden ongewijzigd om het compatibiliteits risico te minimaliseren.  Wanneer u een bestaand profiel bewerkt, worden de instellingen weer gegeven zoals tijdens het maken van het profiel.  

Zie [VPN-profielen op mobiele apparaten](../../../protect/deploy-use/vpn-profiles.md)voor meer informatie.

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Beperkte ondersteuning voor crypto grafie: Next Generation-certificaten (CNG) <!-- 1356191 -->

Configuration Manager heeft beperkte ondersteuning voor crypto grafie: Next Generation (CNG)-certificaten. Configuration Manager-clients kunnen een PKI-certificaat voor client verificatie gebruiken met een persoonlijke sleutel in de SLEUTELARCHIEFPROVIDER. Met de SLEUTELARCHIEFPROVIDER-ondersteuning ondersteunen Configuration Manager-clients op hardware gebaseerde persoonlijke sleutel, zoals TPM-SLEUTELARCHIEFPROVIDER voor PKI-client verificatie certificaten.

Zie voor meer informatie [overzicht CNG-certificaten](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Apparaten beveiligen

### <a name="create-and-deploy-exploit-guard-policies"></a>Exploit Guard-beleids regels maken en implementeren
<!-- 1355468 -->

U kunt [beleids regels maken en implementeren](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) voor het beheren van alle vier onderdelen van Windows Defender exploit Guard, waaronder de kwets baarheid voor aanvallen, Controlled folder Access, exploit Protection en netwerk beveiliging.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Windows Defender Application Guard-beleid maken en implementeren
<!-- 1351960 -->

U kunt [Windows Defender Application Guard-beleids regels maken en implementeren](../../../protect/deploy-use/create-deploy-application-guard-policy.md) met behulp van de Configuration Manager Endpoint Protection.

### <a name="device-guard-policy-changes"></a>Wijzigingen in Device Guard-beleid
<!-- 1355092 -->
De volgende drie wijzigingen zijn aangebracht in verband met het Device Guard-beleid:

- De naam van het Device Guard-beleid is gewijzigd in Windows Defender Application Control-beleid. De **wizard Device Guard-beleid maken** heeft nu bijvoorbeeld de naam **wizard Windows Defender-toepassings beheer beleid maken**.
- Voor apparaten die de update voor het najaar van makers van Windows versie 1709 gebruiken, hoeft u niet opnieuw op te starten om het Windows Defender Application Control-beleid toe te passen. Opnieuw opstarten is nog steeds de standaard instelling, maar u kunt het [opnieuw opstarten uitschakelen](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).
- U kunt [apparaten instellen om automatisch software uit te voeren](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) die wordt vertrouwd door de Intelligent Security Graph.





## <a name="next-steps"></a>Volgende stappen
Wanneer u klaar bent om deze versie te installeren, raadpleegt u [updates voor Configuration Manager](../../servers/manage/updates.md).

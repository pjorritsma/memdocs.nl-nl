---
title: Interoperabiliteit tussen versies
titleSuffix: Configuration Manager
description: Meer informatie over het voor komen van conflicten tussen meerdere Configuration Manager-hiërarchieën op hetzelfde netwerk.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8d5eeeeafa775514bb46fa0906f22572343611d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713084"
---
# <a name="interoperability-between-different-versions-of-configuration-manager"></a>Interoperabiliteit tussen verschillende versies van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt meerdere, onafhankelijke hiërarchieën van Configuration Manager op hetzelfde netwerk installeren en bewerken. Omdat verschillende hiërarchieën van Configuration Manager niet buiten het migratie proces worden uitgevoerd, vereist elke hiërarchie configuraties om conflicten ertussen te voor komen. Daarnaast kunt u bepaalde configuraties maken om resources te helpen die u beheert met de site systemen van de juiste hiërarchie.  

## <a name="interoperability-between-current-branch-and-earlier-versions"></a><a name="BKMK_SupConfigInterop"></a>Interoperabiliteit tussen de huidige vertakking en eerdere versies  

Sites van verschillende versies kunnen niet naast elkaar bestaan in dezelfde Configuration Manager hiërarchie. De enige uitzonde ringen zijn tijdens het proces van de volgende upgrade scenario's:

- Van System Center 2012 Configuration Manager Configuration Manager huidige branch
- Van een Configuration Manager huidige branch-versie naar een nieuwere versie met behulp van de updates in de console

U kunt een Configuration Manager huidige branch-site en-hiërarchie naast elkaar implementeren met een bestaande System Center 2012 Configuration Manager-site of-hiërarchie. Plan om te voor komen dat clients van een van beide versies proberen een site toe te voegen vanuit de andere versie.

Als bijvoorbeeld twee of meer Configuration Manager-hiërarchieën [overlappende grenzen](../../servers/deploy/configure/boundary-groups.md#overlapping-boundaries) hebben die dezelfde netwerk locaties bevatten, wijst u elke nieuwe client toe aan een specifieke site in plaats van automatische site toewijzing te gebruiken. Zie [clients toewijzen aan een site](../../clients/deploy/assign-clients-to-a-site.md)voor meer informatie.  

Daarnaast kunt u geen-client installeren vanuit System Center 2012 Configuration Manager op een computer die als host fungeert voor een site systeemrol van Configuration Manager huidige vertakking. U kunt ook geen Configuration Manager huidige branch-client installeren op een computer die als host fungeert voor een site systeemrol van System Center 2012 Configuration Manager.  

De volgende clients en verbindingen worden niet ondersteund:  

- Alle versies van System Center 2012 Configuration Manager of eerder computer-client  

- Alle System Center 2012 Configuration Manager of eerder Device Management-client  

- Device Management-client voor Windows CE platform Builder (wille keurige versie)  

- System Center Mobile Device Manager VPN-verbinding  

### <a name="client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> Overwegingen voor de sitetoewijzing van de client  

Configuration Manager-clients kunnen slechts worden toegewezen aan één primaire site. U kunt de werkelijke site toewijzing van een client niet voors pellen wanneer aan alle volgende voor waarden wordt voldaan:

- U gebruikt automatische site toewijzing om clients toe te wijzen aan een site tijdens de client installatie
- Meer dan één grens groep bevat dezelfde grens
- De grens groepen hebben verschillende toegewezen sites

Als grenzen voor meerdere Configuration Manager-sites en-hiërarchieën overlappen, zijn clients mogelijk niet toegewezen aan de site die u verwacht of worden deze mogelijk niet toegewezen aan een site.  

Configuration Manager huidige branch-clients controleren de versie van de site voordat ze de site toewijzing volt ooien. Als site grenzen elkaar overlappen, kunt u geen clients toewijzen aan een site met een vorige versie. Het is echter mogelijk dat eerdere System Center 2012-Configuration Manager-clients onjuist worden toegewezen aan een latere Configuration Manager huidige branch-site.  

Als u wilt voor komen dat clients per ongeluk worden toegewezen aan de verkeerde site wanneer twee hiërarchieën overlappende grenzen hebben, configureert u client installatie parameters om clients toe te wijzen aan een specifieke site.  

## <a name="configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a>Configuration Manager beperkingen in een gemengde hiërarchie  

Wanneer u een upgrade van een Configuration Manager huidige vertakkings hiërarchie uitvoert, zijn er situaties waarin verschillende-sites verschillende versies hebben. U kunt bijvoorbeeld eerst een upgrade uitvoeren van de centrale beheer site. Vanwege het onderhouds venster van de site werkt u de primaire sites niet bij tot een later tijdstip en een nieuwe datum.  

Wanneer verschillende-sites in één hiërarchie verschillende versies uitvoeren, zijn bepaalde functies niet beschikbaar. Dit gedrag kan van invloed zijn op de manier waarop u Configuration Manager objecten beheert in de Configuration Manager-console, en welke functionaliteit beschikbaar is voor clients. Normaal gesp roken is de functionaliteit van de nieuwere versie van Configuration Manager niet toegankelijk op sites of voor clients die een lagere versie van het Service Pack uitvoeren.  

### <a name="network-access-account"></a>Netwerktoegangsaccount

U werkt de centrale beheer site bij naar Configuration Manager huidige vertakking. U kunt de details van het netwerk toegangs account weer geven vanuit een Configuration Manager-console die is verbonden met deze bijgewerkte site. Er worden geen account gegevens weer gegeven van sites die nog steeds System Center 2012 Configuration Manager uitvoeren.

Nadat u de primaire site hebt bijgewerkt naar dezelfde versie als de centrale beheer site, zijn de account details zichtbaar in de-console.

Hetzelfde gedrag geldt wanneer u bijwerkt tussen versies van Configuration Manager.

### <a name="boot-images-for-os-deployment"></a>Opstart installatie kopieën voor besturingssysteem implementatie

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-configuration-manager-current-branch"></a>Bij de upgrade van System Center 2012 Configuration Manager naar Configuration Manager huidige branch

Wanneer de site op het hoogste niveau van een hiërarchie wordt bijgewerkt naar Configuration Manager huidige vertakking, worden de standaard opstart installatie kopieën automatisch bijgewerkt voor gebruik van de Windows Assessment and Deployment Kit (ADK) versie 10. Gebruik deze opstart installatie kopieën alleen voor implementaties naar clients op Configuration Manager huidige branch-sites. Zie [planning voor interoperabiliteit van besturingssysteem implementatie](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md)voor meer informatie.

#### <a name="when-upgrading-between-configuration-manager-current-branch-versions"></a>Bij de upgrade tussen Configuration Manager huidige branch-versies

Zolang de nieuwe versies van Configuration Manager de versie van Windows ADK die in gebruik is, niet bijwerken, is dit niet van invloed op installatie kopieën.

### <a name="new-task-sequence-steps"></a>Stappen voor nieuwe takenreeksen

Wanneer u een taken reeks maakt met een stap die is geïntroduceerd in één versie van Configuration Manager die niet beschikbaar is in een eerdere versie, kunnen de volgende problemen optreden:

- Er treedt een fout op wanneer u de taken reeks probeert te bewerken vanaf een site waarop een eerdere versie van Configuration Manager.

- De taken reeks wordt niet uitgevoerd op een computer waarop een eerdere versie van de Configuration Manager-client wordt uitgevoerd.

### <a name="client-to-down-level-management-point-communications"></a>Communicatie van client naar Down Level-beheer punt

Een Configuration Manager-client die communiceert met een beheer punt vanaf een site waarop een lagere versie wordt uitgevoerd dan de client, kan alleen gebruikmaken van de functionaliteit die de versie van het lagere niveau van Configuration Manager ondersteunt. Als u bijvoorbeeld inhoud implementeert vanuit een Configuration Manager huidige branch-site die onlangs is bijgewerkt naar een client die communiceert met een beheer punt dat nog niet is bijgewerkt naar die versie, kan die client geen nieuwe functionaliteit van de nieuwste versie gebruiken.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Pakket-en taken reeks implementaties voor verouderde clients

<!-- SCCMDocs-pr issue #3493 -->

Vanaf versie 1902 kunt u geen pakket of taken reeks implementeren naar een client versie 5,7730 of eerder. U kunt deze beperking omzeilen door de client bij te werken naar een nieuwere versie.

## <a name="software-updates"></a>Software-updates

### <a name="orchestration-groups"></a>Orchestration-groepen

Orchestration-groepen, geïntroduceerd in versie 2002, kunnen niet worden gebruikt in een gemengde hiërarchie. <!--SCCMDocs-pr issue ##5056, 6389000-->

## <a name="interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a>Interoperabiliteit voor de Configuration Manager-console  

Deze sectie bevat informatie over het gebruik van de Configuration Manager-console in een omgeving met een combi natie van Configuration Manager versies.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-configuration-manager-current-branch"></a>Een omgeving met zowel System Center 2012 Configuration Manager als Configuration Manager huidige branch

Als u een Configuration Manager site wilt beheren, moet de-console en de site waarmee de console verbinding maakt, dezelfde versie van Configuration Manager uitvoeren. U kunt bijvoorbeeld geen System Center 2012 Configuration Manager-console gebruiken om een Configuration Manager huidige branch-site te beheren of de andere manier.

Het is niet mogelijk om zowel de System Center 2012 Configuration Manager-console als de Configuration Manager huidige branch-console op dezelfde computer te installeren.

### <a name="an-environment-with-multiple-versions-of-configuration-manager"></a>Een omgeving met meerdere versies van Configuration Manager

Configuration Manager huidige branch ondersteunt het installeren van meer dan één Configuration Manager-console op een computer niet. Om meerdere consoles te gebruiken die specifiek zijn voor verschillende versies van Configuration Manager, installeert u de verschillende consoles op afzonderlijke computers.

Tijdens het proces van het bijwerken van sites in een hiërarchie naar een nieuwe versie, kunt u een-console verbinden met een site waarop een nieuwere versie wordt uitgevoerd en informatie over andere sites in die hiërarchie weer geven. Deze configuratie wordt echter niet aanbevolen. Het is mogelijk dat verschillen tussen de console versie en Configuration Manager site versie kunnen leiden tot gegevens problemen. Sommige functies die beschikbaar zijn in de nieuwste product versie, zijn niet beschikbaar in de-console.

Het is niet mogelijk om een site te beheren wanneer u een-console gebruikt met een versie die niet overeenkomt met de versie van de site. Dit kan leiden tot verlies van gegevens, waardoor uw site risico loopt. Het is bijvoorbeeld niet mogelijk om een-console van versie 1610 te gebruiken voor het beheren van een site waarop versie 1606 wordt uitgevoerd.

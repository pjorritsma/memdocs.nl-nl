---
title: Voorbeeld scenario voor het implementeren en controleren van updates
titleSuffix: Configuration Manager
description: Software-updates in Configuration Manager gebruiken om maandelijkse software-updates te implementeren en te controleren.
ms.date: 10/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ea654c4ec13b95b78a65c85d9d36ce576619854e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714911"
---
# <a name="example-scenario-to-deploy-and-monitor-monthly-software-updates"></a>Voorbeeld scenario voor het implementeren en controleren van maandelijkse software-updates

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit onderwerp vindt u een voorbeeld scenario van hoe u software-updates in Configuration Manager kunt gebruiken om de beveiligings updates te implementeren en te controleren die micro soft maandelijks heeft uitgebracht.  

 In dit scenario volgen we de acties van de Configuration Manager-beheerder bij Woodgrove Bank. De beheerder moet een implementatie strategie voor software-updates maken met de volgende voor waarden en vereisten:  

- Actieve implementatie van software-updates vindt plaats één week nadat Microsoft de beveiligingsupdates publiceert op de tweede dinsdag van elke maand, de welbekende 'patchdinsdag'.  

- Software-updates worden gedownload en voorbereid op distributiepunten. Vervolgens wordt een implementatie getest op een subset van clients voordat de ConfigMgr-beheerder de software-updates volledig implementeert in zijn productie omgeving.  

- De beheerder moet de naleving van de software-updates per maand of per jaar kunnen bewaken.  

  In dit scenario wordt aangenomen dat de infrastructuur van het software-updatepunt al is geïmplementeerd. Gebruik de volgende informatie voor het plannen en configureren van software-updates in Configuration Manager.  

|Proces|Naslaginformatie|  
|-------------|---------------|  
|De belangrijkste concepten voor software-updates doornemen.|[Inleiding tot software-updates](../understand/software-updates-introduction.md)|  
|Software-updates plannen. Met deze informatie kunt u rekening houden met capaciteitsoverwegingen, de infrastructuur van het software-updatepunt, de installatie van het software-updatepunt, synchronisatie-instellingen en clientinstellingen voor software-updates bij het maken van een planning.|[Software-updates plannen](../plan-design/plan-for-software-updates.md)|  
|Software-updates configureren. Met deze informatie kunt u software-updatepunten in uw hiërarchie installeren en configureren, en kunt u software-updates configureren en synchroniseren.<br /><br /> In dit scenario configureert de ConfigMgr-beheerder de synchronisatie planning voor software-updates op de tweede woensdag van elke maand om ervoor te zorgen dat ze de nieuwste beveiligings software-updates van micro soft ophalen.|[Software-updates synchroniseren](../get-started/synchronize-software-updates.md)|  

 De volgende secties in dit onderwerp bevatten voorbeeld stappen om u te helpen bij het implementeren en bewaken van Configuration Manager beveiligings software-updates in uw organisatie.

##  <a name="step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a>Stap 1: een software-update groep voor jaarlijkse naleving maken  
 De Configuration Manager beheerder maakt een software-update groep die kan worden gebruikt om de naleving te bewaken voor alle beveiligings updates die ze hebben uitgebracht in 2016. De beheerder voert de stappen uit in de volgende tabel.  

|Proces|Naslaginformatie|  
|-------------|---------------|  
|Vanuit het knoop punt **alle software-updates** in de Configuration Manager-console voegt de Configuration Manager beheerder criteria toe voor het weer geven van alleen beveiligings software-updates die zijn uitgebracht of bijgewerkt in jaar 2015 die voldoen aan de volgende criteria:<br /><br /><ul><li>**Criterium**: publicatie- of revisiedatum</li><li>**Voorwaarde**: is groter dan of gelijk aan een specifieke datum<br />**Waarde**: 1/1/2015</li><li>**Criterium**: updateclassificatie<br />**Waarde**: beveiligingsupdates</li><li>**Criterium**: verlopen <br />**Waarde**: nee</li></ul>|Geen aanvullende informatie|
|ConfigMgr-beheerder voegt alle gefilterde software-updates toe aan een nieuwe software-update groep met de volgende vereisten:<br /><br /><ul><li>**Naam**: nalevingsgroep - Microsoft-beveiligingsupdates 2015</li><li>**Beschrijving**: software-updates|[Software-updates toevoegen aan een updategroep](add-software-updates-to-an-update-group.md)|  

##  <a name="step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a>Stap 2: een regel voor automatische implementatie maken voor de huidige maand  
 De Configuration Manager beheerder maakt een regel voor automatische implementatie voor de beveiligings updates die door micro soft voor de huidige maand worden uitgebracht. De beheerder voert de stappen uit in de volgende tabel.  

|Proces|Naslaginformatie|  
|-------------|---------------|  
|ConfigMgr-beheerder maakt een regel voor automatische implementatie met de volgende vereisten:<br /><br /><ol><li>Op het tabblad **Algemeen** configureert de ConfigMgr-beheerder het volgende:<br /> <ul><li>Hiermee geeft u de **maandelijkse beveiligings updates** voor de naam op.</li><li>Hiermee selecteert u een test verzameling met beperkte clients.</li><li>Hiermee selecteert u **een nieuwe software-update groep maken**.</li><li>Controleert of **de implementatie inschakelen nadat deze regel is uitgevoerd** niet is geselecteerd.</li></ul></li><li>Op het tabblad **implementatie-instellingen** selecteert de ConfigMgr-beheerder de standaard instellingen.</li><li>Op de pagina **software-updates** configureert de ConfigMgr-beheerder de volgende eigenschappen filters en zoek criteria:<br /><ul><li>Publicatie- of revisiedatum **Afgelopen maand**.</li><li>Updateclassificatie **Beveiligingsupdates**.</li></ul></li><li>Op de pagina **evaluatie** kan de ConfigMgr-beheerder de regel uitvoeren volgens een schema voor de **tweede donderdag** van elke **maand**.  De ConfigMgr-beheerder controleert ook of zijn synchronisatie planning is ingesteld voor uitvoering op de **tweede woensdag** van elke **maand**.</li><li>De ConfigMgr-beheerder gebruikt de standaard instellingen op de pagina's implementatie planning, gebruikers ervaring, waarschuwingen en Download instellingen.</li><li>Op de pagina **implementatie pakket** geeft de ConfigMgr-beheerder een nieuw implementatie pakket op.</li><li>De ConfigMgr-beheerder gebruikt de standaard instellingen op de pagina's Download locatie en taal selecteren.</li></ol>|[Software-updates automatisch implementeren](automatically-deploy-software-updates.md)|  

##  <a name="step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a>Stap 3: controleren of software-updates gereed zijn voor implementatie  
 Op de tweede donderdag van elke maand controleert de ConfigMgr-beheerder of de software-updates gereed zijn voor implementatie. De beheerder voert de volgende stap uit.  

|Proces|Naslaginformatie|  
|-------------|---------------|  
|De ConfigMgr-beheerder controleert of de synchronisatie van software-updates is voltooid.|[Synchronisatiestatus van software-updates](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a>Stap 4: de software-update groep implementeren  
 Nadat de ConfigMgr-beheerder heeft gecontroleerd of de software-updates gereed zijn voor implementatie, implementeren ze de software-updates. De beheerder voert de stappen uit in de volgende tabel.  

|Proces|Naslaginformatie|  
|-------------|---------------|  
|De ConfigMgr-beheerder maakt twee test implementaties voor de nieuwe software-update groep. De beheerder beschouwt de volgende omgevingen voor elke implementatie:<br /><br /> **Implementatie van werk station testen**: de ConfigMgr-beheerder beschouwt het volgende voor de test implementatie van het werk station:<br /><br /><ul><li>Hiermee geeft u een implementatie verzameling op die een subset van Workstation-clients bevat om de implementatie te controleren.</li><li>Hiermee configureert u de implementatie-instellingen die geschikt zijn voor de Workstation-clients in zijn omgeving.</li></ul><br />**Test implementatie**van de server: de ConfigMgr-beheerder beschouwt het volgende voor de test implementatie van de server:<br /><br /><ul><li>Hiermee geeft u een implementatie verzameling op die een subset van Server-clients bevat om de implementatie te verifiëren.</li><li>Hiermee configureert u de implementatie-instellingen die geschikt zijn voor de server-clients in zijn omgeving.</li></ul>|[Software-updates implementeren](deploy-software-updates.md)|  
|De ConfigMgr-beheerder controleert of de test implementaties zijn geïmplementeerd.|[Implementatie status van software-updates](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|De ConfigMgr-beheerder werkt de twee implementaties bij met nieuwe verzamelingen die zijn productie werk stations en-servers bevatten.|Geen aanvullende informatie|  

##  <a name="step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a>Stap 5: naleving bewaken voor geïmplementeerde software-updates  
 De ConfigMgr-beheerder bewaakt de naleving van zijn software-update-implementaties. De beheerder voert de stap uit in de volgende tabel.  

|Proces|Naslaginformatie|  
|-------------|---------------|  
|De ConfigMgr-beheerder bewaakt de implementatie status van software-updates in de Configuration Manager-console en controleert de software-update-implementatie rapporten die beschikbaar zijn via de-console.|[Software-updates controleren](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a>Stap 6: maandelijkse software-updates toevoegen aan de groep voor jaarlijkse updates  
 De ConfigMgr-beheerder voegt de software-updates uit de maandelijkse software-update groep toe aan de jaarlijkse software-update groep. De beheerder voert de stap uit in de volgende tabel.  

|Proces|Naslaginformatie|  
|-------------|---------------|  
|De ConfigMgr-beheerder selecteert de software-updates uit de groep voor maandelijkse software-updates en voegt de software-updates toe aan de groep met software-updates die zijn gemaakt voor jaarlijkse naleving. De beheerder houdt de naleving van software-updates bij en maakt diverse rapporten voor zijn beheer.|[Software-updates toevoegen aan een geïmplementeerde update groep](add-software-updates-to-an-update-group.md)|  

De ConfigMgr-beheerder heeft zijn maandelijkse implementatie voor beveiligings software-updates voltooid. De beheerder blijft de compatibiliteit van software-updates bewaken en rapporteren om ervoor te zorgen dat de clients in zijn omgeving binnen acceptabele nalevings niveaus vallen.  

##  <a name="recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a>Periodiek maandelijks proces voor het implementeren van software-updates  
 Na de eerste maand dat onze ConfigMgr-beheerder software-updates implementeert, voert de beheerder de stappen drie tot en met zes uit om de maandelijkse beveiligings updates van micro soft te implementeren.  

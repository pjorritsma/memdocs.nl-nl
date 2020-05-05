---
title: Endpoint Protection-status bewaken
titleSuffix: Configuration Manager
description: Meer informatie over het bewaken van Endpoint Protection in uw Configuration Manager hiërarchie.
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 18bbbfc6486a1e5a784603e6725629d966f6c11a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722275"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Endpoint Protection status bewaken

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt Endpoint Protection in uw micro soft Configuration Manager-hiërarchie bewaken met behulp van het knoop punt **Endpoint Protection status** onder **beveiliging** in de werk ruimte **bewaking** , het knoop punt **Endpoint Protection** in de werk ruimte **activa en naleving** en met behulp van rapporten.  

##  <a name="how-to-monitor-endpoint-protection-by-using-the-endpoint-protection-status-node"></a><a name="BKMK_1"></a>Endpoint Protection bewaken met behulp van het knoop punt Endpoint Protection status  

1. Klik in de Configuration Manager-console op **bewaking**.  

2. Vouw **beveiliging** uit in de werk ruimte **bewaking** en klik vervolgens op **Endpoint Protection status**.  

3. Selecteer in de lijst **Verzameling** de verzameling waarvoor u de statusinformatie wilt bekijken.  

   > [!IMPORTANT]
   >  Verzamelingen kunnen in de volgende gevallen worden geselecteerd:  
   > 
   > - Wanneer u **deze verzameling weer geven selecteert in het dash board Endpoint Protection** op het tabblad **waarschuwingen** van het dialoog venster**Eigenschappen** van <em><verzamelings naam\></em>.  
   >   -   Wanneer u een Endpoint Protection antimalwarebeleid implementeert voor de verzameling.  
   >   -   Wanneer u Endpoint Protection client instellingen voor de verzameling inschakelt en implementeert.  

4. Lees de informatie in de secties **Veiligheidsstatus** en **Operationele status**. U kunt op elke statuskoppeling klikken om een tijdelijke verzameling te maken in het knooppunt **Apparaten** van de werkruimte **Activa en naleving** . De tijdelijke verzameling bevat de computers met de geselecteerde status.  

   > [!IMPORTANT]  
   >  Informatie die wordt weer gegeven in het knoop punt **Endpoint Protection status** is gebaseerd op de laatste gegevens die zijn gesamenvat van de Configuration Manager-Data Base en zijn mogelijk niet actueel. Als u de meest recente gegevens wilt ophalen, klikt u op het tabblad **Start** op de optie **Samenvatting uitvoeren**of klikt u op **Overzicht plannen** om het interval voor overzichten aan te passen.  

##  <a name="how-to-monitor-endpoint-protection-in-the-assets-and-compliance-workspace"></a><a name="BKMK_2"></a>Endpoint Protection bewaken in de werk ruimte activa en naleving  

1.  Klik op **Activa en naleving**op de Configuration Manager-console.  

2.  Voer in de werkruimte **Activa en naleving** een van de volgende acties uit:  

    -   Klik op **Apparaten**. Selecteer in de lijst **Apparaten** een computer en klik op het tabblad **Details van malware** .  

    -   Klik op **Apparaatverzamelingen**. Selecteer in de lijst **Apparaatverzamelingen** de verzameling met de computer die u wilt bewaken en klik vervolgens op het tabblad **Start** in de groep **Verzameling** op **Leden weergeven**.  

3.  Selecteer een computer in de lijst *naam\> van de<verzameling* en klik vervolgens op het tabblad **Details van malware** .  

##  <a name="how-to-monitor-endpoint-protection-by-using-reports"></a><a name="BKMK_3"></a>Endpoint Protection bewaken met behulp van rapporten  
 Gebruik de volgende rapporten om informatie over Endpoint Protection in uw hiërarchie te bekijken. U kunt deze rapporten ook gebruiken om problemen met Endpoint Protection op te lossen. Zie [Inleiding tot rapportage](../../core/servers/manage/introduction-to-reporting.md) -en [logboek bestanden](../../core/plan-design/hierarchy/log-files.md)voor meer informatie over het configureren van rapportage in Configuration Manager. De Endpoint Protection-rapporten bevinden zich in de map Endpoint Protection.  

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Activiteitenrapport voor anti-malware**|Geeft een overzicht van activiteiten met betrekking tot anti-malware voor een opgegeven verzameling.|  
|**Geïnfecteerde computers**|Geeft een lijst weer van computers waarop een opgegeven bedreiging is gedetecteerd.|  
|**Meest voorkomende gebruikers op bedreigingen**|Geeft een lijst weer met de gebruikers met het hoogste aantal gedetecteerde bedreigingen.|  
|**Lijst met bedreigingen voor gebruiker**|Geeft een lijst weer met bedreigingen die zijn gedetecteerd voor een opgegeven gebruikersaccount.|  

## <a name="malware-alert-levels"></a>Waarschuwingsniveaus voor malware  
 Gebruik de volgende tabel om de verschillende Endpoint Protection waarschuwings niveaus te identificeren die kunnen worden weer gegeven in rapporten of in de Configuration Manager-console.  

|Waarschuwingsniveau|Beschrijving|  
|-----------------|-----------------|  
|**Mislukt**|Endpoint Protection kan de malware niet herstellen. Raadpleeg de logboeken voor meer informatie over de fout.<br /><br /> **Opmerking:** Zie de sectie ' Endpoint Protection ' in het onderwerp [logboek bestanden](../../core/plan-design/hierarchy/log-files.md) voor een lijst met Configuration Manager-en Endpoint Protection-logboek bestanden.|  
|**Verwijderd**|De malware is Endpoint Protection verwijderd.|  
|**In quarantaine**|Endpoint Protection de malware verplaatst naar een veilige locatie en voor komt dat deze wordt uitgevoerd totdat u deze verwijdert of toestaat dat deze wordt uitgevoerd.|  
|**Opgeruimd**|De malware is verwijderd uit het geïnfecteerde bestand.|  
|**Toegestaan**|Een gebruiker met beheerdersrechten heeft toegestaan om de software met de malware uit te voeren.|  
|**Geen actie**|Endpoint Protection hebt geen actie ondernomen over de malware. Dit kan voorkomen als de computer opnieuw wordt opgestart nadat de malware is gedetecteerd en de malware niet meer wordt gedetecteerd. Het kan bijvoorbeeld gebeuren dat een toegewezen netwerkstation waarop malware wordt gedetecteerd niet opnieuw wordt aangesloten wanneer de computer opnieuw wordt opgestart.|  
|**Geblokkeerd**|Endpoint Protection de uitvoering van malware geblokkeerd. Dit kan gebeuren als een proces op de computer malware blijkt te bevatten.|

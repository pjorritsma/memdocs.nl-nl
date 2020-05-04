---
title: Beheer taken voor toepassingen
titleSuffix: Configuration Manager
description: Configuration Manager toepassingen en implementatie typen beheren.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0896204fa994643064676b55b20d63d349c4098b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710116"
---
# <a name="management-tasks-for-configuration-manager-applications"></a>Beheer taken voor Configuration Manager toepassingen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de informatie in dit artikel om u te helpen bij het beheren van Configuration Manager toepassingen en implementatie typen.  

Zie [toepassingen maken](../../apps/deploy-use/create-applications.md)voor meer informatie over het maken van toepassingen en implementatie typen.  

> [!IMPORTANT]  
>  Afhankelijk van het type toepassing of implementatie type zijn sommige beheer opties mogelijk niet beschikbaar.  

##  <a name="manage-applications"></a>Toepassingen beheren  
 Vouw in de werk ruimte **software bibliotheek** het knoop punt toepassingen voor **toepassings beheer** > **uit, kies**de toepassing die u wilt beheren en kies vervolgens een beheer taak.  

|Taak|Details|  
|----------|-------------|  
|**Toegangsaccounts beheren**|Hiermee wordt het dialoogvenster **Toegangsaccounts beheren** geopend, waarin u het toegangsniveau kunt opgeven dat is toegestaan voor de inhoud die aan de geselecteerde toepassing is gekoppeld.|  
|**Voorbereid inhoudsbestand maken**|Hiermee wordt de **Wizard Voorbereid inhoudsbestand maken** geopend, waarmee u de distributie van inhoud naar externe distributiepunten kunt beheren. Wanneer met planning en beperking geen geldige oplossing wordt geboden voor het externe distributiepunt, kunt u de inhoud voorbereiden op het distributiepunt<br /><br /> Zie [inhoud en infra structuur voor inhoud beheren](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Overzicht van wijzigingen**|Hiermee opent u het dialoog venster **overzicht van toepassings** revisies waarmee u de eigenschappen kunt bekijken van wijzigingen die zijn aangebracht aan deze toepassing, oude toepassings revisies te verwijderen en oude versies van deze toepassing te herstellen.<br /><br /> Zie [toepassingen herzien en vervangen](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Implementatietype maken**|Hiermee opent u de **wizard implementatie type maken** waarmee u een nieuw implementatie type kunt toevoegen aan de geselecteerde toepassing.<br /><br /> Zie [toepassingen maken](../../apps/deploy-use/create-applications.md).|  
|**Statistieken bijwerken**|Hiermee wordt de informatie bijgewerkt die in het knooppunt **Implementaties** van de werkruimte **Bewaking** wordt weergegeven over de implementaties van deze toepassing.<br /><br /> Zie [toepassingen bewaken vanuit de Configuration Manager-console](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Opnieuw invoeren**|Een toepassing die buiten gebruik is gesteld met de beheer taak **buiten gebruik stellen** , opnieuw wordt ingesteld.|  
|**Buiten gebruik stellen**|Wanneer u een toepassing buiten gebruik stelt, is deze niet langer beschikbaar voor implementatie, maar de toepassing en implementaties van de toepassing worden niet verwijderd. Bestaande exemplaren van deze toepassing die op clientcomputers werden geïnstalleerd, worden niet verwijderd. Eventuele wijzigingen aan de toepassing worden na 60 dagen uit Configuration Manager verwijderd. Maar geïnstalleerde kopieën van de toepassing worden niet verwijderd.<br /><br /> Als u een toepassing wilt verwijderen, moet u eerst de toepassing buiten gebruik stellen, alle implementaties verwijderen, verwijzingen naar de toepassing verwijderen door andere implementaties en vervolgens alle revisies van de toepassing verwijderen.<br /><br /> Zie [toepassingen herzien en vervangen](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Exporteren**|Hiermee wordt de **wizard toepassing exporteren** geopend, waarmee u de geselecteerde toepassingen kunt exporteren naar een zip-bestand dat u vervolgens op een andere site archiveert of installeert. Als u ervoor kiest toepassings inhoud te exporteren, wordt er een map gemaakt die de inhoud bevat.<br /><br /> U kunt ook toepassings afhankelijkheden, vervangings relaties en voor waarden en inhoud voor de toepassing en de afhankelijkheden hiervan exporteren.<br /><br /> De Windows Power shell **-cmdlet Export-CMApplication**heeft dezelfde functie. Zie [export-CMApplication](https://go.microsoft.com/fwlink/p/?LinkID=258880) in de micro soft System Center 2012 Configuration Manager SP1 cmdlet naslag documentatie voor meer informatie.|  
|**Verwijderen**|Hiermee verwijdert u de geselecteerde toepassing.<br /><br /> U kunt een toepassing niet verwijderen als andere toepassingen ervan afhankelijk zijn, als er een actieve implementatie van de toepassing is of als de toepassing afhankelijke takenreeksen heeft.|  
|**Implementatie simuleren**|Hiermee wordt de **Wizard Implementatie van toepassing simuleren** geopend, waarin u de resultaten van een toepassingsimplementatie op computers kunt testen zonder de toepassing daadwerkelijk te installeren of verwijderen.<br /><br /> Zie [toepassings implementaties simuleren](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Implementeren**|Hiermee wordt de **Wizard Software implementeren** geopend, waarin u de geselecteerde toepassing kunt implementeren naar verzamelingen computers in uw hiërarchie.<br /><br /> Zie [toepassingen implementeren](../../apps/deploy-use/deploy-applications.md).|  
|**Inhoud distribueren**|Hiermee wordt de **Wizard Inhoud distribueren** geopend, waarin u de inhoud voor de geselecteerde toepassing kunt kopiëren naar distributiepunten in uw hiërarchie.<br /><br /> Zie [inhoud en infra structuur voor inhoud beheren](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Relaties weergeven**|Toont een grafisch diagram van de relaties van de geselecteerde toepassingen met andere toepassingen. Kies een van de volgende opties:<br><br><ul><li>**Afhankelijkheid** : hier worden de toepassingen weer gegeven die afhankelijk zijn van de geselecteerde toepassing en de toepassingen waarvan de geselecteerde toepassing afhankelijk is.</li><li>**Vervanging** : geeft toepassingen weer die door de geselecteerde toepassing worden vervangen en toepassingen waarvan de geselecteerde toepassing is vervangen door.</li><li>**Globale voor waarden** – Hiermee worden de globale voor waarden weer gegeven waarnaar deze toepassing verwijst.</li></ol><br /> Zie [toepassingen herzien en vervangen](../../apps/deploy-use/revise-and-supersede-applications.md) en [globale voor waarden maken](../../apps/deploy-use/create-global-conditions.md).|  
|**Toepassingen kopiëren**|Kopieer of Dupliceer Configuration Manager toepassingen om een nieuwe te maken. Deze actie is handig als u iets wilt testen of wanneer u een vergelijk bare toepassing wilt maken. De site maakt een nieuwe toepassing, waarbij **-kopie** wordt toegevoegd aan de naam. Terwijl de site het meren deel van de meta gegevens naar de nieuwe toepassing kopieert, worden er geen implementaties gekopieerd.|

##  <a name="manage-deployment-types"></a>Implementatie typen beheren  
 Vouw in de werk ruimte **software bibliotheek** het knoop punt **toepassings beheer**uit, kies **toepassingen**en kies vervolgens de toepassing die het implementatie type bevat dat u wilt beheren. Klik in het detail venster op het tabblad **implementatie typen** , kies het implementatie type dat u wilt beheren en kies vervolgens een beheer taak.  

|Taak|Details|  
|----------|-------------|  
|**Prioriteit verhogen**|Hiermee wordt de prioriteit van het geselecteerde implementatietype verhoogd. Implementatietypen worden opeenvolgend geëvalueerd. Wanneer een implementatie type voldoet aan de opgegeven vereisten, wordt het uitgevoerd en worden er geen verdere implementatie typen in de lijst met prioriteiten worden geëvalueerd.|  
|**Prioriteit verlagen**|Hiermee wordt de prioriteit van het geselecteerde implementatietype verlaagd.|  
|**Verwijderen**|Hiermee wordt het geselecteerde implementatietype verwijderd.<br><br>U kunt een implementatietype niet verwijderen als ernaar wordt verwezen door een implementatietype in een andere toepassing.<br>Als u een implementatie type wilt verwijderen, moet u alle afhankelijkheden verwijderen voor het implementatie type dat zich in andere implementatie typen bevindt.<br>Bovendien moet u ook eerdere revisies verwijderen van alle toepassingen die een implementatie type hebben dat verwijst naar het implementatie type dat u wilt verwijderen.|  
|**Inhoud bijwerken**|Hiermee wordt de inhoud vernieuwd voor het geselecteerde implementatietype.<br /><br /> Wanneer u deze wizard start voor een implementatie type met een virtuele toepassing, wordt de **wizard inhoud bijwerken** gestart. Met deze wizard kunt u publicatie opties en regels voor vereisten wijzigen voor de geselecteerde virtuele toepassing. Zie [toepassingen maken](../../apps/deploy-use/create-applications.md)voor meer informatie.<br /><br /> Wanneer u de inhoud van een implementatietype vernieuwt, wordt er een nieuwe revisie van de toepassing gemaakt. Hierdoor worden clientapparaten mogelijk bijgewerkt met de nieuwe toepassing.|  

---
title: Synchronisatie van software-updates beheren
titleSuffix: Configuration Manager
description: Volg deze stappen om de synchronisatie van software-updates te plannen, de synchronisatie van software-updates hand matig te starten en de synchronisatie van software-updates te controleren.
ms.date: 05/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d36c6a02868b8ccde9538a286135b2ad1ce08f43
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83269045"
---
#  <a name="synchronize-software-updates"></a><a name="BKMK_SUMSync"></a>Software-updates synchroniseren

*Van toepassing op: Configuration Manager (huidige vertakking)*

 Synchronisatie van software-updates in Configuration Manager is het proces van het ophalen van de meta gegevens van de software-update die voldoen aan de criteria die u configureert. Dit omvat specifieke producten, classificaties en talen. Normaal gesp roken haalt het software-update punt op de centrale beheer site of op een zelfstandige primaire site de meta gegevens op uit Microsoft Update. Vervolgens verzendt de site op het hoogste niveau een synchronisatie aanvraag naar andere sites. Wanneer een site de synchronisatie aanvraag van de bovenliggende site ontvangt, haalt het software-update punt voor de site meta gegevens van software-updates op uit de [synchronisatie bron](../plan-design/plan-for-software-updates.md#BKMK_SyncSource)van de upstream. Zie voor meer informatie over het synchronisatie proces voor software- [updates software](../understand/software-updates-introduction.md#BKMK_Synchronization)-Update synchronisatie.

U kunt de synchronisatie van software-updates configureren zodat deze volgens een schema wordt uitgevoerd in de eigenschappen voor het software-update punt op de site op het hoogste niveau. Wanneer u de synchronisatie planning hebt geconfigureerd, wijzigt u de planning doorgaans niet als onderdeel van de normale bewerkingen. U kunt de synchronisatie van software-updates echter hand matig initiëren wanneer dit nodig is.

  > [!NOTE]  
  >  Software-update punten moeten zijn verbonden met de synchronisatie bron stroomopwaarts om software-updates te synchroniseren. Wanneer de verbinding van een software-updatepunt met de synchronisatiebron stroomopwaarts ervan is verbroken, kunt u de export- en importmethode gebruiken om software-updates te synchroniseren. Zie de sectie [Software-updates synchroniseren vanaf een niet-verbonden software-updatepunt](synchronize-software-updates-disconnected.md)voor meer informatie.  

## <a name="schedule-software-updates-synchronization"></a>Synchronisatie van software-updates plannen
Wanneer u een planning voor synchronisatie van software-updates configureert, start het software-update punt op het hoogste niveau de synchronisatie met Microsoft Update op de geplande datum en tijd. Met de aangepaste planning kunt u software-updates synchroniseren op een datum en tijdstip waarop de vereisten van de Windows Server Update Services (WSUS)-server, site server en het netwerk laag zijn. U kunt bijvoorbeeld het schema zo instellen dat software-updates elke week om 2:00 uur worden gesynchroniseerd. Tijdens de geplande synchronisatie worden alle wijzigingen die sinds de laatste synchronisatie in de metagegevens van de software-updates zijn aangebracht, ingevoegd in de sitedatabase. Dit omvat nieuwe metagegevens van software-updates of metagegevens die zijn gewijzigd, verwijderd of nu zijn verlopen.

Gebruik de volgende procedures op de site op het hoogste niveau om de synchronisatie van software-updates te plannen.  

#### <a name="to-schedule-software-updates-synchronization"></a>Synchronisatie van software-updates plannen  

  1.  Klik op **Beheer**in de Configuration Manager-console.  

  2.  Vouw in de werkruimte Beheer**Siteconfiguratie**uit en klik vervolgens op **Sites**.  

  3.  Klik in het resultatenvenster op de centrale beheersite of de zelfstandige primaire site.  

  4.  Vouw op het tabblad **Start** in de groep **Instellingen** het knooppunt **Siteonderdelen configureren** uit en klik op **Software-updatepunt**.  

  5.  Selecteer in het dialoogvenster Eigenschappen van Software-updatepuntcomponenten **Synchronisatie op een planning inschakelen** en geef vervolgens de synchronisatieplanning op.  

## <a name="manually-start-software-updates-synchronization"></a>De synchronisatie van software-updates hand matig starten
U kunt de synchronisatie van software-updates hand matig initiëren op de site op het hoogste niveau in de Configuration Manager-console vanuit het knoop punt **alle software-updates** in de werk ruimte **software bibliotheek** .  

Gebruik de volgende procedures op de site op het hoogste niveau om de synchronisatie van software-updates hand matig te initiëren.  

#### <a name="to-manually-start-software-updates-synchronization"></a>De synchronisatie van software-updates hand matig starten  

1. Klik in de Configuration Manager-console die is verbonden met de centrale beheer site of zelfstandige primaire site op **software bibliotheek**.  

2. Vouw in de werk ruimte software bibliotheek het knoop punt **software-updates** uit en klik op **alle software-updates** of software- **Update groepen**.  

3. Klik op het tabblad **Start** in de groep **alle software-updates** op **software-updates synchroniseren**. Klik op **Ja** in het dialoogvenster om te bevestigen dat u het synchronisatieproces wilt starten.  

   Nadat u het synchronisatie proces op het software-update punt initieert, kunt u het synchronisatie proces bewaken vanuit de Configuration Manager-console voor alle software-update punten in uw hiërarchie. Gebruik de volgende procedure om het synchronisatieproces van de software-updates te controleren.  


## <a name="monitor-software-updates-synchronization"></a>Synchronisatie van software-updates bewaken
Nadat u het synchronisatie proces hebt gestart, kunt u de Configuration Manager-console gebruiken om het proces voor alle software-update punten in uw hiërarchie te controleren. Gebruik de volgende procedure om het synchronisatieproces voor software-updates te controleren. Zie [software-updates bewaken](../deploy-use/monitor-software-updates.md)voor meer informatie over het bewaken van software-updates, waaronder het synchronisatie proces.

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Het synchronisatieproces voor software-updates controleren  

1. Klik in de Configuration Manager-console op **bewaking**.  

2. Klik in de werk ruimte **bewaking** op **synchronisatie status van software-update punten**.  

   De software-update punten in uw Configuration Manager-hiërarchie worden weer gegeven in het deel venster met resultaten. In deze weergave kunt u de synchronisatiestatus van alle software-updatepunten controleren. Wanneer u meer gedetailleerde informatie over het synchronisatieproces wenst, kunt u het bestand wsyncmgr.log bekijken. Dit bestand bevindt zich op de volgende locatie: <*ConfigMgrInstallationPath*>\logboeken op elke siteserver.  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Updates importeren uit de Microsoft Update catalogus

Het software-update punt op het hoogste niveau gebruikt WSUS om informatie over software-updates van micro soft te verkrijgen in Configuration Manager. Het kan voor komen dat u een update nodig hebt die niet automatisch wordt gesynchroniseerd in WSUS voor uw geselecteerde producten en classificaties, maar wel beschikbaar is in de [Microsoft Update catalogus](https://catalog.update.microsoft.com). Updates die niet automatisch worden gesynchroniseerd in WSUS, zijn doorgaans bedoeld om zeer specifieke problemen op te lossen. Doorgaans als er een update beschikbaar is in de catalogus, kunt u deze importeren in WSUS. U kunt deze vervolgens synchroniseren met Configuration Manager en implementeren zoals elke andere update.

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>Een update importeren uit de Microsoft Update catalogus

1. Open de WSUS-beheer console en verbind deze met de WSUS-server op het hoogste niveau in uw hiërarchie.
   - Als Internet Explorer niet de standaard webbrowser van de computer is, stelt u deze tijdelijk in als de standaard browser.
2. Klik op **updates** of klik op de naam van uw WSUS-server. 
3. Selecteer in het deel venster **acties** de optie **updates importeren... Hiermee** wordt een browser venster geopend voor de [Microsoft Update catalogus](https://catalog.update.microsoft.com).
   ![Selecteer updates importeren in de WSUS-console](media/wsus-console-import-updates.png)
4. Installeer het ActiveX-besturings element Microsoft Update Catalog als u hierom wordt gevraagd. Het besturings element moet worden geïnstalleerd om updates te importeren in WSUS. 
5. Zoek in het browser venster naar de gewenste update. Klik op de knop **toevoegen*** om deze aan het mandje toe te voegen.
6. Klik op **mandje weer geven**. Zorg ervoor dat de optie voor het **rechtstreeks importeren in Windows Server Update Services** is geselecteerd. Klik vervolgens op **importeren**.
    ![Update uit catalogus importeren in WSUS](./media/import-catalog-update-into-wsus.png)
7. Zodra het importeren is voltooid, klikt u op **sluiten** in het browser venster.
     - Stel de standaard browser zo nodig opnieuw in.
8. Synchroniseer uw Configuration Manager software-update punt.


## <a name="next-steps"></a>Volgende stappen
Nadat u software-updates voor de eerste keer hebt gesynchroniseerd, of nadat er nieuwe classificaties of producten beschikbaar zijn, moet u [de nieuwe classificaties en producten configureren](configure-classifications-and-products.md) om software-updates te synchroniseren met de nieuwe criteria.

Nadat u software-updates hebt gesynchroniseerd met de criteria die u nodig hebt, beheert u de [instellingen voor software-updates](manage-settings-for-software-updates.md).  

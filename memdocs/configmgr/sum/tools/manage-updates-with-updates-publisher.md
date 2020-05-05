---
title: Updates beheren
titleSuffix: Configuration Manager
description: De updates beheren die u implementeert en maakt met System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2cb1d1547c23357adbaa26e649e4e22a78e0f39
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717809"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Software-updates beheren in updates Publisher

*Van toepassing op: System Center Updates Publisher*     

In System Center Updates Publisher gebruikt u de **werk ruimte updates** om software-updates en bundels te beheren die u in de opslag plaats hebt geïmporteerd.  

Beheer taken omvatten het dupliceren, bewerken en verlopen of opnieuw activeren van updates en bundelen, en het toewijzen van updates en bundels aan publicaties. U kunt ook aangepaste catalogussen exporteren voor gebruik met andere updates voor Publisher-installaties.

Updates ophalen die u kunt beheren:
-  [Een Update catalogus toevoegen](updates-publisher-catalogs.md#add-software-update-catalogs) aan uw installatie van updates Publisher
-  [Importeer](updates-publisher-catalogs.md#import-updates) de updates uit die catalogus naar uw opslag plaats.

U kunt ook [uw eigen updates maken](create-updates-with-updates-publisher.md).



## <a name="create-a-duplicate-of-an-update"></a>Een duplicaat van een update maken
U kunt dubbele exemplaren of kopieën maken van updates in uw opslag plaats. Vervolgens kunt u de kopie wijzigen in plaats van de oorspronkelijke update te wijzigen. U kunt geen kopieën maken van update bundels.

Als u een kopie wilt maken, selecteert u een update in de **werk ruimte updates**en kiest u **dupliceren**. De kopie van de update wordt weer gegeven op dezelfde locatie in de werk ruimte updates met *kopie van* toegevoegd aan de naam.

Een nieuwe kopie die u maakt, heeft de status niet- **verlopen**, maar de instellingen van het origineel blijven behouden.

## <a name="edit-updates-and-bundles"></a>Updates en bundels bewerken
U kunt updates en bundels selecteren die zich in uw opslag plaats bevinden om deze te wijzigen.

Selecteer in de **werk ruimte updates** een update of bundel en selecteer vervolgens **bewerken** op het tabblad **Start** om de wizard bewerken te openen. Updates en bundels hebben elk afzonderlijke, maar nauw gerelateerde wizards die dezelfde opties presen teren als de wizards [Update maken](create-updates-with-updates-publisher.md#use-the-create-update-wizard) of [bundel maken](create-updates-with-updates-publisher.md#use-the-create-bundle-wizard) .

Wanneer u het bestand bewerkt, kunt u alle beschik bare Details over de update of bundel wijzigen zodat deze in uw omgeving kunnen worden gebruikt. U kunt bijvoorbeeld de regels voor toepas baarheid of prioriteit bewerken of de taal wijzigen. U kunt ook het product en de leverancier wijzigen om de update of bundel te verplaatsen naar een aangepaste map om updates voor uw eigen gebruik te groeperen.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Updates en bundels toewijzen aan een publicatie
U kunt updates en bundels selecteren in de **werk ruimte updates** en vervolgens **toewijzen** kiezen op het tabblad **Start** van het lint om ze toe te voegen aan een publicatie. Hiermee start u de wizard **software-updates toewijzen** .
-  Zie [updates en bundels publiceren](#publish-updates-and-bundles-from-the-updates-workspace) voor informatie over het selecteren en publiceren van updates en bundels als één taak.
-  Zie [publicaties beheren](updates-publisher-publications.md) voor meer informatie over het beheren van groepen updates en bundels als één object. Nadat u updates aan een publicatie hebt toegewezen, kunt u die publicatie beheren, die op zijn beurt alle toegewezen updates bevat.

Wanneer u updates aan een publicatie toewijst:

-   U kunt verlopen en niet-verlopen updates en bundels in dezelfde publicatie toevoegen.

-   Geef het publicatie type op:

    -   **Volledige inhoud** – Hiermee publiceert u de volledige inhoud van de update naar uw WSUS-server. Dit omvat meta gegevens en de binaire update bestanden.

    -   **Alleen meta gegevens** : Hiermee worden alleen de meta gegevens gepubliceerd; binaire update bestanden worden niet gepubliceerd. U kunt deze optie kiezen als u compatibiliteits gegevens wilt verzamelen.

    -   **Automatisch** : deze modus is alleen beschikbaar wanneer u de uitgever van updates hebt verbonden met Configuration Manager (Zie de optie [ConfigMgr-server](updates-publisher-options.md#configmgr-server) .)

    Met dit type worden updates voor Publisher-query's Configuration Manager om te bepalen of de updates of bundels moeten worden gepubliceerd met volledige inhoud of alleen meta gegevens. Volledige inhoud voor een update wordt alleen gepubliceerd wanneer die update voldoet aan de **aangevraagde drempel waarde voor het aantal clients** en de drempel waarde voor de grootte van de **pakket bron,** die wordt opgegeven op de pagina **ConfigMgr-server** van updates Publisher-opties.

-   Een publicatie selecteren:

    -   Gebruik **Software-update toewijzen aan bestaande publicaties** wanneer u al een publicatie hebt gemaakt die u wilt gebruiken. Deze optie is niet beschikbaar totdat ten minste één publicatie bestaat.

    -   Gebruik **Software-update toewijzen aan een nieuwe publicatie** wanneer u geen geschikte publicatie hebt. Hiermee wordt een nieuwe publicatie gemaakt met de naam die u opgeeft.

Nadat u updates aan een publicatie hebt toegewezen, kunt u de **publicatie werkruimte** gebruiken om de publicatie te [publiceren](updates-publisher-publications.md#publish-publications) of te [exporteren](updates-publisher-publications.md#export-a-publication) als groep.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Updates en bundels publiceren vanuit de werk ruimte updates
Wanneer u updates en bundels publiceert, voegt Publisher informatie over deze updates en bundels (meta gegevens) en mogelijk de binaire bestanden voor de updates (volledige inhoud) toe aan een update server voor implementatie op apparaten.

Voordat u de optie voor publiceren hebt, moet u de optie [Update server](updates-publisher-options.md#update-server) configureren voor updates Publisher. Als u deze configuratie optie wilt openen, gaat u naar **updates werk ruimte** &gt; **overzicht** en selecteert u **WSUS en ondertekening certificaat configureren.** U kunt ook naar de pagina Update server gaan in de opties voor updates Publisher.

Er zijn twee manieren om updates en bundels te publiceren:
-   Rechtstreeks vanuit de werk ruimte updates. (Zie de volgende procedure *om updates en bundels te publiceren*.)
-   Als een [publicatie](updates-publisher-publications.md#publish-publications) in de werk ruimte publicaties.  

> [!NOTE]   
> Updates Publisher kan alleen updates publiceren die 375 MB of minder groot zijn.

### <a name="to-publish-updates-and-bundles"></a>Updates en bundels publiceren
1.  Ga naar de **werk ruimte updates** en selecteer een of meer updates en bundels die u wilt publiceren. Kies vervolgens **publiceren** vanuit het tabblad **Start** van het lint.

2.  Selecteer op de pagina **selecteren** van de wizard **publiceren** hoe u de updates wilt publiceren. De opties zijn hetzelfde als voor het [toewijzen van updates](#assign-updates-and-bundles-to-a-publication): **volledige inhoud**, **alleen meta gegevens**of **automatisch**.

    U kunt er ook voor kiezen om alle updates te ondertekenen met een nieuw publicatie certificaat.

3.  Voltooi de wizard.

Als het publiceren mislukt, wordt er een koppeling naar het bestand UpdatesPublisher. log weer gegeven dat meer informatie kan bieden.

## <a name="export-updates"></a>Updates exporteren
U kunt updates en bundels exporteren uit uw update-opslag plaats voor Publisher om een aangepaste Update catalogus te maken. Vervolgens kunt u die catalogus [toevoegen](updates-publisher-catalogs.md#add-software-update-catalogs) en vervolgens [importeren](updates-publisher-catalogs.md#import-updates) naar een andere instantie van updates Publisher. (U kunt [updates ook exporteren als publicatie](updates-publisher-publications.md#export-a-publication).)

Als u rechtstreeks wilt exporteren, gaat u naar **updates werk ruimte** > **alle software-updates** en selecteert u een of meer updates en bundels. U kunt geen map van een leverancier of product exporteren, maar een map selecteren en vervolgens de updates in die map selecteren die u wilt exporteren.

Selecteer een of meer updates, kies **exporteren** op het tabblad **Start** van het lint en geef vervolgens een pad en bestands naam op voor het exporteren van de catalogus.

U kunt afhankelijke software-updates exporteren (insluiten).

## <a name="delete-updates-and-bundles"></a>Updates en bundels verwijderen
U kunt updates en bundels van updates verwijderen om ze te verwijderen uit de updates voor de Publisher-opslag plaats.

Ga naar **updates werk ruimte** > **alle software-updates** en selecteer een of meer afzonderlijke updates. Kies vervolgens **verwijderen** op het tabblad **Start** van het lint.

-   Als uw selectie alleen updates of bundels bevat die niet zijn gepubliceerd of die zijn verlopen, wordt u gevraagd om de verwijdering te bevestigen voordat ze worden verwijderd.

-   Als uw selectie een update of bundel bevat die is gepubliceerd en nog niet is verlopen, krijgt u een waarschuwing. U moet deze updates [laten verlopen](updates-publisher-publications.md#expire-or-reactivate-updates-and-bundles) en vervolgens die wijziging publiceren voordat u ze uit de opslag plaats verwijdert.  

Als u een update of bundel van een leverancier verwijdert en vervolgens die catalogus vervolgens opnieuw importeert, wordt die update teruggezet naar uw opslag plaats.

## <a name="manage-vendor-and-product-folders"></a>Leveranciers-en product mappen beheren
Als u een lijst met leveranciers en producten wilt weer geven voor elke leverancier waarvoor u updates hebt geïmporteerd of bijgewerkt, gaat u naar **updates werkruimte** > **overzicht** > **alle software-updates**.

Mappen voor leveranciers en producten worden automatisch gemaakt door Publisher updates wanneer u een wizard gebruikt voor het importeren of maken van een software-update of-bundel. U kunt deze mappen ook hand matig maken.

-   Als u een map van een leverancier wilt maken, klikt u in het navigatie deel venster van de **werk ruimte updates**met de rechter muisknop op **alle software-updates**en kiest u **leverancier maken**.

-   Als u een productmap wilt maken onder een map leverancier, klikt u met de rechter muisknop op de map leverancier en kiest u **product maken**.

U kunt niet alleen mappen maken, maar ook de naam van een leverancier of product in uw opslag plaats. Als u dit wilt doen, klikt u met de rechter muisknop op de map en kiest u de gewenste optie, wijzigt u de **naam** of het **verwijderen**. Als u een map verwijdert, worden alle updates en bundels in die map en de bijbehorende product mappen verwijderd uit de updates voor de Publisher-opslag plaats.

U kunt updates verplaatsen tussen leveranciers en product mappen, met inbegrip van de mappen die u maakt. Als u een update of bundel naar een nieuwe map wilt verplaatsen, moet u de update of bundel selecteren en vervolgens **bewerken** . Op de pagina **informatie** van de wizard Update bewerken kunt u de leverancier en het product opnieuw toewijzen. Wanneer de wizard **Update bewerken** is voltooid, wordt de wijziging toegepast en wordt de update verplaatst naar de nieuwe map.

## <a name="view-the-xml-of-an-update-or-bundle"></a>De XML van een update of bundel weer geven
U kunt één update of bundel selecteren in de **werk ruimte updates** en vervolgens XML-bestand **weer geven** kiezen om de XML-structuur van die update weer te geven. Er zijn geen opties voor het rechtstreeks bewerken van de XML-structuur.

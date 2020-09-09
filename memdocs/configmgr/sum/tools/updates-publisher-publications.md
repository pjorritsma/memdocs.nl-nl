---
title: Publicaties beheren
titleSuffix: Configuration Manager
description: Groepen van software-updates beheren als een publicatie met System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e3dedef9ffe785ce7127fc371030cfd990d70e38
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608386"
---
# <a name="manage-publications-in-updates-publisher"></a>Publicaties in updates Publisher beheren

*Van toepassing op: System Center Updates Publisher*

U kunt met behulp van publicaties groepen updates en bundels beheren als één object. Dit omvat het publiceren van de updates op een beheer server en het exporteren van de publicatie als groep voor gebruik met een andere installatie van updates Publisher.

## <a name="create-publications"></a>Publicaties maken
Er zijn twee manieren om publicaties te maken:

-   Wanneer u updates en bundels beheert in de **werk ruimte updates**, kunt u ze [toewijzen](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) aan een nieuwe publicatie die op dat moment wordt gemaakt.

-   In de **werk ruimte publicaties** kunt u de knop **maken** gebruiken op het tabblad **publicatie** van het lint. Met deze methode kunt u een publicatie maken voor toekomstig gebruik. Later, wanneer u updates toewijst, kunt u deze publicatie gebruiken.

## <a name="rename-a-publication"></a>De naam van een publicatie wijzigen
Als u de naam van een publicatie wilt wijzigen, selecteert u de publicatie in de **werk ruimte publicaties**en kiest u vervolgens op het tabblad **publicatie** van het lint de optie **bewerken**.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Het publicatie type van updates in een publicatie wijzigen
Vanuit de **werk ruimte publicatie**kunt u het **publicatie type** van updates en bundels wijzigen die zijn toegewezen aan een publicatie.

1. Selecteer de publicatie met de updates die u wilt wijzigen en selecteer vervolgens een of meer updates of bundels uit de naam van **alle &lt; publicatie> leden updates** .

2. Kies vervolgens een van de volgende opties op het tabblad **Start** . Welke opties beschikbaar zijn, is afhankelijk van het publicatie type van de updates die u hebt geselecteerd.

   -   **Automatisch**
   -   **Volledige inhoud**
   -   **Alleen meta gegevens**

Nadat u een wijziging hebt aangebracht, moet u de publicatie weergave mogelijk vernieuwen om de nieuwe waarden te zien.

Zie [updates en bundels toewijzen aan een publicatie](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication)voor meer informatie over de verschillende typen publicaties.

> [!TIP]    
> Wanneer u het publicatie type van een bundel instelt, worden alle software-updates in die bundel gepubliceerd met het publicatie type van die bundel.

## <a name="remove-updates-from-a-publication"></a>Updates verwijderen uit een publicatie
Als u updates of bundels uit een publicatie wilt verwijderen, selecteert u in de **werk ruimte publicaties** de publicatie die u wilt wijzigen en selecteert u vervolgens de updates en bundels die u wilt verwijderen. Klik vervolgens op het tabblad **Start** van het lint op **verwijderen**.

Nadat de updates zijn verwijderd uit een publicatie, blijven ze beschikbaar in de update-opslag plaats voor Publisher.

## <a name="publish-publications"></a>Publicaties publiceren
Wanneer u updates en bundels publiceert, voegt Publisher informatie over deze updates en bundels (meta gegevens) en mogelijk de binaire bestanden voor de updates (volledige inhoud) toe aan een update server voor implementatie op apparaten.

Voordat u de optie voor publiceren hebt, moet u de optie [Update server](updates-publisher-options.md#update-server) configureren voor updates Publisher. Als u deze configuratie optie wilt openen, gaat u naar **updates werk ruimte** &gt; **overzicht** en selecteert u **WSUS en ondertekening certificaat configureren.** U kunt ook naar de pagina Update server gaan in de opties voor updates Publisher.

> [!NOTE]   
> Updates Publisher kan alleen updates publiceren die 375 MB of minder groot zijn.

### <a name="to-publish-a-publication"></a>Een publicatie publiceren

1. Ga naar de **werk ruimte publicaties**en selecteer vervolgens een publicatie die de groep updates en bundels bevat die u wilt publiceren of exporteren. Kies vervolgens **publiceren** vanuit het tabblad **Start** van het lint.

2. Op de pagina **selecteren** van de wizard **publiceren** kunt u ervoor kiezen om alle updates te ondertekenen met een nieuw publicatie certificaat, maar kunt u het publicatie type niet wijzigen.

3. Voltooi de wizard.

   Als het publiceren mislukt, wordt er een koppeling naar het bestand UpdatesPublisher. log weer gegeven dat meer informatie kan bieden.

## <a name="export-a-publication"></a>Een publicatie exporteren
U kunt een publicatie exporteren vanuit uw update-opslag plaats voor Publisher. Hiermee exporteert u de updates en bundels die zijn toegewezen aan die publicatie en maakt u een Update catalogus. U kunt vervolgens die catalogus [toevoegen](updates-publisher-catalogs.md#add-software-update-catalogs) en vervolgens [importeren](updates-publisher-catalogs.md#import-updates) naar een andere instantie van updates Publisher. U kunt ook [updates exporteren](manage-updates-with-updates-publisher.md#export-updates) die geen deel uitmaken van een publicatie.

Als u een publicatie wilt exporteren, gaat u naar de **werk ruimte publicaties** en selecteert u de publicatie die de updates bevat die u wilt exporteren. U kunt slechts één publicatie per keer selecteren.

Als de publicatie is geselecteerd, kiest u **exporteren** in het tabblad **Start** van het lint en geeft u vervolgens een pad en bestands naam op voor het exporteren van de catalogus.

U kunt ook afhankelijke software-updates exporteren (opnemen) als onderdeel van de export.

## <a name="delete-a-publication"></a>Een publicatie verwijderen
Als u een publicatie wilt verwijderen, selecteert u de **werk ruimte publicaties**en kiest u vervolgens **verwijderen** op het tabblad **publicatie** van het lint.

Nadat de publicatie is verwijderd uit updates Publisher, blijven de updates in de publicatie beschikbaar in de update-opslag plaats voor Publisher.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Updates en bundels laten verlopen of opnieuw activeren
U kunt de **werk ruimte updates** gebruiken om updates en bundels te selecteren en vervolgens te laten verlopen of opnieuw te activeren. U kunt updates laten verlopen en opnieuw activeren en zo vaak als u kiest.

-   **Als u updates of bundels wilt laten verlopen**, selecteert u in de werk ruimte updates een of meer updates of bundels die niet zijn verlopen en kiest u vervolgens **verloopt** op het tabblad **Start** . U kunt de update of Configuration Manager bundel pas opnieuw activeren nadat u deze hebt gepubliceerd.

    Voordat u een aangepaste update of bundel van Configuration Manager kunt verwijderen, moet u deze laten verlopen en vervolgens de status verlopen publiceren naar Configuration Manager. Nadat updates of bundels zijn verlopen in Configuration Manager, kunt u de update of bundel niet meer implementeren of opnieuw activeren.

-   **Als u updates of bundels opnieuw wilt activeren**, selecteert u in de werk ruimte updates een of meer updates die zijn verlopen en kiest u vervolgens **opnieuw activeren** op het tabblad **Start** van het lint. Als de verlopen update eerder is gepubliceerd als verlopen voor Configuration Manager, kunt u deze niet opnieuw activeren.

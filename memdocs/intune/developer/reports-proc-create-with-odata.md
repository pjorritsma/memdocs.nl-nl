---
title: Een Intune-rapport maken van de OData-feed met Power BI
titleSuffix: Microsoft Intune
description: Maak een treemapvisualisatie met Power BI Desktop, met een interactief filter uit de Intune-datawarehouse-API.
keywords: Intune-datawarehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/29/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: A2C8A336-29D3-47DF-BB4A-62748339391D
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 081d293432e15fccfd2b30d2eb7b7c300789e74f
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270970"
---
# <a name="create-an-intune-report-from-the-odata-feed-with-power-bi"></a>Een Intune-rapport maken van de OData-feed met Power BI

In dit artikel leest u hoe u een treemapvisualisatie maakt van Intune-gegevens in Power BI Desktop die een interactief filter gebruikt. Uw CFO wil bijvoorbeeld weten hoe de algehele verdeling van apparaten is in vergelijking met de verhouding bedrijfseigen en persoonlijke apparatuur. Deze treemap biedt inzicht in het totaalaantal apparaattypen. U kunt het aantal iOS/iPadOS-, Android- en Windows-apparaten die al dan niet eigendom zijn van het bedrijf weergeven.

## <a name="overview-of-creating-the-chart"></a>Overzicht van het maken van de grafiek

Ga als volgt te werk voor het maken van deze grafiek:
1. Installeer Power BI Desktop als u dat nog niet hebt gedaan.
2. Maak verbinding met het gegevensmodel van het Intune-datawarehouse en haal de actuele gegevens voor het model op.
3. Maak of beheer de relaties in het gegevensmodel.
4. Maak de grafiek met de gegevens uit de tabel **apparaten**.
5. Maak een interactief filter.
6. Bekijk de voltooide grafiek.

### <a name="a-note-about-tables-and-entities"></a>Een opmerking over tabellen en entiteiten

In Power BI werkt u met tabellen. Een tabel bevat gegevensvelden. Elk gegevensveld heeft een gegevenstype. Het veld kan alleen gegevens van dat gegevenstype bevatten. Gegevenstypen zijn getallen, tekst, datums enzovoort. De tabellen in Power BI worden gevuld met recente historische gegevens van uw tenant wanneer u het model laadt. Hoewel de specifieke gegevens in de loop der tijd veranderen, verandert de tabelstructuur niet tenzij het onderliggende gegevensmodel wordt bijgewerkt.

Mogelijk zijn de termen *entiteit* en *tabel* enigszins verwarrend. Het gegevensmodel is toegankelijk via een OData-feed (Open Data Protocol). De containers die in Power BI tabellen worden genoemd, heten entiteiten in de context van OData. Beide termen verwijzen naar hetzelfde item dat uw gegevens bevat. Zie het [OData-overzicht](/odata/overview)voor meer informatie over OData.

## <a name="install-power-bi-desktop"></a>Power BI Desktop installeren

Installeer de nieuwste versie van Power BI Desktop. U kunt Power BI Desktop downloaden van: [PowerBI.microsoft.com](https://powerbi.microsoft.com/desktop)

## <a name="connect-to-the-odata-feed-for-the-intune-data-warehouse-for-your-tenant"></a>Verbinding maken met de OData-feed voor het Intune-datawarehouse van uw tenant

> [!Note]  
> U hebt machtigingen nodig om **Rapporten** te maken in Intune. Zie [Autorisatie](reports-api-url.md#authorization) voor meer informatie.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Rapporten** > **Intune-datawarehouse** > **Datawarehouse**.
3. Kopieer de aangepaste feed-URL. Bijvoorbeeld: `https://fef.tenant.manage.microsoft.com/ReportingService/DataWarehouseFEService?api-version=v1.0`
4. Open Power BI Desktop.
5. Selecteer in de menubalk **Bestand** > **Gegevens ophalen** > **Odata-feed**.
6. Plak de aangepaste feed-URL, die u in de eerdere stap hebt gekopieerd, in het vak voor de URL in het venster **OData-feed**.
7. Selecteer **Eenvoudig**.

    ![OData-feed voor het Intune-datawarehouse van uw tenant](./media/reports-proc-create-with-odata/reports-create-01-odatafeed.png)

8. Selecteer **OK**.
9. Selecteer **Organisatieaccount** en meld u aan met uw Intune-referenties.

    ![Referenties organisatieaccount](./media/reports-proc-create-with-odata/reports-create-02-org-account.png)

10. Selecteer **Verbinden**. De Navigator wordt geopenden er wordt een lijst met tabellen in het Intune-datawarehouse weergegeven.

    ![Schermopname van de Navigator: de lijst met datawarehousetabellen](./media/reports-proc-create-with-odata/reports-create-02-loadentities.png)

11. Selecteer de tabellen **Apparaten** en **OwnerTypes**.  Selecteer **Laden**. Power BI laadt gegevens in het model.

## <a name="create-a-relationship"></a>Relatie maken

U kunt meerdere tabellen importeren, zodat u niet alleen de gegevens in een enkele tabel kunt analyseren, maar ook gerelateerde gegevens in meerdere tabellen. Power BI heeft een functie met de naam **autodetectie** die voor u relaties zoekt en maakt. De tabellen in het datawarehouse zijn gebouwd om te werken met de autodetectiefunctie in Power BI. Maar ook als Power BI de relaties niet automatisch vindt, kunt u toch nog de relaties beheren.

![Relaties beheren van gerelateerde gegevens in verschillende tabellen](./media/reports-proc-create-with-odata/reports-create-03-managerelationships.png)

1. Selecteer **Relaties beheren**.
2. Selecteer **Autodetectie...** als Power BI de relaties nog niet heeft gedetecteerd.

De relatie wordt weergegeven met een kolom Van en een kolom Naar. In dit voorbeeld is het gegevensveld **OwnerTypeKey** in de tabel **apparaten** gekoppeld aan het gegevensveld **ownerTypeKey** in de tabel **ownerTypes**. U gebruikt de relatie om de gewone naam bij de typecode van het apparaat op te zoeken in de tabel **apparaten**.

## <a name="create-a-treemap-visualization"></a>Een treemapvisualisatie maken

In een treemapgrafiek worden hiërarchische gegevens weergegeven als vakken binnen vakken. Elke vertakking van de hiërarchie is een vak dat kleinere vakken bevat, die subvertakkingen weergeven. U kunt Power BI Desktop gebruiken om een treemap te maken van uw Intune-tenantgegevens waarin de relatieve aantallen van de fabrikanttypen van het apparaat worden weergegeven.

![Power BI-treemapvisualizaties](./media/reports-proc-create-with-odata/reports-create-03-treemap.png)

1. Zoek in het deel venster **visualisaties** naar en selecteer **Treemap**. De grafiek **Treemap** wordt toegevoegd aan het rapportcanvas.
2. Zoek in het deelvenster **Velden** de tabel `devices`.
3. Vouw de tabel `devices` uit en selecteer het gegevensveld `manufacturer`.
4. Sleep het gegevensveld `manufacturer` naar het rapportcanvas en plaats het op de grafiek **Treemap**.
5. Sleep het gegevensveld `deviceKey` vanaf de tabel `devices` naar het deelvenster **Visualisaties** en plaats het onder de sectie **Waarden** op het vak met de tekst **Gegevensvelden hier toevoegen**.  

U hebt nu een visueel element dat de verdeling van apparaten per fabrikant binnen uw organisatie weergeeft.

![Treemap met gegevens: de verdeling van apparaatfabrikanten](./media/reports-proc-create-with-odata/reports-create-06-treemapwdata.png)

## <a name="add-a-filter"></a>Een filter toevoegen

U kunt een filter aan uw treemap toevoegen om aanvullende vragen te beantwoorden met uw app.

1. Selecteer het rapportcanvas en selecteer vervolgens het **slicerpictogram** (![treemap met gegevensmodel en ondersteunde relaties](./media/reports-proc-create-with-odata/reports-create-slicer.png)) onder **Visualisaties** om een filter toe te voegen. De lege visualisatie van de **slicer** wordt weer gegeven op het canvas.
2. Zoek in het deelvenster **Velden** de tabel `ownerTypes`.
3. Vouw de tabel `ownerTypes` uit en selecteer het gegevensveld `ownerTypeName`.
4. Sleep het gegevensveld `onwerTypeName` vanaf de tabel `ownerTypes` naar het deelvenster **Filters** en plaats het onder de sectie **Filters op deze pagina** op het vak met de tekst **Gegevensvelden hier toevoegen**.  

   Onder de tabel `OwnerTypes` staat een gegevensveld genaamd `OwnerTypeKey` dat gegevens bevat die aangeven of het apparaat bedrijfseigendom of privé-eigendom is. Ga naar de tabel `ownerTypes` en sleep de **ownerTypeName** naar de slicer om de beschrijvende namen weer te geven. Dit voorbeeld toont aan hoe het gegevensmodel relaties tussen tabellen ondersteunt.

![Treemap met filter: ondersteunt relaties tussen tabellen](./media/reports-proc-create-with-odata/reports-create-08_ownertype.png)

U hebt nu een interactief filter dat u kunt gebruiken om te schakelen tussen apparaten in bedrijfseigendom en persoonlijke apparaten. Gebruik dit filter om te zien hoe de distributie verandert.

1. Selecteer **Bedrijf** in de slicer om de apparaten in bedrijfseigendom weer te geven.
2. Selecteer **Persoonlijk** in de slicer om de persoonlijke apparaten weer te geven.

## <a name="next-steps"></a>Volgende stappen

- Lees de Power BI-documentatie voor meer informatie over het [maken en beheren van relaties](https://powerbi.microsoft.com/documentation/powerbi-desktop-create-and-manage-relationships/) in Power BI Desktop.
- Raadpleeg het [Intune-datawarehousemodel](reports-ref-data-model.md).

---
title: Integreren met Power BI Report Server
titleSuffix: Configuration Manager
description: Integreer Power BI Report Server met Configuration Manager rapportage voor moderne visualisatie en betere prestaties.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc8aa57bda5f5a29d72af854be9a18e4f32760f8
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432537"
---
# <a name="integrate-with-power-bi-report-server"></a>Integreren met Power BI Report Server

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3721603-->

Vanaf versie 2002 kunt u [Power bi Report Server](/power-bi/report-server/get-started) integreren met Configuration Manager-rapportage. Deze integratie biedt u moderne visualisaties en betere prestaties. Het voegt console ondersteuning toe voor Power BI rapporten die vergelijkbaar zijn met wat er al bestaat met SQL Server Reporting Services.

Power BI Desktop rapport bestanden opslaan (. PBIX) en implementeer ze in de Power BI Report Server. Dit proces is vergelijkbaar met SQL Server Reporting Services-rapport bestanden (. RDL). U kunt de rapporten ook rechtstreeks vanuit de Configuration Manager-console starten vanuit de browser.

## <a name="prerequisites"></a>Vereisten

- Power BI Report Server-licentie. Zie [licentie Power bi Report Server](/power-bi/report-server/get-started#licensing-power-bi-report-server)voor meer informatie.

- Down load [Microsoft Power bi Report Server-September 2019](https://www.microsoft.com/download/details.aspx?id=57270)of hoger.

    > [!NOTE]
    > Installeer Power BI Report Server niet meteen. Zie [Configure the Reporting Services Point](#configure-the-reporting-services-point)(Engelstalig) voor het juiste proces op basis van uw omgeving.

- Down load [micro soft power bi Desktop (geoptimaliseerd voor Power bi Report Server-September 2019)](https://www.microsoft.com/download/details.aspx?id=57271)of hoger.

    > [!IMPORTANT]
    > - Gebruik alleen versies van Power BI Desktop van het [micro soft Download centrum](https://www.microsoft.com/download/), maar geen versie van de Microsoft Store.
    > - Gebruik alleen een versie van [Power bi Desktop die **voor Power bi Report Server is geoptimaliseerd**](/power-bi/report-server/install-powerbi-desktop).

- Power BI-integratie gebruikt hetzelfde beheer op basis van rollen voor rapportage.
    > [!NOTE]
    > Power BI Report Server biedt geen ondersteuning voor RBAC-ingeschakelde rapporten. alle kijkers van de rapporten zien dan ook dezelfde resultaten, ongeacht hun toegewezen bereik.

## <a name="configure-the-reporting-services-point"></a>Het Reporting Services-punt configureren

Dit proces is afhankelijk van het feit of u deze functie al in de site hebt.

### <a name="you-have-a-reporting-services-point"></a>U hebt een Reporting Services-punt

Gebruik dit proces alleen als u al een Reporting Services-punt op de site hebt. Alle stappen van dit proces uitvoeren op dezelfde server:

1. Maak een back-up van de **versleutelings sleutels**in de **rapport Server Configuration Manager**. Zie voor meer informatie [SSRS Encryption Keys-back up and Restore Encryption Keys](/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > Als u deze stap overs laat, verliest u de toegang tot aangepaste rapporten in SQL Server Reporting Services.

1. Verwijder de rol Reporting Services-punt van de site.

1. Verwijder SQL Server Reporting Services, maar behoud de data base.

1. Installeer Power BI Report Server.

1. De Power BI Report Server configureren

    1. De vorige Report Server-Data Base gebruiken.

    1. Gebruik **Reporting Server Configuration Manager** om de **versleutelings sleutels**te herstellen.

1. Voeg de rol Reporting Services-punt toe in Configuration Manager.

### <a name="you-dont-have-a-reporting-services-point"></a>U hebt geen Reporting Services-punt

Gebruik dit proces alleen als u nog geen Reporting Services-punt op de site hebt. Alle stappen van dit proces uitvoeren op dezelfde server:

1. Installeer Power BI Report Server.

2. Voeg de rol Reporting Services-punt toe in Configuration Manager. Zie [Configure Reporting](configuring-reporting.md)(Engelstalig) voor meer informatie.

## <a name="configure-the-configuration-manager-console"></a>De Configuration Manager-console configureren

1. Op een computer met de Configuration Manager-console werkt u de Configuration Manager-console bij naar de nieuwste versie.

1. Installeer Power BI Desktop. Controleer of de taal hetzelfde is.

1. Nadat de installatie is uitgevoerd, start u Power BI Desktop ten minste één keer voordat u de Configuration Manager-console opent.

## <a name="create-power-bi-reports"></a>Power BI-rapporten maken

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **rapportage**uit en selecteer het knoop punt nieuwe **Power bi rapporten** .

1. Selecteer in het lint **rapport maken**. Met deze actie wordt Power BI Desktop geopend.

1. Maak een rapport in Power BI Desktop.

    - Als u in Power BI Desktop verbinding maakt met een gegevens bron, selecteert u **DirectQuery** voor de verbindings instellingen.

    - Gebruik alleen ondersteunde SQL-weer gaven in deze rapporten. Zie voor meer informatie [aangepaste rapporten maken met behulp van SQL Server weer gaven in Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

1. Wanneer het rapport klaar is om op te slaan, gaat u naar het menu **bestand** , selecteert u **Opslaan als**en kiest u **Power bi Report Server**.

1. Voer in het venster **Power bi Report Server selectie** de URL in voor het Reporting Services-punt als het **nieuwe rapport server adres**. Bijvoorbeeld `https://rsp.contoso.com/Reports`. Selecteer **OK**.

1. Dubbel klik in het venster **rapport opslaan** op de `ConfigMgr_<SiteCode>` map. Bijvoorbeeld, `ConfigMgr_PS1` waar `PS1` is de ConfigMgr-site code. U kunt desgewenst kiezen of maken (van de rapport server) een submap om deze op te slaan in.
    > [!TIP]
    > Rapporten en rapport mappen met Power BI rapporten moeten zich in de `ConfigMgr_<SiteCode>` map op de rapport server bevinden of ze worden niet weer gegeven in de Configuration Manager-console.

1. Voer in **Bestands naam**een naam in voor het rapport.

In de Configuration Manager-console ziet u het nieuwe rapport in de lijst met Power BI-rapporten. Als uw rapporten niet worden weer gegeven, controleert u of u de rapporten hebt opgeslagen in de `ConfigMgr_<SiteCode>` map.

## <a name="next-steps"></a>Volgende stappen

Nadat u een rapport hebt gemaakt, gebruikt u de volgende acties in de Configuration Manager-console:

- **Uitvoeren in browser**: Hiermee opent u het Power bi rapport in de webbrowser. Deel deze URL met anderen, bijvoorbeeld: `https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > U kunt deze rapporten alleen bekijken in de webbrowser.

- **Bewerken**: wijzigingen aanbrengen in het rapport in Power bi Desktop. Voor een bestaand rapport gebruikt u de optie **Opslaan** om wijzigingen terug te slaan op de rapport server.

Zie [logboek bestand verwijzing-rapportage](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog)voor meer informatie over de logboek bestanden die moeten worden gebruikt voor rapportage.

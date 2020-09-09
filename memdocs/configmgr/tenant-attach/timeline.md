---
title: Tenant koppeling-apparaat-tijd lijn (preview-versie)
titleSuffix: Configuration Manager
description: Bekijk de tijd lijn voor Configuration Manager apparaten in het beheer centrum.
ms.date: 09/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: b2d914d8-6714-4fa1-9e14-0046b77e6b40
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 5065e893a8670911c055910889e8fbae472bfc4c
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564343"
---
# <a name="tenant-attach-device-timeline-in-the-admin-center-preview"></a><a name="bkmk_timeline"></a> Tenant bijvoegen: tijd lijn van apparaat in het beheer centrum (preview-versie)
<!--CM7141381, IN7552762 pubpreview Sept 8, 2020-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Micro soft Endpoint Manager is een geïntegreerde oplossing voor het beheer van al uw apparaten. Micro soft brengt Configuration Manager en intune samen in één console met de naam **micro soft Endpoint Manager-beheer centrum**. Wanneer Configuration Manager een apparaat synchroniseert met micro soft Endpoint Manager via een Tenant, ziet u een tijd lijn met gebeurtenissen. Deze tijdlijn toont eerdere activiteiten op het apparaat die u kunnen helpen bij het oplossen van problemen.

> [!Important]
> - Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

## <a name="prerequisites"></a>Vereisten

De volgende items zijn nodig voor het gebruik van de tijd lijn uit het beheer centrum:

- Alle vereisten voor [Tenant koppeling: client Details ConfigMgr](client-details.md#prerequisites).
- Mini maal Configuration Manager versie 2002 van de [Update Rollup](https://support.microsoft.com/help/4560496/) en de bijbehorende versie van de console geïnstalleerd.
- Endpoint Analytics-gegevens verzameling inschakelen in Configuration Manager:
   1. Ga in de Configuration Manager-console naar de client instellingen voor de **beheerders**  >  **Client Settings**  >  **instelling**.
   1. Klik met de rechter muisknop en selecteer **Eigenschappen** en selecteer vervolgens de instellingen van de **computer agent** .
   1. Stel **endpoint Analytics-gegevens verzameling inschakelen** in op **Ja**.
      - Alleen gebeurtenissen die worden verzameld nadat de client dit beleid ontvangt, worden weer gegeven in het beheer centrum. Gebeurtenissen voordat het beleid wordt ontvangen, zijn niet toegankelijk.

## <a name="permissions"></a>Machtigingen

Het gebruikers account heeft de volgende machtigingen nodig:

- De **Lees** machtiging voor de **verzameling** van het apparaat in Configuration Manager.
- De machtiging **resource lezen** onder **verzameling** in Configuration Manager.
- De machtiging voor het **melden van resources** onder **verzameling** in Configuration Manager. <!--7984188-->
- De gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD.
  - Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt.

## <a name="generate-events"></a>Gebeurtenissen genereren

Apparaten verzenden gebeurtenissen eenmaal per dag naar het beheer centrum. Alleen gebeurtenissen die worden verzameld nadat de client het beleid voor het **verzamelen van endpoint Analytics inschakelen** , worden weer gegeven in het beheer centrum. U kunt test gebeurtenissen eenvoudig genereren door een toepassing of een update van Configuration Manager te installeren of het apparaat opnieuw op te starten. Gebeurtenissen worden 30 dagen bewaard. Gebruik de [grafiek](#collected-events) om gebeurtenissen weer te geven die zijn verzameld.

## <a name="collected-events"></a>Verzamelde gebeurtenissen

|Gebeurtenis naam|Provider naam|Gebeurtenis-id|
|---|---|---|
|Toepassings fout|Toepassings fout|1000|
|Toepassing vastlopen|Toepassing vastlopen|1002|
|Kernel-crash|Micro soft-Windows-WER-SystemErrorReporting|1001|
|Toepassing vastlopen|Windows Foutrapportage|1001|
|Windows Update Agent-installatie van update|Micro soft-Windows-client|19|
|Onbekend afsluiten|Opstarten|0|
|Afsluiten gestart|Opstarten|1074|
|Abnormaal afsluiten|Opstarten|41|
|Grens groep wijzigen|Micro soft-ConfigMgr|20.000|
|Toepassingsimplementatie|Micro soft-ConfigMgr|20001|
|Configuration Manager-installatie van update|Micro soft-ConfigMgr|20002|
|Wijziging firmware versie|Micro soft-ConfigMgr|20003|

## <a name="view-the-timeline"></a>De tijd lijn weer geven

1. Ga in een browser naar [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Selecteer **apparaten** en vervolgens **alle apparaten**.
1. Selecteer een apparaat dat is gesynchroniseerd vanuit Configuration Manager via [Tenant attach](device-sync-actions.md).
1. Selecteer **tijd lijn**. Standaard worden gebeurtenissen van de afgelopen 24 uur weer gegeven.
   - Gebruik de **filter** knop om het **tijds bereik**, de **gebeurtenis niveaus**en de **naam**van de provider te wijzigen.
   - Als u een gebeurtenis selecteert, wordt er een gedetailleerd bericht weer gegeven.
   - Selecteer **synchroniseren** om de recente gegevens op te halen die zijn gegenereerd op de client. Het apparaat verzendt standaard gebeurtenissen een keer per dag naar het beheer centrum. <!--7984188-->
   - Selecteer **vernieuwen** om de pagina opnieuw te laden en nieuwe verzamelde gebeurtenissen weer te geven.

   :::image type="content" source="./media/7141381-timeline.png" alt-text="Tijd lijn van gebeurtenissen voor een apparaat" lightbox="./media/7141381-timeline.png":::

## <a name="next-steps"></a>Volgende stappen

[Problemen met de tijd lijn van het apparaat oplossen](troubleshoot-timeline.md)
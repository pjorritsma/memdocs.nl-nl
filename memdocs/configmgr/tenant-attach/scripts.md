---
title: Invoeg scripts voor het koppelen van tenants (preview) van het beheer centrum
titleSuffix: Configuration Manager
description: Voer scripts uit voor Configuration Manager apparaten vanuit het beheer centrum.
ms.date: 09/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 6b6c0a9b-01c6-4e3f-9ae4-45c780b46f8b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: db3656f98949bfbff2bf31b19b50b0ccb9959845
ms.sourcegitcommit: af4fc4f928203c1bfdb27499a56c91fe0ebae854
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/18/2020
ms.locfileid: "90803281"
---
# <a name="tenant-attach-run-scripts-preview-from-the-admin-center"></a><a name="bkmk_scripts"></a> Tenant bijvoegen: Run scripts (preview) van het beheer centrum
<!--CM6234688, IN7220536-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]
> - Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

Maak gebruik Configuration Manager van de functie voor on-premises uitvoering van scripts in het micro soft Endpoint Manager-beheer centrum. Sta extra personen, zoals Help Desk, toe om Power shell-scripts uit de Cloud uit te voeren op basis van een individueel Configuration Manager beheerd apparaat in realtime. Hiermee krijgt u alle bekende voordelen van PowerShell-scripts die al zijn gedefinieerd en goedgekeurd door de Configuration Manager-beheerder voor deze nieuwe omgeving.

:::image type="content" source="./media/6234688-scripts.png" alt-text="Scherm opname van de script lijst in het beheer centrum" lightbox="./media/6234688-scripts.png":::


## <a name="prerequisites"></a>Vereisten

Voor het uitvoeren van scripts uit het beheer centrum zijn de volgende items vereist:

- Alle vereisten voor [Tenant koppeling: client Details ConfigMgr](client-details.md#prerequisites)
- Ten minste Configuration Manager versie 2006 met [KB4580678-Tenant attached Rollup voor Configuration Manager current branch, versie 2006](https://support.microsoft.com/help/4580678) geïnstalleerd.
   - Alle sites in de hiërarchie moeten voldoen aan de minimum vereiste voor de Configuration Manager-versie.
- Configuration Manager-clients moeten de nieuwste versie-client uitvoeren.
- Voor het uitvoeren van Power shell-scripts moet Power shell-versie 3,0 of hoger worden uitgevoerd op de client.
   - Als een script dat u uitvoert, functionaliteit van een nieuwere versie van Power shell bevat, moet de client waarop u het script uitvoert, die nieuwere versie van Power shell uitvoeren.
- Ten minste één script dat al is gemaakt en goedgekeurd in Configuration Manager.
   - Scripts met para meters worden op dit moment niet ondersteund en worden niet weer gegeven in het micro soft Endpoint Manager-beheer centrum.
   - Alleen scripts die al zijn gemaakt en goedgekeurd, worden weer gegeven in het beheer centrum. Zie [een script goed keuren of weigeren](../apps/deploy-use/create-deploy-scripts.md#run-script-authors-and-approvers)voor meer informatie over het goed keuren van scripts.

## <a name="permissions"></a>Machtigingen

Het gebruikers account heeft de volgende machtigingen nodig:

- De **Lees** machtiging voor de **verzameling** van het apparaat in Configuration Manager.
- De machtiging **resource lezen** voor de **verzameling** van het apparaat in Configuration Manager.
- De gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD.
  - Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt.
- Als u scripts wilt gebruiken, moet u lid zijn van de juiste Configuration Manager beveiligingsrol. Zie [beveiligingsbereiken voor scripts uitvoeren](../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles)voor meer informatie.
- Voor het uitvoeren van scripts moet het account machtigingen voor het uitvoeren van een **script** hebben voor **verzamelingen**.

## <a name="run-a-script"></a>Een script uitvoeren

1. Ga in een browser naar [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Selecteer **apparaten** en vervolgens **alle apparaten**.
1. Selecteer een apparaat dat is gesynchroniseerd vanuit Configuration Manager via [Tenant attach](device-sync-actions.md).
1. Selecteer **scripts**.
   
   Scripts die onlangs zijn uitgevoerd en die rechtstreeks op het apparaat zijn gericht, worden al vermeld. De lijst bevat scripts die worden uitgevoerd vanuit het beheer centrum, de SDK of de Configuration Manager-console. Scripts die worden gestart vanaf de on-premises console, worden niet weer gegeven op verzamelingen met het apparaat, tenzij de scripts specifiek voor het ene apparaat werden gestart.

   :::image type="content" source="./media/6234688-run-script.png" alt-text="Het script uitvoeren vanuit het beheer centrum" lightbox="./media/6234688-run-script.png":::

1. Kies **script uitvoeren**.
   
   De scripts die beschikbaar zijn voor de beheerder op basis van de bereiken die zijn toegewezen in Configuration Manager, worden weer gegeven.
1. Selecteer **uitvoeren** om het script uit te voeren.

1. U ontvangt een melding dat het script is gestart. U hoeft niet te wachten totdat het script is voltooid voordat u een ander naar het apparaat verzendt.
1. Selecteer **vernieuwen** op de hoofd pagina om de lijst met de nieuwste script status en de laatste uitvoerings tijd bij te werken.

1. Wanneer het script is voltooid, kunt u het script selecteren om de resultaten in het deel venster **uitvoer** weer te geven. U kunt de tekst van de script uitvoer kopiëren. Selecteer **script opnieuw uitvoeren** als u het script opnieuw wilt uitvoeren.

   :::image type="content" source="./media/6234688-script-output.png" alt-text="Script uitvoer in het beheer centrum" lightbox="./media/6234688-script-output.png":::

## <a name="next-steps"></a>Volgende stappen

[Een toepassing installeren vanuit het beheer centrum](applications.md)

[Meer informatie over Power shell-script beveiliging](../apps/deploy-use/learn-script-security.md)
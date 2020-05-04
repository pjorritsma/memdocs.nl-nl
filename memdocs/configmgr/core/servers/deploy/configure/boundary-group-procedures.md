---
title: Procedures voor grensgroepen
titleSuffix: Configuration Manager
description: Configureer grens groepen om gerelateerde netwerk locaties logisch in te delen met de naam grenzen.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8a47522cf59cc211f29c572010f9d3250659e1e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715793"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Grens groepen voor Configuration Manager configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat procedures voor het configureren van grens groepen. Voordat u begint, moet u ervoor zorgen dat u bekend bent met de concepten van grens groepen. Zie [grens groepen](boundary-groups.md)voor meer informatie.



## <a name="create-a-boundary-group"></a><a name="bkmk_create"></a>Een grens groep maken  

1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **hiërarchie configuratie**uit en selecteer het knoop punt **grens groepen** .  

2.  Klik op het tabblad **Start** in de groep **maken** op **grens groep maken**.  

3.  Geef in het dialoog venster **grens groep maken** op het tabblad **Algemeen** een **naam** op voor deze grens groep. Geef eventueel een **Beschrijving**op.  

4.  Selecteer **OK** om de nieuwe grens groep op te slaan of ga door naar de volgende sectie om de grens groep te configureren.  


## <a name="configure-a-boundary-group"></a><a name="bkmk_config"></a>Een grens groep configureren  

1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **hiërarchie configuratie**uit en selecteer het knoop punt **grens groepen** .  

2.  Selecteer de grens groep die u wilt wijzigen en selecteer **Eigenschappen** in het lint. Met deze actie wordt de grens groep venster Eigenschappen geopend.  

Configureer de volgende instellingen:  
- [Grenzen toevoegen of verwijderen](#bkmk_add)  
- [Site toewijzing configureren en site systeem servers selecteren](#bkmk_references)  
- [Terugval gedrag configureren](#bkmk_bg-fallback)  
- [Opties voor grens groepen configureren](#bkmk_options)  


### <a name="add-or-remove-boundaries"></a><a name="bkmk_add"></a>Grenzen toevoegen of verwijderen

Gebruik in het venster Eigenschappen grens groep het tabblad **Algemeen** om de grenzen te wijzigen die lid zijn van deze grens groep:  

- Selecteer **toevoegen**om grenzen toe te voegen. Schakel in het venster grenzen toevoegen het selectie vakje in voor een of meer grenzen en selecteer **OK**.  

- Als u grenzen wilt verwijderen, selecteert u de grens in de lijst en selecteert u **verwijderen**.  


### <a name="configure-site-assignment-and-select-site-system-servers"></a><a name="bkmk_references"></a>Site toewijzing configureren en site systeem servers selecteren

Als u de site toewijzing en de bijbehorende configuratie van de site systeem server wilt wijzigen, gaat u naar het tabblad **verwijzingen** in de grens groep venster Eigenschappen.  

- Als u deze grens groep wilt inschakelen voor gebruik door clients voor site toewijzing, selecteert u **deze grens groep gebruiken voor site toewijzing**. Selecteer vervolgens een site in de vervolg keuzelijst **toegewezen site** . Zie [site toewijzing](boundary-groups.md#site-assignment)voor meer informatie.  

- Selecteer **toevoegen**om beschik bare site systeem servers te koppelen aan deze grens groep. Het venster site systemen toevoegen bevat alleen servers met ondersteunde site systeem rollen. Schakel het selectie vakje voor een of meer servers in en selecteer **OK**. Deze worden als gekoppelde site systeem servers toegevoegd aan deze grens groep.  

    > [!NOTE]  
    >  U kunt een combinatie van beschikbare sitesystemen van alle sites in de hiërarchie selecteren. Geselecteerde site systemen worden weer gegeven op het tabblad **site systemen** in de eigenschappen van elke grens die lid is van deze grens groep.  

- Als u een server uit deze grens groep wilt verwijderen, selecteert u de server en selecteert u vervolgens **verwijderen**.  

    > [!NOTE]  
    >  Als u deze grens groep niet meer wilt gebruiken voor het koppelen van site systemen, verwijdert u alle servers die worden vermeld als gekoppelde site systeem servers.  


### <a name="configure-fallback-behavior"></a><a name="bkmk_bg-fallback"></a>Terugval gedrag configureren

Als u terugval gedrag wilt configureren, gaat u naar het tabblad **relaties** in de grens groep venster Eigenschappen.  

- Een relatie maken met een andere grens groep:  

  - Selecteer **Toevoegen**. Selecteer in het venster terugval grens groepen de grens groep die u wilt configureren.  

  - Stel een terugval tijd in voor de volgende site systeem rollen:  
    - Distributiepunt  
    - Software-updatepunt  
    - Beheerpunt  

      > [!Note]  
      > U kunt bijvoorbeeld de venster Eigenschappen voor de grens groep filiaal openen. In het venster terugval grens groepen selecteert u de grens groep hoofd kantoor. U stelt de terugval tijd van het distributie `20`punt in op. Wanneer u deze configuratie opslaat, beginnen clients in de grens groep van het filiaal naar inhoud vanaf de distributie punten in de grens groep van het hoofd kantoor na 20 minuten.  

  - Als u terugval wilt voor komen op een specifieke grens groep, selecteert u de grens groep en selecteert u vervolgens **nooit terugval** voor het type van de site systeemrol. Deze actie kan de *standaard site grens groep*bevatten.  

- Als u de configuratie van een bestaande relatie wilt wijzigen, selecteert u de grens groep in de lijst en selecteert u **wijzigen**. Met deze actie wordt het venster terugval grens groepen geopend voor alleen deze grens groep.  
 
- Als u een relatie wilt verwijderen, selecteert u de grens groep in de lijst en selecteert u **verwijderen**.  

Zie [terugval](boundary-groups.md#fallback)voor meer informatie. 


### <a name="configure-boundary-group-options"></a><a name="bkmk_options"></a>Opties voor grens groepen configureren
<!--1356193-->
Vanaf versie 1806, om aanvullende opties voor clients in deze grens groep te configureren, gaat u naar het tabblad **Opties** . Zie voor meer informatie [Opties voor grens groepen voor het downloaden van peers](boundary-groups.md#bkmk_bgoptions).

- **Peer-down loads in deze grens groep toestaan**: deze optie is standaard ingeschakeld. Het beheer punt biedt clients een lijst met inhouds locaties die peer bronnen bevatten.  

    - **Tijdens het downloaden van de peer gebruikt u alleen peers binnen hetzelfde subnet**: deze instelling is afhankelijk van de hierboven beschreven. Als u deze optie inschakelt, wordt het beheer punt alleen opgenomen in de inhouds locatie lijst peer bronnen die zich in hetzelfde subnet bevinden als de client.  


## <a name="configure-a-fallback-site-for-automatic-site-assignment"></a><a name="bkmk_site-fallback"></a>Een terugval site configureren voor automatische site toewijzing  

Als clients zich niet in een grens groep bevinden met een toegewezen site, wijst u deze toe aan deze site wanneer ze zijn geïnstalleerd.

1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2.  Selecteer **hiërarchie-instellingen**op het tabblad **Start** van het lint in de groep **sites** .  

3.  Schakel op het tabblad **Algemeen** het selectie vakje in om **een terugval site te gebruiken**. Selecteer vervolgens een site in de vervolg keuzelijst **terugval site** .  

4.  Selecteer **OK** om de configuratie op te slaan.  

Zie [site toewijzing](boundary-groups.md#site-assignment)voor meer informatie.


## <a name="enable-use-of-preferred-management-points"></a><a name="bkmk_proc-prefer"></a>Gebruik van voorkeurs beheer punten inschakelen  

Zie [Voorkeurs beheer punten](boundary-groups.md#bkmk_preferred)voor meer informatie.

1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Selecteer **hiërarchie-instellingen**op het tabblad **Start** van het lint in de groep **sites** .  

3. Selecteer op het tabblad **Algemeen** de optie **clients gebruiken liever beheer punten die zijn opgegeven in grens groepen**.  

4. Selecteer **OK** om de configuratie op te slaan.  


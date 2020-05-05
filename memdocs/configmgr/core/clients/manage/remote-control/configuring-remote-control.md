---
title: Beheer op afstand configureren
titleSuffix: Configuration Manager
description: Beheer op afstand instellen in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78f74a9659a011defd50e6ab0e9e1cfe85eec16b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076727"
---
# <a name="configuring-remote-control-in-configuration-manager"></a>Beheer op afstand configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

 In deze procedure wordt beschreven hoe u de standaard client instellingen voor beheer op afstand configureert. Deze instellingen zijn van toepassing op alle computers in uw hiërarchie. Als u wilt dat deze instellingen alleen van toepassing zijn op sommige computers, wijst u een aangepaste apparaatclient toe aan een verzameling die de computers bevat. Zie [client instellingen configureren](../../../../core/clients/deploy/configure-client-settings.md)voor meer informatie. 

Als u hulp op afstand of Extern bureaublad wilt gebruiken, moet u deze installeren en configureren op de computer waarop de Configuration Manager-console wordt uitgevoerd. Zie de Windows-documentatie voor meer informatie over het installeren en configureren van Hulp op afstand en Extern bureaublad.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Beheer op afstand inschakelen en clientinstellingen configureren  

1.  > Kies > in de Configuration Manager-console de**client instellingen voor** **de client instellingen****standaard**.  

2. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

3. Kies in het dialoog venster **standaard** de optie **externe hulpprogram ma's**.  

4. Configureer de instellingen voor extern beheer, hulp op afstand en Extern bureaublad client. Zie [externe Hulpprogram ma's](../../../../core/clients/deploy/about-client-settings.md#remote-tools)voor een lijst met client instellingen voor externe hulpprogram ma's die u kunt configureren.  

   U kunt de bedrijfsnaam die wordt weergegeven in het dialoogvenster **Beheer op afstand van ConfigMgr** wijzigen door een waarde te configureren voor **Organisatienaam weergegeven in Software Center** in de clientinstellingen voor **Computeragent** .  

   De volgende keer dat clientcomputers clientbeleid downloaden, worden deze geconfigureerd met deze instellingen. Zie [clients beheren](../../../../core/clients/manage/manage-clients.md)om het ophalen van het beleid voor één client te initiëren.  

#### <a name="enable-keyboard-translation"></a>Toetsenbord vertaling inschakelen

Configuration Manager verzendt standaard de sleutel positie van de locatie van de viewer naar de locatie van de delende persoon. Dit kan een probleem vormen voor de toetsenbord configuraties die verschillen van de viewer naar de delende map. Een viewer met een Engels toetsen bord zou bijvoorbeeld een ' A ' bevatten, maar het Franse toetsen bord van de delende persoon zou een ' Q ' zijn. U hebt nu de mogelijkheid om beheer op afstand te configureren, zodat het teken zelf van het toetsen bord van de viewer wordt verzonden naar de delende persoon en de manier waarop de viewer ingaat, arriveert bij de delende map.

Als u toetsenbord conversie wilt inschakelen, kiest u in **Configuration Manager beheer op afstand**de optie **actie**en kiest u **toetsenbord vertaling inschakelen** om de sleutel positie te verzenden.

> [!NOTE]
>
> Speciale sleutels, zoals ~! # @ $%, worden niet correct vertaald.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Sneltoetsen voor de viewer voor beheer op afstand

|Sneltoets|Beschrijving|  
|-----------------------|-----------------|  
|Alt + Page Up|Hiermee schakelt u van links naar rechts tussen actieve programma’s.|  
|Alt + Page Down|Hiermee schakelt u van rechts naar links tussen actieve programma’s.|  
|Alt + Insert|Hiermee schakelt u tussen actieve programma's in de volgorde waarin ze zijn geopend.|  
|Alt + Home|Hiermee opent u het menu **Start** .|  
|Ctrl + Alt + End|Hiermee opent u het dialoogvenster Windows-beveiliging (Ctrl+Alt+Del).|  
|Alt + Delete|Hiermee opent u het Windows-menu.|  
|Ctrl + Alt + minteken (op het numerieke toetsenblok)|Hiermee kopieert u het actieve venster van de lokale computer naar het Klembord van de externe computer.|  
|Ctrl + Alt + plusteken (op het numerieke toetsenblok)|Hiermee kopieert u het hele venstergebied van de lokale computer naar het Klembord van de externe computer.|  

---
title: Clientinstellingen configureren
titleSuffix: Configuration Manager
description: Selecteer client instellingen in Configuration Manager.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c64895c7945b972821a1dee1702047e61b740026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713588"
---
# <a name="how-to-configure-client-settings-in-configuration-manager"></a>Client instellingen configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U beheert alle client instellingen in Configuration Manager van de**client instellingen**voor **beheer** > . Wijzig de standaardinstellingen wanneer u de instellingen wilt configureren voor alle gebruikers en apparaten in de hiërarchie waarop geen aangepaste instellingen worden toegepast. Als u verschillende instellingen wilt Toep assen op slechts enkele gebruikers of apparaten, maakt u aangepaste instellingen en implementeert u deze in verzamelingen.  

Zie [over client instellingen](../../../core/clients/deploy/about-client-settings.md)voor meer informatie over elke client instelling.

> [!NOTE]  
>  U kunt ook configuratie-items gebruiken om clients te beheren voor het beoordelen, bijhouden en herstellen van de configuratienaleving van apparaten. Zie apparaatcompatibiliteit [met Configuration Manager](../../../compliance/understand/ensure-device-compliance.md)voor meer informatie.  

##  <a name="configure-the-default-client-settings"></a>De standaard client instellingen configureren    

1.  > Kies > in de Configuration Manager-console de**client instellingen voor** **de client instellingen****standaard**.  

2. Kies op het tabblad **Start** de optie **Eigenschappen**.  

3. Geef de clientinstellingen voor iedere instellingengroep in het navigatiedeelvenster weer en configureer deze.  

   Clientcomputers zullen worden geconfigureerd met deze instellingen wanneer ze de volgende keer het clientbeleid downloaden. Zie het [ophalen van beleid initiëren voor een Configuration Manager-client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [How to manage clients](../../../core/clients/manage/manage-clients.md)om het ophalen van het beleid voor één client te initiëren.  

##  <a name="create-and-deploy-custom-client-settings"></a>Aangepaste client instellingen maken en implementeren  
Wanneer u deze aangepaste instellingen implementeert, overschrijven ze de standaardclientinstellingen. Controleer voordat u met deze procedure begint of u een verzameling hebt die gebruikers of apparaten bevat waarvoor deze aangepaste clientinstellingen nodig zijn.  

1. Kies in de Configuration Manager-console de optie **beheer** > **client instellingen**.  

2. Klik op het tabblad **Start** in de groep **maken** op **aangepaste client instellingen maken**en kies een van de volgende opties:  

   -   **Aangepaste clientapparaatinstellingen maken**  

   -   **Aangepaste clientgebruikersinstellingen maken**  

3. Geef een unieke naam en een beschrijving op voor de optie.  

4. Schakel een of meer selectie vakjes in die een groep instellingen weer geven.  

5. Kies elke groep instellingen in het navigatie deel venster en configureer de beschik bare instellingen en klik vervolgens op **OK**.   

6. Selecteer de aangepaste client instelling die u hebt gemaakt. Klik op het tabblad **Start** in de groep **client instellingen** op **implementeren**.  

7. Selecteer in het dialoog venster **verzameling selecteren** de juiste verzameling en klik vervolgens op **OK**. U kunt de geselecteerde verzameling controleren door te klikken op het tabblad **Implementaties** in het detailvenster.  

8. Bekijk de volg orde van de aangepaste client instelling die u hebt gemaakt. Wanneer u meerdere aangepaste clientinstellingen hebt, worden deze toegepast volgens hun volgordenummer. Als er conflicten zijn, heft de instelling met het laagste volgordenummer de andere stellingen op. Als u het Volg nummer wilt wijzigen, klikt u op het tabblad **Start** in de groep **client instellingen** op **item verplaatsen** of **item omlaag verplaatsen**.  

   Clientcomputers zullen worden geconfigureerd met deze instellingen wanneer ze de volgende keer het clientbeleid downloaden. Zie het [ophalen van beleid initiëren voor een Configuration Manager-client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [How to manage clients](../../../core/clients/manage/manage-clients.md)om het ophalen van het beleid voor één client te initiëren.  



##  <a name="view-client-settings"></a>Client instellingen weer geven  
 Wanneer u meerdere client instellingen op hetzelfde apparaat, dezelfde gebruiker of dezelfde gebruikers groep implementeert, zijn de prioriteiten en combi natie van instellingen complex. De client instellingen weer geven:  

1.  Kies in de Configuration Manager-console **activa en nalevings** > **apparaten** > **gebruikers** of **gebruikers verzamelingen**.  

3.  Selecteer een apparaat, gebruiker of gebruikersgroep en selecteer **Resulterende clientinstellingen** in de groep **Clientinstellingen**.  

4.  Selecteer een client instelling in het linkerdeel venster. de instellingen worden weer gegeven. In deze weer gave zijn de instellingen alleen-lezen. 

    > [!NOTE]  
    >  Als u de client instellingen wilt weer geven, moet u lees toegang hebben voor client instellingen.  

    

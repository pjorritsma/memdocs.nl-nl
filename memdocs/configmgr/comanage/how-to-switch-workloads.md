---
title: Werk belastingen voor co-beheer wisselen
titleSuffix: Configuration Manager
description: Meer informatie over het overschakelen van werk belastingen die momenteel worden beheerd door Configuration Manager naar Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/06/2019
ms.topic: how-to
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 88c8b34437ba52e700ef97885aafed40734a0f32
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776953"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Configuration Manager-workloads overschakelen naar Intune

Een van de voor delen van co-beheer is het wisselen van werk belastingen van Configuration Manager naar Microsoft Intune. Wanneer een Windows 10-apparaat de Configuration Manager-client heeft en is inge schreven bij intune, krijgt u de voor delen van beide services. U bepaalt welke workloads, indien van toepassing, u de instantie overschakelt van Configuration Manager naar intune. Configuration Manager blijft alle andere workloads beheren, met inbegrip van de werk belastingen die u niet overschakelt naar intune en alle andere functies van Configuration Manager die niet door co-beheer worden ondersteund.

Als u een werk belasting overschakelt naar intune, maar later van gedachten verandert, kunt u overschakelen naar Configuration Manager.

Zie [workloads](workloads.md)voor meer informatie over de ondersteunde werk belastingen.

## <a name="switch-workloads-starting-in-version-1906"></a>Werk belastingen scha kelen vanaf versie 1906
<!--3555750 FKA 1357954 -->
Vanaf versie 1906 kunt u verschillende pilot verzamelingen configureren voor elk van de werk belastingen voor co-beheer. Als u verschillende pilot verzamelingen kunt gebruiken, kunt u een nauw keurigere benadering hebben bij het verschuiven van werk belastingen. U kunt overstappen op werk belastingen wanneer u co-beheer inschakelt of later wanneer u klaar bent. Als u co-beheer nog niet hebt ingeschakeld, moet u dat eerst doen. Zie [co-beheer inschakelen](how-to-enable.md)voor meer informatie. Nadat u co-beheer hebt ingeschakeld, wijzigt u de instellingen in de eigenschappen voor co-beheer.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt voor **co-beheer** .  
2. Selecteer het object voor co-beheer en kies **Eigenschappen** in het lint.  
3. Schakel over naar het tabblad **werk belastingen** . Standaard worden alle werk belastingen ingesteld op de instelling **Configuration Manager** . Als u wilt overschakelen op een werk belasting, verplaatst u het besturings element schuif regelaar voor de werk belasting naar de gewenste instelling.  

    ![Scherm afbeelding van het tabblad werk belastingen op de pagina met eigenschappen voor co-beheer](media/3555750-co-management-workloads-tab.png)

    - **Configuration Manager**: Configuration Manager blijft deze werk belasting beheren.  

    - **Pilot intune**: Schakel deze werk belasting alleen uit voor de apparaten in de test verzameling. U kunt de **pilot verzamelingen** wijzigen op het tabblad **fase ring** van de pagina met eigenschappen voor co-beheer.  

    - **Intune**: Schakel deze werk belasting uit voor alle Windows 10-apparaten die zijn Inge schreven bij co-beheer.  

4. Ga naar het tabblad **staging** en wijzig zo nodig de **pilot verzameling** voor een van de werk belastingen.
  
   ![Scherm afbeelding van het tabblad werk belastingen op de pagina met eigenschappen voor co-beheer](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - Voordat u een werk belasting overschakelt, moet u ervoor zorgen dat u de bijbehorende werk belasting correct configureert en implementeert in intune. Zorg ervoor dat workloads altijd worden beheerd door een van de beheer hulpprogramma's voor uw apparaten.
> - Vanaf Configuration Manager versie 1806, wanneer u een werk belasting voor co-beheer overschakelt, wordt het MDM-beleid automatisch gesynchroniseerd vanuit Microsoft Intune. Deze synchronisatie treedt ook op wanneer u de actie **computer beleid downloaden** van client meldingen in de Configuration Manager-console start. Zie [het ophalen van client beleid initiëren met client meldingen](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)voor meer informatie. <!--1357377-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>Werk belastingen overschakelen in versie 1902 en lager

U kunt overstappen op werk belastingen wanneer u co-beheer inschakelt of later wanneer u klaar bent. Als u co-beheer nog niet hebt ingeschakeld, moet u dat eerst doen. Zie [co-beheer inschakelen](how-to-enable.md)voor meer informatie. Nadat u co-beheer hebt ingeschakeld, wijzigt u de instellingen in de eigenschappen voor co-beheer.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt voor **co-beheer** .  

2. Selecteer het object voor co-beheer en kies **Eigenschappen** in het lint.
   - U wordt gevraagd om u aan te melden bij Azure AD. De prompt blokkeert u niet om uw onboarding bij te werken. Telkens wanneer u de pagina **Eigenschappen** opent, wordt u gevraagd om u aan te melden.

3. Schakel over naar het tabblad **werk belastingen** . Standaard worden alle werk belastingen ingesteld op de instelling **Configuration Manager** . Als u wilt overschakelen op een werk belasting, verplaatst u het besturings element schuif regelaar voor de werk belasting naar de gewenste instelling.  

    ![Scherm afbeelding van het tabblad werk belastingen op de pagina met eigenschappen voor co-beheer](media/properties-workloads.png)

    - **Configuration Manager**: Configuration Manager blijft deze werk belasting beheren.  

    - **Pilot intune**: Schakel deze werk belasting alleen uit voor de apparaten in de test verzameling. U kunt de **pilot verzameling** wijzigen op het tabblad **faseren** van de pagina met eigenschappen voor co-beheer.  

    - **Intune**: Schakel deze werk belasting uit voor alle Windows 10-apparaten die zijn Inge schreven bij co-beheer.  

4. Wijzig op het tabblad **fase ring** van de pagina met eigenschappen voor co-beheer de **pilot verzameling** voor uw workloads, indien nodig.

5. Klik op **OK** om eigenschappen voor co-beheer op te slaan en af te sluiten.

> [!Important]  
> - Voordat u een werk belasting overschakelt, moet u ervoor zorgen dat u de bijbehorende werk belasting correct configureert en implementeert in intune. Zorg ervoor dat workloads altijd worden beheerd door een van de beheer hulpprogramma's voor uw apparaten. 
> - Vanaf Configuration Manager versie 1806, wanneer u een werk belasting voor co-beheer overschakelt, wordt het MDM-beleid automatisch gesynchroniseerd vanuit Microsoft Intune. Deze synchronisatie treedt ook op wanneer u de actie **computer beleid downloaden** van client meldingen in de Configuration Manager-console start. Zie [het ophalen van client beleid initiëren met client meldingen](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)voor meer informatie. <!--1357377-->

## <a name="next-steps"></a>Volgende stappen

[Co-beheer bewaken](how-to-monitor.md)

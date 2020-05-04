---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 03/12/2020
ms.openlocfilehash: 37376d137409b06816d4c5dff5a0909f57531443
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710893"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->
1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt voor **co-beheer** . Klik op **co-beheer** in het lint configureren om de **wizard Configuratie van co-beheer**te openen.

2. Configureer op de pagina **abonnement** van de wizard de volgende instellingen:

    - De **Azure-omgeving** die moet worden gebruikt. Bijvoorbeeld de open bare Azure-Cloud of de Azure-Cloud voor de Amerikaanse overheid.<!--4075452-->  

    - Selecteer **Aanmelden**. Meld u aan als een globale Azure AD-beheerder en selecteer **volgende**.  

        > [!TIP]
        > U kunt dit één keer aanmelden voor het doel van deze wizard. De referenties worden niet opgeslagen of elders opnieuw gebruikt.

3. Kies op de pagina **Activering** de volgende instellingen:

   - **Automatische inschrijving in intune** : maakt automatische client inschrijving in intune mogelijk voor bestaande Configuration Manager-clients. Met deze optie kunt u co-beheer inschakelen op een subset van clients om in eerste instantie co-beheer te testen en gezamenlijk beheer te implementeren met behulp van een gefaseerde benadering. Als een apparaat wordt uitgeschreven door de gebruiker, wordt de registratie bij de volgende evaluatie van het beleid opnieuw Inge schreven. <!--3330596-->

      - **Pilot** : alleen de Configuration Manager-clients die lid zijn van de verzameling voor **automatische registratie van intune** , worden automatisch Inge schreven bij intune.
      - **Alle** : automatische inschrijving inschakelen voor alle Windows 10, versie 1709 of hoger, clients.

   - **Automatische inschrijving bij intune** : deze verzameling moet alle clients bevatten die u wilt voorbereiden op co-beheer. Het is in feite een superset van alle andere staging-verzamelingen.

   ![Verzameling voor automatische inschrijving van intune opgeven ](../media/3555750-co-management-onboarding-enablement.png)

      > [!Note]  
      > Vanaf versie 1806 is automatische inschrijving niet direct voor alle clients. Dit gedrag zorgt voor een betere inschrijvings schaal voor grote omgevingen. Configuration Manager is een wille keurige inschrijving op basis van het aantal clients. Als uw omgeving bijvoorbeeld 100.000 clients heeft en u deze instelling inschakelt, vindt de inschrijving meer dan enkele dagen plaats.<!--1358003-->  
      >
      > Vanaf versie 1906:
      >
      > - Een nieuw, door co beheerd apparaat wordt nu automatisch Inge schreven bij de Microsoft Intune-service op basis van het *apparaat* -token van Azure Active Directory (Azure AD). U hoeft niet te wachten totdat een gebruiker zich bij het apparaat aanmeldt voor het starten van de automatische inschrijving. Deze wijziging helpt bij het verminderen van het aantal apparaten met de inschrijvings status *wacht op gebruiker aanmelden*.<!-- 4454491 --> Ter ondersteuning van dit gedrag moet Windows 10, versie 1803 of hoger worden uitgevoerd op het apparaat. Zie voor meer informatie de [inschrijvings status van co-beheer](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - Als u al apparaten hebt geregistreerd voor co-beheer, worden nieuwe apparaten nu onmiddellijk geregistreerd zodra ze voldoen aan de [vereisten](../overview.md#prerequisites).<!--4321130-->

4. Voor apparaten op Internet die al zijn Inge schreven bij intune, kopieert u de opdracht regel en slaat u deze op op de pagina **Activering** . U gebruikt deze opdracht regel om de Configuration Manager-client als een app in intune te installeren voor apparaten op internet. Als u deze opdracht regel nu niet opslaat, kunt u de co-beheer configuratie op elk gewenst moment bekijken om deze opdracht regel op te halen.

5. Kies op de pagina **werk belastingen** voor elke werk belasting welke apparaatgroep u wilt verplaatsen voor beheer met intune. Zie [workloads](../workloads.md)voor meer informatie. Als u co-beheer alleen wilt inschakelen, hoeft u de werk belasting nu niet te wijzigen. U kunt later een andere werk belasting kiezen. Zie [werk belastingen overschakelen](../how-to-switch-workloads.md)voor meer informatie.  

    - **Pilot intune** : Hiermee wordt de bijbehorende werk belasting alleen overgeschakeld voor de apparaten in de test verzamelingen die u opgeeft op de **staging** -pagina. Elke werk belasting kan een andere pilot verzameling hebben.
    - **Intune** : Hiermee schakelt u de bijbehorende werk belasting voor alle met co beheerde Windows 10-apparaten.  

    > [!Important]
    > Voordat u een werk belasting overschakelt, moet u ervoor zorgen dat u de bijbehorende werk belasting correct configureert en implementeert in intune. Zorg ervoor dat workloads altijd worden beheerd door een van de beheer hulpprogramma's voor uw apparaten.  

6. Geef op de pagina voor **fase ring** de pilot verzameling op voor elk van de werk belastingen die zijn ingesteld op **pilot intune**.

   ![Verzameling voor automatische inschrijving van intune opgeven ](../media/3555750-co-management-onboarding-staging.png)

7. Voltooi de wizard om co-beheer in te scha kelen.

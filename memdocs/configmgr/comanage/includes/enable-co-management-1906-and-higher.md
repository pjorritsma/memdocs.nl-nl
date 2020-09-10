---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: b0c25174873e00cf23dacd2c77208775f1fb1ced
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644148"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->

Als u co-beheer inschakelt, kunt u gebruikmaken van de open bare Azure-Cloud, Azure Amerikaanse overheid of Microsoft Azure-China 21Vianet (toegevoegd in versie 2006). Als u co-beheer vanaf Configuration Manager versie 1906 wilt inschakelen, volgt u de onderstaande instructies:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt voor **co-beheer** . Selecteer **co-beheer** in het lint configureren om de **wizard Configuratie van co-beheer**te openen.

1. Configureer op de pagina voor het **voorbereiden van tenants** van de wizard de **Azure-omgeving** die u wilt gebruiken. Kies een van de volgende omgevingen:

   - Open bare Azure-Cloud
   - Azure-Cloud voor de Amerikaanse overheid.<!--4075452-->
   - Azure China-Cloud (toegevoegd in versie 2006)<!--7133238-->
      - Werk de Configuration Manager-client bij naar de nieuwste versie op uw apparaten voordat u de Azure-Cloud voor het eerst opstartt. <!--7630213--> 

   Wanneer u Azure China Cloud of Azure US Government Cloud selecteert, is de optie **uploaden naar micro soft Endpoint Manager-beheer centrum** voor [Tenant koppeling](../../tenant-attach/device-sync-actions.md) uitgeschakeld.

1. Selecteer **Aanmelden.** Meld u aan als een globale Azure AD-beheerder en selecteer **volgende**. U kunt dit één keer aanmelden voor het doel van deze wizard. De referenties worden niet opgeslagen of elders opnieuw gebruikt.

1. Kies op de pagina **Activering** de volgende instellingen:

   - **Automatische inschrijving in intune** : maakt automatische client inschrijving in intune mogelijk voor bestaande Configuration Manager-clients. Met deze optie kunt u co-beheer inschakelen op een subset van clients om in eerste instantie co-beheer te testen en gezamenlijk beheer te implementeren met behulp van een gefaseerde benadering. Als een apparaat wordt uitgeschreven door de gebruiker, wordt de registratie bij de volgende evaluatie van het beleid opnieuw Inge schreven. <!--3330596-->

      - **Pilot** : alleen de Configuration Manager-clients die lid zijn van de verzameling voor **automatische registratie van intune** , worden automatisch Inge schreven bij intune.
      - **Alle** : automatische inschrijving inschakelen voor alle Windows 10, versie 1709 of hoger, clients.

   - **Automatische inschrijving bij intune** : deze verzameling moet alle clients bevatten die u wilt voorbereiden op co-beheer. Het is in feite een superset van alle andere staging-verzamelingen.

   ![Verzameling voor automatische inschrijving van intune opgeven ](../media/3555750-co-management-onboarding-enablement.png)
      
      Automatische inschrijving is niet direct voor alle clients. Dit gedrag zorgt voor een betere inschrijvings schaal voor grote omgevingen. Configuration Manager is een wille keurige inschrijving op basis van het aantal clients. Als uw omgeving bijvoorbeeld 100.000 clients heeft en u deze instelling inschakelt, vindt de inschrijving meer dan enkele dagen plaats.<!--1358003-->

      > [!Note]  
      > Vanaf versie 1906:
      >
      > - Een nieuw, door co beheerd apparaat wordt nu automatisch Inge schreven bij de Microsoft Intune-service op basis van het *apparaat* -token van Azure Active Directory (Azure AD). U hoeft niet te wachten totdat een gebruiker zich bij het apparaat aanmeldt voor het starten van de automatische inschrijving. Deze wijziging helpt bij het verminderen van het aantal apparaten met de inschrijvings status *wacht op gebruiker aanmelden*.<!-- 4454491 --> Ter ondersteuning van dit gedrag moet Windows 10, versie 1803 of hoger worden uitgevoerd op het apparaat. Zie voor meer informatie de [inschrijvings status van co-beheer](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - Als u al apparaten hebt geregistreerd voor co-beheer, worden nieuwe apparaten nu onmiddellijk geregistreerd zodra ze voldoen aan de [vereisten](../overview.md#prerequisites).<!--4321130-->

1. Voor apparaten op Internet die al zijn Inge schreven bij intune, kopieert u de opdracht regel en slaat u deze op op de pagina **Activering** . U gebruikt deze opdracht regel om de Configuration Manager-client als een app in intune te installeren voor apparaten op internet. Als u deze opdracht regel nu niet opslaat, kunt u de co-beheer configuratie op elk gewenst moment bekijken om deze opdracht regel op te halen.

1. Kies op de pagina **werk belastingen** voor elke werk belasting welke apparaatgroep u wilt verplaatsen voor beheer met intune. Zie [workloads](../workloads.md)voor meer informatie. Als u co-beheer alleen wilt inschakelen, hoeft u de werk belasting nu niet te wijzigen. U kunt later een andere werk belasting kiezen. Zie [werk belastingen overschakelen](../how-to-switch-workloads.md)voor meer informatie.  

    - **Pilot intune** : Hiermee wordt de bijbehorende werk belasting alleen overgeschakeld voor de apparaten in de test verzamelingen die u opgeeft op de **staging** -pagina. Elke werk belasting kan een andere pilot verzameling hebben.
    - **Intune** : Hiermee schakelt u de bijbehorende werk belasting voor alle met co beheerde Windows 10-apparaten.  

    > [!Important]
    > Voordat u een werk belasting overschakelt, moet u ervoor zorgen dat u de bijbehorende werk belasting correct configureert en implementeert in intune. Zorg ervoor dat workloads altijd worden beheerd door een van de beheer hulpprogramma's voor uw apparaten.  

1. Geef op de pagina voor **fase ring** de pilot verzameling op voor elk van de werk belastingen die zijn ingesteld op **pilot intune**.

   ![Wizard Configuratie van co-beheer, staging pagina, prototype verzamelingen opgeven](../media/3555750-co-management-onboarding-staging.png)

1. Voltooi de wizard om co-beheer in te scha kelen.

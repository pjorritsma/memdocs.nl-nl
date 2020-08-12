---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 4c669bbbd9f996ae820f695925ba63cd6a92da2a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127296"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
Volg de onderstaande instructies om co-beheer in te scha kelen voor Configuration Manager versie 1902 en eerder:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt voor **co-beheer** . Klik op **co-beheer** in het lint configureren om de **wizard Configuratie van co-beheer**te openen.

2. Selecteer **Aanmelden**op de pagina **abonnement** van de wizard. Meld u aan bij uw intune-Tenant en selecteer **volgende**.  

3. Kies op de pagina **Activering** uw **automatische inschrijving in de intune** -instelling, hetzij **pilot** ofwel **alle**. Als een apparaat wordt uitgeschreven door de gebruiker, wordt de registratie bij de volgende evaluatie van het beleid opnieuw Inge schreven. <!--3330596--> 

    Met deze actie wordt automatische client registratie in intune ingeschakeld voor bestaande Configuration Manager-clients. Wanneer u **pilot**kiest, worden alleen de Configuration Manager-clients die lid zijn van de pilot verzameling automatisch Inge schreven bij intune. Met deze optie kunt u co-beheer inschakelen op een subset van clients om in eerste instantie co-beheer te testen en gezamenlijk beheer te implementeren met behulp van een gefaseerde benadering. 

    Automatische inschrijving is niet direct voor alle clients. Dit gedrag zorgt voor een betere inschrijvings schaal voor grote omgevingen. Configuration Manager is een wille keurige inschrijving op basis van het aantal clients. Als uw omgeving bijvoorbeeld 100.000 clients heeft en u deze instelling inschakelt, vindt de inschrijving meer dan enkele dagen plaats.<!--1358003-->  

4. Voor apparaten op Internet die al zijn Inge schreven bij intune, kopieert u de opdracht regel en slaat u deze op op de pagina **Activering** . U kunt deze opdracht regel gebruiken om de Configuration Manager-client als een app in intune te installeren. Als u deze opdracht regel nu niet opslaat, kunt u de co-beheer configuratie op elk gewenst moment bekijken om deze opdracht regel op te halen.

5. Kies op de pagina **werk belastingen** voor elke werk belasting welke apparaatgroep u wilt verplaatsen voor beheer met intune. Zie [workloads](../workloads.md)voor meer informatie.  

    Als u co-beheer alleen wilt inschakelen, hoeft u de werk belasting nu niet te wijzigen. U kunt later een andere werk belasting kiezen. Zie [werk belastingen overschakelen](../how-to-switch-workloads.md)voor meer informatie.  

    Met de instelling voor de **intune-proef fase** wordt alleen de bijbehorende werk belasting overgeschakeld voor de apparaten in de verzameling prototype. Met de **intune** -instelling wordt de bijbehorende werk belasting overgeschakeld voor alle met co beheerde Windows 10-apparaten.  

    > [!Important]
    > Voordat u een werk belasting overschakelt, moet u ervoor zorgen dat u de bijbehorende werk belasting correct configureert en implementeert in intune. Zorg ervoor dat workloads altijd worden beheerd door een van de beheer hulpprogramma's voor uw apparaten.  

6. Configureer op de pagina voor **fase ring** de volgende instellingen:  

    - **Pilot**: de test groep bevat een of meer verzamelingen die u selecteert. Gebruik deze groep als onderdeel van de gefaseerde implementatie van co-beheer. Begin met een kleine test verzameling en voeg meer verzamelingen toe aan de test groep bij het samen vouwen van co-beheer naar meer gebruikers en apparaten. U kunt de verzamelingen in de test groep op elk gewenst moment wijzigen.  

    - **Productie**: Configureer de **uitsluitings groep** met een of meer verzamelingen. Apparaten die lid zijn van een van de verzamelingen in deze groep, worden uitgesloten van het gebruik van co-beheer.  

7. Voltooi de wizard om co-beheer in te scha kelen.  

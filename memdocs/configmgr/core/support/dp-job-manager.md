---
title: Wachtrijbeheerder DP-taken
titleSuffix: Configuration Manager
description: Gebruik de beheerder van de DP-taak wachtrij voor het oplossen van problemen en het beheren van inhouds distributie taken voor het Configuration Manager van distributie punten.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f6269d559bbcb192b1189419a8450a860d70058
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713658"
---
# <a name="dp-job-queue-manager"></a>Wachtrijbeheerder DP-taken

*Van toepassing op: Configuration Manager (huidige vertakking)*

De taak wachtrij beheerder van het distributie punt (DP) is een van de [Configuration Manager-hulpprogram ma's](tools.md). Gebruik het om lopende inhouds distributie taken te herstellen en te beheren voor het Configuration Manager van distributie punten. 

Het hulp programma geeft de lijst met taken weer die het onderdeel package overdracht Manager heeft in de wachtrij. Ook wordt de status van de taken weer gegeven: gereed om uit te voeren, uit te voeren of opnieuw te proberen. U kunt de taken in de wachtrij bewerken, taken hoger in de lijst plaatsen, een taak annuleren of hand matig starten met het uitvoeren van een taak.

Er wordt ook informatie opgehaald van de site server waarop het distributie punt een taak uitvoert. Het hulp programma maakt verbinding via de provider met de site server. Er wordt geen verbinding gemaakt met elk extern distributie punt om deze informatie te verzamelen. Omdat de IT acties activeert en gegevens ophaalt via de provider, is er een vertraging in de weer spie gelen van externe distributie punten.



## <a name="usage"></a>Gebruik

Voer **DPJobMgr. exe**uit. Het hoofd menu van het hulp programma bevat de volgende tabbladen: 

- [Verbinden](#bkmk_connect): de eerste verbinding met de primaire site server tot stand brengen  

- [Overzicht](#bkmk_overview): Hiermee wordt een overzicht gegeven van alle taken die worden uitgevoerd op alle distributie punten.  

- [Informatie over distributie punt](#bkmk_dp-info): multi-distributie punten selecteren om ze te volgen en een enkele vacature te beheren  

- [Taken beheren](#bkmk_manage-jobs): toont een lijst van alle taken en hun status. Werk taken te bewerken, te verplaatsen, annuleren of hand matig te starten.  


### <a name="connect-tab"></a><a name="bkmk_connect"></a>Tabblad verbinden

Gebruik dit tabblad om de eerste verbinding met de primaire site server tot stand te brengen. Hierbij worden de referenties van de aangemelde gebruiker gebruikt. U kunt geen verbinding maken met de centrale beheer site of secundaire sites. Voor de verbinding is de beveiligingsrol **volledige beheerder** vereist.

Wanneer het hulp programma een verbinding tot stand heeft gebracht, wordt in een melding aan de onderkant van het hulp programma bevestigd dat deze is verbonden met de site server. 


### <a name="overview-tab"></a><a name="bkmk_overview"></a>Tabblad Overzicht

Geeft een samen vatting weer van alle taken op alle distributie punten. Zie de volgende kolommen:  

- **Distributie punt**: hier worden de namen van de distributie punten weer gegeven  

- **Taken uitvoeren**: toont het aantal gelijktijdige taken dat wordt uitgevoerd op een bepaald distributie punt.  

    > [!Tip]  
    > Het aantal gelijktijdige software distributies is een site-instelling. Deze instelling is gewijzigd in de eigenschappen van het software distributie onderdeel.  

- **Totaal aantal taken**: toont het aantal taken dat is gericht op een bepaald distributie punt. Dit aantal bevat de taken die worden uitgevoerd, opnieuw proberen of wachten op uitvoering.  

- **Totaal aantal nieuwe pogingen**: toont het aantal keren dat taken opnieuw zijn uitgevoerd in een bepaald distributie punt. Een hoger nummer kan een algemeen probleem met het desbetreffende distributie punt vertegenwoordigen.  


> [!Tip]  
> - Als u elke kolom op dit tabblad wilt sorteren, klikt u op de kolom naam  
> 
> - Vernieuw de informatie op dit tabblad hand matig door op **vernieuwen** te klikken  
> 
> - Vernieuw automatisch de informatie op dit tabblad door te klikken op **automatisch vernieuwen starten** en het interval voor automatisch vernieuwen in te stellen. Het standaard Vernieuwings interval is twee minuten.  


### <a name="distribution-point-info-tab"></a><a name="bkmk_dp-info"></a>Tabblad informatie over distributie punt

Hiermee wordt de lijst met alle distributie punten weer gegeven onder de verbonden site. In het deel venster aan de linkerkant worden alle distributie punten weer gegeven. Klik op **Alles selecteren** of **Selecteer alles** als dat nodig is, of selecteer specifieke distributie punten in deze lijst. In het deel venster aan de rechter kant worden de taken voor de geselecteerde distributie punten weer gegeven.

Er zijn acht kolommen:  

- **Status pictogram**: er zijn drie mogelijke status pictogrammen:  

    - **Gereed**: geeft aan dat een bepaalde taak alle verificaties tappen heeft voltooid. Het is klaar om te worden toegevoegd aan de actieve gelijktijdige taken. Taken in deze status zijn meestal in een wacht fase. Ze wachten op het volt ooien van de huidige actieve processen om een ruimte te openen.  

    - **Uitvoeren**: geeft aan dat er momenteel een bepaalde taak wordt uitgevoerd op een distributie punt. Voor langlopende taken (grote pakketten) is er meestal tijd om de voortgang te verkrijgen (%) tot voltooiing. Dit percentage wordt weer gegeven in de kolom **voortgang** in deze weer gave. Voor kleine pakketten kan de kolom **voortgang** leeg blijven. De taak wordt mogelijk al voltooid op het moment dat het de status ontvangt van het externe distributie punt.  

    - **Nieuwe poging**: geeft aan dat een bepaalde taak is mislukt en nu een nieuwe status heeft. Er wordt opnieuw geprobeerd om deze taak uit te voeren na het interval voor opnieuw proberen. Dit interval is configureerbaar en is standaard ingesteld op 30 minuten.  

- **Software**: naam van het pakket dat is gericht op een bepaald distributie punt  

- **Pakket-id**: pakket-id van het pakket dat is gericht op een bepaald distributie punt  

- **Grootte**: grootte van het pakket in KB  

- **Voortgang**: percentage taak voltooiing. Zie de beschrijving van het pictogram van de **actieve** status voor meer informatie.  

- **Tijdstip van starten/opnieuw opstarten**: voor een actieve taak is deze waarde de start tijd (groen). Voor een nieuwe taak is deze waarde het tijdstip waarop de taak opnieuw wordt uitgevoerd.  

- **Nieuwe pogingen**: het aantal keren dat het pakket opnieuw is geprobeerd.  

- **Naam van distributie punt**: de Fully QUALIFIED domain name (FQDN) van het distributie punt  

> [!Tip]  
> - Als u elke kolom op dit tabblad wilt sorteren, klikt u op de kolom naam  
> 
> - Vernieuw de informatie op dit tabblad hand matig door op **vernieuwen** te klikken  
> 
> - Vernieuw automatisch de informatie op dit tabblad door te klikken op **automatisch vernieuwen starten** en het interval voor automatisch vernieuwen in te stellen. Het standaard Vernieuwings interval is twee minuten.  
> 
> - Als u een bepaalde taak moet wijzigen, klikt u met de rechter muisknop op de taak in deze weer gave en selecteert u **taak beheren**. Met deze actie opent u het [tabblad taken beheren](#bkmk_manage-jobs).  


### <a name="manage-jobs-tab"></a><a name="bkmk_manage-jobs"></a>Tabblad taken beheren

Wordt weer gegeven in één platte weer gave een lijst van alle taken en hun status. Het bevat dezelfde acht kolommen als het [tabblad informatie over het distributie punt](#bkmk_dp-info). In deze weer gave klikt u met de rechter muisknop op de taken voor de volgende acties:  

- **Uitvoeren**: start een taak die in een andere staat is dan wordt uitgevoerd  

- **Naar boven verplaatsen**: verplaatst een of meer taken naar de bovenkant van de wachtrij. Deze actie kan ertoe leiden dat de taken onmiddellijk worden uitgevoerd. Een taak met een lagere prioriteit kan worden onderbroken vanwege deze actie.  

- Omhoog: Hiermee verplaatst **u**een bepaalde taak één rij hierboven. Een taak met een lagere prioriteit kan worden onderbroken als gevolg van deze actie.  

- **Omlaag**: Hiermee verplaatst u een bepaalde taak naar een rij onder.  

- Naar **beneden verplaatsen**: verplaatst een of meer taken naar de onderkant van de wachtrij.  

    > [!Tip]  
    > Taken slepen en neerzetten in de lijst om ze te verplaatsen.  

- **Annuleren**: probeert een of meer taken te annuleren.  

    > [!Note]  
    > U kunt geen taken in de buurt van de laatste voltooiings tijd annuleren. Als de site server ook een distributie punt is, kunt u geen taken op de site server annuleren.  



## <a name="see-also"></a>Zie ook

- [Basisconcepten voor inhoudsbeheer](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Package overdrachts Manager](../plan-design/hierarchy/package-transfer-manager.md)

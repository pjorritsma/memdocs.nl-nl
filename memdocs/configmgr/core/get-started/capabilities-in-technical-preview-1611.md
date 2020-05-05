---
title: Mogelijkheden van Technical Preview 1611
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1611.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e1348e9d230a5525a91e7e7dceea4da6d1311b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721547"
---
# <a name="capabilities-in-technical-preview-1611-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1611 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*



Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1611. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    

**Bekende problemen in deze technische preview:**   
- ***Status***van de vereiste: wanneer u versie 1611 installeert, kan de algemene status voor vereisten worden weer gegeven als door gegeven met waarschuwingen, maar wordt niet vermeld welke vereisten de waarschuwingen hebben veroorzaakt. Dit kan worden veroorzaakt door de volgende twee vereisten:
  - Opties voor het maken van SQL-index geheugen
  - Controleert op ondersteunde SQL Server versie  

  Omdat dit alleen waarschuwingen zijn, kunnen ze worden genegeerd.

- ***Power shell***: wanneer u vanuit de Configuration Manager-console verbinding maakt met Windows Power shell, wordt mogelijk de volgende fout weer gegeven: **micro soft. ConfigurationManagement. Power shell. types. ps1xml is niet digitaal ondertekend**.  

   U kunt dit probleem oplossen door bepaalde bestanden te vervangen door ondertekende versies van versie 1610. Kopieer alle bestanden met de volgende extensies uit de ** &lt;map install directory>\\ \adminconsole\bin** in uw versie 1610-installatie: **. psd1**, **. ps1xml**en **. psm1**. Plak deze bestanden in de ** &lt;map install directory>\\ \adminconsole\bin** in uw Technical Preview 1611-installatie en het overschrijven van de 1611-versie van de bestanden.


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Inhoud vooraf in cache opslaan voor beschik bare implementaties en taken reeksen
In deze Technical Preview, voor beschik bare implementaties en taken reeksen, kunt u ervoor kiezen de functie vooraf-cache te gebruiken om ervoor te zorgt dat clients alleen relevante inhoud downloaden voordat een gebruiker de inhoud installeert.

Stel bijvoorbeeld dat u een taken reeks voor Windows 10-in-place upgrade wilt implementeren, alleen een enkele taken reeks voor alle gebruikers wilt en meerdere architecturen en/of talen hebt. Als u in Current Branch een beschik bare implementatie maakt en vervolgens op **installeren** in Software Center klikt, wordt de inhoud op dat moment gedownload. Hiermee voegt u extra tijd toe voordat de installatie gereed is om te starten. Als u een beschik bare taken reeks implementatie maakt, wordt in Current Branch ook alle inhoud gedownload waarnaar in de taken reeks wordt verwezen. Dit omvat het upgrade pakket voor het besturings systeem voor alle talen en architecturen. Als elk ongeveer 3 GB groot is, kan het Download pakket erg groot zijn.

De functie voor inhoud in de cache biedt u de mogelijkheid om de client toe te staan de toepasselijke inhoud te downloaden zodra deze de implementatie ontvangt. Als de gebruiker klikt op **installeren** in Software Center, is de inhoud daarom gereed en wordt de installatie snel gestart, omdat de inhoud zich op de lokale harde schijf bevindt.

### <a name="to-configure-the-pre-cache-feature"></a>De functie vooraf-cache configureren

1. Upgrade pakketten voor besturings systemen maken voor specifieke architecturen en talen. Geef de architectuur en taal op het tabblad **gegevens bron** van het pakket op. Voor de taal gebruikt u de decimale conversie (bijvoorbeeld 1033 is de decimale waarde voor Engels en 0x0409 is het hexadecimale equivalent). Zie [een taken reeks maken om een besturings systeem bij te werken](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)voor meer informatie.

    De waarden voor de architectuur en de taal worden gebruikt om te voldoen aan de voor waarden voor de taken reeks stap die u in de volgende stap maakt om te bepalen of het upgrade pakket van het besturings systeem vooraf in het cache geheugen moet worden opgeslagen.
2. Maak een taken reeks met voorwaardelijke stappen voor de verschillende talen en architecturen. U kunt bijvoorbeeld voor de Engelse versie een stap maken zoals in het volgende:

    ![eigenschappen vóór cache](media/precacheproperties2.png)

    ![opties vóór cache](media/precacheoptions2.png)  

3. Implementeer de taken reeks. Configureer het volgende voor de functie vóór de cache:
    - Selecteer op het tabblad **Algemeen** de optie **inhoud vooraf downloaden voor deze taken reeks**.
    - Configureer op het tabblad **implementatie-instellingen** de taken reeks met de **functie** **beschikbaar** voor. Als u een **vereiste** implementatie maakt, werkt de functie vóór de cache niet.
    - Op het tabblad **planning** , voor de **planning wanneer deze implementatie beschikbaar** is, kiest u een tijd in de toekomst waarmee clients voldoende tijd hebben om de inhoud vooraf in het cache geheugen te plaatsen voordat de implementatie beschikbaar wordt gesteld aan gebruikers. U kunt bijvoorbeeld de beschik bare tijd 3 uur in de toekomst instellen om voldoende tijd te hebben om de inhoud vooraf in cache te plaatsen.  
    - Configureer op het tabblad **distributie punten** de instellingen voor de **implementatie opties** . Als de inhoud niet vooraf in de cache op een client wordt opgeslagen voordat een gebruiker de installatie start, worden deze instellingen gebruikt.


### <a name="user-experience"></a>Gebruikerservaring
- Wanneer de client het implementatie beleid ontvangt, wordt de inhoud vooraf in de cache geplaatst. Dit omvat alle inhoud waarnaar wordt verwezen (alle andere pakket typen) en alleen het upgrade pakket van het besturings systeem dat overeenkomt met de client op basis van de voor waarden die u in de taken reeks hebt ingesteld.
- Wanneer de implementatie beschikbaar wordt gesteld aan gebruikers (op het tabblad **planning** van de implementatie), wordt er een melding weer gegeven om gebruikers te informeren over de nieuwe implementatie en wordt de implementatie zichtbaar in Software Center. De gebruiker kan naar Software Center gaan en op **installeren** klikken om de installatie te starten.
- Als de inhoud niet volledig in de cache is opgeslagen, worden de instellingen gebruikt die zijn opgegeven op het tabblad **implementatie optie** van de implementatie. We raden u aan dat er voldoende tijd is tussen het moment waarop de implementatie wordt gemaakt en het tijdstip waarop de implementatie beschikbaar wordt voor gebruikers om clients voldoende tijd te bieden om de inhoud vooraf in de cache op te slaan.


## <a name="see-also"></a>Zie ook
[Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md)

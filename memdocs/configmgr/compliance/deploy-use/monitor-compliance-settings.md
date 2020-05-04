---
title: Instellingen voor naleving bewaken
titleSuffix: Configuration Manager
description: Gebruik een of meer van de procedures in dit onderwerp om de nalevings status van de configuratie basislijn weer te geven.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 839c08c8782a815703a19999bf1315fd65980ed8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712293"
---
# <a name="monitor-compliance-settings-in-configuration-manager"></a>Nalevings instellingen in Configuration Manager bewaken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u Configuration Manager configuratie basislijnen hebt geïmplementeerd op apparaten in uw hiërarchie, kunt u een of meer van de procedures in dit onderwerp gebruiken om de nalevings status van de configuratie basislijn weer te geven:

> [!NOTE]  
>  De validatiecriteriavelden in de rapporten met instellingen voor naleving (het equivalent van het rapport aan de kant van de client is **Beperkingen**) geven het onderliggende SML (Service Modeling Language) weer. Dit kan moeilijk maken voor beheerders die het configuratie-item in de Configuration Manager-console hebben gemaakt om te begrijpen wat de validatie criteria zijn als ze geen kennis hebben van SML. In dit geval gebruikt u de werk ruimte **bewaking** in de Configuration Manager-console om de eigenschappen van het configuratie-item en de validatie criteria ervan weer te geven.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Nalevingsresultaten weergeven in de Configuration Manager-console  
 Gebruik deze procedure om details te bekijken over de naleving van geïmplementeerde configuratie basislijnen in de Configuration Manager-console.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Nalevingsresultaten weergeven in de Configuration Manager-console  

1.  Klik in de Configuration Manager-console op **bewakings** > **implementaties**.  

3.  Selecteer in de lijst **Implementaties** de implementatie van de configuratiebasislijn waarvoor u compatibiliteitsgegevens wilt bekijken.  

4.  U kunt samenvattingsinformatie controleren over de naleving van de implementatie van configuratiebasislijnen op de hoofdpagina. Selecteer, om meer gedetailleerde informatie te zien, de implementatie van de configuratiebasislijn en klik dan op het tabblad **Start** , in de groep **Implementatie** op **Status weergeven** om de pagina **Implementatiestatus** te openen.  

     De pagina **Implementatiestatus** bevat de volgende tabbladen:  

    -   **Compatibel**: geeft de naleving van de configuratiebasislijn weer op basis van het aantal beïnvloede activa. U kunt klikken op een regel om een tijdelijk knooppunt te maken onder het knooppunt **Gebruikers** of het knooppunt **Apparaten** in de werkruimte **Activa en naleving**, die alle gebruikers of apparaten bevat die compatibel zijn met deze regel. Het deelvenster **Activumgegevens** geeft de gebruikers of apparaten weer die compatibel zijn met de configuratiebasislijn. Dubbelklik op een gebruiker of apparaat in de lijst om extra informatie weer te geven.  

        > [!IMPORTANT]  
        >  Een regel voor een configuratie-item wordt niet geëvalueerd als deze niet wordt gedetecteerd of niet van toepassing is op een client apparaat. de regel wordt echter als compatibel geretourneerd.  

    -   **Fout**: geeft een lijst weer met alle fouten voor de geselecteerde configuratiebasislijnimplementatie op basis van het aantal betrokken activa. U kunt klikken op een regel om een tijdelijk knooppunt te maken onder het knooppunt **Gebruikers** of het knooppunt **Apparaten** in de werkruimte **Activa en naleving**, die alle gebruikers bevat die fouten genereerden met deze regel. Wanneer u een gebruiker of apparaat selecteert, geeft het deelvenster **Activumgegevens** de gebruikers of apparaten weer die met het geselecteerde probleem te maken hebben. Dubbelklik op een gebruiker of apparaat in de lijst om aanvullende informatie over het probleem weer te geven.  

    -   **Niet-naleving**: geeft een lijst weer met alle niet-nalevingsregels in de configuratiebasislijn op basis van het aantal betrokken activa. U kunt klikken op een regel om een tijdelijk knooppunt te maken onder het knooppunt **Gebruikers** of het knooppunt **Apparaten** van de werkruimte **Activa en naleving**, die alle gebruikers of apparaten bevat die niet compatibel met deze regel zijn. Wanneer u een gebruiker of apparaat selecteert, geeft het deelvenster **Activumgegevens** de gebruikers of apparaten weer die met het geselecteerde probleem te maken hebben. Dubbelklik op een gebruiker of apparaat in de lijst om aanvullende informatie weer te geven over het probleem.  

    -   **Onbekend**: geeft een lijst weer met alle gebruikers en apparaten die geen naleving hebben gerapporteerd voor de geselecteerde configuratiebasislijn, samen met de huidige clientstatus van apparaten.  

5.  Op de pagina **Implementatiestatus** kunt u gedetailleerde informatie over de naleving van de geïmplementeerde configuratiebasislijn weergeven. Een tijdelijk knooppunt wordt gemaakt onder het knooppunt **Implementaties** waarmee u deze informatie snel kunt terugvinden.  

##  <a name="view-compliance-results-by-using-reports"></a>Nalevings resultaten weer geven met behulp van rapporten  
 De instellingen voor naleving in Configuration Manager bevatten een aantal ingebouwde rapporten waarmee u informatie over configuratie-items, configuratie basislijnen en implementaties kunt bewaken. Deze rapporten hebben de rapportcategorie van **Compatibiliteit en instellingen beheren**.  

> [!IMPORTANT]  
>  U moet een Joker teken (**%**) gebruiken wanneer u de para meters **apparaat filter** en gebruikers filter gebruikt in de rapporten met instellingen voor naleving.  

 Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over het configureren van rapportage in Configuration Manager.

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Nalevings resultaten weer geven op een Configuration Manager Windows-client computer

> [!NOTE]  
>  U kunt geen informatie weer geven op de Configuration Manager Windows-client als u bent aangemeld met een domein gast account.    

1.  Navigeer naar **Configuration Manager** in het Configuratiescherm van de clientcomputer en dubbelklik om de eigenschappen ervan te openen.  

2.  Klik op het tabblad **Configuraties** en bekijk de lijst met geïmplementeerde configuratiebasislijnen.  

3.  Bekijk de **Compatibiliteitsstatus** voor elke configuratiebasislijn:  

    > [!IMPORTANT]  
    >  De resultaten van de beoordeling worden gedurende 15 minuten in cache op de client bewaard. Als u een nieuwe beoordeling binnen de periode van 15 minuten start, worden de compatibiliteitsresultaten uit deze cache geretourneerd en niet van een nieuwe beoordeling. Dus als u een wijziging op de client aanbrengt die van invloed kan zijn op de resultaten van de nalevingsbeoordelingen, wacht dan tot de 15 minuten zijn verstreken voordat u een nieuwe beoordeling begint.  

    -   **Compatibel**: de clientcomputer leeft de geëvalueerde configuratiebasislijn na.  

    -   **Niet-compatibel**: de clientcomputer leeft de geëvalueerde configuratiebasislijn niet na.  

    -   **Onbekend**: de configuratiebasislijn van de clientcomputer is nog niet geëvalueerd. Als u beoordeling buiten de planning voor nalevingsbeoordeling wilt initiëren, selecteert u de te beoordelen configuratiebasislijnen en klikt u vervolgens op **Evalueren**.  

        > [!NOTE]  
        >  Als u lokale beheerdersreferenties op de clientcomputer hebt, kunt u de details van elke geëvalueerde configuratiebasislijn bekijken om te bepalen welk configuratie-item als niet-compatibel wordt gerapporteerd. Selecteer de configuratiebasislijn en klik vervolgens op **Rapport weergeven**om dit te doen.  

4.  Klik op **OK**.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Verzamelingen maken op basis van naleving van de configuratie basislijn  
 Gebruik de volgende procedure om een Configuration Manager verzameling te maken op basis van apparaten met een opgegeven naleving. U kunt verzamelingen maken op basis van de volgende nalevingsstatussen:  

-   **Compatibel**  

-   **Fout**  

-   **Niet compatibel**  

-   **Onbekend**  

1.  Klik in de Configuration Manager-console op **activa en naleving** > **instellingen** > **configuratie basislijnen**.  

3.  Selecteer in de lijst **Configuratiebasislijnen** de configuratiebasislijn vanwaaruit u een verzameling wilt maken.  

4.  Klik op het tabblad **Implementatie** in de **Implementatiegroep**op **Nieuwe verzameling maken** en selecteer vervolgens in de vervolgkeuzelijst het nalevingsniveau waarvoor u een verzameling wenst te maken.  

5.  De **Wizard Gebruikersverzameling maken** of de **Wizard Apparaatverzameling maken** wordt geopend, afhankelijk van het gegeven of het configuratie-item wordt geïmplementeerd voor gebruikers of apparaten. De wizard wordt automatisch ingevuld met de juiste waarden om de verzameling te maken; u kunt deze waarden echter bewerken.  

6.  Nadat u de wizard hebt voltooid, wordt de verzameling weergegeven in het knooppunt **Gebruikersverzamelingen** of het knooppunt **Apparaatverzamelingen** in de werkruimte **Activa en naleving** .  

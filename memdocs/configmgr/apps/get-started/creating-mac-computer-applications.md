---
title: Mac-computertoepassingen maken
titleSuffix: Configuration Manager
description: Bekijk welke overwegingen u moet meenemen wanneer u toepassingen voor Mac-computers maakt en implementeert.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3b734dc6149c1613d986205577b46160d363d31d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075785"
---
# <a name="create-mac-computer-applications-with-configuration-manager"></a>Mac-computer toepassingen maken met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Houd rekening met de volgende overwegingen wanneer u toepassingen voor Mac-computers maakt en implementeert.  

> [!IMPORTANT]  
>  De procedures in dit onderwerp hebben betrekking op informatie over het implementeren van toepassingen op Mac-computers waarop u de Configuration Manager-client hebt geïnstalleerd. Mac-computers die u hebt ingeschreven bij Microsoft Intune, bieden geen ondersteuning voor de implementatie van toepassingen.  

## <a name="general-considerations"></a>Algemene overwegingen  
 U kunt Configuration Manager gebruiken om toepassingen te implementeren op Mac-computers waarop de Configuration Manager Mac-client wordt uitgevoerd. De stappen voor het implementeren van software op Mac-computers zijn vergelijkbaar met de stappen voor het implementeren van software op Windows-computers. Houd echter rekening met het volgende voordat u toepassingen maakt en implementeert voor Mac-computers die worden beheerd door Configuration Manager:  

-   Voordat u Mac-toepassings pakketten kunt implementeren op Mac-computers, moet u het **CMAppUtil** -hulp programma op een Mac-computer gebruiken om deze toepassingen te converteren naar een indeling die kan worden gelezen door Configuration Manager.  

-   Configuration Manager biedt geen ondersteuning voor de implementatie van Mac-toepassingen voor gebruikers. In plaats daarvan moeten deze implementaties worden uitgevoerd op een apparaat. Voor Mac-toepassings implementaties biedt Configuration Manager niet de optie **software implementeren op het primaire apparaat** van de gebruiker op de pagina **implementatie-instellingen** van de **wizard software implementeren**.  

-   Mac-toepassingen ondersteunen gesimuleerde implementaties.  

-   U kunt geen toepassingen implementeren op Mac-computers die het doel **Beschikbaar**hebben.  

-   De optie om ontwaakpakketten te zenden wanneer u software implementeert, is niet ondersteund voor Mac-computers.  

-   Mac-computers bieden geen ondersteuning voor Background Intelligent Transfer Service (BITS) voor het downloaden van toepassings inhoud. Als het downloaden van een toepassing mislukt, wordt deze vanaf het begin opnieuw opgestart.  

-   Configuration Manager biedt geen ondersteuning voor globale voor waarden wanneer u implementatie typen voor Mac-computers maakt.  

## <a name="steps-to-create-and-deploy-an-application"></a>Stappen voor het maken en implementeren van een toepassing  
 De volgende tabel bevat de stappen, Details en informatie voor het maken en implementeren van toepassingen voor Mac-computers.  


|                                         Stap                                          |                                                                                                             Details                                                                                                              |
|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|            **Stap 1**: Mac-toepassingen voorbereiden voor Configuration Manager             | Voordat u Configuration Manager toepassingen van Mac-software pakketten kunt maken, moet u het **CMAppUtil** -hulp programma op een Mac-computer gebruiken om de Mac-software te converteren naar een Configuration Manager<strong>. cmmac</strong> -bestand. |
| **Stap 2**: een Configuration Manager-toepassing maken die de Mac-software bevat |                                                                       Gebruik de **wizard toepassing maken** om een toepassing te maken voor de Mac-software.                                                                       |
|             **Stap 3**: een implementatie type voor de Mac-toepassing maken              |                                                              Deze stap is enkel vereist indien u niet automatisch deze informatie importeerde van de toepassing.                                                               |
|                        **Stap 4**: de Mac-toepassing implementeren                         |                                                                          Gebruik de **wizard software implementeren** om de toepassing op Mac-computers te implementeren.                                                                          |
|               **Stap 5**: de implementatie van de Mac-toepassing bewaken               |                                                                                 Het slagingspercentage van toepassingsimplementaties voor Mac-computers bewaken.                                                                                 |

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Aanvullende procedures voor het maken en implementeren van toepassingen voor Mac-Computers  
 Gebruik de volgende procedures om toepassingen te maken en te implementeren voor Mac-computers die worden beheerd door Configuration Manager.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Stap 1: Mac-toepassingen voor Configuration Manager voorbereiden  
 Het proces voor het maken en implementeren van Configuration Manager-toepassingen op Mac-computers is vergelijkbaar met het implementatie proces voor Windows-computers. Voordat u echter Configuration Manager-toepassingen maakt die Mac-implementatie typen bevatten, moet u de toepassingen voorbereiden met het hulp programma **CMAppUtil** . Dit hulpprogramma is gedownload met de installatiebestanden van de Mac-client. Met het hulpprogramma **CMAppUtil** wordt informatie over de toepassing verzameld, waaronder gegevens van de volgende Mac-pakketten:  

-   Apple-schijfimage (.dmg)  

-   Metapakketbestand (MPKG)  

-   Mac OS X Installer-pakket (.pkg)  

-   Mac OS X-toepassing (.app)  

Nadat het hulpprogramma **CMAppUtil** toepassingsgegevens heeft verzameld, wordt een bestand gemaakt met de extensie **.cmmac**. Dit bestand bevat installatiebestanden voor de Mac-software en informatie over detectiemethodes die gebruikt kunnen worden om te beoordelen of de toepassing reeds geïnstalleerd is. Met **CMAppUtil** kunt u ook **DMG**-bestanden verwerken die meerdere Mac-toepassingen bevatten, en kunt u voor elke toepassing andere implementatietypen maken.  

1.  Kopieer het installatiepakket voor de Mac-software naar de map op de Mac-computer waarnaar u de inhoud hebt uitgepakt van het bestand **macclient.dmg** dat u hebt gedownload van het Microsoft Downloadcentrum.  

2.  Open op dezelfde Mac-computer een terminalvenster en ga naar de map waarnaar u de inhoud van het bestand **macclient.dmg** hebt uitgepakt.  

3.  Ga naar de map **Hulpprogram ma's** en typ de volgende opdracht regel opdracht:  

     **./CMAppUtil** *<eigenschappen\>*  

     Stel bijvoorbeeld dat u de inhoud wilt converteren van een Apple-schijf kopie bestand met de naam **MySoftware. dmg** dat is opgeslagen in de map Bureau blad van de gebruiker in een **cmmac** -bestand in dezelfde map. U wilt ook **cmmac** -bestanden maken voor alle toepassingen die zijn gevonden in het schijf kopie bestand. Gebruik hiervoor de volgende opdrachtregel:  

     **./CMApputil –c /Gebruikers/** *<gebruikersnaam\>* **/Bureaublad/MySoftware.dmg -o /Gebruikers/** *<gebruikersnaam\>* **/Bureaublad -a**  

    > [!NOTE]  
    >  De naam van de toepassing mag niet langer zijn dan 128 tekens.  

     Gebruik de opdrachtregeleigenschappen in de volgende tabel als u opties wilt configureren voor **CMAppUtil**:  

    |Eigenschap|Meer informatie|  
    |--------------|----------------------|  
    |**-h**|Geeft de beschikbare eigenschappen van de opdrachtregel weer.|  
    |**-r**|Voert de **detection.xml** van het opgegeven **CMMAC**-bestand uit naar **stdout**. De uitvoer bevat de detectieparameters en de versie van **CMAppUtil** waarmee het **CMMAC**-bestand is gemaakt.|  
    |**-c**|Hiermee geeft u het bron bestand moet worden geconverteerd.|  
    |**-o**|Hiermee geeft u het uitvoerpad in combi natie met de – c-eigenschap.|  
    |**-a**|Maakt automatisch. cmmac-bestanden in combi natie met de – c-eigenschap voor alle toepassingen en pakketten in het schijf kopie bestand.|  
    |**-s**|Hiermee slaat u het genereren van het bestand **detection.xml** over als er geen detectieparameters worden gevonden. Het **CMMAC** -bestand wordt dan zonder het bestand **detection.xml** gemaakt.|  
    |**-v**|Hiermee wordt meer gedetailleerde uitvoer van het hulpprogramma **CMAppUtil** evenals diagnostische informatie weergegeven.|  

4.  Controleer of het **CMMAC** -bestand in de opgegeven uitvoermap is gemaakt.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Een Configuration Manager-toepassing maken die de Mac-software bevat  

Gebruik de volgende procedure om u te helpen een toepassing te maken voor Mac-computers die worden beheerd door Configuration Manager.  

1.  Kies **software bibliotheek** > toepassingen voor**toepassings beheer** > in de Configuration Manager-**console.**  

3.  Kies op het tabblad **Start** in de groep **maken** de optie **toepassing maken**.  

4.  Selecteer op de pagina **Algemeen** van de **wizard toepassing maken**de optie **automatisch informatie over deze toepassing detecteren uit installatie bestanden**.  

    > [!NOTE]  
    >  Als u zelf informatie over de toepassing wilt opgeven, selecteert u **hand matig de toepassings gegevens opgeven**. Zie [toepassingen maken met Configuration Manager](../../apps/deploy-use/create-applications.md)voor meer informatie over het hand matig opgeven van de informatie.  

5.  Selecteer in de vervolgkeuzelijst **Type** de optie **Mac OS X**.  

6.  Geef in het veld **locatie** het UNC-pad op in het formulier * \\ \\<\> \\ server<\> \\<bestands\> naam te delen* naar het installatie bestand van de Mac-toepassing (**. cmmac** -bestand) dat de toepassings informatie zal detecteren. U kunt ook op **Bladeren** klikken om naar de locatie van het installatie bestand te bladeren en deze op te geven.  

    > [!NOTE]  
    >  U moet toegang hebben tot het UNC-pad dat de toepassing bevat.  

7.  Kies **Volgende**.  

8.  Controleer op de pagina **informatie importeren** van de **wizard toepassing maken**de gegevens die zijn geïmporteerd. Als dat nodig is, kunt u **vorige** kiezen om terug te gaan en eventuele fouten te corrigeren. Klik op **volgende** om door te gaan.  

9. Geef op de pagina **algemene informatie** van de **wizard toepassing maken**informatie op over de toepassing, zoals de toepassings naam, opmerkingen, versie en een optionele referentie waarmee u in de Configuration Manager-console naar de toepassing kunt verwijzen.  

    > [!NOTE]  
    >  Een deel van de toepassings informatie bevindt zich mogelijk al op deze pagina als deze eerder werd verkregen van de installatie bestanden van de toepassing.  

10. Klik op **volgende**, Controleer de toepassings gegevens op de pagina **samen vatting** en voltooi vervolgens de **wizard toepassing maken**.  

11. De nieuwe toepassing wordt weer gegeven in het knoop punt **toepassingen** van de Configuration Manager-console.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Stap 3: een implementatietype voor de Mac-toepassing maken  
 Gebruik de volgende procedure om u te helpen bij het maken van een implementatie type voor Mac-computers die worden beheerd door Configuration Manager.  

> [!NOTE]  
>  Als u automatisch informatie over de toepassing hebt geïmporteerd in de **wizard toepassing maken**, is er mogelijk al een implementatie type voor de toepassing gemaakt.  

1.  Kies **software bibliotheek** > toepassingen voor**toepassings beheer** > in de Configuration Manager-**console.**  

3.  Selecteer een toepassing. Klik vervolgens op het tabblad **Start** in de groep **toepassing** op **implementatie type maken** om een nieuw implementatie type voor deze toepassing te maken.  

    > [!NOTE]  
    >  U kunt de **wizard implementatie type maken** ook starten vanuit de **wizard toepassing maken** en op het tabblad **implementatie typen** van het dialoog venster **Eigenschappen** van *<toepassing\> * .  

4.  Selecteer op de pagina **Algemeen** van de **wizard implementatie type maken**in de vervolg keuzelijst **type** de optie **Mac OS X**.  

5.  Geef in het veld **locatie** het UNC-pad op in het \\ \\ formulier<\> \\ server<\> \\<bestands\> naam te delen naar het installatie bestand van de toepassing (**. cmmac** -bestand). U kunt ook op **Bladeren** klikken om naar de locatie van het installatie bestand te bladeren en deze op te geven.  

    > [!NOTE]  
    >  U moet toegang hebben tot het UNC-pad dat de toepassing bevat.  

6.  Kies **Volgende**.  

7.  Controleer op de pagina **Informatie importeren** van de **Wizard implementatietype maken**de informatie die is geïmporteerd. Klik indien nodig op **vorige** om terug te gaan en eventuele fouten te corrigeren. Kies **Volgende** om door te gaan.  

8.  Geef op de pagina **Algemene informatie** van de **wizard Implementatietype maken**informatie op over de toepassing, zoals de toepassingsnaam, opmerkingen en de talen waarin het implementatietype beschikbaar is.  

    > [!NOTE]  
    >  Een deel van de implementatie type-informatie is mogelijk al aanwezig op deze pagina als deze eerder werd verkregen van de installatie bestanden van de toepassing.  

9. Kies **Volgende**.  

10. Op de pagina **vereisten** van de **wizard implementatie type maken**kunt u de voor waarden opgeven waaraan moet worden voldaan voordat het implementatie type op Mac-computers kan worden geïnstalleerd.  

11. Kies **toevoegen** om het dialoog venster **vereiste maken** te openen en een nieuwe vereiste toe te voegen.  

    > [!NOTE]  
    >  U kunt ook nieuwe vereisten toevoegen op het tabblad **vereisten** van het dialoog venster naam **Properties** *\> eigenschappen van<implementatie type* .  

12. Selecteer in de vervolgkeuzelijst **Categorie** dat dit een vereiste voor een apparaat is.  

13. Selecteer in de vervolg keuzelijst **voor waarde** de voor waarde die u wilt gebruiken om te beoordelen of de Mac-computer voldoet aan de installatie vereisten. De inhoud van deze lijst varieert afhankelijk van de categorie die u selecteert.  

14. Kies in de vervolg keuzelijst **operator** de operator die moet worden gebruikt om de geselecteerde voor waarde te vergelijken met de opgegeven waarde om te beoordelen of de gebruiker of het apparaat voldoet aan de installatie vereisten. De beschik bare Opera tors variëren afhankelijk van de geselecteerde voor waarde.  

15. Geef in het veld **waarde** de waarden op die moeten worden gebruikt met de geselecteerde voor waarde en operator om te beoordelen of de gebruiker of het apparaat voldoet aan de installatie vereiste. De beschik bare waarden variëren, afhankelijk van de voor waarde en de operator die u selecteert.

16. Kies **OK** om de regel voor vereisten op te slaan en het dialoog venster **vereiste maken** te sluiten.  

17. Klik op de pagina **vereisten** van de **wizard implementatie type maken**op **volgende**.  

18. Controleer op de pagina **Overzicht** van de **wizard Implementatietype maken**de acties die de wizard moet uitvoeren.  Klik indien nodig op **vorige** om terug te gaan en implementatie type-instellingen te wijzigen. Klik op **volgende** om het implementatie type te maken.  

19. Nadat de pagina **voortgang** is voltooid, controleert u de acties die zijn uitgevoerd en kiest u **sluiten** om de **wizard implementatie type maken**te volt ooien.  

20. Als u deze wizard hebt gestart vanuit de **wizard toepassing maken**, gaat u terug naar de pagina **implementatie typen** .  

###  <a name="deploy-the-mac-application"></a>De Mac-toepassing implementeren  
 De stappen voor het implementeren van een toepassing op Mac-computers zijn hetzelfde als de stappen voor het implementeren van een toepassing op Windows-computers, met uitzonde ring van de volgende verschillen:  

-   De implementatie van toepassingen aan gebruikers wordt niet ondersteund.  

-   Implementaties die het doel **Beschikbaar** hebben, worden niet ondersteund.  

-   De optie **software implementeren op het primaire apparaat** van de gebruiker op de pagina **implementatie-instellingen** van de **wizard software implementeren** wordt niet ondersteund.  

-   Omdat Mac-computers Software Center niet ondersteunen, wordt de instelling **gebruikers meldingen** instellen op de pagina **gebruikers ervaring** van de **wizard software implementeren** genegeerd.  

-   De optie om ontwaakpakketten te zenden wanneer u software implementeert, is niet ondersteund voor Mac-computers.  

> [!NOTE]  
>  U kunt een verzameling maken die alleen Mac-computers bevat. Als u dit wilt doen, maakt u een verzameling die gebruikmaakt van een query regel en gebruikt u het voor beeld WQL-query in het onderwerp [query's maken](../../core/servers/manage/create-queries.md) .  

 Zie [toepassingen implementeren](../../apps/deploy-use/deploy-applications.md)voor meer informatie.  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Stap 5: de implementatie van de Mac-toepassing bewaken  
 U kunt hetzelfde proces gebruiken voor het bewaken van toepassings implementaties op Mac-computers, zoals u wilt de implementaties van toepassingen op Windows-computers bewaken.  

 Zie [toepassingen bewaken](../deploy-use/monitor-applications-from-the-console.md)voor meer informatie.  

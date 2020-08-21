---
title: Windows to go implementeren
titleSuffix: Configuration Manager
description: Meer informatie over het inrichten van Windows to go in Configuration Manager om een Windows to go-werk ruimte te maken die wordt opgestart vanaf een extern station.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2861214bcdc9162b0121304b342d1d9d48be170
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697939"
---
# <a name="deploy-windows-to-go-with-configuration-manager"></a>Windows to go met Configuration Manager implementeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit onderwerp bevat de stappen voor het inrichten van Windows to go in Configuration Manager. Windows To Go is een ondernemingsfunctie van Windows 8, die het mogelijk maakt een Windows To Go-werkruimte te maken die kan worden opgestart vanaf een via een USB-verbinding aangesloten extern station op computers die voldoen aan de certificeringsvereisten van Windows 7 of Windows 8, ongeacht het besturingssysteem van de computer. Windows To Go-werkruimten kunnen dezelfde installatiekopie gebruiken die ondernemingen gebruiken voor hun desktops en laptops en kunnen op dezelfde wijze worden beheerd.  

 Zie [Windows to go Feature Overview](/previous-versions/windows/it-pro/windows-8.1-and-8/hh831833(v=ws.11))(Engelstalig) voor meer informatie over Windows to go.  

## <a name="provision-windows-to-go"></a>Inrichting Windows To Go  
 Windows To Go is een besturingssysteem dat is opgeslagen op een extern station dat is aangesloten via een USB-verbinding. U kunt het Windows To Go-station inrichten zoals u andere implementaties van het besturingssysteem inricht. Niettemin moet u een lichtjes andere benadering gebruiken om deze stations in te richten, omdat Windows To Go is ontwikkeld als een op de gebruiker gerichte, zeer mobiele oplossing.  

 Op een hoog niveau is Windows To Go een implementatie in twee fasen, waarin u het Windows To Go-apparaat kunt configureren en inhoud voorbereiden voor de implementatie van het besturingssysteem. U kunt dit doen met minimale gevolgen voor de gebruiker en uitval tijd beperken voor de computer van de gebruiker. Nadat u de computer hebt voorbereid, moet u het inrichtingsproces voltooien om te zorgen dat de computer klaar is voor de gebruiker. Het inrichtingsproces lijkt veel op het actuele implementatieproces van het besturingssysteem. Hieronder ziet u de algemene werkstroom voor de voorbereiding van de inhoud en inrichting van Windows To Go:  

1.  [Vereisten voor het inrichten van Windows to go](#BKMK_Prereqs)  

2.  [Voorbereide media maken](#BKMK_CreatePrestagedMedia)  

3.  [Een Windows To Go Creator-pakket maken](#BKMK_CreatePackage)  

4.  [De takenreeks bijwerken om BitLocker voor Windows To Go in te schakelen](#BKMK_UpdateTaskSequence)  

5.  [Het Windows to go Creator-pakket en de taken reeks implementeren](#BKMK_Deployments)  

6.  [De Windows to go Creator wordt uitgevoerd door de gebruiker](#BKMK_UserExperience)  

7.  [Configuration Manager configureert en faseert het Windows to go-station](#BKMK_ConfigureStageDrive)  

8.  [Gebruiker meldt zich aan bij Windows 8](#BKMK_UserLogsIn)  

###  <a name="prerequisites-to-provision-windows-to-go"></a><a name="BKMK_Prereqs"></a> Vereisten voor het inrichten van Windows To Go  
 Voordat u Windows to go inricht, moet u het volgende in Configuration Manager volt ooien:  

-   **Een opstartinstallatiekopie naar een distributiepunt distribueren**  

     Voordat u voorgefaseerde media maakt, moet u de opstartinstallatiekopie naar een distributiepunt distribueren.  

    > [!NOTE]  
    >  Opstart installatie kopieën worden gebruikt om het besturings systeem te installeren op de doel computers in uw Configuration Manager-omgeving. Ze bevatten een versie van Windows PE waarmee het besturingssysteem en eventuele benodigde apparaatstuurprogramma's worden geïnstalleerd. Configuration Manager biedt twee opstart installatie kopieën: één ter ondersteuning van x86-platformen en één ter ondersteuning van x64-platformen. U kunt ook uw eigen opstartinstallatiekopieën maken. Zie [opstart installatie kopieën beheren](../get-started/manage-boot-images.md)voor meer informatie.  

-   **De installatiekopie van het Windows 8-besturingssysteem naar een distributiepunt distribueren**  

     Voordat u voorgefaseerde media maakt, moet u de installatiekopie van het Windows 8-besturingssysteem naar een distributiepunt distribueren.  

    > [!NOTE]  
    >  Installatiekopieën van besturingssystemen zijn WIM-bestanden. Ze omvatten een gecomprimeerde verzameling referentiebestanden en -mappen die zijn vereist om een besturingssysteem correct te installeren en configureren op een computer. Zie [installatie kopieën van besturings systemen beheren](../get-started/manage-operating-system-images.md)voor meer informatie.  

-   **Takenreeks maken om Windows 8 te implementeren**  

     U moet een takenreeks maken voor een implementatie van Windows 8 waarnaar u verwijst bij het maken van voorgefaseerde media. Raadpleeg taken [reeksen beheren om taken te automatiseren](manage-task-sequences-to-automate-tasks.md)voor meer informatie.  

###  <a name="create-prestaged-media"></a><a name="BKMK_CreatePrestagedMedia"></a> Voor bereide media maken  
 Voorbereide media bevatten de opstartinstallatiekopie die wordt gebruikt voor het starten van de doelcomputer en de installatiekopie van het besturingssysteem die op de doelcomputer wordt toegepast. De computer die u inricht met voorgefaseerde media kan worden gestart met behulp van de opstartinstallatiekopie. De computer kan vervolgens een bestaande takenreeks voor implementatie van een besturingssysteem uitvoeren om een volledige implementatie van het besturingssysteem te installeren. De takenreeks waarmee het besturingssysteem wordt geïmplementeerd, staat niet op de media.  

 U kunt inhoud toevoegen, zoals toepassingen en stuurprogramma's, naast de installatiekopie en de opstartinstallatiekopie van het besturingssysteem tijdens de voorbereidende fase. Dit verkort de termijn die nodig is om een besturingssysteem te implementeren en vermindert het netwerkverkeer want de inhoud bevindt zich reeds in het station.  

 De volgende procedure gebruiken om de voorgefaseerde media te maken.  

#### <a name="to-create-prestaged-media"></a>Voorbereide media maken  

1. Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2. Vouw in de werkruimte **Softwarebibliotheek** de optie **Besturingssystemen**uit en klik vervolgens op **Takenreeksen**.  

3. Klik op het tabblad **Start** in de groep **Maken** op **Takenreeksmedia maken** om de wizard Takenreeksmedia maken te starten.  

4. Geef op de pagina **Mediatype selecteren** de volgende informatie op en klik op **Volgende**.  

   -   Selecteer **Voorbereide media**.  

   -   Selecteer **Implementatie van besturingssysteem zonder toezicht toestaan** om de implementatie van Windows To Go gebruikersinteractie op te starten.  

       > [!IMPORTANT]  
       >  Als u deze optie gebruikt met SMSTSPreferredAdvertID aangepaste variabele (later in dit proces instellen), is geen gebruikersinteractie vereist en zal de computer automatisch opstarten naar de implementatie van Windows To Go wanneer deze een Windows To Go-station detecteert. De gebruiker wordt nog steeds gevraagd om een wachtwoord als de media hiervoor is geconfigureerd. Als u de instelling **Implementatie van besturingssysteem zonder toezicht toestaan** gebruikt zonder de variabele SMSTSPreferredAdvertID te configureren, treedt een fout op wanneer u de takenreeks implementeert.  

5. Geef op de pagina **Mediabeheer** de volgende informatie op en klik op **Volgende**.  

   -   Selecteer **Dynamische media** als u wilt toestaan dat een beheerpunt media omleidt naar een ander beheerpunt op basis van de clientlocatie binnen de sitegrenzen.  

   -   Selecteer **Op site gebaseerde media** als u wilt dat de media alleen contact maken met het opgegeven beheerpunt.  

6. Geef op de pagina **Media-eigenschappen**  de volgende informatie op en klik vervolgens op **Volgende**.  

   -   **Gemaakt door**: opgeven wie het medium heeft gemaakt.  

   -   **Versie**: het versienummer van het medium opgeven.  

   -   **Opmerking**: hier kunt u met een unieke beschrijving aangeven waarvoor het medium wordt gebruikt.  

   -   **Mediabestand**: de naam en het pad van de uitvoerbestanden opgeven. De wizard schrijft de uitvoerbestanden naar deze locatie. Bijvoorbeeld: ** \\ \servername\folder\outputfile.Wim**  

7. Geef op de pagina **Beveiliging** de volgende informatie op en klik vervolgens op **Volgende**.  

   -   Selecteer **ondersteuning van onbekende computers inschakelen** zodat de media een besturings systeem kan implementeren op een computer die niet wordt beheerd door Configuration Manager. Er is geen record van deze computers in de Configuration Manager-Data Base. Onbekende computers omvatten het volgende:  

       -   Een computer waarop de Configuration Manager-client niet is geïnstalleerd  

       -   Een computer die niet is geïmporteerd in Configuration Manager  

       -   Een computer die niet is gedetecteerd door Configuration Manager  

   -   Selecteer **De media beveiligen met een wachtwoord** en voer een sterk wachtwoord in om de media te beveiligen tegen onbevoegde toegang. Wanneer u een wachtwoord opgeeft, moet de gebruiker dat wachtwoord leveren om de voorbereide media te gebruiken.  

       > [!IMPORTANT]  
       >  Wijs, als een beste praktijk op vlak van beveiliging, altijd een wachtwoord toe om te helpen de vooraf geplaatste media te beschermen.  

       > [!NOTE]  
       >  Wanneer u de voorgefaseerde media beveiligt met een wachtwoord, wordt de gebruiker om het wachtwoord verzocht zelfs wanneer de media is geconfigureerd met de instelling **Implementatie van besturingssysteem zonder toezicht toestaan** .  

   -   Selecteer **Zelfondertekend certificaat maken**voor HTTP-communicatie en geef vervolgens de begin- en verloopdatum voor het certificaat op.  

   -   Selecteer **PKI-certificaat importeren**voor HTTPS-communicatie en geef vervolgens het certificaat op dat moet worden geïmporteerd met het bijbehorende wachtwoord.  

        Zie [PKI-certificaat vereisten](../../core/plan-design/network/pki-certificate-requirements.md)voor meer informatie over dit client certificaat dat wordt gebruikt voor opstart installatie kopieën.  

   -   **Affiniteit**Configuration Manager van gebruiker met apparaat: Geef op hoe u wilt dat de media gebruikers aan de doel computer koppelen. Zie [gebruikers koppelen aan een doel computer](../get-started/associate-users-with-a-destination-computer.md)voor meer informatie over hoe de besturingssysteem implementatie de gebruikers affiniteit van het apparaat ondersteunt.  

       -   Stel **Affiniteit tussen gebruikers en apparaten toestaan met automatische goedkeuring** in als u wilt dat de media gebruikers automatisch koppelen aan de doelcomputer. Deze functionaliteit is gebaseerd op de acties van de takenreeks waardoor het besturingssysteem wordt geïmplementeerd. In dit scenario brengt de takenreeks een relatie tot stand tussen de opgegeven gebruikers en de doelcomputer wanneer deze het besturingssysteem op de doelcomputer implementeert.  

       -   Stel **Affiniteit tussen gebruikers en apparaten toestaan in afwachting van goedkeuring door beheerder** in als u wilt dat de media gebruikers aan de doelcomputer koppelen nadat er goedkeuring is verleend. Deze functionaliteit is gebaseerd op het bereik van de takenreeks waardoor het besturingssysteem wordt geïmplementeerd. In dit scenario brengt de takenreeks een relatie tot stand tussen de opgegeven gebruikers en de doelcomputer, maar wordt er gewacht op goedkeuring van een gebruiker met beheerderrechten voordat het besturingssysteem wordt geïmplementeerd.  

       -   Stel **Geen affiniteit tussen gebruikers en apparaten toestaan** in als niet wilt dat de media gebruikers aan de doelcomputer koppelen. In dit scenario koppelt de takenreeks geen gebruikers aan de doelcomputer wanneer dit het besturingssysteem implementeert.  

8. Op de pagina **Takenreeks** de takenreeks van Windows 8 opgeven die u in de voorgaande sectie hebt gemaakt.  

9. Geef op de pagina **Opstartinstallatiekopie** de volgende informatie op en klik vervolgens op **Volgende**.  

    > [!IMPORTANT]  
    >  De architectuur van de opstartinstallatiekopie die wordt gedistribueerd moet toepasselijk zijn voor de architectuur van de doelcomputer. Op een x64-doelcomputer kan een x86- of x64-opstartinstallatiekopie worden opgestart en uitgevoerd. Op een x86-doelcomputer kan echter alleen een x86-opstartinstallatiekopie worden opgestart en uitgevoerd. Voor Windows 8-gecertificeerde computers in EFI-modus, moet u een x64 opstartinstallatiekopie gebruiken.  

    -   **Opstartinstallatiekopie**: de opstartinstallatiekopie voor het starten van de doelcomputer opgeven.  

    -   **Distributiepunt**: het distributiepunt opgeven dat als host fungeert voor de opstartinstallatiekopie. De wizard haalt de opstartinstallatiekopie op van het distributiepunt en schrijft deze naar de media.  

        > [!NOTE]  
        >  De gebruiker met beheerdersrechten moet **Leesrechten** hebben tot de inhoud van de opstartinstallatiekopie op het distributiepunt. Zie [pakket toegangs account](../../core/plan-design/hierarchy/accounts.md#package-access-account)voor meer informatie.  

    -   Als u **Op site gebaseerde media** selecteerde op de pagina **Mediabeheer** van deze wizard, geeft u in het venster **Beheerpunt** een beheerpunt op van een primaire site.  

    -   Als u **Dynamische media** selecteerde op de pagina **Mediabeheer** van de wizard, geeft u in het venster **Gekoppelde beheerpunten** de te gebruiken beheerpunten van de primaire site op en een volgorde van prioriteit voor de eerste communicaties.  

10. Geef op de pagina **Installatiekopieën** de volgende informatie op en klik vervolgens op **Volgende**.  

    -   **Installatiekopiepakket**: het pakket met de installatiekopie van het besturingssysteem Windows 8 opgeven.  

    -   **Installatiekopie-index**: de te implementeren installatiekopie opgeven als het pakket meerdere installatiekopieën van besturingssystemen bevat.  

    -   **Distributiepunt**: het distributiepunt opgeven dat het pakket met de installatiekopie van het besturingssysteem host. De wizard haalt de opstartinstallatiekopie van het besturingssysteem op van het distributiepunt en schrijft deze naar de media.  

        > [!NOTE]  
        >  De gebruiker met beheerdersrechten moet **Leesrechten** hebben tot de inhoud van de installatiekopie van het besturingssysteem op het distributiepunt. Zie [pakket toegangs account](../../core/plan-design/hierarchy/accounts.md#package-access-account)voor meer informatie.  

11. Op de pagina **Toepassing selecteren** de toepassingsinhoud opgeven voor opname in het mediabestand en klikken op **Volgende**.  

12. Op de pagina **Pakket selecteren** de aanvullende pakketinhoud opgeven voor opname in het mediabestand en klikken op **Volgende**.  

13. Op de pagina **Stuurprogrammapakket selecteren** de stuurprogramma-inhoud opgeven voor opname in het mediabestand en klikken op **Volgende**.  

14. Selecteer, op de pagina **Distributiepunten** , een of meer distributiepunten die de inhoud bevatten die vereist is door de takenreeks, en klik vervolgens op **Volgende**.  

15. Geef op de pagina **Aanpassing** de volgende informatie op en klik vervolgens op **Volgende**.  

    - **Variabelen**: geef de variabelen op die de takenreeks gebruikt om het besturingssysteem te implementeren. Gebruik voor Windows To Go, de variabele SMSTSPreferredAdvertID om automatisch de implementatie van Windows To Go te selecteren met behulp van de volgende indeling:  

       SMSTSPreferredAdvertID = {*DeploymentID*}, waarbij DeploymentID de implementatie-id is die gekoppeld is aan de takenreeks die u gebruikt om het inrichtingsproces voor het Windows To Go-station te voltooien.  

      > [!TIP]  
      >  Als u deze variabele gebruikt met de takenreeks die ingesteld is om zonder toezicht te worden uitgevoerd (voorheen in dit proces ingesteld), is geen gebruikersinteractie vereist en start de computer automatisch op naar de implementatie van Windows To Go wanneer deze een Windows To Go-station detecteert. De gebruiker wordt nog steeds gevraagd om een wachtwoord als de media hiervoor is geconfigureerd.  

    - **Prestart-opdrachten**: geef eventuele prestart-opdrachten op die u wilt uitvoeren voordat de takenreeks wordt uitgevoerd. Prestart-opdrachten kunnen bestaan uit een script of een uitvoerbaar bestand dat kan communiceren met de gebruiker in Windows PE voordat de takenreeks wordt uitgevoerd om het besturingssysteem te installeren. Het volgende voor de implementatie van Windows To Go configureren:  

      - **OSDBitLockerPIN**: BitLocker voor Windows To Go vereist een wachtwoordzin. De variabele **OSDBitLockerPIN** instellen als onderdeel van een prestart-opdracht om de BitLocker-wachtwoordzin voor het Windows To Go-station in te stellen.  

        > [!WARNING]  
        >  Nadat BitLocker is ingeschakeld voor de wachtwoordzin, moet de gebruiker de wachtwoordzin invoeren telkens wanneer de computer opstart naar het Windows To Go-station.  

      - **SMSTSUDAUsers**: geeft de primaire gebruiker van de doelcomputer op. Gebruik deze variabele om de gebruikersnaam in te zamelen, die vervolgens kan worden gebruikt om de gebruiker te koppelen aan het apparaat. Zie [gebruikers koppelen aan een doel computer](../get-started/associate-users-with-a-destination-computer.md)voor meer informatie.  

        > [!TIP]  
        >  Om de gebruikersnaam op te halen, kunt u een invoervak maken als onderdeel van de prestart-opdracht, laat u de gebruiker zijn gebruikersnaam invoeren en stelt vervolgens de variabele met de waarde in. U kunt bijvoorbeeld de volgende regels toevoegen aan het scriptbestand van de prestart-opdracht:  
        >   
        >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
        >   
        >  `env("SMSTSUDAUsers") = UserID`  

        Zie [prestart-opdrachten voor taken reeks media](../understand/prestart-commands-for-task-sequence-media.md)voor meer informatie over het maken van een script bestand om te gebruiken als uw prestart-opdracht.  

16. Voltooi de wizard.  

    > [!NOTE]  
    >  De wizard kan er lang over doen om het voorgefaseerde mediabestand te voltooien.  

###  <a name="create-a-windows-to-go-creator-package"></a><a name="BKMK_CreatePackage"></a> Een Windows to go Creator-pakket maken  
 Als onderdeel van de implementatie van Windows To Go, moet u een pakket maken om het voorgefaseerde mediabestand te implementeren. Het pakket moet het hulpprogramma bevatten dat het Windows To Go-station configureert en de voorgefaseerde media naar het station uitvoert. Gebruik de volgende procedure om het Windows To Go Creator-pakket te maken.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>Het Windows To Go Creator-pakket maken  

1. Maak op de server om de Windows To Go Creator pakketbestanden te hosten, een bronmap voor de pakketbronbestanden.  

   > [!NOTE]  
   >  Het computeraccount van de siteserver moet **Leesrechten** voor de bronmap hebben.  

2. Kopieer het voorgefaseerde mediabestand dat u maakte in de sectie [Create prestaged media](#BKMK_CreatePrestagedMedia) naar de pakketbronmap.  

3. Kopieer het hulpprogramma van Windows To Go Creator (WTGCreator.exe) naar de pakketbronmap. Het hulp programma Creator is beschikbaar op elke primaire site server op de volgende locatie: <*ConfigMgrInstallationFolder*> \osd\tools\wtg\creator.  

4. Maak een pakket en programma met behulp van de wizard Pakket en Programma maken.  

5. Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

6. Vouw **Toepassingsbeheer** uit in de werkruimte **Softwarebibliotheek**en klik vervolgens op **pakketten**.  

7. Klik op **Pakket maken** in het tabblad **Start** in de groep **Maken**.  

8. Geef op de pagina **Pakket** de naam en beschrijving van het pakket. Voer bijvoorbeeld **Windows to go** in voor de naam van het pakket en geef **pakket op om een Windows to go-station te configureren met behulp van Configuration Manager** voor de pakket beschrijving.  

9. Selecteer **Dit pakket bevat bronbestanden**, geef het pad op naar de pakketbronmap die u maakte in stap 1 en klik vervolgens op **Next**.  

10. Op de pagina **Programmatype** selecteert u **Standaardprogramma**, en klikt u dan op **Volgende**.  

11. Op de pagina **Standaardprogramma** het volgende opgeven:  

    -   **Naam**: de naam van het programma opgeven. Typ bijvoorbeeld **Creator** voor de programmanaam.  

    -   **Opdrachtregel**: typ **WTGCreator.exe /wim:PrestageName.wim**, waarbij PrestageName de naam is van het voorgefaseerde bestand dat u maakte en kopieerde naar de pakketbronmap voor het Windows To Go Creator-pakket.  

         Eventueel kunt u de volgende opties toevoegen:  

        -   **enableBootRedirect**: opdrachtregeloptie om de opstartopties van Windows To Go te wijzigen en een omleiding voor opstarten toe te staan. Als u deze optie gebruikt, zal de computer opstarten vanuit USB zonder dat wijziging van de opstartvolgorde van de computer firmware vereist is of de gebruiker moet worden geselecteerd uit een lijst met opstartopties bij het opstarten. Als een Windows To Go-station is gedetecteerd, start de computer op naar dit station.  

    -   **Uitvoeren**: geef **Normaal** op om het programma uit te voeren dat is gebaseerd op het systeem en standaardprogramma.  

    -   **Het programma kan worden uitgevoerd**: geef op of het programma enkel kan worden uitgevoerd als de gebruiker is aangemeld.  

    -   **Uitvoeringsmodus**: geef op of het programma zal worden uitgevoerd met aangemelde gebruikersmachtigingen of met beheerdersmachtigingen. Verhoogde machtigingen zijn vereist om Windows To Go Creator uit te voeren.  

    -   Selecteer **Gebruikers toestaan de programma-installatie te bekijken en interacties uit te voeren**en klik vervolgens op **Volgende**.  

12. Op de pagina Vereisten het volgende opgeven:  

    - **Platformvereisten**: selecteer de toepasselijke Windows 8-platformen om inrichting toe te staan.  

    - **Geschatte schijfruimte**: specificeer de grootte van de pakketbronmap voor de Windows To Go Creator.  

    - **Maximale toegestane uitvoeringstijd (minuten)**: geef de verwachte maximale duur op voor het uitvoeren van het programma op de clientcomputer. Deze waarde is standaard ingesteld op 120 minuten.  

      > [!IMPORTANT]  
      >  Als u onderhoudsvensters gebruikt voor de verzameling waarop dit programma wordt uitgevoerd, kan er een conflict optreden als de **Maximum toegestane uitvoeringstijd** langer is dan het geplande onderhoudsvenster. Als de maximum uitvoeringstijd is ingesteld op **Onbekend**, zal het starten tijdens het onderhoudsvenster, maar zal het verder worden uitgevoerd tot het voltooid of mislukt is nadat het onderhoudsvenster is gesloten. Als u de maximum uitvoeringstijd instelt op een specifieke periode (niet ingesteld op Onbekend) die langer is dan de lengte van enig beschikbaar onderhoudsvenster, zal het programma niet worden uitgevoerd.  

      > [!NOTE]  
      >  Als de waarde is ingesteld op **onbekend**, stelt Configuration Manager de Maxi maal toegestane uitvoerings tijd in op 12 uur (720 minuten).  

      > [!NOTE]  
      >  Als de maximale uitvoerings tijd (hetzij ingesteld door de gebruiker hetzij als de standaard waarde) wordt overschreden, Configuration Manager het programma wordt gestopt als **uitvoeren met beheerders rechten** is geselecteerd en **toestaan dat gebruikers de programma-installatie kunnen zien en gebruiken** niet is geselecteerd op de pagina **standaard programma** .  

      Klik op **Volgende** en voltooi de wizard.  

###  <a name="update-the-task-sequence-to-enable-bitlocker-for-windows-to-go"></a><a name="BKMK_UpdateTaskSequence"></a> De taken reeks bijwerken om BitLocker voor Windows to go in te scha kelen  
 Windows To Go schakelt BitLocker in op een extern opstartbaar station zonder het gebruik van TPM. Daarom moet u een afzonderlijk hulpprogramma gebruiken om BitLocker op het Windows To Go-station te configureren. Om BitLocker in te schakelen, moet u een actie toevoegen aan de takenreeks na de stap **Windows en ConfigMgr installeren** .  

> [!NOTE]  
>  BitLocker voor Windows To Go vereist een wachtwoordzin. In de stap [Create prestaged media](#BKMK_CreatePrestagedMedia) stelt u de wachtwoordzin in als deel van een prestart-opdracht door de OSDBitLockerPIN-variabele te gebruiken.  

 Gebruik de volgende procedure om de Windows 8-takenreeks bij te werken om BitLocker voor Windows To Go in te schakelen.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>Bijwerken van de Windows 8-takenreeks om BitLocker in te schakelen  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Vouw **Toepassingsbeheer** uit in de werkruimte **Softwarebibliotheek**en klik vervolgens op **pakketten**.  

3.  Klik op **Pakket maken** in het tabblad **Start** in de groep **Maken**.  

4.  Geef op de pagina **Pakket** de naam en beschrijving van het pakket. Typ voor de pakketnaam bijvoorbeeld **BitLocker for Windows To Go** en geef voor de pakketbeschrijving **Package to update BitLocker for Windows To Go** op.  

5.  Selecteer **Dit pakket bevat bronbestanden**, specificeer de locatie voor het BitLocker-hulpprogramma voor Windows To Go, en klik vervolgens op **Volgende**. Het hulp programma BitLocker is beschikbaar op elke Configuration Manager primaire site server op de volgende locatie: <*ConfigMgrInstallationFolder*> \osd\tools\wtg\bitlocker\  

6.  Selecteer op de pagina **Programmatype****Geen programma maken**.  

7.  Klik op **Volgende** en voltooi de wizard.  

8.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

9. Vouw in de werkruimte **Softwarebibliotheek** de optie **Besturingssystemen**uit en klik vervolgens op **Takenreeksen**.  

10. Selecteer de Windows 8-takenreeks waarnaar u verwijst in de voorgefaseerde media.  

11. Klik in het tabblad **Start** in de groep **Takenreeks** op **Bewerken**.  

12. Klik op de stap **Windows en ConfigMgr installeren** , klik op **Toevoegen**, klik op **Algemeen**, en klik vervolgens op **Opdrachtregel uitvoeren**. De stap Opdrachtregel uitvoeren wordt toegevoegd na de stap Windows en ConfigMgr installeren.  

13. Voeg op het tabblad **Eigenschappen** voor de stap **Opdrachtregel uitvoeren** het volgende toe:  

    1.  **Naam**: geef een naam voor de opdrachtregel op, bijvoorbeeld **Enable BitLocker for Windows To Go**.  

    2.  **Opdracht regel**: i386\osdbitlocker_wtg.exe/Enable/pwd: < *geen&#124;AD*>  

         Parameters:  

        -   /PWD: <geen&#124;AD->: Geef de BitLocker-wachtwoord herstel modus op. Deze parameter is vereist als u de parameter /Enable in de opdrachtregel gebruikt.  

             Selecteer **AD** om BitLocker-stationsversleuteling te configureren om een back-up te maken van herstelinformatie voor door BitLocker beschermde stations naar Active Directory Domain Services (AD DS). Het maken van een back-up van herstelwachtwoorden voor een door BitLocker beschermd station laat beheerders toe het station te herstellen als het vergrendeld is. Dit zorgt ervoor dat versleutelde gegevens die behoren tot de onderneming, altijd kunnen worden geopend door geautoriseerde gebruikers. Wanneer u **Geen**specificeert, is de gebruiker verantwoordelijk voor het bewaren van een kopie van het herstelwachtwoord of de herstelsleutel. Als de gebruiker die informatie verliest of negeert om het station te ontsleutelen voordat hij de organisatie verlaat, kunnen beheerders niet gemakkelijk toegang krijgen tot het station.  

        -   /wait: <TRUE&#124;FALSE>: Geef op of de taken reeks wacht tot de versleuteling is voltooid voordat deze is voltooid.  

    3.  Selecteer **Pakket**, en geef dan het pakket dat u aan het begin van deze procedure hebt gemaakt.  

    4.  Specificeer op het tabblad **Opties** de volgende condities:  

        -   Conditie = Takenreeksvariabele  

        -   Variabele = _SMSTSWTG  

        -   Conditie = is gelijk aan  

        -   Waarde = True  

    > [!NOTE]  
    >  De stap **BitLocker inschakelen** , die waarschijnlijk is na de nieuwe opdrachtregelstap, wordt niet gebruikt om BitLocker voor Windows To Go in te schakelen. U kunt deze stap echter in de takenreeks houden om te gebruiken voor Windows 8-implementaties die geen Windows To Go-station gebruiken.  

###  <a name="deploy-the-windows-to-go-creator-package-and-task-sequence"></a><a name="BKMK_Deployments"></a> Het Windows To Go Creator-pakket en de takenreeks implementeren  
 Windows To Go is een proces voor hybride implementatie. Daarom moet u het Windows To Go Creator-pakket en de Windows 8-takenreeks implementeren. Gebruik de volgende procedures om de implementatieproces te voltooien.  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>Het Windows To Go Creator-pakket implementeren  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Vouw **Toepassingsbeheer** uit in de werkruimte **Softwarebibliotheek**en klik vervolgens op **pakketten**.  

3.  Selecteer het Windows To Go-pakket dat u in de stap [Een Windows To Go Creator-pakket maken](#BKMK_CreatePackage) hebt gemaakt.  

4.  Klik op het tabblad **Start** in de groep **Implementatie** op **Implementeren**.  

5.  Geef op het tabblad **Algemeen** de volgende instellingen op:  

    1.  **Software**: controleer of het pakket voor Windows To Go is geselecteerd.  

    2.  **Verzameling**: klik op **Bladeren** om de verzameling te selecteren waarop u het pakket voor Windows To Go wilt implementeren.  

    3.  **Standaarddistributiepuntengroepen gebruiken die aan deze verzameling zijn gekoppeld**: selecteer deze optie als u de pakketinhoud wilt opslaan op de standaarddistributiepuntengroep van de verzameling. Als u de geselecteerde verzameling niet hebt gekoppeld aan een distributiepuntgroep, wordt deze optie onbeschikbaar.  

6.  Klik op de pagina **Inhoud** op **Toevoegen** en selecteer vervolgens de distributiepunten of distributiepuntgroepen waarop u de inhoud wilt implementeren die is gekoppeld met dit pakket en programma.  

7.  Op de pagina **Implementatie-instellingen** selecteert u **Beschikbaar** voor het implementatietype, en klikt u vervolgens op **Volgende**.  

8.  Configureer op de **Planning**wanneer dit pakket en programma zullen worden geïmplementeerd of beschikbaar zullen worden gemaakt voor clientapparaten.  

     De opties op deze pagina zullen verschillen afhankelijk van of de implementatieactie ingesteld is op **Beschikbaar** of **Vereist**.  

9. Configureer op de pagina **Planning**de volgende instellingen en klik vervolgens op **Volgende**.  

    1.  **Plannen wanneer deze implementatie beschikbaar wordt**: geef de datum en tijd wanneer het pakket en programma beschikbaar zijn om te worden uitgevoerd op de doelcomputer. Wanneer u **UTC**selecteert, zorgt deze instelling ervoor dat het pakket en programma beschikbaar zijn voor meerdere doelcomputers tegelijkertijd eerder dan op verschillende tijdstippen, volgens de lokale tijd op de doelcomputers.  

    2.  **Plannen wanneer deze implementatie zal verlopen**: geef de datum en tijd wanneer het pakket en programma verlopen op de doelcomputer. Wanneer u **UTC**selecteert, zorgt deze instelling ervoor dat de takenreeks verloopt op meerdere doelcomputers tegelijkertijd eerder dan op verschillende tijdstippen, volgens de lokale tijd op de doelcomputers.  

10. Geef op de pagina **Gebruikerservaring** van de wizard de volgende informatie:  

    -   **Software-installatie**: hierdoor kan de software worden geïnstalleerd buiten de geconfigureerde onderhoudsvensters.  

    -   **Systeem opnieuw opstarten (indien dit is vereist om de installatie te voltooien)**: een apparaat kan opnieuw worden opgestart buiten de geconfigureerde onderhoudsvensters wanneer de software-installatie dit vereist.  

    -   **Embedded-apparaten**:  wanneer u pakketten en programma's implementeert naar Windows Embedded-apparaten waarvan het schrijffilter is ingeschakeld, kunt u aangeven dat de pakketten en programma's op de tijdelijke overlay moeten worden geïnstalleerd en dat de wijzigingen later worden aangebracht of dat de wijzigingen moeten worden aangebracht tegen de deadline van de installatie of tijdens een onderhoudsvenster. Wanneer u wijzigingen doorvoert tegen de installatiedeadline of tijdens een onderhoudsvenster, moet er opnieuw worden opgestart, zodat de wijzigingen behouden blijven op het apparaat.  

11. Geef op de pagina **Distributiepunten** de volgende informatie:  

    -   **Implementatieopties** : geef **Inhoud downloaden vanaf een extern distributiepunt en lokaal uitvoeren**op.  

    -   **Clients toestaan inhoud te delen met andere clients binnen hetzelfde subnet**: selecteer deze optie om de belasting op het netwerk te verminderen door clients toe te laten inhoud te downloaden van andere clients op het netwerk die reeds inhoud hebben gedownload en gecached. Deze optie gebruikt Windows BranchCache en kan worden gebruikt op computers die Windows Vista SP2 en recenter uitvoeren.  

    -   **Clients toestaan een terugvalbronlocatie voor inhoud te gebruiken**: specificeer of clients toegestaan zijn terug te vallen en een niet-voorkeursdistributiepunt te gebruiken als de bronlocatie voor inhoud wanneer de inhoud niet beschikbaar is op een voorkeursdistributiepunt.  

12. Voltooi de wizard.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>De Windows 8-takenreeks implementeren  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Vouw in de werkruimte **Softwarebibliotheek** de optie **Besturingssystemen**uit en klik vervolgens op **Takenreeksen**.  

3.  Selecteer de Windows 8-takenreeks die in u stap [Prerequisites to provision Windows To Go](#BKMK_Prereqs) hebt gemaakt.  

4.  Klik op het tabblad **Start** in de groep **Implementatie** op **Implementeren**.  

5.  Geef op het tabblad **Algemeen** de volgende instellingen op:  

    1.  **Takenreeks**: controleer of de Windows 8-takenreeks is geselecteerd.  

    2.  **Verzameling**: klik op **Bladeren** om de verzameling te selecteren die alle apparaten bevat waarvoor een gebruiker Windows To Go kan inrichten.  

        > [!IMPORTANT]  
        >  Als de voorgefaseerde media die u in de sectie [Create prestaged media](#BKMK_CreatePrestagedMedia) hebt gemaakt, gebruik maakt van de SMSTSPreferredAdvertID-variabele, kunt u de takenreeks implementeren op de verzameling **Alle systemen** en kunt u de instelling **Alleen Windows PE (verborgen)** op de pagina **Inhoud** specificeren. Omdat de takenreeks verborgen is, zal ze enkel beschikbaar zijn voor media.  

    3.  **Standaarddistributiepuntengroepen gebruiken die aan deze verzameling zijn gekoppeld**: selecteer deze optie als u de pakketinhoud wilt opslaan op de standaarddistributiepuntengroep van de verzameling. Als u de geselecteerde verzameling niet hebt gekoppeld aan een distributiepuntgroep, wordt deze optie onbeschikbaar.  

6.  Configureer op de pagina **Implementatie-instellingen** de volgende instellingen en klik vervolgens op **Volgende**.  

    -   **Doel**: selecteer **Beschikbaar**. Wanneer u de takenreeks op een gebruiker implementeert, ziet de gebruiker de gepubliceerde takenreeks in de Application Catalog en kan hij deze op aanvraag opvragen. Wanneer u de takenreeks op een apparaat implementeert, ziet de gebruiker de takenreeks in Software Center en kan hij deze op aanvraag installeren.  

    -   **Beschikbaar maken voor de volgende**: Geef op of de taken reeks beschikbaar is voor Configuration Manager-clients, media of PXE.  

        > [!IMPORTANT]  
        >  Gebruik de instelling **Alleen media en PXE (verborgen)** voor geautomatiseerde implementaties van takenreeksen. Selecteer **Implementatie van besturingssysteem zonder toezicht toestaan** en stel de SMSTSPreferredAdvertID-variabele in als deel van de voorgefaseerde media om de computer automatisch te laten opstarten naar de Windows To Go-implementatie zonder gebruikersinteractie wanneer het een Windows To Go-station detecteert. Voor meer informatie over deze voorgefaseerde media-instellingen, zie de sectie [Create prestaged media](#BKMK_CreatePrestagedMedia) .  

7.  Configureer op de pagina **Planning** de volgende instellingen en klik vervolgens op **Volgende**.  

    1.  **Plannen wanneer deze implementatie beschikbaar wordt**: geef de datum en tijd wanneer de takenreeks beschikbaar is om te worden uitgevoerd op de doelcomputer. Wanneer u **UTC**selecteert, zorgt deze instelling ervoor dat de takenreeks toegankelijk is voor meerdere doelcomputers tegelijkertijd eerder dan op verschillende tijdstippen, volgens de lokale tijd op de doelcomputers.  

    2.  **Plannen wanneer deze implementatie zal verlopen**: geef de datum en tijd wanneer de takenreeks op de doelcomputer verloopt. Wanneer u **UTC**selecteert, zorgt deze instelling ervoor dat de takenreeks verloopt op meerdere doelcomputers tegelijkertijd eerder dan op verschillende tijdstippen, volgens de lokale tijd op de doelcomputers.  

8.  Geef op de pagina **Gebruikerservaring** de volgende informatie:  

    -   **Voortgang van taken reeks weer geven**: Geef op of de Configuration Manager-client de voortgang van de taken reeks weergeeft.  

    -   **Software-installatie**: specificeer of de gebruiker software mag installeren buiten een geconfigureerd onderhoudsvenster na de geplande tijd.  

    -   **Systeem opnieuw opstarten (indien dit is vereist om de installatie te voltooien)**: een apparaat kan opnieuw worden opgestart buiten de geconfigureerde onderhoudsvensters wanneer de software-installatie dit vereist.  

    -   **Embedded-apparaten**:  wanneer u pakketten en programma's implementeert naar Windows Embedded-apparaten waarvan het schrijffilter is ingeschakeld, kunt u aangeven dat de pakketten en programma's op de tijdelijke overlay moeten worden geïnstalleerd en dat de wijzigingen later worden aangebracht of dat de wijzigingen moeten worden aangebracht tegen de deadline van de installatie of tijdens een onderhoudsvenster. Wanneer u wijzigingen doorvoert tegen de installatiedeadline of tijdens een onderhoudsvenster, moet er opnieuw worden opgestart, zodat de wijzigingen behouden blijven op het apparaat.  

    -   **Op internet gebaseerde clients**: specificeer of de takenreeks mag worden uitgevoerd op een client met internet. Bewerkingen waarbij er software wordt geïnstalleerd, zoals een besturingssysteem, worden bij het gebruik van deze instelling niet ondersteund. Gebruik deze optie alleen voor algemene op scripts gebaseerde takenreeksen die bewerkingen uitvoeren onder het standaardbesturingssysteem.  

9. Geef op de pagina **Waarschuwingen** de waarschuwingsinstelling die u wilt voor de implementatie van deze takenreeks en klik vervolgens op **Volgende**.  

10. Geef op de pagina **Distributiepunten** de volgende informatie op en klik vervolgens op **Volgende**.  

    -   **Implementatieopties**: selecteer **De inhoud lokaal downloaden wanneer deze nodig is voor de takenreeks die wordt uitgevoerd**.  

    -   **Extern distributiepunt gebruiken wanneer geen lokaal distributiepunt beschikbaar is**: specificeer of clients distributiepunten kunnen gebruiken die zich op trage en onbetrouwbare netwerken bevinden zitten om de inhoud te downloaden die vereist is door de takenreeks.  

    -   **Clients toestaan een terugval bron locatie voor inhoud te gebruiken**:
        - *Vóór versie 1610*kunt u het selectie vakje terugval bron locatie voor inhoud toestaan selecteren om clients buiten deze grens groepen toe te staan om terug te vallen en het distributie punt te gebruiken als bron locatie voor inhoud wanneer er geen andere distributie punten beschikbaar zijn.
        - *Vanaf versie 1610*kunt u de **bron locatie voor het toestaan van terugval**niet meer configureren voor inhoud.  In plaats daarvan configureert u relaties tussen grens groepen die bepalen wanneer een client kan beginnen met zoeken naar extra grens groepen voor een geldige locatie van de inhouds bron. 

11. Voltooi de wizard.  

###  <a name="user-runs-the-windows-to-go-creator"></a><a name="BKMK_UserExperience"></a> Windows To Go Creator wordt uitgevoerd door de gebruiker  
 Nadat u het Windows To Go-pakket en de Window 8-takenreeks hebt geïmplementeerd, is Windows To Go Creator toegankelijk voor de gebruiker. De gebruiker kan naar de softwarecatalogus gaan, of Software Center als de Windows To Go Creator werd geïmplementeerd op apparaten, en hij kan het Windows To Go Creator-programma uitvoeren. Zodra het creator-pakket is gedownload, verschijnt een knipperend pictogram op de taakbalk. Wanneer de gebruiker op het pictogram klikt, wordt een dialoogvenster getoond aan de gebruiker om het Windows To Go-station te selecteren om in te richten (tenzij de /drive-opdrachtregeloptie wordt gebruikt). Als het station niet voldoet aan de vereisten voor windows To Go of als het station onvoldoende vrij schrijfruimte heeft om de installatiekopie te installeren, toont het creator-programma een foutboodschap. De gebruiker kan het station en de installatiekopie controleren die vanop de bevestigingspagina zullen worden toegepast. Terwijl de creator inhoud naar het Windows To Go-station configureert en voorbereidt, wordt het vooruitgangsdialoogvenster getoond. Nadat de voorbereiding voltooid is, toont de creator een prompt om de computer opnieuw op te starten om te starten naar het Windows To Go-station.  

> [!NOTE]  
>  Als u opstartomleiding niet hebt ingeschakeld als deel van de opdrachtregel voor het creator-programma in de sectie [Create a Windows To Go Creator package](#BKMK_CreatePackage) , kan de gebruiker verplicht zijn handmatig op te starten naar het Windows To Go-station telkens het systeem opnieuw opstart.  

###  <a name="configuration-manager-configures-and-stages-the-windows-to-go-drive"></a><a name="BKMK_ConfigureStageDrive"></a> Het Windows To Go-station wordt geconfigureerd en voorbereid door Configuration Manager  
 Nadat de computer opnieuw opgestart is naar het Windows To Go-station, zal het station opstarten naar Windows PE en een verbinding maken met het beheerpunt om het beleid te krijgen om de implementatie van het besturingssysteem te voltooien. Configuration Manager configureert en faseert het station. Nadat Configuration Manager het station heeft uitgevoerd, kan de gebruiker de computer opnieuw opstarten om het inrichtings proces te volt ooien (zoals het toevoegen aan een domein of het installeren van apps). Dit proces is hetzelfde voor alle voorgefaseerde media.  

###  <a name="user-logs-in-to-windows-8"></a><a name="BKMK_UserLogsIn"></a> Gebruiker meldt zich aan bij Windows 8  
 Nadat Configuration Manager het inrichtings proces heeft voltooid en het Windows 8-vergrendelings scherm wordt weer gegeven, kan de gebruiker zich aanmelden bij het besturings systeem.
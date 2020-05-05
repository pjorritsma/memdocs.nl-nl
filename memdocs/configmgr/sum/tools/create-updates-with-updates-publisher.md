---
title: Updates maken
titleSuffix: Configuration Manager
description: Software-updates maken en bundelen met System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b2445158732f5adf21c43d73b13039f9e41610c8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723983"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Software-updates en update bundels maken met updates Publisher

*Van toepassing op: System Center Updates Publisher*

Met updates Publisher kunt u de wizard **Update maken** gebruiken om uw eigen updates te maken en de wizard **bundel maken** om bundels van updates te maken.

Omdat deze twee wizards een vergelijk bare werk stroom hebben, verwijst de procedure voor het maken van een update bundel naar de procedure voor het maken van updates, waarbij alleen de relevante verschillen worden beschreven.

## <a name="use-the-create-update-wizard"></a>De wizard Update maken gebruiken
1. Ga in de-console naar de **werk ruimte updates**en kies in het deel venster **aan** de slag de optie **bijwerken** op het tabblad **Start** van het lint. Hiermee opent u de wizard **Update maken** .

2. Gebruik op de pagina **pakket** de volgende informatie om u te helpen bij het configureren van de update:

   -   Kies **Bladeren** om het software-update pakket te zoeken dat u als pakket bron wilt gebruiken. Geldige bronnen zijn. MSI,. MSP of. EXE-bestanden. Updates Publisher heeft toegang tot het bestand nodig om een bestandshash te maken. De hash-en bestands naam worden vervolgens gebruikt in de meta gegevens van de update voor de update die u maakt.

   -   Geef de bron locatie op van de inhoud voor deze update. Normaal gesp roken is dit de locatie waar het binaire bestand van de update wordt gedownload tijdens het publiceren naar een WSUS-server.  Als de optie **een lokale bron voor het publiceren van software-update-inhoud gebruiken** is geselecteerd, is het pad niet vereist.

       Wanneer de update later wordt gepubliceerd op een WSUS-server, downloadt updates Publisher de binaire bestanden voor de update van de aangegeven bron locatie.  Als er geen pad wordt gegeven, zoekt Update Publisher het [pad naar de lokale bron publicatie](updates-publisher-options.md#advanced) voor het binaire update bestand.

   -   Geef de **binaire taal** van de software-update op.

   -   Geef **retour codes voor geslaagde**en **in behandeling zijnde opstart codes** voor de update op. Scheid meerdere retour codes met behulp van een komma. U kunt retour codes gebruiken om te bepalen wanneer de installatie van de update is voltooid en wanneer het opnieuw opstarten is vereist.

       -   Windows Installer-bestanden en-patches (. MSI en. MSP-bestanden) stellen deze waarden automatisch in en kunnen niet worden gewijzigd.

       -   Zo. EXE-updates, de standaard codes die zijn gedefinieerd door de. EXE-bestand wordt gebruikt als er geen retour codes zijn opgegeven.

   -   Geef eventuele opdracht regel argumenten op die vereist zijn voor het installeren van de software-update.

       -   Windows Installer-bestanden en-patches (. MSI en. MSP-bestanden) deze waarden automatisch instellen. Voor deze bestands typen moeten de argumenten als ** \[naam\]=\[waarde\]** worden opgegeven. Daarnaast worden alle opties die beginnen met een **/** (zoals **/qn**) niet ondersteund voor. MSI of. MSP-software-updates.

       -   Zo. EXE-updates, alle argumenten geldig zijn.

3. Op de pagina **informatie** geeft u details op over de update die wordt opgenomen wanneer de update wordt gepubliceerd of geëxporteerd. Details bevatten gelokaliseerde eigenschappen, zoals de naam van de update (titel) en de beschrijving. Vervolgens geeft u meer algemene informatie op, zoals de classificatie, de leverancier, het product en de informatie over de update.

    __Gelokaliseerde eigenschappen:__

   - **Taal**: Selecteer een taal en geef een titel en beschrijving op. U kunt vervolgens extra talen selecteren, één op tijdstip, waarbij elke taal een eigen titel en beschrijving ondersteunt.

   - **Titel**: Voer de naam in van de update. Deze naam wordt weer gegeven in de werk ruimte updates van de update Publisher-console.

   - **Beschrijving**: een beschrijvende beschrijving van de update. U kunt ook zien wat de update installeert en waarom of wanneer deze moet worden gebruikt.

   **Classificatie:** Hieronder vindt u algemene beschrijvingen van de verschillende classificaties.

   - **Update**: een update voor een toepassing of bestand dat momenteel is geïnstalleerd.

   - **Kritiek**: een uitgebreide update voor een specifiek probleem dat betrekking heeft op een kritieke fout die niet gerelateerd is aan de beveiliging.

   - **Feature Pack**: nieuwe product functies die zijn gedistribueerd buiten een product release en die gewoonlijk zijn opgenomen in de volgende volledige product release.

   - **Beveiliging**: een ruim vrijgegeven update voor een productspecifiek probleem dat betrekking heeft op beveiliging.

   - **Update pakket**: een cumulatieve set met hotfixes die samen zijn verpakt voor een eenvoudige implementatie. Deze hotfixes omvatten beveiligingsupdates, essentiële updates, enzovoort. Een update pakket is in het algemeen gericht op een specifiek gebied, zoals beveiliging of een product functie.

   - **Service Pack**: een cumulatieve set met hotfixes die op een toepassing worden toegepast. Deze hotfixes omvatten beveiligingsupdates, essentiële updates, software-updates, enzovoort.

   - **Hulp programma**: Hiermee geeft u een hulp programma of functie op waarmee u een of meer taken kunt volt ooien.

   - **Stuur programma**: een update voor de stuur programma-software.

   **Leverancier:** Geef een leverancier op voor de update. U kunt de vervolg keuzelijst gebruiken om waarden te gebruiken van updates die zich in de opslag plaats bevinden. Wanneer u een leverancier opgeeft, maakt de wizard een map met die leveranciers naam onder **alle software-updates** in de **werk ruimte updates** als deze map nog niet bestaat. Hieronder vindt u Windows Server Update Services (WSUS) gereserveerde namen die niet kunnen worden ingevoerd voor updates die u maakt:
   - Microsoft Corporation
   - Microsoft
   - Bijwerken
   - Software-update
   - Hulpprogramma's
   - Hulpprogramma
   - Kritiek
   - Essentiële updates
   - Beveiliging
   - Beveiligingsupdates
   - Feature Pack
   - Update pakket
   - Service Pack
   - Stuurprogramma
   - Stuur programma-Update
   - Bundel
   - Bundel update

   **Product**: Geef het type product op waarvoor de update is. U kunt de vervolg keuzelijst gebruiken om waarden te gebruiken van updates die zich in de opslag plaats bevinden. Dezelfde lijst met door WSUS gereserveerde namen die niet kunnen worden gebruikt voor de **leverancier**, kan niet worden gebruikt voor het **product**.

   **Meer**informatie-URL: Geef de URL op waar u meer informatie over deze update kunt vinden. U moet kleine letters gebruiken voor **https** of **http** wanneer u deze URL opgeeft.

4. Op de pagina **optionele informatie** kunt u Details configureren die aanvullende informatie over de update bieden.

   -   **Bulletin-id**: Bulletin-id's zijn meestal, maar niet altijd, door update leveranciers.

   -   **Artikel-id**: als er een software-update artikel beschikbaar is, kan de artikel-id handig zijn voor personen die aanvullende informatie over de update zoeken.

   -   **CVE-id's:** Een of meer veelvoorkomende beveiligings lekken en bloot stellingen (CVE)-id's weer geven die beveiligings informatie over de update-of update bundel bieden. Wanneer er meer dan één wordt vermeld, gebruikt u een punt komma om de CVEs te scheiden zoals in dit voor beeld: *CVE1; CVE2.*

   -   **Ondersteunings-URL:** De URL weer geven die ondersteunings informatie bevat voor deze update, indien beschikbaar. U moet kleine letters gebruiken voor **https** of **http** wanneer u deze URL opgeeft.

   -   **Ernst:** Stel het Ernst niveau voor deze update in.

   -   **Impact:** De volgende opties kunnen worden gebruikt om de impact op te geven:
       -   **Normaal –** Gebruik deze optie om aan te geven dat de update standaard installatie procedures vereist.
       -   **Secundair –** Gebruik deze om aan te geven dat de update minimale installatie procedures vereist.
       -   **Exclusief verwerking vereist –** Gebruik deze om aan te geven dat de update op zichzelf moet worden geïnstalleerd, exclusief van andere updates.   <br /><br />

   -   **Gedrag voor opnieuw opstarten:** Hiermee geeft u informatie op over het gedrag voor het opnieuw opstarten van updates. Deze instelling heeft geen invloed op het werkelijke gedrag van de installatie van de update.

       -   **Nooit opnieuw opstarten**: de computer voert het systeem nooit opnieuw te starten na de installatie van de software-update.
       -   **Altijd opnieuw opstarten vereist**: de computer voert altijd opnieuw opstarten van het systeem uit na de installatie van de software-update.
       -   **Kan opnieuw opstarten aanvragen**: na de installatie van de software-update vraagt de computer het systeem alleen opnieuw op als opnieuw opstarten nodig is. De gebruiker heeft de optie om de herstart uit te stellen. Dit is de standaardwaarde. <br /><br />

5. Geef op de pagina **vereisten** de vereisten op die moeten worden geïnstalleerd op een computer voordat deze update kan worden geïnstalleerd. Vereisten kunnen **detectoids** of andere updates zijn. Detectoids zijn regels op hoog niveau, zoals een regel die vereist dat de computers CPU een 64-bits processor zijn. Detectoids kan ook specifieke updates opgeven die moeten worden geïnstalleerd voordat deze update kan worden geïnstalleerd.

   -   Gebruik detectoids in plaats van *Installeer bare* en *geïnstalleerde regels* te maken waarmee dezelfde controle of actie wordt uitgevoerd voor betere prestaties.

   Gebruik de zoek optie voor **beschik bare software-updates en detectoids** om u te helpen bij het vinden van specifieke updates of detectoids. Zoek bijvoorbeeld naar **CPU** om de detectoids te vinden waarmee u de installatie kunt beperken op basis van een specifieke CPU-architectuur.

   U kunt een of meer items tegelijk selecteren om toe te voegen als een vereiste. Bij het toevoegen van vereisten, worden de geselecteerde detectoids toegevoegd als een of meer groepen. Om in aanmerking te komen voor installatie, moet een computer voldoen aan de vereiste van ten minste één lid van elke groep die u configureert:

   -   Wanneer u op **vereiste toevoegen klikt,** worden alle items die u hebt geselecteerd, toegevoegd aan afzonderlijke, afzonderlijke groepen. Om in aanmerking te komen voor deze update, moet een computer voldoen aan de vereisten in deze groep en voldoen aan de vereisten voor eventuele extra groepen die zijn geconfigureerd.

   -   Wanneer u op **groep toevoegen klikt,** worden alle items die u hebt geselecteerd, toegevoegd aan één groep. Een computer die in aanmerking komt voor deze update moet voldoen aan ten minste één van de vereisten in deze groep en de vereisten door geven voor alle extra groepen die zijn geconfigureerd.

6. Geef op de **vervangings** pagina de updates op die door deze update worden vervangen (vervangen). Wanneer deze update is gepubliceerd, markeert Configuration Manager elke update die wordt vervangen als **verlopen**. Clients installeren vervolgens deze update in plaats van de vervangen updates.

7. Gebruik op de pagina **toepas baarheid** de **regel Editor** om een set regels te definiëren waarmee wordt bepaald of een apparaat deze update nodig heeft. (Deze pagina is vergelijkbaar met de **geïnstalleerde** pagina die deze volgt.)

   Als u een nieuwe regel wilt toevoegen, klikt u op ![Nieuwe regel](media/newrule.png). Hiermee opent u de pagina toepasselijkheid regel waar u regels kunt configureren.

   Soorten regels die u kunt maken zijn onder andere:

   -   **Bestand** : gebruik deze regel om te vereisen dat een apparaat een bestand heeft met eigenschappen die voldoen aan een of meer criteria die u opgeeft voordat deze update kan worden toegepast.

   -   **REGI ster –** Gebruik dit type om register Details op te geven die aanwezig moeten zijn voordat een apparaat in aanmerking komt voor het installeren van deze update.

   -   **Systeem:** Deze regel gebruikt systeem gegevens om de toepas baarheid te bepalen. U kunt kiezen tussen het definiëren van een Windows-versie, een Windows-taal, een processor architectuur of het opgeven van een WMI-query voor het identificeren van het besturings systeem van het apparaat.

   -   **Windows Installer –** Gebruik dit regel type om toepas baarheid te bepalen op basis van een geïnstalleerd. MSI-of Windows Installer-patch (. MSP). U kunt ook bepalen of specifieke onderdelen of onderdelen worden geïnstalleerd als onderdeel van de vereiste.

       > [!IMPORTANT]  
       > Op beheerde apparaten kan de Windows Update-agent geen Windows-installatie pakketten detecteren die per gebruiker zijn geïnstalleerd. Wanneer u dit regel type gebruikt, configureert u aanvullende regels voor toepasselijkheid, zoals bestands versies of register sleutel waarden, zodat het Windows Installer-pakket correct kan worden gedetecteerd, ongeacht de basis van een gebruiker of per systeem.

   -   **Opgeslagen regel –** Met deze optie kunt u regels vinden en gebruiken die u hebt *gemaakt in de werk ruimte regels*.

       Nadat u een regel hebt gemaakt, kunt u de andere pictogrammen gebruiken om de regel te wijzigen, en als er meerdere regels zijn, om relaties tussen deze regels te definiëren.

   Wanneer u klaar bent met het maken en toevoegen van regels, klikt u op **OK** in het dialoog venster **regelset maken** om die set op te slaan. U kunt vervolgens een **nieuwe** regel maken en toevoegen aan de set.

   Wanneer u meerdere regels of regel sets aan een update wilt toevoegen, kunt u de logische Opera tors in de **regel Editor** gebruiken om voor waarden te bepalen tussen de regels en in welke volg orde ze worden verwerkt.

8. Gebruik op de pagina **geïnstalleerd** de **regel editor om** een set regels te definiëren waarmee wordt bepaald of de update die u configureert, al is geïnstalleerd op een apparaat. (Deze pagina is vergelijkbaar met de pagina **toepas baarheid** die deze pagina doorloopt.)

   Deze pagina van de wizard ondersteunt het configureren van regels met dezelfde opties en criteria als de pagina **toepasselijkheid** .

   Wanneer de wizard is voltooid, wordt de nieuwe update toegevoegd aan een knoop punt in de **werk ruimte updates** die wordt geïdentificeerd door de **leverancier** en de **product** naam die u voor die update hebt gebruikt.

## <a name="use-the-create-bundle-wizard"></a>De wizard bundel maken gebruiken
Omdat deze wizard dezelfde werk stroom gebruikt als de [wizard Update maken](#use-the-create-update-wizard), gebruikt u die werk stroom, maar let op het volgende verschil voor bundels:

1.  Als u de wizard wilt starten, gaat u naar de **werk ruimte updates**in de-console en selecteert u vervolgens **bundel** op het tabblad **Start** van het lint.

2.  In tegens telling tot de wizard Update maken is er geen pakket pagina bij het maken van een bundel.

3.  Geef op de pagina **gegevens** Details op over de update bundel die worden opgenomen wanneer de update wordt gepubliceerd of geëxporteerd.

4.  Op de pagina **optionele informatie** kunt u Details configureren die extra informatie geven over de update bundel. De beschik bare opties zijn hetzelfde als voor het maken van een update. Opties voor impact en opnieuw starten zijn echter niet beschikbaar, omdat ze niet van toepassing zijn op bundels.

5.  Geef op de pagina **vereisten** de vereisten op die moeten worden geïnstalleerd op een computer voordat deze bundel kan worden geïnstalleerd. Deze regels zijn hetzelfde als voor afzonderlijke updates.

6.  Op de **vervangings** pagina geeft u de updates op die worden vervangen (vervangen) door deze update bundel. Deze regels zijn hetzelfde als voor afzonderlijke updates.

7.  Op de pagina **leden** selecteert u updates om toe te voegen aan de update bundel. Alleen updates die u hebt gemaakt of geïmporteerd in updates Publisher zijn beschikbaar.

Wanneer de wizard is voltooid, wordt de nieuwe update bundel toegevoegd aan een knoop punt in de **werk ruimte updates** die wordt geïdentificeerd door de naam van de **leverancier** die u hebt gebruikt voor de update bundel.

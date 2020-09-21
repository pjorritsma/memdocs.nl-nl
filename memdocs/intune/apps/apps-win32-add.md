---
title: Win32-apps toevoegen en toewijzen aan Microsoft Intune
titleSuffix: ''
description: Ontdek hoe u Win32-apps toevoegt, toewijst en beheert met Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5266f354ea5806743813d1aeb4c456890fa46b19
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083944"
---
# <a name="add-assign-and-monitor-a-win32-app-in-microsoft-intune"></a>Een Win32-app toevoegen, toewijzen en bewaken in Microsoft Intune

Nadat u een [Win32-app hebt voorbereid om te worden geüpload naar Intune](apps-win32-prepare.md) met behulp van het [Microsoft-hulpprogramma voor het voorbereiden van Win32-inhoud](https://go.microsoft.com/fwlink/?linkid=2065730), kunt u de app aan Intune toevoegen. Zie [Inhoud van Win32-apps voorbereiden voor uploaden](apps-win32-prepare.md) voor meer informatie over het voorbereiden van een Win32-app die moet worden geüpload.

## <a name="prerequisites"></a>Vereisten

Als u Win32-app-beheer wilt gebruiken, moet u aan de volgende criteria voldoen:

- Gebruik Windows 10 versie 1607 of hoger (Enterprise, Pro en Education).
- Apparaten moeten worden gekoppeld aan Azure Active Directory (Azure AD) en automatisch ingeschreven. De Intune-beheeruitbreiding biedt ondersteuning voor apparaten die zijn toegevoegd aan Azure AD, aan een hybride domein zijn toegevoegd en via een groepsbeleid zijn ingeschreven. 
  > [!NOTE]
  > Voor het scenario met inschrijving via het groepsbeleid maakt de gebruiker gebruik van het lokale gebruikersaccount om hun Windows 10-apparaat met Azure AD samen te voegen. Gebruikers moeten zich op het apparaat aanmelden met hun Azure AD-gebruikersaccount en zich bij inschrijven bij Intune. Intune installeert de Intune-beheerextensie op het apparaat als een PowerShell-script of een Win32-app op de gebruiker of het apparaat is gericht.
- De grootte van Windows-toepassingen is beperkt tot 8 GB per app.

Net als bij een LOB-app (Line-Of-Business) kunt u een Win32-app aan Microsoft Intune toevoegen. Dit type app wordt doorgaans intern of door een externe partij geschreven. 

## <a name="process-flow-to-add-a-win32-app-to-intune"></a>Processtroom om een Win32-app aan Intune toe te voegen

<img alt="Flow chart of the process to add a Win32 app to Intune." src="./media/apps-win32-app-management/add-win32-app.svg" width="500">

## <a name="add-a-win32-app-to-intune"></a>Een Win32-app toevoegen aan Intune

Met de volgende stappen kunt u een Windows-app aan Intune toevoegen:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Alle apps** > **Toevoegen**.
3. Selecteer in het deelvenster **Een app-type selecteren**, onder het app-type **Overige**, de optie **Windows-app (Win32)** .

    > [!IMPORTANT]
    > Gebruik de nieuwste versie van het hulpprogramma voor voorbereiding van Microsoft Win32-inhoud. Als u de nieuwste versie niet gebruikt, krijgt u de waarschuwing dat de app met een oudere versie van het hulpprogramma is ingepakt. 

4. Klik op **Selecteren**. De stappen voor **App toevoegen** worden weergegeven.

## <a name="step-1-app-information"></a>Stap 1: App-gegevens

### <a name="select-the-app-package-file"></a>Het app-pakketbestand selecteren

1. Klik in het deelvenster **App toevoegen** op **App-pakketbestand selecteren**. 
2. Selecteer in het deelvenster **App-pakketbestand** de bladerknop. Selecteer vervolgens een Windows-installatiebestand met de extensie *.intunewin*.
   De app-gegevens worden weergegeven.
3. Wanneer u klaar bent, selecteert u **OK** in het deelvenster **App-pakketbestand**.

### <a name="set-app-information"></a>App-gegevens instellen

Voeg de details voor de app toe op de pagina **App-gegevens**. Afhankelijk van de app die u hebt gekozen, worden bepaalde waarden in het deelvenster mogelijk automatisch ingevuld.

- **Naam**: voer de naam van de app in zoals deze in de bedrijfsportal wordt weergegeven. Zorg ervoor dat alle app-namen die u gebruikt, uniek zijn. Als dezelfde app-naam twee keer voorkomt, wordt slechts één van de apps weergegeven voor gebruikers in de bedrijfsportal.
- **Beschrijving**: voer een beschrijving van de app in. De beschrijving wordt weergegeven in de bedrijfsportal.
- **Uitgever**: Voer de naam van de uitgever van de app in.
- **Categorie**: selecteer een of meer van de ingebouwde app-categorieën of selecteer een categorie die u hebt gemaakt. Met categorieën kunnen gebruikers de app gemakkelijker vinden wanneer ze door de bedrijfsportal bladeren.
- **Deze weergeven als aanbevolen app in de bedrijfsportal**: Geef de app prominent weer op de hoofdpagina van de bedrijfsportal wanneer gebruikers door apps bladeren.
- **Informatie-URL**: Voer de URL in van een website die informatie over deze app bevat (optioneel). De URL wordt weergegeven in de bedrijfsportal.
- **Privacy-URL**: (optioneel) Voer de URL in van een website die privacyinformatie over deze app bevat. De URL wordt weergegeven in de bedrijfsportal.
- **Ontwikkelaar**: Voer de naam in van de app-ontwikkelaar (optioneel).
- **Eigenaar**: voer een naam in voor de eigenaar van deze app (optioneel). Bijvoorbeeld **HR-afdeling**.
- **Opmerkingen**: voer de opmerkingen in die u aan deze app wilt koppelen.
- **Logo**: upload een pictogram dat aan de app is gekoppeld. Het pictogram wordt samen met de app weergegeven wanneer gebruikers door de bedrijfsportal bladeren.

Selecteer **Volgende** om de pagina **Programma** weer te geven.

## <a name="step-2-program"></a>Stap 2: Programma

Configureer op de pagina **Programma** de opdrachten voor het installeren en verwijderen van de app:

- **Opdracht voor installeren**: Voeg de volledige installatieopdrachtregel toe om de app te installeren. 

    Als de bestandsnaam van uw app bijvoorbeeld **MyApp123** is, voegt u het volgende toe:

    `msiexec /p "MyApp123.msp"`
    
    Als de toepassing `ApplicationName.exe` is, bestaat de opdracht uit de naam van de toepassing, gevolgd door de opdrachtargumenten (switches) die door het pakket worden ondersteund. Bijvoorbeeld:

    `ApplicationName.exe /quiet`
    
    In de vorige opdracht biedt het `ApplicationName.exe`-pakket ondersteuning voor het opdrachtargument `/quiet`. 
    
    Neem voor de specifieke argumenten die door het toepassingspakket worden ondersteund contact op met de leverancier van de toepassing.

    > [!IMPORTANT]
    > Beheerders moeten voorzichtig zijn wanneer ze de opdrachtregelprogramma's gebruiken. Onverwachte of schadelijke opdrachten kunnen worden doorgegeven via de opdrachtvelden **Installeren** en **Verwijderen**.

- **Opdracht voor verwijderen**: Voeg de volledige opdrachtregel om de app te verwijderen op basis van de unieke id van de app. 

    Bijvoorbeeld:
    
    `msiexec /x "{12345A67-89B0-1234-5678-000001000000}"`

- **Installatiegedrag**: stel het Installatiegedrag in op **Systeem** of **Gebruiker**.

    > [!NOTE]
    > U kunt een Win32-app configureren voor installatie in een **gebruikers**- of **systeem**context. Context van de **gebruiker** verwijst slechts naar een bepaalde gebruiker. Een **systeem**context verwijst naar alle gebruikers van een Windows 10-apparaat.
    >
    > Gebruikers hoeven niet te zijn aangemeld bij het apparaat om Win32-apps te installeren.
    > 
    > Het installeren en verwijderen van de Win32-app wordt (standaard) uitgevoerd met beheerdersbevoegdheden wanneer voor de app is ingesteld dat deze in de gebruikerscontext moet worden geïnstalleerd en de gebruiker op het apparaat beheerdersbevoegdheden heeft.
    
- **Gedrag voor opnieuw opstarten van apparaat**: Selecteer een van de volgende opties:
    - **Bepaal gedrag op basis van retourcodes**: Kies deze optie om het apparaat opnieuw op te starten op basis van de retourcodes.
    - **Geen specifieke actie**: Kies deze optie om het opnieuw opstarten van het apparaat te onderdrukken tijdens de app-installatie van op MSI gebaseerde apps.
    - **Na installatie van de app kan opnieuw opstarten van het apparaat worden afgedwongen**: Selecteer deze optie om de installatie van de app te voltooien zonder opnieuw opstarten te onderdrukken.
    - **Via Intune wordt opnieuw opstarten van het apparaat afgedwongen**: Kies deze optie om het apparaat altijd opnieuw op te starten nadat de installatie van een app is voltooid.

- **Geef de retourcodes op het gedrag na installatie op te geven**: Voeg de retourcodes toe waarmee het gedrag voor opnieuw proberen van de installatie of het gedrag na installatie voor de app wordt opgegeven. De retourcodevermeldingen worden tijdens het maken van een app standaard toegevoegd. U kunt echter meer retourcodes toevoegen of bestaande retourcodes wijzigen.
    1. Stel in de kolom **Codetype** het **Codetype** in op een van de volgende opties:
        - **Mislukt**: de retourwaarde die wijst op een app-installatiefout.
        - **Hard opstarten**: de retourcode voor hard opstarten staat niet toe dat de volgende Win32-app worden geïnstalleerd op de client zonder opnieuw op te starten. 
        - **Zacht opstarten**: de retourcode voor zacht opstarten staat toe dat de volgende Win32-app wordt geïnstalleerd zonder dat de client opnieuw moet worden opgestart. Opnieuw opstarten is nodig om de installatie van de huidige app te voltooien.
        - **Opnieuw**: er worden drie pogingen gedaan de app opnieuw te installeren. Tussen de pogingen wordt vijf minuten gewacht. 
        - **Geslaagd**: de retourwaarde die aangeeft dat de app is geïnstalleerd.
    2. Selecteer indien nodig **Toevoegen** om meer retourcodes toe te voegen of bestaande retourcodes te wijzigen.

Selecteer **Volgende** om de pagina **Vereisten** weer te geven.    

## <a name="step-3-requirements"></a>Stap 3: Vereisten

Geef op de pagina **Vereisten** de vereisten op waaraan apparaten moeten voldoen voordat de app wordt geïnstalleerd:

- **Architectuur van besturingssysteem**: kies de architecturen die nodig zijn voor het installeren van de app.
- **Minimumversie van het besturingssysteem**: selecteer de minimumversie van het besturingssysteem die nodig is om de app te installeren.
- **Vereiste schijfruimte (MB)** : voeg optioneel de vrije schijfruimte op het systeemstation toe die nodig is om de app te installeren.
- **Vereiste fysieke geheugen (MB)** : voeg optioneel het fysieke geheugen (RAM) toe dat nodig is om de app te installeren.
- **Minimumaantal vereiste logische processors**: voeg optioneel het minimumaantal logische processors toe dat nodig is om de app te installeren.
- **Minimale vereiste processorsnelheid (MHz)** : voeg optioneel de minimale processorsnelheid toe die nodig is om de app te installeren.
- **Aanvullende vereisteregels configureren**: 
    1. Selecteer **Toevoegen** om het deelvenster **Een vereisteregel toevoegen** weer te geven en meer vereisteregels te configureren. Selecteer de waarde **Vereistetype** om het type regel te kiezen dat u wilt gebruiken om te bepalen hoe een vereiste moet worden gevalideerd. Vereisteregels kunnen op informatie over het bestandssysteem, registerwaarden of PowerShell-scripts worden gebaseerd. 
        - **Bestand**: Als u **Bestand** als waarde voor **Vereistetype** kiest, moet de vereisteregel een bestand of map, datum, versie of grootte detecteren. 
            - **Pad**: Het volledige pad van de map met het bestand of de map die u wilt detecteren.
            - **Bestand of map**: het bestand of de map dat moet worden gedetecteerd.
            - **Eigenschap**: selecteer het type regel dat moet worden gebruikt om de aanwezigheid van de app te valideren.
            - **Gekoppeld aan een 32-bits app op 64-bits clients**: Selecteer **Ja** om eventuele padomgevingsvariabelen in een 32-bits context op 64-bits clients uit te breiden. Selecteer **Nee** (standaard) om padvariabelen in een 64-bits context op 64-bits clients uit te breiden. 32-bits clients gebruiken altijd de 32-bits context.
        - **Register**: Als u **Register** als waarde voor **Vereistetype** kiest, moet de vereisteregel een registerinstelling op basis van een waarde, tekenreeks, geheel getal of versie detecteren.
            - **Sleutelpad**: het volledige pad van de registervermelding die de te detecteren waarde bevat.
            - **Waardenaam**: de naam van de te detecteren registerwaarde. Als deze waarde leeg is, wordt de detectie op de sleutel uitgevoerd. De (standaard)waarde van een sleutel wordt als detectiewaarde gebruikt als de detectiemethode anders is dan het bestaan van het bestand of de map.
            - **Vereiste voor registersleutel**: selecteer het vergelijkingstype voor registersleutels dat wordt gebruikt om te bepalen hoe de vereisteregel moet worden gevalideerd.
            - **Gekoppeld aan een 32-bits app op 64-bits clients**: Selecteer **Ja** om het 32-bits register op 64-bits clients te doorzoeken. Selecteer **Nee** (standaard) om het 64-bits register op 64-bits clients te doorzoeken. Voor 32-bits clients wordt altijd het 32-bits register doorzocht.
        - **Script**: Kies **Script** als de waarde voor **Vereistetype** als u geen vereisteregel kunt maken op basis van een bestand, register of een andere methode die in de Intune-console beschikbaar is.
            - **Scriptbestand**: voor een regel op basis van een PowerShell-scriptvereiste, en als de bestaande code 0 is, wordt de standaarduitvoer (STDOUT) in meer detail gedetecteerd. We kunnen STDOUT bijvoorbeeld als geheel getal met de waarde 1 detecteren.
            - **Script uitvoeren als 32-bits proces op 64-bits clients**: selecteer **Ja** om het script in een 32-bits proces op 64-bits clients uit te voeren. Selecteer **Nee** (standaard) om het script in een 64-bits proces op 64-bits clients uit te voeren. 32-bits clients voeren het script uit in een 32-bits proces.
            - **U kunt dit script als volgt uitvoeren met behulp van de aanmeldingsgegevens**: Selecteer **Ja** om het script uit te voeren met behulp van de referenties waarmee op het apparaat is aangemeld.
            - **Controle van handtekening voor script afdwingen**: selecteer **Ja** om te verifiëren dat een vertrouwde uitgever het script heeft ondertekend, zodat het script zonder waarschuwingen of prompts kan worden uitgevoerd. Het script wordt niet geblokkeerd terwijl het wordt uitgevoerd. Selecteer **Nee** (standaard) om het script met bevestiging van de gebruiker zonder handtekeningverificatie uit te voeren.
            - **Gegevenstype uitvoer selecteren**: selecteer het gegevenstype dat wordt gebruikt voor het bepalen van de overeenkomst met een vereisteregel.
    2. Als u klaar bent met het instellen van de regels voor vereisten, selecteert u **OK**.

Selecteer **Volgende** om de pagina **Detectieregels** weer te geven. 

## <a name="step-4-detection-rules"></a>Stap 4: Detectieregels

Configureer op de pagina **Detectieregels** de regels voor het detecteren van de aanwezigheid van de app:
    
- **Regelnotatie**: selecteer hoe de aanwezigheid van de app moet worden gedetecteerd. U kunt de detectieregels handmatig configureren of een aangepast script gebruiken om de aanwezigheid van de app te detecteren. U moet minstens één detectieregel kiezen. 

  > [!NOTE]
  > U kunt in het deelvenster **Detectieregels** meerdere regels toevoegen. Er moet aan de voorwaarden van *alle* regels worden voldaan om de app te detecteren.
  >
  > Als in Intune wordt gedetecteerd dat de app niet aanwezig is op het apparaat, wordt de app na 24 uur opnieuw aangeboden via Intune. Dit gebeurt alleen voor apps met de vereiste intentie.

- **Detectieregels handmatig configureren**: u kunt een van de volgende regeltypen selecteren:
    - **MSI**: verifiëren op basis van een controle van de MSI-versie. Deze optie kan slechts eenmaal worden toegevoegd. Als u dit regeltype kiest, hebt u twee instellingen:
        - **MSI-productcode**: voeg een geldige MSI-productcode aan de app toe.
        - **Versiecontrole van MSI-product**: selecteer **Ja** om de MSI-productversie en de MSI-productcode te controleren.
    - **Bestand**: verifieer op basis van bestand- of mapdetectie, datum, versie of grootte.
        - **Pad**: voer het volledige pad in van de map met het bestand of de map die u wilt detecteren.
        - **Bestand of map**: voer het bestand (of de map) in dat (die) moet worden gedetecteerd.
        - **Detectiemethode**: selecteer het type detectiemethode dat wordt gebruikt om de aanwezigheid van de app te valideren.
        - **Gekoppeld aan een 32-bits app op 64-bits clients**: Selecteer **Ja** om eventuele padomgevingsvariabelen in een 32-bits context op 64-bits clients uit te breiden. Selecteer **Nee** (standaard) om padvariabelen in een 64-bits context op 64-bits clients uit te breiden. 32-bits clients gebruiken altijd de 32-bits context.
            
        **Voorbeelden van detectie op basis van bestanden**

        Controleer op het bestaan van het bestand.
         
        ![Schermopname van het deelvenster Detectieregels: bestaan van bestand.](./media/apps-win32-app-management/apps-win32-app-03.png)
        
        Controleer op het bestaan van de map.
        
        ![Schermopname van het deelvenster Detectieregels: bestaan van map.](./media/apps-win32-app-management/apps-win32-app-04.png)
        
    - **Register**: verifieer op basis van waarde, tekenreeks, geheel getal of versie.
        - **Sleutelpad**: het volledige pad van de registervermelding die de te detecteren waarde bevat. Een geldige syntaxis is HKEY_LOCAL_MACHINE \Software\WinRAR of HKLM\Software\WinRAR.
        - **Waardenaam**: de naam van de te detecteren registerwaarde. Als deze waarde leeg is, wordt de detectie op de sleutel uitgevoerd. De (standaard)waarde van een sleutel wordt als detectiewaarde gebruikt als de detectiemethode anders is dan het bestaan van het bestand of de map.
        - **Detectiemethode**: selecteer het type detectiemethode dat wordt gebruikt om de aanwezigheid van de app te valideren.
        - **Gekoppeld aan een 32-bits app op 64-bits clients**: Selecteer **Ja** om het 32-bits register op 64-bits clients te doorzoeken. Selecteer **Nee** (standaard) om het 64-bits register op 64-bits clients te doorzoeken. Voor 32-bits clients wordt altijd het 32-bits register doorzocht.
            
        **Voorbeelden voor detectie op basis van een register**
        
        Controleer of de registersleutel bestaat.
            
        ![Schermopname van het deelvenster Detectieregels: registersleutel bestaat.](./media/apps-win32-app-management/apps-win32-app-05.png)    
            
        Controleer of de registerwaarde bestaat.
        
        ![Schermopname van het deelvenster Detectieregels: registerwaarde bestaat.](./media/apps-win32-app-management/apps-win32-app-06.png)    
        
        Controleer op gelijke tekenreeksen aan die van de registerwaarde.
        
        ![Schermopname van het deelvenster Detectieregels: gelijke tekenreeks registerwaarde.](./media/apps-win32-app-management/apps-win32-app-07.png)    
     
- **Een aangepast detectiescript gebruiken**: geef het PowerShell-script op dat wordt gebruikt voor het detecteren van deze app. 
    
   - **Scriptbestand**: selecteer een PowerShell-script waarmee de aanwezigheid van de app op de client wordt gedetecteerd. De app worden gedetecteerd wanneer het script zowel een afsluitcode met waarde **0** retourneert als een tekenreekswaarde naar STDOUT schrijft.

   - **Script uitvoeren als 32-bits proces op 64-bits clients**: selecteer **Ja** om het script in een 32-bits proces op 64-bits clients uit te voeren. Selecteer **Nee** (standaard) om het script in een 64-bits proces op 64-bits clients uit te voeren. 32-bits clients voeren het script uit in een 32-bits proces.

   - **Controle van handtekening voor script afdwingen**: selecteer **Ja** om te verifiëren dat een vertrouwde uitgever het script heeft ondertekend, zodat het script zonder waarschuwingen of prompts kan worden uitgevoerd. Het script wordt niet geblokkeerd terwijl het wordt uitgevoerd. Selecteer **Nee** (standaard) om het script met bevestiging van de gebruiker zonder handtekeningverificatie uit te voeren.
    
   De Intune-agent controleert de resultaten vanuit het script. Het leest de waarden die door het script zijn geschreven naar de STDOUT-stroom, de standaardfoutstroom (STDERR) en de afsluitcode. Als het script wordt afgesloten met een andere waarde dan nul, mislukt het script en is de app-detectiestatus Niet geïnstalleerd. Als de afsluitcode nul is en STDOUT gegevens bevat, is de status van de toepassingsdetectie Geïnstalleerd. 

   > [!NOTE]
   > U wordt aangeraden uw script te coderen als UTF-8. Als het script wordt afgesloten met de waarde **0**, is het script uitgevoerd. Het tweede uitvoerkanaal geeft aan dat de app is gedetecteerd. STDOUT-gegevens geven aan dat de app op de client is gevonden. Er wordt niet naar een bepaalde tekenreeks van STDOUT gezocht.

Nadat u uw regels hebt toegevoegd, selecteert u **Volgende** om de pagina **Afhankelijkheden** weer te geven.

## <a name="step-5-dependencies"></a>Stap 5: Afhankelijkheden

App-afhankelijkheden zijn toepassingen die moeten worden geïnstalleerd voordat u uw Win32-app kunt installeren. U kunt vereisen dat andere apps als afhankelijkheden worden geïnstalleerd. 

Op het apparaat moeten met name de afhankelijke apps worden geïnstalleerd voordat de Win32-app wordt geïnstalleerd. Er is een maximum van 100 afhankelijkheden. Dit is inclusief de afhankelijkheden van eventueel opgenomen afhankelijkheden en de app zelf. 

U kunt alleen Win32-afhankelijkheden toevoegen nadat uw Win32-app is toegevoegd en naar Intune is geüpload. Nadat de Win32-app is toegevoegd, ziet u de optie **Afhankelijkheden** in het deelvenster voor uw Win32-app. 

Elke Win32-app-afhankelijkheid moet ook een Win32-app zijn. Er wordt geen ondersteuning geboden voor afhankelijkheid van andere typen apps, zoals enkelvoudige MSI LOB-apps of Microsoft Store-apps.

Wanneer u een app-afhankelijkheid toevoegt, kunt u een zoekopdracht uitvoeren op basis van de naam en uitgever van de app. Daarnaast kunt u de toegevoegde afhankelijkheden sorteren op basis van de naam en uitgever van de app. Eerder toegevoegde app-afhankelijkheden kunnen niet worden geselecteerd in de lijst met toegevoegde app-afhankelijkheden. 

U kunt kiezen of elke afhankelijke app automatisch moet worden geïnstalleerd. Standaard is de optie **Automatisch installeren** voor elke afhankelijkheid ingesteld op **Ja**. Door automatisch een afhankelijke app te installeren, zelfs als de afhankelijke app niet op de gebruiker of het apparaat is gericht, installeert Intune de app op het apparaat om aan de afhankelijkheid te voldoen voordat u uw Win32-app installeert. 

Let op: een afhankelijkheid kan recursieve onderliggende afhankelijkheden hebben en elke onderliggende afhankelijkheid wordt geïnstalleerd vóór de hoofdafhankelijkheid wordt geïnstalleerd. Daarnaast worden afhankelijkheden niet volgens een bepaalde volgorde bij een gegeven afhankelijkheidsniveau geïnstalleerd.

### <a name="select-the-dependencies"></a>De afhankelijkheden selecteren

Selecteer op de pagina **Afhankelijkheden** toepassingen die moeten worden geïnstalleerd voordat u uw Win32-app kunt installeren:
1. Selecteer **Toevoegen** om het deelvenster **Afhankelijkheid toevoegen** weer te geven.
3. Voeg de afhankelijke apps toe en klik op **Selecteren**.
4. Selecteer **Ja** of **Nee** onder de kolom **Automatisch installeren** om te kiezen of de afhankelijke apps automatisch moeten worden geïnstalleerd.

Nadat u afhankelijkheden hebt geselecteerd, selecteert u **Volgende** om de pagina **Bereiktags** weer te geven.

### <a name="understand-additional-dependency-details"></a>Meer informatie over aanvullende afhankelijkheden

Gebruikers zien meldingen van Windows die aangeven dat er afhankelijke apps worden gedownload en geïnstalleerd als onderdeel van het installatieproces van de Win32-app. Daarnaast zien gebruikers over het algemeen een van de volgende meldingen als een afhankelijke app niet is geïnstalleerd:
- Een of meer afhankelijke apps zijn niet geïnstalleerd.
- Er is niet voldaan aan een of meer vereisten voor afhankelijke apps.
- Een of meer afhankelijke apps zijn in afwachting van het opnieuw opstarten van het apparaat.

Als u geen afhankelijkheid in de kolom **Automatisch installeren** wilt plaatsen, wordt de installatie van de Win32-app niet gestart. Daarnaast wordt in een app-rapport aangegeven dat de afhankelijkheid als `failed` is gemarkeerd. Er wordt vervolgens een reden opgegeven waarom de installatie niet is gelukt. Selecteer een fout (of waarschuwing) in de [installatiedetails](troubleshoot-app-install.md#win32-app-installation-troubleshooting) van de Win32-app om de installatiefout van de afhankelijkheid weer te geven.

Op elke afhankelijkheid wordt de Intune Win32-app-logica voor opnieuw proberen (drie keer opnieuw proberen te installeren na vijf minuten wachten) en de algemene planning voor opnieuw beoordelen toegepast. Daarnaast zijn afhankelijkheden alleen van toepassing tijdens de installatie van de Win32-app op het apparaat. Afhankelijkheden zijn niet van toepassing bij het verwijderen van een Win32-app. Als u een afhankelijkheid wilt verwijderen, selecteert u het beletselteken (drie puntjes) links van de afhankelijke app, aan het einde van de rij van de lijst met afhankelijkheden. 

## <a name="step-6-select-scope-tags-optional"></a>Stap 6: Bereiktags selecteren (optioneel)
U kunt bereiktags gebruiken om te bepalen wie er informatie over client-apps mag bekijken in Intune. Zie [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Op rollen gebaseerd toegangsbeheer en bereiktags gebruiken voor gedistribueerde IT) voor uitgebreide informatie over bereiktags.

Klik op **Bereiktags selecteren** om desgewenst bereiktags toe te voegen voor de app. Selecteer **Volgende** om de pagina **Toewijzingen** weer te geven.

## <a name="step-7-assignments"></a>Stap 7: Toewijzingen

U kunt de groepstoewijzingen **Vereist**, **Beschikbaar voor ingeschreven apparaten** of **Verwijderen** selecteren voor de app. Zie [Groepen toevoegen om gebruikers en apparaten in te delen](../fundamentals/groups-add.md) en [Apps toewijzen aan groepen met Microsoft Intune](apps-deploy.md) voor meer informatie.

1. Selecteer een toewijzingstype voor de specifieke app:
    - **Vereist**: de app wordt geïnstalleerd op apparaten in de geselecteerde groepen.
    - **Beschikbaar voor ingeschreven apparaten**: gebruikers installeren de app vanuit de bedrijfsportal-app of -website.
    - **Verwijderen**: de app wordt verwijderd van apparaten in de geselecteerde groepen.
2. Selecteer **Groep toevoegen** en wijs de groepen toe die deze app gaan gebruiken.
3. Selecteer in het deelvenster **Groepen selecteren** de toe te wijzen groepen op basis van gebruikers of apparaten.
4. Nadat u uw groepen hebt geselecteerd, kunt u ook **Meldingen van eindgebruiker**, **Beschikbaarheid** en **Installatiedeadline** instellen. Zie [Beschikbaarheid en meldingen voor Win32-apps instellen](apps-win32-app-management.md#set-win32-app-availability-and-notifications)voor meer informatie.
5. Als u niet wilt dat deze app-toewijzing van invloed is op groepen gebruikers, selecteert u **Opgenomen** onder de kolom **MODUS**. Wijzig in het deelvenster **Toewijzing bewerken** de waarde voor **Modus** van  **Opgenomen** in **Uitgesloten**. Selecteer **OK** om het deelvenster **Toewijzing bewerken** te sluiten.
6. Selecteer in de sectie **App-instellingen** de waarde voor **Prioriteit van leveringsoptimalisatie** voor de app. Met deze instelling wordt bepaald hoe de inhoud van de app wordt gedownload. U kunt ervoor kiezen om de app-inhoud te downloaden in de achtergrondmodus of de voorgrondmodus op basis van de toewijzing. 

Als u de toewijzingen voor de apps hebt ingesteld, selecteert u **Volgende** om de pagina **Controleren en maken** weer te geven.

## <a name="step-8-review-and-create"></a>Stap 8: Controleren en maken

1. Controleer de waarden en instellingen die u voor de app hebt ingevoerd. Controleer of de app-gegevens die u hebt geconfigureerd correct zijn.
2. Selecteer **Maken** om de app aan Intune toe te voegen.

    Het deelvenster **Overzicht** voor de LOB-app wordt weergegeven.

U hebt nu de stappen voor het toevoegen van een Win32-app aan Intune voltooid. Zie [Apps toewijzen aan groepen met Microsoft Intune](apps-deploy.md) en [App-gegevens en -toewijzingen controleren met Microsoft Intune](apps-monitor.md) voor meer informatie over app-toewijzing en -controle.

## <a name="next-steps"></a>Volgende stappen

- [App-gegevens en -toewijzingen controleren met Microsoft Intune](apps-monitor.md)
- [Problemen met Win32-apps oplossen](apps-win32-troubleshoot.md)

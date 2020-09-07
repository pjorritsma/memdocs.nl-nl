---
title: Microsoft 365-apps toevoegen aan Windows 10-apparaten met behulp van Microsoft Intune
titleSuffix: ''
description: Meer informatie over hoe u Microsoft Intune kunt gebruiken om Microsoft 365-apps op Windows 10-apparaten te installeren.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3292671a-5f5a-429e-90f7-b20019787d22
ms.reviewer: craigma
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2242f8570a5f0ff625855bb3d31029fb4e13e3a8
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996517"
---
# <a name="add-microsoft-365-apps-to-windows-10-devices-with-microsoft-intune"></a>Microsoft 365-apps toevoegen aan Windows 10-apparaten met Microsoft Intune

Voordat u apps kunt toewijzen, controleren, configureren of beveiligen, moet u ze aan Intune toevoegen. Een van de beschikbare [app-typen](apps-add.md#app-types-in-microsoft-intune) is Microsoft 365-apps voor Windows 10-apparaten. Door dit app-type in Intune te selecteren, kunt u Microsoft 365-apps toewijzen aan en installeren op door u beheerde apparaten waarop Windows 10 wordt uitgevoerd. U kunt ook apps toewijzen en installeren voor de Microsoft Project Online-bureaubladclient en Microsoft Visio Online Plan 2, mits u daar licenties voor hebt. De beschikbare Microsoft 365-apps worden als één vermelding weergegeven in de lijst met apps in de Intune-console in Azure.

> [!NOTE]
> De naam van Microsoft Office 365 ProPlus is gewijzigd in **Microsoft 365-apps voor ondernemingen**. In onze documentatie verwijzen we er doorgaans naar met **Microsoft 365-apps**.
> 
> U moet Microsoft 365-apps-licenties gebruiken om apps van Microsoft 365-apps te activeren die via Microsoft Intune zijn geïmplementeerd. De editie Microsoft 365-apps voor ondernemingen wordt ondersteund door Intune, maar u moet de app-suite van de editie Microsoft 365-apps voor ondernemingen configureren met behulp van XML-gegevens. Zie [App-suite configureren met XML-gegevens](apps-add-office365.md#step-2---option-2-configure-app-suite-using-xml-data) voor meer informatie.

## <a name="before-you-start"></a>Voordat u begint

> [!IMPORTANT]
> Als zich op het apparaat van eindgebruiker MSI-Office-apps bevinden, moet u de functie **MSI verwijderen** gebruiken om deze apps veilig te verwijderen. Anders mislukt de installatie van de door Intune geleverde Microsoft 365-apps.

- Op de apparaten waarop u deze apps implementeert, moet de Microsoft Windows 10-makersupdate of hoger zijn geïnstalleerd.
- Intune biedt alleen ondersteuning voor het toevoegen van Office-apps uit de Microsoft 365-apps-suite.
- Als er Office-apps zijn geopend wanneer het app-pakket wordt geïnstalleerd met Intune, kan de installatie mislukken en kunnen gebruikers gegevens in niet-opgeslagen bestanden verliezen.
- Deze installatiemethode wordt niet ondersteund op apparaten met Windows Home, Windows Team, Windows Holographic of Windows Holographic for Business.
- Intune biedt geen ondersteuning voor het installeren van Microsoft 365-desktop-apps vanuit Microsoft Store (die ook wel bekend staan als Office Centennial-apps) op een apparaat waarop u al Microsoft 365-apps met Intune hebt geïmplementeerd. Als u deze configuratie installeert, kan dit leiden tot gegevensverlies of -beschadiging.
- Meerdere vereiste of beschikbare app-toewijzingen tellen niet mee. Een latere app-toewijzing overschrijft reeds bestaande geïnstalleerde app-toewijzingen. Als de eerste set met Office-apps bijvoorbeeld Word bevat maar de laatste set niet, wordt Word verwijderd. Deze voorwaarde geldt niet voor Visio- of Project-toepassingen.
- Meerdere Microsoft 365-implementaties worden momenteel niet ondersteund. Er wordt slechts één implementatie geleverd op het apparaat.
- **Office-versie**: kies of u de 32-bits of 64-bits versie van Office wilt toewijzen. U kunt de 32-bits versie op zowel 32-bits als 64-bits apparaten installeren, maar de 64-bits versie kan alleen worden geïnstalleerd op 64-bits apparaten.
- **MSI verwijderen van de apparaten van eindgebruikers**: kies of u bestaande Office MSI-apps wilt verwijderen van apparaten van eindgebruikers. De installatie mislukt als er zich bestaande MSI-apps op apparaten van eindgebruikers bevinden. De te verwijderen apps zijn niet beperkt tot de apps die zijn geselecteerd voor de installatie in **App-suite configureren**, omdat hierdoor alle Office-apps (MSI) van het apparaat van de eindgebruiker worden verwijderd. Zie [Bestaande MSI-versies van Office verwijderen bij een upgrade naar Microsoft 365-apps](/deployoffice/upgrade-from-msi-version) voor meer informatie. Wanneer u Intune Office opnieuw op de computers van uw eindgebruikers installeert, krijgen eindgebruikers automatisch dezelfde taalpakketten als bij eerdere .MSI Office installaties.

## <a name="select-microsoft-365-apps"></a>Microsoft 365-apps selecteren

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Alle apps** > **Toevoegen**.
3. Selecteer **Windows 10** in de sectie **Microsoft 365-apps** van het deelvenster **Een app-type selecteren**.
4. Klik op **Selecteren**. De stappen voor **Microsoft 365-apps toevoegen** worden weergegeven.


## <a name="step-1---app-suite-information"></a>Stap 1: Gegevens over de app-suite

In deze stap geeft u informatie op over het app-pakket. Aan de hand van deze informatie kunt u het app-pakket vinden in Intune en kunnen gebruikers het app-pakket vinden in de bedrijfsportal.

1. Op de pagina **Gegevens over de app-suite** kunt u de standaardwaarden bevestigen of wijzigen:
    - **Naam pakket**: voer de naam van het app-pakket in zoals deze wordt weergegeven in de bedrijfsportal. Zorg ervoor dat alle pakketnamen die u gebruikt, uniek zijn. Als dezelfde naam van een app-pakket twee keer voorkomt, wordt slechts één van de apps weergegeven voor gebruikers in de bedrijfsportal.
    - **Beschrijving pakket**: voer een beschrijving in voor het app-pakket. Hier kunt u bijvoorbeeld de apps vermelden die in het pakket zijn opgenomen.
    - **Uitgever**: Microsoft wordt weergegeven als de uitgever.
    - **Categorie**: selecteer een of meer ingebouwde app-categorieën of een categorie die u hebt gemaakt (optioneel). Met deze instellingen kunnen gebruikers het app-pakket gemakkelijker vinden wanneer ze door de bedrijfsportal bladeren.
    - **Deze weergeven als aanbevolen app in de bedrijfsportal**: Selecteer deze optie om het app-pakket prominent weer te geven op de hoofdpagina van de bedrijfsportal wanneer gebruikers naar apps bladeren.
    - **Informatie-URL**: Voer de URL in van een website die informatie over deze app bevat (optioneel). De URL wordt weergegeven voor gebruikers in de bedrijfsportal.
    - **Privacy-URL**: (optioneel) Voer de URL in van een website die privacyinformatie over deze app bevat. De URL wordt weergegeven voor gebruikers in de bedrijfsportal.
    - **Ontwikkelaar**: Microsoft wordt weergegeven als de ontwikkelaar.
    - **Eigenaar**: Microsoft wordt weergegeven als de eigenaar.
    - **Opmerkingen**: voer de opmerkingen in die u aan deze app wilt koppelen.
    - **Logo**: het logo van Microsoft 365-apps wordt samen met de app weergegeven wanneer gebruikers door de bedrijfsportal bladeren.
2. Klik op **Volgende** om de pagina **App-suite configureren** weer te geven.

## <a name="step-2---option-1-configure-app-suite-using-the-configuration-designer"></a>Stap 2: (**optie 1**) App-suite configureren met behulp van de Configuration Designer 

U kunt een methode kiezen voor het configureren van appinstellingen door een **Indeling van de configuratie-instellingen** te selecteren. De volgende indelingsopties voor instellingen zijn beschikbaar:
- Configuration Designer
- XML-gegevens invoeren

Wanneer u **Configuratie-ontwerper** kiest, worden in het deelvenster **App toevoegen** drie extra instellingsgebieden weergegeven:
- De app-suite configureren
- Gegevens over de app-suite
- Eigenschappen

<img alt="Add Microsoft 365 Apps - Configuration designer" src="./media/apps-add-office365/apps-add-office365-02.png" width="700">

1. Kies op de pagina **Configuratie van de app-suite** de optie **Configuratie-ontwerper**.
   - **Selecteer Office-apps**: selecteer de standaard-apps van Office die u wilt toewijzen aan apparaten door de apps in de vervolgkeuzelijst te kiezen.
   - **Selecteer andere Office-apps (licentie vereist)** : selecteer de aanvullende apps van Office die u wilt toewijzen aan apparaten en waarvoor u een licentie hebt door de apps in de vervolgkeuzelijst te kiezen. Deze apps bevatten gelicentieerde apps, zoals Microsoft Project Online Desktop Client en Microsoft Visio Online Plan 2.
   - **Architectuur**: kies of u de **32-bits** of **64-bits** versie van Microsoft 365-apps wilt toewijzen. U kunt de 32-bits versie op zowel 32-bits als 64-bits apparaten installeren, maar de 64-bits versie kan alleen worden geïnstalleerd op 64-bits apparaten.
    - **Updatekanaal**: kies hoe Office moet worden bijgewerkt op apparaten. Zie [Overzicht van updatekanalen voor Microsoft 365-apps voor bedrijven](/DeployOffice/overview-of-update-channels-for-office-365-proplus) voor meer informatie over de verschillende updatekanalen. U kunt kiezen uit:
        - **Maandelijks**
        - **Maandelijks (gericht)**
        - **Halfjaarlijks**
        - **Halfjaarlijks (gericht)**

        Nadat u een kanaal hebt gekozen, kunt u het volgende kiezen:
        - **Andere versies**verwijderen: kies **Ja** om andere versies van Office (MSI) van gebruikersapparaten te verwijderen. Kies deze optie als u bestaande Office MSI-apps wilt verwijderen van apparaten van eindgebruikers. De installatie mislukt als er zich bestaande MSI-apps op apparaten van eindgebruikers bevinden. De te verwijderen apps zijn niet beperkt tot de apps die zijn geselecteerd voor de installatie in **App-suite configureren**, omdat hierdoor alle Office-apps (MSI) van het apparaat van de eindgebruiker worden verwijderd. Zie [Bestaande MSI-versies van Office verwijderen bij een upgrade naar Microsoft 365-apps](/deployoffice/upgrade-from-msi-version) voor meer informatie. Wanneer u Intune Office opnieuw op de computers van uw eindgebruikers installeert, krijgen eindgebruikers automatisch dezelfde taalpakketten als bij eerdere .MSI Office installaties. 
        - **Versie die moet worden geïnstalleerd**: kies de Office-versie die moet worden geïnstalleerd.
        - **Specifieke versie**: als u **Specifiek** hebt gekozen als **Versie die moet worden geïnstalleerd** in de bovenstaande instelling, kunt u ervoor kiezen om een specifieke versie van Office te installeren voor het geselecteerde kanaal op apparaten van eindgebruikers. 
            
            Welke versies er beschikbaar zijn, verandert in de loop van de tijd. Daarom is het mogelijk dat er bij het maken van een nieuwe implementatie nieuwere versies beschikbaar zijn en dat bepaalde oudere versies niet meer beschikbaar zijn. Huidige implementaties blijven de oudere versie implementeren, maar de versielijst wordt voortdurend per kanaal bijgewerkt.
            
            Voor apparaten waarop de vastgemaakte versie wordt bijgewerkt (of andere eigenschappen worden bijgewerkt) en die worden geïmplementeerd als beschikbaar, wordt de rapportagestatus weergegeven als Geïnstalleerd als ze de vorige versie hebben geïnstalleerd, totdat het apparaat wordt ingecheckt. Als het apparaat wordt ingecheckt, wordt tijdelijk de status gewijzigd in Onbekend, maar dit wordt niet aan de gebruiker weergegeven. Wanneer de gebruiker met de installatie van de later beschikbaar gekomen versie begint, ziet de gebruiker dat de status wordt gewijzigd in Geïnstalleerd.
            
            Zie [Overzicht van updatekanalen voor Microsoft 365-apps](/DeployOffice/overview-of-update-channels-for-office-365-proplus) voor meer informatie.
    - **Activering van gedeelde computers gebruiken**: selecteer deze optie wanneer meerdere gebruikers een computer delen. Zie [Overzicht van activering van gedeelde computers voor Microsoft 365-apps](/DeployOffice/overview-of-shared-computer-activation-for-office-365-proplus) voor meer informatie.
    - **Gebruiksrechtovereenkomst voor eindgebruikers van de app automatisch accepteren**: selecteer deze optie als het voor eindgebruikers niet vereist is om de gebruiksrechtovereenkomst te accepteren. Intune accepteert de overeenkomst automatisch.
    - **Talen**: Office wordt automatisch geïnstalleerd in de ondersteunde talen die met Windows zijn geïnstalleerd op het apparaat van de eindgebruiker. Selecteer deze opties als u aanvullende talen wilt installeren met het app-pakket. <p></p>
        U kunt aanvullende talen implementeren voor Microsoft 365-apps die via Intune worden beheerd. De lijst met beschikbare talen bevat het taalpakket **Type** (kern, gedeeltelijk en spellingcontrole). Selecteer in Azure Portal **Microsoft Intune** > **Apps** > **Alle apps** > **Toevoegen**. In de lijst **App-type** in et deelvenster **App toevoegen** selecteert u **Windows 10** onder **Microsoft 365-apps**. Selecteer **Talen** in het deelvenster **Instellingen voor app-suite**. Zie voor meer informatie het [overzicht van de implementatie van talen in Microsoft 365-apps](/deployoffice/overview-of-deploying-languages-in-office-365-proplus).
2. Klik op **Volgende** om de pagina **Bereiktags** weer te geven.

## <a name="step-2---option-2-configure-app-suite-using-xml-data"></a>Stap 2: (**optie 2**) App-suite configureren met XML-gegevens 

Als u de optie **XML-gegevens invoeren** hebt geselecteerd onder de vervolgkeuzelijst **Instellingsindeling** op de pagina **App-suite configureren**, kunt u de Office-app-suite configureren met behulp van een aangepast configuratiebestand.

![Office 365 Configuration Designer toevoegen](./media/apps-add-office365/apps-add-office365-01.png)

1. De configuratie-XML is toegevoegd.

    > [!NOTE]
    > De product-id kan Business (`O365BusinessRetail`) of ProPlus (`O365ProPlusRetail`) zijn. U kunt de app-suite van de editie Microsoft 365-apps voor ondernemingen echter alleen configureren met behulp van XML-gegevens. Zoals u ziet is de naam van Microsoft Office 365 ProPlus gewijzigd in **Microsoft 365-apps voor ondernemingen**.

2. Klik op **Volgende** om de pagina **Bereiktags** weer te geven.

Raadpleeg [Configuratie-opties voor het Office-implementatieprogramma](/DeployOffice/configuration-options-for-the-office-2016-deployment-tool) voor meer informatie over het invoeren van XML-gegevens.

## <a name="step-3---select-scope-tags-optional"></a>Stap 3: Bereiktags selecteren (optioneel)
U kunt bereiktags gebruiken om te bepalen wie er informatie over client-apps mag bekijken in Intune. Zie [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Op rollen gebaseerd toegangsbeheer en bereiktags gebruiken voor gedistribueerde IT) voor uitgebreide informatie over bereiktags.

1. Klik op **Bereiktags selecteren** om desgewenst bereiktags toe te voegen voor de app-suite.
2. Klik op **Volgende** om de pagina **Toewijzingen** weer te geven.

## <a name="step-4---assignments"></a>Stap 4: toewijzingen

1. Selecteer de groepstoewijzingen **Vereist**, **Beschikbaar voor ingeschreven apparaten** of **Verwijderen** voor de app-suite. Zie [Groepen toevoegen om gebruikers en apparaten in te delen](../fundamentals/groups-add.md) en [Apps toewijzen aan groepen met Microsoft Intune](apps-deploy.md) voor meer informatie.
2. Klik op **Volgende** om naar de pagina **Controleren en maken** weer te geven.

## <a name="step-5---review--create"></a>Stap 5: beoordelen en maken

1. Controleer de waarden en instellingen die u hebt ingevoerd voor de app-suite.
2. Klik als u klaar bent op **Maken** om de app toe te voegen aan Intune.

    De blade **Overzicht** wordt weergegeven.

## <a name="deployment-details"></a>Implementatiedetails

Nadat het implementatiebeleid van Intune is toegewezen aan de doelmachines via de [Office-configuratieserviceprovider (CSP)](/windows/client-management/mdm/office-csp), downloadt het eindapparaat automatisch het installatiepakket van de locatie *officecdn.microsoft.com*. U ziet twee nieuwe mappen in de map *Program Files*:

![Office-installatiepakketten in de map Program Files](./media/apps-add-office365/office-folder.png)

Onder de map *Microsoft Office* wordt een nieuwe map gemaakt waarin de installatiebestanden worden opgeslagen:

![Nieuwe map gemaakt onder Microsoft Office-directory](./media/apps-add-office365/created-folder.png)

Onder de map *Microsoft Office 15* worden de Klik-en-Klaar-opstartbestanden voor het installeren van Office opgeslagen. De installatie wordt automatisch gestart als het toewijzingstype vereist is:

![Klik-en-Klaar-opstartbestanden voor installatie](./media/apps-add-office365/clicktorun-files.png)

De installatie wordt uitgevoerd in de stille modus als de toewijzing van Microsoft 365 is geconfigureerd als vereist. De gedownloade installatiebestanden worden verwijderd zodra de installatie is voltooid. Als de toewijzing is geconfigureerd als **Beschikbaar**, worden de Office-toepassingen weergegeven in de Bedrijfsportal-toepassing, zodat eindgebruikers de installatie handmatig kunnen starten.

## <a name="troubleshooting"></a>Probleemoplossing
Intune gebruikt het [Office-implementatiehulpprogramma](/DeployOffice/overview-of-the-office-2016-deployment-tool) om Office 365 ProPlus te downloaden en op uw clientcomputers te implementeren met de [Office 365 CDN](/office365/enterprise/content-delivery-networks). Bekijk de best practices die worden vermeld in [Office 365-eindpunten beheren](/office365/enterprise/managing-office-365-endpoints), om ervoor te zorgen dat uw netwerkconfiguratie toestaat dat clients rechtstreeks toegang hebben tot CDN, in plaats van dat CDN-verkeer door centrale proxy's wordt geleid. Zo voorkomt u onnodige latentie.

Voer de [Microsoft-ondersteunings- en herstelassistent voor Microsoft 365](https://diagnostics.office.com) uit op een doelapparaat als u tijdens de installatie of uitvoering problemen ondervindt.

### <a name="additional-troubleshooting-details"></a>Aanvullende gegeven voor het oplossen van problemen

Als u de Microsoft 365-apps niet op een apparaat kunt installeren, moet u vaststellen of het probleem verband houdt met Intune of met het besturingssysteem of Office. Als de twee mappen *Microsoft Office* en *Microsoft Office 15* worden weergegeven in de map *Program Files* map van het apparaat, kunt u bevestigen dat Intune de implementatie met succes heeft gestart. Als u de twee mappen niet ziet verschijnen onder *Program Files*, moet u de onderstaande gevallen bevestigen:

- Het apparaat is goed ingeschreven bij Microsoft Intune. 
- Er is een actieve netwerkverbinding met het apparaat. Als het apparaat zich in de vliegtuigmodus bevindt, is uitgeschakeld of zich op een locatie zonder service bevindt, wordt het beleid pas toegepast nadat de netwerkverbinding tot stand is gebracht.
- Aan de netwerkvereisten voor zowel Intune als Microsoft 365 is voldaan en de bijbehorende IP-bereiken zijn toegankelijk op basis van de volgende artikelen:

  - [Netwerkconfiguratievereisten en bandbreedte voor Intune](/intune/network-bandwidth-use)
  - [Office 365-URL's en IP-adresbereiken](/office365/enterprise/urls-and-ip-address-ranges)

- Het Microsoft 365-app-pakket is toegewezen aan de juiste groepen. 

Controleer bovendien de grootte van de directory *C:\Program Files\Microsoft Office\Updates\Download*. Het van de Intune-cloud gedownloade installatiepakket wordt opgeslagen op deze locatie. Als de grootte niet of erg langzaam toeneemt, is het raadzaam om de netwerkverbinding en bandbreedte te controleren.

Wanneer u kunt concluderen dat zowel Intune als de netwerkinfrastructuur naar verwachting werken, moet u het probleem verder analyseren vanuit besturingssysteemperspectief. Houd rekening met de volgende voorwaarden:

- Het doelapparaat moet werken met Windows 10-makersupdate of hoger.
- Er zijn geen bestaande Office-apps geopend terwijl Intune de toepassingen implementeert.
- Bestaande MSI-versies van Office zijn op de juiste wijze verwijderd van het apparaat. Intune maakt gebruik van Office Klik-en-klaar, dat niet compatibel is met Office MSI. Dit gedrag wordt verder beschreven in dit document:<br>
  [Office op dezelfde computer geïnstalleerd met Klik-en-Klaar en met Windows Installer wordt niet ondersteund](https://support.office.com/article/office-installed-with-click-to-run-and-windows-installer-on-same-computer-isn-t-supported-30775ef4-fa77-4f47-98fb-c5826a6926cd)
- De aanmeldingsgebruiker moet gemachtigd zijn om toepassingen op het apparaat te installeren.
- Bevestig dat er geen problemen zijn op basis van de Windows-Logboeken **Windows-logboeken** -> **Toepassingen**.
- Leg tijdens de installatie uitgebreide Office-installatielogboeken vast. Volg hiervoor de volgende stappen:<br>
    1. Schakel uitgebreide logboekregistratie voor Office-installatie in op de doelcomputers. Hiervoor voert u de volgende opdracht uit om het register te wijzigen:<br>
        `reg add HKLM\SOFTWARE\Microsoft\ClickToRun\OverRide /v LogLevel /t REG_DWORD /d 3`<br>
    2. Implementeer Microsoft 365-apps opnieuw op de doelapparaten.<br>
    3. Wacht ongeveer 15 tot 20 minuten en ga naar de map **%temp%** en de map **%windir%\temp**, sorteer op **Gewijzigd op** en kies de *{machinenaam}-{tijdstempel}.log*-bestanden die zijn gewijzigd op basis van uw reproductietijdstip.<br>
    4. Schakel de uitgebreide logboekregistratie weer uit met de volgende opdracht:<br>
        `reg delete HKLM\SOFTWARE\Microsoft\ClickToRun\OverRide /v LogLevel /f`<br>
        De uitgebreide logboeken kunnen meer gedetailleerde informatie bieden over het installatieproces.

## <a name="errors-during-installation-of-the-app-suite"></a>Fouten tijdens de installatie van het app-pakket

Raadpleeg [ULS-logboekregistratie in Microsoft 365-apps inschakelen](/office/troubleshoot/diagnostic-logs/how-to-enable-office-365-proplus-uls-logging) voor informatie over hoe u uitgebreide installatielogboeken bekijkt.

In de volgende tabellen worden algemene foutcodes en hun betekenis weergegeven.

### <a name="status-for-office-csp"></a>Status voor Office CSP

| Status | Fase | Beschrijving |
|--------------------------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1460 (ERROR_TIMEOUT) | Download | Het downloaden van de Office Deployment Tool is mislukt |
| 13 (ERROR_INVALID_DATA) | - | De handtekening van de gedownloade Office Deployment Tool kan niet worden geverifieerd |
| Foutcode van CertVerifyCertificateChainPolicy | - | De certificeringscontrole van de gedownloade Office Deployment Tool is mislukt |
| 997 | WIP | Wordt geïnstalleerd |
| 0 | Na de installatie | Installatie voltooid |
| 1603 (ERROR_INSTALL_FAILURE) | - | Controle van vereisten is mislukt, zoals SxS (Er is geprobeerd te installeren terwijl 2016 MSI is geïnstalleerd)Versie komt niet overeenOverige |
| 0x8000ffff (E_UNEXPECTED) | - | Er is geprobeerd te verwijderen zonder Office Klik-en-Klaar op de machine |
| 17002 | - | Het scenario (installatie) kan niet worden voltooid. Mogelijke redenen:Installatie geannuleerd door gebruikerInstallatie geannuleerd door een andere installatieOnvoldoende schijfruimte tijdens installatieOnbekende taal-ID |
| 17004 | - | Onbekende SKU’s |


### <a name="office-deployment-tool-error-codes"></a>Office Deployment Tool-foutcodes

| Scenario | Retourcode | Gebruikersinterface | Opmerking |
|------------------------------------------------------------------------------------------------------------------|---------------------------------------|----------------------------------------------------|------------------------------------|
| Er is geprobeerd de installatie te verwijderen zonder actieve Klik-en-Klaar-installatie | -2147418113, 0x8000ffff of 2147549183 | Foutcode: 30088-1008Foutcode: 30125-1011 (404) | Office Deployment Tool |
| Installeren terwijl de MSI-versie is geïnstalleerd | 1603 | - | Office Deployment Tool |
| De installatie is geannuleerd door de gebruiker of door een andere installatie | 17002 | - | Klik-en-Klaar |
| Er is geprobeerd een 64-bits versie te installeren op een apparaat waarop de 32-bits versie is geïnstalleerd. | 1603 | - | Retourcodes Office Deployment Tool |
| Er is geprobeerd een onbekende SKU te installeren (dit is geen geldige use case voor Office CSP omdat er alleen geldige SKU’s mogen worden doorgegeven) | 17004 | - | Klik-en-Klaar |
| Gebrek aan ruimte | 17002 | - | Klik-en-Klaar |
| Kan de Klik-en-Klaar-client niet starten (onverwacht) | 17000 | - | Klik-en-Klaar |
| De Klik-en-Klaar-client kan het scenario niet in de wachtrij zetten (onverwacht) | 17001 | - | Klik-en-Klaar |

## <a name="next-steps"></a>Volgende stappen

- Zie [Apps toewijzen aan groepen](./apps-deploy.md) als u de app-suite aan extra groepen wilt toewijzen.
---
title: Technical Preview 1705
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview-versie 1705 voor Configuration Manager.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0a10726062d679666d14cbbb0b87510af5dfe30c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078801"
---
# <a name="capabilities-in-technical-preview-1705-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1705 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1705. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md) om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    

**Bekende problemen in deze technische preview:**
-   **Operations Manager Suite connector wordt niet bijgewerkt**. Wanneer u een upgrade uitvoert van een eerdere versie van de Technical Preview waarvoor de OMS-connector is geconfigureerd, wordt die connector niet bijgewerkt en is deze niet meer beschikbaar in de-console. Na de upgrade moet u [de wizard Azure-Services gebruiken](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) en opnieuw verbinding maken met uw OMS-werk ruimte.
-   **Er kunnen geen Surface-Stuur Programma's worden gesynchroniseerd**. Hoewel ondersteuning voor Surface-Stuur Programma's wordt weer gegeven in **Wat is er nieuw** in de Configuration Manager-console voor de Technical Preview, werkt deze functie nog niet zoals verwacht.
-   **Kan geen Windows Update maken voor bedrijfs beleid voor uitstel**. Hoewel de mogelijkheid om Windows Update voor bedrijfs uitstel beleid te configureren wordt weer gegeven in **wat** is er nieuw in de Configuration Manager-console voor de Technical Preview, wordt de wizard niet geopend en kunt u geen beleids regels configureren.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Hulpprogramma voor het opnieuw instellen van updates  
U kunt het hulp programma Configuration Manager Update reset, **CMUpdateReset. exe**, gebruiken om problemen op te lossen wanneer de updates in de console problemen ondervinden of repliceren. Dit hulp programma is opgenomen in Technical Preview versie 1705. U kunt het vinden op de site server van uw Technical Preview-site nadat u de preview-versie hebt geïnstalleerd in de map ***\Cd.latest\SMSSETUP\TOOLS*** .

U kunt dit hulp programma gebruiken met Technical Preview versie 1606 of hoger. Deze neerwaartse ondersteuning wordt geboden zodat het hulp programma kan worden gebruikt met een aantal Technical Preview-update scenario's en zonder te hoeven wachten tot de volgende Technical Preview beschikbaar is.

U kunt dit hulp programma gebruiken wanneer een update in de console nog niet is geïnstalleerd en zich in een mislukte status bevindt. Een mislukte status kan betekenen dat het downloaden van de update nog wordt uitgevoerd, maar vastloopt en een buitensporig lange tijd in beslag neemt, mogelijk uur langer dan uw historische verwachtingen voor update pakketten van een vergelijk bare grootte. Het kan ook een fout zijn bij het repliceren van de update op onderliggende primaire sites.  

Wanneer u het hulp programma uitvoert, wordt het uitgevoerd op basis van de update die u opgeeft. Het hulp programma heeft standaard de installatie of gedownloade updates niet verwijderd.  

### <a name="prerequisites"></a>Vereisten
Het account dat u gebruikt om het hulp programma uit te voeren, vereist de volgende machtigingen:
-   **Lees** -en **Schrijf** machtigingen voor de site database van de centrale beheer site en elke primaire site in uw hiërarchie. Als u deze machtigingen wilt instellen, kunt u het gebruikers account toevoegen als lid van de **db_datawriter** en **db_datareader** [vaste database rollen](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) op de Configuration Manager-Data Base van elke site. Het hulp programma heeft geen interactie met secundaire sites.
-   **Lokale beheerder** op de site op het hoogste niveau van uw hiërarchie.
-   **Lokale beheerder** op de computer die het service verbindings punt host.

U hebt de GUID van het update pakket nodig die u opnieuw wilt instellen. De GUID ophalen:
-   Ga in de-console naar **beheer** > **updates en onderhoud** en klik vervolgens in het weergave paneel met de rechter muisknop op de kop van een van de kolommen (zoals **status**) en selecteer vervolgens **pakket-GUID**. Hiermee voegt u die kolom toe aan het weer geven en toont de kolom de GUID van het update pakket.

> [!TIP]  
> Als u de GUID wilt kopiëren, selecteert u de rij voor het update pakket dat u opnieuw wilt instellen en gebruikt u vervolgens CTRL + C om die rij te kopiëren. Als u de gekopieerde selectie in een tekst editor plakt, kunt u vervolgens alleen de GUID kopiëren voor gebruik als een opdracht regel parameter wanneer u het hulp programma uitvoert.

### <a name="run-the-tool"></a>Het hulp programma uitvoeren    
Het hulp programma moet worden uitgevoerd op de site op het hoogste niveau van de hiërarchie.

Wanneer u het hulp programma uitvoert, gebruikt u opdracht regel parameters om de SQL Server op de site op het hoogste niveau van de hiërarchie, de naam van de site database en de GUID van het update pakket op te geven die u opnieuw wilt instellen. Het hulp programma identificeert vervolgens de extra servers die moeten worden geopend, op basis van de update status.   

Als het update pakket een status *na het downloaden* heeft, wordt het pakket niet opgeschoond met het hulp programma. Als optie kunt u het verwijderen van een geslaagde Update afdwingen met behulp van de para meter Force Delete (Zie opdracht regel parameters verderop in dit onderwerp).

Wanneer het hulp programma wordt uitgevoerd:
-   Als een pakket is verwijderd, start u de sites op het hoogste niveau SMS_Executive service opnieuw op en controleert u vervolgens op updates om het pakket opnieuw te downloaden.
-   Als een pakket niet is verwijderd, hoeft u geen actie te ondernemen omdat de update de replicatie of installatie opnieuw moet initialiseren en opnieuw starten.

**Opdracht regel parameters:**  


|                        Parameter                         |                                                            Beschrijving                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;FQDN van de SQL Server van uw site op het hoogste niveau>** | *Vereist* <br> U moet de FQDN opgeven van de SQL Server die als host fungeert voor de site database voor de bovenste site van uw hiërarchie. |
|                **-D &lt;Database naam>**                 |                             *Vereist* <br> U moet de naam van de data base van de bovenste site opgeven.                             |
|                 **-P &lt;Package GUID>**                 |                        *Vereist* <br> U moet de GUID opgeven voor het update pakket dat u opnieuw wilt instellen.                        |
|           **-I &lt;SQL Server exemplaar naam>**           |                   *Beschrijving* <br> Hier kunt u het exemplaar van SQL Server identificeren dat als host fungeert voor de site database.                   |
|                       **-FDELETE**                       |                      *Beschrijving* <br> Gebruik deze om het verwijderen van een geslaagd update pakket af te dwingen.                      |

 **Voorbeelden:**  
 In een typisch scenario wilt u een update met Download problemen opnieuw instellen. De FQDN van de SQL-servers is *Server1.fabrikam.com*, de site database is *CM_XYZ*en de pakket-GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  U voert de volgende handelingen uit: ***CMUpdateReset. exe-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 In een meer extreme scenario wilt u het verwijderen van problematische update pakketten afdwingen. De FQDN van de SQL-servers is *Server1.fabrikam.com*, de site database is *CM_XYZ*en de pakket-GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  U voert de volgende handelingen uit: ***CMUpdateReset. exe-FDELETE-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Het hulp programma testen met de Technical Preview  
U kunt dit hulp programma gebruiken met Technical Preview versie 1606 of hoger. Deze achterwaartse ondersteuning wordt geboden zodat het hulp programma kan worden gebruikt met een groter aantal Technical Preview-update scenario's, zonder dat u hoeft te wachten tot de volgende Technical Preview-versie beschikbaar is.

Voer het hulp programma uit op een update pakket voor een technische preview voordat deze update de vereiste controle heeft voltooid. De status van een voltooide controle op vereisten wordt aangeduid met een van de volgende statussen voor het pakket in **beheer** > **updates en onderhoud**:  
-   **Het controleren van vereisten is voltooid**
-   **Het controleren van vereisten is voltooid met een waarschuwing**
-   **Controleren van vereisten is mislukt**


## <a name="high-dpi-console-support"></a>Ondersteuning voor hoge DPI-console

In deze release moeten problemen worden opgelost met de manier waarop de Configuration Manager-console wordt geschaald en de verschillende onderdelen van de gebruikers interface worden weer gegeven wanneer deze worden weer gegeven op hoge DPI-apparaten (zoals een Surface Book).


## <a name="peer-cache-improvements"></a>Verbeteringen in de peer-cache
Vanaf deze Technical Preview gebruikt peer-cache [niet langer het netwerk toegangs account](../plan-design/hierarchy/client-peer-cache.md) om download aanvragen van peers te verifiëren.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Verbeteringen voor SQL Server AlwaysOn-beschikbaarheids groepen  
Met deze versie kunt u nu asynchrone doorvoer replica's gebruiken in de SQL Server AlwaysOn-beschikbaarheids groepen die u gebruikt met Configuration Manager.  Dit betekent dat u extra replica's aan uw beschikbaarheids groepen kunt toevoegen om te gebruiken als externe back-ups, en ze vervolgens te gebruiken in een nood herstel scenario.  

- Configuration Manager ondersteunt het gebruik van de asynchrone doorvoer replica om uw synchrone replica te herstellen.  Zie [Opties voor herstel van de site database](../servers/manage/recover-sites.md#site-database-recovery-options) in het onderwerp back-up en herstel voor informatie over hoe u dit kunt doen.

- Deze release biedt geen ondersteuning voor failover voor het gebruik van de asynchrone doorvoer replica als uw site database.
  > [!CAUTION]  
  > Omdat Configuration Manager de status van de asynchrone doorvoer replica niet valideert om te bevestigen dat deze actueel is, en [door het ontwerp van een dergelijke replica niet kan worden gesynchroniseerd](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), kunt u het gebruik van een asynchrone doorvoer replica, omdat de site database de integriteit van uw site en gegevens mogelijk maakt.  

- U kunt hetzelfde aantal en type replica's in een beschikbaarheids groep gebruiken, zoals wordt ondersteund door de versie van SQL Server die u gebruikt.   (Eerdere ondersteuning is beperkt tot twee synchroon door Voer-replica's.)

### <a name="configure-an-asynchronous-commit-replica"></a>Een asynchrone doorvoer replica configureren
Als u een asynchrone replica wilt toevoegen aan een [beschikbaarheids groep die u gebruikt met Configuration Manager](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md), hoeft u de vereiste configuratie scripts voor het configureren van een synchrone replica niet uit te voeren. (Dit komt doordat er geen ondersteuning is voor het gebruik van deze asynchrone replica als de site database.) Raadpleeg [de SQL Server-documentatie](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) voor informatie over het toevoegen van secundaire replica's aan beschikbaarheids groepen.

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>De asynchrone replica gebruiken om uw site te herstellen
Voordat u een asynchrone replica gebruikt om de site database te herstellen, moet u de actieve primaire site stoppen om te voor komen dat er extra schrijf bewerkingen naar de site database worden uitgevoerd. Nadat u de site hebt gestopt, kunt u een asynchrone replica gebruiken in plaats van een [hand matig herstelde data base](../servers/manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered)te gebruiken.

Als u de site wilt stoppen, kunt u het [hulp programma voor hiërarchie onderhoud](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md) gebruiken om de belangrijkste services op de site server te stoppen. Gebruik de opdracht regel: **preinst. exe/stopsite**   

Het stoppen van de site is gelijk aan het stoppen van de Site Component Manager-service (sitecomp), gevolgd door de SMS_Executive-service op de site server.


## <a name="improved-user-notifications-for-office-365-updates"></a>Verbeterde gebruikers meldingen voor Office 365-updates
Er zijn verbeteringen aangebracht in het gebruik van de Office-klik-en-klaar-gebruikers ervaring wanneer een client een update van Office 365 installeert. Dit omvat pop-up-en in-app-meldingen en een aftellings ervaring. Voordat deze release werd uitgebracht toen een Office 365-update werd verzonden naar een client, werden Office-toepassingen die zijn geopend, automatisch gesloten zonder dat er een waarschuwing wordt weer gegeven. Na deze update worden Office-toepassingen niet meer onverwacht gesloten.

### <a name="prerequisites"></a>Vereisten
Deze update is van toepassing op Office 365 ProPlus-clients.

### <a name="known-issues"></a>Bekende problemen
Wanneer een client een update toewijzing voor Office 365 voor de eerste keer evalueert en de update een deadline heeft gepland, direct wordt gepland of is gepland binnen 30 minuten, kan de gebruikers ervaring van Office 365 inconsistent zijn. De client kan bijvoorbeeld een dialoog venster voor het aftellen van 30 minuten ontvangen voor de update, maar de werkelijke afdwinging kan beginnen vóór het einde van de aftelling. Houd rekening met het volgende om dit gedrag te voor komen:
- Implementeer de Office 365-update met een deadline die meer dan 60 minuten vóór de huidige tijd is gepland.
- Een onderhouds venster configureren tijdens niet-kantoor uren op de verzameling of een respijt periode voor afdwinging configureren voor de implementatie.

### <a name="try-it-out"></a>Probeer het nu!
Voer de volgende taken uit en stuur ons **feedback** via het tabblad **Start** van het lint om ons te laten weten hoe het werkt:
- Implementeren op een client een update van Office 365 waarbij een deadline is ingesteld op een tijd van ten minste 60 minuten vóór de huidige tijd. Bekijk het nieuwe gedrag op de client.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Windows Defender Application Guard-beleid configureren en implementeren

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) is een nieuwe Windows-functie waarmee u uw gebruikers kunt beschermen door niet-vertrouwde websites te openen in een beveiligde geïsoleerde container die niet toegankelijk is voor andere onderdelen van het besturings systeem. In deze Technical Preview hebt u ondersteuning toegevoegd om deze functie te configureren met behulp van Configuration Manager nalevings instellingen die u configureert, en vervolgens implementeert u deze in een verzameling.
Deze functie wordt uitgebracht als Preview voor de 64-bits versie van de update van Windows 10 Maker. Als u deze functie nu wilt testen, moet u een preview-versie van deze update gebruiken.


### <a name="before-you-start"></a>Voordat u begint

Als u Windows Defender Application Guard-beleid wilt maken en implementeren, moeten de Windows 10-apparaten waarop u het beleid implementeert, worden geconfigureerd met een netwerk isolatie beleid. Zie voor meer informatie het blog bericht dat later wordt verwezen.
Deze functie werkt alleen met huidige Windows 10 Insider-builds. Om het te testen, moeten uw clients een recente Windows 10 Insider-build uitvoeren.

### <a name="try-it-out"></a>Probeer het nu!

Lees het blog bericht voor meer informatie over de basis beginselen van Windows Defender Application Guard.

Een beleid maken en bladeren door de beschik bare instellingen:

1.  Kies in de Configuration Manager-console **activa en naleving**.
2.  Kies **overzicht** > **Endpoint Protection**Endpoint Protection > **Windows Defender Application Guard**in de werk ruimte **activa en naleving** .
3.  Klik op het tabblad **Start** in de groep **maken** op **Windows Defender Application Guard-beleid maken**.
4.  Als u het blog bericht als referentie wilt gebruiken, kunt u door de beschik bare instellingen bladeren en deze configureren om de functie uit te proberen.
5.  Wanneer u klaar bent, voltooit u de wizard en implementeert u het beleid op een of meer Windows 10-apparaten.

### <a name="further-reading"></a>Meer informatie

Zie [dit blog bericht]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)voor meer informatie over Windows Defender Application Guard.
Zie [dit blog bericht](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)voor meer informatie over de zelfstandige Windows Defender Application Guard-modus.




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Nieuwe mogelijkheden voor Azure AD en Cloud beheer

In deze release kunt u Cloud Services configureren voor het gebruik van Azure AD ter ondersteuning van het volgende scenario:

- De Configuration Manager-client hand matig installeren vanaf internet en deze toewijzen aan een Configuration Manager-site.
- Gebruik intune om de Configuration Manager-client te implementeren op apparaten op internet.

### <a name="advantages"></a>Voordelen

Als u Cloud Services en Azure AD gebruikt, wordt de nood zaak voor het gebruik van client verificatie certificaten verwijderd.

U kunt Azure AD-gebruikers vinden op uw site voor gebruik in verzamelingen en andere Configuration Manager bewerkingen.

### <a name="before-you-start"></a>Voordat u begint

- U moet een Azure AD-Tenant hebben.
- Op uw apparaten moet Windows 10 worden uitgevoerd en lid worden van Azure AD.  Clients kunnen naast Azure AD ook lid zijn van een domein.
- Naast de [bestaande vereisten](../plan-design/configs/site-and-site-system-prerequisites.md) voor de site systeemrol van het beheer punt, moet u er ook voor zorgen dat **ASP.net 4,5** (en eventuele andere opties die automatisch met dit systeem worden geselecteerd) zijn ingeschakeld op de computer die als host fungeert voor deze site systeemrol.
- Microsoft Intune gebruiken om de Configuration Manager-client te implementeren:
    - U moet een werkende intune-Tenant hebben (Configuration Manager en intune hoeven niet te zijn verbonden).
    - In intune hebt u een app gemaakt en geïmplementeerd die de Configuration Manager-client bevat. Zie voor meer informatie over hoe u dit doet, clients installeren op met intune MDM-beheerde Windows-apparaten.
- Configuration Manager gebruiken om de-client te implementeren:
    - Ten minste één beheer punt moet worden geconfigureerd voor de HTTPS-modus.
    - U moet een cloudbeheergateway instellen.


### <a name="set-up-the-cloud-management-gateway"></a>De cloudbeheergateway instellen

Stel de cloudbeheergateway zo in dat clients vanaf het Internet toegang hebben tot uw Configuration Manager site zonder gebruik te maken van certificaten.

In de volgende onderwerpen vindt u meer informatie over hoe u dit kunt doen:

- [Plan voor Cloud beheer gateway in Configuration Manager](../clients/manage/cmg/plan-cloud-management-gateway.md).
- [Stel de Cloud beheer gateway in voor Configuration Manager](../clients/manage/cmg/setup-cloud-management-gateway.md).
- [Controleer de Cloud beheer gateway in Configuration Manager](../clients/manage/cmg/monitor-clients-cloud-management-gateway.md).

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>De Azure Services-app instellen in Configuration Manager Cloud Services

Dit verbindt uw Configuration Manager-site met Azure AD en is een vereiste voor alle andere bewerkingen in deze sectie. Om dit te doen:

1. Vouw in de werk ruimte **beheer** van de Configuration Manager-console **Cloud Services**uit en klik vervolgens op **Azure-Services**.
2. Klik op het tabblad **Start** in de groep **Azure-Services** op **Azure-Services configureren**.
3. Selecteer op de pagina **Azure-Services** van de wizard Azure-Services **Cloud beheer** om clients toe te staan met de hiërarchie te verifiëren met behulp van Azure AD.
4. Geef op de pagina **Algemeen** van de wizard een naam en een beschrijving op voor uw Azure-service.
5. Selecteer op de pagina **app** van de wizard uw Azure-omgeving in de lijst en klik vervolgens op **Bladeren** om de server-en client-apps te selecteren die worden gebruikt voor het configureren van de Azure-service:
   - Selecteer in het venster van de **server-app** de server-app die u wilt gebruiken en klik vervolgens op **OK**. Server-apps zijn de Azure-web-apps die de configuraties voor uw Azure-account bevatten, inclusief uw Tenant-ID, client-ID en een geheime sleutel voor clients. Als er geen beschik bare server-app is, gebruikt u een van de volgende opties:
       - **Maken**: als u een nieuwe server-app wilt maken, klikt u op **maken**. Geef een beschrijvende naam op voor de app en de Tenant. Nadat u zich hebt aangemeld bij Azure, maakt Configuration Manager de web-app in azure voor u, met inbegrip van de client-ID en de geheime sleutel voor gebruik met de web-app. Later kunt u deze bekijken in de Azure Portal.
       - **Importeren**: als u een web-app wilt gebruiken die al in uw Azure-abonnement bestaat, klikt u op **importeren**. Geef een beschrijvende naam op voor de app en de Tenant, en geef vervolgens de Tenant-ID, de client-ID en de geheime sleutel op voor de Azure-web-app die u Configuration Manager wilt gebruiken. Nadat u de informatie hebt gecontroleerd, klikt u op **OK** om door te gaan. Deze optie is momenteel niet beschikbaar in deze technische preview.
   - Herhaal hetzelfde proces voor de client-app.

   U moet de machtiging voor het lezen van de gegevens van een *Directory* -toepassing verlenen wanneer u toepassing importeren gebruikt om de juiste machtigingen in de portal in te stellen. Als u het maken van toepassingen gebruikt, worden de machtigingen automatisch gemaakt met de toepassing, maar u moet nog wel toestemming geven voor de toepassing in de Azure Portal.
6. Schakel op de pagina **detectie** van de wizard de optie **detectie van Azure Active Directory gebruiker**in en klik vervolgens op **instellingen**.
   Configureer in het dialoog venster **instellingen van Azure AD-gebruikers detectie** een schema voor wanneer detectie plaatsvindt. U kunt ook Delta detectie inschakelen waarmee alleen nieuwe of gewijzigde accounts in azure AD worden gecontroleerd.
7. Voltooi de wizard.

U hebt uw Configuration Manager-site op dit moment verbonden met Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>De CM-client installeren vanaf internet

Voordat u begint, moet u ervoor zorgen dat de bron bestanden van de client installatie lokaal worden opgeslagen op het apparaat waarop u de client wilt installeren.
Gebruik vervolgens de instructies in [Hoe clients implementeren op Windows-computers](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual) met behulp van de volgende opdracht regel voor de installatie (Vervang de waarden in het voor beeld met uw eigen waarden):

**ccmsetup. exe/NoCrlCheck/Source: C:\CLIENT CCMHOSTNAME = SCCMPROXYCONTOSO. CLOUDAPP. NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode = HEC AADTENANTID = 780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME = contoso AADCLIENTAPPID =\<GUID> AADRESOURCEURI =<https://contososerver>**

- **/NoCrlCheck**: als uw beheer punt of Cloud beheer gateway een niet-openbaar server certificaat gebruikt, kan de client de locatie van de CRL mogelijk niet bereiken.
- **/Source**: lokale map: locatie van de client installatie bestanden.
- **CCMHOSTNAME**: de naam van uw Internet beheer punt. U kunt dit vinden door **gwmi-naam ruimte root\ccm\locationservices-klasse-SMS_ActiveMPCandidate** uit te voeren vanaf een opdracht prompt op een beheerde client.
- **SMSMP**: de naam van uw lookup-beheer punt: dit kan zich op uw intranet bevinden.
- **SMSSiteCode**: de site code van uw Configuration Manager-site.
- **AADTENANTID**, **AADTENANTNAME**: de id en de naam van de Azure AD-tenant die u aan Configuration Manager hebt gekoppeld. U kunt dit vinden door dsregcmd. exe/status uit te voeren vanaf een opdracht prompt op een aan Azure AD toegevoegd apparaat.
- **AADCLIENTAPPID**: de id van de Azure AD-client-app. Zie [Portal gebruiken om een Azure Active Directory toepassing en Service-Principal te maken die toegang hebben tot resources](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)voor meer informatie.
- **AADResourceUri**: de id-URI van de onboarded Azure ad server-app.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>De wizard Azure-Services gebruiken om een verbinding met OMS te configureren
Met ingang van de 1705 Technical Preview-versie gebruikt u de **wizard Azure-Services** om uw verbinding te configureren van Configuration Manager naar de Cloud service operations management suite (OMS). De wizard vervangt eerdere werk stromen om deze verbinding te configureren.

-   De wizard wordt gebruikt voor het configureren van Cloud Services voor Configuration Manager, zoals OMS, Windows Store voor bedrijven (WSfB) en Azure Active Directory (Azure AD).  

-   Configuration Manager maakt verbinding met OMS voor functies als Log Analytics of Upgradegereedheid.

### <a name="prerequisites-for-the-oms-connector"></a>Vereisten voor de OMS-connector
Vereisten voor het configureren van een verbinding met OMS zijn niet gewijzigd ten opzichte van de onderdelen die zijn [gedocumenteerd voor de current branch versie 1702](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm). Deze informatie wordt hier herhaald:  

-   Configuration Manager machtiging verlenen aan OMS.

-   De OMS-connector moet zijn geïnstalleerd op de computer die als host fungeert voor een [service verbindings punt](../servers/deploy/configure/about-the-service-connection-point.md) dat zich in de [online modus](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)bevindt.

-   U moet een micro soft Monitoring Agent installeren voor OMS die is geïnstalleerd op het service aansluitpunt en de OMS-connector. De agent en de OMS-connector moeten worden geconfigureerd voor gebruik van dezelfde **OMS-werk ruimte**. Zie [de agent downloaden en installeren](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) in de OMS-documentatie voor informatie over het installeren van de agent.
-   Nadat u de connector en agent hebt geïnstalleerd, moet u OMS configureren voor het gebruik van Configuration Manager gegevens. Hiervoor [importeert u Configuration Manager verzamelingen](/azure/log-analytics/log-analytics-sccm#import-collections)in de OMS-Portal.

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>De wizard Azure-Services gebruiken om de verbinding met OMS te configureren

1.  Ga in de-console naar **beheer** > **overzicht** > **Cloud Services** > **Azure-Services**en kies vervolgens **Azure-Services configureren** op het tabblad **Start** van het lint om de **wizard Azure-Services**te starten.

2.  Selecteer op de pagina **Azure-Services** de Operations Management Suite-Cloud service. Geef een beschrijvende naam op voor de naam van de **Azure-service** en een optionele beschrijving en klik vervolgens op **volgende**.

3.  Geef uw Azure-omgeving op de pagina **app** op (de Technical Preview ondersteunt alleen de open bare Cloud). Klik vervolgens op **Bladeren** om het venster Server toepassing te openen.

4.  Een web-app selecteren:

    -   **Importeren**: als u een web-app wilt gebruiken die al in uw Azure-abonnement bestaat, klikt u op **importeren**. Geef een beschrijvende naam op voor de app en de Tenant, en geef vervolgens de Tenant-ID, de client-ID en de geheime sleutel op voor de Azure-web-app die u Configuration Manager wilt gebruiken. Nadat u de informatie hebt **gecontroleerd** , klikt u op **OK** om door te gaan.   

    > [!NOTE]   
    > Wanneer u OMS configureert met deze preview, ondersteunt OMS alleen de functie *import* voor een web-app. Het maken van een nieuwe web-app wordt niet ondersteund. Op dezelfde manier kunt u een bestaande app niet opnieuw gebruiken voor OMS.

5.  Als u alle andere procedures hebt uitgevoerd, wordt de informatie in het configuratie scherm voor de **OMS-verbinding** automatisch weer gegeven op deze pagina. Gegevens voor de verbindings instellingen moeten worden weer gegeven voor uw **Azure-abonnement**, **Azure-resource groep**en **Operations Management Suite-werk ruimte**.

6.  De wizard maakt verbinding met de OMS-service met de informatie die u hebt ingevoerd. Selecteer de apparaatsets die u wilt synchroniseren met OMS en klik vervolgens op **toevoegen**.

7.  Controleer uw Verbindings instellingen op het scherm **samen vatting** en selecteer vervolgens **volgende**. Het scherm **voortgang** toont de verbindings status en moet vervolgens worden **voltooid**.

8.  Nadat de wizard is voltooid, ziet u in de Configuration Manager-console dat u **Operation Management Suite** hebt geconfigureerd als een **type Cloud service**.

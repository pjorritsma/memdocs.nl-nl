---
title: Waarschuwingen en het status systeem
titleSuffix: Configuration Manager
description: Configureer waarschuwingen en gebruik het status systeem om op de hoogte te blijven van de status van uw Configuration Manager-implementatie.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c066a61380e09961192bcbe7192e2e945341c97c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720714"
---
# <a name="use-alerts-and-the-status-system-for-configuration-manager"></a>Waarschuwingen en het status systeem voor Configuration Manager gebruiken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configureer waarschuwingen en gebruik het ingebouwde status systeem om op de hoogte te blijven van de status van uw Configuration Manager-implementatie.  


##  <a name="status-system"></a><a name="bkmk_Status"></a> Statussysteem  
 Alle primaire site-onderdelen genereren statusberichten die feedback geven over de bewerkingen voor de site en hiërarchie.    Met deze informatie blijft u op de hoogte van de status van de verschillende siteprocessen. U kunt het waarschuwingssysteem zodanig instellen dat ruis voor bekende problemen wordt genegeerd terwijl de vroege zichtbaarheid van andere problemen die mogelijk uw aandacht vereisen wordt vergroot.  

 Het Configuration Manager-status systeem werkt standaard zonder configuratie door instellingen te gebruiken die geschikt zijn voor de meeste omgevingen. U kunt echter het volgende configureren:  

-   **Statusoverzichten:** u kunt de statusoverzichten op elke site bewerken om de frequentie te beheren van statusberichten die een statusindicatorwijziging voor de volgende vier overzichten genereren:  

    -   Samenvattingsprogramma voor implementatie van toepassing  

    -   Samenvattingsprogramma voor statistieken van toepassing  

    -   Statussamenvattingsprogramma onderdelen  

    -   Samenvattingsprogramma van het sitesysteem  

-   **Statusfilterregels** : u kunt nieuwe statusfilterregels maken, de prioriteit van regels wijzigen, regels in- of uitschakelen en ongebruikte regels op elke site verwijderen.  

    > [!NOTE]  
    >  Statusfilterregels bieden geen ondersteuning voor het gebruik van omgevingsvariabelen om externe opdrachten uit te voeren.  

-   **Status rapportage:** U kunt zowel de rapportage van server-als client onderdelen configureren om te wijzigen hoe status berichten worden gerapporteerd aan het Configuration Manager status systeem, en op te geven waar status berichten worden verzonden.  

    > [!WARNING]  
    >  Omdat de standaardinstellingen voor rapportage geschikt zijn voor de meeste omgevingen, kunt u deze het beste alleen wijzigen als u hier een goede reden voor hebt. Wanneer u het status rapportage niveau verhoogt door ervoor te kiezen om alle status details te rapporteren, kunt u het aantal te verwerken status berichten verhogen. Hierdoor wordt de verwerkings belasting op de Configuration Manager site verhoogd. Als u het statusrapportageniveau verlaagt, beperkt u mogelijk het nut van de statusoverzichten.  

Omdat in het statussysteem afzonderlijke configuraties voor elke site worden gehanteerd, moet u elke site afzonderlijk bewerken.  

###  <a name="procedures-for-configuring-the-status-system"></a><a name="bkmk_configstatus"></a> Procedures voor het configureren van het statussysteem  

##### <a name="to-configure-status-summarizers"></a>Statusoverzichten configureren  

1.  Navigeer in de Configuration Manager-console naar **beheer** > **site configuratie** >**sites**en selecteer vervolgens de site waarvoor u het status systeem wilt configureren.  

2.  Klik op het tabblad **Start** in de groep **Instellingen** op **Statusoverzichten**.  

3.  Selecteer in het dialoogvenster **Statusoverzichten** het statusoverzicht dat u wilt configureren en klik vervolgens op **Bewerken** om de eigenschappen voor dat overzicht te openen. Als u het samenvattingsprogramma voor de implementatie of de statistieken van de toepassing wilt bewerken wilt, gaat u verder met stap 5. Als u de onderdeelstatus wilt bewerken, gaat u verder met stap 6. Als u de sitesysteemstatus wilt bewerken wilt, gaat u verder met stap 7.  

4.  Voer de volgende stappen uit nadat u de eigenschappenpagina voor Samenvattingsprogramma voor implementatie van toepassing of Samenvattingsprogramma voor statistieken van toepassing hebt geopend:  

    1.  Configureer de samenvattingsintervallen op het tabblad **Algemeen** van de eigenschappenpagina en klik op **OK** om de eigenschappenpagina te sluiten.  

    2.  Klik op **OK** om het dialoogvenster **Statusoverzichten** te sluiten en deze procedure te voltooien.  

5.  Voer de volgende stappen uit nadat u de eigenschappenpagina voor Samenvattingsprogramma van onderdeelstatus hebt uitgevoerd:  

    1.  Configureer de waarden voor replicatie en drempel periode op het tabblad **Algemeen** van de eigenschappen pagina van de samen vatting.  

    2.  Selecteer op het tabblad **Drempels** het **berichttype** dat u wilt configureren en klik op de naam van een onderdeel in de lijst **Drempels** .  

    3.  Bewerk de waarden voor waarschuwingen en kritieke drempelwaarden in het dialoogvenster **Eigenschappen van drempelwaarde voor status** en klik vervolgens op **OK**.  

    4.  Herhaal zo nodig stap 6.b en 6.c, en klik vervolgens op **OK** om de eigenschappenpagina te sluiten.  

    5.  Klik op **OK** om het dialoogvenster **Statusoverzichten** te sluiten en deze procedure te voltooien.  

6.  Voer de volgende stappen uit nadat u de eigenschappenpagina voor Samenvattingsprogramma van het sitesysteem hebt uitgevoerd:  

    1.  Configureer de replicatie-en plannings waarden op het tabblad **Algemeen** van de eigenschappen pagina van de samen vattingen.  

    2.  Geef op het tabblad **Drempels** waarden voor **Standaard drempelwaarden** op voor de weergaven van kritieke en waarschuwingsstatussen.  

    3.  Als u de waarden voor specifieke **opslagobjecten**wilt bewerken, selecteert u het object in de lijst **Specifieke drempelwaarden** en klikt u op de knop **Eigenschappen** om de waarschuwings- en kritieke drempelwaarden voor opslagobjecten te openen en te bewerken. Klik op **OK** om de eigenschappen voor opslagobjecten te sluiten.  

    4.  Als u een nieuw opslagobject wilt maken, klikt u op de knop **Object maken** en geeft u de waarden voor het opslagobject op. Klik op **OK** om de eigenschappen voor het object te sluiten.  

    5.  Als u een opslagobject wilt verwijderen, selecteert u het object en klikt u op de knop **Verwijderen** .  

    6.  Herhaal stap 7. b tot en met 7. e Als dat nodig is. Klik vervolgens op **OK** om de overzichtseigenschappen te sluiten.  

    7.  Klik op **OK** om het dialoogvenster **Statusoverzichten** te sluiten en deze procedure te voltooien.  

##### <a name="to-create-a-status-filter-rule"></a>Een statusfilterregel maken  

1.  Navigeer in de Configuration Manager-console naar **beheer** > **site configuratie** >**sites**en selecteer vervolgens de site waarvoor u het status systeem wilt configureren.  

2.  Klik op het tabblad **Start** in de groep **Instellingen** op **Statusfilterregels**. Het dialoogvenster **Statusfilterregels** wordt geopend.  

3.  Klik op **maken**.  

4.  Op de pagina **Algemeen**van de wizard **Statusfilterregel maken** geeft u een naam op voor de nieuwe statusfilterregel en configureert u regelcriteria voor overeenkomende berichten. Vervolgens klikt u op **Volgende**.  

5.  Op de pagina **Acties** geeft u op welke acties moeten worden uitgevoerd wanneer een statusbericht overeenkomt met de filterregel. Klik vervolgens op **Volgende**.  

6.  Bekijk de details voor de nieuwe regel op de pagina **Samenvatting** en voltooi vervolgens de wizard.  

    > [!NOTE]  
    >  Voor Configuration Manager moet alleen de nieuwe status filter regel een naam hebben. Als de regel is gemaakt, maar u geen criteria opgeeft om statusberichten te verwerken, heeft de statusfilterregel geen effect. Dankzij dit gedrag kunt u regels maken en organiseren voordat u de statusfiltercriteria voor elke regel configureert.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>Een statusfilterregel wijzigen of verwijderen  

1.  Navigeer in de Configuration Manager-console naar **beheer** > **site configuratie** >**sites**en selecteer vervolgens de site waarvoor u het status systeem wilt configureren.  

2.  Klik op het tabblad **Start** in de groep **Instellingen** op **Statusfilterregels**.  

3.  Selecteer de regel die u wilt wijzigen in het dialoogvenster **Statusfilterregels** en voer vervolgens een van de volgende acties uit:  

    -   Klik op **Prioriteit verhogen** of **Prioriteit verlagen** om de verwerkingsvolgorde van de statusfilterregel te wijzigen. Selecteer vervolgens nog een actie of ga naar stap 8 van deze procedure om deze taak te voltooien.  

    -   Klik op **Uitschakelen** of **Inschakelen** om de status van de regel te wijzigen. Wanneer u de status van de regel hebt gewijzigd, selecteert u nog een actie of gaat u naar stap 8 van deze procedure om deze taak te voltooien.  

    -   Klik op **Verwijderen** als u de statusfilterregel van deze site wilt verwijderen en klik vervolgens op **Ja** om de actie te bevestigen. Wanneer u een regel hebt verwijderd, selecteert u nog een actie of gaat u naar stap 8 van deze procedure om deze taak te voltooien.  

    -   Klik op **Bewerken** als u de criteria voor de statusberichtregel wilt wijzigen en ga verder met stap 5 van deze procedure.  

4.  Wijzig de regel en criteria voor overeenkomende berichten op het tabblad **Algemeen** van het eigenschappenvenster voor statusfilterregels.  

5.  Op de pagina **Acties** wijzigt u welke acties moeten worden uitgevoerd wanneer een statusbericht overeenkomt met de filterregel.  

6.  Klik op **OK** om de wijzigingen op te slaan.  

7.  Klik op **OK** om het dialoogvenster **Statusfilterregels** te sluiten.  

##### <a name="to-configure-status-reporting"></a>Statusrapportage configureren  

1.  Navigeer in de Configuration Manager-console naar **beheer** > **site configuratie** > **sites**en selecteer vervolgens de site waarvoor u het status systeem wilt configureren.  

2.  Klik op het tabblad **Start** in de groep **Instellingen** op **Siteonderdelen configureren**en selecteer **Statusrapportage**.  

3.  Geef in het dialoogvenster **Eigenschappen van onderdeel voor statusrapportage** op welke server- en clientstatusberichten u wilt rapporteren of vastleggen:  

    1.  Configureer **rapport** om status berichten te verzenden naar het Configuration Manager status bericht systeem.  

    2.  Configureer **Logboek** om het type en de ernst van statusberichten naar het Windows-gebeurtenislogboek te schrijven.  

4.  Klik op **OK**.  

###  <a name="monitor-the-status-system-of-configuration-manager"></a><a name="BKMK_MonitorSystemStatus"></a> Het statussysteem van Configuration Manager controleren  
 **Systeem status** in Configuration Manager biedt een overzicht van de algemene bewerkingen van sites en site server bewerkingen van uw hiërarchie. Dit kan operationele problemen onthullen voor site systeem servers of-onderdelen en u kunt de systeem status gebruiken om specifieke Details voor verschillende Configuration Manager bewerkingen te controleren. U bewaakt de systeem status van het knoop punt **systeem status** van de werk ruimte **bewaking** in de Configuration Manager-console.  

 De meeste Configuration Manager site systeem rollen en-onderdelen genereren status berichten. Gegevens van statusberichten worden in elk operationeel logboek van de onderdelen geregistreerd, maar worden ook verzonden naar de sitedatabase waar ze samengevat worden en getoond in een algemene rollup van elk onderdeel of van status van sitesystemen. Deze rollups van statusberichten leveren gegevensdetails voor standaardbewerkingen en -waarschuwingen en foutdetails. U kunt de drempels configureren waarbij waarschuwingen of fouten worden getriggerd en het systeem fijn bewerken om ervoor te zorgen dat rollup-informatie bekende problemen, die niet relevant zijn voor u, negeert, terwijl ze de aandacht vestigt op actuele problemen op servers of voor bewerkingen op onderdelen die u eventueel verder wenst te onderzoeken.  

 Systeemstatus wordt gerepliceerd naar andere sites in een hiërarchie als sitegegevens, niet als globale gegevens. Dit betekent dat u alleen de status van de site kunt zien waarmee uw Configuration Manager-console verbinding maakt, en eventuele onderliggende sites onder die site. Overweeg daarom om uw Configuration Manager-console te verbinden met de site op het hoogste niveau van uw hiërarchie wanneer u de systeem status bekijkt.  

 Gebruik de volgende tabel om de verschillende systeemstatusweergaves te identificeren en om te bepalen wanneer elk van die weergaves dient gebruikt te worden.  

|Knooppunt|Meer informatie|  
|----------|----------------------|  
|Sitestatus|Gebruik dit knooppunt om een rollup te zien van de status van elk sitesysteem om de status van elke sitesysteemserver te controleren. Sitesysteemstatus is bepaald door drempels die u configureert voor elke site in het **Samenvattingsprogramma van het sitesysteem**.<br /><br /> U kunt statusberichten zien voor elk sitesysteem, drempels instellen voor statusberichten en de werking van de onderdelen op sitesystemen beheren door gebruik te maken van **Configuration Manager Service Manager**.|  
|Onderdeelstatus|Gebruik dit knoop punt om een samen vatting van de status van elk Configuration Manager onderdeel weer te geven om de operationele status van het onderdeel te controleren. Onderdeelstatus is bepaald door drempels die u configureert voor elke site in het **Samenvattingsprogramma van het sitesysteem**.<br /><br /> U kunt statusberichten zien voor elk onderdeel, drempels instellen voor statusberichten en de werking van de onderdelen beheren door gebruik te maken van **Configuration Manager Service Manager**.|  
|Conflicterende records|Gebruik dit knooppunt om statusberichten over clients te raadplegen die eventueel conflicterende records hebben.<br /><br /> Configuration Manager gebruikt de hardware-ID om clients te identificeren die mogelijk duplicaten zijn en u te waarschuwen voor de conflicterende records. Als u bijvoorbeeld een computer moet installeren, zou de hardware-ID dezelfde zijn, maar de GUID die Configuration Manager gebruikt, kan worden gewijzigd.|  
|Statusberichtquery 's|Gebruik dit knooppunt om de statusberichten te bevragen op specifieke gebeurtenissen en gerelateerde details. U kunt statusberichtquery's gebruiken om de statusberichten te vinden die gerelateerd zijn aan specifieke gebeurtenissen.<br /><br /> U kunt vaak status bericht query's gebruiken om te identificeren wanneer een specifiek onderdeel, een bepaalde bewerking of een Configuration Manager object is gewijzigd en het account dat is gebruikt om de wijziging aan te brengen. U kunt bijvoorbeeld de ingebouwde query voor **Verzamelingen, gemaakt, gewijzigd en gewist** uitvoeren om te bepalen wanneer een specifieke verzameling werd gemaakt, en de gebruikersaccount te identificeren die werd gebruikt om de verzameling te maken.|  

####  <a name="manage-site-status-and-component-status"></a><a name="bkmk_managestatus"></a> De sitestatus en onderdeelstatus beheren  
 Gebruik de volgende informatie om de site- en onderdeelstatus te beheren:  

-   Zie [Procedures voor het configureren van het statussysteem](#bkmk_configstatus)om drempels te configureren voor het statussysteem.  

-   Als u afzonderlijke onderdelen in Configuration Manager wilt beheren, gebruikt u de **Configuration Manager Service Manager**.  

####  <a name="view-status-messages"></a><a name="bkmk_view"></a> Statusberichten weergeven  
 U kunt de statusberichten zien voor afzonderlijke sitesysteemservers en -onderdelen.  

 Als u status berichten in de Configuration Manager-console wilt weer geven, selecteert u een specifieke site systeem server of onderdeel en klikt u vervolgens op **berichten weer geven**. Wanneer u berichten ziet, kunt u selecteren om specifieke berichttypes te zien of berichten van een bepaalde tijdsperiode, en kunt u de resultaten filteren op basis van de statusberichtgegevens.  

##  <a name="alerts"></a><a name="bkmk_Alerts"></a>Berichten  
 Configuration Manager waarschuwingen worden gegenereerd door bepaalde bewerkingen wanneer een specifieke voor waarde optreedt.  

- Waarschuwingen worden doorgaans gegenereerd wanneer er een fout optreedt die u moet oplossen.  

- Meldingen kunnen worden gegenereerd om u te waarschuwen dat er sprake is van een probleem, zodat u de situatie kunt blijven bewaken.  

- Bepaalde waarschuwingen kunt u zelf configureren, zoals waarschuwingen voor de status van Endpoint Protection en de client, terwijl andere waarschuwingen automatisch worden geconfigureerd.  

- U kunt abonnementen op waarschuwingen configureren, zodat de details vervolgens via e-mail kunnen worden verzonden en u beter op de hoogte bent van belangrijke problemen.  

  In de volgende tabel vindt u informatie over het configureren van waarschuwingen en waarschuwings abonnementen in Configuration Manager:  


|Bewerking|Meer informatie|  
|------------|----------------------|  
|Endpoint Protection waarschuwingen voor een verzameling configureren|Zie **waarschuwingen configureren voor Endpoint Protection in Configuration Manager** in [Endpoint Protection configureren](../../../protect/deploy-use/endpoint-protection-configure.md)|  
|Clientstatuswaarschuwingen voor een verzameling configureren|Zie de [client status configureren](../../../core/clients/deploy/configure-client-status.md).|  
|Configuration Manager-waarschuwingen beheren|Zie de sectie [Management tasks for alerts](#BKMK_Manage) in dit onderwerp.|  
|E-mailabonnementen op waarschuwingen configureren|Zie de sectie [management tasks for alerts](#BKMK_Manage) in dit onderwerp.|  
|Waarschuwingen controleren|Zie de sectie [Waarschuwingen controleren](#BKMK_MonitorAlerts)|  

###  <a name="management-tasks-for-alerts"></a><a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>Algemene waarschuwingen beheren  

1. Navigeer in de Configuration Manager-console naar **controle** > **waarschuwingen**en selecteer vervolgens een beheer taak.  

   Gebruik de volgende tabel voor meer informatie over de beheertaken waarvoor u mogelijk meer uitleg nodigt hebt voordat u ze selecteert.  

|Beheertaak|Details|  
    |---------------------|-------------|  
    |**Configureren**|Hiermee opent u het\>**Properties** * &lt;* dialoog venster Eigenschappen van waarschuwings naam, waarin u de naam, de ernst en de drempel waarden voor de geselecteerde waarschuwing kunt wijzigen. Als u de ernst van de waarschuwing wijzigt, is deze configuratie van invloed op hoe de waarschuwingen worden weer gegeven in de Configuration Manager-console.|  
    |**Opmerking bewerken**|Voer een opmerking voor de geselecteerde waarschuwingen in. Deze opmerkingen worden weer gegeven met de waarschuwing in de Configuration Manager-console.|  
    |**Uitstellen**|De bewaking van de waarschuwing wordt onderbroken tot de opgegeven datum is bereikt. Op dat moment wordt de status van de waarschuwing bijgewerkt.<br /><br /> U kunt een waarschuwing alleen uitstellen wanneer deze is ingeschakeld.|  
    |**Abonnement maken**|Hiermee opent u het dialoogvenster **Nieuw abonnement** , waarin u een e-mailabonnement op de geselecteerde waarschuwing kunt maken.|  

<!--##### To configure Endpoint Protection alerts for a collection  

1.  pending  -->

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>Een clientstatuswaarschuwing voor een verzameling configureren  

1.  Klik in de Configuration Manager-console op **assets en** >   **verzamelingen**met naleving van apparaten.  

2.  Selecteer in de lijst **Apparaatverzamelingen** de verzameling waarvoor u waarschuwingen wilt configureren en klik vervolgens op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

    > [!NOTE]  
    >  U kunt geen waarschuwingen voor gebruikersverzamelingen configureren.  

3.  Klik op het tabblad **waarschuwingen** van het\>**Properties** **Add** * &lt;* dialoog venster Eigenschappen van verzamelings naam op toevoegen.  

    > [!NOTE]  
    >  Het tabblad **Waarschuwingen** is alleen zichtbaar als aan de beveiligingsrol waaraan u gekoppeld bent machtigingen voor waarschuwingen zijn toegewezen.  

4.  Geef in het dialoogvenster **Nieuwe verzamelingmeldingen toevoegen** op welke meldingen moeten worden gegenereerd wanneer clientstatuswaarden onder een bepaalde drempelwaarde vallen en klik vervolgens op **OK**.  

5.  Selecteer elke clientstatuswaarschuwing in de lijst **Voorwaarden** van het tabblad **Waarschuwingen** en geef vervolgens de volgende gegevens op.  

    -   **Naam van waarschuwing** : accepteer de standaard naam of voer een nieuwe naam in voor de waarschuwing.  

    -   **Ernst van waarschuwing** : Kies in de vervolg keuzelijst het waarschuwings niveau dat wordt weer gegeven in de Configuration Manager-console.  

    -   **Waarschuwing activeren** : Geef het drempel percentage voor de waarschuwing op.  

6.  Klik op **OK** om het\>**Properties** * &lt;* dialoog venster Eigenschappen van verzamelings naam te sluiten.  

##### <a name="to-configure-email-notification-for-alerts"></a>E-mailmeldingen voor waarschuwingen configureren  

1.  Navigeer in de Configuration Manager-console naar **bewaking** > van**waarschuwingen** > **abonnementen**.  

2.  Klik op **E-mailmeldingen configureren** in het tabblad **Start** in de groep **Maken**.  

3.  Geef in het dialoogvenster **Eigenschappen van onderdeel voor e-mailmeldingen** de volgende informatie op:  

    -   **E-mail meldingen inschakelen voor waarschuwingen**: Schakel dit selectie vakje in om in te scha kelen Configuration Manager een SMTP-server te gebruiken om e-mail waarschuwingen te verzenden.  

    -   **FQDN of IP-adres van de SMTP-server voor verzenden van e-mailwaarschuwingen**: voer de volledig gekwalificeerde domeinnaam (FQDN) of het IP-adres en de SMTP-poort voor de e-mailserver in die u wilt gebruiken voor deze waarschuwingen.  

    -   **SMTP-server verbindings account**: Geef de verificatie methode op die Configuration Manager moet gebruiken om de e-mail server te verbinden.  

    -   **Adres van afzender voor e-mailwaarschuwingen**: het e-mailadres opgeven waarvandaan de e-mailwaarschuwingen worden verzonden.  

    -   **SMTP-server testen**: een test-e-mail verzenden naar het e-mailadres dat bij **Adres van afzender voor e-mailwaarschuwingen**is opgegeven.  

4.  Klik op **OK** om de instellingen op te slaan en het dialoogvenster **Eigenschappen van onderdeel voor e-mailinstellingen** te sluiten.  

##### <a name="to-subscribe-to-email-alerts"></a>Abonneren op e-mailwaarschuwingen  

1.  Navigeer in de Configuration Manager-console naar **controle** > **waarschuwingen**.  

2.  Selecteer een waarschuwing en klik op het tabblad **Start** in de groep **Abonnement** vervolgens op **Abonnement maken**.  

3.  Geef in het dialoogvenster **Nieuw abonnement** de volgende informatie op:  

    -   **Naam**: voer een unieke naam voor het e-abonnement in. U kunt maximaal 255 tekens gebruiken.  

    -   **E-mailadres**: voer de e-mailadressen in waarnaar u waarschuwingen wilt verzenden. U kunt meerdere e-mailadressen opgeven door deze te scheiden met een puntkomma (;).  

    -   **Taal e-mail**: geef in de lijst de taal voor de e-mail op.  

4.  Klik op **OK** om het dialoogvenster **Nieuw abonnement** te sluiten en het e-mailabonnement te maken.  

    > [!NOTE]  
    >  U kunt in de werkruimte **Bewaking** abonnementen verwijderen en bewerken wanneer u het knooppunt **Waarschuwingen** uitvouwt en vervolgens op het knooppunt **Abonnementen** klikt.  

###  <a name="monitor-alerts"></a><a name="BKMK_MonitorAlerts"></a>Waarschuwingen bewaken  
 U kunt meldingen zien in het knooppunt **Meldingen** van de werkruimte **Controle** . Waarschuwingen hebben één van de volgende statussen:  

- **Nooit geactiveerd**: er wordt niet aan de voorwaarde van voor de waarschuwing voldaan.  

- **Actief**: er wordt aan de voorwaarde van de waarschuwing voldaan.  

- **Geannuleerd**: er wordt niet meer voldaan aan de voorwaarde van een actieve waarschuwing. Deze toestand geeft aan dat de conditie die de melding veroorzaakte, nu opgelost is.  

- **Uitgesteld**: een gebruiker met beheerders rechten heeft Configuration Manager geconfigureerd om de status van de waarschuwing op een later tijdstip te evalueren.  

- **Uitgeschakeld**: de waarschuwing is uitgeschakeld door een gebruiker met beheerdersrechten. Wanneer een waarschuwing deze status heeft, wordt de waarschuwing niet door Configuration Manager bijgewerkt, zelfs niet als de status van de waarschuwing verandert.  

  U kunt een van de volgende acties uitvoeren wanneer Configuration Manager een waarschuwing genereert:  

- De conditie oplossen die de melding veroorzaakte. U lost bijvoorbeeld een netwerk- of configuratieprobleem op dat de melding genereerde. Nadat Configuration Manager detecteert dat het probleem niet meer bestaat, verandert de status van de waarschuwing in **Annuleren**.  

- Indien de melding een bekende kwestie is, kunt u de melding uitstellen gedurende een bepaalde tijdsperiode. Op dat moment wordt de waarschuwing in Configuration Manager bijgewerkt naar de huidige status.  

   U kunt een melding alleen uitstellen als ze actief is.  

- U kunt de **Commentaar** van een melding bewerken zodat andere gebruikers met beheerdersrechten kunnen zien dat u zich bewust bent van de melding. In de commentaar kunt u bijvoorbeeld aangeven hoe de conditie op te lossen, informatie leveren over de huidige toestand van de conditie of uitleggen waarom u de melding uitstelde.  

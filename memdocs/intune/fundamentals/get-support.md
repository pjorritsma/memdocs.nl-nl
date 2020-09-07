---
title: Ondersteuning voor Microsoft Intune krijgen
titleSuffix: Microsoft Intune
description: Online- en telefonische ondersteuning verkrijgen voor betaalde Microsoft Intune-abonnementen en proefabonnementen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/25/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7fc95d17-098e-4da5-8a09-a96476569dd9
ms.reviewer: crisk
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a476be4fb8c9d40150648e72d3203df564893dd
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994341"
---
# <a name="how-to-get-support-for-microsoft-intune"></a>Ondersteuning voor Microsoft Intune krijgen

Microsoft biedt wereldwijde technische, voorverkoop-, facturerings- en abonnementsondersteuning voor Microsoft Intune. Ondersteuning is online en telefonisch beschikbaar voor betaalde abonnementen en proefabonnementen. Online technische ondersteuning is beschikbaar in het Engels en Japans. Telefonische ondersteuning en online-ondersteuning bij factureren zijn in meer talen beschikbaar.

Als Intune-beheerder kunt u de optie **Help en ondersteuning** gebruiken om vanuit de Azure-portal een onlineondersteuningsticket voor Intune in te dienen. Als u een ondersteuningsincident wilt maken en beheren, moet uw account een Azure Active Directory-rol (Azure AD) hebben met de *actie* **microsoft.office365.supportTickets**. Zie [beheerdersrollen in Azure Active Directory](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) voor informatie over rollen en machtigingen in Azure AD die zijn vereist voor het maken van een ondersteuningsticket.

>[!IMPORTANT]
> Neem voor technische ondersteuning voor externe producten die met Intune werken (zoals SaaSwedo, Cisco of Lookout), contact op met de leverancier van dat product. Open pas een ondersteuningsaanvraag voor Intune als u zeker weet dat het andere product juist is geconfigureerd.
>
> Raadpleeg de sectie [Probleemoplossing](help-desk-operators.md) in de Intune-documentatie voor informatie over het oplossen van problemen met betrekking tot Microsoft Intune.

## <a name="help-and-support-experience"></a>Help en ondersteuning-ervaring

De Help en ondersteuning-ervaring van Intune is beschikbaar via het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en via alle blades (of pagina's) onder Intune in Azure Portal.

De *Help en ondersteuning*-ervaring is vergelijkbaar met de ervaring in het [Microsoft 365-beheercentrum](https://admin.microsoft.com/) en vervangt de vorige *Help en ondersteuning*, die beschikbaar blijft voor andere services in Azure.

### <a name="options-to-access-help-and-support"></a>Opties voor toegang tot Help en ondersteuning

Wanneer u een nieuw gemaakte tenant voor Intune gebruikt, is het mogelijk dat *Help en ondersteuning* niet kan worden geopend en het volgende bericht wordt weergegeven:

- *Er is een onbekend probleem opgetreden. Vernieuw de pagina, maar als het probleem zich blijft voordoen, dient u een ondersteuningsaanvraag in via het [M365-beheercentrum](https://admin.microsoft.com) en verwijst u naar de gegeven sessie-id.*

De foutdetails bestaan onder andere uit een *sessie-id*, *extensie*gegevens en meer.

Dit probleem treedt op wanneer u uw nieuwe tenantaccount niet hebt geverifieerd via het **Microsoft 365-beheercentrum** op https://admin.microsoft.com of de **Office 365-portal** op https://portal.office.com. U kunt dit probleem oplossen door de koppeling naar het *Microsoft 365-beheercentrum* in het bericht te selecteren of door naar https://portal.office.com te gaan en u aan te melden. Na verificatie op beide sites hebt u toegang tot *Help en ondersteuning* voor Intune.

**Toegang tot Help en ondersteuning**:

- **In de Azure-Portal**

  - Selecteer **Help en ondersteuning** vanaf een willekeurige Intune-blade of -pagina.

  > [!NOTE]  
  > Als uw exemplaar van Intune wordt gehost in de privécloud voor de overheid (ook wel een soevereine cloud genoemd, bijv. Azure Government) raadpleegt u [Intune-ondersteuning voor de privécloud voor de overheid](#intune-support-for-private-cloud-for-government) verderop in dit artikel. De *Help en ondersteuning*-ervaring voor Intune komt pas volgend jaar beschikbaar voor de privécloud voor de overheid.

- **Vanuit het Microsoft Endpoint Manager-beheercentrum** doet u het volgende

  - Selecteer vanuit elk willekeurig knooppunt in het Microsoft Endpoint Manager-beheercentrum het **?** -pictogram in de rechterbovenhoek van de portal om het deelvenster **Help** te openen. Selecteer **Help en ondersteuning** om de pagina **Selecteer een beheertype** te openen.

    > [!div class="mx-imgBorder"]
    > ![Open de pagina selectie van beheertype](./media/get-support/management-types.png)

    Gebruik de vervolgkeuzelijst om het beheertype te selecteren waarbij u hulp wilt om de toepasselijke pagina Help en ondersteuning te openen. Het Microsoft Endpoint Manager-beheercentrum ondersteunt de volgende beheertypen. U moet het specifieke type selecteren waarbij u hulp nodig hebt, bijvoorbeeld Intune:

    - Configuration Manager
    - Intune
    - Co-beheer

    > [!div class="mx-imgBorder"]
    > ![Een beheertype selecteren](./media/get-support/select-management-type.png)

    Nadat u een beheertype hebt geselecteerd, wordt de van toepassing zijnde pagina *Help en ondersteuning* geopend, waar u details kunt opgeven voor [het zoeken naar oplossingen](#find-solutions) voor een specifiek probleem. Details worden gefilterd op basis van het geselecteerde beheertype.

     Als het correcte beheertype niet is geselecteerd **(1)** , klikt u op *Een beheertype selecteren* **(2)** om terug te keren naar de vervolgkeuzelijst met beheertypen:

    > [!div class="mx-imgBorder"]
    > ![Het beheertype bevestigen](./media/get-support/confirm-management-selection.png)

  - Als u inzoomt op een ander knooppunt, zoals *Apparaten*, *Apps* of *Gebruikers* en vervolgens *Help en ondersteuning* selecteert, kunt u geen beheertype selecteren en wordt het type niet weergegeven onder *Help en ondersteuning*. In dit geval wordt uitgegaan van *Intune*. Als u niet wilt dat de context Intune is, gebruikt u de optie **?** , zodat u een ander beheertype kunt selecteren.

### <a name="the-support-experience"></a>De ondersteuningservaring

  Wanneer u Help en ondersteuning opent, verschijnt in de portal het venster **Hulp nodig?** :

  ![Venster 'Hulp nodig?' weergeven](./media/get-support/need-help.png)

  In de linkerbovenhoek ziet u drie pictogrammen die u kunt selecteren om verschillende deelvensters van het venster *Hulp nodig?* te openen. Het deelvenster dat momenteel wordt weergegeven, wordt gemarkeerd door onderstreping.

  Klanten met een **Premier**- of **Unified**-ondersteuningscontract hebben [extra opties](#premier-and-unified-support-customers) voor ondersteuning en zien een banner in het venster *Hulp nodig?* die op de volgende afbeelding lijkt: ![Premier-banner](./media/get-support/premier-banner.png)

  Via *Hulp nodig?* wordt het deelvenster *Oplossingen zoeken* geopend. Als u echter een actieve ondersteuningscase hebt, wordt vanuit het venster het deelvenster *Serviceaanvragen* geopend, waar u details over uw actieve en gesloten ondersteuningscases kunt bekijken.

#### <a name="find-solutions"></a>Oplossingen zoeken

![Deelvenster 'Oplossingen zoeken' selecteren](./media/get-support/find-solutions.png)

Geef in het deelvenster *Oplossingen zoeken* een aantal details over een probleem op in het daarvoor bestemde tekstvak. Op basis van de tekst die u opgeeft over een probleem, vult het deelvenster zich met inzichten die mogelijk overeenkomen. U krijgt ook koppelingen naar aanbevolen artikelen die u kunnen helpen bij het oplossen van het probleem.

Als er een sterke overeenkomst is gevonden voor de details die u opgeeft, kunnen er direct tips voor probleemoplossing verschijnen in het venster *Hulp nodig?* .

U kunt bijvoorbeeld **Fout met wachtwoordsynchronisatie** opgeven. De resultaten omvatten dan richtlijnen voor probleemoplossing direct in het deelvenster, evenals koppelingen naar aanbevolen artikelen uit onze documentatiebibliotheek.

![Inzichten voor probleemoplossing weergeven](./media/get-support/troubleshooting-insights.png)

#### <a name="contact-support"></a>Contact opnemen met de ondersteuning

![Selecteer het deelvenster 'Contact opnemen met ondersteuning'](./media/get-support/contact-support.png)

Vanuit het deelvenster *Contact opnemen met ondersteuning* kunt u een hulpverzoek indienen. Dit deelvenster is beschikbaar nadat u enkele eenvoudige trefwoorden hebt opgegeven in het deelvenster *Oplossingen zoeken*.

Als u hulp wilt aanvragen, geeft u een probleembeschrijving op met zoveel details als nodig is.  Nadat u uw telefoonnummer en e-mailadres hebt bevestigd, selecteert u de gewenste contactwijze. In het venster wordt een reactietijd weergegeven voor elke contactwijze, waarmee u een idee krijgt wanneer er ongeveer contact met u wordt opgenomen. Voordat u uw aanvraag indient, voegt u bestanden toe (bijv. logboeken of schermafbeeldingen) waarmee u meer details over het probleem kunt opgeven.

![Contactformulier voor ondersteuning](./media/get-support/contact-support-form.png)

Nadat u de vereiste gegevens hebt ingevuld, selecteert u **Neem contact met mij op** om de aanvraag in te dienen.

#### <a name="service-requests"></a>Serviceaanvragen

![Deelvenster Serviceaanvragen selecteren](./media/get-support/service-requests.png)

In het deelvenster *Serviceaanvragen* wordt uw geschiedenis van ondersteuningscases weergegeven. Actieve cases staan bovenaan de lijst, daarna volgen gesloten problemen die u nog kunt bekijken.

![Lijst met serviceaanvragen weergeven](./media/get-support/service-requests-pane.png)

Als u een actief ondersteuningscasenummer hebt, kunt u dit hier invoeren om naar dat probleem te gaan. U kunt ook een incident selecteren uit de lijst met actieve en gesloten incidenten om meer informatie erover weer te geven.

Wanneer u klaar bent met het bekijken van de details van een incident, selecteert u de pijl naar links bovenaan het venster Serviceaanvragen, net boven de drie pictogrammen voor het deelvenster *Hulp nodig?* . Via de pijl naar links gaat u terug naar de lijst met ondersteuningscases die u hebt geopend.

#### <a name="premier-and-unified-support-customers"></a>Klanten met Premier- en Unified-ondersteuning

Als klant met een **Premier**- of **Unified**-ondersteuningscontract kunt u de ernst van uw probleem opgeven en een terugbelmoment voor ondersteuning inplannen op een datum en tijdstip naar keuze. Deze opties zijn beschikbaar wanneer u een nieuw probleem opent of indient en wanneer u een actieve ondersteuningsaanvraag bewerkt.

**Ernst** - De opties om de ernst van een probleem op te geven, zijn afhankelijk van uw ondersteuningscontract:

- *Premier*: Ernst A, B of C
- *Unified*: Kritiek of niet-kritiek

Door ernstniveau **A** of **Kritiek** te selecteren, beperkt u zich tot een telefonische ondersteuningscase, wat de snelste ondersteuningsoptie is.

**Terugbelmoment plannen** - U kunt een terugbelmoment inplannen op een datum en tijdstip naar keuze.

## <a name="azure-help--support-experience"></a>Azure Help en ondersteuning-ervaring

U hebt geen toegang meer tot de *Help en ondersteuning* van Azure om hulp te krijgen bij Intune, tenzij u een abonnement op een privécloud voor de overheid hebt.
Als uw exemplaar van Intune niet in een privécloud voor de overheid wordt uitgevoerd, wordt u bij navigatie in *Help en ondersteuning* van Azure omgeleid naar de *Help en ondersteuning*-ervaring van Intune voor het maken en beheren van ondersteuningsincidenten:

Wanneer u het navigatiedeelvenster **Help en ondersteuning** aan de linkerkant gebruikt of de optie **?** gebruikt om het deelvenster *Help* te openen en **Help en ondersteuning** selecteert, wordt de pagina *Help en ondersteuning* van Azure geopend.

Selecteer op deze pagina **+ Nieuwe ondersteuningsaanvraag** om het tabblad *Basis* van de pagina *Help en ondersteuning + Nieuwe ondersteuningsaanvraag* te openen.

![Help en ondersteuning](./media/get-support/help-plus-support.png)

Op deze pagina:

- Selecteer **Technisch** bij *Type probleem*.
- Selecteer **Microsoft Intune** bij *Service*.

  U krijgt dan een koppeling waarmee u wordt doorgestuurd naar de [Help- en ondersteuningspagina van Intune](https://aka.ms/intunehelpsupport).
  
  ![Nieuwe ondersteuningsaanvraag](./media/get-support/new-request.png)

## <a name="intune-support-for-private-cloud-for-government"></a>Intune-ondersteuning voor de privécloud voor de overheid

Als uw Intune-abonnement wordt gehost in de privécloud voor de overheid (ook wel een soevereine cloud genoemd, bijvoorbeeld Azure Government), hebt u nog geen toegang tot de nieuwere Help en ondersteuning van Intune.  Gebruik in plaats daarvan de volgende informatie om ondersteuning te vragen voor Intune.

### <a name="create-an-online-support-ticket"></a>Een onlineondersteuningsticket maken

>[!IMPORTANT]
> Als *Help en ondersteuning* wordt overgezet naar een nieuw systeem dat nog niet beschikbaar is voor de privécloud voor de overheid en u een ondersteuningsincident maakt, wordt in de portal een ondersteuningscase voorzien van een identificatienummer van 15 cijfers. Wanneer het 15-cijferige geval wordt gemaakt, wordt die case gespiegeld voor gebruik door Microsoft Ondersteuning. Deze gespiegelde case wordt gemaakt in een nieuw ondersteuningssysteem, maakt gebruik van een 8-cijferige case-id en wordt gebruikt door ondersteuningsservices voor het bijhouden van alle activiteit en communicatie voor uw ondersteuningsincident. Kort nadat uw 15-cijferige case is gemaakt, ontvangt u een e-mailbericht met het 8-cijferige nummer van de gespiegelde ondersteuningscase die wordt gebruikt door de ondersteuningsservices.
>
> Ondersteun persoonlijk werk en communiceer op basis van de 8-cijferige ondersteuningscase. Gebruik de 8-cijferige ondersteuningscase alleen om de communicatie te registreren en de voortgang van het incident bij te houden. U ontvangt updates per e-mail op basis van die 8-cijferige ondersteuningscase die fungeert als de record voor het bijhouden van het werk aan uw case. Er worden geen details gelogd in het 15-cijferige ondersteuningsincident. Wanneer de ondersteuning is voltooid en de 8-cijferige ondersteuningscase wordt gesloten, wordt deze status ook weergegeven in de 15-cijferige ondersteuningscase die u kunt bekijken in de Azure-portal.  Er mogen geen andere updates of statuswijzigingen worden verwacht voor de ondersteuningscase van 15 cijfers.
>
> Als de overgangen tussen ondersteuningsprogramma's later dit jaar worden voltooid, lijkt de ondersteuningservaring die door Intune op de cloud voor de overheid wordt gehost, op de standaard *Help en ondersteuning*-ervaring die op dit moment beschikbaar is voor Intune-abonnementen die worden gehost op de openbare cloud.

1. Meld u aan bij Azure Portal (<https://portal.azure.us>) met de referenties van een Intune-beheerder. Kies de **?** in de rechterbovenhoek van de portal en selecteer vervolgens **Help + ondersteuning** om naar de gelijknamige[Azure Help + ondersteuning](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview)pagina te gaan.

   ![Afbeelding van de vraagtekenkoppeling, waarbij de koppeling Help en ondersteuning is gemarkeerd](./media/get-support/azure-get-support.png)

2. Selecteer **Nieuwe ondersteuningsaanvraag** op de pagina **Help en ondersteuning** van Azure.

   ![Afbeelding van de pagina Help en ondersteuning met de koppeling Nieuwe ondersteuningsaanvraag gemarkeerd](./media/get-support/azure-support-ticket-link.png)

3. Op het tabblad **Basis** moet u voor de meeste technische problemen met Intune de volgende opties kiezen:
   - **Type probleem**: **Technisch**
   - **Abonnement**: <*uw abonnement*>
   - **Service**: **Microsoft Intune**
   - **Type probleem**: Kies het probleemtype in de vervolgkeuzelijst.
   - **Subtype van het probleem**: Kies het subprobleemtype in de vervolgkeuzelijst.
   - **Onderwerp**: Beschrijf kort het probleem waarbij u hulp nodig hebt.

   ![Afbeelding van het tabblad Basis op de pagina Help en ondersteuning - Nieuwe ondersteuningsaanvraag](./media/get-support/help-new-support-case-basics.png)

   Kies **Volgende: Oplossingen** om door te gaan.
4. Bekijk op het tabblad **Oplossing** de aanbevolen stappen die u mogelijk helpen uw probleem op te lossen zonder een ticket in te dienen. Als u nog steeds een ondersteuningsaanvraag wilt maken nadat u de stappen hebt bekeken, klikt u op **Volgende: Details**.

   ![Afbeelding van het tabblad Oplossing op de pagina Help en ondersteuning - Nieuwe ondersteuningsaanvraag](./media/get-support/help-new-support-case-solutions.png)
5. Vul in het tabblad **Details** de details van uw probleem, de ondersteuningsmethode en uw contactgegevens in en klik op **Volgende: Beoordelen en maken**.

   ![Afbeelding van het tabblad Details op de pagina Help en ondersteuning - Nieuwe ondersteuningsaanvraag](./media/get-support/help-new-support-case-details.png)
6. Bekijk de informatie, controleer of deze klopt, en kies vervolgens **Maken** om uw ondersteuningsaanvraag in te dienen.

   ![Afbeelding van het tabblad Beoordelen en maken op de pagina Nieuwe ondersteuningsaanvraag](./media/get-support/help-new-support-case-create.png)

>[!IMPORTANT]
>Als u een vraag over facturering of abonnementen hebt, kunt u een aanvraag voor ondersteuning openen in het [Microsoft 365-beheercentrum](https://admin.microsoft.com/Support/SupportEntry.aspx).

### <a name="view-support-requests"></a>Ondersteuningsaanvragen weergeven  

U kunt uw ondersteuningsaanvragen weergeven in de Azure-portal. De beschikbare informatie is echter beperkt.  Ga als volgt te werk om uw incidenten weer te geven:

1. Meld u aan bij Azure (<https://portal.azure.com>) met uw Intune-beheerdersreferenties en selecteer de **?** in de rechterbovenhoek van de portal en selecteer vervolgens **Help + ondersteuning** om naar de gelijknamige[Azure Help + ondersteuning](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview)pagina te gaan.

2. Op de pagina **Help en ondersteuning** kunt u de lijst met **recente ondersteuningsaanvragen** weergeven.

   > [!IMPORTANT]  
   > Klanten van de privécloud voor de overheid kunnen alleen het ondersteuningscasenummer van 15 cijfers en de incidentstatus weergeven. Alle communicatie over de case en bijgehouden werk of waarschuwingen worden per e-mail verzonden en verwijzen naar het ondersteuningscasenummer van 8 cijfers dat is gemaakt als gespiegelde ondersteuningscase van de aanvraag die in de Intune-console is geopend.

## <a name="additional-resources"></a>Extra resources  

- [Ondersteuning voor facturerings- en abonnementsbeheer](https://support.office.com/article/Contact-Office-365-for-business-support-Admin-Help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b)
- [Volumelicenties](https://go.microsoft.com/fwlink/p/?LinkID=282015)
- [Problemen met Intune oplossen](help-desk-operators.md)
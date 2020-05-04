---
title: Bewerkingen en onderhoud voor rapportage
titleSuffix: Configuration Manager
description: Meer informatie over het beheren van rapporten en rapport abonnementen in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 5e154f2859a7541ac8f67b8588da7dfb8877c940
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713714"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Bewerkingen en onderhoud voor rapportage in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat de infra structuur is ingesteld voor rapportage in Configuration Manager, is er een aantal bewerkingen waarmee u doorgaans rapporten en rapport abonnementen kunt beheren.

> [!NOTE]
> Dit artikel richt zich op rapporten in SQL Server Reporting Services. Vanaf versie 2002 kunt u de rapportage met Power BI Report Server integreren. Zie [integreren met Power bi Report Server](powerbi-report-server.md)voor meer informatie.

## <a name="run-a-report-from-reporting-services"></a>Een rapport uitvoeren vanuit Reporting Services

Configuration Manager de rapporten worden opgeslagen in SQL Server Reporting Services. Het rapport haalt gegevens op uit de Configuration Manager-site database. U hebt toegang tot rapporten in de Configuration Manager-console of door gebruik te maken van Report Manager via een webbrowser. Open rapporten vanuit een webbrowser op een computer die toegang heeft tot het Reporting Services-punt en de gebruiker voldoende rechten heeft om de rapporten weer te geven. Als u rapporten wilt uitvoeren, hebt u **Lees** rechten nodig voor de **site** machtiging en de machtiging **rapport uitvoeren** voor specifieke objecten.

Wanneer u een rapport uitvoert, worden de rapport titel, beschrijving en categorie weer gegeven in de taal van het lokale besturings systeem. Zie [talen voor rapporten](configuring-reporting.md#-languages-for-reports)voor meer informatie.

> [!NOTE]  
> Report Manager is een webgebaseerd rapport toegang en beheer programma. U kunt dit gebruiken om één exemplaar van een rapport server te beheren via een HTTPS-verbinding. Gebruik Report Manager voor operationele taken: rapporten weer geven, rapport eigenschappen wijzigen en gekoppelde rapport abonnementen beheren. Dit artikel bevat de stappen om een rapport weer te geven en rapport eigenschappen te wijzigen in Report Manager. Zie [Wat is Report Manager?](https://docs.microsoft.com/sql/reporting-services/report-manager-ssrs-native-mode) voor meer informatie over andere opties in Report Manager.

Gebruik de volgende procedures om een Configuration Manager-rapport uit te voeren.

### <a name="run-a-report-in-the-configuration-manager-console"></a>Een rapport uitvoeren in de Configuration Manager-console

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** . Vouw **rapportage**uit en selecteer vervolgens **rapporten**. Dit knoop punt bevat een lijst met de beschik bare rapporten.

    > [!TIP]
    > Als op dit knoop punt geen rapporten worden weer gegeven, controleert u of het Reporting Services-punt is geïnstalleerd en geconfigureerd. Zie [Configure Reporting](configuring-reporting.md)(Engelstalig) voor meer informatie.

1. Selecteer het rapport dat u wilt uitvoeren. Selecteer op het tabblad **Start** van het lint in de sectie **rapport groep** de optie **uitvoeren** om het rapport te openen.

1. Als er vereiste para meters zijn, geeft u deze op en selecteert u vervolgens **rapport weer geven**.

### <a name="run-a-report-in-a-web-browser"></a>Een rapport uitvoeren in een webbrowser

1. Ga in uw webbrowser naar de URL van de Report Manager, bijvoorbeeld `https://Server1/Reports`. Dit adres vindt u op de pagina **Report Manager URL** in Reporting Services-Configuration Manager.

1. Selecteer in Report Manager de rapportmap voor Configuration Manager, bijvoorbeeld **ConfigMgr_CAS**.

    > [!TIP]
    > Als Report Manager geen rapporten vermeld, controleert u of het Reporting Services-punt is geïnstalleerd en geconfigureerd. Zie [Configure Reporting](configuring-reporting.md)(Engelstalig) voor meer informatie.

1. Selecteer de rapport categorie voor het rapport dat u wilt uitvoeren en selecteer vervolgens het specifieke rapport. Het rapport wordt geopend in Report Manager.

1. Als er vereiste para meters zijn, geeft u deze op en selecteert u vervolgens **rapport weer geven**.

## <a name="modify-the-properties-of-a-report"></a>De eigenschappen van een rapport wijzigen

Rapport eigenschappen bevatten de naam en beschrijving van het rapport. U kunt de eigenschappen van een rapport weer geven n de Configuration Manager-console.

Als u de eigenschappen wilt wijzigen, gebruikt u Report Manager:

1. Ga in uw webbrowser naar de URL van de Report Manager, bijvoorbeeld `https://Server1/Reports`.

1. Selecteer in Report Manager de rapportmap voor Configuration Manager, bijvoorbeeld **ConfigMgr_CAS**.

1. Selecteer de categorie rapport en selecteer vervolgens het specifieke rapport. Het rapport wordt geopend in Report Manager.

1. Selecteer het tabblad **Eigenschappen** . Wijzig de naam en beschrijving van het rapport en selecteer vervolgens **Toep assen**.

Report Manager slaat de rapport eigenschappen op de rapport server op. De Configuration Manager-console bevat de bijgewerkte rapport eigenschappen voor het rapport.

## <a name="edit-a-report"></a><a name="bkmk_edit"></a>Een rapport bewerken

Wanneer een bestaand Configuration Manager rapport niet de informatie ophaalt die u wilt, kunt u deze bewerken in Report Builder. U kunt Report Builder ook gebruiken om de indeling of het ontwerp van het rapport te wijzigen. Hoewel u een standaard rapport rechtstreeks kunt bewerken, is het het beste om het te klonen. Open het rapport dat u wilt bewerken en selecteer vervolgens **Opslaan als**.

Als u een rapport wilt bewerken, hebt u de machtiging **site wijzigen** nodig en kunt u de machtigingen voor het **rapport wijzigen** voor de specifieke objecten in het rapport.

> [!IMPORTANT]
> Met site-updates worden ingebouwde rapporten bewaard. Als u een standaard rapport wijzigt, wordt de naam van het rapport gewijzigd wanneer de site wordt bijgewerkt met een onderstrepings`_`teken (). Dit gedrag zorgt ervoor dat het gewijzigde rapport niet door de site-update wordt overschreven door het standaard rapport.
>
> Als u vooraf gedefinieerde rapporten wijzigt, maakt u een back-up van uw aangepaste rapporten voordat u een site-update installeert. Na de update herstelt u het rapport in Reporting Services. Als u belang rijke wijzigingen aanbrengt in een vooraf gedefinieerd rapport, maakt u in plaats daarvan een nieuw rapport. Nieuwe rapporten die u maakt voordat u een site upgradet, worden niet overschreven.

Gebruik de volgende procedure om de eigenschappen van een Configuration Manager rapport te bewerken.

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** . Vouw **rapportage**uit en selecteer vervolgens het knoop punt **rapporten** .

1. Selecteer het rapport dat u wilt wijzigen. Selecteer op het tabblad **Start** van het lint in de sectie **rapport groep** de optie **bewerken**. Mogelijk wordt u gevraagd om referenties in te voeren. Als Report Builder niet op de computer is geïnstalleerd, wordt u door Configuration Manager gevraagd om het te installeren. Report Builder is vereist om rapporten te wijzigen en te maken.

1. Wijzig de juiste rapport instellingen in Report Builder. Selecteer **Opslaan** om het rapport op de rapport server op te slaan.

## <a name="create-reports"></a>Rapporten maken

Er zijn twee soorten rapporten die u kunt maken:

- Met een **rapport op basis van model** kunt u interactief de items selecteren die u in het rapport wilt gebruiken. Zie [aangepaste rapport modellen maken voor Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md)voor meer informatie over het maken van aangepaste rapport modellen.

- Met een **rapport op basis van SQL** kunt u gegevens ophalen die zijn gebaseerd op een rapport SQL-instructie.

> [!IMPORTANT]
> Als u een nieuw rapport wilt maken, moet uw account machtigingen voor het wijzigen van de **site** hebben. U kunt alleen een rapport maken in mappen waarvoor u de machtiging **rapport wijzigen** hebt.

### <a name="create-a-model-based-report"></a>Een rapport op basis van model maken

Gebruik de volgende procedure om een Configuration Manager rapport op basis van een model te maken.

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **rapportage**uit en selecteer het knoop punt **rapporten** .

1. Op het tabblad **Start** van het lint, in de sectie **maken** , selecteert u **rapport maken**. Met deze actie wordt de **wizard Rapport maken**geopend.

1. Configureer op de pagina **informatie** de volgende instellingen:

    - **Type**: Selecteer **rapport op basis van model**.

    - **Naam**: Geef een naam op voor het rapport.

    - **Beschrijving**: Geef een beschrijving op voor het rapport.

    - **Server**: geeft de naam weer van de rapport server waarop u dit rapport maakt.

    - **Pad**: Selecteer **Bladeren** om een map op te geven waarin u het rapport wilt opslaan.

1. Selecteer op de pagina **model selectie** een beschikbaar model in de lijst om dit rapport te maken. In het gedeelte **Preview** worden de SQL Server weergaven en entiteiten weer gegeven die beschikbaar zijn in dit rapport model.

1. Voltooi de wizard Rapport maken.

1. Open Report Builder om de rapport instellingen te configureren. Zie [een Configuration Manager rapport bewerken](#bkmk_edit)voor meer informatie.

1. In Report Builder maakt u de rapport indeling, selecteert u gegevens in de weer gaven beschik bare SQL Server en voegt u para meters aan het rapport toe.

1. Selecteer **uitvoeren** om het rapport uit te voeren. Controleer of het rapport de informatie bevat die u verwacht. Selecteer zo nodig **ontwerp** om het rapport verder te wijzigen.

1. Selecteer **Opslaan** om het rapport op de rapport server op te slaan.

### <a name="create-a-sql-based-report"></a>Een rapport op basis van SQL maken

Wanneer u een SQL-instructie voor een aangepast rapport maakt, verwijst u niet rechtstreeks naar SQL Server tabellen. Altijd verwijzen naar ondersteunde rapportage SQL Server weergaven van de site database. Deze weer gaven hebben namen die beginnen `v_`met. Zie voor meer informatie [aangepaste rapporten maken met behulp van SQL Server weer gaven in Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

U kunt ook verwijzen naar open bare opgeslagen procedures vanuit de site database. Deze opgeslagen procedures hebben namen die beginnen met `sp_`.

Gebruik de volgende procedure om een Configuration Manager rapport op basis van SQL te maken.

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **rapportage**uit en selecteer het knoop punt **rapporten** .

1. Op het tabblad **Start** van het lint, in de sectie **maken** , selecteert u **rapport maken**. Met deze actie wordt de **wizard Rapport maken**geopend.

1. Configureer op de pagina **informatie** de volgende instellingen:

    - **Type**: Selecteer het **rapport op basis van SQL**.

    - **Naam**: Geef een naam op voor het rapport.

    - **Beschrijving**: Geef een beschrijving op voor het rapport.

    - **Server**: geeft de naam weer van de rapport server waarop u dit rapport maakt.

    - **Pad**: Selecteer **Bladeren** om een map op te geven waarin u het rapport wilt opslaan.

1. Voltooi de wizard Rapport maken.

1. Open Report Builder om de rapport instellingen te configureren. Zie [een Configuration Manager rapport bewerken](#bkmk_edit)voor meer informatie.

1. Geef in Report Builder de SQL-instructie voor het rapport op. U kunt ook de SQL-instructie bouwen met behulp van kolommen in beschik bare weer gaven. Indien nodig voegt u para meters aan het rapport toe.

1. Selecteer **uitvoeren** om het rapport uit te voeren. Controleer of het rapport de informatie bevat die u verwacht. Selecteer zo nodig **ontwerp** om het rapport verder te wijzigen.

1. Selecteer **Opslaan** om het rapport op de rapport server op te slaan.

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a>Rapport abonnementen beheren

Met rapport abonnementen in SQL Server Reporting Services kunt u de automatische levering van opgegeven rapporten per e-mail of naar een bestands share op geplande intervallen configureren. Als u rapport abonnementen wilt configureren, gebruikt u de **wizard abonnement maken** in Configuration Manager.

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Een rapport abonnement maken om een rapport te leveren aan een bestands share

Wanneer u een rapport abonnement maakt om een rapport te leveren aan een bestands share, kopieert Reporting Services het rapport in de opgegeven indeling naar de bestands share die u opgeeft. U kunt zich abonneren op en slechts één rapport per keer bezorgen.

Wanneer u een abonnement maakt dat gebruikmaakt van een bestands share, geeft u een bestaande gedeelde map op als doel. De rapport server maakt de map of netwerk share niet. Wanneer u de doelmap opgeeft in een abonnement, gebruikt u een UNC-pad en neemt u geen afsluitende`\`backslashes () op in het mappad. Het volgende voor beeld is een geldig UNC-pad voor de doelmap `\\server\reportfiles\operations\2001`:.

> [!NOTE]
> Wanneer u het abonnement maakt, geeft u een gebruikers naam en wacht woord op. Dit account moet toegang hebben tot deze share met **Schrijf** machtigingen voor de doelmap.

Met Reporting Services kunnen rapporten in verschillende bestands indelingen worden weer gegeven. Bijvoorbeeld MHTML of Excel. U selecteert de indeling wanneer u het abonnement maakt. Hoewel u een ondersteunde weer gave-indeling kunt selecteren, werken sommige indelingen beter dan bij andere rendering van een bestand.

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>Beperkingen voor rapport abonnementen op een bestands share

De volgende lijst bevat de beperkingen van rapport abonnementen op een bestands share:

- In tegens telling tot rapporten die u host en beheert op een rapport server, levert Reporting Services rapporten aan een gedeelde map als statische bestanden.

- Interactieve functies van het rapport werken niet voor rapporten die als bestanden zijn opgeslagen. Het rapport vertegenwoordigt alle interactieve functies als statische elementen.

- Als het rapport grafieken bevat, wordt de standaard presentatie gebruikt.

- Als het rapport is gekoppeld aan een ander rapport, wordt de koppeling als statische tekst weer gegeven.

Als u interactieve functies in een geleverd rapport wilt blijven gebruiken, gebruik dan e-mail bezorging. Zie [een rapport abonnement maken om een rapport via e-mail te leveren](#bkmk_subscription-email)voor meer informatie.

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>Proces voor het maken van een rapport abonnement voor een bestands share

Gebruik de volgende procedure om een rapport abonnement te maken voor het leveren van een rapport aan een bestands share.  

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **rapportage**uit en selecteer het knoop punt **rapporten** .

1. Selecteer een rapportmap en selecteer vervolgens het rapport waarop u zich wilt abonneren. Selecteer op het tabblad **Start** van het lint in de sectie **rapport groep** de optie **abonnement maken**. Met deze actie wordt de **wizard abonnement maken**geopend.

1. Configureer de volgende instellingen op de pagina **bezorgings abonnementen** :  

    - **Rapport geleverd door**: Selecteer **Windows-bestands share**.

    - **Bestands naam**: Geef de bestands naam voor het rapport op. Het rapport bestand bevat standaard geen bestandsnaam extensie. Selecteer **bestands extensie toevoegen wanneer** deze is gemaakt om automatisch een bestandsnaam extensie toe te voegen op basis van de indeling.

    - **Pad**: Geef een UNC-pad op naar een bestaande map waar u dit rapport wilt leveren. Bijvoorbeeld `\\server\reportfiles\operations`.

    - **Weer gave-indeling**: Selecteer een van de volgende indelingen voor het rapport bestand:

      - **XML-bestand met rapport gegevens**
      - **CSV (door komma's gescheiden)**
      - **TIFF-bestand**
      - **PDF-bestand (Acrobat)**
      - **HTML 4,0**
        > [!NOTE]
        > Als uw rapport afbeeldingen bevat, bevat de HTML 4,0-indeling deze niet.
      - **MHTML (webarchief)**
      - **Rpl-renderer** (rapport pagina-indeling)
      - **Excel**
      - **Word**

    - **Gebruikers naam**: Geef een Windows-gebruikers account met *Schrijf* machtigingen op voor het opgegeven **pad**.

    - **Wacht woord**: Geef het wacht woord voor het bovenstaande Windows-gebruikers account op.

    - **Overschrijf optie**: Selecteer een van de volgende opties om het gedrag te configureren wanneer een bestand met dezelfde naam bestaat in de doelmap:

      - **Een bestaand bestand overschrijven met een nieuwere versie**
      - **Een bestaand bestand niet overschrijven**
      - **Bestands namen laten oplopen als nieuwe versies worden toegevoegd**: met deze optie wordt een getal toegevoegd aan de bestands naam van het nieuwe rapport om het te onderscheiden van eerdere versies.

    - **Beschrijving**: Geef desgewenst aanvullende informatie op over dit rapport abonnement.

1. Selecteer op de pagina **abonnements schema** een van de volgende opties voor het bezorgings schema voor het rapport abonnement:

    - **Gedeelde planning gebruiken**: een gedeelde planning is een eerder gedefinieerde planning die door andere rapport abonnementen kan worden gebruikt. Wanneer u deze optie selecteert, moet u ook een gedeelde planning selecteren. Als er geen gedeelde schema's zijn, selecteert u de optie om een nieuwe planning te maken.

    - **Nieuwe planning maken**: Configureer de planning waarmee dit rapport wordt uitgevoerd. De planning bevat het interval, de start tijd en de datum, en de eind datum voor dit abonnement. Standaard maakt een nieuw abonnement een nieuw schema dat elke uur wordt uitgevoerd, te beginnen bij de huidige datum en tijd.

1. Geef op de pagina **abonnements parameters** alle para meters op die dit rapport vereist om zonder toezicht uit te voeren. Als het rapport geen para meters heeft, wordt deze pagina niet weer gegeven in de wizard.

1. Voltooi de wizard.

1. Controleer of Configuration Manager het rapport abonnement hebt gemaakt. Selecteer het knoop punt **abonnementen** om rapport abonnementen weer te geven en te wijzigen.

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a>Een rapport abonnement maken om een rapport via e-mail te leveren

Wanneer u een rapport abonnement maakt om een rapport per e-mail te leveren, stuurt Reporting Services een e-mail bericht naar de ontvangers die u configureert. Het e-mail bericht bevat het rapport als bijlage. De rapport server valideert geen e-mail adressen of ontvangt deze van een e-mail server. U kunt rapporten verzenden naar een geldig e-mail account binnen of buiten uw organisatie.

> [!NOTE]
> Als u de optie **e-mail** abonnement wilt inschakelen, moet u de e-mail instellingen configureren in Reporting Services. Zie [e-mail bezorging in Reporting Services](https://docs.microsoft.com/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services)voor meer informatie.

U kunt een of beide van de volgende bezorgings opties voor e-mail selecteren:

- Een melding verzenden met een koppeling naar het gegenereerde rapport.

- Een Inge sloten of bijgevoegd rapport verzenden. De indeling en browser bepalen of het rapport wordt Inge sloten of gekoppeld.

  - Als uw browser HTML 4,0 en MHTML ondersteunt en u de indeling **MHTML (webarchief)** selecteert, wordt het rapport in het bericht in de e-mail Inge sloten.
  - Alle andere indelingen leveren rapporten als bijlagen.
  - Reporting Services controleert de grootte van de bijlage of het bericht niet voordat het rapport wordt verzonden. Als de bijlage of het bericht de Maxi maal toegestane limiet van uw e-mail server overschrijdt, wordt het rapport niet bezorgd.

Gebruik de volgende procedure om een rapport abonnement te maken voor het leveren van een rapport via e-mail.  

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **rapportage**uit en selecteer het knoop punt **rapporten** .

1. Selecteer een rapportmap en selecteer vervolgens het rapport waarop u zich wilt abonneren. Selecteer op het tabblad **Start** van het lint in de sectie **rapport groep** de optie **abonnement maken**. Met deze actie wordt de **wizard abonnement maken**geopend.

1. Configureer de volgende instellingen op de pagina **bezorgings abonnementen** :  

    - **Rapport geleverd door**: **E-mail**selecteren.

    - **Aan**: Geef een geldig e-mail adres op als ontvanger.

        > [!NOTE]
        > Als u meerdere ontvangers wilt invoeren, scheidt u elk e-`;`mail adres met een punt komma ().

    - **CC**: Geef eventueel een e-mail adres op om een kopie van dit rapport te ontvangen.

    - **BCC**: Geef eventueel een e-mail adres op om een blinde kopie van dit rapport te ontvangen.

    - **Beantwoorden**: Geef het antwoord adres op. Als de ontvanger het e-mail bericht beantwoordt, gaat het antwoord naar dit adres.

    - **Onderwerp**: Geef een onderwerpregel op voor het e-mail bericht voor het abonnement.

    - **Prioriteit**: Selecteer de prioriteits markering voor dit e-mail bericht: **laag**, **normaal**of **hoog**. Micro soft Exchange gebruikt deze vlag om het belang van het e-mail bericht aan te geven.

    - **Opmerking**: Geef de tekst voor de hoofd tekst van het e-mail bericht van het abonnement op.

    - **Beschrijving**: Geef desgewenst aanvullende informatie op over dit rapport abonnement.

    - **Koppeling toevoegen**: Neem de URL voor dit rapport op in de hoofd tekst van het e-mail bericht.

    - **Rapport toevoegen**: koppel het rapport aan het e-mail bericht. Gebruik de optie **weergave formaat** om de rapport indeling op te geven die moet worden gekoppeld.

    - **Weer gave-indeling**: Selecteer een van de volgende indelingen voor het bijgevoegde rapport bestand:

      - **XML-bestand met rapport gegevens**
      - **CSV (door komma's gescheiden)**
      - **TIFF-bestand**
      - **PDF-bestand (Acrobat)**
      - **MHTML (webarchief)**
      - **Excel**
      - **Word**

1. Selecteer op de pagina **abonnements schema** een van de volgende opties voor het bezorgings schema voor het rapport abonnement:

    - **Gedeelde planning gebruiken**: een gedeelde planning is een eerder gedefinieerde planning die door andere rapport abonnementen kan worden gebruikt. Wanneer u deze optie selecteert, moet u ook een gedeelde planning selecteren. Als er geen gedeelde schema's zijn, selecteert u de optie om een nieuwe planning te maken.

    - **Nieuwe planning maken**: Configureer de planning waarmee dit rapport wordt uitgevoerd. De planning bevat het interval, de start tijd en de datum, en de eind datum voor dit abonnement. Standaard maakt een nieuw abonnement een nieuw schema dat elke uur wordt uitgevoerd, te beginnen bij de huidige datum en tijd.

1. Geef op de pagina **abonnements parameters** alle para meters op die dit rapport vereist om zonder toezicht uit te voeren. Als het rapport geen para meters heeft, wordt deze pagina niet weer gegeven in de wizard.

1. Voltooi de wizard.

1. Controleer of Configuration Manager het rapport abonnement hebt gemaakt. Selecteer het knoop punt **abonnementen** om rapport abonnementen weer te geven en te wijzigen.

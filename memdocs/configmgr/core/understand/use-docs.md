---
title: De documenten gebruiken
titleSuffix: Configuration Manager
description: Meer tips over het gebruik van de bibliotheek met Configuration Manager technische documentatie.
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aca3322c245fa22a7c87f30e328833d8a8a128bc
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699038"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>De Configuration Manager docs gebruiken

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u bronnen en tips voor het gebruik van de documentatie bibliotheek van Configuration Manager.

- Zoeken
- Document fouten, uitbrei dingen, vragen en nieuwe ideeën verzenden
- Hoe kan ik op de hoogte worden gebracht van wijzigingen
- Bijdragen aan documenten

Zie [Help zoeken](find-help.md)voor algemene hulp bij het product.

## <a name="search"></a><a name="bkmk_searchtips"></a> Opdracht

Gebruik de volgende zoektips om de benodigde informatie te vinden:

- Wanneer u uw favoriete zoek machine gebruikt om inhoud te zoeken voor Configuration Manager, kunt u `ConfigMgr` uw zoek woorden samen voegen.

  - Zoek naar resultaten van `docs.microsoft.com/mem/configmgr` voor Configuration Manager huidige vertakking. De resultaten van `docs.microsoft.com/previous-versions` zijn voor oudere product versies.

  - Als u de zoek resultaten verder wilt richten op de huidige inhouds bibliotheek, neemt `site:docs.microsoft.com` u de zoek machine op als bereik.

- Gebruik zoek termen die overeenkomen met de terminologie in de gebruikers interface en online documentatie. Vermijd onofficiële voor waarden of afkortingen die u kunt zien in de Community-inhoud. Zoek bijvoorbeeld naar:

  - ' beheer punt ' in plaats van ' MP '
  - ' implementatie type ' in plaats van ' DT '
  - ' software-updates ' in plaats van ' SUM '

- Als u in het huidige artikel wilt zoeken, gebruikt u de **Zoek** functie van uw browser. Bij de meeste moderne webbrowsers drukt u op **CTRL** + **F** en voert u de zoek termen in.

- Elk artikel op `docs.microsoft.com` bevat de volgende velden om te helpen bij het zoeken naar de inhoud:

  - **Zoek** in de rechter bovenhoek. Als u alle artikelen wilt doorzoeken, voert u voor waarden in dit veld in. De artikelen in de Configuration Manager-bibliotheek bevatten automatisch het `ConfigMgr` bereik om deze documentatie bibliotheek alleen te doorzoeken.

  - **Filteren op titel** boven de inhouds opgave links. Als u wilt zoeken in de huidige inhouds opgave, voert u voor waarden in dit veld in. Dit veld komt alleen overeen met de voor waarden die worden weer gegeven in de titel van het artikel voor het huidige knoop punt. Bijvoorbeeld: **kern infrastructuur** ( `docs.microsoft.com/configmgr/core` ) of **toepassings beheer** ( `docs.microsoft.com/configmgr/apps` ).

- Ondervindt u problemen met het vinden van iets? [Feedback over bestanden.](#bkmk_docfeedback) Wanneer u het probleem opslaat, geeft u de zoek machine op die u wilt gebruiken, de tref woorden die u hebt geprobeerd en het doel artikel. Deze feedback helpt micro soft bij het optimaliseren van de inhoud voor betere zoek mogelijkheden.

> [!TIP]
> Vanaf Configuration Manager versie 1902 is er een **documentatie** knooppunt in de nieuwe werk ruimte van de **Community** van de Configuration Manager-console. Dit knoop punt bevat actuele informatie over Configuration Manager documentatie en ondersteunings artikelen. Zie [de Configuration Manager-console gebruiken](../servers/manage/admin-console.md#bkmk_doc-dashboard)voor meer informatie.

## <a name="feedback"></a><a name="bkmk_docfeedback"></a> Feedback

Selecteer de koppeling **feedback** in de rechter bovenhoek van een artikel om naar de sectie feedback onderaan te gaan. Deze sectie is geïntegreerd met GitHub-problemen. Zie het [blog bericht](/teamblog/a-new-feedback-system-is-coming-to-docs)over het docs-platform voor meer informatie over de integratie met github-problemen.

Selecteer **product feedback**om feedback te geven over het Configuration Manager product zelf. Zie [product feedback](find-help.md#product-feedback)voor meer informatie.

Een [github-account](https://github.com/join) is een vereiste om documentatie feedback te geven. Nadat u zich hebt aangemeld, is er een eenmalige autorisatie voor de MicrosoftDocs-organisatie. Wanneer u vervolgens **inhouds feedback**selecteert, voert u een titel en een opmerking in en **verzendt u feedback**. Met deze actie wordt een nieuw probleem voor het doel artikel in de [SCCMdocs-opslag plaats](https://github.com/MicrosoftDocs/SCCMdocs/issues).

In deze integratie worden ook eventuele bestaande openstaande of gesloten problemen voor het doel artikel weer gegeven. Als dat het geval is, raadpleegt u deze voordat u een nieuw probleem verzendt. Als u een verwant probleem vindt, selecteert u het gezichts pictogram om een reactie toe te voegen, of u kunt het uitbreiden om een opmerking toe te voegen.

#### <a name="types-of-feedback"></a>Typen feedback

Gebruik GitHub-problemen om de volgende typen feedback in te dienen:

- Doc-fout: de inhoud is verouderd, onduidelijk, verwarrend of beschadigd.
- Document verbetering: een suggestie voor het verbeteren van het artikel.
- Doc-vraag: u hebt hulp nodig bij het zoeken van bestaande documentatie.
- Document idee: een suggestie voor een nieuw artikel. Gebruik deze methode in plaats van UserVoice voor documentatie feedback.
- Kudos: positieve feedback over een nuttig of informatieve artikel!
- Lokalisatie: feedback over inhouds vertalingen.
- Optimalisatie van zoek machines (SEO): feedback over problemen met het zoeken naar inhoud. Neem de zoek machine, tref woorden en het doel artikel op in de opmerkingen.

Als u een probleem voor niet-document-gerelateerde onderwerpen maakt, worden de problemen gesloten. Bijvoorbeeld:

- [Productfeedback](find-help.md#product-feedback)
- [Product vragen](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [Ondersteuningsaanvragen](https://aka.ms/cmcbsupport)

Zie [opmerkingen over docs](https://aka.ms/sitefeedback)voor informatie over het delen van feedback op het belangrijkste docs.Microsoft.com-platform. Het platform bevat alle wrapper-onderdelen, zoals de koptekst, de inhouds opgave en het rechter menu. Ook hoe de artikelen worden weer gegeven in de browser, zoals het letter type, de waarschuwings vakken en pagina ankers.

## <a name="notifications"></a><a name="bkmk_notifications"></a> Meldingen

Als u meldingen wilt ontvangen wanneer inhoud in de documentatie bibliotheek wordt gewijzigd, gebruikt u de volgende stappen:

1. Gebruik de [docs-zoek opdracht](/search/index?scope=ConfigMgr) om een artikel of set artikelen te vinden. Bijvoorbeeld:

    - Zoeken naar één artikel op titel, [logboek bestanden voor probleem oplossing-Configuration Manager](/search/index?scope=ConfigMgr&search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22)

    - Zoeken naar artikelen over [SQL](/search/index?scope=ConfigMgr&search=SQL)

2. Selecteer in de rechter bovenhoek de koppeling **RSS** .

3. Gebruik deze feed in een RSS-toepassing om meldingen te ontvangen wanneer er een wijziging is in een van de zoek resultaten.

> [!TIP]
> U kunt ook de [SCCMdocs-opslag plaats](https://github.com/MicrosoftDocs/SCCMdocs) **bekijken** op github. Met deze methode worden veel meldingen gegenereerd. Het bevat ook geen wijzigingen van een privé-opslag plaats die wordt gebruikt door micro soft.

## <a name="contribute"></a><a name="bkmk_contribute"></a> Noteer

De documentatie bibliotheek Configuration Manager, zoals de meeste inhoud op docs.microsoft.com, is open source op GitHub. In deze bibliotheek worden de bijdragen van de Community geaccepteerd en aangemoedigd. Zie de [gids voor inzenders](/contribute)voor meer informatie over hoe u aan de slag kunt gaan. De enige vereiste is het maken van een [github-account](https://github.com/join).

### <a name="basic-steps-to-contribute-to-sccmdocs"></a>Basis stappen voor het bijdragen aan SCCMdocs

1. Selecteer in het doel artikel **bewerken**. Met deze actie wordt het bron bestand geopend in GitHub.

2. Als u het bron bestand wilt bewerken, selecteert u het potlood pictogram.

3. Wijzigingen aanbrengen in de bron voor de prijs verlaging. Zie voor meer informatie de [korting gebruiken voor het schrijven van docs](/contribute/markdown-reference).

4. Voer in de sectie bestands wijziging Voorst Ellen de open bare opmerking in die beschrijft *wat* u hebt gewijzigd. Selecteer vervolgens **Bestands wijziging**Voorst Ellen.

5. Schuif omlaag en controleer de wijzigingen die u hebt aangebracht. Selecteer **pull-aanvraag maken** om het formulier te openen. Geef aan *Waarom* u deze wijziging hebt aangebracht. Codeer de auteur van het artikel en vraag deze te beoordelen. Selecteer **pull-aanvraag maken**.

### <a name="what-to-contribute"></a>Wat u moet bijdragen

Als u een bijdrage wilt leveren, maar niet weet waar u moet beginnen, raadpleegt u de volgende suggesties:

- Zoek in de lijst met problemen naar de Community-doel etiketten:

  - [goed-eerste-probleem](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [hulp gewenst](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Micro soft-auteurs wijzen deze labels toe aan problemen die goede kandidaten zijn voor de bijdrage van de community.

- Bekijk een artikel op nauw keurigheid. Werk vervolgens de **MS. date** -meta gegevens bij met de `mm/dd/yyyy` indeling. Deze bijdrage helpt de inhoud te vernieuwen.

- Voeg uitleg, voor beelden of richt lijnen toe op basis van uw ervaring. Deze bijdrage maakt gebruik van de kracht van de community om kennis te delen.

- Corrigeer vertalingen in een niet-Engelse taal. Deze bijdrage verbetert de bruikbaarheid van gelokaliseerde inhoud.

> [!NOTE]
> Als u geen micro soft-werk nemer bent, moet u voor grote bijdragen een contributie licentie overeenkomst (CLA) ondertekenen. GitHub vereist automatisch dat u deze overeenkomst moet ondertekenen wanneer een bijdrage voldoet aan de drempel waarde.

### <a name="tips"></a>Tips

Volg deze algemene richt lijnen wanneer u bijdraagt aan Configuration Manager documenten:

- Zorg dat u geen grote pull-aanvragen verwacht. In plaats daarvan [een probleem in het bestand op te lossen](#bkmk_docfeedback) en een discussie te starten. Vervolgens kunnen we akkoord gaan met de richting voordat u een grote hoeveelheid tijd belegt.

- Lees de [micro soft-stijl gids](https://aka.ms/MicrosoftStyle). De [10 belangrijkste tips voor micro soft-stijl en-stem](/style-guide/top-10-tips-style-voice).

- Gebruik de [sjabloon voor pull-aanvragen](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md) als uitgangs punt voor uw werk.

- Volg de [werk stroom](https://guides.github.com/introduction/flow/)van de GitHub-stroom.

- Blog en Tweet (of wat) over uw bijdragen, regel matig!

(Deze lijst is geleend uit de [gids voor .net-bijdragen](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts).)

## <a name="consolidation-of-documentation-for-microsoft-endpoint-manager"></a>Consolidatie van documentatie voor micro soft Endpoint Manager

Voor betere ondersteuning van gecombineerde scenario's voor intune en Configuration Manager worden de documentatie bibliotheken geconsolideerd op de [micro soft-site voor eindpunt beheer](/mem). De intune-documentatie is nu op [docs.Microsoft.com/mem/intune](../../../intune/index.yml)en de Configuration Manager documentatie is nu op [docs.Microsoft.com/mem/ConfigMgr](../../index.yml). Als u nog steeds een oude URL gebruikt, wordt deze automatisch omgeleid, zodat u geen wijzigingen hoeft aan te brengen voor het lezen van deze inhoud.

Als u feedback geeft of een bijdrage levert aan artikelen, zijn er nog enkele wijzigingen nodig:

- Bestaande GitHub-problemen blijven in de oorspronkelijke opslag plaats, [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) of [SCCMDocs](https://github.com/MicrosoftDocs/SCCMDocs/issues).

  - Deze problemen worden niet weer gegeven als open of gesloten problemen in het gedeelte feedback van het gekoppelde artikel.

  - We blijven werken om deze problemen op te lossen.

  - In sommige gevallen kunnen we de moeilijkste beslissing nemen om een probleem op te lossen dat wij niet kunnen verhelpen.

  - Als u een probleem hebt in de bestaande opslag plaats en er enthousiast over hebt, kunt u feedback geven over het gemigreerde artikel in de [MEMDocs-opslag plaats](https://github.com/MicrosoftDocs/MEMDocs).

- Wanneer u nu feedback hebt gegeven of een artikel bewerkt, gaat het probleem of de pull-aanvraag naar de MEMDocs-opslag plaats.
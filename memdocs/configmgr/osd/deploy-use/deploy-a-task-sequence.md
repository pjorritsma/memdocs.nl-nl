---
title: Een takenreeks implementeren
titleSuffix: Configuration Manager
description: Gebruik deze informatie om een taken reeks te implementeren op de computers in een verzameling.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c16e89cc75bff1ccecd03a98cd12782c419a40
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455154"
---
# <a name="deploy-a-task-sequence"></a>Een takenreeks implementeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u een taken reeks hebt gemaakt en de inhoud hebt gedistribueerd, implementeert u deze in een verzameling apparaten. Met deze actie kan de taken reeks op een apparaat worden uitgevoerd. Een geïmplementeerde taken reeks kan automatisch worden uitgevoerd of wanneer deze wordt geïnstalleerd door een gebruiker van het apparaat.

> [!WARNING]  
> U kunt het gedrag voor de implementatie van takenreeksen met een hoge risico beheren. Een implementatie met een hoog risico is een implementatie die automatisch wordt geïnstalleerd en de potentie heeft om ongewenste resultaten te veroorzaken. Een taken reeks met het doel **vereist** voor het implementeren van een besturings systeem wordt bijvoorbeeld beschouwd als een implementatie met een hoog risico. Zie [instellingen voor het beheren van implementaties met een hoog risico](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.  

## <a name="process"></a>Proces

Gebruik de volgende procedure om een takenreeks te implementeren voor de computers in een verzameling.  

> [!NOTE]  
> De status berichten voor de taken reeks implementatie worden weer gegeven in het bericht venster op een primaire site, maar ze worden niet weer gegeven op een centrale beheer site.  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **taken reeksen** .  

2. Selecteer in de lijst **Takenreeks** de takenreeks die u wilt implementeren.  

3. Klik op het tabblad **Start** van het lint in de groep **implementatie** op **implementeren**.  

    > [!NOTE]  
    > Als **implementeren** niet beschikbaar is, bevat de taken reeks een ongeldige verwijzing. Corrigeer de verwijzing en probeer vervolgens opnieuw of u de takenreeks kunt implementeren.  

4. Geef op de pagina **Algemeen** de volgende informatie op.  

    - **Taken reeks**: Geef de taken reeks op die u wilt implementeren. In dit vak wordt standaard de geselecteerde taken reeks weer gegeven.  

    - **Verzameling**: Selecteer de verzameling die de computers bevat waarop de taken reeks moet worden uitgevoerd.  

        Implementeer geen taken reeks waarmee een besturings systeem wordt geïnstalleerd op ongepaste verzamelingen, zoals een verzameling van al uw Data Center-servers. Zorg ervoor dat de geselecteerde verzameling alleen de computers bevat waarop u de taken reeks wilt uitvoeren.  

        Zie [implementaties met een hoog risico](#bkmk_high-risk)voor meer informatie over implementaties met een hoog risico.

    - **Standaard distributiepunten groepen gebruiken die aan deze verzameling zijn gekoppeld**: Sla de taken reeks inhoud op in de standaard distributiepunten groep van de verzameling. Als u de geselecteerde verzameling niet hebt gekoppeld aan een distributiepunten groep, wordt deze optie grijs weer gegeven.  

    - **Inhoud voor afhankelijkheden automatisch distribueren**: als een inhoud waarnaar wordt verwezen, afhankelijkheden heeft, verzendt de site ook afhankelijke inhoud naar distributie punten.  

    - **Inhoud voor deze taken reeks vooraf downloaden**: Zie [inhoud van vóór de cache configureren](configure-precache-content.md)voor meer informatie.  

    - **Implementatie sjabloon selecteren**: Sla een implementatie sjabloon op voor een taken reeks en geef deze op.<!--1357391-->  

        > [!IMPORTANT]  
        > Sommige items worden niet in de sjabloon opgeslagen.<!--510610--> Zorg ervoor dat u de volgende items toepast wanneer u de implementatie wizard uitvoert:  
        >
        > - Software-installatie
        > - Planning
        > - Inhoud vooraf downloaden

    - **Opmerkingen (optioneel)**: geef aanvullende informatie op die deze implementatie van de takenreeks beschrijft.  

5. Geef op de pagina **implementatie-instellingen** de volgende informatie op:  

    - **Doel**: kies in de vervolgkeuzelijst één van de volgende opties:  

        - **Beschikbaar**: de gebruiker ziet de taken reeks in Software Center en kan deze op aanvraag installeren.  

        - **Vereist**: de taken reeks wordt door Configuration Manager automatisch uitgevoerd volgens de geconfigureerde planning. Als de taken reeks niet verborgen is, kan een gebruiker de implementatie status nog steeds volgen. Ze kunnen ook software Center gebruiken om de taken reeks vóór de deadline te installeren.  

        > [!NOTE]
        > Als meerdere gebruikers zijn aangemeld bij het apparaat, worden er mogelijk geen pakket-en taken reeks implementaties weer gegeven in Software Center.  

    - **Beschikbaar maken voor de volgende**: Geef op of de taken reeks beschikbaar is voor een van de volgende typen:  

        - Alleen Configuration Manager-clients  
        - Configuration Manager-clients, media en PXE  
        - Alleen media en PXE  
        - Alleen media en PXE (verborgen)  

        > [!IMPORTANT]  
        > Gebruik de instelling **Alleen media en PXE (verborgen)** voor geautomatiseerde implementaties van takenreeksen. Selecteer **implementatie van besturings systeem zonder toezicht toestaan** en stel de variabele **SMSTSPreferredAdvertID** in als onderdeel van de media om de computer automatisch te laten opstarten naar de implementatie zonder tussen komst van de gebruiker. Zie [taken reeks variabelen](../understand/task-sequence-variables.md#SMSTSPreferredAdvertID)voor meer informatie over taken reeks variabelen.  

    - **Ontwaak pakketten verzenden**: als de implementatie **vereist** is en u deze optie selecteert, stuurt de site een Ontwaak pakket naar computers voordat de client de implementatie uitvoert. Met dit pakket wordt de computer uit de slaap stand gehaald tijdens de deadline van de installatie. Voordat u deze optie kunt gebruiken, moeten computers en netwerken worden geconfigureerd voor Wake On LAN. Zie [plan How to wake up clients](../../core/clients/deploy/plan/plan-wake-up-clients.md)(Engelstalig) voor meer informatie.  

    - **Clients met een Internet verbinding naar gebruik toestaan inhoud te downloaden na de installatie deadline, waarvoor extra kosten in rekening kunnen**worden gebracht: deze optie is alleen beschikbaar voor **vereiste** implementaties. Wanneer u een aangepaste taken reeks hebt waarmee een toepassing wordt geïnstalleerd, maar die geen besturings systeem implementeert, kunt u opgeven of u wilt toestaan dat clients inhoud downloaden na een installatie deadline wanneer deze Internet verbindingen met een Data limiet gebruiken. Internet providers worden soms kosten in rekening gebracht op basis van de hoeveelheid gegevens die u gebruikt wanneer u gebruikmaakt van een Internet verbinding met data limiet.  

        > [!NOTE]  
        > Hoewel het gebruik van een Internet verbinding met data limiet mogelijk werkt voor taken reeksen die geen besturings systeem implementeren, wordt dit niet ondersteund.  

6. Geef op de pagina **planning** de volgende informatie op:  

    > [!IMPORTANT]  
    > Wanneer een Windows PE-client wordt gestart vanaf PXE-of opstart media, evalueert de client geen implementatie planningen. Deze schema's zijn onder andere start-, verval-en deadline tijden. Configureer alleen schema's in implementaties naar clients die beginnen met het volledige Windows-besturings systeem. Overweeg het gebruik van andere methoden, zoals onderhoudvensters, waarmee reeksen actieve taken worden beheerd die geïmplementeerd zijn op clients die starten vanaf Windows PE.  

    - **Plannen wanneer deze implementatie beschikbaar wordt**: geef de datum en tijd wanneer de takenreeks beschikbaar is om te worden uitgevoerd op de doelcomputer. Wanneer u de optie **UTC** selecteert, is de taken reeks beschikbaar voor meerdere computers tegelijk. Anders is de implementatie beschikbaar op verschillende tijdstippen, volgens de lokale tijd op elke computer.  

        Als de begin tijd eerder is dan de vereiste tijd, downloadt de client de inhoud van de taken reeks op de start tijd.  

    - **Plannen wanneer deze implementatie zal verlopen**: geef de datum en tijd wanneer de takenreeks op de doelcomputer verloopt. Wanneer u de optie **UTC** selecteert, verloopt de taken reeks op meerdere doel computers tegelijk. Anders verloopt de implementatie op verschillende tijdstippen, op basis van de lokale tijd op elke computer.  

    - **Toewijzings planning**: Geef voor een **vereiste** implementatie op wanneer de client de taken reeks uitvoert. U kunt meerdere planningen toevoegen. De toewijzings planning kan een van de volgende configuraties hebben:  

        - Een specifieke datum en tijd  
        - Maandelijks, wekelijks of aangepast terugkeer patroon  
        - Zo snel mogelijk  
        - Aanmelden of gebeurtenissen afmelden  

        > [!NOTE]  
        > Als u een begin tijd plant voor een vereiste implementatie die ouder is dan de datum en tijd waarop de taken reeks beschikbaar is, downloadt de Configuration Manager-client de inhoud op de toegewezen begin tijd. Dit gedrag treedt ook op als u hebt gepland dat de taken reeks op een later tijdstip beschikbaar is.<!--SCCMDocs issue 777-->  

    - **Gedrag voor opnieuw uitvoeren**: Geef op wanneer de taken reeks opnieuw wordt uitgevoerd. Selecteer één van de volgende opties:  

        - **Geïmplementeerd programma nooit opnieuw uitvoeren**: als de client eerder de taken reeks heeft uitgevoerd, wordt deze niet opnieuw gestart. De taken reeks wordt niet opnieuw uitgevoerd, zelfs als deze oorspronkelijk is mislukt of als de taken reeks bestanden zijn gewijzigd.  

        - **Programma altijd opnieuw uitvoeren**: de taken reeks wordt altijd opnieuw uitgevoerd op de client wanneer de implementatie is gepland. Deze wordt uitgevoerd, zelfs als de taken reeks al is uitgevoerd. Deze instelling is nuttig wanneer u herhaalde implementaties gebruikt waarbij de taken reeks regel matig wordt bijgewerkt.  

            > [!IMPORTANT]  
            > Deze optie is standaard ingeschakeld. Het heeft echter geen effect totdat u een vereiste implementatie toewijst. Een gebruiker kan altijd beschik bare implementaties opnieuw uitvoeren.  

        - **Opnieuw uitvoeren als de vorige poging is mislukt**: de taken reeks wordt opnieuw uitgevoerd wanneer de implementatie is gepland, alleen als deze eerder niet kon worden uitgevoerd. Deze instelling is nuttig voor een vereiste implementatie. Als de laatste poging om uit te voeren is mislukt, wordt automatisch geprobeerd om te herhalen volgens de toewijzings planning.  

        - **Opnieuw uitvoeren als de vorige poging is gelukt**: de taken reeks wordt alleen opnieuw uitgevoerd als deze eerder is uitgevoerd op de client. Deze instelling is bijzonder nuttig wanneer u herhaalde implementaties gebruikt waarbij de takenreeks regelmatig wordt bijgewerkt en waarbij het voor elke update vereist is dat de vorige update is geïnstalleerd.  

        > [!NOTE]  
        > Een gebruiker kan een beschik bare taken reeks implementatie opnieuw uitvoeren. Voordat u een beschik bare taken reeks implementeert in een productie omgeving, moet u eerst testen wat er gebeurt als een gebruiker de taken reeks meerdere keren uitvoert.  

7. Geef op de pagina **Gebruikerservaring** de volgende informatie:  

    - **Gebruiker toestaan het programma onafhankelijk van toewijzingen uit te voeren**: Geef op of een gebruiker een vereiste implementatie mag uitvoeren buiten de toewijzings planning. Deze optie is altijd ingeschakeld voor beschik bare implementaties.  

    - **Voortgang van taken reeks weer geven**: Geef op of de Configuration Manager-client de voortgang van de taken reeks weergeeft.  

    - **Software-installatie**: Geef op of de gebruiker software mag installeren buiten een geconfigureerd onderhouds venster na de geplande tijd.  

    - **Systeem opnieuw opstarten (indien dit is vereist om de installatie te voltooien)**: geef op of de gebruiker de computer na een software-installatie buiten een geconfigureerd onderhoudsvenster na de toegewezen periode opnieuw mag opstarten.  

    - **Verwerking van schrijf filters voor Windows Embedded-apparaten**: met deze instelling bepaalt u het installatie gedrag op Windows Embedded-apparaten waarvoor een schrijf filter is ingeschakeld. Kies de optie om wijzigingen door te voeren bij de deadline van de installatie of tijdens een onderhouds venster. Wanneer u deze optie selecteert, moet de computer opnieuw worden opgestart en worden de wijzigingen op het apparaat bewaard. Anders wordt de toepassing geïnstalleerd op de tijdelijke overlay en later vastgelegd. Wanneer u een taken reeks implementeert op een Windows Embedded-apparaat, moet u ervoor zorgen dat het apparaat lid is van een verzameling met een geconfigureerd onderhouds venster.  

    - **Taken reeks mag voor client worden uitgevoerd op Internet**: Geef op of de taken reeks mag worden uitgevoerd op een client op internet. Bewerkingen waarvoor een opstart medium vereist is, zoals de installatie van een besturings systeem, worden niet ondersteund met deze instelling. Gebruik deze optie alleen voor algemene software-installaties of op scripts gebaseerde taken reeksen die bewerkingen uitvoeren in het standaard besturingssysteem.  

        - Deze instelling wordt ondersteund voor implementaties van een Windows 10-in-place upgrade taken reeks naar op internet gebaseerde clients via de Cloud beheer gateway. Zie [Deploying Windows 10 in-place upgrade via CMG](#deploy-windows-10-in-place-upgrade-via-cmg)voor meer informatie.  

8. Geef op de pagina **waarschuwingen** de waarschuwings instellingen op die u wilt voor de implementatie van deze taken reeks.  

9. Geef op de pagina **Distributiepunten** de volgende informatie:  

    - **Implementatie opties**: Zie [implementatie opties](#bkmk_deploy-options)voor meer informatie.

    - **Een extern distributie punt gebruiken wanneer er geen lokaal distributie punt beschikbaar is**: Geef op of clients distributie punten kunnen gebruiken van een grens groep in de nabijheid om de inhoud te downloaden die vereist is voor de taken reeks.  

    - **Clients toestaan distributie punten van de standaard site grens groep te gebruiken**: Geef op of clients inhoud moeten downloaden van een distributie punt in de standaard grens groep van de site, wanneer deze niet beschikbaar is vanaf een distributie punt in de huidige of grens groepen van de buur.  

        > [!Note]  
        > Vanaf versie 1810, wanneer op een apparaat een taken reeks wordt uitgevoerd en inhoud moet worden opgehaald, worden gedragingen van de grens groep gebruikt die vergelijkbaar zijn met de Configuration Manager-client. Zie [taken reeks ondersteuning voor grens groepen](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd)voor meer informatie.<!--1359025-->  

10. Als u deze instellingen opnieuw wilt gebruiken, selecteert u **Opslaan als sjabloon**op het tabblad **samen vatting** . Geef een naam op voor de sjabloon en selecteer de instellingen die u wilt opslaan.  

11. Voltooi de wizard.  

### <a name="deployment-options"></a><a name="bkmk_deploy-options"></a>Implementatie opties

<!-- MEMDocs#328, SCCMDocs#2114 -->

Deze opties bevinden zich op het tabblad **distributie punten** van de taken reeks implementatie. Ze zijn dynamisch op basis van andere selecties in de implementatie en kenmerken van de taken reeks. Het is niet altijd mogelijk om alle opties te zien.

> [!NOTE]  
> Wanneer u multi cast gebruikt om een besturings systeem te implementeren, moet u de inhoud naar de computers downloaden, hetzij naar behoefte, hetzij voordat de taken reeks wordt uitgevoerd.  

- **Inhoud lokaal downloaden wanneer deze nodig is voor de taken reeks die wordt uitgevoerd**: Geef op dat clients inhoud downloaden van het distributie punt, zoals het nodig is voor de taken reeks. De client start de taken reeks. Wanneer een stap in de taken reeks inhoud vereist, wordt deze gedownload voordat de stap wordt uitgevoerd.  

- **Alle inhoud lokaal downloaden voordat de taken reeks wordt gestart**: Hiermee geeft u op dat clients alle inhoud vanaf het distributie punt downloaden voordat de taken reeks wordt uitgevoerd. Als u de taken reeks beschikbaar maakt voor PXE-en opstart media-implementaties op de pagina **implementatie-instellingen** , wordt deze optie niet weer gegeven.  

- **Direct toegang tot inhoud vanaf een distributie punt wanneer dit nodig is voor de taken reeks die wordt uitgevoerd**: Geef op dat clients de inhoud vanaf het distributie punt moeten uitvoeren. Deze optie is alleen beschikbaar wanneer u alle pakketten die aan de taken reeks zijn gekoppeld, inschakelt voor het gebruik van een pakket share op het distributie punt. Zie het tabblad **Gegevenstoegang** in de **eigenschappen** van de afzonderlijke pakketten voor informatie over het inschakelen van inhoud voor het gebruik van een pakketshare.  

> [!IMPORTANT]  
> Voor de beste beveiliging selecteert u de opties om **inhoud lokaal te downloaden wanneer deze nodig is voor de taken reeks die wordt uitgevoerd** , of **alle inhoud lokaal downloaden voordat de taken reeks wordt gestart**. Wanneer u een van deze opties selecteert, Configuration Manager hashes van het pakket, zodat de pakket integriteit kan worden gegarandeerd. Wanneer u de optie selecteert voor het **rechtstreeks openen van inhoud vanaf een distributie punt wanneer dit nodig is voor de taken reeks die wordt uitgevoerd**, controleert Configuration Manager de pakket-hash niet voordat het opgegeven programma wordt uitgevoerd. Omdat de site de pakket integriteit niet kan garanderen, is het mogelijk dat gebruikers met beheerders rechten de pakket inhoud kunnen wijzigen of knoeien.  

#### <a name="example-1-one-deployment-option"></a>Voor beeld 1: één implementatie optie

U implementeert een besturingssysteem implementatie taken reeks waarmee de schijf wordt gewist en een installatie kopie wordt toegepast. Op de pagina **implementatie-instellingen** kunt u deze beschikbaar maken voor een optie die media en PXE bevat:

:::image type="content" source="media/deploy-setting-make-available.png" alt-text="Taken reeks implementeren, beschikbaar maken voor de volgende":::

Op de pagina **distributie punten** is er slechts één implementatie optie:

- **Inhoud lokaal downloaden wanneer deze nodig is voor de taken reeks die wordt uitgevoerd**

:::image type="content" source="media/deploy-option-1.png" alt-text="Taken reeks implementeren, één implementatie optie":::

De optie voor het **lokaal downloaden van alle inhoud voordat de taken reeks wordt gestart** , is niet beschikbaar omdat de implementatie beschikbaar is gemaakt voor media en PXE.

De mogelijkheid om **rechtstreeks vanaf een distributie punt toegang te krijgen tot inhoud, is niet beschikbaar voor de taken reeks die wordt uitgevoerd** . Niet alle inhoud waarnaar wordt verwezen, maakt gebruik van een pakket share.

#### <a name="example-2-two-deployment-options"></a>Voor beeld 2: twee implementatie-opties

U implementeert een besturingssysteem implementatie taken reeks waarmee de schijf wordt gewist en een installatie kopie wordt toegepast. Op de pagina **implementatie-instellingen** kunt u deze alleen beschikbaar maken voor Configuration Manager- **clients**. Er zijn twee implementatie opties beschikbaar op de pagina **distributie punten** :

- **Inhoud lokaal downloaden wanneer deze nodig is voor de taken reeks die wordt uitgevoerd**
- **Alle inhoud lokaal downloaden voordat de taken reeks wordt gestart**

:::image type="content" source="media/deploy-option-2.png" alt-text="Taken reeks implementeren, twee implementatie opties":::

De mogelijkheid om **rechtstreeks vanaf een distributie punt toegang te krijgen tot inhoud, is niet beschikbaar voor de taken reeks die wordt uitgevoerd** . Niet alle inhoud waarnaar wordt verwezen, maakt gebruik van een pakket share.

#### <a name="example-3-three-deployment-options"></a>Voor beeld 3: drie implementatie opties

U hebt verschillende pakketten met beheer scripts en gekoppelde inhoud. Op het tabblad **gegevens toegang** van de pakket eigenschappen configureert u dat allemaal om **de inhoud in dit pakket te kopiëren naar een pakket share op distributie punten**.

U maakt een taken reeks die slechts verschillende **installatie pakket** stappen voor deze script pakketten heeft en de implementatie ervan. Op de pagina **implementatie-instellingen** is de enige optie alleen beschikbaar voor Configuration Manager- **clients**. Deze optie is alleen beschikbaar. De taken reeks is niet voor implementatie van het besturings systeem, omdat er geen opstart installatie kopie aan is gekoppeld. Er zijn drie implementatie opties beschikbaar op de pagina **distributie punten** :

- **Inhoud lokaal downloaden wanneer deze nodig is voor de taken reeks die wordt uitgevoerd**
- **Alle inhoud lokaal downloaden voordat de taken reeks wordt gestart**
- **Direct toegang tot inhoud vanaf een distributie punt wanneer dit nodig is voor de taken reeks die wordt uitgevoerd**

:::image type="content" source="media/deploy-option-3.png" alt-text="Taken reeks implementeren, drie implementatie opties":::

## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Windows 10-in-place upgrade implementeren via CMG

<!-- 1357149 -->
De taken reeks Windows 10 in-place upgrade ondersteunt de implementatie voor clients op Internet die worden beheerd via de [Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG). Met deze mogelijkheid kunnen externe gebruikers eenvoudiger een upgrade uitvoeren naar Windows 10 zonder dat ze verbinding hoeven te maken met het intranet.

Zorg ervoor dat alle inhoud waarnaar wordt verwezen door de in-place upgrade taken reeks, wordt gedistribueerd naar een CMG waarvoor inhoud is ingeschakeld. (Schakel de [instelling CMG](../../core/clients/manage/cmg/setup-cloud-management-gateway.md#settings)in: **CMG als Cloud distributiepunt laten functioneren en inhoud van Azure Storage afleveren**.) U kunt ook een [Cloud distributiepunt](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)gebruiken. Op andere apparaten kan de taken reeks niet worden uitgevoerd.

Wanneer u een upgrade taken reeks implementeert, gebruikt u de volgende instellingen:

- **Taken reeks mag voor client worden uitgevoerd op het Internet**, op het tabblad gebruikers ervaring van de implementatie.  

- Kies een van de volgende opties op het tabblad distributie punten van de implementatie:

  - **Down load de inhoud lokaal wanneer dit nodig is voor de taken reeks die wordt uitgevoerd**. Vanaf versie 1910 kan de engine van de taken reeks pakketten op aanvraag downloaden van een CMG of een Cloud distributiepunt. Deze wijziging biedt extra flexibiliteit met uw Windows 10-in-place upgrade implementaties op apparaten op internet.<!--3601238-->

  - **Alle inhoud lokaal downloaden voordat de taken reeks wordt gestart**. In Configuration Manager versie 1906 en lager, werken andere opties, zoals **het lokaal downloaden van inhoud wanneer dit nodig is voor de taken reeks die wordt uitgevoerd** , niet in dit scenario. De taken reeks engine kan geen inhoud downloaden van een Cloud bron. De Configuration Manager-client moet de inhoud van de Cloud bron downloaden voordat de taken reeks wordt gestart. U kunt deze optie nog steeds gebruiken in versie 1910, indien nodig om aan uw vereisten te voldoen.

- (*Optioneel*) **Down load inhoud vooraf voor deze taken reeks**op het tabblad Algemeen van de implementatie. Zie [inhoud vooraf in cache configureren](configure-precache-content.md)voor meer informatie.  

> [!NOTE]
> Start de taken reeks vanuit software Center. Dit scenario biedt geen ondersteuning voor Windows PE, PXE of taken reeks media.

## <a name="high-risk-deployments"></a><a name="bkmk_high-risk"></a>Implementaties met een hoog risico

Wanneer u een implementatie met een hoog risico implementeert, zoals een besturings systeem, worden in het venster **verzameling selecteren** alleen de aangepaste verzamelingen weer gegeven die voldoen aan de verificatie-instellingen voor de implementatie die zijn geconfigureerd in de eigenschappen van de site. Implementaties met een hoog risico zijn altijd beperkt tot aangepaste verzamelingen, verzameling die uzelf maakt en de ingebouwde verzameling **Onbekende computers** . Wanneer u een implementatie met een hoog risico maakt, kunt u geen ingebouwde verzameling selecteren, zoals **alle systemen**. Als u alle aangepaste verzamelingen wilt zien die minder clients dan de geconfigureerde maximum grootte hebben, schakelt u de optie voor het **verbergen van verzamelingen met een aantal leden groter dan de minimale configuratie van de site**uit. Zie [instellingen voor het beheren van implementaties met een hoog risico](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.  

De instellingen voor het verifiëren van de implementatie zijn gebaseerd op het huidige lidmaatschap van de verzameling. Nadat u de taken reeks hebt geïmplementeerd, wordt door Configuration Manager het lidmaatschap van de verzameling voor de implementatie-instellingen met een hoog risico niet opnieuw geëvalueerd.  

Stel bijvoorbeeld dat u de **standaard grootte** instelt op 100 en de **maximale grootte** op 1000. Wanneer u een implementatie met een hoog risico maakt, worden in het venster **verzameling selecteren** alleen verzamelingen weer gegeven die minder dan 100 clients bevatten. Als u het selectie vakje **verzamelingen verbergen met een aantal leden dat groter is dan de minimale configuratie-instelling van de site** wist, worden in het venster verzamelingen weer gegeven die minder dan 1000 clients bevatten.  

Wanneer u een verzameling met een siterol selecteert, geldt het volgende gedrag:  

- Als de verzameling een site systeem server bevat en u de verificatie-instellingen voor de implementatie hebt geconfigureerd om verzamelingen met site systeem servers te blok keren, treedt er een fout op. U kunt niet door gaan met het maken van de implementatie.  

- Als een van de volgende criteria van toepassing is, wordt in de wizard software implementeren een waarschuwing met een hoog risico weer gegeven. Als u wilt door gaan, moet u akkoord gaan met het maken van een implementatie met een hoog risico. Op de site wordt een controle status bericht gegenereerd.  

  - Als de verzameling een site systeem server bevat en u de verificatie-instellingen voor de implementatie hebt geconfigureerd om te waarschuwen voor verzamelingen met site systeem servers  

  - Als de verzameling de standaard grootte overschrijdt

  - Als de verzameling een server bevat  

## <a name="see-also"></a>Zie ook

[Takenreeksen beheren om taken te automatiseren](manage-task-sequences-to-automate-tasks.md)

---
title: Plannen voor het automatiseren van taken
titleSuffix: Configuration Manager
description: Plan voordat u taken reeksen maakt om taken met Configuration Manager te automatiseren.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0348cc245efdfd5e4d1e0bad25a457ea3b1ca609
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723563"
---
# <a name="plan-for-automating-tasks-in-configuration-manager"></a>Plannen voor het automatiseren van taken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt taak reeksen maken om taken in uw Configuration Manager omgeving te automatiseren. Deze taken variëren van het vastleggen van een besturings systeem op een referentie computer om het besturings systeem te implementeren op een of meer doel computers. De bewerkingen van de takenreeks worden gedefinieerd in de individuele stappen van de reeks. Wanneer de taken reeks wordt uitgevoerd, worden de acties van elke stap uitgevoerd op het niveau van de opdracht regel in de context van het lokale systeem. Dit gedrag betekent dat de taken reeks volledig geautomatiseerd wordt uitgevoerd zonder tussen komst van de gebruiker.

## <a name="task-sequence-steps-and-actions"></a><a name="BKMK_TSStepsActions"></a>Stappen en acties van taken reeksen  

Stappen zijn de basis onderdelen van een taken reeks. Ze kunnen opdrachten bevatten zoals:

- Het besturings systeem van een referentie computer configureren en vastleggen
- Windows, hardwarestuurprogramma's, de Configuration Manager-client en de software op de doel computer installeren

De acties van de stap definiëren de opdrachten van een taken reeks stap. Er zijn twee soorten acties:  

- Een actie die u definieert door een opdracht regel teken reeks te gebruiken, wordt een *aangepaste actie* genoemd  
- Een actie die vooraf wordt gedefinieerd door Configuration Manager wordt een *ingebouwde actie*genoemd.  

Een taken reeks kan elke combi natie van aangepaste en ingebouwde acties uitvoeren.  

Taken reeks stappen kunnen ook voor waarden bevatten die bepalen hoe de stap zich gedraagt. Dit gedrag omvat het stoppen van de taken reeks of het voortzetten van de taken reeks als er een fout optreedt. Een type voor waarde is een taken reeks variabele. U kunt bijvoorbeeld de variabele **SMSTSLastActionRetCode** gebruiken om de voor waarde van de vorige stap te testen. Voor waarden toevoegen aan één stap of een groep van stappen.  

De taken reeks verwerkt stappen sequentieel. Deze reeks bevat de actie van de stap en eventuele voor waarden voor de stap. Als Configuration Manager begint met het verwerken van een taken reeks stap, wordt de volgende stap niet gestart totdat de vorige bewerking is voltooid.

Een taken reeks wordt als voltooid beschouwd als:

- Alle stappen zijn voltooid  
- Een mislukte stap zorgt ervoor dat Configuration Manager de uitvoering van de taken reeks stopt voordat alle stappen zijn voltooid.  

Als de stap van een taken reeks bijvoorbeeld een afbeelding of pakket waarnaar wordt verwezen, niet kan vinden op een distributie punt, bevat de taken reeks een verbroken verwijzing. Configuration Manager stopt met het uitvoeren van de taken reeks op dat punt, tenzij de mislukte stap een voor waarde heeft om door te gaan wanneer er een fout optreedt.  

> [!IMPORTANT]  
> Standaard mislukt een takenreeks nadat er één stap of bewerking mislukt. Als u wilt dat de taken reeks verder gaat, zelfs wanneer een stap mislukt, bewerkt u de taken reeks, gaat u naar het tabblad **Opties** en selecteert u vervolgens **door gaan bij fout**.  

Zie [taken reeks stappen](../understand/task-sequence-steps.md)voor meer informatie over de stappen die aan een taken reeks kunnen worden toegevoegd.  

## <a name="task-sequence-groups"></a><a name="BKMK_TSGroups"></a> Takenreeksgroepen  

U kunt meerdere stappen binnen een taken reeks groeperen. Een taken reeks groep bestaat uit een naam, een optionele beschrijving en eventuele optionele voor waarden. De taken reeks evalueert de groeps voorwaarden als een eenheid voordat deze verdergaat met de volgende stap. Nest groepen binnen elkaar of Voeg een combi natie van stappen en subgroepen toe. Groepen kunnen nuttig zijn voor het combineren van meerdere stappen die een gemeenschappelijke voorwaarde delen.  

Wijs een naam toe aan taken reeks groepen. Het hoeft niet uniek te zijn. U kunt ook een optionele beschrijving geven van de takenreeksgroep.  

> [!IMPORTANT]  
> Standaard kan een takenreeksgroep niet worden uitgevoerd wanneer er een stap of ingesloten groep binnen de groep niet kan worden uitgevoerd. Als u wilt dat de taken reeks doorgaat wanneer een stap of Inge sloten groep mislukt, stelt u de optie **door gaan bij fout** in voor de stap of groep.  

De volgende tabel toont hoe de optie **door gaan bij fout** werkt wanneer u stappen groepeert.  

In dit voor beeld zijn er twee groepen taken reeksen die elk drie taken reeks stappen bevatten.  

|Takenreeksgroep of -stap|Instelling van Doorgaan bij fout|  
|---------------------------------|-------------------------------|  
|**Taken reeks groep 1**|**Door gaan bij fout** geselecteerd.|  
|Taken reeks stap 1|**Door gaan bij fout** geselecteerd.|  
|Taken reeks stap 2|Niet ingesteld.|  
|Taken reeks stap 3|Niet ingesteld.|  
|**Taken reeks groep 2**|Niet ingesteld.|  
|Taken reeks stap 4|Niet ingesteld.|  
|Taken reeks stap 5|Niet ingesteld.|  
|Taken reeks stap 6|Niet ingesteld.|  

- Als de taken reeks stap 1 mislukt, wordt de taken reeks voortgezet met de taken reeks stap 2.  

- Als de taken reeks stap 2 mislukt, wordt de taken reeks stap 3 niet uitgevoerd door de taken reeks. Omdat taken reeks groep 1 is geconfigureerd om **door te gaan**met de fout, gaat de taken reeks door naar taken reeks groep 2. De taak reeks stap 4 wordt nu uitgevoerd.  

- Als er een fout optreedt in de taken reeks stap 4, worden er geen stappen meer uitgevoerd. De taken reeks mislukt omdat de instelling **door gaan bij fout** niet is geconfigureerd voor taken reeks groep 2.  

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Onderliggende taken reeksen toevoegen aan een taken reeks

<!--1261338-->

Voeg een nieuwe taken reeks stap toe die een andere taken reeks uitvoert. Met deze stap maakt u een relatie tussen een bovenliggend/onderliggend item tussen de taken reeksen. Met deze stap kunt u meer modulaire taken reeksen maken die u opnieuw kunt gebruiken.  

Zie [Run Task sequence](../understand/task-sequence-steps.md#child-task-sequence)voor meer informatie.

> [!Note]  
> Configuration Manager schakelt deze optionele functie standaard niet in. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="task-sequence-variables"></a><a name="BKMK_TSVariables"></a>Taken reeks variabelen  

Taken reeks variabelen zijn een set naam-en waardeparen. Ze leveren configuratie-en besturingssysteem implementatie-instellingen voor computer-, OS-en gebruikers status configuratie taken op een Configuration Manager-client. Takenreeksvariabelen bieden een mechanisme om de stappen in een takenreeks te configureren en aan te passen.  

Wanneer u een taken reeks uitvoert, worden veel van de taken reeks instellingen opgeslagen als omgevings variabelen. U kunt de waarden van ingebouwde taken reeks variabelen openen of wijzigen. U kunt ook nieuwe taken reeks variabelen maken om de manier aan te passen waarop een taken reeks wordt uitgevoerd op een doel computer.  

U kunt taken reeks variabelen gebruiken om de volgende acties uit te voeren:  

- Instellingen voor een taken reeks actie configureren  

- Opdracht regel argumenten opgeven voor een taken reeks stap  

- Een voor waarde evalueren die bepaalt of een taken reeks stap of-groep wordt uitgevoerd  

- Geef waarden op voor aangepaste scripts die worden gebruikt in een taken reeks  

U hebt bijvoorbeeld een taken reeks die een taken reeks stap **lid maken van domein of werk groep** bevat. Implementeer de taken reeks op verschillende verzamelingen, waarbij het lidmaatschap van de verzameling wordt bepaald door het domein lidmaatschap. Geef een taken reeks variabele per verzameling op voor de domein naam van elke verzameling. Gebruik vervolgens die taken reeks variabele om de juiste domein naam op te geven in de taken reeks.  

Zie [How to use Task sequence Varia bles](../understand/using-task-sequence-variables.md)(Engelstalig) voor meer informatie.

## <a name="create-a-task-sequence"></a><a name="BKMK_TSCreate"></a>Een taken reeks maken  

Maak takenreeksen via de wizard Takenreeks maken. De wizard kan ingebouwde taken reeksen maken die specifieke taken of aangepaste taken reeksen uitvoeren die veel verschillende taken kunnen uitvoeren. Met de wizard kunt u de volgende typen taken reeksen maken:

- Een bestaande installatie kopie van een besturings systeem op een doel computer installeren  

- Een installatie kopie van een besturings systeem van een referentie computer bouwen en vastleggen  

- Upgraden naar Windows 10 vanuit een upgrade pakket voor een besturings systeem op een doel computer

- Een aangepaste taken reeks maken die een aangepaste taak of gespecialiseerde besturingssysteem implementatie doet  

Zie [taken reeksen maken](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence)voor meer informatie.  

## <a name="edit-a-task-sequence"></a><a name="BKMK_TSEdit"></a> Een takenreeks bewerken  

Bewerk de taken reeks met behulp van de **taken reeks editor**. De editor kan de volgende wijzigingen aanbrengen in de taken reeks:  

- Stappen toevoegen aan of verwijderen uit de taken reeks  

- De volg orde van de stappen van de taken reeks wijzigen  

- Groepen van stappen toevoegen of verwijderen  

- Opgeven of de taken reeks wordt voortgezet wanneer er een fout optreedt  

- Voor waarden toevoegen aan de stappen en groepen van een taken reeks  

> [!IMPORTANT]  
> Als de taken reeks niet-gekoppelde verwijzingen naar een object bevat als resultaat van de bewerking, moet u de verwijzing corrigeren voordat deze kan worden gesloten. Mogelijke acties zijn:  
>
> - Corrigeer de verwijzing
> - Het niet-verwezen object verwijderen uit de taken reeks  
> - De mislukte taken reeks stap tijdelijk uitschakelen totdat de verbroken verwijzing is gecorrigeerd of verwijderd  

Zie [de taken reeks editor gebruiken](../understand/task-sequence-editor.md)voor meer informatie over het bewerken van taken reeksen.  

## <a name="deploy-a-task-sequence"></a><a name="BKMK_TSDeploy"></a>Een taken reeks implementeren  

Een taken reeks implementeren op doel computers die zich in een wille keurige Configuration Manager-verzameling bevinden. Gebruik de ingebouwde verzameling **alle onbekende computers** om besturings systemen op onbekende computers te implementeren. U kunt een taken reeks niet implementeren voor gebruikers verzamelingen.  

> [!IMPORTANT]  
> Implementeer geen taken reeksen die besturings systemen installeren op ongepaste verzamelingen. Zorg ervoor dat de verzameling waarnaar u de taken reeks implementeert, alleen de computers bevat waarop u het besturings systeem wilt installeren. Configureer instellingen voor implementaties met een hoog risico om ongewenste besturingssysteem implementaties te helpen voor komen. Zie [instellingen voor het beheren van implementaties met een hoog risico](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.  

Elke doel computer die de taken reeks ontvangt, voert de taken reeks uit volgens de in de implementatie opgegeven instellingen. De taken reeksen zelf bevatten geen gekoppelde bestanden of Program ma's. Bestanden die door een taken reeks worden verwezen, moeten al aanwezig zijn op de doel computer of worden opgeslagen op een distributie punt waartoe clients toegang hebben.

> [!NOTE]  
> De taken reeks installeert pakketten waarnaar wordt verwezen door Program ma's, zelfs als het programma of pakket al is geïnstalleerd op de doel computer.
>
> Als met de taken reeks een toepassing wordt geïnstalleerd, wordt de toepassing alleen geïnstalleerd als aan de regels voor vereisten voor de toepassing wordt voldaan en de toepassing nog niet is geïnstalleerd, op basis van de detectie methode die is opgegeven voor de toepassing.  

De Configuration Manager-client voert een taken reeks implementatie uit wanneer het client beleid downloadt. Zie het [ophalen van beleid initiëren voor een Configuration Manager-client](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)om deze actie te activeren in plaats van te wachten tot de volgende polling-cyclus.  

Wanneer u taken reeksen implementeert op Windows Embedded-apparaten waarvoor een schrijf filter is ingeschakeld, kunt u opgeven of het schrijf filter op het apparaat tijdens de implementatie moet worden uitgeschakeld en het apparaat vervolgens opnieuw moet worden opgestart na de implementatie. Als het schrijf filter niet is uitgeschakeld, wordt de taken reeks geïmplementeerd naar een tijdelijke overlay en is deze niet beschikbaar wanneer het apparaat opnieuw wordt opgestart.  

> [!NOTE]  
> Wanneer u een taken reeks implementeert op een Windows Embedded-apparaat, moet u ervoor zorgen dat het apparaat lid is van een verzameling met een geconfigureerd onderhouds venster. Hiermee kunt u beheren wanneer het schrijf filter is uitgeschakeld en ingeschakeld en wanneer het apparaat opnieuw wordt opgestart.  
>
> Als clients taken reeksen downloaden buiten een onderhouds venster, wordt de taken reeks twee keer gedownload. In dit scenario downloadt de client de taken reeks, schakelt het schrijf filter uit, wordt de computer opnieuw opgestart en wordt de taken reeks opnieuw gedownload. Dit gedrag is omdat de taken reeks oorspronkelijk is gedownload naar de tijdelijke overlay, die wordt gewist wanneer het apparaat opnieuw wordt opgestart.  

Zie de [taken reeks implementeren](../deploy-use/deploy-a-task-sequence.md)voor meer informatie over het implementeren van taken reeksen.  

## <a name="export-and-import"></a><a name="BKMK_TSExportImport"></a>Exporteren en importeren

Met Configuration Manager kunt u taken reeksen exporteren en importeren. Als u een takenreeks exporteert, kunt u de objecten toevoegen waar de takenreeks naar verwijst.

Zie [taken reeksen exporteren en importeren](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport)voor meer informatie.  

## <a name="run-a-task-sequence"></a><a name="BKMK_TSRun"></a> Een takenreeks uitvoeren  

Taken reeksen worden altijd uitgevoerd met behulp van het lokale systeem account. Wanneer de taken reeks wordt uitgevoerd, controleert de Configuration Manager-client eerst of er pakketten met verwijzingen zijn voordat de stappen van de taken reeks worden gestart. Als een pakket waarnaar wordt verwezen, niet kan worden gevalideerd of gedownload, retourneert de taken reeks een fout voor de gekoppelde taken reeks stap.  

> [!Note]  
> De taken reeks stap **opdracht regel uitvoeren** biedt de mogelijkheid om een opdracht uit te voeren als een ander account.  

Als u een taken reeks implementatie configureert om te downloaden en uit te voeren, downloadt de Configuration Manager-client alle afhankelijke inhoud naar de cache. Als de cache grootte van de client te klein is of als de inhoud niet wordt gevonden, mislukt de taken reeks. De client genereert een status bericht.

U kunt ook opgeven dat de client de inhoud alleen downloadt wanneer deze vereist is. Als u deze actie wilt uitvoeren, selecteert u **inhoud lokaal downloaden wanneer deze nodig is door de taken** reeks in de taken reeks implementatie uit te voeren. Een andere optie is om het **programma uit te voeren vanaf een distributie punt**. Met deze optie installeert de client de bestanden rechtstreeks van het distributie punt zonder dat ze eerst naar de cache worden gedownload.

Wanneer u de taken reeks implementatie als **beschikbaar**configureert en de client afhankelijke inhoud voor de taken reeks niet kan vinden, wordt er onmiddellijk een fout bericht verzonden. Voor een **vereiste** implementatie wacht de Configuration Manager-client in deze situatie. Er wordt opnieuw geprobeerd om de inhoud te downloaden tot de deadline, in het geval dat de inhoud nog niet is gerepliceerd naar een inhouds locatie waartoe de client toegang kan hebben.  

Wanneer een taken reeks met succes is voltooid of mislukt, Configuration Manager deze status in de client geschiedenis registreren.

Wanneer een taken reeks op een computer wordt gestart, kunt u deze niet annuleren of stoppen.  

> [!IMPORTANT]  
> Als een taken reeks stap vereist dat de computer opnieuw wordt opgestart, moet de client kunnen opstarten naar een geformatteerde schijf partitie. Anders mislukt de taken reeks, ongeacht eventuele fout afhandeling die u in de taken reeks opgeeft.  

Wanneer een afhankelijk object van een taken reeks wordt bijgewerkt naar een nieuwere versie, wordt elke taken reeks die verwijst naar het pakket automatisch bijgewerkt. Het verwijst naar de nieuwste versie, ongeacht het aantal updates dat u hebt geïmplementeerd.  

## <a name="use-maintenance-windows"></a><a name="BKMK_TSMaintenanceWindow"></a>Onderhouds Vensters gebruiken

U kunt opgeven wanneer de taken reeks kan worden uitgevoerd door een onderhouds venster te definiëren voor de verzameling apparaten. U kunt onderhouds Vensters configureren met een begin datum, een begin-en eind tijd en een terugkeer patroon. Wanneer u de planning instelt voor het onderhouds venster, kunt u opgeven dat het onderhouds venster alleen van toepassing is op taken reeksen. Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie.  

> [!IMPORTANT]  
> Wanneer u een onderhoudsvenster configureert om een takenreeks uit te voeren, gaat na de start van de takenreeks de uitvoering van de takenreeks gewoon door als het onderhoudsvenster wordt gesloten.  

Als op een apparaat meer dan één onderhouds venster is toegepast, kan de client een onderhouds venster van **alle implementaties** negeren. Met ingang van versie 1810 kunt u de volgende client instelling gebruiken om dit gedrag te beheren: de **installatie van software-updates inschakelen in het onderhouds venster ' alle implementaties ' wanneer het onderhouds venster Software-update beschikbaar is**. Zie [client instellingen](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint) voor meer informatie.<!-- SCCMDocs-pr #4596 -->


## <a name="task-sequences-and-the-network-access-account"></a><a name="BKMK_TSNetworkAccessAccount"></a>Taken reeksen en het netwerk toegangs account  

> [!Important]  
> Voor sommige implementatie scenario's voor besturings systemen is geen gebruik van het netwerk toegangs account vereist. Zie [Enhanced http](#enhanced-http)(Engelstalig) voor meer informatie.

Hoewel taken reeksen alleen worden uitgevoerd in de context van het lokale systeem account, moet u mogelijk het [netwerk toegangs account](../../core/plan-design/hierarchy/accounts.md#network-access-account) in de volgende omstandigheden configureren:  

- Als de taken reeks probeert toegang te krijgen tot Configuration Manager inhoud op distributie punten. Het netwerk toegangs account correct configureren, anders mislukt de taken reeks.

- Wanneer u een opstart installatie kopie gebruikt om een besturingssysteem implementatie te initiëren. In dit geval gebruikt Configuration Manager de Windows PE-omgeving, die geen volledig besturings systeem is. De Windows PE-omgeving maakt gebruik van een automatisch gegenereerde, wille keurige naam die geen lid is van een domein. Als u het netwerk toegangs account niet correct configureert, heeft de computer geen toegang tot de vereiste inhoud voor de taken reeks.  

> [!NOTE]  
> Het netwerk toegangs account wordt nooit gebruikt als de beveiligings context voor het uitvoeren van Program ma's, het installeren van toepassingen, het installeren van updates of het uitvoeren van taken reeksen. Het netwerk toegangs account wordt alleen gebruikt voor toegang tot de gekoppelde bronnen in het netwerk.  

Zie [netwerk toegangs account](../../core/plan-design/hierarchy/accounts.md#network-access-account)voor meer informatie over het netwerk toegangs account.  

### <a name="enhanced-http"></a>Verbeterde HTTP
<!--1358278-->

Wanneer u **Enhanced http**inschakelt, is voor de volgende scenario's geen netwerk toegangs account vereist om inhoud te downloaden vanaf een distributie punt:

- Taken reeksen die worden uitgevoerd vanaf opstart media of PXE  
- Taken reeksen die worden uitgevoerd vanuit software Center  

Deze taken reeksen kunnen voor de implementatie van het besturings systeem of aangepast zijn. Het wordt ook ondersteund voor werkgroepcomputers.

Zie [Enhanced http](../../core/plan-design/hierarchy/enhanced-http.md)(Engelstalig) voor meer informatie.  

> [!Note]  
> Voor de volgende scenario's voor besturingssysteem implementaties is nog steeds een netwerk toegangs account vereist:
>  
> - De optie voor de [implementatie](../deploy-use/deploy-a-task-sequence.md)van taken reeksen, **rechtstreeks vanuit een distributie punt toegang tot inhoud, wanneer dit nodig is voor de taken reeks die wordt uitgevoerd**
> - Met de optie [status opslag opvragen](../understand/task-sequence-steps.md#BKMK_RequestStateStore) **als het computer account geen verbinding kan maken met een status opslag, het netwerk toegangs account gebruiken**
> - Wanneer u verbinding maakt met een niet-vertrouwd domein of over Active Directory forests
> - De optie [installatie kopie van het besturings systeem Toep assen](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) , **rechtstreeks vanuit het distributie punt toegang tot inhoud**
> - De [geavanceerde instelling](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) van de taken reeks om **eerst een ander programma uit te voeren**
> - [Cast](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)  

## <a name="create-media"></a><a name="BKMK_TSCreateMedia"></a>Media maken

U kunt taken reeksen en de bijbehorende bestanden en afhankelijkheden naar verschillende media typen schrijven. Configuration Manager ondersteunt Verwissel bare media zoals een DVD-of USB-flash station voor vastleggen, zelfstandige en opstart bare media. Voor bereide media maakt gebruik van een Windows-installatie kopie (WIM)-bestand.  

Wanneer u media maakt, moet u een wacht woord opgeven om de toegang te beheren. Vervolgens moet een persoon op de doel computer het wacht woord invoeren om de taken reeks uit te voeren.  

Wanneer u een taken reeks uitvoert vanaf media, wordt de opgegeven processor architectuur van de media niet herkend. Als de opgegeven architectuur niet overeenkomt met de doel computer, probeert de taken reeks nog steeds uit te voeren. Als de architectuur van de media niet overeenkomt met de architectuur van de doel computer, mislukt de taken reeks.  

Zie [taken reeks media maken](../deploy-use/create-task-sequence-media.md)voor meer informatie.  

### <a name="media-types"></a>Mediatypen

Configuration Manager ondersteunt de volgende typen media:  

#### <a name="capture-media"></a>Vastleg media

Deze media legt een installatie kopie van het besturings systeem vast die u kunt configureren en maken buiten de Configuration Manager-infra structuur. registrerende media kunnen aangepaste programma's bevatten die u kunt uitvoeren voordat een takenreeks wordt uitgevoerd. Het aangepaste programma kan met het bureau blad communiceren, de gebruiker vragen om invoer waarden of variabelen maken die door de taken reeks moeten worden gebruikt.  

Zie [Capture-media maken](../deploy-use/create-capture-media.md)voor meer informatie.  

#### <a name="stand-alone-media"></a>Zelfstandige media

Zelfstandige media bevatten de takenreeks en alle gekoppelde objecten die nodig zijn voor de uitvoering van de taak. Taken reeksen met zelfstandige media kunnen worden uitgevoerd wanneer Configuration Manager beperkte of geen verbinding met het netwerk heeft. Zelfstandige media uitvoeren op de volgende manieren:  

- Als de doel computer niet is opgestart, wordt de Windows PE-installatie kopie die is gekoppeld aan de taken reeks, gebruikt vanaf de zelfstandige media en wordt de taken reeks gestart.  

- Start de zelfstandige media hand matig. Als een gebruiker is aangemeld bij de computer, kunnen ze de taken reeks vanaf de media initiëren.  

> [!IMPORTANT]  
> De stappen van de taken reeks voor zelfstandige media moeten kunnen worden uitgevoerd zonder gegevens op te halen uit het netwerk. Anders mislukt de taken reeks stap die probeert de gegevens op te halen. Bijvoorbeeld een taken reeks stap waarvoor een distributie punt is vereist om een pakket te verkrijgen, mislukt. Als het zelfstandige medium het benodigde pakket bevat, slaagt de taken reeks stap.  

Zie voor meer informatie [maken van zelfstandige media](../deploy-use/create-stand-alone-media.md).  

#### <a name="bootable-media"></a>Opstartbare media

Opstart bare media bevatten de vereiste bestanden om een doel computer op te starten, zodat deze verbinding kan maken met de Configuration Manager-infra structuur. Vervolgens wordt bepaald welke taken reeksen moeten worden uitgevoerd op basis van de bijbehorende verzamelings lidmaatschappen. Deze media bevatten geen taken reeks of afhankelijke objecten. In plaats daarvan downloadt de client de inhoud via het netwerk. Deze methode is handig voor nieuwe computers of bare-metal implementaties, wanneer er geen besturings systeem op de doel computer is.  

Zie [opstart bare media maken](../deploy-use/create-bootable-media.md)voor meer informatie.  

#### <a name="prestaged-media"></a>Voorbereide media

Voorgefaseerde media implementeren een installatie kopie van een besturings systeem op een doel computer die niet is ingericht. De voorgefaseerde media worden opgeslagen als een Windows-installatie kopie (WIM)-bestand. Dit bestand kan worden geïnstalleerd op een bare-metal computer door de fabrikant of in een Enter prise staging Center. Een voor deel van voor bereide media is dat voor deze locaties geen verbinding met uw Configuration Manager omgeving nodig is.  

Zie voor [bereide media maken](../deploy-use/create-prestaged-media.md)voor meer informatie.  

## <a name="next-steps"></a>Volgende stappen

- [Beveiliging en privacy voor besturingssysteemimplementatie](security-and-privacy-for-operating-system-deployment.md)

- [Sitesysteemrollen voor besturingssysteemimplementaties voorbereiden](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)

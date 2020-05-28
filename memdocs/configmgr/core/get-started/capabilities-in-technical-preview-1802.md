---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview-versie 1802 voor Configuration Manager.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 94208da3eda33cba69f04bbbf42edd08b585c1c4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428196"
---
# <a name="capabilities-in-technical-preview-1802-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1802 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1802. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. 

Bekijk de [technische preview voor Configuration Manager](technical-preview.md) voordat u deze versie van de Technical Preview installeert. In dit artikel wordt u vertrouwd met de algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Bekende problemen in deze Technical Preview
- **Bijwerken naar een nieuwe preview-versie mislukt wanneer u een site server in de passieve modus hebt**. Als u een [primaire site server in de passieve modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)hebt, moet u de site server van de passieve modus verwijderen voordat u de nieuwe preview-versie bijwerkt. U kunt de site server van de passieve modus opnieuw installeren nadat de update door de site is voltooid.

  De site server van de passieve modus verwijderen:
  1. Ga in de Configuration Manager-console naar **beheer**  >  **overzicht**  >  **site configuratie**  >  **servers en site systeem rollen**en selecteer vervolgens de site server passieve modus.
  2. Klik in het deel venster **site systeem rollen** met de rechter muisknop op de **site** serverrol en kies vervolgens **rol verwijderen**.
  3. Klik met de rechter muisknop op de site server in de passieve modus en kies **verwijderen**.
  4. Nadat de installatie van de site server ongedaan is gemaakt, start u de service **CONFIGURATION_MANAGER_UPDATE**opnieuw op de actieve primaire site server.
  <!--sms 489412-->


</br>

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Overgang Endpoint Protection werk belasting naar intune met behulp van co-beheer    
<!-- 1357365 -->
In deze release kunt u de Endpoint Protection workload nu overzetten van Configuration Manager naar intune nadat u co-beheer hebt ingeschakeld. Als u de Endpoint Protection workload wilt door lopen, gaat u naar de pagina met eigenschappen voor co-beheer en verplaatst u de schuif regelaar van Configuration Manager naar **pilot** of **alle**. Zie voor meer informatie [co-beheer voor Windows 10-apparaten](../../comanage/overview.md).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Windows Delivery Optimization configureren om Configuration Manager grens groepen te gebruiken
<!-- 1324696 -->
U gebruikt Configuration Manager grens groepen om de distributie van inhoud in uw bedrijfs netwerk en externe kant oren te definiëren en te reguleren. [Windows Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) is een op de cloud gebaseerde peer-to-peer-technologie voor het delen van inhoud tussen Windows 10-apparaten. Vanaf deze release configureert u Delivery Optimization om uw grens groepen te gebruiken bij het delen van inhoud tussen peers. Een nieuwe client instelling past de grens groep-ID toe als de id van de leverings optimalisatie groep op de client. Wanneer de client communiceert met de Delivery Optimization-Cloud service, wordt deze id gebruikt om peers met de gewenste inhoud te vinden. 

### <a name="prerequisites"></a>Vereisten
- Delivery Optimization is alleen beschikbaar op Windows 10-clients

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.

1. Maak in de Configuration Manager-console, werk ruimte **beheer** , knoop punt **client instellingen** een aangepast beleid voor client Apparaatinstellingen.
2. Selecteer de nieuwe **Delivery Optimization** -groep.
3. Schakel de instelling **gebruik Configuration Manager grens groepen in voor de id van de leverings optimalisatie groep**.

Zie voor meer informatie de optie **groep** Delivery mode in [Delivery Optimization Options](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#how-microsoft-uses-delivery-optimization).



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Windows 10 in-place upgrade taken reeks via de Cloud beheer gateway
<!-- 1357149 -->

De [taken reeks](../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) Windows 10 in-place upgrade ondersteunt nu implementatie voor clients op Internet die worden beheerd via de [Cloud beheer gateway](../clients/manage/cmg/plan-cloud-management-gateway.md). Met deze mogelijkheid kunnen externe gebruikers eenvoudiger een upgrade uitvoeren naar Windows 10 zonder dat ze verbinding hoeven te maken met het bedrijfs netwerk. 

Zorg ervoor dat alle inhoud waarnaar wordt verwezen door de in-place upgrade taken reeks, wordt gedistribueerd naar een [Cloud distributiepunt](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Op andere apparaten kan de taken reeks niet worden uitgevoerd.

Wanneer u een upgrade taken reeks implementeert, gebruikt u de volgende instellingen:
- **Taken reeks mag voor client worden uitgevoerd op het Internet**, op het tabblad gebruikers ervaring van de implementatie.
- **Alle inhoud lokaal downloaden voordat de taken reeks wordt gestart**op het tabblad distributie punten van de implementatie. Andere opties, zoals **het lokaal downloaden van inhoud wanneer deze nodig is voor de taken reeks die wordt uitgevoerd,** werken niet in dit scenario. De taken reeks engine kan momenteel geen inhoud van een Cloud distributiepunt ophalen. De Configuration Manager-client moet de inhoud van het Cloud distributiepunt downloaden voordat de taken reeks wordt gestart.
- (*Optioneel*) **Down load inhoud vooraf voor deze taken reeks**op het tabblad Algemeen van de implementatie. Zie [inhoud vooraf in cache configureren](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content)voor meer informatie.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Taken reeks voor verbeteringen in Windows 10 in-place upgrade
<!-- 1357425 -->
De standaard taken reeks sjabloon voor Windows 10 in-place upgrade bevat nu extra groepen met aanbevolen acties om toe te voegen voor en na het upgrade proces. Deze acties zijn gebruikelijk voor veel klanten die apparaten met succes upgraden naar Windows 10. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Nieuwe groepen onder **voor bereiding voor upgrade**
- **Batterij controles**: Voeg stappen toe aan deze groep om te controleren of de computer accu gebruikt of bekabelde voeding. Voor deze actie is een aangepast script of hulp programma vereist om deze controle uit te voeren.
- **Controles van netwerk/bekabelde verbinding**: Voeg stappen toe aan deze groep om te controleren of de computer is verbonden met een netwerk en geen draadloze verbinding gebruikt. Voor deze actie is een aangepast script of hulp programma vereist om deze controle uit te voeren.
- **Niet-compatibele toepassingen verwijderen**: Voeg stappen toe aan deze groep om alle toepassingen te verwijderen die niet compatibel zijn met deze versie van Windows 10. De methode voor het verwijderen van een toepassing varieert. Als de toepassing Windows Installer gebruikt, kopieert u de opdracht regel voor het **Uninstall-programma** van het tabblad **Program ma's** van de Windows Installer implementatie type-eigenschappen van de toepassing. Voeg vervolgens de stap **opdracht regel uitvoeren** in deze groep toe met de opdracht regel voor het verwijderen van het programma. Bijvoorbeeld: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Niet-compatibele Stuur Programma's verwijderen**: Voeg stappen toe aan deze groep om stuur Programma's te verwijderen die niet compatibel zijn met deze versie van Windows 10.
- **Beveiliging van derden verwijderen/opschorten**: Voeg stappen toe aan deze groep voor het verwijderen of onderbreken van externe beveiligings Programma's, zoals antivirus software.
   - Als u een schijf versleutelings programma van derden gebruikt, geeft u het versleutelings stuur programma voor het Windows Setup met de [opdracht regel optie](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers** . Voeg een [set taken reeks variabelen voor sets](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) toe aan de taken reeks in deze groep. Stel de taken reeks variabele in op **OSDSetupAdditionalUpgradeOptions**. Stel de waarde in op **/ReflectDriver** met het pad naar het stuur programma. Met deze [taken reeks actie variabele](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS) wordt de Windows Setup opdracht regel toegevoegd die wordt gebruikt door de taken reeks. Neem contact op met de software leverancier voor meer informatie over dit proces.

### <a name="new-groups-under-post-processing"></a>Nieuwe groepen onder **naverwerking**
- Op **installatie-gebaseerde Stuur programma's toep assen**: Voeg in deze groep stappen toe om stuur programma's (. exe) te installeren op basis van pakketten.
- **Beveiliging van derden installeren/inschakelen**: Voeg stappen toe aan deze groep om beveiligings Programma's van derden, zoals anti virus, te installeren of in te scha kelen. 
- **Windows-standaard-apps en-koppelingen instellen**: Voeg de stappen in deze groep toe om Windows-standaard-apps en-bestands koppelingen in te stellen. Bereid eerst een referentie computer voor met de gewenste app-koppelingen. Voer vervolgens de volgende opdracht regel uit om te exporteren: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Voeg het XML-bestand toe aan een pakket. Voeg vervolgens een stap [opdracht regel uitvoeren](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) toe aan deze groep. Geef het pakket op dat het XML-bestand bevat en geef vervolgens de volgende opdracht regel op: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Zie [standaard toepassings koppelingen exporteren of importeren](https://docs.microsoft.com/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)voor meer informatie.
- **Aanpassingen en persoonlijke instellingen Toep assen**: Voeg stappen toe aan deze groep om aanpassingen aan het start menu toe te passen, zoals het organiseren van programma groepen. Zie [het Start scherm aanpassen](https://docs.microsoft.com/windows-hardware/manufacture/desktop/customize-the-start-screen)voor meer informatie.

### <a name="additional-recommendations"></a>Extra aanbevelingen
- Raadpleeg de Windows-documentatie om [Windows 10-upgrade fouten op te lossen](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Dit artikel bevat ook gedetailleerde informatie over het upgrade proces.
- Op de standaard stap voor het controleren van de **gereedheid** kunt u **ervoor zorgen dat het minimale aantal beschik bare schijf ruimte (MB)** is. Stel de waarde in op ten minste **16384** (16 GB) voor een 32-bits OS-upgrade pakket, of **20480** (20 GB) voor de 64-bits. 
- Gebruik de **SMSTSDownloadRetryCount** [ingebouwde taken reeks variabele](../../osd/understand/task-sequence-variables.md) SMSTSDownloadRetryCount om het beleid opnieuw te downloaden. Op dit moment wordt de client standaard twee maal opnieuw geprobeerd. Deze variabele is ingesteld op twee (2). Als uw clients zich niet op een bekabelde bedrijfs netwerk verbinding bevinden, helpen extra nieuwe pogingen om de client beleid te verkrijgen. Het gebruik van deze variabele veroorzaakt geen negatief neven effect, anders dan vertraagd mislukken als het beleid niet kan worden gedownload.<!-- 501016 --> Verhoog ook de **SMSTSDownloadRetryDelay** -variabele van de standaard waarde van 15 seconden.
- Een inline-compatibiliteits beoordeling uitvoeren. 
   - Voeg in de groep **voorbereiden voor upgrade** een tweede stap van het **besturings systeem uit** . Geef een naam voor de *upgrade beoordeling*op. Geef hetzelfde upgrade pakket op en schakel vervolgens de optie in om **Windows Setup compatibiliteits scan uit te voeren zonder de upgrade te starten**. Schakel **door gaan bij fout** in op het tabblad Opties. 
   - Voeg direct na deze stap voor de *upgrade beoordeling* een stap **opdracht regel uitvoeren** toe. Geef de volgende opdracht regel op:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Voeg op het tabblad **Opties** de volgende voor waarde toe: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Deze retour code is het decimale equivalent van MOSETUP_E_COMPAT_SCANONLY (0xC1900210). Dit is een geslaagde compatibiliteits scan zonder problemen. Als de stap *upgrade beoordeling* slaagt en deze code retourneert, wordt deze stap overgeslagen. Als de evaluatie stap een andere retour code retourneert, mislukt deze stap de taken reeks met de retour code van de Windows Setup compatibiliteits scan.
   - Zie [upgrade van besturings systeem](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS)voor meer informatie.
- Als u het apparaat wilt wijzigen van BIOS in UEFI tijdens deze taken reeks, raadpleegt u de [conversie van BIOS naar UEFI tijdens een in-place upgrade](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

Verzend **feedback** vanaf het tabblad **Start** van het lint als u nog meer aanbevelingen of suggesties hebt.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Verbeteringen van distributie punten met PXE-functionaliteit
<!-- 1357580 -->
Ter verduidelijking van het gedrag van de [nieuwe PXE-functionaliteit](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6) die als eerste werd geïntroduceerd in Technical Preview versie 1706, is de naam van de **IPv6-** optie voor ondersteuning gewijzigd. Schakel op het tabblad **PXE** van de eigenschappen van het distributie punt het selectie vakje **PXE-Responder inschakelen zonder Windows Deployment service**in. 

Met deze optie wordt een PXE-responder op het distributie punt ingeschakeld, waarvoor Windows Deployment Services (WDS) niet vereist is. Als u deze nieuwe optie inschakelt op een distributie punt dat al met PXE is ingeschakeld, wordt de WDS-service door Configuration Manager onderbroken. Als u deze nieuwe optie uitschakelt, maar **PXE-ondersteuning voor clients wel inschakelt**, schakelt het distributie punt WDS opnieuw in.

Omdat WDS niet vereist is, kan het distributie punt met PXE-functionaliteit een client-of Server besturingssysteem zijn, met inbegrip van Windows Server Core. Deze nieuwe PXE responder-service blijft IPv6 ondersteunen en verbetert ook de flexibiliteit van distributie punten met PXE-functionaliteit in externe kant oren.

> [!NOTE]
> Deze service gebruikt dezelfde fundamentele technologie als de op [client gebaseerde PXE-responder-service](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) in Technical Preview-versie 1712. Deze functie vereist geen overhead van de distributiepunt rol.

### <a name="multicast"></a>Cast
Als u multi cast wilt inschakelen en configureren op het tabblad **multi cast** van de eigenschappen van het distributie punt, moet het distributie punt WDS gebruiken. 
- Als u **PXE-ondersteuning voor clients inschakelt** en multi cast inschakelt **om gelijktijdig gegevens te verzenden naar meerdere clients**, kunt u geen **PXE-Responder inschakelen zonder Windows Deployment service**.
- Als u **PXE-ondersteuning voor clients inschakelt** en **een PXE-responder zonder Windows Deployment service**inschakelt, kunt u **multi cast niet inschakelen om gelijktijdig gegevens te verzenden naar meerdere clients**



## <a name="deployment-templates-for-task-sequences"></a>Implementatie sjablonen voor taken reeksen
<!-- 1357391 -->
De implementatie wizard voor taken reeksen kan nu een implementatie sjabloon maken. De implementatie sjabloon kan worden opgeslagen en toegepast op een bestaande of nieuwe taken reeks voor het maken van een implementatie. 

### <a name="try-it-out"></a>Probeer het nu!  
Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt. 

 **Een implementatie sjabloon maken voor een nieuwe taken reeks implementatie** <br/> 
1. Vouw in de werk ruimte **software bibliotheek** **besturings systemen**uit en selecteer **taken reeksen**.
2. Klik met de rechter muisknop op een taken reeks en selecteer **implementeren**. 
3. Op het tabblad **Algemeen** ziet u nu een optie voor het selecteren van de **implementatie sjabloon**. 
4. Ga verder met de **wizard software implementeren** om de implementatie-instellingen voor de taken reeks te selecteren. 
5. Wanneer u het tabblad **samen vatting** van de **wizard software implementeren**bereikt, klikt u op **Opslaan als sjabloon**.
6. Geef een naam op voor de sjabloon en selecteer de instellingen die u in de sjabloon wilt opslaan. 
7. Klik op **Opslaan**. De sjabloon is nu beschikbaar voor gebruik in de optie **implementatie sjabloon selecteren** .



## <a name="product-lifecycle-dashboard"></a>Dash board voor product levenscyclus
<!--1319632-->
Het nieuwe [product levenscyclus dashboard](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md) toont de status van het micro soft Product Lifecycle-beleid voor micro soft-producten geïnstalleerd op apparaten die worden beheerd met Configuration Manager. Het dash board biedt informatie over micro soft-producten in uw omgeving, de ondersteunings status en de ondersteuning voor eind datums. U kunt het dash board gebruiken om inzicht te krijgen in de beschik baarheid van de ondersteuning voor elk product. 

Als u toegang wilt krijgen tot het levenscyclus dashboard, gaat u in de Configuration Manager-console naar **activa en naleving**  > **Asset Intelligence**  > **product levenscyclus**



## <a name="improvements-to-reporting"></a>Verbeteringen in rapportage
<!--1357653-->
Als gevolg van [uw feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) hebben we een nieuw rapport toegevoegd, **voor Windows 10-onderhouds Details voor een specifieke verzameling**. Dit rapport bevat de resource-ID, de NetBIOS-naam, de naam van het besturings systeem, de naam van de besturingssysteem release, de build, de besturingssysteem vertakking en de onderhouds status voor Windows 10-apparaten. Als u het rapport wilt openen, gaat u naar **bewaking**  > **rapport**  > **rapporten**  > **besturings systemen**  > **Windows 10 service Details voor een specifieke verzameling**.



## <a name="improvements-to-software-center"></a>Verbeteringen in Software Center
<!--1357592-->
Als gevolg van [uw feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) kunnen geïnstalleerde toepassingen nu worden verborgen in Software Center. Toepassingen die al zijn geïnstalleerd, worden niet meer weer gegeven op het tabblad toepassingen wanneer deze optie is ingeschakeld. 

### <a name="try-it-out"></a>Probeer het nu!
Schakel de instelling **geïnstalleerde toepassingen verbergen in Software Center** in de client instellingen voor Software Center in. Bekijk het gedrag van het Software Center wanneer de eind gebruiker een toepassing installeert.



## <a name="improvements-to-run-scripts"></a>Verbeteringen voor het uitvoeren van scripts
<!--1236459-->
De functie [scripts uitvoeren](../../apps/deploy-use/create-deploy-scripts.md) retourneert nu script uitvoer met behulp van JSON-indeling. Deze indeling retourneert consistent een lees bare script uitvoer. Scripts die niet worden uitgevoerd, krijgen mogelijk geen uitvoer geretourneerd. 



## <a name="boundary-group-fallback-for-management-points"></a>Terugval van grens groep voor beheer punten
<!-- 1324594 -->
Vanaf deze release kunt u terugval relaties configureren voor beheer punten tussen [grens groepen](../servers/deploy/configure/boundary-groups.md). Dit gedrag biedt meer controle over de beheer punten die clients gebruiken. Op het tabblad **relaties** van de eigenschappen van de grens groep bevindt zich een nieuwe kolom voor het beheer punt. Wanneer u een nieuwe terugval grens groep toevoegt, is de terugval tijd voor het beheer punt momenteel altijd nul (0). Dit gedrag is hetzelfde voor het **standaard gedrag** van de standaard grens groep van de site.

Voorheen treedt er een veelvoorkomend probleem op wanneer u een beveiligd beheer punt in een beveiligd netwerk hebt. Clients op het hoofd beleid voor de ontvangst van het bedrijfs netwerk dat dit beveiligde beheer punt bevat, zelfs als ze niet via een firewall kunnen communiceren. Als u dit probleem wilt oplossen, gebruikt u de optie **nooit terugval** om ervoor te zorgen dat clients alleen terugvallen op beheer punten waarmee ze kunnen communiceren.

Wanneer u een upgrade van de site naar deze versie uitvoert, voegt Configuration Manager alle niet-Internet gerichte beheer punten toe aan de standaard grens groep van de site. Dit upgrade gedrag zorgt ervoor dat oudere client versies blijven communiceren met beheer punten. Verplaats uw beheer punten naar de gewenste grens groepen om optimaal gebruik te kunnen maken van deze functie.

Terugval groep grens groepen van beheer punten wijzigt het gedrag tijdens client installatie (ccmsetup) niet. Als de opdracht regel niet het eerste beheer punt specificeert met behulp van de para meter/MP, ontvangt de nieuwe client de volledige lijst met beschik bare beheer punten. Voor het eerste Boots trap proces gebruikt de client het eerste beheer punt waartoe het toegang heeft. Zodra de client bij de site is geregistreerd, ontvangt de lijst met beheer punten correct gesorteerd met dit nieuwe gedrag. 

### <a name="prerequisites"></a>Vereisten
- [Voorkeurs beheer punten](../servers/deploy/configure/boundary-groups.md#bkmk_preferred)inschakelen. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie** uit en selecteer **sites**. Klik op **hiërarchie-instellingen** in het lint. Schakel op het tabblad **Algemeen** de optie **clients gebruiken liever beheer punten die zijn opgegeven in grens groepen**. 

### <a name="known-issues"></a>Bekende problemen
- Implementatie processen van besturings systemen zijn niet op de hoogte van grens groepen.

### <a name="troubleshooting"></a>Problemen oplossen
Nieuwe vermeldingen worden weer gegeven in het **bestand locationservices. log**. Het kenmerk **localiteit** identificeert een van de volgende statussen:
- 0: onbekend
- 1: het opgegeven beheer punt bevindt zich alleen in de standaard site grens groep voor terugval
- 2: het opgegeven beheer punt bevindt zich in een grens groep van het externe gebied of een neighbor. Wanneer het beheer punt zich in een neighbor en de standaard grens groepen van de site bevindt, is de locatie 2.
- 3: het opgegeven beheer punt bevindt zich in de lokale of huidige grens groep. Wanneer het beheer punt zich in de huidige grens groep bevindt, en ofwel een neighbor of de standaard grens groep van de site is, is de plaats 3. Als u de instelling voorkeurs beheer punten niet inschakelt in de hiërarchie-instellingen, is de locatie altijd 3, ongeacht in welke grens groep het beheer punt zich bevindt.

Clients gebruiken eerst lokale beheer punten (lokale naam 3), externe seconde (lokale plaats 2) en vervolgens terugval (locatie 1). 

Wanneer een client vijf fouten in tien minuten ontvangt en niet kan communiceren met een beheer punt in de huidige grens groep, probeert het contact te maken met een beheer punt in een neighbor of de standaard grens groep van de site. Als het beheer punt in de huidige grens groep later weer online is, keert de client terug naar het lokale beheer punt tijdens de volgende vernieuwings cyclus. De vernieuwings cyclus is 24 uur of wanneer de Configuration Manager Agent-service opnieuw wordt gestart.



## <a name="improved-support-for-cng-certificates"></a>Verbeterde ondersteuning voor CNG-certificaten
<!-- 1357314 -->
Configuration Manager (current branch) versie 1710 ondersteunt [crypto grafie: Next Generation (CNG)-certificaten](../plan-design/network/cng-certificates-overview.md). Versie 1710 beperkt de ondersteuning voor client certificaten in verschillende scenario's. 

In deze technische preview-versie gebruikt u CNG-certificaten voor de volgende HTTPS-server functies:
- Beheerpunt
- Distributiepunt
- Software-updatepunt

De lijst met [niet-ondersteunde scenario's](../plan-design/network/cng-certificates-overview.md#unsupported-scenarios) blijft hetzelfde.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Cloud Management gateway-ondersteuning voor Azure Resource Manager
<!-- 1324735 -->
Bij het maken van een exemplaar van de [Cloud beheer gateway](../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) biedt de wizard nu de mogelijkheid om een **Azure Resource Manager-implementatie**te maken. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) is een modern platform voor het beheren van alle oplossings resources als één entiteit, een zogenaamde [resource groep](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Bij het implementeren van CMG met Azure Resource Manager gebruikt de site Azure Active Directory (Azure AD) om de benodigde cloud resources te verifiëren en te maken. Voor deze moderne implementatie is het klassieke Azure-beheer certificaat niet vereist.  

De wizard CMG biedt nog steeds de optie voor een **klassieke service-implementatie** met behulp van een Azure-beheer certificaat. Voor het vereenvoudigen van de implementatie en het beheer van resources, raden we u aan het Azure Resource Manager-implementatie model te gebruiken voor alle nieuwe CMG-instanties. Implementeer, indien mogelijk, bestaande CMG-exemplaren opnieuw via Resource Manager.

Configuration Manager migreert geen bestaande klassieke CMG-instanties naar het Azure Resource Manager-implementatie model. Maak nieuwe CMG-instanties met Azure Resource Manager-implementaties en verwijder vervolgens klassieke CMG-instanties. 

> [!IMPORTANT]
> Deze functie biedt geen ondersteuning voor Azure Cloud service providers (CSP). De CMG-implementatie met Azure Resource Manager blijft de klassieke Cloud service gebruiken, die niet door de CSP wordt ondersteund. Zie [beschik bare Azure-Services in azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services)voor meer informatie.  

### <a name="prerequisites"></a>Vereisten
- Integratie met [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). Azure AD-gebruikers detectie is niet vereist.
- Dezelfde [vereisten voor Cloud beheer gateway](../clients/manage/cmg/plan-cloud-management-gateway.md#requirements), met uitzonde ring van het Azure-beheer certificaat.

### <a name="try-it-out"></a>Probeer het nu!  
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.

1. Vouw in de Configuration Manager-console de werk ruimte **beheer** **Cloud Services**uit en selecteer **cloudbeheergateway**. Klik op **Cloudbeheergateway maken** op het lint. 
2. Selecteer **Azure Resource Manager implementatie**op de pagina **Algemeen** . Klik op **Aanmelden** om te verifiëren met een Azure-abonnement beheerders account. Met de wizard worden de resterende velden automatisch ingevuld op basis van de Azure AD-abonnements gegevens die zijn opgeslagen tijdens de integratie vereisten. Als u meerdere abonnementen hebt, selecteert u het gewenste abonnement. Klik op **Volgende**.  
3. Geef op de pagina **instellingen** op de gebruikelijke wijze het PKI-certificaat bestand van de server op. Dit certificaat definieert de naam van de CMG-service in Azure. Selecteer de **regio**en selecteer vervolgens een optie voor de resource groep om **nieuwe te maken** of **bestaande te gebruiken**. Voer de naam van de nieuwe resource groep in of selecteer een bestaande resource groep in de vervolg keuzelijst. 
4. Voltooi de wizard.

> [!NOTE] 
> Voor de geselecteerde Azure AD-server-app wijst Azure de machtiging voor het abonnement op de **mede werker** toe. 

Controleer de voortgang van de service-implementatie met **cloudmgr. log** op het service verbindings punt.



## <a name="approve-application-requests-for-users-per-device"></a>Toepassings aanvragen voor gebruikers per apparaat goed keuren
<!-- 1357015 -->
Vanaf deze release, wanneer een gebruiker een toepassing aanvraagt die goed keuring vereist, is de specifieke apparaatnaam nu deel uit van de aanvraag. Als de beheerder de aanvraag goedkeurt, kan de gebruiker de toepassing alleen op dat apparaat installeren. De gebruiker moet een andere aanvraag indienen om de toepassing op een ander apparaat te installeren. 

> [!NOTE]
> Deze functie is optioneel. Wanneer u deze versie bijwerkt, schakelt u deze functie in de update wizard in. U kunt de functie ook later inschakelen in de-console. Zie voor meer informatie [Enable optional features from updates](../servers/manage/install-in-console-updates.md#bkmk_options).

### <a name="prerequisites"></a>Vereisten
- De Configuration Manager-client upgraden naar de nieuwste versie
- Schakel de client instelling **nieuwe software Center gebruiken** in de groep [computer agent](../clients/deploy/about-client-settings.md#computer-agent) in

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.

1. Implementeer een toepassing als beschikbaar voor een gebruikers verzameling.
2. Schakel op de pagina **implementatie-instellingen** de optie in: **een beheerder moet een aanvraag voor deze toepassing goed keuren op het apparaat**.
3. Als doel gebruiker kunt u Software Center gebruiken om een aanvraag in te dienen voor de toepassing. 
4. **Goedkeurings aanvragen** weer geven onder **toepassings beheer** in de werk ruimte **software bibliotheek** van de Configuration Manager-console. Er is nu een kolom **apparaat** in de lijst voor elke aanvraag. Wanneer u actie onderneemt voor de aanvraag, bevat het dialoog venster toepassings verzoek ook de naam van het apparaat van waaruit de gebruiker de aanvraag heeft ingediend.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Software Center gebruiken om door gebruikers beschik bare toepassingen te bladeren en te installeren op apparaten die zijn toegevoegd aan Azure AD
<!-- 1322613 -->
Als u toepassingen implementeert als beschikbaar voor gebruikers, kunnen ze deze nu bekijken en installeren via Software Center op Azure Active Directory Azure AD-apparaten.  

### <a name="prerequisites"></a>Vereisten
- HTTPS inschakelen op het beheer punt
- De site integreren met [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md)
- Een toepassing implementeren als beschikbaar voor een gebruikers verzameling
- Toepassings inhoud distribueren naar een [Cloud distributiepunt](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- Schakel de client instelling **nieuwe software Center gebruiken** in de groep [computer agent](../clients/deploy/about-client-settings.md#computer-agent) in
- De client moet: 
   - Windows 10
   - Azure AD-lid, ook wel bekend als een Cloud domein
- Voor de ondersteuning van Internet-clients:
    - [Cloudbeheergateway](../clients/manage/cmg/plan-cloud-management-gateway.md) 
    - Schakel de client instelling in: **gebruikers beleids aanvragen van internetclients inschakelen** in de [client beleids](../clients/deploy/about-client-settings.md#client-policy) groep
- Clients in het bedrijfs netwerk ondersteunen:
    - Het Cloud distributiepunt toevoegen aan een grens groep die wordt gebruikt door de clients
    - Clients moeten de Fully Qualified Domain Name (FQDN) van het beheer punt met HTTPS-functionaliteit kunnen omzetten



## <a name="report-on-windows-autopilot-device-information"></a>Gegevens over Windows auto pilot-apparaten rapporteren
<!-- 1351442 -->
Windows auto pilot is een oplossing voor het voorbereiden en configureren van nieuwe Windows 10-apparaten op een moderne manier. Zie voor meer informatie een [overzicht van Windows auto pilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Eén methode voor het registreren van bestaande apparaten met Windows auto pilot is het uploaden van apparaatgegevens naar het Microsoft Store voor bedrijven en onderwijs. Deze informatie omvat het serie nummer van het apparaat, de Windows-product-id en een hardware-id. Gebruik Configuration Manager om deze apparaatgegevens te verzamelen en te rapporteren. 

### <a name="prerequisites"></a>Vereisten
- Deze apparaatgegevens zijn alleen van toepassing op clients met Windows 10, versie 1703 en hoger

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.

1. Vouw in de Configuration Manager-console in de werk ruimte **bewaking** het knoop punt **rapportage** uit, vouw **rapporten**uit en selecteer het knoop punt **Hardware-algemeen** .
2. Voer het nieuwe rapport en de gegevens van het **Windows auto pilot-apparaat** uit en Bekijk de resultaten. 
3. Klik in de rapport viewer op het pictogram voor **exporteren** en selecteer **CSV (door komma's gescheiden)** .
4. Nadat u het bestand hebt opgeslagen, uploadt u de gegevens naar de Microsoft Store voor bedrijven en onderwijs. Zie voor meer informatie [apparaten toevoegen in Microsoft Store voor bedrijven en onderwijs](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Verbeteringen aan Configuration Manager-beleid voor Windows Defender exploit Guard
<!-- 1356220 -->
Er zijn aanvullende beleids instellingen voor de onderdelen kwets baarheid voor aanvallen en Controlled folder Access toegevoegd in Configuration Manager voor [Windows Defender exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection).

**Nieuwe instellingen voor gecontroleerde mappen toegang**<br/>
Er zijn twee extra opties voor het configureren van beheerde mappen toegang: **alleen schijf sectoren blok keren** en **alleen schijf sectoren controleren**. Deze twee instellingen zorgen ervoor dat Controlled folder Access alleen kan worden ingeschakeld voor opstart sectoren en de beveiliging van specifieke mappen of de standaard beveiligde mappen niet mogelijk maakt. 

**Nieuwe instellingen voor kwets baarheid voor aanvallen verminderen**
- Gebruik geavanceerde beveiliging tegen Ransomware.
- Blok keren dat referenties worden gestolen vanuit het subsysteem voor de lokale beveiligings autoriteit van Windows. 
- Voorkomen dat uitvoerbare bestanden worden uitgevoerd tenzij deze voldoen aan een bepaalde gangbaarheid, ouderdom of criteria voor vertrouwde lijsten. 
- Blokkeer niet-vertrouwde en niet-ondertekende processen die worden uitgevoerd vanaf een USB.



## <a name="microsoft-edge-browser-policies"></a>Micro soft Edge-browser beleid
<!-- 1357310 -->
Voor klanten die de [micro soft Edge](https://www.microsoft.com/itpro/microsoft-edge) -webbrowser op Windows 10-clients gebruiken, kunt u nu een Configuration Manager beleid voor nalevings instellingen maken voor het configureren van verschillende instellingen voor micro soft Edge. Dit beleid bevat momenteel de volgende instellingen:
- **Stel de micro soft Edge-browser in als standaard**: Hiermee wordt de Windows 10-standaard instelling voor apps voor de webbrowser geconfigureerd in micro soft Edge
- **Vervolg keuzelijst voor de adres balk toestaan**: vereist Windows 10, versie 1703 of hoger. Zie [AllowAddressBarDropdown-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)voor meer informatie.
- **Synchronisatie van favorieten tussen micro soft-browsers toestaan**: vereist Windows 10, versie 1703 of hoger. Zie [SyncFavoritesBetweenIEAndMicrosoftEdge-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)voor meer informatie.
- **Browse gegevens wissen bij afsluiten toestaan**: vereist Windows 10, versie 1703 of hoger. Zie [ClearBrowsingDataOnExit-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)voor meer informatie.
- **Do not track-headers toestaan**: Zie [AllowDoNotTrack-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)voor meer informatie.
- **Automatisch invullen toestaan**: Zie [AllowAutofill-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)voor meer informatie.
- **Cookies toestaan**: Zie [AllowCookies-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)voor meer informatie.
- **Pop-upblokkering toestaan**: Zie [AllowPopups-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)voor meer informatie.
- **Zoek suggesties in de adres balk toestaan**: Zie [AllowSearchSuggestionsinAddressBar-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)voor meer informatie.
- **Verzenden van intranet verkeer naar Internet Explorer toestaan**: Zie [SendIntranetTraffictoInternetExplorer-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)voor meer informatie.
- **Wachtwoord beheer toestaan**: Zie [AllowPasswordManager-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)voor meer informatie.
- **Ontwikkelhulpprogramma's toestaan**: Zie [AllowDeveloperTools-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)voor meer informatie.
- **Extensies toestaan**: Zie [AllowExtensions-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)voor meer informatie.

### <a name="prerequisites"></a>Vereisten
- Windows 10-client die Azure Active Directory lid is. 

### <a name="known-issues"></a>Bekende problemen
- On-premises apparaten die aan een domein zijn toegevoegd, kunnen dit beleid niet Toep assen in deze release. Dit probleem is ook van toepassing op hybride apparaten die lid zijn van een domein.

### <a name="try-it-out"></a>Probeer het nu!  
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.

**Beleid maken**
1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Vouw **instellingen voor naleving** uit en selecteer het knoop punt nieuwe **micro soft Edge-browser profielen** . Klik op de lint optie om het **micro soft Edge-browser beleid te maken**.
2. Geef een **naam** op voor het beleid, geef eventueel een **Beschrijving**op en klik op **volgende**.
3. Wijzig op de pagina **instellingen** de waarde die moet worden **geconfigureerd** voor de instellingen die u in dit beleid wilt gebruiken en klik op **volgende**.
4. Selecteer op de pagina **ondersteunde platforms** de versies van het besturings systeem en de architecturen waarop dit beleid van toepassing is en klik op **volgende**. 
5. Voltooi de wizard.

**Het beleid implementeren**
1. Selecteer uw beleid en klik op de lint optie die u wilt **implementeren**.
2. Klik op **Bladeren** om de verzameling van de gebruiker of het apparaat te selecteren waarvoor u het beleid wilt implementeren. 
3. Selecteer indien nodig extra opties. Waarschuwingen genereren wanneer het beleid niet compatibel is. Stel het schema in waarmee de client de naleving van het apparaat evalueert met dit beleid.
4. Klik op **OK** om de implementatie te maken.

Net als bij elk beleid voor nalevings instellingen herstelt de client de instellingen op de door u opgegeven planning. [Controleer en meld op](../../compliance/deploy-use/monitor-compliance-settings.md) apparaatcompatibiliteit in de Configuration Manager-console.



## <a name="report-for-default-browser-counts"></a>Rapport voor standaard aantal browsers
<!-- 1357830 -->
Er is nu een nieuw rapport om het aantal clients met een specifieke webbrowser weer te geven als de Windows-standaard versie. 

### <a name="known-issues"></a>Bekende problemen
- Wanneer u het rapport voor het eerst opent, worden alleen de aantallen en niet de BrowserProgID weer gegeven. U kunt dit probleem omzeilen door de query voor het rapport te bewerken in de volgende syntaxis:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Probeer het nu!  
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.
1. Vouw in de **Configuration Manager** -console, werk ruimte **controleren** , **rapportage**uit, vouw **rapporten**uit, selecteer **software-bedrijven en producten**.
2. Voer het rapport **aantal standaard browser** -items uit.

Gebruik de volgende referentie voor algemene BrowserProgIDs:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: micro soft Edge
- **Internet Explorer. HTTP**: micro soft Internet Explorer
- **ChromeHTML**: Google Chrome
- **OperaStable**: Opera Software
- **FirefoxURL-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Ondersteuning voor Windows 10 ARM64-apparaten
<!-- 1353704 -->
Vanaf deze release wordt de Configuration Manager-client ondersteund op Windows 10 ARM64-apparaten. Bestaande client beheer functies moeten samen werken met deze nieuwe apparaten. Bijvoorbeeld hardware-en software-inventaris, software-updates en toepassings beheer. Implementatie van besturings systeem wordt momenteel niet ondersteund. 

## <a name="changes-to-phased-deployments"></a>Wijzigingen in gefaseerde implementaties
<!-- 1357405 -->
Met gefaseerde implementaties wordt een gecoördineerde, geordende implementatie van software in meerdere verzamelingen geautomatiseerd. In deze Technical Preview-versie kan de gefaseerde implementatie wizard worden voltooid voor taken reeksen in de beheer console en implementaties worden gemaakt. De tweede fase wordt echter niet automatisch gestart na het voldoen aan de criteria voor slagen van de eerste fase. De tweede fase kan hand matig worden gestart met een SQL-instructie.   

### <a name="try-it-out"></a>Probeer het nu!  
  Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.
 
**Een gefaseerde implementatie voor een takenreeks maken** </br>
1. Vouw in de werk ruimte **software bibliotheek** **besturings systemen**uit en selecteer **taken reeksen**.
2. Klik met de rechter muisknop op een bestaande taken reeks en selecteer **gefaseerde implementatie maken**. 
3. Geef op het tabblad **Algemeen** de gefaseerde implementatie een naam, beschrijving (optioneel) en selecteer **automatisch een standaard implementatie met twee fasen maken**. 
4. Vul de velden **eerste verzameling** en **tweede verzameling** in. Selecteer **Next**.
5. Kies op het tabblad **instellingen** één optie voor elk van de plannings instellingen en selecteer **volgende** als u klaar bent. 
6. Bewerk op het tabblad **fasen** de gewenste fasen en klik vervolgens op **volgende**.
7. Bevestig uw selecties op het tabblad **samen vatting** en klik vervolgens op **volgende** om door te gaan.
8. Wanneer de criteria voor het slagen van de eerste fase zijn bereikt, volgt u de instructies om de tweede fase te starten met een SQL-instructie.
 
**Tweede fase starten met een SQL-instructie**
1. Bepaal de PhasedDeploymentID voor de implementatie die u hebt gemaakt met de volgende SQL-query:<br/> `Select * from PhasedDeployment`
2. Voer de volgende instructie uit om de productie fase te starten:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Volgende stappen
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking.    

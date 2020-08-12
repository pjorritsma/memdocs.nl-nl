---
title: Toepassingen implementeren
titleSuffix: Configuration Manager
description: Een implementatie van een toepassing maken of simuleren voor een apparaat of gebruikers verzameling
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c2fcd583e860273e2fbfc9fcda1e08053336345
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127510"
---
# <a name="deploy-applications-with-configuration-manager"></a>Toepassingen implementeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Een implementatie van een toepassing maken of simuleren voor een apparaat of gebruikers verzameling in Configuration Manager. Deze implementatie bevat instructies voor de Configuration Manager-client over hoe en wanneer de software moet worden geïnstalleerd.

Voordat u een toepassing kunt implementeren, moet u ten minste één implementatie type voor de toepassing maken. Zie [toepassingen maken](create-applications.md)voor meer informatie.

Vanaf versie 1906 kunt u een groep toepassingen maken die u kunt verzenden naar een gebruiker of apparaat als één implementatie. Zie [toepassings groepen maken](create-app-groups.md)voor meer informatie.

U kunt de implementatie van een toepassing ook simuleren. Deze simulatie test de toepas baarheid van een implementatie zonder de toepassing te installeren of te verwijderen. Een gesimuleerde implementatie evalueert de detectie methode, vereisten en afhankelijkheden voor een implementatie type en rapporteert de resultaten in het knoop punt **implementaties** van de werk ruimte **bewaking** . Zie [toepassings implementaties simuleren](simulate-application-deployments.md)voor meer informatie.

> [!NOTE]
> U kunt alleen de implementatie van vereiste toepassingen, maar geen pakketten of software-updates, simuleren.
>
> Door MDM Inge schreven apparaten bieden geen ondersteuning voor gesimuleerde implementaties, gebruikers ervaring of plannings instellingen.

## <a name="deploy-an-application"></a><a name="bkmk_deploy"></a>Een toepassing implementeren

1. In de Configuration Manager-console gaat u naar de werk ruimte **software bibliotheek** , vouwt u **toepassings beheer**uit en selecteert u het knoop punt **toepassingen** of **toepassings groepen** .

1. Selecteer een toepassing of toepassings groep in de lijst om te implementeren. Selecteer **implementeren**in het lint.  

> [!NOTE]
> Wanneer u de eigenschappen van een bestaande implementatie bekijkt, komen de volgende secties overeen met de tabbladen in het venster implementatie-eigenschappen:  
>
> - [Algemeen](#bkmk_deploy-general)
> - [Inhoud](#bkmk_deploy-content)
> - [Implementatie-instellingen](#bkmk_deploy-settings)
> - [Planning](#bkmk_deploy-sched)
> - [Gebruikers ervaring](#bkmk_deploy-ux)
> - [Waarschuwingen](#bkmk_deploy-alerts)

### <a name="deployment-general-information"></a><a name="bkmk_deploy-general"></a>**Algemene** informatie over implementatie

Geef op de pagina **Algemeen** van de wizard software implementeren de volgende informatie op:  

- **Software**: met deze waarde wordt de toepassing weer gegeven die moet worden geïmplementeerd. Selecteer **Bladeren** om een andere toepassing te kiezen.  

- **Verzameling**: Selecteer **Bladeren** om de doel verzameling voor deze toepassings implementatie te kiezen.

- **Standaard distributiepunten groepen gebruiken die aan deze verzameling zijn gekoppeld**: Sla de toepassings inhoud op in de standaard distributiepunten groep van de verzameling. Als u de geselecteerde verzameling niet hebt gekoppeld aan een distributiepunten groep, wordt deze optie grijs weer gegeven.  

- **Automatisch inhoud voor afhankelijkheden distribueren**: als een van de implementatie typen in de toepassing afhankelijkheden heeft, verzendt de site ook afhankelijke toepassings inhoud naar distributie punten.  

    >[!NOTE]
    > Als u de afhankelijke toepassing bijwerkt nadat u de primaire toepassing hebt geïmplementeerd, distribueert de site niet automatisch nieuwe inhoud voor de afhankelijkheid.

- **Opmerkingen (optioneel)**: Voer desgewenst een beschrijving in voor deze implementatie.

### <a name="deployment-content-options"></a><a name="bkmk_deploy-content"></a>Opties voor implementatie- **inhoud**

Selecteer op de pagina **inhoud** **toevoegen** om de inhoud voor deze toepassing te distribueren naar een distributie punt of een distributiepunten groep.

Als u de optie voor het **gebruik van standaard distributie punten die aan deze verzameling zijn gekoppeld** op de pagina algemeen hebt geselecteerd, wordt deze optie automatisch ingevuld. Alleen een lid van de beveiligingsrol **toepassings beheerder** kan dit wijzigen.

Als de inhoud van de toepassing al is gedistribueerd, worden deze hier weer gegeven.

### <a name="deployment-settings"></a><a name="bkmk_deploy-settings"></a>**Implementatie-instellingen**

Geef op de pagina **implementatie-instellingen** de volgende informatie op:  

- **Actie**: Kies in de vervolg keuzelijst of u deze implementatie wilt **installeren** of de toepassing wilt **verwijderen** .  

    > [!NOTE]  
    > Als u een implementatie maakt voor het **installeren** van een app en een andere implementatie om dezelfde app op hetzelfde apparaat te **verwijderen** , heeft de **installatie** -implementatie prioriteit.  

    U kunt de actie van een implementatie niet wijzigen nadat u deze hebt gemaakt.  

- **Doel**: kies in de vervolgkeuzelijst één van de volgende opties:  

  - **Beschikbaar**: de gebruiker ziet de toepassing in Software Center. Ze kunnen de app op aanvraag installeren.  

  - **Vereist**: de app wordt door de client automatisch geïnstalleerd volgens het schema dat u hebt ingesteld. Als de toepassing niet is verborgen, kan een gebruiker de implementatie status ervan volgen. Ze kunnen ook software Center gebruiken om de toepassing te installeren vóór de deadline.  

    > [!NOTE]  
    > Wanneer u de implementatie actie instelt op **verwijderen**, wordt het doel van de implementatie automatisch ingesteld op **vereist**. U kunt dit gedrag niet wijzigen.  

- **Eind gebruikers toestaan om deze toepassing te herstellen**: vanaf versie 1810, als u de toepassing met een herstel opdracht regel hebt gemaakt, schakelt u deze optie in. Gebruikers zien een optie in Software Center om de toepassing te **herstellen** .<!--1357866-->  

- **Software vooraf implementeren op het primaire apparaat van de gebruiker**: als de implementatie voor een gebruiker is, selecteert u deze optie om de toepassing te implementeren op het primaire apparaat van de gebruiker. Deze instelling vereist niet dat de gebruiker zich aanmeldt voordat de implementatie wordt uitgevoerd. Als de gebruiker moet communiceren met de installatie, selecteert u deze optie niet. Deze optie is alleen beschikbaar wanneer de implementatie is **vereist**.  

- **Ontwaak pakketten verzenden**: als de implementatie **vereist**is, stuurt Configuration Manager een Ontwaak pakket naar computers voordat de-client de implementatie uitvoert. Dit pakket activeert de computers tijdens de deadline van de installatie. Voordat u deze optie kunt gebruiken, moeten computers en netwerken worden geconfigureerd voor Wake On LAN. Zie [plan How to wake up clients](../../core/clients/deploy/plan/plan-wake-up-clients.md)(Engelstalig) voor meer informatie.  

- **Clients met een Internet verbinding naar gebruik toestaan inhoud te downloaden na de installatie deadline, waarvoor extra kosten**in rekening kunnen worden gebracht: deze optie is alleen beschikbaar voor implementaties met een **vereist**doel.  

- **Vervangen versie van deze toepassing automatisch bijwerken**: de vervangende versie van de toepassing wordt door de client bijgewerkt met de vervangende toepassing.

    > [!NOTE]
    > Deze optie werkt onafhankelijk van de goed keuring van de beheerder. Als een beheerder de vervangen versie al heeft goedgekeurd, hoeven ze de vervangende versie ook niet goed te keuren. Goed keuring is alleen voor nieuwe aanvragen, niet voor vervangen van upgrades.<!--515824-->  
    >
    > Voor het **beschik bare** installatie doel kunt u deze optie in-of uitschakelen. <!--1351266-->

#### <a name="approval-settings"></a><a name="bkmk_approval"></a>Goedkeurings instellingen

Het goedkeurings gedrag van de toepassing is afhankelijk van het feit of u de aanbevolen optionele functie inschakelt, **toepassings aanvragen voor gebruikers per apparaat goed keuren**.

- **Een beheerder moet een aanvraag voor deze toepassing op het apparaat goed keuren**: als u de optionele functie inschakelt, keurt de beheerder gebruikers aanvragen voor de toepassing goed voordat de gebruiker deze op het aangevraagde apparaat kan installeren. Als de beheerder de aanvraag goedkeurt, kan de gebruiker de toepassing alleen op dat apparaat installeren. De gebruiker moet een andere aanvraag indienen om de toepassing op een ander apparaat te installeren. Deze optie is niet beschikbaar wanneer het implementatie doel **vereist**is of wanneer u de toepassing implementeert in een verzameling apparaten.

- **Goed keuring van de beheerder vereisen als gebruikers deze toepassing aanvragen**: als u de optionele functie niet inschakelt, keurt de beheerder gebruikers aanvragen voor de toepassing goed voordat de gebruiker deze kan installeren. Deze optie is niet beschikbaar wanneer het implementatie doel **vereist**is of wanneer u de toepassing implementeert in een verzameling apparaten.  

Zie [toepassingen goed keuren](app-approval.md)voor meer informatie.

#### <a name="deployment-properties-deployment-settings"></a>Implementatie- **instellingen** voor implementatie-eigenschappen

Wanneer u de eigenschappen van een implementatie bekijkt, wordt de volgende optie weer gegeven op het tabblad **implementatie-instellingen** als deze wordt ondersteund door de implementatie type-technologie:

**Sluit automatisch alle actieve uitvoer bare bestanden die u hebt opgegeven op het tabblad installatie gedrag van het dialoog venster Eigenschappen van implementatie type**. Zie [controleren op actieve uitvoer bare bestanden voor het installeren van een toepassing](#bkmk_exe-check)voor meer informatie.

### <a name="deployment-scheduling-settings"></a><a name="bkmk_deploy-sched"></a>Instellingen voor implementatie **planning**

Stel op de pagina **planning** de tijd in waarop deze toepassing wordt geïmplementeerd of beschikbaar wordt gesteld voor client apparaten.

Configuration Manager wordt het implementatie beleid standaard beschikbaar voor clients. Als u de implementatie wilt maken, maar deze niet beschikbaar wilt maken voor clients tot een latere datum, configureert u de optie om **de toepassing zo te plannen dat deze beschikbaar moet zijn**. Selecteer vervolgens de datum en tijd, inclusief of dat is gebaseerd op UTC of de lokale tijd van de client.

Als de implementatie **vereist**is, geeft u ook de deadline voor de **installatie**op. Deze deadline is standaard zo snel mogelijk.

U moet bijvoorbeeld een nieuwe line-of-Business-toepassing implementeren. Alle gebruikers moeten de app op een bepaald moment installeren, maar u wilt ze de mogelijkheid geven om in een vroeg stadium te kiezen. U moet er ook voor zorgen dat de-site de inhoud heeft gedistribueerd naar alle distributie punten. U plant dat de toepassing binnen vijf dagen beschikbaar is vanaf vandaag. Dit schema geeft u de tijd om de inhoud te distribueren en de status ervan te bevestigen. Vervolgens stelt u de installatie deadline voor één maand vanaf vandaag in. Gebruikers zien de toepassing in Software Center wanneer deze binnen vijf dagen beschikbaar is. Als ze niets doen, installeert de-client de toepassing automatisch tijdens de installatie deadline.

Als de toepassing die u implementeert, een andere toepassing vervangt, stelt u de deadline van de installatie in wanneer gebruikers de nieuwe toepassing ontvangen. Stel de **installatie deadline** in om gebruikers met de vervangen toepassing te upgraden.

#### <a name="delay-enforcement-with-a-grace-period"></a>Afdwinging met een respijt periode

U kunt gebruikers meer tijd geven om vereiste toepassingen te installeren *na* eventuele deadlines die u hebt ingesteld. Dit gedrag is doorgaans vereist wanneer een computer gedurende een lange periode wordt uitgeschakeld en veel toepassingen moeten worden geïnstalleerd. Wanneer een gebruiker bijvoorbeeld een vakantie retourneert, moet deze gedurende een lange periode worden gewacht wanneer de client achterstallige implementaties installeert. Definieer een respijt periode voor afdwinging om dit probleem op te lossen.

- Configureer eerst deze respijt periode met de eigenschap **respijt periode voor afdwingen na de deadline van de implementatie (uren)** in de client instellingen. Zie de groep [computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent) voor meer informatie. Geef een waarde op tussen **1** en **120** uur.  

- Schakel op de pagina **planning** van een vereiste toepassings implementatie de optie in om het **afdwingen van deze implementatie op basis van gebruikers voorkeuren te vertragen, tot de respijt periode die in de client instellingen is gedefinieerd**. De respijt periode voor afdwinging is van toepassing op alle implementaties waarbij deze optie is ingeschakeld en is gericht op apparaten waarop u ook de client instelling hebt geïmplementeerd.

Na de deadline installeert de-client de toepassing in het eerste niet-zakelijke venster, dat door de gebruiker is geconfigureerd, tot deze respijt periode. De gebruiker kan echter nog steeds Software Center openen en de toepassing op elk gewenst moment installeren. Zodra de respijt periode is verlopen, wordt de afdwinging hersteld naar het normale gedrag voor achterstallige implementaties.

:::image type="content" source="media/grace-period.svg" alt-text="DIagram van tijd lijn van respijt periode":::

<!-- SCCMDocs issue #1599 -->

> [!NOTE]
> In de meeste gevallen behandelt deze functie het scenario wanneer het apparaat wordt uitgeschakeld terwijl de gebruiker zich niet op kantoor bevindt. Technisch gezien begint de respijt periode wanneer de client beleid na de deadline van de implementatie ontvangt. Hetzelfde gedrag treedt op als u de Configuration Manager-client service (CcmExec) stopt en deze na de deadline van de implementatie op een later tijdstip opnieuw opstart.

### <a name="deployment-user-experience-settings"></a><a name="bkmk_deploy-ux"></a>Instellingen voor **gebruikers ervaring** voor implementatie

Geef op de pagina **gebruikers ervaring** informatie op over hoe gebruikers kunnen communiceren met de installatie van de toepassing.

- **Meldingen voor gebruikers**: Geef op of meldingen in Software Center moeten worden weer gegeven op de geconfigureerde beschik bare tijd. Met deze instelling bepaalt u ook of gebruikers op de client computers moeten worden gewaarschuwd. Voor beschik bare implementaties kunt u de optie om te **verbergen in Software Center en alle meldingen**niet selecteren.  

  - **Wanneer er software wijzigingen zijn vereist, een dialoog venster weer geven voor de gebruiker in plaats van een pop-upmelding**<!--3555947-->: Vanaf versie 1902 selecteert u deze optie om de gebruikers ervaring te wijzigen. Dit geldt alleen voor vereiste implementaties. Zie [plan for Software Center](../plan-design/plan-for-software-center.md#bkmk_impact)(Engelstalig) voor meer informatie.

- **Software-installatie** en **opnieuw opstarten**van het systeem: Configureer deze instellingen alleen voor vereiste implementaties. Ze geven het gedrag aan wanneer de implementatie de deadline bereikt buiten de gedefinieerde onderhouds Vensters. Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.  

- **Verwerking van schrijf filters voor Windows Embedded-apparaten**: met deze instelling bepaalt u het installatie gedrag op Windows Embedded-apparaten waarvoor een schrijf filter is ingeschakeld. Kies de optie om wijzigingen door te voeren bij de deadline van de installatie of tijdens een onderhouds venster. Wanneer u deze optie selecteert, moet de computer opnieuw worden opgestart en worden de wijzigingen op het apparaat bewaard. Anders wordt de toepassing geïnstalleerd op de tijdelijke overlay en later vastgelegd.  

  - Wanneer u een software-update implementeert op een Windows Embedded-apparaat, moet u ervoor zorgen dat het apparaat lid is van een verzameling met een geconfigureerd onderhouds venster. Zie [Windows Embedded-toepassingen maken](../get-started/creating-windows-embedded-applications.md)voor meer informatie over onderhouds Vensters en Windows Embedded-apparaten.  

### <a name="deployment-alerts"></a><a name="bkmk_deploy-alerts"></a>Implementatie **waarschuwingen**

Configureer op de pagina **waarschuwingen** hoe Configuration Manager waarschuwingen genereert voor deze implementatie. Als u ook System Center Operations Manager gebruikt, moet u de waarschuwingen ook configureren. U kunt bepaalde waarschuwingen alleen configureren voor vereiste implementaties.

## <a name="create-a-phased-deployment"></a><a name="bkmk_phased"></a>Een gefaseerde implementatie maken

<!--1358147-->
Met gefaseerde implementaties kunt u een gecoördineerde, geordende implementatie van software organiseren op basis van aanpas bare criteria en groepen. U kunt bijvoorbeeld de toepassing implementeren in een pilot verzameling en vervolgens de implementatie automatisch voortzetten op basis van de criteria voor geslaagde pogingen.

Raadpleeg voor meer informatie de volgende artikelen:  

- [Een gefaseerde implementatie maken](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gefaseerde implementaties beheren en bewaken](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

## <a name="delete-a-deployment"></a><a name="bkmk_delete"></a>Een implementatie verwijderen

1. In de Configuration Manager-console gaat u naar de werk ruimte **software bibliotheek** , vouwt u **toepassings beheer**uit en selecteert u het knoop punt **toepassingen** of **toepassings groepen** .  

1. Selecteer de toepassing of toepassings groep die de implementatie bevat die u wilt verwijderen.  

1. Ga naar het tabblad **implementaties** van het detail venster en selecteer de implementatie.  

1. Selecteer in het lint op het tabblad **implementatie** in de groep **implementatie** de optie **verwijderen**.  

Wanneer u een toepassings implementatie verwijdert, worden alle exemplaren van de toepassing die clients al hebben geïnstalleerd, niet verwijderd. Als u deze **toepassingen wilt verwijderen**, implementeert u de toepassing op computers om te verwijderen. Als u een toepassings implementatie verwijdert, is de toepassing niet meer zichtbaar in Software Center. Hetzelfde gedrag treedt op wanneer u een resource verwijdert uit de doel verzameling voor de implementatie.

## <a name="user-notifications-for-required-deployments"></a><a name="bkmk_notify"></a>Gebruikers meldingen voor vereiste implementaties

Wanneer gebruikers de vereiste software ontvangen en de instelling **uitstellen en herinneren** selecteren, kunnen ze kiezen uit de volgende opties:  

- **Later**: geeft aan dat meldingen worden gepland op basis van de instellingen voor meldingen die in de client instellingen zijn geconfigureerd.  

- **Vaste tijd**: Hiermee geeft u op dat de melding moet worden weer gegeven na de geselecteerde tijd. Als u bijvoorbeeld 30 minuten selecteert, wordt de melding weer gegeven in 30 minuten.  

:::image type="content" source="media/ComputerAgentSettings.png" alt-text="Computer agent-groep in standaard client instellingen":::

De maximale uitstel tijd is altijd gebaseerd op de meldings waarden die op elke keer worden geconfigureerd in de client instellingen in de implementatie tijdlijn. Bijvoorbeeld:  

- U configureert de **implementatie deadline langer dan 24 uur, stelt gebruikers elke (uren)** instelling voor 10 uur op de pagina **computer agent** in.  

- De client geeft het meldings dialoogvenster meer dan 24 uur vóór de deadline van de implementatie weer.  

- In het dialoog venster worden de opties voor uitstellen weer gegeven tot maar nooit meer dan 10 uur.  

- Naarmate de implementatie deadline aanpakt, worden in het dialoog venster minder opties weer gegeven. Deze opties zijn consistent met de relevante client instellingen voor elk onderdeel van de implementatie tijdlijn.  

Voor een implementatie met een hoog risico, zoals een taken reeks die een besturings systeem implementeert, is het gebruikers meldings proces meer in de praktijk. In plaats van een waarschuwing op de taak balk wordt een dialoog venster weer gegeven, zoals in het volgende voor beeld van een melding dat kritiek software onderhoud is vereist:

:::image type="content" source="media/client-toast-notification.png" alt-text="Dialoog venster met vereiste software waarschuwt u voor kritiek software onderhoud":::

## <a name="check-for-running-executable-files"></a><a name="bkmk_exe-check"></a>Controleren op het uitvoeren van uitvoer bare bestanden

Configureer een implementatie om te controleren of bepaalde uitvoer bare bestanden worden uitgevoerd op de client. Gebruik deze optie om te controleren of er processen zijn die de installatie van de toepassing kunnen verstoren. Als een van deze uitvoer bare bestanden wordt uitgevoerd, blokkeert de client de installatie van het implementatie type. De gebruiker moet het uitgevoerde uitvoer bare bestand sluiten voordat de client het implementatie type kan installeren. Voor implementaties met een doel van vereist, kan de client automatisch het uitgevoerde uitvoer bare bestand sluiten.

1. Open de **Eigenschappen** voor het implementatie type.

1. Ga naar het tabblad **installatie gedrag** en selecteer **toevoegen**.

1. Voer in het venster **uitvoerbaar bestand toevoegen** de naam in van het uitvoer bare bestand van het doel. Voer desgewenst een beschrijvende naam in voor de toepassing om deze in de lijst te identificeren.

1. Selecteer **OK** om het venster Eigenschappen van implementatie type op te slaan en te sluiten.

1. Wanneer u de toepassing implementeert, selecteert u de optie voor het **automatisch sluiten van uitvoer bare bestanden die u hebt opgegeven op het tabblad installatie gedrag van het dialoog venster Eigenschappen van implementatie type**. Deze optie bevindt zich op het tabblad **implementatie-instellingen** van de implementatie-eigenschappen.  

> [!NOTE]
> Als u een toepassing configureert om te controleren of uitvoer bare bestanden worden uitgevoerd en deze op te geven in de taken reeks stap [toepassing installeren](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) , kan deze niet worden geïnstalleerd door de taken reeks. Als u deze taken reeks stap niet configureert om door te gaan met de fout, mislukt de hele taken reeks.

### <a name="client-behaviors-and-user-notifications"></a>Client gedrag en gebruikers meldingen

Nadat clients de implementatie hebben ontvangen, geldt het volgende gedrag:  

- Als u de toepassing als **beschikbaar**hebt geïmplementeerd en een gebruiker probeert deze te installeren, vraagt de client de gebruiker om de opgegeven uitvoer bare bestanden te sluiten voordat de installatie wordt voortgezet.  

- Als u de toepassing als **vereist**implementeerde en hebt opgegeven voor het **automatisch sluiten van uitvoer bare bestanden die u hebt opgegeven op het tabblad installatie gedrag van het dialoog venster Eigenschappen van implementatie type**, wordt er een melding weer gegeven op de client. Hiermee wordt de gebruiker ervan op de hoogte gebracht dat de opgegeven uitvoer bare bestanden automatisch worden gesloten wanneer de deadline voor de installatie van de toepassing wordt bereikt.  

  - Plan deze dialoog vensters in de groep **computer agent** van client instellingen. Zie [computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent)voor meer informatie.  

  - Als u niet wilt dat de gebruiker deze berichten ziet, selecteert u de optie om te **verbergen in Software Center en alle meldingen** op het tabblad **gebruikers ervaring** van de eigenschappen van de implementatie. Zie [instellingen voor gebruikers ervaring voor implementatie](#bkmk_deploy-ux)voor meer informatie.  

- Als u de toepassing als **vereist**hebt geïmplementeerd en geen **actieve uitvoer bare bestanden die u hebt opgegeven op het tabblad installatie gedrag van het dialoog venster Eigenschappen van implementatie type worden automatisch gesloten**, mislukt de installatie van de app als een of meer van de opgegeven toepassingen worden uitgevoerd.  

## <a name="deploy-user-available-applications"></a>Gebruikers beschik bare toepassingen implementeren

Wanneer u toepassingen implementeert als **beschikbaar** voor gebruikers verzamelingen, kunnen gebruikers door Software Center bladeren en de apps installeren die ze nodig hebben. Voor on-premises clients die lid zijn van een domein, gebruikt software Center de domein referenties van de gebruiker om de lijst met beschik bare toepassingen van het beheer punt op te halen.

Er zijn aanvullende vereisten voor clients die zijn gebaseerd op internet en die lid zijn van Azure Active Directory (Azure AD) of beide.

### <a name="azure-ad-joined-devices"></a>Azure AD-toegevoegde apparaten
<!-- 1322613 -->

Als u toepassingen implementeert als beschikbaar voor gebruikers, kunnen ze door middel van software Center op Azure AD-apparaten bladeren en deze installeren. Configureer de volgende vereisten om dit scenario in te scha kelen:

- HTTPS inschakelen op het beheer punt  

- De site integreren met [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) voor **Cloud beheer**  

  - [Azure AD-gebruikers detectie](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc) configureren  

- Een toepassing implementeren als beschikbaar voor een verzameling gebruikers vanuit Azure AD  

- Schakel de client instelling **nieuwe software Center gebruiken** in de groep [computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent) in  

- Het besturings systeem van de client moet Windows 10 zijn en lid zijn van Azure AD. Als een net-lid van een Cloud domein of hybride Azure AD.  

- Voor de ondersteuning van Internet-clients:  

  - [Cloud beheer gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG)

  - Toepassings inhoud distribueren naar een CMG of een [Cloud distributiepunt](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

  - Schakel de client instelling in: **gebruikers beleids aanvragen van internetclients inschakelen** in de [client beleids](../../core/clients/deploy/about-client-settings.md#client-policy) groep  

- Clients op het intranet ondersteunen:  

  - Voeg het CMG of Cloud distributiepunt toe aan een grens groep die wordt gebruikt door de clients  

  - Clients moeten de Fully Qualified Domain Name (FQDN) van het beheer punt met HTTPS-functionaliteit oplossen  

  > [!NOTE]
  > Voor een client die is gedetecteerd als op het intranet, maar communiceert via de Cloud Management Gateway (CMG) in Configuration Manager versie 2002 en eerder, gebruikt software Center Windows-verificatie. Als er is geprobeerd de lijst met door gebruikers beschik bare apps op te halen via CMG, mislukt dit. Vanaf versie 2006 maakt het gebruik van de identiteit van Azure Active Directory (Azure AD) voor apparaten die zijn gekoppeld aan Azure AD. Deze apparaten kunnen deel uitmaken van de Cloud of hybride lid zijn.<!--6935376-->

## <a name="next-steps"></a>Volgende stappen

- [Toepassingen bewaken](monitor-applications-from-the-console.md)
- [Problemen oplossen met de implementatie van toepassingen](troubleshoot-application-deployment.md)
- [Beheer taken voor toepassingen](management-tasks-applications.md)
- [Gebruikershandleiding van Software Center](../../core/understand/software-center.md)

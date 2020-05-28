---
title: Toepassingen goedkeuren
titleSuffix: Configuration Manager
description: Meer informatie over de instellingen en het gedrag voor het goed keuren van toepassingen in Configuration Manager.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f725c1b7dc380a84cd94e666b98dbd309df3744c
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802052"
---
# <a name="approve-applications-in-configuration-manager"></a>Toepassingen goed keuren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u [een toepassing implementeert](deploy-applications.md) in Configuration Manager, kunt u goed keuring vereisen vóór de installatie. Gebruikers aanvragen de toepassing in Software Center en vervolgens controleert u de aanvraag in de Configuration Manager-console. U kunt de aanvraag goed keuren of weigeren.

## <a name="approval-settings"></a><a name="bkmk_approval"></a>Goedkeurings instellingen

Het goedkeurings gedrag van de toepassing is afhankelijk van of u de aanbevolen ervaring voor het [goed keuren van de optionele app](#bkmk_opt)inschakelt. Een van de volgende goedkeurings instellingen wordt weer gegeven op de pagina **implementatie-instellingen** van de implementatie van de toepassing:  

### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a><a name="bkmk_opt"></a>Een beheerder moet een aanvraag voor deze toepassing op het apparaat goed keuren

> [!Note]  
> Configuration Manager schakelt deze functie standaard niet in. Voordat u deze kunt gebruiken, moet u de optionele functie **toepassings aanvragen voor gebruikers per apparaat goed keuren**. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
>
> Als u deze functie niet inschakelt, ziet u de [vorige ervaring](#bkmk_prior).  

De beheerder keurt gebruikers aanvragen voor de toepassing goed voordat de gebruiker deze op het aangevraagde apparaat kan installeren. Als de beheerder de aanvraag goedkeurt, kan de gebruiker de toepassing alleen op dat apparaat installeren. De gebruiker moet een andere aanvraag indienen om de toepassing op een ander apparaat te installeren. Deze optie is niet beschikbaar wanneer het implementatie doel **vereist**is of wanneer u de toepassing implementeert in een verzameling apparaten. <!--1357015-->  

> [!Note]  
> Als u gebruik wilt maken van nieuwe Configuration Manager functies, moet u clients eerst bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.<!--SCCMDocs issue 646-->  

**Toepassings aanvragen** weer geven onder **toepassings beheer** in de werk ruimte **software bibliotheek** van de Configuration Manager-console. (In versie 1902 en eerder wordt dit knoop punt **goedkeurings aanvragen**genoemd.) Er is nu een kolom **apparaat** in de lijst voor elke aanvraag. Wanneer u actie onderneemt voor de aanvraag, bevat het dialoog venster toepassings verzoek ook de naam van het apparaat van waaruit de gebruiker de aanvraag heeft ingediend.

Als een aanvraag niet binnen 30 dagen wordt goedgekeurd, wordt deze verwijderd. Wanneer de client opnieuw wordt geïnstalleerd, worden alle goedkeurings aanvragen in behandeling geannuleerd.  

Wanneer u goed keuring vereist voor een implementatie naar een apparaat, wordt de app niet weer gegeven in Software Center. Als u goed keuring vereist voor een implementatie naar een gebruikers verzameling, wordt de app weer gegeven in Software Center. U kunt deze nog steeds verbergen voor gebruikers met de client instelling, niet- **goedgekeurde toepassingen verbergen in Software Center**. Zie [client instellingen voor Software Center](../../core/clients/deploy/about-client-settings.md#software-center)voor meer informatie.

Nadat u een toepassing hebt goedgekeurd voor installatie, kunt u de aanvraag in de Configuration Manager-console **weigeren** . Als gebruikers de toepassing nog niet hebben geïnstalleerd, stopt deze actie met het installeren van nieuwe exemplaren van de toepassing vanuit software Center. Als een toepassing eerder is goedgekeurd en geïnstalleerd en u de aanvraag voor de toepassing **weigert** , verwijdert de client de toepassing van het apparaat van de gebruiker.<!--1357891-->

Vanaf versie 1906, als u een app-aanvraag goedkeurt in de-console en deze vervolgens weigert, kunt u deze nu opnieuw goed keuren. Nadat u het hebt goedgekeurd, wordt de app opnieuw op de client geïnstalleerd.  <!-- 4224910 -->

Automatiseer het goedkeurings proces met de Power shell [-cmdlet goed keuren-CMApprovalRequest](https://docs.microsoft.com/powershell/module/configurationmanager/approve-cmapprovalrequest?view=sccm-ps) . Vanaf versie 1902 bevat deze cmdlet de para meter **InstallActionBehavior** . Gebruik deze para meter om op te geven of de toepassing direct moet worden geïnstalleerd of buiten kantoor uren.<!-- SCCMDocs-pr issue #3418 -->

Vanaf 1906 kunt u zien welke implementaties goed keuring vereisen. Selecteer een app in het knoop punt **toepassingen** . Ga in het detail venster naar het tabblad **implementaties** . Er is een nieuwe kolom die standaard wordt weer gegeven, **vereist goed keuring**.

#### <a name="retry-the-install-of-pre-approved-applications"></a><a name="bkmk_retry"></a>De installatie van vooraf goedgekeurde toepassingen opnieuw uitvoeren

<!--4336307-->
Vanaf versie 1906 kunt u de installatie opnieuw uitvoeren van een app die u eerder hebt goedgekeurd voor een gebruiker of apparaat. De goedkeurings optie is alleen voor beschik bare implementaties. Als de gebruiker de app verwijdert of als het eerste installatie proces mislukt, Configuration Manager de status ervan niet opnieuw evalueren en opnieuw installeren. Met deze functie kan een ondersteunings medewerker snel de installatie van de app opnieuw proberen voor een gebruiker die hulp aanroept.

1. Open de Configuration Manager-console als een gebruiker met de machtiging **goed keuren** voor het toepassings object. De ingebouwde rollen van de **toepassings beheerder** of de maker van de **toepassing** hebben bijvoorbeeld deze machtiging.

1. Implementeer een app waarvoor goed keuring is vereist en goed keuring.

    > [!Tip]  
    > U kunt ook [een toepassing voor een apparaat installeren](install-app-for-device.md). Er wordt een goedgekeurde aanvraag voor de app op het apparaat gemaakt.  

Als de toepassing niet kan worden geïnstalleerd, of als de gebruiker de app verwijdert, gebruikt u het volgende proces om het opnieuw te proberen:

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **toepassings aanvragen** . (In versie 1902 en eerder wordt dit knoop punt **goedkeurings aanvragen**genoemd.)

1. Selecteer de eerder goedgekeurde app. Selecteer opnieuw **installeren**in de groep goedkeurings aanvraag van het lint.

#### <a name="other-app-approval-resources"></a>Andere resources voor het goed keuren van apps

- [Verbeteringen in de goedkeuring van toepassingen in ConfigMgr 1810](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534)
- [Updates voor het goedkeurings proces van de toepassing in Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048)

### <a name="require-administrator-approval-if-users-request-this-application"></a><a name="bkmk_prior"></a>Goed keuring van de beheerder vereisen als gebruikers deze toepassing aanvragen

> [!Note]  
> Deze ervaring is van toepassing als u de aanbevolen [ervaring voor het goed keuren van een optionele app](#bkmk_opt)niet inschakelt.

De beheerder keurt alle gebruikers aanvragen voor de toepassing goed voordat deze door de gebruiker kan worden geïnstalleerd. Deze optie is niet beschikbaar wanneer het implementatie doel **vereist**is of wanneer u de toepassing implementeert in een verzameling apparaten.  

Aanvragen voor het goed keuren van toepassingen worden weer gegeven in het knoop punt **toepassings aanvragen** onder **toepassings beheer** in de werk ruimte **software bibliotheek** . (In versie 1902 en eerder wordt dit knoop punt **goedkeurings aanvragen**genoemd.) Als een aanvraag niet binnen 30 dagen wordt goedgekeurd, wordt deze verwijderd. Wanneer de client opnieuw wordt geïnstalleerd, worden alle goedkeurings aanvragen in behandeling geannuleerd.  

Nadat u een toepassing hebt goedgekeurd voor installatie, kunt u de aanvraag in de Configuration Manager-console **weigeren** . Deze actie zorgt er niet voor dat de client de toepassing van alle apparaten verwijdert. Hiermee wordt voor komen dat gebruikers nieuwe exemplaren van de toepassing installeren vanuit software Center.  

## <a name="email-notifications"></a><a name="bkmk_email-approve"></a>E-mail meldingen

<!--1321550-->

U kunt e-mail meldingen configureren voor aanvragen voor het goed keuren van toepassingen. Wanneer een gebruiker een toepassing aanvraagt, ontvangt u een e-mail bericht. Klik op koppelingen in het e-mail bericht om de aanvraag goed te keuren of te weigeren zonder dat de Configuration Manager-console is vereist.

U kunt de e-mail adressen opgeven van de gebruikers die de aanvraag kunnen goed keuren of weigeren tijdens het maken van een nieuwe implementatie voor de toepassing. Als u later de lijst met e-mail adressen wilt wijzigen, gaat u naar de werk ruimte **bewaking** , vouwt u **waarschuwingen**uit en selecteert u het knoop punt **abonnementen** . Selecteer **Eigenschappen** van een van de **toepassing goed keuren via e-mail** abonnementen die betrekking hebben op de implementatie van uw toepassing.

Als er meer dan één waarschuwing is, kunt u bepalen welke waarschuwing meegaat met de implementatie. Open de eigenschappen van de waarschuwing en Bekijk de lijst met **Geselecteerde waarschuwingen** op het tabblad Algemeen. De implementatie is ingeschakeld als de waarschuwing voor dit abonnement.

Gebruikers kunnen een opmerking toevoegen aan de aanvraag vanuit software Center. Deze opmerking wordt weer gegeven in de toepassings aanvraag in de Configuration Manager-console. Vanaf versie 1902 wordt die opmerking ook in het e-mail bericht weer gegeven. Met deze opmerking in het e-mail bericht kunnen goed keurders een betere beslissing nemen om de aanvraag goed te keuren of te weigeren.<!--3594063-->

### <a name="prerequisites"></a>Vereisten

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>E-mail meldingen verzenden en actie ondernemen op intern netwerk

Met deze vereisten ontvangen ontvangers een e-mail met een melding van de aanvraag. Als ze zich in het interne netwerk bevinden, kunnen ze de aanvraag ook vanuit de e-mail goed keuren of weigeren.

- De [optionele functie](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **voor het goed keuren van toepassings aanvragen voor gebruikers per apparaat**inschakelen.  

- [E-mail meldingen voor waarschuwingen](../../core/servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts)configureren.  

    > [!NOTE]
    > De gebruiker met beheerders rechten die de toepassing implementeert, heeft toestemming nodig om een waarschuwing en een abonnement te maken. Als deze gebruiker niet over deze machtigingen beschikt, zien ze een fout aan het einde van de **wizard software implementeren**: "u hebt geen beveiligings rechten om deze bewerking uit te voeren."<!-- 2810283 -->

- Schakel de SMS-provider op de primaire site in om een certificaat te gebruiken.<!--SCCMDocs-pr issue 3135--> Gebruik een van de volgende opties:  

  - Aanbevelingen [Uitgebreide http](../../core/plan-design/hierarchy/enhanced-http.md) inschakelen voor de primaire site.

    > [!Note]  
    > Wanneer de primaire site een certificaat voor de SMS-provider maakt, wordt deze niet vertrouwd door de webbrowser op de client. Op basis van uw beveiligings instellingen wordt er mogelijk een beveiligings waarschuwing weer gegeven wanneer u reageert op een toepassings aanvraag.  

  - U kunt een PKI-certificaat hand matig binden aan poort 443 in IIS op de server die als host fungeert voor de functie SMS-provider op de primaire site.

> [!NOTE]
> Als u meerdere onderliggende primaire sites in een hiërarchie hebt, configureert u deze vereisten voor elke primaire site waar u deze functie wilt inschakelen. De koppelingen in de e-mail melding zijn voor de beheer service op de primaire site.<!-- 7108472 -->

#### <a name="to-take-action-from-internet"></a>Actie ondernemen van Internet

Met deze aanvullende optionele vereisten kan de ontvanger de aanvraag vanaf elke locatie goed keuren of afwijzen die toegang heeft tot internet.

- Schakel de service SMS-provider beheer in via de Cloud beheer gateway. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **servers en site systeem rollen** . Selecteer de server met de functie SMS-provider. Selecteer in het detail venster de rol **SMS-provider** en selecteer **Eigenschappen** in het lint op het tabblad siterol. selecteer de optie om **Configuration Manager Cloud beheer gateway verkeer voor de beheer service toe te staan**.  

- De SMS-provider vereist **.net 4.5.2** of hoger.  

- Stel een [Cloud beheer gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)in.

- De site onboarden naar [Azure-Services](../../core/servers/deploy/configure/azure-services-wizard.md) voor **Cloud beheer**.

- Schakel [Azure AD-gebruikers detectie](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc)in.

- Instellingen in azure AD hand matig configureren:  

    1. Ga naar de [Azure Portal](https://portal.azure.com) als gebruiker met *globale beheerders* machtigingen. Ga naar **Azure Active Directory**en selecteer **app-registraties**.  

    1. Selecteer de toepassing die u hebt gemaakt voor Configuration Manager integratie van **Cloud beheer** .  

    1. Selecteer in het menu **beheren** de optie **verificatie**.  

        1. Plak in het gedeelte **omleidings-uri's** in het volgende pad:`https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

        1. Vervang door `<CMG FQDN>` de Fully Qualified Domain Name (FQDN) van uw CMG-service (Cloud Management Gateway). Bijvoorbeeld GraniteFalls.Contoso.com.  

        1. Selecteer vervolgens **Opslaan**.  

    1. Selecteer in het menu **beheren** de optie **manifest**.  

        1. Zoek in het deel venster manifest bewerken de eigenschap **oauth2AllowImplicitFlow** .  

        1. Wijzig de waarde in **True**. De volledige regel moet er bijvoorbeeld uitzien als in de volgende regel:`"oauth2AllowImplicitFlow": true,`  

        1. Selecteer **Opslaan**.  

### <a name="configure-email-approval"></a>Goed keuring van e-mail configureren

1. Implementeer in de Configuration Manager-console [een toepassing](deploy-applications.md) als beschikbaar voor een verzameling gebruikers. Schakel op de pagina **implementatie-instellingen** het in voor goed keuring. Voer vervolgens een of meer e-mail adressen in om een melding te ontvangen. Scheid e-mail adressen met een punt komma ( `;` ).  

     > [!Note]  
     > Iedereen in uw Azure AD-organisatie die het e-mail bericht ontvangt, kan de aanvraag goed keuren. Stuur het e-mail bericht niet door naar anderen, tenzij u wilt dat ze actie ondernemen.  

2. Als gebruiker vraagt u de toepassing op in Software Center.  

3. U ontvangt binnen vijf minuten een e-mail melding. De inhoud van het e-mail bericht is vergelijkbaar met het volgende voor beeld:  

![Voor beeld van een e-mail melding voor een toepassings goedkeuring](media/1321550-email.png)

> [!Note]  
> De koppeling die u wilt goed keuren of weigeren, is voor eenmalig gebruik. U kunt bijvoorbeeld een groeps alias configureren voor het ontvangen van meldingen. MB keurt de aanvraag goed. Bruce kan de aanvraag nu niet weigeren.  

Controleer het bestand **NotiCtrl. log** op de site server voor probleem oplossing.

## <a name="maintenance"></a>Onderhoud

Configuration Manager slaat de informatie over de goedkeurings aanvraag van de toepassing op in de site database. Voor aanvragen die worden geannuleerd of geweigerd, verwijdert de site de aanvraag geschiedenis na 30 dagen. U kunt dit verwijderings gedrag configureren met de taak **verouderde gegevens** van de [site](../../core/servers/manage/maintenance-tasks.md)voor toepassings aanvraag verwijderen. De site verwijdert nooit goedgekeurde of in behandeling zijnde toepassings aanvragen.

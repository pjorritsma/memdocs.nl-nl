---
title: Wat is er nieuw in versie 2006
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 2006 van Configuration Manager current branch.
ms.date: 09/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b071746-61e1-404b-8053-60978de028a7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3c061236202e685a6b59eeca3254a80cc1ddabf9
ms.sourcegitcommit: 9d5c7a5e6ec430dc02d6d345028f6b29f6579b20
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385359"
---
# <a name="whats-new-in-version-2006-of-configuration-manager-current-branch"></a>Wat is er nieuw in versie 2006 van Configuration Manager current branch

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 2006 voor Configuration Manager current branch is beschikbaar als een update in de console. Deze update Toep assen op sites waarop versie 1810 of hoger wordt uitgevoerd. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->In dit artikel vindt u een overzicht van de wijzigingen en nieuwe functies in Configuration Manager, versie 2006.

Bekijk altijd de laatste controle lijst voor het installeren van deze update. Zie [Check List for Install update 2006](../../servers/manage/checklist-for-installing-update-2006.md)(Engelstalig) voor meer informatie. Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).

Als u optimaal wilt profiteren van de nieuwe functies van Configuration Manager, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

> [!TIP]
> Als u een melding wilt ontvangen wanneer deze pagina wordt bijgewerkt, kopieert en plakt u de volgende URL in uw RSS feed-lezer: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2006+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Micro soft Endpoint Manager-Tenant koppelen

### <a name="tenant-attach-microsoft-defender-antivirus-policies-in-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> Tenant bijvoegen: micro soft Defender anti virus Policies in het beheer centrum van micro soft Endpoint Manager
<!--4812909-->
U kunt nu micro soft Defender anti virus-beleid maken in de micro soft Endpoint Manager-console en implementeren in Configuration Manager-verzamelingen. Raadpleeg de volgende artikelen voor meer informatie, waaronder gedetailleerde instructies en beschik bare instellingen:
- [Tenant bijvoegen: Configuration Manager-clients onboarden naar micro soft Defender ATP vanuit het beheer centrum (preview-versie)](../../../tenant-attach/atp-onboard.md)
- [Tenant bijvoegen: beleid voor beveiliging van eind punten implementeren vanuit het beheer centrum (preview-versie)](../../../tenant-attach/deploy-antivirus-policy.md)
- [Instellingen voor het anti virus beleid van micro soft Defender voor aan de Tenant gekoppelde apparaten in Microsoft intune](../../../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json). 

### <a name="install-applications-from-the-admin-center"></a>Toepassingen installeren vanuit het beheer centrum
<!--7518897, 6024389-->
Vanuit het micro soft Endpoint Manager-beheer centrum kunt u een installatie van een toepassing in realtime initiëren voor een apparaat dat is gekoppeld aan een Tenant. Vanaf Configuration Manager versie 2006 bevat de lijst met toepassingen die beschikbaar zijn voor het apparaat ook toepassingen die zijn geïmplementeerd op de momenteel aangemelde gebruiker van het apparaat. Zie voor meer informatie [Tenant koppelen: Installeer een toepassing vanuit het beheercentrum](../../../tenant-attach/applications.md).  

### <a name="import-previously-created-azure-ad-application-during-tenant-attach-onboarding"></a>Eerder gemaakte Azure AD-toepassing importeren tijdens het voorbereiden van de Tenant bijvoegen
<!--6479246-->
Tijdens een nieuwe onboarding kan een beheerder een eerder gemaakte toepassing opgeven tijdens het voorbereiden op het koppelen van de Tenant. Raadpleeg voor meer informatie [Microsoft Endpoint Manager-tenant koppelen: Synchronisatie van apparaten en apparaatacties](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app).

## <a name="endpoint-analytics"></a><a name="bkmk_ea"></a> Endpoint Analytics

### <a name="endpoint-analytics-data-collection-enabled-by-default"></a>Endpoint Analytics-gegevens verzameling is standaard ingeschakeld
<!--7065447, 7741111-->
De client instelling **endpoint Analytics-gegevens verzameling inschakelen** is nu standaard ingeschakeld. Met deze instelling kunnen uw beheerde eind punten gegevens verzenden, zoals het opstarten van prestatie inzichten, naar uw Configuration Manager-site server. Deze wijziging is alleen van invloed op lokale gegevens verzameling. Endpoint Analytics-gegevens worden niet geüpload naar het beheer centrum van micro soft Endpoint Manager totdat u het [uploaden van gegevens in Configuration Manager inschakelt](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload). De nieuwe standaard waarde is van toepassing op de standaard client instellingen en eventuele aangepaste client instellingen die zijn gemaakt na de upgrade naar versie 2006.

- Als u een upgrade uitvoert van versie 2002 naar versie 2006, worden bestaande waarden voor aangepaste client instellingen behouden. De standaard waarde voor het inschakelen van de **gegevens verzameling endpoint Analytics** in Configuration Manager versie 2002 is **Nee**.
- Als u een upgrade uitvoert naar versie 2006 van Configuration Manager versie 1910 of eerder, nemen alle vooraf bestaande aangepaste client instellingen die de groep instellingen van **computer agent** bevatten de nieuwe standaard waarde **Ja** voor het **inschakelen van gegevens verzameling endpoint Analytics**.

Zie [Configure endpoint Analytics-gegevens verzameling in Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload)voor meer informatie.

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Site-infra structuur

### <a name="vpn-boundary-type"></a>Type VPN-grens

<!--7020519-->

Om het beheer van externe clients te vereenvoudigen, kunt u nu een nieuw grens type maken voor Vpn's. Voorheen moest u grenzen voor VPN-clients maken op basis van het IP-adres of subnet. Deze configuratie kan lastig of niet mogelijk zijn vanwege de configuratie van het subnet of het VPN-ontwerp.

Wanneer een client een locatie aanvraag verstuurt, bevat deze extra informatie over de netwerk configuratie. Op basis van deze informatie bepaalt de server of de client zich op een VPN bevindt.

Zie [grenzen definiëren](../../servers/deploy/configure/boundaries.md)voor meer informatie.

### <a name="management-insights-to-optimize-for-remote-workers"></a>Beheer inzichten die u kunt optimaliseren voor externe werk nemers

<!--6982226-->

Deze release voegt een nieuwe groep beheer inzichten toe en **Optimaliseer voor externe werk nemers**. Deze inzichten helpen u bij het maken van betere ervaringen voor externe werk nemers en het verminderen van de belasting van uw infra structuur. De inzichten in deze release zijn voornamelijk gericht op VPN:

- **VPN-grens groepen definiëren**
- **VPN-verbonden clients configureren om de voor keur te geven aan cloud-gebaseerde inhouds bronnen**
- **Peer-to-peer delen van inhoud uitschakelen voor door VPN verbonden clients**

Zie [Management Insights](../../servers/manage/management-insights.md)voor meer informatie.

### <a name="improved-support-for-windows-virtual-desktop"></a>Verbeterde ondersteuning voor virtueel bureau blad van Windows

<!--6527576-->

Het **Windows 10 Enter prise-platform voor meerdere sessies** is beschikbaar in de lijst met ondersteunde versies van besturings systemen op objecten met vereiste regels of toepasings lijsten.

Zie [ondersteunde versies van besturings systemen voor clients en apparaten](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)voor meer informatie over de ondersteuning van Configuration Manager voor het virtuele bureau blad van Windows.

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a>Intranet-clients kunnen een CMG-software-update punt gebruiken
<!--7102873-->
Intranet-clients hebben nu toegang tot een CMG-software-update punt wanneer het wordt toegewezen aan een grens groep. Zie [grens groepen configureren](../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup)voor meer informatie.

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Cloud-gekoppeld beheer

### <a name="use-the-company-portal-app-on-co-managed-devices"></a>Gebruik de bedrijfsportal-app op gezamenlijk beheerde apparaten

<!--CMADO-3601237,INADO-4297660-->

De Bedrijfsportal is nu de platformoverschrijdende app Portal-ervaring voor micro soft Endpoint Manager. Door gezamenlijk beheerde apparaten te configureren om ook gebruik te maken van de Bedrijfsportal, kunt u op alle apparaten een consistente gebruikers ervaring bieden.

Zie [De bedrijfsportal-app configureren op co-beheerde apparaten](../../../comanage/company-portal.md) voor meer informatie.

### <a name="use-microsoft-azure-china-21vianet-for-co-management"></a>Gebruik Microsoft Azure China 21Vianet voor co-beheer
<!--7133238-->
U kunt nu de Azure China-Cloud als uw Azure-omgeving selecteren wanneer u co-beheer inschakelt. Zie [co-beheer inschakelen](../../../comanage/how-to-enable.md)voor meer informatie.

### <a name="notification-for-azure-ad-app-secret-key-expiration"></a>Melding voor het verlopen van geheime sleutels van Azure AD-apps

<!--6386392-->

Als u Azure-Services configureert om uw site te koppelen aan de Cloud, worden in de Configuration Manager-console nu meldingen weer gegeven voor de volgende omstandigheden:

- Een of meer geheime sleutels van de Azure AD-App verlopen binnenkort
- Een of meer geheime sleutels van Azure AD-app zijn verlopen

Zie [geheime sleutel vernieuwen](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew)voor meer informatie.

### <a name="desktop-analytics"></a>Desktop Analytics

Zie [what's New in Desktop Analytics](../../../desktop-analytics/whats-new.md)(Engelstalig) voor meer informatie over de maandelijkse wijzigingen in de Cloud service van Desktop Analytics.

#### <a name="change-to-diagnostic-data-labels"></a>Wijzigen in labels voor diagnostische gegevens

<!-- 7363467 -->

Deze instellingen hebben nieuwe labels voor het verbeteren van de vereisten voor het bureau blad Analytics voor diagnostische gegevens van Windows:

| Versie 2006 en hoger | Versie 2002 en lager |
|---------|---------|
| Vereist | Basic |
| Optioneel (beperkt) | Verbeterd (beperkt) |
| N.v.t. | Verbeterd |
| Optioneel | Volledig |

Als u eerder apparaten op het niveau **verbeterd** hebt geconfigureerd, worden deze teruggezet naar **optioneel (beperkt)** wanneer u een upgrade uitvoert naar versie 2006. Ze verzenden minder gegevens naar micro soft. Deze wijziging is niet van invloed op wat u ziet in Desktop Analytics.

Zie voor meer informatie [delen van gegevens inschakelen voor desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Real-time beheer

### <a name="improvements-to-cmpivot"></a>Verbeteringen in CMPivot
<!--6518631-->
De volgende verbeteringen zijn aangebracht in CMPivot:

- CMPivot van de-console en CMPivot zelfstandige zijn geconvergeerd
- CMPivot uitvoeren vanaf een afzonderlijk apparaat of meerdere apparaten zonder een verzameling te selecteren of te maken
- Vanuit CMPivot-query resultaten kunt u een afzonderlijk apparaat of meerdere apparaten selecteren en vervolgens een afzonderlijk CMPivot-exemplaar starten dat is geselecteerd in uw selectie.

Zie [CMPivot vanaf versie 2006](../../servers/manage/cmpivot-changes.md#bkmk_2006)voor meer informatie.

## <a name="client-management"></a><a name="bkmk_client"></a> Client beheer

### <a name="install-and-upgrade-the-client-on-a-metered-connection"></a>De client installeren en upgraden op een verbinding met een Data limiet

<!--6976145-->

Als het apparaat eerder was verbonden met een netwerk met data limiet, zouden nieuwe clients niet kunnen installeren. Bestaande clients zijn alleen bijgewerkt als u alle client communicatie hebt toegestaan. Voor apparaten die vaak worden zwerven op een netwerk met data limiet, zouden ze onbeheerd of op een oudere client versie worden gebruikt. Vanaf deze release kunt u de client installeren en upgraden wanneer u de client **communicatie instelt op Internet verbindingen** met een Data limiet op **toestaan** of **beperken**. Met deze instelling kunt u de client in staat stellen om op de hoogte te blijven, maar wel de client communicatie te beheren op een netwerk met data limiet.

Voor het definiëren van het gedrag voor een nieuwe client installatie, is er een nieuwe ccmsetup-para meter **/AllowMetered**. Wanneer u client communicatie toestaat op een netwerk met data limiet voor ccmsetup, wordt de inhoud gedownload, geregistreerd bij de site en wordt het eerste beleid gedownload. Alle verdere client communicatie volgt de configuratie van de client instelling uit dat beleid.

Raadpleeg voor meer informatie de volgende artikelen:

- [Clientinstellingen](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [Over para meters en eigenschappen van client installatie](../../clients/deploy/about-client-installation-properties.md#allowmetered)

### <a name="improvements-to-managing-device-restarts"></a>Verbeteringen voor het beheren van het opnieuw opstarten van apparaten

<!--3601213-->

Configuration Manager biedt veel opties voor het beheren van het opnieuw opstarten van apparaten en het opnieuw starten van meldingen. U kunt nu een client instelling configureren om te voor komen dat apparaten automatisch opnieuw worden gestart wanneer een implementatie deze vereist. Deze instelling geeft u meer controle over unieke situaties. Standaard kan de client instelling **Configuration Manager geforceerd dat het opnieuw opstarten van een apparaat** wordt ingeschakeld, Configuration Manager zodat de apparaten nog steeds opnieuw kunnen worden opgestart. Deze instelling is alleen van toepassing op toepassingen, software-updates en pakket implementaties waarvoor opnieuw moet worden opgestart.

Zie meldingen voor het [opnieuw opstarten van apparaten](../../clients/deploy/device-restart-notifications.md)voor meer informatie.

## <a name="application-management"></a><a name="bkmk_app"></a> Toepassings beheer

### <a name="improvements-to-available-apps-via-cmg"></a>Verbeteringen in beschik bare apps via CMG

<!--6935376-->
Deze release corrigeert een probleem met de verificatie van software Center en Azure Active Directory (Azure AD). Voor een client die is gedetecteerd als op het intranet maar wel communiceert via de Cloud Management Gateway (CMG), gebruikt voorheen Software Center Windows-verificatie. Als er is geprobeerd de lijst met door gebruikers beschik bare apps op te halen, mislukt dit. Er wordt nu gebruikgemaakt van Azure Active Directory-identiteit (Azure AD) voor apparaten die zijn gekoppeld aan Azure AD. Deze apparaten kunnen deel uitmaken van de Cloud of hybride lid zijn.

Zie voor meer informatie [gebruikers beschik bare Apps implementeren](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications).

### <a name="microsoft-365-apps-for-enterprise"></a>Microsoft 365-apps voor ondernemingen
<!--6298093-->
Office 365 ProPlus is gewijzigd in Microsoft 365 apps voor ondernemingen op 21 april 2020. Vanaf versie 2006 zijn de volgende wijzigingen aangebracht:

- De Configuration Manager-console is bijgewerkt met de nieuwe naam.
  - Deze wijziging omvat ook update kanaal namen voor Microsoft 365-apps.
- Er is een banner melding toegevoegd aan de-console om u te informeren of een of meer regels voor automatische implementatie verouderd kanaal namen hebben in de **titel** criteria voor updates van Microsoft 365-apps.

Zie [Microsoft 365 apps-kanaal namen](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) en [Microsoft 365 apps Readiness dash board](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash)voor meer informatie.

## <a name="os-deployment"></a><a name="bkmk_osd"></a> Implementatie van besturings systeem

### <a name="task-sequence-media-support-for-cloud-based-content"></a>Ondersteuning voor taken reeks media voor Cloud inhoud

<!--6209223-->

Taken reeks media kunnen nu inhoud op basis van de cloud downloaden. U kunt bijvoorbeeld een USB-sleutel naar een gebruiker op een extern kantoor verzenden om de installatie kopie van het apparaat te versleutelen. Of een kantoor met een lokale PXE-server, maar u wilt dat apparaten zo veel mogelijk Cloud Services priori teren. In plaats van het WAN verder te belasten om grote implementatie-inhoud voor het besturings systeem te downloaden, kunnen opstart media en PXE-implementaties nu inhoud ophalen van Cloud bronnen. Bijvoorbeeld een CMG (Cloud Management Gateway) waarmee u inhoud kunt delen.

> [!NOTE]
> Het apparaat heeft nog steeds een intranet verbinding met het beheer punt nodig.

Zie [opstart bare media gebruiken om Windows via het netwerk te implementeren](../../../osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content)voor meer informatie.

### <a name="improvements-to-task-sequences-via-cmg"></a>Verbeteringen in taken reeksen via CMG

Deze release bevat de volgende verbeteringen voor het implementeren van taken reeksen op apparaten die communiceren via een CMG (Cloud Management Gateway):

- Ondersteuning voor besturingssysteem implementatie<!--6997525-->: Met een taken reeks die een installatie kopie gebruikt om een besturings systeem te implementeren, kunt u deze implementeren op een apparaat dat communiceert via CMG. De gebruiker moet de taken reeks starten vanuit software Center. Zie [plan for CMG-specificaties](../../clients/manage/cmg/plan-cloud-management-gateway.md#specifications)voor meer informatie.

- Deze release corrigeert de twee [bekende problemen](../../servers/deploy/install/release-notes.md#task-sequences-cant-run-over-cmg) met Configuration Manager huidige versie 2002 van de branch.<!-- 6983320 --> U kunt nu een taken reeks uitvoeren op een apparaat dat via CMG communiceert in de volgende omstandigheden:

  - Een werk groep-apparaat dat u registreert met een [massa registratie token](../../clients/deploy/deploy-clients-cmg-token.md)

  - U configureert de site voor [verbeterde http](../hierarchy/enhanced-http.md) en het beheer punt is http

### <a name="improvements-to-bitlocker-task-sequence-steps"></a>Verbeteringen in de taken reeks stappen van BitLocker

<!--6995601-->

U kunt nu de schijf versleutelings modus opgeven in de taken reeks stappen **BitLocker inschakelen** en **BitLocker vooraf inrichten** . Standaard blijven de standaard versleutelings methode voor de versie van het besturings systeem worden gebruikt.

De stap **BitLocker inschakelen** bevat nu ook een instelling om **deze stap over te slaan voor computers die geen TPM hebben of wanneer TPM niet is ingeschakeld**. Wanneer u deze instelling inschakelt, registreert de stap een fout op een apparaat zonder een TPM of een TPM die niet wordt geïnitialiseerd, en wordt de taken reeks voortgezet. Met deze instelling kunt u het gedrag van taken reeksen eenvoudiger beheren op apparaten die BitLocker niet volledig ondersteunen.

Zie [taken reeks stappen](../../../osd/understand/task-sequence-steps.md)voor meer informatie.

### <a name="management-insight-rules-for-os-deployment"></a>Beheer Insight-regels voor implementatie van besturings systemen

<!--6982275-->

Wanneer de grootte van het taken reeks beleid groter is dan 32 MB, kan de client het grote beleid niet verwerken. De client kan de taken reeks implementatie vervolgens niet uitvoeren. Deze release bevat de volgende beheer inzichten om u te helpen bij het beheren van de beleids grootte van taken reeksen:

- **Grote taken reeksen kunnen bijdragen aan het overschrijden van de maximale beleids grootte**

- **De totale beleids grootte voor taken reeksen overschrijdt de limiet voor het beleid**

> [!TIP]
> Deze regels bevinden zich in een nieuwe groep voor de **implementatie van besturings systemen**. De bestaande regel voor **ongebruikte opstart installatie kopieën** bevindt zich nu ook in deze groep.

Zie [Management Insight](../../servers/manage/management-insights.md#operating-system-deployment)(Engelstalig) voor meer informatie.

### <a name="improvements-to-os-deployment"></a>Verbeteringen in de implementatie van het besturings systeem

Deze release bevat de volgende aanvullende verbeteringen voor de implementatie van het besturings systeem:

- Gebruik een taken reeks variabele om het doel van de stap [schijf Format teren en partitioneren](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) op te geven. Deze optie nieuwe variabele ondersteunt complexere taken reeksen met dynamische gedragingen. Een aangepast script kan bijvoorbeeld de schijf detecteren en de variabele instellen op basis van het hardwaretype. Vervolgens kunt u meerdere exemplaren van deze stap gebruiken om verschillende typen hardware en partities te configureren.<!--6610288-->

- De stap [gereedheids controle](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness) bevat nu een controle om te bepalen of het apparaat gebruikmaakt van UEFI. Het bevat ook een nieuwe alleen-lezen taken reeks variabele, **_TS_CRUEFI**.<!--6452769-->

- Als u het [venster voortgang van taken reeks](../../../osd/understand/user-experience.md#task-sequence-progress) inschakelt om meer gedetailleerde voortgangs gegevens weer te geven, worden de stappen in een uitgeschakelde groep nu niet meegeteld. Met deze wijziging kunt u de voortgang van de schatting nauw keuriger maken.<!--6448412-->

- Tijdens een taken reeks om een apparaat bij te werken naar Windows 10, wordt een opdracht prompt venster geopend tijdens een van de laatste Windows-configuratie fasen. Het venster bevindt zich boven op de Windows out-of-Box Experience (OOBE) en gebruikers kunnen hiermee communiceren om het upgrade proces te verstoren. De scripts SetupCompleteTemplate. cmd en SetupRollbackTemplate. cmd van Configuration Manager bevatten nu een wijziging om dit opdracht prompt venster te verbergen.<!--2837795-->

- Sommige klanten bouwen aangepaste taken reeks interfaces met behulp van de methode **IProgressUI:: ShowMessage** , maar er wordt geen waarde geretourneerd voor het antwoord van de gebruiker. Deze release voegt de methode [IProgressUI:: ShowMessageEx](../../../develop/reference/core/clients/client-classes/iprogressui--showmessageex-method.md) toe. Deze nieuwe methode is vergelijkbaar met de bestaande methode, maar bevat ook een nieuwe integer-resultaat variabele, **pResult**.<!--6448458-->

## <a name="protection"></a>Protection

### <a name="cmg-support-for-endpoint-protection-policies"></a>CMG-ondersteuning voor Endpoint Protection-beleid

<!--4773948-->

Terwijl de Cloud beheer gateway (CMG) een ondersteund Endpoint Protection-beleid heeft, hebben apparaten die toegang nodig hebben tot on-premises domein controllers. Vanaf deze release kunnen clients die via een CMG communiceren, direct Endpoint Protection-beleids regels Toep assen zonder een actieve verbinding met Active Directory.

Zie [CMG-ondersteuning voor Configuration Manager-functies](../../clients/manage/cmg/plan-cloud-management-gateway.md#support-for-configuration-manager-features)voor meer informatie.

### <a name="bitlocker-management-support-for-hierarchies"></a>Ondersteuning voor BitLocker-beheer voor hiërarchieën

<!-- 5925693 -->

U kunt nu de BitLocker Self-Service Portal en de beheer-en bewakings website installeren op de centrale beheer site.

Zie [BitLocker-portals instellen](../../../protect/deploy-use/bitlocker/setup-websites.md)voor meer informatie.

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-console

### <a name="community-hub-and-github"></a>Community-hub en GitHub
<!--3555935, 3555936, deep link included 4224406-->

*(Voor het eerst geïntroduceerd in juni 2020)*

De IT-beheerder heeft een schat aan kennis ontwikkeld over de jaren. In plaats van items zoals scripts en rapporten helemaal opnieuw te hoeven maken, hebben we een Configuration Manager **Community-hub** gemaakt waar u met elkaar kunt delen. Door gebruik te maken van anderen, kunt u uren werk besparen. De Community-hub bevordert creativiteit door te bouwen op het werk van anderen en andere mensen op uw bedrijf te bouwen. GitHub heeft al branchespecifieke processen en hulpprogram ma's die zijn ontworpen voor delen. De Community-hub maakt nu gebruik van deze hulpprogram ma's rechtstreeks in de Configuration Manager-console als basis onderdelen voor het aansturen van deze nieuwe community. Voor de eerste release wordt de inhoud die beschikbaar is in de Community hub alleen geüpload door micro soft. 

Zie [Community hub en github](../../servers/manage/community-hub.md)voor meer informatie.

### <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> Directe koppelingen naar Community-hub-items
<!--4224406-->
U kunt eenvoudig navigeren naar en verwijzen naar items in het knoop punt van de Configuration Manager console-hub met een directe koppeling. Zie [directe koppelingen naar Community-hub-items](../../servers/manage/community-hub.md#bkmk_deeplink)voor meer informatie.

### <a name="notifications-from-microsoft"></a>Meldingen van micro soft
<!--3953121-->
U kunt nu kiezen voor het ontvangen van meldingen van micro soft in de Configuration Manager-console. Met deze meldingen kunt u op de hoogte blijven van nieuwe of bijgewerkte functies, wijzigingen in Configuration Manager en gekoppelde services, en problemen waarvoor actie moet worden doorgevoerd.

Zie [een site configureren voor het ontvangen van berichten van micro soft](../../servers/manage/admin-console-notifications.md#bkmk_msft)voor meer informatie.

### <a name="power-bi-sample-reports"></a>Voorbeeld rapporten Power BI
<!--5679791-->

*(Voor het eerst geïntroduceerd in juni 2020)*

Wanneer u Power BI Report Server integreert met Configuration Manager-rapportage, zijn er voorbeeld Power BI rapporten beschikbaar. Down load en installeer de volgende voorbeeld rapporten:

- Status van software-Updatenaleving
- Implementatie status van software-updates

Zie [voorbeeld rapporten van Power bi installeren](../../servers/manage/powerbi-sample-reports.md)voor meer informatie.

<!-- Unused sections in this release:
## Reporting
## <a name="bkmk_userxp"></a> User experience
## <a name="bkmk_sum"></a> Software updates
## Office management
## <a name="bkmk_content"></a> Content management
## <a name="bkmk_comgmt"></a> Co-management
-->

## <a name="deprecated-operating-systems"></a><a name="bkmk_deprecated"></a> Afgeschafte besturings systemen

Meer informatie over ondersteunings wijzigingen voordat ze worden geïmplementeerd in [verwijderde en afgeschafte items](deprecated/removed-and-deprecated.md).

Zoals het eerst wordt aangekondigd in versie 1906, daalt versie 2006 geen ondersteuning voor de volgende client besturingssysteem versies:  

- Windows CE 7,0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise

## <a name="other-updates"></a>Andere Updates

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

Zie [release opmerkingen voor Power shell versie 2006](/powershell/sccm/2006-release-notes?view=sccm-ps)voor meer informatie over wijzigingen in de Windows Power shell-cmdlets voor Configuration Manager.

Zie [release opmerkingen voor de beheer service](../../../develop/adminservice/release-notes.md#bkmk_2006)voor meer informatie over wijzigingen in de beheer service rest API.

Afgezien van nieuwe functies bevat deze release ook aanvullende wijzigingen, zoals oplossingen voor problemen. Zie [overzicht van wijzigingen in Configuration Manager current branch, versie 2006](https://support.microsoft.com/help/4578830)voor meer informatie.

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Volgende stappen

<!-- At this time, version 2006 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring). -->

Vanaf 31 augustus 2020 is versie 2006 wereld wijd beschikbaar voor alle klanten die moeten worden geïnstalleerd.

Wanneer u klaar bent om deze versie te installeren, raadpleegt u [updates voor Configuration Manager](../../servers/manage/updates.md) en [controle lijst voor het installeren van update 2006](../../servers/manage/checklist-for-installing-update-2006.md).

> [!TIP]
> Als u een nieuwe site wilt installeren, gebruikt u een basislijn versie van Configuration Manager.
>
> Meer informatie over:
>
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)

Zie de opmerkingen bij de [release](../../servers/deploy/install/release-notes.md)voor bekende belang rijke problemen.

Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).

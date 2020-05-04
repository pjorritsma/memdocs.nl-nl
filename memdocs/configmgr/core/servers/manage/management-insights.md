---
title: Beheerinzichten
titleSuffix: Configuration Manager
description: Meer informatie over de Management Insights-functionaliteit die beschikbaar is in de Configuration Manager-console.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9aae1da48deabd0cc339cd25055827caf07354b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713735"
---
# <a name="management-insights-in-configuration-manager"></a>Beheer inzichten in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Beheer inzichten in Configuration Manager bieden informatie over de huidige status van uw omgeving. De informatie is gebaseerd op de analyse van gegevens uit de site database. Inzichten helpt u uw omgeving beter te begrijpen en actie te ondernemen op basis van het inzicht. <!--1353967-->

## <a name="review-management-insights"></a>Beheer inzichten evalueren

Voor het weer geven van de regels heeft uw account de machtiging **lezen** nodig voor het object **site** .

1. Open de Configuration Manager-console.  

2. Ga naar de werk ruimte **beheer** , vouw **beheer inzichten**uit en selecteer **alle inzichten**.  

    > [!Note]  
    > Wanneer u het **Management Insights** -knoop punt selecteert, wordt het [Management Insights-dash board](#bkmk_insights)weer gegeven.  

3. Open de naam van de Management Insights-groep die u wilt controleren. Selecteer **inzichten weer geven** in het lint.  

De volgende vier tabbladen zijn beschikbaar voor beoordeling:

- **Alle regels**: Hiermee geeft u de volledige lijst met regels voor de gekozen beheer Insight-groep.  

- **Volt ooien**: bevat een lijst met regels waarvoor geen actie is vereist.  

- Wordt **uitgevoerd**: geeft regels weer waarbij sommige, maar niet alle, vereisten zijn voltooid.  

- **Actie vereist**: de regels die moeten worden uitgevoerd, worden weer gegeven. Selecteer **meer details** voor het ophalen van specifieke items waarvoor actie is vereist.  

In het deel venster **vereisten** worden de vereiste items vermeld die nodig zijn om de regel uit te voeren.

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Alle regels en vereisten voor de groep Cloud Services

![Beheer inzichten: alle regels en vereisten voor de Cloud Services-groep](./media/Management-insights-all-cloud-rules.png)

Selecteer een regel en selecteer vervolgens **meer details** om de regel details weer te geven.

## <a name="operations"></a>Bewerkingen

De regels voor beheer Insight evalueren hun toepasselijkheid op een wekelijks schema opnieuw. Als u een regel op aanvraag opnieuw wilt evalueren, klikt u met de rechter muisknop op de regel en selecteert u **opnieuw evalueren**.

Het logboek bestand voor management Insight rules is **SMS_DataEngine. log** op de site server.

<!--1357930-->
Met sommige regels kunt u actie ondernemen. Selecteer een regel, selecteer **meer details**en klik vervolgens, indien beschikbaar, op **actie ondernemen**.

Afhankelijk van de regel heeft deze actie een van de volgende gedragingen:  

- Navigeer in de-console automatisch naar het knoop punt waar u verdere actie kunt ondernemen. Als door de Management Insight bijvoorbeeld wordt geadviseerd om een client instelling te wijzigen, gaat u naar het knoop punt client instellingen om actie te ondernemen. Ga vervolgens verder met het wijzigen van het standaard-of een aangepast client instellingen object.  

- Navigeer naar een gefilterde weer gave op basis van een query. Als u bijvoorbeeld actie onderneemt voor de lege verzamelingen regel, worden alleen deze verzamelingen weer gegeven in de lijst met verzamelingen. Onderneem vervolgens verdere actie, zoals het verwijderen van een verzameling of het wijzigen van de lidmaatschaps regels.  

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a>Management Insights-dash board

<!--1357979-->

Het knoop punt **Management Insights** bevat een grafisch dash board. Dit dash board geeft een overzicht van de statussen van de regel, waardoor u uw voortgang gemakkelijker kunt weer geven.

Gebruik de volgende filters boven aan het dash board om de weer gave te verfijnen:

- Voltooide items weer geven
- Optioneel
- Aanbevolen
- Kritiek

Het dash board bevat de volgende tegels:  

- **Management Insights-index**: houdt de algehele voortgang bij van beheer Insights-regels. De index is een gewogen gemiddelde. Kritieke regels zijn het meest. Deze index geeft het minste gewicht aan optionele regels.  

- **Beheer Insights-groepen**: Hiermee wordt het percentage van de regels in elke groep weer gegeven, waarbij de filters worden gehonoreerd. Selecteer een groep om in te zoomen op de specifieke regels in deze groep.  

- **Prioriteit van management Insights**: geeft het percentage van de regels op prioriteit weer, waarbij de filters worden nageleefd.  

- **Alle inzichten**: een tabel met inzichten, waaronder prioriteit en status. Gebruik het **filter** veld boven aan de tabel om teken reeksen in een van de beschik bare kolommen te vergelijken. Het dash board sorteert de tabel in de volgende volg orde:

  - Status: actie vereist, voltooid, onbekend  
  - Prioriteit: kritiek, aanbevolen, optioneel  
  - Laatst gewijzigd: oudere datums bovenaan  

![Scherm opname van het management Insights-dash board](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>Groepen en regels

Regels zijn ingedeeld in de volgende beheer Insight-groepen:

- [Toepassingen](#applications)
- [Cloud Services](#cloud-services)
- [Verzamelingen](#collections)
- [Configuration Manager beoordeling](#configuration-manager-assessment)
- [Proactief onderhoud](#proactive-maintenance)
- [Beveiliging](#security)
- [Vereenvoudigd beheer](#simplified-management)
- [Software Center](#software-center)
- [Windows 10](#windows-10)

### <a name="applications"></a>Toepassingen

Inzichten voor uw toepassings beheer.

- **Toepassingen zonder implementaties**: hier wordt een lijst weer gegeven met de toepassingen in uw omgeving die geen actieve implementaties hebben. Met deze regel kunt u ongebruikte toepassingen vinden en verwijderen om de lijst met toepassingen die in de-console worden weer gegeven, te vereenvoudigen. Zie [toepassingen implementeren](../../../apps/deploy-use/deploy-applications.md)voor meer informatie.  

### <a name="cloud-services"></a>Cloud services

Helpt u te integreren met veel Cloud Services, waarmee u uw apparaten modern kunt beheren.

- **Gereedheid voor co-beheer beoordelen**: helpt u inzicht te krijgen in de stappen die nodig zijn om co-beheer in te scha kelen. Deze regel heeft vereisten. Zie [overzicht van co-beheer](../../../comanage/overview.md)voor meer informatie.  

- **Apparaten die niet zijn geüpload naar Azure AD**: vanaf versie 2002 geeft deze regel een lijst van apparaten die niet zijn geüpload naar Azure ad omdat de site niet goed is geconfigureerd voor HTTPS.<!--6268489--> [Verbeterde http](../../plan-design/hierarchy/enhanced-http.md)configureren of ten minste één beheer punt inschakelen voor HTTPS. Als u de site voor HTTPS-communicatie al hebt geconfigureerd, wordt deze regel niet weer gegeven.

- **Azure-Services configureren voor gebruik met Configuration Manager**: deze regel helpt u bij het voorbereiden van Configuration Manager naar Azure AD, waarmee clients kunnen verifiëren met de site met behulp van Azure AD. Zie [Azure-Services configureren](../deploy/configure/azure-services-wizard.md)voor meer informatie.  

- **Apparaten kunnen hybride Azure Active Directory lid zijn**: met Azure AD toegevoegde apparaten kunnen gebruikers zich aanmelden met hun domein referenties, terwijl apparaten voldoen aan de beveiligings-en nalevings normen van de organisatie. Zie [ontwerp overwegingen voor Azure AD Hybrid Identity](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)voor meer informatie.  

- **Sites die niet over de juiste HTTPS-configuratie beschikken**: vanaf versie 2002 worden in deze regel sites in uw hiërarchie weer gegeven die niet juist zijn geconfigureerd voor HTTPS. Met deze configuratie wordt voor komen dat de site de resultaten van het [verzamelings lidmaatschap synchroniseert met Azure Active Directory-groepen (Azure AD)](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Dit kan ertoe leiden dat Azure AD Sync niet alle apparaten uploadt. Het beheer van deze clients werkt mogelijk niet goed.<!--6268489--> [Verbeterde http](../../plan-design/hierarchy/enhanced-http.md)configureren of ten minste één beheer punt inschakelen voor HTTPS. Als u de site voor HTTPS-communicatie al hebt geconfigureerd, wordt deze regel niet weer gegeven.

- **Clients bijwerken naar de nieuwste versie van Windows 10**: Windows 10, versie 1709 of hoger verbetert de computer ervaring van uw gebruikers en bemodernt deze. Zie [belang rijke artikelen over het aannemen van Windows als een service](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service)voor meer informatie.  

### <a name="collections"></a>Verzamelingen

Inzichten die het beheer vereenvoudigen door verzamelingen te verwijderen en opnieuw te configureren.

- **Lege verzamelingen**: bevat verzamelingen in uw omgeving die geen leden hebben. Zie [verzamelingen beheren](../../clients/manage/collections/manage-collections.md)voor meer informatie.  

Vanaf versie 1902 zijn er nieuwe regels met aanbevelingen voor het beheren van verzamelingen.<!--3555752--> Gebruik deze inzichten om het beheer te vereenvoudigen en de prestaties te verbeteren:

- **Verzamelingen zonder query regels en zonder rechtstreekse leden**: als u de lijst met verzamelingen in uw hiërarchie wilt vereenvoudigen, verwijdert u deze verzamelingen.  

- **Verzamelingen met dezelfde begin tijd voor opnieuw evalueren**: deze verzamelingen hebben dezelfde herevaluatietijd als andere verzamelingen. Wijzig de tijd van de nieuwe evaluatie zodat deze geen conflict veroorzaakt.  

- **Verzamelingen met een query tijd van meer dan twee seconden**: Controleer de query regels voor deze verzameling. Overweeg om de verzameling te wijzigen of te verwijderen.

- De volgende regels bevatten configuraties die mogelijk onnodig belasting op de site veroorzaken. Bekijk deze verzamelingen en verwijder deze of schakel de regel evaluatie uit:  

  - **Verzamelingen zonder query regels en incrementele updates ingeschakeld**  

  - **Verzamelingen zonder query regels en ingeschakeld voor geplande of incrementele evaluatie**  

  - **Verzamelingen zonder query regels en volledige evaluatie plannen geselecteerd**  

### <a name="configuration-manager-assessment"></a>Configuration Manager beoordeling

<!--3607758-->

Vanaf versie 2002 is deze groep een beleefdheids van micro soft premier field engineering. Deze regels zijn een voor beeld van de vele meer controles die micro soft Premier biedt in de [Services hub](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments).

- **Active Directory detectie van beveiligings groepen is zo geconfigureerd dat ze te vaak worden uitgevoerd**: u hoeft de detectie van Active Directory beveiligings groep doorgaans niet te configureren om vaker dan om de drie uur te doen. Een frequentere configuratie kan een negatieve invloed hebben op de prestaties van Active Directory, het netwerk en Configuration Manager. Schakel incrementele synchronisatie in in plaats van een volledige synchronisatie planning. Zie voor meer informatie [Active Directory groeps detectie](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).

- **Active Directory systeem detectie is zo geconfigureerd dat het te vaak wordt uitgevoerd**: u hoeft Active Directory systeem detectie doorgaans niet meer dan om de drie uur te configureren. Een frequentere configuratie kan een negatieve invloed hebben op de prestaties van Active Directory, het netwerk en Configuration Manager. Schakel incrementele synchronisatie in in plaats van een volledige synchronisatie planning. Zie [Active Directory-systeem detectie](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem)voor meer informatie.

- **Active Directory gebruikers detectie is zo geconfigureerd dat ze te vaak worden uitgevoerd**: u hoeft niet in te stellen Active Directory gebruikers detectie vaker dan om de drie uur vaker optreedt. Een frequentere configuratie kan een negatieve invloed hebben op de prestaties van Active Directory, het netwerk en Configuration Manager. Schakel incrementele synchronisatie in in plaats van een volledige synchronisatie planning. Zie [Active Directory gebruikers detectie](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser)voor meer informatie.

- **Verzamelingen beperkt tot alle systemen of alle gebruikers**: Bekijk verzamelingen die gebruikmaken van de verzamelingen **alle systemen** of **alle gebruikers** als beperkende verzameling. Met Configuration Manager wordt het lidmaatschap van deze standaard verzamelingen bijgewerkt met gegevens van de Active Directory detectie methoden. Deze gegevens zijn mogelijk geen geldige informatie voor Configuration Manager-clients.

- **Heartbeat-detectie is uitgeschakeld**: voor heartbeat-detectie moet de Configuration Manager-client op apparaten worden geïnstalleerd. Het is de enige detectie methode die clients starten. Alle andere methoden vinden plaats op site servers. Heartbeat-detectie is essentieel om de status van client activiteiten actueel te laten blijven. Het zorgt ervoor dat de site de resource records uit de site database niet per ongeluk heeft geleeftijd. Zie [heartbeat-detectie](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)voor meer informatie.

- **Langdurige query's voor het uitvoeren van een verzameling ingeschakeld voor incrementele updates**: verzamelingen met een laatste incrementele vernieuwings tijd van meer dan 30 seconden site server-en database bronnen gebruiken die mogelijk van invloed kunnen zijn op de algehele Configuration Manager prestaties. Zie [Aanbevolen procedures voor verzamelingen](../../clients/manage/collections/best-practices-for-collections.md)voor meer informatie.

- **Verminder het aantal toepassingen en pakketten op distributie punten**: micro soft officieel ondersteunt een gecombineerd totaal van maxi maal 10.000 pakketten en toepassingen op een distributie punt. Een overschrijding van dit totaal kan leiden tot operationele problemen. Zie [grootte en schaal getallen-distributie punt](../../plan-design/configs/size-and-scale-numbers.md#distribution-point)voor meer informatie.

- Problemen met de installatie van de **secundaire site**: de installatie status van sommige secundaire sites **in behandeling** of **mislukt**. Deze statussen betekenen dat u de installatie hebt gestart, maar niet is voltooid. Totdat de installatie van de secundaire site is voltooid, communiceren clients mogelijk niet goed met de primaire site. Controleer de werk ruimte **bewaking** en voer de installatie opnieuw uit. Zie [de installatie van een mislukte update opnieuw uitvoeren](install-in-console-updates.md#bkmk_retry)voor meer informatie.

- **Alle sites bijwerken naar dezelfde versie**: gebruik dezelfde versie van Configuration Manager in een hiërarchie. Deze configuratie zorgt ervoor dat alle sites dezelfde functionaliteit bieden. Sites van verschillende versies in dezelfde hiërarchie introduceren interoperabiliteits scenario's. Latere versies van Configuration Manager bevatten nieuwe functies en oplossingen voor bekende problemen. Zie [interoperabiliteit tussen verschillende versies](../../plan-design/hierarchy/interoperability-between-different-versions.md)voor meer informatie.

Zie [herstel stappen voor Configuration Manager management Insights](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr)voor meer informatie over deze regels.

> [!TIP]
> Als u al een klant van micro soft Unified of micro soft premier bent, meldt u zich aan bij de [Services hub](https://serviceshub.microsoft.com/assessments/) voor aanvullende evaluaties op aanvraag.
>
> Zie [oplossingen voor ondersteuning](https://www.microsoft.com/enterprise/services/support)voor meer informatie over micro soft-Services.

### <a name="proactive-maintenance"></a>Proactief onderhoud

<!--1352184-->
De regels in deze groep markeren mogelijke configuratie problemen om te voor komen dat Configuration Manager objecten worden bewaard.

- **Grens groepen zonder toegewezen site systemen**: als u geen site systemen hebt toegewezen, kunnen grens groepen alleen worden gebruikt voor site toewijzing. Zie [grens groepen configureren](../deploy/configure/boundary-groups.md)voor meer informatie.  

- **Grens groepen zonder leden**: grens groepen zijn niet van toepassing op site toewijzing of het opzoeken van inhoud als ze geen leden hebben. Zie [grens groepen configureren](../deploy/configure/boundary-groups.md)voor meer informatie.  

- **Distributie punten die geen inhoud leveren aan clients**: distributie punten die in de afgelopen 30 dagen geen inhoud hebben aangeboden aan clients. Deze gegevens zijn gebaseerd op rapporten van clients van hun download geschiedenis. Zie [distributie punten installeren en configureren](../deploy/configure/install-and-configure-distribution-points.md)voor meer informatie.  

- **WSUS-opschoning inschakelen**: controleert of u de optie voor het uitvoeren van WSUS-opschoning hebt ingeschakeld op de eigenschappen van het onderdeel Software-update punt. Met deze optie kunt u de prestaties van WSUS verbeteren. Zie [Software update Maintenance](../../../sum/deploy-use/software-updates-maintenance.md)(Engelstalig) voor meer informatie.  

- **Ongebruikte opstart installatie kopieën**: er wordt niet naar opstart installatie kopieën verwezen voor het opstarten van de PXE-opstart bewerking of de taken reeks Zie [opstart installatie kopieën beheren](../../../osd/get-started/manage-boot-images.md)voor meer informatie.  

- **Ongebruikte configuratie-items**: configuratie-items die geen deel uitmaken van een configuratie basislijn en ouder zijn dan 30 dagen. Zie [configuratie basislijnen maken](../../../compliance/deploy-use/create-configuration-baselines.md)voor meer informatie.  

- **Peer-cache bronnen upgraden naar de nieuwste versie van de Configuration Manager-client**: Identificeer clients die fungeren als peer-cache bron, maar die niet zijn bijgewerkt van een pre-1806-client versie. Pre-1806-clients kunnen niet worden gebruikt als peer-cache bron voor clients waarop versie 1806 of hoger wordt uitgevoerd. Selecteer **actie ondernemen** om een weer gave apparaat te openen waarin de lijst met clients wordt weer gegeven.<!--1358008-->  

### <a name="security"></a>Beveiliging

Inzichten voor het verbeteren van de beveiliging van uw infra structuur en apparaten.

- **NTLM-terugval is ingeschakeld**:<!--4572953--> Met ingang van versie 1906 detecteert deze regel of u de terugval methode voor minder veilige NTLM-verificatie hebt ingeschakeld voor de site. Wanneer u de client push methode voor het installeren van de Configuration Manager-client gebruikt, kan voor de site wederzijdse verificatie van Kerberos vereist zijn. Deze verbetering helpt bij het beveiligen van de communicatie tussen de server en de client. Zie [clients installeren met client push](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)voor meer informatie.

- **Niet-ondersteunde antimalware-client versies**: meer dan 10% van de clients voert een versie van System Center-Endpoint Protection uit die niet worden ondersteund. Zie [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)voor meer informatie.  

### <a name="simplified-management"></a>Vereenvoudigd beheer

Inzichten waarmee u het dagelijkse beheer van uw omgeving kunt vereenvoudigen.

- **De site verbinden met de micro soft-Cloud voor Configuration Manager-updates**: deze regel zorgt ervoor dat uw Configuration Manager service verbindings punt in de afgelopen zeven dagen verbinding heeft met de micro soft-Cloud. Deze verbinding is het downloaden van inhoud voor regel matige updates. Controleer DMPDownloader. log en hman. log. Zie [vereisten voor Internet toegang](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates)voor meer informatie.

- **Niet-CB-client versies**: een lijst met alle clients waarvan de versies geen CB-build (current branch) zijn. Zie [upgrade-clients](../../clients/manage/upgrade/upgrade-clients.md)voor meer informatie.  

- **Clients bijwerken naar een ondersteunde versie van Windows 10**: vanaf versie 1902 rapporteert deze regel op clients met een versie van Windows 10 die niet meer wordt ondersteund. Het bevat ook clients met een Windows 10-versie die bijna op het einde van de service (drie maanden) ligt.<!--3897268-->  

### <a name="software-center"></a>Software Center

Inzichten voor het beheren van software Center.

- **Gebruikers naar Software Center leiden in plaats van toepassingscatalogus**: controleren of gebruikers in de afgelopen 14 dagen toepassingen hebben geïnstalleerd of aangevraagd in de toepassings catalogus. De primaire functionaliteit van de toepassings catalogus is nu opgenomen in Software Center. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [afgeschafte functies](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)voor meer informatie.  

- **De nieuwe versie van software Center gebruiken**: de vorige versie van software Center wordt niet meer ondersteund. Stel clients in om het nieuwe software Center te gebruiken door de client instelling **Nieuw Software Center** in de groep **computer agent** in te scha kelen. Zie [over client instellingen](../../clients/deploy/about-client-settings.md#use-new-software-center)voor meer informatie.  

### <a name="software-updates"></a>Software-updates

- **Client instellingen zijn niet geconfigureerd om clients toe te staan Delta-inhoud te downloaden**: sommige software-updates die in uw omgeving worden gesynchroniseerd, bevatten Delta-inhoud. De client instelling inschakelen, **clients toestaan om Delta-inhoud te downloaden wanneer deze beschikbaar zijn**. Als u deze instelling niet inschakelt, zal de client onnodig meer inhoud downloaden dan nodig is om deze updates te implementeren. Zie [client instellingen-software-updates](../../clients/deploy/about-client-settings.md#software-updates)voor meer informatie.

- **De product categorie software-updates (Windows 10, versie 1903 en hoger) inschakelen**: er is een nieuwe product categorie voor software-updates voor Windows 10, versie 1903 of hoger. Als u Windows 10-updates synchroniseert en clients met Windows 10, versie 1903 of hoger hebt, selecteert u de product categorie **Windows 10, versie 1903 en hoger** in de eigenschappen van de software-update punt component. Zie voor meer informatie[classificaties en producten configureren om te synchroniseren](../../../sum/get-started/configure-classifications-and-products.md).

### <a name="windows-10"></a>Windows 10

Inzichten met betrekking tot de implementatie en het onderhoud van Windows 10. De Windows 10 Management Insight-groep is alleen beschikbaar wanneer er meer dan de helft van clients Windows 7, Windows 8 of Windows 8,1 wordt uitgevoerd.

- **Windows diagnostische gegevens en commerciële ID-sleutel configureren**: als u gegevens van Desktop Analytics wilt gebruiken, configureert u apparaten met een commerciële id-sleutel en schakelt u het verzamelen van diagnostische gegevens in. Stel Windows 10-apparaten in op het niveau **verbeterd (beperkt)** of hoger. Zie voor meer informatie [delen van gegevens inschakelen voor desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).

#### <a name="windows-10-management-insights-rules"></a>Regels voor Windows 10 Management Insights

![Management Insights-regels voor Windows 10](./media/Windows-10-insights-group.png)

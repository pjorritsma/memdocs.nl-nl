---
title: Beheerinzichten
titleSuffix: Configuration Manager
description: Meer informatie over de Management Insights-functionaliteit die beschikbaar is in de Configuration Manager-console.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: de3c75982e19e6183260a2a5f99f65b9c785d27f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700511"
---
# <a name="management-insights-in-configuration-manager"></a>Beheer inzichten in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Beheer inzichten in Configuration Manager bieden informatie over de huidige status van uw omgeving. De informatie is gebaseerd op de analyse van gegevens uit de site database. Inzichten helpt u uw omgeving beter te begrijpen en actie te ondernemen op basis van het inzicht. <!--1353967-->

## <a name="review-management-insights"></a>Beheer inzichten evalueren

Voor het weer geven van de inzichten heeft uw account de machtiging **lezen** nodig voor het object **site** .

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **beheer inzichten**uit en selecteer **alle inzichten**.

    > [!NOTE]
    > Wanneer u het **Management Insights** -knoop punt selecteert, wordt het [Management Insights-dash board](#bkmk_insights)weer gegeven.

1. Open de naam van de Management Insights-groep die u wilt controleren.

1. Selecteer **inzichten weer geven**in het lint.

De volgende vier tabbladen zijn beschikbaar voor beoordeling:

- **Alle regels**: Hiermee geeft u de volledige lijst met inzichten voor de gekozen groep.

- **Volt ooien**: geeft een overzicht van inzichten waarvoor geen actie is vereist.

- Wordt **uitgevoerd**: toont inzichten waarbij sommige, maar niet alle, vereisten zijn voltooid.

- **Actie vereist**: op dit tabblad ziet u inzichten waarvoor u actie moet ondernemen. Selecteer **meer details** om specifieke items weer te geven waar actie nodig is.

In het deel venster **vereisten** worden de vereiste items vermeld die nodig zijn om het geselecteerde inzicht uit te voeren.

De volgende scherm afbeelding toont bijvoorbeeld een voor beeld van het tabblad **alle regels** voor de groep **Cloud Services** :

:::image type="content" source="media/management-insights-all-cloud-rules.png" alt-text="Management Insights: alle regels en vereisten voor Cloud Services groep":::

Als u de details wilt weer geven, selecteert u een inzicht en selecteert u vervolgens **meer details**.

## <a name="operations"></a>Bewerkingen

De site evalueert de toepasselijkheid van de Management Insights op een wekelijks schema opnieuw. Als u een inzicht hand matig wilt evalueren, klikt u met de rechter muisknop op het inzicht en selecteert u **opnieuw evalueren**.

Het logboek bestand voor management Insights is **SMS_DataEngine. log** op de site server.

<!--1357930-->
Met sommige inzichten kunt u actie ondernemen. Selecteer een inzicht, selecteer **meer details**en klik vervolgens indien beschikbaar op **actie ondernemen**. Afhankelijk van het inzicht heeft deze actie een van de volgende gedragingen:

- Navigeer in de-console automatisch naar het knoop punt waar u verdere actie kunt ondernemen. Als door de Management Insight bijvoorbeeld wordt geadviseerd om een client instelling te wijzigen, gaat u naar het knoop punt **client instellingen** om actie te ondernemen. Ga vervolgens verder met het wijzigen van het standaard-of een aangepast client instellingen object.

- Navigeer naar een gefilterde weer gave op basis van een query. Als u bijvoorbeeld actie onderneemt op de lege verzamelingen inzicht, worden alleen deze verzamelingen weer gegeven in de lijst met verzamelingen. Onderneem vervolgens verdere actie, zoals het verwijderen van een verzameling of het wijzigen van de lidmaatschaps regels.

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> Management Insights-dash board

<!--1357979-->

Selecteer het knoop punt **Management Insights** om een grafisch dash board weer te geven. Dit dash board geeft een overzicht van de inzicht statussen, waardoor u uw voortgang gemakkelijker kunt weer geven.

Gebruik de volgende filters boven aan het dash board om de weer gave te verfijnen:

- Voltooide items weer geven
- Optioneel
- Aanbevolen
- Kritiek

Het dash board bevat de volgende tegels:  

- **Management Insights-index**: houdt de algehele voortgang bij beheer inzichten bij. De index is een gewogen gemiddelde. Essentiële inzichten zijn de meeste. Deze index geeft het minste gewicht voor de optionele inzichten.

- **Beheer Insights-groepen**: Hiermee wordt het percentage inzichten in elke groep weer gegeven, waarbij de filters worden gehonoreerd. Selecteer een groep om in te zoomen op de specifieke inzichten in deze groep.

- **Prioriteit van management Insights**: geeft het percentage inzichten op prioriteit weer, waarmee de filters worden gehonoreerd.

- **Top 10 van toepas bare inzichten regels**: een tabel met inzichten, waaronder prioriteit en status. Gebruik het **filter** veld boven aan de tabel om teken reeksen in een van de beschik bare kolommen te vergelijken. Het dash board sorteert de tabel in de volgende volg orde:

  - Status: actie vereist, voltooid, onbekend  
  - Prioriteit: kritiek, aanbevolen, optioneel  
  - Laatst gewijzigd: oudere datums bovenaan  

:::image type="content" source="media/1357979-management-insights-dashboard.png" alt-text="Scherm opname van het management Insights-dash board" lightbox="media/1357979-management-insights-dashboard.png":::

## <a name="groups-and-insights"></a>Groepen en inzichten

Inzichten zijn ingedeeld in de volgende beheer Insight-groepen:

- [Toepassingen](#applications)
- [Cloud Services](#cloud-services)
- [Verzamelingen](#collections)
- [Configuration Manager beoordeling](#configuration-manager-assessment)
- [Optimaliseren voor externe werk rollen](#optimize-for-remote-workers)
- [Proactief onderhoud](#proactive-maintenance)
- [Beveiliging](#security)
- [Vereenvoudigd beheer](#simplified-management)
- [Software Center](#software-center)
- [Software-updates](#software-updates)
- [Windows 10](#windows-10)

> [!NOTE]
> Uw site mag niet alle volgende groepen en inzichten weer geven. Sommige inzichten worden niet weer gegeven wanneer u de-site al hebt geconfigureerd voor de aanbeveling.

### <a name="applications"></a>Toepassingen

Inzichten voor uw toepassings beheer.

- **Toepassingen zonder implementaties of verwijzingen**: hier wordt een lijst weer gegeven met de toepassingen in uw omgeving die geen actieve implementaties of verwijzingen hebben. Verwijzingen zijn onder andere afhankelijkheden, taken reeksen en virtuele omgevingen. Met deze inzichten kunt u ongebruikte toepassingen vinden en verwijderen om de lijst met toepassingen die in de-console worden weer gegeven, te vereenvoudigen. Zie [toepassingen implementeren](../../../apps/deploy-use/deploy-applications.md)voor meer informatie.<!-- B585E3FF-585F-4CE9-AE2C-648A7CA2F143 -->

### <a name="cloud-services"></a>Cloud services

Helpt u te integreren met veel Cloud Services, waarmee u uw apparaten modern kunt beheren.

- **Gereedheid voor co-beheer beoordelen**: helpt u inzicht te krijgen in de stappen die nodig zijn om co-beheer in te scha kelen. Dit inzicht heeft vereisten. Zie [overzicht van co-beheer](../../../comanage/overview.md)voor meer informatie.<!-- D99F094A-A965-402F-AFE5-EE00CCAF0A12 -->

- **Apparaten die niet zijn geüpload naar Azure AD**: vanaf versie 2002 is dit inzicht een lijst met apparaten die de site nog niet heeft geüpload naar Azure Active Directory (Azure AD) omdat u deze niet hebt geconfigureerd voor HTTPS.<!--6268489--> [Verbeterde http](../../plan-design/hierarchy/enhanced-http.md)configureren of ten minste één beheer punt inschakelen voor HTTPS. Als u de site voor HTTPS-communicatie al hebt geconfigureerd, wordt dit inzicht niet weer gegeven.<!-- 609F03D4-D9B4-4D0D-A67F-9E365F6C0DD0 -->

- **Cloud beheer gateway inschakelen**: de Cloud Management Gateway (CMG) biedt een eenvoudige manier om Configuration Manager-clients te beheren via internet. Door de CMG te implementeren als een Cloud service in Microsoft Azure, kunt u door gaan met het beheren en verwerken van inhoud aan clients die zwerven op internet. Met CMG hebt u geen extra on-premises infra structuur nodig die toegankelijk is via internet. Zie [plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md)voor meer informatie.<!-- 451B9B3A-D86A-4EF1-ACC3-FE6A207886BA -->

- **Apparaten kunnen hybride Azure Active Directory lid zijn**: met Azure AD toegevoegde apparaten kunnen gebruikers zich aanmelden met hun domein referenties en ervoor zorgen dat apparaten voldoen aan de beveiligings-en nalevings normen van de organisatie. Zie [ontwerp overwegingen voor Azure AD Hybrid Identity](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-overview)voor meer informatie.<!-- 6DC6B149-8B48-45E9-B189-F1E12A62D994 -->

- **Sites die niet over de juiste HTTPS-configuratie beschikken**: vanaf versie 2002 is dit inzicht een lijst met sites in uw hiërarchie die niet juist zijn geconfigureerd voor HTTPS. Met deze configuratie wordt voor komen dat de site de resultaten van het [verzamelings lidmaatschap synchroniseert met Azure ad-groepen](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Dit kan ertoe leiden dat Azure AD Sync niet alle apparaten uploadt. Het beheer van deze clients werkt mogelijk niet goed.<!--6268489--> [Verbeterde http](../../plan-design/hierarchy/enhanced-http.md)configureren of ten minste één beheer punt inschakelen voor HTTPS. Als u de site voor HTTPS-communicatie al hebt geconfigureerd, wordt dit inzicht niet weer gegeven.<!-- 73884047-3395-430E-B971-F853806D4349 -->

- **Clients bijwerken naar de nieuwste versie van Windows 10**: Windows 10, versie 1709 of hoger verbetert de computer ervaring van uw gebruikers en bemodernt deze. Zie [belang rijke artikelen over het aannemen van Windows als een service](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service)voor meer informatie.<!-- FD2C7B93-E5C6-4DCB-89AF-9EFCFCD01524 -->

### <a name="collections"></a>Verzamelingen

Inzichten die het beheer vereenvoudigen door verzamelingen te verwijderen en opnieuw te configureren.

- **Lege verzamelingen**: bevat verzamelingen in uw omgeving die geen leden hebben. Zie [verzamelingen beheren](../../clients/manage/collections/manage-collections.md)voor meer informatie.<!-- 4266054A-695D-4BCA-8000-27BD32F7C006 -->

<!--3555752-->
- **Verzamelingen zonder query regels en zonder rechtstreekse leden**: als u de lijst met verzamelingen in uw hiërarchie wilt vereenvoudigen, verwijdert u deze verzamelingen.<!-- 3C234964-B3F3-49EE-AA13-048CD2021924 -->

- **Verzamelingen met dezelfde begin tijd voor opnieuw evalueren**: deze verzamelingen hebben dezelfde herevaluatietijd als andere verzamelingen. Wijzig de tijd van de nieuwe evaluatie zodat deze geen conflict veroorzaakt.<!-- A85B79A6-BA81-404F-8DA4-DD7C87582CCD -->

- **Verzamelingen met een query tijd van meer dan vijf minuten**: Controleer de query regels voor deze verzameling. Overweeg om de verzameling te wijzigen of te verwijderen.<!-- 6AF42536-BDF4-4535-87C1-535AE1B813DA -->

- De volgende inzichten bevatten configuraties die mogelijk onnodig belasting op de site veroorzaken. Bekijk deze verzamelingen en verwijder deze of schakel de evaluatie van de verzamelings regel uit:

  - **Verzamelingen zonder query regels en incrementele updates ingeschakeld**<!-- 6A4845AB-6D2C-4F2A-B7AB-EC77C81FD571 -->

  - **Verzamelingen zonder query regels en zijn ingeschakeld voor elk schema**<!-- 219B9C45-BD02-4E7E-A29D-B66094366200 -->

  - **Verzamelingen zonder query regels en volledige evaluatie plannen geselecteerd**<!-- 8A401207-5A7C-4200-A1DB-990A197458FA -->

### <a name="configuration-manager-assessment"></a>Configuration Manager beoordeling

<!--3607758-->

Vanaf versie 2002 is deze groep een beleefdheids van micro soft premier field engineering. Deze inzichten zijn een voor beeld van de vele meer controles die micro soft Premier biedt in de [Services hub](/services-hub/health/getting_started_with_on_demand_assessments).

- **Active Directory detectie van beveiligings groepen is zo geconfigureerd dat ze te vaak worden uitgevoerd**: u hoeft de detectie van Active Directory beveiligings groep doorgaans niet te configureren om vaker dan om de drie uur te doen. Een frequentere configuratie kan een negatieve invloed hebben op de prestaties van Active Directory, het netwerk en Configuration Manager. Schakel incrementele synchronisatie in in plaats van een volledige synchronisatie planning. Zie voor meer informatie [Active Directory groeps detectie](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).<!-- 4E739B65-AEC9-4B1D-8B36-AC6AC4A72022 -->

- **Active Directory systeem detectie is zo geconfigureerd dat het te vaak wordt uitgevoerd**: u hoeft Active Directory systeem detectie doorgaans niet meer dan om de drie uur te configureren. Een frequentere configuratie kan een negatieve invloed hebben op de prestaties van Active Directory, het netwerk en Configuration Manager. Schakel incrementele synchronisatie in in plaats van een volledige synchronisatie planning. Zie [Active Directory-systeem detectie](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem)voor meer informatie.<!-- 353CAFBC-AC90-4FD3-B3CF-51D6D9FB376C -->

- **Active Directory gebruikers detectie is zo geconfigureerd dat ze te vaak worden uitgevoerd**: u hoeft niet in te stellen Active Directory gebruikers detectie vaker dan om de drie uur vaker optreedt. Een frequentere configuratie kan een negatieve invloed hebben op de prestaties van Active Directory, het netwerk en Configuration Manager. Schakel incrementele synchronisatie in in plaats van een volledige synchronisatie planning. Zie [Active Directory gebruikers detectie](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser)voor meer informatie.<!-- 2E742924-7319-4013-B1E1-97DE7EB16B74 -->

- **Verzamelingen beperkt tot alle systemen of alle gebruikers**: Bekijk verzamelingen die gebruikmaken van de verzamelingen **alle systemen** of **alle gebruikers** als beperkende verzameling. Met Configuration Manager wordt het lidmaatschap van deze standaard verzamelingen bijgewerkt met gegevens van de Active Directory detectie methoden. Deze gegevens zijn mogelijk geen geldige informatie voor Configuration Manager-clients.<!-- 2382F0C9-A36D-4079-AB37-E3D8EE47E8D4 -->

- **Heartbeat-detectie is uitgeschakeld**: voor heartbeat-detectie moet de Configuration Manager-client op apparaten worden geïnstalleerd. Het is de enige detectie methode die clients starten. Alle andere methoden vinden plaats op site servers. Heartbeat-detectie is essentieel om de status van client activiteiten actueel te laten blijven. Het zorgt ervoor dat de site de resource records uit de site database niet per ongeluk heeft geleeftijd. Zie [heartbeat-detectie](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)voor meer informatie.<!-- A3089798-DF4E-490A-AF78-4AF474B214CF -->

- **Langdurige query's voor het uitvoeren van een verzameling ingeschakeld voor incrementele updates**: verzamelingen met een laatste incrementele vernieuwings tijd van meer dan 30 seconden site server-en database bronnen gebruiken die mogelijk van invloed kunnen zijn op de algehele Configuration Manager prestaties. Zie [Aanbevolen procedures voor verzamelingen](../../clients/manage/collections/best-practices-for-collections.md)voor meer informatie.<!-- 21F14C0E-008B-47F3-B1E2-19CF79DC97B4 -->

- **Verminder het aantal toepassingen en pakketten op distributie punten**: micro soft officieel ondersteunt een gecombineerd totaal van maxi maal 10.000 pakketten en toepassingen op een distributie punt. Een overschrijding van dit totaal kan leiden tot operationele problemen. Zie [grootte en schaal getallen-distributie punt](../../plan-design/configs/size-and-scale-numbers.md#distribution-point)voor meer informatie.<!-- FFE6906E-932E-4927-8EE0-BA25C37943CB -->

- Problemen met de installatie van de **secundaire site**: de installatie status van sommige secundaire sites **in behandeling** of **mislukt**. Deze statussen betekenen dat u de installatie hebt gestart, maar niet is voltooid. Totdat de installatie van de secundaire site is voltooid, communiceren clients mogelijk niet goed met de primaire site. Controleer de werk ruimte **bewaking** en voer de installatie opnieuw uit. Zie [de installatie van een mislukte update opnieuw uitvoeren](install-in-console-updates.md#bkmk_retry)voor meer informatie.<!-- ED3F5BDD-2F02-44A4-87F4-BB2C1032D4DE -->

- **Alle sites bijwerken naar dezelfde versie**: gebruik dezelfde versie van Configuration Manager in een hiërarchie. Deze configuratie zorgt ervoor dat alle sites dezelfde functionaliteit bieden. Sites van verschillende versies in dezelfde hiërarchie introduceren interoperabiliteits scenario's. Latere versies van Configuration Manager bevatten nieuwe functies en oplossingen voor bekende problemen. Zie [interoperabiliteit tussen verschillende versies](../../plan-design/hierarchy/interoperability-between-different-versions.md)voor meer informatie.<!-- 88C630A5-6D6B-4DDB-95D7-78E12107970D -->

Zie [herstel stappen voor Configuration Manager management Insights](/services-hub/health/remediation-steps-configmgr)voor meer informatie over deze inzichten.

> [!TIP]
> Als u al een klant van micro soft Unified of micro soft premier bent, meldt u zich aan bij de [Services hub](https://serviceshub.microsoft.com/assessments/) voor aanvullende evaluaties op aanvraag.
>
> Zie [oplossingen voor ondersteuning](https://www.microsoft.com/enterprise/services/support)voor meer informatie over micro soft-Services.

### <a name="operating-system-deployment"></a>Implementatie van besturingssystemen

<!--6982275-->

Vanaf versie 2006 kunt u met de volgende beheer inzichten de beleids grootte van taken reeksen beheren. Wanneer de grootte van het taken reeks beleid groter is dan 32 MB, kan de client het grote beleid niet verwerken. De client kan de taken reeks implementatie vervolgens niet uitvoeren.

- **Grote taken reeksen kunnen bijdragen aan meer dan de maximale beleids grootte**: als u deze taken reeksen implementeert, kunnen clients de grote beleids objecten mogelijk niet verwerken. Verklein de grootte van het taken reeks beleid om te voor komen dat er problemen ontstaan met de verwerking van beleid.<!-- D9A15248-832E-4780-8151-ACD1B9E53FE1 -->

- De **totale beleids grootte voor taken reeksen overschrijdt de limiet**voor het beleid: clients kunnen het beleid voor deze taken reeksen niet verwerken omdat het te groot is. Verklein de grootte van het taken reeks beleid zodat de implementatie op clients kan worden uitgevoerd.<!-- 6568F6A3-D1D8-4E63-940B-FE44F8349802 -->

Zie [de grootte van het taken reeks beleid beperken](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize)voor meer informatie.

In versie 2006 is het volgende inzicht van de **proactieve onderhouds** groep naar deze groep verplaatst:

- **Ongebruikte opstart installatie kopieën**: er wordt niet naar opstart installatie kopieën verwezen voor het opstarten van de PXE-opstart bewerking of de taken reeks Zie [opstart installatie kopieën beheren](../../../osd/get-started/manage-boot-images.md)voor meer informatie.<!-- 4C1FBA51-AD56-4CA8-8326-066F65D24F0E -->

### <a name="optimize-for-remote-workers"></a>Optimaliseren voor externe werk rollen

<!--6982226-->

Met ingang van versie 2006 kunt u met de volgende inzichten betere ervaringen maken voor externe werk nemers en de belasting van uw infra structuur verminderen:

- **VPN-verbonden clients configureren om de voor keur te geven aan Cloud-inhouds bronnen**: als u het verkeer op de VPN wilt beperken, schakelt u de optie voor grens groepen in om de voor keur te geven aan **Cloud bronnen over on-premises bronnen**. Met deze optie kunnen clients inhoud downloaden van Internet in plaats van distributie punten via de VPN-verbinding. Zie [Opties voor grens groepen](../deploy/configure/boundary-groups.md#bkmk_bgoptions4)voor meer informatie.<!-- 1BFD7A7A-077C-4E8A-9EAA-4559E41D400A -->

- **VPN-grens groepen definiëren**: een VPN-grens maken en koppelen aan een grens groep. Koppel VPN-specifieke site systemen aan de groep en configureer de instellingen voor uw omgeving. In dit inzicht wordt gecontroleerd op ten minste één grens groep met ten minste één VPN-grens. Selecteer in de eigenschappen van deze inzichten **controleren acties** om naar het knoop punt **grens groepen** te gaan. Zie [type VPN-grens](../deploy/configure/boundaries.md#vpn)voor meer informatie.<!-- E44BF0CC-0ADA-4B00-A4DF-4005256DF73E -->

- **Peer-to-peer-inhoud delen uitschakelen voor VPN-verbonden clients**: als u wilt voor komen dat het peer-to-peer-verkeer dat waarschijnlijk geen voor deel is van de externe clients, schakelt u de optie grens groep uit om **peer-down loads in deze grens groep toe te staan**. Zie [Opties voor grens groepen](../deploy/configure/boundary-groups.md#bkmk_bgoptions1)voor meer informatie.<!-- 60404B23-96A9-4EE2-B8D6-1F226C2F2F5A -->

### <a name="proactive-maintenance"></a>Proactief onderhoud

<!--1352184-->
De inzichten in deze groep markeren mogelijke configuratie problemen om te voor komen dat Configuration Manager objecten worden bewaard.

- **Grens groepen zonder toegewezen site systemen**: als u geen site systemen hebt toegewezen, kunnen grens groepen alleen worden gebruikt voor site toewijzing. Zie [grens groepen configureren](../deploy/configure/boundary-groups.md)voor meer informatie.<!-- 01E5A4BC-0E31-494E-A553-2B32C410FA5B -->

- **Grens groepen zonder leden**: grens groepen zijn niet van toepassing op site toewijzing of het opzoeken van inhoud als ze geen leden hebben. Zie [grens groepen configureren](../deploy/configure/boundary-groups.md)voor meer informatie.<!-- 4f0d37b1-f979-4ba3-b15b-7fe3c915f239 -->

- **Distributie punten die geen inhoud leveren aan clients**: distributie punten die in de afgelopen 30 dagen geen inhoud hebben aangeboden aan clients. Deze gegevens zijn gebaseerd op rapporten van clients van hun download geschiedenis. Zie [distributie punten installeren en configureren](../deploy/configure/install-and-configure-distribution-points.md)voor meer informatie.<!-- 9A115092-F8D4-4AB7-B846-C09143B9B9B0 -->

- **WSUS-opschoning inschakelen**: controleert of u de optie voor het uitvoeren van WSUS-opschoning hebt ingeschakeld op de eigenschappen van het onderdeel Software-update punt. Met deze optie kunt u de prestaties van WSUS verbeteren. Zie [Software update Maintenance](../../../sum/deploy-use/software-updates-maintenance.md)(Engelstalig) voor meer informatie.<!-- D43080F1-FE98-4F24-94ED-FEB1C2DDEF50 -->

- **Ongebruikte configuratie-items**: configuratie-items die geen deel uitmaken van een configuratie basislijn en ouder zijn dan 30 dagen. Zie [configuratie basislijnen maken](../../../compliance/deploy-use/create-configuration-baselines.md)voor meer informatie.<!-- 0597907B-17D4-4EA5-92E4-CCE692E1468D -->

- **Peer-cache bronnen upgraden naar de nieuwste versie van de Configuration Manager-client**:<!--1358008--> Clients identificeren die als peer-cache bron fungeren, maar geen upgrade hebben uitgevoerd van een pre-1806-client versie. Pre-1806-clients kunnen niet worden gebruikt als peer-cache bron voor clients waarop versie 1806 of hoger wordt uitgevoerd. Selecteer **actie ondernemen** om een weer gave apparaat te openen waarin de lijst met clients wordt weer gegeven.<!-- B51C6733-F9FF-46BC-8F5E-624F2CBED719 -->

> [!TIP]
> In versie 2006 wordt het inzicht voor **ongebruikte opstart installatie kopieën** verplaatst naar de nieuwe implementatie groep voor het [besturings systeem](#operating-system-deployment) .

### <a name="security"></a>Beveiliging

Inzichten voor het verbeteren van de beveiliging van uw infra structuur en apparaten.

- **NTLM-terugval is ingeschakeld**:<!--4572953--> Vanaf versie 1906 wordt met dit inzicht gedetecteerd als u de terugval methode voor minder veilige NTLM-verificatie hebt ingeschakeld voor de site. Wanneer u de client push methode voor het installeren van de Configuration Manager-client gebruikt, kan voor de site wederzijdse verificatie van Kerberos vereist zijn. Deze verbetering helpt bij het beveiligen van de communicatie tussen de server en de client. Zie [clients installeren met client push](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)voor meer informatie.<!-- C16C6826-8209-47A9-BA71-14A8C83E4C35 -->

- **Niet-ondersteunde antimalware-client versies**: meer dan 10% van de clients voert een versie van System Center-Endpoint Protection uit die niet worden ondersteund. Zie [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)voor meer informatie.<!-- ACD63321-CF15-4CDD-B1A3-69005887C633 -->

### <a name="simplified-management"></a>Vereenvoudigd beheer

Inzichten waarmee u het dagelijkse beheer van uw omgeving kunt vereenvoudigen.

- **De site verbinden met de micro soft-Cloud voor Configuration Manager-updates**: dit inzicht zorgt ervoor dat uw Configuration Manager service verbindings punt in de afgelopen zeven dagen verbinding heeft met de micro soft Cloud. Deze verbinding is het downloaden van inhoud voor regel matige updates. Controleer DMPDownloader. log en hman. log. Zie [vereisten voor Internet toegang](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates)voor meer informatie.<!-- AC662C91-54DF-4B43-B09A-B19D2766144B -->

- **Niet-CB-client versies**: een lijst met alle clients waarvan de versies geen CB-build (current branch) zijn. Zie [upgrade-clients](../../clients/manage/upgrade/upgrade-clients.md)voor meer informatie.<!-- 450090EA-DF71-428C-AB49-6DEBB85A004C -->

- **Clients bijwerken naar een ondersteunde versie van Windows 10**:<!--3897268--> Dit inzicht rapporteert op clients met een versie van Windows 10 die niet meer wordt ondersteund. Het bevat ook clients met een Windows 10-versie die bijna op het einde van de service (drie maanden) ligt.<!-- 560669D6-1756-4814-9505-C54BDB4930D0 -->

### <a name="software-center"></a>Software Center

Inzichten voor het beheren van software Center.

- **Gebruikers naar Software Center leiden in plaats van toepassingscatalogus**: controleren of gebruikers in de afgelopen 14 dagen toepassingen hebben geïnstalleerd of aangevraagd in de toepassings catalogus. De primaire functionaliteit van de toepassings catalogus is nu opgenomen in Software Center. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [afgeschafte functies](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)voor meer informatie.<!-- DB9E65CF-C59C-4B76-B6A0-ADB95D809246 -->

- **De nieuwe versie van software Center gebruiken**: de vorige versie van software Center wordt niet meer ondersteund. Stel clients in om het nieuwe software Center te gebruiken door de client instelling **Nieuw Software Center** in de groep **computer agent** in te scha kelen. Zie [over client instellingen](../../clients/deploy/about-client-settings.md#use-new-software-center)voor meer informatie.<!-- A9BCA10D-834F-4F39-89F5-CDCCE8F80C56 -->

### <a name="software-updates"></a>Software-updates

- **Client instellingen zijn niet geconfigureerd om clients toe te staan Delta-inhoud te downloaden**: sommige software-updates die in uw omgeving worden gesynchroniseerd, bevatten Delta-inhoud. De client instelling inschakelen, **clients toestaan om Delta-inhoud te downloaden wanneer deze beschikbaar zijn**. Als u deze instelling niet inschakelt, zal de client onnodig meer inhoud downloaden dan nodig is om deze updates te implementeren. Zie [client instellingen-software-updates](../../clients/deploy/about-client-settings.md#software-updates)voor meer informatie.<!-- 3E2E9E10-1CDC-47E3-BFC9-3A46AB7FE1BD -->

- **De product categorie software-updates (Windows 10, versie 1903 en hoger) inschakelen**: er is een nieuwe product categorie voor software-updates voor Windows 10, versie 1903 of hoger. Als u Windows 10-updates synchroniseert en clients met Windows 10, versie 1903 of hoger hebt, selecteert u de product categorie **Windows 10, versie 1903 en hoger** in de eigenschappen van software-update punt componenten. Zie voor meer informatie[classificaties en producten configureren om te synchroniseren](../../../sum/get-started/configure-classifications-and-products.md).<!-- 16B1152D-6511-4DC7-824E-539B2597F9B0 -->

### <a name="windows-10"></a>Windows 10

Inzichten met betrekking tot de implementatie en het onderhoud van Windows 10. De Windows 10 Management Insight-groep is alleen beschikbaar wanneer er meer dan de helft van clients Windows 7, Windows 8 of Windows 8,1 wordt uitgevoerd.

- **Windows diagnostische gegevens en commerciële ID-sleutel configureren**: als u gegevens van Desktop Analytics wilt gebruiken, configureert u apparaten met een commerciële id-sleutel en schakelt u het verzamelen van diagnostische gegevens in. Stel Windows 10-apparaten in op het niveau **verbeterd (beperkt)** of hoger. Zie voor meer informatie [delen van gegevens inschakelen voor desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).<!-- B224393F-B255-4C80-A1D1-1014BE1DC7D4 -->
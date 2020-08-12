---
title: Grens groepen configureren
titleSuffix: Configuration Manager
description: Clients helpen site systemen te vinden door gebruik te maken van grens groepen om gerelateerde netwerk locaties logisch te organiseren met de naam grenzen
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7a925c29b5d186f3ca6f320741f5ca602b0bbb79
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128389"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Grens groepen voor Configuration Manager configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik grens groepen in Configuration Manager om gerelateerde netwerk locaties ([grenzen](boundaries.md)) logisch te organiseren, zodat u uw infra structuur eenvoudiger kunt beheren. Wijs grenzen toe aan grens groepen voordat u de grens groep gebruikt.

Configuration Manager maakt standaard een standaard site grens groep op elke site.

Als u grens groepen wilt configureren, koppelt u grenzen (netwerk locaties) en site systeem rollen, zoals distributie punten, aan de grens groep. Deze configuratie helpt clients te koppelen aan site systeem servers zoals distributie punten die zich in de buurt van de clients op het netwerk bevinden.

Als u de beschik baarheid van servers naar een breder aantal netwerk locaties wilt verg Roten, wijst u dezelfde grens en dezelfde server toe aan meer dan één grens groep.

Clients gebruiken een grens groep voor:  

- Automatische sitetoewijzing  
- Een site systeem server zoeken die een service kan bieden, waaronder:

  - Distributie punten voor locatie van inhoud  
  - Software-update punten  
  - Status migratie punten  

    > [!NOTE]
    > Het status migratie punt maakt geen gebruik van terugval relaties. Zie [terugval](#fallback)voor meer informatie.

  - Voorkeurs beheer punten  

    > [!NOTE]  
    > Als u voorkeurs beheer punten gebruikt, schakelt u deze optie in voor de hiërarchie, niet vanuit de configuratie van de grens groep. Zie het [gebruik van voorkeurs beheer punten inschakelen](boundary-group-procedures.md#bkmk_proc-prefer)voor meer informatie.  

  - Cloud beheer gateway (vanaf versie 1902)

## <a name="boundary-groups-and-relationships"></a>Grens groepen en relaties

Voor elke grens groep in uw hiërarchie kunt u het volgende toewijzen:

- Een of meer grenzen. De **huidige** grens groep van een client is een netwerk locatie die is gedefinieerd als een grens die is toegewezen aan een specifieke grens groep. Een client kan meer dan één huidige grens groep hebben.  

- Een of meer site systeem rollen. Clients kunnen altijd rollen gebruiken die zijn gekoppeld aan hun huidige grens groep. Afhankelijk van aanvullende configuraties kunnen ze rollen gebruiken in aanvullende grens groepen.  

Voor elke grens groep die u maakt, kunt u een eenrichtings koppeling naar een andere grens groep configureren. De koppeling wordt een **relatie**genoemd. De grens groepen waarnaar u een koppeling wilt maken, worden **naburige** grens groepen genoemd. Een grens groep kan meer dan één relatie hebben, elk met een specifieke grens groep voor de neighbor.

Wanneer een client geen beschikbaar site systeem in de huidige grens groep kan vinden, bepaalt de configuratie van elke relatie wanneer een grens groep wordt gestart. Deze zoek opdracht van extra groepen heet **terugval**.

Zie voor meer informatie de volgende procedures:  

- [Een grens groep maken](boundary-group-procedures.md#bkmk_create)  
- [Een grens groep configureren](boundary-group-procedures.md#bkmk_config)  

### <a name="show-boundary-groups-for-devices"></a><a name="bkmk_show-boundary"></a>Grens groepen voor apparaten weer geven

<!--6521835-->

Vanaf versie 2002 kunt u de grens groepen voor specifieke apparaten weer geven om het gedrag van apparaten met grens groepen beter te identificeren en op te lossen. Voeg de kolom nieuwe **grens groep (en)** toe aan de lijst weergave van het knoop punt **apparaten** of wanneer u de leden van een **apparaat verzameling**weergeeft.

- Als een apparaat zich in meer dan één grens groep bevindt, is de waarde een lijst met door komma's gescheiden namen van grens groepen.

- De gegevens worden bijgewerkt wanneer de client een locatie aanvraag naar de site of Maxi maal elke 24 uur uitvoert.

- Als een client roaming heeft en geen lid is van een grens groep, is de waarde leeg.

> [!NOTE]
> Deze informatie is site gegevens en alleen beschikbaar op primaire sites. Er wordt geen waarde voor deze kolom weer geven wanneer u de Configuration Manager verbindt met een centrale beheer site.

## <a name="fallback"></a>Terugval

Als u problemen wilt voor komen wanneer clients geen beschikbaar site systeem in hun huidige grens groep kunnen vinden, definieert u de relatie tussen grens groepen voor terugval gedrag. Met terugval kan een client de zoek opdracht uitbreiden naar extra grens groepen om een beschikbaar site systeem te vinden.

Relaties worden geconfigureerd op het tabblad Eigenschappen **relaties** van een grens groep. Wanneer u een relatie configureert, definieert u een koppeling naar een grens groep in de nabijheid. Configureer voor elk type ondersteunde site systeemrol onafhankelijke instellingen voor terugval naar de grens groep van de neighbor. Zie [terugval gedrag configureren](boundary-group-procedures.md#bkmk_bg-fallback)voor meer informatie.

Wanneer u bijvoorbeeld een relatie configureert met een specifieke grens groep, moet u terugval instellen voor distributie punten die na 20 minuten moeten worden uitgevoerd. De standaard waarde is 120 minuten voor een uitgebreidere voor beeld. Zie [voor beeld van het gebruik van grens groepen](#example-of-using-boundary-groups).

Als een client geen beschik bare site systeemrol in de huidige grens groep kan vinden, gebruikt de client de terugval tijd in minuten. Deze terugval tijd bepaalt wanneer de client begint te zoeken naar een beschikbaar site systeem dat is gekoppeld aan de grens groep van de neighbor.  

Wanneer een client geen beschikbaar site systeem kan vinden, begint het met zoeken naar locaties vanuit grens groepen in de buur. Dit gedrag verhoogt de groep beschik bare site systemen. De configuratie van grens groepen en hun relaties definieert het gebruik van deze groep beschik bare site systemen van de client.

- Een grens groep kan meer dan één relatie hebben. Met deze configuratie kunt u terugval configureren voor elk type site systeem naar verschillende neighbors na verschillende Peri Oden.  

- Clients vallen alleen terug naar een grens groep die een directe buur is van de huidige grens groep.  

- Wanneer een client lid is van meer dan een grens groep, definieert deze de huidige grens groep als een samen voeging van alle grens groepen. De client terugvalt op de neighbors van een van deze oorspronkelijke grens groepen.  

> [!NOTE]
> De rol van het status migratie punt maakt geen gebruik van terugval relaties. Als u zowel het status migratie punt als distributiepunt rollen aan dezelfde site systeem server toevoegt, moet u terugval niet configureren op de grens groep. Als u de grens groep terugval voor het distributie punt moet gebruiken, voegt u de rol status migratie punt op een andere site systeem server toe.<!-- 2838807 -->

### <a name="the-default-site-boundary-group"></a>De standaard site grens groep

U kunt uw eigen grens groepen maken en elke site heeft een standaard site grens groep die Configuration Manager maakt. Deze groep krijgt de naam **standaard-site-boundary-group &lt;>**. De groep voor site ABC krijgt bijvoorbeeld de naam **standaard-site-grens-groep &lt; ABC>**.

Voor elke grens groep die u maakt, maakt Configuration Manager automatisch een impliciete koppeling naar elke standaard site grens groep in de hiërarchie.  

- De geïmpliceerde koppeling is een standaard terugval optie van een huidige grens groep naar de standaard grens groep van de site. De standaard terugval tijd is 120 minuten.  

- Voor clients die zich niet in een grens bevinden die is gekoppeld aan een grens groep: als u geldige site systeem rollen wilt identificeren, gebruikt u de standaard site grens groep van hun toegewezen site.  

Terugval beheren op de standaard site grens groep:  

- Open de eigenschappen van de standaard grens groep van de site en wijzig de waarden op het tabblad **standaard gedrag** . wijzigingen die u hier aanbrengt, zijn van toepassing op *alle* impliciete koppelingen naar deze grens groep. Wanneer u een expliciete koppeling naar deze standaard site grens groep configureert vanuit een andere grens groep, overschrijft u deze standaard instellingen.  

- Open de eigenschappen van een aangepaste grens groep. Wijzig de waarden voor de expliciete koppeling naar een standaard site grens groep. Wanneer u een nieuwe tijd in minuten voor terugval instelt of terugval blokkeert, is deze wijziging alleen van invloed op de koppeling die u wilt configureren. Configuratie van de expliciete koppeling overschrijft de instellingen op het tabblad **standaard gedrag** van een standaard site grens groep.  

## <a name="site-assignment"></a>Site toewijzing  

U kunt iedere grensgroep configureren met een toegewezen site voor clients.  

- Een nieuw geïnstalleerde client die gebruikmaakt van automatische site toewijzing, wordt gekoppeld aan de toegewezen site van een grens groep die de huidige netwerk locatie van de client bevat.  

- Na het toewijzen aan een-site, wijzigt een client de toewijzing van de site niet wanneer de netwerk locatie ervan wordt gewijzigd. Een client kan bijvoorbeeld zwerven naar een nieuwe netwerk locatie. Deze locatie is een grens in een grens groep met een andere site toewijzing. De toegewezen site van de client wordt niet gewijzigd.  

- Wanneer Active Directory systeem detectie een nieuwe resource detecteert, evalueert de site de netwerk gegevens voor de resource op basis van de grenzen in grens groepen. In dit proces wordt de nieuwe bron aan een toegewezen site gekoppeld voor de push-clientinstallatie.  

- Wanneer een grens lid is van meer dan een grens groepen met verschillende toegewezen sites, selecteren clients wille keurig een van de sites.  

- Wijzigingen in de toegewezen site van een grens groep gelden alleen voor nieuwe acties voor site toewijzingen. Clients die eerder aan een site zijn toegewezen, evalueren hun site toewijzing niet opnieuw op basis van wijzigingen in de configuratie van een grens groep (of op hun eigen netwerk locatie).  

Zie [automatische site toewijzing gebruiken voor computers](../../../clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment)voor meer informatie over de toewijzing van client sites.  

Zie de volgende procedures voor meer informatie over het configureren van site toewijzing:

- [Site toewijzing configureren en site systeem servers selecteren](boundary-group-procedures.md#bkmk_references)
- [Een terugval site configureren voor automatische site toewijzing](boundary-group-procedures.md#bkmk_site-fallback)

## <a name="distribution-points"></a>Distributiepunten

Wanneer een client de locatie van een distributie punt aanvraagt, stuurt Configuration Manager de client een lijst met site systemen. Deze site systemen zijn van het juiste type dat is gekoppeld aan elke grens groep die de huidige netwerk locatie van de client bevat:

- **Tijdens software distributie**vragen clients een locatie aan voor implementatie-inhoud op een geldige inhouds bron. Deze locatie kan een distributie punt of een peer-cache bron zijn.  

- **Tijdens de implementatie van het besturings systeem**vragen clients een locatie aan voor het verzenden of ontvangen van hun status migratie-informatie.  

  - Clients verwerven inhoud op basis van gedrag van grens groepen. Zie [taken reeks ondersteuning voor grens groepen](#bkmk_bgr-osd)voor meer informatie.  

Als een client inhoud aanvraagt die niet beschikbaar is vanuit een bron in de huidige grens groep, wordt tijdens de implementatie van de inhoud de client nog steeds gevraagd om die inhoud. De client probeert verschillende inhouds bronnen in de huidige grens groep te halen totdat deze de terugval periode voor een neighbor of de standaard site grens groep bereikt. Als de client nog geen inhoud heeft gevonden, wordt de zoek opdracht voor inhouds bronnen uitgevouwen om de grens groepen in de buur op te halen.

Als u de inhoud zodanig configureert dat deze op aanvraag wordt gedistribueerd en deze niet beschikbaar is op een distributie punt wanneer een client hierom vraagt, begint de site met het overdragen van de inhoud naar dat distributie punt. Het is mogelijk dat de client de server als een inhouds bron detecteert voordat deze terugvalt op het gebruik van een grens groep in de buur.

### <a name="client-installation"></a><a name="bkmk_ccmsetup"></a>Client installatie

Het installatie programma van de Configuration Manager-client, ccmsetup, kan installatie-inhoud ophalen van een lokale bron of via een beheer punt. Het eerste gedrag is afhankelijk van de opdracht regel parameters die u gebruikt om de-client te installeren:<!-- MEMDocs#286 -->

- Als u de para meters **/MP** of **/Source** niet gebruikt, probeert ccmsetup een lijst met beheer punten te verkrijgen van Active Directory of DNS.
- Als u alleen **/Source**opgeeft, wordt de installatie van het opgegeven pad geforceerd. Er worden geen beheer punten gedetecteerd. Als de ccmsetup.cab niet kan worden gevonden op het opgegeven pad, mislukt ccmsetup.
- Als u zowel **/MP** als **/Source**opgeeft, worden de opgegeven beheer punten gecontroleerd en detecteert deze. Als er geen geldig beheer punt kan worden gevonden, valt het terug naar het opgegeven bronpad.

Zie [para meters en eigenschappen van client installatie](../../../clients/deploy/about-client-installation-properties.md)voor meer informatie over deze ccmsetup-para meters.

<!--1358840-->
Wanneer ccmsetup contact maakt met het beheer punt om de benodigde inhoud te vinden, retourneert het beheer punt distributie punten op basis van de configuratie van de grens groep. Als u relaties voor de grens groep definieert, retourneert het beheer punt de distributie punten in de volgende volg orde:

1. Huidige grens groep  
2. Grens groepen in de buur  
3. De standaard site grens groep  

> [!Note]  
> Het installatie proces van de client maakt geen gebruik van de terugval tijd. Als u zo snel mogelijk inhoud wilt zoeken, keert u direct terug naar de volgende grens groep.
>
> In eerdere versies van Configuration Manager heeft het beheer punt tijdens dit proces alleen distributie punten geretourneerd in de huidige grens groep van de client. Als er geen inhoud beschikbaar was, wordt het installatie proces teruggestuurd om inhoud te downloaden vanaf het beheer punt. Er is geen optie om terug te vallen op distributie punten in andere grens groepen die mogelijk de benodigde inhoud hebben.

### <a name="task-sequence-support-for-boundary-groups"></a><a name="bkmk_bgr-osd"></a>Ondersteuning van taken reeksen voor grens groepen

<!--1359025-->
Wanneer een apparaat een taken reeks uitvoert en inhoud moet verkrijgen, worden er gedragen van grens groepen gebruikt die vergelijkbaar zijn met de Configuration Manager-client.

Configureer dit gedrag met behulp van de volgende instellingen op de pagina **distributie punten** van de taken reeks implementatie:

- **Als er geen lokaal distributie punt beschikbaar is, gebruikt u een extern distributie punt**: voor deze implementatie kan de taken reeks terugkeren naar distributie punten in een grens groep in de nabijheid.  

- **Clients toestaan distributie punten te gebruiken van de standaard site grens groep**: voor deze implementatie kan de taken reeks terugkeren naar distributie punten in de standaard site grens groep.  

Als u dit nieuwe gedrag wilt gebruiken, moet u ervoor zorgen dat clients worden bijgewerkt naar de nieuwste versie.

#### <a name="location-priority"></a>Locatie prioriteit  

De taken reeks probeert inhoud in de volgende volg orde te verkrijgen:  

1. Peer-cache bronnen  

2. Distributie punten in de *huidige* grens groep  

3. Distributie punten *in een grens* groep in de nabijheid  

    > [!Important]  
    > Als gevolg van de real-time van de taken reeks verwerking, wordt niet gewacht op de failover-tijd van een grens groep in de nabijheid. Het gebruikt de failover-tijden voor het bepalen van de prioriteit van de grens groepen van de neighbor. Als de taken reeks bijvoorbeeld geen inhoud kan ophalen van een distributie punt in de huidige grens groep, probeert deze onmiddellijk een distributie punt in een grens groep in de nabijheid met de kortste failover-tijd. Als dit proces mislukt, wordt er een failover uitgevoerd naar een distributie punt in een grens groep in de nabijheid met een grotere timer tijd.  

4. Distributie punten in de *standaard site* grens groep  

In het logboek bestand van de taken reeks **bestand smsts. log** wordt de prioriteit weer gegeven van de locatie bronnen die worden gebruikt op basis van de implementatie-eigenschappen.

### <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>Opties voor grens groepen voor het downloaden van peers

<!--1356193, 1358749-->
Grens groepen bevatten de volgende aanvullende instellingen om u meer controle te geven over de distributie van inhoud in uw omgeving:  

- [Peer-down loads in deze grens groep toestaan](#bkmk_bgoptions1)  

- [Gebruik tijdens het downloaden van de peer alleen peers binnen hetzelfde subnet](#bkmk_bgoptions2)  

- [Voor keur voor distributie punten boven peers met hetzelfde subnet](#bkmk_bgoptions3)  

- [Distributie punten in de Cloud via distributie punten](#bkmk_bgoptions4)  

Zie [een grens groep configureren](boundary-group-procedures.md#bkmk_config)voor meer informatie over het configureren van deze instellingen.

Als een apparaat zich in meer dan één grens groep bevindt, geldt het volgende gedrag voor deze instellingen:

- **Downloaden van peers in deze grens groep toestaan**: als deze functie is uitgeschakeld in een van de grens groepen, gebruikt de client geen Delivery Optimization.
- **Tijdens het downloaden van de peer gebruikt u alleen peers met hetzelfde subnet**: als deze optie is ingeschakeld in een van de grenzen van een groep, wordt deze instelling van kracht.
- Voor **keur voor distributie punten boven peers binnen hetzelfde subnet**: als deze optie is ingeschakeld in een van de grens groepen, wordt deze instelling van kracht.
- **Voor keur voor Cloud bronnen op basis van on-premises bronnen**: als deze optie is ingeschakeld in een van de grens groepen, wordt deze instelling van kracht.

#### <a name="allow-peer-downloads-in-this-boundary-group"></a><a name="bkmk_bgoptions1"></a>Peer-down loads in deze grens groep toestaan

Deze instelling is standaard ingeschakeld. Het beheer punt biedt clients een lijst met inhouds locaties die peer bronnen bevatten. Deze instelling is ook van invloed op het Toep assen van groeps-Id's voor [optimalisatie van levering](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).  

Er zijn twee veelvoorkomende scenario's waarin u deze optie kunt uitschakelen:  

- Als u een grens groep hebt die grenzen bevat van geografisch verspreide locaties, zoals een VPN. Twee clients kunnen zich in dezelfde grens groep bevinden omdat ze zijn verbonden via VPN, maar op een groot aantal verschillende locaties die niet geschikt zijn voor het delen van inhoud in de peer.  

- Als u een enkele grote grens groep gebruikt voor site toewijzing die niet verwijst naar een distributie punt.  

> [!IMPORTANT]
> Als een apparaat zich in meer dan één grens groep bevindt, moet u deze instelling inschakelen voor alle grens groepen voor het apparaat. Anders kan de client geen leverings optimalisatie gebruiken. De register sleutel DOGroupID kan bijvoorbeeld niet worden ingesteld.

#### <a name="during-peer-downloads-only-use-peers-within-the-same-subnet"></a><a name="bkmk_bgoptions2"></a>Gebruik tijdens het downloaden van de peer alleen peers binnen hetzelfde subnet

Deze instelling is afhankelijk van de voor gaande optie. Als u deze optie inschakelt, wordt het beheer punt alleen opgenomen in de inhouds locatie lijst peer bronnen die zich in hetzelfde subnet bevinden als de client.

Algemene scenario's voor het inschakelen van deze optie:

- Het ontwerp van de grens groep voor inhouds distributie bevat één grote grens groep die andere kleinere grens groepen overlapt. Met deze nieuwe instelling bevat de lijst met inhouds bronnen die het beheer punt aan clients levert alleen peer bronnen uit hetzelfde subnet.

- U hebt één grote grens groep voor alle externe kantoor locaties. Als u deze optie inschakelt, delen clients alleen inhoud in het subnet op de externe kantoor locatie, in plaats van een risico op het delen van inhoud tussen locaties.

Vanaf versie 2002, afhankelijk van de configuratie van uw netwerk, kunt u bepaalde subnetten uitsluiten voor overeenkomende treffers. U wilt bijvoorbeeld een grens opnemen, maar een specifiek VPN-subnet uitsluiten. Configuration Manager sluit standaard het standaard Teredo-subnet () uit `2001:0000:%` .<!--3555777-->

> [!NOTE]
> Wanneer u in versie 2002 [een zelfstandige primaire site uitbreidt](../install/prerequisites-for-installing-sites.md#bkmk_expand) om een centrale beheer site toe te voegen, wordt de lijst met uitsluitingen van het subnet teruggezet naar de standaard waarde. U kunt dit probleem omzeilen door na het uitbreiden van de site het Power shell-script uit te voeren om de lijst met uitsluitingen van het subnet te aanpassen op de CAS.<!-- 6309068 -->

Importeer de lijst met uitgesloten subnetten als een teken reeks met door komma's gescheiden subnetten. Gebruik het procent teken ( `%` ) als Joker teken. Stel op de site server op het hoogste niveau de Inge sloten eigenschap **SubnetExclusionList** in voor het onderdeel **SMS_HIERARCHY_MANAGER** in de klasse **SMS_SCI_Component** . Zie [SMS_SCI_Component Server WMI-klasse](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)voor meer informatie.

##### <a name="sample-powershell-script-to-update-the-subnet-exclusion-list"></a>Power shell-voorbeeld script voor het bijwerken van de lijst met uitgesloten subnetten

Het volgende script is een voor beeld van een manier om deze waarde te wijzigen. Voeg uw subnetten toe aan de variabele **PropertyValue** na `2001:0000:%,172.16.16.0` . Het is een door komma's gescheiden teken reeks. Voer dit script uit op de site server op het hoogste niveau in uw hiërarchie.

```PowerShell
$PropertyValue = "2001:0000:%,172.16.16.0"
$PropertyName = "SubnetExclusionList"

$providerMachine = Get-WmiObject -Class "SMS_ProviderLocation" -Namespace "root\sms"

if ($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = Get-WmiObject -Query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_HIERARCHY_MANAGER"' -ComputerName $providerMachine.Machine -Namespace root\sms\site_$SiteCode
$properties = $component.props

Write-host "Updating property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -like $PropertyName)
  {
    Write-host "Current value for SubnetExclusionList is  " $property.value1
    $property.value1 = $PropertyValue
    Write-host "Updating value for SubnetExclusionList to " $property.value1
    break
  }
}

$component.props = $properties
$component.put()
```

> [!NOTE]
> Configuration Manager bevat standaard het Teredo-subnet in deze lijst. Lees altijd eerst de bestaande waarde wanneer u de lijst wijzigt. Voeg extra subnetten toe aan de lijst en stel vervolgens de nieuwe waarde in.

#### <a name="prefer-distribution-points-over-peers-with-the-same-subnet"></a><a name="bkmk_bgoptions3"></a>Voor keur voor distributie punten boven peers met hetzelfde subnet

Het beheer punt heeft standaard prioriteit voor peer-cache bronnen boven aan de lijst met inhouds locaties. Deze instelling omkeert die prioriteit voor clients die zich in hetzelfde subnet bevinden als de peer-cache bron.

> [!TIP]
> Dit gedrag is van toepassing op de Configuration Manager-client. Het is niet van toepassing wanneer de taken reeks inhoud downloadt. Wanneer de taken reeks wordt uitgevoerd, geeft deze de voor keur aan peer-cache bronnen via distributie punten.<!-- SCCMDocs#1376 -->

#### <a name="prefer-cloud-distribution-points-over-distribution-points"></a><a name="bkmk_bgoptions4"></a>Distributie punten in de Cloud via distributie punten

Als u een filiaal hebt met een snellere Internet koppeling, kunt u nu de prioriteit van de Cloud inhoud bepalen.  

In versie 1902 is deze instelling nu de titel van de **voor keur voor Cloud bronnen over on-premises bronnen**. Cloud bronnen zijn onder andere het volgende:<!-- SCCMDocs#1529 -->

- Cloud distributiepunten
- Microsoft Update (toegevoegd in versie 1902)

## <a name="software-update-points"></a><a name="bkmk_sup"></a>Software-update punten 

Clients gebruiken grens groepen om een nieuw software-update punt te vinden. Als u wilt bepalen welke servers een client kan vinden, voegt u afzonderlijke software-update punten toe aan verschillende grens groepen.

Als u alle bestaande software-update punten aan de standaard site grens groep toevoegt, selecteert de client een software-update punt uit de groep beschik bare servers. Dit gedrag is vergelijkbaar met eerdere versies van Configuration Manager current branch. Voor beheerde selectie en terugval gedrag voegt u afzonderlijke software-update punten toe aan verschillende grens groepen.

Als u een nieuwe site installeert, worden software-update punten niet toegevoegd aan de standaard site grens groep. Wijs software-update punten toe aan een grens groep zodat clients deze kunnen vinden en gebruiken.

### <a name="fallback-for-software-update-points"></a>Terugval voor software-update punten

Terugval voor software-update punten is geconfigureerd als andere site systeem rollen, maar heeft het volgende voor behoud:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>Nieuwe clients gebruiken grens groepen om software-update punten te selecteren

Wanneer u nieuwe clients installeert, selecteren ze een software-update punt van die servers die zijn gekoppeld aan de grens groepen die u configureert. Dit gedrag vervangt het vorige gedrag waarbij clients wille keurig een software-update punt selecteren uit een lijst met servers die het forest van de client delen.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>Clients blijven een laatste bekend-goed software-update punt gebruiken totdat ze terugval een nieuwe hebben gevonden

Clients die al een software-update punt hebben, blijven deze gebruiken totdat het niet kan worden bereikt. Dit gedrag omvat een blijvend gebruik van een software-update punt dat niet is gekoppeld aan de huidige grens groep van de client.

Dit gedrag is opzettelijk. De client blijft een bestaand software-update punt gebruiken, zelfs wanneer het zich niet in de huidige grens groep van de client bevindt. Wanneer het software-update punt wordt gewijzigd, synchroniseert de client gegevens met de nieuwe server, waardoor een aanzienlijk netwerk gebruik wordt veroorzaakt. Als alle clients tegelijkertijd overschakelen naar een nieuwe server, helpt de vertraging in overgang om te voor komen dat uw netwerk verzadigt.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>Een client probeert het laatst bekende goede software-update punt gedurende 120 minuten altijd te bereiken voordat de terugval wordt gestart

Als de client geen contact heeft gemaakt, wordt na 120 minuten terugval gestart. Wanneer terugval wordt gestart, ontvangt de client een lijst met alle software-update punten in de huidige grens groep. Er zijn extra software-update punten in de neighbor-en site standaard grens groepen beschikbaar op basis van terugval configuraties.

### <a name="fallback-configurations-for-software-update-points"></a>Terugval configuraties voor software-update punten

U kunt **terugval tijden (in minuten)** configureren voor software-update punten die kleiner zijn dan 120 minuten. De client probeert echter wel het oorspronkelijke software-update punt voor 120 minuten te bereiken. Vervolgens wordt de zoek opdracht uitgebreid naar extra servers. Terugval tijden voor grens groepen worden gestart wanneer de client de oorspronkelijke server niet kan bereiken. Wanneer de client de zoek opdracht uitbreidt, biedt de site alle grens groepen die minder dan 120 minuten zijn geconfigureerd.

Als u terugval wilt blok keren voor een software-update punt naar een grens groep in de nabijheid, configureert u de instelling **nooit terugval**.

Als de oorspronkelijke server gedurende twee uur niet kan worden bereikt, gebruikt de client een kortere cyclus om verbinding te maken met een nieuw software-update punt. Dit gedrag zorgt ervoor dat de client snel kan zoeken in de lijst met mogelijke software-update punten.

#### <a name="example"></a>Voorbeeld

U kunt software-update punten in grens groep *A* zo configureren dat deze na **10** minuten worden teruggevallen. U configureert dezelfde instelling voor grens groep *B* tot **130** minuten. Een client in grens groep *Z* kan het laatst bekende-goede software-update punt niet bereiken.

- De client probeert de volgende 120 minuten alleen om de oorspronkelijke server in grens groep Z te bereiken. Na 10 minuten voegt Configuration Manager de software-update punten van grens groep A toe aan de groep beschik bare servers. De client probeert echter geen contact op te nemen met hen of een andere server tot de eerste periode van 120 minuten is verstreken.  

- Na het maken van een verbinding met het oorspronkelijke software-update punt gedurende 120 minuten, breidt de client de zoek opdracht uit. Het voegt servers toe aan de beschik bare groep software-update punten die zich in het huidige en alle neighbor-grens groepen bevinden die gedurende 120 minuten of minder zijn geconfigureerd. Deze groep bevat de servers in grens groep A, die eerder zijn toegevoegd aan de groep beschik bare servers.  

- Na 10 minuten breidt de-client de zoek opdracht uit om software-update punten van grens groep B te gebruiken. Deze periode is 130 minuten van de totale tijd waarna de client het laatst bekende-goede software-update punt niet kan bereiken.  

### <a name="manually-switch-to-a-new-software-update-point"></a>Hand matig overschakelen naar een nieuw software-update punt

In combi natie met terugval gebruikt u client melding om een apparaat hand matig te dwingen om over te scha kelen naar een nieuw software-update punt.

Wanneer u overschakelt naar een nieuwe server, gebruiken de apparaten terugval om die nieuwe server te vinden. Clients scha kelen naar het nieuwe software-update punt tijdens de volgende scan cyclus voor software-updates.<!-- SCCMDocs#1537 -->

Controleer de configuratie van de grens groep. Voordat u met deze wijziging begint, moet u ervoor zorgen dat de software-update punten zich in de juiste grens groepen bevinden.

Zie [hand matig clients overschakelen naar een nieuw software-update punt](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs)voor meer informatie.

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a><a name="bkmk_cmg-sup"></a>Intranet-clients kunnen een CMG-software-update punt gebruiken
<!--7102873-->
Vanaf versie 2006 kunnen intranet-clients toegang krijgen tot een CMG-software-update punt wanneer het wordt toegewezen aan een grens groep en de [optie **Configuration Manager Cloud beheer gateway verkeer toestaan** is ingeschakeld](../../../clients/manage/cmg/setup-cloud-management-gateway.md#bkmk_role) op het software-update punt. U kunt intranet apparaten laten scannen op basis van een CMG-software-update punt in de volgende scenario's:

- Wanneer een Internet machine verbinding maakt met de VPN, gaat deze door met scannen naar het software-update punt CMG via internet.
- Als het enige software-update punt voor de grens groep het CMG software-update punt is, worden alle intranet-en Internet apparaten hierop gecontroleerd.

## <a name="management-points"></a>Beheer punten

<!-- 1324594 -->
Terugval relaties configureren voor beheer punten tussen grens groepen. Dit gedrag biedt meer controle over de beheer punten die clients gebruiken. Op het tabblad **relaties** van de eigenschappen van de grens groep is er een kolom voor het beheer punt. Wanneer u een nieuwe terugval grens groep toevoegt, is de terugval tijd voor het beheer punt momenteel altijd nul (0). Dit gedrag is hetzelfde voor het **standaard gedrag** van de standaard grens groep van de site.

Voorheen werd een veelvoorkomend probleem opgetreden toen u een beveiligd beheer punt in een beveiligd netwerk had. Clients in het hoofd netwerk hebben beleid ontvangen dat dit beveiligde beheer punt bevatte, zelfs als ze niet kunnen communiceren met de server via een firewall. Als u dit probleem nu wilt oplossen, gebruikt u de optie **nooit terugval** om ervoor te zorgen dat clients alleen terugvallen op beheer punten waarmee ze kunnen communiceren.

> [!Note]  
> Als u distributie punten in de standaard grens groep van de site inschakelt voor terugval en een beheer punt zich op een distributie punt bevindt, voegt de site ook dat beheer punt toe aan de standaard grens groep van de site.<!--VSO 2841292-->  

Als een client zich in een grens groep bevindt die geen toegewezen beheer punt heeft, geeft de site de client de volledige lijst met beheer punten. Dit gedrag zorgt ervoor dat een client altijd een lijst met beheer punten ontvangt.

Terugval groep grens groepen van beheer punten wijzigt het gedrag tijdens client installatie (ccmsetup.exe) niet. Als de opdracht regel niet het initiële beheer punt opgeeft met de para meter/MP, ontvangt de nieuwe client de volledige lijst met beschik bare beheer punten. Voor het eerste Boots trap proces gebruikt de client het eerste beheer punt waartoe het toegang heeft. Zodra de client bij de site is geregistreerd, ontvangt de lijst met beheer punten correct gesorteerd met dit nieuwe gedrag.

Zie [client installatie](#bkmk_ccmsetup)voor meer informatie over het gedrag van de client voor het verkrijgen van inhoud tijdens de installatie.

Als u tijdens de client upgrade geen/MP-opdracht regel parameter opgeeft, vraagt de client bronnen zoals Active Directory en WMI op voor elk beschikbaar beheer punt. De configuratie van de grens groep wordt niet door de client upgrade gehonoreerd. <!--VSO 2841292-->  

Als u wilt dat clients deze mogelijkheid gebruiken, schakelt u de volgende instelling in: **clients gebruiken liever beheer punten die zijn opgegeven in grens groepen** in de **hiërarchie-instellingen**.

> [!Note]  
> BESTURINGSSYSTEEM implementatie processen zijn niet op de hoogte van grens groepen voor beheer punten.  

### <a name="troubleshooting"></a>Problemen oplossen

Nieuwe vermeldingen worden weer gegeven in het **bestand locationservices. log**. Het kenmerk **localiteit** identificeert een van de volgende statussen:

- **0**: onbekend  

- **1**: het opgegeven beheer punt bevindt zich alleen in de standaard site grens groep voor terugval  

- **2**: het opgegeven beheer punt bevindt zich in een grens groep van het externe gebied of een neighbor. Wanneer het beheer punt zich in een neighbor en de standaard grens groepen van de site bevindt, is de locatie 2.  

- **3**: het opgegeven beheer punt bevindt zich in de lokale of huidige grens groep. Wanneer het beheer punt zich in de huidige grens groep bevindt en ofwel een neighbor of de standaard grens groep van de site is, is de locatie 3. Als u de instelling voor voorkeurs beheer punten niet inschakelt in de hiërarchie-instellingen, is de locatie altijd 3, ongeacht in welke grens groep het beheer punt zich bevindt.  

Clients gebruiken eerst lokale beheer punten (lokale naam 3), externe seconde (lokale plaats 2) en vervolgens terugval (locatie 1).

Wanneer een client vijf fouten in tien minuten ontvangt en niet kan communiceren met een beheer punt in de huidige grens groep, probeert het contact te maken met een beheer punt in een neighbor of de standaard grens groep van de site. Als het beheer punt in de huidige grens groep later weer online is, keert de client terug naar het lokale beheer punt tijdens de volgende vernieuwings cyclus. De vernieuwings cyclus is 24 uur of wanneer de Configuration Manager Agent-service opnieuw wordt gestart.

## <a name="preferred-management-points"></a><a name="bkmk_preferred"></a>Voorkeurs beheer punten

> [!Note]
> Het gedrag van deze hiërarchie-instelling, **clients gebruiken liever beheer punten die zijn opgegeven in grens groepen**, gewijzigd in versie 1802. Wanneer u deze instelling inschakelt, gebruikt Configuration Manager de functionaliteit van de grens groep voor het toegewezen beheer punt. Zie [beheer punten](#management-points)voor meer informatie.

Met voorkeurs beheer punten kunnen clients een beheer punt identificeren dat is gekoppeld aan de huidige netwerk locatie (grens).  

- Een client probeert een voorkeurs beheer punt te gebruiken van de toegewezen site voordat er een wordt gebruikt dat niet is geconfigureerd als voor keur van de toegewezen site.  

- Als u deze optie wilt gebruiken, moet u **clients liever gebruikmaken van beheer punten die zijn opgegeven in grens groepen** in de **hiërarchie-instellingen**. Configureer vervolgens grens groepen op afzonderlijke primaire sites. Neem de beheer punten op die moeten worden gekoppeld aan de gekoppelde grenzen van de grens groep. Zie het [gebruik van voorkeurs beheer punten inschakelen](boundary-group-procedures.md#bkmk_proc-prefer)voor meer informatie.  

- Wanneer u voorkeurs beheer punten configureert en een client de lijst van beheer punten ordent, plaatst de client de voorkeurs beheer punten boven aan de lijst. Deze lijst bevat alle beheer punten van de toegewezen site van de client.  

> [!NOTE]  
> Client roaming betekent dat de netwerk locaties ervan worden gewijzigd. Bijvoorbeeld wanneer een laptop naar een externe kantoor locatie wordt verplaatst. Wanneer een client roamt, kan deze een beheer punt van de lokale site gebruiken voordat een server van de toegewezen site wordt gebruikt. Deze lijst met servers van de toegewezen site bevat de voorkeurs beheer punten. Zie [begrijpen hoe clients site resources en-services vinden](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)voor meer informatie.  

## <a name="overlapping-boundaries"></a>Overlappende grenzen  

Configuration Manager ondersteunt configuraties met overlappende grenzen voor locatie van inhoud. Wanneer de netwerk locatie van de client tot meer dan een grens groep behoort:

- Wanneer een client inhoud aanvraagt, stuurt Configuration Manager de client een lijst met alle distributie punten die de inhoud hebben.  

- Wanneer een client een server aanvraagt voor het verzenden of ontvangen van de status migratie-informatie, Configuration Manager stuurt de client een lijst met alle status migratie punten die zijn gekoppeld aan een grens groep die de huidige netwerk locatie van de client bevat.  

De client kan door dit gedrag de dichtstbijzijnde server selecteren vanwaar inhoud of statusmigratie-informatie wordt overgedragen.  

## <a name="example-of-using-boundary-groups"></a>Voor beeld van het gebruik van grens groepen

In het volgende voor beeld wordt een-client gebruikt voor het zoeken naar inhoud vanaf een distributie punt. Dit voor beeld kan worden toegepast op andere site systeem rollen die gebruikmaken van grens groepen.

Maak drie grens groepen die geen grenzen of site systeem servers delen:  

- Groeps BG_A met distributie punten DP_A1 en DP_A2  

- Groeps BG_B met distributie punten DP_B1 en DP_B2  

- Groeps BG_C met distributie punten DP_C1 en DP_C2  

Voeg de netwerk locaties van uw clients als grenzen toe aan de grens groep BG_A. Configureer vervolgens relaties van deze grens groep tot de andere twee grens groepen:  

- Configureer distributie punten voor de eerste groep *neighbor* (BG_B) die na 10 minuten moeten worden gebruikt. Deze groep bevat distributie punten DP_B1 en DP_B2. Beide zijn goed verbonden met de grens locaties van de eerste groep.  

- Configureer de tweede *neighbor* -groep (BG_C) die na 20 minuten moet worden gebruikt. Deze groep bevat distributie punten DP_C1 en DP_C2. Beide bevinden zich in een WAN van de andere twee grens groepen.  

- Voeg ook toe aan de standaard site grens groep een ander distributie punt dat zich op de site server bevindt. Deze server is uw minst voorkeurs locatie voor inhouds bronnen, maar is centraal te vinden in alle grens groepen.

    Voor beeld van grens groepen en terugval tijden:

    ![Voor beeld van grens groepen en terugval tijden](media/BG_Fallback.png)  

Met deze configuratie:  

- De client begint met het zoeken naar inhoud vanaf distributie punten in de *huidige* grens groep (BG_A). Het zoekt elk distributie punt gedurende twee minuten en schakelt vervolgens over naar het volgende distributie punt in de grens groep. De groep van geldige inhouds bron locaties van de client bevat DP_A1 en DP_A2.  

- Als de client na tien minuten geen inhoud van de *huidige* grens groep kan vinden, voegt deze de distributie punten van de BG_B grens groep toe aan de zoek opdracht. Vervolgens wordt gezocht naar inhoud van een distributie punt in de gecombineerde groep servers. Deze groep bevat nu servers van zowel de BG_A als BG_B grens groepen. De client blijft binnen twee minuten contact opnemen met elk distributie punt en schakelt vervolgens over naar de volgende server in de groep. De groep van geldige inhouds bron locaties van de client bevat DP_A1, DP_A2, DP_B1 en DP_B2.  

- Na een extra periode van tien minuten (totaal van 20 minuten), als de client nog steeds geen distributie punt met inhoud heeft gevonden, wordt de groep uitgebreid met beschik bare servers uit de tweede groep *neighbor* , grens groep BG_C. De client heeft nu zes distributie punten om te zoeken: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 en DP_C2. Het wordt steeds om de twee minuten overgeschakeld naar een nieuw distributie punt totdat er inhoud wordt gevonden.  

- Als de client na een totaal van 120 minuten geen inhoud heeft gevonden, wordt de *standaard site grens groep* opgenomen als onderdeel van de voortgezette zoek opdracht. De pool bevat nu alle distributie punten van de drie geconfigureerde grens groepen en het laatste distributie punt op de site server. De client gaat vervolgens door met zoeken naar inhoud, waarbij distributie punten elke twee minuten worden gewijzigd totdat de inhoud is gevonden.  

Door de verschillende groepen van de neighbor te configureren die op verschillende tijdstippen beschikbaar moeten zijn, kunt u bepalen wanneer specifieke distributie punten worden toegevoegd als de locatie van de inhouds bron. De client gebruikt terugval voor de standaard site grens groep als een veiligheids-net voor inhoud die niet beschikbaar is op een andere locatie.

## <a name="changes-from-prior-versions"></a>Wijzigingen ten opzichte van eerdere versies

Hieronder vindt u de belangrijkste wijzigingen in grens groepen en hoe clients inhoud vinden in Configuration Manager huidige vertakking. Veel van deze wijzigingen en concepten werken samen.

### <a name="configurations-for-fast-or-slow-are-removed"></a>Configuraties voor snelle of trage verbindingen worden verwijderd

U kunt afzonderlijke distributie punten niet meer configureren om snel of traag te zijn. In plaats daarvan wordt elk site systeem dat is gekoppeld aan een grens groep, op dezelfde manier behandeld. Als gevolg van deze wijziging wordt het tabblad **verwijzingen** van de eigenschappen van de grens groep niet meer ondersteund voor snelle of langzame configuratie.  

### <a name="new-default-boundary-group-at-each-site"></a>Nieuwe standaard grens groep op elke site

Elke primaire site heeft een nieuwe standaard grens groep met de naam **standaard-site-boundary-group &lt;>**. Wanneer een client zich niet op een netwerk locatie bevindt die is toegewezen aan een grens groep, worden de site systemen gebruikt die zijn gekoppeld aan de standaard groep van de toegewezen site. Plan het gebruik van deze grens groep als een vervanging van de locatie van de tijdelijke inhoud van het concept.

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>**Terugval bron locaties voor inhoud toestaan** is verwijderd

U configureert geen expliciet een distributie punt dat voor terugval moet worden gebruikt. De opties voor het configureren van deze instelling worden verwijderd uit de-console.

Daarnaast is het resultaat van de instelling **clients toestaan een terugval bron locatie te gebruiken voor inhoud** van een implementatie type voor toepassingen is gewijzigd. Met deze instelling voor een implementatie type kan een client de standaard site grens groep gebruiken als de locatie van de inhouds bron.

#### <a name="boundary-groups-relationships"></a>Relaties grens groepen

U kunt elke grens groep koppelen aan een of meer extra grens groepen. Deze koppelingen vormen formulier relaties die u configureert op het tabblad nieuwe eigenschappen van grens groep met de naam **relaties**:  

- Elke grens groep waaraan een client rechtstreeks is gekoppeld, wordt een **huidige** grens groep genoemd.  

- Een grens groep die een client kan gebruiken vanwege een koppeling tussen de *huidige* grens groep van die client en een andere groep, wordt een grens groep in de vorm van een **buur** genoemd.  

- Voeg op het tabblad **relaties** de grens groepen toe die u als *een grens* groep wilt gebruiken. Configureer ook een tijd in minuten voor terugval. Wanneer een client geen inhoud kan vinden van een distributie punt in de *huidige* groep, is deze tijd wanneer de client de inhouds locaties van de grens groepen van de *buur* begint te doorzoeken.  

    Wanneer u de configuratie van een grens groep toevoegt of wijzigt, kunt u terugval naar die specifieke grens groep blok keren vanuit de huidige groep die u configureert.  

Als u de nieuwe configuratie wilt gebruiken, definieert u expliciete koppelingen (koppelingen) van de ene grens groep naar een andere. Configureer alle distributie punten in die gekoppelde groep met dezelfde tijd in minuten. Wanneer een client geen inhouds bron van de *huidige* grens groep kan vinden, wordt de tijd die u configureert, bepaald wanneer wordt gezocht naar inhouds bronnen uit de grens groep van de naburige.

Naast de grens groepen die u expliciet configureert, heeft elke grens groep een geïmpliceerde koppeling naar de standaard site grens groep. Deze koppeling wordt na 120 minuten actief. Vervolgens wordt de standaard site grens groep een grens groep in de nabijheid. Dit gedrag stelt de clients in staat om als inhouds bron locaties de distributie punten te gebruiken die zijn gekoppeld aan deze grens groep.

Dit gedrag vervangt wat eerder als terugval voor inhoud werd genoemd. Negeer dit standaard gedrag van 120 minuten door de standaard site grens groep expliciet te koppelen aan een *huidige* groep. Stel een specifieke tijd in minuten in of blok keer terugval volledig om het gebruik ervan te voor komen.

### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>Clients proberen inhoud van elk distributie punt Maxi maal twee minuten op te halen

Wanneer een client zoekt naar een locatie van de inhouds bron, probeert het een distributie punt voor twee minuten te benaderen voordat vervolgens een ander distributie punt wordt uitgevoerd. Dit gedrag is een wijziging ten opzichte van vorige versies waar clients tot Maxi maal twee uur proberen verbinding te maken met een distributie punt.

- Clients selecteren wille keurig het eerste distributie punt uit de groep beschik bare servers in de *huidige* grens groep (of groepen) van de client.  

- Als de-client na twee minuten geen inhoud heeft gevonden, wordt er een nieuw distributie punt geactiveerd en wordt er een poging gedaan om inhoud van die server op te halen. Dit proces wordt elke twee minuten herhaald totdat de client de inhoud heeft gevonden of de laatste server in de groep heeft bereikt.  

- Als een client geen geldige locatie van de inhouds bron van de *huidige* pool kan vinden voordat deze de periode voor terugval naar *een grens* groep in de nabijheid bereikt, voegt de client de distributie punten van die groep *neighbor* toe aan het einde van de huidige lijst. Vervolgens wordt gezocht in de uitgevouwen groep bron locaties die de distributie punten van beide grens groepen bevat.  

    > [!TIP]  
    > Wanneer u een expliciete koppeling van de huidige grens groep naar de standaard site grens groep maakt en een terugval tijd definieert die kleiner is dan de terugval tijd voor een koppeling naar een grens groep in de nabijheid, beginnen clients met het zoeken naar bron locaties vanaf de standaard site grens groep voordat de groep neighbor wordt opgenomen.  

- Wanneer de client geen inhoud kan ophalen van de laatste server in de groep, wordt het proces opnieuw gestart.  

## <a name="see-also"></a>Zie ook

- [Procedures voor grensgroepen](boundary-group-procedures.md)  

- [Over grenzen](boundaries.md)  

- [Basisconcepten voor inhoudsbeheer](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)  

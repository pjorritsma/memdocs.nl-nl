---
title: Orchestration-groepen
titleSuffix: Configuration Manager
description: Maak indelings groepen en implementeer er updates voor.
ms.date: 07/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cddbebea-b418-4839-b0a8-7809486c8a4c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b42a0260b347fb12444e8611e7ec02be38cc387
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088408"
---
# <a name="orchestration-groups-in-configuration-manager"></a>Orchestration-groepen in Configuration Manager
<!--3098816-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Vanaf Configuration Manager versie 2002 kunt u indelings groepen maken. Maak een Orchestration-groep om de implementatie van software-updates op apparaten beter te beheren. Veel server beheerders moeten updates voor specifieke werk belastingen zorgvuldig beheren en het gedrag tussen automatiseren.

Een Orchestration-groep biedt u de flexibiliteit om apparaten bij te werken op basis van een percentage, een specifiek getal of een expliciete volg orde. U kunt ook een Power shell-script uitvoeren voor en nadat de update-implementatie op de apparaten is uitgevoerd.

Leden van een Orchestration-groep kunnen elk Configuration Manager-client zijn, niet alleen servers. De groeps beleidsregels zijn van toepassing op de apparaten voor alle software-update-implementaties voor een verzameling die een groeps groepslid bevat. Andere implementatie gedragingen zijn nog steeds van toepassing. Voor beeld: onderhouds Vensters en implementatie planningen.

> [!NOTE]
> In deze versie van Configuration Manager is Orchestration-groepen een functie van de voorlopige versie. Zie [functies van voorlopige versies](../../core/servers/manage/pre-release-features.md)om deze functie in te scha kelen.  
>
> De functie **Orchestration groups** is de ontwikkeling van de functie [Server groepen](service-a-server-group.md) . Een Orchestration-groep is een object in Configuration Manager.

## <a name="orchestration-group-usage-example"></a>Voor beeld van het gebruik van Orchestration-groep

- Als beheerder van de software-updates beheert u alle updates voor uw organisatie.
- U hebt één grote verzameling voor alle-servers en één grote verzameling voor alle clients. U implementeert alle updates voor deze verzamelingen.
- De SQL-beheerders willen alle software beheren die is geïnstalleerd op de SQL-servers. Ze willen vijf servers in een specifieke volg orde patchen. Het huidige proces is het hand matig stoppen van specifieke services voordat updates worden geïnstalleerd. daarna start u de services daarna opnieuw.
- U maakt een Orchestration-groep en voegt alle vijf SQL-servers toe. U voegt ook pre-en post scripts toe met behulp van de Power shell-scripts van de SQL-beheerders.
- Tijdens de volgende update cyclus maakt en implementeert u de software-updates als normaal voor de grote verzameling van servers. De SQL-beheerders voeren de implementatie uit en de indelings groep automatiseert de volg orde en de services.

## <a name="prerequisites"></a>Vereisten

### <a name="site-server-and-permission-prerequisites"></a>Vereisten voor de site server en de machtiging
- Als u alle Orchestration-groepen en-updates voor die groepen wilt weer geven, moet uw account een **volledige beheerder**zijn.
   - Op rollen gebaseerd beheer voor indelings groepen is op dit moment niet beschikbaar.
- Schakel de functie **Orchestration groups** in. Zie [optionele functies inschakelen](../../core/servers/manage/install-in-console-updates.md#bkmk_options)voor meer informatie.
   - Wanneer u indelings **groepen**inschakelt, schakelt de site de functie **Server groepen** uit. Dit gedrag voor komt conflicten tussen de twee functies.

### <a name="client-prerequisites"></a>Client vereisten

- Voer een upgrade uit voor de doel apparaten naar de nieuwste versie van de Configuration Manager-client.
- Leden van een Orchestration-groep moeten worden toegewezen aan dezelfde site.
- Apparaten kunnen zich niet in meer dan één indelings groep bevallen.
   - Apparaten die al deel uitmaken van een Orchestration-groep zijn niet beschikbaar om te selecteren wanneer nieuwe leden worden toegevoegd.


## <a name="limitations"></a>Beperkingen

- U kunt Maxi maal 1000 Orchestrator-groeps leden hebben.
- Indelings groepen werken niet in de samenwerkings modus. Zie [interoperabiliteit tussen verschillende versies van Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#bkmk_mixed)voor meer informatie. <!--6389000-->
- Als er updates worden geïnitieerd door gebruikers vanuit software Center, wordt de indeling omzeild. <!--6362887-->

## <a name="server-groups-are-automatically-updated-to-orchestration-groups"></a>Server groepen worden automatisch bijgewerkt naar Orchestration-groepen

De functie **Orchestration groups** is de ontwikkeling van de functie [Server groepen](service-a-server-group.md) . Wanneer u Configuration Manager versie 2002 of hoger installeert en Server groepen hebt ingeschakeld, worden uw server groepen automatisch verplaatst naar indelings groepen.

## <a name="create-an-orchestration-group"></a>Een Orchestration-groep maken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **Orchestration-groep** .

1. Selecteer in het lint de optie **Orchestration-groep maken** om de **wizard Orchestration-groep maken**te openen.

1. Geef op de pagina **Algemeen** een **naam** en eventueel een **Beschrijving**op voor de indelings groep. Geef uw waarden op voor de volgende items:
   - **Time-out van Orchestrator-groep (in minuten)**: tijds limiet voor alle groeps leden om de installatie van de update te volt ooien.
   - **Time-out voor het lid van de groeps leden (in minuten)**: de tijds limiet voor één apparaat in de groep om de installatie van de update te volt ooien.

1. Geef op de pagina **lidselectie** de **site code**op. Selecteer vervolgens **toevoegen** om apparaat-resources toe te voegen als leden van deze indelings groep. **Zoek** apparaten op naam en voeg deze vervolgens **toe** . U kunt uw zoek opdracht ook filteren op een enkele verzameling met behulp **van zoeken in verzameling**.  Selecteer **OK** wanneer u klaar bent met het toevoegen van apparaten aan de lijst geselecteerde resources.
   - Wanneer u resources selecteert voor de groep, worden alleen geldige clients weer gegeven. Er worden controles uitgevoerd om de site code te controleren, dat de-client is geïnstalleerd en dat bronnen niet worden gedupliceerd.

1. Selecteer op de pagina **regel selectie** een van de volgende opties:

   - Hiermee **staat u toe dat een percentage van de machines tegelijk wordt bijgewerkt**en selecteert of voert u een getal in voor dit percentage. Gebruik deze instelling om toekomstige flexibiliteit van de indelings groep toe te staan. Uw Orchestration-groep bevat bijvoorbeeld 50-apparaten en u stelt deze waarde in op 10. Tijdens de implementatie van een software-update kunnen met Configuration Manager vijf apparaten gelijktijdig de implementatie uitvoeren. Als u later de grootte van de Orchestration-groep op 100-apparaten verhoogt, worden er vervolgens tien apparaten tegelijk bijgewerkt.

   - **Toestaan dat een aantal machines tegelijk wordt bijgewerkt**en vervolgens een getal selecteren of invoeren voor dit specifieke aantal. Gebruik deze instelling om altijd te beperken tot een specifiek aantal apparaten, ongeacht de totale grootte van de Orchestration-groep.

   - **Geef de onderhouds volgorde**op en sorteer vervolgens de geselecteerde resources in de juiste volg orde. Gebruik deze instelling om de volg orde te bepalen waarin apparaten de implementatie van software-updates uitvoeren.

1. Voer op de pagina **vóór script** een Power shell-script in dat moet worden uitgevoerd op elk apparaat *voordat* de implementatie wordt uitgevoerd. Het script moet de waarde `0` voor geslaagd of `3010` voor geslaagde herstart retour neren.

1. Voer op de pagina **na het script** een Power shell-script in dat moet worden uitgevoerd op elk apparaat *nadat* de implementatie is uitgevoerd en opnieuw opstarten, indien nodig. Het gedrag is anders hetzelfde als het voor-script.

1. Voltooi de wizard.

> [!WARNING]
> Zorg ervoor dat pre-scripts en post scripts worden getest voordat u deze voor Orchestration-groepen gebruikt. De pre-scripts en post scripts zijn niet time-out en worden uitgevoerd totdat de time-out voor de groeps beleidsleden is bereikt.

## <a name="view-orchestration-groups-and-members"></a>Orchestration-groepen en-leden weer geven

Selecteer in de werk ruimte **activa en naleving** het knoop punt **Orchestration-groep** . Als u leden wilt weer geven, selecteert u een Orchestration-groep en selecteert u **leden weer geven** in het lint. Zie [Orchestration-groepen en-leden controleren](#bkmk_orch_monitor)voor meer informatie over de beschik bare kolommen voor de knoop punten.

## <a name="edit-or-delete-an-orchestration-group"></a>Een Orchestration-groep bewerken of verwijderen

Als u de Orchestration-groep wilt verwijderen, selecteert u deze en klikt u vervolgens op **verwijderen** in het lint of in het snelmenu. Als u een Orchestration-groep wilt bewerken, selecteert u deze en klikt u op **Eigenschappen** in het lint of in het snelmenu. Wijzig de instellingen van de volgende tabbladen:

   - **Algemeen**: 
      - **Naam**: de naam van de Orchestration-groep
      - **Beschrijving**: beschrijving van Orchestrator-groep (optioneel)
      - **Time-out van Orchestrator-groep (in minuten)**: tijds limiet voor alle groeps leden om de installatie van de update te volt ooien.
      - **Time-out voor het lid van de groeps leden (in minuten)**: de tijds limiet voor één apparaat in de groep om de installatie van de update te volt ooien.

  - **Lidselectie:**
     - **Site code**: site code voor de Orchestration-groep.
     - **Leden**: Klik op **toevoegen** om extra apparaten voor de Orchestration-groep te selecteren. Klik op **verwijderen** om het geselecteerde apparaat te verwijderen.

   - **Selectie van regels**:
      - Hiermee **staat u toe dat een percentage van de machines tegelijk wordt bijgewerkt**en selecteert of voert u een getal in voor dit percentage. Gebruik deze instelling om toekomstige flexibiliteit van de indelings groep toe te staan. Uw Orchestration-groep bevat bijvoorbeeld 50-apparaten en u stelt deze waarde in op 10. Tijdens de implementatie van een software-update kunnen met Configuration Manager vijf apparaten gelijktijdig de implementatie uitvoeren. Als u later de grootte van de Orchestration-groep op 100-apparaten verhoogt, worden er vervolgens tien apparaten tegelijk bijgewerkt.
      - **Toestaan dat een aantal machines tegelijk wordt bijgewerkt**en vervolgens een getal selecteren of invoeren voor dit specifieke aantal. Gebruik deze instelling om altijd te beperken tot een specifiek aantal apparaten, ongeacht de totale grootte van de Orchestration-groep.
      - **De onderhouds volgorde opgeven**: de geselecteerde resources op de juiste volg orde sorteren. Gebruik deze instelling om de volg orde te bepalen waarin apparaten de implementatie van software-updates uitvoeren.

   - **Pre-script**: 
       - Voer een Power shell-script in dat op elk apparaat wordt uitgevoerd *voordat* de implementatie wordt uitgevoerd. Het script moet de waarde `0` voor geslaagd of `3010` voor geslaagde herstart retour neren.
       
   - **Post-script**:
      - Voer een Power shell-script in dat op elk apparaat moet worden uitgevoerd *nadat* de implementatie is uitgevoerd en dat, indien nodig, opnieuw wordt opgestart. Het script moet de waarde `0` voor geslaagd of `3010` voor geslaagde herstart retour neren.
  
   > [!WARNING]
   > Zorg ervoor dat pre-scripts en post scripts worden getest voordat u deze voor Orchestration-groepen gebruikt. De pre-scripts en post scripts zijn niet time-out en worden uitgevoerd totdat de time-out voor de groeps beleidsleden is bereikt.


## <a name="start-orchestration"></a>Indeling starten

1. [Software-updates implementeren](deploy-software-updates.md) in een verzameling die de leden van de Orchestration-groep bevat.

1. Indeling wordt gestart wanneer een client in de groep elke software-update op deadline of tijdens een onderhouds venster probeert te installeren. Het wordt gestart voor de hele groep en zorgt ervoor dat de apparaten worden bijgewerkt door de groeps regels voor Orchestration te volgen.
1. U kunt de indeling hand matig starten door deze te selecteren in het knoop punt **Orchestration Group** en vervolgens de optie **Orchestration starten** te kiezen vanuit het lint of het snelmenu.
1. Als een Orchestration-groep een *mislukte* status heeft:
   1. Bepaal waarom de Orchestration is mislukt en los eventuele problemen op.
   1. [Stel de Orchestration-status voor groeps leden opnieuw in](#bkmk_reset).
   1. Klik in het knoop punt **Orchestration-groep** op de knop **Orchestration starten** om de indeling opnieuw te starten.
   [![Indeling starten](./media/3098816-start-orchestration.png)](./media/3098816-start-orchestration.png#lightbox)


> [!TIP]
> - Orchestration-groepen zijn alleen van toepassing op implementaties van software-updates. Ze zijn niet van toepassing op andere implementaties.
> - U kunt met de rechter muisknop op een groep van een Orchestrationgroep klikken en **lid van de groep met Orchestrator opnieuw instellen**selecteren. Hierdoor kunt u de indeling opnieuw uitvoeren.


## <a name="monitor-orchestration-groups"></a><a name="bkmk_orch_monitor"></a>Orchestration-groepen bewaken

Selecteer in de werk ruimte **activa en naleving** het knoop punt **Orchestration-groep** . Voeg een van de volgende kolommen toe om informatie over de groepen op te halen:

- **Orchestration-naam**: de naam van uw Orchestration-groep.
- **Site code**: site code voor de groep.
- **Orchestration-type**: is een van de volgende typen:
   - Aantal
   - Percentage
   - Reeks

- Indelings **waarde**: het aantal leden of het percentage van leden dat tegelijkertijd een vergren deling kan krijgen. De **indelings** **waarde** wordt alleen ingevuld wanneer het Orchestration-type *getal* of *percentage*is.  
- Indelings **status**: wordt uitgevoerd tijdens de indeling. Niet-actief wanneer deze niet wordt uitgevoerd.
- **Begin tijd**van de Orchestration: de datum en tijd waarop de Orchestration is gestart.
- **Huidig Volg nummer**: geeft aan waarvoor het lid van de groeps indeling actief is. Dit nummer komt overeen met het **Volg nummer** van het lid.  
- **Orchestration-time-out (in minuten)**: waarde van de indeling van de indelings **groep (in minuten)** die is ingesteld op de pagina **Algemeen** bij het maken van de groep of het tabblad **Algemeen** bij het bewerken van de groep.
- **Time-out van leden van Orchestrator-groep (in minuten)**: waarde van de **time-out van de groeps leden (in minuten)** die is ingesteld op de pagina **Algemeen** bij het maken van de groep of het tabblad **Algemeen** bij het bewerken van de groep.
- Indelings **groep-** id: id van de groep, de id wordt gebruikt in Logboeken en de-data base.
- De unieke id van de indelings **groep**: de unieke id van de groep, de unieke id wordt gebruikt in Logboeken en de data base.

## <a name="monitor-orchestration-group-members"></a>Groeps leden van Orchestrator bewaken

Selecteer een indelings groep in het knoop punt van de **groep met Orchestrator** . Selecteer **leden weer geven**op het lint. U kunt de leden van de groep weer geven en de indelings status ervan. Voeg een van de volgende kolommen toe om informatie over de leden op te halen:

- **Naam**: apparaatnaam van het lid van de groep met Orchestrator
- **Huidige status**: geeft u de status van het apparaat van de gebruiker.
   - Wordt **uitgevoerd** tijdens de indeling.
   - **Wachten**: Hiermee wordt aangegeven dat de client op de vergren deling wacht om updates te installeren.
   - **Niet-actief** wanneer de indeling is voltooid of niet wordt uitgevoerd.
- **Status code**: u kunt met de rechter muisknop op het lid van de groep voor Orchestrator klikken en lid van de **groep van Orchestrator opnieuw instellen**selecteren. Met deze instelling kunt u de indeling opnieuw uitvoeren. Statussen zijn onder andere: 
   - Niet-actief
   - In afwachting van het apparaat wacht op de beurt
   - De installatie van een update wordt uitgevoerd
   - Mislukt
   - Opnieuw opstarten in behandeling
- **Aanschaf tijd vergren deling**: de vergren delingen worden door de client aangevraagd op basis van het bijbehorende beleid. Zodra de client een vergren deling heeft verkregen, wordt de indeling ervan geactiveerd.  
-**Laatste gemelde tijd**: het tijdstip waarop het lid het laatst een status heeft gemeld.
- **Volg nummer**: de locatie van de client in de wachtrij voor het installeren van updates.
- **Site code**: de site code voor het lid.
- **Client activiteit**: geeft aan of de client actief of niet actief is.
- **Primaire gebruiker (s)**: welke gebruikers primair zijn voor het apparaat.
- **Client type**: het type apparaat dat de client is.
- **Gebruiker die momenteel is aangemeld**: de gebruiker die momenteel is aangemeld bij het apparaat.
- **Ogboek-id**: id van de Orchestration-groep waartoe het lid behoort.
- **Unieke id van ogboek**: de unieke id van de Orchestration-groep waartoe het lid behoort.
- **Resource-id**: bron-id van het apparaat.

## <a name="reset-the-orchestration-state-for-a-group-member"></a><a name="bkmk_reset"></a>De Orchestration-status voor een groepslid opnieuw instellen

Als u de indeling opnieuw wilt uitvoeren op een groepslid, kunt u de status wissen, zoals *volledig* of *mislukt*. Als u de status wilt wissen, klikt u met de rechter muisknop op het lid van de groep voor de Orchestrator en selecteert u lid van de **groep Orchestrator instellen**. U kunt ook klikken op **groeps Beleidslid opnieuw instellen** op het lint. Voordat u de status opnieuw instelt, moet u de client controleren om te zien waarom deze is mislukt en de gevonden problemen te verhelpen.
   [![Lid van Orchestrator-groep opnieuw instellen](./media/3098816-reset-group-member.png)](./media/3098816-reset-group-member.png#lightbox)

## <a name="log-files"></a>Logboekbestanden

Gebruik de volgende logboek bestanden op de site server om te controleren en problemen op te lossen:

### <a name="site-server"></a>Siteserver

- **Policypv. log**: hier wordt weer gegeven dat de site de Orchestration-groep aan de clients streeft.
- **SMS_OrchestrationGroup. log**: toont het gedrag van de Orchestration-groep.

### <a name="client"></a>Client

- **MaintenanceCoordinator. log**: hier ziet u de vergren deling, update-installatie, pre-en post-scripts en het vergrendelings proces.
- **UpdateDeployment. log**: toont het installatie proces van de update.
- **Policy Agent. log**: controleert of de client zich in een Orchestration-groep bevindt.

## <a name="next-steps"></a>Volgende stappen

[Software-updates implementeren](deploy-software-updates.md)
---
title: Wake on LAN configureren
titleSuffix: Configuration Manager
description: Selecteer Wake On LAN instellingen in Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dcf6005d0364106df8717a1151dbad617e455ff9
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127032"
---
# <a name="how-to-configure-wake-on-lan-in-configuration-manager"></a>Wake on LAN configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Geef de instellingen voor Wake on LAN voor Configuration Manager op wanneer u computers uit de slaap stand wilt halen.

## <a name="wake-on-lan-starting-in-version-1810"></a><a name="bkmk_wol-1810"></a>Wake-on-LAN vanaf versie 1810
<!--3607710-->
Vanaf Configuration Manager 1810 is er een nieuwe manier om slapende computers te activeren. U kunt clients uit de Configuration Manager-console ontwaken, zelfs als de client zich niet in hetzelfde subnet bevindt als de site server. Als u onderhoud of query apparaten wilt uitvoeren, bent u niet beperkt door externe clients die in de slaap stand zijn. De site server maakt gebruik van het kanaal voor client meldingen om andere clients te identificeren die zich in hetzelfde externe subnet bevinden. vervolgens worden deze clients gebruikt om een Wake on LAN-aanvraag (Magic Packet) te verzenden. Met behulp van het kanaal voor client meldingen voor komt u dat MAC-kleppen worden afgesloten. Dit kan ertoe leiden dat de poort wordt uitgeschakeld door de router. De nieuwe versie van Wake on LAN kan op hetzelfde moment als de [oudere versie](#bkmk_wol-previous)worden ingeschakeld.

### <a name="limitations"></a>Beperkingen
<!--7323898, 7363492-->
- Ten minste één client in het doel-subnet moet actief zijn.
- Deze functie biedt geen ondersteuning voor de volgende netwerk technologieën:
   - IPv6
   - 802.1 x-netwerk verificatie
    >[!NOTE]
    > 802.1 x-netwerk verificatie kan met aanvullende configuratie worden uitgevoerd, afhankelijk van de hardware en de configuratie.
- Machines die alleen worden geactiveerd wanneer u via de **Wake-up** -client melding op de hoogte wordt gebracht.
    - Voor wake-up wanneer er een deadline optreedt, wordt de oudere versie van Wake on LAN gebruikt.
    -  Als de oudere versie niet is ingeschakeld, treedt de client niet meer op voor implementaties die zijn gemaakt met de instellingen **Wake-on-LAN gebruiken om clients te laten ontwaken voor vereiste implementaties of voor** het **verzenden van Ontwaak pakketten**.  

### <a name="security-role-permissions"></a>Machtigingen voor beveiligings rollen

- **Resource informeren** onder de verzamelings categorie

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>De clients configureren voor het gebruik van Wake on LAN vanaf versie 1810

Voorheen moest u de client voor Wake on LAN hand matig inschakelen in de eigenschappen van de netwerk adapter. Configuration Manager 1810 bevat een nieuwe client instelling met de naam **netwerk Wake-up toestaan**. Configureer en implementeer deze instelling in plaats van de eigenschappen van de netwerk adapter te wijzigen.

1. Onder **beheer**gaat u naar **client instellingen**.
1. Selecteer de client instellingen die u wilt bewerken of maak nieuwe aangepaste client instellingen om te implementeren. Zie [client instellingen configureren](configure-client-settings.md)voor meer informatie.
1. Selecteer op de client instellingen voor **energie beheer** **inschakelen** voor de instelling **netwerk Wake-up toestaan** . Zie [over client instellingen](about-client-settings.md#power-management)voor meer informatie over deze instelling.

4. Vanaf Configuration Manager 1902 is de nieuwe versie van Wake on LAN van kracht op de aangepaste UDP-poort die u opgeeft voor de [client instelling](about-client-settings.md#power-management)voor **Wake on LAN poort nummer (UDP)** . Deze instelling wordt gedeeld door de nieuwe en oudere versie van Wake on LAN.
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>Een client activeren met behulp van client melding vanaf 1810
 
U kunt één client of slapende clients in een verzameling activeren. Voor apparaten die zich al in de verzameling bevinden, wordt er geen actie ondernomen. Alleen clients die in de slaap stand worden geplaatst, krijgen een aanvraag voor Wake on LAN. Zie [client melding](../manage/client-notification.md)voor meer informatie over het melden van een client aan Wake.

- **Eén client activeren:** Klik met de rechter muisknop op de client, ga naar **client melding**en selecteer **Wake up**.

   ![Client melding activeren in de console](media/wol-wake-up-client-notification.png)

- **Alle slapende clients in een verzameling activeren:** Klik met de rechter muisknop op de verzameling apparaten, ga naar **client melding**en selecteer **Wake up**.
   - Deze actie kan niet worden uitgevoerd op ingebouwde verzamelingen.
   - Wanneer u een combi natie van slaap stand en aanwakkerde clients in een verzameling hebt, worden alleen de clients die in de slaap blijven, een Wake on LAN-aanvraag verzonden.
   - Vanaf Configuration Manager 2002 is deze actie beschikbaar vanuit een-console die is verbonden met een centrale beheer site, een zelfstandige site of een onderliggende primaire site.
   - In versie 1910 en eerder is deze actie alleen actief wanneer de Configuration Manager-console is verbonden met een zelfstandige of onderliggende primaire site. Als er verbinding is met een centrale beheer site, is de actie niet beschikbaar.

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>Wat u kunt verwachten wanneer alleen de nieuwe versie van Wake on LAN is ingeschakeld

Wanneer u alleen de nieuwe versie van Wake on LAN ingeschakeld hebt, wordt alleen de **Wake-up** -client melding ingeschakeld. Clients verzenden geen meldingen wanneer een deadline wordt ontvangen voor implementaties zoals taken reeksen, software distributie of installatie van software-updates. Zodra een slapende computer weer online is, wordt deze in de-console weer gegeven wanneer deze wordt ingecheckt met het beheer punt.

Vanaf Configuration Manager versie 1902 kunt u de Wake on LAN-poort opgeven. Deze instelling wordt gedeeld door de nieuwe en oudere versie van Wake on LAN.

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>Wat u kunt verwachten wanneer beide versies van Wake on LAN zijn ingeschakeld

Wanneer u beide versies van Wake on LAN hebt ingeschakeld, kunt u de melding client **ontwaken** en activeren na deadline gebruiken. De client melding werkt iets anders dan traditionele Wake on LAN. Zie de sectie [Wake-on-LAN starten in versie 1810](#bkmk_wol-1810) voor een korte uitleg van de werking van de client melding. Met de nieuwe client instelling **netwerk Wake-up toestaan** worden de NIC-eigenschappen gewijzigd om Wake on LAN toe te staan. U hoeft deze niet meer hand matig te wijzigen voor nieuwe machines die aan uw omgeving worden toegevoegd. Alle andere functionaliteit van Wake on LAN is niet gewijzigd.

Vanaf versie 1902 van de **Wake-up** -client wordt de huidige instelling voor het **Wake on LAN poort nummer (UDP)** nageleefd.


## <a name="wake-on-lan-for-version-1806-and-earlier"></a><a name="bkmk_wol-previous"></a>Wake on LAN voor versie 1806 en lager

Geef de instellingen voor Wake on LAN voor Configuration Manager op wanneer u computers uit de slaap stand wilt halen om de vereiste software te installeren, zoals software-updates, toepassingen, taken reeksen en Program ma's.

U kunt Wake on LAN aanvullen door gebruik te maken van de client instellingen voor wake-up proxy. Als u Wake-up proxy wilt gebruiken, moet u echter eerst Wake on LAN inschakelen voor de site en **alleen Ontwaak pakketten** opgeven en de optie **unicast** voor de methode Wake on LAN-verzen ding. Deze Ontwaak oplossing biedt ook ondersteuning voor ad-hoc-verbindingen, zoals een verbinding met een extern bureau blad.

Gebruik de eerste procedure om een primaire site te configureren voor Wake on LAN. Gebruik vervolgens de tweede procedure voor het configureren van de client instellingen voor wake-up proxy. Met deze tweede procedure configureert u de standaard client instellingen voor de Wake-up proxy-instellingen die moeten worden toegepast op alle computers in de hiërarchie. Als u wilt dat deze instellingen alleen van toepassing zijn op geselecteerde computers, maakt u een aangepaste apparaat-instelling en wijst u deze toe aan een verzameling die de computers bevat die u wilt configureren voor wake-up proxy. Zie [client instellingen configureren](../../../core/clients/deploy/configure-client-settings.md)voor meer informatie over het maken van aangepaste client instellingen.

Een computer die de client instellingen voor wake-up proxy ontvangt, onderbreekt waarschijnlijk de netwerk verbinding gedurende 1-3 seconden. Dit komt doordat de client de netwerk interface kaart opnieuw moet instellen om het stuur programma voor wake-up proxy in te scha kelen.

> [!WARNING]
> Om onverwachte onderbreking van uw netwerk services te voor komen, moet u eerst de Wake-up proxy in een geïsoleerde en representatieve netwerk infrastructuur evalueren. Gebruik vervolgens aangepaste client instellingen om uw test uit te breiden naar een geselecteerde groep computers op verschillende subnetten. Zie [plan How to wake up clients](../../../core/clients/deploy/plan/plan-wake-up-clients.md)(Engelstalig) voor meer informatie over de werking van Wake-up proxy.


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>Wake on LAN configureren voor een site voor versie 1806 en lager

 Als u Wake on LAN wilt gebruiken, moet u dit inschakelen voor elke site in een hiërarchie.

1. Ga in de Configuration Manager-console naar **beheer > site configuratie > sites**.
2. Klik op de primaire site die u wilt configureren en klik vervolgens op **Eigenschappen**.
3. Klik op het tabblad **Wake-on-LAN** en configureer de opties die u nodig hebt voor deze site. Als u Wake-up proxy wilt ondersteunen, moet u ervoor zorgen dat u **alleen Ontwaak pakketten gebruiken** en **unicast**selecteert. Zie [plan How to wake up clients](../../../core/clients/deploy/plan/plan-wake-up-clients.md)(Engelstalig) voor meer informatie.
4. Klik op **OK** en herhaal de procedure voor alle primaire sites in de hiërarchie.

![Wake On LAN in de site-eigenschappen inschakelen](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>Client instellingen voor wake-up proxy configureren

1. Ga in de Configuration Manager-console naar **beheer > client instellingen**.
2. Klik op **standaard client instellingen**en klik vervolgens op **Eigenschappen**.
3. Selecteer **energie beheer** en kies vervolgens **Ja** om **Wake-up proxy in te scha kelen**.
4. Controleer en configureer zo nodig de andere instellingen voor wake-up proxy. Zie [instellingen voor energie beheer](../../../core/clients/deploy/about-client-settings.md#power-management)voor meer informatie over deze instellingen.
5. Klik op **OK** om het dialoog venster te sluiten en klik vervolgens op **OK** om het dialoog venster standaard client instellingen te sluiten.

U kunt de volgende Wake On LAN-rapporten gebruiken om de installatie en configuratie van Wake-up proxy te bewaken:

- Samenvatting van implementatiestatus van Wake-up proxy
- Details van implementatiestatus van Wake-up proxy

> [!TIP]
> Als u wilt testen of wake-up proxy werkt, test u een verbinding met een computer in de slaap stand. Maak bijvoorbeeld verbinding met een gedeelde map op die computer of probeer verbinding te maken met de computer met behulp van Extern bureaublad. Als u directe toegang gebruikt, controleert u of de IPv6-voor voegsels werken door dezelfde tests uit te voeren voor een slapende computer die momenteel op internet is.

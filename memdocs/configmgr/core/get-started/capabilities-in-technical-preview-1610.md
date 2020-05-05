---
title: Mogelijkheden van Technical Preview 1610
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1610.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 6402205ae694d719845492b1af37000a0b9335c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721470"
---
# <a name="capabilities-in-technical-preview-1610-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1610 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*



Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1610. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site.      Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filteren op inhouds grootte in regels voor automatische implementatie
U kunt nu filteren op de inhouds grootte voor software-updates in regels voor automatische implementatie. U kunt bijvoorbeeld het filter voor **inhouds grootte (KB)** instellen op **< 2048** om alleen software-updates te downloaden die kleiner zijn dan 2 MB. Als u dit filter gebruikt, voor komt u dat grote software-updates automatisch worden gedownload voor een betere ondersteuning van vereenvoudigde Windows-onderhoud op lagere niveaus wanneer de netwerk bandbreedte beperkt is. Zie [Configuration Manager en vereenvoudigd Windows-onderhoud op besturings systemen van lagere niveaus](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)voor meer informatie.

#### <a name="to-configure-the-content-size-field"></a>Het veld inhouds grootte configureren
Als u het veld **inhouds grootte (KB)** wilt configureren, gaat u naar de pagina **software-updates** in de wizard regel voor automatische implementatie maken wanneer u een ADR maakt of gaat u naar het tabblad software- **updates** in de eigenschappen voor een bestaande ADR.

![Veld voor inhouds grootte](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Verbeterde functionaliteit voor het dialoog venster vereiste software
Wanneer een gebruiker de vereiste software ontvangt, van de instelling **uitstellen en herinneren:** , kunnen ze in de volgende vervolg keuzelijst met waarden selecteren:
- Later: geeft aan dat meldingen worden gepland op basis van de instellingen voor meldingen die zijn geconfigureerd in de instellingen van de client agent.
- Vaste tijd: Hiermee geeft u op dat de melding moet worden weer gegeven na de geselecteerde tijd. Als een gebruiker bijvoorbeeld 30 minuten selecteert, wordt de melding over 30 minuten weer gegeven.

![Pagina computer agent in instellingen van client agent](media/computeragentsettings.png)

De maximale uitstel tijd is altijd gebaseerd op de meldings waarden die zijn geconfigureerd in de instellingen van de client agent op elke keer via de implementatie tijdlijn. Als de deadline van de **implementatie meer dan 24 uur is, herinnert u gebruikers elke (uren)** instelling op de pagina computer agent is 10 uur lang en is deze meer dan 24 uur vóór de deadline wanneer het dialoog venster wordt gestart. de gebruiker wordt weer gegeven met een set opties voor uitstellen, maar nooit langer dan 10 uur. Naarmate de deadline nadert, worden in het dialoog venster minder opties weer gegeven, consistent met de relevante instellingen van de client agent voor elk onderdeel van de implementatie tijdlijn.

Daarnaast is er voor een implementatie met een hoog risico, zoals een taken reeks die een besturings systeem implementeert, de melding van de eind gebruiker nu meer in de praktijk. In plaats van een waarschuwing op de taak balk wordt elke keer dat de gebruiker wordt gewaarschuwd dat essentieel software onderhoud vereist is, een dialoog venster zoals het volgende wordt weer gegeven op de computer van de gebruiker:

![Dialoog venster vereiste software](media/requiredsoftwaredialog.png)


Voor meer informatie:
- [Instellingen voor het beheren van implementaties met een hoog risico](../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Clientinstellingen configureren](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Eerder goedgekeurde toepassings aanvragen weigeren

Als beheerder kunt u nu een eerder goedgekeurde toepassings aanvraag weigeren. Zodra de toepassing is geweigerd, moeten gebruikers de aanvraag later opnieuw verzenden. Met de weigering wordt de toepassing niet verwijderd. in plaats daarvan wordt het opnieuw goed keuren afgedwongen voor elke nieuwe aanvraag voor die toepassing van die gebruiker. Voorheen was toepassings aanvraag weigering alleen beschikbaar voor toepassings aanvragen die niet zijn goedgekeurd.

#### <a name="try-it-out"></a>Uitproberen
Een door een toepassing goedgekeurde aanvraag weigeren:

1. In de Configuration Manager-console [maakt en implementeert u een toepassing](../../apps/deploy-use/create-applications.md) waarvoor goed keuring is vereist.
2. Open Software Center op een client computer en dien een aanvraag in voor de toepassing.
3. In de Configuration Manager-console keurt u de toepassings aanvraag goed.
4. De goedgekeurde toepassings aanvraag weigeren: in de Configuration Manager-console navigeert u in het**overzicht** > van de **software bibliotheek** > op**toepassings beheer** > **goedkeurings aanvragen** en selecteert u de toepassings aanvraag die u wilt weigeren.  Klik op het lint op **weigeren**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Clients uitsluiten van automatische upgrade
Technical Preview 1610 introduceert een nieuwe instelling die u kunt gebruiken om een verzameling clients te uitsluiten van de automatische installatie van bijgewerkte client versies.  Dit geldt voor automatische upgrades en andere methoden, zoals upgrades op basis van software-updates, aanmeldings scripts en groeps beleid. Dit kan worden gebruikt voor een verzameling computers die meer aandacht nodig hebben bij het upgraden van de client. Een client die zich in een uitgesloten verzameling bevindt, negeert aanvragen om bijgewerkte client software te installeren.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Uitsluiting van automatische upgrade configureren
Automatische uitsluitingen voor upgrades configureren:
1. Open in de Configuration Manager-console **hiërarchie-instellingen** onder **beheer > site configuratie > sites**en selecteer vervolgens het tabblad **client upgrade** .
2. Schakel het selectie vakje **in voor het uitsluiten van de opgegeven clients uit de upgrade**en selecteer vervolgens **de verzameling die**u wilt uitsluiten. U kunt slechts één verzameling voor uitsluiting selecteren.
3. Klik op **OK** om de configuratie te sluiten en op te slaan. Na het bijwerken van het beleid voor clients in de uitgesloten verzameling worden updates voor de client software niet meer automatisch geïnstalleerd.

   ![Instellingen voor automatische upgrade uitsluiting](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Hoewel in de gebruikers interface wordt aangegeven dat clients niet via een methode worden bijgewerkt, zijn er twee methoden die u kunt gebruiken om deze instellingen te overschrijven. Client push installatie en een hand matige client installatie kunnen worden gebruikt om deze configuratie te onderdrukken. Zie de volgende sectie voor meer informatie.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Een upgrade uitvoeren van een client die zich in een uitgesloten verzameling bevindt
Zolang een verzameling is geconfigureerd om te worden uitgesloten, kunnen leden van die verzameling alleen hun client software upgraden met een van de twee methoden, waardoor de uitsluiting wordt overschreven:
- **Push-client installatie** : u kunt Push-client installatie gebruiken om een client in een uitgesloten verzameling bij te werken. Dit is toegestaan omdat deze wordt beschouwd als het doel van de beheerder en u in staat stelt om clients te upgraden zonder de volledige verzameling uit de uitsluiting te verwijderen.       
- **Hand matige client installatie** : u kunt clients die zich in een uitgesloten verzameling bevinden, hand matig bijwerken wanneer u de volgende opdracht regel optie gebruikt met ccmsetup: ***/ignoreskipupgrade***

  Als u probeert een client die lid is van de uitgesloten verzameling hand matig te upgraden en deze switch niet gebruikt, zal de client de nieuwe client software niet installeren. Zie [Configuration Manager-clients hand matig installeren](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)voor meer informatie.

Zie [clients implementeren op Windows-computers](../clients/deploy/deploy-clients-to-windows-computers.md)voor meer informatie over client installatie methoden.

## <a name="windows-defender-configuration-settings"></a>Configuratie-instellingen voor Windows Defender

U kunt nu Windows Defender-client instellingen configureren op door intune Inge schreven Windows 10-computers met configuratie-items in de Configuration Manager-console.

U kunt met name de volgende instellingen voor Windows Defender configureren:
- Real-timecontrole toestaan
- Gedragscontrole toestaan
- Systeem voor netwerkinspectie inschakelen
- Alle downloads scannen
- Scannen van scripts toestaan
- Activiteiten van bestanden en programma's bewaken
  - Bewaakte bestanden
- Dagen om opgeloste problemen met malware bij te houden
- Toegang tot gebruikersinterface van client toestaan
- Een systeemscan plannen
  - Geplande dag
  - Geplande tijd
- Een dagelijkse snelle scan plannen
  - Geplande tijd
- Het CPU-gebruik% beperken tijdens de archief bestanden voor scan scans
- E-mailberichten scannen
- Verwisselbare stations scannen
- Toegewezen stations scannen
- Bestanden scannen die zijn geopend vanuit net shares
- Update-interval voor handtekeningen
- Cloudbeveiliging toestaan
- Gebruikers vragen om voor beelden
- Detectie van mogelijk ongewenste toepassingen
- Uitgesloten bestanden/mappen
- Uitgesloten bestands extensies
- Uitgesloten processen

> [!NOTE]
> Deze instellingen kunnen alleen worden geconfigureerd op client computers met Windows 10 november update (1511) en hoger.

### <a name="try-it-out"></a>Probeer het nu!

1. Ga in de Configuration Manager-console naar **activa en naleving** > **overzicht** > **configuratie-items**voor**compatibiliteits instellingen** > en maak een nieuw **configuratie-item**.
2. Voer een naam in en selecteer **windows 8,1 en Windows 10** onder **instellingen voor apparaten die worden beheerd zonder de Configuration Manager-client** en klik op **volgende**.
3. Zorg ervoor dat **alle Windows 10-(64-bits)** en **alle windows 10 (32-bits)** zijn geselecteerd op de pagina **ondersteunde platforms** en klik vervolgens op **volgende**.
4. Selecteer de instellings groep **Windows Defender** en klik vervolgens op **volgende**.
5. Configureer de gewenste instellingen op deze pagina en klik vervolgens op **volgende**.
6. Voltooi de wizard.
7. Voeg dit configuratie-item toe aan een configuratie basislijn en implementeer deze basis lijn op computers met Windows 10 november update (1511) of hoger.

> [!NOTE]
> Vergeet niet om het selectie vakje niet- **compatibele instellingen herstellen** bij het implementeren van de configuratie basislijn in te scha kelen.

## <a name="request-policy-sync-from-administrator-console"></a>Synchronisatie van aanvragen beleid van de Administrator-console

U kunt nu een beleids synchronisatie aanvragen voor een mobiel apparaat vanuit de Configuration Manager-console, in plaats van dat u een synchronisatie van het apparaat zelf wilt aanvragen. Informatie over de status van de synchronisatie aanvraag is beschikbaar als een nieuwe kolom in apparaat weergaven, de **externe synchronisatie status**genoemd. De status wordt ook weer gegeven in de sectie **detectie gegevens** van het dialoog venster **Eigenschappen** voor elk mobiel apparaat.

### <a name="try-it-out"></a>Probeer het nu!

1. Ga in de Configuration Manager-console naar **activa en naleving** > **overzicht** > apparaten.
2. Selecteer in het menu **acties voor externe apparaten** de optie **synchronisatie aanvraag verzenden**.

De synchronisatie kan vijf tot tien minuten duren. Eventuele wijzigingen in het beleid worden gesynchroniseerd met het apparaat. U kunt de status van de synchronisatie aanvraag volgen in de kolom **externe synchronisatie status** in de weer gave **apparaten** of in het dialoog venster **Eigenschappen** van het apparaat.

## <a name="additional-security-role-support"></a>Aanvullende ondersteuning voor beveiligings rollen

Naast de volledige beheerder hebben de volgende ingebouwde beveiligings rollen nu volledige toegang tot items in het knoop punt **alle apparaten in bedrijfs eigendom** , inclusief vooraf **gedeclareerde apparaten**, **IOS-inschrijvings profielen**en **Windows-inschrijvings profielen**:
- **Asset Intelligence-beheerder**
- **Toegangs beheer voor bedrijfs bronnen**

Alleen-lezen toegang tot deze gebieden van de Configuration Manager-console wordt nog steeds verleend aan de rol **alleen-lezen analist** .

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Voorwaardelijke toegang voor Windows 10 VPN-profielen

U kunt nu vereisen dat Windows 10-apparaten die zijn Inge schreven in Azure Active Directory voldoen aan de vereisten voor VPN-toegang via Windows 10 VPN-profielen die zijn gemaakt in de Configuration Manager-console. Dit is mogelijk via het selectie vakje nieuwe **voorwaardelijke toegang inschakelen voor deze VPN-verbinding** op de pagina **verificatie methode** van de wizard VPN-profiel en VPN-profiel eigenschappen voor Windows 10 VPN-profielen. U kunt ook een afzonderlijk certificaat opgeven voor verificatie van eenmalige aanmelding als u voorwaardelijke toegang inschakelt voor het profiel.

## <a name="see-also"></a>Zie ook
[Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md)

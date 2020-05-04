---
title: BitLocker-rapporten weergeven
titleSuffix: Configuration Manager
description: Meer informatie over de BitLocker-beheer rapporten in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0bae9477-0500-41cf-8aa3-5e6efadd0554
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d10717f980922e1f6d1fca9224e288b4df709da2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717354"
---
# <a name="view-bitlocker-reports"></a>BitLocker-rapporten weergeven

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3601034-->

Nadat u [de rapporten](setup-websites.md) op het Reporting Services-punt hebt geïnstalleerd, kunt u de rapporten weer geven. De rapporten tonen de compatibiliteit van BitLocker voor de onderneming en voor afzonderlijke apparaten. Ze bevatten tabellaire informatie en grafieken en bevatten filters waarmee u gegevens uit verschillende perspectieven kunt bekijken.

Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **rapportage**uit en selecteer het knoop punt **rapporten** . De volgende rapporten bevinden zich in de categorie voor **BitLocker-beheer** :

- [Naleving van BitLocker-computer](#bkmk-compliancereport)

- [Dash board voor naleving van BitLocker-bedrijfs vereisten](#bkmk-dashboard)

- [Details van de naleving van BitLocker-onderneming](#bkmk-compliancedetails)

- [Overzicht van BitLocker Enter prise-naleving](#bkmk-compliancesummary)

- [Controle rapport voor herstel](#bkmk-audit)

U kunt al deze rapporten rechtstreeks openen via de website van het Reporting Services-punt.

> [!NOTE]
> Als u wilt dat deze rapporten volledige gegevens weer geven:
>
> - Een BitLocker-beheer beleid maken en implementeren in een apparaat verzameling
> - Clients in de doel verzameling moeten de hardware-inventaris verzenden

## <a name="bitlocker-computer-compliance"></a><a name="bkmk-compliancereport"></a>Naleving van BitLocker-computer

Gebruik dit rapport om informatie te verzamelen die specifiek is voor een computer. Het bevat gedetailleerde versleutelings informatie over het station van het besturings systeem en eventuele vaste gegevens stations. Als u de details van elk station wilt weer geven, vouwt u de vermelding voor de computer naam uit. Ook wordt het beleid aangegeven dat wordt toegepast op elk schijf type op de computer.

[![Voor beeld van een scherm opname van het rapport met BitLocker-computer naleving](media/bitlocker-computer-compliance.png)](media/bitlocker-computer-compliance.png#lightbox)

U kunt dit rapport ook gebruiken om de laatst bekende BitLocker-versleutelings status van verloren of gestolen computers te bepalen. Configuration Manager bepaalt de naleving van het apparaat op basis van de BitLocker-beleids regels die u implementeert. Voordat u probeert de BitLocker-versleutelings status van een apparaat te bepalen, controleert u het beleid dat u hebt geïmplementeerd.

> [!NOTE]
> In dit rapport wordt de versleutelings status van Verwissel bare gegevens volumes niet weer gegeven.

### <a name="computer-details"></a>Computer Details

|Kolom&nbsp;naam|Beschrijving|
|----------------|----|
|Computernaam|Door de gebruiker opgegeven naam van de DNS-computer.|
|Domeinnaam|De volledig gekwalificeerde domein naam voor de computer.|
|Computer type|Type computer, geldige typen zijn **niet-draagbaar** en **draagbaar**.|
|Besturingssysteem|Type besturings systeem van de computer.|
|Algemene naleving|Algemene BitLocker-compatibiliteits status van de computer. Geldige statussen zijn **compatibel** met en **niet-compatibel**. De [nalevings status per schijf](#bkmk_volume) kan duiden op verschillende nalevings Staten. Dit veld vertegenwoordigt echter de nalevings status van het opgegeven beleid.|
|Compatibiliteit van besturings systeem|Nalevings status van het besturings systeem op de computer. Geldige statussen zijn **compatibel** met en **niet-compatibel**.|
|Naleving van vast gegevens station|Nalevings status van een vast gegevens station op de computer. Geldige statussen zijn **compatibel** met en **niet-compatibel**.|
|Datum van de laatste update|De datum en tijd waarop de computer voor het laatst contact heeft gemaakt met de server om de nalevings status te rapporteren.|
|Gesteld|Hiermee wordt aangegeven of de gebruiker wordt uitgesloten van het BitLocker-beleid of niet is uitgesloten.|
|Uitgesloten gebruiker|De gebruiker die niet is uitgesloten van het BitLocker-beleid.|
|Datum van uitzonde ring|De datum waarop de uitzonde ring is verleend.|
|Details van nalevings status|Fout-en status berichten over de nalevings status van de computer uit het opgegeven beleid.|
|Sterkte van beleids versleuteling|De coderings sterkte die u hebt geselecteerd in het beleid voor BitLocker-beheer.|
|Beleid: station van het besturings systeem|Hiermee wordt aangegeven of versleuteling is vereist voor het station van het besturings systeem en het juiste beveiligings type.|
|Beleid: vast gegevens station|Hiermee wordt aangegeven of versleuteling is vereist voor de vaste schijf.|
|Fabrikant|De naam van de computer fabrikant zoals deze wordt weer gegeven in het BIOS van de computer.|
|Model|De naam van het computer fabrikant model zoals deze wordt weer gegeven in het BIOS van de computer.|
|Gebruikers van het apparaat|Bekende gebruikers op de computer.|

### <a name="computer-volume"></a><a name="bkmk_volume"></a>Computer volume

|Kolom&nbsp;naam|Beschrijving|
|----------------|----|
|Stationsletter|De stationsletter van de computer.|
|Type station|Type station. Geldige waarden zijn het station van het **besturings systeem** en het **station met vaste gegevens**. Deze vermeldingen zijn fysieke stations in plaats van logische volumes.|
|Codeer sterkte|De coderings sterkte die u hebt geselecteerd in het beleid voor BitLocker-beheer.|
|Beveiligings typen|Type Protector dat u hebt geselecteerd in het beleid om het station te versleutelen. De geldige beveiligings typen voor een OS-station zijn **TPM** of **TPM + pincode**. Het geldige beveiligings type voor een vaste gegevens schijf is een **wacht woord**.|
|Status van beveiliging|Geeft aan dat het beveiligings type dat is opgegeven in het beleid is ingeschakeld op de computer. De geldige statussen zijn **in** -of **uitgeschakeld**.|
|Versleutelings status|Versleutelings status van het station. Geldige statussen zijn **versleuteld**, **niet versleuteld**of **versleuteld**.|

## <a name="bitlocker-enterprise-compliance-dashboard"></a><a name="bkmk-dashboard"></a>Dash board voor naleving van BitLocker-bedrijfs vereisten

Dit rapport bevat de volgende grafieken, waarin de nalevings status van BitLocker in uw organisatie wordt weer gegeven:

- Distributie status van naleving

- Distributie met niet-compatibele fouten

- Distributie status van naleving per schijf type

[![Voor beeld van een scherm opname van het dash board BitLocker Enter prise naleving](media/bitlocker-enterprise-compliance-dashboard.png)](media/bitlocker-enterprise-compliance-dashboard.png#lightbox)

### <a name="compliance-status-distribution"></a>Distributie status van naleving

In dit cirkel diagram wordt de nalevings status weer gegeven voor computers in de organisatie. Ook wordt het percentage computers met die nalevings status weer gegeven, vergeleken met het totale aantal computers in de geselecteerde verzameling. Het werkelijke aantal computers met elke status wordt ook weer gegeven.

In het cirkel diagram worden de volgende nalevings statussen weer gegeven:

- Compatibel

- Niet-compatibel

- Gebruiker uitgezonderd

- Tijdelijke gebruikers uitsluiting

- Beleid niet afgedwongen

- Onbekend. Deze computers hebben een status fout gerapporteerd, of ze deel uitmaken van de verzameling, maar hebben nog nooit hun nalevings status gerapporteerd. Het ontbreken van een nalevings status kan optreden als de verbinding van de computer met de organisatie is verbroken.

### <a name="non-compliant---errors-distribution"></a>Distributie met niet-compatibele fouten

Dit cirkel diagram toont de categorieën computers in uw organisatie die niet compatibel zijn met het BitLocker-stationsversleuteling-beleid. Ook wordt het aantal computers in elke categorie weer gegeven. Het rapport berekent elk percentage van het totale aantal niet-conforme computers in de verzameling.

- Door de gebruiker uitgestelde versleuteling

- Kan geen compatibele TPM vinden

- Systeem partitie niet beschikbaar of groot genoeg

- TPM is zichtbaar maar niet geïnitialiseerd

- Beleids conflict

- Wachten op het automatisch inrichten van de TPM

- Er is een onbekende fout opgetreden

- Geen informatie. Op deze computers is de BitLocker-beheer agent niet geïnstalleerd of geïnstalleerd, maar niet geactiveerd. De service werkt bijvoorbeeld niet.

### <a name="compliance-status-distribution-by-drive-type"></a>Distributie status van naleving per schijf type

In dit staaf diagram wordt de huidige BitLocker-nalevings status weer gegeven op schijf type. De statussen zijn **compatibel** en **niet-compatibel**. Balken worden weer gegeven voor harde schijven en stations met een besturings systeem. Het rapport bevat computers zonder een vaste gegevens schijf en bevat alleen een waarde in de station balk van het **besturings systeem** . De grafiek bevat geen gebruikers die een uitzonde ring hebben gekregen van het BitLocker-stationsversleuteling beleid of de categorie geen beleid.

## <a name="bitlocker-enterprise-compliance-details"></a><a name="bkmk-compliancedetails"></a>Details van de naleving van BitLocker-onderneming

In dit rapport wordt informatie weer gegeven over de algemene BitLocker-naleving in uw organisatie voor de verzameling van computers waarop u het BitLocker-beheer beleid hebt geïmplementeerd.

[![Voor beeld van een scherm opname van BitLocker Enter prise-nalevings Details](media/bitlocker-enterprise-compliance-details.png)](media/bitlocker-enterprise-compliance-details.png#lightbox)

|Kolomnaam|Beschrijving|
|--- |--- |
|Beheerde computers|Het aantal computers waarop u een BitLocker-beheer beleid hebt geïmplementeerd.|
|% Compatibel|Percentage van compatibele computers in de organisatie.|
|% Niet-compatibel|Het percentage niet-conforme computers in de organisatie.|
|% Onbekende compatibiliteit|Het percentage computers met een nalevings status die niet bekend is.|
|% Uitgezonderd|Het percentage computers dat is uitgesloten van de BitLocker-versleutelings vereiste.|
|% Niet-uitgesloten|Percentage computers die niet zijn uitgesloten van de BitLocker-versleutelings vereiste.|
|Compatibel|Aantal compatibele computers in de organisatie.|
|Niet-compatibel|Aantal niet-conforme computers in de organisatie.|
|Onbekende naleving|Aantal computers met een nalevings status die niet bekend is.|
|Uitgesloten|Telling van computers die zijn uitgesloten van de BitLocker-versleutelings vereiste.|
|Niet-uitgesloten|Aantal computers dat niet is uitgesloten van de BitLocker-versleutelings vereiste.|

### <a name="computer-details"></a>Computer Details

|Kolomnaam|Beschrijving|
|--- |--- |
|Computernaam|De naam van de DNS-computer van het beheerde apparaat.|
|Domeinnaam|De volledig gekwalificeerde domein naam voor de computer.|
|Nalevings status|Algemene nalevings status van de computer. Geldige statussen zijn **compatibel** met en **niet-compatibel**.|
|Gesteld|Hiermee wordt aangegeven of de gebruiker wordt uitgesloten van het BitLocker-beleid of niet is uitgesloten.|
|Gebruikers van het apparaat|Gebruikers van het apparaat.|
|Details van nalevings status|Fout-en status berichten over de nalevings status van de computer uit het opgegeven beleid.|
|Laatste contact|De datum en tijd waarop de computer voor het laatst contact heeft gemaakt met de server om de nalevings status te rapporteren.|

## <a name="bitlocker-enterprise-compliance-summary"></a><a name="bkmk-compliancesummary"></a>Overzicht van BitLocker Enter prise-naleving

Gebruik dit rapport om de algemene BitLocker-naleving in uw organisatie weer te geven. Ook wordt de compatibiliteit weer gegeven voor afzonderlijke computers waarop u het BitLocker-beheer beleid hebt geïmplementeerd.

[![Voor beeld van een scherm opname van het overzicht van BitLocker-bedrijfs naleving](media/bitlocker-enterprise-compliance-summary.png)](media/bitlocker-enterprise-compliance-summary.png#lightbox)

|Kolomnaam|Beschrijving|
|--- |--- |
|Beheerde computers|Het aantal computers dat u beheert met het BitLocker-beleid.|
|% Compatibel|Percentage van compatibele computers in uw organisatie.|
|% Niet-compatibel|Het percentage niet-conforme computers in uw organisatie.|
|% Onbekende compatibiliteit|Het percentage computers met een nalevings status die niet bekend is.|
|% Uitgezonderd|Het percentage computers dat is uitgesloten van de BitLocker-versleutelings vereiste.|
|% Niet-uitgesloten|Percentage computers die niet zijn uitgesloten van de BitLocker-versleutelings vereiste.|
|Compatibel|Aantal compatibele computers in uw organisatie.|
|Niet-compatibel|Aantal niet-conforme computers in uw organisatie.|
|Onbekende naleving|Aantal computers met een nalevings status die niet bekend is.|
|Uitgesloten|Telling van computers die zijn uitgesloten van de BitLocker-versleutelings vereiste.|
|Niet-uitgesloten|Aantal computers dat niet is uitgesloten van de BitLocker-versleutelings vereiste.|

## <a name="recovery-audit-report"></a><a name="bkmk-audit"></a>Controle rapport voor herstel

> [!NOTE]
> Dit rapport is ook beschikbaar via de [website van BitLocker-beheer en-bewaking](helpdesk-portal.md#reports).
>
> Als u dit rapport wilt weer geven in de Configuration Manager-console, gaat u naar de werk ruimte **bewaking** . Vouw in het navigatie deel venster het knoop punt **rapportage** uit, vouw **rapporten**uit en vouw vervolgens de map **BitLocker-beheer** uit. Selecteer de submap voor de gelokaliseerde versie van het rapport, bijvoorbeeld en **-US**.

Gebruik dit rapport om gebruikers te controleren die toegang tot BitLocker-herstel sleutels hebben aangevraagd. U kunt filteren op de volgende criteria:

- Een specifiek type gebruiker, bijvoorbeeld een helpdesk gebruiker of een eind gebruiker
- Als de aanvraag is mislukt of is geslaagd
- Het specifieke type sleutel aangevraagd: wacht woord voor de herstel sleutel, de herstel sleutel-ID of de TPM-wachtwoord-hash
- Een datum bereik waarbinnen het ophalen is uitgevoerd

[![Voor beeld van een scherm opname van het BitLocker-herstel controle rapport](media/bitlocker-recovery-audit-report.png)](media/bitlocker-recovery-audit-report.png#lightbox)

|Kolom&nbsp;naam|Beschrijving|
|----------------|----|
|Datum en tijd van aanvraag|De datum en tijd waarop een eind gebruiker of helpdesk gebruiker een sleutel heeft aangevraagd.|
|Bron controle aanvraag|De site van waaruit de aanvraag afkomstig is. Geldige waarden zijn **selfservice Portal** of de **Help Desk**.|
|Resultaat van aanvraag|De status van de aanvraag. Geldige waarden zijn **geslaagd** of **mislukt**.|
|Gebruikers-Help Desk|De gebruiker met beheerders rechten die de sleutel heeft aangevraagd. Als een helpdesk beheerder de sleutel herstelt zonder de gebruikers naam op te geven, is het veld voor de **eind gebruiker** leeg. Een standaard-helpdesk gebruiker moet de gebruikers naam opgeven die in dit veld wordt weer gegeven. Voor herstel via de Self-Service Portal wordt in dit veld en het veld **eind gebruiker** de naam weer gegeven van de gebruiker die de aanvraag maakt.|
|Eindgebruiker|De naam van de gebruiker die de sleutel ophalen heeft aangevraagd.|
|Computer|De naam van de computer die is hersteld.|
|Type sleutel|Het type sleutel dat de gebruiker heeft aangevraagd. De drie soorten sleutels zijn:<br/><br/>- **Wacht woord voor herstel sleutel**: wordt gebruikt voor het herstellen van een computer in de herstel modus<br/>- **Herstel sleutel-id**: wordt gebruikt om een computer in de herstel modus te herstellen voor een andere gebruiker<br/>- **Wacht woord-hash van TPM**: wordt gebruikt om een computer met een vergrendelde TPM te herstellen|
|Beschrijving van reden|Waarom de gebruiker het opgegeven sleutel type heeft aangevraagd, gebaseerd op de geselecteerde optie in het formulier.|

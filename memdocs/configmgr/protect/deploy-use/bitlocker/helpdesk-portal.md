---
title: Website voor BitLocker-beheer en-bewaking
titleSuffix: Configuration Manager
description: De BitLocker-beheer-en bewakings website (helpdesk Portal) gebruiken in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b64e09561def3d19c306b9cfcd4f7eb808763fd
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129253"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>Website voor BitLocker-beheer en-bewaking

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3601034-->

De website BitLocker-beheer en-controle is een beheer interface voor BitLocker-stationsversleuteling. Het wordt ook wel de helpdesk Portal genoemd. Gebruik deze website om rapporten te bekijken, stations van gebruikers te herstellen en Tpm's te beheren.

[![Scherm afbeelding van standaard-BitLocker-beheer-en-bewakings website](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

Voordat u deze kunt gebruiken, installeert u dit onderdeel op een webserver. Zie [BitLocker-rapporten en-portals instellen](setup-websites.md)voor meer informatie.

Open de website beheer en controle via de volgende URL:`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> U kunt het **rapport herstel controle** bekijken op de website beheer en controle. U voegt andere BitLocker-beheer rapporten toe aan het Reporting Services-punt. Zie [BitLocker-rapporten weer geven](view-reports.md)voor meer informatie.

## <a name="groups"></a>Groepen

Om toegang te krijgen tot specifieke gebieden van de beheer-en bewakings website, moet uw gebruikers account zich in een van de volgende groepen bezien. Maak deze groepen in Active Directory een wille keurige naam die u wilt gebruiken. Wanneer u deze website installeert, geeft u deze groeps namen op. Zie [BitLocker-rapporten en-portals instellen](setup-websites.md)voor meer informatie.

|Groep|Beschrijving|
|--- |--- |
|Beheerders van BitLocker-Help Desk|Biedt toegang tot alle gebieden van de beheer-en bewakings website. Wanneer u een gebruiker helpt hun stations te herstellen, voert u alleen de herstel sleutel in en niet de domein-en gebruikers naam. Als een gebruiker lid is van zowel deze groep als de gebruikers groep van de BitLocker-Help Desk, worden de machtigingen van de gebruikers groep overschreven door de beheerders groep.|
|Gebruikers van BitLocker-Help Desk|Biedt toegang tot de modules **TPM** en **stations herstellen** van de beheer-en bewakings website. Wanneer u een van beide gebieden gebruikt, moet u alle velden invullen, inclusief het domein en de account naam van de gebruiker. Als een gebruiker lid is van zowel deze groep als de beheerders groep van de BitLocker-Help Desk, worden de machtigingen van de gebruikers groep overschreven door de beheerders groep.|
|Gebruikers van BitLocker-rapport|Geeft toegang tot het gebied **rapporten** van de website beheer en controle.|

## <a name="manage-tpm"></a>TPM beheren

Als een gebruiker de verkeerde pincode te vaak invoert, kan de TPM worden vergrendeld. Het aantal keren dat een gebruiker een onjuiste pincode mag invoeren voordat de TPM-vergren delingen variëren van fabrikant tot fabrikant. Vanuit het gebied **TPM beheren** van de website beheer en controle opent u het centrale sleutel herstel gegevens systeem.

Zie voor meer informatie over TPM-eigendom [MBAM configureren om de TPM te borgen en OwnerAuth-wacht woorden op te slaan](https://docs.microsoft.com/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm).

> [!NOTE]
> Vanaf Windows 10, versie 1607, houdt Windows het wacht woord voor TPM-eigenaar niet bij het inrichten van de TPM.

1. Ga naar de website voor beheer en controle in de webbrowser `https://webserver.contoso.com/HelpDesk` .

1. Selecteer in het linkerdeel venster het gebied **TPM beheren** .

    ![Website voor BitLocker-beheer en-controle TPM-pagina beheren](media/bitlocker-admin-manage-tpm.png)

1. Voer de Fully Qualified Domain Name voor de computer en de naam van de computer in.

1. Voer, indien nodig, het domein en de gebruikers naam van de gebruiker in om het wachtwoord bestand voor de TPM-eigenaar op te halen.

1. Kies een van de volgende opties voor de **reden voor het aanvragen van het wachtwoord bestand voor de TPM-eigenaar**:

    - PINCODE vergrendeling opnieuw instellen
    - TPM inschakelen
    - TPM uitschakelen
    - TPM-wacht woord wijzigen
    - TPM wissen
    - Overige

    Nadat u het formulier hebt **verzonden** , retourneert de website een van de volgende antwoorden:

    - Als er geen overeenkomend wachtwoord bestand voor de TPM-eigenaar kan worden gevonden, wordt er een fout bericht weer gegeven.

    - Het wachtwoord bestand voor de TPM-eigenaar voor de verzonden computer

    Nadat u het wachtwoord bestand voor de TPM-eigenaar hebt opgehaald, wordt het eigenaars wachtwoord door de website weer gegeven.

1. Selecteer **Opslaan**om het wacht woord op te slaan in een bestand.

1. Selecteer in het gebied **TPM beheren** de optie **TPM-vergren deling opnieuw instellen** en geef het wachtwoord bestand voor de TPM-eigenaar op.

    De TPM-vergren deling wordt opnieuw ingesteld. BitLocker herstelt de toegang van de gebruiker tot het apparaat.

    > [!IMPORTANT]
    > Deel geen TPM-hashwaarde of wachtwoord bestand voor TPM-eigenaar.

## <a name="drive-recovery"></a>Herstel van station

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a>Een station herstellen in herstel modus

Stations gaan in de herstel modus in de volgende scenario's:

- De gebruiker de pincode of het wacht woord kwijtraakt of vergeet
- Het Trusted module platform (TPM) detecteert wijzigingen in de BIOS-of opstart bestanden van de computer

Als u een herstel wachtwoord wilt ophalen, gebruikt u het gedeelte **stations herstellen** van de website beheer en controle.

> [!IMPORTANT]
> Herstel wachtwoorden verlopen na één gebruik. Op stations voor het besturings systeem en vaste schijven wordt de regel voor eenmalig gebruik automatisch toegepast. Op Verwissel bare stations wordt toegepast wanneer u het station verwijdert en opnieuw plaatst.

1. Ga naar de website voor beheer en controle in de webbrowser `https://webserver.contoso.com/HelpDesk` .

1. Selecteer in het linkerdeel venster het gebied voor het herstel van de **schijf** .

    ![BitLocker-beheer-en bewakings pagina stuur programma herstellen](media/bitlocker-admin-drive-recovery.png)

1. Voer, indien nodig, het domein en de gebruikers naam van de gebruiker in om de herstel gegevens weer te geven.

1. Voer de eerste acht cijfers van de herstel sleutel-ID in om een lijst met mogelijke overeenkomende herstel sleutels weer te geven. Als u de exacte herstel sleutel wilt ophalen, geeft u de volledige herstel sleutel-ID op.

1. Kies een van de volgende opties als de **reden voor het ontgrendelen van het station**:

    - De opstart volgorde van het besturings systeem is gewijzigd
    - BIOS gewijzigd
    - Bestanden van het besturings systeem zijn gewijzigd
    - De opstart sleutel is verloren gegaan
    - Verloren pincode
    - TPM opnieuw instellen
    - Verloren wachtwoordzin
    - Verloren Smart Card
    - Overige

    Nadat u het formulier hebt **verzonden** , retourneert de website een van de volgende antwoorden:

    - Als de gebruiker meerdere overeenkomende herstel wachtwoorden heeft, worden er meerdere mogelijke overeenkomsten geretourneerd.

    - Het herstel wachtwoord en het herstel pakket voor de ingediende gebruiker.

        > [!NOTE]
        > Als u een beschadigd station herstelt, biedt de herstel pakket optie BitLocker met essentiële informatie die nodig is om het station te herstellen.

    - Als er geen overeenkomend herstel wachtwoord kan worden gevonden, wordt er een fout bericht weer gegeven.

    Nadat u het herstel wachtwoord en het herstel pakket hebt opgehaald, wordt in de website het herstel wachtwoord weer gegeven.

1. Selecteer **sleutel kopiëren**om het wacht woord te kopiëren. Selecteer **Opslaan**om het herstel wachtwoord op te slaan in een bestand.

Als u het station wilt ontgrendelen, voert u het herstel wachtwoord in of gebruikt u het herstel pakket.

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a>Een verplaatste schijf herstellen

Wanneer u een station naar een nieuwe computer verplaatst, omdat de TPM anders is, accepteert BitLocker de vorige pincode niet. Als u het verplaatste station wilt herstellen, moet u de herstel sleutel-ID ophalen om het herstel wachtwoord op te halen.

Als u een verplaatste station wilt herstellen, gebruikt u het gebied voor **schijf herstel** van de website beheer en controle.

1. Op de computer met het verplaatste station, start u de computer in de modus Windows Recovery Environment (WinRE).

1. In WinRE behandelt BitLocker het verplaatste station van het besturings systeem als een vast gegevens station. BitLocker geeft de wacht woord-ID van het station weer en vraagt om het herstel wachtwoord.

    > [!NOTE]
    > In sommige gevallen selecteert u tijdens het opstart proces **de pincode** wanneer de optie beschikbaar is. Voer vervolgens de herstel modus in om de herstel sleutel-ID weer te geven.

1. Gebruik de herstel sleutel-ID om het herstel wachtwoord op te halen van de website beheer en controle. Zie [herstellen van een station in de herstel modus](#bkmk_recovery)voor meer informatie.

Als u het verplaatste station hebt geconfigureerd voor het gebruik van een TPM-chip op de oorspronkelijke computer, voert u de volgende stappen uit. Anders is het herstel proces voltooid.

1. Nadat u het station hebt ontgrendeld, start u de computer in de modus WinRE. Open een opdracht prompt in WinRE en gebruik de `manage-bde` opdracht om het station te ontsleutelen. Dit hulp programma is de enige manier om de beveiliging van **TPM + pincode** te verwijderen zonder de oorspronkelijke TPM-chip. Zie [Manage-BDE](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde)voor meer informatie over deze opdracht.

1. Wanneer het is voltooid, start u de computer normaal op. Configuration Manager wordt het BitLocker-beleid afgedwongen voor het versleutelen van het station met de TPM plus pincode van de nieuwe computer.

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a>Een beschadigd station herstellen

Gebruik de herstel sleutel-ID om een herstel sleutel pakket op te halen van de website beheer en controle. Zie [herstellen van een station in de herstel modus](#bkmk_recovery)voor meer informatie.

1. Sla het **herstel sleutel pakket** op uw computer op en kopieer het naar de computer met het beschadigde station.

1. Open een opdracht prompt als beheerder en typ de volgende opdracht:

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    Vervang de volgende waarden:

    - `<corrupted drive>`: De stationsletter van het beschadigde station, bijvoorbeeld`D:`
    - `<fixed drive>`: De stationsletter van een beschik bare harde schijf met een vergelijk bare of grotere grootte dan het beschadigde station. BitLocker herstelt en verplaatst gegevens op het beschadigde station naar het opgegeven station. Alle gegevens op dit station worden overschreven.
    - `<key package>`: De locatie van het herstel sleutel pakket
    - `<recovery password>`: Het bijbehorende herstel wachtwoord

    Bijvoorbeeld:

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

Zie [Repair-BDE](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde)voor meer informatie over deze opdracht.

## <a name="reports"></a>Rapporten

De website beheer en controle bevat het **rapport herstel controle**. Andere rapporten zijn beschikbaar op het Configuration Manager Reporting Services-punt. Zie [BitLocker-rapporten weer geven](view-reports.md)voor meer informatie.

1. Ga naar de website voor beheer en controle in de webbrowser `https://webserver.contoso.com/HelpDesk` .

1. Selecteer het gebied **rapporten** in het linkerdeel venster.

1. Selecteer in de bovenste menu balk het **rapport herstel controle**.

Zie [herstel controle rapport](view-reports.md#bkmk-audit) voor meer informatie over dit rapport

> [!TIP]
> Als u rapport resultaten wilt opslaan, selecteert u **exporteren** op de menu balk **rapporten** .

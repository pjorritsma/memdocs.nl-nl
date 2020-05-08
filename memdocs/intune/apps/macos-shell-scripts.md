---
title: Shell-scripts op macOS-apparaten gebruiken in Intune | Microsoft Docs
description: Shell-scripts maken, toewijzen en controleren en problemen oplossen met Shell-scripts voor macOS-apparaten in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5839154ab0c884e933e8d11055e745d54503433
ms.sourcegitcommit: 8a8378b685a674083bfb9fbc9c0662fb0c7dda97
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/01/2020
ms.locfileid: "82619539"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>Shell-scripts op macOS-apparaten gebruiken in Intune (openbare preview)

> [!NOTE]
> Shell-scripts voor macOS-apparaten zijn momenteel beschikbaar als preview-versie. Bekijk de lijst met [Bekende problemen in Preview](macos-shell-scripts.md#known-issues) voordat u deze functie gebruikt.

Gebruik Shell-scripts om de mogelijkheden voor apparaatbeheer uit te breiden op Intune tot voorbij de mogelijkheden die worden ondersteund door het macOS-besturingssysteem. 

## <a name="prerequisites"></a>Vereisten
Zorg ervoor dat aan de volgende vereisten wordt voldaan bij het opstellen van Shell-scripts en het toewijzen ervan aan macOS-apparaten. 
 - Op apparaten wordt macOS 10.12 of hoger uitgevoerd.
 - De apparaten worden beheerd met Intune. 
 - Shell-scripts beginnen met `#!` en moeten zich op een geldige locatie bevinden, zoals `#!/bin/sh` of `#!/usr/bin/env zsh`.
 - Er zijn vertalers voor de opdrachtregel voor de toepasselijke Shells geïnstalleerd.

## <a name="important-considerations-before-using-shell-scripts"></a>Belangrijke overwegingen voordat u Shell-scripts gebruikt
 - Voor Shell-scripts moet de Microsoft Intune-beheeragent op het macOS-apparaat zijn geïnstalleerd. Zie [Microsoft Intune-beheeragent voor macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos) voor meer informatie.
 - Shell-scripts worden parallel uitgevoerd op apparaten als afzonderlijke processen.
 - Shell-scripts die worden uitgevoerd als de aangemelde gebruiker, worden uitgevoerd voor alle aangemelde gebruikersaccounts op het apparaat op het moment van de uitvoering.
 - Een eindgebruiker moet zich aanmelden bij het apparaat om scripts uit te voeren die worden uitgevoerd als een aangemelde gebruiker.
 - Rootgebruikersbevoegdheden zijn vereist als het script vereist dat er wijzigingen worden aangebracht die niet met een standaardgebruikersaccount kunnen worden aangebracht.
 - Voor Shell-scripts wordt vaker geprobeerd deze uit te voeren dan de gekozen scriptfrequentie voor bepaalde voorwaarden, bijvoorbeeld als de schijf vol is, als de opslaglocatie is gewijzigd, als de lokale cache wordt verwijderd, of als het Mac-apparaat opnieuw wordt opgestart.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Een Shell-scriptbeleid maken en toewijzen
1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **macOS** > **Scripts** > **Toevoegen**.
3. Voer in **Basisinformatie** de volgende eigenschappen in en selecteer **Volgende**:
   - **Naam**: Voer een naam in voor het Shell-script.
   - **Beschrijving**: Voer een beschrijving in voor het Shell-script. Deze instelling is optioneel, maar wordt aanbevolen.
4. Voer in **Scriptinstellingen** de volgende eigenschappen in en selecteer **Volgende**:
   - **Script uploaden**: Blader naar het Shell-script. Het scriptbestand moet kleiner zijn dan 200 kB.
   - **Script uitvoeren als aangemelde gebruiker**: Selecteer **Ja** om het script op het apparaat uit te voeren met de referenties van de gebruiker. Kies **Nee** (standaard) om het script als de rootgebruiker uit te voeren. 
   - **Scriptmeldingen op apparaten verbergen:** Scriptmeldingen worden standaard weergegeven voor elk script dat wordt uitgevoerd. Eindgebruikers zien een melding van Intune op macOS-apparaten over dat *deze de computer wordt geconfigureerd door de IT-afdeling*.
   - **Scriptfrequentie:** Selecteer hoe vaak het script moet worden uitgevoerd. Kies **Niet geconfigureerd** (standaard) om een script slechts één keer uit te voeren.
   - **Maximum aantal keren dat het script opnieuw moet worden uitgevoerd als het script mislukt:** Selecteer hoe vaak het script moet worden uitgevoerd als er een afsluitcode wordt geretourneerd die niet gelijk is aan nul (0 betekent geslaagd). Kies **Niet geconfigureerd** (standaard) om een script niet opnieuw uit te voeren nadat het is mislukt.
5. Voeg in **Bereiktags** desgewenste bereiktags toe voor het script en selecteer **Volgende**. U kunt bereiktags gebruiken om te bepalen wie scripts mag bekijken in Intune. Zie [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Op rollen gebaseerd toegangsbeheer en bereiktags gebruiken voor gedistribueerde IT) voor uitgebreide informatie over bereiktags.
6. Selecteer **Toewijzingen** > **Selecteer groepen om in te sluiten**. Er wordt een bestaande lijst met Azure AD-groepen weergegeven. Selecteer een of meer apparaatgroepen die de gebruikers bevatten wiens macOS-apparaten het script moeten ontvangen. Kies **Selecteren**. De groepen die u hebt gekozen, worden weergegeven in de lijst en ontvangen uw scriptbeleid.
   > [!NOTE]
   > - Shell-scripts in Intune kunnen alleen worden toegewezen aan Azure AD-apparaatbeveiligingsgroepen. De toewijzing van de gebruikersgroep wordt niet ondersteund in de preview-versie. 
   > - Bij het bijwerken van toewijzingen voor Shell-scripts worden ook toewijzingen voor de [Microsoft Intune-beheeragent voor macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos) bijgewerkt.
7. In **Controleren en toevoegen** wordt een samenvatting weer gegeven van de instellingen die u hebt geconfigureerd. Selecteer **Toevoegen** om het script op te slaan. Wanneer u **Toevoegen** selecteert, wordt het scriptbeleid geïmplementeerd in de groepen die u hebt gekozen.

Het script dat u hebt gemaakt, wordt weergegeven in de lijst met scripts. 

## <a name="monitor-a-shell-script-policy"></a>Een Shell-scriptbeleid controleren
U kunt de uitvoeringsstatus van alle toegewezen scripts voor gebruikers en apparaten controleren door een van de volgende rapporten te kiezen:
- **Scripts** > **selecteer het script dat u wilt controleren** > **Apparaatstatus**
- **Scripts** > **selecteer het script dat u wilt controleren** > **Gebruikersstatus**

>[!IMPORTANT]
> Ongeacht de geselecteerde **scriptfrequentie** wordt de uitvoeringsstatus van het script alleen gerapporteerd wanneer een script voor het eerst wordt uitgevoerd. De uitvoeringsstatus van het script wordt niet bijgewerkt bij volgende uitvoeringen. Bijgewerkte scripts worden echter behandeld als nieuwe scripts en de uitvoeringsstatus wordt opnieuw gerapporteerd.

Wanneer een script wordt uitgevoerd, wordt een van de volgende statussen geretourneerd:
- De uitvoeringsstatus **Mislukt** geeft aan dat het script een afsluitcode heeft geretourneerd die niet gelijk is aan nul of dat het script een onjuiste indeling heeft. 
- De uitvoeringsstatus **Geslaagd** geeft aan dat het script nul als afsluitcode heeft geretourneerd. 

## <a name="troubleshoot-macos-shell-script-policies-using-log-collection"></a>Problemen met macOS Shell-scriptbeleid oplossen met behulp van logboekverzameling

U kunt apparaatlogboeken verzamelen om problemen met scripts op macOS-apparaten op te lossen. 

### <a name="requirements-for-log-collection"></a>Vereisten voor logboekverzameling
De volgende items zijn vereist voor logboekverzameling op een macOS-apparaat:
- U moet het volledige absolute pad naar het logboekbestand opgeven.
- Bestandspaden moeten worden gescheiden door een puntkomma (;).
- U kunt een logboekverzameling van maximaal 60 MB (gecomprimeerd) of 25 bestanden uploaden, wat zich het eerst voordoet.
- Bestandstypen die zijn toegestaan voor logboekverzameling zijn onder meer de volgende extensies: *.log, .zip, .gz, .tar, .txt, .xml, .crash, .rtf*

#### <a name="collect-device-logs"></a>Apparaatlogboeken verzamelen
1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer een apparaat in het rapport **Apparaatstatus** of **Gebruikersstatus**.
3. Selecteer **Logboeken verzamelen**, geef mappaden of logboekbestanden op die alleen gescheiden zijn door een puntkomma (;), zonder spaties of nieuwe regels tussen paden.<br>Meerdere paden moeten bijvoorbeeld worden geschreven als `/Path/to/logfile1.zip;/Path/to/logfile2.log`. 

   >[!IMPORTANT]
   > Als meerdere logboekbestandspaden zijn gescheiden door een komma, een punt, een nieuwe regel of aanhalingstekens met of zonder spaties, leidt dit tot een logboekverzamelingsfout. Spaties zijn ook niet toegestaan als scheidingsteken tussen paden.

4. Selecteer **OK**. De logboeken worden verzameld de volgende keer dat de Intune-beheeragent op het apparaat wordt ingecheckt bij Intune. Deze incheck vindt doorgaans elke acht uur plaats.

   >[!NOTE]
   > 
   > - Verzamelde logboeken worden versleuteld op het apparaat, verzonden en dertig dagen opgeslagen in Microsoft Azure Storage. Opgeslagen logboeken worden op aanvraag ontsleuteld en gedownload met behulp van Microsoft Endpoint Manager-beheercentrum.
   > - Naast de door de beheerder opgegeven logboeken worden de Intune-beheeragentlogboeken ook verzameld vanuit deze mappen: `/Library/Logs/Microsoft/Intune` en `~/Library/Logs/Microsoft/Intune`. De namen van de agentlogboekbestanden zijn `IntuneMDMDaemon date--time.log` en `IntuneMDMAgent date--time.log`. 
   > - Als een door de beheerder opgegeven bestand ontbreekt of de verkeerde bestandsextensie heeft, worden deze bestandsnamen vermeld in `LogCollectionInfo.txt`.     

### <a name="log-collection-errors"></a>Fouten bij logboekverzameling
De logboekverzameling kan mogelijk niet worden uitgevoerd om een van de redenen in de onderstaande tabel. Volg de herstelstappen om deze fouten op te lossen.

| Foutcode (hexadecimaal) | Foutcode (decimaal) | Foutbericht | Herstelstappen |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | Logboekbestand mag niet groter zijn dan 60 MB. | Zorg ervoor dat gecomprimeerde logboeken kleiner zijn dan 60 MB. |
| 0X87D300D1 | 2016214831 | Het opgegeven pad van het logboekbestand moet bestaan. De systeemgebruikersmap is een ongeldige locatie voor logboekbestanden. | Zorg ervoor dat het opgegeven bestandspad geldig en toegankelijk is. |
| 0X87D300D2 | 2016214830 | Bestand uploaden voor logboekverzameling is mislukt vanwege het verlopen van de upload-URL. | Voer de actie **Logboeken verzamelen** opnieuw uit. |
| 0X87D300D3, 0X87D300D5, 0X87D300D7 | 2016214829, 2016214827, 2016214825 | Bestand uploaden voor logboekverzameling is mislukt vanwege een versleutelingsfout. Probeer nogmaals het logboek te uploaden. | Voer de actie **Logboeken verzamelen** opnieuw uit. |
| | 2016214828 | Het aantal logboekbestanden overschrijdt de toegestane limiet van 25 bestanden. | Er kunnen maar maximaal 25 logboekbestanden tegelijk worden verzameld. |
| 0X87D300D6 | 2016214826 | Bestand uploaden voor logboekverzameling is mislukt vanwege een zip-fout. Probeer nogmaals het logboek te uploaden. | Voer de actie **Logboeken verzamelen** opnieuw uit. |
| | 2016214740 | De logboeken kunnen niet worden versleuteld omdat er geen gecomprimeerde logboeken zijn gevonden. | Voer de actie **Logboeken verzamelen** opnieuw uit. |
| | 2016214739 | De logboeken zijn verzameld, maar kunnen niet worden opgeslagen. | Voer de actie **Logboeken verzamelen** opnieuw uit. |

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Waarom worden toegewezen Shell-scripts niet op het apparaat uitgevoerd?
Hiervoor kunnen verschillende redenen zijn:
* De agent moet mogelijk worden ingecheckt om nieuwe of bijgewerkte scripts te ontvangen. Dit incheckproces vindt elke 8 uur plaats en wijkt af van het inchecken bij MDM. Zorg ervoor dat het apparaat actief is en is verbonden met een netwerk om de agent in te checken en te wachten totdat de agent wordt ingecheckt.
* De agent is mogelijk niet geïnstalleerd. Controleer of de agent is geïnstalleerd op `/Library/Intune/Microsoft Intune Agent.app` op het macOS-apparaat.
* De status van de agent is mogelijk niet in orde. Er zal 24 uur worden geprobeerd de agent te herstellen, waarna de agent wordt verwijderd en opnieuw geïnstalleerd als er nog Shell-scripts aan zijn toegewezen.

### <a name="how-frequently-is-script-run-status-reported"></a>Hoe vaak wordt de uitvoeringsstatus van het script gerapporteerd?
De uitvoeringsstatus van het script wordt gerapporteerd aan de Microsoft Endpoint Manager-beheerconsole zodra het script is uitgevoerd. Als een script volgens een ingestelde frequentie regelmatig wordt uitgevoerd, wordt er alleen een status gerapporteerd van de eerste keer dat de uitvoering wordt uitgevoerd.

### <a name="when-are-shell-scripts-run-again"></a>Wanneer worden Shell-scripts opnieuw uitgevoerd?
Een script wordt pas opnieuw uitgevoerd wanneer de instelling **Maximum aantal keren dat het script opnieuw moet worden uitgevoerd als het script mislukt** is geconfigureerd en het script niet kan worden uitgevoerd. Als de instelling **Maximum aantal keren dat het script opnieuw moet worden uitgevoerd als het script mislukt** niet is geconfigureerd en het uitvoeren van het script mislukt, wordt het niet opnieuw uitgevoerd en krijgt het de uitvoeringsstatus **Mislukt**. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Welke Intune-rolmachtigingen zijn vereist voor Shell-scripts?
Voor uw toegewezen Intune-rol zijn machtigingen vereist voor **Apparaatconfiguraties** om Shell-scripts te verwijderen, toe te wijzen, te maken, bij te werken of te lezen.

## <a name="microsoft-intune-management-agent-for-macos"></a>Microsoft Intune-beheeragent voor macOS
 ### <a name="why-is-the-agent-required"></a>Waarom is de agent vereist?
De Microsoft Intune-beheeragent moet worden geïnstalleerd op beheerde macOS-apparaten om geavanceerde mogelijkheden voor apparaatbeheer mogelijk te maken die niet worden ondersteund door het systeemeigen macOS-besturingssysteem.
 
 ### <a name="how-is-the-agent-installed"></a>Hoe wordt de agent geïnstalleerd?
 De agent wordt automatisch en op de achtergrond geïnstalleerd op de door Intune beheerde macOS-apparaten waaraan u ten minste één Shell-script toewijst in het Microsoft Endpoint Manager-beheercentrum. De agent wordt indien van toepassing geïnstalleerd op `/Library/Intune/Microsoft Intune Agent.app` en wordt niet weergegeven in **Finder** > **Programma's** op macOS-apparaten. De agent wordt weergegeven als `IntuneMdmAgent` in **Activiteitsbewaking** wanneer de agent wordt uitgevoerd op macOS-apparaten.

### <a name="what-does-the-agent-do"></a>Wat doet de agent?
 - De agent wordt op de achtergrond geverifieerd bij Intune-services voordat deze wordt ingecheckt om toegewezen Shell-scripts voor het macOS-apparaat te ontvangen.
 - De agent ontvangt toegewezen Shell-scripts en voert de scripts uit op basis van het geconfigureerde schema, het aantal nieuwe pogingen, de meldingsinstellingen en andere instellingen die door de beheerder zijn ingesteld.
 - De agent controleert meestal elke 8 uur op nieuwe of bijgewerkte scripts bij Intune-services. Dit check-inproces is onafhankelijk van het inchecken bij MDM. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Hoe kan ik handmatig het inchecken van een agent initiëren vanaf een Mac-computer?
Open **Terminal** op een Mac-computer waarop de agent is geïnstalleerd, en voer de opdracht `sudo killall IntuneMdmAgent` uit om het `IntuneMdmAgent`-proces te beëindigen. Het `IntuneMdmAgent`-proces wordt onmiddellijk opnieuw gestart. Hierdoor wordt een check-in bij Intune geïnitieerd.

U kunt ook het volgende doen:
1. Open **Activiteitbewaking** > **Weergeven** > *en selecteer **Alle processen**.* 
2. Zoek naar processen met de naam `IntuneMdmAgent`. 
3. Sluit het proces dat wordt uitgevoerd voor **rootgebruiker**. 

> [!NOTE]
> Met de actie **Instellingen controleren** in de bedrijfsportal en de actie **Synchroniseren** voor apparaten in de Microsoft Endpoint Manager-beheerconsole wordt een MDM-check-in geïnitieerd. Inchecken van de agent wordt niet afgedwongen.

 ### <a name="when-is-the-agent-removed"></a>Wanneer wordt de agent verwijderd?
 Er zijn verschillende omstandigheden die ertoe kunnen leiden dat de agent van het apparaat wordt verwijderd, zoals:
 - Shell-scripts zijn niet meer toegewezen aan het apparaat. 
 - Het macOS-apparaat wordt niet meer beheerd.
 - De agent bevindt zich in een onherstelbare status van meer dan 24 uur (de actieve tijd van het apparaat).

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Hoe kan ik de gebruiksgegevens die naar Microsoft worden verstuurd uitschakelen voor Shell-scripts?
 Als u de gebruiksgegevens die naar Microsoft worden verzonden wilt uitschakelen vanuit de Intune-beheeragent, opent u de bedrijfsportal en selecteert u **Menu** > **Voorkeuren** >  *en schakelt u het selectievakje Microsoft toestaan gebruiksgegevens te verzamelen* uit. Hiermee worden de gebruiksgegevens uitgeschakeld die worden verstuurd voor zowel de agent als de bedrijfsportal.

## <a name="known-issues"></a>Bekende problemen
- **Toewijzing van de gebruikersgroep:** Shell-scripts die zijn toegewezen aan gebruikersgroepen, zijn niet van toepassing op apparaten. De toewijzing van de gebruikersgroep wordt momenteel niet ondersteund in de preview-versie. Gebruik toewijzing van apparaatgroepen om scripts toe te wijzen.
- **Logboeken verzamelen:** De actie Logboeken verzamelen is zichtbaar. Wanneer u echter logboeken probeert te verzamelen, wordt het foutbericht 'Er is een fout opgetreden' weergegeven en worden de logboeken niet vastgelegd. Het verzamelen van logboeken wordt momenteel niet ondersteund in de preview-versie.
- **Geen uitvoeringsstatus van script:** In het onwaarschijnlijke geval dat een script wordt ontvangen op het apparaat en het apparaat offline gaat voordat de uitvoeringsstatus is gerapporteerd, wordt de uitvoeringsstatus van het script niet gerapporteerd in de beheerconsole.
- **Rapport van gebruikersstatus:** Er is een probleem met een leeg rapport. Selecteer **Controleren** in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431). De gebruikersstatus toont een leeg rapport.

## <a name="next-steps"></a>Volgende stappen

- [Een nalevingsbeleid maken in Microsoft Intune](..\protect\create-compliance-policy.md)

---
title: Health Attestation
titleSuffix: Configuration Manager
description: Meer informatie over de Apparaatstatusverklaring functionaliteit die wordt weer gegeven in de Configuration Manager-console.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d57be201274c347e5dcd492734b2141c64d579b
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700007"
---
# <a name="health-attestation-for-configuration-manager"></a>Status verklaring voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Beheerders kunnen de status van[ Windows 10 Health Attestation](/windows/security/threat-protection/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices) van apparaten bekijken in de Configuration Manager-console.  Met Health Attestation van apparaten kan de beheerder ervoor zorgen dat clientcomputers over de volgende betrouwbare configuraties van BIOS, TPM en opstartsoftware beschikken:  

-   Early Launch Antimalware: Early Launch Antimalware (ELAM) beschermt uw computer wanneer deze wordt gestart en voordat de stuurprogramma's van derden worden geïnitialiseerd. [ELAM inschakelen](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker: Windows BitLocker-stationsversleuteling is software waarmee u alle gegevens kunt versleutelen die zijn opgeslagen op het Windows-besturingssysteemvolume.  [BitLocker inschakelen](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Beveiligd opstarten: beveiligd opstarten is een standaard die is ontwikkeld door leden van de pc-industrie om ervoor te zorgen dat uw pc opstart met alleen de software die wordt vertrouwd door de fabrikant van de computer. [Meer informatie over beveiligd opstarten](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824987(v=win.10))  
-   Code-integriteit: code-integriteit is een functie die de beveiliging van het besturingssysteem verbetert door de integriteit van een stuurprogramma of systeembestand te valideren elke keer wanneer dit in het geheugen wordt geladen. [Meer informatie over code-integriteit](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd348642(v=ws.10))  

Deze functionaliteit is beschikbaar voor pc's en on-premises bronnen die worden beheerd door Configuration Manager en mobiele apparaten die met behulp van Microsoft Intune worden beheerd. Beheerders kunnen opgeven of rapportage plaatsvindt via de cloud of on-premises infrastructuur. Door de bewaking van on-premises apparaatstatusverklaring kan de beheerder client-Pc's zonder Internet toegang controleren.

## <a name="enable-health-attestation"></a>Status verklaring inschakelen

 **Vereiste**  

-   Client apparaten met Windows 10 versie 1607 of Windows Server 2016 versie 1607 met [Apparaatstatusverklaring ingeschakeld](/windows-server/security/device-health-attestation).
-   TPM 1,2 of TPM 2 ingeschakelde apparaten.
-   Wanneer u Cloud beheer gebruikt, wordt de communicatie tussen de Configuration Manager client agent en het beheer punt met de Health Attestation-service van *has.spserv.Microsoft.com* (poort 443) (Cloud beheer). Bij on-premises moet de client kunnen communiceren met het beheer punt voor apparaatstatusverklaring-functionaliteit.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Health Attestation-servicecommunicatie inschakelen op Configuration Manager-clientcomputers

Gebruik deze procedure om apparaatstatusverklaring-bewaking in te scha kelen voor apparaten die verbinding maken met internet.

1.  Kies in de Configuration Manager-console **beheer**  >  **overzicht**  >  **client instellingen**.  Kies het tabblad voor **Computeragent** -instellingen.  
2.  Selecteer in het dialoogvenster **Standaardinstellingen** de optie **Computeragent** en schuif vervolgens omlaag naar **Communicatie met de Health Attestation-service inschakelen**  
3.  Stel de optie **Communicatie met de Health Attestation-Service inschakelen** in op **Ja**en klik vervolgens op **OK**.  
4. Richt de verzamelingen van apparaten in die de apparaatstatus moeten rapporteren.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>On-premises Health Attestation-servicecommunicatie inschakelen op Configuration Manager-clientcomputers
Gebruik deze procedure om de apparaatstatusverklaring-bewaking in te scha kelen voor on-premises apparaten die geen verbinding maken met internet.

Vanaf Configuration Manager 1702 kan de URL van de on-premises apparaatstatusverklaring-service op het beheer punt worden geconfigureerd voor de ondersteuning van client apparaten zonder Internet toegang.

1. Ga in de Configuration Manager-console naar **beheer**  >  **overzicht**  >  **site configuratie**  >  **sites**.
2. Klik met de rechter muisknop op de primaire of secundaire site met het beheer punt dat ondersteuning biedt voor on-premises apparaatstatusverklaring-clients en selecteer **site onderdelen**  >  **beheer punt**configureren. De pagina **Eigenschappen van beheer punt onderdelen** wordt geopend.
3. Selecteer op het tabblad **Geavanceerde opties** de optie **toevoegen** en geef een geldige on-premises URL voor de apparaatstatusverklaring-service op. U kunt meerdere Url's toevoegen. Als er meerdere on-premises Url's worden opgegeven, ontvangen clients de volledige set en kiezen die wille keurig te gebruiken.
4.  Kies in de Configuration Manager-console **beheer**  >  **overzicht**  >  **client instellingen**.  Kies het tabblad voor **Computeragent** -instellingen.  
5.  Schuif omlaag om **communicatie met de Health Attestation-service in te scha kelen**en stel in op **Ja**.
7.  Klik op de optie **on-premises Health Attestaion-service gebruiken** en stel dit in op **Ja**.
8. Richt u op de verzamelingen apparaten die de status van apparaten moeten rapporteren met de instellingen van de client agent om apparaatstatusverklaring-rapportage in te scha kelen.

U kunt ook Url's van apparaatstatusverklaring-service **bewerken** of **verwijderen** .

> [!NOTE]
> Als u apparaatstatusverklaring hebt gebruikt voordat u een upgrade uitvoert naar Configuration Manager 1702, worden de on-premises Url's die zijn opgegeven in de instellingen van de client agent vooraf ingevuld in de beheer punt eigenschappen tijdens de upgrade. On-premises clients blijven de URL gebruiken die is opgegeven in de instellingen van de client agent totdat ze zijn bijgewerkt. Vervolgens wordt overgeschakeld naar een van de Url's die zijn opgegeven op het beheer punt.

## <a name="monitor-device-health-attestation"></a>Apparaatstatusverklaring controleren

1.  Als u de Health Attestation van apparaten wilt weergeven, doet u het volgende: ga in de Configuration Manager-console naar de werkruimte **Bewaking** , klik op het knooppunt **Beveiliging** en klik vervolgens op **Health Attestation**.  
2.  Health Attestation van apparaten wordt weergegeven.  

In Configuration Manager Health Attestation van apparaten wordt het volgende weergegeven:  

-   **Status Health Attestation** : geeft het aantal apparaten weer met een compatibele, niet-compatibele, onjuiste of onbekende status  
-   **Health Attestation-apparaatrapportage** : geeft het aantal apparaten weer waarvan de Health Attestation-status is gerapporteerd  
-   **Niet-compatibele apparaten op clienttype** : geeft het aantal mobiele apparaten en computers weer die niet compatibel zijn  
-   **Instellingen voor bovenste ontbrekende Health Attestation** : geeft het aantal apparaten weer waarvan de Health Attestation-instelling ontbreekt, weergegeven per instelling
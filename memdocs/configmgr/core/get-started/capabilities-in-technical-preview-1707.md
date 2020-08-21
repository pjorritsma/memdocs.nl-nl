---
title: Technical Preview 1707
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview-versie 1707 voor Configuration Manager.
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 6ff280a01b7388f3e4d296625a94c0184a0e6b09
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692975"
---
# <a name="capabilities-in-technical-preview-1707-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1707 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1707. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md) om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Bekende problemen in deze technische preview:**
- **Update voor preview versie 1707 mislukt wanneer u een site server in de passieve modus hebt**. Wanneer u de preview-versie 1706 uitvoert en een [primaire site server in de passieve modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)hebt, moet u de site server van de passieve modus verwijderen voordat u uw preview-site kunt bijwerken naar versie 1707. U kunt de site server van de passieve modus opnieuw installeren nadat versie 1707 van de site is uitgevoerd.

  De site server van de passieve modus verwijderen:
  1. Ga in de-console naar **beheer**  >  **overzicht**  >  **site configuratie**  >  **servers en site systeem rollen**en selecteer vervolgens de site server passieve modus.
  2. Klik in het deel venster **site systeem rollen** met de rechter muisknop op de **site** serverrol en kies vervolgens **rol verwijderen**.
  3. Klik met de rechter muisknop op de site server in de passieve modus en kies **verwijderen**.
  4. Nadat de installatie van de site server ongedaan is gemaakt, start u de service **CONFIGURATION_MANAGER_UPDATE**opnieuw op de actieve primaire site server.



**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Ondersteuning van peer-cache voor clients voor bestanden voor snelle installatie voor Windows 10 en Office 365
<!-- 1352486 -->
Vanaf deze release ondersteunt peer-cache distributie van inhoud snelle installatie bestanden voor Windows 10 en van update bestanden voor Office 365. Er zijn geen aanvullende configuraties vereist.

## <a name="surface-device-dashboard"></a>Surface Device-dash board
<!--1355788-->
Het Surface Device-dash board bevat informatie over de Surface-apparaten die in uw omgeving zijn gevonden. Ga in de-console naar **bewakings**  >  **oppervlak apparaten**. U kunt het volgende bekijken:
- percentage van Opper vlakken
- percentage Surface-modellen
- Top vijf versies van besturings systemen

Klik op een gedeelte van het diagram **Surface Models** voor een volledige lijst met apparaten.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Windows Defender Application Guard-beleid configureren en implementeren
<!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) is een nieuwe Windows-functie waarmee u uw gebruikers kunt beschermen door niet-vertrouwde websites te openen in een beveiligde geïsoleerde container die niet toegankelijk is voor andere onderdelen van het besturings systeem. In deze Technical Preview hebt u ondersteuning toegevoegd om deze functie te configureren met behulp van Configuration Manager nalevings instellingen die u configureert, en vervolgens implementeert u deze in een verzameling. Deze functie wordt uitgebracht als Preview voor de 64-bits versie van de update van Windows 10 over het najaar van de maker (code code: RS3). Als u deze functie nu wilt testen, moet u een preview-versie van deze update gebruiken.

### <a name="before-you-start"></a>Voordat u begint

Als u Windows Defender Application Guard-beleid wilt maken en implementeren, moeten de Windows 10-apparaten waarop u het beleid implementeert, worden geconfigureerd met een netwerk isolatie beleid. Zie [dit blog bericht](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)voor meer informatie. Deze functie werkt alleen met huidige Windows 10 Insider-builds. Om het te testen, moeten uw clients een recente Windows 10 Insider-build uitvoeren.

### <a name="try-it-out"></a>Probeer het nu!

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Een beleid maken en bladeren door de beschik bare instellingen:

1. Kies in de Configuration Manager-console **activa en naleving**.
2. Kies **overzicht**Endpoint Protection **Assets and Compliance**  >  **Endpoint Protection**  >  **Windows Defender Application Guard**in de werk ruimte activa en naleving.
3. Klik op het tabblad **Start** in de groep **maken** op **Windows Defender Application Guard-beleid maken**.
4. Als u het blog bericht als referentie wilt gebruiken, kunt u door de beschik bare instellingen bladeren en deze configureren om de functie uit te proberen.
5. In deze release hebben we de nieuwe **netwerk definitie** pagina aan de wizard toegevoegd. Op deze pagina geeft u de bedrijfs identiteit op en definieert u de grens van uw bedrijfs netwerk.<br>Windows 10-Pc's slaan slechts één netwerk isolatie lijst op de client op. In deze release kunt u twee verschillende soorten netwerk isolatie lijsten maken (één van Windows Information Protection en één van Windows Defender Application Guard) en implementeren op de client. Als u beide beleids regels implementeert, moeten deze netwerk isolatie lijsten overeenkomen. Als u lijsten implementeert die niet overeenkomen met dezelfde client, mislukt de implementatie.
Meer informatie over het opgeven van netwerk definities vindt u in de [documentatie van Windows Information Protection](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Wanneer u klaar bent, voltooit u de wizard en implementeert u het beleid op een of meer Windows 10-apparaten.

### <a name="further-reading"></a>Meer lezen
Zie [dit blog bericht](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)voor meer informatie over Windows Defender Application Guard. Zie [dit blog bericht](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)voor meer informatie over de zelfstandige Windows Defender Application Guard-modus.

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Para meters toevoegen wanneer u Power shell-scripts van Configuration Manager implementeert

<!-- 1236459 --->

In de laatste technische preview hebt u een nieuwe mogelijkheid geïntroduceerd waarmee u [Power shell-scripts kunt maken en uitvoeren vanuit de Configuration Manager-console](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
In deze Technical Preview zijn deze mogelijkheden uitgebreid. Configuration Manager leest nu het Power shell-script en geeft alle para meters weer in de wizard script maken. U kunt een waarde opgeven voor de para meter in de wizard die wordt gebruikt wanneer het script wordt uitgevoerd. U kunt de para meter ook leeg laten. Als u dit doet, moet u een waarde opgeven voor de para meter bij het uitvoeren van het script.
In deze Technical Preview moet u para meters opgeven die voor een script nodig zijn. In een toekomstige versie moeten we het aanleveren van script parameters optioneel maken.

### <a name="try-it-out"></a>Probeer het nu!

1. Volg de instructies om [Power shell-scripts te maken en uit te voeren vanuit de Configuration Manager-console](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
2. Kies op de pagina nieuwe **script parameters** van de **wizard script maken**een para meter en klik vervolgens op **bewerken**.
3. Geef een parameter waarde op voor de geselecteerde para meter en klik vervolgens op **OK**.
4. Voltooi de wizard.

Wanneer het script wordt uitgevoerd, worden alle parameter waarden gebruikt die u hebt geconfigureerd.
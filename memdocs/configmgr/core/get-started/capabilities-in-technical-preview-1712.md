---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview-versie 1712 voor Configuration Manager.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 65e0a1f39cb4347b78c8c10186df7be4aa527bea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721274"
---
# <a name="capabilities-in-technical-preview-1712-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1712 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1712. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. 

Bekijk de [technische preview voor Configuration Manager](technical-preview.md) voordat u deze versie van de Technical Preview installeert. In dit artikel wordt u vertrouwd met de algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Bekende problemen in deze technische preview:**
- **Bijwerken naar een nieuwe preview-versie mislukt wanneer u een site server in de passieve modus hebt**. Als u een [primaire site server in de passieve modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)hebt, moet u de site server van de passieve modus verwijderen voordat u de nieuwe preview-versie bijwerkt. U kunt de site server van de passieve modus opnieuw installeren nadat de update door de site is voltooid.

  De site server van de passieve modus verwijderen:
  1. Ga in de Configuration Manager-console naar **beheer** > **overzicht** > **site configuratie** > **servers en site systeem rollen**en selecteer vervolgens de site server passieve modus.
  2. Klik in het deel venster **site systeem rollen** met de rechter muisknop op de **site** serverrol en kies vervolgens **rol verwijderen**.
  3. Klik met de rechter muisknop op de site server in de passieve modus en kies **verwijderen**.
  4. Nadat de installatie van de site server ongedaan is gemaakt, start u de service **CONFIGURATION_MANAGER_UPDATE**opnieuw op de actieve primaire site server.
  <!--sms489412-->


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Vervangen toepassingen niet automatisch bijwerken
<!-- 1351266 -->
Op basis van [feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior)van de gebruiker, in deze release, hebt u de optie om een toepassings implementatie te configureren om te voor komen dat vervangen versie automatisch wordt bijgewerkt. Wanneer u de implementatie nu maakt, kunt u op de pagina **implementatie-instellingen** van de **wizard software implementeren**voor **beschikbaar** of **vereist** installatie doel de optie voor het **automatisch bijwerken van vervangen versies van deze toepassing**in-of uitschakelen.


## <a name="install-multiple-applications-in-software-center"></a>Meerdere toepassingen installeren in Software Center
<!-- 1357126 -->
Als een eind gebruiker of een desktop technicus meerdere toepassingen op een apparaat moet installeren, ondersteunt Software Center nu het installeren van meerdere geselecteerde toepassingen. Hierdoor is de gebruiker efficiënter en wordt niet gewacht totdat de ene installatie is voltooid voordat de volgende wordt gestart.

Wanneer u de modus voor meervoudige selectie op het tabblad **toepassingen** gebruikt, bepalen de volgende criteria welke apps Software Center geschikt is voor meervoudige selectie:
- De app is zichtbaar voor de gebruiker
- De app is niet al geïnstalleerd
- Goed keuring van de beheerder is niet vereist of is al verleend
- De status van de app is beschikbaar (bijvoorbeeld niet al downloadt inhoud)

### <a name="try-it-out"></a>Probeer het nu!
**In de Configuration Manager-console:** Implementeren op een gebruiker of apparaat meerdere toepassingen voor installatie, als beschikbaar of vereist (met de deadline in de toekomst). Goed keuring door de beheerder is niet vereist. Zie [toepassingen implementeren](../../apps/deploy-use/deploy-applications.md)voor meer informatie.

**In Software Center:**
 1. Het tabblad **toepassingen** wordt standaard geopend. 
 2. Als u de modus voor meervoudige selectie in de lijst weergave wilt openen, klikt u op het pictogram Nieuw ![Pictogram Software Center multi-select](media/software-center-multi-select-apps.png) in de rechter bovenhoek.
 3. Selecteer twee of meer apps die u wilt installeren door te klikken op het selectie vakje links van de apps in de lijst.
 4. Klik op de knop **geselecteerde items installeren** .

De apps worden zo normaal geïnstalleerd, maar nu na elkaar.


## <a name="client-based-pxe-responder-service"></a>PXE-responder-service op basis van client
<!-- 1357148 -->
Een veelvoorkomende uitdaging voor klanten is het leveren van PXE-Services op externe kant oren of filialen met weinig of geen server infrastructuur. De distributiepuntrol ondersteunt client besturingssystemen, maar kan niet worden ingeschakeld voor PXE vanwege de afhankelijkheid van Windows Deployment Services.

Er zijn nu nieuwe client instellingen beschikbaar om een PXE-responder-service op Configuration Manager-clients in te scha kelen. Een opstart installatie kopie met PXE-functionaliteit moet zich bevinden in de client cache van de PXE-responder.

### <a name="try-it-out"></a>Probeer het nu!
Zorg ervoor dat er geen bestaande distributie punten met PXE-functionaliteit of andere PXE-servers in de test omgeving zijn die kunnen conflicteren met deze client PXE-responder.

In de Configuration Manager-console:
1. In de werk ruimte **software bibliotheek** onder **besturings systemen**, **taken reeksen**: een taken reeks maken met behulp van de aangepaste sjabloon.
   1. Klik op **toevoegen**, selecteer **Algemeen**en klik vervolgens op de stap **taken reeks variabele instellen** . Voer **smstspersiscontent** in als de taken reeks variabele en voer de waarde **waar**in.
   1. Klik op **toevoegen**, selecteer **Software**en vervolgens de stap **pakket inhoud downloaden** . Klik op het gouden sterretje en selecteer vervolgens een opstart installatie kopie met PXE-functionaliteit. Zowel x86-als x64-opstart installatie kopieën bevatten. Configureer de stap om deze in de **Configuration Manager-client cache**te plaatsen.
   1. Klik op **toevoegen**, selecteer **Algemeen**en klik vervolgens op de stap **taken reeks variabele instellen** . Voer **SMSTSPreserveContent** in als de taken reeks variabele en voer de waarde **waar**in.
2. In de werk ruimte **beheer** onder **client instellingen**: Maak een aangepast beleid voor client Apparaatinstellingen.
   1. Selecteer de **client cache-instellingen** groep.
   1. Stel de instelling **Configuration Manager-client inschakelen in volledig besturings systeem in voor het delen van inhoud** in op **Ja**.
   1. Stel de service-instelling voor **PXE-Responder inschakelen** in op **Ja**.
   1. Klik voor de instelling **een zelfondertekend certificaat maken of een PKI-client certificaat importeren** op **een certificaat opgeven**. Selecteer **certificaat importeren** als uw test omgeving PKI heeft, anders klikt u op **OK** om een zelfondertekend certificaat te maken. 
   1. Configureer zo nodig de resterende instellingen voor uw test omgeving. (De standaard instellingen moeten werken tenzij er specifieke netwerk-of beveiligings vereisten zijn.)
3. Implementeer de taken reeks en aangepaste client instellingen voor een verzameling van doel clients om PXE-responders te zijn. Wacht totdat het beleid is toegepast en de taken reeks wordt uitgevoerd.
4. Start een andere client op hetzelfde subnet naar PXE/Network boot als normaal.

### <a name="known-issues"></a>Bekende problemen
- De taken reeks editor geeft een rood fout pictogram weer voor de stap **pakket inhoud downloaden** wanneer u een opstart installatie kopie toevoegt, maar de taken reeks wordt opgeslagen. Als u deze taken reeks opnieuw opent in de editor, ziet u ook een onschadelijke waarschuwing dat er geen objecten kunnen worden gevonden. <!-- sms427542 -->
- De opstart installatie kopie van de stap pakket inhoud downloaden wordt niet weer gegeven in de lijst met verwijzingen van de aangepaste taken reeks. De actie **inhoud distribueren** is ook niet beschikbaar. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Wijziging in de installatie van de Configuration Manager-client  
Als gevolg van de feedback van uw gebruikers [worden Silverlight niet meer automatisch geïnstalleerd op clients.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Overschakelen naar het Surface Device-dash board
Het Surface-dash board geeft nu firmware versies weer voor Surface-apparaten in plaats van de versie van het besturings systeem. Ga in de-console naar **bewakings** > **oppervlak apparaten**. U kunt de volgende items bekijken:
- Percentage van Opper vlakken
- Percentage Surface-modellen
- Top vijf van firmware versies
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Verbeteringen aan Office 365-dash board voor client beheer 
Het Office 365-client beheer dashboard geeft nu een lijst met relevante apparaten weer wanneer secties van de grafiek worden geselecteerd. Ga in de-console naar **software bibliotheek** >**Overview** >**Office 365 client management**. Het dash board wordt aan de rechter kant weer gegeven. Als u criteria in de grafiek selecteert, wordt een lijst met apparaten weer gegeven.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Verbeteringen in de Configuration Manager-console 
We hebben de volgende verbeteringen aangebracht in de Configuration Manager-console, die het resultaat zijn van de feedback van uw gebruikers stem.

- In de [lijst met apparaten wordt de primaire gebruiker weer gegeven](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): apparaten lijsten onder activa en naleving, apparaten, nu standaard de primaire gebruiker weer geven. De laatst aangemelde gebruiker kan ook worden toegevoegd als een optionele kolom. <!-- 1357280 -->
- [Hernoemde verzamelingen worden weer gegeven in bestaande regels voor verzamelings lidmaatschap](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): als een verzameling lid is van een andere verzameling en de naam ervan wordt gewijzigd, wordt de nieuwe naam bijgewerkt onder de lidmaatschaps regels.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Verbeteringen in de implementatie van besturings systemen
We hebben de volgende verbeteringen aangebracht in de implementatie van het besturings systeem, wat het resultaat was van de feedback van uw gebruikers stem.
- [Standaard logboek-viewer in opstart installatie kopie](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a): in Windows PE wordt bij het starten van cmtrace. exe niet meer gevraagd of u dit programma wilt instellen als de standaard viewer voor logboek bestanden. <!-- SMS 500897 -->
- Stap pakket inhoud downloaden: u kunt nu opstart installatie kopieën toevoegen aan deze taken reeks stap.


## <a name="windows-10-feedback-hub-app-integration"></a>Windows 10 feedback hub-integratie van apps

We hebben graag feedback, zodat we nu feedback kunnen geven via de ingebouwde [app feedback hub](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) van Windows 10. Wanneer u **nieuwe feedback toevoegt**, moet u ervoor zorgen dat u de categorie **ondernemings beheer** selecteert en vervolgens een van de volgende subcategorieën kiest:
- Configuration Manager-client
- Configuration Manager-Console
- Implementatie van Configuration Manager besturings systeem
- Configuration Manager server

Ga door met onze [gebruikers spraak pagina](https://configurationmanager.uservoice.com/) om te stemmen met nieuwe ideeën voor functies in Configuration Manager.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Volgende stappen
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking.    

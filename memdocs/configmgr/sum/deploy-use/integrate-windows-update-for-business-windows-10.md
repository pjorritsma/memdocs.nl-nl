---
title: Windows Update voor bedrijven integreren
titleSuffix: Configuration Manager
description: Gebruik Windows Update voor bedrijven (WUfB) om Windows 10 up-to-date te houden voor apparaten die zijn verbonden met de Windows Update-service.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 51e64f8f815c4ba90522acf6529cff4d971dd553
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699803"
---
# <a name="integrate-with-windows-update-for-business"></a>Integreren met Windows Update voor bedrijven

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met Windows Update voor bedrijven (WUfB) kunt u Windows 10-apparaten in uw organisatie altijd up-to-date houden met de nieuwste beveiligings beveiligingen en Windows-onderdelen wanneer deze apparaten rechtstreeks verbinding maken met de service van Windows Update (WU). Configuration Manager kan onderscheid maken tussen Windows 10-computers die gebruikmaken van WUfB en WSUS voor het ophalen van software-updates.  

> [!WARNING]
> Als u co-beheer gebruikt voor uw apparaten en u het [Windows Update-beleid](../../comanage/workloads.md#windows-update-policies) naar intune hebt verplaatst, krijgen uw apparaten de [Windows Update voor bedrijfs beleid van intune](/intune/windows-update-for-business-configure).
> - Als de Configuration Manager-client nog steeds is geïnstalleerd op het door co beheerde apparaat, worden de instellingen voor cumulatieve updates en functie-updates beheerd door intune. Patching van derden, als dit is ingeschakeld in de [**client instellingen**](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates), wordt echter nog steeds beheerd door Configuration Manager.  

 Sommige Configuration Manager-functies zijn niet meer beschikbaar wanneer Configuration Manager-clients zijn geconfigureerd voor het ontvangen van updates van WU, waaronder WUfB of Windows insiders:  

- Windows Update-nalevingsrapportages:  
  - Configuration Manager is niet op de hoogte van de updates die naar WU worden gepubliceerd. Met de Configuration Manager-clients die zijn geconfigureerd om updates te ontvangen van WU, wordt voor deze updates **onbekend** weer gegeven in de Configuration Manager-console.  

  - Het oplossen van problemen met de algehele compatibiliteits status is lastig, omdat een **onbekende** status alleen is voor de clients die de scan status van WSUS niet had hebben gerapporteerd. Het bevat nu ook Configuration Manager-clients die updates van WU ontvangen.  

  - Naleving van definitie-updates maakt deel uit van de algehele rapportage van update naleving en werkt niet zoals verwacht.

- Algemene Endpoint Protection rapportage voor Defender op basis van de status van de update naleving retourneert geen nauw keurige resultaten vanwege de ontbrekende scan gegevens.  

- Configuration Manager kunt geen micro soft-updates implementeren, zoals Microsoft 365 apps, IE en Visual Studio naar clients die zijn verbonden met WUfB voor het ontvangen van updates.  

- Configuration Manager kunt nog steeds updates van derden implementeren die zijn gepubliceerd in WSUS en via Configuration Manager worden beheerd naar clients die zijn verbonden met WUfB voor het ontvangen van updates. Als u niet wilt dat er updates van derden worden geïnstalleerd op clients die verbinding maken met WUfB, schakelt u de client instelling [software-updates op clients inschakelen](../../core/clients/deploy/about-client-settings.md#software-updates)uit.

- Configuration Manager volledige client implementatie die gebruikmaakt van de infra structuur voor software-updates, werkt niet voor clients die zijn verbonden met WUfB voor het ontvangen van updates.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Clients identificeren die gebruikmaken van WUfB voor Windows 10-updates

Gebruik de volgende procedure om clients te identificeren die gebruikmaken van WUfB voor het ophalen van updates en upgrades voor Windows 10. Configureer deze clients vervolgens zodanig dat WSUS niet meer wordt gebruikt om updates op te halen en implementeer een instelling voor client agent om de werk stroom voor software-updates voor deze clients uit te scha kelen.  

### <a name="prerequisites-for-wufb"></a>Vereisten voor WUfB

- Clients met Windows 10 Desktop Pro of Windows 10 Enterprise Edition versie 1511 of hoger

- [Windows Update voor bedrijven](/windows/deployment/update/waas-manage-updates-wufb) wordt geïmplementeerd en clients gebruiken WUfB om Windows 10-updates en -upgrades op te halen.  

### <a name="to-identify-clients-that-use-wufb"></a>Clients identificeren die gebruikmaken van WUfB  

1. Zorg ervoor dat de Windows Update Agent niet scant op WSUS, als deze eerder was ingeschakeld. De volgende register sleutel kan worden gebruikt om aan te geven of de computer scant op WSUS of Windows Update. Als de register sleutel niet bestaat, wordt deze niet gescand met WSUS.
    - **HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**
1. Er is een nieuw kenmerk, **UseWUServer**, onder het knoop punt **Windows Update** in Configuration Manager resource Explorer.
1. Maak een verzameling op basis van het **UseWUServer** -kenmerk voor alle computers die via WUfB zijn verbonden voor updates en upgrades. U kunt een verzameling maken op basis van een query die er ongeveer als volgt uitziet:  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. Maak een client agent-instelling om de werk stroom voor software-updates uit te scha kelen. Implementeer de instelling op de verzameling van computers die rechtstreeks zijn verbonden met WUfB.
1. Op de computers die via WUfB worden beheerd, wordt **onbekend** weer gegeven in de compatibiliteits status en worden niet geteld als onderdeel van het algehele compatibiliteits percentage.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Windows Update voor beleid voor bedrijfs uitstel configureren
<!-- 1290890 -->
Vanaf Configuration Manager versie 1706 kunt u uitstel beleid configureren voor Windows 10-onderdelen updates of kwaliteits updates voor Windows 10-apparaten die rechtstreeks worden beheerd door Windows Update voor bedrijven. U kunt het uitstel beleid beheren in het knoop punt nieuwe **Windows Update voor bedrijfs beleid** onder **software bibliotheek**  >  **Windows 10 Servicing**.

> [!NOTE]
> Vanaf Configuration Manager versie 1802 kunt u uitstel beleid voor Windows Insider instellen. <!--507201-->  
Zie aan de slag [met Windows Insider Program for Business](/windows/deployment/update/waas-windows-insider-for-business)voor meer informatie over het Windows Insider-programma.

### <a name="prerequisites-for-deferral-policies"></a>Vereisten voor uitstel beleid

- Windows 10 versie 1703 of hoger
- Windows 10-apparaten die worden beheerd door Windows Update voor bedrijven, moeten een Internet verbinding hebben

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Een Windows Update voor beleid voor bedrijfs uitstel maken

1. In **software bibliotheek**  >  **Windows 10-onderhouds**  >  **Windows Update voor bedrijfs beleid**
1. Selecteer op het tabblad **Start** in de groep **maken** de optie **Windows Update maken voor bedrijfs beleid** om de wizard Windows Update voor bedrijven-beleid maken te openen.
1. Geef op de pagina **Algemeen** een naam en beschrijving voor het beleid op.
1. Configureer op de pagina **uitstel beleid** of functie-updates moeten worden uitstellen of onderbroken. Upgrades van onderdelen zijn over het algemeen nieuwe functies van Windows. Nadat u de instelling voor het niveau van de **Branch-gereedheid** hebt geconfigureerd, kunt u opgeven of en hoe lang u de ontvangst van onderdelen wilt uitstellen na hun Beschik baarheid van micro soft.
    - **Branche gereedheids niveau**: Stel de vertakking in waarvoor het apparaat Windows-updates zal ontvangen. Kies een semi-Annual-kanaal (targeted), semi-Annual-kanaal of een Windows Insider-build.

        > [!NOTE]
        > Beleid voor **Semi-Annual-kanaal (targeted)** implementeren in Windows 10, *versie 1903 of hoger*. Beleids regels implementeren voor **Semi-Annual-kanaal** naar Windows 10, *versie 1809 of eerder*.
        >
        > Als u een beleid voor **Semi-Annual-kanaal** implementeert in Windows 10, versie 1903 of hoger, mislukt de implementatie met de fout **0x8004100c**.<!-- 5593139 -->

    - **Uitstel periode (dagen)**: Geef het aantal dagen op waarvoor updates van onderdelen worden uitgesteld. U kunt het ontvangen van deze onderdelen updates uitstellen tot 365 dagen vanaf de release.
    - **Onderbreken van onderdelen updates starten**: Selecteer of u wilt onderbreken dat apparaten maxi maal 35 dagen worden ontvangen vanaf het moment dat u de updates onderbreekt. Als het maximum aantal dagen is verstreken, verloopt de functionaliteit voor onderbreken automatisch en zoekt het apparaat in Windows-Updates naar toepasselijke updates. Na deze scan kunt u de updates opnieuw onderbreken. U kunt de onderbreking van de functie-updates uitschakelen door het selectie vakje uit te scha kelen.
1. Kies of u kwaliteits updates wilt uitstellen of onderbreken. Kwaliteitsupdates zijn doorgaans oplossingen en verbeteringen in de bestaande Windows-functionaliteit. Deze worden normaal gesproken op de eerste dinsdag van elke maand gepubliceerd, maar kunnen op elk gewenst moment door Microsoft worden vrijgegeven. U kunt opgeven of, en hoe u de installatie van kwaliteitsupdates wilt uitstellen na hun beschikbaarheid.
    - **Uitstel periode (dagen)**: Geef het aantal dagen op dat kwaliteits updates moeten worden uitgesteld. U kunt het ontvangen van deze kwaliteits updates uitstellen gedurende Maxi maal 30 dagen vanaf de release.
    - Het **starten van kwaliteits updates onderbreken**: Selecteer of u wilt onderbreken dat apparaten maxi maal 35 dagen na het pauzeren van de updates worden ontvangen van kwaliteits updates. Als het maximum aantal dagen is verstreken, verloopt de functionaliteit voor onderbreken automatisch en zoekt het apparaat in Windows-Updates naar toepasselijke updates. Na deze scan kunt u de updates opnieuw onderbreken. U kunt de kwaliteit van de kwaliteits updates verwijderen door het selectie vakje uit te scha kelen.
1. Selecteer **updates van andere micro soft-producten installeren** om de groeps beleids instelling in te scha kelen waarmee uitstel instellingen worden ingesteld die van toepassing zijn op Microsoft Update, evenals Windows-updates.
1. Selecteer **Stuur Programma's insluiten met Windows Update** om stuur Programma's automatisch bij te werken van Windows-updates. Als u deze instelling uitschakelt, worden stuur programma-updates niet gedownload van Windows-updates.
1. Voltooi de wizard om het nieuwe uitstel beleid te maken.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Een Windows Update voor beleid voor bedrijfs uitstel implementeren

1. In **software bibliotheek**  >  **Windows 10-onderhouds**  >  **Windows Update voor bedrijfs beleid**
1. Selecteer op het tabblad **Start** in de groep **implementatie** de optie **Windows Update implementeren voor bedrijfs beleid**.
1. Configureer de volgende instellingen:
    - **Te implementeren configuratie beleid**: selecteer de Windows Update voor bedrijfs beleid dat u wilt implementeren.
    - **Verzameling**: Klik op **Bladeren** om de verzameling te selecteren waarvoor u het beleid wilt implementeren.
    - **Herstel toestaan buiten het onderhouds venster**: als er een onderhouds venster is geconfigureerd voor de verzameling waarnaar u het beleid implementeert, schakelt u deze optie in om de waarde buiten het onderhouds venster te laten herstellen met beleids instellingen. Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.
    - **Planning**: Geef het evaluatie schema voor naleving op waarmee het geïmplementeerde beleid wordt geëvalueerd op client computers. U kunt een eenvoudig of aangepast schema opgeven.
1. Voltooi de wizard om het beleid te implementeren.
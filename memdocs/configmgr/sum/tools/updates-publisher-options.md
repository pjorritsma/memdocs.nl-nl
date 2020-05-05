---
title: Opties configureren
titleSuffix: Configuration Manager
description: Opties configureren voor het gebruik van System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b6578e32d5ae5a003c485960b556f3b87e8d557
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717725"
---
# <a name="configure-options-for-updates-publisher"></a>Opties configureren voor updates Publisher

*Van toepassing op: System Center Updates Publisher*

Bekijk en configureer de opties en gerelateerde instellingen die van invloed zijn op de werking van updates Publisher.

Als u de Publisher-opties voor updates wilt gebruiken, klikt u in de linkerbovenhoek van de console op het tabblad **updates Publisher** - **Eigenschappen** en kiest u vervolgens **Opties**.

![Opties](media/properties1.png)   


De opties zijn onderverdeeld in het volgende:

-   Update Server
-   ConfigMgr-server
-   Proxy-instellingen
-   Vertrouwde uitgevers
-   Geavanceerd
-   Updates
-   Logboekregistratie

## <a name="update-server"></a>Update Server
U moet updates Publisher configureren om te werken met update server als Windows Server Update Services (WSUS) voordat u [updates kunt publiceren](manage-updates-with-updates-publisher.md#publish-updates-and-bundles-from-the-updates-workspace). Dit omvat het opgeven van de server, de methoden om verbinding te maken met die server wanneer deze extern is van de-console en een certificaat voor het digitaal ondertekenen van updates die u publiceert.

- **Configureer een update server**. Wanneer u een update server configureert, selecteert u de WSUS-server op het hoogste niveau (update server) in uw Configuration Manager-hiërarchie zodat alle onderliggende sites toegang hebben tot de updates die u publiceert.

  Als uw update server extern is van uw updates Publisher-server, geeft u de Fully Qualified Domain Name (FQDN) van de-server op en als u verbinding maakt via SSL. Wanneer u verbinding maakt via SSL, verandert de standaard poort van 8530 in 8531. Zorg ervoor dat de poort die u hebt ingesteld, overeenkomt met wat wordt gebruikt door de update server.

  > [!TIP]  
  > Als u geen update server configureert, kunt u nog steeds updates Publisher gebruiken om software-updates te schrijven.

- **Het handtekening certificaat configureren**. U moet een update server configureren en verbinding laten maken voordat u het handtekening certificaat kunt configureren.

  Updates Publisher gebruikt het handtekening certificaat voor het ondertekenen van de software-updates die op de update server zijn gepubliceerd. Publiceren mislukt als het digitale certificaat niet beschikbaar is in het certificaat archief van de update server of de computer waarop updates Publisher wordt uitgevoerd.

  Zie [certificaten en beveiliging voor updates Publisher](updates-publisher-security.md)voor meer informatie over het toevoegen van het certificaat aan het certificaat archief.

  Als een digitaal certificaat niet automatisch wordt gedetecteerd voor de update server, kiest u een van de volgende opties:

  -   **Bladeren**: bladeren is alleen beschikbaar wanneer de update server is geïnstalleerd op de server waarop u de-console uitvoert. Nadat u een certificaat hebt geselecteerd, moet u **maken** kiezen om dat certificaat toe te voegen aan het WSUS-certificaat archief op de update server. U moet het **PFX** -bestands wachtwoord opgeven voor certificaten die u door deze methode selecteert.

  -   **Maken:** Gebruik deze optie om een nieuw certificaat te maken. Hiermee wordt ook het certificaat toegevoegd aan het WSUS-certificaat archief op de update server.

  **Als u uw eigen handtekening certificaat maakt**, configureert u het volgende:

  -   Schakel de optie **persoonlijke sleutel mag worden geëxporteerd** in.

  -   Stel het **sleutel gebruik** in op digitale hand tekening.

  -   Stel de **minimale sleutel grootte** in op een waarde die gelijk is aan of groter is dan 2048 bits.

  Gebruik de optie **verwijderen** om een certificaat uit het WSUS-certificaat archief te verwijderen. Deze optie is beschikbaar wanneer de update server lokaal is voor de updates Publisher-console die u gebruikt, of wanneer u **SSL** gebruikt om verbinding te maken met een externe update server.

## <a name="configmgr-server"></a>ConfigMgr-server
Gebruik deze opties wanneer u Configuration Manager gebruikt met updates Publisher.

-   **Geef de Configuration Manager server op:** Nadat u ondersteuning voor Configuration Manager hebt ingeschakeld, geeft u de locatie van de site server op het hoogste niveau op uit uw Configuration Manager hiërarchie. Als die server extern is van de updates Publisher installeren, geeft u de FQDN van de site server op. Kies **verbinding testen** om te controleren of u verbinding kunt maken met de site server.

-   **Drempel waarden configureren:** Er worden drempel waarden gebruikt wanneer u updates publiceert met het publicatie type automatisch. De drempel waarden helpen te bepalen wanneer de volledige inhoud voor een update wordt gepubliceerd in plaats van alleen de meta gegevens. Zie [updates toewijzen aan een publicatie](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) voor meer informatie over de verschillende typen publicaties

    U kunt een of beide van de volgende drempel waarden opgeven:

    -   **Drempel waarde voor aantal aangevraagde clients:** Hiermee definieert u hoeveel clients een update moeten aanvragen vóór updates Publisher kan de volledige set met inhoud voor die update automatisch publiceren. Totdat het opgegeven aantal clients de update aanvraagt, worden alleen de meta gegevens van de updates gepubliceerd.

    -   **Drempel waarde voor pakket bron grootte (MB):** Hiermee wordt voor komen dat updates die groter zijn dan de grootte die u opgeeft, automatisch worden gepubliceerd. Als de grootte van de updates deze waarde overschrijdt, worden alleen de meta gegevens gepubliceerd. Voor updates die kleiner zijn dan de opgegeven grootte, kan de volledige inhoud worden gepubliceerd.

## <a name="proxy-settings"></a>Proxy-instellingen
Updates Publisher gebruikt de proxy-instellingen wanneer u software catalogussen van Internet importeert of updates op internet publiceert.

-   Geef de FQDN of het IP-adres van een proxy server op. IPv4 en IPv6 worden ondersteund.

-   Als de proxy server gebruikers verifieert voor Internet toegang, moet u de Windows-naam opgeven. Een universele principle-naam (UPN) wordt niet ondersteund.

## <a name="trusted-publishers"></a>Vertrouwde uitgevers
Wanneer u een Update catalogus importeert, wordt de bron van die catalogus (op basis van het certificaat) toegevoegd als een vertrouwde uitgever. En wanneer u een update publiceert, wordt de bron van het updates certificaat toegevoegd als een vertrouwde uitgever.

U kunt certificaat gegevens weer geven voor elke uitgever en een uitgever verwijderen uit de lijst met vertrouwde uitgevers.

Inhoud van uitgevers die niet worden vertrouwd, kan schadelijk zijn voor client computers wanneer de client op updates scant. U moet alleen inhoud accepteren van uitgevers die u vertrouwt.

## <a name="advanced"></a>Geavanceerd
Geavanceerde opties zijn onder meer de volgende:

-   **Locatie van opslag plaats:** Bekijk en wijzig de locatie van het database bestand, **scupdb. sdf**. Dit bestand is de opslag plaats voor updates Publisher.

-   **Tijds tempel:** Wanneer deze functie is ingeschakeld, wordt er een tijds tempel toegevoegd aan de updates die worden geïdentificeerd wanneer het is ondertekend. Een update die is ondertekend terwijl een certificaat geldig was, kan worden gebruikt nadat het handtekening certificaat is verlopen. Standaard kunnen software-updates niet worden geïmplementeerd nadat het handtekening certificaat is verlopen.

-   **Controleren op updates voor geabonneerde catalogi:** Telkens wanneer de updates van Publisher worden gestart, kan deze automatisch controleren op updates voor catalogi waarop u bent geabonneerd. Wanneer een catalogus update wordt gevonden, worden de details als **recente waarschuwingen** vermeld in het venster **overzicht** van de **werk ruimte updates**.

-   **Intrekken van certificaten:** Selecteer deze optie om certificaat intrekkings controles in te scha kelen.

-   **Lokale publicatie van de bron:** Updates Publisher kan gebruikmaken van een lokale kopie van een update die u publiceert voordat u die update downloadt van Internet. De locatie moet een map zijn op de computer waarop updates Publisher wordt uitgevoerd. Deze locatie is standaard **mijn Documents\LocalSourcePublishing.** Gebruik dit wanneer u eerder een of meer updates hebt gedownload of wijzigingen hebt aangebracht in een update die u wilt implementeren.

-   **Wizard voor het opruimen van software-updates:** Start de wizard updates opruimen. De wizard verloopt updates op de update server, maar niet in de updates voor de Publisher-opslag plaats. Zie [verloopt niet-gerefereerde updates](#expire-unreferenced-software-updates) voor meer informatie.

## <a name="updates"></a>Updates
 Updates Publisher kan automatisch controleren op nieuwe updates telkens wanneer deze wordt geopend. U kunt ook kiezen om Preview-versies van updates Publisher te ontvangen.

Als u hand matig op updates wilt controleren, klikt u in de ![updates Publisher-console op Eigenschappen](media/properties2.png)  
om de **Eigenschappen van Publisher updates**te openen en kies vervolgens **controleren op update**.

Nadat updates in Publisher een nieuwe update heeft gevonden, wordt het venster **beschik bare update** weer gegeven en kunt u ervoor kiezen om het te installeren. Als u ervoor kiest om de update niet te installeren, wordt deze de volgende keer dat u de-console opent, aangeboden.

## <a name="logging"></a>Logboekregistratie
Updates Publisher registreert basis informatie over updates Publisher naar **%windir%\Temp\UpdatesPublisher.log**.

Gebruik Klad blok of **CMTrace** om het logboek weer te geven. CMTrace is het hulp programma Configuration Manager logboek bestand en is te vinden in de map **\SMSSetup\Tools** van de bron media Configuration Manager.

U kunt de grootte van het logboek en het detail niveau wijzigen.

Wanneer u database logboek registratie inschakelt, worden er gegevens opgenomen over de query's die worden uitgevoerd op de updates Publisher-data base. Het gebruik van database logboek registratie kan leiden tot verminderde prestaties van de updates Publisher-computer.

Als u het logboek bestand wilt weer geven, klikt u ![in](media/properties2.png) de-console op Eigenschappen om de **updates Publisher-eigenschappen**te openen en kiest u vervolgens **logboek bestand weer geven**.

## <a name="expire-unreferenced-software-updates"></a>Niet-referentie software-updates laten verlopen
U kunt de **wizard software-update opruiming** uitvoeren om updates te laten verlopen die zich op de update server bevinden, maar niet in de Publisher-opslag plaats voor updates. Hiermee wordt Configuration Manager gemeld dat deze updates vervolgens worden verwijderd uit toekomstige implementaties.

De handeling van het verlopen van een update kan niet ongedaan worden gemaakt. Voer deze taak alleen uit wanneer u zeker weet dat de software-updates die u selecteert, niet langer worden vereist door uw organisatie.

### <a name="to-remove-expired-software-updates"></a>Verlopen software-updates verwijderen
1.  Klik in de update Publisher-console op ![eigenschappen](media/properties2.png) om de **updates Publisher-eigenschappen**te openen en kies vervolgens **Opties**.

2.  Kies **Geavanceerd**en klik vervolgens onder **wizard software-update opschonen** op **Start**.

3.  Selecteer de software-updates die u wilt laten verlopen en klik vervolgens op **volgende**.

4.  Nadat u uw selecties hebt bekeken, kiest u **volgende** om de selecties te accepteren en deze updates te laten verlopen.

5.  Nadat de wizard is voltooid, kiest u **sluiten** om de wizard te volt ooien.

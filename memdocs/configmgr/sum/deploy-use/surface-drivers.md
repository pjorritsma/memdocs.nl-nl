---
title: Updates voor Surface drivers beheren
titleSuffix: Configuration Manager
description: Configuration Manager worden updates van Surface-Stuur Programma's gesynchroniseerd voor implementatie op Surface-apparaten.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: 6428b6e1992af6dbb1f6d49b9ef1eac3010dd833
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/09/2020
ms.locfileid: "84614981"
---
# <a name="manage-surface-drivers-with-configuration-manager"></a>Surface-Stuur Programma's beheren met Configuration Manager

*Van toepassing op: System Center Configuration Manager (Current Branch)*

Met System Center Configuration Manager kunt u stuur Programma's voor Surface-apparaten synchroniseren en implementeren zoals een software-update. Met deze functie kunt u ervoor zorgen dat op uw Surface-apparaten de meest recente beschik bare Stuur Programma's worden uitgevoerd. Deze synchronisatie is voor het eerst in versie 1706 geïntroduceerd als een voorlopige versie en de functie werd in 1710. <!--3684621, 3608197, 1098490-->

## <a name="prerequisites-for-synchronizing-surface-drivers"></a>Vereisten voor het synchroniseren van Surface-Stuur Programma's

- Een Internet verbonden software-update punt op het hoogste niveau.
- Alle software-update punten moeten Windows Server 2016 uitvoeren met de cumulatieve update KB4025339 of later geïnstalleerd.
- Configuration Manager schakelt deze optionele functie standaard niet in. Schakel deze functie in voordat u deze gebruikt. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="enable-sync-for-surface-drivers"></a>Synchronisatie inschakelen voor Surface-Stuur Programma's

Voer de volgende stappen uit om de synchronisatie van Surface-Stuur Programma's in te scha kelen:

1. Verbind de Configuration Manager-console met de site server op het hoogste niveau.
1. Ga naar **beheer**  >  **site configuratie**  >  **sites**en klik vervolgens op uw site op het hoogste niveau.
1. Selecteer in het lint **instellingen**  >  **configuratie site onderdelen**  >  **Software-update punt**.
1. Klik op het tabblad **classificaties** en klik vervolgens op het selectie vakje voor **micro soft Surface-Stuur Programma's en firmware-updates** en klik op **Toep assen**.

     ![Surface-Stuur Programma's inschakelen via de eigenschappen van het software-update punt](media/enable-surface-driver-sync.png)

1. Klik op het tabblad **producten** in de eigenschappen van de software-update punt component. Zie de secties [producten voor Surface-Stuur Programma's](#bkmk_prod) en [Surface-modellen](#bkmk_models) voor meer informatie.
1. Selecteer de producten voor elke versie van Windows 10 waarvoor u Surface drivers wilt ondersteunen. U ziet dat er twee verschillende versies van elk van de producten voor Stuur Programma's zijn:

   - Stuur Programma's voor Windows 10- *versie* - **Update en hoger**
   - Windows 10- *versie* - **Update en latere upgrade & onderhouds Stuur Programma's**.

     ![Product lijst met stuur Programma's voor Windows 10-versies](media/surface-driver-products-sup.png)

1. Wanneer u klaar bent met het selecteren van de producten, klikt u op **OK**.
1. [Synchroniseer het software-update punt](../get-started/synchronize-software-updates.md) om de Surface-Stuur programma's naar Configuration Manager te brengen.
1. Zodra de Surface-Stuur Programma's zijn gesynchroniseerd, implementeert u deze op dezelfde manier als u andere updates implementeert.

## <a name="products-for-surface-drivers"></a><a name="bkmk_prod"></a>Producten voor Surface-Stuur Programma's

De meeste Stuur Programma's horen bij de volgende product groepen:

- Stuur Programma's voor Windows 10 en hoger
- Windows 10 en latere upgrade & onderhouds Stuur Programma's
- Windows 10 jubileum update en latere onderhouds Stuur Programma's
- Windows 10 jubileum update en latere upgrade & onderhouds Stuur Programma's
- Windows 10 Crea tors update en latere onderhouds Stuur Programma's
- Windows 10 Crea tors update en latere upgrade & onderhouds Stuur Programma's
- Windows 10-onderhouds-en recentere Stuur Programma's bijwerken
- Windows 10-onderhouds werkzaamheden bijwerken en latere upgrade & onderhoud van Stuur Programma's
- Stuur Programma's voor Windows 10 S en later
- Windows 10 S versie 1709 en hoger voor het onderhouden van Stuur Programma's voor testen
- Windows 10 S versie 1709 en hoger upgrade & onderhouds Stuur Programma's voor testen
- Stuur Programma's voor Windows 10 S versie 1803 en hoger
- Windows 10 S versie 1803 en hoger upgrade & onderhouds Stuur Programma's
- Windows 10 S versie 1809 en hoger, onderhouds Stuur Programma's
- Windows 10 S versie 1809 en hoger, upgrade & onderhouds Stuur Programma's
- Windows 10 S versie 1903 en hoger, onderhouds Stuur Programma's
- Windows 10 S versie 1903 en hoger, upgrade & onderhouds Stuur Programma's
- Stuur Programma's voor Windows 10 versie 1803 en hoger
- Windows 10 versie 1803 en hoger upgrade & onderhouds Stuur Programma's
- Windows 10 versie 1809 en hoger, onderhouds Stuur Programma's
- Windows 10 versie 1809 en hoger, upgrade & onderhouds Stuur Programma's
- Windows 10 versie 1903 en hoger, onderhouds Stuur Programma's
- Windows 10 versie 1903 en hoger, upgrade & onderhouds Stuur Programma's

> [!NOTE]
> De meeste Surface-Stuur Programma's behoren tot meerdere Windows 10-product groepen. Het is niet mogelijk om alle producten die hier worden vermeld, te selecteren. Om het aantal producten dat uw Update catalogus vult te beperken, raden we u aan om alleen de producten te selecteren die uw omgeving vereist voor synchronisatie.

## <a name="surface-models"></a><a name="bkmk_models"></a>Surface-modellen

De volgende tabel bevat de Surface modellen en versies van Windows 10 waarop Configuration Manager Stuur Programma's kunt installeren. Updates voor Surface drivers zijn niet beschikbaar in Configuration Manager dezelfde dag dat ze worden gepubliceerd in de Microsoft Update catalogus. Configuration Manager behoudt een eigen lijst met de Stuur Programma's die worden geïmporteerd. Deze lijst wordt regel matig gepubliceerd en bevat de Stuur Programma's die zijn gepubliceerd op of voor een bepaalde datum. Apparaten met Windows 10 S-producten moeten worden genoteerd.

**Surface-Stuur Programma's die zijn gepubliceerd op of vóór 9 juni 2020 zijn beschikbaar in Configuration Manager**. 


|Surface model|Windows 10 1709| Windows 10 1803|Windows 10 1809|Windows 10 1903|Windows 10 1909|
|----|----|----|----|----|----|
|Surface Pro 3|Ja| Ja| Ja |Ja|Ja|
|Surface Pro 4|Ja| Ja| Ja |Ja|Ja|
|Surface Pro 6|N.v.t.| Ja| Ja |Ja|Ja|
|Surface Pro 7|N.v.t.| N.v.t.| N.v.t. |Ja|Ja|
|Surface Pro X|N.v.t.| N.v.t.| N.v.t. |Ja|Ja|
|Surface Book|Ja| Ja| Ja |Ja|Ja|
|Oppervlakte rapport 2|Ja| Ja| Ja |Ja|Ja|
|Surface Book 3|N.v.t.| N.v.t.| N.v.t. |N.v.t.|Ja|
|Surface-laptop|Ja, met het product ' Windows 10 S versie 1709 en latere onderhouds Stuur Programma's ' geselecteerd| Ja, met het product ' Windows 10 S versie 1803 en latere onderhouds Stuur Programma's ' geselecteerd|Ja, met het product Windows 10 S versie 1809 en hoger upgrade & onderhouds Stuur Programma's ' geselecteerd|Ja, met het product Windows 10 S versie 1903 en hoger upgrade & onderhouds Stuur Programma's ' geselecteerd|Ja, met het product Windows 10 S versie 1903 en hoger upgrade & onderhouds Stuur Programma's ' geselecteerd|
|Surface-laptop 2|Ja| Ja |Ja|Ja|Ja|
|Surface-laptop 3|N.v.t.| N.v.t.|N.v.t.|Ja |Ja|
|Oppervlakte bezoek|N.v.t.| Ja, met het product ' Windows 10 S versie 1803 en latere onderhouds Stuur Programma's ' geselecteerd|Ja, met het product Windows 10 S versie 1809 en hoger upgrade & onderhouds Stuur Programma's ' geselecteerd|Ja, met het product Windows 10 S versie 1903 en hoger upgrade & onderhouds Stuur Programma's ' geselecteerd|Ja, met het product Windows 10 S versie 1903 en hoger upgrade & onderhouds Stuur Programma's ' geselecteerd|
|Oppervlakte Go 2|N.v.t.| Ja| Ja |Ja|Ja, met het product Windows 10 S versie 1903 en hoger upgrade & onderhouds Stuur Programma's ' geselecteerd|
|Surface Studio|Ja| Ja| Ja |Ja|Ja|
|Surface Studio 2|N.v.t.| Ja| Ja |Ja|Ja|

## <a name="verify-the-configuration"></a>De configuratie controleren

Als u wilt controleren of het software-update punt correct is geconfigureerd, gebruikt u **bestand Wsyncmgr. log** en **WCM. log**.

1. Open bestand Wsyncmgr. log en controleer op de volgende logboek vermelding:

    ```text
    Surface Drivers can be supported in this hierarchy since all software update points are on Windows Server 2016, WCM SCF property Sync Catalog Drivers is set. 
    …
    Sync Catalog Drivers SCF value is set to : 1
    ```

1. Als een van de volgende vermeldingen zijn geregistreerd in **bestand Wsyncmgr. log**, controleert u of u de optie **micro soft Surface drivers en firmware-updates toevoegen** hebt geselecteerd in de eigenschappen van uw software-update punt:
   - `Sync Surface Drivers option is not set`
   - `Sync Catalog Drivers SCF value is set to : 0`

1. Open **WCM. log** en zoek naar items die vergelijkbaar zijn met de volgende vermeldingen:
   ```text
   <Categories>
   <Category Id="Product:05eebf61-148b-43cf-80da-1c99ab0b8699"><![CDATA[Windows 10 and later drivers]]></Category>
   <Category Id="Product:06da2f0c-7937-4e28-b46c-a37317eade73"><![CDATA[Windows 10 Creators Update and Later Upgrade & Servicing Drivers]]></Category>
   <Category Id="Product:c1006636-eab4-4b0b-b1b0-d50282c0377e"><![CDATA[Windows 10 S and Later Servicing Drivers]]></Category>
   … …
   </Categories>
   ```

   Dit item is een XML-element met een lijst met elke product groep en classificatie die momenteel is gesynchroniseerd door de server van uw software-update punt. Als u de producten die u hebt geselecteerd, niet kunt vinden, controleert u of de producten voor het software-update punt zijn opgeslagen.
1. U kunt ook wachten tot de volgende synchronisatie is voltooid. Controleer vervolgens of het Surface-stuur programma en de firmware-updates worden weer gegeven in software-updates in de Configuration Manager-console. De-console kan bijvoorbeeld de volgende informatie weer geven: ![ gesynchroniseerde Surface-Stuur Programma's in Configuration Manager-console](media/synchronized-surface-drivers.png)

## <a name="frequently-asked-questions-faq"></a>Veelgestelde vragen

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>Nadat ik de stappen in dit artikel heb gevolgd, worden de Surface-Stuur Programma's nog steeds niet gesynchroniseerd. Hoe komt dat?

Als u synchroniseert vanaf een upstream-Windows Server Update Services (WSUS) in plaats van Microsoft Update, moet u ervoor zorgen dat de upstream-WSUS-server is geconfigureerd voor ondersteuning en synchronisatie van updates voor Surface-Stuur Programma's. Alle downstream-servers zijn beperkt tot updates die aanwezig zijn in de upstream-WSUS-Server database.

### <a name="after-i-follow-the-steps-in-this-article-some-surface-drivers-are-synchronized-but-not-the-expected-drivers-why"></a>Nadat ik de stappen in dit artikel heb gevolgd, worden sommige Surface-Stuur Programma's gesynchroniseerd, maar niet de verwachte Stuur Programma's. Hoe komt dat?

De verwerkings tijd voor het testen van Stuur Programma's en het bevestigen ervan voor implementatie via WSUS en Configuration Manager varieert. Daarom is het oppervlak stuur programma-updates niet per se op dezelfde dag beschikbaar voor zowel de hand matige installatie als de implementatie van Configuration Manager-console.

Daarnaast zijn er meer dan 68.000 updates die zijn geclassificeerd als stuur Programma's in WSUS. Micro soft filtert de synchronisatie van Stuur Programma's op basis van een acceptatie lijst om te voor komen dat niet-Opper vlakken worden gesynchroniseerd met Configuration Manager. Surface-Stuur Programma's moeten extra tests door lopen voordat ze aan deze lijst kunnen worden toegevoegd. Nadat de nieuwe acceptatie lijst is gepubliceerd en opgenomen in Configuration Manager, worden de nieuwe Stuur Programma's toegevoegd aan de-console na de volgende synchronisatie.

### <a name="is-the-driver-allow-list-published-is-it-downloadable"></a>Is de lijst met toegestane Stuur Programma's gepubliceerd? Is het downloadbaar?

De acceptatie lijst van het Surface-stuur programma wordt niet online gepubliceerd. Deze lijst wordt via de update-en onderhouds kanalen aan Configuration Manager geleverd. Als uw Configuration Manager omgeving online is en u nieuwe updates kunt detecteren, ontvangt u automatisch updates in de lijst.

Als uw Configuration Manager omgeving offline is, wordt een nieuwe acceptatie lijst geïmporteerd telkens wanneer u de onderhouds updates naar Configuration Manager importeert. U moet ook een nieuwe WSUS-catalogus met de Stuur Programma's importeren voordat de updates worden weer gegeven in de Configuration Manager-console. Omdat een zelfstandige WSUS-omgeving meer Stuur Programma's bevat dan een Configuration Manager software-update punt, wordt u aangeraden een Configuration Manager omgeving te maken die online mogelijkheden heeft en die u configureert voor het synchroniseren van Surface-Stuur Programma's. Dit biedt een kleinere WSUS-export die lijkt op de offline omgeving.

Een andere oplossing is het gebruik van [alternatieve methoden](#bkmk_alt) voor het implementeren van Surface-Stuur Programma's en firmware-updates.

### <a name="i-require-the-latest-firmware-update-and-i-cant-wait-for-it-to-be-approved-for-import-into-configuration-manager-can-i-manually-import-the-driver-into-wsus"></a>Ik heb de meest recente firmware-update nodig en ik kan niet wachten tot deze is goedgekeurd voor importeren in Configuration Manager. Kan ik het stuur programma hand matig in WSUS importeren? 

Nee. Zelfs als de update in WSUS wordt geïmporteerd, wordt de update niet geïmporteerd in de Configuration Manager-console voor implementatie als deze niet in de acceptatie lijst staat.

Een andere oplossing is het gebruik van [alternatieve methoden](#bkmk_alt) voor het implementeren van Surface-Stuur Programma's en firmware-updates.

### <a name="can-i-manually-add-a-driver-to-the-allow-list"></a>Kan ik een stuur programma hand matig toevoegen aan de acceptatie lijst? 

Nee. De lijst wordt opgeslagen in de Configuration Manager-Data Base. Eventuele wijzigingen in de lijst worden overschreven de volgende keer dat het CAB-bestand wordt verwerkt.


### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a><a name="bkmk_alt"></a>Welke alternatieve methoden moet ik gebruiken voor het implementeren van Surface-Stuur Programma's en firmware-updates?

Zie [Surface-Stuur Programma's en firmware-updates beheren](https://docs.microsoft.com/surface/manage-surface-pro-3-firmware-updates)voor meer informatie over het implementeren van Surface-Stuur Programma's en firmware-updates via alternatieve kanalen.

Als u het MSI-of exe-bestand wilt downloaden en vervolgens wilt implementeren via traditionele software-implementatie kanalen, raadpleegt u [Surface firmware bijgewerkt met Configuration Manager](https://blogs.technet.microsoft.com/thejoncallahan/2016/06/20/keeping-surface-firmware-updated-with-configuration-manager/).

## <a name="next-steps"></a>Volgende stappen

Raadpleeg de volgende artikelen voor meer informatie over Surface-Stuur Programma's:

- [Overwegingen voor Opper vlak en System Center Configuration Manager](https://docs.microsoft.com/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager)
- [Geschiedenis van Surface update](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [Down load de nieuwste firmware en stuur Programma's voor Surface-apparaten](https://docs.microsoft.com/surface/deploy-the-latest-firmware-and-drivers-for-surface-devices)

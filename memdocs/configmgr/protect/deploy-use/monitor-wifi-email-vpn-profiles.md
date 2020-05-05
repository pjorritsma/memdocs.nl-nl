---
title: E-mail, Wi-Fi-en VPN-profielen bewaken
titleSuffix: Configuration Manager
description: Meer informatie over het bewaken van de compatibiliteits status van e-mail-, Wi-Fi-en VPN-profielen in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 59e372641c303e77f0d88e655bb917660c9e677c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724494"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Bewaak E-mail, Wi-Fi-en VPN-profielen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u Configuration Manager e-mail-, Wi-Fi-of VPN-profielen hebt geïmplementeerd voor gebruikers in uw hiërarchie, kunt u de volgende procedures gebruiken om de nalevings status van het profiel te controleren:  

-   [Nalevingsresultaten weergeven in de Configuration Manager-console](#BKMK_console)  

-   [De nalevingsresultaten weergeven met behulp van rapporten](#BKMK_Reports)  

##  <a name="how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a>Nalevings resultaten weer geven in de Configuration Manager-console  
 Gebruik deze procedure om details te bekijken over de naleving van geïmplementeerde profielen in de Configuration Manager-console.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Nalevingsresultaten weergeven in de Configuration Manager-console  

1.  Klik in de Configuration Manager-console op **bewaking**.  

2.  Klik in de werkruimte **Bewaking** op **Implementaties**.  

3.  Selecteer in de lijst **implementaties** de profiel implementatie waarvoor u de compatibiliteits informatie wilt bekijken.  

4.  U kunt samenvattings informatie over de compatibiliteit van de profiel implementatie bekijken op de hoofd pagina. Als u meer gedetailleerde informatie wilt weer geven, selecteert u de profiel implementatie en klikt u vervolgens op het tabblad **Start** in de groep **implementatie** op **status weer geven** om de pagina **Implementatie status** te openen.  

     De pagina **Implementatiestatus** bevat de volgende tabbladen:  

    -   **Compatibel:** Geeft de compatibiliteit weer van het profiel dat is gebaseerd op het aantal beïnvloede activa. U kunt dubbelklikken op een regel om een tijdelijk knooppunt te creëren onder het knooppunt **Gebruikers** in de werkruimte **Activa en naleving** , die alle gebruikers bevat die compatibel met dit profiel zijn. In het deel venster **activum gegevens** worden de gebruikers weer gegeven die compatibel zijn met het profiel. Dubbelklik op een gebruiker in de lijst om extra informatie weer te geven.  

        > [!IMPORTANT]  
        >  Een profiel wordt niet geëvalueerd als het niet van toepassing is op een client apparaat. deze wordt echter als compatibel geretourneerd.  

    -   **Fout:** Geeft een lijst weer van alle fouten voor de geselecteerde profiel implementatie die is gebaseerd op het aantal beïnvloede activa. U kunt dubbelklikken op een regel om een tijdelijk knooppunt te creëren onder het knooppunt **Gebruikers** in de werkruimte **Activa en naleving** , die alle gebruikers bevat die fouten genereerden met dit profiel. Wanneer u een gebruiker selecteert, geeft het deelvenster **Activumgegevens** de gebruikers weer die met het geselecteerde probleem te maken krijgen. Dubbelklik op een gebruiker in de lijst om extra informatie weer te geven over het probleem.  

    -   **Niet-compatibel:** Geeft een lijst weer van alle niet-compatibele regels binnen het profiel dat is gebaseerd op het aantal beïnvloede activa. U kunt dubbelklikken op een regel om een tijdelijk knooppunt te creëren onder het knooppunt **Gebruikers** in de werkruimte **Activa en naleving** , die alle gebruikers bevat die niet conform dit profiel zijn. Wanneer u een gebruiker selecteert, geeft het deelvenster **Activumgegevens** de gebruikers weer die met het geselecteerde probleem te maken krijgen. Dubbelklik op een gebruiker in de lijst om verdere informatie weer te geven over het probleem.  

    -   **Onbekend:** Geeft een lijst weer van alle gebruikers die geen naleving hebben gerapporteerd voor de geselecteerde profiel implementatie samen met de huidige client status van de apparaten.  

5.  Op de pagina **Implementatie status** kunt u gedetailleerde informatie bekijken over de naleving van het geïmplementeerde profiel. Een tijdelijk knooppunt wordt gemaakt onder het knooppunt **Implementaties** waarmee u deze informatie snel kunt terugvinden.  

##  <a name="how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a>Nalevings resultaten weer geven met behulp van rapporten  
 Nalevings instellingen, waaronder profielen in Configuration Manager, bevatten ook een aantal ingebouwde rapporten waarmee u informatie over profielen kunt bewaken. Deze rapporten hebben de rapportcategorie van **Compatibiliteit en instellingen beheren**.  

> [!IMPORTANT]  
>  U moet een jokerteken (%) gebruiken wanneer u de parameters **Apparaatfilter** en **Gebruikerfilter** gebruikt in de rapporten van instellingen voor naleving.  

 Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over het configureren van rapportage in Configuration Manager.  

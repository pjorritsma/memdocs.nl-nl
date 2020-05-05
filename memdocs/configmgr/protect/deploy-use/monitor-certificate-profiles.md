---
title: Certificaatprofielen controleren
titleSuffix: Configuration Manager
description: Meer informatie over het controleren van de nalevings status van Configuration Manager-certificaat profielen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1f43e113aa91f75c09bd264e8b3bc2704220a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722296"
---
# <a name="how-to-monitor-certificate-profiles-in-configuration-manager"></a>Certificaat profielen bewaken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Nalevings resultaten weer geven in de Configuration Manager-console  

Voor het controleren van de compatibiliteit van het SCEP-certificaat gebruikt u de-console niet, maar gebruikt u in plaats daarvan [rapporten](#view-compliance-results-by-using-reports). 

1. Kies in de Configuration Manager-console **bewakings**>  **implementaties**.  

2. Selecteer de implementatie van het certificaat profiel.  

3. Bekijk de informatie over de naleving van het certificaat op de hoofd pagina. Voor meer informatie, selecteert u het certificaat profiel en vervolgens klikt u op het tabblad **Start** in de groep **implementatie** op **status weer geven** om de pagina **Implementatie status** te openen.  

    De pagina **Implementatiestatus** bevat de volgende tabbladen:  

   -   **Compatibel**: Hier wordt de compatibiliteit van het certificaatprofiel weergegeven op basis van het aantal activa dat is beïnvloed. U kunt op een regel dubbelklikken om een tijdelijk knooppunt te maken onder het knooppunt **Gebruikers** in de werkruimte **Activa en naleving** . Dit knooppunt bevat alle gebruikers die compatibel zijn met het certificaatprofiel. In het deelvenster **Activumgegevens** worden ook de gebruikers weergegeven die compatibel zijn met dit profiel. Dubbel klik op een gebruiker in de lijst voor meer informatie.  

       > [!IMPORTANT]  
       >  Een certificaatprofiel wordt niet geëvalueerd als het niet van toepassing is op een clientapparaat. Het wordt in dat geval echter wel geretourneerd als compatibel.  

   -   **Fout**: Hier wordt een lijst met alle fouten voor de geselecteerde certificaatprofielimplementatie weergegeven op basis van het aantal activa dat is beïnvloed. U kunt dubbelklikken op een regel om een tijdelijk knooppunt te maken onder het knooppunt **Gebruikers** van de werkruimte **Activa en naleving** . Dit knooppunt bevat alle gebruikers waarvoor fouten zijn gegenereerd met dit profiel. Wanneer u een gebruiker selecteert, geeft het deelvenster **Activumgegevens** de gebruikers weer die met het geselecteerde probleem te maken krijgen. Dubbel klik op een gebruiker in de lijst die u wilt weer geven voor meer informatie.  

   -   **Niet-compatibel**: Hier wordt een lijst met alle niet-compatibele regels binnen het certificaatprofiel weergegeven op basis van het aantal activa dat is beïnvloed. U kunt dubbelklikken op een regel om een tijdelijk knooppunt te maken onder het knooppunt **Gebruikers** van de werkruimte **Activa en naleving** . Dit knooppunt bevat alle gebruikers die niet compatibel zijn met dit profiel. Wanneer u een gebruiker selecteert, geeft het deelvenster **Activumgegevens** de gebruikers weer die met het geselecteerde probleem te maken krijgen. Dubbelklik op een gebruiker in de lijst om verdere informatie weer te geven over het probleem.  

   -   **Onbekend**: Hier wordt een lijst weergegeven met alle gebruikers waarvoor naast de huidige clientstatus van de apparaten geen compatibiliteitsstatus is gerapporteerd voor de geselecteerde certificaatprofielimplementatie.  

4. Bekijk op de pagina **Implementatie status** gedetailleerde informatie over de naleving van het geïmplementeerde certificaat profiel. Een tijdelijk knooppunt wordt gemaakt onder het knooppunt **Implementaties** waarmee u deze informatie snel kunt terugvinden.  

    De status van inschrijving van het certificaat wordt weergegeven als een numerieke waarde. Gebruik de volgende tabel om te begrijpen wat elke waarde betekent:  


   | Status van inschrijving |                                                                                                                   Beschrijving                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         De inschrijving is voltooid en het certificaat is uitgegeven.                                                                                          |
   |    0x00000002     |                                                                    De aanvraag is verzonden en de inschrijving is in behandeling of de aanvraag is buiten band uitgegeven.                                                                    |
   |    0x00000004     |                                                                                                          Inschrijving moet worden uitgesteld.                                                                                                           |
   |    0x00000010     |                                                                                                               Er is een fout opgetreden.                                                                                                                |
   |    0x00000020     |                                                                                                        De status van de inschrijving is onbekend.                                                                                                        |
   |    0x00000040     | De statusgegevens zijn overgeslagen. Dit kan gebeuren als een Hyper link<https://msdn.microsoft.com/windows/ms721572>"" \l "_security_certification_authority_gly" certificerings instantie niet geldig is of niet is geselecteerd voor bewaking. |
   |    0x00000100     |                                                                                                           Inschrijving is geweigerd.                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>Nalevings resultaten weer geven met behulp van rapporten

Instellingen voor naleving in Configuration Manager omvatten ingebouwde rapporten die u kunt gebruiken om gegevens over certificaat profielen te bewaken. Deze rapporten hebben de rapportcategorie van **Compatibiliteit en instellingen beheren**.  

> [!IMPORTANT]  
>  U moet een jokerteken (%) gebruiken wanneer u de parameters **Apparaatfilter** en **Gebruikersfilter** gebruikt in de rapporten voor compatibiliteitsinstellingen.  

Voor het controleren van de compatibiliteit van het SCEP-certificaat gebruikt u deze certificaat rapporten in het rapport knooppunt **toegang tot bedrijfs bronnen**:  

-   Geschiedenis van certificaatuitgifte  
-   Lijst met activa met certificaten die de vervaldatum bijna hebben bereikt  
-   Lijst met activa per certificaatuitgiftestatus  



 Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over het configureren van rapportage in Configuration Manager.  

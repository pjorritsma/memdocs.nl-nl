---
title: Aan de slag met instellingen voor naleving
titleSuffix: Configuration Manager
description: Meer informatie over kern concepten en hoe de instellingen voor naleving werken
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d5e042980a1fa6fb8a92abcff6d3938874cf6b38
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694590"
---
# <a name="get-started-with-compliance-settings-in-configuration-manager"></a>Aan de slag met instellingen voor naleving in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u Configuration Manager instellingen voor naleving maakt, moet u eerst leren over kern concepten en begrijpen hoe ze werken.  



## <a name="how-compliance-settings-work"></a>Hoe instellingen voor naleving werken  
Met instellingen voor naleving kunt u de configuratie en naleving van clients in uw organisatie beheren.  

Configuratie-items kunnen worden onderverdeeld in twee hoofdcategorieën:  

- **Instellingen voor apparaten die worden beheerd met de Configuration Manager client** -meestal apparaten waarop u Configuration Manager-client software hebt geïnstalleerd om het apparaat te kunnen beheren.  

- **Instellingen voor apparaten die worden beheerd zonder de Configuration Manager clients** , meestal apparaten die worden beheerd met Microsoft intune, of met Configuration Manager on-premises Apparaatbeheer.  



## <a name="what-devices-are-supported"></a>Welke apparaten worden ondersteund?  

| Apparaattype | Meer informatie |  
|------------|----------------------|  
| Windows-Pc's (met de Configuration Manager-client) | Aangepaste configuratie-items maken om objecten zoals register sleutels, bestanden en Active Directory kenmerken te beoordelen.<br /><br /> Wanneer u het Windows 10-configuratie-item type gebruikt, selecteert u instellingen in een vooraf gedefinieerde lijst. |  
| Windows-Pc's (Inge schreven bij on-premises MDM) | Selecteer instellingen in een vooraf gedefinieerde lijst. |  
| Windows Phone-apparaten (Inge schreven bij on-premises MDM) | Selecteer instellingen in een vooraf gedefinieerde lijst. |  
| Mac-computers (met de Configuration Manager-client) | Aangepaste configuratie-items maken om objecten zoals macOS-voor keuren te beoordelen en resultaten die door een script worden geretourneerd. |  



## <a name="what-is-a-configuration-item"></a>Wat is een configuratie-item?  
Een configuratie-item is een container waarin specifieke informatie wordt opgeslagen. De informatie die u configureert, is afhankelijk van het type configuratie-item. Configuratie-items kunnen de volgende informatie bevatten:

- **Informatie over de detectie methode** is alleen voor Windows-configuratie-items die toepassings instellingen bevatten. Hiermee wordt gedetecteerd of een toepassing is geïnstalleerd. Deze detectie maakt gebruik van het Windows Installer-bestand voor de toepassing of met behulp van een aangepast script.  

- **Instellingen** vertegenwoordigen de zakelijke of technische voor waarden voor het beoordelen van de naleving op client apparaten. Configureer een nieuwe instelling of blader naar een bestaande instelling op een referentie computer.  

- Met **compliantie regels** geeft u de voor waarden op waarmee de compatibiliteit van een configuratie-item instelling wordt gedefinieerd. Voordat de client een instelling voor naleving evalueert, moet deze ten minste één compliantie regel hebben. Sommige instellingen herstellen waarden die niet compliant zijn. Nieuwe regels maken of naar een bestaande instelling in een configuratie-item bladeren en de regels daarin selecteren.  

- **Ondersteunde platforms** zijn de platformen die u definieert waarop de client de naleving van de configuratie-items evalueert. Als u een configuratie-item implementeert op een apparaat dat zich niet in de lijst met ondersteunde platforms bevindt, wordt de naleving niet geëvalueerd.  



## <a name="what-is-a-configuration-baseline"></a>Wat is een configuratiebasislijn?  
Definieer een configuratie basislijn die de configuratie-items bevat die moeten worden geëvalueerd. Neem ook de instellingen en regels op die het vereiste compatibiliteits niveau beschrijven. Importeer deze configuratie gegevens uit Configuration Manager-configuratie pakketten. Micro soft en andere leveranciers definiëren deze configuratie pakketten. Of nieuwe configuratie-items en configuratie basislijnen maken.  

Nadat u een configuratie basislijn hebt gedefinieerd, implementeert u deze voor gebruikers-en apparaat-verzamelingen. De client evalueert vervolgens de basislijn instellingen voor naleving van een schema. U kunt meer dan één configuratie basislijn implementeren op apparaten. Deze granulatie biedt meer controle over de naleving. 

Clientapparaten evalueren hun compatibiliteit aan de hand van elke geïmplementeerde configuratiebasislijn en rapporteren de resultaten rechtstreeks naar de site met behulp van statusberichten. Als een apparaat momenteel niet wordt losgekoppeld van het netwerk, maar de configuratie basislijn heeft gedownload, wordt nog steeds de naleving van de configuratie-items geëvalueerd. Hiermee wordt de compatibiliteits informatie verzonden wanneer deze opnieuw verbinding maakt.  

### <a name="monitoring-configuration-baselines"></a>Configuratie basislijnen bewaken
- Controleer de resultaten van de nalevings evaluatie in de Configuration Manager-console, in de werk ruimte **bewaking** , in het knoop punt **implementaties** . Bijvoorbeeld:
  - Veelvoorkomende oorzaken van niet-naleving
  - Fouten
  - Het aantal betrokken gebruikers en apparaten
- Voer de rapporten voor nalevings instellingen uit met aanvullende informatie. Bijvoorbeeld:
  - Welke apparaten voldoen aan het beleid of niet voldoen aan het beleid
  - Welk element van de configuratie basislijn zorgt ervoor dat een computer niet compatibel is
- Bekijk de resultaten van de nalevings evaluatie van Windows-computers waarop de Configuration Manager-client wordt uitgevoerd. Open het configuratie scherm van **Configuration Manager** en schakel over naar het tabblad **configuraties** .  



## <a name="user-data-and-profiles-configuration-items"></a>Configuratie-items voor gebruikersgegevens en -profielen  
Configuratie-items voor gebruikers gegevens en-profielen bevatten instellingen waarmee wordt bepaald hoe gebruikers op computers met Windows 8 en hoger beheren:  
- Mapomleiding
- Offline bestanden
- Zwervende profielen  

Implementeer deze configuratie-items voor gebruikers verzamelingen. Controleer hun naleving vanuit het knoop punt **controle** van de Configuration Manager-console. In tegens telling tot andere configuratie-items, voegt u deze niet toe aan configuratie basislijnen voordat u ze implementeert. Implementeer deze rechtstreeks door te klikken op **implementeren** in het lint.  

Zie configuratie-items voor [gebruikers gegevens en-profielen maken](../deploy-use/create-user-data-and-profiles-configuration-items.md)voor meer informatie.  



## <a name="remote-connection-profiles"></a>Profielen voor externe verbindingen  
Externe verbindings profielen bieden een set hulpprogram ma's en bronnen die u helpen bij het maken, implementeren en bewaken van instellingen voor externe verbindingen. Door deze instellingen te implementeren op apparaten, minimaliseert u de moeite die eind gebruikers nodig hebben om hun computers te verbinden met het bedrijfs netwerk.  

Zie [profielen voor externe verbinding maken](../deploy-use/create-remote-connection-profiles.md)voor meer informatie.  



## <a name="windows-edition-upgrade"></a>Een upgrade uitvoeren voor uw Windows-editie
Met het beleid voor editie-upgrades worden apparaten waarop bepaalde versies van Windows 10 worden uitgevoerd, automatisch bijgewerkt naar een nieuwere versie. Dit beleid levert een nieuwe product code of licentie bestand dat het apparaat gebruikt om een upgrade uit te kunnen zetten.

Zie [Windows-apparaten upgraden met het beleid voor editie-upgrades](../deploy-use/upgrade-windows-version.md) voor meer informatie.

## <a name="microsoft-edge-legacy-browser-profiles"></a>Oudere browser profielen voor micro soft Edge
<!-- 1357310 -->
Voor klanten die de [micro soft Edge verouderde](/microsoft-edge/deploy/) webbrowser op Windows 10-clients gebruiken, maakt u een Configuration Manager nalevings beleid om de browser instellingen te configureren.

Zie voor meer informatie [micro soft Edge verouderde browser profielen](../deploy-use/browser-profiles.md).
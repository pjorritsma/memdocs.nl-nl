---
title: Implementatie naar productie
titleSuffix: Configuration Manager
description: Een hand leiding voor het implementeren van een desktop Analytics-productie groep.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c7a14da1505e89dfd61a3dc4f13385fbf5c21d41
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723654"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Implementatie in productie met Desktop Analytics

Nadat u hebt [geïmplementeerd op pilot](deploy-pilot.md) en de status van uw assets hebt gecontroleerd, kunt u de rest van uw productie omgeving bijwerken.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Er zijn drie belang rijke onderdelen voor het uitvoeren van de implementatie van updates voor productie-apparaten:

1. [Activa bekijken waarvoor een upgrade beslissing is vereist](#bkmk_review): als u wilt dat apparaten gereed zijn voor productie-implementatie, moeten de bijbehorende activa hun upgrade besluit instellen op **gereed** of **gereed, herstel bewerkingen vereist**.  

2. [Implementeren op apparaten die gereed zijn](#bkmk_deploy): gebruik Configuration Manager om apparaten bij te werken die gereed zijn. Desktop Analytics bevat de lijst met apparaten die gereed zijn voor productie-implementatie en rapporten voor het bewaken van het succes van de implementatie.  

3. [De status van bijgewerkte apparaten bewaken](#bkmk_monitor): als de update-implementatie vordert, controleert u de status van belang rijke assets. Als er iets aandacht vereist, kunt u problemen oplossen en deze problemen oplossen. Als u besluit dat de problemen niet kunnen worden opgelost, stopt u de implementatie met de betreffende apparaten door hun upgrade besluit in te stellen op **niet**.  

> [!NOTE]  
> Wanneer u zeker bent van het succes van de proef implementatie, start u de productie-implementatie op elk gewenst moment. Er is geen vereiste dat alle test apparaten eerst de status ' voltooid ' bereiken.  



## <a name="review-assets-that-need-an-upgrade-decision"></a><a name="bkmk_review"></a>Activa bekijken waarvoor een upgrade beslissing is vereist

Desktop Analytics helpt u bij het controleren van uw assets voor productie-implementaties. In de Azure Portal gaat u naar **implementatie plannen**, selecteert u een implementatie plan en selecteert u vervolgens **productie voorbereiden** in het linkermenu.

![Scherm opname van productie weergave voorbereiden in Desktop Analytics](media/prepare-production.png)

Bekijk de status van uw apps. Gebruik deze informatie om de upgrade beslissing voor elk van deze activa in te stellen.

Gebruik elk van de tabbladen om de status van de apps te controleren. In elke weer gave met tabbladen kunt u de resultaten filteren om apparaten weer te geven die op schema staan voor de upgrade, moet u uw aandacht best Eden aan de apparaten met gemengde resultaten en die apparaten met een onbepaalde status.

Selecteer **doel stellingen** voor een vergadering om de weer gave te filteren op activa die waarschijnlijk gereed zijn voor productie-implementatie op basis van de volgende criteria:

- Risico: een evaluatie vooraf van de upgrade van bekende Risico's voor het bijwerken van apparaten waarop deze asset is geïnstalleerd  

- Status: een evaluatie na de upgrade van apparaten in andere implementaties en of er problemen zijn opgetreden na de installatie van de update. Zie [de status van bijgewerkte apparaten bewaken](#bkmk_monitor)voor meer informatie over de status.  

Als u een activum voor een upgrade wilt goed keuren, selecteert u de naam in de lijst en selecteert u vervolgens een van de volgende opties in de lijst met **Update beslissingen** :

- Beoordeling wordt uitgevoerd
- Gereed
- Gereed (met herstel)
- Lukt
- Niet gecontroleerd

Als u deze waarde voor meerdere apps tegelijk wilt instellen, gebruikt u de eerste kolom om **dit item te selecteren**en kiest u **upgrade beslissing instellen**.

![Optie voor upgrade besluit op meerdere apps instellen](media/prep-prod-set-upgrade-decision.png)

Selecteer **geen gegevens** om activa weer te geven die niet kunnen worden geclassificeerd. Deze activa zijn over het algemeen niet voldoende dekking voor desktop Analytics om een analyse van het risico of de integriteits status uit te voeren. Als u de dekking wilt verbeteren, voegt u extra apparaten met deze assets toe aan de pilot of vraagt u een proef gebruiker om deze activa te proberen.

Er kunnen ook activa zijn met de status **vereist** of **gemengde resultaten** . Deze activa kunnen extra beoordeling vereisen voordat u een upgrade besluit kunt nemen.

Alle apps controleren. Zodra een bepaald apparaat een positieve upgrade besluit heeft voor alle assets, verandert de status van ' gereed voor productie '. Bekijk het huidige aantal op de hoofd pagina van het implementatie plan door de derde implementatie stap te selecteren, **implementeren**.


## <a name="deploy-to-devices-that-are-ready"></a><a name="bkmk_deploy"></a>Implementeren op apparaten die gereed zijn

Configuration Manager gebruikt de gegevens uit de Desktop Analytics om een verzameling voor de productie-implementatie te maken. Implementeer de taken reeks niet met een traditionele implementatie. Gebruik de volgende procedure om een met Desktop Analytics geïntegreerde implementatie te maken:

Als u het aanbevolen proces voor het [implementeren van pilot-apparaten](deploy-pilot.md#deploy-to-pilot-devices)hebt gevolgd, is de Configuration Manager gefaseerde implementatie klaar. Wanneer u assets markeert als *gereed*, worden deze apparaten door Desktop Analytics automatisch gesynchroniseerd met Configuration Manager. Deze apparaten worden vervolgens toegevoegd aan de productie verzameling. Wanneer de gefaseerde implementatie naar de tweede fase wordt verplaatst, ontvangen deze productie apparaten de upgrade-implementatie.

Als u de gefaseerde implementatie hebt geconfigureerd om **hand matig de implementatie van de tweede fase te starten**, moet u deze hand matig verplaatsen naar de volgende fase. Zie [gefaseerde implementaties beheren en bewaken](../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_move)voor meer informatie.

Als u een met Desktop Analytics geïntegreerde implementatie hebt gemaakt voor de test verzameling, moet u dit proces herhalen om te implementeren in de productie verzameling.


### <a name="address-deployment-alerts"></a>Waarschuwingen voor het implementeren van adressen

Net als bij de proef implementatie adviseert Desktop Analytics u problemen die uw aandacht nodig hebben tijdens de productie-implementatie. Ga in Desktop Analytics naar het implementatie plan en selecteer de **Implementatie status** in het linkermenu. In de implementatie status weergave worden apparaten vermeld in de volgende categorieën:  

- Niet gestart
- Wordt uitgevoerd
- Voltooid
- Aandacht vereist: apparaten (gesorteerd op apparaatnaam)
- Aandacht vereist: problemen (gesorteerd op probleem type)

![Scherm opname van de productie-implementatie status van de Desktop Analytics](media/prod-deployment-status.png)


## <a name="monitor-the-health-of-updated-devices"></a><a name="bkmk_monitor"></a>De status van bijgewerkte apparaten bewaken

De pagina **productie voorbereiden** is gericht op het helpen bij het maken van upgrade beslissingen voor uw activa. Op deze pagina worden standaard alleen de activa weer gegeven die nog niet in de status **gereed** zijn. Op de pagina **Monitor status** worden status problemen voor een wille keurig activum weer gegeven, zelfs de activa die als **gereed**zijn gemarkeerd. Als zich problemen voordoen, kunt u het probleem oplossen en oplossen, of de upgrade beslissing wijzigen in **niet**. Wanneer u de upgrade beslissing wijzigt, voor komt deze actie toekomstige upgrades op apparaten met die Asset.

Filter deze pagina op assets met de volgende statussen:

| Status filter | Beschrijving |
|----------------------|-------------|
| **Aandacht vereist** | (Standaard filter) Desktop Analytics detecteert een statistisch significante regressie voor bepaalde status waarden voor die Asset
| **Doel stellingen van vergadering** | Desktop Analytics detecteert geen regressie problemen |
| **Onvoldoende gegevens** | Desktop Analytics heeft niet genoeg gegevens over deze asset om aanbevelingen te doen |
| **Geen gegevens** | Er zijn nog geen gebruiks gegevens beschikbaar voor deze asset |

Als u een niet-gefilterde weer gave van alle assets wilt weer geven, selecteert u het huidige filter. Met deze actie wordt dat filter verwijderd.

> [!NOTE]  
> Voor het verminderen van het aantal assets met onvoldoende gegevens, bewaakt Desktop Analytics de assets op al uw apparaten die zijn bijgewerkt naar de Windows-doel versie die is opgegeven in uw implementatie plan. Dit zijn onder andere de apparaten die niet zijn opgenomen in het specifieke implementatie plan.  

De standaardsorteervolgorde is het aantal apparaten dat een incident met het betreffende activum heeft gehad, zodat u snel kunt zien welke problemen het meest voor komen. Wanneer u bijvoorbeeld **apps**bekijkt, worden deze gesorteerd op **apparaten met app die de laatste twee weken zijn vastgelopen**.

Als u de status van alle assets wilt bekijken, zelfs die assets met onvoldoende gegevens voor desktop Analytics om statistische interferenties te maken, gebruikt u het volgende proces:

1. Selecteer de vervolg keuzelijst op de **apparaten met incidenten in de afgelopen twee weken** kolom. Voeg een filter toe aan alleen die activa die incidenten hebben gehad op een minimum aantal apparaten dat interessant moet zijn. U kunt bijvoorbeeld items weer geven met waarden die **groter zijn dan** 100.  

2. Selecteer de vervolg keuzelijst in de kolom **% apparaten met incidenten in de afgelopen twee weken** en selecteer om te sorteren op **Aflopend**.  

    In de resulterende weer gave worden de assets met het hoogste incident met een minimum aantal incidenten weer gegeven.  

3. Selecteer een activum voor meer informatie of wijzig de beslissing over de upgrade.  

Zie controle van de [status](health-status-monitoring.md)voor meer informatie.

---
title: Toepassingen voor een apparaat installeren
titleSuffix: Configuration Manager
description: Gebruik Configuration Manager om onmiddellijk een toepassing te installeren op een apparaat zonder een verzameling.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a9f0c7d6eb7d8ccc42c5740bdb4b67926f676d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710221"
---
# <a name="install-applications-for-a-device"></a>Toepassingen voor een apparaat installeren

<!--4402180-->

Vanaf versie 1906 van de Configuration Manager-console kunt u in realtime toepassingen op een apparaat installeren. Met deze functie kunt u de nood zaak van afzonderlijke verzamelingen voor elke toepassing verminderen.

## <a name="prerequisites"></a>Vereisten

- De [optionele functie](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **voor het goed keuren van toepassings aanvragen voor gebruikers per apparaat**inschakelen.  

- [Implementeer de toepassing](deploy-applications.md) als *beschikbaar* voor een verzameling apparaten.  

    - Selecteer op de pagina **implementatie-instellingen** van de implementatie wizard de volgende optie: **een beheerder moet een aanvraag voor deze toepassing op het apparaat goed keuren**.  

        > [!Note]  
        > Met deze implementatie-instellingen wordt er geen beleid verzonden naar de client. De app wordt niet weer gegeven als beschikbaar in Software Center en een gebruiker kan de app niet installeren met deze implementatie. Nadat u deze actie hebt gebruikt om de app te installeren, kan de gebruiker deze uitvoeren en de installatie status bekijken in Software Center.

- Uw gebruikers account heeft de volgende machtigingen nodig:

    - **Toepassing**: lezen, goed keuren

    - **Verzameling**: lezen, resource lezen, resource wijzigen, verzameld bestand weer geven

    De ingebouwde rol van de **toepassings beheerder** heeft bijvoorbeeld deze machtigingen.

> [!TIP]
> Wacht op toepassings-en implementatie gegevens in een hiërarchie om te repliceren naar de primaire site waaraan de doel-client is toegewezen.<!-- SCCMDocs#2113 -->

## <a name="process"></a>Proces

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **apparaten** . Selecteer het doel apparaat en selecteer vervolgens de actie **toepassing installeren** in het lint.

1. Selecteer een of meer toepassingen in de lijst. In de lijst worden alleen toepassingen weer gegeven die u al hebt geïmplementeerd met de vereiste instellingen.

Met deze actie wordt de installatie van de geselecteerde vooraf geïmplementeerde toepassingen geactiveerd op het apparaat.

Als u de status van de goedkeurings aanvraag wilt bekijken, vouwt u in de werk ruimte **software bibliotheek** de optie **toepassings beheer**uit en selecteert u het knoop punt **toepassings aanvragen** .

Controleer de installatie van de app op dezelfde manier als gebruikelijk in het knoop punt **implementaties** van de werk ruimte **bewaking** .


## <a name="see-also"></a>Zie ook

[Toepassingen goedkeuren](app-approval.md)

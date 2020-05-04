---
title: Foutberichten
titleSuffix: Configuration Manager
description: Meer informatie over de fout berichten van package Conversion Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d4a2fa66dc1c4a8af3b3f7f16c67d58edebb5fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709885"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Technische documentatie voor fout berichten van package Conversion Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1357861-->

In dit artikel worden de fout berichten beschreven die worden weer gegeven in package Conversion Manager. Het bevat ook de mogelijke oorzaken van de fout en de methoden om de fout te corrigeren. Pakket conversie beheer registreert fout berichten in **PCMTrace. log**. Zie [logboek bestanden](troubleshoot-pcm.md#log-files)voor meer informatie, waaronder het beheren van het uitbreidings niveau.


#### <a name="application-creation-failed-with-the-following-exception"></a>Het maken van de toepassing is mislukt met de volgende uitzonde ring

De opgegeven uitzonde ring is opgetreden tijdens het indienen van het toepassings object bij de Configuration Manager-server.

Controleer uw machtigingen in Configuration Manager, Valideer uw verbinding en probeer het opnieuw. Als u het probleem niet kunt oplossen met deze acties, bekijkt u het bestand **PCMtrace. log** (uitgebreidheids niveau 4) en **SMSProv. log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Conversie fout: is van toepassing op een pakket transformatie STATUS

Er is een algemene uitzonde ring opgetreden tijdens de conversie van het pakket. Zoek in het bestand **PCMtrace. log** (uitgebreidheids niveau 4).

Controleer de gebruikers machtigingen voor de netwerk share (gegevens bron van het pakket), Valideer uw verbinding en probeer het opnieuw. Als u het probleem niet kunt oplossen met deze acties, bekijkt u het bestand **PCMtrace. log** (uitgebreidheids niveau 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>Er is geen omgezet pakket en de resulterende toepassing gevonden in de werk stroom uitvoer
De toepassing (geconverteerd pakket/programma) is verwijderd.

Wijzig het afhankelijke pakket/programma om ervoor te zorgen dat het afhankelijke pakket/programma bestaat.


#### <a name="objects-were-not-created-successfully"></a>De objecten zijn niet gemaakt
Er zijn verschillende mogelijke oorzaken.

Controleer uw machtigingen in Configuration Manager, Valideer uw verbinding en probeer het opnieuw. Als u het probleem niet kunt oplossen met deze acties, bekijkt u het bestand **PCMtrace. log** (uitgebreidheids niveau 4) en het bestand **SMSProv. log** .


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Sluit de wizard en los eventuele problemen met het geselecteerde pakket op. Zie PCMTrace. log voor meer informatie
Er zijn verschillende mogelijke oorzaken.

Controleer uw machtigingen in Configuration Manager, Valideer uw verbinding en probeer het opnieuw. Als u het probleem niet kunt oplossen met deze acties, bekijkt u het bestand **PCMtrace. log** (uitgebreidheids niveau 4) en het bestand **SMSProv. log** .


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>Voor sommige implementatie typen ontbreken detectie methoden. Alle implementatie typen moeten detectie methoden hebben
Er ontbreken detectie methoden in het programma.

Voeg een of meer detectie methoden toe tijdens het **herstel-en conversie** proces.


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Er is een fout opgetreden bij het voorbereiden van het pakket voor conversie
Er zijn verschillende mogelijke oorzaken.

Controleer uw machtigingen in Configuration Manager, Valideer uw verbinding en probeer het opnieuw. Als u het probleem niet kunt oplossen met deze acties, bekijkt u het bestand **PCMtrace. log** (uitgebreidheids niveau 4) en het bestand **SMSProv. log** .



---
title: Uw Android-apparaat lijkt versleuteld te zijn | Microsoft Docs
description: De versleutelingsstatus in de bedrijfsportal- en Microsoft Intune-app oplossen
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/14/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ba593c08-1a78-4013-8525-b45a948772ec
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a6984f4e6eafee1f81340f483dc557fdb6091ec9
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910754"
---
# <a name="device-encrypted-but-apps-say-otherwise"></a>Het apparaat is versleuteld, maar in apps wordt iets anders aangegeven

Als in de bedrijfsportal- of Microsoft Intune-app wordt aangeven dat uw apparaat niet is versleuteld, maar u zeker weet dat dit wel het geval is, volgt u de stappen in dit artikel.  

## <a name="add-a-startup-pin"></a>Een opstartpincode toevoegen

Voor bepaalde Android-apparaten moet u een opstartpincode instellen om ervoor te zorgen dat uw apparaat beveiligd is. De locatie van deze instelling is in de app **Instellingen** van uw apparaat. De naam en locatie van de instelling kunnen verschillen. Op de Samsung Galaxy-S7 wordt de instelling bijvoorbeeld aangeduid als **Veilig opstarten**. Als u dit wilt inschakelen en een wachtwoordcode wilt maken, gaat u naar **Instellingen** > **Vergrendelingsscherm en beveiliging** > **Veilig opstarten**.  

## <a name="encrypt-the-entire-device"></a>Het hele apparaat versleutelen

Deze sectie is alleen van toepassing op de Bedrijfsportal-app. Op sommige apparaten kunt u kiezen of u het hele apparaat of alleen de gebruikte ruimte wilt versleutelen. Kies de optie om het hele apparaat te versleutelen. Als u ervoor hebt gekozen om alleen de gebruikte ruimte te versleutelen:

1. [Verwijder dit apparaat uit de bedrijfsportal](unenroll-your-device-from-intune-android.md).
2. Ontsleutel de gebruikte ruimte.  
3. Versleutel het hele apparaat.  
4. Schrijf het apparaat opnieuw in.  

## <a name="downgrade-your-version-of-android"></a>Uw versie van Android downgraden

Deze sectie is alleen van toepassing op de Bedrijfsportal-app. Als uw apparaat u de optie biedt naar Android 6.0 en later te downgraden, kies daar dan voor. Er is een risico van gegevensverlies als u uw apparaat probeert te downgraden. Anders is het raadzaam dat u contact opneemt met het ondersteuningsteam van uw bedrijf om dit probleem op te lossen. Haal contactgegevens voor uw bedrijfsondersteuning op bij de [Bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).  

## <a name="specific-manufacturer-issues"></a>Fabrikant-specifieke problemen

Sommige Android-apparaten met versie 7.0 en later versleutelen gegevens op een manier die inconsistent is met bepaalde Android-platformstandaarden. Met deze versleutelingsmethoden lopen de apparaatgegevens risico. Als gevolg hiervan worden deze apparaten niet ondersteund.

Zie het artikel [Ondersteunde besturingssystemen en browsers in Intune](/intune/fundamentals/supported-devices-browsers#supported-samsung-knox-standard-devices) voor een niet-uitputtende lijst met ondersteunde Android-apparaten. Als uw apparaat niet wordt weergegeven, raadpleegt u de fabrikant van het apparaat of neemt u contact op met uw ondersteuningsmedewerker.

> [!Note]
> Microsoft werkt samen met fabrikanten aan het oplossen van problemen die worden gevonden tijdens het testen of die gebruikers rapporteren. Dit artikel wordt bijgewerkt wanneer nieuwe informatie beschikbaar is.

## <a name="update-devices"></a>Apparaten bijwerken

Als u uw apparaat niet hebt bijgewerkt naar de nieuwste Android-versie gaat u naar de app **Instellingen** van uw apparaat en selecteert u **Bijwerken**.  

## <a name="next-steps"></a>Volgende stappen

Nog hulp nodig? Neem contact op met het ondersteuningsteam van het bedrijf (zie de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980) voor contactgegevens) of stuur een e-mail naar het <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with enrolling my Android device&body=Describe the issue you're experiencing here.">Microsoft Android-team</a>.
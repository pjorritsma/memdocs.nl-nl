---
title: Android-apparaat versleutelen voor Intune | Microsoft Docs
description: Stappen voor het inschakelen van de versleuteling van Android-apparaten wanneer dit vereist is door Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/31/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 268e1ab9b76cc214b7e755763ada6a2bd09ed80e
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880577"
---
# <a name="encrypting-your-android-device"></a>Uw Android-apparaat versleutelen

Met apparaatversleuteling worden uw bestanden en mappen beschermd tegen onbevoegde toegang als uw apparaat is vermist of gestolen. Hiermee worden de gegevens op uw apparaat ontoegankelijk en onleesbaar voor personen zonder een wachtwoordcode. 

Voordat u toegang krijgt tot school- of werkresources, moet u van uw organisatie mogelijk het volgende doen:

* [Een apparaat versleutelen](#encrypt-device)
* [Beveiligd opstarten inschakelen](#enable-secure-startup)
* [Een wachtwoordcode, pincode of andere verificatiemethode voor opstarten instellen](#set-startup-passcode)  

> [!Note]
> Bepaalde Android-apparaten, zoals Huawei, Vivo en OPPO, kunnen niet worden versleuteld. Raadpleeg [Apparaat is versleuteld maar de app zegt iets anders](your-device-appears-encrypted-but-cp-says-otherwise-android.md) voor meer informatie.  

## <a name="encrypt-device"></a>Apparaat versleutelen

Volg deze stappen om uw apparaat te versleutelen. Het apparaat wordt mogelijk meerdere keren opnieuw opgestart. 

De naam en locatie van de versleutelingsoptie variëren, afhankelijk van de fabrikant van uw apparaat en de Android-versie. 

1. Open de app **Instellingen**.
2. Typ **beveiliging** of **versleutelen** in de zoekbalk van de app om gerelateerde instellingen te vinden.
3. Tik op de optie om het apparaat te versleutelen. Volg de instructies op het scherm.  
4. Stel een wachtwoord voor het vergrendelingsscherm, pincode of andere verificatiemethode in, wanneer u hierom wordt gevraagd (indien toegestaan in uw organisatie). 
5. Open de bedrijfsportal of Microsoft Intune-app om de instellingen opnieuw te controleren.
    * Bedrijfsportal-gebruikers: Selecteer uw apparaat en tik op **Apparaatinstellingen controleren**. 
    * Microsoft Intune-gebruikers: U moet wachten tot de pagina is bijgewerkt, maar als dat is gebeurd, is de versleutelingsstatus gewijzigd in conform. 

## <a name="enable-secure-startup"></a>Beveiligd opstarten inschakelen

In uw organisatie is mogelijk vereist dat u beveiligd opstarten inschakelt als onderdeel van het versleutelingsbeleid. Met deze functie wordt het apparaat nog extra beschermd, omdat er een wachtwoord of pincode moet worden ingevoerd voordat de telefoon kan worden opgestart. Mogelijk hebt u nog aanvullende verificatieopties. Dit varieert, afhankelijk van wat is toegestaan in uw organisatie. 

De naam en locatie van de optie voor beveiligd opstarten variëren, afhankelijk van de fabrikant van uw apparaat en de Android-versie. Op sommige apparaten heet deze instelling **Versterkte beveiliging**. 

1. Open de app **Instellingen**.
2. Typ **beveiligd opstarten** in de zoekbalk van de app.
3. Tik op **Beveiligd opstarten** > **Pincode vereisen wanneer het apparaat inschakelt**.
4. Voer de pincode van het apparaat in, wanneer u hierom wordt gevraagd.   
5. Open de bedrijfsportal of Microsoft Intune-app om de instellingen opnieuw te controleren.
    * Bedrijfsportal-gebruikers: Selecteer uw apparaat en tik op **Apparaatinstellingen controleren**. 
    * Microsoft Intune-gebruikers: U moet wachten tot de pagina is bijgewerkt, maar als dat is gebeurd, is de versleutelingsstatus gewijzigd in conform.  


## <a name="set-startup-passcode"></a>Wachtwoordcode voor opstarten instellen   
Bij het [versleutelen van uw apparaat](#encrypt-device) en het [inschakelen van beveiligd opstarten](#enable-secure-startup) wordt u gevraagd om een pincode, wachtwoord of andere verificatiemethode voor het apparaat in te stellen (indien toegestaan in uw organisatie). Er zijn geen verdere stappen vereist. 

Het type vergrendelingsscherm kiezen of wijzigen:

1. Open de app **Instellingen**.
2. Typ **schermvergrendeling** in de zoekbalk van de app.
3. Tik op **Type schermvergrendeling**.
4. Tik op het type schermvergrendeling dat u wilt gebruiken, en volg de instructies op het scherm om dit te bevestigen.  

## <a name="troubleshoot"></a>Problemen oplossen    
**Probleem**: De versleutelingsknop is uitgeschakeld.   

**Wat u kunt doen**: 
* Controleer of het apparaat volledig is opgeladen en is aangesloten. Versleuteling kan enige tijd duren en vereist een volledig opgeladen batterij.   

**Probleem**: Er wordt een bericht weergegeven dat u het apparaat nog moet versleutelen.  

**Wat u kunt doen**:
   *  [Stel een vergrendelingsscherm in](#set-startup-passcode) op het apparaat. 
   * [Schakel beveiligd opstarten in](#enable-secure-startup).

Nog hulp nodig? Neem contact op met het ondersteuningsteam van het bedrijf (zie de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980) voor contactgegevens) of stuur een e-mail naar het <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android-team</a>.  

---
title: Android-apparaat versleutelen voor Intune | Microsoft Docs
description: Stappen voor het inschakelen van de versleuteling van Android-apparaten wanneer dit vereist is door Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ee2d220e308b406251f049e1c17422f89ee36534
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348780"
---
# <a name="encrypting-your-android-device"></a>Uw Android-apparaat versleutelen

Met apparaatversleuteling worden uw bestanden en mappen beschermd tegen onbevoegde toegang als uw apparaat is vermist of gestolen. Nadat u apparaatversleuteling hebt ingeschakeld, kunnen alleen personen met het juiste wachtwoord of de juiste pincode zich aanmelden bij uw apparaat. 

Voordat u toegang krijgt tot school- of werkresources, moet u mogelijk uw Android-apparaat verplicht versleutelen van uw organisatie. Sommige nieuwere Android-apparaten worden standaard versleuteld.  

## <a name="turn-on-encryption"></a>Versleuteling inschakelen

Als bedrijfsportal of de Microsoft Intune app u vraagt om uw apparaat te versleutelen, voert u de volgende stappen uit. 

> [!Note]
> Bepaalde Android-apparaten, zoals Huawei, Vivo en OPPO, kunnen niet worden versleuteld. Zie [hier](your-device-appears-encrypted-but-cp-says-otherwise-android.md) voor meer informatie.  

1. Stel een schermvergrendeling voor het apparaat in.  
    a. Ga naar **Instelling** > **Vergrendelscherm en beveiliging** > **Type schermvergrendeling**.  
    b. Selecteer **Pincode**, **Wachtwoord** of **Patroon**.  
    c. Volg de instructies op het scherm voor het configureren van de beeldschermvergrendeling.  

2. Ga terug naar **Vergrendelingsscherm en beveiliging** en selecteer **Beveiligd opstarten**.
3. Kies **Pincode vereisen wanneer het apparaat inschakelt** > **OK**.
4. Voer uw pincode in om te bevestigen en versleutel uw apparaat.
5. Open de bedrijfsportal of Microsoft Intune-app.
    * Bedrijfsportal-gebruikers: Selecteer uw apparaat en tik op **Apparaatinstellingen controleren**. 
    * Microsoft Intune-gebruikers: U moet wachten tot de pagina is bijgewerkt, maar als dat is gebeurd, is de versleutelingsstatus gewijzigd in conform.  

Apparaten met Android 4.4 en eerder hebben mogelijk niet de optie **Beveiligd opstarten**. In dat geval voert u de volgende stappen uit om uw apparaat te versleutelen.

1. Ga naar **Instellingen** > **Beveiliging** > **Apparaat versleutelen**. Labels op het scherm zijn afhankelijk van Android-apparaten. Als u de optie **Apparaat versleutelen** niet ziet, kijkt u in:
    * **Opslag** > **Opslagversleuteling**
    * **Opslag** > **Vergrendelingsscherm en beveiliging** > **Overige beveiligingsinstellingen** 

2. Volg de instructies op het scherm. Tijdens het versleutelen wordt het apparaat mogelijk meerdere keren opnieuw opgestart.
3. Open de bedrijfsportal of Microsoft Intune-app.
    * Bedrijfsportal-gebruikers: Selecteer uw apparaat en tik op **Apparaatinstellingen controleren**.  
    * Microsoft Intune-gebruikers: U moet wachten tot de pagina is bijgewerkt, maar als dat is gebeurd, is de versleutelingsstatus gewijzigd in conform.

## <a name="troubleshoot"></a>Problemen oplossen  
**Probleem**: U hebt uw apparaat al versleuteld en

- De versleutelingsknop is uitgeschakeld.
- Er wordt een bericht weergegeven dat u nog moet versleutelen.
- Er treden fouten op bij het gebruik van de bedrijfsportal- of Microsoft Intune-app.

**Wat u kunt doen**

- Zorg dat het apparaat is geladen en aangesloten.  
- Zorg ervoor dat u een pincode of wachtwoord hebt ingesteld op het apparaat.  

Nog hulp nodig? Neem contact op met het ondersteuningsteam van het bedrijf (zie de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980) voor contactgegevens) of stuur een e-mail naar het <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android-team</a>.  

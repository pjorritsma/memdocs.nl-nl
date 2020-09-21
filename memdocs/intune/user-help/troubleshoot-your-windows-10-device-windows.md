---
title: Problemen met toegang tot school- of werkaccount via Windows 10-apparaten oplossen | Microsoft Intune
description: Los toegangs- of accountverbindingsproblemen op voor een ingeschreven Windows 10-apparaat.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/09/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 4ab630b6-47ff-443b-a2a5-be23388bcea7
searchScope:
- User help
ROBOTS: ''
ms.reviewer: amanh
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 7c96bef7c1be004714f0b06dd47c9c28850118da
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643423"
---
# <a name="troubleshoot-windows-10-device-access"></a>Problemen met Windows 10-apparaten oplossen
In dit artikel wordt beschreven hoe u toegangsproblemen voor een ingeschreven Windows 10-apparaat kunt oplossen. 

## <a name="check-wi-fi-connection"></a>Wi-Fi-verbinding controleren  

Er is een verbinding met Wi-Fi vereist voor toegang tot werk- of schoolresources. Controleer of u bent verbonden met Wi-Fi en probeer opnieuw toegang te krijgen tot de resources.  

## <a name="add-work-or-school-account-in-settings-app"></a>Werk- of schoolaccount toevoegen in app Instellingen  
Deze stappen zijn hetzelfde als bij het inschrijven van uw apparaat. Als uw account echter niet wordt weergegeven in de app **Instellingen**, moet u deze stappen misschien nog eens uitvoeren.  

1. Open de app **Instellingen**. 
2. Selecteer **Accounts**.
3. Deze volgende stap is afhankelijk van de versie van Windows 10 die u gebruikt. 
    * Versie 1607 en hoger: Selecteer **Toegang tot werk of school**.
    * Versie 1511 en lager: Selecteer **Toegang via werknetwerk**.  
4. Controleer of uw account wordt vermeld. Als het niet wordt vermeld, selecteert u de knop **Verbinding maken** met het plusteken om het toe te voegen. 
5. Meld u aan met de referenties van uw werk- of schoolaccount. 
6. Volg de prompts op het scherm om de verbinding tot stand te brengen.  
7. Wanneer u klaar bent, is het account toegevoegd als een verbinding. U hebt toegang tot alle resources die uw organisatie beschikbaar maakt.   

## <a name="contact-it-support-for-access-requirements"></a>Neem contact op met IT-ondersteuning voor toegangsvereisten  
Als uw werk- of schoolaccount wordt weergegeven in de app Instellingen, zijn uw apparaat en account al verbonden. Neem contact op met de IT-ondersteuningsmedewerker voor meer hulp bij toegangsproblemen. Ze kunnen te maken hebben met beperkingen of vereisten die verhinderen dat u toegang hebt tot bepaalde resources.  

## <a name="error-messages"></a>Foutberichten  

### <a name="we-couldnt-auto-discover-a-management-endpoint-matching-the-username-entered-please-check-your-username-and-try-again-if-you-know-the-url-to-your-management-endpoint-please-enter-it"></a>Er is geen beheereindpunt automatisch gedetecteerd dat overeenkomt met de ingevoerde gebruikersnaam. Controleer de gebruikersnaam en probeer het opnieuw. Als u de URL naar het beheereindpunt kent, voert u deze in.

**Oorzaak**: Uw account kan niet worden geverifieerd met de meegeleverde URL (ook wel het beheereindpunt genoemd).  

#### <a name="resolution"></a>Oplossing
1. Voer uw gebruikersnaam en wachtwoord nogmaals in. 
2. Als u nog steeds geen verbinding kunt maken, neem dan contact op met uw IT-ondersteuningsmedewerker om de juiste URL te verkrijgen (bijvoorbeeld: www.yourcompany.onmicrosoft.com). 
3. Wanneer u hierom wordt gevraagd, voert u de opgegeven URL in. 

### <a name="it-looks-like-youre-not-connected-make-sure-youre-connected-to-the-network"></a>Het lijkt erop dat u niet bent verbonden. Controleer of u bent verbonden met het netwerk.

**Oorzaak**: Het apparaat is niet verbonden met Wi-Fi en er is een verbinding vereist om een werk- of schoolaccount toe te voegen.     

#### <a name="resolution"></a>Oplossing
1. Selecteer op de werkbalk of in de instellingen van het apparaat het wereldbolpictogram **Netwerkstatus**.
2. Selecteer een Wi-Fi-netwerk > **Verbinding maken**.  
3. Probeer opnieuw verbinding te maken met uw account.  


## <a name="next-steps"></a>Volgende stappen  

Nog hulp nodig? Neem contact op met IT-ondersteuning. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).

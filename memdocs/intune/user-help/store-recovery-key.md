---
title: Een herstelsleutel opslaan in Intune via de bedrijfsportalwebsite
description: Upload en bewaar de herstelsleutel voor uw apparaat via de bedrijfsportalwebsite.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: annochiva
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: f0a674753ff23fca509bd21e6b52101104a6803f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910788"
---
# <a name="store-your-personal-filevault-key"></a>Uw persoonlijke FileVault-sleutel opslaan 

Bewaar een FileVault-sleutel voor uw persoonlijke versleutelde macOS-apparaat. Door uw sleutel in Intune op te slaan, voldoet u niet alleen aan versleutelingsvereisten, maar kunt u ook: 

* Eenvoudig en snel de sleutel ophalen of draaien op een willekeurig apparaat. 
* Uw ondersteuningsmedewerker om hulp vragen als u de sleutel moet ophalen of draaien en geen toegang hebt tot de apps of website om dit zelf te doen.


## <a name="retrieve-or-rotate-the-key"></a>De sleutel ophalen of draaien

Als u van uw apparaat wordt uitgesloten, kunt u de sleutel op de volgende locaties ophalen:
   
- Bedrijfsportalwebsite
- Bedrijfsportal-app voor iOS/iPadOS 
- Bedrijfsportal-app voor Android
- Intune-app
 
 IT-ondersteuningsmedewerkers met beheerderstoegang tot Intune kunnen uw persoonlijke herstelsleutel voor u draaien als uw apparaat is vergrendeld. Ze kunnen ook sleutels weergeven, maar alleen als die behoren tot apparaten die eigendom zijn van het bedrijf. IT-ondersteuningsmedewerkers kunnen geen herstelsleutels weergeven die tot persoonlijke apparaten behoren.   


## <a name="do-i-need-to-store-my-key"></a>Moet ik mijn sleutel opslaan?  
Een IT-ondersteuningsmedewerker laat u weten of u een persoonlijke herstelsleutel moet uploaden. U ontvangt mogelijk een melding van de bedrijfsportal-apps voor iOS/iPadOS of Android als de IT-afdeling van uw organisatie normaal gesproken op deze manier met u communiceert. 

Het wordt aanbevolen een herstelsleutel alleen te uploaden als u in een van de volgende categorieën valt:
* U hebt uw apparaat versleuteld voordat u het bij uw organisatie hebt ingeschreven. 
* U hebt uw apparaat handmatig versleuteld via de macOS-systeemvoorkeuren.   

Afhankelijk van het beleid van uw organisatie hebt u mogelijk geen toegang meer tot zakelijke resources op uw apparaat tot u uw sleutel hebt geüpload.  

## <a name="upload-personal-recovery-key"></a>Persoonlijke herstelsleutel uploaden 
Voer de volgende stappen uit om de persoonlijke FileVault-sleutel voor uw versleutelde Mac-apparaat op te slaan.  


1. Ga naar de [bedrijfsportalwebsite](https://portal.manage.microsoft.com) en meld u aan met uw school- of werkaccount. 
2. Selecteer uw versleutelde apparaat.
3. Selecteer **Herstelsleutel opslaan**.  
4. Voer de alfanumerieke FileVault-sleutel van 24 tekens in.  
5. Voer de sleutel opnieuw in. Selecteer vervolgens **Opslaan**.
6. Bedrijfsportal probeert uw persoonlijke herstelsleutel te verifiëren, draaien en op te slaan. Er is geen verdere actie vereist zodra de sleutel is opgeslagen. Als u de website verlaat voordat het uploaden is voltooid, kunt u de status weergeven op de pagina Details van apparaat als u zich volgende keer aanmeldt.  

Zie [Bedrijfsportal-berichten](store-recovery-key.md#company-portal-messages) voor meer informatie over de berichten die tijdens dit proces worden weergegeven.  

## <a name="company-portal-messages"></a>Berichten op de bedrijfsportal

|Bericht  |Betekenis  |
|---------|---------|
|De sleutels moeten overeenkomen. Controleer de sleutels en probeer het opnieuw.     | Wordt weergegeven onder het vak **Herstelsleutel bevestigen** om u te laten weten dat de sleutels niet met elkaar overeenkomen. Typ de sleutels in beide velden opnieuw en probeer ze vervolgens opnieuw op te slaan.        |
|Kan de herstelsleutel voor het apparaat niet bijwerken.| Wordt weergegeven als een pop-upmelding bovenaan het scherm om u te laten weten dat Bedrijfsportal geen herstelsleutel voor u kan opslaan. Selecteer uw versleutelde apparaat voor meer informatie. Lees vervolgens het bericht aan bovenaan de pagina voor de volgende stappen. |
|De herstelsleutel kan niet worden geüpload. Controleer of u de juiste sleutel hebt opgegeven en probeer het opnieuw. Probeer uw sleutel handmatig te draaien als het probleem zich blijft voordoen. Tik voor meer informatie.     | Wordt weergegeven op de pagina met details van het apparaat en kan een paar dingen betekenen: Ten eerste kan de Bedrijfsportal de sleutel niet draaien en opslaan omdat de ingevoerde sleutel onjuist is. Controleer of u de juiste sleutel hebt en probeer het opnieuw. De tweede mogelijkheid is dat uw apparaat al enige tijd niet is ingecheckt bij uw organisatie. Selecteer uw apparaat > **Status** > **Toegang controleren** om de meest recente updates van uw organisatie te synchroniseren. Probeer de herstelsleutel vervolgens opnieuw op te slaan. Als het probleem zich blijft voordoen, kan het ten slotte betekenen dat uw organisatie geen FileVault heeft ingeschakeld. Neem contact op met uw IT-ondersteuningsmedewerker om deze te informeren dat u uw apparaat hebt gesynchroniseerd, maar dat u uw FileVault-sleutel nog steeds niet kunt opslaan.         |
|Uw herstelsleutel is bijgewerkt. Meld u aan bij Bedrijfsportal en selecteer **Herstelsleutel ophalen** als u ooit geen toegang meer hebt tot uw apparaat en uw sleutel moet ophalen.    | Wordt weergegeven op de pagina met details van het apparaat. De sleutel die u hebt opgeslagen is gedraaid en de nieuwe persoonlijke herstelsleutel is opgeslagen.    |



## <a name="it-pro-support"></a>IT Pro-ondersteuning

Zie [FileVault-schijfversleuteling gebruiken voor macOS met Intune](../protect/encrypt-devices-filevault.md) als u een IT-ondersteuningsmedewerker bent en FileVault-versleuteling wilt configureren en beheren voor macOS-apparaten.  

## <a name="next-steps"></a>Volgende stappen

U kunt uw sleutel altijd ophalen via de bedrijfsportalwebsite, de Intune-app en de Bedrijfsportal-apps voor iOS en Android en deze gebruiken om toegang te krijgen tot uw Mac-apparaat. Zie [Herstelsleutel ophalen](get-recovery-key-cpweb.md) voor meer informatie over het ophalen van uw herstelsleutel.

Ontdek wat u nog meer kunt doen vanuit de bedrijfsportalwebsite. Zie [De Intune-bedrijfsportalwebsite gebruiken](using-the-intune-company-portal-website.md) voor een lijst met acties.  

Nog hulp nodig? Neem contact op met IT-ondersteuning. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).
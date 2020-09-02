---
title: Windows-apparaat verwijderen uit Intune-beheer
description: Hierin wordt beschreven hoe u een Windows-apparaat uit Intune-beheer kunt verwijderen
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/03/2018
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 018bda65-7238-41f5-b92a-e5f67b7fe085
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jieyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: d6cb9693f0bafcff22f3fce9d3f972e9eac41b22
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909088"
---
# <a name="remove-your-windows-device-from-management"></a>Windows-apparaat verwijderen uit beheer

U kunt een geregistreerd Windows-apparaat in de volgende gevallen verwijderen uit beheer:  
* U gebruikt dit apparaat niet meer voor werk of school. 
* U gebruikt dit apparaat niet meer voor toegang tot werk- of school-e-mails, -apps of andere bronnen.

Nadat u de registratie van het apparaat hebt verwijderd, hebt u op dit apparaat geen toegang meer tot school- en werkbronnen. U kunt de volgende Windows-apparaten uit beheer verwijderen.  
* Windows 10-apparaten 
* Windows 8.1-computer
* Windows 8.1-telefoon
 
Voor meer informatie over wat er gebeurt nadat u een apparaat hebt verwijderd uit beheer, raadpleegt u [Wat gebeurt er wanneer u de registratie van uw apparaat bij Intune ongedaan maakt?](what-happens-if-you-unenroll-your-device-from-intune-windows.md).  

## <a name="remove-your-windows-10-device"></a>Uw Windows 10-apparaat verwijderen
Voer de volgende stappen uit om een Windows 10-apparaat te verwijderen uit beheer.

### <a name="remove-in-company-portal-app-home-page"></a>Verwijderen in de bedrijfsportal-app: **startpagina**  

1. Open de app Bedrijfsportal.
2. Ga op de **startpagina** onderaan naar het gedeelte **Mijn apparaten**.
3. Selecteer het apparaat dat u wilt verwijderen.
3. Selecteer in de rechterbovenhoek van de pagina het pictogram **Meer info**.
4. Selecteer **Verwijderen**. 
5. Selecteer **Verwijderen** om te bevestigen dat u het apparaat wilt verwijderen.  

### <a name="remove-in-company-portal-app-device-context-menu"></a>Verwijderen in de bedrijfsportal-app: het contextmenu voor apparaten  

1. Open de bedrijfsportal-app en ga naar **Mijn apparaten**.

    ![Voorbeeldschermopname van de bedrijfsportal-app voor Windows: de startpagina met het gedeelte Mijn apparaten gemarkeerd.](./media/1809_CheckAccess_Context_Select_Device.png)

2. Klik met de rechtermuisknop op een apparaat of houd het apparaat ingedrukt om het [contextmenu](//windows/uwp/design/controls-and-patterns/menus) hiervan te openen.  

3. Selecteer **Verwijderen**.  

    ![Voorbeeldschermopname van de bedrijfsportal-app voor Windows: de startpagina. Het contextmenu van het apparaat kan worden bekeken in het gedeelte **Mijn apparaten** van de pagina. Hier ziet u de acties Naam wijzigen, Verwijderen en Toegang controleren.](./media/1809_DeviceContextMenu_Windows_CP.png)  

5. Klik in het bevestigingsbericht op **Meer informatie** om te lezen hoe uw toegang tot werk- en schoolbronnen mogelijk verandert. Selecteer **Verwijderen** om te bevestigen dat u het apparaat wilt verwijderen.   

     ![Voorbeeldschermopname van de bedrijfsportal-app voor Windows: de startpagina. Het veld Naam wijzigen wordt weergegeven bij apparaten. Hierin kan de gebruiker een nieuwe naam typen en op Naam wijzigen of Annuleren klikken.](./media/1808_RemoveDevice_Popup.png)  


### <a name="remove-in-device-settings-app"></a>Verwijderen in de app Instellingen van het apparaat
1. Open de app Instellingen. 
2. Ga naar **Accounts** > **Toegang tot werk of school**.
3. Selecteer het verbonden account dat u wilt verwijderen > **Loskoppelen**.
4. Selecteer **Ja** om te bevestigen dat u het apparaat wilt verwijderen.

## <a name="remove-your-windows-81-computer"></a>Uw Windows 8.1-computer verwijderen
Voer de volgende stappen uit om een Windows 8.1-apparaat te verwijderen uit Intune.

1. Ga naar **Pc-instellingen** > **Netwerk** > **Werkplek**.
2. Selecteer onder **Workplace Join** de optie **Verlaten**.
3. Selecteer onder **Apparaatbeheer inschakelen** de optie **Uitschakelen**.
4. Selecteer **Uitschakelen** in het pop-upvenster dat wordt geopend.

## <a name="remove-your-windows-81-phone"></a>Uw Windows 8.1-telefoon verwijderen
Voer de volgende stappen uit om een Windows 8.1-telefoon te verwijderen uit Intune.

1. Tik op **Instellingen** > **Werkplek**.
2. Tik op het werkplekaccount dat u wilt uitschrijven.
3. Tik boven in het scherm op **Verwijderen**.
4. Tik in het dialoogvenster **Account verwijderen** op **Verwijderen**.  
## <a name="removing-your-personal-information-after-removing-the-company-portal"></a>Uw persoonlijke gegevens verwijderen na het verwijderen van de bedrijfsportal  

Er zijn twee soorten gegevens die door de bedrijfsportal op uw Windows-apparaat worden opgeslagen:

- **Diagnostische logboeken**: standaardgegevens over app-activiteit die door Microsoft worden verzameld. Deze wordenautomatisch gewist zodra u de Bedrijfsportal-app verwijdert. Activiteitgegevens van een app omvatten bijvoorbeeld gegevens over hoelang de app geopend was en of de app is vastgelopen.
- **Toepassingscache**: ondersteuningsbestanden die de app nodig heeft om te kunnen werken, zoals pictogrammen en instellingen.

Als u de opgeslagen logboeken en de cache wilt verwijderen, voert u een van de volgende stappen uit:

* [De app Bedrijfsportal verwijderen](https://support.microsoft.com/help/4028003/windows-10-uninstall-apps-and-programs) 

* Stel de Bedrijfsportal-app opnieuw in. Open de app **Instellingen** en selecteer > **Apps** > **Bedrijfsportal** > **Geavanceerde opties** > **Opnieuw instellen**. 

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).
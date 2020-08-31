---
title: Uw Windows-apparaat handmatig synchroniseren | Microsoft Docs
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ba2f9d2e3f9e89d37b1dc8361cd80451155a6869
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820677"
---
# <a name="sync-your-windows-device-manually"></a>Uw Windows-apparaat handmatig synchroniseren

Voer een handmatige synchronisatie van uw apparaat uit als een app erg langzaam wordt geïnstalleerd. Bij een handmatige synchronisatie maakt uw apparaat verbinding met Intune en worden de nieuwste updates en communicatie opgehaald. De installatiesnelheid kan verbeteren nadat de apparaatsynchronisatie is voltooid.

Intune ondersteunt handmatige synchronisatie via de bedrijfsportal-app, de taakbalk of het menu Start op desktops en vanuit de app Instellingen van een apparaat. De functionaliteit van de bedrijfsportal-app wordt ondersteund op Windows 10-apparaten waarop de makersupdate (1703) of hoger wordt uitgevoerd. 

Alle Windows-apparaten kunnen worden gesynchroniseerd vanuit de app Instellingen van het apparaat, met inbegrip van:

* [Windows 10 Desktop](#windows-10-desktop)  
* [Microsoft HoloLens](#microsoft-hololens)   

## <a name="sync-directly-from-company-portal-app-for-windows"></a>Rechtstreeks synchroniseren vanuit de bedrijfsportal-app voor Windows
Voer deze stappen uit als u een Windows 10-apparaat wilt synchroniseren waarop makersupdate (versie 1709) of hoger wordt uitgevoerd.

1. Open de bedrijfsportal-app op uw apparaat.

2. Selecteer **Instellingen** > **Synchroniseren**.

    ![Schermafbeelding van de startpagina van de bedrijfsportal-app waarin Instellingen is gemarkeerd](./media/RS1_homePage_settings_04.png)  
    
    ![Schermafbeelding van de instellingenpagina van de bedrijfsportal-app waarin de knop Synchroniseren is gemarkeerd](./media/RS1_settingspage_sync05.png)  

## <a name="sync-from-device-taskbar-or-start-menu"></a>Synchroniseren vanaf de taakbalk van het apparaat of vanuit het menu Start   

U kunt ook het synchronisatiebesturingselement buiten de app openen, vanaf het bureaublad van uw apparaat. Dit kan handig zijn als u de app direct aan de taakbalk of aan het menu Start hebt vastgemaakt en snel wilt synchroniseren.  

1. Zoek het pictogram van de bedrijfsportal-app op de taakbalk of in het menu Start.  
2. Klik met de rechtermuisknop op het pictogram van de app, zodat het menu (ook wel een jumplijst genoemd) wordt weergegeven.  

    ![Schermafbeelding van de Windows-taakbalk op het bureaublad van een apparaat. Het pictogram van de bedrijfsportal-app is geselecteerd, waardoor er een menu met de opties Aan taakbalk vastmaken, Venster sluiten en Dit apparaat synchroniseren wordt weergegeven.](./media/sync-device-from-start-menu-1807.png)  

3. Selecteer **Dit apparaat synchroniseren**. De bedrijfsportal-app wordt geopend op de pagina **Instellingen** en de synchronisatie wordt gestart.  

## <a name="sync-from-settings-app"></a>Synchroniseren vanuit de app Instellingen 
Voltooi deze stappen als u uw Microsoft HoloLens- of Windows 10 desktopapparaat handmatig wilt synchroniseren vanuit de app Instellingen.  

### <a name="windows-10-desktop"></a>Windows 10 Desktop
1. Selecteer op het apparaat **Start** > **Instellingen**.

2. Selecteer **Accounts**.

    ![Accounts kiezen op de pagina Instellingen](./media/win10pc-sync-2-settings-accounts.png)  

3. Er bestaan meerdere versies van Windows 10 voor pc's. Vergelijk uw scherm met onderstaande schermafbeeldingen om te bepalen welke reeks stappen u moet volgen. 

    * Als in het scherm **Toegang tot werk of school** wordt weergegeven, gaat u verder met de stappen in [Toegang tot werk of school](#access-work-or-school-steps).

    ![Optie Toegang tot werk of school in app Instellingen](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

    * Als in het scherm **Toegang via het werknetwerk** wordt weergegeven, gaat u verder met de stappen onder [Toegang via het werknetwerk](#work-access-steps).  

    ![Toegang via het werknetwerk kiezen als het accounttype](./media/win10pc-sync-3-work-access.png)

### <a name="microsoft-hololens"></a>Microsoft HoloLens  
Deze instructies zijn van toepassing op HoloLens-apparaten waarop de Windows 10 Jubileumupdate (ook wel RS1 genoemd) wordt uitgevoerd.  

1. Open de app Instellingen op uw apparaat.  

2. Selecteer **Accounts** > **Toegang via werknetwerk**.  

    ![Schermafbeelding van de app Instellingen in HoloLens waarin de koppeling Accounts is gemarkeerd](./media/RS1_holoLens_SettingsRS1_Accounts_06.png)  

3. Selecteer uw verbonden account > **Synchroniseren**.  

    ![Schermafbeelding van de app Instellingen in HoloLens waarin de knop Synchroniseren is gemarkeerd](./media/RS1_holoLens_SyncRS1_Sync_08.png)   

#### <a name="access-work-or-school-steps"></a>Stappen voor toegang tot werk of school  

1. Selecteer **Toegang tot werk of school**.

    ![Schermafbeelding van de optie Toegang tot werk of school](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

2. Selecteer het account waarnaast het pictogram van een werkmap wordt weergegeven. Als u dit account helemaal niet ziet, heeft uw bedrijf uw instellingen mogelijk op een andere manier geconfigureerd. Selecteer in dat geval het account waarnaast een Microsoft-logo wordt weergegeven.

     ![Kies de naam van het account naast de aktetas of het Microsoft-logo](./media/win10pc-rs1-sync-info-button.png)

3. Selecteer **Info**. 

4. Selecteer **Synchroniseren**. 

#### <a name="work-access-steps"></a>Stappen voor toegang via het werknetwerk

1. Selecteer **Toegang via werknetwerk**.

    ![Toegang via het werknetwerk kiezen als het accounttype](./media/win10pc-sync-3-work-access.png)

2. Selecteer onder **Registreren voor apparaatbeheer** de naam van uw bedrijf.

    ![De naam van het bedrijf kiezen voor apparaatbeheer](./media/win10pc-sync-4-tap-com-name.png)

3. Selecteer **Synchroniseren**. De knop blijft uitgeschakeld totdat de synchronisatie is voltooid.

    ![De knop Synchroniseren kiezen](./media/win10pc-sync-5-tap-sync.png)  
    
## <a name="next-steps"></a>Volgende stappen  

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).

---
title: Een Android-apparaat inschrijven bij de Intune-bedrijfsportal | Microsoft Docs
description: Hierin wordt beschreven hoe u een Android-apparaat bij de Intune-bedrijfsportal kunt inschrijven
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/01/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 2ef0cf3909442cec818fd775bef4f848d6be5a83
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022310"
---
# <a name="enroll-your-device-with-company-portal"></a>Uw apparaat inschrijven bij de bedrijfsportal  
Schrijf uw persoonlijke of zakelijke Android-apparaat in voor veilige toegang tot uw zakelijke e-mail, apps en gegevens. De bedrijfsportal biedt ondersteuning voor Android-apparaten, inclusief Samsung Knox, met Android 4.4 en hoger.  
</br>
> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o?rel=0]

> [!NOTE]
> Samsung Knox is een beveiligingstype dat door sommige Samsung-apparaten wordt gebruikt als extra bescherming naast de beveiligingsfuncties van systeemeigen Android-apparaten. Als u wilt controleren of u een Samsung Knox-apparaat hebt, gaat u naar **Instellingen** > **Over apparaat**. Als de **Knox-versie** niet wordt vermeld, hebt u een systeemeigen Android-apparaat.

## <a name="enroll-device"></a>Een apparaat inschrijven  
Zorg ervoor dat u de Intune-bedrijfsportal-app hebt geïnstalleerd [uit Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal). Zie [Bedrijfsportal-app installeren in de Volksrepubliek China](install-company-portal-android-china.md) voor een lijst met app-stores die de app aanbieden in de Volksrepubliek China.

Tijdens de registratie wordt u mogelijk gevraagd om een categorie te kiezen die het beste beschrijft hoe u uw apparaat gebruikt. Het ondersteuningsteam van het bedrijf gebruikt uw antwoord om te controleren tot welke apps u toegang hebt.  

1. Open de bedrijfsportal-app en meld u aan met het account van uw werk of school.  

2. Als u wordt gevraagd de algemene voorwaarden van uw organisatie te accepteren, tikt u op **ACCEPT ALL**.  

   ![Voorbeeldafbeelding van de bedrijfsportal, scherm met de voorwaarden, waarin de knop Alles accepteren is gemarkeerd.](./media/accept-terms-1911.png)  


3. Bekijk wat wel en niet zichtbaar is in uw organisatie. Tik vervolgens op **doorgaan**.


    ![Voorbeeldafbeelding van het scherm Uw privacy is belangrijk voor ons in de Bedrijfsportal, waarin de knop Doorgaan is gemarkeerd.](./media/android-privacy-screen-1911.png)  
4. Bekijk wat u in de komende stappen kunt verwachten. Tik vervolgens op **VOLGENDE**.  

    ![Voorbeeldafbeelding van de bedrijfsportal, scherm De volgende stap, met de knop Volgende gemarkeerd.](./media/android-whats-next-1911.png)  


5. Afhankelijk van uw versie van Android wordt u mogelijk gevraagd om toegang tot bepaalde onderdelen van uw apparaat toe te staan. Deze prompts zijn vereist voor Google en worden niet beheerd door Microsoft.  

    Tik op **Toestaan** voor de volgende machtigingen:  
    * **De bedrijfsportal toestaan telefoongesprekken uit te voeren en te beheren**: Met deze machtiging kan uw apparaat het IMEI-nummer (International Mobile station Equipment Identity) delen met Intune, de apparaatbeheerprovider van uw organisatie. U kunt deze machtiging veilig toestaan. Microsoft zal nooit telefoongesprekken voeren of beheren.  
    * **Toestaan dat Bedrijfsportal toegang heeft tot uw contactpersonen**: Met deze machtiging kan de bedrijfsportal-app uw werkaccount maken, gebruiken en beheren.  U kunt deze machtiging veilig toestaan. Microsoft heeft nooit toegang tot uw contactpersonen. 

    Als u geen toestemming verleent, wordt u de volgende keer dat u zich aanmeldt bij de bedrijfsportal opnieuw gevraagd toestemming te verlenen. Als u deze berichten wilt uitschakelen, selecteert u **Niet opnieuw vragen**. Als u app-machtigingen wilt beheren, gaat u naar de app Instellingen > **Apps** > **Bedrijfsportal** > **Machtigingen** > **Telefoon**.  

6. Activeer de apparaatbeheerder-app. 

    Bedrijfsportal heeft apparaatbeheerdersmachtigingen nodig om uw apparaat veilig te beheren. Als u de app activeert, kan uw organisatie mogelijke beveiligingsproblemen identificeren, zoals herhaalde mislukte pogingen om uw apparaat te ontgrendelen, en daar op de juiste wijze op reageren.  

    ![Voorbeeldafbeelding van het scherm Apparaatbeheerder activeren, met de knop Activeren gemarkeerd.](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> Microsoft beheert de berichten op dit scherm niet. We begrijpen dat de formulering enigszins drastisch kan lijken. Bedrijfsportal kan niet opgeven welke beperkingen en toegang relevant zijn voor uw organisatie. Als u vragen hebt over hoe uw organisatie de app gebruikt, neemt u contact op met uw IT-ondersteuningsmedewerker. [Ga naar de website van de bedrijfsportal](https://go.microsoft.com/fwlink/?linkid=2010980) om de contactgegevens van uw organisatie op te zoeken.  


7. Het apparaat wordt ingeschreven. Als u een Samsung Knox-apparaat gebruikt, wordt u gevraagd het privacybeleid van de ELM-agent eerst te controleren en te bevestigen.   

    ![Voorbeeldafbeelding van het scherm Samsung Knox-privacybeleid dat wordt weer gegeven tijdens de inschrijving.](./media/and-enroll-7-knox-privacy-policy.png)  

8. Controleer in het scherm **Bedrijfstoegang instellen** of uw apparaat is ingeschreven. Tik vervolgens op **doorgaan**.  

    ![Voorbeeldafbeelding van de bedrijfsportal, scherm Bedrijfstoegang instellen, waarin Uw apparaat laten beheren is voltooid.](./media/update-settings-1911.png)  

9. In uw organisatie is mogelijk vereist dat u de apparaatinstellingen bijwerkt. Tik op **OMZETTEN** om een instelling aan te passen. Wanneer u klaar bent met het bijwerken van de instellingen, tikt u op **DOORGAAN**.  

   ![Voorbeeldafbeelding van Apparaatinstellingen bijwerken in de bedrijfsportal, waarin de knoppen Omzetten en Doorgaan zijn gemarkeerd.](./media/resolve-settings-1911.png)  

10. Wanneer de installatie is voltooid, tikt u op **GEREED**.    

    ![Voorbeeldafbeelding van het scherm Bedrijfstoegang instellen in de Bedrijfsportal, waarin de voltooide installatie en de knop Gereed zijn gemarkeerd.](./media/android-enrollment-done-1911.png) 

## <a name="next-steps"></a>Volgende stappen  

Ga naar **Instellingen** > **Beveiliging** en schakel **Onbekende bronnen** in voordat u een school- of bedrijfsapp installeert. Als u deze optie niet inschakelt, ziet u het volgende bericht wanneer u een app installeert: "Installatie geblokkeerd. Uw apparaat is uit veiligheidsoverwegingen zo ingesteld dat installaties van apps die afkomstig zijn van onbekende bronnen, worden geblokkeerd." U kunt tikken op **Instellingen** in het bericht om rechtstreeks naar **Onbekende bronnen**te gaan.  

> [!Note]
> Als uw organisatie gebruikmaakt van Telecom Expense Management-software, zijn er een aantal aanvullende stappen die u moet doorlopen om uw apparaat volledig in te schrijven. Zie [hier](enroll-your-device-with-telecom-expense-management-android.md) voor meer informatie.

Als er een fout optreedt bij het registreren van uw apparaat bij Intune, kunt u [een e-mailbericht naar het ondersteuningsteam van uw bedrijf verzenden](send-logs-to-your-it-admin-by-email-android.md).  

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).  
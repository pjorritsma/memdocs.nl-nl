---
title: Uw Mac inschrijven bij de Intune-bedrijfsportal | Microsoft Docs
description: Meer informatie over hoe u uw Mac registreert bij Intune met de bedrijfsportal-app.
keywords: Mac OS X, Mac OS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/16/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: kakyker
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 2ef7951217b0b6df21a86ca29a8637385aa65715
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "79337015"
---
# <a name="enroll-your-macos-device-using-the-company-portal-app"></a>Uw macOS-apparaat inschrijven via de bedrijfsportal-app  

Registreer uw macOS-apparaat met de bedrijfsportal-app van Intune voor beveiligde toegang tot e-mail, bestanden en apps van uw werk of school.

Organisaties verplichten u vaak om uw apparaat in te schrijven voordat u toegang krijgt tot de vertrouwelijke gegevens van de organisatie. Nadat uw apparaat is geregistreerd, wordt het *beheerd*. Uw organisatie kan beleid en apps aan het apparaat toewijzen via een MDM-provider (Mobile Device Management), zoals Intune. Voor continue toegang tot werk- of schoolgegevens op uw apparaat moet u uw apparaat zo configureren dat het overeenkomt met de beleidsinstellingen van uw organisatie.  

In dit artikel wordt beschreven hoe u met behulp van de bedrijfsportal-app voor macOS uw apparaat zo kunt registreren, configureren en onderhouden dat dit voldoet aan de vereisten van uw organisatie.  


## <a name="what-to-expect-from-the-company-portal-app"></a>Wat u kunt verwachten van de bedrijfsportal-app

Tijdens de eerste configuratie verplicht de bedrijfsportal-app u om u aan te melden en uzelf te verifiëren bij uw organisatie. Bedrijfsportal vertelt u vervolgens welke apparaatinstellingen u moet configureren om te voldoen aan de vereisten van uw organisatie. Organisaties stellen bijvoorbeeld vaak wachtwoordvereisten van een minimum- of maximumaantal tekens waaraan u moet voldoen.    

Nadat u uw apparaat hebt ingeschreven, wordt in de bedrijfsportal altijd gecontroleerd of uw apparaat is beveiligd volgens de vereisten van uw organisatie. Als u bijvoorbeeld een app van een niet-vertrouwde bron installeert, wordt in de bedrijfsportal een waarschuwing weergegeven en wordt de toegang tot de resources van uw organisatie mogelijk beperkt. Een app-beschermingsbeleid zoals dit komt veel voor. Om weer toegang te krijgen, moet u de niet-vertrouwde app waarschijnlijk verwijderen. 

Als uw organisatie na de registratie een nieuwe beveiligingsvereiste oplegt, zoals meervoudige verificatie, wordt u via de bedrijfsportal op de hoogte gebracht. U hebt de mogelijkheid om uw instellingen aan te passen, zodat u op uw apparaat kunt blijven werken.  

Zie [Wat gebeurt er wanneer ik de bedrijfsportal-app installeer en mijn apparaat inschrijf?](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md) voor meer informatie over de registratie.  

## <a name="get-your-macos-device-managed"></a>Uw macOS-apparaat laten beheren  
Gebruik de volgende stappen om uw macOS-apparaat in te schrijven bij uw organisatie. Op het apparaat moet macOS 10.12 of later worden uitgevoerd.   

> [!NOTE]
> Tijdens dit proces wordt u mogelijk gevraagd de bedrijfsportal toe te staan vertrouwelijke informatie te gebruiken die is opgeslagen in uw sleutelhanger. Deze instructies maken deel uit van Apple Security. Wanneer u de melding krijgt, typt u uw aanmeldingswachtwoord voor de sleutelhanger in en selecteert u **Altijd toestaan**. Als u op **Enter** of **Return** drukt op het toetsenbord, wordt in plaats daarvan **Toestaan** geselecteerd, wat kan leiden tot extra prompts.  

### <a name="install-company-portal-app"></a>De bedrijfsportal-app installeren  
1. Ga naar [Mijn Mac inschrijven](https://go.microsoft.com/fwlink/?linkid=853070).  
2. Het installatiebestand .pkg van de bedrijfsportal wordt gedownload. Open het installatieprogramma en doorloop de stappen. 
3. Ga akkoord met de gebruiksrechtovereenkomst van de software. 
4. Voer het apparaatwachtwoord of de geregistreerde vingerafdruk in om de software te installeren.  
5. Open Bedrijfsportal. 

> [!IMPORTANT]
> Microsoft AutoUpdate wordt mogelijk geopend om uw Microsoft-software bij te werken. Nadat alle updates zijn geïnstalleerd, opent u de bedrijfsportal-app. Installeer de meest recente versies van Microsoft AutoUpdate en de bedrijfsportal voor de beste installatie-ervaring.  


### <a name="enroll-your-mac"></a>Uw Mac inschrijven  


1. Meld u aan bij de bedrijfsportal met het account van uw werk of school.  
2. Wanneer de app wordt geopend, selecteert u **Beginnen**.  
3. Bekijk welke informatie op uw ingeschreven apparaat wel en niet zichtbaar is in uw organisatie. Selecteer vervolgens **Doorgaan**.
4.  Als u hierom wordt gevraagd, typt u het wachtwoord van uw apparaat in het scherm **Beheerprofiel installeren**.

    ![Voorbeeldschermopname van het scherm Beheerprofiel installeren in de bedrijfsportal met de wachtwoordprompt gemarkeerd.](./media/install-management-profile-macos-1912.PNG)   
5. Selecteer **Systeemvoorkeuren openen** in het scherm **Apparaatbeheer bevestigen**.  

    ![Voorbeeldschermopname van het scherm Apparaatbeheer bevestigen, met de knop 'Systeemvoorkeuren openen' gemarkeerd.](./media/confirm-device-management-macos-1912.PNG)  
6. De systeemvoorkeuren van uw apparaat worden geopend. Selecteer **Beheerprofiel** in de lijst met apparaatprofielen en selecteer vervolgens **Goedkeuren** > **Goedkeuren**.  
    ![Voorbeeldschermopname van het scherm Beheerprofiel in Systeemvoorkeuren met de knop 'Goedkeuren' gemarkeerd.](./media/management-profile-approve-macos-1912.PNG)   
1. Keer terug naar de bedrijfsportal en selecteer **Doorgaan**.    
2. In uw organisatie is mogelijk vereist dat u de apparaatinstellingen bijwerkt. Wanneer u klaar bent met het bijwerken van de instellingen, selecteert u **Instellingen controleren**.  

    ![Voorbeeldschermopname van het scherm Apparaatinstellingen bijwerken in de bedrijfsportal met de knop 'Instellingen controleren' gemarkeerd.](./media/update-settings-mac-1911.PNG)  
9. Wanneer de installatie is voltooid, selecteert u **Gereed**.  


 ## <a name="troubleshooting-and-feedback"></a>Probleemoplossing en feedback   

Als u tijdens de registratie problemen ondervindt, gaat u naar **Help** > **Diagnostische rapport verzenden** om het probleem te melden bij de Microsoft-app-ontwikkelaars. Deze informatie wordt gebruikt om de app te verbeteren. Ze gebruiken deze informatie ook om het probleem op te lossen als uw IT-ondersteuningsmedewerker om hulp vraagt.  

Nadat u het probleem hebt gemeld bij Microsoft, kunt u de details van uw ervaring naar uw IT-ondersteuningsmedewerker sturen. Selecteer **E-maildetails**. Typ in de hoofdtekst van het e-mailbericht wat u hebt ondervonden. Als u het e-mailadres van uw ondersteuningsmedewerker wilt zoeken, gaat u naar de bedrijfsportal-app > **Contact opnemen**. U kunt ook de [Bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980) raadplegen.  
 

Bovendien zou het Microsoft Intune-bedrijfsportalteam graag uw feedback horen. Ga naar **Help** > **Feedback verzenden** om uw ideeën te delen.  

## <a name="unverified-profiles"></a>Niet-geverifieerde profielen  
Wanneer u de geïnstalleerde MDM-profielen (Mobile Device Management) in **Systeemvoorkeuren** > **Profielen** weergeeft, hebben sommige profielen mogelijk de status Niet geverifieerd. Zolang het beheerprofiel de status Geverifieerd heeft, hoeft u zich geen zorgen te maken.  

Het beheerprofiel definieert de MDM-kanaalverbinding. Zolang het beheerprofiel is geverifieerd, nemen alle andere profielen die via dat kanaal aan de machine worden geleverd, de beveiligingseigenschappen van het beheerprofiel over.  

## <a name="updating-the-company-portal-app"></a>De bedrijfsportal-app bijwerken

U kunt de bedrijfsportal-app net als alle andere Office-apps bijwerken via Microsoft AutoUpdate voor macOS. U vindt hier meer informatie over het [bijwerken van Microsoft-apps voor macOS](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1).  

## <a name="next-steps"></a>Volgende stappen  
Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).  



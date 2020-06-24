---
title: Een Android-apparaat inschrijven met de Intune-bedrijfsportal en Intercede
description: Schrijf een Android-apparaat in en stel verificatie met afgeleide referenties in met Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a681020dded298e10d2bcb2fa20ebd7dd0c179e
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531771"
---
# <a name="set-up-android-device-with-company-portal-and-intercede"></a>Een Android-apparaat instellen via de bedrijfsportal en Intercede

Registreer uw apparaat met de Intune-bedrijfsportal voor beveiligde, mobiele toegang tot e-mail, bestanden en apps van uw organisatie. Nadat uw apparaat is geregistreerd, wordt het *beheerd*. Uw organisatie kan beleid en apps aan het apparaat toewijzen via een MDM-provider (Mobile Device Management), zoals Intune.

Tijdens de registratie installeert u ook een afgeleide referentie op het apparaat. Uw organisatie vereist mogelijk dat u de afgeleide referentie gebruikt als verificatiemethode bij het openen van resources of voor het ondertekenen en versleutelen van e-mailberichten.

U moet waarschijnlijk een afgeleide referentie instellen als u een smartcard gebruikt voor het volgende:

* Aanmelden bij school- of werk-apps, Wi-Fi en virtuele particuliere netwerken (VPN's)
* E-mailberichten voor school of werk ondertekenen en versleutelen met S/MIME-certificaten

In dit artikel gaat u het volgende doen:

* Schrijf een mobiel Android-apparaat in met de Intune-bedrijfsportal.
* Stel uw smartcard in door een afgeleide referentie te installeren van de provider van afgeleide referenties van uw organisatie, [Intercede](https://www.intercede.com/).  

## <a name="what-are-derived-credentials"></a>Wat zijn afgeleide referenties?

Een afgeleide referentie is een certificaat dat is afgeleid van uw smartcardreferenties en dat op uw apparaat is geïnstalleerd. Het biedt u externe toegang tot werkresources, waarbij wordt voorkomen dat onbevoegde gebruikers toegang krijgen tot gevoelige informatie.

Afgeleide referenties worden gebruikt voor het volgende:

* Studenten en medewerkers verifiëren die zich aanmelden bij school-of werk-apps, Wi-Fi en VPN
* E-mailberichten voor school of werk ondertekenen en versleutelen met S/MIME-certificaten

Afgeleide referenties zijn een implementatie van de NIST-richtlijnen (National Institute of Standards and Technology) voor afgeleide PIV-referenties (Personal Identity Verification) als onderdeel van Special Publication (SP) 800-157.

## <a name="prerequisites"></a>Vereisten

 Als u de inschrijving wilt voltooien, hebt u het volgende nodig:

* De smartcard van uw school of werk
* Toegang tot een computer of kiosk waarbij u zich kunt aanmelden met uw smartcard
* Een nieuw apparaat of een apparaat met fabrieksinstellingen met Android 7.0 of hoger
* De geïnstalleerde Microsoft Intune-app op uw apparaat

## <a name="enroll-device"></a>Een apparaat inschrijven  

1. Schakel uw nieuwe apparaat of het apparaat waarop de fabrieksinstellingen zijn hersteld in.  
2. Selecteer uw taal in het scherm **Welkom**. Als u het apparaat moet inschrijven met een QR-code of via NFC, volgt u de bijbehorende stappen.  
     * NFC: Houd het apparaat dat NFC ondersteunt tegen een programmeerapparaat om verbinding te maken met het bedrijfsnetwerk. Volg de instructies op het scherm. Wanneer het scherm met de servicevoorwaarden van Chrome wordt weergegeven, kunt u verder met stap 5.  

     * QR-code: Volg de stappen in [Inschrijven met behulp van QR-code](#qr-code-enrollment).  

     Als u een andere methode moet volgen, gaat u verder naar stap 3.    

3. Maak verbinding met Wi-Fi en tik op **VOLGENDE**. Volg de stap die overeenkomt met uw inschrijvingsmethode. 

    * Token: Wanneer het aanmeldscherm van Google wordt weergegeven, voert u de stappen uit die worden beschreven in [Tokeninschrijving](#token-enrollment).  
    * Google Zero Touch: Nadat u verbinding met Wi-Fi hebt gemaakt, wordt uw apparaat herkend door uw bedrijf. Ga verder met stap 4 en volg de instructies op het scherm totdat de installatie is voltooid.    
 
       ![Voorbeeldafbeelding van het scherm met de voorwaarden van Google dat verschijnt als u Google Zero Touch gebruikt, waarin de knop Accept & Continue is gemarkeerd.](./media/google-zero-touch-intune-app-01.png)   
   
4. Lees de voorwaarden van Google. Tik vervolgens op **ACCEPT & CONTINUE**.  

      ![Voorbeeldafbeelding van het scherm met de voorwaarden van Google, waarin de knop Accept & Continue is gemarkeerd.](./media/fully-managed-intune-app-04.png)   

5. Lees de servicevoorwaarden van Chrome. Tik vervolgens op **ACCEPT & CONTINUE**.  

   ![Voorbeeldafbeelding van het scherm met de servicevoorwaarden van Chrome, waarin de knop Accept & Continue is gemarkeerd.](./media/fully-managed-intune-app-06.png)  

6. Tik in het aanmeldingsscherm op **Aanmeldingsopties** en vervolgens op **Aanmelding vanaf een ander apparaat**. 

7. Schrijf de code op het scherm op.  

8. Schakel naar uw apparaat waarvoor smartcards zijn ingeschakeld en ga naar het webadres dat op uw scherm wordt weergegeven. 

9. Voer de code in die u eerder hebt geschreven.

   > [!div class="mx-imgBorder"]
   > ![Schermopname van de prompt Code invoeren van de bedrijfsportalwebsite.](./media/enter-code-intercede.png)

10. Plaats de smartcard om u aan te melden.  

11. Selecteer op het aanmeldingsscherm uw werk- of schoolaccount. Schakel vervolgens terug naar uw mobiele apparaat.

12. Afhankelijk van de vereisten van uw bedrijf, moet u mogelijk instellingen bijwerken, zoals schermvergrendeling of versleuteling. Als u hierom wordt gevraagd, tikt u op **INSTELLEN** en volgt u de instructies op het scherm.  

       ![Voorbeeldafbeelding van het instellen van uw zakelijke telefoon, waarin de knop Instellen is gemarkeerd.](./media/fully-managed-intune-app-10.png)   

13. Tik op **INSTALLEREN** om de bedrijfsapps op uw apparaat te installeren. Wanneer de installatie is voltooid, tikt u op **VOLGENDE**.  

       ![Voorbeeldafbeelding van het instellen van uw zakelijke telefoon, waarin de knop Installeren is gemarkeerd.](./media/fully-managed-intune-app-11.png)    

14. Tik op **START** om de Microsoft Intune-app te openen. 

    ![Voorbeeldafbeelding van het instellen van uw zakelijke telefoon, waarin de knop Starten is gemarkeerd.](./media/fully-managed-intune-app-17.png)   
 

15. Keer terug naar de Intune-app op uw mobiele apparaat en volg de instructies op het scherm tot uw inschrijving is voltooid. 

    ![Voorbeeldafbeelding van Toegang instellen, scherm apparaat registreren, knop Gereed gemarkeerd.](./media/fully-managed-intune-app-19.png)   

16. Ga verder met de sectie [Smartcard instellen](enroll-android-device-intercede.md#set-up-smart-card) in dit artikel om het instellen van uw apparaat te voltooien.  

### <a name="qr-code-enrollment"></a>Inschrijven met behulp van QR-code  
In deze sectie gaat u de QR-code scannen die u van uw bedrijf hebt ontvangen.  Wanneer u klaar bent, wordt u teruggeleid naar de stappen voor de registratie van het apparaat.     
  
1. Tik in het scherm **Welkom** vijf maal op het scherm om de installatie van de QR-code te starten.  

   ![Voorbeeldafbeelding van het scherm Welkom waarin de instructies voor tikken op het scherm zijn gemarkeerd.](./media/qr-code-intune-app-01.png)  

2. Volg de instructies op het scherm om verbinding te maken met Wi-Fi.  
3. Als uw apparaat geen QC-codescanner heeft, wordt in de installatieschermen de voortgang weergegeven als er een scanner is geïnstalleerd. Wacht tot de installatie is voltooid.  
4. Wanneer u hierom wordt gevraagd, scant u de QR-code van het inschrijvingsprofiel die u van uw bedrijf hebt ontvangen.  
5. Ga terug naar [Apparaat inschrijven](#enroll-device), stap 4, om door te gaan met de installatie.  

### <a name="token-enrollment"></a>Tokeninschrijving  
In deze sectie gaat u het token invoeren dat u van uw bedrijf hebt ontvangen. Wanneer u klaar bent, wordt u teruggeleid naar de stappen voor de registratie van het apparaat.  

1. Typ in het aanmeldscherm van Google **afw #setup** in het vak **E-mailadres of telefoonnummer**. Tik vervolgens op **Volgende**. 

   ![Voorbeeldafbeelding van het aanmeldscherm van Google waarin afw#setup in het veld is getypt.](./media/token-intune-app-01.png)   

2. Kies **Installeren** voor de app **Beleid voor Android-apparaat**. Ga verder met de installatie. Afhankelijk van uw apparaat moet u mogelijk aanvullende voorwaarden lezen en accepteren.    

3. Selecteer **Volgende** in het scherm **Dit apparaat inschrijven**.  

4. Selecteer **Code invoeren**.  

5. Typ in het scherm **Code scannen of invoeren** de code die u van uw bedrijf hebt ontvangen.  Klik op **Volgende**.  

   ![Voorbeeldafbeelding van het scherm Code scannen of invoeren, waarin de knop Volgende is gemarkeerd.](./media/token-intune-app-04.png)  

6. Ga terug naar [Apparaat inschrijven](#enroll-device), stap 4, om door te gaan met de installatie.

## <a name="set-up-smart-card"></a>Smartcard instellen  

1. Nadat de inschrijving is voltooid, ontvangt u via de Intune-app een melding over het instellen van uw smartcard. Tik op de melding. Als u geen melding ontvangt, controleert u uw e-mail.

   > [!div class="mx-imgBorder"]
   > ![Voorbeeldschermopname van de pushmelding van de bedrijfsportal op het startscherm van het apparaat.](./media/action-required-in-app-android.png)

2. Ga als volgt te werk op het scherm **Smartcard instellen**:

   1. Tik op de koppeling naar de installatie-instructies van uw organisatie. Als uw organisatie geen aanvullende instructies verstrekt, wordt u naar dit artikel gestuurd.

   2. Tik op **BEGINNEN**.  

   > [!div class="mx-imgBorder"]
   > ![Voorbeeldschermopname van het bedrijfsportalscherm Toegang tot mobiele smartcard instellen.](./media/smart-card-open-entrust-android.png)

3. Schakel over naar uw voor smartcard geschikte apparaat of selfservice-kiosk en open de app MyID. Meld u aan met uw werkreferenties.

4. Selecteer de optie om uw id aan te vragen.

5. Wanneer u wordt gevraagd welk profiel u wilt gebruiken, selecteert u de optie om te activeren met een mobiele referentie. Er wordt een QR-code weergegeven.  

6. Keer terug naar uw Android-apparaat. Tik in het scherm Bedrijfsportal > **QR-code ophalen** op **VOLGENDE**.

    > [!div class="mx-imgBorder"]
    > ![Voorbeeldschermopname van het bedrijfsportalscherm QR-code ophalen.](./media/get-qr-code-entrust-android.png)

7. Als u wordt gevraagd om de Intune-app in staat te stellen uw camera te gebruiken, tikt u op **Toestaan**.

8. Scan de afbeelding van de QR-code die op uw voor smartcard geschikte apparaat staat.

9. Via de Intune-app wordt begonnen met het downloaden en installeren van de certificaten die nodig zijn voor toegang tot werk- of schoolresources. Afhankelijk van uw internetverbinding kan dit proces enige tijd duren. Sluit de app tijdens dit proces niet.

    > [!div class="mx-imgBorder"]
    > ![Voorbeeldschermopname van het bedrijfsportalscherm Certificaten downloaden en installeren](./media/install-certificates-entrust-android.png)

10. Zodra alle certificaten zijn verwerkt, wacht u totdat het instellen van uw apparaat via de Intune-app is voltooid. Het instellen is voltooid als de melding **Gereed** wordt weergegeven op het scherm.

    > [!div class="mx-imgBorder"]
    > ![Voorbeeldschermopname van het scherm Gereed](./media/all-set-android.png)

## <a name="next-steps"></a>Volgende stappen

Nadat de inschrijving is voltooid, hebt u toegang tot werkresources, zoals e-mail, Wi-Fi en alle apps die uw organisatie beschikbaar stelt. Als u meer informatie wilt over het ophalen, zoeken, installeren en verwijderen van apps in de Intune-app, raadpleegt u:

* [Beheerde apps op een apparaat gebruiken](use-managed-apps-on-your-device-android.md)  
* [Apps beheren via de Bedrijfsportalwebsite](manage-apps-cpweb.md)  

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).

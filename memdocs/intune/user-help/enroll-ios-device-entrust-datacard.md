---
title: iOS- of iPadOS-apparaat inschrijven met Intune-bedrijfsportal en Entrust Datacard
description: Een iOS- of iPadOS-apparaat inschrijven en afgeleide referentieverificatie instellen met Entrust Datacard.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: e24a03f3706256c1d18efb2eaebf520a4312edb1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881532"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-entrust-datacard"></a>iOS- of iPadOS-apparaat instellen met Intune-bedrijfsportal en Entrust Datacard

Registreer uw apparaat met de Intune-bedrijfsportal voor beveiligde, mobiele toegang tot e-mail, bestanden en apps van uw organisatie. Nadat uw apparaat is geregistreerd, wordt het *beheerd*. Uw organisatie kan beleid en apps aan het apparaat toewijzen via een MDM-provider (Mobile Device Management), zoals Intune.  

Tijdens de registratie installeert u ook een afgeleide referentie op het apparaat. Uw organisatie vereist mogelijk dat u de afgeleide referentie gebruikt als verificatiemethode bij het openen van resources of voor het ondertekenen en versleutelen van e-mailberichten. 

U moet waarschijnlijk een afgeleide referentie instellen als u een smartcard gebruikt voor het volgende:  

* Aanmelden bij school- of werk-apps, Wi-Fi en virtuele particuliere netwerken (VPN's)
* E-mailberichten voor school of werk ondertekenen en versleutelen met S/MIME-certificaten  

In dit artikel gaat u het volgende doen:  

   * Een mobiel iOS- of iPadOS-apparaat inschrijven met Intune-bedrijfsportal.  
   * Een afgeleide referentie ophalen van de provider van afgeleide referenties van uw organisatie, [Entrust Datacard](https://www.entrustdatacard.com/).  

### <a name="what-are-derived-credentials"></a>Wat zijn afgeleide referenties?  
Een afgeleide referentie is een certificaat dat is afgeleid van uw smartcardreferenties en op uw apparaat is geïnstalleerd. Het biedt u externe toegang tot werkresources, waarbij wordt voorkomen dat onbevoegde gebruikers toegang krijgen tot gevoelige informatie.  

Afgeleide referenties worden gebruikt voor het volgende: 
* Studenten en medewerkers verifiëren die zich aanmelden bij school-of werk-apps, Wi-Fi en VPN
* E-mailberichten voor school of werk ondertekenen en versleutelen met S/MIME-certificaten

Afgeleide referenties zijn een implementatie van de NIST-richtlijnen (National Institute of Standards and Technology) voor afgeleide PIV-referenties (Personal Identity Verification) als onderdeel van Special Publication (SP) 800-157.  

## <a name="prerequisites"></a>Vereisten

 Als u de inschrijving wilt voltooien, hebt u het volgende nodig:

* De smartcard van uw school of werk
* Toegang tot een computer of kiosk waarbij u zich kunt aanmelden met uw smartcard
* Uw mobiele apparaat
* De Intune-bedrijfsportal-app voor iOS en iPadOS die op uw apparaat is geïnstalleerd  


## <a name="enroll-device"></a>Een apparaat inschrijven  
1. Open de bedrijfsportal-app voor iOS/iPadOS op uw mobiele apparaat en meld u aan met uw werkaccount.  

2. Schrijf de code op het scherm op.  

    ![Voorbeeldafbeelding van de bedrijfsportal-app met bericht en code op het scherm.](./media/copy-code-intercede.png)   

3. Schakel over naar het apparaat dat geschikt is voor smartcards en ga naar https://microsoft.com/devicelogin. 
4. Voer de code in die u eerder hebt geschreven.  

    ![Voorbeeldschermopname van de prompt 'Code invoeren' van de bedrijfsportalwebsite.](./media/enter-code-intercede.png)   

5. Plaats de smartcard om u aan te melden.   
6. Ga terug naar de bedrijfsportal-app op uw mobiele apparaat en volg de instructies op het scherm om uw apparaat in te schrijven.  
7. Zodra de inschrijving is voltooid, ontvangt u van de bedrijfsportal een melding over het instellen van uw smartcard. Tik op de melding. Als u geen melding ontvangt, controleert u uw e-mail.   

    ![Voorbeeldschermopname van de pushmelding van de bedrijfsportal op het startscherm van het apparaat.](./media/action-required-in-app-intercede.png)  

8. In het scherm **Toegang tot mobiele smartcard instellen**:   
    a. Tik op de koppeling naar de installatie-instructies van uw organisatie. Als uw organisatie geen aanvullende instructies verstrekt, wordt u naar dit artikel gestuurd.  
    b. Tik op **Beginnen**.  

    ![Voorbeeldschermopname van het bedrijfsportalscherm Toegang tot mobiele smartcard instellen.](./media/smart-card-info-intercede.png)

9. Schakel over naar het apparaat dat geschikt is voor smartcards en open IdentityGuard. 
10. Zoek het aanmeldingsgebied voor smartreferenties en selecteer de aanmeldknop.  
11. Wanneer u wordt gevraagd om een certificaat te selecteren, kiest u uw smartcardreferenties. Selecteer vervolgens **OK**. 
12. Voer de pincode van uw smartcard in.  
13. U wordt gevraagd om te kiezen uit een lijst met acties. Selecteer de actie waarmee u zich kunt inschrijven voor een afgeleide mobiele smartreferentie. Op de koppeling of knop staat iets als **Ik wil me inschrijven voor een afgeleide mobiele smartcardreferentie.**  
14. Selecteer dat u de voor smartreferenties geschikte toepassing hebt gedownload en geïnstalleerd. Ga dan door naar het volgende scherm.   
15. Voer informatie in over uw afgeleide smartcardreferentie.  
    a. Voer voor de identiteitsnaam een naam in, zoals *Afgeleide Entrust-referentie*.  
    b. Selecteer in het vervolgkeuzemenu **IdentityGudard Mobile Smart Credential**.  
    c. Ga door naar het volgende scherm. Er wordt een QR-code met een numeriek wachtwoord weergegeven.  

16. Ga terug naar uw mobiele apparaat. Tik in het scherm Bedrijfsportal > **QR-code ophalen** op **Doorgaan**. 

    ![Voorbeeldschermopname van het bedrijfsportalscherm QR-code ophalen.](./media/get-qr-code-intercede.png)  
17. Tik op **Camera gebruiken** > **OK**.  

    ![Voorbeeldschermopname van een bedrijfsportalprompt, waarin wordt gevraagd om toegang tot de camera toe te staan.](./media/allow-cp-camera-access-intercede.png)  
18. Scan de afbeelding van de QR-code die op uw voor smartcard geschikte apparaat staat.  
19. Voer het numerieke wachtwoord in dat wordt weergegeven onder de QR-code.  

    ![Voorbeeldschermopname van het bedrijfsportalscherm Wachtwoord vereist, veld Wachtwoord invoeren.](./media/enter-password-derived-credentials.png)   

20. Wacht tot uw apparaat in de bedrijfsportal is ingesteld.  


## <a name="next-steps"></a>Volgende stappen  
Nadat de inschrijving is voltooid, hebt u toegang tot werkresources, zoals e-mail, Wi-Fi en alle apps die uw organisatie beschikbaar stelt. Als u meer informatie wilt over hoe u apps ophaalt, zoekt, installeert en verwijdert in bedrijfsportal raadpleegt u:

* [Apps beheren via de Bedrijfsportalwebsite](manage-apps-cpweb.md)  
* [Beheerde apps op een apparaat gebruiken](use-managed-apps-on-your-device-ios.md)  

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).  

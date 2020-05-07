---
title: iOS- of iPadOS-apparaat inschrijven met Intune-bedrijfsportal en Intercede
description: Meer informatie over het registreren van een iOS- of iPadOS-apparaat en het instellen van afgeleide referentieverificatie met Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
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
ms.openlocfilehash: b83092521f1ab0058d47d599e7fd9c10c2fd6d35
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077764"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-intercede"></a>iOS- of iPadOS-apparaat instellen met de bedrijfsportal en Intercede

Registreer uw apparaat met de Intune-bedrijfsportal voor beveiligde, mobiele toegang tot e-mail, bestanden en apps van uw organisatie.  Nadat uw apparaat is geregistreerd, wordt het *beheerd*. Uw organisatie kan beleid en apps aan het apparaat toewijzen via een MDM-provider (Mobile Device Management), zoals Intune.  

Tijdens de registratie installeert u ook een afgeleide referentie op het apparaat. Uw organisatie vereist mogelijk dat u de afgeleide referentie gebruikt als verificatiemethode bij het openen van resources of voor het ondertekenen en versleutelen van e-mailberichten. 

U moet waarschijnlijk een afgeleide referentie instellen als u een smartcard gebruikt voor het volgende:

* Aanmelden bij school- of werk-apps, Wi-Fi en virtuele particuliere netwerken (VPN's)
* E-mailberichten voor school of werk ondertekenen en versleutelen met S/MIME-certificaten  

In dit artikel gaat u het volgende doen:  

* Een mobiel iOS- of iPadOS-apparaat inschrijven met Intune-bedrijfsportal.  
* Een afgeleide referentie ophalen van de provider van afgeleide referenties van uw organisatie, [Intercede](https://www.intercede.com/).   


## <a name="what-are-derived-credentials"></a>Wat zijn afgeleide referenties?  
Een afgeleide referentie is een certificaat dat is afgeleid van uw smartcardreferenties en op uw apparaat is geïnstalleerd. Het biedt u externe toegang tot werkresources, waarbij wordt voorkomen dat onbevoegde gebruikers toegang krijgen tot gevoelige informatie.  

Afgeleide referenties worden gebruikt voor het volgende: 
* Studenten en medewerkers verifiëren die zich aanmelden bij school-of werk-apps, Wi-Fi en VPN
* E-mailberichten voor school of werk ondertekenen en versleutelen met S/MIME-certificaten  

Afgeleide referenties zijn een implementatie van de NIST-richtlijnen (National Institute of Standards and Technology) voor afgeleide PIV-referenties (Personal Identity Verification) als onderdeel van Special Publication (SP) 800-157.  

## <a name="prerequisites"></a>Vereisten

 Als u de inschrijving wilt voltooien, hebt u het volgende nodig:

* De smartcard van uw school of werk
* Toegang tot een computer of selfservice-kiosk waarbij u zich kunt aanmelden met uw smartcard
* Uw mobiele apparaat
* De Intune-bedrijfsportal-app voor iOS en iPadOS die op uw apparaat is geïnstalleerd


## <a name="enroll-device"></a>Een apparaat inschrijven  
1. Open de bedrijfsportal-app voor iOS/iPadOS op uw mobiele apparaat en meld u aan met uw werkaccount.  
2. Schrijf de code op die op het scherm wordt weergegeven.  

    ![Voorbeeldafbeelding van de bedrijfsportal-app met bericht en code op het scherm.](./media/copy-code-intercede.png)  
1. Schakel over naar het apparaat dat geschikt is voor smartcards en ga naar https://microsoft.com/devicelogin. 

1. Voer de code in die u eerder hebt geschreven.
 
2. Plaats de smartcard om u aan te melden.   

3. Ga terug naar de bedrijfsportal-app op uw mobiele apparaat en volg de instructies op het scherm om uw apparaat in te schrijven.  
4. Zodra de inschrijving is voltooid, ontvangt u van de bedrijfsportal een melding over het instellen van uw smartcard. Tik op de melding. Als u geen melding ontvangt, controleert u uw e-mail.   

    ![Voorbeeldschermopname van de pushmelding van de bedrijfsportal op het startscherm van het apparaat.](./media/action-required-in-app-intercede.png)  

5. In het scherm **Toegang tot mobiele smartcard instellen**:  
    a. Tik op de koppeling naar de installatie-instructies van uw organisatie. Als uw organisatie geen aanvullende instructies verstrekt, wordt u naar dit artikel gestuurd.  
    b. Tik op **Beginnen**.  

    ![Voorbeeldschermopname van het bedrijfsportalscherm Toegang tot mobiele smartcard instellen.](./media/smart-card-info-intercede.png)  

6. Schakel over naar uw voor smartcard geschikte apparaat of selfservice-kiosk en open de app MyID. Meld u aan met uw werkreferenties.  
7. Selecteer de optie om uw id aan te vragen. 
8. Wanneer u wordt gevraagd welk profiel u wilt gebruiken, selecteert u de optie om te activeren met een mobiele referentie. Er wordt een QR-code weergegeven.  
9. Ga terug naar uw mobiele apparaat. Tik in het scherm Bedrijfsportal > **QR-code ophalen** op **Doorgaan**.  

    ![Voorbeeldschermopname van het bedrijfsportalscherm QR-code ophalen.](./media/get-qr-code-intercede.png) 
 
10. Tik op **Camera gebruiken** > **OK**.  

    ![Voorbeeldschermopname van een bedrijfsportalprompt, waarin wordt gevraagd om toegang tot de camera toe te staan.](./media/allow-cp-camera-access-intercede.png)  

11. Scan de afbeelding van de QR-code die op uw voor smartcard geschikte apparaat wordt weergegeven. 
12. Wacht tot uw apparaat in de bedrijfsportal is ingesteld.  

## <a name="next-steps"></a>Volgende stappen  
Nadat de inschrijving is voltooid, hebt u toegang tot werkresources, zoals e-mail, Wi-Fi en alle apps die uw organisatie beschikbaar stelt. Als u meer informatie wilt over hoe u apps ophaalt, zoekt, installeert en verwijdert in bedrijfsportal raadpleegt u:

* [Apps beheren via de Bedrijfsportalwebsite](manage-apps-cpweb.md)  
* [Beheerde apps op een apparaat gebruiken](use-managed-apps-on-your-device-ios.md)  

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).

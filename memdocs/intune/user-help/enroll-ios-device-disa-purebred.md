---
title: iOS- of iPadOS-apparaat inschrijven met Intune-bedrijfsportal en DISA Purebred
description: Meer informatie over het registreren van een iOS- of iPadOS-apparaat en het instellen van afgeleide referentieverificatie met DISA Purebred.
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
ms.openlocfilehash: 268ed874be65c9ade7f801b89528d1a23f176ee1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077798"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>iOS- of iPadOS-apparaat instellen met bedrijfsportal en DISA Purebred  

Registreer uw apparaat met de Intune-bedrijfsportal voor beveiligde, mobiele toegang tot e-mail, bestanden en apps van uw organisatie. Nadat uw apparaat is geregistreerd, wordt het *beheerd*. Uw organisatie kan beleid en apps aan het apparaat toewijzen via een MDM-provider (Mobile Device Management), zoals Intune.  

Tijdens de registratie installeert u ook een afgeleide referentie op het apparaat. Uw organisatie vereist mogelijk dat u de afgeleide referentie gebruikt als verificatiemethode bij het openen van resources of voor het ondertekenen en versleutelen van e-mailberichten. 

U moet waarschijnlijk een afgeleide referentie instellen als u een smartcard gebruikt voor het volgende:

* Aanmelden bij school- of werk-apps, Wi-Fi en virtuele particuliere netwerken (VPN's)
* E-mailberichten voor school of werk ondertekenen en versleutelen met S/MIME-certificaten  

In dit artikel gaat u het volgende doen:  

   * Een mobiel iOS- of iPadOS-apparaat inschrijven met Intune-bedrijfsportal.  
   * Een afgeleide referentie ophalen bij de provider van afgeleide referenties van uw organisatie, DISA Purebred: https:\//cyber.mil/pki-pke/purebred/.  

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
* Uw mobiele apparaat
* De Intune-bedrijfsportal-app voor iOS en iPadOS die op uw apparaat is geïnstalleerd   

Tijdens de installatie moet u ook contact opnemen met een Purebred-agent of-vertegenwoordiger.      

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
    b. Klik op **Openen** om de Purebred-app te openen.  

    ![Voorbeeldschermopname van het bedrijfsportalscherm Toegang tot mobiele smartcard instellen.](./media/smart-card-open-disa-purebred.png)  
9. Als u wordt gevraagd om de bedrijfsportal de app voor Purebred-registratie te laten openen, selecteert u **Openen**.   

    ![Voorbeeldschermopname van de bedrijfsportalprompt om DISA Purebred-app te openen.](./media/open-app-prompt-disa-purbred.png)  
10. Wanneer de app werkt, moet u samenwerken met de Purebred-agent van uw organisatie om het Purebred-configuratieprofiel vóór inschrijving te configureren en downloaden.   
11. Ga naar de app Instellingen > **Algemeen** > **Profielen en apparaatbeheer** > **Profiel installeren** en tik op **Installeren**.  
12. Voer uw apparaatwachtwoord in.  
13. Installeer het profiel. Mogelijk moet u meerdere keren op **Installeren** tikken om de installatie te starten. 
14. Ga terug naar de Purebred-registratie-app. Volg de instructies van uw Purebred-agent om door te gaan.  
 
15. Nadat u het configuratieprofiel hebt gedownload, gaat u naar de app Instellingen > **Algemeen** > **Profielen en apparaatbeheer** > **Profiel installeren** en tikt u op **Installeren**.   
16.  Voer uw apparaatwachtwoord in.
17. Installeer het profiel. Mogelijk moet u meerdere keren op **Installeren** tikken om de installatie te starten. 
18. Nadat de installatie is voltooid, keert u terug naar de bedrijfsportal-app.  
19.  In het scherm **Toegang tot mobiele smartcard instellen** tikt u op **Doorgaan**.  

20. In het scherm **Certificaten importeren** kunt u de afgeleide referentie ophalen en importeren die u hebt ontvangen van DISA Purebred.  

    a. Tik op **Doorgaan**.   

    ![Voorbeeldschermopname van het bedrijfsportalscherm Importcertificaten instellen.](./media/import-certificate-disa-purebred.png)  
    b. Ga naar iCloud Drive **Bladeren** > **Locaties** en tik op **Meer locaties**.  

    ![Voorbeeldschermopname van iCloud Drive, menu Bladeren met optie Meer locaties gemarkeerd.](./media/icloud-drive-more-locations.png)  
    c. Tik op de switch om **Purebred-sleutelhanger** in te schakelen.  

    ![Voorbeeldschermopname van iCloud Drive, weergave Bladeren, waarin is gemarkeerd dat de switch Purebred-sleutelhanger is ingeschakeld.](./media/icloud-drive-enable-purebred-keychain.png)   

    d. Tik op **Purebred-referentiepakket**.  

    ![Voorbeeldschermopname van een iOS-scherm met een te selecteren optie Purebred-referentiepakket.](./media/purebred-credential-package.png)  
    f. Er wordt een lijst met certificaten weergegeven. Selecteer een optie en tik vervolgens op **Sleutel importeren**.  

    ![Voorbeeldschermopname van een lijst met te selecteren certificaten, waarbij er al een is geselecteerd.](./media/import-purebred-keychain.png) 
21. Ga terug naar de bedrijfsportal-app en wacht tot bedrijfsportal uw apparaat heeft ingesteld.   

## <a name="next-steps"></a>Volgende stappen  
Nadat de inschrijving is voltooid, hebt u toegang tot werkresources, zoals e-mail, Wi-Fi en alle apps die uw organisatie beschikbaar stelt. Als u meer informatie wilt over hoe u apps ophaalt, zoekt, installeert en verwijdert in bedrijfsportal raadpleegt u:

* [Apps beheren via de Bedrijfsportalwebsite](manage-apps-cpweb.md)  
* [Beheerde apps op een apparaat gebruiken](use-managed-apps-on-your-device-ios.md)  

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).

---
title: Problemen oplossen met Jamf Pro-integratie met Microsoft Intune
titleSuffix: Microsoft Intune
description: Suggesties voor het oplossen van de meestvoorkomende problemen wanneer u Jamf Pro voor Mac-apparaten integreert met Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f685f1f3d009d7ba7a1dc061ec3025b2f8c96b5f
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084636"
---
# <a name="troubleshoot-integration-of-jamf-pro-with-microsoft-intune"></a>Problemen oplossen met integratie van Jamf Pro met Microsoft Intune

Dit artikel helpt Intune-beheerders om problemen met de integratie van Jamf Pro voor macOS met Intune te begrijpen en op te lossen.

> [!TIP]  
> Veel van de informatie in dit artikel is oorspronkelijk afkomstig uit [Problemen oplossen wanneer u Jamf met Microsoft Intune integreert](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune) op support.microsoft.com.

## <a name="prerequisites"></a>Vereisten

Voordat u begint met het oplossen van problemen, moet u wat basisinformatie verzamelen om het probleem duidelijk te maken en sneller een oplossing te vinden. Wanneer u bijvoorbeeld een probleem aantreft met betrekking tot de integratie van Jamf in Intune, moet u altijd controleren of aan alle voorwaarden is voldaan. Lees de volgende overwegingen voordat u begint met het oplossen van problemen:

- Lees de voorwaarden bij [Jamf Pro integreren met Intune](conditional-access-integrate-jamf.md#prerequisites).
- Alle gebruikers moeten over Microsoft Intune- en Microsoft AAD Premium P1-licenties beschikken 
- U moet over een gebruikersaccount met machtigingen voor integratie met Microsoft Intune beschikken in de Jamf Pro-console.
- U moet over een gebruikersaccount met globale beheerdersmachtigingen beschikken in Azure.


Houd rekening met de volgende informatie wanneer u de Jamf Pro-integratie met Intune onderzoekt: 
- Wat is het exacte foutbericht?
- Waar is het foutbericht?
- Wanneer is het probleem begonnen?  Heeft de Jamf Pro-integratie met Intune ooit gewerkt?
- Hoeveel gebruikers treft het probleem? Geldt het probleem voor alle gebruikers of voor bepaalde gebruikers?
- Voor hoeveel apparaten geldt het probleem? Geldt het probleem voor alle apparaten of voor bepaalde apparaten?
 

## <a name="common-problems"></a>Algemene problemen 

Met behulp van de volgende informatie kunt u algemene problemen voor apparaten identificeren en oplossen nadat u de integratie tussen Intune en Jamf Pro hebt ingesteld.  

| Probleem   | Meer informatie                  |
|-----------------|--------------------------|
| **Apparaten worden in Jamf Pro gemarkeerd met de status 'Reageert niet'**  | [Apparaten kunnen niet worden ingecheckt bij Jamf Pro of Azure AD](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **Gebruikers van Mac-apparaten wordt gevraagd zich met de sleutelhanger aan te melden wanneer ze een app openen Apparaten kunnen niet worden geregistreerd**  | [Gebruikers wordt gevraagd hun wachtwoord in te voeren zodat apps kunnen worden geregistreerd bij Azure AD](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app). |
| **Apparaten kunnen niet worden geregistreerd**  | De volgende oorzaken zijn mogelijk van toepassing: <br> **-** [***Oorzaak 1***: de Jamf Pro-app in Azure heeft niet de juiste machtigingen](#cause-1) <br> **-** [***Oorzaak 2***: er is een probleem met de app *Jamf Native macOS Connector* in Azure AD](#cause-2) <br> **-** [***Oorzaak 3***: de gebruiker heeft geen geldige Intune- of Jamf-licentie](#cause-3) <br> **-** [***Oorzaak 4***: de gebruiker heeft niet de Jamf-selfservice gebruikt om de bedrijfsportal-app te starten](#cause-4) <br> **-** [***Oorzaak 5***: Intune-integratie is uitgeschakeld](#cause-5) <br> **-** [***Oorzaak 6***: het apparaat was eerder ingeschreven in Intune, of de gebruiker heeft meerdere keren geprobeerd het apparaat te registreren](#cause-6) <br> **-** [***Oorzaak 7***: JamfAAD vraagt toegang aan tot een 'Microsoft Workplace Join Key' via de sleutelhanger van de gebruiker](#cause-7) |
|  **Mac-apparaat wordt als compatibel weergegeven in Intune maar als niet-compatibel in Azure** | [Problemen met de registratie van het apparaat](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **Dubbele invoer wordt weergegeven in de Intune-console voor Mac-apparaten die zijn ingeschreven met behulp van Jamf** | [Meerdere registraties vanaf hetzelfde apparaat](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **Het apparaat kan niet worden geëvalueerd door het nalevingsbeleid** | [Beleid is gericht op apparaatgroepen](#compliance-policy-fails-to-evaluate-the-device) |
| **Kan het toegangstoken voor Microsoft Graph API niet ophalen** | De volgende oorzaken zijn mogelijk van toepassing: <br> -[Machtigingen voor de Jamf Pro-app in Azure](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> - [Verlopen licentie voor Jamf of Intune](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-** [Poorten zijn niet open](#the-required-ports-arent-open-on-your-network)|
 

### <a name="devices-are-marked-as-unresponsive-in-jamf-pro"></a>Apparaten worden in Jamf Pro gemarkeerd met de status 'Reageert niet'  

**Oorzaak**: Wanneer apparaten in Jamf Pro met de status *Reageert niet* worden gemarkeerd, heeft dit vaak een van de volgende algemene oorzaken:

- Apparaat kan niet worden ingecheckt bij Jamf Pro.  
  Jamf Pro verwacht dat apparaten elke 15 minuten worden ingecheckt. Apparaten die binnen een periode van 24 uur niet inchecken, worden in Jamf gemarkeerd met de status 'Reageert niet'.  

- Apparaat wordt niet ingecheckt bij Azure AD.  
  Als macOS-apparaten worden geregistreerd bij Azure AD, ontvangt u hiervoor een Azure-token:
  - Dit token wordt elke 12 uur vernieuwd.   
  - Wanneer het token langer dan 24 uur niet wordt vernieuwd, wordt het apparaat in Jamf Pro met de status 'Reageert niet' gemarkeerd.  
  - Als het Azure-token verloopt, wordt gebruikers gevraagd zich bij Azure aan te melden om een nieuw token op te halen. Een vernieuwingstoken voor Azure-toegang wordt elke zeven dagen gegenereerd.

**Oplossing**  
Nadat een apparaat met de status *Reageert niet* is gemarkeerd in Jamf Pro, moet de ingeschreven gebruiker van het apparaat zich aanmelden om de status te herstellen. Dit moet de gebruiker zijn die het account via de werkplek heeft gekoppeld, aangezien hij of zij de identiteit van Intune in zijn of haar aanmeldsleutelhanger heeft staan.



### <a name="mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app"></a>Op Mac-apparaten wordt aan gebruikers gevraagd om zich met de sleutelhanger aan te melden wanneer ze een app openen  

Nadat u de integratie van Intune en Jamf Pro hebt geconfigureerd en voorwaardelijke toegangsbeleidsregels hebt geïmplementeerd, wordt gebruikers van apparaten die met Jamf Pro worden beheerd, gevraagd een wachtwoord in te voeren wanneer ze Microsoft Office 365-toepassingen openen zoals Teams, Outlook en andere apps waarvoor Azure AD-verificatie is vereist. 

Een prompt met tekst zoals in het volgende voorbeeld wordt bijvoorbeeld weergegeven wanneer Microsoft Teams wordt geopend:

``` 
  Microsoft Teams wants to sign using key "Microsoft Workplace Join Key" in your keychain.  
  To allow this, enter the "login" keychain password 
```

**Oorzaak**: Deze prompts worden gegenereerd door Jamf Pro voor elke van toepassing zijnde app waarvoor Azure AD-registratie is vereist. 

**Oplossing**   
Bij de prompt moeten gebruikers hun apparaatwachtwoord invoeren om zich aan te melden bij Azure AD. Opties zijn onder andere:
- **Weigeren**: niet aanmelden en niet de app gebruiken.
- **Toestaan**: een eenmalige aanmelding. Wanneer de app de volgende keer wordt geopend, wordt de gebruiker gevraagd zich opnieuw aan te melden.
- **Altijd toestaan**: de aanmeldreferenties worden in het cachegeheugen van de toepassing opgeslagen. Wanneer de app de volgende keer wordt geopend, wordt de gebruiker niet gevraagd zich aan te melden.  

Wanneer u *Altijd toestaan* voor de ene app selecteert, wordt alleen die app goedgekeurd voor toekomstig aanmelden. In extra apps wordt om verificatie gevraagd totdat ook deze apps zijn ingesteld op *Altijd toestaan*. Referenties die voor één app in de cache zijn opgeslagen, kunnen niet voor een andere app worden gebruikt.  

### <a name="devices-fail-to-register"></a>Apparaten kunnen niet worden geregistreerd  

Er zijn verschillende algemene oorzaken voor Mac-apparaten die kunnen niet worden geregistreerd.  

#### <a name="cause-1"></a>Oorzaak 1  

**De zakelijke Jamf Pro-toepassing in Azure heeft niet de juiste machtiging of heeft meer dan één machtiging**  

  Wanneer u de app in Azure maakt, moet u alle API-standaardmachtigingen verwijderen en vervolgens één machtiging van *update_device_attributes* aan Intune toewijzen. 

  **Oplossing**  
  Lees en corrigeer waar nodig de machtigingen voor de Jamf-app die u hebt gemaakt in Azure AD. Bekijk de procedure voor het [maken van een toepassing voor Jamf in Azure AD](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory). 

#### <a name="cause-2"></a>Oorzaak 2  

**De app **Jamf Native macOS Connector** is niet gemaakt in uw Azure AD-tenant of toestemming voor de connector is ondertekend door een account dat niet over globale beheerdersrechten beschikt**  

  **Oplossing**  
  Zie de sectie *macOS Intune-integratie configureren* in [Integratie met Microsoft Intune](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html) op docs.jamf.com. 

#### <a name="cause-3"></a>Oorzaak 3

**De gebruiker heeft geen geldige Intune- of Jamf-licentie**  

  Het ontbreken van een geldige licentie kan leiden tot de volgende fout, waarmee wordt aangegeven dat de Jamf-licentie is verlopen:  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **Oplossing**
  - Jamf-licentie: Neem contact op met Jamf voor hulp bij het verkrijgen van een nieuwe licentie voor Jamf.  
  - Intune-licentie: Wijs een geldige licentie aan de gebruiker toe of neem contact op met Microsoft of uw partner voor informatie over het verkrijgen van een actuele licentie.

#### <a name="cause-4"></a>Oorzaak 4  

**De gebruiker heeft niet de *Jamf-selfservice* gebruikt om de bedrijfsportal-app** te starten

Gebruikers die een apparaat willen inschrijven en registreren bij Intune door middel van Jamf, moeten de Jamf-selfservice gebruiken om de Intune-bedrijfsportal te openen. Als de gebruiker de bedrijfsportal handmatig opent, wordt het apparaat ingeschreven en geregistreerd zonder verbinding met Jamf.  

U kunt bepalen welke service wordt gebruikt voor het inschrijven en registreren van het apparaat door in de bedrijfsportal-app op het apparaat te kijken. Wanneer de registratie via Jamf is uitgevoerd, ontvangt u een melding om de selfservice-app te openen om wijzigingen door te voeren.

In de bedrijfsportal-app ziet de gebruiker mogelijk **`Not registered`** , en mogelijk wordt in de bedrijfsportal-logboeken invoer zoals in het volgende voorbeeld weergegeven:  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**Oplossing**  
U kunt de registratiebron als volgt van Intune wijzigen in Jamf:
1. [De registratie van het macOS-apparaat bij Intune ongedaan maken](https://docs.microsoft.com/mem/intune/user-help/unenroll-your-device-from-intune-macos). Om het voor apparaten die niet volledig uit Intune zijn verwijderd niet nog ingewikkelder te maken, raadpleegt u [*Oorzaak 6*](#cause-6) in deze lijst met oorzaken.  

2. Gebruik Jamf-selfservice op het apparaat om de bedrijfsportal-app te openen en het apparaat vervolgens in te schrijven bij Intune. Voor deze taak moet u [Jamf hebben gebruikt om de bedrijfsportal-app voor macOS te implementeren](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro) en [een beleid in Jamf Pro hebben gemaakt waarmee het gebruikersapparaat bij Azure AD wordt geregistreerd](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory).  

3. Wanneer de portal wordt geopend, wordt u op het eerste scherm gevraagd u aan te melden. Uw werk- of schoolaccount gebruiken  

4. De bedrijfsportal bevestigt uw accountgegevens en geeft de status van de apparaatregistratie en apparaatcompatibiliteit weer. Gele driehoeken markeren de acties die u moet uitvoeren om uw macOS-apparaat te beveiligen voor school of werk. Klik op Beginnen om de registratie te starten.  

5. Typ de aanmeldgegevens van uw computer in wanneer u daarom wordt gevraagd.  
     
Het duurt mogelijk enkele minuten om uw apparaat in beheer te registreren. Gedurende deze tijd kunt u andere dingen doen op uw apparaat. U krijgt een bericht zodra het instellen van de bedrijfstoegang is voltooid, zodat u weet dat u klaar bent.

#### <a name="cause-5"></a>Oorzaak 5  

**Intune-integratie is uitgeschakeld**

Als Intune-integratie is uitgeschakeld, krijgen gebruikers in de bedrijfsportal een pop-upvenster te zien met daarin het volgende bericht wanneer ze een apparaat proberen te registreren:  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

De Jamf Pro-server stuurt een puls naar de Intune-servers wanneer integratie is uitgeschakeld; zo weet Intune dat integratie is uitgeschakeld. 

**Oplossing**  
Schakel Intune-integratie opnieuw in via Jamf Pro. Zie [Microsoft Intune-integratie in Jamf Pro configureren](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro).


#### <a name="cause-6"></a><a name="cause-6"></a>Oorzaak 6  

**Het apparaat was eerder ingeschreven in Intune, of de gebruiker heeft meerdere keren geprobeerd het apparaat te registreren**

Als een apparaat uit Jamf wordt uitgeschreven maar niet op de juiste manier uit Intune wordt verwijderd, of wanneer gebruikers meerdere keren proberen het apparaat te registreren, ziet u mogelijk meerdere exemplaren van hetzelfde apparaat in de portal. Hierdoor mislukt de inschrijving bij Jamf.

**Oplossing**  
1. Start **Terminal** op het Mac-apparaat.
2. Voer **sudo JAMF removemdmprofile** uit.
3. Voer **sudo JAMF removeFramework** uit.
4. Verwijder de voorraadrecord van de computer van de JAMF Pro-server.
5. Verwijder het apparaat uit AzureAD.
6. Verwijder de volgende bestanden van het apparaat, indien deze aanwezig zijn:
   - /Library/Application Support/com.microsoft.CompanyPortal.usercontext.info
   - /Library/Application Support/com.microsoft.CompanyPortal
   - /Library/Application Support/com.jamfsoftware.selfservice.mac
   - /Library/Saved Application
   - State/com.jamfsoftware.selfservice.mac.savedState
   - /Library/Saved Application State/com.microsoft.CompanyPortal.savedState
   - /Library/Preferences/com.microsoft.CompanyPortal.plist
   - /Library/Preferences/com.jamfsoftware.selfservice.mac.plist
   - /Library/Preferences/com.jamfsoftware.management.jamfAAD.plist
   - /Users/<username>/Library/Cookies/com.microsoft.CompanyPortal.binarycookies
   - /Users/<username>/Library/Cookies/com.jamf.management.jamfAAD.binarycookies
   - com.microsoft.CompanyPortal
   - com.microsoft.CompanyPortal.HockeySDK
   - enterpriseregistration.windows.net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Microsoft Session Transport Key (openbare en persoonlijke sleutels)
   - Microsoft Workplace Join Key (openbare en persoonlijke sleutels)
7. Verwijder alles van de sleutelhanger op het apparaat waarmee wordt verwezen naar *Microsoft*, *Intune* of de *bedrijfsportal*, inclusief DeviceLogin.microsoft.com-certificaten. Verwijder verwijzingen naar *JAMF*, met uitzondering van de openbare en persoonlijke JAMF-sleutels. 
   > [!IMPORTANT]  
   > Wanneer u de openbare en persoonlijke sleutels verwijdert, wordt de apparaatinschrijving verbroken.

8. Verwijder alle volgende ingevoerde items, indien u deze aantreft:  
   - Type: Toepassingswachtwoord; account: com.microsoft.workplacejoin.thumbprint
   - Type: Toepassingswachtwoord; account: com.microsoft.workplacejoin.registeredUserPrincipalName
   - Type: Certificaat; uitgegeven door: MS-Organization-Access
   - Type: Voorkeur voor identiteit; naam (ADFS STS URL, indien aanwezig): https://adfs\<DNSName>.com/adfs/ls
   - Type: Voorkeur voor identiteit; naam: https://enterpriseregistration.windows.net
   - Type: Voorkeur voor identiteit; naam: https://enterpriseregistration.windows.net/  
9. Start het Mac-apparaat opnieuw op.
10. Verwijder de bedrijfsportal van het apparaat.
11. Ga naar portal.manage.microsoft.com en verwijder alle exemplaren van het Mac-apparaat. Wacht ten minste 30 minuten voordat u naar de volgende stap gaat.
12. Schrijft het apparaat opnieuw in bij JAMF Pro.
13. Open de selfservice weer en start het registratiebeleid.


#### <a name="cause-7"></a>Oorzaak 7  

**JamfAAD vraagt toegang aan tot een 'Microsoft Workplace Join Key' via de sleutelhanger van de gebruiker**

Tijdens de registratie ontvangen gebruikers van een macOS-apparaat de volgende vraag om JamfAAD toegang te verlenen tot een sleutel van hun sleutelhanger: 

```
   JamfAAD wants to access key "Microsoft Workplace Join Key" in your keychain. 
    
   To allow this, enter the "login" keychain password
```

**Oplossing**  
Gebruikers moeten hun accountwachtwoord opgeven en **Toestaan** selecteren om het apparaat bij Azure AD te registreren.

Deze aanvraag is vergelijkbaar met [de vraag aan gebruikers van Mac-apparaten om zich aan te melden met de sleutelhanger wanneer ze een app openen](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app), eerder in dit artikel.  

 
### <a name="mac-device-shows-compliant-in-intune-but-noncompliant-in-azure"></a>Mac-apparaat wordt als compatibel weergegeven in Intune maar als niet-compatibel in Azure  

**Oorzaak**: Door de volgende oorzaken kan het voorkomen dat een apparaat als compatibel wordt weergegeven in Intune maar als niet-compatibel in Azure:  
- Het apparaat is niet op de juiste manier geregistreerd.  
- Het apparaat is meerdere keren geregistreerd zonder de benodigde opschoonacties.

**Oplossing**  
U kunt dit probleem oplossen met de oplossing voor [*Oorzaak 6*](#cause-6) voor *apparaten die niet kunnen worden geregistreerd*, eerder in dit artikel. 


### <a name="duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf"></a>Dubbele invoer wordt weergegeven in de Intune-console voor Mac-apparaten die zijn ingeschreven met behulp van Jamf  
 
**Oorzaak**: Een apparaat wordt meerdere keren bij Intune geregistreerd, en wordt vaak opnieuw geregistreerd nadat het uit Intune is verwijderd.  

Wanneer een apparaat uit de integratie van Intune en Jamf Pro wordt verwijderd, is het mogelijk dat een aantal gegevens bewaard blijven, waardoor er dubbele vermeldingen ontstaan door opeenvolgende registraties.  

**Oplossing**  
U kunt dit probleem oplossen met de oplossing voor [*Oorzaak 6*](#cause-6) voor *apparaten die niet kunnen worden geregistreerd*, eerder in dit artikel. 

### <a name="compliance-policy-fails-to-evaluate-the-device"></a>Het apparaat kan niet worden geëvalueerd door het nalevingsbeleid  

**Oorzaak**: Jamf-integratie met Intune ondersteunt geen nalevingsbeleid voor apparaatgroepen. 

**Oplossing**  
Pas het nalevingsbeleid voor macOS-apparaten aan die aan gebruikersgroepen moeten worden toegewezen. 


### <a name="could-not-retrieve-the-access-token-for-microsoft-graph-api"></a>Kan de toegangstoken voor Microsoft Graph API niet ophalen

U ontvangt de volgende fout:

```
   Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.
```   

Deze fout kan door een van de volgende problemen zijn veroorzaakt: 

#### <a name="theres-a-permission-issue-with-the-jamf-pro-application-in-azure"></a>Er is sprake van een machtigingsprobleem met de Jamf Pro-toepassing in Azure

Tijdens de registratie van de Jamf Pro-app in Azure is een van de volgende situaties opgetreden:  
- De app heeft meer dan één machtiging ontvangen.
- De optie **Beheerderstoestemming verlenen voor *\<uw bedrijf>*** is niet geselecteerd.  

**Oplossing**  
Zie de oplossing voor oorzaak 1 voor [apparaten die niet kunnen worden geregistreerd](#devices-fail-to-register), eerder in dit artikel.

#### <a name="a-license-required-for-jamf-intune-integration-has-expired"></a>Een vereiste licentie voor Jamf-Intune-integratie is verlopen

**Oplossing**: Zie de oplossing voor oorzaak 3 voor [apparaten die niet kunnen worden geregistreerd](#devices-fail-to-register). 

#### <a name="the-required-ports-arent-open-on-your-network"></a>De vereiste poorten zijn niet geopend in uw netwerk

**Oplossing**: Lees de informatie voor netwerkpoorten bij de [voorwaarden](conditional-access-integrate-jamf.md#prerequisites) voor de integratie van Jamf Pro met Intune.


## <a name="next-steps"></a>Volgende stappen
Meer informatie over [de integratie van Jamf Pro met Intune](conditional-access-integrate-jamf.md)
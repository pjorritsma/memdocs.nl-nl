---
title: Nalevingsinstellingen voor Android-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk een overzicht van alle instellingen die u kunt gebruiken bij het instellen van naleving voor uw Android-apparaten in Microsoft Intune. Stel regels voor wachtwoorden in, kies een minimum- of maximumversie van het besturingssysteem, beperk bepaalde apps, voorkomen hergebruik van wachtwoorden, en meer.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f8cb75907befaa747ebae1718815d9722ff7085
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729219"
---
# <a name="android-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Android-instellingen om te markeren of apparaten wel of niet conform zijn met behulp van Intune

Dit artikel bevat een overzicht en beschrijving van de verschillende nalevingsinstellingen die u kunt configureren op Android-apparaten in Intune. Gebruik deze instellingen als onderdeel van uw MDM-oplossing (Mobile Device Management) om geroote (opengebroken) apparaten als niet-conform te markeren, een toegestaan bedreigingsniveau in te stellen, Google Play Protect in te schakelen, en meer.

Deze functie is van toepassing op:

- Android-apparaatbeheerder

Gebruik deze nalevingsinstellingen als Intune-beheerder om de resources van uw organisatie beter te beschermen. Zie [Aan de slag met apparaatnalevingsbeleid](device-compliance-get-started.md) voor meer informatie over nalevingsbeleid en wat dit doet.

## <a name="before-you-begin"></a>Voordat u begint

[Een nalevingsbeleid maken](create-compliance-policy.md#create-the-policy). Selecteer bij **Platform** de optie **Android-apparaatbeheerder**.

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

- **Vereisen dat het apparaat de risicoscore voor computers niet overschrijdt**  

  Selecteer de maximale toegestane risicoscore voor apparaten die door Microsoft Defender ATP worden geëvalueerd. Apparaten die deze score overschrijden, worden gemarkeerd als niet-compatibel.
  - **Niet geconfigureerd** (*standaard*)
  - **Veilig**
  - **Laag**
  - **Gemiddeld**
  - **Hoog**

## <a name="device-health"></a>Apparaatstatus

- **Apparaten die met de apparaatbeheerder worden beheerd**  
  De *Apparaatbeheerder*-mogelijkheden voor Android-apparaten zijn vervangen door Android Enterprise.

  - **Niet geconfigureerd** (*standaard*)
  - **Blokkeren**: wanneer apparaatbeheerder wordt geblokkeerd, worden gebruikers begeleid bij de overgang naar Android Enterprise-werkprofielbeheer om opnieuw toegang te krijgen.

- **Geroote apparaten**  
  Voorkom dat geroote apparaten toegang hebben tot bedrijfsgegevens. (Deze controle op naleving wordt ondersteund voor Android 4.0 en hoger)

  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Blokkeren** - Geroote (jailbroken) apparaten als niet-compatibel markeren.

- **Vereisen dat het apparaat zich op of onder het apparaatdreigingsniveau bevindt**  
  Gebruik deze instelling om de risicobeoordeling van een MTD-service (Mobile Threat Defense) bij bedreigingen te gebruiken als voorwaarde voor naleving.

  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Beveiligd** - Deze optie is het veiligst, omdat het apparaat geen bedreigingen kan hebben. Als een van de bedreigingsniveaus voor het apparaat wordt gedetecteerd, wordt het apparaat geëvalueerd als niet-compatibel.
  - **Laag** - Het apparaat wordt als compatibel beoordeeld als er alleen bedreigingen met een laag niveau op staan. Als een hoger niveau wordt aangetroffen, krijgt het apparaat de status niet-compatibel.
  - **Gemiddeld** - Het apparaat wordt als compatibel beoordeeld als bestaande bedreigingen op het apparaat van laag of gemiddeld niveau zijn. Als bedreigingen met hoog niveau worden aangetroffen op het apparaat, wordt het apparaat als niet-compatibel beoordeeld.
  - **Hoog** - Deze optie is het minst veilig, omdat alle bedreigingsniveaus zijn toegestaan. Deze optie kan handig zijn als u deze alleen gebruikt voor rapportagedoeleinden.

### <a name="google-play-protect"></a>Google Play Protect

- **Google Play Services is geconfigureerd**  
  Google Play Services maakt beveiligingsupdates mogelijk en vormt een basisafhankelijkheid voor veel beveiligingsfuncties op door Google gecertificeerde apparaten.

  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.  
  - **Vereisen** - Vereisen dat de app Google Play Services is geïnstalleerd en ingeschakeld.  

- **Bijgewerkte beveiligingsprovider**

  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Vereisen** - Vereisen dat het apparaat tegen bekende beveiligingsproblemen wordt beveiligd door een actuele beveiligingsprovider.

- **Bedreigingsscan voor apps**

  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Vereisen** - Hiermee kunt u vereisen dat de Android-functie **Apps controleren** is ingeschakeld.

  > [!NOTE]
  > Deze functie is op oudere Android-platforms een nalevingsinstelling. Intune kan alleen controleren of deze instelling is ingeschakeld op het apparaatniveau.

- **SafetyNet-attestation voor apparaat**  
  hiermee kunt u instellen aan welk integriteitsniveau voor [SafetyNet-attestation](https://developer.android.com/training/safetynet/attestation.html) het apparaat moet voldoen. Uw opties zijn:

  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Basisintegriteit controleren**
  - **Basisintegriteit en gecertificeerde apparaten controleren**

> [!NOTE]
> Zie [Beveiligingsbeleidsinstellingen voor Intune-apps](../apps/app-protection-policy-settings-android.md#conditional-launch) in Android om Google Play Protect-instellingen te configureren met behulp van beveiligingsbeleid voor apps.

## <a name="device-properties"></a>Apparaateigenschappen

### <a name="operating-system-version"></a>Versie van besturingssysteem

- **Minimale versie van het besturingssysteem**  
  als een apparaat niet voldoet aan de minimumvereisten met betrekking tot de versie van het besturingssysteem, wordt dit apparaat gerapporteerd als niet-compatibel. Er wordt een koppeling met informatie over het uitvoeren van een upgrade weergegeven. Gebruikers kunnen dan kiezen om een upgrade van hun apparaat uit te voeren, waarna ze toegang tot bedrijfsresources krijgen.

  *Standaard is er geen versie geconfigureerd*.

- **Maximale versie van het besturingssysteem**  
  Wanneer een apparaat een versie van het besturingssysteem gebruikt die hoger is dan de versie die is gespecificeerd in de regel, wordt de toegang tot bedrijfsresources geblokkeerd. De gebruiker wordt gevraagd contact op te nemen met de IT-beheerder. Tot er een wijziging is doorgevoerd in de regel om de versie van het besturingssysteem toe te staan, kan dit apparaat geen toegang tot bedrijfsresources krijgen.

  *Standaard is er geen versie geconfigureerd*.

## <a name="system-security"></a>Systeembeveiliging

### <a name="password"></a>Wachtwoord

- **Wachtwoord vereisen voor het ontgrendelen van mobiele apparaten**  
  *Wordt ondersteund op Android 4.0 en hoger of KNOX 4.0 of hoger.*

  Met deze beleidsinstelling geeft u aan of gebruikers een wachtwoord moeten invoeren om toegang te krijgen tot informatie op hun mobiele apparaat. Aanbevolen waarde: Vereist  

  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Vereisen** - Gebruikers moeten een wachtwoord invoeren voordat ze toegang kunnen krijgen tot hun apparaat.

- **Vereist wachtwoordtype**  
  *Wordt ondersteund op Android 4.0 en hoger of KNOX 4.0 of hoger.*

  kies of een wachtwoord alleen numerieke tekens mag bevatten of ook een combinatie van cijfers en andere tekens.

  - **Standaardwaarde apparaat**: als u de naleving van wachtwoorden wilt evalueren, selecteert u een andere wachtwoordsterkte dan **Standaardwaarde apparaat**.
  - **Lage beveiligingsbiometrie**
  - **Ten minste numeriek**
  - **Numeriek complex** - Herhaalde of opeenvolgende cijfers (zoals `1111` of `1234`) zijn niet toegestaan.
  - **Ten minste alfabetisch**
  - **Ten minste alfanumeriek**
  - **Minstens alfanumeriek met symbolen**

  Op basis van de configuratie van deze instelling zijn een of meer van de volgende opties beschikbaar:

  - **Minimale wachtwoordlengte**  
    *Wordt ondersteund op Android 4.0 en hoger of KNOX 4.0 of hoger.*

    Voer het minimale aantal cijfers of tekens in waaruit het wachtwoord van de gebruiker moet bestaan.

  - **Maximumaantal minuten inactief voordat wachtwoord is vereist**  
    *Wordt ondersteund op Android 4.0 en hoger of KNOX 4.0 of hoger.*

    Voer in na hoeveel niet-actieve tijd gebruikers hun wachtwoord opnieuw moeten invoeren. Als u **Niet geconfigureerd** (standaard) kiest, wordt deze instelling niet beoordeeld op naleving of niet-naleving.

  - **Het aantal dagen totdat het wachtwoord verloopt**  
  *Wordt ondersteund op Android 4.0 en hoger of KNOX 4.0 of hoger.*

  Selecteer het aantal dagen waarna het wachtwoord verloopt en de gebruiker een nieuw wachtwoord moet maken.

  - **Aantal eerdere wachtwoorden dat niet opnieuw mag worden gebruikt**  
    voer het aantal recente wachtwoorden in dat niet opnieuw mag worden gebruikt. Gebruik deze instelling om te voorkomen dat de gebruiker eerder gebruikte wachtwoorden hergebruikt. (Ondersteund voor Android 4.0 en hoger, of KNOX 4.0 en hoger.)

### <a name="encryption"></a>Versleuteling

- **Versleuteling van gegevensopslag op een apparaat**  
  *Wordt ondersteund op Android 4.0 en hoger of KNOX 4.0 of hoger.*

  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Vereisen**: de gegevensopslag op uw apparaten versleutelen. Apparaten worden versleuteld wanneer u de instelling **Wachtwoord vereisen voor het ontgrendelen van mobiele apparaten** kiest.

### <a name="device-security"></a>Apparaatbeveiliging

- **Apps van onbekende bronnen blokkeren**  
  *Ondersteund op Android 4.0 tot Android 7.x. Niet ondersteund in Android 8.0 en hoger*

  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Blokkeren**: blokkeer apparaten waarop **Beveiliging > Onbekende bronnen** is ingeschakeld. (*Wordt ondersteund op Android 4.0 tot en met Android 7.x. Wordt niet ondersteund op Android 8.0 en hoger*.)

  Als u sideloading wilt uitvoeren voor apps, moeten onbekende bronnen worden toegestaan. Als u Android-apps niet met behulp van sideloading laadt, stelt u deze functie in op **Blokkeren** om dit nalevingsbeleid in te schakelen.

  > [!IMPORTANT]
  > Voor sideloading van toepassingen moet de instelling **Apps uit onbekende bronnen blokkeren** zijn ingeschakeld. Dwing dit nalevingsbeleid alleen af als u Android-apps niet met behulp van sideloading op apparaten laadt.

- **Runtime-integriteit van de bedrijfsportal-app**
  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Vereisen** - Kies *Vereisen* om te bevestigen dat de bedrijfsportal-app aan alle volgende vereisten voldoet:

    - De reguliere runtime-omgeving is geïnstalleerd
    - Is correct ondertekend
    - Bevindt zich niet in de foutopsporingsmodus
    - Is geïnstalleerd via een bekende bron

- **USB-foutopsporing op apparaat blokkeren**  
  *(Wordt ondersteund op Android 4.2 en hoger)*

  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Blokkeren** - Voorkomen dat apparaten de functie voor USB-foutopsporing gebruiken.

- **Minimaal beveiligingspatchniveau**  
  *(Wordt ondersteund op Android 6.0 en hoger)*

  selecteer het oudste beveiligingspatchniveau dat een apparaat mag hebben. Apparaten die niet ten minste dit patchniveau hebben, zijn niet-conform. De datum moet worden opgegeven in de indeling `YYYY-MM-DD`.

  *Standaard is er geen datum geconfigureerd*.

- **Beperkte apps**  
  Voer de **appnaam** en de **app-bundel-id** in van apps die moeten worden beperkt, en selecteer vervolgens **Toevoegen**. Een apparaat waarop ten minste één beperkte app is geïnstalleerd, wordt gemarkeerd als niet-compatibel.

## <a name="next-steps"></a>Volgende stappen

- [Voeg acties voor niet-conforme apparaten toe](actions-for-noncompliance.md) en [gebruik bereiktags om beleidsregels te filteren](../fundamentals/scope-tags.md).
- [Controleer uw nalevingsbeleid](compliance-policy-monitor.md).
- Zie [Instellingen voor nalevingsbeleid voor Android Enterprise](compliance-policy-create-android-for-work.md)-apparaten.

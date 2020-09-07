---
title: Outlook voor iOS en Android beheren met Intune
description: Hanteer het Intune-beveiligings- en configuratiebeleid voor apps met Outlook voor iOS en Android zodat samenwerkingservaringen voor teams altijd onder veilige omstandigheden toegankelijk zijn.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ac2133455d4440e8048e7b9aba8f9f9b13d98a53
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996534"
---
# <a name="manage-messaging-collaboration-access-by-using-outlook-for-ios-and-android-with-microsoft-intune"></a>Toegang tot samenwerking via berichten beheren met behulp van Outlook voor iOS en Android met Microsoft Intune

Met de Outlook-app voor iOS en Android kunnen gebruikers in uw organisatie meer doen op hun mobiele apparaten met hun e-mail, agenda, contactpersonen en andere bestanden bij elkaar.

De meest veelzijdige en breedste beveiligingsmogelijkheden voor Microsoft 365-gegevens zijn beschikbaar wanneer u zich abonneert op de Enterprise Mobility + Security Suite, die functies bevat van Microsoft Intune en Azure Active Directory Premium, zoals voorwaardelijke toegang. U moet minimaal een beleid voor voorwaardelijke toegang implementeren dat connectiviteit toestaat voor Outlook voor iOS en Android vanaf mobiele apparaten en een Intune-beleid voor app-beveiliging dat ervoor zorgt dat de samenwerkingservaring wordt beschermd.

## <a name="apply-conditional-access"></a>Voorwaardelijke toegang toepassen
Organisaties kunnen gebruikmaken van het beleid voor voorwaardelijke toegang van Azure AD om ervoor te zorgen dat gebruikers alleen toegang hebben tot werk- of schoolinhoud met behulp van Outlook voor iOS en Android. Hiervoor hebt u een beleid voor voorwaardelijke toegang nodig dat zich richt op alle potentiële gebruikers. Meer informatie over het maken van dit beleid vindt u in [Beveiligingsbeleid voor apps vereisen voor toegang tot cloud-apps met voorwaardelijke toegang](/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Volg stap 1: Een beleid voor voorwaardelijke toegang tot Azure AD voor Office 365 configureren in [scenario 1: Voor Office 365-apps zijn goedgekeurde apps met app-beveiligingsbeleid vereist](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies) waarmee Outlook voor iOS en Android is toegestaan, maar Exchange ActiveSync-clients met OAuth worden geblokkeerd en geen verbinding kunnen maken met Exchange Online.

   > [!NOTE]
   > Dit beleid zorgt ervoor dat mobiele gebruikers toegang hebben tot alle Office-eindpunten met behulp van de toepasselijke apps.

2. Volg stap 2: Een beleid voor voorwaardelijke toegang voor Azure AD configureren voor Exchange Online met ActiveSync (EAS) in [scenario 1: Voor Office 365-apps zijn goedgekeurde apps met app-beveiligingsbeleid](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies) vereist, waarmee wordt voorkomen dat voor Exchange ActiveSync-clients basisverificatie wordt gebruikt om verbinding te maken met Exchange Online.

   In de bovenstaande beleidsregels wordt gebruikgemaakt van het toekenningsbeheer [Beleid voor app-beveiliging vereisen](/azure/active-directory/active-directory-conditional-access-technical-reference), dat ervoor zorgt dat beleid voor Intune-app-beveiliging wordt toegepast op het gekoppelde account in Outlook voor iOS en Android voordat toegang wordt verleend. Als de gebruiker niet is toegewezen aan een beveiligingsbeleid voor Intune-apps, geen licentie voor Intune heeft of als de app niet is opgenomen in het beleid voor Intune-app-beveiliging, voorkomt het beleid dat de gebruiker een toegangstoken kan verkrijgen en toegang kan krijgen tot berichtgegevens.

3. Volg ten slotte [Instructies: Verouderde verificatie voor Azure AD blokkeren met voorwaardelijke toegang](/azure/active-directory/conditional-access/block-legacy-authentication) voor het blokkeren van verouderde verificatie voor andere Exchange-protocollen op iOS-en Android-apparaten. Dit beleid moet alleen gericht zijn op Microsoft 365 Exchange Online-Cloud-apps en iOS-en Android-apparaatplatformen. Dit zorgt ervoor dat mobiele apps met behulp van Exchange Web Services-, IMAP4- of POP3-protocollen met basisverificatie geen verbinding kunnen maken met Exchange Online.

## <a name="create-intune-app-protection-policies"></a>Beveiligingsbeleid voor apps in Intune maken

App-beveiligingsbeleid (APP) bepaalt welke apps zijn toegestaan en welke acties deze kunnen uitvoeren met de gegevens van uw organisatie. Dankzij de opties die beschikbaar zijn in APP kunnen organisaties de beveiliging aanpassen aan hun specifieke behoeften. Het is mogelijk niet voor iedereen duidelijk welke beleidsinstellingen vereist zijn om een volledig scenario te implementeren. Microsoft heeft een taxonomie geïntroduceerd voor het APP-gegevensbeschermingsframework voor het beheer van mobiele iOS- en Android-apps om organisaties te helpen bij het bepalen van de prioriteit van de beveiliging van mobiele clienteindpunten.

Het APP-gegevensbeschermingsframework is onderverdeeld in drie afzonderlijke configuratieniveaus, waarbij elk niveau is gebaseerd op het vorige niveau:

- Met **Basisgegevensbescherming voor ondernemingen** (niveau 1) worden apps beveiligd met een pincode en versleuteld, en worden selectieve wisbewerkingen uitgevoerd. Voor Android-apparaten wordt met dit niveau Android-apparaatbevestiging gevalideerd. Dit is een configuratie op instapniveau die vergelijkbare gegevensbescherming biedt in het Exchange Online-postvakbeleid en die IT en de gebruikerspopulatie laat kennismaken met APP.
- Met **Geavanceerde gegevensbescherming voor ondernemingen** (niveau 2) worden mechanismen voor preventie van gegevenslekkage en minimale vereisten voor het besturingssysteem geïntroduceerd. Dit is de configuratie die van toepassing is op de meeste mobiele gebruikers die toegang hebben tot werk- of schoolgegevens.
- Met **Hoge gegevensbeveiliging voor ondernemingen** (niveau 3) worden geavanceerde mechanismen voor gegevensbeveiliging, verbeterde configuratie van de pincode en APP Mobile Threat Defense geïntroduceerd. Deze configuratie is wenselijk voor gebruikers die toegang hebben tot gegevens met een hoog risico.

Als u de specifieke aanbevelingen voor elk configuratieniveau en de apps die minimaal moeten worden beveiligd, wilt bekijken, bestudeert u [Gegevensbeschermingsframework met behulp van beveiligingsbeleid voor apps](app-protection-framework.md).

Of het apparaat nu wel of niet is ingeschreven in een UEM-oplossing (Unified endpoint Management), er moet een Intune-app-beveiligingsbeleid worden gemaakt voor zowel iOS- als Android-apps, met behulp van de stappen in [App-beveiligingsbeleid maken en toewijzen](app-protection-policies.md). Deze beleidsregels moeten minimaal voldoen aan de volgende voorwaarden:

1. Ze omvatten alle mobiele Microsoft 365-toepassingen, zoals Microsoft Edge, Outlook, OneDrive, Office of Teams, omdat dit ervoor zorgt dat gebruikers op een veilige manier toegang hebben tot werk- of schoolgegevens binnen elke Microsoft-app.

2. Ze worden toegewezen aan alle gebruikers. Dit zorgt ervoor dat alle gebruikers worden beveiligd, ongeacht of ze Outlook voor iOS of Android gebruiken.

3. Bepaal welk frameworkniveau voldoet aan uw vereisten. De meeste organisaties moeten de instellingen implementeren die zijn gedefinieerd in **Geavanceerde gegevensbescherming voor ondernemingen** (niveau 2), omdat hiermee besturingselementen voor gegevensbescherming en toegangsvereisten worden ingeschakeld.

Zie [Beveiligingsbeleidsinstellingen voor Android-apps](app-protection-policy-settings-android.md) en [Beveiligingsbeleidsinstellingen voor iOS-apps](app-protection-policy-settings-ios.md) voor meer informatie over de beschikbare instellingen.

> [!IMPORTANT]
> Als u Intune-app-beveiligingsbeleid wilt toepassen op apps op Android-apparaten die niet zijn ingeschreven bij Intune, moet de gebruiker ook de Intune-bedrijfsportal installeren. Raadpleeg [Wat u kunt verwachten wanneer uw Android-app wordt beheerd door een app-beveiligingsbeleid](../fundamentals/end-user-mam-apps-android.md) voor meer informatie.

## <a name="utilize-app-configuration"></a>Configuratie van apps gebruiken

Outlook voor iOS en Android ondersteunt app-instellingen waarmee Unified Endpoint Management-beheerders, zoals Microsoft Endpoint Manager, het gedrag van de app kunnen aanpassen.

App-configuratie kan worden geleverd via het OS-kanaal van Mobile Device Management (MDM) op geregistreerde apparaten (kanaal [Beheerde app-configuratie](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) voor iOS of kanaal [Android in de Enterprise](https://developer.android.com/work/managed-configurations) voor Android) of via het kanaal Intune-app-beveiligingsbeleid (APP). Outlook voor iOS en Android ondersteunt de volgende configuratiescenario's:

- Alleen werk- of schoolaccounts toestaan
- Algemene configuratie-instellingen voor apps
- S/MIME-instellingen
- Instellingen voor gegevensbeveiliging

Zie [Deploying Outlook for iOS and Android app configuration settings](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune) (Configuratie-instellingen voor de Outlook-app voor iOS en Android implementeren) voor specifieke stappen en gedetailleerde informatie over de configuratie-instellingen die de Outlook-app voor iOS en Android ondersteunt.

## <a name="next-steps"></a>Volgende stappen

- [Wat zijn beleidsregels voor de beveiliging van apps?](app-protection-policy.md) 
- [App-configuratiebeleid voor Microsoft Intune](app-configuration-policies-overview.md)
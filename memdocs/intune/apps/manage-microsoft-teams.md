---
title: Teams voor iOS en Android beheren met Intune
titleSuffix: ''
description: Hanteer het Intune-beveiligings- en configuratiebeleid voor apps met Teams voor iOS en Android zodat samenwerkingservaringen voor teams altijd onder veilige omstandigheden toegankelijk zijn.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1531de9ceab57b26bc9af5faac08673b8b758b0
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993097"
---
# <a name="manage-team-collaboration-access-by-using-teams-for-ios-and-android-with-microsoft-intune"></a>Toegang tot samenwerking als team beheren met behulp van Teams voor iOS en Android met Microsoft Intune

Microsoft Teams is de hub voor teamsamenwerking in Microsoft 365 die de personen, content en hulpprogramma's integreert die uw team nodig heeft om beter en effectiever te kunnen werken.

De meest veelzijdige en breedste beveiligingsmogelijkheden voor Microsoft 365-gegevens zijn beschikbaar wanneer u zich abonneert op de Enterprise Mobility + Security Suite, die functies bevat van Microsoft Intune en Azure Active Directory Premium, zoals voorwaardelijke toegang. U moet minimaal een beleid voor voorwaardelijke toegang implementeren dat connectiviteit toestaat voor Teams voor iOS en Android vanaf mobiele apparaten en een Intune-beleid voor app-beveiliging dat ervoor zorgt dat de samenwerkingservaring wordt beschermd.

## <a name="apply-conditional-access"></a>Voorwaardelijke toegang toepassen
Organisaties kunnen gebruikmaken van het beleid voor voorwaardelijke toegang van Azure AD om ervoor te zorgen dat gebruikers alleen toegang hebben tot werk- of schoolinhoud met behulp van Teams voor iOS en Android. Hiervoor hebt u een beleid voor voorwaardelijke toegang nodig dat zich richt op alle potentiële gebruikers. Meer informatie over het maken van dit beleid vindt u in [Beveiligingsbeleid voor apps vereisen voor toegang tot cloud-apps met voorwaardelijke toegang](/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Volg "Stap 1: Een beleid voor voorwaardelijke toegang tot Azure AD voor Office 365 configureren" in [scenario 1: Voor Office 365-apps zijn goedgekeurde apps met app-beveiligingsbeleid vereist](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), waarmee Teams voor iOS en Android is toegestaan, maar externe clients voor mobiele apparaten met OAuth worden geblokkeerd en geen verbinding kunnen maken met Office 365-eindpunten.

   >[!NOTE]
   > Dit beleid zorgt ervoor dat mobiele gebruikers toegang hebben tot alle Office-eindpunten met behulp van de toepasselijke apps.

## <a name="create-intune-app-protection-policies"></a>Beveiligingsbeleid voor apps in Intune maken

App-beveiligingsbeleid (APP) bepaalt welke apps zijn toegestaan en welke acties deze kunnen uitvoeren met de gegevens van uw organisatie. Dankzij de opties die beschikbaar zijn in APP kunnen organisaties de beveiliging aanpassen aan hun specifieke behoeften. Het is mogelijk niet voor iedereen duidelijk welke beleidsinstellingen vereist zijn om een volledig scenario te implementeren. Microsoft heeft een taxonomie geïntroduceerd voor het APP-gegevensbeschermingsframework voor het beheer van mobiele iOS- en Android-apps om organisaties te helpen bij het bepalen van de prioriteit van de beveiliging van mobiele clienteindpunten.

Het APP-gegevensbeschermingsframework is onderverdeeld in drie afzonderlijke configuratieniveaus, waarbij elk niveau is gebaseerd op het vorige niveau:

- Met **Basisgegevensbescherming voor ondernemingen** (niveau 1) worden apps beveiligd met een pincode en versleuteld, en worden selectieve wisbewerkingen uitgevoerd. Voor Android-apparaten wordt met dit niveau Android-apparaatbevestiging gevalideerd. Dit is een configuratie op instapniveau die vergelijkbare gegevensbescherming biedt in het Exchange Online-postvakbeleid en die IT en de gebruikerspopulatie laat kennismaken met APP.
- Met **Geavanceerde gegevensbescherming voor ondernemingen** (niveau 2) worden mechanismen voor preventie van gegevenslekkage en minimale vereisten voor het besturingssysteem geïntroduceerd. Dit is de configuratie die van toepassing is op de meeste mobiele gebruikers die toegang hebben tot werk- of schoolgegevens.
- Met **Hoge gegevensbeveiliging voor ondernemingen** (niveau 3) worden geavanceerde mechanismen voor gegevensbeveiliging, verbeterde configuratie van de pincode en APP Mobile Threat Defense geïntroduceerd. Deze configuratie is wenselijk voor gebruikers die toegang hebben tot gegevens met een hoog risico.

Als u de specifieke aanbevelingen voor elk configuratieniveau en de apps die minimaal moeten worden beveiligd, wilt bekijken, bestudeert u [Gegevensbeschermingsframework met behulp van beveiligingsbeleid voor apps](app-protection-framework.md).

Of het apparaat nu wel of niet is ingeschreven in een UEM-oplossing (Unified endpoint Management), er moet een Intune-app-beveiligingsbeleid worden gemaakt voor zowel iOS- als Android-apps, met behulp van de stappen in [App-beveiligingsbeleid maken en toewijzen](app-protection-policies.md). Deze beleidsregels moeten minimaal voldoen aan de volgende voorwaarden:

1. Ze omvatten alle mobiele Microsoft 365-toepassingen, zoals Microsoft Edge, Outlook, OneDrive, Office of Teams, omdat dit ervoor zorgt dat gebruikers op een veilige manier toegang hebben tot werk- of schoolgegevens binnen elke Microsoft-app.

2. Ze worden toegewezen aan alle gebruikers. Dit zorgt ervoor dat alle gebruikers worden beveiligd, ongeacht of ze Teams voor iOS of Android gebruiken.

3. Bepaal welk frameworkniveau voldoet aan uw vereisten. De meeste organisaties moeten de instellingen implementeren die zijn gedefinieerd in **Geavanceerde gegevensbescherming voor ondernemingen** (niveau 2), omdat hiermee besturingselementen voor gegevensbescherming en toegangsvereisten worden ingeschakeld.

Zie [Beveiligingsbeleidsinstellingen voor Android-apps](app-protection-policy-settings-android.md) en [Beveiligingsbeleidsinstellingen voor iOS-apps](app-protection-policy-settings-ios.md) voor meer informatie over de beschikbare instellingen.

> [!IMPORTANT]
> Als u Intune-app-beveiligingsbeleid wilt toepassen op apps op Android-apparaten die niet zijn ingeschreven bij Intune, moet de gebruiker ook de Intune-bedrijfsportal installeren. Raadpleeg [Wat u kunt verwachten wanneer uw Android-app wordt beheerd door een app-beveiligingsbeleid](../fundamentals/end-user-mam-apps-android.md) voor meer informatie.

## <a name="utilize-app-configuration"></a>Configuratie van apps gebruiken

Teams voor iOS en Android ondersteunt app-instellingen waarmee Unified Endpoint Management-beheerders, zoals Microsoft Endpoint Manager, het gedrag van de app kunnen aanpassen.

App-configuratie kan worden geleverd via het OS-kanaal van Mobile Device Management (MDM) op geregistreerde apparaten (kanaal [Beheerde app-configuratie](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) voor iOS of kanaal [Android in de Enterprise](https://developer.android.com/work/managed-configurations) voor Android) of via het kanaal Intune-app-beveiligingsbeleid (APP). Teams voor iOS en Android ondersteunt de volgende configuratiescenario's:

- Alleen werk- of schoolaccounts toestaan

> [!IMPORTANT]
> Voor configuratiescenario's waarvoor apparaatregistratie op Android is vereist, moeten de apparaten worden ingeschreven bij Android Enterprise en moet Teams voor Android worden geïmplementeerd via de Beheerde Google Play Store. Zie [Inschrijving van apparaten met Android Enterprise-werkprofielen instellen](../enrollment/android-work-profile-enroll.md) en [App-configuratiebeleid toevoegen voor beheerde Android Enterprise-apparaten](app-configuration-policies-use-android.md) voor meer informatie.

Elk configuratiescenario heeft zijn eigen specifieke vereisten. Bijvoorbeeld of voor het configuratiescenario apparaatregistratie vereist is en of dit hierdoor werkt met elke UEM-provider of dat Intune-app-beveiligingsbeleid vereist is.

> [!NOTE]
> Met Microsoft Endpoint Manager wordt de app-configuratie die via het MDM-OS-kanaal wordt geleverd, aangeduid als het app-configuratiebeleid (App Configuration Policy; ACP) **Beheerde apparaten**; app-configuratie die via het kanaal App-beveiligingsbeleid wordt geleverd, wordt het app-configuratiebeleid **Beheerde apps** genoemd.

## <a name="only-allow-work-or-school-accounts"></a>Alleen werk- of schoolaccounts toestaan

Het respecteren van het beleid voor gegevensbeveiliging en naleving van onze grootste en uiterst gereguleerde klanten is een belangrijke pijler van Microsoft 365. Sommige bedrijven zijn verplicht om alle communicatie-informatie in hun bedrijfsomgeving vast te leggen, en om ervoor te zorgen dat de apparaten alleen voor bedrijfscommunicatie worden gebruikt. Ter ondersteuning van deze vereisten kan Teams voor iOS en Android op geregistreerde apparaten zo worden geconfigureerd dat maar één bedrijfsaccount kan worden ingericht binnen de app.

Meer informatie over het configureren van de instelling voor door de organisatie toegestane accounts vindt u hier:

- [Android-instelling](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS-instelling](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Dit configuratiescenario werkt alleen met geregistreerde apparaten. Een UEM-provider wordt echter wel ondersteund. Als u geen gebruik maakt van Microsoft Endpoint Manager, moet u de UEM-documentatie raadplegen voor informatie over hoe u deze configuratiesleutels implementeert.

## <a name="next-steps"></a>Volgende stappen

- [Wat zijn beleidsregels voor de beveiliging van apps?](app-protection-policy.md) 
- [App-configuratiebeleid voor Microsoft Intune](app-configuration-policies-overview.md)
---
title: Office voor iOS en Android beheren met Intune
titleSuffix: ''
description: Hanteer het Intune-beveiligings- en configuratiebeleid voor apps met Office voor iOS en Android zodat samenwerkingservaringen altijd onder veilige omstandigheden toegankelijk zijn.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/09/2020
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
ms.openlocfilehash: 5d23eaeee839122bad46cd9619a790b9ca6332a6
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383254"
---
# <a name="manage-collaboration-experiences-using-office-for-ios-and-android-with-microsoft-intune"></a>Samenwerkingservaringen beheren met Office voor iOS en Android met Microsoft Intune

Office voor iOS en Android biedt verschillende belangrijke voordelen, waaronder:

- Word, Excel en PowerPoint worden gecombineerd op een manier die de ervaring vereenvoudigt met minder apps om te downloaden of tussen te schakelen. Het vergt veel minder telefoonopslag dan het installeren van afzonderlijke apps, terwijl u vrijwel alle mogelijkheden van de bestaande mobiele apps die mensen al kennen en gebruiken, behoudt.
- Integratie van de Office Lens-technologie om de kracht van de camera te ontgrendelen met mogelijkheden zoals het converteren van afbeeldingen naar bewerkbare Word- en Excel-documenten, het scannen van PDF's en het vastleggen van whiteboards met automatische digitale verbeteringen om de inhoud gemakkelijker te kunnen lezen.
- Het toevoegen van nieuwe functionaliteit voor veelvoorkomende taken die vaak voorkomen bij het werken op een telefoon, zoals het maken van snelle notities, het ondertekenen van PDF's, het scannen van QR-codes en het overdragen van bestanden tussen apparaten.

De meest veelzijdige en breedste beveiligingsmogelijkheden voor Office 365-gegevens zijn beschikbaar wanneer u zich abonneert op de Enterprise Mobility + Security Suite, die functies bevat van Microsoft Intune en Azure Active Directory Premium, zoals voorwaardelijke toegang. U moet minimaal een beleid voor voorwaardelijke toegang implementeren dat connectiviteit toestaat voor Office voor iOS en Android vanaf mobiele apparaten en een Intune-beleid voor app-beveiliging dat ervoor zorgt dat de samenwerkingservaring wordt beschermd.

## <a name="apply-conditional-access"></a>Voorwaardelijke toegang toepassen
Organisaties kunnen gebruikmaken van het beleid voor voorwaardelijke toegang van Azure AD om ervoor te zorgen dat gebruikers alleen toegang hebben tot werk- of schoolinhoud met behulp van Office voor iOS en Android. Hiervoor hebt u een beleid voor voorwaardelijke toegang nodig dat zich richt op alle potentiële gebruikers. Meer informatie over het maken van dit beleid vindt u in [Beveiligingsbeleid voor apps vereisen voor toegang tot cloud-apps met voorwaardelijke toegang](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Volg stap 1: Een beleid voor voorwaardelijke toegang tot Azure AD voor Office 365 configureren" in [scenario 1: Voor Office 365-apps zijn goedgekeurde apps met app-beveiligingsbeleid vereist](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), waarmee Office voor iOS en Android is toegestaan, maar externe clients voor mobiele apparaten met OAuth worden geblokkeerd en geen verbinding kunnen maken met Office 365-eindpunten.

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

2. Ze worden toegewezen aan alle gebruikers. Dit zorgt ervoor dat alle gebruikers worden beveiligd, ongeacht of ze Office voor iOS of Android gebruiken.

3. Bepaal welk frameworkniveau voldoet aan uw vereisten. De meeste organisaties moeten de instellingen implementeren die zijn gedefinieerd in **Geavanceerde gegevensbescherming voor ondernemingen** (niveau 2), omdat hiermee besturingselementen voor gegevensbescherming en toegangsvereisten worden ingeschakeld.

Zie [Beveiligingsbeleidsinstellingen voor Android-apps](app-protection-policy-settings-android.md) en [Beveiligingsbeleidsinstellingen voor iOS-apps](app-protection-policy-settings-ios.md) voor meer informatie over de beschikbare instellingen.

> [!IMPORTANT]
> Als u Intune-app-beveiligingsbeleid wilt toepassen op apps op Android-apparaten die niet zijn ingeschreven bij Intune, moet de gebruiker ook de Intune-bedrijfsportal installeren. Raadpleeg [Wat u kunt verwachten wanneer uw Android-app wordt beheerd door een app-beveiligingsbeleid](../fundamentals/end-user-mam-apps-android.md) voor meer informatie.

## <a name="utilize-app-configuration"></a>Configuratie van apps gebruiken

Office voor iOS en Android ondersteunt app-instellingen waarmee Unified Endpoint Management-beheerders, zoals Microsoft Endpoint Manager, het gedrag van de app kunnen aanpassen.

App-configuratie kan worden geleverd via het OS-kanaal van Mobile Device Management (MDM) op geregistreerde apparaten (kanaal [Beheerde app-configuratie](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) voor iOS of kanaal [Android in de Enterprise](https://developer.android.com/work/managed-configurations) voor Android) of via het kanaal Intune-app-beveiligingsbeleid (APP). Office voor iOS en Android ondersteunt de volgende configuratiescenario's:

- Alleen werk- of schoolaccounts toestaan
- Instellingen voor gegevensbeveiliging

> [!IMPORTANT]
> Voor configuratiescenario's waarvoor apparaatregistratie op Android is vereist, moeten de apparaten worden ingeschreven bij Android Enterprise en moet Office voor Android worden geïmplementeerd via de Beheerde Google Play Store. Zie [Inschrijving van apparaten met Android Enterprise-werkprofielen instellen](../enrollment/android-work-profile-enroll.md) en [App-configuratiebeleid toevoegen voor beheerde Android Enterprise-apparaten](app-configuration-policies-use-android.md) voor meer informatie.

Elk configuratiescenario heeft zijn eigen specifieke vereisten. Bijvoorbeeld of voor het configuratiescenario apparaatregistratie vereist is en of dit hierdoor werkt met elke UEM-provider of dat Intune-app-beveiligingsbeleid vereist is.

> [!NOTE]
> Met Microsoft Endpoint Manager wordt de app-configuratie die via het MDM-OS-kanaal wordt geleverd, aangeduid als het app-configuratiebeleid (App Configuration Policy; ACP) **Beheerde apparaten**; app-configuratie die via het kanaal App-beveiligingsbeleid wordt geleverd, wordt het app-configuratiebeleid **Beheerde apps** genoemd.

## <a name="only-allow-work-or-school-accounts"></a>Alleen werk- of schoolaccounts toestaan

Het respecteren van het beleid voor gegevensbeveiliging en naleving van onze grootste en uiterst gereguleerde klanten is een belangrijke pijler van Microsoft 365. Sommige bedrijven zijn verplicht om alle communicatie-informatie in hun bedrijfsomgeving vast te leggen, en om ervoor te zorgen dat de apparaten alleen voor bedrijfscommunicatie worden gebruikt. Ter ondersteuning van deze vereisten kan Office voor Android op geregistreerde apparaten zo worden geconfigureerd dat maar één bedrijfsaccount kan worden ingericht binnen de app.

Meer informatie over het configureren van de instelling voor door de organisatie toegestane accounts vindt u hier:

- [Android-instelling](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Dit configuratiescenario werkt alleen met geregistreerde apparaten. Een UEM-provider wordt echter wel ondersteund. Als u geen gebruik maakt van Microsoft Endpoint Manager, moet u de UEM-documentatie raadplegen voor informatie over hoe u deze configuratiesleutels implementeert.

> [!NOTE]
> Op dit moment ondersteunt alleen Office voor Android de modus voor door de organisatie toegestane accounts.

## <a name="data-protection-app-configuration-scenarios"></a>App-configuratiescenario's voor gegevensbescherming

Office voor iOS en Android ondersteunt beleidsregels voor app-configuratie door de instellingen voor gegevensbeveiliging te volgen wanneer de app wordt beheerd door Microsoft Endpoint Manager met een Intune-app-beveiligingsbeleid dat is toegepast op het werk- of schoolaccount dat is aangemeld bij de app:

- De Bestandsoverdracht via de actie Bestanden verzenden beheren
- Bestandsoverdrachten beheren via de actie In de buurt delen

Deze instellingen kunnen worden geïmplementeerd in de app, ongeacht de inschrijvingsstatus van het apparaat.

### <a name="manage-file-transfers"></a>Bestandsoverdrachten beheren

Office voor iOS en Android stelt gebruikers automatisch in staat om inhoud te delen met behulp van verschillende mechanismen:

- Als het bestand wordt gehost in OneDrive of SharePoint, kunnen gebruikers rechtstreeks vanuit het bestand een share-aanvraag initiëren.
- Gebruikers kunnen bestanden overdragen naar desktopsystemen met behulp van de actie **Bestanden overdragen**.
- Gebruikers kunnen bestanden delen met mobiele apparaten in de buurt met behulp van de actie **Delen in de buurt**.

De acties **Bestanden overdragen** en **Delen in de buurt** werken alleen met mediabestanden en lokale bestanden, en met bestanden die niet zijn beveiligd met een app-beveiligingsbeleid. 

|    Sleutel    |    Waarde    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.ShareNearby.IsAllowed.IntuneMAMOnly    |    **true** (standaard) schakelt de functie voor delen in de buurt voor het werk- of schoolaccount in<br>**false** schakelt de functie voor delen in de buurt voor het werk- of schoolaccount uit    |
|    com.microsoft.office.TransferFiles.IsAllowed.IntuneMAMOnly    |    **true** (standaard) schakelt de functie voor Bestanden verzenden voor het werk- of schoolaccount in<br>**false** schakelt de functie voor Bestanden verzenden voor het werk- of schoolaccount uit    |

### <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Configuratiescenario's voor apps implementeren met Microsoft Endpoint Manager

Als u Microsoft Endpoint Manager als uw provider voor het beheren van mobiele apps gebruikt, raadpleegt u [App-configuratiebeleidsregels toevoegen voor beheerde apps zonder apparaatinschrijving](app-configuration-policies-managed-app.md) over het maken van een app-configuratiebeleid voor beheerde apps. Dit is voor de configuratiescenario's voor de gegevensbeschermings-app. Nadat de configuratie is gemaakt, kunt u het beleid ervan toewijzen aan groepen gebruikers.

## <a name="next-steps"></a>Volgende stappen

- [Wat zijn beleidsregels voor de beveiliging van apps?](app-protection-policy.md) 
- [App-configuratiebeleid voor Microsoft Intune](app-configuration-policies-overview.md)
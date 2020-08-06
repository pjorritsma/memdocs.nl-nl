---
title: Beveiligingsconfiguraties voor Android Enterprise-werkprofiel
titleSuffix: Microsoft Intune
description: Krijg meer informatie over de beperkingen en instellingen die zijn voorgesteld voor standaardbeveiliging en hoge beveiliging voor Android Enterprise-apparaten.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4283caf8f21e87736b09a3d6c7b31f8daf1f6075
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546823"
---
# <a name="android-enterprise-work-profile-security-configurations"></a>Beveiligingsconfiguraties voor Android Enterprise-werkprofiel

Als onderdeel van het [configuratieframework voor beveiliging van Android Enterprise](android-configuration-framework.md) past u de volgende instellingen toe voor gebruikers van volledig beheerde mobiele Android Enterprise-apparaten. Zie [Android Enterprise-instellingen om apparaten te markeren als niet compatibel met behulp van Intune](../protect/compliance-policy-create-android-for-work.md#work-profile) en [Android Enterprise-apparaatinstellingen voor het toestaan of beperken van functies met behulp van Intune](../configuration/device-restrictions-android-for-work.md#work-profile-only) voor meer informatie over elke beleidsinstelling.

Wanneer u de instellingen kiest, moet u gebruiksscenario's controleren en categoriseren. Configureer vervolgens gebruikers volgens de richtlijnen voor het gekozen beveiligingsniveau. U kunt de voorgestelde instellingen aanpassen op basis van de behoeften van uw organisatie. Zorg ervoor dat uw beveiligingsteam de dreigingsomgeving, risicobereidheid en impact op de bruikbaarheid evalueert.

Er zijn twee aanbevolen configuratieframeworks voor beveiliging voor apparaten met een werkprofiel die persoonlijk eigendom zijn:

- [Werkprofiel: standaardbeveiliging (niveau 1)](#work-profile-basic-security) 
- [Werkprofiel: hoge beveiliging (niveau 3)](#work-profile-high-security) 

> [!Note]
> Vanwege de instellingen die beschikbaar zijn voor Android Enterprise-apparaten met een werkprofiel, bestaat er geen aanbieding voor uitgebreide beveiliging (niveau 2). De beschikbare instellingen rechtvaardigen geen verschil tussen niveau 1 en niveau 2.

## <a name="work-profile-basic-security"></a>Werkprofiel: standaardbeveiliging

Niveau 1 is de aanbevolen minimale beveiligingsconfiguratie voor persoonlijke apparaten waarop gebruikers toegang hebben tot werk- of schoolgegevens. Deze configuratie kan van toepassing zijn op de meeste mobiele gebruikers. Sommige van de besturingselementen kunnen van invloed zijn op de gebruikerservaring.

### <a name="device-compliance"></a>Apparaatcompatibiliteit

| Sectie | Instelling | Waarde | Opmerkingen |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Vereisen dat het apparaat de risicoscore voor computers niet overschrijdt | Niet geconfigureerd ||
| Apparaatstatus | Geroote apparaten | Blokkeren ||
| Apparaatstatus | Vereisen dat het apparaat zich op of onder het apparaatdreigingsniveau bevindt | Niet geconfigureerd||
| Apparaatstatus | Google Play Services is geconfigureerd | Vereist ||
| Apparaatstatus | Bijgewerkte beveiligingsprovider | Vereist ||
| Apparaatstatus | SafetyNet-apparaatattestation | Basisintegriteit en gecertificeerde apparaten controleren | Met deze instelling wordt SafetyNet-attestation van Google geconfigureerd op de apparaten van eindgebruikers. Met basisintegriteit wordt de integriteit van het apparaat gevalideerd. Geroote apparaten, emulators, virtuele apparaten en apparaten met zichtbare sabotagesporen voldoen niet aan de basisintegriteit.<p>Met basisintegriteit en gecertificeerde apparaten worden de compatibiliteit van het apparaat met services van Google gevalideerd. Alleen niet-aangepaste apparaten die door Google zijn gecertificeerd, voldoen aan deze controle. |
| Apparaateigenschappen | Minimale versie van het besturingssysteem | Indeling: Major.Minor<br>Voorbeeld: 5.0| Microsoft raadt aan de minimale primaire versie van Android te configureren, zodat deze overeenkomt met de ondersteunde Android-versies voor Microsoft-apps. OEM's en apparaten die voldoen aan de aanbevolen Android Enterprise-vereisten, moeten ondersteuning bieden voor de release die nu wordt vrijgegeven + upgrade van één letter. Op dit moment wordt Android 8.0 of hoger door Android aangeraden voor kennismedewerkers. Zie [Aanbevolen Android Enterprise-vereisten](https://www.android.com/enterprise/recommended/requirements/) voor de nieuwste aanbevelingen van Android. |
| Apparaateigenschappen | Maximale versie van het besturingssysteem | Niet geconfigureerd ||
| Systeembeveiliging | Wachtwoord vereist voor het ontgrendelen van mobiele apparaten | Vereist ||
| Systeembeveiliging | Vereist wachtwoordtype | Complex numeriek | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Systeembeveiliging | Minimale wachtwoordlengte | 6 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Systeembeveiliging | Maximumaantal minuten inactief voordat wachtwoord is vereist| 5 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid.|
| Systeembeveiliging | Het aantal dagen totdat het wachtwoord verloopt| Niet geconfigureerd | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Systeembeveiliging | Aantal eerdere wachtwoorden dat niet mag worden gebruikt | Niet geconfigureerd | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Systeembeveiliging | Versleuteling van gegevensopslag op apparaat | Vereist ||
| Systeembeveiliging | Apps van onbekende bronnen blokkeren | Blokkeren ||
| Systeembeveiliging | Runtime-integriteit van de bedrijfsportal-app | Vereist ||
| Systeembeveiliging | USB-foutopsporing op apparaat blokkeren | Blokkeren | Naast dat deze instelling foutopsporing met behulp van een USB-apparaat blokkeert, is ook de mogelijkheid voor het verzamelen van logboeken uitgeschakeld, wat handig kan zijn bij het oplossen van problemen. |
| Systeembeveiliging | Minimaal beveiligingspatchniveau | Niet geconfigureerd | Android-apparaten kunnen maandelijkse beveiligingspatches ontvangen, maar de release is afhankelijk van OEM's en/of providers. Organisaties moeten ervoor zorgen dat geïmplementeerde Android-apparaten beveiligingspatches ontvangen voordat deze instelling wordt geïmplementeerd. Zie [Android-beveiligingsbulletins](https://source.android.com/security/bulletin/) voor de nieuwste patchreleases. |
| Acties voor niet-nageleefd | Het apparaat markeren als niet-compatibel | Onmiddellijk | Het beleid is standaard zo geconfigureerd dat het apparaat wordt gemarkeerd als niet-compatibel. Er zijn aanvullende acties beschikbaar. Zie [Acties configureren voor niet-compatibele apparaten in Intune](../protect/actions-for-noncompliance.md) voor meer informatie.|

### <a name="device-restrictions"></a>Apparaatbeperkingen

| Sectie | Instelling | Waarde | Opmerkingen |
| ----- | ----- | ----- | ----- |
| Werkprofielinstellingen | Kopiëren en plakken tussen werkprofielen en persoonlijke profielen | Blokkeren ||
| Werkprofielinstellingen | Gegevens delen tussen werkprofielen en persoonlijke profielen | Met apps in het werkprofiel kunnen aanvragen voor delen van het persoonlijke profiel worden verwerkt ||
| Werkprofielinstellingen | Werkprofielmeldingen terwijl het apparaat is vergrendeld | Niet geconfigureerd | Als u deze instelling blokkeert, zijn gevoelige gegevens niet beschikbaar in werkprofielmeldingen, wat de bruikbaarheid kan beïnvloeden. |
| Werkprofielinstellingen | Standaardapp-machtigingen | Standaardwaarde apparaat | Beheerders moeten de machtigingen controleren en aanpassen die worden verleend via apps die ze implementeren. |
| Werkprofielinstellingen | Accounts toevoegen en verwijderen | Blokkeren ||
| Werkprofielinstellingen | Contactpersoon delen via Bluetooth | Inschakelen | Toegang tot zakelijke contactpersonen is standaard niet beschikbaar op andere apparaten, zoals auto's via Bluetooth-integratie. Het inschakelen van deze instelling verbetert de handsfree-gebruikerservaring. De contactpersonen kunnen via het Bluetooth-apparaat echter in de cache worden geplaatst wanneer de eerste keer verbinding wordt gemaakt. Organisaties moeten bij het implementeren van deze instelling overwegen wat de juiste balans is tussen bruikbaarheidsscenario's en de behoeften aan gegevensbescherming. |
| Werkprofielinstellingen | Schermopname | Blokkeren ||
| Werkprofielinstellingen | Beller-id van zakelijk contactpersoon weergeven in persoonlijk profiel | Niet geconfigureerd ||
| Werkprofielinstellingen | Werkcontacten zoeken in persoonlijk profiel | Niet geconfigureerd | Gebruikers vanuit hun persoonlijke profiel de toegang blokkeren tot zakelijke contactpersonen kan impact hebben op bepaalde bruikbaarheidsscenario´s, zoals sms'en en bellen vanuit het persoonlijke profiel. Organisaties moeten bij het implementeren van deze instelling overwegen wat de juiste balans is tussen bruikbaarheidsscenario's en de behoeften aan gegevensbescherming. |
| Werkprofielinstellingen | Camera | Niet geconfigureerd ||
| Werkprofielinstellingen | Widgets van apps in het werkprofiel toestaan | Inschakelen ||
| Werkprofielinstellingen | Werkprofielwachtwoord vereisen | Vereist ||
| Werkprofielinstellingen | Minimale wachtwoordlengte | 6 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Werkprofielinstellingen | Maximum aantal minuten van inactiviteit voordat het werkprofiel wordt vergrendeld| 5 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Werkprofielinstellingen | Aantal mislukte aanmeldingen voordat het werkprofiel wordt gewist| 10 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Werkprofielinstellingen | Wachtwoordverlooptijd (dagen) | Niet geconfigureerd | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Werkprofielinstellingen | Vereist wachtwoordtype | Complex numeriek ||
| Werkprofielinstellingen | Wachtwoorden niet opnieuw gebruiken | Niet geconfigureerd | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid.|
| Werkprofielinstellingen | Ontgrendelen met vingerafdruk | Niet geconfigureerd ||
| Werkprofielinstellingen | Smart Lock en andere trustagenten | Niet geconfigureerd |||
| Wachtwoord van apparaat | Minimale wachtwoordlengte | 6 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Wachtwoord van apparaat | Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld | 5 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Wachtwoord van apparaat | Aantal mislukte aanmeldingen voordat een apparaat wordt gewist | 10 | Met deze instelling wordt het wissen van een werkprofiel geactiveerd, en niet het wissen van een apparaat. |
| Wachtwoord van apparaat | Wachtwoordverlooptijd (dagen) | Niet geconfigureerd | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Wachtwoord van apparaat | Vereist wachtwoordtype | Complex numeriek ||
| Wachtwoord van apparaat | Wachtwoorden niet opnieuw gebruiken | Niet geconfigureerd | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Wachtwoord van apparaat | Ontgrendelen met vingerafdruk | Niet geconfigureerd ||
| Wachtwoord van apparaat | Smart Lock en andere trustagenten | Niet geconfigureerd ||
| Systeembeveiliging | Bedreigingsscan voor apps | Vereist | Deze instelling zorgt ervoor dat de scanfunctie voor Apps controleren van Google wordt ingeschakeld voor apparaten van eindgebruikers. Als deze instelling is geconfigureerd, wordt de toegang geblokkeerd voor de eindgebruiker zolang deze de scanfunctie van Google voor apps niet inschakelt op het Android-apparaat. |
| Systeembeveiliging | Voorkomen dat apps uit onbekende bronnen worden geïnstalleerd in het persoonlijke profiel | Blokkeren ||

> [!Note]
> Wanneer Android Enterprise-werkprofiel is ingeschakeld, is standaard Eén vergrendeling geconfigureerd om de wachtwoordcodes voor het apparaat en het werkprofiel te combineren. Eén vergrendeling kan worden uitgeschakeld om de wachtwoordcodes voor het werkprofiel en apparaat, indien nodig, te scheiden onder de werkprofielinstellingen.

## <a name="work-profile-high-security"></a>Werkprofiel: hoge beveiliging

Niveau 3 is de aanbevolen configuratie voor apparaten die worden gebruikt door gebruikers of groepen die een uniek hoog risico lopen. Bijvoorbeeld, gebruikers die zeer gevoelige gegevens verwerken, waarbij niet-geautoriseerde openbaarmaking een aanzienlijk verlies van materiaal veroorzaakt. Een organisatie die veel kans loopt het doelwit te zijn van goed gefinancierde en geavanceerde indringers, kan voordeel ondervinden van de extra beperkingen die hieronder worden beschreven. Deze configuratie is een uitbreiding van de configuratie in niveau 1:
- Het bevat de implementatie van Mobile Threat Defense of Microsoft Defender ATP.
- Gegevensscenario's voor werkprofielen zijn beperkt.
- Er is beleid voor sterkere wachtwoorden vereist.

De beleidsinstellingen die worden afgedwongen op niveau 3 omvatten alle aanbevolen beleidsinstellingen van niveau 1. De hieronder vermelde instellingen omvatten echter alleen de instellingen die zijn toegevoegd of gewijzigd. Deze instellingen hebben mogelijk iets meer impact voor gebruikers of toepassingen. Op basis ervan wordt een beveiligingsniveau afgedwongen dat geschikter is voor gebruikers die risico lopen, met toegang tot gevoelige informatie op mobiele apparaten.

### <a name="device-compliance"></a>Apparaatcompatibiliteit

| Sectie | Instelling | Waarde | Opmerkingen |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Vereisen dat het apparaat de risicoscore voor computers niet overschrijdt | Veilig | Voor deze instelling is Microsoft Defender ATP vereist. Zie [Naleving voor Microsoft Defender ATP met voorwaardelijke toegang in Intune afdwingen](../protect/advanced-threat-protection.md) voor meer informatie.<p>Klanten moeten overwegen Microsoft Defender ATP of een Mobile Threat Defense-oplossing te implementeren. Het is niet nodig om beide te implementeren. |
| Apparaatstatus | Vereisen dat het apparaat zich op of onder het apparaatdreigingsniveau bevindt | Beveiligd | Deze instelling vereist een Mobile Threat Defense-product. Zie [Mobile Threat Defense voor ingeschreven apparaten](../protect/mtd-device-compliance-policy-create.md) voor meer informatie.<p>Klanten moeten overwegen Microsoft Defender ATP of een Mobile Threat Defense-oplossing te implementeren. Het is niet nodig om beide te implementeren.|
| Apparaateigenschappen | Minimale versie van het besturingssysteem | Indeling: Major.Minor<br>Voorbeeld: 8.0| Microsoft raadt aan de minimale primaire versie van Android te configureren, zodat deze overeenkomt met de ondersteunde Android-versies voor Microsoft-apps. OEM's en apparaten die voldoen aan de aanbevolen Android Enterprise-vereisten, moeten ondersteuning bieden voor de release die nu wordt vrijgegeven + upgrade van één letter. Op dit moment wordt Android 8.0 of hoger door Android aangeraden voor kennismedewerkers. Zie Aanbevolen Android Enterprise-vereisten voor de nieuwste aanbevelingen van Android |
| Systeembeveiliging | Het aantal dagen totdat het wachtwoord verloopt | 365 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Systeembeveiliging | Aantal eerdere wachtwoorden dat niet mag worden gebruikt | 5 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |


### <a name="device-restrictions"></a>Apparaatbeperkingen

| Sectie | Instelling | Waarde | Opmerkingen |
| ----- | ----- | ----- | ----- |
| Werkprofielinstellingen | Werkprofielmeldingen terwijl het apparaat is vergrendeld | Blokkeren | Als u deze instelling blokkeert, zijn gevoelige gegevens niet beschikbaar in werkprofielmeldingen, wat de bruikbaarheid kan beïnvloeden. |
| Werkprofielinstellingen | Contactpersoon delen via Bluetooth | Niet geconfigureerd | Toegang tot zakelijke contactpersonen is standaard niet beschikbaar op andere apparaten, zoals auto's via Bluetooth-integratie. Het inschakelen van deze instelling verbetert de handsfree-gebruikerservaring. De contactpersonen kunnen via het Bluetooth-apparaat echter in de cache worden geplaatst wanneer de eerste keer verbinding wordt gemaakt. Organisaties moeten bij het implementeren van deze instelling overwegen wat de juiste balans is tussen bruikbaarheidsscenario's en de behoeften aan gegevensbescherming. |
| Werkprofielinstellingen | Werkcontacten zoeken in persoonlijk profiel | Blokkeren | Gebruikers vanuit hun persoonlijke profiel de toegang blokkeren tot zakelijke contactpersonen kan impact hebben op bepaalde bruikbaarheidsscenario's, zoals sms'en en bellen vanuit het persoonlijke profiel. Organisaties moeten bij het implementeren van deze instelling overwegen wat de juiste balans is tussen bruikbaarheidsscenario's en de behoeften aan gegevensbescherming. |
| Werkprofielinstellingen | Widgets van apps in het werkprofiel toestaan | Niet geconfigureerd ||
| Werkprofielinstellingen | Aantal mislukte aanmeldingen voordat het werkprofiel wordt gewist | 5 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Werkprofielinstellingen | Wachtwoordverlooptijd (dagen) | 365 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Werkprofielinstellingen | Wachtwoorden niet opnieuw gebruiken | 5 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Werkprofielinstellingen | Smart Lock en andere trustagenten | Blokkeren ||
| Wachtwoord van apparaat | Aantal mislukte aanmeldingen voordat een apparaat wordt gewist | 5 | Met deze instelling wordt het wissen van een werkprofiel geactiveerd, en niet het wissen van een apparaat. |
| Wachtwoord van apparaat | Wachtwoordverlooptijd (dagen) | 365 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Wachtwoord van apparaat | Wachtwoorden niet opnieuw gebruiken | 5 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |

## <a name="next-steps"></a>Volgende stappen

Beheerders kunnen de bovenstaande configuratieniveaus opnemen in hun ringimplementatiemethode voor test- en productiegebruik door de voorbeeld-[JSON-sjablonen voor het configuratieframework van Intune-app-beveiligingsbeleid](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) met [PowerShell-scripts](https://github.com/microsoftgraph/powershell-intune-samples) te importeren.

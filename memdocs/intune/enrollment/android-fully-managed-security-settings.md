---
title: Volledig beheerde configuraties voor Android Enterprise-beveiliging
titleSuffix: Microsoft Intune
description: 'Krijg meer informatie over voorgestelde instellingen voor volledig beheerde Android Enterprise-beveiliging: standaard, uitgebreid en hoog.'
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
ms.openlocfilehash: 99b17cc165fc8d24fdf1b0f48525f3b23d8cc9b7
ms.sourcegitcommit: d647eefa23c8849f49584442df568284d51d7525
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/09/2020
ms.locfileid: "86195630"
---
# <a name="android-enterprise-fully-managed-security-configurations"></a>Volledig beheerde configuraties voor Android Enterprise-beveiliging

Als onderdeel van het [configuratieframework voor beveiliging van Android Enterprise](android-configuration-framework.md) past u de volgende instellingen toe voor gebruikers van volledig beheerde mobiele Android Enterprise-apparaten. Zie [Instellingen voor Android Enterprise-apparaateigenaren om apparaten te markeren als niet compatibel met behulp van Intune](../protect/compliance-policy-create-android-for-work.md#device-owner) en [Android Enterprise-apparaatinstellingen voor het toestaan of beperken van functies met behulp van Intune](../configuration/device-restrictions-android-for-work.md#device-owner-only) voor meer informatie over elke beleidsinstelling.

Wanneer u de instellingen kiest, moet u gebruiksscenario's controleren en categoriseren. Configureer vervolgens gebruikers volgens de richtlijnen voor het gekozen beveiligingsniveau. U kunt de voorgestelde instellingen aanpassen op basis van de behoeften van uw organisatie. Zorg ervoor dat uw beveiligingsteam de dreigingsomgeving, risicobereidheid en impact op de bruikbaarheid evalueert.

Voor volledig beheerde apparaten in bedrijfseigendom, zijn er drie aanbevolen configuratieframeworks voor beveiliging:

- [Volledig beheerd: standaardbeveiliging (niveau 1)](#fully-managed-basic-security) 
- [Volledig beheerd: uitgebreide beveiliging (niveau 2)](#fully-managed-enhanced-security)
- [Volledig beheerde: hoge beveiliging (niveau 3)](#fully-managed-high-security) 

## <a name="fully-managed-basic-security"></a>Volledig beheerd: standaardbeveiliging

Niveau 1 is de aanbevolen minimale beveiligingsconfiguratie voor mobiele apparaten die eigendom zijn van de organisatie.

Het beleid in niveau 1 dwingt een redelijk toegangsniveau voor gegevens af, waarbij de gevolgen voor gebruikers minimaal blijft. Dit wordt gedaan door wachtwoordbeleid, een minimumversie voor het besturingssysteem, en SafetyNet-apparaatattestation af te dwingen, en bepaalde apparaatfuncties uit te schakelen (zoals USB-bestandsoverdrachten). 

### <a name="device-compliance"></a>Apparaatcompatibiliteit

| Sectie | Instelling | Waarde | Opmerkingen |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Vereisen dat het apparaat de risicoscore voor computers niet overschrijdt | Niet geconfigureerd ||
| Apparaatstatus | Vereisen dat het apparaat zich op of onder het apparaatdreigingsniveau bevindt | Niet geconfigureerd||
| Apparaatstatus | SafetyNet-apparaatattestation | Basisintegriteit en gecertificeerde apparaten controleren | Met deze instelling wordt SafetyNet-attestation van Google geconfigureerd op de apparaten van eindgebruikers. Met basisintegriteit wordt de integriteit van het apparaat gevalideerd. Geroote apparaten, emulators, virtuele apparaten en apparaten met zichtbare sabotagesporen voldoen niet aan de basisintegriteit.<br>Met basisintegriteit en gecertificeerde apparaten worden de compatibiliteit van het apparaat met services van Google gevalideerd. Alleen niet-aangepaste apparaten die door Google zijn gecertificeerd, voldoen aan deze controle. |
| Apparaateigenschappen | Minimale versie van het besturingssysteem | Indeling: Major.Minor<br>Voorbeeld: 8.0| Microsoft raadt aan de minimale primaire versie van Android te configureren, zodat deze overeenkomt met de ondersteunde Android-versies voor Microsoft-apps. OEM's en apparaten die voldoen aan de aanbevolen Android Enterprise-vereisten, moeten ondersteuning bieden voor de release die nu wordt vrijgegeven + upgrade van één letter. Op dit moment wordt Android 8.0 of hoger door Android aangeraden voor kennismedewerkers. Zie [Aanbevolen Android Enterprise-vereisten](https://www.android.com/enterprise/recommended/requirements/) voor de nieuwste aanbevelingen van Android. |
| Apparaateigenschappen | Maximale versie van het besturingssysteem | Niet geconfigureerd ||
| Apparaateigenschappen | Minimaal beveiligingspatchniveau | Niet geconfigureerd | Android-apparaten kunnen maandelijkse beveiligingspatches ontvangen, maar de release is afhankelijk van OEM's en/of providers. Organisaties moeten ervoor zorgen dat geïmplementeerde Android-apparaten beveiligingspatches ontvangen voordat deze instelling wordt geïmplementeerd. Zie [Android-beveiligingsbulletins](https://source.android.com/security/bulletin/) voor de nieuwste patchreleases. |
| Systeembeveiliging | Wachtwoord vereist voor het ontgrendelen van mobiele apparaten | Vereist ||
| Systeembeveiliging | Vereist wachtwoordtype | Complex numeriek | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Systeembeveiliging | Minimale wachtwoordlengte | 6 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Systeembeveiliging | Maximumaantal minuten inactief voordat wachtwoord is vereist| 5 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid.|
| Systeembeveiliging | Het aantal dagen totdat het wachtwoord verloopt| Niet geconfigureerd ||
| Systeembeveiliging |    Het vereiste aantal wachtwoorden voordat de gebruiker een wachtwoord opnieuw kan gebruiken | Niet geconfigureerd ||
| Systeembeveiliging | Versleuteling van gegevensopslag op apparaat | Vereist ||
| Acties voor niet-nageleefd | Het apparaat markeren als niet-compatibel | Onmiddellijk | Het beleid is standaard zo geconfigureerd dat het apparaat wordt gemarkeerd als niet-compatibel. Er zijn aanvullende acties beschikbaar. Zie [Acties configureren voor niet-compatibele apparaten in Intune](../protect/actions-for-noncompliance.md) voor meer informatie.|

### <a name="device-restrictions"></a>Apparaatbeperkingen

| Sectie | Instelling | Waarde | Opmerkingen |
| ----- | ----- | ----- | ----- |
| Algemeen | Schermopname | Niet geconfigureerd ||
| Algemeen | Camera | Niet geconfigureerd ||
| Algemeen | Standaardmachtigingsbeleid | Standaardwaarde apparaat ||
| Algemeen | Wijzigingen in datum en tijd | Niet geconfigureerd ||
| Algemeen | Volumewijzigingen | Niet geconfigureerd ||
| Algemeen | Fabrieksinstellingen terugzetten | Blokkeren ||
| Algemeen | Opstarten in veilige modus | Blokkeren ||
| Algemeen | Statusbalk | Niet geconfigureerd ||
| Algemeen | Roaming gegevensservices | Niet geconfigureerd ||
| Algemeen | Wijzigingen in Wi-Fi-instellingen | Niet geconfigureerd ||
| Algemeen | Bluetooth-configuratie | Niet geconfigureerd ||
| Algemeen | Tethering en toegang tot hotspots | Niet geconfigureerd ||
| Algemeen | USB-opslag | Niet geconfigureerd ||
| Algemeen | USB-bestandsoverdracht | Blokkeren ||
| Algemeen | Externe media | Blokkeren ||
| Algemeen | Gegevens beamen met NFC | Niet geconfigureerd ||
| Algemeen | Foutopsporingsfuncties | Niet geconfigureerd ||
| Algemeen | Microfoon aanpassen | Niet geconfigureerd ||
| Algemeen | E-mailadressen resetbeveiliging fabrieksinstellingen | Niet geconfigureerd ||
| Algemeen | Netwerknooduitgang | Niet geconfigureerd ||
| Algemeen | Systeemupdate | Automatisch ||
| Algemeen | Meldingsvensters | Niet geconfigureerd ||
| Algemeen | Hints voor eerste gebruik overslaan | Niet geconfigureerd ||
| Systeembeveiliging | Bedreigingsscan voor apps |Vereist ||
| Apparaatervaring | Type inschrijvingsprofiel | Volledig beheerd ||
| Apparaatervaring | Microsoft Launcher instellen als standaardstartprogramma | Niet geconfigureerd | Organisaties kunnen ervoor kiezen om Microsoft Launcher te implementeren, om te zorgen voor een consistente ervaring met het startscherm op volledig beheerde apparaten. Raadpleeg [Microsoft Launcher installeren op volledig beheerde Android Enterprise-apparaten met Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134) voor meer informatie |
| Wachtwoord | Vergrendelingsscherm uitschakelen | Niet geconfigureerd ||
| Wachtwoord | Uitgeschakelde functies van het vergrendelingsscherm | 0 geselecteerd ||
| Wachtwoord | Vereist wachtwoordtype | Complex numeriek ||
| Wachtwoord | Minimale wachtwoordlengte | 6 ||
| Wachtwoord | Het aantal dagen totdat het wachtwoord verloopt | Niet geconfigureerd ||
| Wachtwoord | Het vereiste aantal wachtwoorden voordat de gebruiker een wachtwoord opnieuw kan gebruiken | Niet geconfigureerd ||
| Wachtwoord | Aantal mislukte aanmeldingen voordat een apparaat wordt gewist | 10 ||
| Energie-instellingen | Tijd tot het scherm wordt vergrendeld | 5 ||
| Energie-instellingen | Scherm aan terwijl het apparaat is aangesloten | Niet geconfigureerd ||
| Gebruikers en accounts | Nieuwe gebruikers toevoegen | Niet geconfigureerd ||
| Gebruikers en accounts | Gebruiker verwijderen | Niet geconfigureerd ||
| Gebruikers en accounts | Accountwijzigingen (alleen toegewezen apparaten) | Niet geconfigureerd ||
| Gebruikers en accounts | Persoonlijke Google-accounts | Niet geconfigureerd ||
| Gebruikers en accounts | Gebruiker kan referenties configureren | Blokkeren ||
| Toepassingen | Installatie vanuit onbekende bronnen toestaan | Niet geconfigureerd ||
| Toepassingen | Toegang tot alle apps in Google Play Store toestaan | Niet geconfigureerd | Gebruikers kunnen standaard geen persoonlijke apps installeren op volledig beheerde apparaten vanuit de Google Play Store. Als organisaties willen toestaan dat volledig beheerde apparaten worden aangewend voor persoonlijk gebruik, kunt u deze instelling wijzigen. |
| Toepassingen | App wordt automatisch bijgewerkt | Alleen Wi-Fi | Organisaties moeten deze instelling zo nodig aanpassen, omdat er kosten voor data-abonnementen in rekening kunnen worden gebracht als app-updates via het mobiele netwerk worden uitgevoerd. |

## <a name="fully-managed-enhanced-security"></a>Volledig beheerd: uitgebreide beveiliging

Niveau 2 is de aanbevolen configuratie voor apparaten waarbij gebruikers toegang hebben tot meer gevoelige informatie. Deze apparaten zijn tegenwoordig vaak het doelwit in ondernemingen. Voor deze instellingen wordt niet uitgegaan van een groot personeelsbestand of zeer ervaren beveiligingspersoneel. Daarom zijn ze toegankelijk voor de meeste ondernemingen. Deze configuratie is een uitbreiding van de configuratie van niveau 1, door beleid voor sterkere wachtwoorden te vereisen, en mogelijkheden voor gebruikers/accounts uit te schakelen.

De instellingen van niveau 2 omvatten alle aanbevolen beleidsinstellingen van niveau 1. De hieronder vermelde instellingen omvatten echter alleen de instellingen die zijn toegevoegd of gewijzigd. Deze instellingen hebben mogelijk iets meer impact voor gebruikers of toepassingen. Op basis ervan wordt een beveiligingsniveau afgedwongen dat geschikter is voor gebruikers die risico lopen, met toegang tot gevoelige informatie op mobiele apparaten.

### <a name="device-compliance"></a>Apparaatcompatibiliteit

| Sectie | Instelling | Waarde | Opmerkingen |
| ----- | ----- | ----- | ----- |
| Systeembeveiliging | Het aantal dagen totdat het wachtwoord verloopt | 365 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Systeembeveiliging |    Het vereiste aantal wachtwoorden voordat de gebruiker een wachtwoord opnieuw kan gebruiken | 5 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |

### <a name="device-restrictions"></a>Apparaatbeperkingen

| Sectie | Instelling | Waarde | Opmerkingen |
| ----- | ----- | ----- | ----- |
| Algemeen | E-mailadressen resetbeveiliging fabrieksinstellingen | E-mailadressen Google-account ||
| Algemeen | Lijst met e-mailadressen (alleen optie E-mailadressen Google-account) | example@gmail.com | Werk dit beleid handmatig bij om de Google-e-mailadressen op te geven van apparaatbeheerders die de apparaten kunnen ontgrendelen nadat ze zijn gewist. |
| Wachtwoord van apparaat | Het aantal dagen totdat het wachtwoord verloopt | 365 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Wachtwoord van apparaat | Het vereiste aantal wachtwoorden voordat de gebruiker een wachtwoord opnieuw kan gebruiken | 5 | Organisaties moeten deze instelling mogelijk bijwerken, zodat deze overeenkomt met het wachtwoordbeleid. |
| Wachtwoord van apparaat | Aantal mislukte aanmeldingen voordat een apparaat wordt gewist | 5 ||
| Gebruikers en accounts | Nieuwe gebruikers toevoegen | Blokkeren ||
| Gebruikers en accounts | Gebruiker verwijderen | Blokkeren ||
| Gebruikers en accounts | Persoonlijke Google-accounts | Blokkeren ||

## <a name="fully-managed-high-security"></a>Volledig beheerd: hoge beveiliging

Niveau 3 is de aanbevolen configuratie voor:
- Organisaties met grote en geavanceerde beveiligingsorganisaties.
- Specifieke gebruikers en groepen die een uniek doelwit zijn voor indringers.
Dergelijke organisaties zijn doorgaans gericht op goed gefinancierde en geavanceerde indringers. Daarom ondervinden zij voordeel van de extra beperkingen en besturingselementen die hieronder worden vermeld.

Deze configuratie is een uitbreiding van niveau 2:
- De minimumversie van het besturingssysteem is hoger.
- Er wordt gezorgd dat apparaten compatibel zijn door het veiligste Microsoft Defender ATP-niveau of Mobile Threat Defense-niveau af te dwingen.
- De minimumversie van het besturingssysteem is hoger.
- Er worden aanvullende apparaatbeperkingen afgedwongen (zoals het uitschakelen van niet-geredigeerde meldingen op het vergrendelingsscherm).
- Apps moeten altijd up-to-date zijn. 

De beleidsinstellingen die worden afgedwongen op niveau 3 omvatten alle aanbevolen beleidsinstellingen van niveau 2. De hieronder vermelde instellingen omvatten alleen de instellingen die zijn toegevoegd of gewijzigd. Deze instellingen kunnen een aanzienlijke impact hebben voor gebruikers of toepassingen. Op basis ervan wordt een beveiligingsniveau afgedwongen dat geschikter is voor organisaties die risico lopen.


### <a name="device-compliance"></a>Apparaatcompatibiliteit

| Sectie | Instelling | Waarde | Opmerkingen |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Vereisen dat het apparaat de risicoscore voor computers niet overschrijdt | Veilig | Voor deze instelling is Microsoft Defender ATP vereist. Zie [Naleving voor Microsoft Defender ATP met voorwaardelijke toegang in Intune afdwingen](../protect/advanced-threat-protection.md) voor meer informatie.<p> Klanten moeten overwegen Microsoft Defender ATP of een Mobile Threat Defense-oplossing te implementeren. Het is niet nodig om beide te implementeren. |
| Apparaatstatus | Vereisen dat het apparaat zich op of onder het apparaatdreigingsniveau bevindt | Beveiligd | Deze instelling vereist een Mobile Threat Defense-product. Zie [Mobile Threat Defense voor ingeschreven apparaten](../protect/mtd-device-compliance-policy-create.md) voor meer informatie.<p>Klanten moeten overwegen Microsoft Defender ATP of een Mobile Threat Defense-oplossing te implementeren. Het is niet nodig om beide te implementeren.|
| Apparaateigenschappen | Minimale versie van het besturingssysteem | Indeling: Major.Minor<br>Voorbeeld: 10.0| Microsoft raadt aan de minimale primaire versie van Android te configureren, zodat deze overeenkomt met de ondersteunde Android-versies voor Microsoft-apps. OEM's en apparaten die voldoen aan de aanbevolen Android Enterprise-vereisten, moeten ondersteuning bieden voor de release die nu wordt vrijgegeven + upgrade van één letter. Op dit moment wordt Android 8.0 of hoger door Android aangeraden voor kennismedewerkers. Zie Aanbevolen Android Enterprise-vereisten voor de nieuwste aanbevelingen van Android |

### <a name="device-restrictions"></a>Apparaatbeperkingen

| Sectie | Instelling | Waarde | Opmerkingen |
| ----- | ----- | ----- | ----- |
| Algemeen | Wijzigingen in datum en tijd | Blokkeren ||
| Algemeen | Tethering en toegang tot hotspots | Blokkeren ||
| Algemeen | Gegevens beamen met NFC | Blokkeren ||
| Wachtwoord van apparaat | Uitgeschakelde functies van het vergrendelingsscherm | Trustagenten, niet-geredigeerde meldingen ||
| Toepassingen | App wordt automatisch bijgewerkt | Altijd | Organisaties moeten deze instelling zo nodig aanpassen, omdat er kosten voor data-abonnementen in rekening kunnen worden gebracht als app-updates via het mobiele netwerk worden uitgevoerd. |


## <a name="next-steps"></a>Volgende stappen

Beheerders kunnen de bovenstaande configuratieniveaus opnemen in hun ringimplementatiemethode voor test- en productiegebruik door de voorbeeld-[JSON-sjablonen voor het configuratieframework van Intune-app-beveiligingsbeleid](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) met [PowerShell-scripts](https://github.com/microsoftgraph/powershell-intune-samples) te importeren.

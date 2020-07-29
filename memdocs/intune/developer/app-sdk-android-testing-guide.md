---
title: Testhandleiding voor ontwikkelaars voor Microsoft Intune App SDK voor Android
description: Met de testhandleiding voor de Intune App-SDK voor Android kunt u uw door Intune beheerde Android-app testen.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4ef8f421-9610-4d34-a464-cc02eb1578a9
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: b47361bf4812de91d12c779a6eb58fef35e9d0f2
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262044"
---
# <a name="microsoft-intune-app-sdk-for-android-developers-testing-guide"></a>Testhandleiding voor ontwikkelaars voor Microsoft Intune App SDK voor Android

De testhandleiding voor de Intune App-SDK voor Android is ontworpen om uw door Intune beheerde Android-app testen.

## <a name="demo-tenant-setup"></a>Demotenant installeren
Als uw bedrijf nog niet over een tenant beschikt, kunt u een demotenant met of zonder vooraf gegenereerde gegevens maken. U moet zich registreren als [Microsoft-partner](https://partner.microsoft.com/business-opportunities/why-microsoft) om toegang te krijgen tot Microsoft CDX. Een nieuw account maken:
1. Ga naar de [Microsoft CDX-website voor het maken van tenants](https://cdx.transform.microsoft.com/my-tenants/create-tenant) en maak een Microsoft 365 Enterprise-tenant.
2. [Stel Intune in](../fundamentals/setup-steps.md) om Mobile Device Management (MDM) in te schakelen.
3. [Gebruikers maken](../fundamentals/users-add.md).
4. [Groepen maken](../fundamentals/groups-add.md).
5. [Licenties toewijzen](../fundamentals/licenses-assign.md) die geschikt zijn voor het testen.


## <a name="azure-portal-policy-configuration"></a>Beleidsconfiguratie Azure Portal
[Maak beveiligingsbeleid voor apps en wijs dit toe](../apps/app-protection-policies.md) in de [Intune-blade van Azure Portal](https://portal.azure.com/?feature.customportal=false#blade/Microsoft_Intune_Apps/MainMenu/14/selectedMenuItem/Overview). U kunt uw [app-configuratiebeleid](../apps/app-configuration-policies-overview.md) ook maken en toewijzen in de Intune-blade.

> [!NOTE]
> Als uw app niet wordt vermeld in Azure Portal, kunt u een beleid hier alsnog op richten door het selecteren van de optie **Meer apps** en het opgeven van de naam van het pakket in het tekstvak.

## <a name="test-cases"></a>Testcases

De volgende testcases bieden configuratie- en bevestigingsstappen. Gebruik deze tests om uw nieuwe, geïntegreerde Android-app te verifiëren.

### <a name="required-pin-and-corporate-credentials"></a>Vereiste pincode en zakelijke referenties

U kunt een pincode vereisen voor toegang tot bedrijfsresources. U kunt ook een zakelijke verificatie afdwingen voordat gebruikers de beheerde apps kunnen gebruiken. Dit werkt als volgt:

1. Stel **Pincode vereisen voor toegang** en **Zakelijke referenties vereisen voor toegang** in op **Ja**. Zie [Instellingen beveiligingsbeleid voor Android-apps in Microsoft Intune](../apps/app-protection-policy-settings-android.md#access-requirements) voor meer informatie.
2. Bevestig de volgende voorwaarden:
    - Bij het starten van de app dient een prompt voor het invoeren van de pincode of de productiegebruiker die is gebruikt tijdens de inschrijving bij de bedrijfsportal te worden weergegeven.
    - Wanneer er geen geldige aanmeldingsprompt wordt weergegeven, kan dit zijn veroorzaakt door een onjuist geconfigureerd Android-manifest, in het bijzonder de waarden voor de integratie van ADAL (Azure Active Directory Authentication Library) (SkipBroker, ClientID en Authority).
    - Wanneer er geen prompt wordt weergegeven, wordt dit mogelijk veroorzaakt door een onjuist geïntegreerde `MAMActivity`-waarde. Zie de [ontwikkelaarshandleiding voor de Microsoft Intune App-SDK voor Android](app-sdk-android.md) voor meer informatie over `MAMActivity`.

> [!NOTE] 
> Als de voorgaande test niet werkt, zullen de volgende tests waarschijnlijk ook mislukken. Controleer de integratie van de [SDK](app-sdk-android.md#sdk-integration) en [ADAL](app-sdk-android.md#configure-azure-active-directory-authentication-library-adal).

### <a name="restrict-transferring-and-receiving-data-with-other-apps"></a>Overdracht en ontvangst van gegevens ten aanzien van andere apps beperken
U kunt de gegevensoverdracht tussen door het bedrijf beheerde toepassingen als volgt regelen:

1. Stel **Apps toestaan om gegevens over te dragen aan andere apps** in op **Door beleid beheerde apps**.
2. Stel **App mag gegevens ontvangen van andere apps** in op **Alle apps**. 

Het gebruik van intenties en inhoudsproviders wordt beïnvloed door dit beleid.
3. Bevestig de volgende voorwaarden:
    - Het in uw app openen van gegevens uit een niet-beheerde app werkt correct.
    - Het delen van inhoud tussen uw app en beheerde apps is toegestaan.
    - Delen van uw app op niet-beheerde apps (bijvoorbeeld Chrome) is geblokkeerd.


#### <a name="restrict-receiving-data-from-other-apps"></a>De ontvangst van gegevens van andere apps beperken

1. Stel de optie **Organisatiegegevens naar andere apps verzenden** in op **Alle apps**.
2. Stel de optie **Gegevens ontvangen van andere apps** in op **Door beleid beheerde apps**. 
3. Bevestig de volgende voorwaarden:
    - Het naar een onbeheerde app verzenden vanuit uw app werkt correct.
    - Het delen van inhoud tussen uw app en beheerde apps is toegestaan.
    - Delen vanuit niet-beheerde apps (bijvoorbeeld Chrome) met uw app is geblokkeerd.

Als v oor uw app [geïntegreerde Openen vanaf-besturingselementen](app-sdk-android.md#opening-data-from-a-local-or-cloud-storage-location) vereist zijn, kunt u de functionaliteit voor **Openen vanaf** als volgt beheren:

1. Stel de optie **Gegevens ontvangen van andere apps** in op **Door beleid beheerde apps**. 
2. Stel **Gegevens openen in organisatiedocumenten** in op **Blokkeren**. 
3. Bevestig de volgende voorwaarden:
    - Openen is beperkt tot alleen geschikte, beheerde locaties.

### <a name="restrict-cut-copy-and-paste"></a>Knippen, kopiëren en plakken beperken
U kunt het systeemklembord als volgt beperken tot beheerde toepassingen:

1. Stel **Knippen, kopiëren en plakken met andere apps beperken** in op **Door beleid beheerde apps met Plakken in**.
2. Bevestig de volgende voorwaarden:
    - Tekst kopiëren van uw app naar een niet-beheerde app (bijvoorbeeld Berichten) is geblokkeerd.

### <a name="prevent-save"></a>Opslaan voorkomen
Als voor uw app [geïntegreerde Opslaan als-besturingselementen](app-sdk-android.md#example-data-transfer-between-apps-and-device-or-cloud-storage-locations) vereist zijn, kunt u de functionaliteit voor **Opslaan als** als volgt beheren:

1. Stel **Opslaan als voorkomen** in op **Ja**.
2. Bevestig de volgende voorwaarden:
    - Opslaan is beperkt tot alleen geschikte, beheerde locaties.

### <a name="file-encryption"></a>Bestandsversleuteling
U kunt gegevens op het apparaat als volgt versleutelen:

1. Stel **App-gegevens versleutelen** in op **Ja**.
2. Bevestig de volgende voorwaarden:
    - Normaal toepassingsgedrag wordt niet beïnvloed.

### <a name="prevent-android-backups"></a>Back-ups van Android voorkomen
U kunt als volgt back-ups van apps regelen:

1. Als u [Geïntegreerde back-upbeperkingen](app-sdk-android.md#protecting-backup-data) hebt ingesteld, stelt u **Back-ups van Android voorkomen** in op **Ja**.
2. Bevestig de volgende voorwaarden:
    - Back-ups zijn beperkt.

### <a name="wipe"></a>Wissen
U kunt uit beheerde apps op afstand zakelijke e-mails en documenten wissen. Persoonsgegevens worden versleuteld wanneer ze niet meer worden beheerd. Dit werkt als volgt:

1. [Geef opdracht om te wissen](../apps/apps-selective-wipe.md) vanuit Azure Portal.
2. Controleer de volgende voorwaarden als uw app niet voor handlers voor wissen is geregistreerd:
    - De app wordt volledig gewist.
3. Bevestig of de volgende voorwaarden als uw app is geregistreerd voor `WIPE_USER_DATA` of `WIPE_USER_AUXILARY_DATA`:
    - De beheerde inhoud wordt verwijderd uit de app. Zie de [ontwikkelaarshandleiding voor de Microsoft Intune App-SDK voor Android - Selectief wissen](app-sdk-android.md#selective-wipe) voor meer informatie.

### <a name="multi-identity-support"></a>Ondersteuning voor meerdere identiteiten
De integratie van [ondersteuning voor meerdere identiteiten](app-sdk-android.md#multi-identity-optional) is een wijziging met een hoog risico die grondig moet worden getest. De meest voorkomende problemen treden op vanwege een onjuiste instelling van de actieve identiteit (`MAMFileProtectionManager` versus threadniveau) of het onjuist bijhouden van bestandsidentiteiten (`Context`).

Controleer minimaal het volgende:

- Het beleid voor **Opslaan als** werkt correct voor beheerde identiteiten.
- Beperkingen voor kopiëren en plakken worden correct gehandhaafd van beheerd naar persoonlijk.
- Alleen gegevens die behoren tot de beheerde identiteit worden versleuteld en persoonlijke bestanden worden niet gewijzigd.
- Met selectief wissen worden tijdens het uitschrijven van apparaten alleen gegevens van de beheerde identiteit verwijderd.
- De eindgebruiker wordt gevraagd om voorwaardelijk te starten wanneer een account wordt gewijzigd van een niet-beheerd in een beheerd account (alleen de eerste keer).

### <a name="app-configuration-optional"></a>App-configuratie (optioneel)
U kunt het gedrag van beheerde apps configureren. Als uw app de instellingen van de app-configuratie gebruikt, moet u testen of uw app alle waarden correct verwerkt die u (als beheerder) kunt instellen. U kunt [app-configuratiebeleidsregels](../apps/app-configuration-policies-overview.md) maken en toewijzen in Intune.



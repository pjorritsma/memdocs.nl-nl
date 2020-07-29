---
title: Zakelijke id’s toevoegen aan Intune
titleSuffix: ''
description: Meer informatie over het toevoegen van zakelijke id's (registratiemethode, IMEI en serienummers) aan Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 566ed16d-8030-42ee-bac9-5f8252a83012
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b9796df0da4974b860348bf52ef06db202219136
ms.sourcegitcommit: cb9b452f8e566fe026717b59c142b65f426e5033
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/20/2020
ms.locfileid: "86491113"
---
# <a name="identify-devices-as-corporate-owned"></a>Apparaten identificeren als bedrijfseigendom

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Als Intune-beheerder kunt u apparaten identificeren als bedrijfseigendom om het beheer en de identificatie ervan te verfijnen. Bij apparaten in bedrijfseigendom kan Intune extra beheertaken uitvoeren en meer informatie verzamelen, zoals het volledige telefoon en een inventaris van apps. Ook kunt u ook apparaatbeperkingen instellen om inschrijving door apparaten die geen bedrijfseigendom zijn te blokkeren.

Tijdens het inschrijven wijst Intune automatisch de status Bedrijfseigendom toe aan apparaten die zijn:

- Ingeschreven met een [apparaatinschrijvingsbeheerder](device-enrollment-manager-enroll.md)-account (alle platforms)
- Ingeschreven via het Apple-[apparaatinschrijvingsprogramma](device-enrollment-program-enroll-ios.md), [Apple School Manager](apple-school-manager-set-up-ios.md) of [Apple Configurator](apple-configurator-enroll-ios.md) (alleen iOS)
- [Herkend als bedrijfseigendom voorafgaand aan inschrijving](#identify-corporate-owned-devices-with-imei-or-serial-number) met een internationaal identificatienummer voor mobiele apparaten (IMEI; alle platforms met IMEI-nummers) of een serienummer (iOS en Android)
- Deelgenomen aan Azure Active Directory met de referenties van uw werk- of school. [Apparaten die zijn geregistreerd bij Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/overview) worden gemarkeerd als persoonlijk.
- Opgegeven als Zakelijk in de [lijst Eigenschappen van het apparaat](#change-device-ownership)

Na het inschrijven kunt u [de eigendomsinstelling wijzigen](#change-device-ownership) en schakelen tussen **Persoonlijk** en **Zakelijk**.

## <a name="identify-corporate-owned-devices-with-imei-or-serial-number"></a>Herkenning van apparaten in bedrijfseigendom met IMEI-nummer of serienummer

Als Intune-beheerder kunt u een bestand met door komma's gescheiden waarden (.csv) maken en importeren, waarin de IMEI-nummers of serienummers van 14 cijfers worden vermeld. Intune gebruikt deze id's om het eigendom van het apparaat als zakelijk op te geven tijdens het inschrijven van het apparaat. Voor elk IMEI-nummer of serienummer kunnen gegevens zijn opgegeven in de lijst voor beheerdoeleinden.

Deze functie wordt ondersteund op de volgende platformen:

| Platform | IMEI-nummers | Serienummers |
|---|---|---|
| Windows | Ondersteund (Windows Phone) | Niet ondersteund |
| iOS/macOS | Niet ondersteund (Zie Belangrijk hieronder)  | Ondersteund |
| Door apparaatbeheerder beheerd Android OS V10 | Niet ondersteund | Niet ondersteund |
| Andere Android | Niet ondersteund | Ondersteund |

<!-- When you upload serial numbers for corporate-owned iOS/iPadOS devices, they must be paired with a corporate enrollment profile. Devices must then be enrolled using either Apple's Automated Device Enrollment or Apple Configurator to have them appear as corporate-owned. -->

[Lees hier meer informatie over het vinden van het serienummer van een Apple-apparaat](https://support.apple.com/HT204308).<br>
[Lees hier meer informatie over het vinden van het serienummer van een Android-apparaat](https://support.google.com/store/answer/3333000).

## <a name="add-corporate-identifiers-by-using-a-csv-file"></a>Bedrijfs-id's toevoegen met behulp van een CSV-bestand
Maak een lijst met twee kolommen met door komma's gescheiden waarden (.csv) zonder koptekst. Plaats de IMEI- of serienummers van 14 cijfers in de linkerkolom en de details in de rechterkolom. U kunt in één CSV-bestand maar één type id, IMEI-nummer of serienummer importeren. De details zijn beperkt tot 128 tekens en zijn alleen bedoeld voor beheerders. De details worden niet op het apparaat weergegeven. De huidige limiet is 5.000 rijen per CSV-bestand.

**Een CSV-bestand met serienummers uploaden**: maak een lijst in twee kolommen met door komma's gescheiden waarden (CSV) zonder koptekst. Zorg ervoor dat het CSV-bestand niet meer dan 5000 apparaten bevat en niet groter is dan 5 MB.

|||
|-|-|
|&lt;Id 1&gt;|&lt;Details apparaat 1&gt;|
|&lt;Id 2&gt;|&lt;Details apparaat 2&gt;|

Dit CSV-bestand ziet er in een teksteditor als volgt uit:

```
01234567890123,device details
02234567890123,device details
```

> [!IMPORTANT]
> Sommige Android- en iOS-/iPadOS-apparaten hebben meerdere IMEI-nummers. Intune leest maar één IMEI-nummer per ingeschreven apparaat. Als u een IMEI-nummer importeert dat niet het IMEI-nummer is dat in Intune is geïnventariseerd, wordt het apparaat geclassificeerd als een persoonlijk apparaat in plaats van een apparaat in bedrijfseigendom. Als u meerdere IMEI-nummers voor een apparaat importeert, krijgen niet-geïnventariseerde nummers de inschrijvingsstatus **Onbekend**.<br>
>Let ook hierop: Serienummers zijn de aanbevolen identificatiewijze voor iOS/iPadOS-apparaten.
>Android-serienummers zijn niet gegarandeerd uniek of aanwezig. U kunt de leverancier van uw apparaat vragen of het serienummer van uw apparaat een betrouwbare id is.
>De serienummers van het apparaat die aan Intune worden gemeld, komen mogelijk niet overeen met de id die wordt weergegeven in het menu Info of Instellingen van het apparaat. Controleer het type van het serienummer dat door de fabrikant van het apparaat wordt vermeld.
>Wanneer wordt geprobeerd een bestand te uploaden met serienummers met punten (.), mislukt de upload. Serienummers met punten worden niet ondersteund.

### <a name="upload-a-csv-list-of-corporate-identifiers"></a>Een CSV-lijst met bedrijfs id's uploaden

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431), kies **Apparaten** > **Apparaten inschrijven** > **Bedrijfsapparaat-id's** > **Toevoegen** > **CSV-bestand uploaden**.

2. Op de blade **Id's toevoegen** geeft u het id-type op: **IMEI** of **Serienummer**.

3. Klik op het mappictogram en geef het pad op naar de lijst die u wilt importeren. Navigeer naar het CSV-bestand en kies **Toevoegen**. 

4. Als het CSV-bestand bedrijfs-id's bevat die zich al in Intune bevinden, maar andere details hebben, wordt de pop-up **Dubbele id's controleren** weergegeven. Selecteer de id's die u wilt overschrijven in Intune en kies **OK** om de id's toe te voegen. Voor elke id wordt alleen de eerste kopie vergeleken.

## <a name="manually-enter-corporate-identifiers"></a>Bedrijfs-id's handmatig invoeren

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431), kies **Apparaten** > **Apparaten inschrijven** > **Bedrijfsapparaat-id's** > **Toevoegen** > **Handmatig invoeren**.

2. Op de blade **Id's toevoegen** geeft u het id-type op: **IMEI** of **Serienummer**.

3. Voer waarden voor **Id** en **Details** in voor elke id die u wilt toevoegen. Wanneer u klaar bent met het invoeren van id's, kiest u **Toevoegen**.

5. Als u bedrijfs-id's hebt ingevoerd die zich al in Intune bevinden, maar andere details hebben, wordt de pop-up **Dubbele id's controleren** weergegeven. Selecteer de id's die u wilt overschrijven in Intune en kies **OK** om de id's toe te voegen. Voor elke id wordt alleen de eerste kopie vergeleken.

Klik op **Vernieuwen** voor een overzicht van nieuwe apparaat-id's.

Geïmporteerde apparaten zijn niet noodzakelijkerwijs ingeschreven. Apparaten kunnen de status **Ingeschreven** of **Geen contact opgenomen** hebben. **Geen contact gemaakt** betekent dat het apparaat nooit gecommuniceerd heeft met de Intune-service.

## <a name="delete-corporate-identifiers"></a>Zakelijke id's verwijderen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431), kies **Apparaten** > **Apparaten inschrijven** > **Bedrijfsapparaat-id's**.
2. Selecteer de apparaat-id’s die u wilt verwijderen en kies vervolgens **Verwijderen**.
3. Bevestig de verwijdering.

Wanneer u een zakelijke id voor een ingeschreven apparaat verwijdert, wordt het eigendom van het apparaat niet gewijzigd. Als u het eigendom van een apparaat wilt wijzigen, gaat u naar **Apparaten**, selecteert u het apparaat, kiest u **Eigenschappen** en wijzigt u het **Apparaateigendom**.

## <a name="imei-specifications"></a>IMEI-specificaties
Zie [3GGPP TS 23.003](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=729) voor gedetailleerde specificaties over International Mobile Equipment Identifiers.

## <a name="change-device-ownership"></a>Apparaateigendom wijzigen

De apparaateigenschappen tonen **Eigendom** voor de records van elk apparaat in Intune. Als beheerder kunt u apparaten als **Persoonlijk** of **Zakelijk** opgeven. Wanneer het eigendomstype van een apparaat wordt gewijzigd van Zakelijk in Persoonlijk, worden alle app-gegevens die eerder van het apparaat zijn verzameld, binnen zeven dagen verwijderd door Intune. Indien van toepassing, verwijdert Intune ook het bewaarde telefoonnummer. 

**Ga als volgt te werk om het apparaateigendom te wijzigen:**
1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) kies **Apparaten** > **Alle apparaten** > kies het apparaat.
2. Kies **Eigenschappen**.
3. Selecteer voor **Apparaateigendom** de optie **Persoonlijk** of **Zakelijk**.

   ![Apparaateigenschappen die de apparaatcategorie en opties van Apparaateigendom weergeeft](./media/corporate-identifiers-add/device-properties.png)

U kunt uit het oogpunt van privacy een pushmelding configureren die naar de gebruikers van zowel de Android- als de iOS-bedrijfsportal wordt verzonden wanneer het eigendomstype voor hun apparaat is gewijzigd van **Persoonlijk** in **Zakelijk**. 

Wanneer het eigendomstype van een apparaat wordt gewijzigd van Zakelijk in Persoonlijk, worden alle app-gegevens die eerder van het apparaat zijn verzameld, binnen zeven dagen verwijderd door Intune. Indien van toepassing, verwijdert Intune ook het bewaarde telefoonnummer. Via Intune wordt nog steeds een inventaris gemaakt van de apps die door de IT-beheerder op het apparaat worden geïnstalleerd en wordt nog steeds een gedeeltelijk telefoonnummer voor het apparaat verzameld nadat het is gemarkeerd als persoonlijk.

U kunt deze instelling vinden in Microsoft Endpoint Manager door **Tenantbeheer** > **Aanpassing** te selecteren. Zie [Bedrijfsportal - Configuratie](../apps/company-portal-app.md#configuration) voor meer informatie.
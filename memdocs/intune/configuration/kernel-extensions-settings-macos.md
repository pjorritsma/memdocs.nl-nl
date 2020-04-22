---
title: macOS-kernelinstellingen in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Het toevoegen, configureren of maken van instellingen op macOS-apparaten voor het gebruik van kernelextensies. U kunt ook toestaan dat gebruikers goedgekeurde extensies overschrijven, alle extensies van een team-id toestaan of specifieke extensies of apps toestaan in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e18fad8f1112681a62bcdacd63c652cfd4ad3ac
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359290"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-extensions-in-intune"></a>instellingen voor macOS-apparaten om kernelextensies te configureren en gebruiken in Intune

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen voor kernelextensies die u kunt beheren op macOS-apparaten. Gebruik deze instellingen om kernelextensies aan uw apparaten toe te voegen en te beheren als onderdeel van uw MDM-oplossing (Mobile Device Management).

Zie [macOS-kernelextensies toevoegen](kernel-extensions-overview-macos.md) voor meer informatie over de kernelextensies in Intune en eventuele vereisten.

Deze instellingen worden toegevoegd aan een apparaatconfiguratieprofiel in Intune en vervolgens toegewezen aan of geïmplementeerd op uw macOS-apparaten.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een configuratieprofiel voor apparaatkernelextensies](kernel-extensions-overview-macos.md).

> [!NOTE]
> Deze instellingen zijn van toepassing op verschillende inschrijvingstypen. Zie [macOS-inschrijving](../enrollment/macos-enroll.md) voor meer informatie over de verschillende inschrijvingstypen.

## <a name="kernel-extensions"></a>Kernelextensies

### <a name="settings-apply-to-user-approved-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Door de gebruiker goedgekeurde, geautomatiseerde apparaatinschrijving

- **Negeren door gebruiker toestaan**: Met **toestaan** kunnen gebruikers de kernelextensies goedkeuren die niet zijn opgenomen in het configuratieprofiel. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard voorkomen dat gebruikers extensies kunnen toestaan die niet zijn opgenomen in het configuratieprofiel. Dit betekent dat alleen extensies zijn toegestaan die zijn opgenomen in het configuratieprofiel.

  Zie [user-approved kernel extension loading](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (laden van door de gebruiker goedgekeurde kernelextensies, opent de website van Apple) voor meer informatie over deze functie.

- **Toegestane team-id's**: Gebruik deze instelling om een of meer team-id's toe te staan. Alle kernelextensies die zijn ondertekend met de team-id's die u invoert, zijn toegestaan en worden vertrouwd. Met andere woorden, gebruik deze optie om alle kernelextensies binnen dezelfde team-id toe te staan. Dit kan ook een specifieke ontwikkelaar of partner zijn.

  U kunt een team-id **toevoegen** van geldige en ondertekende kernelextensies die u wilt laden. U kunt meerdere team-id's toevoegen. De team-id moet alfanumeriek zijn (letters en cijfers) en mag uit 10 tekens bestaan. Voer bijvoorbeeld `ABCDE12345` in.

  Nadat u een team-id hebt toegevoegd, kan deze ook worden verwijderd.

  Op [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Zoek uw team-id, opent de website van Apple) vindt u meer informatie.

- **Toegestane kernelextensies**: Gebruik deze instelling om specifieke kernelextensies toe te staan. Alleen de kernelextensies die u invoert, worden toegestaan of vertrouwd.

  U kunt de bundel-id en team-id **toevoegen** van een kernelextensie die u wilt laden. Voor niet-ondertekende verouderde kernelextensies gebruikt u een lege team-id. U kunt meerdere kernelextensies toevoegen. De team-id moet alfanumeriek zijn (letters en cijfers) en mag uit 10 tekens bestaan. Voer bijvoorbeeld `com.contoso.appname.macos` in voor **Bundel-id** en `ABCDE12345` voor **Team-id**.

  > [!TIP]
  > Als u de bundel-id van een kernelextensie (Kext) op een macOS-apparaat wilt ophalen, kunt u het volgende doen:
  >
  > 1. Voer `kextstat | grep -v com.apple` uit in de Terminal en noteer de uitvoer. Installeer de gewenste software of Kext. Voer `kextstat | grep -v com.apple` opnieuw uit en zoek naar wijzigingen.
  >
  >    In de Terminal bevat `kextstat` alle kernelextensies op het besturingssysteem. 
  >
  > 2. Open op het apparaat het bestand met de eigenschappenlijst van de informatie (info. plist) voor een Kext. De bundel-id wordt weergegeven. In elke Kext is een info.plist-bestand opgeslagen.

> [!NOTE]
> U hoeft geen team-id's en kernelextensies toe te voegen. U kunt de een of de andere configureren.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

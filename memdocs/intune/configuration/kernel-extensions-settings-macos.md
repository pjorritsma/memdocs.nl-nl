---
title: Instellingen voor macOS-extensies in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Het toevoegen, configureren of maken van instellingen op macOS-apparaten voor het gebruik van systeemextensies en kernelextensies. U kunt ook toestaan dat gebruikers goedgekeurde extensies overschrijven, alle extensies van een team-id toestaan of specifieke extensies of apps toestaan in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
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
ms.openlocfilehash: 8b716a7e85f817e95a9f1fec992458e052570d81
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429516"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-and-system-extensions-in-intune"></a>instellingen voor macOS-apparaten om kernel- en systeemextensies te configureren en gebruiken in Intune

> [!NOTE]
> macOS-kernel-extensies worden vervangen door systeemextensies. Voor meer informatie raadpleegt u [Ondersteuningstip: Systeemextensies in plaats van kernelextensies gebruiken voor macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen voor kernel- en systeemextensies die u kunt beheren op macOS-apparaten. Gebruik deze instellingen om extensies aan uw apparaten toe te voegen en te beheren als onderdeel van uw MDM-oplossing (Mobile Device Management).

Zie [macOS-extensies toevoegen](kernel-extensions-overview-macos.md) voor meer informatie over de extensies in Intune en eventuele vereisten.

Deze instellingen worden toegevoegd aan een apparaatconfiguratieprofiel in Intune en vervolgens toegewezen aan of geïmplementeerd op uw macOS-apparaten.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een configuratieprofiel voor macOS-extensies](kernel-extensions-overview-macos.md).

> [!NOTE]
> Deze instellingen zijn van toepassing op verschillende inschrijvingstypen. Zie [macOS-inschrijving](../enrollment/macos-enroll.md) voor meer informatie over de verschillende inschrijvingstypen.

## <a name="kernel-extensions"></a>Kernelextensies

Deze functie is van toepassing op:

- macOS 10.13.2 en hoger
- Door de gebruiker goedgekeurde apparaatinschrijving is vereist 

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Door de gebruiker goedgekeurde apparaatinschrijving, automatische apparaatregistratie

- **Negeren door gebruiker toestaan**: Met **Ja** kunnen gebruikers de kernelextensies goedkeuren die niet zijn opgenomen in het configuratieprofiel. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard voorkomen dat gebruikers extensies kunnen toestaan die niet zijn opgenomen in het configuratieprofiel. Dit betekent dat alleen extensies zijn toegestaan die zijn opgenomen in het configuratieprofiel.

  Zie [laden van door de gebruiker goedgekeurde kernelextensies](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (hiermee wordt de website van Apple geopend) voor meer informatie over deze functie.

- **Toegestane team-id's**: Gebruik deze instelling om een of meer team-id's toe te staan. Alle kernelextensies die zijn ondertekend met de team-id's die u invoert, zijn toegestaan en worden vertrouwd. Met andere woorden, gebruik deze optie om alle kernelextensies binnen dezelfde team-id toe te staan. Dit kan ook een specifieke ontwikkelaar of partner zijn.

  U kunt een team-id **toevoegen** van geldige en ondertekende kernelextensies die u wilt laden. U kunt meerdere team-id's toevoegen. De team-id moet alfanumeriek zijn (letters en cijfers) en mag uit 10 tekens bestaan. Voer bijvoorbeeld `ABCDE12345` in.

  Nadat u een team-id hebt toegevoegd, kan deze ook worden verwijderd.

  Op [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Zoek uw team-id, opent de website van Apple) vindt u meer informatie.

- **Toegestane kernelextensies**: Gebruik deze instelling om specifieke kernelextensies toe te staan. Alleen de kernelextensies die u invoert, worden toegestaan of vertrouwd.

  **Voeg** de bundel-id en team-id toe van een kernelextensie die u wilt laden. Voor niet-ondertekende verouderde kernelextensies gebruikt u een lege team-id. U kunt meerdere kernelextensies toevoegen. De team-id moet alfanumeriek zijn (letters en cijfers) en mag uit 10 tekens bestaan. Voer bijvoorbeeld `com.contoso.appname.macos` in voor **Bundel-id** en `ABCDE12345` voor **Team-id**.

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

## <a name="system-extensions"></a>Systeemextensies

Deze functie is van toepassing op:

- macOS 10.15 of hoger
- Door de gebruiker goedgekeurde apparaatinschrijving is vereist

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Door de gebruiker goedgekeurde apparaatinschrijving, automatische apparaatregistratie

- **Negeren door gebruiker blokkeren**: Met **Ja** wordt voorkomen dat gebruikers systeemextensies goedkeuren die zich niet op de lijst met toegestane extensies bevinden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers onbekende extensies goedkeuren die niet zijn opgenomen in het configuratieprofiel. Dit betekent dat extensies die niet zijn opgenomen in het configuratieprofiel zijn toegestaan.

- **Toegestane team-id's**: Gebruik deze instelling om een of meer team-id's toe te staan. Alle systeemextensies die zijn ondertekend met de team-id's die u invoert, zijn altijd toegestaan en worden altijd vertrouwd. Met andere woorden, gebruik deze optie om alle systeemextensies binnen dezelfde team-id toe te staan. Dit kan ook een specifieke ontwikkelaar of partner zijn.

  U kunt een **team-id** **toevoegen** van geldige en ondertekende systeemextensies die u wilt laden. U kunt meerdere team-id's toevoegen. De team-id moet alfanumeriek zijn (letters en cijfers) en mag uit 10 tekens bestaan. Voer bijvoorbeeld `ABCDE12345` in.

  Nadat u een team-id hebt toegevoegd, kan deze ook worden verwijderd.

  Op [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Zoek uw team-id, opent de website van Apple) vindt u meer informatie.

- **Toegestane systeemextensies**: Gebruik deze instelling om specifieke systeemextensies altijd toe te staan. Alleen de systeemextensies die u invoert, worden toegestaan of vertrouwd.

  **Voeg** de **bundel-id** en **team-id** toe van een systeemextensie die u wilt laden. Voor niet-ondertekende verouderde systeemextensies gebruikt u een lege team-id. U kunt meerdere systeemextensies toevoegen. De team-id moet alfanumeriek zijn (letters en cijfers) en mag uit 10 tekens bestaan. Voer bijvoorbeeld `com.contoso.appname.macos` in voor **Bundel-id** en `ABCDE12345` voor **Team-id**.

- **Toegestane typen systeemextensies**: Voer de team-id en de typen systeemextensies in die moeten worden toegestaan voor de team-id:
  - **Team-id**: Voer de team-id in van een andere systeemextensie waarvoor u specifieke extensietypen wilt toestaan. Of voer een team-id in die u hebt toegevoegd aan **Toegestane systeemextensies**.
  - **Toegestane typen systeemextensies**: Selecteer de typen systeemextensies die u voor elke team-id wilt toestaan. Uw opties zijn:
    - Alles selecteren
    - Stuurprogramma-extensies
    - Netwerkextensies
    - Beveiligingsextensies van eindpunt

    Zie [Systeemextensies](https://developer.apple.com/system-extensions/) (hiermee opent u de website van Apple) voor meer informatie over deze typen extensies.

    U kunt een team-id toevoegen uit de lijst **Toegestane systeemextensies** en een specifiek extensietype toestaan. Als de extensie een type is dat niet is toegestaan, wordt de extensie mogelijk niet uitgevoerd.

    Als u alle extensietypen voor een team-id wilt toestaan, voegt u de team-id toe aan de lijst **Toegestane systeemextensies**. Voeg de team-id niet toe aan de lijst **Toegestane typen systeemextensies**. Met andere woorden, als een team-id zich wel op de lijst **Toegestane systeemextensies** en niet op de lijst **Toegestane typen systeemextensies** bevindt, zijn alle extensietypen toegestaan voor die team-id.

> [!NOTE]
> Het toevoegen van dezelfde team-id voor **Toegestane systeemextensies** en **Toegestane team-id's** kan resulteren in een fout en mislukken van het profiel. Voeg dezelfde specifieke team-id niet aan beide instellingen toe. 

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

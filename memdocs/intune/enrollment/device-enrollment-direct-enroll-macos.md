---
title: Directe inschrijving voor macOS-apparaten gebruiken
titleSuffix: Microsoft Intune
description: Meer informatie over het inschrijven van macOS-apparaten met Directe inschrijving.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f12b90dd49dc9a9783a39fb78d74c40c6838b1e
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819965"
---
# <a name="use-direct-enrollment-for-macos-devices"></a>Directe inschrijving voor macOS-apparaten gebruiken

Intune ondersteunt de inschrijving van macOS-apparaten met behulp van Directe inschrijving (Direct Enrollment, DE) voor bedrijfsapparaten. Bij directe inschrijving wordt het apparaat niet gewist. Hiermee wordt het apparaat ingeschreven via de macOS-instellingen. Deze methode ondersteunt apparaten **zonder gebruikersaffiniteit**.

## <a name="prerequisites"></a>Vereisten

- Fysieke toegang tot macOS-apparaten
- [MDM-instantie instellen](../fundamentals/mdm-authority-set.md)
- [Een Apple MDM-pushcertificaat](apple-mdm-push-certificate-get.md)
 - Beheerdersrechten op de macOS-apparaten die u wilt inschrijven

## <a name="create-an-apple-configurator-profile-for-devices"></a>Een Apple Configurator-profiel maken voor apparaten

Met een inschrijvingsprofiel voor apparaten worden de instellingen tijdens het inschrijven gedefinieerd. Deze instellingen worden slechts eenmaal toegepast. Volg deze stappen om een inschrijvingsprofiel te maken om macOS-apparaten in te schrijven met directe inschrijving.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **Apparaten inschrijven** > **Apple-inschrijving** > **Apple Configurator**.

2. Kies **Profielen** > **Maken**.

3. Typ onder **Inschrijvingsprofiel maken** een **naam** en **beschrijving** voor het profiel (voor administratieve doeleinden). Gebruikers zien deze gegevens niet. U kunt dit veld Naam gebruiken om een dynamische groep te maken in Azure Active Directory. Gebruik de profielnaam om de parameter enrollmentProfileName te definiëren om apparaten aan dit inschrijvingsprofiel toe te wijzen. Meer informatie over dynamische Azure Active Directory-groepen.

4. Kies voor **Gebruikersaffiniteit** **Inschrijven zonder gebruikersaffiniteit**: kies deze optie voor apparaten die niet aan één gebruiker zijn gelieerd. Gebruik dit voor apparaten waarmee taken worden uitgevoerd zonder toegang tot lokale gebruikersgegevens. Apps waarvoor een gebruikersrelatie is vereist, zoals de bedrijfsportal-app die wordt gebruikt voor het installeren van LOB-apps, zullen niet werken. Vereist voor directe inschrijving.

     > [!NOTE]
     > **Inschrijven met gebruikersaffiniteit** wordt niet ondersteund in macOS wanneer u directe inschrijving gebruikt. Voor apparaten waarvoor gebruikersaffiniteit is vereist, gebruikt u Automatische apparaatinschrijving.

6. Kies **Maken** om het profiel op te slaan.

## <a name="direct-enrollment"></a>Directe inschrijving
De bedrijfsportal kan niet worden gebruikt om de beschikbare toepassingen te installeren omdat directe inschrijving alleen ondersteuning biedt voor inschrijving zonder gebruikersaffiniteit.

### <a name="export-the-profile-and-install-on-macos-devices"></a>Het profiel exporteren en installeren op macOS-apparaten

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **Apparaten inschrijven** > **Apple-inschrijving** > **Apple Configurator** > **Profielen** > kies het te exporteren profiel > **Profiel exporteren**.
2. Kies onder **Directe inschrijving** voor **Profiel downloaden** en sla het bestand op. 

     > [!NOTE]
     > Een gedownload inschrijvingsprofiel blijft na het downloaden twee weken geldig. Met deze koppeling kunt u zoveel inschrijvingsprofielen downloaden als u wilt. Als u een nieuw profiel downloadt, wordt het vorige profiel niet ongeldig. De verlooptijd van het eerder gedownloade bestand wordt hierdoor echter ook niet verlengd.
         
3. Breng het bestand over naar een macOS-apparaat om het rechtstreeks te installeren.
4. Dubbelklik op de opgeslagen **.mobileconfig** om het bestand te openen in Profielen.
5. Wanneer u wordt gevraagd het beheerprofiel te installeren, selecteert u **Installeren**.
6. Bevestig de volgende vraag of u het beheerprofiel wilt installeren door **Installeren**te selecteren.
7. Voer op het macOS-apparaat de referenties voor een beheerdersaccount in en klik op **OK**.
8. Het macOS-apparaat is nu ingeschreven bij Intune en wordt beheerd, doelprofielen worden gedownload.

## <a name="next-steps"></a>Volgende stappen

Nadat de macOS-apparaten zijn ingeschreven, kunt u [deze gaan beheren](../remote-actions/device-management.md).
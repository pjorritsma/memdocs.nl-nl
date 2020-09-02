---
title: De Bedrijfsportal-app voor macOS toevoegen
titleSuffix: Microsoft Intune
description: Voeg de Bedrijfsportal-app voor macOS toe.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1eb64f8ed2bc67b4800a4583010dea150ade421d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914154"
---
# <a name="add-the-macos-company-portal-app"></a>De Bedrijfsportal-app voor macOS toevoegen

Als gebruikers apparaten willen beheren, optionele apps willen installeren en toegang willen krijgen tot resource die worden beveiligd met voorwaardelijke toegang op macOS-apparaten met gebruikersaffiniteit, moeten zij de Bedrijfsportal-app installeren en zich hiermee aanmelden. U kunt uw gebruikers instructies geven om Bedrijfsportal voor macOS te installeren of deze app zelf installeren op apparaten die al rechtstreeks zijn ingeschreven bij Intune.

U kunt een van de volgende opties gebruiken om de Bedrijfsportal-app voor macOS te installeren:
- [Gebruikers instrueren om Bedrijfsportal te downloaden en installeren](#instruct-users-to-download-and-install-company-portal)
- [Bedrijfsportal voor macOS installeren als macOS Line-Of-Business-app](#install-company-portal-for-macos-as-a-macos-lob-app)
- [Bedrijfsportal voor macOS installeren met behulp van een macOS Shell-script](#install-company-portal-for-macos-by-using-a-macos-shell-script)

Om de apps veiliger te maken en up-to-date te houden na de installatie wordt de Bedrijfsportal-app geleverd met Microsoft AutoUpdate (MAU).

> [!NOTE]
> De Bedrijfsportal-app kan alleen automatisch worden geïnstalleerd op apparaten met Intune die al zijn ingeschreven met behulp van directe inschrijving of geautomatiseerde apparaatinschrijving. Voor persoonlijke apparaten of handmatige inschrijving moet de Bedrijfsportal-app worden gedownload en geïnstalleerd om de inschrijving te initiëren. Raadpleeg [Gebruikers instrueren om Bedrijfsportal te downloaden en installeren](#instruct-users-to-download-and-install-company-portal).
## <a name="instruct-users-to-download-and-install-company-portal"></a>Gebruikers instrueren om Bedrijfsportal te downloaden en installeren

U kunt gebruikers instrueren om Bedrijfsportal voor macOS te downloaden en installeren en zich aan te melden. Raadpleeg [Uw macOS-apparaat inschrijven via de bedrijfsportal-app](../user-help/enroll-your-device-in-intune-macos-cp.md) voor instructies over het downloaden en installeren van de Bedrijfsportal en het aanmelden.

##  <a name="install-company-portal-for-macos-as-a-macos-lob-app"></a>Bedrijfsportal voor macOS installeren als macOS Line-Of-Business-app

Bedrijfsportal voor macOS kan worden gedownload en geïnstalleerd met behulp van de functie [macOS Line-Of-Business-apps](lob-apps-macos.md). De versie die wordt gedownload is de versie die altijd wordt geïnstalleerd. Deze moet mogelijk periodiek worden bijgewerkt om ervoor te zorgen dat gebruikers de beste ervaring krijgen tijdens de initiële inschrijving.

1. Download Bedrijfsportal voor macOS vanuit https://go.microsoft.com/fwlink/?linkid=853070. 

2. Volg de instructies voor het maken van een macOS Line-Of-Business-app in [macOS Line-Of-Business-apps](lob-apps-macos.md).

> [!NOTE]
> Na de installatie zal de Bedrijfsportal-app voor macOS automatisch worden bijgewerkt met behulp van Microsoft AutoUpdate (MAU).
## <a name="install-company-portal-for-macos-by-using-a-macos-shell-script"></a>Bedrijfsportal voor macOS installeren met behulp van een macOS-shellscript

Bedrijfsportal voor macOS kan worden gedownload en geïnstalleerd met behulp van de functie [macOS Shell-scripts](macos-shell-scripts.md). Met deze optie wordt altijd de huidige versie van Bedrijfsportal voor macOS geïnstalleerd, maar beschikt u niet over een installatierapportage voor apps die u kunt gebruiken bij het implementeren van toepassingen met [macOS Line-Of-Business-apps](lob-apps-macos.md).

1. Download een voorbeeldscript om Bedrijfsportal voor macOS te installeren in [Intune Shell Script-voorbeelden: Bedrijfsportal](https://github.com/microsoft/shell-intune-samples/tree/master/Apps/Company%20Portal).

2. Volg de instructies voor het implementeren van het macOS Shell-script met [macOS Shell-scripts](macos-shell-scripts.md). 
    - Stel **Script uitvoeren als aangemelde gebruiker** in op **Nee** (om in de systeemcontext te worden uitgevoerd).
    - Stel **Maximum aantal keren dat het script opnieuw moet worden uitgevoerd als het script mislukt** in op **3**.

> [!NOTE]
> Voor het script is internettoegang vereist wanneer het wordt uitgevoerd om de huidige versie van Bedrijfsportal voor macOS te downloaden. 
## <a name="next-steps"></a>Volgende stappen
- Zie [Apps aan groepen toewijzen](apps-deploy.md) voor meer informatie over het toewijzen van apps.
- Zie [Programma voor apparaatinschrijving: macOS inschrijven](../enrollment/device-enrollment-program-enroll-macos.md) voor meer informatie over het configureren van automatische apparaatinschrijving.
- Zie [Mac-updates](/windows/security/threat-protection/microsoft-defender-atp/mac-updates) voor meer informatie over het configureren van instellingen voor Microsoft AutoUpdate op macOS.
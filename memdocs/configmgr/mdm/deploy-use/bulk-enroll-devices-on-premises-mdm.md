---
title: Apparaten bulksgewijs inschrijven
titleSuffix: Configuration Manager
description: Apparaten bulksgewijs inschrijven op een geautomatiseerde manier met on-premises Mobile Device Management (MDM) in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 474d59ec22d1edaf8e662298e90555e6772d302b
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698793"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Apparaten bulksgewijs inschrijven met on-premises MDM in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Bulk inschrijving in Configuration Manager on-premises Mobile Device Management (MDM) is een geautomatiseerde methode voor het inschrijven van apparaten. De andere methode is gebruikers registratie, waarvoor gebruikers hun referenties moeten invoeren om het apparaat in te schrijven. Voor bulkinschrijving wordt gebruikgemaakt van een inschrijvingspakket om het apparaat tijdens de inschrijving te verifiëren. Het pakket is een. ppkg-bestand, dat ook certificaat-en Wi-Fi-profielen kan bevatten ter ondersteuning van de inschrijving.

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a> Een certificaat profiel maken

Neem een certificaat profiel op om automatisch een vertrouwd basis certificaat op het apparaat te installeren. Dit basis certificaat is vereist voor een vertrouwde communicatie tussen de apparaten en de site systeem rollen die nodig zijn voor on-premises MDM.

Wanneer u de site voorbereidt voor on-premises MDM, exporteert u het vertrouwde basis certificaat. Gebruik dit certificaat in het certificaat Profiel van het inschrijvings pakket. Zie [het vertrouwde basis certificaat exporteren](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert)voor meer informatie over het ophalen van het vertrouwde basis certificaat.

Het geëxporteerde certificaat gebruiken om een certificaat profiel te maken. Zie [certificaat profielen maken](../../protect/deploy-use/create-certificate-profiles.md)voor meer informatie.

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a> Een Wi-Fi-profiel maken

Een ander onderdeel van het pakket voor bulk inschrijving is een Wi-Fi-profiel. Dit profiel kan ervoor zorgen dat het apparaat is verbonden met het netwerk om inschrijving te ondersteunen.

Zie [Wi-Fi-profielen maken](../../protect/deploy-use/create-wifi-profiles.md)voor meer informatie over het maken van een Wi-Fi-profiel in Configuration Manager.

### <a name="wi-fi-profile-limitations"></a>Beperkingen voor Wi-Fi-profielen

Lees de volgende beperkingen wanneer u een Wi-Fi-profiel maakt voor een on-premises MDM-bulk registratie.

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>Wi-Fi-beveiligings configuraties voor on-premises MDM

De huidige vertakking van Configuration Manager ondersteunt alleen de volgende Wi-Fi-beveiligings configuraties voor on-premises MDM:

- Beveiligingstypen: **WPA2-Enterprise** of **WPA2-Personal**

- Versleutelingstypen : **AES** of **TKIP**

- EAP-typen: **smartcard of ander certificaat** of **PEAP**

#### <a name="proxy-server"></a>Proxyserver

Hoewel Configuration Manager een instelling heeft voor proxyserver gegevens in het Wi-Fi-profiel, wordt de proxy niet geconfigureerd wanneer het apparaat wordt Inge schreven. Als u een proxy server op bulksgewijs geregistreerde apparaten moet instellen:

- De instellingen implementeren met configuratie-items zodra apparaten zijn Inge schreven.

- Maak een tweede pakket met behulp van de Windows-installatie kopie en Configuration Designer (ICD) en implementeer het vervolgens samen met het pakket voor bulk inschrijving.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> Een inschrijvings profiel maken

Met het inschrijvings profiel kunt u instellingen opgeven die vereist zijn voor het inschrijven van apparaten. Deze instellingen omvatten een [certificaat profiel](#bkmk_createCert) en een [Wi-Fi-profiel](#CreateWifi).

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **alle apparaten in bedrijfs eigendom**uit, vouw **Windows**uit en selecteer het knoop punt **inschrijvings profielen** .

1. Selecteer **inschrijvings profiel maken**op het lint.

1. Geef op de pagina **Algemeen** van de wizard inschrijvings profiel maken de volgende informatie op:

    - **Naam**: een unieke naam om het profiel te identificeren

    - **Beschrijving**: een optioneel veld om het profiel verder te beschrijven

    - **Beheer instantie**: alleen **on-premises** selecteren

1. Selecteer op de pagina **site toewijzing** de code van de **beheer site** met een apparaatbeheerpunt.

1. Selecteer op de pagina **inschrijvings proxy punt selecteren** de optie **alleen intranet**en selecteer vervolgens een of meer proxy punten voor inschrijving. Het apparaat zal deze servers gebruiken om het registratie proces te starten.

1. Selecteer op de pagina **vertrouwd basis certificaat selecteren** het certificaat profiel met het vertrouwde basis certificaat.

1. Selecteer op de pagina **Wi-Fi-profielen** het Wi-Fi-profiel met de benodigde netwerk instellingen voor apparaten om verbinding te maken.

    > [!TIP]
    > Als u geen Wi-Fi-profiel gebruikt voor uw inschrijvings pakket, kunt u deze stap overs Laan.

1. Voltooi de wizard.

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a> Een inschrijvings pakket maken

Het inschrijvings pakket (ppkg) is het bestand dat u gebruikt voor het bulksgewijs inschrijven van apparaten voor on-premises MDM. Maak dit bestand met Configuration Manager. U kunt vergelijk bare typen pakketten maken met Windows ICD, maar alleen pakketten die u in Configuration Manager maakt, kunnen worden gebruikt om apparaten in te schrijven voor on-premises MDM. Een pakket dat u met Windows ICD maakt, kan alleen de user principal name (UPN) opgeven die nodig is voor de registratie. het kan echter niet starten met het feitelijke inschrijvings proces.

Het proces voor het maken van het inschrijvingspakket vereist Windows Assessment and Deployment Toolkit (ADK) voor Windows 10. Installeer de nieuwste versie van Windows ADK op de computer waarop de Configuration Manager-console wordt uitgevoerd. Selecteer de functie **Imaging and Configuration Designer (ICD)** en eventuele afhankelijkheden. (Deze versie hoeft niet overeen te komen met de versie die wordt gebruikt voor de implementatie van het besturings systeem door de Configuration Manager-site.) Zie [de Windows ADk voor Windows 10 downloaden](/windows-hardware/get-started/adk-install)voor meer informatie.

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **alle apparaten in bedrijfs eigendom**uit, vouw **Windows**uit en selecteer het knoop punt **inschrijvings profielen** .

1. Selecteer een bestaand inschrijvings profiel. Selecteer **exporteren**in het lint.

1. Geef in het venster inschrijvings pakket exporteren de volgende informatie op:

    - **Geldigheids periode (dagen)**: standaard stelt Configuration Manager het inschrijvings pakket in op een verval datum van twee weken (14 dagen). U kunt het pakket voor apparaatregistratie niet gebruiken nadat de geldigheids periode is verstreken. Voer een geheel getal in tussen 1 en 30.

    - **Pakket bestand**: Geef een lokaal pad of een bestandspad en een bestands naam op voor het. ppkg-bestand.

    - **Pakket versleutelen**: Schakel deze optie in om het pakket met een wacht woord te beveiligen. Nadat u het pakket hebt geëxporteerd, wordt in Configuration Manager het gegenereerde wacht woord weer gegeven. Kopieer het wacht woord en sla het op een beveiligde locatie op. U kunt het geëxporteerde inschrijvings pakket niet gebruiken zonder het wacht woord.

        > [!IMPORTANT]
        > Configuration Manager slaat het wacht woord niet op en u kunt het niet aanpassen of wijzigen. Wanneer u het venster sluit waarin het wacht woord wordt weer gegeven, is het niet mogelijk om het wacht woord op te halen.

1. Selecteer **Exporteren**. Configuration Manager maakt gebruik van de Windows ADK om het inschrijvings pakket te maken.

Configuration Manager houdt geldige inschrijvings pakketten bij. Vouw in de-console het knoop punt voor het **inschrijvings profiel** uit en selecteer **geëxporteerde pakketten**.

> [!TIP]
> Als u een inschrijvings pakket uit de Configuration Manager-console verwijdert, kunt u dit niet gebruiken om apparaten in te schrijven. Gebruik deze methode om inschrijvings pakketten te beheren die u niet wilt dat anderen voor bulk inschrijving gebruiken.

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a> Een apparaat bulksgewijs inschrijven

U kunt een pakket gebruiken om apparaten in te schrijven vóór of na het OOBE-proces (out-of-Box Experience) van het apparaat. Het inschrijvings pakket kan ook worden opgenomen als onderdeel van een OEM-inrichtings pakket (Original Equipment Manufacturer).

Als u het pakket voor bulk registratie wilt gebruiken, moet u het fysiek leveren op het apparaat. Er zijn verschillende methoden, afhankelijk van uw behoeften, bijvoorbeeld:

- Kopiëren van het bestands systeem

- Aan een e-mail bericht koppelen

- Kopiëren via een NFC-verbinding (Near Field Communication)

- Kopiëren van een geheugen kaart

- Een streepjescode scannen

- Kopiëren van een aangesloten apparaat

- In een OEM-inrichtings pakket toevoegen

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>Een apparaat inschrijven met het pakket voor bulk inschrijving

1. Open het. ppkg-bestand op een apparaat. Als administrator uitvoeren als dat nodig is.

1. Windows vraagt of het pakket afkomstig is van een vertrouwde bron. Selecteer **Ja**.

Het registratie proces wordt gestart.

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a> Inschrijving verifiëren

### <a name="verify-bulk-enrollment-on-the-device"></a>Bulk inschrijving op het apparaat controleren

1. Open **instellingen**op het apparaat.

1. Selecteer **accounts**en selecteer **toegang tot werk of school**. Wanneer de inschrijving is geslaagd, ziet u een account onder **CompanyApps**.

1. Selecteer het account en selecteer vervolgens **synchroniseren**. Met deze actie wordt het beheer met Configuration Manager gestart.

### <a name="verify-enrollment-in-the-console"></a>Inschrijving in de console verifiëren

Gebruik de Configuration Manager-console om te controleren of de apparaten zijn Inge schreven. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer **apparaten**. Blader of zoek naar het geregistreerde apparaat in de lijst met apparaten.
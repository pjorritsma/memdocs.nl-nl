---
title: Inschrijving instellen voor on-premises MDM
titleSuffix: Configuration Manager
description: Gebruikers machtigen om hun apparaten in te schrijven voor on-premises Mobile Device Management (MDM) in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721841"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>Registratie van apparaten instellen voor on-premises MDM in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De laatste stap voor het instellen van on-premises Mobile Device Management (MDM) is om gebruikers in staat te stellen hun apparaten in te schrijven. Gebruik Configuration Manager client instellingen om gebruikers toestemming te verlenen om apparaten in te schrijven in on-premises MDM.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a>Een inschrijvings profiel maken

Als u de instellingen wilt pushen die vereist zijn om gebruikers toe te staan mobiele apparaten te registreren, voegt u een nieuw inschrijvings profiel toe aan de standaard-client instellingen. Dit profiel is vervolgens van toepassing op alle gebruikers op de Configuration Manager-site.

> [!NOTE]
> Dit proces maakt gebruik van de **standaard client instellingen**, die automatisch van toepassing zijn op alle apparaten en gebruikers. U kunt ook aangepaste client instellingen maken en vervolgens implementeren naar verzamelingen van uw keuze. Deze alternatieve methode vereist ten minste twee aangepaste client instellingen, één voor *Apparaatinstellingen* en één voor *gebruikers* instellingen. Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor meer informatie.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **client instellingen** . Open **standaard client instellingen** en selecteer de **registratie** groep.

1. Geef onder Apparaatinstellingen het **polling-interval voor moderne apparaten (minuten) op**. Dit interval is standaard 60 minuten.

1. Schakel onder gebruikers instellingen de optie in om **gebruikers toe te staan moderne apparaten in te schrijven**.

1. Selecteer **profiel instellen**voor het **inschrijvings profiel voor moderne apparaten**. Selecteer in het venster inschrijvings profiel de optie **maken**.

1. Geef in het venster inschrijvings profiel maken de volgende informatie op:

    - Een unieke en beschrijvende **naam** voor het inschrijvings profiel.

    - Een optionele **Beschrijving** om aanvullende informatie over het profiel op te geven.

    - Kies de **code van de beheer site** die het apparaatbeheerpunt bevat. Selecteer **OK** om op te slaan en te sluiten.

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>Aanvullende client instellingen configureren

Er zijn aanvullende client instellingen voor het configureren van apparaten nadat ze zijn Inge schreven. Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor meer algemene informatie.

Configuration Manager ondersteunt de volgende client instellingen voor on-premises MDM:

- **Client beleid**: met deze instellingen bepaalt u de frequentie voor het downloaden van client beleid naar het apparaat. U kunt ook instellingen voor gebruikers beleid inschakelen. Zie [client instellingen-client beleid](../../core/clients/deploy/about-client-settings.md#client-policy)voor meer informatie.

- **Software-implementatie**: Stel het interval voor het evalueren van software-implementaties in. Zie [client instellingen-software-implementatie](../../core/clients/deploy/about-client-settings.md#software-deployment)voor meer informatie.

    > [!NOTE]
    > Voor on-premises MDM kunnen instellingen voor software-implementatie alleen worden gebruikt als standaard client instellingen.

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>Gebruikers detecteren

Als gebruikers de client instellingen moeten ontvangen met het inschrijvings profiel voor on-premises MDM, detecteert de site hun gebruikers account in Active Directory. Voer detectie voor Active Directory-gebruikers om te zorgen dat iedereen die het inschrijvingsprofiel nodig heeft, het ontvangt. Zie [Active Directory gebruikers detectie](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)voor meer informatie.

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>Het vertrouwde basis certificaat installeren

Apparaten die lid zijn van een domein, krijgen het vertrouwens basis certificaat voor vertrouwde communicatie met de servers die als host fungeren voor de site systeem rollen. Active Directory Certificate Services distribueert automatisch het vertrouwde basis certificaat. Computers en mobiele apparaten die niet lid zijn van een domein, moeten dit certificaat via een andere manier installeren om inschrijving toe te staan.

> [!NOTE]
> Als de webserver certificaten zijn uitgegeven door een open bare certificerings instantie, worden deze Ca's al door de meeste apparaten vertrouwd. Als uw ontwerp gebruik maakt van een van deze open bare Ca's, hoeft u deze stap niet uit te voeren.

Nadat u [het vertrouwde basis certificaat hebt geëxporteerd](set-up-certificates-on-premises-mdm.md#bkmk_exportCert), moet u het installeren op apparaten waarop het moet worden inge schreven. Bijvoorbeeld apparaten die niet zijn toegevoegd aan het domein en niet automatisch kunnen worden opgehaald uit Active Directory. Het proces dat u gebruikt, is afhankelijk van de volgende factoren:

- Specifieke apparaattypen en technische mogelijkheden
- Versie van het besturingssysteem
- De vereisten voor uw bedrijf, beveiliging en gebruikers ervaring

De volgende lijst bevat enkele voor beelden van methoden voor het leveren en installeren van het vertrouwde basis certificaat op apparaten:

- Bestandsshare

- E-mailbijlage

- Geheugenkaart

- Aangesloten apparaat

- Opslag in de cloud (zoals OneDrive)

- NFC-verbinding (Near Field Communication)

- Streepjescodescanner

- OOBE- inrichtingspakket (out of box experience)

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>Het vertrouwde basis certificaat hand matig installeren in Windows

1. Op het apparaat dat moet worden inge schreven, bladert u in Verkenner naar het bestand met het vertrouwde basis certificaat (. CER) en **opent** u het.

1. Selecteer **certificaat installeren**in het venster certificaat.

1. Selecteer in de wizard Certificaat importeren de optie **lokale computer**en selecteer vervolgens **volgende** om door te gaan als Administrator.

1. Selecteer op de pagina certificaat archief **alle certificaten in het onderstaande archief opslaan**en selecteer vervolgens **Bladeren**.

1. Selecteer in het venster certificaat archief selecteren de optie **vertrouwde basis certificerings instanties**en selecteer **OK**.

1. Volt ooien en wizard.

## <a name="next-step"></a>Volgende stap

> [!div class="nextstepaction"]
> [Apparaten inschrijven](../deploy-use/enroll-devices-on-premises-mdm.md)

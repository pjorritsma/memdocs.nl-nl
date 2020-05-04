---
title: MacOS-clients upgraden
titleSuffix: Configuration Manager
description: Voer een upgrade uit voor de Configuration Manager-client op Mac-computers.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34d0c9233b4f7384dfc2280dc92334450a785ed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715002"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Clients op Mac-computers bijwerken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Volg de stappen op hoog niveau in dit artikel om een upgrade uit te voeren van de client voor Mac-computers met behulp van een Configuration Manager-toepassing. U kunt het installatie bestand voor de Mac-client ook downloaden, kopiëren naar een gedeelde netwerk locatie of een lokale map op de Mac-computer en vervolgens gebruikers instrueren om de installatie hand matig uit te voeren.  

> [!NOTE]  
> Voordat u deze stappen uitvoert, moet u ervoor zorgen dat uw Mac-computer voldoet aan de vereisten. Zie [ondersteunde besturings systemen voor Mac-computers](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="download-the-latest-mac-client"></a>De nieuwste Mac-client downloaden

De Mac-client voor Configuration Manager is niet opgegeven op de Configuration Manager-installatie media. Down load het vanuit het micro soft Download centrum, [micro soft Endpoint Configuration Manager-MacOS client (64-bits)](https://www.microsoft.com/download/details.aspx?id=100850). De installatie bestanden van de Mac-client bevinden zich in een Windows Installer bestand met de naam **ConfigmgrMacClient. msi**.  

## <a name="create-the-mac-client-installation-file"></a>Het installatie bestand voor de Mac-client maken

Op een computer waarop Windows wordt uitgevoerd, voert u **ConfigmgrMacClient. msi**uit. Dit installatie programma pakt het installatie bestand van de Mac-client met de naam **Macclient. dmg**uit. U kunt dit bestand standaard vinden in de volgende map: **C:\Program Files\Microsoft\System Center Configuration Manager voor Mac-client**.  

## <a name="extract-the-client-installation-files"></a>De client installatie bestanden uitpakken

Kopieer **Macclient. dmg** naar een Mac-computer. Koppel het bestand Macclient. dmg in macOS en kopieer de inhoud vervolgens naar een map op de Mac-computer.  

## <a name="create-a-cmmac-file"></a>Een. cmmac-bestand maken

1. Open de map **Hulpprogram ma's** van de Mac-client installatie bestanden. Gebruik het hulp programma **CMAppUtil** om een. cmmac-bestand te maken op basis van het client installatie pakket. U gebruikt dit bestand om de Configuration Manager-toepassing te maken.  

2. Kopieer het nieuwe bestand **CMClient. pak. cmmac** naar een netwerk locatie die beschikbaar is voor de computer waarop de Configuration Manager-console wordt uitgevoerd.  

    Zie de aanvullende procedures voor het [maken en implementeren van toepassingen voor Mac-computers](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers)voor meer informatie.  

## <a name="create-and-deploy-the-app"></a>De app maken en implementeren

1. Maak in de Configuration Manager-console [een toepassing](../../../../apps/get-started/creating-mac-computer-applications.md) vanuit het bestand **CMClient. pak. cmmac** .  

2. [Implementeer deze toepassing](../../../../apps/deploy-use/deploy-applications.md) op Mac-computers in uw-hiërarchie.  

## <a name="install-the-updated-client"></a>De bijgewerkte client installeren

De bestaande Configuration Manager-client op Mac-computers vraagt de gebruiker of er een update beschikbaar is om te worden geïnstalleerd. Na installatie van de client moeten gebruikers hun Mac-computer opnieuw opstarten.  

Nadat de computer opnieuw is opgestart, wordt automatisch de wizard **computer registratie** uitgevoerd om een nieuw gebruikers certificaat aan te vragen.

Als u Configuration Manager-inschrijving niet gebruikt, maar het client certificaat onafhankelijk van Configuration Manager installeert, raadpleegt u [clients configureren voor het gebruik van een bestaand certificaat](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="configure-clients-to-use-an-existing-certificate"></a><a name="BKMK_UpgradingClient_MachineEnrollment"></a>Clients configureren voor het gebruik van een bestaand certificaat

Gebruik deze procedure om te voor komen dat de wizard computer registratie wordt uitgevoerd en om de bijgewerkte client te configureren voor het gebruik van een bestaand client certificaat.  

1. Maak in de Configuration Manager-console [een configuratie-item](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) van het type **Mac OS X**.  

1. Voeg een instelling toe aan dit configuratie-item met het instellingstype **Script**.  

1. Voeg het volgende script toe aan de instelling:  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. Voeg het configuratie-item toe aan een [configuratie basislijn](../../../../compliance/deploy-use/create-configuration-baselines.md). [Implementeer vervolgens de configuratie basislijn](../../../../compliance/deploy-use/deploy-configuration-baselines.md) op alle Mac-computers waarop een certificaat onafhankelijk van Configuration Manager wordt geïnstalleerd.  

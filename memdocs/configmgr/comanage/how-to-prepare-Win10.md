---
title: Op internet gebaseerde apparaten gezamenlijk beheren
titleSuffix: Configuration Manager
description: Meer informatie over het voorbereiden van uw Windows 10-apparaten op internet voor co-beheer.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/14/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 66e6156466d0432aaa8b3b162263f8207bdc9d78
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455103"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Het voorbereiden van op internet gebaseerde apparaten voor co-beheer

Dit artikel is gericht op het tweede pad naar co-beheer, voor nieuwe apparaten op internet. Dit scenario is wanneer u nieuwe Windows 10-apparaten hebt die lid worden van Azure AD en automatisch worden inge schreven bij intune. U installeert de Configuration Manager-client om een co-beheer status te bereiken.  

## <a name="windows-autopilot"></a>Windows Autopilot

Voor nieuwe Windows 10-apparaten kunt u de auto pilot-service gebruiken om de out of Box Experience (OOBE) te configureren. Dit proces omvat het toevoegen van het apparaat aan Azure AD en het inschrijven van het apparaat bij intune.  

Zie [overzicht van Windows auto pilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot)voor meer informatie.

Als u uw apparaten zo wilt configureren dat deze automatisch worden inge schreven bij intune wanneer ze lid worden van Azure AD, raadpleegt u [Windows-apparaten inschrijven voor Microsoft intune](https://docs.microsoft.com/intune/windows-enroll).  

### <a name="gather-information-from-configuration-manager"></a>Gegevens van Configuration Manager verzamelen

Gebruik Configuration Manager om de apparaatgegevens te verzamelen en te rapporteren die vereist zijn voor intune. Deze informatie omvat het serie nummer van het apparaat, de Windows-product-id en een hardware-id. Het wordt gebruikt om het apparaat te registreren bij intune voor de ondersteuning van Windows auto pilot.

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw het knoop punt **rapportage** uit, vouw **rapporten**uit en selecteer het knoop punt **Hardware-algemeen** .  

2. Voer het rapport en de **gegevens van Windows auto pilot-apparaten**uit en Bekijk de resultaten.  

3. Selecteer in de rapport viewer het pictogram voor **exporteren** en kies de **CSV (door komma's gescheiden)** optie.  

4. Nadat u het bestand hebt opgeslagen, uploadt u de gegevens naar intune.  

Zie [apparaten toevoegen in intune](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices)voor meer informatie.

### <a name="autopilot-for-existing-devices"></a>Automatische pilot voor bestaande apparaten
<!--1358333-->

[Windows auto pilot voor bestaande apparaten](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) is beschikbaar in Windows 10, versie 1809 of hoger. Met deze functie kunt u de installatie kopie van een Windows 7-apparaat voor de door de [gebruiker gestuurde Windows-modus voor automatische Piloting](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) en het inrichten met één systeem eigen Configuration Manager taken reeks.

Zie voor meer informatie [Windows auto pilot voor bestaande apparaten taken reeks](../osd/deploy-use/windows-autopilot-for-existing-devices.md).

## <a name="install-the-configuration-manager-client"></a>De Configuration Manager-client installeren

Voor apparaten op internet in het tweede pad moet u een app maken in intune. Implementeer deze app op Windows 10-apparaten die niet al Configuration Manager-clients zijn.

> [!NOTE]
> Voordat u deze app toewijst aan apparaten in intune, moet u ervoor zorgen dat de apparaten het CMG Server-verificatie certificaat vertrouwen. Zie [CMG voor vertrouwde basis certificaten voor clients](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot)voor meer informatie. Als een apparaat het certificaat voor verificatie van de CMG-server niet vertrouwt, ziet u een WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA fout in de ccmsetup. log op de client.

### <a name="get-the-command-line-from-configuration-manager"></a>De opdracht regel ophalen uit Configuration Manager

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt voor **co-beheer** .  

2. Selecteer het object voor co-beheer en kies **Eigenschappen** in het lint.  

3. Kopieer de opdracht regel op het tabblad **Activering** . Plak deze in Klad blok om op te slaan voor het volgende proces.  

De volgende opdracht regel is een voor beeld:`CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
Bepaal welke opdracht regel eigenschappen u voor uw omgeving nodig hebt:  

- De volgende opdracht regel eigenschappen zijn vereist in alle scenario's:  
  - CCMHOSTNAME  
  - SMSSITECODE  

- De volgende eigenschappen zijn vereist wanneer u Azure AD gebruikt voor client verificatie in plaats van client verificatie certificaten op basis van PKI:  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- Als de client terugkeert naar het intranet, gebruikt u de volgende eigenschap:
  - SMSMP  

- Als u uw eigen PKI-certificaat gebruikt en uw CRL niet is gepubliceerd op internet, is de volgende para meter vereist:  
  - /noCRLCheck  

    Zie voor meer informatie [planning voor crl's](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

- Vanaf versie 2002 gebruikt u de volgende eigenschap om een taken reeks onmiddellijk na de registratie van de client op te bootslen:
  - PROVISIONTS

    Zie [over eigenschappen van client installatie-PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts)voor meer informatie.

De site publiceert extra Azure AD-gegevens naar de Cloud beheer gateway (CMG). Een client die lid is van Azure AD, haalt deze informatie op uit de CMG tijdens het ccmsetup-proces, waarbij dezelfde Tenant wordt gebruikt waaraan deze is gekoppeld. Dit gedrag vereenvoudigt het inschrijven van apparaten op co-beheer in een omgeving met meer dan één Azure AD-Tenant. De enige twee vereiste ccmsetup-eigenschappen zijn **CCMHOSTNAME** en **SMSSITECODE**.<!--3607731-->

> [!NOTE]
> Als u de Configuration Manager-client al in intune implementeert, werkt u de intune-app bij met een nieuwe opdracht regel en een nieuw MSI-bestand. <!-- SCCMDocs-pr issue 3084 -->

Het volgende voor beeld bevat al deze eigenschappen:

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

Zie [Eigenschappen van client installatie](../core/clients/deploy/about-client-installation-properties.md)voor meer informatie.

### <a name="create-the-app-in-intune"></a>De app in intune maken

1. Ga naar het [beheer centrum van micro soft Endpoint Manager](https://endpoint.microsoft.com)en vouw vervolgens het navigatie deel venster aan de linkerkant uit.  

2. Selecteer **apps**  >  **alle apps**  >  **toevoegen**.  

3. Onder **andere**selecteert u de **line-of-Business-app**.  

4. Upload het bestand **ccmsetup. msi** -app-pakket. Dit bestand vindt u in de volgende map op de site server Configuration Manager: `<ConfigMgr installation directory>\bin\i386` .  

    > [!Tip]  
    > Wanneer u de site bijwerkt, zorg er dan voor dat u deze app ook bijwerkt in intune.  

5. Nadat de app is bijgewerkt, configureert u de app-gegevens met de opdracht regel die u van Configuration Manager hebt gekopieerd.  

> [!IMPORTANT]
> Als u deze opdracht regel aanpast, moet u ervoor zorgen dat deze niet langer is dan 1024 tekens. Wanneer de opdracht regel langer is dan 1024 tekens, mislukt de installatie van de client.

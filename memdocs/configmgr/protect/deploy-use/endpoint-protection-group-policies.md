---
title: Endpoint Protection beheren met groepsbeleid
titleSuffix: Configuration Manager
description: Meer informatie over het beheren van Endpoint Protection met behulp van groeps beleid.
ms.date: 08/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d028dc6149ae1fee2d61634b96ccf450fc8f4b24
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700596"
---
# <a name="use-group-policy-settings-to-manage-endpoint-protection-in-previous-versions-of-windows"></a>groepsbeleid-instellingen gebruiken voor het beheren van Endpoint Protection in eerdere versies van Windows

**Van toepassing op:**

- [Micro soft Defender Advanced Threat Protection (micro soft Defender ATP)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE2O8jv)
- System Center Endpoint Protection op de volgende apparaten op het lagere niveau:
    - Windows Server 2012 R2
    - Windows 8.1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

Het kan zijn dat u een aantal down level-of verouderde Windows-apparaten hebt die zijn ingeschakeld met Endpoint Protection, maar buiten uw Configuration Manager-hiërarchie vallen. Bijvoorbeeld apparaten in een gedemilitariseerde zone of apparaten die zijn geïntegreerd met fusies en acquisities. 

U kunt Endpoint Protection op dergelijke apparaten met behulp van groepsbeleid-instellingen beheren, zoals hieronder wordt beschreven:

- [Endpoint Protection beleids definities kopiëren](#copy-endpoint-protection-policy-definitions)
- Laad Endpoint Protection beleids definities op een van de volgende locaties:
    - [Centraal archief op een domein controller (aanbevolen)](#load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller)
    - [Lokaal apparaat](#load-endpoint-protection-group-policy-settings-into-your-local-device)

> [!NOTE]
> Zie [Groepsbeleid-instellingen gebruiken voor het configureren en beheren van micro soft Defender anti virus](/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus)voor informatie over het gebruik van Groepsbeleid instellingen voor het beheren van micro soft Defender anti virus in Windows 10, windows server 2019 en windows server 2016.

## <a name="copy-endpoint-protection-policy-definitions"></a>Endpoint Protection beleids definities kopiëren

Kopieer op een Windows-apparaat dat wordt beheerd door Endpoint Protection, de Endpoint Protection-beleids definitie bestanden.

1. Ga naar **C:\Program Files\Microsoft Security Client\Admx**. 

2. Comprimeer de volgende bestanden naar een zip-bestand, bijvoorbeeld **SCEP_admx.zip**:
    - **EndPointProtection. ADML**
    - **EndPointProtection. ADMX**
3. Kopieer het zip-bestand naar een tijdelijke map. Bijvoorbeeld, **c:\ temp_SCEP_GPO_admx**.
4. Pak het bestand uit. 

> [!NOTE]
> De register sleutels voor het configureren van Endpoint Protection beleids instellingen bevinden zich in **Hkey_Local_Machine \software\policies\microsoft\microsoft antimalware**.

## <a name="load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller"></a>Endpoint Protection groepsbeleid-instellingen laden in een centraal archief op een domein controller

Als u een [centraal archief voor groepsbeleid Beheersjablonen](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra)gebruikt, voert u de volgende stappen uit om Endpoint Protection groeps beleids instellingen te laden en te configureren. Dit is de aanbevolen methode.

1. Ga naar de map waarin u de Endpoint Protection Policy Definition Files hebt uitgepakt.
2. Kopieer de. ADMX-en. ADML-bestanden naar de map **PolicyDefinitions** op de domein controller:
    1. Kopieer **EndPointProtection. ADMX** naar ** \\ \\ \<forest.root\> \\ SYSVOL- \\ \<domain\> \\ beleids regels \\ PolicyDefinitions**. 
    2. Kopieer **EndPointProtection. ADML** naar ** \\ \\ \<forest.root\> \\ SYSVOL \\ \<domain\> \\ \\ -beleid PolicyDefinitions \\ en-US**.  

    Bijvoorbeeld:
    
    - Kopieer **EndPointProtection. ADMX** naar ** \\ DC\SYSVOL\contoso.com\Policies\PolicyDefinitions**.
    - Kopieer **EndPointProtection. ADML** naar ** \\ DC\SYSVOL\contoso.com\Policies\PolicyDefinitions\en-US**.
    
    waarbij **DC** de naam van uw domein controller is en **contoso.com** uw domein is.

3. Open de [console Groepsbeleidbeheer](/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11) en maak een nieuw Groepsbeleid-object (GPO) in uw domein, bijvoorbeeld **Endpoint Protection**.
4. Klik met de rechter muisknop op het groeps beleidsobject voor Endpoint Protection en klik op **bewerken**.
5. Ga in Groepsbeleidsbeheer-editor naar **computer configuratie**  >  **beleid**  >  **Beheersjablonen: beleids definities**  >  **Windows-onderdelen**  >  **Endpoint Protection**.

   De lijst met Endpoint Protection groeps beleid wordt weer gegeven.

6. Vouw de sectie uit die de instelling bevat die u wilt configureren, dubbel klik op de instelling om deze te openen en configuratie wijzigingen aan te brengen.

## <a name="load-endpoint-protection-group-policy-settings-into-your-local-device"></a>Endpoint Protection groepsbeleid-instellingen in het lokale apparaat laden

In plaats van centraal archief te gebruiken voor het laden van Endpoint Protection beleids definities, kunt u deze lokaal opslaan op uw apparaat.

1. Ga naar de map waarin u de Endpoint Protection Policy Definition Files hebt uitgepakt.
2. Kopieer de. ADMX-en. ADML-bestanden naar de lokale map PolicyDefinitions.
    1. Kopieer **EndPointProtection. ADMX** naar **% System root%/PolicyDefinitions**. 
    2. Kopieer **EndPointProtection. ADML** naar **% System root%/PolicyDefinitions/en-US**.
    
    Bijvoorbeeld:

    - Kopieer **EndPointProtection. ADMX** naar **C:\Windows\PolicyDefinitions**.
    - Kopieer **EndPointProtection. ADML** naar **C:\Windows\PolicyDefinitions\en-US**.
    
3. Open Lokale groepsbeleidsobjecteditor.
4. Ga naar **computer configuratie**  >  **Beheersjablonen**  >  **Windows-onderdelen**  >  **Endpoint Protection**.

    De lijst met Endpoint Protection groeps beleid wordt weer gegeven.

5. Vouw de sectie uit die de instelling bevat die u wilt configureren, dubbel klik op de instelling om deze te openen en configuratie wijzigingen aan te brengen.

## <a name="next-steps"></a>Volgende stappen
- Zie [Endpoint Protection](endpoint-protection.md)voor een overzicht van Endpoint Protection.
- Zie [Endpoint Protection op een zelfstandige client configureren](endpoint-protection-configure-standalone-client.md)voor meer informatie over het hand matig configureren van Endpoint Protection op een zelfstandige client.
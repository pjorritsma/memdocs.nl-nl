---
title: Apparaten versleutelen met de versleutelingsmethode die wordt ondersteund op platforms
titleSuffix: Microsoft Intune
description: Versleutel apparaten met ingebouwde versleutelingsmethoden zoals BitLocker of FileVault, en beheer de herstelsleutels voor deze versleutelde apparaten vanuit de Intune-portal.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: ac81ceced473eacc32a3fca566f7c36eb7a262e2
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084881"
---
# <a name="use-device-encryption-with-intune"></a>Apparaatversleuteling gebruiken met Intune

U kunt Intune gebruiken om de versleuteling van de ingebouwde schijf of het station van een apparaat te beheren voor het beschermen van de gegevens op uw apparaten.

Configureer schijfversleuteling als onderdeel van een apparaatconfiguratieprofiel voor Endpoint Protection. De volgende platforms en versleutelingstechnologieën worden ondersteund door Intune:

- macOS: FileVault
- Windows 10 en hoger: BitLocker

Intune biedt ook een ingebouwd [versleutelingsrapport](encryption-monitor.md) met informatie over de versleutelingsstatus van apparaten, voor alle beheerde apparaten.

## <a name="filevault-encryption-for-macos"></a>FileVault-versleuteling voor macOS

Gebruik Intune om FileVault-schijfversleuteling te configureren op apparaten waarop macOS wordt uitgevoerd. Gebruik vervolgens het Intune-versleutelingsrapport voor het weergeven van de versleutelingsgegevens voor deze apparaten en voor het beheren van herstelsleutels voor met FileVault versleutelde apparaten.

Door de gebruiker goedgekeurde apparaatinschrijving is vereist om FileVault op het apparaat te laten werken. De inschrijving geldt alleen als goedgekeurd door de gebruiker als deze het beheerprofiel handmatig goedkeurt vanuit de systeemvoorkeuren.

FileVault is een programma voor de versleuteling van volledige schijven. Het programma wordt geleverd bij macOS. U kunt Intune gebruiken om FileVault te configureren op apparaten waarop **macOS 10.13 of hoger** wordt uitgevoerd.

Als u FileVault wilt configureren, maakt u een [apparaatconfiguratieprofiel](../configuration/device-profile-create.md) voor Endpoint Protection voor het macOS-platform. De FileVault-instellingen vormen een eigen instellingencategorie in Endpoint Protection voor macOS.

Wanneer u een beleid hebt gemaakt voor het met FileVault versleutelen van apparaten, wordt het beleid in twee fasen toegepast op apparaten. In eerste instantie wordt het apparaat voorbereid zodat Intune kan worden gebruikt voor het ophalen van en het maken van back-ups van de herstelsleutel. Deze actie heet ook wel 'escrow'. Wanneer er een escrow-sleutel is gemaakt, kan worden gestart met de schijfversleuteling.

![FileVault-instellingen](./media/encrypt-devices/filevault-settings.png)

Voor meer informatie over de FileVault-instelling die u met Intune kunt beheren, ziet u [FileVault](endpoint-protection-macos.md#filevault) in het Intune-artikel over Endpoint Protection-instellingen voor macOS.

### <a name="permissions-to-manage-filevault"></a>Machtigingen voor het beheren van FileVault

Als u FileVault in Intune wilt beheren, moet uw account beschikken over de juiste machtigingen voor [op rollen gebaseerd toegangsbeheer](../fundamentals/role-based-access-control.md) (RBAC).

Hieronder vindt u de FileVault-machtigingen die deel uitmaken van de categorie **Externe taken** en de ingebouwde RBAC-rollen waarmee de machtiging wordt verleend:
 
- **De FileVault-sleutel ophalen**:
  - Helpdeskmedewerker
  - Endpoint Security Manager

- **FileVault-sleutel roteren**
  - Helpdeskmedewerker

### <a name="how-to-configure-macos-filevault"></a>FileVault voor macOS configureren

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Stel de volgende opties in:

   - Platform: macOS
   - Profieltype: Endpoint Protection

4. Selecteer **Instellingen** > **FileVault**.

5. Bij *FileVault* selecteert u **Inschakelen**.

6. Bij *Herstelsleuteltype* wordt alleen de optie **Persoonlijke sleutel** ondersteund.

   Overweeg een bericht toe te voegen om eindgebruikers te helpen bij het ophalen van de herstelsleutel voor hun apparaat. Deze informatie kan nuttig zijn voor uw eindgebruikers wanneer u de instelling voor wijziging van persoonlijke herstelsleutels gebruikt. Met deze instelling kan periodiek automatisch een nieuwe herstelsleutel voor een apparaat worden gegenereerd.

   Bijvoorbeeld: Als u een verloren of onlangs vernieuwde herstelsleutel wilt ophalen, meldt u zich aan op de website van de Intune-bedrijfsportal. Dit kan vanaf elk apparaat. Ga in de portal naar *Apparaten* en selecteer het apparaat waarvoor FileVault is ingeschakeld. Selecteer dan *Herstelsleutel ophalen*. De huidige herstelsleutel wordt weergegeven.

7. Configureer de overige [FileVault-instellingen](endpoint-protection-macos.md#filevault) zodanig dat er aan de vereisten van uw bedrijf wordt voldaan. Selecteer vervolgens **OK**.

  8. Voltooi de configuratie van de aanvullende instellingen en sla het profiel op.  

### <a name="manage-filevault"></a>FileVault beheren

Wanneer Intune een macOS-apparaat versleutelt met FileVault, kunt u de FileVault-herstelsleutels bekijken en beheren tijdens het bekijken van het Intune-[versleutelingsrapport](encryption-monitor.md).

Nadat Intune een macOS-apparaat versleutelt met FileVault, kunt u op elk apparaat de persoonlijke herstelsleutel van het apparaat bekijken in de online bedrijfsportal. Kies in de online bedrijfsportal het versleutelde macOS-apparaat en kies vervolgens 'Herstelsleutel ophalen' als externe actie.

### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices"></a>Persoonlijke herstelsleutel ophalen van met MEM versleutelde macOS-apparaten

Eindgebruikers kunnen hun persoonlijke herstelsleutel (FileVault-sleutel) ophalen met behulp van de iOS-bedrijfsportal-app, de Android-bedrijfsportal-app of via de Android Intune-app. Het apparaat met de persoonlijke herstelsleutel moet zijn geregistreerd bij Intune en moet zijn versleuteld met FileVault via Intune. Met de iOS-bedrijfsportal-app, Android-bedrijfsportal-app, de Android Intune-app of de Bedrijfsportal-website kunnen eindgebruikers de **FileVault**-herstelsleutel zien die nodig is om toegang te krijgen tot hun Mac-apparaten. Eindgebruikers kunnen **Apparaten** > *het versleutelde en ingeschreven macOS-apparaat* > **Herstelsleutel ophalen** selecteren. In de browser wordt de Webbedrijfsportal getoond waarin de herstelsleutel wordt weergegeven. 

## <a name="bitlocker-encryption-for-windows-10"></a>BitLocker-versleuteling voor Windows 10

Gebruik Intune om BitLocker-stationsversleuteling te configureren op apparaten waarop Windows 10 wordt uitgevoerd. Gebruik vervolgens het Intune-versleutelingsrapport om de versleutelingsgegevens voor deze apparaten te bekijken. U hebt ook toegang tot voor BitLocker belangrijke informatie over uw apparaten, zoals te zien is in Azure Active Directory (Azure AD).

BitLocker is beschikbaar op apparaten met **Windows 10 of hoger**.

Configureer BitLocker bij het maken van een [apparaatconfiguratieprofiel](../configuration/device-profile-create.md) voor Endpoint Protection in Windows 10 of op een nieuwer platform. De BitLocker-instellingen bevinden zich in de categorie Windows-versleutelingsinstellingen voor Windows 10 Endpoint Protection.

![BitLocker-instellingen](./media/encrypt-devices/bitlocker-settings.png)

### <a name="how-to-configure-windows-10-bitlocker"></a>BitLocker configureren voor Windows 10

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Stel de volgende opties in:

   - Platform: Windows 10 en hoger
   - Profieltype: Endpoint Protection

4. Selecteer **Instellingen** > **Windows-versleuteling**.

5. Configureer de instellingen van BitLocker zodat er aan de vereisten van uw bedrijf wordt voldaan. Selecteer dan **OK**.

6. Voltooi de configuratie van de aanvullende instellingen en sla het profiel op.

### <a name="silently-enable-bitlocker-on-devices"></a>BitLocker op de achtergrond inschakelen op apparaten

U kunt een BitLocker-beleid configureren waardoor BitLocker automatisch en op de achtergrond op een apparaat wordt geactiveerd. Dat houdt in dat BitLocker wordt ingeschakeld zonder dat eindgebruikers een gebruikersinterface te zien krijgen, zelfs wanneer die gebruiker geen lokale beheerder op het apparaat is.

**Apparaatvereisten**:

op een apparaat moet aan de volgende voorwaarden worden voldaan om in aanmerking te komen voor het op de achtergrond inschakelen van BitLocker:

- Op het apparaat moet Windows 10 versie 1809 of hoger worden uitgevoerd
- Het apparaat moet aan Azure AD zijn toegevoegd  

**BitLocker-beleidsconfiguratie**:

De volgende twee instellingen voor [BitLocker-basisinstellingen](../protect/endpoint-protection-windows-10.md#bitlocker-base-settings) moeten in het BitLocker-beleid zijn geconfigureerd:

- **Waarschuwing voor andere schijfversleuteling** = *Blokkeren*.
- **Standaardgebruikers toestaan om versleuteling in te schakelen tijdens Azure AD Join** = *Toestaan*

Via het BitLocker-beleid **mag niet worden vereist** dat er een opstartpincode of -sleutel wordt gebruikt. Wanneer een TPM-opstartpincode of -sleutel is *vereist*, kan BitLocker niet op de achtergrond worden ingeschakeld en is interactie van de eindgebruiker vereist.  Aan deze vereiste wordt voldaan door middel van de volgende drie [BitLocker-instellingen voor het besturingssysteemstation](../protect/endpoint-protection-windows-10.md#bitlocker-os-drive-settings) in hetzelfde beleid:

- **Compatibele TPM-opstartpincode** mag niet worden ingesteld op *Opstartpincode met TPM vereisen*
- **Compatibele TPM-opstartsleutel** mag niet worden ingesteld op *Opstartsleutel met TPM vereisen*
- **Compatibele opstartsleutel en -pincode voor TPM** mag niet worden ingesteld op *Opstartsleutel en -pincode met TPM vereisen*



### <a name="manage-bitlocker"></a>BitLocker beheren

Wanneer Intune een Windows 10-apparaat versleutelt met BitLocker, kunt u de BitLocker-herstelsleutels bekijken en ophalen tijdens het bekijken van het Intune-[versleutelingsrapport](encryption-monitor.md).

### <a name="rotate-bitlocker-recovery-keys"></a>BitLocker-herstelsleutels roteren

U kunt een Intune-apparaatactie gebruiken om de BitLocker-herstelsleutel van een apparaat met Windows 10 versie 1909 of hoger op afstand te roteren.

#### <a name="prerequisites"></a>Vereisten

Apparaten moeten voldoen aan de volgende vereisten om rotatie van de BitLocker-herstelsleutel te ondersteunen:

- Op de apparaten moet Windows 10 versie 1909 of hoger aanwezig zijn

- Op aan Azure AD gekoppelde apparaten en aan Hybrid gekoppelde apparaten moet ondersteuning voor het roteren van sleutels zijn ingeschakeld:

  - **Clientgestuurde rotatie van herstelwachtwoorden**

  Deze instelling vindt u onder *Windows-versleuteling* als onderdeel van een configuratiebeleid voor Endpoint Protection in Windows 10.
  
#### <a name="to-rotate-the-bitlocker-recovery-key"></a>De BitLocker-herstelsleutel roteren

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Alle apparaten**.

3. Selecteer een apparaat in de lijst met apparaten die u beheert, selecteer **Meer** en selecteer de externe apparaatactie **BitLocker-sleutelrotatie**.

## <a name="next-steps"></a>Volgende stappen

Een [nalevingsbeleid voor apparaten](compliance-policy-create-windows.md) maken.

U kunt op basis van het versleutelingsrapport de volgende zaken beheren:

- [BitLocker-herstelsleutels](encryption-monitor.md#bitlocker-recovery-keys)
- [FileVault-herstelsleutels](encryption-monitor.md#filevault-recovery-keys)

Bekijk welke versleutelingsinstellingen u met Intune kunt configureren voor:

- [BitLocker](endpoint-protection-windows-10.md#windows-encryption)
- [FileVault](endpoint-protection-macos.md#filevault)

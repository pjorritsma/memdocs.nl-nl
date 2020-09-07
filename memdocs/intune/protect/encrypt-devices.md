---
title: Windows 10-apparaten versleutelen met BitLocker in Intune
titleSuffix: Microsoft Intune
description: Versleutel apparaten met de ingebouwde versleutelingsmethode BitLocker en beheer de herstelsleutels voor deze versleutelde apparaten vanuit de Intune-portal.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 8843ab5c8bf3d0e6970398c1ad81a8a2b3b8f9cb
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193960"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>Het BitLocker-beleid voor Windows 10 in Intune beheren

Gebruik Intune om BitLocker-stationsversleuteling te configureren op apparaten waarop Windows 10 wordt uitgevoerd.

BitLocker is beschikbaar op apparaten met Windows 10 of hoger. Voor sommige instellingen van BitLocker moet het apparaat over een ondersteunde TPM beschikken.

Gebruik een van de volgende beleidstypen om BitLocker op uw beheerde apparaten te configureren

- **[Versleutelingsbeleid voor eindpuntbeveiligingsschijf voor Windows 10 BitLocker](#create-an-endpoint-security-policy-for-bitlocker)** . Het BitLocker-profiel in *eindpuntbeveiliging* is een gerichte groep instellingen die is toegewezen aan het configureren van BitLocker.

  Bekijk de BitLocker-instellingen die beschikbaar zijn in [de BitLocker-profielen van het schijfversleutelingsbeleid](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker).

- **[Configuratieprofiel van het apparaat voor eindpuntbescherming voor Windows 10 BitLocker](#create-an-endpoint-security-policy-for-bitlocker)** . De BitLocker-instellingen zijn een van de beschikbare instellingscategorieën voor Windows 10 eindpuntbescherming.

  Bekijk de BitLocker-instellingen die beschikbaar zijn voor [BitLocker in eindpuntbeschermingsprofielen op het formulier voor het apparaatconfiguratiebeleid](../protect/endpoint-protection-windows-10.md#windows-settings).

> [!TIP]
> Intune biedt een ingebouwd [versleutelingsrapport](encryption-monitor.md) met informatie over de versleutelingsstatus van al uw beheerde apparaten. Nadat Intune een Windows 10-apparaat met BitLocker heeft versleuteld, kunt u de BitLocker-herstelsleutels bekijken en ophalen wanneer u het versleutelingsrapport bekijkt.
>
> U hebt ook toegang tot voor BitLocker belangrijke informatie over uw apparaten, zoals te zien is in Azure Active Directory (Azure AD).
Een [versleutelingsrapport](encryption-monitor.md) met informatie over de versleutelingsstatus van apparaten, voor alle beheerde apparaten.

## <a name="permissions-to-manage-bitlocker"></a>Machtigingen voor het beheren van BitLocker

Als u BitLocker in Intune wilt beheren, moet uw account beschikken over de juiste Intune-machtigingen voor [op rollen gebaseerd toegangsbeheer](../fundamentals/role-based-access-control.md) (RBAC).

Hieronder vindt u de BitLocker-machtigingen die deel uitmaken van de categorie Externe taken en de ingebouwde RBAC-rollen waarmee de machtiging wordt verleend:

- **BitLocker-sleutels draaien**
  - Helpdeskmedewerker

## <a name="create-and-deploy-policy"></a>Beleid opstellen en implementeren

Gebruik een van de volgende procedures om het gewenste beleidstype op te stellen.

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>Een eindpuntbeveiligingsbeleid voor BitLocker opstellen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Eindpuntbeveiliging** > **Schijfversleuteling** > **Beleid maken**.

3. Stel de volgende opties in:
   1. **Platform**: Windows 10 of hoger
   2. **Profiel**: BitLocker

   ![Het BitLocker-profiel selecteren](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. Configureer de instellingen van BitLocker op de pagina **Configuratie-instellingen** zodat aan de vereisten van uw bedrijf wordt voldaan.  

   Als u BitLocker op de achtergrond wilt inschakelen, raadpleegt u [BitLocker op de achtergrond inschakelen op apparaten](#silently-enable-bitlocker-on-devices) voor aanvullende vereisten en de specifieke instellingsconfiguraties die u moet gebruiken.

   Selecteer **Volgende**.

5. Selecteer op de pagina **Bereik (tags)** de optie **Bereiktags selecteren** om het deelvenster Tags selecteren te openen en bereiktags aan het profiel toe te wijzen.

   Selecteer **Volgende** om door te gaan.

6. Selecteer op de pagina **Toewijzingen** de groepen die dit profiel zullen ontvangen. Zie Gebruikers- en apparaatprofielen toewijzen voor meer informatie over het toewijzen van profielen.

   Selecteer **Volgende**.

7. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>Een apparaatconfiguratieprofiel voor BitLocker aanmaken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Stel de volgende opties in:
   1. **Platform**: Windows 10 en hoger
   2. **Profieltype**: Endpoint Protection

   ![Het profiel selecteren](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. Selecteer **Instellingen** > **Windows-versleuteling**.

   ![BitLocker-instellingen](./media/encrypt-devices/bitlocker-settings.png)

5. Configureer de instellingen van BitLocker zodat aan de vereisten van uw bedrijf wordt voldaan.

   Als u BitLocker op de achtergrond wilt inschakelen, raadpleegt u [BitLocker op de achtergrond inschakelen op apparaten](#silently-enable-bitlocker-on-devices) voor aanvullende vereisten en de specifieke instellingsconfiguraties die u moet gebruiken.

6. Selecteer **OK**.

7. Voltooi de configuratie van de aanvullende instellingen en sla het profiel op.

## <a name="manage-bitlocker"></a>BitLocker beheren

Zie [Schijfversleuteling controleren](../protect/encryption-monitor.md) voor informatie over apparaten die het BitLocker-beleid ontvangen. U kunt de BitLocker-herstelsleutels ook bekijken en ophalen wanneer u het versleutelingsrapport bekijkt.

### <a name="silently-enable-bitlocker-on-devices"></a>BitLocker op de achtergrond inschakelen op apparaten

U kunt een BitLocker-beleid configureren waardoor BitLocker automatisch en op de achtergrond op een apparaat wordt geactiveerd. Dat houdt in dat BitLocker wordt ingeschakeld zonder dat eindgebruikers een gebruikersinterface te zien krijgen, zelfs wanneer die gebruikers geen lokale beheerders op het apparaat zijn.

**Apparaatvereisten**:

op een apparaat moet aan de volgende voorwaarden worden voldaan om in aanmerking te komen voor het op de achtergrond inschakelen van BitLocker:

- Als eindgebruikers zich bij de apparaten aanmelden als Beheerder, moet Windows 10 versie 1803 of hoger op het apparaat worden uitgevoerd.
- Als eindgebruikers zich bij de apparaten aanmelden als Standaardgebruiker, moet Windows 10 versie 1809 of hoger op het apparaat worden uitgevoerd.
- Het apparaat moet aan Azure AD zijn toegevoegd  

**BitLocker-beleidsconfiguratie**:

De volgende twee instellingen voor *BitLocker-basisinstellingen* moeten in het BitLocker-beleid zijn geconfigureerd:

- **Waarschuwing voor andere schijfversleuteling** = *Blokkeren*.
- **Standaardgebruikers toestaan om versleuteling in te schakelen tijdens Azure AD Join** = *Toestaan*

Via het BitLocker-beleid **mag niet worden vereist** dat er een opstartpincode of -sleutel wordt gebruikt. Wanneer een TPM-opstartpincode of -sleutel is *vereist*, kan BitLocker niet op de achtergrond worden ingeschakeld en is interactie van de eindgebruiker vereist.  Aan deze vereiste wordt voldaan door middel van de volgende drie *BitLocker-instellingen voor het besturingssysteemstation* in hetzelfde beleid:

- **Compatibele TPM-opstartpincode** mag niet worden ingesteld op *Opstartpincode met TPM vereisen*
- **Compatibele TPM-opstartsleutel** mag niet worden ingesteld op *Opstartsleutel met TPM vereisen*
- **Compatibele opstartsleutel en -pincode voor TPM** mag niet worden ingesteld op *Opstartsleutel en -pincode met TPM vereisen*

### <a name="view-details-for-recovery-keys"></a>Details weergeven voor herstelsleutels

Intune biedt toegang tot de Microsoft Azure Active Directory-blade voor BitLocker, zodat u via de Intune-portal BitLocker-sleutel-id's en herstelsleutels voor uw Windows 10-apparaten kunt weergeven. Een apparaat is alleen toegankelijk als de sleutels van dat apparaat naar Azure AD worden geborgd.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Alle apparaten**.

3. Selecteer een apparaat in de lijst en selecteer vervolgens onder *Monitor* **Herstelsleutels**.
  
   Als er sleutels in Azure AD beschikbaar zijn, is de volgende informatie beschikbaar:
   - BitLocker-sleutel-id
   - BitLocker-herstelsleutel
   - Type station

   Als er geen sleutels aanwezig zijn in Azure AD, wordt *Er is geen BitLocker-sleutel gevonden voor dit apparaat* weergegeven.

De informatie voor BitLocker wordt verkregen met behulp van de [BitLocker-configuratieserviceprovider](/windows/client-management/mdm/bitlocker-csp) (CSP). BitLocker CSP wordt ondersteund op Windows 10-versie 1703 en hoger en voor Windows 10 Pro-versie 1809 en hoger.

### <a name="rotate-bitlocker-recovery-keys"></a>BitLocker-herstelsleutels roteren

U kunt een Intune-apparaatactie gebruiken om de BitLocker-herstelsleutel van een apparaat met Windows 10 versie 1909 of hoger op afstand te roteren.

#### <a name="prerequisites"></a>Vereisten

Apparaten moeten voldoen aan de volgende vereisten om rotatie van de BitLocker-herstelsleutel te ondersteunen:

- Op de apparaten moet Windows 10 versie 1909 of hoger aanwezig zijn

- Op aan Azure AD gekoppelde apparaten en hybride gekoppelde apparaten moet ondersteuning voor het roteren van sleutels zijn ingeschakeld via configuratie van BitLocker-beleid:

  - **Clientgestuurde rotatie van herstelwachtwoorden** moet zijn ingesteld op *Rotatie inschakelen op apparaten die zijn toegevoegd aan Azure AD* of *Rotatie inschakelen op apparaten die zijn toegevoegd aan Azure AD en op hybride apparaten*
  - **BitLocker-herstelgegevens opslaan in Azure Active Directory** moet zijn ingesteld op *Ingeschakeld*
  - **Herstelgegevens opslaan in Azure Active Directory voordat BitLocker wordt ingeschakeld**moet zijn ingesteld op *Vereist*

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>De BitLocker-herstelsleutel roteren

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Alle apparaten**.

3. Selecteer een apparaat in de lijst met apparaten die u beheert, selecteer **Meer** en selecteer de externe apparaatactie **BitLocker-sleutelrotatie**.

4. Selecteer op de pagina **Overzicht** van het apparaat de optie **BitLocker-sleutelrotatie**. Als deze optie niet wordt weergegeven, selecteert u het weglatingsteken ( **...** ) om extra opties weer te geven en vervolgens selecteert u de externe apparaatactie **BitLocker-sleutelrotatie**.

   ![Het weglatingsteken selecteren om meer opties weer te geven](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>Volgende stappen

[FileVault-beleid beheren](../protect/encrypt-devices-filevault.md)

[Schijfversleuteling controleren](../protect/encryption-monitor.md)

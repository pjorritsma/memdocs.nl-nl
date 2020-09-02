---
title: Windows Defender-toepassingsbeheer op HoloLens 2-apparaten gebruiken in Microsoft Intune-Azure | Microsoft Docs
description: Configureer de Windows Defender Application Control (WDAC) CSP om te voorkomen dat apps kunnen worden geopend op Windows-apparaten met HoloLens 2 in Microsoft Intune. Gebruik PowerShell en een aangepast configuratieprofiel.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4a1929749c5921714078ec54ac687f4cefe1474
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915871"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>Gebruik WDAC en Windows PowerShell om apps op HoloLens 2-apparaten met Microsoft Intune toe te staan of te blokkeren

Microsoft HoloLens 2-apparaten ondersteunen de [Windows Defender Application Control (WDAC)-CSP](/windows/client-management/mdm/applicationcontrol-csp), waarmee de [AppLocker CSP](/windows/client-management/mdm/applocker-csp) wordt vervangen.

Met Windows PowerShell en Microsoft Intune kunt u de WDAC-CSP gebruiken om specifieke apps toe te staan of te blokkeren voor het openen van Microsoft HoloLens 2-apparaten. U kunt bijvoorbeeld toestaan of voorkomen dat de Cortana-app wordt geopend op apparaten van HoloLens 2 in uw organisatie.

Deze functie is van toepassing op:

- HoloLens 2-apparaten met Windows Holographic for Business

De WDAC-CSP is gebaseerd op de [functie Windows Defender Application Control (WDAC)](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). U kunt ook meerdere [WDAC-beleidsregels gebruiken](/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

In dit artikel leest u informatie over:

1. Windows PowerShell gebruiken om WDAC-beleid te maken.
2. Gebruik Windows PowerShell om de WDAC-beleidsregels te converteren naar XML, de XML bij te werken en de XML vervolgens te converteren naar een binair bestand.
3. Maak in Microsoft Intune een [aangepast configuratieprofiel voor het apparaat](custom-settings-windows-holographic.md), voeg dit binaire bestand voor het WDAC-beleid toe en pas het beleid toe op uw HoloLens 2-apparaten.

In Intune moet u een aangepast configuratieprofiel maken om de Windows Defender Application Control (WDAC)-CSP te gebruiken. 

Gebruik de stappen in dit artikel als sjabloon voor het toestaan of weigeren van specifieke apps op HoloLens 2-apparaten.

## <a name="prerequisites"></a>Vereisten

- Bekend zijn met Windows PowerShell.
- Meld u aan bij Intune als lid van:

  - Intune-rol **Beleids- en Profielbeheerder** of **Intune-rolbeheerder**

    OF

  - De Azure AD-rollen **Globale beheerder** of **Intune-servicebeheerder**

  Meer informatie in [Op rollen gebaseerd toegangsbeheer (RBAC) met Intune](../fundamentals/role-based-access-control.md).

- Maak een gebruikersgroep of apparatengroep met uw HoloLens 2-apparaten. Zie [Gebruikersgroepen versus apparaatgroepen](device-profile-assign.md#user-groups-vs-device-groups) voor meer informatie.

## <a name="example"></a>Voorbeeld

In dit voorbeeld wordt Windows PoweShell gebruikt om een beleid voor Windows Defender Application Control (WDAC) te maken. Met het beleid wordt voorkomen dat specifieke apps worden geopend. Vervolgens kunt u Intune gebruiken om het beleid te implementeren op HoloLens 2-apparaten.

1. Open de **Windows PowerShell**-app op uw desktopcomputer.
2. Informatie over het geïnstalleerde toepassingspakket op uw desktopcomputer:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    Voer bijvoorbeeld het volgende in:

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    Bevestig vervolgens dat het pakket toepassingskenmerken heeft:

    ```powershell
    $package1
    ```

    U ziet kenmerken die vergelijkbaar zijn met de volgende app-details:

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. Maak een WDAC-beleid en voeg het app-pakket toe aan de regel voor WEIGEREN:

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. Herhaal stap 2 en 3 voor alle andere toepassingen die u wilt weigeren:

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    Voer bijvoorbeeld het volgende in:

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. Converteer het WDAC-beleid naar **newPolicy.xml**:

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    Als u alle versies van een app wilt targeten, in newPolicy.xml of zorg dat `PackageVersion="65535.65535.65535.65535"` zich in het knooppunt Weigeren bevindt:

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    U kunt voor `PackageFamilyNameRules` de volgende versies gebruiken:

    - **Toestaan**: Voer `PackageVersion, 0.0.0.0` in, wat betekent dat "deze versie en hoger wordt toegestaan".
    - **Weigeren**: Voer `PackageVersion, 65535.65535.65535.65535` in, wat betekent dat deze versie en lager worden geweigerd.

6. **newPolicy.xml samenvoegen** met het standaardbeleid dat op uw desktopcomputer is ingesteld. Met deze stap maakt u **mergedPolicy.xml**. U kunt bijvoorbeeld de Windows, WHQ- ondertekende stuurprogramma's toestaan en ondertekende Apps opslaan om uit te voeren:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Schakel de **Controlemodus**-regel uit in **mergedPolicy.xml**. Wanneer u alles samenvoegt, wordt de controlemodus automatisch ingeschakeld:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. Schakel de regel **InvalidateEA’s bij opnieuw opstarten** in bij **mergedPolicy.xml**:

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    Zie [Meer informatie over WDAC-beleidsregels en -bestandsregels](/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create) voor meer informatie over deze regels.

9. Converteer **mergedPolicy.xml** naar een binaire indeling. Met deze stap maakt u **compiledPolicy.bin**. U voegt dit binaire bestand **compiledPolicy.bin** toe aan Intune.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Maak in Intune een aangepast apparaatconfiguratieprofiel:

    1. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431), maak een aangepast Windows 10-apparaatconfiguratieprofiel.

        Zie [Een aangepast profiel maken met behulp van OMA-URI in Intune](custom-settings-configure.md) voor de specifieke stappen.

    2. Wanneer u het profiel maakt, voert u de volgende instellingen in:

      - **OMA-URI**: Voer `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>` in. Vervang `<PolicyGUID>` door het PolicyTypeID-knooppunt in het bestand **mergedPolicy.xml** dat u in stap 6 hebt gemaakt.

        Voer bijvoorbeeld `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076` in.

        De beleids-GUID **moet overeenkomen met** het knooppunt PolicyTypeID in het bestand **mergedPolicy.xml** (gemaakt in stap 6).

      - **Gegevenstype**: Instellen op **Base64-bestand**. Het bestand wordt automatisch geconverteerd van bin naar base64.
      - **Certificaatbestand**: Upload het binaire bestand **compiledPolicy.bin** dat u hebt gemaakt in stap 9.

      Uw instellingen zien er ongeveer uit zoals de volgende:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Voeg een aangepaste OMA-URI toe om ApplicationControl CSP in Microsoft Intune te configureren.":::

11. Controleer de profielstatus wanneer het profiel wordt [toegewezen](device-profile-assign.md) aan uw HoloLens 2-groep. Nadat het profiel is toegepast, start u de HoloLens 2-apparaten opnieuw op.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

[Meer informatie over aangepaste profielen in Intune](custom-settings-configure.md).
---
title: Apparaatprofielen maken in Microsoft Intune - Azure | Microsoft Docs
description: Voeg een apparaatconfiguratieprofiel toe in Microsoft Intune of configureer er een. Selecteer het platformtype, configureer de instellingen en voeg een bereiktag toe.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bd1cb0445ceb4c9434b93949973125422aa1df19
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146419"
---
# <a name="create-a-device-profile-in-microsoft-intune"></a>Een apparaatprofiel maken in Microsoft Intune

Met apparaatprofielen kunt u instellingen toevoegen en configureren, en deze instellingen vervolgens naar apparaten in uw organisatie pushen. Raadpleeg [Functies en instellingen toepassen op uw apparaten met apparaatprofielen](device-profiles.md) voor meer informatie ondaer andere over wat u allemaal kunt doen.

Dit artikel:

- Laat zien welke stappen nodig zijn voor het maken van een profiel.
- Laat u zien hoe u een bereiktag kunt toevoegen om het profiel te filteren.
- Beschrijft de regels voor toepasselijkheid op Windows 10-apparaten en laat zien hoe u een regel kunt maken.
- Geeft de cyclusduur voor vernieuwen van check-ins weer wanneer apparaten profielen ontvangen en bij eventuele profielupdates.

## <a name="create-the-profile"></a>Het profiel maken

Profielen worden gemaakt in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431). Selecteer **Apparaten**in dit beheercentrum. U hebt de volgende opties:

- **Overzicht**: geeft de status van uw profielen weer en biedt aanvullende details over de profielen die u aan gebruikers en apparaten hebt toegewezen.
- **Bewaken**: Controleer de status van uw profielen op slagen of falen en bekijk ook logboeken over uw profielen.
- **Op platform**: Maak beleidsregels en profielen op basis van uw platform. In deze weergave kunnen ook specifieke functies voor het platform worden weergegeven. Selecteer bijvoorbeeld **Windows**. U ziet Windows-specifieke functies, zoals **Windows 10-update-ringen** en **PowerShell-scripts**.
- **Beleid**: Maak apparaatprofielen en upload aangepaste [PowerShell-scripts](../apps/intune-management-extension.md) die op apparaten worden uitgevoerd, en voeg met [eSIM](esim-device-configuration.md) gegevensplannen toe aan apparaten.

Wanneer u een profiel maakt (**Configuratieprofielen** > **Profiel maken**), kiest u uw platform:

- **Android-apparaatbeheerder**
- **Android Enterprise**
- **iOS/iPadOS**
- **macOS**
- **Windows 10 en hoger**
- **Windows 8.1 en hoger**

Kies vervolgens het profieltype. Welke instellingen u kunt configureren, is afhankelijk van het platform dat u kiest. In de volgende artikelen worden de instellingen voor de verschillende profieltypen beschreven:

- [Beheersjablonen (Windows)](administrative-templates-windows.md)
- [Aangepast](custom-settings-configure.md)
- [Delivery Optimization (Windows)](delivery-optimization-windows.md)
- [Afgeleide referentie (Android Enterprise, iOS, iPadOS)](../protect/derived-credentials.md)
- [Apparaatfuncties (macOS, iOS, iPadOS)](device-features-configure.md)
- [Apparaatfirmware (Windows)](device-firmware-configuration-interface-windows.md)
- [Apparaatbeperkingen](device-restrictions-configure.md)
- [Domeindeelname (Windows)](domain-join-configure.md)
- [Editie-upgrade en modusschakelaar (Windows)](edition-upgrade-configure-windows-10.md)
- [Onderwijs (iOS, iPadOS)](../fundamentals/education-settings-configure-ios.md)
- [E-mail](email-settings-configure.md)
- [Endpoint Protection (macOS, Windows)](../protect/endpoint-protection-configure.md)
- [Extensies (macOS)](kernel-extensions-overview-macos.md)
- [Identiteitsbescherming (Windows)](../protect/identity-protection-configure.md)
- [Kiosk](kiosk-settings.md)
- [Microsoft Defender ATP (Windows)](../protect/advanced-threat-protection.md)
- [Mobiliteitsextensiesprofiel (MX, Android-apparaatbeheer)](android-zebra-mx-overview.md)
- [OEMConfig (Android Enterprise)](android-oem-configuration-overview.md)
- [PKCS-certificaat](../protect/certficates-pfx-configure.md)
- [PKCS-geïmporteerd certificaat](../protect/certificates-imported-pfx-configure.md)
- [Voorkeursbestand (macOS)](preference-file-settings-macos.md)
- [SCEP-certificaat](../protect/certificates-scep-configure.md)
- [Veilige evaluatie (onderwijs) (Windows)](education-settings-configure.md)
- [Gedeeld apparaat voor meerdere gebruikers (Windows)](shared-user-device-settings.md)
- [Telecommunicatie-uitgaven (Android-apparaatbeheerder, iOS, iPadOS)](telecom-expenses-monitor.md)
- [Vertrouwd certificaat](../protect/certificates-configure.md)
- [VPN](vpn-settings-configure.md)
- [Wi-Fi](wi-fi-settings-configure.md)
- [Bedrade netwerken (macOS)](wired-network-settings-macos.md)

Als u bijvoorbeeld **iOS/iPadOS** als platform selecteert, lijken uw profielopties op het volgende profiel:

:::image type="content" source="./media/device-profile-create/create-device-profile.png" alt-text="Een iOS-/iPadOS-profiel in Microsoft Intune maken.":::

## <a name="scope-tags"></a>Bereiktags

Nadat u de instellingen hebt toegevoegd, kunt u ook een bereiktag toevoegen aan het profiel. Met bereiktags worden profielen gefilterd op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Ze worden ook gebruikt in de gedistribueerde IT.

Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags en wat u hiermee kunt doen.

## <a name="applicability-rules"></a>Toepasselijkheidsregels

Van toepassing op:

- Windows 10 en hoger

Met regels voor toepasselijkheid kunnen beheerders doelapparaten instellen in een groep die aan bepaalde criteria voldoet. U maakt bijvoorbeeld een profiel voor beperkingen voor apparaten dat van toepassing is op de groep **Alle Windows 10-apparaten**. En u wilt het profiel alleen toewijzen aan apparaten met Windows 10 Enterprise.

Hiertoe maakt u een **regel voor toepasselijkheid**. Deze regels zijn handig voor de volgende scenario's:

- U gebruikt Windows 10 Education (EDU). Bij Bellows College wilt u alle Windows 10 EDU-apparaten tussen RS3 en RS4 instellen als doel.
- U wilt alle gebruikers in HR op Contoso instellen, maar alleen Windows 10 Professional- of Enterprise-apparaten.

In deze scenario's doet u het volgende:

- Maak een groep apparaten die alle apparaten bij Bellows College omvat. Voeg in het profiel een regel voor toepasselijkheid toe die van toepassing is als de minimumversie van het besturingssysteem `16299` is en de maximumversie `17134` is. Wijs dit profiel toe aan de groep Bellows College-apparaten.

  Wanneer deze is toegewezen, is het profiel van toepassing op apparaten tussen de minimum- en maximumversie die u opgeeft. Apparaten waarvan de versie niet tussen de door u ingevoerde minimum- en maximumversie ligt, hebben de status **Niet van toepassing**.

- Maak een gebruikersgroep met alle gebruikers in Human Resources (HR) bij Contoso. Voeg in het profiel een regel voor toepasselijkheid toe die van toepassing is op apparaten met Windows 10 Professional of Enterprise. Wijs dit profiel toe aan de HR-gebruikersgroep.

  Na de toewijzing is het profiel van toepassing op apparaten met Windows 10 Professional of Enterprise. Apparaten met een andere editie dan deze hebben de status **Niet van toepassing**.

- Als er twee profielen zijn met exact dezelfde instellingen, wordt het profiel zonder een regel voor toepasselijkheid toegepast. 

  Profiel A heeft bijvoorbeeld als doel de groep Windows 10-apparaten, schakelt BitLocker in en heeft geen regel voor toepasselijkheid. Profiel B heeft als doel dezelfde groep Windows 10-apparaten, schakelt BitLocker in, en heeft een regel voor toepasselijkheid om het profiel alleen toe te passen op Windows 10 Enterprise.

  Wanneer beide profielen worden toegewezen, wordt profiel A toegepast omdat dat profiel geen regel voor toepasselijkheid heeft. 

Wanneer u het profiel aan de groepen toewijst, fungeren de regels voor toepasselijkheid als filters en worden ze alleen toegepast op de apparaten die voldoen aan uw criteria.

### <a name="add-a-rule"></a>Een regel toevoegen

1. Selecteer **Regels voor toepasselijkheid**. U kunt de **Regel** en **Eigenschap** kiezen:

    :::image type="content" source="./media/device-profile-create/applicability-rules.png" alt-text="Voeg een toepasselijkheidsregel aan een configuratieprofiel voor Windows 10-apparaten toe in Microsoft Intune.":::

2. Kies in **Regel** of u gebruikers of groepen wilt opnemen of uitsluiten. Uw opties zijn:

    - **Profiel toewijzen als**: hiermee kunt u gebruikers of groepen opnemen die voldoen aan de criteria die u invoert.
    - **Profiel niet toewijzen als**: hiermee kunt u gebruikers of groepen uitsluiten die voldoen aan de criteria die u invoert.

3. Kies in **Eigenschap** het gewenste filter. Uw opties zijn: 

    - **Editie van het besturingssysteem**: Selecteer in de lijst de Windows 10-edities die u in de regel wilt opnemen (of uitsluiten).
    - **Versie van het besturingssysteem**: Voer het **minimum** en **maximum** in voor de Windows 10-versienummers die u met de regel wilt opnemen (of uitsluiten). Beide waarden zijn vereist.

      U kunt bijvoorbeeld `10.0.16299.0` (RS3 of 1709) invoeren voor de minimumversie en `10.0.17134.0` (RS4 of 1803) voor de maximumversie. U kunt ook specifieke waarden opgeven, zoals `10.0.16299.001` voor de minimumversie en `10.0.17134.319` voor de maximumversie.

4. Selecteer **Toevoegen** om uw wijzigingen op te slaan.

## <a name="refresh-cycle-times"></a>Cyclusduur vernieuwen

In Intune worden verschillende vernieuwingscycli gebruikt om te controleren op updates voor configuratieprofielen. Als het apparaat onlangs is ingeschreven, worden de check-ins vaker uitgevoerd. In [Vernieuwingscycli voor beleidsregels en profielen](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) worden de geschatte vernieuwingstijden vermeld.

Gebruikers kunnen ook de bedrijfsportal-app openen en het apparaat synchroniseren om op elk gewenst moment op aanwezig beleid te controleren.

## <a name="recommendations"></a>Aanbevelingen

Houd bij het maken van profielen rekening met de volgende aanbevelingen:

- Geef elk beleid een naam zodat u weet wat het is en wat het doet. Elk [nalevingsbeleid](../protect/create-compliance-policy.md) en alle [configuratieprofielen](../configuration/device-profile-create.md) hebben een optionele eigenschap **Beschrijving**. Wees specifiek bij het opgeven van de **beschrijving**, zodat anderen weten wat het beleid doet.

  Enkele voorbeelden van configuratieprofielen zijn:

  **Profielnaam**: Beheersjabloon - OneDrive-configuratieprofiel voor alle Windows 10-gebruikers  
  **Profielbeschrijving**: sjabloonprofiel van de OneDrive-beheerder met de minimale en de basisinstellingen voor alle Windows 10-gebruikers. Gemaakt door user@contoso.com om te voorkomen dat gebruikers organisatiegegevens delen met persoonlijke OneDrive-accounts.

  **Profielnaam**: VPN-profiel voor alle iOS-/iPadOS-gebruikers  
  **Profielbeschrijving**: VPN-profiel met de minimale en basisinstellingen voor alle iOS-/iPadOS-gebruikers om verbinding te maken met Contoso VPN. Gemaakt door user@contoso.com, zodat gebruikers automatisch worden geverifieerd voor VPN, in plaats van gebruikers te vragen om hun gebruikersnaam en wachtwoord op te geven.

- Maak uw profiel op basis van de bijbehorende taak, zoals Microsoft Edge-instellingen configureren, Microsoft Defender-antivirusinstellingen inschakelen, opengebroken iOS-/iPadOS-apparaten blokkeren enzovoort.

- Maak profielen die van toepassing zijn op specifieke groepen, zoals Marketing, Verkoop, IT-beheerders, of op locatie of schoolsysteem.

- Gebruikersbeleid gescheiden houden van apparaatbeleid.

  [Beheersjablonen in Intune](administrative-templates-windows.md) bevatten bijvoorbeeld duizenden ADMX-instellingen. Deze sjablonen tonen of een instelling van toepassing is op gebruikers of op apparaten. Als u beheersjablonen maakt, wijst u de gebruikersinstellingen toe aan een gebruikersgroep en wijst u de apparaatinstellingen toe aan een apparaatgroep.

  In de volgende afbeelding ziet u een voorbeeld van een instelling die kan worden toegepast op gebruikers en/of apparaten:

  :::image type="content" source="./media/device-profile-create/setting-applies-to-user-and-device.png" alt-text="Intune-beheersjabloon die van toepassing is op gebruikers en apparaten.":::

- Informeer uw gebruikers bij elk restrictief beleid dat u maakt over de wijziging. Als u bijvoorbeeld de wachtwoordvereiste wijzigt van vier (4) tekens in zes (6) tekens, laat dit dan aan uw gebruikers weten voordat u het beleid toewijst.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

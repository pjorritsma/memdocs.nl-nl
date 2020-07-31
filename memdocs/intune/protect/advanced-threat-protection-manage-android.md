---
title: Microsoft Defender ATP-webbeveiliging voor Android-apparaten beheren in Microsoft Intune - Azure | Microsoft Docs
description: Microsoft Defender Advanced Threat Protection-webbeveiliging (Microsoft Defender ATP) voor Android configureren in Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1e3b12251117e689f3b4a5456cf20bae3797083a
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264517"
---
# <a name="configure-microsoft-defender-atp-on-android-devices-you-manage-with-intune"></a>Microsoft Defender ATP configureren op Android-apparaten die u beheert met Intune

Wanneer u Microsoft Intune en Microsoft Defender Advanced Threat Protection (ATP) integreert, kunt u configuratieprofielen voor apparaten gebruiken om bepaalde instellingen van Microsoft Defender ATP op Android-apparaten te wijzigen.

Voordat u verder gaat, moet u [Microsoft Defender ATP in Intune configureren](../protect/advanced-threat-protection-configure.md) en Android-apparaten onboarden naar Microsoft Defender ATP.

## <a name="configure-web-protection-on-devices-that-run-android"></a>Webbeveiliging configureren op apparaten met Android

Microsoft Defender ATP voor Android bevat standaard het onderdeel webbeveiliging en schakelt dit in. [Webbeveiliging](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) helpt bij het beveiligen van apparaten tegen webbedreigingen en beschermt gebruikers tegen phishing-aanvallen.

Hoewel deze optie standaard is ingeschakeld, zijn er geldige redenen om deze beveiliging op sommige Android-apparaten uit te schakelen. U kunt er bijvoorbeeld voor kiezen om alleen de scanfunctie van de Microsoft Defender ATP-app te gebruiken of om te voorkomen dat webbeveiliging gebruikmaakt van uw VPN tijdens het scannen op schadelijke URL's.

Intune ondersteunt het uitschakelen van de gehele of gedeeltelijke webbeveiligingsfunctie. De methode die u gebruikt en de mogelijkheden die u kunt uitschakelen, zijn afhankelijk van hoe het Android-apparaat is ingeschreven bij Intune:

- **Android-apparaatbeheerder**: Gebruik een configuratieprofiel om aangepaste OMA-URI-instellingen op het apparaat in te stellen om de gehele webbeveiligingsfunctie uit te schakelen of alleen het gebruik van VPN's uit te schakelen. Zie voor algemene informatie over aangepaste instellingen voor Android-toestellen [Aangepaste instellingen](../configuration/custom-settings-android.md).

- **Werkprofiel voor Android Enterprise**: Gebruik een app-configuratieprofiel en de *configuratieontwerper* om webbeveiliging uit te schakelen. Deze methode en het inschrijvingstype ondersteunen het uitschakelen van alle webbeveiligingsopties, maar ondersteunen niet het uitschakelen van alleen het gebruik van VPN's. Zie [De configuratieontwerper gebruiken](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer) voor algemene informatie over app-configuratiebeleidsregels.

Als u webbeveiliging op apparaten wilt configureren, gebruikt u de volgende procedures om de toepasselijke configuratie te maken en te implementeren.

### <a name="disable-web-protection-for-android-device-administrator"></a>Webbeveiliging voor Android-apparaatbeheerder uitschakelen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Voer de volgende instellingen in:

   - **Platform**: Selecteer **Android-apparaatbeheerder**
   - **Profiel**: Selecteer **Aangepast**

   Selecteer **Maken**.

4. Voer de volgende gegevens in onder **Basisinformatie**:

   - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Bijvoorbeeld *aangepast Android-profiel voor Microsoft Defender ATP-webbeveiliging*
   - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

5. Selecteer in **Configuratie-instellingen** de optie **Toevoegen**.

   Geef de instellingen op voor de configuratie die u wilt implementeren:

   - **Webbeveiliging uitschakelen**:
     - **Naam**: Voer een unieke naam in voor deze OMA-URI-instelling, zodat u deze gemakkelijk kunt vinden. Bijvoorbeeld *Microsoft Defender ATP-webbeveiliging uitschakelen*
     - **Beschrijving**: (Optioneel) Voer een beschrijving in met een overzicht van de instelling en eventuele andere belangrijke details.
     - **OMA-URI**: Voer **./Vendor/MSFT/DefenderATP/AntiPhishing** in
     - **Gegevenstype**: Selecteer in de vervolgkeuzelijst **Geheel getal**
     - **Waarde**: Voer **0** in om webbeveiliging uit te schakelen, inclusief de op VPN gebaseerde scan.
       > [!NOTE]
       > Voer **1** in om webbeveiliging in te schakelen. Dit is de standaardinstelling voor webbeveiliging.

   - **Schakel alleen het gebruik van VPN via webbeveiliging uit**:
     - **Naam**: Voer een unieke naam in voor deze OMA-URI-instelling, zodat u deze gemakkelijk kunt vinden. Bijvoorbeeld *Microsoft Defender ATP-webbeveiliging VPN uitschakelen*
     - **Beschrijving**: (Optioneel) Voer een beschrijving in met een overzicht van de instelling en eventuele andere belangrijke details.
     - **OMA-URI**: Voer **./Vendor/MSFT/DefenderATP/Vpn** in
     - **Gegevenstype**: Selecteer in de vervolgkeuzelijst **Geheel getal**
     - **Waarde**: Voer **0** in om de op VPN gebaseerde scan uit te schakelen.
       > [!NOTE]
       > Voer **1** in om webbeveiliging in te schakelen. Dit is de standaardinstelling voor webbeveiliging.

   Selecteer **Toevoegen** om de configuratie van de OMA-URI-instellingen op te slaan en selecteer vervolgens **Volgende** om door te gaan.

6. Geef op de pagina **Toewijzingen** de groepen op die dit profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

7. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Webbeveiliging voor Android Enterprise-werkprofiel uitschakelen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apps** > **App-configuratiebeleid** > **Toevoegen** en Beheerde apparaten.

3. Voer de volgende gegevens in onder **Basisinformatie**:

   - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Bijvoorbeeld *Android-app-configuratie voor Microsoft Defender ATP-webbeveiliging*.
   - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.
   - **Platform**: Selecteer **Android Enterprise**
   - **Profieltype**: Selecteer **Alleen werkprofiel**
   - **Beoogde app**: Klik op **App selecteren**.

4. Zoek onder **Gekoppelde app** en selecteer **Defender ATP** en klik op **OK** > **Volgende**.

5. Selecteer onder **Instellingen** in de vervolgkeuzelijst **Indeling van de configuratie-instellingen** de optie **Configuratieontwerper gebruiken** en klik op **Toevoegen**. De JSON-editor wordt geopend.

6. Zoek en selecteer **Webbeveiliging** en selecteer **OK** om terug te gaan naar de pagina **Instellingen**.

7. Voer voor de **configuratiewaarde** **0** in om webbeveiliging uit te schakelen.

   > [!NOTE]
   > Voer **1** in om webbeveiliging in te schakelen. Dit is de standaardinstelling voor webbeveiliging.

   Selecteer **Volgende** om door te gaan.

8. Geef op de pagina **Toewijzingen** de groepen op die dit profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

9. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

## <a name="next-steps"></a>Volgende stappen

- [Naleving van risiconiveaus bewaken](../protect/advanced-threat-protection-monitor.md)
- [Beveiligingstaken gebruiken in combinatie met kwetsbaarheidsbeheer in ATP om problemen op apparaten op te lossen](../protect/atp-manage-vulnerabilities.md)

Meer informatie vindt u in de Microsoft Defender ATP-documentatie:

- [Voorwaardelijke toegang van Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP-risicodashboard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

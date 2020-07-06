---
title: macOS-apparaten versleutelen met FileVault-schijfversleuteling met Intune
titleSuffix: Microsoft Intune
description: Versleutel macOS-apparaten met de ingebouwde versleutelingsmethode FileVault en beheer de herstelsleutels voor deze versleutelde apparaten vanuit de Intune-portal.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/24/2020
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
ms.openlocfilehash: 1f2a6955a430427fe3f4e2791da6bbaecdd90523
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353565"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>FileVault-schijfversleuteling gebruiken voor macOS met Intune

Intune biedt ondersteuning voor macOS FileVault-schijfversleuteling. FileVault is een programma voor de versleuteling van volledige schijven. Het programma wordt geleverd bij macOS. U kunt Intune gebruiken om FileVault te configureren op apparaten waarop **macOS 10.13 of hoger** wordt uitgevoerd.

Gebruik een van de volgende beleidstypen om FileVault op uw beheerde apparaten te configureren:

- **[Een eindpuntbeveiligingsbeleid voor macOS FileVault opstellen](#create-endpoint-security-policy-for-filevault)** . Het FileVault-profiel in *eindpuntbeveiliging* is een gerichte groep instellingen die is toegewezen aan het configureren van FileVault.

  Bekijk de FileVault-instellingen die beschikbaar zijn in [de profielen voor het schijfversleutelingsbeleid](../protect/endpoint-security-disk-encryption-profile-settings.md).

- **[Configuratieprofiel van het apparaat voor eindpuntbescherming voor macOs FileVault](#create-endpoint-security-policy-for-filevault)** . De FileVault-instellingen vormen een eigen instellingencategorie in Endpoint Protection voor macOS. Zie [een apparaatprofiel maken in Intune](../configuration/device-profile-create.md) voor meer informatie over het gebruik van een configuratieprofiel voor apparaten.

  Bekijk de FileVault-instellingen die beschikbaar zijn voor [Bin eindpuntbeschermingsprofielen op het formulier voor het apparaatconfiguratiebeleid](../protect/endpoint-protection-macos.md#filevault).

Zie [BitLocker-beleid beheren](../protect/encrypt-devices.md) als u BitLocker voor Windows 10 wilt beheren.

> [!TIP]
> Intune biedt een ingebouwd [versleutelingsrapport](encryption-monitor.md) met informatie over de versleutelingsstatus van al uw beheerde apparaten.

Wanneer u een beleid hebt gemaakt voor het met FileVault versleutelen van apparaten, wordt het beleid in twee fasen toegepast op apparaten. In eerste instantie wordt het apparaat voorbereid zodat Intune kan worden gebruikt voor het ophalen van en het maken van back-ups van de herstelsleutel. Deze actie heet ook wel 'escrow'. Wanneer er een escrow-sleutel is gemaakt, kan worden gestart met de schijfversleuteling.

Door de gebruiker goedgekeurde apparaatinschrijving is vereist om FileVault op een apparaat te laten werken. De inschrijving geldt alleen als goedgekeurd door de gebruiker als deze het beheerprofiel handmatig goedkeurt vanuit de systeemvoorkeuren.

## <a name="permissions-to-manage-filevault"></a>Machtigingen voor het beheren van FileVault

Als u FileVault in Intune wilt beheren, moet uw account beschikken over de juiste machtigingen voor [op rollen gebaseerd toegangsbeheer](../fundamentals/role-based-access-control.md) (RBAC).

Hieronder vindt u de FileVault-machtigingen die deel uitmaken van de categorie **Externe taken** en de ingebouwde RBAC-rollen waarmee de machtiging wordt verleend:

- **De FileVault-sleutel ophalen**:
  - Helpdeskmedewerker
  - Endpoint Security Manager

- **FileVault-sleutel roteren**
  - Helpdeskmedewerker

## <a name="create-endpoint-security-policy-for-filevault"></a>Eindpuntbeveiligingsbeleid voor FileVault opstellen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **eindpuntbeveiliging** > **schijfversleuteling** > **Maak beleid**.

3. Voer op de pagina **Basisinformatie** de volgende eigenschappen in en kies vervolgens **Volgende**.
   - **Platform**: macOS
   - **Profiel**: FileVault

   ![Het FileVault-profiel selecteren](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. Op de pagina **Configuratie-instellingen**:
   1. Stel *FileVault inschakelen* in op **Ja**.
   2. Bij *Herstelsleuteltype* wordt alleen de optie **Persoonlijke herstelsleutel** ondersteund.
   3. Configureer aanvullende instellingen om te voldoen aan uw vereisten.

   Overweeg een bericht toe te voegen om gebruikers te helpen bij het ophalen van de herstelsleutel voor hun apparaat. Deze informatie kan nuttig zijn voor uw gebruikers wanneer u de instelling voor wijziging van persoonlijke herstelsleutels gebruikt. Met deze instelling kan periodiek automatisch een nieuwe herstelsleutel voor een apparaat worden gegenereerd.

   Bijvoorbeeld: Als u een verloren of onlangs vernieuwde herstelsleutel wilt ophalen, meldt u zich aan op de website van de Intune-bedrijfsportal. Dit kan vanaf elk apparaat. Ga in de portal naar Apparaten en selecteer het apparaat waarvoor FileVault is ingeschakeld. Selecteer dan *Herstelsleutel ophalen*. De huidige herstelsleutel wordt weergegeven.

5. Wanneer u klaar bent met het configureren van instellingen, selecteert u **Volgende**.

6. Selecteer op de pagina **Bereik (tags)** de optie **Bereiktags selecteren** om het deelvenster Tags selecteren te openen en bereiktags aan het profiel toe te wijzen.

   Selecteer **Volgende** om door te gaan.

7. Selecteer op de pagina **Toewijzingen** de groepen die dit profiel zullen ontvangen. Zie Gebruikers- en apparaatprofielen toewijzen voor meer informatie over het toewijzen van profielen.
Selecteer **Volgende**.

8. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

## <a name="create-device-configuration-policy-for-filevault"></a>Configuratiebeleid voor FileVault maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Stel op de pagina **Een profiel maken** de volgende opties in. Klik vervolgens op **Maken**:
   - **Platform**: macOS
   - **Profiel**: Endpoint Protection

   ![Het FileVault-profiel selecteren](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. Voer op de pagina **Basisinformatie** de volgende eigenschappen in:

   - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam bevat bijvoorbeeld mogelijk het profieltype en het platform.

   - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.

5. Selecteer op de pagina **Configuratie-instellingen** de optie **FileVault** om de beschikbare instellingen uit te vouwen:

   > [!div class="mx-imgBorder"]
   > ![FileVault-instellingen](./media/encrypt-devices-filevault/filevault-settings.png)

6. Configureer de volgende instellingen:
  
   - Selecteer voor *FileVault* de optie **Ja**.

   - Selecteer voor *Type herstelsleutel* de optie **Persoonlijke sleutel**.

   - Voeg voor *Escrow-locatiebeschrijving van persoonlijke herstelsleutel* een bericht toe om gebruikers te helpen bij het ophalen van de herstelsleutel voor hun apparaat. Deze informatie kan nuttig zijn voor uw gebruikers wanneer u de instelling voor wijziging van persoonlijke herstelsleutels gebruikt. Met deze instelling kan periodiek automatisch een nieuwe herstelsleutel voor een apparaat worden gegenereerd.

     Bijvoorbeeld: Als u een verloren of onlangs vernieuwde herstelsleutel wilt ophalen, meldt u zich aan op de website van de Intune-bedrijfsportal. Dit kan vanaf elk apparaat. Ga in de portal naar *Apparaten* en selecteer het apparaat waarvoor FileVault is ingeschakeld. Selecteer dan *Herstelsleutel ophalen*. De huidige herstelsleutel wordt weergegeven.

   Configureer de overige [FileVault-instellingen](endpoint-protection-macos.md#filevault) zodanig dat er aan de vereisten van uw bedrijf wordt voldaan. Selecteer vervolgens **Volgende**.

7. Selecteer op de pagina **Bereik (tags)** de optie **Bereiktags selecteren** om het deelvenster Tags selecteren te openen en bereiktags aan het profiel toe te wijzen.

   Selecteer **Volgende** om door te gaan.

8. Selecteer op de pagina **Toewijzingen** de groepen die dit profiel zullen ontvangen. Zie Gebruikers- en apparaatprofielen toewijzen voor meer informatie over het toewijzen van profielen.
Selecteer **Volgende**.

9. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

## <a name="manage-filevault"></a>FileVault beheren

Zie [schrijfversleuteling controleren](../protect/encryption-monitor.md) voor informatie over apparaten die het FileVault-beleid ontvangen.

Wanneer Intune een macOS-apparaat voor het eerst versleutelt met FileVault, wordt er een persoonlijke herstelsleutel gemaakt. Na het versleutelen wordt de persoonlijke sleutel één keer weergegeven aan de apparaatgebruiker.

Bij beheerde apparaten kan Intune een escrow-sleutel maken van de persoonlijke herstelsleutel. Met escrow-sleutels kunnen Intune-beheerders sleutels vernieuwen om de bescherming van apparaten te verbeteren en kunnen gebruikers verloren geraakte of vernieuwde persoonlijke herstelsleutels herstellen.

Nadat Intune een macOS-apparaat versleutelt met FileVault:

- Beheerders kunnen de FileVault-herstelsleutels weergeven en beheren met behulp van het Intune-versleutelingsrapport.
- Gebruikers kunnen de persoonlijke herstelsleutel van een apparaat weergeven vanuit de online Bedrijfsportal op het apparaat. Kies in de online bedrijfsportal het versleutelde macOS-apparaat en kies vervolgens 'Herstelsleutel ophalen' als externe actie.

> [!IMPORTANT]
> Apparaten die door gebruikers zijn versleuteld (en niet door Intune), kunnen niet door Intune worden beheerd. Dit betekent dat Intune geen escrow-sleutel kan maken voor het persoonlijke herstel van de apparaten en dat de vernieuwing van de herstelsleutel niet kan worden beheerd. Voordat Intune kan worden gebruikt voor het beheer van FileVault en herstelsleutels voor het apparaat, moet de gebruiker het apparaat ontsleutelen. Daarna kan het apparaat met Intune worden versleuteld.

### <a name="retrieve-personal-recovery-key"></a>Persoonlijke herstelsleutel ophalen

Bij een macOS-apparaat dat door Intune is versleuteld, kunnen eindgebruikers hun persoonlijke herstelsleutel (FileVault-sleutel) ophalen met behulp van de iOS-bedrijfsportal-app, de Android-bedrijfsportal-app of via de Android Intune-app.

Het apparaat met de persoonlijke herstelsleutel moet zijn geregistreerd bij Intune en moet zijn versleuteld met FileVault via Intune. Met de iOS-bedrijfsportal-app, Android-bedrijfsportal-app, de Android Intune-app of de Bedrijfsportal-website kunnen gebruikers de **FileVault**-herstelsleutel zien die nodig is om toegang te krijgen tot hun Mac-apparaten.

Apparaatgebruikers kunnen **Apparaten** > *het versleutelde en ingeschreven macOS-apparaat* > **Herstelsleutel ophalen** selecteren. In de browser wordt de Webbedrijfsportal getoond waarin de herstelsleutel wordt weergegeven.

### <a name="rotate-recovery-keys"></a>Herstelsleutels wijzigen

Intune biedt ondersteuning voor meerdere opties voor het vernieuwen en herstellen van persoonlijke herstelsleutels. Persoonlijke herstelsleutels kunnen bijvoorbeeld worden vernieuwd als de huidige persoonlijke herstelsleutel verloren is geraakt of er sprake is van een risico.

- **Automatisch wijzigen**: Als beheerder kunt u de FileVault-instelling voor het wijzigen van persoonlijke herstelsleutels zodanig configureren dat er automatisch periodiek nieuwe herstelsleutels worden gegenereerd. Wanneer er een nieuwe sleutel wordt gegenereerd voor een apparaat, wordt de sleutel niet weergegeven aan de gebruiker. In plaats daarvan moet de gebruiker de sleutel ophalen bij een beheerder, of de app Bedrijfsportal gebruiken.

- **Handmatig wijzigen**: u kunt als beheerder informatie bekijken over apparaten die u met Intune beheert en die met FileVault zijn versleuteld. U kunt ervoor kiezen om de herstelsleutels voor zakelijke apparaten handmatig te vernieuwen. Het is niet mogelijk om de herstelsleutels voor persoonlijke apparaten te vernieuwen.

  Een herstelsleutel vernieuwen:

  1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

  2. Selecteer **Apparaten** > **Alle apparaten**.

  3. Selecteer in de lijst met apparaten het apparaat dat is versleuteld en waarvoor u de sleutel wilt vernieuwen. Selecteer vervolgens onder Bewaken de optie  **Herstelsleutels**.
  
  4. In het deelvenster Herstelsleutels selecteert u **FileVault-herstelsleutel vernieuwen**.

     De volgende keer dat het apparaat incheckt bij Intune, wordt de persoonlijke sleutel vernieuwd. Indien nodig kan de nieuwe sleutel door de gebruiker worden verkregen via de bedrijfsportal.

### <a name="recover-recovery-keys"></a>Herstelsleutels herstellen

- **Beheerder**: beheerders kunnen de persoonlijke herstelsleutels voor apparaten die zijn versleuteld met FileVault niet bekijken.

- **Eindgebruiker**: eindgebruikers gebruiken de bedrijfsportalwebsite vanaf een apparaat om hun huidige persoonlijke herstelsleutel te gebruiken voor een van hun beheerde apparaten. Het is niet mogelijk om herstelsleutels te bekijken vanuit de app Bedrijfsportal.

  Een herstelsleutel weergeven:
  
  1. Meld u op een apparaat aan bij de *Intune-bedrijfsportal*website.

  2. Ga in de portal naar **Apparaten** en selecteer het macOS-apparaat dat is versleuteld met FileVault.

  3. Selecteer **Herstelsleutel ophalen**. De huidige herstelsleutel wordt weergegeven.

## <a name="next-steps"></a>Volgende stappen

[BitLocker-beleid beheren](../protect/encrypt-devices.md)

[Schijfversleuteling controleren](../protect/encryption-monitor.md)

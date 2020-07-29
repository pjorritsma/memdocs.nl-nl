---
title: macOS-apparaten versleutelen met FileVault-schijfversleuteling met Intune
titleSuffix: Microsoft Intune
description: Versleutel macOS-apparaten met de ingebouwde versleutelingsmethode FileVault en beheer de herstelsleutels voor deze versleutelde apparaten vanuit de Intune-portal.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: cdfec1d82d68e97544172c56cecc416846b4a0f6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460481"
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

Naast het gebruik van Intune-beleid voor het versleutelen van een apparaat met FileVault kunt u beleid implementeren op een beheerd apparaat zodat er in Intune vanuit kan worden gegaan dat [het apparaat wordt beheerd door FileVault als het is versleuteld door de gebruikers](#assume-management-of-filevault-on-previously-encrypted-devices). Voor dit scenario is het vereist dat het apparaat het FileVault-beleid van Intune ontvangt, waarna de gebruiker de persoonlijke herstelsleutel uploadt naar Intune.

Door de gebruiker goedgekeurde apparaatinschrijving is vereist om FileVault op een apparaat te laten werken. De inschrijving geldt alleen als goedgekeurd door de gebruiker als deze het beheerprofiel handmatig goedkeurt vanuit de systeemvoorkeuren.

## <a name="permissions-to-manage-filevault"></a>Machtigingen voor het beheren van FileVault

Als u FileVault in Intune wilt beheren, moet uw account beschikken over de juiste machtigingen voor [op rollen gebaseerd toegangsbeheer](../fundamentals/role-based-access-control.md) (RBAC).

Hieronder vindt u de FileVault-machtigingen die deel uitmaken van de categorie **Externe taken** en de ingebouwde RBAC-rollen waarmee de machtiging wordt verleend:

- **De FileVault-sleutel ophalen**:
  - Helpdeskmedewerker
  - Endpoint Security Manager

- **FileVault-sleutel roteren**
  - Helpdeskmedewerker

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

   - Voeg voor *Escrow-locatiebeschrijving van persoonlijke herstelsleutel* een bericht toe om gebruikers te helpen bij [het ophalen van de herstelsleutel](#retrieve-a-personal-recovery-key) voor hun apparaat. Deze informatie kan nuttig zijn voor uw gebruikers wanneer u de instelling voor wijziging van persoonlijke herstelsleutels gebruikt. Met deze instelling kan periodiek automatisch een nieuwe herstelsleutel voor een apparaat worden gegenereerd.

     Bijvoorbeeld: Als u een verloren of onlangs vernieuwde herstelsleutel wilt ophalen, meldt u zich aan op de website van de Intune-bedrijfsportal. Dit kan vanaf elk apparaat. Ga in de portal naar *Apparaten* en selecteer het apparaat waarvoor FileVault is ingeschakeld. Selecteer dan *Herstelsleutel ophalen*. De huidige herstelsleutel wordt weergegeven.

   Configureer de overige [FileVault-instellingen](endpoint-protection-macos.md#filevault) zodanig dat er aan de vereisten van uw bedrijf wordt voldaan. Selecteer vervolgens **Volgende**.

7. Selecteer op de pagina **Bereik (tags)** de optie **Bereiktags selecteren** om het deelvenster Tags selecteren te openen en bereiktags aan het profiel toe te wijzen.

   Selecteer **Volgende** om door te gaan.

8. Selecteer op de pagina **Toewijzingen** de groepen die dit profiel zullen ontvangen. Zie Gebruikers- en apparaatprofielen toewijzen voor meer informatie over het toewijzen van profielen.
Selecteer **Volgende**.

9. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

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

   U kunt een bericht toevoegen om gebruikers te helpen bij [het ophalen van de herstelsleutel](#retrieve-a-personal-recovery-key) voor hun apparaat. Deze informatie kan nuttig zijn voor uw gebruikers wanneer u de instelling voor wijziging van persoonlijke herstelsleutels gebruikt. Met deze instelling kan periodiek automatisch een nieuwe herstelsleutel voor een apparaat worden gegenereerd.

   Bijvoorbeeld: Als u een verloren of onlangs vernieuwde herstelsleutel wilt ophalen, meldt u zich aan op de website van de Intune-bedrijfsportal. Dit kan vanaf elk apparaat. Ga in de portal naar Apparaten en selecteer het apparaat waarvoor FileVault is ingeschakeld. Selecteer dan *Herstelsleutel ophalen*. De huidige herstelsleutel wordt weergegeven.

5. Wanneer u klaar bent met het configureren van instellingen, selecteert u **Volgende**.

6. Selecteer op de pagina **Bereik (tags)** de optie **Bereiktags selecteren** om het deelvenster Tags selecteren te openen en bereiktags aan het profiel toe te wijzen.

   Selecteer **Volgende** om door te gaan.

7. Selecteer op de pagina **Toewijzingen** de groepen die dit profiel zullen ontvangen. Zie Gebruikers- en apparaatprofielen toewijzen voor meer informatie over het toewijzen van profielen.
Selecteer **Volgende**.

8. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

## <a name="manage-filevault"></a>FileVault beheren

Zie [schrijfversleuteling controleren](../protect/encryption-monitor.md) voor informatie over apparaten die het FileVault-beleid ontvangen.

Wanneer Intune een macOS-apparaat voor het eerst versleutelt met FileVault, wordt er een persoonlijke herstelsleutel gemaakt. Na het versleutelen wordt de persoonlijke sleutel één keer weergegeven aan de apparaatgebruiker.

Bij beheerde apparaten kan Intune een escrow-sleutel maken van de persoonlijke herstelsleutel. Met escrow-sleutels kunnen Intune-beheerders sleutels vernieuwen om de bescherming van apparaten te verbeteren en kunnen gebruikers verloren geraakte of vernieuwde persoonlijke herstelsleutels herstellen.

Intune borgt een herstelsleutel wanneer Intune-beleid een apparaat versleutelt of nadat een gebruiker zijn of haar herstelsleutel heeft geüpload voor een apparaat dat handmatig is versleuteld.

Nadat Intune de persoonlijke herstelsleutel heeft geborgd:

- Beheerders kunnen de FileVault-herstelsleutels voor elk beheerd macOS-apparaat beheren en draaien met behulp van het Intune-versleutelingsrapport.
- Beheerders kunnen de persoonlijke herstelsleutel alleen weergeven voor beheerde macOS-apparaten die zijn gemarkeerd als *zakelijk*. Ze kunnen de herstelsleutel voor persoonlijke apparaten niet weergeven.
- Gebruikers kunnen hun persoonlijke herstelsleutel weergeven en [ophalen van een ondersteunde locatie](#retrieve-a-personal-recovery-key). De gebruiker kan op de bedrijfsportalwebsite bijvoorbeeld kiezen om *de herstelsleutel op te halen*  als een actie voor een extern apparaat.

### <a name="assume-management-of-filevault-on-previously-encrypted-devices"></a>Het beheer van FileVault veronderstellen op apparaten die eerder zijn versleuteld

Intune kan FileVault-schijfversleuteling beheren op macOS-apparaten die zijn versleuteld door middel van Intune-beleid. Intune kan ook het beheer overnemen van FileVault op apparaten die zijn versleuteld door gebruikers van het apparaat en niet via Intune-beleid.

#### <a name="prerequisites-to-assume-management-of-filevault"></a>Vereisten om het beheer van FileVault te veronderstellen

Om het beheer van eerder versleutelde apparaten te veronderstellen, moet aan de volgende voorwaarden worden voldaan:

1. **Implementeer een FileVault-beleid op het apparaat**. Het eerder versleutelde apparaat moet een beleid van Intune ontvangen waarmee FileVault-schijfversleuteling wordt ingeschakeld.

   In dit scenario wordt het apparaat niet ontsleuteld of opnieuw versleuteld met het beleid. In plaats daarvan kan Intune het beheer veronderstellen van de FileVault-versleuteling die al op het apparaat is ingeschakeld.  U kunt het versleutelingsbeleid voor de eindpuntbeveiliging gebruiken of eindpuntbeveiligingsbeleid voor apparaatconfiguratie gebruiken om apparaten te versleutelen met FileVault.

   Raadpleeg [Beleid opstellen en implementeren](#create-device-configuration-policy-for-filevault).

2. **Gebruikers uploaden hun persoonlijke herstelsleutel naar Intune**.  Nadat het apparaat het FileVault-beleid heeft ontvangen, instrueert u de apparaatgebruiker die het apparaat heeft versleuteld om de persoonlijke herstelsleutel te uploaden naar Intune. Als de sleutel met succes is ingevoerd, veronderstelt Intune het beheer van de FileVault-versleuteling en wordt er een nieuwe persoonlijke herstelsleutel gemaakt voor het apparaat en de gebruiker.

   > [!IMPORTANT]
   > Intune waarschuwt gebruikers niet dat ze hun persoonlijke herstelsleutel moeten uploaden om de versleuteling te voltooien. Gebruik in plaats daarvan uw normale IT-communicatiekanalen om gebruikers die eerder hun macOS-apparaat met FileVault hebben versleuteld te waarschuwen dat ze hun persoonlijke herstelsleutel moeten uploaden naar Intune.  
   >
   > Afhankelijk van uw nalevingsbeleid kan de toegang van uw apparaat tot zakelijke resources mogelijk worden geblokkeerd totdat Intune het beheer van FileVault-versleuteling op het apparaat heeft verondersteld.

#### <a name="upload-a-personal-recovery-key"></a>Een persoonlijke herstelsleutel uploaden

Als u Intune wilt inschakelen om FileVault te beheren op een eerder versleuteld apparaat, moet de gebruiker van het apparaat de huidige persoonlijke herstelsleutel voor het apparaat via de bedrijfsportalwebsite uploaden naar Intune.  Bij het uploaden draait Intune de sleutel om een nieuwe persoonlijke herstelsleutel te maken, die vervolgens door Intune wordt opgeslagen voor eventueel toekomstig herstel.

De gebruiker zoekt op de bedrijfsportalwebsite het versleutelde macOS-apparaat en selecteert de optie **Herstelsleutel opslaan**. Zodra de persoonlijke herstelsleutel is ingevoerd, probeert Intune de sleutel te draaien om een nieuwe sleutel te genereren. Het draaien wordt uitgevoerd om te controleren of de ingevoerde sleutel klopt voor dat apparaat. Deze nieuwe sleutel wordt vervolgens door Intune opgeslagen en beheerd voor het geval de gebruiker het apparaat in de toekomst moet herstellen.

Als het draaien van de sleutel mislukt, is het FileVault-beleid van het apparaat niet verwerkt of klopt de ingevoerde sleutel niet voor het apparaat.

Na een geslaagde rotatie kan een gebruiker [de nieuwe persoonlijke herstelsleutel ophalen op een ondersteunde locatie](#retrieve-a-personal-recovery-key).

 Bekijk de [inhoud van de eindgebruiker voor het uploaden van de persoonlijke herstelsleutel](../user-help/store-recovery-key.md).

> [!IMPORTANT]
> Intune kan de FileVault-versleuteling niet beheren voor een apparaat dat door een gebruiker en niet door Intune is versleuteld totdat het apparaat een FileVault-beleid ontvangt en de gebruiker van het apparaat zijn of haar persoonlijke herstelsleutel uploadt.

### <a name="retrieve-a-personal-recovery-key"></a>Een persoonlijke herstelsleutel ophalen

Eindgebruikers kunnen voor een macOS-apparaat met FileVault-versleuteling die door Intune wordt beheerd hun persoonlijke herstelsleutel (FileVault-sleutel) ophalen uit de volgende locaties, met behulp van elk apparaat:

- Bedrijfsportalwebsite
- Bedrijfsportal-app voor iOS/iPadOS
- Android-bedrijfsportal-app
- Intune-app

Beheerders kunnen persoonlijke herstelsleutels weergeven voor versleutelde macOS-apparaten die zijn gemarkeerd als een *zakelijk* apparaat. Ze kunnen de herstelsleutel voor een persoonlijk apparaat niet weergeven.

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

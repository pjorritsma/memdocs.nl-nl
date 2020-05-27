---
title: Nalevingsbeleid voor apparaten maken in Microsoft Intune - Azure | Microsoft Docs
description: Nalevingsbeleid voor apparaten maken, overzicht van status- en ernstniveaus zien, status voor Respijtperiode gebruiken, werken met voorwaardelijke toegang, apparaten zonder toegewezen beleid verwerken, en de verschillen in naleving bekijken in de Azure-portal en de klassieke portal in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: de23dc438ac176383cf5f5fbfac4da22f91bd4b2
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988823"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>Een nalevingsbeleid maken in Microsoft Intune

Nalevingsbeleid voor apparaten is belangrijk voor het beveiligen van de resources van uw organisatie als u gebruikmaakt van Intune. In Intune kunt u regels en instellingen maken waar apparaten zich aan moeten houden om te voldoen, zoals een minimale versie van het besturingssysteem. Als het apparaat niet voldoet, kunt u toegang tot gegevens en resources blokkeren met behulp van [voorwaardelijke toegang](conditional-access.md).

U kunt ook maatregelen nemen bij niet-naleving; zo kunt u bijvoorbeeld een e-mailmelding naar de gebruiker verzenden. Zie [Aan de slag met apparaatnaleving](device-compliance-get-started.md) voor een overzicht van de werking van nalevingsbeleid.

Dit artikel:

- Geeft de vereisten en stappen weer voor het maken van nalevingsbeleid.
- Laat zien hoe u het beleid kunt toewijzen aan uw gebruikers- en apparaatgroepen.
- Beschrijft aanvullende functies, waaronder bereiktags om uw beleid te filteren, en stappen die u kunt uitvoeren voor apparaten die niet compatibel zijn.
- Geeft de cyclusduur voor vernieuwen van check-ins weer wanneer apparaten beleidsupdates ontvangen.

## <a name="before-you-begin"></a>Voordat u begint

Neem het volgende in acht voor het gebruik van het nalevingsbeleid voor apparaten:

- Gebruik de volgende abonnementen:

  - Intune
  - U hebt de Azure AD (Active Directory) Premium-editie nodig om voorwaardelijke toegang te gebruiken. In [Prijzen van Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) wordt vermeld wat u krijgt bij de verschillende edities. voor Intune-naleving is geen Azure AD vereist.

- Gebruik een ondersteund platform:

  - Android-apparaatbeheerder
  - Android Enterprise
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Apparaten registreren in Intune (vereist om de nalevingsstatus te zien)

- Registreer apparaten voor één gebruiker of registreer ze zonder een primaire gebruiker. Apparaten die zijn geregistreerd voor meerdere gebruikers worden niet ondersteund.

## <a name="create-the-policy"></a>Beleid maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Nalevingsbeleid** > **Beleid** > **Beleid maken**.

3. Selecteer een **Platform** voor dit beleid uit de volgende opties:
   - *Android-apparaatbeheerder*
   - *Android Enterprise*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows Phone 8.1*
   - *Windows 8.1 en hoger*
   - *Windows 10 en hoger*

    Voor *Android Enterprise* selecteert u ook een **Beleidstype**:
     - *Nalevingsbeleid van de apparaateigenaar van het Android-apparaat*
     - *Nalevingsbeleid voor Android-werkprofiel*

    Selecteer vervolgens **Maken** om het configuratievenster **Beleid maken** te openen.

4. Geef op het tabblad **Basisinformatie** een **Naam** op waaraan u het beleid later kunt herkennen. **iOS/iPadOS-apparaten die zijn opengebroken, niet markeren als compatibel** is bijvoorbeeld een goede beleidsnaam.

   U kunt er ook voor kiezen om een **Beschrijving** op te geven.
  
5. Vouw op het tabblad **Nalevingsinstellingen** de beschikbare categorieën uit en configureer de instellingen voor uw beleid.  In de volgende artikelen worden de instellingen voor elk platform beschreven:
   - [Android-apparaatbeheerder](compliance-policy-create-android.md)
   - [Android Enterprise](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows Phone 8.1, Windows 8.1 en hoger](compliance-policy-create-windows-8-1.md)
   - [Windows 10 en hoger](compliance-policy-create-windows.md)  

6. Op het tabblad **Locaties** kunt u naleving afdwingen op basis van de locatie van het apparaat. Kies uit bestaande locaties. Als u nog geen beschikbare locatie hebt, raadpleegt u [Locaties gebruiken (netwerkgrens)](use-network-locations.md) voor hulp.
   > [!TIP]
   > **Locaties** zijn alleen beschikbaar voor het platform *Android-apparaatbeheerder*.

7. Geef op het tabblad **Acties voor niet-naleving** een reeks acties op die automatisch moeten worden toegepast op apparaten die niet voldoen aan dit nalevingsbeleid.

   U kunt meerdere acties toevoegen, en voor sommige acties kunt u schema's en aanvullende details configureren. U kunt bijvoorbeeld de planning van de standaardactie *Het apparaat als niet-compatibel markeren* zo wijzigen dat deze na één dag wordt uitgevoerd. U kunt vervolgens een actie toevoegen om een e-mailbericht naar de gebruiker te verzenden wanneer het apparaat niet voldoet aan deze status. U kunt ook acties toevoegen waarmee apparaten die niet-compatibel blijven, worden vergrendeld of buiten gebruik worden gesteld.

   Voor informatie over de acties die u kunt configureren raadpleegt u [Acties voor niet-conforme apparaten toevoegen](actions-for-noncompliance.md). U leest hier ook hoe u e-mailmeldingen die naar uw gebruikers kunt versturen.

   Een ander voorbeeld is het gebruik van Locaties waarbij u ten minste één locatie toevoegt aan een nalevingsbeleid. In dit geval wordt de standaardactie bij niet-naleving uitgevoerd wanneer u ten minste één locatie selecteert. Als het apparaat niet is verbonden met een van de geselecteerde locaties, wordt het apparaat beschouwd als 'niet conform'. U kunt het schema zo configureren dat gebruikers een respijtperiode van bijvoorbeeld één dag krijgen.

8. Op het tabblad **Bereiktags** kunt u tags selecteren om het beleid te filteren op specifieke groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Nadat u de instellingen hebt toegevoegd, kunt u ook een bereiktag toevoegen aan het nalevingsbeleid. 

   Zie [Bereiktags gebruiken om beleidsregels te filteren](../fundamentals/scope-tags.md) voor meer informatie over het gebruik van bereiktags.

9. Op het tabblad **Toewijzingen** kunt u het beleid toewijzen aan uw groepen.  

   Selecteer **+ Groepen selecteren die moeten worden opgenomen** en wijs het beleid toe aan een of meer groepen. Het beleid wordt op deze groepen toegepast wanneer u het beleid na de volgende stap opgeslagen. 

10. Controleer de instellingen op het tabblad **Beoordelen en maken** en selecteer **Maken** als u klaar bent om het nalevingsbeleid op te slaan.  

    De gebruikers of apparaten waarop het beleid is gericht, worden beoordeeld op naleving wanneer ze worden ingecheckt bij Intune.

<!-- Evaluate option  - pending details as to its fate with this new Full Screen UI udpate  

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.
-->

## <a name="refresh-cycle-times"></a>Cyclusduur vernieuwen

In Intune worden verschillende vernieuwingscycli gebruikt om te controleren op updates voor nalevingsbeleid. Als het apparaat onlangs is ingeschreven, worden de check-ins vaker uitgevoerd. In [Vernieuwingscycli voor beleidsregels en profielen](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) worden de geschatte vernieuwingstijden vermeld.

Gebruikers kunnen ook op elk gewenst moment de bedrijfsportal-app openen en het apparaat synchroniseren om onmiddellijk op beleidsupdates te controleren.

### <a name="assign-an-ingraceperiod-status"></a>Een Respijtperiode-status toewijzen

De Respijtperiode-status voor een nalevingsbeleid is een waarde. Deze waarde wordt bepaald door de combinatie van de respijtperiode van een apparaat en de daadwerkelijke status van een apparaat voor dit nalevingsbeleid.

Als een apparaat de status Niet-compatibel heeft voor een toegewezen nalevingsbeleid, en:

- er geen respijtperiode is toegewezen aan het apparaat, is de toegewezen waarde voor het nalevingsbeleid Niet-compatibel
- de respijtperiode voor het apparaat is verlopen, is de toegewezen waarde voor het nalevingsbeleid Niet-compatibel
- de respijtperiode voor het apparaat in de toekomst ligt, is de toegewezen waarde voor het nalevingsbeleid Respijtperiode

De volgende tabel geeft een overzicht van deze punten:

|Werkelijke nalevingsstatus|Waarde van toegewezen respijtperiode|Effectieve nalevingsstatus|
|---------|---------|---------|
|Niet-compatibel |Er is geen respijtperiode toegewezen |Niet-compatibel |
|Niet-compatibel |De datum van gisteren|Niet-compatibel|
|Niet-compatibel |De datum van morgen|Respijtperiode|

Zie [Nalevingsbeleid voor Intune-apparaten controleren](compliance-policy-monitor.md) voor meer informatie over het controleren van nalevingsbeleid voor apparaten.

### <a name="assign-a-resulting-compliance-policy-status"></a>Een resulterende nalevingsbeleidsstatus toewijzen

Wanneer een apparaat meerdere nalevingsbeleidsregels heeft en het apparaat verschillende nalevingsstatussen heeft voor twee of meer toegewezen nalevingsbeleidsregels, wordt één resulterende nalevingsstatus toegewezen. Deze toewijzing is gebaseerd op een conceptueel ernstniveau dat is toegewezen aan elke nalevingsstatus. Elke nalevingsstatus heeft een van de volgende ernstniveaus:

|Status  |Ernst  |
|---------|---------|
|Onbekend     |1|
|Niet van toepassing     |2|
|Compliant|3|
|Respijtperiode|4|
|Niet-compatibel|5|
|Fout|6|

Wanneer een apparaat meerdere nalevingsbeleidsregels heeft, wordt het hoogste ernstniveau van alle beleidsregels toegewezen aan dat apparaat.

Aan een apparaat kunnen bijvoorbeeld drie nalevingsbeleidsregels zijn toegewezen: één met de status Unknown (ernst = 1), één met de status Compliant (ernst = 3) en één met de status InGracePeriod (ernst =4). De status InGracePeriod heeft het hoogste ernstniveau. Dus hebben alle drie de beleidsregels de nalevingsstatus InGracePeriod.

## <a name="next-steps"></a>Volgende stappen

[Controleer uw beleidsregels](compliance-policy-monitor.md).

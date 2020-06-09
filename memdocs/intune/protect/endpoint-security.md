---
title: Eindpuntbeveiliging beheren in Microsoft Intune | Microsoft Docs
description: Meer informatie over hoe beveiligingsbeheerders het knooppunt eindpuntbeveiliging kunnen gebruiken om de beveiliging van apparaten te beheren en problemen van apparaten te herstellen in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 99ac1e069386c69011543ac40878dd62a0d50527
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990822"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>Eindpuntbeveiliging beheren in Microsoft Intune

Als beveiligingsbeheerder kunt u het knooppunt *eindpuntbeveiliging* gebruiken in Intune om de beveiliging van het apparaat te configureren en beveiligingstaken voor apparaten te beheren wanneer deze apparaten risico lopen. Het eindpuntbeveiligingsbeleid is ontworpen om u te helpen zich te concentreren op de beveiliging van uw apparaten en het risico te beperken. De taken die beschikbaar zijn, helpen u bij het identificeren van apparaten die risico lopen, om die apparaten te herstellen en deze terug te zetten naar een compatibele of veiligere status.

Het knooppunt eindpuntbeveiliging groepeert de hulpprogramma's die beschikbaar zijn via Intune en die u gebruikt om apparaten te beveiligen:

- **Bekijk de status van alle beheerde apparaten**. Gebruik de weergave [alle apparaten](#manage-devices) waar u de naleving van apparaten op een hoog niveau kunt bekijken en vervolgens inzoomen op specifieke apparaten om te begrijpen aan welke nalevingsbeleidsregels niet is voldaan zodat u deze kunt oplossen.

- **Implementeer beveiligingsbasislijnen die best practice-beveiligingsconfiguraties voor apparaten tot stand brengen**. Intune bevat [beveiligingsbasislijnen](#manage-security-baselines) voor Windows-apparaten en een groeiende lijst met toepassingen, zoals Microsoft Defender Advanced Threat Protection (Defender ATP) en Microsoft Edge. Beveiligingsbasislijnen zijn vooraf geconfigureerde Windows-instellingen waarmee u een beproefde groep instellingen en standaardwaarden kunt toepassen die door relevante beveiligingsteams worden aanbevolen.

- **Beveiligingsconfiguraties op apparaten beheren door middel van nauwkeurig beleid**.  Elk [eindpuntbeveiligingsbeleid](#use-policies-to-manage-device-security) richt zich op aspecten van de beveiliging van apparaten, zoals virussen, schijfversleuteling, firewalls en verschillende gebieden die beschikbaar worden gesteld via integratie met Defender ATP.

- **Stel de apparaat- en gebruikersvereisten in via het nalevingsbeleid**. Met [nalevingsbeleid](../protect/device-compliance-get-started.md) stelt u de regels in waaraan apparaten en gebruikers moeten voldoen om als compatibel te worden beschouwd. Regels kunnen versies van het besturingssysteem, wachtwoordvereisten, bedreigingsniveaus van apparaten en meer zijn.

  Wanneer u integreert met het Azure Active Directory (Azure AD)-[beleid voor voorwaardelijke toegang](#configure-conditional-access) om een nalevingsbeleid af te dwingen, kunt u de toegang tot bedrijf resources voor zowel beheerde apparaten en apparaten die nog niet worden beheerd, op poort plaatsen.

- **Intune integreren met uw Microsoft Defender ATP-team**. Door te [Integreren met Defender ATP](#set-up-integration-with-defender-atp) krijgt u toegang tot [beveiligingstaken](#review-security-tasks-from-defender-atp). Met beveiligingstaken worden de Defender-ATP en Intune met elkaar gecombineerd om uw beveiligingsteam te helpen bij het identificeren van apparaten die risico lopen en gedetailleerde herstelstappen aan Intune-beheerders te geven die vervolgens kunnen handelen.

In de volgende secties van dit artikel vindt u informatie over de verschillende taken die u kunt uitvoeren vanuit het knooppunt eindpuntbeveiliging van het beheercentrum en de RBAC-machtigingen (op rollen gebaseerd toegangsbeheer) die nodig zijn om ze te gebruiken.

## <a name="manage-devices"></a>Apparaten beheren

Het eindpunt beveiligingsknooppunt bevat de weergave *Alle apparaten*, waarin u een lijst met alle apparaten uit uw Azure AD kunt bekijken die beschikbaar zijn in Microsoft Endpoint Manager.

In deze weergave kunt u apparaten selecteren om in te zoomen voor meer informatie, zoals het beleid waarmee een apparaat niet compatibel is. U kunt ook toegang vanuit deze weergave gebruiken om problemen voor een apparaat op te lossen, zoals het opnieuw opstarten van een apparaat, het starten van een scan op malware of het roteren van BitLocker-sleutels op een Windows 10-apparaat.

Zie [Apparaten met eindpuntbeveiliging beheren in Microsoft Intune](../protect/endpoint-security-manage-devices.md) voor meer informatie.

## <a name="manage-security-baselines"></a>Beveiligingsbasislijnen beheren

Beveiligingsbasislijnen in Intune zijn vooraf geconfigureerde groepen instellingen die best practice-aanbevelingen zijn van de relevante Microsoft-beveiligingsteams voor het product. Intune biedt ondersteuning voor beveiligingsbasislijnen voor apparaatinstellingen van Windows 10, Microsoft Edge, Microsoft Defender Advanced Threat Protection en meer.

U kunt beveiligingsbasislijnen gebruiken om snel een *best practice*-configuratie van apparaat- en toepassingsinstellingen te implementeren om uw gebruikers en apparaten te beveiligen. Beveiligingsbasislijnen worden ondersteund voor apparaten met Windows 10-versie 1809 en hoger.

Zie [Beveiligingsbasislijnen gebruiken om Windows 10-apparaten te configureren in Intune](../protect/security-baselines.md) voor meer informatie.

Beveiligingsbasislijnen zijn een van de verschillende methoden in Intune om instellingen op apparaten te configureren. Bij het beheren van instellingen is het belangrijk om te begrijpen welke andere methoden in uw omgeving worden gebruikt voor het configureren van uw apparaten, zodat u conflicten kunt voorkomen. Zie [Beleidsconflicten voorkomen](#avoid-policy-conflicts) verderop in dit artikel.

## <a name="review-security-tasks-from-defender-atp"></a>Beveiligingstaken van Defender ATP controleren

Wanneer u Intune integreert met Microsoft Defender Advanced Threat Protection (Defender ATP), kunt u *Beveiligingstaken* in Intune controleren om te bepalen welke apparaten risico lopen en hoe dat risico kan worden verholpen. U kunt de taken vervolgens gebruiken om terug te rapporteren aan Defender ATP wanneer deze risico's worden verholpen.

- Uw Defender ATP-team bepaalt welke apparaten risico lopen en geeft deze informatie door aan uw Intune-team als een beveiligingstaak. Met een paar klikken maken ze een beveiligingstaak voor Intune die de apparaten aanduidt die risico lopen, het beveiligingslek aangeven en richtlijnen geven voor het oplossen van dat risico.

- De Intune-beheerders controleren beveiligingstaken en handelen vervolgens in Intune om deze taken te herstellen. Zodra de taak is verholpen, wordt deze door de gebruiker ingesteld op voltooid, waardoor deze status weer wordt gecommuniceerd naar het Defender ATP-team.

Met behulp van beveiligingstaken blijven beide teams in synchronisatie zien welke apparaten risico lopen en hoe en wanneer deze risico's worden hersteld.

Zie [Intune gebruiken voor het oplossen van beveiligingsproblemen geïdentificeerd door Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md) voor meer informatie.

## <a name="use-policies-to-manage-device-security"></a>Beleid gebruiken voor het beheren van de beveiliging van apparaten

Als beveiligingsbeheerder gebruikt u het beveiligingsbeleid dat is te vinden onder *Beheren* in het knooppunt eindpuntbeveiliging. Met dit beleid kunt u de beveiliging van apparaten configureren zonder de overhead om te moeten navigeren door het hoofdgedeelte en een breed scala aan instellingen die u in de configuratieprofielen en beveiligingsbasislijnen voor apparaten aantreft.

![Beleid beheren](./media/endpoint-security/endpoint-security-policies.png)

Voor meer informatie over het gebruik van dit beveiligingsbeleid, zie [Beveiliging van apparaten beheren met beleidsregels voor eindpuntbeveiliging](../protect/endpoint-security-policy.md).

Een beleid voor eindpuntbeveiliging is een van de verschillende methoden in Intune om instellingen op apparaten te configureren. Bij het beheren van instellingen is het belangrijk om te begrijpen welke andere methoden in uw omgeving worden gebruikt voor het configureren van uw apparaten en het voorkomen van conflicten. Zie [Beleidsconflicten voorkomen](#avoid-policy-conflicts) verderop in dit artikel.

Onder *Beheren* vind u ook het beleid *Apparaatnaleving* en *Voorwaardelijke toegang*. Deze beleidsregels zijn niet gericht op een beveiligingsbeleid voor het configureren van eindpunten, maar zijn belangrijke hulpprogramma's voor het beheren van apparaten en toegang tot uw bedrijfsresources.

## <a name="use-device-compliance-policy"></a>Nalevingsbeleid voor apparaten gebruiken

Gebruik het nalevingsbeleid voor apparaten om de voorwaarden te bepalen voor de apparaten en gebruikers die toegang tot uw netwerk- en bedrijfsresources mogen hebben.

De [beschikbare instellingen voor naleving](../protect/device-compliance-get-started.md#next-steps) zijn afhankelijk van het platform dat u gebruikt, maar algemene beleidsregels zijn:

- Vereisen dat apparaten een minimale of specifieke versie van het besturingssysteem uitvoeren
- Vereisten voor wachtwoorden instellen
- Het opgeven van een maximaal toegestane bedreigingsniveau voor apparaten, zoals wordt bepaald door Defender ATP of een andere Mobile Threat Defense-partner

Naast de beleidsregels ondersteunt het nalevingsbeleid:

- [Locaties](../protect/use-network-locations.md) die u in Intune definieert. Wanneer u locaties met een nalevingsbeleid gebruikt, kan het beleid ervoor zorgen dat apparaten zijn verbonden met een werknetwerk dat compatibel is.
- [Acties voor niet-naleving](../protect/actions-for-noncompliance.md). Deze acties zijn een tijdgebonden reeks acties die moeten worden toegepast op niet-compatibele apparaten. Acties omvatten het verzenden van e-mails of meldingen om gebruikers van apparaten te waarschuwen over niet-naleving, extern vergrendelen van apparaten of zelfs het buiten gebruik stellen van niet-compatibele apparaten en het verwijderen van bedrijfsgegevens die erop kunnen staan.

Wanneer u Intune integreert met het Azure AD-[beleid voor voorwaardelijke toegang](#configure-conditional-access) om een nalevingsbeleid af te dwingen, kunt Voorwaardelijke toegang de nalevingsgegevens gebruiken om toegang tot bedrijfsresources voor zowel beheerde apparaten en apparaten die nog niet worden beheerd, op poort plaatsen.

Zie [Regels instellen op apparaten om toegang tot resources in uw organisatie met behulp van Intune toe te staan](../protect/device-compliance-get-started.md) voor meer informatie.

Een beleid voor apparaatnaleving is een van de verschillende methoden in Intune om instellingen op apparaten te configureren. Bij het beheren van instellingen is het belangrijk om te begrijpen welke andere methoden in uw omgeving worden gebruikt voor het configureren van uw apparaten en om conflicten te voorkomen. Zie [Beleidsconflicten voorkomen](#avoid-policy-conflicts) verderop in dit artikel.

## <a name="configure-conditional-access"></a>Voorwaardelijke toegang configureren

Als u uw apparaten en bedrijfsresources wilt beveiligen, kunt u gebruikmaken van het beleid voor voorwaardelijke toegang van Azure Active Directory (Azure AD) met Intune.

Intune geeft de resultaten van uw nalevingsbeleid voor apparaten door aan Azure AD, dat vervolgens het beleid voor voorwaardelijke toegang gebruikt om af te dwingen welke apparaten en apps toegang hebben tot uw bedrijfsresources. Met beleidsregels voor voorwaardelijke toegang kunt u toegang krijgen tot apparaten die niet worden beheerd door Intune. U kunt zelfs nalevingsdetails van [Mobile Threat Defense-partners](../protect/mobile-threat-defense.md) gebruiken die u integreert met Intune.

Hieronder vindt u twee veelvoorkomende methoden voor het gebruik van voorwaardelijke toegang met Intune:

- **Voorwaardelijke toegang op basis van apparaten**, om ervoor te zorgen dat alleen beheerde en compatibele apparaten toegang hebben tot netwerkresources.
- **Op apps gebaseerde voorwaardelijke toegang**, die gebruikmaakt van een app-beveiligingsbeleid voor het beheren van de toegang tot netwerkresources door gebruikers op apparaten die u niet beheert met Intune.

Zie [Meer informatie over voorwaardelijke toegang en Intune](../protect/conditional-access.md) voor meer informatie over het gebruik van voorwaardelijke toegang met Intune.

## <a name="set-up-integration-with-defender-atp"></a>Integratie met Windows Defender ATP instellen

Wanneer u Microsoft Defender Advanced Threat Protection (Defender ATP) integreert met Intune, verbetert u de mogelijkheid om risico's te identificeren en erop te reageren.

Hoewel Intune kan worden geïntegreerd met verschillende [Mobile Threat Defense-partners](../protect/mobile-threat-defense.md), wanneer u Defender ATP gebruikt, hebt u een nauwe integratie tussen de Defender-ATP en Intune met toegang tot uitgebreide opties voor het beveiligen van apparaten, waaronder:

- Beveiligingstaken: naadloze communicatie tussen ATP-en Intune-beheerders over apparaten die risico lopen, het herstellen ervan en de bevestiging wanneer deze risico's worden verholpen.
- Gestroomlijnde onboarding voor Defender ATP op clients.
- Het gebruik van de risicosignalen van een ATP-apparaat in het Intune-nalevingsbeleid.
- Toegang tot mogelijkheden voor *Manipulatiebeveiliging*.

 Zie [Naleving voor Microsoft Defender ATP met voorwaardelijke toegang in Intune afdwingen](../protect/advanced-threat-protection.md) voor meer informatie over Defender ATP met Intune gebruiken.

## <a name="role-based-access-control-requirements"></a>Vereisten voor op rollen gebaseerd toegangsbeheer

Om taken te beheren in het knooppunt eindpuntbeveiliging van het Beheercentrum voor Microsoft Endpoint Manager moet een account:

- Een licentie voor Intune toegewezen krijgen.
- Beschikken over machtigingen voor op rollen gebaseerd toegangsbeheer (RBAC) die gelijk zijn aan de machtigingen van de ingebouwde Intune-rol van **Endpoint Security Manager**. De rol *beheerder van eindpuntbeveiliging* geeft toegang tot het Beheercentrum voor Microsoft Endpoint Manager. Deze rol kan worden gebruikt om beveiligings- en nalevingsfuncties te beheren, waaronder beveiligingsbasislijnen, apparaatcompatibiliteit, voorwaardelijke toegang en Microsoft Defender ATP.

Zie [Op rollen gebaseerd toegangsbeheer (RBAC) met Microsoft Intune](../fundamentals/role-based-access-control.md) voor meer informatie

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>Machtigingen die worden verleend door de rol *beheerder van eindpuntbeveiliging*

U kunt de volgende lijst met machtigingen weergeven in het Beheercentrum van Microsoft Endpoint Manager door naar **Tenantbeheer** > **Rollen** > **Alle rollen** te gaan, en dan **Endpoint Security Manager** > **Eigenschappen**.

**Machtigingen:**

- **Android for Work**
  - Raadplegen
- **Controledatabase**
  - Raadplegen
- **Bedrijfsapparaat-id's**
  - Raadplegen
- **Nalevingsbeleid voor apparaten**
  - Toewijzen
  - Maken
  - Verwijderen
  - Raadplegen
  - Bijwerken
  - Rapporten weergeven
- **Apparaatconfiguraties**
  - Raadplegen
- **Apparaatinschrijvingsbeheerder**
  - Raadplegen
- **Endpoint Protection-rapporten**
  - Raadplegen
- **Inschrijvingsprogramma’s**
  - Apparaat lezen
  - Profiel lezen
  - Token lezen
- **Intune-datawarehouse**
  - Raadplegen
- **Beheerde apps**
  - Raadplegen
- **Beheerde apparaten**
  - Verwijderen
  - Raadplegen
  - Primaire gebruiker instellen
  - Bijwerken
- **Mobiele apps**
  - Raadplegen
- **Organisatie**
  - Raadplegen
- **PolicySets**
  - Raadplegen
- **Hulp op afstand**
  - Raadplegen
- **Externe taken**
  - FileVault-sleutel ophalen.
- **Rollen**
  - Raadplegen
- **Beveiligingsbasislijnen**
  - Toewijzen
  - Maken
  - Verwijderen
  - Raadplegen
  - Bijwerken
- **Beveiligingstaken**
  - Raadplegen
  - Bijwerken
- **Telecomkosten**
  - Raadplegen
- **Voorwaarden**
  - Raadplegen

## <a name="avoid-policy-conflicts"></a>Beleidsconflicten voorkomen

Veel van de instellingen die u kunt configureren voor apparaten, kunnen worden beheerd door verschillende functies in Intune. Deze functies omvatten, maar zijn niet beperkt tot:

- Eindpuntbeveiligingsbeleid
- Beveiligingsbasislijnen
- Beleidsregels voor apparaatconfiguratie
- Inschrijvingsbeleid voor Windows 10

De instellingen die worden gevonden in beleidsregels voor eindpuntbeveiliging zijn bijvoorbeeld een subset van de instellingen die zijn gevonden in *Endpoint Protection* en *apparaatbeperking*-profielen in het configuratiebeleid voor apparaten en die ook worden beheerd via verschillende beveiligingsbasislijnen.

Een manier om conflicten te voorkomen, is het gebruik van geen verschillende basislijnen, exemplaren van dezelfde basislijn of verschillende beleidstypen en instanties om dezelfde instellingen op een apparaat te beheren. Hiervoor moet worden gepland welke methoden u gaat gebruiken voor het implementeren van configuraties op verschillende apparaten. Wanneer u meerdere methoden of exemplaren van dezelfde methode gebruikt om dezelfde instelling te configureren, moet u ervoor zorgen dat uw verschillende methoden overeenkomen of niet zijn geïmplementeerd op dezelfde apparaten.

Als er conflicten optreden, kunt u de ingebouwde hulpprogramma's van Intune gebruiken om de bron van deze conflicten te identificeren en op te lossen. Zie voor meer informatie:

- [Beleidsregels en profielen voor het oplossen van problemen in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Uw beveiligingsbasislijnen bewaken](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Volgende stappen

Configureren:

- [Beveiligingsbasislijnen](../protect/security-baselines.md)
- [Nalevingsbeleid](../protect/device-compliance-get-started.md)
- [Beleid voor voorwaardelijke toegang](#configure-conditional-access)
- [Integratie met Windows Defender ATP](../protect/advanced-threat-protection.md)

---
title: Nalevingsbeleid voor apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Ga aan de slag met het gebruik van apparaatnalevingsbeleid, overzicht van status- en ernstniveaus, gebruik van respijtperiode-status, werken met voorwaardelijke toegang, en verwerking van apparaten zonder toegewezen beleid.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 559d9a704f0b33e3fda3adf628626b56ff263de3
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989719"
---
# <a name="set-rules-on-devices-to-allow-access-to-resources-in-your-organization-using-intune"></a>Regels instellen op apparaten om toegang tot resources in uw organisatie met behulp van Intune toe te staan

Veel MDM-oplossingen (mobile device management) beschermen bedrijfsgegevens, doordat gebruikers en apparaten aan bepaalde vereisten moeten voldoen. In Intune wordt deze functie 'nalevingsbeleid' genoemd. Het nalevingsbeleid bepaalt aan welke regels en instellingen apparaten moeten voldoen om compatibel te zijn. Indien gecombineerd met voorwaardelijke toegang kunnen beheerders gebruikers en apparaten blokkeren die niet aan de regels voldoen.

Zo kan een Intune-beheerder eisen dat:

- eindgebruikers een wachtwoord gebruiken voor toegang tot bedrijfsgegevens op mobiele apparaten
- het apparaat niet jailbroken of geroot is
- er een minimum- of maximumversie van het besturingssysteem op het apparaat staat
- het apparaat zich op of onder het apparaatdreigingsniveau bevindt

U kunt deze functie ook gebruiken om de nalevingsstatus op apparaten in uw organisatie te bewaken.

> [!IMPORTANT]
> Intune volgt het incheckschema van het apparaat voor alle nalevingsevaluaties op het apparaat. [Vernieuwingscycli voor beleidsregels en profielen](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) bevat de geschatte vernieuwingstijden.

<!---### Actions for noncompliance

You can specify what needs to happen when a device is determined as noncompliant. This can be a sequence of actions during a specific time.
When you specify these actions, Intune will automatically initiate them in the sequence you specify. See the following example of a sequence of
actions for a device that continues to be in the noncompliant status for
a week:

- When the device is first determined to be noncompliant, an email with noncompliant notification is sent to the user.

- 3 days after initial noncompliance state, a follow up reminder is sent to the user.

- 5 days after initial noncompliance state, a final reminder with a notification that access to company resources will be blocked on the device in 2 days if the compliance issues are not remediated is sent to the user.

- 7 days after initial noncompliance state, access to company resources is blocked. This requires that you have Conditional Access policy that specifies that access from noncompliant devices should    be blocked for services such as Exchange and SharePoint.

### Grace Period

This is the time between when a device is first determined as
noncompliant to when access to company resources on that device is blocked. This time allows for time that the user has to resolve
compliance issues on the device. You can also use this time to create your action sequences to send notifications to the user before their access is blocked.

Remember that you need to implement Conditional Access policies in addition to compliance policies in order for access to company resources to be blocked.--->

## <a name="device-compliance-policies-work-with-azure-ad"></a>Apparaatnalevingsbeleid werkt met Azure AD

Intune maakt gebruik van [voorwaardelijke toegang](../protect/conditional-access.md) om naleving af te dwingen. Voorwaardelijke toegang is een technologie van Azure Active Directory (Azure AD).

Wanneer een apparaat is ingeschreven bij Intune, wordt het Azure AD-registratieproces gestart, en worden de apparaatgegevens bijgewerkt in Azure AD. Een van de belangrijkste apparaatgegevens is de nalevingsstatus van het apparaat. Deze nalevingsstatus wordt door de beleidsregels voor voorwaardelijke toegang gebruikt om de toegang tot e-mail en andere organisatieresources toe te staan of te blokkeren.

Meer informatie over voorwaardelijke toegang en Intune:

- [Gebruikelijke manieren om voorwaardelijke toegang met Intune te gebruiken](conditional-access-intune-common-ways-use.md)

Meer informatie over voorwaardelijke toegang vindt u in de Azure AD-documentatie:
  - [Wat is voorwaardelijke toegang](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
  - [Wat is een apparaat-id](https://docs.microsoft.com/azure/active-directory/device-management-introduction)

## <a name="ways-to-use-device-compliance-policies"></a>Nalevingsbeleid voor apparaten gebruiken

### <a name="with-conditional-access"></a>Met voorwaardelijke toegang

Voor apparaten die aan beleidsregels voldoen, kunt u deze apparaten toegang verlenen tot e-mail en andere organisatieresources. Als de apparaten niet aan beleidsregels voldoen, krijgen ze geen toegang tot organisatieresources. Dit wordt voorwaardelijke toegang genoemd.

### <a name="without-conditional-access"></a>Zonder voorwaardelijke toegang

U kunt nalevingsbeleid voor apparaten ook zonder voorwaardelijke toegang gebruiken. Bij onafhankelijk gebruik van nalevingsbeleid worden de betreffende apparaten geëvalueerd en samen met hun nalevingsstatus gerapporteerd. U kunt bijvoorbeeld rapporteren over het aantal apparaten dat niet is versleuteld of over welke apparaten jailbroken of geroot zijn. Wanneer u nalevingsbeleid zonder voorwaardelijke toegang gebruikt, zijn er geen toegangsbeperkingen tot bedrijfsresources.

## <a name="ways-to-deploy-device-compliance-policies"></a>Nalevingsbeleid voor apparaten implementeren

U kunt nalevingsbeleid implementeren voor gebruikers in gebruikersgroepen of apparaten in apparaatgroepen. Wanneer er nalevingsbeleid wordt geïmplementeerd voor een gebruiker, worden alle apparaten van de gebruiker gecontroleerd op naleving. Het gebruik van apparaatgroepen maakt rapportage over naleving in dit scenario eenvoudiger.

Intune bevat ook een set ingebouwde instellingen voor nalevingsbeleid. Het volgende ingebouwde beleid wordt geëvalueerd op alle apparaten die zijn ingeschreven in Intune:

- **Apparaten waaraan geen nalevingsbeleid is toegewezen markeren als**: Dit is een standaardactie voor niet-naleving. Deze eigenschap heeft twee waarden:

  - **Compatibel** (*standaard*): beveiligingsfunctie uit
  - **Niet compatibel**: beveiligingsfunctie aan

  Als er geen nalevingsbeleid aan een apparaat is toegewezen, wordt dit apparaat standaard als incompatibel beschouwd. Als u voorwaardelijke toegang met nalevingsbeleid gebruikt, is het raadzaam de standaardinstelling te wijzigen in **Niet compatibel**. Als een eindgebruiker incompatibel is omdat er geen beleid is toegewezen, wordt `No compliance policies have been assigned` vermeld in de [bedrijfsportal-app](../apps/company-portal-app.md).

- **Verbeterde jailbreakdetectie** (*Is van toepassing op iOS/iPadOS*): als deze instelling is ingeschakeld, wordt de status van apparaten met jailbreak vaker weergegeven op iOS/iPadOS-apparaten. Deze instelling is alleen van invloed op apparaten waarop een nalevingsbeleid is gericht waarmee apparaten met jailbreak worden geblokkeerd. Door het inschakelen van deze eigenschap worden de locatieservices van het apparaat gebruikt. Ook kan dit invloed hebben op het batterijverbruik. De locatiegegevens van de gebruiker worden niet door Intune opgeslagen en worden alleen gebruikt om jailbreakdetectie vaker te activeren op de achtergrond. 

  Wanneer u deze instelling inschakelt, moeten apparaten:
  - Locatieservices op het niveau van het besturingssysteem inschakelen.
  - De bedrijfsportal altijd toestaan om locatieservices te gebruiken.

  Verbeterde detectie werkt via de locatieservices. De evaluatie wordt geactiveerd door de bedrijfsportal-app te openen of het apparaat een aanzienlijke afstand van 500 meter of meer te verplaatsen. Op apparaten met iOS 13 en hoger moeten gebruikers voor deze functie steeds de optie Altijd toestaan selecteren wanneer ze worden gevraagd door te gaan; hierdoor kan hun locatie op de achtergrond worden gebruikt in de bedrijfsportal. Als gebruikers toegang tot hun locatie niet altijd toestaan en een beleid hebben ingesteld waarbij deze instelling is geconfigureerd, wordt hun apparaat gemarkeerd als Niet-compatibel. Houd er rekening mee dat Intune niet kan garanderen dat elke grote locatiewijziging ervoor zorgt dat er op jailbreakdetectie wordt gecontroleerd, aangezien dit afhankelijk is van de netwerkverbinding van een apparaat op dat moment.

- **Geldigheidsperiode van nalevingsstatus (dagen)** : Voer de tijdsduur in dat apparaten de status voor alle ontvangen nalevingsbeleidsregels moeten rapporteren. Apparaten die niet binnen deze tijdsduur de status retourneren, worden als Niet compatibel beschouwd. De standaardwaarde is 30 dagen. De maximumwaarde is 120 dagen. De minimumwaarde is 1 dag.

  Deze instelling wordt weergegeven als het standaardnalevingsbeleid **Is actief** (**Apparaten** > **Controleren** > **Naleving van instelling**). De achtergrondtaak voor dit beleid wordt één keer per dag uitgevoerd.

U kunt dit ingebouwde beleid gebruiken om deze instellingen te bewaken. In Intune worden [controles voor updates ook vernieuwd](create-compliance-policy.md#refresh-cycle-times) met verschillende intervallen, afhankelijk van het apparaatplatform. [Algemene vragen, problemen en oplossingen met apparaatbeleid en -profielen in Microsoft Intune](../configuration/device-profile-troubleshoot.md) is een goede resource.

Nalevingsrapporten zijn een uitstekende manier om de status van apparaten te controleren. [Nalevingsbeleid bewaken](compliance-policy-monitor.md) bevat enkele richtlijnen.

## <a name="non-compliance-and-conditional-access-on-the-different-platforms"></a>Niet-naleving en voorwaardelijke toegang op verschillende platforms

In de volgende tabel wordt beschreven hoe niet-compatibele instellingen worden beheerd wanneer een nalevingsbeleid wordt gebruikt in combinatie met beleid voor voorwaardelijke toegang.

---------------------------

|**Beleidsinstelling**| **Platform** |
| --- | ----|
| **Configuratie van pincode of wachtwoord** | - **Android 4.0 en hoger**: In quarantaine<br>- **Samsung Knox Standard 4.0 en hoger**: In quarantaine<br>- **Android Enterprise**: In quarantaine  <br>  <br>- **iOS 8.0 en hoger**: Hersteld<br>- **macOS 10.11 en hoger**: Hersteld  <br>  <br>- **Windows 8.1 en hoger**: Hersteld<br>- **Windows Phone 8.1 en hoger**: Hersteld|
| **Apparaatversleuteling** | - **Android 4.0 en hoger**: In quarantaine<br>- **Samsung Knox Standard 4.0 en hoger**: In quarantaine<br>- **Android Enterprise**: In quarantaine<br><br>- **iOS 8.0 en hoger**: Hersteld (door een pincode in te stellen)<br>- **macOS 10.11 en hoger**: Hersteld (door een pincode in te stellen)<br><br>- **Windows 8.1 en hoger**: Niet van toepassing<br>- **Windows Phone 8.1 en hoger**: Hersteld |
| **Opengebroken of geroot apparaat** | - **Android 4.0 en hoger**: In quarantaine (geen instelling)<br>- **Samsung Knox Standard 4.0 en hoger**: In quarantaine (geen instelling)<br>- **Android Enterprise**: In quarantaine (geen instelling)<br><br>- **iOS 8.0 en hoger**: In quarantaine (geen instelling)<br>- **macOS 10.11 en hoger**: Niet van toepassing<br><br>- **Windows 8.1 en hoger**: Niet van toepassing<br>- **Windows Phone 8.1 en hoger**: Niet van toepassing |
| **E-mailprofiel** | - **Android 4.0 en hoger**: Niet van toepassing<br>- **Samsung Knox Standard 4.0 en hoger**: Niet van toepassing<br>- **Android Enterprise**: Niet van toepassing<br><br>- **iOS 8.0 en hoger**: In quarantaine<br>- **macOS 10.11 en hoger**: In quarantaine<br><br>- **Windows 8.1 en hoger**: Niet van toepassing<br>- **Windows Phone 8.1 en hoger**: Niet van toepassing |
| **Minimale versie van het besturingssysteem** | - **Android 4.0 en hoger**: In quarantaine<br>- **Samsung Knox Standard 4.0 en hoger**: In quarantaine<br>- **Android Enterprise**: In quarantaine<br><br>- **iOS 8.0 en hoger**: In quarantaine<br>- **macOS 10.11 en hoger**: In quarantaine<br><br>- **Windows 8.1 en hoger**: In quarantaine<br>- **Windows Phone 8.1 en hoger**: In quarantaine |
| **Maximale versie van het besturingssysteem** | - **Android 4.0 en hoger**: In quarantaine<br>- **Samsung Knox Standard 4.0 en hoger**: In quarantaine<br>- **Android Enterprise**: In quarantaine<br><br>- **iOS 8.0 en hoger**: In quarantaine<br>- **macOS 10.11 en hoger**: In quarantaine<br><br>- **Windows 8.1 en hoger**: In quarantaine<br>- **Windows Phone 8.1 en hoger**: In quarantaine |
| **Windows Health Attestation** | - **Android 4.0 en hoger**: Niet van toepassing<br>- **Samsung Knox Standard 4.0 en hoger**: Niet van toepassing<br>- **Android Enterprise**: Niet van toepassing<br><br>- **iOS 8.0 en hoger**: Niet van toepassing<br>- **macOS 10.11 en hoger**: Niet van toepassing<br><br>- **Windows 10 en Windows 10 Mobile**: In quarantaine<br>- **Windows 8.1 en hoger**: In quarantaine<br>- **Windows Phone 8.1 en hoger**: Niet van toepassing |

---------------------------

**Hersteld**: Het besturingssysteem van het apparaat dwingt naleving af. De gebruiker wordt bijvoorbeeld gedwongen een pincode in te stellen.

**In quarantaine**: Het besturingssysteem van het apparaat dwingt geen naleving af. Bij Android- en Android Enterprise-apparaten wordt de gebruiker bijvoorbeeld niet gedwongen het apparaat te versleutelen. Als het apparaat niet compatibel is, worden de volgende acties uitgevoerd:

- Het apparaat wordt geblokkeerd als een beleid voor voorwaardelijke toegang van toepassing is voor de gebruiker.
- Via de bedrijfsportal-app wordt de gebruiker op de hoogte gebracht van eventuele nalevingsproblemen.

## <a name="next-steps"></a>Volgende stappen

- [Maak een beleid](create-compliance-policy.md) en bekijk de vereisten.
- Bekijk de nalevingsinstellingen voor de verschillende apparaatplatforms:

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows Phone 8.1](compliance-policy-create-windows-8-1.md)
  - [Windows 8.1 en hoger](compliance-policy-create-windows-8-1.md)
  - [Windows 10 en hoger](compliance-policy-create-windows.md)

- [Naslag voor beleidsentiteiten](../developer/reports-ref-policy.md) bevat meer informatie over de beleidsentiteiten voor Intune-datawarehouse.

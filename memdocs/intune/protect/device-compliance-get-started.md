---
title: Nalevingsbeleid voor apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Aan de slag met het gebruik van beleidsregels voor compliance, inclusief instellingen voor compliancebeleid en compliancebeleid voor apparaten voor Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
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
ms.openlocfilehash: 6bb3397432f1c171418ea99510cb04f1bdefc639
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252789"
---
# <a name="use-compliance-policies-to-set-rules-for-devices-you-manage-with-intune"></a>Beleidsregels voor compliance gebruiken om regels in te stellen voor apparaten die u beheert met Intune

Met MDM-oplossingen (mobile device management), zoals Intune, beschermt u bedrijfsgegevens, doordat gebruikers en apparaten aan bepaalde vereisten moeten voldoen. In Intune wordt deze functie *nalevingsbeleid* genoemd.

Nalevingsbeleid in Intune:

- De regels en instellingen vaststellen waaraan gebruikers en apparaten moeten voldoen om compatibel te zijn.
- Neem daarbij ook acties op die van toepassing zijn op apparaten die niet compatibel zijn. Met acties voor niet-naleving kunnen gebruikers op de hoogte worden gebracht van de voorwaarden van niet-naleving en de gegevens op niet-compatibele apparaten beveiligen.
- Kan [worden gecombineerd met Voorwaardelijke toegang](#integrate-with-conditional-access), waardoor gebruikers en apparaten die niet aan de regels voldoen vervolgens kunnen worden geblokkeerd.

Er zijn twee onderdelen voor nalevingsbeleid in Intune:

- **Instellingen voor nalevingsbeleid**: Instellingen voor de hele tenant, die fungeren als een ingebouwd compliancebeleid dat door elk apparaat wordt ontvangen. Instellingen van het nalevingsbeleid bepalen de ondergrens van hoe compliancebeleid functioneert in uw Intune-omgeving, waarbij ook van een apparaat dat geen compliancebeleid heeft ontvangen, wordt vastgesteld of het compatibel is of niet.

- **Compliancebeleid van een apparaat**: Platformspecifieke regels die u configureert en implementeert voor groepen gebruikers of apparaten.  Met deze regels worden de vereisten voor apparaten gedefinieerd, zoals minimale besturingssystemen of het gebruik van schijfversleuteling. Apparaten moeten voldoen aan deze regels om te worden beschouwd als een apparaat dat het beleid naleeft.

Net als bij andere beleidsregels van Intune, zijn evaluaties van het compliancebeleid voor een apparaat afhankelijk van wanneer het apparaat wordt ingecheckt bij Intune en [de vernieuwingscycli van het beleid en het profiel](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="compliance-policy-settings"></a>Instellingen voor nalevingsbeleid

*Instellingen voor nalevingsbeleid* zijn instellingen voor de hele tenant die bepalen hoe de complianceservice van Intune met uw apparaten communiceert. Deze instellingen zijn anders dan de instellingen die u configureert in een compliancebeleid voor apparaten.

Als u de instellingen voor het nalevingsbeleid wilt beheren, meldt u zich aan bij [Beheercentrum voor Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) en gaat u naar **Eindpuntbeveiliging** > **Apparaatcompatibiliteit** > **Instellingen voor nalevingsbeleid**.

Instellingen voor nalevingsbeleid bevatten de volgende instellingen:

- **Apparaten waaraan geen nalevingsbeleid is toegewezen markeren als**

  Met deze instelling bepaalt u hoe Intune omgaat met apparaten waaraan geen compliancebeleid voor apparaten is toegewezen. Deze instelling heeft twee waarden:
  - **Compatibel** (*standaard*): Deze beveiligingsfunctie is uitgeschakeld. Apparaten waar geen apparaatnalevingsbeleid naartoe is gestuurd, worden beschouwd als *compatibel*.
  - **Niet compatibel**: Deze beveiligingsfunctie is ingeschakeld. Apparaten die geen apparaatnalevingsbeleid hebben ontvangen, worden beschouwd als niet-compatibel.

  Als u Voorwaardelijke toegang met uw nalevingsbeleid voor apparaten gebruikt, raden we u aan deze instelling te wijzigen in **Niet-compatibel** om ervoor te zorgen dat alleen apparaten die zijn bevestigd als compatibel, toegang hebben tot uw resources.

  Als een eindgebruiker niet compatibel is omdat er geen beleid aan hem of haar is toegewezen, wordt in de [bedrijfsportal-app](../apps/company-portal-app.md) vermeld: Er is geen compliancebeleid toegewezen.

- **Verbeterde jailbreakdetectie** (*alleen van toepassing op iOS/iPadOS*)

  Deze instelling werkt alleen op apparaten waarop u een apparaatcompliancebeleid richt waarmee gekraakte apparaten worden geblokkeerd.  (Zie de instellingen voor [Apparaatstatus](compliance-policy-create-ios.md#device-health) voor iOS/iPadOS).

  Deze instelling heeft twee waarden:

  - **Uitgeschakeld** (*standaard*): Deze beveiligingsfunctie is uitgeschakeld. Deze instelling heeft geen invloed op uw apparaten die een apparaatnalevingsbeleid ontvangen waarmee gekraakte apparaten worden geblokkeerd.
  - **Ingeschakeld**: Deze beveiligingsfunctie is ingeschakeld. Apparaten die een apparaatnalevingsbeleid ontvangen om gekraakte apparaten te blokkeren, gebruiken de Verbeterde jailbreakdetectie.

  Wanneer deze functie is ingeschakeld op een van toepassing zijnd iOS/iPadOS-apparaat, wordt het apparaat:

  - Locatieservices op het niveau van het besturingssysteem ingeschakeld.
  - Toegang tot locatieservices verleend aan de Bedrijfsportal.
  - Gebruikgemaakt van de locatieservices om jailbreakdetectie vaker op de achtergrond te activeren. De locatiegegevens van de gebruiker worden niet opgeslagen met Intune.

  Verbeterde jailbreakdetectie voert een evaluatie uit wanneer:

  - De bedrijfsportal-app wordt geopend
  - Het apparaat fysiek een aanzienlijke afstand van ongeveer 500 meter of meer wordt verplaatst. Intune kan niet garanderen dat elke aanzienlijke locatiewijziging resulteert in een controle op jailbreakdetectie, aangezien deze controle afhankelijk is van de netwerkverbinding van een apparaat op dat moment.

  Op apparaten met iOS 13 en hoger moeten gebruikers voor deze functie steeds de optie *Altijd toestaan* selecteren wanneer hen wordt gevraagd door te gaan; hierdoor kan hun locatie op de achtergrond worden gebruikt in de Bedrijfsportal. Als gebruikers toegang tot hun locatie niet altijd toestaan en een beleid hebben ingesteld waarbij deze instelling is geconfigureerd, wordt hun apparaat gemarkeerd als niet-compatibel.

- **Geldigheidsperiode van nalevingsstatus (dagen)**

  Geef een periode op waarin apparaten met succes moeten rapporteren over al hun ontvangen nalevingsbeleidsregels. Als een apparaat de nalevingsstatus voor een beleid niet rapporteert voordat de geldigheidsperiode is verstreken, wordt het apparaat als niet-compatibel behandeld.

  De periode is standaard ingesteld op 30 dagen. U kunt een periode van 1 tot 120 dagen configureren.

  U kunt details over de naleving van het apparaat weergeven voor de instelling voor de geldigheidsperiode. Meld u aan bij [Beheercentrum voor Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) en ga naar **Apparaten** > **Controleren** > **Instelling compliance**. Deze instelling heeft de naam **Is actief** in de kolom *Instelling*.  Zie [Apparaatcompatibiliteit controleren](compliance-policy-monitor.md) voor meer informatie over deze en gerelateerde weergaven over de status van naleving.

## <a name="device-compliance-policies"></a>Nalevingsbeleid voor apparaten

Intune apparaatnalevingsbeleid:

- De regels en instellingen vaststellen waaraan gebruikers en beheerde apparaten moeten voldoen om compatibel te zijn. Voorbeelden van regels zijn de vereiste dat op apparaten een minimale versie van het besturingssysteem wordt uitgevoerd, niet gekraakt of geroot zijn, en zich op of onder een *bedreigingsniveau* bevinden, zoals opgegeven door de beheersoftware voor bedreigingen die u hebt geïntegreerd met Intune.
- Ondersteuningsacties die van toepassing zijn op apparaten die niet voldoen aan uw nalevingsregels. Voorbeelden van acties zijn op afstand vergrendelen of het verzenden van een e-mail van een apparaatgebruiker over de apparaatstatus, zodat het probleem kan worden opgelost.
- Implementeer voor gebruikers in gebruikersgroepen of apparaten in apparaatgroepen. Wanneer er nalevingsbeleid wordt geïmplementeerd voor een gebruiker, worden alle apparaten van de gebruiker gecontroleerd op naleving. Het gebruik van apparaatgroepen maakt rapportage over naleving in dit scenario eenvoudiger.

Als u Voorwaardelijke toegang gebruikt, kunnen voor uw beleid voor Voorwaardelijke toegang de nalevingsresultaten van uw apparaat worden gebruikt om toegang tot resources van niet-compatibele apparaten te blokkeren.

De beschikbare instellingen die u in een compliancebeleid voor apparaten kunt opgeven, zijn afhankelijk van het platformtype dat u selecteert bij het maken van een beleid. Verschillende platformen voor apparaten ondersteunen verschillende instellingen en voor elk platformtype is een afzonderlijk beleid vereist.  

De volgende onderwerpen bevatten een koppeling naar artikelen die specifiek gaan over verschillende aspecten van het configuratiebeleid voor apparaten.

- [**Acties voor niet-naleving**](actions-for-noncompliance.md): Elk nalevingsbeleid voor apparaten bevat een of meer acties voor niet-naleving. Deze acties zijn regels die worden toegepast op apparaten die niet voldoen aan de voorwaarden die u in het beleid hebt ingesteld.

  Elk nalevingsbeleid voor apparaten bevat standaard de actie om een apparaat als niet-compatibel te markeren als het niet kan voldoen aan een beleidsregel. Middels het beleid worden vervolgens op het apparaat alle aanvullende acties voor niet-naleving toegepast die u hebt geconfigureerd, op basis van de planningen die u voor deze acties hebt ingesteld.

  Via acties voor niet-naleving kunnen gebruikers worden gewaarschuwd wanneer het apparaat niet compatibel is of kunnen gegevens worden beveiligd die zich op een apparaat kunnen bevinden. Voorbeelden van acties zijn:

  - **Verzenden van e-mailwaarschuwingen** naar gebruikers en groepen met details over het apparaat dat niet compatibel is. U kunt het beleid zo configureren dat er direct een e-mail wordt verzonden nadat het apparaat is gemarkeerd als niet-compatibel, en vervolgens periodiek opnieuw, totdat het apparaat compatibel is.
  - **Apparaten op afstand vergrendelen** die enige tijd niet compatibel zijn.
  - **Apparaten buiten gebruik stellen** nadat deze al enige tijd niet compatibel zijn. Met deze actie verwijdert u het apparaat uit Intune-beheer en verwijdert u alle bedrijfsgegevens van het apparaat.

- [**Netwerklocaties configureren**](use-network-locations.md): Ondersteund door Android-apparaten. U kunt *netwerklocaties* configureren en vervolgens die locaties gebruiken als een nalevingsregel voor apparaten. Met dit type regel kunt u een apparaat als niet-compatibel markeren wanneer het zich buiten een opgegeven netwerk bevindt of dit netwerk verlaat. Voordat u een locatieregel kunt opgeven, moet u de netwerklocaties configureren.

- [**Een beleid maken**](create-compliance-policy.md): Met de informatie in dit artikel kunt u de vereisten bekijken, de opties voor het configureren van regels doorlopen, acties voor niet-naleving opgeven en het beleid toewijzen aan groepen. Dit artikel bevat ook informatie over de tijden voor het vernieuwen van het beleid.

  Bekijk de instellingen voor apparaatcompatibiliteit voor de verschillende apparaatplatformen:

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows 8.1 en hoger](compliance-policy-create-windows-8-1.md)
  - [Windows 10 en hoger](compliance-policy-create-windows.md)

## <a name="monitor-compliance-status"></a>Status voor naleving bewaken

Intune bevat een dashboard voor apparaatcompatibiliteit dat u gebruikt om de nalevingsstatus van apparaten te controleren en om in te zoomen op beleid en apparaten voor meer informatie. Zie [Controleren op naleving van het apparaat](compliance-policy-monitor.md) voor meer informatie over dit dashboard.

## <a name="integrate-with-conditional-access"></a>Integreren met Voorwaardelijke toegang

Wanneer u Voorwaardelijke toegang gebruikt, kunt u uw beleid voor Voorwaardelijke toegang configureren om de resultaten van het nalevingsbeleid van uw apparaat te gebruiken om te bepalen welke apparaten toegang krijgen tot de resources van uw organisatie. Dit toegangsbeheer is aanvullend op en gescheiden van de acties voor niet-naleving die u in uw nalevingsbeleid voor apparaten opneemt.

Wanneer een apparaat wordt ingeschreven bij Intune, wordt het geregistreerd in Microsoft Azure AD. De nalevingsstatus voor apparaten wordt gerapporteerd aan Microsoft Azure AD. Als u in uw beleid voor Voorwaardelijke toegang het Toegangsbeheer hebt ingesteld op *Vereisen dat het apparaat wordt gemarkeerd als compatibel*, dan gebruikt Voorwaardelijke toegang die nalevingsstatus om te bepalen of toegang tot e-mail en andere resources van de organisatie wordt toegekend of geblokkeerd.

Als u de nalevingsstatus van het apparaat gebruikt met beleidsregels voor Voorwaardelijke toegang, raadpleegt u hoe in uw tenant *Apparaten waaraan geen nalevingsbeleid is toegewezen markeren als*, dat u beheert onder [Instellingen nalevingsbeleid](#compliance-policy-settings), is geconfigureerd.

Zie [Voorwaardelijke toegang op basis van het apparaat](conditional-access-intune-common-ways-use.md#device-based-conditional-access) voor meer informatie over het gebruik van Voorwaardelijke toegang met uw nalevingsbeleid voor apparaten

Meer informatie over voorwaardelijke toegang vindt u in de Microsoft Azure AD-documentatie:

- [Wat is voorwaardelijke toegang](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Wat is een apparaat-id](https://docs.microsoft.com/azure/active-directory/device-management-introduction)

### <a name="reference-for-non-compliance-and-conditional-access-on-the-different-platforms"></a>Naslag voor niet-naleving en voorwaardelijke toegang op verschillende platformen

In de volgende tabel wordt beschreven hoe niet-compatibele instellingen worden beheerd wanneer een nalevingsbeleid wordt gebruikt in combinatie met beleid voor voorwaardelijke toegang.

- **Hersteld**: Het besturingssysteem van het apparaat dwingt naleving af. De gebruiker wordt bijvoorbeeld gedwongen een pincode in te stellen.

- **In quarantaine**: Het besturingssysteem van het apparaat dwingt geen naleving af. Bij Android- en Android Enterprise-apparaten wordt de gebruiker bijvoorbeeld niet gedwongen het apparaat te versleutelen. Als het apparaat niet compatibel is, worden de volgende acties uitgevoerd:
  - Het apparaat wordt geblokkeerd als een beleid voor voorwaardelijke toegang van toepassing is voor de gebruiker.
  - Via de bedrijfsportal-app wordt de gebruiker op de hoogte gebracht van eventuele nalevingsproblemen.

---------------------------

|**Beleidsinstelling**| **Platform** |
| --- | ----|
| **Configuratie van pincode of wachtwoord** | - **Android 4.0 en hoger**: In quarantaine<br>- **Samsung Knox Standard 4.0 en hoger**: In quarantaine<br>- **Android Enterprise**: In quarantaine  <br>  <br>- **iOS 8.0 en hoger**: Hersteld<br>- **macOS 10.11 en hoger**: Hersteld  <br>  <br>- **Windows 8.1 en hoger**: Hersteld|
| **Apparaatversleuteling** | - **Android 4.0 en hoger**: In quarantaine<br>- **Samsung Knox Standard 4.0 en hoger**: In quarantaine<br>- **Android Enterprise**: In quarantaine<br><br>- **iOS 8.0 en hoger**: Hersteld (door een pincode in te stellen)<br>- **macOS 10.11 en hoger**: Hersteld (door een pincode in te stellen)<br><br>- **Windows 8.1 en hoger**: Niet van toepassing|
| **Opengebroken of geroot apparaat** | - **Android 4.0 en hoger**: In quarantaine (geen instelling)<br>- **Samsung Knox Standard 4.0 en hoger**: In quarantaine (geen instelling)<br>- **Android Enterprise**: In quarantaine (geen instelling)<br><br>- **iOS 8.0 en hoger**: In quarantaine (geen instelling)<br>- **macOS 10.11 en hoger**: Niet van toepassing<br><br>- **Windows 8.1 en hoger**: Niet van toepassing |
| **E-mailprofiel** | - **Android 4.0 en hoger**: Niet van toepassing<br>- **Samsung Knox Standard 4.0 en hoger**: Niet van toepassing<br>- **Android Enterprise**: Niet van toepassing<br><br>- **iOS 8.0 en hoger**: In quarantaine<br>- **macOS 10.11 en hoger**: In quarantaine<br><br>- **Windows 8.1 en hoger**: Niet van toepassing |
| **Minimale versie van het besturingssysteem** | - **Android 4.0 en hoger**: In quarantaine<br>- **Samsung Knox Standard 4.0 en hoger**: In quarantaine<br>- **Android Enterprise**: In quarantaine<br><br>- **iOS 8.0 en hoger**: In quarantaine<br>- **macOS 10.11 en hoger**: In quarantaine<br><br>- **Windows 8.1 en hoger**: In quarantaine|
| **Maximale versie van het besturingssysteem** | - **Android 4.0 en hoger**: In quarantaine<br>- **Samsung Knox Standard 4.0 en hoger**: In quarantaine<br>- **Android Enterprise**: In quarantaine<br><br>- **iOS 8.0 en hoger**: In quarantaine<br>- **macOS 10.11 en hoger**: In quarantaine<br><br>- **Windows 8.1 en hoger**: In quarantaine |
| **Windows Health Attestation** | - **Android 4.0 en hoger**: Niet van toepassing<br>- **Samsung Knox Standard 4.0 en hoger**: Niet van toepassing<br>- **Android Enterprise**: Niet van toepassing<br><br>- **iOS 8.0 en hoger**: Niet van toepassing<br>- **macOS 10.11 en hoger**: Niet van toepassing<br><br>- **Windows 10**: In quarantaine<br>- **Windows 8.1 en hoger**: In quarantaine |

---------------------------

## <a name="next-steps"></a>Volgende stappen

- [Locaties configureren](../protect/use-network-locations.md) voor gebruik met Android-apparaten
- [Beleid maken en implementeren](../protect/create-compliance-policy.md) en vereisten beoordelen
- [Apparaatcompatibiliteit bewaken](../protect/compliance-policy-monitor.md)
- [Algemene vragen, problemen en oplossingen met apparaatbeleid en -profielen in Microsoft Intune](../configuration/device-profile-troubleshoot.md)
- [Naslag voor beleidsentiteiten](../developer/reports-ref-policy.md) bevat meer informatie over de beleidsentiteiten voor Intune Data Warehouse

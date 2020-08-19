---
title: E-mailinstellingen in Microsoft Intune configureren - Azure | Microsoft Docs
titleSuffix: ''
description: Een e-mailprofiel maken in Microsoft Intune en dit profiel implementeren voor Android-apparaatbeheer-, Android Enterprise-, iOS-, iPadOS- en Windows-apparaten. Gebruik e-mailprofielen om algemene e-mailinstellingen te configureren, inclusief een e-mailserver en verificatiemethoden om verbinding te maken met zakelijke e-mail op apparaten die u beheert.
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: de260f56753e292ed95ac22c76b9cc16457c981b
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88145994"
---
# <a name="add-email-settings-to-devices-using-intune"></a>E-mailinstellingen toevoegen aan apparaten met Intune

Microsoft Intune omvat verschillende e-mailinstellingen die u op apparaten in uw organisatie kunt implementeren. Een IT-beheerder maakt e-mailprofielen met specifieke instellingen om verbinding te maken met een e-mailserver, zoals Office 365 en Gmail. Eindgebruikers kunnen vervolgens verbinding maken, verifiëren en het e-mailaccount van hun organisatie op hun mobiele apparaten synchroniseren. Door een e-mailprofiel te maken en te implementeren, kunt u bevestigen dat instellingen op veel apparaten standaard zijn. Ook kan dit het aantal ondersteuningsaanvragen verminderen dat wordt ingediend door eindgebruikers die de juiste e-mailinstellingen niet weten.

U kunt e-mailprofielen gebruiken om de ingebouwde e-mailinstellingen te configureren voor de volgende apparaten:

- Android-apparaatbeheer op Samsung Knox Standard 5.0 en hoger
- Android Enterprise
- iOS 11.0 en hoger
- iPadOS 13.0 en hoger
- Windows 10 (desktop)

In dit artikel wordt uitgelegd hoe u een e-mailprofiel maakt in Microsoft Intune. Het bevat ook koppelingen naar de verschillende platforms voor meer specifieke instellingen.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: Kies het platform van uw apparaten. Uw opties zijn:  

        - **Android-apparaatbeheer** (alleen Samsung Android Knox Standard)
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **Windows 10 en hoger**

    - **Profiel**: Selecteer **E-mail**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **Windows 10: E-mailinstellingen voor alle Windows 10-apparaten**.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Welke instellingen u kunt configureren in **Configuratie-instellingen**, is afhankelijk van het platform dat u hebt gekozen. Kies uw platform voor gedetailleerde instellingen:

    - [Android-apparaatbeheer (Samsung Android Knox Standard)](email-settings-android.md)
    - [Android Enterprise](email-settings-android-enterprise.md)
    - [iOS/iPadOS](email-settings-ios.md)
    - [Windows 10](email-settings-windows-10.md)

8. Selecteer **Volgende**.
9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruikers of apparaatgroepen die uw profiel zullen ontvangen. Zie [Wat u moet weten](#what-you-need-to-know) (in dit artikel) voor meer informatie over het toewijzen van profielen. [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) biedt ook enkele richtlijnen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="what-you-need-to-know"></a>Wat u dient te weten

- E-mailprofielen worden geïmplementeerd voor de gebruiker die het apparaat heeft geregistreerd. Om het e-mailprofiel te configureren, gebruikt Intune de Azure Active Directory-eigenschappen in het e-mailprofiel van de gebruiker tijdens de inschrijving.

- Microsoft Outlook voor iOS/iPadOS- en Android-apparaten bieden geen ondersteuning voor e-mailprofielen. Implementeer in plaats daarvan een app-configuratiebeleid. Zie [Configuratie-instellingen voor Outlook](../apps/app-configuration-policies-outlook.md) voor meer informatie.

  Op Android Enterprise-apparaten implementeert u Gmail of Nine for Work met behulp van de beheerde Google Play Store. In [Beheerde Google Play-apps toevoegen](../apps/apps-add-android-for-work.md) worden de stappen weergegeven.

- E-mail is gebaseerd op identiteits- en gebruikersinstellingen. E-mailprofielen worden meestal toegewezen aan gebruikersgroepen, niet aan apparaatgroepen. Enkele aandachtspunten:

  - Als het e-mailprofiel gebruikerscertificaten bevat, moet u het e-mailprofiel aan gebruikersgroepen toewijzen. Het is mogelijk dat u meerdere profielen voor gebruikerscertificaten hebt die zijn toegewezen. Deze meerdere profielen zorgen voor een keten van profielimplementaties. Implementeer deze profielketen in gebruikersgroepen.

    Als één profiel in deze keten wordt geïmplementeerd in een apparaatgroep, worden gebruikers mogelijk voortdurend gevraagd om hun wachtwoord in te voeren.

  - Apparaatgroepen worden meestal gebruikt wanneer er geen primaire gebruiker is of als u niet weet wie de gebruiker wordt. E-mailprofielen die zijn gericht op apparaatgroepen (niet gebruikersgroepen), worden mogelijk niet bezorgd op het apparaat.

    Als uw e-mailprofiel bijvoorbeeld is gericht op een groep met allemaal iOS/iPadOS-apparaten, moet u ervoor zorgen dat al deze apparaten een gebruiker hebben. Als een apparaat geen gebruiker heeft, kan het e-mail profiel niet worden geïmplementeerd. Vervolgens beperkt u het profiel en kunnen bepaalde apparaten ontbreken. Wanneer het apparaat een primaire gebruiker heeft, zou de implementatie in apparaatgroepen moeten werken.

    Zie [Bekende problemen met e-mailprofielen](troubleshoot-email-profiles-in-microsoft-intune.md) voor meer informatie over mogelijke problemen met het gebruik van apparaatgroepen.

## <a name="remove-an-email-profile"></a>Een e-mailprofiel verwijderen

Er zijn verschillende manieren om een e-mailprofiel van een apparaat te verwijderen, zelfs als het apparaat maar één e-mailprofiel bevat:

- **Optie 1**: Open het e-mailprofiel (**Apparaten** > **Configuratieprofielen** > selecteer uw profiel) en kies **Toewijzingen**. Op het tabblad **Opnemen** worden de groepen weergegeven waaraan het profiel is toegewezen. Klik met de rechtermuisknop op de groep > **Verwijderen**. Klik vervolgens op **Opslaan** om uw wijzigingen op te slaan.

- **Optie 2**: [het apparaat wissen of buiten gebruik stellen](../remote-actions/devices-wipe.md). U kunt met deze handelingen een aantal of alle gegevens en instellingen verwijderen.

## <a name="secure-email-access"></a>Toegang tot e-mail beveiligen

U kunt e-mailprofielen beveiligen met behulp van de volgende opties:

- **Certificaten**: wanneer u het e-mailprofiel maakt, kiest u een certificaatprofiel dat u eerder hebt gemaakt in Intune. Dit certificaat wordt het identiteitscertificaat genoemd. Het wordt geverifieerd aan de hand van een vertrouwd-certificaatprofiel of een basiscertificaat om te bepalen of een apparaat van de gebruiker verbinding mag maken. Het vertrouwde certificaat wordt toegewezen aan de computer die de e-mailverbinding verifieert. Dit is meestal de systeemeigen e-mailserver.

  Als u gebruikmaakt van verificatie op basis van certificaten voor uw e-mailprofiel, implementeert u het e-mailprofiel, het certificaatprofiel en het vertrouwde basisprofiel in dezelfde groepen. Door deze implementatie kan elk apparaat de geldigheid van uw certificeringsinstantie herkennen.

  Zie [How to configure certificates with Intune](../protect/certificates-configure.md) (Certificaten configureren met Intune) voor meer informatie over het gebruiken en maken van certificaatprofielen in Intune.

- **Gebruikersnaam en wachtwoord**: de gebruiker wordt geverifieerd op de systeemeigen e-mailserver door de gebruikersnaam en het wachtwoord in te voeren. Het wachtwoord is niet aanwezig in het e-mailprofiel. De gebruiker voert dus het wachtwoord in wanneer verbinding wordt gemaakt met de e-mail.

## <a name="how-intune-handles-existing-email-accounts"></a>Hoe Intune omgaat met bestaande e-mailaccounts

Als de gebruiker al een e-mailaccount heeft geconfigureerd, is wordt het e-mailprofiel, afhankelijk van het platform, anders toegewezen.

- **iOS/iPadOS**: Een bestaand, dubbel e-mailprofiel wordt gedetecteerd op basis van de hostnaam en het e-mailadres. De toewijzing van een Intune-profiel wordt geblokkeerd op basis van het dubbele e-mailprofiel. In dit geval deelt de bedrijfsportal-app de gebruiker mee dat deze niet voldoet aan de eisen en wordt de eindgebruiker gevraagd het geconfigureerde profiel handmatig te verwijderen. Als u dit scenario wilt voorkomen, vertelt u uw eindgebruikers dat ze het apparaat eerst moeten inschrijven *voordat* ze een e-mailprofiel installeren, zodat Intune het profiel kan instellen.

- **Windows:** Een bestaand, dubbel e-mailprofiel wordt gedetecteerd op basis van de hostnaam en het e-mailadres. Intune overschrijft het bestaande e-mailprofiel dat is gemaakt door de eindgebruiker.

- **Android Samsung Knox - Standard**: Een bestaand, dubbel e-mailprofiel wordt gedetecteerd op basis van het e-mailadres. Het bestaande e-mailprofiel wordt overschreven door het Intune-profiel. Android gebruikt geen hostnaam om het profiel te identificeren. Maak niet meerdere e-mailprofielen met hetzelfde e-mailadres op verschillende hosts. De profielen overschrijven elkaar.

- **Android-werkprofielen**: Intune bevat twee Android-profielen voor zakelijke e-mail, een voor de app van Gmail en een voor de app van Nine Work. Deze apps zijn beschikbaar in de Google Play Store en worden geïnstalleerd in het werkprofiel van het apparaat. Door deze apps worden geen dubbele profielen gemaakt. Beide apps ondersteunen verbindingen met Exchange. Voor het gebruik van connectiviteit voor e-mail implementeert u een van deze e-mail-apps op uw gebruikersapparaten. Maak en implementeer vervolgens het e-mailprofiel. U kunt Gmail- en Nine-e-mailconfiguratieprofielen gebruiken die werken voor de inschrijvingstypen Werkprofiel en Volledig beheerd, toegewezen werkprofiel in bedrijfseigendom, waaronder het gebruik van certificaatprofielen voor beide e-mailconfiguratietypen. Gmail- of Nine-beleidsregels die u in Apparaatconfiguratie voor werkprofielen maakt, blijven van toepassing op het apparaat. Het is niet nodig om deze naar het app-configuratiebeleid te verplaatsen. E-mail-apps zoals Nine Work zijn mogelijk niet gratis. Raadpleeg de licentiegegevens van de app of neem contact op met het bedrijf dat de app heeft gemaakt voor meer informatie.

## <a name="changes-to-assigned-email-profiles"></a>Wijzigingen in toegewezen e-mailprofielen

Als u wijzigingen aanbrengt aan een e-mailprofiel dat u eerder had toegewezen, zien eindgebruikers mogelijk een bericht waarin ze wordt gevraagd de herconfiguratie van hun e-mailinstellingen goed te keuren.

## <a name="next-steps"></a>Volgende stappen

Als het profiel is gemaakt, doet het nog niets. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

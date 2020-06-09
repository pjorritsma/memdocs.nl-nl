---
title: macOS-systeem- en kernelextensies maken met Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Een macOS-apparaatprofiel toevoegen of maken dat systeemextensies of kernelextensies configureert om gebruikers toe te staan acties te overschrijven, een team-id toe te voegen en vervolgens een bundel- en team-id toe te voegen in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fce8218c9f8fb8757f0aef892f0854f1c386a8bd
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990297"
---
# <a name="add-macos-system-and-kernel-extensions-in-intune"></a>macOS-systeem- en kernelextensies toevoegen in Intune

> [!NOTE]
> macOS-kernel-extensies worden vervangen door systeemextensies. Voor meer informatie raadpleegt u [Ondersteuningstip: Systeemextensies in plaats van kernelextensies gebruiken voor macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Op macOS-apparaten kunt u kernelextensies en systeemextensies toevoegen. Met zowel kernelextensies als systeemextensies kunnen gebruikers app-extensies installeren waarmee de systeemeigen mogelijkheden van het besturingssysteem worden uitgebreid. Kernelextensies voeren hun code uit op kernelniveau. Systeemextensies worden uitgevoerd in een strikt beheerde gebruikersruimte.

Gebruik Microsoft Intune om extensies toe te voegen die altijd op uw apparaten mogen worden geladen. Intune maakt gebruik van configuratieprofielen om deze instellingen te maken voor en af te stemmen op de behoeften van uw organisatie. Nadat u deze functies aan een profiel hebt toegevoegd, kunt u het profiel pushen naar en implementeren op macOS-apparaten in uw organisatie.

In dit artikel worden systeemextensies en kernelextensies beschreven. Ook wordt getoond hoe u een apparaatconfiguratieprofiel maakt met behulp van extensies in Intune.

## <a name="system-extensions"></a>Systeemextensies

Systeemextensies worden uitgevoerd in de gebruikersruimte en hebben geen toegang tot de kernel. Het doel is de beveiliging te verhogen en de eindgebruiker meer controle te bieden, terwijl aanvallen op kernelniveau worden beperkt. Dit kunnen de volgende extensies zijn:

- Stuurprogramma-extensies, met inbegrip van stuurprogramma's op USB, netwerkinterfacekaarten (NIC), seriële controllers en Human Interface-apparaten (HID)
- Netwerkextensies, inclusief inhoudsfilters, DNS-proxy's en VPN-clients
- Eindpuntbeveiligingsextensies, inclusief eindpuntdetectie, eindpuntreactie en antivirus

Systeemextensies zijn opgenomen in de bundel van een app en worden geïnstalleerd vanuit de app.

Zie [systeemextensies](https://developer.apple.com/documentation/systemextensions) (hiermee opent u de website van Apple) voor meer informatie over systeemextensies.

## <a name="kernel-extensions"></a>Kernelextensies

Kernelextensies voegen functies toe op kernelniveau. Deze functies hebben toegang tot delen van het besturingssysteem waartoe reguliere programma's geen toegang hebben. Uw organisatie heeft mogelijk specifieke behoeften of vereisten die niet beschikbaar zijn in een app, een apparaatfunctie, enzovoort.

U hebt bijvoorbeeld een antivirusprogramma waarmee u uw apparaat kunt scannen op schadelijke inhoud. U kunt de kernelextensie van dit virusscanprogramma als een toegestane kernelextensie toevoegen in Intune. Vervolgens wijst u de extensie toe aan uw macOS-apparaten.

Met deze functie kunnen beheerders gebruikers toestemming geven om kernelextensies te overschrijven, team-id's toe te voegen en specifieke kernelextensies toe te voegen aan Intune.

Zie [kernelextensies](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (hiermee opent u de website van Apple) voor meer informatie over kernelextensies.

## <a name="prerequisites"></a>Vereisten

- Deze functie is van toepassing op:

  - macOS 10.13.2 en hoger (kernelextensies)
  - macOS 10.15 en hoger (systeemextensies)

  Vanaf macOS 10.15 tot 10.15.4 kunnen kernelextensies en systeemextensies naast elkaar worden uitgevoerd.

- Als u deze functie wilt gebruiken, moeten de apparaten aan de volgende voorwaarden voldoen:

  - Ingeschreven zijn bij Intune met behulp van het Device Enrollment Program (DEP) van Apple. Zie [macOS-apparaten automatisch inschrijven](../enrollment/device-enrollment-program-enroll-macos.md) voor meer informatie.

    OF

  - Ingeschreven zijn bij Intune met door de gebruiker goedgekeurde inschrijving (term van Apple). Zie [Voorbereiding op wijzigingen in kernelextensies in macOS High Sierra](https://support.apple.com/en-us/HT208019) (hiermee opent u de website van Apple) voor meer informatie.

## <a name="what-you-need-to-know"></a>Wat u dient te weten

- Niet-ondertekende verouderde kernelextensies en systeemextensies kunnen worden toegevoegd.
- Zorg ervoor dat u de juiste team-id en bundel-id van de extensie invoert. De waarden die u invoert, worden niet door Intune gevalideerd. Als u onjuiste gegevens invoert, werkt de extensie niet op het apparaat. Een team-id is precies tien alfanumerieke tekens lang.

> [!NOTE]
> Apple heeft informatie over ondertekening en notariële erkenning vrijgegeven voor alle software. Voor macOS 10.14.5 en hoger hoeven kernelextensies die via Intune zijn geïmplementeerd niet te voldoen aan het notariële erkenningsbeleid van Apple.
>
> Raadpleeg de volgende bronnen voor meer informatie over dit notariële erkenningsbeleid en eventuele updates of wijzigingen:
>
> - [Notariële erkenning voor uw app vóór distributie](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (hiermee opent u de website van Apple) 
> - [Voorbereiding op wijzigingen in kernelextensies in macOS High Sierra](https://support.apple.com/en-us/HT208019) (hiermee opent u de website van Apple)

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: **macOS** selecteren
    - **Profiel**: Selecteer **Extensies**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **macOS: Antivirusscans toevoegen aan kernelextensies op apparaten**.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Configureer in **Configuratie-instellingen** uw instellingen:

    - [macOS](kernel-extensions-settings-macos.md)

8. Selecteer **Volgende**.
9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruikers of groepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="next-steps"></a>Volgende stappen

Nadat het profiel is gemaakt, is het klaar om te worden toegewezen. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

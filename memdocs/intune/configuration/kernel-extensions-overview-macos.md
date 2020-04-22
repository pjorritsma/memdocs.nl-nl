---
title: macOS-apparaatprofielen met kernelextensies maken met Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Voeg een macOS-apparaatprofiel toe of maak een macOS-apparaatprofiel en configureer vervolgens kernelextensies om gebruikers toe te staan acties te overschrijven, een team-id toe te voegen en vervolgens een bundel- en team-id toe te voegen in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8f9212d275b17db6a40e3133b5363cd13c9d13d6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551424"
---
# <a name="add-macos-kernel-extensions-in-intune"></a>macOS-kernelextensies toevoegen in Intune

> [!NOTE]
> macOS-kernel-extensies worden vervangen door systeemextensies. Voor meer informatie raadpleegt u [Ondersteuningstip: Systeemextensies in plaats van kernelextensies gebruiken voor macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Op macOS-apparaten kunt u functies toevoegen op kernelniveau. Deze functies hebben toegang tot delen van het besturingssysteem waartoe reguliere programma's geen toegang hebben. Uw organisatie heeft mogelijk specifieke behoeften of vereisten die niet beschikbaar zijn in een app, een apparaatfunctie, enzovoort. 

Als u kernelextensies wilt toevoegen die altijd op uw apparaten mogen worden geladen, voegt u kernelextensies (KEXT) toe aan Microsoft Intune en implementeert u deze extensies vervolgens op uw apparaten.

U hebt bijvoorbeeld een antivirusprogramma waarmee u uw apparaat kunt scannen op schadelijke inhoud. U kunt de kernelextensie van dit virusscanprogramma als een toegestane kernelextensie toevoegen in Intune. Vervolgens wijst u de extensie toe aan uw macOS-apparaten.

Met deze functie kunnen beheerders gebruikers toestemming geven om kernelextensies te overschrijven, team-id's toe te voegen en specifieke kernelextensies toe te voegen aan Intune.

Deze functie is van toepassing op:

- macOS 10.13.2 en hoger

Als u deze functie wilt gebruiken, moeten de apparaten aan de volgende voorwaarden voldoen:

- Ingeschreven zijn bij Intune met behulp van het Device Enrollment Program (DEP) van Apple. Zie [macOS-apparaten automatisch inschrijven](../enrollment/device-enrollment-program-enroll-macos.md) voor meer informatie.

  OF

- Ingeschreven zijn bij Intune met door de gebruiker goedgekeurde inschrijving (term van Apple). Zie [Voorbereiding op wijzigingen in kernelextensies in macOS High Sierra](https://support.apple.com/en-us/HT208019) (hiermee opent u de website van Apple) voor meer informatie.

Intune maakt gebruik van configuratieprofielen om deze instellingen te maken voor en af te stemmen op de behoeften van uw organisatie. Nadat u deze functies aan een profiel hebt toegevoegd, kunt u het profiel pushen naar en implementeren op macOS-apparaten in uw organisatie.

In dit artikel wordt beschreven hoe u een apparaatconfiguratieprofiel maakt met behulp van kernelextensies in Intune.

> [!TIP]
> Zie [overzicht van kernelextensies](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (hiermee opent u de website van Apple) voor meer informatie over kernelextensies.

## <a name="what-you-need-to-know"></a>Wat u dient te weten

- Niet-ondertekende verouderde kernelextensies kunnen worden toegevoegd.
- Zorg ervoor dat u de juiste team-id en bundel-id van de kernelextensie invoert. De waarden die u invoert, worden niet door Intune gevalideerd. Als u onjuiste gegevens invoert, werkt de extensie niet op het apparaat. Een team-id is precies tien alfanumerieke tekens lang. 

> [!NOTE]
> Apple heeft informatie over ondertekening en notariële erkenning vrijgegeven voor alle software. Voor macOS 10.14.5 en hoger hoeven kernelextensies die via Intune zijn geïmplementeerd niet te voldoen aan het notariële erkenningsbeleid van Apple.
>
> Raadpleeg de volgende bronnen voor meer informatie over dit notariële erkenningsbeleid en eventuele updates of wijzigingen:
>
> - [Notariële erkenning voor uw app vóór distributie](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (hiermee opent u de website van Apple) 
> - [Voorbereiding op wijzigingen in kernelextensies in macOS High Sierra](https://support.apple.com/en-us/HT208019) (hiermee opent u de website van Apple)

> [!NOTE]
> De Intune-gebruikersinterface wordt bijgewerkt naar een versie voor volledig scherm. Dit kan enkele weken duren. Totdat de tenant deze update ontvangt, hebt u een enigszins afwijkende werkstroom wanneer u instellingen maakt of bewerkt zoals beschreven in dit artikel.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: **macOS** selecteren
    - **Profiel**: Selecteer **Extensies**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **macOS: kernelextensies toevoegen aan apparaten**.
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

---
title: Een groot aantal OEMConfig-profielen implementeren op Zebra-apparaten met behulp van Microsoft Intune - Azure | Microsoft Docs
description: Gebruik Microsoft Intune om meerdere OEMConfig-apparaten te maken en te implementeren op Zebra-apparaten met Android Enterprise. Gebruik Zebra-acties en stappen om uw profielen te ordenen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a38c445018200d9fe80db19142f123aba783b60
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311154"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Meerdere profielen van OEMConfig implementeren op apparaten van Zebra in Microsoft Intune

In Microsoft Intune kunt u OEMConfig gebruiken om OEM-specifieke instellingen voor Android Enterprise-apparaten aan te passen. Deze instellingen zijn specifiek voor de fabrikant van het apparaat en worden geïmplementeerd met behulp van configuratieprofielen in Intune.

Op Zebra-apparaten kunt u meerdere profielen implementeren of toewijzen aan hetzelfde apparaat. Bestaande OEMConfig-profielen kunnen deze functie de volgende keer dat de apparaten worden gesynchroniseerd met Intune gebruiken.

Deze functie is van toepassing op:

- Zebra-apparaten met Android Enterprise

Voor meer informatie over OEMConfig, met inbegrip van wat het doet en hoe u het kunt gebruiken, raadpleegt u [OEMConfig configuration profile](android-oem-configuration-overview.md) (OEMConfig-configuratieprofiel).

In dit artikel wordt beschreven hoe u meerdere OEMConfig-profielen implementeert op Zebra-apparaten, hoe u ze ordent en het gebruik van de rapportagefuncties in Microsoft Intune.

## <a name="prerequisites"></a>Vereisten

Een [OEMConfig-configuratieprofiel](android-oem-configuration-overview.md) maken.

## <a name="use-multiple-profiles"></a>Meerdere profielen gebruiken

Op Zebra-apparaten kunt u op elk apparaat meerdere profielen tegelijk hebben. Met deze functie kunt u uw Zebra OEMConfig-instellingen in kleinere profielen opsplitsen. U kunt bijvoorbeeld een basislijnprofiel maken dat van invloed is op alle apparaten. Maak vervolgens meer profielen voor het configureren van instellingen die specifiek zijn voor een apparaat.

Het OEMConfig-schema van Zebra gebruikt ook **acties**. Acties zijn bewerkingen die worden uitgevoerd op het apparaat. Ze configureren geen instellingen. Gebruik deze acties om het downloaden van bestanden te activeren, het klembord te wissen en nog veel meer. Zie de [documentatie van Zebra](https://techdocs.zebra.com/oemconfig/10-0/about/) (opent de website van Zebra) voor een volledige lijst met ondersteunde acties.

U kunt bijvoorbeeld een Zebra OEMConfig-profiel maken dat sommige instellingen op het apparaat toepast. Een ander Zebra OEMConfig-profiel bevat een actie waarmee het klembord wordt gewist. U wijst het eerste profiel toe aan een Zebra-apparatengroep. Later moet u het klembord op deze apparaten wissen. U wijst het tweede profiel toe aan dezelfde groep apparaten, zonder het eerste profiel te wijzigen. Het klembord van het apparaat wordt gewist zonder dat de configuratie-instellingen die in het eerste profiel zijn gemaakt, opnieuw worden verzenden of worden beïnvloed.

Nog een voorbeeld: u hebt een OEMConfig-profiel toegewezen dat enkele instellingen voor Zebra-apparaten heeft geconfigureerd. Onlangs hebben gebruikers problemen met een specifieke toepassing gemeld, en u wilt de cache van de app wissen. Maak een nieuw OEMConfig-profiel dat alleen de actie 'cache leegmaken' bevat. Wijs het profiel toe aan de apparaten die dit nodig hebben.

## <a name="ordering"></a>Ordenen

Met meerdere profielen op elk apparaat staat de volgorde waarin de profielen worden geïmplementeerd niet vast. Dit is een Google Play beperking. Als u bewerkingen op volgorde wilt uitvoeren, kunt u de [functie voor transactiestappen van Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/) (opent de website van Zebra) gebruiken. 

In het kort: als u een bepaalde volgorde wilt aanhouden, gebruikt u de [functie voor transactiestappen van Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/) (opent de website van Zebra). Als de volgorde niet van belang is, gebruikt u meerdere Intune-profielen. 

We kijken naar enkele voorbeelden:

- U wilt Bluetooth inschakelen voor alle nieuw ingeschreven Zebra-apparaten voordat u een andere instelling op deze apparaten configureert. Als u bewerkingen op volgorde wilt uitvoeren, gebruikt u de functie **Steps** in het schema van Zebra.

  Maak één Intune-profiel dat twee transactiestappen bevat. De eerste stap bevat Bluetooth-instellingen en de tweede stap configureert de andere instelling. Wanneer de OEMConfig-app van Zebra het profiel ontvangt, worden de stappen in de aangegeven volgorde uitgevoerd.

  Zie [Zebra's transaction steps](https://techdocs.zebra.com/oemconfig/10-0/mc/) (Transactiestappen in Zebra) (opent de website van Zebra) voor meer informatie.

- U wilt dat alle Zebra-apparaten de tijd in 24-uursnotatie weergeven. Voor sommige van deze apparaten wilt u de camera uitschakelen. De instellingen voor tijd en camera zijn niet afhankelijk van elkaar.

  Maak twee Intune-profielen:

  - **Profiel 1**: Hiermee wordt de tijd weergegeven in de 24-uursnotatie. Op maandag wordt dit profiel toegewezen aan de groep **Alle Zebra AE-apparaten**.
  - **Profiel 2**: Hiermee wordt de camera uitgeschakeld. Op dinsdag wordt dit profiel toegewezen aan de groep **Zebra AE-fabrieksapparaten**.

  Op woensdag schrijft u 10 nieuwe Zebra-apparaten in met Intune. Profiel 1 en profiel 2 worden toegewezen. Nadat de nieuwe apparaten zijn gesynchroniseerd met Intune, ontvangen ze de profielen. Op de apparaten kan profiel 2 eerder worden opgehaald dan profiel 1.

## <a name="enhanced-reporting"></a>Uitgebreide rapportage

U implementeert een profiel en het wordt uitgevoerd door de Zebra OEMConfig-app op het apparaat. De Zebra OEMConfig-app rapporteert de profielstatus naar Intune. In het beheercentrum van Endpoint Manager kunt u de status van geïmplementeerde OEMConfig-profielen en eventuele fouten of waarschuwingen bekijken.

1. Open het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer uw Zebra OEMConfig-profiel > **Controleren** > **Apparaatstatus**. Met deze optie worden de apparaten weergegeven waaraan uw OEMConfig-profiel is toegewezen.
3. Selecteer een apparaat > **Apparaatconfiguratie** > selecteer uw Zebra OEMConfig-profiel. Met deze optie worden de profielinstellingen weergegeven die zijn geslaagd of mislukt.

    Selecteer een rij. Er worden details weergegeven over waarom de fout is opgetreden.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [OEMConfig-configuratieprofielen](android-oem-configuration-overview.md).
- Configureer [Mobility Extensions (MX)](android-zebra-mx-overview.md) in Android-apparaatbeheer.
- [De profielstatus bewaken](device-profile-monitor.md).

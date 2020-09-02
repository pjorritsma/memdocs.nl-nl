---
title: Aangepaste instellingen toevoegen voor Windows 10-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Een aangepast profiel toevoegen of maken om de OMA-URI-instellingen te gebruiken voor apparaten met Windows 10 in Microsoft Intune. Een aangepast profiel gebruiken voor het toevoegen van aangepaste instellingen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28a867c735a05cfa4a4765534d200b806711f9b5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913015"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Aangepaste instellingen gebruiken voor Windows 10-apparaten in Intune

In dit artikel vindt u een overzicht en beschrijving van de verschillende aangepaste instellingen die u kunt beheren op apparaten met Windows 10 en hoger. Gebruik deze instellingen voor het configureren van instellingen die niet zijn ingebouwd in Intune, als onderdeel van uw MDM-oplossing (Mobile Device Management).

Zie [Een profiel maken met aangepaste instellingen](custom-settings-configure.md) voor meer informatie over aangepaste profielen.

Deze instellingen worden toegevoegd aan een apparaatconfiguratieprofiel in Intune en vervolgens toegewezen aan of geïmplementeerd op uw Windows 10-apparaten.

Deze functie is van toepassing op:

- Windows 10 en nieuwer

In aangepaste profielen voor Windows 10 worden OMA-URI-instellingen (Open Mobile Alliance Uniform Resource Identifier) gebruikt om verschillende functies te configureren. Deze instellingen worden doorgaans gebruikt door fabrikanten van mobiele apparaten om functies op het apparaat te beheren.

In Windows 10 zijn veel CSP-instellingen (Configuration Service Provider) beschikbaar, zoals de [beleids-CSP (Policy Configuration Service Provider)](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers).

Als u een specifieke instelling zoekt, moet u er rekening mee houden dat het [beperkingsprofiel voor Windows 10-apparaten](device-restrictions-windows-10.md) tal van ingebouwde instellingen bevat. U hoeft daarom mogelijk geen aangepaste waarden in te voeren.

## <a name="before-you-begin"></a>Voordat u begint

[Een aangepast Windows 10-profiel maken](custom-settings-configure.md#create-the-profile).

## <a name="oma-uri-settings"></a>OMA-URI-instellingen

**Toevoegen**: Voer de volgende instellingen in:

- **Naam**: Voer een unieke naam in voor de OMA-URI-instelling waaraan u deze kunt herkennen in de lijst met instellingen.
- **Beschrijving**: Voer een beschrijving in met een overzicht van de instelling en eventuele andere belangrijke details.
- **OMA-URI** (hoofdlettergevoelig): Voer de OMA-URI in die u als instelling wilt gebruiken.
- **Gegevenstype**: Selecteer het gegevenstype dat u voor deze OMA-URI-instelling gaat gebruiken. Uw opties zijn:

  - Base64 (bestand)
  - Boolean-waarde
  - Tekenreeks (XML-bestand)
  - Datum en tijd
  - Tekenreeks
  - Drijvende komma
  - Geheel getal

- **Waarde**: Voer de gegevenswaarde in die moet worden gekoppeld aan de OMA-URI die u hebt ingevoerd. De waarde is afhankelijk van het gegevenstype dat u hebt geselecteerd. Als u bijvoorbeeld **Datum en tijd** selecteert, selecteert u de waarde in een datumkiezer.

Nadat u een aantal instellingen hebt toegevoegd, kunt u **Exporteren** selecteren. Met **Exporteren** maakt u een lijst met alle waarden die u hebt toegevoegd in een bestand met door komma's gescheiden waarden (.csv).

## <a name="find-the-policies-you-can-configure"></a>De beleidsregels zoeken die u kunt configureren

Een complete lijst met alle CSP's (configuratieserviceproviders) die door Windows 10 worden ondersteund, vindt u in de [naslaginformatie voor configuratieserviceproviders](/windows/client-management/mdm/configuration-service-provider-reference).

Niet alle instellingen zijn compatibele met alle versies van Windows 10. In [Referentie voor Configuration Service Providers](/windows/client-management/mdm/configuration-service-provider-reference) leest u welke versies worden ondersteund voor elke CSP.

Bovendien biedt Intune geen ondersteuning voor alle instellingen die worden vermeld in de [naslaginformatie voor configuratieserviceproviders](/windows/client-management/mdm/configuration-service-provider-reference). Als u wilt weten of de gewenste instelling door Intune wordt ondersteund, opent u het artikel voor de betreffende instelling. U kunt op elke instellingenpagina zien welke bewerkingen worden ondersteund. Voor gebruik in combinatie met Intune moet de instelling de bewerking **Toevoegen**, **Vervangen** en **Ophalen** ondersteunen. Als de waarde die is geretourneerd door de bewerking **Ophalen** niet overeenkomt met de waarde die is opgegeven door de bewerkingen **Toevoegen** of **Vervangen**, meldt Intune vervolgens een compatibiliteitsfout.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

[Meer informatie over aangepaste profielen in Intune.](custom-settings-configure.md)
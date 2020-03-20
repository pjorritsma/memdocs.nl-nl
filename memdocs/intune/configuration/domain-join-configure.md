---
title: Profielinstellingen voor domeindeelname voor Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Maak een apparaatconfiguratieprofiel voor domeindeelname voor apparaten die zijn toegevoegd aan hybride Azure AD. Gebruik dit profiel om on-premises Active Directory-domeingegevens te implementeren op apparaten die zijn ingericht met Windows Autopilot en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 207b3983c214ad4e166ae58ea0ccd18ea23bf418
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364393"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Configuratie-instellingen voor domeindeelname voor apparaten die zijn toegevoegd aan hybride Azure AD in Microsoft Intune

In veel omgevingen wordt gebruikgemaakt van on-premises Active Directory (AD). Wanneer apparaten die zijn toegevoegd aan het AD-domein ook zijn toegevoegd aan Azure AD, worden het apparaten genoemd die zijn toegevoegd aan hybride Azure AD. Met Windows Autopilot kunt u [apparaten die zijn toegevoegd aan hybride AD inschrijven](../enrollment/windows-autopilot-hybrid.md) bij Intune. Voor inschrijving hebt u ook een configuratieprofiel voor **Domeindeelname** nodig.

Een configuratieprofiel voor **Domeindeelname** bevat on-premises Active Directory-domeingegevens. Wanneer apparaten worden ingericht (meestal offline), worden met dit profiel de AD-domeindetails geïmplementeerd, zodat bekend is aan welk on-premises domein de apparaten moeten worden toegevoegd. Als u geen domeindeelnameprofiel maakt, kan de implementatie voor deze apparaten mislukken.

Deze functie is van toepassing op:

- Windows 10 en nieuwer
- Apparaten die zijn toegevoegd aan hybride Azure AD
- Hybride implementatie met Autopilot en Intune

In dit artikel wordt aangegeven hoe u een domeindeelnameprofiel maakt voor een hybride Autopilot-implementatie. U kunt ook de beschikbare instellingen weergeven.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **Windows 10: domeindeelnameprofiel dat on-premises domeingegevens bevat voor inschrijving van hybride AD-apparaten met Windows Autopilot**.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.
    - **Platform**: Kies **Windows 10 en hoger**.
    - **Profieltype**: Selecteer **Domeindeelname (preview)** .

4. Selecteer **Instellingen**. Voer de volgende eigenschappen in:

    - **Computernaamvoorvoegsel**: Voer een voorvoegsel voor de apparaatnaam in. Computernamen bestaan uit 15 tekens. Na het voorvoegsel worden de resterende 15 tekens willekeurig gegenereerd.
    - **Domeinnaam**: Voer de FQDN (Fully Qualified Domain Name) in waaraan de apparaten moeten worden toegevoegd. Voer bijvoorbeeld in: `americas.corp.contoso.com.`
    - **Organisatie-eenheid** (optioneel): Voer het volledige pad ([DN-naam](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) in naar de organisatie-eenheid (OE) waarin de computeraccounts moeten worden gemaakt. Voer bijvoorbeeld `"CN=Users,DC=Contoso,DC=com"` in. Als u geen waarde opgeeft, wordt er een bekende computerobjectcontainer gebruikt.

      Zie [Apparaten die zijn toegevoegd aan hybride Azure AD implementeren](../enrollment/windows-autopilot-hybrid.md) voor meer informatie en advies over deze instelling.

5. Wanneer u klaar bent, selecteert u **OK** > **Maken** om uw wijzigingen op te slaan.

Het profiel wordt gemaakt en weergegeven in de lijst met profielen. U kunt het nu gebruiken om [apparaten die zijn toegevoegd aan hybride Azure AD te implementeren met behulp van Intune en Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Volgende stappen

Nadat het profiel is gemaakt, is het klaar om te worden toegewezen. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

[Apparaten die zijn toegevoegd aan hybride Azure AD implementeren met behulp van Intune en Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

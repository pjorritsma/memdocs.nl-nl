---
title: Profielinstellingen voor domeindeelname voor Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Maak een apparaatconfiguratieprofiel voor domeindeelname voor apparaten die zijn toegevoegd aan hybride Azure AD. Gebruik dit profiel om on-premises Active Directory-domeingegevens te implementeren op apparaten die zijn ingericht met Windows Autopilot en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/31/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8285b15a3fd7d473641ce9480fe1e6522b54e814
ms.sourcegitcommit: ded11a8b999450f4939dcfc3d1c1adbc35c42168
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/01/2020
ms.locfileid: "89281095"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Configuratie-instellingen voor domeindeelname voor apparaten die zijn toegevoegd aan hybride Azure AD in Microsoft Intune

In veel omgevingen wordt gebruikgemaakt van on-premises Active Directory (AD). Wanneer apparaten die zijn toegevoegd aan het AD-domein ook zijn toegevoegd aan Azure AD, worden het apparaten genoemd die zijn toegevoegd aan hybride Azure AD. Met Windows Autopilot kunt u [apparaten die zijn toegevoegd aan hybride AD inschrijven](../../autopilot/windows-autopilot-hybrid.md) bij Intune. Voor inschrijving hebt u ook een configuratieprofiel voor **Domeindeelname** nodig.

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

    - **Platform**: Kies **Windows 10 en hoger**.
    - **Profiel**: Selecteer **Domeindeelname (preview)** .

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **Windows 10: domeindeelnameprofiel dat on-premises domeingegevens bevat voor inschrijving van hybride AD-apparaten met Windows Autopilot**.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.
7. Voer de volgende eigenschappen in bij **Configuratie-instellingen**:

    - **Computernaamvoorvoegsel**: Voer een voorvoegsel voor de apparaatnaam in. Computernamen bestaan uit 15 tekens. Na het voorvoegsel worden de resterende 15 tekens willekeurig gegenereerd.
    - **Domeinnaam**: Voer de FQDN (Fully Qualified Domain Name) in waaraan de apparaten moeten worden toegevoegd. Voer bijvoorbeeld in: `americas.corp.contoso.com.`
    - **Organisatie-eenheid** (optioneel): Voer het volledige pad ([DN-naam](/windows/win32/ad/object-names-and-identities#distinguished-name)) in naar de organisatie-eenheid (OE) waarin de computeraccounts moeten worden gemaakt. Voer bijvoorbeeld `"CN=Users,DC=Contoso,DC=com"` in. Als u geen waarde opgeeft, wordt er een bekende computerobjectcontainer gebruikt.

      Zie [Apparaten die zijn toegevoegd aan hybride Azure AD implementeren](../../autopilot/windows-autopilot-hybrid.md) voor meer informatie en advies over deze instelling.

8. Selecteer **Volgende**.

9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de apparaatgroepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Als u apparaten wilt toevoegen aan verschillende domeinen of organisatie-eenheden, moet u verschillende apparaatgroepen maken.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

U kunt het nu gebruiken om [apparaten die zijn toegevoegd aan hybride Azure AD te implementeren met behulp van Intune en Windows Autopilot](../../autopilot/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Volgende stappen

Wanneer het profiel is [toegewezen, ](device-profile-assign.md)moet u de [status ervan controleren](device-profile-monitor.md).

[Apparaten die zijn toegevoegd aan hybride Azure AD implementeren met behulp van Intune en Windows Autopilot](../../autopilot/windows-autopilot-hybrid.md).

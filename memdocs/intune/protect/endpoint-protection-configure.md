---
title: Instellingen voor Endpoint Protection configureren in Microsoft Intune - Azure | Microsoft Docs
description: Instellingen voor Endpoint Protection in Microsoft Intune maken wanneer u een profiel voor een macOS- of Windows 10-apparaat maakt.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 4071614c7cb93194eef00f49aa2e1759ba1028f6
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359261"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>Instellingen voor Endpoint Protection toevoegen in Intune

Met Intune kunt u configuratieprofielen voor apparaten gebruiken voor het beheren van algemene beveiligingsfuncties voor eindpunten op apparaten, waaronder:

- Firewall
- BitLocker
- Apps toestaan en blokkeren
- Microsoft Defender en versleuteling

U kunt bijvoorbeeld een Endpoint Protection-profiel maken waarmee macOS-gebruikers alleen apps uit de Mac App Store kunnen installeren. Of u kunt Windows SmartScreen inschakelen bij het uitvoeren van apps op Windows 10-apparaten.

Lees voordat u een profiel maakt de volgende artikelen door, zodat u precies weet welke instellingen voor de bescherming van eindpunten Intune kan beheren voor elk ondersteund platform:

- [macOS-instellingen](endpoint-protection-macos.md)
- [Windows 10-instellingen](endpoint-protection-windows-10.md)

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>Een apparaatprofiel met instellingen voor Endpoint Protection maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Voer de volgende eigenschappen in:

    - **Platform**: Kies het platform van uw apparaten. Uw opties zijn:

        - **macOS**
        - **Windows 10 en hoger**

    - **Profiel**: Selecteer **Endpoint Protection**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **macOS: Endpoint Protection-profiel waarmee de firewall wordt geconfigureerd voor alle macOS-apparaten**.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Welke instellingen u kunt configureren in **Configuratie-instellingen**, is afhankelijk van het platform dat u hebt gekozen. Kies uw platform voor gedetailleerde instellingen:

   - [macOS-instellingen](endpoint-protection-macos.md)
   - [Windows 10-instellingen](endpoint-protection-windows-10.md)

8. Selecteer **Volgende**.
9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruikers of groepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Aangepaste firewallregels toevoegen voor Windows 10-apparaten

Als u de Microsoft Defender Firewall configureert als onderdeel van een profiel met Endpoint Protection-regels voor Windows 10, kunt u aangepaste regels configureren voor firewalls. Met aangepaste regels kunt u de vooraf gedefinieerde set firewallregels die worden ondersteund voor Windows 10 uitbreiden.

Als u van plan bent profielen met aangepaste firewallregels te gebruiken, moet u rekening houden met de volgende informatie; deze kan van invloed kan zijn op de manier waarop u firewallregels in uw profielen groepeert:

- Elk profiel ondersteunt maximaal 150 firewallregels. Als u meer dan 150 regels gebruikt, maakt u extra profielen met elk een maximum van 150 regels.

- Als één regel niet kan worden toegepast in een profiel, mislukt het uitvoeren van álle regels. Er wordt dan dus geen enkele regel toegepast op het apparaat.

- Als een regel niet kan worden toegepast, wordt van alle regels in het profiel gerapporteerd dat ze zijn mislukt. Intune kan niet identificeren welke specifieke regel dan is mislukt.  

De firewallregels die door Intune kunnen worden beheerd, worden beschreven in de Windows [Firewall](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp)-configuratieprovider (CSP). Zie [Aangepaste firewallregels](endpoint-protection-windows-10.md#firewall-rules) voor een overzicht van de aangepaste-firewallinstellingen voor Windows 10-apparaten die door Intune worden ondersteund.

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Aangepaste firewallregels toevoegen aan een Endpoint Protection-profiel

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Selecteer bij *Platform* **Windows 10 en hoger** en vervolgens bij *Profiel* **Endpoint Protection**.

    Selecteer **Maken**.

4. Voer een **naam** voor uw profiel in > **Volgende**.
5. Selecteer **Microsoft Defender Firewall** bij de **configuratie-instellingen**. Selecteer bij *Firewallregels* **Toevoegen** om de pagina **Regel maken** te openen.

6. Geef instellingen voor de firewallregel op en selecteer **OK** om deze op te slaan. Zie [Aangepaste firewallregels](endpoint-protection-windows-10.md#firewall-rules)om de beschikbare opties voor aangepaste firewallregels te bekijken in de documentatie.

    1. De regel wordt weergegeven op de pagina *Microsoft Defender Firewall*, in de lijst met regels.
    2. Als u een regel wilt wijzigen, selecteert u de regel in de lijst. De pagina **Regel bewerken** wordt dan geopend.
    3. Als u een regel uit een profiel wilt verwijderen, selecteert u het beletselteken **(...)** bij de regel. Selecteer vervolgens **Verwijderen**.
    4. Als u de volgorde wilt wijzigen waarin de regels worden weergegeven, selecteert u het pictogram *pijl-omhoog en pijl-omlaag* bovenaan de lijst met regels.

7. Selecteer **Volgende** totdat u bij **Beoordelen en maken** aankomt. Wanneer u **Maken** selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt mogelijk nog niets. Vervolgens kunt u [het profiel toewijzen](../configuration/device-profile-assign.md) en [de status ervan controleren](../configuration/device-profile-monitor.md).

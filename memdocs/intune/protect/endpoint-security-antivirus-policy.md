---
title: Instellingen voor antivirus tegen aanvallen beheren met eindpuntbeveiligingsbeleid in Microsoft Intune | Microsoft Docs
description: Configureer en implementeer beleidsregels en gebruik rapporten voor apparaten die u beheert met eindpuntbeveiligingsinstellingen voor antivirusbeleid in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: b0d0bbeb174d8f90d47ea6242ce6bd4be2dcfac6
ms.sourcegitcommit: cb9b452f8e566fe026717b59c142b65f426e5033
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/20/2020
ms.locfileid: "86491164"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Antivirusbeleid voor eindpuntbeveiliging in Intune

Het antivirusbeleid van de Intune-eindpuntbeveiliging kan beveiligingsbeheerders helpen om zich te richten op het beheren van de afzonderlijke groep antivirusinstellingen voor beheerde apparaten. U kunt Intune integreren met Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) als Mobile Threat Defense-oplossing om een antivirusbeleid te gebruiken.

Antivirusbeleid bevat verschillende profielen. Elk profiel bevat alleen de instellingen die relevant zijn voor Microsoft Defender ATP-antivirus voor macOS, Windows 10 of voor de gebruikerservaring in de Windows-beveiligingstoepassing op Windows 10-apparaten.

U vindt dit antivirusbeleid vinden onder **Beheren** in het knooppunt Eindpuntbeveiliging van het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

Het antivirusbeleid bevat dezelfde instellingen die zijn gevonden in *Endpoint Protection* of *apparaatbeperkings*profielen voor [apparaatconfirgutatie](../configuration/device-profile-create.md)beleid en zijn vergelijkbaar met instellingen van [apparaatcompliance](../protect/device-compliance-get-started.md)beleid. Deze beleidstypen bevatten echter aanvullende categorieën instellingen die geen betrekking hebben op antivirus. De extra instellingen kunnen de taak voor het configureren van antivirus bemoeilijken. Daarnaast zijn de instellingen die worden gevonden in het antivirusbeleid voor macOS niet beschikbaar via de andere beleidstypen. Het antivirusprofiel van macOS vervangt de noodzaak om de instellingen te configureren met behulp van `.plist` bestanden.

## <a name="prerequisites-for-antivirus-policy"></a>Vereisten voor antivirusbeleid

- **macOS**
  - Een ondersteunde versie van macOS
  - Microsoft Defender ATP moet op een apparaat zijn geïnstalleerd om de antivirus-instellingen op dat apparaat te beheren met Intune. Zie. [Microsoft Defender ATP voor macOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (in de documentatie van Microsoft Defender ATP)

- **Windows 10 en hoger**
  - Er zijn geen aanvullende voorwaarden vereist. 

## <a name="antivirus-profiles"></a>Antivirus-profielen

**macOS-profielen**:

- **Antivirus**: [Instellingen voor antivirusbeleid beheren](../protect/antivirus-microsoft-defender-settings-macos.md) voor macOS.

  Wanneer u [Microsoft Defender ATP voor Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) gebruikt, kunt u antivirus-instellingen configureren en implementeren op uw beheerde macOS-apparaten via Intune in plaats van deze instellingen te configureren met behulp van `.plist` bestanden.

**Windows 10-profielen**:

- **Microsoft Defender Antivirus**: beheer de instellingen van het [Antivirus-beleid](../protect/antivirus-microsoft-defender-settings-windows.md) voor Windows 10.

  Defender Antivirus is de volgende generatie van beveiligingsonderdelen van Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). De volgende generatie beveiliging combineert machine learning, analyse van big data, diepgaande bescherming tegen bedreigingen en cloudinfrastructuur om apparaten in uw bedrijfsorganisatie te beschermen.

  Het *Microsoft Defender Antivirus*-profiel is een afzonderlijk exemplaar van de antivirusinstellingen die worden gevonden in het *Beperkingsprofiel voor apparaten* voor het configuratiebeleid voor apparaten.
  
  In tegenstelling tot de antivirus-instellingen in een *Restrictieprofiel voor apparaten*, kunt u deze instellingen gebruiken voor apparaten die gezamenlijk worden beheerd. Als u deze instellingen wilt gebruiken, moet u de [schuifregelaar voor cobeheerworkload](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) voor Endpoint Protection instellen op Intune.

- **Windows Security-ervaring**: beheer welke [app-instellingen van Windows Security](../protect/antivirus-security-experience-windows-settings.md) eindgebruikers kunnen bekijken in het Microsoft Defender-beveiligingscentrum en welke meldingen ze ontvangen. De Windows-beveiligingsapp wordt gebruikt door een aantal Windows-beveiligingsfuncties om meldingen over de status en beveiliging van de machine te geven. Meldingen over beveiligingsapps zijn onder andere firewalls, antivirusproducten, Windows Defender SmartScreen en anderen.

## <a name="antivirus-policy-reports"></a>Beleidsrapporten voor antivirus

In rapporten van het antivirusbeleid worden statusgegevens weergegeven over het antivirusbeleid van eindpuntbeveiliging en de apparaatstatus. Deze rapporten zijn te vinden in het knooppunt eindpuntbeveiliging van het Beheercentrum voor Microsoft Endpoint Manager.

Als u de rapporten wilt weergeven, gaat u in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) naar eindpuntbeveiliging en selecteert u **Antivirus**. Als u antivirus selecteert, wordt de Overzichtspagina geopend. Aanvullende rapporten en statusweergaven zijn beschikbaar als extra pagina's.

### <a name="summary"></a>Samenvatting

Op de **Overzichtspagina** kunt u [nieuwe beleidsregels maken](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) en een lijst met de eerder gemaakte beleidsregels weergeven. De lijst bevat details op hoog niveau over het profiel dat door dat beleid wordt opgenomen (beleidstype), en als het beleid is toegewezen.

![Overzichtspagina van antivirusbeleid](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Wanneer u een beleid selecteert in de lijst, wordt de *Overzichtspagina* voor dat beleidsexemplaar geopend en wordt er meer informatie weergegeven. Wanneer u een tegel in deze weergave selecteert, geeft Intune extra informatie weer voor dat profiel als dit beschikbaar is.

![Overzichtspagina van antivirusbeleid](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Beschadigde eindpunten voor Windows 10

U kunt op de pagina **Beschadigde eindpunten voor Windows 10** de informatie bekijken over de antivirusstatus van uw door MDM beheerde Windows 10-apparaten. Deze informatie wordt geretourneerd door Windows Defender Antivirus dat op het apparaat wordt uitgevoerd, zoals *status van de bedreigingsagent*.

In deze weergave worden alleen apparaten met gedetecteerde problemen weergegeven. In deze weergave worden geen details weergegeven voor apparaten die als veilig worden geïdentificeerd.

![Overzichtspagina van antivirusbeleid](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Volgende stappen

[Eindpuntbeveiligingsbeleid configureren](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)

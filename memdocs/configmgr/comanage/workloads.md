---
title: Werk belastingen voor co-beheer
titleSuffix: Configuration Manager
description: Meer informatie over de werk belastingen die u kunt omschakelen van Configuration Manager naar Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: 8c91ba1c2b4b5ef7072c030eddd9b97dd69933e5
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075707"
---
# <a name="co-management-workloads"></a>Werk belastingen voor co-beheer

U hoeft de werk belastingen niet te scha kelen of u kunt ze individueel doen wanneer u klaar bent. Configuration Manager blijft alle andere workloads beheren, met inbegrip van de werk belastingen die u niet overschakelt naar intune en alle andere functies van Configuration Manager die niet door co-beheer worden ondersteund.

Als u een werk belasting overschakelt naar intune, maar later van gedachten verandert, kunt u overschakelen naar Configuration Manager.

Co-beheer ondersteunt de volgende werk belastingen:

- [Nalevings beleid](#compliance-policies)  

- [Windows Update beleid](#windows-update-policies)  

- [Toegangs beleid voor bronnen](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Apparaatconfiguratie](#device-configuration)  

- [Office klik-en-klaar-apps](#office-click-to-run-apps)  

- [Client-apps](#client-apps)  

## <a name="compliance-policies"></a>Compliance beleidsregels

Nalevings beleid definieert de regels en instellingen waaraan een apparaat moet voldoen om te worden beschouwd als compatibel met het beleid voor voorwaardelijke toegang. U kunt ook nalevings beleid gebruiken om nalevings problemen met apparaten onafhankelijk van voorwaardelijke toegang te controleren en te herstellen. Vanaf Configuration Manager versie 1910 kunt u evaluatie van aangepaste configuratie basislijnen toevoegen als beoordelings regel voor nalevings beleid. Zie [aangepaste configuratie basislijnen opnemen als onderdeel van de evaluatie van het nalevings beleid](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines)voor meer informatie.

Zie [nalevings beleid voor apparaten](https://docs.microsoft.com/intune/device-compliance-get-started)voor meer informatie over de intune-functie.  

## <a name="windows-update-policies"></a>Windows Update beleid

Met Windows Update for business-beleid kunt u uitstel beleid configureren voor Windows 10-onderdelen updates of kwaliteits updates voor Windows 10-apparaten die rechtstreeks worden beheerd door Windows Update voor bedrijven.

Zie voor meer informatie over de intune-functie [Windows update configureren voor bedrijfs beleid voor uitstel](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

## <a name="resource-access-policies"></a>Toegangs beleid voor bronnen

Bron toegangs beleid configureren VPN-, Wi-Fi-, e-mail-en certificaat instellingen op apparaten.

Zie [toegangs profielen voor resources implementeren](https://docs.microsoft.com/intune/device-profiles)voor meer informatie over de intune-functie.

> [!Note]  
> De werk belasting voor resource toegang maakt ook deel uit van de apparaatconfiguratie. Deze beleids regels worden beheerd door intune wanneer u de werk belasting van de [apparaatconfiguratie](#device-configuration) overschakelt.

## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

De Endpoint Protection werk belasting bevat de Windows Defender-suite van antimalware Protection-functies:

- Windows Defender antimalware
- Windows Defender Application Guard  
- Windows Defender Firewall  
- Windows Defender SmartScreen  
- Windows-versleuteling
- Windows Defender Exploit Guard  
- Windows Defender Application Control  
- Windows Defender Security Center  
- Windows Defender Advanced Threat Protection (nu bekend als micro soft Defender Threat Protection)
- Windows Information Protection  

Zie voor meer informatie over de intune-functie [Endpoint Protection voor Microsoft intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

> [!Note]  
> Wanneer u deze werk belasting overschakelt, blijft het Configuration Manager-beleid op het apparaat totdat het intune-beleid deze overschrijft. Dit gedrag zorgt ervoor dat het apparaat nog steeds beveiligings beleid heeft tijdens de overgang.
>
> De Endpoint Protection werk belasting maakt ook deel uit van de apparaatconfiguratie. Hetzelfde gedrag geldt wanneer u de workload van de [apparaatconfiguratie](#device-configuration) overschakelt.<!-- SCCMDocs.nl-nl issue #4 -->
>
> De micro soft Defender anti virus-instellingen die deel uitmaken van het profiel type voor beperkingen van het apparaat voor de configuratie van het intune-apparaat, zijn niet opgenomen in het bereik van de Endpoint Protection-schuif regelaar. Als u micro soft Defender anti virus wilt beheren voor door co beheerde apparaten waarvoor de Endpoint Protection-schuif regelaar is ingeschakeld, gebruikt u het nieuwe antivirus beleid in **micro soft Endpoint Manager-beheer centrum** > **Endpoint Security** > **anti virus**. Het nieuwe beleids type heeft nieuwe en verbeterde beschik bare opties en biedt ondersteuning voor alle instellingen die beschikbaar zijn in het profiel voor beperkingen van apparaten. <!--6609171-->
>
> Het Windows-versleutelings onderdeel bevat BitLocker-beheer. Zie [Deploying BitLocker Management](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune)(Engelstalig) voor meer informatie over het gedrag van deze functie met co-beheer.<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>Apparaatconfiguratie

<!--1357903-->

De werk belasting voor apparaatconfiguratie bevat instellingen die u beheert voor apparaten in uw organisatie. Als u deze werk belasting wijzigt, worden de **resource toegang** en **Endpoint Protection** -workloads ook verplaatst.

U kunt nog steeds instellingen van Configuration Manager implementeren op door co beheerde apparaten, zelfs als intune de configuratie-instantie van de apparaat is. Deze uitzonde ring kan worden gebruikt om instellingen te configureren die uw organisatie vereist, maar die nog niet beschikbaar zijn in intune. Geef deze uitzonde ring op een [Configuration Manager configuratie basislijn](../compliance/deploy-use/create-configuration-baselines.md)op. Schakel de optie om **deze basis lijn altijd toe te passen, zelfs voor clients die gezamenlijk worden beheerd** bij het maken van de basis lijn. U kunt dit later wijzigen op het tabblad **Algemeen** van de eigenschappen van een bestaande basis lijn.  

Zie [een apparaatprofiel maken in Microsoft intune](https://docs.microsoft.com/intune/device-profile-create)voor meer informatie over de intune-functie.  

## <a name="office-click-to-run-apps"></a>Office klik-en-klaar-apps

<!--1357841-->

Deze workload beheert Office 365-apps op gezamenlijk beheerde apparaten.

- Nadat de werk belasting is verplaatst, wordt de app weer gegeven in de **bedrijfsportal** op het apparaat  

- Het kan ongeveer 24 uur duren voordat Office-updates worden weer gegeven op de client, tenzij de apparaten opnieuw zijn opgestart  

- Er is een nieuwe globale voor waarde, **zijn Office 365-toepassingen die worden beheerd door intune op het apparaat**. Deze voor waarde wordt standaard toegevoegd als vereiste voor nieuwe Office 365-toepassingen. Wanneer u deze werk belasting overstapt, voldoen gezamenlijk beheerde clients niet aan de vereiste voor de toepassing. Vervolgens installeren ze geen Office 365 dat is geïmplementeerd via Configuration Manager.  

Zie [Office 365-apps toewijzen aan Windows 10-apparaten met Microsoft intune](https://docs.microsoft.com/intune/apps-add-office365)voor meer informatie over de intune-functie.

## <a name="client-apps"></a>Client-apps

<!--1357892-->

Gebruik intune voor het beheren van client-apps en Power shell-scripts op met co beheerde Windows 10-apparaten. Nadat u deze werk belasting hebt overgezet, zijn alle beschik bare apps die zijn geïmplementeerd vanuit intune, beschikbaar in de Bedrijfsportal. Apps die u vanaf Configuration Manager implementeert, zijn beschikbaar in Software Center.

Zie [Wat is Microsoft intune app Management?](https://docs.microsoft.com/intune/app-management)voor meer informatie over de intune-functie.

> [!Tip]  
> Deze functie werd voor het eerst in versie 1806 geïntroduceerd als een [voorlopige functie](../core/servers/manage/pre-release-features.md). Vanaf versie 2002 is het niet langer een functie van de voorlopige versie.  
>
> Deze functie kan worden weer gegeven in de lijst met functies als **mobiele apps voor door co beheerde apparaten**.<!-- 5849669 -->

Met ingang van versie 1910, wanneer u micro soft Connected cache op uw Configuration Manager-distributie punten inschakelt, kunnen ze nu Microsoft Intune Win32-apps voor gezamenlijk beheerde clients gebruiken. Zie voor meer informatie [micro soft Connected cache in Configuration Manager](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune).

## <a name="diagram-for-app-workloads"></a>Diagram voor app-workloads

![Diagram van werk belastingen van de app voor co-beheer](media/co-management-apps.svg)

[Het diagram op volledige grootte weer geven](media/co-management-apps.svg)

## <a name="known-issues"></a>Bekende problemen

Wanneer de Endpoint Protection werk belasting wordt verplaatst naar intune, kan de client nog steeds beleid naleven dat door Configuration Manager en micro soft Defender is ingesteld. <!--5024559-->

U kunt dit probleem omzeilen door de CleanUpPolicy. XML toe te passen met behulp van ConfigSecurityPolicy. exe nadat de intune-beleids regels zijn ontvangen door de client met behulp van de onderstaande stappen:

1. Kopieer de onderstaande tekst en sla deze `CleanUpPolicy.xml`op als.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```
1. Open een opdracht prompt met verhoogde bevoegdheden `ConfigSecurityPolicy.exe`naar. Dit uitvoer bare bestand bevindt zich doorgaans in een van de volgende directory's:
   - C:\Program Files\Windows Defender
   - C:\Program Files\Microsoft Security-client
1. Geef vanuit de opdracht prompt het XML-bestand door om het beleid op te schonen. Bijvoorbeeld `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`.  

## <a name="next-steps"></a>Volgende stappen

[Werk belastingen overschakelen](how-to-switch-workloads.md)  

---
title: Uitsluitingen van virussen
titleSuffix: Configuration Manager
description: Meer informatie over aanbevolen antivirus uitsluitingen voor gebruik bij het oplossen van mogelijke problemen.
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: f3f38de1d7440ffd0293bde359deeb6be3bbeffb
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906195"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Aanbevolen uitsluitingen van virussen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat aanbevelingen die een beheerder kunnen helpen bij het bepalen van de oorzaak van mogelijke instabiliteit op een computer met een ondersteunde versie van Configuration Manager site servers, site systemen en clients wanneer deze wordt gebruikt in combi natie met antivirus software.

> [!IMPORTANT]
>
> - U wordt aangeraden deze procedures tijdelijk toe te passen om een systeem te evalueren. Als uw systeem prestaties of stabiliteit wordt verbeterd door de aanbevelingen die in dit artikel worden beschreven, neemt u contact op met de leverancier van uw antivirus software voor instructies of voor een bijgewerkte versie van de antivirus software.
> - Dit artikel bevat informatie over hoe u de beveiligings instellingen kunt verlagen of hoe u de beveiligings functies van een computer tijdelijk uitschakelt. U kunt deze wijzigingen aanbrengen om inzicht te krijgen in de aard van een specifiek probleem. Voordat u deze wijzigingen aanbrengt, wordt u aangeraden de Risico's te evalueren die zijn gekoppeld aan het implementeren van deze tijdelijke oplossing in uw specifieke omgeving.

## <a name="possible-symptoms"></a>Mogelijke symptomen 

Antivirus real-time beveiliging kan veel problemen veroorzaken op Configuration Manager site servers, site systemen en clients.

Hier volgt een niet-uitgebreide lijst met mogelijke symptomen:

- Externe site systeem onderdelen zijn niet geïnstalleerd. SiteComp. log, Distmgr. log, hman. log of andere Configuration Manager logboek bestanden bevatten mogelijk fouten zoals fout 80070005.
- De Configuration Manager-client kan niet worden geïnstalleerd met behulp van client push.
- De inventarisatie gegevens van de client zijn onjuist, ontbreken of zijn verouderd.
- Achterstand vindt plaats in de *Install_Directory*map \Program Files\Microsoft Configuration Manager\Inboxes.
- Software Center wordt niet gevuld door geïmplementeerde software op client systemen of start niet. Het bestand CCMRepair. log bevat mogelijk fouten die lijken op het volgende voor beeld:

  > De database verificatie is mislukt met het volgende resultaat: 0x80004005, maar DB: C:\Windows\CCM\filename.sdf kan worden geopend, DB-reparatie wordt overgeslagen.

- Software die is geïmplementeerd op clients kan niet worden geïnstalleerd.
- Compatibiliteits gegevens voor software-implementaties zijn onjuist.

## <a name="exclusions"></a>Uitsluitingen

Om dergelijke problemen te voor komen, raden we u aan de volgende uitsluitingen voor real-time beveiliging toe te voegen:

### <a name="default-installation-folders"></a>Standaard installatie mappen

|  |  |
| - | - |
|*Installatiemap van ConfigMgr*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*MP-installatiemap*  |% Program Files% \ SMS_CCM  |  
|*Installatiemap van client*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>Uitsluitingen van mappen voor site servers

- \Inboxes *ConfigMgr-installatiemap*
- \Logs *ConfigMgr-installatiemap*
- \EasySetupPayload *ConfigMgr-installatiemap*

### <a name="folder-exclusions-for-site-systems"></a>Uitsluitingen van mappen voor site systemen

- Beheer punten
  - *MP-installatiemap*\ServiceData
  - Een van de volgende:
    - \MP\OUTBOXES *ConfigMgr-installatiemap*
    - \SMS\MP\OUTBOXES *installatie station*
- Distributiepunten
  - *Client installatie map*\ServiceData
  - *ContentLib_Drive*\ SMS_DP $
  - *ContentLib_Drive*\SMSPKG*Drive_Letter*$
  - *ContentLib_Drive*\SMSPKG
  - *ContentLib_Drive*\SMSPKGSIG
  - *ContentLib_Drive*\SMSSIG $
- Site database servers
  - [Antivirus software kiezen voor uitvoering op computers met SQL Server](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>Uitsluitingen van mappen voor clients

- Installatiemap van de *client* \\ \* . sdf
- *Client installatie map*\ServiceData
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *Client installatie map*\Logs

### <a name="file-exclusions-for-mps"></a>Uitsluitingen van bestanden voor MPs

- POL00000. Pol in
  - *MP-installatiemap*\PolReqStaging

### <a name="process-exclusions"></a>Procesuitsluitingen

Proces uitsluitingen zijn alleen nodig als agressieve antivirus Programma's Configuration Manager programma bestanden (exe-bestanden) worden beschouwd als processen met een hoog risico.

- \Bin\64\Smsexec.exe *ConfigMgr-installatiemap*
- Een van de volgende processen:
  - *Client installatie map*\Ccmexec.exe
  - *MP-installatiemap*\Ccmexec.exe
- *Client installatie map*\CmRcService.exe (aan client zijde)
- \Bin\64\Sitecomp.exe *ConfigMgr-installatiemap*
- \Bin\64\Smswriter.exe *ConfigMgr-installatiemap*
- *ConfigMgr-installatiemap*\bin\64\Smssqlbkup.exe of SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- \Bin\64\Cmupdate.exe *ConfigMgr-installatiemap*
- *Client installatie map*\Ccmrepair.exe (aan client zijde)
- %*windir*% \ CCMSetup\Ccmsetup.exe (aan client zijde)

## <a name="next-steps"></a>Volgende stappen

Raadpleeg de volgende artikelen voor meer informatie over uitsluitingen van virussen:

[Configuration Manager Current Branch antivirus uitsluitingen-System Center premier field engineer-blog](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-current-branch-antivirus-exclusions/ba-p/884831)

[De uitsluitingen van System Center 2012 Configuration Manager anti virus zijn bijgewerkt met meer informatie over OSD-en opstart installatie kopieën](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/updated-system-center-2012-configuration-manager-antivirus/ba-p/884371)

[Antivirus software kiezen voor uitvoering op computers met SQL Server](https://support.microsoft.com/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[Aanbevelingen voor virus scans voor Enter prise-computers waarop momenteel ondersteunde versies van Windows worden uitgevoerd](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)

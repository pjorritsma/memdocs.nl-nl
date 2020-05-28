---
title: BitLocker-beheer plannen
titleSuffix: Configuration Manager
description: Plannen voor het beheer van BitLocker-stationsversleuteling met Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2523d06034f4a7effe769235cb5a4ede4df7e167
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764115"
---
# <a name="plan-for-bitlocker-management"></a>BitLocker-beheer plannen

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!-- 3601034 -->

Vanaf versie 1910 gebruikt u Configuration Manager om BitLocker-stationsversleuteling (BDE) te beheren voor on-premises Windows-clients. Het biedt een volledig beheer van de BitLocker-levenscyclus waarmee het gebruik van micro soft BitLocker Administration and monitoring (MBAM) kan worden vervangen.

> [!Note]  
> Configuration Manager schakelt deze optionele functie standaard niet in. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Zie [overzicht van BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview)voor meer informatie.

> [!TIP]
> Als u versleuteling wilt beheren op met co beheerde Windows 10-apparaten met behulp van de micro soft Endpoint Manager-Cloud service, schakelt u de [ **Endpoint Protection** workload](../../comanage/workloads.md#endpoint-protection) over naar intune. Zie [Windows-versleuteling](/intune/protect/endpoint-protection-windows-10#windows-encryption)voor meer informatie over het gebruik van intune.

## <a name="features"></a>Functies

Configuration Manager biedt de volgende beheer mogelijkheden voor BitLocker-stationsversleuteling:

### <a name="client-deployment"></a>Clientimplementatie

De BitLocker-client implementeren op beheerde Windows-apparaten met Windows 10 of Windows 8,1

### <a name="manage-encryption-policies"></a>Versleutelings beleid beheren

- Bijvoorbeeld: Kies stationsversleuteling en coderings sterkte, Configureer het gebruikers vrijstellings beleid, de versleutelings instellingen voor het vaste gegevens station.

- Bepaal de algoritmen waarmee het apparaat moet worden versleuteld en de schijven die u wilt versleutelen.

- Dwing gebruikers af om aan de slag te gaan met het nieuwe beveiligings beleid voordat het apparaat wordt gebruikt.

- Pas het beveiligings Profiel van uw organisatie aan per apparaat.

- Wanneer een gebruiker het station van het besturings systeem ontgrendelt, geeft u op of alleen een OS-station of alle bijgevoegde stations moeten worden vergrendeld.

### <a name="compliance-reports"></a>Nalevings rapporten

Ingebouwde rapporten voor:

- Versleutelings status per volume of per apparaat
- De primaire gebruiker van het apparaat
- Nalevings status
- Redenen voor niet-naleving

### <a name="administration-and-monitoring-website"></a>Website voor beheer en controle

Sta andere personen in uw organisatie buiten de Configuration Manager-console toe om te helpen bij sleutel herstel, zoals het draaien van sleutels en andere ondersteuning voor BitLocker. Helpdesk beheerders kunnen bijvoorbeeld gebruikers helpen met sleutel herstel.

### <a name="user-self-service-portal"></a>Self-Service Portal voor gebruikers

Laat gebruikers zichzelf helpen met een sleutel voor eenmalig gebruik voor het ontgrendelen van een apparaat dat is versleuteld met BitLocker. Zodra deze sleutel wordt gebruikt, wordt er een nieuwe sleutel voor het apparaat gegenereerd.

## <a name="prerequisites"></a>Vereisten

- Als u een beheer beleid voor BitLocker wilt maken, moet u de rol **volledige beheerder** hebben in Configuration Manager.

- De BitLocker-herstel service vereist HTTPS voor het versleutelen van de herstel sleutels in het netwerk van de Configuration Manager-client naar het beheer punt. Er zijn twee opties:

  - HTTPS: Schakel de IIS-website in op het beheer punt dat als host fungeert voor de herstel service. Deze optie is alleen van toepassing op Configuration Manager versie 2002.<!-- 5925660 -->

  - Configureer het beheer punt voor HTTPS. Deze optie is van toepassing op Configuration Manager versie 1910 of 2002.

  Zie [herstel gegevens versleutelen](../deploy-use/bitlocker/encrypt-recovery-data.md)voor meer informatie.

- Als u de BitLocker-beheer rapporten wilt gebruiken, installeert u de site systeemrol van het Reporting Services-punt. Zie [Configure Reporting](../../core/servers/manage/configuring-reporting.md)(Engelstalig) voor meer informatie.

    > [!NOTE]
    > Voor het uitvoeren van het **rapport herstel controle** op de website beheer en controle gebruikt u alleen een Reporting Services-punt op de primaire site.

- Als u de Self-Service Portal of de beheer-en controle website wilt gebruiken, hebt u een Windows Server met IIS nodig. U kunt een Configuration Manager-site systeem opnieuw gebruiken of een zelfstandige webserver gebruiken die verbinding heeft met de site database server. Gebruik een [ondersteunde versie van het besturings systeem voor site systeem servers](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).

    > [!NOTE]
    > Installeer alleen de Self-Service Portal en de beheer-en bewakings website met een primaire site database. Installeer deze websites voor elke primaire site in een hiërarchie.

- Op de webserver waarop de Self-Service Portal wordt gehost, installeert u [micro soft ASP.NET MVC 4,0](https://docs.microsoft.com/aspnet/mvc/mvc4).

- Het gebruikers account dat het installatie script voor de portal uitvoert, heeft SQL **sysadmin** -rechten nodig op de site database server. Tijdens het installatie proces stelt het script aanmeldings-, gebruikers-en SQL-rollen rechten in voor het computer account van de webserver. U kunt dit gebruikers account verwijderen uit de sysadmin-rol nadat u de installatie van de Self-Service Portal en de beheer-en controle website hebt voltooid.

- BitLocker-beheer wordt niet ondersteund op virtuele machines (Vm's) of op server-besturings systemen. Daarom werken sommige functies mogelijk niet zoals verwacht op virtuele machines of op server-besturings systemen. Bijvoorbeeld op virtuele machines BitLocker-beheer start de versleuteling niet op vaste schijven van virtuele machines. Daarnaast kunnen harde schijven in virtuele machines worden weer gegeven als compatibel, zelfs als ze niet zijn versleuteld.

> [!TIP]
> Met de taken reeks stap **BitLocker inschakelen** wordt standaard alleen de *gebruikte ruimte* op het station versleuteld. BitLocker-beheer maakt gebruik van een *volledige schijf* versleuteling. Deze taken reeks stap configureren om de optie voor het **gebruik van volledige schijf versleuteling**in te scha kelen. Zie [taken reeks stappen-BitLocker inschakelen](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Herstel gegevens versleutelen](../deploy-use/bitlocker/encrypt-recovery-data.md) (een optionele vereiste voordat u het beleid voor de eerste keer implementeert)

[BitLocker-beheer-client implementeren](../deploy-use/bitlocker/deploy-management-agent.md)

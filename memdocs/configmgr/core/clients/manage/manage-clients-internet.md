---
title: Clients op internet beheren
titleSuffix: Configuration Manager
description: Meer informatie over het beheren van clients met Cloud beheer gateway en client beheer op internet in Configuration Manager.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2840b30bee20d2fa73531b07c095e028979f6274
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715591"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Clients op Internet beheren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Doorgaans in Configuration Manager zijn de meeste beheerde computers en servers fysiek op hetzelfde interne netwerk als de site systeem servers die beheer functies uitvoeren. U kunt echter clients buiten uw interne netwerk beheren wanneer ze zijn verbonden met internet. Met deze mogelijkheid hoeven clients geen verbinding te maken via VPN om de site systeem servers te bereiken.

Configuration Manager biedt twee manieren om clients met Internet verbinding te beheren:

- Cloudbeheergateway

- Clientbeheer via internet

> [!NOTE]
> U kunt een combi natie van beide services voor één site hebben. Als een apparaat beleid van de site voor zowel IBCM als CMG, dan is het wille keurig voor communicatie. Het enige mechanisme dat beschikbaar is om communicatie te beheren, is client verificatie. Als een Azure AD-client bijvoorbeeld het Server verificatie certificaat van het beheer punt op internet niet vertrouwt, kan het alleen de CMG gebruiken. Als een client die lid is van een domein, niet het Server verificatie certificaat van de CMG vertrouwt, kan deze alleen het beheer punt op Internet gebruiken.<!-- SCCMDocs#1541 -->

## <a name="cloud-management-gateway"></a>Cloudbeheergateway

De Cloud beheer gateway biedt beheer van clients op internet. Er wordt gebruikgemaakt van een combi natie van een Microsoft Azure-Cloud service en een on-premises site systeemrol die met die service communiceert. Clients op Internet gebruiken de Cloud service om te communiceren met de on-premises Configuration Manager.

### <a name="cmg-advantages"></a>Voor delen van CMG

- Geen extra on-premises infra structuur-investering vereist.  

- Maakt geen on-premises infra structuur beschikbaar op internet.  

- Virtuele machines in de cloud die de service uitvoeren, worden volledig beheerd door Azure en vereisen geen onderhoud.  

- Eenvoudig in te stellen en te configureren in de Configuration Manager-console.  

### <a name="cmg-disadvantages"></a>Nadelen CMG  

- Kosten voor Cloud abonnementen.  

- Beheer gegevens die via de Cloud service worden verzonden.  

Zie voor meer informatie [plannen voor Cloud beheer gateway](cmg/plan-cloud-management-gateway.md).  

## <a name="internet-based-client-management"></a>Clientbeheer via internet

Deze methode is afhankelijk van Internet gerichte site systeem servers waarmee clients rechtstreeks communiceren voor beheer doeleinden. Hiervoor moeten clients en site systeem servers worden geconfigureerd voor client beheer op internet (IBCM).

### <a name="ibcm-advantages"></a>Voor delen van IBCM

- Geen Cloud service afhankelijkheid.  

- Er zijn geen extra kosten verbonden aan een Cloud abonnement.  

- Volledig beheer van servers en rollen die de service bieden.  

### <a name="ibcm-disadvantages"></a>Nadelen IBCM

- Extra investering in infra structuur vereisen.  

- Overhead en operationele kosten van een extra infra structuur.  

- Infra structuur moet worden blootgesteld aan Internet.  

Zie voor meer informatie [plannen voor client beheer op Internet](plan-internet-based-client-management.md).  

---
title: Licenties en branches
titleSuffix: Configuration Manager
description: Meer informatie over de licentie vereisten voor de beschik bare installatie opties voor Configuration Manager
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed335c65369840085fe44ba2f1b81d7806a0e3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906055"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Licenties en vertakkingen voor Configuration Manager

*Van toepassing op: Configuration Manager (current branch), & System Center Configuration Manager (vertakking voor langlopende Servicing)*

In dit artikel vindt u meer informatie over de licentie vereisten voor de beschik bare installatie opties van Configuration Manager. Deze installatie opties zijn onder andere de volgende vertakkingen:

- Huidige vertakking
- Long-term Servicing Branch (LTSB)
- Evaluatie-installatie van de huidige vertakking
- Branch voor Technical Preview

## <a name="licensing-overview"></a>Licentieoverzicht

Klanten met een actieve Software Assurance (SA) op Configuration Manager licenties of met gelijkwaardige abonnements rechten vanaf 1 oktober 2016 hebben recht op het gebruik van de versie 1606-release van Configuration Manager van oktober 2016. Klanten met rechten voor het Configuration Manager op of na 1 oktober 2016 vinden twee gelicentieerde opties bij de installatie: current branch en Long-term Servicing Branch (LTSB).

Zie [licentie voorwaarden en documentatie](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)voor de volledige voor waarden voor de producten die u aanschaft via micro soft Volume Licensing Program ma's.


## <a name="licensed-branches"></a>Gelicentieerde branches

In dit artikel wordt verwezen naar de Software Assurance-overeenkomst of gelijkwaardige abonnements rechten. In deze micro soft Licensing Agreement worden rechten verleend om Configuration Manager te installeren en te gebruiken.

### <a name="current-branch"></a>Huidige vertakking

Voor de huidige vertakking is een actieve Software Assurance-overeenkomst of gelijkwaardige rechten vereist om Configuration Manager. Zie [Software Assurance en de current branch](#software-assurance-and-the-current-branch)voor meer informatie.

Deze vertakking wordt ondersteund voor gebruik in productie omgevingen die normale kwaliteit en functie-updates van micro soft willen ontvangen. Het biedt toegang tot het gebruik van alle functies en verbeteringen.

Vanaf de 1710-release blijft de update versie 18 maanden geldig vanaf de release datum van de algemene Beschik baarheid. Zie [ondersteuning voor Configuration Manager huidige branch-versies](../servers/manage/current-branch-versions-supported.md)voor meer informatie.

### <a name="long-term-servicing-branch-ltsb"></a>Long-term Servicing Branch (LTSB)

De LTSB vereist een actuele Software Assurance-overeenkomst met micro soft vanaf 1 oktober 2016. Zie [Software Assurance en de LTSB](#software-assurance-and-the-ltsb)voor meer informatie.

Deze vertakking wordt ondersteund voor gebruik in productie omgevingen. Het is bedoeld voor gebruik door klanten die de rechten van Software Assurance (SA) of gelijkwaardige abonnementen Configuration Manager laten verlopen na 1 oktober 2016. Deze vertakking is beperkt in vergelijking met de Current Branch.

Essentiële beveiligings updates voor Configuration Manager worden beschikbaar gesteld aan deze Branch, maar er worden geen nieuwe functies beschikbaar gesteld.

### <a name="evaluation-installation-of-the-current-branch"></a>Evaluatie-installatie van de huidige vertakking

Voor de evaluatie versie is geen Software Assurance-overeenkomst met micro soft vereist. [Evaluatie-installaties](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) zijn altijd de huidige vertakking en u kunt ze 180 dagen gebruiken.

U kunt de evaluatie-installatie bijwerken naar een volledige installatie van de huidige vertakking. U kunt een evaluatie-installatie niet upgraden naar de Long-term Servicing Branch.

### <a name="technical-preview-branch"></a>Branch voor Technical Preview

De [vertakking Technical Preview](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) is ook beschikbaar. Deze vertakking is een beperkte build van Configuration Manager waarmee u nieuwe functies kunt uitproberen. U installeert de technische preview met behulp van verschillende media dan de gelicentieerde versies. Zie [Technical Preview](../get-started/technical-preview.md)voor meer informatie.


## <a name="software-assurance-agreements"></a>Software Assurance-overeenkomsten

De status van Software Assurance op uw Configuration Manager licenties of vergelijk bare abonnements rechten op of na 1 oktober 2016 bepaalt de vertakking die u kunt installeren en gebruiken.

### <a name="software-assurance-and-the-current-branch"></a>Software Assurance en de huidige branch

De rechten voor het gebruik van Configuration Manager current branch kunnen worden gegeven door:

- **System Center:** Klanten met actieve SA op System Center Standard-of Data Center-licenties kunnen de huidige vertakkings optie van Configuration Manager installeren en gebruiken.

- **System Center Configuration Manager:** Klanten met actieve SA op Configuration Manager licenties of met gelijkwaardige abonnements rechten, kunnen de huidige vertakkings optie van Configuration Manager installeren en gebruiken.

Als u een actieve SA hebt op Configuration Manager licenties of vergelijk bare abonnements rechten op of na 1 oktober 2016:

- U kunt de huidige vertakking installeren en gebruiken.
- Als u toestaat dat de SA of het abonnement vervalt, moet u de huidige vertakking verwijderen.

### <a name="software-assurance-and-the-ltsb"></a>Software Assurance en de LTSB

Als u een actieve SA hebt op Configuration Manager licenties of vergelijk bare abonnements rechten op of na 1 oktober 2016:

- U kunt de LTSB installeren en gebruiken. Klanten die over permanente rechten beschikken voor Configuration Manager of die hun SA of een verstrijken toestaan, kunnen de versie van Configuration Manager LTSB installeren die op het moment van vertraging is bijgewerkt.

LTSB is gebaseerd op huidige branch versie 1606 en heeft de volgende beperkingen:

- Er is geen ondersteuning voor het converteren van een huidige vertakking naar het LTSB. Als u momenteel een huidige branch-site hebt, moet u de LTSB installeren als een nieuwe site.  

- LTSB biedt geen ondersteuning voor alle mogelijkheden van de huidige vertakking. Zie [Introduction to the Long-term Servicing Branch](introduction-to-the-ltsb.md)(Engelstalig) voor meer informatie. Deze beperkingen omvatten een beperkt aantal functies, beperkte upgrade opties en een afzonderlijke levens cyclus voor product ondersteuning.  

### <a name="software-assurance-expiration-date"></a>Verval datum Software Assurance

Vanaf de release van oktober 2016 van de basis media van versie 1606 voor Configuration Manager, kunt u de verval datum van uw Software Assurance-overeenkomst opgeven. De **verval datum van de Software Assurance** is een optionele waarde als een handige herinnering. Voeg het toe wanneer u Configuration Manager Setup of later vanuit de Configuration Manager-console uitvoert.

> [!NOTE]
> Micro soft valideert niet de verval datum die u opgeeft en gebruikt deze datum niet voor validatie van licenties. Gebruik dit als een herinnering voor uw verval datum. Deze waarde is handig wanneer Configuration Manager periodiek controleert of nieuwe software-updates online worden aangeboden. De licentie status van uw Software Assurance moet actueel zijn om deze aanvullende updates te kunnen gebruiken.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>De verval datum van de Software Assurance opgeven

- Wanneer u het installatie programma uitvoert vanaf het Configuration Manager medium, geeft u de waarde op de pagina **product code** van de installatie wizard.

- In de Configuration Manager-console, in **hiërarchie-instellingen**, geeft u de waarde op het tabblad **licenties** .


## <a name="licensing-resources"></a>Licentie bronnen

Gebruik de volgende bronnen voor meer informatie over de licentie gegevens van een product.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Microsoft Volume Licensing Service Center (VLSC)

- [Overzicht van VLSC](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Micro soft Volume Licensing-product termen](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)

- Klanten met een volume licentie kunnen een samen vatting krijgen van hun licenties via het [Volume License-Service Centrum](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Ga naar het menu **licenties** en selecteer **licentie samenvatting**.

### <a name="vlsc-videos"></a>VLSC-Video's

- Voor trainings Video's over hoe VLSC werkt, gaat u naar [Microsoft Volume Licensing service center training en resources](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) en selecteert u **hoe Video's**.

- [Waar kunt u uw actieve Software Assurance-overeenkomst opzoeken](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (vanaf 43 seconden)  

- [Machtigingen voor VLSC ophalen](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). U kunt VLSC Lees-en schrijf machtigingen voor andere personen in uw organisatie delegeren.

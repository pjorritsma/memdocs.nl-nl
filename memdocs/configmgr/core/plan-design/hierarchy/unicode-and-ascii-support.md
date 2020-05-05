---
title: Unicode- en ASCII-ondersteuning
titleSuffix: Configuration Manager
description: Meer informatie over ondersteuning voor Unicode-en ASCII-tekens in Configuration Manager-objecten.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bd3dad5f0ef24074ac8c8e6d2edf01d5641b541
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717550"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Unicode-en ASCII-ondersteuning in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager maakt de meeste objecten met behulp van Unicode-tekens. Meerdere objecten ondersteunen echter alleen ASCII-tekens of ze hebben andere beperkingen.  

## <a name="objects-that-use-ascii-characters"></a><a name="BKMK_ASCIIchar"></a>Objecten die gebruikmaken van ASCII-tekens

Wanneer u de volgende objecten maakt, ondersteunt Configuration Manager alleen de ASCII-tekenset:  

- Site code  

- Alle computer namen van site systeem server  

- De volgende Configuration Manager accounts:  

    > [!NOTE]  
    > Deze accounts ondersteunen ASCII-tekens en RUS-tekens op een site die wordt uitgevoerd in Russisch.  

    - Account voor push-client installatie  

    - Account voor verbinding met beheer punt database  

    - Netwerktoegangsaccount  

    - Pakket toegangs account  

    - Standaard account voor afzender  

    - Installatie account site systeem  

    - Verbindings account software-update punt  

    - Proxyserver account software-update punt  

    > [!NOTE]  
    > De accounts die u opgeeft voor op rollen gebaseerd beheer ondersteunen Unicode.  
    >
    > Het Reporting Services-punt account ondersteunt Unicode, met uitzonde ring van RUS-tekens.  

- FQDN-naam (Fully Qualified Domain Name) voor site servers en site systemen  

- Installatiepad voor Configuration Manager  

- SQL Server exemplaar namen  

- Het pad voor de volgende site systeem rollen:  

    - Inschrijvingspunt  

    - Proxypunt voor inschrijving  

    - Reporting Services-punt  

    - Statusmigratiepunt  

- Het pad voor de volgende mappen:  

    - De map waarin de migratie gegevens van de client status worden opgeslagen  

    - De map die de Configuration Manager rapporten bevat  

    - De map waarin de back-up van de Configuration Manager wordt opgeslagen  

    - De map waarin de bron bestanden van de installatie voor de site-installatie worden opgeslagen  

    - De map waarin de vereiste down loads voor gebruik door Setup worden opgeslagen  

- Het pad voor de volgende objecten:  

    - IIS-website  

    - Installatiepad van virtuele toepassing  

    - Naam van virtuele toepassing  

- ISO-bestands namen voor opstarten van medium  


## <a name="additional-limitations"></a><a name="BKMK_OtherCharLimitations"></a>Aanvullende beperkingen

Hieronder vindt u meer beperkingen voor ondersteunde teken sets en taal versies:  

- Configuration Manager biedt geen ondersteuning voor het wijzigen van de land instellingen van de site Server computer.  

- Een Enter prise-certificerings instantie (CA) biedt geen ondersteuning voor client computer namen die DBCS (double-byte character sets) gebruiken. De namen van de client computers die u kunt gebruiken, worden beperkt door de PKI-beperking van de IA5-tekenset. Configuration Manager biedt geen ondersteuning voor CA-namen of waarden met een onderwerpnaam die DBCS gebruiken.  


## <a name="objects-that-arent-localized"></a><a name="BKMK_LangNonLocalize"></a>Objecten die niet zijn gelokaliseerd

De Configuration Manager-Data Base ondersteunt Unicode voor de meeste objecten die worden opgeslagen. Als dat mogelijk is, wordt deze informatie weer gegeven in de taal van het besturings systeem die overeenkomt met de land instellingen van een computer. De land instelling van de computer moet overeenkomen met een client-of server taal die u op een site installeert voor de client interface of Configuration Manager-console om informatie weer te geven in de taal van het besturings systeem van de computer.  

Meerdere Configuration Manager-objecten bieden geen ondersteuning voor Unicode. Ze worden opgeslagen in de-data base door gebruik te maken van ASCII, of ze hebben extra taal beperkingen. Deze informatie wordt altijd weer gegeven met de ASCII-tekenset, of in de taal die in gebruik was toen u het object maakte.  

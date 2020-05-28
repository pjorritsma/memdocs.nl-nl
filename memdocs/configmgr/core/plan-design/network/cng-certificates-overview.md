---
title: Overzicht van de CNG-certificaten
titleSuffix: Configuration Manager
description: Meer informatie over ondersteuning voor CNG-certificaten (Cryptography Next Generation) voor Configuration Manager-clients en-servers.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: deb3108d492a955eb0ec6b1635e306dcb85e0062
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904220"
---
# <a name="cng-certificates-overview"></a>Overzicht van de CNG-certificaten
<!-- 1356191 --> 

Configuration Manager heeft beperkte ondersteuning voor crypto grafie: Next Generation (CNG)-certificaten. Configuration Manager-clients kunnen een PKI-certificaat voor client verificatie gebruiken met een persoonlijke sleutel in de SLEUTELARCHIEFPROVIDER. Met de SLEUTELARCHIEFPROVIDER-ondersteuning ondersteunen Configuration Manager-clients op hardware gebaseerde persoonlijke sleutel, zoals TPM-SLEUTELARCHIEFPROVIDER voor PKI-client verificatie certificaten.

## <a name="supported-scenarios"></a>Ondersteunde scenario's
U kunt [crypto GRAFIE API: Next Generation (CNG)-](https://docs.microsoft.com/windows/win32/seccng/cng-features) certificaat sjablonen gebruiken voor de volgende scenario's:

- Client registratie en communicatie met een HTTPS-beheer punt   
- Software distributie en toepassings implementatie met een HTTPS-distributie punt   
- Implementatie van besturingssystemen  
- SDK voor client berichten (met de nieuwste update) en ISV-proxy   
- cloudbeheergateway configuratie  

Vanaf versie 1802 gebruiken CNG-certificaten voor de volgende server functies met HTTPS-functionaliteit: <!-- 1357314 -->   
- Beheerpunt
- Distributiepunt
- Software-updatepunt
- Statusmigratiepunt     

Vanaf versie 1806 gebruiken CNG-certificaten voor de volgende server functies met HTTPS-functionaliteit:

- Certificaat registratiepunt, met inbegrip van de NDES-server met de Configuration Manager-beleids module <!--1357314-->

> [!NOTE]
> CNG is achterwaarts compatibel met de cryptografische API (CAPI). CAPI-certificaten worden nog steeds ondersteund, zelfs wanneer CNG-ondersteuning is ingeschakeld op de client.

## <a name="unsupported-scenarios"></a>Niet-ondersteunde scenario's

De volgende scenario's worden momenteel niet ondersteund:

- De volgende server functies zijn niet operationeel wanneer deze zijn geïnstalleerd in de HTTPS-modus met een CNG-certificaat dat is gekoppeld aan de website in Internet Information Services (IIS): 
    - Application Catalog-webservice
    - Application catalog-website
    - Inschrijvingspunt  
    - Proxypunt voor inschrijving  

- Software Center geeft geen toepassingen en pakketten weer als beschikbaar die zijn geïmplementeerd voor verzamelingen van gebruikers of gebruikers groepen.

- Gebruik CNG-certificaten om een Cloud distributiepunt te maken.

- Als de NDES-beleids module een CNG-certificaat gebruikt voor client verificatie, mislukt de communicatie met het certificaat registratiepunt. 
    - Dit wordt ondersteund vanaf Configuration Manager versie 1806.

- Als u een CNG-certificaat opgeeft bij het maken van taken reeks media, kan de wizard geen opstart bare media maken.
    - Dit wordt ondersteund vanaf Configuration Manager versie 1806.

## <a name="to-use-cng-certificates"></a>CNG-certificaten gebruiken

Als u CNG-certificaten wilt gebruiken, moet uw certificerings instantie (CA) CNG-certificaat sjablonen opgeven voor doel computers. De sjabloon details variëren afhankelijk van het scenario. de volgende eigenschappen zijn echter vereist:

- **Compatibiliteit met eerdere versies** tabblad

    - De **certificerings instantie** moet Windows Server 2008 of hoger zijn. (Windows Server 2012 wordt aanbevolen.)

    - De ontvanger van het **certificaat** moet Windows Vista/Server 2008 of hoger zijn. (Windows 8/Windows Server 2012 wordt aanbevolen.)

- **Cryptografie** tabblad

    - **Provider categorie** moet een **sleutelarchiefprovider zijn.** lang
    - **Voor de aanvraag moet een van de volgende providers worden gebruikt:** moet **micro soft software Key Storage Provider**zijn. 

> [!NOTE]
> De vereisten voor uw omgeving of organisatie kunnen afwijken. Neem contact op met uw PKI-expert. Het belang rijk punt om rekening mee te houden, is dat een certificaat sjabloon een Sleutelarchiefprovider moet gebruiken om gebruik te maken van CNG.

Voor de beste resultaten raden we u aan om de onderwerpnaam te bouwen op basis van Active Directory informatie. Gebruik de DNS-naam voor de indeling van de **onderwerpnaam** en voeg de DNS-naam toe aan de naam van het alternatieve onderwerp. Anders moet u deze informatie opgeven wanneer het apparaat wordt Inge schreven in het certificaat profiel.

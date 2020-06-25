---
title: Instellingen voor bekabeld netwerk configureren voor macOS-apparaten in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Lees hoe u een configuratieprofiel voor een bekabeld netwerkapparaat kunt toevoegen of maken voor macOS-apparaten. Zie de verschillende instellingen, voeg certificaten toe, kies een EAP-type en het selecteer een verificatiemethode in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41b11a29cdfd61382e68130479a1ab465bf354c6
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107414"
---
# <a name="add-wired-network-settings-for-macos-devices-in-microsoft-intune"></a>Bekabeld netwerkinstellingen voor macOS-apparaten in Microsoft Intune toevoegen

U kunt een profiel maken met specifieke instellingen voor een bekabeld netwerk en dit profiel vervolgens implementeren op uw macOS-apparaten. Microsoft Intune biedt veel functies, waaronder het verifiëren bij het netwerk, het toevoegen van een PKCS- of SCEP-certificaat en meer.

In dit artikel worden de instellingen beschreven die u kunt configureren.

## <a name="before-you-begin"></a>Voordat u begint

[Een configuratieprofiel voor een bekabeld netwerkapparaat maken](wired-networks-configure.md).

> [!NOTE]
> Deze instellingen zijn beschikbaar voor alle inschrijvingstypen. Zie [macOS-inschrijving](../enrollment/macos-enroll.md) voor meer informatie over de inschrijvingstypen.

## <a name="wired-network"></a>Bekabeld netwerk

- **Netwerkinterface**: Selecteer de netwerkinterfaces op het apparaat waarop het profiel van toepassing is, op basis van de prioriteit van de servicevolgorde. Uw opties zijn:
  
  - **Eerste actieve Ethernet** (standaard)
  - **Tweede actieve Ethernet**
  - **Derde actieve Ethernet**
  - **Eerste Ethernet**
  - **Tweede Ethernet**
  - **Derde Ethernet**
  - **Elk Ethernet**

  Opties waar "actief" titel staat, maken gebruik van interfaces die actief op het apparaat werken. Als er geen actieve interfaces zijn, wordt de volgende interface die de hoogste prioriteit heeft in de servicevolgorde geconfigureerd. **Eerste actieve Ethernet** is standaard geselecteerd. Dit is ook de standaardinstelling geconfigureerd door macOS.

- **EAP-type**: Selecteer het type Extensible Authentication Protocol (EAP) dat wordt gebruikt om beveiligde bekabelde verbindingen te verifiëren. Uw opties zijn:

  - **EAP-FAST**: Voer de **PAC-instellingen (Protected Access Credential)** in. Deze optie gebruikt beveiligde toegangsreferenties om een geverifieerde tunnel tussen de client en de verificatieserver te maken. Uw opties zijn:
    - **(PAC) niet gebruiken**
    - **(PAC) gebruiken**: Als er een al PAC-bestand bestaat, gebruik dit dan.
    - **PAC gebruiken en inrichten**: Maak het PAC-bestand en voeg dit toe aan uw apparaten.
    - **PAC anoniem inrichten en gebruiken**: maak het PAC-bestand en voeg het toe aan uw apparaten zonder verificatie met de server.

  - **EAP-TLS**: Voer ook in:

    - **Vertrouwelijke server** - **Namen van certificaatservers**: **voeg** een of meer algemene namen toe die worden gebruikt in de certificaten die zijn uitgegeven door uw vertrouwde certificeringsinstantie (CA). Wanneer u deze informatie verstrekt, kunt u het venster Dynamisch vertrouwen negeren dat wordt weergegeven op apparaten van gebruikers als zij verbinding maken met dit netwerk.
    - **Basiscertificaat voor servervalidatie**: Selecteer een bestaand profiel voor een vertrouwd basiscertificaat. Als vanuit de client verbinding wordt gemaakt met het netwerk wordt dit certificaat aan de server gepresenteerd. Het wordt gebruikt om de verbinding te verifiëren.
    - **Clientverificatie** - **Certificaten**: Selecteer het profiel van het SCEP- of PKCS-clientcertificaat dat ook op het apparaat is geïmplementeerd. Dit certificaat is de identiteit die door het apparaat wordt gepresenteerd aan de server om de verbinding te verifiëren.
    - **Identiteitsprivacy (externe identiteit)** : Voer de tekst in die wordt verzonden in antwoord op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben, zoals `anonymous`. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.

  - **EAP-TTLS**: Voer ook in:

    - **Vertrouwelijke server** - **Namen van certificaatservers**: **voeg** een of meer algemene namen toe die worden gebruikt in de certificaten die zijn uitgegeven door uw vertrouwde certificeringsinstantie (CA). Wanneer u deze informatie verstrekt, kunt u het venster Dynamisch vertrouwen negeren dat wordt weergegeven op apparaten van gebruikers als zij verbinding maken met dit netwerk.
    - **Basiscertificaat voor servervalidatie**: Selecteer een bestaand profiel voor een vertrouwd basiscertificaat. Als vanuit de client verbinding wordt gemaakt met het netwerk wordt dit certificaat aan de server gepresenteerd. Het wordt gebruikt om de verbinding te verifiëren.
    - **Clientverificatie**: Een **verificatiemethode** selecteren. Uw opties zijn:
      - **Gebruikersnaam en wachtwoord**: De gebruiker wordt gevraagd om een gebruikersnaam en wachtwoord om de verbinding te verifiëren. Voer ook in:
        - **Niet-EAP-methode (interne identiteit)** : Selecteer hoe de verbinding moet worden geverifieerd. Zorg ervoor dat u hetzelfde protocol kiest dat op uw netwerk is geconfigureerd. Uw opties zijn:
          - **Niet-versleuteld wachtwoord (PAP)**
          - **Challenge Henshake Authentication Protocol (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP versie 2 (MS-CHAP v2)**
      - **Certificaten**: Selecteer het profiel van het SCEP- of PKCS-clientcertificaat dat ook op het apparaat is geïmplementeerd. Dit certificaat is de identiteit die door het apparaat wordt gepresenteerd aan de server om de verbinding te verifiëren.
      - **Identiteitsprivacy (externe identiteit)** : Voer de tekst in die wordt verzonden in antwoord op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben, zoals `anonymous`. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.

  - **LEAP**

  - **PEAP**: Voer ook in:

    - **Vertrouwelijke server** - **Namen van certificaatservers**: **voeg** een of meer algemene namen toe die worden gebruikt in de certificaten die zijn uitgegeven door uw vertrouwde certificeringsinstantie (CA). Wanneer u deze informatie verstrekt, kunt u het venster Dynamisch vertrouwen negeren dat wordt weergegeven op apparaten van gebruikers als zij verbinding maken met dit netwerk.
    - **Basiscertificaat voor servervalidatie**: Selecteer een bestaand profiel voor een vertrouwd basiscertificaat. Als vanuit de client verbinding wordt gemaakt met het netwerk wordt dit certificaat aan de server gepresenteerd. Het wordt gebruikt om de verbinding te verifiëren.
    - **Clientverificatie**: Een **verificatiemethode** selecteren. Uw opties zijn:
      - **Gebruikersnaam en wachtwoord**: De gebruiker wordt gevraagd om een gebruikersnaam en wachtwoord om de verbinding te verifiëren.
      - **Certificaten**: Selecteer het profiel van het SCEP- of PKCS-clientcertificaat dat ook op het apparaat is geïmplementeerd. Dit certificaat is de identiteit die door het apparaat wordt gepresenteerd aan de server om de verbinding te verifiëren.
      - **Identiteitsprivacy (externe identiteit)** : Voer de tekst in die wordt verzonden in antwoord op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben, zoals `anonymous`. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt mogelijk niets. Zorg ervoor dat u [dit profiel toewijst](device-profile-assign.md) en[de status ervan bewaakt](device-profile-monitor.md).

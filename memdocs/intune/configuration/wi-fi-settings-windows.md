---
title: Wi-Fi-instellingen toevoegen voor Windows 10-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Voeg een Wi-Fi-configuratieprofiel toe of maak een Wi-Fi-configuratieprofiel met behulp van Wi-Fi-instellingen voor apparaten met Windows 10 en hoger in Microsoft Intune. U kunt eenvoudige basisinstellingen of instellingen op ondernemingsniveau configureren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.reviewer: tycast
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea4b196a6b2fade8ca926d13c3436207cb4b764e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429773"
---
# <a name="add-wi-fi-settings-for-windows-10-and-later-devices-in-intune"></a>Wi-Fi-instellingen toevoegen voor apparaten met Windows 10 en hoger in Intune

U kunt een profiel maken met specifieke Wi-Fi-instellingen en dit profiel vervolgens implementeren op uw apparaten met Windows 10 of hoger. Microsoft Intune bevat veel functies, waaronder het verifiëren bij uw netwerk, het gebruik van een vooraf gedeelde sleutel en meer.

In dit artikel worden deze instellingen beschreven.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een apparaatprofiel](wi-fi-settings-configure.md).

## <a name="basic-profile"></a>Basic-profiel

- **Wi-Fi-type**: Selecteer **Basic**. 

- **Wi-Fi-naam (SSID)** : Afkorting voor serviceset-id. Deze waarde is de echte naam van het draadloze netwerk waarmee apparaten verbinding maken. Gebruikers zien echter alleen de **Verbindingsnaam** die u hebt geconfigureerd wanneer ze de verbinding kiezen.

- **Verbindingsnaam**: Voer een gebruikersvriendelijke naam voor deze Wi-Fi-verbinding in. De tekst die u invoert, is de naam die gebruikers op hun apparaat te zien krijgen in de lijst met beschikbare verbindingen.

- **Automatisch verbinding maken binnen bereik**: Wanneer **Ja** is geselecteerd, maken apparaten automatisch verbinding als ze binnen het bereik van dit netwerk komen. Wanneer **Nee** is geselecteerd, maken apparaten niet automatisch verbinding.

  - **Verbinding maken met een voorkeursnetwerk indien beschikbaar**: Als de apparaten zich binnen het bereik van een voorkeursnetwerk bevinden, kiest u **Ja** om het voorkeursnetwerk te gebruiken. Kies **Nee** om het Wi-Fi-netwerk in dit configuratieprofiel te gebruiken.

    U maakt bijvoorbeeld een Wi-Fi-netwerk met de naam **ContosoCorp** en gebruikt **ContosoCorp** binnen dit configuratieprofiel. Ook het Wi-Fi-netwerk **ContosoGuest** ligt binnen bereik. Wanneer de bedrijfsapparaten binnen het bereik vallen, wilt u dat deze automatisch verbinding maken met **ContosoCorp**. In dit scenario stelt u de eigenschap **Verbinding maken met voorkeursnetwerk indien beschikbaar** in op **Nee**.

  - **Verbinding maken met dit netwerk, zelfs wanneer de SSID van het netwerk niet wordt uitgezonden**: Kies **Ja** als u wilt dat het configuratieprofiel automatisch verbinding maakt met uw netwerk, zelfs wanneer het netwerk verborgen is (wat betekent dat de SSID niet openbaar wordt uitgezonden). Kies **Nee** als u niet wilt dat dit configuratieprofiel verbinding maakt met uw verborgen netwerk.

- **Limiet voor verbinding naar gebruik**: Een beheerder kan kiezen hoe het verkeer van het netwerk wordt gemeten. Toepassingen kunnen vervolgens hun gedrag voor netwerkverkeer aanpassen op basis van deze instelling. Uw opties zijn:

  - **Onbeperkt**: Standaard. De verbinding niet wordt gemeten en er zijn geen beperkingen op het verkeer.
  - **Vast**: Gebruik deze optie als het netwerk is geconfigureerd met een vaste limiet voor het netwerkverkeer. Nadat deze limiet is bereikt, is toegang tot het netwerk niet meer toegestaan.
  - **Variabel**: Gebruik deze optie als het netwerkverkeer per byte in rekening wordt gebracht (kosten per byte).

- **Type voor draadloze beveiliging**: Het beveiligingsprotocol dat wordt gebruikt voor verificatie van apparaten in uw netwerk. Uw opties zijn:
  - **Open (geen verificatie)** : Gebruik deze optie alleen als het netwerk niet beveiligd is.
  - **WPA/WPA2-Personal**: Dit is een veiligere optie die doorgaans wordt gebruikt voor Wi-Fi-connectiviteit. Voor betere beveiliging kunt u ook een vooraf gedeelde wachtwoordsleutel of netwerksleutel invoeren.

    - **Vooraf gedeelde sleutel** (PSK): Optioneel. Dit wordt weergegeven wanneer u de optie **WPA/WPA2-Personal** kiest als beveiligingstype. Wanneer het netwerk van uw organisatie is ingesteld of geconfigureerd, wordt er ook een wachtwoord of netwerksleutel geconfigureerd. Voer dit wachtwoord of deze netwerksleutel in voor de PSK-waarde. Voer een tekenreeks in van minimaal 8 en maximaal 64 tekens. Als het wachtwoord of de netwerksleutel 64 tekens lang is, voert u hexadecimale tekens in.

      > [!IMPORTANT]
      > De PSK is hetzelfde voor alle apparaten waarop u het profiel richt. Als de sleutel is gecompromitteerd, kan deze door elk apparaat worden gebruikt om verbinding te maken met het Wi-Fi-netwerk. Beveilig uw PSK's om onbevoegde toegang te voor komen.

- **Proxyinstellingen van bedrijf**: Kies deze optie om de proxyinstellingen binnen uw organisatie te gebruiken. Uw opties zijn:
  - **Geen**: Er zijn geen proxyinstellingen geconfigureerd.
  - **Handmatig configureren**: voer het **IP-adres van de proxyserver** en het bijbehorende **poortnummer** in.
  - **Automatisch configureren**: voer de URL in die naar een proxyscript voor automatische configuratie (PAC) verwijst. Voer bijvoorbeeld `http://proxy.contoso.com/proxy.pac` in.

## <a name="enterprise-profile"></a>Enterprise-profiel

- **Wi-Fi-type**: Kies **Enterprise**.

- **Wi-Fi-naam (SSID)** : Afkorting voor serviceset-id. Deze waarde is de echte naam van het draadloze netwerk waarmee apparaten verbinding maken. Gebruikers zien echter alleen de **Verbindingsnaam** die u hebt geconfigureerd wanneer ze de verbinding kiezen.

- **Verbindingsnaam**: Voer een gebruikersvriendelijke naam voor deze Wi-Fi-verbinding in. De tekst die u invoert, is de naam die gebruikers op hun apparaat te zien krijgen in de lijst met beschikbare verbindingen.

- **Automatisch verbinding maken binnen bereik**: Wanneer **Ja** is geselecteerd, maken apparaten automatisch verbinding als ze binnen het bereik van dit netwerk komen. Wanneer **Nee** is geselecteerd, maken apparaten niet automatisch verbinding.
  - **Verbinding maken met een voorkeursnetwerk indien beschikbaar**: Als de apparaten zich binnen het bereik van een voorkeursnetwerk bevinden, kiest u **Ja** om het voorkeursnetwerk te gebruiken. Kies **Nee** om het Wi-Fi-netwerk in dit configuratieprofiel te gebruiken.

    U maakt bijvoorbeeld een Wi-Fi-netwerk met de naam **ContosoCorp** en gebruikt **ContosoCorp** binnen dit configuratieprofiel. Ook het Wi-Fi-netwerk **ContosoGuest** ligt binnen bereik. Wanneer de bedrijfsapparaten binnen het bereik vallen, wilt u dat deze automatisch verbinding maken met **ContosoCorp**. In dit scenario stelt u de eigenschap **Verbinding maken met voorkeursnetwerk indien beschikbaar** in op **Nee**.

  - **Verbinding maken met dit netwerk, zelfs wanneer de SSID van het netwerk niet wordt uitgezonden**: Kies **Ja** als u wilt dat het configuratieprofiel automatisch verbinding maakt met uw netwerk, zelfs wanneer het netwerk verborgen is (wat betekent dat de SSID niet openbaar wordt uitgezonden). Kies **Nee** als u niet wilt dat dit configuratieprofiel verbinding maakt met uw verborgen netwerk.

- **Limiet voor verbinding naar gebruik**: Een beheerder kan kiezen hoe het verkeer van het netwerk wordt gemeten. Toepassingen kunnen vervolgens hun gedrag voor netwerkverkeer aanpassen op basis van deze instelling. Uw opties zijn:

  - **Onbeperkt**: Standaard. De verbinding niet wordt gemeten en er zijn geen beperkingen op het verkeer.
  - **Vast**: Gebruik deze optie als het netwerk is geconfigureerd met een vaste limiet voor het netwerkverkeer. Nadat deze limiet is bereikt, is toegang tot het netwerk niet meer toegestaan.
  - **Variabel**: Gebruik deze optie als het netwerkverkeer per byte in rekening wordt gebracht.

- **Eenmalige aanmelding (SSO)** : Hiermee kunt u eenmalige aanmelding (SSO) configureren, waarbij referenties worden gedeeld voor aanmelden via een computer en via een Wi-Fi-netwerk. Uw opties zijn:
  - **Uitschakelen**: Hiermee schakelt u SSO-gedrag uit. De gebruiker moet afzonderlijk bij het netwerk worden geverifieerd.
  - **Inschakelen voordat de gebruiker zich aanmeldt bij het apparaat**: gebruik eenmalige aanmelding om te verifiëren bij het netwerk net vóór het aanmeldingsproces voor de gebruiker.
  - **Inschakelen nadat de gebruiker zich aanmeldt bij het apparaat**: gebruik eenmalige aanmelding om te verifiëren bij het netwerk direct nadat het aanmeldingsproces voor de gebruiker is voltooid.
  - **Maximale tijd voor het verifiëren voordat de time-out optreedt**: geef het maximum aantal seconden op dat moet worden gewacht voordat de verificatie bij het netwerk wordt uitgevoerd, tussen 1 en 120 seconden.
  - **Windows toestaan om een gebruiker te vragen om aanvullende verificatiereferenties**: Als u **Ja** kiest, staat u toe dat het Windows-systeem de gebruiker om aanvullende verificatiereferenties vraagt als dit conform de verificatiemethode is vereist. Kies **Nee** om deze vragen te verbergen.

- **In PMK-cache (Pairwise Master Key) opslaan inschakelen**: Selecteer **Ja** om de PMK die bij verificatie is gebruikt in de cache op te slaan. Doorgaans zorgt plaatsing in de cache ervoor dat verificatie bij het netwerk sneller kan worden voltooid. Kies **Nee** om de verificatiehandshake af te dwingen wanneer u verbinding met het Wi-Fi-netwerk maakt.

  - **Maximale tijd dat een PMK in de cache wordt opgeslagen**: voer het aantal minuten in dat een Pairwise Master Key (PMK) wordt opgeslagen in de cache, tussen 5 en 1440 minuten.
  - **Maximaal aantal PMK's dat in de cache wordt opgeslagen**: voer het aantal sleutels in dat wordt opgeslagen in de cache, tussen 1 en 255.

- **Verificatie vooraf inschakelen**: Door verificatie vooraf kan het profiel verifiëren bij alle toegangspunten voor het netwerk in het profiel voordat u verbinding maakt. Bij het verplaatsen tussen toegangspunten kunnen gebruikers of apparaten door verificatie vooraf sneller opnieuw verbinding maken. Kies **Ja** als u wilt dat het profiel verifieert bij alle toegangspunten voor dit netwerk die binnen het bereik vallen. Kies **Nee** als u wilt vereisen dat gebruikers of apparaten bij elk toegangspunt afzonderlijk verifiëren.

  - **Maximum aantal pogingen voor verificatie vooraf**: voer in hoe vaak verificatie vooraf mag worden geprobeerd, tussen 1 en 16.

- **EAP-type**: Kies het type Extensible Authentication Protocol (EAP) dat wordt gebruikt om beveiligde draadloze verbindingen te verifiëren. Uw opties zijn:

  - **EAP-SIM**
  - **EAP-TLS**
  - **EAP-TTLS**
  - **Beveiligde PEAP** (PEAP)

    **Extra instellingen EAP-TLS, EAP-TTLS en PEAP**:

    > [!NOTE]
    > Momenteel worden alleen SCEP-certificaatprofielen ondersteund bij het gebruik van een EAP-type. PKCS-certificaatprofielen worden niet ondersteund. Steeds wanneer een gebruiker wordt gevraagd een certificaat in te voeren, moet u een SCEP-certificaat kiezen.

    - **Server Trust**  

      **Namen van certificaatservers**: Gebruiken met EAP-typen **EAP-TLS**, **EAP-TTLS** of **PEAP**. Voer een of meer algemene namen in die worden gebruikt in de certificaten die zijn uitgegeven door uw vertrouwde certificeringsinstantie (CA). Als u deze informatie verstrekt, kunt u het dialoogvenster Dynamisch vertrouwen negeren dat wordt weergegeven op apparaten van gebruikers als zij verbinding maken met dit Wi-Fi-netwerk.  

      **Basiscertificaat voor servervalidatie**: Gebruiken met EAP-typen **EAP-TLS**, **EAP-TTLS** of **PEAP**. Kies het profiel voor een vertrouwd basiscertificaat dat wordt gebruikt om de verbinding te verifiëren.  

      **Identiteitsprivacy (externe identiteit)** : Gebruiken met AEP-type **PEAP**. Voer de tekst in die wordt verzonden in antwoord op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.  

    - **Clientauthenticatie**

      **Clientcertificaat voor clientverificatie (identiteitscertificaat)** : Gebruiken met EAP-type **EAP-TLS**. Kies het certificaatprofiel dat wordt gebruikt om de verbinding te verifiëren.

      **Verificatiemethode**: Gebruiken met EAP-type **EAP-TTLS**. Selecteer de verificatiemethode voor de verbinding:  

      - **Certificaten**: selecteer het clientcertificaat dat het identiteitscertificaat is dat aan de server wordt gepresenteerd.
      - **Gebruikersnaam en wachtwoord**: voer een **niet-EAP-methode (interne identiteit)** in voor verificatie. Uw opties zijn:

        - **Niet-versleuteld wachtwoord (PAP)**
        - **Challenge Handshake (CHAP)**
        - **Microsoft CHAP (MS-CHAP)**
        - **Microsoft CHAP versie 2 (MS-CHAP v2)**

      **Identiteitsprivacy (externe identiteit)** : Gebruiken met EAP-type **EAP-TTLS**. Voer de tekst in die wordt verzonden in antwoord op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.

- **Proxyinstellingen van bedrijf**: Kies deze optie om de proxyinstellingen binnen uw organisatie te gebruiken. Uw opties zijn:
  - **Geen**: Er zijn geen proxyinstellingen geconfigureerd.
  - **Handmatig configureren**: voer het **IP-adres van de proxyserver** en het bijbehorende **poortnummer** in.
  - **Automatisch configureren**: voer de URL in die naar een proxyscript voor automatische configuratie (PAC) verwijst. Voer bijvoorbeeld `http://proxy.contoso.com/proxy.pac` in.

- **Afdwingen dat het Wi-Fi-profiel voldoet aan Federal Information Processing Standard (FIPS)** : Kies **Ja** wanneer u wilt valideren op basis van de FIPS 140-2-standaard. Deze standaard is vereist voor alle instanties van de Amerikaanse federale overheid die beveiligingssystemen op basis van cryptografie gebruiken om gevoelige, niet-geclassificeerde informatie te beveiligen die digitaal is opgeslagen. Kies **Nee** om niet FIPS-compatibel te zijn.

## <a name="use-an-imported-settings-file"></a>Een bestand met geïmporteerde instellingen gebruiken

Voor alle instellingen die niet beschikbaar zijn in Intune, kunt u Wi-Fi-instellingen exporteren vanaf een ander Windows-apparaat. Bij deze export wordt een XML-bestand met daarin alle instellingen gemaakt. Importeer vervolgens dit bestand in Intune en gebruik dit als het Wi-Fi-profiel. Zie [Wi-Fi-instellingen voor Windows-apparaten exporteren en importeren](wi-fi-settings-import-windows-8-1.md).

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt niets. Vervolgens [wijst u dit profiel toe](device-profile-assign.md).

## <a name="more-resources"></a>Meer bronnen

- Zie de instellingen die beschikbaar zijn voor [Windows 8.1](wi-fi-settings-import-windows-8-1.md).
- [Overzicht Wi-Fi-instellingen](wi-fi-settings-configure.md), met inbegrip van andere platformen.

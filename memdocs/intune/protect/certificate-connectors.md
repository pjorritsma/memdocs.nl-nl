---
title: Certificaatconnectors voor Microsoft Intune - Azure | Microsoft Docs
description: Meer informatie over het gebruik van certificaatconnectors voor SCEP- (Simple Certificate Enrollment Protocol) of PKCS- (Public Key Cryptography Standards) -certificaten en -certificaatprofielen met Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f891e7989ad3f0f8d798dd9a5f0207a19ac5b95
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/03/2020
ms.locfileid: "89428892"
---
# <a name="certificate-connectors-for-microsoft-intune"></a>Certificaatconnectors voor Microsoft Intune

Intune moet een certificaatconnector gebruiken om het gebruik van certificaten voor verificatie en het ondertekenen en versleutelen van e-mail met S/MIME te ondersteunen. Een certificaatconnector is software die u installeert op een on-premises server. Met de connector kunnen in de cloud beheerde apparaten certificaten inrichten vanuit een on-premises infrastructuur, zoals een certificeringsinstantie.

In dit artikel vindt u een beschrijving van de beschikbare connectors, de levenscyclus, vereisten voor gebruik en hoe u ze up-to-date kunt houden.  

## <a name="available-connectors"></a>Beschikbare connectors

Er zijn twee certificaatconnectors voor Intune. Elk heeft zijn eigen gebruik en vereisten.

### <a name="pfx-certificate-connector-for-microsoft-intune"></a>PFX-certificaatconnector voor Microsoft Intune

De **PFX-certificaatconnector** ondersteunt de implementatie van certificaten voor PCKS #12-certificaataanvragen en verwerkt aanvragen voor PFX-bestanden die zijn geïmporteerd in Intune voor S/MIME-e-mailversleuteling voor een specifieke gebruiker.

> [!TIP]
> Vóór de update van augustus voor deze connector werden PKCS #12-certificaataanvragen verwerkt door de *Intune-certificaatconnector*. Met de update van augustus werd de functionaliteit voor alle PKCS-certificaataanvragen geconsolideerd in de *PFX-certificaatconnector*, die automatische updates van de connector naar nieuwe versies ondersteunt en waarvoor gebruik van .NET Framework-versie 4.7.2 vereist is.
>
> De functionaliteit van de Microsoft Intune-connector is niet afgeschaft en kan nog steeds worden gebruikt met PKCS-certificaatprofielen. Als u echter geen SCEP gebruikt of op een andere manier het gebruik van NDES vereist, kunt u overschakelen naar de PFX-certificaatconnector en NDES van uw servers verwijderen. 

**De PFX-certificaatconnector**:

- Ondersteunt meerdere exemplaren van deze connector voor elke Intune-tenant. Elk exemplaar van de connector moet worden geïnstalleerd op een Windows-server en toegang hebben tot de persoonlijke sleutel die wordt gebruikt voor het versleutelen van de wachtwoorden van de geüploade PFX-bestanden.
- Kan op dezelfde server worden geïnstalleerd die een exemplaar van de *Microsoft Intune-connector* host.
- Ondersteunt [automatische updates](#automatic-update) naar nieuwe versies. Als u automatisch nieuwe versies wilt installeren, moet de computer die als host voor de connector fungeert contact opnemen met **autoupdate.msappproxy.net** op poort **443**. Als de connector niet automatisch kan worden bijgewerkt, kunt u deze handmatig bijwerken.
- Ondersteunt het intrekken van certificaten (hiervoor is connectorversie **6.2008.60.607** of hoger vereist)
- Heeft dezelfde netwerkvereisten als [beheerde apparaten](../fundamentals/intune-endpoints.md#access-for-managed-devices)

  Zie [Netwerkeindpunten voor Microsoft Intune](../fundamentals/intune-endpoints.md) en [Netwerkconfiguratievereisten en bandbreedte voor Intune](../fundamentals/network-bandwidth-use.md) voor meer informatie.

**De Windows-server waarop de connector wordt geïnstalleerd**:

- Hierop moet Windows Server 2012 R2 of hoger worden uitgevoerd.
- Hierop moet .NET Framework-versie 4.7.2 worden uitgevoerd.  

**De PFX-certificaatconnector installeren**:

Zie [De PFX-certificaatconnector downloaden, installeren en configureren](certficates-pfx-configure.md) voor begeleiding bij de installatie van deze connector.

### <a name="microsoft-intune-connector"></a>Microsoft Intune-connector

De **Microsoft Intune-connector** wordt soms ook wel de *Microsoft Intune Certificate Connector* genoemd. Deze connector ondersteunt de implementatie van certificaten wanneer u gebruikmaakt van *Simple Certificate Enrollment Protocol* (SCEP) en een Active Directory Certificate Services-certificeringsinstantie (CA) hebt. Dit type CA wordt ook *Microsoft-CA*genoemd.

Als u SCEP met een Microsoft-CA gebruikt, moet u ook de **registratieservice voor netwerkapparaten (NDES)** configureren. Daarom wordt deze connector vaak aangeduid als de *NDES-certificaatconnector*.

Als u een [certificeringsinstantie van derden gebruikt](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration), hoeft u deze connector niet te gebruiken en is NDES niet vereist.

**De Microsoft Intune-connector**:

- Wordt geïnstalleerd op een Windows-server, die ook een exemplaar van de *PFX-certificaatconnector* kan hosten.
- Ondersteunt maximaal 100 instanties van deze connector per tenant, met elke instantie op een afzonderlijke Windows-server. Wanneer u meerdere connectors gebruikt:
  - Alle exemplaren van de *Microsoft Intune connector* in uw omgeving moeten dezelfde versie hebben.
  - Uw infrastructuur ondersteunt redundantie en taakverdeling, aangezien elk beschikbaar connectorexemplaar uw certificaataanvragen kan verwerken.
- Voor het installeren van de nieuwe versie van de connector is een [handmatige update](#manual-update) vereist. Voor handmatige updates moet u de huidige connector verwijderen en vervolgens de nieuwe versie van de connector installeren. Er zijn geen aanvullende acties vereist.
- Ondersteunt de *Federal Information Processing Standard-modus (FIPS)* . FIPS is niet vereist. Als FIPS is ingeschakeld, kunt u certificaten verlenen en intrekken.
- Hiervoor zijn dezelfde netwerkvereisten van toepassing als voor [beheerde apparaten](../fundamentals/intune-endpoints.md#access-for-managed-devices).

  Zie [Netwerkeindpunten voor Microsoft Intune](../fundamentals/intune-endpoints.md) en [Netwerkconfiguratievereisten en bandbreedte voor Intune](../fundamentals/network-bandwidth-use.md) voor meer informatie.

**De Windows-server waarop de connector wordt geïnstalleerd**:

- Hierop moet Windows Server 2012 R2 of hoger worden uitgevoerd.
- Hierop moet .NET Framework-versie 4.5 worden uitgevoerd. Als deze connector op dezelfde server als de *PFX-certificaatconnector* wordt geïnstalleerd, moet u .NET Framework 4.7.2 gebruiken. Dit is vereist voor de PFX-connector.
- Kan niet dezelfde server zijn die als host fungeert voor uw uitgevende certificeringsinstantie (CA).
- Als deze voor SCEP wordt gebruikt met een Microsoft-CA, is toegang vereist tot een server waarop NDES wordt uitgevoerd. NDES wordt uitgevoerd op een Windows-server en kan worden uitgevoerd op dezelfde server als deze connector.

**Als NDES is vereist**:

- Verbeterde beveiliging van Internet Explorer[ moet zijn uitgeschakeld op de server die als host fungeert voor NDES](/previous-versions/windows/it-pro/windows-server-2003/cc775800(v=ws.10)) en de server die de *Microsoft Intune-connector* host.
- Voor de connector zijn aanvullende configuraties vereist om te communiceren met NDES. U vindt de procedures voor het installeren en configureren van NDES bij de procedures voor het installeren van de *Microsoft Intune-connector*.

  Zie [Hulp bij Registratieservice voor netwerkapparaten](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)) voor meer informatie.

**De Microsoft Intune-connector installeren**:

Zie [Infrastructuur configureren om SCEP te ondersteunen in Intune](certificates-scep-configure.md) voor meer informatie over het installeren van deze connector.

## <a name="connector-lifecycle"></a>Levenscyclus van connector

Er worden regelmatig bijgewerkte versies van certificaatconnectors uitgebracht. Aankondigingen voor nieuwe releases van de connector worden weergegeven in het artikel (What's New] (.. /fundamentals/whats-new.MD) voor Intune en in de sectie [Wat is er nieuw voor connectors](#whats-new-for-connectors) aan het einde van dit artikel.

Als er een nieuwe versie wordt uitgebracht, wordt de ondersteuning voor de vorige versie afgeschaft. Er geldt nog een beperkte respijtperiode voor het voortgezette gebruik. Nadat de respijtperiode is verlopen, wordt de ondersteuning voor de afgeschafte versie beëindigd. Deze kan dan op elk gewenst moment niet meer functioneren. De respijtperiode is zes maanden.

Plan het bijwerken van een connector naar de nieuwste versie zodra u daarvoor in de gelegenheid bent. Elke connector heeft een ander pad naar de update:

- **Connector voor PFX-certificaten voor Microsoft Intune**: ondersteunt automatische updates.
- **Microsoft Intune-connector**: moet handmatig worden bijgewerkt.

### <a name="automatic-update"></a>Automatisch bijwerken

Als dit door het connectortype en uw omgeving wordt ondersteund, kan Intune de connector automatisch bijwerken naar de meest recente versie nadat de connectorversie is uitgebracht.  

Voor automatisch bijwerken, moet de server die als host fungeert voor de connector toegang hebben tot de **Azure-updateservice**:

- Poort: **443**
- Eindpunt: **autoupdate.msappproxy.net**

Als firewalls, infrastructuur of netwerkconfiguraties de toegang voor automatische updates beperken, moet u de problemen met de blokkering oplossen of de connector handmatig bijwerken naar de nieuwe versie.

### <a name="manual-update"></a>Handmatig bijwerken

Het proces voor het handmatig bijwerken van een certificaatconnector is hetzelfde als voor het opnieuw installeren van een connector.

U kunt een certificaatconnector ook handmatig bijwerken wanneer deze automatische updates ondersteunt. U kunt de connector bijvoorbeeld handmatig bijwerken wanneer uw netwerkconfiguratie een automatische update blokkeert.  

### <a name="to-reinstall-a-certificate-connector"></a>Ga als volgt te werk om een certificaatconnector opnieuw te installeren

1. Gebruik **Windows-apps en -onderdelen** op de Windows-server waarop de connector wordt gehost om de connector te verwijderen.

2. U kunt de nieuwe versie installeren middels de procedure om een nieuwe versie van de connector te installeren. Controleer of er nieuwe of bijgewerkte vereisten zijn wanneer u een nieuwere versie van een connector installeert:
   - SCEP: [Infrastructuur configureren om SCEP te ondersteunen in Intune](certificates-scep-configure.md)
   - PKCS: [De PFX-certificaatconnector voor Microsoft Intune downloaden, installeren en configureren](certficates-pfx-configure.md)

## <a name="connector-status-and-version"></a>Connectorstatus en -versie

In het beheercentrum van Microsoft Endpoint Manager kunt u een certificaatconnector selecteren om informatie over de status ervan weer te geven en de versie te controleren:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Ga naar **Tenantbeheer** > **Connectors en tokens** > **Certificaatconnectors**.

3. Selecteer een connector om de status ervan weer te geven.

Als u de connectorstatus weergeeft:

- Bij afgeschafte connectors wordt een **waarschuwing** weergegeven. Na de respijtperiode van zes maanden wordt de waarschuwing gewijzigd in een fout.
- Bij connectors waarvoor de respijtperiode is afgelopen, wordt een fout weergegeven. Deze connectors worden niet meer ondersteund en kunnen op elk moment niet meer werken.

## <a name="whats-new-for-connectors"></a>Wat is er nieuw voor connectors

Updates voor de twee certificaatconnectors worden regelmatig uitgebracht. Als we een connector bijwerken, kunt u hier over de wijzigingen lezen.

### <a name="pfx-certificate-connector-release-history"></a>Releasegeschiedenis van de PFX-certificaatconnector

De *PFX-certificaatconnector voor Microsoft Intune* [ondersteunt automatische updates](#automatic-update).

#### <a name="august-26-2020"></a>26 augustus 2020

**Versie 6.2008.60.607** - Wijzigingen in deze release:

- Hiervoor is .NET Framework-versie 4.7.2 vereist
- Vervangt het gebruik van de *Microsoft Intune-connector* voor gebruik met PKCS-certificaatprofielen. De *PFX-certificaatconnector* is nu de enige connector die is vereist voor het gebruik van PCKS #12- of geïmporteerde PFX-certificaten.
- Voegt ondersteuning toe voor het gebruik van PKCS-certificaatprofielen met alle ondersteunde platformen, met uitzondering van Windows 8.1.
- Voegt ondersteuning toe voor het intrekken van certificaten voor Outlook S/MIME.

#### <a name="november-18-2019"></a>18 november 2019

**Versie: 6.1911.11.602** -wijzigingen in deze release:

- S/MIME-ondersteuning voor het importeren van PFX is toegevoegd.  

#### <a name="may-17-2019"></a>17 mei 2019

**Versie 6.1905.0.404** - wijzigingen in deze release:

- Er is een probleem opgelost waarbij bestaande PFX-certificaten steeds opnieuw worden verwerkt, zodat de connector stopt met het verwerken van nieuwe aanvragen. 

#### <a name="may-6-2019"></a>6 mei 2019

**Versie 6.1905.0.402** - wijzigingen in deze release:

- De polling-interval voor de connector wordt verlaagd van 5 minuten naar 30 seconden.

#### <a name="april-2-2019"></a>2 april 2019

**Versie 6.1904.0.401** - wijzigingen in deze release:

- Deze connector ondersteunt nu automatische updates.
- Er is een probleem opgelost waarbij de connector zich mogelijk niet kan inschrijven bij Intune na aanmelding bij de connector met een globale beheerdersaccount.

### <a name="microsoft-intune-connector-release-history"></a>Releasegeschiedenis voor Microsoft Intune-connector

#### <a name="april-2-2019"></a>2 april 2019

**Versie 6.1904.1.0** - wijzigingen in deze release:  

- Er is een probleem opgelost waarbij de connector zich mogelijk niet kan inschrijven bij Intune na aanmelding bij de connector met een globale beheerdersaccount.
- Deze bevat betrouwbaarheidsoplossingen voor het intrekken van certificaten.
- Deze bevat prestatieoplossingen om de snelheid te verhogen waarmee PKCS-certificaataanvragen worden verwerkt.

## <a name="next-steps"></a>Volgende stappen

Maak SCEP-, PKCS- of geïmporteerde PKCS-certificaatprofielen voor elk platform dat u wilt gebruiken. Raadpleeg de volgende artikelen om verder te gaan:

- [Infrastructuur configureren om SCEP-certificaten te ondersteunen in Intune](certificates-scep-configure.md)  
- [PKCS-certificaten configureren en beheren met Intune](certficates-pfx-configure.md)  
- [Een geïmporteerd PKCS-certificaatprofiel maken](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)

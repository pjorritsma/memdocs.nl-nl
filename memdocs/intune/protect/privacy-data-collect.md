---
title: Gegevensverzameling in Intune
titleSuffix: Microsoft Intune
description: Lees informatie over het verzamelen van persoonlijke gegevens in Intune.
keywords: privacy, persoonlijke gegevens
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1171740-936d-46a5-af37-f418bd6fa63e
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcd7ff1ae51314bc57be2bed39c7fe8ca7114d82
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076104"
---
# <a name="data-collection-in-intune"></a>Gegevensverzameling in Intune

Wanneer gebruikers hun zakelijke of persoonlijke apparaten inschrijven met behulp van Intune, verzamelt, verwerkt en deelt Intune bepaalde persoonlijke gegevens ter ondersteuning van bedrijfsactiviteiten, om zaken te doen met de klant en de service te ondersteunen. Intune verzamelt persoonlijke gegevens van de volgende bronnen:

- De beheerders gebruiken Intune in het Microsoft Endpoint Manager-beheercentrum.
- Apparaten van eindgebruikers (wanneer apparaten zijn ingeschreven voor Intune-beheer en tijdens het gebruik).
- Klantaccounts bij de services van derden (volgens de instructies van de beheerder).
- Diagnostische gegevens, prestatiegegevens en gebruiksgegevens.

Uit deze resources verzamelt Intune gegevens die in de volgende twee categorieën vallen: [vereist](#required-data), [optioneel](#optional-data). In elk van de categorieën worden gegevens verder onderverdeeld in klantgegevens, persoonlijke gegevens, diagnostische gegevens en door de service gegenereerde gegevens. 

> [!NOTE]
> We verkopen gegevens die door onze service worden verzameld om geen enkele reden aan externe partijen.

## <a name="required-data"></a>Vereiste gegevens

Gegevens in de categorie Vereist zijn gegevens die nodig zijn om onze service te laten werken zoals de klant verwacht. De meeste gegevens die door Intune worden verzameld, zijn vereiste gegevens. Deze gegevens zijn gekoppeld aan een gebruiker, apparaat of toepassing en zijn essentieel voor de aard van het beheer. De verzamelde gegevens bevatten zowel persoonlijke als niet-persoonlijke gegevens. Persoonlijke gegevens zijn identificeerbare gegevens, aan de hand waarvan de eindgebruiker direct kan worden geïdentificeerd, of gepseudonimiseerde gegevens met een unieke, door het systeem gegenereerde id, die worden gebruikt om de zakelijke service aan klanten te leveren en gegevens en accountgegevens te ondersteunen. Niet-persoonlijke gegevens zijn door de service gegenereerde metagegevens van het systeem en organisatorische/tenantgegevens. Intune verzamelt daarnaast ook gegevens voor het beheren van toegang tot administratieve rollen en functies via functies als [Op rollen gebaseerd toegangsbeheer](../fundamentals/role-based-access-control.md).

Vereiste gegevens die door Intune worden verzameld, zijn onder andere (maar niet alleen): 

- Gebruikersgegevens
  - Weergave van de naam van de eigenaar/gebruiker (de in Azure geregistreerde naam van de gebruiker, zoals aangegeven in AzureUserID)
  - User principal name of e-mailadres
  - Telefoonnummer
  - Identificaties van externe gebruikers (zoals Apple ID)
- Hardware-inventarisatiegegevens
  - Apparaatnaam
  - Fabrikant
  - Besturingssysteem
  - Serienummer
  - IMEI-nummer
  - Het IP-adres
  - Wi-Fi MacAddress
  - ICCID
- Informatie uit auditlogboeken, waaronder gegevens over de volgende activiteiten
  - Beheren
  - Maken
  - Bijwerken (bewerken)
  - Verwijderen
  - Toewijzen
  - Externe taken
- Ondersteuningsinformatie
  - Contactgegevens (naam, telefoonnummer, e-mailadres)
  - E-mailwisselingen met Microsoft Ondersteuning en leden van het product- en/of kwaliteitsverbeteringsteam
- Toegangsbeheergegevens 
  - Statische verificators (wachtwoord van de klant)
  - Privacysleutels voor certificaten 
- Beheer- en accountgegevens
  - Voornaam en achternaam van de gebruiker met beheerdersrechten
  - Naam van de gebruiker met beheerdersrechten
  - UPN (e-mail)
  - Telefoonnummer
  - E-mailadres van accounteigenaar
  - Active Directory-id van de IT-beheerder van elke klant
  - Betalingsgegevens voor klantfacturering
  - Abonnementssleutel
- Toepassingsinventaris, zoals
  - app-naam
  - versie
  - app-id
  - grootte
  - installatielocatie
  - Inventarisgegevens van toepassingen worden alleen verzameld wanneer deze door de beheerder zijn gemarkeerd als een apparaat in bedrijfseigendom of wanneer de functie voor compatibele apps is ingeschakeld.  
- Tenant-id's van derden (zoals de Apple ID)
- Apparaatgegevens
  - Intune-apparaat-id
  - Apparaat-id van Azure Active Directory
  - Intune-apparaatbeheer-id
  - Tenant-id
  - Account-id
  - EAS-apparaat-id
  - Platformspecifieke id's
  - Apple ID voor iOS/iPadOS-apparaten
  - MAC-adres voor Mac-apparaten
  - Windows-id voor Windows-apparaten
- Beheerde toepassingsgegevens
  - Beheerde toepassing-id
  - Apparaattag van beheerde toepassing
  - Intune-apparaatbeheer-id
  - Apparaat-id van Azure Active Directory
  - Versleutelingssleutels
- Beheerdersgebruiksgegevens van alle Intune-tenants (bijvoorbeeld beheerdersbesturingselementen die zijn geselecteerd voor de communicatie met de beheerconsole)
- Gegevens van het tenantaccount (deze gegevens zijn beschikbaar via de blade van Intune)
  - Aantal ingeschreven apparaten of gebruikers
  - Aantal geïdentificeerde apparaatplatformen  
  - Aantal geïnstalleerde apparaten
  - installedDeviceCount: het aantal apparaten waarop de toepassing is geïnstalleerd.
  - notApplicableDeviceCount: het aantal apparaten waarvoor de toepassing niet van toepassing is.
  - notInstalledDeviceCount: het aantal apparaten waarvoor de toepassing van toepassing is, maar waarop de installatie niet is uitgevoerd.
  - pendingInstallDeviceCount: het aantal apparaten waarvoor de toepassing van toepassing is en waarvoor de installatie in behandeling is.

## <a name="optional-data"></a>Optionele gegevens

Gegevens in de categorie Optioneel zijn niet essentieel voor het product of de service-ervaring. Klanten kunnen de verzameling optionele gegevens beheren. Intune biedt klanten de mogelijkheid om zich aan of af te melden voor optionele gegevensverzameling. Voorbeelden van de optionele gegevens zijn gegevens die door Intune worden verzameld voor diagnose en telemetrie. Houd er rekening mee dat mensen naar onze mening dwingende redenen kunnen hebben om deze optionele gegevens te delen, omdat deze kansen creëren voor nieuwe en rijkere ervaringen, maar we begrijpen het belang om gebruikers de mogelijkheid te bieden om deze keuzes zelf te maken. 

Voorbeelden van optionele diagnostische gegevens zijn gegevens over toepassingsgebruik, fout- en prestatiegegevens. Alle diagnostische gegevens die Microsoft verzamelt tijdens het gebruik van Microsoft 365-apps voor bedrijfstoepassingen en -services, worden gepseudonimiseerd overeenkomstig de ISO/IEC 19944:2017-standaard (sectie 8.3.3).

## <a name="certain-end-user-data-or-content-is-never-collected"></a>Bepaalde eindgebruikersgegevens of -inhoud worden nooit verzameld

Intune verzamelt geen gespreks- of webbrowsegeschiedenis, persoonlijke e-mail, sms-berichten, contactpersonen, wachtwoorden voor persoonlijke accounts, agendagebeurtenissen of foto's, inclusief die in een foto-app of camera van eindgebruikers en staat beheerders niet toe deze te bekijken. Zie [Apparaten registreren](../enrollment/device-enrollment.md).

Zie [Hoe Microsoft gegevens categoriseert voor onlineservices](https://www.microsoft.com/trust-center/privacy/customer-data-definitions) voor meer informatie over de gegevenstypen en -definitie. 

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe Intune persoonlijke gegevens [opslaat en verwerkt](privacy-data-store-process.md), en [deelt](privacy-data-secure-share.md). 

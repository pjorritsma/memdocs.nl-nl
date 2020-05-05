---
title: Certificaat sjabloon machtigingen plannen
titleSuffix: Configuration Manager
description: Meer informatie over het plannen van de machtigingen die u nodig hebt om de certificaat sjablonen te configureren die Configuration Manager gebruikt.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 91434b70ca514430ab4cfd6815186bc6d6bc33db
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210125"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-configuration-manager"></a>Plannen van certificaat sjabloon machtigingen voor certificaat profielen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*


De volgende informatie kan u helpen bij het plannen van de configuratie van machtigingen voor de certificaat sjablonen die Configuration Manager gebruikt wanneer u certificaat profielen implementeert.  

## <a name="default-security-permissions-and-considerations"></a>Standaardbeveiligingsmachtigingen en overwegingen hiervoor  
 De standaard beveiligings machtigingen die vereist zijn voor de certificaat sjablonen die Configuration Manager gebruiken om certificaten voor gebruikers en apparaten aan te vragen, zijn als volgt:  

- Lezen en Registreren voor het account waarvan de toepassingsgroep Registratieservice voor netwerkapparaten gebruik maakt  

- Lezen voor het account waarmee de Configuration Manager-console wordt uitgevoerd  

  Zie [Configuring Certificate Infrastructure](../deploy-use/certificate-infrastructure.md)(Engelstalig) voor meer informatie over deze beveiligings machtigingen.  

  Wanneer u deze standaardconfiguratie gebruikt, kunnen gebruikers en apparaten niet rechtstreeks certificaten van de certificaatsjablonen aanvragen, en moeten alle aanvragen worden geïnitieerd door de registratieservice voor netwerkapparaten. Dit is een belangrijke beperking, omdat deze certificaatsjablonen moeten worden geconfigureerd met **Met de aanvraag meeleveren** voor het certificaat Onderwerp, wat betekent dat er een risico op imitatie bestaat als een kwaadwillende gebruiker of een apparaat waarmee is geknoeid, een certificaat aanvraagt. In de standaardconfiguratie moet een dergelijke aanvraag worden geïnitieerd door de registratieservice voor netwerkapparaten. Dit risico op imitatie blijft echter bestaan als er wordt geknoeid met de service waarop de registratieservice voor netwerkapparaten wordt uitgevoerd. Om dit risico te voorkomen, volgt u alle aanbevolen beveiligingsprocedures voor de registratieservice voor netwerkapparaten en voor de computer waarop deze rollenservice wordt uitgevoerd.  

  Als de standaardbeveiligingsmachtigingen niet voorzien in uw zakelijke vereisten, hebt u nog een andere optie om de beveiligingsmachtigingen voor de certificaatsjablonen te configureren: u kunt de machtigingen Lezen en Registreren toevoegen voor gebruikers en computers.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>De machtigingen Lezen en Registreren toevoegen voor gebruikers en computers  
 Het toevoegen van machtigingen voor lezen en inschrijven voor gebruikers en computers kan geschikt zijn als een afzonderlijk team het infrastructuur team van uw certificerings instantie (CA) beheert en dat afzonderlijke team Configuration Manager om te controleren of gebruikers een geldig Active Directory Domain Services account hebben voordat ze een certificaat profiel voor het aanvragen van een gebruikers certificaat kunnen verzenden. Voor deze configuratie moet u een of meer beveiligingsgroepen opgeven die de gebruikers bevatten, en vervolgens aan die groepen de machtigingen Lezen en Registreren verlenen voor de certificaatsjablonen. In dit scenario beheert de beheerder van de certificeringsinstantie de beveiligingscontrole.  

 U kunt op vergelijkbare wijze een of meer beveiligingsgroepen opgeven die computeraccounts bevatten, en aan deze groepen de machtigingen Lezen en Registreren verlenen voor de certificaatsjablonen. Als u een profiel voor een computercertificaat implementeert op een computer die lid is van een domein, moet aan het computeraccount van die computer de machtigingen Lezen en Registreren worden verleend. Deze machtigingen zijn niet vereist als de computer geen lid van een domein is. Als het bijvoorbeeld een werkgroepcomputer of een persoonlijk mobiel apparaat is.  

 Hoewel voor deze configuratie een extra beveiligingscontrole wordt gebruikt, is het niet raadzaam deze als aanbevolen procedure te gebruiken. De opgegeven gebruikers of eigen aren van de apparaten kunnen certificaten onafhankelijk van Configuration Manager aanvragen en waarden opgeven voor het certificaat onderwerp dat kan worden gebruikt om een andere gebruiker of een ander apparaat te imiteren.  

 Als u bovendien accounts opgeeft die niet kunnen worden geverifieerd op het moment dat de certificaataanvraag plaatsvindt, zal de certificaataanvraag standaard mislukken. Zo mislukt de certificaataanvraag bijvoorbeeld als de server waarop de registratieservice voor netwerkapparaten wordt uitgevoerd, zich in een Active Directory-forest bevindt dat niet wordt vertrouwd door het forest dat de sitesysteemserver van het certificaatregistratiepunt bevat. U kunt het certificaatregistratiepunt zodanig configureren dat het doorgaat als een account niet kan worden geverifieerd omdat er geen reactie is van een domeincontroller. Dit is echter geen aanbevolen beveiligingsprocedure.  

 Als het certificaatregistratiepunt is geconfigureerd om accountmachtigingen te controleren en er een domeincontroller beschikbaar is die de verificatieaanvraag afwijst (bijvoorbeeld als het account is vergrendeld of verwijderd), mislukt de aanvraag voor certificaatregistratie.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>De machtigingen Lezen en Registreren controleren voor gebruikers en computers die lid zijn van het domein  

1.  Maak op de site systeem server waarop het certificaat registratiepunt wordt gehost de volgende DWORD-register sleutel voor een waarde van 0: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Als een account niet kan worden geverifieerd omdat er geen reactie van een domeincontroller is, en u de machtigingscontrole wilt omzeilen:  

    -   Maak op de site systeem server waarop het certificaat registratiepunt wordt gehost de volgende DWORD-register sleutel voor een waarde van 1: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  Op de certificeringsinstantie die het certificaat verleent, voegt u op het tabblad **Beveiliging** bij de eigenschappen voor de certificaatsjabloon een of meer beveiligingsgroepen toe om de machtigingen Lezen en Registreren te verlenen aan de gebruiker of het apparaat.  

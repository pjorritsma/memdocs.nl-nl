---
title: Interoperabiliteit van besturingssysteem implementatie
titleSuffix: Configuration Manager
description: Meer informatie over interoperabiliteits problemen wanneer verschillende Configuration Manager sites in één hiërarchie verschillende versies gebruiken.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723549"
---
# <a name="plan-for-os-deployment-interoperability"></a>Compatibiliteit van besturingssysteem implementaties plannen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer verschillende Configuration Manager-sites in één hiërarchie verschillende versies gebruiken, is sommige Configuration Manager functionaliteit niet beschikbaar. Normaal gesp roken is de functionaliteit van de nieuwere versie van Configuration Manager niet toegankelijk op sites of op clients waarop een lagere versie wordt uitgevoerd. Zie [interoperabiliteit tussen verschillende versies van Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)voor meer informatie.  


## <a name="objects"></a>Objecten

Houd rekening met de volgende objecten wanneer u de site op het hoogste niveau in uw hiërarchie bijwerkt en andere sites in uw hiërarchie Configuration Manager met een lagere versie uitvoeren:  

### <a name="client-installation-package"></a>Client installatie pakket  

- De bron voor het standaard client installatie pakket wordt automatisch bijgewerkt. Alle distributie punten in de hiërarchie worden bijgewerkt met het nieuwe client installatie pakket. Dit gebeurt zelfs op distributie punten van sites in de hiërarchie met een lagere versie.  

- U kunt geen nieuwe versie-clients toewijzen aan sites die u nog niet hebt bijgewerkt naar de nieuwe versie. De toewijzing wordt geblokkeerd op het beheer punt.  

### <a name="boot-images"></a>Installatiekopieën  

- Wanneer u de site op het hoogste niveau bijwerkt naar de nieuwste versie van Configuration Manager, worden de standaard opstart installatie kopieën (x86 en x64) automatisch bijgewerkt. De update maakt gebruik van Windows ADK voor Windows 10, met inbegrip van Windows PE 10. De bestanden die aan de standaard installatie kopieën zijn gekoppeld, worden bijgewerkt met de meest recente Configuration Manager versie van de bestanden. Aangepaste opstart installatie kopieën worden niet automatisch bijgewerkt op de site. U moet aangepaste opstart installatie kopieën, waaronder oudere versies van Windows PE, hand matig bijwerken.  

- Vermijd het gebruik van dynamische media wanneer uw site hiërarchie sites bevat met verschillende versies van Configuration Manager. Gebruik in plaats daarvan op site gebaseerde media om contact op te nemen met een specifiek beheer punt. Nadat u alle sites hebt bijgewerkt naar dezelfde versie van Configuration Manager, kunt u dynamische media opnieuw gebruiken.

- Controleer of de nieuwste Configuration Manager opstart installatie kopieën uw aanpassingen bevatten. Werk vervolgens alle distributie punten op de nieuwe versie-sites bij met de nieuwste versie van de nieuwe opstart installatie kopieën.  

### <a name="user-state-migration-tool-usmt"></a>Hulpprogramma voor migratie van gebruikersstatus (USMT)  

Wanneer u de site op het hoogste niveau bijwerkt naar de nieuwste versie van Configuration Manager, wordt het standaard USMT-pakket automatisch bijgewerkt naar de meest recente versie. Aangepaste USMT-pakketten worden niet automatisch bijgewerkt. U moet deze pakketten hand matig bijwerken.  

### <a name="new-task-sequence-steps"></a>Stappen voor nieuwe takenreeksen  

Er worden regel matig nieuwe taken reeks stappen geïntroduceerd met nieuwe versies van Configuration Manager. Wanneer u een taken reeks implementeert met een nieuwe stap voor oudere clients, mislukt de taken reeks stap. Voordat u een takenreeks implementeert met een nieuwe stap, controleert u of de clients in de doelverzameling zijn bijgewerkt naar de nieuwe versie.  

### <a name="os-deployment-media"></a>BESTURINGSSYSTEEM implementatie media  

Wanneer de site wordt bijgewerkt naar een nieuwe versie, moet u alle media bijwerken met het nieuwe Configuration Manager-client pakket. Deze media typen zijn onder andere opstart bare, vastleg ging, vooraf geplaatste en zelfstandige.

### <a name="third-party-extensions-to-os-deployment"></a>Uitbrei dingen van derden voor besturingssysteem implementatie  

Wanneer u uitbrei dingen van derden hebt voor de implementatie van besturings systemen en u verschillende versies van Configuration Manager-sites of Configuration Manager-clients hebt, kunnen er problemen optreden met de uitbrei dingen.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Nieuwste versie van Configuration Manager-sites in een gemengde hiërarchie  

Wanneer u een upgrade uitvoert van een site naar de meest recente versie van Configuration Manager, worden taken reeksen die verwijzen naar het standaard client installatie pakket automatisch gestart voor het implementeren van de meest recente Configuration Manager-client versie.

Taken reeksen die naar een aangepast client installatie pakket verwijzen, blijven de versie van de client in dat aangepaste pakket implementeren. Aangepaste pakketten bevatten waarschijnlijk een eerdere versie van de Configuration Manager-client. Als u problemen met de implementatie van taken reeksen wilt voor komen, moet u alle aangepaste client installatie pakketten bijwerken naar de meest recente versie.

Wanneer u een taken reeks configureert om een aangepast client installatie pakket te gebruiken, voert u een van de volgende acties uit:

- Werk de taken reeks stap bij om de nieuwste Configuration Manager versie van het client installatie pakket te gebruiken
- Het aangepaste pakket bijwerken voor het gebruik van de nieuwste Configuration Manager client installatie bron

> [!IMPORTANT]  
> Implementeer geen taken reeks die verwijst naar het nieuwste Configuration Manager-client installatie pakket naar clients op een oudere Configuration Manager-site. Wanneer clients die zijn toegewezen aan een oudere Configuration Manager site worden bijgewerkt naar de nieuwste Configuration Manager-client versie, Configuration Manager blokkeert de toewijzing aan de oudere Configuration Manager-site. Deze clients zijn niet meer toegewezen aan een site. Totdat u de client hand matig toewijst aan de meest recente Configuration Manager-site of de oudere Configuration Manager versie van de client opnieuw installeert op de computer, zijn deze clients niet-beheerd.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Oudere versies van Configuration Manager in een gemengde hiërarchie  

Wanneer u uw centrale beheer site bijwerkt naar de nieuwste versie van Configuration Manager, moet u ervoor zorgen dat de implementatie taken reeksen van het besturings systeem die u implementeert, deze clients niet in een niet-beheerde status laten staan. Bijvoorbeeld als u implementeert voor clients die zijn toegewezen aan een oudere Configuration Manager site die u nog niet hebt bijgewerkt naar de meest recente versie van Configuration Manager.

Maak een kopie van een taken reeks die u gebruikt om te implementeren op clients in de meest recente versie van Configuration Manager-site. Wijzig vervolgens de taken reeks zodat u deze kunt implementeren op clients in een oudere Configuration Manager-site. Configureer de taken reeks om te verwijzen naar een aangepast client installatie pakket dat gebruikmaakt van de oudere Configuration Manager client installatie bron. Als u nog niet beschikt over een aangepast client installatie pakket dat verwijst naar de oudere Configuration Manager client installatie bron, moet u er hand matig een maken.  

> [!Important]  
> Vanaf versie 1902 kunt u geen pakket of taken reeks implementeren naar een client versie 5,7730 of eerder. U kunt deze beperking omzeilen door de client bij te werken naar een nieuwere versie.<!-- SCCMDocs-pr issue #3493 -->

---
title: Veelgestelde vragen over producten en licenties
titleSuffix: Configuration Manager
description: Vind antwoorden op veelgestelde vragen over producten en licenties voor Configuration Manager.
ms.date: 07/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7c92423316f83841875aed2493442881bc3a1d74
ms.sourcegitcommit: 9eebe77af18045fceb3d41b43d76b370fe92b30e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/05/2020
ms.locfileid: "87821594"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Veelgestelde vragen over Configuration Manager branches en licenties

*Van toepassing op: Configuration Manager (current branch) & System Center Configuration Manager (onderhouds branche voor de lange termijn)*

Deze veelgestelde vragen hebben betrekking op veelvoorkomende licentie vragen over Configuration Manager current branch en de Long-term Servicing Branch (LTSB)-versies die beschikbaar zijn via micro soft Volume Licensing-Program ma's. Dit artikel is ter informatie bedoeld. Het vervangt geen documentatie met betrekking tot Configuration Manager-licenties. Zie voor meer informatie de [product voorwaarden](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). In de product termen worden de gebruiks voorwaarden voor alle micro soft-producten in volume licenties beschreven.

### <a name="whats-current-branch"></a><a name="bkmk_cb"></a>Wat is de huidige vertakking?

De huidige vertakking is de productie-gereed build van Configuration Manager die een actief service model biedt. Dit onderhouds model lijkt op de ervaring met Windows 10. Deze benadering biedt ondersteuning voor klanten die zich verplaatsen naar een Cloud uitgebracht en sneller willen innoveren. Met het huidige branch-onderhouds model blijven nieuwe functies en functionaliteit ontvangen. Daarom kunnen alleen klanten met een actieve Software Assurance op Configuration Manager-licenties of met gelijkwaardige abonnements rechten de huidige vertakking van Configuration Manager installeren en gebruiken.

### <a name="whats-the-long-term-servicing-branch-ltsb"></a><a name="bkmk_ltsb"></a>Wat is de Long-term Servicing Branch (LTSB)?  

De LTSB is een build van Configuration Manager die gereed is voor productie. Het is bedoeld voor klanten die toestemming hebben om Software Assurance of gelijkwaardige abonnements rechten te laten verlopen. In vergelijking met de huidige vertakking heeft de LTSB [verminderde functionaliteit](introduction-to-the-ltsb.md#features-that-arent-available). Klanten die Software Assurance of gelijkwaardige abonnements rechten toestaan om te verlopen, moeten de huidige vertakking van Configuration Manager verwijderen. Klanten die over permanente licentie rechten beschikken voor Configuration Manager, kunnen vervolgens de LTSB-build van de Configuration Manager versie installeren en gebruiken die actueel is op het moment dat ze verlopen.

### <a name="what-do-the-acronyms-sa-and-lsa-mean-in-regard-to-configuration-manager"></a><a name="bkmk_licensing-acronyms"></a>Wat betekenen de acroniemen *sa* en *L&sa* in betrekking tot Configuration Manager?

Zowel **Software Assurance** (SA) als **licentie-en Software Assurance** (L&SA) zijn licentie opties die rechten verlenen voor het gebruik van Configuration Manager. SA is een optie voor een klant die de SA-dekking van een eerdere overeenkomst verlengt. L&SA is een optie voor een klant die een nieuwe licentie en SA-dekking koopt.

- **Software Assurance (SA)**: klanten moeten actieve SA hebben op Configuration Manager licenties, of gelijkwaardige abonnements rechten, om de huidige vertakkings optie van Configuration Manager te kunnen installeren en gebruiken.

  Hoewel SA optioneel is voor sommige micro soft-producten, is de enige manier om rechten te krijgen voor het gebruik van Configuration Manager current branch is met SA *of gelijkwaardige abonnements rechten*. Zie [Veelgestelde vragen over Software Assurance](https://www.microsoft.com/licensing/licensing-programs/FAQ-Software-Assurance.aspx)voor meer informatie.

- **Micro soft-licentie en Software Assurance (L&SA)**: klanten die nieuwe licenties kopen voor Configuration Manager, moeten L&sa aanschaffen (de licentie-en sa-dekking).

  - De SA verleent rechten voor het gebruik van de huidige vertakking.

  - Als uw SA verloopt en u nog steeds een licentie voor Configuration Manager hebt, kunt u de huidige vertakking niet meer gebruiken. Meer informatie vindt u in de veelgestelde vragen [als mijn SA verloopt en ik L&sa had, wat kan ik krijgen?](#bkmk_sa-expires)

Zie voor meer informatie over licentie aanbiedingen manieren om [product voorwaarden](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64) [te kopen en te](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs) verlenen.  

### <a name="what-are-equivalent-subscriptions"></a><a name="bkmk_equiv-sub"></a>Wat zijn *gelijkwaardige abonnementen*?

Gelijkwaardige abonnementen verwijzen naar Program ma's als [Enterprise Mobility + Security](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) of [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise). Er kunnen anderen zijn, maar dit zijn de meest voorkomende Program ma's. In de micro soft Volume Licensing-product termen wordt verwezen naar deze Program ma's als equivalente licenties voor beheer licenties.

Configuration Manager is opgenomen in de volgende abonnementen:

- InTune-licentie voor gebruikers abonnementen (GEBRUIKERSABONNEMENTSLICENTIES)
- EMS E3
- EMS E5
- Microsoft 365 E3
- Microsoft 365 E5
- Microsoft 365 F3 (voorheen Microsoft 365 F1)

<!-- Sources:
https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans
https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing
-->

> [!IMPORTANT]
> Configuration Manager is niet opgenomen in het [Microsoft 365 Business](https://www.microsoft.com/microsoft-365/business) plan.

### <a name="what-changes-with-licensing-for-co-management-in-microsoft-endpoint-manager"></a><a name="bkmk_mem"></a>Wat is er veranderd in licentie voor co-beheer in micro soft Endpoint Manager?

<!-- 7202432 -->

Met de licentie voor co-beheer kunnen Configuration Manager klanten met Software Assurance intune-PC-beheer rechten ophalen zonder dat ze afzonderlijke intune-licenties hoeven te kopen en toewijzen aan gebruikers. Met deze licentie kunt u Windows-apparaten eenvoudiger beheren met micro soft Endpoint Manager.

- Apparaten die al worden beheerd door Configuration Manager die u hebt Inge schreven bij intune voor co-beheer, hebben bijna dezelfde rechten als een door intune beheerde PC. Als u Windows opnieuw instelt op dit apparaat, kunt u het niet inrichten met Windows auto pilot. Voor auto pilot is een volledige intune-licentie vereist.

- Als u een Windows 10-apparaat op een andere manier inschrijft bij intune, is er nog steeds een volledige intune-licentie vereist. U kunt bijvoorbeeld auto pilot gebruiken om een apparaat in te richten, of een gebruiker voert hand matig registratie van de self-service uit.

- Voor bestaande door Configuration Manager beheerde apparaten om in intune te worden inge schreven voor co-beheer op schaal zonder tussen komst van de gebruiker, gebruikt co-beheer een functie van Azure Active Directory (Azure AD) met de naam automatische inschrijving voor Windows 10. Automatische inschrijving met co-beheer vereist licenties voor zowel Azure AD Premium (AADP1) als intune. Vanaf 1 december 2019 hoeft u geen afzonderlijke intune-licenties meer toe te wijzen voor dit scenario. Micro soft Endpoint Manager bevat nu de intune-licenties voor co-beheer. De afzonderlijke AADP1-licentie vereisten blijven hetzelfde voor dit scenario. U moet nog steeds intune-licenties toewijzen voor andere inschrijvings scenario's.

- Als u intune wilt gebruiken voor het beheren van iOS-, Android-of macOS-apparaten, hebt u het juiste intune-abonnement nodig via een zelfstandige licentie, Enterprise Mobility + Security (EMS) of Microsoft 365.

- Als u geen abonnement op intune hebt, ter ondersteuning van co-beheer moet u ten minste één intune-licentie aanschaffen. Deze licentie is voor een beheerder om het abonnement te activeren en toegang te krijgen tot het micro soft Endpoint Manager-beheer centrum.

- Als u de Microsoft 365 ingebouwde [eenvoudige mobiliteit en beveiliging](https://support.microsoft.com/office/capabilities-of-built-in-mobile-device-management-for-microsoft-365-a1da44e5-7475-4992-be91-9ccec25905b0)gebruikt, kunt u de nieuwe licentie voor gezamenlijk beheer niet gebruiken voor een gebruiker die ook apparaten heeft die worden beheerd door de basis mobiliteit en beveiliging. Voer een van de volgende acties uit om de co-beheer licentie te gebruiken voor het door Configuration Manager beheerde apparaat van de gebruiker:

  - Wijs een volledige intune-licentie toe aan de gebruiker en beheer hun apparaten via intune.
  - De registratie van apparaten bij basis mobiliteit en beveiliging ongedaan maken.

- De licenties die u eerder had voor System Center Configuration Manager, zijn nog steeds van toepassing op micro soft endpoint Configuration Manager. Als u een nieuwe site installeert, gebruikt u bestaande product codes.

|Functie | Licentie voor co-beheer | Volledige intune-licentie |
|---------|---------|---------|
|Windows 10-inschrijving|Ja (alleen voor bestaande door ConfigMgr beheerde apparaten)|Ja|
|iOS-, Android-, macOS-inschrijving|Nee|Ja|
|Autopilot|Nee|Ja|
|Mobile Application Management (MAM)|Nee|Ja|
|Voorwaardelijke toegang<br>(aanvullende AADP1 vereist)|Ja|Ja|
|Apparaatprofielen|Ja|Ja|
|Beheer van software-updates|Ja|Ja|
|Inventaris|Ja|Ja|
|Appbeheer|Ja|Ja|
|Hulp op afstand<br>(Team Viewer-licentie vereist)|Ja|Ja|
|Desktop Analytics<br>(Windows-abonnements licenties vereist|Ja|N.v.t.|
|Tenantkoppeling|Ja|N.v.t.|
|Eindpuntanalyse|Ja|Ja|

Raadpleeg voor meer informatie de volgende artikelen:

- [Vereisten voor co-beheer](../../comanage/overview.md#prerequisites)
- [Windows auto pilot-vereisten](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)
- [Vereisten voor desktop Analytics](../../desktop-analytics/overview.md#prerequisites)
- [Vereisten voor Tenant koppelen](../../tenant-attach/device-sync-actions.md#prerequisites)
- [Licentie vereisten voor endpoint Analytics](../../../analytics/overview.md#licensing-prerequisites)
- [Voorwaardelijke toegang gebruiken met intune](../../../intune/protect/conditional-access.md#use-conditional-access-with-intune)
- [Team Viewer-vereisten](../../../intune/remote-actions/teamviewer-support.md#prerequisites)

### <a name="i-have-enterprise-mobility--security-and-it-expired-what-must-i-do-now"></a><a name="bkmk_ems-expires"></a>Ik heb Enterprise Mobility + Security en het is verlopen. Wat moet ik nu doen?  

EMS verleent rechten voor het gebruik van Configuration Manager huidige vertakking en de langlopende service vertakking. Wanneer deze rechten verlopen, hebt u geen rechten meer om een van beide vertakkingen te gebruiken en moet u de installatie ervan ongedaan maken.  

### <a name="if-my-sa-expires-and-i-had-lsa-what-do-i-get"></a><a name="bkmk_sa-expires"></a>Wat kan ik doen als mijn SA verloopt en ik L&SA had?

Als uw SA na 1 oktober 2016 is verlopen, is het mogelijk dat u een permanente licentie voor het gebruik van de LTSB kunt bewaren, afhankelijk van het programma dat u hebt&aangeschaft. Als u momenteel de huidige vertakking gebruikt, moet u deze verwijderen en vervolgens de LTSB installeren. Er is geen ondersteuning voor het migreren of converteren naar de LTSB van de huidige vertakking.

Als uw SA vóór 1 oktober 2016 is verlopen en u een permanente licentie naar Configuration Manager hebt behouden, is de optie voor het gebruik van System Center 2012 R2 Configuration Manager en de beschik bare service packs. U moet de huidige branch verwijderen als uw SA verloopt en de eerdere versie van het product opnieuw installeren. Er is geen ondersteuning voor het migreren van naar of Down graden van Configuration Manager huidige vertakking naar eerdere versies van Configuration Manager.

Als u System Center Endpoint Protection gebruikt en uw SA verloopt, moet u deze verwijderen. System Center Endpoint Protection biedt geen *L (licentie)* rechten en geen permanente rechten.<!--506238-->

### <a name="do-i-own-the-current-branch"></a><a name="bkmk_owncb"></a>Ben ik eigenaar van de huidige vertakking?

Nee. U hebt een licentie voor het gebruik van de huidige branch terwijl u actieve SA hebt. Bijvoorbeeld: via *L&sa*, wanneer *sa* verloopt, hebt u dan alleen *L (licentie)* rechten, die geen rechten hebben voor het gebruik van de huidige vertakking. Als uw L permanente rechten biedt, kunt u de Configuration Manager LTSB gebruiken in plaats van de huidige vertakking. Als uw SA vóór 1 oktober 2016 is verlopen, kunt u ook System Center 2012 R2 Configuration Manager gebruiken.

### <a name="can-i-purchase-configuration-manager-standalone-without-sa"></a><a name="bkmk_standalone"></a>Kan ik Configuration Manager zelfstandig aanschaffen zonder SA?

Nee. De enige manier om rechten te krijgen voor het gebruik van Configuration Manager is het verkrijgen van een licentie met SA of een gelijkwaardig abonnement. Er zijn ontwikkel Programma's zoals MSDN waar Configuration Manager wordt aangeboden voor ontwikkelings-en test doeleinden, maar niet voor productie gebruik.

### <a name="does-a-non-production-environment-for-testing-or-development-require-an-explicit-license"></a><a name="bkmk_lab"></a>Is er een expliciete licentie vereist voor een niet-productie omgeving voor testen of ontwikkeling?

<!-- SCCMDocs#1848 -->

- Als u dezelfde huidige branch-software gebruikt als uw productie omgeving, hebt u een expliciete licentie nodig. Neem contact op met uw account team om te bepalen of uw specifieke licentie overeenkomst betrekking heeft op meerdere exemplaren in meerdere omgevingen.

- Sommige ontwikkel Programma's zoals MSDN bieden producten als Configuration Manager voor ontwikkeling en testen, maar niet voor productie gebruik.

- Voor een tijdelijke omgeving kunt u de [evaluatie versie](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) gedurende 180 dagen gebruiken.

- Voor een test omgeving kunt u de [vertakking Technical Preview](../get-started/technical-preview.md)gebruiken. Technical Preview heeft dezelfde functionaliteit als de huidige vertakking, maar heeft een aantal beperkingen op het gebied van schaal en ondersteunde platforms.

### <a name="do-i-have-rights-to-install-any-update-in-the-configuration-manager-console"></a><a name="bkmk_update-rights"></a>Heb ik rechten om een update te installeren in de Configuration Manager-console?

Als u actieve *sa*hebt, hebt u rechten.

Als u geen actieve SA hebt, verwijdert u de huidige vertakking en installeert u vervolgens de LTSB van Configuration Manager. De LTSB ontvangt geen updates voor incrementele versies van Configuration Manager, maar ontvangt beveiligings updates op basis van de ondersteunings levenscyclus.

### <a name="i-have-purchased-ems-or-microsoft-365-through-a-cloud-solution-provider-csp-do-i-have-rights-to-use-configuration-manager"></a><a name="bkmk_csp"></a>Ik heb EMS of Microsoft 365 gekocht via een Cloud Solution Provider (CSP), ik heb dan rechten om Configuration Manager te gebruiken?

Ja, u hebt rechten om Configuration Manager te gebruiken voor het beheren van clients die onder de EMS-licentie vallen. Down load en installeer eerst de [evaluatie software](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection). Neem contact op met Microsoft Ondersteuning om de licentie sleutel te verkrijgen.<!--issue472--> Wanneer u met Microsoft Ondersteuning praat, vraagt u deze om te verwijzen naar de interne artikel-ID 4033838.<!-- SCCMDocs issue 493 -->

### <a name="is-my-subscription-end-date-the-same-as-an-sa-expiration-date"></a><a name="bkmk_expiration-date"></a>Is de eind datum van mijn abonnement hetzelfde als voor de verval datum van een SA?

Als *sa* of uw abonnement actief is, hebt u rechten voor Configuration Manager huidige vertakking. Een actief abonnement is gelijk aan actieve *sa*, maar geen permanente *L (licentie)*. Nadat uw abonnement is afgelopen, verwijdert u de huidige vertakking. U hebt op dit moment geen rechten om de LTSB te gebruiken.  

### <a name="what-are-the-use-rights-associated-with-the-sql-technology-provided-with-configuration-manager"></a><a name="bkmk_sql"></a>Wat zijn de gebruiks rechten die zijn gekoppeld aan de SQL-technologie van Configuration Manager?

Configuration Manager SQL Server technologie bevat. Met de licentie voorwaarden van micro soft voor dit product kan uw gebruik van SQL Server technologie alleen worden gebruikt voor de ondersteuning van Configuration Manager-onderdelen. SQL Server licenties voor client toegang zijn niet vereist voor dat gebruik.

Goedgekeurde gebruiks rechten voor de SQL-mogelijkheden met Configuration Manager zijn onder andere:

- Site database functie
- Windows Server Update Services (WSUS) voor de rol van software-update punt
- SQL Server Reporting Services (SSRS) voor rapportage punt rol
- Rol van data warehouse-service punt
- Database replica's voor beheer punt rollen

De SQL Server licentie die is opgenomen in Configuration Manager ondersteunt elk exemplaar van SQL Server dat u installeert voor het hosten van een Data Base voor Configuration Manager. Er kunnen echter alleen data bases voor Configuration Manager in de voor gaande lijst worden uitgevoerd op die SQL Server wanneer u deze licentie gebruikt. Als een Data Base voor een ander product van micro soft of derden de SQL Server, moet u een afzonderlijke licentie voor die SQL Server instantie hebben.
 <!-- sms500967 -->

### <a name="does-on-premises-mobile-device-management-mdm-require-an-intune-subscription"></a><a name="bkmk_opmdm"></a>Is voor een on-premises Mobile Device Management (MDM) een intune-abonnement vereist?

In versie 1806 en eerder kunt u een Microsoft Intune-abonnement hebben om te beginnen met het gebruik van on-premises MDM. Het abonnement is alleen vereist voor het bijhouden van de licentie verlening voor de apparaten en wordt niet gebruikt om beheer gegevens voor de apparaten te beheren of op te slaan. Alle beheer gegevens worden opgeslagen in uw organisatie met behulp van de on-premises Configuration Manager-infra structuur.  

Vanaf versie 1810 is een intune-verbinding niet langer vereist voor nieuwe on-premises MDM-implementaties.<!--3607730, fka 1359124--> Uw organisatie heeft nog steeds intune-licenties nodig om deze functie te gebruiken. Zie het [blog bericht intune-ondersteuning](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150)voor meer informatie.

---
title: Hulpprogramma voor migratie van firewallregels voor eindpuntbeveiliging voor Microsoft Intune - Azure | Microsoft Docs
description: Meer informatie over het gebruik van het hulpprogramma voor migratie van firewallregels voor eindpuntbeveiliging Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: mattsha
ms.openlocfilehash: 7dd6d3a01d18e4d8b334bdeee3f72eeaeed67c0a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86464983"
---
# <a name="endpoint-security-firewall-rule-migration-tool-overview"></a>Overzicht van het hulpprogramma voor migratie van firewallregels voor eindpuntbeveiliging

Veel organisaties willen hun beveiligingsconfiguratie verplaatsen naar Microsoft Endpoint Manager om gebruik te maken van modern beheer in de cloud.

Eindpuntbeveiliging in Endpoint Manager biedt een rijke beheerervaring met Windows Firewall-configuratie en gedetailleerd beheer van firewallregels.

Veel organisaties hebben al groepsbeleid voor het beheren van hun Windows Firewall regels. De overstap naar modern beheer kan lastig zijn omdat het handmatig maken van honderden firewallregels nogal tijdrovend kan zijn.

Om klanten te helpen de configuratie van hun firewallregels naar beleid voor eindpuntbeveiliging in Endpoint Manager te verplaatsen, werd het **hulpprogramma voor het migreren van firewallregels voor eindpuntbeveiliging** ontwikkeld.

Klanten kunnen het **hulpprogramma voor de migratie van firewallregels voor eindpuntbeveiliging** uitvoeren op een referentieclient/vooraf geconfigureerde Windows 10-client en automatisch beleid voor de firewallregel voor eindpuntbeveiliging maken in Endpoint Manager. Na het maken kunnen beheerders deze regels richten op Azure AD-groepen om MDM en gezamenlijk beheerde clients te configureren.

Download het [hulpprogramma voor migratie van firewallregels voor eindpuntbeveiliging](https://aka.ms/EndpointSecurityFWRuleMigrationTool):<br>
<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## <a name="tool-usage"></a>Het hulpprogramma gebruiken

Het hulpprogramma wordt uitgevoerd op een referentiecomputer en migreert de huidige configuratie van Windows Firewall-regels. Als u het hulpprogramma uitvoert, worden alle ingeschakelde firewallregels die op het apparaat aanwezig zijn geëxporteerd en wordt er automatisch nieuw Intune-beleid gemaakt met de verzamelde regels.

1. Meld u bij de referentiecomputer aan met lokale beheerdersmachtigingen.
2. Download het bestand `Export-FirewallRules.zip` en pak het uit. <br>
   Het zip-bestand bevat het scriptbestand `Export-FirewallRules.ps1`. 
3. Voer het `Export-FirewallRules.ps1`-script uit op de computer. <br>
   Met het script worden alle vereiste onderdelen gedownload die moeten worden uitgevoerd. Geef de juiste referenties voor de Intune-beheerder op als hier om wordt gevraagd. Raadpleeg [Vereiste machtigingen](#required-permissions) voor meer informatie over uw opties om vereiste machtigingen te configureren.
4. Geef een beleidsnaam op wanneer u hierom wordt gevraagd. <br>
   Dit beleid wordt in [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) weergegeven in het deelvenster **Eindpuntbeveiliging** > **Firewall**. 

    > [!IMPORTANT]
    > De beleidsnaam moet uniek zijn voor de tenant.

    Als er meer dan 150 firewallregels worden gevonden, worden er meerdere beleidsregels gemaakt.

    > [!NOTE]
    > Standaard worden alleen ingeschakelde firewallregels gemigreerd. Bovendien worden standaard alleen firewallregels gemigreerd die door GPO zijn gemaakt. Er zijn schakelopties om deze standaardwaarden te wijzigen. Zie [Schakelopties](#switches) voor meer informatie.
    >
    > Afhankelijk van het aantal gevonden firewallregels kan het enige tijd duren voordat het hulpprogramma is uitgevoerd.

5. Nadat het hulpprogramma is voltooid, genereert het hulpprogramma een telling van het aantal firewallregels dat niet automatisch kon worden gemigreerd. Zie [Niet-ondersteunde configuratie](#unsupported-configuration) voor meer informatie.

## <a name="switches"></a>Schakelopties

U kunt de volgende schakelopties (parameters) gebruiken om de standaardfunctionaliteit van het hulpprogramma te wijzigen.

- `IncludeLocalRules`: Met deze schakeloptie worden alle lokaal gemaakte/standaard Windows Firewall-regels in de export opgenomen. Houd er rekening mee dat het inschakelen van deze schakeloptie kan leiden tot veel opgenomen regels. 
- `IncludedDisabledRules`: Met deze schakeloptie worden alle ingeschakelde en uitgeschakelde Windows Firewall-regels in de export opgenomen. Houd er rekening mee dat het inschakelen van deze schakeloptie kan leiden tot veel opgenomen regels.

## <a name="unsupported-configuration"></a>Niet-ondersteunde configuratie

De volgende op het register gebaseerde instellingen worden niet ondersteund vanwege een gebrek aan MDM-ondersteuning in Windows. Deze instellingen zijn ongebruikelijk, maar als u deze instellingen nodig hebt, moet u deze behoefte kenbaar maken via uw standaard ondersteuningskanalen.

|     GPO-veld    |     Reden    |
|-|-|
|      TYPE-VALUE =/ "Security=" IFSECURE-VAL    |     IPSec-gerelateerde instelling die niet wordt ondersteund door Windows MDM    |
|      TYPE-VALUE =/ "Security2_9=" IFSECURE2-9-VAL    |     IPSec-gerelateerde instelling die niet wordt ondersteund door Windows MDM    |
|      TYPE-VALUE =/ "Security2=" IFSECURE2-10-VAL     |     IPSec-gerelateerde instelling die niet wordt ondersteund door Windows MDM    |
|      TYPE-VALUE =/ "IF=" IF-VAL    |     De interface-id (LUID) kan niet worden beheerd    |
|      TYPE-VALUE =/ "Defer=" DEFER-VAL    |     Inkomend gerelateerd NAT-verkeer dat niet beschikbaar is via groepsbeleid of Windows MDM    |
|      TYPE-VALUE =/ "LSM=" BOOL-VAL    |     Vrije brontoewijzing niet beschikbaar via groepsbeleid of Windows MDM    |
|      TYPE-VALUE =/ "Platform=" PLATFORM-VAL    |     Versies van het besturingssysteem niet beschikbaar via groepsbeleid of Windows MDM    |
|      TYPE-VALUE =/ "RMauth=" STR-VAL    |     IPSec-gerelateerde instelling die niet wordt ondersteund door Windows MDM    |
|      TYPE-VALUE =/ "RUAuth=" STR-VAL    |     IPSec-gerelateerde instelling die niet wordt ondersteund door Windows MDM    |
|      TYPE-VALUE =/ "AuthByPassOut=" BOOL-VAL    |     IPSec-gerelateerde instelling die niet wordt ondersteund door Windows MDM    |
|      TYPE-VALUE =/ "LOM=" BOOL-VAL    |     Alleen lokale toewijzing niet beschikbaar via groepsbeleid of Windows MDM    |
|      TYPE-VALUE =/ "Platform2=" PLATFORM-OP-VAL    |     Overbodige instelling niet beschikbaar via groepsbeleid of Windows MDM    |
|      TYPE-VALUE =/ "PCross=" BOOL-VAL    |     Profielkruising toestaan niet beschikbaar via groepsbeleid of Windows MDM    |
|      TYPE-VALUE =/ "LUOwn=" STR-VAL    |     Eigenaar-SID van lokale gebruiker niet van toepassing in MDM    |
|      TYPE-VALUE =/ "TTK=" TRUST-TUPLE-KEYWORD-VAL    |     Verkeer afstemmen met het trust tuple-trefwoord niet beschikbaar via groepsbeleid of Windows MDM    |
|      TYPE-VALUE =/ “TTK2_22=” TRUST-TUPLE-KEYWORD-VAL2-22    |     Verkeer afstemmen met het trust tuple-trefwoord niet beschikbaar via groepsbeleid of Windows MDM    |
|      TYPE-VALUE =/ “TTK2_27=” TRUST-TUPLE-KEYWORD-VAL2-27    |     Verkeer afstemmen met het trust tuple-trefwoord niet beschikbaar via groepsbeleid of Windows MDM    |
|      TYPE-VALUE =/ “TTK2_28=” TRUST-TUPLE-KEYWORD-VAL2-28    |     Verkeer afstemmen met het trust tuple-trefwoord niet beschikbaar via groepsbeleid of Windows MDM    |
|      TYPE-VALUE =/ "NNm=" STR-ENC-VAL    |     IPSec-gerelateerde instelling die niet wordt ondersteund door Windows MDM    |
|      TYPE-VALUE =/ "SecurityRealmId=" STR-VAL    |     IPSec-gerelateerde instelling die niet wordt ondersteund door Windows MDM    |

## <a name="unsupported-setting-values"></a>Niet-ondersteunde instellingswaarden
De volgende instellingswaarden worden niet ondersteund voor migratie:

**Poorten**
- `PlayToDiscovery` wordt niet ondersteund als een bereik van lokale of externe poorten.

**Adresbereiken**
- `LocalSubnet6` wordt niet ondersteund als een bereik van lokale of externe adressen. 
- `LocalSubnet4` wordt niet ondersteund als een bereik van lokale of externe adressen.
- `PlatToDevice` wordt niet ondersteund als een bereik van lokale of externe adressen.

Zodra het hulpprogramma is uitgevoerd, wordt er een rapport gegenereerd met regels die niet zijn gemigreerd. U kunt deze regels weergeven door `RulesError.csv` te bekijken die in `C:\<folder needed>`zijn gevonden. 

## <a name="required-permissions"></a>Vereiste machtigingen
Endpoint Security Manager-gebruikers, Intune-servicebeheerders of globale beheerder kunnen Windows Firewall-regels migreren naar beleidsregels voor eindpuntbeveiliging. U kunt ook een aangepaste rol gebruiken waarbij machtigingen voor beveiligingsbasislijnen zijn ingesteld waarop machtigingen voor **Verwijderen**, **Lezen**, **Toewijzen**, **Maken** en **Bijwerken** zijn toegepast. Zie [Beheerdersmachtigingen verlenen aan Intune](../fundamentals/users-add.md#grant-admin-permissions) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

- Wijs de regels toe aan Azure AD-groepen om MDM en gezamenlijk beheerde clients te configureren. Zie [Groepen toevoegen om gebruikers en apparaten te organiseren](../fundamentals/groups-add.md) voor meer informatie.

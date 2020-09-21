---
title: Tenant gekoppelde gegevens verzameling
titleSuffix: Configuration Manager
description: Meer informatie over de diagnostische gegevens die worden Configuration Manager verzameld voor functies voor het koppelen van tenants.
ms.date: 09/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 4b305a71-9ad8-4332-9692-d51554158981
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00a01e4ceadc716a42381999b2e4603bcbe55524
ms.sourcegitcommit: eaa077aa028a76a4873e4aa7437888f901a7e77f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/18/2020
ms.locfileid: "90767799"
---
# <a name="tenant-attach-data-collection"></a>Tenant gekoppelde gegevens verzameling

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!-- 6505626 -->
Wanneer u uw Configuration Manager-site koppelt aan een Microsoft Intune-Tenant, stuurt de site aanvullende gegevens naar micro soft. Dit artikel bevat een overzicht van de gegevens die worden verzonden.

Met Tenant koppeling wordt de micro soft Endpoint Manager-beheer centrum uw console in de Cloud. Met de architectuur kan de Configuration Manager-site gegevens over het apparaat en de gebruiker synchroniseren met uw intune-Tenant. U kunt vervolgens in realtime gegevens opvragen en presen teren vanuit uw on-premises omgeving in de Cloud console zonder actieve synchronisatie. Het kan grote vluchtige gegevens ophalen van uw on-premises site. Bij Tenant koppeling wordt gebruikgemaakt van een combi natie van deze methoden om een efficiënte up-to-date informatie te bieden in de Cloud console.

> [!IMPORTANT]
> Het beleid voor gegevens verwerking van micro soft wordt beschreven in de [privacyverklaring van Microsoft intune](/legal/intune/microsoft-intune-privacy-statement). We gebruiken alleen uw klant gegevens om u de services te bieden die u hebt geregistreerd voor.
>
> We verkopen geen gegevens die door onze service worden verzameld om enigerlei reden.
>
> De gegevens zijn alle vereiste service gegevens die nodig zijn voor het koppelen van gekoppelde tenants. De vereiste service gegevens bevatten de volgende informatie:
>
> - **Inhoud**van de klant, die inhoud bevat die u maakt. Bijvoorbeeld de naam van uw LOB-toepassing.
> - **Functionele gegevens**, waaronder informatie die nodig is voor een verbonden ervaring om de taak uit te voeren. Bijvoorbeeld configuratie-informatie over de app.
> - **Diagnostische gegevens**van de service: de gegevens die nodig zijn om de service veilig, up-to-date te houden en op de verwachte manier uit te voeren. Omdat deze gegevens strikt zijn gerelateerd aan de verbonden ervaring, zijn ze gescheiden van de vereiste of optionele diagnostische gegevens niveaus.

Micro soft Endpoint Manager verzamelt informatie die in drie categorieën valt:

- **Geïdentificeerde gegevens**: de meeste gegevens die door micro soft Endpoint Manager worden verzameld, worden geïdentificeerd als gegevens. Deze gegevens zijn gekoppeld aan een gebruiker, apparaat of toepassing en zijn essentieel voor de aard van het beheer. Geïdentificeerde gegevens worden gebruikt voor het beheren van het apparaat en de toepassingen van een gebruiker.

- **Pseudoniemde gegevens**: deze gegevens zijn gekoppeld aan een unieke id. Het is doorgaans een getal dat wordt gegenereerd door het systeem en dat zelf geen individuele persoon kan identificeren. Micro soft Endpoint Manager gebruikt deze gegevens voor het leveren van de Enter prise-service.

- **Cumulatieve gegevens**: deze gegevens zijn gebruiks statistieken, zoals het aantal apparaten of de besturings elementen die u gebruikt in het micro soft Endpoint Manager-beheer centrum.

De volgende secties bevatten voor beelden van de typen gegevens die door tenants worden gesynchroniseerd met de Cloud. Ze worden gegroepeerd op functionele entiteit, zodat u kunt controleren of er specifieke functies zijn die u gebruikt.

## <a name="applications"></a>Toepassingen
<!-- 6502080 -->

Voor elk Windows Installer-implementatie type (MSI):

- **ProductName**: de naam van de toepassing
- **Uitgever**: de entiteit die de software heeft gepubliceerd
- **Versie**: de versie van de toepassing
- **ProductLanguage**: de taal code voor de toepassing
- **ProgramID**: een id voor het implementatie type

## <a name="device-sync"></a>Synchronisatie van apparaat
<!-- 6505639 -->

Voor elk apparaat:

- **SMSID**: de unieke id van uw Configuration Manager-hiërarchie
- **AADTenantID**: de unieke id van uw Azure Active Directory-Tenant (Azure AD)
- **AADDeviceID**: de unieke id van het apparaat in azure AD
- **Naam**: de hostnaam van het apparaat
- **DeviceOS**: de naam van het besturings systeem van het apparaat. Bijvoorbeeld: `Microsoft Windows NT Server 6.3`
- **DeviceOSBuild**: de build-versie van het besturings systeem van het apparaat. Bijvoorbeeld: `10.0.19041`
- **AADPrimaryUserID**: de unieke id van de primaire gebruiker van het apparaat in azure AD
- **Model**: het model van het apparaat
- **Fabrikant**: de fabrikant van het apparaat
- **Serialnumber**: het serie nummer van het apparaat
- **Domein**namen: elke domein naam voor het apparaat
- **SKU**

## <a name="windows-defender-advanced-threat-protection-atp"></a>Windows Defender Advanced Threat Protection (ATP)
<!-- 6505652 -->

Voor elke verzameling die u selecteert voor de implementatie van het ATP-beleid:

- **CollectionId**: de unieke id van de verzameling. Bijvoorbeeld: `ABC00014`
- **Verzamelingsset**: de naam van de verzameling. Bijvoorbeeld: `All Windows servers`
- **Collection**type: geeft aan of het een apparaat-of gebruikers verzameling is.
- **CountTargeted**: het aantal apparaten dat u met dit beleid richt
- **CountCompliant**: het aantal apparaten dat compatibel is met dit beleid
- **CountNonCompliant**: het aantal apparaten dat niet compatibel is met dit beleid
- **CountFailed**: het aantal apparaten dat dit beleid niet kan verwerken
- **CountActivated**
- **CountEnforced**

## <a name="see-also"></a>Zie ook

Voor meer algemene informatie over de gegevens die Configuration Manager verzamelt, raadpleegt u [Diagnostische en gebruiks gegevens voor Configuration Manager](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

Raadpleeg de volgende artikelen voor meer informatie over verwante privacy-aspecten:

- [Privacyverklaring van Microsoft Intune](/legal/intune/microsoft-intune-privacy-statement)
- [Naleving van Windows 10 en privacy](/windows/privacy/windows-10-and-privacy-compliance)
- [Licentie voorwaarden en documentatie](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Beveiliging en privacy op Microsoft Azure data centers](https://azure.microsoft.com/global-infrastructure/)  
- [Vertrouwen in de vertrouwde Cloud](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Vertrouwenscentrum](https://www.microsoft.com/trustcenter)  

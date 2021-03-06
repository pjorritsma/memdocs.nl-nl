---
title: Wat is er nieuw in Desktop Analytics
titleSuffix: Configuration Manager
description: Een samen vatting van de nieuwe functies in de meest recente maandelijkse versie van de Desktop Analytics-Cloud service.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: dd188b80375861cd08784d0574e737bfce7f2d92
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993143"
---
# <a name="whats-new-in-desktop-analytics"></a>Wat is er nieuw in Desktop Analytics

Meer informatie over wat er elke maand nieuw is in Desktop Analytics.

> [!TIP]
> Het kan tot drie dagen duren voordat elke maandelijkse update is geïmplementeerd. Sommige functies worden gedurende een aantal weken geïmplementeerd en zijn mogelijk niet voor alle gebruikers in de eerste week beschikbaar.

Als u een melding wilt ontvangen wanneer deze pagina wordt bijgewerkt, kopieert en plakt u de volgende URL in uw RSS feed-lezer: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="august-2020"></a>Augustus 2020

### <a name="apps-deployed-from-configuration-manager-are-important-by-default"></a>Apps die zijn geïmplementeerd vanuit Configuration Manager zijn standaard belang rijk

<!-- 4859763 -->

De **urgentie** configuratie van een app is essentieel voor desktop Analytics om te bepalen welke apparaten moeten worden toegevoegd voor test implementaties. Een beheerder heeft nodig om het belang voor alle apps in Desktop Analytics hand matig te configureren. Alleen wanneer u de test valideert, kunt u door gaan met een productie-implementatie.

Voor elke app die u met Configuration Manager implementeert, wordt deze door Desktop Analytics standaard automatisch geconfigureerd als belang rijk. Met dit gedrag kunt u de apps in uw omgeving sneller configureren, zodat u sneller kunt werken in een productie-implementatie.

Zie [assets-apps](about-assets.md#apps)voor meer informatie.

<!-- 6049643 -->

### <a name="improved-processing-of-diagnostic-data-during-snapshot-generation"></a>Verbeterde verwerking van diagnostische gegevens tijdens het genereren van moment opnamen

Micro soft is verbeterd hoe ze Windows diagnostische gegevens verzamelen en verwerken op basis van apparaten die zijn Inge schreven in Desktop Analytics. Deze verbeteringen verg Roten de betrouw baarheid van het dagelijks genereren van de moment opname en bereidt nieuwe functies in ontwikkeling voor. Als gevolg van dit werk heeft micro soft tijdelijk het aantal **apparaten dat deze app heeft gestart in de afgelopen 30 dagen in de** implementatie plannen uitgeschakeld. Zie [assets-apps](about-assets.md#usage)voor meer informatie.

## <a name="july-2020"></a>Juli 2020

### <a name="windows-10-version-2004-now-available-in-desktop-analytics"></a>Windows 10, versie 2004, nu beschikbaar in Desktop Analytics

<!-- 7370207 -->

Wanneer u de updates voor beveiliging en onderdelen bewaken in de portal van de Desktop Analytics, ziet u nu Windows 10, versie 2004. Wanneer u een implementatie plan maakt, kunt u Windows 10, versie 2004, als doel versie selecteren.

### <a name="improved-support-for-viewing-the-portal-from-any-device"></a>Verbeterde ondersteuning voor het weer geven van de portal vanaf elk apparaat

<!-- 6270240 -->

U kunt nu de bureau blad Analytics-Portal in het micro soft Endpoint Manager-beheer centrum bekijken vanuit diverse typen apparaten. Het voldoet nu aan de richt lijnen voor toegankelijkheid van webinhoud (WCAG) 2,1 voor een weergave resolutie van minder dan 320 x 256 pixels. De volgende afbeelding is bijvoorbeeld van de portal van een Apple iPhone 8:

:::image type="content" source="media/dashboard-iphone8.png" alt-text="Desktop Analytics-Portal op een iPhone 8":::

### <a name="notifications-for-service-impacting-events"></a>Meldingen voor gebeurtenissen die betrekking hebben op de service

<!-- 4982509 -->

De Desktop Analytics-Portal kan nu meldings banners weer geven. Met deze meldingen kan micro soft met u communiceren over belang rijke gebeurtenissen en problemen. Bijvoorbeeld bekende problemen met de service, gegevens latentie of nieuwe vereisten. Zie [service meldingen](troubleshooting.md#service-notifications)voor meer informatie.

## <a name="june-2020"></a>Juni 2020

### <a name="improvement-to-prerequisites"></a>Verbetering van vereisten

Voor desktop Analytics is het niet meer vereist dat u een Microsoft 365-service implementeert in uw Azure Active Directory Azure AD-Tenant. De **Office 365-client beheer** -app in azure AD is nu de app **Desktop Analytics** om Configuration Manager het ophalen van gegevens en de status van de service mogelijk te maken.

## <a name="may-2020"></a>Mei 2020

### <a name="reduce-the-number-of-apps-for-review"></a>Verminder het aantal apps voor beoordeling

<!-- 5542186 -->

Voor het consolideren en verminderen van het aantal apps dat wordt weer gegeven op de pagina assets in de portal, worden nu alle versies van apps met dezelfde naam en uitgever gecombineerd. Het aantal apps in de tegel ' **interessant ' apps** ' weerspiegelt deze instelling. In plaats van honderden exemplaren van micro soft Edge te vermelden, is er bijvoorbeeld één exemplaar voor alle versies. U kunt beslissingen voor alle versies eenmaal maken. Als u beslissingen moet nemen over specifieke versies van een app, kunt u dit gedrag configureren.

Zie [about assets-apps (](about-assets.md#apps)Engelstalig) voor meer informatie.

## <a name="march-2020"></a>Maart 2020

### <a name="support-for-multiple-hierarchies"></a>Ondersteuning voor meerdere hiërarchieën

<!-- 4814075, 6079184 -->

U kunt nu meerdere Configuration Manager-hiërarchieën verbinden met één Azure Active Directory Tenant met één commerciële ID voor desktop Analytics. De portal categoriseert apparaten uit verschillende hiërarchieën en verbetert de ervaring voor wereld wijde Pilots en implementatie plannen.

- Wanneer u uw wereld wijde pilot configureert en er verzamelingen worden opgenomen die meer dan 20% van uw totale geregistreerde apparaten bevatten, wordt er een waarschuwing weer gegeven in de portal.
- Wanneer u een implementatie plan maakt en verzamelingen voor meerdere hiërarchieën selecteert, wordt er een waarschuwing weer gegeven in de portal.

> [!NOTE]
> Ondersteuning voor meerdere hiërarchieën vereist Configuration Manager versie 1910 of hoger.

Raadpleeg voor meer informatie de volgende artikelen:

- [Wereld wijde pilot](deploy-pilot.md#bkmk_GlobalPilot)
- [Implementatie plannen maken](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>Compatibiliteits beveiligingen bepalen

<!-- 5746559 -->

Windows-compatibiliteits gegevens classificeert enkele apps en stuur Programma's met een *beveiliging*, waardoor de update naar Windows 10 kan mislukken of worden teruggedraaid. Desktop Analytics kan u nu helpen om deze beveiligings maatregelen vooraf te identificeren, zodat u de Asset kunt herstellen voordat u de update implementeert. Zie [compatibiliteits beoordeling-beveiligingen](compat-assessment.md#safeguards)voor meer informatie.

## <a name="january-2020"></a>Januari 2020

### <a name="additional-app-usage-detail"></a>Meer details over het app-gebruik

<!-- 5533890 -->

Wanneer u een app selecteert om meer informatie weer te geven, bevat het deel venster Details nu aanvullende informatie over het gebruik. U kunt deze gegevens gebruiken om inzicht te krijgen in de mate van installatie voor een app en op apparaten waarop gebruikers de app regel matig gebruiken. Zie [over assets-app-gebruik](about-assets.md#usage)voor meer informatie.

### <a name="provide-feedback-on-desktop-analytics"></a>Feedback geven over desktop Analytics

<!-- 5451636 -->

Als u uw feedback over desktop Analytics wilt delen, selecteert u het pictogram **een glim lach verzenden** bovenaan de portal aan de rechter kant. Zie voor meer informatie [product feedback delen](get-support.md#bkmk_feedback).

## <a name="october-2019"></a>Oktober 2019

### <a name="improvements-to-compatibility-recommendations"></a>Verbeteringen in aanbevelingen voor compatibiliteit

<!-- 3594545 -->

Desktop Analytics biedt nu aanvullende details wanneer wordt gedetecteerd dat de Windows-upgrade een toepassing of stuur programma volledig of gedeeltelijk verwijdert. Zie [Compatibility Assessment](compat-assessment.md#asset-is-removed-during-upgrade)(Engelstalig) voor meer informatie.

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>Migreren van Windows Analytics naar een bestaande Tenant

<!-- 5202803 -->

U kunt nu invoer van een bestaande Windows Analytics-werk ruimte migreren na onboarding naar Desktop Analytics.

## <a name="september-2019"></a>September 2019

### <a name="migrate-inputs-from-windows-analytics"></a>Invoer van Windows Analytics migreren

<!-- 4252663 -->

Tijdens het voorbereiden kunt u nu invoer van een bestaande Windows Analytics-werk ruimte migreren.

### <a name="offboard-from-desktop-analytics"></a>Niet meer vrijgeven uit Desktop Analytics

<!-- 4972396 -->

Als u Desktop Analytics in uw omgeving instelt, maar u de service niet meer wilt gebruiken, kunt u uw account nu sluiten. Als u van gedachten verandert in 90 dagen, kunt u het account opnieuw activeren. Zie [uw account sluiten](account-close.md)voor meer informatie.

## <a name="august-2019"></a>augustus 2019

### <a name="reset-your-account"></a>Uw account opnieuw instellen

<!-- 3733897 -->

Als u Desktop Analytics in uw omgeving instelt, maar u opnieuw wilt beginnen met voorbereiden en inschrijven, kunt u dit nu opnieuw instellen. Zie [uw account opnieuw instellen](account-reset.md)voor meer informatie over het proces.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>Beslissing over automatische upgrade van systeem-en Store-apps

<!-- 3587232 -->

Bepaalde typen apps worden automatisch gemarkeerd als *niet belang rijk*om u te helpen uw inspanningen te verminderen bij het aanwijzen van interessante apps. De beslissing over de upgrade van het implementatie plan voor deze apps wordt ook gemarkeerd als *gereed*. De volgende apps zijn compatibel en blijven werken na het upgraden van Windows:

- Systeem-apps en-onderdelen die zijn gepubliceerd door micro soft

- Apps die worden beheerd en bijgewerkt via de Microsoft Store

Zie voor meer informatie het [automatisch upgraden van de systeem-en Store-apps](about-assets.md#bkmk_plan-autoapp).

## <a name="whats-new-in-configuration-manager"></a>Wat is er nieuw in Configuration Manager

De documentatie voor desktop Analytics heeft altijd betrekking op de functionaliteit van de nieuwste versie van Configuration Manager current branch. Raadpleeg de volgende artikelen voor meer informatie over de meest recente wijzigingen in Configuration Manager:

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [Wat is er nieuw in versie 1906](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>Verouderde functies:

Wanneer micro soft een belang rijke functie van de Desktop Analytics-service wil verwijderen, wordt die wijziging vooraf aangekondigd als Configuration Manager afgeschafte functie. Zie [afgeschafte functies](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)voor meer informatie.

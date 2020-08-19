---
title: Apps toevoegen aan Microsoft Intune
titleSuffix: ''
description: Ontdek hoe u apps toevoegt aan Microsoft Intune zodat u ook apps kunt toewijzen aan gebruikers en apparaten. Intune biedt ondersteuning voor een breed scala aan app-typen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/12/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1ded457-0ecf-4f9c-a2d2-857d57f8d30a
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ccbd923ba1110f99c57b499115a41a03ec3317c1
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252806"
---
# <a name="add-apps-to-microsoft-intune"></a>Apps toevoegen aan Microsoft Intune 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Voordat u apps kunt configureren, toewijzen, beveiligen of bewaken moet u deze aan Microsoft Intune toevoegen.

De gebruikers van apps en apparaten in uw bedrijf (het personeel) hebben mogelijk verschillende vereisten voor apps. Voordat u apps toevoegt aan Intune en u deze beschikbaar maakt voor uw personeel, vindt u het misschien nuttig om enkele app-grondbeginselen te beoordelen en te doorgronden. Er zijn verschillende typen apps beschikbaar voor Intune. U moet de app-vereisten bepalen die nodig zijn voor de gebruikers in uw bedrijf, zoals de platforms en mogelijkheden die uw personeel nodig heeft. U moet bepalen of u Intune gebruikt voor het beheren van de apparaten (en de apps), of dat u Intune de apps laat beheren zonder dat de apparaten worden beheerd. Ook moet u bepalen welke apps en mogelijkheden uw personeel nodig heeft en welke medewerkers deze nodig hebben. De informatie in dit artikel helpt u op weg.

## <a name="app-types-in-microsoft-intune"></a>App-typen in Microsoft Intune

Intune biedt ondersteuning voor een breed scala aan app-typen. De beschikbare opties verschillen per app-type. Met Intune kunt u de volgende app-typen toevoegen en toewijzen:

| App-typen | Installatie | Updates |
|---|---|---|
| Apps uit de Store (Store-apps) | De app wordt door Intune op het apparaat geïnstalleerd.  | App-updates worden automatisch uitgevoerd. |
| Apps die intern zijn ontwikkeld (line-of-business) | De app wordt door Intune op het apparaat geïnstalleerd (u levert het installatiebestand). | U moet de app bijwerken. |
| Apps die zijn ingebouwd (ingebouwde apps) | De app wordt door Intune op het apparaat geïnstalleerd.  | App-updates worden automatisch uitgevoerd. |
| Apps op internet (webkoppeling) | Er wordt door Intune een snelkoppeling gemaakt naar de web-app op het beginscherm van het apparaat. | App-updates worden automatisch uitgevoerd. |
| Apps van andere Microsoft-services  | Intune maakt een snelkoppeling naar de app in de bedrijfsportal. Zie [App source setting options](../apps/company-portal-app.md#app-source-setting-options) (Opties voor app-broninstellingen) voor meer informatie. | App-updates worden automatisch uitgevoerd. |

### <a name="specific-app-type-details"></a>Details specifieke app-typen
 
De volgende tabel bevat de specifieke app-typen en informatie over hoe u deze kunt toevoegen via het deelvenster **App toevoegen** in Intune:

| **App-specifiek type** | **Algemeen type** | **App-specifieke procedures** |
| --- | --- | --- |
| Android Store-apps  | Store-app  | Selecteer **Android** als het **app-type** en voer de Google Play Store-URL in voor de app. |
| Android Enterprise-apps  | Store-app  | Selecteer **Android** als het **app-type** en voer de beheerde Google Play Store-URL in voor de app. <sup>1</sup> |
| iOS/iPadOS Store-app  | Store-app  | Selecteer **iOS** als het **app-type**, zoek de app en selecteer de app in Intune. |
| Microsoft Store-apps  | Store-app  | Selecteer **Windows** als het **app-type** en voer de URL van de Microsoft Store in voor de app. |
| Beheerde Google Play-apps | Store-app  | Selecteer **Beheerde Google Play** als het **apptype**, zoek de app en selecteer de app in Intune. |
| Office 365-apps voor Windows 10  | Store-app (Office 365) | Selecteer **Windows 10** bij **Microsoft 365-apps** als het **app-type**, en selecteer vervolgens de Office 365-app die u wilt installeren.  |
| Office 365-apps voor macOS | Store-app (Office 365) | Selecteer **macOS** bij **Microsoft 365-apps** als het **app-type** en selecteer vervolgens de Office 365-app-suite. |
| Microsoft Edge versie 77 en hoger voor Windows 10 | Store-app | Selecteer **Windows 10** bij **Microsoft Edge versie 77 en hoger** als het **app-type**. |
| Microsoft Edge versie 77 en hoger voor macOS | Store-app | Selecteer **macOS** bij **Microsoft Edge versie 77 en hoger** als het **app-type**. |
| Android LOB-apps (Line-Of-Business) | LOB-app | Selecteer **Line-Of-Business**-app als het **app-type**, selecteer het **app-pakketbestand** en voeg vervolgens een Android-installatiebestand toe met de extensie **.apk**.  |
| iOS/iPadOS LOB-apps | LOB-app | Selecteer **Line-Of-Business**-app als het **app-type**, selecteer het **app-pakketbestand** en voeg vervolgens een iOS-/iPadOS-installatiebestand toe met de extensie **.ipa**.  |
| Windows LOB-app | LOB-app | Selecteer **Line-Of-Business**-app als het app-type, selecteer het **app-pakketbestand** en voeg vervolgens een Windows-installatiebestand toe met de extensie **.msi**, **.appx**, **.appxbundle**, **.msix** of **.msixbundle**. |
| Ingebouwde iOS-/iPadOS-app  | Ingebouwde app | Selecteer **Ingebouwde app** als het **app-type** en selecteer vervolgens de ingebouwde app in de lijst beschikbare apps.  |
| Ingebouwde Android-app  | Ingebouwde app | Selecteer **Ingebouwde app** als het **app-type** en selecteer vervolgens de ingebouwde app in de lijst beschikbare apps.  |
| Web-apps  | Web-app  | Selecteer **Webkoppeling** als het **app-type** en voer vervolgens een geldige URL in die verwijst naar de web-app.  |
| Android Enterprise-systeem-apps  | Store-app  | Selecteer **Android Enterprise-systeem-app** als het **app-type** en voer vervolgens de naam, de uitgever en het pakketbestand van de app in.  |
| Windows-app (Win32)  | LOB-app  | Selecteer **Windows-app (Win32)** als het **app-type**, selecteer het **app-pakketbestand** en voeg vervolgens een installatiebestand toe met de extensie **.intunewin**.  |
| macOS LOB-apps | LOB-app  | Selecteer **Line-of-business** als het **app-type**, selecteer het **App-pakketbestand** en selecteer vervolgens een installatiebestand met de extensie **.intunemac**.  |

<sup>1</sup> Zie [Informatie over apps met licentie](apps-add.md#understanding-licensed-apps) verderop voor meer informatie over Android Enterprise- en Android-werkprofielen.

U kunt in Microsoft Intune een app toevoegen door **Apps** > **Alle apps** > **Toevoegen** te selecteren. Het deelvenster **Een app-type selecteren** wordt weergegeven. Hier kunt u het **app-type** selecteren. 

>[!TIP]
> Een LOB-app is een app die u vanaf een app-installatiebestand toevoegt. Als u bijvoorbeeld een LOB-app voor iOS/iPadOS wilt installeren, voegt u de app toe door in het deelvenster **Een app-type selecteren** de optie **LOB-app** als het **app-type** te kiezen. U selecteert vervolgens het app-pakketbestand (met de extensie .ipa). Deze app-typen worden doorgaans intern ontwikkeld.

## <a name="assess-app-requirements"></a>De app-vereisten beoordelen
Als IT-beheerder moet u niet alleen vaststellen welke apps door de groep moeten worden gebruikt, maar moet u ook bepalen over welke functies elke groep en subgroep moet beschikken. U bepaalt voor elke app welke platformen er moeten worden gebruikt, welke gebruikersgroepen de app nodig hebben, welk configuratiebeleid van toepassing is voor die groepen en welk beveiligingsbeleid moet worden toegepast.  

Daarnaast moet u bepalen of u zich richt op Mobile Device Management (MDM) of alleen op Mobile Application Management (MAM). 

Intune gebruiken om het apparaat met MDM te beheren, is handig wanneer:
- Gebruikers over een wifi- of VPN-bedrijfsconnectiviteitsprofiel moeten beschikken om te kunnen werken.
- Er voor de gebruikers een aantal apps naar hun apparaat moet worden gepusht.
- Uw organisatie moet voldoen aan de regelgeving of andere beleidsregels ten aanzien van specifieke MDM-beheerelementen, zoals de beveiliging of versleuteling.

Intune gebruiken om apps te beheren met MAM zonder het apparaat te beheren, is handig wanneer:
- U wilt toestaan dat gebruikers hun eigen apparaat gebruiken (BYOD).
- U de gebruikers eenmalig via een pop-upbericht wilt laten weten dat MAM-beveiliging van kracht is, in plaats van continu meldingen op apparaatniveau te verzenden.
- U wilt voldoen aan beleidsregels waarvoor minder beheerfuncties op persoonlijke apparaten nodig zijn. U wilt bijvoorbeeld de bedrijfsgegevens voor de apps beheren en niet de bedrijfsgegevens voor het hele apparaat.

Raadpleeg [MDM en MAM vergelijken](../fundamentals/byod-technology-decisions.md) voor meer informatie.

### <a name="determine-who-will-use-the-app"></a>Bepalen wie de app gaat gebruiken

Houd rekening met de verschillende groepen gebruikers en apps die zij gebruiken wanneer u bepaalt welke apps uw personeel nodig heeft. Als u weet welke verschillende groepen er zijn, komt dat ook van pas na het toevoegen van een app. Nadat u een app toevoegt, wijst u een groep gebruikers toe die de app mag gebruiken. 

U moet eerst op basis van de vertrouwelijkheid van de gegevens in de app bepalen welke groep toegang mag krijgen tot de app. U moet mogelijk bepaalde soorten rollen binnen uw organisatie opnemen of uitsluiten. Het verkoopteam heeft misschien alleen bepaalde LOB-apps nodig, terwijl medewerkers die zich bezighouden met engineering, financiën, HR of juridische aangelegenheden mogelijk geen LOB-apps gebruiken. Daarnaast is er voor het verkoopteam mogelijk aanvullende gegevensbeveiliging nodig en moet het team op hun mobiele apparaten toegang hebben tot interne bedrijfsservices. U moet bepalen hoe deze groep met de app verbinding maakt met de resources. Worden de gegevens die worden opgehaald met de app in de cloud of op een on-premises server opgeslagen? En hoe maken de gebruikers met de app verbinding met de resources? 

Intune biedt ook ondersteuning voor het inschakelen van beveiligde toegang tot client-apps die worden gebruikt om on-premises gegevens te openen, zoals een line-of-business-app-server. Doorgaans geeft u dit soort toegang met behulp van [door Intune beheerde certificaten](../protect/certificates-configure.md) voor toegangsbeheer in combinatie met een standaard VPN-gateway of proxy in het perimeternetwerk, zoals de Azure Active Directory-toepassingsproxy. U kunt met de [App Wrapping Tool en App SDK](../developer/apps-prepare-mobile-application-management.md) van Intune de opgehaalde gegevens binnen de LOB-app houden, zodat de bedrijfsgegevens niet worden doorgegeven aan consumenten-apps of -services.

In de [Intune-handleiding voor implementatieplanning, ontwerp en implementatie](../fundamentals/planning-guide.md) kunt u lezen hoe u bepaalt welke organisatiegroepen gekoppeld zijn aan elk gebruiksscenario en ondergeschikt gebruiksscenario voor apps. Raadpleeg [Apps aan groepen toewijzen met Microsoft Intune](apps-deploy.md) voor meer informatie over het toewijzen van apps aan groepen.

### <a name="determine-the-type-of-app-for-your-solution"></a>Het type app voor uw oplossing bepalen

U kunt kiezen uit de volgende app-typen:
- **Apps uit de store**: een app die naar de Microsoft Store, iOS/iPadOS Store of Android Store is geüpload, is een store-app. De aanbieder van een store-app onderhoudt de app en levert hiervoor updates. U selecteert de app in de lijst van de store en voegt deze met behulp van Intune toe als een beschikbare app voor uw gebruikers.
- **Apps die intern zijn ontwikkeld (line-of-business)** : apps die intern zijn gemaakt, worden LOB-apps (line-of-business) genoemd. De functionaliteit van dit type app is gemaakt voor een van de platformen die door Intune worden ondersteund, zoals Windows, iOS/iPadOS, macOS of Android. Uw organisatie maakt en levert u updates als een afzonderlijk bestand. U levert updates van de app aan gebruikers door de updates via Intune toe te voegen en te implementeren.
- **Apps op internet**: web-apps zijn client-/servertoepassingen. De server levert de web-app, waaronder de gebruikersinterface, inhoud en functionaliteit. Bovendien bieden moderne webhostingplatformen meestal beveiliging, taakverdeling en andere voordelen. Dit type app wordt afzonderlijk onderhouden op internet. U gebruikt Intune om naar dit type app te verwijzen. U wijst ook de groepen gebruikers toe die toegang krijgen tot de app. Houd er rekening mee dat Android geen ondersteuning biedt voor web-apps.
- **Apps van andere Microsoft-services**: Apps die ofwel uit Azure AD ofwel uit Office Online afkomstig zijn. **Azure AD-ondernemingstoepassingen** worden geregistreerd en toegewezen via de [Azure-portal](https://portal.azure.com). **Office Online-toepassingen** worden toegewezen met behulp van de licentiecontroles die beschikbaar zijn in het [M365-beheercentrum](https://admin.microsoft.com). In de bedrijfsportal kunt u Azure AD Enterprise- en Office Online-apps verbergen voor of tonen aan eindgebruikers. U vindt deze configuratie-instelling door in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) **Tenantbeheer** > **Aanpassing** te selecteren. Selecteer **Verbergen** of **Weergeven** om **Azure AD-ondernemingstoepassingen** of **Office Online-toepassingen** in de bedrijfsportal te verbergen voor of tonen aan alle gebruikers. Elke eindgebruiker ziet de volledige toepassingscatalogus van de gekozen Microsoft-service. Standaard wordt elke extra app-bron ingesteld op **Verbergen**. Zie [App source setting options](../apps/company-portal-app.md#app-source-setting-options) (Opties voor app-broninstellingen) voor meer informatie. 

Wanneer u bepaalt welke apps uw organisatie nodig heeft, houd er dan rekening mee hoe de apps worden geïntegreerd met cloudservices, welke gegevens worden opgehaald met de apps, of de apps beschikbaar zijn voor BYOD-gebruikers en of internettoegang nodig is voor de apps.

Raadpleeg de sectie 'Apps' binnen de sectie 'Functievereisten' in [Een ontwerp maken](../fundamentals/planning-guide-design.md#feature-requirements) voor meer informatie over de app-typen die uw organisatie nodig heeft.

### <a name="understanding-app-management-and-protection-policies"></a>Informatie over app-beheer en beveiligingsbeleid
U kunt in Intune de functionaliteit wijzigen van apps die u implementeert, zodat deze in overeenstemming zijn met het nalevings- en beveiligingsbeleid van uw bedrijf. Met dit beheer kunt u bepalen hoe de bedrijfsgegevens worden beveiligd. Door Intune beheerde apps worden ingeschakeld met een uitgebreide reeks van beveiligingsbeleidsregels voor mobiele toepassingen, zoals:

- De beperking van functies voor kopiëren en plakken en opslaan als.
- Webkoppelingen zo configureren dat deze in de Microsoft Edge-app worden geopend.
- De inschakeling van het gebruik van meerdere identiteiten en voorwaardelijke toegang op app-niveau.

Voor apps die door Intune worden beheerd, kan ook app-beveiliging worden ingeschakeld zonder dat een apparaat hoeft te worden ingeschreven. U kunt op die manier beleid voor de preventie van gegevensverlies toepassen zonder dat u het apparaat van de gebruiker hoeft te beheren. Daarnaast kunt u het beheer van mobiele apps in uw mobiele apps en LOB-apps opnemen via de Intune App SDK en de App Wrapping Tool. Raadpleeg [Overzicht van de Intune App SDK](../developer/app-sdk.md) voor meer informatie over deze hulpprogramma's.

### <a name="understanding-licensed-apps"></a>Informatie over apps met licentie
Naast het feit dat er verschillende typen apps zijn, zoals web-apps, store-apps en LOB-apps, moet u ook het verschil begrijpen tussen apps die zijn aangeschaft via een volumeaankoopprogramma en apps met licentie, bijvoorbeeld: 
- **Apple-volumeaankoopprogramma voor bedrijven (iOS)** : u kunt in de iOS/iPadOS App Store meerdere licenties aanschaffen voor een app die u in uw bedrijf wilt uitvoeren. Door meerdere exemplaren aan te schaffen, kunt u apps in uw bedrijf efficiënt beheren. Raadpleeg [iOS-/iPadOS-apps beheren die zijn aangeschaft via een volumeaankoopprogramma met Microsoft Intune](vpp-apps-ios.md) voor meer informatie.
- **Android-werkprofiel**: Hoe u apps toewijst aan apparaten met een Android-werkprofiel verschilt van hoe u deze apps toewijst aan standaard Android-apparaten. Alle apps die u installeert voor Android-werkprofielen, zijn afkomstig uit de beheerde Google Play Store. U gebruikt Intune om te zoeken naar de gewenste apps en u keurt ze goed. De app verschijnt vervolgens op het knooppunt **Gelicentieerde apps** in Azure Portal, waarna u de toewijzing van apps kunt beheren zoals u bij elke app zou doen.
- **Microsoft Store voor Bedrijven (Windows 10)** : in de Microsoft Store voor Bedrijven kunt u apps zoeken en aanschaffen, zowel afzonderlijke exemplaren als in grotere volumes. Als u Windows Store voor Bedrijven aan Microsoft Intune koppelt, kunt u apps die zijn aangeschaft via een volumeaankoopprogramma, beheren in Azure Portal. Raadpleeg [Apps die u hebt aangeschaft in Microsoft Store voor Bedrijven, beheren met Microsoft Intune](windows-store-for-business.md) voor meer informatie.

    > [!NOTE]
    > De bestandsextensies voor Windows-apps zijn **.msi**, **.appx**, **.appxbundle**, **.msix** en **.msixbundle**.  

## <a name="before-you-add-apps"></a>Voordat u apps toevoegt
Overweeg de volgende punten voordat u begint met het toevoegen en toewijzen van apps:

- Wanneer u een app vanuit een App Store toevoegt en toewijst, moeten uw gebruikers beschikken over een account bij die store om de app te kunnen installeren.
- Sommige apps of items die u toewijst, zijn mogelijk afhankelijk van ingebouwde iOS-/iPadOS-apps. Als u bijvoorbeeld een boek uit de iOS/iPadOS Store toewijst, moet de app iBooks op het apparaat staan. Als u de ingebouwde app iBooks hebt verwijderd, kunt u Intune niet gebruiken om dit te herstellen.

> [!IMPORTANT]
> Als u de naam van de app wijzigt via Intune Azure Portal nadat u de app hebt geïnstalleerd en geïmplementeerd, kunt u geen beleid meer richten op de app met behulp van opdrachten.

## <a name="cloud-storage-space"></a>Cloudopslag
Alle apps die u maakt met het installatietype van het software-installatieprogramma (bijvoorbeeld een Line-Of-Business-app), worden verpakt en geüpload naar Intune-cloudopslag. Een proefabonnement op Intune omvat 2 GB (gigabyte) cloudopslag, die wordt gebruikt voor het opslaan van beheerde apps en updates. De totale hoeveelheid opslagruimte wordt niet beperkt met een volledig abonnement.

De vereisten voor cloudopslag zijn als volgt:

- Alle app-installatiebestanden moeten zich in dezelfde map bevinden.
- De maximale bestandsgrootte voor elk bestand dat u uploadt, is 8 GB.

  > [!NOTE]
  > Windows Line-Of-Business-apps (LOB), waaronder Win32, Windows Universal AppX, Windows Universal AppX-bundel, Windows Universal MSI X en Windows Universal MSI X-bundel, hebben een maximale grootte van 8 GB per app. Alle andere LOB-apps, inclusief iOS/iPadOS LOB-apps, hebben een maximale grootte van 2 GB per app.

## <a name="create-and-edit-categories-for-apps"></a>Categorieën voor apps maken en bewerken

App-categorieën kunnen worden gebruikt om apps te sorteren, zodat gebruikers deze sneller kunnen vinden in de bedrijfsportal. U kunt een of meer categorieën toewijzen aan een app, bijvoorbeeld *Ontwikkelaars-apps* of *Communicatie-apps*.

Als u een app aan Intune toevoegt, kunt u de gewenste categorie selecteren. Aan de hand van de platformspecifieke onderwerpen kunt u een app toevoegen en categorieën toewijzen. Als u uw eigen categorieën wilt maken en bewerken, gebruikt u de volgende procedure:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selecteer **Apps** > **App-categorieën**.  
    In het deelvenster **App-categorieën** wordt een lijst met categorieën weergegeven. 
5. Gebruik een van de volgende methoden:
    - Selecteer **Toevoegen** in het deelvenster **Categorie maken** en voer een naam in voor de categorie om een categorie te toe te voegen.  
    Namen kunnen slechts in één taal worden ingevoerd en worden niet door Intune vertaald.
    - Als u een categorie wilt bewerken, selecteert u het weglatingsteken ( **...** ) naast de categorie en vervolgens **Vastmaken aan dashboard** of **Verwijderen**.
6. Selecteer **Maken**.

## <a name="apps-that-are-added-automatically-by-intune"></a>Apps die automatisch door Intune zijn toegevoegd

Voorheen bevatte Intune een aantal ingebouwde apps die u snel kon toewijzen. Op basis van klantenfeedback over Intune hebben we deze lijst verwijderd en worden de ingebouwde apps niet langer weergegeven. Als u echter al ingebouwde apps hebt toegewezen, blijven deze apps zichtbaar in de lijst met apps. U kunt de apps desgewenst blijven toewijzen.

> [!NOTE]
> Voor de installatie van een vereiste niet-Line-of-Business-app probeert Intune de app te installeren door een installatie-opdracht te sturen wanneer het apparaat incheckt, ervan uitgaande dat de app niet is gedetecteerd en de installatiestatus van de app niet *Installatie in behandeling* is.

## <a name="installing-updating-or-removing-required-apps"></a>Vereiste apps installeren, bijwerken of verwijderen

Intune kan een vereiste app automatisch binnen 24 uur opnieuw installeren, bijwerken of verwijderen in plaats van te wachten op de herbeoordelingscyclus van 7 dagen.

Intune zal een vereiste app op basis van de volgende voorwaarden automatisch opnieuw installeren, bijwerken of verwijderen:
- Als een eindgebruiker een app verwijdert waarvan u hebt aangegeven dat deze moet zijn geïnstalleerd op het apparaat van de eindgebruiker, zal Intune de app automatisch opnieuw installeren zodra deze planning is verstreken.
- Als de installatie van een vereiste app is mislukt of als de app niet op het apparaat aanwezig is, evalueert Intune de naleving en wordt de app opnieuw geïnstalleerd zodra deze planning is verstreken.  
- Een beheerder geeft voor een gebruikersgroep aan dat een app beschikbaar is en de eindgebruiker installeert de app vanuit de bedrijfsportal op het apparaat. Later zal de beheerder de app bijwerken van v1 naar v2. Intune werkt de app bij zodra deze planning is verstreken, mits eerdere versies van de app nog steeds op het apparaat aanwezig zijn.
- Als de beheerder een verwijderintentie implementeert en de app op het apparaat aanwezig is maar niet kan worden verwijderd, evalueert Intune de naleving en wordt de app verwijderd zodra deze planning is verstreken.   

## <a name="uninstall-an-app"></a>Een app verwijderen

Als u een app moet verwijderen van apparaten van de gebruiker, volgt u de volgende stappen.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Alle apps** > *de app* > **Toewijzingen** > **Groep toevoegen**.
3. Selecteer **Verwijderen** in het deelvenster **Groep toevoegen**.
4. Selecteer **Opgenomen groepen** om de gebruikersgroepen te selecteren die worden beïnvloed door deze app-toewijzing.
5. Selecteer de groepen waarop u de verwijderingstoewijzing wilt toepassen.
6. Klik op **Selecteren** in het deelvenster **Groepen selecteren**.
7. Klik op **OK** in het deelvenster **Toewijzen** om de toewijzing in te stellen.
8. Selecteer **Groepen uitsluiten** als u gebruikersgroepen wilt uitsluiten zodat ze niet worden beïnvloed door deze app-toewijzing.
9. Kies **Selecteren** in **Groepen selecteren** als u hebt besloten dat u groepen wilt uitsluiten.
10. Selecteer **OK** in het deelvenster **Groep toevoegen**.
11. Selecteer **Opslaan** in het deelvenster **Toewijzingen** van de app.

> [!IMPORTANT]
> Als u de app wilt verwijderen, moet u de leden of groepstoewijzing voor installatie verwijderen voordat u ze toewijst om te worden verwijderd. Als een groep wordt toegewezen voor zowel het installeren als het verwijderen van een app, blijft de app gehandhaafd en wordt deze niet verwijderd.

## <a name="app-installation-errors"></a>App-installatiefouten

Zie [App-installatiefouten](troubleshoot-app-install.md) voor meer informatie over installatiefouten bij Intune-apps.

## <a name="next-steps"></a>Volgende stappen

Als u wilt leren hoe u voor elk platform apps aan Intune toevoegt, raadpleegt u:

- [Android Store-apps](store-apps-android.md)
- [Android LOB-apps](lob-apps-android.md)
- [iOS Store-apps](store-apps-ios.md)
- [iOS LOB-apps](lob-apps-ios.md)
- [macOS LOB-apps](lob-apps-macos.md)
- [Web-apps (voor alle platformen)](web-app.md)
- [Microsoft Store-apps](store-apps-windows.md)
- [Windows LOB-app](lob-apps-windows.md)
- [Office 365-apps voor Windows 10](apps-add-office365.md)
- [Office 365-apps voor macOS](apps-add-office365-macos.md)
- [Beheerde Google Play-apps](apps-add-android-for-work.md)
- [Microsoft Edge voor Windows 10](apps-windows-edge.md)
- [Microsoft Edge voor macOS](apps-edge-macos.md)
- [Ingebouwde apps](apps-add-built-in.md)
- [Android Enterprise-systeem-app](apps-ae-system.md)
- [Win32-apps](apps-win32-app-management.md)

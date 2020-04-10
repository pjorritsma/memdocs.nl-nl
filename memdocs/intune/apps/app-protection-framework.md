---
title: Gegevensbeschermingsframework met beleid voor app-beveiliging
titleSuffix: Microsoft Intune
description: Meer informatie over hoe beleid voor app-beveiliging ervoor zorgt dat de bedrijfsgegevens veilig blijven of worden opgenomen in een beheerde app, ongeacht of het apparaat al of niet is ingeschreven.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 635804a9ad5cd76d104f16bcd204df1daa28b114
ms.sourcegitcommit: e17fc618d4c56c38a65c489b73ba27baa133ee7b
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/06/2020
ms.locfileid: "80696486"
---
# <a name="data-protection-framework-using-app-protection-policies"></a>Gegevensbeschermingsframework met beleid voor app-beveiliging 

Naarmate meer organisaties strategieën voor mobiele apparaten voor toegang tot werk- of schoolgegevens implementeren, wordt de beveiliging tegen lekkage van gegevens van cruciaal belang. De Mobile Application Management-oplossing van Intune voor beveiliging tegen gegevenslekken is een app-beveiligingsbeleid. Met beleid voor app-beveiliging wordt ervoor gezorgd dat de bedrijfsgegevens veilig blijven of worden opgenomen in een beheerde app, ongeacht of het apparaat al of niet is ingeschreven. Zie [Overzicht van beleid voor app-beveiliging](app-protection-policy.md) voor meer informatie.

Bij het configureren van beleid voor app-beveiliging kunnen organisaties diverse instellingen en opties gebruiken om de beveiliging aan te passen aan hun specifieke behoeften. Vanwege deze flexibiliteit is het wellicht niet duidelijk welke permutatie van beleidsinstellingen vereist is voor het implementeren van een volledig scenario. Om organisaties te helpen bij het bepalen van prioriteiten voor beperkingen voor clienteindpunten, heeft Microsoft een nieuwe taxonomie geïntroduceerd voor [beveiligingsconfiguraties in Windows 10](https://aka.ms/secconframework) en maakt Intune gebruik van een vergelijkbare taxonomie voor het gegevensbeschermingsframework met beleid voor app-beveiliging voor het beheer van mobiele apps.  

Het framework voor de configuratie van gegevensbescherming met beleid voor app-beveiliging is onderverdeeld in drie aparte configuratiescenario's:

- Basisgegevensbeveiliging voor ondernemingen (niveau 1): Microsoft raadt deze configuratie aan als de minimale configuratie voor gegevensbeveiliging voor een bedrijfsapparaat.

- Geavanceerde gegevensbeveiliging voor ondernemingen (niveau 2): Microsoft raadt deze configuratie aan voor apparaten waarop gebruikers toegang krijgen tot gevoelige of vertrouwelijke informatie. Deze configuratie is van toepassing voor de meeste mobiele gebruikers die toegang hebben tot werk- of schoolgegevens. Sommige van de besturingselementen kunnen van invloed zijn op de gebruikerservaring.

- Hoge gegevensbeveiliging voor ondernemingen (niveau 3): Microsoft raadt deze configuratie aan voor apparaten die worden uitgevoerd door een organisatie met een groter of meer geavanceerd beveiligingsteam, of voor specifieke gebruikers of groepen die een uniek hoog risico hebben (een organisatie heeft bijvoorbeeld gebruikers geïdentificeerd die gegevens verwerken waarvan de diefstal direct ernstige gevolgen voor hun aandelenprijs zou hebben). Een organisatie die veel kans loopt het doelwit te zijn van goed gefinancierde en geavanceerde aanvallers, moet streven naar deze configuratie.

## <a name="app-data-protection-framework-deployment-methodology"></a>Implementatiemethodologie van gegevensbeschermingsframework met beleid voor app-beveiliging

Net als bij elke implementatie van nieuwe software, functies of instellingen, raadt Microsoft aan om te investeren in een ringmethodologie voor testvalidaties voorafgaand aan de implementatie van het gegevensbeschermingsframework met beleid voor app-beveiliging. Het definiëren van implementatieringen is over het algemeen een eenmalige gebeurtenis (of ten minste een niet veel voorkomende gebeurtenis), maar deze groepen moeten opnieuw worden gecontroleerd om ervoor te zorgen dat het sequentiëren nog steeds correct is.

Microsoft raadt de volgende implementatieringmethode aan voor het gegevensbeschermingsframework met beleid voor app-beveiliging:

| Implementatiering  | Tenant  | Evaluatieteams  | Uitvoer  | Tijdlijn  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| Kwaliteitsgarantie  | Tenant vóór productie  | Eigenaren van mobiele mogelijkheden, beveiliging, evaluatie van risico's, privacy, UX  | Validatie van functionele scenario's, conceptdocumentatie  | 0-30 dagen  |
| Preview  | Productietenant  | Eigenaren van mobiele mogelijkheden, UX  | Validatie van scenario's voor eindgebruikers, documentatie voor gebruikers  | 7-14 dagen, kwaliteitsgarantie achteraf  |
| Productie  | Productietenant  | Eigenaren van mobiele mogelijkheden, IT-helpdesk  | N.v.t.  | 7 dagen tot verschillende weken, na preview  |

Zoals in de bovenstaande tabel wordt aangegeven, moeten alle wijzigingen in het beleid voor app-beveiliging eerst worden uitgevoerd in een pre-productieomgeving om inzicht te krijgen in de gevolgen van de beleidsinstellingen. Zodra het testen is voltooid, kunnen de wijzigingen worden verplaatst naar de productie en worden toegepast op een subset productiegebruikers, meestal de IT-afdeling en andere toepasselijke groepen. En ten slotte kan de implementatie worden voltooid naar de rest van de mobiele-gebruikerscommunity. Implementatie naar productie kan enige tijd duren, afhankelijk van hoe groot de impact van de wijziging is. Als er geen gevolgen voor de gebruikers zijn, wordt de wijziging waarschijnlijk snel geïmplementeerd. Maar als de wijziging wel gevolgen voor de gebruikers heeft, is er mogelijk meer tijd nodig voor de implementatie omdat de gebruikers van de wijzigingen op de hoogte moeten worden gesteld.

Bij het testen van wijzigingen in een beleid voor app-beveiliging moet u zich bewust zijn van de [leveringstiming](app-protection-policy-delivery.md). De status van de levering van het beleid voor app-beveiliging voor een bepaalde gebruiker kan worden gecontroleerd. Zie [How to monitor app protection policies](app-protection-policies-monitor.md) (App-beveiligingsbeleid controleren) voor meer informatie.

Afzonderlijke instellingen van het beleid voor app-beveiliging voor elke app kunnen worden gevalideerd op apparaten met Edge en de URL *about:Intunehelp*. Zie [Logboeken van beveiliging voor client-apps controleren](app-protection-policy-settings-log.md) en [Internettoegang beheren met behulp van Microsoft Edge met Microsoft Intune](manage-microsoft-edge.md#use-microsoft-edge-to-access-managed-app-logs) voor meer informatie.

## <a name="app-data-protection-framework-settings"></a>Gegevensbeschermingsframework met beleid voor app-beveiliging

De volgende instellingen voor het app-beveiligingsbeleid moeten worden ingeschakeld voor de toepasselijke apps en worden toegewezen aan alle mobiele gebruikers. Zie [Beveiligingsbeleidsinstellingen voor iOS-apps](app-protection-policy-settings-ios.md) en [Beveiligingsbeleidsinstellingen voor Android-apps](app-protection-policy-settings-android.md) voor meer informatie over de beleidsinstellingen.

Microsoft raadt u aan gebruiksscenario's te bekijken en te categoriseren, en vervolgens gebruikers te configureren met behulp van de specifieke richtlijnen voor dat niveau. Net als bij elk framework moeten instellingen binnen een overeenkomstig niveau mogelijk worden aangepast op basis van de behoeften van de organisatie, omdat bij de gegevensbescherming de dreigingsomgeving, risicobereidheid en impact op de bruikbaarheid moeten worden beoordeeld.  

### <a name="conditional-access-policies"></a>Beleid voor voorwaardelijke toegang
Beleid voor voorwaardelijke toegang van Azure Active Directory is vereist om ervoor te zorgen dat alleen apps die ondersteuning bieden voor app-beveiligingsbeleid toegang hebben tot gegevens in werk- en schoolaccounts. Zie **Scenario 1: Office 365-apps vereisen goedgekeurde apps met app-beveiligingsbeleid** in [App-beveiligingsbeleid vereisen voor toegang tot cloud-apps met voorwaardelijke toegang](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access) voor stappen voor het implementeren van specifiek beleid.

### <a name="apps-to-include-in-the-app-protection-policies"></a>Apps die moeten worden opgenomen in het app-beveiligingsbeleid  

Voor elk app-beveiligingsbeleid moeten de volgende Microsoft-kern-apps worden opgenomen:

- Edge
- Excel
- Kantoor
- OneDrive
- OneNote
- Outlook
- PowerPoint
- Microsoft Teams
- Microsoft To-Do
- Word
- Microsoft SharePoint

Het beleid moet ook gelden voor andere Microsoft-apps op basis van bedrijfsbehoeften, extra openbare apps van derden waarin de Intune-SDK die in de organisatie wordt gebruikt is geïntegreerd, evenals Line-Of-Business-apps waarin de [Intune-SDK](../developer/app-sdk.md) is geïntegreerd (of die zijn verpakt).

### <a name="level-1-enterprise-basic-data-protection"></a>Basisgegevensbeveiliging voor ondernemingen op niveau 1

Niveau 1 is de minimale configuratie van gegevensbeveiliging voor mobiele bedrijfsapparaten. Deze configuratie vervangt de noodzaak van basis-Exchange Online-beleid voor toegang tot apparaten door een pincode te vereisen voor toegang tot werk- of schoolgegevens, de gegevens van het werk- of schoolaccount te versleutelen en de mogelijkheid te bieden om de school- of werkgegevens selectief te wissen. In tegenstelling tot het Exchange Online-beleid voor toegang tot apparaten zijn de onderstaande instellingen voor app-beveiligingsbeleid van toepassing op alle apps die in het beleid zijn geselecteerd, zodat de toegang tot gegevens ook buiten de scenario's voor mobiele berichten is beveiligd.

Met het beleid in niveau 1 wordt een redelijk gegevenstoegangsniveau afgedwongen, terwijl de gevolgen voor gebruikers worden geminimaliseerd en de standaardinstellingen voor gegevensbeveiliging en -toegang worden gespiegeld wanneer er een app-beveiligingsbeleid in Microsoft Eindpuntbeheer wordt gemaakt.  

#### <a name="data-protection"></a>Gegevensbescherming

| Instelling | Beschrijving van instelling |             Waarde  |             Platform        |
|-----------------|--------------------------------------------------------|-----------------------|----------------------------------------|
| Gegevensoverdracht |             Back-up van organisatiegegevens naar...  |             Toestaan  |             iOS/iPadOS, Android        |
| Gegevensoverdracht |       Organisatiegegevens naar andere apps verzenden  |             Alle apps  |             iOS/iPadOS, Android        |
| Gegevensoverdracht |       Gegevens ontvangen van andere apps  |             Alle apps  |             iOS/iPadOS, Android        |
| Gegevensoverdracht |       Knippen, kopiëren en plakken tussen apps beperken  |             Elke app  |             iOS/iPadOS, Android        |
| Gegevensoverdracht |       Toetsenborden van derden  |             Toestaan  |             iOS/iPadOS        |
| Gegevensoverdracht |       Goedgekeurde toetsenborden  |             Niet vereist  |             Android        |
| Gegevensoverdracht |       Schermopname en Google Assistant  |             Toestaan  |             Android        |
| Versleuteling |             Organisatiegegevens versleutelen  |             Vereist  |             iOS/iPadOS, Android        |
| Versleuteling |       Organisatiegegevens op ingeschreven apparaten versleutelen  |             Vereist  |             Android        |
| Functionaliteit  |             App synchroniseren met systeemeigen app Contactpersonen  |             Toestaan  |             iOS/iPadOS, Android        |
| Functionaliteit  |       Organisatiegegevens afdrukken  |             Toestaan  |             iOS/iPadOS, Android        |
| Functionaliteit  |       Overdracht van webinhoud met andere apps beperken  |             Elke app  |             iOS/iPadOS, Android        |
| Functionaliteit  |       Meldingen van organisatiegegevens  |             Toestaan  |             iOS/iPadOS, Android        |

#### <a name="access-requirements"></a>Vereisten voor toegang 

| Instelling  | Waarde  | Platform  | Opmerkingen  |
|----------------------------------------------------------------|---------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pincode voor toegang  | Vereist  | iOS/iPadOS, Android  |   |
| Pincodetype  | Numeriek  | iOS/iPadOS, Android  |   |
| Eenvoudige pincode  | Toestaan  | iOS/iPadOS, Android  |   |
| Minimale lengte pincode selecteren  | 4  | iOS/iPadOS, Android  |   |
| Biometrische gegevens in plaats van pincode voor toegang  | Toestaan  | iOS/iPadOS, Android  |   |
| Biometrische gegevens in plaats van pincode voor toegang overschrijven  | Vereist  | iOS/iPadOS, Android  |   |
| Time-out (minuten van inactiviteit)  | 720  | iOS/iPadOS, Android  |   |
| Face ID in plaats van pincode voor toegang  | Toestaan  | iOS/iPadOS  |   |
| Pincode na aantal dagen opnieuw instellen  | Nee  | iOS/iPadOS, Android  |   |
| Pincode voor de app wanneer een apparaatpincode is ingesteld  | Vereist  | iOS/iPadOS, Android  | Als het apparaat is ingeschreven bij Intune, kunnen beheerders overwegen om dit in te stellen op Niet vereist als ze een sterke pincode voor het apparaat afdwingen via een nalevingsbeleid voor apparaten.  |
| Aanmeldingsgegevens voor werk- of schoolaccount voor toegang  | Niet vereist  | iOS/iPadOS, Android  |   |
| Toegangsvereisten opnieuw controleren na (minuten van inactiviteit)  | 30  | iOS/iPadOS, Android  |   |

#### <a name="conditional-launch"></a>Voorwaardelijk starten 

| Instelling | Beschrijving van instelling |          Waarde/actie  |          Platform        | Opmerkingen |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| App-voorwaarden |       Maximum aantal pincodepogingen  |          5/Pincode opnieuw instellen  |          iOS/iPadOS, Android  |                  |
| App-voorwaarden |       Offlinerespijtperiode  |          720/Toegang blokkeren (minuten)  |          iOS/iPadOS, Android  |                  |
| App-voorwaarden |       Offlinerespijtperiode  |          90/Gegevens wissen (dagen)  |          iOS/iPadOS, Android  |                  |
| Apparaatvoorwaarden  |       Apparaten die zijn opengebroken of geroot  |        N.v.t./Toegang blokkeren  |          iOS/iPadOS, Android  |                  |
| Apparaatvoorwaarden  |       SafetyNet-attestation voor apparaat  |          Basisintegriteit en gecertificeerde apparaten/Toegang blokkeren  |          Android  |          <p>Met deze instelling wordt SafetyNet-Attestation van Google op apparaten van de eindgebruiker geconfigureerd. Met basisintegriteit wordt de integriteit van het apparaat gevalideerd. Geroote apparaten, emulators, virtuele apparaten en apparaten met zichtbare sabotagesporen voldoen niet aan de basisintegriteit. </p><p> Met basisintegriteit en gecertificeerde apparaten worden de compatibiliteit van het apparaat met services van Google gevalideerd. Alleen niet-aangepaste apparaten die door Google zijn gecertificeerd, voldoen aan deze controle.</p>  |
| Apparaatvoorwaarden  |       Bedreigingsscan voor apps vereisen  |        N.v.t./Toegang blokkeren  |          Android  |          Deze instelling zorgt ervoor dat de scanfunctie voor Apps controleren van Google wordt ingeschakeld voor eindgebruikerapparaten. Als deze instelling is geconfigureerd, wordt de toegang geblokkeerd voor de eindgebruiker zolang deze de scanfunctie van Google voor apps niet inschakelt op het Android-apparaat.        |

#### <a name="level-2-enterprise-enhanced-data-protection"></a>Geavanceerde gegevensbeveiliging voor ondernemingen op niveau 2

Niveau 2 is de configuratie voor gegevensbeveiliging die wordt aanbevolen als standaard voor apparaten waarbij gebruikers toegang hebben tot meer gevoelige informatie. Deze apparaten zijn tegenwoordig vaak het doelwit in ondernemingen. Bij deze aanbevelingen wordt er niet uitgegaan van een groot aantal medewerkers met veel ervaring op het gebied van beveiliging. Om die reden is het belangrijk dat de configuratie voor veel bedrijven toegankelijk is. Deze configuratie is een uitbreiding van de configuratie in niveau 1 door scenario's voor gegevensoverdracht te beperken en door een minimumversie van het besturingssysteem te vereisen.

De beleidsinstellingen die in niveau 2 worden afgedwongen, bevatten alle beleidsinstellingen die worden aanbevolen voor niveau 1 en de onderstaande beleidsinstellingen worden alleen toegevoegd of bijgewerkt om meer besturingselementen en een meer geavanceerde configuratie dan niveau 1 te implementeren. Hoewel deze instellingen misschien iets meer impact op gebruikers of toepassingen hebben, wordt een niveau van gegevensbescherming afgedwongen dat beter past bij de risico's die gelden voor gebruikers met toegang tot gevoelige informatie op mobiele apparaten.

#### <a name="data-protection"></a>Gegevensbescherming

| Instelling | Beschrijving van instelling |             Waarde  |             Platform        | Opmerkingen |
|---------------|----------------------------------------------------------|-----------------------------------------------|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Gegevensoverdracht |       Back-up van organisatiegegevens naar...  |          Blokkeren  |          iOS/iPadOS, Android  |                  |
| Gegevensoverdracht |       Organisatiegegevens naar andere apps verzenden  |          Door beleid beheerde apps  |          iOS/iPadOS, Android  |          <p>Bij iOS/iPadOS kunnen beheerders deze waarde configureren als Door beleid beheerde apps, Door beleid beheerde apps met delen van het besturingssysteem of Door beleid beheerde apps met filteren op openen in/delen. </p><p>Door beleid beheerde apps met delen van het besturingssysteem is beschikbaar wanneer het apparaat ook is ingeschreven bij Intune. Met deze instelling is gegevensoverdracht naar andere door beleid beheerde apps toegestaan, evenals bestandsoverdracht naar andere apps die worden beheerd met Intune. </p><p>Met Door beleid beheerde apps met filteren op openen in/delen worden de dialoogvensters Openen in/Delen van het besturingssysteem zo gefilterd dat alleen door beleid beheerde apps worden weergegeven. </p><p> Zie [Beveiligingsbeleidsinstellingen voor iOS-apps](app-protection-policy-settings-ios.md) voor meer informatie.</p> |
| Gegevensoverdracht |       Kopieën van de organisatiegegevens opslaan  |          Blokkeren  |          iOS/iPadOS, Android  |                  |
| Gegevensoverdracht |       De gebruiker toestaan om kopieën op te slaan in de geselecteerde services  |          OneDrive voor Bedrijven, SharePoint Online |          iOS/iPadOS, Android  |                  |
| Gegevensoverdracht |       Knippen, kopiëren en plakken tussen apps beperken  |          Door beleid beheerde apps met plakken in  |          iOS/iPadOS, Android  |                  |
| Gegevensoverdracht |       Schermopname en Google Assistant  |          Blokkeren  |          Android  |                  |
| Functionaliteit |       Overdracht van webinhoud met andere apps beperken  |          Microsoft Edge  |          iOS/iPadOS, Android  |                  |
| Functionaliteit |       Meldingen van organisatiegegevens  |          Organisatiegegevens blokkeren  |          iOS/iPadOS, Android  |          Zie [Beveiligingsbeleidsinstellingen voor iOS-apps](app-protection-policy-settings-ios.md) en [Beveiligingsbeleidsinstellingen voor Android-apps](app-protection-policy-settings-android.md) voor een lijst met apps die deze instelling ondersteunen.       |

#### <a name="conditional-launch"></a>Voorwaardelijk starten

| Instelling | Beschrijving van instelling |          Waarde/actie  |          Platform        | Opmerkingen |
|--------------------|----------------------------|-----------------------------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Apparaatvoorwaarden  |       Minimale versie van het besturingssysteem  |          *Indeling: Major.Minor.Build <br>Voorbeeld:   12.4.4*/Toegang blokkeren |          iOS/iPadOS        | Microsoft raadt aan de minimale primaire iOS-versie te configureren zodat deze overeenkomt met de ondersteunde iOS-versies voor Microsoft-apps.   Microsoft-apps ondersteunen een N-1-benadering waarbij N de huidige versie van de primaire iOS-release is. Voor primaire en buildversies raadt Microsoft aan ervoor te zorgen dat apparaten zijn bijgewerkt met de respectieve beveiligingspatches. Zie [Apple-beveiligingspatches](https://support.apple.com/en-us/HT201222) voor de meest recente aanbevelingen van Apple |
| Apparaatvoorwaarden  |       Minimale versie van het besturingssysteem  |          *Indeling: Major.Minor<br> Voorbeeld: 8.0*/Toegang blokkeren   |          Android        | Microsoft raadt aan de minimale primaire versie van Android te configureren zodat deze overeenkomt met de ondersteunde Android-versies voor Microsoft-apps. OEM's en apparaten die voldoen aan de aanbevolen Android Enterprise-vereisten, moeten ondersteuning bieden voor de release die nu wordt vrijgegeven + upgrade van één letter.   Op dit moment wordt Android 8.0 of hoger door Android aangeraden voor kennismedewerkers.   Zie [Aanbevolen Android Enterprise-vereisten](https://www.android.com/enterprise/recommended/requirements/) voor de nieuwste aanbevelingen van Android |
| Apparaatvoorwaarden  |       Minimale patchversie  |          *Indeling:   JJJJ-MM-DD <br> Voorbeeld: 2020-01-01*/Toegang blokkeren  |          Android        | Android-apparaten kunnen maandelijkse beveiligingspatches ontvangen, maar de release is afhankelijk van OEM's en/of providers. Organisaties moeten ervoor zorgen dat geïmplementeerde Android-apparaten beveiligingspatches ontvangen voordat deze instelling wordt geïmplementeerd. Zie [Android-beveiligingsbulletins](https://source.android.com/security/bulletin/) voor de nieuwste patchreleases.  |

#### <a name="level-3-enterprise-high-data-protection"></a>Hoge gegevensbeveiliging voor ondernemingen op niveau 3 

Niveau 3 is de configuratie voor gegevensbeveiliging die wordt aanbevolen als standaard voor organisaties met veel ervaren beveiligingsmedewerkers of voor specifieke gebruikers en groepen die een grote kans op aanvallen hebben. Het gaat hier vaak om goed gefinancierde geavanceerde aanvallen zodat de hier beschreven extra beperkingen en besturingselementen heel nuttig zijn. Deze configuratie is een uitbreiding van de configuratie in niveau 2 door extra scenario's voor gegevensoverdracht te beperken, de complexiteit van de configuratie van pincodes te verhogen en detectie van mobiele bedreigingen toe te voegen.  

De beleidsinstellingen die in niveau 3 worden afgedwongen, bevatten alle beleidsinstellingen die worden aanbevolen voor niveau 2 en 1, en de onderstaande beleidsinstellingen worden alleen toegevoegd of bijgewerkt om striktere configuratie en besturingselementen voor gegevensbeveiliging te implementeren. Deze beleidsinstellingen kunnen veel impact op gebruikers of toepassingen hebben, doordat een beveiligingsniveau wordt afgedwongen dat beter past bij organisaties die risico's lopen.  

#### <a name="data-protection"></a>Gegevensbescherming

| Instelling | Beschrijving van instelling |             Waarde  |             Platform        | Opmerkingen |
|---------------|---------------------------------------|----------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------------------|
| Gegevensoverdracht |       Gegevens ontvangen van andere apps  |          Door beleid beheerde apps  |          iOS/iPadOS, Android         |  |
| Gegevensoverdracht |       Toetsenborden van derden  |          Blokkeren  |          iOS/iPadOS        | Hiermee worden in iOS alle toetsenborden van derden in de app geblokkeerd.  |
| Gegevensoverdracht |       Goedgekeurde toetsenborden  |          Vereist  |          Android        | Bij Android moeten er toetsenborden worden geselecteerd voor gebruik op de geïmplementeerde Android-apparaten.  |
| Gegevensoverdracht |       Toetsenborden selecteren voor goedkeuring  |          *toetsenborden toevoegen/verwijderen*  |          Android        | Bij Android moeten er toetsenborden worden geselecteerd voor gebruik op de geïmplementeerde Android-apparaten.  |
| Functionaliteit |       Organisatiegegevens afdrukken  |          Blokkeren  |          iOS/iPadOS, Android         |  |

#### <a name="access-requirements"></a>Vereisten voor toegang

|       Instelling  |          Waarde  |          Platform  |
|-----------------------------------------------------------|--------------------|---------------------------------|
|       Eenvoudige pincode  |          Blokkeren  |          iOS/iPadOS, Android  |
|       Minimale lengte pincode selecteren  |          6  |          iOS/iPadOS, Android  |
|       Pincode na aantal dagen opnieuw instellen  |          Ja  |          iOS/iPadOS, Android  |
|       Aantal dagen  |          365  |          iOS/iPadOS, Android  |

#### <a name="conditional-launch"></a>Voorwaardelijk starten

| Instelling | Beschrijving van instelling |          Waarde/actie  |          Platform        | Opmerkingen |
|----------------------------|--------------------------------------|-------------------|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       Apparaatvoorwaarden  |          Apparaten die zijn opengebroken of geroot  |        N.v.t./Gegevens wissen  |          iOS/iPadOS, Android        |  |
|       Apparaatvoorwaarden  |          Maximaal toegestaan bedreigingsniveau  |          Beveiligd/Toegang blokkeren  |          iOS/iPadOS, Android        | <p>Apparaten die niet zijn ingeschreven, kunnen worden gecontroleerd op bedreigingen met behulp van Mobile Threat Defense. Zie [Mobile Threat Defense voor niet-ingeschreven apparaten](https://aka.ms/mtdmamdocs) voor meer informatie.      </p><p>     Als het apparaat is ingeschreven, kan deze instelling worden overgeslagen als u Mobile Threat Defense voor ingeschreven apparaten wilt implementeren. Zie [Mobile Threat Defense voor ingeschreven apparaten](../protect/mtd-device-compliance-policy-create.md) voor meer informatie.</p> |

## <a name="next-steps"></a>Volgende stappen

Beheerders kunnen de bovenstaande configuratieniveaus opnemen in hun ringimplementatiemethode voor test- en productiegebruik door de voorbeeld-[JSON-sjablonen voor het framework voor de configuratie van Intune-app-beveiligingsbeleid](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) met [PowerShell-scripts](https://github.com/microsoftgraph/powershell-intune-samples) te importeren.

## <a name="see-also"></a>Zie tevens

- [Beveiligingsbeleid voor apps maken en implementeren met Microsoft Intune](app-protection-policies.md)
- [Beschikbare instellingen voor beveiligingsbeleid voor Android-apps met Microsoft Intune](app-protection-policy-settings-android.md)
- [Beschikbare instellingen voor beveiligingsbeleid voor iOS-/iPadOS-apps met Microsoft Intune](app-protection-policy-settings-ios.md)
- Apps van derden, zoals de mobiele app van Salesforce, werken gericht met Intune om bedrijfsgegevens te beveiligen. Ga voor meer informatie over hoe de Salesforce-app met Intune werkt (inclusief MDM-configuratie-instellingen voor apps), naar [Salesforce-app en Microsoft Intune](https://gallery.technet.microsoft.com/Salesforce-App-and-Intune-c47d44ee/file/188000/1/Salesforce%20App%20and%20Intune%20for%20external.pdf).

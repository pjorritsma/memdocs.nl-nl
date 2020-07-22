---
title: Wandera Mobile Threat Protection-integratie met Intune instellen
titleSuffix: Intune on Azure
description: Lees hoe u de Wandera Mobile Threat Protection-oplossing instelt met Microsoft Intune om toegang tot uw bedrijfsbronnen met mobiele apparaten te beheren.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: b227148a6e16f7c9f8d62cb58eeb628afbd84123
ms.sourcegitcommit: 2e0bc4859f7e27dea20c6cc59d537a31f086c019
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/21/2020
ms.locfileid: "86872015"
---
# <a name="integrate-wandera-mobile-threat-protection-with-intune"></a>Wandera Mobile Threat Protection integreren met Intune  

Voer de volgende stappen uit om de Wandera Mobile Threat Defense-oplossing te integreren met Intune.  

## <a name="before-you-begin"></a>Voordat u begint  

Voordat u het integratieproces van Wandera met Intune begint, moet u ervoor zorgen dat u beschikt over het volgende:

- Intune-abonnement
- Azure Active Directory-beheerdersreferenties en toegewezen rol om de volgende machtigingen te verlenen:

    - Aanmelden en gebruikersprofiel lezen
    - Toegang tot de map als de aangemelde gebruiker
    - Mapgegevens lezen
    - Risicogegevens van een apparaat naar Intune verzenden
 
- Een geldig Wandera-abonnement
    - Een beheerdersaccount met superbeheerdersbevoegdheden

## <a name="integration-overview"></a>Integratieoverzicht

Inschakeling van Mobile Threat Defense-integratie tussen Wandera en Intune omvat het volgende:

- UEM Connect-service van Wandera inschakelen voor het synchroniseren van informatie met Azure en Intune. Dit omvat de LCM-metagegevens (Life Cycle Management) van de gebruiker en het apparaat, samen met het dreigingsniveau van de Mobile Threat Defense (MTD) van het apparaat.
- Activeringsprofielen in Wandera maken om het gedrag van de apparaatinschrijving te bepalen.
- Wandera draadloos implementeren op beheerde iOS- en Android-apparaten.
- Wandera configureren voor selfservice voor eindgebruikers met MAM-WE op niet-beheerde iOS-en Android-apparaten.

## <a name="set-up-wandera-mobile-threat-defense-integration"></a>Wandera Mobile Threat Defense-integratie instellen

Het instellen van de integratie tussen Wandera en Intune kan gemakkelijk binnen enkele minuten worden gerealiseerd. Hiervoor is geen ondersteuning van Wandera-personeel vereist.

### <a name="enable-support-for-wandera-in-intune"></a>Ondersteuning voor Wandera in Intune inschakelen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Tenantbeheer** > **Connectors en tokens** > **Mobile Threat Defense** > **Toevoegen**.
3. Ga naar de pagina **Connector toevoegen** en gebruik de vervolgkeuzelijst om **Wandera** te selecteren. En selecteer vervolgens **Maken**.  
4. Selecteer in het Mobile Threat Defense-venster de MTD-connector **Wandera** uit de lijst met connectors om het deelvenster **Connector bewerken** te openen. Selecteer **Open de Wandera-beheerdersconsole** om [RADAR](https://radar.wandera.com/login), de beheerdersconsole van Wandera, te openen en meld u aan. 
5. Ga in de Wandera RADAR-console naar **Integraties > UEM-integratie** en selecteer het tabblad **UEM Connect**. Gebruik de vervolgkeuzelijst EMM-leverancier om **Microsoft Intune** te selecteren.
6. Er wordt een scherm weergegeven dat lijkt op het onderstaande, met de machtigingen die zijn vereist voor het voltooien van de integratie:

   ![Integraties en machtigingen](./media/wandera-mtd-connector-integration/integrations-and-permissions.png) 

7. Naast Intune User and Device Sync klikt u op de knop Toekennen om het proces te starten en Wandera toestemming te geven om de LCM-functies (Life Cycle Management) met Azure en Intune uit te voeren.
8. Selecteer of voer uw Azure-beheerdersreferenties in wanneer daarom wordt gevraagd. Controleer de aangevraagde machtigingen en schakel het selectievakje in om namens uw organisatie toestemming te geven. Klik ten slotte op Accepteren om de LCM-integratie te autoriseren.

   ![Machtigingen accepteren](./media/wandera-mtd-connector-integration/permissions.png)

9. U keert automatisch terug naar de RADAR-beheerconsole.  Als de autorisatie is geslaagd, ziet u een groen vinkje naast de knop Toekennen.
10. Herhaal het toestemmingsproces voor de resterende lijstintegraties door op de bijbehorende toekenningsknoppen te klikken totdat er groene vinkjes naast elke integratie staan.

11. Ga terug naar de Intune-console en bewerk de Wandera MTD-connector. Stel de beschikbare schakelknoppen in op Aan en klik op Opslaan om de configuratie op te slaan.

    ![Wandera inschakelen](./media/wandera-mtd-connector-integration/enable-wandera.png)

Intune en Wandera zijn nu verbonden.

## <a name="create-activation-profiles-in-wandera"></a>Maak activeringsprofielen in Wandera

Implementaties op basis van Intune worden mogelijk gemaakt met behulp van Wandera-activeringsprofielen die zijn gedefinieerd in RADAR.  Elk activeringsprofiel definieert specifieke configuratieopties, zoals verificatievereisten, servicemogelijkheden en eerste groepslidmaatschap.

Nadat u een activeringsprofiel in Wandera hebt gemaakt, wijst u dit toe aan gebruikers en apparaten in Intune.  Hoewel een activeringsprofiel universeel is voor apparaatplatforms en beheerstrategieën, wordt met de volgende stappen gedefinieerd hoe Intune moet worden geconfigureerd op basis van deze verschillen.

Voor de komende stappen wordt ervan uitgegaan dat u in Wandera een activeringsprofiel hebt gemaakt dat u via Intune wilt implementeren op uw doelapparaten. Zie de [handleiding voor activeringsprofielen](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/article/Enrollment-Links) voor meer informatie over het maken en gebruiken van Wandera-activeringsprofielen.

> [!NOTE]
> Bij het maken van activeringsprofielen voor implementatie via Intune of MAM-WE moet de optie Gekoppelde gebruiker zijn ingesteld op Geverifieerd door id-provider > Azure Active Directory voor maximale beveiliging, compatibiliteit met andere platformen en een gestroomlijnde eindgebruikerservaring.

## <a name="deploying-wandera-over-the-air-to-mdm-managed-devices"></a>Wandera draadloos implementeren op door MDM beheerde apparaten

Voor iOS- en Android-apparaten die worden beheerd door Intune, kan Wandera draadloos worden geïmplementeerd voor snelle activeringen op basis van pushberichten. Zorg ervoor dat u de benodigde activeringsprofielen al hebt gemaakt voordat u doorgaat met deze sectie. Voor het implementeren van Wandera voor beheerde apparaten is het volgende vereist:
- Wandera-configuratieprofielen aan Intune toevoegen en aan doelapparaten toewijzen.
- De Wandera-app en de bijbehorende app-configuraties toevoegen aan Intune en toewijzen aan doelapparaten.

### <a name="configure-and-deploy-ios-configuration-profiles"></a>iOS-configuratieprofielen configureren en implementeren 

In deze sectie downloadt u **vereiste** configuratiebestanden voor iOS-apparaten en stuurt u ze draadloos via MDM aan uw door Intune beheerde apparaten.

1. In **RADAR** gaat u naar het activeringsprofiel dat u wilt implementeren (Apparaten > Activeringen) en klikt u op het tabblad **Implementatiestrategieën > Beheerde apparaten > Microsoft Endpoint Manager**.
2. Vouw de sectie **Apple iOS onder supervisie** of **Apple iOS niet onder supervisie** uit op basis van de configuratie van uw apparaatfleet.
3. Download de opgegeven configuratieprofielen en bereid ze voor om ze in een volgende stap te uploaden.
4. Open de **Microsoft Intune-beheerconsole** en ga naar **Apparaten > iOS/iPadOS > Configuratieprofielen**.  Klik op **Profiel maken**.
5. Kies in het deelvenster dat wordt geopend **iOS/iPadOS** onder **Platform** en vervolgens **Aangepast** onder Profiel. Klik vervolgens op **Maken**.
6. Geef in het veld **Naam** een beschrijvende titel op voor de configuratie, in het ideale geval met de naam van het activeringsprofiel in RADAR. Dit zal in de toekomst helpen om kruisverwijzingen te vergemakkelijken. Indien gewenst kunt u ook de code van het activeringsprofiel opgeven. Geef aan of de configuratie bestemd is voor apparaten onder of zonder supervisie door een achtervoegsel aan de naam toe te voegen.
7. U kunt eventueel een **Beschrijving** opgeven om meer informatie te bieden voor andere beheerders over het doel/gebruik van de configuratie. Klik op **Volgende**.
8. Klik op **Een bestand selecteren** en zoek het gedownloade configuratieprofiel dat overeenkomt met het juiste activeringsprofiel dat u in stap 3 hebt gedownload. Zorg ervoor dat u het juiste profiel onder of zonder supervisie selecteert als u beide downloadt. Klik op **Volgende**.
   <!-- image placeholder - ending future availability -->
9.  Definieer **Bereiktags** zoals vereist door uw Intune RBAC-praktijken.  Klik op **Volgende**.
10. U moet het configuratieprofiel **toewijzen** aan groepen gebruikers of apparaten waarop Wandera moet worden geïnstalleerd.  U kunt het beste beginnen met een testgroep en deze vervolgens uitbreiden nadat u hebt gecontroleerd of de activeringen correct werken. Klik op **Volgende**.
11. Controleer of de configuratie correct is en pas deze aan waar nodig. Klik op **Maken** om het configuratieprofiel te maken en te implementeren.

> [!NOTE]
> Wandera biedt een uitgebreid implementatieprofiel voor iOS-apparaten onder supervisie. Als u een gemengde fleet met apparaten onder of zonder supervisie hebt, herhaalt u de bovenstaande stappen voor het andere profieltype naar behoefte. Deze stappen moeten worden gevolgd voor toekomstige activeringsprofielen die moeten worden geïmplementeerd via Intune. Neem contact op met de Wandera-ondersteuning als u een gemengde fleet hebt van iOS-apparaten onder en zonder supervisie en u hulp nodig hebt met beleidstoewijzingen op basis van supervisiemodus. 

## <a name="deploying-wandera-to-mam-we-devices"></a>Wandera implementeren op MAM-WE-apparaten
Voor apparaten die niet worden beheerd door Intune en MAM-WE-apparaten zijn, maakt Wandera gebruik van een geïntegreerde, op verificatie gebaseerde onboardingervaring om bedrijfsgegevens binnen MAM-apps te activeren en te beveiligen. 

In de volgende secties wordt beschreven hoe u Wandera en Intune configureert om eindgebruikers in staat te stellen Wandera naadloos te activeren voordat ze toegang krijgen tot bedrijfsgegevens. 

### <a name="configure-azure-device-provisioning-in-a-wandera-activation-profile"></a>Azure-apparaatinrichting configureren in een Wandera-activeringsprofiel
Voor activeringsprofielen die moeten worden gebruikt met MAM-WE moet Gekoppelde gebruiker zijn ingesteld op Geverifieerd op id-provider > Azure Active Directory.
1. Selecteer in de **Wandera RADAR**-portal een bestaand activeringsprofiel of maak een nieuw profiel dat MAM-WE-apparaten zullen gebruiken tijdens de inschrijving in Apparaten > Activeringen. 
2. Klik op het **tabblad Implementatiestrategieën en vervolgens op Niet-beheerde apparaten**. Schuif vervolgens naar de sectie **Azure-apparaatinrichting**.
3. Voer uw **Azure AD-tenant-id** in het bijbehorende tekstveld in. Als u uw tenant-id niet bij de hand hebt, klikt u op de koppeling **Mijn tenant-id ophalen** om Azure AD te openen op een nieuw tabblad waar u deze waarde eenvoudig kunt kopiëren naar uw klembord.
4. (Optioneel) Geef **Groep-id('s)** op om de activering van gebruikers te beperken tot specifieke groepen.
   - Als een of meer **Groep-id's** zijn gedefinieerd, moet een gebruiker die MAM-WE activeert, lid zijn van ten minste een van de opgegeven groepen om dit activeringsprofiel te activeren.
   - U kunt meerdere activeringsprofielen instellen die zijn geconfigureerd met dezelfde Azure-tenant-id, maar met verschillende groep-id's. Zo kunt u apparaten inschrijven in Wandera op basis van het lidmaatschap van een Azure-groep, waardoor er gedifferentieerde mogelijkheden per groep worden geboden tijdens de activering.
   - U kunt een standaard activeringsprofiel configureren waarmee geen groeps-id's worden opgegeven.  Deze groep zal dienen als vangnet voor alle activeringen waarbij de geverifieerde gebruiker geen lid is van een groep die is gekoppeld met een ander activeringsprofiel.
5. Klik op **Opslaan** in de rechterbovenhoek van de pagina.

## <a name="next-steps"></a>Volgende stappen
- Maak client-apps in Intune met uw Wandera-activeringsprofielen in RADAR geladen om de Wandera-app op Android- en iOS/iPadOS-apparaten te implementeren. De configuratie van de Wandera-app biedt essentiële functionaliteit als aanvulling op gepushte apparaatconfiguratieprofielen en wordt aanbevolen voor alle implementaties. Raadpleeg [MTD-apps toevoegen](mtd-apps-ios-app-configuration-policy-add-assign.md) voor de procedures en aangepaste details die specifiek zijn voor Wandera-apps. 
- Nu Wandera is geïntegreerd met Endpoint Manager, kunt u uw configuratie aanpassen, rapporten weergeven en breder implementeren op uw mobiele apparaten. Zie de [handleiding Aan de slag voor het ondersteuningscentrum](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/getting-started) in de Wandera-documentatie voor gedetailleerde configuratiehandleidingen.

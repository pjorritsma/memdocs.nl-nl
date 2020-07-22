---
title: Zebra Mobility Extensions gebruiken op Android-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Gebruik Microsoft Intune om Zebra-apparaten die worden uitgevoerd met Android te beheren en te gebruiken met Zebra Mobility Extensions (MX). Bekijk alle de stappen, waaronder de Bedrijfsportal-app installeren, de app sideloaden, de rol Apparaatbeheerder toewijzen, een StageNow-profiel maken en meer.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cb1d4917e94528dc64fa336df8eacc085a4d685c
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461977"
---
# <a name="use-and-manage-zebra-devices-with-zebra-mobility-extensions-in-microsoft-intune"></a>Zebra-apparaten gebruiken en beheren met Zebra Mobility Extensions in Microsoft Intune

Intune bevat een uitgebreide set functies, waaronder apps beheren en apparaatinstellingen configureren. Deze ingebouwde functies en instellingen worden gebruikt om Android-apparaten te beheren die zijn gemaakt door Zebra Technologies. Deze apparaten worden ook wel Zebra-apparaten genoemd.

Gebruik op Android-apparaten **Mobility Extensions (MX)** -profielen van Zebra om Zebra-specifieke instellingen aan te passen of toe te voegen.

In dit artikel wordt beschreven hoe u Zebra Mobility Extensions (MX) gebruikt op Zebra-apparaten in Microsoft Intune.

Deze functie is van toepassing op:

- Android-apparaatbeheerder

Gebruik [OEMConfig](android-oem-configuration-overview.md) voor Android Enterprise-apparaten.

Uw bedrijf kan gebruikmaken van Zebra-apparaten voor de detailhandel, op de werkvloer en meer. Stel dat u een detailhandelaar bent en de verkoopmedewerkers in uw omgeving duizenden mobiele Zebra-apparaten gebruiken. Met Intune kunt u deze apparaten beheren als onderdeel van uw Mobile Device Management-oplossing (MDM).

Met Intune kunt u Zebra-apparaten registreren om Line-Of-Business-apps te implementeren op apparaten. Met apparaatconfiguratieprofielen kunt u MX-profielen maken om uw Zebra-specifieke instellingen te beheren.

> [!NOTE]
> De Zebra MX-API's zijn standaard niet vergrendeld op apparaten. Voordat een apparaat in Intune wordt ingeschreven, is het mogelijk dat het apparaat op schadelijke wijze kan zijn gemanipuleerd. Wanneer het apparaat vrij is van eventuele problemen, wordt aanbevolen MX-API's te vergrendelen met behulp van Access Manager (AccessMgr). U kunt er bijvoorbeeld voor kiezen alleen de bedrijfsportal-app en apps die u vertrouwt, MX-API's te laten aanroepen.
>
> Zie [Uw apparaat vergrendelen](https://developer.zebra.com/community/home/blog/2017/04/11/locking-down-your-device) op de website van Zebra voor meer informatie.

## <a name="before-you-begin"></a>Voordat u begint

- Zorg ervoor dat u over de nieuwste versie van de StageNow-desktop-app van Zebra Technologies beschikt.
- Controleer de [Volledige functiematrix van Zebra](http://techdocs.zebra.com/mx/compatibility) (hiermee wordt de Zebra-website geopend) om te bevestigen dat de profielen die u maakt compatibel zijn met de MX-versie, de besturingssysteemversie en het model van het apparaat.
- Bepaalde apparaten, zoals TC20/25-apparaten, ondersteunen niet alle beschikbare MX-functies in StageNow. Controleer de [Functiematrix van Zebra](http://techdocs.zebra.com/mx/tc2x/) (hiermee wordt de Zebra-website geopend) voor bijgewerkte ondersteuningsinformatie.

## <a name="step-1-install-the-latest-company-portal-app"></a>Stap 1: De nieuwste Bedrijfsportal-app installeren

Open de Google Play Store op het apparaat. Download en installeer de Intune-bedrijfsportal-app van Microsoft. Na te zijn geïnstalleerd vanuit Google Play worden er automatisch updates en fixes in de Bedrijfsportal-app geïnstalleerd.

Als Google Play niet beschikbaar is, downloadt u de [Microsoft Intune-bedrijfsportal voor Android](https://www.microsoft.com/download/details.aspx?id=49140) (hiermee wordt een andere Microsoft-website geopend), en [sideloadt u de app](#sideload-the-company-portal-app) (in dit artikel). Wanneer de app op deze manier is geïnstalleerd, worden er niet automatisch updates en fixes in geïnstalleerd. Zorg er daarom voor dat u regelmatig handmatig updates en patches voor de app installeert.

### <a name="sideload-the-company-portal-app"></a>De Bedrijfsportal-app sideloaden

Sideloaden houdt in dat u niet gebruikmaakt van Google Play om een app te installeren. Gebruik StageNow om de Bedrijfsportal-app te sideloaden. 

De volgende stappen bevatten een overzicht. Zie de Zebra-documentatie voor specifieke details. [Enroll in an MDM using StageNow ](http://techdocs.zebra.com/stagenow/3-1/Profiles/enrollmdm/) (Registreren bij MDM met behulp van StageNow) (hiermee wordt de Zebra-website geopend) kan een goede resource zijn.

1. Maak in StageNow een profiel voor **Enroll in an MDM** (Registratie bij een MDM).
2. Kies er bij **Deployment** (Implementatie) voor om het MDM-agentbestand te downloaden.
3. Stel de stappen **Support App** (App ondersteunen) en **Download Configuration** (Configuratie downloaden) in op **No** (Nee).
4. Selecteer bij **Download MDM** (MDM downloaden) de optie **Transfer/Copy File** (Bestand overdragen/kopiëren). Voeg de bron en bestemming van het Bedrijfsportal Android-pakket (APK) toe.
5. Laat bij **Launch MDM** (MDM starten) de standaardwaarden staan. Voeg de volgende gegevens toe:

    - **Pakketnaam**: `com.microsoft.windowsintune.companyportal`
    - **Klassenaam**: `com.microsoft.windowsintune.companyportal.views.SplashActivity`

Ga door met het publiceren van het profiel en verbruik het met de app StageNow op het apparaat. De Bedrijfsportal-app wordt geïnstalleerd en geopend op het apparaat.

> [!TIP]
> Zie [StageNow Android device staging ](https://www.zebra.com/us/en/products/software/mobile-computers/mobile-app-utilities/stagenow.html) (Fasering van Android-apparaten via StageNow) (hiermee wordt de Zebra-website geopend) voor meer informatie over StageNow en wat het doet.

## <a name="step-2-confirm-the-company-portal-app-has-device-administrator-role"></a>Stap 2: Bevestigen dat de rol Apparaatbeheerder is toegekend aan de Bedrijfsportal-app

Voor de bedrijfsportal-app is Apparaatbeheerder vereist om Android-apparaten te beheren. Sommige Zebra-apparaten bieden een gebruikersinterface op het apparaat om de rol Apparaatbeheerder te activeren. Als het apparaat een gebruikersinterface bevat, wordt de eindgebruiker in de Bedrijfsportal-app gevraagd om de rol Apparaatbeheerder toe te kennen tijdens de [registratie](#step-3-enroll-the-device-in-to-intune) (in dit artikel).

Als er geen gebruikersinterface beschikbaar is, gebruikt u de **DevAdmin Manager** in StageNow om een profiel te maken waarin Apparaatbeheerder handmatig wordt toegekend aan de bedrijfsportal-app.

De volgende stappen bevatten een overzicht. Zie de Zebra-documentatie voor specifieke details. 
[Set battery swap mode as device administrator ](https://zebratechnologies.force.com/s/article/Set-Battery-Swap-Mode-as-Device-Administrator-using-StageNow-Tool) (Accuwisselmodus instellen als apparaatbeheerder) (hiermee wordt de Zebra-website geopend) kan een goede resource zijn.

1. Maak een profiel in StageNow en selecteer **Xpert Mode**.
2. Voeg **DevAdmin Manager** toe aan het profiel.
3. Stel **Device Administration Action** (Apparaatbeheeractie) in op **Turn On as Device Administrator** (Inschakelen als apparaatbeheerder).
4. Stel **Device Admin Package Name** (Naam van apparaatbeheerderspakket) in op `com.microsoft.windowsintune.companyportal`.
5. Stel **Device Admin Class Name** (Naam van apparaatbeheerdersklasse) in op `com.microsoft.omadm.client.PolicyManagerReceiver`.

Ga door met het publiceren van het profiel en verbruik het met de app StageNow op het apparaat. De rol Apparaatbeheerder is toegekend aan de Bedrijfsportal-app.

## <a name="step-3-enroll-the-device-in-to-intune"></a>Stap 3: Het apparaat registreren bij Intune

Na het voltooien van de eerste twee stappen is de Bedrijfsportal-app op het apparaat geïnstalleerd. Het apparaat is gereed om te worden geregistreerd bij Intune.

De stappen worden vermeld bij [Android-apparaten registreren](../enrollment/android-enroll.md). Als u veel Zebra-apparaten hebt, wilt u misschien gebruikmaken van een [beheeraccount voor apparaatregistratie](../enrollment/device-enrollment-manager-enroll.md). Met behulp van dit account wordt ook de optie om de registratie ongedaan te maken uit de Bedrijfsportal-app verwijderd, zodat gebruikers de registratie van het apparaat niet gemakkelijk ongedaan kunnen maken.

## <a name="step-4-create-a-device-management-profile-in-stagenow"></a>Stap 4: Een apparaatbeheerprofiel maken in StageNow

Gebruik StageNow om een profiel te maken waarmee u de instellingen die u wilt beheren op het apparaat configureert. Zie de Zebra-documentatie voor specifieke details. [Profiles](http://techdocs.zebra.com/stagenow/3-2/stagingprofiles/) (Profielen) (hiermee wordt de Zebra-website geopend) kan een goede resource zijn.

Bij het maken van het profiel in StageNow selecteert u bij de laatste stap **Export to MDM** (Exporteren naar MDM). Met deze stap wordt een XML-bestand gegenereerd. Sla dit bestand op. U hebt het nodig in een latere stap.

- Het is raadzaam om het profiel te testen voordat u het op apparaten in uw organisatie implementeert. Dit doet u door **Test**-opties te gebruiken in de laatste stap voor het maken van profielen met StageNow op uw computer. Verbruik het door StageNow gegenereerde bestand vervolgens met de StageNow-app op het apparaat.

  In de app StageNow op het apparaat worden de logboeken weergegeven die zijn gegenereerd toen u het profiel testte. [StageNow-logboeken gebruiken op Zebra-apparaten met Android in Intune](android-zebra-mx-logs-troubleshoot.md) bevat informatie over het gebruik van StageNow-logboeken om meer inzicht te krijgen in fouten.

- Als u naar apps verwijst, pakketten bijwerkt of andere bestanden bijwerkt in uw StageNow-profiel, wilt u dat deze updates op het apparaat terechtkomen. Het apparaat moet bij het toepassen van het profiel verbinding maken met de StageNow-implementatieserver om de updates te verkrijgen. 

  U kunt ook ingebouwde functies in Intune gebruiken om deze wijzigingen te verkrijgen, waaronder:

  - App-beheerfuncties voor het [toevoegen](../apps/apps-add.md), [implementeren](../apps/apps-deploy.md), bijwerken en [bewaken](../apps/apps-monitor.md) van apps.
  - [Systeem- en app-updates](device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile) beheren op Android Enterprise-apparaten

Nadat u het bestand hebt getest, bestaat de volgende stap uit het implementeren van het profiel op apparaten met behulp van Intune.

- U kunt een of meer MX-profielen op een apparaat implementeren.
- U kunt ook meerdere StageNow-profielen exporteren en de instellingen combineren in één XML-bestand. Upload vervolgens het XML-bestand naar Intune om dit bestand op uw apparaten te implementeren.

  > [!WARNING]
  > Als meerdere MX-profielen op dezelfde groep zijn gericht en dezelfde eigenschap wordt geconfigureerd, zullen zich conflicten voordoen op het apparaat.
  >
  > Als dezelfde eigenschap meerdere keren wordt geconfigureerd in één MX-profiel, heeft de laatste configuratie prioriteit.

## <a name="step-5-create-a-profile-in-intune"></a>Stap 5: Een profiel maken in Intune

Maak in Intune een apparaatconfiguratieprofiel:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het nieuwe profiel.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.
    - **Platform**: Selecteer **Android-apparaatbeheer**.
    - **Profieltype**: Selecteer **MX-profiel (alleen Zebra)** .

4. Voeg aan **MX-profiel in XML-indeling** het XML-profielbestand toe dat [u hebt geëxporteerd uit StageNow](#step-4-create-a-device-management-profile-in-stagenow) (in dit artikel).
5. Selecteer **OK** > **Maken** om uw wijzigingen op te slaan. Het beleid wordt gemaakt en in de lijst weergegeven.

    > [!TIP]
    > Uit veiligheidsoverwegingen wordt de profiel-XML-tekst niet meer weergegeven nadat u deze hebt opgeslagen. De tekst is versleuteld en u ziet alleen sterretjes (`****`). Ter referentie is het raadzaam om kopieën van de MX-profielen op te slaan voordat u deze aan Intune toevoegt.

Het profiel is gemaakt, maar er gebeurt nog niets. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

De volgende keer dat op het apparaat wordt gecontroleerd of er configuratieupdates zijn, wordt het MX-profiel op het apparaat geïmplementeerd. Apparaten worden met Intune gesynchroniseerd tijdens de apparaatregistratie en vervolgens ongeveer elke acht uur. U kunt ook [synchronisatie afdwingen in Intune](../remote-actions/device-sync.md). Of u gaat op het apparaat naar **Bedrijfsportal-app** > **Instellingen** > **Synchroniseren**. 

## <a name="update-a-zebra-mx-configuration-after-its-assigned"></a>Een Zebra MX-configuratie bijwerken nadat deze is toegewezen

Als u de specifieke MX-configuratie van een Zebra-apparaat wilt bijwerken, kunt u: 

- Een bijgewerkt StageNow XML-bestand maken, het bestaande Intune MX-profiel bewerken en het nieuwe StageNow XML-bestand uploaden. Met dit nieuwe bestand wordt het vorige beleid in het profiel overschreven en wordt de vorige configuratie vervangen.
- Een nieuw StageNow XML-bestand maken waarmee verschillende instellingen worden geconfigureerd, een nieuw Intune MX profiel maken, het nieuwe StageNow XML-bestand uploaden en dit toewijzen aan dezelfde groep. Er worden meerdere profielen geïmplementeerd. Als met het nieuwe profiel instellingen worden geconfigureerd die al in bestaande profielen aanwezig zijn, treden conflicten op.

## <a name="next-steps"></a>Volgende stappen

- [Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).
- [StageNow Logboeken gebruiken om problemen op Zebra-apparaten op te lossen](android-zebra-mx-logs-troubleshoot.md).

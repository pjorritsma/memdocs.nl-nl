---
title: Apparaten inschrijven in Desktop Analytics
titleSuffix: Configuration Manager
description: Meer informatie over het inschrijven van apparaten in Desktop Analytics.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 22b5461df3a560449316009471ea029967118f5d
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864890"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Apparaten inschrijven in Desktop Analytics

Wanneer u [Configuration Manager verbinding maakt](connect-configmgr.md) met Desktop Analytics, configureert u instellingen voor het registreren van apparaten bij Desktop Analytics. U kunt deze instellingen op elk gewenst moment wijzigen. Zorg er ook voor dat de apparaten up-to-date zijn.

## <a name="update-devices"></a>Apparaten bijwerken

Desktop Analytics maakt gebruik van twee hoofd Windows-onderdelen:

- **Compatibiliteits onderdeel**: met het compatibiliteits onderdeel (**evaluatie**versie) wordt Diagnostische gegevens op het Windows-apparaat uitgevoerd om de compatibiliteits status te evalueren met de nieuwste versies van Windows 10.

- **Verbonden gebruikers ervaringen en telemetrie-service**: met de diagnostische gegevens van Windows ingeschakeld, de verbonden gebruikers ervaring en de telemetrie-service (**DiagTrack**) verzamelt systeem-, toepassings-en stuur programma-gegevens. Micro soft analyseert deze gegevens en deelt deze weer aan u via desktop Analytics.

Installeer de nieuwste versie van deze onderdelen om de beste ervaring met Desktop Analytics te krijgen.

De volgende tabel geeft een overzicht van de updates voor elk onderdeel op ondersteunde versies van besturings systemen:

| Besturingssysteemversie | Beoordeling | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | Opgenomen <sup> [Opmerking 1](#bkmk_note1)</sup> | [Meest recente cumulatieve update](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | Opgenomen <sup> [Opmerking 1](#bkmk_note1)</sup> | [Meest recente cumulatieve update](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | Opgenomen <sup> [Opmerking 1](#bkmk_note1)</sup> | [Meest recente cumulatieve update](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | Opgenomen <sup> [Opmerking 1](#bkmk_note1)</sup> | [Meest recente cumulatieve update](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | Opgenomen <sup> [Opmerking 1](#bkmk_note1)</sup> | [Meest recente cumulatieve update](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978) <sup> [Opmerking 2](#bkmk_note2)</sup> | [Meest recente maandelijkse Rollup](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) <sup> [Opmerking 3](#bkmk_note3)</sup> | [Meest recente maandelijkse Rollup](https://support.microsoft.com/help/4009469) |

> [!TIP]
> Gebruik Configuration Manager om deze updates automatisch te installeren. Zie [software-updates implementeren](../sum/deploy-use/deploy-software-updates.md)voor meer informatie.
>
> Apparaten opnieuw opstarten nadat u de compatibiliteits updates voor de eerste keer hebt geïnstalleerd.

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a>Opmerking 1: Windows 10

Hoewel Windows 10 deze onderdelen bevat, is voor Windows 10-apparaten standaard de meest recente cumulatieve update nodig om de volledige functionaliteit van Desktop Analytics te krijgen, zoals het evalueren van het apparaat voor compatibiliteit met de meest recente versie van het besturings systeem.

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a>Opmerking 2: Windows 8,1

Micro soft verhoogt regel matig de updates voor dit onderdeel, maar het bijbehorende KB-nummer wordt niet gewijzigd. Zorg ervoor dat u altijd over de meest recente versie van de update beschikt.

Dit onderdeel voert diagnostische gegevens uit op Windows 8,1-systemen die deel uitmaken van de Windows-Customer Experience Improvement Program. Deze diagnostische gegevens helpen te bepalen of u compatibiliteits problemen ondervindt bij het uitvoeren van een upgrade naar Windows 10.

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a>Opmerking 3: Windows 7

Als uw organisatie geen updates voor de maandelijkse kwaliteit van Windows 7-apparaten toepast en alleen updates voor alleen beveiliging toepast, vindt u enkele beveiligings updates in de [lijst met updates die zijn vervangen door KB 2952664](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c). U kunt deze nieuwere updates installeren in plaats van KB 2952664.

> [!NOTE]
> Voor Windows 8,1 reviseert micro soft alleen KB 2976978 als onderdeel van de updates voor het totaliseren van de maandelijkse kwaliteit.

## <a name="device-enrollment"></a>Apparaatinschrijving

De service desktop Analytics heeft geen agents om te installeren. Voor het inschrijven van apparaten moet u instellingen configureren op de apparaten die u wilt bewaken. Deze instellingen bepalen aan welk Desktop Analytics-exemplaar de gegevens moeten worden verzonden en andere configuratie opties.

> [!Note]  
> Als u eerder Windows Analytics hebt gebruikt, gebruikt u diezelfde werk ruimte voor desktop Analytics. U moet apparaten opnieuw inschrijven voor desktop Analytics die u eerder hebt geregistreerd in Windows Analytics.
>
> U kunt slechts één desktop Analytics-werk ruimte hebben per Azure AD-Tenant. Apparaten kunnen alleen diagnostische gegevens verzenden naar één werk ruimte.  

Configuration Manager biedt een geïntegreerde ervaring voor het beheren en implementeren van deze instellingen voor clients. Gebruik Configuration Manager voor de beste ervaring.

Wanneer u Configuration Manager verbinding maakt met Desktop Analytics, configureert u de instellingen voor het inschrijven van apparaten. Zie [How to connect Configuration Manager with Desktop Analytics](connect-configmgr.md#bkmk_connect)(Engelstalig) voor meer informatie.

Als u deze instellingen wilt wijzigen, gebruikt u de volgende procedure:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure-Services** . Selecteer de verbinding met Desktop Analytics en kies **Eigenschappen** in het lint.

2. Breng op de pagina **Diagnostische gegevens** de gewenste wijzigingen aan in de volgende instellingen:  

    - **Commerciële id**: deze waarde moet automatisch worden ingevuld met de id van uw organisatie. Als dat niet het geval is, moet u ervoor zorgen dat de proxy server zo is geconfigureerd dat alle vereiste [eind punten](enable-data-sharing.md#endpoints) worden toegestaan voordat u doorgaat. U kunt uw commerciële ID ook hand matig ophalen via de [Desktop Analytics-Portal](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Niveau van diagnostische gegevens voor Windows 10**: Zie [Diagnostische gegevens niveaus](enable-data-sharing.md#diagnostic-data-levels)voor meer informatie.  

    - **Apparaatnaam in diagnostische gegevens toestaan**: Zie de naam van het [apparaat](#device-name)voor meer informatie.  

    Wanneer u wijzigingen aanbrengt op deze pagina, toont de pagina **beschik bare functionaliteit** een voor beeld van de functionaliteit van het bureau blad Analytics met de geselecteerde instellingen voor diagnostische gegevens.  

3. Breng op de pagina **verbinding met bureau blad Analytics** zo nodig wijzigingen aan in de volgende instellingen:

    - **Weergave naam**: de bureau blad Analytics-portal geeft deze Configuration Manager verbinding weer met behulp van deze naam.  

    - **Doel verzameling**: deze verzameling bevat alle apparaten die Configuration Manager configureert met de instellingen voor uw commerciële id en diagnostische gegevens. Het is de volledige set apparaten waarmee Configuration Manager verbinding maakt met de Desktop Analytics-service.  

    - **Apparaten in de doel verzameling gebruiken een door de gebruiker geverifieerde proxy voor uitgaande communicatie**: deze waarde is standaard ingesteld op **Nee**. Stel dit in op **Ja**als dat nodig is in uw omgeving. Zie verificatie van de [proxy server](enable-data-sharing.md#proxy-server-authentication)voor meer informatie.

    - **Specifieke verzamelingen selecteren om te synchroniseren met Desktop Analytics**: Selecteer **toevoegen** om extra verzamelingen te gebruiken uit de hiërarchie van de **doel verzameling** . Deze verzamelingen zijn beschikbaar in de Desktop Analytics-Portal om te groeperen met implementatie plannen. Zorg ervoor dat u verzamelingen van pilot-en pilot-uitsluitingen opneemt.  <!-- 4097528 -->

        > [!IMPORTANT]
        > Deze verzamelingen blijven synchroniseren wanneer hun lidmaatschap wordt gewijzigd. Uw implementatie plan gebruikt bijvoorbeeld een verzameling met een lidmaatschaps regel voor Windows 7. Als deze apparaten worden bijgewerkt naar Windows 10 en Configuration Manager het lidmaatschap van de verzameling evalueert, worden deze apparaten uit het verzamelings-en implementatie plan verwijderd.

### <a name="windows-settings"></a>Windows-instellingen

Wanneer Configuration Manager apparaten registreert bij Desktop Analytics, wordt het Windows-beleid ingesteld voor het configureren van het apparaat voor desktop Analytics. In de meeste gevallen gebruikt u Configuration Manager voor het configureren van deze instellingen. Deze instellingen zijn niet ook van toepassing op domein groeps beleidsobjecten.

Zie voor meer informatie [groeps beleids instellingen voor desktop Analytics](group-policy-settings.md).

### <a name="device-name"></a>Apparaatnaam

Vanaf Windows 10, versie 1803, wordt de naam van het apparaat niet standaard verzameld. Het verzamelen van de apparaatnaam met de diagnostische gegevens vereist een afzonderlijke opt-in. Zonder de naam van het apparaat is het moeilijker om te bepalen welke apparaten aandacht vereisen tijdens het evalueren van een upgrade naar een nieuwe versie van Windows.

Als u de apparaatnaam niet verzendt, wordt deze in Desktop Analytics weer gegeven als ' onbekend ':

![Lijst met apparaten in het bureau blad Analytics met de naam ' onbekend '](media/unknown-device-name.png)

Er is een optie in de Configuration Manager instellingen voor desktop Analytics voor het configureren van deze optie: **apparaatnaam in diagnostische gegevens toestaan**. Met deze Configuration Manager instelling bepaalt u de [Windows-beleids instelling](group-policy-settings.md) **AllowDeviceNameInTelemetry**.

### <a name="conflict-resolution"></a>Conflictoplossing

In het algemeen gebruikt u Configuration Manager verzamelingen om instellingen en registraties voor desktop Analytics te richten. Gebruik direct lidmaatschap of query's om apparaten op te nemen of uit te sluiten van de verzameling. Zie [verzamelingen maken](../core/clients/manage/collections/create-collections.md)voor meer informatie.

Configuration Manager configureert alleen de Windows-instellingen als er nog geen waarde bestaat. Als u verschillende instellingen voor een unieke groep apparaten wilt configureren, kunt u [groeps beleid](group-policy-settings.md)gebruiken. Instellingen die zijn gericht op groeps beleid hebben voor rang op Configuration Manager instellingen. Apparaten waarop groeps beleid is gericht, geven mogelijk niet de juiste status weer in het dash board voor [verbindings status](monitor-connection-health.md) .

Wanneer u het niveau van de diagnostische gegevens configureert, stelt u de bovenste grens voor het apparaat in. In Windows 10 versie 1803 en hoger kunnen gebruikers ervoor kiezen om een lager niveau in te stellen. U kunt dit gedrag best uren met behulp van de groeps beleids instelling, de **optie voor het instellen van telemetrie configureren van de gebruikers interface**. Zie voor meer informatie [groeps beleids instellingen voor desktop Analytics](group-policy-settings.md).

### <a name="proxy-settings"></a>Proxyinstellingen

Als uw organisatie verificatie van de proxy server gebruikt voor Internet toegang, moet u ervoor zorgen dat deze correct wordt geconfigureerd of uw apparaten. Zie verificatie van de [proxy server](enable-data-sharing.md#proxy-server-authentication)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

Ga naar het volgende artikel voor het maken van implementatie plannen in Desktop Analytics.
> [!div class="nextstepaction"]
> [Implementatieplannen maken](create-deployment-plans.md)

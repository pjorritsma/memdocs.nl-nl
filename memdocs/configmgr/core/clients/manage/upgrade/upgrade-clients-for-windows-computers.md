---
title: Clients in Windows bijwerken
titleSuffix: Configuration Manager
description: Clients op Windows-computers bijwerken in Configuration Manager.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b0a69b07a3be633434203f93b0724cec4ea88a3
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347135"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>Clients voor Windows-computers bijwerken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voer een upgrade uit van de Configuration Manager-client op Windows-computers met behulp van client installatie methoden of de functie voor automatische client upgrade. De volgende clientinstallatiemethoden zijn geldige manieren om de clientsoftware op Windows-computers bij te werken:  

- Installatie van Groepsbeleid  

- Aanmeldingscriptinstallatie  

- Handmatige installatie  

- Upgrade-installatie  

Zie [clients implementeren op Windows-computers](../../deploy/deploy-clients-to-windows-computers.md)voor meer informatie.

Clients uitsluiten van een upgrade door een uitsluitings verzameling op te geven. Zie voor meer informatie [clients uitsluiten van upgrade](exclude-clients-windows.md). Uitgesloten clients worden nog steeds gedownload en uitvoeren CCMSETUP, maar kunnen niet worden bijgewerkt.

> [!TIP]  
> Als u een upgrade van uw server infrastructuur uitvoert van een eerdere versie van Configuration Manager, voltooit u de server upgrades voordat u de Configuration Manager-clients bijwerkt. Dit proces omvat het installeren van alle updates van de huidige branch. De meest recente update van de huidige branch bevat de meest recente versie van de client. Upgrade clients nadat u alle Configuration Manager-updates hebt geïnstalleerd.

> [!NOTE]
> Als u van plan bent om de-site opnieuw toe te wijzen voor de clients tijdens de upgrade, geeft u de nieuwe site op met behulp van de `SMSSITECODE` client. msi-eigenschap. Als u de waarde van `AUTO` voor de `SMSSITECODE` opgeeft, moet u ook opgeven `SITEREASSIGN=TRUE` . Met deze eigenschap kan automatische site toewijzing tijdens de upgrade worden uitgevoerd. Zie [Eigenschappen van client installatie-SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode)voor meer informatie.

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a>Over automatische client upgrade

Configureer de site zo dat clients automatisch worden bijgewerkt naar de nieuwste versie van Configuration Manager. Wanneer Configuration Manager identificeert dat een toegewezen client versie eerder is dan de versie van de hiërarchie, wordt de client automatisch bijgewerkt. Dit scenario omvat het bijwerken van de client naar de meest recente versie wanneer deze probeert toe te wijzen aan een Configuration Manager-site.  

Een client kan automatisch worden bijgewerkt in de volgende scenario's:  

- De versie van de client is ouder dan de versie die in de hiërarchie wordt gebruikt.  

- Op de client op de centrale beheer site (CAS) is een taal pakket geïnstalleerd en de bestaande client is niet aanwezig.  

- Een vereiste voor een client in de hiërarchie heeft een verschillende versie dan de op de client geïnstalleerde.  

- Een of meer clientinstallatiebestanden hebben een verschillende versie.  

> [!NOTE]  
> Als u de verschillende versies van de Configuration Manager-client in uw hiërarchie wilt identificeren, gebruikt u het rapport **aantal Configuration Manager clients op client versies** in de rapportmap **site-client gegevens**.  

Configuration Manager maakt standaard een upgrade pakket. Het pakket wordt automatisch naar alle distributie punten in de hiërarchie verzonden. Als u wijzigingen aanbrengt in het client pakket op de CAS, Configuration Manager het pakket automatisch bijgewerkt en wordt het opnieuw gedistribueerd. Een voor beeld van een wijziging is wanneer u een client taal pakket toevoegt. Als u automatische client upgrade inschakelt, installeert elke client automatisch het nieuwe client taal pakket.

Schakel automatische client upgrade in in uw hiërarchie. Met deze configuratie blijven uw clients up-to-date met minder inspanning.  

Als u uw Configuration Manager-site systemen ook beheert als clients, moet u bepalen of u deze wilt opnemen als onderdeel van het automatische upgrade proces. U kunt alle servers of een specifieke verzameling uitsluiten van de client upgrade. Sommige Configuration Manager site rollen delen het client-Framework. Bijvoorbeeld het beheer punt en het pull-distributie punt. Deze rollen worden bijgewerkt wanneer u de site bijwerkt, zodat de client versie op deze servers op hetzelfde moment wordt bijgewerkt.

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a>Automatische client upgrade configureren

Gebruik de volgende procedure voor het configureren van een automatische client upgrade op de CAS. Deze configuratie is van toepassing op alle clients in uw hiërarchie.  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer vervolgens het knoop punt **sites** .  

1. Selecteer **hiërarchie-instellingen**op het tabblad **Start** van het lint in de groep **sites** .  

1. Schakel over naar het tabblad **client upgrade** . Controleer de versie en de datum van de productie-client. Zorg ervoor dat dit de versie is die u wilt gebruiken om uw clients bij te werken. Als dat niet de client versie is die u verwacht, moet u mogelijk de pre-production-client verhogen naar productie. Zie [Client upgrades testen in een pre-productie verzameling](test-client-upgrades.md)voor meer informatie.  

1. Selecteer **upgrade uitvoeren voor alle clients in de hiërarchie met behulp van de productie-client**. Selecteer **OK** om te bevestigen.  

1. Als u niet wilt dat client upgrades worden toegepast op servers, selecteert u **servers niet upgraden**.  

1. Geef het aantal dagen op waarin apparaten de client moeten upgraden. Nadat het apparaat beleid heeft ontvangen, wordt de client met een wille keurig interval binnen dit aantal dagen bijgewerkt. Dit gedrag voor komt dat een groot aantal clients tegelijkertijd upgradet.

    > [!NOTE]
    > Er moet een computer worden uitgevoerd om de client bij te werken. Als een computer niet actief is op het moment dat de upgrade wordt ontvangen, wordt de upgrade niet uitgevoerd. Wanneer de computer wordt ingeschakeld en het beleid wordt ontvangen, wordt de upgrade voor een wille keurige tijd gepland binnen het toegestane aantal dagen. Als dit gebeurt nadat het aantal dagen voor de upgrade is verlopen, wordt de upgrade op een wille keurige tijd gepland binnen 24 uur nadat de computer is ingeschakeld.
    >
    > Vanwege dit gedrag kan het upgraden van computers die regel matig worden afgesloten, langer duren dan verwacht als de tijd van de wille keurige geplande upgrade zich niet in de normale werk uren bevindt.

1. Als u clients wilt uitsluiten van de upgrade, selecteert u **opgegeven clients uitsluiten van upgrade**en geeft u de verzameling op die moet worden uitgesloten. Zie [clients uitsluiten van upgrade](exclude-clients-windows.md)voor meer informatie.

1. Als u wilt dat de site het client installatie pakket kopieert naar distributie punten die u hebt ingeschakeld voor voor [bereide inhoud](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent), selecteert u de optie voor het **automatisch distribueren van client installatie pakketten naar distributie punten die zijn ingeschakeld voor voor bereide inhoud**.  

1. Selecteer **OK** om de instellingen op te slaan en de eigenschappen van de hiërarchie-instellingen te sluiten.

Clients ontvangen deze instellingen wanneer ze de volgende keer het beleid downloaden.

> [!NOTE]
> Bij Client upgrades worden Configuration Manager onderhouds Vensters geaccepteerd die u hebt geconfigureerd. De execmgr-thread voert alleen de client installatie Boots trap programma (ccmsetup. exe) uit tijdens een onderhouds venster. Als op het apparaat een Windows-editie met een schrijf filter wordt uitgevoerd, probeert ccmsetup tegelijkertijd te downloaden en te installeren. Anders is ccmsetup wille keurig een tijd om inhoud te downloaden. Nadat de inhoud is gedownload en het lokale beleid is gecompileerd, wordt de client upgrade door execmgr gepland tijdens het volgende onderhouds venster.<!-- SCCMDocs#896 -->

## <a name="next-steps"></a>Volgende stappen

Zie [clients implementeren op Windows-computers](../../deploy/deploy-clients-to-windows-computers.md)voor alternatieve methoden voor het bijwerken van clients.

Specifieke clients uitsluiten van automatische upgrade. Zie voor meer informatie [clients uitsluiten van upgrade](exclude-clients-windows.md).

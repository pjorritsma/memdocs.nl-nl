---
title: Serviceverbindingspunt
titleSuffix: Configuration Manager
description: Meer informatie over deze Configuration Manager-site systeemrol en het bereik van het gebruik ervan begrijpen en plannen.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721183"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Over het service aansluitpunt in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het service verbindings punt is een site systeemrol die verschillende belang rijke functies voor de hiërarchie biedt. Voordat u het service aansluitpunt instelt, begrijpt en plant u het bereik van het gebruik. Het plannen van het gebruik kan van invloed zijn op hoe u deze site systeemrol instelt:

- Down load updates die van toepassing zijn op uw Configuration Manager-infra structuur. Alleen relevante updates voor uw infra structuur worden beschikbaar gesteld op basis van de gebruiks gegevens die u uploadt.

- Upload gebruiks gegevens van uw Configuration Manager-infra structuur. U kunt het niveau of de hoeveelheid details beheren die u uploadt. Zie [gebruiks gegevens niveaus en instellingen](../install/setup-reference.md#bkmk_usage)voor meer informatie.

- Een [Cloud beheer gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md) in azure implementeren

- Apps synchroniseren met de [Microsoft Store voor bedrijven en onderwijs](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)

- Gebruikers en groepen in [Azure Active Directory ontdekken (Azure AD)](about-discovery-methods.md#azureaddisc)

- Gebruik [Desktop Analytics](../../../../desktop-analytics/overview.md) om inzicht te krijgen in Windows 10-update en app-gereedheid

Elke hiërarchie ondersteunt één exemplaar van deze rol. Het kan alleen worden geïnstalleerd op de bovenste site van uw hiërarchie. Dit is een centrale beheer site (CAS) of een zelfstandige primaire site. Als u een zelfstandige primaire site uitbreidt naar een grotere hiërarchie, verwijdert u deze rol van de primaire site en installeert u deze op de CAS.

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a>Bewerkings modi

Het serviceverbindingspunt ondersteunt twee bewerkingsmodi:

- **Online**: het service aansluitpunt controleert automatisch elke 24 uur op updates. Er worden nieuwe updates gedownload die beschikbaar zijn voor uw huidige infra structuur en product versie om ze beschikbaar te maken in de Configuration Manager-console.

- **Offline**: het service verbindings punt maakt geen verbinding met de micro soft-Cloud service. Gebruik het [hulp programma voor service verbindingen](../../manage/use-the-service-connection-tool.md)om hand matig beschik bare updates te importeren.

### <a name="change-mode"></a>Modus wijzigen

Als u wijzigingen aanbrengt tussen de online-of offline modus nadat u het service verbindings punt hebt geïnstalleerd, start u de **SMS_DMP_DOWNLOADER** -thread van de SMS_Executive-service opnieuw. Als deze thread opnieuw wordt gestart, wordt de wijziging van kracht. Gebruik de Configuration Manager Service Manager om deze thread opnieuw op te starten.

> [!TIP]
> U kunt ook de SMS_Executive-service opnieuw starten voor Configuration Manager, waardoor de meeste site onderdelen opnieuw worden gestart. U kunt ook wachten op een geplande taak, zoals een site back-up, waarmee de SMS_Executive-service voor u wordt gestopt en opnieuw wordt gestart.

Als u de Configuration Manager Service Manager wilt gebruiken om de SMS_DMP_DOWNLOADER-thread opnieuw te starten:

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **systeem status**uit en selecteer het knoop punt **onderdeel status** . Kies in het lint **Start**en selecteer vervolgens **Configuration Manager Service Manager**.

1. Vouw in het navigatie deel venster Service Manager de site uit, vouw **onderdelen**uit en kies vervolgens het onderdeel dat u opnieuw wilt starten: **SMS_DMP_DOWNLOADER**.

1. Ga naar het **onderdeel** menu en kies **query**.

1. Bevestig de huidige status van het onderdeel. Ga vervolgens naar het menu **onderdeel** en klik op **stoppen**.  

1. **Vraag** het onderdeel opnieuw aan om te bevestigen dat het is gestopt. Kies vervolgens de actie onderdeel **starten** om het opnieuw te starten.

## <a name="remote-site-system-requirements"></a>Systeem vereisten voor externe site

Wanneer u het service aansluitpunt installeert op een site systeem server die zich op afstand van de site server bevinden, configureert u de volgende vereisten:

- Het computer account van de site server moet een lokale beheerder zijn op de computer die als host fungeert voor een extern service verbindings punt.

- Stel de site systeem server in die als host fungeert voor deze rol met een [installatie account van een site systeem](../../../plan-design/hierarchy/accounts.md#site-system-installation-account). Distribution Manager op de site server gebruikt het installatie account van het site systeem om updates van het service verbindings punt over te dragen.

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a>Vereisten voor Internet toegang

Als uw organisatie netwerk communicatie met Internet beperkt met behulp van een firewall of proxy apparaat, moet u het service verbindings punt toestaan om toegang te krijgen tot internet-eind punten.

Zie [vereisten voor Internet toegang](../../../plan-design/network/internet-endpoints.md#bkmk_scp)voor meer informatie.

## <a name="install"></a>Installeren

Wanneer u **Setup** uitvoert om de site op de bovenste laag van een hiërarchie te installeren, kunt u het service verbindings punt installeren.

Nadat Setup is uitgevoerd, of als u de rol opnieuw wilt installeren, gebruikt u de wizard **site systeem rollen toevoegen** of de wizard **site systeem server maken** . (Installeer alleen het service aansluitpunt op de bovenste site van uw hiërarchie.) Zie [site systeem rollen installeren](install-site-system-roles.md)voor meer informatie.

## <a name="move-the-role"></a><a name="bkmk_move"></a>De rol verplaatsen

<!-- SCCMDocs#922 -->
Er zijn verschillende scenario's waarin u het service verbindings punt mogelijk moet verplaatsen naar een andere server:

- [Herstel](../../manage/recover-sites.md)
- [Siteserver met hoge beschikbaarheid](site-server-high-availability.md)
- [Site-uitbrei ding](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

Nadat u het service verbindings punt hebt verplaatst, controleert u alle site functies. Het is bijvoorbeeld mogelijk dat u de geheime sleutel moet vernieuwen voor verbindingen met Azure Active Directory-tenants (Azure AD). Zie [geheime sleutel vernieuwen](azure-services-wizard.md#bkmk_renew)voor meer informatie.

## <a name="log-files"></a>Logboekbestanden

Als u informatie wilt weer geven over uploads naar micro soft, bekijkt u de **Dmpuploader. log** op de server waarop het service verbindings punt wordt uitgevoerd. Bekijk de voortgang van het downloaden van updates in **Dmpdownloader. log**. Zie [logboek bestanden-service verbindings punt](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog)voor een volledige lijst met logboeken die betrekking hebben op het service verbindings punt.

## <a name="next-steps"></a>Volgende stappen

Gebruik de volgende stroom diagrammen om inzicht te krijgen in de proces stroom-en sleutel logboek vermeldingen. Dit proces omvat update downloads en replicatie van updates voor andere sites.

- [Stroomdiagram: updates downloaden](../../manage/download-updates-flowchart.md)

- [Stroomdiagram: updatereplicatie](../../manage/update-replication-flowchart.md)

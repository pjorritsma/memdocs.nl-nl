---
title: Zelfstandige media gebruiken om Windows te implementeren
titleSuffix: Configuration Manager
description: Gebruik zelfstandige media in Configuration Manager om Windows te implementeren waarbij band breedte beperkt is tot een optie om computers te vernieuwen, te installeren of bij te werken.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51b39e450fb5f8ffd7d83b4122d7514489383dfb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124649"
---
# <a name="use-standalone-media-to-deploy-windows-without-using-the-network"></a>Zelfstandige media gebruiken om Windows te implementeren zonder gebruik van het netwerk

*Van toepassing op: Configuration Manager (huidige vertakking)*

Zelfstandige media in Configuration Manager bevatten alles wat u nodig hebt om een besturings systeem op een computer te implementeren. Het medium bevat de opstart installatie kopie, de installatie kopie van het besturings systeem, het taken reeks beleid, toepassingen, stuur Programma's en meer. Met implementaties met zelfstandige media kunt u besturings systemen implementeren in de volgende situaties:

- In omgevingen waar het niet praktisch is om een installatie kopie van een besturings systeem of andere grote pakketten over het netwerk te kopiëren.

- In omgevingen zonder netwerk verbinding of netwerk verbinding met een lage band breedte.

Gebruik zelfstandige media in de volgende implementatie scenario's voor besturings systemen:

- [Een bestaande computer vernieuwen met een nieuwe versie van Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)

- [Windows bijwerken naar de laatste versie](upgrade-windows-to-the-latest-version.md)

Voer de stappen in een van deze scenario's voor implementatie van het besturings systeem uit. Gebruik vervolgens de volgende secties om de zelfstandige media voor te bereiden en te maken.

## <a name="unsupported-task-sequence-actions"></a>Niet-ondersteunde taken reeks acties

Wanneer u zelfstandige media gebruikt, ondersteunt Configuration Manager de volgende acties in de taken reeks niet:

- De stap [Stuur Programma's automatisch Toep assen](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) . Automatische toepassing van apparaatstuurprogramma's uit de stuurprogrammacatalogus wordt niet ondersteund. Als u een specifieke set stuur Programma's beschikbaar wilt maken voor Windows Setup, gebruikt u de stap [Stuur programmapakket Toep assen](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) .

- Installatie van software-updates.

- Software installeren voordat het besturings systeem wordt geïmplementeerd.

- Gebruikers koppelen aan de doel computer voor affiniteit tussen gebruikers en apparaten.

- Dynamisch pakket wordt geïnstalleerd met de stap [pakket installeren](../understand/task-sequence-steps.md#BKMK_InstallPackage) .

- Dynamische toepassing wordt geïnstalleerd met de stap [toepassing installeren](../understand/task-sequence-steps.md#BKMK_InstallApplication) .

> [!NOTE]
> Als uw taken reeks voor het implementeren van een besturings systeem de stap **pakket installeren** bevat en u de zelfstandige media op een centrale beheer site (CAS) maakt, kan er een fout optreden. De certificerings instanties beschikken niet over het benodigde beleid voor client configuratie om de Software Distribution agent in te scha kelen wanneer de taken reeks wordt uitgevoerd. De volgende fout kan worden weer gegeven in het bestand **CreateTsMedia. log** :
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>
> Voor zelfstandige media met de stap **pakket installeren** maakt u de zelfstandige media op een primaire site waarop de agent voor software distributie is ingeschakeld
>
> U kunt ook de taken reeks bewerken om een stap [opdracht regel uitvoeren](../understand/task-sequence-steps.md#BKMK_RunCommandLine) toe te voegen na de stap [Windows en ConfigMgr installeren](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) . Met deze **opdracht regel** stap voert u de volgende WMI-opdracht uit om de Software Distribution agent in te scha kelen voordat de eerste stap **pakket installeren** wordt uitgevoerd:
>
> ```command
> WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
> ```

## <a name="configure-deployment-settings"></a>Implementatie-instellingen configureren

Wanneer u zelfstandige media gebruikt om het implementatie proces van het besturings systeem te starten, moet u de implementatie configureren om het besturings systeem beschikbaar te stellen voor media. Selecteer op de pagina **implementatie-instellingen** van de implementatie een van de volgende opties voor de instelling **beschikbaar maken voor de volgende** :

- Configuration Manager-clients, media en PXE

- Alleen media en PXE

- Alleen media en PXE (verborgen)

## <a name="create-the-standalone-media"></a>De zelfstandige media maken

U kunt opgeven of de zelfstandige media een USB-flash station of een CD/DVD-set is. De computer die de media start, moet ondersteuning bieden voor de optie die u kiest als een opstartbaar station. Zie [zelfstandige media maken](create-stand-alone-media.md)voor meer informatie.

## <a name="install-the-os-from-standalone-media"></a>Het besturings systeem installeren vanaf zelfstandige media

Als u het besturings systeem wilt installeren, plaatst u het zelfstandige medium op de computer en schakelt u het vervolgens in.

## <a name="next-steps"></a>Volgende stappen

[Gebruikerservaring voor implementatie van besturingssysteem](../understand/user-experience.md#task-sequence-wizard)

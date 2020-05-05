---
title: Uw account sluiten
titleSuffix: Configuration Manager
description: Desktop Analytics verwijderen uit uw Azure-account
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e1d031588100f3930bf5bf25970f544b91017d77
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722520"
---
# <a name="how-to-close-your-account"></a>Uw account sluiten

Als u Desktop Analytics in uw omgeving instelt en vervolgens besluit dat u deze moet verwijderen, gebruikt u dit proces om uw account te sluiten.

## <a name="prerequisites"></a>Vereisten

Alleen een **globale beheerder** kan het account sluiten of opnieuw activeren in de Azure Portal.

## <a name="process-to-offboard"></a>Naar niet meer vrijgeven verwerken

1. Open de [Portal voor desktop Analytics](https://aka.ms/desktopanalytics) in Microsoft 365 Apparaatbeheer als gebruiker met de rol **globale beheerder** .

1. Selecteer in het menu **globale instellingen** de optie **verbonden services**. Selecteer in de sectie apparaten inschrijven de optie **niet meer vrijgeven**.

1. Als u besluit om door te gaan, wordt uw account gesloten.

> [!Important]
> Ga na 90 dagen pas verder met de rest van dit artikel of als u het niet opnieuw activeert.
>
> Als je je account volledig wilt sluiten zonder 90 dagen te wachten, moet je je account eerst [opnieuw instellen](account-reset.md) .

## <a name="reactivate"></a>Opnieuw activeren

Elke beheerder van uw organisatie die toegang heeft tot de Desktop Analytics-Portal, ziet de volgende 90 dagen een bericht dat u niet meer vrijgeven hebt gekozen.

Een globale beheerder kan het account binnen 90 dagen opnieuw activeren. Als u Desktop Analytics voor uw organisatie wilt herstellen, selecteert u de optie om **terug te gaan**.

## <a name="delete-the-solution"></a>De oplossing verwijderen

> [!Warning]
> Ga na 90 dagen pas verder met de rest van dit artikel of als u het niet opnieuw activeert. Als u deze andere onderdelen verwijdert en verbreekt, probeert u niet opnieuw te activeren.

1. Meld u aan bij de [Azure Portal](https://portal.azure.com) als gebruiker met de rol **globale beheerder** .

1. Zoek in **alle resources** naar de naam van de werk ruimte van uw bureau blad-analyse. Deze naam is wat u hebt gemaakt toen u zich aanmeldt voor de service.

1. Verwijderen `Microsoft365Analytics(YourWorkspaceName)` van de type **oplossing**.

De gegevens van het Desktop Analytics vallen op basis van het Bewaar beleid voor gegevens voor de werk ruimte. U kunt alle andere oplossingen in dezelfde werk ruimte blijven gebruiken.

> [!Important]  
> Als u de Log Analytics-werk ruimte met andere oplossingen gebruikt, verwijdert u de werk ruimte niet.

## <a name="remove-user-and-app-access"></a>Gebruikers-en app-toegang verwijderen

1. Meld u aan bij de [Azure Portal](https://portal.azure.com) als gebruiker met de rol **globale beheerder** . Ga naar **Azure Active Directory**.

1. In **rollen en beheerders**zoekt u naar de rol **Desktop Analytics-beheerder** . Verwijder de leden ervan.

1. Verwijder in **groepen**de leden van de volgende groepen:

    - **M365 Analytics-client beheerders (Log Analytics eigen aren)**
    - **M365 Analytics-client beheerders (Log Analytics inzenders)**

1. In **bedrijfs toepassingen**kunt u toegangs machtigingen voor de volgende apps verwijderen of intrekken:

    - `MaLogAnalyticsReader`

    - De ConfigMgr-app. Als u de naam van deze app wilt vinden, gaat u naar de Configuration Manager-console. Vouw **Cloud Services**uit in de werk ruimte **beheer** en selecteer het knoop punt **Azure-Services** . Open de eigenschappen van de **bureau blad Analytics** -service en schakel over naar het tabblad **toepassingen** . De **Web-app** is deze Azure-app.

        > [!Important]  
        > Voordat u wijzigingen aanbrengt in deze app in azure AD, moet u ervoor zorgen dat u deze niet opnieuw gebruikt met een andere service in Configuration Manager.

## <a name="disconnect-configuration-manager"></a>Verbinding verbreken Configuration Manager

1. Open de Configuration Manager-console als gebruiker met de rol **volledige beheerder** .

1. Ga naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure-Services** .

1. De Desktop Analytics-service verwijderen.

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>Verzamelingen voor de test-en productie-implementaties verwijderen

1. Selecteer in de Configuration Manager-console de optie **apparaten verzamelingen** in de werk ruimte **activa en naleving** .

1. Verwijder verzamelingen die u niet meer gebruikt. De verzamelingen bevinden zich standaard in de map **implementatie plannen** .  

## <a name="reconfigure-clients"></a>Clients opnieuw configureren

### <a name="unenroll-devices"></a>Inschrijving van apparaten ongedaan maken

Verwijder op geregistreerde apparaten de waarde CommercialID uit de volgende Windows-register sleutels:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configuratie van Windows diagnostische gegevens

Als u niet wilt dat uw apparaten diagnostische gegevens gaan verzenden:

- Windows 10: Stel het niveau van diagnostische gegevens in op **beveiliging**
- Windows 7 SP1 of 8,1: de **opt-in-sleutel voor commerciële gegevens** uitschakelen

Stel deze waarden in met een van de volgende methoden:

- Groeps beleid, in **computer configuratie** > **Beheersjablonen** > van**gegevens verzameling en Preview-versies** van Windows-**onderdelen** > 
- Beheer van mobiele apparaten (MDM), zoals [Microsoft intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Zie [Diagnostische gegevens van Windows in uw organisatie configureren](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization) voor meer informatie.

> [!NOTE]  
> Wanneer u deze wijzigingen toepast, stoppen apparaten direct met het verzenden van diagnostische gegevens. Het kan 24-48 uur duren voordat micro soft het verwerken van inzichten voor uw werk ruimte stopt. Micro soft verwijdert deze gegevens binnen 30 dagen of minder in de Cloud Services.

---
title: Micro soft Edge, versie 77 en hoger implementeren en bijwerken
titleSuffix: Configuration Manager
description: Micro soft Edge, versie 77 en hoger met Configuration Manager implementeren en bijwerken
ms.date: 07/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 423864c2c954cc67da4ef54d55d7263ae346e786
ms.sourcegitcommit: 24ce7df7dadf2385afe364b817ec58feeb04c700
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2020
ms.locfileid: "86212283"
---
# <a name="microsoft-edge-management"></a>Micro soft Edge-beheer

*Van toepassing op: Configuration Manager (Current Branch)*

De alles-nieuwe micro soft Edge is gereed voor bedrijven. Vanaf Configuration Manager versie 1910 kunt u nu [micro soft Edge, versie 77 en hoger](https://docs.microsoft.com/deployedge/) implementeren voor uw gebruikers. Er wordt een Power shell-script gebruikt om de geselecteerde Edge-build te installeren. Het script schakelt ook automatische updates voor rand uit zodat deze kunnen worden beheerd met Configuration Manager.

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a>Micro soft Edge implementeren
<!--4561024-->
Beheerders kunnen de bèta, het dev of het stabiele kanaal kiezen, samen met een versie van de micro soft Edge-client die moet worden geïmplementeerd. Elke versie bevat informatie en verbeteringen van onze klanten en community.

### <a name="prerequisites-for-deploying"></a>Vereisten voor het implementeren van

Voor clients die zijn gericht op een micro soft Edge-implementatie:

- Het Power shell- [uitvoerings beleid](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies) kan niet worden ingesteld op beperkt.
  - Power shell wordt uitgevoerd om de installatie uit te voeren.

- Micro soft Edge Installer en [CMPivot](../../core/servers/manage/cmpivot.md) zijn ondertekend met het **micro soft** -certificaat voor ondertekening van programma code. Als dat certificaat niet in het archief **vertrouwde uitgevers** wordt vermeld, moet u het toevoegen. Anders wordt micro soft Edge Installer en CMPivot niet uitgevoerd wanneer het Power shell-uitvoerings beleid is ingesteld op **Alles ondertekend**. <!--7585106-->

Het apparaat waarop de Configuration Manager-console wordt uitgevoerd, heeft toegang tot de volgende eind punten nodig:

|Locatie|Gebruik|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Informatie over versies van micro soft Edge|
|`http://dl.delivery.mp.microsoft.com`|Inhoud voor micro soft Edge-releases|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a>Het update beleid van micro soft Edge controleren

#### <a name="configuration-manager-version-1910"></a>Configuration Manager versie 1910

In versie 1910, wanneer micro soft Edge wordt geïmplementeerd, schakelt het installatie script automatische updates voor micro soft Edge uit zodat deze kunnen worden beheerd met Configuration Manager. U kunt dit gedrag wijzigen met behulp van groepsbeleid. Zie [uw implementatie van micro soft Edge](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies) en [micro soft Edge update-beleid](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies)plannen voor meer informatie.

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager versie 2002 en hoger
<!--4561024-->
Vanaf versie 2002 kunt u een micro soft Edge-toepassing maken die is ingesteld voor het ontvangen van automatische updates in plaats van dat automatische updates zijn uitgeschakeld. Met deze wijziging kunt u ervoor kiezen om updates voor micro soft Edge te beheren met Configuration Manager of micro soft Edge automatisch te laten bijwerken. Wanneer u de toepassing maakt, selecteert **u micro soft Edge toestaan de versie van de client op het apparaat van de eind gebruiker automatisch bij te werken** op de pagina **micro soft Edge-instellingen** . Als u eerder groepsbeleid hebt gebruikt om dit gedrag te wijzigen, overschrijft groepsbeleid de instelling die door Configuration Manager wordt gemaakt tijdens de installatie van micro soft Edge.

[![Instelling voor automatische updates van micro soft Edge](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>Een implementatie maken

Maak een micro soft Edge-toepassing met behulp van de ingebouwde toepassings ervaring, waardoor micro soft Edge eenvoudiger te beheren is:

1. In de-console is er onder **software bibliotheek**een nieuw knoop punt met de naam **micro soft Edge Management**.
1. Selecteer **micro soft Edge-toepassing maken** in het lint of door met de rechter muisknop op het knoop punt **micro soft Edge-beheer** te klikken.

   ![Klik met de rechter muisknop op actie voor het beheer knooppunt van micro soft Edge](./media/4561024-create-microsoft-edge-application.png)

1. Geef op de pagina **Toepassings instellingen** van de wizard een naam, beschrijving en locatie op voor de inhoud van de app. Zorg ervoor dat de map voor de inhouds locatie die u opgeeft, leeg is.
1. Selecteer op de pagina **micro soft Edge-instellingen** :
   - Het te implementeren kanaal
   - De versie die moet worden geïmplementeerd
   - Als u wilt **toestaan dat micro soft Edge automatisch de versie van de client op het apparaat van de eind gebruiker bijwerkt** (toegevoegd in versie 2002)
1. Bepaal op de pagina **implementatie** of u de toepassing wilt implementeren. Als u **Ja**selecteert, kunt u de implementatie-instellingen voor de toepassing opgeven. Zie [toepassingen implementeren](deploy-applications.md#bkmk_deploy-general)voor meer informatie over implementatie-instellingen.
1. In **Software Center** op het client apparaat kan de gebruiker de toepassing weer geven en installeren.

   ![De pagina instellingen van micro soft Edge in de implementatie wizard](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>Logboek bestanden voor implementatie

|Locatie|Log|Gebruik|
|---|---|---|
| Siteserver|SMSProv.log|Geeft details weer als het maken van de app of implementatie mislukt.|
| [Varieert](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| Geeft details weer als het downloaden van de inhoud mislukt|
| Client|  AppEnforce.log|Bevat informatie over de installatie|

## <a name="update-microsoft-edge"></a>Micro soft Edge bijwerken
<!--4831871-->

Vanaf Configuration Manager versie 1910 ziet u een knoop punt met de naam **alle updates van micro soft Edge** onder **micro soft Edge Management**. Dit knoop punt helpt u bij het beheren van updates voor alle micro soft Edge-kanalen.<!--initial edge updates released Jan 15,2020-->

1. Als u updates voor micro soft Edge wilt downloaden, moet u ervoor zorgen dat de **Update** classificatie en het **micro soft Edge** -product zijn [geselecteerd voor synchronisatie](../../sum/get-started/configure-classifications-and-products.md).

   [![Micro soft Edge als product selecteren in eigenschappen van software-update punt](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. Vouw in de werk ruimte **software bibliotheek** het item **micro soft Edge Management** uit en klik op het knoop punt **alle updates van micro soft Edge** .

1. Klik indien nodig op **software-updates synchroniseren** in het lint om een synchronisatie te starten. Zie [software-updates synchroniseren](../../sum/get-started/synchronize-software-updates.md)voor meer informatie.

   ![Knoop punt alle updates van micro soft Edge](./media/4831871-all-microsoft-edge-updates.png)

1. Het beheren en implementeren van updates van micro soft Edge, zoals elke andere update, zoals het toevoegen aan de [regel voor automatische implementatie](../../sum/deploy-use/automatically-deploy-software-updates.md). Enkele van de algemene updates die u kunt uitvoeren vanuit het knoop punt **alle updates van micro soft Edge** zijn onder andere:

   - [Een gefaseerde implementatie maken](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [Software-updates handmatig implementeren](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [Software-updates downloaden](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a>Micro soft Edge Management dash board
<!--3871913-->
*(Geïntroduceerd in versie 2002)*

Vanaf Configuration Manager 2002 biedt het micro soft Edge Management dash board inzicht in het gebruik van micro soft Edge en andere browsers. In dit dash board kunt u het volgende doen:

- Bekijk hoeveel van uw apparaten micro soft Edge hebben geïnstalleerd
- Bekijk hoeveel clients verschillende versies van micro soft Edge hebben geïnstalleerd.
   - Deze grafiek bevat geen Canarische Channel.
- Een weer gave hebben van de geïnstalleerde browsers op verschillende apparaten
- Een weer gave van de voorkeurs browser per apparaat <!--5907383-->
   - Deze grafiek is momenteel leeg voor de 2002-release.

### <a name="prerequisites-for-the-dashboard"></a>Vereisten voor het dash board

Schakel de volgende eigenschappen in in de [hardware-inventaris](../../core/clients/manage/inventory/extend-hardware-inventory.md) klassen voor het micro soft Edge Management-dash board:

- **Geïnstalleerde software-Asset Intelligence (SMS_InstalledSoftware)**
   - Software code
   - Productnaam
   - Product versie

- **Standaard browser (SMS_DefaultBrowser)**
   - Browser programma-ID

- **Browser gebruik (SMS_BrowserUsage)**
   - Browsernaam
   - UsagePercentage

### <a name="view-the-dashboard"></a>Het dashboard weergeven

Klik in de werk ruimte **software bibliotheek** op **micro soft Edge Management** om het dash board weer te geven. Wijzig de verzameling voor de grafiek gegevens door te klikken op **Bladeren** en een andere verzameling te kiezen. Uw vijf grootste verzamelingen bevinden zich standaard in de vervolg keuzelijst. Wanneer u een verzameling selecteert die zich niet in de lijst bevindt, neemt de zojuist geselecteerde verzameling de onderste plaats in de vervolg keuzelijst.

[![Micro soft Edge Management dash board](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="known-issues"></a>Bekende problemen

### <a name="hardware-inventory-may-fail-to-process"></a>Hardware-inventarisatie kan niet worden verwerkt
<!--7535675-->
Hardware-inventarisatie van apparaten kan mogelijk niet worden verwerkt. De fouten die vergelijkbaar zijn met de hieronder hieronder, worden mogelijk weer gegeven in het bestand Dataldr. log:

```text
Begin transaction: Machine=<machine>
*** [23000][2627][Microsoft][SQL Server Native Client 11.0][SQL Server]Violation of PRIMARY KEY constraint 'BROWSER_USAGE_HIST_PK'. Cannot insert duplicate key in object 'dbo.BROWSER_USAGE_HIST'. The duplicate key value is (XXXX, Y). : dbo.dBROWSER_USAGE_DATA
ERROR - SQL Error in
ERROR - is NOT retyrable.
Rollback transaction: XXXX
```

**Risico beperking:** U kunt dit probleem omzeilen door de verzameling van de hardware-inventaris klasse voor het gebruik van de browser (SMS_BrowerUsage) uit te scha kelen.

## <a name="next-steps"></a>Volgende stappen

[Toepassingen bewaken](monitor-applications-from-the-console.md)

[Software-updates controleren](../../sum/deploy-use/monitor-software-updates.md)

[Gefaseerde implementaties beheren en bewaken](../../osd/deploy-use/manage-monitor-phased-deployments.md)

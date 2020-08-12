---
title: Meldingen over opnieuw starten van apparaat
titleSuffix: Configuration Manager
description: Meldings gedrag voor het opnieuw starten van verschillende client instellingen in Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feb9f4206df65ee34228577a9e589ddd1be72870
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127241"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Meldingen voor het opnieuw opstarten van apparaten in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De meldingen die een gebruiker ontvangt voor een apparaat dat opnieuw moet worden opgestart, kunnen variëren, afhankelijk van de [client instellingen voor het opnieuw opstarten](#client-settings) van de computer en de versie van Configuration Manager die u gebruikt. Dit artikel helpt u bij het configureren van de gebruikers ervaring voor meldingen voor het opnieuw opstarten van apparaten.

## <a name="deployment-types-for-restart-notifications"></a>Implementatie typen voor meldingen over opnieuw opstarten

De [client instellingen voor het opnieuw opstarten](#client-settings) van de computer wijzigen de gebruikers ervaring voor alle vereiste implementaties waarvoor het opnieuw opstarten van de volgende typen is vereist:

- [Toepassing](../../../apps/deploy-use/deploy-applications.md)
- [Takenreeks](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Software-update](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Meldings typen opnieuw opstarten

Wanneer een apparaat opnieuw moet worden opgestart, wordt door de client een melding weer gegeven aan de eind gebruiker van de eerstvolgende keer dat de computer opnieuw wordt opgestart.

### <a name="toast-notification"></a>Pop-upmelding

Met een Windows-pop-upmelding wordt de gebruiker geïnformeerd dat het apparaat opnieuw moet worden opgestart. De informatie in de pop-upmelding kan verschillen, afhankelijk van welke versie van Configuration Manager u uitvoert. Dit type melding is systeem eigen voor het Windows-besturings systeem. Mogelijk ziet u ook software van derden met behulp van dit type melding.

:::image type="content" source="media/3555947-restart-toast.png" alt-text="Pop-upmelding van wacht op opnieuw starten":::

### <a name="software-center-notification-with-snooze"></a>Melding over Software Center met uitstellen

Software Center toont een melding met de optie uitstellen en de resterende tijd voordat de apparaten opnieuw worden opgestart. Het bericht kan afwijken, afhankelijk van uw versie van Configuration Manager.

:::image type="content" source="media/3976435-snooze-restart-countdown.png" alt-text="Melding over opnieuw starten in behandeling Software Center met knop uitstellen":::

### <a name="software-center-final-countdown-notification"></a>Melding over laatste aftelling Software Center

Software Center toont deze laatste melding over aftelling die de gebruiker niet kan sluiten of uitstellen.

:::image type="content" source="media/3976435-final-restart-countdown.png" alt-text="Melding over laatste aftelling Software Center":::

Vanaf versie 1906 ziet de gebruiker geen voortgangs balk in de melding over opnieuw opstarten totdat de herstart van de computer minder dan 24 uur duurt.

### <a name="software-center-notification-before-deadline"></a>Melding van software Center vóór deadline

Als de gebruiker de vereiste software proactief vóór de deadline installeert en opnieuw moet worden opgestart, wordt een andere melding weer geven. De volgende melding treedt op wanneer de instelling gebruikers ervaring meldingen toestaat en u geen pop-upmeldingen gebruikt voor de implementatie. Voor meer informatie over het configureren van deze instellingen raadpleegt u [instellingen voor **gebruikers ervaring** voor implementatie](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) en [gebruikers meldingen voor vereiste implementaties](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Melding voor proactief geïnstalleerde software":::

#### <a name="available-apps"></a>Available apps

Wanneer u geen pop-upmeldingen gebruikt, is het dialoog venster voor software dat is gemarkeerd als **beschikbaar** , vergelijkbaar met proactief geïnstalleerde software. Voor **beschik bare** software heeft de melding geen deadline voor het opnieuw opstarten en kan de gebruiker een eigen uitstel interval kiezen. Zie [goedkeurings instellingen](../../../apps/deploy-use/deploy-applications.md#bkmk_approval)voor meer informatie.

:::image type="content" source="media/3555947-deployment-marked-available-restart.png" alt-text="De beschik bare software heeft geen deadline om opnieuw te worden opgestart in de melding":::

### <a name="software-center-notification-of-required-restart"></a>Melding van software Center over vereiste herstart

<!--3601213-->

Vanaf versie 2006 kunt u client instellingen configureren om te voor komen dat apparaten automatisch opnieuw worden gestart wanneer een implementatie deze vereist. Wanneer een vereiste implementatie vereist dat het apparaat opnieuw wordt opgestart, maar u de client instelling uitschakelt **Configuration Manager kan een apparaat geforceerd opnieuw opstarten**, wordt de volgende melding weer geven:

:::image type="content" source="media/3601213-restart-your-computer.png" alt-text="Melding van software Center om de computer opnieuw op te starten":::

Als u **deze melding** uitstelt, wordt deze weer gegeven op basis van de manier waarop u de frequentie van herinneringen voor opnieuw starten configureert. Het apparaat wordt pas opnieuw opgestart als u Windows **opnieuw opstarten** selecteert of opnieuw opstart.

> [!NOTE]
> Standaard kunnen apparaten door Configuration Manager nog steeds opnieuw worden opgestart.

## <a name="client-settings"></a>Clientinstellingen

Als u het gedrag van het opnieuw opstarten van de client wilt beheren, configureert u de volgende client instellingen voor het apparaat in de groep **computer opnieuw opstarten** . Zie [client instellingen configureren](configure-client-settings.md)voor meer informatie.

### <a name="configuration-manager-can-force-a-device-to-restart"></a>Configuration Manager kan een apparaat geforceerd opnieuw opstarten

<!--3601213-->

Vanaf versie 2006 kunt u client instellingen configureren om te voor komen dat apparaten automatisch opnieuw worden gestart wanneer een implementatie deze vereist. Configuration Manager deze instelling standaard ingeschakeld.

> [!IMPORTANT]
> Deze client instelling is van toepassing op alle toepassingen, software-updates en pakket implementaties op het apparaat. Totdat een gebruiker het apparaat hand matig opnieuw opstart:
>
> - Software-updates en app-revisies zijn mogelijk niet volledig geïnstalleerd
> - Extra software-installaties worden mogelijk niet uitgevoerd

Wanneer u deze instelling uitschakelt, kunt u niet de hoeveelheid tijd opgeven na de deadline dat het apparaat opnieuw wordt opgestart of de gebruiker wordt een definitieve aftellings melding gegeven.

> [!NOTE]
> Als u optimaal wilt profiteren van de nieuwe functies van Configuration Manager, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

### <a name="specify-the-amount-of-time-after-the-deadline-before-a-device-gets-restarted-minutes"></a>De hoeveelheid tijd na de deadline opgeven voordat een apparaat opnieuw wordt gestart (minuten)

Deze instelling moet korter zijn dan het kortste onderhouds venster dat wordt toegepast op de computer. Zie [onderhouds Vensters gebruiken](../manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.

De standaard waarde is 90 minuten. Vanaf versie 1906 wordt de maximum waarde verhoogd van 1440 minuten (24 uur) tot 20160 minuten (twee weken).

> [!NOTE]
> Deze instelling werd eerder getiteld **een tijdelijke melding weer gegeven aan de gebruiker die het interval aangeeft voordat de gebruiker wordt afgemeld of de computer opnieuw wordt opgestart (minuten)**.

### <a name="specify-the-amount-of-time-that-a-user-is-presented-a-final-countdown-notification-before-a-device-gets-restarted-minutes"></a>Geef de hoeveelheid tijd op dat een gebruiker een melding voor de uiteindelijke aftelling krijgt voordat een apparaat opnieuw wordt opgestart (minuten)

Deze instelling moet korter zijn dan het kortste onderhouds venster dat wordt toegepast op de computer. Zie [onderhouds Vensters gebruiken](../manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.

De standaardwaarde is 15 minuten.

> [!NOTE]
> Deze instelling was eerder getiteld **een dialoog venster weer geven dat de gebruiker niet kan sluiten, waarin het aftellings interval wordt weer gegeven voordat de gebruiker wordt afgemeld of de computer opnieuw wordt opgestart (minuten)**.

### <a name="specify-the-frequency-of-reminder-notifications-presented-to-the-user-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Geef de frequentie op van de herinnerings meldingen die na de deadline aan de gebruiker worden gepresenteerd voordat een apparaat opnieuw wordt opgestart (minuten)
<!--3976435-->
_Vanaf versie 1906_

De waarde van de frequentie duur moet kleiner zijn dan de waarde van de **tijd opgeven na de deadline voordat een apparaat opnieuw wordt opgestart (minuten),** min de waarde van **de periode opgeven dat een gebruiker een melding voor de uiteindelijke aftelling krijgt voordat een apparaat opnieuw wordt opgestart (minuten)**. Anders werken de herinnerings meldingen niet.

De standaard waarde is 240 minuten.

> [!NOTE]
> Deze instelling was eerder getiteld **de duur van het opnieuw starten van de computer (minuten) opgeven**.

### <a name="when-a-deployment-requires-a-restart-show-a-dialog-window-to-the-user-instead-of-a-toast-notification"></a>Wanneer een implementatie opnieuw moet worden opgestart, een dialoog venster weer geven voor de gebruiker in plaats van een pop-upmelding
<!--3555947-->
Vanaf versie 1902 kunt u met deze instelling **Ja** wijzigingen aanbrengen in de gebruikers ervaring. Deze instelling is van toepassing op alle implementaties van toepassingen, taken reeksen en software-updates. Zie [plan for Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact)(Engelstalig) voor meer informatie.

> [!IMPORTANT]
> In Configuration Manager 1902 worden pop-upmeldingen in het dialoog venster niet vervangen. Om dit probleem op te lossen, installeert u het [Update pakket voor Configuration Manager versie 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="device-restart-notifications-version-1906"></a>Meldingen voor opnieuw opstarten van apparaat (versie 1906)
<!--3976435-->
Sommige klanten geven de voor keur aan meldingen over veelvuldig opnieuw opstarten en toestaan dat gebruikers een kort tijds bestek hebben om uit te stellen. Anderen stellen gebruikers in staat om opnieuw opstarten langer dan langere tijd uit te stellen en gebruikers te informeren over het opnieuw opstarten in behandeling. Vanaf Configuration Manager versie 1906 hebt u meer controle over de timing en de frequentie van meldingen over opnieuw starten.

### <a name="install-required-software-at-or-after-the-deadline"></a>Vereiste software installeren op of na de deadline

Wanneer vereiste software is geïnstalleerd op of na de deadline, zien uw gebruikers meldingen, afhankelijk van de client instellingen die u hebt geselecteerd.

Als de instelling voor het **opnieuw opstarten van een implementatie vereist is, wordt een dialoog venster weer gegeven voor de gebruiker in plaats van een pop-upmelding** is ingesteld op:

- **Nee**: Windows geeft pop-upmeldingen weer totdat de implementatie de laatste melding over aftelling bereikt.

- **Ja**: in Software Center wordt een melding weer gegeven:

  - Als de herstart langer dan 24 uur duurt, wordt een geschatte start tijd weer gegeven. De timing van deze melding is gebaseerd op de instelling: **Geef de hoeveelheid tijd op na de deadline voordat een apparaat opnieuw wordt gestart (minuten)**.

    :::image type="content" source="media/3976435-notification-greater-than-24-hours.png" alt-text="De tijd voor opnieuw opstarten is langer dan 24 uur":::

  - Als de herstart minder dan 24 uur duurt, wordt een voortgangs balk weer gegeven. De timing van deze melding is gebaseerd op de instelling: **Geef de hoeveelheid tijd op na de deadline voordat een apparaat opnieuw wordt gestart (minuten)**.

    :::image type="content" source="media/3976435-notification-less-than-24-hours.png" alt-text="De herstart-tijd is minder dan 24 uur":::

Als de gebruiker **uitstellen**selecteert, wordt er een andere tijdelijke melding weer gegeven nadat de uitstel periode is verstreken. Dit gedrag gaat ervan uit dat de laatste aftelling nog niet is bereikt. De timing van de volgende melding is gebaseerd op de instelling: **Geef de frequentie op van de herinnerings meldingen die aan de gebruiker worden gepresenteerd na de deadline voordat een apparaat opnieuw wordt opgestart (minuten)**. Als de gebruiker **uitstellen**selecteert en uw uitstel interval is één uur, stuurt Software Center de gebruiker opnieuw over 60 minuten. Dit gedrag gaat ervan uit dat de laatste aftelling nog niet is bereikt.

Wanneer de laatste aftelling is bereikt, toont Software Center de gebruiker een melding dat ze niet kunnen worden gesloten. De voortgangs balk is rood en de gebruiker kan deze niet **uitstellen** .

:::image type="content" source="media/3976435-1906-final-restart-countdown.png" alt-text="Melding over laatste aftelling Software Center in versie 1906":::

### <a name="proactively-install-required-software-before-the-deadline"></a>Installeer de vereiste software proactief vóór de deadline

Als de gebruiker de vereiste software die vóór de deadline opnieuw moet worden opgestart, proactief installeert, zien ze een andere melding. Voor meer informatie over het configureren van deze instellingen raadpleegt u [instellingen voor **gebruikers ervaring** voor implementatie](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) en [gebruikers meldingen voor vereiste implementaties](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

De volgende melding treedt op wanneer de instelling gebruikers ervaring meldingen toestaat en u geen pop-upmeldingen gebruikt voor de implementatie:

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Melding voor proactief geïnstalleerde software":::

Zodra de deadline van de implementatie is bereikt, volgt Software Center het gedrag om de [vereiste software op of na de deadline te installeren](#install-required-software-at-or-after-the-deadline).

## <a name="example-configurations"></a>Voorbeeld configuraties

In de volgende voor beelden wordt beschreven hoe u de client instellingen configureert voor specifiek gedrag.

### <a name="reminders-are-off"></a>Herinneringen zijn uitgeschakeld

| Instelling | Waarde |
|---------|---------|
|De hoeveelheid tijd na de deadline opgeven voordat een apparaat opnieuw wordt gestart (minuten)|180|
|Geef de hoeveelheid tijd op dat een gebruiker een melding voor de uiteindelijke aftelling krijgt voordat een apparaat opnieuw wordt opgestart (minuten)|60|
|Geef de frequentie op van de herinnerings meldingen die na de deadline aan de gebruiker worden gepresenteerd voordat een apparaat opnieuw wordt opgestart (minuten)|240|
|Wanneer een implementatie opnieuw moet worden opgestart, een dialoog venster weer geven voor de gebruiker in plaats van een pop-upmelding|Nee|

Het apparaat wordt na de deadline van de implementatie drie uur (**180** minuten) opnieuw opgestart. Een uur (**60** minuten) voordat deze opnieuw wordt opgestart, ziet de gebruiker een aftelling die niet kan worden gesloten of uitgesteld. De eerste herinnerings melding is ingesteld op het begin van vier uur (**240** minuten) na de deadline, na het opnieuw opstarten. Zodat de gebruiker geen enkele herinnering ziet.

### <a name="low-reminder-frequency"></a>Frequentie lage herinnering

| Instelling | Waarde |
|---------|---------|
|De hoeveelheid tijd na de deadline opgeven voordat een apparaat opnieuw wordt gestart (minuten)|7200|
|Geef de hoeveelheid tijd op dat een gebruiker een melding voor de uiteindelijke aftelling krijgt voordat een apparaat opnieuw wordt opgestart (minuten)|120|
|Geef de frequentie op van de herinnerings meldingen die na de deadline aan de gebruiker worden gepresenteerd voordat een apparaat opnieuw wordt opgestart (minuten)|900|
|Wanneer een implementatie opnieuw moet worden opgestart, een dialoog venster weer geven voor de gebruiker in plaats van een pop-upmelding|Ja|

Het apparaat wordt na de deadline van de implementatie vijf dagen (**7200** minuten) opnieuw opgestart. Twee uur (**120** minuten) voordat deze opnieuw wordt opgestart, ziet de gebruiker een aftelling die niet kan worden gesloten of uitgesteld. Met deze configuratie kan gedurende 118 uur herinneringen () worden weer gegeven `(7200 - 120) / 60` . 15 uur (**900** minuten) na de deadline wordt in Software Center de eerste herinnering weer gegeven. Er worden Maxi maal zes extra herinneringen per 15 uur (**900 minuten**) weer gegeven. De gebruiker ziet de herinnering als een venster op het scherm, in plaats van een melding die binnen een paar seconden verdwijnt.

### <a name="high-reminder-frequency"></a>Frequentie van hoge herinnering

| Instelling | Waarde |
|---------|---------|
|De hoeveelheid tijd na de deadline opgeven voordat een apparaat opnieuw wordt gestart (minuten)|2880|
|Geef de hoeveelheid tijd op dat een gebruiker een melding voor de uiteindelijke aftelling krijgt voordat een apparaat opnieuw wordt opgestart (minuten)|60|
|Geef de frequentie op van de herinnerings meldingen die na de deadline aan de gebruiker worden gepresenteerd voordat een apparaat opnieuw wordt opgestart (minuten)|30|
|Wanneer een implementatie opnieuw moet worden opgestart, een dialoog venster weer geven voor de gebruiker in plaats van een pop-upmelding|Ja|

Het apparaat wordt na de deadline van de implementatie twee dagen (**2880** minuten) opnieuw opgestart. Een uur (**60** minuten) voordat deze opnieuw wordt opgestart, ziet de gebruiker een aftelling die niet kan worden gesloten of uitgesteld. Met deze configuratie kan gedurende 47 uur herinneringen () worden weer gegeven `(2880 - 60) / 60` . **30** minuten na de deadline wordt in Software Center de eerste herinnering weer gegeven. Er worden Maxi maal 92 extra herinneringen per **30 minuten**weer gegeven. De gebruiker ziet de herinnering als een venster op het scherm, in plaats van een melding die binnen een paar seconden verdwijnt.

## <a name="device-restart-notifications-version-1902"></a>Meldingen voor opnieuw opstarten van apparaat (versie 1902)

<!--3555947-->
Soms zien gebruikers de Windows-pop-upmelding over het opnieuw opstarten of de vereiste implementatie niet. De ervaring wordt dan niet weer geven om de herinnering af te stellen. Dit gedrag kan leiden tot een slechte gebruikers ervaring wanneer de client een deadline bereikt.

Vanaf versie 1902, wanneer er software wijzigingen zijn vereist of implementaties opnieuw moeten worden opgestart, hebt u de mogelijkheid om een meer opvallend dialoog venster te gebruiken.

Schakel in de groep [computer opnieuw opstarten](#client-settings) van client instellingen de volgende optie in: **Wanneer een implementatie opnieuw moet worden opgestart, wordt een dialoog venster weer gegeven voor de gebruiker in plaats van een pop-upmelding**.  

Als u deze client instelling configureert, wordt de gebruikers ervaring voor alle vereiste implementaties gewijzigd waarvoor opnieuw opstarten is vereist voor pop-upmeldingen:

:::image type="content" source="media/3555947-restart-toast-initial.png" alt-text="Pop-upmelding dat opnieuw opstarten is vereist":::

Het dialoog venster Software Center meer opvallend:

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Dialoog venster om de computer opnieuw op te starten":::

Als de gebruiker het apparaat na de installatie niet opnieuw heeft opgestart, krijgen ze een melding als een herinnering. Deze tijdelijke herinnering wordt weer gegeven aan de gebruiker op basis van de client instelling: **geeft een tijdelijke melding weer voor de gebruiker die het interval aangeeft voordat de gebruiker wordt afgemeld of de computer opnieuw wordt opgestart (minuten)**. Deze instelling is de totale tijd die de gebruiker heeft om de computer opnieuw op te starten voordat de herstart wordt afgedwongen.

- Tijdelijke melding wanneer u pop-upmeldingen gebruikt:

    :::image type="content" source="media/3555947-restart-toast.png" alt-text="Pop-upmelding van wacht op opnieuw starten":::

- Tijdelijke melding wanneer u het dialoog venster Software Center gebruikt en niet op pop-up:

    :::image type="content" source="media/3555947-1902-hide-notification.png" alt-text="Melding over opnieuw starten in behandeling Software Center met knop uitstellen":::

Als de gebruiker niet opnieuw wordt opgestart na de tijdelijke melding, krijgt deze de laatste melding over aftelling dat ze niet kunnen worden gesloten. Het tijdstip waarop de laatste melding wordt weer gegeven, is gebaseerd op de client instelling: **een dialoog venster weer geven dat de gebruiker niet kan sluiten, waarin het aftellings interval wordt weer gegeven voordat de gebruiker wordt afgemeld of de computer opnieuw wordt opgestart (minuten)**. Als de instelling bijvoorbeeld 60 is, wordt een uur voordat de computer opnieuw wordt opgestart, de laatste melding voor de gebruiker weer gegeven:

:::image type="content" source="media/3555947-1902-final-countdown.png" alt-text="Melding over laatste aftelling Software Center":::

De volgende instellingen moeten korter zijn dan het kortste [onderhouds venster](../manage/collections/use-maintenance-windows.md) dat wordt toegepast op de computer:

- **Een tijdelijke melding weer geven aan de gebruiker die het interval aangeeft voordat de gebruiker wordt afgemeld of de computer opnieuw opstart (minuten)**
- **Een dialoog venster weer geven dat de gebruiker niet kan sluiten en waarin het aftellings interval wordt weer gegeven voordat de gebruiker wordt afgemeld of de computer opnieuw opstart (minuten)**

> [!IMPORTANT]
> In Configuration Manager 1902 worden pop-upmeldingen in het dialoog venster niet vervangen. Om dit probleem op te lossen, installeert u het [Update pakket voor Configuration Manager versie 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="log-files"></a>Logboekbestanden

Gebruik de bestanden **RebootCoordinator. log** en **SCNotify. log** op de client om problemen met het opnieuw opstarten van het apparaat op te lossen. Op basis van het specifieke implementatie type moet u mogelijk ook aanvullende client [logboek bestanden](../../plan-design/hierarchy/log-files.md)gebruiken.

## <a name="next-steps"></a>Volgende stappen

- [Clientinstellingen configureren](configure-client-settings.md)
- [Instellingen voor **gebruikers ervaring** voor toepassings implementatie](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [Gebruikers meldingen voor vereiste app-implementaties](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)

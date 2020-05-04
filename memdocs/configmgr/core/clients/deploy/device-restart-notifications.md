---
title: Meldingen over opnieuw starten van apparaat
titleSuffix: Configuration Manager
description: Meldings gedrag voor het opnieuw starten van verschillende client instellingen in Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b6d383b2d5904f4d31fff5f549127dc21c39f29
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713392"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Meldingen voor het opnieuw opstarten van apparaten in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De meldingen die een gebruiker ontvangt voor een apparaat dat opnieuw moet worden opgestart, kunnen variëren, afhankelijk van de [client instellingen voor de computer opnieuw opstarten](about-client-settings.md#computer-restart) en welke versie van Configuration Manager wordt gebruikt. Dit artikel helpt beheerders bij het bepalen van de gebruikers ervaring voor het opnieuw opstarten van apparaten in behandeling.

>[!NOTE]
> - Dit artikel richt zich op client instellingen in Configuration Manager versie 1902 en versie 1906.


## <a name="deployment-types-for-restart-notifications"></a>Implementatie typen voor meldingen over opnieuw opstarten

De [client instellingen voor het opnieuw opstarten](about-client-settings.md#computer-restart) van de computer wijzigen de gebruikers ervaring voor alle vereiste implementaties waarvoor het opnieuw opstarten van de volgende typen is vereist:

- [Toepassing](../../../apps/deploy-use/deploy-applications.md)
- [Takenreeks](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Software-update](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Meldings typen opnieuw opstarten

Wanneer opnieuw opstarten is vereist, wordt de eind gebruiker op de hoogte gesteld van de aanstaande herstart. Er zijn vier algemene meldingen die gebruikers kunnen ontvangen:

**Pop-upmelding** waarin u wordt geïnformeerd dat opnieuw opstarten nodig is. De informatie in de pop-upmelding kan verschillen, afhankelijk van welke versie van Configuration Manager u uitvoert. Dit type melding is systeem eigen voor het Windows-besturings systeem en u kunt ook software van derden bekijken met dit type melding.

![Pop-upmelding van wacht op opnieuw starten](media/3555947-restart-toast.png)

Melding van software Center met een uitstel optie waarmee de resterende tijd wordt weer gegeven voordat de herstart wordt afgedwongen. Het bericht kan afwijken, afhankelijk van uw versie van Configuration Manager.

![Melding over opnieuw starten in behandeling Software Center met knop uitstellen](media/3976435-snooze-restart-countdown.png)

Melding over definitieve Aftel tijd van software Center dat niet door de gebruiker kan worden gesloten. De knop uitstellen wordt grijs weer gegeven.

![Melding over laatste aftelling Software Center](media/3976435-final-restart-countdown.png)

Als de gebruiker de vereiste software die opnieuw moet worden opgestart, proactief installeert voordat de deadline plaatsvindt, zien ze een andere melding. De volgende melding treedt op wanneer de instelling gebruikers ervaring meldingen toestaat en u geen pop-upmeldingen gebruikt voor de implementatie. Voor meer informatie over het configureren van deze instellingen raadpleegt u [instellingen voor **gebruikers ervaring** voor implementatie](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) en [gebruikers meldingen voor vereiste implementaties](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Melding voor proactief geïnstalleerde software](media/3976435-proactive-user-restart-notification.png)

- Wanneer u geen pop-upmeldingen gebruikt, is het dialoog venster voor software dat is gemarkeerd als **beschikbaar** , vergelijkbaar met proactief geïnstalleerde software.

  - Voor **beschik bare** software heeft de melding geen deadline voor het opnieuw opstarten en kan de gebruiker een eigen uitstel interval kiezen. Zie [goedkeurings instellingen](../../../apps/deploy-use/deploy-applications.md#bkmk_approval)voor meer informatie.

    ![Software die is gemarkeerd als beschikbaar, heeft geen deadline om opnieuw op te starten in de melding.](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>Meldingen voor het opnieuw opstarten van apparaten in versie 1902

<!--3555947-->
Soms zien gebruikers de Windows-pop-upmelding over het opnieuw opstarten of de vereiste implementatie niet. De ervaring wordt dan niet weer geven om de herinnering af te stellen. Dit gedrag kan leiden tot een slechte gebruikers ervaring wanneer de client een deadline bereikt.

Vanaf versie 1902, wanneer er software wijzigingen zijn vereist of implementaties opnieuw moeten worden opgestart, hebt u de mogelijkheid om een meer opvallend dialoog venster te gebruiken.

Schakel in de groep [computer opnieuw opstarten](about-client-settings.md#computer-restart) van client instellingen de volgende optie in: **Wanneer een implementatie opnieuw moet worden opgestart, wordt een dialoog venster weer gegeven voor de gebruiker in plaats van een pop-upmelding**.  

Als u deze client instelling configureert, wordt de gebruikers ervaring voor alle vereiste implementaties gewijzigd waarvoor opnieuw opstarten is vereist voor pop-upmeldingen:

![Pop-upmelding dat opnieuw opstarten is vereist](media/3555947-restart-toast-initial.png)  

Het dialoog venster Software Center meer opvallend:

![Dialoog venster om de computer opnieuw op te starten](media/3976435-proactive-user-restart-notification.png)

Als de gebruiker het apparaat na de installatie niet opnieuw heeft opgestart, krijgen ze een melding als een herinnering. Deze tijdelijke herinnering wordt weer gegeven aan de gebruiker op basis van de client instelling: **geeft een tijdelijke melding weer voor de gebruiker die het interval aangeeft voordat de gebruiker wordt afgemeld of de computer opnieuw wordt opgestart (minuten)**. Deze instelling is de totale tijd die de gebruiker heeft om de computer opnieuw op te starten voordat de herstart wordt afgedwongen.

- Tijdelijke melding wanneer u pop-upmeldingen gebruikt:

  ![Pop-upmelding van wacht op opnieuw starten](media/3555947-restart-toast.png)

- Tijdelijke melding wanneer u het dialoog venster Software Center gebruikt en niet op pop-up:

  ![Melding over opnieuw starten in behandeling Software Center met knop uitstellen](media/3555947-1902-hide-notification.png)

Als de gebruiker niet opnieuw wordt opgestart na de tijdelijke melding, krijgt deze de laatste melding over aftelling dat ze niet kunnen worden gesloten. Het tijdstip waarop de laatste melding wordt weer gegeven, is gebaseerd op de client instelling: **een dialoog venster weer geven dat de gebruiker niet kan sluiten, waarin het aftellings interval wordt weer gegeven voordat de gebruiker wordt afgemeld of de computer opnieuw wordt opgestart (minuten)**. Als de instelling bijvoorbeeld 60 is, wordt een uur voordat de computer opnieuw wordt opgestart, de laatste melding voor de gebruiker weer gegeven:

![Melding over laatste aftelling Software Center](media/3555947-1902-final-countdown.png)

De volgende instellingen moeten korter zijn dan het kortste [onderhouds venster](../manage/collections/use-maintenance-windows.md) dat wordt toegepast op de computer:

- **Een tijdelijke melding weer geven aan de gebruiker die het interval aangeeft voordat de gebruiker wordt afgemeld of de computer opnieuw opstart (minuten)**
- **Een dialoog venster weer geven dat de gebruiker niet kan sluiten en waarin het aftellings interval wordt weer gegeven voordat de gebruiker wordt afgemeld of de computer opnieuw opstart (minuten)**

> [!IMPORTANT]
> In Configuration Manager 1902 worden pop-upmeldingen in het dialoog venster niet vervangen. Om dit probleem op te lossen, installeert u het [Update pakket voor Configuration Manager versie 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="device-restart-notifications-starting-in-version-1906"></a>Meldingen voor opnieuw opstarten van apparaat vanaf versie 1906
<!--3976435-->
Sommige beheerders geven de voor keur aan meldingen die vaak opnieuw worden gestart en een korte periode waarin het opnieuw opstarten kan worden uitgesteld. Andere beheerders stellen gebruikers in staat om opnieuw opstarten uit te stellen voor langere Peri Oden en dat gebruikers op de hoogte moeten worden gesteld van de wacht tijd die opnieuw moet worden opgestart. Configuration Manager versie 1906 geeft een beheerder extra controle over de timing en de frequentie van meldingen voor opnieuw opstarten. De volgende items zijn in 1906 geïntroduceerd om de beheerder meer controle te geven:

- **Geef de duur voor uitstellen op voor het opnieuw starten van de computer (minuten)** is toegevoegd aan de [client instellingen](about-client-settings.md#computer-restart)voor het opnieuw opstarten van de computer.
- De maximum waarde voor **het weer geven van een tijdelijke melding aan de gebruiker die het interval aangeeft voordat de gebruiker wordt afgemeld of de computer opnieuw wordt opgestart (minuten)** , verhoogd van 1440 minuten (24 uur) tot 20160 minuten (twee weken).
- De gebruiker ziet geen voortgangs balk in de melding opnieuw opstarten totdat de herstart van de computer minder dan 24 uur duurt.

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>Meldingen wanneer vereiste software is geïnstalleerd op of na de deadline

Wanneer vereiste software is geïnstalleerd op of na de deadline, zien uw gebruikers meldingen, afhankelijk van de client instellingen die u hebt geselecteerd.

Als de instelling voor het **opnieuw opstarten van een implementatie vereist is, wordt een dialoog venster weer gegeven voor de gebruiker in plaats van een pop-upmelding** is ingesteld op:

- **Er worden geen** meldingen voor de pop-uptaak gebruikt totdat de uiteindelijke aftellings melding is bereikt.
- **Ja** , er is een melding van een software Center weer gegeven.
  - Als de herstart langer dan 24 uur duurt, wordt een geschatte tijd voor opnieuw opstarten gezien. De timing van deze melding is gebaseerd op de instelling: **een tijdelijke melding weer geven aan de gebruiker die het interval aangeeft voordat de gebruiker wordt afgemeld of de computer opnieuw wordt opgestart (minuten)**.

     ![De tijd voor opnieuw opstarten is langer dan 24 uur](media/3976435-notification-greater-than-24-hours.png)

  - Als de herstart minder dan 24 uur is, wordt er een voortgangs balk weer gegeven. De timing van deze melding is gebaseerd op de instelling: **een tijdelijke melding weer geven aan de gebruiker die het interval aangeeft voordat de gebruiker wordt afgemeld of de computer opnieuw opstart (minuten)**

     ![De herstart-tijd is minder dan 24 uur](media/3976435-notification-less-than-24-hours.png)

Als de gebruiker de knop **uitstellen** selecteert, wordt er een andere tijdelijke melding weer gegeven nadat de uitstel periode is verstreken, ervan uitgaande dat de laatste aftelling nog niet is bereikt. De timing van de volgende melding is gebaseerd op de instelling: **Geef de duur voor uitstellen op voor het opnieuw starten van de computer (uren)**. Als de gebruiker **uitstellen** selecteert en uw uitstel interval één uur is, wordt de gebruiker opnieuw in 60 minuten gewaarschuwd, ervan uitgaande dat de laatste aftelling nog niet is bereikt.

Wanneer de laatste aftelling is bereikt, krijgt de gebruiker een melding dat ze niet kunnen worden gesloten. De voortgangs balk is rood en de gebruiker kan niet op **uitstellen**worden geklikt.

![Melding over laatste aftelling Software Center in versie 1906](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>De gebruiker wordt proactief vóór de deadline geïnstalleerd

Als de gebruiker de vereiste software die opnieuw moet worden opgestart, proactief installeert voordat de deadline plaatsvindt, zien ze een andere melding. Voor meer informatie over het configureren van deze instellingen raadpleegt u [instellingen voor **gebruikers ervaring** voor implementatie](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) en [gebruikers meldingen voor vereiste implementaties](../../../apps/deploy-use/deploy-applications.md#bkmk_notify). 

De volgende melding treedt op wanneer de instelling gebruikers ervaring meldingen toestaat en u geen pop-upmeldingen gebruikt voor de implementatie:

![Melding voor proactief geïnstalleerde software](media/3976435-proactive-user-restart-notification.png)

Zodra de deadline voor de software is bereikt, worden de [meldingen wanneer de vereiste software is geïnstalleerd op of na de deadline](#notifications-when-required-software-is-installed-at-or-after-the-deadline) , gevolgd.

## <a name="log-files"></a>Logboekbestanden

Gebruik **RebootCoordinator. log** en **SCNotify. log** voor het oplossen van problemen met het opnieuw opstarten van apparaten. Mogelijk moet u ook aanvullende client [logboek bestanden](../../plan-design/hierarchy/log-files.md) gebruiken op basis van het gebruikte implementatie type.

## <a name="next-steps"></a>Volgende stappen

- [Inleiding tot toepassings beheer](../../../apps/understand/introduction-to-application-management.md)
- [Inleiding tot besturingssysteemimplementaties](../../../osd/understand/introduction-to-operating-system-deployment.md)
- [Inleiding tot beheer van software-updates](../../../sum/understand/software-updates-introduction.md)

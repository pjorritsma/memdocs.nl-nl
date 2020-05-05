---
title: Gebruikerservaring voor implementatie van besturingssysteem
titleSuffix: Configuration Manager
description: Meer informatie over gebruikers ervaringen, zoals de wizard voortgang en media van de taken reeks voor de implementatie van besturings systemen in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f92e76047a70f6d86406b1a364603163d902e62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719930"
---
# <a name="user-experiences-for-os-deployment"></a>Gebruikerservaring voor implementatie van besturingssysteem

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u [een taken reeks hebt geïmplementeerd](../deploy-use/deploy-a-task-sequence.md), is er afhankelijk van het scenario verschillende manieren om gebruikers te laten communiceren met de implementatie. In dit artikel vindt u informatie over de belangrijkste gebruikers ervaring met besturingssysteem implementaties en over hoe u deze kunt configureren:

- Gebruikers melding van software Center voor een implementatie met hoge impact
- Een voor beeld van een PXE-opstart ervaring
- Wizard taken reeks van media
- Voortgangs venster wanneer de taken reeks wordt uitgevoerd
- Fout venster wanneer de taken reeks mislukt

## <a name="software-center"></a>Software Center

Voor een implementatie met hoge impact kunt u het bericht aanpassen dat in Software Center wordt weer gegeven. Wanneer de gebruiker de implementatie van het besturings systeem in Software Center opent, wordt een bericht weer gegeven dat vergelijkbaar is met het volgende venster:

![Aangepaste taken reeks melding voor de eind gebruiker vanuit software Center](../media/user-notification-enduser.png)

Zie [een aangepaste melding voor implementaties met een hoog risico maken](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments)voor meer informatie over het aanpassen van het bericht in dit venster.

U kunt ook de naam van de organisatie aan de bovenkant van het venster aanpassen. (In het bovenstaande voor beeld wordt de standaard `IT Organization`waarde weer gegeven). Wijzig de client instelling **organisatie naam** in de groep **computer agent** . Zie [over client instellingen](../../core/clients/deploy/about-client-settings.md#computer-agent)voor meer informatie.

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

Zie [Software Center gebruiken om Windows via het netwerk te implementeren](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md)voor meer informatie.

## <a name="pxe"></a>PXE

Verschillende hardwareprofielen hebben verschillende ervaringen voor PXE. Om het netwerk op te starten, gebruiken UEFI-apparaten doorgaans de `Enter` sleutel en gebruiken BIOS-apparaten de `F12` -sleutel.

In het volgende voor beeld wordt de PXE-ervaring van Hyper-V gen1 (BIOS) weer gegeven:

![Voor beeld van BIOS-PXE-scherm van een Hyper-V-virtuele machine](media/hyperv-pxe.png)

Nadat het apparaat is opgestart via PXE, gedraagt het zich op dezelfde manier als opstart bare media. Zie de volgende sectie van de [wizard taken reeks](#task-sequence-wizard)voor meer informatie.

Zie [PXE gebruiken om Windows via het netwerk te implementeren](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie.

> [!WARNING]
> Als u PXE-implementaties gebruikt en de hardware van het apparaat configureert met de netwerk adapter als het eerste opstart apparaat, kunnen deze apparaten automatisch een taken reeks voor besturingssysteem implementatie starten zonder tussen komst van de gebruiker. Deze configuratie wordt niet beheerd door implementatie verificatie. Hoewel deze configuratie het proces kan vereenvoudigen en de gebruikers interactie vermindert, wordt het apparaat voor een groter risico voor onbedoelde herinstallatie kopieën geplaatst.

## <a name="task-sequence-wizard"></a>Wizard taken reeks

Wanneer u [taken reeks media](../deploy-use/create-task-sequence-media.md)gebruikt, wordt de wizard taken reeks uitgevoerd om het proces te begeleiden.

### <a name="welcome-to-the-task-sequence-wizard"></a>Welkom bij de wizard taken reeks

![Scherm afbeelding van de hoofd pagina van de wizard taken reeks](media/welcome-task-sequence-wizard.png)

- Als u de media met een wacht woord beveiligt, moet de gebruiker het wacht woord invoeren op deze welkomst pagina.

- Selecteer **netwerk instellingen configureren** om een statisch IP-adres of andere aangepaste netwerk instellingen op te geven. Anders gebruikt het apparaat standaard DHCP.

- Als uw netwerk een proxy vereist, selecteert u **proxy-instellingen configureren**.

### <a name="select-a-task-sequence-to-run"></a>Een uit te voeren taken reeks selecteren

Als u meer dan één taken reeks op het apparaat implementeert, ziet u deze pagina om een taken reeks te selecteren. Zorg ervoor dat u een naam en beschrijving gebruikt voor uw taken reeks die gebruikers kunnen begrijpen.

![Scherm afbeelding van de pagina taken reeks selectie van de wizard taken reeks](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>Taken reeks variabelen bewerken

Als taken reeks variabelen lege waarden bevatten, wordt in de wizard een pagina weer gegeven voor het bewerken van de waarden van de variabele.

![Scherm afbeelding van de pagina taken reeks variabelen bewerken van de wizard taken reeks](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>Prestart-opdrachten

U kunt taken reeks media of opstart installatie kopieën aanpassen om een prestart-opdracht uit te voeren. Een prestart-opdracht wordt uitgevoerd voordat de taken reeks wordt gestart. De volgende acties zijn een aantal van de meest voorkomende waarden:

- De gebruiker vragen om dynamische waarden, zoals de computer naam
- Netwerk configuratie opgeven
- Affiniteit van gebruiker met apparaat instellen

De prestart-opdracht is een opdracht regel die u met een script of programma opgeeft. De gebruikers ervaring is uniek voor dat script of programma.

Raadpleeg voor meer informatie de volgende artikelen:

- [Prestart-opdrachten voor takenreeksmedia](prestart-commands-for-task-sequence-media.md)
- [Opstartinstallatiekopieën beheren](../get-started/manage-boot-images.md#customization)
- [Taken reeks media](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>Voortgang van taken reeks

Wanneer de taken reeks wordt uitgevoerd, wordt het venster voortgang van de **installatie** weer gegeven:

![Voor beeld van het venster voortgang van taken reeks](media/task-sequence-progress.png)

- Dit venster bevindt zich altijd op de voor grond. u kunt deze verplaatsen, maar niet sluiten of minimaliseren.

- U kunt de naam van de organisatie aan de bovenkant van het venster aanpassen. (In het bovenstaande voor beeld wordt de standaard `IT Organization`waarde weer gegeven). Wijzig de client instelling **organisatie naam** in de groep **computer agent** . Zie [over client instellingen](../../core/clients/deploy/about-client-settings.md#computer-agent)voor meer informatie.

    > [!TIP]
    > De taken reeks slaat deze waarde op in de variabele met het kenmerk alleen-lezen [_SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName).

- U kunt de subkoppen aanpassen. (In het bovenstaande voor beeld ziet u de `Running: <task sequence name>`standaard waarde,.) Selecteer op de eigenschappen van de taken reeks de optie voor het **gebruik van aangepaste tekst** voor de voortgangs meldings tekst. Dit kan Maxi maal 255 tekens lang zijn.

- **Actie uitvoeren**: de eerste regel bevat de naam van de huidige taken reeks stap. In de onderstaande voortgangs balk ziet u de algemene voltooiing van de taken reeks.

- Op de tweede regel worden alleen de stappen weer gegeven die een gedetailleerdere voortgang bieden.

- Gebruik de taken reeks variabele [TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI) om te bepalen wanneer de taken reeks de voortgang weergeeft.

    Als u het voortgangs venster volledig wilt uitschakelen, schakelt u de optie uit om de **voortgang van taken reeksen weer te geven** op de pagina **gebruikers ervaring** van de taken reeks implementatie.

Vanaf versie 2002 bevat het venster voortgang van taken reeks de volgende verbeteringen:<!--5932692-->

- Hier worden het huidige stap nummer, het totale aantal stappen en het voltooiings percentage weer gegeven

- De breedte van het venster verg root zodat u meer ruimte krijgt om de naam van de organisatie in één regel weer te geven

![Voor beeld van voortgangs venster taken reeks](media/2356386-task-sequence-progress.png)

Het venster voortgang van taken reeksen maakt standaard gebruik van de bestaande tekst. Als u geen wijzigingen aanbrengt, blijft de werking hetzelfde als in versie 1910 en eerder. Geef de taken reeks variabele [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel)op om de nieuwe voortgangs gegevens weer te geven.

Het aantal en het percentage dat is voltooid, zijn alleen bedoeld voor algemene richt lijnen. Deze waarden zijn gebaseerd op het totaal aantal stappen in de taken reeks. Voor een complexere taken reeks met stappen die voorwaardelijk worden uitgevoerd op basis van de taken reeks logica, is de voortgang mogelijk niet-lineair.

Het totale aantal stappen bevat niet de volgende items in de taken reeks:

- Groepen. Dit item is een container voor andere stappen, niet een stap zelf.

- Exemplaren van de stap **taken reeks uitvoeren** . Deze stap is een container voor andere stappen.

- Stappen die u expliciet uitschakelt. Een uitgeschakelde stap wordt niet uitgevoerd tijdens de taken reeks.

    > [!NOTE]
    > De ingeschakelde stappen in een uitgeschakelde groep worden nog steeds opgenomen in het totaal aantal.

## <a name="task-sequence-error"></a>Taken reeks fout

Als de taken reeks mislukt, wordt het venster met de **taken reeks fout** weer gegeven.

![Voor beeld van een taken reeks fout venster](media/task-sequence-error.png)

- U kunt de koptekst informatie op hetzelfde instellen als het voortgangs venster van de taken reeks.

- De naam van de taken reeks, een fout code en een algemeen bericht voor gebruikers worden weer gegeven. Bijvoorbeeld: `Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- Het venster wordt automatisch gesloten na een time-outperiode. Deze time-out is standaard 15 minuten. U kunt deze waarde aanpassen met de taken reeks variabele [SMSTSErrorDialogTimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout).

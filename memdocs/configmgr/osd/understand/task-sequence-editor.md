---
title: De takenreekseditor gebruiken
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van de editor voor taken reeksen in de Configuration Manager-console
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2047ae9e276ac94b633d1dc30814ed641cd34d03
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711425"
---
# <a name="use-the-task-sequence-editor"></a>De takenreekseditor gebruiken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Taken reeksen bewerken in de Configuration Manager-console met behulp van de **taken reeks editor**. Gebruik de editor voor het volgende:  

- Een weer gave met het kenmerk alleen-lezen van de taken reeks openen

- Stappen toevoegen aan of verwijderen uit de taken reeks  

- De volg orde van de stappen van de taken reeks wijzigen  

- Groepen van stappen toevoegen of verwijderen  

- Stappen kopiëren en plakken tussen taken reeksen

- Stap opties instellen, zoals of de taken reeks doorgaat als er een fout optreedt  

- Voor waarden toevoegen aan de stappen en groepen van een taken reeks  

- Voor waarden kopiëren en plakken tussen stappen in een taken reeks

- De taken reeks doorzoeken om snel stappen te vinden

Voordat u een taken reeks kunt bewerken, moet u deze maken. Zie [taken reeksen beheren en maken](../deploy-use/manage-task-sequences-to-automate-tasks.md)voor meer informatie.

## <a name="about-the-task-sequence-editor"></a>Over de taken reeks editor

De editor voor taken reeksen bevat de volgende onderdelen:

![Scherm opname van de voorbeeld taken reeks editor venster met aantekeningen](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. De naam van de taken reeks
2. Opdracht. Zie [zoeken](#bkmk_search)voor meer informatie.
3. **Eigenschappen** voor de geselecteerde groep of stap in de reeks

    Zie [over taken reeks stappen](task-sequence-steps.md)voor meer informatie over de eigenschappen en opties van een specifieke stap.

4. **Opties** voor de geselecteerde groep of stap in de reeks

    Zie [over taken reeks stappen](task-sequence-steps.md)voor meer informatie over algemene opties voor alle stappen of opties van een specifieke stap.

    Zie [voor waarden](#bkmk_conditions)voor meer informatie over het configureren van voor waarden.

5. Een groep of stappen **toevoegen**
6. Een groep of stappen **verwijderen**
7. Alle groepen samen vouwen of alle groepen uitvouwen
8. De positie van een groep of stap in de reeks verplaatsen (omhoog, omlaag)
9. De taken reeks:
    - Bekijk de volg orde van de stappen en groepen.
    - Een groep uitvouwen of samen vouwen.
    - Wanneer u een stap of groep uitschakelt op de **Opties**, wordt deze grijs weer gegeven in de reeks.
    - Het pictogram van een stap verandert in een rood fout als er een probleem is met de stap. Er ontbreekt bijvoorbeeld een vereiste waarde.
10. **OK**: opslaan en sluiten
11. **Annuleren**: sluiten zonder wijzigingen op te slaan
12. **Toep assen**: wijzigingen opslaan en open houden

U kunt de grootte van de taken reeks editor wijzigen met behulp van standaard Windows-besturings elementen. Als u de breedte van de twee hoofd vensters wilt verg Roten of verkleinen, gebruikt u de muis om de balk tussen de taken reeks en de stap eigenschappen te selecteren en sleept u deze naar links of rechts.

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a>Een taken reeks weer geven

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **taken reeksen** .  

2. Selecteer in de lijst **taken reeks** de taken reeks die u wilt weer geven.  

3. Klik op het tabblad **Start** van het lint in de groep **taken reeks** op **weer gave**.

    > [!TIP]
    > Dit is de standaard actie. Als u dubbelklikt op een taken reeks, **bekijkt** u de taken reeks.

Met deze actie wordt de taken reeks editor geopend in de modus alleen-lezen. In deze modus kunt u de volgende acties uitvoeren:

- Alle groepen, stappen, eigenschappen en opties weer geven
- Groepen uitvouwen en samen vouwen
- De taken reeks doorzoeken
- Het formaat van het editor venster wijzigen

In deze alleen-lezen modus kunt u geen wijzigingen aanbrengen, inclusief het kopiëren van een stap of voor waarde. Met deze actie wordt de taken reeks ook niet vergrendeld zodat deze kan worden bewerkt. Zie voor meer informatie over deze vergren deling [vergren delen voor het bewerken van taken reeksen](#bkmk_sedo).

Als u wijzigingen wilt aanbrengen in een taken reeks, sluit u de taken reeks editor die u hebt geopend in de modus alleen-lezen. [Bewerk](#bkmk_edit) vervolgens de taken reeks.

> [!NOTE]  
> Wanneer u een taken reeks bekijkt of bewerkt die is gemaakt met de wizard taken reeks maken, kan de naam van de stap de actie of het type van de stap zijn. U ziet bijvoorbeeld een stap met de naam ' partitie schijf 0 '. Dit is de actie voor een stap van het type [Format en Partition Disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk). Alle taken reeks stappen worden gedocumenteerd op basis van het *type*, niet noodzakelijkerwijs door de naam van de stap die wordt weer gegeven in de editor.  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a> Een takenreeks bewerken

Gebruik de volgende procedure om een bestaande taken reeks te wijzigen:  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **taken reeksen** .  

2. Selecteer in de lijst **Takenreeks** de takenreeks die u wilt bewerken.  

3. Selecteer **bewerken**op het tabblad **Start** van het lint in de groep **taken reeks** . Voer vervolgens een van de volgende acties uit:  

    - **Een stap toevoegen**: Selecteer **toevoegen**, selecteer een categorie en selecteer vervolgens de stap die u wilt toevoegen. Als u bijvoorbeeld de stap [opdracht regel uitvoeren](task-sequence-steps.md#BKMK_RunCommandLine) wilt toevoegen, selecteert **u toevoegen**, kiest u de categorie **Algemeen** en selecteert u vervolgens **opdracht regel uitvoeren**. Met deze actie wordt de stap toegevoegd na de momenteel geselecteerde stap.

    - **Een groep toevoegen**: Selecteer **toevoegen**en kies vervolgens **nieuwe groep**. Nadat u een groep hebt toegevoegd, voegt u er stappen aan toe.  

    - **De volg orde wijzigen**: Selecteer de stap of groep die u opnieuw wilt ordenen. Gebruik vervolgens de pictogrammen **omhoog** of **omlaag** . U kunt slechts één stap of groep op hetzelfde moment verplaatsen. Deze acties zijn ook beschikbaar wanneer u met de rechter muisknop op een groep of stap klikt.

        U kunt een groep of een stap knippen, kopiëren en plakken. Klik met de rechter muisknop op het item en selecteer de actie. U kunt ook standaard snel toetsen gebruiken voor elke actie:

        - Knippen: **CTRL** + **X**
        - Kopiëren: **CTRL** + **C**
        - Plakken: **CTRL** + **V**

    - **Een stap of groep verwijderen**: Selecteer de stap of groep en kies **verwijderen**.  

4. Selecteer **OK** om uw wijzigingen op te slaan en het venster te sluiten. Selecteer **Annuleren** om uw wijzigingen te negeren en het venster te sluiten. Selecteer **Toep assen** om uw wijzigingen op te slaan en de taken reeks editor geopend te houden.  

Zie [taken reeks stappen](task-sequence-steps.md)voor een lijst met de beschik bare taken reeks stappen.  

> [!IMPORTANT]  
> Als de taken reeks niet-gekoppelde verwijzingen naar een object bevat als resultaat van de bewerking, moet u de verwijzing corrigeren voordat deze kan worden gesloten. Mogelijke acties zijn:  
>
> - Corrigeer de verwijzing
> - Het niet-verwezen object verwijderen uit de taken reeks  
> - De mislukte taken reeks stap tijdelijk uitschakelen totdat de verbroken verwijzing is gecorrigeerd of verwijderd  

U kunt gelijktijdig meer dan één exemplaar van de taken reeks editor openen. Met dit gedrag kunt u meerdere taken reeksen vergelijken, of de stappen ertussen kopiëren en plakken. U kunt een taken reeks **bewerken** en een andere **weer geven** , maar niet beide acties voor dezelfde taken reeks.

## <a name="conditions"></a><a name="bkmk_conditions"></a>Nader

Gebruik voor waarden om te bepalen hoe de taken reeks zich gedraagt. Voor waarden toevoegen aan één stap of een groep van stappen. De taken reeks evalueert de voor waarden voordat de stap op het apparaat wordt uitgevoerd. De stap wordt alleen uitgevoerd als aan de voor waarden wordt voldaan. Als een voor waarde wordt geëvalueerd als onwaar, slaat de taken reeks de groep of stap over.

Gebruik het tabblad **Opties** om voor waarden te beheren:

![Voor waarden beheren op het tabblad Opties van de taken reeks editor](media/4621098-copy-paste-ts-condition.png)

De volgende typen voor waarden zijn beschikbaar:

- **If-instructie**: gebruik een *if* -instructie om voor waarden te groeperen. U kunt **alle voor waarden**, **elke voor waarde**of **geen**evalueren.

- **Taken reeks variabele**. Evalueer de huidige waarde van een ingebouwde, aangepaste of alleen-lezen [taken reeks variabele](task-sequence-variables.md) in de taken reeks omgeving. Zie voor meer informatie [stap voorwaarden](using-task-sequence-variables.md#bkmk_access-condition).

    > [!NOTE]
    > U kunt in dit voor waarde een matrix variabele gebruiken, maar u moet het specifieke matrixlid opgeven. Hiermee geeft u `OSDAdapter0EnableDHCP` bijvoorbeeld op of de *eerste* netwerk adapter DHCP ondersteunt. Zie [matrix variabelen](using-task-sequence-variables.md#bkmk_array)voor meer informatie.

- **Besturingssysteem versie**: Evalueer de versie van het besturings systeem van het apparaat waarop de taken reeks wordt uitgevoerd. Deze lijst bevat de algemene versies van het besturings systeem die in Configuration Manager worden gebruikt. Als u een gedetailleerdere versie van het besturings systeem, zoals een specifieke versie van Windows 10, wilt evalueren, gebruikt u de **WMI-** voor waarde voor de query.

- **Taal van besturings systeem**: Evalueer de taal van het besturings systeem van het apparaat waarop de taken reeks wordt uitgevoerd. Deze lijst bevat de 257 talen die door Windows worden ondersteund.

- **Bestands eigenschappen**: Controleer de versie of tijds tempel van elk bestand op het apparaat waarop de taken reeks wordt uitgevoerd.

- **Mapeigenschappen**: Controleer de tijds tempel van een wille keurige map op het apparaat waarop de taken reeks wordt uitgevoerd.

- **Register instelling**: Evalueer elke register sleutel waarde van het apparaat waarop de taken reeks wordt uitgevoerd.

- **Query uitvoeren op WMI**: Geef de naam ruimte en de query op die moet worden geëvalueerd op het apparaat waarop de taken reeks wordt uitgevoerd.

- **Geïnstalleerde software**: geef een Windows Installer bestand op om product informatie te laden die overeenkomt met het apparaat waarop de taken reeks wordt uitgevoerd. U kunt afstemmen op een specifiek product of een wille keurige versie van het product.

### <a name="cmdlets-for-conditions"></a>Cmdlets voor voor waarden

Voor waarden beheren met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConditionFile](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFile?view=sccm-ps)
- [Get-CMTSStepConditionFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFolder?view=sccm-ps)
- [Get-CMTSStepConditionIfStatement](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement?view=sccm-ps)
- [Get-CMTSStepConditionOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem?view=sccm-ps)
- [Get-CMTSStepConditionQueryWmi](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi?view=sccm-ps)
- [Get-CMTSStepConditionRegistry](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry?view=sccm-ps)
- [Get-CMTSStepConditionSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware?view=sccm-ps)
- [Get-CMTSStepConditionVariable](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionVariable?view=sccm-ps)

### <a name="copy-and-paste-conditions"></a>Voor waarden kopiëren en plakken

<!-- 4621098 -->

Als u de voor waarden van de ene stap naar de andere opnieuw wilt gebruiken, vanaf versie 1910 kunt u nu voor waarden kopiëren en plakken in de taken reeks editor. Selecteer een voor waarde die u wilt knippen of kopiëren. Als een voor waarde onderliggende items heeft, wordt het hele blok gekopieerd. Als er een voor waarde is op het klem bord, kunt u deze plakken met de volgende opties:

- Plakken vóór
- Plakken na
- Plakken onder (alleen van toepassing op geneste omstandigheden)

Standaard snel toetsen gebruiken om te kopiëren (**CTRL +** + **c**) en knippen (**CTRL** + **X**). De standaardtoetsen bord van **CTRL** + **V** heeft de actie **Plakken na** .

Er zijn ook nieuwe opties om voor waarden omhoog of omlaag te verplaatsen in de lijst.

> [!Note]  
> U kunt voor waarden tussen stappen in een taken reeks kopiëren en plakken. Deze actie wordt niet ondersteund tussen verschillende taken reeksen.

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a>Vergren deling voor bewerken terugclaimen

<!--3699337-->
Als de Configuration Manager-console niet meer reageert, kunt u de vergren deling vergren delen om verdere wijzigingen aan te brengen tot de vergrendeling na 30 minuten verloopt. Deze vergren deling maakt deel uit van de Configuration Manager SEDO (geserialiseerd editing of Distributed Objects). Zie [Configuration Manager Sedo](../../develop/core/understand/sedo.md)voor meer informatie.

Vanaf versie 1906 kunt u de vergren deling van een taken reeks wissen. Deze actie is alleen van toepassing op uw gebruikers account met de vergren deling en op hetzelfde apparaat waarvan de site de vergren deling heeft gekregen. Wanneer u probeert toegang te krijgen tot een vergrendelde taken reeks, kunt u nu de **wijzigingen negeren**en door gaan met het bewerken van het object. Deze wijzigingen zijn toch verloren gegaan wanneer de vergren deling is verlopen.

> [!TIP]
> Vanaf versie 1910 kunt u de vergren deling van een object in de Configuration Manager-console wissen. Zie [de Configuration Manager-console gebruiken](../../core/servers/manage/admin-console.md#bkmk_sedo)voor meer informatie.<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a>Opdracht

<!-- 4621085 -->

Als u een grote taken reeks hebt met veel groepen en stappen, kan het lastig zijn om specifieke stappen te vinden. Vanaf versie 1910 kunt u nu zoeken in de editor voor taken reeksen. Met deze actie kunt u sneller stappen in de taken reeks vinden.

![Zoeken in de taken reeks editor](media/4621085-task-sequence-search.png)

Voer een zoek term in om te starten. U kunt uw zoek opdracht bereiken met de volgende typen:

- Stap naam
- Stap beschrijving
- Type stap
- Groepsnaam
- Groepsbeschrijving
- Naam van de variabele
- Voorwaarden
- Andere inhoud, bijvoorbeeld teken reeksen zoals variabele waarden of opdracht regels

Alle scopes worden standaard ingeschakeld.

U kunt ook filteren op alle stappen met de volgende kenmerken:

- Door gaan bij fout
- Heeft voor waarden

Standaard wordt filter niet ingeschakeld.

Wanneer u zoekt, markeert het editor venster in geel de stappen die overeenkomen met uw zoek criteria.

Snel toegang krijgen tot deze zoek velden en door de zoek resultaten navigeren met de volgende sneltoetsen:

- **CTRL** + **F**: Voer een zoek reeks in
- **CTRL** + **O**: Selecteer de zoek opties om de resultaten te beperken
- **F3** of **Enter**: stapsgewijs door de resultaten gaan
- **Shift** + **F3**: een achterwaartse stap in de resultaten

## <a name="see-also"></a>Zie ook

- [Takenreeksen maken en beheren](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [Stappen voor takenreeksen](task-sequence-steps.md)

- [Takenreeksvariabelen gebruiken](using-task-sequence-variables.md)

- [De Configuration Manager-console gebruiken](../../core/servers/manage/admin-console.md)

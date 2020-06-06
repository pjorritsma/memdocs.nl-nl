---
title: Vooraf in cachegeheugen opgeslagen inhoud configureren
titleSuffix: Configuration Manager
description: Meer informatie over hoe clients besturingssysteem implementatie-inhoud kunnen downloaden voordat een gebruiker de taken reeks installeert.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec465f3dee33ca311aec120e74a2994a81a90ec9
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455222"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>Inhoud in de cache vooraf configureren voor taken reeksen

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1021244-->
Met de functie voor het vooraf opslaan van beschik bare implementaties van taken reeksen kunnen clients relevante inhoud downloaden voordat een gebruiker de taken reeks installeert. De client kan inhoud vooraf in de cache opslaan voor taken reeksen waarmee [een besturings systeem wordt bijgewerkt](create-a-task-sequence-to-upgrade-an-operating-system.md) of [een installatie kopie van een besturings systeem wordt geïnstalleerd](create-a-task-sequence-to-install-an-operating-system.md).

> [!Note]  
> In versie 1910 Configuration Manager deze functie standaard ingeschakeld. In versie 1906 of eerder is Configuration Manager deze optionele functie standaard niet ingeschakeld. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

U wilt bijvoorbeeld slechts één in-place upgrade taken reeks voor alle gebruikers en een groot aantal architecturen en talen hebben. In vorige versies wordt de inhoud gedownload wanneer de gebruiker een beschik bare taken reeks implementatie installeert vanuit software Center. Deze vertraging voegt extra tijd toe voordat de installatie gereed is om te starten. Alle inhoud waarnaar in de taken reeks wordt verwezen, wordt gedownload. Deze inhoud bevat het upgrade pakket voor het besturings systeem voor alle talen en architecturen. Als elk upgrade pakket ongeveer 3 GB groot is, is de totale inhoud zeer groot.

Inhoud vooraf-cache biedt u de mogelijkheid om de client alleen de toepasselijke inhoud en alle andere inhoud waarnaar wordt verwezen, te downloaden zodra de implementatie wordt ontvangen. Wanneer de gebruiker op **installeren** in Software Center klikt, is de inhoud gereed. De installatie wordt snel gestart, omdat de inhoud zich op de lokale harde schijf bevindt.

In Configuration Manager versie 1902 en eerder is dit gedrag alleen van toepassing op het *upgrade pakket van het besturings systeem*. Dat pakket is de enige inhoud waarop u de overeenkomende architectuur of taal opgeeft. Als de taken reeks bijvoorbeeld ook verwijst naar meerdere Stuur programmapakketten, downloadt de client deze allemaal. De taken reeks engine evalueert de voor waarden voor de stappen wanneer de taken reeks wordt uitgevoerd, en niet vooraf. De-client gebruikt de tags in de pakket eigenschappen om te bepalen welke inhoud vooraf in de cache wordt opgeslagen.

Vanaf versie 1906,<!--4224642--> u kunt vooraf-caching gebruiken om het bandbreedte verbruik van de volgende inhouds typen te verminderen:

- OS-upgrade pakketten
- Installatiekopieën van het besturingssysteem
- Driverpakketten
- Pakketten

## <a name="configure-pre-caching"></a>Caching vooraf configureren

Er zijn drie stappen voor het configureren van de functie vooraf-cache:

1. [De pakketten maken en configureren](#bkmk_createpkg)
2. [Een taken reeks met voorwaardelijke stappen maken](#bkmk_createts)
3. [De taken reeks implementeren en vooraf opslaan in cache inschakelen](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a>1. de pakketten maken en configureren

De-client evalueert de kenmerken van de pakketten om te bepalen welke inhoud wordt gedownload tijdens de voor bereiding van de cache.  

#### <a name="os-upgrade-package"></a>OS-upgrade pakket

[OS-upgrade pakketten](../get-started/manage-operating-system-upgrade-packages.md) maken voor specifieke architecturen en talen. Geef de **architectuur** en **taal** op het tabblad **gegevens bron** van de eigenschappen op.

#### <a name="os-image"></a>Installatie kopie van besturings systeem

[Installatie kopieën van het besturings systeem](../get-started/manage-operating-system-images.md) maken voor specifieke architecturen en talen. Geef de **architectuur** en **taal** op het tabblad **gegevens bron** van de eigenschappen op.

#### <a name="driver-package"></a>Stuurprogrammapakket

[Stuur programmapakketten](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages) maken voor specifieke hardware-modellen. Geef het **model** op het tabblad **Algemeen** van de eigenschappen op.

Om te bepalen welk Stuur programmapakket wordt gedownload tijdens de voor bereiding van de cache, evalueert de client het model met de **naam** eigenschap van de WMI-klasse **Win32_ComputerSystemProduct** .

> [!TIP]
> De werkelijke query gebruikt een `LIKE` instructie met Joker tekens: `select * from win32_computersystemproduct where name like "%yourstring%"` . Als u bijvoorbeeld opgeeft `Surface` als het model, wordt de query overeenkomt met alle modellen die die teken reeks bevatten.<!-- 6315551 -->

#### <a name="package"></a>Pakket

Maak [pakketten](../../apps/deploy-use/packages-and-programs.md) voor specifieke architecturen en talen. Geef de **architectuur** en **taal** op het tabblad **Algemeen** van de eigenschappen op.


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a>2. een taken reeks maken

Maak een taken reeks met voorwaardelijke stappen voor de verschillende talen en architecturen of verschillende hardware-modellen voor Stuur programmapakketten.

|Inhoud|Stap|
|---------|---------|
|OS-upgrade pakket|[Besturings systeem bijwerken](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|Installatie kopie van besturings systeem|[Installatie kopie van besturings systeem Toep assen](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|Stuurprogrammapakket|[Stuurprogrammapakket toepassen](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|Pakket|[Pakket installeren](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

In de volgende stap van het **besturings systeem** voor de upgrade wordt bijvoorbeeld de Engelse versie gebruikt:  

![Taken reeks editor met meerdere stappen voor het bijwerken van het besturings systeem voor ENU, DEU en JPN](../media/precacheproperties2.png)

![Taken reeks editor, tabblad Opties, waarin de WMI WQL-query voor land instellingen en OSArchitecture wordt weer gegeven](../media/precacheoptions2.png)  

> [!Tip]
> De volgende WMI-query wordt aanbevolen voor de Engelse versie van het besturings systeem (Verenigde Staten) en de 64-bits architectuur:
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> Voeg eerst de taal toe door de taal voorwaarde voor het **besturings systeem** te selecteren. Bewerk vervolgens de WMI-query om de component architecture toe te voegen.

### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a>3. de taken reeks implementeren

[Implementeer de taken reeks](deploy-a-task-sequence.md). Configureer de volgende instellingen voor de functie vóór de cache:  

- Selecteer op het tabblad **Algemeen** de optie **inhoud vooraf downloaden voor deze taken reeks**.  

- Configureer op het tabblad **implementatie-instellingen** de taken reeks als **beschikbaar**.  

- Kies op het tabblad **planning** de momenteel geselecteerde tijd voor de instelling, **plannen wanneer deze implementatie beschikbaar**is. De client start de inhoud vooraf in het cache geheugen op de beschik bare tijd van de implementatie. Wanneer een doel client dit beleid ontvangt, ligt de beschik bare tijd in het verleden, waardoor de vooraf-cache down load meteen wordt gestart. Als de client dit beleid ontvangt, maar de beschik bare tijd in de toekomst ligt, start de client de inhoud niet vooraf in het cache geheugen voordat de beschik bare tijd wordt weer gegeven.  

- Configureer op het tabblad **distributie punten** de instellingen voor de **implementatie opties** . Als de inhoud niet vooraf in de cache wordt opgeslagen voordat een gebruiker de installatie start, gebruikt de client deze instellingen.  

    > [!Important]  
    > Voor een taken reeks die een installatie kopie van een besturings systeem installeert, gebruikt u niet de implementatie optie om **inhoud lokaal te downloaden wanneer deze nodig is voor de taken reeks die wordt uitgevoerd**. Wanneer de taken reeks de schijf gewist voordat de installatie kopie van het besturings systeem wordt toegepast, wordt de client cache verwijderd. Omdat de inhoud is verdwenen, mislukt de taken reeks.<!-- SCCMDocs-PR #1338 --> Deze implementatie opties zijn dynamisch op basis van andere opties die u voor de implementatie selecteert. Zie [Een takenreeks implementeren](deploy-a-task-sequence.md#bkmk_deploy-options)voor meer informatie.<!-- MEMDocs#328, SCCMDocs#2114 -->

## <a name="user-experience"></a>Gebruikerservaring

- Wanneer de client het implementatie beleid ontvangt, wordt de inhoud vooraf in de cache geplaatst na de beschik bare tijd van de implementatie. Deze inhoud bevat alle pakketten waarnaar wordt verwezen, maar alleen het upgrade pakket van het besturings systeem dat overeenkomt met de architectuur en taal kenmerken van het pakket.  

- Wanneer de-client de implementatie beschikbaar maakt voor gebruikers, wordt een melding weer gegeven om gebruikers te informeren over de nieuwe implementatie. Nu is de taken reeks zichtbaar in Software Center. De gebruiker kan naar Software Center gaan en op **installeren** klikken om de installatie te starten.  

- Als de-client de inhoud niet volledig in de cache plaatst wanneer de gebruiker de taken reeks installeert, gebruikt de client de instellingen die u opgeeft op het tabblad **implementatie optie** van de implementatie.  

## <a name="see-also"></a>Zie ook

- [Een takenreeks maken voor het bijwerken van een besturingssysteem](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [Scenario voor het upgraden van Windows naar de nieuwste versie](upgrade-windows-to-the-latest-version.md)

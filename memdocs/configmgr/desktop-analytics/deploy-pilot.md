---
title: Implementeren naar pilot
titleSuffix: Configuration Manager
description: Een hand leiding voor het implementeren van een desktop Analytics-test groep.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0e939b51c464215ac1d4feea539ceb5677a01a6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723682"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Implementeren voor pilot met Desktop Analytics

Een van de voor delen van Desktop Analytics is om de kleinste set apparaten te identificeren die de breedste dekking van factoren bieden. Het richt zich op de factoren die het belangrijkst zijn voor een pilot van Windows-upgrades en-updates. Als u er zeker van wilt zijn dat de pilot meer succes heeft, kunt u sneller en veiliger overstappen op grote implementaties in de productie omgeving.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

## <a name="identify-devices"></a>Apparaten identificeren

De eerste stap is het identificeren van apparaten die moeten worden meegenomen in de pilot. Desktop Analytics raadt apparaten aan op basis van de gerapporteerde gegevens en u kunt apparaten in deze lijst opnemen of vervangen.

1. Ga naar de [Desktop Analytics-Portal](https://aka.ms/desktopanalytics)en selecteer in de groep beheren de optie **implementatie plannen**.

1. Selecteer een implementatie plan.

1. Selecteer in de groep voor bereiding van het implementatie plan de optie **pilot identificeren**.

De gegevens van Desktop Analytics worden weer gegeven met het aantal apparaten dat wordt aanbevolen, inclusief voor de beste dekking. Dit algoritme is voornamelijk gebaseerd op het gebruik van belang rijke en kritieke apps en de breedte van hardwareconfiguraties.

Voer de volgende acties uit voor de lijst met aanvullende aanbevolen apparaten:

- **Alles toevoegen aan de pilot**: Hiermee worden alle aanbevolen apparaten toegevoegd aan de test groep
- **Toevoegen aan pilot**: alleen afzonderlijke apparaten toevoegen
- Alle specifieke apparaten **vervangen** door de pilot

Wanneer u apparaten toevoegt van de **Aanbevolen** lijst, worden de dekking en redundantie voor uw kritieke en belang rijke assets **in de pilot** verhoogd. Een hogere redundantie betekent dat de activa die worden behandeld, een statistisch aanzienlijk aantal apparaten in uw pilot hebben.

## <a name="global-pilot"></a><a name="bkmk_GlobalPilot"></a>Wereld wijde pilot

U kunt ook op het hele systeem beslissingen nemen over welke Configuration Manager verzamelingen moeten worden opgenomen of uitgesloten van Pilots. Selecteer in het hoofd menu van Desktop Analytics in de groep globale instellingen de optie **globale pilot**.

Als u meerdere Configuration Manager-hiërarchieën verbindt met hetzelfde bureau blad Analytics-exemplaar, wordt in een weergave naam voor de hiërarchie de naam van de verzameling voor voegsels in de globale pilot configuratie. Deze naam is de **weergave naam** eigenschap in de verbinding met de bureau blad Analytics in de Configuration Manager-console.<!-- 4814075 -->

> [!NOTE]
> Ondersteuning voor meerdere hiërarchieën vereist Configuration Manager versie 1910 of hoger.

- Neem geen verzamelingen op die meer dan 20% van uw totale geregistreerde apparaten bevatten voor desktop Analytics. Als u een grote verzameling opneemt, wordt er een waarschuwing weer gegeven in de portal. U kunt meerdere kleine verzamelingen zonder waarschuwing toevoegen, maar nog steeds voorzichtig zijn met het aantal apparaten in uw pilot. <!-- 6079184 -->

- Voor nauw keurige pilot aanbevelingen voor implementatie plannen in een specifieke Configuration Manager-hiërarchie, moet u alleen verzamelingen uit die hiërarchie bevatten.

### <a name="example"></a>Voorbeeld

- U configureert de verbinding met de bureau blad Analytics in Configuration Manager voor de verzameling **alle systemen** . Met deze actie worden alle clients bij de service geregistreerd.

- U kunt ook extra verzamelingen configureren om te synchroniseren met Desktop Analytics:

  - Alle Windows 10-clients (3.000 apparaten)

  - Alle IT-apparaten (200 totaal aantal apparaten, 150 van waarop Windows 10 wordt uitgevoerd)

  - CEO Office (20 apparaten)

- In de **globale pilot** -instellingen voegt u de **Windows 10-clients** verzamelingen toe. U sluit de **CEO Office** -verzameling uit.

- U maakt een implementatie plan en selecteert **alle IT-apparaten** verzameling als uw **doel groep**. U bent van plan dit implementatie plan alleen voor apparaten in de IT-afdeling.

- De lijst met **opgenomen pilot-apparaten** bevat de subset van apparaten die zich in **de doel groep**BEvinden: **alle IT-apparaten** en de lijst met algemene proef *insluitingen* : **alle Windows 10-clients**. 150-apparaten bevinden zich in deze lijst, omdat alleen 150-apparaten in de verzameling **alle IT-apparaten** Windows 10 uitvoeren.

- De lijst met **extra aanbevolen apparaten** bevat een set apparaten uit uw **doel groep** die maximale dekking en redundantie voor uw belang rijke assets bieden. In deze lijst wordt geen enkel apparaat in de lijst met *uitsluitingen* van globale Pilotes van de Blade Analytics uitgesloten: **CEO Office**.

## <a name="address-issues"></a>Problemen oplossen

Gebruik de Desktop Analytics-Portal om gerapporteerde problemen met activa te bekijken die uw implementatie kunnen blok keren. Goed keuren, afwijzen of wijzigen van de voorgestelde correctie. Alle items moeten worden gemarkeerd als **gereed** of **gereed (met herbemiddeling)** voordat de test implementatie wordt gestart.

1. Ga naar de [Desktop Analytics-Portal](https://aka.ms/desktopanalytics)en selecteer in de groep beheren de optie **implementatie plannen**.  

2. Selecteer een implementatie plan.  

3. Selecteer **pilot voorbereiden**in de groep voor bereiding van het implementatie plan.  

4. Controleer op het tabblad **apps** de apps waarvoor uw invoer nodig is.  

5. Voor elke app selecteert u de naam van de app. Bekijk de aanbeveling in het informatie venster en selecteer de upgrade beslissing. Als u ervoor kiest **niet** te **controleren of niet**, dan bevat Desktop Analytics geen apparaten met deze app in de test implementatie. Als u **gereed (met herstel)** kiest, gebruikt u de **herstel notities** om de acties vast te leggen die u moet uitvoeren om een probleem op te lossen, zoals *opnieuw installeren* of *de aanbevolen versie van de fabrikant zoeken*.

6. Herhaal deze beoordeling voor andere assets.  

Zie [compatibiliteits beoordeling](compat-assessment.md)voor meer informatie over dit controle proces.

## <a name="create-software"></a>Software maken

Voordat u Windows kunt implementeren, moet u eerst de software-objecten in Configuration Manager maken. Zie [Windows 10 in-place upgrade taken reeks](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)voor meer informatie.

## <a name="deploy-to-pilot-devices"></a>Implementeren op pilot-apparaten

Configuration Manager gebruikt de gegevens uit de Desktop Analytics om verzamelingen te maken voor de test-en productie-implementaties. Om ervoor te zorgen dat apparaten in orde zijn na elke implementatie fase, gebruikt u de volgende procedure voor het maken van een door een bureau blad Analytics geïntegreerde, gefaseerde implementatie:

1. Ga in de Configuration Manager-console naar de **software bibliotheek**, vouw **Desktop Analytics Servicing**uit en selecteer het knoop punt **implementatie plannen** .  

2. Selecteer uw implementatie plan en selecteer vervolgens Details van het **implementatie plan** in het lint.  

3. Selecteer **gefaseerde implementatie maken** op het lint. Met deze actie wordt de wizard gefaseerde implementatie maken gestart.

    > [!Tip]  
    > Als u een klassieke taken reeks implementatie voor alleen de pilot verzameling wilt maken, selecteert u **implementeren** in de tegel status van de **pilot** . Met deze actie wordt de wizard software implementeren gestart. Zie [Een takenreeks implementeren](../osd/deploy-use/deploy-a-task-sequence.md)voor meer informatie.  

4. Voer een naam in voor de implementatie en selecteer de taken reeks die u wilt gebruiken. Gebruik de optie om **automatisch een standaard implementatie met twee fasen te maken**en configureer vervolgens de volgende verzamelingen:  

    - **Eerste verzameling**: Zoek en selecteer de **pilot** verzameling voor dit implementatie plan. De standaard naam Conventie voor deze verzameling is `<deployment plan name> (Pilot)`.

    - **Tweede verzameling**: Zoek en selecteer de **productie** verzameling voor dit implementatie plan. De standaard naam Conventie voor deze verzameling is `<deployment plan name> (Production)`.

    > [!Note]  
    > Met de integratie van het bureau blad Analytics maakt Configuration Manager automatisch pilot-en productie verzamelingen voor het implementatie plan. Voordat u deze kunt gebruiken, kan het enige tijd duren voordat deze verzamelingen worden gesynchroniseerd. Zie [problemen oplossen-gegevens latentie](troubleshooting.md#data-latency)voor meer informatie.<!-- 4984639 -->
    >
    > Deze verzamelingen zijn gereserveerd voor apparaten met een desktop Analytics-implementatie plan. Hand matige wijzigingen in deze verzamelingen worden niet ondersteund.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Voltooi de wizard om de gefaseerde implementatie te configureren. Zie voor meer informatie [gefaseerde implementaties maken](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

    > [!Note]  
    > Gebruik de standaard instelling om **deze fase automatisch te starten na een uitstel periode (in dagen)**. De tweede fase kan pas worden gestart als aan de volgende criteria is voldaan:
    >
    > 1. In de eerste fase worden de criteria voor het slagen van de **implementatie** van succes bereikt. U configureert deze instelling voor de gefaseerde implementatie.
    > 1. U moet upgrade beslissingen controleren en nemen in Desktop Analytics om belang rijke en kritieke assets te markeren als *gereed*. Zie [activa bekijken waarvoor een upgrade beslissing is vereist](deploy-prod.md#bkmk_review)voor meer informatie.
    > 1. Desktop Analytics wordt gesynchroniseerd met de Configuration Manager verzamelingen productie apparaten die voldoen aan de *gereede* criteria.

> [!Important]  
> Deze verzamelingen blijven synchroniseren wanneer hun lidmaatschap wordt gewijzigd. Als u bijvoorbeeld een probleem met een Asset identificeert en dit markeert als **niet**, voldoen apparaten met dat activum niet meer aan de *gereede* criteria. Deze apparaten worden verwijderd uit de productie-implementatie verzameling.

## <a name="monitor"></a>Controleren

### <a name="configuration-manager-console"></a>Configuration Manager-console

Open het implementatie plan. De **voor bereiding van upgrade beslissingen-algemene status** tegel biedt een samen vatting van de status van het implementatie plan. Deze status is voor uw pilot-en productie verzameling. Apparaten kunnen in een van de volgende categorieën vallen:

- **Up-to-date**: apparaten zijn bijgewerkt naar de doel-Windows-versie voor dit implementatie plan

- **Update besluit voltooid**: een van de volgende statussen:

  - Apparaten met vermakene activa die **klaar** of **klaar zijn met herbemiddeling**

  - De apparaatstatus is **geblokkeerd**, het apparaat [**vervangen**](about-deployment-plans.md#plan-assets) of het **apparaat opnieuw installeren**

- **Niet gecontroleerd**: apparaten met een **onverwerkte** activa die **niet worden gecontroleerd** of worden gecontroleerd

De apparaatstatus worden bijgewerkt met de volgende acties in de **test status** en **productie status** tegels:

- U wijzigingen aanbrengt in de compatibiliteits beoordeling
- Apparaten worden bijgewerkt naar de doel versie van Windows
- De implementatie wordt uitgevoerd

U kunt Configuration Manager implementatie bewaking ook gebruiken als andere taken reeks implementaties. Zie [implementaties van besturings systemen bewaken](../osd/deploy-use/monitor-operating-system-deployments.md)voor meer informatie.

### <a name="desktop-analytics-portal"></a>Desktop Analytics-Portal

Gebruik de [Desktop Analytics-Portal](https://aka.ms/desktopanalytics) om de status van een implementatie plan weer te geven. Selecteer het implementatie plan en selecteer vervolgens **overzicht abonnement**.

![Scherm opname van het implementatie plan Overview in Desktop Analytics](media/deployment-plan-overview.png)

Selecteer de tegel **pilot** . Hiermee wordt de huidige status van de test implementatie samenvatten. In deze tegel worden ook gegevens weer gegeven voor het aantal apparaten dat niet is gestart, in uitvoering, voltooid of het retour neren van problemen.

Apparaten die fouten rapporteren of andere problemen worden ook weer gegeven in het detail gebied pilot aan de rechter kant. Selecteer **beoordeling**om details van het gemelde probleem te verkrijgen. Met deze actie wordt de weer gave op de pagina **Implementatie status** gewijzigd

Op de pagina **Implementatie status** vindt u een lijst met apparaten in de volgende categorieën:

- Niet gestart
- Wordt uitgevoerd
- Voltooid
- Aandacht vereist: apparaten
- Aandacht vereist: problemen

De **attentie** categorieën van vereisten geven dezelfde informatie weer, maar worden anders gesorteerd.

Selecteer een specifieke vermelding in de weer gave om meer informatie over het gedetecteerde probleem te krijgen.

Wanneer u deze implementatie problemen verhelpt, blijft het dash board de voortgang van apparaten weer geven. De IT-service wordt bijgewerkt wanneer de **vereisten** van de apparaten worden verplaatst naar **voltooid**.

## <a name="next-steps"></a>Volgende stappen

Laat de test gedurende een tijdje uitvoeren om operationele gegevens te verzamelen. Moedig gebruikers van pilot-apparaten aan om apps te testen.

Als uw test implementatie voldoet aan de criteria voor succes, gaat u naar het volgende artikel om te implementeren in productie.
> [!div class="nextstepaction"]  
> [Implementeren voor productie](deploy-prod.md)  

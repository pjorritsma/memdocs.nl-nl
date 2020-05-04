---
title: Een toepassing maken en implementeren
titleSuffix: Configuration Manager
description: Maak en implementeer een toepassing met een line-of-Business-app en lees hoe u apps effectief kunt beheren.
ms.date: 07/19/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b2d2a3465aebf66db37722629991078093abaaa7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710508"
---
# <a name="create-and-deploy-an-application-with-configuration-manager"></a>Een toepassing maken en implementeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit onderwerp gaat u meteen aan de slag en maakt u een toepassing met Configuration Manager. In dit voor beeld maakt en implementeert u een toepassing die een line-of-Business-app bevat voor Windows-Pc's met de naam **contoso. msi**, die moet worden geïnstalleerd op alle computers met Windows 10 in uw bedrijf. U leert hoe veel van de dingen die u kunt doen om toepassingen effectief te beheren.  

 Deze procedure is ontworpen om u een overzicht te geven van het maken en implementeren van Configuration Manager-toepassingen. Dit geldt echter niet voor alle configuratie opties of het maken en implementeren van toepassingen voor andere platforms.  

 Zie een van de volgende onderwerpen voor specifieke details die relevant zijn voor elk platform:  

- [Windows-toepassingen maken](creating-windows-applications.md)
- [Windows Phone-toepassingen maken](../../mdm/deploy-use/management-tasks-applications.md#bkmk_winphone)
- [Mac-computertoepassingen maken](creating-mac-computer-applications.md)
- [Linux- en UNIX-servertoepassingen maken](creating-linux-and-unix-server-applications.md)
- [Windows Embedded-toepassingen maken](creating-windows-embedded-applications.md)


Als u al bekend bent met Configuration Manager-toepassingen, kunt u dit onderwerp overs Laan. Het is echter mogelijk dat u de optie voor het [maken van toepassingen](../../apps/deploy-use/create-applications.md) wilt bekijken voor meer informatie over de opties die beschikbaar zijn wanneer u toepassingen maakt en implementeert.  

## <a name="before-you-start"></a>Voordat u begint  

Zorg ervoor dat u de informatie in [Inleiding tot toepassings beheer](../understand/introduction-to-application-management.md) hebt bekeken, zodat u uw site hebt voor bereid op het installeren van toepassingen en u de terminologie begrijpt die in dit onderwerp wordt gebruikt.  

 Zorg er ook voor dat de installatie bestanden voor de app **contoso. msi** zich op een toegankelijke locatie in uw netwerk bevinden.  

## <a name="create-the-configuration-manager-application"></a>De Configuration Manager-toepassing maken  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>De wizard toepassing maken starten en de toepassing maken  

1. Kies **software bibliotheek** > toepassingen voor**toepassings beheer** > in de Configuration Manager-**console.**  

2. Kies op het tabblad **Start** in de groep **maken** de optie **toepassing maken**.  

3. Kies op de pagina **Algemeen** van de **wizard toepassing maken**de optie **automatisch informatie over deze toepassing detecteren uit installatie bestanden**. Hiermee wordt een deel van de informatie in de wizard vooraf ingevuld met informatie die is geëxtraheerd uit het MSI-installatie bestand. Geef vervolgens de volgende gegevens op:  

   - **Type**: Kies **Windows Installer (\*MSI-bestand)**.  

   - **Locatie**: Typ de locatie (of kies **Bladeren** om de locatie te selecteren) van het installatie bestand **contoso. msi**. Houd er rekening mee dat de locatie moet worden opgegeven in de vorm * \\\Server\Share\File* voor Configuration Manager om de installatie bestanden te vinden.  

   Er wordt een item weer gegeven dat er ongeveer zo uitziet als in de volgende scherm afbeelding:  

   ![Algemene pagina voor de wizard app Management](media/App-management-wizard-general-page.png)  

4. Kies **Volgende**. Op de pagina **informatie importeren** ziet u enkele informatie over de app en alle bijbehorende bestanden die zijn geïmporteerd in Configuration Manager. Wanneer u klaar bent, kiest u opnieuw **volgende** .  

5. Op de pagina **algemene informatie** kunt u meer informatie over de toepassing opgeven om deze te sorteren en te zoeken in de Configuration Manager-console.  

    Daarnaast kunt u in het veld **installatie programma** de volledige opdracht regel opgeven die wordt gebruikt om de toepassing op pc's te installeren. U kunt dit bewerken om uw eigen eigenschappen toe te voegen (bijvoorbeeld **/q** voor een installatie zonder toezicht).  

   > [!TIP]  
   > Bepaalde velden op deze pagina van de wizard mogelijk zijn mogelijk automatisch ingevuld toen u de installatiebestanden van de toepassing importeerde.  

    Er wordt een scherm weer gegeven dat er ongeveer als volgt uitziet:  

    ![Pagina met algemene informatie over de wizard voor het beheer van apps](media/App-management-wizard-general-information-page.png)  

6. Kies **Volgende**. Op de pagina samen vatting kunt u de toepassings instellingen bevestigen en vervolgens de wizard volt ooien.  

   De app is gemaakt. Als u deze wilt vinden, vouwt u in de werk ruimte **software bibliotheek** het knoop punt **toepassings beheer**uit en kiest u vervolgens **toepassingen**. Voor dit voorbeeld wordt het volgende weergegeven:  

   ![Uiteindelijke afbeelding van app](media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>De eigenschappen en het implementatietype van de toepassing bekijken  

Nu u een toepassing hebt gemaakt, kunt u indien nodig de toepassings instellingen verfijnen. Als u de toepassings eigenschappen wilt bekijken, selecteert u de app en klikt u vervolgens op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

 In het dialoog venster **<eigenschappen van Contoso\> -toepassing** ziet u veel items die u kunt configureren om het gedrag van de toepassing te verfijnen. Zie [toepassingen maken](../../apps/deploy-use/create-applications.md)voor meer informatie over alle instellingen die u kunt configureren. In dit voorbeeld wijzigt u enkele eigenschappen van het implementatietype van de toepassing.  

 Kies het tabblad **implementatie typen** > implementatie type **Contoso-toepassing** > **bewerken**.

Er wordt een soortgelijk dialoogvenster als hier weergegeven:  

![Eigenschappen pagina app-beheer toepassing](media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Een vereiste toevoegen aan het implementatietype

 Vereisten specificeren voorwaarden waaraan moet worden voldaan voordat een toepassing kan worden geïnstalleerd op een apparaat.  U kunt kiezen uit de ingebouwde vereisten of u kunt uw eigen behoeften maken. In dit voor beeld voegt u een vereiste toe dat de toepassing alleen wordt geïnstalleerd op computers met Windows 10.  

1. Klik op de pagina eigenschappen van implementatie type die u zojuist hebt geopend, op het tabblad **vereisten** .  

2. Kies **toevoegen** om het dialoog venster **vereiste maken** te openen.  

3. Geef in het dialoogvenster **Vereiste maken** de volgende informatie op:  

    - **Categorie**: **apparaat**  

    - **Voor waarde**: **besturings systeem**  

    - **Regel type**: **waarde**  

    - **Operator**: **een van**  

    - Selecteer in de lijst met besturingssystemen **Windows 10**.  

    Het volgende dialoogvenster wordt weergegeven:  

    ![Pagina vereisten voor app-beheer](media/App-management-requirements-page.png)  

4. Kies **OK** om elke eigenschappen pagina die u hebt geopend, te sluiten. Ga vervolgens terug naar de lijst met **toepassingen** in de Configuration Manager-console.  

> [!TIP]  
> Met vereisten kunt u het aantal Configuration Manager verzamelingen beperken dat u nodig hebt. Omdat u zojuist hebt opgegeven dat de toepassing alleen kan worden geïnstalleerd op computers met Windows 10, kunt u dit later implementeren voor een verzameling met Pc's die veel verschillende besturings systemen uitvoeren. De toepassing wordt echter alleen op Windows 10-Pc's geïnstalleerd.

## <a name="add-the-application-content-to-a-distribution-point"></a>De toepassingsinhoud toevoegen aan een distributiepunt  

Als u de toepassing vervolgens op Pc's wilt implementeren, moet u ervoor zorgen dat de toepassings inhoud naar een distributie punt wordt gekopieerd. Pc's hebben toegang tot het distributie punt om de toepassing te installeren.  

> [!TIP]  
> Zie [inhoud en infra structuur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)voor inhoud beheren voor meer informatie over distributie punten en inhouds beheer in Configuration Manager.

1. Kies in de Configuration Manager-console de optie **software bibliotheek**.  

2. Vouw **toepassingen**uit in de werk ruimte **software bibliotheek** . Selecteer vervolgens in de lijst met toepassingen de contoso- **toepassing** die u hebt gemaakt.  

3. Klik op het tabblad **Start** in de groep **implementatie** op **inhoud distribueren**.  

4. Controleer op de pagina **Algemeen** van de **wizard inhoud distribueren**of de naam van de toepassing juist is en klik vervolgens op **volgende**.  

5. Controleer op de pagina **inhoud** de gegevens die naar het distributie punt worden gekopieerd en klik vervolgens op **volgende**.  

6. Kies op de pagina **doel** van inhoud **toevoegen** een of meer distributie punten of distributiepunt groepen waarop u de toepassings inhoud wilt installeren.  

7. Voltooi de wizard.  

U kunt controleren of de inhoud van de toepassing is gekopieerd naar het distributie punt vanuit de werk ruimte **bewaking** , onder status van **distributie status** > **inhoud**.  

## <a name="deploy-the-application"></a>De toepassing implementeren  

Vervolgens implementeert u de toepassing voor een apparaatverzameling in uw hiërarchie. In dit voor beeld implementeert u de toepassing in de apparaat verzameling **alle systemen** .  

> [!TIP]  
> Houd er rekening mee dat alleen Windows 10-computers de toepassing zullen installeren vanwege de vereisten die u eerder hebt geselecteerd.

1. Kies **software bibliotheek** > toepassingen voor**toepassings beheer** > in de Configuration Manager-**console.**  

2. Selecteer in de lijst met toepassingen de toepassing die u eerder hebt gemaakt (**Contoso-toepassing**) en kies vervolgens op het **tabblad Start** in de groep **implementatie** de optie **implementeren**.  

3. Klik op de pagina **Algemeen** van de **wizard software implementeren**op **Bladeren** om de apparaat-verzameling **alle systemen** te selecteren.  

4. Controleer op de pagina **inhoud** of het distributie punt is geselecteerd van waaruit u wilt dat pc's worden geïnstalleerd.  

5. Controleer op de pagina **implementatie-instellingen** of de implementatie actie is ingesteld op **installeren**en of het implementatie doel is ingesteld op **vereist**.  

    > [!TIP]  
    > Als u het implementatie doel instelt op **vereist**, zorgt u ervoor dat de toepassing wordt geïnstalleerd op computers die voldoen aan de vereisten die u instelt. Als u deze waarde instelt op **Beschikbaar**, kunnen gebruikers de toepassing op verzoek vanuit Software Center installeren.

6. Op de pagina **Planning** kunt u configureren wanneer de toepassing wordt geïnstalleerd. Selecteer voor dit voorbeeld **Zo snel mogelijk na het beschikbaar komen**.  

7. Kies op de pagina **gebruikers ervaring** **volgende** om de standaard waarden te accepteren.  

8. Voltooi de wizard.  

Gebruik de informatie in de volgende sectie **de toepassing bewaken** om de status van de toepassings implementatie te bekijken.  

## <a name="monitor-the-application"></a>Monitoren van de toepassing

 In deze sectie gaat u een kort overzicht bekijken van de implementatie status van de toepassing die u zojuist hebt geïmplementeerd.  

### <a name="to-review-the-deployment-status"></a>De implementatiestatus controleren  

1. Kies in de Configuration Manager-console **bewakings** > **implementaties**.  

2. Selecteer in de lijst met implementaties **Contoso-toepassing**.  

3. Klik op het tabblad **Start** in de groep **implementatie** op **status weer geven**.  

4. Selecteer een van de volgende tabbladen om meer status updates te bekijken over de implementatie van de toepassing:  

    - **Geslaagd**: de toepassing is geïnstalleerd op de aangegeven pc's.  

    - Wordt uitgevoerd: de installatie **van**de toepassing is nog niet voltooid.  

    - **Fout**: er is een fout opgetreden tijdens het installeren van de toepassing op de aangegeven pc's. Er wordt ook meer informatie over de fout weergegeven.  

    - **Niet voldaan aan vereisten**: er is geen installatie poging gedaan op de aangegeven apparaten omdat deze niet voldoen aan de vereisten die u hebt geconfigureerd (in dit voor beeld omdat ze niet worden uitgevoerd in Windows 10).  

    - **Onbekend**: de status van de implementatie kan niet door Configuration Manager worden gerapporteerd. Probeer het later opnieuw.  

> [!TIP]  
> Er zijn een paar manieren waarop u toepassings implementaties kunt bewaken. Zie [toepassingen bewaken](../deploy-use/monitor-applications-from-the-console.md)voor meer informatie.

## <a name="end-user-experience"></a>De ervaring voor de eindgebruiker  

Gebruikers die beschikken over Pc's die worden beheerd door Configuration Manager en Windows 10 uitvoeren, zien een bericht dat ze de toepassing contoso moeten installeren. Zodra de installatie is geaccepteerd, wordt de toepassing geïnstalleerd.  

Vanaf Configuration Manager versie 1906 is de melding dat de **nieuwe software beschikbaar is** , slechts één keer voor een gebruiker voor een bepaalde toepassing en revisie weer gegeven. De gebruiker krijgt de melding niet meer te zien wanneer deze zich aanmeldt. Er wordt alleen een andere melding voor een toepassing weer geven als de toepassing is gewijzigd of opnieuw is geïmplementeerd.

## <a name="next-steps"></a>Volgende stappen

[Toepassingen bewaken](../deploy-use/monitor-applications-from-the-console.md)

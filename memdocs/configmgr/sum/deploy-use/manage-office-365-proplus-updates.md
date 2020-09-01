---
title: Microsoft 365-app-updates beheren
titleSuffix: Configuration Manager
description: Configuration Manager synchroniseert Microsoft 365 apps-client updates van de WSUS-catalogus naar de site server om updates beschikbaar te maken voor de implementatie op clients.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: d850e582b43e08743e5a61b17e6958ddc6084af1
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194137"
---
# <a name="manage-microsoft-365-apps-with-configuration-manager"></a>Microsoft 365-apps beheren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Note]
> Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Zie [name wijzigen voor Office 365 ProPlus](/deployoffice/name-change)voor meer informatie. Mogelijk ziet u nog steeds verwijzingen naar de oude naam in de Configuration Manager-console en de ondersteunende documentatie terwijl de-console wordt bijgewerkt.

Met Configuration Manager kunt u Microsoft 365 apps op de volgende manieren beheren:

- [Microsoft 365-Apps implementeren](#bkmk_deploy): u kunt het installatie programma van Microsoft 365 apps starten vanuit het [Office 365-client beheer dashboard](office-365-dashboard.md) om de initiële installatie van Microsoft 365 apps gemakkelijker te maken. Met de wizard kunt u de installatie-instellingen voor Microsoft 365 apps configureren, bestanden downloaden van Office Content Delivery Networks (Cdn's) en een script toepassing maken en implementeren met de inhoud.

- [Updates voor Microsoft 365-Apps implementeren](#bkmk_update): u kunt Microsoft 365 apps-client updates beheren via de werk stroom voor software-update beheer. Wanneer micro soft een nieuwe update van Microsoft 365-apps publiceert naar de Office Content Delivery Network (CDN), publiceert micro soft ook een update pakket naar Windows Server Update Services (WSUS). Nadat Configuration Manager de Microsoft 365 apps-updates van de WSUS-catalogus naar de site server hebt gesynchroniseerd, is de update beschikbaar om te implementeren op clients.

   > [!NOTE]
   > Vanaf Configuration Manager versie 2002 kunt u Microsoft 365 apps-updates importeren in niet-verbonden omgevingen. Zie [Microsoft 365 apps-updates synchroniseren vanaf een niet-verbonden software-update punt](../get-started/synchronize-office-updates-disconnected.md)voor meer informatie.   

- [Talen toevoegen voor Microsoft 365 down loads update-apps](#bkmk_o365_lang): u kunt ondersteuning voor Configuration Manager toevoegen om updates te downloaden voor alle talen die worden ondersteund door Microsoft 365-apps. Wat betekent dat Configuration Manager de taal niet hoeft te ondersteunen zolang Microsoft 365 apps wel. Vóór Configuration Manager versie 1610, moet u updates downloaden en implementeren in dezelfde talen die zijn geconfigureerd op Microsoft 365 apps-clients.

- [Het update kanaal wijzigen](#bkmk_channel): u kunt groeps beleid gebruiken om een wijziging in de register sleutel te distribueren naar Microsoft 365 apps-clients om het update kanaal te wijzigen.

Gebruik het [Office 365-dash board voor client beheer](office-365-dashboard.md)om de client gegevens van Microsoft 365 apps te controleren en enkele van deze bewerkingen voor het beheren van de Microsoft 365-apps te starten.

## <a name="deploy-microsoft-365-apps"></a><a name="bkmk_deploy"></a> Microsoft 365-Apps implementeren
Start het installatie programma voor de Microsoft 365-apps vanuit het Office 365-client beheer dashboard voor de eerste installatie van de Microsoft 365-apps. Met de wizard kunt u de installatie-instellingen voor Microsoft 365 apps configureren, bestanden downloaden van de Office Content Delivery Networks (Cdn's) en een script toepassing maken en implementeren voor de bestanden. Microsoft 365 app-updates zijn niet van toepassing totdat Microsoft 365-apps zijn geïnstalleerd op clients en de [Microsoft 365 apps automatische updates](/deployoffice/overview-update-process-microsoft-365-apps) worden uitgevoerd. Voor test doeleinden kunt u de update taak hand matig uitvoeren.

Voor eerdere versies van Configuration Manager moet u de volgende stappen uitvoeren om Microsoft 365-apps voor de eerste keer te installeren op clients:
- Office Deployment Tool (ODT) downloaden
- Down load de bron bestanden voor de installatie van de Microsoft 365-apps, inclusief alle taal pakketten die u nodig hebt.
- Genereer de Configuration.xml waarmee de juiste versie en het kanaal van de Microsoft 365-apps worden opgegeven.
- Maak en implementeer een verouderd pakket of een script toepassing voor clients om Microsoft 365-apps te installeren.

### <a name="requirements"></a>Vereisten
- De computer waarop het installatie programma wordt uitgevoerd, moet toegang hebben tot internet.  
- De gebruiker die het installatie programma uitvoert, moet **Lees** -en **Schrijf** toegang hebben tot de inhouds locatie share die in de wizard is opgenomen.
- Als u een 404-Download fout ontvangt, kopieert u de volgende bestanden naar de map gebruiker% Temp%:
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1806-or-higher"></a>Microsoft 365-Apps implementeren met Configuration Manager versie 1806 of hoger: 
Vanaf Configuration Manager 1806 is het hulp programma voor het aanpassen van Office geïntegreerd met het installatie programma in de Configuration Manager-console. Bij het maken van een implementatie voor Microsoft 365-apps, kunt u de meest recente beheer baarheid-instellingen dynamisch configureren. <!--1358149-->

1. Navigeer in de Configuration Manager-console naar **software bibliotheek**  >  **Overview**  >  **Office 365 client management**.
2. Klik in het rechterdeel venster op **Office 365 Installer** . De installatie wizard wordt geopend.
3. Geef op de pagina **Toepassings instellingen** een naam en beschrijving voor de app op, voer de download locatie voor de bestanden in en klik op **volgende**. De locatie moet worden opgegeven als &#92;&#92;*server*&#92;*share*.
4. Klik op de pagina **Office-instellingen** op **Ga naar het hulp programma voor het aanpassen van Office**. Hiermee opent u het [hulp programma voor het aanpassen van de Office-aanpassing voor klik-en-klaar](https://config.office.com).
5. Configureer de gewenste instellingen voor de installatie van uw Microsoft 365-apps. Klik op het **verzenden** in de rechter bovenhoek van de pagina wanneer u de configuratie voltooit. 
6. Bepaal op de pagina **implementatie** of u nu of op een later tijdstip wilt implementeren. Als u ervoor kiest om later te implementeren, kunt u de toepassing vinden in **software bibliotheek**toepassingen voor  >  **toepassings beheer**  >  **Applications**.  
7. Bevestig de instellingen op de pagina **samen vatting** . 
8. Klik op **volgende** en klik vervolgens op **sluiten** nadat de wizard is voltooid. 

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1802-and-prior"></a>Microsoft 365-Apps implementeren met behulp van Configuration Manager versie 1802 en eerder:

1. Navigeer in de Configuration Manager-console naar **software bibliotheek**  >  **Overview**  >  **Office 365 client management**.
2. Klik in het rechterdeel venster op **Office 365 Installer** . De installatie wizard wordt geopend.
3. Geef op de pagina **Toepassings instellingen** een naam en beschrijving voor de app op, voer de download locatie voor de bestanden in en klik op **volgende**. De locatie moet worden opgegeven als &#92;&#92;*server*&#92;*share*.
4. Kies op de pagina **client instellingen importeren** of u de client instellingen van de Microsoft 365-Apps wilt importeren uit een bestaand XML-configuratie bestand of dat u de instellingen hand matig wilt opgeven. Klik op **volgende** wanneer u klaar bent.  

    Wanneer u een bestaand configuratie bestand hebt, voert u de locatie voor het bestand in en gaat u verder met stap 7. U moet de locatie opgeven in de vorm &#92;&#92;*server*&#92;*share*&#92;*Bestands naam*. Indeling.
    > [!IMPORTANT]    
    > Het XML-configuratie bestand mag alleen [talen bevatten die worden ondersteund door Office 2016](/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. Selecteer op de pagina **client producten** de Microsoft 365 Apps-suite die u gebruikt. Selecteer de toepassingen die u wilt toevoegen. Selecteer eventuele extra producten die moeten worden opgenomen en klik vervolgens op **volgende**.
6. Kies op de pagina **client instellingen** de instellingen die u wilt toevoegen en klik vervolgens op **volgende**.
7. Kies op de pagina **implementatie** of u de toepassing wilt implementeren en klik vervolgens op **volgende**. <br/>Als u ervoor kiest om het pakket niet in de wizard te implementeren, gaat u naar stap 9.
8. Configureer de rest van de wizard pagina's zoals u zou doen voor een typische toepassings implementatie. Zie [een toepassing maken en implementeren](../../apps/get-started/create-and-deploy-an-application.md)voor meer informatie.
9. Voltooi de wizard.
10. U kunt de toepassing implementeren of bewerken vanuit **software bibliotheek**  >  **overzicht**toepassingen voor  >  **toepassings beheer**  >  **Applications**.

Nadat u Microsoft 365 apps hebt gemaakt en geïmplementeerd met behulp van het installatie programma, worden de Microsoft 365 apps-updates standaard niet door Configuration Manager beheerd. Zie [Microsoft 365-Apps implementeren met Configuration Manager](#bkmk_update)om Microsoft 365 apps-clients in staat te stellen updates te ontvangen van Configuration Manager.

Nadat u Microsoft 365 apps hebt geïmplementeerd, kunt u regels voor automatische implementatie maken om de apps te onderhouden. Als u een regel voor automatische implementatie wilt maken voor Microsoft 365 apps, klikt u op **een ADR maken** in het [Office 365-client beheer dashboard](office-365-dashboard.md). Selecteer **Office 365-client** wanneer u het product kiest. Zie [software-updates automatisch implementeren](automatically-deploy-software-updates.md)voor meer informatie.


## <a name="drill-through-required-microsoft-365-apps-updates"></a>Bekijk de vereiste updates voor Microsoft 365 apps
<!--4224414-->
*(Geïntroduceerd in versie 1906)*

U kunt inzoomen op nalevings statistieken om te zien welke apparaten een specifieke Microsoft 365 apps software-update nodig hebben. Als u de lijst met apparaten wilt weer geven, hebt u machtigingen nodig voor het weer geven van updates en de verzamelingen waartoe de apparaten behoren. Inzoomen op de apparaten lijst:

1. Ga naar **Software Library**  >  **Office 365 client management**  >  **Office 365 updates**.
1. Selecteer een update die vereist is voor ten minste één apparaat.
1. Ga naar het tabblad **samen vatting** en zoek het cirkel diagram onder  **Statistieken**.
1. Selecteer de **weer gave vereiste** Hyper link naast het cirkel diagram om in te zoomen op de apparaten lijst.
1. Met deze actie gaat u naar een tijdelijk knoop punt onder **apparaten** waar u de apparaten kunt zien waarvoor de update is vereist. U kunt ook acties uitvoeren voor het knoop punt, zoals het maken van een nieuwe verzameling in de lijst.


## <a name="deploy-microsoft-365-apps-updates"></a><a name="bkmk_update"></a> Updates van Microsoft 365-Apps implementeren

Gebruik de volgende stappen om updates van Microsoft 365-apps te implementeren met Configuration Manager:

1. [Controleer de vereisten voor het](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) gebruik van Configuration Manager voor het beheren van Microsoft 365 apps client updates in de **vereisten voor het gebruik van Configuration Manager voor het beheren van de sectie Microsoft 365 apps client updates** van het artikel.  

2. [Software-update punten configureren](../get-started/configure-classifications-and-products.md) om de Microsoft 365 apps-client updates te synchroniseren. Stel **updates** in voor de classificatie en selecteer **Office 365 client** voor het product. Software-updates synchroniseren nadat u de software-update punten hebt geconfigureerd om de **Update** classificatie te gebruiken.
3. Microsoft 365 apps-clients in staat stellen updates van Configuration Manager te ontvangen. Gebruik Configuration Manager client instellingen of groeps beleid om de client in te scha kelen.

    **Methode 1**: vanaf Configuration Manager versie 1606 kunt u de Configuration Manager-client instelling gebruiken om de client agent van Microsoft 365-apps te beheren. Nadat u deze instelling hebt geconfigureerd en Microsoft 365 apps hebt geïmplementeerd, communiceert de Configuration Manager-client agent met de client agent van Microsoft 365 apps om de updates vanaf een distributie punt te downloaden en te installeren. Configuration Manager maakt inventaris van client instellingen voor Microsoft 365 apps.    

      1. Klik in de Configuration Manager-console op **beheer**  >  **overzicht**  >  **client instellingen**.  

      2. Open de juiste Apparaatinstellingen om de client agent in te scha kelen. Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor meer informatie over standaard-en aangepaste client instellingen.  

      3. Klik op **software-updates** en selecteer **Ja** voor de instelling **beheer van de Office 365-client agent inschakelen** .  

    **Methode 2**:  [Schakel Microsoft 365 apps in om updates van Configuration Manager te ontvangen](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) met behulp van de Office Deployment Tool of Groepsbeleid.  

4. [Implementeer de updates van de Microsoft 365-apps](deploy-software-updates.md) op-clients.

> [!NOTE]  
>
> Als Microsoft 365-apps onlangs zijn geïnstalleerd en afhankelijk van hoe de app is geïnstalleerd, is het mogelijk dat het update kanaal nog niet is ingesteld. In dat geval worden geïmplementeerde updates gedetecteerd als niet van toepassing. Er is een [geplande automatische updates taak](/deployoffice/overview-of-the-update-process-for-office-365-proplus) gemaakt wanneer Microsoft 365-apps worden geïnstalleerd. In deze situatie moet deze taak ten minste één keer worden uitgevoerd om het update kanaal in te stellen en gedetecteerde updates.
>
> Als Microsoft 365 apps recent is geïnstalleerd en geïmplementeerde updates niet zijn gedetecteerd, kunt u voor test doeleinden de taak Office Automatische updates hand matig starten en vervolgens de [evaluatie cyclus](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process) voor de implementatie van software-updates op de client starten. Zie [Microsoft 365-apps bijwerken in een taken reeks](manage-office-365-proplus-updates.md#bkmk_ts)voor instructies over het uitvoeren van dit in een taken reeks.

## <a name="restart-behavior-and-client-notifications-for-microsoft-365-apps-updates"></a>Gedrag voor opnieuw opstarten en client meldingen voor updates van Microsoft 365-apps
Wanneer u een update implementeert op een Microsoft 365 apps-client, zijn het gedrag voor opnieuw opstarten en client meldingen verschillend, afhankelijk van de versie van Configuration Manager. De volgende tabel bevat informatie over de eindgebruikers ervaring wanneer de client een update van de Microsoft 365-apps ontvangt:

|Configuration Manager versie |Ervaring voor de eindgebruiker|  
|----------------|---------------------|
|1706, 1710|De client ontvangt pop-upmeldingen en in-app-meldingen, evenals een dialoog venster voor aftellen voordat de update wordt geïnstalleerd.|
|1802| De client ontvangt pop-upmeldingen en in-app-meldingen, evenals een dialoog venster voor aftellen voordat de update wordt geïnstalleerd. </br>Als er Microsoft 365-apps worden uitgevoerd tijdens het afdwingen van de client update, worden de Microsoft 365-apps niet geforceerd afgesloten. In plaats daarvan wordt de installatie van de update geretourneerd wanneer het opnieuw opstarten van het systeem is vereist <!--510006-->|


> [!Important]
>
>In Configuration Manager versie 1706, Let op de volgende details:
>
>- Een meldings pictogram wordt weer gegeven in het systeemvak op de taak balk voor vereiste apps waarvan de deadline binnen 48 uur in de toekomst ligt en de update-inhoud is gedownload. 
>- Een dialoog venster voor tellingen wordt weer gegeven voor vereiste apps waarvan de deadline binnen 7,5 uur in de toekomst ligt en de update is gedownload. De gebruiker kan het dialoog venster voor het aftellen Maxi maal drie keer vóór de deadline uitstellen. Wanneer dit is uitgesteld, wordt het aftellen weer gegeven na twee uur. Als dit niet wordt uitgesteld, wordt een aftelling van 30 minuten en wordt de update geïnstalleerd wanneer de aftelling verloopt.
>- Een pop-upmelding kan pas worden weer gegeven wanneer de gebruiker op het pictogram in het systeemvak klikt. Als het systeemvak een minimale ruimte heeft, kan het meldings pictogram bovendien niet zichtbaar zijn, tenzij de gebruiker het systeemvak opent of uitbreidt. 
>- Het dialoog venster melding en Aftel tijd kan worden gestart terwijl de gebruiker niet actief op het apparaat werkt. Als het apparaat bijvoorbeeld 's nachts wordt vergrendeld, kunnen Microsoft 365 apps die op het apparaat worden uitgevoerd, worden gesloten om de update te installeren. Voordat u de app sluit, worden de app-gegevens opgeslagen om gegevens verlies te voor komen. 
>- Als de deadline zich in het verleden bevindt of zo snel mogelijk is geconfigureerd, wordt het uitvoeren van Microsoft 365 apps mogelijk geforceerd afgesloten zonder meldingen. 
>- Als de gebruiker een update van de Microsoft 365-apps vóór de deadline installeert, Configuration Manager verifieert of de update wordt geïnstalleerd wanneer de deadline wordt bereikt. Als de update niet op het apparaat wordt gedetecteerd, wordt de update geïnstalleerd. 
>- De in-app-meldings balk wordt niet weer gegeven in een app die wordt uitgevoerd voordat de update wordt gedownload. Nadat de update is gedownload, wordt de in-app-melding alleen weer gegeven voor onlangs geopende apps.
>- Voor updates van Microsoft 365-apps die zijn geactiveerd door een service venster of die zijn gepland voor niet-werk uren, is het mogelijk dat het uitvoeren van Office-apps wordt afgesloten om de update te installeren zonder meldingen. 
>- Zie voor meer informatie [meldingen voor eind gebruikers updates voor Microsoft 365-apps](/deployoffice/end-user-update-notifications-microsoft-365-apps)


## <a name="add-languages-for-microsoft-365-apps-update-downloads"></a><a name="bkmk_o365_lang"></a> Talen toevoegen voor het downloaden van updates voor Microsoft 365-apps
U kunt ondersteuning voor Configuration Manager toevoegen om updates te downloaden voor alle talen die door Microsoft 365 apps worden ondersteund.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Updates downloaden voor extra talen in versie 1902
<!--3555955-->

Vanaf Configuration Manager versie 1902 van de werk stroom update wordt de 38 talen gescheiden voor **Windows Update** van de talloze extra talen voor **Office 365 client update**.

Als u de benodigde talen wilt selecteren, gebruikt u de pagina **taal selecteren** op de volgende locaties:
- Wizard regel voor automatische implementatie maken
- Wizard software-updates implementeren
- Wizard software-updates downloaden
- Eigenschappen van regel voor automatische implementatie

Selecteer op de pagina **taal** selecteren de optie **Office 365-client update**en klik vervolgens op **bewerken**. Voeg de benodigde talen voor Microsoft 365 apps toe en klik vervolgens op **OK**.

![Scherm afbeelding van het toevoegen van extra talen voor Microsoft 365-apps](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>Ondersteuning toevoegen om updates te downloaden voor extra talen in versie 1810 en lager

Gebruik de volgende procedure op het software-update punt op de centrale beheer site of zelfstandige primaire site.

> [!IMPORTANT]  
> Het configureren van aanvullende Microsoft 365-apps update talen is een instelling die voor de hele site geldt. Nadat u de talen hebt toegevoegd met behulp van de volgende procedure, worden alle updates van de apps van Microsoft 365 gedownload in die talen, evenals de talen die u selecteert op de pagina **taal selecteren** in de wizard software-updates downloaden of software-updates implementeren.

1. Typ in een opdracht prompt *WBEMTest* als gebruiker met beheerders rechten om de Windows Management Instrumentation Tester te openen.
2. Klik op **verbinding maken**en typ vervolgens *root\sms\ site_ &lt; site &gt; *code.
3. Klik op **query**en voer de volgende query uit: *selecteer &#42; van SMS_SCI_Component waarbij componentnaam = "SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![WMI-query](../media/1-wmiquery.png)
4. Dubbel klik in het resultaten venster op het object met de site code voor de centrale beheer site of zelfstandige primaire site.
5. Selecteer de eigenschap **Props** , klik op **eigenschap bewerken**en klik vervolgens op **Inge sloten weer geven**.
   ![Eigenschappen editor](../media/2-propeditor.png)
6. Begin bij het eerste query resultaat en open elk object totdat u het hebt gevonden met **AdditionalUpdateLanguagesForO365** voor de eigenschap **PropertyName** .
7. Selecteer **waarde2** en klik op **eigenschap bewerken**.  
   ![De eigenschap Value2 bewerken](../media/3-queryresult.png)
8. Voeg extra talen toe aan de eigenschap **Value2** en klik op **eigenschap opslaan**. <br/> Bijvoorbeeld: pt-pt (voor Portugees-Portugal), af-ZA (voor Afrikaans-Zuid-Afrika), nn-no (voor Noors (Nynorsk)-Noor wegen), enzovoort. U typt `pt-pt,af-za,nn-no` voor de voorbeeld talen. Gebruik geen spaties tussen de talen.
 
   ![Talen toevoegen in eigenschaps editor](../media/4-props.png)  
9. Klik op **sluiten**, klik op **sluiten**, klik op **eigenschap opslaan**en klik op **object opslaan** (als u op **sluiten** klikt, worden de waarden genegeerd). Klik op **sluiten**en klik vervolgens op **afsluiten** om de Windows Management Instrumentation Tester af te sluiten.
10. Ga in de Configuration Manager-console naar overzicht van **software bibliotheken**  >  **Overview**  >  **Office 365 client management**  >  **Office 365 updates**.
11. Wanneer u nu updates van Microsoft 365 apps downloadt, worden de updates gedownload in de talen die u in de wizard hebt geselecteerd en geconfigureerd in deze procedure. Als u wilt controleren of de updates in de juiste talen worden gedownload, gaat u naar de pakket bron voor de update en zoekt u naar bestanden met de taal code in de bestands naam.  
    ![Bestands namen met extra talen](../media/5-verification.png)

## <a name="updating-microsoft-365-apps-in-a-task-sequence"></a><a name="bkmk_ts"></a> Microsoft 365 apps in een taken reeks bijwerken
Wanneer u de taken reeks stap [software-updates installeren](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) gebruikt om updates van Microsoft 365 apps te installeren, worden geïmplementeerde updates gedetecteerd als niet van toepassing.  Dit kan gebeuren als de geplande Office Automatische updates-taak niet ten minste eenmaal is uitgevoerd (Zie de opmerking in [Deploy Microsoft 365 apps updates](manage-office-365-proplus-updates.md#bkmk_update)). Dit kan bijvoorbeeld gebeuren als Microsoft 365-Apps onmiddellijk zijn geïnstalleerd voordat u deze stap uitvoert.

Gebruik een van de volgende methoden om ervoor te zorgen dat het update kanaal zodanig is ingesteld dat geïmplementeerde updates correct worden gedetecteerd:

**Methode 1:**
1. Open op een computer met dezelfde versie van Microsoft 365-apps taak planner (Taskschd. msc) en Identificeer de taak automatische updates van Microsoft 365 apps. Normaal gesp roken bevindt deze zich onder de **taak planner-bibliotheek**  > **micro soft** > **Office**.
2. Klik met de rechter muisknop op de taak automatische updates en selecteer **Eigenschappen**.
3. Ga naar het tabblad **acties** en klik op **bewerken**. Kopieer de opdracht en eventuele argumenten. 
4. Bewerk de taken reeks in de Configuration Manager-console.
5. Voeg een nieuwe stap **opdracht regel uitvoeren** toe vóór de stap **software-updates installeren** in de taken reeks. Als Microsoft 365-apps is geïnstalleerd als onderdeel van dezelfde taken reeks, moet u ervoor zorgen dat deze stap wordt uitgevoerd nadat Office is geïnstalleerd.
6. Kopieer de opdracht en de argumenten die u hebt verzameld van de geplande Office-taak voor automatische updates. 
7. Klik op **OK**. 

**Methode 2:**
1. Open op een computer met dezelfde versie van Microsoft 365-apps taak planner (Taskschd. msc) en Identificeer de taak automatische updates van Microsoft 365 apps. Normaal gesp roken bevindt deze zich onder de **taak planner-bibliotheek**  > **micro soft** > **Office**.
2. Bewerk de taken reeks in de Configuration Manager-console.
3. Voeg een nieuwe stap **opdracht regel uitvoeren** toe vóór de stap **software-updates installeren** in de taken reeks. Als Microsoft 365-apps is geïnstalleerd als onderdeel van dezelfde taken reeks, moet u ervoor zorgen dat deze stap wordt uitgevoerd nadat Office is geïnstalleerd.
4. Voer in het veld opdracht regel de opdracht regel in waarmee de geplande taak wordt uitgevoerd. Zie voor beeld hieronder om te controleren of de teken reeks tussen aanhalings tekens overeenkomt met het pad en de naam van de taak die u in stap 1 hebt opgegeven.  

    Voorbeeld: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. Klik op **OK**. 

## <a name="update-channels-for-microsoft-365-apps"></a><a name="bkmk_channel"></a> Kanalen voor Microsoft 365-apps bijwerken
<!--6298093-->
Wanneer Office 365 ProPlus is gewijzigd in **Microsoft 365 apps voor bedrijven**, zijn de update kanalen ook hernoemd. Als u een regel voor automatische implementatie (ADR) gebruikt om updates te implementeren, moet u wijzigingen aanbrengen in uw Adr's als ze afhankelijk zijn van de eigenschap **title** . Dat komt doordat de naam van de update pakketten in de Microsoft Update catalogus wordt gewijzigd.

Op dit moment begint de titel van een update pakket voor Office 365 ProPlus met ' Office 365 client update ', zoals in het volgende voor beeld wordt weer gegeven:

&nbsp;&nbsp;Office 365-client update-Semi-Annual-kanaal versie 1908 voor x64-editie (Build 11929,20648)

Voor update pakketten die zijn uitgebracht op en na 9 juni, begint de titel met ' Microsoft 365 apps bijwerken ', zoals in het volgende voor beeld wordt weer gegeven:

&nbsp;&nbsp;Updates van Microsoft 365-apps-Semi-Annual-kanaal versie 1908 voor x64-editie (Build 11929,50000)
</br>
</br>

|Nieuwe kanaal naam|Vorige kanaal naam|
|--|--|
|Semi-Annual-kanaal voor ondernemingen|Semi-Annual-kanaal|
|Semi-Annual Enter prise-kanaal (preview-versie)|Semi-Annual-kanaal (Targeted)|
|Maandelijks bedrijfs kanaal|NA|
|Huidig kanaal|Monthly-kanaal|
|Huidig kanaal (preview-versie)|Monthly-kanaal (targeted)|
|Bèta-kanaal|Handel|

Zie [software-updates automatisch implementeren](automatically-deploy-software-updates.md)voor meer informatie over het wijzigen van uw adr's. Zie voor meer informatie over de naamswijziging naam [wijzigen voor Office 365 ProPlus](/deployoffice/name-change).


## <a name="change-the-update-channel-after-you-enable-microsoft-365-apps-clients-to-receive-updates-from-configuration-manager"></a>Wijzig het update kanaal nadat u hebt ingeschakeld Microsoft 365 apps-clients updates van Configuration Manager ontvangen

Na de implementatie van Microsoft 365-apps, kunt u het update kanaal wijzigen met groepsbeleid of de Office Deployment Tool (ODT). U kunt bijvoorbeeld een apparaat verplaatsen van een semi-Annual-kanaal naar een semi-Annual-kanaal (targeted). Wanneer u het kanaal wijzigt, wordt Office automatisch bijgewerkt zonder dat de volledige versie opnieuw moet worden geïnstalleerd of gedownload. Zie voor meer informatie [het Microsoft 365-apps-update kanaal wijzigen voor apparaten in uw organisatie](/deployoffice/change-update-channels).

## <a name="next-steps"></a>Volgende stappen

Gebruik het Office 365-dash board voor client beheer in Configuration Manager om Microsoft 365 apps-client gegevens te controleren en Microsoft 365-apps te implementeren. Zie voor meer informatie [Office 365-dash board voor client beheer](office-365-dashboard.md).
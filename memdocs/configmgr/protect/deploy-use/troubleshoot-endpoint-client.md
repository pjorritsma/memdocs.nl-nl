---
title: Problemen met Endpoint Protection oplossen
titleSuffix: Configuration Manager
description: Meer informatie over het oplossen van problemen met Windows Defender en Endpoint Protection.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724487"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>Problemen oplossen voor de Windows Defender- of Endpoint Protection-client

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u problemen ondervindt met Windows Defender of Endpoint Protection, gebruikt u dit artikel om de volgende problemen op te lossen:  

- [Windows Defender of Endpoint Protection bijwerken](#update-windows-defender-or-endpoint-protection)  
- [Windows Defender-of Endpoint Protection-Service starten](#starting-windows-defender-or-endpoint-protection-service)  
- [Problemen met de Internet verbinding](#internet-connection-issues)  
- [Een gedetecteerde bedreiging kan niet worden hersteld](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a>Windows Defender of Endpoint Protection bijwerken

### <a name="symptoms"></a>Symptomen

Windows Defender of Endpoint Protection werkt automatisch met Microsoft Update om ervoor te zorgen dat uw virus-en Spyware definities up-to-date blijven.  

In deze sectie worden veelvoorkomende problemen met automatische updates opgelost, met inbegrip van de volgende situaties:  

- U ziet foutberichten die aangeven dat er updates zijn mislukt.  

- Wanneer u controleert op updates, wordt een fout bericht weer gegeven dat de updates van de virus-en Spyware definities niet kunnen worden gecontroleerd, gedownload of geïnstalleerd.  

- Hoewel uw apparaat is verbonden met internet, mislukken de updates.  

- Updates worden niet automatisch volgens de planning geïnstalleerd.  

### <a name="causes"></a>Oorzaken

De meest voorkomende oorzaken voor problemen met updates zijn problemen met de Internet verbinding. Als u weet dat uw apparaat is verbonden met internet omdat u naar andere websites kunt bladeren, kan het probleem worden veroorzaakt door conflicten met uw Internet instellingen in Windows.  

### <a name="options-to-resolve"></a>Opties om op te lossen

#### <a name="step-1-reset-your-internet-settings"></a>Stap 1: uw Internet instellingen opnieuw instellen  

1. Sluit alle geopende Program ma's, inclusief de webbrowser.  

    > [!NOTE]  
    > Wanneer u deze Internet instellingen opnieuw instelt, worden de tijdelijke bestanden, cookies, browse geschiedenis en online wacht woorden van uw browser verwijderd. Uw favorieten worden niet verwijderd.  

2. Ga naar het menu **Start** en open `inetcpl.cpl`.  

3. Ga naar het tabblad **Geavanceerd** .  

4. Selecteer **opnieuw**instellen in de sectie **instellingen voor Internet Explorer opnieuw**instellen en selecteer vervolgens opnieuw **instellen** om te bevestigen.  

5. Selecteer **OK** wanneer de instellingen opnieuw worden ingesteld.

6. Probeer Windows Defender opnieuw bij te werken.

Als het probleem zich blijft voordoen, gaat u verder met de volgende stap.  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Stap 2: Controleer of de datum en tijd correct zijn ingesteld op uw computer  

Als het fout bericht de code 0x80072f8f bevat, wordt het probleem waarschijnlijk veroorzaakt door een onjuiste datum-of tijd instelling op de computer. Ga naar het menu **Start** , selecteer **instellingen**, selecteer **tijd & taal**en selecteer **datum & tijd**.

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>Stap 3: de naam van de map software distributie op uw computer wijzigen  

1. Stop de **Windows Update** -service.  

    1. Ga naar **Start**en open **Services. msc**.  

    2. Selecteer de **Windows Update** -service. Ga naar het **actie** menu en selecteer **stoppen**.

2. Wijzig de naam van de map **SoftwareDistribution** .  

    1. Open een opdrachtprompt als beheerder.  

    2. Voer de volgende opdrachten in:

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. Start de **Windows Update** -service opnieuw.

    1. Ga terug naar het venster **Services** .  

    2. Selecteer de **Windows Update** -service. Ga naar het **actie** menu en selecteer **starten**.

    3. Sluit het venster Services.  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Stap 4: de micro soft anti virus-update-engine op uw computer opnieuw instellen  

1. Open een opdrachtprompt als beheerder.

2. Voer de volgende opdrachten in:

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. Start de computer opnieuw op.  

4. Probeer Windows Defender opnieuw bij te werken.

Als het probleem zich blijft voordoen, gaat u verder met de volgende stap.  

#### <a name="step-5-manually-install-the-definition-updates"></a>Stap 5: de definitie-updates hand matig installeren  

[Down load de nieuwste updates hand matig](https://www.microsoft.com/en-us/wdsi/defenderupdates).  

#### <a name="step-6-contact-microsoft-support"></a>Stap 6: contact opnemen met micro soft ondersteuning  

Neem contact op met micro soft ondersteuning als het probleem niet is opgelost met deze stappen. Zie [ondersteunings opties en community-resources](../../core/understand/find-help.md#BKMK_SupportOptions)voor meer informatie.  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a> De Windows Defender- of Endpoint Protection-service starten

### <a name="symptom"></a>Symptoom

U ontvangt een bericht met de melding dat **Windows Defender of Endpoint Protection uw computer niet bewaakt omdat de service van het programma is gestopt. U moet de computer nu opnieuw opstarten.**

### <a name="solution"></a>Oplossing

#### <a name="step-1-restart-your-computer"></a>Stap 1: de computer opnieuw opstarten

Sluit alle toepassingen en start de computer opnieuw op.  

#### <a name="step-2-check-the-windows-service"></a>Stap 2: de Windows-service controleren

1. Ga naar **Start**en open **Services. msc**.  

2. Selecteer de **Windows Defender anti virus-service**.  

3. Zorg ervoor dat het **opstart type** is ingesteld op **automatisch**.

4. Ga naar het **actie** menu en selecteer **starten**.

    1. Als deze actie niet beschikbaar is, selecteert u **stoppen**. Wacht tot de service is gestopt en selecteer vervolgens de actie **starten** om de service opnieuw te starten.  

Noteer eventuele fouten die tijdens dit proces kunnen worden weer gegeven. [Neem contact op met Microsoft ondersteuning](../../core/understand/find-help.md#BKMK_SupportOptions) en geef de fout informatie op.  

#### <a name="step-3-remove-any-third-party-security-programs"></a>Stap 3: externe beveiligings Programma's van derden verwijderen  

> [!NOTE]  
> Sommige beveiligings toepassingen kunnen niet volledig worden verwijderd. Mogelijk moet u het hulp programma voor het opschonen van uw vorige beveiligings toepassing downloaden en uitvoeren om deze volledig te verwijderen.  

1. Ga naar **Start** en open **appwiz. cpl**.  

2. Verwijder alle beveiligings Programma's van derden in de lijst met geïnstalleerde Program ma's.

3. Start de computer opnieuw op.  

> [!CAUTION]  
> Wanneer u beveiligings Programma's verwijdert, is de computer mogelijk niet beveiligd. Neem contact op met [Microsoft ondersteuning](https://support.microsoft.com/supportforbusiness/productselection)als u problemen ondervindt met de installatie van Windows Defender nadat u de bestaande beveiligings Programma's hebt verwijderd. Selecteer de **beveiligings** productfamilie en vervolgens het **Windows Defender** -product.

## <a name="internet-connection-issues"></a> Problemen met de internetverbinding

Als uw computer de meest recente updates van Windows Update wilt ontvangen, verbindt u deze met internet.  

1. Ga naar **Start** en open **ncpa. cpl**.  

2. Open de naam van de verbinding om de verbindings **status**weer te geven.  

3. Als uw computer is verbonden, is de status van **IPv4-verbinding** en/of **IPv6-connectiviteit** **Internet**.  

4. Als uw computer niet is verbonden, selecteert u de naam van de verbinding en selecteert u **diagnose van deze verbinding**.

Sluit alle geopende programma's en start de computer opnieuw op.  

## <a name="detected-threat-cant-be-remediated"></a>Een gedetecteerde bedreiging kan niet worden hersteld

Wanneer Windows Defender of Endpoint Protection een mogelijke bedreiging detecteert, probeert de dreiging te verhelpen door de dreiging te in quarantaine of te verwijderen. Deze bedreigingen kunnen worden verborgen in een gecomprimeerd archief`.zip`() of in een netwerk share.

### <a name="remove-or-scan-the-file"></a>Het bestand verwijderen of scannen  

- Als de gedetecteerde bedreiging zich in een gecomprimeerd archief bestand bevond, bladert u naar het bestand. Verwijder het bestand of scan het hand matig. Klik met de rechter muisknop op het bestand en selecteer **scannen met Windows Defender**. Als Windows Defender extra bedreigingen in het bestand detecteert, wordt u hiervan op de hoogte gebracht. Vervolgens kunt u een passende actie kiezen.  

- Als de gedetecteerde bedreiging zich in een netwerk share bevindt, opent u de share en scant u deze hand matig. Klik met de rechter muisknop op het bestand en selecteer **scannen met Windows Defender**. Als Windows Defender extra bedreigingen in de netwerk share detecteert, wordt u hiervan op de hoogte gebracht. Vervolgens kunt u een passende actie kiezen.  

- Als u niet zeker bent van de oorsprong van het bestand, voert u een volledige scan op uw computer uit. Het kan enige tijd duren voordat een volledige scan is voltooid.  

## <a name="see-also"></a>Zie ook

[Veelgestelde vragen over Endpoint Protection-client](endpoint-protection-client-faq.md)

[Help voor Endpoint Protection-client](endpoint-protection-client-help.md)

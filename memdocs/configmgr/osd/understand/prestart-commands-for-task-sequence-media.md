---
title: Prestart-opdrachten voor takenreeksmedia
titleSuffix: Configuration Manager
description: Maak een script om te gebruiken voor de prestart-opdracht, Distribueer de inhoud die is gekoppeld aan de prestart-opdracht en configureer de prestart-opdracht in media.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 06c96d668d3c37b107ae8e290ebcd124e8a2b773
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124377"
---
# <a name="prestart-commands-for-task-sequence-media-in-configuration-manager"></a>Prestart-opdrachten voor taken reeks media in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt een prestart-opdracht maken in Configuration Manager voor gebruik met opstart media, zelfstandige media en voorgefaseerde media. De prestart-opdracht is een script of een uitvoerbaar bestand dat wordt uitgevoerd voordat de takenreeks wordt geselecteerd en dat kan communiceren met de gebruiker in Windows PE. Met de prestart-opdracht kan een gebruiker om informatie worden gevraagd die vervolgens wordt opgeslagen in de takenreeksomgeving. Daarnaast kan een query op een takenreeksvariabele worden uitgevoerd om informatie te verzamelen. Wanneer de doelcomputer wordt opgestart, wordt de opdrachtregel uitgevoerd voordat het beleid wordt gedownload van het beheerpunt. Gebruik de volgende procedures om een script te maken voor de prestart-opdracht, de inhoud gekoppeld aan de prestart-opdracht te distribueren en de prestart-opdracht voor media te configureren.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Een scriptbestand maken voor de prestart-opdracht  
 Takenreeksvariabelen kunnen door het COM-object Microsoft.SMS.TSEnvironment worden gelezen en geschreven terwijl de takenreeks wordt uitgevoerd. In het volgende voorbeeld wordt door een Visual Basic-scriptbestand een query op de takenreeksvariabele _SMSTSLogPath uitgevoerd om de huidige logboeklocatie te achterhalen. Met het script wordt ook een aangepaste variabele ingesteld.  

``` VBScript
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Een pakket voor het scriptbestand maken en de inhoud distribueren  
 Wanneer u het script of uitvoerbare bestand voor de prestart-opdracht hebt gemaakt, moet u een pakketbron maken om de bestanden voor het script of uitvoerbare bestand te hosten, een pakket voor de bestanden maken (geen programma vereist) en de inhoud vervolgens distribueren naar een distributiepunt.  

 Zie [pakketten en Program ma's](../../apps/deploy-use/packages-and-programs.md)voor meer informatie over het maken van een pakket.  

 Zie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)voor meer informatie over het distribueren van inhoud.  

## <a name="configure-the-prestart-command-in-media"></a>De prestart-opdracht configureren voor media  
 U kunt een prestart-opdracht in de wizard Takenreeksmedia maken configureren voor zelfstandige media, opstartbare media en voorgefaseerde media. Zie [taken reeks media maken](../deploy-use/create-task-sequence-media.md)voor meer informatie over de media typen. Gebruik de volgende procedure om een prestart-opdracht voor media te maken.  

#### <a name="to-create-a-prestart-command-in-media"></a>Een prestart-opdracht voor media maken  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Vouw in de werkruimte **Softwarebibliotheek** de optie **Besturingssystemen**uit en klik vervolgens op **Takenreeksen**.  

3.  Klik op het tabblad **Start** in de groep **Maken** op **Takenreeksmedia maken** om de wizard Takenreeksmedia maken te starten.  

4.  Selecteer op de pagina **Mediatype selecteren** de optie **Zelfstandige media**, **Opstartbare media**of **Voorgefaseerde media**en klik vervolgens op **Volgende**.  

5.  Navigeer naar de pagina **Aanpassing** van de wizard. Zie [taken reeks media maken](../deploy-use/create-task-sequence-media.md)voor meer informatie over het configureren van de andere pagina's in de wizard.  

6.  Geef op de pagina **Aanpassing** de volgende informatie op en klik vervolgens op **Volgende**.  

    -   Selecteer **Prestart-opdracht inschakelen**.  

    -   Voer in het tekstvak **Opdrachtregel** het script of uitvoerbare bestand in dat u hebt gemaakt voor de prestart-opdracht.  

        > [!IMPORTANT]  
        >  Gebruik **cmd/c <prestart- \> opdracht** om de prestart-opdracht op te geven. Als u bijvoorbeeld TSScript.vbs hebt gebruikt als de naam voor uw prestart-opdrachtscript, voert u dus **cmd /C TSScript.vbs** in op de opdrachtregel. Hierbij opent u met **cmd /C** een nieuw venster van de Windows-opdrachtinterpreter en wordt de omgevingsvariabele Path gebruikt om het script of uitvoerbare bestand voor de prestart-opdracht te vinden. U kunt ook het volledige pad naar de prestart-opdracht opgeven, maar de stationsletter kan afwijken op computers met andere stationsconfiguraties.  

    -   Selecteer **Inclusief bestanden voor de prestart-opdracht**.  

    -   Klik op **Instellen** om het pakket te selecteren dat is gekoppeld aan de prestart-opdrachtbestanden.  

    -   Klik op **Bladeren** om het distributiepunt te selecteren dat de inhoud voor de prestart-opdracht host.  

7.  Voltooi de wizard.  

---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: Meer informatie over het beheren van antimalwarebeleid en Windows Firewall beveiliging voor clients.
ms.date: 03/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0a7ee54e3bfa4a4231d0d57b48caa49cf9869b76
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/01/2020
ms.locfileid: "85591099"
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Van toepassing op: Configuration Manager (huidige vertakking)*

Endpoint Protection beheert antimalware-beleid en Windows Firewall beveiliging voor client computers in uw Configuration Manager-hiërarchie.  

> [!IMPORTANT]  
>  U moet een licentie hebben om Endpoint Protection te gebruiken voor het beheren van clients in uw Configuration Manager hiërarchie.  

 Wanneer u Endpoint Protection gebruikt met Configuration Manager, hebt u de volgende voor delen:  

-   Antimalwarebeleid, Windows Firewall-instellingen en het beheren van micro soft Defender Advanced Threat Protection op geselecteerde groepen computers configureren  
-   Gebruik Configuration Manager software-updates om de meest recente definitie bestanden voor antimalware te downloaden om client computers up-to-date te houden  
-   E-mail meldingen verzenden, bewaking in-console gebruiken en rapporten weer geven. Deze acties stellen gebruikers met beheerders rechten op de hoogte wanneer er malware wordt gedetecteerd op client computers.  

Vanaf Windows 10-en Windows Server 2016-computers is Windows Defender al geïnstalleerd. Voor deze besturings systemen wordt een Management-client voor Windows Defender geïnstalleerd wanneer de Configuration Manager-client wordt geïnstalleerd. Op Windows 8,1 en eerdere computers wordt de Endpoint Protection-client geïnstalleerd met de Configuration Manager-client. Windows Defender en de Endpoint Protection-client hebben de volgende mogelijkheden:  

-   Detecteren en herstellen van malware en spyware  
-   Rootkitdetectie en herstel  
-   Evalueren van kritieke beveiligingsproblemen en automatische definitie en engine-updates  
-   Detecteren van kwetsbare plekken in het netwerk via het netwerkinspectiesysteem  
-   Integratie met Cloud Protection Service om malware aan micro soft te melden. Wanneer u deelneemt aan deze service, downloadt de Endpoint Protection-client of Windows Defender de meest recente definities van het Malware Protection Center wanneer onbekende malware op een computer wordt gedetecteerd.  

> [!NOTE]  
>  De Endpoint Protection-client kan worden geïnstalleerd op een server waarop Hyper-V en op virtuele gast machines met ondersteunde besturings systemen worden uitgevoerd. Endpoint Protection acties hebben een ingebouwde wille keurige vertraging, zodat de beveiligings Services niet tegelijkertijd worden uitgevoerd om buitensporig CPU-gebruik te voor komen.  

 Daarnaast beheert u Windows Firewall instellingen met Endpoint Protection in de Configuration Manager-console.  

 [Voorbeeld scenario: System Center Endpoint Protection gebruiken om computers te beveiligen tegen schadelijke software](scenarios-endpoint-protection.md) Endpoint Protection en de Windows Firewall.  


## <a name="managing-malware-with-endpoint-protection"></a>Malware beheren met Endpoint Protection  
 Met Endpoint Protection in Configuration Manager kunt u een antimalwarebeleid maken dat instellingen bevat voor Endpoint Protection client configuraties. Implementeer deze antimalwarebeleid op client computers. Controleer vervolgens de naleving in het knoop punt **Endpoint Protection status** onder **beveiliging** in de werk ruimte **bewaking** . Gebruik ook Endpoint Protection rapporten in het knoop punt **rapportage** .  

 Extra informatie:  

-   [Antimalwarebeleid voor Endpoint Protection maken en implementeren](endpoint-antimalware-policies.md) : antimalwarebeleid maken, implementeren en bewaken met een lijst met instellingen die u kunt configureren  

-   [Informatie over het bewaken](monitor-endpoint-protection.md) van activiteiten rapporten voor Endpoint Protection bewaking, geïnfecteerde client computers en meer.  

-   [Antimalwarebeleid en Firewall instellingen voor Endpoint Protection](endpoint-antimalware-firewall.md) herstellen-malware die op client computers is gevonden  

-   [Logboek bestanden voor Endpoint Protection](../../core/plan-design/hierarchy/log-files.md#BKMK_EPLog)  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Windows Firewall beheren met Endpoint Protection  
 Endpoint Protection in Configuration Manager biedt basis beheer van de Windows Firewall op client computers. Voor elk netwerkprofiel kunt u de volgende instellingen configureren:  

-   Windows Firewall in- of uitschakelen.  

-   Blokkeer binnenkomende verbindingen, inclusief verbindingen in de lijst met toegestane programma's.  

-   Waarschuw de gebruiker wanneer een nieuw programma door Windows Firewall wordt geblokkeerd.  

> [!NOTE]  
>  Endpoint Protection biedt alleen ondersteuning voor het beheren van Windows Firewall.  


 Zie [Windows Firewall beleid voor Endpoint Protection maken en implementeren](create-windows-firewall-policies.md)voor meer informatie.  


## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Endpoint Protection beheert en bewaakt micro soft Defender Advanced Threat Protection (ATP), voorheen bekend als Windows Defender ATP. De micro soft Defender ATP-service helpt ondernemingen bij het detecteren, onderzoeken en reageren op geavanceerde aanvallen op het bedrijfs netwerk. Zie [micro soft Defender Advanced Threat Protection](defender-advanced-threat-protection.md)(Engelstalig) voor meer informatie.

## <a name="endpoint-protection-workflow"></a>Endpoint Protection-werkstroom  
 Gebruik het volgende diagram om inzicht te krijgen in de werk stroom voor het implementeren van Endpoint Protection in uw Configuration Manager-hiërarchie.  

 ![Endpoint Protection-werkstroom](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Endpoint Protection-client voor Mac-computers en Linux-servers  

> [!Important]  
> Ondersteuning voor System Center Endpoint Protection (SCEP) voor Mac en Linux (alle versies) eindigt op 31 december 2018. De beschik baarheid van nieuwe virus definities voor SCEP voor Mac en SCEP voor Linux kan na het einde van de ondersteuning worden stopgezet. Zie [End of support blog post](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257)voor meer informatie.  

 System Center Endpoint Protection bevat een Endpoint Protection-client voor Linux en voor Mac-computers. Deze clients worden niet geleverd met Configuration Manager. Down load de volgende producten van de [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx):  

-   System Center-Endpoint Protection voor Mac  

-   System Center-Endpoint Protection voor Linux  


> [!Note]  
>  U moet klant van Microsoft Volume License zijn om de Endpoint Protection-installatiebestanden voor Linux en de Mac te kunnen downloaden.  

 Deze producten kunnen niet worden beheerd vanuit de Configuration Manager-console. Een System Center Operations Manager management pack wordt geleverd met de installatie bestanden, waarmee u de client voor Linux kunt beheren.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>De Endpoint Protection-client voor Mac-computers en Linux-servers ophalen

Gebruik de volgende stappen om het installatie kopie bestand te downloaden met de Endpoint Protection-client software en-documentatie voor Mac-computers en Linux-servers.
1. Meld u aan bij de [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Selecteer het tabblad **down loads en sleutels** boven aan de website.
3. Filteren op product **System Center Endpoint Protection (huidige branch)**.
4. Klik op koppeling om te **downloaden**
5. Klik op **Doorgaan**. Er moeten verschillende bestanden worden weer geven, waaronder een met de naam: **System Center Endpoint Protection (huidige versie 1606) voor Linux OS en Macintosh OS multi taal 32/64 bits 1878 MB ISO**.
6. Klik op het pijl pictogram om het bestand te downloaden. De bestands naam is **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050. ISO**.

De update van januari 2018 (X21-67050) bevat de volgende versies:

- System Center Endpoint Protection voor Mac 4.5.32.0 (ondersteuning voor macOS 10,13 High Sierra)
- System Center-Endpoint Protection voor Linux 4.5.20.0 

  Voor meer informatie over het installeren en beheren van de Endpoint Protection-clients voor Linux-en Mac-computers gebruikt u de documentatie bij deze producten. Deze product documentatie bevindt zich in de map **Documentation** van. ISO-bestand.

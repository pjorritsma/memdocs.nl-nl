---
title: Console installeren
titleSuffix: Configuration Manager
description: Installeer de Configuration Manager-console om verbinding te maken met een centrale beheer site of primaire site.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718236"
---
# <a name="install-the-configuration-manager-console"></a>De Configuration Manager-console installeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Beheerders gebruiken de Configuration Manager-console voor het beheren van de Configuration Manager omgeving. Elke Configuration Manager-console kan verbinding maken met een centrale beheer site (CAS) of een primaire site. U kunt een Configuration Manager-console niet verbinden met een secundaire site.

De Configuration Manager-console wordt altijd geïnstalleerd op de site server voor de CA'S of een primaire site. Als u de-console los van de installatie van de site server wilt installeren, voert u het zelfstandige installatie programma uit.  



## <a name="prerequisites"></a>Vereisten

- U hebt lokale **beheer** rechten op de doel computer voor de-console.  

- U hebt **Lees** machtigingen voor de locatie van de installatie bestanden van de Configuration Manager-console.  



## <a name="source-paths"></a>Bron paden

Bepaal welk bronpad u moet gebruiken:  

- De map ConsoleSetup op de site server:`<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    Wanneer u een-site server installeert, worden de installatie bestanden van de-console en ondersteunde taal pakketten voor de site gekopieerd naar de submap **Tools\ConsoleSetup** . Desgewenst kunt u de map **ConsoleSetup** naar een andere locatie kopiëren om de installatie te starten. Wanneer u de site bijwerkt, blijft de lokale versie altijd up-to-date.  

- Configuration Manager-installatie media:`<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    Wanneer u de Configuration Manager-console vanaf het installatie medium installeert, wordt de Engelse versie altijd geïnstalleerd. Dit gedrag treedt zelfs op als de site server verschillende talen ondersteunt, of als het besturings systeem van de doel computer is ingesteld op een andere taal.  

Als dat mogelijk is, start u het installatie programma van de-console vanuit de map **ConsoleSetup** in plaats van vanaf de bron media.

> [!Important]  
> Installeer de-console niet met behulp van de **cd. Meest recente** bron bestanden. Het is een niet-ondersteund scenario en kan problemen veroorzaken met de installatie van de-console. Zie de CD voor meer informatie [. Meest recente map](../../manage/the-cd.latest-folder.md#unsupported-scenarios).<!-- SCCMDocs issue 1359 -->  

Als u een pakket maakt voor het installeren van de-console op andere computers, moet u ervoor zorgen dat het pakket de volgende bestanden bevat:<!--3612513-->

- ConsoleSetup. exe
- AdminConsole. msi
- ConfigMgr. AC_Extension. i386. cab (vanaf versie 1902)
- ConfigMgr. AC_Extension. amd64. cab (vanaf versie 1902)



## <a name="use-the-setup-wizard"></a>De wizard Setup gebruiken  

1. Blader naar het bronpad en open **ConsoleSetup. exe**.  

    > [!IMPORTANT]  
    > Installeer de-console altijd via **ConsoleSetup. exe**. Hoewel u de Configuration Manager-console kunt installeren door AdminConsole. msi uit te voeren, voert deze methode geen vereisten of afhankelijkheids controles uit. De installatie wordt mogelijk niet correct geïnstalleerd.  

2. Selecteer **volgende**in de wizard.  

3. Voer op de pagina **Site Server** de Fully QUALIFIED domain name (FQDN) in van de site server waarmee de Configuration Manager-console verbinding maakt.  

4. Voer op de pagina **installatiemap** de installatiemap voor de Configuration Manager-console in. Het mappad mag geen Volg spaties of Unicode-tekens bevatten.  

5. Selecteer op de pagina **Customer Experience Improvement Program** of u wilt samen voegen met de Customer Experience Improvement Program (CEIP).  

    > [!Note]  
    > Vanaf Configuration Manager versie 1802 wordt de functie CEIP verwijderd uit het product.

6. Selecteer **installeren**op de pagina **gereed voor installatie** .  



## <a name="install-from-a-command-prompt"></a>Installeren vanaf een opdracht prompt  

> [!TIP]  
> Wanneer u de Configuration Manager-console installeert vanaf een opdracht prompt, wordt de Engelse versie altijd geïnstalleerd. Dit gedrag treedt zelfs op als het besturings systeem van de doel computer is ingesteld op een andere taal. Als u de Configuration Manager-console in een andere taal dan Engels wilt installeren, [gebruikt u de wizard Setup](#use-the-setup-wizard).  


### <a name="consolesetupexe-command-line-options"></a>Opdracht regel opties voor ConsoleSetup. exe

#### <a name="q"></a>/q

Installeert de Configuration Manager-console zonder toezicht. De opties **EnableSQM**, **TargetDir**en **DefaultSiteServerName** zijn vereist wanneer u deze optie gebruikt.

#### <a name="uninstall"></a>/uninstall

Hiermee verwijdert u de Configuration Manager-console. Geef deze optie eerst op wanneer u deze gebruikt met de optie **/q** .

#### <a name="langpackdir"></a>LangPackDir

Hiermee geeft u het pad op naar de map die de taal bestanden bevat. U kunt het download programma voor de **installatie** gebruiken om de taal bestanden te downloaden. Als u deze optie niet gebruikt, zoekt Setup naar de taalmap in de huidige map. Als de taal map niet wordt gevonden, blijft de installatie van alleen Engels. Zie het [Download programma](setup-downloader.md)voor meer informatie.

#### <a name="targetdir"></a>TargetDir

Hiermee geeft u de installatiemap op voor de installatie van de Configuration Manager-console. Deze optie is vereist wanneer u de optie **/q** gebruikt.

#### <a name="enablesqm"></a>EnableSQM

Hiermee wordt opgegeven of de Customer Experience Improvement Program (CEIP) moet worden toegevoegd. Gebruik de waarde **1** om lid te worden van het CEIP en een waarde van **0** om het programma niet toe te voegen. Deze optie is vereist wanneer u de optie **/q** gebruikt.

> [!Important]  
> Vanaf Configuration Manager versie 1802 wordt de functie CEIP verwijderd uit het product. Als u de para meter gebruikt, mislukt de installatie.

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

Hiermee geeft u de FQDN op van de site server waarmee de console verbinding maakt wanneer deze wordt geopend. Deze optie is vereist wanneer u de optie **/q** gebruikt.


### <a name="examples"></a>Voorbeelden

> [!Important]  
> Neem voor versie 1802 en hoger de para meter **EnableSQM** niet op

#### <a name="silent-install"></a>Stille installatie

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Stille installatie met taal pakketten

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Achtergrond verwijderen

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>Zie ook

Een beheerder ziet objecten in de-console op basis van de machtigingen die zijn toegewezen aan hun gebruikers account. Zie [basis principes van beheer op basis van rollen](../../../understand/fundamentals-of-role-based-administration.md)voor meer informatie.

Zie [using the console](../../manage/admin-console.md)(Engelstalig) voor meer informatie over de grond beginselen van het navigeren door de Configuration Manager-console.

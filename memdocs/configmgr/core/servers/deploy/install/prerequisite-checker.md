---
title: Prerequisite Checker
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van prerequisite Checker voor het identificeren en oplossen van problemen die de installatie van een site of site systeemrol kunnen blok keren.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ee871d99285bee3a4489d88bf0d203bf74cde3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718173"
---
# <a name="prerequisite-checker-for-configuration-manager"></a>Prerequisite Checker voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

 Voordat u het installatie programma uitvoert om een Configuration Manager site te installeren of bij te werken of voordat u een site systeemrol op een nieuwe server installeert, kunt u deze zelfstandige toepassing (**Prereqchk. exe**) gebruiken uit de versie van Configuration Manager die u wilt gebruiken om de gereedheid van de server te controleren. Gebruik de prerequisite checker om problemen op te sporen en op te lossen die de installatie van een site of site systeemrol blok keren.  

> [!NOTE]  
>  Prerequisite checker wordt altijd uitgevoerd als onderdeel van Setup.  

Wanneer prerequisite checker wordt uitgevoerd:  

-   Hiermee wordt de server gevalideerd waarop deze wordt uitgevoerd.  
-   De lokale computer wordt gescand op een bestaande site server en alleen de controles die van toepassing zijn op de site worden uitgevoerd.  
-   Als er geen bestaande sites worden gedetecteerd, worden alle vereiste regels uitgevoerd.  
-   Er worden regels gecontroleerd om te controleren of de vereiste software en instellingen voor de installatie zijn geïnstalleerd. Het is mogelijk dat vereiste software aanvullende configuratie-of software-updates nodig heeft die niet worden gecontroleerd door de prerequisite Checker.  
-   De resultaten worden geregistreerd in het bestand **ConfigMgrPrereq. log** op het systeem station van de computer. Het logboek bestand kan aanvullende informatie bevatten die niet in de toepassings interface wordt weer gegeven.  

Wanneer u prerequisite Checker uitvoert vanaf een opdracht prompt en specifieke opdracht regel opties opgeeft:  

-   Prerequisite Checker voert alleen de controles uit die zijn gekoppeld aan de site server of site systemen die u opgeeft op de opdracht regel.  
-   Als u een externe computer wilt controleren, moet uw gebruikers account over beheerders rechten voor de externe computer beschikken.  

Voor meer informatie over de controles die prerequisite Checker uitvoert, zie de [lijst met vereisten controles voor Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Prerequisite Checker-bestanden kopiëren naar een andere computer  

1.  Ga in Windows Verkenner naar een van de volgende locaties:  

    -   **&lt;*Configuration Manager installatie media*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager installatiepad*\>\BIN\X64**  

2.  Kopieer de volgende bestanden naar de doelmap op de andere computer:  

    - prereqchk. exe
    - prereqcore. dll
    - prereqchkres. dll
      - Dit bestand bevindt zich in de submap voor de taal van de installatie. Bijvoorbeeld: Engels bevindt zich `00000409` in de submap. <!--586808-->
    - basesql. dll
    - basesvr. dll
    - baseutil. dll

##  <a name="run-prerequisite-checker-with-default-checks"></a>Prerequisite Checker uitvoeren met standaard controles  

1.  Ga in Windows Verkenner naar een van de volgende locaties:  

    -   **&lt;*Configuration Manager installatie media*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager installatiepad*\>\BIN\X64**  

2.  Voer **prereqchk. exe** uit om prerequisite Checker te starten.   
    Prerequisite Checker detecteert bestaande sites, en indien gevonden, voert controles uit voor upgrade Readiness. Als er geen sites worden gevonden, worden alle controles uitgevoerd. De kolom **site type** bevat informatie over de site server of het site systeem waaraan de regel is gekoppeld.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Prerequisite Checker uitvoeren vanaf een opdracht prompt voor alle standaard controles  

1.  Open een opdracht prompt venster en wijzig de mappen in een van de volgende locaties:  

    -   **&lt;*Configuration Manager installatie media*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager installatiepad*\>\BIN\X64**  

2.  Voer **prereqchk. exe/Local** in om prerequisite Checker te starten en alle vereiste controles op de server uit te voeren.  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>Prerequisite Checker uitvoeren vanaf een opdracht prompt om opties te gebruiken  

1. Open een opdracht prompt venster en wijzig de mappen in een van de volgende locaties:  

   -   **&lt;*Configuration Manager installatie media*\>\SMSSETUP\BIN\X64**  
   -   **&lt;*Configuration Manager installatiepad*\>\BIN\X64**  

2. Voer **prereqchk. exe** in om een of meer van de volgende opdracht regel opties toe te voegen.  

   Als u bijvoorbeeld een primaire site wilt controleren, kunt u het volgende gebruiken:  

      **prereqchk. exe [/NOUI]/PRI/SQL &lt;fqdn van SQL Server\> /SDK &lt;FQDN van de SMS\> -provider &lt;[/join FQDN van de\>centrale beheer site &lt;] [/MP FQDN\>van het beheer &lt;punt] [/DP\>FQDN van het distributie punt]**  

   **Server van centrale beheer site:**  

   -   **/NOUI**  

        Niet vereist. Hiermee wordt de prerequisite Checker gestart zonder de gebruikers interface weer te geven. U moet deze optie vóór een andere optie opgeven op de opdracht regel.  

   -   **/CAS**  

        Vereist. Verifieert of de lokale computer voldoet aan de vereisten voor de centrale beheer site.  

   -   **/SQL &lt; *FQDN van SQL Server*>**  

        Vereist. Door de Fully Qualified Domain Name (FQDN) te gebruiken, controleert u of de opgegeven computer voldoet aan de vereisten voor SQL Server om de data base van de Configuration Manager-site te hosten.  

   -   **/SDK &lt; *FQDN van SMS-provider*>**  

        Vereist. Verifieert of de opgegeven computer voldoet aan de vereisten voor de SMS-provider.  

   -   **/Ssbport**  

        Niet vereist. Verifieert of er een firewall uitzondering actief is om communicatie toe te staan op de poort van SQL Server Service Broker (SSB). De standaard SSB-poort is 4022.  

   -   **Installatiepad &lt;van InstallDir *Configuration Manager*>**  

        Niet vereist. Hiermee wordt de minimale schijf ruimte gecontroleerd op vereisten voor site-installatie.  

   **Primaire site server:**  

   -   **/NOUI**  

       Niet vereist. Hiermee wordt de prerequisite Checker gestart zonder de gebruikers interface weer te geven. U moet deze optie vóór een andere optie opgeven op de opdracht regel.  

   -   **/PRI**  

        Vereist. Verifieert of de lokale computer voldoet aan de vereisten voor de primaire site.  

   -   **/SQL &lt; *FQDN van SQL Server*>**  

        Vereist. Verifieert of de opgegeven computer voldoet aan de vereisten voor SQL Server om de Configuration Manager-site database te hosten.  

   -   **/SDK &lt; *FQDN van SMS-provider*>**  

        Vereist. Verifieert of de opgegeven computer voldoet aan de vereisten voor de SMS-provider.  

   -   **/Join &lt; *FQDN van de centrale beheer site*>**  

        Niet vereist. Verifieert of de lokale computer voldoet aan de vereisten om verbinding te maken met de server van de centrale beheer site.  

   -   **/MP &lt; *FQDN van beheer punt*>**  

        Niet vereist. Verifieert of de opgegeven computer voldoet aan de vereisten voor de site systeemrol van het beheer punt. Deze optie wordt alleen ondersteund wanneer u de optie **/pri** gebruikt.  

   -   **/DP &lt; *FQDN van distributie punt*>**  

        Niet vereist. Verifieert of de opgegeven computer voldoet aan de vereisten voor de site systeemrol van het distributie punt. Deze optie wordt alleen ondersteund wanneer u de optie **/pri** gebruikt.  

   -   **/Ssbport**  

        Niet vereist. Verifieert of er een firewall uitzondering actief is om communicatie toe te staan voor de SSB-poort. De standaard SSB-poort is 4022.  

   -   **Installatiepad &lt;van InstallDir *Configuration Manager*>**  

        Niet vereist. Hiermee wordt de minimale schijf ruimte gecontroleerd op vereisten voor site-installatie.  

   **Secundaire site server:**  

   -   **/NOUI**  

        Niet vereist. Hiermee wordt de prerequisite Checker gestart zonder de gebruikers interface weer te geven. U moet deze optie vóór een andere optie opgeven op de opdracht regel.  

   -   **&lt; *FQDN-naam van secundaire site server* /sec.>**  

        Vereist. Verifieert of de opgegeven computer voldoet aan de vereisten voor de secundaire site.  

   -   **/INSTALLSQLEXPRESS**  

        Niet vereist. Hiermee wordt gecontroleerd of SQL Server Express op de opgegeven computer kan worden geïnstalleerd.  

   -   **/Ssbport**  

        Niet vereist. Verifieert of er een firewall uitzondering actief is om communicatie toe te staan voor de SSB-poort. De standaard SSB-poort is 4022.  

   -   **/Sqlport**  

        Niet vereist. Verifieert of er een firewall uitzondering actief is om communicatie toe te staan voor de SQL Server service poort en dat de poort niet wordt gebruikt door een ander benoemd exemplaar van SQL Server. De standaardpoort is 1433.  

   -   **Installatiepad &lt;van InstallDir *Configuration Manager*>**  

        Niet vereist. Hiermee wordt de minimale schijf ruimte gecontroleerd op vereisten voor site-installatie.  

   -   **/SourceDir**  

        Niet vereist. Hiermee wordt gecontroleerd of het computer account van de secundaire site toegang heeft tot de map die de bron bestanden host voor het installatie programma.  

   **Configuration Manager-console:**  

   -   **/Adminui**  

        Vereist. Verifieert of de lokale computer voldoet aan de vereisten voor het installeren van Configuration Manager.  

3. In de gebruikers interface van prerequisite checker wordt met prerequisite Checker een lijst met gedetecteerde problemen gemaakt in de sectie met de **vereiste resultaten** .  

   -   Klik op een item in de lijst voor meer informatie over het oplossen van het probleem.  
   -   U moet alle items in de lijst met een **fout** status oplossen voordat u de site server, het site systeem of de Configuration Manager-console installeert.  
   -   U kunt ook het bestand **ConfigMgrPrereq. log** in de hoofdmap van het systeem station openen om de resultaten van de controle van vereisten te controleren. Het logboek bestand kan aanvullende informatie bevatten die niet wordt weer gegeven in de gebruikers interface van de prerequisite Checker.  

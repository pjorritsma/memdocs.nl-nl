---
title: Windows-computer op afstand beheren
titleSuffix: Configuration Manager
description: Een externe Windows-client computer beheren met behulp van Configuration Manager.
ms.date: 11/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801654b95470889d0b661315d40d3e00efa8e542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715107"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-configuration-manager"></a>Een Windows-client computer op afstand beheren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)* Met Configuration Manager kunt u verbinding maken met client computers met behulp van **Configuration Manager beheer op afstand**. Voordat u met beheer op afstand begint, moet u de informatie in de volgende artikelen door nemen:  

-   [Vereisten voor extern beheer](prerequisites-for-remote-control.md)  

-   [Configureren van beheer op afstand](configuring-remote-control.md)  

Hier volgen drie manieren om de viewer voor beheer op afstand te starten:  

-   In de Configuration Manager-console.  

-   In een Windows-opdracht prompt.  

-   Ga in het menu **Start** van Windows op een computer waarop de Configuration Manager-console wordt uitgevoerd, in de programma groep **micro soft System Center** .  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Een clientcomputer op afstand beheren vanuit de Configuration Manager-console  

1.  Kies in de Configuration Manager-console de optie **activa en nalevings** > **apparaten** of **apparaat-verzamelingen**.  

3.  Selecteer de computer die u op afstand wilt beheren en kies op het tabblad **Start** in de groep **apparaat** de optie beheer **op** > **afstand**starten.  

    > [!IMPORTANT]  
    >  Als de clientinstelling **Gebruikers vragen naar machtiging voor Beheer op afstand** is ingesteld op **Waar**, wordt de verbinding pas geïnitieerd als de gebruiker op de externe computer hiermee instemt. Zie [Configuring Remote Control](configuring-remote-control.md)(Engelstalig) voor meer informatie.  

4.  Als het venster **Configuration Manager - Beheer op afstand** wordt geopend, kunt u de clientcomputer op afstand beheren. Gebruik de volgende opties om de verbinding te configureren.  

    > [!NOTE]  
    >  Als de computer waarmee u verbinding maakt, meerdere monitors heeft, wordt de weer gave van alle monitors weer gegeven in het venster voor beheer op afstand.  

    -   **Bestand**
        - **Verbinden** : Maak verbinding met een andere computer. Deze optie is niet beschikbaar als een sessie voor beheer op afstand actief is.  
        -   **Verbreek** de verbinding met de actieve sessie voor beheer op afstand, maar sluit het venster **Configuration Manager beheer op afstand** niet.  
        - **Afsluiten** : Hiermee wordt de actieve sessie voor beheer op afstand verbroken en wordt het venster **Configuration Manager beheer op afstand** gesloten.  

        > [!NOTE]  
        >  Wanneer u de verbinding van een sessie voor beheer op afstand verbreekt, wordt op de computer die u weergeeft de inhoud van het Windows Klembord verwijderd.


    - **Weergave**
      - **Kleur diepte** : Kies 16 bits of 32 bits per pixel.
      -  **Volledig scherm** : maximaliseert het venster **Configuration Manager beheer op afstand** . Druk op Ctrl+Alt+Break om de modus voor volledig scherm af te sluiten.  
      - **Optimaliseren voor verbinding met lage band breedte** : Kies deze optie als de verbinding een lage band breedte heeft.
      - **Weergave:**
        - **Alle schermen** -toegevoegd in Configuration Manager 1902. Als de computer waarmee u verbinding maakt, meerdere monitors heeft, wordt de weer gave van alle monitors weer gegeven in het venster voor beheer op afstand. **Alle schermen** is de enige weer gave voor computers met meerdere monitors vóór 1902.
        -  **Eerste scherm** -toegevoegd in Configuration Manager 1902. Het *eerste scherm* bevindt zich bovenaan en links, zoals wordt weer gegeven in de Windows-weer gave-instellingen. U kunt geen specifiek scherm selecteren. Wanneer u de configuratie van de viewer overschakelt, moet u opnieuw verbinding maken met de externe sessie. De viewer slaat uw voor keur voor toekomstige verbindingen op.
        -  **Schaal aanpassen aan** de weer gave van de externe computer zodat deze overeenkomt met de grootte van het venster **Configuration Manager beheer op afstand** .
        - **Status balk** : Hiermee schakelt u de weer gave van de Configuration Manager status balk voor **beheer op afstand** .  

       > [!NOTE]  
       >  De viewer slaat uw voor keur voor toekomstige verbindingen op.

    -   **Actie**
        - **Toets Ctrl + Alt + del verzenden** : Hiermee verzendt u een toetscombinatie met Ctrl + Alt + del naar de externe computer. 
        - **Klem bord delen inschakelen** : Hiermee kunt u items naar en van de externe computer kopiëren en plakken. Als u deze waarde wijzigt, moet u de sessie voor beheer op afstand opnieuw starten om de wijziging door te voeren.   
          - Als u klem bord delen niet wilt inschakelen in de Configuration Manager-console, stelt u op de computer waarop de-console wordt uitgevoerd, de waarde van de register sleutel **HKEY_CURRENT_USER \Software\microsoft\configmgr10\remote Control\clipboard sharing delen** in op **0**.
        - **Toetsenbord vertaling inschakelen** : vertaalt de toetsenbord indeling van de computer waarop de-console wordt uitgevoerd naar de indeling van het verbonden apparaat.
        - **Extern toetsen bord en muis vergren delen** : Hiermee vergrendelt u het externe toetsen bord en de muis om te voor komen dat de gebruiker de externe computer kunt gebruiken.  

    -   **Help**
        - **Over extern beheer** : hier wordt de huidige versie van de viewer weer gegeven.  

5.  Gebruikers op de externe computer kunnen meer informatie over de sessie voor beheer op afstand weer geven wanneer ze op het pictogram Configuration Manager **beheer op afstand** klikken. Het pictogram bevindt zich in het Windows-systeemvak of het pictogram op de sessie balk voor beheer op afstand.  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>De viewer voor beheer op afstand starten via de Windows-opdrachtregel  

-   Typ _<Configuration Manager installatiemap\>_ in het Windows-opdracht prompt**\AdminConsole\Bin\i386\CmRcViewer.exe**  

CmRcViewer.exe ondersteunt de volgende opdrachtregelopties:  

- *Adres* : Hiermee geeft u de NetBIOS-naam, de Fully QUALIFIED domain name (FQDN) of het IP-adres van de client computer waarmee u verbinding wilt maken.
- *Naam site server* : Hiermee geeft u de naam op van de Configuration Manager site server waarnaar u status berichten wilt verzenden die zijn gerelateerd aan de sessie voor beheer op afstand.
- **/?** -Hiermee geeft u de opdracht regel opties voor de viewer voor beheer op afstand weer.  
     
**Voor beeld: CmRcViewer. exe** *<\> adres* * < \\\Site server name>* 

> [!NOTE]  
> De viewer voor beheer op afstand wordt ondersteund op alle besturings systemen die worden ondersteund voor de Configuration Manager-console. Zie [ondersteunde configuraties voor Configuration Manager-consoles](../../../plan-design/configs/supported-operating-systems-consoles.md) en- [vereisten voor beheer op afstand](prerequisites-for-remote-control.md)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Gebruik van beheer op afstand controleren](audit-remote-control-usage.md)

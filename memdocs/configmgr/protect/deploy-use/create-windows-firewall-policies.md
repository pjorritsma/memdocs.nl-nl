---
title: Windows Firewall beleid voor Endpoint Protection
titleSuffix: Configuration Manager
description: Meer informatie over het maken en implementeren van firewall beleid voor Endpoint Protection in System Center 2012 Configuration Manager.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c017e750e175e09a67deb4651cf7e8eb98f1bc1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715492"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-configuration-manager"></a>Windows Firewall-beleid voor Endpoint Protection in Configuration Manager maken en implementeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met het firewall beleid voor Endpoint Protection in Configuration Manager kunt u eenvoudige Windows Firewall configuratie-en onderhouds taken uitvoeren op client computers in uw hiërarchie. U kunt met de Windows Firewall-beleidsregels de volgende taken uitvoeren:  

-   Bepalen of Windows Firewall is in- of uitgeschakeld.  

-   Bepalen of binnenkomende verbindingen naar clientcomputers zijn toegestaan.  

-   Bepalen of gebruikers een melding ontvangen wanneer Windows Firewall een nieuw programma blokkeert.  

1.  Klik op **Activa en naleving**op de Configuration Manager-console.  

2.  Vouw in de werk ruimte **activa en naleving** de optie **Endpoint Protection**uit en klik vervolgens op **Windows Firewall beleids regels**.  

3.  Klik op het tabblad **Start** in de groep **Maken** op **Windows Firewall-beleid maken**.  

4.  Geef op de pagina **Algemeen** van de **wizard Windows Firewall-beleid maken**een naam en eventueel een beschrijving voor dit firewallbeleid op en klik vervolgens op **Volgende**.  

5.  Configureer op de pagina **Profielinstellingen** van de wizard de volgende instellingen voor elk netwerkprofiel:  

    > [!NOTE]  
    >  Raadpleeg de Windows-documentatie voor meer informatie over netwerkprofielen.  

    -   **Windows Firewall inschakelen**  

        > [!NOTE]  
        >  Als **Windows Firewall inschakelen** niet is ingeschakeld, zijn de andere instellingen op deze pagina van de wizard niet beschikbaar.  

    -   **Alle binnenkomende verbindingen blokkeren, inclusief verbindingen in de lijst met toegestane programma's**  

    -   **De gebruiker waarschuwen wanneer een nieuw programma door Windows Firewall wordt geblokkeerd**  

6.  Controleer welke acties moeten worden ondernomen op de pagina **Overzicht** van de wizard en voltooi de wizard.  

7.  Controleer of de nieuwe Windows Firewall-beleid wordt weergegeven in de lijst **Windows Firewall-beleid** .  

##  <a name="to-deploy-a-windows-firewall-policy"></a><a name="BKMK_Assign"></a> Een Windows Firewall-beleid implementeren  

1.  Klik op **Activa en naleving**op de Configuration Manager-console.  

2.  Vouw in de werk ruimte **activa en naleving** de optie **Endpoint Protection**uit en klik vervolgens op **Windows Firewall beleids regels**.  

3.  Selecteer in de lijst **Windows Firewall-beleid** het Windows Firewall-beleid dat u wilt implementeren.  

4.  Klik op het tabblad **Start** in de groep **Implementatie** op **Implementeren**.  

5.  Geef in het dialoogvenster **Windows Firewall-beleid implementeren** de verzameling op waaraan u dit Windows Firewall-beleid wilt toewijzen en geef een toewijzingsplanning op. Het Windows Firewall-beleid evalueert de naleving door gebruik te maken van dit schema en configureert de Windows Firewall-instellingen op clients opnieuw zodat wordt voldaan aan het Windows Firewall-beleid.  

6.  Klik op **OK** om het dialoogvenster **Windows Firewall-beleid implementeren** te sluiten en het Windows Firewall-beleid te implementeren.  

    > [!IMPORTANT]  
    >  Wanneer u een Windows Firewall-beleid voor een verzameling implementeert, wordt dit beleid gedurende een periode van twee uur in willekeurige volgorde toegepast op computers om te voorkomen dat het netwerk wordt overspoeld.

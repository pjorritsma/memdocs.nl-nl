---
title: Energiebeheer schema's maken en Toep assen
titleSuffix: Configuration Manager
description: Energiebeheer schema's maken en Toep assen in Configuration Manager.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ba5479a4c75d3ab8f91a8439a6799589b93972d0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076693"
---
# <a name="how-to-create-and-apply-power-plans-in-configuration-manager"></a>Energiebeheer schema's maken en Toep assen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met energie beheer in Configuration Manager kunt u energie schema's Toep assen die worden geleverd met Configuration Manager aan verzamelingen computers in uw hiërarchie, of uw eigen aangepaste energiebeheer schema's maken. Volg de procedure in dit onderwerp om een ingebouwd of aangepast energiebeheerschema op computers toe te passen.  

> [!IMPORTANT]  
>  U kunt alleen Configuration Manager energiebeheer schema's Toep assen op apparaten in verzamelingen.  

 Als een computer lid is van meerdere verzamelingen, die elk verschillende energiebeheerschema’s toepassen, worden de volgende acties ondernomen:  

- Energiebeheerschema: als er meerdere waarden voor energie-instellingen op een computer worden toegepast, wordt de minst beperkende waarde gebruikt.  

- Activeringstijd: als er meerdere activeringstijden worden toegepast op een desktopcomputer, wordt de tijd gebruikt die het dichtst bij middernacht ligt.  

  Gebruik het rapport **Computers met meerdere energiebeheerschema's** om alle computers weer te geven waarop meerdere energiebeheerschema's worden toegepast. Hierdoor kunt u computers met energiebeheerconflicten ontdekken. Zie [energie beheer bewaken en plannen voor](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)meer informatie over energiebeheer rapporten.  

> [!IMPORTANT]  
>  Energie-instellingen die zijn geconfigureerd met behulp van Windows groepsbeleid, overschrijven de instellingen die zijn geconfigureerd door Configuration Manager energie beheer.  

 Gebruik de volgende procedure om een Configuration Manager energiebeheer schema te maken en toe te passen.  

### <a name="to-create-and-apply-a-power-plan"></a>Een energiebeheerschema maken en toepassen  

1. Klik op **Activa en naleving**op de Configuration Manager-console.  

2. Klik op **Apparaatverzamelingen** in de werkruimte **Activa en naleving**.  

3. Klik in de lijst **Apparaatverzamelingen** op de verzameling waarop u instellingen voor energiebeheer wilt toepassen en klik vervolgens op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

4. Selecteer op het tabblad **energie beheer** van het dialoog venster**Eigenschappen** van <em><\>verzameling</em> **instellingen energie beheer opgeven voor deze verzameling**.  

   > [!NOTE]  
   >  U kunt ook klikken op **Bladeren** en de instellingen voor energiebeheer van een geselecteerde verzameling naar de geselecteerde verzameling kopiëren.  

5. Geef in het veld **Start** en het veld **Einde** de begin- en eindtijd voor piekuren (of kantooruren) op.  

6. Schakel **Activeringstijd (desktopcomputers)** in om een tijd op te geven waarop een desktopcomputer uit de slaapstand of sluimerstand wordt gehaald om geplande updates of software-installaties te installeren.  

   > [!IMPORTANT]  
   >  Energiebeheer maakt gebruik van de interne Windows-activeringsfunctie om computers uit de slaapstand of sluimerstand te halen. Activeringstijdinstellingen worden niet toegepast op draagbare computers om te voorkomen dat ze worden geactiveerd wanneer ze niet op netstroom zijn aangesloten. De activeringstijd wordt op een willekeurig tijdstip ingesteld en computers worden ergens gedurende een periode van één uur na de opgegeven activeringstijd geactiveerd.  

7. Als u een aangepast energiebeheerschema voor piekuren (of kantooruren) wilt configureren, selecteert u **Aangepaste piek (ConfigMgr)** in de vervolgkeuzelijst **Schema voor piekuren** en klikt u vervolgens op **Bewerken**. Als u een energiebeheerschema voor niet-piekuren (of buiten kantooruren) wilt configureren, selecteert u **Aangepaste niet-piek (ConfigMgr)** in de vervolgkeuzelijst **Schema voor niet-piekuren** en klikt u vervolgens op **Bewerken**.  

   > [!NOTE]  
   >  U kunt het rapport **Computeractiviteit** gebruiken om de planning te bepalen die moet worden gebruikt voor piek- en niet-piekuren wanneer u energiebeheerschema's op verzamelingen computers toepast. Zie [energie beheer bewaken en plannen voor](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)meer informatie.  

    U kunt ook een selectie maken in de ingebouwde energiebeheerschema's, **Gebalanceerd (ConfigMgr)**, **Hoge prestaties (ConfigMgr)** en **Energiebesparing (ConfigMgr)**, en vervolgens op **Weergeven** klikken om de eigenschappen van elk energiebeheerschema weer te geven.  

   > [!NOTE]  
   >  U kunt het ingebouwde energiebeheerschema niet wijzigen.  

8. Configureer de volgende instellingen in het dialoog venster <em>naam\>eigenschappen van<energiebeheer schema</em>:**Properties**  

   -   **Naam:** geef een naam op voor dit energiebeheerschema of gebruik de opgegeven standaardwaarde.  

   -   **Beschrijving:**  geef een beschrijving op voor dit energiebeheerschema of gebruik de opgegeven standaardwaarde.  

   -   **De eigenschappen opgeven voor deze energieplanning:** configureer de eigenschappen van het energiebeheerschema. Schakel het selectievakje uit als u een eigenschap wilt uitschakelen. Zie [Available power management plan settings](#BKMK_Plans) in dit onderwerp voor meer informatie over de beschikbare instellingen.  

       > [!IMPORTANT]  
       >  Ingeschakelde instellingen worden toegepast op computers wanneer het energiebeheerschema wordt toegepast. Als u het selectievakje voor een energiebeheerschema uitschakelt, wordt de waarde op de clientcomputer niet gewijzigd wanneer het energiebeheerschema wordt toegepast. Door een selectievakje uit te schakelen worden de energiebeheerinstellingen niet hersteld naar de vorige waarde voordat een energiebeheerschema werd toegepast.  

9. Klik op **OK** om**het dialoog venster** <em><naam\>van het energiebeheer schema</em>te sluiten.  

10. Klik op **OK** om het dialoog venster**instellingen** voor <em><\>verzamelings naam</em>te sluiten en het energiebeheer schema toe te passen.  

##  <a name="available-power-management-plan-settings"></a><a name="BKMK_Plans"></a> Available power management plan settings  
 De volgende tabel bevat de instellingen voor energie beheer die beschikbaar zijn in Configuration Manager. U kunt afzonderlijke instellingen configureren voor wanneer de computer op netstroom is aangesloten of op de accu werkt. Afhankelijk van de versie van Windows die u gebruikt, kunnen bepaalde instellingen mogelijk niet worden geconfigureerd.  

> [!NOTE]  
>  Energie-instellingen die u niet configureert, behouden hun huidige waarde op clientcomputers.  

|Naam|Beschrijving|  
|----------|-----------------|  
|**Beeldscherm uitschakelen na (minuten)**|Hiermee geeft u de tijdsduur aan in minuten die de computer inactief moet zijn voordat het beeldscherm wordt uitgeschakeld. Geef de waarde **0** op als u niet wilt dat energiebeheer het beeldscherm uitschakelt.|  
|**Slaapstand na (minuten)**|Hiermee geeft u de tijdsduur in minuten aan die de computer inactief moet zijn voordat de slaapstand in werking treedt. Geef de waarde **0** op als u niet wilt dat energiebeheer de computer naar de slaapstand laat overschakelen.|  
|**Een wachtwoord vereisen bij uit slaapstand komen**|Een waarde **Ja** of **Nee** geeft aan of een wacht woord vereist is om de computer te ontgrendelen wanneer de Wake vanuit de slaap stand wordt geactiveerd.|  
|**Actie knop Energie**|Hiermee geeft u de actie op die wordt uitgevoerd wanneer de aan/uit-knop van de computer wordt ingedrukt. Mogelijke waarden **doen niets**, **slaap stand**, **sluimer stand**en **Afsluiten**.|  
|**Aan-uitknop in het menu Start**|Hiermee geeft u de actie op die wordt uitgevoerd wanneer u op de knop aan/uit in het menu **Start** van de computer drukt. Mogelijke waarden voor de **slaap stand**, **sluimer stand**en **Afsluiten**.|  
|**Actie van de slaapstandknop**|Hiermee geeft u de actie op die wordt uitgevoerd wanneer u op de **slaapstandknop** van de computer drukt. Mogelijke waarden **doen niets**, **slaap stand**, **sluimer stand**en **Afsluiten**.|  
|**Actie deksel sluiten**|Hiermee geeft u de actie aan die wordt uitgevoerd wanneer de gebruiker het deksel een draagbare computer sluit. Mogelijke waarden **doen niets**, **slaap stand**, **sluimer stand**en **Afsluiten**.|  
|**Vaste schijf uitschakelen na (minuten)**|Hiermee geeft u de tijds duur in minuten op dat de harde schijf van de computer inactief moet zijn voordat deze wordt uitgeschakeld. Geef een waarde van **0** op als u niet wilt dat energie beheer de vaste schijf van de computer uitschakelt.|  
|**Sluimerstand na (minuten)**|Hiermee geeft u de tijdsduur in minuten aan die de computer inactief moet zijn voordat de sluimerstand in werking treedt. Geef de waarde **0** op als u niet wilt dat energiebeheer de computer naar de sluimerstand overschakelt.|  
|**Actie batterij laag**|Hiermee geeft u de actie op die wordt uitgevoerd wanneer de accu van de computer het opgegeven meldings niveau voor laag accu bereikt. Mogelijke waarden **doen niets**, **slaap stand**, **sluimer stand**en **Afsluiten**.|  
|**Actie kritieke batterij**|Hiermee geeft u de actie op die wordt uitgevoerd wanneer de accu van de computer het opgegeven kritieke meldings niveau bereikt. Als **er op de accu** mogelijke waarden in de **slaap stand**, **sluimer stand**en **Afsluiten**worden uitgevoerd. Als u de mogelijke waarden hebt **aangesloten** , **gebeurt niets**, **slaap stand**, **sluimer stand**en **Afsluiten**.|  
|**Hybride slaapstand toestaan**|Als u de waarde aan of **uit** selecteert, geeft u **op** of Windows een slaapstandbestand opslaat tijdens het activeren van de slaap stand. Dit kan worden gebruikt om de status van de computer te herstellen in het geval van stroom verlies terwijl de slaap stand is geactiveerd.<br /><br /> De hybride slaapstand is bedoeld voor desktopcomputers en is standaard niet ingeschakeld op draagbare computers. Op computers waarop Windows 7 wordt uitgevoerd, schakelt u met de hybride slaapstand de functionaliteit van de sluimerstand in.|  
|**Stand-bystatus toestaan tijdens slaapactie**|Als u de waarde **aan** of **uit** selecteert, kan de computer op stand-by worden gezet, waardoor er nog steeds enige stroom wordt verbruikt, maar de computer sneller kan worden geactiveerd. Als deze instelling wordt ingesteld op **Uit**kan de computer alleen in de sluimerstand worden gezet of worden uitgeschakeld.|  
|**Vereiste inactiviteit voor slaapstand (%)**|Hiermee geeft u het percentage niet-actieve tijd van de processortijd van de computer op die is vereist om de computer te laten overschakelen naar de slaapstand. Voor computers met Windows 7 is deze waarde altijd ingesteld op **0**.|  
|**Windows-ontwaaktimer inschakelen voor bureaubladcomputers**|Als u de waarde **in** -of **uitschakelen** selecteert, kan de ingebouwde Windows-timer worden gebruikt door energie beheer om een desktop computer uit te scha kelen. Wanneer een desktopcomputer wordt geactiveerd door middel van de Windows-ontwaaktimer, blijft deze standaard 10 minuten actief zodat de computer updates kan installeren of beleid kan ontvangen.<br /><br /> Ontwaaktimers worden niet ondersteund op draagbare computers om te voorkomen dat ze worden geactiveerd wanneer ze niet op netstroom zijn aangesloten.|  

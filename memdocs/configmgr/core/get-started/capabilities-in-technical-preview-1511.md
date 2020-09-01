---
title: Mogelijkheden van Technical Preview 1511
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1511.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a7b61e1a609e0693ffcd30f3f7dc931f4cb38eef
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193635"
---
# <a name="capabilities-in-technical-preview-1511-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1511 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1511. Deze versie is een basis installatie van de technische preview die u kunt gebruiken om een nieuwe Technical Preview-site te installeren of om een upgrade uit te kunnen uitvoeren van een eerdere versie van de Technical Preview.   Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.  

Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.  

##  <a name="integration-with-windows-update-for-business-in-windows-10"></a><a name="BKMK_WUfB"></a> Integratie met Windows Update voor bedrijven in Windows 10  
 Configuration Manager heeft nu de mogelijkheid om onderscheid te maken tussen een Windows 10-computer die rechtstreeks is verbonden via Windows Update for Business (WUfB) en de computers die met WSUS zijn verbonden voor het ophalen van updates en upgrades voor Windows 10.  Voor computers die zijn verbonden via WUfB kunnen de updates en upgrades worden beheerd op de uitgebracht die is ingesteld door een gebruiker met beheerders rechten via groeps beleid of MDM-beleid. deze updates/upgrades kunnen rechtstreeks vanuit WUfB worden geïnstalleerd.    
Voor computers die zijn verbonden via WUfB is Configuration Manager niet in staat om te rapporteren over de nalevings status (inclusief Windows-updates of definitie-updates). Het is ook Configuration Manager niet mogelijk om micro soft-updates of updates van derden te implementeren op deze computers.  

 **Vereisten voor dit scenario:**  

-   Windows 10 Desktop Pro of Windows 10 Enter prise Edition versie 1511 of hoger  

-   Computers die worden beheerd via [Windows Update voor bedrijven](/windows/deployment/update/waas-manage-updates-wufb).  

### <a name="try-it-out"></a>Probeer het nu!  
 Voer de volgende taak uit en gebruik vervolgens de feedback informatie boven aan dit onderwerp om ons te laten weten hoe het werkt:  

1.  Schakel de Windows Update Agent uit zodat deze niet scant ten opzichte van WSUS als deze eerder werd ingeschakeld.   
    De register sleutel **HKEY_LOCAL_MACHINE \software\policies\microsoft\windows\windowsupdate\au\usewsusserver** kan worden ingesteld om aan te geven of de computer SCANT op WSUS of Windows Update.  Wanneer de waarde 2 is, wordt niet gescand op WSUS.  

2.  Noteer het nieuwe kenmerk **UseWUServer**, onder het knoop punt **Windows Update** in Configuration Manager resource Explorer.  

3.  Maak een verzameling op basis van het **UseWUServer** -kenmerk voor alle computers die via WUfB zijn verbonden voor updates en upgrades.  

4.  Maak een clientagentinstelling voor het uitschakelen van de werkstroom voor software-updates en pas de instelling toe op de verzameling van computers die rechtstreeks zijn verbonden met WUfB.  

5.  Op de computers die via WUfB worden beheerd, wordt **onbekend** weer gegeven in de compatibiliteits status en worden niet geteld als onderdeel van het algehele compatibiliteits percentage.  

##  <a name="managing-microsoft-365-apps-for-enterprise-client-update-through-configuration-manager"></a><a name="BKMK_Office365ProPlus"></a> Microsoft 365-apps voor Enter prise-client update beheren via Configuration Manager  
Configuration Manager hebt nu de mogelijkheid om Microsoft 365-client updates te beheren met behulp van de Configuration Manager Software Update Management-werk stroom.
Wanneer micro soft een nieuwe Microsoft 365 bureau blad-client update publiceert naar Windows Server Update Services (WSUS), kan Configuration Manager de update synchroniseren naar de catalogus als de Microsoft 365 update is geconfigureerd om deel uit te maken van de catalogus synchronisatie.  De Configuration Manager-site server downloadt de Microsoft 365-client updates en distribueert het pakket naar Configuration Manager distributie punten.  De Configuration Manager-client waarschuwt Microsoft 365 desktop-clients waar de updates worden opgehaald en wanneer het installatie proces van de update wordt gestart.  

**Vereisten voor dit scenario:**  

### <a name="try-it-out"></a>Probeer het nu!  
 Voer de volgende taak uit en gebruik vervolgens de feedback informatie boven aan dit onderwerp om ons te laten weten hoe het werkt:  

1. U kunt Microsoft 365 updates synchroniseren naar de Configuration Manager-site server en deze weer geven vanuit de Configuration Manager-console.  

2. U kunt Microsoft 365 updates goed keuren en implementeren.  

3. U kunt updates voor clients downloaden en Microsoft 365.  

4. U kunt naleving voor Microsoft 365-updates controleren met behulp van de controle of rapporten in de console.  

   Zie [Microsoft 365-client updates beheren met Configuration Manager Technical Preview](/deployoffice/manage-microsoft-365-apps-updates-configuration-manager)voor gedetailleerde stappen.  

##  <a name="support-for-sql-server-alwayson-for-highly-available-databases"></a><a name="BKMK_AlwasyOn"></a> Ondersteuning voor SQL Server AlwaysOn voor Maxi maal beschik bare data bases  
 Configuration Manager ondersteunt nu het gebruik van een SQL Server AlwaysOn-beschikbaarheids groepen voor het hosten van de site database.  Wanneer u een nieuwe site installeert, kunt u instellen dat de beschikbaarheids groep wordt gebruikt in plaats van een normaal exemplaar van SQL Server.  

> [!NOTE]  
>  Voor een geslaagde configuratie en het gebruik van beschikbaarheids groepen moet u vertrouwd zijn met het configureren van SQL Server-beschikbaarheids groepen en is afhankelijk van de documentatie en procedures in de documentatie bibliotheek van SQL Server.  

Het proces op hoog niveau voor het configureren en gebruiken van beschikbaarheids groepen omvat:  

1.  Configureer de beschikbaarheids groep in SQL Server.  

2.  Installeer een nieuwe Configuration Manager-site en tijdens de installatie moet de site de beschikbaarheids groep gebruiken door het eind punt van de groepen op te geven.  

**Vereisten voor dit scenario:**  

-   Vereist een versie van SQL Server die wordt ondersteund door de Configuration Manager Technical Preview  

-   U moet de SQL Server beschikbaarheids groep maken en configureren voordat u Configuration Manager installeert  

-   De beschikbaarheidsgroep moet één primaire replica hebben, en mag maximaal twee gesynchroniseerde, secundaire replica’s hebben  

-   De beschikbaarheids groep moet ten minste één eind punt hebben  

-   U moet een netwerk locatie hebben die elke SQL Server in de beschikbaarheids groep kan openen. Deze locatie wordt gebruikt door Setup bij het configureren van de beschikbaarheids groep en kan worden verwijderd nadat de installatie is voltooid.  

**Bekende problemen voor deze release:**  

-   U kunt geen nieuw lid van de replica toevoegen aan een beschikbaarheids groep die al wordt gebruikt als een site database. In plaats daarvan moet u de site opnieuw installeren nadat het nieuwe lid van de replica is toegevoegd.  

-   Voor dit scenario moet u mogelijk de **SQL Server 2012 native client** installeren ([vanuit het SQL Server 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=29065)) op de beheer punt server. Hiermee wordt voor komen dat SQL-verbindings fouten (die worden vastgelegd in de **mp_getauth. log** op de beheer punt server).  

### <a name="try-it-out"></a>Probeer het nu!  
Voer de volgende taken uit en gebruik daarna de feedback informatie boven aan dit onderwerp om ons te laten weten hoe ze hebben gewerkt:  

-   Ik kan een primaire site installeren die gebruikmaakt van een database server die is geconfigureerd voor SQL AlwaysOn-beschikbaarheidsgroepen  

-   Ik kon mijn SQL AlwaysOn-beschikbaarheids groep een failover naar een nieuwe replica in de groep en de primaire site is nog actief  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>SQL Server AlwaysOn configureren voor Configuration Manager  
 Gebruik de volgende procedures om eerst de beschikbaarheids groep te maken en te configureren en vervolgens een nieuwe Configuration Manager-site te installeren die gebruikmaakt van de beschikbaarheids groep.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>Een SQL Server AlwaysOn-beschikbaarheids groep maken  
Het proces voor het [maken van een SQL Server beschikbaarheids groep](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-ver15) wordt beschreven in de documentatie bibliotheek van SQL Server.  Wanneer u de beschikbaarheids groep maakt, moet u ervoor zorgen dat aan de volgende vereisten wordt voldaan voor gebruik met Configuration Manager:  

-   Maxi maal drie leden:  

    -   Eén primaire replica en Maxi maal twee secundaire replica's  

    -   Secundaire replica's moeten synchroon zijn.  

        > [!TIP]  
        >  Het is raadzaam dat secundaire replica's zodanig worden geconfigureerd dat ze alleen-lezen zijn. Hierdoor kunt u een secundaire replica gebruiken voor functies zoals rapportage, terwijl de prestaties van de primaire replica voor site bewerkingen behouden blijven.  

-   Ten minste één eind punt. De virtuele naam van dit eind punt wordt gebruikt wanneer u de Configuration Manager-site installeert.  

    > [!TIP]  
    >  Hoewel de groep meerdere eind punten kan bevatten, kan Configuration Manager slechts een van deze te gebruiken.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Een Configuration Manager-site installeren die gebruikmaakt van de beschikbaarheids groep  
Een site installeren die gebruikmaakt van een SQL Server beschikbaarheids groep:  

1.  Vervang het volgende wanneer u hierom wordt gevraagd door Configuration Manager Setup:  

    -   **SQL Server naam**: Voer de virtuele naam in voor het eind punt dat u hebt geconfigureerd bij het maken van de beschikbaarheids groep. De virtuele naam moet een volledige DNS-naam zijn, zoals ** &lt; eindpuntserver \> . fabrikam.com**.  

    -   **Exemplaar**: deze waarde moet leeg blijven. Er is geen exemplaar van deze configuratie.  

    -   **Data Base**: Voer de naam in van de data base die u hebt gemaakt op de primaire replica van de beschikbaarheids groep.  

2.  Vervolgens moet u een netwerk locatie opgeven waarvan elke SQL Server in de groep toegang heeft:  

    -   Voor het computer account en het service account van elke SQL Server is volledige controle toegang tot deze locatie vereist.  

    -   Deze locatie wordt alleen gebruikt tijdens de installatie, en kan worden ontdeeld of verwijderd nadat de installatie is voltooid en de site is geïnstalleerd.  

3.  Nadat u deze informatie hebt verstrekt, voltooit u de installatie met uw normale proces en configuraties.  

##  <a name="service-a--server-cluster"></a><a name="BKMK_ClusterServerUpdates"></a> Een server cluster onderhouden  
U kunt nu een verzameling maken die servers in een cluster bevat en vervolgens de cluster instellingen configureren die moeten worden gebruikt bij het implementeren van updates voor het cluster. U kunt het percentage servers beheren dat op elk gewenst moment online is, evenals voor het configureren van Power shell-scripts voor vóór de implementatie en na de implementatie om aangepaste acties uit te voeren.  

**Bekende problemen voor deze release:**  

-   Rapportage is niet beschikbaar voor het controleren van de status van de implementatie van software-updates voor cluster servers.  

-   De optie onderhouds volgorde op de pagina **cluster instellingen** is uitgeschakeld en niet beschikbaar in deze release.  

### <a name="try-it-out"></a>Probeer het nu!  
Voer de volgende taak uit en gebruik vervolgens de feedback informatie boven aan dit onderwerp om ons te laten weten hoe het werkt:  

-   Ik kan een verzameling maken die een cluster van servers vertegenwoordigt. Voor deze test kunt u de regels voor het verzamelen van lidmaatschap configureren om 2 computers in deze verzameling te hebben.  

-   Ik kan opgeven dat slechts 50% van de servers in het cluster offline kunnen zijn op elk moment in cluster onderhoud. Gebruik de voorbeeld scripts in de procedure om de scripts voor de pre-implementatie en na de implementatie op te geven.  

-   Implementeer een update voor deze verzameling. Controleer de start.txt-en end.txt bestanden in C:\Temp en controleer de begin-en eind tijden voor de implementatie op de servers in het cluster. Raadpleeg het bestand UpdatesDeployment. log voor meer informatie.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Een verzameling voor een server cluster maken  

1.  [Maak een verzameling apparaten](../clients/manage/collections/create-collections.md) die de servers in het cluster bevat.  

2.  Klik in de werk ruimte **activa en naleving** op **apparaten verzamelingen**, klik met de rechter muisknop op de verzameling met de servers in het cluster en klik vervolgens op **Eigenschappen**.  

3.  Selecteer op het tabblad **Algemeen** de optie **alle apparaten zijn onderdeel van hetzelfde server cluster**en klik vervolgens op **instellingen**.  

4.  Selecteer op de pagina **cluster instellingen** het percentage servers dat tegelijkertijd offline kan worden gehaald om software-updates te installeren. Eén cluster server kan mogelijk offline worden gehaald, ongeacht het percentage dat u opgeeft. Configuration Manager wordt afgerond bij het selecteren van het aantal servers dat in één keer wordt verwerkt. Als u bijvoorbeeld 51% kiest en er vier servers in het cluster staan, worden twee servers op hetzelfde moment offline gezet.  

5.  Geef aan of u een script voor het uitvoeren van een voor bereiding (knooppunt afvoer) of na de implementatie (knoop punt voor het hervatten) wilt gebruiken.  

    > [!TIP]  
    >  Hier volgen enkele voor beelden die u kunt gebruiken bij het testen van scripts voor vóór de implementatie en na de implementatie die de huidige tijd naar een tekst bestand schrijven:  
    >   
    >  **Pre-implementatie**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Na de implementatie**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>Software-updates implementeren op het server cluster  

1.  [Software-updates implementeren](../../sum/deploy-use/deploy-software-updates.md) in de server cluster verzameling.  

2.  [Controleer de implementatie van de software-update](../../sum/deploy-use/monitor-software-updates.md).
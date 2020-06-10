---
title: Classificaties en producten synchroniseren
titleSuffix: Configuration Manager
description: Volg deze stappen om software-update classificaties en producten te configureren voor synchronisatie in de Configuration Manager-console.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 4f13ff305ba5fc2b5c5080bafb6fed2412ff8366
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/09/2020
ms.locfileid: "84614083"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>Classificaties en producten configureren voor synchronisatie  

*Van toepassing op: Configuration Manager (huidige vertakking)*

Meta gegevens van software-updates worden tijdens het synchronisatie proces in Configuration Manager opgehaald op basis van de instellingen die u opgeeft in de eigenschappen van de software-update punt component. Nadat u software-updates voor de eerste keer hebt gesynchroniseerd, of wanneer er nieuwe producten en classificaties worden uitgebracht, moet u naar de eigenschappen gaan om de nieuwe items te selecteren. Volg de volgende procedure om classificaties en producten te configureren die moeten worden gesynchroniseerd.  

> [!NOTE]  
> Volg de procedure in deze sectie enkel op de site op het hoogste niveau.  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>Classificaties en producten configureren die moeten worden gesynchroniseerd  

1. Ga in de **Configuration Manager** -console naar **beheer**  >  **site configuratie**  >  **sites**.

2. Selecteer de centrale beheer site of de zelfstandige primaire site.  

3. Klik op het tabblad **Start** in de groep **Instellingen** op **Sitecomponenten configureren** en klik op **Software-updatepunt**.

4. Geef op het tabblad **Classificaties** de software-updateclassificaties waarvoor u software-updates wilt synchroniseren.  

    Elke software-update wordt gedefinieerd met een updateclassificatie die helpt de verschillende types updates te organiseren. Tijdens het synchronisatieproces worden de metagegevens van de software-updates voor de opgegeven classificaties gesynchroniseerd. Configuration Manager biedt de mogelijkheid om software-updates te synchroniseren met de volgende update classificaties:  

     - **Essentiële updates**: Hiermee geeft u een uitgebreide oplossing op voor een specifiek probleem dat een kritieke bug zonder beveiliging verbiedt.  
     - **Definitie-updates**: Hiermee geeft u een uitgebreide en regel matige software-update op die toevoegingen aan de definitie database van een product bevat.  
     - **Feature packs**: Hiermee geeft u de nieuwe product functionaliteit op die voor het eerst wordt gedistribueerd buiten een product release en die doorgaans is opgenomen in de volgende volledige product release.  
     - **Beveiligings updates**: Hiermee geeft u een grote oplossing voor een beveiligings probleem met betrekking tot een specifiek product op.  
     - **Service packs**: Hiermee geeft u een geteste, cumulatieve set van alle hotfixes, beveiligings updates, essentiële updates en updates die worden toegepast op een product. Daarnaast kunnen service packs aanvullende oplossingen bevatten voor problemen die intern worden gevonden sinds de release van het product.  
     - **Hulpprogram ma's**: geeft een hulp programma of onderdeel aan waarmee u een of meer taken kunt volt ooien.  
     - **Update pakketten**: Hiermee geeft u een geteste, cumulatieve set van hotfixes, beveiligings updates, essentiële updates en updates die samen zijn verpakt voor een eenvoudige implementatie. Een update pakket is in het algemeen gericht op een specifiek gebied, zoals een beveiligings-of product onderdeel.  
     - **Updates**: Hiermee geeft u een uitgebreide oplossing voor een specifiek probleem op. Een update is een oplossing voor een niet-kritieke fout die niet aan beveiliging voldoet.  
     - **Upgrade**: Hiermee geeft u een upgrade op voor Windows 10-functies en-functionaliteit. Voor uw software-update punten en-sites moet mini maal WSUS 6,2 met [hotfix 3095113](https://support.microsoft.com/kb/3095113) worden uitgevoerd om de **upgrade** classificatie te verkrijgen. Zie [vereisten voor software-updates](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012)voor meer informatie over het installeren van deze update en andere updates voor **upgrades**.
    
    > [!NOTE]
    > U kunt het selectie vakje **micro soft Surface-Stuur Programma's en firmware-updates** voor het synchroniseren van micro soft Surface-Stuur Programma's selecteren.<!--1098490--> Alle software-update punten moeten Windows Server 2016 of hoger uitvoeren om Surface-Stuur Programma's te synchroniseren. Als u een software-update punt inschakelt op een computer met Windows Server 2012 nadat u Surface drivers hebt ingeschakeld, zijn de scan resultaten voor de stuur programma-updates niet nauw keurig. Dit resulteert in onjuiste compatibiliteits gegevens die worden weer gegeven in de Configuration Manager-console en in Configuration Manager-rapporten. Zie [Surface drivers beheren met Configuration Manager](../deploy-use/surface-drivers.md)voor meer informatie.

5. Geef op het tabblad **Producten** de producten op waarvoor u software-updates wilt synchroniseren, en klik vervolgens op **Sluiten**.  

    - Configuration Manager slaat een lijst van producten en product families op waaruit u kunt kiezen wanneer u het software-update punt voor het eerst installeert. Producten en product families die zijn vrijgegeven nadat Configuration Manager is uitgebracht, zijn mogelijk niet beschikbaar om te selecteren tot u de synchronisatie van software-updates hebt voltooid, waarmee de lijst met beschik bare producten en product families wordt bijgewerkt waaruit u kunt kiezen.  

    - De metagegevens voor elke software-update definiëren de producten waarvoor de update van toepassing is. Een product is een specifieke editie van een besturingssysteem of toepassing, zoals Windows Server 2012. Een productfamilie is het basisbesturingssysteem of de basistoepassing waarvan de afzonderlijke producten zijn afgeleid. Een voorbeeld van een productfamilie is Windows, waarvan Windows Server 2012 een lid is. U kunt een productfamilie of individuele producten binnen een productfamilie opgeven. Hoe meer producten u selecteert, hoe langer het duurt om software-updates te synchroniseren.  

    - Wanneer software-updates van toepassing zijn op meerdere producten, en ten minste een van de producten is geselecteerd voor synchronisatie, worden alle producten weer gegeven in de Configuration Manager-console, zelfs als sommige producten niet zijn geselecteerd. Als Windows Server 2012 bijvoorbeeld het enige besturings systeem is dat u hebt geselecteerd, en als een software-update van toepassing is op Windows 8 en Windows Server 2012, worden beide producten weer gegeven in de Configuration Manager-console.  

    > [!NOTE]  
    > **Windows 10, versie 1903 en hoger** is toegevoegd aan Microsoft Update als een eigen product in plaats van dat ze deel uitmaken van het **Windows 10** -product zoals eerdere versies. Als gevolg van deze wijziging hebt u een aantal hand matige stappen uitgevoerd om ervoor te zorgen dat uw clients deze updates zien. We hebben geholpen het aantal hand matige stappen te verminderen dat u moet ondernemen voor het nieuwe product in Configuration Manager versie 1906. <!--4682946-->
    >
    > Wanneer u bijwerkt naar Configuration Manager versie 1906 en het **Windows 10** -product hebt geselecteerd voor synchronisatie, worden de volgende acties automatisch uitgevoerd:
    > - Het product **Windows 10, versie 1903 en hoger** wordt toegevoegd voor synchronisatie.
    > - [Regels voor automatische implementatie](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) die het **Windows 10** -product bevatten, worden bijgewerkt met **Windows 10 versie 1903 en hoger**.
    > - [Onderhouds plannen](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) worden bijgewerkt met het product **Windows 10, versie 1903 en hoger** .


## <a name="configuring-products-for-versions-of-windows-10"></a>Producten configureren voor versies van Windows 10

### <a name="windows-10-version-1909"></a>Windows 10, versie 1909

Windows 10, versie 1909 deelt een gemeen schappelijk kern besturingssysteem met Windows 10, versie 1903. Beide versies worden onderhouden met dezelfde cumulatieve updates. Zie de blog post [Windows 10, versie 1909 Delivery Options](https://aka.ms/1909mechanics) (Engelstalig) voor meer informatie over Windows 10, versie 1909.

Om ervoor te zorgen dat de Windows 10-versie 1909 en Windows 10, versie 1903-clients updates installeren vanaf Configuration Manager:

- Goed keuring van updates voor de 1909-en 1903-versies van Windows 10.
  - De updates hebben verschillende titels en regels voor toepasselijkheid voor elke versie van het besturings systeem.
  - Het goed keuren van elke update per versie en architectuur van het besturings systeem houdt het normale goedkeurings proces voor beheerders bij.
- De cumulatieve update-installatie bestanden zijn hetzelfde voor de 1909-en 1903-versies van Windows 10.
  - Configuration Manager worden de bron bestanden van de update slechts eenmaal gedownload.

#### <a name="feature-updates-for-windows-10-version-1909"></a>Functie-updates voor Windows 10, versie 1909

Wanneer u functie-updates voor Windows 10, versie 1909, goed keuren, ziet u een aantal verschillende opties:

- Windows 10, versie 1903-clients worden een [activerings pakket](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package)aangeboden, uitgebracht op 12 november 2019.
  - Het activerings pakket is een klein, snel te installeren bestand dat de functies van Windows 10, versie 1909 activeert en het apparaat opnieuw opstart.
  - De vereisten voor het pakket voor activering zijn onder andere:
    - Een minimale cumulatieve update van [KB4517389](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389), uitgebracht op 8 oktober 2019.
    - Een minimale onderhouds stack-update van [KB4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390), uitgebracht op 24 september 2019.
  - Deze update, zoals andere onderdelen update, is niet beschikbaar voor importeren uit `https:\\catalog.update.microsoft.com` .
  - De update wordt automatisch gesynchroniseerd met WSUS als u het product **Windows 10, versie 1903 en hoger** hebt en de classificatie voor de **upgrade** is geselecteerd voor synchronisatie.
  - Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **Windows 10 Servicing**uit en selecteer het knoop punt **alle updates voor Windows 10** . Zoek naar de termen "activering" of "4517245".

    > [!TIP]
    > Omdat deze onderdelen updates zijn, worden ze niet vermeld in het knoop punt **alle software-updates** .

- Windows 10, versie 1809 en eerdere clients worden bijgewerkt met één directe functie-update.
  - Dit is net als alle andere eerdere installaties voor functie-updates die u hebt uitgevoerd voor Windows 10.

> [!NOTE]
> Zowel het pakket voor activering als de traditionele functie-update voor Windows 10, versie 1909 wordt weer gegeven als ' geïnstalleerd ' in Reporting, ongeacht het pad dat is gebruikt om het te installeren.

### <a name="windows-10-version-1903-and-later"></a>Windows 10, versie 1903 en hoger

**Windows 10, versie 1903 en hoger** is toegevoegd aan Microsoft Update als een eigen product in plaats van dat ze deel uitmaken van het **Windows 10** -product zoals eerdere versies. Als gevolg van deze wijziging hebt u een aantal hand matige stappen uitgevoerd om ervoor te zorgen dat uw clients deze updates zien. We hebben geholpen het aantal hand matige stappen te verminderen dat u moet ondernemen voor het nieuwe product in Configuration Manager versie 1906. <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>Windows 10, versie 1903 en hoger met Configuration Manager versie 1906
Wanneer u bijwerkt naar Configuration Manager versie 1906 en het **Windows 10** -product hebt geselecteerd voor synchronisatie, worden de volgende acties automatisch uitgevoerd:
- Het product **Windows 10, versie 1903 en hoger** wordt toegevoegd voor synchronisatie.
- [Regels voor automatische implementatie](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) die het **Windows 10** -product bevatten, worden bijgewerkt met **Windows 10 versie 1903 en hoger**.
- [Onderhouds plannen](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) worden bijgewerkt met het product **Windows 10, versie 1903 en hoger** .

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>Windows 10, versie 1903 en hoger met Configuration Manager versie 1902
Als u Configuration Manager 1902 met Windows 10, versie 1903-clients gebruikt, moet u het volgende doen:
- Selecteer het product **Windows 10, versie 1903 en hoger** voor synchronisatie.
- Alle [regels voor automatische implementatie](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) van Windows 10 versie 1903-clients bijwerken.
- [Onderhouds plannen](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) voor Windows 10, versie 1903-clients bijwerken.

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a>Windows Insider-programma
<!--3556023-->
Vanaf september 2019 kunt u apparaten met Windows Insider preview-builds met Configuration Manager onderhouden en bijwerken. Deze wijziging betekent dat u deze apparaten kunt beheren zonder uw normale processen te wijzigen of Windows Update voor bedrijven in te scha kelen. U kunt functie-updates en cumulatieve updates voor Windows Insider preview-builds downloaden naar Configuration Manager, net als bij elke andere update of upgrade van Windows 10. Zie voor meer informatie het blog bericht release [-updates van Windows 10 publiceren naar WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054) .

Zie [ondersteuning voor Windows 10](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support)voor meer informatie over ondersteuning voor Windows Insider in Configuration Manager.

### <a name="prerequisites"></a>Vereisten

- Configuration Manager versie 1906 of hoger, geconfigureerd voor [Software-update beheer](../plan-design/plan-for-software-updates.md).
- Windows 10-apparaten met [Windows Insider preview-versie](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-get-started).
- Een verzameling die de Windows Insider-apparaten bevat.

### <a name="enable-windows-insider-upgrades-and-updates"></a>Windows Insider-upgrades en-updates inschakelen

U moet de producten en classificaties inschakelen voor Windows Insider-upgrades en-updates. Onderdeel updates, cumulatieve updates en andere updates voor Windows Insider vindt u onder de product categorie **Windows Insider Prerelease** .

1. Ga in de **Configuration Manager** -console naar **beheer**  >  **site configuratie**  >  **sites**.
2. Selecteer de centrale beheer site of de zelfstandige primaire site.  
3. Klik op het tabblad **Start** in de groep **Instellingen** op **Sitecomponenten configureren** en klik op **Software-updatepunt**.
4. Controleer op het tabblad **producten** of de volgende producten zijn geselecteerd voor synchronisatie:
    - Voorlopige versie van Windows Insider
    - Windows 10, versie 1903 en hoger
5. Controleer op het tabblad **classificaties** of de volgende classificaties zijn geselecteerd voor synchronisatie:
    - Uitvoeren
    - Beveiligingsupdates
    - Updates (optioneel)
6. Klik op **OK** om de **Eigenschappen van software-update punt componenten**te sluiten.

### <a name="upgrading-windows-insider-devices"></a>Windows Insider-apparaten bijwerken

Zodra de upgrades voor Windows insiders zijn gesynchroniseerd, kunt u ze zien in **software bibliotheek**  >  **Windows 10 onderhoud**van  >  **alle Windows 10-updates**.

![Updates van Windows insiders-onderdelen voor Windows 10-onderhoud](media/3556023-windows-insiders-pre-release-feature-update.png)

Implementeer functie-updates voor Windows Insider naar uw doel verzameling net als andere upgrades. Houd echter rekening met de volgende punten wanneer u deze onderdelen updates implementeert:

- Deze upgrades zijn van toepassing op alle Windows 10-clients 1903 of eerder, met overeenkomende architectuur, editie en taal.
- Er zijn licentie voorwaarden. uw implementatie moet de voor waarden accepteren om te kunnen installeren.
- U kunt de [thread prioriteit in client instellingen](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority)gebruiken.
- Dynamische update installeert automatisch essentiële updates, met inbegrip van de meest recente cumulatieve update, rechtstreeks vanuit Microsoft Update. Dit gedrag is gestart met functie-updates voor Windows 10 versie 1903. 
  - U kunt [dynamische update expliciet uitschakelen in client instellingen](../../core/clients/deploy/about-client-settings.md#bkmk_du) of met een [setupconfig. ini-bestand](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options). 
  - Zie het blog bericht over [dynamische updates voor Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) voor meer informatie.

Zie [Windows als een service beheren](../../osd/deploy-use/manage-windows-as-a-service.md)voor meer informatie over het implementeren van upgrades.


### <a name="keeping-insider-devices-up-to-date"></a>Insider-apparaten up-to-date houden

Cumulatieve updates voor Windows insider zijn beschikbaar voor WSUS en op uitbrei ding van Configuration Manager. Deze cumulatieve updates worden uitgebracht met een frequentie die overeenkomt met de cumulatieve updates voor Windows 10 versie 1903. De cumulatieve updates voor Windows Insider bevinden zich in de **pre-release** product categorie van Windows Insider en zijn geclassificeerd als **beveiligings updates** of **updates**. U kunt de cumulatieve updates voor Windows Insider implementeren met behulp van uw reguliere software-update proces, zoals het gebruik van [automatische implementatie regels](../deploy-use/automatically-deploy-software-updates.md) of [gefaseerde implementaties](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a>Uitgebreide beveiligings updates en Configuration Manager

Het [ESU-programma (Extended Security updates)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) is een laatste redmiddel-optie voor klanten die bepaalde verouderde micro soft-producten na het einde van de ondersteuning moeten uitvoeren. Het bevat essentiële en/of belang rijke beveiligings updates (zoals gedefinieerd door het [micro soft Security Response Center (MSRC)](https://www.microsoft.com/msrc)) voor een maximum van drie jaar na het einde van de uitgebreide ondersteunings datum van het product.

Producten die niet langer zijn dan hun ondersteunings levenscyclus, worden niet ondersteund voor gebruik met Configuration Manager. Dit omvat alle producten die onder het ESU-programma vallen. Bijvoorbeeld Windows 7. Beveiligings updates die zijn uitgebracht onder het ESU-programma, worden gepubliceerd op Windows Server Update Services (WSUS). Deze updates worden weer gegeven in de Configuration Manager-console. Hoewel producten die onder het programma ESU vallen, niet langer worden ondersteund voor gebruik met Configuration Manager, kan de [meest recente versie van Configuration Manager current branch](../../core/servers/manage/updates.md#version-details) worden gebruikt voor het implementeren en installeren van Windows-beveiligings updates die zijn uitgebracht onder het programma. De nieuwste versie van de release kan ook worden gebruikt om Windows 10 te implementeren op apparaten met Windows 7.

Client beheer functies die geen verband houden met het beheer van software-updates of implementatie van het besturings systeem, worden niet meer getest op de besturings systemen die onder het ESU-programma vallen en wij garanderen niet dat ze blijven functioneren. Het wordt ten zeerste aanbevolen om de huidige versie van de besturings systemen zo snel mogelijk te upgraden of te migreren om client beheer ondersteuning te ontvangen.


## <a name="next-steps"></a>Volgende stappen

Start de synchronisatie van software-updates om software-updates op te halen op basis van de nieuwe criteria. Zie [software-updates synchroniseren](synchronize-software-updates.md)voor meer informatie.

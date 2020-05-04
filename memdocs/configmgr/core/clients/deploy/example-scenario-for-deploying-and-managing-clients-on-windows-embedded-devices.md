---
title: 'Voorbeeld scenario: Windows Embedded-clients implementeren'
titleSuffix: Configuration Manager
description: Bekijk een voorbeeld scenario voor het implementeren en beheren van Configuration Manager-clients op Windows Embedded-apparaten.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e6252a3528e62153e7226ff285d24cd6ecf013
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713329"
---
# <a name="example-scenario-for-deploying-and-managing-configuration-manager-clients-on-windows-embedded-devices"></a>Voorbeeld scenario voor het implementeren en beheren van Configuration Manager-clients op Windows Embedded-apparaten

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit scenario laat zien hoe u Windows Embedded-apparaten met schrijf filter kunt beheren met Configuration Manager. als uw Inge sloten apparaten geen schrijf filters ondersteunen, gedragen ze zich als standaard Configuration Manager-clients en zijn deze procedures niet van toepassing.  

Coho wijn & Winery opent een bezoekers centrum en vereist kiosken met Windows Embedded om interactieve presentaties uit te voeren. Het gebouw voor het nieuwe bezoekers centrum is niet dicht bij de IT-afdeling, dus de kiosken moeten op afstand worden beheerd. Naast de software waarmee de presentaties worden uitgevoerd, moeten deze apparaten bijgewerkte antimalware Protection-software uitvoeren om te voldoen aan het beveiligings beleid van het bedrijf. De kiosken moeten 7 dagen per week worden uitgevoerd, zonder uitval tijd terwijl het bezoekers centrum open is.  

 Coho voert Configuration Manager al uit om apparaten op hun netwerk te beheren. Configuration Manager is geconfigureerd voor het uitvoeren van Endpoint Protection en het installeren van software-updates en-toepassingen. Maar omdat het IT-team nog geen Windows Embedded-apparaten heeft beheerd, voert de Configuration Manager beheerder een pilot uit om twee kiosken te beheren in de receptie lobby.   

 Als u deze Windows Embedded-apparaten wilt beheren waarvoor schrijf filters zijn ingeschakeld, voert Configuration Manager beheerder de volgende stappen uit om de Configuration Manager-client te installeren, de client te beveiligen met behulp van Endpoint Protection en de interactieve presentatie software te installeren.  

1. De Configuration Manager-beheerder (de beheerder) leest hoe Windows Embedded-apparaten schrijf filters gebruiken en hoe Configuration Manager dit eenvoudiger kan maken door de schrijf filters automatisch uit te scha kelen en vervolgens opnieuw in te scha kelen om een software-installatie te behouden.  

    Zie [planning voor client implementatie op Windows Embedded-apparaten](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)voor meer informatie.  

2. Voordat de beheerder de Configuration Manager-client installeert, maakt de beheerder een nieuwe op query's gebaseerde apparaat verzameling voor de Windows Embedded-apparaten. Omdat het bedrijf gebruikmaakt van standaard naamgevings indelingen om hun computers te identificeren, kan de beheerder Windows Embedded-apparaten op unieke wijze identificeren met de eerste zes letters van de computer naam: **WEMDVC**. De beheerder gebruikt de volgende WQL-query om deze verzameling te maken: **selecteer SMS_R_System. netbiosnaam van SMS_R_System waarbij SMS_R_System. NetBIOS-name, zoals "WEMDVC%"**  

    Met deze verzameling kan de beheerder de Windows Embedded-apparaten beheren met verschillende configuratie opties van de andere apparaten. De beheerder gebruikt deze verzameling om het opnieuw opstarten te beheren, Endpoint Protection te implementeren met client instellingen en de interactieve presentatie toepassing te implementeren.  

    Zie [verzamelingen maken](../../../core/clients/manage/collections/create-collections.md).  

3. De beheerder configureert de verzameling voor een onderhouds venster om er zeker van te zijn dat opnieuw opstarten nodig is voor het installeren van de presentatie toepassing en eventuele upgrades worden niet uitgevoerd tijdens openings tijden voor het bezoekers centrum. De openingstijden zijn van 09:00 tot 18:00 uur, maandag tot zondag. De beheerder configureert het onderhouds venster voor elke dag, 18:30 tot en met 06:00.  

4. Zie [onderhouds Vensters gebruiken](../../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie.  

5. De beheerder configureert vervolgens een aangepaste apparaatclient voor het installeren van de Endpoint Protection-client door **Ja** te selecteren voor de volgende instellingen en implementeert vervolgens deze aangepaste client instelling voor de Windows Embedded-apparaat-verzameling:  

   - **Endpoint Protection-client op clientcomputers installeren**  

   - **Voor Windows Embedded-apparaten met schrijffilters voert u de installatie van de Endpoint Protection-client door (computer moet opnieuw worden opgestart)**  

   - **Installatie van Endpoint Protection-client en herstart buiten onderhoudsvensters toestaan**  

     Wanneer de Configuration Manager-client is geïnstalleerd, installeren deze instellingen de Endpoint Protection-client en zorgt u ervoor dat deze persistent wordt gemaakt in het besturings systeem als onderdeel van de installatie, in plaats van alleen naar de overlay te schrijven. Het beveiligings beleid van het bedrijf vereist dat de antimalware-software altijd wordt geïnstalleerd en dat de beheerder niet in staat is het risico uit te voeren van de kiosken die niet worden beveiligd gedurende een korte periode als ze opnieuw worden gestart.  

   > [!NOTE]  
   >  Het opstarten dat nodig is voor de installatie van de Endpoint Protection-client gebeurt eenmaal, en wel tijdens de installatieperiode voor de apparaten en voordat het bezoekerscentrum in bedrijf gaat. In tegens telling tot de periodieke implementatie van toepassingen of updates van software definities, is de volgende keer dat de Endpoint Protection-client wordt geïnstalleerd op hetzelfde apparaat waarschijnlijk wanneer het bedrijf een upgrade uitvoert naar de volgende versie van Configuration Manager.  

    Zie [Endpoint Protection configureren](../../../protect/deploy-use/endpoint-protection-configure.md)voor meer informatie.  

6. Omdat de configuratie-instellingen voor de client nu zijn geïmplementeerd, wordt de beheerder voor bereid om de Configuration Manager-clients te installeren. Voordat de beheerder de clients kan installeren, moeten ze het schrijf filter hand matig uitschakelen op de Windows Embedded-apparaten. De beheerder leest de OEM-documentatie bij de kiosken en volgt de instructies om de schrijf filters uit te scha kelen.  

    De beheerder wijzigt de naam van het apparaat, zodat het gebruikmaakt van de standaard naamgevings indeling van het bedrijf en installeert de client hand matig door CCMSetup uit te voeren met de volgende opdracht vanaf een toegewezen station met de client bron bestanden: **CCMSetup. exe/MP: mpserver. cohovineyardandwinery. com SMSSITECODE = co1**  

    Met deze opdracht wordt de client geïnstalleerd en toegewezen aan het beheerpunt dat het intranet FQDN bevat van **mpserver.cohovineyardandwinery.com**en wordt de client toegewezen aan de primaire site die **CO1**wordt genoemd.  

    De beheerder weet dat het altijd even duurt voordat clients zijn geïnstalleerd en hun status naar de site sturen. De beheerder wacht dus voordat ze bevestigt dat de clients zijn geïnstalleerd, toewijzen aan de site en als clients worden weer gegeven in de verzameling die ze hebben gemaakt voor Windows Embedded-apparaten.  

    Als aanvullende bevestiging controleert de beheerder de eigenschappen van Configuration Manager in het configuratie scherm op de apparaten en vergelijkt deze met de standaard Windows-computers die worden beheerd door de site. Op het tabblad **Onderdelen** wordt bij de **Agent voor hardware-inventarisatie****Ingeschakeld**weergegeven en op het tabblad **Acties** zijn 11 acties beschikbaar, waaronder **Evaluatiecyclus voor installatie van toepassingen** en **Verzamelfase zoekgegevens**.  

    Als u zeker weet dat de clients zijn geïnstalleerd, toegewezen en ontvangen van het beheer punt, schakelt de beheerder vervolgens hand matig de schrijf filters in door de instructies van de OEM te volgen.  

    Zie voor meer informatie:  

   -   [Clients implementeren op Windows-computers](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [Clients toewijzen aan een site](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. Nu de Configuration Manager-client is geïnstalleerd op de Windows Embedded-apparaten, bevestigt de beheerder dat deze op dezelfde manier kan worden beheerd als de standaard Windows-clients. De beheerder kan bijvoorbeeld vanuit de Configuration Manager-console deze op afstand beheren met behulp van extern beheer, client beleid voor hen initiëren en client eigenschappen en hardware-inventaris weer geven.  

    Omdat deze apparaten zijn gekoppeld aan een Active Directory domein, hoeft de beheerder ze niet hand matig goed te keuren als vertrouwde clients en bevestigt de Configuration Manager-console dat ze zijn goedgekeurd.  

    Zie [clients beheren](../../../core/clients/manage/manage-clients.md)voor meer informatie.  

8. De beheerder voert de **wizard software implementeren** uit en configureert een vereiste toepassing om de interactieve presentatie software te installeren. Op de pagina **gebruikers ervaring** van de wizard, in de sectie **verwerking van schrijf filters voor Windows Embedded-apparaten** , wordt de standaard optie voor het selecteren van **wijzigingen door voeren bij deadline of tijdens een onderhouds venster geaccepteerd (opnieuw opstarten nood zakelijk)**.  

    De beheerder houdt deze standaard optie voor schrijf filters in om ervoor te zorgen dat de toepassing wordt bewaard nadat de computer opnieuw is opgestart, zodat deze altijd beschikbaar is voor de bezoekers die de kiosken gebruiken. Het dagelijkse onderhoudsvenster biedt een opslagperiode waarin het opstarten voor installaties en updates kan plaatsvinden.  

    De-beheerder implementeert de toepassing op de verzameling met Windows Embedded-apparaten.  

    Zie [toepassingen implementeren met Configuration Manager](../../../apps/deploy-use/deploy-applications.md)voor meer informatie.  

9. Voor het configureren van definitie-updates voor Endpoint Protection, gebruikt de beheerder software-updates en voert de wizard regel voor automatische implementatie maken uit. Ze selecteren de sjabloon **definitie-updates** om de wizard vooraf in te vullen met instellingen die geschikt zijn voor Endpoint Protection.  

     Dit zijn onder andere de volgende instellingen op de pagina **Gebruikerservaring** :  

   - **Deadlinegedrag**: het selectievakje **Software-installatie** wordt niet geselecteerd.  

   - **Verwerking van schrijffilters voor Windows Embedded-apparaten**: het selectievakje **Wijzigingen doorvoeren bij deadline of tijdens onderhoud (opnieuw opstarten noodzakelijk)** wordt niet geselecteerd.  

     De beheerder houdt deze standaard instellingen bij. Met deze twee opties en deze configuratie kunnen alle software-updatedefinities voor Endpoint Protection overdag worden geïnstalleerd in de overlay en hoeven de installatie en het doorvoeren ervan niet te worden uitgesteld voor tijdens het onderhoudsvenster. Deze configuratie komt het beste overeen met het beveiligingsbeleid van het bedrijf voor computers om bijgewerkte antimalware te gebruiken.  

     > [!NOTE]  
     >  In tegenstelling tot software-installaties voor toepassingen kunnen software-updatedefinities voor Endpoint Protection heel vaak gebeuren, zelfs meerdere keren per dag. Het gaat vaak om kleine bestanden. Voor dit soort beveiligingsimplementaties kan het vaak nuttig zijn altijd naar de overlay te installeren in plaats van te wachten op het onderhoudsvenster. De Configuration Manager-client installeert de software-definitie updates snel opnieuw als het apparaat opnieuw wordt opgestart, omdat met deze actie een evaluatie controle wordt gestart en er niet wordt gewacht tot de volgende geplande evaluatie wordt uitgevoerd.  

     De beheerder selecteert de verzameling met Windows Embedded-apparaten voor de regel voor automatische implementatie.  

     Zie voor meer informatie  
               Stap 3: Configuration Manager software-updates configureren voor het leveren van definitie-updates aan client computers bij het [configureren van Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)  

10. De beheerder besluit een onderhouds taak te configureren die regel matig alle wijzigingen doorvoert op de overlay. Deze taak is de ondersteuning van de implementatie van software-updatedefinities om het aantal updates te verminderen dat toeneemt en iedere keer wanneer het apparaat opnieuw wordt gestart opnieuw geïnstalleerd moet worden. In de ervaring van de beheerder kunnen de antimalware-Program ma's efficiënter worden uitgevoerd.  

    > [!NOTE]  
    >  Deze software-updatedefinities zouden automatisch worden doorgevoerd naar de installatiekopie als de ingesloten apparaten een andere beheertaak uitvoerden voor het doorvoeren van de wijzigingen. Door de installatie van een nieuwe versie van de interactieve presentatiesoftware zouden bijvoorbeeld ook de wijzigingen voor software-updatedefinities worden doorgevoerd. Of door de installatie van standaardsoftware-updates iedere maand tijdens het onderhoudsvenster zouden ook de wijzigingen voor software-updatedefinities worden doorgevoerd. In dit scenario, waarin standaardsoftware-updates niet worden uitgevoerd en de interactieve presentatiesoftware naar alle waarschijnlijkheid niet vaak wordt bijgewerkt, kan het maanden duren voordat de software-definitieupdates automatisch worden doorgevoerd naar de installatiekopie.  

     De beheerder maakt eerst een aangepaste taken reeks zonder andere instellingen dan de naam. Ze voeren de wizard taken reeks maken uit:  

    1. Op de pagina **nieuwe taken reeks maken** selecteert de beheerder **een nieuwe aangepaste taken reeks maken**en klikt vervolgens op **volgende**.  

    2. Op de pagina **taken reeks informatie** voert de beheerder **onderhouds taak in om wijzigingen op Inge sloten apparaten door te voeren** voor de naam van de taken reeks en klikt vervolgens op **volgende**.  

    3. Op de pagina **samen vatting** selecteert de beheerder **volgende**en voltooit de wizard.  

       De beheerder implementeert vervolgens deze aangepaste taken reeks voor de verzameling met Windows Embedded-apparaten en configureert het schema om elke maand te worden uitgevoerd. Als onderdeel van de implementatie-instellingen selecteren ze het selectie vakje **wijzigingen door voeren bij deadline of tijdens een onderhouds venster (opnieuw opstarten nood zakelijk)** om de wijzigingen na het opnieuw opstarten te behouden. Als u deze implementatie wilt configureren, selecteert de beheerder de aangepaste taken reeks die ze zojuist hebben gemaakt en klik vervolgens op het tabblad **Start** in de groep **implementatie** op **implementeren** om de wizard software implementeren te starten:  

    4. Op de pagina **Algemeen** selecteert de beheerder de verzameling met Windows Embedded-apparaten en klikt vervolgens op **volgende**.  

    5. Op de pagina **implementatie-instellingen** selecteert de beheerder het **doel** **vereist**en klikt vervolgens op **volgende**.  

    6. Op de pagina **planning** klikt de beheerder op **Nieuw** om een wekelijks schema op te geven tijdens het onderhouds venster en klikt vervolgens op **volgende**.  

    7. De beheerder voltooit de wizard zonder verdere wijzigingen.  

       Zie voor meer informatie  
                 [Taak reeksen beheren om taken te automatiseren](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. De beheerder schrijft een script om de apparaten te configureren voor de volgende instellingen om de kiosken automatisch uit te voeren:  

    - Automatisch aanmelden met behulp van een gastaccount zonder wachtwoord.  

    - Voer de interactieve presentatiesoftware automatisch uit bij het opstarten.  

      De beheerder gebruikt pakketten en Program ma's om dit script te implementeren in de verzameling met Windows Embedded-apparaten. Wanneer de beheerder de wizard software implementeren uitvoert, worden ze opnieuw het selectie vakje **wijzigingen door voeren bij deadline of tijdens onderhoud (opnieuw opstarten nood zakelijk)** geselecteerd om de wijzigingen na het opnieuw opstarten te behouden.  

      Zie [pakketten en Program ma's](../../../apps/deploy-use/packages-and-programs.md)voor meer informatie.  

12. De volgende ochtend controleert de beheerder de Windows Embedded-apparaten. Ze bevestigen het volgende:  

    - De kiosk wordt automatisch aangemeld met de gastaccount.  

    - De interactieve presentatiesoftware wordt uitgevoerd.  

    - De Endpoint Protection-client wordt geïnstalleerd en heeft de laatste software-update.  

    - Dat het apparaat opnieuw opstartte tijdens het onderhoudsvenster.  

      Zie voor meer informatie:  

    - [Endpoint Protection controleren](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [Toepassingen bewaken met Configuration Manager](../../../apps/deploy-use/monitor-applications-from-the-console.md)  

13. De beheerder bewaakt de kiosken en rapporteert het geslaagde beheer voor hun manager. Als gevolg hiervan worden 20 kiosken besteld voor het bezoekerscentrum.  

     Om te voor komen dat de Configuration Manager-client hand matig wordt geïnstalleerd, zodat de schrijf filters hand matig moeten worden uitgeschakeld en ingeschakeld, zorgt de beheerder ervoor dat de order een aangepaste installatie kopie bevat die al de installatie-en site toewijzing van de Configuration Manager client bevat. Bovendien krijgen de apparaten een naam volgens het naamformaat van het bedrijf.  

     De kiosken worden geleverd aan het bezoekerscentrum een week voor het opent. Gedurende die tijd zijn de kiosken verbonden met het netwerk, alle apparaatbeheer ervoor is automatisch en er is geen lokale beheerder vereist. De beheerder bevestigt dat de kiosken werken zoals vereist:  

    -   De clients op de kiosken vervolledigen sitetoewijzing en downloaden de vertrouwde basissleutel van Active Directory Domain Services.  

    -   De clients op de kiosken worden automatisch toegevoegd aan de in Windows ingesloten apparaatverzameling en geconfigureerd met het onderhoudsvenster.  

    -   De Endpoint Protection-client wordt geïnstalleerd en heeft de laatste software-update definities voor antimalware bescherming.  

    -   De interactieve presentatiesoftware is geïnstalleerd en draait automatisch, klaar voor gebruikers.  

14. Na de initiële installatie, kan opnieuw opstarten, wat vereist kan zijn voor updates, alleen gebeuren als het bezoekerscentrum gesloten is;  

---
title: Schema-uitbreidingen
titleSuffix: Configuration Manager
description: Breid het Active Directory schema uit ter ondersteuning van Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ace560130e43fd5675b51b6d507e84043c01407
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904075"
---
# <a name="schema-extensions-for-configuration-manager"></a>Schema-uitbreidingen voor System Center Configuration

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt het Active Directory schema uitbreiden ter ondersteuning van Configuration Manager. Hiermee bewerkt u het Active Directory schema van een forest om een nieuwe container en verschillende kenmerken toe te voegen die Configuration Manager sites gebruiken om belang rijke informatie te publiceren in Active Directory waar clients deze veilig kunnen gebruiken. Deze informatie kan de implementatie en configuratie van clients vereenvoudigen en clients helpt bij het vinden van site resources, zoals servers met geïmplementeerde inhoud of die verschillende services bieden aan clients.  

-   Het is een goed idee om het Active Directory schema uit te breiden, maar dit is niet vereist.  

Voordat u het [Active Directory-schema uitbreidt](https://docs.microsoft.com/sccm/core/plan-design/network/extend-the-active-directory-schema), dient u bekend te zijn met Active Directory Domain Services en te weten hoe u [het Active Directory-schema wijzigt](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10)).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Overwegingen voor uitbrei ding van het Active Directory schema voor Configuration Manager  

-   De Active Directory schema-uitbrei dingen voor Configuration Manager zijn niet gewijzigd ten opzichte van die Configuration Manager 2007 en Configuration Manager 2012. Als u het schema al eens hebt uitgebreid voor een van de versies, hoeft u het schema niet nogmaals uit te breiden.  

-   Uitbrei ding van het schema is een eenmalige, onomkeerbare actie in het hele forest.  

-   Alleen een gebruiker die lid is van de groep Schema-administrators of aan wie voldoende machtigingen zijn gedelegeerd om het schema te wijzigen, kan het schema uitbreiden.  

-   Hoewel u het schema kunt uitbreiden voor-of nadat u Configuration Manager Setup hebt uitgevoerd, is het een goed idee om het schema uit te breiden voordat u begint met het configureren van uw sites en hiërarchie-instellingen. Zodoende kunt u veel van de latere configuratiestappen vereenvoudigen.  

-   Nadat u het schema hebt uitgebreid, wordt de Active Directory globale catalogus gerepliceerd in het hele forest. Plan daarom om het schema uit te breiden wanneer het replicatie verkeer geen nadelige invloed heeft op andere processen die afhankelijk zijn van het netwerk:  

    -   In Windows 2000-forests is het uitbreiden van het schema een volledige synchronisatie van de hele globale catalogus.  

    -   Vanaf Windows 2003-forests worden alleen de nieuw toegevoegde kenmerken gerepliceerd.  

**Apparaten en clients die het Active Directory-schema niet gebruiken:**  

-   Mobiele apparaten die worden beheerd door de Exchange Server-connector  

-   De client voor Mac-computers  

-   De client voor Linux- en UNIX-servers  

-   Mobiele apparaten die zijn Inge schreven door Configuration Manager  

-   Mobiele apparaten die zijn Inge schreven door Microsoft Intune  

-   Verouderde clients van mobiele apparaten  

-   Windows-clients die zijn geconfigureerd voor client beheer op Internet  

-   Windows-clients die door Configuration Manager op internet worden gedetecteerd  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Mogelijkheden die profiteren van de uitbreiding van het schema  
**Installatie van client computer en site toewijzing** : wanneer op een Windows-computer een nieuwe client wordt geïnstalleerd, zoekt de client Active Directory Domain Services naar installatie-eigenschappen.  

-   **Tijdelijke oplossingen:** Als u het schema niet uitbreidt, gebruikt u een van de volgende opties om configuratie details op te geven die op computers moeten worden geïnstalleerd:  

    -   **Gebruik client-pushinstallatie**. Voordat u een client installatie methode gebruikt, moet u ervoor zorgen dat aan alle vereisten wordt voldaan. Zie de sectie installatie methode-afhankelijkheden in [vereisten voor het implementeren van clients op Windows-computers](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)voor meer informatie.  

    -   **Installeer clients hand matig** en geef eigenschappen voor de client installatie op met behulp van de opdracht regel eigenschappen van CCMSetup-installatie. Dit moet het volgende omvatten:  

        -   Geef een beheer punt of bronpad op van waaruit de computer de installatie bestanden kan downloaden met behulp van de CCMSetup-eigenschap **/MP: = &lt; naam van \> het beheer punt computer naam** of **/Source: &lt; pad naar client bron bestanden \> ** op de CCMSetup-opdracht regel tijdens client installatie.  

        -   Geef een lijst met eerste beheer punten op die de client moet gebruiken, zodat deze aan de site kan worden toegewezen en down load vervolgens client beleid en site-instellingen. Gebruik hiervoor de Client.msi- eigenschap SMSMP van CCMSetup.  

    -   **Publiceer het beheerpunt in DNS of WINS** en configureer clients voor het gebruik van deze servicelocatiemethode.  

**Poort configuratie voor communicatie van client naar server** : wanneer een client wordt geïnstalleerd, wordt deze geconfigureerd met poort informatie die is opgeslagen in Active Directory. Als u later de communicatie poort van de client naar de server wijzigt voor een site, kan een client deze nieuwe poort instelling verkrijgen van Active Directory Domain Services.  

-   **Tijdelijke oplossingen:** als u het schema niet uitbreidt, dient u een van de volgende tijdelijke oplossingen te gebruiken om deze nieuwe poortconfiguratie voor bestaande clients:  

    -   **Clients opnieuw installeren** met behulp van de opties voor het configureren van de nieuwe poort.  

    -   **Implementeer op clients een aangepast script om de poortinformatie bij te werken**. Als clients niet met een site kunnen communiceren vanwege een poort wijziging, kunt u Configuration Manager niet gebruiken om dit script te implementeren. U kunt bijvoorbeeld een groepsbeleid gebruiken.  

**Scenario's voor inhouds implementatie** : wanneer u inhoud op de ene site maakt en die inhoud vervolgens op een andere site in de hiërarchie implementeert, moet de ontvangende site de hand tekening van de ondertekende inhouds gegevens kunnen verifiëren. Hiervoor is toegang vereist tot de openbare sleutel van de bronsite waar u deze gegevens maakt. Wanneer u het Active Directory schema voor Configuration Manager uitbreidt, is de open bare sleutel van een site beschikbaar voor alle sites in de hiërarchie.  

-   **Tijdelijke oplossing:** als u het schema niet uitbreidt, kunt u het hulpprogramma voor hiërarchie-onderhoud, **preinst.exe**, gebruiken om informatie over de beveiligingssleutel uit te wisselen tussen sites.  

     Als u bijvoorbeeld van plan bent om inhoud te maken op een primaire site en die inhoud op een secundaire site onder een andere primaire site te implementeren, moet u het Active Directory-schema uitbreiden zodat de secundaire site de open bare sleutel van de primaire bron site kan ophalen, of u kunt preinst. exe gebruiken om sleutels rechtstreeks te delen tussen de twee sites.  

## <a name="active-directory-attributes-and-classes"></a>Kenmerken en klassen Active Directory  
Wanneer u het schema voor Configuration Manager uitbreidt, worden de volgende klassen en kenmerken toegevoegd aan het schema en zijn deze beschikbaar voor alle Configuration Manager-sites in dat Active Directory forest.  

-   Kenmerken:  

    -   CN = mS-SMS-toewijzing-site-code  

    -   CN = mS-SMS-mogelijkheden  

    -   CN = MS-SMS-default-MP  

    -   CN = mS-SMS-Device-Management-Point  

    -   CN = mS-SMS-Health-status  

    -   CN = MS-SMS-MP-Address  

    -   CN = MS-SMS-MP-name  

    -   CN = MS-SMS-bereikd-IP-hoog  

    -   CN = MS-SMS-bereik-IP-laag  

    -   CN = MS-SMS-roaming-Boundary's  
        op  

    -   CN = MS-SMS-site-Boundary's  

    -   CN = MS-SMS-site-code  

    -   CN = mS-SMS-source-forest  

    -   CN = mS-SMS-version  

-   Klassen:  

    -   CN = MS-SMS-beheer punt  

    -   CN = MS-SMS-roaming-boundary-bereik  

    -   CN = MS-SMS-server-Locator-Point  

    -   CN = MS-SMS-site  

> [!NOTE]
> 
>  De schema-uitbrei dingen kunnen kenmerken en klassen bevatten die worden getransporteerd uit eerdere versies van het product, maar die niet door Configuration Manager worden gebruikt. Bijvoorbeeld:  
> 
> 
> - Kenmerk: CN = MS-SMS-site-Boundary's  
>   -   Klasse: CN = MS-SMS-server-Locator-Point  

U kunt controleren of de voor gaande lijsten actueel zijn door de ConfigMgr_ad_schema weer te geven **. LDF** -bestanden uit de map **\SMSSETUP\BIN\x64** van de installatie media van Configuration Manager.  

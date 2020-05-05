---
title: Publiceren en het Active Directory schema
titleSuffix: Configuration Manager
description: Breid het Active Directory-schema uit voor Configuration Manager om het proces van het implementeren en configureren van clients te vereenvoudigen.
ms.date: 09/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3595273d55bf01158691fb46587ac264af16bffa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718761"
---
# <a name="prepare-active-directory-for-site-publishing"></a>Active Directory voorbereiden op site publicatie

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u het Active Directory schema voor Configuration Manager uitbreidt, worden er nieuwe structuren geïntroduceerd in Active Directory die door Configuration Manager-sites worden gebruikt om belang rijke informatie te publiceren op een veilige locatie waar clients deze eenvoudig kunnen openen.  

Het is een goed idee om Configuration Manager te gebruiken met een uitgebreid Active Directory schema wanneer u on-premises clients beheert. Een uitgebreid schema kan het implementeren en configureren van clients vereenvoudigen. Met een uitgebreid schema kunnen clients efficiënt resources vinden, zoals inhouds servers en aanvullende services die de verschillende Configuration Manager site systeem rollen bieden.  

-   Als u niet bekend bent met welk uitgebreid schema voorziet in een Configuration Manager-implementatie, kunt u meer lezen over [schema-uitbrei dingen voor Configuration Manager](../../../core/plan-design/network/schema-extensions.md) om u te helpen deze beslissing te nemen.  

-   Wanneer u geen uitgebreid schema gebruikt, kunt u andere methoden configureren, zoals DNS en WINS, om services en site systeem servers te zoeken. Voor deze methoden van servicelocatie zijn aanvullende configuraties vereist en de methoden hebben niet de voorkeur bij servicelocatie door clients. Meer informatie vindt u in [begrijpen hoe clients site resources en-services vinden voor Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md),  

-   Als uw Active Directory-schema is uitgebreid voor Configuration Manager 2007 of System Center 2012 Configuration Manager, hoeft u niet meer te doen. De schema-uitbrei dingen blijven ongewijzigd en zijn al aanwezig.  

Het uitbreiden van het schema is een eenmalige actie voor een forest. Voer de volgende stappen uit om uit te breiden en vervolgens het uitgebreide Active Directory schema te gebruiken:  

## <a name="step-1-extend-the-schema"></a>Stap 1. Het schema uitbreiden  
Als u het schema voor Configuration Manager wilt uitbreiden, doet u het volgende:  

-   Gebruik een account dat lid is van de beveiligings groep Schema-administrators.  

-   Zijn aangemeld bij de schema master domein controller.  

-   Voer het hulp programma **Extadsch. exe** uit of gebruik het opdracht regel hulpprogramma ldifde met het bestand **ConfigMgr_ad_schema. ldf** . Het hulp programma en het bestand bevinden zich in de map **SMSSETUP\BIN\X64** op de Configuration Manager-installatie media.  

#### <a name="option-a-use-extadschexe"></a>Optie A: gebruik Extadsch.exe  

1.  Voer **extadsch.exe** uit om nieuwe klassen en kenmerken aan het Active Directory-schema toe te voegen.  

    > [!TIP]  
    >  Voer dit hulpprogramma uit vanaf een opdrachtregel om feedback weer te geven terwijl het programma wordt uitgevoerd.  

2.  Controleer of de schema-uitbrei ding is geslaagd door extadsch. log te controleren in de hoofdmap van het systeem station.  

#### <a name="option-b-use-the-ldif-file"></a>Optie B: gebruik het LDIF-bestand  

1.  Bewerk het **ldf** -bestand van ConfigMgr_ad_schema om het Active Directory hoofd domein te definiëren dat u wilt uitbreiden:  

    -   Vervang alle instanties van de tekst, **DC = x**, in het bestand met de volledige naam van het domein dat u wilt uitbreiden.  

    -   Als de volledige naam van het domein dat moet worden uitgebreid bijvoorbeeld widgets.microsoft.com heet, wijzigt u alle instanties van DC = x in het bestand in **DC = widgets, DC = micro soft, DC = com**.  

2.  Gebruik het opdracht regel hulpprogramma LDIFDE om de inhoud van het bestand **ConfigMgr_ad_schema. ldf** te importeren in Active Directory Domain Services:  

    -   Met de volgende opdracht regel worden bijvoorbeeld de schema-uitbrei dingen geïmporteerd in Active Directory Domain Services, wordt uitgebreide logboek registratie ingeschakeld en wordt een logboek bestand gemaakt tijdens het import proces: **ldifde-i-f ConfigMgr_ad_schema. ldf- &lt;v-j-locatie\>voor het opslaan van het logboek bestand**.  

3.  Controleer of de schema-uitbrei ding is geslaagd door een logboek bestand te bekijken dat is gemaakt door de opdracht regel die in de vorige stap is gebruikt.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Stap 2.  De container Systeembeheer maken en sites machtigingen aan de container toekennen  
 Nadat u het schema hebt uitgebreid, moet u een container met de naam **System Management** in Active Directory Domain Services (AD DS) maken:  

-   U maakt deze container één keer in elk domein met een primaire of secundaire site waarmee gegevens naar Active Directory worden gepubliceerd.  

-   Voor elke container wijst u machtigingen toe aan het computer account van elke primaire en secundaire site server waarmee gegevens naar dat domein worden gepubliceerd. Elk account moet **volledig beheer** hebben over de container met de geavanceerde machtiging, **Toep assen op**, gelijk aan **Dit object en alle onderliggende objecten**.  

#### <a name="to-add-the-container"></a>De container toevoegen  

1.  Gebruik een account dat beschikt over de machtiging **Alle onderliggende objecten maken** in de container **Systeem** in Active Directory Domain Services.  

2.  Voer **ADSI Edit** (adsiedit. msc) uit en maak verbinding met het domein van de site server.  

3.  Maak de container:  

    -   Vouw **domein** &lt;computer Fully Qualified Domain name\>uit, &lt;vouw DN\>-naam uit, klik met de rechter muisknop op **CN = systeem**, kies **Nieuw**en kies vervolgens **object**.  

    -   Kies in het dialoog venster **object maken** de optie **container**en klik vervolgens op **volgende**.  

    -   Voer **systeem beheer**in het vak **waarde** in en kies **volgende**.  

4.  Wijs machtigingen toe:  

    > [!NOTE]  
    >  U kunt desgewenst ook andere hulpprogram ma's zoals Active Directory het beheer programma gebruikers en computers (DSA. msc) gebruiken om machtigingen toe te voegen aan de container.  

    -   Klik met de rechter muisknop op **CN = systeem beheer**en kies **Eigenschappen**.  

    -   Kies het tabblad **beveiliging** , klik op **toevoegen**en voeg vervolgens het computer account van de site server toe met de machtiging **volledig beheer** .  

    -   Kies **Geavanceerd**, kies het computer account van de site server en klik vervolgens op **bewerken**.  

    -   Kies in de lijst **Toep assen op** **Dit object en alle onderliggende objecten**.  

5.  Kies **OK** om de console te sluiten en de configuratie op te slaan.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Stap 3. Sites instellen om naar Active Directory Domain Services te publiceren  
 Nadat de container is ingesteld, worden er machtigingen verleend en hebt u een Configuration Manager primaire site geïnstalleerd. u kunt deze site instellen om gegevens te publiceren naar Active Directory.  

 Zie [site gegevens publiceren voor Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md)voor meer informatie over publiceren.  

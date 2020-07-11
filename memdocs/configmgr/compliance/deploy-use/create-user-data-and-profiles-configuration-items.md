---
title: Configuratie-items voor gebruikersgegevens en -profielen maken
titleSuffix: Configuration Manager
description: Configuratie-items voor gegevens en profielen gebruiken in Configuration Manager voor het beheren van Mapomleiding, offline bestanden en zwervende profielen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 51c97ae3cd947e0bdfa82c595cb6446351412d21
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240368"
---
# <a name="create-user-data-and-profiles-configuration-items-in-configuration-manager"></a>Configuratie-items voor gebruikers gegevens en-profielen maken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuratie-items voor gebruikers gegevens en-profielen in Configuration Manager bevatten instellingen waarmee Mapomleiding, offline bestanden en zwervende profielen kunnen worden beheerd op computers met Windows 8 en hoger voor gebruikers in uw hiërarchie. U kunt bijvoorbeeld:  

- De map documenten van een gebruiker omleiden naar een netwerk share.  

- Zorg ervoor dat opgegeven bestanden op het netwerk beschikbaar zijn op de computer van een gebruiker wanneer de netwerk verbinding niet beschikbaar is.  

- Configureer welke bestanden in het zwervende profiel van een gebruiker worden gesynchroniseerd met een netwerk share wanneer de gebruiker zich aan-of afmeldt.  

  In tegens telling tot andere configuratie-items in Configuration Manager voegt u geen configuratie-items voor gebruikers gegevens en-profielen toe aan een configuratie basislijn die u vervolgens implementeert. In plaats daarvan implementeert u het configuratie-item rechtstreeks via het dialoogvenster **Configuratie-item voor gebruikersgegevens en -profielen implementeren** .  

> [!IMPORTANT]  
>  U kunt alleen configuratie-items voor gebruikersgegevens en -profielen implementeren naar gebruikersverzamelingen.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Gebruikersgegevens en -profielen inschakelen voor instellingen voor naleving  
 Gebruik de volgende procedure om de standaardclientinstelling te configureren voor de instellingen voor de naleving van gebruikersgegevens en -profielen en die van toepassing zijn op alle computers in uw hiërarchie. Als u deze instellingen alleen wilt toepassen op bepaalde computers, maakt u een aangepaste apparaatclientinstelling en wijst u deze toe aan een verzameling waartoe de computers behoren waarvoor u de instellingen voor de naleving van de gebruikersgegeven en -profielen wilt gebruiken. Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor meer informatie over het maken van aangepaste apparaatinstellingen.  

1.  Klik in de Configuration Manager-console **Administration**op standaard instellingen voor de beheer  >  **client instellingen**  >  **Default Settings**.  

4.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

5.  Klik in het dialoogvenster **Standaardinstellingen** op **Instellingen voor naleving**.  

6.  Selecteer in de vervolgkeuzelijst **Gebruikersgegevens en -profielen inschakelen** de optie **Ja**.  

7.  Klik op **OK** om het dialoogvenster **Standaardinstellingen** te sluiten.  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Een configuratie-item voor gebruikers gegevens en-profielen maken  

1. Klik in de Configuration Manager-console op **activa en**nalevings  >  **instellingen voor naleving**  >  **gebruikers gegevens en-profielen**.  

2. Op het tabblad **Start** in de groep **Maken** klikt u op **Configuratie-item voor gebruikersgegevens en -profielen maken**.  

3. Geef op de pagina **Algemeen** van de wizard **Configuratie-item voor gebruikersgegevens en -profielen maken**de volgende informatie op:  

   -   **Naam** : voer een unieke naam in voor het configuratie-item. U kunt maximaal 256 tekens gebruiken.  

   -   **Beschrijving:** Geef een beschrijving op die een overzicht geeft van het configuratie-item en andere relevante informatie waarmee het kan worden geïdentificeerd in de Configuration Manager-console. U kunt maximaal 256 tekens gebruiken.  

   -   **Mapomleiding:** schakel dit selectievakje in als u instellingen wilt configureren voor Mapomleiding voor dit configuratie-item.  

   -   **Offlinebestanden:** schakel dit selectievakje in als u instellingen wilt configureren voor offlinebestanden voor dit configuratie-item.  

   -   **Zwervende gebruikersprofielen:** schakel dit selectievakje in als u instellingen wilt configureren voor zwervende gebruikersprofielen voor dit configuratie-item.  

4. Op de pagina **Mapomleiding** van de wizard **Configuratie-item voor gebruikersgegevens en -profielen maken**geeft u op hoe u Mapomleiding wilt beheren op clientcomputers van gebruikers die dit configuratie-item ontvangen. U kunt instellingen configureren voor elk apparaat waarmee de gebruiker zich aanmeldt of alleen voor de primaire apparaten van de gebruiker. Raadpleeg de Windows Server-documentatie voor meer informatie over mapomleiding.  

   > [!NOTE]  
   >  Deze pagina wordt alleen weer gegeven als u **Mapomleiding** hebt ingeschakeld op de pagina **Algemeen** van de wizard.  

5. Op de pagina **Offlinebestanden** van de wizard **Configuratie-item voor gebruikersgegevens en -profielen maken**kunt u offlinebestanden in- of uitschakelen voor gebruikers die dit configuratie-item ontvangen en kunt u instellingen configureren voor het gedrag van offlinebestanden. U kunt ook offlinebestanden opgeven die altijd beschikbaar zijn op een computer waarbij de gebruiker zich aanmeldt. Raadpleeg de Windows Server-documentatie voor meer informatie over offlinebestanden.  

   > [!NOTE]  
   >  Deze pagina wordt alleen weer gegeven als u het selectie vakje **offline bestanden** hebt ingeschakeld op de pagina **Algemeen** van de wizard.  

6. Op de pagina **Zwervende profielen** van de wizard **Configuratie-item voor gebruikersgegevens en -profielen maken**kunt u configureren of zwervende profielen beschikbaar zijn op computers waarbij de gebruiker zich aanmeldt en kunt u ook meer informatie configureren over de werking van deze profielen. Raadpleeg de Windows Server-documentatie voor meer informatie over zwervende profielen.  

   > [!NOTE]  
   >  Deze pagina wordt alleen weer gegeven als u het selectie vakje **zwervende gebruikers profielen** hebt ingeschakeld op de pagina **Algemeen** van de wizard.  

7. Voltooi de wizard.  

   Het nieuwe configuratie-item voor gebruikersgegevens en -profielen wordt weergegeven in het knooppunt **Gebruikersgegevens en -profielen** van de werkruimte **Activa en naleving** .  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Een configuratie-item voor gebruikers gegevens en-profielen implementeren  

1.  Klik in de Configuration Manager-console op **activa en**nalevings  >  **instellingen voor naleving**  >  **gebruikers gegevens en-profielen**.  

3.  Selecteer het configuratie-item voor gebruikersgegevens en -profielen dat u wilt implementeren en klik vervolgens op het tabblad **Start** in de groep **Implementatie** op **Implementeren**.  

4.  Geef in het dialoogvenster **Configuratie-item voor gebruikersgegevens en -profielen implementeren** de volgende informatie op.  

    -   **Verzameling** : klik op **Bladeren** om de gebruikersverzameling te selecteren waarvoor u het configuratie-item wilt implementeren.  

        > [!IMPORTANT]  
        >  U kunt alleen configuratie-items voor gebruikersgegevens en -profielen implementeren naar gebruikersverzamelingen.  

    -   **Regels die niet compliant zijn herstellen, waar ondersteund** : schakel deze optie in om automatisch regels te herstellen die als niet-compatibel op clientcomputers worden geëvalueerd.  

    -   **Herstel toestaan buiten het onderhoudsvenster** : Als er een onderhoudsvenster is geconfigureerd voor de verzameling waarnaar u het configuratie-item implementeert, schakelt u deze optie in om de waarde buiten het onderhoudsvenster te laten herstellen met de instellingen voor naleving. Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.  

    -   **Waarschuwing genereren** : Schakel deze optie in om een waarschuwing te configureren die wordt gegenereerd als de naleving van het configuratie-item op een opgegeven datum en tijd minder is dan een opgegeven percentage. U kunt tevens opgeven of u een melding naar System Center Operations Manager wilt verzenden.  

    -   **Geef het evaluatieschema voor compatibiliteit op voor dit configuratie-item** : Geef de planning op waarmee het geïmplementeerde configuratie-item wordt geëvalueerd op clientcomputers. U kunt een eenvoudige of een aangepaste planning opgeven.  

5.  Klik op **OK** om het dialoogvenster **Configuratie-item voor gebruikersgegevens en -profielen implementeren** te sluiten en de implementatie te maken.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>Een configuratie-item voor gebruikersgegevens en -profielen bewaken  
 U kunt dit type configuratie-item op dezelfde manier bewaken als u andere instellingen voor naleving bewaakt.  

 Zie [nalevings instellingen controleren](../../compliance/deploy-use/monitor-compliance-settings.md)voor meer informatie.  

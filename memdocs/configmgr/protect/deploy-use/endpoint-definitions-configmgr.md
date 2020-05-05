---
title: Definities van Endpoint Protection schadelijke software
titleSuffix: Configuration Manager
description: Meer informatie over het configureren van Configuration Manager software-updates voor het leveren van definitie-updates aan client computers.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b734fe2a63373e8fd1af9abe77cde7f52b6824
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126084"
---
# <a name="use-configuration-manager-to-deliver-definition-updates"></a>Configuration Manager gebruiken om definitie-updates te leveren

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt Configuration Manager software-updates configureren om automatisch definitie-updates te leveren aan client computers. Voordat u begint met het maken van regels voor automatische implementatie, moet u Configuration Manager software-updates configureren. Zie [Introduction to software updates](../../sum/understand/software-updates-introduction.md)(Engelstalig) voor meer informatie.

> [!NOTE]
> Deze procedure is specifiek voor Endpoint Protection. Zie [software-updates automatisch implementeren](../../sum/deploy-use/automatically-deploy-software-updates.md)voor meer algemene informatie over regels voor automatische implementatie.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **software-updates**uit en selecteer **regels voor automatische implementatie**.

1. Klik op het tabblad **Start** van het lint in de groep **maken** op **regel voor automatische implementatie maken**.

1. Geef op de pagina **Algemeen** van de **wizard Regel voor automatische implementatie maken**de volgende gegevens op:

    - **Naam**: geef een unieke naam op voor de regel voor automatische implementatie.

    - **Verzameling**: Selecteer de verzameling apparaten waarvoor u de definitie-updates wilt implementeren.

        > [!NOTE]
        > U kunt geen definitie-updates implementeren voor een verzameling gebruikers.

1. Selecteer **toevoegen aan een bestaande software-update groep**.

1. Selecteer **de implementatie inschakelen nadat deze regel is uitgevoerd**.

1. Selecteer op de pagina **implementatie-instellingen** van de wizard, voor het **detail niveau**, **alleen fout berichten**.

    > [!NOTE]
    > Wanneer u **alleen fout berichten**selecteert, wordt het aantal status berichten dat door de definitie-implementatie wordt verzonden, gereduceerd. Deze configuratie vermindert de CPU-verwerking op de Configuration Manager servers.

1. Op de pagina **software-updates** :

    1. Selecteer het eigenschappen Filter voor de **Update classificatie** . Selecteer in de lijst **zoek criteria** de optie **<items die\>u wilt zoeken**.

        Selecteer in het venster **zoek criteria** de optie **definitie-updates**en selecteer vervolgens **OK**.

    1. Selecteer het filter van de **product** eigenschap. Selecteer in de lijst **zoek criteria** de optie **<items die\>u wilt zoeken**.

        Selecteer in het venster **zoek criteria** **System Center Endpoint Protection** voor Windows 8,1 en eerder of **Windows Defender** voor Windows 10 en hoger en selecteer vervolgens **OK**.

    > [!NOTE]
    > U kunt eventueel vervangen updates filteren. Selecteer het **verouderde** eigenschappen Filter. Selecteer in de lijst **zoek criteria** de optie **<items die\>u wilt zoeken**. Selecteer **Nee**in het venster **zoek criteria** en selecteer vervolgens **OK**.

1. Selecteer op de pagina **evaluatie planning** van de wizard **de regel uitvoeren na elke synchronisatie van software-update punten**.

1. Configureer op de pagina **Implementatieplanning** van de wizard de volgende instellingen:

    - **Tijdstip gebaseerd op**: Selecteer **UTC**als u wilt dat alle clients op hetzelfde moment de meest recente definities installeren. De werkelijke installatie tijd varieert binnen twee uur.

    - **Tijd waarop de software beschikbaar is**: Geef de beschik bare tijd op voor de implementatie die door deze regel wordt gemaakt. Het opgegeven tijdstip moet ten minste één uur na de uitvoering van de regel voor automatische implementatie plaatsvinden. Deze configuratie zorgt ervoor dat de inhoud voldoende tijd heeft om te repliceren naar de distributie punten. Sommige definitie-updates kunnen ook engine-updates voor anti-malware bevatten, waardoor het langer kan duren voordat de distributiepunten worden bereikt.

    - **Installatiedeadline**: selecteer **Zo snel mogelijk**.

        > [!NOTE]
        > De deadline voor software-updates varieert gedurende een periode van twee uur. Dit gedrag voor komt dat alle clients tegelijkertijd een update aanvragen.

1. Selecteer op de pagina **gebruikers ervaring** van de wizard, voor **gebruikers meldingen**, **de optie verbergen in Software Center en alle meldingen**. Met deze configuratie worden de definitie-updates op de achtergrond geïnstalleerd.

1. Selecteer op de pagina **implementatie pakket** van de wizard een bestaand implementatie pakket of maak een nieuwe.

    > [!NOTE]
    > Overweeg het plaatsen van definitie-updates in een pakket dat geen andere software-updates bevat. Op die manier blijft de grootte van het definitie-updatepakket beperkt, waardoor het pakket sneller naar de distributiepunten kan worden gerepliceerd.

1. Als u een nieuw implementatie pakket maakt, selecteert u op de pagina **distributie punten** van de wizard een of meer distributie punten. De site kopieert de inhoud voor dit pakket naar deze distributie punten.

1. Selecteer op de pagina **Download locatie** de optie **software-updates downloaden van het Internet**.

1. Selecteer op de pagina **taal selectie** elke taal versie van de updates die u wilt downloaden.

1. Selecteer op de pagina **Download instellingen** het Download gedrag van de benodigde software-updates.

1. Voltooi de wizard.

Controleer of de nieuwe regel wordt weer gegeven in het knoop punt **automatische implementatie regels** van de Configuration Manager-console.

> [!div class="nextstepaction"]
> [Antimalwarebeleid maken en implementeren](endpoint-antimalware-policies.md)

---
title: Endpoint Protection waarschuwingen configureren
titleSuffix: Configuration Manager
description: Meer informatie over het configureren van Endpoint Protection waarschuwingen in Configuration Manager.
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b44147006a9ae4d38d2275a4515d71d61eec55c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074857"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Waarschuwingen voor Endpoint Protection in Configuration Manager configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

 U kunt Endpoint Protection waarschuwingen configureren in micro soft Configuration Manager om gebruikers met beheerders rechten op de hoogte te stellen wanneer specifieke gebeurtenissen, zoals een malware-infectie, optreden in uw-hiërarchie. Meldingen worden weer gegeven in het Endpoint Protection dash board in de Configuration Manager-console in het knoop punt **waarschuwingen** van de werk ruimte **controle** of kunnen worden verzonden naar opgegeven gebruikers.

 Gebruik de volgende stappen en de aanvullende procedures in dit onderwerp voor het configureren van waarschuwingen voor Endpoint Protection in Configuration Manager.

> [!IMPORTANT]
>  U moet beschikken over de machtiging **beveiliging afdwingen** voor verzamelingen om Endpoint Protection waarschuwingen te configureren.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Stappen voor het configureren van waarschuwingen voor Endpoint Protection in Configuration Manager

1.  Klik op **Activa en naleving**op de Configuration Manager-console.

2.  Klik op **Apparaatverzamelingen** in de werkruimte **Activa en naleving**.

3.  Selecteer in de lijst **Apparaatverzamelingen** de verzameling waarvoor u waarschuwingen wilt configureren en klik vervolgens op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.

    > [!NOTE]
    >  U kunt geen waarschuwingen voor gebruikersverzamelingen configureren.

4.  Selecteer op het tabblad **waarschuwingen** van het dialoog venster **Eigenschappen** van _<-verzamelings naam\> _ de optie **deze verzameling weer geven in het Endpoint Protection-dash board** als u details over antimalware-bewerkingen voor deze verzameling wilt weer geven in de werk ruimte **bewaking** van de Configuration Manager-console.

    > [!NOTE]
    >  Deze optie is niet beschikbaar voor de verzameling **Alle systemen** .

5.  Klik op het tabblad **waarschuwingen** van het dialoog venster **Eigenschappen** van _<\> verzamelings naam_ op **toevoegen**.

6.  Selecteer in het dialoog venster **nieuwe verzamelings waarschuwingen toevoegen** in het gedeelte **een waarschuwing genereren wanneer deze voor waarden van toepassing zijn** de waarschuwingen die u wilt Configuration Manager genereren wanneer de opgegeven Endpoint Protection gebeurtenissen optreden en klik vervolgens op **OK**.

7.  Selecteer in de lijst **voor waarden** van het tabblad **waarschuwingen** elke Endpoint Protection waarschuwing en geef de volgende informatie op:

    -   **Naam van waarschuwing** : accepteer de standaard naam of voer een nieuwe naam in voor de waarschuwing.

    -   **Ernst van waarschuwing** : Selecteer in de lijst het waarschuwings niveau dat u wilt weer geven in de Configuration Manager-console.

8.  Geef de volgende aanvullende informatie op, afhankelijk van de waarschuwing die u selecteert:

    -   **Detectie van malware** : deze waarschuwing wordt gegenereerd als er malware wordt gedetecteerd op een computer in de verzameling die u bewaken. De **drempel waarde voor detectie van malware** specificeert de detectie niveaus van malware waarbij deze waarschuwing wordt gegenereerd:

        -   **Hoog-alle detecties** : de waarschuwing wordt gegenereerd wanneer er zich een of meer computers in de opgegeven verzameling bevinden waarop malware wordt gedetecteerd, ongeacht welke actie door de Endpoint Protection-client wordt uitgevoerd.

        -   **Middel-gedetecteerd, in afwachting van actie** : de waarschuwing wordt gegenereerd wanneer er een of meer computers in de opgegeven verzameling zijn waarop malware wordt gedetecteerd, en u moet de schadelijke software hand matig verwijderen.

        -   **Laag-gedetecteerd, nog steeds actief** : de waarschuwing wordt gegenereerd wanneer er sprake is van een of meer computers in de opgegeven verzameling waarop malware is gedetecteerd en nog steeds actief is.

    -   **Malware-uitsplitsing** : deze waarschuwing wordt gegenereerd als opgegeven malware wordt gedetecteerd op een opgegeven percentage computers in de verzameling die u bewaken.

        -   **Percentage computers waarop malware is gedetecteerd** : de waarschuwing wordt gegenereerd wanneer het percentage computers met schadelijke software die in de verzameling wordt gedetecteerd, groter is dan het percentage dat u opgeeft. Geef een percentage van **1** tot en met **99**op.

            > [!NOTE]
            >  De percentage waarde is gebaseerd op het aantal computers in de verzameling, maar sluit computers waarop geen Configuration Manager-client is geïnstalleerd. Het bevat computers waarop de Endpoint Protection-client nog niet is geïnstalleerd.

    -   **Herhaalde detectie van malware** : deze waarschuwing wordt gegenereerd als specifieke malware meer dan een opgegeven aantal keren wordt gedetecteerd gedurende een opgegeven aantal uren op de computers in de verzameling die u bewaken. Geef de volgende gegevens op om deze waarschuwing te configureren:

        -   **Aantal keer dat de malware is gedetecteerd:** de waarschuwing wordt gegenereerd wanneer dezelfde malware meer dan het opgegeven aantal keren op computers in de verzameling wordt gedetecteerd. Geef een getal op van **2** tot en met **32**.

        -   **Interval voor detectie (uren):** geef de interval voor de detectie op (in uren) waarin het aantal malwaredetecties moet plaatsvinden. Geef een getal op van **1** tot en met **168**.

    -   **Detectie van meerdere malware** : deze waarschuwing wordt gegenereerd als meer dan een opgegeven aantal typen malware wordt gedetecteerd over een opgegeven aantal uren op computers in de verzameling die u bewaken. Geef de volgende gegevens op om deze waarschuwing te configureren:

        -   **Aantal malwaretypen dat is gedetecteerd:** de waarschuwing wordt gegenereerd wanneer het opgegeven aantal verschillende malwaretypen op computers in de verzameling wordt gedetecteerd. Geef een getal op van **2** tot en met **32**.

        -   **Interval voor detectie (uren):** Geef het detectie-interval in uren op waarin het aantal detecties van malware moet plaatsvinden. Geef een getal op van **1** tot en met **168**.

9. Klik op **OK** om het dialoog venster **Eigenschappen** van _<\> verzamelings naam_ te sluiten.  

## <a name="alert-for-outdated-malware-client"></a>Waarschuwing voor verouderde malware-client

Vanaf Configuration Manager versie 1702 kunt u een waarschuwing configureren om ervoor te zorgen Endpoint Protection-clients niet verouderd zijn. Vanuit elk apparaat, kunt u nu kolommen toevoegen aan de lijst voor de volgende kenmerken van **antimalware-client versie** en **Endpoint Protection implementatie status**. In de-console navigeert u bijvoorbeeld naar **activa en naleving** > **overzicht** > **apparaat verzamelingen** > **alle Bureau bladen en Server clients**. Klik met de rechter muisknop op de kolomkop en selecteer de kolommen die u wilt toevoegen. Als u wilt controleren op een waarschuwing, bekijkt u **waarschuwingen** in de werk ruimte **bewaking** . Als er meer dan 20% van beheerde clients een verlopen versie van de antimalware-software uitvoert, wordt de antimalware-client versie verouderde waarschuwing weer gegeven. Deze waarschuwing wordt niet weer gegeven op het tabblad **controle** > **overzicht** . Schakel software-updates voor antimalware-clients in om verlopen antimalware-clients bij te werken.

Als u het percentage wilt configureren waarmee de waarschuwing wordt gegenereerd, vouwt u **bewakings** > **waarschuwingen** > **alle waarschuwingen**uit, dubbelklikt u op **antimalware-clients verouderd** en wijzigt u de **waarschuwing voor het activeren als het percentage beheerde clients met een verouderde versie van de antimalware meer is dan de** optie.

> [!div class="button"]
> [Volgende stap >](endpoint-definition-updates.md)
> 
> [!div class="button"]
> [Terug >](endpoint-protection-site-role.md)

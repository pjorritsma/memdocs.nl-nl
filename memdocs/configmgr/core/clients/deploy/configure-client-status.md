---
title: Client status configureren
titleSuffix: Configuration Manager
description: Selecteer client status instellingen in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bb77e1e9f55919a03368d549946ee4dd1cda58a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713574"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>De client status in Configuration Manager configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u Configuration Manager client status kunt bewaken en problemen die worden gevonden, moet u uw site configureren om de para meters op te geven die worden gebruikt om clients als inactief te markeren en opties te configureren om u te waarschuwen als client activiteit onder een opgegeven drempel waarde valt. U kunt ook uitschakelen dat computers automatisch problemen oplossen die worden gevonden door de client status.  

##  <a name="to-configure-client-status"></a><a name="BKMK_1"></a>De client status configureren  

1.  Klik in de Configuration Manager-console op **bewaking**.  

2.  Klik in de werk ruimte **bewaking** op **client status**en klik vervolgens op het tabblad **Start** in de groep **client status** op **client status instellingen**.  

3.  Geef in het dialoog venster **Eigenschappen van client status instellingen** de volgende waarden op om client activiteiten te bepalen:  

    > [!NOTE]  
    >  Als aan geen van de instellingen wordt voldaan, wordt de client als inactief gemarkeerd.  

    -   **Client beleids aanvragen gedurende de volgende dagen:** Geef op hoeveel dagen geleden een client beleid heeft aangevraagd. De standaardwaarde is **7** dagen.  

    -   **Heartbeat-detectie gedurende de volgende dagen:** Geef op hoeveel dagen geleden de client computer een heartbeat-detectie record naar de site database heeft verzonden. De standaardwaarde is **7** dagen.  

    -   **Hardware-inventarisatie gedurende de volgende dagen:** Geef op hoeveel dagen geleden de client computer een hardware-inventarisatie record naar de site database heeft verzonden. De standaardwaarde is **7** dagen.  

    -   **Software-inventarisatie gedurende de volgende dagen:** Geef op hoeveel dagen geleden de client computer een software-inventarisatie record naar de site database heeft verzonden. De standaardwaarde is **7** dagen.  

    -   **Status berichten gedurende de volgende dagen:** Geef op hoeveel dagen geleden de client computer status berichten naar de site database heeft verzonden. De standaardwaarde is **7** dagen.  

4.  Geef in het dialoog venster **Eigenschappen van client status instellingen** de volgende waarde op om te bepalen hoe lang geschiedenis gegevens van de client status behouden moeten blijven:  

    -   **Geschiedenis van client status bewaren gedurende het volgende aantal dagen:** Geef op hoelang u wilt dat de geschiedenis van de client status in de site database blijft. De standaard waarde is **31** dagen.  

5.  Klik op **OK** om de eigenschappen op te slaan en het dialoog venster **Eigenschappen van client status instellingen** te sluiten.  

##  <a name="to-configure-the-schedule-for-client-status"></a><a name="BKMK_Schedule"></a>Het schema voor de client status configureren  

1.  Klik in de Configuration Manager-console op **bewaking**.  

2.  Klik in de werk ruimte **bewaking** op **client status**en klik vervolgens op het tabblad **Start** in de groep **client status** op **client status update plannen**.  

3.  Configureer in het dialoog venster **client status update plannen** het interval waarvoor u de client status wilt bijwerken en klik vervolgens op OK.  

    > [!NOTE]  
    >  Wanneer u de planning voor client status updates wijzigt, wordt de update pas van kracht nadat de volgende geplande client status update (voor het eerder geconfigureerde schema) is uitgevoerd.  

##  <a name="to-configure-alerts-for-client-status"></a><a name="BKMK_2"></a>Waarschuwingen voor de client status configureren  

1. Klik op **Activa en naleving**op de Configuration Manager-console.  

2. Klik op **Apparaatverzamelingen** in de werkruimte **Activa en naleving**.  

3. Selecteer in de lijst **Apparaatverzamelingen** de verzameling waarvoor u waarschuwingen wilt configureren en klik vervolgens op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

   > [!NOTE]  
   >  U kunt geen waarschuwingen voor gebruikersverzamelingen configureren.  

4. Klik op het tabblad **waarschuwingen** van het**Properties** **Add** <em> &lt;dialoog\>venster Eigenschappen van verzamelings naam</em>op toevoegen.  

   > [!NOTE]  
   >  Het tabblad **Waarschuwingen** is alleen zichtbaar als aan de beveiligingsrol waaraan u gekoppeld bent machtigingen voor waarschuwingen zijn toegewezen.  

5. Geef in het dialoogvenster **Nieuwe verzamelingmeldingen toevoegen** op welke meldingen moeten worden gegenereerd wanneer clientstatuswaarden onder een bepaalde drempelwaarde vallen en klik vervolgens op **OK**.  

6. Selecteer elke clientstatuswaarschuwing in de lijst **Voorwaarden** van het tabblad **Waarschuwingen** en geef vervolgens de volgende gegevens op.  

   -   **Naam van waarschuwing** : accepteer de standaard naam of voer een nieuwe naam in voor de waarschuwing.  

   -   **Ernst van waarschuwing** : Kies in de vervolg keuzelijst het waarschuwings niveau dat wordt weer gegeven in de Configuration Manager-console.  

   -   **Waarschuwing activeren** : Geef het drempel percentage voor de waarschuwing op.  

7. Klik op **OK** om het**Properties** <em> &lt;dialoog venster\>eigenschappen van verzamelings naam</em>te sluiten.  

##  <a name="to-exclude-computers-from-automatic-remediation"></a><a name="BKMK_3"></a>Computers uitsluiten van automatisch herstel  

1. Open de REGI ster-editor op de client computer waarvoor u automatisch herstel wilt uitschakelen.  

   > [!WARNING]  
   >  Als u de REGI ster-editor onjuist gebruikt, kunt u ernstige problemen veroorzaken waardoor u het besturings systeem opnieuw moet installeren. Microsoft biedt geen garantie dat u problemen kunt oplossen die veroorzaakt worden door onjuist gebruik van de Registry Editor. Gebruik de Registry Editor op eigen risico.  

2. Ga naar **HKEY_LOCAL_MACHINE \software\microsoft\ccm\ccmeval\notifyonly**.  

3. Voer een van de volgende waarden in voor deze register sleutel:  

   -   **Waar** : de problemen die worden gevonden door de client computer worden niet automatisch hersteld. Er wordt echter nog steeds een waarschuwing weer in de werk ruimte **bewaking** over problemen met deze client.  

   -   **Onwaar** : de client computer zal automatisch problemen oplossen wanneer ze worden gevonden en u wordt gewaarschuwd in de werk ruimte **bewaking** . Dit is de standaardinstelling.  

4. Sluit de Register-editor.  

   U kunt ook clients installeren met behulp van de CCMSetup **NotifyOnly** -installatie-eigenschap om ze uit te sluiten van automatisch herstel. Zie [over eigenschappen van client installatie](../../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie over deze client installatie-eigenschap.  

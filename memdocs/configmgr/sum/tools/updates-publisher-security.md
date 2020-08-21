---
title: Certificaten en beveiliging
titleSuffix: Configuration Manager
description: Certificaten en beveiliging voor System Center Updates Publisher beheren
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc8e31245212136cd67f6f8cac062723c2cabefb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696001"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Certificaten en beveiliging voor updates Uitgever beheren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Aan de hand van de volgende procedures kunt u het certificaat archief op de update server configureren, een zelfondertekende certificaat configureren op de client computer en de groepsbeleid configureren zodat de Windows Update-Agent op computers kan scannen op gepubliceerde updates.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Het certificaat archief op de update server configureren
 Updates Publisher gebruikt een digitaal certificaat voor het ondertekenen van de updates in de catalogussen die worden gepubliceerd. Voordat een catalogus naar de update server kan worden gepubliceerd, moet dat certificaat zich in het certificaat archief op de update server bevindt, en in het certificaat archief van de computer van de update Publisher als die computer extern is van de server voor updates.

De volgende procedure is een van de verschillende mogelijke methoden om het certificaat toe te voegen aan het certificaat archief op de update server.

### <a name="to-configure-the-certificate-store"></a>Het certificaat archief configureren
1.  Klik op een computer die toegang heeft tot de computer van de updates Publisher en de update server op **Start**, klik op **uitvoeren**, typ **MMC** in het tekstvak en klik vervolgens op **OK** om de micro soft Management Console (MMC) te openen.

2.  Klik op **bestand**, klik op **module toevoegen/verwijderen**, klik op **toevoegen**, klik op **certificaten**, klik op **toevoegen**, selecteer **computer account**en klik vervolgens op **volgende**.

3.  Selecteer **een andere computer**, typ de naam van de update server of klik op **Bladeren** om de Update Server computer te zoeken, klik op **volt ooien**, klik op **sluiten**, en klik vervolgens op **OK**.

4.  Vouw **certificaten (*Update server name*)** uit, vouw **WSUS**uit en klik vervolgens op **certificaten**.

5.  Klik in het resultaten venster met de rechter muisknop op het gewenste certificaat, klik op **alle taken**en klik vervolgens op **exporteren**.

6.  Gebruik in de wizard Certificaat exporteren de standaard instellingen om een export bestand te maken met de naam en locatie die zijn opgegeven in de wizard. Dit bestand moet beschikbaar zijn voor de update server voordat u verdergaat met de volgende stap.

7.  Klik met de rechter muisknop op **vertrouwde uitgevers**, klik op **alle taken**en klik vervolgens op **importeren**. Voltooi de wizard Certificaat importeren met het geëxporteerde bestand uit stap 6.

8.  Klik met de rechter muisknop op **vertrouwde basis certificerings instanties**, klik op **alle taken**, en klik vervolgens op **importeren**om een zelfondertekend certificaat te gebruiken, zoals **WSUS Publishers zelf ondertekend**. Voltooi de wizard Certificaat importeren met het geëxporteerde bestand uit stap 6.

9.  Klik met de rechter muisknop op **certificaten (*Update server naam*)**, klik op **verbinding maken met een andere computer**, voer de computer naam voor de updates Publisher-computer in en klik op **OK**.

10. Als updates Publisher extern is van de update server, herhaalt u stap 7 tot en met 9 om het certificaat te importeren in het certificaat archief op de computer met updates Publisher.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Een zelfondertekende certificaat configureren op client computers
Op client computers scant de Windows Update Agent (WUA) naar de updates uit de catalogus. Dit proces kan geen updates installeren wanneer de agent dat digitale certificaat niet kan vinden in het archief met vertrouwde uitgevers op de lokale computer. Als er een zelfondertekend certificaat werd gebruikt voor het publiceren van de Update catalogus, zoals **WSUS Publishers zelf ondertekend**, moet het certificaat ook in het certificaat archief vertrouwde basis certificerings instanties op de lokale computer staan, zodat de agent de geldigheid van het certificaat kan controleren.

U kunt een van de volgende methoden gebruiken voor het configureren van certificaten op client computers, zoals het gebruik van groepsbeleid en de **wizard Certificaat importeren** of met het hulp programma certutil en software distributie.

Hieronder vindt u een voor beeld van het configureren van het handtekening certificaat op client computers.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>Een zelfondertekende certificaat configureren op client computers
1. Klik op een computer met toegang tot de update server op **Start**, klik op **uitvoeren**, typ **MMC** in het tekstvak en klik vervolgens op **OK** om de micro soft Management Console (MMC) te openen.

2. Klik op **bestand**, klik op **module toevoegen/verwijderen**, klik op **toevoegen**, klik op **certificaten**, klik op **toevoegen**, selecteer **computer account**en klik vervolgens op **volgende**.

3. Selecteer **een andere computer**, typ de naam van de update server of klik op **Bladeren** om de Update Server computer te zoeken, klik op **volt ooien**, klik op **sluiten**, en klik vervolgens op **OK**.

4. Vouw **certificaten (*Update server name*)** uit, vouw **WSUS**uit en klik vervolgens op **certificaten**.

5. Klik met de rechter muisknop op het certificaat in het resultaten venster, klik op **alle taken**en klik vervolgens op **exporteren**. Voltooi de **wizard Certificaat exporteren** door de standaard instellingen te gebruiken voor het maken van een export certificaat bestand met de naam en locatie die zijn opgegeven in de wizard.

6. Gebruik een van de volgende methoden om het certificaat toe te voegen dat wordt gebruikt voor het ondertekenen van de Update catalogus op elke client computer die WUA gebruikt om te scannen naar de updates in de catalogus. Voeg als volgt het certificaat toe op de client computer:

   -   Voor zelfondertekende certificaten: Voeg het certificaat toe aan de certificaat archieven **vertrouwde basis certificerings instanties** en **vertrouwde uitgevers** .

   -   Voor verleende certificaten van certificerings instantie (CA): Voeg het certificaat toe aan het certificaat archief van **vertrouwde uitgevers** .

   > [!NOTE]
   > De WUA controleert ook of de instelling **ondertekende inhoud van intranet locatie van micro soft-Update service toestaan** Groepsbeleid is ingeschakeld op de lokale computer. Deze beleidsinstelling moet worden ingeschakeld voor WUA om te scannen naar de updates die zijn gemaakt en gepubliceerd met Updates Publisher. Zie [How to configure the Groepsbeleid op client computers](/previous-versions/bb530967(v=technet.10))(Engelstalig) voor meer informatie over het inschakelen van deze Groepsbeleid instelling.



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>groepsbeleid configureren zodat WUA op computers kan scannen op gepubliceerde updates
Voordat de Windows Update Agent (WUA) op computers scant op updates die zijn gemaakt en gepubliceerd met updates Publisher, moet een beleids instelling zijn ingeschakeld voor het toestaan van ondertekende inhoud van een intranet locatie van micro soft-Update service. Als de beleids instelling is ingeschakeld, accepteert WUA updates die worden ontvangen via een intranet locatie als de updates worden ondertekend in het certificaat archief **vertrouwde uitgevers** op de lokale computer. Er zijn verschillende methoden voor het configureren van groepsbeleid op computers in de omgeving.

Voor computers die zich niet in het domein bevinden, kan de instelling van een register sleutel worden geconfigureerd om ondertekende inhoud toe te staan vanaf een intranet locatie van Microsoft Update service.

De volgende procedures bevatten de basis stappen die kunnen worden gebruikt voor het configureren van groepsbeleid voor computers in het domein en een register sleutel waarde op computers die zich niet in het domein bevinden.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>groepsbeleid zodanig configureren dat WUA kan scannen op gepubliceerde updates
1.  Open de Groepsbeleidsobjecteditor MMC-module (micro soft Management Console) met een gebruiker met de juiste beveiligings rechten voor het configureren van groepsbeleid.

2.  Klik op **Bladeren** en selecteer het domein, de OE of de groeps beleidsobjecten die zijn gekoppeld aan de site waar de geconfigureerde Groepsbeleid worden door gegeven aan de gewenste client computers. Klik op **OK**, klik op **volt ooien**, klik op **sluiten**en klik vervolgens op **OK**.

3.  Vouw de geselecteerde beleids instelling uit in de console structuur, vouw **computer configuratie**uit, vouw **Beheersjablonen**uit, vouw **Windows-onderdelen**uit en klik vervolgens op **Windows Update**.

4.  Klik in het resultaten venster met de rechter muisknop op **ondertekende inhoud toestaan van intranet locatie van micro soft-Update service**, klikt u op **Eigenschappen**, klikt u op **ingeschakeld**en klikt u vervolgens op **OK**.
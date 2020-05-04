---
title: Definities downloaden van een netwerk share
titleSuffix: Configuration Manager
description: Meer informatie over het hand matig downloaden van de nieuwste definitie-updates van micro soft en het configureren van clients om deze definities te downloaden.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9afeee7f7111994f0ae3891c7ecd99a11d7edd7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715681"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share"></a>Endpoint Protection malware-definities inschakelen om te downloaden van een netwerk share

*Van toepassing op: Configuration Manager (huidige vertakking)*

 U kunt handmatig de meest recente definitie-updates van Microsoft downloaden en vervolgens clients zo configureren dat deze de definities uit een gedeelde map op het netwerk downloaden. Gebruikers kunnen ook definitie-updates in gang zetten wanneer u deze bron voor updates gebruikt.

> [!NOTE]
>  Clients moeten leestoegang hebben tot de gedeelde map om de definitie-updates te kunnen downloaden.

 Voor meer informatie over het downloaden van de definitie-en engine-updates om op te slaan op de bestands share, Zie [de nieuwste micro soft antimalware en anti spyware-software installeren](https://www.microsoft.com/wdsi/definitions).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Definitiedownloads van een bestandsshare configureren

1.  Klik op **Activa en naleving**op de Configuration Manager-console.

2.  Vouw **Endpoint Protection** uit in de werkruimte **Activa en naleving**en klik vervolgens op **Anti-malwarebeleidsregels**.

3.  Open de eigenschappenpagina van het **standaard toegepaste anti-malwarebeleid** of maak een nieuw anti-malwarebeleid. Zie voor meer informatie over het maken van antimalwarebeleid [beleid voor het maken en implementeren van antimalwarebeleid voor Endpoint Protection](endpoint-antimalware-policies.md).

4.  Klik in de sectie **beveiligings updates** van het dialoog venster Eigenschappen van anti-malware op **bron instellen**.
    - De sectie **definitie-updates** is gewijzigd in **beveiligings updates** die beginnen met Configuration Manager versie 1902.

5.  Selecteer in het dialoogvenster **Definitie-updatebronnen configureren** de optie **Updates vanuit UNC-bestandsshares**.

6.  Klik op **OK** om het dialoogvenster **Definitie-updatebronnen configureren** te sluiten.

7.  Klik op **Paden instellen**. Voeg vervolgens in het dialoogvenster **UNC-paden voor definitie-updates configureren** een of meer UNC-paden toe aan de locatie van de definitie-updates op een netwerkshare.

8.  Klik op **OK** om het dialoogvenster **UNC-paden voor definitie-updates configureren** te sluiten.


> [!div class="button"]
> [Volgende stap >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Terug >](endpoint-configure-alerts.md)

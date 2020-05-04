---
title: Definitie-updates configureren
titleSuffix: Configuration Manager
description: Meer informatie over het selecteren en configureren van methoden met Endpoint Protection in Configuration Manager om antimalware-definities up-to-date te houden op client computers.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce11ba0cbe4298d32a11de409910ebc3e14c097b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715765"
---
# <a name="configure-definition-updates-for-endpoint-protection"></a>Definitie-updates voor Endpoint Protection configureren  

*Van toepassing op: Configuration Manager (huidige vertakking)*

 Met Endpoint Protection in Configuration Manager kunt u een van de verschillende beschik bare methoden gebruiken om antimalware-definities up-to-date te houden op client computers in uw hiërarchie. U kunt deze methoden aan de hand van de informatie in dit onderwerp selecteren en configureren.

 Als u anti-malwaredefinities wilt bijwerken, kunt u een of meer van de volgende methoden gebruiken:

- [Gedistribueerde updates van Configuration Manager](endpoint-definitions-configmgr.md) : deze methode gebruikt Configuration Manager software-updates om definitie-en engine-updates te leveren aan computers in uw hiërarchie.

- [Gedistribueerde updates van Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) : deze methode maakt gebruik van de WSUS-infra structuur voor het leveren van definitie-en engine-updates voor computers.

- [Gedistribueerde updates van Microsoft Update](endpoint-definitions-microsoft-updates.md) : met deze methode kunnen computers rechtstreeks verbinding maken met Microsoft Update om definitie-en engine-updates te downloaden. Deze methode kan nuttig zijn voor computers die niet vaak verbinding maken met het bedrijfsnetwerk.

- [Gedistribueerde updates van micro soft Malware Protection Center](endpoint-definitions-protection-center.md) : met deze methode worden de definitie-updates gedownload vanuit het micro soft Malware Protection Center.

- [Updates van UNC-bestands shares](endpoint-definitions-network.md) : met deze methode kunt u de meest recente definitie-en engine-updates op een share in het netwerk opslaan. Clients krijgen vervolgens toegang tot het netwerk om de updates te installeren.

  U kunt meerdere definitie-updatebronnen configureren en de volgorde bepalen waarin deze worden beoordeeld en toegepast. Dit doet u in het dialoogvenster **Definitie-updatebronnen configureren** wanneer u een anti-malwarebeleid maakt.

> [!IMPORTANT]
>  Voor Windows 10-Pc's moet u Endpoint Protection configureren voor het bijwerken van malware-definities voor Windows Defender.

## <a name="how-to-configure-definition-update-sources"></a>Definitie-updatebronnen configureren
 Gebruik de volgende procedure voor het configureren van de definitie-updatebronnen zodat deze kunnen worden gebruikt voor elk anti-malwarebeleid.

1.  Klik op **Activa en naleving**op de Configuration Manager-console.

2.  Vouw **Endpoint Protection** uit in de werkruimte **Activa en naleving**en klik vervolgens op **Anti-malwarebeleidsregels**.

3.  Open de eigenschappenpagina van het **standaard toegepaste anti-malwarebeleid** of maak een nieuw anti-malwarebeleid. Zie voor meer informatie over het maken van antimalwarebeleid [beleid voor het maken en implementeren van antimalwarebeleid voor Endpoint Protection](endpoint-antimalware-policies.md).

4.  Klik in de sectie **beveiligings updates** van het dialoog venster Eigenschappen van anti-malware op **bron instellen**.
    - De sectie **definitie-updates** is gewijzigd in **beveiligings updates** die beginnen met Configuration Manager versie 1902.

5.  Selecteer in het dialoogvenster **Definitie-updatebronnen configureren** de bronnen die moeten worden gebruikt voor de definitie-updates. U kunt op **Omhoog** of **Omlaag** klikken om de volgorde waarin deze bronnen worden gebruikt te wijzigen.

6.  Klik op **OK** om het dialoogvenster **Definitie-updatebronnen configureren** te sluiten.

## <a name="configure-endpoint-protection-definitions"></a>Endpoint Protection definities configureren

-   [Gedistribueerde updates van Configuration Manager](endpoint-definitions-configmgr.md) : deze methode gebruikt Configuration Manager software-updates om definitie-en engine-updates te leveren aan computers in uw hiërarchie.

-   [Gedistribueerde updates van Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) : deze methode maakt gebruik van de WSUS-infra structuur voor het leveren van definitie-en engine-updates voor computers.

-   [Gedistribueerde updates van Microsoft Update](endpoint-definitions-microsoft-updates.md) : met deze methode kunnen computers rechtstreeks verbinding maken met Microsoft Update om definitie-en engine-updates te downloaden. Deze methode kan nuttig zijn voor computers die niet vaak verbinding maken met het bedrijfsnetwerk.

-   Gedistribueerde updates van micro soft Malware Protection Center: met deze methode worden de definitie-updates gedownload vanuit het micro soft Malware Protection Center.

-   [Updates van UNC-bestands shares](endpoint-definitions-network.md) : met deze methode kunt u de meest recente definitie-en engine-updates op een share in het netwerk opslaan. Clients krijgen vervolgens toegang tot het netwerk om de updates te installeren.

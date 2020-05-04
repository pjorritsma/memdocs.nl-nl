---
title: De instellingen voor naleving plannen en configureren
titleSuffix: Configuration Manager
description: Meer informatie over de vereisten en configuratie taken voor het werken met nalevings instellingen in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73ccec4ca318b522c0714bc8e5cc89f6c8899edd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712153"
---
# <a name="plan-for-and-configure-compliance-settings-in-configuration-manager"></a>De instellingen voor naleving plannen en configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u aan de slag gaat met Configuration Manager instellingen voor naleving, zijn er enkele vereisten die u moet weten en sommige configuratie taken die u moet uitvoeren.  

## <a name="prerequisites-for-compliance-settings"></a>Vereisten voor de nalevingsinstellingen  

|Vereiste|Meer informatie|  
|------------------|----------------------|  
|Windows Configuration Manager-clients moeten zijn ingeschakeld en geconfigureerd voor compatibiliteits evaluatie.|Zie hieronder|  
|Als u rapporten uitvoeren wilt, moet u de rapportage voor uw site configureren.|[Inleiding op rapportage](../../core/servers/manage/introduction-to-reporting.md)|  
|Vereiste beveiligings machtigingen.|De beveiligingsrol **nalevings instellingen Manager** bevat de benodigde machtigingen voor het beheren van instellingen voor naleving, configuratie-items voor gebruikers gegevens en-profielen en profielen voor externe verbindingen.<br /><br /> [Beheer op basis van rollen configureren](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Nalevings instellingen inschakelen en configureren (alleen voor Windows-Pc's)  

Met deze procedure configureert u de standaardclientinstellingen voor de instellingen voor naleving en past u deze toe op alle computers in uw hiërarchie. Als u wilt dat deze instellingen alleen van toepassing zijn op enkele computers, maakt u een aangepaste apparaatclientinstelling en wijst u deze toe aan een verzameling die de computers bevat waarvoor u de instellingen voor naleving wilt gebruiken. Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor meer informatie over het maken van aangepaste apparaatinstellingen.  

> [!TIP]  
>  Andere typen apparaten vereisen geen specifieke configuratie om de instellingen voor naleving te evalueren.  

1.  Klik in de Configuration Manager-console op**standaard instellingen**voor de **beheer** > **client instellingen** > .  
2.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  
3.  Klik in het dialoogvenster **Standaardinstellingen** op **Instellingen voor naleving**.  
4.  Configureer de volgende nalevingsinstellingen voor clients:
    - **Compatibiliteits evaluatie op clients inschakelen** : Stel deze optie in op **True** als u compliantie op client apparaten wilt evalueren.
    - **Nalevings evaluatie plannen** : Klik op **schema** als u het standaard evaluatie schema voor naleving op client apparaten wilt wijzigen.
    - **Gebruikers gegevens en-profielen inschakelen** : Schakel deze optie in als u configuratie-items voor gebruikers gegevens en-profielen wilt maken en implementeren op Windows-computers. Zie [configuratie-items voor gebruikers gegevens en-profielen maken](../deploy-use/create-remote-connection-profiles.md)voor meer informatie.
5. Klik op **OK** om het dialoogvenster **Standaardinstellingen** te sluiten.  

De volgende keer dat clientcomputers clientbeleid downloaden, worden deze geconfigureerd met deze instellingen.  

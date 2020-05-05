---
title: Definities van schadelijke software Endpoint Protection van WSUS
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Meer informatie over het configureren van Windows Server updates services voor het automatisch goed keuren van definitie-updates.
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126026"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>Endpoint Protection malware-definities inschakelen voor het downloaden van WSUS voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u WSUS gebruikt om de anti-malwaredefinities up-to-date te houden, kunt u deze zo configureren dat de definitie-updates automatisch worden goedgekeurd. Hoewel het gebruik van Configuration Manager software-updates de aanbevolen methode is om definities up-to-date te houden, kunt u WSUS ook configureren als een methode om gebruikers toe te staan om definities hand matig bij te werken. Gebruik de volgende procedures om WSUS te configureren als een definitie-updatebron.

## <a name="synchronize-definition-updates-for-configuration-manager"></a>Definitie-updates voor Configuration Manager synchroniseren

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer vervolgens **sites**.

1. Selecteer de site die het software-updatepunt bevat. Selecteer in de groep **instellingen** van het lint de optie **site onderdelen configureren**en selecteer vervolgens **Software-update punt**.

1. Ga in het venster **Eigenschappen van software-update punt component** naar het tabblad **classificaties** . Selecteer **definitie-updates**.

1. Als u de **producten** wilt opgeven die zijn bijgewerkt met WSUS, gaat u naar het tabblad **producten** .

    - Voor Windows 10 en hoger: Selecteer onder micro soft > Windows **Windows Defender**.

    - Voor Windows 8,1 en eerder: Selecteer onder micro soft > Forefront de optie **System Center Endpoint Protection**.

1. Selecteer **OK** om het venster **Eigenschappen van software-update punt componenten** te sluiten.

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>Definitie-updates voor zelfstandige WSUS synchroniseren

Gebruik de volgende procedure om Endpoint Protection-updates te configureren wanneer uw WSUS-server niet is geïntegreerd in uw Configuration Manager omgeving.

1. Vouw in de WSUS-beheer console **computers**uit, selecteer **Opties**en selecteer vervolgens **producten en classificaties**.

1. Als u de **producten** wilt opgeven die zijn bijgewerkt met WSUS, gaat u naar het tabblad **producten** .

    - Voor Windows 10 en hoger: Selecteer onder micro soft > Windows **Windows Defender**.

    - Voor Windows 8,1 en eerder: Selecteer onder micro soft > Forefront de optie **System Center Endpoint Protection**.

1. Schakel over naar het tabblad **classificaties** . Selecteer **definitie-updates** en- **updates**.

## <a name="approve-definition-updates"></a>Definitie-updates goed keuren

Endpoint Protection definitie-updates moeten worden goedgekeurd en gedownload naar de WSUS-server voordat ze worden aangeboden aan clients die de lijst met beschik bare updates aanvragen. Clients maken verbinding met de WSUS-server om te controleren op de benodigde updates en vragen vervolgens de meest recent goedgekeurde definitie-updates aan.

### <a name="approve-definitions-and-updates-in-wsus"></a>Definities en updates goed keuren in WSUS

1. Selecteer **updates**in de WSUS-beheer console. Selecteer vervolgens **alle updates** of de classificatie van updates die u wilt goed keuren.

1. Klik in de lijst met updates met de rechter muisknop op de update of updates die u wilt goed keuren voor installatie en selecteer vervolgens **goed keuren**.

1. Selecteer in het venster **updates goed keuren** de computer groep waarvoor u de updates wilt goed keuren en selecteer vervolgens **goedgekeurd voor installatie**.

### <a name="configure-an-automatic-approval-rule"></a>Een automatische goedkeurings regel configureren

U kunt ook een automatische goedkeurings regel voor definitie-updates en Endpoint Protection updates instellen. Met deze actie wordt WSUS zo geconfigureerd dat Endpoint Protection definitie-updates die worden gedownload door WSUS, automatisch worden goedgekeurd.

1. Selecteer in de WSUS-beheer console **Opties**en selecteer vervolgens **Automatische goed keuringen**.

1. Selecteer op het tabblad **update regels** de optie **nieuwe regel**.

1. Selecteer in het venster **regel toevoegen** onder **stap 1: eigenschappen selecteren**de optie: **Wanneer een update zich in een specifieke classificatie bevindt**.

    1. Selecteer bij **stap 2: de eigenschappen bewerken** **een wille keurige classificatie**.

    1. Wis alle opties behalve **definitie-updates**en selecteer vervolgens **OK**.

1. Selecteer in het venster **regel toevoegen** onder **stap 1: eigenschappen selecteren**de optie: **Wanneer een update zich in een specifiek product bevindt**.

    1. Selecteer **een product**onder **stap 2: de eigenschappen bewerken**.

    1. Wis alle opties behalve **System Center Endpoint Protection** voor Windows 8,1 en eerder of **Windows Defender** voor Windows 10 en hoger. Selecteer vervolgens **OK**.

1. Voer onder **stap 3: een naam opgeven**een naam in voor de regel en selecteer vervolgens **OK**.

1. Selecteer in het dialoog venster **Automatische goed keuringen** de regel die u zojuist hebt gemaakt en selecteer vervolgens **regel uitvoeren**.

> [!NOTE]
> Weiger oude definitie-updates zodat de prestaties van uw WSUS-server en clientcomputers optimaal zijn. Als u wilt dat deze taak wordt uitgevoerd, kunt u automatische goedkeuring voor revisies en automatische weigering van verlopen updates configureren. Zie [Microsoft ondersteuning artikel 938947](https://support.microsoft.com/kb/938947)voor meer informatie.

> [!div class="nextstepaction"]
> [Antimalwarebeleid maken en implementeren](endpoint-antimalware-policies.md)

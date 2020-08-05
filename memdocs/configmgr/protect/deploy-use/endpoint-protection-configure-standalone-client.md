---
title: Endpoint Protection op een zelfstandige client configureren
titleSuffix: Configuration Manager
description: Meer informatie over het configureren van Endpoint Protection op een zelfstandige client.
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a7640fade49c70c013cf1d7c0939957a07f223fd
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546898"
---
# <a name="configure-endpoint-protection-on-a-standalone-client"></a>Endpoint Protection op een zelfstandige client configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Uw organisatie kan een aantal zelfstandige clients hebben die u niet kunt beheren of beveiligen met micro soft endpoint Configuration Manager. Zonder dat er Endpoint Protection aanwezig is, zijn deze zelfstandige clients kwetsbaar voor mogelijke aanvallen op malware. Als u dergelijke zelfstandige clients wilt beveiligen, kunt u ze hand matig configureren met Endpoint Protection, zoals wordt beschreven in dit onderwerp.

Endpoint Protection op een zelfstandige client hand matig configureren:

- [Een antimalwarebeleid maken voor de zelfstandige client](#create-an-antimalware-policy-for-the-standalone-client)
- [Endpoint Protection-client installatie pakket overzetten naar de zelfstandige client](#transfer-endpoint-protection-client-installation-package-to-the-standalone-client)
- [Endpoint Protection op de zelfstandige client installeren](#install-endpoint-protection-on-the-standalone-client)

## <a name="prerequisites"></a>Vereisten

Hier volgen de vereisten voor het configureren van Endpoint Protection op een zelfstandige client:

- U moet toegang hebben tot het Endpoint Protection-client installatie pakket, **scepinstall.exe**. U kunt dit pakket vinden in de map **C:\Program Files\Microsoft Configuration Manager\Client** . 
- Zorg ervoor dat de [anti-malware-platform update van januari 2017 voor Endpoint Protection-clients](https://support.microsoft.com/help/3209361/january-2017-anti-malware-platform-update-for-endpoint-protection-clie) is geïnstalleerd. 

## <a name="create-an-antimalware-policy-for-the-standalone-client"></a>Een antimalwarebeleid maken voor de zelfstandige client

In deze stap maakt u een aangepast antimalwarebeleid in de Configuration Manager-console en brengt u het vervolgens over naar de zelfstandige client.

Wanneer u het antimalwarebeleid maakt, moet u de bron van de definitie-update configureren om de beleids definities up-to-date te houden op de zelfstandige client. U kunt de bron voor definitie-updates configureren als [Microsoft Update](endpoint-definitions-microsoft-updates.md) en [micro soft Malware Protection Center](endpoint-definitions-protection-center.md)als uw zelfstandige client is verbonden met internet. U kunt ook [netwerk share](endpoint-definitions-network.md) selecteren als definitie distributie bron en deze regel matig bijwerken met het meest recente definitie-update pakket. 

Een antimalwarebeleid maken voor de zelfstandige client:

1. Klik in de **Configuration Manager** -console op **activa en naleving**.
2. Vouw **Endpoint Protection** uit in de werkruimte **Activa en naleving**en klik vervolgens op **Anti-malwarebeleidsregels**.
3. Klik op het tabblad **Start** in de groep **Maken** op **Antimalwarebeleid**maken.
4. Geef in de sectie **Algemeen** van het dialoogvenster **Antimalwarebeleid maken** een naam en beschrijving voor het nieuwe beleid op.
5. Configureer in het dialoogvenster **Antimalwarebeleid maken** de instellingen die u nodig hebt voor deze beleidsregel en klik vervolgens op **OK**. Zie [lijst met instellingen voor het Antimalwarebeleid](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings)voor een lijst met instellingen die u kunt configureren.
    > [!NOTE]
    > Selecteer voor de instelling **definitie-updates** de optie **updates gedistribueerd van Microsoft Update** en updates die worden **gedistribueerd vanuit micro soft Malware Protection Center** als uw zelfstandige client is verbonden met internet.  
    > U kunt ook **updates van UNC-bestands shares** selecteren om de beleids definities via de netwerk share te distribueren. Voeg vervolgens een of meer UNC-paden toe aan de locatie van de definitie-update bestanden op een netwerk share.

6. Exporteer het zojuist gemaakte beleid als een XML-bestand:
    1. Klik met de rechter muisknop op uw beleid in de lijst met beleids regels voor anti- **malware** .
    1. Selecteer **Exporteren**.
    1. Sla het beleid op als een XML-bestand, bijvoorbeeld **standalone.xml**.
7. Zet de nieuwe XML van het antimalwarebeleid over naar de zelfstandige doel client waarop u Endpoint Protection wilt configureren.

## <a name="transfer-endpoint-protection-client-installation-package-to-the-standalone-client"></a>Endpoint Protection-client installatie pakket overzetten naar de zelfstandige client

In deze stap kopieert u het Endpoint Protection-client installatie pakket (**scepinstall.exe**) van de Configuration Manager-server en brengt u deze over naar de zelfstandige client.

1. Meld u aan bij de Configuration Manager-server.
2. Ga naar de map **client** van de installatiemap van Configuration Manager (**C:\Program Files\Microsoft Configuration Manager\Client**).
3. **scepinstall.exe**kopiëren.
4. Breng **scepinstall.exe** over naar de zelfstandige doel client waarop u de Endpoint Protection-client software wilt installeren.

## <a name="install-endpoint-protection-on-the-standalone-client"></a>Endpoint Protection op de zelfstandige client installeren
In deze stap voert u het installatie pakket (**scepinstall.exe**) en het antimalwarebeleid (dat beide eerder zijn overgedragen van de Configuration Manager-server) uit vanaf de opdracht prompt op de zelfstandige client.

Endpoint Protection op de zelfstandige client installeren:

1. Open op de zelfstandige client een opdracht prompt als beheerder.
2. Ga naar de map waarin u het **scepinstall.exe** -installatie bestand hebt opgeslagen.
3. Voer de volgende opdracht in om **scepinstall.exe** uit te voeren met het antimalwarebeleid:

    ```cmd
    scepinstall.exe /policy <full path>\<policy file>
    ```

    Vervang door `full path` het pad waar u het XML-bestand van het antimalwarebeleid hebt opgeslagen en `policy file` met de bestands naam voor het antimalwarebeleid.
 
    Het installatie programma wordt uitgepakt en de installatie wizard wordt gestart.

4. Volg de instructies op het scherm om de client installatie te volt ooien.

    Op het laatste scherm van de installatie wizard wordt de optie voor het scannen van de computer op mogelijke dreigingen na het ophalen van de meest recente updates standaard geselecteerd. U kunt het selectie vakje uitschakelen om het scannen over te slaan.

## <a name="change-antimalware-policy-settings-on-a-standalone-endpoint-protection-client"></a>Instellingen voor antimalwarebeleid wijzigen op een zelfstandige Endpoint Protection-client

Het antimalwarebeleid op uw zelfstandige Endpoint Protection-client wijzigen of bijwerken: 

1. [Een antimalwarebeleid maken voor de zelfstandige client](#create-an-antimalware-policy-for-the-standalone-client).
2. Voer de volgende opdracht uit op de zelfstandige client:

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```

Vervang door `full path` het pad waar u het nieuwe XML-bestand van het antimalwarebeleid hebt opgeslagen en `policy file` met de bestands naam voor het antimalwarebeleid.

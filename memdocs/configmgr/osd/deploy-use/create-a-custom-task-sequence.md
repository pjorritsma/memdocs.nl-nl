---
title: Een aangepaste takenreeks maken
titleSuffix: Configuration Manager
description: Bewerk een aangepaste taken reeks in Configuration Manager om stappen toe te voegen aan de taken reeks.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f390c3857ad5a277002839c4c14ab1307d9ab281
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125573"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>Een aangepaste taken reeks maken met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u een aangepaste taken reeks in Configuration Manager maakt, bevat deze geen taken reeks stappen. Nadat u de taken reeks hebt gemaakt, bewerkt u deze en voegt u de taken reeks stappen toe die u nodig hebt.  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a>Een aangepaste taken reeks maken

Gebruik de volgende procedure om een aangepaste taken reeks te maken:

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **taken reeksen** .  

1. Selecteer **taken reeks maken**op het tabblad **Start** van het lint in de groep **maken** . Met deze actie wordt de wizard taken reeks maken gestart.  

1. Selecteer **Nieuwe aangepaste takenreeks maken** op de pagina **Nieuwe takenreeks maken**.  

1. Op de pagina **taken reeks informatie** geeft u het volgende op:

    - Een naam voor de taken reeks
    - Een beschrijving van de taken reeks
    - Een optionele opstart installatie kopie voor de taken reeks die moet worden gebruikt

Nadat u de wizard taken reeks maken hebt voltooid, voegt Configuration Manager de aangepaste taken reeks toe aan het knoop punt **taken reeksen** . U kunt deze takenreeks nu bewerken om er takenreeksstappen aan toe te voegen.  

## <a name="see-also"></a>Zie ook

Zie [taken reeks stappen](../understand/task-sequence-steps.md)voor een lijst met beschik bare taken reeks stappen.  

Zie [de taken reeks editor gebruiken](../understand/task-sequence-editor.md)voor meer informatie over het bewerken van een taken reeks.  

Meestal gebruikt u taken reeksen om taken voor de implementatie van het besturings systeem te automatiseren, maar u kunt een aangepaste taken reeks maken om verschillende soorten taken te automatiseren. Zie [een taken reeks maken voor niet-besturingssysteem implementaties](create-a-task-sequence-for-non-operating-system-deployments.md)voor meer informatie.

Vanaf versie 2002 kunt u complexe toepassingen installeren met behulp van taken reeksen via het toepassings model. Voeg een implementatie type toe aan een app die een taken reeks is, ofwel om de app te installeren of te verwijderen. Zie [Windows-toepassingen maken](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)voor meer informatie.<!-- 3555953 -->

## <a name="next-steps"></a>Volgende stappen

[De taken reeks implementeren](deploy-a-task-sequence.md)

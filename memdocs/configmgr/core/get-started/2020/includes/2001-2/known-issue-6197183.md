---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: 0db30a8fdc96bc1e1d2d1ff2a059eca8d454d48e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712090"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a>Kan enkele verzamelingen niet maken of bewerken

<!--6197183-->
In deze versie van de Technical Preview-vertakking kunt u geen nieuwe verzameling maken. U kunt ook de eigenschappen van een bestaande gebruikers verzameling niet bewerken.

U kunt dit probleem omzeilen door Configuration Manager Power shell-cmdlets te gebruiken voor het maken van nieuwe verzamelingen en het bewerken van bestaande gebruikers verzamelingen. Enkele van de beschik bare cmdlets voor het beheren van verzamelingen zijn onder andere:

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)

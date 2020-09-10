---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: c7fce3664d23d6402d28b053129fb2b15b540a87
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644398"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Kan enkele verzamelingen niet maken of bewerken

<!--6197183-->
In deze versie van de Technical Preview-vertakking kunt u geen nieuwe verzameling maken. U kunt ook de eigenschappen van een bestaande gebruikers verzameling niet bewerken.

U kunt dit probleem omzeilen door Configuration Manager Power shell-cmdlets te gebruiken voor het maken van nieuwe verzamelingen en het bewerken van bestaande gebruikers verzamelingen. Enkele van de beschik bare cmdlets voor het beheren van verzamelingen zijn onder andere:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
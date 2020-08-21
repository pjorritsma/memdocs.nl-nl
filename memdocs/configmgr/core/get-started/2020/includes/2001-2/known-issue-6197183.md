---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: fca1d884b75380f90a2e2e3cdc2fb0cac357b6b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703033"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Kan enkele verzamelingen niet maken of bewerken

<!--6197183-->
In deze versie van de Technical Preview-vertakking kunt u geen nieuwe verzameling maken. U kunt ook de eigenschappen van een bestaande gebruikers verzameling niet bewerken.

U kunt dit probleem omzeilen door Configuration Manager Power shell-cmdlets te gebruiken voor het maken van nieuwe verzamelingen en het bewerken van bestaande gebruikers verzamelingen. Enkele van de beschik bare cmdlets voor het beheren van verzamelingen zijn onder andere:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
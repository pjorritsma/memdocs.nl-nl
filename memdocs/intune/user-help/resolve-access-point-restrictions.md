---
title: Beperkingen voor toegangspunten die zijn ingesteld in Intune oplossen
description: Neem de drie veelvoorkomende berichten voor het Intune-beleid voor beperkingen voor toegangspunten door en lees hoe u deze oplost
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/28/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: b196b7e29ee8423efebd458564d12be950c14102
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79347506"
---
# <a name="resolve-access-point-restrictions"></a>Beperkingen voor toegangspunten oplossen

Organisaties kunnen de locaties beperken van waaruit apparaten toegang hebben tot bedrijfsgegevens.
Ze geven goedgekeurde netwerklocaties op en stellen deze in om deze *beperkingen voor toegangspunten* te configureren.  

Wanneer u probeert om met een niet-herkend of niet-goedgekeurd netwerk verbinding te maken, kunt u een of meer van de volgende berichten ontvangen:

* Er zijn geen beperkingen voor toegangspunten ingesteld.
* U bent niet verbonden met een goedgekeurd netwerk.
* Er is een fout opgetreden en de beperkingen voor toegangspunten kunnen niet worden doorgevoerd.

 In de onderstaande tabellen wordt elk bericht vermeld en wordt beschreven wat het bericht betekent en hoe u weer toegang kunt krijgen tot uw bedrijfsresources.

## <a name="access-point-restrictions-not-set-up"></a>Er zijn geen beperkingen voor toegangspunten ingesteld  
| Bedrijfsportalbericht | Wat het bericht betekent | Wat u moet doen                                                               
|------------------------|--------------------------|--------------------------|
| **Er zijn geen beperkingen voor toegangspunten ingesteld: er zijn beperkingen voor toegangspunten actief en deze moeten worden ingesteld.** | Uw bedrijf heeft beperkingen voor toegangspunten toegepast op uw apparaat. Voor deze instelling moet de bedrijfsportal-app enkele netwerkinstellingen op uw apparaat controleren. | Tik op **Oplossen**. De bedrijfsportal-app zal een controle uitvoeren om na te gaan of u verbonden bent met een netwerk dat is goedgekeurd door het bedrijf. |

## <a name="not-connected-to-an-approved-network"></a>Niet verbonden met een goedgekeurd netwerk  

| Bedrijfsportalbericht | Wat het bericht betekent | Wat u moet doen                                                                   
|------------------------|-----------------------------------|--------------------------|
| **Het apparaat is niet verbonden met een goedgekeurd netwerk: maak verbinding met een goedgekeurd draadloos netwerk.** | U bent verbonden met een netwerk dat niet is goedgekeurd voor bedrijfstoegang. Zolang u met dit netwerk verbonden bent, kunt u geen toegang krijgen tot zakelijke e-mail, apps en andere beveiligde bedrijfsresources. | Maak verbinding met een netwerk dat is goedgekeurd door het bedrijf. Tik vervolgens op **Oplossen** om het opnieuw te proberen. |

## <a name="restrictions-couldnt-be-enforced"></a>De beperkingen kunnen niet worden doorgevoerd  

| Bedrijfsportalbericht | Wat het bericht betekent | Wat u moet doen                                                                      
|------------------------|-----------------------------------|--------------------------|
| **De beperkingen voor toegangspunten kunnen niet worden doorgevoerd: er is een fout opgetreden in de bedrijfsportal.** | Intune kan niet bepalen of u bent verbonden met een goedgekeurd netwerk. Deze fout is mogelijk het gevolg van een slechte netwerkverbinding, een bijna lege batterij, de batterijbesparingsmodus of een fout in de bedrijfsportal. | Controleer of u een goede netwerkverbinding hebt. Schakel de batterijbesparingsmodus uit en controleer of de levensduur van de batterij nog ten minste 30% is. Tik vervolgens op **Oplossen** om het opnieuw te proberen. 

Nog hulp nodig? U kunt het beste contact opnemen met het ondersteuningsteam van uw bedrijf. Ga voor de specifieke contactgegevens naar de [bedrijfsportalwebsite](https://portal.manage.microsoft.com/#HelpDeskDialog).
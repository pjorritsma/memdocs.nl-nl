---
title: Profielen voor het inrichten van iOS-/iPadOS-apps in Microsoft Intune
titleSuffix: ''
description: Intune biedt u de hulpmiddelen om proactief een nieuw inrichtingsprofiel toe te wijzen aan apparaten met apps die bijna zijn verlopen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: bbc3ba4a-df48-4aeb-988b-69a177764e3a
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: faf7a5b2b5fd027d3ee3f468acb8e6f0d4eef2f7
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989596"
---
# <a name="use-ios-app-provisioning-profiles-to-prevent-your-apps-from-expiring"></a>Inrichtingsprofielen gebruiken voor iOS-apps om te voorkomen dat uw apps verlopen

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

## <a name="introduction"></a>Inleiding

Apple iOS/iPadOS mobiele Line-Of-Business-apps die zijn toegewezen aan iPhones en iPads, zijn gebouwd met een inrichtingsprofiel en code die is ondertekend met een certificaat. Wanneer de app wordt uitgevoerd, bevestigt iOS/iPadOS de integriteit van de iOS-/iPadOS-app en worden beleidsregels afgedwongen die zijn gedefinieerd door het inrichtingsprofiel. De volgende validaties vinden plaats:

- **Integriteit van installatiebestand**: iOS/iPadOS vergelijkt de details van de app met de openbare sleutel van het handtekeningcertificaat van de onderneming. Als deze verschillen, is de inhoud van de app mogelijk gewijzigd en mag de app niet worden uitgevoerd.
- **Mogelijkheden afdwingen**: iOS/iPadOS probeert de app-mogelijkheden af te dwingen van het inrichtingsprofiel van de onderneming (geen afzonderlijke inrichtingsprofielen van ontwikkelaars) dat zich in het app-installatiebestand (.ipa) bevindt.


Het handtekeningcertificaat voor ondernemingen dat u gebruikt om apps te ondertekenen is doorgaans drie jaar geldig. Echter, het inrichtingsprofiel verloopt na één jaar. Zolang het certificaat nog geldig is, biedt Intune u de hulpmiddelen om proactief een nieuw inrichtingsprofiel toe te wijzen aan apparaten met apps die binnenkort verlopen.
Nadat het certificaat is verlopen, moet u de app opnieuw ondertekenen met een nieuw certificaat en een nieuw inrichtingsprofiel implementeren met de sleutel van het nieuwe certificaat.

Als beheerder kunt u beveiligingsgroepen in- en uitsluiten om de inrichtingsconfiguratie van iOS-/iPadOS-apps toe te wijzen. U kunt bijvoorbeeld de inrichtingsconfiguratie van een iOS-/iPadOS-app aan Alle gebruikers toewijzen, maar een managementgroep uitsluiten.

## <a name="how-to-create-an-ios-mobile-app-provisioning-profile"></a>Een inrichtingsprofiel voor mobiele iOS-apps maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Inrichtingsprofielen voor iOS-apps** > **Profiel maken**.
3. Voeg op de pagina **Basisinformatie** de volgende waarden toe:
    - **Naam**: geef een naam op voor dit mobiele inrichtingsprofiel.
    - **Beschrijving**: geef indien gewenst een beschrijving op voor het beleid.
    - **Profielbestand uploaden**: kies het pictogram **Openen** en kies vervolgens een Apple-profielbestand voor mobiele configuratie (met de extensie `.mobileprovision`) dat u hebt gedownload van de [Apple-website voor ontwikkelaars](https://developer.apple.com/).

   De **Vervaldatum** wordt ingevuld op basis van een waarde in het bestand Apple-profiel voor mobiele configuratie dat u hierboven hebt toegevoegd.<br>

   <img alt="Create profile - Basics" src="./media/app-provisioning-profile-ios/app-provisioning-profile-ios-01.png">

4. Klik op **Volgende: Bereiktags**.<br>
   Op de pagina **Bereiktags** kunt u desgewenst bereiktags configureren om te bepalen wie het inrichtingsprofiel voor iOS-/iPadOS-apps in Intune kan zien. Zie [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Op rollen gebaseerd toegangsbeheer en bereiktags gebruiken voor gedistribueerde IT) voor meer informatie over bereiktags.
5. Klik op **Volgende: Toewijzingen**.<br>
   Op de pagina **Toewijzingen** kunt u het profiel toewijzen aan gebruikers en apparaten. Het is belangrijk dat u weet dat u een profiel kunt toewijzen aan een apparaat, ongeacht of het apparaat wordt beheerd in Intune.
6. Klik op **Volgende: beoordelen en maken** om de waarden te controleren die u hebt ingevoerd voor het profiel.
7. Wanneer u klaar bent, klikt u op **Maken** om het inrichtingsprofiel voor iOS-/iPadOS-apps in Intune te maken. 

## <a name="next-steps"></a>Volgende stappen

Wijs het profiel toe aan de vereiste iOS-/iPadOS-apparaten. Voor meer informatie gebruikt u de stappen in [Apparaatprofielen toewijzen](../configuration/device-profile-assign.md).

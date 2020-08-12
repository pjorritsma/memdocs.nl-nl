---
title: Meldingen over Configuration Manager-console
titleSuffix: Configuration Manager
description: Meer informatie over meldingen van de Configuration Manager-console.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0d709fa-c4f8-46e1-b432-582cc293be35
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12ec788fdf19ec72e954f5a9f229a5a3f95a4610
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129638"
---
# <a name="configuration-manager-console-notifications"></a>Meldingen over Configuration Manager-console

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3556016, fka 1318035-->
Vanaf Configuration Manager versie 1902 geeft de Configuration Manager-console u op de hoogte van specifieke gebeurtenissen die optreden. U kunt enkele gebeurtenis meldingen configureren voor uw Configuration Manager-sites.

- Niet-Configureer bare gebeurtenis meldingen:
   - Wanneer er een update beschikbaar is voor Configuration Manager zichzelf
   - Wanneer er levens cyclus-en onderhouds gebeurtenissen optreden in de omgeving
- Configureer bare gebeurtenis meldingen:
   - [Status wijzigingen niet-kritieke site](#bkmk_noncrit)
   - [Berichten van micro soft](#bkmk_msft) (vanaf versie 2006)

Deze melding is een balk boven aan het console venster onder het lint. De vorige ervaring wordt vervangen wanneer Configuration Manager updates beschikbaar zijn. In deze meldingen in de console worden nog steeds essentiële gegevens weer gegeven, maar uw werk in de console wordt niet verstoord. U kunt geen kritieke meldingen negeren. In de-console worden alle meldingen in een nieuw systeemvak van de titel balk weer gegeven.

![Meldings balk en vlag in console](./media/1318035-notify-eval-version-expired.png)

## <a name="configure-a-site-to-show-non-critical-notifications"></a><a name="bkmk_noncrit"></a>Een site configureren voor het weer geven van niet-kritieke meldingen

U kunt elke site zo configureren dat niet-kritieke meldingen worden weer gegeven in de eigenschappen van de site.

1. Vouw **site configuratie**uit in de werk ruimte **beheer** en selecteer vervolgens het knoop punt **sites** .
1. Selecteer de site die u wilt configureren voor niet-kritieke meldingen.
1. Selecteer **Eigenschappen**in het lint.
1. Selecteer op het tabblad **waarschuwingen** de optie om **console meldingen in te scha kelen voor niet-kritieke status wijzigingen van de site**.
   - Als u deze instelling inschakelt, zien alle console gebruikers essentiële, waarschuwings-en informatie meldingen. Deze instelling is standaard ingeschakeld.  
   - Als u deze instelling uitschakelt, bekijken console gebruikers alleen kritieke meldingen.  

De meeste console meldingen zijn per sessie. Query's worden geëvalueerd wanneer een gebruiker de console start. Start de console opnieuw om de wijzigingen in de meldingen te bekijken. Als een gebruiker een niet-kritieke melding heeft gesloten, wordt deze opnieuw weer gemeld wanneer de console opnieuw wordt opgestart als deze nog steeds van toepassing is.

De volgende meldingen worden elke vijf minuten opnieuw geëvalueerd:

- Site bevindt zich in onderhouds modus  
- Site bevindt zich in de herstel modus  
- De site bevindt zich in de upgrade modus  

Meldingen volgen de machtigingen voor beheer op basis van rollen. Als een gebruiker bijvoorbeeld geen machtigingen heeft om Configuration Manager updates te zien, worden deze meldingen niet weer geven.

Sommige meldingen hebben een gerelateerde actie. Als de-console versie bijvoorbeeld niet overeenkomt met de versie van de-site, selecteert u **de nieuwe console versie installeren**. Met deze actie wordt het installatie programma van de-console gestart.

Als u vanaf versie 2006 Azure-Services configureert om uw site te koppelen, worden er meldingen weer geven met een actie voor [het vernieuwen van de geheime sleutel](../deploy/configure/azure-services-wizard.md#bkmk_renew).<!--6386392--> De site evalueert eenmaal per uur de status van de volgende waarschuwingen:

- Een of meer geheime sleutels van de Azure AD-App verlopen binnenkort
- Een of meer geheime sleutels van Azure AD-app zijn verlopen

De volgende meldingen zijn het meest van toepassing op de Technical Preview-vertakking:  

- De evaluatie versie ligt binnen 30 dagen na verloop van tijd (waarschuwing): de huidige datum valt binnen 30 dagen na de verval datum van de evaluatie versie  
- De evaluatie versie is verlopen (kritiek): de huidige datum valt na de verval datum van de evaluatie versie  
- Niet-overeenkomende console versies (kritiek): de versie van de console komt niet overeen met de site versie  
- Site-upgrade is beschikbaar (waarschuwing): er is een nieuw update pakket beschikbaar  

Zie het bestand **SmsAdminUI. log** op de-console computer voor meer informatie en hulp bij het oplossen van problemen. Dit logboek bestand bevindt zich standaard op het volgende pad: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log` .

## <a name="configure-a-site-to-receive-messages-from-microsoft"></a><a name="bkmk_msft"></a>Een site configureren voor het ontvangen van berichten van micro soft
 <!--3953121-->

Vanaf versie 2006 kunt u meldingen van micro soft ontvangen in de Configuration Manager-console. Met deze meldingen kunt u op de hoogte blijven van nieuwe of bijgewerkte functies, wijzigingen in Configuration Manager en gekoppelde services, en problemen waarvoor actie moet worden doorgevoerd.

### <a name="configure-notification-settings-for-microsoft-messages"></a>Instellingen voor meldingen configureren voor micro soft-berichten

1. Ga naar **beheer**  >  **site configuratie**  >  **sites**.
1. Klik met de rechter muisknop op een site en selecteer **Eigenschappen**.
1. Schakel op het tabblad **waarschuwingen** de meldingen in door **berichten van micro soft ontvangen**te selecteren. U kunt de volgende meldingen uitschakelen als u deze liever niet wilt ontvangen:  
   - **Voor komen/oplossen**: bekende problemen die van invloed zijn op uw organisatie en waarvoor u mogelijk actie moet ondernemen.
   - **Plan voor wijziging**: wijzigingen in Configuration Manager waarvoor u mogelijk actie moet ondernemen.
   - **Blijf**op de hoogte: informeert u van nieuwe of bijgewerkte functies die beschikbaar zijn.

     [![Melding van micro soft-opties in de site-eigenschappen](./media/3953121-microsoft-notifications.png)](./media/3953121-microsoft-notifications.png#lightbox)



## <a name="next-steps"></a>Volgende stappen

- [De console gebruiken](admin-console.md)
- [Console tips](admin-console-tips.md)
- [Toegankelijkheidsfuncties](../../understand/accessibility-features.md)

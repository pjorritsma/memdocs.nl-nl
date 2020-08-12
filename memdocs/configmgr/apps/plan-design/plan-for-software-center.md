---
title: Software Center plannen
titleSuffix: Configuration Manager
description: Bepaal hoe u Software Center zo wilt configureren dat gebruikers met Configuration Manager kunnen communiceren.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b32fc2de3c945ff2292f119a10d84d982d08677
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127355"
---
# <a name="plan-for-software-center"></a>Software Center plannen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruikers kunnen instellingen wijzigen, zoeken naar toepassingen en toepassingen installeren vanuit software Center. Wanneer u de Configuration Manager-client op een Windows-apparaat installeert, wordt ook automatisch software center geïnstalleerd.

Zie de [Gebruikers handleiding voor Software Center](../../core/understand/software-center.md)voor meer informatie over de andere functies van software Center.  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a>Software Center configureren  

Werk uw Configuration Manager-sites en-clients bij naar versie 1906 of hoger om te profiteren van de nieuwste functies van software Center.

> [!IMPORTANT]
> Deze herhaalde verbeteringen voor Software Center en het beheer punt zijn het buiten gebruik stellen van de functies van de toepassings catalogus.
>
> - De Silverlight-gebruikers ervaring wordt niet ondersteund op de huidige branch-versie 1806.
> - Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren.
> - Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.

- De client instelling **Nieuw Software Center gebruiken** in de groep **computer agent** is standaard ingeschakeld. De vorige versie van software Center wordt niet meer ondersteund. Zie [verwijderde en afgeschafte functies](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.

- Geef de zicht baarheid van de Application catalog-website koppeling op het tabblad **installatie status** van software Center op. Zie client instellingen voor [Software Center](../../core/clients/deploy/about-client-settings.md#software-center) voor meer informatie.

- Vanaf versie 1906 kunt u Maxi maal vijf aangepaste tabbladen toevoegen aan software Center. Zie [client instellingen voor Software Center](../../core/clients/deploy/about-client-settings.md#software-center)voor meer informatie. <!--4063773-->

- Gebruikers kunnen affiniteit tussen gebruikers en apparaten configureren in Software Center. Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie.

> [!IMPORTANT]
> Als u gebruik wilt maken van nieuwe Configuration Manager functies, moet u clients eerst bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

### <a name="software-center-and-user-available-applications"></a>Software Center en gebruikers beschik bare toepassingen

- De functies van de toepassings catalogus zijn niet vereist voor het weer geven van gebruikers beschik bare toepassingen in Software Center. Dit gedrag helpt u de server infrastructuur te verminderen die nodig is voor het leveren van toepassingen aan gebruikers. Software Center is afhankelijk van het beheer punt om deze informatie te verkrijgen, waardoor grotere omgevingen beter kunnen worden geschaald door ze toe te wijzen aan [grens groepen](../../core/servers/deploy/configure/boundary-groups.md#management-points).<!--1358309-->

- Gebruikers kunnen door gebruikers beschik bare toepassingen zoeken en installeren op apparaten die zijn toegevoegd aan Azure Active Directory (Azure AD). Vanaf versie 2006 kunnen gebruikers apps die beschikbaar zijn op het internet en apparaten die lid zijn van een domein, ophalen. Zie voor meer informatie [gebruikers beschik bare toepassingen implementeren](../deploy-use/deploy-applications.md#deploy-user-available-applications).

- Vanaf versie 1906 communiceert Software Center met een beheer punt voor apps die zijn gericht op gebruikers als beschikbaar. De toepassings catalogus wordt niet meer gebruikt. Met deze wijziging wordt het voor u eenvoudiger om de toepassings catalogus uit de site te verwijderen.

- Voorheen heeft het Software Center het eerste beheer punt gekozen uit de lijst met beschik bare servers. Vanaf versie 1906 maakt het gebruik van hetzelfde beheer punt dat door de client wordt gebruikt. Met deze wijziging kan software center hetzelfde beheer punt van de toegewezen primaire site gebruiken als de client.

## <a name="replace-toast-notifications-with-dialog-window"></a><a name="bkmk_impact"></a>Pop-upmeldingen vervangen door dialoog venster

<!--3555947-->
Soms zien gebruikers de Windows-pop-upmelding over het opnieuw opstarten of de vereiste implementatie niet. De ervaring wordt dan niet weer geven om de herinnering af te stellen. Dit gedrag kan leiden tot een slechte gebruikers ervaring wanneer de client een deadline bereikt.

Vanaf versie 1902, wanneer er [software wijzigingen zijn vereist](#software-changes-are-required) of implementaties [opnieuw moeten worden opgestart](#restart-required), hebt u de mogelijkheid om een meer opvallend dialoog venster te gebruiken.

### <a name="software-changes-are-required"></a>Software wijzigingen zijn vereist

Wanneer u [een toepassing implementeert](../deploy-use/deploy-applications.md) zoals vereist met een deadline in de toekomst, selecteert u op de pagina **gebruikers ervaring** van de wizard software implementeren de volgende opties voor gebruikers meldingen:

- **Weer geven in Software Center en alle meldingen weer geven**
- **Wanneer er software wijzigingen zijn vereist, een dialoog venster weer geven voor de gebruiker in plaats van een pop-upmelding**

Als u deze implementatie-instelling configureert, wordt de gebruikers ervaring voor dit scenario gewijzigd.

Van de volgende pop-upmelding:

![Pop-upmelding dat software wijzigingen zijn vereist](media/3555947-required-toast.png)  

In het volgende dialoog venster:

![Dialoog venster voor vereiste software wijzigingen](media/3555947-required-dialog.png)


### <a name="restart-required"></a>Opnieuw opstarten is vereist

Schakel in de groep [computer opnieuw opstarten](../../core/clients/deploy/about-client-settings.md#computer-restart) van client instellingen de volgende optie in: **Wanneer een implementatie opnieuw moet worden opgestart, wordt een dialoog venster weer gegeven voor de gebruiker in plaats van een pop-upmelding**.  

Als u deze client instelling configureert, wordt de gebruikers ervaring voor alle vereiste implementaties gewijzigd waarvoor het opnieuw opstarten van de volgende typen is vereist:

- [Toepassing](../deploy-use/deploy-applications.md)
- [Takenreeks](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Software-update](../../sum/deploy-use/deploy-software-updates.md)

Van de volgende pop-upmelding:

![Pop-upmelding dat opnieuw opstarten is vereist](media/3555947-restart-toast.png)  

In het volgende dialoog venster:

![Dialoog venster om de computer opnieuw op te starten](media/3555947-restart-dialog.png)

> [!IMPORTANT]
> In Configuration Manager 1902 worden pop-upmeldingen in het dialoog venster niet vervangen. Om dit probleem op te lossen, installeert u het [Update pakket voor Configuration Manager versie 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="brand-software-center"></a>Merk Software Center

Wijzig de vormgeving van software Center om te voldoen aan de huismerk vereisten van uw organisatie. Deze configuratie helpt gebruikers bij het vertrouwen van software Center.

### <a name="configure-software-center-branding"></a>Branding voor Software Center configureren

<!-- 1351224 -->
Pas het uiterlijk van software Center aan door de huisstijl elementen van uw organisatie toe te voegen en de zicht baarheid van tabbladen op te geven.

Raadpleeg voor meer informatie de volgende artikelen:

- [Software Center](../../core/clients/deploy/about-client-settings.md#software-center) -groep van client instellingen  
- [Clientinstellingen configureren](../../core/clients/deploy/configure-client-settings.md)  

### <a name="branding-priorities"></a>Huismerk prioriteiten

Configuration Manager past aangepaste huis stijl voor Software Center toe aan de hand van de volgende prioriteiten:  

1. Client instellingen voor **Software Center** . Zie [over client instellingen](../../core/clients/deploy/about-client-settings.md#software-center)voor meer informatie.  

2. **Organisatie naam** client instelling in groep **computer agent** . Zie [over client instellingen](../../core/clients/deploy/about-client-settings.md#computer-agent)voor meer informatie.  

#### <a name="application-catalog-branding-priorities"></a>Prioriteiten voor toepassings catalogus huisstijl

> [!IMPORTANT]
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  

Als u de toepassings catalogus gebruikt, heeft het merk de volgende prioriteiten:  

1. Client instellingen voor **Software Center** . Zie [over client instellingen](../../core/clients/deploy/about-client-settings.md#software-center)voor meer informatie.  

2. De *naam* en *kleur* van de organisatie die u opgeeft in de eigenschappen van het Application catalog-website punt. Zie [configuratie opties voor Application catalog-website punt](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)voor meer informatie.  

3. **Organisatie naam** client instelling in groep **computer agent** . Zie [over client instellingen](../../core/clients/deploy/about-client-settings.md#computer-agent)voor meer informatie.  

## <a name="see-also"></a>Zie ook

- [Gebruikershandleiding van Software Center](../../core/understand/software-center.md)
- [Toepassingsbeheer plannen en configureren](plan-for-and-configure-application-management.md)

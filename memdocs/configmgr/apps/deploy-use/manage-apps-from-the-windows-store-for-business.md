---
title: Microsoft Store-apps
titleSuffix: Configuration Manager
description: Apps beheren en implementeren vanuit de Microsoft Store voor bedrijven en onderwijs met Configuration Manager.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d6a61324f8c777ba5ed09dd26816152d6f17af9
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643205"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-and-education-with-configuration-manager"></a>Apps beheren via de Microsoft Store voor bedrijven en onderwijs met Configuration Manager

De [Microsoft Store voor bedrijven en onderwijs](https://docs.microsoft.com/microsoft-store/) is waar u Windows-apps voor uw organisatie vindt en aanschaft. Wanneer u de Store verbindt met Configuration Manager, synchroniseert u vervolgens de lijst met apps die u hebt aangeschaft. Bekijk deze apps in de Configuration Manager-console en implementeer ze zoals u een andere app implementeert.

## <a name="online-and-offline-apps"></a><a name="bkmk_apps"></a>Online-en offline-Apps

De Microsoft Store voor bedrijven en onderwijs ondersteunt twee typen apps:

- **Online**: dit licentie type vereist gebruikers en apparaten om verbinding te maken met de Store om een app en de bijbehorende licentie te verkrijgen. Windows 10-apparaten moeten worden Azure Active Directory (Azure AD), gekoppeld aan of hybride Azure AD.  

- **Offline**: met dit type kunt u apps en licenties in de cache opslaan om deze rechtstreeks in uw on-premises netwerk te implementeren. Apparaten hoeven geen verbinding te maken met de Store of hebben geen verbinding met internet.

Zie voor meer informatie het [overzicht van Microsoft Store voor bedrijven en onderwijs](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview).

### <a name="summary-of-capabilities"></a>Samen vatting van mogelijkheden

Configuration Manager biedt ondersteuning voor het beheren van Microsoft Store voor zakelijke en onderwijs-apps op Windows 10-apparaten met de Configuration Manager-client en ook Windows 10-apparaten die zijn Inge schreven bij Microsoft Intune. Configuration Manager biedt de volgende mogelijkheden voor online-en offline-Apps:

|Mogelijkheid|Offline-Apps|Online-apps|
|------------|------------|------------|
|App-gegevens synchroniseren met Configuration Manager<br>(synchronisatie vindt elke 24 uur plaats)|Ja|Ja|
|Configuration Manager-toepassingen maken op basis van Store-apps|Ja|Ja|
|Ondersteuning voor gratis apps uit de Store|Ja|Ja|
|Ondersteuning voor betaalde apps uit de Store|Nee|Ja,<sup>[Opmerking 1](#bkmk_note1)</sup>|
|Ondersteuning voor vereiste implementaties voor gebruikers-of apparaat-verzamelingen|Ja|Ja|
|Beschik bare implementaties voor gebruikers-of apparaat-verzamelingen ondersteunen|Ja|Ja|
|Line-of-Business-Apps uit de Store ondersteunen|Ja|Ja|
|Een Store-app inrichten voor alle gebruikers op een apparaat<sup>[Opmerking 2](#bkmk_note2)</sup><!--1358310-->|Ja|Ja|

#### <a name="note-1-online-licensed-apps-version-requirement"></a><a name="bkmk_note1"></a>Opmerking 1: vereiste versie van online gelicentieerde apps

Als u apps met een online licentie wilt implementeren op Windows 10-apparaten met de Configuration Manager-client, moet Windows 10, versie 1703 of hoger worden uitgevoerd.  

#### <a name="note-2-configuration-manager-minimum-version"></a><a name="bkmk_note2"></a>Opmerking 2: minimale versie van Configuration Manager

Vanaf versie 1806. Zie [Windows-toepassingen maken](../get-started/creating-windows-applications.md#bkmk_provision)voor meer informatie.  

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-and-education-to-devices-that-run-the-configuration-manager-client"></a>Online Apps implementeren met behulp van de Microsoft Store voor bedrijven en onderwijs naar apparaten waarop de Configuration Manager-client wordt uitgevoerd

Houd rekening met de volgende punten voordat u Microsoft Store implementeert voor zakelijke en onderwijs-apps op apparaten die de volledige Configuration Manager-client uitvoeren:

- Voor volledige functionaliteit moeten op apparaten Windows 10, versie 1703 of hoger worden uitgevoerd.  

- Registreer of Voeg apparaten toe aan dezelfde Azure AD-Tenant waar u de Microsoft Store voor bedrijven en onderwijs hebt geregistreerd als een beheer programma.  

- Wanneer het lokale Administrator-account zich op het apparaat aanmeldt, heeft het geen toegang tot Microsoft Store voor zakelijke en onderwijs-apps.  

- Apparaten moeten een Live Internet verbinding hebben met de Microsoft Store voor bedrijven en onderwijs. Zie [vereisten](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business)voor meer informatie, waaronder proxy configuratie.  

### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Opmerkingen voor apparaten met eerdere versies van Windows 10

Op apparaten met de Configuration Manager-client en Windows 10 versie 1607 of eerder wordt uitgevoerd, geldt de volgende functionaliteit:  

Wanneer u de installatie van de app op het apparaat afdwingt met een van de volgende methoden:  

- De gebruiker installeert de app  

- De installatie deadline van de implementatie is bereikt

- Nieuwe evaluatie na de installatie voor vereiste implementaties  

Daarna gebeurt het volgende gedrag:  

- De Configuration Manager-client dwingt de app af door de Microsoft Store-app te starten  

- De gebruiker moet de installatie uit de Store volt ooien  

- In de Configuration Manager-console mislukt de implementatie status van de app met de volgende fout: "de Microsoft Store-app is geopend op de client-PC en wacht tot de gebruiker de installatie heeft voltooid."  

Bij de volgende evaluatie fase van de toepassing:  

- Als de gebruiker de toepassing uit de Store heeft geïnstalleerd, rapporteert de toepassing de status **geslaagd**  

- Als de gebruiker de app niet wil installeren vanuit de Store:  

  - Voor vereiste implementaties probeert de Configuration Manager-client de Store-app opnieuw te starten  

  - Beschik bare implementaties worden niet opnieuw afgedwongen Configuration Manager

#### <a name="devices-running-earlier-versions-of-windows-10"></a>Apparaten met eerdere versies van Windows 10

- U kunt geen line-of-Business-Apps implementeren vanuit het Microsoft Store voor bedrijven en onderwijs

- Wanneer u betaalde apps uit de Store implementeert, moeten gebruikers zich aanmelden bij de Store en de app zelf verkrijgen  

- Als u een groeps beleid implementeert om de toegang tot de consumenten versie van de Microsoft Store uit te scha kelen, werken implementaties van de Microsoft Store voor bedrijven en onderwijs niet. Dit gedrag treedt zelfs op als u de Microsoft Store voor bedrijven en onderwijs inschakelt.  

## <a name="set-up-synchronization"></a><a name="bkmk_setup"></a>Synchronisatie instellen

Wanneer u de lijst met Microsoft Store voor zakelijke en onderwijs-apps synchroniseert die uw organisatie heeft aangeschaft, ziet u deze apps in de Configuration Manager-console.

Verbind uw Configuration Manager-site met Azure AD en de Microsoft Store voor bedrijven en onderwijs. Zie [Azure-Services configureren](../../core/servers/deploy/configure/azure-services-wizard.md)voor meer informatie en Details van dit proces. Maak een verbinding met de service **Microsoft Store voor bedrijven** .

Zorg ervoor dat het service aansluitpunt en de doel apparaten toegang hebben tot de Cloud service. Zie [vereisten voor Microsoft Store voor zakelijke en onderwijs-proxy configuratie](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration)voor meer informatie.

### <a name="supplemental-information-and-configuration"></a><a name="bkmk_config"></a>Aanvullende informatie en configuratie

Configureer op de pagina **app** van de wizard Azure-Services eerst de **Azure-omgeving** en **Web-app**. Lees vervolgens de sectie **meer informatie** aan de onderkant van de pagina. Deze informatie bevat de volgende aanvullende acties in de Microsoft Store voor de Business-en Education-portal:  

- Configureer Configuration Manager als het hulp programma voor het beheer van opslag. Zie [Configure Management provider](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business)(Engelstalig) voor meer informatie.  

- Schakel ondersteuning voor offline gelicentieerde apps in. Zie voor meer informatie het [distribueren van offline-Apps](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).  

- U moet ten minste één app ophalen. Zie [apps zoeken en verkrijgen](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview)voor meer informatie.  

Geef op de pagina **configuratie** van de wizard Azure-Services de volgende informatie op:  

- **Pad naar Microsoft Store inhouds opslag voor zakelijke apps**: Geef een gedeeld netwerkpad op, inclusief een map. Bijvoorbeeld `\\server\share\folder`. Wanneer de site server met de Store synchroniseert, wordt de inhoud op deze locatie in de cache opgeslagen. Wanneer u een toepassing maakt in Configuration Manager, kopieert de site server de app-inhoud van deze lokale cache naar de inhouds bibliotheek van de site.  

- **Geselecteerde talen**: Selecteer de talen die u wilt synchroniseren uit de Store en weer geven voor gebruikers in Software Center. Als de gebruiker bijvoorbeeld Windows voor Duits configureert, worden in Software Center Duitse teken reeksen weer gegeven voor de Store-app. Voor dit gedrag moet de taal worden gesynchroniseerd en voor de specifieke toepassing bestaan.

- **Standaard taal**: als de taal van de gebruiker niet beschikbaar is, selecteert u de standaard taal die u wilt gebruiken.  

> [!NOTE]
> Configuration Manager synchroniseert het app-pictogram niet vanuit het archief. Als u een pictogram nodig hebt om weer te geven voor deze app in Software Center, voegt u dit hand matig toe in de app-eigenschappen. Zie [hand matig toepassings gegevens opgeven](create-applications.md#bkmk_manual-app)voor meer informatie.<!-- 2837053 -->

## <a name="create-and-deploy-the-app"></a><a name="bkmk_deploy"></a>De app maken en implementeren

Na de synchronisatie maakt en implementeert u de Microsoft Store voor zakelijke en onderwijs-apps die vergelijkbaar zijn met andere Configuration Manager toepassingen.

1. Vouw **toepassings beheer**uit in de werk ruimte **software bibliotheek** van de Configuration Manager-console en selecteer vervolgens het knoop punt **licentie-informatie voor Store-apps** .  

2. Kies de app die u wilt implementeren en selecteer vervolgens **toepassing maken** in het lint.  

Op de site wordt een Configuration Manager-toepassing gemaakt met de Microsoft Store voor zakelijke en onderwijs-apps.

Implementeer en bewaak vervolgens deze toepassing op dezelfde manier als andere Configuration Manager-toepassingen. Raadpleeg voor meer informatie de volgende artikelen:  

- [Toepassingen implementeren](deploy-applications.md)
- [Toepassingen bewaken vanaf de console](monitor-applications-from-the-console.md)

## <a name="next-steps"></a>Volgende stappen

Vouw in de werk ruimte **software bibliotheek** de optie **toepassings beheer**uit en selecteer vervolgens het knoop punt **licentie-informatie voor Store-apps** .

Voor elke Store-app die u beheert, bekijkt u de volgende informatie over de app:

- App-naam
- App-platform
- Het aantal licenties voor de app waarvan u de eigenaar bent
- Het aantal beschik bare licenties

Na de implementatie van online-apps, komen alle updates voor die app rechtstreeks van de Microsoft Store. Daarnaast controleert Configuration Manager niet de versie compatibiliteit van online apps, alleen dat Windows de app rapporteert als geïnstalleerd.  

Bij het implementeren van offline-Apps op Windows 10-apparaten met de Configuration Manager-client, mogen gebruikers geen toepassingen die extern kunnen worden bijgewerkt met Configuration Manager-implementaties. Het beheren van updates voor offline Apps is vooral belang rijk in omgevingen met meerdere gebruikers, zoals klas lokalen. Een optie om de Microsoft Store uit te scha kelen, is met behulp van [groeps beleid](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#block-microsoft-store-using-group-policy).

Nadat de Microsoft Store voor Business-en Education-beheerder een offline app heeft verkregen, publiceert u de app niet voor gebruikers via de Store. Deze configuratie zorgt ervoor dat gebruikers niet online kunnen installeren of bijwerken. Gebruikers ontvangen alleen offline-app-updates via Configuration Manager.

## <a name="see-also"></a>Zie tevens

[Problemen oplossen met de Microsoft Store voor zakelijke en onderwijs integratie met Configuration Manager](troubleshoot-microsoft-store-for-business-integration.md)

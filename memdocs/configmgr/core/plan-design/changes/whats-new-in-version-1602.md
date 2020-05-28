---
title: Nieuw in versie 1602
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1602 van Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 2e398795a14f5073141f103d93ccd82e61d4d7a8
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904900"
---
# <a name="what39s-new-in-version-1602-of-configuration-manager"></a>Wat&#39;s nieuw in versie 1602 van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*


Update 1602 voor Configuration Manager is alleen beschikbaar als een update in de console voor eerder geïnstalleerde sites waarop versie 1511 wordt uitgevoerd. Versie 1511 is de initiële basis versie die u gebruikt om nieuwe Configuration Manager-sites te installeren.  


> [!TIP]  
> Meer informatie over:  
>   
> - [Nieuwe sites installeren](../../servers/deploy/install/prepare-to-install-sites.md) (met een basislijn versie zoals 1511)  
> - [Updates installeren op sites](../../servers/manage/updates.md) (zoals update 1602)  

 De volgende secties bevatten informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1602 van Configuration Manager.  

## <a name="site-infrastructure"></a>Site-infra structuur  

###  <a name="in-place-upgrade-the-operating-system-of-site-servers-that-run-windows-server-2008-r2"></a><a name="bkmk_UpgradeOS"></a>In-place upgrade uitvoeren van het besturings systeem van site servers waarop Windows Server 2008 R2 wordt uitgevoerd  
 Configuration Manager sites waarop versie 1602 of hoger wordt uitgevoerd, ondersteunen de in-place upgrade van het besturings systeem site servers van Windows Server 2008 R2 naar Windows Server 2012 R2.  

> [!WARNING]  
>  Voordat u de upgrade naar Windows Server 2012 R2 uitvoert, dient u WSUS 3.2 te verwijderen van de server.  
>   
>  Zie de sectie nieuwe en gewijzigde functionaliteit in [Windows Server Update Services overzicht](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality)voor meer informatie over deze kritieke stap.  

 Als u een server wilt bijwerken, gebruikt u de upgrade procedures voor Windows Server 2012 R2. U hoeft na de upgrade geen Configuration Manager site server-herstel uit te voeren. Zie [Upgradeopties voor Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11)) in de Windows Server-documentatie voor de upgradeprocedures.  

###  <a name="sql-server-alwayson-availability-groups"></a><a name="bkmk_AOAG"></a>SQL Server AlwaysOn-beschikbaarheids groepen  
 Gebruik SQL Server AlwaysOn-beschikbaarheids groepen voor het hosten van de site database op primaire sites en de centrale beheer site als oplossing voor hoge Beschik baarheid en herstel na nood gevallen.  

 Zie [SQL Server AlwaysOn voor een Maxi maal beschik bare site database voor Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)voor meer informatie.  

## <a name="operating-system-deployment"></a>Implementatie van besturingssystemen  

### <a name="windows-10-servicing"></a>Onderhoud van Windows 10  
 De volgende verbeteringen voor onderhoud van Windows 10 zijn toegevoegd in Configuration Manager versie 1602:  

-   Er zijn nieuwe filter opties beschikbaar voor onderhouds plannen waarmee u kunt filteren op **taal**, **vereist**en **titel**. Alleen de upgrades die voldoen aan de opgegeven criteria worden aan de gekoppelde implementatie toegevoegd.  

-   Wanneer u de classificatie **upgrades** voor software-update synchronisatie selecteert, wordt er een waarschuwing weer gegeven. Deze waarschuwing laat u weten dat [hotfix 3095113](https://support.microsoft.com/kb/3095113) voor Windows Server Update Services (WSUS) 4,0 is vereist voordat u software-updates kunt synchroniseren, en dat Windows 10-onderhoud goed werkt. Vanuit het waarschuwings bericht gaat u naar het bijbehorende Knowledge Base-artikel.  

-   Beschik bare Windows 10-upgrades worden nu alleen weer gegeven in het knoop punt Windows 10- **onderhoud**  \  **alle updates van Windows** 10 van de Configuration Manager-console. Deze updates worden niet meer weer gegeven in het knoop punt **Software**-updates voor software-updates  \  **All Software Updates** van de-console.  

-   Een onderhouds plan wordt beschouwd als een implementatie met een hoog risico en het venster **verzameling selecteren** bevat alleen de aangepaste verzamelingen die voldoen aan de verificatie-instellingen voor de implementatie die zijn geconfigureerd in de eigenschappen van de site. Zie [instellingen voor het beheren van implementaties met een hoog risico voor Configuration Manager](../../servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.  

-   Gebruikers die een Windows 10-upgrade pakket starten, ontvangen nu een bericht dat ze een upgrade van het besturings systeem uitvoeren.  

## <a name="application-management"></a>Toepassingsbeheer  

### <a name="ios-app-configuration-policies"></a>Configuratiebeleidsregels voor IOS-apps  
 Gebruik Configuration Manager app-configuratie beleidsregels om instellingen op te geven die mogelijk vereist zijn wanneer de gebruiker een iOS-app uitvoert. Een app kan bijvoorbeeld vereisen dat de gebruiker een aangepast poort nummer, taal, beveiligings instellingen of huisstijl instellingen (zoals een bedrijfs logo) moet opgeven. Als deze instellingen onjuist zijn ingevoerd, kan dit de belasting van uw Help Desk verhogen en ook de acceptatie van nieuwe apps vertragen.  

 Het app-configuratie beleid kan u helpen deze problemen te elimineren door deze instellingen te implementeren voor gebruikers in een beleid, voordat ze de app uitvoeren. De instellingen worden vervolgens automatisch aangeleverd en de gebruiker hoeft geen actie te ondernemen.

### <a name="manage-volume-purchased-ios-apps"></a>iOS-apps beheren die zijn gekocht via het volume-aankoopprogramma  
 Met Configuration Manager kunt u apps implementeren en beheren die u via het volume-aankoop programma (VPP) van Apple hebt aangeschaft. Configuration Manager de licentie gegevens uit de App Store te importeren en houdt bij hoeveel licenties u hebt gebruikt.  


### <a name="automatic-creation-of-office-mobile-apps"></a>Automatisch maken van mobiele Office-apps  
 Wanneer u updatet naar versie 1602 van 1511, maakt Configuration Manager automatisch de volgende Microsoft Office Mobile-Apps voor Android en iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Micro soft OneNote (alleen iOS)  

-   Microsoft Outlook  

Deze apps vindt u in het knoop punt **toepassingen** van de Configuration Manager-console.  

 Zie [toepassingen implementeren met Configuration Manager](../../../apps/deploy-use/deploy-applications.md)voor meer informatie over het implementeren van toepassingen.  

## <a name="software-updates"></a>Software-updates  

### <a name="manage-office-365-client-updates"></a>Office 365-client updates beheren  
 Configuration Manager beschikt over de mogelijkheid om Office 365-client updates te beheren met behulp van de software-update beheer werk stroom. Zie [Office 365 ProPlus-updates beheren met Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md)voor meer informatie.  

## <a name="compliance-settings"></a>Instellingen voor naleving  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Nalevings instellingen voor apparaten met Windows 10 team  
 Er zijn nieuwe instellingen toegevoegd aan het configuratie-item **windows 8,1 en Windows 10** . Met deze instellingen kunt u apparaten beheren waarop Windows 10 team wordt uitgevoerd, zoals een Surface Hub apparaat.  

 Zie [configuratie-items maken voor windows 8,1-en Windows 10-apparaten die worden beheerd zonder de Configuration Manager-client](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)voor meer informatie.  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Kiosk modus instellingen voor Android Samsung KNOX Standard-apparaten  
 In de kiosk modus kunt u een apparaat zodanig vergren delen dat alleen bepaalde functies werken. U kunt bijvoorbeeld toestaan dat een apparaat slechts één beheerde app uitvoert die u opgeeft, of kunt u de volumeknoppen op een apparaat uitschakelen. Deze instellingen kunnen worden gebruikt voor een demonstratiemodel van een apparaat of voor een apparaat dat is toegewezen aan slechts één functie, zoals een verkooppuntapparaat. In Configuration Manager kunt u nu instellingen voor de kiosk modus opgeven voor Samsung KNOX Standard-apparaten.  


## <a name="conditional-access"></a>Voorwaardelijke toegang  

### <a name="conditional-access-for-pcs-managed-by-configuration-manager"></a>Voorwaardelijke toegang voor Pc's die worden beheerd door Configuration Manager  
 Voor het instellen van voorwaardelijke toegang voor een PC met de voor gaande versie moest de PC worden inge schreven bij intune of moet deze een PC zijn die lid is van een domein. Vanaf de 1602-update wordt voorwaardelijke toegang ondersteund voor Pc's die worden beheerd door Configuration Manager. Voor uw Pc's die worden beheerd door Configuration Manager, kunt u de toegang tot Exchange Online en share point online beperken tot apparaten die voldoen aan het nalevings beleid dat u hebt ingesteld.  


### <a name="restricting-access-based-on-the-health-of-devices"></a>Toegang beperken op basis van de status van apparaten  
 U kunt de toegang tot e-mail en Office 365-Services nu beperken op basis van de status van de apparaten, zoals gerapporteerd door de Health Attestation-service. Daarnaast worden apparaten die door intune worden beheerd, opgenomen in de status rapporten van het apparaat.  

 De Configuration Manager-console bevat een nieuwe nalevings regel waarmee u kunt opgeven of de apparaten toegang moeten krijgen of moeten worden geblokkeerd op basis van hun status. Zie [Health Attestation voor Configuration Manager](../../../core/servers/manage/health-attestation.md)voor meer informatie over Health Attestation-service en hoe de status van apparaten in intune wordt gerapporteerd.  

### <a name="new-compliance-policy-rules"></a>Nieuwe regels voor nalevings beleid  
 Nieuwe regels voor nalevings beleid, zoals automatische updates en het vereisen van een wacht woord voor het ontgrendelen van apparaten, zijn toegevoegd ter ondersteuning van betere beveiligings vereisten.


### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Zorg ervoor dat Inge schreven en compatibele apparaten altijd toegang hebben tot Exchange on-premises  
 Wanneer u de volgende optie inschakelt, krijgen apparaten die zijn Inge schreven bij intune en voldoen aan het nalevings beleid, toegang tot Exchange on-premises: **standaard regel negeren-apparaten die zijn Inge schreven bij intune, altijd toegang tot Exchange on-premises toestaan:**. Deze regel is beschikbaar op de **pagina Algemeen** van de **wizard beleid voor voorwaardelijke toegang configureren** voor Exchange on-premises.

 Met deze regel wordt de standaard regel overschreven, wat betekent dat zelfs als u de standaard regel instelt op quarantaine of toegang blokkeert, Inge schreven en compatibele apparaten nog steeds toegang hebben tot Exchange on-premises. Gebruik deze instelling als u wilt dat Inge schreven en compatibele apparaten altijd toegang hebben tot e-mail via Exchange on-premises.   

 Zie [toegang tot E-mail beheren](../../../mdm/understand/what-happened-to-hybrid.md)voor een gedetailleerd overzicht.  

## <a name="client-management"></a>Clientbeheer  

### <a name="client-online-status"></a>Onlinestatus van clients  
 Er is een nieuwe status voor clients beschikbaar om te controleren of een computer online is of niet. Een computer wordt als online beschouwd als deze is verbonden met het toegewezen beheer punt. Om aan te geven dat de computer online is, verzendt de client ping-achtige berichten naar het beheer punt. Als het beheer punt na vijf minuten geen bericht heeft ontvangen, wordt de client als offline beschouwd.  

 Zie [clients controleren](../../../core/clients/manage/monitor-clients.md)voor meer informatie.  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>PC-computer-en gebruikers beleid vernieuwen vanuit software Center  
 Er is een nieuwe optie, **synchronisatie beleid**toegevoegd aan de pagina **Opties**  >  **computer onderhoud** van software Center dat ervoor zorgt dat de PC het Configuration Manager computer-en gebruikers beleid vernieuwd.  

### <a name="software-center-branding-changes"></a>Huismerk wijzigingen voor Software Center  
 U kunt de kleur, de organisatie naam en het pictogram wijzigen die worden weer gegeven in Software Center. Deze instellingen worden toegepast op basis van de volgende regels:  

- Als de site serverrol toepassingscatalogus website punt niet is geïnstalleerd, wordt in Software Center de naam van de organisatie weer gegeven die is opgegeven in de **computer agent** -client instelling naam **van de organisatie in Software Center**.  

- Als de site serverrol toepassingscatalogus website punt is geïnstalleerd, wordt in Software Center de naam en kleur van de organisatie weer gegeven die zijn opgegeven in de eigenschappen van de site serverrol toepassingscatalogus website punt.  

- Als een Microsoft Intune-abonnement is geconfigureerd en verbonden met de Configuration Manager omgeving, worden in Software Center de naam van de organisatie, de kleur en het bedrijfs logo weer gegeven die zijn opgegeven in de eigenschappen van het intune-abonnement.  

### <a name="health-attestation"></a>Status verklaring  
 Beheerders kunnen de status van Windows 10 Health Attestation van apparaten bekijken in de Configuration Manager-console. Dit is beschikbaar voor Configuration Manager en Configuration Manager met Microsoft Intune. Met Health Attestation van apparaten kan de beheerder ervoor zorgen dat clientcomputers over de volgende betrouwbare configuraties van BIOS, TPM en opstartsoftware beschikken:  

-   Vroegtijdig starten van anti-malware  

-   BitLocker  

-   Secure Boot  

-   Code-integriteit  

Zie [Health Attestation voor Configuration Manager](../../../core/servers/manage/health-attestation.md)voor meer informatie.  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Verbeteringen aan Endpoint Protection antimalware-instellingen  
 1602 voegt de volgende nieuwe instellingen toe aan Endpoint Protection antimalware-beleid voor Windows Defender:  

-   Real-time beveiliging: tijdens het downloaden kunnen mogelijk ongewenste toepassingen worden geblokkeerd vóór de installatie.  

-   Scan instellingen: toegewezen netwerk stations scannen tijdens een volledige scan.  

-   Instellingen voor automatisch verzenden van voorbeeld bestanden:  

     De antimalware-engine kan aanvragen dat bestands voorbeelden naar micro soft worden verzonden voor verdere analyse. Standaard wordt altijd om bevestiging gevraagd voordat dergelijke voorbeeldbestanden worden verzonden. Beheerders kunnen nu de volgende instellingen beheren om dit gedrag te configureren:  

    -   Geavanceerd: automatisch verzenden van voorbeeld bestanden inschakelen zodat micro soft kan bepalen of bepaalde gedetecteerde items kwaad aardig zijn.  

    -   Geavanceerd: Hiermee staat u gebruikers toe automatische instellingen voor het verzenden van voorbeeld bestanden te wijzigen.  

    Daarnaast kunt u in de sectie uitsluitings instellingen van het antimalwarebeleid van Endpoint Protection de bestaande instelling **bestanden en mappen uitsluiten** nu uitsluitingen van apparaten toestaan.  

Zie [antimalware-beleid voor Endpoint Protection maken en implementeren](../../../protect/deploy-use/endpoint-antimalware-policies.md)voor meer informatie.  

## <a name="mobile-device-management"></a>Beheer van mobiele apparaten  

### <a name="ios-activation-lock"></a>iOS-Activeringsslot  
 Configuration Manager kan u helpen bij het beheren van iOS-Activeringsslot, een functie van de app zoek mijn iPhone voor iOS 7,1 en hoger. Activeringsvergrendeling is automatisch ingeschakeld wanneer de app Zoek mijn iPhone op een apparaat wordt gebruikt. Nadat de vergrendeling is ingeschakeld, moeten de Apple ID en het wachtwoord van de gebruiker worden ingevoerd voordat een van de volgende handelingen kan worden verricht:  

-   Zoek mijn iPhone uitschakelen.  

-   Het apparaat wissen.  

-   Activeer het apparaat opnieuw.  

Configuration Manager kunt de Activeringsslot status van apparaten onder Super visie en niet-super visie aanvragen waarop iOS 7,1 of hoger wordt uitgevoerd. Voor apparaten onder Super visie kan Configuration Manager de Activeringsslot bypass-code ophalen en deze rechtstreeks aan het apparaat verlenen.  

### <a name="monitor-terms-and-conditions-deployments"></a>Implementaties van voor waarden bewaken  
 U kunt implementaties voor voor waarden bewaken in de Configuration Manager-console.  

 Selecteer de implementatie van voor waarden in de lijst met implementaties. In het gebied samen vatting worden de volgende statistieken weer gegeven:  

-   **Compatibel**: gebruikers hebben de nieuwste versie van de voor waarden geaccepteerd.  

-   **Fout**  

-   Niet- **compatibel**: gebruikers hebben een versie van de voor waarden geaccepteerd, maar niet de meest recente versie.  

-   **Onbekend**: gebruikers hebben de voor waarden nooit geaccepteerd, inclusief verbindingen zonder Inge schreven apparaat.  

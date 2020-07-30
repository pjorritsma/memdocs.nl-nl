---
title: Clientinstellingen
titleSuffix: Configuration Manager
description: Meer informatie over de standaard-en aangepaste instellingen voor het beheren van client gedrag
ms.date: 07/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f6bb29930a6e2d4faf4ffdd141d3c9cd1831305
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365505"
---
# <a name="about-client-settings-in-configuration-manager"></a>Over client instellingen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Beheer alle client instellingen in de Configuration Manager-console vanuit het knoop punt **client instellingen** in de werk ruimte **beheer** . Configuration Manager wordt geleverd met een set standaard instellingen. Wanneer u de standaard instellingen van de client wijzigt, worden deze instellingen toegepast op alle clients in de hiërarchie. U kunt ook aangepaste client instellingen configureren, waardoor de standaard client instellingen worden overschreven wanneer u deze toewijst aan verzamelingen. Zie [client instellingen configureren](configure-client-settings.md)voor meer informatie.

In de volgende secties worden de instellingen en opties in meer detail beschreven.  


## <a name="background-intelligent-transfer-service-bits"></a>Background Intelligent Transfer Service (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Beperk de maximale netwerkbandbreedte voor BITS-overdrachten op de achtergrond

Als deze optie **Ja**is, gebruiken clients bits-bandbreedte beperking. Als u de andere instellingen in deze groep wilt configureren, moet u deze instelling inschakelen.

### <a name="throttling-window-start-time"></a>Begintijd beperkingsvenster

Geef de lokale start tijd voor het venster BITS-beperking op.  

### <a name="throttling-window-end-time"></a>Eindtijd beperkingsvenster

Geef de lokale eind tijd op voor het BITS-beperkings venster. Als de eind tijd gelijk is aan de **begin tijd van het beperkings venster**, is bits-beperking altijd ingeschakeld.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Maximale overdrachtssnelheid tijdens het beperkingsvenster (Kbps)

Geef de maximale overdrachts frequentie op die clients tijdens het venster kunnen gebruiken.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>BITS-downloads buiten het beperkingsvenster toestaan

Clients toestaan om afzonderlijke BITS-instellingen buiten het opgegeven venster te gebruiken.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Maximale overdrachtssnelheid buiten het beperkingsvenster (Kbps)

Geef de maximale overdrachts snelheid op die clients buiten het BITS-beperkings venster kunnen gebruiken.  



## <a name="client-cache-settings"></a>Client cache-instellingen

### <a name="configure-branchcache"></a>BranchCache configureren

Stel de client computer voor [Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
)in. Als u BranchCache-caching wilt toestaan op de client, stelt u **BranchCache inschakelen** in op **Ja**.

- **BranchCache inschakelen**: Hiermee schakelt u BranchCache in op client computers.

- **Maximale cache grootte van BranchCache (percentage van de schijf)**: het percentage van de schijf dat door BranchCache mag worden gebruikt.

> [!TIP]
> Als u **BranchCache configureren** instelt op **Nee**, worden in Configuration Manager geen BranchCache-instellingen geconfigureerd.
>
> Als u BranchCache wilt uitschakelen, stelt u **BranchCache configureren** in op **Ja**en stelt u **BranchCache** in op **Nee**.<!-- 6244852 -->

### <a name="configure-client-cache-size"></a>Client cache grootte configureren

De Configuration Manager-client cache op Windows-computers slaat tijdelijke bestanden op die worden gebruikt voor het installeren van toepassingen en Program ma's. Als deze optie is ingesteld op **Nee**, is de standaard grootte 5.120 MB.

Als u **Ja**kiest, geeft u het volgende op:

- **Maximale cache grootte (MB)**
- **Maximale cache grootte (percentage van schijf)**: de cache grootte van de client wordt uitgebreid naar de maximale grootte in mega bytes (MB) of het percentage van de schijf, afhankelijk van wat kleiner is.

### <a name="enable-as-peer-cache-source"></a>Inschakelen als peer-cache-bron

> [!Note]  
> In versie 1902 en eerder is deze instelling de naam **enable Configuration Manager client in volledig besturings systeem om inhoud te delen**. Het gedrag van de instelling is niet gewijzigd.

Hiermee wordt [peer-cache](../../plan-design/hierarchy/client-peer-cache.md) voor Configuration Manager-clients ingeschakeld. Kies **Ja**en geef vervolgens de poort op waarmee de client communiceert met de peer-computer.

- **Poort voor eerste netwerk uitzending** (standaard UDP 8004): Configuration Manager gebruikt deze poort in Windows PE of het volledige Windows-besturings systeem. De taken reeks engine in Windows PE verzendt de broadcast om inhouds locaties op te halen voordat de taken reeks wordt gestart.<!--SCCMDocs issue 910-->

- **Poort voor downloaden van inhoud van peer** (standaard TCP 8003): Configuration Manager configureert automatisch Windows Firewall regels om dit verkeer toe te staan. Als u een andere firewall gebruikt, moet u de regels hand matig configureren om dit verkeer toe te staan.  

    Zie [poorten die worden gebruikt voor verbindingen](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp)voor meer informatie.  

### <a name="minimum-duration-before-cached-content-can-be-removed-minutes"></a>Minimale duur voordat inhoud in de cache kan worden verwijderd (minuten)

<!--4485509-->
Vanaf versie 1906 geeft u de minimum tijd op voor de Configuration Manager-client om inhoud in de cache te blijven gebruiken. Deze client instelling definieert de minimale hoeveelheid tijd Configuration Manager agent moet wachten voordat de inhoud uit de cache kan worden verwijderd in het geval dat er meer ruimte nodig is.

Deze waarde is standaard 1.440 minuten (24 uur).
De maximum waarde voor deze instelling is 10.080 minuten (één week).

Deze instelling geeft u meer controle over de client cache op verschillende typen apparaten. U kunt de waarde verlagen op clients met kleine harde schijven en geen bestaande inhoud behoud voordat een andere implementatie wordt uitgevoerd.


## <a name="client-policy"></a>Client beleid  

### <a name="client-policy-polling-interval-minutes"></a>Pollinginterval voor clientbeleid (minuten)

Hiermee geeft u op hoe vaak de volgende Configuration Manager-clients client beleid downloaden:

- Windows-computers (bijvoorbeeld desktops, servers, laptops)  
- Mobiele apparaten die Configuration Manager inschrijven  
- Mac-computers  
- Computers met Linux of UNIX  

Deze waarde is standaard 60 minuten. Door deze waarde te verlagen, kunnen clients de site vaker controleren. Bij veel clients kan dit gedrag een negatieve invloed hebben op de prestaties van de site. De [richt lijnen voor grootte en schaal](../../plan-design/configs/size-and-scale-numbers.md) zijn gebaseerd op de standaard waarde. Het verhogen van deze waarde zorgt ervoor dat clients de site minder vaak kunnen navragen. Wijzigingen in het client beleid, met inbegrip van nieuwe implementaties, nemen clients langer in gebruik om deze te downloaden en te verwerken.<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>Gebruikers beleid op clients inschakelen

Wanneer u deze optie instelt op **Ja**en [gebruikers detectie](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)gebruikt, ontvangen clients toepassingen en Program ma's die zijn gericht op de aangemelde gebruiker.  

Als deze instelling **Nee**is, ontvangen gebruikers geen vereiste toepassingen die u voor gebruikers implementeert. Gebruikers ontvangen ook geen andere beheer taken in gebruikers beleid.  

Deze instelling geldt voor gebruikers wanneer hun computer zich op het intranet of Internet bevindt. Het moet **Ja** zijn als u ook gebruikers beleid wilt inschakelen op internet.  

> [!Note]  
> Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt geen nieuwe functies van de toepassings catalogus installeren.
>
> Als u nog steeds de Application Catalog gebruikt, ontvangt deze de lijst met beschik bare software voor gebruikers van de site server. Deze instelling hoeft dus niet te zijn ingesteld op **Ja** voor gebruikers om toepassingen uit de Application Catalog te bekijken en aan te vragen. Als deze instelling niet is ingesteld op **Nee**, kunnen gebruikers de toepassingen die ze in de toepassings catalogus zien, niet installeren.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Gebruikers beleids aanvragen van internetclients inschakelen

Stel deze optie in op **Ja** als u wilt dat gebruikers het gebruikers beleid op internet computers ontvangen. De volgende vereisten zijn ook van toepassing:  

- De client en site zijn geconfigureerd voor [client beheer op Internet](../manage/plan-internet-based-client-management.md) of een [Cloud beheer gateway](../manage/cmg/plan-cloud-management-gateway.md).  

- De instelling **gebruikers beleid op clients inschakelen** is **Ja**.  

- Het beheer punt op Internet verifieert de gebruiker met behulp van Windows-verificatie (Kerberos of NTLM). Zie [overwegingen voor client communicatie via internet](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)voor meer informatie.  

- De Cloud beheer gateway verifieert de gebruiker met behulp van Azure Active Directory. Zie voor meer informatie [gebruikers beschik bare toepassingen implementeren op apparaten die zijn toegevoegd aan Azure AD](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).  

Als u deze optie instelt op **Nee**, of als aan een van de vorige vereisten niet wordt voldaan, ontvangt een computer op internet alleen computer beleid. In dit scenario kunnen gebruikers nog steeds toepassingen zien, aanvragen en installeren vanuit een toepassings catalogus op internet. Als deze instelling **Nee**is, maar **gebruikers beleid op clients inschakelen** is **Ja**, worden gebruikers geen gebruikers beleid ontvangen totdat de computer is verbonden met het intranet.  

> [!NOTE]  
> Voor client beheer op basis van Internet is voor goedkeurings aanvragen voor toepassingen van gebruikers geen gebruikers beleid of gebruikers verificatie vereist. De Cloud beheer gateway ondersteunt geen aanvragen voor het goed keuren van toepassingen.  

### <a name="enable-user-policy-for-multiple-user-sessions"></a>Gebruikers beleid voor meerdere gebruikers sessies inschakelen

<!--4737447-->

*Van toepassing op versie 1910*

Deze instelling is standaard uitgeschakeld. Zelfs als u gebruikers beleid inschakelt, vanaf versie 1906 wordt deze door de client standaard uitgeschakeld op een apparaat dat meerdere gelijktijdige actieve gebruikers sessies toestaat. Bijvoorbeeld Terminal servers of Windows 10 Enter prise meerdere sessies in [Windows virtueel bureau blad](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

De client schakelt het gebruikers beleid alleen uit wanneer dit type apparaat wordt gedetecteerd tijdens een nieuwe installatie. Het vorige gedrag blijft bestaan voor een bestaande client van dit type die u bijwerkt naar versie 1906 of hoger. Op een bestaand apparaat wordt de instelling voor gebruikers beleid geconfigureerd, zelfs als deze detecteert dat het apparaat meerdere gebruikers sessies toestaat.

Als u in dit scenario gebruikers beleid nodig hebt en mogelijke prestatie problemen wilt accepteren, schakelt u deze client instelling in.


## <a name="cloud-services"></a>Cloud services

### <a name="allow-access-to-cloud-distribution-point"></a>Toegang tot Cloud distributiepunt toestaan

Stel deze optie in op **Ja** als u wilt dat clients inhoud ophalen van een Cloud distributiepunt. Deze instelling vereist niet dat het apparaat op internet is gebaseerd.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Automatisch nieuwe aan Windows 10-domein gekoppelde apparaten registreren met Azure Active Directory

Wanneer u Azure Active Directory configureert ter ondersteuning van hybride deelname, Configuration Manager Windows 10-apparaten configureren voor deze functionaliteit. Zie [Configure hybrid Azure Active Directory joind devices](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)(Engelstalig) voor meer informatie.

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Clients inschakelen om een Cloud beheer gateway te gebruiken

Standaard gebruiken alle clients voor Internet-roaming alle beschik bare [Cloud beheer gateway](../manage/cmg/plan-cloud-management-gateway.md). Een voor beeld van het configureren van deze instelling op **Nee** is het bereiken van het gebruik van de service, zoals tijdens een proef project of het besparen van kosten.



## <a name="compliance-settings"></a>Instellingen voor naleving  

### <a name="enable-compliance-evaluation-on-clients"></a>Compatibiliteitsevaluatie op clients toestaan

Stel deze optie in op **Ja** om de andere instellingen in deze groep te configureren.

### <a name="schedule-compliance-evaluation"></a>Compatibiliteitsevaluatie plannen

Selecteer **planning** om de standaard planning voor implementaties van configuratie basislijn te maken. Deze waarde kan voor elke basis lijn worden geconfigureerd in het dialoog venster **configuratie basislijn implementeren** .  

### <a name="enable-user-data-and-profiles"></a>Gebruikersgegevens en -profielen inschakelen

Kies **Ja** als u configuratie-items voor [gebruikers gegevens en-profielen](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) wilt implementeren.



## <a name="computer-agent"></a>Computer agent  

### <a name="user-notifications-for-required-deployments"></a>Gebruikers meldingen voor vereiste implementaties

Zie [gebruikers meldingen voor vereiste implementaties](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)voor meer informatie over de volgende drie instellingen:

- **Implementatie deadline langer dan 24 uur, gebruiker herinneren elke (uur)**
- **Deadline voor implementatie minder dan 24 uur, gebruiker herinneren elke (uur)**
- **Deadline voor implementatie minder dan 1 uur, gebruiker herinneren elke (minuten)**

### <a name="default-application-catalog-website-point"></a>Standaard Application Catalog-websitepunt

> [!Important]  
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Configuration Manager gebruikt deze instelling om gebruikers te verbinden met de Application Catalog vanuit software Center. Selecteer **website instellen** om een server op te geven die als host fungeert voor het Application catalog-website punt. Voer de NetBIOS-naam of FQDN in, geef automatische detectie op of geef een URL op voor aangepaste implementaties. In de meeste gevallen is automatische detectie de beste keuze.

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Voeg de standaard Application Catalog-website toe aan de zone met vertrouwde sites in Internet Explorer

> [!Important]  
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Als deze optie is ingesteld op **Ja**, wordt de huidige standaard Application catalog-website-URL automatisch toegevoegd aan de zone met vertrouwde websites van Internet Explorer.  

Deze instelling zorgt ervoor dat de instelling Internet Explorer voor de beveiligde modus niet is ingeschakeld. Als de beveiligde modus is ingeschakeld, kan de Configuration Manager-client mogelijk geen toepassingen uit de Application Catalog installeren. Standaard ondersteunt de zone met vertrouwde sites ook gebruikers aanmelding voor de Application Catalog, waarvoor Windows-verificatie is vereist.  

Als u deze optie **niet**opgeeft, kunnen Configuration Manager-clients mogelijk geen toepassingen uit de Application Catalog installeren. Een alternatieve methode is het configureren van deze instellingen voor Internet Explorer in een andere zone voor de Application Catalog-URL die clients gebruiken.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Toestaan dat Silverlight-toepassingen worden uitgevoerd in verhoogde vertrouwensmodus

> [!Important]  
> Silverlight wordt niet automatisch geïnstalleerd door de client.
>
> Vanaf versie 1806 wordt de **Silverlight-gebruikers ervaring** voor het Application catalog-website punt niet meer ondersteund. Gebruikers moeten het nieuwe software Center gebruiken. Zie [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)voor meer informatie.  

Deze instelling moet **Ja** zijn als u wilt dat gebruikers de Application Catalog gebruiken.  

Als u deze instelling wijzigt, wordt deze van kracht wanneer gebruikers de browser vervolgens laden of het geopende browser venster vernieuwen.  

Zie [certificaten voor micro soft Silverlight 5 en verhoogde vertrouwens modus vereist voor de Application Catalog](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5)voor meer informatie over deze instelling.  

### <a name="organization-name-displayed-in-software-center"></a>Weergegeven organisatienaam in Software Center

Typ de naam die wordt weergegeven in Software Center. Deze huismerkgegevens helpen gebruikers om deze toepassing als een vertrouwde bron te identificeren. Zie [huismerk Software Center](../../../apps/plan-design/plan-for-software-center.md#branding-software-center)(Engelstalig) voor meer informatie over de prioriteit van deze instelling.  

### <a name="use-new-software-center"></a>Het nieuwe Software Center gebruiken

De standaard instelling is **Ja**.

Wanneer u deze optie instelt op **Ja**, gebruiken alle client computers het Software Center. Software Center toont software, software-updates en taken reeksen die u implementeert voor gebruikers of apparaten.

### <a name="enable-communication-with-health-attestation-service"></a>Communicatie met de Health Attestation-service inschakelen

Stel deze optie in op **Ja** voor Windows 10-apparaten voor het gebruik van [Health Attestation](../../servers/manage/health-attestation.md). Wanneer u deze instelling inschakelt, is de volgende instelling ook beschikbaar voor configuratie.

### <a name="use-on-premises-health-attestation-service"></a>On-premises Health Attestation-service gebruiken

Stel deze optie in op **Ja** als u wilt dat apparaten een on-premises service gebruiken. Ingesteld op **Nee** voor apparaten om de micro soft-Cloud service te gebruiken.  

### <a name="install-permissions"></a>Installatiemachtigingen

Configureren hoe gebruikers software, software-updates en taken reeksen kunnen installeren:  

- **Alle gebruikers**: gebruikers met toestemming, behalve gast.  

- **Alleen beheerders**: gebruikers moeten lid zijn van de lokale groep Administrators.  

- **Alleen beheerders en primaire gebruikers**: gebruikers moeten lid zijn van de lokale groep Administrators of een primaire gebruiker van de computer zijn.  

- **Geen gebruikers**: geen gebruikers die zijn aangemeld op een client computer, kunnen software, software-updates en taken reeksen installeren. Vereiste implementaties voor de computer worden altijd op de deadline geïnstalleerd. Gebruikers kunnen software niet installeren vanuit software Center.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Invoer BitLocker-pincode opschorten bij opnieuw opstarten

Als voor computers BitLocker-pincode vereist is, wordt met deze optie niet de vereiste om een pincode in te voeren wanneer de computer opnieuw wordt opgestart na een software-installatie.  

- **Always**: Configuration Manager BitLocker wordt tijdelijk onderbroken nadat het software heeft geïnstalleerd waarvoor opnieuw moet worden opgestart en de computer opnieuw wordt opgestart. Deze instelling is alleen van toepassing wanneer Configuration Manager de computer opnieuw opstart. Met deze instelling wordt de vereiste voor het invoeren van de BitLocker-pincode niet opgeschort wanneer de gebruiker de computer opnieuw opstart. De BitLocker pincode entry-vereiste wordt hervat na het opstarten van Windows.

- **Nooit**: Configuration Manager BitLocker niet wordt onderbroken nadat het software heeft geïnstalleerd waarvoor opnieuw moet worden opgestart. In dit scenario kan de software-installatie niet worden voltooid totdat de gebruiker de pincode heeft ingevoerd om het standaard opstart proces te volt ooien en Windows te laden.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>Aanvullende software beheert de implementatie van toepassingen en software-updates

Schakel deze optie alleen in als een van de volgende voor waarden van toepassing is:  

- U gebruikt een leveranciersoplossing waarvoor deze instelling moet worden ingeschakeld.  

- U gebruikt de Configuration Manager Software Development Kit (SDK) om meldingen van de client agent en de installatie van toepassingen en software-updates te beheren.  

> [!WARNING]  
> - Als u deze optie kiest wanneer geen van deze voor waarden van toepassing is, installeert de client software-updates en vereiste toepassingen niet. Met deze instelling wordt niet voor komen dat gebruikers beschik bare software vanuit software Center installeren, met inbegrip van toepassingen, pakketten en taken reeksen.  
> -  Wanneer u deze instelling inschakelt, worden pop-upmeldingen voor nieuwe software of vereiste software niet uitgevoerd op clients. <!--6347668-->

### <a name="powershell-execution-policy"></a>PowerShell-uitvoeringsbeleid

Configureren hoe Configuration Manager-clients Windows Power shell-scripts kunnen uitvoeren. U kunt deze scripts gebruiken voor detectie in configuratie-items voor compatibiliteits instellingen. U kunt de scripts in een implementatie ook verzenden als een standaard script.  

- **Bypass**: de Configuration Manager-client omzeilt de Windows Power shell-configuratie op de client computer zodat niet-ondertekende scripts kunnen worden uitgevoerd.  

- **Beperkt**: de Configuration Manager-client gebruikt de huidige Power shell-configuratie op de client computer. Deze configuratie bepaalt of niet-ondertekende scripts kunnen worden uitgevoerd.  

- **Alle ondertekende**: de Configuration Manager-client voert alleen scripts uit als een vertrouwde uitgever deze heeft ondertekend. Deze beperking is van toepassing onafhankelijk van de huidige Power shell-configuratie op de client computer.  

Deze optie vereist ten minste Windows Power shell-versie 2,0. De standaard instelling is **alle ondertekende**.  

> [!TIP]  
> Als niet-ondertekende scripts niet kunnen worden uitgevoerd vanwege deze client instelling, wordt deze fout door Configuration Manager op de volgende manieren gerapporteerd:  
>
> - In de werk ruimte **bewaking** in de-console wordt de implementatie status fout-id **0x87D00327**weer gegeven. Ook het script voor de beschrijving wordt weer gegeven **, is niet ondertekend**.  
> - In rapporten wordt de fout type **detectie fout**weer gegeven. Vervolgens worden rapporten weer gegeven met de fout code **0x87D00327** en wordt het script van de beschrijving **niet ondertekend**, of is de fout code **0X87D00320** en de beschrijving **die de scripthost nog niet is geïnstalleerd**. Een voor beeld van een rapport is: **Details van fouten van configuratie-items in een configuratie basislijn voor een Asset**.  
> - In het bestand **DcmWmiProvider. log** wordt het bericht **script niet ondertekend (fout: 87D00327; Bron: CCM)**.  

### <a name="show-notifications-for-new-deployments"></a>Meldingen weergeven voor nieuwe implementaties

Kies **Ja** om een melding weer te geven voor implementaties die minder dan een week beschikbaar zijn. Dit bericht wordt weer gegeven wanneer de client agent wordt gestart.

### <a name="disable-deadline-randomization"></a>Willekeurig toepassen van deadline uitschakelen

Na de deadline van de implementatie bepaalt deze instelling of de client een activerings vertraging van Maxi maal twee uur gebruikt om de vereiste software-updates te installeren. De vertraging is standaard uitgeschakeld.  

Voor VDI (Virtual Desktop Infrastructure)-scenario's helpt deze vertraging de CPU-verwerking en gegevens overdracht te distribueren voor een hostcomputer met meerdere virtuele machines. Zelfs als u geen VDI gebruikt, kan het CPU-gebruik op de site server negatief worden door veel clients tegelijk te installeren. Dit gedrag kan ook de distributie punten vertragen en de beschik bare netwerk bandbreedte aanzienlijk verminderen.  

Als clients de vereiste software-updates zonder vertraging moeten installeren tijdens de implementatie deadline, configureert u deze instelling in **Ja**.

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Respijt periode voor afdwingen na de deadline van de implementatie (uren)

Als u gebruikers meer tijd wilt geven om de vereiste implementaties van software-updates na de deadline te installeren, stelt u een waarde in voor deze optie. Deze respijt periode is voor een lange periode uitgeschakeld voor een computer en de gebruiker moet een groot aantal toepassings-of update-implementaties installeren. Deze instelling is bijvoorbeeld handig als een gebruiker van vakantie terugkeert en gedurende een lange periode moet wachten terwijl de client achterstallige toepassings implementaties installeert.

Stel een respijt periode van 0 tot 120 uur in. Gebruik deze instelling samen met de implementatie-eigenschap **vertraging afdwingen van deze implementatie op basis van gebruikers voorkeuren**. Zie [toepassingen implementeren](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period)voor meer informatie.


### <a name="enable-endpoint-analytics-data-collection"></a>Endpoint Analytics-gegevens verzameling inschakelen

Hiermee wordt het verzamelen van lokale gegevens op de client ingeschakeld voor upload naar endpoint Analytics. Ingesteld op **Ja** om apparaten te configureren voor het verzamelen van lokale gegevens. Ingesteld op **Nee** om het verzamelen van lokale gegevens uit te scha kelen. Zie [Configuration Manager apparaten inschrijven bij Endpoint Analytics](../../../../analytics/enroll-configmgr.md)voor meer informatie.

## <a name="computer-restart"></a>Computer opnieuw opstarten

Zie meldingen over het [opnieuw opstarten van apparaten](device-restart-notifications.md)voor meer informatie over deze instellingen.<!-- 7182335 -->

## <a name="delivery-optimization"></a>Delivery optimization

<!-- 1324696 -->
U gebruikt Configuration Manager grens groepen om de distributie van inhoud in uw bedrijfs netwerk en externe kant oren te definiëren en te reguleren. [Windows Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) is een op de cloud gebaseerde peer-to-peer-technologie voor het delen van inhoud tussen Windows 10-apparaten. Configureer Delivery Optimization om uw grens groepen te gebruiken bij het delen van inhoud tussen peers.

> [!Note]
> - Delivery Optimization is alleen beschikbaar op Windows 10-clients.
> - Internet toegang tot de Cloud service voor leverings optimalisatie is een vereiste voor het gebruik van de peer-to-peer-functionaliteit. Zie [Veelgestelde vragen over Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)voor meer informatie over de benodigde Internet-eind punten.
> - Wanneer u een CMG gebruikt voor de opslag van inhoud, worden de inhoud voor updates van derden niet gedownload naar clients als de instelling **Delta-inhoud downloaden wanneer de beschik bare** [client](#allow-clients-to-download-delta-content-when-available) is ingeschakeld. <!--6598587--> 

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>Configuration Manager grens groepen gebruiken voor de ID van de leverings optimalisatie groep

Kies **Ja** om de grens groep-ID toe te passen als de id van de leverings optimalisatie groep op de client. Wanneer de client communiceert met de Delivery Optimization-Cloud service, wordt deze id gebruikt om peers te zoeken met de inhoud. Als u deze instelling inschakelt, wordt ook de download modus voor de leverings optimalisatie ingesteld op de groep (2) op de doel clients.

> [!Note]
> Micro soft raadt aan de client in staat te stellen deze instelling te configureren via lokaal beleid in plaats van met groeps beleid. Hierdoor kan de grens groep-ID worden ingesteld als de id van de bezorgings optimalisatie groep op de client. Zie [Delivery Optimization](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)voor meer informatie.

### <a name="enable-devices-managed-by-configuration-manager-to-use-microsoft-connected-cache-servers-for-content-download"></a>Apparaten die worden beheerd door Configuration Manager inschakelen voor het gebruik van micro soft Connected cache servers voor het downloaden van inhoud

<!--3555764-->
Kies **Ja** om clients toe te staan inhoud te downloaden van een on-premises distributie punt dat u inschakelt als een micro soft-verbonden cache server. Zie voor meer informatie [micro soft Connected cache in Configuration Manager](../../plan-design/hierarchy/microsoft-connected-cache.md).


## <a name="endpoint-protection"></a>Endpoint Protection

> [!Tip]
> Naast de volgende informatie vindt u in voorbeeld scenario informatie over het gebruik van Endpoint Protection-client instellingen [: het gebruik van Endpoint Protection om computers te beveiligen tegen malware](../../../protect/deploy-use/scenarios-endpoint-protection.md).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Endpoint Protection-client op client computers beheren

Kies **Ja** als u bestaande Endpoint Protection-en Windows Defender-clients wilt beheren op computers in uw-hiërarchie.  

Kies deze optie als u de Endpoint Protection-client al hebt geïnstalleerd en deze wilt beheren met Configuration Manager. Deze afzonderlijke installatie bevat een script proces dat gebruikmaakt van een Configuration Manager toepassing of pakket en programma. Voor Windows 10-apparaten hoeft de Endpoint Protection-agent niet te zijn geïnstalleerd. Op deze apparaten moet echter nog steeds **Endpoint Protection-client worden beheerd op client computers** ingeschakeld. <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>Endpoint Protection-client op clientcomputers installeren

Kies **Ja** om de Endpoint Protection-client te installeren en in te scha kelen op client computers waarop de-client nog niet wordt uitgevoerd. Voor Windows 10-clients hoeft de Endpoint Protection-agent niet te zijn geïnstalleerd.  

> [!NOTE]  
> Als de Endpoint Protection-client al is geïnstalleerd, kiest u **Nee** om de Endpoint Protection-client niet te verwijderen. Als u de Endpoint Protection-client wilt verwijderen, stelt u de client instelling **Endpoint Protection-client op client computers beheren** in op **Nee**. Implementeer vervolgens een pakket en programma om de Endpoint Protection-client te verwijderen.  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Endpoint Protection-client installatie toestaan en opnieuw opstarten buiten onderhouds Vensters. Onderhouds Vensters moeten ten minste 30 minuten lang zijn voor client installatie

Stel deze optie in op **Ja** als u het normale installatie gedrag wilt vervangen door onderhouds Vensters. Deze instelling voldoet aan de bedrijfs vereisten voor de prioriteit van systeem onderhoud ten behoeve van de beveiliging.

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Voor Windows Embedded-apparaten met schrijf filters, door voeren Endpoint Protection-client installatie (opnieuw opstarten nood zakelijk)

Kies **Ja** om het schrijf filter op het Windows Embedded-apparaat uit te scha kelen en start het apparaat opnieuw op. Met deze actie wordt de installatie op het apparaat doorgevoerd.  

Als u **Nee**kiest, wordt de client geïnstalleerd op een tijdelijke overlay die wordt gewist wanneer het apparaat opnieuw wordt opgestart. In dit scenario wordt de Endpoint Protection-client pas volledig geïnstalleerd wanneer een andere installatie wijzigingen doorvoert op het apparaat. Deze configuratie is de standaard instelling.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Verplicht opnieuw opstarten van de computer onderdrukken nadat de Endpoint Protection-client is geïnstalleerd

Kies **Ja** om te onderdrukken dat de computer opnieuw wordt opgestart nadat de Endpoint Protection-client is geïnstalleerd.  

> [!IMPORTANT]  
> Als de Endpoint Protection-client vereist dat de computer opnieuw wordt opgestart en deze instelling **Nee**is, wordt de computer opnieuw opgestart, ongeacht het geconfigureerde onderhouds venster.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>De toegestane periode waarmee gebruikers een vereiste herstart kunnen uitstellen om de Endpoint Protection-installatie te volt ooien (uur)

Als een herstart nodig is nadat de Endpoint Protection-client is geïnstalleerd, wordt met deze instelling het aantal uren aangegeven dat gebruikers de vereiste herstart kunnen uitstellen. Deze instelling vereist dat u de volgende instelling uitschakelt: de **vereiste herstart van de computer onderdrukken nadat de Endpoint Protection-client is geïnstalleerd**.

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Alternatieve bronnen uitschakelen (zoals micro soft Windows Update, micro soft Windows Server Update Services of UNC-shares) voor de eerste definitie-update op client computers

Kies **Ja** als u wilt dat Configuration Manager alleen de initiële definitie-update op client computers installeert. Deze instelling kan nuttig zijn om onnodige netwerk verbindingen te voor komen en de netwerk bandbreedte te verminderen tijdens de eerste installatie van de definitie-update.  



## <a name="enrollment"></a>Inschrijving

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Polling-interval voor verouderde clients voor mobiele apparaten

Selecteer **interval instellen** om de tijds duur, in minuten of uren, op te geven dat verouderde mobiele apparaten moeten worden gecontroleerd op beleid. Deze apparaten zijn onder andere platforms als Windows CE, macOS en UNIX of Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Polling-interval voor moderne apparaten (minuten)

Voer het aantal minuten in dat moderne apparaten de poll voor het beleid controleren. Deze instelling is voor Windows 10-apparaten die worden beheerd via on-premises Mobile Device Management.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Gebruikers toestaan mobiele apparaten en Mac-computers te registreren

Stel deze optie in op **Ja**en configureer de volgende instelling om op de gebruiker gebaseerde inschrijving van verouderde apparaten in te scha kelen:

- **Inschrijvings profiel**: Selecteer **profiel instellen** om een inschrijvings profiel te maken of te selecteren. Zie [client instellingen voor inschrijving configureren](deploy-clients-to-macs.md#configure-client-settings)voor meer informatie.

### <a name="allow-users-to-enroll-modern-devices"></a>Gebruikers toestaan moderne apparaten te registreren

Als u moderne apparaten op basis van de gebruiker wilt inschrijven, stelt u deze optie in op **Ja**en configureert u de volgende instelling:

- **Inschrijvings profiel voor modern apparaat**: Selecteer **profiel instellen** om een inschrijvings profiel te maken of te selecteren. Zie [een inschrijvings profiel maken waarmee gebruikers moderne apparaten kunnen registreren](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf)voor meer informatie.



## <a name="hardware-inventory"></a>Hardware-inventaris  

### <a name="enable-hardware-inventory-on-clients"></a>Hardware-inventaris op clients inschakelen

Deze instelling is standaard **Ja**. Zie [Inleiding op Hardware-inventarisatie](../manage/inventory/introduction-to-hardware-inventory.md)voor meer informatie.

### <a name="hardware-inventory-schedule"></a>Planning hardware-inventaris

Selecteer **schema** om de frequentie aan te passen waarmee clients de hardware-inventarisatie fase uitvoeren. Deze cyclus wordt standaard elke zeven dagen uitgevoerd.

### <a name="maximum-random-delay-minutes"></a>Maximale wille keurige vertraging (minuten)

Geef het maximum aantal minuten op dat de Configuration Manager-client de hardware-inventarisatie fase vanuit het gedefinieerde schema mag verwillen. Deze wille keurige tussen client helpt de belasting van de inventaris verwerking op de site server te verdelen. U kunt een waarde tussen 0 en 480 minuten opgeven. Deze waarde is standaard ingesteld op 240 minuten (4 uur).

### <a name="maximum-custom-mif-file-size-kb"></a>Maximale grootte aangepast MIF-bestand (KB)

Geef de maximale grootte, in kilo bytes (KB), op die is toegestaan voor elk aangepaste Management Information Format (MIF)-bestand dat door de client wordt verzameld tijdens een hardware-inventarisatie fase. De Configuration Manager hardware-inventaris agent verwerkt geen aangepaste MIF-bestanden die deze grootte overschrijden. U kunt een grootte van 1 KB instellen op 5.120 KB. Deze waarde is standaard ingesteld op 250 KB. Deze instelling heeft geen invloed op de grootte van het normale hardware-inventaris gegevensbestand.  

> [!NOTE]  
> Deze instelling is alleen beschikbaar in de standaard instellingen van de client.  

### <a name="hardware-inventory-classes"></a>Hardware-inventarisklassen

Selecteer **klassen instellen** om de hardware-informatie uit te breiden die u verzamelt van clients zonder het sms_def. MOF-bestand hand matig te bewerken. Zie [hardware-inventaris configureren](../manage/inventory/configure-hardware-inventory.md)voor meer informatie.  

### <a name="collect-mif-files"></a>MIF-bestanden verzamelen

Gebruik deze instelling om op te geven of u MIF-bestanden wilt verzamelen van Configuration Manager-clients tijdens de hardware-inventarisatie.  

Voor een MIF-bestand dat door hardware-inventaris wordt verzameld, moet het op de juiste locatie op de client computer zijn. De bestanden bevinden zich standaard in de volgende paden:  

- **IDMIF-bestanden** moeten zich in de map map windows\system32\ccm\inventory\idmif. bevindt.

- **NOIDMIF-bestanden** moeten zich in de map map windows\system32\ccm\inventory\noidmif. bevindt.

> [!NOTE]  
> Deze instelling is alleen beschikbaar in de standaard instellingen van de client.



## <a name="metered-internet-connections"></a>Internet verbindingen naar gebruik  

Beheren hoe Internet verbindingen met een Data limiet worden gebruikt voor computers met Windows 8 en hoger om met Configuration Manager te communiceren. Internet providers worden soms kosten in rekening gebracht op basis van de hoeveelheid gegevens die u verzendt en ontvangt wanneer u gebruikmaakt van een Internet verbinding met data limiet.  

> [!NOTE]  
> De geconfigureerde client instelling wordt niet toegepast in de volgende scenario's:  
>
> - Als de computer zich op een zwervende gegevens verbinding bevindt, voert de Configuration Manager-client geen taken uit waarvoor gegevens moeten worden overgedragen naar Configuration Manager-sites.  
> - Als de eigenschappen van de Windows-netwerk verbinding zijn geconfigureerd als niet-data limiet, gedraagt de Configuration Manager-client zich alsof de verbinding niet-data limiet is en worden gegevens overgedragen naar de site.  

### <a name="client-communication-on-metered-internet-connections"></a>Client communicatie via Internet verbindingen met data limiet

Kies een van de volgende opties voor deze instelling:  

- **Toestaan**: alle client communicatie is toegestaan via de Internet verbinding naar gebruik, tenzij het client apparaat een zwervende gegevens verbinding gebruikt.  

- **Limiet**: alleen de volgende client communicatie is toegestaan via de Internet verbinding met data limiet:  

    - Clientbeleid ophalen  

    - Clientstatusberichten om te verzenden naar de site  

    - Software-installatie aanvragen van software Center  

    - Vereiste implementaties (zodra de installatiedeadline wordt bereikt)  

    Als de client de limiet voor gegevens overdracht voor de Internet verbinding met data limiet bereikt, probeert de client niet langer te communiceren met Configuration Manager-sites.  

- **Blok keren**: de Configuration Manager-client probeert niet te communiceren met Configuration Manager-sites wanneer deze zich op een Internet verbinding met data limiet bevinden. Dit is de standaardoptie.  

> [!IMPORTANT]  
> De client staat altijd software-installaties toe vanuit software Center, ongeacht de instellingen voor de Internet verbinding met data limiet. Als de gebruiker een software-installatie aanvraagt terwijl het apparaat zich op een netwerk met data limiet bevindt, wordt het doel van de gebruiker door het Software Center gerespecteerd.<!-- MEMDocs#285 -->


## <a name="power-management"></a>Energiebeheer  

### <a name="allow-power-management-of-devices"></a>Energie beheer van apparaten toestaan

Stel deze optie in op **Ja** om energie beheer in te scha kelen op clients. Zie [Introduction to Power Management](../manage/power/introduction-to-power-management.md)(Engelstalig) voor meer informatie.

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Toestaan dat gebruikers hun apparaat uit energiebeheer uitsluiten

Kies **Ja** om gebruikers van software Center hun computer te laten uitsluiten van de geconfigureerde Energiebeheer instellingen.  

### <a name="allow-network-wake-up"></a>Wake-up van netwerk toestaan

Wanneer u deze instelling inschakelt, configureert de client de energie-instellingen op de computer zodat de netwerk adapter het apparaat kan activeren. Als u deze instelling uitschakelt, kan de netwerk adapter van de computer het apparaat niet meer activeren.

### <a name="enable-wake-up-proxy"></a>Wake-up proxy inschakelen

Geef **Ja** op als aanvulling op de instelling van de site Wake on LAN, wanneer deze is geconfigureerd voor unicast pakketten.  

Zie [plan How to wake up clients](plan/plan-wake-up-clients.md)(Engelstalig) voor meer informatie over Wake-up proxy.  

> [!WARNING]  
> Schakel Wake-up proxy niet in een productie netwerk in zonder eerst te weten hoe het werkt en het te evalueren in een test omgeving.  

Configureer vervolgens de volgende extra instellingen, indien nodig:

- **Poort nummer Wake-up proxy (UDP)**: het poort nummer dat clients gebruiken om Ontwaak pakketten te verzenden naar slapende computers. Behoud de standaard poort 25536 of wijzig het getal in een waarde van uw keuze.  

- **Wake on LAN poort nummer (UDP)**: behoud de standaard waarde van 9, tenzij u het poort nummer van de Wake on LAN (UDP) hebt gewijzigd op het tabblad **poorten** van de site- **Eigenschappen**.  

    > [!IMPORTANT]  
    > Dit nummer moet overeenkomen met het nummer in de **Eigenschappen**van de site. Als u dit aantal op één plek wijzigt, wordt het niet automatisch bijgewerkt op de andere locatie.  

- **Windows Defender firewall-uitzonde ring voor wake-up proxy**: de Configuration Manager-client configureert automatisch het poort nummer van de Wake-up proxy op apparaten waarop Windows Defender firewall wordt uitgevoerd. Selecteer **configureren** om de Firewall profielen op te geven.  

    Als clients een andere firewall uitvoeren, moet u deze hand matig configureren zodat het **poort nummer van de Wake-up proxy (UDP)** wordt toegestaan.  

- **IPv6-voor voegsels, indien nodig voor DirectAccess of andere tussenliggende netwerk apparaten. Gebruik een komma om meerdere vermeldingen op te geven**: Voer de benodigde IPv6-voor voegsels voor wake-up proxy in op uw netwerk.



## <a name="remote-tools"></a>Externe hulpprogramma's  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Beheer op afstand inschakelen op clients en firewall-uitzonderings profielen

Selecteer **configureren** om de functie beheer op afstand van Configuration Manager in te scha kelen. Optioneel kunt u Firewall instellingen configureren zodat extern beheer op client computers kan worden uitgevoerd.  

Beheer op afstand is standaard uitgeschakeld.  

> [!IMPORTANT]  
> Als u de firewall instellingen niet configureert, werkt beheer op afstand mogelijk niet goed.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Gebruikers kunnen instellingen voor beleid of meldingen in Software Center wijzigen

Kies of gebruikers opties voor beheer op afstand kunnen wijzigen vanuit software Center.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Extern beheer van een onbeheerde computer toestaan

Kies of een beheerder Extern beheer kan gebruiken om toegang te krijgen tot een client computer die is afgemeld of vergrendeld. Alleen een aangemelde en niet-vergrendelde computer kunnen op afstand worden beheerd als deze instelling is uitgeschakeld.  

### <a name="prompt-user-for-remote-control-permission"></a>Gebruiker vragen naar machtiging voor beheer op afstand

Kies of op de client computer een bericht wordt weer gegeven dat de gebruiker om toestemming wordt gevraagd voordat een sessie voor beheer op afstand wordt toegestaan.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Gebruiker vragen om toestemming voor het overdragen van inhoud van het gedeelde klem bord

Voordat u inhoud overbrengt van het gedeelde klem bord in een sessie voor beheer op afstand, kunnen gebruikers de mogelijkheid hebben om bestands overdrachten te accepteren of te weigeren. Gebruikers hoeven slechts eenmaal per sessie toestemming te verlenen. De Viewer kan zelf geen toestemming geven om het bestand over te dragen.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Machtigingen voor beheer op afstand toekennen aan lokale groep beheerders

Kies of lokale beheerders op de server die de verbinding voor beheer op afstand starten, extern beheer van sessies tot client computers kunnen maken.  

### <a name="access-level-allowed"></a>Toegestaan toegangsniveau

Geef het niveau van de toegang tot beheer op afstand voor toestaan. Kies een van de volgende instellingen:  

- **Geen toegang**
- **Alleen weer geven**
- **Volledig beheer**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Toegestane viewers van beheer op afstand en hulp op afstand

Selecteer **viewers instellen** om de namen op te geven van de Windows-gebruikers die extern beheer sessies kunnen tot stand brengen op client computers.  

### <a name="show-session-notification-icon-on-taskbar"></a>Sessiemeldingspictogram weergeven op de taakbalk

Stel deze instelling in op **Ja** om een pictogram weer te geven op de Windows-taak balk van de client om een actieve sessie voor beheer op afstand aan te duiden.  

### <a name="show-session-connection-bar"></a>Sessieverbindingsbalk weergeven

Stel deze optie in op **Ja** om een sessie met een hoge zicht baarheid van sessies weer te geven op clients om een actieve sessie voor beheer op afstand aan te duiden.  

### <a name="play-a-sound-on-client"></a>Een geluid afspelen op client

Stel deze optie in om geluid te gebruiken om aan te geven wanneer een sessie voor beheer op afstand actief is op een client computer. Selecteer één van de volgende opties:

- **Geen geluid**
- **Begin en einde van de sessie** (standaard)
- **Herhaaldelijk tijdens sessie**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Instellingen voor ongevraagde hulp op afstand beheren

Stel deze instelling in op **Ja** om ongevraagde externe hulp sessies Configuration Manager te beheren.  

In een ongevraagde sessie van hulp op afstand heeft de gebruiker op de client computer geen hulp aangevraagd voor het starten van de sessie.  

### <a name="manage-solicited-remote-assistance-settings"></a>Instellingen voor gevraagde hulp op afstand beheren

Stel deze optie in op **Ja** om de aangevraagde sessies voor hulp op afstand Configuration Manager te laten beheren.  

In een aangevraagde sessie voor hulp op afstand heeft de gebruiker op de client computer een aanvraag voor hulp op afstand verzonden naar de beheerder.  

### <a name="level-of-access-for-remote-assistance"></a>Toegangsniveau voor hulp op afstand

Kies het toegangs niveau dat u wilt toewijzen aan sessies voor hulp op afstand die worden gestart in de Configuration Manager-console. Selecteer één van de volgende opties:

- **Geen** (standaard)
- **Externe weer gave**
- **Volledig beheer**

> [!NOTE]  
> De gebruiker op de clientcomputer moet altijd toegang verlenen opdat een externe hulpsessie zou kunnen plaatsvinden.  

### <a name="manage-remote-desktop-settings"></a>Instellingen voor extern bureaublad beheren

Stel deze optie in op **Ja** als u extern bureaublad-sessies voor computers wilt Configuration Manager beheren.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Toegelaten viewers toestaan om verbinding te maken via externe bureaublad-verbinding

Stel deze optie in op **Ja** als u gebruikers die zijn opgegeven in de lijst met toegestane viewer wilt toevoegen aan de Extern bureaublad lokale gebruikers groep op clients.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Eis verificatie op netwerkniveau op computers die het besturingssysteem Windows Vista en latere versies uitvoeren.

Stel deze optie in op **Ja** als u verificatie op netwerk niveau (NLA) wilt gebruiken om extern bureaublad verbindingen met client computers tot stand te brengen. NLA vereist voor het eerst minder bronnen voor externe computers, omdat de verificatie van de gebruiker is voltooid voordat een Extern bureaublad verbinding tot stand wordt gebracht. Het gebruik van NLA is een veiligere configuratie. NLA helpt de computer te beschermen tegen kwaadwillende gebruikers of software, en Hiermee wordt het risico op denial-of-service-aanvallen verminderd.  



## <a name="software-center"></a>Software Center

### <a name="select-these-new-settings-to-specify-company-information"></a>Selecteer deze nieuwe instellingen om bedrijfs gegevens op te geven

Stel deze optie in op **Ja**en geef de volgende instellingen op voor het logo Software Center voor uw organisatie:

- **Bedrijfs naam**: Voer de naam in van de organisatie die gebruikers zien in Software Center.  

- **Kleuren schema voor Software Center**: Klik op **kleur selecteren** om de primaire kleur te definiëren die wordt gebruikt door Software Center.  

- **Selecteer een logo voor Software Center**: Klik op **Bladeren** om een installatie kopie te selecteren die u wilt weer geven in Software Center. Het logo moet een JPEG, PNG of BMP van 400 x 100 pixels zijn, met een maximale grootte van 750 KB. De naam van het logo bestand mag geen spaties bevatten.  

### <a name="hide-unapproved-applications-in-software-center"></a><a name="bkmk_HideUnapproved"></a>Niet-goedgekeurde toepassingen verbergen in Software Center

Wanneer u deze optie inschakelt, worden gebruikers beschik bare toepassingen die goed keuring vereisen, verborgen in Software Center.<!--1355146-->

### <a name="hide-installed-applications-in-software-center"></a><a name="bkmk_HideInstalled"></a>Geïnstalleerde toepassingen verbergen in Software Center

Wanneer u deze optie inschakelt, worden toepassingen die al zijn geïnstalleerd, niet meer weer gegeven op het tabblad toepassingen. Deze optie wordt ingesteld als de standaard waarde wanneer u Configuration Manager installeert of als u een upgrade naar uitvoert. Geïnstalleerde toepassingen zijn nog steeds beschikbaar voor controle op het tabblad installatie status. <!--1357592-->

### <a name="hide-application-catalog-link-in-software-center"></a><a name="bkmk_HideAppCat"></a>toepassingscatalogus koppeling verbergen in Software Center

De zicht baarheid van de Application catalog-website koppeling in Software Center opgeven. Als deze optie is ingesteld, krijgen gebruikers de koppeling Application catalog-website niet te zien in het knoop punt installatie status van software Center. <!--1358214-->

> [!Important]  
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  

### <a name="software-center-tab-visibility"></a>Zicht baarheid tabblad Software Center

#### <a name="starting-in-version-1906"></a>Vanaf versie 1906
<!--4063773-->

Kies de tabbladen die moeten worden weer gegeven in Software Center. Gebruik de knop **toevoegen** om een tabblad naar **zicht bare tabbladen**te verplaatsen. Gebruik de knop **verwijderen** om deze naar de lijst met **verborgen tabbladen** te verplaatsen. Volg de tabbladen met de knoppen **omhoog** of **omlaag** . 

Beschik bare tabbladen:
- **Toepassingen**
- **Updates**
- **Besturings systemen**
- **Installatie status**
- **Apparaatcompatibiliteit**
- **Opties**
- U kunt Maxi maal vijf aangepaste tabbladen toevoegen door te klikken op de knop **tabblad toevoegen** .
  - Geef de **tabblad naam** en de **inhouds-URL** op voor het aangepaste tabblad.
  - Selecteer **tabblad verwijderen** om een aangepast tabblad te verwijderen.  

  >[!Important]  
  > - Sommige website functies werken mogelijk niet wanneer deze worden gebruikt als aangepast tabblad in Software Center. Zorg ervoor dat u de resultaten test voordat u deze op clients implementeert. <!--519659-->
  > - Geef alleen vertrouwde of intranet website adressen op wanneer u een aangepast tabblad toevoegt.<!--SCCMDocs issue 1575-->

#### <a name="version-1902-and-earlier"></a>Versie 1902 en lager

Stel de extra instellingen in deze groep in op **Ja** om de volgende tabbladen zichtbaar te maken in Software Center:

- **Toepassingen**
- **Updates**
- **Besturings systemen**
- **Installatie status**
- **Apparaatcompatibiliteit**
- **Opties**
- **Een aangepast tabblad opgeven voor Software Center** <!--1358132-->
    - **Tabbladnaam**
    - **Inhouds-URL**

    >[!Important]  
    > Sommige website functies werken mogelijk niet wanneer deze worden gebruikt als aangepast tabblad in Software Center. Zorg ervoor dat u de resultaten test voordat u deze op clients implementeert. <!--519659-->
    >
    > Geef alleen vertrouwde of intranet website adressen op wanneer u een aangepast tabblad toevoegt.<!--SCCMDocs issue 1575-->

Als uw organisatie bijvoorbeeld geen nalevings beleid gebruikt en u het tabblad apparaatcompatibiliteit in Software Center wilt verbergen, stelt u het tabblad apparaatcompatibiliteit **inschakelen** in op **Nee**.

### <a name="configure-default-views-in-software-center"></a><a name="bkmk_swctr_defaults"></a>Standaard weergaven in Software Center configureren
<!--3612112-->
*(Geïntroduceerd in versie 1902)*

- Configureer het **standaard toepassings filter** als **alle** of alleen de **vereiste** toepassingen.  

  - Software Center gebruikt altijd de standaard instelling. Gebruikers kunnen dit filter wijzigen, maar Software Center blijft de voor keur niet behouden.  

- Stel de **standaard weergave** van de toepassing in op de **tegel weergave** of de **lijst weergave**.

  - Als een gebruiker deze configuratie wijzigt, wordt de voor keur van de gebruiker in de toekomst door Software Center gehandhaafd.


## <a name="software-deployment"></a>Software-implementatie  

### <a name="schedule-re-evaluation-for-deployments"></a>Nieuwe evaluatie voor implementaties plannen

Configureer een planning voor wanneer Configuration Manager de regels voor vereisten voor alle implementaties opnieuw evalueert. De standaard waarde is elke zeven dagen.  

> [!IMPORTANT]  
> Deze instelling is meer invasief voor de lokale client dan het netwerk of de site server. Een meer agressieve evaluatie planning is een negatieve invloed op de prestaties van uw netwerk en client computers. Micro soft raadt u niet aan een lagere waarde in te stellen dan de standaard instelling. Als u deze waarde wijzigt, controleert u de prestaties nauw keurig.  

Start deze actie vanaf een client als volgt: Selecteer in het configuratie scherm van **Configuration Manager** , in het tabblad **acties** , de **evaluatie cyclus**voor de implementatie van de toepassing.  



## <a name="software-inventory"></a>Software-inventaris  

### <a name="enable-software-inventory-on-clients"></a>Software-inventaris op clients inschakelen

Deze optie is standaard ingesteld op **Ja** . Zie [Inleiding tot software-inventarisatie](../manage/inventory/introduction-to-software-inventory.md)voor meer informatie.

### <a name="schedule-software-inventory-and-file-collection"></a>Software-inventaris en verzamelen van bestanden plannen

Selecteer **planning** om de frequentie aan te passen waarmee clients de software-inventaris en de verzamelings cycli uitvoeren. Deze cyclus wordt standaard elke zeven dagen uitgevoerd.

### <a name="inventory-reporting-detail"></a>Detail inventarisrapportage

Geef een van de volgende niveaus van bestands informatie op voor inventarisatie:

- **Alleen bestand**
- **Alleen product**
- **Volledige details** (standaard)

### <a name="inventory-these-file-types"></a>Deze bestandstypen inventariseren

Als u het type bestand wilt opgeven dat u wilt inventariseren, selecteert u **typen instellen**en configureert u vervolgens de volgende opties:  

> [!NOTE]  
> Als er meerdere aangepaste client instellingen worden toegepast op een computer, wordt de inventarisatie van elke instelling samengevoegd.  

- Selecteer **Nieuw** om een nieuw bestands type toe te voegen aan de inventarisatie. Geef vervolgens de volgende gegevens op in het dialoog venster **geïnventariseerde bestands eigenschappen** :  

    - **Naam**: Geef een naam op voor het bestand dat u wilt inventariseren. Gebruik een asterisk ( `*` ) als Joker teken voor wille keurige tekst en een vraag teken ( `?` ) die een enkel teken voor stelt. Als u bijvoorbeeld alle bestanden met de extensie. doc wilt inventariseren, geeft u de bestands naam op `*.doc` .  

    - **Locatie**: Selecteer **instellen** om het dialoog venster **Eigenschappen van pad** te openen. Software-inventaris configureren om op alle harde schijven van de client te zoeken naar het opgegeven bestand, zoek een opgegeven pad (bijvoorbeeld `C:\Folder` ) of zoek naar een opgegeven variabele (bijvoorbeeld `%windir%` ). U kunt ook zoeken in alle submappen onder het opgegeven pad.  

    - **Versleutelde en gecomprimeerde bestanden uitsluiten**: wanneer u deze optie kiest, worden gecomprimeerde of versleutelde bestanden niet geïnventariseerd.  

    - **Bestanden in de map Windows uitsluiten**: wanneer u deze optie kiest, worden alle bestanden in de Windows-map en de bijbehorende submappen niet geïnventariseerd.  

    Selecteer **OK** om het dialoog venster **geïnventariseerde bestands eigenschappen** te sluiten. Voeg alle bestanden toe die u wilt inventariseren en selecteer vervolgens **OK** om het dialoog venster **client instelling configureren** te sluiten.  

### <a name="collect-files"></a>Bestanden verzamelen

Als u bestanden wilt verzamelen van client computers, selecteert u **bestanden instellen**en configureert u de volgende instellingen:  

> [!NOTE]  
> Als er meerdere aangepaste client instellingen worden toegepast op een computer, wordt de inventarisatie van elke instelling samengevoegd.  

- Selecteer in het dialoog venster **client instelling configureren** de optie **Nieuw** om een bestand toe te voegen dat moet worden verzameld.  

- Voer, in het dialoogvenster **Eigenschappen verzameld bestand** , de volgende informatie in:  

    - **Naam**: Geef een naam op voor het bestand dat u wilt verzamelen. Gebruik een asterisk ( `*` ) als Joker teken voor wille keurige tekst en een vraag teken ( `?` ) die een enkel teken voor stelt.  

    - **Locatie**: Selecteer **instellen** om het dialoog venster **Eigenschappen van pad** te openen. Software-inventaris configureren om te zoeken naar alle harde schijven van de client voor het bestand dat u wilt verzamelen, zoek een opgegeven pad (bijvoorbeeld `C:\Folder` ) of zoek naar een opgegeven variabele (bijvoorbeeld `%windir%` ). U kunt ook zoeken in alle submappen onder het opgegeven pad.  

    - **Versleutelde en gecomprimeerde bestanden uitsluiten**: wanneer u deze optie kiest, worden gecomprimeerde of versleutelde bestanden niet verzameld.  

    - **Stoppen met verzamelen van bestanden wanneer de totale grootte van de bestanden groter is dan (KB)**: Geef de bestands grootte op, in kilo bytes (KB), waarna de client stopt met het verzamelen van de opgegeven bestanden.  

    > [!NOTE]  
    > De site server verzamelt de vijf meest recent gewijzigde versies van verzamelde bestanden en slaat deze op in de `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` map. Als een bestand sinds de laatste software-inventarisatie fase niet is gewijzigd, wordt het bestand niet opnieuw verzameld.  
    >
    > Software-inventaris verzamelt geen bestanden die groter zijn dan 20 MB.  
    >
    > De waarde **maximum grootte voor alle verzamelde bestanden (KB)** in het dialoog venster **client instelling configureren** toont de maximum grootte voor alle verzamelde bestanden. Wanneer deze grootte is bereikt, stopt het verzamelen van bestanden. Alle reeds verzamelde bestanden worden weerhouden en naar de siteserver gezonden.  

    > [!IMPORTANT]
    > Als u software-inventaris configureert om vele grote bestanden te verzamelen, kan deze configuratie een negatieve invloed hebben op de prestaties van uw netwerk en site server.  

    Zie [resource Explorer gebruiken om software-inventaris weer te geven](../manage/inventory/use-resource-explorer-to-view-software-inventory.md)voor meer informatie over het weer geven van verzamelde bestanden.  

    Selecteer **OK** om het dialoog venster **Eigenschappen van verzamelde bestanden** te sluiten. Voeg alle bestanden toe die u wilt verzamelen en selecteer vervolgens **OK** om het dialoog venster **client instelling configureren** te sluiten.  

### <a name="set-names"></a>Namen instellen

De software-inventaris agent haalt fabrikant-en product namen op uit informatie over de header van het bestand. Deze namen zijn niet altijd gestandaardiseerd in de informatie over de bestands header. Wanneer u software-inventaris in resource Explorer bekijkt, kunnen er verschillende versies van dezelfde fabrikant of product naam worden weer gegeven. Als u deze weergave namen wilt standaardiseren, selecteert u **namen instellen**en configureert u de volgende instellingen:  

- **Naam type**: software-inventaris verzamelt informatie over fabrikanten en producten. Kies of u weergave namen wilt configureren voor een **fabrikant** of een **product**.  

- **Weergave naam**: Geef de weergave naam op die u wilt gebruiken in plaats van de namen in de lijst **geïnventariseerde namen** . Selecteer **Nieuw**om een nieuwe weergave naam op te geven.  

- **Geïnventariseerde namen**: Selecteer **Nieuw**om een geïnventariseerde naam toe te voegen. Deze naam wordt in software-inventarisatie vervangen door de naam die u hebt gekozen in de lijst **weergave naam** . U kunt meerdere namen toevoegen om te vervangen.  



## <a name="software-metering"></a>Softwaremeter

### <a name="enable-software-metering-on-clients"></a>Software meter op clients inschakelen

Deze instelling is standaard ingesteld op **Ja** . Zie [software licentie controle](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering)voor meer informatie.

### <a name="schedule-data-collection"></a>Gegevens verzameling plannen

Selecteer **schema** om de frequentie aan te passen waarmee clients de software licentie controle cyclus uitvoeren. Deze cyclus wordt standaard elke zeven dagen uitgevoerd.



## <a name="software-updates"></a>Software-updates  

### <a name="enable-software-updates-on-clients"></a>Software-updates op clients inschakelen

Gebruik deze instelling om software-updates op Configuration Manager-clients in te scha kelen. Wanneer u deze instelling uitschakelt, wordt bestaande implementatie beleidsregels van clients door Configuration Manager verwijderd. Wanneer u deze instelling opnieuw inschakelt, zal de client het huidige implementatiebeleid downloaden.  

> [!IMPORTANT]  
> Wanneer u deze instelling uitschakelt, werkt het nalevings beleid dat afhankelijk is van software-updates niet meer.  

### <a name="software-update-scan-schedule"></a>Planning software-updatescan

Selecteer **planning** om op te geven hoe vaak de client een scan op nalevings beoordeling start. Deze scan bepaalt de status voor software-updates op de client (bijvoorbeeld vereist of geïnstalleerd). Zie [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance)voor meer informatie over nalevingsbeoordeling.  

Deze scan gebruikt standaard een eenvoudig schema om elke zeven dagen te beginnen. U kunt een aangepaste planning maken. U kunt een exacte start datum en-tijd opgeven, UTC (Universal Coordinated Time) of de lokale tijd gebruiken en het terugkerende interval configureren voor een specifieke dag van de week.  

> [!NOTE]  
> Als u een interval van minder dan één dag opgeeft, wordt Configuration Manager automatisch ingesteld op één dag.  

> [!WARNING]  
> De werkelijke start tijd op client computers is de start tijd plus een wille keurige hoeveelheid tijd, Maxi maal twee uur. Deze wille keurige manier voor komt dat client computers de scan starten en verbinding maken met het actieve software-update punt.  

### <a name="schedule-deployment-re-evaluation"></a>Nieuwe evaluatie van implementatie plannen

Selecteer **schema** om te configureren hoe vaak de client agent voor software-updates software-updates opnieuw evalueert voor de installatie status op Configuration Manager-client computers. Wanneer eerder geïnstalleerde software-updates niet meer op clients zijn gevonden, maar nog steeds vereist zijn, installeert de client de software-updates opnieuw.

Pas deze planning aan op basis van het bedrijfs beleid voor naleving van software-updates en of gebruikers software-updates kunnen verwijderen. Elke nieuwe evaluatie cyclus voor implementaties resulteert in de activiteit netwerk-en client computer processor. Deze instelling maakt standaard gebruik van een eenvoudig schema om elke zeven dagen de scan opnieuw te evalueren voor de implementatie.  

> [!NOTE]  
> Als u een interval van minder dan één dag opgeeft, wordt Configuration Manager automatisch ingesteld op één dag.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Wanneer een deadline voor de implementatie van software-updates is bereikt, installeert u alle andere software-update-implementaties met een deadline die binnen een bepaalde periode komt te staan

Stel deze optie in op **Ja** om alle software-updates te installeren vanuit de vereiste implementaties met deadlines die binnen een bepaalde periode vallen. Wanneer een vereiste software-update-implementatie een deadline bereikt, start de client de installatie voor de software-updates in de implementatie. Met deze instelling wordt bepaald of software-updates moeten worden geïnstalleerd op basis van andere vereiste implementaties met een deadline binnen de opgegeven tijd.  

Gebruik deze instelling om de installatie te versnellen voor vereiste software-updates. Deze instelling heeft ook de mogelijkheid om client beveiliging te verbeteren, meldingen te verlagen voor de gebruiker en de client opnieuw op te starten. Deze waarde is standaard ingesteld op **Nee**.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>De periode gedurende welke alle in afwachting zijnde implementaties met deadlines in deze periode eveneens worden geïnstalleerd

Gebruik deze instelling om de periode voor de vorige instelling op te geven. U kunt een waarde tussen 1 en 23 uur en 1 tot 365 dagen invoeren. Deze instelling is standaard 7 dagen geconfigureerd.  

### <a name="allow-clients-to-download-delta-content-when-available"></a>Clients toestaan om Delta-inhoud te downloaden wanneer deze beschikbaar is

*(Geïntroduceerd in versie 1902)*

Stel deze optie in op **Ja** als u wilt dat clients Delta-inhouds bestanden gebruiken. Met deze instelling kan de Windows Update-Agent op het apparaat bepalen welke inhoud nodig is en het selectief downloaden. 

- Voordat u deze client instelling inschakelt, zorgt u ervoor dat Delivery Optimization correct is geconfigureerd voor uw omgeving. Zie [Windows Delivery Optimization](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization) en de [instelling Delivery Optimization client](#delivery-optimization)voor meer informatie.
 - Deze client instelling vervangt de **installatie van bestanden voor snelle installatie op clients**. Stel deze optie in op **Ja** als u wilt dat clients snelle installatie bestanden kunnen gebruiken. Zie voor meer informatie [bestanden voor snelle installatie beheren voor Windows 10-updates](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).
 - Vanaf Configuration Manager versie 1910, wanneer deze optie is ingesteld, wordt Delta-down load gebruikt voor alle installatie bestanden van Windows Update, niet alleen snelle installatie bestanden.
    - Wanneer u een CMG gebruikt voor de opslag van inhoud, worden de inhoud voor updates van derden niet gedownload naar clients als de instelling **Delta-inhoud downloaden wanneer de beschik bare** client is ingeschakeld. <!--6598587--> 


### <a name="port-that-clients-use-to-receive-requests-for-delta-content"></a>Poort die clients gebruiken om aanvragen voor Delta-inhoud te ontvangen

*(Geïntroduceerd in versie 1902)*

Met deze instelling configureert u de lokale poort voor de HTTP-listener voor het downloaden van Delta-inhoud. Deze is standaard ingesteld op 8005. U hoeft deze poort niet te openen in de firewall van de client. 

> [!NOTE]
>Deze client instelling vervangt **poort die wordt gebruikt voor het downloaden van inhoud voor bestanden voor snelle installatie**.


### <a name="enable-management-of-the-office-365-client-agent"></a>Beheer van de Office 365-client agent inschakelen

Wanneer u deze optie instelt op **Ja**, wordt de configuratie van Office 365-installatie-instellingen ingeschakeld. Ook kunt u hiermee bestanden downloaden van Office Content Delivery Networks (Cdn's) en de bestanden implementeren als een toepassing in Configuration Manager. Zie [Office 365 ProPlus beheren](../../../sum/deploy-use/manage-office-365-proplus-updates.md)voor meer informatie.

### <a name="enable-installation-of-software-updates-in-all-deployments-maintenance-window-when-software-update-maintenance-window-is-available"></a><a name="bkmk_SUMMaint"></a>Installatie van software-updates inschakelen in het onderhouds venster ' alle implementaties ' wanneer het onderhouds venster voor software-updates beschikbaar is

Wanneer u deze optie instelt op **Ja**en de client ten minste één onderhouds venster voor software-updates heeft gedefinieerd, worden software-updates geïnstalleerd tijdens het onderhouds venster ' alle implementaties '.

Deze waarde is standaard ingesteld op **Nee**. Deze waarde gebruikt hetzelfde gedrag als eerder: als beide typen bestaan, wordt het venster genegeerd. <!--2839307-->

> [!NOTE]
> Deze instelling is ook van toepassing op onderhouds Vensters die u configureert voor het Toep assen op **taken reeksen**.<!-- SCCMDocs-pr #4596 -->
>
> Als op de client alleen een venster met **implementaties** beschikbaar is, worden software-updates of taken reeksen nog steeds in dat venster geïnstalleerd.

#### <a name="maintenance-window-example"></a>Voor beeld van onderhouds venster

U kunt bijvoorbeeld de volgende onderhouds Vensters configureren:

- **Alle implementaties**: 02:00-04:00
- **Software-updates**: 04:00-06:00

De client installeert standaard alleen software-updates tijdens het tweede onderhouds venster. Het onderhouds venster voor alle implementaties in dit scenario wordt genegeerd. Wanneer u deze instelling wijzigt in **Ja**, installeert de client software-updates tussen 02:00-06:00.


### <a name="specify-thread-priority-for-feature-updates"></a><a name="bkmk_thread-priority"></a>De thread prioriteit voor onderdeel updates opgeven

<!--3734525-->
Vanaf Configuration Manager versie 1902 kunt u de prioriteit aanpassen waarmee clients met Windows 10 versie 1709 of hoger een onderdeel Update installeren via [Windows 10 Servicing](../../../osd/deploy-use/manage-windows-as-a-service.md). Deze instelling heeft geen invloed op Windows 10-in-place upgrade taken reeksen.

Deze client instelling biedt de volgende opties:

- **Niet geconfigureerd**: Configuration Manager de instelling niet wijzigt. Beheerders kunnen hun eigen setupconfig.ini-bestand vooraf faseren. Dit is de standaardwaarde.

- **Normaal**: Windows Setup maakt meer systeem bronnen en updates sneller. Er wordt meer processor tijd gebruikt, waardoor de totale installatie tijd korter is, maar de storing van de gebruiker langer is.  

    - Hiermee configureert u het setupconfig.ini-bestand op het apparaat met de `/Priority Normal` [Windows Setup-opdracht regel optie](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

- **Laag**: u kunt op het apparaat blijven werken terwijl het op de achtergrond wordt gedownload en bijgewerkt. De totale installatie tijd is langer, maar de onderbreking van de gebruiker is korter. Mogelijk moet u de maximale uitvoerings tijd van de update verhogen om een time-out te voor komen wanneer u deze optie gebruikt.  

    - Hiermee verwijdert u de `/Priority` [Windows Setup-opdracht regel optie](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) uit het setupconfig.ini-bestand.


### <a name="enable-third-party-software-updates"></a>Updates van software van derden inschakelen

Wanneer u deze optie instelt op **Ja**, wordt het beleid ingesteld voor het **toestaan van ondertekende updates voor een intranet locatie van micro soft Update service** en wordt het handtekening certificaat geïnstalleerd in het archief met vertrouwde uitgevers op de client.

### <a name="enable-dynamic-update-for-feature-updates"></a><a name="bkmk_du"></a>Dynamische updates voor functie-updates inschakelen
<!--4062619-->
Vanaf Configuration Manager versie 1906 kunt u de [dynamische update voor Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847)configureren. Met de dynamische update worden taal pakketten, onderdelen op aanvraag, stuur Programma's en cumulatieve updates geïnstalleerd tijdens de installatie van Windows door de client te sturen om deze updates via internet te downloaden. Als deze instelling is ingesteld op **Ja** of **Nee**, wordt het [setupconfig](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) -bestand dat wordt gebruikt tijdens de installatie van de functie-update, door Configuration Manager gewijzigd.

- **Niet geconfigureerd** : de standaard waarde. Er worden geen wijzigingen aangebracht in het setupconfig-bestand.
  - Dynamische updates is standaard ingeschakeld op alle ondersteunde versies van Windows 10.
    - Voor Windows 10 versie 1803 en eerder controleert dynamische update de WSUS-server van het apparaat op goedgekeurde dynamische updates. In Configuration Manager omgevingen worden dynamische updates nooit rechtstreeks goedgekeurd in de WSUS-server, zodat deze apparaten niet worden geïnstalleerd.
    - Met ingang van Windows 10 versie 1809 maakt dynamische update gebruik van de Internet verbinding van het apparaat om dynamische updates van Microsoft Update te verkrijgen. Deze dynamische updates worden niet gepubliceerd voor gebruik van WSUS.
- **Ja** , Hiermee schakelt u dynamische updates in.
- Met **Nee** , dynamische update uitschakelen.


## <a name="state-messaging"></a>Status berichten

### <a name="state-message-reporting-cycle-minutes"></a>Rapportage cyclus status bericht (minuten)

Hiermee geeft u op hoe vaak clients status berichten rapporteren. Deze instelling is standaard 15 minuten.



## <a name="user-and-device-affinity"></a>Affiniteit van gebruiker en apparaat  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Gebruiksdrempel affiniteit van gebruiker met apparaat (minuten)

Geef het aantal minuten op voordat Configuration Manager een affiniteits toewijzing van een gebruiker met apparaat maakt. Deze waarde is standaard 2880 minuten (twee dagen).

### <a name="user-device-affinity-usage-threshold-days"></a>Gebruiksdrempel affiniteit van gebruiker met apparaat (dagen)

Geef het aantal dagen op waarover de client de drempel waarde voor de affiniteit van apparaten op basis van het gebruik meet. Deze waarde is standaard 30 dagen.

> [!NOTE]  
> U kunt bijvoorbeeld de **gebruiks drempel van affiniteit van gebruiker met apparaat (minuten)** opgeven als **60** minuten en de **drempel waarde voor het gebruik van affiniteit tussen gebruikers en apparaten (dagen)** als **5** dagen. Vervolgens moet de gebruiker gedurende een periode van vijf dagen het apparaat gedurende 60 minuten gebruiken om automatische affiniteit met het apparaat te maken.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Affiniteit van gebruikers met apparaat automatisch configureren via gebruiksgegevens

Kies **Ja** om automatische gebruikers affiniteit met apparaat te maken op basis van de gebruiks gegevens die door Configuration Manager verzameld.  

### <a name="allow-user-to-define-their-primary-devices"></a>Gebruikers toestaan hun primaire apparaten te definiëren
<!--3485366-->
Als deze instelling is ingesteld op **Ja**, kunnen gebruikers hun eigen primaire apparaten in Software Center identificeren. Zie de [Gebruikers handleiding voor Software Center](../../understand/software-center.md#work-information)voor meer informatie.

## <a name="windows-analytics"></a>Windows Analytics

> [!Important]  
> De Windows Analytics-service wordt vanaf 31 januari 2020 buiten gebruik gesteld. Zie [KB 4521815: Windows Analytics is buiten gebruik gesteld op 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement)voor meer informatie.
>
> Desktop Analytics is de ontwikkeling van Windows Analytics. Zie [Wat is Desktop Analytics](../../../desktop-analytics/overview.md)? voor meer informatie.

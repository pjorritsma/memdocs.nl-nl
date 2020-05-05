---
title: Technical Preview 1709
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview-versie 1709 voor Configuration Manager.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bedb515c8446e13189fb84644bc0ce7563cc1574
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078767"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1709 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1709. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md) om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bekende problemen in deze technische preview:**
- **Update voor preview versie 1709 mislukt wanneer u een site server in de passieve modus hebt**. Wanneer u de preview-versie 1706, 1707 of 1708 uitvoert en een [primaire site server in de passieve modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)hebt, moet u de site server van de passieve modus verwijderen voordat u uw preview-site kunt bijwerken naar versie 1709. U kunt de site server van de passieve modus opnieuw installeren nadat versie 1709 van de site is uitgevoerd.

  De site server van de passieve modus verwijderen:
  1. Ga in de-console naar **beheer** > **overzicht** > **site configuratie** > **servers en site systeem rollen**en selecteer vervolgens de site server passieve modus.
  2. Klik in het deel venster **site systeem rollen** met de rechter muisknop op de **site** serverrol en kies vervolgens **rol verwijderen**.
  3. Klik met de rechter muisknop op de site server in de passieve modus en kies **verwijderen**.
  4. Nadat de installatie van de site server ongedaan is gemaakt, start u de service **CONFIGURATION_MANAGER_UPDATE**opnieuw op de actieve primaire site server.


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Verbeterde VPN-profiel ervaring in Configuration Manager-console
<!-- 1313282 -->
In deze release hebben we de wizard VPN-profiel en eigenschappen bijgewerkt om de instellingen weer te geven die geschikt zijn voor het geselecteerde platform. Met name:

- Elk platform heeft zijn eigen werk stroom, wat betekent dat nieuwe VPN-profielen alleen de instelling bevatten die door het platform wordt ondersteund.
- De pagina's met **ondersteunde platforms** worden nu weer gegeven na de pagina **Algemeen** .  U kiest nu het platform voordat u eigenschaps waarden instelt.
- Wanneer het platform is ingesteld op **Android**, **Android for Work**of **Windows Phone 8,1**, is de pagina met **ondersteunde platforms** niet nodig en wordt deze niet weer gegeven.
- De Configuration Manager werk stroom op de client is gecombineerd met de op clients gebaseerde Windows 10-werk stromen op basis van het Hybrid Mobile Device (MDM). ze ondersteunen dezelfde instellingen.
- Elke werk stroom van het platform bevat alleen de instellingen die geschikt zijn voor die werk stroom.  De Android-werk stroom bevat bijvoorbeeld instellingen die geschikt zijn voor Android. de juiste instellingen voor iOS of Windows 10 Mobile worden niet meer weer gegeven in de Android-werk stroom.
- Voor Windows 8,1-apparaten worden instellingen die worden beheerd door Configuration Manager duidelijk gemarkeerd.
- De automatische VPN-pagina is verouderd en is verwijderd.

Deze wijzigingen zijn van toepassing op nieuwe VPN-profielen.  

Bestaande VPN-profielen worden ongewijzigd om het compatibiliteits risico te minimaliseren.  Wanneer u een bestaand profiel bewerkt, worden de instellingen weer gegeven zoals tijdens het maken van het profiel.  

### <a name="try-it-out"></a>Probeer het nu!

Maak een nieuw VPN-profiel met behulp van het gebruikelijke proces. U ziet dat de eerste pagina in de opties van de wizard VPN-profiel is gewijzigd.

1. Ga naar **activa en naleving** > **overzicht** > **instellingen** > voor naleving van**bedrijfs bronnen toegang** > **VPN-profielen** en kies vervolgens **VPN-profiel maken**.
2. Voer op de pagina **Algemeen** een naam in en kies een van de volgende opties onder **Geef het type VPN-profiel op dat u wilt maken**:

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS en macOS  
    - Android  
    - Android for Work  

3. Als u kiest voor **Windows 8,1**, kunt u ook een **Nieuw profiel maken** of **importeren uit een bestand**.
4. Voltooi de wizard om het profiel te maken.

Wanneer u verschillende platforms selecteert, ziet u dat alleen de instellingen die relevant zijn voor het geselecteerde platform worden weer gegeven.

## <a name="co-management-for-windows-10-devices"></a>Co-beheer voor Windows 10-apparaten    
<!-- 1350871 -->
Veel klanten willen Windows 10-apparaten op dezelfde manier beheren als mobiele apparaten met behulp van een vereenvoudigde, voordelige oplossing in de Cloud. Het maken van de overgang van traditioneel beheer naar moderne beheer kan echter lastig zijn. Vanaf Windows 10, versie 1607 (ook wel bekend als de jubileum update), kunt u een Windows 10-apparaat toevoegen aan on-premises Active Directory (AD) en in de cloud gebaseerde Azure AD tegelijkertijd (hybride Azure AD). Co-beheer maakt gebruik van deze verbetering en stelt u in staat om Windows 10-apparaten gelijktijdig te beheren met behulp van Configuration Manager en intune. Het is een oplossing die een brug biedt van traditioneel naar modern beheer en biedt u een pad om de overgang te maken met behulp van een gefaseerde benadering. 

### <a name="prerequisites"></a>Vereisten
U moet beschikken over de volgende vereisten om co-beheer in te scha kelen. Er zijn algemene vereisten en andere vereisten voor bestaande Configuration Manager-clients en-apparaten die geen-clients zijn.

### <a name="known-issues"></a>Bekende problemen
Nadat u een beleid voor co-beheer hebt gemaakt, kunt u het beleid niet bewerken. Als u het beleid wilt wijzigen, verwijdert u het en maakt u het vervolgens opnieuw met de instellingen die u nodig hebt. 

#### <a name="general-prerequisites"></a>Algemene vereisten
Hieronder vindt u algemene vereisten voor het inschakelen van co-beheer:  

- Technical Preview voor Configuration Manager versie 1709
- Azure AD 
- EMS-of intune-licentie voor alle gebruikers
- InTune-abonnement &#40;MDM-instantie in intune is ingesteld op **intune**&#41;

   > [!Note]  
   > Als u een Hybrid MDM-omgeving (intune geïntegreerd met Configuration Manager) hebt, kunt u co-beheer niet inschakelen.

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Aanvullende vereisten voor bestaande Configuration Manager-clients
- Windows 10, versie 1709 (update van het najaar van makers) en hoger
- Hybride Azure AD-join (gekoppeld aan AD en Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Aanvullende vereisten voor nieuwe Windows 10-apparaten
- Windows 10, versie 1709 (update van het najaar van makers) en hoger
- [Cloudbeheergateway](../clients/manage/manage-clients-internet.md#cloud-management-gateway) in Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Workloads die u kunt overschakelen naar intune
Nadat u co-beheer hebt ingeschakeld, blijft Configuration Manager alle werk belastingen gaan beheren. Wanneer u besluit dat u klaar bent, kunt u intune starten met het beheer van beschik bare workloads. In deze versie kunt u de volgende werk belastingen beheren met intune.   

#### <a name="compliance-policies"></a>Compliance beleidsregels
Nalevings beleid definieert de regels en instellingen waaraan een apparaat moet voldoen om te worden beschouwd als compatibel met het beleid voor voorwaardelijke toegang. U kunt ook nalevingsbeleid gebruiken om nalevingsproblemen met apparaten te bewaken en onafhankelijk van voorwaardelijke toegang op te lossen.

#### <a name="windows-update-for-business-policies"></a>Windows Update voor bedrijfs beleid
Met Windows Update for business-beleid kunt u uitstel beleid configureren voor Windows 10-onderdelen updates of kwaliteits updates voor Windows 10-apparaten die rechtstreeks worden beheerd door Windows Update voor bedrijven. Zie [Configure Windows Update for Business policies](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)(Engelstalig) voor meer informatie.  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Externe acties die beschikbaar zijn in intune op Azure voor gezamenlijk beheerde apparaten
Wanneer een Windows 10-apparaat is ingeschakeld voor co-beheer, hebt u de volgende externe acties beschikbaar in intune op Azure:  
- [Fabrieks instellingen terugzetten](https://docs.microsoft.com/intune/devices-wipe#wipe)
- [Selectief wissen](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Apparaten verwijderen](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Apparaat opnieuw opstarten](https://docs.microsoft.com/intune/device-restart)
- [Fresh Start](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>InTune voorbereiden voor co-beheer
Voordat u overschakelt van Configuration Manager naar intune, moet u de profielen en beleids regels maken die u in intune nodig hebt om ervoor te zorgen dat uw apparaten blijven worden beveiligd.
U kunt in intune objecten maken op basis van de objecten die u in Configuration Manager hebt. Als uw huidige strategie is gebaseerd op verouderd of traditioneel beheer, wilt u wellicht een stap terugnemen om te zien welke beleids regels en profielen u nodig hebt voor modern beheer. Gebruik de volgende bronnen om de beleids regels en profielen te maken.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Windows Update voor bedrijfs beleid](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Apparaatconfiguratieprofielen](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Architectuur overzicht voor co-beheer
Het volgende diagram biedt een architectuur overzicht van co-beheer en hoe het past in bestaande configuratie-en intune-infra structuren.

![Architectuur diagram voor co-beheer](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Scenario's voor het inschakelen van co-beheer  
U kunt co-beheer inschakelen voor Windows 10-apparaten die zijn Inge schreven bij Microsoft Intune en bestaande Windows 10 Configuration Manager-clients. Beide scenario's leiden ertoe dat Windows 10-apparaten gelijktijdig worden beheerd door Configuration Manager en intune, en zijn gekoppeld aan AD en Azure AD.  

#### <a name="devices-enrolled-in-intune"></a>Apparaten die zijn ingeschreven bij Intune  
Wanneer Windows 10-apparaten zijn Inge schreven bij intune, kunt u de Configuration Manager-client installeren op de apparaten (met behulp van een specifiek opdracht regel argument) om de clients voor te bereiden voor co-beheer. Vervolgens schakelt u co-beheer in vanuit de Configuration Manager-console om te beginnen met het verplaatsen van specifieke workloads naar intune voor specifieke Windows 10-apparaten.  

Voor Windows 10-apparaten die nog niet zijn Inge schreven bij intune, kunt u automatische inschrijving in azure gebruiken om de apparaten in te schrijven. Voor nieuwe Windows 10-apparaten kunt u Windows auto pilot gebruiken om de out of Box Experience (OOBE) te configureren, waaronder automatische inschrijving waarmee apparaten worden inge schreven bij intune.  

#### <a name="configuration-manager-clients"></a>Configuration Manager-clients
Wanneer u Windows 10-apparaten hebt die Configuration Manager-clients zijn, kunt u deze apparaten registreren en co-beheer inschakelen via de Configuration Manager-console. Configuration Manager automatische inschrijving in intune wordt geactiveerd op basis van de gegevens van de Azure AD-Tenant.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Windows 10-apparaten voorbereiden op co-beheer
U kunt co-beheer inschakelen op Windows 10-apparaten die zijn gekoppeld aan AD en Azure AD, en die zijn Inge schreven bij intune en een client in Configuration Manager. Voor nieuwe Windows 10-apparaten en voor apparaten die al zijn Inge schreven bij intune, installeert u de Configuration Manager-client voordat ze gezamenlijk kunnen worden beheerd. Voor Windows 10-apparaten die al Configuration Manager-clients zijn, kunt u de apparaten inschrijven bij intune en co-beheer inschakelen in de Configuration Manager-console.

#### <a name="command-line-to-install-configuration-manager-client"></a>Opdracht regel voor de installatie van Configuration Manager-client
Maak een app in intune voor Windows 10-apparaten die nog niet Configuration Manager-clients zijn. Wanneer u de app in de volgende secties maakt, gebruikt u de volgende opdracht regel:

ccmsetup. msi CCMSETUPCMD = "/MP: &#60;*URL van het wederzijdse verificatie-eind punt voor de Cloud beheer gateway*&#62;/CCMHOSTNAME =&#60;*URL van de Cloud beheer gateway wederzijdse verificatie-eind punt*&#62; SMSSiteCode =&#60;*site* code&#62; SMSMP = https: &#47;/&#60;*FQDN van MP*&#62; AADTENANTID =&#60;*Aad-Tenant-id*&#62; AADTENANTNAME =&#60;*naam* van de Tenant&#62; AADCLIENTAPPID =&#60;*Server AppID voor Aad* *-* integratie&#62; AADRESOURCEURI = https: &#47;

Als u bijvoorbeeld de volgende waarden had:

- **URL van het wederzijdse verificatie-eind punt van de Cloud beheer gateway**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Gebruik de waarde **MutualAuthPath** in de SQL-weer gave **VProxy_Roles** voor de **URL van de gemeen schappelijke verificatie-eind punt waarde van de Cloud beheer gateway** .

- **FQDN van beheer punt (MP)**: sccmmp.Corp.contoso.com    
- **Site**code: PS1    
- **Azure AD-Tenant-id**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Azure AD-Tenant naam**: contoso    
- **Id van Azure AD-client-app**: bef323b3-042f-41a6-907A-f9faf0d1XXXX     
- **URI van Aad-resource-id**: ConfigMgrServer    

  > [!Note]    
  > Gebruik de waarde **IdentifierUri** die in **vSMS_AAD_Application_Ex** de SQL-weer gave van de **Aad-resource-id** is gevonden.

U gebruikt de volgende opdracht regel:

ccmsetup. msi CCMSETUPCMD = "/MP: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME = contoso. cloudapp. net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode = PS1 SMSMP = https:/&#47;sccmmp.corp.contoso.com AADTENANTID = 72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME = contoso AADCLIENTAPPID = bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI = https:/&#47;ConfigMgrServer"

> [!Tip]
>U kunt de opdracht regel parameters voor uw site vinden door de volgende stappen uit te voeren:     
> 1. Ga in de Configuration Manager-console naar **beheer** > **overzicht** > **Cloud Services** > **co-beheer**.  
> 2. Kies op het tabblad Start in de groep beheren de optie **co-beheer configureren** om de wizard voor het onboarden van co-beheer te openen.    
> 3. Klik op de pagina abonnement op **Aanmelden** en meld u aan bij uw intune-Tenant en klik vervolgens op **volgende**.    
> 4. Klik op de pagina activering op **kopiëren** in het gedeelte apparaten die zijn **Inge schreven in intune** om de opdracht regel naar het klem bord te kopiëren en sla de opdracht regel vervolgens op voor gebruik in de procedure om de app te maken.  
> 5. Klik op **Annuleren** om de wizard af te sluiten.

#### <a name="new-windows-10-devices"></a>Nieuwe Windows 10-apparaten
Voor nieuwe Windows 10-apparaten kunt u de auto pilot-service gebruiken voor het configureren van de out-of-Box-ervaring, waaronder het toevoegen van het apparaat aan AD en Azure AD, en het inschrijven van het apparaat bij intune. Maak vervolgens in intune een app om de Configuration Manager-client te implementeren.  
1. Schakel Auto Pilot in voor de nieuwe Windows 10-apparaten. Zie [overzicht van Windows auto pilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot)voor meer informatie.  
2. Configureer automatische inschrijving in azure AD voor uw apparaten die automatisch moeten worden inge schreven bij intune. Zie [Windows-apparaten inschrijven voor Microsoft intune](https://docs.microsoft.com/intune/windows-enroll)voor meer informatie.
3. Maak een app in intune met het Configuration Manager-client pakket en implementeer de app op Windows 10-apparaten die u gezamenlijk wilt beheren. Gebruik de [opdracht regel om Configuration Manager-client te installeren](#command-line-to-install-configuration-manager-client) wanneer u de stappen door lopen om [clients van Internet te installeren met behulp van Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Windows 10-apparaten die niet zijn Inge schreven bij intune of een Configuration Manager-client
Voor Windows 10-apparaten die niet zijn Inge schreven bij intune of de Configuration Manager-client, kunt u automatische inschrijving gebruiken om het apparaat in te schrijven bij intune. Maak vervolgens in intune een app om de Configuration Manager-client te implementeren.
1. Configureer automatische inschrijving in azure AD voor uw apparaten die automatisch moeten worden inge schreven bij intune. Zie [Windows-apparaten inschrijven voor Microsoft intune](https://docs.microsoft.com/intune/windows-enroll)voor meer informatie.  
2. Maak een app in intune met het Configuration Manager-client pakket en implementeer de app op Windows 10-apparaten die u gezamenlijk wilt beheren. Gebruik de [opdracht regel om Configuration Manager-client te installeren](#command-line-to-install-configuration-manager-client) wanneer u de stappen door lopen om [clients van Internet te installeren met behulp van Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Windows 10-apparaten die zijn Inge schreven bij intune
Voor Windows 10-apparaten die al zijn Inge schreven bij intune, maakt u een app in intune om de Configuration Manager-client te implementeren. Gebruik de [opdracht regel om Configuration Manager-client te installeren](#command-line-to-install-configuration-manager-client) wanneer u de stappen door lopen om [clients van Internet te installeren met behulp van Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Configuration Manager-workloads overschakelen naar Intune
In de vorige sectie hebt u Windows 10-apparaten voor bereid voor co-beheer. Deze apparaten zijn nu gekoppeld aan AD en Azure AD, en ze zijn geregistreerd bij intune en hebben de Configuration Manager-client. Waarschijnlijk zijn er nog steeds Windows 10-apparaten die zijn gekoppeld aan AD en die de Configuration Manager-client hebben, maar niet zijn toegevoegd aan Azure AD of zijn Inge schreven bij intune. De volgende procedure bevat de stappen voor het inschakelen van co-beheer, het voorbereiden van de rest van uw Windows 10-apparaten (Configuration Manager-clients zonder registratie van intune) voor co-beheer, en u kunt aan de slag gaan met het overschakelen van specifieke Configuration Manager workloads naar intune.

1. Ga in de Configuration Manager-console naar **beheer** > **overzicht** > **Cloud Services** > **co-beheer**.    
2. Kies op het tabblad Start in de groep beheren de optie **co-beheer configureren** om de wizard voor het onboarden van co-beheer te openen.    
3. Klik op de pagina abonnement op **Aanmelden** en meld u aan bij uw intune-Tenant en klik vervolgens op **volgende**.   
4. Configureer op de pagina voor fase ring de volgende instellingen en klik vervolgens op **volgende**:
    - **Test groep**: de test groep bevat een of meer verzamelingen die u selecteert. Gebruik deze groep als onderdeel van de gefaseerde implementatie van co-beheer. U kunt beginnen met een kleine test verzameling en vervolgens meer verzamelingen toevoegen aan de test groep bij het samen vouwen van co-beheer naar meer gebruikers en apparaten. U kunt de verzamelingen in de test groep op elk gewenst moment wijzigen in de eigenschappen voor co-beheer.
    - **Productie**: wanneer u deze instelling selecteert, worden alle ondersteunde Windows 10-apparaten ingeschakeld voor co-beheer. Configureer de **uitsluitings groep** met een of meer verzamelingen. Apparaten die lid zijn van een van de verzamelingen in deze groep, worden uitgesloten van het gebruik van co-beheer. 
5. Kies op de pagina Activering de optie **pilot** of **alle** (afhankelijk van de instellingen die u hebt geconfigureerd op de pagina staging) om automatische inschrijving in intune in te scha kelen en klik vervolgens op **volgende**. Wanneer u **pilot**kiest, worden alleen de Configuration Manager-clients die lid zijn van de test groep automatisch Inge schreven bij intune. Zo kunt u co-beheer inschakelen op een subset van clients om het co-beheer te testen en met behulp van een gefaseerde aanpak. 
6. Kies op de pagina workloads of u wilt overschakelen Configuration Manager workloads die worden beheerd door intune en klik vervolgens op **volgende**. Gebruik de schuif regelaars om te selecteren of u de werk belasting wilt overschakelen naar de test groep of voor alle Windows 10-clients (afhankelijk van de instellingen die u hebt geconfigureerd op de test pagina). 
7. Voltooi de wizard om co-beheer in te scha kelen.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Zie ook
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking. 

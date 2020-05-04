---
title: Client beveiliging en privacy
titleSuffix: Configuration Manager
description: Meer informatie over beveiliging en privacy voor Configuration Manager-clients.
ms.date: 07/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4922502b49ab2da9ce393fab809e4dc583fd962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714008"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Beveiliging en privacy voor Configuration Manager-clients

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel worden beveiligings-en privacy-informatie voor Configuration Manager-clients beschreven. Het bevat ook informatie voor mobiele apparaten die worden beheerd door de [Exchange Server-connector](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-clients"></a><a name="BKMK_Security_Clients"></a>Aanbevolen beveiligings procedures voor clients  

Op de Configuration Manager-site worden gegevens geaccepteerd van apparaten waarop de Configuration Manager-client wordt uitgevoerd. Dit gedrag introduceert het risico dat de clients de site aanvallen. Ze kunnen bijvoorbeeld een ongeldige inventaris versturen of proberen om de sitesystemen te overbelasten. Implementeer de Configuration Manager-client alleen naar apparaten die u vertrouwt. Gebruik bovendien de volgende aanbevolen procedures voor beveiliging om de site te helpen beschermen tegen rogue of aangetaste apparaten:  

### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>Open bare-sleutel infrastructuur (PKI)-certificaten gebruiken voor client communicatie met site systemen die IIS uitvoeren  

- Configureer **Sitesysteeminstellingen** voor **alleen HTTPS** als een site-eigenschap.  

- Installeer clients met de `UsePKICert` CCMSetup-eigenschap.  

- Gebruik een certificaatintrekkingslijst (CRL) en zorg ervoor dat clients en communicerende servers er altijd toegang tot hebben.  

Voor clients van mobiele apparaten en bepaalde Internet-clients zijn deze certificaten vereist. Micro soft raadt deze certificaten aan voor alle client verbindingen op het intranet.  

Zie [PKI-certificaat vereisten](../../../plan-design/network/pki-certificate-requirements.md)voor meer informatie over de vereisten voor PKI-certificaten en hoe deze worden gebruikt om Configuration Manager te beveiligen.  

### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Clientcomputers van vertrouwde domeinen automatisch goedkeuren en andere computers handmatig controleren en goedkeuren  

Wanneer u PKI-verificatie niet kunt gebruiken, identificeert goed keuring een computer die u vertrouwt om te worden beheerd door Configuration Manager. De hiërarchie bevat de volgende opties voor het configureren van de client goedkeuring:  

- Handmatig
- Automatisch voor computers in vertrouwde domeinen
- Automatisch voor alle computers  

De veiligste goedkeurings methode is het automatisch goed keuren van clients die lid zijn van vertrouwde domeinen. Vervolgens moet u alle andere computers hand matig controleren en goed keuren. Het automatisch goed keuren van alle clients wordt niet aanbevolen, tenzij u andere toegangs controles hebt om onbetrouwbare computers de toegang tot uw netwerk te voor komen.  

Zie [clients beheren vanaf het knoop punt apparaten](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)voor meer informatie over het hand matig goed keuren van computers.  

### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>Vertrouw niet op blok keren om te voor komen dat clients toegang krijgen tot de Configuration Manager-hiërarchie  

Geblokkeerde clients worden geweigerd door de Configuration Manager-infra structuur. Als clients zijn geblokkeerd, kunnen ze niet communiceren met site systemen om beleid te downloaden, inventaris gegevens te uploaden of status berichten te verzenden.

Blok keren is ontworpen voor de volgende scenario's:

- Verloren of gemanipuleerde opstart media blok keren wanneer u een besturings systeem implementeert naar clients
- Wanneer alle site systemen HTTPS-client verbindingen accepteren

Wanneer site systemen HTTP-client verbindingen accepteren, vertrouwt u niet op blok keren om de Configuration Manager-hiërarchie van niet-vertrouwde computers te beveiligen. In dit scenario kan een geblokkeerde client de site opnieuw samen voegen met een nieuw zelfondertekend certificaat en hardware-ID.

Het intrekken van certificaten is de belangrijkste verdediging tegen mogelijk aangetaste certificaten. Een certificaatintrekkingslijst (CRL) is alleen beschikbaar vanuit een ondersteunde open bare-sleutel infrastructuur (PKI). Het blok keren van clients in Configuration Manager biedt een tweede verdedigings linie om uw hiërarchie te beschermen.  

Zie [bepalen of clients moeten worden geblokkeerd](determine-whether-to-block-clients.md)voor meer informatie.  

### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Gebruik de veiligste client installatie methoden die praktisch zijn voor uw omgeving  

- Voor domeincomputers zijn installatie van groepsbeleid van de client en installatie van de client via software-updates veiliger dan een clientpushinstallatie.  

- Als u toegangs beheer en besturings elementen voor wijzigingen toepast, kunt u gebruikmaken van Imaging en hand matige installatie methoden.  

- Gebruik in versie 1806 of hoger Kerberos wederzijdse verificatie met client push installatie.  

Van alle client installatie methoden is client push installatie het minst veilig vanwege de vele afhankelijkheden. Deze afhankelijkheden omvatten lokale beheer machtigingen, de admin $-share en firewall-uitzonde ringen. Het aantal en type van deze afhankelijkheden verhogen uw kwets baarheid.  

Vanaf versie 1806, wanneer client push wordt gebruikt, kan de site Kerberos wederzijdse verificatie vereisen door geen terugval toe te staan op NTLM voordat de verbinding tot stand wordt gebracht. Deze verbetering helpt bij het beveiligen van de communicatie tussen de server en de client. Zie [clients installeren met client push](../deploy-clients-to-windows-computers.md#BKMK_ClientPush)voor meer informatie.<!--1358204-->  

Zie [client installatie methoden](client-installation-methods.md)voor meer informatie over de verschillende client installatie methoden.  

Selecteer waar mogelijk een client installatie methode die de minste beveiligings machtigingen vereist in Configuration Manager. Beperk de gebruikers met beheerders rechten die beveiligings rollen hebben toegewezen met machtigingen die kunnen worden gebruikt voor andere doel einden dan client implementatie. Voor het configureren van automatische Client upgrades is bijvoorbeeld de beveiligingsrol **volledige beheerder** vereist, waarmee een gebruiker met beheerders rechten alle beveiligings machtigingen toekent.  

Zie voor meer informatie over de afhankelijkheden en beveiligings machtigingen die voor elke client installatie methode zijn vereist ' afhankelijkheden van installatie methoden ' in [vereisten voor computer-clients](../prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>Als u clientpushinstallatie moet gebruiken, dient u bijkomende stappen te nemen om het Clientpushinstallatieaccount te beveiligen.  

Dit account moet lid zijn van de lokale groep **Administrators** op elke computer die de Configuration Manager-client installeert. Voeg nooit het account voor push-installatie van de client toe aan de groep **domein Administrators** . Maak in plaats daarvan een globale groep en voeg die globale groep vervolgens toe aan de lokale groep **Administrators** op uw clients. Maak een groeps beleidsobject om een beperkte groeps instelling toe te voegen om het client push installatie account toe te voegen aan de lokale groep **Administrators** .  

Maak voor extra beveiliging meerdere accounts voor push-installatie van clients, elk met beheerders toegang tot een beperkt aantal computers. Als er met één account is geknoeid, zijn alleen de client computers waarvoor dat account toegang heeft, aangetast.  

### <a name="remove-certificates-before-imaging-clients"></a>Certificaten verwijderen vóór Imaging-clients  

Wanneer u clients implementeert met behulp van installatie kopieën van het besturings systeem, moet u certificaten altijd verwijderen voordat u de installatie kopie vastlegt. Deze certificaten bevatten PKI-certificaten voor client verificatie en zelfondertekende certificaten. Als u deze certificaten niet verwijdert, kunnen clients elkaar imiteren. U kunt de gegevens voor elke client niet verifiëren.  

Zie [een taken reeks maken voor het vastleggen van een besturings systeem](../../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)voor meer informatie.  

### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Zorg ervoor dat de Configuration Manager computer-clients een geautoriseerde kopie van deze certificaten verkrijgen  

#### <a name="the-configuration-manager-trusted-root-key-certificate"></a>Het Configuration Manager vertrouwde basis sleutel certificaat  

Wanneer beide van de volgende-instructies waar zijn, vertrouwen clients op de Configuration Manager vertrouwde basis sleutel om geldige beheer punten te verifiëren:  

- U hebt het Active Directory schema voor Configuration Manager niet uitgebreid
- Clients gebruiken geen PKI-certificaten wanneer ze communiceren met beheer punten  

In dit scenario hebben clients geen manier om te controleren of het beheer punt wordt vertrouwd voor de hiërarchie, tenzij ze de vertrouwde basis sleutel gebruiken. Zonder de vertrouwde basissleutel kan een ervaren aanvaller clients omleiden naar een rogue beheerpunt.  

Wanneer clients de Configuration Manager vertrouwde basis sleutel niet kunnen downloaden uit de globale catalogus of door PKI-certificaten te gebruiken, dient u de clients vooraf in te richten met de vertrouwde basis sleutel. Met deze actie zorgt u ervoor dat ze niet kunnen worden omgeleid naar een Rogue-beheer punt. Zie [planning voor de vertrouwde basis sleutel](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)voor meer informatie.  

#### <a name="the-site-server-signing-certificate"></a>Het handtekeningcertificaat van de siteserver  

Clients gebruiken dit certificaat om te controleren of de site server het beleid heeft ondertekend dat is gedownload van een beheer punt. Dit certificaat wordt zelfondertekend door de siteserver en gepubliceerd naar Active Directory Domain Services.  

Wanneer clients het handtekening certificaat van de site server niet kunnen downloaden uit de globale catalogus, downloaden ze dit standaard van het beheer punt. Als het beheer punt wordt blootgesteld aan een niet-vertrouwd netwerk, zoals het Internet, installeert u het handtekening certificaat van de site server hand matig op clients. Met deze actie zorgt u ervoor dat het niet-gemanipuleerde client beleid van een aangetast beheer punt niet kan worden gedownload.  

Gebruik de eigenschap **SMSSIGNCERT** van CCMSetup client.msi om het handtekeningcertificaat van de siteserver handmatig te installeren. Zie [over eigenschappen van client installatie](../about-client-installation-properties.md)voor meer informatie.  

### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>Gebruik automatische site toewijzing niet als de client de vertrouwde basis sleutel downloadt van het eerste beheer punt waarmee het contact opneemt  

Om het risico te voor komen dat een nieuwe client de vertrouwde basis sleutel downloadt van een Rogue-beheer punt, gebruikt u alleen automatische site toewijzing in de volgende scenario's:  

- De client heeft toegang tot Configuration Manager site-informatie die is gepubliceerd op Active Directory Domain Services.  

- U richt de client vooraf in met de vertrouwde basissleutel.  

- U kunt PKI-certificaten gebruiken van een bedrijfscertificeringsinstantie om het vertrouwen tussen de client en het beheerpunt vast te leggen.  

Zie [planning voor de vertrouwde basis sleutel](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)voor meer informatie over de vertrouwde basis sleutel.  

### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>Clientcomputers installeren met de optie SMSDIRECTORYLOOKUP = NoWINS van CCMSetup Client.msi  

Active Directory Domain Services gebruiken is de meest beveiligde servicelocatiemethode voor clients om sites en beheerpunten te vinden. Soms is deze methode niet mogelijk voor sommige omgevingen. Omdat u bijvoorbeeld het Active Directory schema voor Configuration Manager niet kunt uitbreiden of omdat clients zich in een niet-vertrouwd forest of een werk groep bevinden. Als deze methode niet mogelijk is, gebruikt u DNS-publicatie als een alternatieve service locatie methode. Als beide methoden mislukken en wanneer het beheer punt niet is geconfigureerd voor HTTPS-client verbindingen, kunnen clients terugvallen op het gebruik van WINS.  

Publiceren naar WINS is minder veilig dan de andere publicatie methoden. Configureer de client computers zo dat deze niet terugvallen op het gebruik van WINS door **SMSDIRECTORYLOOKUP = ' WINS**' op te geven. Als u WINS moet gebruiken voor service locatie, gebruikt u **SMSDIRECTORYLOOKUP = WINSSECURE**. Dit is de standaardinstelling. Hierbij wordt gebruikgemaakt van de Configuration Manager vertrouwde basis sleutel om het zelfondertekende certificaat van het beheer punt te valideren.  

> [!NOTE]  
> Wanneer u de-client configureert voor **SMSDIRECTORYLOOKUP = WINSSECURE** en een beheer punt van WINS vindt, controleert de client zijn kopie van de Configuration Manager vertrouwde basis sleutel in WMI.  
>
> Als de hand tekening van het certificaat van het beheer punt overeenkomt met de kopie van de vertrouwde basis sleutel van de client, wordt het certificaat gevalideerd. Na het valideren van het certificaat communiceert de client met het beheer punt dat het heeft gevonden met behulp van WINS.  
>
> Als de hand tekening op het beheer punt certificaat niet overeenkomt met de kopie van de vertrouwde basis sleutel van de client, is het certificaat niet geldig. In dit scenario communiceert de client niet met het beheer punt dat is gevonden met behulp van WINS.  

### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Zorg ervoor dat de onderhoudsvensters groot genoeg zijn om kritieke software-updates te implementeren  

Onderhouds Vensters voor Apparaatsets beperken de tijden waarop Configuration Manager software op deze apparaten kan installeren. Als u het onderhouds venster te klein configureert, is het mogelijk dat de client geen essentiële software-updates installeert. Dit gedrag zorgt ervoor dat de client kwetsbaar is voor aanvallen die de software-update vermindert.  

### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Neem extra beveiligings maatregelen om de kwets baarheid op Windows Embedded-apparaten met schrijf filters te verminderen  

Wanneer u schrijf filters op Windows Embedded-apparaten inschakelt, worden software-installaties of-wijzigingen alleen aan de overlay toegevoegd. Deze wijzigingen blijven niet behouden nadat het apparaat opnieuw is opgestart. Als u Configuration Manager gebruikt om de schrijf filters uit te scha kelen, is het Inge sloten apparaat in deze periode kwetsbaar voor wijzigingen aan alle volumes. Deze volumes bevatten gedeelde mappen.  

Configuration Manager wordt de computer tijdens deze periode vergrendeld zodat alleen lokale beheerders zich kunnen aanmelden. Neem, indien mogelijk, extra beveiligings maatregelen om de computer te beveiligen. Schakel bijvoorbeeld extra beperkingen in voor de firewall.  

Als u onderhouds Vensters gebruikt om wijzigingen te behouden, moet u deze Windows zorgvuldig plannen. Minimaliseer de tijd dat schrijf filters zijn uitgeschakeld, maar zorg dat ze lang genoeg zijn om software-installaties toe te staan en opnieuw op te starten.  

### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>De nieuwste client versie gebruiken met client installatie op basis van software-updates

Als u client installatie op basis van software-updates gebruikt en een nieuwere versie van de client op de site installeert, moet u de gepubliceerde software-update bijwerken. Daarna ontvangen clients de nieuwste versie van het software-update punt.  

Wanneer u de site bijwerkt, wordt de software-update voor client implementatie die naar het software-update punt is gepubliceerd, niet automatisch bijgewerkt. Publiceer de Configuration Manager-client opnieuw naar het software-update punt en werk het versie nummer bij.  

Zie [Configuration Manager-clients installeren met behulp van installatie op basis van software-updates](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP)voor meer informatie.  

### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>Invoer van BitLocker-pincode alleen onderbreken op apparaten met vertrouwde en beperkte toegang  

Configureer de client instelling alleen om **BitLocker-pincode bij opnieuw opstarten** in te stellen op **altijd** voor computers die u vertrouwt en die beperkte fysieke toegang hebben.

Wanneer u deze client instelling instelt op **altijd**, kan Configuration Manager de installatie van de software volt ooien. Dit gedrag helpt bij het installeren van essentiële software-updates en het hervatten van services. Als een aanvaller het proces voor het opnieuw opstarten onderschept, kan deze de controle over de computer overnemen. Gebruik deze instelling alleen wanneer u de computer vertrouwt en wanneer fysieke toegang tot de computer is beperkt. Deze instelling is bijvoorbeeld mogelijk geschikt voor servers in een Data Center.  

Zie [over client instellingen](../about-client-settings.md#suspend-bitlocker-pin-entry-on-restart)voor meer informatie over deze client instelling.  

### <a name="dont-bypass-powershell-execution-policy"></a>Het Power shell-uitvoerings beleid niet overs Laan

Als u de Configuration Manager client instelling configureert voor het uitvoeren van het **Power shell-uitvoerings beleid** om **over te slaan**, kunnen niet-ondertekende Power shell-scripts worden uitgevoerd door Windows. Dit gedrag kan toestaan dat schadelijke software wordt uitgevoerd op client computers. Als uw organisatie deze optie vereist, gebruikt u een aangepaste client instelling. Wijs het toe aan alleen de client computers die niet-ondertekende Power shell-scripts moeten uitvoeren.  

Zie [over client instellingen](../about-client-settings.md#powershell-execution-policy)voor meer informatie over deze client instelling.  


## <a name="security-best-practices-for-mobile-devices"></a><a name="bkmk_mobile"></a>Aanbevolen beveiligings procedures voor mobiele apparaten  

### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Installeer het proxy punt voor inschrijving in een perimeter netwerk en het inschrijvings punt op het intranet  

Installeer het proxy punt voor inschrijving in een perimeter netwerk en het inschrijvings punt op het intranet voor mobiele apparaten op Internet die u registreert bij Configuration Manager. Deze scheiding van rollen help om het proxypunt voor inschrijving te beveiligen tegen een aanval. Als een aanvaller het inschrijvings punt inbreuk maakt, kunnen ze certificaten voor verificatie verkrijgen. Ze kunnen ook de referenties stelen van gebruikers die hun mobiele apparaten inschrijven.  

### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>De wachtwoord instellingen configureren om mobiele apparaten te beveiligen tegen onbevoegde toegang  

*Voor mobiele apparaten die zijn Inge schreven door Configuration Manager*: gebruik een configuratie-item voor een mobiel apparaat om de wachtwoord complexiteit als pincode te configureren. Geef ten minste de standaard minimale wachtwoord lengte op.  

*Voor mobiele apparaten waarop de Configuration Manager-client niet is geïnstalleerd, maar die worden beheerd door de Exchange Server-connector*: Configureer de **wachtwoord instellingen** voor de Exchange Server-connector, zodat de complexiteit van het wacht woord de pincode is. Geef ten minste de standaard minimale wachtwoord lengte op.  

### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Alleen toestaan dat toepassingen worden uitgevoerd die zijn ondertekend door bedrijven die u vertrouwt  

Helpt te voor komen dat inventaris informatie en status gegevens knoeien door te zorgen dat toepassingen alleen worden uitgevoerd wanneer ze zijn ondertekend door bedrijven die u vertrouwt. Niet toestaan dat apparaten niet-ondertekende bestanden installeren.  

*Voor mobiele apparaten die zijn Inge schreven door Configuration Manager*: gebruik een configuratie-item van een mobiel apparaat om de beveiligings instelling **niet-ondertekende toepassingen** te configureren als **verboden**. Configureer **installatie van niet-ondertekende bestanden** als een vertrouwde bron.  

*Voor mobiele apparaten waarop de Configuration Manager-client niet is geïnstalleerd, maar die worden beheerd door de Exchange Server-connector*: Configureer de **Toepassings instellingen** voor de Exchange Server-connector zodanig dat **installatie van niet-ondertekend bestand** en **niet-ondertekende toepassingen** niet zijn **toegestaan**.  

### <a name="lock-mobile-devices-when-not-in-use"></a>Mobiele apparaten vergren delen als ze niet worden gebruikt  

Help-uitbrei ding van bevoegdheden voor komen door het mobiele apparaat te vergren delen wanneer dit niet wordt gebruikt.

*Voor mobiele apparaten die zijn Inge schreven door Configuration Manager*: gebruik een configuratie-item van een mobiel apparaat om de wachtwoord instelling **niet-actieve tijd in minuten voordat het mobiele apparaat wordt vergrendeld**te configureren.  

*Voor mobiele apparaten waarop de Configuration Manager-client niet is geïnstalleerd, maar die worden beheerd door de Exchange Server-connector*: Configureer de **wachtwoord instellingen** voor de Exchange Server-connector om de **niet-actieve tijd in minuten in te stellen voordat het mobiele apparaat wordt vergrendeld**.  

### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Beperk de gebruikers die hun mobiele apparaten kunnen inschrijven  

Help-uitbrei ding van bevoegdheden te voor komen door de gebruikers te beperken die hun mobiele apparaten kunnen registreren. Gebruik een aangepaste clientinstelling in plaats van standaardclientinstellingen om alleen geautoriseerde gebruikers toe te staan hun mobiele apparaten te registreren.  

### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Richt lijnen voor affiniteit tussen gebruikers en apparaten voor mobiele apparaten  

Implementeer geen toepassingen voor gebruikers die mobiele apparaten hebben Inge schreven door Configuration Manager of Microsoft Intune in de volgende scenario's:  

- Het mobiele apparaat wordt door meer dan één persoon gebruikt.  

- Het apparaat wordt namens een gebruiker geregistreerd door een beheerder.  

- Het apparaat wordt overgedragen aan een andere persoon zonder het apparaat buiten gebruik te stellen en vervolgens opnieuw in te schrijven.  

Met apparaatregistratie maakt u een affiniteits relatie tussen gebruikers en apparaten. Deze relatie is een toewijzing van de gebruiker die de inschrijving uitvoert op het mobiele apparaat. Als een andere gebruiker het mobiele apparaat gebruikt, kunnen ze de toepassingen uitvoeren die zijn geïmplementeerd voor de oorspronkelijke gebruiker. Dit kan leiden tot een verhoging van bevoegdheden. En als een beheerder het mobiele apparaat inschrijft voor een gebruiker, worden toepassingen die zijn geïmplementeerd voor de gebruiker niet geïnstalleerd op het mobiele apparaat. In plaats daarvan kunnen toepassingen die worden geïmplementeerd naar de beheerder, worden geïnstalleerd.  

In tegens telling tot de affiniteit tussen gebruikers en apparaten voor Windows-computers, kunt u de informatie over de affiniteit van gebruikers apparaten niet hand matig definiëren voor mobiele apparaten die zijn Inge schreven door Microsoft Intune.  

Als u het eigendom overdraagt van een mobiel apparaat dat is inge schreven door intune, moet u eerst het mobiele apparaat buiten gebruik stellen vanuit intune. Met deze actie wordt de relatie van de gebruikers affiniteit met apparaat verwijderd. Vraag de huidige gebruiker vervolgens het apparaat opnieuw in te schrijven.  

### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Zorg ervoor dat gebruikers hun eigen mobiele apparaten registreren voor Microsoft Intune  

Er wordt een relatie tussen het apparaat en de gebruikers affiniteit gemaakt tijdens de registratie. Met deze actie wordt de gebruiker toegewezen die de inschrijving uitvoert op het mobiele apparaat. Als een beheerder het mobiele apparaat voor een gebruiker registreert, worden toepassingen die voor de gebruiker zijn geïmplementeerd, niet op het mobiele apparaat geïnstalleerd. In plaats daarvan kunnen toepassingen die worden geïmplementeerd naar de beheerder, worden geïnstalleerd.  

### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>De verbinding tussen de Configuration Manager site server en de Exchange-Server beveiligen

Als de Exchange Server on-premises is, gebruikt u IPsec. Gehoste Exchange beveiligt de verbinding automatisch met behulp van SSL.  

### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Het principe van minimale bevoegdheden voor de connector gebruiken  

Zie [mobiele apparaten beheren met Configuration Manager en Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)voor een lijst met de minimale cmdlets die de Exchange Server-connector nodig heeft.  


## <a name="security-best-practices-for-macs"></a><a name="bkmk_macs"></a>Aanbevolen beveiligings procedures voor Macs  

### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>De bron bestanden van de client op een beveiligde locatie opslaan en openen  

Voordat u de client op een Mac-computer installeert of registreert, controleert Configuration Manager niet of deze client bron bestanden zijn gemanipuleerd. Down load deze bestanden vanaf een betrouw bare bron. Sla ze veilig op en open ze.  

### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>De geldigheids periode van het certificaat controleren en bijhouden  

Stel de bedrijfscontinuïteit veilig door de geldigheidsperiode van het certificaat dat voor Mac-computers wordt gebruikt, te controleren en te volgen. Configuration Manager biedt geen ondersteuning voor automatische verlenging van dit certificaat of u krijgt een waarschuwing dat het certificaat bijna verloopt. Een typische geldigheids periode is een jaar.  

Zie het certificaat van [de Mac-client hand matig vernieuwen](../deploy-clients-to-macs.md#renew-the-mac-client-certificate)voor meer informatie over het vernieuwen van het certificaat.  

### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Configureer het vertrouwde basis certificaat alleen voor SSL  

Configureer het certificaat voor de vertrouwde basis certificerings instantie zodat het alleen wordt vertrouwd voor het SSL-protocol om u te helpen beschermen tegen misbruik van bevoegdheden.

Wanneer u Mac-computers registreert, wordt automatisch een gebruikers certificaat geïnstalleerd voor het beheren van de Configuration Manager-client. Dit gebruikers certificaat bevat de vertrouwde basis certificaten in de vertrouwens keten. Als u het vertrouwen van dit basis certificaat alleen wilt beperken tot het SSL-protocol, gebruikt u de volgende procedure:  

1. Open een terminalvenster op de Mac-computer.  

2. Voer de volgende opdracht in:`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3. Klik in het dialoog venster **toegang tot sleutel hanger** in het gedeelte hoofd **ketens** op **systeem**. Klik vervolgens in de sectie **categorie** op **certificaten**.  

4. Zoek en dubbel klik op het basis-CA-certificaat voor het Mac-client certificaat.  

5. Vouw in het dialoogvenster voor het basis-CA-certificaat de sectie **Vertrouwen** uit en breng vervolgens de volgende wijzigingen aan:  

    1. **Wanneer u dit certificaat gebruikt**: Wijzig de instelling **altijd vertrouwen** om de **standaard waarden**van het systeem te gebruiken.  

    2. **Secure Sockets Layer (SSL)**: **Er is geen waarde opgegeven** die is ingesteld op **altijd vertrouwen**.  

6. Sluit het dialoogvenster. Wanneer u hierom wordt gevraagd, voert u het beheerders wachtwoord in en klikt u vervolgens op **instellingen bijwerken**.  

Nadat u deze procedure hebt voltooid, wordt het basis certificaat alleen vertrouwd voor het valideren van het SSL-protocol. Andere protocollen die nu niet worden vertrouwd met dit basis certificaat zijn onder andere beveiligde E-mail (S/MIME), uitbreid bare verificatie (EAP) of ondertekening van programma code.  

> [!NOTE]  
> Gebruik deze procedure ook als u het client certificaat onafhankelijk van Configuration Manager hebt geïnstalleerd.


## <a name="security-issues-for-configuration-manager-clients"></a><a name="BKMK_SecurityIssues_Clients"></a>Beveiligings problemen voor Configuration Manager-clients  

Er zijn voor de volgende beveiligingsproblemen geen matigingsmaatregelen bekend:  

### <a name="status-messages-arent-authenticated"></a>Status berichten worden niet geverifieerd

Er wordt geen verificatie uitgevoerd voor statusberichten. Wanneer een beheerpunt HTTP-clientverbindingen accepteert, kan elk apparaat statusberichten naar het beheerpunt verzenden. Als het beheer punt alleen HTTPS-client verbindingen accepteert, moet een apparaat een geldig client verificatie certificaat hebben, maar kan ook een status bericht verzenden. Het beheer punt verwijdert een ongeldig status bericht dat is ontvangen van een client.  

Er zijn enkele mogelijke aanvallen tegen dit beveiligingslek:

- Een aanvaller zou een pseudo-status bericht kunnen verzenden om lidmaatschap van een verzameling te verkrijgen die is gebaseerd op status bericht query's.
- Elke client zou een DoS-aanval op het beheerpunt kunnen starten door dit met statusberichten te overspoelen.
- Als statusberichten acties in werking stellen via regels voor het statusberichtfilter, zou een kwaadwillend persoon deze regels in werking kunnen stellen.
- Een aanvaller zou status bericht kunnen verzenden waarmee rapport gegevens onjuist worden weer gegeven.  

### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>Beleid kan opnieuw worden afgestemd op clients waarop dit niet is gericht  

Er zijn verschillende methoden die kwaadwillende personen zouden kunnen gebruiken om beleid dat op één client is gericht, toe te passen op een geheel andere client. Een aanvaller op een vertrouwde client zou bijvoorbeeld valse inventaris-of detectie-informatie kunnen verzenden om de computer toe te voegen aan een verzameling waartoe deze geen deel moet uitmaken. Deze client ontvangt vervolgens alle implementaties voor deze verzameling.

Er zijn besturings elementen aanwezig om te voor komen dat kwaadwillende personen het beleid rechtstreeks wijzigen. Aanvallers kunnen echter een bestaand beleid nemen waarmee een besturings systeem opnieuw wordt ingedeeld en opnieuw wordt geïmplementeerd en dit naar een andere computer wordt verzonden. Dit omgeleide beleid kan een denial-of-service tot gevolg hebben. Deze typen aanvallen vereisen een nauw keurige timing en uitgebreide kennis van de Configuration Manager-infra structuur.  

### <a name="client-logs-allow-user-access"></a>Clientlogboeken staan gebruikerstoegang toe  

Alle client logboek bestanden staan de groep **gebruikers** met *Lees* toegang toe en de speciale **interactieve** gebruiker met *Schrijf* toegang. Als u uitgebreide logboekregistratie inschakelt, kunnen kwaadwillende personen eventueel de logboekbestanden lezen op zoek naar informatie over kwetsbaarheden op het vlak van het systeem of compatibiliteit. Processen zoals software die de-client installeert in de context van een gebruiker moeten naar Logboeken schrijven met een gebruikers account met een beperkte rechten. Dit kan betekenen dat een aanvaller ook naar de logboeken kan schrijven met een account met beperkte rechten.  

Het ernstigste risico is dat een aanvaller informatie kan verwijderen uit de logboek bestanden. Een beheerder heeft deze informatie mogelijk nodig voor controle en inbraak detectie.  

### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>Een computer kan worden gebruikt voor het verkrijgen van een certificaat dat is ontworpen voor inschrijving van mobiele apparaten  

Wanneer Configuration Manager een inschrijvings aanvraag verwerkt, kan de aanvraag niet worden gecontroleerd vanaf een mobiel apparaat in plaats van vanaf een computer. Als de aanvraag afkomstig is van een computer, kan er een PKI-certificaat worden geïnstalleerd dat het vervolgens kan registreren bij Configuration Manager.

Ter voorkoming van een uitbrei ding van bevoegdheden voor een aanval in dit scenario, mogen alleen vertrouwde gebruikers hun mobiele apparaten inschrijven. Bewaak de activiteiten voor het registreren van apparaten zorgvuldig in de site.  

### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>Een geblokkeerde client kan nog steeds berichten naar het beheer punt verzenden

Wanneer u een client blokkeert die u niet meer vertrouwt, maar er een netwerk verbinding voor client meldingen tot stand is gebracht, wordt de sessie Configuration Manager niet verbroken. De geblokkeerde client kan doorgaan met het verzenden van pakketten naar het beheerpunt, totdat de client de verbinding met het netwerk verbreekt. Deze pakketten zijn alleen kleine, Keep-Alive pakketten. Deze client kan niet worden beheerd door Configuration Manager tot deze is gedeblokkeerd.  

### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>Het beheer punt wordt niet gecontroleerd door automatische client upgrade

Wanneer u automatische client upgrade gebruikt, kan de client worden omgeleid naar een beheer punt om de bron bestanden van de client te downloaden. In dit scenario verifieert de client het beheer punt niet als een vertrouwde bron.  

### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>Wanneer gebruikers eerst Mac-computers inschrijven, zijn ze kwetsbaar voor DNS-spoofing  

Wanneer de Mac-computer tijdens het inschrijven verbinding maakt met het proxy punt voor inschrijving, is het onwaarschijnlijk dat de Mac-computer al beschikt over het vertrouwde basis-CA-certificaat. Op dit moment vertrouwt de Mac-computer de server niet en wordt de gebruiker gevraagd om door te gaan. Als een Rogue DNS-server de Fully Qualified Domain Name (FQDN) van het inschrijvings proxy punt zet, kan de Mac-computer worden doorgestuurd naar een proxy punt voor Rogue-inschrijving om certificaten van een niet-vertrouwde bron te installeren. Volg de aanbevolen procedures voor het vermijden van DNS-vervalsing in uw omgeving om dit risico te reduceren.  

### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>Mac-inschrijving beperkt certificaat aanvragen niet  

Telkens wanneer er een nieuw certificaat wordt aangevraagd, kunnen gebruikers hun Mac-computer opnieuw inschrijven. Configuration Manager controleert niet op meerdere aanvragen of beperkt het aantal aangevraagde certificaten op een enkele computer. Een Rogue-gebruiker kan een script uitvoeren dat de aanvraag voor de inschrijving van de opdracht regel herhaalt. Deze aanval kan leiden tot een denial of service op het netwerk of op de verlenende certificerings instantie (CA). Controleer de uitgevende certificeringsinstantie nauwlettend op dit type verdacht gedrag om dit risico te reduceren. Blok keer direct vanuit de Configuration Manager hiërarchie elke computer die dit gedrags patroon weergeeft.  

### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>Bij een bevestiging van wissen wordt niet gecontroleerd of het apparaat is gewist  

Wanneer u een actie voor wissen initieert voor een mobiel apparaat en Configuration Manager het wissen bevestigt, is de verificatie dat het bericht Configuration Manager *verzonden* . Er wordt niet gecontroleerd of het apparaat op de aanvraag heeft *gehandeld* .

Voor mobiele apparaten die worden beheerd door de Exchange Server-connector, wordt met een bevestiging voor wissen gecontroleerd of de opdracht is ontvangen door Exchange, niet door het apparaat.  

### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Als u de opties gebruikt om wijzigingen door te voeren op Windows Embedded-apparaten, is het mogelijk dat accounts eerder dan verwacht worden vergrendeld  

Als op het Windows Embedded-apparaat een versie van het besturings systeem wordt uitgevoerd dat ouder is dan Windows 7 en een gebruiker probeert zich aan te melden terwijl de schrijf filters zijn uitgeschakeld door Configuration Manager, staat Windows slechts een helft van het geconfigureerde aantal mislukte pogingen toe voordat het account wordt vergrendeld.

U kunt bijvoorbeeld het domein beleid voor de **drempel waarde voor account vergrendeling** instellen op zes pogingen. Een gebruiker typt het wacht woord drie keer en het account is vergrendeld. Dit gedrag zorgt ervoor dat een denial of service wordt gemaakt. Als gebruikers zich in dit scenario moeten aanmelden bij embedded-apparaten, moet u zich ervan op de hoogte brengen van de kans op een beperkt vergrendelings drempel.  


## <a name="privacy-information-for-configuration-manager-clients"></a><a name="BKMK_Privacy_Clients"></a>Privacy-informatie voor Configuration Manager-clients  

Wanneer u de Configuration Manager-client implementeert, schakelt u client instellingen voor Configuration Manager-functies in. De instellingen die u gebruikt om de functies te configureren, kunnen van toepassing zijn op alle clients in de hiërarchie van de Configuration Manager. Dit gedrag is hetzelfde, ongeacht of ze rechtstreeks zijn verbonden met het interne netwerk, via een externe sessie zijn verbonden of verbinding hebben met internet.  

Client informatie wordt opgeslagen in de Configuration Manager-data base in uw SQL-Server en wordt niet naar micro soft verzonden. Gegevens worden bewaard in de data base tot deze worden verwijderd door de site-onderhouds taken **verouderde detectie gegevens** elke 90 dagen verwijderen. U kunt het verwijderingsinterval configureren. 

Sommige samenvattings-of aggregatie-en gebruiks gegevens worden naar micro soft verzonden. Zie [diagnostiek en gebruiks gegevens](../../../plan-design/diagnostics/diagnostics-and-usage-data.md)voor meer informatie.  

Voordat u de Configuration Manager-client configureert, moet u rekening houden met uw privacy-vereisten.  

Meer informatie over het verzamelen van gegevens en het gebruik van micro soft vindt u in de [privacyverklaring van micro soft](https://privacy.microsoft.com/privacystatement).

### <a name="client-status"></a>Clientstatus  

Configuration Manager de activiteit van clients controleert. De Configuration Manager-client wordt periodiek geëvalueerd en kan problemen met de client en de bijbehorende afhankelijkheden oplossen. De client status is standaard ingeschakeld. Hierbij worden metrische gegevens aan de server zijde gebruikt voor de controles van client activiteiten. Client status maakt gebruik van acties aan de client zijde voor zelf controle, herstel en het verzenden van client status gegevens naar de site. De client voert de zelf controles uit volgens een schema dat u configureert. De client verzendt de resultaten van de controles naar de Configuration Manager-site. Deze gegevens zijn versleuteld tijdens de overdracht.  

Client status informatie wordt opgeslagen in de Configuration Manager-data base in uw SQL-Server en wordt niet naar micro soft verzonden. De informatie wordt niet in een versleutelde indeling opgeslagen in de site database. Deze informatie wordt bewaard in de data base tot deze wordt verwijderd volgens de waarde die is geconfigureerd voor de **geschiedenis van de client status behouden voor het volgende aantal dagen voor de** client status instelling. De standaardwaarde voor deze instelling is elke 31 dagen.  

Houd rekening met de vereisten van uw privacy voordat u de Configuration Manager-client installeert met client status controle.  


## <a name="privacy-information-for-mobile-devices-that-are-managed-with-the-exchange-server-connector"></a><a name="BKMK_Privacy_ExchangeConnector"></a>Privacy-informatie voor mobiele apparaten die worden beheerd met de Exchange Server-connector  

De Exchange Server-connector zoekt en beheert apparaten die verbinding maken met een on-premises of gehoste Exchange-server met behulp van het ActiveSync-protocol. De records die worden gevonden door de Exchange Server-connector, worden opgeslagen in de Configuration Manager-data base in uw SQL-Server. De gegevens worden verzameld van de Exchange-Server. Het bevat geen aanvullende informatie van wat de mobiele apparaten naar Exchange server verzenden.  

De gegevens van mobiele apparaten worden niet naar micro soft verzonden. De gegevens van mobiele apparaten worden opgeslagen in de Configuration Manager-data base in uw SQL-Server. Informatie wordt bewaard in de data base totdat deze wordt verwijderd door de site onderhouds taak **verouderde detectie gegevens** elke 90 dagen verwijderen. U kunt het verwijderings interval configureren.  

Denk na over uw privacyvereisten voordat u de Exchange Server-connector installeert en configureert.  

Meer informatie over het verzamelen van gegevens en het gebruik van micro soft vindt u in de [privacyverklaring van micro soft](https://privacy.microsoft.com/privacystatement).

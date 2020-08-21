---
title: Clients implementeren in Windows
titleSuffix: Configuration Manager
description: Meer informatie over het implementeren van de Configuration Manager-client op Windows-computers.
ms.date: 09/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2eea75f39430f1cc38ff994280425ca918eaa432
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694556"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Clients implementeren op Windows-computers in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u informatie over het implementeren van de Configuration Manager-client op Windows-computers. Zie de volgende artikelen voor meer informatie over het plannen en voorbereiden van de implementatie van de client:

- [Clientinstallatiemethoden](plan/client-installation-methods.md)  
- [Vereisten voor het implementeren van clients op Windows-computers](prerequisites-for-deploying-clients-to-windows-computers.md)
- [Beveiliging en privacy voor Configuration Manager-clients](plan/security-and-privacy-for-clients.md)  
- [Aanbevolen procedures voor de implementatie van clients](plan/best-practices-for-client-deployment.md)  


## <a name="client-push-installation"></a><a name="BKMK_ClientPush"></a> Push-client installatie

Er zijn drie belang rijke manieren om client-push te gebruiken:  

- Wanneer u Push-client installatie voor een site configureert, wordt de client installatie automatisch uitgevoerd op computers die de site detecteert. Deze methode ligt binnen het bereik van de geconfigureerde grenzen van de site wanneer deze grenzen als een grens groep zijn geconfigureerd.  

- Start de Push-client installatie door de wizard Push-client installatie uit te voeren voor een specifieke verzameling of bron binnen een verzameling.  

- Gebruik de wizard Push-client installatie om de Configuration Manager-client te installeren, die u kunt gebruiken om een [query](../../servers/manage/introduction-to-queries.md) uit te voeren op het resultaat. De installatie slaagt alleen als een van de items die door de query zijn geretourneerd, het kenmerk **ResourceID** van de **bron klasse System** .

Als de site server geen verbinding kan maken met de client computer of het installatie proces start, wordt de installatie elk uur automatisch opnieuw geprobeerd. De server blijft Maxi maal zeven dagen opnieuw proberen.  

Als u het client installatie proces wilt volgen, installeert u een terugval status punt voordat u de clients installeert. Wanneer u een terugval status punt installeert, wordt het automatisch toegewezen aan clients wanneer ze door de Push-client installatie methode worden geïnstalleerd. Bekijk de client implementatie-en toewijzings rapporten om de voortgang van de client installatie bij te houden.

Client-logboek bestanden bieden gedetailleerde informatie over het oplossen van problemen. Voor de logboek bestanden is geen terugval status punt vereist. Het bestand CCM. log op de site server registreert bijvoorbeeld problemen die zich voordoen wanneer de site server verbinding maakt met de computer. Het bestand CCMSetup. log op de client registreert het installatie proces.  

> [!IMPORTANT]  
> Client push slaagt alleen als aan alle vereisten wordt voldaan. Zie [afhankelijkheden van installatie methoden](prerequisites-for-deploying-clients-to-windows-computers.md#installation-method-dependencies)voor meer informatie.

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>De site configureren om client push automatisch te gebruiken voor gedetecteerde computers

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Selecteer de site waarvoor u automatische Push-client installatie voor de gehele site wilt configureren.  

3. Selecteer op het tabblad **Start** van het lint in de groep **instellingen** de optie **client installatie-instellingen**en selecteer vervolgens **client push installatie**.  

4. Op het tabblad **Algemeen** van de Push-client installatie venster Eigenschappen selecteert u **automatische Push-client installatie voor de gehele site inschakelen**.

5. Vanaf versie 1806, wanneer u de site bijwerkt, is een Kerberos-controle voor client push ingeschakeld. De optie voor het toestaan van een terugval van de **verbinding met NTLM** is standaard ingeschakeld. Dit is consistent met het vorige gedrag. Als de site de client niet kan verifiëren met behulp van Kerberos, wordt de verbinding opnieuw geprobeerd door gebruik te maken van NTLM. De aanbevolen configuratie voor een betere beveiliging is het uitschakelen van deze instelling, waarvoor Kerberos is vereist zonder NTLM-terugval.<!--1358204-->  

    > [!NOTE]  
    > Wanneer client push wordt gebruikt om de Configuration Manager-client te installeren, maakt de site server een externe verbinding met de client. Vanaf versie 1806 kan de site Kerberos wederzijdse verificatie vereisen door geen terugval op NTLM toe te staan voordat de verbinding tot stand wordt gebracht. Deze verbetering helpt bij het beveiligen van de communicatie tussen de server en de client.  
    >
    > Afhankelijk van uw beveiligings beleid heeft uw omgeving mogelijk al een voor keur of is Kerberos vereist voor de oudere NTLM-verificatie. Meer informatie over de beveiligings overwegingen van deze verificatie protocollen vindt [u in de instelling Windows-beveiligings beleid voor het beperken van NTLM](/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    >
    > Als u deze functie wilt gebruiken, moeten clients zich in een vertrouwde Active Directory-forest bevinden. Kerberos in Windows is afhankelijk van Active Directory voor wederzijdse verificatie.  

6. Selecteer de systeem typen waarop Configuration Manager de client software moet pushen. Selecteer of u de-client wilt installeren op domein controllers.  

7. Geef op het tabblad **accounts** een of meer Accounts voor Configuration Manager op die moeten worden gebruikt wanneer verbinding wordt gemaakt met de doel computer. Selecteer het pictogram **maken** , geef de **gebruikers naam** en het **wacht woord** op (Maxi maal 38 tekens), bevestig het wacht woord en selecteer **OK**. Geef ten minste één Push-client installatie account op. Dit account moet lokale beheerders rechten hebben op de doel computer om de client te installeren. Als u geen account voor push-client installatie opgeeft, probeert Configuration Manager het site systeem computer account te gebruiken. De client Push van meerdere domeinen mislukt wanneer het site systeem computer account wordt gebruikt.  

    > [!NOTE]  
    > Als u client push vanaf een secundaire site wilt gebruiken, geeft u het account op de secundaire site op die de client-push start.  
    >
    > Zie de volgende procedure, [de wizard Push-client installatie gebruiken](#use-the-client-push-installation-wizard)voor meer informatie over het client push installatie account.  

8. Geef de vereiste installatie-eigenschappen op het tabblad **installatie-eigenschappen** op.

    Als u het Active Directory schema voor Configuration Manager hebt uitgebreid, worden de opgegeven [client installatie-eigenschappen](about-client-installation-properties.md) door de site naar Active Directory Domain Services gepubliceerd. Wanneer CCMSetup wordt uitgevoerd zonder installatie-eigenschappen, worden deze eigenschappen van Active Directory gelezen.  

    > [!NOTE]  
    > Als u Push-client installatie op een secundaire site inschakelt, stelt u de eigenschap **SMSSITECODE** in op de Configuration Manager site code van de bovenliggende primaire site. Als u het Active Directory schema voor Configuration Manager hebt uitgebreid, stelt u deze eigenschap in op **automatisch**om automatisch de juiste site toewijzing te vinden.

### <a name="use-the-client-push-installation-wizard"></a>De wizard Push-client installatie gebruiken

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Selecteer de site waarvoor u automatische Push-client installatie voor de gehele site wilt configureren.  

3. Selecteer op het tabblad **Start** van het lint in de groep **instellingen** de optie **client installatie-instellingen**en selecteer vervolgens **client push installatie**.  

4. Geef de vereiste installatie-eigenschappen op het tabblad **installatie-eigenschappen** op.  

    Als u het Active Directory schema voor Configuration Manager hebt uitgebreid, worden de opgegeven [client installatie-eigenschappen](about-client-installation-properties.md) door de site naar Active Directory Domain Services gepubliceerd. Wanneer CCMSetup wordt uitgevoerd zonder installatie-eigenschappen, worden deze eigenschappen van Active Directory gelezen.

5. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** .  

6. Selecteer een of meer computers in het knoop punt **apparaten** . Of selecteer een verzameling computers in het knoop punt **apparaat Collections** .  

7. Kies een van de volgende opties op het tabblad **Start** van het lint:  

    - Als u de client naar een of meer apparaten wilt pushen, selecteert u in de groep **apparaat** de optie **client installeren**.  

    - Als u de client naar een verzameling apparaten wilt pushen, selecteert u in de groep **verzameling** de optie **client installeren**.  

8. Lees de informatie op de pagina **voordat u begint** van de wizard Configuration Manager-client installeren en selecteer vervolgens **volgende**.  

9. Selecteer de gewenste opties op de pagina **installatie opties** .  

10. Controleer de installatie-instellingen en voltooi vervolgens de wizard.  

> [!NOTE]  
> Gebruik deze wizard om clients te installeren, zelfs als de site niet is geconfigureerd voor client push.  

## <a name="software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> Installatie op basis van software-updates  

Client installatie op basis van software-updates publiceert de client naar een software-update punt als een software-update. Gebruik deze methode voor een installatie of upgrade voor de eerste keer.  

Als de Configuration Manager-client op een computer is geïnstalleerd, ontvangt de computer client beleid van de site. Dit beleid bevat de server naam van het software-update punt en de poort van waaruit software-updates worden opgehaald.

> [!IMPORTANT]  
> Voor installatie op basis van software-updates gebruikt u dezelfde Windows Server Update Services-server (WSUS) voor client installatie en software-updates. Deze server moet het actieve software-updatepunt in een primaire site zijn. Zie [Software-update punten installeren](../../../sum/get-started/install-a-software-update-point.md)voor meer informatie.

Als de Configuration Manager-client niet is geïnstalleerd op een computer, kunt u een groepsbeleid-object configureren en toewijzen. Met de groepsbeleid geeft u de server naam op van het software-update punt.  

U kunt geen opdracht regel eigenschappen toevoegen aan een client installatie op basis van software-updates. Als u het Active Directory schema voor Configuration Manager hebt uitgebreid, wordt door de client installatie automatisch een query uitgevoerd op Active Directory Domain Services voor de installatie-eigenschappen.  

Als u het Active Directory schema niet hebt uitgebreid, gebruikt u groepsbeleid om instellingen voor client installatie in te richten. Deze instellingen worden automatisch toegepast op client installatie op basis van software-updates. Zie de sectie over het [inrichten van client installatie-eigenschappen](#BKMK_Provision) en het artikel over het toewijzen van [clients aan een site](assign-clients-to-a-site.md)voor meer informatie.  

Gebruik de volgende procedures om computers zonder Configuration Manager-client te configureren voor het gebruik van het software-update punt. Er is ook een procedure voor het publiceren van de-client software naar het software-update punt.  

> [!TIP]  
> Als de computer opnieuw wordt opgestart na een eerdere software-installatie, kan een client installatie op basis van een software-update ertoe leiden dat het systeem opnieuw wordt opgestart.  

### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Een groepsbeleid-object configureren om het software-update punt op te geven  

1. Gebruik de **console Groepsbeleidbeheer** om een nieuw of bestaand Groepsbeleid-object te openen.  

2. Vouw **computer configuratie**, **Beheersjablonen**en **Windows-onderdelen**uit en selecteer vervolgens **Windows Update**.  

3. Open de eigenschappen van de instelling **intranet micro soft-Update service locatie opgeven**en selecteer **ingeschakeld**.  

4. **Stel de update service in het intranet in voor het detecteren van updates**: Geef de naam en poort op van de software-update punt server.  

    - Als u het site systeem van Configuration Manager hebt geconfigureerd voor het gebruik van een Fully Qualified Domain Name (FQDN), gebruikt u die indeling.  

    - Als het Configuration Manager-site systeem niet is geconfigureerd voor het gebruik van een FQDN-naam, gebruikt u een indeling voor korte namen.

    > [!TIP]  
    > Zie [bepalen welke poort instellingen worden gebruikt voor WSUS](../../../sum/plan-design/plan-for-software-updates.md)om het poort nummer te bepalen.

    Voor beeld in FQDN-indeling: `http://server1.contoso.com:8530`  

5. **Intranet server voor statistieken instellen**: deze instelling wordt meestal geconfigureerd met dezelfde server naam.

6. Wijs het groepsbeleid-object toe aan de computers waarop u de client wilt installeren en software-updates wilt ontvangen.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>De Configuration Manager-client publiceren naar het software-update punt  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Selecteer de site waarvoor u client installatie op basis van software-updates wilt configureren.  

3. Op het tabblad **Start** van het lint, in de groep **instellingen** , selecteert u **instellingen voor client installatie**en selecteert u **client installatie op basis van software-updates**.  

4. Selecteer **client installatie op basis van software-updates inschakelen**.  

5. Als de client versie van de site recenter is dan de versie op het software-update punt, wordt het dialoog venster **latere versie van client pakket gedetecteerd** geopend. Selecteer **Ja** om de meest recente versie te publiceren.  

    > [!NOTE]  
    > Dit dialoog venster is leeg als u de-client software nog niet hebt gepubliceerd op het software-update punt.

De software-update voor de Configuration Manager-client wordt niet automatisch bijgewerkt wanneer er een nieuwe versie is. Wanneer u de site bijwerkt, herhaalt u deze procedure om de-client bij te werken.  

## <a name="group-policy-installation"></a><a name="BKMK_ClientGP"></a> Installatie van groepsbeleid

Gebruik groepsbeleid in Active Directory Domain Services om de Configuration Manager-client te publiceren of toe te wijzen. De client wordt geïnstalleerd wanneer de computer wordt opgestart. Wanneer u groepsbeleid gebruikt, wordt de-client weer gegeven in het **onderdeel Software** van het configuratie scherm. De gebruiker kan de app vanaf daar installeren.  

Gebruik het Windows Installer-pakket CCMSetup.msi voor installaties op basis van groepsbeleid. Dit bestand bevindt zich in de `<ConfigMgr installation directory>\bin\i386` map op de site server. U kunt geen eigenschappen toevoegen aan dit bestand om het installatie gedrag te wijzigen.  

> [!IMPORTANT]  
> U moet beheerders machtigingen hebben voor toegang tot de client installatie bestanden.  

- Als u het Active Directory schema voor Configuration Manager hebt uitgebreid en u het domein hebt geselecteerd op het tabblad **publiceren** van het dialoog venster **site-eigenschappen** , zoeken client computers automatisch Active Directory Domain Services op installatie-eigenschappen. Zie [over client installatie-eigenschappen die zijn gepubliceerd op Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md)voor meer informatie.  

- Als u het Active Directory schema niet hebt uitgebreid, raadpleegt u de sectie over het [inrichten van client installatie-eigenschappen](#BKMK_Provision) voor informatie over het opslaan van installatie-eigenschappen in het Windows-REGI ster van computers. De client gebruikt deze installatie-eigenschappen wanneer deze wordt geïnstalleerd.  

Zie [Groepsbeleid gebruiken om software op afstand te installeren](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server)voor meer informatie.  

## <a name="manual-installation"></a><a name="BKMK_Manual"></a> Hand matige installatie

Installeer de-client software hand matig op computers met behulp van CCMSetup.exe. U vindt dit programma en de ondersteunende bestanden in de map client in de installatiemap Configuration Manager op de site server. De site deelt deze map met het netwerk als:  

`\\<site server name>\SMS_<site code>\Client\`  

`<site server name>` is de naam van de primaire site server. `<site code>` is de code van de primaire site waaraan de client is toegewezen. Als u CCMSetup.exe vanaf de opdracht regel op de client wilt uitvoeren, maakt u verbinding met deze netwerk locatie en voert u de opdracht uit.  

> [!IMPORTANT]  
> U moet beheerders machtigingen hebben voor toegang tot de client installatie bestanden.  

CCMSetup.exe kopieert alle benodigde vereisten naar de client computer en roept het Windows Installer pakket (Client.msi) aan om de client te installeren. U kunt Client.msi niet rechtstreeks uitvoeren.  

Als u het gedrag van de client installatie wilt wijzigen, geeft u opdracht regel opties op voor zowel CCMSetup.exe als Client.msi. Zorg ervoor dat u de CCMSetup-para meters opgeeft die beginnen met `/` voordat u Client.msi eigenschappen opgeeft. Bijvoorbeeld:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

In dit voor beeld wordt de client geïnstalleerd met de volgende opties:  

|Optie|Beschrijving|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Deze CCMSetup-para meter geeft het beheer punt SMSMP01 op om de vereiste client installatie bestanden te downloaden.|  
|`/logon`|Met deze CCMSetup-para meter wordt aangegeven dat de installatie moet worden gestopt als er een bestaande Configuration Manager-client op de computer wordt gevonden.|  
|`SMSSITECODE=AUTO`|Deze Client.msi eigenschap geeft aan dat de client probeert om de Configuration Manager site code te zoeken die u wilt gebruiken, bijvoorbeeld door middel van Active Directory Domain Services.|  
|`FSP=SMSFP01`|Deze Client.msi eigenschap geeft aan dat het terugval status punt met de naam SMSFP01 wordt gebruikt om status berichten te ontvangen die vanaf de client computer worden verzonden.|  

Zie [over para meters en eigenschappen van client installatie](about-client-installation-properties.md)voor meer informatie.  

> [!TIP]  
> Zie voor de procedure voor het installeren van de Configuration Manager-client op een modern Windows 10-apparaat met behulp van de identiteit van Azure Active Directory (Azure AD) [Configuration Manager Windows 10-clients installeren en toewijzen met behulp van Azure AD voor verificatie](deploy-clients-cmg-azure.md). Deze procedure geldt voor clients op een intranet of Internet.  

### <a name="manual-installation-examples"></a>Voor beelden van hand matige installatie

Deze voor beelden zijn voor Active Directory-clients in een intranet. Ze gebruiken de volgende waarden:  

- **MPSERVER**: server die als host fungeert voor het beheer punt
- **FSPSERVER**: server die als host fungeert voor het terugval status punt  
- **ABC**: site code  
- **contoso.com**: domein naam  

Stel dat u alle site systeem servers hebt geconfigureerd met een intranet-FQDN en de site-informatie naar Active Directory hebt gepubliceerd.  

Begin met de volgende stappen op de client computer:  

1. Meld u aan als een lokale beheerder.  
2. Station Z toewijzen aan `\\MPSERVER\SMS_ABC\Client` .  
3. Schakel de opdracht prompt om Z te zetten.  

Voer vervolgens een van de volgende opdrachten uit:  

#### <a name="manual-example-1"></a>Hand matig voor beeld 1  

`CCMSetup.exe`  

Met deze opdracht wordt de client zonder aanvullende para meters of eigenschappen geïnstalleerd. De client wordt automatisch geconfigureerd met de client installatie-eigenschappen die zijn gepubliceerd op Active Directory Domain Services, met inbegrip van de volgende instellingen:  

- Site code: voor deze instelling moet de netwerk locatie van de client zijn opgenomen in een grens groep die u hebt geconfigureerd voor client toewijzing.  
- Beheer punt.
- Terugval status punt.
- Communiceren alleen via HTTPS.  

Zie [over client installatie-eigenschappen die zijn gepubliceerd op Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md)voor meer informatie.  

#### <a name="manual-example-2"></a>Hand matig voor beeld 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Met deze opdracht wordt de automatische configuratie overschreven die Active Directory Domain Services biedt. U hoeft de netwerk locatie van de client niet op te nemen in een grens groep die is geconfigureerd voor client toewijzing. In plaats daarvan geeft de installatie de volgende instellingen:

- Site code
- Intranet beheer punt
-  Beheerpunt op internet
- Terugval status punt dat verbindingen van het internet accepteert
- Een client certificaat voor open bare-sleutel infrastructuur (PKI) gebruiken (indien beschikbaar) met de langste geldigheids duur

## <a name="logon-script-installation"></a><a name="BKMK_ClientLogonScript"></a> Installatie van aanmeldings script

Configuration Manager ondersteunt het gebruik van aanmeldings scripts om de Configuration Manager-client software te installeren. Gebruik het programma bestand CCMSetup.exe in een aanmeldings script om de client installatie te activeren.  

Voor de aanmeldingsscriptinstallatie worden dezelfde methodes gebruikt als handmatige clientinstallatie. Geef de `/logon` installatie parameter voor CCMSsetup.exe op. Als er al een versie van de client op de computer bestaat, wordt door deze para meter voor komen dat de client wordt geïnstalleerd. Dit gedrag voor komt dat de client opnieuw wordt geïnstalleerd telkens wanneer het aanmeldings script wordt uitgevoerd.  

Als u geen installatie bron opgeeft met behulp `/Source` van de para meter en geen beheer punt van waaruit de installatie wordt verkregen, wordt opgegeven door de `/MP` para meter, CCMSetup.exe het beheer punt zoekt door te zoeken naar Active Directory Domain Services. Dit gedrag treedt alleen op als u het schema voor Configuration Manager hebt uitgebreid en de site hebt gepubliceerd op Active Directory Domain Services. De client kan in plaats daarvan DNS of WINS gebruiken om een beheerpunt te zoeken.  

## <a name="package-and-program-installation"></a><a name="BKMK_ClientApp"></a> Pakket-en programma-installatie

Gebruik Configuration Manager voor het maken en implementeren van een pakket en programma waarmee de client software wordt bijgewerkt voor geselecteerde apparaten. Configuration Manager levert een Package Definition File waarmee de pakket eigenschappen worden gevuld met meestal gebruikte waarden. Pas het gedrag van de client installatie aan door aanvullende opdracht regel parameters en eigenschappen op te geven.  

> [!NOTE]  
> U kunt Configuration Manager 2007-clients niet bijwerken met behulp van deze methode. Gebruik in plaats daarvan de automatische clientupgrade, waarbij automatisch een pakket wordt geïmplementeerd met de meest recente versie van de client. Zie [upgrade-clients](../manage/upgrade/upgrade-clients.md)voor meer informatie.  
>
> Zie [een strategie voor client migratie plannen](../../migration/planning-a-client-migration-strategy.md)voor meer informatie over het migreren van oudere versies van de Configuration Manager-client.  

### <a name="create-a-package-and-program-for-the-client-software"></a>Een pakket en programma voor de client software maken  

Gebruik de volgende procedure om een Configuration Manager-pakket en-programma te maken dat u kunt implementeren op Configuration Manager-client computers om de client software bij te werken.  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **pakketten** .  

2. Op het tabblad **Start** van het lint, in de groep **maken** , selecteert u **pakket maken van definitie**.  

3. Selecteer op de pagina **pakket definitie** van de wizard de optie **micro soft** in de lijst met **uitgevers** en selecteer **Configuration Manager client upgrade** uit de lijst **pakket definities** .  

4. Selecteer op de pagina **bron bestanden** **altijd bestanden ophalen uit een bronmap**.  

5. Selecteer **netwerkpad (UNC-naam)** op de pagina **bron map** . Voer vervolgens het netwerkpad in van de server en de share die de client installatie bestanden bevat.  

    > [!NOTE]  
    > De computer waarop de Configuration Manager implementaties worden uitgevoerd, moet toegang hebben tot de opgegeven netwerkmap. Anders mislukt de installatie van de client.  

    Als u de eigenschappen van de client installatie wilt wijzigen, wijzigt u de CCMSetup.exe opdracht regel op het tabblad **Algemeen** van het dialoog venster **Eigenschappen van Configuration Manager agent Silent upgrade** . De standaard installatie-eigenschappen zijn `/noservice SMSSITECODE=AUTO` .  

6. Het pakket naar alle distributiepunten distribueren waarnaar u het clientupgradepakket wilt hosten. Implementeer vervolgens het pakket op apparaat verzamelingen die clients bevatten die u wilt upgraden.  

## <a name="intune-mdm-managed-windows-devices"></a><a name="bkmk_mdm"></a> Door MDM beheerde Windows-apparaten met intune

Implementeer de Configuration Manager-client op apparaten die zijn Inge schreven bij Microsoft Intune.

Deze procedure is voor een traditionele client die is verbonden met een intranet. Er wordt gebruikgemaakt van traditionele methoden voor client verificatie. Om ervoor te zorgen dat het apparaat zich in een beheerde status bevindt nadat de client is geïnstalleerd, moet deze zich op het intranet en binnen een Configuration Manager site-grens bevindt.  

Zie voor de procedure om de Configuration Manager-client op een modern Windows 10-apparaat te installeren met behulp van de Azure AD-identiteit, [Configuration Manager Windows 10-clients installeren en toewijzen met behulp van Azure AD voor verificatie](deploy-clients-cmg-azure.md).

Nadat u de Configuration Manager-client hebt geïnstalleerd, wordt de registratie van apparaten bij intune niet ongedaan gemaakt. Ze kunnen de Configuration Manager client en MDM-inschrijving tegelijk gebruiken. Zie [overzicht van co-beheer](../../../comanage/overview.md)voor meer informatie.  

> [!Note]
> U kunt andere client installatie methoden gebruiken om de Configuration Manager-client te installeren op een apparaat dat door intune wordt beheerd. Als een door intune beheerd apparaat bijvoorbeeld op het intranet staat en lid is van het Active Directory domein, kunt u groeps beleid gebruiken om de Configuration Manager-client te installeren.<!-- SCCMDocs#757 -->

### <a name="install-the-configuration-manager-client-by-using-intune"></a>De Configuration Manager-client installeren met behulp van intune

1. Voeg in intune [een Windows line-of-Business-app toe](https://docs.microsoft.com/mem/intune/apps/lob-apps-windows) die het Configuration Manager client installatie bestand bevat **CCMSetup.msi**. U kunt dit bestand vinden in de `\bin\i386` map van de Configuration Manager-installatiemap op de site server.  

2. Voer in het Intune Software Publisher opdracht regel parameters in. Gebruik deze opdracht bijvoorbeeld met een traditionele client op een intranet:  

    `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

    > [!NOTE]  
    > Zie voor een voor beeld van een opdracht die wordt gebruikt met een moderne Windows 10-client met behulp van Azure AD [-verificatie hoe u op internet gebaseerde apparaten voorbereidt voor co-beheer](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).  

3. [Wijs de app](../../../../intune/apps/apps-deploy.md) toe aan een groep van de Inge schreven Windows-computers.  

## <a name="os-image-installation"></a><a name="BKMK_ClientImage"></a> Installatie kopie van besturings systeem installeren

Installeer de Configuration Manager-client vooraf op een referentie computer die u gebruikt om een installatie kopie van het besturings systeem te maken.

> [!IMPORTANT]  
> Wanneer u de taken reeks Configuration Manager gebruikt voor het implementeren van een installatie kopie van een besturings systeem, verwijdert de stap [ConfigMgr-client voorbereiden](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture) de Configuration Manager-client volledig.  

### <a name="prepare-the-client-computer-for-imaging"></a>De client computer voorbereiden voor Imaging  

1. Installeer de Configuration Manager-client software hand matig op de referentie computer. Zie [Configuration Manager-clients hand matig installeren](#BKMK_Manual)voor meer informatie.  

    > [!IMPORTANT]  
    > Geef geen Configuration Manager site code op voor de client in de CCMSetup.exe opdracht regel eigenschappen.  

2. Typ bij een opdracht prompt `net stop ccmexec` om de SMS agent host-service (CcmExec.exe) op de referentie computer te stoppen.  

3. Verwijder het SMSCFG.INI-bestand uit de map Windows op de referentie computer.  

4. Verwijder alle certificaten die zijn opgeslagen in het archief van de lokale computer op de referentie computer. Als u bijvoorbeeld PKI-certificaten gebruikt, verwijdert u de certificaten in het **persoonlijke** Archief voor de **computer** en **gebruiker**voordat u een installatie kopie van de computer maakt.  

5. Als de clients zijn geïnstalleerd in een andere Configuration Manager hiërarchie dan de hiërarchie van de referentie computer, verwijdert u de vertrouwde basis sleutel van de referentie computer.  

    > [!NOTE]  
    > Als clients geen Active Directory Domain Services kunnen zoeken om een beheer punt te vinden, gebruiken ze de vertrouwde basis sleutel om vertrouwde beheer punten te bepalen. Als u alle clients met installatie kopieën in dezelfde hiërarchie als die van de hoofd computer implementeert, moet u de vertrouwde basis sleutel in plaats laten staan.
    >
    > Als u de clients in verschillende hiërarchieën implementeert, verwijdert u de vertrouwde basis sleutel. Richt deze clients ook in met de nieuwe vertrouwde basis sleutel. Zie [planning voor de vertrouwde basis sleutel](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)voor meer informatie.  

6. Gebruik uw beeldbewerkings software om een installatie kopie van de referentie computer vast te leggen.  

7. Implementeer de installatie kopie op de doel computers.  

## <a name="workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> Werkgroepcomputers

Configuration Manager ondersteunt client installatie voor computers in werk groepen. Installeer de-client op werkgroepcomputers met behulp van de methode die is opgegeven in de [installatie van Configuration Manager-clients hand matig](#BKMK_Manual).  

### <a name="prerequisites"></a>Vereisten  

- Installeer de client hand matig op elke werkgroepcomputer. Tijdens de installatie moet de interactieve gebruiker lokale beheerders rechten hebben.  

- Als u toegang wilt krijgen tot resources in het domein van de Configuration Manager site server, configureert u het netwerk toegangs account voor de site. Geef dit account op in het onderdeel Software Distribution site. Zie [site onderdelen](../../servers/deploy/configure/site-components.md)voor meer informatie.  

### <a name="limitations"></a>Beperkingen  

- Werkgroepcomputers kunnen geen beheer punten vinden van Active Directory Domain Services. In plaats daarvan gebruiken ze DNS, WINS of een ander beheer punt.  

- Globale roaming wordt niet ondersteund. Werkgroepcomputers kunnen Active Directory Domain Services voor site-informatie niet opvragen.  

- Active Directory detectie methoden kunnen computers in werk groepen niet detecteren.  

- U kunt software niet implementeren voor gebruikers van computers in werk groepen.  

- U kunt de client push installatie methode niet gebruiken om de-client te installeren op werkgroepcomputers.  

- Workgroup-clients kunnen Kerberos niet gebruiken voor verificatie en ze kunnen hand matige goed keuring vereisen.  

- U kunt een werkgroep-client niet configureren als een distributie punt. Configuration Manager vereist dat distributiepunt computers lid zijn van een domein.  

### <a name="install-the-client-on-workgroup-computers"></a>De-client installeren op computers in werk groepen  

Controleer de vereisten en volg de instructies in de sectie [hand matig Configuration Manager-clients installeren](#BKMK_Manual).  

#### <a name="workgroup-example-1"></a>Voor beeld van werk groep 1

In dit voor beeld worden de volgende acties uitgevoerd:

- Installeert de client voor intranet-client beheer
- Hiermee geeft u de site code
- Hiermee geeft u het DNS-achtervoegsel op om een beheer punt te zoeken  

`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

#### <a name="workgroup-example-2"></a>Voor beeld 2 van werk groep

Dit voor beeld vereist dat de client zich op een netwerk locatie bevindt die is geconfigureerd in een grens groep. Als aan deze vereiste niet wordt voldaan, werkt automatische site toewijzing niet. De opdracht bevat een terugval status punt op server FSPSERVER. Deze eigenschap helpt bij het volgen van client implementatie en voor het identificeren van client communicatie problemen.

`CCMSetup.exe FSP=fspserver.constoso.com`  

## <a name="internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> Client beheer op Internet  

> [!NOTE]  
> Deze sectie is niet van toepassing op clients die gebruikmaken van een [Cloud beheer gateway](../manage/cmg/plan-cloud-management-gateway.md). Zie [Configuration Manager Windows 10-clients installeren en toewijzen met behulp van Azure AD voor verificatie](deploy-clients-cmg-azure.md)als u clients op internet wilt installeren met behulp van een Cloud beheer gateway.  

Wanneer de Configuration Manager-site [client beheer op Internet](../manage/plan-internet-based-client-management.md) ondersteunt voor clients die zich soms op een intranet bevinden en soms op internet, hebt u twee opties wanneer u clients installeert op het intranet:  

- Neem de Client.msi eigenschap `CCMHOSTNAME=<internet FQDN of the internet-based management point>` op wanneer u de client installeert, bijvoorbeeld door hand matige installatie of client push te gebruiken. Wanneer u deze methode gebruikt, wijst u de client rechtstreeks aan de site toe. U kunt automatische site toewijzing niet gebruiken. Zie de sectie [hand matig Configuration Manager-clients installeren](#BKMK_Manual) , die een voor beeld van deze configuratie methode bevat.  

- Installeer de client voor intranet client beheer en wijs vervolgens een client beheer punt op Internet toe aan de client. Wijzig het beheer punt met behulp van de client eigenschappen op de pagina **Configuration Manager** van het configuratie scherm of met behulp van een script. Wanneer u deze methode gebruikt, kunt u automatische clienttoewijzing gebruiken. Zie de sectie [clients configureren voor client beheer op Internet na client installatie](#BKMK_ConfigureIBCM_MP) voor meer informatie.  

Als u clients wilt installeren die op het Internet zijn, kiest u een van de volgende ondersteunde methoden:  

- Bieden een mechanisme voor deze clients om tijdelijk verbinding te maken met het intranet met een VPN. Installeer vervolgens de client met behulp van een geschikte client installatie methode.  

- Gebruik een installatie methode die onafhankelijk is van Configuration Manager. U kunt bijvoorbeeld de bron bestanden van de client installatie inpakken op Verwissel bare media en de media naar gebruikers verzenden. De bron bestanden van de client installatie bevinden zich in de `<installation path>\Client` map op de Configuration Manager site server. Voeg op de media een script toe om de client map hand matig te kopiëren. Installeer de client vanuit deze map met behulp van CCMSetup.exe en alle toepasselijke CCMSetup-opdracht regel eigenschappen.  

> [!NOTE]  
> Configuration Manager biedt geen ondersteuning voor het installeren van een client rechtstreeks vanaf het beheer punt op internet of het software-update punt op internet.

Clients die via internet worden beheerd, moeten communiceren met site systemen op internet. Zorg ervoor dat deze clients ook PKI-certificaten (Public Key Infrastructure) hebben voordat u de-client installeert. Installeer deze certificaten onafhankelijk van Configuration Manager. Zie [PKI-certificaat vereisten](../../plan-design/network/pki-certificate-requirements.md)voor meer informatie.  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Clients op Internet installeren door CCMSetup-opdracht regel eigenschappen op te geven  

1. Volg de instructies in de sectie [hand matig Configuration Manager-clients installeren](#BKMK_Manual). Altijd de volgende opties toevoegen:  

    - CCMSetup-opdracht regel parameter `/source:<local path of the copied Client folder>`  

    - CCMSetup-opdracht regel parameter `/UsePKICert`  

    - Client.msi eigenschap `CCMHOSTNAME=<FQDN of internet-based management point>`  

    - Client.msi eigenschap `SMSSIGNCERT=<local path of exported site server signing certificate>`  

    - Client.msi eigenschap `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    > Als de site meer dan één beheer punt op internet heeft, maakt het niet uit welke naam u voor de `CCMHOSTNAME` eigenschap opgeeft. Wanneer een Configuration Manager-client verbinding maakt met het opgegeven beheer punt op internet, stuurt de client een lijst met beschik bare beheer punten op internet in de site. De client selecteert een wille keurige naam in de lijst.

2. Als u niet wilt dat de client de certificaatintrekkingslijst (CRL) controleert, geeft u de CCMSetup-opdracht regel parameter op `/NoCRLCheck` .  

3. Als u een terugval status punt op Internet gebruikt, geeft u de eigenschap Client.msi op `FSP=<internet FQDN of the internet-based fallback status point>` .  

4. Als u de client installeert voor client beheer op internet, geeft u de eigenschap Client.msi op `CCMALWAYSINF=1` .  

5. Bepaal of u aanvullende CCMSetup-opdracht regel parameters moet opgeven. Als de client meer dan één geldig PKI-certificaat heeft, moet u mogelijk een selectie criterium voor het certificaat opgeven. Zie [over para meters en eigenschappen van client installatie](about-client-installation-properties.md)voor een lijst met beschik bare eigenschappen.  

#### <a name="internet-based-example"></a>Voor beeld op Internet

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`

In dit voor beeld wordt de client geïnstalleerd met het volgende gedrag:

- Bron bestanden van een map op station D gebruiken.
- Gebruik een PKI-client certificaat.
- Selecteer het certificaat met de langste geldigheids periode.
- Client beheer op internet.
- Wijs de client toe om het beheer punt op internet te gebruiken met de naam SERVER1.
- Wijs het terugval status punt op Internet toe in het domein contoso.com.
- Wijs de client toe aan de ABC-site.  

### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> Clients configureren voor client beheer op Internet na installatie van de client  

Gebruik een van de volgende procedures om het beheer punt op Internet toe te wijzen nadat u de client hebt geïnstalleerd. De eerste vereist hand matige configuratie en is geschikt voor een aantal clients. De tweede is geschikter voor het configureren van veel clients.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Clients configureren voor client beheer op Internet na client installatie vanuit het Configuration Manager configuratie scherm  

1. Open het configuratie scherm van **Configuration Manager** op de client.  

2. Voer op het tabblad **Internet** de Fully QUALIFIED domain name (FQDN) van het beheer punt op internet in als de **Internet-FQDN**.  

    > [!NOTE]  
    > Het tabblad **Internet** is alleen beschikbaar als de client een PKI-client certificaat heeft.  

3. Als de client toegang heeft tot internet via een proxy server, voert u de instellingen van de proxy server in.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Clients configureren voor client beheer op Internet na installatie van de client met behulp van een script  

##### <a name="powershell"></a>PowerShell

1. Open een Power shell-in-line editor, zoals Power shell ISE of Visual Studio code. U kunt ook een tekst editor gebruiken, zoals Klad blok.

2. Kopieer de volgende regels code en voeg deze in de editor in. Vervang door `'mp.contoso.com'` de Internet-FQDN van uw beheer punt op internet.

    ``` PowerShell
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    ```

    > [!NOTE]  
    > De laatste regel is er alleen om de nieuwe waarde voor het internet beheer punt te controleren.
    >
    > Als u een opgegeven beheer punt op internet wilt verwijderen, verwijdert u de server-FQDN-waarde binnen de aanhalings tekens. De regel wordt `$newInternetBasedManagementPointFQDN = ''` .

3. Sla het bestand op met de extensie. ps1.  

4. Voer het script uit met verhoogde rechten op client computers. Gebruik een van de volgende methoden:  

    - Implementeer het bestand naar bestaande Configuration Manager-clients door gebruik te maken van een pakket en een programma.  

    - Voer het bestand lokaal uit op bestaande Configuration Manager-clients door te dubbel klikken op het script bestand in Verkenner.  

Mogelijk moet u de client opnieuw opstarten om de wijzigingen van kracht te laten worden.  

## <a name="provision-client-installation-properties"></a><a name="BKMK_Provision"></a> Eigenschappen van client installatie inrichten

Provisioning client installatie-eigenschappen voor groeps beleid en client installaties op basis van software-updates. Gebruik Windows groepsbeleid om computers in te richten met Configuration Manager-client installatie-eigenschappen. Deze eigenschappen worden opgeslagen in het REGI ster van de computer. De client leest ze tijdens de installatie. Deze procedure is normaal gesp roken niet vereist, maar kan nodig zijn voor bepaalde scenario's voor client installatie, zoals:  

- U gebruikt de instellingen voor groeps beleid of client installatie op basis van software-updates. U hebt het Active Directory schema voor Configuration Manager niet uitgebreid.  

- U wilt de eigenschappen van clientinstallatie op specifieke computers overschrijven.  

> [!NOTE]  
> Als er installatie-eigenschappen worden opgegeven op de CCMSetup.exe opdracht regel, worden de installatie-eigenschappen die zijn ingericht op computers niet gebruikt.

Er wordt een beheer sjabloon voor groeps beleid `ConfigMgrInstallation.adm` met de naam opgegeven op de Configuration Manager-installatie media. Gebruik deze sjabloon om client computers in te richten met installatie-eigenschappen.

> [!TIP]
> Standaard `ConfigMgrInstallation.adm` biedt geen ondersteuning voor teken reeksen die groter zijn dan 255 tekens. Deze configuratie kan van invloed zijn op het toevoegen van meerdere para meters of para meters met lange waarden, zoals CCMCERTISSUERS.<!-- SCCMDocs#1648 -->
>
> U kunt dit probleem als volgt oplossen:
>
> 1. Bewerken `ConfigMgrInstallation.adm` in Klad blok.
> 2. `VALUENAME SetupParameters`Wijzig de waarde voor de eigenschap `MAXLEN` in een groter geheel getal. Bijvoorbeeld `MAXLEN 511`.

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Eigenschappen van client installatie configureren en toewijzen met behulp van een groeps beleidsobject  

1. Importeer de beheer sjabloon ConfigMgrInstallation. adm in een nieuw of bestaand groeps beleidsobject (GPO) door gebruik te maken van een editor zoals Windows Groepsbeleidsobjecteditor. U kunt dit bestand vinden in de `TOOLS\ConfigMgrADMTemplates` map op de Configuration Manager-installatie media.  

2. Open de eigenschappen van de geïmporteerde instelling **Configureer instellingen clientimplementatie**.  

3. Selecteer **Ingeschakeld**.  

4. Voer in het vakje **CCMSetup** de vereiste CCMSetup-opdrachtregeleigenschappen in. Zie [over client installatie parameters en eigenschappen](about-client-installation-properties.md)voor een lijst met alle CCMSetup-opdracht regel eigenschappen en voor beelden van het gebruik ervan.  

5. Wijs het groeps beleidsobject toe aan de computers die u wilt inrichten met Configuration Manager client installatie-eigenschappen.
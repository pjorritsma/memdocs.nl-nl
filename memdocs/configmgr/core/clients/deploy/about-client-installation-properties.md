---
title: Client installatie parameters en eigenschappen
titleSuffix: Configuration Manager
description: Meer informatie over de ccmsetup-opdracht regel parameters en eigenschappen voor het installeren van de Configuration Manager-client.
ms.date: 06/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 388a051f899369aa6a7754f94b0a7727f943f0ec
ms.sourcegitcommit: efe89408a3948b79b38893174cb19268ee37c8f3
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "85854402"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>Over para meters en eigenschappen van client installatie in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de opdracht CCMSetup.exe om de Configuration Manager-client te installeren. Als u client installatie *parameters* op de opdracht regel opgeeft, wordt het installatie gedrag gewijzigd. Als u *Eigenschappen* voor client installatie op de opdracht regel opgeeft, wordt de oorspronkelijke configuratie van de geïnstalleerde client agent gewijzigd.

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a>Over CCMSetup.exe

De CCMSetup.exe opdracht downloadt de benodigde bestanden om de client te installeren vanaf een beheer punt of een bron locatie. Deze bestanden kunnen het volgende omvatten:  

- Het Windows Installer-pakket client.msi waarmee de client software wordt geïnstalleerd

- Client vereisten

- Updates en oplossingen voor de Configuration Manager-client

> [!NOTE]
> U kunt client.msi niet rechtstreeks installeren.  

CCMSetup.exe biedt opdracht regel *parameters* voor het aanpassen van de installatie. Para meters worden voorafgegaan door een slash ( `/` ) en per Conventie zijn in kleine letters. U geeft de waarde van een para meter op wanneer dit nodig is met behulp van een dubbele punt ( `:` ) direct gevolgd door de waarde. Zie [CCMSetup.exe opdracht regel parameters](#ccmsetupexe-command-line-parameters)voor meer informatie.

U kunt ook *Eigenschappen* opgeven op de CCMSetup.exe opdracht regel om het gedrag van client.msi te wijzigen. Eigenschappen per Conventie zijn hoofd letters. U geeft een waarde voor een eigenschap op met behulp van een gelijkteken ( `=` ) direct gevolgd door de waarde. Zie [Client.msi eigenschappen](#clientMsiProps)voor meer informatie.

> [!IMPORTANT]  
> Geef CCMSetup-para meters op voordat u eigenschappen voor client.msi opgeeft.  

CCMSetup.exe en de ondersteunende bestanden bevinden zich op de site server in de map **client** van de installatiemap van Configuration Manager. Configuration Manager deze map te delen met het netwerk onder de site share. Bijvoorbeeld `\\SiteServer\SMS_ABC\Client`.

Aan de opdrachtregel gebruikt de opdracht CCMSetup.exe de volgende indeling:  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

Bijvoorbeeld:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

In dit voor beeld worden de volgende dingen gedaan:  

- Hiermee geeft u het beheer punt met de naam SMSMP01 op om een lijst met distributie punten aan te vragen om de client installatie bestanden te downloaden.  

- Hiermee geeft u op dat de installatie moet worden gestopt als er al een versie van de client op de computer bestaat.  

- Geeft client.msi de instructie om de client toe te wijzen aan de sitecode S01.  

- Hiermee ontvangt client.msi de instructie het terugvalstatuspunt SMSFP01 te gebruiken.  

> [!TIP]  
> Als een parameter waarde spaties bevat, plaatst u deze tussen aanhalings tekens.  

Als u het Active Directory schema voor Configuration Manager uitbreidt, publiceert de site veel client installatie-eigenschappen in Active Directory Domain Services. Deze eigenschappen worden automatisch door de Configuration Manager-client gelezen. Zie [over eigenschappen van client installatie die zijn gepubliceerd op Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md) voor meer informatie.  

## <a name="ccmsetupexe-command-line-parameters"></a>CCMSetup.exe opdracht regel parameters

### <a name=""></a><a name="bkmk_help"></a> /?

Bevat beschik bare opdracht regel parameters voor ccmsetup.exe.  

Voorbeeld: `ccmsetup.exe /?`

### <a name="source"></a>/source

Hiermee geeft u de locatie voor het downloaden van bestanden. Gebruik een lokaal of UNC-pad. Het apparaat downloadt bestanden met behulp van het SMB-protocol (Server Message Block). Voor het gebruik van **/Source**moet het Windows-gebruikers account voor de client installatie **Lees** machtigingen voor de locatie hebben.

Zie [grens groepen-client installatie](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup)voor meer informatie over hoe ccmsetup inhoud downloadt. Dit artikel bevat ook informatie over ccmsetup-gedrag als u de para meters **/MP** en **/Source** gebruikt.

> [!TIP]  
> U kunt de para meter **/Source** meer dan één keer in een opdracht regel gebruiken om alternatieve download locaties op te geven.  

Voorbeeld: `ccmsetup.exe /source:"\\server\share"`

### <a name="mp"></a>/MP

Hiermee geeft u een bron beheer punt voor computers waarmee verbinding moet worden gemaakt. Computers gebruiken dit beheer punt om het dichtstbijzijnde distributie punt voor de installatie bestanden te vinden. Als er geen distributie punten zijn of als computers de bestanden niet kunnen downloaden van de distributie punten na vier uur, downloaden ze de bestanden van het opgegeven beheer punt.  

Zie [grens groepen-client installatie](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup)voor meer informatie over hoe ccmsetup inhoud downloadt. Dit artikel bevat ook informatie over ccmsetup-gedrag als u de para meters **/MP** en **/Source** gebruikt.

> [!IMPORTANT]  
> Met deze para meter geeft u een initieel beheer punt voor computers op om een download bron te vinden. Dit kan elk beheer punt in elke site zijn. De client wordt niet *toegewezen* aan het opgegeven beheer punt.

Computers downloaden de bestanden via een HTTP- of HTTPS-verbinding, afhankelijk van de sitesysteemrolconfiguratie voor clientverbindingen. De down load kan ook gebruikmaken van BITS-beperking als u deze configureert. Als u alle distributie punten en beheer punten alleen voor HTTPS-client verbindingen configureert, controleert u of de client computer een geldig client certificaat heeft.  

U kunt de opdracht regel parameter **/MP** gebruiken om meer dan één beheer punt op te geven. Als de computer geen verbinding kan maken met de eerste, wordt de volgende in de opgegeven lijst geprobeerd. Wanneer u meerdere beheer punten opgeeft, scheidt u de waarden van elkaar door punt komma's.

Als de client verbinding maakt met een beheer punt met behulp van HTTPS, geeft u de FQDN op, niet de computer naam. De waarde moet overeenkomen met het **onderwerp** of de **alternatieve naam**van het beheer punt PKI-certificaat. Hoewel Configuration Manager ondersteuning biedt voor het gebruik van een computer naam in het certificaat voor verbindingen op het intranet, wordt het gebruik van een FQDN aanbevolen.

Voor beeld met de computer naam:`ccmsetup.exe /mp:SMSMP01`  

Voor beeld met de FQDN:`ccmsetup.exe /mp:smsmp01.contoso.com`  

Met deze para meter kunt u ook de URL van een CMG (Cloud Management Gateway) opgeven. Gebruik deze URL om de-client te installeren op een op internet gebaseerd apparaat. Gebruik de volgende stappen om de waarde voor deze para meter op te halen:

- Een CMG maken. Zie [een CMG instellen](../manage/cmg/setup-cloud-management-gateway.md)voor meer informatie.
- Open een Windows Power shell-opdracht prompt als beheerder op een actieve client.
- Voer de volgende opdracht uit:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
    ```

- Voeg het `https://` voor voegsel toe voor gebruik met de para meter **/MP** .

Voor beeld voor wanneer u de URL voor de Cloud beheer gateway gebruikt:`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Wanneer u de URL van een Cloud beheer gateway opgeeft voor de para meter **/MP** , moet deze beginnen met `https://` .

### <a name="regtoken"></a>/regtoken

<!--5686290-->

Met ingang van versie 2002 kunt u deze para meter gebruiken om een token voor bulk registratie op te geven. Een apparaat op Internet gebruikt dit token in het registratie proces via een CMG (Cloud Management Gateway). Zie [verificatie op basis van tokens voor CMG](deploy-clients-cmg-token.md)voor meer informatie.

Wanneer u deze para meter gebruikt, neemt u ook de volgende para meters en eigenschappen op:

- [**/MP**](#mp)
- [**CCMHOSTNAME**](#ccmhostname)
- [**SMSSiteCode**](#smssitecode)
- [**SMSMP**](#smsmp)

De volgende voorbeeld opdracht regel bevat de andere vereiste installatie parameters en eigenschappen:

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/Retry

Als CCMSetup.exe installatie bestanden niet kunt downloaden, gebruikt u deze para meter om het interval voor nieuwe pogingen in minuten op te geven. CCMSetup blijft het opnieuw proberen totdat het de limiet bereikt die is opgegeven in de para meter [**/downloadtimeout**](#downloadtimeout) .

Voorbeeld: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Met deze para meter wordt voor komen dat CCMSetup als een service wordt uitgevoerd. dit gebeurt standaard. Wanneer CCMSetup als een service wordt uitgevoerd, wordt dit uitgevoerd in de context van het lokale systeem account van de computer. Dit account heeft mogelijk onvoldoende rechten voor toegang tot de vereiste netwerk bronnen voor de installatie. Met **/noservice**wordt CCMSetup.exe uitgevoerd in de context van het gebruikers account dat u gebruikt om de installatie te starten.

Voorbeeld: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Specificeert dat CCMSetup moet worden uitgevoerd als een service die gebruikmaakt van het lokale systeem account.  

> [!TIP]
> Als u een script gebruikt om CCMSetup.exe uit te voeren met de para meter **/service** , wordt CCMSetup.exe afgesloten nadat de service is gestart. De installatie Details worden mogelijk niet goed gerapporteerd aan het script.

Voorbeeld: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Gebruik deze para meter om de Configuration Manager-client te verwijderen. Zie [de client verwijderen](../manage/manage-clients.md#BKMK_UninstalClient)voor meer informatie.

Voorbeeld: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Als er al een versie van de client is geïnstalleerd, wordt met deze para meter opgegeven dat de installatie van de client moet worden gestopt.  

Voorbeeld: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

Gebruik deze para meter om te zorgen dat de computer zo nodig opnieuw wordt opgestart om de installatie te volt ooien. Als u deze para meter niet opgeeft, wordt CCMSetup afgesloten wanneer opnieuw opstarten nodig is. Daarna wordt de volgende hand matig opnieuw opgestart.

Voorbeeld: `CCMSetup.exe /forcereboot`

### <a name="bitspriority"></a>/BITSPriority

Wanneer het apparaat client installatie bestanden via een HTTP-verbinding downloadt, gebruikt u deze para meter om de Download prioriteit op te geven. Geef een van de volgende mogelijke waarden op:

- `FOREGROUND`

- `HIGH`

- `NORMAL`prijs

- `LOW`

Voorbeeld: `ccmsetup.exe /BITSPriority:HIGH`

### <a name="downloadtimeout"></a>/downloadtimeout

Als CCMSetup de client installatie bestanden niet kan downloaden, wordt met deze para meter de maximale time-out in minuten opgegeven. Na deze time-out stopt CCMSetup met het downloaden van de installatie bestanden. De standaard waarde is **1440** minuten (één dag).

Gebruik de para meter [**/Retry**](#retry) om het interval tussen nieuwe pogingen op te geven.

Voorbeeld: `ccmsetup.exe /downloadtimeout:100`

### <a name="usepkicert"></a>/UsePKICert

Geef deze para meter op voor de client om een PKI-certificaat voor client verificatie te gebruiken. Als u deze para meter niet opneemt of als de client geen geldig certificaat kan vinden, wordt een HTTP-verbinding met een zelfondertekend certificaat gebruikt.

Voorbeeld: `CCMSetup.exe /UsePKICert`  

> [!NOTE]
> In sommige scenario's hoeft u deze para meter niet op te geven, maar toch een client certificaat te gebruiken. Bijvoorbeeld client-push en software-update-gebaseerde client installatie. Gebruik deze para meter wanneer u een client hand matig installeert en de para meter **/MP** gebruikt met een beheer punt waarvoor https is ingeschakeld.
>
> Geef deze para meter ook op wanneer u een client installeert voor communicatie via internet. Gebruik de eigenschap **CCMALWAYSINF = 1** samen met de eigenschappen voor het beheer punt op internet (**CCMHOSTNAME**) en de site code (**SMSSITECODE**). Zie [overwegingen voor client communicatie via internet of een niet-vertrouwd forest](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)voor meer informatie over client beheer op internet.  

### <a name="nocrlcheck"></a>/NoCRLCheck

Hiermee geeft u op dat een client de certificaatintrekkingslijst (CRL) niet moet controleren wanneer deze via HTTPS communiceert met een PKI-certificaat. Wanneer u deze para meter niet opgeeft, controleert de client de CRL voordat er een HTTPS-verbinding tot stand wordt gebracht. Zie [planning voor PKI-certificaat intrekking](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)voor meer informatie over de CRL-controle van de client.

Voorbeeld: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="config"></a>/config

Met deze para meter geeft u een tekst bestand op dat de eigenschappen van de client installatie vermeldt.

- Als CCMSetup als een service wordt uitgevoerd, plaatst u dit bestand in de map CCMSetup System: `%Windir%\Ccmsetup` .

- Als u de para meter [**/noservice**](#noservice) opgeeft, plaatst u dit bestand in dezelfde map als CCMSetup.exe.

Voorbeeld: `CCMSetup.exe /config:"configuration file name.txt"`

Als u de juiste bestands indeling wilt opgeven, gebruikt u het bestand **bestand mobileclienttemplate. TCF** in de `\bin\<platform>` map in de installatiemap Configuration Manager op de site server. Dit bestand bevat opmerkingen over de secties en hoe u deze kunt gebruiken. Geef de client installatie-eigenschappen op in de `[Client Install]` sectie na de volgende tekst: `Install=INSTALL=ALL` .

Voor beeld van `[Client Install]` sectie vermelding:`Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereq"></a>/skipprereq

Deze para meter geeft aan dat CCMSetup.exe de opgegeven vereiste niet installeert. U kunt meer dan één waarde invoeren. Gebruik de punt komma ( `;` ) als scheidings teken voor elke waarde.

Voorbeelden:

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe`

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`

Zie [vereisten voor Windows-clients](prerequisites-for-deploying-clients-to-windows-computers.md)voor meer informatie over de vereisten van de client.

### <a name="forceinstall"></a>/forceinstall

Opgeven dat CCMSetup.exe elke bestaande client verwijdert en een nieuwe client installeert.  

### <a name="excludefeatures"></a>/ExcludeFeatures

Met deze para meter geeft u op dat CCMSetup.exe de opgegeven functie niet installeert.

Voor beeld: `CCMSetup.exe /ExcludeFeatures:ClientUI` installeert software Center niet op de client.  

> [!NOTE]  
> `ClientUI`is de enige waarde die de para meter **/ExcludeFeatures** ondersteunt.

### <a name="alwaysexcludeupgrade"></a>/AlwaysExcludeUpgrade

Met deze para meter wordt opgegeven of een client automatisch wordt bijgewerkt wanneer u [**automatische client upgrade**](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)inschakelt.

Ondersteunde waarden:

- `TRUE`: De client wordt niet automatisch bijgewerkt
- `FALSE`: De client wordt automatisch bijgewerkt (standaard)

Bijvoorbeeld:  

`CCMSetup.exe /AlwaysExcludeUpgrade:TRUE`

Zie [Extended interoperabiliteit client](../../understand/interoperability-client.md)voor meer informatie.

> [!NOTE]  
> Wanneer u de para meter **/AlwaysExcludeUpgrade** gebruikt, wordt de automatische upgrade nog steeds uitgevoerd. Als CCMSetup echter wordt uitgevoerd om de upgrade uit te voeren, ziet u dat de para meter **/AlwaysExcludeUpgrade** is ingesteld en de volgende regel in het **CCMSetup. log**wordt geregistreerd:
>
> `Client is stamped with /alwaysexcludeupgrade. Stop proceeding.`
>
> CCMSetup wordt vervolgens onmiddellijk afgesloten en de upgrade niet uit te voeren.

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a>CCMSetup.exe retour codes

De CCMSetup.exe opdracht bevat de volgende retour codes. Als u problemen wilt oplossen, controleert u `%WinDir%\ccmsetup\ccmsetup.log` op de client voor context en aanvullende details over retour codes.

|Retourcode|Betekenis|  
|-----------|-------|  
|0|Geslaagd|  
|6|Fout|  
|7|Opnieuw opstarten is vereist|  
|8|Setup wordt reeds uitgevoerd|  
|9|Fout bij evaluatie van vereisten|  
|10|De hash-validatie is mislukt voor Setup-manifest|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a>Ccmsetup.msi eigenschappen

De volgende eigenschappen kunnen het installatie gedrag van ccmsetup.msi wijzigen.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

Gebruik deze ccmsetup. *MSI* -eigenschap om aanvullende opdracht regel parameters en eigenschappen door te geven aan ccmsetup. *exe*. Neem andere para meters en eigenschappen tussen aanhalings tekens ( `"` ) op. Gebruik deze eigenschap wanneer u de Configuration Manager-client Boots trapt met de [installatie methode van intune MDM](plan/client-installation-methods.md#microsoft-intune-mdm-installation).

Voorbeeld: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> Microsoft Intune beperkt de opdracht regel tot 1024 tekens.

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a>Client.msi eigenschappen

De volgende eigenschappen kunnen het installatie gedrag van client.msi wijzigen, dat ccmsetup.exe geïnstalleerd. Als u de [Push-client installatie methode](plan/client-installation-methods.md#client-push-installation)gebruikt, geeft u deze eigenschappen op het tabblad **client** van de eigenschappen van de **client push installatie** op in de Configuration Manager-console.

### <a name="aadclientappid"></a>AADCLIENTAPPID

Hiermee geeft u de id van de client-app voor Azure Active Directory (Azure AD). U maakt of importeert de client-app wanneer u [Azure-Services configureert](../../servers/deploy/configure/azure-services-wizard.md) voor Cloud beheer. Een Azure-beheerder kan de waarde voor deze eigenschap ophalen uit de Azure Portal. Zie voor meer informatie [toepassings-id ophalen](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). Voor de eigenschap **AADCLIENTAPPID** is deze toepassings-id voor het **systeem eigen** toepassings type.

Voorbeeld: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

Hiermee geeft u de id van de Azure AD-server-app op. U maakt of importeert de server-app wanneer u [Azure-Services configureert](../../servers/deploy/configure/azure-services-wizard.md) voor Cloud beheer. Wanneer u de server-app maakt in het venster Server toepassing maken, is deze eigenschap de **App-ID-URI**.

Een Azure-beheerder kan de waarde voor deze eigenschap ophalen uit de Azure Portal. Zoek in **Azure Active Directory**de server-app onder **app-registraties**. Zoek naar het toepassings type **Web app/API**. Open de app, selecteer **instellingen**en selecteer vervolgens **Eigenschappen**. Gebruik de **URI-waarde van de App-ID** voor deze **AADRESOURCEURI** -client installatie-eigenschap.

Voorbeeld: `ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTID

Hiermee geeft u de id van de Azure AD-Tenant. Configuration Manager koppelingen naar deze Tenant wanneer u [Azure-Services configureert](../../servers/deploy/configure/azure-services-wizard.md) voor Cloud beheer. Als u de waarde voor deze eigenschap wilt ophalen, gebruikt u de volgende stappen:

- Open een opdracht prompt op een Windows 10-apparaat dat is gekoppeld aan dezelfde Azure AD-Tenant.
- Voer de volgende opdracht uit:`dsregcmd.exe /status`
- Zoek in de sectie Apparaatstatus de waarde **TenantId** op. Bijvoorbeeld: `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

  > [!Note]
  > Een Azure-beheerder kan deze waarde ook verkrijgen in de Azure Portal. Zie [Tenant-id ophalen](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)voor meer informatie.

Voorbeeld: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Geeft een of meerdere Windows-gebruikersaccounts of -groepen om toegang te krijgen tot clientinstellingen en beleidsregels. Deze eigenschap is handig als u geen lokale beheerders referenties op de client computer hebt. Geef een lijst met accounts op die worden gescheiden door punt komma's ( `;` ).

Voorbeeld: `CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Als dat nodig is, laat u de computer na de installatie van de client op de achtergrond opnieuw opstarten.

> [!IMPORTANT]  
> Wanneer u deze eigenschap gebruikt, wordt de computer opnieuw opgestart zonder dat er een waarschuwing wordt gegeven. Dit probleem doet zich zelfs voor als een gebruiker is aangemeld bij Windows.

Voorbeeld: `CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

Als u wilt opgeven dat de client altijd op internet is gebaseerd en nooit verbinding maakt met het intranet, stelt u deze eigenschaps waarde in op `1` . Het verbindingstype van de client geeft **Altijd internet**weer.  

Gebruik deze eigenschap met [**CCMHOSTNAME**](#ccmhostname) om de FQDN-naam van het beheer punt op Internet op te geven. Gebruik deze ook met de CCMSetup-para meter [**/UsePKICert**](#usepkicert) en de site code ([**SMSSITECODE**](#smssitecode)).

Zie [overwegingen voor client communicatie via internet of een niet-vertrouwd forest](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)voor meer informatie over client beheer op internet.

Voorbeeld: `CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

Gebruik deze eigenschap om de lijst met certificaat verleners op te geven. Deze lijst bevat certificaat gegevens voor vertrouwde basis certificerings instanties (CA) die de Configuration Manager site vertrouwt.  

Deze waarde is een hoofdletter gevoelige overeenkomst voor kenmerk kenmerken die zich in het basis-CA-certificaat bevinden. Scheid kenmerken door een komma ( `,` ) of een punt komma ( `;` ). Geef meer dan één basis-CA-certificaat op met behulp van een scheidings balk ( `|` ).

Voorbeeld: `CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> Gebruik de waarde van het kenmerk **CertificateIssuers** in het bestand **mobileclient. TCF** voor de site. Dit bestand bevindt zich in de `\bin\<platform>` submap van de installatiemap van Configuration Manager op de site server.

Voor meer informatie over de lijst met certificaat verleners en hoe clients deze gebruiken tijdens het certificaat selectie proces, Zie [planning voor de selectie van PKI-client certificaten](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).

### <a name="ccmcertsel"></a>CCMCERTSEL

Als de client meer dan één certificaat voor HTTPS-communicatie heeft, geeft deze eigenschap de criteria op om een geldig client verificatie certificaat te selecteren.

Gebruik de volgende tref woorden om de onderwerpnaam van het certificaat of de alternatieve naam voor het onderwerp te zoeken:

- **Onderwerp**: een exacte overeenkomst zoeken
- **SubjectStr**: een gedeeltelijke overeenkomst zoeken

Voorbeelden:

- `CCMCERTSEL="Subject:computer1.contoso.com"`: Zoek naar een certificaat met een exacte overeenkomst met de naam van de computer `computer1.contoso.com` in de onderwerpnaam of de alternatieve naam voor het onderwerp.

- `CCMCERTSEL="SubjectStr:contoso.com"`: Zoek naar een certificaat dat `contoso.com` in de onderwerpnaam of de alternatieve naam voor het onderwerp bevat.

Gebruik het sleutel woord **SubjectAttr** om te zoeken naar de kenmerken van de object-id (OID) of de DN-naam in de onderwerpnaam of alternatieve naam voor het onderwerp.

Voorbeelden:

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`: Zoek naar het kenmerk organisatie-eenheid uitgedrukt als een object-id en met de naam `Computers` .

- `CCMCERTSEL="SubjectAttr:OU = Computers"`: Zoek naar het kenmerk organisatie-eenheid, uitgedrukt als een DN-naam en met de naam `Computers` .

> [!IMPORTANT]
> Als u de onderwerpnaam gebruikt, is het sleutel woord **onderwerp** hoofdletter gevoelig en is het sleutel woord **SubjectStr** niet hoofdletter gevoelig.
>
> Als u de alternatieve naam voor het onderwerp gebruikt, zijn de **onderwerp** -en **SubjectStr** -sleutel woorden niet hoofdletter gevoelig.

Zie [ondersteunde kenmerk waarden voor de selectie criteria van PKI-certificaten](#BKMK_attributevalues)voor de volledige lijst met kenmerken die u kunt gebruiken voor het selecteren van certificaten.

Als meer dan één certificaat overeenkomt met de zoek opdracht en u [**CCMFIRSTCERT**](#ccmfirstcert) instelt op `1` , selecteert het client installatie programma het certificaat met de langste geldigheids periode.

### <a name="ccmcertstore"></a>CCMCERTSTORE

Als het installatie programma van de client geen geldig certificaat kan vinden in het standaard **persoonlijke** certificaat Archief voor de computer, gebruikt u deze eigenschap om een alternatieve naam voor het certificaat archief op te geven.

Voorbeeld: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

Met deze eigenschap wordt logboek registratie van fout opsporing ingeschakeld wanneer de client wordt geïnstalleerd. Deze eigenschap zorgt ervoor dat de client informatie op laag niveau registreert voor het oplossen van problemen. Vermijd het gebruik van deze eigenschap in productie sites. Overmatige logboek registratie kan optreden, waardoor het lastig is om relevante informatie te vinden in de logboek bestanden. Schakel [**CCMENABLELOGGING**](#ccmenablelogging)ook in.

Ondersteunde waarden:

- `0`: Logboek registratie voor fout opsporing uitschakelen (standaard)
- `1`: Schakel logboek registratie van fout opsporing in

Voorbeeld: `CCMSetup.exe CCMDEBUGLOGGING=1`  

Zie [over logboek bestanden](../../plan-design/hierarchy/about-log-files.md)voor meer informatie.

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

Met Configuration Manager wordt logboek registratie standaard ingeschakeld.

Ondersteunde waarden:

- `TRUE`: Logboek registratie inschakelen (standaard)
- `FALSE`: Logboek registratie uitschakelen

Voorbeeld: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

Zie [over logboek bestanden](../../plan-design/hierarchy/about-log-files.md)voor meer informatie.

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

De frequentie in minuten waarmee het hulp programma voor client status evaluatie (ccmeval.exe) wordt uitgevoerd. Geef een geheel getal op van `1` tot `1440` . Ccmeval wordt standaard eenmaal per dag uitgevoerd (1440 minuten).

Voorbeeld: `CCMSetup.exe CCMEVALINTERVAL=1440`

Zie [clients controleren](../manage/monitor-clients.md#bkmk_health)voor meer informatie over de evaluatie van de client status.

### <a name="ccmevalhour"></a>CCMEVALHOUR

Het uur gedurende de dag waarop het hulp programma voor de evaluatie van de client status (ccmeval.exe) wordt uitgevoerd. Geef een geheel getal op tussen `0` (middernacht) tot en met `23` (11:00 pm). Ccmeval wordt standaard om middernacht uitgevoerd.

Zie [clients controleren](../manage/monitor-clients.md#bkmk_health)voor meer informatie over de evaluatie van de client status.

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

Als u deze eigenschap instelt op `1` , selecteert de client het PKI-certificaat met de langste geldigheids duur.

Voorbeeld: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

Als de client via internet wordt beheerd, geeft deze eigenschap de FQDN-naam van het beheer punt op internet.  

Geef deze optie niet op met de installatie-eigenschap **SMSSITECODE = auto**. Wijs rechtstreeks op internet gebaseerde clients toe aan een site op internet.

Voorbeeld: `CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Met deze eigenschap kunt u het adres van een CMG (Cloud Management Gateway) opgeven. Als u de waarde voor deze eigenschap wilt ophalen, gebruikt u de volgende stappen:

- Een CMG maken. Zie [een CMG instellen](../manage/cmg/setup-cloud-management-gateway.md)voor meer informatie.
- Open een Windows Power shell-opdracht prompt als beheerder op een actieve client.
- Voer de volgende opdracht uit:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- Gebruik de geretourneerde waarde als-is met de eigenschap **CCMHOSTNAME** .

Bijvoorbeeld: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Wanneer u het adres opgeeft van een CMG voor de eigenschap **CCMHOSTNAME** , moet u geen voor voegsel toevoegen, zoals `https://` . Gebruik dit voor voegsel alleen met de **/MP** -URL van een CMG.

### <a name="ccmhttpport"></a>CCMHTTPPORT

Hiermee geeft u de poort op die de client moet gebruiken wanneer deze via HTTP communiceert met site systeem servers. Deze waarde is standaard ingesteld op `80` .

Voorbeeld: `CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Hiermee geeft u de poort op die de client moet gebruiken wanneer deze via HTTPS communiceert met site systeem servers. Deze waarde is standaard ingesteld op `443` .

Voorbeeld: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

Gebruik deze eigenschap om de map in te stellen voor de installatie van de Configuration Manager-client bestanden. De standaard instelling wordt gebruikt `%WinDir%\CCM` .

> [!TIP]
> Ongeacht waar u de client bestanden installeert, wordt altijd het **ccmcore.dll** -bestand in de map geïnstalleerd `%WinDir%\System32` . Op een 64-bits besturings systeem wordt een kopie van ccmcore.dll in de `%WinDir%\SysWOW64` map geïnstalleerd. Dit bestand ondersteunt 32-bits toepassingen die gebruikmaken van de 32-bits versie van de client-Api's van de Configuration Manager SDK.

Voorbeeld: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Met deze eigenschap geeft u het detail niveau op dat naar Configuration Manager logboek bestanden moet worden geschreven.

Ondersteunde waarden:

- `0`: Uitgebreid
- `1`: Standaard
- `2`: Waarschuwingen en fouten
- `3`: Alleen fouten

Voorbeeld: `CCMSetup.exe CCMLOGLEVEL=0`

Zie [over logboek bestanden](../../plan-design/hierarchy/about-log-files.md)voor meer informatie.

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Wanneer een Configuration Manager logboek bestand de maximale grootte bereikt, wordt de naam van de client gewijzigd als back-up en wordt er een nieuw logboek bestand gemaakt. Met deze eigenschap geeft u op hoeveel vorige versies van het logboek bestand moeten worden bewaard. De standaardwaarde is `1`. Als u de waarde instelt op `0` , houdt de client geen logboek bestands geschiedenis.

Voorbeeld: `CCMSetup.exe CCMLOGMAXHISTORY=5`

Zie [over logboek bestanden](../../plan-design/hierarchy/about-log-files.md)voor meer informatie.

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Met deze eigenschap geeft u de maximale grootte van het logboek bestand in bytes. Wanneer een logboek groter wordt dan de opgegeven grootte, wordt de naam van de client gewijzigd in een geschiedenis bestand en wordt er een nieuwe gemaakt. De standaard grootte is 250.000 bytes en de minimale grootte is 10.000 bytes.

Voor beeld: `CCMSetup.exe CCMLOGMAXSIZE=300000` (300.000 bytes)

### <a name="disablesiteopt"></a>DISABLESITEOPT

Stel deze eigenschap in op `TRUE` om te voor komen dat beheerders de toegewezen site wijzigen in het configuratie scherm van Configuration Manager.

Voorbeeld: **CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Als deze eigenschap is ingesteld op TRUE, wordt de mogelijkheid van gebruikers met beheerders rechten voor het wijzigen van de instellingen van de cachemap van de client in het configuratie scherm van **Configuration Manager** .  

Voorbeeld: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

Geef een DNS-domein voor clients op om beheer punten te vinden die u in DNS publiceert. Wanneer de client een beheer punt vindt, vertelt het de client over andere beheer punten in de hiërarchie. Dit gedrag houdt in dat het beheer punt dat de client van DNS vindt, een wille keurig item in de hiërarchie kan zijn.

> [!NOTE]
> U hoeft deze eigenschap niet op te geven als de client zich in hetzelfde domein bevindt als een gepubliceerd beheer punt. In dat geval wordt het domein van de client automatisch gebruikt voor het zoeken naar DNS voor beheer punten.

Zie [service locatie en hoe clients het toegewezen beheer punt bepalen](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)voor meer informatie over DNS-publicatie als een service locatie methode voor Configuration Manager-clients.

> [!NOTE]  
> DNS wordt standaard niet door Configuration Manager ingeschakeld.

Voorbeeld: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

Geef het terugval status punt op dat status berichten ontvangt en verwerkt die door Configuration Manager clients worden verzonden.

Zie [bepalen of u een terugval status punt nodig hebt](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)voor meer informatie.

Voorbeeld: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

Als u deze eigenschap instelt op `TRUE` , controleert het installatie programma van de client niet de mini maal vereiste versie van micro soft Application Virtualization (app-V).

> [!IMPORTANT]  
> Als u de Configuration Manager-client installeert zonder app-V te installeren, kunt u geen [virtuele toepassingen implementeren](../../../apps/get-started/deploying-app-v-virtual-applications.md).

Voorbeeld: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

Wanneer u deze eigenschap inschakelt, wordt de status van de client gerapporteerd, maar worden de gevonden problemen niet opgelost.

Voorbeeld: `CCMSetup.exe NOTIFYONLY=TRUE`

Zie [How to configure client status](configure-client-status.md)voor meer informatie.

### <a name="provisionts"></a>PROVISIONTS

<!--5526972-->

Vanaf versie 2002 gebruikt u deze eigenschap om een taken reeks op een client te starten nadat deze is geregistreerd bij de site.

> [!NOTE]
> Als de taken reeks software-updates of-toepassingen installeert, hebben clients een geldig certificaat voor client verificatie nodig. Alleen token verificatie werkt niet. Zie [release opmerkingen-OS-implementatie](../../servers/deploy/install/release-notes.md#os-deployment)voor meer informatie.<!--7527072-->
      
U kunt bijvoorbeeld een nieuw Windows 10-apparaat met Windows auto pilot inrichten, het automatisch inschrijven voor Microsoft Intune en vervolgens de Configuration Manager-client installeren voor co-beheer. Als u deze nieuwe optie opgeeft, voert de zojuist ingerichte client een taken reeks uit. Dit proces biedt extra flexibiliteit voor het installeren van toepassingen en software-updates, of het configureren van instellingen.


Gebruik het volgende proces:

1. [Maak een taken reeks voor een implementatie zonder besturings systeem](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md) om apps te installeren, software-updates te installeren en instellingen te configureren.

1. [Implementeer deze taken reeks](../../../osd/deploy-use/deploy-a-task-sequence.md) voor de nieuwe ingebouwde verzameling, **alle inrichtings apparaten**. Let op de implementatie-ID van de taken reeks, bijvoorbeeld `PRI20001` .

1. [Installeer de Configuration Manager-client](deploy-clients-to-windows-computers.md#BKMK_Manual) op een apparaat en voeg de volgende eigenschap toe: `PROVISIONTS=PRI20001` . Stel de waarde van deze eigenschap in als de ID van de taken reeks implementatie.

    - Als u de-client van intune installeert tijdens de inschrijving van het co-beheer, Zie [hoe u op internet gebaseerde apparaten voorbereidt voor co-beheer](../../../comanage/how-to-prepare-Win10.md).

      > [!NOTE]
      > Deze methode kan extra vereisten hebben. U kunt bijvoorbeeld de site inschrijven voor Azure Active Directory of een Cloud beheer gateway maken die geschikt is voor inhoud.

Nadat de client is geïnstalleerd en op de juiste wijze is geregistreerd bij de site, wordt de taken reeks waarnaar wordt verwezen, gestart. Als de client registratie mislukt, wordt de taken reeks niet gestart.



### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

Als een client de verkeerde Configuration Manager vertrouwde basis sleutel heeft, kan deze geen verbinding maken met een vertrouwd beheer punt om de nieuwe vertrouwde basis sleutel te ontvangen. Gebruik deze eigenschap om de oude vertrouwde basis sleutel te verwijderen. Deze situatie kan zich voordoen wanneer u een client verplaatst van de ene site hiërarchie naar een andere. Deze eigenschap is van toepassing op cliënten die HTTP- en HTTPS-clientcommunicatie gebruiken. Zie [planning voor de vertrouwde basis sleutel](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)voor meer informatie.

Voorbeeld: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Hiermee wordt automatische site toewijzing voor client upgrades ingeschakeld wanneer deze wordt gebruikt met [SMSSITECODE = auto](#smssitecode).

Voorbeeld: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Hiermee geeft u de locatie van de cachemap van de client op de client computer. De locatie van de cache is standaard `%WinDir%\ccmcache` .

Voorbeeld: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Gebruik deze eigenschap met de eigenschap [**SMSCACHEFLAGS**](#smscacheflags) om de locatie van de cachemap van de client te beheren. Als u bijvoorbeeld de cachemap van de client wilt installeren op het grootste beschik bare client schijf station:`CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Gebruik deze eigenschap om verdere installatie Details op te geven voor de cachemap van de client. U kunt **SMSCACHEFLAGS** -eigenschappen afzonderlijk of in combi natie gescheiden door punt komma's ( `;` ) gebruiken.

Als u deze eigenschap niet opneemt:

- De-client installeert de cachemap volgens de eigenschap [**SMSCACHEDIR**](#smscachedir)
- De map is niet gecomprimeerd
- De-client gebruikt de eigenschap [**SMSCACHESIZE**](#smscachesize) als de maximale grootte in MB van de cache

Wanneer u een bestaande client bijwerkt, wordt deze eigenschap door het installatie programma van de client genegeerd.

#### <a name="values-for-the-smscacheflags-property"></a>Waarden voor de eigenschap SMSCACHEFLAGS

- **PERCENTDISKSPACE**: Stel de cache grootte in als een percentage van de *totale* schijf ruimte. Als u deze eigenschap opgeeft, stelt u ook [**SMSCACHESIZE**](#smscachesize) in op een percentage waarde.

- **PERCENTFREEDISKSPACE**: Stel de cache grootte in als een percentage van de *vrije* schijf ruimte. Als u deze eigenschap opgeeft, stelt u ook [**SMSCACHESIZE**](#smscachesize) in als een percentage waarde. De schijf heeft bijvoorbeeld 10 MB gratis en u geeft aan `SMSCACHESIZE=50` . Het client installatie programma stelt de cache grootte in op 5 MB. U kunt deze eigenschap niet gebruiken met de eigenschap **PERCENTDISKSPACE** .

- **MAXDRIVE**: Installeer de cache op de grootste beschik bare schijf. Als u een pad opgeeft met de eigenschap [**SMSCACHEDIR**](#smscachedir) , wordt deze waarde door het client installatie programma genegeerd.

- **MAXDRIVESPACE**: Installeer de cache op het schijf station met de meeste vrije ruimte. Als u een pad opgeeft met de eigenschap [**SMSCACHEDIR**](#smscachedir) , wordt deze waarde door het client installatie programma genegeerd.

- **NTFSONLY**: Installeer alleen de cache op een schijf station met NTFS-indeling. Als u een pad opgeeft met de eigenschap [**SMSCACHEDIR**](#smscachedir) , wordt deze waarde door het client installatie programma genegeerd.

- **Comprimeren**: Sla de cache op in een gecomprimeerde vorm.

- **FAILIFNOSPACE**: als er onvoldoende ruimte is om de cache te installeren, verwijdert u de Configuration Manager-client.

Voorbeeld: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Client instellingen zijn beschikbaar voor het opgeven van de grootte van de cachemap van de client. Het toevoegen van die clientinstellingen vervangt SMSCACHESIZE als client.msi-eigenschap voor het opgeven van de grootte van de clientcache. Zie de [clientinstellingen voor cachegrootte](about-client-settings.md#client-cache-settings)voor meer informatie.  

Wanneer u een bestaande client bijwerkt, wordt deze instelling door het installatie programma van de client genegeerd. De client negeert ook de cache grootte wanneer software-updates worden gedownload.

Voorbeeld: `CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> Als u een client opnieuw installeert, kunt u **SMSCACHESIZE** of **SMSCACHEFLAGS** niet gebruiken om de cache grootte zo in te stellen dat deze kleiner is dan voorheen. De vorige grootte is de minimum waarde.

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Gebruik deze eigenschap om de locatie en volg orde op te geven die het client installatie programma controleert op configuratie-instellingen. Het is een teken reeks van een of meer tekens die elk een specifieke configuratie bron definiëren:

- `R`: Controleer op configuratie-instellingen in het REGI ster.

  Zie [Eigenschappen van client installatie inrichten](deploy-clients-to-windows-computers.md#BKMK_Provision)voor meer informatie.

- `P`: Controleer op configuratie-instellingen in de installatie-eigenschappen vanaf de opdracht regel.

- `M`: Controleren op bestaande instellingen wanneer u een oudere client bijwerkt.

- `U`: Upgrade de geïnstalleerde client naar een nieuwere versie en gebruik de toegewezen site code.

Standaard gebruikt het installatie programma van de client `PU` . Eerst worden de installatie-eigenschappen ( `P` ) en vervolgens de bestaande instellingen ( `U` ) gecontroleerd.  

Voorbeeld: `CCMSetup.exe SMSCONFIGSOURCE=RP`

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

Specificeert of de client Windows Internet Name Service (WINS) kan gebruiken om een beheerpunt te vinden dat HTTP-verbindingen aanvaardt. Clients gebruiken deze methode wanneer ze geen beheer punt in Active Directory Domain Services of in DNS kunnen vinden.

Deze eigenschap is niet van invloed op het feit of de client WINS gebruikt voor naam omzetting.

U kunt twee verschillende modi voor deze eigenschap configureren:

- Niet **-WINS**: deze waarde is de veiligste instelling voor deze eigenschap. Het voor komt dat clients een beheer punt in WINS vinden. Wanneer u deze instelling gebruikt, moeten clients een andere methode hebben om een beheer punt op het intranet te vinden. Bijvoorbeeld Active Directory Domain Services of DNS-publicatie.

- **WINSSECURE** (standaard): in deze modus kan een client die http-communicatie gebruikt, WINS gebruiken om een beheer punt te vinden. De client moet echter een kopie van de vertrouwde basissleutel hebben voordat het een verbinding kan maken met het beheerpunt. Zie [planning voor de vertrouwde basis sleutel](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)voor meer informatie.

Voorbeeld: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Hiermee geeft u een initieel beheer punt voor de Configuration Manager-client moet worden gebruikt.  

> [!IMPORTANT]  
> Als het beheer punt alleen client verbindingen via HTTPS accepteert, wordt de naam van het beheer punt voorafgegaan door `https://` .

Voorbeelden:

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

Als de client de Configuration Manager vertrouwde basis sleutel niet kan verkrijgen van Active Directory Domain Services, gebruikt u deze eigenschap om de sleutel op te geven. Deze eigenschap is van toepassing op clients die gebruikmaken van HTTP-en HTTPS-communicatie. Zie [planning voor de vertrouwde basis sleutel](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)voor meer informatie.

Voorbeeld: `CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> Haal de waarde voor de vertrouwde basis sleutel van de site op uit het bestand mobileclient. TCF op de site server. Zie [een client vooraf inrichten met de vertrouwde basis sleutel met behulp van een bestand](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file)voor meer informatie.

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

Gebruik deze eigenschap om de Configuration Manager vertrouwde basis sleutel opnieuw te installeren. Hiermee geeft u het volledige pad en de naam van een bestand dat de vertrouwde basis sleutel bevat. Deze eigenschap is van toepassing op cliënten die HTTP- en HTTPS-clientcommunicatie gebruiken. Zie [planning voor de vertrouwde basis sleutel](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)voor meer informatie.

Voorbeeld: `CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

Hiermee geeft u het volledige pad en de naam van het geëxporteerde zelfondertekende certificaat op de site server. De site server slaat dit certificaat op in het **SMS** -certificaat archief. Het heeft de object naam **Site Server** en de beschrijvende naam **handtekening certificaat van de site server**.

Voorbeeld: `CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

Met deze eigenschap geeft u een Configuration Manager site op waaraan u de client toewijst. Deze waarde kan een site code van drie tekens of het woord zijn `AUTO` . Als u `AUTO` Deze eigenschap opgeeft of niet opgeeft, probeert de client de site toewijzing te bepalen van Active Directory Domain Services of van een opgegeven beheer punt. Als u wilt inschakelen `AUTO` voor client upgrades, stelt u ook [SITEREASSIGN = True](#sitereassign)in.

> [!NOTE]  
> Als u ook een beheer punt op Internet opgeeft met de eigenschap [**CCMHOSTNAME**](#ccmhostname) , gebruikt u niet `AUTO` met **SMSSITECODE**. De client rechtstreeks toewijzen aan de site door de site code op te geven.

Voorbeeld: `CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a>Kenmerk waarden voor de selectie criteria van het certificaat

Configuration Manager ondersteunt de volgende kenmerk waarden voor de selectie criteria van PKI-certificaten:

|OID-kenmerk|DN-naamkenmerk|Kenmerkdefinitie|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|Domeinonderdeel|  
|1.2.840.113549.1.9.1|E of e-mailbericht|E-mailadres|  
|2.5.4.3|CN|Algemene naam|  
|2.5.4.4|SN|Onderwerpnaam|  
|2.5.4.5|SERIENUMMER|Serienummer|  
|2.5.4.6|C|Landcode|  
|2.5.4.7|L|Plaats|  
|2.5.4.8|S of ST|Naam van staat of provincie|  
|2.5.4.9|STRAAT|Adres|  
|2.5.4.10|O|Organisatienaam|  
|2.5.4.11|ORGANISATIE-EENHEID|Organisatie-eenheid|  
|2.5.4.12|T of titel|Titel|  
|2.5.4.42|G of GN of voornaam|Voornaam|  
|2.5.4.43|I of initialen|Initialen|  
|2.5.29.17|(geen waarde)|Alternatieve onderwerpnaam|  

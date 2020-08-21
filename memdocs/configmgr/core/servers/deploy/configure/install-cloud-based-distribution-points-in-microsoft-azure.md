---
title: Cloud distributiepunten installeren
titleSuffix: Configuration Manager
description: Gebruik deze stappen om een Cloud distributiepunt in Configuration Manager in te stellen.
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4a1e19025af82c9beeed8c227871df94b4674791
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692703"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Een Cloud distributiepunt voor Configuration Manager installeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> De implementatie voor het delen van inhoud van Azure is gewijzigd. Gebruik een Cloud beheer gateway die is ingeschakeld voor inhoud door de optie in te scha kelen om **CMG te laten functioneren als een Cloud distributiepunt en inhoud te bezorgen bij Azure Storage**. Zie [een CMG wijzigen](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg)voor meer informatie.
>
> U kunt in de toekomst geen traditioneel Cloud distributiepunt maken. Zie [verwijderde en afgeschafte functies](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.

In dit artikel vindt u meer informatie over de stappen voor het installeren van een Configuration Manager Cloud distributiepunt in Microsoft Azure. De sectie bevat de volgende secties:

- [Voordat u begint](#bkmk_before)
- [Instellen](#bkmk_setup)
- [DNS configureren](#bkmk_dns)
- [Site server proxy instellen](#bkmk_proxy)
- [Inhoud distribueren en clients configureren](#bkmk_client)
- [Beheren en bewaken](#bkmk_monitor)
- [Wijzigen](#bkmk_modify)
- [Geavanceerde probleemoplossing](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a> Voordat u begint

Lees eerst het artikel [een Cloud distributiepunt gebruiken](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Dit artikel helpt u bij het plannen en ontwerpen van uw Cloud distributiepunten.

Gebruik de volgende controle lijst om ervoor te zorgen dat u over de benodigde informatie en vereisten beschikt voor het maken van een Cloud distributiepunt:  

- De site server kan verbinding maken met Azure. Als uw netwerk gebruikmaakt van een proxy, [configureert u de site systeemrol](#bkmk_proxy).  

- De **Azure-omgeving** die moet worden gebruikt. Bijvoorbeeld de open bare Azure-Cloud of de Azure-Cloud voor de Amerikaanse overheid.  

- Vanaf versie 1806 en *Aanbevolen*moet u de **Azure Resource Manager-implementatie**gebruiken. Hiervoor gelden de volgende vereisten:<!--1322209-->  

    - Integratie met [Azure Active Directory](azure-services-wizard.md) voor **Cloud beheer**. Azure AD-gebruikers detectie is niet vereist.  

    - De ID van het Azure **-abonnement**.  

    - De Azure- **resource groep**.  

    - Een **account voor abonnements beheerders** moet zich aanmelden tijdens de wizard.  

- Een **certificaat voor Server verificatie**, geëxporteerd als een. PFX-bestand.  

- Een wereld wijd unieke **service naam** voor het Cloud distributiepunt.  

    > [!TIP]  
    > Voordat u het Server verificatie certificaat aanvraagt dat deze service naam gebruikt, controleert u of de gewenste Azure-domein naam uniek is. Bijvoorbeeld *WallaceFalls.CloudApp.net*.
    >
    > 1. Meld u aan bij de [Azure-portal](https://portal.azure.com).
    > 1. Selecteer **alle resources**en selecteer vervolgens **toevoegen**.
    > 1. Zoek naar de **Cloud service**. Selecteer **Maken**.
    > 1. Typ in het veld **DNS-naam** het gewenste voor voegsel, bijvoorbeeld *WallaceFalls*. De interface geeft aan of de domein naam beschikbaar is of al door een andere service wordt gebruikt.
    >
    > Maak de service niet in de portal. Gebruik dit proces alleen om de beschik baarheid van de naam te controleren.

- De Azure- **regio** voor deze implementatie.  

- Als u de implementatie van de klassieke Azure- **service** nog steeds moet gebruiken in Configuration Manager versie 1810 of eerder, hebt u de volgende vereisten nodig:  

    > [!Important]  
    > Vanaf versie 1810 worden de klassieke service-implementaties in azure afgeschaft in Configuration Manager. Begin met het gebruik van Azure Resource Manager-implementaties voor het Cloud distributiepunt. Zie [Azure Resource Manager](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager)voor meer informatie.  
    >
    > Vanaf Configuration Manager versie 1902 is Azure Resource Manager het enige implementatie mechanisme voor nieuwe exemplaren van het Cloud distributiepunt.<!-- 3605704 -->

    - De ID van het Azure **-abonnement**.  

    - Een Azure- **beheer certificaat**, geëxporteerd als beide. CER en. PFX-bestanden. Een beheerder van een Azure-abonnement moet de toevoegen. CER-beheer certificaat voor het abonnement in de [Azure Portal](https://portal.azure.com).  

### <a name="branchcache"></a>BranchCache

Als u een Cloud distributiepunt wilt inschakelen voor het gebruik van Windows BranchCache, installeert u het onderdeel BranchCache op de site server.<!-- SCCMDocs-pr#4054 -->

- Als de site server een site systeemrol van een on-premises distributie punt heeft, configureert u de optie in de eigenschappen van die rol om BranchCache in te **scha kelen en te configureren**. Zie [Configure a Distribution Point (een distributie punt configureren](install-and-configure-distribution-points.md#bkmk_config-general)) voor meer informatie.

- Als de site server geen rol voor distributie punt heeft, installeert u de BranchCache-functie in Windows. Zie [de BranchCache-functie installeren](/windows-server/networking/branchcache/deploy/install-the-branchcache-feature)voor meer informatie.

Als u inhoud al hebt gedistribueerd naar een Cloud distributiepunt en vervolgens wilt inschakelen BranchCache, installeert u eerst de functie. Distribueer de inhoud vervolgens opnieuw naar het Cloud distributiepunt.

> [!NOTE]  
> Als u meer dan één Cloud distributiepunt hebt, moet u in Configuration Manager versie 1810 en eerder de wachtwoordzin voor de BranchCache-sleutel hand matig instellen. Zie [Microsoft ondersteuning KB 4458143](https://support.microsoft.com/help/4458143)voor meer informatie.

## <a name="set-up"></a><a name="bkmk_setup"></a> Instellen  

Voer deze procedure uit op de site als host van dit Cloud distributiepunt zoals bepaald door uw [ontwerp](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology).  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer **Cloud distributiepunten**. Selecteer in het lint **Cloud distributiepunt maken**.  

2. Configureer de volgende instellingen op de pagina **Algemeen** van de wizard Cloud distributiepunt maken:  

    1. Geef eerst de **Azure-omgeving**op.  

    2. Vanaf versie 1806 en *Aanbevolen*selecteert u **Azure Resource Manager implementatie** als implementatie methode. Selecteer **Aanmelden** om te verifiëren met een Azure-abonnement beheerders account. Met de wizard worden de resterende velden automatisch ingevuld op basis van de gegevens die zijn opgeslagen tijdens de vereisten voor Azure AD-integratie. Als u meerdere abonnementen hebt, selecteert u de **abonnements-id** van het gewenste abonnement dat u wilt gebruiken.  

    > [!Note]  
    > Vanaf versie 1810 worden de klassieke service-implementaties in azure afgeschaft in Configuration Manager.
    >
    > Als u een klassieke service-implementatie wilt gebruiken, selecteert u die optie op deze pagina. Voer eerst uw Azure **-abonnements-id**in. Selecteer vervolgens **Bladeren** en selecteer de. PFX-bestand voor het Azure-beheer certificaat.  

3. Selecteer **Next**. Wacht tot de site de verbinding met Azure test.  

4. Geef op de pagina **instellingen** de volgende instellingen op en selecteer **volgende**:  

    - **Regio**: Selecteer de Azure-regio waar u het Cloud distributiepunt wilt maken.  

    - **Resource groep** (alleen Azure Resource Manager implementatie methode)  

        - **Bestaande gebruiken**: Selecteer een bestaande resource groep in de vervolg keuzelijst.  

        - **Nieuwe maken**: Voer de naam in van de nieuwe resource groep die u in uw Azure-abonnement wilt maken.  

    - **Primaire site**: Selecteer de primaire site om inhoud te distribueren naar dit distributie punt.

    - **Certificaat bestand**: Selecteer **Bladeren** en selecteer de. PFX-bestand voor het Server verificatie certificaat van dit Cloud distributiepunt. De algemene naam van dit certificaat vult de vereiste velden **FQDN** en **service naam** van de service in.  

        > [!NOTE]  
        > Het certificaat voor Server verificatie van het Cloud distributiepunt ondersteunt joker tekens. Als u een certificaat met Joker tekens gebruikt, vervangt u het sterretje ( `*` ) in het veld **FQDN van service** door de gewenste hostnaam voor de service.  

5. Stel op de pagina **waarschuwingen** opslag quota's, quota voor overdracht en in welk percentage van deze quota's u Configuration Manager waarschuwingen wilt genereren. Selecteer vervolgens **Volgende**.  

6. Voltooi de wizard.  

### <a name="monitor-installation"></a>Installatie bewaken  

De site begint met het maken van een nieuwe gehoste service voor het Cloud distributiepunt. Nadat u de wizard hebt gesloten, controleert u de voortgang van de installatie van het Cloud distributiepunt in de Configuration Manager-console. Bewaak ook het bestand **CloudMgr. log** op de primaire site server. Controleer, indien nodig, de inrichting van de Cloud service in de Azure Portal.  

> [!NOTE]  
> Het kan tot 30 minuten duren om een nieuw distributie punt in te richten in Azure. Het bestand **CloudMgr. log** herhaalt het volgende bericht totdat het opslag account is ingericht:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Nadat het opslag account is ingericht, wordt de service gemaakt en geconfigureerd.  

### <a name="verify-installation"></a>De installatie controleren

Controleer of de installatie van het Cloud distributiepunt is voltooid met behulp van de volgende methoden:  

- Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **Cloud Services**uit en selecteer het knoop punt **Cloud distributiepunten** . Zoek het nieuwe Cloud distributiepunt in de lijst. De kolom Status moet **gereed**zijn.  

- Ga in de Configuration Manager-console naar de werk ruimte **bewaking** . Vouw **systeem status**uit en selecteer het knoop punt **onderdeel status** . Geef alle berichten van het onderdeel **SMS_CLOUD_SERVICES_MANAGER** weer en zoek naar status bericht-id **9409**.  

- Ga indien nodig naar de Azure Portal. In de **implementatie** voor het Cloud distributiepunt wordt de status **gereed**weer gegeven.  


## <a name="configure-dns"></a><a name="bkmk_dns"></a> DNS configureren  

Voordat clients het Cloud distributiepunt kunnen gebruiken, moeten ze de naam van het Cloud distributiepunt kunnen omzetten naar een IP-adres dat door Azure wordt beheerd. Het beheer punt geeft de **service-FQDN** van het Cloud distributiepunt. Het Cloud distributiepunt bestaat in azure als de **service naam**. Zie deze waarden op het tabblad **instellingen** van de eigenschappen van het Cloud distributiepunt.

> [!Note]  
> Het knoop punt **Cloud distributiepunt** in de-console bevat een kolom met de naam **service naam**, maar de waarde van de **service-FQDN** wordt in werkelijkheid weer gegeven. Als u beide waarden wilt zien, opent u **Eigenschappen** voor het Cloud distributiepunt en schakelt u over naar het tabblad **instellingen** .  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

De algemene naam van het Server verificatie certificaat moet uw domein naam bevatten. Deze naam is vereist wanneer u een certificaat van een open bare provider aanschaft. Het wordt aanbevolen om dit certificaat uit te geven via uw PKI. Bijvoorbeeld `WallaceFalls.contoso.com`. Wanneer u dit certificaat opgeeft in de wizard Cloud distributiepunt maken, vult de algemene naam de **service FQDN** -eigenschap ( `WallaceFalls.contoso.com` ) in. De **service naam** heeft dezelfde hostnaam ( `WallaceFalls` ) en voegt deze toe aan de naam van het Azure-domein `cloudapp.net` . In dit scenario moeten clients de **service FQDN** () van uw domein omzetten `WallaceFalls.contoso.com` in de **naam** van de Azure-service ( `WallaceFalls.cloudapp.net` ). Maak een CNAME-alias om deze namen toe te wijzen.

### <a name="create-cname-alias"></a>CNAME-alias maken

Maak een canonieke naam record (CNAME) in de open bare, Internet gerichte DNS van uw organisatie. Met deze record wordt een alias gemaakt voor de service- **FQDN** -eigenschap van het Cloud distributiepunt die door clients wordt ontvangen en de naam van de Azure- **service**. Maak bijvoorbeeld een nieuwe CNAME-record voor `WallaceFalls.contoso.com` `WallaceFalls.cloudapp.net` .  

### <a name="client-name-resolution-process"></a>Proces van client naam omzetting

In het volgende proces ziet u hoe een client de naam van het Cloud distributiepunt herleidt:  

1. De client ontvangt de **FQDN** van de service van het Cloud distributiepunt in de lijst met inhouds bronnen. Bijvoorbeeld `WallaceFalls.contoso.com`.  

2. Er wordt een query uitgevoerd op DNS, waarmee de FQDN van de service wordt omgezet met de CNAME-alias voor de naam van de Azure- **service**. Bijvoorbeeld `WallaceFalls.cloudapp.net`.  

3. DNS voert opnieuw een query uit, waarmee de naam van de Azure-service wordt omgezet in het open bare IP-adres van Azure.  

4. De client gebruikt dit IP-adres om communicatie met het Cloud distributiepunt te starten.  

5. Het Cloud distributiepunt geeft het Server verificatie certificaat aan de client. De client gebruikt de vertrouwens keten van het certificaat om te valideren.  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a> Site server proxy instellen  

De primaire site server die het Cloud distributiepunt beheert, moet communiceren met Azure. Als uw organisatie een proxy server gebruikt om Internet toegang te beheren, moet u de primaire site server configureren voor het gebruik van deze proxy.  

Zie [ondersteuning voor proxy server](../../../plan-design/network/proxy-server-support.md)voor meer informatie.  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a> Inhoud distribueren en clients configureren

Distribueer inhoud naar het Cloud distributiepunt hetzelfde als elk ander on-premises distributie punt. Het beheer punt bevat niet het distributie punt van de cloud in de lijst met inhouds locaties, tenzij het de inhoud bevat die clients aanvragen. Zie [inhoud distribueren en beheren](deploy-and-manage-content.md)voor meer informatie.

Beheer een Cloud distributiepunt hetzelfde als elk ander on-premises distributie punt. Deze acties omvatten het toewijzen van deze aan een distributiepunten groep en het beheren van inhouds pakketten. Zie [distributie punten installeren en configureren](install-and-configure-distribution-points.md)voor meer informatie.

Met standaard client instellingen kunnen clients automatisch Cloud distributiepunten gebruiken. Beheer de toegang tot alle Cloud distributiepunten in uw hiërarchie met de volgende client instelling:  

- Wijzig in de groep **Cloud instellingen** de instelling **toegang toestaan tot Cloud distributiepunten**.  

    - Deze instelling is standaard ingesteld op **Ja**.  

    - Wijzig en implementeer deze instelling voor zowel gebruikers als apparaten.  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a> Beheren en bewaken  

Bewaak inhoud die u naar een Cloud distributiepunt distribueert hetzelfde als met andere on-premises distributie punten. Zie [inhoud bewaken](monitor-content-you-have-distributed.md)voor meer informatie.

Wanneer u de lijst met Cloud distributiepunten weergeeft in de-console, kunt u aanvullende kolommen toevoegen aan de lijst. Bijvoorbeeld, de kolom **gegevens** uitgaand toont de hoeveelheid gegevensclients die in de afgelopen 30 dagen van de service is gedownload.<!-- SCCMDocs#755 -->

### <a name="alerts"></a><a name="bkmk_alerts"></a> Berichten  

Configuration Manager controleert periodiek de Azure-service. Als de service niet actief is of als er problemen zijn met het abonnement of het certificaat, wordt er Configuration Manager een waarschuwing gegenereerd.

Stel drempel waarden in voor de hoeveelheid gegevens die u wilt opslaan op het Cloud distributiepunt en voor de hoeveelheid gegevens die clients downloaden van het distributie punt. Gebruik waarschuwingen voor deze drempels om u te helpen bepalen wanneer u de Cloud service wilt stoppen of verwijderen, de inhoud wilt aanpassen die u opslaat op het Cloud distributiepunt of wijzigen welke clients de service kunnen gebruiken.

- **Waarschuwings drempel voor opslag**: met de waarschuwings drempel voor de opslag stelt u een bovenlimiet in van GB voor de hoeveelheid gegevens of inhoud die u wilt opslaan op het Cloud distributiepunt. Deze drempel waarde is standaard 2.000 GB. Configuration Manager genereert waarschuwings-en kritieke waarschuwingen wanneer de resterende vrije ruimte de niveaus bereikt die u opgeeft. Deze waarschuwingen worden standaard uitgevoerd om 50% en 90% van de drempel waarde.  

- **Waarschuwings drempel voor maandelijkse overdracht**: met de waarschuwings drempel voor maandelijkse overdracht kunt u de hoeveelheid inhoud bewaken die wordt overgedragen van het distributie punt naar clients gedurende een periode van 30 dagen. Deze drempel waarde is standaard 10.000 GB. De site genereert waarschuwings-en kritieke waarschuwingen wanneer overdrachten waarden bereiken die u definieert. Deze waarschuwingen worden standaard uitgevoerd om 50% en 90% van de drempel waarde.  

    > [!IMPORTANT]  
    > Configuration Manager bewaakt de overdracht van gegevens, maar stopt de overdracht van gegevens buiten de opgegeven waarschuwings drempel voor de overdracht.  

Geef drempels op voor elk Cloud distributiepunt tijdens de installatie, of gebruik het tabblad **waarschuwingen** van de eigenschappen van het Cloud distributiepunt.  

> [!NOTE]  
> Waarschuwingen voor een Cloud distributiepunt zijn afhankelijk van gebruiks statistieken van Azure. Dit kan tot 24 uur duren. Zie [Opslaganalyse](/rest/api/storageservices/storage-analytics)voor meer informatie over Opslaganalyse voor Azure.  

In een cyclus van een uur, downloadt de primaire site die het Cloud distributiepunt bewaakt transactie gegevens van Azure. Deze transactie gegevens worden opgeslagen in het `CloudDP-<ServiceName>.log` bestand op de site server. Configuration Manager wordt deze informatie vervolgens geëvalueerd op basis van de opslag-en overdrachts quota voor elk Cloud distributiepunt. Als de overdracht van gegevens het opgegeven volume bereikt of overschrijdt voor waarschuwingen of kritieke waarschuwingen, wordt Configuration Manager de juiste waarschuwing gegenereerd.  

> [!WARNING]  
> Omdat de site elk uur informatie over gegevens overdrachten downloadt van Azure, overschrijdt het gebruik mogelijk de drempel waarde voor waarschuwing of kritiek voordat Configuration Manager toegang krijgt tot de gegevens en een waarschuwing kan genereren.  


## <a name="modify"></a><a name="bkmk_modify"></a> Wijzigen

Bekijk informatie op hoog niveau over het distributie punt in het knoop punt **Cloud distributiepunten** onder **Cloud Services** in de werk ruimte **beheer** van de Configuration Manager-console. Selecteer een distributie punt en selecteer **Eigenschappen** om meer details weer te geven.  

Wanneer u de eigenschappen van een Cloud distributiepunt bewerkt, bevatten de volgende tabbladen de instellingen die u wilt bewerken:  

#### <a name="settings"></a>Instellingen

- **Beschrijving**  

- **Certificaat bestand**: Geef voordat het Server verificatie certificaat verloopt een nieuw certificaat met dezelfde algemene naam op. Voeg vervolgens het nieuwe certificaat toe om de service te gaan gebruiken. Als het certificaat is verlopen, worden clients niet vertrouwd en gebruiken ze de service niet.  

#### <a name="alerts"></a>Waarschuwingen

Wijzig de drempel waarden voor de gegevens voor opslag en waarschuwingen voor maandelijkse overdracht.  

#### <a name="content"></a>Inhoud

Beheer inhoud hetzelfde als voor een on-premises distributie punt.  

### <a name="redeploy-the-service"></a>De service opnieuw implementeren

Meer belang rijke wijzigingen, zoals de volgende configuraties, vereisen het opnieuw implementeren van de service:

- Klassieke implementatie methode voor het Azure Resource Manager
- Abonnement
- Servicenaam
- Privé voor open bare PKI
- Azure-regio

Vanaf versie 1806, als u een bestaand Cloud distributiepunt hebt op de klassieke implementatie methode, moet u een nieuw Cloud distributiepunt implementeren om de implementatie methode Azure Resource Manager te gebruiken. Er zijn twee opties:

- Als u dezelfde service naam opnieuw wilt gebruiken:  

    1. Verwijder eerst het klassieke Cloud distributiepunt. Als er nog geen Cloud distributiepunt is, kunnen clients mogelijk geen inhoud ophalen.  

    2. Maak een nieuw distributie punt in de Cloud met behulp van een Resource Manager-implementatie. Het certificaat voor Server verificatie opnieuw gebruiken.  

    3. Distribueer de inhoud van het benodigde software pakket naar het nieuwe Cloud distributiepunt.  

- Als u een nieuwe service naam wilt gebruiken:  

    1. Maak een nieuw distributie punt in de Cloud met behulp van een Resource Manager-implementatie. Gebruik een nieuw certificaat voor Server verificatie.  

    2. Distribueer de inhoud van het benodigde software pakket naar het nieuwe Cloud distributiepunt.  

    3. Het klassieke Cloud distributiepunt verwijderen.

> [!Tip]  
> Het huidige implementatie model van een Cloud distributiepunt bepalen:<!--SCCMDocs issue #611-->  
>
> 1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Cloud distributiepunten** .  
> 2. Voeg het kenmerk **implementatie model** als een kolom toe aan de lijst weergave. Dit kenmerk is **Azure Resource Manager**voor een Resource Manager-implementatie.  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>De Cloud service op aanvraag stoppen of starten

Stop een Cloud distributiepunt op elk gewenst moment in de Configuration Manager-console. Met deze actie voor komt u dat clients extra inhoud van de service kunnen downloaden. Start de Cloud service opnieuw vanuit de Configuration Manager-console om de toegang tot clients te herstellen. U kunt bijvoorbeeld een Cloud service stoppen wanneer deze een drempel waarde voor gegevens bereikt.  

Wanneer u een Cloud distributiepunt stopt, wordt de inhoud van het opslag account niet verwijderd door de Cloud service. Ook wordt niet voor komen dat de site server extra inhoud overdraagt naar het Cloud distributiepunt. Het beheer punt retourneert nog steeds het distributie punt van de Cloud naar clients als een geldige inhouds bron.

Gebruik de volgende procedure om een Cloud distributiepunt te stoppen:  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **Cloud Services**uit en selecteer het knoop punt **Cloud distributiepunten** .  

2. Selecteer het Cloud distributiepunt. Als u de Cloud service die in azure wordt uitgevoerd wilt stoppen, selecteert u **service stoppen** in het lint.  

3. Selecteer **service starten** om het Cloud distributiepunt opnieuw op te starten.  

### <a name="delete-a-cloud-distribution-point"></a>Een Cloud distributiepunt verwijderen

Als u een Cloud distributiepunt wilt verwijderen, selecteert u het distributie punt in de Configuration Manager-console en selecteert u vervolgens **verwijderen**.  

Wanneer u een Cloud distributiepunt verwijdert uit een hiërarchie, verwijdert Configuration Manager de inhoud uit de Cloud service in Azure.

Het hand matig verwijderen van onderdelen in azure zorgt ervoor dat het systeem inconsistent is. Deze status blijft zwevende informatie en er kan onverwachte problemen optreden.


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a> Geavanceerde probleem oplossing

Als u diagnostische logboek registratie wilt verzamelen van de Azure-Vm's om problemen met uw Cloud distributiepunt op te lossen, gebruikt u het volgende Power shell-voor beeld om de service diagnostische uitbrei ding voor het abonnement in te scha kelen:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

Het volgende voor beeld is een voorbeeld bestand **Diagnostics. wadcfgx** waarnaar wordt verwezen in de variabele **public_config** in het bovenstaande Power shell-script. Zie [Azure Diagnostics schema voor extensie configuratie](/azure/monitoring-and-diagnostics/azure-diagnostics-schema)voor meer informatie.  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```
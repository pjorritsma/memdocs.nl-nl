---
title: Releaseopmerkingen
titleSuffix: Configuration Manager
description: Meer informatie over urgente problemen die nog niet zijn opgelost in het product of die zijn opgenomen in een Microsoft Ondersteuning Knowledge Base-artikel.
ms.date: 05/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 131b6104d5724c8a4eeb0bb68c4afd9a5319abb7
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823959"
---
# <a name="release-notes-for-configuration-manager"></a>Release opmerkingen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met Configuration Manager zijn de opmerkingen bij de product release beperkt tot urgente problemen. Deze problemen zijn nog niet opgelost in het product of beschreven in een Microsoft Ondersteuning Knowledge Base-artikel.  

Documentatie voor specifieke onderdelen bevat informatie over bekende problemen die van invloed zijn op de kern scenario's.  

Dit artikel bevat opmerkingen bij de release voor de huidige vertakking van Configuration Manager. Voor informatie over de Technical Preview-vertakking raadpleegt u [Technical Preview](../../../get-started/technical-preview.md)  

Raadpleeg de volgende artikelen voor meer informatie over de nieuwe functies die in verschillende versies worden geïntroduceerd:

- [Wat is er nieuw in versie 2002](../../../plan-design/changes/whats-new-in-version-2002.md)
- [Wat is er nieuw in versie 1910](../../../plan-design/changes/whats-new-in-version-1910.md)
- [Wat is er nieuw in versie 1906](../../../plan-design/changes/whats-new-in-version-1906.md)  
- [Wat is er nieuw in versie 1902](../../../plan-design/changes/whats-new-in-version-1902.md)

Zie [what's New in Desktop Analytics](../../../../desktop-analytics/whats-new.md)(Engelstalig) voor meer informatie over de nieuwe functies van bureau blad Analytics.

> [!Tip]  
> Als u een melding wilt ontvangen wanneer deze pagina wordt bijgewerkt, kopieert en plakt u de volgende URL in uw RSS feed-lezer:`https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>Instellen en bijwerken  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>Automatische upgrade van de client gebeurt onmiddellijk voor alle clients

<!-- 6040412 -->

*Van toepassing op versie 1910*

Als uw site gebruikmaakt van [automatische client upgrade](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade), wanneer u de site bijwerkt naar versie 1910, worden alle clients onmiddellijk bijgewerkt nadat de site is bijgewerkt. De enige wille keurige waarde is wanneer clients het beleid ontvangen die standaard elk uur zijn. Voor een grote site met veel clients kan dit gedrag een aanzienlijke hoeveelheid netwerk verkeer en stress-distributie punten verbruiken.

Zie voor meer informatie over betrokken versies [client update voor Configuration Manager current branch versie 1910](https://support.microsoft.com/help/4538166).

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>Configuration. mof wordt niet bijgewerkt door de site server in de passieve modus

<!-- 5787848 -->

*Van toepassing op versie 1910*

Als uw site een [site server in de passieve modus](../configure/site-server-high-availability.md)bevat, verliest u mogelijk inventaris aanpassingen wanneer u de site bijwerkt. De site synchroniseert momenteel niet de configuratie. MOF wanneer u een failover hebt uitgevoerd voor de site servers.

U kunt dit probleem omzeilen door hand matig een back-up te maken en de Configuration. mof van de site te herstellen.

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Waarschuwing voor vereiste installatie van het domein functionaliteits niveau op server 2019

<!-- 4904376 -->

*Van toepassing op versie 1906*

Wanneer u de update voor versie 1906 installeert in een omgeving met domein controllers met Windows Server 2019, wordt de volgende waarschuwing weer gegeven voor de controle van de vereisten voor het functionele domein niveau:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

U kunt dit probleem omzeilen door de waarschuwing te negeren.

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>De synchronisatie van Azure AD-gebruikers detectie en-verzamelings groepen werkt niet na site-uitbrei ding

<!-- 4797313 -->
*Van toepassing op versie 1906*

Nadat u een van de volgende functies hebt geconfigureerd:

- Detectie van gebruikers groepen Azure Active Directory
- Resultaten van verzamelings lidmaatschap synchroniseren met Azure Active Directory groepen

Als u vervolgens een zelfstandige primaire site uitbreidt naar een hiërarchie met een centrale beheer site, ziet u de volgende fout in SMS_AZUREAD_DISCOVERY_AGENT. log:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

U kunt dit probleem omzeilen door de sleutel te vernieuwen die is gekoppeld aan de app-registratie in azure AD. Zie [geheime sleutel vernieuwen](../configure/azure-services-wizard.md#bkmk_renew)voor meer informatie.

## <a name="role-based-administration"></a>Op rollen gebaseerd beheer

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>Beveiligingsbereiken voor bepaalde mappen worden niet gerepliceerd van CA'S naar primaire sites
<!--6306759-->
*Van toepassing op versie 1910*

Na een upgrade naar versie 1910 worden [beveiligingsbereiken voor mappen](../configure/configure-role-based-administration.md#bkmk_config-folder) in gebruikers verzamelingen en verzamelingen niet gerepliceerd van de certificerings instanties naar primaire sites.

## <a name="application-management"></a>Toepassingsbeheer

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>Kan geen certificaat ophalen voor de Power Shell-fout bij het implementeren van micro soft Edge, versie 77 en hoger
<!--5769384-->
*Van toepassing op: Configuration Manager versie 1910*

Als u de Configuration Manager-console uitvoert in een besturings systeem waarbij de taal Zweeds, Hong aars of Japans is, wordt de volgende fout weer gegeven bij de implementatie van micro soft Edge, versie 77 en hoger:

`Unable to get certificate for Powershell`

Deze fout treedt op omdat een `scripts` map niet bestaat in de `AdminConsole\bin` Directory voor Zweedse, Hongaarse of Japanse talen. De map scripts is gelokaliseerd in deze talen van het besturings systeem.

U kunt dit probleem omzeilen door een map te maken `scripts` met de naam in de `AdminConsole\bin` map. Kopieer de bestanden vanuit uw gelokaliseerde map naar de zojuist gemaakte `scripts` map. Implementeer micro soft Edge, versie 77 en hoger zodra de bestanden zijn gekopieerd.

## <a name="os-deployment"></a>Besturingssysteemimplementatie

### <a name="task-sequences-cant-run-over-cmg"></a>Taken reeksen kunnen niet worden uitgevoerd via CMG

*Van toepassing op: Configuration Manager versie 2002*

Er zijn twee exemplaren waarin taken reeksen niet kunnen worden uitgevoerd op een apparaat dat communiceert via een Cloud beheer gateway (CMG):

- U configureert de site voor verbeterde HTTP en het beheer punt is HTTP.<!-- 6358851 -->

    U kunt dit probleem omzeilen door het beheer punt voor HTTPS te configureren.

- U hebt de client geïnstalleerd en geregistreerd met een token voor massa registratie voor verificatie.<!-- 6377921 -->

    Gebruik een van de volgende verificatie methoden om dit probleem te omzeilen:

  - Registreer het apparaat vooraf in het interne netwerk
  - Het apparaat configureren met een certificaat voor client verificatie
  - Het apparaat toevoegen aan Azure AD

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>Nadat de passieve site server is gepromoveerd, hebben de standaard installatie kopie pakketten nog steeds pakket bron op de vorige actieve server

<!--3453224, SCCMDocs-pr issue 3097-->
*Van toepassing op: Configuration Manager versie 1810*

Als u een site server in de passieve modus (Server B) hebt, wordt de locatie van de inhoud van de standaard installatie kopieën naar de vorige actieve server (Server A) gepromoveerd wanneer u deze naar activeert. Als server A een hardwarestoring heeft, kunt u de standaard installatie kopieën niet bijwerken of wijzigen.

Er is geen oplossing voor dit probleem.

## <a name="software-updates"></a>Software-updates

### <a name="security-roles-are-missing-for-phased-deployments"></a>Er ontbreken beveiligings rollen voor gefaseerde implementaties

<!--3479337, SCCMDocs-pr issue 3095-->
*Van toepassing op: Configuration Manager versies 1810, 1902*

Het **besturings systeem Deployment Manager** ingebouwde beveiligingsrol heeft machtigingen voor [gefaseerde implementaties](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md). Deze machtigingen ontbreken voor de volgende rollen:  

- **Toepassingsbeheerder**  
- **Beheerder toepassingsimplementaties**  
- **Software-update beheer**  

De **Auteur** van de app heeft mogelijk enkele machtigingen voor gefaseerde implementaties, maar kan geen implementaties maken.

Een gebruiker met een van deze rollen kan de wizard gefaseerde implementatie starten en kan de gefaseerde implementaties van een toepassing of software-update zien. Ze kunnen de wizard niet volt ooien of wijzigingen aanbrengen in een bestaande implementatie.

U kunt dit probleem omzeilen door een aangepaste beveiligingsrol te maken. Kopieer een bestaande beveiligingsrol en voeg de volgende machtigingen toe aan de klasse van de **gefaseerde implementatie** object:

- Maken  
- Verwijderen  
- Wijzigen  
- Lezen  

Zie [aangepaste beveiligings rollen maken](../configure/configure-role-based-administration.md#BKMK_CreateSecRole) voor meer informatie

## <a name="desktop-analytics"></a>Desktop Analytics

### <a name="an-extended-security-update-for-windows-7-causes-them-to-show-as-unable-to-enroll"></a><a name="dawin7-diagtrack"></a>Een uitgebreide beveiligings update voor Windows 7 geeft aan dat ze niet kunnen worden **Inge schreven**

<!-- 7283186 -->
_Van toepassing op: Configuration Manager versies 1902, 1906, 1910 en 2002_

De uitgebreide beveiligings update van april 2020 (ESU) voor Windows 7 heeft de mini maal vereiste versie van diagtrack. dll gewijzigd van 10586 naar 10240. Door deze wijziging worden Windows 7-apparaten weer gegeven als niet in staat **om in te schrijven** in het dash board **verbindings status** van de bureau blad Analytics. Wanneer u inzoomt op de weer gave apparaat voor deze status, wordt de volgende status weer gegeven in de eigenschap **DiagTrack service configuration** :`Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`

Er is geen tijdelijke oplossing vereist voor dit probleem. Verwijder de ESU van april niet. Als op een andere manier op de juiste wijze is geconfigureerd, rapporteren de Windows 7-apparaten nog steeds diagnostische gegevens naar de Desktop Analytics-service en worden ze nog steeds weer gegeven in de portal.

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>Als u hardware-inventarisatie gebruikt voor gedistribueerde weer gaven, kunt u niet onboarden naar Desktop Analytics

<!-- 4950335 -->
*Van toepassing op: Configuration Manager versie 1902 met update pakket en versie 1906*

Als u een-hiërarchie hebt en de **Hardware-inventarisatie** site gegevens voor [gedistribueerde weer gaven](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) op replicatie koppelingen naar een site inschakelt, wordt de volgende fout weer gegeven in M365UploadWorker. log, nadat u de verbinding met de bureau blad Analytics in Configuration Manager hebt geconfigureerd:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

U kunt dit probleem omzeilen door de **hardware-inventaris** site gegevens voor gedistribueerde weer gaven op elke site replicatie koppeling uit te scha kelen.

### <a name="console-unexpectedly-closes-when-removing-collections"></a>De console wordt onverwacht gesloten wanneer verzamelingen worden verwijderd

<!-- 4749443 -->
*Van toepassing op: Configuration Manager versie 1902 met update pakket*

Nadat u de site hebt verbonden met [Desktop Analytics](../../../../desktop-analytics/connect-configmgr.md), kunt u **specifieke verzamelingen selecteren om te synchroniseren met Desktop Analytics**. Als u een verzameling verwijdert en de wijzigingen toepast, wordt een onverwerkte uitzonde ring veroorzaakt door het onmiddellijk toevoegen van een nieuwe verzameling. De console wordt onverwacht afgesloten.

U kunt dit probleem omzeilen door bij het verwijderen van een verzameling **OK** te selecteren om het venster Eigenschappen te sluiten. Open vervolgens de eigenschappen opnieuw om een nieuwe verzameling toe te voegen op het tabblad **verbinding met bureau blad Analytics** .

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>De tegel status van de pilot bevat enkele apparaten als ' niet gedefinieerd '

<!-- 4547783 -->
*Van toepassing op: Configuration Manager versie 1902 met update pakket*

Wanneer u de Configuration Manager-console gebruikt voor het bewaken van de implementatie status van uw prototype, worden proef apparaten die up-to-date zijn van de doel versie van Windows voor dat implementatie plan weer gegeven als niet- **gedefinieerd** in de tegel status van de pilot.  

Deze niet- **gedefinieerde** apparaten zijn **up-to-date** met de doel versie van het besturings systeem voor dat implementatie plan. Er is geen verdere actie nodig.

## <a name="cloud-services"></a>Cloud services

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>De Azure-service voor de Amerikaanse overheids Cloud laat zien als een open bare Cloud

<!-- 6036748 -->

*Van toepassing op versie 1910*

Als u een verbinding maakt met een Azure-service en de **Azure-omgeving** instelt op de Government Cloud, worden de eigenschappen van de verbinding weer gegeven als de open bare Azure-Cloud. Dit probleem is slechts een weergave probleem in de-console. de service bevindt zich in de Government Cloud. Als u de configuratie wilt bevestigen, voert u de volgende SQL-query uit op de site database:

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

Voor de overheids-Cloud is het resultaat van deze query `2` voor de specifieke Tenant.

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>Kan geen inhoud downloaden van een Cloud beheer gateway die is ingeschakeld voor TLS 1,2

<!-- 5771680 -->

*Van toepassing op versie 1906, 1910 vroege update ring*

Als u een CMG (Cloud Management Gateway) inschakelt om **als een Cloud distributiepunt te functioneren en inhoud van Azure Storage te leveren** en **TLS 1,2**af te dwingen, kunnen de inhoud niet worden gedownload.

De volgende fouten worden weer gegeven in de bestand datatransferservice. log op de client:

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

De volgende fouten worden weer gegeven in CMGContentService. log op de server:

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

Dit probleem omzeilen:

- Werk de site bij naar de wereld wijd beschik bare versie van 1910, uitgebracht op 20 december 2019. (Als u eerder hebt bijgewerkt naar de 1910 vroege update ring, moet u deze build bijwerken wanneer deze beschikbaar is.)

- U kunt ook een traditioneel [Cloud distributiepunt](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)gebruiken. Deze rol dwingt geen TLS 1,2 af, maar is compatibel met clients waarvoor TLS 1,2 vereist is.

## <a name="protection"></a>Protection

### <a name="bitlocker-management-appears-in-version-1906"></a>BitLocker-beheer wordt weer gegeven in versie 1906

*Van toepassing op versie 1906*

<!-- 5984688 -->

Na 21 november 2019, als u updatet naar versie 1906 van versie 1902 of eerder, wordt de functie voor het beheren van BitLocker ingeschakeld en beschikbaar. Deze functie is een optioneel onderdeel dat begint bij versie 1910. Het wordt niet ondersteund in versie 1906. Als u het probeert te gebruiken in versie 1906, kunnen er onverwachte resultaten optreden. Als u de functie niet gebruikt, is er geen impact.

Als u de [functie BitLocker-beheer](../../../../protect/plan-design/bitlocker-management.md)wilt gebruiken, moet u bijwerken naar versie 1910.

<!--
## Backup and recovery

## Client deployment and upgrade
-->

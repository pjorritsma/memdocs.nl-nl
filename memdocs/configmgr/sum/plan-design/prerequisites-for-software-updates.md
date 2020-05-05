---
title: Vereisten voor software-updates
titleSuffix: Configuration Manager
description: Meer informatie over vereisten voor software-updates in Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 138ff268f42dae1c15e11b34c92e6c7a3044705b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078444"
---
# <a name="prerequisites-for-software-updates-in-configuration-manager"></a>Vereisten voor software-updates in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u de vereisten voor software-updates in Configuration Manager. Voor elk van de vereisten worden de externe afhankelijkheden en interne afhankelijkheden in afzonderlijke tabellen vermeld.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Afhankelijkheden van software-updates die extern zijn Configuration Manager  
 De volgende secties bevatten een lijst met de externe afhankelijkheden voor software-updates.  

### <a name="internet-information-services"></a>Internet Information Services  
 Internet Information Services (IIS) moet zijn geïnstalleerd op de site systeem servers om het software-update punt, het beheer punt en het distributie punt uit te voeren. Zie [vereisten voor site systeem rollen](../../core/plan-design/configs/site-and-site-system-prerequisites.md)voor meer informatie.  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Windows Server Update Services (WSUS) is vereist voor de synchronisatie van software-updates en voor het controleren van toepasselijkheid van software-updates op clients. De WSUS-server moet zijn geïnstalleerd voordat u de rol van het software-update punt maakt. De volgende versies van WSUS worden ondersteund voor een software-update punt:  

- WSUS-10.0.14393 (rol in Windows Server 2016)
- WSUS-10.0.17763 (rol in Windows Server 2019) (hiervoor is Configuration Manager 1810 of hoger vereist)
- WSUS 6,2 en 6,3 (rol in Windows Server 2012 en Windows Server 2012 R2)
  - Er zijn [kb 3095113 en kb 3159706 (of een equivalente update)](#BKMK_wsus2012) nodig voor WSUS 6,2 en 6,3 als u Windows 10-upgrades implementeert.

> [!NOTE]
> - Wanneer u meerdere software-update punten op een site hebt, moet u ervoor zorgen dat ze allemaal dezelfde versie van WSUS uitvoeren.

### <a name="wsus-administration-console"></a>WSUS-beheerconsole  
De WSUS-beheer console is vereist op de Configuration Manager-site server wanneer het software-update punt zich op een externe site systeem server bevindt en WSUS niet al op de site server is geïnstalleerd.  

> [!IMPORTANT]  
> - De WSUS-versie op de site server moet hetzelfde zijn als de WSUS-versie die wordt uitgevoerd op de software-update punten.
> - Gebruik niet de WSUS-beheer console om WSUS-instellingen te configureren. Configuration Manager maakt verbinding met het exemplaar van WSUS dat wordt uitgevoerd op het software-update punt en configureert de toepasselijke instellingen.  


### <a name="windows-update-agent"></a>Windows Update-agent  
 De WUA-client (Windows Update Agent) is vereist op clients, zodat ze verbinding kunnen maken met de WSUS-server. WUA haalt de lijst met software-updates op die moeten worden gescand op naleving.  

 Wanneer u Configuration Manager installeert, wordt de meest recente versie van WUA gedownload. Wanneer u vervolgens de Configuration Manager-client installeert, wordt WUA indien nodig bijgewerkt. Als de installatie mislukt, moet u een andere methode gebruiken om WUA te upgraden.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Afhankelijkheden van software-updates die intern zijn voor Configuration Manager  
 De volgende secties bevatten een overzicht van de interne afhankelijkheden voor software-updates in Configuration Manager.  

### <a name="management-points"></a>Beheer punten  
 Beheer punten wisselen gegevens over tussen client computers en de Configuration Manager-site. De beheer punten zijn vereist voor software-updates.  

### <a name="software-update-points"></a>Software-update punten  
 U moet een software-update punt op de WSUS-server installeren om software-updates te implementeren in Configuration Manager. Zie [een software-update punt installeren en configureren](../get-started/install-a-software-update-point.md)voor meer informatie.

### <a name="distribution-points"></a>Distributiepunten  
 Distributie punten zijn vereist voor het opslaan van de inhoud voor software-updates. Zie [inhoud en infra structuur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)voor inhoud beheren voor meer informatie over het installeren van distributie punten en het beheren van inhoud.  

### <a name="client-settings-for-software-updates"></a>Clientinstellingen voor software-updates  
Software-updates zijn standaard ingeschakeld voor clients. Er zijn andere beschik bare instellingen die bepalen hoe en wanneer clients naleving voor de software-updates beoordelen en bepalen hoe de software-updates worden geïnstalleerd.  

 Raadpleeg voor meer informatie de volgende artikelen:  

- [Clientinstellingen voor software-updates](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [Client instellingen voor software-updates](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Reporting Services-punten  
 De sitesysteemrol Reporting Services kan rapporten voor software-updates weergeven. Deze rol is optioneel, maar wordt aanbevolen. Zie [Configuring Reporting](../../core/servers/manage/configuring-reporting.md)(Engelstalig configureren) voor meer informatie over het maken van een Reporting Services-punt.  

## <a name="which-updates-are-required-on-wsus-62-and-63"></a><a name="BKMK_wsus2012"></a>Welke updates zijn vereist voor WSUS 6,2 en 6,3?

Er zijn twee updates vereist voor het synchroniseren van de classificatie van **upgrades** in WSUS 6,2 en 6,3. Af en toe ziet u mogelijk een fout bij het downloaden of implementeren van upgrades als ze zijn gesynchroniseerd voordat KB3095113 en KB3159706 werden geïnstalleerd. Informatie over mogelijke problemen vindt u in de volgende sectie.  

- U moet [KB 3095113](https://support.microsoft.com/kb/3095113)installeren, uitgebracht in oktober 2015, op uw software-update punten en site servers voordat u de classificatie **upgrades** synchroniseert.
  - Met deze update wordt de classificatie **upgrades** ingeschakeld.
- Voor de service Windows 10 versie 1607 en hoger moet u [KB 3159706](https://support.microsoft.com/en-us/help/3159706)installeren en configureren. KB 3159706 is uitgebracht in mei 2016.
  - Met deze update kunt u de bestanden die worden gebruikt voor het upgraden van Windows 10 versie 1607 en hoger, in WSUS systeem eigen decoderen.

>[!IMPORTANT]
> Zowel KB 3095113 als KB 3159706 zijn opgenomen in de **Security Monthly Total Rollup** , te beginnen in juli 2017. Dit betekent dat u KB 3095113 en KB 3159706 mogelijk niet ziet als geïnstalleerde updates, omdat deze mogelijk zijn geïnstalleerd met een Rollup. Als u echter een van deze updates nodig hebt, raden we u aan om een beveiligings update van een **maand van maandelijkse kwaliteit** uit te voeren na oktober 2017, omdat ze een extra updates voor WSUS bevatten om het geheugen gebruik op de CLIENTWEBSERVICE van WSUS te verlagen.

## <a name="download-of-windows-10-upgrades-fails-with-error-invalid-certificate-signature-or-0xc1800118"></a><a name="BKMK_RecoverUpgrades"></a>Het downloaden van upgrades van Windows 10 mislukt met ' fout: ongeldige certificaat handtekening ' of 0xc1800118

De updates en problemen die in deze sectie worden beschreven, zijn alleen van toepassing op WSUS die wordt uitgevoerd op Windows Server 2012-of Windows Server 2012 R2-machines (WSUS 6,2 en 6,3). Normaal gesp roken ziet u alleen de problemen die worden beschreven in deze sectie als u WSUS vóór juli 2017 hebt geïnstalleerd en onlangs de classificatie **upgrades** hebt ingeschakeld. Het is echter mogelijk dat deze problemen ook in andere situaties worden weer geven.

### <a name="historical-information-about-kb-3095113"></a>Historische informatie over KB 3095113

 [KB 3095113](https://support.microsoft.com/kb/3095113) is in oktober 2015 [uitgebracht als een hotfix](https://blogs.technet.microsoft.com/wsus/2015/12/03/important-update-for-wsus-4-0-kb-3095113/) voor het toevoegen van ondersteuning voor Windows 10-upgrades naar WSUS. Met de update kan WSUS updates synchroniseren en distribueren in de classificatie **upgrades** voor Windows 10.

Als u upgrades synchroniseert zonder eerst [KB 3095113](https://support.microsoft.com/kb/3095113)te installeren, vult u de WSUS-data base (SUSDB) in met niet-bruikbare gegevens. Deze gegevens moeten worden gewist voordat de upgrades op de juiste wijze kunnen worden geïmplementeerd. Windows 10-upgrades in deze status kunnen niet worden gedownload met behulp van de wizard software-updates downloaden.

Op de pagina voltooiing van de wizard software-updates downloaden worden fouten weer gegeven die er ongeveer als volgt uitzien:

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

Daarnaast worden in het bestand PatchDownloader. log fouten weer gegeven die vergelijkbaar zijn met de volgende:

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

Als deze fouten zijn opgetreden, worden ze opgelost door een gewijzigde versie van de [oplossings stappen voor WSUS](https://blogs.technet.microsoft.com/wsus/2016/01/29/how-to-delete-upgrades-in-wsus/)uit te voeren. Omdat deze stappen vergelijkbaar zijn met de oplossing voor het niet uitvoeren van de hand matige stappen die vereist zijn na de installatie van KB 3159706, hebben we beide sets stappen gecombineerd tot één oplossing in de volgende sectie:

- [U kunt de synchronisatie van de upgrades herstellen voordat u KB 3095113 of kb 3159706 installeert](#bkmk_fix-upgrades).

### <a name="historical-information-about-kb-3159706"></a>Historische informatie over KB 3159706

KB 3148812 is in eerste instantie uitgebracht in april 2016 zodat WSUS de. esd-bestanden die worden gebruikt voor het upgraden van Windows 10-pakketten systeem eigen kunnen ontsleutelen. [Kb 3148812 heeft problemen voor sommige klanten veroorzaakt](https://blogs.technet.microsoft.com/wsus/2016/05/05/the-long-term-fix-for-kb3148812-issues/) en is vervangen door [KB 3159706](https://support.microsoft.com/en-us/help/3159706). KB 3159706 moet worden geïnstalleerd op alle software-update punten en site servers voordat u Windows 10-versie 1607 en hoger kunt onderhouden. Er kunnen echter problemen optreden als u de KB niet wilt realiseren, moeten de volgende hand matige stappen na de installatie:

1. Vanaf een opdracht prompt met verhoogde bevoegdheid `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`.
1. Start de WSUS-service opnieuw op alle WSUS-servers.

Als u niet beseft dat KB 3159706 hand matige stappen heeft na de installatie, of als u een synchronisatie hebt uitgevoerd in de upgrade voor Windows 10 1607 vóór de installatie van KB 3159706, worden er problemen ondervonden met het maken van verbinding met de WSUS-console en de implementatie van de upgrade respectievelijk. Wanneer een client het upgrade bestand heeft gedownload, wordt er een [ **0xC1800118** -fout code](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus)weer geven.

Omdat de oplossings stappen vergelijkbaar zijn met de oplossing voor het synchroniseren van upgrades vóór KB 3095113-installatie, hebben we beide sets stappen gecombineerd tot één oplossing in de volgende sectie.
 

### <a name="to-recover-from-synchronizing-the-upgrades-before-you-install-kb-3095113-or-kb-3159706"></a><a name="bkmk_fix-upgrades"></a>U kunt de synchronisatie van de upgrades herstellen voordat u KB 3095113 of KB 3159706 installeert

Volg de onderstaande stappen om zowel de 0xc1800118-fout als ' fout: ongeldige certificaat handtekening ' op te lossen:

1. Schakel de classificatie **upgrades** uit in zowel WSUS als Configuration Manager. U wilt niet dat er een synchronisatie wordt uitgevoerd totdat u door deze instructies bent geleid.  
   - Schakel de classificatie **upgrades** uit in de eigenschappen van de software-update punt component op de site op het hoogste niveau.
     - Zie [classificaties en producten configureren](../get-started/configure-classifications-and-products.md)voor meer informatie.
   - Schakel de classificatie **upgrades** van WSUS onder **producten en classificaties** uit op de [pagina **Opties** ](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations)of gebruik de Power shell-ISE die als Administrator wordt uitgevoerd.
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq "Upgrades"} | Set-WsusClassification -Disable
      ```  
     - Als u de WSUS-data base tussen meerdere WSUS-servers deelt, hoeft u de **upgrade** voor elke Data Base slechts één keer uit te checken.  
1. Voer op elke WSUS-server een opdracht prompt met verhoogde bevoegdheden uit `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`:. Start vervolgens de WSUS-service opnieuw op alle WSUS-servers.
   -  WSUS plaatst de data base in de [modus voor één gebruiker](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode) voordat wordt gecontroleerd of er onderhoud nodig is. De service wordt uitgevoerd of wordt niet uitgevoerd op basis van de resultaten van de controle. Vervolgens wordt de Data Base weer in de modus voor meerdere gebruikers geplaatst. 
   - Als u de WSUS-data base tussen meerdere WSUS-servers deelt, hoeft u dit niet één keer te doen voor elke Data Base.
1. Verwijder alle Windows 10-upgrades van elke WSUS-data base met behulp van de Power shell-ISE die wordt uitgevoerd als Administrator.
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. Verwijder bestanden uit de tabel tbFile uit de WSUS-data bases die worden gebruikt door uw software-update punten. Voer in de WSUS-data base de volgende opdrachten uit SQL Server Management Studio:
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. Start de synchronisatie van software-updates op de site op het hoogste niveau in Configuration Manager en wacht totdat deze is voltooid. Een volledige synchronisatie wordt uitgevoerd omdat er een wijziging is aangebracht in de classificaties Configuration Manager toen we **upgrades**hebben verwijderd. (Zie [software-updates synchroniseren](../get-started/synchronize-software-updates.md)voor meer informatie.
1. Selecteer de classificatie **upgrades** in de eigenschappen van de software-update punt component. Start vervolgens een andere synchronisatie van software-updates om de **upgrades** terug te brengen naar WSUS en Configuration Manager. U hoeft de classificatie **upgrades** niet in te scha kelen omdat Configuration Manager deze voor u doet.
1. Als de-clients de **0xC1800118** -fout code hebben ontvangen tijdens het downloaden van een upgrade, moet u het gegevens archief verwijderen dat wordt gebruikt door de Windows Update-Agent. Mogelijk moet u ook de verborgen map ~ BT op het apparaat verwijderen. De volgende keer dat de client scant, is dit een volledige scan voor de WSUS-server in plaats van een Delta. U kunt een Power shell-script gebruiken dat vergelijkbaar is met het volgende voorbeeld script:  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>Volgende stappen
[Beheer van software-updates voorbereiden](../get-started/prepare-for-software-updates-management.md)

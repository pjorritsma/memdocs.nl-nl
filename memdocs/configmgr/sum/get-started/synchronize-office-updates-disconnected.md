---
title: Updates van Microsoft 365-apps zonder Internet verbinding synchroniseren
titleSuffix: Configuration Manager
description: Updates van Microsoft 365 apps synchroniseren op het software-update punt op het hoogste niveau dat niet is verbonden met internet.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 4739703436d7feec7c4c899e60b33d38ce28babf
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125726"
---
# <a name="synchronize-microsoft-365-apps-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a>Updates van Microsoft 365-apps synchroniseren vanaf een niet-verbonden software-update punt

*Van toepassing op: Configuration Manager (huidige vertakking)*
<!--4065163-->
Vanaf Configuration Manager versie 2002 kunt u een hulp programma gebruiken om Microsoft 365 apps-updates te importeren van een met internet verbonden WSUS-server naar een niet-verbonden Configuration Manager omgeving. Als u eerder meta gegevens voor software die is bijgewerkt in omgevingen zonder verbinding hebt geëxporteerd en geïmporteerd, kunt u geen updates voor Microsoft 365 Apps implementeren. Voor updates van Microsoft 365-apps zijn aanvullende meta gegevens vereist die zijn gedownload van een Office-API en het Office CDN, wat niet mogelijk is met niet-verbonden omgevingen.

> [!Note]
> Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Zie [name wijzigen voor Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change)voor meer informatie. Mogelijk ziet u nog steeds verwijzingen naar de oude naam in de Configuration Manager-console en de ondersteunende documentatie terwijl de-console wordt bijgewerkt.

## <a name="prerequisites"></a>Vereisten

- Een met internet verbonden WSUS-server met mini maal Windows Server 2012.
- De WSUS-server moet verbinding hebben met deze twee Internet eindpunten:
   - `officecdn.microsoft.com`
   - `config.office.com`
- Kopieer het hulp programma OfflineUpdateExporter en de afhankelijkheden ervan naar het Internet Connected WSUS-server.
  - Het hulp programma en de bijbehorende afhankelijkheden bevinden zich in de ** &lt; ConfigMgrInstallDir>/tools/offlineupdateexporter** -map.
- De gebruiker die het hulp programma uitvoert, moet deel uitmaken van de groep **WSUS-Administrators** .
- De map die is gemaakt om de Microsoft 365-apps op te slaan meta gegevens en inhoud moeten de juiste toegangs beheer lijsten (Acl's) hebben om de bestanden te beveiligen.
    - Deze map moet ook leeg zijn.
- Gegevens die van de online-WSUS-server naar de niet-verbonden omgeving worden verplaatst, moeten veilig worden verplaatst.

> [!IMPORTANT]
> Inhoud wordt gedownload voor alle talen van Microsoft 365-apps. Elke update kan ongeveer 10 GB aan inhoud hebben.

## <a name="synchronize-then-decline-unneeded-microsoft-365-apps-updates"></a>Synchroniseren en vervolgens niet-vereiste updates van Microsoft 365 apps weigeren

1. Open de WSUS-console op uw Internet verbinding met WSUS.
1. Selecteer **Opties** en vervolgens op **producten en classificaties**.
1. Op het tabblad **producten** selecteert u **Office 365-client** en selecteert u **updates** op het tabblad **classificaties** . [ ![ producten en classificaties voor updates van Microsoft 365-apps in WSUS](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. Ga naar **synchronisaties** en selecteer **Nu synchroniseren** om de Microsoft 365 apps-updates in WSUS op te halen.
1. Wanneer de synchronisatie is voltooid, moet u de updates van Microsoft 365-apps die u niet wilt implementeren met Configuration Manager weigeren. U hoeft geen updates van Microsoft 365 apps goed te keuren om ze te kunnen downloaden.  
   - Als u ongewenste Microsoft 365 Apps verwijdert in WSUS, worden deze niet gestopt tijdens het exporteren van een WsusUtil.exe, maar wordt de inhoud niet meer gedownload door het hulp programma OfflineUpdateExporter.
   - Het hulp programma OfflineUpdateExporter het downloaden van updates voor de Microsoft 365-apps. Andere producten moeten nog steeds worden goedgekeurd om te worden gedownload als u updates voor hen wilt exporteren.
    - Maak een [nieuwe update weergave in WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus) om onnodige updates van Microsoft 365-apps in WSUS te bekijken en af te wijzen.
1. Als u andere product updates wilt goed keuren voor downloaden en exporteren, wacht u totdat de inhoud is gedownload voordat u de inhoud van de map WSUSContent exporteert WsusUtil.exe exporteren en kopiëren. Zie [software-updates synchroniseren vanaf een niet-verbonden software-update punt](synchronize-software-updates-disconnected.md) voor meer informatie

## <a name="exporting-the-microsoft-365-apps-updates"></a>De updates van de Microsoft 365-apps exporteren

1. Kopieer de map OfflineUpdateExporter van Configuration Manager naar het Internet Connected WSUS-server.
    - Het hulp programma en de bijbehorende afhankelijkheden bevinden zich in de ** &lt; ConfigMgrInstallDir>/tools/offlineupdateexporter** -map.
1. Voer het hulp programma uit vanaf een opdracht prompt op het Internet Connected WSUS-server met het volgende gebruik: **OfflineUpdateExporter.exe-O-D &lt; doelpad>**

   |OfflineUpdateExporter-para meter|Beschrijving|
   |---|---|
   |**-O**|  **-Office**. Hiermee wordt het product opgegeven voor het exporteren van updates is Office 365-of Microsoft 365-apps|
   |**-D**|**-Bestemming**. Doel is een vereiste para meter en het volledige pad naar de doelmap is nodig.|

   - Het hulp programma **OfflineUpdateExporter** voert de volgende handelingen uit:
      - Maakt verbinding met WSUS
      - Hiermee worden de meta gegevens van de Microsoft 365-apps in WSUS gelezen
      - Downloadt de inhoud en eventuele aanvullende meta gegevens die nodig zijn voor de updates van de Microsoft 365-apps naar de doelmap

1. Ga via de opdracht prompt op het Internet Connected WSUS-server naar de map met WsusUtil.exe. Het hulp programma bevindt zich standaard in%*Program Files*% \ update Services\Tools. Als het hulpprogramma zich op de standaardlocatie bevindt, typ dan bijvoorbeeld **cd %ProgramFiles%\Update Services\Tools**.
   - Als u Windows Server 2012 gebruikt, moet u ervoor zorgen dat [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) is geïnstalleerd op de WSUS-servers.
   - De gebruiker die het WsusUtil-hulp programma uitvoert, moet lid zijn van de lokale groep Administrators op de server.

1. Typ het volgende om de meta gegevens van software-updates te exporteren naar een GZIP-bestand:  

    **WsusUtil.exe***bestand* voor het exporteren van*pakketnaam*      

    Bijvoorbeeld:  

    **WsusUtil.exe exporteren export.xml. gz exporteren. log**

1. Kopieer het bestand **export.xml. gz** naar de WSUS-server op het hoogste niveau op het niet-verbonden netwerk.
1. Als u updates voor andere producten hebt goedgekeurd, kopieert u de inhoud van de map WSUSContent naar de map WSUSContent van de niet-verbonden WSUS-server.
1. Kopieer de doelmap die wordt gebruikt voor de **OfflineUpdateExporter** naar het hoogste niveau Configuration Manager site server op het niet-verbonden netwerk.

## <a name="import-the-microsoft-365-apps-updates"></a>De updates van de Microsoft 365-apps importeren

1. Importeer op de niet-verbonden WSUS-server op het hoogste niveau de meta gegevens van de update uit de **export.xml. gz** die u hebt gegenereerd op de met internet verbonden WSUS-server.
   
    Bijvoorbeeld:  

    **WsusUtil.exe importeren export.xml. gz import. log**
    
    Het WsusUtil.exe-hulp programma bevindt zich standaard in%*Program Files*% \ update Services\Tools.

1. Zodra het importeren is voltooid, moet u een eigenschap site besturings element configureren op de niet-verbonden Configuration Manager site server op het hoogste niveau. Deze configuratie wijziging wijst Configuration Manager de inhoud voor Microsoft 365-apps. De configuratie van de eigenschap wijzigen:
   1. Kopieer het [Power shell-script O365OflBaseUrlConfigured](#bkmk_o365_script) naar de niet-verbonden Configuration Manager site server op het hoogste niveau.
   1. Ga `"D:\Office365updates\content"` naar het volledige pad van de gekopieerde map met de inhoud van de Microsoft 365 apps en de meta gegevens die zijn gegenereerd door OfflineUpdateExporter.
      > [!IMPORTANT]
      > Alleen lokale paden werken voor de eigenschap O365OflBaseUrlConfigured.
   1. Sla het script op als`O365OflBaseUrlConfigured.ps1`
   1. Voer vanuit een Power shell-venster met verhoogde bevoegdheden uit op de niet-verbonden Configuration Manager site server op het hoogste niveau `.\O365OflBaseUrlConfigured.ps1` .
   1. Start de **SMS_Executive** -service opnieuw op de site server.
1. Ga in de **Configuration Manager** -console naar **beheer**  >  **site configuratie**  >  **sites**.
1. Klik met de rechter muisknop op de site op het hoogste niveau en selecteer vervolgens **site onderdelen configureren**  >  **Software-update punt**.
1. Selecteer *updates*op het tabblad **classificaties** . Op het tabblad **Products** selecteert u *Office 365 client*.
1. [Software-updates synchroniseren](synchronize-software-updates.md#manually-start-software-updates-synchronization) voor Configuration Manager
1. Wanneer de synchronisatie is voltooid, gebruikt u uw normale proces voor het implementeren van updates van Microsoft 365-apps.

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a>Proxy configuratie

- Proxy configuratie is niet ingebouwd in het hulp programma. Als proxy is ingesteld in de Internet opties op de server waarop het hulp programma wordt uitgevoerd, wordt dit in theorie gebruikt en moet het goed functioneren.
   - Voer vanaf een opdracht prompt uit `netsh winhttp show proxy` om de geconfigureerde proxy weer te geven.



## <a name="modify-o365oflbaseurlconfigured-property"></a><a name="bkmk_o365_script"></a>Eigenschap O365OflBaseUrlConfigured wijzigen

```powershell
# Name: O365OflBaseUrlConfigured.ps1
#
# Description: This sample sets the O365OflBaseUrlConfigured property for the SMS_WSUS_CONFIGURATION_MANAGER component on the top-level site.
# This script must be run on the disconnected top-level Configuration Manager site server
#
# Replace "D:\Office365updates\content" with the full path to the copied directory containing all the Office metadata and content generated by the OfflineUpdateExporter tool.
# Only local paths work for the O365OflBaseUrlConfigured property.

$PropertyValue = "D:\Office365updates\content"

# Don't change any of the lines below
$PropertyName = "O365OflBaseUrlConfigured"

# Get provider instance
$providerMachine = Get-WmiObject -namespace "root\sms" -class "SMS_ProviderLocation"

if($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = gwmi -ComputerName $providerMachine.Machine -namespace root\sms\site_$SiteCode -query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_WSUS_CONFIGURATION_MANAGER"'
$properties = $component.props

Write-host "Updating $PropertyName property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -eq $PropertyName) 
  {
    Write-host "Current value for $PropertyName is $($property.value2)"
    $property.value2 = $PropertyValue
    Write-host "Updating value for $PropertyName to $($property.value2)"
    break
  }
}

$component.props = $properties
$component.put()
```

## <a name="next-steps"></a>Volgende stappen

[Software-updates toevoegen aan een updategroep](../deploy-use/add-software-updates-to-an-update-group.md)
---
title: Problemen met Win32-apps in Microsoft Intune oplossen
titleSuffix: ''
description: Meer informatie over de meest voorkomende methoden voor het oplossen van problemen met Win32-apps in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bbdc929f5d3a9703f3d299b8e3a68dd624c450c2
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083910"
---
# <a name="troubleshoot-win32-app-issues"></a>Problemen met Win32-apps oplossen

Bij het oplossen van problemen met Win32-apps die worden gebruikt in Microsoft Intune, kunt u een aantal methoden gebruiken. Dit artikel bevat probleemoplossingsinformatie en informatie om u te helpen bij het oplossen van problemen met Win32-apps. Zie [Problemen met de installatie van Win32-apps oplossen](troubleshoot-app-install.md#win32-app-installation-troubleshooting) voor meer informatie.

> [!NOTE]
> Deze app-beheermogelijkheid biedt ondersteuning voor zowel 32- als 64-bits besturingssysteemarchitecturen voor Windows-toepassingen.

> [!IMPORTANT]
> Wanneer u Win32-apps implementeert, kunt u de [Intune-beheeruitbreiding](../apps/intune-management-extension.md) exclusief gebruiken, met name wanneer u een Win32-app-installatieprogramma voor meerdere bestanden hebt. Als u de installatie van Win32-apps en LOB-apps (Line-Of-Business) tijdens de Autopilot-registratie combineert, is het mogelijk dat de installatie van de app mislukt. De Intune-beheeruitbreiding wordt altijd automatisch geïnstalleerd wanneer een PowerShell-script of Win32-app wordt toegewezen aan de gebruiker of het apparaat.

## <a name="app-troubleshooting-details"></a>Details van de app-probleemoplossing

U kunt installatieproblemen bekijken, zoals wanneer de app was gemaakt, bewerkt, ingericht op en geleverd aan een apparaat. In het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) vindt u deze en andere informatie in het deelvenster **Probleemoplossing en ondersteuning**. Zie [Details van de app-probleemoplossing](troubleshoot-app-install.md#app-troubleshooting-details) voor meer informatie.

## <a name="troubleshooting-app-issues-by-using-logs"></a>Problemen met apps oplossen met behulp van logboeken

Door de details van logboeken te bekijken, kunt u de oorzaak van de problemen die u ervaart, vaststellen en oplossen. U kunt ervoor kiezen om de logboeken te bekijken [die worden weergegeven in Intune](apps-win32-troubleshoot.md#logs-displayed-in-intune) of de [die worden weergegeven via CMTrace](apps-win32-troubleshoot.md#logs-displayed-through-cmtrace). 

### <a name="logs-displayed-in-intune"></a>Logboeken weergegeven in Intune

Als er een installatieprobleem optreedt met een Win32-app, kunt u in Intune de optie **Logboeken verzamelen** kiezen in het deelvenster **Installatiegegevens** voor de app. Voor meer informatie raadpleegt u [Problemen met de installatie van Win32-app oplossen](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

### <a name="logs-displayed-through-cmtrace"></a>Logboeken weergegeven via CMTrace

Agent-logboeken op de clientcomputer bevinden zich meestal in *C:\ProgramData\Microsoft\IntuneManagementExtension\Logs*. U kunt *CMTrace.exe* gebruiken om deze logboekbestanden te bekijken. Zie [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace) voor meer informatie.

![Schermopname van de agentlogboeken op de clientcomputer.](./media/apps-win32-app-management/apps-win32-app-10.png)

> [!IMPORTANT]
> Als u wilt toestaan dat LOB Win32-apps goed worden geïnstalleerd en uitgevoerd, moeten via de antimalware-instellingen worden ingesteld dat de volgende mappen niet worden gescand:<p>
> **Voor X64-clientcomputers**:<br>
> *C:\Program Files (x86)\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>  
> **Voor X86-clientcomputers**:<br>
> *C:\Program Files\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>
> Zie [Virusscanaanbevelingen voor enterprise computers waarop momenteel ondersteunde versies van Windows worden uitgevoerd](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers) voor meer informatie.

## <a name="detecting-the-win32-app-file-version-by-using-powershell"></a>De bestandsversie van de Win32-app detecteren met behulp van PowerShell

Als u problemen ondervindt bij het detecteren van de bestandsversie van de Win32-app, kunt u de volgende PowerShell-opdracht gebruiken of aanpassen:

``` PowerShell

$FileVersion = [System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion
#The below line trims the spaces before and after the version name
$FileVersion = $FileVersion.Trim();
if ("<file version of successfully detected file>" -eq $FileVersion)
{
#Write the version to STDOUT by default
$FileVersion
exit 0
}
else
{
#Exit with non-zero failure code
exit 1
}
```

Vervang in de voorgaande PowerShell-opdracht de tekenreeks `<path to binary file>` door het pad naar uw Win32-app-bestand. Een voorbeeld van een pad ziet er als volgt uit:

`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

Vervang ook de tekenreeks `<file version of successfully detected file>` door de bestandsversie die u moet detecteren. Een voorbeeld van een tekenreeks voor een bestandsversie ziet er als volgt uit:

`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

Als u de versiegegevens van uw Win32-app moet ophalen, kunt u de volgende PowerShell-opdracht gebruiken:

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

Vervang in de voorgaande PowerShell-opdracht `<path to binary file>` door het bestandspad.

## <a name="additional-troubleshooting-areas-to-consider"></a>Aanvullende gebieden voor probleemoplossing die u kunt overwegen
- Controleer het doel om na te gaan of de agent op het apparaat is geïnstalleerd. Een Win32-app die is gericht op een groep of een PowerShell-script dat is gericht op een groep maakt een agent-installatiebeleid voor een beveiligingsgroep.
- Controleer de versie van het besturingssysteem: Windows 10 1607 en hoger.  
- Controleer de Windows 10-SKU. Windows 10 S en Windows-versies met de S-modus ingeschakeld bieden geen ondersteuning voor MSI-installatie.

Zie [Problemen met de installatie van Win32-apps oplossen](troubleshoot-app-install.md#win32-app-installation-troubleshooting) voor meer informatie over het oplossen van problemen met Win32-apps. Zie [App types supported on ARM64 device](../apps/troubleshoot-app-install.md#app-types-supported-on-arm64-devices) (Typen apps die worden ondersteund op ARM64-apparaten) voor meer informatie over app-typen op ARM64-apparaten.

## <a name="next-steps"></a>Volgende stappen

- [Problemen met app-installatie oplossen](troubleshoot-app-install.md)

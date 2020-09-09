---
title: Een familienaam van een pakket (PFN) zoeken voor VPN per app
titleSuffix: Configuration Manager
description: Meer informatie over de twee manieren om de naam van een pakket familie te vinden, zodat u een VPN per app kunt configureren.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 357b13b06bcfaabf6c22f68a3c21e498630cebf2
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608214"
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Een familienaam van een pakket (PFN) zoeken voor VPN per app

*Van toepassing op: Configuration Manager (huidige vertakking)*


Er zijn twee manieren om een PFN te zoeken, zodat u VPN per app kunt configureren.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Een PFN zoeken voor een app die is geïnstalleerd op een Windows 10-computer

Als de app waarmee u werkt, al is geïnstalleerd op een Windows 10-computer, kunt u de PowerShell-cmdlet [Get-AppxPackage](/powershell/module/appx/get-appxpackage) gebruiken om de PFN op te halen.

De syntaxis voor Get-AppxPackage is:

``` Syntax
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> Mogelijk moet u Power shell uitvoeren als een beheerder om de PFN op te halen.

Als u bijvoorbeeld informatie wilt ophalen over alle universele apps die op uw computer zijn geïnstalleerd, gebruikt u `Get-AppxPackage`.

Voor informatie over een app waarvan u de naam of een deel van de naam weet, gebruikt u `Get-AppxPackage *<app_name>`. Als u niet zeker weet wat de volledige naam van de app is, kunt u het jokerteken gebruiken. Als u bijvoorbeeld informatie voor OneNote wilt ophalen, gebruikt u `Get-AppxPackage *OneNote`.


Hier vindt u de informatie die is opgehaald voor OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Een PFN zoeken als de niet op een computer is geïnstalleerd

1. Ga naar https://www.microsoft.com/store/apps
2. Typ de naam van de app in de zoekbalk. In het voorbeeld wordt gezocht naar OneNote.
3. Klik op de koppeling naar de app. De URL die u opent heeft een reeks letters aan het eind. In ons voor beeld ziet de URL er als volgt uit: `https://www.microsoft.com/store/apps/onenote/9wzdncrfhvjl`
4. Plak op een ander tabblad de volgende URL, `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata` , vervangen `<app id>` door de app-id die u hebt verkregen met behulp van de https://www.microsoft.com/store/apps reeks letters aan het eind van de URL in stap 3. In het voorbeeld voor OneNote plakt u het volgende: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

In Microsoft Edge wordt de gewenste informatie weergegeven. In Internet Explorer klikt u op **Openen** om de informatie weer te geven. De PFN-waarde wordt weergegeven op de eerste regel. De resultaten voor het voorbeeld zien er als volgt uit:

``` JSON
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
```
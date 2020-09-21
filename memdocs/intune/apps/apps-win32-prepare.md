---
title: Een Win32-app voorbereiden om te worden geüpload naar Microsoft Intune
titleSuffix: ''
description: Meer informatie over het voorbereiden van een Win32-app die moet worden geüpload naar Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 94626b6cc7e9586ff6b9230206c3e57e6b01b86f
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083794"
---
# <a name="prepare-win32-app-content-for-upload"></a>De Win32-app-inhoud voorbereiden om te worden geüpload

Voordat u een Win32-app kunt toevoegen aan Microsoft Intune, moet u de app voorbereiden met behulp van het [hulpprogramma voor voorbereiding van Microsoft Win32-inhoud](https://go.microsoft.com/fwlink/?linkid=2065730).

## <a name="prerequisites"></a>Vereisten

Als u Win32-app-beheer wilt gebruiken, moet u aan de volgende criteria voldoen:

- Gebruik Windows 10 versie 1607 of hoger (Enterprise, Pro en Education).
- Apparaten moeten worden gekoppeld aan Azure Active Directory (Azure AD) en automatisch ingeschreven. De Intune-beheeruitbreiding biedt ondersteuning voor apparaten die zijn toegevoegd aan Azure AD, aan een hybride domein zijn toegevoegd en via een groepsbeleid zijn ingeschreven. 
  > [!NOTE]
  > Voor het scenario met inschrijving via het groepsbeleid maakt de gebruiker gebruik van het lokale gebruikersaccount om hun Windows 10-apparaat met Azure AD samen te voegen. Gebruikers moeten zich op het apparaat aanmelden met hun Azure AD-gebruikersaccount en zich bij inschrijven bij Intune. Intune installeert de Intune-beheerextensie op het apparaat als een PowerShell-script of een Win32-app op de gebruiker of het apparaat is gericht.
- De grootte van Windows-toepassingen is beperkt tot 8 GB per app.

## <a name="convert-the-win32-app-content"></a>De inhoud van de Win32-app converteren

Gebruik het [hulpprogramma voor voorbereiding van Microsoft Win32-inhoud](https://go.microsoft.com/fwlink/?linkid=2065730) om klassieke Windows-apps (Win32) alvast te verwerken. Met het hulpprogramma converteert u de app-installatiebestanden naar de indeling *.intunewin*. Het hulpprogramma detecteert ook enkele kenmerken die voor Intune zijn vereist om de installatiestatus van de toepassing te bepalen. Nadat u dit hulpprogramma hebt gebruikt in de map van het app-installatieprogramma, kunt u een Win32-app maken in de Intune-console.

> [!IMPORTANT]
> Alle bestanden en submappen worden met het [hulpprogramma voor de voorbereiding van Microsoft Win32-inhoud](https://go.microsoft.com/fwlink/?linkid=2065730) ingepakt wanneer het *.intunewin*-bestand wordt gemaakt. Zorg ervoor dat u het hulpprogramma voor de voorbereiding van Microsoft Win32-inhoud gescheiden houdt van de bestanden en mappen van het installatieprogramma, zodat u het hulpprogramma of andere onnodige bestanden en mappen niet in uw *.intunewin*-bestand insluit.

U kunt het [hulpprogramma voor voorbereiding van Microsoft Win32-inhoud](https://go.microsoft.com/fwlink/?linkid=2065730) als zip-bestand downloaden via GitHub. Het ingepakte bestand bevat de map *Microsoft-Win32-Content-Prep-Tool-master*. In de map vindt u het voorbereidingsprogramma, de licentie, een readme-bestand en de release-opmerkingen. 

### <a name="process-flow-to-create-a-intunewin-file"></a>Processtroom voor het maken van een .intunewin-bestand

   <img alt="Flow chart of the process to create a .intunewin file." src="./media/apps-win32-app-management/prepare-win32-app.png" width="700">

### <a name="running-the-microsoft-win32-content-prep-tool"></a>Het hulpprogramma voor de voorbereiding van Microsoft Win32-inhoud uitvoeren

Als u `IntuneWinAppUtil.exe` uitvoert zonder parameters vanuit het opdrachtvenster, krijgt u in het hulpprogramma stapsgewijze instructies voor het invoeren van de vereiste parameters. Of u kunt de parameters aan de opdracht toevoegen op basis van de volgende beschikbare opdrachtregelparameters.

### <a name="available-command-line-parameters"></a>Beschikbare opdrachtregelparameters 

|    **Opdrachtregelparameter**    |    **Beschrijving**    |
|--------------------------------|------------------------------------------------------------|
|    `-h`     |    Help    |
|    `-c <setup_folder>`     |    De map voor alle installatiebestanden. Alle bestanden in deze map worden gecomprimeerd naar een *.intunewin*-bestand.    |
|    `-s <setup_file>`     |    Installatiebestand (zoals *setup.exe* of *setup.msi*).    |
|    `-o <output_folder>`     |    Uitvoermap voor het gegenereerde *.intunewin*-bestand.    |
|    `-q`       |    Stille modus.    |

### <a name="example-commands"></a>Voorbeeldopdrachten

|    **Voorbeeldopdracht**    |    **Beschrijving**    |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `IntuneWinAppUtil -h`    |    Met deze opdracht worden de gebruiksgegevens voor het hulpprogramma weergegeven.    |
|    `IntuneWinAppUtil -c c:\testapp\v1.0 -s c:\testapp\v1.0\setup.exe -o c:\testappoutput\v1.0 -q`    |    Met deze opdracht genereert u het *.intunewin*-bestand van de opgegeven bronmap en het installatiebestand. Dit hulpprogramma haalt vereiste informatie voor Intune op voor het MSI-installatiebestand. Als `-q` is opgegeven, wordt de opdracht uitgevoerd in de stille modus. Als het uitvoerbestand al bestaat, wordt dit overschreven. Als de uitvoermap niet bestaat, wordt deze automatisch gemaakt.    |

Wanneer u het *.intunewin*-bestand genereert, plaatst u eventuele referentiebestanden in een submap van de map van het installatieprogramma. Vervolgens gebruikt u een relatief pad om te verwijzen naar het specifieke bestand dat u nodig hebt. Bijvoorbeeld:

**Bronmap voor installatieprogramma:** *c:\testapp\v1.0*<br>
**Licentiebestand:** *c:\testapp\v1.0\licenses\license.txt*

Verwijs naar het bestand *license.txt* door het relatieve pad *licenses\license.txt* te gebruiken.

## <a name="next-steps"></a>Volgende stappen

- [Een Win32-app toevoegen aan Microsoft Intune](apps-win32-add.md)

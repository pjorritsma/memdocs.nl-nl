---
title: Windows-toepassingen maken
titleSuffix: Configuration Manager
description: Meer informatie over het maken en implementeren van Windows-toepassingen in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ddd01055ac6edf2872854c93cc5172b396052ad2
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270851"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Windows-toepassingen maken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Naast de andere Configuration Manager-vereisten en-procedures voor het [maken van een toepassing](../deploy-use/create-applications.md), moet u ook rekening houden met de volgende overwegingen wanneer u toepassingen voor Windows-apparaten maakt en implementeert.  

## <a name="general-considerations"></a><a name="bkmk_general"></a>Algemene overwegingen  

Configuration Manager ondersteunt de implementatie van Windows-app-pakket (. appx) en app-bundel (. appxbundle) voor Windows 8,1-en Windows 10-apparaten.

Wanneer u een toepassing maakt in de Configuration Manager-console, selecteert u het installatie bestands **type** van de toepassing als **Windows-app-pakket ( \* . appx, \* . appxbundle, \* . msix, \* . msixbundle)**. Zie [toepassingen maken](../deploy-use/create-applications.md)voor meer informatie over het maken van apps in het algemeen. Zie [ondersteuning voor MSIX-indeling](#bkmk_msix)voor meer informatie over de MSIX-indeling.

> [!Note]  
> Als u gebruik wilt maken van nieuwe Configuration Manager functies, moet u clients eerst bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.<!--SCCMDocs issue 646-->  

## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a><a name="bkmk_provision"></a>Windows-app-pakketten inrichten voor alle gebruikers op een apparaat
<!--1358310-->
Richt een toepassing in met een Windows-app-pakket voor alle gebruikers op het apparaat. Een veelvoorkomend voor beeld van dit scenario is het inrichten van een app van de Microsoft Store for Business en Education, zoals Minecraft: Education Edition, op alle apparaten die worden gebruikt door studenten op school. Voorheen Configuration Manager alleen de installatie van deze toepassingen per gebruiker ondersteund. Nadat u zich hebt aangemeld bij een nieuw apparaat, moet een student wachten op toegang tot een app. Wanneer de app nu voor alle gebruikers op het apparaat wordt ingericht, kunnen ze sneller productief zijn.

> [!Important]  
> Wees voorzichtig met het installeren, inrichten en bijwerken van verschillende versies van hetzelfde Windows-app-pakket op een apparaat. Dit kan leiden tot onverwachte resultaten. Dit gedrag kan optreden wanneer Configuration Manager wordt gebruikt om de app in te richten, maar vervolgens gebruikers toestaan om de app vanuit de Microsoft Store bij te werken. Zie de volgende richt lijnen voor meer informatie over het [beheren van apps vanuit de Microsoft Store voor bedrijven](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Bij het implementeren van offline-Apps op Windows 10-apparaten met de Configuration Manager-client, mogen gebruikers geen toepassingen die extern kunnen worden bijgewerkt met Configuration Manager-implementaties. Het beheren van updates voor offline Apps is vooral belang rijk in omgevingen met meerdere gebruikers, zoals klas lokalen. Zie [apps beheren vanuit de Microsoft Store voor bedrijven en onderwijs met Configuration Manager](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps)voor meer informatie.<!-- MEMDocs#316 -->

Configuration Manager ondersteunt het inrichten van apps op alle ondersteunde versies van Windows 10.<!--SCCMDocs-pr issue 2762-->

<!--
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later
-->

Als u een Windows-app-implementatie type voor deze functie wilt configureren, schakelt u de optie voor het **inrichten van deze toepassing voor alle gebruikers op het apparaat**in. Zie [toepassingen maken](../deploy-use/create-applications.md)voor meer informatie.

> [!Note]  
> Als u een ingerichte toepassing moet verwijderen van apparaten waarop gebruikers al zijn aangemeld, moet u twee implementaties voor verwijderen maken. Richt de eerste implementatie voor het verwijderen naar een verzameling apparaten die de apparaten bevat. Richt de tweede implementatie voor verwijderen uit voor een gebruikers verzameling die de gebruikers bevat die al zijn aangemeld bij apparaten met de ingerichte toepassing. Wanneer u een ingerichte app op een apparaat verwijdert, wordt die app momenteel niet door Windows verwijderd voor gebruikers.

## <a name="support-for-msix-format"></a><a name="bkmk_msix"></a>Ondersteuning voor MSIX-indeling
<!--1357427-->

Configuration Manager ondersteunt de indelingen voor het Windows 10-app-pakket (. msix) en app-bundel (. msixbundle). Windows 10 versie 1809 of hoger ondersteunen deze indelingen.

- Ga voor een overzicht van MSIX naar [een](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix)meer informatie over MSIX.  

- Zie voor meer informatie over het maken van een nieuwe MSIX-app [MSIX-ondersteuning geïntroduceerd in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  

### <a name="convert-applications-to-msix"></a>Toepassingen converteren naar MSIX
<!--3607729, fka 1359029-->

Converteer uw bestaande Windows Installer-toepassingen (. msi) naar de MSIX-indeling.

#### <a name="prerequisites-for-msix"></a>Vereisten voor MSIX

- Een referentie apparaat met Windows 10 versie 1809 of hoger  

- Meld u aan bij Windows op dit apparaat als een gebruiker met lokale beheerders rechten  

- De volgende apps installeren op dit apparaat:  

  - Configuration Manager-console  

  - Installeer het [MSIX-verpakkings programma](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) vanaf het Microsoft Store  

  - Installeer het [stuur programma](https://docs.microsoft.com/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers) voor het MSIX-pakket<!--SCCMDocs-pr issue #3091-->  

Installeer geen andere apps of services op dit apparaat. Het is uw referentie systeem.

#### <a name="process-to-convert-applications-to-msix-format"></a>Proces voor het converteren van toepassingen naar de MSIX-indeling

1. Breid de Configuration Manager-console uit, ga naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **toepassingen** .  

2. Selecteer een toepassing met een Windows Installer-implementatie type (. msi).  

    > [!Note]  
    > U moet toegang hebben tot de bron inhoud van de toepassing van het referentie apparaat.  
    >
    > De naam van de toepassing mag geen speciale tekens bevatten. Configuration Manager gebruikt de app-naam als de naam van het uitvoer bestand.  
    >
    > Installeer deze toepassing niet vooraf op het referentie apparaat.  

3. Selecteer **converteren naar. MSIX** in het lint.

Wanneer de wizard is voltooid, maakt het MSIX-hulp programma een MSIX-bestand op de locatie die u in de wizard hebt opgegeven. Tijdens dit proces wordt de toepassing door Configuration Manager op de achtergrond geïnstalleerd op het referentie apparaat.

Als het proces mislukt, verwijst de pagina samen vatting naar het logboek bestand met meer informatie. Als er een fout is opgetreden bij het vastleggen van de gebruikers status, meldt u zich af bij Windows. Dit probleem kan mogelijk worden opgelost als u zich opnieuw aanmeldt.

Als u deze MSIX-app wilt gebruiken, moet u deze eerst digitaal ondertekenen zodat clients deze kunnen vertrouwen. Zie de volgende artikelen voor meer informatie over dit proces:

- [MSIX: het MSIX-hulp programma voor het ondertekenen van het MSIX-pakket](https://docs.microsoft.com/archive/blogs/sgern/msix-the-msix-packaging-tool-signing-the-msix-package)
- [Een app-pakket ondertekenen met SignTool](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

Nadat u de app hebt ondertekend, maakt u een nieuw implementatie type voor de toepassing in Configuration Manager. Zie [implementatie typen voor de toepassing maken](../deploy-use/create-applications.md#bkmk_create-dt)voor meer informatie.

## <a name="task-sequence-deployment-type"></a><a name="bkmk_tsdt"></a>Implementatie type voor taken reeks

<!--3555953-->

> [!Note]  
> In deze versie van Configuration Manager is het implementatie type van de taken reeks een functie van de voorlopige versie. Zie [functies van voorlopige versies](../../core/servers/manage/pre-release-features.md)om deze functie in te scha kelen.  

Vanaf versie 2002 kunt u complexe toepassingen installeren met behulp van taken reeksen via het toepassings model. Voeg een taken reeks implementatie type toe aan een app om de app te installeren of te verwijderen. Dit implementatie type biedt het volgende gedrag:

<!-- - Deploy an app task sequence to a user collection -->

- De taken reeks van de app weer geven met een pictogram in Software Center. Een pictogram maakt het gemakkelijker voor gebruikers om de taken reeks van de app te vinden en te identificeren.

- Aanvullende meta gegevens definiëren voor de taken reeks van de app, inclusief gelokaliseerde informatie

U kunt een taken reeks voor een implementatie zonder besturings systeem alleen toevoegen als een implementatie type voor een app. Het hoge effect, de implementatie van besturings systemen of upgrade taken reeksen van besturings systemen worden niet ondersteund. <!--A user-targeted deployment still runs in the user context of the local System account.-->

Wanneer u dit implementatie type toevoegt aan een app, configureert u de eigenschappen op de pagina **taken reeks** . Zie [implementatie type **taken reeks** opties](../deploy-use/create-applications.md#bkmk_dt-ts)voor meer informatie.

### <a name="prerequisites-for-a-task-sequence-deployment-type"></a>Vereisten voor een implementatie type voor een taken reeks

Een aangepaste taken reeks maken:

- Gebruik alleen implementatie stappen zonder besturings systeem, bijvoorbeeld: **pakket installeren**, **opdracht regel uitvoeren**of **Power shell-script uitvoeren**. Zie [een taken reeks maken voor niet-besturingssysteem implementaties](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)voor meer informatie over de volledige lijst met ondersteunde stappen.

- Op de taken reeks eigenschappen, tabblad **gebruikers melding** , selecteert u niet de optie voor een taken reeks met een hoge impact.

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

Wanneer u de toepassing maakt, moet uw gebruikers account machtigingen voor het lezen van taken reeksen toevoegen om een implementatie type voor de taken reeks toe te voegen.<!-- 6348976 --> Gebruik een van de volgende opties om deze machtigingen te configureren:

- Voeg het gebruikers account van de app-beheerder toe aan de ingebouwde rol **alleen-lezen analist** . Met deze rol kunnen ze alle Configuration Manager-objecten weer geven.

- Kopieer de ingebouwde rol **toepassings beheerder** om een aangepaste rol te maken. Voeg de machtiging **lezen** toe aan het object van het **taken reeks pakket** .

### <a name="known-issues-for-a-task-sequence-deployment-type"></a>Bekende problemen voor een implementatie type voor een taken reeks

- U kunt een app-taken reeks nog niet implementeren voor een gebruikers verzameling

- Gebruik niet de stap **toepassing installeren** in deze taken reeks. Gebruik de stap [pakket installeren](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) om apps te installeren.

## <a name="support-for-universal-windows-platform-uwp-apps"></a><a name="bkmk_uwp"></a>Ondersteuning voor Universeel Windows-platform-apps (UWP)  

Voor Windows 10-apparaten is geen sideloading-code vereist om line-of-Business-Apps te installeren. Als u extern laden wilt inschakelen, moet de register sleutel echter de `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` waarde **1**hebben.  

Als u deze register sleutel niet configureert, wordt deze waarde door Configuration Manager automatisch ingesteld op **1** wanneer u voor het eerst een app op het apparaat implementeert. Als u deze waarde instelt op **0**, kan Configuration Manager de waarde niet automatisch wijzigen en mislukt de implementatie van de line-of-Business-app.  

UWP line-of-Business-Apps van een digitale hand tekening voorzien. Gebruik een certificaat voor ondertekening van programma code dat wordt vertrouwd op elk apparaat waarop u de app implementeert. Certificaten uit de PKI van uw organisatie gebruiken of een certificaat aanschaffen bij een externe provider waarvan het open bare basis certificaat al wordt vertrouwd door Windows.  

Als u mobiele app-pakketten wilt ondertekenen, gebruikt u de volgende tabel om te bepalen welk type certificaat voor ondertekening van programma code moet worden gebruikt:

| Pakket  | Symantec  | Niet-Symantec  |
|---------|---------|---------|
| Universele **. appx** -pakketten op Windows 10 Mobile-apparaten | Ja | Ja |
| **. xap** -pakketten | Yes | Nee |
| **. appx** -pakketten die zijn gemaakt voor Windows Phone 8,1, kunnen worden geïnstalleerd op Windows 10 Mobile-apparaten | Yes | Nee |

## <a name="deploy-windows-installer-apps-to-mdm-enrolled-windows-10-devices"></a><a name="bkmk_mdm-msi"></a>Windows Installer-apps implementeren op MDM-Inge schreven Windows 10-apparaten  

Met het implementatie type **Windows Installer via MDM ( \* . msi)** kunt u op Windows Installer gebaseerde apps maken en implementeren op apparaten die zijn geregistreerd met MDM met Windows 10.  

Wanneer u dit implementatie type gebruikt, moet u rekening houden met de volgende punten:

- Upload slechts één bestand met de MSI-extensie.  

- Configuration Manager gebruikt de product code en product versie van het bestand voor app-detectie.  

- Windows maakt gebruik van het standaard gedrag voor opnieuw opstarten van de app. Configuration Manager heeft geen invloed op het opnieuw opstarten van de app.  

- MSI-pakketten per gebruiker worden voor één gebruiker geïnstalleerd.  

- MSI-pakketten per computer worden voor alle gebruikers van het apparaat geïnstalleerd.  

- Configuration Manager ondersteunt app-updates. De MSI-product code van elke versie moet hetzelfde zijn.  

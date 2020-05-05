---
title: Evaluatie van de compatibiliteit
titleSuffix: Configuration Manager
description: Meer informatie over compatibiliteits evaluatie voor Windows-apps en-stuur Programma's in Desktop Analytics.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eedd33999ce17417122b2403c777a0b560e5f197
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/24/2020
ms.locfileid: "82109995"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Compatibiliteits evaluatie in Desktop Analytics

De upgrade-evaluaties in de vorige oplossingen waren bijvoorbeeld algemeen, zoals de aandacht die nodig is of die is opgelost. Het biedt geen visuele indicator voor het bepalen van de prioriteit van apps of stuur Programma's met problemen of het bijwerken van inzichten. Desktop Analytics vervangt deze functie met **compatibiliteits Risico's**. Desktop Analytics toont alleen de evaluatie voor apps in de implementatie weergave voor een scenario vóór de upgrade. De apps worden gecategoriseerd op basis van inzichten die door micro soft worden opgehaald van de computers die zijn opgenomen in een huidige implementatie plan.

Desktop Analytics maakt gebruik van de volgende categorieën van de compatibiliteits beoordeling:

- **Laag**: de service heeft geen signalen gevonden om deze app risico te nemen voor een Windows-upgrade. Het werkt waarschijnlijk met het doel besturingssysteem.

- **Medium**: Analytics geeft aan dat de toepassing mogelijk een gebrekkige functionaliteit heeft, hoewel herstel waarschijnlijk wel mogelijk is.

- **Hoog**: de toepassing is bijna zeker mislukt tijdens of na de upgrade. Mogelijk is er een herbemiddeling vereist.

- **Onbekend**: de app is niet geëvalueerd. Er zijn geen andere inzichten zoals *bekende problemen met MS*.

In de lijst met app-of stuur programma-assets in een implementatie plan ziet u deze waarde voor elk element in de kolom **compatibiliteits risico** .

## <a name="app-risk-assessment"></a>Risico analyse van de app

![Diagram van bronnen van de risico analyse van de app](media/app-risk-assessment-sources.png)

Er zijn verschillende bronnen die door Desktop Analytics worden gebruikt voor het genereren van de beoordelings classificatie voor toepassingen:

- [Bekende problemen met micro soft](#microsoft-known-issues)
- [Geavanceerde inzichten](#advanced-insights)

U kunt de evaluatie voor elke bron in de app vinden in Desktop Analytics. Selecteer in de lijst met app-assets in een implementatie plan een afzonderlijke app om het deel venster met de eigenschappen te openen. U ziet een algemene aanbeveling en beoordelings niveau. De sectie **compatibiliteits risico factoren** bevat Details voor deze evaluaties.

## <a name="microsoft-known-issues"></a>Bekende problemen met micro soft

Desktop Analytics bekijkt de compatibiliteits database van micro soft app voor bekende problemen. Deze data base wordt gebruikt om te bepalen of er bestaande compatibiliteits blokken zijn voor openbaar beschik bare toepassingen van micro soft of andere uitgevers. Deze controle is alleen van toepassing op het doel besturingssysteem voor het implementatie plan dat u selecteert.

U ziet de volgende problemen in het deel venster app-eigenschappen als **MS-bekende problemen**:

### <a name="asset-is-removed-during-upgrade"></a>Activa worden tijdens de upgrade verwijderd

Windows heeft compatibiliteits problemen met een toepassing of stuur programma gedetecteerd. De Asset wordt niet gemigreerd naar de nieuwe versie van het besturings systeem. Voor de upgrade is geen actie vereist om door te gaan. Installeer een compatibele versie van de toepassing of het stuur programma op de nieuwe versie van het besturings systeem.

<!-- 3594545 -->
Windows kan deze assets gedeeltelijk of volledig verwijderen:

- Volledig verwijderd: Windows Setup verwijdert de app of het stuur programma volledig van het apparaat tijdens de upgrade.
- Gedeeltelijk verwijderen: Windows Setup verwijdert de app of het stuur programma gedeeltelijk van het apparaat. U moet deze hand matig verwijderen nadat u Windows hebt bijgewerkt.

In beide gevallen kan de gebruiker na het uitvoeren van een upgrade van Windows de app of de hardware die aan het stuur programma is gekoppeld, niet meer gebruiken.

Ga als volgt te voor deze aanbeveling in de Desktop Analytics-portal:

1. Selecteer **pilot voorbereiden**in een implementatie plan.
1. Selecteer het tabblad **apps** .
1. Selecteer een app en Bekijk de compatibiliteits Risico's en aanbevelingen in het zijvenster.

[![Scherm afbeelding van de aanbeveling van het activum in de Desktop Analytics-Portal](media/3594545-app-removed.png)](media/3594545-app-removed.png#lightbox)

### <a name="blocking-upgrade"></a>Upgrade blok keren

Er zijn problemen met het blok keren gedetecteerd en de toepassing kan niet worden verwijderd tijdens de upgrade. Het werkt mogelijk niet in de nieuwe versie van het besturings systeem. Voordat u een upgrade uitvoert, moet u de toepassing verwijderen. Installeer het programma opnieuw en test het op de nieuwe versie van het besturings systeem.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>De upgrade wordt geblokkeerd, maar kan na de upgrade opnieuw worden geïnstalleerd

De toepassing is compatibel met de nieuwe versie van het besturings systeem, maar kan niet worden gemigreerd. Verwijder de toepassing voordat u een upgrade van Windows uitvoert. Installeer het opnieuw op de nieuwe versie van het besturings systeem.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>De upgrade wordt geblokkeerd, de toepassing wordt bijgewerkt naar de nieuwste versie

De bestaande versie van de toepassing is niet compatibel met de nieuwe versie van het besturings systeem en kan niet worden gemigreerd. Er is een compatibele versie van de toepassing beschikbaar. Werk de toepassing bij voordat u de upgrade uitvoert.

### <a name="disk-encryption-blocking-upgrade"></a>Upgrade van schijf versleuteling blokkeert

De versleutelings functies van de toepassing blok keren de upgrade. Schakel de versleutelings functie uit voordat u Windows bijwerkt en deze na de upgrade inschakelt.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Werkt niet met een nieuw besturings systeem, maar blokkeert geen upgrade

De toepassing is niet compatibel met de nieuwe versie van het besturings systeem, maar blokkeert de upgrade niet. Voor de upgrade is geen actie vereist om door te gaan. Installeer een compatibele versie van de toepassing op de nieuwe versie van het besturings systeem.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Werkt niet met een nieuw besturings systeem en blokkeert de upgrade

De toepassing is niet compatibel met de nieuwe versie van het besturings systeem en de upgrade wordt geblokkeerd. Verwijder de toepassing voordat u de upgrade uitvoert. Er is mogelijk een compatibele versie van de toepassing beschikbaar.

### <a name="evaluate-application-on-new-os"></a>De toepassing op een nieuw besturings systeem evalueren

De toepassing wordt door Windows gemigreerd, maar er zijn problemen gedetecteerd die van invloed kunnen zijn op de prestaties van de app op de nieuwe versie van het besturings systeem. Voor de upgrade is geen actie vereist om door te gaan. Test de toepassing op de nieuwe versie van het besturings systeem.

### <a name="may-block-upgrade-test-application"></a>Kan de upgrade blok keren, de toepassing testen

Windows heeft problemen gedetecteerd die de upgrade kunnen belemmeren, maar moet verder worden onderzocht. Test het gedrag van de toepassing tijdens de upgrade. Als de upgrade wordt geblokkeerd, moet u deze verwijderen voordat u een upgrade uitvoert. Installeer het vervolgens opnieuw en test op de nieuwe versie van het besturings systeem.

### <a name="multiple"></a>Meerdere

Meerdere problemen zijn van invloed op de toepassing. Selecteer **query** om details weer te geven over de problemen die worden gedetecteerd door Windows.

### <a name="reinstall-application-after-upgrading"></a>Toepassing opnieuw installeren na de upgrade

De toepassing is compatibel met de nieuwe versie van het besturings systeem, maar u moet deze opnieuw installeren nadat u Windows hebt bijgewerkt. Het upgrade proces verwijdert de toepassing. Voor de upgrade is geen actie vereist om door te gaan. Installeer de toepassing opnieuw op de nieuwe versie van het besturings systeem.

### <a name="safeguards"></a>Veiligheids maatregelen

<!-- 5746559 -->

Windows-compatibiliteits gegevens classificeert enkele apps en stuur Programma's met een *beveiliging*, waardoor de update naar Windows 10 kan mislukken of kan worden teruggedraaid. Windows kan ook worden bijgewerkt, maar de app of het stuur programma wordt verwijderd. Desktop Analytics kan u nu helpen om deze beveiligings maatregelen vooraf te identificeren, zodat u de Asset kunt herstellen voordat u de update implementeert.

1. Selecteer een implementatie plan in de Desktop Analytics-Portal.

1. Selecteer **assets plannen** in het menu en schakel over naar het tabblad **apps** .

1. Filter de kolom naam om items weer te geven met waarden die het `Safeguard`woord bevatten. Selecteer het resultaat om meer informatie weer te geven.

    > [!NOTE]
    > Dit item is geen echte app die op uw apparaten is geïnstalleerd. Het is een tijdelijke aanduiding waarmee u apps of stuur Programma's in uw omgeving kunt identificeren met de compatibiliteits label voor beveiliging.

1. Selecteer in de sectie aanbeveling de koppeling voor *meer informatie*. Met deze koppeling opent u de Windows-website met de huidige lijst met apps of stuur Programma's met de tag beveiliging.

1. Vergelijk de huidige gepubliceerde lijst met de lijst met assets in uw omgeving. Herstel alle mogelijk problematische apps of stuur Programma's door een update naar een compatibele versie uit te voeren.

[![Scherm afbeelding van de beveiligde app in Desktop Analytics](media/5746559-safeguards.png)](media/5746559-safeguards.png#lightbox)

## <a name="advanced-insights"></a>Geavanceerde inzichten

Desktop Analytics kan ook problemen detecteren met de volgende aanvullende inzichten:

### <a name="adopted-version-available"></a>Aangenomen versie beschikbaar

Er is een andere versie van deze app die Maxi maal door andere klanten wordt goedgekeurd. Dit signaal gebruikt acceptatie gegevens van het Windows-ecosysteem. Als er upgrade blokken met uw huidige versie zijn, kunt u overwegen om de alternatieve versie te implementeren. Zie Toepassings status onder ' productie voorbereiden ' voor meer informatie over alternatieve toepassingen die zijn goedgekeurd.

### <a name="driver-dependency"></a>Afhankelijkheids afhankelijkheid

De app is afhankelijk van een stuur programma. Desktop Analytics raadt de app aan voor test doeleinden om eventuele regressies te detecteren. Als u problemen ondervindt, neemt u contact op met de uitgever om een versie aan te vragen die compatibel is met Windows 10.

### <a name="additional-insights"></a>Meer inzichten

<!-- 4021225 -->
Wanneer u de Configuration Manager-site en-clients bijwerkt naar versie 1906, rapporteren clients ook deze aanvullende inzichten wanneer het niveau van diagnostische gegevens is ingesteld op uitgebreid beperkt:

> [!Important]  
> Als u optimaal wilt profiteren van de nieuwe functies van Configuration Manager, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Dit scenario is pas functioneel als de client versie ook het meest recent is.

#### <a name="16-bit-apps"></a>16-bits apps

Verwijder alle 16-bits onderdelen van toepassingen en vervang door 32-bits of 64-bits-equivalenten. Zie voor meer informatie [het artikel over Windows Vista en Windows Server 2008 Developer: Application Compatibility Cookbook](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\))(Engelstalig).

De andere optie is NT Virtual DOS machine (NTVDM) inschakelen voor ondersteuning in Windows 10.

#### <a name="requires-admin-privileges"></a>Beheerders bevoegdheden zijn vereist

De gebruiker moet beheerders toegang tot het apparaat hebben voor de app. Gebruik een app-manifest voor deze apps waarvoor beheerders machtigingen zijn vereist. Zie [een toepassings manifest maken en insluiten](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\))voor meer informatie.

Desktop Analytics raadt de app aan voor test doeleinden om eventuele regressies te detecteren.

#### <a name="java-dependency"></a>Java-afhankelijkheid

Veel Java-toepassingen zijn afhankelijk van een afzonderlijk geïnstalleerd Java Runtime Environment (JRE). Hoewel oudere JRE-versies mogelijk blijven werken in Windows 10, ondersteunt Oracle alleen de nieuwste JRE-versies. Het gebruik van een oudere, niet-ondersteunde JRE kan beveiligings problemen bevatten. Controleer of uw toepassing wordt uitgevoerd met de meest recente JRE-versies.

#### <a name="not-dpi-aware"></a>Niet-DPI-detectie

Er zijn mogelijk problemen met de weer gave van de app met geavanceerde scherm resoluties in Windows 10. Gebruik een app-manifest om problemen met hoge DPI-resoluties te voor komen. Zie [toepassings manifesten](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests)voor meer informatie.

Desktop Analytics raadt de app aan voor test doeleinden om eventuele regressies te detecteren.

#### <a name="silverlight-framework"></a>Silverlight-framework

Micro soft adviseert dat niet-browser-apps niet gebruikmaken van Silverlight. De ondersteunings eind datum voor Silverlight 5 is 2021 oktober.

De meeste huidige webbrowsers bieden geen ondersteuning voor Silverlight.

| Browser | Ondersteuning |
|---------|---------|
| Google Chrome | Einde van de ondersteuning: september 2015 |
| Firefox | Einde van de ondersteuning: maart 2017 |
| Microsoft Edge | Geen invoeg toepassing beschikbaar |

Desktop Analytics raadt de app aan voor test doeleinden om eventuele regressies te detecteren.

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

De .NET Framework versie 1,0 wordt niet ondersteund in Windows 10. Versie 1,1 is niet compatibel met Windows 10. Als de app afkomstig is van een uitgever van derden, neemt u contact op met de leverancier om een versie aan te vragen die compatibel is met Windows 10. Als dat niet het geval is, kunt u de toepassing opnieuw ontwikkelen voor gebruik van een ondersteunde versie van .NET.

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

.NET 2,0-en 3,5-frameworks worden ondersteund op Windows 10. Mogelijk moet u de Windows-functie inschakelen. Zie [install the .NET Framework 3,5 in Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10)(Engelstalig) voor meer informatie.

#### <a name="ui-access"></a>Toegang tot gebruikers interface

Toepassingen die toegang hebben tot de gebruikers interface, kunnen de besturings niveaus van de configuratie van de gebruiker en de invoer op het bureau blad op de Windows-computer. Gebruik deze instelling alleen voor Program ma's die hulp bieden aan de gebruikers interface.

Als u geen gebruik maakt van toegankelijkheids functies in uw app, stelt u de toegangs vlag voor de gebruikers interface in het app-manifest in op ONWAAR. Zie [een toepassings manifest maken en insluiten](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\))voor meer informatie.

Desktop Analytics raadt de app aan voor test doeleinden om eventuele regressies te detecteren.

## <a name="driver-risk-assessment"></a>Risico analyse van Stuur Programma's

Desktop Analytics bevat ook lijsten en groepen per Beschik baarheid van Stuur Programma's die niet worden gemigreerd naar de versie van het besturings systeem.

U kunt de evaluatie vinden in het stuur programma in Desktop Analytics. Selecteer in de lijst met stuur programma-assets in een implementatie plan een afzonderlijk stuur programma om het deel venster met de eigenschappen te openen. U ziet een algemene aanbeveling en beoordelings niveau. De sectie **compatibiliteits risico factoren** bevat Details voor deze evaluaties.

| Beschik baarheid Stuur Programma's | Actie vereist? | Wat het betekent | Richtlijnen |
|---------------------|------------------|---------------|----------|
| Beschikbaar in box | Nee, alleen voor bewustzijn | De momenteel geïnstalleerde versie van een toepassing of stuur programma wordt niet gemigreerd naar de nieuwe versie van het besturings systeem. Er wordt een compatibele versie geïnstalleerd met de nieuwe versie van het besturings systeem. | Voor de upgrade is geen actie vereist om door te gaan. |
| Importeren uit Windows Update | Ja | De versie van een stuur programma die momenteel is geïnstalleerd, wordt niet gemigreerd naar de nieuwe versie van het besturings systeem. Een compatibele versie is beschikbaar via Windows Update. | Als de computer automatisch updates ontvangt van Windows Update, is geen actie vereist. Als dat niet het geval is, kunt u na het upgraden van Windows een nieuw stuur programma importeren uit Windows Update. |
| Beschikbaar in box en van Windows Update | Ja | De versie van een stuur programma die momenteel is geïnstalleerd, wordt niet gemigreerd naar de nieuwe versie van het besturings systeem. Hoewel er tijdens de upgrade een nieuw stuur programma wordt geïnstalleerd, is er een nieuwere versie beschikbaar van Windows Update. | Als de computer automatisch updates ontvangt van Windows Update, is geen actie vereist. Als dat niet het geval is, kunt u na het upgraden van Windows een nieuw stuur programma importeren uit Windows Update. |
| Controleren bij leverancier | Ja | Het stuur programma wordt niet gemigreerd naar de nieuwe versie van het besturings systeem en desktop Analytics kan geen compatibele versie vinden. | Voor een oplossing raadpleegt u de onafhankelijke hardwareleverancier die het stuur programma produceert, of de OEM (Original Equipment Manufacturer) die het apparaat heeft geleverd. |

## <a name="see-also"></a>Zie ook

Het FastTrack Center-voor deel voor Windows 10 biedt toegang tot de **desktop-app**. Dit voor deel is een nieuwe service die is ontworpen om problemen met Windows 10-en Microsoft 365-apps te verhelpen voor compatibiliteit met bedrijven. Zie voor meer informatie [bureau blad-app garanderen](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).

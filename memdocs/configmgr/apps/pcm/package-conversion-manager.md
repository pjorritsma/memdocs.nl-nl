---
title: Package Conversion Manager
titleSuffix: Configuration Manager
description: Meer informatie over package Conversion Manager voor het converteren van pakketten naar toepassingen in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 075dd860d20662679e5bdf58dae23d0220fa751e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709913"
---
# <a name="package-conversion-manager"></a>Package Conversion Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1357861-->

Vanaf versie 1806 kunt u met package Conversion Manager Configuration Manager verouderde pakketten omzetten in toepassingen. Toepassingen hebben extra voor delen, zoals afhankelijkheden, vereisten regels, detectie methoden en affiniteit tussen gebruikers en apparaten.

> [!Tip]  
> Deze functie werd voor het eerst in versie 1806 geïntroduceerd als een [voorlopige functie](../../core/servers/manage/pre-release-features.md). Vanaf versie 1810 is deze functie niet langer een functie van de voorlopige versie.  


Een Configuration Manager toepassing bevat bestanden en Program ma's die u implementeert op client apparaten. Maar in tegens telling tot oudere pakketten en Program ma's biedt een toepassing aanvullende gebruikers gerichte functionaliteit. Een toepassing kan bijvoorbeeld implementatie typen bevatten voor een lokale installatie van een software pakket, een virtueel toepassings pakket of een versie van de toepassing voor mobiele apparaten.

Raadpleeg voor meer informatie de volgende artikelen: 
- [Inleiding op toepassingsbeheer](../understand/introduction-to-application-management.md)  
- [Pakketten en programma's](../deploy-use/packages-and-programs.md)  

> [!Important]  
> Als u eerder een oudere versie van package Conversion Manager hebt geïnstalleerd, moet u deze eerst verwijderen voordat u de site bijwerkt. Voor deze geïntegreerde versie is geen installatie vereist, maar dit kan conflicteren met bestaande versies.  

Deze geïntegreerde versie van package Conversion Manager werkt op pakketten in de Configuration Manager huidige branch-site. Het is geen zelfstandig hulp programma. Als u pakketten en Program ma's in een oudere versie van Configuration Manager hebt, migreert u de pakketten eerst naar uw huidige branch-site. Zie voor meer informatie [migreren van gegevens tussen hiërarchieën](../../core/migration/migrate-data-between-hierarchies.md).

<!-- SCCMDocs-pr issue #3357 -->
Configuration Manager versie 1902 bevat de volgende verbeteringen:
- Geplande pakket analyse wordt standaard elke 7 dagen uitgevoerd
- Power shell-cmdlets voor het analyseren en converteren van pakketten
- Algemene oplossingen voor fouten en verbeteringen



## <a name="planning"></a>Planning

Voordat u begint met het converteren van pakketten naar toepassingen, moet u eerst een plan ontwikkelen. Het volgende proces is een voor beeld van een plan:

- [Een gedetailleerd plan voor pakket conversie definiëren](#bkmk_define)  

- [Pakketten selecteren en voorbereiden voor de conversie](#bkmk_prepare)  

- [Test pakketten selecteren](#bkmk_test)  

- [Pakketten analyseren, onderzoeken en converteren](#bkmk_analyze)  

- [De toepassingen testen en implementeren](#bkmk_deploy)  


### <a name="define-a-detailed-package-conversion-plan"></a><a name="bkmk_define"></a>Een gedetailleerd plan voor pakket conversie definiëren

In deze sectie worden twee voorbeeld plannen voor pakket conversie beschreven:  

- [Een test omgeving met hoge bronnen](#bkmk_define-high): u hebt een test omgeving met de resources, machtigingen en architectuur om uw productie omgeving volledig te repliceren.  

- [Een test omgeving met een beperkt aantal resources](#bkmk_define-limited): u hebt geen test omgeving die uw productie omgeving volledig repliceert.  

Pas deze plannen zo nodig aan voor andere problemen die specifiek zijn voor uw omgeving.

#### <a name="sample-plan-for-a-high-resource-test-environment"></a><a name="bkmk_define-high"></a>Voorbeeld plan voor een test omgeving met hoge bronnen

Uw test omgeving heeft de resources, machtigingen en architectuur die vergelijkbaar zijn met uw productie omgeving. Gebruik de test omgeving om alle pakketten efficiënt te analyseren en te converteren en test vervolgens al uw Configuration Manager toepassingen. Nadat u het werk hebt voltooid, brengt u het over naar de productie omgeving. 

Uw plan voor pakket conversie kan overeenkomen met de volgende stappen:  

1.  Selecteer de pakketten die u wilt converteren.  

2.  Migreer de pakketten voor conversie naar uw test omgeving.  

3.  Bereid de pakketten voor op de conversie.  

4.  Selecteer test pakketten.  

5.  Analyseer, onderzoek en converteer de test pakketten.  

6.  De geconverteerde toepassingen testen.  

7.  Analyseer en converteer de resterende pakketten (niet-test).  

8.  Exporteer de toepassingen uit de test omgeving. Importeer ze in uw productie omgeving.  

#### <a name="sample-plan-for-a-limited-resource-test-environment"></a><a name="bkmk_define-limited"></a>Voorbeeld plan voor een test omgeving met een beperkt aantal resources

Uw test omgeving beschikt niet over de resources, machtigingen en architectuur die vergelijkbaar zijn met uw productie omgeving. U kunt niet alle pakketten analyseren, testen en converteren. In dit scenario kunt u de test pakketten alleen analyseren, onderzoeken, converteren en testen. Migreer vervolgens de resterende pakketten naar de productie omgeving om te analyseren en te converteren. 

Uw plan voor pakket conversie kan overeenkomen met de volgende stappen:

1.  Selecteer de pakketten die u wilt converteren.  

2.  Selecteer test pakketten.  

3.  Migreer de test pakketten naar uw test omgeving.  

4.  Bereid de test pakketten voor op de conversie.  

5.  Analyseer, onderzoek en converteer de test pakketten.  

6.  De geconverteerde toepassingen testen.  

7.  Exporteer de test toepassingen vanuit de test omgeving. Importeer ze vervolgens in uw productie omgeving.  

8.  Migreer de resterende pakketten naar de productie omgeving en bereid ze voor op conversie.  

9.  Analyseer, onderzoek en converteer de resterende pakketten in de productie omgeving.  

10. Geef de overige toepassingen vrij voor de productie omgeving.  


### <a name="select-and-prepare-packages-for-conversion"></a><a name="bkmk_prepare"></a>Pakketten selecteren en voorbereiden voor de conversie

#### <a name="select-the-packages-that-you-want-to-convert"></a><a name="bkmk_prepare-select"></a>De pakketten selecteren die u wilt converteren

Niet alle pakketten zijn geschikt om te worden geconverteerd naar toepassingen. Voordat u begint met het converteren van pakketten, identificeert u de pakketten die niet worden geconverteerd. 

De beste typen pakket voor conversie naar toepassingen zijn die op gebruikers gerichte software, bijvoorbeeld:  

- Windows Installer-bestanden (MSI en MSU)  

- Micro soft Application Virtualization-Program ma's (app-V)  

- Uitvoer bare Windows-bestanden (. exe)  

De volgende typen pakketten zijn het meest geschikt om te worden bewaard als pakket en zijn niet geconverteerd naar toepassingen:

- Systeem onderhoud-hulpprogram ma's. Bijvoorbeeld scripts of hulpprogram ma's voor back-ups.  

- Pakketten voor software die niet meer worden ondersteund.

> [!Tip]  
> Na het identificeren van pakketten die niet geschikt zijn voor conversie naar toepassingen, verplaatst u ze naar een afzonderlijke map in de Configuration Manager-console. Een pakketmap maken in de Configuration Manager-console:  
> - Klik met de rechter muisknop op het knoop punt **pakketten** .  
> - Selecteer **mappen**en selecteer vervolgens **map maken**.  
> - Voer de naam van de map in `Not Converted`, bijvoorbeeld.  
> - Klik op **OK**.  

#### <a name="prepare-the-packages-for-conversion"></a>De pakketten voorbereiden voor de conversie

Voor elk pakket dat u wilt converteren, moet u ervoor zorgen dat ze voldoen aan de volgende voor waarden:  

- De locatie van de bron bestanden is bijvoorbeeld `\\Server\Share\File`een volledig UNC-pad.  

- Voor Windows Installer-bestanden wordt slechts één unieke product code gebruikt.  


### <a name="select-test-packages"></a><a name="bkmk_test"></a>Test pakketten selecteren

Indien mogelijk moet uw groep test pakketten pakketten bevatten die voldoen aan de volgende criteria:  

- Ten minste één test pakket met de gereedheids status **automatisch**.  

- Ten minste één test pakket met de gereedheids status **hand matig**.  

In het ideale geval moeten uw test pakketten kern pakketten zijn, bijvoorbeeld:  

- Pakketten waarvan u weet dat ze goed zijn.  

- Pakketten die het belangrijkst zijn voor uw organisatie.  

- Pakketten die u het gemakkelijkst kunt testen.  

Identificeer de pakketten die geschikt zijn voor het testen. Verplaats ze vervolgens naar een afzonderlijke map in de Configuration Manager-console.


### <a name="analyze-investigate-and-convert-packages"></a><a name="bkmk_analyze"></a>Pakketten analyseren, onderzoeken en converteren

#### <a name="analyze-packages"></a>Pakketten analyseren

Als u een afzonderlijk pakket of een kleine groep wilt analyseren, gebruikt u pakket conversie beheer geïntegreerd in de Configuration Manager-console. Zie [pakketten analyseren en converteren](how-to-analyze-and-convert.md)voor meer informatie.  

> [!NOTE]  
> Zie het knoop punt **pakket conversie status** in de werk ruimte **bewaking** . Het geeft samenvattings informatie weer over de analyse-en conversie processen.  

#### <a name="investigate-analysis-results"></a>Analyse resultaten onderzoeken

Na het analyseren van de test pakketten onderzoekt u de pakketten met de gereedheids status **hand matig** of **fout**. Bepaal de redenen waarom ze deze status hebben. Enkele veelvoorkomende redenen voor de gereedheids status **hand matig** of **fout** zijn onder andere:

- Het pakket bevat niet de vereiste informatie voor het maken van een detectie methode in een toepassings implementatie type.  

- Het pakket bevat niet de vereiste gegevens voor het converteren van verzamelingen naar globale voor waarden en vereisten.  

- Het pakket bevat meer dan één programma.  

- Het pakket is afhankelijk van een ander pakket dat u niet hebt geconverteerd naar een toepassing.  

Gebruik de volgende bronnen voor meer informatie:  

- Raadpleeg de fout berichten en oplossingen in [technische Naslag informatie over fout berichten van package Conversion Manager](error-messages.md)  

- Controleer het logboek bestand **PCMTrace. log**  

- [Problemen met Package Conversion Manager oplossen](troubleshoot-pcm.md)  

#### <a name="convert-the-packages"></a>De pakketten converteren

Zie [pakketten analyseren en converteren](how-to-analyze-and-convert.md)voor meer informatie over het converteren van pakketten.

> [!NOTE]  
> Zie het knoop punt **pakket conversie status** in de werk ruimte **bewaking** . Het geeft samenvattings informatie weer over de analyse-en conversie processen.  


### <a name="test-and-deploy-the-applications"></a><a name="bkmk_deploy"></a>De toepassingen testen en implementeren

Test de toepassingen, in uw test omgeving of in uw productie omgeving, op basis van uw gedetailleerde pakket conversie plan.



## <a name="recommendations"></a>Aanbevelingen

- Gebruik het knoop punt **pakket conversie status** in de werk ruimte **bewaking** . Het geeft samenvattings informatie weer over de analyse-en conversie processen.  

- Onderzoek de Program ma's in uw pakketten die wrappers worden genoemd. Gebruik de package Conversion Manager-invoeg toepassing om hun functies te converteren naar de equivalente Configuration Manager functionaliteit.  

- Zorg ervoor dat elke geconverteerde toepassing uitvoerig wordt getest voordat u deze in een productie omgeving implementeert.  



## <a name="next-steps"></a>Volgende stappen

[Pakketten analyseren en converteren](how-to-analyze-and-convert.md)

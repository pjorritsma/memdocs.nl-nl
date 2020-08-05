---
title: Windows Autopilot met co-beheer
titleSuffix: Configuration Manager
description: Gebruik Windows auto pilot met co-beheer in Configuration Manager om het instellen van nieuwe Windows 10-apparaten te vereenvoudigen.
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f77cb76e3cfd9c932a6f3789f98e5616cdaa27eb
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546430"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot met co-beheer

Het ontvangen van een nieuw Windows 10-apparaat is interessant. Het kan echter tijd duren om al uw instellingen en apps te configureren, zodat u productief kunt zijn. Met co-beheer is dit probleem met het inrichten van apparaten opgelost met Windows auto pilot.

Auto Pilot biedt een vereenvoudigde ervaring voor zowel u als uw gebruikers in de volgende situaties:
- Nieuwe Windows 10-apparaten instellen en vooraf configureren  
- Bestaande apparaten opnieuw instellen, recyclen en herstellen  

Automatische pilot vermindert de tijd, bronnen en complexiteit die zijn gekoppeld aan het implementeren, beheren en buiten gebruik stellen van apparaten. Tegelijkertijd wordt de ervaring van uw gebruikers gestroomlijnd en is deze eenvoudig vanaf de eerste keer opgestart.

Windows auto pilot ondersteunt verschillende scenario's, die allemaal zijn gemaximaliseerd met co-beheer:

- Gebruikers kunnen hun eigen implementaties van nieuwe apparaten in een Active Directory met hybride Azure AD-deelname of Azure Active Directory (Azure AD).  

- U kunt zelf nieuwe implementaties van een apparaat instellen in azure AD voor gedeelde apparaten en kiosken  

- Met Windows auto pilot voor bestaande apparaten gebruikt u Configuration Manager om een bestaand apparaat te migreren van Windows 7 en Active Directory naar Windows 10 en Azure AD  

In de volgende video is Senior Program Manager Danny Guillory en Principal Program Manager Andrew McMurray discussiëren en demonstratie Windows auto pilot met co-beheer:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Voordelen

Als u co-beheer en auto pilot samen gebruikt, zorgt u ervoor dat nieuwe apparaten die uw netwerk binnenkomen, in dezelfde staat van beheer terechtkomen. In deze installatie worden apparaten Inge schreven bij intune en beschikken ze over een Configuration Manager-client.  Hiermee kunt u het nieuwe inrichtings model van Windows 10 gebruiken en kunt u de nood zaak om aangepaste installatie kopieën van besturings systemen te maken, te onderhouden en bij te werken, uitschakelen. 

In al deze scenario's kunt u [co-beheer automatisch inschakelen](how-to-prepare-Win10.md) met intune. Deze automatisering helpt bij het inrichtings proces en voor doorlopend beheer van het apparaat.

Met auto pilot hoeft u zich geen zorgen te maken over installatie kopieën en stuur Programma's. Richt u op het inrichten van apparaten op basis van dit geautomatiseerde proces met intune en Configuration Manager via co-beheer.


Met het gebruik van co-beheer en automatische piloten kunt u nu meteen aan de slag:

#### <a name="reduce-time-costs-and-complexity"></a>Minder tijd, kosten en complexiteit
Windows auto pilot maakt gebruik van de door de OEM geoptimaliseerde versie van Windows 10 die vooraf is geïnstalleerd op het apparaat. Deze configuratie bespaart organisaties de inspanningen om aangepaste installatie kopieën en stuur Programma's te onderhouden voor elk model van het apparaat dat wordt gebruikt. In plaats van het apparaat opnieuw te moeten vervormen, moet u de bestaande Windows 10-installatie omzetten in een status die gereed is voor het bedrijf. Het past instellingen en beleid toe, installeert apps en wijzigt de editie van Windows 10. Bijvoorbeeld een upgrade van Windows 10 Pro naar Windows 10 Enter prise, zodat u geavanceerde functies kunt ondersteunen.

#### <a name="improve-the-user-experience"></a>De gebruikers ervaring verbeteren
De beste gebruikers ervaring veroorzaakt de minste onderbrekingen en helpt ze bij het bepalen van de nadruk op hun werk. Windows auto pilot biedt een eenvoudige benadering om uw gebruikers te helpen snel in te stellen met een paar eenvoudige klikken en hun Azure AD-referenties. Voor veel organisaties met een groot veld van externe werk nemers, kunt u Windows auto pilot gebruiken om nieuwe apparaten direct van de fabrikant te verzenden.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Automatische pilot en Configuration Manager gebruiken om bestaande Windows 7-apparaten te migreren naar Windows 10
Met Windows auto pilot voor bestaande apparaten maakt u een configuratie bestand en implementeert u dit met een Configuration Manager taken reeks. Dit proces migreert eenvoudig bestaande apparaten van Windows 7 naar Windows 10. U gebruikt een handtekening installatie kopie van Windows 10 in Configuration Manager en past deze vervolgens toe op het bestaande Windows 7-apparaat met de auto pilot-configuratie. Wanneer de gebruiker het apparaat start, gebruiken ze het voorbereidings proces voor automatische test gebruikers.

Dit zijn de stappen voor automatische test voor bestaande apparaten:

![Overzicht van het proces voor Windows auto pilot voor bestaande apparaten](media/autopilot-for-existing-devices.png)

1. Groeps beleid implementeren om bekende mappen om te leiden naar OneDrive
2. Auto Pilot-configuratie bestand genereren
3. Taken reeks implementeren voor een upgrade naar Windows 10
4. Windows 10-computer loopt door automatische pilot bij eerste keer opstarten

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modern inrichten van apparaten voor alle soorten werk rollen
Met auto pilot kunt u nu een hand-free installatie van het besturings systeem leveren aan onbemande apparaten of gedeelde apparaten die gebruikmaken van de zelf-implementatie modus. Deze installatie voldoet aan de behoeften van al uw verschillende soorten werk nemers. De Windows auto pilot reset-functie zorgt er ook voor dat het opnieuw inrichten van een apparaat naar een nieuwe gebruiker eenvoudig en eenvoudig is. Dit proces vereenvoudigt wat een moeilijke taak was wanneer u seizoen-of contract medewerkers hebt. 



## <a name="case-study"></a>Casestudy

De Duitse logistiek-en rails-Schenker maakt gebruik van auto pilot om de productiviteit van werk nemers te verg Roten en de IT-teams vrij te maken van werk op dagelijkse ondersteunings taken. DB Schenker is verwijderd van traditionele Imaging en is vervangen door het inrichten via de Cloud. Ze maken nu gebruik van Azure AD-samen voegen en intune om nieuwe apparaten snel aan de slag te krijgen. 

In plaats van dat hun externe werk nemers tijd verspillen op een locatie met IT-Services, maakt DB Schenker nu gebruik van Windows auto pilot. Ze leveren hun werk nemers rechtstreeks van de fabrikant naar hun lokale veld kantoor. De werk nemer verbindt het nieuwe apparaat met internet en meldt zich aan met hun Azure AD-referenties. Het apparaat maakt vervolgens verbinding met de toepassingen en services die door de IT-afdeling van de DB-Schenker worden toegewezen aan het afzonderlijke Profiel van de gebruiker.

Zie voor meer informatie [Global logistiek Fiat centraliseren, werk nemers samen met moderne digitale werk plek](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Toegevoegde waarde

Maak tevredenheid in uw organisatie door een betere gebruikers ervaring voor uw gebruikers te maken. Gebruik Windows auto pilot om de kosten te verlagen. Maak uw tijd vrij om zich te richten op andere projecten om meer waarde en invloed voor uw organisatie te best Eden.



## <a name="configure"></a>Configureren

Raadpleeg voor meer informatie de volgende artikelen:

[InTune gebruiken om Windows auto pilot-profielen te maken](https://docs.microsoft.com/intune/enrollment-autopilot)

[Windows Autopilot implementeren voor bestaande apparaten](../../autopilot/existing-devices.md)

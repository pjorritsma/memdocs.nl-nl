---
title: Voorbereide media maken
titleSuffix: Configuration Manager
description: Gebruik voorgefaseerde media in Configuration Manager om de implementatie van Windows in verschillende scenario's te vereenvoudigen.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82bb02d8154939b4b0e0ee89bcc6637e9393acff
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125216"
---
# <a name="create-prestaged-media"></a>Voorbereide media maken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voor bereide media in Configuration Manager is een Windows-installatie kopie (WIM)-bestand. De software kan worden geïnstalleerd op een bare-metal computer door de fabrikant of in het faserings centrum dat niet is verbonden met de productie Configuration Manager omgeving. Voor bereide media bevatten de opstart installatie kopie die wordt gebruikt voor het starten van de doel computer en de installatie kopie van het besturings systeem die wordt toegepast op de doel computer. U kunt ook toepassingen, pakketten en stuurprogrammapakketten opgeven die moeten worden opgenomen als onderdeel van de voorgefaseerde media. De taken reeks die het besturings systeem implementeert, is niet opgenomen in de media. Voorbereide media worden toegepast op de harde schijf van een nieuwe computer voordat de computer wordt verzonden naar de eindgebruiker.

Gebruik voorgefaseerde media voor de volgende implementatie scenario's voor besturings systemen:  

- [Een installatiekopie voor een OEM in de fabriek of bij een lokaal depot maken](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)  

- [Windows to Go implementeren](deploy-windows-to-go.md)  


## <a name="usage"></a>Gebruik

Wanneer de computer voor de eerste keer wordt opgestart nadat u de voor bereide media hebt toegepast, wordt de computer gestart in Windows PE. Er wordt verbinding gemaakt met een beheer punt om de taken reeks te vinden waarmee het implementatie proces van het besturings systeem wordt voltooid. Wanneer u een taken reeks implementeert die gebruikmaakt van vooraf geplaatste media, controleert de client eerst de lokale taken reeks cache op geldige inhoud. Als de inhoud niet wordt gevonden of is gewijzigd, downloadt de client de inhoud van een distributie punt of peer.  


## <a name="prerequisites"></a>Vereisten

Voordat u voorgefaseerde media maakt met behulp van de wizard taken reeks media maken, moet u ervoor zorgen dat aan alle voor waarden wordt voldaan.

### <a name="boot-image"></a>Opstartinstallatiekopie

Houd rekening met de volgende punten over de opstart installatie kopie die u in de taken reeks gebruikt om het besturings systeem te implementeren:

- De architectuur van de opstart installatie kopie moet geschikt zijn voor de architectuur van de doel computer. Op een x64-doelcomputer kan een x86- of x64-opstartinstallatiekopie worden opgestart en uitgevoerd. Op een x86-doelcomputer kan echter alleen een x86-opstartinstallatiekopie worden opgestart en uitgevoerd.
- Zorg ervoor dat de opstart installatie kopie de netwerk-en opslag Stuur Programma's bevat die nodig zijn om de doel computer in te richten.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Een taken reeks maken om een besturings systeem te implementeren

Geef als onderdeel van de voorgefaseerde media de taken reeks op om het besturings systeem te implementeren. Zie [een taken reeks maken om een besturings systeem te installeren](create-a-task-sequence-to-install-an-operating-system.md)voor meer informatie.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Alle aan de takenreeks gekoppeld inhoud distribueren

Alle inhoud distribueren die de taken reeks nodig heeft tot ten minste één distributie punt. Deze inhoud bevat de opstart installatie kopie, de installatie kopie van het besturings systeem en andere gekoppelde bestanden. De wizard verzamelt de inhoud van het distributie punt bij het maken van de voor bereide media.

Uw gebruikers account moet ten minste **Lees** rechten hebben voor de inhouds bibliotheek op dat distributie punt. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="hard-drive-on-the-destination-computer"></a>Harde schijf op de doelcomputer

De harde schijf van de doel computer moet zijn geformatteerd voordat de voorgefaseerde media worden toegepast. Als de harde schijf niet is geformatteerd wanneer de media wordt toegepast, mislukt de taken reeks die het besturings systeem implementeert wanneer het de doel computer probeert op te starten.

> [!NOTE]  
> De wizard taken reeks media maken stelt de volgende voor waarde voor de taken reeks variabele in op de media: **_SMSTSMediaType = OEMMedia**. U kunt dezelfde voor waarde in uw taken reeks gebruiken.  


## <a name="process"></a>Proces

 > [!NOTE]  
 > Voor PKI-omgevingen, omdat de basis-CA is opgegeven op de primaire site, moet u ervoor zorgen dat de voorgefaseerde media op de primaire site worden gemaakt. De CAS-site heeft niet de basis-CA-gegevens om de voor bereide media te maken.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer het knoop punt **taken reeksen** .  

2. Klik op het tabblad **Start** van het lint in de groep **maken** op **taken reeks media maken**. Met deze actie wordt de wizard taken reeks media maken gestart.  

3. Geef op de pagina **media type selecteren** de volgende opties op:  

    - Selecteer **Voorbereide media**.  

    - Als u alleen wilt toestaan dat het besturings systeem wordt geïmplementeerd zonder dat er gebruikers invoer is vereist, selecteert u **implementatie van besturings systeem zonder toezicht toestaan**.  

        > [!IMPORTANT]  
        > Wanneer u deze optie selecteert, wordt de gebruiker niet gevraagd om informatie over de netwerk configuratie of voor optionele taken reeksen. Als u de media voor wachtwoord beveiliging configureert, wordt de gebruiker nog steeds gevraagd om een wacht woord.  

4. Geef op de pagina **Media beheer** een van de volgende opties op:  

    - **Dynamische media**: Hiermee staat u toe dat een beheer punt de media omleidt naar een ander beheer punt op basis van de client locatie in de grenzen van de site.  

    - **Op site gebaseerde media**: de media nemen alleen contact op met het opgegeven beheer punt.  

5. Geef op de pagina **media-eigenschappen** de volgende informatie op:  

    - **Gemaakt door**: opgeven wie het medium heeft gemaakt.  

    - **Versie**: het versienummer van het medium opgeven.  

    - **Opmerking**: hier kunt u met een unieke beschrijving aangeven waarvoor het medium wordt gebruikt.  

    - **Mediabestand**: de naam en het pad van de uitvoerbestanden opgeven. De wizard schrijft de uitvoerbestanden naar deze locatie. Bijvoorbeeld: `\\servername\folder\outputfile.wim`  

    - **Tijdelijke map**<!--1359388-->: Voor het maken van media kan veel tijdelijke schijf ruimte nodig zijn. Deze locatie is standaard vergelijkbaar met het volgende pad: `%UserProfile%\AppData\Local\Temp` . Vanaf versie 1902, om u meer flexibiliteit te bieden bij het opslaan van deze tijdelijke bestanden, wijzigt u deze waarde in een ander station en pad.  

6. Geef op de pagina **beveiliging** de volgende opties op:  

    - **Ondersteuning van onbekende computers inschakelen**: de media toestaan om een besturings systeem te implementeren op een computer die niet wordt beheerd door Configuration Manager. Er is geen record van deze computers in de Configuration Manager-Data Base. Zie [voor bereidingen voor onbekende computer implementaties](../get-started/prepare-for-unknown-computer-deployments.md)voor meer informatie.  

    - **Media beveiligen met een wacht woord**: Voer een sterk wacht woord in om de media te beveiligen tegen onbevoegde toegang. Wanneer u een wachtwoord opgeeft, moet de gebruiker dat wachtwoord leveren om de voorbereide media te gebruiken.  

        > [!IMPORTANT]  
        > Wijs, als een beste praktijk op vlak van beveiliging, altijd een wachtwoord toe om te helpen de vooraf geplaatste media te beschermen.  
 
    - Voor HTTP-communicatie selecteert u **zelfondertekend certificaat maken**. Geef vervolgens de begin-en verval datum voor het certificaat op.  
    
        > [!NOTE] 
        > Als u deze optie HTTPS-beheer punten selecteert, zijn niet beschikbaar voor selectie op de pagina **opstart installatie kopie** van deze wizard.

    - Selecteer **PKI-certificaat importeren**voor HTTPS-communicatie. Geef vervolgens het certificaat op dat u wilt importeren en het bijbehorende wacht woord.  

        Zie [PKI-certificaat vereisten](../../core/plan-design/network/pki-certificate-requirements.md)voor meer informatie over dit client certificaat dat wordt gebruikt voor opstart installatie kopieën.  

    - **Affiniteit**Configuration Manager van gebruiker met apparaat: Geef op hoe u wilt dat de media gebruikers aan de doel computer koppelen. Zie [gebruikers koppelen aan een doel computer](../get-started/associate-users-with-a-destination-computer.md)voor meer informatie over hoe de besturingssysteem implementatie de gebruikers affiniteit van het apparaat ondersteunt.  

        - **Affiniteit tussen gebruikers en apparaten toestaan met automatische goed keuring**: de media koppelt automatisch gebruikers aan de doel computer. Deze functionaliteit is gebaseerd op de acties van de taken reeks waarmee het besturings systeem wordt geïmplementeerd. In dit scenario maakt de taken reeks een relatie tussen de opgegeven gebruikers en de doel computer wanneer deze het besturings systeem implementeert op de doel computer.  

        - **Gebruikers affiniteit met apparaat in afwachting van goed keuring van beheerder toestaan**: de media koppelt gebruikers aan de doel computer nadat goed keuring is verleend. Deze functionaliteit is gebaseerd op het bereik van de taken reeks die het besturings systeem implementeert. In dit scenario maakt de taken reeks een relatie tussen de opgegeven gebruikers en de doel computer, maar wordt er gewacht op goed keuring van een gebruiker met beheerders rechten voordat het besturings systeem wordt geïmplementeerd.  

        - **Gebruikers affiniteit met apparaat niet toestaan**: de media koppelt geen gebruikers aan de doel computer. In dit scenario koppelt de taken reeks geen gebruikers aan de doel computer wanneer deze het besturings systeem implementeert.  

7. Selecteer op de pagina **taken reeks** de taken reeks die wordt uitgevoerd op de doel computer. Controleer de lijst met inhoud waarnaar wordt verwezen door de taken reeks.  

    - **Gekoppelde toepassings afhankelijkheden detecteren en toevoegen aan deze media**: Voeg ook inhoud toe aan de media voor toepassings afhankelijkheden.  

        > [!TIP]  
        > Als de verwachte toepassings afhankelijkheden niet worden weer geven, schakelt u deze optie uit om de lijst te vernieuwen.  

8. Geef op de pagina **opstart installatie kopie** de volgende opties op:  

    > [!IMPORTANT]  
    > De architectuur van de opstart installatie kopie die u distribueert, moet geschikt zijn voor de architectuur van de doel computer. Op een x64-doelcomputer kan een x86- of x64-opstartinstallatiekopie worden opgestart en uitgevoerd. Op een x86-doelcomputer kan echter alleen een x86-opstartinstallatiekopie worden opgestart en uitgevoerd.  

    - **Opstart installatie kopie**: Selecteer de opstart installatie kopie om de doel computer te starten.  

    - **Distributie punt**: Selecteer het distributie punt met de opstart installatie kopie. De wizard haalt de opstartinstallatiekopie op van het distributiepunt en schrijft deze naar de media.  

        > [!NOTE]  
        > Uw gebruikers account heeft mini maal **Lees** machtigingen nodig voor de inhouds bibliotheek op het distributie punt.  

    - **Beheer punt**: alleen voor *site-gebaseerde media*selecteert u een beheer punt van een primaire site.  

    - **Gekoppelde beheer punten**: alleen voor *dynamische media*, selecteer de beheer punten van de primaire site die moeten worden gebruikt en een prioriteits volgorde voor de eerste communicatie.  

        > [!NOTE]  
        > Beheer punten met HTTPS-functionaliteit worden alleen weer gegeven wanneer er een PKI-certificaat is opgegeven op de pagina **beveiliging** van deze wizard.  

9. Geef op de pagina **installatie kopieën** de volgende opties op:  

    - **Installatie kopie pakket**: Geef de installatie kopie van het besturings systeem op die moet worden gebruikt. Zie [installatie kopieën van besturings systemen beheren](../get-started/manage-operating-system-images.md)voor meer informatie.  

    - **Afbeeldings index**: als het pakket meerdere installatie kopieën van het besturings systeem bevat, geeft u de index op van de installatie kopie die moet worden geïmplementeerd.  

    - **Distributie punt**: Geef het distributie punt op dat het installatie kopie pakket van het besturings systeem bevat. De wizard haalt de installatie kopie van het besturings systeem op van het distributie punt en schrijft deze naar de media.  

10. Selecteer op de pagina **toepassing selecteren** de optie extra toepassingen om toe te voegen aan het voor bereide Media bestand.  

11. Selecteer op de pagina **pakket selecteren** de optie extra pakketten om toe te voegen aan het voor bereide Media bestand.  

12. Selecteer op de pagina **Stuur programmapakket selecteren** de extra Stuur programmapakketten die u aan het voor bereide Media bestand wilt toevoegen.  

13. Selecteer op de pagina **distributie punten** een of meer distributie punten waarvan u inhoud wilt ophalen.  

    Configuration Manager worden alleen distributie punten met de inhoud weer gegeven. Distribueer alle inhoud die is gekoppeld aan de taken reeks naar ten minste één distributie punt voordat u doorgaat. Nadat u de inhoud hebt gedistribueerd, vernieuwt u de lijst met distributie punten. Verwijder alle distributie punten die u al op deze pagina hebt geselecteerd, gaat u naar de vorige pagina en vervolgens weer terug naar de pagina **distributie punten** . U kunt ook de wizard opnieuw starten. Zie [inhoud distribueren waarnaar wordt verwezen door een taken reeks](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) en [inhoud en infra structuur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)voor inhoud beheren voor meer informatie.  

14. Geef op de pagina **aanpassing** de volgende opties op:  

    - Voeg alle variabelen toe die door de taken reeks worden gebruikt.  

    - **Prestart-opdracht inschakelen**: Geef eventuele prestart-opdrachten op die u wilt uitvoeren voordat de taken reeks wordt uitgevoerd. Prestart-opdrachten bestaan uit een script of een uitvoerbaar bestand dat kan communiceren met de gebruiker in Windows PE voordat de taken reeks wordt uitgevoerd. Zie [prestart-opdrachten voor taken reeks media](../understand/prestart-commands-for-task-sequence-media.md)voor meer informatie.  

        > [!TIP]  
        > Tijdens het maken van de media schrijft de taken reeks de pakket-ID en prestart-opdracht regel, inclusief de waarde voor eventuele taken reeks variabelen, naar het bestand **CreateTSMedia. log** op de computer waarop de Configuration Manager-console wordt uitgevoerd. U kunt dit logboekbestand controleren om de waarde voor de takenreeksvariabelen te verifiëren.  

        Als de prestart-opdracht inhoud vereist, selecteert u de optie voor **het toevoegen van bestanden voor de prestart-opdracht**.  

15. Voltooi de wizard.  


## <a name="next-steps"></a>Volgende stappen

[Een installatiekopie voor een OEM in de fabriek of bij een lokaal depot maken](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)

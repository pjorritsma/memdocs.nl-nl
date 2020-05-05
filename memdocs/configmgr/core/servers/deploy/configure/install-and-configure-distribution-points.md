---
title: Distributie punten beheren
titleSuffix: Configuration Manager
description: Gebruik distributie punten om de inhoud te hosten die u implementeert op apparaten en gebruikers.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1cc931bd0e02be66f608db11e0052fde571a427
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718852"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Distributie punten installeren en configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Installeer Configuration Manager distributie punten om de inhouds bestanden te hosten die u implementeert op apparaten en gebruikers. Maak distributiepunten groepen om te vereenvoudigen hoe u distributie punten beheert en hoe u inhoud distribueert naar distributie punten.  

U *installeert een nieuw distributie punt* met behulp van de installatie wizard. Zie [een distributie punt installeren](#bkmk_install)voor meer informatie. Bewerk de eigenschappen van het distributie punt om *de eigenschappen van een bestaand distributie punt te beheren*. Zie [Configure a Distribution Point (een distributie punt configureren](#bkmk_configs)) voor meer informatie.

Configureer de meeste distributiepunt instellingen met een van beide methoden. Enkele instellingen zijn alleen beschikbaar wanneer u een installatie of bewerking uitvoert, maar niet beide:  

- Instellingen die alleen beschikbaar zijn wanneer u een distributie punt installeert:  

    - **Configuration Manager de installatie van IIS op de distributiepunt computer toestaan**

    - **De instellingen voor de schijf ruimte voor het distributie punt configureren**  

- Instellingen die alleen beschikbaar zijn wanneer u de eigenschappen van een distributie punt bewerkt:  

    - **Relaties van distributiepunt groepen beheren**  

    - **Inhoud weer geven die is geïmplementeerd op het distributie punt**  

    - **Frequentie limieten configureren voor gegevens overdracht naar distributie punten**  

    - **Schema's configureren voor gegevens overdracht naar distributie punten**  


## <a name="install-a-distribution-point"></a><a name="bkmk_install"></a>Een distributie punt installeren  

Kies een site systeem server als een distributie punt voordat de inhoud beschikbaar kan worden gemaakt voor client computers. Wijs een distributie punt toe aan minstens één [grens groep](boundary-groups.md#distribution-points) voordat on-premises client computers dat distributie punt kunnen gebruiken als de locatie van de inhouds bron. Voeg de rol distributie punt toe aan een nieuwe site systeem server of voeg deze toe aan een bestaande site systeem server.

### <a name="prerequisites"></a><a name="bkmk_install-prereq"></a>Vereisten

Wanneer u een nieuw distributie punt installeert, gebruikt u een installatie wizard die u door de beschik bare instellingen leidt. Voordat u begint, moet u rekening houden met de volgende vereisten:  

- U moet de volgende beveiligings machtigingen hebben om een distributie punt te maken en te configureren:  

    - **Lezen** voor het **distributie punt** object  

    - **Kopiëren naar distributie punt** voor het **distributiepunt** object  

    - **Wijzigen** voor het **site** object  

    - **Certificaten beheren voor de implementatie van besturings systemen** voor het **site** -object  

- Installeer Internet Information Services (IIS) op de Windows-Server die als host fungeert voor het distributie punt. Of, wanneer u de site systeemrol installeert, Configuration Manager IIS voor u kunt installeren en configureren.  

### <a name="procedure-to-install-a-distribution-point"></a><a name="bkmk_install-procedure"></a>Procedure voor het installeren van een distributie punt  

Gebruik deze procedure om een nieuw distributie punt toe te voegen. Zie de sectie [een distributie punt configureren](#bkmk_configs) voor meer informatie over het wijzigen van de configuratie van een bestaand distributie punt.  

Begin met de algemene procedure voor het [installeren van site systeem rollen](install-site-system-roles.md). Selecteer de rol **distributie punt** op de pagina **selectie van systeem rollen** van de wizard site systeem server maken. Met deze actie worden de volgende pagina's toegevoegd aan de wizard:  

- [Distributiepunt](#bkmk_config-general)
- [Communicatie](#bkmk_config-comm)
- [Instellingen voor station](#bkmk_config-drive)
- [Pull-distributie punt](#bkmk_config-pull)
- [PXE-instellingen](#bkmk_config-pxe)
- [Cast](#bkmk_config-multicast)
- [Validatie van inhoud](#bkmk_config-valid)
- [Grens groepen](#bkmk_config-boundary)

> [!Important]  
> De volgende instellingen zijn alleen beschikbaar wanneer u een distributie punt installeert:  
>
> - **Configuration Manager de installatie van IIS op de distributiepunt computer toestaan**  
>
> - **De instellingen voor de schijf ruimte voor het distributie punt configureren**  

Zie de sectie [een distributie punt configureren](#bkmk_configs) voor meer informatie over de pagina's van de wizard die specifiek is voor de distributiepunt rol. Als u bijvoorbeeld het distributie punt als een [pull-distributie punt](#bkmk_config-pull)wilt installeren, kiest u de optie om **Dit distributie punt in te scha kelen om inhoud van andere distributie punten op te halen**. Breng vervolgens de aanvullende configuraties voor pull-distributie punten.  

Nadat u de wizard site systeem server maken hebt voltooid, voegt de-site de rol van distributie punt toe aan de site systeem server.  


## <a name="manage-distribution-point-groups"></a><a name="bkmk_manage"></a>Distributiepunt groepen beheren  

Distributiepuntgroepen bieden een logische groepering van distributiepunten voor inhoudsdistributie. Gebruik deze groepen voor het beheren en bewaken van inhoud vanaf een centrale locatie voor distributie punten die meerdere sites omvatten. Houd het volgende punt in acht:

- Voeg een of meer distributie punten toe van elke site in de hiërarchie naar een distributiepunten groep.  

- Een distributie punt toevoegen aan meer dan een distributiepunten groep.  

- Wanneer u inhoud distribueert naar een distributiepunten groep, wordt de inhoud door Configuration Manager gedistribueerd naar alle distributie punten die lid zijn van de groep.  

- Als u een distributie punt toevoegt aan de groep na een initiële inhouds distributie, distribueert Configuration Manager de inhoud automatisch naar het nieuwe lid van het distributie punt.  

- Een verzameling koppelen aan een distributiepunten groep. Wanneer u inhoud distribueert naar die verzameling, bepaalt Configuration Manager welke groepen aan de verzameling zijn gekoppeld. Vervolgens wordt de inhoud gedistribueerd naar alle distributie punten die lid zijn van deze groepen.  

    > [!NOTE]  
    > Wanneer u inhoud naar een verzameling hebt gedistribueerd en u vervolgens de verzameling koppelt aan een nieuwe distributiepunten groep, moet u de inhoud opnieuw distribueren naar de verzameling voordat de inhoud wordt gedistribueerd naar de nieuwe distributiepunt groep.  

De volgende secties bevatten een lijst met de procedures voor de volgende acties voor het beheren van distributiepunt groepen:  

- [Een nieuwe distributiepunten groep maken en configureren](#bkmk_dpgroup-create)
- [Een bestaande distributiepunten groep wijzigen](#bkmk_dpgroup-modify)
- [Geselecteerde distributie punten toevoegen aan bestaande distributiepunten groepen](#bkmk_dpgroup-addexist)

### <a name="procedure-to-create-and-configure-a-new-distribution-point-group"></a><a name="bkmk_dpgroup-create"></a>Procedure voor het maken en configureren van een nieuwe distributiepunten groep  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **distributiepunten groepen** .  

2. Selecteer in het lint **groep maken**.  

3. Voer in het venster nieuwe distributiepunt groep maken de **naam**en eventueel een **Beschrijving** voor de groep in.  

4. Selecteer **toevoegen**op het tabblad **leden** .  

5. Selecteer in het venster distributie punten toevoegen een of meer distributie punten die u wilt toevoegen als leden van de groep. Klik vervolgens op **OK**.  

6. Als dat nodig is, gaat u naar het tabblad **verzamelingen** in het venster nieuwe distributiepunt groep maken en selecteert u **toevoegen**.  

7. Selecteer in het venster verzamelingen selecteren de verzamelingen die u aan de distributiepunten groep wilt koppelen en klik vervolgens op **OK**.  

8. Kies in het venster nieuwe distributiepunt groep maken de optie **OK** om de groep te maken.  

#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Een nieuwe groep maken op basis van een bestaand distributie punt

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **distributie punten** . Selecteer een of meer distributie punten om aan een nieuwe distributiepunten groep toe te voegen.  

2. Selecteer in het lint **geselecteerde items toevoegen**en selecteer vervolgens **geselecteerde items toevoegen aan nieuwe distributiepunten groep**.  

Met dit proces wordt het tabblad **leden** van het venster nieuwe distributiepunt groep maken automatisch ingevuld met de geselecteerde servers.

### <a name="procedure-to-modify-an-existing-distribution-point-group"></a><a name="bkmk_dpgroup-modify"></a>Procedure voor het wijzigen van een bestaande distributiepunten groep  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **distributiepunten groepen** .  

2. Selecteer een bestaande distributiepunten groep die u wilt wijzigen. Selecteer **Eigenschappen**in het lint.  

3. Als u nieuwe verzamelingen wilt koppelen aan deze groep, gaat u naar het tabblad **verzamelingen** en kiest u **toevoegen**. Selecteer de verzamelingen en klik vervolgens op **OK**.  

4. Als u nieuwe distributie punten aan deze groep wilt toevoegen, gaat u naar het tabblad **leden** en klikt u op **toevoegen**. Selecteer de distributie punten en klik vervolgens op **OK**.  

5. Klik op **OK** om de wijzigingen voor de distributiepunten groep op te slaan.  

### <a name="procedure-to-add-selected-distribution-points-to-existing-distribution-point-groups"></a><a name="bkmk_dpgroup-addexist"></a>Procedure voor het toevoegen van geselecteerde distributie punten aan bestaande distributiepunten groepen  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **distributie punten** . Selecteer een of meer distributie punten om aan een bestaande groep toe te voegen.  

2. Selecteer in het lint **geselecteerde items toevoegen**en selecteer vervolgens **geselecteerde items toevoegen aan bestaande distributiepunten groepen**.  

3. Selecteer in de **beschik bare distributiepunten groepen**de groepen waaraan de geselecteerde distributie punten als leden worden toegevoegd. Klik vervolgens op **OK**.  


## <a name="reassign-a-distribution-point"></a><a name="bkmk_reassign"></a>Een distributie punt opnieuw toewijzen

<!-- 1306937 -->

Veel klanten hebben grote Configuration Manager-infra structuren en verlaagt de primaire of secundaire sites om hun omgeving te vereenvoudigen. Ze moeten nog steeds distributie punten op filiaal locaties bewaren voor het leveren van inhoud aan beheerde clients. Deze distributie punten bevatten vaak meerdere terabytes of meer inhoud. Deze inhoud is in bepaalde tijd en netwerk bandbreedte gedistribueerd om naar deze externe servers te distribueren.

Met deze functie kunt u een distributie punt opnieuw toewijzen aan een andere primaire site zonder de inhoud opnieuw te distribueren. Met deze actie wordt de site systeem toewijzing bijgewerkt en wordt alle inhoud op de server bewaard. Als u meerdere distributie punten opnieuw wilt toewijzen, moet u deze actie eerst uitvoeren op één distributie punt. Ga vervolgens één keer door met extra servers.

> [!IMPORTANT]  
> De doel server kan alleen de distributiepuntrol hosten. Als de site systeem server als host fungeert voor een andere Configuration Manager serverrol, zoals het status migratie punt, kunt u het distributie punt niet opnieuw toewijzen. U kunt een Cloud distributiepunt niet opnieuw toewijzen.

Voordat u een distributie punt opnieuw toewijst, moet u het computer account van de doel site server toevoegen aan de lokale beheerders groep op de doel distributiepunt server.

Volg deze stappen om een distributie punt opnieuw toe te wijzen:

1. Maak in de Configuration Manager-console verbinding met de centrale beheer site.  

2. Ga naar de werk ruimte **beheer** en selecteer het knoop punt **distributie punten** .  

3. Klik met de rechter muisknop op het doel distributiepunt en selecteer **distributie punt opnieuw toewijzen**.  

4. Selecteer de doel site server en de site code waaraan u dit distributie punt opnieuw wilt toewijzen.  

Controleer de hertoewijzing op dezelfde manier als bij het toevoegen van een nieuwe rol. De eenvoudigste methode is de weer gave van de console te vernieuwen na enkele minuten. Voeg de kolom site code toe aan de weer gave. Deze waarde verandert wanneer Configuration Manager de server opnieuw toewijst. Als u probeert een andere actie uit te voeren op de doel server voordat u de console weergave vernieuwt, wordt de fout ' object niet gevonden ' weer gegeven. Controleer of het proces is voltooid en vernieuw de weer gave van de console voordat u andere acties op de server start.

Wanneer u een distributie punt opnieuw toewijst, moet u het certificaat van de server vernieuwen. De nieuwe site server moet dit certificaat opnieuw versleutelen met behulp van de open bare sleutel en opslaan in de site database. Zie voor meer informatie het **maken van een zelfondertekend certificaat of het importeren van een PKI-client certificaat (Public Key Infrastructure) voor de distributiepunt** instelling op het tabblad [Algemeen](#bkmk_config-general) van de eigenschappen van het distributie punt.

- Voor PKI-certificaten hoeft u geen nieuw certificaat te maken. Importeer hetzelfde. PFX en voer het wacht woord in.  

- Voor zelfondertekende certificaten past u de verval datum of-tijd aan om deze bij te werken.  

- Als u het certificaat niet vernieuwt, wordt er nog steeds inhoud door het distributie punt gebruikt, maar de volgende functies mislukken:  

    - Verificatie berichten voor inhoud (het distmgr. log geeft aan dat het certificaat niet kan worden ontsleuteld)  

    - PXE-ondersteuning voor clients  

### <a name="tips"></a>Tips

- Voer deze actie uit vanaf de centrale beheer site. Deze procedure helpt bij het repliceren van de primaire sites.  

- Distribueer geen inhoud naar de doel server en probeer deze opnieuw toe te wijzen. Het distribueren van inhouds taken die worden uitgevoerd, kan mislukken tijdens het hertoewijzings proces, maar dit is een nieuwe poging per normaal.  

- Als de server ook een Configuration Manager-client is, moet u ervoor zorgen dat u de client ook opnieuw toewijst aan de nieuwe primaire site. Deze stap is met name van belang voor pull-distributie punten, die client onderdelen gebruiken om inhoud te downloaden.  

- Dit proces verwijdert het distributie punt uit de standaard grens groep van de oude site. U moet deze hand matig toevoegen aan de standaard grens groep van de nieuwe site, indien nodig. Alle andere toewijzingen van grens groepen blijven hetzelfde.  


## <a name="maintenance-mode"></a><a name="bkmk_maint"></a>Onderhouds modus

<!--3555754-->

Vanaf versie 1902 kunt u een distributie punt instellen in de onderhouds modus. Schakel de onderhouds modus in wanneer u software-updates installeert of wijzigingen aanbrengt aan de server.

Terwijl het distributie punt zich in de onderhouds modus bevindt, heeft het het volgende gedrag:

- Er wordt geen inhoud naar de site gedistribueerd.  

- Beheer punten retour neren niet de locatie van dit distributie punt naar clients.

- Wanneer u de site bijwerkt, wordt er nog een distributie punt in de onderhouds modus bijgewerkt.

- De eigenschappen van het distributie punt zijn alleen-lezen. Het is bijvoorbeeld niet mogelijk om het certificaat te wijzigen of grens groepen toe te voegen.  

- Alle geplande taken, zoals inhouds validatie, worden nog steeds uitgevoerd volgens hetzelfde schema.

Ga voorzichtig te werk om de onderhouds modus in te scha kelen op meer dan één distributie punt. Deze actie kan invloed hebben op de prestaties van uw andere distributie punten. Afhankelijk van de configuraties van de grens groep hebben clients mogelijk meer download tijden of kan inhoud niet worden gedownload.

De onderhouds modus mag geen lange termijn status voor een distributie punt zijn. Voor acties met een lange duur moet u eerst de distributiepuntrol verwijderen.

> [!NOTE]
> Terwijl een distributie punt zich in de onderhouds modus bevindt, moet u niet de volgende acties uitvoeren:<!-- SCCMDocs-pr #4699 -->
>
> - Rol verwijderen
> - Distributie punt opnieuw toewijzen

### <a name="enable-maintenance-mode"></a>Onderhoudsmodus inschakelen

Als u een distributie punt in de onderhouds modus wilt plaatsen, moet uw gebruikers account de machtiging **wijzigen** hebben voor de klasse **site** . De ingebouwde rollen **infrastructuur beheerder** en **volledige beheerder** hebben bijvoorbeeld deze machtiging.<!-- SCCMDocs-pr issue #3407 -->

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** .  

2. Selecteer het knoop punt **distributie punten** .  

3. Selecteer het doel distributiepunt en kies **onderhouds modus inschakelen** op het lint.  

Als u de huidige status van de distributie punten wilt weer geven, voegt u de kolom onderhouds modus toe aan het knoop punt **distributie punten** in de-console.

Zie [methode SetDPMaintenanceMode in klasse SMS_DistributionPointInfo](../../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md)voor meer informatie over het automatiseren van dit proces met de SDK van Configuration Manager.


## <a name="configure-a-distribution-point"></a><a name="bkmk_configs"></a>Een distributie punt configureren  

Individuele distributie punten bieden ondersteuning voor verschillende configuraties. Niet alle typen distributie punten ondersteunen echter alle configuraties. Distributie punten in de Cloud bieden bijvoorbeeld geen ondersteuning voor PXE-of multi cast-implementaties. Raadpleeg de volgende artikelen voor meer informatie over specifieke beperkingen:  

- [Een Cloud distributiepunt gebruiken](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- [Een pull-distributiepunt gebruiken](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)  

In de volgende secties worden de configuratie van het distributie punt beschreven wanneer u [een nieuwe installeert](#bkmk_install-procedure) of [een bestaand item bewerkt](#bkmk_change-procedure):  

- [Algemene instellingen](#bkmk_config-general)
- [Communicatie](#bkmk_config-comm)
- [Instellingen voor station](#bkmk_config-drive)
- [Firewall instellingen](#bkmk_firewall)
- [Pull-distributie punt](#bkmk_config-pull)
- [PXE-instellingen](#bkmk_config-pxe)
- [Cast](#bkmk_config-multicast)
- [Validatie van inhoud](#bkmk_config-valid)
- [Grens groepen](#bkmk_config-boundary)

#### <a name="procedure-to-change-a-distribution-point"></a><a name="bkmk_change-procedure"></a>Procedure voor het wijzigen van een distributie punt

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **distributie punten** .  

2. Selecteer het distributie punt dat u wilt configureren. Kies **Eigenschappen**in het lint.  

3. Gebruik de informatie in de volgende secties wanneer u de eigenschappen van het distributie punt bewerkt.  

4. Nadat u de gewenste wijzigingen hebt aangebracht, selecteert u **OK** om uw instellingen op te slaan en de eigenschappen van het distributie punt te sluiten.  

### <a name="general"></a><a name="bkmk_config-general"></a>Algemene  

> [!Note]  
> In versie 1902 en eerder heeft deze pagina extra instellingen voor HTTP/HTTPS en certificaten. Vanaf versie 1906 zijn deze instellingen nu op de [communicatie](#bkmk_config-comm) pagina.

De volgende instellingen bevinden zich op de pagina **distributie punt** van de wizard site systeem server maken en op het tabblad **Algemeen** van het venster Eigenschappen van distributie punt:  

- **Beschrijving**: een optionele beschrijving voor deze distributiepunten rol.  

- **Installeer en CONFIGUREER IIS indien vereist door Configuration Manager**: als IIS niet al is geïnstalleerd op de server, wordt het door Configuration Manager geïnstalleerd en geconfigureerd. Configuration Manager vereist IIS op alle distributie punten. Als u deze instelling niet kiest en IIS niet is geïnstalleerd op de server, moet u eerst IIS installeren voordat Configuration Manager het distributie punt kan installeren.  

    > [!NOTE]  
    > Deze optie bevindt zich alleen op de pagina **distributie punt** van de wizard site systeem server maken. Het is alleen beschikbaar wanneer u [een nieuw distributie punt installeert](#bkmk_install-procedure).  

- **BranchCache voor dit distributie punt inschakelen en configureren**: Kies deze instelling als u wilt Configuration Manager Windows BranchCache op de distributiepunt server kunt configureren. Zie [BranchCache](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)voor meer informatie.  

- **De download snelheid aanpassen om de ongebruikte netwerk bandbreedte te gebruiken (Windows LEDBAT)**<!--1358112-->: Vanaf versie 1806 kunnen distributie punten gebruikmaken van het beheer van congestie van het netwerk. Zie [Windows LEDBAT](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat)voor meer informatie. Minimale vereisten voor LEDBAT-ondersteuning:<!-- SCCMDocs issue 883 -->  

    - Configuration Manager versie 1806 (algemene versie)  

        - Windows Server, versie 1709 of hoger  

    - Configuration Manager versie 1806 met update pakket (4462978) of hoger  

        - Windows Server, versie 1709 of hoger
        - Windows Server 2016 met updates KB4132216 en KB4284833

    - Configuration Manager versie 1810 of hoger:

        - Windows Server, versie 1709 of hoger
        - Windows Server 2016 met updates KB4132216 en KB4284833
        - Windows Server 2019  

- **Dit distributie punt inschakelen voor voor bereide inhoud**: met deze instelling kunt u inhoud toevoegen aan de server voordat u software distribueert. Omdat de inhouds bestanden al in de inhouds bibliotheek staan, worden ze niet via het netwerk overgedragen wanneer u de software distribueert. Zie voor [bereide inhoud](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent)voor meer informatie.  

- **Dit distributie punt kan worden gebruikt als micro soft Connected cache server**: vanaf versie 1906 kunt u een micro soft Connected cache-server installeren op uw distributie punten. Door deze inhoud on-premises in de cache te plaatsen, kunnen uw clients profiteren van de functie voor Delivery Optimization, maar kunt u WAN-koppelingen helpen beveiligen. Zie voor meer informatie, inclusief een beschrijving van de aanvullende instellingen, [micro soft Connected cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).


### <a name="communication"></a><a name="bkmk_config-comm"></a>Verbindings

> [!Note]  
> Vanaf versie 1906 zijn de volgende instellingen op het tabblad **communicatie** . In versie 1902 en eerder zijn deze instellingen te vinden op het tabblad [Algemeen](#bkmk_config-general) .

De volgende instellingen bevinden zich op de pagina **communicatie** van de wizard site systeem server maken en het venster Eigenschappen van distributie punt:  

- **Configureren hoe client apparaten met het distributie punt communiceren**: er zijn voor delen en nadelen voor het gebruik van **http** of **https**. Zie [aanbevolen beveiligings procedures voor inhouds beheer](../../../plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement)voor meer informatie.  

- **Clients toestaan anoniem verbinding te maken: met**deze instelling geeft u op of het distributie punt anonieme verbindingen van Configuration Manager clients met de inhouds bibliotheek toestaat.  

<!-- I don't think this applies any more, but commenting instead of removing just in case.
    > [!Important]  
    > If you don't use this setting, apply the changes described in Microsoft Knowledge Base article [2619572](https://support.microsoft.com/help/2619572/) on Windows 7 clients. Otherwise repair of Windows Installer applications can fail.  
    >
    > When you deploy a Windows Installer application, the Configuration Manager client downloads the file to its local cache. The client eventually removes the files after the installation finishes. The Configuration Manager client updates the Windows Installer source list for the application. It sets the content path to the content library on associated distribution points. Later, if you try to repair the application on the device, MSIExec attempts to access the content path by using an anonymous user.  
    >
    > After you install the update on clients and modify the documented registry key, MSIExec accesses the content path by using the signed-in user account.  
 -->

- **Een zelfondertekend certificaat maken of een PKI-client certificaat importeren**: Configuration Manager gebruikt dit certificaat voor de volgende doel einden:  

    - Het distributie punt wordt geverifieerd naar een beheer punt voordat het distributie punt status berichten verzendt.  

    - Wanneer u **PXE-ondersteuning voor clients inschakelt** op de pagina **PXE-instellingen** , verzendt het distributie punt het naar computers die PXE-opstart. Deze computers gebruiken deze vervolgens om verbinding te maken met een beheer punt tijdens het implementatie proces van het besturings systeem.  

    Wanneer u al uw beheer punten in de site voor HTTP configureert, selecteert u de optie voor het maken van een **zelfondertekend certificaat**. Wanneer u de beheer punten voor HTTPS configureert, gebruikt u de optie voor het importeren van het **certificaat** uit de PKI.  

    Als u het certificaat wilt importeren, bladert u naar een geldig PKCS #12-bestand (Public Key Cryptography Standard). Dit PFX-of CER-bestand heeft het PKI-certificaat met de volgende vereisten voor Configuration Manager:  

    - Het beoogde gebruik omvat client verificatie  

    - De persoonlijke sleutel exporteren inschakelen  

    > [!TIP]  
    > Er zijn geen specifieke vereisten voor het onderwerp van het certificaat of de alternatieve naam voor het onderwerp (SAN). Gebruik, indien nodig, hetzelfde certificaat voor meerdere distributie punten.  

    Zie [PKI-certificaat vereisten](../../../plan-design/network/pki-certificate-requirements.md)voor meer informatie over de certificaat vereisten.  

    Zie [het client certificaat voor distributie punten implementeren](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)voor een voorbeeld implementatie van dit certificaat.  

### <a name="drive-settings"></a><a name="bkmk_config-drive"></a>Instellingen voor station  

> [!NOTE]  
> Deze opties zijn alleen beschikbaar wanneer u een nieuw distributie punt installeert.  

Geef de instellingen voor het station op voor het distributie punt. Configureer Maxi maal twee schijf stations voor de inhouds bibliotheek en twee schijf stations voor de pakket share. Configuration Manager kunt extra schijven gebruiken wanneer de eerste twee de geconfigureerde schijf ruimte reserveren. De pagina **station-instellingen** configureert de prioriteit voor de schijf stations en de hoeveelheid vrije schijf ruimte die op elk schijf station blijft.  

- **Gereserveerde ruimte op station (MB)**: deze waarde bepaalt de hoeveelheid beschik bare ruimte op een station voordat Configuration Manager een ander station kiest en het kopieer proces doorloopt naar dat station. Inhoudsbestanden kunnen meerdere stations omvatten.  

- **Inhouds locaties**: Geef de locaties op voor de inhouds bibliotheek en pakket share op dit distributie punt. Standaard zijn alle inhouds locaties ingesteld op **automatisch**. Configuration Manager kopieert inhoud naar de primaire inhouds locatie totdat de hoeveelheid beschik bare ruimte de waarde bereikt die is opgegeven voor **gereserveerde ruimte op station (MB)**. Wanneer u **automatisch**selecteert, stelt Configuration Manager de primaire inhouds locaties in op het schijf station met de meeste schijf ruimte tijdens de installatie. De secundaire locaties worden ingesteld op het schijf station met de seconde van de meeste vrije schijf ruimte. Wanneer de primaire en secundaire locaties de reserve ring van de schijf ruimte bereiken, Configuration Manager een andere beschik bare schijf selecteren met de meeste vrije schijf ruimte om het kopieer proces voort te zetten.  

> [!Tip]  
> Als u wilt voor komen dat Configuration Manager op een specifiek station installeert, maakt u een leeg bestand met de naam **no_sms_on_drive. SMS** en kopieert u het naar de hoofdmap van het station voordat u het distributie punt installeert.  

Zie [de inhouds bibliotheek](../../../plan-design/hierarchy/the-content-library.md)voor meer informatie.

### <a name="firewall-settings"></a><a name="bkmk_firewall"></a>Firewall instellingen

Het distributie punt moet de volgende regels voor binnenkomend verkeer hebben dat is geconfigureerd in Windows Firewall:

- Windows Management Instrumentation (DCOM-in)
- Windows Management Instrumentation (WMI-in)

Zonder deze regels ontvangen clients fout 0x801901F4 in bestand datatransferservice. log bij het downloaden van inhoud.

### <a name="pull-distribution-point"></a><a name="bkmk_config-pull"></a>Pull-distributie punt  

Wanneer u **Dit distributie punt inschakelt om inhoud te halen van andere distributie punten**, wordt het een pull-distributie punt. U kunt het gedrag wijzigen van de manier waarop het distributie punt de inhoud die u distribueert, ontvangt. Zie [een pull-distributie punt gebruiken](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)voor meer informatie.

Geef voor elk pull-distributie punt dat u configureert een of meer bron distributiepunten op waarvan de inhoud wordt opgehaald:  

- Kies **toevoegen**en selecteer vervolgens een of meer van de beschik bare distributie punten als bronnen.  

- Gebruik de pijl knoppen om de prioriteit aan te passen. Wanneer het pull-distributie punt inhoud probeert over te dragen, is de prioriteit de volg orde waarin deze contact opneemt met de bron distributiepunten. Eerst neemt de distributie punten contact op met de laagste waarde.  

### <a name="pxe"></a><a name="bkmk_config-pxe"></a>PXE  

Geef op of PXE moet worden ingeschakeld op het distributie punt. PXE gebruiken om besturingssysteem implementaties op clients te starten. Zie [PXE gebruiken om Windows via het netwerk te implementeren](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie over het gebruik van pxe in Configuration Manager.

Wanneer u PXE inschakelt, installeert Configuration Manager Windows Deployment Services (WDS) op de server, indien nodig. WDS is de service die de PXE-opstart bewerking uitvoert om besturings systemen te installeren. Nadat u de wizard hebt voltooid voor het maken van het distributie punt, wordt door Configuration Manager een provider in WDS geïnstalleerd die de PXE-opstart functies gebruikt.

Vanaf versie 1806 kunt u PXE inschakelen op een distributie punt zonder WDS.

Selecteer de optie om **PXE-ondersteuning voor clients in te scha kelen**en configureer vervolgens de volgende instellingen:  

> [!Note]  
> Selecteer **Ja** in het dialoog venster **vereiste poorten voor PXE controleren** om te bevestigen dat u PXE wilt inschakelen. Configuration Manager configureert automatisch de standaard poorten op Windows Firewall. Als u een andere firewall gebruikt, moet u de poorten hand matig configureren.  
>
> Als u WDS en DHCP op dezelfde server installeert, moet u WDS configureren om op een andere poort te Luis teren. DHCP luistert standaard op dezelfde poort. Zie [Overwegingen wanneer u WDS en DHCP op dezelfde server uitvoert](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP)voor meer informatie.  

- **Dit distributie punt toestaan te reageren op binnenkomende PXE-aanvragen**: Geef op of WDS moet reageren op PXE-service aanvragen. Gebruik deze instelling om de service in en uit te scha kelen zonder de PXE-functionaliteit van het distributie punt te verwijderen.  

- **Ondersteuning van onbekende computers inschakelen**: Geef op of ondersteuning moet worden ingeschakeld voor computers die Configuration Manager niet worden beheerd. Zie [voor bereidingen voor onbekende computer implementaties](../../../../osd/get-started/prepare-for-unknown-computer-deployments.md)voor meer informatie.  

- **Een PXE-Responder inschakelen zonder Windows Deployment-service**: vanaf versie 1806 wordt met deze optie een PXE-responder op het distributie punt ingeschakeld waarvoor WDS niet is vereist. Deze PXE-responder ondersteunt IPv6-netwerken. Als u deze optie inschakelt op een distributie punt dat al met PXE is ingeschakeld, wordt de WDS-service door Configuration Manager onderbroken. Als u deze optie uitschakelt, maar **PXE-ondersteuning voor clients wel inschakelt**, schakelt het distributie punt WDS opnieuw in.<!--1357580-->  

    > [!Note]  
    > In versie 1810 en lager wordt het niet ondersteund om de PXE-responder te gebruiken zonder WDS op servers waarop ook een DHCP-server wordt uitgevoerd.
    >
    > Vanaf versie 1902, wanneer u een PXE-responder inschakelt op een distributie punt zonder Windows Deployment-service, kan het zich nu op dezelfde server bevinden als de DHCP-service. <!--3734270-->  

- **Wacht woord vereisen wanneer computers PXE gebruiken**: Geef een sterk wacht woord op om extra beveiliging te bieden voor uw PXE-implementaties.  

- **Gebruikers affiniteit apparaat**: Geef op hoe het distributie punt gebruikers moet koppelen aan de doel computer voor PXE-implementaties. Kies een van de volgende opties:  

  - **Affiniteit tussen gebruikers en apparaten toestaan met automatische goed keuring**: Kies deze instelling om gebruikers automatisch te koppelen aan de doel computer zonder te hoeven wachten op goed keuring.  

  - **Gebruikers affiniteit met apparaat in afwachting van goed keuring van beheerder toestaan**: Kies deze instelling als u wilt wachten op goed keuring van een gebruiker met beheerders rechten voordat gebruikers aan de doel computer zijn gekoppeld.  

  - **Gebruikers affiniteit met apparaat niet toestaan**: Kies deze instelling om op te geven dat gebruikers niet aan de doel computer zijn gekoppeld. Dit is de standaardinstelling.  

    Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie over gebruikers affiniteit met apparaat.  

- **Netwerk interfaces**: Geef op dat het distributie punt reageert op PXE-aanvragen van alle netwerk interfaces of van specifieke netwerk interfaces. Als het distributie punt reageert op specifieke netwerk interfaces, geeft u voor elke netwerk interface het MAC-adres op.  

    > [!Note]  
    > Wanneer u de netwerk interface wijzigt, start u de WDS-service opnieuw om er zeker van te zijn dat de configuratie correct wordt opgeslagen. Start in versie 1806, wanneer de PXE-responder-service wordt gebruikt, de **CONFIGMGR PXE responder-service** (SccmPxe) opnieuw.<!--SCCMDocs issue 642-->  

- **Geef de reactie vertraging van de PXE-server op (seconden)**: als u meerdere PXE-servers gebruikt, geeft u op hoelang dit distributie punt met PXE-functionaliteit moet wachten voordat het op computer aanvragen reageert. Standaard reageert het Configuration Manager distributie punt met PXE-functionaliteit direct.  

### <a name="multicast"></a><a name="bkmk_config-multicast"></a>Cast  

Geef op of multi cast moet worden ingeschakeld op het distributie punt. Multi cast-implementaties besparen netwerk bandbreedte door gegevens gelijktijdig te verzenden naar meerdere Configuration Manager-clients. Zonder multi cast verzendt de server een kopie van de gegevens naar elke client via een afzonderlijke verbinding. Zie [multi cast gebruiken om Windows via het netwerk te implementeren](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)voor meer informatie over het gebruik van multi cast voor implementatie van het besturings systeem.

Wanneer u multi cast inschakelt, installeert Configuration Manager Windows Deployment Services (WDS) op de server, indien nodig.  

Selecteer de optie om **multi cast in te scha kelen om gelijktijdig gegevens te verzenden naar meerdere clients**en configureer vervolgens de volgende instellingen:  

- **Multicast verbindings account**: Geef het account op dat moet worden gebruikt wanneer u Configuration Manager database verbindingen configureert voor multi cast. Zie voor meer informatie het [multi cast-verbindings account](../../../plan-design/hierarchy/accounts.md#multicast-connection-account).  

- **Instellingen voor multi cast-adressen**: Geef de IP-adressen op voor het verzenden van gegevens naar de doel computers. Standaard wordt het IP-adres opgehaald van een DHCP-server die is ingeschakeld voor het distribueren van multi cast-adressen. Afhankelijk van de netwerk omgeving, kunt u een bereik van IP-adressen van 239.0.0.0 tot en met 239.255.255.255 opgeven.  

    > [!IMPORTANT]  
    > De IP-adressen die u configureert, moeten toegankelijk zijn voor de doel computers die de installatie kopie van het besturings systeem aanvragen. Controleer of routers en firewalls multicast verkeer tussen de doel computer en het distributie punt toestaan.  

- **UDP-poort bereik voor multi cast**: Geef het bereik van UDP-poorten op die worden gebruikt voor het verzenden van gegevens naar de doel computers.  

    > [!IMPORTANT]  
    > De UDP-poorten moeten toegankelijk zijn voor de doel computers die de installatie kopie van het besturings systeem aanvragen. Controleer of routers en firewalls multicast verkeer tussen de doel computer en de site server toestaan.  

- **Maximum aantal clients**: Hiermee geeft u op hoeveel doel computers de installatie kopie van het besturings systeem vanaf dit distributie punt kunnen downloaden.  

- **Geplande multi cast inschakelen**: Geef op hoe Configuration Manager bepaalt wanneer het implementeren van besturings systemen op doel computers wordt gestart. Configureer de volgende opties:  

    - **Start vertraging van sessie (minuten)**: Geef het aantal minuten op dat Configuration Manager wacht voordat de eerste implementatie aanvraag wordt beantwoord.  

    - **Minimale sessie grootte (clients)**: Geef op hoeveel aanvragen er moeten worden ontvangen voordat Configuration Manager begint met de implementatie van het besturings systeem.  

> [!IMPORTANT]  
> Vanaf versie 1806, om multi cast in te scha kelen en te configureren op het tabblad **multi cast** van de eigenschappen van het distributie punt, moet het distributie punt gebruikmaken van de Windows Deployment-service.  
>
> - Als u **PXE-ondersteuning voor clients inschakelt** en multi cast inschakelt **om gelijktijdig gegevens te verzenden naar meerdere clients**, kunt u geen **PXE-Responder inschakelen zonder Windows Deployment service**.  
>
> - Als u **PXE-ondersteuning voor clients inschakelt** en **een PXE-responder zonder Windows Deployment service**inschakelt, kunt u **multi cast niet inschakelen om gelijktijdig gegevens te verzenden naar meerdere clients**  

### <a name="group-relationships"></a><a name="bkmk_config-group"></a>Groeps Relaties  

> [!NOTE]  
> Deze opties zijn alleen beschikbaar wanneer u de eigenschappen van een eerder geïnstalleerd distributie punt bewerkt.  

Beheer de distributiepunten groepen waarvan dit distributie punt lid is.  

Als u dit distributie punt als een lid wilt toevoegen aan een bestaande distributiepunten groep, kiest u **toevoegen**. Selecteer in het venster groepen van distributie punt toevoegen een bestaande groep en kies vervolgens **OK**.  

Als u dit distributie punt uit een distributiepunten groep wilt verwijderen, selecteert u de groep in de lijst en kiest u vervolgens **verwijderen**. Als u het distributie punt uit een distributiepunten groep verwijdert, wordt de inhoud van het distributie punt niet verwijderd.

### <a name="content"></a><a name="bkmk_config-content"></a>Inhoudbeheer  

> [!NOTE]  
> Deze opties zijn alleen beschikbaar wanneer u de eigenschappen van een eerder geïnstalleerd distributie punt bewerkt.  

De inhoud beheren die u hebt gedistribueerd naar het distributie punt. Selecteer in de lijst met implementatie pakketten en voer de volgende acties uit:  

- **Valideren**: start het proces om de integriteit van de inhouds bestanden voor de software te valideren. Als u de resultaten van het proces voor het valideren van inhoud wilt weer geven, vouwt u in de werk ruimte **bewaking** **distributie status**uit en kiest u vervolgens het knoop punt **inhouds status** . Zie [inhoud valideren](deploy-and-manage-content.md#validate-content)voor meer informatie.  

- Opnieuw **distribueren**: kopieert alle inhouds bestanden voor de geselecteerde software naar het distributie punt en overschrijft de bestaande bestanden. Normaal gesp roken gebruikt u deze actie om inhouds bestanden te herstellen. Zie [inhoud opnieuw distribueren](deploy-and-manage-content.md#redistribute-content)voor meer informatie.  

- **Verwijderen**: Hiermee verwijdert u de inhouds bestanden voor de software van het distributie punt. Zie [inhoud verwijderen](deploy-and-manage-content.md#remove-content)voor meer informatie.  

### <a name="content-validation"></a><a name="bkmk_config-valid"></a>Validatie van inhoud  

Stel een planning in om de integriteit van inhouds bestanden op het distributie punt te valideren. Wanneer u inhouds validatie op een planning inschakelt, wordt Configuration Manager het proces op het geplande tijdstip gestart. Hiermee wordt alle inhoud op het distributie punt gecontroleerd op basis van de lokale SMS_PackagesInContLib SCCMDP-klasse. U kunt ook de prioriteit van de inhouds validatie configureren. De prioriteit is standaard ingesteld op **laagste**. Het verhogen van de prioriteit kan het processor-en schijf gebruik tijdens het validatie proces verg Roten op de server, maar dit wordt sneller uitgevoerd.

Als u de resultaten van het proces voor het valideren van inhoud wilt weer geven, vouwt u in de werk ruimte **bewaking** **distributie status**uit en kiest u vervolgens het knoop punt **inhouds status** . Hierin wordt de inhoud voor elk software type weer gegeven, bijvoorbeeld toepassing, software-update pakket en opstart installatie kopie.  

> [!WARNING]  
> Hoewel u het schema voor de inhouds validatie opgeeft met behulp van de lokale tijd voor de computer, toont de Configuration Manager-console het schema in UTC.  

Zie [inhoud valideren](deploy-and-manage-content.md#validate-content)voor meer informatie.

### <a name="boundary-groups"></a><a name="bkmk_config-boundary"></a>Grens groepen  

Beheer de grens groepen waaraan u dit distributie punt toewijst. Voeg het distributie punt toe aan ten minste één grens groep. Tijdens de implementatie van inhoud moeten clients zich in een grens groep bevindt die is gekoppeld aan een distributie punt om dat distributie punt als bron locatie voor inhoud te gebruiken.

Configureer grens groeps *relaties* die definiëren wanneer en aan welke grens groepen een client kan terugvallen om inhoud te zoeken. Zie [grens groepen](boundary-groups.md)voor meer informatie.

Kies **toevoegen** en selecteer een bestaande grens groep in de lijst.

Kies **maken**om een nieuwe grens groep te maken voor dit distributie punt. Zie [procedures voor grens groepen](boundary-group-procedures.md)voor meer informatie over het maken en configureren van een grens groep.

Wanneer u de eigenschappen van een eerder geïnstalleerd distributie punt bewerkt, beheert u de optie om **in te scha kelen voor distributie op aanvraag**. Met deze optie kan Configuration Manager automatisch inhoud naar deze server distribueren wanneer een client deze aanvraagt. Zie [inhoud distribueren op aanvraag](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution)voor meer informatie.

### <a name="schedule"></a><a name="bkmk_config-sched"></a>Planning  

> [!NOTE]  
> Deze opties zijn alleen beschikbaar wanneer u de eigenschappen van een eerder geïnstalleerd distributie punt bewerkt.
>
> Dit tabblad is alleen beschikbaar wanneer u de eigenschappen bewerkt van een distributie punt dat zich op afstand van de site server bevindt.  

Configureer een planning die beperkt wanneer Configuration Manager gegevens kan overdragen naar het distributie punt. Gegevens beperken op basis van prioriteit of de verbinding voor geselecteerde tijds perioden sluiten.

Als u de gegevens wilt beperken, selecteert u de tijds periode in het raster en kiest u een van de volgende instellingen voor **Beschik baarheid**:  

- **Open voor alle prioriteiten**: Configuration Manager verzendt gegevens naar het distributie punt zonder beperkingen. Deze instelling is de standaard waarde voor alle tijds perioden.  

- **Gemiddelde en hoge prioriteit toestaan**: Configuration Manager alleen gegevens met een gemiddelde en hoge prioriteit naar het distributie punt verzendt.  

- **Alleen hoge prioriteit toestaan**: Configuration Manager alleen gegevens met hoge prioriteit naar het distributie punt verzendt.  

- **Gesloten**: Configuration Manager verzendt geen gegevens naar het distributie punt.  

Configureer de **distributie prioriteit** van software op het tabblad **distributie-instellingen** van de eigenschappen van de software.

> [!IMPORTANT]  
> De planning is gebaseerd op de tijd zone van de verzendende site, niet het distributie punt.  

### <a name="rate-limits"></a><a name="bkmk_config-rate"></a>Frequentie limieten  

> [!NOTE]  
> Deze opties zijn alleen beschikbaar wanneer u de eigenschappen van een eerder geïnstalleerd distributie punt bewerkt.  
>
> Dit tabblad is alleen beschikbaar wanneer u de eigenschappen bewerkt van een distributie punt dat zich op afstand van de site server bevindt.  

Configureer frequentie limieten om de netwerk bandbreedte te beheren die Configuration Manager gebruikt om inhoud over te dragen naar het distributie punt. Kies uit de volgende opties:  

- **Onbeperkt bij het verzenden naar deze bestemming**: Configuration Manager verzenden van inhoud naar het distributie punt zonder beperkingen voor frequentie limieten. Dit is de standaardinstelling.  

- **Pulse-modus**: met deze optie geeft u de grootte van de gegevens blokken op die door de site server naar het distributie punt worden verzonden. U kunt daarnaast een vertraging tussen het verzenden van de afzonderlijke gegevensblokken opgeven. Gebruik deze optie wanneer u gegevens via een netwerk verbinding met een lage band breedte naar het distributie punt moet verzenden. Zo hebt u beperkingen voor het verzenden van 1 KB aan gegevens elke vijf seconden, ongeacht de snelheid van de koppeling of het gebruik ervan op een bepaald moment.  

- **Beperkt tot opgegeven maximale overdrachts snelheid per uur**: Stel deze instelling in om een site gegevens te laten verzenden naar een distributie punt door alleen het percentage tijd te gebruiken dat u configureert. Wanneer u deze optie gebruikt, identificeert Configuration Manager niet de beschik bare band breedte van het netwerk. In plaats daarvan wordt de tijd gedeeld waarop gegevens kunnen worden verzonden. De server verzendt gegevens gedurende korte tijd, gevolgd door Peri Oden waarin geen gegevens worden verzonden. Als u bijvoorbeeld de **beschik bare band breedte beperkt** tot **50%** instelt, verzendt Configuration Manager gegevens voor een bepaalde periode, gevolgd door een periode waarin er geen gegevens worden verzonden. De werkelijke hoeveelheid gegevens, of de grootte van het gegevens blok, wordt niet beheerd. Het beheert alleen de hoeveelheid tijd waarin gegevens worden verzonden.  

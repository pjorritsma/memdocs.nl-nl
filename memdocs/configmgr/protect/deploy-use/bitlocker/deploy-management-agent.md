---
title: BitLocker-beleid implementeren
titleSuffix: Configuration Manager
description: De BitLocker-beheer agent implementeren voor het Configuration Manager van clients en de herstel service naar beheer punten
ms.date: 07/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ba72e9accb7cbc5a7dc1149c6c9d947cb3e0692b
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2020
ms.locfileid: "87526080"
---
# <a name="deploy-bitlocker-management"></a>BitLocker-beleid implementeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3601034-->

BitLocker-beheer in Configuration Manager omvat de volgende onderdelen:

- **BitLocker-beheer agent**: Configuration Manager maakt deze agent op een apparaat mogelijk wanneer u [een beleid maakt](#create-a-policy) en [implementeert in een verzameling](#deploy-a-policy).

- **Recovery-service**: het Server onderdeel dat BitLocker-herstel gegevens ontvangt van clients. Zie [Recovery service](#recovery-service)(Engelstalig) voor meer informatie.

Voordat u het beleid voor BitLocker-beheer maakt en implementeert:

- De [vereisten](../../plan-design/bitlocker-management.md#prerequisites) controleren

- Als dat nodig is, [versleutelt u de herstel sleutels](encrypt-recovery-data.md) in de site database

## <a name="create-a-policy"></a>Beleid maken

Wanneer u dit beleid maakt en implementeert, schakelt de Configuration Manager-client de BitLocker-beheer agent op het apparaat in.

> [!NOTE]
> Als u een beheer beleid voor BitLocker wilt maken, moet u de rol **volledige beheerder** hebben in Configuration Manager.

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **Endpoint Protection**uit en selecteer het knoop punt **BitLocker-beheer** .

1. Selecteer in het lint **BitLocker-beheer beheer beleid maken**.

1. Geef op de pagina **Algemeen** een naam en een optionele beschrijving op. Selecteer de onderdelen om in te scha kelen op clients met dit beleid:  

    - **Besturingssysteem station**: beheren of het station van het besturings systeem is versleuteld

    - **Vast station**: versleuteling voor extra gegevens stations op een apparaat beheren

    - **Verwisselbaar station**: versleuteling beheren voor stations die u kunt verwijderen van een apparaat, zoals een USB-sleutel

    - **Client beheer**: de back-up van de sleutel herstel service van BitLocker-stationsversleuteling herstel gegevens beheren  

1. Configureer op de pagina **Setup** de volgende algemene instellingen voor BitLocker-stationsversleuteling:

    > [!NOTE]
    > Configuration Manager deze instellingen Toep assen wanneer u BitLocker inschakelt. Als het station al is versleuteld of wordt uitgevoerd, wordt de versleuteling van het station op het apparaat niet gewijzigd door wijzigingen in deze beleids instellingen.
    >
    > Als u deze instellingen uitschakelt of niet configureert, gebruikt BitLocker de standaard versleutelings methode (AES 128-bits).

    - Schakel voor Windows 8,1-apparaten de optie voor de **methode voor stationsversleuteling en**de codeer sterkte in. Selecteer vervolgens de versleutelings methode.

    - Schakel voor Windows 10-apparaten de optie voor de **versleutelings methode voor stations en de codeer sterkte in (Windows 10)**. Selecteer vervolgens de versleutelings methode voor OS-stations, harde schijven en verwissel bare gegevens stations afzonderlijk.

    Zie [instellingen referentie-Setup](../../tech-ref/bitlocker/settings.md#setup)voor meer informatie over deze en andere instellingen op deze pagina.

1. Geef op de pagina station van het **besturings systeem** de volgende instellingen op:  

    - **Versleutelings instellingen voor het besturings systeem station**: als u deze instelling inschakelt, moet de gebruiker het OS-station beveiligen en BitLocker versleutelt het station. Als u deze optie uitschakelt, kan de gebruiker het station niet beveiligen.  

    Op apparaten met een compatibele TPM kunnen tijdens het opstarten twee typen verificatie methoden worden gebruikt om extra beveiliging te bieden voor versleutelde gegevens. Wanneer de computer wordt gestart, kan deze alleen de TPM voor verificatie gebruiken, of kan de vermelding van een persoonlijk identificatie nummer (pincode) ook vereist zijn. Configureer de volgende instellingen:

    - **Selecteer beveiliging voor het station van het besturings systeem**: Configureer dit voor het gebruik van een TPM en pincode, of alleen voor de TPM.

    - **Minimale lengte voor pincodes configureren voor opstarten**: als u een pincode nodig hebt, is deze waarde de kortste lengte die de gebruiker kan opgeven. De gebruiker voert deze pincode in wanneer de computer opstart om het station te ontgrendelen. De minimale lengte van de pincode is standaard `4` .

    Zie [instellingen referentie-OS station](../../tech-ref/bitlocker/settings.md#os-drive)voor meer informatie over deze en andere instellingen op deze pagina.

1. Geef op de pagina **vast station** de volgende instellingen op:

    - **Versleuteling van het vaste gegevens station**: als u deze instelling inschakelt, moeten gebruikers van BitLocker alle vaste-gegevens stations onder beveiliging plaatsen. Vervolgens worden de gegevens stations versleuteld. Wanneer u dit beleid inschakelt, schakelt u automatisch ontgrendelen of de instellingen voor het **wachtwoord beleid vaste gegevens schijf**in.

    - **Automatisch ontgrendelen configureren voor harde schijf**: het versleutelde gegevens station toestaan of vereisen dat BitLocker automatisch wordt ontgrendeld. Als u automatisch ontgrendelen wilt gebruiken, moet BitLocker ook het station van het besturings systeem versleutelen.

    Zie voor meer informatie over deze en andere instellingen op deze pagina [instellingen referentie-vast station](../../tech-ref/bitlocker/settings.md#fixed-drive).

1. Geef op de pagina **Verwissel bare schijf** de volgende instellingen op:

    - **Versleuteling van Verwissel bare gegevens stations**: wanneer u deze instelling inschakelt en gebruikers toestaat BitLocker-beveiliging toe te passen, slaat de Configuration Manager-client herstel gegevens over Verwissel bare stations op in het beheer punt. Dit gedrag stelt gebruikers in staat om het station te herstellen als ze de Protector (wacht woord) verg eten of kwijt raken.

    - **Gebruikers toestaan BitLocker-beveiliging toe te passen op Verwissel bare gegevens stations**: gebruikers kunnen BitLocker-beveiliging inschakelen voor een verwisselbaar station.

    - **Verwisselbaar gegevens station wachtwoord beleid**: gebruik deze instellingen om de beperkingen voor wacht woorden in te stellen voor het ontgrendelen van met BitLocker beveiligde Verwissel bare stations.

    Zie [instellingen referentie-verwisselbaar station](../../tech-ref/bitlocker/settings.md#removable-drive)voor meer informatie over deze en andere instellingen op deze pagina.

1. Geef op de pagina **client beheer** de volgende instellingen op:

    > [!IMPORTANT]
    > Als u geen beheer punt hebt met een website met HTTPS-functionaliteit, kunt u deze instelling niet configureren. Zie [Recovery service](#recovery-service)(Engelstalig) voor meer informatie.

    - **BitLocker-beheer Services configureren**: wanneer u deze instelling inschakelt, Configuration Manager automatisch een back-up van sleutel herstel gegevens in de site database. Als u deze instelling uitschakelt of niet configureert, worden sleutel herstel gegevens niet opgeslagen in Configuration Manager.

        - **BitLocker-herstel gegevens selecteren om op te slaan**: Configureer deze voor het gebruik van een herstel wachtwoord en sleutel pakket, of alleen een herstel wachtwoord.

        - **Toestaan dat herstel gegevens worden opgeslagen in tekst zonder opmaak**: zonder BitLocker-versleutelings certificaat Configuration Manager worden de sleutel herstel gegevens opgeslagen als tekst zonder opmaak. Zie [herstel gegevens versleutelen](encrypt-recovery-data.md)voor meer informatie.

    Zie [Settings Reference-client management](../../tech-ref/bitlocker/settings.md#client-management)(Engelstalig) voor meer informatie over deze en andere instellingen op deze pagina.

1. Voltooi de wizard.

Als u de instellingen van een bestaand beleid wilt wijzigen, kiest u het in de lijst en selecteert u **Eigenschappen**.

Wanneer u meer dan één beleids regel maakt, kunt u hun relatieve prioriteit configureren. Als u meerdere beleids regels op een client implementeert, wordt de prioriteits waarde gebruikt om de instellingen te bepalen.

## <a name="deploy-a-policy"></a>Een beleid implementeren

1. Kies een bestaand beleid in het knoop punt **BitLocker-beheer** . Selecteer **implementeren**in het lint.

1. Selecteer een apparaat verzameling als het doel van de implementatie.

1. Als u wilt dat het apparaat de stations op elk gewenst moment kan versleutelen of ontsleutelen, selecteert u de optie voor **herstel toestaan buiten het onderhouds venster**. Als de verzameling onderhouds Vensters heeft, wordt dit BitLocker-beleid nog steeds hersteld.

1. Een **eenvoudige** of **aangepaste** planning configureren. De-client evalueert de compatibiliteit op basis van de instellingen die zijn opgegeven in de planning.

1. Selecteer **OK** om het beleid te implementeren.

U kunt meerdere implementaties van hetzelfde beleid maken. Als u meer informatie over elke implementatie wilt weer geven, selecteert u het beleid in het knoop punt **BitLocker-beheer** en gaat u naar het tabblad **implementaties** in het detail venster.

> [!IMPORTANT]
> De MBAM-client start niet BitLocker-stationsversleuteling acties als een verbinding met een extern bureau blad-protocol actief is. Alle verbindingen met de externe console moeten worden gesloten en er moet een gebruiker zijn aangemeld bij een fysieke console sessie voordat BitLocker-stationsversleuteling begint.


## <a name="monitor"></a>Controleren

Basis compatibiliteits statistieken weer geven over de beleids implementatie in het detail venster van het **BitLocker-beheer** knooppunt:

- Aantal nalevingen
- Aantal fouten
- Aantal niet-naleving

Ga naar het tabblad **implementaties** om het compatibiliteits percentage en de aanbevolen actie te bekijken. Selecteer de implementatie en selecteer vervolgens **status weer geven**in het lint. Met deze actie schakelt u de weer gave in op het knoop punt **implementaties** van **de werk ruimte** . Net als bij de implementatie van andere implementaties van configuratie beleid, kunt u in deze weer gave een gedetailleerdere nalevings status bekijken.

Zie [niet-nalevings codes](../../tech-ref/bitlocker/non-compliance-codes.md)voor meer informatie waarom clients rapporteren die niet compatibel zijn met het beheer beleid van BitLocker.

Zie [problemen met BitLocker oplossen](../../tech-ref/bitlocker/troubleshoot.md)voor meer informatie over probleem oplossing.

Gebruik de volgende logboeken om te controleren en problemen op te lossen:

### <a name="client-logs"></a>Client logboeken

- MBAM-gebeurtenis logboek: Ga in de Windows Logboeken naar toepassingen en services > micro soft > Windows > MBAM.  Zie [informatie over BitLocker-gebeurtenis logboeken](../../tech-ref/bitlocker/about-event-logs.md) en [client gebeurtenis logboeken](../../tech-ref/bitlocker/client-event-logs.md)voor meer informatie.

- **BitlockerMangementHandler. log** in client logboeken `%WINDIR%\CCM\Logs` standaard pad

### <a name="management-point-logs-recovery-service"></a>Beheer punt Logboeken (Recovery-Service)

- Gebeurtenis logboek van de herstel service: Ga in Windows Logboeken naar toepassingen en services > micro soft > Windows > MBAM-web. Zie [informatie over BitLocker-gebeurtenis logboeken](../../tech-ref/bitlocker/about-event-logs.md) en [server gebeurtenis logboeken](../../tech-ref/bitlocker/server-event-logs.md)voor meer informatie.

- Tracerings logboeken van de herstel service:`<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>Recovery-service

De BitLocker Recovery-service is een server onderdeel dat BitLocker-herstel gegevens van Configuration Manager-clients ontvangt. De site implementeert de Recovery-service wanneer u een BitLocker-beheer beleid maakt. Configuration Manager installeert automatisch de herstel service op elk beheer punt met een website met HTTPS-functionaliteit.

Configuration Manager worden de herstel gegevens opgeslagen in de site database. Zonder BitLocker-versleutelings certificaat Configuration Manager worden de sleutel herstel gegevens opgeslagen als tekst zonder opmaak.

Zie [herstel gegevens versleutelen](encrypt-recovery-data.md)voor meer informatie.

## <a name="migration-considerations"></a>Overwegingen bij migratie

Als u momenteel micro soft BitLocker Administration and monitoring (MBAM) gebruikt, kunt u het beheer naadloos migreren naar Configuration Manager. Wanneer u het beleid voor het beheren van BitLocker-beheer in Configuration Manager implementeert, uploaden clients automatisch herstel sleutels en pakketten naar de Configuration Manager Recovery-service.

> [!IMPORTANT]
> Wanneer u migreert van zelfstandige MBAM naar Configuration Manager BitLocker-beheer, moet u zelfstandige MBAM-servers of-onderdelen niet opnieuw gebruiken met Configuration Manager BitLocker-beheer als u bestaande functionaliteit van zelfstandige MBAM nodig hebt. Als u deze servers opnieuw gebruikt, werkt zelfstandige MBAM niet meer wanneer de onderdelen van Configuration Manager BitLocker-beheer op die servers worden geïnstalleerd. Voer het MBAMWebSiteInstaller.ps1 script niet uit om de BitLocker-portals op zelfstandige MBAM-servers in te stellen. Wanneer u Configuration Manager BitLocker-beheer instelt, gebruikt u afzonderlijke servers.

### <a name="group-policy"></a>Groeps beleid

- De instellingen voor BitLocker-beheer zijn volledig compatibel met instellingen voor groeps beleid voor MBAM. Als apparaten zowel instellingen voor groeps beleid als Configuration Manager beleid ontvangen, moet u deze configureren om te vergelijken.

  > [!NOTE]
  > Als er een groeps beleids instelling bestaat voor zelfstandige MBAM, wordt de equivalente instelling die wordt geprobeerd door Configuration Manager, overschreven. Zelfstandige MBAM maakt gebruik van groeps beleid van domein, terwijl Configuration Manager lokaal beleid instelt voor BitLocker-beheer. Domein beleid overschrijft de lokale Configuration Manager BitLocker-beheer beleidsregels. Als het groeps beleid van de zelfstandige MBAM niet overeenkomt met het Configuration Manager beleid, mislukt Configuration Manager BitLocker-beheer. Als een domein groeps beleid bijvoorbeeld de zelfstandige MBAM-server voor sleutel herstel Services instelt, kan Configuration Manager BitLocker-beheer niet dezelfde instelling instellen voor het beheer punt. Dit gedrag zorgt ervoor dat clients hun herstel sleutels niet rapporteren aan de Configuration Manager BitLocker-beheer sleutel herstel service op het beheer punt.

- Configuration Manager implementeert niet alle groeps beleids instellingen voor MBAM. Als u aanvullende instellingen in groeps beleid configureert, voldoet de BitLocker-beheer agent op Configuration Manager-clients over deze instellingen.

  > [!IMPORTANT]
  > Stel geen groeps beleid in voor een instelling die door Configuration Manager BitLocker-beheer al is opgegeven. Stel alleen groeps beleidsregels in voor instellingen die momenteel niet bestaan in Configuration Manager BitLocker-beheer. Configuration Manager versie 2002 heeft pariteit van functies met zelfstandige MBAM. Met Configuration Manager versie 2002 en hoger mag in de meeste gevallen geen reden zijn voor het instellen van een domein groeps beleid voor het configureren van BitLocker-beleid. Vermijd het gebruik van groeps beleid voor BitLocker om conflicten en problemen te voor komen. Configureer alle instellingen via Configuration Manager beleid voor het beheer van BitLocker.

### <a name="tpm-password-hash"></a>TPM-wachtwoord-hash

- Eerdere MBAM-clients uploaden de TPM-wachtwoord-hash niet naar Configuration Manager. De-client uploadt de TPM-wachtwoord hash slechts één keer.

- Als u deze gegevens naar de Configuration Manager Recovery-service moet migreren, wist u de TPM op het apparaat. Nadat de computer opnieuw is opgestart, wordt de nieuwe hash van het wacht woord voor TPM geüpload naar de Recovery-service.

### <a name="re-encryption"></a>Opnieuw versleutelen

Configuration Manager stations die al met BitLocker-stationsversleuteling zijn beveiligd, worden niet opnieuw versleuteld. Als u een BitLocker-beheer beleid implementeert dat niet overeenkomt met de huidige beveiliging van het station, wordt het als niet-compatibel gerapporteerd. Het station is nog steeds beveiligd.

U hebt bijvoorbeeld MBAM gebruikt voor het versleutelen van het station met het AES-XTS 128-versleutelings algoritme, maar voor het Configuration Manager-beleid is AES-XTS 256 vereist. Het station voldoet niet aan het beleid, ook al is het station versleuteld.

U kunt dit probleem omzeilen door BitLocker op het apparaat uit te scha kelen. Implementeer vervolgens een nieuw beleid met de nieuwe instellingen.

## <a name="co-management-and-intune"></a>Co-beheer en intune

<!-- SCCMDocs#2321 -->

De Configuration Manager-client-handler voor BitLocker is op zichzelfe hoogte. Als het apparaat wordt beheerd door co-beheer en u de [Endpoint Protection workload](../../../comanage/workloads.md#endpoint-protection) overschakelt naar intune, wordt het BitLocker-beleid door de Configuration Manager-client genegeerd. Het apparaat ontvangt een Windows-versleutelings beleid van intune.

Wanneer u overschakelt van versleutelings beheer instanties en de gewenste versleutelings algoritme wordt ook gewijzigd, moet u de [hercodering](#re-encryption) plannen.

Raadpleeg de volgende artikelen voor meer informatie over het beheren van BitLocker met intune:

- [Apparaatversleuteling gebruiken met intune](../../../../intune/protect/encrypt-devices.md)
- [Problemen met BitLocker-beleid in Microsoft Intune oplossen](../../../../intune/protect/troubleshoot-bitlocker-policies.md)

## <a name="next-steps"></a>Volgende stappen

[BitLocker-rapporten en-portals instellen](setup-websites.md)

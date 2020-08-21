---
title: Certificaten voor on-premises MDM
titleSuffix: Configuration Manager
description: Certificaten instellen voor vertrouwde communicatie met on-premises Mobile Device Management (MDM) in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ac8d416e05b97b824ae236c2b1a2ff958b946b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700024"
---
# <a name="set-up-certificates-for-trusted-communications-with-on-premises-mdm"></a>Certificaten instellen voor vertrouwde communicatie met on-premises MDM

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voor Configuration Manager on-premises Mobile Device Management (MDM) is vereist dat u de site systeem rollen configureert voor vertrouwde communicatie met beheerde apparaten. U hebt twee typen certificaten nodig:

- Een **webserver certificaat** in IIS op de servers die als host fungeren voor de vereiste site systeem rollen. Als één server als host fungeert voor meerdere site systeem rollen, hebt u slechts één certificaat voor die server nodig. Als elke rol zich op een afzonderlijke server bevindt, moet elke server een afzonderlijk certificaat hebben.

- Het **vertrouwde basis certificaat** van de certificerings instantie (CA) die de webserver certificaten uitgeeft. Installeer dit basis certificaat op alle apparaten die verbinding moeten maken met de site systeem rollen.

Voor apparaten die lid zijn van een domein, kan de certificaten automatisch worden geïnstalleerd op alle apparaten als u Active Directory Certificate Services gebruikt. Voor apparaten die niet lid zijn van een domein, installeert u het vertrouwde basis certificaat op een andere manier.

Voor bulksgewijs Inge schreven apparaten kunt u het certificaat in het inschrijvings pakket toevoegen. Voor apparaten die door de gebruiker worden ingeschreven, moet u het certificaat via e-mail, webdownload of een andere methode toevoegen.

Als u een bekende open bare certificerings instantie zoals VeriSign of GoDaddy gebruikt om de server certificaten te verlenen, kunt u voor komen dat u het vertrouwde basis certificaat op elk apparaat hand matig moet installeren. De meeste apparaten vertrouwen deze open bare instanties systeem eigen. Deze methode is een handig alternatief voor door de gebruiker Inge schreven apparaten, in plaats van het certificaat op een andere manier te installeren.

> [!IMPORTANT]  
> Er zijn veel manieren voor het instellen van de certificaten voor vertrouwde communicatie tussen apparaten en de site systeem servers voor on-premises MDM. De informatie in dit artikel is een voor beeld van een manier om dit te doen. Voor deze methode is Active Directory Certificate Services vereist, met een certificerings instantie en de rol webregistratie voor certificerings instantie. Zie voor meer informatie [Active Directory Certificate Services](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740\(v=ws.11\)).

## <a name="publish-the-crl"></a><a name="bkmk_configCa"></a> De CRL publiceren

De Active Directory certificerings instantie (CA) gebruikt standaard op LDAP gebaseerde certificaatintrekkingslijsten (Crl's). Hiermee kunnen verbindingen met de CRL worden toegestaan voor apparaten die lid zijn van een domein. Als u apparaten die niet lid zijn van een domein wilt toestaan certificaten te vertrouwen die zijn uitgegeven door de CA, voegt u een op HTTP gebaseerde CRL toe.

1. Ga op de server met de certificerings instantie voor uw site naar het menu **Start** , selecteer **systeem beheer**en kies **certificerings instantie**.

1. Klik in de certificerings instantie console met de rechter muisknop op **CertificateAuthority**en selecteer vervolgens **Eigenschappen**.

1. In CertificateAuthority eigenschappen gaat u naar het tabblad **extensies** . Zorg ervoor dat de **optie uitbrei ding** is ingesteld op **CRL-distributie punt (CDP)**.

1. Selecteer `http://<ServerDNSName>/CertEnroll/<CAName><CRLNameSuffix><DeltaCRLAllowed>.crl`. Selecteer vervolgens de volgende opties:

    - **In Crl's opnemen. clients gebruiken deze om locaties met Delta-CRL'S te vinden.**

    - **Aan de CDP-extensie van uitgegeven certificaten toevoegen.**

    - **Opnemen in de IDP-extensie van uitgegeven CRL's.**

1. Ga naar het tabblad **uitgifte module** . Selecteer **Eigenschappen**en selecteer vervolgens **certificaten mogen worden gepubliceerd naar het bestands systeem**. Er wordt een melding weer gegeven dat Active Directory Certificate Services opnieuw moet worden gestart.

1. Klik met de rechter muisknop op **ingetrokken certificaten**, selecteer **alle taken**en kies vervolgens **publiceren**.

1. Selecteer in het venster CRL publiceren de optie **alleen Delta-CRL**en selecteer vervolgens **OK** om het venster te sluiten.

## <a name="create-the-certificate-template"></a><a name="bkmk_certTempl"></a> De certificaat sjabloon maken

De CA gebruikt het sjabloon webserver certificaat om certificaten uit te geven voor de servers die als host fungeren voor de site systeem rollen. Deze servers worden SSL-eind punten voor vertrouwde communicatie tussen de site systeem rollen en Inge schreven apparaten.

1. Maak een domein beveiligings groep met de naam **CONFIGMGR MDM-servers**. Voeg de computer accounts van de site systeem servers toe aan de groep.

1. Klik in de certificerings instantie console met de rechter muisknop op **certificaat sjablonen**en kies **beheren**. Met deze actie wordt de certificaat sjablonen console geladen.

1. Klik in het resultaten venster met de rechter muisknop op het item dat **webserver** weergeeft in de kolom **weergave naam van sjabloon** en selecteer vervolgens **sjabloon dupliceren**.

1. In het venster **sjabloon dupliceren** selecteert u **Windows 2003 server, Enter prise edition** of **Windows 2008 server, Enter prise Edition**en selecteert u **OK**.

    > [!TIP]
    > Configuration Manager ondersteunt Windows 2008-server certificaat sjablonen, ook wel v3 of crypto grafie: Next Generation (CNG)-certificaten. Zie voor meer informatie [overzicht CNG-certificaten](../../core/plan-design/network/cng-certificates-overview.md).

    Als uw certificerings instantie op Windows Server 2012 of hoger wordt uitgevoerd, wordt in dit venster niet de optie weer gegeven voor de certificaat sjabloon versie. Nadat u de sjabloon hebt gedupliceerd, selecteert u de versie op het tabblad **compatibiliteit** van de sjabloon eigenschappen.

1. Voer in het venster **Eigenschappen van nieuwe sjabloon** op het tabblad **Algemeen** een sjabloon naam in. De CA gebruikt deze naam om de webcertificaten te genereren die zullen worden gebruikt op Configuration Manager site systemen. Typ bijvoorbeeld **CONFIGMGR MDM-webserver**.

1. Ga naar het tabblad **onderwerpnaam** en selecteer **samen stellen vanuit Active Directory informatie**. Geef voor de indeling van de object naam de **DNS-naam**op. Als **User Principal Name (UPN)** is geselecteerd, schakelt u de optie uit voor alternatieve object naam.

1. Ga naar het tabblad **beveiliging** .

    1. Verwijder de machtiging **Inschrijven** uit de beveiligings groepen **domein Administrators** en **ondernemings Administrators** .

    1. Selecteer **toevoegen**en voer de naam van de beveiligings groep in. Bijvoorbeeld **CONFIGMGR MDM-servers**. Selecteer **OK** om het venster te sluiten.

    1. Selecteer de machtiging **Inschrijven** voor deze groep. Verwijder de machtiging **lezen** niet.

1. Selecteer **OK** om uw wijzigingen op te slaan en sluit de certificaat sjablonen console.

1. Klik in de certificerings instantie console met de rechter muisknop op **certificaat sjablonen**, selecteer **Nieuw**en kies **te verlenen certificaat sjablonen**.

1. Selecteer in het venster **certificaat sjablonen inschakelen** de nieuwe sjabloon. Bijvoorbeeld **CONFIGMGR MDM-webserver**. Selecteer vervolgens **OK** om het venster op te slaan en te sluiten.

## <a name="request-the-certificate"></a><a name="bkmk_requestCert"></a> Het certificaat aanvragen

In dit proces wordt beschreven hoe u het webserver certificaat voor IIS aanvraagt. Voer dit proces uit voor elke site systeem server die als host fungeert voor een van de rollen voor on-premises MDM.

1. Open een opdracht prompt als beheerder op de site systeem server die als host fungeert voor een van de rollen. Voer `mmc` in om een lege micro soft Management console te openen.

1. Ga in het console venster naar het menu **bestand** en selecteer **module toevoegen/verwijderen**.

    1. Kies **certificaten** in de lijst met beschik bare modules en selecteer **toevoegen**.

    1. Kies **computer account**in het venster certificaten-module. Selecteer **volgende**en selecteer vervolgens **volt ooien** om de lokale computer te beheren.

    1. Selecteer **OK** om het venster module toevoegen of verwijderen te sluiten.

1. Vouw **certificaten (lokale computer)** uit en selecteer het **persoonlijke** archief. Ga naar het **actie** menu, selecteer **alle taken**en kies **Nieuw certificaat aanvragen**. Deze actie communiceert met Active Directory Certificate Services om een nieuw certificaat te maken met behulp van de sjabloon die u eerder hebt gemaakt.

    1. Selecteer in de wizard Certificaat inschrijving op de pagina voordat u begint de optie **volgende**.

    1. Selecteer op de pagina Certificaatinschrijvingsbeleid selecteren de optie **Active Directory inschrijvings beleid**en selecteer **volgende**.

    1. Selecteer de sjabloon webserver certificaat (**CONFIGMGR MDM-webserver**) en selecteer vervolgens **registreren**.

    1. Nadat het certificaat is aangevraagd, selecteert u **volt ooien**.

Elke server moet een uniek webserver certificaat hebben. Herhaal dit proces voor elke server die als host fungeert voor een van de vereiste site systeem rollen. Als één server als host fungeert voor alle sitesysteemrollen, hoeft u maar één webservercertificaat aan te vragen.

## <a name="bind-the-certificate"></a><a name="bkmk_bindCert"></a> Het certificaat binden

De volgende stap is het koppelen van het nieuwe certificaat aan de webserver. Volg deze procedure voor elke server die als host fungeert voor de site systeem rollen van het *inschrijvings punt* en het *inschrijvings proxy punt* . Als één server als host fungeert voor alle site systeem rollen, hoeft u dit proces maar één keer uit te voeren.

> [!NOTE]
> U hoeft dit proces niet uit te voeren voor de site systeem rollen van het distributie punt en het apparaatbeheerpunt. Ze ontvangen automatisch het vereiste certificaat tijdens de inschrijving.

1. Ga op de server die als host fungeert voor het inschrijvings punt of het inschrijvings proxy punt naar het menu **Start** , selecteer **systeem beheer**en kies **IIS-beheer**.

1. Selecteer in de lijst met verbindingen de **standaard website**en selecteer vervolgens **bindingen bewerken**.

    1. Selecteer in het venster site bindingen de optie **https**en selecteer vervolgens **bewerken**.

    1. Selecteer in het venster site binding bewerken het nieuwe certificaat dat u hebt Inge schreven voor het **SSL-certificaat**. Selecteer **OK** om op te slaan en selecteer vervolgens **sluiten**.

1. Selecteer in de IIS-beheer console in de lijst met verbindingen de webserver. Selecteer **opnieuw opstarten**in het deel venster actie aan de rechter kant. Met deze actie wordt de Web Server-service opnieuw gestart.

## <a name="export-the-trusted-root-certificate"></a><a name="bkmk_exportCert"></a> Het vertrouwde basis certificaat exporteren

Active Directory Certificate Services installeert automatisch het vereiste certificaat van de certificerings instantie op alle apparaten die lid zijn van het domein. Als u het certificaat wilt ophalen dat is vereist voor apparaten die niet lid zijn van een domein om te communiceren met de site systeem rollen, moet u het exporteren van het certificaat dat is gebonden aan de webserver.

1. Selecteer de **standaard website**in IIS-beheer. Selecteer **bindingen**in het deel venster actie aan de rechter kant.

1. Selecteer in het venster site bindingen de optie **https**en selecteer vervolgens **bewerken**.

1. Selecteer het webserver certificaat en selecteer **weer gave**.

1. Ga in eigenschappen van het webserver certificaat naar het tabblad **certificeringspad** . Selecteer de hoofdmap van het certificeringspad en selecteer **certificaat weer geven**.

1. Ga in de eigenschappen van het basis certificaat naar het tabblad **Details** en selecteer **kopiëren naar bestand**.

1. Selecteer in de wizard Certificaat exporteren op de pagina Welkom de optie **volgende**.

1. Selecteer **der Encoded Binary X. 509 (. CER)** als de indeling en selecteer **volgende**.

1. Voer een pad en een bestands naam in om dit vertrouwde basis certificaat te identificeren. Klik voor de bestands naam op **Bladeren...**, kies een locatie om het certificaat bestand op te slaan, geef het bestand een naam en selecteer **volgende**.

1. Controleer de instellingen en selecteer **volt ooien** om het certificaat te exporteren naar een bestand.

Afhankelijk van het ontwerp van de certificerings instantie moet u mogelijk aanvullende basis certificaten van de onderliggende CA exporteren. Herhaal dit proces voor het exporteren van de andere certificaten in het certificeringspad van het webserver certificaat.

## <a name="next-step"></a>Volgende stap

> [!div class="nextstepaction"]
> [Apparaatinschrijving instellen](set-up-device-enrollment-on-premises-mdm.md)
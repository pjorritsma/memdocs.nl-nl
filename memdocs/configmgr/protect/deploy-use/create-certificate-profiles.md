---
title: SCEP-certificaatprofielen maken, of
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van certificaat profielen om beheerde apparaten in te richten met de certificaten die ze nodig hebben
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 84f1ea48887f89cf06ed4b41d0de0dfc24e9d508
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697123"
---
# <a name="create-certificate-profiles"></a>Certificaatprofielen maken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik certificaat profielen in Configuration Manager om beheerde apparaten in te richten met de certificaten die nodig zijn om toegang te krijgen tot bedrijfs bronnen. Voordat u certificaat profielen maakt, moet u de certificaat infrastructuur instellen zoals beschreven in [certificaat infrastructuur instellen](certificate-infrastructure.md).  

> [!TIP]
> Voor gezamenlijk beheerde apparaten kunt u overwegen om de [werk belasting van het **resource toegangs beleid** ](../../comanage/workloads.md#resource-access-policies) te verplaatsen naar intune. Gebruik vervolgens intune-beleid om deze certificaten te beheren. Zie [werk belastingen overschakelen](../../comanage/how-to-switch-workloads.md)voor meer informatie.

In dit artikel wordt beschreven hoe u SCEP-certificaat profielen (Trusted Root and Simple Certificate Enrollment Protocol) maakt. Als u PFX-certificaat profielen wilt maken, raadpleegt u [PFX-certificaat profielen maken](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

Een certificaat profiel maken:

1. Start de wizard Certificaat profiel maken.
1. Geef algemene informatie over het certificaat op.
1. Configureer een certificaat van een vertrouwde certificerings instantie (CA).  
1. SCEP-certificaat gegevens configureren.  
1. Geef ondersteunde platforms voor het certificaat profiel op.

## <a name="start-the-wizard"></a>De wizard starten  

Het profiel voor het maken van het certificaat starten:

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit, vouw **toegang tot bedrijfs bronnen**uit en selecteer het knoop punt **certificaat profielen** .  

1. Selecteer **certificaat profiel maken**op het tabblad **Start** van het lint in de groep **maken** .  

## <a name="general"></a>Algemeen

Geef op de pagina **Algemeen** van de wizard Certificaatprofiel maken de volgende informatie op:  

- **Naam**: voer een unieke naam in voor het certificaatprofiel. U kunt maximaal 256 tekens gebruiken.  

- **Beschrijving**: Geef een beschrijving op die een overzicht geeft van het certificaat profiel. Neem ook andere relevante informatie op die u helpt bij het identificeren ervan in de Configuration Manager-console. U kunt maximaal 256 tekens gebruiken.  

- Geef op welk type certificaat profiel u wilt maken:

  - **Vertrouwd CA-certificaat**: Selecteer dit type om een vertrouwde basis certificerings instantie (CA) of tussenliggend CA-certificaat te implementeren om een certificaat vertrouwens keten te vormen wanneer de gebruiker of het apparaat een ander apparaat moet verifiëren. Het apparaat zou bijvoorbeeld een Remote Authentication Dial-In User Service (RADIUS)-server of een virtueel particulier netwerk (VPN)-server kunnen zijn.
  
    Configureer ook een profiel voor een vertrouwd CA-certificaat voordat u een SCEP-certificaat profiel kunt maken. In dit geval moet het vertrouwde CA-certificaat zijn voor de CA die het certificaat uitgeeft aan de gebruiker of het apparaat.  

  - **Instellingen voor Simple Certificate Enrollment Protocol (SCEP)**: Selecteer dit type om een certificaat aan te vragen voor een gebruiker of apparaat met de Simple Certificate Enrollment Protocol en de functie Service registratie service voor netwerk apparaten (NDES).

  - **PFX-instellingen (Personal Information Exchange PKCS #12)-importeren**: Selecteer deze optie om een pfx-certificaat te importeren. Zie [PFX-certificaat profielen importeren](../../mdm/deploy-use/import-pfx-certificate-profiles.md)voor meer informatie.

  - **PFX-instellingen (Personal Information Exchange PKCS #12)-maken**: Selecteer deze optie om pfx-certificaten te verwerken met een certificerings instantie. Zie [PFX-certificaat profielen maken](../../mdm/deploy-use/create-pfx-certificate-profiles.md)voor meer informatie.

## <a name="trusted-ca-certificate"></a>Vertrouwd CA-certificaat  

> [!IMPORTANT]  
> Voordat u een SCEP-certificaat profiel maakt, moet u ten minste één profiel voor een vertrouwd CA-certificaat configureren.
>
> Als u een van deze waarden wijzigt nadat het certificaat is geïmplementeerd, wordt er een nieuw certificaat aangevraagd:
>
> - Sleutelarchiefprovider
> - Naam van certificaatsjabloon
> - Certificaattype
> - Indeling van de onderwerpnaam
> - Alternatieve naam voor het onderwerp
> - Geldigheidsduur van certificaat
> - Sleutel gebruik
> - Sleutel grootte
> - Uitgebreide-sleutel gebruik
> - Basis-CA-certificaat

1. Geef op de pagina **Vertrouwd CA-certificaat** van de wizard Certificaatprofiel maken de volgende informatie op:  

    - **Certificaat bestand**: Selecteer **importeren**en blader vervolgens naar het certificaat bestand.  

    - **Doelarchief**: voor apparaten met meer dan één certificaatarchief selecteert u waar het certificaat wordt opgeslagen. Voor apparaten die slechts één archief hebben, wordt deze instelling wordt genegeerd.  

2. Gebruik de **vinger afdruk** waarde van het certificaat om te controleren of u het juiste certificaat hebt geïmporteerd.  

## <a name="scep-certificates"></a>SCEP-certificaten

### <a name="1-scep-servers"></a>1. SCEP-servers

Op de pagina **SCEP-servers** van de wizard Certificaatprofiel maken geeft u de URL's op voor de NDES-servers die via SCEP certificaten uitgeven. U kunt automatisch een NDES-URL toewijzen op basis van de configuratie van het certificaat registratiepunt of Url's hand matig toevoegen.  

### <a name="2-scep-enrollment"></a>2. SCEP-inschrijving

Voltooi de pagina **SCEP-registratie** van de wizard Certificaat profiel maken.

- **Nieuwe pogingen**: Geef het aantal keren op dat het apparaat automatisch opnieuw probeert de certificaat aanvraag naar de NDES-server. Deze instelling ondersteunt het scenario waarbij een CA-Manager een certificaat aanvraag moet goed keuren voordat het wordt geaccepteerd. Deze instelling wordt doorgaans gebruikt voor sterk beveiligde omgevingen of als u een zelfstandige verlenende CA en geen bedrijfs-CA hebt. U kunt deze instelling mogelijk ook gebruiken voor testdoeleinden zodat u de certificaataanvraagopties kunt inspecteren alvorens de verlenende CA de certificaataanvraag verwerkt. Gebruik deze instellingen met de instelling **Tijd tussen pogingen (minuten)** .  

- **Vertraging voor opnieuw proberen (minuten)**: geef het interval op, in minuten, tussen elke registratiepoging wanneer u goedkeuring van een CA-manager gebruikt voordat het verlenende CA de certificaataanvraag verwerkt. Als u goed keuring van Manager gebruikt voor test doeleinden, geeft u een lage waarde op. Vervolgens wacht u niet lang totdat het apparaat de certificaat aanvraag opnieuw probeert nadat u de aanvraag hebt goedgekeurd.

    Als u goed keuring van Manager gebruikt op een productie netwerk, geeft u een hogere waarde op. Dit gedrag maakt het voldoende tijd om de CA-beheerder in afwachting van goed keuringen goed te keuren of te weigeren.  

- **Drempelwaarde voor verlenging (%)**: geef het percentage van de levensduur van het certificaat op dat resteert voordat het apparaat verlenging van het certificaat aanvraagt.  

- **Sleutelarchiefprovider**: Geef op waar de sleutel voor het certificaat wordt opgeslagen. Kies een van de volgende waarden:  

  - **Installeren in Trusted Platform Module (TPM), indien aanwezig**: de sleutel wordt in de TPM geïnstalleerd. Als de TPM niet aanwezig is, wordt de sleutel geïnstalleerd in de opslag provider voor de software sleutel.  

  - **Installeren in Trusted Platform Module (TPM), anders niet installeren**: de sleutel wordt in de TPM geïnstalleerd. Als de TPM-module niet aanwezig is, mislukt de installatie.  

  - **Installeren in Windows hello voor bedrijven, anders mislukt**: deze optie is beschikbaar voor Windows 10-apparaten. U kunt het certificaat opslaan in de Windows hello voor bedrijven-Store, dat wordt beveiligd door multi-factor Authentication. Zie [Windows hello voor bedrijven](/windows/security/identity-protection/hello-for-business/hello-identity-verification)voor meer informatie.

    > [!NOTE]  
    > Deze optie biedt geen ondersteuning voor smartcard aanmelding voor het uitgebreide sleutel gebruik op de pagina eigenschappen van certificaat.

  - **Installeren in sleutelarchiefprovider**: de sleutel wordt in de archiefprovider voor de softwaresleutel geïnstalleerd.  

- **Apparaten voor certificaat inschrijving**: als u het certificaat profiel voor een gebruikers verzameling implementeert, mag u alleen certificaat inschrijving toestaan op het primaire apparaat van de gebruiker of op een apparaat waarop de gebruiker zich aanmeldt.

    Als u het certificaat profiel implementeert voor een verzameling apparaten, mag u de certificaat inschrijving alleen voor de primaire gebruiker van het apparaat of voor alle gebruikers die zich aanmelden bij het apparaat.  

### <a name="3-certificate-properties"></a>3. eigenschappen van certificaat

Geef op de pagina **Certificaateigenschappen** van de wizard Certificaatprofiel maken de volgende informatie op:  

- **Certificaat sjabloon naam**: Selecteer de naam van een certificaat sjabloon die u hebt geconfigureerd in NDES en die is toegevoegd aan een verlenende CA. Als u wilt bladeren naar certificaat sjablonen, moet uw gebruikers account **Lees** machtigingen hebben voor het certificaat sjabloon. Als u niet kunt **zoeken** naar het certificaat, typt u de naam ervan.  

  > [!IMPORTANT]
  > Als de naam van de certificaat sjabloon niet-ASCII-tekens bevat, wordt het certificaat niet geïmplementeerd. (Een voor beeld van deze tekens is van het Chinese alfabet.) Om ervoor te zorgen dat het certificaat wordt geïmplementeerd, moet u eerst een kopie maken van het certificaat sjabloon op de CA. Wijzig de naam van de kopie met behulp van ASCII-tekens.  

  - Als u *bladert* om de naam van de certificaat sjabloon te selecteren, worden sommige velden op de pagina automatisch ingevuld op basis van het certificaat sjabloon. In sommige gevallen kunt u deze waarden alleen wijzigen als u een ander certificaat sjabloon kiest.  

  - Als u de naam van de certificaat sjabloon *typt* , moet u ervoor zorgen dat de naam exact overeenkomt met een van de certificaat sjablonen. De naam moet overeenkomen met de namen die worden vermeld in het REGI ster van de NDES-server. Zorg ervoor dat u de naam van het certificaat sjabloon opgeeft en niet de weergave naam van het certificaat sjabloon.  

    Als u de namen van certificaat sjablonen wilt zoeken, bladert u naar de volgende register sleutel: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP` . De certificaat sjablonen worden vermeld als de waarden voor **EncryptionTemplate**, **GeneralPurposeTemplate**en **SignatureTemplate**. Standaard is de waarde voor alle drie certificaat sjablonen **IPSECIntermediateOffline**, die wordt toegewezen aan de sjabloon weergave naam van **IPSec (offline-aanvraag)**.  

    > [!WARNING]  
    > Wanneer u de naam van de certificaat sjabloon typt, kan Configuration Manager de inhoud van het certificaat sjabloon niet verifiëren. U kunt mogelijk opties selecteren die het certificaat sjabloon niet ondersteunt. Dit kan resulteren in een mislukte certificaat aanvraag. Als dit probleem zich voordoet, wordt er een fout bericht weer gegeven voor w3wp.exe in het CPR. log-bestand dat de sjabloon naam in de aanvraag voor certificaat ondertekening (CSR) en de uitdaging niet overeenkomen.  
    >
    > Wanneer u de naam van de certificaat sjabloon typt die is opgegeven voor de waarde **GeneralPurposeTemplate** , selecteert u de **sleutel codering** en de opties voor de **digitale hand tekening** voor dit certificaat profiel. Als u alleen de optie **sleutel codering** in dit certificaat profiel wilt inschakelen, geeft u de certificaat sjabloon naam op voor de sleutel **EncryptionTemplate** . Op dezelfde manier dient u, als u alleen de optie **Digitale handtekening** in dit certificaatprofiel wilt inschakelen, de naam van het certificaatsjabloon op te geven voor de sleutel **SignatureTemplate** .  

- **Certificaat type**: Selecteer of u het certificaat wilt implementeren op een apparaat of een gebruiker.  

- **Indeling van de onderwerpnaam**: selecteer hoe Configuration Manager automatisch de onderwerpnaam in de certificaat aanvraag maakt. Als het certificaat voor een gebruiker is, kunt u ook het e-mailadres van de gebruiker in de onderwerpnaam opnemen.

    > [!NOTE]  
    > Als u het **IMEI-nummer** of **serie nummer**selecteert, kunt u onderscheid maken tussen verschillende apparaten die eigendom zijn van dezelfde gebruiker. Deze apparaten kunnen bijvoorbeeld een algemene naam delen, maar geen IMEI-nummer of serie nummer. Als het apparaat geen IMEI-of serie nummer rapporteert, wordt het certificaat uitgegeven met de algemene naam.

- **Alternatieve onderwerpnaam**: Geef op hoe Configuration Manager automatisch de waarden voor de alternatieve naam voor het onderwerp (San) in de certificaat aanvraag maakt. Als u bijvoorbeeld een gebruikerscertificaattype selecteerde, kunt u de User Principal Name (UPN) gebruiken in de alternatieve naam van het onderwerp. Als het client certificaat wordt geverifieerd bij een Network Policy Server, stelt u de alternatieve naam voor het onderwerp in op de UPN.  

- **Geldigheids**duur van certificaat: als u een aangepaste geldigheids periode op de verlenende CA instelt, geeft u de resterende tijd op voordat het certificaat verloopt.

    > [!TIP]
    > Stel een aangepaste geldigheids periode in met de volgende opdracht regel: `certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE`
    > Zie [certificaat infrastructuur](certificate-infrastructure.md)voor meer informatie over deze opdracht.  

    U kunt een waarde opgeven die lager is dan de geldigheids periode in het opgegeven certificaat sjabloon, maar niet hoger. Als de geldigheids periode van het certificaat in het certificaat sjabloon bijvoorbeeld twee jaar is, kunt u een waarde van één jaar opgeven, maar geen waarde van vijf jaar. De waarde moet ook lager zijn dan de resterende geldigheidsperiode van het certificaat van de verlenende CA.  

- **Sleutelgebruik**: geef opties voor sleutelgebruik voor het certificaat op. Kies uit de volgende opties:  

  - **Sleutelcodering**: Sta sleuteluitwisseling alleen toe als de sleutel is versleuteld.  

  - **Digitale handtekening**: Sta sleuteluitwisseling alleen toe als de sleutel wordt beveiligd met een digitale handtekening.  

  Als u een certificaat sjabloon hebt bekeken, kunt u deze instellingen niet wijzigen, tenzij u een ander certificaat sjabloon selecteert.  

  Configureer het geselecteerde certificaat sjabloon met een of beide van de volgende opties voor sleutel gebruik. Als dat niet het geval is, wordt het volgende bericht weer gegeven in het logboek bestand van het certificaat registratiepunt, **CRP. log**: het **sleutel gebruik in CSR en de uitdaging komen niet overeen**  

- **Sleutelgrootte (bits)**: selecteer de grootte van de sleutel in bits.  

- **Uitgebreide-sleutel gebruik**: Voeg waarden toe voor het beoogde doel van het certificaat. In de meeste gevallen vereist het certificaat **client verificatie** zodat de gebruiker of het apparaat bij een server kan worden geverifieerd. U kunt elk gewenst sleutel gebruik toevoegen als dat nodig is.  

- **Hash-algoritme**: selecteer een van de beschikbare typen hash-algoritme om met dit certificaat te gebruiken. Selecteer het sterkste beveiligingsniveau dat door de verbindende apparaten wordt ondersteund.  

  > [!NOTE]  
  > **SHA-2** ondersteunt SHA-256, SHA-384 en SHA-512. **SHA-3** ondersteunt alleen SHA-3.  

- **Basis-CA-certificaat**: Kies een basis-CA-certificaat profiel dat u eerder hebt geconfigureerd en voor de gebruiker of het apparaat hebt geïmplementeerd. Dit CA-certificaat moet het basis certificaat zijn voor de CA die het certificaat verleent dat u in dit certificaat profiel gaat configureren.  

  > [!IMPORTANT]  
  > Als u een basis-CA-certificaat opgeeft dat niet is geïmplementeerd voor de gebruiker of het apparaat, start Configuration Manager niet de certificaat aanvraag die u in dit certificaat profiel configureert.  

## <a name="supported-platforms"></a>Ondersteunde platforms  

Selecteer op de pagina **ondersteunde platforms** van de wizard Certificaat profiel maken de versies van het besturings systeem waarop u het certificaat profiel wilt installeren. Kies **Alles selecteren** als u het certificaat profiel wilt installeren voor alle beschik bare besturings systemen.

## <a name="next-steps"></a>Volgende stappen

Het nieuwe certificaat profiel wordt weer gegeven in het knoop punt **certificaat profielen** in de werk ruimte **activa en naleving** . U kunt de app nu implementeren voor gebruikers of apparaten. Zie [profielen implementeren](deploy-wifi-vpn-email-cert-profiles.md)voor meer informatie.
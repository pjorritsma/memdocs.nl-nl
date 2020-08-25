---
title: Naslag informatie over BitLocker-instellingen
titleSuffix: Configuration Manager
description: Alle instellingen voor BitLocker-beheer die beschikbaar zijn in Configuration Manager
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b52fe5a60899d7e871381d1a34a2360bbe68a36c
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820473"
---
# <a name="bitlocker-settings-reference"></a>Naslag informatie over BitLocker-instellingen

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!-- 5925683 -->

Het BitLocker-beheer beleid in Configuration Manager bevatten de volgende beleids groepen:

- Instellen
- Station van het besturings systeem
- Vast station
- Verwisselbaar station
- Clientbeheer

In de volgende secties worden configuraties beschreven en Voorst Ellen voor de instellingen in elke groep.

> [!NOTE]
> Deze instellingen zijn gebaseerd op Configuration Manager versie 2002. Versie 1910 bevat niet al deze instellingen.

## <a name="setup"></a>Instellen

De instellingen op deze pagina configureren globale BitLocker-versleutelings opties.

### <a name="drive-encryption-method-and-cipher-strength"></a>Versleutelings methode en coderings sterkte van station

*Voorgestelde configuratie*: **ingeschakeld** met de standaard of grotere versleutelings methode.

> [!NOTE]
> De pagina **installatie** -eigenschappen bevat twee groepen instellingen voor verschillende versies van Windows. In deze sectie worden beide beschreven.

#### <a name="windows-81-devices"></a>Windows 8.1-apparaten

Voor Windows 8,1-apparaten schakelt u de optie voor de **versleutelings methode van het station en**de codeer sterkte in en selecteert u een van de volgende versleutelings methoden:

- AES 128-bits met diffusor
- AES 256-bits met diffusor
- AES 128-bits (standaard)
- AES 256-bits

Zie [New-CMBLEncryptionMethodPolicy](/powershell/module/configurationmanager/new-cmblencryptionmethodpolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

#### <a name="windows-10-devices"></a>Windows 10-apparaten

Schakel voor Windows 10-apparaten de optie voor de **versleutelings methode voor stations en de codeer sterkte in (Windows 10)**. Selecteer vervolgens een van de volgende versleutelings methoden voor OS-stations, harde schijven en verwissel bare gegevens stations:

- AES-CBC 128-bits
- AES-CBC 256-bits
- XTS-AES 128-bits (standaard)
- XTS-AES 256 bits

> [!TIP]
> BitLocker maakt gebruik van AES (Advanced Encryption Standard) als algoritme, met configureerbare sleutellengtes van 128 of 256 bits. Op Windows 10-apparaten ondersteunt de AES-versleuteling Cipher Block Chaining (CBC) of gecodeerde tekst stelen (XTS).
>
> Als u een verwisselbaar station wilt gebruiken op apparaten waarop Windows 10 niet wordt uitgevoerd, gebruikt u AES-CBC.

Zie [New-CMBLEncryptionMethodWithXts](/powershell/module/configurationmanager/new-cmblencryptionmethodwithxts?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>Algemene gebruiks notities voor stationsversleuteling en codeer sterkte

- Als u deze instellingen uitschakelt of niet configureert, gebruikt BitLocker de standaard versleutelings methode.

- Configuration Manager deze instellingen Toep assen wanneer u BitLocker inschakelt.

- Als het station al is versleuteld of wordt uitgevoerd, wordt de versleuteling van het station op het apparaat niet gewijzigd door wijzigingen in deze beleids instellingen.

- Als u de standaard waarde gebruikt, kan het nalevings rapport van de BitLocker-computer de coderings sterkte weer geven als **onbekend**. U kunt dit probleem omzeilen door deze instelling in te scha kelen en een expliciete waarde voor code sterkte in te stellen.

### <a name="prevent-memory-overwrite-on-restart"></a>Voor komen dat geheugen wordt overschreven bij opnieuw opstarten

*Voorgestelde configuratie*: **niet geconfigureerd**

Configureer dit beleid om de prestaties van het opnieuw opstarten te verbeteren zonder BitLocker-geheimen te overschrijven in het geheugen bij het opnieuw opstarten.

Wanneer u dit beleid niet configureert, verwijdert BitLocker de geheimen uit het geheugen wanneer de computer opnieuw wordt opgestart.

Zie [New-CMNoOverwritePolicy](/powershell/module/configurationmanager/new-cmnooverwritepolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>Naleving van regels voor smartcard certificaat gebruik valideren

*Voorgestelde configuratie*: **niet geconfigureerd**

Dit beleid configureren voor het gebruik van BitLocker-beveiliging op basis van smartcard certificaten. Geef vervolgens de **object-id**van het certificaat op.

Wanneer u dit beleid niet configureert, gebruikt BitLocker de standaard object-id `1.3.6.1.4.1.311.67.1.1` om een certificaat op te geven.

Zie [New-CMScCompliancePolicy](/powershell/module/configurationmanager/new-cmsccompliancepolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="organization-unique-identifiers"></a>Unieke id's van de organisatie

*Voorgestelde configuratie*: **niet geconfigureerd**

Dit beleid configureren voor het gebruik van een op certificaten gebaseerde gegevens herstel agent of de BitLocker To Go-lezer.

Wanneer u dit beleid niet configureert, gebruikt BitLocker het veld **id** niet.

Als uw organisatie hogere beveiligings metingen vereist, configureert u het veld **identificatie** . Stel dit veld in op alle doel-USB-apparaten en lijn het uit met deze instelling.

Zie [New-CMUidPolicy](/powershell/module/configurationmanager/new-cmuidpolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

## <a name="os-drive"></a>Station van het besturingssysteem

De instellingen op deze pagina configureren de versleutelings instellingen voor het station waarop Windows is geïnstalleerd.

### <a name="operating-system-drive-encryption-settings"></a>Versleutelings instellingen voor het besturings systeem station

*Voorgestelde configuratie*: **ingeschakeld**

Als u deze instelling inschakelt, moet de gebruiker het station van het besturings systeem beveiligen en BitLocker versleutelt het station. Als u deze optie uitschakelt, kan de gebruiker het station niet beveiligen. Als u dit beleid niet configureert, is BitLocker-beveiliging niet vereist op het station van het besturings systeem.

> [!NOTE]
> Als het station al is versleuteld en u deze instelling uitschakelt, ontsleutelt BitLocker het station.  

Als u apparaten hebt zonder een [Trusted Platform Module (TPM)](/windows/security/information-protection/tpm/trusted-platform-module-top-node), gebruikt u de optie voor het **toestaan van BitLocker zonder een compatibele TPM (vereist een wacht woord)**. Met deze instelling kan BitLocker het station van het besturings systeem versleutelen, zelfs als het apparaat geen TPM heeft. Als u deze optie toestaat, vraagt Windows de gebruiker om een wacht woord voor BitLocker op te geven.

Op apparaten met een compatibele TPM kunnen tijdens het opstarten twee typen verificatie methoden worden gebruikt om extra beveiliging te bieden voor versleutelde gegevens. Wanneer de computer wordt gestart, kan deze alleen de TPM voor verificatie gebruiken, of kan de vermelding van een persoonlijk identificatie nummer (pincode) ook vereist zijn. Configureer de volgende instellingen:

- **Selecteer beveiliging voor het station van het besturings systeem**: Configureer dit voor het gebruik van een TPM en pincode, of alleen voor de TPM.

- **Minimale lengte voor pincodes configureren voor opstarten**: als u een pincode nodig hebt, is deze waarde de kortste lengte die de gebruiker kan opgeven. De gebruiker voert deze pincode in wanneer de computer opstart om het station te ontgrendelen. De minimale lengte van de pincode is standaard `4` .

> [!TIP]
> Voor een betere beveiliging kunt u de volgende instellingen voor groeps beleid *uitschakelen* in de slaap stand van het **systeem**  >  **energie beheer**als u apparaten met TPM + pincode-beveiliging inschakelt  >  **Sleep Settings**.
>
> - Stand-by statussen (S1-S3) toestaan wanneer de slaap stand wordt ingeschakeld (netstroom)
>
> - Stand-by statussen (S1-S3) toestaan tijdens het slapen (op batterij)

Zie [New-CMBMSOSDEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsosdencryptionpolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="allow-enhanced-pins-for-startup"></a>Uitgebreide pincodes voor opstarten toestaan

*Voorgestelde configuratie*: **niet geconfigureerd**

BitLocker configureren voor het gebruik van verbeterde opstart pincodes. Met deze pincodes kunt u het gebruik van extra tekens, zoals hoofd letters en kleine letters, symbolen, cijfers en spaties, toestaan. Deze instelling is van toepassing wanneer u BitLocker inschakelt.

> [!IMPORTANT]
> Niet alle computers kunnen verbeterde pincodes in de pre-boot omgeving ondersteunen. Controleer of uw apparaten compatibel zijn met deze functie voordat u het gebruik ervan inschakelt.

Als u deze instelling inschakelt, kan de gebruiker met alle nieuwe BitLocker-opstart pincodes verhoogde pincodes maken.

- **Alleen ASCII-pincodes vereisen**: verbeterde pincodes zijn compatibel met computers die het type of aantal tekens beperken dat u kunt invoeren in de pre-boot omgeving.

Als u deze beleids instelling uitschakelt of niet configureert, gebruikt BitLocker geen verbeterde pincodes.

Zie [New-CMEnhancedPIN](/powershell/module/configurationmanager/new-cmenhancedpin?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="operating-system-drive-password-policy"></a>Wachtwoord beleid besturings systeem

*Voorgestelde configuratie*: **niet geconfigureerd**

Gebruik deze instellingen om de beperkingen voor wacht woorden in te stellen voor het ontgrendelen van BitLocker beveiligde OS-stations. Als u niet-TPM-beveiligingen op OS-stations toestaat, configureert u de volgende instellingen:

- **Wachtwoord complexiteit configureren voor besturingssysteem stations**: als u complexiteits vereisten voor het wacht woord wilt afdwingen, selecteert u **wachtwoord complexiteit vereisen**.

- **Minimale wachtwoord lengte voor het besturings systeem station**: de minimum lengte is standaard `8` .

- **Alleen ASCII-wacht woorden vereisen voor Verwissel bare OS-stations**

Als u deze beleids instelling inschakelt, kunnen gebruikers een wacht woord configureren dat voldoet aan de vereisten die u definieert.

Zie [New-CMOSPassphrase](/powershell/module/configurationmanager/new-cmospassphrase?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>Algemene gebruiks opmerkingen voor wachtwoord beleid voor het besturings systeem-station

- Als u de instellingen voor de complexiteits vereisten effectief wilt maken, moet u ook het wacht woord voor groeps beleids instelling inschakelen om te **voldoen aan complexiteits vereisten** in **computer configuratie**  >  **Windows-instellingen**  >  **beveiligings instellingen**  >  **account**beleid  >  **wachtwoord beleid**.

- BitLocker dwingt deze instellingen af wanneer u deze inschakelt, niet wanneer u een volume ontgrendelt. Met BitLocker kunt u een station ontgrendelen met een van de beveiligingen die beschikbaar zijn op het station.

- Als u groeps beleid gebruikt om FIPS-compatibele algoritmen voor versleuteling, hashing en ondertekening in te scha kelen, kunt u wacht woorden niet als BitLocker-Protector toestaan.

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>Platform validatie gegevens opnieuw instellen na BitLocker-herstel

*Voorgestelde configuratie*: **niet geconfigureerd**

Hiermee bepaalt u of Windows platform validatie gegevens vernieuwt wanneer deze worden gestart na BitLocker-herstel.

Als u deze instelling inschakelt of niet configureert, vernieuwt Windows de platform validatie gegevens in deze situatie.

Als u deze beleids instelling uitschakelt, worden de validatie gegevens van het platform in deze situatie niet vernieuwd.

Zie [New-CMTpmAutoResealPolicy](/powershell/module/configurationmanager/new-cmtpmautoresealpolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="pre-boot-recovery-message-and-url"></a>Preboot-herstelbericht en -URL

*Voorgestelde configuratie*: **niet geconfigureerd**

Wanneer BitLocker het station van het besturings systeem vergrendelt, gebruikt u deze instelling om een aangepast herstel bericht of een URL weer te geven op het pre-boot BitLocker-herstel scherm. Deze instelling is alleen van toepassing op Windows 10-apparaten.

Wanneer u deze instelling inschakelt, selecteert u een van de volgende opties voor het pre-boot herstel bericht:

- **Standaard herstel bericht en URL gebruiken**: Hiermee wordt het standaard herstel bericht en de URL van BitLocker weer gegeven in het pre-boot BitLocker-herstel scherm. Als u eerder een aangepast herstel bericht of een URL hebt geconfigureerd, gebruikt u deze optie om het standaard bericht te herstellen.

- **Aangepast herstel bericht gebruiken**: Neem een aangepast bericht op in het pre-boot BitLocker-herstel scherm.

  - **Aangepaste optie voor herstel bericht**: Typ het aangepaste bericht dat moet worden weer gegeven. Als u ook een herstel-URL wilt opgeven, moet u deze opnemen als onderdeel van dit aangepaste herstel bericht. De maximale teken reeks lengte is 32.768 tekens.

- **Aangepaste herstel-URL gebruiken**: Vervang de standaard-URL die wordt weer gegeven in het pre-boot BitLocker-herstel scherm.

  - **Optie voor aangepaste herstel-URL**: Typ de URL die u wilt weer geven. De maximale teken reeks lengte is 32.768 tekens.

> [!NOTE]
> Niet alle tekens en talen worden ondersteund in de pre-boot. Test eerst uw aangepaste bericht of URL om te controleren of deze correct wordt weer gegeven op het BitLocker-herstel scherm vóór het opstarten.

Zie [New-CMPrebootRecoveryInfo](/powershell/module/configurationmanager/new-cmprebootrecoveryinfo?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="encryption-policy-enforcement-settings-os-drive"></a>Instellingen voor afdwingen van versleutelings beleid (OS-station)

*Voorgestelde configuratie*: **ingeschakeld**

Het aantal dagen configureren dat gebruikers BitLocker-compatibiliteit voor het station van het besturings systeem kunnen uitstellen. De **respijt periode** voor niet-naleving begint wanneer Configuration Manager deze eerst als niet-compatibel detecteert. Nadat deze respijt periode is verlopen, kunnen gebruikers de vereiste actie niet uitstellen of een uitzonde ring aanvragen.

Als voor het versleutelings proces gebruikers invoer is vereist, wordt in Windows een dialoog venster weer gegeven dat de gebruiker niet kan sluiten totdat de vereiste gegevens worden opgegeven. Deze beperking geldt niet voor toekomstige meldingen voor fouten of status.

Als BitLocker geen gebruikers interactie vereist om een protector toe te voegen nadat de respijt periode is verlopen, start BitLocker de versleuteling op de achtergrond.

Als u deze instelling uitschakelt of niet configureert, vereist Configuration Manager niet dat gebruikers voldoen aan het BitLocker-beleid.

Als u het beleid onmiddellijk wilt afdwingen, stelt u een respijt periode van in `0` .

Zie [New-CMUseOsEnforcePolicy](/powershell/module/configurationmanager/new-cmuseosenforcepolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

## <a name="fixed-drive"></a>Vast station

Met de instellingen op deze pagina configureert u versleuteling voor extra gegevens stations in een apparaat.

### <a name="fixed-data-drive-encryption"></a>Versleuteling van de vaste gegevens schijf

*Voorgestelde configuratie*: **ingeschakeld**

Uw vereiste voor het versleutelen van vaste-gegevens stations beheren. Als u deze instelling inschakelt, moeten gebruikers van BitLocker alle vaste-gegevens stations onder beveiliging plaatsen. Vervolgens worden de gegevens stations versleuteld.

Wanneer u dit beleid inschakelt, schakelt u automatisch ontgrendelen of de instellingen voor het **wachtwoord beleid vaste gegevens schijf**in.

- **Automatisch ontgrendelen configureren voor harde schijf**: het versleutelde gegevens station toestaan of vereisen dat BitLocker automatisch wordt ontgrendeld. Als u automatisch ontgrendelen wilt gebruiken, moet BitLocker ook het [station van het besturings systeem](#os-drive)versleutelen.

Als u deze instelling niet configureert, vereist BitLocker dat gebruikers geen vaste gegevens stations onder beveiliging kunnen plaatsen.

Als u deze instelling uitschakelt, kunnen gebruikers hun vaste gegevens stations niet onder BitLocker-beveiliging plaatsen. Als u dit beleid uitschakelt nadat BitLocker vaste gegevens stations heeft versleuteld, ontsleutelt BitLocker de vaste schijven.

Zie [New-CMBMSFDVEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsfdvencryptionpolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>Schrijf toegang weigeren voor vaste stations die niet worden beveiligd met BitLocker

*Voorgestelde configuratie*: **niet geconfigureerd**

BitLocker-beveiliging voor Windows vereist voor het schrijven van gegevens naar vaste stations op het apparaat. Dit beleid wordt door BitLocker toegepast wanneer u het inschakelt.

Wanneer u deze instelling inschakelt:

- Als BitLocker een vaste gegevens schijf beveiligt, koppelt Windows deze met lees-en schrijf toegang.

- Voor alle vaste gegevens schijven die BitLocker niet beveiligt, koppelt Windows deze als alleen-lezen.

Wanneer u deze instelling niet configureert, koppelt Windows alle vaste-gegevens stations met lees-en schrijf toegang.

Zie [New-CMFDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmfdvdenywriteaccesspolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="fixed-data-drive-password-policy"></a>Wachtwoord beleid voor vaste gegevens stations

*Voorgestelde configuratie*: **niet geconfigureerd**

Gebruik deze instellingen om de beperkingen voor wacht woorden in te stellen voor het ontgrendelen van met BitLocker beveiligde vaste-gegevens stations.

Als u deze instelling inschakelt, kunnen gebruikers een wacht woord configureren dat voldoet aan uw gedefinieerde vereisten.

Voor een betere beveiliging schakelt u deze instelling in en configureert u de volgende instellingen:

- **Wacht woord vereisen voor vaste-schijf station**: gebruikers moeten een wacht woord opgeven om een met BitLocker beveiligde vaste-gegevens schijf te ontgrendelen.

- **Wachtwoord complexiteit voor harde schijven configureren**: als u complexiteits vereisten voor het wacht woord wilt afdwingen, selecteert u **wachtwoord complexiteit vereisen**.

- **Minimale wachtwoord lengte voor harde schijf**: standaard is de minimum lengte `8` .

Als u deze instelling uitschakelt, kunnen gebruikers geen wacht woord configureren.

Wanneer het beleid niet is geconfigureerd, ondersteunt BitLocker wacht woorden met de standaard instellingen. De standaard instellingen bevatten geen vereisten voor wachtwoord complexiteit en vereisen slechts acht tekens.

Zie [New-CMFDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmfdvpassphrasepolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>Algemene gebruiks notities voor het wachtwoord beleid voor vaste gegevens stations

- Als u de instellingen voor de complexiteits vereisten effectief wilt maken, moet u ook het wacht woord voor groeps beleids instelling inschakelen om te **voldoen aan complexiteits vereisten** in **computer configuratie**  >  **Windows-instellingen**  >  **beveiligings instellingen**  >  **account**beleid  >  **wachtwoord beleid**.

- BitLocker dwingt deze instellingen af wanneer u deze inschakelt, niet wanneer u een volume ontgrendelt. Met BitLocker kunt u een station ontgrendelen met een van de beveiligingen die beschikbaar zijn op het station.

- Als u groeps beleid gebruikt om FIPS-compatibele algoritmen voor versleuteling, hashing en ondertekening in te scha kelen, kunt u wacht woorden niet als BitLocker-Protector toestaan.

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>Instellingen voor afdwingen van versleutelings beleid (vaste gegevens station)

*Voorgestelde configuratie*: **ingeschakeld**

Hiermee configureert u het aantal dagen dat gebruikers BitLocker-compatibiliteit voor harde schijven kunnen uitstellen. De **respijt periode** voor niet-naleving begint wanneer Configuration Manager eerst het vaste-gegevens station detecteert als niet-compatibel. Het beleid voor vaste-gegevens stations wordt niet afgedwongen totdat het station van het besturings systeem compatibel is. Nadat de respijt periode is verlopen, kunnen gebruikers de vereiste actie niet uitstellen of een uitzonde ring aanvragen.

Als voor het versleutelings proces gebruikers invoer is vereist, wordt in Windows een dialoog venster weer gegeven dat de gebruiker niet kan sluiten totdat de vereiste gegevens worden opgegeven. Deze beperking geldt niet voor toekomstige meldingen voor fouten of status.

Als BitLocker geen gebruikers interactie vereist om een protector toe te voegen nadat de respijt periode is verlopen, start BitLocker de versleuteling op de achtergrond.

Als u deze instelling uitschakelt of niet configureert, vereist Configuration Manager niet dat gebruikers voldoen aan het BitLocker-beleid.

Als u het beleid onmiddellijk wilt afdwingen, stelt u een respijt periode van in `0` .

Zie [New-CMUseFddEnforcePolicy](/powershell/module/configurationmanager/new-cmusefddenforcepolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

## <a name="removable-drive"></a>Verwisselbaar station

De instellingen op deze pagina configureren versleuteling voor Verwissel bare stations, zoals USB-sleutels.

### <a name="removable-data-drive-encryption"></a>Versleuteling van Verwissel bare gegevens stations

*Voorgestelde configuratie*: **ingeschakeld**

Met deze instelling bepaalt u het gebruik van BitLocker op Verwissel bare stations.

- **Gebruikers toestaan BitLocker-beveiliging toe te passen op Verwissel bare gegevens stations**: gebruikers kunnen BitLocker-beveiliging inschakelen voor een verwisselbaar station.

- **Gebruikers toestaan BitLocker te onderbreken en ontsleutelen op Verwissel bare gegevens stations**: gebruikers kunnen BitLocker-stationsversleuteling van een verwisselbaar station verwijderen of tijdelijk opschorten.

Wanneer u deze instelling inschakelt en gebruikers toestaat BitLocker-beveiliging toe te passen, slaat de Configuration Manager-client herstel gegevens over Verwissel bare stations op in het beheer punt. Dit gedrag stelt gebruikers in staat om het station te herstellen als ze de Protector (wacht woord) verg eten of kwijt raken.

Wanneer u deze instelling inschakelt:

- De instellingen voor het **wachtwoord beleid voor Verwissel bare gegevens stations** inschakelen

- *Schakel* de volgende groeps beleids instellingen **System**uit in de  >  **toegang tot de Verwissel bare opslag** van het systeem voor zowel gebruikers & computer configuraties:

  - **Alle Verwissel bare-opslag klassen: alle toegang weigeren**
  - **Verwissel bare schijven: schrijf toegang weigeren**
  - **Verwissel bare schijven: Lees toegang weigeren**

Als u deze instelling uitschakelt, kunnen gebruikers geen BitLocker gebruiken op Verwissel bare stations.

Zie [New-CMRDVConfigureBDEPolicy](/powershell/module/configurationmanager/new-cmrdvconfigurebdepolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>Schrijf toegang weigeren voor Verwissel bare stations die niet worden beveiligd met BitLocker

*Voorgestelde configuratie*: **niet geconfigureerd**

BitLocker-beveiliging voor Windows vereist voor het schrijven van gegevens naar Verwissel bare stations op het apparaat. Dit beleid wordt door BitLocker toegepast wanneer u het inschakelt.

Wanneer u deze instelling inschakelt:

- Als BitLocker een verwisselbaar station beveiligt, koppelt Windows het met lees-en schrijf toegang.

- Voor een verwisselbaar station dat BitLocker niet beveiligt, koppelt Windows het als alleen-lezen.

- Als u de optie voor het **weigeren van schrijf toegang voor apparaten die in een andere organisatie zijn geconfigureerd**, biedt BitLocker alleen schrijf toegang tot Verwissel bare stations met id-velden die overeenkomen met de toegestane id-velden. Definieer deze velden met de algemene instellingen voor de **organisatie unieke id's** op de pagina [Setup](#setup) .

Wanneer u deze instelling uitschakelt of niet configureert, koppelt Windows alle Verwissel bare stations met lees-en schrijf toegang.

> [!NOTE]
> U kunt deze instelling onderdrukken met de instellingen voor groeps **System**beleid in de  >  **toegang tot de Verwissel bare opslag**van het systeem. Als u de groeps beleids instelling **Verwissel bare schijven inschakelt: schrijf toegang weigeren**, negeert BitLocker deze Configuration Manager instelling.

Zie [New-CMRDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmrdvdenywriteaccesspolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="removable-data-drive-password-policy"></a>Verwisselbaar gegevens station wachtwoord beleid

*Voorgestelde configuratie*: **ingeschakeld**

Gebruik deze instellingen om de beperkingen voor wacht woorden in te stellen voor het ontgrendelen van met BitLocker beveiligde Verwissel bare stations.

Als u deze instelling inschakelt, kunnen gebruikers een wacht woord configureren dat voldoet aan uw gedefinieerde vereisten.

Voor een betere beveiliging schakelt u deze instelling in en configureert u de volgende instellingen:

- **Wacht woord vereisen voor verwisselbaar gegevens station**: gebruikers moeten een wacht woord opgeven om een met BitLocker beveiligd verwisselbaar station te ontgrendelen.

- **Wachtwoord complexiteit voor Verwissel bare gegevens stations configureren**: als u complexiteits vereisten voor het wacht woord wilt afdwingen, selecteert u **wachtwoord complexiteit vereisen**.

- **Minimale wachtwoord lengte voor Verwissel bare gegevens stations**: de minimum lengte is standaard `8` .

Als u deze instelling uitschakelt, kunnen gebruikers geen wacht woord configureren.

Wanneer het beleid niet is geconfigureerd, ondersteunt BitLocker wacht woorden met de standaard instellingen. De standaard instellingen bevatten geen vereisten voor wachtwoord complexiteit en vereisen slechts acht tekens.

Zie [New-CMRDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmrdvpassphrasepolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>Algemene gebruiks opmerkingen voor het wachtwoord beleid voor Verwissel bare gegevens stations

- Als u de instellingen voor de complexiteits vereisten effectief wilt maken, moet u ook het wacht woord voor groeps beleids instelling inschakelen om te **voldoen aan complexiteits vereisten** in **computer configuratie**  >  **Windows-instellingen**  >  **beveiligings instellingen**  >  **account**beleid  >  **wachtwoord beleid**.

- BitLocker dwingt deze instellingen af wanneer u deze inschakelt, niet wanneer u een volume ontgrendelt. Met BitLocker kunt u een station ontgrendelen met een van de beveiligingen die beschikbaar zijn op het station.

- Als u groeps beleid gebruikt om FIPS-compatibele algoritmen voor versleuteling, hashing en ondertekening in te scha kelen, kunt u wacht woorden niet als BitLocker-Protector toestaan.

## <a name="client-management"></a>Clientbeheer

De instellingen op deze pagina configureren BitLocker-beheer Services en-clients.

### <a name="bitlocker-management-services"></a>BitLocker-beheer Services

*Voorgestelde configuratie*: **ingeschakeld**

Wanneer u deze instelling inschakelt, wordt in de site database automatisch een back-up van sleutel herstel gegevens gemaakt Configuration Manager en op de achtergrond. Als u deze instelling uitschakelt of niet configureert, worden sleutel herstel gegevens niet opgeslagen in Configuration Manager.

- **BitLocker-herstel gegevens selecteren om op te slaan**: Configureer de service voor sleutel herstel om back-ups te maken van BitLocker-herstel gegevens. Het biedt een beheer methode voor het herstellen van gegevens die zijn versleuteld met BitLocker, waardoor gegevens verlies wordt voor komen door het ontbreken van belang rijke gegevens.

- **Toestaan dat herstel gegevens worden opgeslagen in tekst zonder opmaak**: zonder BitLocker-versleutelings certificaat voor SQL Server, Configuration Manager de sleutel herstel gegevens opslaan als tekst zonder opmaak. Zie [herstel gegevens versleutelen](../../deploy-use/bitlocker/encrypt-recovery-data.md)voor meer informatie.

- **Frequentie van client controle status (minuten)**: de client controleert de BitLocker-beveiligings beleidsregels en-status op de computer en maakt ook een back-up van de client herstel sleutel. De BitLocker-herstel gegevens van de Configuration Manager-client worden standaard elke 90 minuten bijgewerkt.

Zie voor meer informatie over het maken van dit beleid met Windows Power shell:

- [Set-CMBlmPlaintextStorage](/powershell/module/configurationmanager/set-cmblmplaintextstorage?view=sccm-ps)
- [New-CMBMSClientConfigureCheckIntervalPolicy](/powershell/module/configurationmanager/new-cmbmsclientconfigurecheckintervalpolicy?view=sccm-ps)

### <a name="user-exemption-policy"></a>Beleid voor gebruikers uitsluiting

*Voorgestelde configuratie*: **niet geconfigureerd**

Een contact wijze configureren voor gebruikers om een uitzonde ring van BitLocker-versleuteling aan te vragen.

Als u deze beleids instelling inschakelt, geeft u de volgende informatie op:

- **Maximum aantal dagen dat moet worden uitgesteld**: het aantal dagen dat de gebruiker een afgedwongen beleid kan uitstellen. Deze waarde is standaard ingesteld op `7` dagen (één week).

- **Contact methode**: Geef op hoe gebruikers een uitzonde ring kunnen aanvragen: URL, e-mail adres of telefoon nummer.

- **Contact persoon**: Geef de URL, het e-mail adres of het telefoon nummer op. Wanneer een gebruiker een uitzonde ring van BitLocker-beveiliging aanvraagt, wordt er een Windows-dialoog venster weer geven met instructies voor het Toep assen. Configuration Manager valideert niet de gegevens die u invoert.

  - **URL**: gebruik de standaard-URL-indeling, `https://website.domain.tld` . Windows geeft de URL weer als een Hyper link.

  - **E-mail adres**: gebruik de standaard indeling voor e-mail adressen, `user@domain.tld` . In Windows wordt het adres als de volgende Hyper link weer gegeven: `mailto:user@domain.tld?subject=Request exemption from BitLocker protection` .

  - **Telefoon nummer**: Geef het nummer op dat uw gebruikers moeten bellen. In Windows wordt het nummer met de volgende beschrijving weer gegeven: `Please call <your number> for applying exemption` .

Als u deze instelling uitschakelt of niet configureert, worden de instructies voor de uitzonderings aanvraag niet door Windows weer gegeven aan gebruikers.

> [!NOTE]
> BitLocker beheert uitzonde ringen per gebruiker, niet per computer. Als meerdere gebruikers zich aanmelden bij dezelfde computer en een gebruiker niet is uitgesloten, versleutelt BitLocker de computer.

Zie [New-CMBMSUserExemptionPolicy](/powershell/module/configurationmanager/new-cmbmsuserexemptionpolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

### <a name="url-for-the-security-policy-link"></a>URL voor de koppeling naar het beveiligings beleid

*Voorgestelde configuratie*: **ingeschakeld**

Geef een URL op die voor gebruikers moet worden weer gegeven als het **beveiligings beleid** van het bedrijf in Windows. Gebruik deze koppeling om gebruikers informatie te geven over de versleutelings vereisten. Er wordt weer gegeven wanneer BitLocker de gebruiker vraagt om een station te versleutelen.

Als u deze instelling inschakelt, configureert u de **koppelings-URL voor het beveiligings beleid**.

Als u deze instelling uitschakelt of niet configureert, wordt de koppeling beveiligings beleid niet weer gegeven in BitLocker.

Zie [New-CMMoreInfoUrlPolicy](/powershell/module/configurationmanager/new-cmmoreinfourlpolicy?view=sccm-ps)voor meer informatie over het maken van dit beleid met Windows Power shell.

## <a name="next-steps"></a>Volgende stappen

Als u Windows Power shell gebruikt om deze beleids objecten te maken, gebruikt u de cmdlet [New-CMBlmSetting](/powershell/module/configurationmanager/new-cmblmsetting?view=sccm-ps) . Met deze cmdlet maakt u een object met beleids instellingen voor BitLocker-beheer dat alle opgegeven beleids regels bevat. Gebruik de cmdlet [New-CMSettingDeployment](/powershell/module/configurationmanager/new-cmsettingdeployment?view=sccm-ps) om de beleids instellingen te implementeren voor een verzameling.

---
title: Certificaten met een persoonlijke en openbare sleutel gebruiken in Microsoft Intune - Azure | Microsoft Docs
description: Gebruik PKCS-certificaten (Public Key Cryptography Standards) met Microsoft Intune, werk met basiscertificaten en certificaatsjablonen, de installatie van de Microsoft Intune-connector (NDES) en gebruik apparaatconfiguratieprofielen voor een PKCS-certificaat.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1024681ed42c192983ffde23777de72c40622c65
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423714"
---
# <a name="configure-and-use-pkcs-certificates-with-intune"></a>PKCS-certificaten configureren en gebruiken met Intune

Intune ondersteunt het gebruik van certificaten voor persoonlijke en openbare sleutelparen (PKCS). Met behulp van dit artikel kunt u de vereiste infrastructuur, zoals on-premises certificaatconnectors, configureren, een PKCS-certificaat exporteren en vervolgens het certificaat toevoegen aan een Intune-apparaatconfiguratieprofiel.

Microsoft Intune bevat ingebouwde instellingen voor het gebruik van PKCS-certificaten voor toegang en verificatie van uw bedrijfsbronnen. Met certificaten wordt de toegang tot uw bedrijfsbronnen, zoals een VPN of Wi-Fi-netwerk, geverifieerd en beveiligd. U implementeert deze instellingen naar apparaten met behulp van apparaatconfiguratieprofielen in Intune.

Zie [Geïmporteerde PFX-certificaten](certificates-imported-pfx-configure.md) voor meer informatie over het gebruik van geïmporteerde PKCS-certificaten.


## <a name="requirements"></a>Vereisten

Als u PKCS-certificaten wilt gebruiken met Intune, hebt u de volgende infrastructuur nodig:

- **Active Directory-domein**:  
  Alle servers die in dit gedeelte worden genoemd, moeten lid zijn van uw Active Directory-domein.

  Zie [AD DS-ontwerp- en -planning](/windows-server/identity/ad-ds/plan/ad-ds-design-and-planning) voor meer informatie over het installeren en configureren van AD DS (Active Directory Domain Services).

- **Certificeringsinstantie**:  
   Een certificeringsinstantie (CA) voor ondernemingen.

  Raadpleeg [Stapsgewijze handleiding bij Active Directory Certificate Services](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772393(v=ws.10)) als u informatie wilt over het installeren en configureren van Active Directory Certificate Services (AD CS).

  > [!WARNING]  
  > Voor Intune moet u AD CS uitvoeren met een certificeringsinstantie (CA) voor ondernemingen, niet met een zelfstandige certificeringsinstantie.

- **Een client**:  
  deze wordt gekoppeld aan de CA voor ondernemingen.

- **Basiscertificaat**:  
  Een geëxporteerde kopie van uw basiscertificaat van uw CA voor ondernemingen.

- **PFX-certificaatconnector voor Microsoft Intune**:

  Zie [Certificate connectors](certificate-connectors.md) (Certificaatconnectors) voor meer informatie over de PFX-certificaatconnector, inclusief vereisten en releaseversies.

  > [!IMPORTANT]
  > Vanaf de release van versie 6.2008.60.607 van de PFX-certificaatconnector is de Microsoft Intune-connector niet langer vereist voor PKCS-certificaatprofielen. 
  
## <a name="export-the-root-certificate-from-the-enterprise-ca"></a>Het basiscertificaat exporteren vanuit de CA voor ondernemingen

Voor verificatie van een apparaat met VPN, Wi-Fi of andere resources hebt u op elk apparaat een basis- of tussen-CA-certificaat nodig. In de volgende stappen wordt uitgelegd hoe u het vereiste certificaat kunt verkrijgen op basis van uw CA voor ondernemingen.

**Opdrachtregel invoeren**:  

1. Meld u aan bij de basiscertificeringsinstantieserver met een beheerdersaccount.

2. Ga naar **Start** > **Uitvoeren** en voer vervolgens **Cmd** uit om de opdrachtprompt openen.

3. Geef **certutil -ca.cert ca_name.cer** op om het basiscertificaat te exporteren als een bestand met de naam *ca_name.cer*.

## <a name="configure-certificate-templates-on-the-ca"></a>Certificaatsjablonen configureren op de CA

1. Meld u aan bij uw CA voor ondernemingen met een account met beheerdersbevoegdheden.
2. Open de console **Certificeringsinstantie**, klik met de rechtermuisknop op **Certificaatsjablonen** en selecteer **Beheren**.
3. Zoek naar de certificaatsjabloon **Gebruiker**, klik er met de rechtermuisknop op en kies **Sjabloon dupliceren** om **Eigenschappen van nieuwe sjabloon** te openen.

    > [!NOTE]
    > Voor scenario's voor S/MIME-e-mailversleuteling en -ondertekening gebruiken veel beheerders afzonderlijke certificaten voor ondertekening en versleuteling. Als u Microsoft Active Directory Certificate Services gebruikt, kunt u de sjabloon **Alleen Exchange-handtekening** gebruiken voor S/MIME-e-mailondertekeningscertificaten en de sjabloon **Exchange-gebruiker** voor S/MIME-versleutelingscertificaten.  Als u een certificeringsinstantie van derden gebruikt, is het verstandig de richtlijnen te raadplegen voor het instellen van sjablonen voor ondertekening en versleuteling.

4. Op het tabblad **Compatibiliteit**:

    - Stel **Certificeringsinstantie (CA)** in op **Windows Server 2008 R2**
    - Stel **Ontvanger van certificaat** in op **Windows 7 / Server 2008 R2**

5. Stel op het tabblad **Algemeen** **Weergavenaam van sjabloon** in op iets dat voor u herkenbaar is.

    > [!WARNING]
    > **Sjabloonnaam** is standaard hetzelfde als **Weergavenaam van sjabloon**, maar dan *zonder spaties*. Noteer de naam van de sjabloon; deze hebt u later nodig.

6. Selecteer in **Afhandeling van aanvragen** de optie **De persoonlijke sleutel exporteerbaar maken**.

    > [!NOTE]
    > In tegenstelling tot SCEP wordt met PKCS de persoonlijke sleutel van het certificaat gegenereerd op de server waarop de connector is geïnstalleerd en niet op het apparaat. Het is een vereiste dat de certificaatsjabloon het exporteren van de persoonlijke sleutel mogelijk maakt, zodat de certificaatconnector het PFX-certificaat kan exporteren en naar het apparaat kan verzenden. 
    >
    > Houd er echter rekening mee dat de certificaten worden geïnstalleerd op het apparaat zelf met een als niet-exporteerbaar gemarkeerde persoonlijke sleutel.

7. Bevestig in **Cryptografie** dat de **Minimale sleutelgrootte** is ingesteld op 2048.
8. Kies **Leveren met het verzoek** in **Onderwerpnaam**.
9. Bevestig in **Extensies** dat Encrypting File System, Beveiligde e-mail en Clientauthenticatie worden weergegeven onder **Toepassingsbeleid**.

    > [!IMPORTANT]
    > Ga voor iOS-/iPadOS-certificaatsjablonen naar het tabblad **Extensies**, werk **Sleutelgebruik** bij en zorg ervoor dat **Handtekening is bewijs van authenticiteit** niet is ingeschakeld.

10. Voeg in **Beveiliging** het computeraccount toe voor de server waarop u de Microsoft Intune-connector installeert. Geef dit account machtigingen voor **Lezen** en **Registreren**.
11. Selecteer **Toepassen** > **OK** om de certificaatsjabloon op te slaan. Sluit de **console Certificaatsjablonen**.
12. Klik in de **certificeringsinstantieconsole** met de rechtermuisknop op **Certificaatsjablonen** > , klik op **Nieuw** >  en klik vervolgens op **Te verlenen certificaatsjablonen**. Kies de sjabloon die u in de eerdere stappen hebt gemaakt. Selecteer **OK**.
13. Voer de volgende stappen uit om ervoor te zorgen dat de server certificaten beheert voor geregistreerde apparaten en gebruikers:

    1. Klik met de rechtermuisknop op de CA en kies **Eigenschappen**.
    2. Voeg op het tabblad Beveiliging het computeraccount toe voor de server waarop u de connectors (**Microsoft Intune-connector** of **PFX-certificaatconnector voor Microsoft Intune**) uitvoert. 
    3. Verleen de machtigingen **Certificaten verlenen en beheren** en **Certificaten aanvragen** aan het computeraccount.

14. Meld u af bij de CA voor ondernemingen.

## <a name="download-install-and-configure-the-pfx-certificate-connector"></a>De PFX-certificaatconnector downloaden, installeren en configureren

Controleer voordat u begint de [beoordelingsvereisten voor de connector](certificate-connectors.md) en zorgt u ervoor dat uw omgeving en Windows-server klaar zijn voor de ondersteuning van de connector.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Tenantbeheer** > **Connectors en tokens** > **Certificaatconnectors** >  **+ Toevoegen**.

3. Klik op *De certificaatconnectorsoftware downloaden* voor de connector voor PKCS #12 en sla het bestand op op een locatie waartoe u toegang hebt vanaf de server waarop u de connector gaat installeren.

   ![Microsoft Intune-connector downloaden](./media/certficates-pfx-configure/download-connector.png)

4. Nadat het downloaden is voltooid, meldt u zich aan bij de server en voert u het installatieprogramma (PfxCertificateConnectorBootstrapper.exe) uit.  
   - Wanneer u de standaard installatielocatie accepteert, wordt de connector geïnstalleerd in `Program Files\Microsoft Intune\PFXCertificateConnector`.
   - De connectorservice wordt uitgevoerd onder het lokale systeemaccount. Als een proxy is vereist voor toegang tot internet, moet u bevestigen dat het lokale serviceaccount toegang heeft tot de proxy-instellingen op de server.

5. Het tabblad **Inschrijving** wordt na de installatie geopend. Als u de verbinding met Intune wilt inschakelen, kiest u **Aanmelden** en geeft u een account met globale beheerdersmachtigingen voor Azure of beheerdersbevoegdheden voor Intune op.

   > [!WARNING]
   > In Windows Server wordt **Configuratie verbeterde beveiliging IE** standaard ingesteld op **Ingeschakeld**, wat kan leiden tot aanmeldingsproblemen bij Office 365.

6. Sluit het venster.

7. Ga in het Microsoft Endpoint Manager-beheercentrum terug naar **Tenantbeheer** > **Connectors en tokens** > **Certificaatconnectors**. Even later wordt een groen vinkje weergegeven en wordt de verbindingsstatus bijgewerkt. Uw connector-server kan nu communiceren met Intune.

## <a name="create-a-trusted-certificate-profile"></a>Een vertrouwd certificaatprofiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Ga naar **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Voer de volgende eigenschappen in:
   - **Platform**: Kies het platform van de apparaten die dit profiel zullen ontvangen.
   - **Profiel**: Selecteer **Vertrouwd certificaat**
  
4. Selecteer **Maken**.

5. Voer in **Basisinformatie** de volgende eigenschappen in:
   - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld *Vertrouwd-certificaatprofiel voor hele bedrijf*.
   - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Geef bij **Configuratie-instellingen** het eerder geëxporteerde CER-bestand met het basis-CA-certificaat op.

   > [!NOTE]
   > Afhankelijk van het platform dat u in **stap 3** kiest, hebt u al dan niet de mogelijkheid het **Doelarchief** voor het certificaat te kiezen.

   ![Een profiel maken en een vertrouwd certificaat uploaden](./media/certficates-pfx-configure/certificates-pfx-configure-profile-fill.png)

8. Selecteer **Volgende**.

9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

   Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruiker of groepen die uw profiel zullen ontvangen. Plan de implementatie van dit certificaatprofiel zodat dit naar dezelfde groepen wordt geïmplementeerd die het PKCS-certificaatprofiel ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. (*Alleen van toepassing op Windows 10*) Geef in **Toepasselijkheidsregels**de toepasselijkheidsregels op om de toewijzing van dit profiel te verfijnen. U kunt ervoor kiezen om het profiel al dan niet toe te wijzen op basis van de versie van het besturingssysteem of een apparaat.

  Zie [Toepasselijkheidsregels](../configuration/device-profile-create.md#applicability-rules) in *Een apparaatprofiel maken in Microsoft Intune*voor meer informatie.

12. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u Maken selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="create-a-pkcs-certificate-profile"></a>Een PKCS-certificaatprofiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Ga naar **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Voer de volgende eigenschappen in:
   - **Platform**: Kies het platform van uw apparaten. Uw opties zijn:
     - Android-apparaatbeheerder
     - Android Enterprise > Volledig beheerd, toegewezen werkprofiel in bedrijfseigendom
     - Android Enterprise > Alleen werkprofiel
     - iOS/iPadOS
     - macOS
     - Windows 10 en hoger
   - **Profiel**: Selecteer **PKCS-certificaat**

   > [!NOTE]
   > Op apparaten met een Android Enterprise-profiel zijn certificaten die zijn geïnstalleerd met een PKCS-certificaatprofiel niet zichtbaar op het apparaat. Controleer de status van het profiel in de Intune-console om te controleren of de implementatie van het certificaat is geslaagd.
4. Selecteer **Maken**.

5. Voer in **Basisinformatie** de volgende eigenschappen in:
   - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld *PKCS-profiel voor hele bedrijf*.
   - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.
7. Welke instellingen u kunt configureren in **Configuratie-instellingen**, is afhankelijk van het platform dat u hebt gekozen. Selecteer uw platform voor gedetailleerde instellingen: -Android-apparaatbeheer -Android Enterprise -iOS/iPadOS -Windows 10
   
   |Instelling     | Platform     | Details   |
   |------------|------------|------------|
   |**Drempelwaarde voor verlenging (%)**        |<ul><li>Alle         |20% wordt aanbevolen  | 
   |**Geldigheidsduur van certificaat**  |<ul><li>Alle         |Als u de certificaatsjabloon niet hebt gewijzigd, kan deze optie worden ingesteld op één jaar. |
   |**Sleutelarchiefprovider (KSP)**   |<ul><li>Windows 10  |Voor Windows selecteert u waar u de sleutels op het apparaat wilt opslaan. |
   |**Certificeringsinstantie**      |<ul><li>Alle         |Geeft de interne FQDN (Fully Qualified Domain Name) van uw CA voor ondernemingen weer.  |
   |**Naam van certificeringsinstantie** |<ul><li>Alle         |Geeft de naam van uw CA voor ondernemingen weer, bijvoorbeeld "Contoso Certification Authority". |
   |**Certificaatsjabloonnaam**    |<ul><li>Alle         |Hier wordt de naam van uw certificaatsjabloon weergegeven. |
   |**Certificaattype**             |<ul><li>Android Enterprise (*Werkprofiel*)</li><li>iOS</li><li>macOS</li><li>Windows 10 en hoger|Selecteer een type: <ul><li> **Gebruiker**-certificaten kunnen zowel gebruikers- als apparaatkenmerken in het onderwerp ende SAN van het certificaat bevatten. </il><li>**Apparaat**-certificaten kunnen alleen apparaatkenmerken in het onderwerp en SAN van het certificaat bevatten. Gebruik Apparaat voor scenario's als apparaten zonder gebruiker, zoals kiosken of andere gedeelde apparaten.  <br><br> Deze selectie is van invloed op de indeling van de onderwerpnaam. |
   |**Indeling van de onderwerpnaam**          |<ul><li>Alle         |Zie [Indeling van de onderwerpnaam](#subject-name-format) verderop in dit artikel voor meer informatie over het configureren van de indeling van de onderwerpnaam.  <br><br> Voor de meeste platformen gebruikt u de optie **Algemene naam** tenzij anders aangegeven. <br><br>Voor de volgende platformen wordt de indeling van de onderwerpnaam bepaald door het certificaattype: <ul><li>Android Enterprise (*Werkprofiel*)</li><li>iOS</li><li>macOS</li><li>Windows 10 en hoger</li></ul>  <p>  |
   |**Alternatieve naam voor het onderwerp**     |<ul><li>Alle         |Bij *Kenmerk* selecteert u **User Principal Name (UPN)** tenzij anders vereist, configureert u een bijbehorende *Waarde* en klikt u vervolgens op **Toevoegen**. <br><br>Zie [Indeling van de onderwerpnaam](#subject-name-format) verderop in dit artikel voor meer informatie.|
   |**Uitgebreide-sleutelgebruik**           |<ul><li> Android-apparaatbeheerder </li><li>Android Enterprise (*Apparaateigenaar*, *Werkprofiel*) </li><li>Windows 10 |Certificaten vereisen meestal *Clientverificatie*, zodat de gebruiker of het apparaat bij een server kan worden geverifieerd. |
   |**Alle apps mogen toegang hebben tot de persoonlijke sleutel** |<ul><li>macOS  |Stel in op **Inschakelen** om apps die zijn geconfigureerd voor het bijbehorende Mac-apparaat toegang te geven tot de persoonlijke sleutel van de PKCS-certificaten. <br><br> Zie *AllowAllAppsAccess* in de sectie Nettolading van certificaat van [Referentiemateriaal configuratieprofiel](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf) in de Apple-documentatie voor ontwikkelaars voor meer informatie over deze instelling. |
   |**Basiscertificaat**             |<ul><li>Android-apparaatbeheerder </li><li>Android Enterprise (*Apparaateigenaar*, *Werkprofiel*) |Selecteer een basis-CA-certificaatprofiel dat eerder is toegewezen. |

8. Selecteer **Volgende**.

9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

   Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruiker of groepen die uw profiel zullen ontvangen. Plan de implementatie van dit certificaatprofiel zodanig dat het in dezelfde groepen wordt geïmplementeerd die het vertrouwde certificaatprofiel ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u Maken selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.


### <a name="subject-name-format"></a>Indeling van de onderwerpnaam

Wanneer u een PKCS-certificaatprofiel voor de volgende platformen maakt, zijn de opties voor de indeling van de onderwerpnaam afhankelijk van het certificaattype dat u selecteert, ofwel **Gebruiker** ofwel **Apparaat**.  

Platformen:

- Android Enterprise (*Werkprofiel*)
- iOS
- macOS
- Windows 10 en hoger

> [!NOTE]
> Er is een bekend probleem bij het gebruik van PKCS, [hetzelfde probleem dat ook bij SCEP optreedt](certificates-profile-scep.md#avoid-certificate-signing-requests-with-escaped-special-characters), om certificaten op te halen wanneer in de onderwerpnaam in de resulterende aanvraag voor certificaatondertekening (Certificate Signing Request, CSR) een van de volgende tekens staat na een escape-teken (een backslash \\):
> - \+
> - ;
> - ,
> - =

- **Certificaattype Gebruiker**  
  De indelingsopties voor de *Indeling van de onderwerpnaam* omvatten twee variabelen: **Algemene naam (CN)** en **E-mail (E)** . **Algemene naam (CN)** kan worden ingesteld op een van de volgende variabelen:

  - **CN={{UserName}}** : De user principal name van de gebruiker, bijvoorbeeld janedoe@contoso.com.
  - **CN={{AAD_Device_ID}}** : Een id die wordt toegewezen wanneer u een apparaat in Azure Active Directory (AD) registreert. Deze id wordt doorgaans gebruikt voor verificatie met Azure AD.
  - **CN={{SERIALNUMBER}}** : Het unieke serienummer (SN) dat doorgaans wordt gebruikt door de fabrikant om een apparaat te identificeren.
  - **CN={{IMEINumber}}** : Het unieke nummer van de International Mobile Equipment Identity (IMEI) dat wordt gebruikt om een mobiele telefoon te identificeren.
  - **CN={{OnPrem_Distinguished_Name}}** : Een reeks RDN's (Relative Distinguished Name), gescheiden door komma's, zoals *CN=Jane Doe,OU=UserAccounts,DC=corp,DC=contoso,DC=com*.

    Als u de variabele *{{OnPrem_Distinguished_Name}}* wilt gebruiken, moet u het gebruikerskenmerk *onpremisesdistinguishedname* met behulp van [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) synchroniseren met uw Azure AD.

  - **CN={{onPremisesSamAccountName}}** : Beheerders kunnen het kenmerk samAccountName van Active Directory met behulp van Azure AD Connect synchroniseren met Azure AD in een kenmerk met de naam *onPremisesSamAccountName*. Deze variabele kan in Intune worden vervangen als onderdeel van een aanvraag voor certificaatuitgifte in het onderwerp van een certificaat. Het kenmerk samAccountName is de aanmeldingsnaam van de gebruiker die wordt gebruikt ter ondersteuning van clients en servers van een oudere versie dan Windows 2000. De indeling voor de aanmeldingsnaam van de gebruiker is: *DomainName\testUser* of alleen *testUser*.

    Als u de variabele *{{onPremisesSamAccountName}}* wilt gebruiken, moet u het gebruikerskenmerk *onPremisesSamAccountName* met behulp van [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) synchroniseren met uw Azure AD.

  Door een combinatie van een of meer van deze variabelen en statische tekenreeksen te gebruiken, kunt u een aangepaste indeling voor de naam van een certificaathouder maken, bijvoorbeeld:  
  - **CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US**
  
  Dat voorbeeld bevat een indeling van de onderwerpnaam waarin gebruik wordt gemaakt van de variabelen CN en E, plus tekenreeksen voor de waarden Organizational Unit, Organization, Location, State en Country. [De functie CertStrToName](/windows/win32/api/wincrypt/nf-wincrypt-certstrtonamea) beschrijft deze functie en de ondersteunde tekenreeksen.

- **Certificaattype Apparaat**  
  Indelingsopties voor de Indeling van de onderwerpnaam zijn de volgende variabelen: 
  - **{{AAD_Device_ID}}**
  - **{{Device_Serial}}**
  - **{{Device_IMEI}}**
  - **{{SerialNumber}}**
  - **{{IMEINumber}}**
  - **{{AzureADDeviceId}}**
  - **{{WiFiMacAddress}}**
  - **{{IMEI}}**
  - **{{DeviceName}}**
  - **{{FullyQualifiedDomainName}}** *(Alleen van toepassing op Windows-apparaten en apparaten die aan een domein zijn toegevoegd)*
  - **{{MEID}}**

  U kunt deze variabelen opgeven in het tekstvak, gevolgd door de tekst voor de variabele. De algemene naam voor een apparaat met de naam *Device1* kan bijvoorbeeld worden toegevoegd als **CN={{DeviceName}}Device1**.

  > [!IMPORTANT]  
  > - Plaats bij het opgeven van een variabele de naam van de variabele tussen accolades {}, zoals in het voorbeeld te zien is, om fouten te voorkomen.  
  > - Apparaateigenschappen die worden gebruikt in het *onderwerp* of de *SAN* van een apparaatcertificaat, zoals **IMEI**, **SerialNumber** en **FullyQualifiedDomainName**, zijn eigenschappen die kunnen worden vervalst door een persoon die toegang tot het apparaat heeft.
  > - Een apparaat moet alle variabelen ondersteunen die zijn opgegeven in een certificaatprofiel, anders kan het profiel niet worden geïnstalleerd op het apparaat.  Als bijvoorbeeld **{{IMEI}}** wordt gebruikt in de onderwerpnaam van een SCEP-profiel en deze variabele wordt toegewezen aan een apparaat dat geen IMEI-nummer heeft, mislukt de installatie van het profiel.

## <a name="next-steps"></a>Volgende stappen

[Gebruik SCEP voor certificaten](certificates-scep-configure.md) of [verleen PKCS-certificaten via een webservice van Symantec PKI-manager](certificates-digicert-configure.md).

[Problemen met PKCS-certificaatprofielen oplossen](../protect/troubleshoot-pkcs-certificate-profiles.md)

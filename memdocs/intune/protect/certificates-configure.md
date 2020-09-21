---
title: Certificatenprofiel maken in Microsoft Intune - Azure | Microsoft Docs
description: Meer informatie het gebruik van SCEP-certificaatprofielen (Simple Certificate Enrollment Protocol) of PKCS-certificaatprofielen (Public Key Cryptography Standards) en certificaatprofielen met Microsoft Intune.
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
ms.assetid: 5eccfa11-52ab-49eb-afef-a185b4dccde1
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f91de698a518a8f8530ae42d5a8842d7876074a1
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076216"
---
# <a name="use-certificates-for-authentication-in-microsoft-intune"></a>Certificaten voor verificatie gebruiken in Microsoft Intune

Gebruik certificaten in Intune om uw gebruikers te verifiëren voor toepassingen en bedrijfsresources via een VPN-, Wi-Fi- of e-mailprofiel. Wanneer u certificaten gebruikt om deze verbindingen te verifiëren, hoeven uw eindgebruikers geen gebruikersnamen en wachtwoorden in te voeren, waardoor ze naadloos toegang kunnen krijgen. Certificaten worden ook gebruikt voor het ondertekenen en versleutelen van e-mail met behulp van S/MIME.

## <a name="intune-supported-certificates-and-usage"></a>Door Intune ondersteunde certificaten en ondersteund gebruik

| Type              | Verificatie | S/MIME-ondertekening | S/MIME-versleuteling  |
|--|--|--|--|
| Geïmporteerd PKCS-certificaat (Public Key Cryptography Standards) |  | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png)|
| PKCS #12 (of PFX)    | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) |  |
| Simple Certificate Enrollment Protocol (SCEP)  | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) | |

Als u deze certificaten wilt implementeren, moet u certificaatprofielen maken en deze toewijzen aan apparaten.

Elk afzonderlijk certificaatprofiel dat u maakt, ondersteunt één platform. Als u bijvoorbeeld PKCS-certificaten gebruikt, moet u een PKCS-certificaatprofiel voor Android en een afzonderlijk PKCS-certificaatprofiel voor iOS/iPadOS maken. Als u ook SCEP-certificaten voor deze twee platforms gebruikt, moet u een SCEP-certificaatprofiel voor Android en een ander SCEP-certificaatprofiel voor iOS/iPadOS maken.

### <a name="general-considerations-when-you-use-a-microsoft-certification-authority"></a>Algemene overwegingen als u een Microsoft-certificeringsinstantie gebruikt

Als u een Microsoft-certificeringsinstantie gebruikt (CA):

- SCEP-certificaatprofielen gebruiken:
  - [Stel een NDES-server (Network Device Enrollment Service) in](certificates-scep-configure.md#set-up-ndes) voor gebruik met Intune.
  - [Installeer de Microsoft Certificate Connector](certificates-scep-configure.md#install-the-microsoft-intune-connector).

- PKCS-certificaatprofielen gebruiken:
  - [Installeer de PFX-certificaatconnector voor Microsoft Intune](certficates-pfx-configure.md).
  
- Geïmporteerde PKCS-certificaten gebruiken:
  - [Installeer de PFX-certificaatconnector voor Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).
  - Exporteer certificaten van de certificeringsinstantie en importeer deze vervolgens in Microsoft Intune. Zie [het PowerShell-project PFXImport](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

- Certificaten implementeren met behulp van de volgende mechanismen:
  - [Vertrouwde certificaatprofielen](certificates-configure.md#create-trusted-certificate-profiles) om van het vertrouwde basis-CA-certificaat vanuit uw basis-CA of tussenliggende (verlenende) CA naar apparaten te implementeren
  - SCEP-certificaatprofielen
  - PKCS-certificaatprofielen
  - Geïmporteerde PKCS-certificaatprofielen

### <a name="general-considerations-when-you-use-a-third-party-certification-authority"></a>Algemene overwegingen als u een externe certificeringsinstantie gebruikt

Als u een externe (niet-Microsoft) certificeringsinstantie (CA) gebruikt:

- SCEP-certificaatprofielen gebruiken:
  - Stel integratie met een externe certificeringsinstantie in van [een van onze ondersteunde partners](certificate-authority-add-scep-overview.md#third-party-certification-authority-partners). Dit instellen omvat het volgen van de instructies van de externe certificeringsinstantie waardoor de integratie van hun CA met Intune wordt voltooid.
  - [Maak een toepassing in Azure AD](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration) die de rechten voor Intune delegeert zodat de validatie van de SCEP-certificaatverificatievraag kan worden uitgevoerd.

- Voor geïmporteerde PKCS-certificaten moet u de [PFX-certificaatconnector voor Microsoft Intune installeren](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).

- Certificaten implementeren met behulp van de volgende mechanismen:
  - [Vertrouwde certificaatprofielen](certificates-configure.md#create-trusted-certificate-profiles) om van het vertrouwde basis-CA-certificaat vanuit uw basis-CA of tussenliggende (verlenende) CA naar apparaten te implementeren
  - SCEP-certificaatprofielen
  - PKCS-certificaatprofielen *(alleen ondersteund voor het [Digicert PKI-platform](certificates-digicert-configure.md))*
  - Geïmporteerde PKCS-certificaatprofielen

## <a name="supported-platforms-and-certificate-profiles"></a>Ondersteunde platforms en certificaatprofielen

| Platform              | Vertrouwd certificaatprofiel | PKCS-certificaatprofiel | SCEP-certificaatprofiel | Geïmporteerd PKCS-certificaatprofiel  |
|--|--|--|--|---|
| Android-apparaatbeheerder | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png)|  ![Ondersteund](./media/certificates-configure/green-check.png) |
| Android Enterprise <br> - Volledig beheerd (apparaateigenaar)   | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png)  | ![Ondersteund](./media/certificates-configure/green-check.png) |  ![Ondersteund](./media/certificates-configure/green-check.png)  |
| Android Enterprise <br> - Toegewezen (apparaateigenaar)   | ![Ondersteund](./media/certificates-configure/green-check.png)  | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png)  | ![Ondersteund](./media/certificates-configure/green-check.png)|
| Android Enterprise <br> Werkprofiel in bedrijfseigendom   | ![Ondersteund](./media/certificates-configure/green-check.png)  | ![Ondersteund](./media/certificates-configure/green-check.png)  | ![Ondersteund](./media/certificates-configure/green-check.png)  | ![Ondersteund](./media/certificates-configure/green-check.png)  |
| Android Enterprise <br> - Werkprofiel    | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) |
| iOS/iPadOS                   | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) |
| macOS                 | ![Ondersteund](./media/certificates-configure/green-check.png) |  ![Ondersteund](./media/certificates-configure/green-check.png) |![Ondersteund](./media/certificates-configure/green-check.png)|![Ondersteund](./media/certificates-configure/green-check.png)|
| Windows 8.1 en hoger |![Ondersteund](./media/certificates-configure/green-check.png)  |  |![Ondersteund](./media/certificates-configure/green-check.png) |   |
| Windows 10 en hoger  | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) | ![Ondersteund](./media/certificates-configure/green-check.png) |

## <a name="export-the-trusted-root-ca-certificate"></a>Het vertrouwde basis-CA-certificaat exporteren

Als u geïmporteerde PKCS-, SCEP- en PKCS-certificaten wilt gebruiken, moeten apparaten uw basiscertificeringsinstantie vertrouwen. Als u vertrouwen tot stand wilt brengen, exporteert u het certificaat van de vertrouwde basis-CA, evenals tussenliggende certificaten of certificaten van verlenende certificeringsinstanties, als een openbaar certificaat (.cer). U kunt deze certificaten ophalen bij de verlenende CA of vanaf elk apparaat dat uw verlenende CA vertrouwt.

Raadpleeg de documentatie van uw certificeringsinstantie om het certificaat te exporteren. U moet het openbare certificaat exporteren als een CER-bestand.  Exporteer niet de persoonlijke sleutel (een PFX-bestand).

U gebruikt dit CER-bestand wanneer u [vertrouwde certificaatprofielen](#create-trusted-certificate-profiles) maakt om dat certificaat op uw apparaten te implementeren.

## <a name="create-trusted-certificate-profiles"></a>profielen voor vertrouwde certificaten maken

U moet een vertrouwd certificaatprofiel maken en implementeren voordat u een SCEP-, PKCS- of geïmporteerd PKCS-certificaatprofiel maakt. Wanneer u een vertrouwd certificaatprofiel implementeert naar dezelfde groepen die de andere typen certificaatprofiel ontvangen, zorgt u ervoor dat elk apparaat de geldigheid van uw certificeringsinstantie kan herkennen. Dit omvat profielen zoals die voor VPN, Wi-Fi en e-mail.

SCEP-certificaat profielen verwijzen rechtstreeks naar een vertrouwd certificaatprofiel. PKCS-certificaatprofielen verwijzen niet rechtstreeks naar het vertrouwde certificaatprofiel, maar wel naar de server die als host fungeert voor uw CA. Geïmporteerde PKCS-certificaatprofielen verwijzen niet rechtstreeks naar het vertrouwde certificaatprofiel, maar kunnen er wel gebruik van maken op het apparaat. Het implementeren van een vertrouwd certificaatprofiel op apparaten zorgt ervoor dat deze vertrouwensrelatie tot stand wordt gebracht. Wanneer een apparaat de basis-CA niet vertrouwt, mislukt het SCEP- of PKCS-certificaatprofielbeleid.

Maak een afzonderlijk vertrouwd certificaatprofiel voor elk apparaatplatform dat u wilt ondersteunen, net zoals u dat voor SCEP-, PKCS- en geïmporteerde PKCS-certificaatprofielen gaat doen.

> [!IMPORTANT]
> Vertrouwde basisprofielen die u maakt voor het platform *Windows 10 en hoger*, worden in het Microsoft Endpoint Manager-beheercentrum weergegeven voor het platform *Windows 8.1 en hoger*. 
>
> Dit is een bekend probleem met de presentatie van het platform voor vertrouwde certificaatprofielen. Terwijl in het profiel het platform Windows 8.1 en hoger wordt weergegeven, is het functioneel voor Windows 10 en hoger.

> [!NOTE]
> Het profiel *vertrouwd certificaat* in Intune kan alleen worden gebruikt voor het leveren van basiscertificaten of tussenliggende certificaten. De implementatie van dergelijke certificaten is bedoeld om een vertrouwensketen tot stand te brengen. Het gebruik van het vertrouwd certificaat-profiel voor het leveren van andere certificaten dan basiscertificaten of tussenliggende certificaten wordt niet door Microsoft ondersteund. Mogelijk kunt u geen certificaten importeren die niet als basiscertificaten of tussenliggende certificaten worden beschouwd als u het vertrouwd certificaat-profiel in de Intune-portal selecteert. Zelfs als u met dit profieltype een certificaat kunt importeren en implementeren dat geen basiscertificaat of tussenliggend certificaat is, zult u waarschijnlijk onverwachte resultaten ondervinden tussen verschillende platformen, zoals iOS en Android.

### <a name="to-create-a-trusted-certificate-profile"></a>Een profiel voor een vertrouwd certificaat maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Ga naar **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

   ![Ga naar Intune en maak een nieuw profiel voor een vertrouwd certificaat](./media/certificates-configure/certificates-configure-profile-new.png)

3. Voer de volgende eigenschappen in:
   - **Platform**: Kies het platform van de apparaten die dit profiel zullen ontvangen.
   - **Profiel**: Selecteer **Vertrouwd certificaat**
  
4. Selecteer **Maken**.

5. Voer in **Basisinformatie** de volgende eigenschappen in:
   - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld *Vertrouwd-certificaatprofiel voor hele bedrijf*.
   - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Geef bij **Configuratie-instellingen** het eerder geëxporteerde CER-bestand van het vertrouwde basis-CA-certificaat op. 

   Voor Windows 8.1- en Windows 10-apparaten selecteert u het **doelarchief** voor het vertrouwde certificaat vanuit:

   - **Certificaatarchief van de computer – basis**
   - **Certificaatarchief van de computer – tijdelijk**
   - **Certificaatarchief van de gebruiker – tijdelijk**

   ![Een profiel maken en een vertrouwd certificaat uploaden](./media/certificates-configure/certificates-configure-profile-fill.png)

8. Selecteer **Volgende**.

9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

   Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruiker of groepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. (*Alleen van toepassing op Windows 10*) Geef in **Toepasselijkheidsregels**de toepasselijkheidsregels op om de toewijzing van dit profiel te verfijnen. U kunt ervoor kiezen om het profiel al dan niet toe te wijzen op basis van de versie van het besturingssysteem of een apparaat.

  Zie [Toepasselijkheidsregels](../configuration/device-profile-create.md#applicability-rules) in *Een apparaatprofiel maken in Microsoft Intune*voor meer informatie.

12. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u Maken selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="additional-resources"></a>Extra resources

- [Apparaatprofielen toewijzen](../configuration/device-profile-assign.md)  
- [S/MIME gebruiken om e-mailberichten te ondertekenen en te versleutelen](certificates-s-mime-encryption-sign.md)  
- [Een externe certificeringsinstantie gebruiken](certificate-authority-add-scep-overview.md)  

## <a name="next-steps"></a>Volgende stappen

Maak SCEP-, PKCS- of geïmporteerde PKCS-certificaatprofielen voor elk platform dat u wilt gebruiken. Raadpleeg de volgende artikelen om verder te gaan:

- [Infrastructuur configureren om SCEP-certificaten te ondersteunen in Intune](certificates-scep-configure.md)  
- [PKCS-certificaten configureren en beheren met Intune](certficates-pfx-configure.md)  
- [Een geïmporteerd PKCS-certificaatprofiel maken](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)

Meer informatie over [certificaatconnectors](certificate-connectors.md)
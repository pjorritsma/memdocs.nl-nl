---
title: Problemen met het gebruik van PKCS-certificaatprofielen oplossen om certificaten in te richten met Microsoft Intune | Microsoft Docs
description: Problemen met het gebruik van profielen voor persoonlijke en openbare sleutelparen (PKCS) op apparaten oplossen om certificaten aan te vragen voor gebruik met Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: acc61df344cb4134a863d75fff517047e78d067d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914783"
---
# <a name="troubleshoot-pkcs-certificate-deployment-in-microsoft-intune"></a>Problemen met de implementatie van PKCS-certificaten oplossen in Microsoft Intune

De informatie in dit artikel kan u helpen verschillende veelvoorkomende problemen op te lossen wanneer u certificaten voor persoonlijke en openbare sleutelparen (PKCS) implementeert in Microsoft Intune. Vóórdat u problemen gaat oplossen, moet u ervoor zorgen dat u de volgende taken hebt voltooid, zoals beschreven in [PKCS-certificaten configureren en gebruiken met Intune](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca):

- De [vereisten voor het gebruik van PKCS-certificaatprofielen](../protect/certficates-pfx-configure.md#requirements) bekijken
- Het basiscertificaat exporteren vanuit de CA (certificeringsinstantie) voor ondernemingen
- Certificaatsjablonen configureren bij de certificeringsinstantie
- De Intune Certificate Connector installeren en configureren
- Een vertrouwd certificaatprofiel maken en implementeren om het basiscertificaat te implementeren
- Een PKCS-certificaatprofiel maken en implementeren

De meest voorkomende bron van problemen voor PKCS-certificaatprofielen heeft betrekking op de configuratie van het PKCS-certificaatprofiel. Controleer de configuratie van het profiel en zoek naar foutjes in de servernamen of FQDN's (Fully Qualified Domain Name), en bevestig dat de **certificeringsinstantie** en de **naam van de certificeringsinstantie** juist zijn.

- **Certificeringsinstantie**: De interne FQDN van de certificeringsinstantiecomputer. Bijvoorbeeld server1.domain.local.
- **Naam van certificeringsinstantie**: De naam van de certificeringsinstantie, zoals die wordt weergegeven in de MMC voor de certificeringsinstantie. Kijk onder **Certificeringsinstantie (lokaal)**

U kunt het [opdrachtregelprogramma certutil](/windows-server/administration/windows-commands/certutil) in de CA gebruiken om de juiste certificeringsinstantie en naam voor de certificeringsinstantie te bevestigen.

## <a name="pkcs-communication-overview"></a>Overzicht van PKCS-communicatie

De volgende afbeelding bevat een basisoverzicht van het implementatieproces voor het PKCS-certificaat in Intune.

> [!div class="mx-imgBorder"]
> ![Stroom van PKCS-certificaatprofiel](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. Een beheerder maakt een PKCS-certificaatprofiel in Intune.
2. De Intune-service vraagt aan dat via de on-premises Intune Certificate Connector een nieuw certificaat voor de gebruiker wordt gemaakt.
3. Via de Intune Certificate Connector worden een PFX-blob en -aanvraag verzonden naar uw certificeringsinstantie van Microsoft.
4. De certificeringsinstantie verleent en verzendt het PFX-gebruikerscertificaat terug naar de Intune Certificate Connector.
5. Met de Intune Certificate Connector wordt het versleutelde PFX-gebruikerscertificaat geüpload naar Intune.
6. Met Intune wordt het PFX-gebruikerscertificaat ontsleuteld en opnieuw versleuteld voor het apparaat, met behulp van het apparaatbeheercertificaat.  Intune verzendt het PFX-gebruikerscertificaat vervolgens naar het apparaat.
7. Het apparaat rapporteert de certificaatstatus aan Intune.

## <a name="data-and-log-files"></a>Gegevens en logboekbestanden

Als u problemen wilt identificeren voor de werkstroom voor communicatie en inrichting van certificaten, bekijkt u de logboekbestanden van zowel de serverinfrastructuur als van apparaten. In latere secties voor het oplossen van problemen met PKCS-certificaatprofielen komen logboekbestanden aan de orde waarnaar in deze sectie wordt verwezen.

- [Infrastructuur- en serverlogboeken](#logs-for-on-premises-infrastructure)

Apparaatlogboeken zijn afhankelijk van het platform van het apparaat:

- [iOS en iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>Logboeken voor on-premises infrastructuur
  
Een on-premises infrastructuur die ondersteuning biedt voor het gebruik van PKCS-certificaatprofielen voor certificaatimplementaties, omvat de Microsoft Intune Certificate Connector, NDES die wordt uitgevoerd op een Windows Server, en de certificeringsinstantie.

Logboekbestanden voor deze rollen omvatten onder andere Windows Logboeken, certificaatconsoles en verschillende logboekbestanden die specifiek zijn voor de Intune Certificate Connector, NDES of andere functies en bewerkingen die deel uitmaken van de on-premises infrastructuur.

- **NDESConnector_date_time.svclog**:

  In dit logboek wordt communicatie van de Microsoft Intune Certificate Connector met de Intune-cloudservice weergegeven. U kunt de [viewer voor servicetraceringen](/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) gebruiken om dit logboekbestand weer te geven.

  Gerelateerde registersleutel: *HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  Locatie: Op de server die als host fungeert voor NDES in *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **CertificateRegistrationPoint_date_time.svclog**:

  In dit logboek wordt de NDES-beleidsmodule die certificaataanvragen ontvangt en verifieert weergegeven. U kunt de [viewer voor servicetraceringen](/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) gebruiken om dit logboekbestand weer te geven.

  Locatie: Op de server die als host fungeert voor NDES in *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **NDESPlugin.log**:

  In dit logboek wordt het doorgeven van certificaataanvragen aan het certificaatregistratiepunt en de resulterende verificatie van deze aanvragen weergegeven.

  Locatie: Op de server die als host fungeert voor NDES in *%program_files%\Microsoft Intune\NDESPolicyModule\logs*

- **Windows-logboek**:

  Locatie: Op de server die als host fungeert voor NDES: voer **eventvwr. msc** uit om Windows Logboeken te openen

### <a name="logs-for-android-devices"></a>Logboeken voor Android-apparaten

Voor apparaten met Android gebruikt u het **Android-bedrijfsportal**, app-logboekbestand **OMADM. log**. Voordat u logboeken verzamelt en bekijkt, moet u ervoor zorgen dat [Uitgebreide logboekregistratie](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md) is ingeschakeld en reproduceert u vervolgens het probleem.

Zie [Logboeken uploaden en e-mailen via een USB-kabel](../user-help/send-logs-to-your-it-admin-using-cable-android.md) voor informatie over het verzamelen van de OMADM.-logboeken van een apparaat.

U kunt [logboeken ook uploaden en e-mailen](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app) naar de ondersteuningsafdeling.

### <a name="logs-for-ios-and-ipados-devices"></a>Logboeken voor iOS- en iPadOS-apparaten

Voor apparaten waarop iOS/iPadOS wordt uitgevoerd, gebruikt u logboeken voor foutopsporing en **Xcode** die wordt uitgevoerd op een Mac-computer:

1. Verbind het iOS/iPadOS-apparaat met Mac en ga vervolgens naar **Toepassingen** > **Hulpprogramma's** om de console-app te openen.

2. Selecteer onder **Actie** de opties **Infoberichten opnemen** en  **Foutopsporingsberichten opnemen**.

   ![Logboekopties selecteren](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. Reproduceer het probleem en sla de logboeken op in een tekstbestand:
   1. Selecteer **Bewerken** > **Alles selecteren** om alle berichten op het huidige scherm te selecteren en selecteer vervolgens **Bewerken** > **Kopiëren** om de berichten naar het klembord te kopiëren.
   2. Open de toepassing TextEdit, plak de gekopieerde logboeken in een nieuw tekstbestand en sla het bestand op.

Het bedrijfsportal-logboek voor iOS- en iPadOS-apparaten bevat geen informatie over PKCS-certificaatprofielen.

### <a name="logs-for-windows-devices"></a>Logboeken voor Windows-apparaten

Voor apparaten waarop Windows wordt uitgevoerd, gebruikt u de Windows-gebeurtenislogboeken om problemen met registratie of apparaatbeheer op te sporen voor apparaten die u met Intune beheert.

Open **Logboeken** > **Logboeken Toepassingen en Services** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider**

![Windows-gebeurtenislogboeken](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## <a name="antivirus-exclusions"></a>Antivirussoftware-uitsluitingen

U kunt antivirusuitsluitingen toevoegen aan servers die als host voor NDES of de certificaatconnector fungeren wanneer:

- Certificaataanvragen de server of de Intune-certificaatconnector bereiken, maar niet worden verwerkt 
- Certificaten langzaam worden uitgegeven

Hieronder ziet u enkele voorbeelden van locaties die u kunt uitsluiten:

- *%program_files%* \Microsoft Intune\PfxRequest
- *%program_files%* \Microsoft Intune\CertificateRequestStatus
- *%program_files%* \Microsoft Intune\CertificateRevocationStatus

## <a name="common-errors"></a>Algemene fouten

De volgende veelvoorkomende fouten worden behandeld in een van de volgende secties:

- [De RPC-server is niet beschikbaar 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [Er kan geen inschrijvingsbeleidsserver worden gevonden 0x80094015](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [De verzending is in behandeling](#the-submission-is-pending)
- [De parameter is onjuist 0x80070057](#the-parameter-is-incorrect-0x80070057)
- [Geweigerd door beleidsmodule](#denied-by-policy-module)
- [Certificaatprofiel blijft hangen op In behandeling](#certificate-profile-stuck-as-pending)
- [Fout -2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED](#error--2146875374-certsrv_e_subject_email_required)

### <a name="the-rpc-server-is-unavailable-0x800706ba"></a>De RPC-server is niet beschikbaar 0x800706ba

Tijdens de PFX-implementatie wordt het vertrouwde basiscertificaat weergegeven op het apparaat, maar het PFX-certificaat verschijnt niet op het apparaat. Het NDESConnector-logboekbestand bevat de tekenreeks **De RPC-server is niet beschikbaar. 0x800706ba**, zoals te zien is in de eerste regel van het volgende voorbeeld:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

#### <a name="cause-1---incorrect-configuration-of-the-ca-in-intune"></a>Oorzaak 1: onjuiste configuratie van de CA in Intune

Dit probleem kan optreden wanneer het PKCS-certificaatprofiel de verkeerde server opgeeft, of wanneer deze spelfouten bevat voor de naam of FQDN van de CA. De CA wordt opgegeven in de volgende eigenschappen van het profiel:

- Certification authofity
- Naam van certificeringsinstantie

**Oplossing**:

Controleer de volgende instellingen en pas ze aan als ze onjuist zijn:

- De eigenschap **Certificeringsinstantie** geeft de interne FQDN van de CA-server weer.
- De eigenschap **Naam van certificeringsinstantie** geeft de naam van de CA weer.

#### <a name="cause-2---ca-doesnt-support-certificate-renewal-for-requests-signed-by-previous-ca-certificates"></a>Oorzaak 2: CA biedt geen ondersteuning voor het vernieuwen van certificaten voor aanvragen die zijn ondertekend met eerdere CA-certificaten

Als de FQDN en naam van de CA in het PKCS-certificaatprofiel juist zijn, controleert u het Windows-toepassingslogboek dat zich op de certificeringsinstantieserver bevindt. Zoek naar een **Gebeurtenis-id 128** die lijkt op het volgende voorbeeld:

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

Wanneer het CA-certificaat wordt vernieuwd, moet het OCSP-antwoordcertificaat voor ondertekenen (Online Certificate Status Protocol) ermee zijn ondertekend. Door te ondertekenen kunnen andere certificaten met het OCSP-antwoordcertificaat voor ondertekenen worden gevalideerd, door de bijbehorende intrekkingsstatus te controleren. Deze handtekening is niet standaard ingeschakeld.

**Oplossing**:

Ondertekenen van het certificaat handmatig afdwingen:

1. Open op de CA-server een verhoogde opdrachtprompt en voer de volgende opdracht uit: **certutil -setreg ca\UseDefinedCACertInRequest 1**
2. Start de Certificate Services-service opnieuw.

Nadat de Certificate Services-service opnieuw is gestart, kunnen apparaten certificaten ontvangen.

### <a name="an-enrollment-policy-server-cannot-be-located-0x80094015"></a>Er kan geen inschrijvingsbeleidsserver worden gevonden 0x80094015

**Er kan geen inschrijvingsbeleidsserver worden gevonden** en **0x80094015**, zoals weergegeven in het volgende voorbeeld:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094015): An enrollment policy server cannot be located. (Exception from HRESULT: 0x80094015)
```

#### <a name="cause---certificate-enrollment-policy-server-name"></a>Oorzaak: naam van certificaatinschrijvingsbeleidsserver

Dit probleem treedt op als de computer die als host fungeert voor de Intune NDES-connector, geen certificaatinschrijvingsbeleidsserver kan vinden.

**Oplossing**:

Configureer handmatig de naam van certificaatinschrijvingsbeleidsserver op de computer die als host fungeert voor de NDES-connector. Gebruik de PowerShell-cmdlet [add-CertificateEnrollmentPolicyServer](/powershell/module/pkiclient/add-certificateenrollmentpolicyserver?view=win10-ps) om de naam te configureren.

### <a name="the-submission-is-pending"></a>De verzending is in behandeling

Nadat u een PKCS-certificaatprofiel hebt geïmplementeerd op mobiele apparaten, worden de certificaten niet opgehaald. Het NDESConnector-logboek bevat de tekenreeks **De verzending is in behandeling**, zoals weergegeven in het volgende voorbeeld:

```
IssuePfx - The submission is pending: Taken Under Submission
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission is pending
```

Daarnaast ziet u op de certificeringsinstantieserver de PFX-aanvraag in de map **Aanvragen in behandeling**:

> [!div class="mx-imgBorder"]
> ![Schermopname van de certificeringsinstantiemap Aanvragen in behandeling](./media/troubleshoot-pkcs-certificate-profiles/pending-requests.png)

#### <a name="cause---incorrect-configuration-for-request-handling"></a>Oorzaak: onjuiste configuratie voor afhandeling van aanvragen

Dit probleem treedt op als de optie **Status van de certificaataanvraag instellen op In behandeling. De beheerder moet dit certificaat expliciet verlenen.** is geselecteerd in het dialoogvenster **Eigenschappen** > **Beleidsmodule** > **Eigenschappen** van de certificeringsinstantie.

> [!div class="mx-imgBorder"]
> ![Schermopname van de beleidsmodule-eigenschappen](./media/troubleshoot-pkcs-certificate-profiles/policy-module-properties.png)

**Oplossing**:

Bewerk de beleidsmodule-eigenschappen naar: **Volg de instellingen in het certificaatsjabloon, indien van toepassing. Als dit niet het geval is, verleent u het certificaat automatisch.**

### <a name="the-parameter-is-incorrect-0x80070057"></a>De parameter is onjuist 0x80070057

Nu de Intune Certificate Connector is geïnstalleerd en geconfigureerd, ontvangen apparaten geen PKCS-certificaten. Het NDESConnector-logboek bevat de tekenreeks **De parameter is onjuist. 0x80070057**, zoals weergegeven in het volgende voorbeeld:

```
CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
```

#### <a name="cause---configuration-of-the-pkcs-profile"></a>Oorzaak: configuratie van het PKCS-profiel

Dit probleem treedt op als het PKCS-profiel in Intune onjuist is geconfigureerd. Hier volgen enkele veelvoorkomende onjuiste configuraties:

- Het profiel bevat een onjuiste naam voor de CA.
- De SAN (alternatieve naam voor onderwerp) is geconfigureerd voor e-mailadres, maar de doelgebruiker heeft nog geen geldig e-mailadres. Deze combinatie resulteert in een null-waarde voor de SAN, wat ongeldig is.

**Oplossing**:

Controleer de volgende configuraties voor het PKCS-profiel. Wacht vervolgens tot het beleid is vernieuwd op het apparaat:

- Geconfigureerd met de naam van de CA
- Toegewezen aan de juiste gebruikersgroep
- Gebruikers in de groep hebben geldige e-mailadressen

Zie [PKCS-certificaten configureren en gebruiken met Intune](../protect/certficates-pfx-configure.md) voor meer informatie.

### <a name="denied-by-policy-module"></a>Geweigerd door beleidsmodule

Wanneer apparaten het vertrouwde basiscertificaat ontvangen, maar het PFX-certificaat niet ontvangen. Het NDESConnector-logboek bevat de tekenreeks **De verzending is mislukt: Geweigerd door beleidsmodule**, zoals weergegeven in het volgende voorbeeld:

```
IssuePfx - The submission failed: Denied by Policy Module
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission failed
   at Microsoft.Management.Services.NdesConnector.MicrosoftCA.GetCertificate(PfxRequestDataStorage pfxRequestData, String containerName, String& certificate, String& password)
Issuing Pfx certificate for Device ID <Device ID> failed  
```

#### <a name="cause--computer-account-permissions-to-the-certificate-template"></a>Oorzaak: machtigingen voor computeraccounts voor de certificaatsjabloon

Dit probleem treedt op wanneer het computeraccount van de server die als host fungeert voor de Intune Certificate Connector, geen machtigingen heeft voor de certificaatsjabloon.

**Oplossing**:

1. Meld u aan bij uw CA voor ondernemingen met een account met beheerdersbevoegdheden.
2. Open de console **Certificeringsinstantie**, klik met de rechtermuisknop op **Certificaatsjablonen en selecteer Beheren**.
3. Ga naar de certificaatsjabloon en open het dialoogvenster **Eigenschappen** van de sjabloon.
4. Selecteer het tabblad **Beveiliging** en voeg het computeraccount toe voor de server waarop u de Microsoft Intune Certificate Connector hebt geïnstalleerd. Verleen dit account machtigingen voor **Lezen** en **Inschrijven**.
5. Selecteer **Toepassen** > **OK** om de certificaatsjabloon op te slaan, en sluit vervolgens de console **Certificaatsjablonen**.
6. Klik in de **certificeringsinstantieconsole** met de rechtermuisknop op **Certificaatsjablonen** > , klik op **Nieuw** >  en klik vervolgens op **Te verlenen certificaatsjablonen**.
7. Selecteer de sjabloon die u hebt gewijzigd, en klik vervolgens op **OK**.

Zie [Certificaatsjablonen configureren op de CA](../protect/certficates-pfx-configure.md#configure-certificate-templates-on-the-ca) voor meer informatie.

### <a name="certificate-profile-stuck-as-pending"></a>Certificaatprofiel blijft hangen op In behandeling

In het Microsoft Endpoint Manager-beheercentrum mislukt het implementeren van PKCS-certificaatprofielen met een status **In behandeling**. Er zijn geen duidelijke fouten in het NDESConnector-logboekbestand.
Omdat de oorzaak van dit probleem niet duidelijk wordt geïdentificeerd in logboeken, kunt u de volgende oorzaken nagaan.

#### <a name="cause-1---unprocessed-request-files"></a>Oorzaak 1: niet-verwerkte aanvraagbestanden

Controleer de aanvraagbestanden op fouten die aangeven waarom het verwerken is mislukt.

1. Gebruik op de computer die als host fungeert voor de NDES-connector, Bestandenverkenner om naar **%programfiles%\Microsoft Intune\PfxRequest** te navigeren.
2. Bekijk bestanden in de mappen **Mislukt** en **Verwerkingen**, met behulp van uw favoriete teksteditor.

   > [!div class="mx-imgBorder"]
   > ![De map PfxRequest controleren](./media/troubleshoot-pkcs-certificate-profiles/pfxrequest-folder.png)

3. Zoek in deze bestanden naar vermeldingen die duiden op fouten of mogelijke problemen. Zoek met behulp van een webzoekactie in de foutberichten naar aanwijzingen over waarom de verwerking van de aanvraag is mislukt, en naar oplossingen voor deze problemen.

#### <a name="cause-2---misconfiguration-for-the-pkcs-certificate-profile"></a>Oorzaak 2: onjuiste configuratie van het PKCS-certificaatprofiel

Als u geen aanvraagbestanden hebt gevonden in de mappen **Mislukt**, **Verwerkingen** of **Geslaagd**, kan het zijn dat het verkeerde certificaat is gekoppeld aan het PKCS-certificaatprofiel. Een onderliggende CA kan bijvoorbeeld zijn gekoppeld aan het profiel, of het verkeerde basiscertificaat kan zijn gebruikt.

**Oplossing**:

1. Controleer het vertrouwde certificaatprofiel om er zeker van te zijn dat u het basiscertificaat vanuit de CA voor ondernemingen hebt geïmplementeerd op apparaten.
2. Controleer het PKCS-certificaatprofiel om er zeker van te zijn dat dit verwijst naar de juiste CA, en naar het juiste certificaattype en vertrouwde certificaatprofiel waarmee het basiscertificaat wordt geïmplementeerd op apparaten.

Raadpleeg [Certificaten gebruiken voor verificatie](../protect/certificates-configure.md) in Microsoft Intune voor meer informatie.

### <a name="error--2146875374-certsrv_e_subject_email_required"></a>Fout -2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED

Implementeren van PKCS-certificaten mislukt, en de certificaatconsole op de verlenende CA geeft een bericht weer met de tekenreeks **-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED**, zoals weergegeven in het volgende voorbeeld:

```
Active Directory Certificate Services denied request abc123 because The Email name is unavailable and cannot be added to the Subject or Subject Alternate name. 0x80094812 (-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED). The request was for CN=” Common Name”.  Additional information: Denied by Policy Module”.
```

#### <a name="cause---supply-in-the-request-is-miscongifured"></a>Oorzaak: 'Met de aanvraag meeleveren' is onjuist geconfigureerd

Dit probleem doet zich voor als de optie **Met de aanvraag meeleveren** niet is ingeschakeld op het tabblad **Onderwerpnaam** in het dialoogvenster **Eigenschappen** van de certificaatsjabloon.

> [!div class="mx-imgBorder"]
> ![De NDES-eigenschappen configureren](./media/troubleshoot-pkcs-certificate-profiles/supply-in-the-request.png)

**Oplossing**:

Bewerk de sjabloon om het configuratieprobleem op te lossen:

1. Meld u aan bij uw CA voor ondernemingen met een account met beheerdersbevoegdheden.
2. Open de console **Certificeringsinstantie**, klik met de rechtermuisknop op **Certificaatsjablonen** en selecteer **Beheren**.
3. Open het dialoogvenster Eigenschappen van de certificaatsjabloon.
4. Selecteer op het tabblad **Onderwerpnaam** de optie **Met de aanvraag meeleveren**.
5. Selecteer **OK** om de certificaatsjabloon op te slaan, en sluit vervolgens de console **Certificaatsjablonen**.
6. Klik in de console **Certificeringsinstantie** met de rechtermuisknop op **Sjablonen** > **Nieuw** >  **en klik vervolgens op Te verlenen certificaatsjablonen**.
7. Selecteer de sjabloon die u hebt gewijzigd, en selecteer vervolgens **OK**.

## <a name="next-steps"></a>Volgende stappen

Als u nog steeds een oplossing nodig hebt of als u meer informatie wilt over Intune, kunt u een vraag posten op ons [Microsoft Intune-forum](https://social.technet.microsoft.com/Forums/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Veel technische ondersteuningsmedewerkers, MVP's en leden van ons ontwikkelingsteam bezoeken de forums regelmatig. Er bestaat dus een goede kans dat iemand kan helpen.

Raadpleeg [Ondersteuning krijgen voor Microsoft Intune](../fundamentals/get-support.md) als u een ondersteuningsaanvraag bij het Microsoft Intune-productondersteuningsteam wilt openen.
Zie de volgende artikelen voor meer informatie over de implementatie van een PKCS-certificaat:

- [PKCS-certificaten configureren en gebruiken met Intune](../protect/certficates-pfx-configure.md)
- [Een certificaatprofiel configureren voor uw apparaten in Microsoft Intune](../protect/certificates-configure.md)
- [SCEP- en PKCS-certificaten verwijderen in Microsoft Intune](../protect/remove-certificates.md)
---
title: iOS-/iPadOS-apparaten inschrijven - Device Enrollment Program
titleSuffix: Microsoft Intune
description: Meer informatie over het registreren van iOS-/iPadOS-apparaten in bedrijfseigendom met het Device Enrollment Program (DEP).
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2db33dbe94ff5aef62563531149250fbd4268acc
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986978"
---
# <a name="automatically-enroll-iosipados-devices-with-apples-automated-device-enrollment"></a>iOS-/iPadOS-apparaten automatisch inschrijven met Automated Device Enrollment van Apple

> [!IMPORTANT]
> Apple is recent overgestapt van het Apple Device Enrollment Program (DEP) naar Apple Automated Device Enrollment (ADE). In verband hiermee wordt de gebruikersinterface van Intune momenteel bijgewerkt. Totdat deze aanpassingen zijn voltooid, wordt *Device Enrollment Program* in de Intune-portal weergegeven. Waar Automatische apparaatinschrijving (Automated Device Enrollment) wordt weergegeven, wordt dit gebruikt.

U kunt Intune zo instellen dat iOS-/iPadOS-apparaten die zijn gekocht via [Automated Device Enrollment (ADE)](https://deploy.apple.com) van Apple (voorheen het Device Enrollment Program) worden ingeschreven. Met Automated Device Enrollment kunt u grote aantallen apparaten inschrijven zonder op de apparaten zelf aan de slag te gaan. Apparaten als iPhones, iPads en MacBooks kunnen rechtstreeks naar gebruikers worden verzonden. Als de gebruiker het apparaat inschakelt, wordt Configuratieassistent, met de herkenbare kant-en-klare ervaring voor Apple-producten, uitgevoerd met vooraf gedefinieerde instellingen en het apparaat ingeschreven bij beheer.

Als u ADE wilt inschakelen, gebruikt u zowel de Intune- als de [Apple School Manager-portal (ABM)](https://business.apple.com/) of de [Apple School Manager-portal (ASM)](https://school.apple.com/). U hebt een lijst met serienummers of een aankoopordernummer nodig om apparaten voor beheer aan Intune toe te wijzen in een Apple-portal. U maakt ADE-inschrijvingsprofielen in Intune met instellingen die tijdens de inschrijving op de apparaten zijn toegepast. ADE kan niet worden gebruikt met een account van een [apparaatinschrijvingsmanager](device-enrollment-manager-enroll.md).

> [!NOTE]
> Met ADE worden configuraties ingesteld die niet noodzakelijkerwijs kunnen worden verwijderd door de eindgebruiker. Daarom moet het apparaat vóór de [migratie naar ADE](../fundamentals/migration-guide-considerations.md) worden gewist om het terug te zetten naar een Out-Of-Box-status (fabrieksstatus).

## <a name="automated-device-enrollment-and-the-company-portal"></a>Automated Device Enrollment en de bedrijfsportal

ADE-inschrijvingen zijn niet compatibel met de App Store-versie van de bedrijfsportal-app. U kunt gebruikers toegang geven tot de bedrijfsportal-app op een ADE-apparaat. U kunt deze toegang geven om gebruikers te laten kiezen welke zakelijke apps ze willen gebruiken op hun apparaat of om moderne verificatie te gebruiken om het inschrijvingsproces te voltooien. 

Push de app naar het apparaat met **Bedrijfsportal installeren met VPP** (Volume Purchase Program) in het ADE-profiel om moderne verificatie tijdens de inschrijving in te schakelen. Zie [iOS-/iPadOS-apparaten automatisch inschrijven met ADE van Apple](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) voor meer informatie.

Als u wilt inschakelen dat de bedrijfsportal automatisch wordt bijgewerkt en de bedrijfsportal-app wordt weergegeven op apparaten die al bij ADE zijn geregistreerd, implementeert u de bedrijfsportal-app via Intune als een vereiste VPP-app (Volume Purchase Program) waarop een [toepassingsconfiguratiebeleid](../apps/app-configuration-policies-use-ios.md) is toegepast.

## <a name="what-is-supervised-mode"></a>Wat is de supervisiemodus?

Apple heeft de supervisiemodus geïntroduceerd in iOS/iPadOS 5. Een iOS-/iPadOS-apparaat in de supervisiemodus kan worden beheerd met meer besturingselementen, zoals het blokkeren van schermopnamen en blokkeren dat apps vanuit de App Store kunnen worden geïnstalleerd. Hierdoor is het vooral handig voor apparaten van het bedrijf. Intune ondersteunt het configureren van apparaten voor de supervisiemodus als onderdeel van ADE.

Ondersteuning voor ADE-apparaten zonder supervisie is afgeschaft in iOS/iPadOS 11. In iOS/iPadOS 11 en later moeten met ADE geconfigureerde apparaten altijd onder supervisie staan. De ADE-vlag *is_supervised* wordt genegeerd in iOS-/iPadOS 13.0 of later. Alle iOS/iPadOS-apparaten met versie 13.0 en later worden automatisch gecontroleerd wanneer deze zijn ingeschreven bij de automatische inschrijving van apparaten. 

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Vereisten
- Apparaten die zijn aangeschaft via [ADE van Apple](https://deploy.apple.com)
- [Mobile Device Management-autoriteit (MDM)](../fundamentals/mdm-authority-set.md)
- [Apple MDM-pushcertificaat](apple-mdm-push-certificate-get.md)

## <a name="supported-volume"></a>Ondersteund volume

- Maximum aantal inschrijvingsprofielen per token: 1000  
- Maximum aantal Automated Device Enrollment-apparaten per profiel: geen limiet (binnen het maximum aantal apparaten per token)
- Maximum aantal Automated Device Enrollment-tokens per Intune-account: 2,000
- Maximum aantal Automated Device Enrollment-apparaten per token: 75.000

## <a name="get-an-apple-ade-token"></a>Een Apple ADE-token ophalen

Voordat u iOS-/iPadOS-apparaten kunt inschrijven via ADE, moet u een ADE-tokenbestand (.p7m) van Apple ontvangen. Intune kan met dit token informatie synchroniseren over ADE-apparaten die eigendom zijn van uw bedrijf. Ook kan Intune hiermee inschrijvingsprofielen naar Apple uploaden en apparaten toewijzen aan die profielen.

U gebruikt de [Apple Business Manager](https://business.apple.com/)- (ABM) of [Apple School Manager](https://school.apple.com/)-portal (ASM) om een token te maken. U gebruikt de ABM/ASM-portal ook om apparaten aan Intune toe te wijzen voor beheer.

> [!NOTE]
> Als u het token verwijdert uit de klassieke Intune-portal voordat u naar Azure migreert, herstelt Intune mogelijk een verwijderd Apple ADE-token. U kunt het ADE-token opnieuw verwijderen via Azure Portal.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Stap 1. Download het openbare-sleutelcertificaat van Intune dat is vereist om het token te maken.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apparaten** > **iOS** > **iOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > **Toevoegen**.

    ![Een token voor het inschrijvingsprogramma ophalen.](./media/device-enrollment-program-enroll-ios/image01.png)

2. Geef Microsoft toestemming om gebruikers- en apparaatgegevens naar Apple te verzenden door **Ik ga akkoord** te selecteren.

   > [!NOTE]
   > Zodra u verder bent dan stap 2 voor het downloaden van het Intune-openbare-sleutelcertificaat, sluit u de wizard niet af en verlaat u deze pagina niet. Anders wordt het certificaat dat u hebt gedownload ongeldig en moet u dit proces opnieuw uitvoeren. Als deze situatie zich voordoet, zult u doorgaans zien dat de knop **Maken** op het tabblad **Beoordelen en maken** grijs wordt weergegeven en kunt u het proces niet voltooien.

   ![Schermopname van het deelvenster Token voor het inschrijvingsprogramma in de werkruimte Apple-certificaten voor het downloaden van de openbare sleutel.](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

3. Kies **Uw openbare-sleutelcertificaat downloaden** en sla het bestand met de versleutelingssleutel (.pem) lokaal op. Het PEM-bestand wordt gebruikt om een vertrouwensrelatiecertificaat aan te vragen bij de Apple-portal.


### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Stap 2. Gebruik uw sleutel om een token van Apple te downloaden.

1. Kies **Een token voor Apple Device Enrollment Program maken** om de Business-portal van Apple te openen en meld u aan met uw Apple ID. Deze Apple ID kunt u gebruiken om uw ADE-token te verlengen.
2. Kies **Aan de slag** bij **Device Enrollment Program** in de [Business-portal](https://business.apple.com) van Apple.

3. Kies **MDM-server toevoegen** op de pagina **Servers beheren**.
4. Voer de **MDM-servernaam** in en kies **Volgende**. De servernaam is voor eigen referentie en dient om de MDM-server te identificeren. Het is niet de naam of URL van de Microsoft Intune-server.

5. Het dialoogvenster **Voeg &lt;servernaam&gt;** wordt geopend, met de instructie dat u uw **openbare sleutel moet uploaden**. Selecteer **Bestand kiezen...** om het .pem-bestand te uploaden en kies **Volgende**.

6. Ga naar **Implementatieprogramma** &gt; **Programma apparaatinschrijving** &gt; **Apparaten beheren**.
7. Geef onder **Kies apparaten op** aan hoe apparaten worden geïdentificeerd:
    - **Serienummer**
    - **Ordernummer**
    - **CSV-bestand uploaden**

   ![Schermopname van het opgeven van apparaten op serienummer, het kiezen van een actie zoals toewijzen aan server en de naam van de server selecteren.](./media/device-enrollment-program-enroll-ios/enrollment-program-token-specify-serial.png)

8. Voor **Kies actie** kiest u **Toewijzen aan server**, kiest u de &lt;Servernaam&gt; die is opgegeven voor Microsoft Intune en kiest u vervolgens **OK**. De opgegeven apparaten worden voor beheer toegewezen aan de Intune-server en er verschijnt een melding dat de **toewijzing is voltooid**.

   Ga in de Apple-portal naar **Deployment Programs** &gt; **Device Enrollment Program** &gt; **Toewijzingsgeschiedenis weergeven** om een lijst van apparaten en hun toewijzing aan de MDM-server te bekijken.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Stap 3. Sla de Apple-id op die u hebt gebruikt om dit token te maken.

Geef in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de Apple ID op voor toekomstige referentie.

![Schermopname van het invoeren van de Apple ID die is gebruikt voor het maken van het token voor het inschrijvingsprogramma en het uploaden van het token.](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token-and-choose-scope-tags"></a>Stap 4. Uw token uploaden en bereikstags kiezen.

1. Ga in het venster **Apple-token** naar het certificaatbestand (.p7m) en kies **Openen**.
2. Als u [bereiktags](../fundamentals/scope-tags.md) wilt toevoegen aan dit DEP-token, kiest u **Bereik (tags)** en selecteert u de bereiktags die u wilt toevoegen. Bereiktags die zijn toegepast op een token, worden overgenomen door profielen en apparaten die aan dit token zijn toegevoegd.
3. Kies **Maken**.

Met het pushcertificaat kan Intune iOS-/iPadOS-apparaten inschrijven en beheren door beleid naar ingeschreven mobiele apparaten te pushen. Intune wordt automatisch gesynchroniseerd met Apple om het account voor het inschrijvingsprogramma weer te geven.

## <a name="create-an-apple-enrollment-profile"></a>Een Apple-inschrijvingsprofiel maken

Na installatie van het token kunt u een inschrijvingsprofiel voor ADE-apparaten maken. Met een inschrijvingsprofiel voor apparaten worden de instellingen gedefinieerd die worden toegepast op een groep apparaten tijdens de inschrijving. Er geldt een limiet van 100 inschrijvingsprofielen per ADE-token.

> [!NOTE]
> Apparaten worden geblokkeerd als er niet genoeg bedrijfsportal-licenties zijn voor een VPP-token, of als het token is verlopen. In Intune wordt een waarschuwing weergegeven wanneer een token bijna verloopt of als er nog maar weinig licenties beschikbaar zijn.
 

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **iOS** > **iOS-inschrijving** > **Tokens voor het inschrijvingsprogramma**.
2. Selecteer een token, kies **Profielen** > **Profiel maken** > **iOS**.

    ![Maak een schermafdruk van het profiel.](./media/device-enrollment-program-enroll-ios/image04.png)

3. Voer op de pagina **Basisinformatie** een **Naam** en een **Beschrijving** voor het profiel in voor administratieve doeleinden. Gebruikers zien deze gegevens niet. 

    ![Naam en beschrijving van het profiel.](./media/device-enrollment-program-enroll-ios/image05.png)

4. Selecteer **Volgende: Instellingen voor apparaatbeheer**.

5. Geef voor **Gebruikersaffiniteit** aan of andere apparaten met dit profiel met of zonder toegewezen gebruiker moeten worden ingeschreven.
    - **Inschrijven met gebruikersaffiniteit**: kies deze optie voor apparaten die eigendom zijn van gebruikers en waarvoor de bedrijfsportal moet worden gebruikt voor services zoals het installeren van apps. Als u gebruikmaakt van ADFS en u Configuratieassistent gebruikt voor verificatie, is [Gebruikersnaam/gemengd eindpunt voor WS-Trust 1.3](https://technet.microsoft.com/library/adfs2-help-endpoints) [Meer informatie](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint) vereist.

    - **Inschrijven zonder gebruikersaffiniteit**: kies deze optie voor een apparaat dat niet aan één gebruiker is gelieerd. Gebruik deze optie voor apparaten die geen toegang hebben tot lokale gebruikersgegevens. Apps als de Bedrijfsportal-app werken niet.

5. Als u kiest voor **Inschrijven met gebruikersaffiniteit**, kunt u gebruikers zich te laten verifiëren met de bedrijfsportal in plaats van de Apple-configuratieassistent.

    ![Verificatie met de bedrijfsportal.](./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > Als u een van het volgende wilt uitvoeren, stelt u **Selecteren waar gebruikers de verificatie moeten uitvoeren** in op **Bedrijfsportal**.
    >    - meervoudige verificatie gebruiken
    >    - gebruikers vragen het wachtwoord te wijzigen als ze zich de eerste keer aanmelden
    >    - gebruikers vragen om hun verlopen wachtwoorden tijdens het inschrijven te herstellen
    >
    > Deze worden niet ondersteund bij het verifiëren met Apple-configuratieassistent.

6. Als u **Bedrijfsportal** kiest voor **Selecteren waar gebruikers de verificatie moeten uitvoeren**, kunt u een VPP-token gebruiken om de bedrijfsportal automatisch op het apparaat te installeren. In dit geval hoeft de gebruiker geen Apple-id op te geven. Als u de Bedrijfsportal wilt installeren met een VPP-token, kiest u een token onder **Install Company Portal with VPP** (Bedrijfsportal installeren met VPP). Daarvoor moet de bedrijfsportal al zijn toegevoegd aan het VPP-token. Om ervoor te zorgen dat de bedrijfsportal-app na de registratie nog steeds wordt bijgewerkt, moet u ervoor zorgen dat u een app-implementatie in Intune hebt geconfigureerd (Intune > Client-apps). Als u interactie van de gebruiker wilt vermijden, kunt u de bedrijfsportal gebruiken in de vorm van een iOS/iPadOS VPP-app, er een vereiste app van maken en apparaatlicenties voor de toewijzing gebruiken. Controleer of het token niet verloopt en of u voldoende apparaatlicenties hebt voor de bedrijfsportal-app. Als het token verloopt of onvoldoende licenties heeft, installeert Intune in plaats daarvan de App Store-bedrijfsportal en vraagt het om een Apple-id. 

    > [!NOTE]
    > Wanneer **Selecteren waar gebruikers de verificatie moeten uitvoeren** is ingesteld op **Bedrijfsportal**, moet u ervoor zorgen dat het apparaatinschrijvingsproces wordt uitgevoerd binnen de eerste 24 uur dat de bedrijfsportal is gedownload op het ADE-apparaat. Anders mislukt de inschrijving en is er een herstel naar fabrieksinstellingen nodig om het apparaat in te schrijven.
    
    ![Schermafbeelding van de installatie van de bedrijfsportal met VPP.](./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png)

7. Als u **Configuratieassistent** kiest voor **Selecteren waar gebruikers de verificatie moeten uitvoeren**, maar u wilt ook voorwaardelijke toegang gebruiken of zakelijke apps implementeren op de apparaten, moet u de bedrijfsportal installeren op de apparaten. U doet dit door **Ja** te kiezen voor **Bedrijfsportal installeren**.  Als u wilt dat gebruikers de bedrijfsportal ontvangen zonder zich te hoeven verifiëren bij de App Store, kiest u **Bedrijfsportal installeren met VPP** en selecteert u een VPP-token. Controleer of het token niet verloopt en of u voldoende apparaatlicenties hebt voor de bedrijfsportal-app om op een juiste manier te implementeren.

8. Als u voor een token hebt gekozen bij **Bedrijfsportal installeren met VPP**, kunt u het apparaat te vergrendelen in de modus voor enkele toepassing (met name de bedrijfsportal-app) direct nadat Configuratieassistent is voltooid. Kies **Ja** voor **Bedrijfsportal-app uitvoeren in de modus voor enkele toepassing tot verificatie** als u deze optie wilt instellen. Voor het gebruik van het apparaat moet de gebruiker eerst worden geverifieerd door zich via de bedrijfsportal-app aan te melden.

    Meervoudige verificatie wordt niet ondersteund op een apparaat dat is vergrendeld in de Modus voor enkele toepassing. Deze beperking bestaat omdat het apparaat niet kan overschakelen naar een andere app om de tweede verificatie te voltooien. Als u daarom meervoudige verificatie wilt op een apparaat met de Modus voor enkele toepassing, moet de tweede verificatie plaatsvinden op een ander apparaat.

    Deze functie wordt alleen ondersteund voor iOS/iPadOS 11.3.1 en hoger.

   ![Schermopname van de modus enkele app.](./media/device-enrollment-program-enroll-ios/single-app-mode.png)

9. Als u wilt dat apparaten met dit profiel onder supervisie wilt, kiest u **Ja** voor **Onder supervisie**.

    ![Schermopname Instellingen voor apparaatbeheer.](./media/device-enrollment-program-enroll-ios/supervisedmode.png)

    Met apparaten **onder supervisie** krijgt u meer beheeropties en de activeringsvergrendeling is standaard uitgeschakeld. Microsoft raadt het gebruik van ADE aan als mechanisme voor het inschakelen van de supervisiemodus, met name als u veel iOS-/iPadOS-apparaten implementeert.

    Gebruikers worden op twee manieren gewaarschuwd dat hun apparaten onder supervisie staan:

   - Het vergrendelingsscherm meldt: 'Deze iPhone wordt beheerd door Contoso.'
   - Het scherm **Instellingen** > **Algemeen** > **Info** meldt: 'Deze iPhone is onder supervisie. Contoso kan uw internetverkeer bijhouden en de locatie van dit apparaat bepalen'.

     > [!NOTE]
     > Een apparaat dat is ingeschreven zonder supervisie, kan alleen opnieuw worden ingesteld met behulp van de Apple Configurator. Als u het apparaat op deze manier opnieuw wilt instellen, moet u een iOS-/iPadOS-apparaat verbinden met een Mac via een USB-kabel. Meer informatie hierover vindt u in de [Apple Configurator-documentatie](http://help.apple.com/configurator/mac/2.3).

10. Kies of u vergrendelde inschrijving wilt voor apparaten die dit profiel gebruiken. **Vergrendelde inschrijving** schakelt de iOS-/iPadOS-instellingen uit, waardoor het beheerprofiel kan worden verwijderd uit het menu **Instellingen**. Als het apparaat is ingeschreven, kunt u deze instelling niet wijzigen zonder het apparaat te wissen. Bij dergelijke apparaten is het vereist dat de beheermodus **Onder supervisie** is ingesteld op *Ja*. 

    > [!NOTE]
    > Nadat het apparaat is ingeschreven via **Vergrendelde inschrijving**, kunnen gebruikers geen gebruik meer maken van **Apparaat verwijderen** of **Fabrieksinstellingen** in de Bedrijfsportal-app. De opties zijn dan niet beschikbaar voor de gebruiker. De gebruiker kan het apparaat dan ook niet verwijderen via de Bedrijfsportal-website (https://portal.manage.microsoft.com).
    > Verder geldt dat als een BYOD-apparaat is geconverteerd naar een apparaat met Automated Device Enrollment van Apple en het is ingeschreven met een profiel waarvoor **Vergrendelde inschrijving** is ingeschakeld, de gebruiker **Apparaat verwijderen** en **Fabrieksinstellingen** dertig dagen mag gebruiken, waarna de opties worden uitgeschakeld of onbeschikbaar worden gemaakt. Naslaginformatie: https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859.

11. Kies of u wilt dat apparaten die dit profiel gebruiken, kunnen **synchroniseren met computers**. Als u **Apple Configurator per certificaat toestaan** kiest, moet u een certificaat kiezen onder **Apple Configurator-certificaten**.

     > [!NOTE]
     > Als **Synchroniseren met computers** is ingesteld op **Alles weigeren**, wordt de poort op iOS- en iPadOS-apparaten beperkt. De poort kan alleen worden gebruikt om op te laden, en voor niets anders. De poort wordt geblokkeerd voor het gebruik van iTunes of Apple Configurator 2.
     Als **Gesynchroniseerd met computers** is ingesteld op **Apple Configurator per certificaat toestaan**, moet u ervoor zorgen dat u een lokale kopie van het certificaat opslaat, waartoe u later toegang hebt. U kunt geen wijzigingen aanbrengen in de geüploade kopie en het is belangrijk om dit certificaat in de toekomst te bewaren. Als u verbinding wilt maken met het iOS/iPadOS-apparaat vanaf een macOS-apparaat of pc, moet hetzelfde certificaat zijn geïnstalleerd op het apparaat dat de verbinding maakt met het iOS/iPadOS-apparaat dat is geregistreerd bij het geautomatiseerde inschrijvingsprofiel voor apparaten met deze configuratie en dit certificaat.

12. Als u in de vorige stap hebt gekozen voor **Apple Configurator per certificaat toestaan**, moet u een Apple Configurator-certificaat kiezen om te importeren.

13. U kunt een naamgevingsindeling opgeven voor apparaten die automatisch wordt toegepast wanneer zij zich inschrijven en na elke keer dat succesvol wordt ingecheckt. Als u een naamgevingssjabloon wilt maken, selecteert u **Ja** onder **Sjabloon voor apparaatnamen toepassen**. Voer vervolgens in het tekstvak **Apparaatnaamsjabloon** het te gebruiken sjabloon in voor de naam die dit profiel gebruiken. U kunt een sjabloonindeling opgeven waarin het apparaattype en serienummer wordt opgenomen. 

14. Kies **Volgende: Aanpassing van Configuratieassistent**.

15. Configureer op de pagina **Aanpassing van Configuratieassistent** de volgende profielinstellingen: ![Aanpassing van Configuratieassistent](./media/device-enrollment-program-enroll-ios/setupassistantcustom.png).


    | Afdelingsinstellingen | Beschrijving |
    |---|---|
    | <strong>Naam afdeling</strong> | Wordt weergegeven wanneer de gebruiker tijdens de activering op <strong>Over configuratie</strong> tikt. |
    |    <strong>Telefoonnummer van afdeling</strong>     | Wordt weergegeven wanneer de gebruiker tijdens de activering de knop <strong>Hulp nodig?</strong> klikt. |

    U kunt ervoor kiezen om de Configuratieassistent-schermen te verbergen tijdens de gebruikersinstallatie.
    - Als u kiest voor **Verbergen** wordt het scherm tijdens het instellen niet weergegeven. Na het instellen van het apparaat kan de gebruiker het menu **Instellingen** nog steeds openen om de functie in te stellen.
    - Als u kiest voor **Weergeven** wordt het scherm tijdens het instellen weergegeven. Gebruikers kunnen sommige schermen overslaan zonder actie te ondernemen. Maar ze kunnen het menu **Instellingen** van het apparaat later weer openen om de functie in te stellen. 


    | Instellingen van configuratieassistentschermen | Als u kiest voor **Weergeven**, zal het apparaat tijdens het instellen... |
    |------------------------------------------|------------------------------------------|
    | <strong>Wachtwoordcode</strong> | De gebruiker om een wachtwoordcode vragen. Vraag altijd om een wachtwoordcode voor onbeveiligde apparaten, tenzij toegang op een andere manier wordt beheerd (bijvoorbeeld een kioskmodus die het apparaat tot één app beperkt). Voor iOS/iPadOS 7.0 en hoger. |
    | <strong>Locatieservices</strong> | De gebruiker om zijn of haar locatie vragen. Voor macOS 10.11 en hoger en iOS/iPadOS 7.0 en hoger. |
    | <strong>Herstellen</strong> | Geef het scherm Apps en gegevens weer. Dit scherm biedt de gebruiker de mogelijkheid tijdens het instellen van het apparaat gegevens te herstellen of over te brengen vanuit de iCloud-back-up. Voor macOS 10.9 en hoger en iOS/iPadOS 7.0 en hoger. |
    | <strong>iCloud en Apple-id</strong> | Geef de gebruiker de mogelijkheid zich aan te melden met zijn of haar Apple-id en iCloud te gebruiken. Voor macOS 10.9 en hoger en iOS/iPadOS 7.0 en hoger.   |
    | <strong>Voorwaarden</strong> | Vraag de gebruiker om de voorwaarden van Apple te accepteren. Voor macOS 10.9 en hoger iOS/iPadOS 7.0 en hoger. |
    | <strong>Touch-id</strong> | Geef de gebruiker de mogelijkheid identificatie met een vingerafdruk in te stellen voor het apparaat. Voor macOS 10.12.4 en hoger en iOS/iPadOS 8.1 en hoger. |
    | <strong>Apple Pay</strong> | Geef de gebruiker de mogelijkheid Apple Pay in te stellen op het apparaat. Voor macOS 10.12.4 en hoger en iOS/iPadOS 7.0 en hoger. |
    | <strong>In- en uitzoomen</strong> | Geef de gebruiker de mogelijkheid om in te zoomen op het scherm tijdens het instellen van het apparaat. Voor iOS/iPadOS 8.3 en hoger. |
    | <strong>Siri</strong> | Geef de gebruiker de mogelijkheid Siri in te stellen. Voor macOS 10.12 en hoger iOS/iPadOS 7.0 en hoger. |
    | <strong>Diagnostische gegevens</strong> | Geef het scherm Diagnose en gebruik weer voor de gebruiker. Met dit scherm heeft de gebruiker de mogelijkheid diagnostische gegevens naar Apple te verzenden. Voor macOS 10.9 en hoger en iOS/iPadOS 7.0 en hoger. |
    | <strong>Weergavetoon</strong> | Geef de gebruiker de mogelijkheid om Weergavetoon in te schakelen. Voor macOS 10.13.6 en hoger en iOS/iPadOS 9.3.2 en hoger. |
    | <strong>Privacy</strong> | Geef het scherm Privacy weer voor de gebruiker. Voor macOS 10.13.4 en hoger en iOS/iPadOS 11.3 en hoger. |
    | <strong>Android-migratie</strong> | Geef de gebruiker de mogelijkheid om gegevens van een Android-apparaat te migreren. Voor iOS/iPadOS 9.0 en hoger.|
    | <strong>iMessage en FaceTime</strong> | Geef de gebruiker de mogelijkheid iMessage en FaceTime in te stellen. Voor iOS/iPadOS 9.0 en hoger. |
    | <strong>Onboarding</strong> | Informatieve onboarding-schermen weergeven ter educatie van de gebruiker, zoals Contactkaart, Multitasking en Beheercentrum. Voor iOS/iPadOS 11.0 en hoger. |
    | <strong>Watch-migratie</strong> | Geef de gebruiker de mogelijkheid om gegevens van een horloge te migreren. Voor iOS/iPadOS 11.0 en hoger.|
    | <strong>Schermtijd</strong> | Hiermee wordt het scherm Schermtijd weergeven. Voor macOS 10.15 en hoger en iOS/iPadOS 12.0 en hoger. |
    | <strong>Software-update</strong> | Hiermee wordt het scherm voor verplichte software-updates weergegeven. Voor iOS/iPadOS 12.0 en hoger. |
    | <strong>SIM-installatie</strong> | Geef de gebruiker de mogelijkheid een mobiel abonnement toe te voegen. Voor iOS/iPadOS 12.0 en hoger. |
    | <strong>Uiterlijk</strong> | Geef het scherm Uiterlijk weer aan de gebruiker. Voor macOS 10.14 en hoger en iOS/iPadOS 13.0 en hoger. |
    | <strong>Express-taal</strong>| Geeft het scherm Express-taal weer aan de gebruiker. |
    | <strong>Voorkeurstaal</strong> | Geeft de gebruiker de mogelijkheid om zijn **Voorkeurstaal** op te geven. |
    | <strong>Migratie van apparaat naar apparaat</strong> | Geef de gebruiker de mogelijkheid om gegevens te migreren van een oud apparaat naar dit apparaat. Voor iOS/iPadOS 13.0 en hoger. |
    | <strong>Registratie</strong> | Het registratiescherm weergeven voor de gebruiker. Voor macOS 10.9 en hoger. |
    | <strong>FileVault</strong> | Het FileVault 2-versleutelingsscherm weergeven voor de gebruiker. Voor macOS 10.10 en hoger. |
    | <strong>Diagnostische gegevens over iCloud</strong> | Geef het iCloud Analaytics-scherm weer voor de gebruiker. Voor macOS 10.12.4 en hoger. |
    | <strong>iCloud-opslag</strong> | Geef het iCloud Documents- en Desktop-scherm weer aan de gebruiker. Voor macOS 10.13.4 en hoger. |
    

16. Kies **Volgende** om naar de pagina **Beoordelen en maken** te gaan.

17. Kies **Maken** om een profiel op te slaan.

### <a name="dynamic-groups-in-azure-active-directory"></a>Dynamische groepen beheren in Azure Active Directory

U kunt bij het inschrijven het veld **Naam** gebruiken om een dynamische groep te maken in Azure Active Directory. Zie voor meer informatie het artikel over [dynamische Azure Active Directory-groepen](/azure/active-directory/users-groups-roles/groups-dynamic-membership).

U kunt de profielnaam gebruiken om de [parameter enrollmentProfileName](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) te definiëren om apparaten aan dit inschrijvingsprofiel toe te wijzen.

Voor de snelste beleidsimplementatie op ADE-apparaten met gebruikersaffiniteit, moet u ervoor zorgen dat de inschrijvende gebruiker voorafgaand aan het instellen van het apparaat lid is van een AAD-gebruikersgroep. 

Het toewijzen van dynamische groepen aan inschrijvingsprofielen kan leiden tot enige vertraging bij het leveren van toepassingen en beleid aan apparaten na de registratie.


## <a name="sync-managed-devices"></a>Beheerde apparaten synchroniseren
Nu Intune toestemming heeft om uw apparaten te beheren, kunt u Intune synchroniseren met Apple om uw beheerde apparaten weer te geven in Intune in Azure Portal.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **iOS** > **iOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > kies een token in de lijst > **Apparaten** > **Synchroniseren**. ![Schermafbeelding van het knooppunt Apparaten voor het inschrijvingsprogramma en de koppeling Synchronisatie.](./media/device-enrollment-program-enroll-ios/image06.png)

   Intune legt de volgende beperkingen op om aan de voorwaarden van Apple voor acceptabel verkeer van het inschrijvingsprogramma te voldoen:
   - Een volledige synchronisatie kan niet vaker dan eens in de zeven dagen worden uitgevoerd. Tijdens een volledige synchronisatie haalt Intune de volledige bijgewerkte lijst met serienummers op die is toegewezen aan de Apple MDM-server die is verbonden met Intune. Als er een ADE-apparaat wordt verwijderd uit de Intune-portal, moet de toewijzing ongedaan worden gemaakt in de Apple MDM-server in de ADE-portal. Als de toewijzing niet ongedaan wordt gemaakt, wordt het apparaat niet meer in Intune geïmporteerd totdat de volledige synchronisatie wordt uitgevoerd.   
   - Er wordt automatisch elke 12 uur een synchronisatie uitgevoerd. U kunt ook synchroniseren door op de knop **Synchroniseren** te klikken (maximaal één keer per 15 minuten). Synchronisatieaanvragen krijgen 15 minuten de tijd om te worden uitgevoerd. De knop **Synchroniseren** blijft uitgeschakeld totdat de synchronisatie is voltooid. Met de synchronisatie wordt de huidige apparaatstatus vernieuwt en worden nieuwe apparaten die aan de Apple MDM-server zijn toegewezen, geïmporteerd.   


## <a name="assign-an-enrollment-profile-to-devices"></a>Een inschrijvingsprofiel toewijzen aan apparaten
U moet een profiel voor een inschrijvingsprogramma aan apparaten toewijzen voordat deze kunnen worden ingeschreven.

>[!NOTE]
>U kunt ook serienummers aan profielen toewijzen via de blade **Apple-serienummers**.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **iOS** > **iOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > kies een token in de lijst.
2. Kies **Apparaten** > kies apparaten uit de lijst > **Profiel toewijzen**.
3. Kies onder **Profiel toewijzen** een profiel voor de apparaten > **Toewijzen**.

### <a name="assign-a-default-profile"></a>Een standaardprofiel toewijzen

U kunt een standaardprofiel kiezen dat wordt toegepast op apparaten die zich inschrijven met een specifiek token.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **iOS** > **iOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > kies een token in de lijst.
2. Kies **Standaardprofiel instellen**, kies een profiel in de vervolgkeuzelijst en kies vervolgens **Opslaan**. Dit profiel wordt toegepast op alle apparaten die zich met het token inschrijven.

## <a name="distribute-devices"></a>Apparaten distribueren
U hebt beheer en synchronisatie tussen Apple en Intune ingeschakeld, en een profiel toegewezen om uw ADE-apparaten te kunnen inschrijven. De apparaten kunnen nu worden uitgedeeld aan de gebruikers. Voor apparaten met gebruikersaffiniteit moet aan elke gebruiker een Intune-licentie worden toegewezen. Voor apparaten zonder gebruikersaffiniteit is een apparaatlicentie vereist. Een geactiveerd apparaat kan geen inschrijvingsprofiel toepassen, tenzij het apparaat is gewist.

Zie [Uw iOS-/iPadOS-apparaat inschrijven in Intune in met het Device Enrollment Program](../user-help/enroll-your-device-dep-ios.md).

## <a name="renew-an-ade-token"></a>Een ADE-token vernieuwen  

> [!NOTE]
> Naast het jaarlijks vernieuwen van uw ADE-token moet u uw inschrijvingsprogrammatoken in Intune en Apple Business Manager vernieuwen wanneer het beheerde Apple ID-wachtwoord voor de gebruiker die het token in Apple Business Manager heeft ingesteld, wordt gewijzigd of wanneer die gebruiker uw Apple Business Manager-organisatie verlaat.

1. Ga naar business.apple.com.  
2. Kies onder **Manage Servers** de MDM-server die is gekoppeld aan het tokenbestand dat u wilt vernieuwen.
3. Kies **Generate New Token**.

    ![Schermopname van nieuw token genereren.](./media/device-enrollment-program-enroll-ios/generatenewtoken.png)

4. Kies **Your Server Token**.  
5. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **iOS** > **iOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > kies het token.
    ![Schermopname van tokens voor het inschrijvingsprogramma.](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

6. Kies **Token vernieuwen** en voer de Apple ID in die is gebruikt om het oorspronkelijke token te maken.  
    ![Schermopname van nieuw token genereren.](./media/device-enrollment-program-enroll-ios/renewtoken.png)

8. Upload het token dat u net hebt gedownload.  
9. Kies **Token vernieuwen**. U krijgt een bevestiging te zien dat het token is vernieuwd.   
    ![Schermopname van de bevestiging.](./media/device-enrollment-program-enroll-ios/confirmation.png)

## <a name="delete-an-ade-token-from-intune"></a>Een ADE-token verwijderen uit Intune

U kunt de tokens voor het inschrijvingsprofiel verwijderen uit Intune zolang
- er geen apparaten aan het token zijn toegewezen
- er geen apparaten aan het standaardprofiel zijn toegewezen

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **iOS/macOS** > **iOS/macOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > kies het token > **Apparaten**.
2. Verwijder alle apparaten die aan het token zijn toegewezen.
3. Ga naar **Apparaten** > **iOS/macOS** > **iOS/macOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > kies het token > **Profielen**.
4. Als er een standaardprofiel is, verwijdert u het.
5. Ga naar **Apparaten** > **iOS/macOS** > **iOS/macOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > kies het token > **Verwijderen**.

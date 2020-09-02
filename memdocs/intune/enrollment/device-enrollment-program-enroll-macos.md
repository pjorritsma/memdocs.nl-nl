---
title: macOS-apparaten inschrijven - Apple Business Manager of Apple School Manager
titleSuffix: ''
description: Meer informatie over het inschrijven van macOS-apparaten in bedrijfseigendom.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/06/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7afe3897c040673ad869584e1e8e8f55f4fc08ff
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911893"
---
# <a name="automatically-enroll-macos-devices-with-the-apple-business-manager-or-apple-school-manager"></a>macOS-apparaten automatisch inschrijven met Apple Business Manager of Apple School Manager

> [!IMPORTANT]
> Apple is recent overgestapt van het Apple Device Enrollment Program (DEP) naar het Apple Automated Device Enrollment (ADE). In verband hiermee wordt de gebruikersinterface van Intune momenteel bijgewerkt. Totdat deze aanpassingen zijn voltooid, wordt *Device Enrollment Program* in de Intune-portal weergegeven. Waar Automatische apparaatinschrijving (Automated Device Enrollment) wordt weergegeven, wordt dit gebruikt.

U kunt de Intune-registratie instellen voor macOS-apparaten die zijn gekocht via [Apple Business Manager](https://business.apple.com/) of [Apple School Manager](https://school.apple.com/) van Apple. U kunt beide soorten inschrijvingen gebruiken voor grote aantallen apparaten zonder op de apparaten zelf aan de slag te gaan. U kunt macOS-apparaten rechtstreeks verzenden naar gebruikers. Als de gebruiker het apparaat inschakelt, wordt Configuratieassistent uitgevoerd met vooraf gedefinieerde instellingen en wordt het apparaat ingeschreven bij Intune-beheer.

Voor het instellen van inschrijving moet u zowel de Intune-portal als de Apple-portal gebruiken. U maakt inschrijvingsprofielen met instellingen die tijdens de inschrijving op de apparaten van toepassing zijn geweest.

Overigens werken Apple Business Manager-inschrijving en Apple School Manager niet met de [apparaatinschrijvingsmanager](device-enrollment-manager-enroll.md).

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Vereisten

- Apparaten die zijn gekocht in [Apple School Manager](http://deploy.apple.com) of [Automatische apparaatinschrijving van Apple](https://school.apple.com/)
- Een lijst met serienummers of een inkoopordernummer.
- [MDM-instantie](../fundamentals/mdm-authority-set.md)
- [Apple MDM-pushcertificaat](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-ade-token"></a>Een Apple ADE-token ophalen

Voordat u macOS-apparaten kunt inschrijven bij ADE of Apple School Manager, hebt u een tokenbestand (.p7m) van Apple nodig. Intune kan met dit token gegevens synchroniseren van de apparaten die in eigendom zijn van uw organisatie. Hiermee kunnen in Intune ook inschrijvingsprofielen worden geüpload naar Apple en deze profielen worden toegewezen aan apparaten.

U gebruikt de Apple-portal om een token te maken. U gebruikt de Apple-portal ook om apparaten aan Intune toe te wijzen voor beheer.

> [!NOTE]
> Als u het token verwijdert uit de klassieke Intune-portal voordat u naar Azure migreert, herstelt Intune mogelijk een verwijderd Apple-token. U kunt het token opnieuw verwijderen via de Azure-portal.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Stap 1. Download het openbare-sleutelcertificaat van Intune dat is vereist om het token te maken.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apparaten** > **macOS** > **macOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > **Toevoegen**.

    ![Een token voor het inschrijvingsprogramma ophalen.](./media/device-enrollment-program-enroll-macos/image01.png)

2. Geef Microsoft toestemming om gebruikers- en apparaatgegevens naar Apple te verzenden door **Ik ga akkoord** te selecteren.

   ![Schermopname van het deelvenster Token voor het inschrijvingsprogramma in de werkruimte Apple-certificaten voor het downloaden van de openbare sleutel.](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

3. Kies **Uw openbare-sleutelcertificaat downloaden** en sla het bestand met de versleutelingssleutel (.pem) lokaal op. Het PEM-bestand wordt gebruikt om een vertrouwensrelatiecertificaat aan te vragen bij de Apple-portal.

### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Stap 2. Gebruik uw sleutel om een token van Apple te downloaden.

1. Kies **Een token maken via Apple Business Manager** of **Een token maken via Apple School Manager** om de gewenste portal van Apple te openen en meld u aan met uw Apple ID. Deze Apple ID kunt u gebruiken om uw token te verlengen.
2. Voor DEP: kies in de Apple-portal **Aan de slag** voor **Device Enrollment Program** > **Servers beheren** > **MDM-server toevoegen**.
3. Voor Apple School Manager: kies in de Apple-portal **MDM-servers** > **MDM-server toevoegen**.
4. Voer de **MDM-servernaam** in en kies **Volgende**. De servernaam is voor eigen referentie en dient om de MDM-server te identificeren. Het is niet de naam of URL van de Microsoft Intune-server.

5. Het dialoogvenster **Voeg &lt;servernaam&gt;** wordt geopend, met de instructie dat u uw **openbare sleutel moet uploaden**. Selecteer **Bestand kiezen...** om het .pem-bestand te uploaden en kies **Volgende**.

6. Ga naar **Implementatieprogramma** &gt; **Programma apparaatinschrijving** &gt; **Apparaten beheren**.
7. Geef onder **Kies apparaten op** aan hoe apparaten worden geïdentificeerd:
    - **Serienummer**
    - **Ordernummer**
    - **CSV-bestand uploaden**

   ![Schermopname van het opgeven van apparaten op serienummer, het kiezen van een actie zoals toewijzen aan server en de naam van de server selecteren.](./media/device-enrollment-program-enroll-macos/enrollment-program-token-specify-serial.png)

8. Voor **Kies actie** kiest u **Toewijzen aan server**, kiest u de &lt;Servernaam&gt; die is opgegeven voor Microsoft Intune en kiest u vervolgens **OK**. De opgegeven apparaten worden voor beheer toegewezen aan de Intune-server en er verschijnt een melding dat de **toewijzing is voltooid**.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Stap 3. De Apple-id opslaan die u hebt gebruikt om dit token te maken

Geef in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de Apple ID op voor toekomstige referentie.

![Schermopname van het invoeren van de Apple ID die is gebruikt voor het maken van het token voor het inschrijvingsprogramma en het uploaden van het token.](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token"></a>Stap 4. Uw token uploaden
Ga in het venster **Apple-token** naar het certificaatbestand (.pem), kies **Openen** en vervolgens **Maken**. Met het pushcertificaat kunnen macOS-apparaten worden ingeschreven en beheerd in Intune door beleid te pushen naar ingeschreven apparaten. Intune wordt automatisch gesynchroniseerd met Apple om het account voor het inschrijvingsprogramma weer te geven.

## <a name="create-an-apple-enrollment-profile"></a>Een Apple-inschrijvingsprofiel maken

Na installatie van de token kunt u een inschrijvingsprofiel voor apparaten maken. Met een inschrijvingsprofiel voor apparaten worden de instellingen gedefinieerd die worden toegepast op een groep apparaten tijdens de inschrijving.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apparaten** > **macOS** > **macOS-inschrijving** > **Tokens voor het inschrijvingsprogramma**.
2. Selecteer een token, kies **Profielen** en kies vervolgens **Profiel maken** > **macOS**.

    ![Maak een schermafdruk van het profiel.](./media/device-enrollment-program-enroll-macos/image04.png)

3. Voer op de pagina **Basisinformatie** een **Naam** en een **Beschrijving** voor het profiel in voor administratieve doeleinden. Gebruikers zien deze gegevens niet. U kunt dit veld **Naam** gebruiken om een dynamische groep te maken in Azure Active Directory. Gebruik de profielnaam om de parameter enrollmentProfileName te definiëren om apparaten aan dit inschrijvingsprofiel toe te wijzen. Meer informatie over [Azure Active Directory dynamic groups](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) (dynamische Azure Active Directory-groepen).

    ![Naam en beschrijving van het profiel.](./media/device-enrollment-program-enroll-macos/createprofile.png)

4. Kies **macOS** als **platform**.

5. Selecteer **Volgende** om naar de pagina **Beheerinstellingen** te gaan.

6. Geef voor **Gebruikersaffiniteit** aan of andere apparaten met dit profiel met of zonder toegewezen gebruiker moeten worden ingeschreven.
    - **Inschrijven met gebruikersaffiniteit**: kies deze optie voor apparaten die eigendom zijn van gebruikers en waarvoor de bedrijfsportal-app moet worden gebruikt voor services zoals het installeren van apps. Als u ADFS gebruikt, vereist gebruikersaffiniteit [WS-Trust 1.3 gebruikersnaam/gemengd eindpunt](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)). [Meer informatie](/powershell/module/adfs/get-adfsendpoint?view=win10-ps). Meervoudige verificatie wordt niet ondersteund voor macOS ADE-apparaten met gebruikersaffiniteit.

    - **Inschrijven zonder gebruikersaffiniteit**: kies deze optie voor een apparaat dat niet aan één gebruiker is gelieerd. Gebruik dit voor apparaten waarmee taken worden uitgevoerd zonder toegang tot lokale gebruikersgegevens. Apps als de Bedrijfsportal-app werken niet.

6. Voor **Vergrendelde inschrijving** kiest u of u vergrendelde inschrijving wilt voor apparaten die dit profiel gebruiken. Met **Ja** worden de macOS-instellingen uitgeschakeld op basis waarvan het beheerprofiel kan worden verwijderd uit het menu **Systeemvoorkeuren** of via de **Terminal**. Als het apparaat is ingeschreven, kunt u deze instelling niet wijzigen zonder het apparaat te wissen.

7. Selecteer **Volgende** om naar de pagina **Configuratieassistent** te gaan.

8. Configureer op de pagina **Configuratieassistent** de volgende profielinstellingen:

    ![Aanpassing van Configuratieassistent.](./media/device-enrollment-program-enroll-macos/setupassistantcustom-macos.png)

    | Afdelingsinstellingen | Beschrijving |
    |---|---|
    | <strong>Naam afdeling</strong> | Wordt weergegeven wanneer de gebruiker tijdens de activering op <strong>Over configuratie</strong> tikt. |
    | <strong>Telefoonnummer van afdeling</strong> | Wordt weergegeven wanneer de gebruiker tijdens de activering de knop <strong>Hulp nodig?</strong> klikt. |

    U kunt kiezen voor het weergeven of verbergen van tal van schermen van de configuratieassistent op het apparaat tijdens het instellen van het apparaat door de gebruiker.
    - Als u kiest voor **Verbergen** wordt het scherm tijdens het instellen niet weergegeven. Na het instellen van het apparaat kan de gebruiker het menu **Instellingen** nog steeds openen om de functie in te stellen.
    - Als u kiest voor **Weergeven** wordt het scherm tijdens het instellen weergegeven. Gebruikers kunnen sommige schermen overslaan zonder actie te ondernemen. Maar ze kunnen het menu **Instellingen** van het apparaat later weer openen om de functie in te stellen. 

    | Instellingen van configuratieassistentschermen | Als u kiest voor **Weergeven**, zal het apparaat tijdens het instellen... |
    |------------------------------------------|------------------------------------------|
    | <strong>Wachtwoordcode</strong> | De gebruiker om een wachtwoordcode vragen. Vraag altijd om een wachtwoordcode voor onbeveiligde apparaten, tenzij toegang op een andere manier wordt beheerd (bijvoorbeeld een kioskmodus die het apparaat tot één app beperkt). Voor iOS/iPadOS 7.0 en hoger. |
    | <strong>Locatieservices</strong> | De gebruiker om zijn of haar locatie vragen. Voor macOS 10.11 en hoger en iOS/iPadOS 7.0 en hoger. |
    | <strong>Herstellen</strong> | Geef het scherm Apps en gegevens weer. Dit scherm biedt de gebruiker de mogelijkheid tijdens het instellen van het apparaat gegevens te herstellen of over te brengen vanuit de iCloud-back-up. Voor macOS 10.9 en hoger en iOS/iPadOS 7.0 en hoger. |
    | <strong>Apple-id</strong> | Geef de gebruiker de mogelijkheid zich aan te melden met zijn of haar Apple-id en iCloud te gebruiken. Voor macOS 10.9 en hoger en iOS/iPadOS 7.0 en hoger.   |
    | <strong>Voorwaarden</strong> | Vraag de gebruiker om de voorwaarden van Apple te accepteren. Voor macOS 10.9 en hoger iOS/iPadOS 7.0 en hoger. |
    | <strong>Touch-id</strong> | Geef de gebruiker de mogelijkheid identificatie met een vingerafdruk in te stellen voor het apparaat. Voor macOS 10.12.4 en hoger en iOS/iPadOS 8.1 en hoger. |
    | <strong>Apple Pay</strong> | Geef de gebruiker de mogelijkheid Apple Pay in te stellen op het apparaat. Voor macOS 10.12.4 en hoger en iOS/iPadOS 7.0 en hoger. |
    | <strong>In- en uitzoomen</strong> | Geef de gebruiker de mogelijkheid om in te zoomen op het scherm tijdens het instellen van het apparaat. Voor iOS/iPadOS 8.3 en hoger. |
    | <strong>Siri</strong> | Geef de gebruiker de mogelijkheid Siri in te stellen. Voor macOS 10.12 en hoger iOS/iPadOS 7.0 en hoger. |
    | <strong>Diagnostische gegevens</strong> | Geef het scherm Diagnose en gebruik weer voor de gebruiker. Met dit scherm heeft de gebruiker de mogelijkheid diagnostische gegevens naar Apple te verzenden. Voor macOS 10.9 en hoger en iOS/iPadOS 7.0 en hoger. |
    | <strong>FileVault</strong> | Het FileVault 2-versleutelingsscherm weergeven voor de gebruiker. Voor macOS 10.10 en hoger. |
    | <strong>Diagnostische gegevens over iCloud</strong> | Geef het iCloud Analytics-scherm weer voor de gebruiker. Voor macOS 10.12.4 en hoger. |
    | <strong>iCloud-opslag</strong> | Geef het iCloud Documents- en Desktop-scherm weer aan de gebruiker. Voor macOS 10.13.4 en hoger. |
    | <strong>Weergavetoon</strong> | Geef de gebruiker de mogelijkheid om Weergavetoon in te schakelen. Voor macOS 10.13.6 en hoger en iOS/iPadOS 9.3.2 en hoger. |
    | <strong>Uiterlijk</strong> | Geef het scherm Uiterlijk weer aan de gebruiker. Voor macOS 10.14 en hoger en iOS/iPadOS 13.0 en hoger. |
    | <strong>Registratie</strong> | Het registratiescherm weergeven voor de gebruiker. Voor macOS 10.9 en hoger. |
    | <strong>Schermtijd</strong> | Hiermee wordt het scherm Schermtijd weergeven. Voor macOS 10.15 en hoger en iOS/iPadOS 12.0 en hoger. |
    | <strong>Privacy</strong> | Geef het scherm Privacy weer voor de gebruiker. Voor macOS 10.13.4 en hoger en iOS/iPadOS 11.3 en hoger. |
    
9. Selecteer **Volgende** om naar de pagina **Controleren en maken** te gaan.

10. Kies **Maken** om een profiel op te slaan.

## <a name="sync-managed-devices"></a>Beheerde apparaten synchroniseren

Nu Intune toestemming heeft om uw apparaten te beheren, kunt u Intune synchroniseren met Apple om uw beheerde apparaten weer te geven in Intune in Azure Portal.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apparaten** > **macOS** > **macOS-inschrijving** > **Tokens voor het inschrijvingsprogramma**.

2. Kies een token in de lijst > **Apparaten** > **Synchronisatie**. ![Schermopname van het geselecteerde knooppunt Apparaten voor het inschrijvingsprogramma en een pijl naar de koppeling Synchroniseren.](./media/device-enrollment-program-enroll-macos/image06.png)

   Om te voldoen aan de voorwaarden van Apple voor acceptabel verkeer van het inschrijvingsprogramma, legt Intune de volgende beperkingen op:
   - Een volledige synchronisatie kan niet vaker dan eens in de zeven dagen worden uitgevoerd. Tijdens een volledige synchronisatie haalt Intune de volledige bijgewerkte lijst met serienummers op die is toegewezen aan de Apple MDM-server die is verbonden met Intune. Wanneer een apparaat uit het inschrijvingsprogramma wordt verwijderd van de Intune-portal zonder dat het eerst is afgemeld bij de Apple MDM-server in de Apple-portal, wordt het apparaat pas opnieuw in Intune geïmporteerd wanneer de volledige synchronisatie wordt uitgevoerd.   
   - Er wordt automatisch elke 24 uur een synchronisatie uitgevoerd. U kunt ook synchroniseren door op de knop **Synchroniseren** te klikken (maximaal één keer per 15 minuten). Synchronisatieaanvragen krijgen 15 minuten de tijd om te worden uitgevoerd. De knop **Synchroniseren** blijft uitgeschakeld totdat de synchronisatie is voltooid. Met de synchronisatie wordt de huidige apparaatstatus vernieuwt en worden nieuwe apparaten die aan de Apple MDM-server zijn toegewezen, geïmporteerd.

## <a name="assign-an-enrollment-profile-to-devices"></a>Een inschrijvingsprofiel toewijzen aan apparaten

U moet een profiel voor een inschrijvingsprogramma aan apparaten toewijzen voordat deze kunnen worden ingeschreven.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **macOS** > **macOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > kies een token in de lijst.
2. Kies **Apparaten** > kies apparaten uit de lijst > **Profiel toewijzen**.
3. Kies onder **Profiel toewijzen** een profiel voor de apparaten > **Toewijzen**.

### <a name="assign-a-default-profile"></a>Een standaardprofiel toewijzen

U kunt een standaardprofiel in macOS en iOS/iPadOS kiezen om toe te passen op alle apparaten die worden ingeschreven met een specifiek token. 

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **macOS** > **macOS-inschrijving** > **Tokens voor het inschrijvingsprogramma** > kies een token in de lijst.
2. Kies **Standaardprofiel instellen**, kies een profiel in de vervolgkeuzelijst en kies vervolgens **Opslaan**. Dit profiel wordt toegepast op alle apparaten die zich met het token inschrijven.

## <a name="distribute-devices"></a>Apparaten distribueren

U hebt beheer en synchronisatie tussen Apple en Intune ingeschakeld, en een profiel toegewezen om uw apparaten te kunnen inschrijven. De apparaten kunnen nu worden uitgedeeld aan de gebruikers. Voor apparaten met gebruikersaffiniteit moet aan elke gebruiker een Intune-licentie worden toegewezen. Voor apparaten zonder gebruikersaffiniteit is een apparaatlicentie vereist. Een geactiveerd apparaat kan geen inschrijvingsprofiel toepassen, tenzij het apparaat is gewist.

## <a name="renew-an-ade-token"></a>Een ADE-token vernieuwen

1. Ga naar deploy.apple.com.  
2. Kies onder **Manage Servers** de MDM-server die is gekoppeld aan het tokenbestand dat u wilt vernieuwen.
3. Kies **Generate New Token**.

    ![Schermopname van nieuw token genereren.](./media/device-enrollment-program-enroll-macos/generatenewtoken.png)

4. Kies **Your Server Token**.  
5. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaatinschrijving** > **Apple-inschrijving** > **Tokens voor het inschrijvingsprogramma** > kies het token.
    ![Schermopname van tokens voor het inschrijvingsprogramma.](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

6. Kies **Token vernieuwen** en voer de Apple ID in die is gebruikt om het oorspronkelijke token te maken.  
    ![Schermopname van nieuw token genereren.](./media/device-enrollment-program-enroll-ios/renewtoken.png)

7. Upload het token dat u net hebt gedownload.  
8. Kies **Token vernieuwen**. U krijgt een bevestiging te zien dat het token is vernieuwd.
    ![Schermopname van de bevestiging.](./media/device-enrollment-program-enroll-macos/confirmation.png)

## <a name="next-steps"></a>Volgende stappen

Nadat de macOS-apparaten zijn ingeschreven, kunt u [deze gaan beheren](../remote-actions/device-management.md).
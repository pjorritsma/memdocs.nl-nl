---
title: De Jamf Pro-cloudconnector integreren met Microsoft Intune
titleSuffix: Microsoft Intune
description: Gebruik de Jamf Pro-cloudconnector samen met Microsoft Intune-nalevingsbeleid met voorwaardelijke toegang voor Azure Active Directory om apparaten te integreren en te beveiligen die met Jamf worden beheerd.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 734a1361d8889ca1463e8d8986239e088b90cd09
ms.sourcegitcommit: eb51bb38d484e8ef2ca3ae3c867561249fa413f3
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/29/2020
ms.locfileid: "84206363"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>De Jamf Pro-cloudconnector gebruiken met Microsoft Intune

In dit artikel vindt u informatie over het installeren van de Jamf-cloudconnector om Jamf Pro te integreren met Microsoft Intune. Met de cloudconnector worden veel van de stappen geautomatiseerd die nodig zijn wanneer u de integratie handmatig configureert zoals beschreven in [Jamf Pro integreren met Intune voor naleving](../protect/conditional-access-integrate-jamf.md).

Wanneer u de cloudconnector instelt:

- Met het instellen worden automatisch de Jamf Pro-toepassingen in Azure gemaakt, zodat deze niet meer handmatig hoeven te worden geconfigureerd.
- U kunt meerdere exemplaren van Jamf Pro integreren met dezelfde Azure-tenant die als host fungeert voor uw Intune-abonnement.

Het verbinden van meerdere exemplaren van Jamf Pro met één Azure-tenant wordt alleen ondersteund wanneer u de cloudconnector gebruikt. Wanneer u een handmatig geconfigureerde verbinding gebruikt, kan slechts één exemplaar van Jamf worden geïntegreerd met een Azure-tenant.

Het gebruik van de cloudconnector is optioneel:

- Voor nieuwe tenants die nog niet zijn geïntegreerd met Jamf, kunt u ervoor kiezen om de cloudconnector te configureren zoals beschreven in dit artikel. U kunt de integratie ook handmatig configureren zoals beschreven in [Jamf Pro integreren met Intune voor naleving](../protect/conditional-access-integrate-jamf.md)
- Voor tenants die al handmatig zijn geconfigureerd, kunt u deze integratie verwijderen en vervolgens de cloudconnector instellen. In dit artikel worden de verwijdering van een bestaande integratie en de instelling van de cloudconnector beschreven.

Als u van plan bent om uw vorige integratie te vervangen door de Jamf-cloudconnector:

- Gebruik de [procedure om uw huidige configuratie te verwijderen](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant), zoals het verwijderen van de bedrijfsapps voor Jamf Pro en het uitschakelen van de handmatige integratie. Vervolgens gebruikt u de [procedure voor het configureren van de cloudconnector](#configure-the-cloud-connector-for-a-new-tenant).
- U hoeft apparaten niet opnieuw te registreren. Apparaten die zijn al geregistreerd, kunnen gebruikmaken van de cloudconnector zonder extra configuratie.
- Zorg ervoor dat u de cloudconnector binnen 24 uur na het verwijderen van uw handmatige integratie configureert om ervoor te zorgen dat uw geregistreerde apparaten hun status kunnen blijven rapporteren.

Zie [De macOS Intune-integratie configureren met behulp van de cloudconnector](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html) op docs.jamf.com voor meer informatie over de Jamf-cloudconnector.

## <a name="prerequisites"></a>Vereisten

**Producten en services**:  
- Jamf Pro 10.18 of hoger
- Een Jamf Pro-gebruikersaccount met rechten voor voorwaardelijke toegang  
- Microsoft Intune
- Microsoft Azure AD Premium
- [Bedrijfsportal-app voor macOS ](https://aka.ms/macoscompanyportal)
- macOS-apparaten met OS X 10.12 Yosemite of hoger

**Netwerk**:  
De volgende poorten en eindpunten moeten toegankelijk zijn voor Jamf en Intune voor een juiste integratie:

- **Intune**: Poort 443
- **Apple**: Poort 2195, 2196 en 5223 (pushmeldingen naar Intune)
- **Jamf**: Poort 80 en 5223

- Eindpunten:
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

Voor de juiste werking van APNS in het netwerk moet u ook uitgaande verbindingen met en omleidingen vanuit de volgende poorten inschakelen:

- De blokkering van Apple 17.0.0.0/8 via TCP-poort 5223 en 443 van alle clientnetwerken.
- De poorten 2195 en 2196 van Jamf Pro-servers.

Zie de volgende artikelen voor meer informatie over deze poorten:

- [Netwerkconfiguratievereisten en bandbreedte voor Intune](../fundamentals/network-bandwidth-use.md).
- [Network Ports Used by Jamf Pro](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro) (Netwerkpoorten die worden gebruikt door Jamf Pro) op jamf.com.
- [TCP and UDP ports used by Apple software products](https://support.apple.com/HT202944) (TCP-en UDP-poorten die worden gebruikt door softwareproducten van Apple) op support.apple.com

**Accounts**:  
In de procedures in dit artikel is het gebruik van accounts met de volgende machtigingen vereist:

- **Jamf Pro-console**: Een account met machtigingen voor het beheren van Jamf Pro
- **Microsoft Endpoint Manager-beheercentrum**: Hoofdbeheerder
- **Azure Portal**: Hoofdbeheerder

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>De Jamf Pro-integratie voor een eerder geconfigureerde tenant verwijderen

Gebruik de volgende procedure om een handmatig geconfigureerde integratie van Jamf Pro te verwijderen uit uw Azure-tenant *voordat* u de cloudconnector kunt configureren.

Als u nog geen verbinding hebt ingesteld tussen Jamf Pro en Intune, of als u een of meer verbindingen hebt waarvoor de cloudconnector al wordt gebruikt, slaat u deze procedure over en begint u met [De cloudconnector configureren voor een nieuwe tenant](#configure-the-cloud-connector-for-a-new-tenant).

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>Een handmatig geconfigureerde Jamf Pro-integratie verwijderen

1. Meld u aan bij de Jamf Pro-console.

2. Selecteer **Instellingen** (het tandwielpictogram in de rechterbovenhoek) en ga vervolgens naar **Globale instellingen** > **Voorwaardelijke toegang**.

   ![Navigeren naar Voorwaardelijke toegang](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Selecteer **Bewerken**.

4. Schakel het selectievakje voor **Intune-integratie voor macOS inschakelen** uit.

   Wanneer u deze instelling uitschakelt, wordt de verbinding uitgeschakeld, maar wordt uw configuratie opgeslagen.

5. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en ga naar **Tenantbeheer** > **Apparaatbeheer partner**.

   Op het knooppunt **Apparaatbeheer partner** verwijdert u de **toepassings-id** in het veld **De Azure Active Directory-app-id voor Jamf opgeven** en selecteert u vervolgens **Opslaan**.

   De toepassings-id is de id van de Azure Enterprise-app die is gemaakt in Azure bij het instellen van een handmatige integratie van Jamf Pro.

6. Meld u aan bij [Azure Portal](https://portal.azure.com/) met een account met globale beheerdersmachtigingen en ga naar **Azure Active Directory** > **Enterprise-toepassingen**.

   Zoek de twee Jamf-apps op en verwijder ze. Nieuwe toepassingen worden automatisch gemaakt wanneer u de Jamf-cloudconnector configureert in de volgende procedure.

   ![Selecteer de Jamf-apps die u wilt verwijderen](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   Nadat u de integratie in Jamf Pro hebt uitgeschakeld en de Enterprise-toepassingen hebt verwijderd, wordt in het knooppunt **Apparaatbeheer partner** de verbindingsstatus **Beëindigd** weergegeven.

   ![De verbindingsstatus Beëindigd](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

Nu u de handmatige configuratie voor de Jamf Pro-integratie hebt verwijderd, kunt u de integratie met behulp van de cloudconnector instellen. Zie hiervoor [De cloudconnector configureren voor een nieuwe tenant](#configure-the-cloud-connector-for-a-new-tenant) in dit artikel.

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>De cloudconnector configureren voor een nieuwe tenant

Gebruik de volgende procedure om de Jamf-cloudconnector te configureren voor de integratie van Jamf Pro en Microsoft Intune in de volgende gevallen:

- U hebt geen integratie tussen Jamf Pro en Intune geconfigureerd voor uw Azure-tenant.
- U hebt al een cloudconnector ingesteld tussen Jamf Pro en Intune in uw Azure-tenant en wilt een extra Jamf-exemplaar integreren met uw abonnement.

Als u momenteel een handmatig geconfigureerde integratie tussen Intune en Jamf Pro hebt, raadpleegt u [De Jamf Pro-integratie voor een eerder geconfigureerde tenant verwijderen](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) in dit artikel om die integratie te verwijderen voordat u verdergaat. Het verwijderen van een handmatig geconfigureerde integratie is vereist om de Jamf-cloudconnector te kunnen instellen.

### <a name="create-a-new-connection"></a>Een nieuwe verbinding maken

1. Meld u aan bij de Jamf Pro-console.

2. Selecteer **Instellingen** (het tandwielpictogram in de rechterbovenhoek) en ga vervolgens naar **Globale instellingen** > **Voorwaardelijke toegang**.

   ![Navigeren naar Voorwaardelijke toegang](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Selecteer **Bewerken**.

4. Schakel het selectievakje voor **Intune-integratie voor macOS inschakelen** in.
   - Selecteer deze instelling om Jamf Pro inventarisupdates te laten verzenden naar Microsoft Intune.
   - U kunt deze instelling uitschakelen, waarmee de verbinding wordt uitgeschakeld, maar uw configuratie wordt opgeslagen.

   > [!IMPORTANT]
   > Als **Intune-integratie inschakelen voor macOS** al is geselecteerd en de optie *Verbindingstype* is ingesteld op **handmatig**, moet u die integratie verwijderen voordat u doorgaat. Zie [De Jamf Pro-integratie voor een eerder geconfigureerde tenant verwijderen](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) in dit artikel voor dat u verdergaat.

5. Selecteer onder *Verbindingstype* **Cloudconnector**.

   ![Selecteer Cloudconnector in de Jamf Pro-console](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. Selecteer in het pop-upmenu **Onafhankelijke cloud** de locatie van uw onafhankelijke cloud van Microsoft. Als u de vorige integratie wilt vervangen door de Jamf-cloudconnector, kunt u deze stap overslaan als de locatie is opgegeven.

7. Selecteer een van de volgende landingspaginaopties voor computers die niet worden herkend door Microsoft Azure:
   - **De standaardpagina voor het registreren van Jamf Pro**: afhankelijk van de status van het macOS-apparaat worden gebruikers door deze optie omgeleid naar de portal voor het inschrijven van Jamf Pro-apparaten (om te registreren bij Jamf Pro) of de Intune-bedrijfsportal-app (om te registreren bij Azure AD).
   - **De pagina Toegang geweigerd**
   - **Aangepaste URL**
  
   Als u de vorige integratie wilt vervangen door de Jamf-cloudconnector, kunt u deze stap overslaan als de landingspagina is opgegeven.
  
8. Selecteer **Verbinden**. U wordt omgeleid om de Jamf Pro-toepassingen in Azure te registreren.

   Geef desgevraagd uw Microsoft Azure-referenties op en volg de instructies op het scherm om de aangevraagde machtigingen te verlenen. U verleent machtigingen voor de **cloudconnector** en vervolgens opnieuw voor de **registratie-app voor cloudconnectorgebruikers**. Beide apps worden in Azure geregistreerd als Enterprise-toepassingen.

   Nadat de machtigingen voor beide apps zijn verleend, wordt de pagina **Toepassings-id** geopend.

9. Selecteer op de pagina **Toepassings-id** de optie **Intune kopiëren en openen**.

   ![Toepassings-id](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   De *toepassings-id* wordt naar het klembord van uw systeem gekopieerd voor gebruik in de volgende stap, en het knooppunt **Apparaatbeheer partner** in het *Microsoft Endpoint Manager-beheercentrum* wordt geopend. (**Tenantbeheer** > **Apparaatbeheer partner**).

10. Op het knooppunt **Apparaatbeheer partner** *plakt* u de **toepassings-id** in het veld **De Azure Active Directory-app-id voor Jamf opgeven** en selecteert u vervolgens **Opslaan**.

    ![Apparaatbeheer partner configureren](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. Ga terug naar de pagina Toepassings-id in Jamf Pro en selecteer **Bevestigen**.

12. Jamf Pro voltooit en test de configuratie en geeft het slagen of mislukken van de verbinding weer op de pagina met instellingen van Voorwaardelijke toegang. De volgende afbeelding biedt een voorbeeld van een geslaagde configuratie:

    ![Een geslaagde configuratie wordt bevestigd in Jamf Pro](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. Vernieuw het knooppunt **Apparaatbeheer partner** in het Microsoft Endpoint Manager-beheercentrum. De verbinding geeft nu **Actief** weer:

    ![De verbindingsstatus is actief](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

Wanneer de verbinding tussen Jamf Pro en Microsoft Intune tot stand is gebracht, verzendt Jamf Pro inventarisgegevens naar Microsoft Intune van elke computer die bij Azure AD is geregistreerd (registreren bij Azure AD is een werkstroom voor eindgebruikers). U kunt de inventarisstatus van voorwaardelijke toegang voor een gebruiker en een computer weergeven in de categorie Lokaal gebruikersaccount van de inventarisgegevens van een computer in Jamf Pro.

Nadat u een exemplaar van Jamf Pro hebt geïntegreerd met behulp van de Jamf-cloudconnector, kunt u dezelfde procedure gebruiken om extra exemplaren van Jamf Pro te configureren met hetzelfde Intune-abonnement in uw Azure-tenant.  

## <a name="set-up-compliance-policies-and-register-devices"></a>Nalevingsbeleid instellen en apparaten registreren

Nadat u de integratie tussen Intune en Jamf hebt geconfigureerd, moet u [nalevingsbeleid toepassen op door Jamf beheerde apparaten](../protect/conditional-access-assign-jamf.md).

## <a name="disconnect-jamf-pro-and-intune"></a>Verbinding tussen Jamf Pro en Intune verbreken

Als u de integratie van Jamf Pro met Intune moet verwijderen, gebruikt u de volgende stappen om de verbinding uit de Jamf Pro-console te verwijderen. Deze informatie is van toepassing op zowel de cloudconnector als voor een handmatige geconfigureerde integratie.

1. Ga in Jamf Pro naar **Global Management** > **Conditional Access**. Selecteer op het tabblad **macOS Intune Integration** de optie **Edit**.

2. Schakel het selectievakje **Enable Intune Integration for macOS** uit.

3. Selecteer **Opslaan**. Jamf Pro stuurt uw configuratie naar Intune, waarna de integratie wordt beëindigd

4. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

5. Selecteer **Tenantbeheer** > **Connectors en tokens** > **Apparaatbeheer partner** om te controleren of de status nu **Beëindigd** is.

   > [!NOTE]
   > De Mac-apparaten in uw organisatie worden verwijderd op de datum (3 maanden) die wordt weergegeven in uw console.

## <a name="get-support-for-the-cloud-connector"></a>Ondersteuning voor de cloudconnector krijgen

Omdat de cloudconnector automatisch de Azure Enterprise-apps maakt die noodzakelijk zijn voor integratie, moet uw eerste contactpunt voor ondersteuning **Jamf** zijn. Opties zijn onder andere:

- Ondersteuning via e-mail op `support@jamf.com`
- Gebruik de ondersteuningsportal op Jamf Nation: https://www.jamf.com/support/ 


Voordat u contact opneemt met ondersteuning:

- Bekijk de vereisten zoals de poorten en de productversie die u gebruikt.
- Controleer of de machtigingen voor de volgende twee Jamf Pro-apps die zijn gemaakt in Azure, niet zijn gewijzigd. Wijzigingen in de app-machtigingen worden niet ondersteund door Intune en kunnen ertoe leiden dat de integratie mislukt.

  **Registratie-app voor cloudconnectorgebruikers**:
  - API-naam: Microsoft Graph
    - Machtiging: Aanmelden en gebruikersprofiel lezen
    - Type: Gedelegeerd
    - Verleend via: Toestemming van de beheerder
    - Verleend door: Een beheerder

  **Cloudconnector-app**:
  - API-naam: Microsoft Graph (exemplaar 1)
    - Machtiging: Aanmelden en gebruikersprofiel lezen
    - Type: Gedelegeerd
    - Verleend via: Toestemming van de beheerder
    - Verleend door: Een beheerder

  - API-naam: Microsoft Graph (exemplaar 2)
    - Machtiging: Mapgegevens lezen
    - Type: Toepassing
    - Verleend via: Toestemming van de beheerder
    - Verleend door: Een beheerder

  - API-naam: Intune-API
    - Machtiging: Kenmerk van apparaat naar Microsoft Intune verzenden
    - Type: Toepassing
    - Verleend via: Toestemming van de beheerder
    - Verleend door: Een beheerder

## <a name="common-questions-about-the-jamf-cloud-connector"></a>Veelgestelde vragen over de Jamf-cloudconnector

### <a name="what-data-is-shared-via-the-cloud-connector"></a>Welke gegevens worden gedeeld via de cloudconnector?

De cloudconnector wordt geverifieerd Microsoft Azure en verzendt apparaatinventarisgegevens van Jamf Pro naar Azure. Daarnaast beheert de cloudconnector de servicedetectie in Azure, uitwisseling van tokens, communicatiefouten en herstel na noodgevallen.

### <a name="where-is-device-inventory-data-stored"></a>Waar worden de apparaatinventarisgegevens opgeslagen?

De apparaatinventarisgegevens worden opgeslagen in de Jamf Pro-database.

### <a name="what-credentials-are-stored"></a>Welke referenties worden opgeslagen?

Er worden geen referenties opgeslagen. Bij het configureren van de cloudconnector moeten beheerders toestemming geven om de Jamf-app voor meerdere tenants en de systeemeigen macOS-connector-app toe te voegen aan hun Azure AD-tenant. Zodra de toepassing voor meerdere tenants is toegevoegd, vraagt de cloudconnector om toegangstokens om met de Azure-API te communiceren. De toegang tot toepassingen kan op elk gewenst moment worden beperkt in Microsoft Azure.

### <a name="how-is-data-encrypted"></a>Hoe worden gegevens versleuteld?

De cloudconnector gebruikt TLS (Transport Layer Security) voor gegevens die worden verzonden tussen Jamf Pro en Microsoft Azure.

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>Hoe weet Jamf welk apparaat is gekoppeld aan welk exemplaar van Jamf Pro?

Jamf Pro maakt gebruik van microservices in AWS om de apparaatgegevens correct naar het juiste exemplaar te sturen.

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>Kan ik overschakelen van het gebruik van de cloudconnector naar het handmatige verbindingstype?

Ja. U kunt het verbindingstype weer in handmatig wijzigen en de stappen voor handmatige installatie volgen. Als u hulp wilt en vragen hebt, moet u deze richten aan Jamf.

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>Wordt er ondersteuning geboden wanneer de machtigingen zijn gewijzigd voor een of beide vereiste apps (*cloudconnector* en *de registratie-app voor cloudconnectorgebruikers*) en de registratie niet werkt?

Het wijzigen van de machtigingen voor de apps wordt niet ondersteund.

### <a name="is-there-a-log-file-in-jamf-pro-that-shows-if-the-connection-type-has-been-changed"></a>Is er een logboekbestand in Jamf Pro dat laat zien of het verbindingstype is gewijzigd?

Ja, de wijzigingen worden vastgelegd in het bestand JAMFChangeManagement.log. Als u de logboeken voor wijzigingsbeheer wilt bekijken, meldt u zich aan bij Jamf Pro, gaat u naar **Instellingen** > **Systeeminstellingen** > **Wijzigingsbeheer** > **Logboeken**, zoekt u naar **Objecttype** voor **Voorwaardelijke toegang**, en klikt u vervolgens op **Details** om de wijzigingen weer te geven.

## <a name="next-steps"></a>Volgende stappen

- [Nalevingsbeleid toepassen op door Jamf beheerde apparaten](../protect/conditional-access-assign-jamf.md)
- [Gegevens die Jamf verzendt naar Intune](../protect/data-jamf-sends-to-intune.md)

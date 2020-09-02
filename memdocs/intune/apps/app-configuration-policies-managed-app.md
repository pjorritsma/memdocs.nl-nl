---
title: Configuratiebeleidsregels toevoegen voor beheerde apps zonder apparaatinschrijving
titleSuffix: Microsoft Intune
description: Meer informatie over het configureren van beleidsregels voor beheerde apps zonder apparaatinschrijving.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: E61C1618-79D0-41A1-B61F-4123FB6672FC
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 20b5b3de16023ac475cc41a633e5d3ab915a1bd0
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910720"
---
# <a name="add-app-configuration-policies-for-managed-apps-without-device-enrollment"></a>App-configuratiebeleidsregels toevoegen voor beheerde apps zonder apparaatinschrijving

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

U kunt app-configuratiebeleidsregels gebruiken voor beheerde apps die de Intune App SDK ondersteunen, zelfs op apparaten die niet zijn ingeschreven. 

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Kies de opties **Apps** > **App-configuratiebeleid** > **Toevoegen** > **Beheerde apps**.
3. Stel op de pagina **Basisinformatie** de volgende gegevens in:
    - **Naam**: De naam van het profiel die in Azure Portal wordt weergegeven.
    - **Beschrijving**: De beschrijving van het profiel die in Azure Portal wordt weergegeven.
    - **Type apparaatinschrijving**: Beheerde apps is geselecteerd.
4. Kies **Openbare apps selecteren** of **Aangepaste apps selecteren** om de app te kiezen die u wilt configureren. Selecteer de app in de lijst met apps die u hebt goedgekeurd en die zijn gesynchroniseerd met Intune.
5. Klik op **Volgende** om de pagina **Instelling** weer te geven.
6. De pagina **Instellingen** bevat opties die worden weergegeven op basis van de app die u configureert:

    - **Algemene configuratie-instellingen**: voor elke algemene, door de app ondersteunde configuratie-instelling typt u de **Naam** en **Waarde**. 
 
        Voor Intune App SDK-functionaliteit geschikte apps ondersteunen configuraties in sleutel-waardeparen. Raadpleeg de documentatie van elke app voor meer informatie over welke sleutel-waardeconfiguraties worden ondersteund. Houd er rekening mee dat u tokens kunt gebruiken die dynamisch worden gevuld met gegevens die zijn gegenereerd door de app. Als u een algemene configuratie-instelling wilt verwijderen, kiest u het beletselteken ( **...** ) en selecteert u **Verwijderen**. Zie [Configuratiewaarden voor het gebruik van tokens](app-configuration-policies-managed-app.md#configuration-values-for-using-tokens) voor meer informatie. 

    - **Configuratie-instellingen voor Outlook**: Outlook voor iOS en Android biedt beheerders de mogelijkheid om de standaardconfiguratie voor verschillende in-app-instellingen aan te passen. Zie [Outlook voor iOS en Android - Scenario's voor algemene configuratie-instellingen](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#general-app-configuration-scenarios) voor meer informatie.
   
    - **S/MIME**: Secure Multipurpose Internet Mail Extensions (S/MIME) is een specificatie waarmee gebruikers e-mailberichten die digitaal zijn ondertekend en versleuteld, kunnen verzenden en ontvangen.
        - **S/MIME inschakelen**: Geef op of S/MIME-besturingselementen zijn ingeschakeld bij het opstellen van een e-mailbericht. Standaardwaarde: **Niet geconfigureerd**.
        - **Gebruiker toestaan om de instelling te wijzigen**: Geef aan of de gebruiker de synchronisatie-instelling mag wijzigen. S/MIME moet zijn ingeschakeld. Standaardwaarde: **Ja**.
        
    Zie [Configuratie-instellingen voor de Outlook-app voor iOS en Android implementeren](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune) voor informatie over configuratiebeleidsinstellingen voor de Outlook-app.

7. Klik op **Volgende** om de pagina **Toewijzingen** weer te geven.
8. Klik op **Groepen selecteren die moeten worden opgenomen**.
9. Selecteer een groep in het deelvenster **Groepen selecteren die moeten worden opgenomen** en klik op **Selecteren**.
10. Klik op **Groepen voor uitsluiten selecteren** om het gerelateerde deelvenster weer te geven.
11. Kies de groepen die u wilt uitsluiten en klik vervolgens op **Selecteren**.

    >[!NOTE]
    >Wanneer u een groep toevoegt en als er al een andere groep is opgenomen voor een gegeven toewijzingstype, wordt deze groep vooraf geselecteerd. Dit kan niet worden gewijzigd voor andere toewijzingstypen voor opnemen. De groep die is gebruikt, kan daarom niet als een uitgesloten groep worden gebruikt.

12. Klik op **Volgende** om naar de pagina **Controleren en maken** weer te geven.
13. Klik op **Maken** om het configuratiebeleid toe te voegen aan Intune.

## <a name="configuration-values-for-using-tokens"></a>Configuratiewaarden voor het gebruik van tokens

Intune kan bepaalde tokens genereren en deze verzenden naar de beheerde toepassing. Als bijvoorbeeld uw app-configuratie een e-mailinstelling kan gebruiken, kunt u een dynamische e-mail toevoegen met behulp van een token. Typ de naam die door de app wordt verwacht in het veld **Naam** en typ vervolgens `{{mail}}` in het veld **Waarde**.

Intune ondersteunt de volgende tokentypen in de configuratie-instellingen. Andere aangepaste sleutel-/waardeparen worden niet ondersteund.

- \{\{userprincipalname\}\}- bijvoorbeeld John@contoso.com
- \{\{mail\}\}- bijvoorbeeld John@contoso.com
- \{\{partialupn\}\} - bijvoorbeeld Jan
- \{\{accountid\}\} - bijvoorbeeld fc0dc142-71d8-4b12-bbea-bae2a8514c81
- \{\{userid\}\} - bijvoorbeeld 3ec2c00f-b125-4519-acf0-302ac3761822
- \{\{username\}\} - bijvoorbeeld Jan de Vries
- \{\{PrimarySMTPAddress\}\}- bijvoorbeeld testuser@ad.domain.com

> [!Note]  
> De tekens \{\{ en \}\} worden alleen gebruikt door tokentypen en mogen niet worden gebruikt voor andere doeleinden.

## <a name="next-steps"></a>Volgende stappen

Ga vervolgens als gebruikelijk door met [toewijzen](apps-deploy.md) en [bewaken](apps-monitor.md) van de app.
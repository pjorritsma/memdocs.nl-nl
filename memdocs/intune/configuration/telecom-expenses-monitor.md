---
title: Een Telecom Expense Management-service instellen in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Integreer Microsoft Intune met de onkostenbeheerservice van Saaswedo om het gegevensgebruik te bewaken en drempelwaarden of limieten in te stellen op Android-apparaatbeheer-, iOS- en iPadOS-apparaten.
keywords: Saaswedo
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/08/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: b7bf5802-4b65-4aeb-ac99-8e639dd89c2a
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3cabf3bad447ef3db8250d14fcb376cb86aefad3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907546"
---
# <a name="set-up-a-telecom-expense-management-service-in-intune"></a>Een Telecom Expense Management-service instellen in Intune

Met Intune kunt u telecommunicatiekosten beheren van gegevensgebruik op mobiele apparaten die eigendom zijn van de organisatie. Intune kan worden geïntegreerd met [Datalert Telecom Expense Management](http://datalert.biz/get-started) van Saaswedo. Datalert is een realtime Telecom Expense Management-oplossing waarmee u telecomgegevensgebruik kunt beheren. Zo kunt u onverwachte gegevens- en roamingkosten voor uw door Intune beheerde apparaten voorkomen.

Door de integratie met Datalert kunt u limieten instellen, controleren en afdwingen voor roaming en binnenlands gegevensgebruik. Wanneer de limieten de drempelwaarden overschrijden, worden er automatisch waarschuwingen gegeven. U kunt de service ook configureren om verschillende acties toe te passen op gebruikers of groepen, zoals het uitschakelen van roaming of overschrijden van de drempelwaarde. In de Datalert-beheerconsole zijn rapporten over het gegevensgebruik en rapporten met controlegegevens beschikbaar.

De volgende afbeelding laat zien hoe Intune is geïntegreerd met Datalert:

> [!div class="mx-imgBorder"]
> ![Diagram van Intune en Datalert-integratie](./media/telecom-expenses-monitor/tem-datalert-intune-solution-diagram.png)

Als u de Datalert-service met Intune wilt gebruiken, zijn er enkele configuratie-instellingen in Datalert en Intune nodig. In dit artikel leest u informatie over:

- Het configureren van instellingen in de Datalert-console om de Datalert-service te verbinden met Intune.
- Het controleren of deze verbinding actief is en is ingeschakeld in Intune.
- Het gebruiken van Intune om de Datalert-app toe te voegen aan uw apparaten.
- Het uitschakelen van de Datalert-service en voor Intune (optioneel).

## <a name="supported-platforms"></a>Ondersteunde platforms

- Android-apparaatbeheer 4.4- en nieuwere apparaten met Knox-ondersteuning (Samsung)
- iOS 8.0 en hoger
- iPadOS 13.0 en hoger

## <a name="prerequisites"></a>Vereisten

- Een abonnement op Microsoft Intune en toegang tot het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431)
- Een abonnement op [Datalert](http://www.datalert.biz/) (opent de Datalert-website)

## <a name="telecom-expense-management-providers"></a>Telecom Expense Management-providers

Intune kan worden geïntegreerd met de volgende Telecom Expense Management-providers:

- [Telecom Expense Management-service Datalert van Saaswedo](http://www.datalert.biz/) (opent de Datalert-website)

## <a name="deploy-the-intune-and-datalert-solution"></a>De Intune en Datalert-oplossing implementeren

### <a name="step-1-connect-the-datalert-service-to-intune"></a>Stap 1: De Datalert-service verbinden met Intune

1. Meld u aan bij de Datalert-beheerconsole met beheerdersreferenties.

2. Ga in de console naar het tabblad **Instellingen** > **MDM-configuratie**.

3. Selecteer **Blokkering opheffen**. Nadat u **Blokkering opheffen** hebt geselecteerd, kunt u de instellingen op de pagina wijzigen of bijwerken.

4. Selecteer **Microsoft Intune** in **Intune/Datalert-verbinding** > **Server-MDM**.

5. Voer uw Azure-tenant-id in bij **Azure AD-domein**. Selecteer **Verbinding**.

    Wanneer u **Verbinding** selecteert, maakt de Datalert-service contact met Intune. Er wordt bevestigd dat er geen bestaande Datalert-verbindingen zijn. Na enkele ogenblikken verschijnt een Microsoft-aanmeldingspagina, gevolgd door de Azure-verificatie voor Datalert.

6. Selecteer **Accepteren** op de Microsoft-verificatiepagina.

    U wordt doorgestuurd naar de **bedank**pagina van Datalert, die na enkele ogenblikken wordt gesloten. Datalert valideert de verbinding, en er wordt een groen vinkje weergegeven naast de items die zijn gevalideerd. Als de validatie mislukt, ziet u een bericht in rood. Neem dan contact op met de Datalert-ondersteuning voor hulp.

    In de volgende afbeelding ziet u de groene vinkjes wanneer de verbinding is geslaagd:

      > [!div class="mx-imgBorder"]
      > ![Datalert-pagina die geslaagde verbinding toont](./media/telecom-expenses-monitor/tem-datalert-connection.png)

7. Stel bij **Datalert-app/ADAL-toestemming** de schakelaar in op **Aan**. Selecteer **Accepteren** op de Microsoft-verificatiepagina.

    U wordt doorgestuurd naar de **bedank**pagina van Datalert, die na enkele ogenblikken wordt gesloten. Datalert valideert de verbinding, en er wordt een groen vinkje weergegeven naast de items die zijn gevalideerd. Als de validatie mislukt, ziet u een bericht in rood. Neem dan contact op met de Datalert-ondersteuning voor hulp.

    In de volgende afbeelding ziet u de groene vinkjes wanneer de verbinding is geslaagd:

      > [!div class="mx-imgBorder"]
      > ![Datalert-pagina die geslaagde verbinding toont](./media/telecom-expenses-monitor/tem-datalert-adal-consent.png)

8. In **MDM-profielbeheer (optioneel)** stelt u de schakeloptie in op **Aan**. Met deze instelling kan Datalert de beschik bare profielen in Intune lezen om u te helpen bij het instellen van beleidsregels. 

    Selecteer **Accepteren** op de Microsoft-verificatiepagina.

    U wordt doorgestuurd naar de **bedank**pagina van Datalert, die na enkele ogenblikken wordt gesloten. Datalert valideert de verbinding, en er wordt een groen vinkje weergegeven naast de items die zijn gevalideerd. Als de validatie mislukt, ziet u een bericht in rood. Neem dan contact op met de Datalert-ondersteuning voor hulp.

    In de volgende afbeelding ziet u de groene vinkjes wanneer de verbinding is geslaagd:

    > [!div class="mx-imgBorder"]
    > ![Datalert-pagina die geslaagde verbinding toont](./media/telecom-expenses-monitor/tem-datalert-mdm-profiles.png)

### <a name="step-2-confirm-telecom-expense-management-is-active-in-intune"></a>Stap 2: Bevestigen dat Telecom Expense Management-service actief is in Intune

Nadat u stap 1 hebt voltooid, wordt de verbinding automatisch ingeschakeld. In Intune is de verbindingsstatus **Actief**. Gebruik de volgende stappen om te bevestigen dat de status Actief is:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Tenantbeheer** > **Connectors en tokens** > **Telecom Expense Management**. Zoek naar de verbindingsstatus **Actief**:

    > [!div class="mx-imgBorder"]
    > ![Intune-pagina met Datalert-verbindingsstatus Actief](./media/telecom-expenses-monitor/tem-azure-portal-enable-service.png)

### <a name="step-3-deploy-the-datalert-app-to-devices"></a>Stap 3: De Datalert-app implementeren op apparaten

Als u wilt bevestigen dat alleen gegevensgebruik van lijnen die eigendom zijn van de organisatie wordt verzameld, doet u het volgende:

- Apparaatcategorieën maken in Intune.
- De Datalert-app alleen richten op telefoons van de organisatie.

In deze sectie vindt u deze stappen.

#### <a name="create-device-categories-and-device-groups-mapped-to-your-categories"></a>Maak apparaatcategorieën en -groepen die zijn toegewezen aan uw categorieën

Afhankelijk van de behoeften van uw organisatie maakt u ten minste twee categorieën voor apparaten, bijvoorbeeld Zakelijk en Persoonlijk. Vervolgens maakt u dynamische apparaatgroepen voor elke categorie. U kunt meer categorieën voor uw organisatie maken, indien nodig.

Zie [Apparaten toewijzen aan groepen](../enrollment/device-group-mapping.md) voor instructies over het maken van apparaatcategorieën in Intune.

Deze categorieën worden weergegeven aan gebruikers tijdens de inschrijving ([Android-apparaten inschrijven](../enrollment/android-enroll.md)). Afhankelijk van welke categorie de gebruiker kiest, wordt het ingeschreven apparaat verplaatst naar de overeenkomstige apparaatgroep.

> [!div class="mx-imgBorder"]
> ![Schermafbeelding van het deelvenster Een beleid toevoegen](./media/telecom-expenses-monitor/tem-dynamic-membership-rules.png)

#### <a name="add-the-datalert-app-to-intune"></a>De Datalert-app toevoegen aan Intune

Met de volgende stappen wordt de Datalert-app toegevoegd. Als voorbeeld wordt iOS/iPadOS gebruikt. [Apps toevoegen](../apps/apps-add.md) en [Bereiktags gebruiken](../fundamentals/scope-tags.md) bevatten meer specifieke informatie over deze stappen.

1. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apps** > **Alle apps** > **Toevoegen**.

2. Selecteer uw **App-type**. Voor iOS/iPadOS selecteert u bijvoorbeeld **Store-app - iOS/iPadOS**.

3. Typ **Datalert** in **Zoeken in de App Store** om de Datalert-app te vinden.

4. Kies de **Datalert**-app > **Selecteren**:

    > [!div class="mx-imgBorder"]
    > ![De Datalert-app uit de App Store toevoegen aan de Intune-client-apps](./media/telecom-expenses-monitor/tem-select-app-from-apple-app-store.png)

5. Voer eventuele aanvullende eigenschappen in, zoals app-gegevens en bereiktags:

    > [!div class="mx-imgBorder"]
    > ![Voer de app-eigenschappen in, zoals de naam en beschrijving, en kies het besturingssysteem en meer instellingen voor de app in Intune](./media/telecom-expenses-monitor/tem-steps-to-create-the-app.png)

6. Selecteer **OK** > **Toevoegen** om uw wijzigingen op te slaan. De Datalert-app wordt weergegeven in de lijst.

#### <a name="assign-the-datalert-app-to-the-corporate-device-group"></a>De app Datalert aan de groep bedrijfsapparaten toewijzen

1. Selecteer in **Apps** > **Alle apps** de Datalert-app die u in de vorige stap hebt toegevoegd.

2. Selecteer **Toewijzingen** > **Groep toevoegen**. Kies hoe de app wordt toegewezen. [Apps aan groepen toewijzen in Intune](../apps/apps-deploy.md) bevat meer informatie over deze instellingen.

    In deze stappen kiest u of u de installatie van de app verplicht of optioneel wilt maken voor de groep. In het volgende voorbeeld wordt de installatie weergegeven als vereist. Wanneer dit vereist is, moeten gebruikers de Datalert-app installeren nadat ze hun apparaat hebben ingeschreven.

    > [!div class="mx-imgBorder"]
    > ![Schermafbeelding van het deelvenster Een beleid toevoegen](./media/telecom-expenses-monitor/tem-assign-datalert-app-to-device-group.png)

### <a name="step-4-add-organization-phone-lines-to-the-datalert-console"></a>Stap 4: Telefoonlijnen van de organisatie aan de Datalert-console toevoegen

De Intune- en Datalert-services zijn nu geconfigureerd om met elkaar te communiceren. Voeg vervolgens de betaalde telefoonlijnen van de organisatie toe aan de Datalert-console. Voer drempels en acties voor eventuele overschrijding van mobiel of roaming gebruik in. U kunt betaalde bedrijfstelefoonlijnen handmatig aan de Datalert-console toevoegen, of automatisch laten toevoegen nadat het apparaat is ingeschreven bij Intune.

Ga voor het instellen van deze items naar [Datalert-installatie voor Microsoft Intune](http://www.datalert.fr/microsoft-intune/intune-setup) (opent de website van Datalert). Volg onder het tabblad **Instellingen** de stappen in de wizard.

> [!div class="mx-imgBorder"]
> ![Schermafbeelding van het deelvenster Een beleid toevoegen](./media/telecom-expenses-monitor/tem-add-phone-lines-to-datalert-console.png)

De Datalert-service is nu actief. Er wordt begonnen met het controleren van het gegevensgebruik en het uitschakelen van mobiele en roaminggegevens op apparaten die de geconfigureerde gebruikslimieten overschrijden.

## <a name="end-user-enrollment"></a>Inschrijving van eindgebruikers

Voor de ervaring van de eindgebruiker kunnen de volgende artikelen helpen:

- [Uw iOS/iPadOS-apparaat registreren bij Telecom Expense Management](../user-help/enroll-your-device-with-telecom-expense-management-ios.md)
- [Uw Android-apparaat registreren bij Telecom Expense Management](../user-help/enroll-your-device-with-telecom-expense-management-android.md)

## <a name="turn-off-the-datalert-service"></a>De Datalert-service uitschakelen

1. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Tenantbeheer** > **Connectors en tokens** > **Telecom Expense Management**.
2. Stel **Telecom Expense Management inschakelen en mobiele gegevens en/of roaminggegevens blokkeren op apparaten die geconfigureerde gebruiksquota hebben overschreden** in op **Uitschakelen**.
3. U moet vervolgens de wijzigingen **Opslaan**.

> [!IMPORTANT]
> Het uitschakelen van de Datalert-service in Intune leidt tot het volgende:
>
> - Alle acties die zijn toegepast op apparaten als gevolg van eerdere schendingen van de gebruikslimieten, worden ongedaan gemaakt.
> - gebruikers zijn niet meer geblokkeerd voor gegevenstoegang en roaming.
> - Intune ontvangt nog wel de signalen van de service, maar negeert de signalen.

## <a name="next-steps"></a>Volgende stappen

Rapporten over gegevensgebruik zijn alleen beschikbaar in de Datalert-beheerconsole van Saaswedo.
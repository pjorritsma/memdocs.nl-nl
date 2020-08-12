---
title: Verbinding maken met Configuration Manager
titleSuffix: Configuration Manager
description: Een hand leiding voor het verbinden van Configuration Manager met Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7015ab4c180ed56b00149ffbff99c9e5a8112e95
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125998"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Configuration Manager verbinding maken met Desktop Analytics

Desktop Analytics is nauw geïntegreerd met Configuration Manager. Controleer eerst of de site up-to-date is voor het ondersteunen van de nieuwste functies. Maak vervolgens de verbinding met de bureau blad Analytics in Configuration Manager. Controleer ten slotte de status van de verbinding.

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a>De site bijwerken

Zorg er eerst voor dat op uw Configuration Manager-site ten minste versie 1902 wordt uitgevoerd. Zie [updates binnen de console installeren](../core/servers/manage/install-in-console-updates.md)voor meer informatie.

U moet ook versie 1902 update pakket (4500571) installeren ter ondersteuning van de integratie met Desktop Analytics. Zie [Update pakket voor Configuration Manager current branch versie 1902](https://support.microsoft.com/help/4500571)voor meer informatie over deze update.

1. Werk de site bij met het update pakket voor versie 1902. Zie [updates binnen de console installeren](../core/servers/manage/install-in-console-updates.md)voor meer informatie.

2. Clients bijwerken. U kunt dit proces vereenvoudigen door gebruik te maken van automatische client upgrade. Zie [upgrade-clients](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)voor meer informatie.

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a>Verbinding maken met de service

> [!TIP]
> Voordat u de wizard startte, maakt u de doel verzameling die wordt vermeld in stap 8, omdat u niet buiten de wizard kunt selecteren nadat u deze hebt gestart.

Gebruik deze procedure om Configuration Manager verbinding te maken met Desktop Analytics en apparaatinstellingen te configureren. Deze procedure is een eenmalig proces om uw hiërarchie te koppelen aan de Cloud service.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure-Services** . Selecteer **Azure-Services configureren** in het lint.

    > [!TIP]
    > Maak rechtstreeks verbinding met de service vanuit het knoop punt voor **onderhoud van Desktop Analytics** . Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** en selecteer het knoop punt **Desktop Analytics-onderhoud** . Selecteer in het vak *Nieuw naar Desktop Analytics?* de tweede koppeling om *Configuration Manager te verbinden met de Desktop Analytics-Service*.

2. Configureer de volgende instellingen op de pagina **Azure-Services** van de wizard Azure-Services:

    - Geef een **naam** op voor het object in Configuration Manager.

    - Geef een optionele **Beschrijving** op die u kan helpen bij het identificeren van de service.

    - Selecteer **Desktop Analytics** in de lijst met beschik bare Services.

   Selecteer **Next**.

3. Selecteer op de pagina **app** de juiste **Azure-omgeving**. Selecteer vervolgens **Bladeren** voor de web-app.

4. Als u een bestaande app hebt die u voor deze service wilt gebruiken, kiest u deze in de lijst en selecteert u **OK**.

5. In de meeste gevallen kunt u met deze wizard een app maken voor de Desktop Analytics-verbinding. Selecteer **Maken**.<!-- 3572123 -->

    > [!TIP]
    > Als u de app niet kunt maken op basis van deze wizard, moet u de app hand matig maken in azure AD en vervolgens importeren in Configuration Manager. Zie voor meer informatie [app maken en importeren voor Configuration Manager](troubleshooting.md#create-and-import-app-for-configuration-manager).

6. Configureer de volgende instellingen in het venster **Server toepassing maken** :

    - **Toepassings naam**: een beschrijvende naam voor de app in azure AD.

    - **URL van start pagina**: deze waarde wordt niet gebruikt door Configuration Manager, maar is vereist voor Azure AD. Standaard is deze waarde ingesteld op `https://ConfigMgrService`.

    - **App-ID-URI**: deze waarde moet uniek zijn in uw Azure AD-Tenant. Het is in het toegangs token dat door de Configuration Manager-client wordt gebruikt om toegang tot de service aan te vragen. Standaard is deze waarde ingesteld op `https://ConfigMgrService`.

    - **Geldigheids duur van geheime sleutel**: Kies **1 jaar** of **2 jaar** in de vervolg keuzelijst. Een jaar is de standaard waarde.

    Selecteer **Aanmelden** . Nadat de verificatie naar Azure is geslaagd, wordt op de pagina de naam van de **Azure AD-Tenant** voor referentie weer gegeven.

    > [!NOTE]
    > Voer deze stap uit als **globale beheerder**. Deze referenties worden niet opgeslagen door Configuration Manager. Deze persoon heeft geen machtigingen nodig in Configuration Manager en hoeft niet hetzelfde account te zijn dat de wizard Azure-Services uitvoert.

    Selecteer **OK** om de web-app te maken in azure AD en sluit het dialoog venster Server toepassing maken. Selecteer **OK**in het dialoog venster server app. Selecteer vervolgens **volgende** op de pagina app van de wizard Azure-Services.

7. Configureer de volgende instellingen op de pagina **Diagnostische gegevens** :

    - **Commerciële id**: deze waarde moet automatisch worden ingevuld met de id van uw organisatie. Als dat niet het geval is, moet u ervoor zorgen dat de proxy server zo is geconfigureerd dat alle vereiste [eind punten](enable-data-sharing.md#endpoints) worden toegestaan voordat u doorgaat. U kunt ook uw commerciële ID hand matig ophalen via de [Desktop Analytics-Portal](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Niveau van diagnostische gegevens voor Windows 10**: Selecteer mini maal **vereist**. Zie [Diagnostische gegevens niveaus](enable-data-sharing.md#diagnostic-data-levels)voor meer informatie.

        > [!TIP]
        > In Configuration Manager versie 2002 en eerder is deze waarde **Basic**genoemd.<!-- 7363467 -->

    - **Apparaatnaam in diagnostische gegevens toestaan**: Selecteer **inschakelen**

        > [!NOTE]
        > Vanaf Windows 10 versie 1803 wordt de apparaatnaam niet standaard naar micro soft verzonden. Als u de apparaatnaam niet verzendt, wordt deze in Desktop Analytics weer gegeven als ' onbekend '. Dit gedrag kan het lastig maken om apparaten te identificeren en te beoordelen.

   Selecteer **Next**. Op de pagina **beschik bare functionaliteit** ziet u de functionaliteit van het bureau blad Analytics die beschikbaar is met de instellingen voor diagnostische gegevens van de vorige pagina. Selecteer **volgende** om door te gaan of op **vorige** om wijzigingen aan te brengen.

    ![Voor beeld van een beschik bare functionaliteits pagina in de wizard Azure-Services](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. Configureer op de pagina **verzamelingen** de volgende instellingen:

    - **Weergave naam**: de bureau blad Analytics-portal geeft deze Configuration Manager verbinding weer met behulp van deze naam. Gebruik het om onderscheid te maken tussen verschillende hiërarchieën en om verzamelingen van afzonderlijke hiërarchieën te identificeren. Gebruik termen om eenvoudig meerdere hiërarchieën in uw omgeving te onderscheiden, bijvoorbeeld: *test lab* of *productie*.

    - **Doel verzameling**: deze verzameling bevat alle apparaten die Configuration Manager configureert met de instellingen voor uw commerciële id en diagnostische gegevens. Het is de volledige set apparaten waarmee Configuration Manager verbinding maakt met de Desktop Analytics-service.

    - **Apparaten in de doel verzameling gebruiken een door de gebruiker geverifieerde proxy voor uitgaande communicatie**: deze waarde is standaard ingesteld op **Nee**. Stel dit in op **Ja**als dat nodig is in uw omgeving.

    - **Specifieke verzamelingen selecteren om te synchroniseren met Desktop Analytics**: Selecteer **toevoegen** om extra verzamelingen te gebruiken uit de hiërarchie van de **doel verzameling** . Deze verzamelingen zijn beschikbaar in de Desktop Analytics-Portal om te groeperen met implementatie plannen. Zorg ervoor dat u verzamelingen van pilot-en pilot-uitsluitingen opneemt.  <!-- 4097528 -->

        > [!TIP]
        > In het venster verzamelingen selecteren worden alleen de verzamelingen weer gegeven die zijn beperkt door de **doel verzameling**.
        >
        > In het volgende voor beeld selecteert u Collectiona als uw doel verzameling. Wanneer u vervolgens extra verzamelingen toevoegt, ziet u Collectiona, CollectionB en CollectionC. U kunt geen verzamelde verzameling toevoegen.
        >
        > - Verzamelinga: beperkt door de verzameling **alle systemen**
        >     - CollectionB: beperkt door Verzamelinga
        >         - CollectionC: beperkt door CollectionB
        > - Verzameld: beperkt door **alle systemen** verzameling
        >
        > Als u de verzamelingen wilt beheren die beschikbaar zijn in de Desktop Analytics-portal voor groepering met implementatie plannen, gaat u in de Configuration Manager-console naar de werk ruimte **beheer** , vouwt u **Cloud Services**uit en selecteert u het knoop punt **Azure-Services** . Selecteer de vermelding die is gekoppeld aan de Azure-service voor **Desktop Analytics** en werk uw instellingen bij op de pagina met **Desktop Analytics-verzameling** .

        > [!IMPORTANT]
        > Deze verzamelingen blijven synchroniseren wanneer hun lidmaatschap wordt gewijzigd. Uw doel verzameling gebruikt bijvoorbeeld een verzameling met een lidmaatschaps regel voor Windows 7. Als deze apparaten worden bijgewerkt naar Windows 10 en Configuration Manager het lidmaatschap van de verzameling evalueert, worden deze apparaten uit de verzameling en bureaublad analyse verwijderd.

9. Voltooi de wizard.

Configuration Manager maakt een instellingen beleid voor het configureren van apparaten in de doel verzameling. Dit beleid bevat de instellingen voor diagnostische gegevens om apparaten in staat te stellen gegevens naar micro soft te verzenden. Standaard wordt het beleid voor clients elk uur bijgewerkt. Na het ontvangen van de nieuwe instellingen, kan het enkele uren duren voordat de gegevens beschikbaar zijn in Desktop Analytics.

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a>Verbindings status bewaken

Controleer de configuratie van uw apparaten op Desktop Analytics. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw het knoop punt **Desktop Analytics Servicing** uit en selecteer het dash board **verbindings status** .

Zie [verbindings status controleren](monitor-connection-health.md)voor meer informatie.

Configuration Manager synchroniseert uw verzamelingen binnen 60 minuten na het maken van de verbinding. Ga in de Desktop Analytics-Portal naar**globale pilot**en bekijk uw Configuration Manager apparaten.

> [!NOTE]
> De Configuration Manager verbinding met Desktop Analytics is afhankelijk van het service verbindings punt. Wijzigingen in deze site systeemrol kunnen van invloed zijn op de synchronisatie met de Cloud service. Zie [about the Service Connection Point](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move)(Engelstalig) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

Ga naar het volgende artikel om apparaten in te schrijven voor desktop Analytics.
> [!div class="nextstepaction"]
> [Apparaten inschrijven](enroll-devices.md)

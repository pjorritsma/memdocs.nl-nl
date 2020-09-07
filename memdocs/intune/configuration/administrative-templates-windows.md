---
title: Sjablonen voor Windows 10-apparaten gebruiken in Microsoft Intune - Azure | Microsoft Docs
description: Gebruik beheersjablonen in Microsoft Intune en Endpoint Manager om groepen instellingen te maken voor Windows 10-apparaten. Gebruik deze instellingen in een apparaatconfiguratieprofiel om Office-programma's en Microsoft Edge te beheren, Internet Explorer te beveiligen, toegang tot OneDrive te krijgen, Extern bureaublad te gebruiken, automatisch afspelen in te schakelen, instellingen voor energiebeheer in te stellen, afdrukken via HTTP te gebruiken, aanmeldingen door gebruikers te beheren en de grootte van het gebeurtenislogboek te wijzigen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: faa217bd5e56a304b80298f2039ad3c541612e54
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992800"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Windows 10-sjablonen gebruiken voor het configureren van instellingen voor groepsbeleid in Microsoft Intune

Wanneer u apparaten in uw organisatie beheert, moet u groepen instellingen maken die van toepassing zijn op verschillende apparaatgroepen. Stel dat u beschikt over verschillende apparaatgroepen. Aan GroupA wilt u een specifieke set instellingen toewijzen. Aan GroupB wilt u een andere set instellingen toewijzen. U wilt ook een eenvoudig overzicht verkrijgen van de instellingen die u kunt configureren.

U kunt deze taak uitvoeren met **Beheersjablonen** in Microsoft Intune. De beheersjablonen bevatten duizenden instellingen waarmee functies kunnen worden geconfigureerd voor Microsoft Edge (versie 77 en hoger), Internet Explorer, Microsoft Office-programma's, Extern bureaublad, OneDrive, wachtwoorden, pincodes, en nog veel meer. Met deze instellingen kunnen groepsbeheerders groepsbeleid beheren via de cloud.

Deze functie is van toepassing op:

- Windows 10 en nieuwer

De Windows-instellingen zijn vergelijkbaar met instellingen voor groepsbeleid (GPO) in Active Directory (AD). Deze instellingen zijn ingebouwd in Windows. Het zijn [door ADMX ondersteunde instellingen](/windows/client-management/mdm/understanding-admx-backed-policies) die gebruikmaken van XML. De instellingen voor Office en Microsoft Edge worden door ADMX opgenomen en gebruiken ADMX-instellingen in [Office-bestanden met beheersjablonen](https://www.microsoft.com/download/details.aspx?id=49030) en [Microsoft Edge-bestanden met beheersjablonen](https://www.microsoftedgeinsider.com/enterprise). En de Intune-sjablonen zijn 100% cloudgebaseerd. Ze bieden een eenvoudige en duidelijke manier om de instellingen te configureren en om de gewenste instellingen te zoeken.

**Beheersjablonen** zijn ingebouwd in Intune en hoeven niet te worden aangepast; dit geldt ook voor het gebruik van de OMA-URI. Gebruik deze sjablooninstellingen als basis voor het beheren van uw Windows 10-apparaten, als onderdeel van uw MDM-oplossing (Mobile Device Management).

In dit artikel vindt u de stappen voor het maken van een sjabloon voor Windows 10-apparaten. U leest hier ook meer over het filteren van de beschikbare instellingen in Intune. Wanneer u de sjabloon maakt, wordt er ook een apparaatconfiguratieprofiel gemaakt. U kunt dit profiel vervolgens toewijzen aan of implementeren op Windows 10-apparaten in uw organisatie.

## <a name="before-you-begin"></a>Voordat u begint

- Sommige van deze instellingen zijn beschikbaar vanaf Windows 10 versie 1709 (RS2/build 15063). Sommige instellingen zijn niet in alle Windows-edities beschikbaar. Voor de beste ervaring wordt u aangeraden Windows 10 Enterprise versie 1903 (19H1/build 18362) of nieuwer te gebruiken.

- De Windows-instellingen maken gebruik van [beleids-CSP's voor Windows](/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies). De CSP's werken op verschillende edities van Windows zoals Home, Professional, Enterprise enzovoort. Ga naar [Beleids-CSP's voor Windows](/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies) om te zien of een bepaalde CSP in een specifieke editie werkt.

## <a name="create-the-template"></a>De sjabloon maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: Kies **Windows 10 en hoger**.
    - **Profiel**: Selecteer **Beheersjablonen**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld **Beheersjabloon: Windows 10-beheersjabloon waarmee de instellingen xyz in Microsoft Edge worden geconfigureerd.**
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Selecteer in **Configuratie-instellingen** de optie **Alle instellingen** om een alfabetische lijst met alle instellingen weer te geven. Of configureer instellingen die van toepassing zijn op apparaten (**Computerconfiguratie**) en instellingen die van toepassing zijn op gebruikers **(Gebruikersconfiguratie**):

    > [!div class="mx-imgBorder"]
    > ![ADMX-sjablooninstellingen toepassen op gebruikers en apparaten in Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. Wanneer u **Alle instellingen** selecteert, wordt elke instelling weer gegeven. Schuif omlaag als u de pijlen voor vorige en volgende wilt gebruiken om meer instellingen te bekijken:

    > [!div class="mx-imgBorder"]
    > ![Een voorbeeldlijst met instellingen bekijken en de knoppen Vorige en Volgende gebruiken](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

9. Selecteer een willekeurige instelling. U kunt bijvoorbeeld filteren op **Office** en **Beperkt browsen activeren** selecteren. Er wordt een gedetailleerde beschrijving van de instelling weergegeven. Kies **Ingeschakeld**, **Uitgeschakeld** of laat de instellingen op **Niet geconfigureerd** staan (standaard). In de gedetailleerde beschrijving wordt ook uitgelegd wat er gebeurt wanneer u kiest voor **Ingeschakeld**, **Uitgeschakeld** of **Niet geconfigureerd**.

    > [!TIP]
    > De Windows-instellingen in Intune correleren met het pad naar het on-premises groepsbeleidsobject dat u ziet in Lokale groepsbeleidsobjecteditor (`gpedit`)

10. Wanneer u **Computerconfiguratie** of **Gebruikersconfiguratie** selecteert, worden de instellingscategorieën weergegeven. U kunt elke categorie selecteren om de beschikbare instellingen te bekijken.

    Selecteer bijvoorbeeld **Computerconfiguratie** > **Windows-onderdelen** > **Internet Explorer** als u alle apparaatinstellingen wilt zien die van toepassing zijn op Internet Explorer:

    > [!div class="mx-imgBorder"]
    > ![Alle apparaatinstellingen bekijken die van toepassing zijn op Internet Explorer in Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

11. Selecteer **OK** om uw wijzigingen op te slaan.

    Doorloop de lijst met instellingen verder en configureer de instellingen die u in uw omgeving wilt gebruiken. Enkele voorbeelden:

    - Gebruik de instelling **VBA Macro Notification Settings** (Meldingsinstellingen voor VBA-macro's) om in te stellen hoe in verschillende Microsoft Office-programma's moet worden omgegaan met VBA-macro's, bijvoorbeeld in Word en Excel.
    - Gebruik de instelling **Bestand downloaden toestaan** als u wilt toestaan of voorkomen dat er vanuit Internet Explorer wordt gedownload.
    - Gebruik **Een wachtwoord vereisen wanneer de computer uit de slaapstand komt (netstroom)** om gebruikers te vragen om een wachtwoord in te voeren wanneer apparaten uit de slaapstand worden gehaald.
    - Gebruik de instelling **ActiveX-besturingselementen zonder handtekening downloaden** om te voorkomen dat gebruikers niet-ondertekende ActiveX-besturingselementen downloaden via Internet Explorer.
    - Gebruik de instelling **Systeemherstel uitschakelen** om te voorkomen dat gebruikers systeemherstel uitvoeren op het apparaat.
    - Gebruik de instelling **Importeren van favorieten toestaan** om toe te staan of te blokkeren dat gebruikers favorieten van een andere browser kunnen importeren in Microsoft Edge.
    - En nog veel meer...

12. Selecteer **Volgende**.
13. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](..//fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

14. Selecteer in **Toewijzingen** de gebruiker of groepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Als het profiel is toegewezen aan gebruikersgroepen, zijn de geconfigureerde ADMX-instellingen van toepassing op elk apparaat waarop de gebruiker zich inschrijft en aanmeldt. Als het profiel is toegewezen aan apparaatgroepen, zijn de geconfigureerde ADMX-instellingen van toepassing op elke gebruiker die zich bij dat apparaat aanmeldt. Deze toewijzing vindt alleen plaats als de ADMX-instelling een computerconfiguratie (`HKEY_LOCAL_MACHINE`) of een gebruikersconfiguratie (`HKEY_CURRENT_USER`) is. Bij sommige instellingen kan een computerinstelling die aan een gebruiker is toegewezen, ook invloed hebben op de ervaring van andere gebruikers van dat apparaat.

    Zie [Gebruikersgroepen versus apparaatgroepen](device-profile-assign.md#user-groups-vs-device-groups) voor meer informatie.

    Selecteer **Volgende**.

15. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

De volgende keer dat het apparaat controleert op configuratie-updates, worden de instellingen toegepast die u hebt geconfigureerd.

## <a name="find-some-settings"></a>Enkele instellingen zoeken

In deze sjablonen zijn duizenden verschillende instellingen beschikbaar. Gebruik de volgende ingebouwde functies om het eenvoudiger te maken om specifieke instellingen te zoeken:

- Selecteer in uw sjabloon de kolom **Instellingen**, **Status**, **Instellingstype** of **Pad** om de lijst te sorteren. Selecteer bijvoorbeeld de kolom **Pad** en gebruik de pijl Volgende om de instellingen in het pad `Microsoft Excel` te bekijken.

- Gebruik in uw sjabloon het vak **Zoeken** om specifieke instellingen te zoeken. U kunt zoeken op instelling of pad. Selecteer **Alle instellingen** en zoek naar `copy`. Alle instellingen met `copy` worden weergegeven:

  > [!div class="mx-imgBorder"]
  > ![Zoeken naar 'copy' om alle apparaatinstellingen in beheersjablonen in Intune weer te geven](./media/administrative-templates-windows/search-copy-settings.png) 

  Zoek in een ander voorbeeld naar `microsoft word`. U ziet de instellingen die u voor het programma Microsoft Word kunt instellen. Zoek naar `explorer` om te bekijken welke Internet Explorer-instellingen u aan uw sjabloon kunt toevoegen.

- U kunt uw zoekopdracht ook verfijnen door alleen **Computerconfiguratie** of **Gebruikersconfiguratie** te selecteren.

  Als u bijvoorbeeld alle beschikbare gebruikersinstellingen voor Internet Explorer wilt zien, selecteert u **Gebruikersconfiguratie** en zoekt u naar `Internet Explorer`. Alleen de IE-instellingen die van toepassing zijn op gebruikers worden weer gegeven:

  :::image type="content" source="./media/administrative-templates-windows/show-all-internet-explorer-settings-user-configuration.png" alt-text="Selecteer Gebruikersconfiguratie in de ADMX-sjabloon en zoek naar of filter op Internet Explorer in Microsoft Intune.":::

## <a name="next-steps"></a>Volgende stappen

De sjabloon is gemaakt, maar het is mogelijk dat er nog niets gebeurt. De volgende stap is [de sjabloon, ook wel een profiel genoemd, toewijzen](device-profile-assign.md) en [de status ervan bewaken](device-profile-monitor.md).

[Microsoft 365 bijwerken met behulp van beheersjablonen](administrative-templates-update-office.md).

[Zelfstudie: De cloud gebruiken voor het configureren van groepsbeleid op Windows 10-apparaten met ADMX-sjablonen en Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
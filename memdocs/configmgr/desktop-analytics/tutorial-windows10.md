---
title: Zelf studie-Windows 10 implementeren
titleSuffix: Configuration Manager
description: Een zelf studie over het gebruik van Desktop Analytics en Configuration Manager voor het implementeren van Windows 10 naar een test groep.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b991c2ddd0ea121251eb19afbdb032844be8738d
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268195"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Zelf studie: Windows 10 implementeren naar pilot

In deze zelf studie wordt gebruikgemaakt van bureau blad Analytics en Configuration Manager voor het implementeren van Windows 10 naar een test groep. Het markeert de integratie van de Cloud service om inzichten te leveren om Windows te implementeren met het on-premises product. Gebruik Desktop Analytics om de beste apparaten te bepalen die in een test groep moeten worden geplaatst. Gebruik vervolgens Configuration Manager om de huidige met Windows op te halen.

In deze zelfstudie leert u het volgende:  

> [!div class="checklist"]  
> * Desktop Analytics instellen in de Azure Portal  
> * Configuration Manager verbinding maken en apparaatinstellingen configureren  
> * Een desktop Analytics-implementatie plan voor Windows 10 maken  
> * Configuration Manager gebruiken om Windows 10 te implementeren in de test groep  

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free) aan voordat u begint. Wanneer het gebruik van Desktop Analytics op de juiste wijze is geconfigureerd, worden er geen Azure-kosten in rekening gebracht.

Desktop Analytics maakt gebruik van een *log Analytics-werk ruimte* in uw Azure-abonnement. Een werkruimte is in wezen een container met accountgegevens en eenvoudige configuratiegegevens voor het account. Zie [werk ruimten beheren](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json)voor meer informatie.



## <a name="prerequisites"></a>Vereisten

Voordat u met deze zelf studie begint, moet u ervoor zorgen dat u over de volgende vereisten beschikt:  

- Een actief Azure-abonnement met [**globale beheerders**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) machtigingen  

    Zie [vereisten voor desktop Analytics](overview.md#prerequisites)voor meer informatie.

- Configuration Manager, versie 1902 met update pakket (4500571) of hoger, met **volledige beheerdersrol**  

- Installatie media voor de nieuwste versie van Windows 10

- Ten minste één Windows 10-apparaat met de volgende configuraties:  

    - Windows 10, versie 1709 of hoger, maar minder dan de versie van het installatie medium dat u wilt gebruiken

    - De meest recente update voor de cumulatieve kwaliteit van Windows 10  

    - Configuration Manager client versie 1902 met update pakket (4500571) of hoger  

- Zakelijke goed keuring voor het configureren van het Windows diagnostische gegevens niveau op **uitgebreid (beperkt)** op de pilot-apparaten  

    Zie [privacy van Desktop Analytics](privacy.md)voor meer informatie.

- Netwerk verbinding van het apparaat met de volgende Internet eindpunten:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net`(alleen bij Configuration Manager serverrol)
    - `https://*.manage.microsoft.com`(alleen bij Configuration Manager serverrol)

    Zie voor meer informatie [delen van gegevens inschakelen voor desktop Analytics](enable-data-sharing.md#endpoints).  

> [!Important]  
> Deze vereisten gelden voor de doel einden van deze zelf studie. Zie [vereisten](overview.md#prerequisites)voor meer informatie over de algemene vereisten voor desktop Analytics met Configuration Manager.  



## <a name="set-up-desktop-analytics"></a>Desktop Analytics instellen

Gebruik deze procedure om u aan te melden bij Desktop Analytics en deze te configureren in uw abonnement. Deze procedure is een eenmalig proces voor het instellen van Desktop Analytics voor uw organisatie.  

1. Open de [Portal voor desktop Analytics](https://aka.ms/desktopanalytics) in Microsoft 365 Apparaatbeheer als gebruiker met **globale beheerders** machtigingen. Selecteer **Starten**.  

2. Controleer de service overeenkomst op de pagina **Service overeenkomst accepteren** en selecteer **accepteren**.  

3. Op de pagina **uw abonnement bevestigen** is de lijst met vereiste licenties voor het inschakelen van Windows-Apparaatstatus van Desktop Analytics. Selecteer **Volgende** om door te gaan.  

4. Op de pagina **gebruikers toegang geven** :

    - **Desktop Analytics toestaan Directory rollen namens u te beheren**: Desktop Analytics wijst automatisch de eigenaar van de **werk ruimte** toe aan de Administrator-rol van **Desktop Analytics** . Als deze groepen al een **globale beheerder**zijn, is er geen wijziging.  

        Als u deze optie niet selecteert, voegt Desktop Analytics nog steeds gebruikers toe als leden van de beveiligings groep. Een **globale beheerder** moet hand matig de rol **Desktop Analytics-beheerder** voor de gebruikers toewijzen.  

        Zie [Administrator role permissions](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)(Engelstalig) in azure Active Directory voor meer informatie over het toewijzen van machtigingen voor beheerdersrol in azure Active Directory en de machtigingen die zijn toegewezen aan **bureau blad Analytics-beheerders**.  

    - Met Desktop Analytics wordt de beveiligings groep **eigen aren van werk ruimten** vooraf geconfigureerd in azure Active Directory voor het maken en beheren van werk ruimten en implementatie plannen. 

        Als u een gebruiker aan de groep wilt toevoegen, typt u de naam of het e-mail adres in de sectie **naam of e-mail adres invoeren** . Selecteer **Volgende** als u klaar bent.

5. Op de pagina om **uw werk ruimte**in te stellen:  

    > [!Note]  
    > Voor het volt ooien van deze stap moet de gebruiker machtigingen voor de **werkruimte eigenaar** hebben en aanvullende toegang tot het Azure-abonnement en de resource groep. Zie [vereisten](overview.md#prerequisites)voor meer informatie.  

    - Selecteer uw Azure-abonnement.  

    - Als u een bestaande werk ruimte voor desktop Analytics wilt gebruiken, selecteert u deze en gaat u verder met de volgende stap.  

    - Als u een werk ruimte voor desktop Analytics wilt maken, selecteert u **werk ruimte toevoegen**.  

        1. Voer de **naam van een werk ruimte**in.  

        2. Selecteer de vervolg keuzelijst om **de naam van het Azure-abonnement voor deze werk ruimte te selecteren**en kies het Azure-abonnement voor deze werk ruimte.  

        3. **Nieuwe maken** Resource groep of **gebruik bestaande**.  

        4. Selecteer de **regio** in de lijst en selecteer vervolgens **toevoegen**.  

6. Selecteer een nieuwe of bestaande werk ruimte en selecteer vervolgens **instellen als werk ruimte voor desktop Analytics**.  Selecteer vervolgens **door gaan** in het dialoog venster **bevestigen en toegang verlenen** .  

7. Kies op het tabblad nieuwe browser een account om u aan te melden. Selecteer de optie om **namens uw organisatie toestemming** te geven en selecteer **accepteren**.  


    > [!Note]  
    > Deze toestemming is het toewijzen van de MALogAnalyticsReader-toepassing de rol van Log Analytics lezer voor de werk ruimte. Deze toepassingsrol is vereist voor desktop Analytics. Zie [MALogAnalyticsReader Application Role](troubleshooting.md#bkmk_MALogAnalyticsReader)(Engelstalig) voor meer informatie.  

8. Selecteer **volgende**op de pagina om **uw werk ruimte**in te stellen.  

9. Selecteer op de pagina **laatste stappen** **naar bureau blad Analytics**. De **Start** pagina van bureau blad Analytics wordt weer gegeven op de Azure Portal.  



## <a name="connect-configuration-manager"></a>Verbinding maken met Configuration Manager

Gebruik deze procedure om Configuration Manager bij te werken, verbinding te maken met Desktop Analytics en apparaatinstellingen te configureren. Deze procedure is een eenmalig proces om uw hiërarchie te koppelen aan de Cloud service.  

### <a name="update-configuration-manager"></a>Configuration Manager bijwerken

Installeer de Configuration Manager versie 1902 update pakket (4500571) ter ondersteuning van de integratie met Desktop Analytics. Zie [Update pakket voor Configuration Manager current branch versie 1902](https://support.microsoft.com/help/4500571)voor meer informatie over deze update.

1. Werk de site bij met het update pakket voor versie 1902. Zie [updates binnen de console installeren](../core/servers/manage/install-in-console-updates.md)voor meer informatie.  

2. Clients bijwerken. U kunt dit proces vereenvoudigen door gebruik te maken van automatische client upgrade. Zie [upgrade-clients](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)voor meer informatie.  


### <a name="connect-to-the-service"></a>Verbinding maken met de service

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure-Services** . Selecteer **Azure-Services configureren** in het lint.  

2. Configureer de volgende instellingen op de pagina **Azure-Services** van de wizard Azure-Services:  

    - Geef een **naam** op voor het object in Configuration Manager  

    - Geef een optionele **Beschrijving** op die u kan helpen bij het identificeren van de service  

    - **Desktop Analytics** selecteren in de lijst met beschik bare Services  
  
   Selecteer **Next**.  

3. Selecteer op de pagina **app** de juiste **Azure-omgeving**. Selecteer vervolgens **Bladeren** voor de web-app.

4. Selecteer **maken** om eenvoudig een Azure AD-app toe te voegen voor de Desktop Analytics-verbinding.

5. Configureer de volgende instellingen in het venster **Server toepassing maken** :  

    - **Toepassings naam**: een beschrijvende naam voor de app in azure AD.

    - **URL van start pagina**: deze waarde wordt niet gebruikt door Configuration Manager, maar is vereist voor Azure AD. Standaard is deze waarde ingesteld op `https://ConfigMgrService`.  

    - **App-ID-URI**: deze waarde moet uniek zijn in uw Azure AD-Tenant. Het is in het toegangs token dat door de Configuration Manager-client wordt gebruikt om toegang tot de service aan te vragen. Standaard is deze waarde ingesteld op `https://ConfigMgrService`.  

    - **Geldigheids duur van geheime sleutel**: Kies **1 jaar** of **2 jaar** in de vervolg keuzelijst. Een jaar is de standaard waarde.  

    Selecteer **Aanmelden**. Nadat de verificatie naar Azure is geslaagd, wordt op de pagina de naam van de **Azure AD-Tenant** voor referentie weer gegeven.

    > [!Note]  
    > Voer deze stap uit als **globale beheerder**. Deze referenties worden niet opgeslagen door Configuration Manager. Deze persoon heeft geen machtigingen nodig in Configuration Manager en hoeft niet hetzelfde account te zijn dat de wizard Azure-Services uitvoert.  

    Selecteer **OK** om de web-app te maken in azure AD en sluit het dialoog venster Server toepassing maken. Selecteer **OK**in het dialoog venster server app. Selecteer vervolgens **volgende** op de pagina app van de wizard Azure-Services.  

6. Configureer de volgende instellingen op de pagina **Diagnostische gegevens** :  

    - **Commerciële id**: deze waarde moet automatisch worden ingevuld met de id van uw organisatie  

    - **Niveau van diagnostische gegevens voor Windows 10**: Selecteer ten minste **uitgebreid (beperkt)**  

    - **Apparaatnaam in diagnostische gegevens toestaan**: Selecteer **inschakelen**  
  
   Selecteer **Next**. Op de pagina **beschik bare functionaliteit** ziet u de functionaliteit van het bureau blad Analytics die beschikbaar is met de instellingen voor diagnostische gegevens van de vorige pagina. Selecteer **Next**.  

7. Configureer op de pagina **verzamelingen** de volgende instellingen:  

    - **Weergave naam**: de bureau blad Analytics-portal geeft deze Configuration Manager verbinding weer met behulp van deze naam. Gebruik het om onderscheid te maken tussen verschillende hiërarchieën. Bijvoorbeeld *test lab* of *productie*.  

    - **Doel verzameling**: deze verzameling bevat alle apparaten die Configuration Manager configureert met de instellingen voor uw commerciële id en diagnostische gegevens. Het is de volledige set apparaten waarmee Configuration Manager verbinding maakt met de Desktop Analytics-service.  

    - **Apparaten in de doel verzameling gebruiken een door de gebruiker geverifieerde proxy voor uitgaande communicatie**: deze waarde is standaard ingesteld op **Nee**. Stel dit in op **Ja**als dat nodig is in uw omgeving.  

    - **Specifieke verzamelingen selecteren om te synchroniseren met Desktop Analytics**: Selecteer **toevoegen** om extra verzamelingen op te treffen. Deze verzamelingen zijn beschikbaar in de Desktop Analytics-Portal om te groeperen met implementatie plannen. Zorg ervoor dat u verzamelingen van pilot-en pilot-uitsluitingen opneemt.  

        Deze verzamelingen blijven synchroniseren wanneer hun lidmaatschap wordt gewijzigd. Uw implementatie plan gebruikt bijvoorbeeld een verzameling met een lidmaatschaps regel voor Windows 7. Als deze apparaten worden bijgewerkt naar Windows 10 en Configuration Manager het lidmaatschap van de verzameling evalueert, worden deze apparaten uit het verzamelings-en implementatie plan verwijderd.  

8. Voltooi de wizard.  

Configuration Manager maakt een instellingen beleid voor het configureren van apparaten in de doel verzameling. Dit beleid bevat de instellingen voor diagnostische gegevens om apparaten in staat te stellen gegevens naar micro soft te verzenden. Standaard wordt het beleid voor clients elk uur bijgewerkt. Na het ontvangen van de nieuwe instellingen, kan het enkele uren duren voordat de gegevens beschikbaar zijn in Desktop Analytics.

> [!Note]  
> Zie [Windows-instellingen](enroll-devices.md#windows-settings)voor meer informatie over deze instellingen.  

Controleer de configuratie van uw apparaten op Desktop Analytics. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw het knoop punt **Desktop Analytics Servicing** uit en selecteer het dash board **verbindings status** .  

Configuration Manager synchroniseert uw verzamelingen binnen 60 minuten na het maken van de verbinding. Ga in de Desktop Analytics-Portal naar **globale pilot**en bekijk uw Configuration Manager apparaten. Het kan twee tot drie dagen duren voordat de rest van de portal volledige gegevens weergeeft. Zie [Data latentie](troubleshooting.md#data-latency)voor meer informatie.

## <a name="create-a-desktop-analytics-deployment-plan"></a>Een implementatie plan voor desktop Analytics maken

Gebruik deze procedure voor het maken van een implementatie plan in Desktop Analytics.

1. Open de [Desktop Analytics-Portal](https://aka.ms/desktopanalytics). Gebruik referenties met ten minste machtigingen voor **werk ruimte-inzenders** .  

2. Selecteer **implementatie plannen** in de groep beheren.  

3. Selecteer **maken**in het deel venster **implementatie plannen** .  

4. Configureer de volgende instellingen in het deel venster **implementatie plan maken** :  

    - **Naam**: een unieke naam voor het implementatie plan, bijvoorbeeld`Windows 10 pilot`  

    - **Producten en versies**: Selecteer het **Windows** -product en de laatst beschik bare aanbevolen versie. Bijvoorbeeld **Windows 10, versie 1809 (aanbevolen)**.  

    - **Apparaatgroepen**: Selecteer een of meer groepen op het tabblad Configuration Manager en selecteer vervolgens **instellen als doel groepen**. Deze groepen zijn verzamelingen gesynchroniseerd vanuit Configuration Manager.  

    - **Gereedheids regels**: deze regels helpen om te bepalen welke apparaten in aanmerking komen voor een upgrade. Selecteer **Windows-besturings systeem** en configureer de volgende instellingen:  

        - **Mijn computers krijgen automatisch Stuur Programma's van Windows Update**: de standaard instelling is **uitgeschakeld**, wat wordt aanbevolen bij het implementeren met Configuration Manager.  

        - **Definieer een lage drempel waarde voor het aantal installaties voor uw apps**: de standaard instelling is `2%` . Apps onder deze drempel waarde worden automatisch ingesteld op het *aantal kleine installaties*. Met Desktop Analytics worden deze invoeg toepassingen niet gevalideerd tijdens de test fase.  

            *Als een*app wordt geïnstalleerd op een hoger percentage computers dan deze drempel waarde, markeert het implementatie plan de app als een afdoende. Vervolgens kunt u het belang bepalen dat u tijdens de test fase wilt testen.  

    - **Voltooiings datum**: Kies de datum waarop Windows volledig moet worden geïmplementeerd op alle doel apparaten.  

5. Selecteer **Maken**. Het nieuwe plan wordt weer gegeven in de lijst met implementatie plannen terwijl het wordt verwerkt. Als u de verwerking wilt versnellen, moet u een gegevens vernieuwing op aanvraag aanvragen. Zie [Veelgestelde vragen over desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)voor meer informatie.

6. Open het implementatie plan door de naam ervan te selecteren.  

7. Selecteer in het menu voor het implementatie plan in de groep **voorbereiden** de optie **belang rijkheid identificeren**.  

    1. Selecteer op het tabblad **apps** de optie om alleen **niet-gecontroleerde** assets weer te geven.  

    2. Selecteer elke app en selecteer vervolgens **bewerken**. U kunt meer dan één app selecteren om tegelijkertijd te bewerken.  

    3. Kies een urgentie niveau in de lijst **urgentie** . Als u wilt dat Desktop Analytics de app tijdens de test valideert, selecteert u **kritiek** of **belang rijk**. Apps die zijn gemarkeerd als **niet belang rijk**, worden niet gevalideerd. Evalueer de [compatibiliteit](compat-assessment.md) en andere plan inzichten bij het toewijzen van urgentie niveaus.  

        Bij het toewijzen van urgentie niveaus kunt u ook kiezen voor de upgrade beslissing.  

    4. Selecteer **Opslaan** wanneer u klaar bent.  

8. Selecteer in het menu voor het implementatie plan in de groep **voorbereiden** de optie **pilot identificeren**.  

    1. Bekijk de aanbevolen apparaten voor de test.  

    2. Selecteer elk apparaat en selecteer **toevoegen aan pilot**. Als u niet akkoord gaat met de aanbeveling, selecteert u **vervangen**.  

        Voor meer informatie over hoe Desktop Analytics deze aanbevelingen doet, selecteert u het informatie pictogram in de rechter bovenhoek van het deel venster **prototype identificeren** .



## <a name="deploy-windows-10-in-configuration-manager"></a>Windows 10 in Configuration Manager implementeren

Gebruik deze procedure om Windows 10 in Configuration Manager te implementeren in de test groep.

- Als u er nog geen hebt, moet u eerst [een upgrade pakket voor het besturings systeem maken voor Windows 10](#bkmk_create-package)  

- Als u er nog geen hebt, moet u [een upgrade taken reeks voor het besturings systeem maken voor Windows 10](#bkmk_create-ts)  

- [De taken reeks implementeren](#bkmk_deploy-ts) met het implementatie plan voor desktop Analytics  

- [De taken reeks installeren](#bkmk_install-ts) vanuit software Center op een doel apparaat  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a>Een upgrade pakket voor het besturings systeem maken voor Windows 10

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **upgrade pakketten van het besturings systeem** .  

2. Klik op het tabblad **Start** van het lint in de groep **maken** op **upgrade pakket besturings systeem toevoegen**. Met deze actie wordt de wizard upgrade van besturings systeem toevoegen gestart.  

3. Geef op de pagina **gegevens bron** **het netwerkpad op naar de** installatie bron bestanden van het upgrade pakket van het besturings systeem. Bijvoorbeeld `\\server\share\path`.  

    > [!NOTE]  
    > De bron bestanden voor installatie bevatten Setup. exe en andere bestanden en mappen om het besturings systeem te installeren.  

4. Geef op de pagina **Algemeen** een unieke **naam** op voor het upgrade pakket van het besturings systeem.  

5. Voltooi de wizard Upgrade pakket besturings systeem toevoegen.  

#### <a name="distribute-content"></a>Inhoud distribueren

Distribueer vervolgens het upgrade pakket van het besturings systeem naar distributie punten.  

1. Selecteer het upgrade pakket voor het besturings systeem in de lijst. Klik op het tabblad **Start** van het lint in de groep **implementatie** op **inhoud distribueren**. De wizard inhoud distribueren wordt geopend.  

2. Controleer op de pagina **Algemeen** of de vermelde inhoud de inhoud is die u wilt distribueren en selecteer vervolgens **volgende**.  

3. Selecteer op de pagina **doel van inhoud** de optie **toevoegen**en kies **distributie punt**. Selecteer een bestaand distributie punt en selecteer vervolgens **OK**. Wanneer u klaar bent met het toevoegen van inhouds bestemmingen, selecteert u **volgende**.  

4. Voltooi de wizard inhoud distribueren.  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a>Een taken reeks voor de upgrade van een besturings systeem maken voor Windows 10

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens **taken reeksen**.  

2. Selecteer **taken reeks maken**op het tabblad **Start** van het lint in de groep **maken** .  

3. Selecteer op de pagina **nieuwe taken reeks maken** van de wizard taken reeks maken de optie **een besturings systeem bijwerken vanuit een upgrade pakket**en selecteer **volgende**.  

4. Geef op de pagina **taken reeks informatie** een naam op voor de **taken reeks** die de taken reeks identificeert.  

5. Geef op de pagina **Windows-besturings systeem bijwerken** de volgende instellingen op en selecteer **volgende**:  

    - **Upgrade pakket**: Geef het upgrade pakket op dat de bron bestanden voor het bijwerken van het besturings systeem bevat.  

    - **Editie-index**: als er meerdere OS Edition-indexen beschikbaar zijn in het pakket, selecteert u de gewenste editie-index. De wizard selecteert standaard de eerste index.  

    - **Product code**: Geef de Windows-product code op voor het besturings systeem dat u wilt installeren. Geef gecodeerde volume licentie sleutels of standaard product codes op. Als u een standaard product code gebruikt, scheidt u elke groep van vijf tekens met een streepje (-). Bijvoorbeeld: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Wanneer de upgrade is voor een volume licentie-editie, is de product code mogelijk niet vereist.  

        > [!Note]  
        > Deze product code kan een meervoudige activerings code (MAK) of een algemene volume licentie code (GVLK) zijn. Een GVLK wordt ook wel een configuratie sleutel voor de KMS-client (Key Management service) genoemd. Zie [volume activering plannen](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)voor meer informatie. Zie [bijlage a](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) van de Windows Server-activerings handleiding voor een lijst met installatie sleutels voor KMS-clients.

6. Selecteer op de pagina **updates toevoegen** de optie **volgende** om software-updates te installeren.  

7. Selecteer op de pagina **toepassingen installeren** de optie **volgende** om geen toepassingen te installeren.

8. Voltooi de wizard taken reeks maken.  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a>De taken reeks implementeren met het implementatie plan voor desktop Analytics

1. Ga in de Configuration Manager-console naar de **software bibliotheek**, vouw **Desktop Analytics Servicing**uit en selecteer het knoop punt **implementatie plannen** .  

2. Selecteer uw implementatie plan voor Windows 10 pilot en selecteer vervolgens **Details van het implementatie plan** in het lint.  

3. Kies in de tegel status van de **pilot** **taken reeks** in de vervolg keuzelijst en selecteer vervolgens **implementeren**.  

4. Selecteer op de pagina **Algemeen** van de wizard software implementeren de optie **Bladeren** naast het veld **Software** . Selecteer uw Windows 10-in-place upgrade taken reeks en selecteer **volgende**.  

    > [!Note]  
    > Met de integratie van het bureau blad Analytics maakt Configuration Manager automatisch pilot-en productie verzamelingen voor het implementatie plan. Voordat u deze kunt gebruiken, kan het enige tijd duren voordat deze verzamelingen worden gesynchroniseerd. Zie [problemen oplossen-gegevens latentie](troubleshooting.md#data-latency)voor meer informatie.<!-- 4984639 -->
    >
    > Deze verzameling is gereserveerd voor apparaten met een desktop Analytics-implementatie plan. Hand matige wijzigingen in deze verzameling worden niet ondersteund.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Selecteer op de pagina **inhoud** **toevoegen**en selecteer vervolgens **distributie punt**. Selecteer een beschikbaar distributie punt voor het hosten van de installatie-inhoud en selecteer **OK**. Selecteer vervolgens **Volgende**.  

6. Selecteer op de pagina **implementatie-instellingen** de optie **volgende** om de standaard instellingen te accepteren. (Een beschik bare installatie.)  

7. Selecteer op de pagina **planning** **volgende** om de standaard instellingen te accepteren. (Zo snel mogelijk beschikbaar.)  

8. Selecteer op de pagina **gebruikers ervaring** **volgende** om de standaard instellingen te accepteren. (Weer geven in Software Center en alleen meldingen weer geven wanneer de computer opnieuw wordt opgestart.)  

9. Selecteer op de pagina **waarschuwingen** **volgende** om de standaard instellingen te accepteren.  

10. Voltooi de wizard.  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a>De taken reeks installeren vanuit software Center

1. Meld u aan bij een apparaat dat lid is van het proef implementatie plan.  

2. Open **Software Center** en installeer het beschik bare besturings systeem voor Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Volgende stappen

Ga naar het volgende artikel voor meer informatie over implementatie plannen voor desktop Analytics.
> [!div class="nextstepaction"]  
> [Implementatieplannen](about-deployment-plans.md)

---
title: Aangepaste rapporten maken
titleSuffix: Configuration Manager
description: Definieer rapport modellen om te voldoen aan uw bedrijfs vereisten en implementeer vervolgens de rapport modellen om Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: fe570eeedc2c050bdaf27903d30ddffff63109d9
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879152"
---
# <a name="creating-custom-report-models-for-configuration-manager-in-sql-server-reporting-services"></a>Aangepaste rapport modellen maken voor Configuration Manager in SQL Server Reporting Services

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voorbeeld rapport modellen zijn opgenomen in Configuration Manager, maar u kunt ook rapport modellen definiëren om te voldoen aan uw eigen zakelijke behoeften en vervolgens het rapport model implementeren op Configuration Manager om te gebruiken wanneer u nieuwe rapporten op basis van modellen maakt. De volgende tabel geeft de stappen voor het maken en implementeren van een basisrapportmodel.  

> [!NOTE]  
>  Zie de rubriek [Steps for Creating an Advanced Report Model in SQL Server Reporting Services](#AdvancedReportModel) in dit onderwerp voor de stappen om een geavanceerder rapportmodel te maken.  

|Stap|Beschrijving|Meer informatie|  
|----------|-----------------|----------------------|  
|Controleer of SQL Server Business Intelligence Development Studio is geïnstalleerd|Rapportmodellen worden toegewezen en gebouwd met SQL Server Business Intelligence Development Studio. Controleer of SQL Server Business Intelligence Development Studio is geïnstalleerd op de computer waarop u het aangepaste rapportmodel maakt.|Zie voor meer informatie over SQL Server Business Intelligence Development Studio de documentatie bij SQL Server 2008.|  
|Maak een rapportmodelproject|Een rapportmodelproject bevat de definitie van de gegevensbron (een .ds file), de definitie van de gegevensbronweergave (een .dsv file) en het rapportmodel (een .smdl file).|Zie de sectie [To create the report model project](#BKMK_CreateReportModelProject) in dit onderwerp voor meer informatie.|  
|Een gegevensbron definiëren voor een rapportmodel|Na het voltooien van een rapportmodelproject definieert u een gegevensbron waarvandaan u bedrijfsgegevens importeert. Dit is normaal gesp roken de Configuration Manager-site database.|Zie de sectie [To define the data source for the report model](#BKMK_DefineReportModelDataSource) in dit onderwerp voor meer informatie.|  
|Een gegevensbronweergave definiëren voor een rapportmodel|Na de definitie van de gegevensbronnen die u gebruikt in uw rapportmodelproject, bestaat de volgende stap uit het definiëren van een gegevensbronweergave voor het project. Een gegevensbronweergave is een logisch datamodel dat is gebaseerd op een of meerdere gegevensbronnen. Gegevensbronweergaven bevatten toegang tot de fysieke objecten, zoals tabellen en weergaven, die zich in onderliggende gegevensbronnen bevinden. SQL Server Reporting Services genereert het rapportmodel vanaf de gegevensbronweergave.<br /><br /> Gegevensbronweergaven helpen u bij het ontwerpproces voor modellen door middel van een nuttige weergave van de gegevens die u hebt opgegeven. U kunt zonder de onderliggende gegevensbron te wijzigen tabellen en velden opnieuw benoemen en samengestelde velden en afgeleide tabellen toevoegen in een gegevensbronweergave. Voor een efficiënt model voegt u alleen die tabellen toe aan de gegevensbronweergave die u gaat gebruiken.|Zie de sectie [To define the data source view for the report model](#BKMK_DefineReportModelDataSourceView) in dit onderwerp voor meer informatie.|  
|Een rapportmodel maken|Een rapportmodel is een laag bovenop een database die bedrijven, velden en rollen kan identificeren. Bij publicatie kunnen Report Builder-gebruikers met behulp van deze modellen rapporten ontwikkelen zonder verdere kennis te hebben van databasestructuren of het samenstellen van query's. Modellen bestaan uit sets gerelateerde rapportitems die zijn gegroepeerd onder een beschrijvende naam, met vooraf gedefinieerde relaties tussen deze zakelijke items en met vooraf gedefinieerde berekeningen. Modellen worden gedefinieerd met behulp van een XML-taal, die SMDL (Semantic Model Definition Language) wordt genoemd. De bestandsnaamextensie voor rapportmodelbestanden is .smdl.|Zie de sectie [To create the report model](#BKMK_CreateReportModel) in dit onderwerp voor meer informatie.|  
|Een rapportmodel publiceren|Om een rapport samen te stellen met behulp van het model dat u zojuist hebt gemaakt, moet u het naar een rapportserver publiceren. De gegevensbron en gegevensbronweergave zijn in het model opgenomen wanneer het wordt gepubliceerd.|Zie de sectie [To publish the report model for use in SQL Server Reporting Services](#BKMK_PublishReportModel) in dit onderwerp voor meer informatie.|  
|Het rapport model implementeren naar Configuration Manager|Voordat u een aangepast rapport model kunt gebruiken in de **wizard Rapport maken** om een rapport op basis van een model te maken, moet u het rapport model implementeren op Configuration Manager.|Zie de sectie [To deploy the custom report model to Configuration Manager](#BKMK_DeployReportModel) in dit onderwerp voor meer informatie.|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>Stappen voor het maken van een basisrapportmodel in SQL Server Reporting Services  
 U kunt de volgende procedures gebruiken om een basis rapport model te maken die gebruikers op uw site kunnen gebruiken om bepaalde model rapporten op basis van gegevens te bouwen in één weer gave van de Configuration Manager Data Base. U maakt een rapportmodel met daarin informatie over de clientcomputers op uw site voor de auteur van het rapport. Deze informatie wordt opgehaald uit de weer gave **v_R_System** in de Configuration Manager-Data Base.  

 Controleer op de computer waar u deze procedures uitvoert of u SQL Server Business Intelligence Development Studio hebt geïnstalleerd en dat de computer netwerkverbinding heeft met de Reporting Services-puntserver. Zie voor meer informatie over SQL Server Business Intelligence Development Studio de documentatie bij SQL Server 2008.  

###  <a name="to-create-the-report-model-project"></a><a name="BKMK_CreateReportModelProject"></a>Het rapport model project maken  

1.  Klik op het bureaublad op **Start**, dan op **Microsoft SQL Server 2008**, en daarna op **SQL Server Business Intelligence Development Studio**.  

2.  Klik, nadat **SQL Server Business Intelligence Development Studio** geopend hebt in Microsoft Visual Studio, op **Bestand**, daarna op **Nieuw**, en tot slot op **Project**.  

3.  In het dialoogvenster **Nieuw project** selecteert u **Rapportmodelproject** in de lijst **Sjablonen** .  

4.  Geef in het **Naam** -vak een naam op voor dit rapportmodel. Typ voor dit voorbeeld **Simple_Model**.  

5.  Klik op **OK**om het rapportmodelproject te maken.  

6.  De oplossing **Simple_Model** wordt weergegeven in de **Solution Explorer**.  

    > [!NOTE]  
    >  Als u het deelvenster **Solution Explorer** niet kunt zien, klikt u op **Weergeven**en vervolgens op **Solution Explorer**.  

###  <a name="to-define-the-data-source-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSource"></a>De gegevens bron voor het rapport model definiëren  

1.  Klik in het deelvenster **Solution Explorer** van **SQL Server Business Intelligence Development Studio**met de rechtermuisknop op **Gegevensbronnen** om **Nieuwe gegevensbron toevoegen**te selecteren.  

2.  Klik op de pagina **Welkom bij de wizard Gegevensbron** op **Volgende**.  

3.  Controleer op de pagina **De definitie voor de verbinding selecteren** of **Een gegevensbron maken op basis van een bestaande of nieuwe verbinding** is geselecteerd en klik vervolgens op **Nieuw**.  

4.  Specificeer in het dialoogvenster **Verbindingsbeheer** de volgende verbindingseigenschappen voor de gegevensbron:  

    -   **Server naam**: Typ de naam van de Configuration Manager-site database server of Selecteer deze in de lijst. Als u werkt met een benoemd exemplaar in plaats van het standaard exemplaar, typt u de naam van het &lt; *database server* > \\ &lt; *exemplaar*>.  

    -   Selecteer **Windows-verificatie gebruiken**.  

    -   Selecteer in de lijst **een database naam selecteren of invoeren** de naam van uw Configuration Manager-site database.  

5.  Klik op **Verbinding testen**om de verbinding met de database te controleren.  

6.  Als de verbinding slaagt, klikt u op **OK** om het dialoogvenster **Verbindingsbeheer** te sluiten. Als de verbinding niet slaagt, controleer dan of de informatie die u hebt ingevoerd juist is en klik daarna opnieuw op **Verbinding testen** .  

7.  Controleer op de pagina **De definitie voor de verbinding selecteren** of **Een gegevensbron maken op basis van een bestaande of nieuwe verbinding** is geselecteerd, controleer of de gegevensbron die u zojuist hebt opgegeven is geselecteerd in **Gegevensverbindingen**en klik vervolgens op **Volgende**.  

8.  Geef in **Naam van gegevensbron**een naam op voor de gegevensbron en klik vervolgens op **Voltooien**. Typ voor dit voorbeeld **Simple_Model**.  

9. De gegevensbron **Simple_Model.ds** wordt nu weergegeven in **Solution Explorer** onder het knooppunt **Gegevensbronnen** .  

    > [!NOTE]  
    >  Als u de eigenschappen van een bestaande gegevensbron wilt bewerken, dubbelklikt u op de gegevensbron in de map **Gegevensbronnen** van het deelvenster **Solution Explorer** om de gegevensbroneigenschappen weer te geven in Gegevensbronontwerper.  

###  <a name="to-define-the-data-source-view-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSourceView"></a>De gegevens bron weergave voor het rapport model definiëren  

1.  Klik in **Solution Explorer**met de rechtermuisknop op **Gegevensbronweergaven** om **Nieuwe gegevensbronweergave toevoegen**te selecteren.  

2.  Klik op de pagina **Welkom bij de wizard Gegevensbronweergave** op **Volgende**. De pagina **Een gegevensbron selecteren** wordt weergegeven.  

3.  Controleer in het venster **Relationele gegevensbronnen** of de gegevensbron **Simple_Model** is geselecteerd en klik vervolgens op **Volgende**.  

4.  Selecteer op de pagina **Tabellen en weergaven selecteren** de volgende weergave in de lijst **Beschikbare objecten** die u wilt gebruiken in het rapportmodel: **v_R_System (dbo)**.  

    > [!TIP]  
    >  Klik voor hulp bij het vinden van weergaven in de lijst **Beschikbare objecten** op de kop **Naam** bovenin de lijst om de objecten op alfabetische volgorde te sorteren.  

5.  Nadat u de weer gave hebt geselecteerd, klikt **>** u op om het object over te zetten naar de lijst met **opgenomen objecten** .  

6.  Als de pagina **Overeenkomst met naam** wordt weergeven, accepteert u de standaardselecties en klikt u op **Volgende**.  

7.  Wanneer u de nodige objecten hebt geselecteerd, klikt u op **Volgende**en specificeert u een naam voor de gegevensbronweergave. Typ voor dit voorbeeld **Simple_Model**.  

8.  Klik op **Voltooien**. De gegevensbronweergave **Simple_Model.dsv** wordt in de map **Gegevensbronweergaven** van **Solution Explorer**weergegeven.  

###  <a name="to-create-the-report-model"></a><a name="BKMK_CreateReportModel"></a>Het rapport model maken  

1.  Klik in **Solution Explorer**met de rechtermuisknop op **Rapportmodellen** om **Nieuw rapportmodel toevoegen**te selecteren.  

2.  Klik op de pagina **Welkom bij de wizard Rapportmodel** op **Volgende**.  

3.  Selecteer in de pagina **Gegevensbronweergaven selecteren** de gegevensbronweergave in de lijst **Beschikbare gegevensbronweergaven** en klik op **Volgende**. Selecteer voor dit voorbeeld **Simple_Model.dsv**.  

4.  Accepteer op de pagina **Aanmaakregels voor rapportmodel selecteren** de standaardwaarden en klik vervolgens op **Volgende**.  

5.  Controleer op de pagina **Modelstatistieken verzamelen** of **Modelstatistieken bijwerken voor het aanmaken** is geselecteerd en klik vervolgens op **Volgende**.  

6.  Geef op de pagina **De wizard wordt voltooid** een naam op voor het rapportmodel. Controleer voor dit voorbeeld of **Simple_Model** wordt weergegeven.  

7.  Klik op **Uitvoeren**om de wizard te voltooien en het rapportmodel te maken.  

8.  Klik op **Voltooien**om de wizard te sluiten. Het rapportmodel wordt weergegeven in het venster Ontwerpen.  

###  <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a><a name="BKMK_PublishReportModel"></a> To publish the report model for use in SQL Server Reporting Services  

1.  Klik in **Solution Explorer**met de rechtermuisknop op het rapportmodel om **Implementeren**te selecteren. Voor dit voorbeeld is het rapportmodel **Simple_Model.smdl**.  

2.  Controleer de implementatiestatus onderin de linkerhoek van het venster **SQL Server Business Intelligence Development Studio** . Wanneer de implementatie is voltooid, wordt **Implementatie geslaagd** weergegeven. Als de implementatie mislukt, wordt de reden hiervoor weergegeven in het venster **Uitvoer** . Het nieuwe rapportmodel is nu beschikbaar op uw SQL Server Reporting Services-website.  

3.  Klik op **Bestand**, op **Alles opslaan**en sluit **SQL Server Business Intelligence Development Studio**.  

###  <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a><a name="BKMK_DeployReportModel"></a>Het aangepaste rapport model implementeren naar Configuration Manager  

1. Vind de map waarin u het rapportmodelproject hebt gemaakt. Bijvoorbeeld:%*userprofile*% \ Documents\Visual Studio 2008 \ \\ * &lt; project name van projecten \> .*  

2. Kopieer de volgende bestanden van de map rapportmodelproject naar een tijdelijke map op uw computer:  

   -   * &lt; Model naam \> * **. DSV**  

   -   * &lt; Model naam \> * **. smdl**  

3. Open de voorgaande bestanden met een tekstbewerkingstoepassing, zoals Kladblok.  

4. Zoek in de bestands _ &lt; model \> naam_**. DSV**de eerste regel van het bestand, die als volgt wordt gelezen:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Bewerk deze regel als volgt:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`  

5. Kopieer de gehele inhoud van het bestand naar het Windows-klembord.  

6. Sluit de _ &lt; naam \> _van het bestands model **. DSV**.  

7. Zoek in de bestands _ &lt; model \> naam_**. smdl**de laatste drie regels van het bestand, die er als volgt uitzien:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Plak de inhoud van de bestands _ &lt; model naam \> _**. DSV** direct vóór de laatste regel van het bestand (** &lt; semanticmodel bevindt \> **).  

9. Sla de _ &lt; naam \> _van het bestands model op en sluit deze **. smdl**.  

10. Kopieer de _ &lt; naam \> _van het bestands model **. smdl** naar de map *% Program Files%* \Microsoft Configuration Manager \AdminConsole\XmlStorage\Other op de Configuration Manager site server.  

    > [!IMPORTANT]  
    >  Nadat u het rapport model bestand naar de Configuration Manager-site server hebt gekopieerd, moet u de Configuration Manager-console sluiten en opnieuw starten voordat u het rapport model kunt gebruiken in de **wizard Rapport maken**.  

##  <a name="steps-for-creating-an-advanced-report-model-in-sql-server-reporting-services"></a><a name="AdvancedReportModel"></a> Steps for Creating an Advanced Report Model in SQL Server Reporting Services  
 U kunt de volgende procedures gebruiken om een geavanceerd rapport model te maken die gebruikers op uw site kunnen gebruiken om op basis van gegevens in meerdere weer gaven van de Configuration Manager-Data Base bepaalde rapporten op basis van modellen te bouwen. U maakt een rapportmodel met daarin informatie over de clientcomputers en het besturingssysteem dat is geïnstalleerd op deze computers voor de auteur van het rapport. Deze informatie wordt opgehaald uit de volgende weer gaven in de Configuration Manager-Data Base:  

- **V_R_System**: bevat informatie over gedetecteerde computers en de Configuration Manager-client.  

- **V_GS_OPERATING_SYSTEM**: bevat informatie over het besturingssysteem dat op de clientcomputer is geïnstalleerd.  

  Geselecteerde items van de voorgaande weergaven worden in één lijst samengevoegd, voorzien van beschrijvende namen en vervolgens gepresenteerd aan de auteur van een rapport in Report Builder om in bepaalde rapporten te gebruiken.  

  Controleer op de computer waar u deze procedures uitvoert of u SQL Server Business Intelligence Development Studio hebt geïnstalleerd en dat de computer netwerkverbinding heeft met de Reporting Services-puntserver. Voor gedetailleerde informatie over SQL Server Business Intelligence Development Studio, zie de SQL Server documentatie.  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  Klik op het bureaublad op **Start**, dan op **Microsoft SQL Server 2008**, en daarna op **SQL Server Business Intelligence Development Studio**.  

2.  Klik, nadat **SQL Server Business Intelligence Development Studio** geopend hebt in Microsoft Visual Studio, op **Bestand**, daarna op **Nieuw**, en tot slot op **Project**.  

3.  In het dialoogvenster **Nieuw project** selecteert u **Rapportmodelproject** in de lijst **Sjablonen** .  

4.  Geef in het **Naam** -vak een naam op voor dit rapportmodel. Typ voor dit voorbeeld **Advanced_Model**.  

5.  Klik op **OK**om het rapportmodelproject te maken.  

6.  De oplossing **Advanced_Model** wordt weergegeven in **Solution Explorer**.  

    > [!NOTE]  
    >  Als u het deelvenster **Solution Explorer** niet kunt zien, klikt u op **Weergeven**en vervolgens op **Solution Explorer**.  

#### <a name="to-define-the-data-source-for-the-report-model"></a>To define the data source for the report model  

1.  Klik in het deelvenster **Solution Explorer** van **SQL Server Business Intelligence Development Studio**met de rechtermuisknop op **Gegevensbronnen** om **Nieuwe gegevensbron toevoegen**te selecteren.  

2.  Klik op de pagina **Welkom bij de wizard Gegevensbron** op **Volgende**.  

3.  Controleer op de pagina **De definitie voor de verbinding selecteren** of **Een gegevensbron maken op basis van een bestaande of nieuwe verbinding** is geselecteerd en klik vervolgens op **Nieuw**.  

4.  Specificeer in het dialoogvenster **Verbindingsbeheer** de volgende verbindingseigenschappen voor de gegevensbron:  

    -   **Server naam**: Typ de naam van de Configuration Manager-site database server of Selecteer deze in de lijst. Als u werkt met een benoemd exemplaar in plaats van het standaard exemplaar, typt u de naam van het &lt; *database server* > \\ &lt; *exemplaar*>.  

    -   Selecteer **Windows-verificatie gebruiken**.  

    -   Selecteer in de lijst **Selecteer of voer een database naam** de naam van uw Configuration Manager-site database.  

5.  Klik op **Verbinding testen**om de verbinding met de database te controleren.  

6.  Als de verbinding slaagt, klikt u op **OK** om het dialoogvenster **Verbindingsbeheer** te sluiten. Als de verbinding niet slaagt, controleer dan of de informatie die u hebt ingevoerd juist is en klik daarna opnieuw op **Verbinding testen** .  

7.  Controleer op de pagina **Selecteren hoe u de verbinding wilt definiëren** of **Een gegevensbron maken op basis van een bestaande of nieuwe verbinding** is geselecteerd, controleer of de gegevensbron die u zojuist hebt gespecificeerd, geselecteerd is in de keuzelijst **Gegevensverbindingen** en klik vervolgens op **Volgende**.  

8.  Specificeer in **Naam gegevensbron**een naam voor de gegevensbron en klik daarna op **Voltooien**. Typ voor dit voorbeeld **Advanced_Model**.  

9. De gegevensbron **Advanced_Model.ds** wordt weergegeven in **Solution Explorer** onder het knooppunt **Gegevensbronnen** .  

    > [!NOTE]  
    >  Als u de eigenschappen van een bestaande gegevensbron wilt bewerken, dubbelklikt u op de gegevensbron in de map **Gegevensbronnen** van het deelvenster **Solution Explorer** om de gegevensbroneigenschappen weer te geven in Gegevensbronontwerper.  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>To define the data source view for the report model  

1. Klik in **Solution Explorer**met de rechtermuisknop op **Gegevensbronweergaven** om **Nieuwe gegevensbronweergave toevoegen**te selecteren.  

2. Klik op de pagina **Welkom bij de wizard Gegevensbronweergave** op **Volgende**. De pagina **Een gegevensbron selecteren** wordt weergegeven.  

3. Controleer in het venster **Relationele gegevensbronnen** of de gegevensbron **Advanced_Model** is geselecteerd, en klik vervolgens op **Volgende**.  

4. Selecteer op de pagina **Tabellen en weergaven selecteren** de volgende weergaven in de lijst **Beschikbare objecten** die in het rapportmodel gebruikt zullen worden:  

   - **v_R_System (dbo)**  

   - **v_GS_OPERATING_SYSTEM (dbo)**  

     Nadat u elke weer gave hebt geselecteerd, klikt **>** u op om het object over te zetten naar de lijst met **opgenomen objecten** .  

   > [!TIP]  
   >  Klik voor hulp bij het vinden van weergaven in de lijst **Beschikbare objecten** op de kop **Naam** bovenin de lijst om de objecten op alfabetische volgorde te sorteren.  

5. Als het dialoogvenster **Namen matchen** verschijnt, accepteer dan de standaard selecties en klik op **Volgende**.  

6. Wanneer u de gewenste objecten geselecteerd hebt, klikt u op **Volgende**, en vervolgens geeft u een naam op voor de gegevensbronweergave. Typ voor dit voorbeeld **Advanced_Model**.  

7. Klik op **Voltooien**. De gegevensbronweergave **Advanced_Model.dsv** wordt weergegeven in de map **Gegevensbronweergaven** van **Solution Explorer**.  

#### <a name="to-define-relationships-in-the-data-source-view"></a>Relaties in de gegevensbronweergave definiëren  

1.  Dubbelklik in **Solution Explorer**op **Advanced_Model.dsv** om het Ontwerpen-venster te openen.  

2.  Klik met de rechtermuisknop op de titelbalk van het venster **v_R_System** om **Tabel vervangen**te selecteren en klik vervolgens op **Met nieuwe benoemde query**.  

3.  Klik in het dialoogvenster **Benoemde query maken** op het pictogram **Tabel toevoegen** (meestal het laatste pictogram in het lint).  

4.  Klik in het dialoogvenster **Tabel toevoegen** op het tabblad **Weergaven** , selecteer **V_GS_OPERATING_SYSTEM** in de lijst en klik daarna op **Toevoegen**.  

5.  Klik op **Sluiten** om het dialoogvenster **Tabel toevoegen** te sluiten.  

6.  Geef in het dialoogvenster **Benoemde query maken** de volgende informatie op:  

    -   **Naam:** geef de naam voor de query op. Typ voor dit voorbeeld **Advanced_Model**.  

    -   **Beschrijving:** geef een beschrijving op voor de query. Typ voor dit voorbeeld **Example Reporting Services report model**.  

7.  Selecteer in het venster **v_R_System** de volgende items in de lijst met objecten die in het rapportmodel moeten worden getoond:  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  Selecteer in het venster **v_GS_OPERATING_SYSTEM** de volgende items in de lijst met objecten die in het rapportmodel moeten worden getoond:  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. Om de objecten in deze weergaven als één lijst aan de rapportauteur te presenteren, moet u een relatie tussen de twee tabellen of weergaven aangeven door middel van een join. U kunt de twee weergaven met elkaar verbinden via het object **ResourceID**, dat in beide weergaven aanwezig is.  

10. Klik in het venster **v_R_System** op het object **ResourceID** en sleep het naar het object **ResourceID** in het venster **v_GS_OPERATING_SYSTEM** .  

11. Klik op **OK.**  

12. Het venster **Advanced_Model** vervangt het venster **v_R_System** en bevat alle benodigde objecten voor het rapportmodel uit de weergaven **v_R_System** en **v_GS_OPERATING_SYSTEM** . U kunt het venster **v_GS_OPERATING_SYSTEM** nu verwijderen uit de gegevensbronweergave-ontwerper. Klik met de rechtermuisknop op de titelbalk van het venster **v_GS_OPERATING_SYSTEM** om **Tabel uit DSV verwijderen**te selecteren. Klik in het dialoogvenster **Objecten verwijderen** op **OK** om de verwijdering te bevestigen.  

13. Klik op **Bestand** en vervolgens op **Alles opslaan**.  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  Klik in **Solution Explorer**met de rechtermuisknop op **Rapportmodellen** om **Nieuw rapportmodel toevoegen**te selecteren.  

2.  Klik op de pagina **Welkom bij de wizard Rapportmodel** op **Volgende**.  

3.  Selecteer op de pagina **Gegevensbronweergave selecteren** de gegevensbronweergave in de lijst **Beschikbare gegevensbronweergaven** en klik vervolgens op **Volgende**. Selecteer voor dit voorbeeld **Simple_Model.dsv**.  

4.  Wijzig op de pagina **Aanmaakregels voor een rapportmodel selecteren** niet de standaardwaarden, en klik op **Volgende**.  

5.  Controleer op de pagina **Modelstatistieken verzamelen** of **Modelstatistieken bijwerken voor het aanmaken** is geselecteerd en klik vervolgens op **Volgende**.  

6.  Geef op de pagina **De wizard wordt voltooid** een naam op voor het rapportmodel. Controleer in dit voorbeeld of **Advanced_Model** is weergegeven.  

7.  Klik op **Uitvoeren**om de wizard te voltooien en het rapportmodel te maken.  

8.  Klik op **Voltooien**om de wizard te sluiten.  

9. Het rapportmodel wordt weergegeven in het venster Ontwerpen.  

#### <a name="to-modify-object-names-in-the-report-model"></a>Objectnamen in het rapportmodel wijzigen  

1.  Klik in **Solution Explorer**met de rechtermuisknop op een rapportmodel om **Designer bekijken**te selecteren. Selecteer voor dit voorbeeld **Advanced_Model.smdl**.  

2.  Klik in de ontwerpweergave van het rapportmodel met de rechtermuisknop op een willekeurige objectnaam om **Naam wijzigen**te selecteren.  

3.  Voer een nieuwe naam in voor het geselecteerde object en druk daarna op Enter. U kunt bijvoorbeeld het object **CSD_Version_0** de nieuwe naam **Windows Servicepackversie**geven.  

4.  Wanneer u klaar bent met het wijzigen van objectnamen klikt u op **Bestand**en vervolgens op **Alle opslaan**.  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>To publish the report model for use in SQL Server Reporting Services  

1.  Klik in **Solution Explorer**met de rechtermuisknop op **Advanced_Model.smdl** om **Implementeren**te selecteren.  

2.  Controleer de implementatiestatus onderin de linkerhoek van het venster **SQL Server Business Intelligence Development Studio** . Wanneer de implementatie is voltooid, wordt **Implementatie geslaagd** weergegeven. Als de implementatie mislukt, wordt de reden hiervoor weergegeven in het venster **Uitvoer** . Het nieuwe rapportmodel is nu beschikbaar op uw SQL Server Reporting Services-website.  

3.  Klik op **Bestand**, op **Alles opslaan**en sluit **SQL Server Business Intelligence Development Studio**.  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1. Vind de map waarin u het rapportmodelproject hebt gemaakt. Bijvoorbeeld:%*userprofile*% \ Documents\Visual Studio 2008 \ \\ * &lt; project name van projecten \> .*  

2. Kopieer de volgende bestanden van de map rapportmodelproject naar een tijdelijke map op uw computer:  

   -   * &lt; Model naam \> * **. DSV**  

   -   * &lt; Model naam \> * **. smdl**  

3. Open de voorgaande bestanden met een tekstbewerkingstoepassing, zoals Kladblok.  

4. Zoek in de bestands _ &lt; model \> naam_**. DSV**de eerste regel van het bestand, die als volgt wordt gelezen:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Bewerk deze regel als volgt:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`

5. Kopieer de gehele inhoud van het bestand naar het Windows-klembord.  

6. Sluit de _ &lt; naam \> _van het bestands model **. DSV**.  

7. Zoek in de bestands _ &lt; model \> naam_**. smdl**de laatste drie regels van het bestand, die er als volgt uitzien:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Plak de inhoud van de bestands _ &lt; model naam \> _**. DSV** direct vóór de laatste regel van het bestand (** &lt; semanticmodel bevindt \> **).  

9. Sla de _ &lt; naam \> _van het bestands model op en sluit deze **. smdl**.  

10. Kopieer de _ &lt; naam \> _van het bestands model **. smdl** naar de map *% Program Files%* \Microsoft endpoint Manager\AdminConsole\XmlStorage\Other op de site server van Configuration Manager.  

    > [!IMPORTANT]  
    >  Nadat u het rapport model bestand naar de Configuration Manager-site server hebt gekopieerd, moet u de Configuration Manager-console sluiten en opnieuw starten voordat u het rapport model kunt gebruiken in de **wizard Rapport maken**.  

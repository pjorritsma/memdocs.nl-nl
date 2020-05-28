---
title: Asset Intelligence configureren
titleSuffix: Configuration Manager
description: Asset Intelligence instellen in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1a5c89d3fdd82bfa654f806c6931bde2621e714b
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906612"
---
# <a name="configure-asset-intelligence-in-configuration-manager"></a>Asset Intelligence configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Asset Intelligence voor raden en beheert het gebruik van software licenties.   

## <a name="steps-to-configure-asset-intelligence"></a>Stappen voor het configureren van Asset Intelligence  
   

- **Stap 1**: voor het verzamelen van de inventarisatie gegevens die zijn vereist voor Asset Intelligence-rapporten, moet u de client agent voor hardware-inventaris inschakelen, zoals beschreven in de [hardware-inventaris uitbreiden](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).
- **Stap 2**: [Schakel de Asset Intelligence-rapportage klassen voor hardware-inventarisatie in](#BKMK_EnableAssetIntelligence).  
- **Stap 3**: [een Asset Intelligence synchronisatie punt installeren](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **Stap 4**: [controle van geslaagde aanmeldings gebeurtenissen inschakelen](#BKMK_EnableSuccessLogonEvents)  
- **Stap 5**: [software licentie gegevens importeren](#BKMK_ImportSoftwareLicenseInformation)  
- **Stap 6**: [Asset Intelligence onderhouds taken configureren](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Als u Asset Intelligence in Configuration Manager sites wilt inschakelen, moet u een of meer Asset Intelligence-rapportage klassen voor hardware-inventarisatie inschakelen. U kunt de klassen inschakelen op de startpagina **Asset Intelligence** of in de werkruimte **Beheer** , in het knooppunt **Clientinstellingen** in de eigenschappen voor clientinstellingen. Gebruik een van de volgende procedures.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Asset Intelligence-rapportageklassen voor hardware-inventarisatie inschakelen via de startpagina Asset Intelligence  

1.  Kies in de Configuration Manager-console de optie **activa en naleving**  >  **Asset Intelligence**.  

3.  Klik op het tabblad **Start** in de groep **Asset Intelligence** op **inventaris klassen bewerken**.   

4.  Als u Asset Intelligence rapportage wilt inschakelen, selecteert u **alle Asset Intelligence rapportage klassen inschakelen** of **alleen de geselecteerde Asset Intelligence rapportage klassen inschakelen**en selecteert u ten minste één rapportage klasse in de weer gegeven klassen.  

    > [!NOTE]  
    >  Asset Intelligence-rapporten die afhankelijk zijn van de hardware-inventarisatieklassen die u inschakelt via deze procedure, bevatten pas gegevens als clients hebben gescand op hardware-inventaris en deze hebben geretourneerd.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Asset Intelligence-rapportageklassen voor hardware-inventarisatie inschakelen via de eigenschappen voor clientinstellingen  

1.  Kies in de Configuration Manager-console **Administration**de instellingen van de  >   **Client Settings**  >  **client agent standaard instellingen**voor de beheer client. Als u aangepaste client instellingen hebt gemaakt, kunt u die in plaats daarvan selecteren.  

3.  Kies **Eigenschappen**in het tabblad **Start** > groep **Eigenschappen** .   

4.  Kies **Hardware Inventory**  >  **set classes**. .  

5.  Kies **filteren op categorie**  >  **Asset Intelligence rapportage klassen**. De lijst met klassen wordt vernieuwd met alleen de Asset Intelligence-rapportageklassen voor hardware-inventarisatie.  

6.  Selecteer ten minste één rapportage klasse in de lijst.  

    > [!NOTE]  
    >  Asset Intelligence-rapporten die afhankelijk zijn van de hardware-inventarisatieklassen die u inschakelt via deze procedure, bevatten pas gegevens als clients hebben gescand op hardware-inventaris en deze hebben geretourneerd.  
  

###  <a name="install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

De site systeemrol Asset Intelligence synchronisatie punt wordt gebruikt om Configuration Manager-sites te verbinden met System Center online om Asset Intelligence catalogus gegevens te synchroniseren. Het Asset Intelligence synchronisatie punt kan alleen worden geïnstalleerd op een site systeem dat zich bevindt op de site op het hoogste niveau van de Configuration Manager hiërarchie en vereist Internet toegang om te synchroniseren met System Center online via TCP-poort 443.

Via het Asset Intelligence-synchronisatiepunt kunnen nieuwe Asset Intelligence-catalogusgegevens worden gedownload en kan informatie over aangepaste softwaretitels voor categorisatie worden geüpload naar System Center Online. Micro soft behandelt alle geüploade software titels als open bare informatie. Zorg ervoor dat uw aangepaste software titels geen vertrouwelijke of eigendoms informatie bevatten. Zie [Request a catalog update for uncategorized software titles](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate)voor meer informatie over het aanvragen van categorisatie van softwaretitels.  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Een sitesysteemrol Asset Intelligence-synchronisatiepunt installeren  

1.  Kies in de Configuration Manager-console **beheer** >  **site configuratie**  >  **servers en site systeem rollen**.  

3.  Voeg de site systeemrol Asset Intelligence synchronisatie punt toe aan een nieuwe of bestaande site systeem server:  

    -  Voor een **nieuwe site systeem server**: Klik op het tabblad **Start** in de groep **maken** op **site systeem server maken** om de wizard te starten.   

        > [!NOTE]  
        >  Wanneer Configuration Manager een site systeemrol installeert, worden de installatie bestanden standaard geïnstalleerd op het eerste beschik bare vaste-schijf station met NTFS-indeling dat de meest beschik bare vrije schijf ruimte heeft. Als u wilt voor komen dat Configuration Manager op specifieke stations installeert, maakt u een leeg bestand met de naam No_sms_on_drive. SMS en kopieert u het naar de hoofdmap van het station voordat u de site systeem server installeert.  

    -  Voor een **bestaande site systeem server**: Kies de server waarop u de site systeemrol Asset Intelligence synchronisatie punt wilt installeren. Wanneer u een server kiest, worden in het detail venster een lijst weer gegeven met de site systeem rollen die al op de server zijn geïnstalleerd.  

         Klik op het tabblad **Start** in de groep **Server** op **site systeemrol toevoegen** om de wizard te starten.  

4.  Voltooi de pagina **Algemeen** . Wanneer u de sitesysteemrol Asset Intelligence-synchronisatiepunt aan een bestaande sitesysteemserver wilt toevoegen, dient u de eerder geconfigureerde waarden te verifiëren.  

5.  Selecteer **Asset Intelligence synchronisatie punt** in de lijst met beschik bare rollen op de pagina **selectie van systeem rollen** .  

6.  Kies op de pagina **Verbindings instellingen van het Asset Intelligence synchronisatie punt** op **volgende**.  

     Standaard is de instelling **Dit Asset Intelligence-synchronisatiepunt gebruiken** geselecteerd en deze instelling kan niet worden gewijzigd op deze pagina. Omdat System Center Online alleen netwerkverkeer via TCP-poort 443 accepteert, kan de instelling **SSL-poortnummer** niet worden geconfigureerd op deze pagina van de wizard.  

7.  U kunt desgewenst een pad naar het bestand met het System Center online-verificatie certificaat (. pfx) opgeven. Normaal gesproken geeft u geen pad voor het certificaat op omdat het verbindingscertificaat automatisch wordt geleverd tijdens de installatie van de siterol.  

8.  Op de pagina **proxyserver instellingen** geeft u op of het Asset Intelligence synchronisatie punt een proxy server gebruikt wanneer verbinding met System Center online wordt gemaakt om de catalogus te synchroniseren en of referenties moeten worden gebruikt om verbinding te maken met de proxy server.  

    > [!WARNING]  
    >  Als een proxyserver vereist is om verbinding te maken met System Center Online, kan het verbindingscertificaat ook worden verwijderd als het wachtwoord voor het geconfigureerde gebruikersaccount voor verificatie van de proxyserver verloopt.  

9. Geef op de pagina **Synchronisatieplanning** op of de Asset Intelligence-catalogus volgens een schema moet worden gesynchroniseerd. Als u de synchronisatieplanning inschakelt, kunt u een eenvoudig of aangepast synchronisatieschema opgeven. Tijdens de geplande synchronisatie maakt het Asset Intelligence-synchronisatiepunt verbinding met System Center Online om de meest recente Asset Intelligence-catalogus op te halen. U kunt de Asset Intelligence catalogus hand matig synchroniseren via het knoop punt Asset Intelligence in de Configuration Manager-console. Zie de sectie de [Asset Intelligence catalogus hand matig synchroniseren](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) in de [bewerkingen voor Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)voor de stappen om de Asset Intelligence catalogus hand matig te synchroniseren.  

10. Voltooi de wizard 

###  <a name="enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Vier Asset Intelligence-rapporten bevatten gegevens die zijn verzameld uit de Windows-beveiligingslogboeken op clientcomputers. U kunt als volgt de aanmeldings instellingen voor computer beveiligings beleid configureren om de controle van geslaagde aanmeldings gebeurtenissen in te scha kelen.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>De registratie van geslaagde aanmeldingsgebeurtenissen inschakelen op basis van lokaal beveiligingsbeleid  

1.  Kies op een Configuration Manager-client computer **Start**  >  **systeem beheer**  >  **lokale beveiligings beleid**.  

2.  Vouw in het dialoog venster **lokaal beveiligings beleid** onder **beveiligings instellingen**het item **lokaal beleid**uit en kies vervolgens **controle beleid**.  

3.  Dubbel klik in het deel venster met resultaten op **aanmeldings gebeurtenissen controleren**, Controleer of het selectie vakje **geslaagd** is ingeschakeld en klik vervolgens op **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>De registratie van geslaagde aanmeldingsgebeurtenissen inschakelen op basis van een Active Directory-domeinbeveiligingsbeleid  

1.  Kies op een domein controller computer **Start**, wijs **systeem beheer**aan en kies vervolgens **domein beveiligings beleid**.  

2.  Vouw in het dialoog venster **lokaal beveiligings beleid** onder **beveiligings instellingen**het item **lokaal beleid**uit en kies vervolgens **controle beleid**.  

3.  Dubbel klik in het deel venster met resultaten op **aanmeldings gebeurtenissen controleren**, Controleer of het selectie vakje **geslaagd** is ingeschakeld en klik vervolgens op **OK**.  

###  <a name="import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 In de volgende secties worden de procedures beschreven die nodig zijn om micro soft-en algemene software licentie gegevens te importeren in de Configuration Manager-site database met behulp van de wizard software licentie importeren. Wanneer u softwarelicentiegegevens vanuit licentieverklaringsbestanden in de sitedatabase importeert, moet het siteservercomputeraccount over de machtiging **Volledig beheer** voor het NTFS-bestandssysteem beschikken voor de bestandsshare die wordt gebruikt voor het importeren van softwarelicentiegegevens.  

> [!IMPORTANT]  
>  Als softwarelicentiegegevens worden geïmporteerd in de sitedatabase, worden bestaande softwarelicentiegegevens overschreven. Het bestand met softwarelicentiegegevens dat u in de wizard Softwarelicentie importeren gebruikt, moet een volledige lijst met alle benodigde softwarelicentiegegevens bevatten.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Softwarelicentiegegevens importeren in de Asset Intelligence-catalogus  

1.  Kies in de werk ruimte **activa en naleving** de optie **Asset Intelligence**.  

2.  Klik op het tabblad **Start** in de groep **Asset Intelligence** op **software licenties importeren**.   

4.  Geef op de pagina **Importeren** op of u een MVLS-bestand (.xml of .csv) of een algemene licentieverklaring (.csv) wilt importeren. Zie [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) verderop in dit onderwerp voor meer informatie over het maken van een bestand met een algemene licentieverklaring.  

    > [!WARNING]  
    >  Ga naar het [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx)als u een MVLS-bestand in de CSV-indeling wilt downloaden dat u kunt importeren in de Asset Intelligence-catalogus. U krijgt alleen toegang tot deze gegevens als u over een geregistreerd account op de website beschikt. Neem contact op met uw Microsoft-accountmedewerker voor informatie over het ontvangen van een MVLS-bestand in de XML-indeling.  

5.  Voer het UNC-pad naar het bestand met de licentie verklaring in of kies **Bladeren** om een gedeelde netwerkmap en een bestand te selecteren.  

    > [!NOTE]  
    >  De gedeelde map moet correct zijn beveiligd om onbevoegde toegang tot het bestand met licentiegegevens te voorkomen. Daarnaast moet aan het computeraccount van de computer waarop de wizard wordt uitgevoerd de machtiging Volledig beheer zijn toegewezen voor de share met het licentie-importbestand.  

6. Voltooi de wizard.  

###  <a name="create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 Een algemene licentieverklaring kan ook in de Asset Intelligence-catalogus worden geïmporteerd via een handmatig gemaakt licentie-importbestand in een door komma’s gescheiden bestandsindeling (.csv).  

> [!NOTE]  
>  Hoewel alleen de velden **Name**, **Publisher**, **Version**en **EffectiveQuantity** gegevens moeten bevatten, moeten alle velden worden ingevoerd op de eerste rij van het licentie-importbestand. Alle datumvelden moeten de volgende notatie hebben: Dag-Maand-Jaar, bijvoorbeeld 04-08-2008.  

In Asset Intelligence worden de door u opgegeven producten in de algemene licentieverklaring vergeleken op basis van de productnaam en versie van het product, maar niet op basis van de naam van de uitgever. U moet in de algemene licentieverklaring een productnaam gebruiken die exact overeenkomt met de productnaam die is opgeslagen in de sitedatabase. Asset Intelligence neemt het **EffectiveQuantity** nummer op dat is opgegeven in de algemene licentie verklaring en vergelijkt het nummer met het aantal geïnstalleerde producten dat in Configuration Manager-inventaris is gevonden.  

> [!TIP]  
>  Als u een volledige lijst wilt krijgen met de product namen die zijn opgeslagen in de Configuration Manager-site database, kunt u de volgende query uitvoeren op de site database: Selecteer Productname0 SELECT in v_GS_INSTALLED_SOFTWARE.  

 U kunt exacte versies voor een product of een deel van de versie opgeven, bijvoorbeeld alleen de primaire versie. In de volgende voorbeelden worden de resulterende versieovereenkomsten voor de versie-invoer van een algemene licentieverklaring voor een specifiek product gegeven.  

|Invoer algemene licentieverklaring|Overeenkomende sitedatabase-items|  
|-------------------------------------|------------------------------------|  
|Naam: "MySoftware", ProductVersion0: "2"|Productname0 Select: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> Productname0 Select: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> Productname0 Select: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> Productname0 Select: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> Productname0 Select: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> Productname0 Select: "MySoftware", ProductVersion0: "2.10.1234"|  
|Naam: "MySoftware", versie "2,05"|Productname0 Select: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> Productname0 Select: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> Productname0 Select: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|Naam: "Mysoftware", versie "2"<br /><br /> Naam: "Mysoftware", versie "2,05"|Fout tijdens het importeren. Het importeren mislukt wanneer meerdere items overeenkomen met deze productversie.|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Een importbestand voor een algemene licentieverklaring maken met Microsoft Excel  

1.  Open Microsoft Excel en maak een nieuw werkblad.  

2.  Voer op de eerste rij van het nieuwe werkblad alle veldnamen voor softwarelicentiegegevens in.  

3.  Voer op de tweede en volgende rijen van het nieuwe werkblad de vereiste softwarelicentiegegevens in. Zorg ervoor dat in elk geval alle vereiste velden voor softwarelicentiegegevens op de volgende rijen zijn ingevoerd voor elke softwarelicentie die moet worden geïmporteerd. De naam van de softwaretitel die in het werkblad wordt ingevoerd, moet gelijk zijn aan de softwaretitel die in Resource Explorer voor een client wordt weergegeven na het uitvoeren van een hardware-inventarisatie.  

4.  Sla het bestand op in de CSV-indeling.  

5.  Kopieer het CSV-bestand naar de bestandsshare die wordt gebruikt voor het importeren van softwarelicentiegegevens in de Asset Intelligence-catalogus.  

6.  Gebruik in de Configuration Manager-console de wizard software licentie importeren om het zojuist gemaakte CSV-bestand te importeren.  

7.  Voer het Asset Intelligence **License 15a-third party software-afstemmings rapport** uit om te controleren of de licentie gegevens zijn geïmporteerd in de Asset Intelligence catalogus.  

> [!NOTE]  
>  Voor een voor beeld van een algemeen software licentie bestand dat u voor test doeleinden kunt gebruiken, raadpleegt u [voor beeld Asset Intelligence algemeen licentie-import bestand](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Voorbeeldtabel voor beschrijving van softwarelicenties  
 Wanneer u een importbestand voor een algemene licentieverklaring maakt, kunt u de gegevens in de volgende tabel gebruiken om softwarelicenties te beschrijven die moeten worden geïmporteerd in de Asset Intelligence-catalogus.  

|Kolomnaam|Gegevenstype|Vereist|Voorbeeld|  
|-----------------|---------------|--------------|-------------|  
|Naam|Maximaal 255 tekens|Ja|Softwaretitel|  
|Uitgever|Maximaal 255 tekens|Ja|Software-uitgever|  
|Versie|Maximaal 255 tekens|Ja|Versie softwaretitel|  
|Taal|Maximaal 255 tekens|Ja|Taal softwaretitel|  
|EffectiveQuantity|Geheel getal|Ja|Aantal aangeschafte licenties|  
|PONumber|Maximaal 255 tekens|Nee|Inkoopordergegevens|  
|ResellerName|Maximaal 255 tekens|Nee|Informatie van verkoper|  
|DateOfPurchase|Datumwaarde in de volgende notatie: DD-MM-JJJJ|Nee|Datum van aanschaf van licentie|  
|SupportPurchased|Waarde in bits|Nee|0 of 1: 0 voor Ja of 1 voor Nee invoeren|  
|SupportExpirationDate|Datumwaarde in de volgende notatie: DD-MM-JJJJ|Nee|Einddatum van gekochte ondersteuning|  
|Opmerkingen|Maximaal 255 tekens|Nee|Optionele opmerkingen|  

###  <a name="configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 De volgende onderhoudstaken zijn beschikbaar voor Asset Intelligence:  

-   **Titel van toepassing controleren met inventaris informatie**: controleert of de software titel die in de software-inventaris wordt gerapporteerd, wordt afgestemd op de software titel in de Asset Intelligence catalogus. Deze taak is standaard ingeschakeld en wordt gepland om na 12:00 uur te worden uitgevoerd op zaterdag en vóór 5:00 uur Deze onderhouds taak is alleen beschikbaar op de site op het hoogste niveau in uw Configuration Manager-hiërarchie.  

-   **Geïnstalleerde software gegevens samenvatten**: bevat de informatie die wordt weer gegeven in de werk ruimte **activa en naleving** , in het knoop punt **geïnventariseerde software** onder het knoop punt **Asset Intelligence** . Wanneer de taak wordt uitgevoerd, wordt door Configuration Manager een aantal verzameld voor alle geïnventariseerde software titels op de primaire site. Standaard is deze taak ingeschakeld en wordt deze elke dag na 12:00 uur uitgevoerd. en vóór 5:00 uur Deze onderhouds taak is alleen beschikbaar op primaire sites.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Asset Intelligence-onderhoudstaken configureren  

1.  Klik in de Configuration Manager-console op **beheer**  >  **site configuratie**  >  **sites**.  

3.  Selecteer de site waarop de Asset Intelligence-onderhoudstaak moet worden geconfigureerd.  

4.  Klik op het tabblad **Start** in de groep **instellingen** op **site onderhoud**. Selecteer een taak en kies **bewerken** om de instellingen te wijzigen. 

    U wordt aangeraden de tijds periode in te stellen op de daluren van de site. De periode is het tijdsinterval waarin de taak kan worden uitgevoerd. De periode wordt gedefinieerd op basis van de opgegeven waarden bij **Starten na** en **Laatste starttijd** in het dialoogvenster **Taakeigenschappen** .  

    U kunt de taak meteen starten door de huidige dag te selecteren en bij **Starten na** een tijd enkele minuten na de huidige tijd in te stellen.  

7.  Kies **OK** om uw instellingen op te slaan. De taak wordt nu uitgevoerd volgens schema.  

    > [!NOTE]  
    >  Als een taak niet kan worden uitgevoerd bij de eerste poging, probeert Configuration Manager de taak opnieuw uit te voeren totdat de taak is uitgevoerd of totdat de periode is verstreken waarin de taak kan worden uitgevoerd.  

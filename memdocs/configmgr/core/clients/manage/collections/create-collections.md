---
title: Verzamelingen maken
titleSuffix: Configuration Manager
description: Verzamelingen maken in Configuration Manager om groepen gebruikers en apparaten gemakkelijker te beheren.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7eccc3bf6b7ded9db93f5af78d55f090e9704cbc
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438611"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Verzamelingen maken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Verzamelingen zijn groepen van gebruikers of apparaten. Verzamelingen gebruiken voor taken zoals het beheren van toepassingen, het implementeren van nalevings instellingen of het installeren van software-updates. U kunt verzamelingen ook gebruiken om groepen clientinstellingen te beheren of te gebruiken met op rollen gebaseerd beheer om de resources op te geven waartoe een gebruiker met beheerdersrechten toegang heeft. Configuration Manager bevat verschillende ingebouwde verzamelingen. Zie [Inleiding tot verzamelingen](introduction-to-collections.md)voor meer informatie.  

> [!NOTE]  
> Een verzameling kan gebruikers of apparaten bevatten, maar niet beide.  


De informatie in dit artikel kan u helpen bij het maken van verzamelingen in Configuration Manager. U kunt ook verzamelingen importeren die zijn gemaakt op de huidige Configuration Manager site of op een andere. Zie [verzamelingen beheren](manage-collections.md)voor meer informatie over het exporteren en importeren van verzamelingen.  


## <a name="collection-rules"></a>Verzamelings regels

Er zijn verschillende soorten regels die u kunt gebruiken om de leden van een verzameling in Configuration Manager te configureren.  


### <a name="direct-rule"></a>Directe regel

Gebruik directe regels om de gebruikers of computers te kiezen die u wilt toevoegen aan een verzameling. Het lidmaatschap wordt alleen gewijzigd als u een resource verwijdert uit Configuration Manager. Voordat u de resources aan een directe regel verzameling kunt toevoegen, moet Configuration Manager deze hebben gedetecteerd of moeten ze zijn geïmporteerd. Directe regel verzamelingen hebben meer administratieve overhead dan query regel verzamelingen, omdat hiervoor hand matige wijzigingen zijn vereist.


### <a name="query-rule"></a>Queryregel

Het lidmaatschap van een verzameling dynamisch bijwerken op basis van een query die Configuration Manager volgens een planning wordt uitgevoerd. U kunt bijvoorbeeld een verzameling gebruikers maken die lid zijn van de organisatie-eenheid Human Resources in Active Directory Domain Services. Deze verzameling wordt automatisch bijgewerkt wanneer nieuwe gebruikers worden toegevoegd aan of verwijderd uit de organisatie-eenheid Human resources.

Zie [query's maken](../../../servers/manage/create-queries.md)voor een voor beeld van query's die u kunt gebruiken om verzamelingen te bouwen.


### <a name="device-category-rule"></a>Regel voor apparaatcategorie

U kunt het beheer van uw apparaten eenvoudiger maken door apparaatcategorieën te koppelen aan de verzamelingen van apparaten. 

Zie [apparaten automatisch categoriseren in verzamelingen](automatically-categorize-devices-into-collections.md)voor meer informatie.<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Regel voor opnemen van verzameling

Neem de leden van een andere verzameling op in een Configuration Manager verzameling. Als de opgenomen verzameling wordt gewijzigd, wordt in Configuration Manager het lidmaatschap van de huidige verzameling bijgewerkt volgens een schema.

U kunt meerdere regels voor het opnemen van verzamelingen toevoegen aan een verzameling.


### <a name="exclude-collection-rule"></a>Regel voor uitsluiten van verzameling

Met de uitsluiting van verzamelings regels kunt u de leden van een verzameling uitsluiten van een andere Configuration Manager verzameling. Als de uitgesloten verzameling wordt gewijzigd, wordt in Configuration Manager het lidmaatschap van de huidige verzameling bijgewerkt volgens een schema.

U kunt meerdere regels voor het uitsluiten van een verzameling toevoegen aan een verzameling. Als een verzameling zowel de regels include Collection als exclude Collection bevat en er een conflict optreedt, heeft de regel voor het uitsluiten van een verzameling prioriteit.

#### <a name="example"></a>Voorbeeld
U maakt een verzameling met één verzamelings regel voor opnemen en één regel voor het uitsluiten van een verzameling. De regel voor het opnemen van een verzameling is bedoeld voor een verzameling Dell-desktopcomputers. De uitsluitings verzameling is een verzameling computers met minder dan 4 GB RAM-geheugen. De nieuwe verzameling bevat Dell-Desk tops met ten minste 4 GB RAM-geheugen.



## <a name="create-a-collection"></a><a name="bkmk_create"></a>Een verzameling maken  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** .  

    - Als u een *apparaat verzameling*wilt maken, selecteert u het knoop punt **apparaat Collections** . Selecteer vervolgens op het tabblad **Start** van het lint in de groep **maken** de optie **apparaat-verzameling maken**.  

    - Als u een *gebruikers verzameling*wilt maken, selecteert u het knoop punt **gebruikers verzamelingen** . Selecteer vervolgens op het tabblad **Start** van het lint in de groep **maken** de optie **gebruikers verzameling maken**.  

2. Geef op de pagina **Algemeen** van de wizard een **naam** en een **Opmerking**op. Selecteer in de sectie **verzameling beperken** de optie **Bladeren**en selecteer vervolgens een beperkende verzameling. De verzameling die u maakt, bevat alleen leden uit de beperkende verzameling.  

4. Selecteer op de pagina **lidmaatschaps regels** in de lijst **regel toevoegen** het type lidmaatschaps regel dat u wilt gebruiken voor de verzameling. U kunt meerdere regels voor elke verzameling configureren. De configuratie voor elke regel varieert. Zie de volgende secties in dit artikel voor meer informatie over het configureren van elke regel:  
    - [Directe regel](#bkmk-direct)
    - [Queryregel](#bkmk-query)
    - [Regel voor apparaatcategorie](#bkmk-category)
    - [Regel voor opnemen van verzameling](#bkmk-include)
    - [Regel voor uitsluiten van verzameling](#bkmk-exclude)

5. Controleer ook de volgende instellingen op de pagina **lidmaatschaps regels** .

    - **Incrementele updates gebruiken voor deze verzameling**: Selecteer deze optie om periodiek alleen nieuwe of gewijzigde resources van de vorige verzamelings evaluatie te scannen en bij te werken. Dit proces is onafhankelijk van een volledige verzamelings evaluatie. Standaard worden incrementele updates met een interval van vijf minuten uitgevoerd.  

        > [!IMPORTANT]  
        >  Verzamelingen met query regels die de volgende klassen gebruiken, ondersteunen geen incrementele updates:  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (alleen voor verzamelingen van gebruikers)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (alleen voor verzamelingen van gebruikers)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **Een volledige update plannen voor deze verzameling**: een regel matige volledige evaluatie van het lidmaatschap van de verzameling plannen.  

        Vanaf versie 1810 kunnen deze wijzigingen in het verzamelings evaluatie gedrag de prestaties van de site verbeteren:<!--3607726-->  

        - Wanneer u eerder een planning voor een op query's gebaseerde verzameling hebt geconfigureerd, zal de site de query toch gaan evalueren, ongeacht of u de instelling voor het verzamelen **van een volledige update voor deze verzameling**hebt ingeschakeld. Als u het schema volledig wilt uitschakelen, moet u het schema wijzigen in **geen**.

            De site wist nu het schema wanneer u deze instelling uitschakelt. Als u een planning voor het verzamelen van de verzameling wilt opgeven, schakelt u de optie voor het **plannen van een volledige update voor deze verzameling**in.  

            Wanneer u uw site bijwerkt voor een bestaande verzameling waarvoor u een planning hebt opgegeven, kan de site de optie voor het **plannen van een volledige update voor deze verzameling**. Hoewel deze configuratie mogelijk niet uw bedoeling is, was het het werkelijke gedrag van het schema voordat u de site hebt bijgewerkt. Schakel deze optie uit om de site te stoppen met het evalueren van een verzameling volgens een planning.  

        - U kunt de evaluatie van ingebouwde verzamelingen, zoals **alle systemen**, niet uitschakelen, maar de planning kan nu worden geconfigureerd. Dit gedrag stelt u in staat om deze actie aan te passen op een moment dat voldoet aan uw vereisten. 

            > [!TIP]  
            > In ingebouwde verzamelingen wijzigt u alleen de **tijd** van het aangepaste schema. Wijzig het **terugkeer patroon**niet. Toekomstige herhalingen kunnen een specifiek terugkeer patroon afdwingen.  

6. Voltooi de wizard om de nieuwe verzameling te maken. De nieuwe verzameling wordt weergegeven in het knooppunt **Apparaatverzamelingen** van de werkruimte **Activa en naleving** .  

> [!NOTE]  
> U moet de Configuration Manager-console vernieuwen of opnieuw laden om de leden van de verzameling weer te geven. Ze worden pas na de eerste geplande update weer gegeven in de verzameling. U kunt ook hand matig **Update lidmaatschap** selecteren voor de verzameling. Het kan enkele minuten duren voordat een verzamelings update is voltooid.  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a>Een directe regel configureren  

1. Geef op de pagina **zoeken naar resources** van de **wizard regel voor direct lidmaatschap maken**de volgende informatie op.  

    - **Resource klasse**: Selecteer het type resource dat u wilt zoeken en toevoegen aan de verzameling. Bijvoorbeeld:
        - **Systeem bron**: zoeken naar inventaris gegevens die zijn geretourneerd door client computers.
        - **Onbekende computer**: Selecteer waarden die worden geretourneerd door onbekende computers.
        - **Gebruikers bron**: zoeken naar gebruikers gegevens die worden verzameld door Configuration Manager.
        - **Resource van de gebruikers groep**: zoek naar gegevens van de gebruikers groep die zijn verzameld door Configuration Manager.

    - **Kenmerk naam**: Selecteer het kenmerk dat is gekoppeld aan de geselecteerde resource klasse die u wilt zoeken. Bijvoorbeeld:  

        - Als u computers wilt selecteren op basis van hun NetBIOS-naam, selecteert u **systeem bron** in de lijst **resource klasse** en **NetBIOS-naam** in de lijst **kenmerk naam** .  

        - Als u gebruikers wilt selecteren op basis van de naam van de organisatie-eenheid (OE), selecteert u **gebruikers bron** in de lijst **resource klasse** en de naam van de **gebruikers-OE** in de lijst **kenmerk naam** .  

    - **Uitgesloten resources die als verouderd zijn gemarkeerd**: als een client computer is gemarkeerd als verouderd, moet u deze waarde niet opnemen in de zoek resultaten.  

    - **Resources uitsluiten waarop de Configuration Manager-client niet is geïnstalleerd**: deze resources worden niet weer gegeven in de zoek resultaten.  

    - **Waarde**: Voer een waarde in om de geselecteerde kenmerk naam op te zoeken. Gebruik het procent teken (%) als Joker teken. Bijvoorbeeld:  
        - Als u wilt zoeken naar computers met een NetBIOS-naam die begint met 'm ', typt u **M%** in dit veld.  
        - Als u wilt zoeken naar gebruikers in de organisatie-eenheid contoso, voert u **Contoso** in dit veld in.

2. Op de pagina **resources selecteren** selecteert u de resources die u wilt toevoegen aan de verzameling in de lijst **resources** en selecteert u vervolgens **volgende**.  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a>Een query regel configureren  

Geef in het dialoog venster **query regel eigenschappen** de volgende informatie op.  

- **Naam**: Geef een unieke naam op voor de query.  

- **Query-instructie importeren**: Hiermee opent u het dialoog venster **Bladeren in query** . Selecteer een [Configuration Manager query](../../../servers/manage/create-queries.md) die u wilt gebruiken als de query regel voor de verzameling.   

- **Resource klasse**: Selecteer het type resource dat u wilt zoeken en toevoegen aan de verzameling. Selecteer een waarde in **systeem bron** om te zoeken naar inventaris gegevens die zijn geretourneerd door client computers of van **onbekende computers** om te selecteren uit waarden die worden geretourneerd door onbekende computers.  

- **Query-instructie bewerken**: Hiermee opent u het dialoog venster **Eigenschappen van query-instructie** waarin u een query kunt schrijven om te gebruiken als regel voor de verzameling. Zie [Inleiding tot query's](../../../servers/manage/introduction-to-queries.md)voor meer informatie over query's.  

        
        > [!TIP]  
        > On the General tab, selecting the checkbox to **Omit duplicate rows (select distinct)** may result in less rows returned and potentially quicker results. 

### <a name="device-category-rule"></a><a name="bkmk-category"></a>Regel voor apparaatcategorie

De volgende acties zijn beschikbaar in het venster **apparaatcategorieën selecteren** .

- **Maken**: Geef een naam op om een nieuwe categorie te maken.
- **Naam wijzigen**: Wijzig de naam van de geselecteerde categorie.
- **Verwijderen**: Selecteer een of meer categorieën en gebruik deze actie om deze te verwijderen uit de lijst.

Zie [apparaten automatisch categoriseren in verzamelingen](automatically-categorize-devices-into-collections.md)voor meer informatie.<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a>Een regel voor het insluiten van een verzameling configureren  

Selecteer in het dialoog venster **verzamelingen selecteren** de verzamelingen die u wilt toevoegen in de nieuwe verzameling en selecteer vervolgens **OK**.  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a>Een regel voor het uitsluiten van een verzameling configureren  

Selecteer in het dialoog venster **verzamelingen selecteren** de verzamelingen die u wilt uitsluiten van de nieuwe verzameling en selecteer vervolgens **OK**.  



## <a name="import-a-collection"></a><a name="bkmk_import"></a>Een verzameling importeren  

Wanneer u een verzameling exporteert vanuit een-site, Configuration Manager deze opslaat als een Managed Object Format bestand (MOF). Gebruik deze procedure om dat bestand te importeren in de-site database. Als u deze procedure wilt uitvoeren, moet u de machtigingen **maken** voor de klasse Collections.

> [!IMPORTANT]  
> - Zorg ervoor dat het bestand alleen verzamelings gegevens bevat, afkomstig is van een vertrouwde bron en niet is geknoeid met.  
> 
> - Zorg ervoor dat het bestand is geëxporteerd van een site met dezelfde versie van Configuration Manager die u gebruikt.  

Zie [verzamelingen beheren](manage-collections.md)voor meer informatie over het exporteren van verzamelingen.


1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Selecteer de knoop punten **gebruikers verzamelingen** of **apparaat** .  

2. Selecteer op het tabblad **Start** van het lint in de groep **maken** de optie **verzamelingen importeren**.  

3. Selecteer **volgende**op de pagina **Algemeen** van de **wizard verzamelingen importeren**.  

4. Klik op de pagina **MOF-bestands naam** op **Bladeren**. Blader naar het MOF-bestand met de verzamelings gegevens die u wilt importeren.  

5. Voltooi de wizard om de verzameling te importeren. De nieuwe verzameling wordt weergegeven in het knooppunt **Gebruikersverzamelingen** of **Apparaatverzamelingen** van de werkruimte **Activa en naleving** . Vernieuw de Configuration Manager-console of laad deze opnieuw om de verzamelings leden voor de zojuist geïmporteerde verzameling te zien.  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a>Resultaten van verzamelings lidmaatschap synchroniseren met Azure Active Directory groepen

<!--3607475-->
> [!Tip]  
> Deze functie werd voor het eerst in versie 1906 geïntroduceerd als een [voorlopige functie](../../../servers/manage/pre-release-features.md). Vanaf versie 2002 is het niet langer een functie van de voorlopige versie.  

U kunt de synchronisatie van verzamelings lidmaatschappen inschakelen voor een groep Azure Active Directory (Azure AD). Met deze synchronisatie kunt u uw bestaande on-premises groeperings regels in de Cloud gebruiken door Azure AD-groepslid maatschappen te maken op basis van de resultaten van het verzamelings lidmaatschap. U kunt apparaat verzamelingen synchroniseren. Alleen apparaten met een Azure Active Directory record worden weer gegeven in de Azure AD-groep. Zowel hybride Azure AD join als aan Azure Active Director gekoppelde apparaten worden ondersteund.

De Azure AD-synchronisatie gebeurt elke vijf minuten. Het is een eenrichtings proces van Configuration Manager naar Azure AD. Wijzigingen die zijn aangebracht in azure AD, worden niet weer gegeven in Configuration Manager verzamelingen, maar worden niet overschreven door Configuration Manager. Als de verzameling Configuration Manager bijvoorbeeld twee apparaten heeft en de Azure AD-groep drie verschillende apparaten heeft, heeft de Azure AD-groep na het synchroniseren vijf apparaten.

### <a name="prerequisites"></a>Vereisten

- Integratie met Azure AD voor [Cloud beheer](../../../servers/deploy/configure/azure-services-wizard.md)
- [Gebruikers detectie Azure Active Directory](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- Een HTTPS [-of Enhanced HTTP-](../../../plan-design/hierarchy/enhanced-http.md) beheer punt
- Toegang tot de verzameling **alle systemen**

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>Een groep maken en de eigenaar instellen in azure AD

1. Ga naar [https://portal.azure.com](https://portal.azure.com).
1. Navigeer naar **Azure Active Directory**  >  **groepen**  >  **alle groepen**.
1. Klik op **nieuwe groep** en typ een **groeps naam** en optioneel een beschrijving voor de **groep**.
1. Zorg ervoor dat het **lidmaatschaps type** is **toegewezen**.
1. Selecteer **eigen aren**en voeg vervolgens de identiteit toe waarmee de synchronisatie relatie wordt gemaakt in Configuration Manager.
1. Klik op **maken** om de Azure AD-groep te maken.

### <a name="enable-collection-synchronization-for-the-azure-service"></a>Verzamelings synchronisatie voor de Azure-service inschakelen

1. Ga in de Configuration Manager-console naar **beheer**  >  **overzicht**  >  **Cloud Services**  >  **Azure-Services**.
1. Klik met de rechter muisknop op de Azure AD-Tenant waar u de groep hebt gemaakt en selecteer **Eigenschappen**.
1. Schakel op het tabblad Synchronisatie van de **verzameling** het selectie vakje in voor de **synchronisatie van Azure Directory-groepen inschakelen**.
1. Klik op **OK** om de instelling op te slaan.

### <a name="enable-the-collection-to-synchronize"></a>De verzameling voor synchronisatie inschakelen

1. Ga in de Configuration Manager-console naar **activa en naleving**  >  **overzicht**  >  **apparaat verzamelingen**.
1. Klik met de rechter muisknop op de verzameling die u wilt synchroniseren en klik vervolgens op **Eigenschappen**. 
1. Klik op het tabblad **Cloud Sync** op **toevoegen**.
1. Selecteer in de vervolg keuzelijst de **Tenant** waar u uw Azure AD-groep hebt gemaakt.
1. Typ uw zoek criteria in het veld **naam begint met** en klik vervolgens op **zoeken**.
  - Als u wordt gevraagd om u aan te melden, gebruikt u de identiteit die u hebt opgegeven als de eigenaar van de Azure AD-groep.
1. Selecteer de doel groep en klik vervolgens op **OK** om de groep toe te voegen en nogmaals op **OK** om de eigenschappen van de verzameling af te sluiten.
1. U moet ongeveer 5 tot 7 minuten wachten voordat u de groepslid maatschappen in de Azure Portal kunt controleren.
   - Als u een volledige synchronisatie wilt starten, klikt u met de rechter muisknop op de verzameling en selecteert u **lidmaatschap synchroniseren**.


### <a name="verify-the-azure-ad-group-membership"></a>Het lidmaatschap van de Azure AD-groep controleren

1. Ga naar [https://portal.azure.com](https://portal.azure.com).
1. Navigeer naar **Azure Active Directory**  >  **groepen**  >  **alle groepen**.
1. Zoek de groep die u hebt gemaakt en selecteer **leden**. 
1. Controleer of de leden overeenkomen met die in de verzameling Configuration Manager.
   - Alleen apparaten met Azure AD-identiteit worden weer gegeven in de groep.


![Verzamelingen synchroniseren met Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Power shell gebruiken

U kunt Power shell gebruiken om verzamelingen te maken en te importeren. Zie voor meer informatie:

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>Volgende stappen

[Verzamelingen beheren](manage-collections.md)

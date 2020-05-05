---
title: Beheer op basis van rollen configureren
titleSuffix: Configuration Manager
ms.date: 11/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 14258c3e7e2cfe5423b97064a26fdf5616d6b0a4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078614"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Op rollen gebaseerd beheer configureren voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In Configuration Manager combineert beheer op basis van rollen beveiligings rollen, beveiligingsbereiken en toegewezen verzamelingen om het beheer bereik te definiëren voor elke gebruiker met beheerders rechten. Een beheer bereik bevat de objecten die een gebruiker met beheerders rechten kan weer geven in de Configuration Manager-console en de taken die betrekking hebben op deze objecten die de gebruiker met Administrator machtigingen mag uitvoeren. Configuraties voor beheer op basis van rollen worden toegepast op elke site in een hiërarchie.  

 Zie de [basis principes van beheer op basis van rollen](../../../understand/fundamentals-of-role-based-administration.md)als u nog niet bekend bent met concepten voor beheer op basis van rollen.  

 De informatie in de volgende procedures kan u helpen bij het maken en configureren van beheer op basis van rollen en gerelateerde beveiligings instellingen:  

- [Aangepaste beveiligings rollen maken](#BKMK_CreateSecRole)  
- [Beveiligingsrollen configureren](#BKMK_ConfigSecRole)  
- [Beveiligingsbereiken voor een object configureren](#BKMK_ConfigSecScope)  
- [Verzamelingen voor het beheren van beveiliging configureren](#BKMK_ConfigColl)  
- [Een nieuwe gebruiker met beheerdersrechten maken](#BKMK_Create_AdminUser)  
- [Het beheerbereik van een gebruiker met beheerdersrechten wijzigen](#BKMK_ModAdminUser)  

## <a name="create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Aangepaste beveiligingsrollen maken

 Configuration Manager biedt verschillende ingebouwde beveiligings rollen. Indien u bijkomende beveiligingsrollen nodig hebt, kunt u een aangepaste beveiligingsrol maken door een kopie te maken van een bestaande beveiligingsrol en dan de kopie te wijzigen. U kunt een aangepaste beveiligingsrol maken om gebruikers met beheerders rechten de extra beveiligings machtigingen te verlenen die ze nodig hebben en die niet zijn opgenomen in een momenteel toegewezen beveiligingsrol. Door een aangepaste beveiligingsrol te gebruiken, verleent u hen enkel de machtigingen die ze nodig hebben, en vermijdt u een beveiligingsrol toe te wijzen die meer machtigingen verleent dan ze nodig hebben.  

 Gebruik de volgende procedure om een nieuwe beveiligingsrol te maken door gebruik te maken van een bestaande beveiligingsrol als sjabloon.  

### <a name="to-create-custom-security-roles"></a>Aangepaste beveiligingsrollen maken

1. Ga in de Configuration Manager-console naar **beheer**.  

2. Vouw **beveiliging**uit in de werk ruimte **beheer** en kies **beveiligings rollen**.  

   Gebruik één van de volgende processen om de nieuwe beveiligingsrol te maken:  

    - Voer de volgende acties uit om een aangepaste beveiligingsrol te maken:  

      1. Selecteer een bestaande beveiligingsrol om die te gebruiken voor de nieuwe beveiligingsrol.
      2. Klik op het tabblad **Start** in de groep **beveiligingsrol** op **kopiëren**. Met deze actie maakt u een kopie van de bron beveiligingsrol.  
      3. Geef in de wizard Beveiligingsrol kopiëren een **Naam** op voor de nieuwe aangepaste beveiligingsrol.  
      4. Vouw in **Toewijzingen beveiligingsbewerking**het knooppunt **Beveiligingsbewerkingen** uit om de beschikbare acties weer te geven.  
      5. Als u de instelling voor een beveiligings bewerking wilt wijzigen, kiest u de pijl omlaag in de kolom **waarde** en kiest u **Ja** of **Nee**.

            > [!CAUTION]  
            > Wanneer u een aangepaste beveiligingsrol configureert, moet u ervoor zorgen dat u geen machtigingen verleent die niet vereist zijn door gebruikers met beheerders rechten die zijn gekoppeld aan de nieuwe beveiligingsrol. De **wijzigings** waarde voor de beveiligings bewerking **beveiligings rollen** geeft bijvoorbeeld gebruikers met beheerders rechten machtigingen voor het bewerken van een toegankelijke beveiligingsrol, zelfs als ze niet aan die beveiligingsrol zijn gekoppeld.  

      6. Nadat u de machtigingen hebt geconfigureerd, kiest u **OK** om de nieuwe beveiligingsrol op te slaan.  

    - Voer de volgende acties uit om een beveiligingsrol te importeren die is geëxporteerd uit een andere Configuration Manager-hiërarchie:  

        1. Kies op het tabblad **Start** in de groep **maken** de optie **beveiligingsrol importeren**.  
        2. Geef het. XML-bestand op dat de beveiligingsrol configuratie bevat die u wilt importeren. Kies **openen** om de procedure te volt ooien en de beveiligingsrol op te slaan.  

            > [!NOTE]  
            > Nadat u een beveiligingsrol importeert, kunt u de eigenschappen van de beveiligingsrol bewerken om de objectmachtigingen te wijzigen die zijn gekoppeld aan de beveiligingsrol.  

## <a name="configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a>Beveiligings rollen configureren

 De groepen van beveiligingsmachtiging die gedefinieerd zijn voor een beveiligingsmachtigingen worden beveiligingsbewerkingstoewijzingen genoemd. Beveiligingsbewerkingstoewijzingen vertegenwoordigen een combinatie van objecttypes en -acties die beschikbaar zijn voor elk type object. U kunt wijzigen welke beveiligings bewerkingen beschikbaar zijn voor een aangepaste beveiligingsrol, maar u kunt de ingebouwde beveiligings rollen die Configuration Manager biedt, niet wijzigen.  

 Gebruik de volgende procedure om de beveiligingsbewerkingen te wijzigen voor een beveiligingsrol.  

### <a name="to-modify-security-roles"></a>Beveiligingsrollen wijzigen

1. Klik in de Configuration Manager-console op **beheer**.  
2. Vouw **beveiliging**uit in de werk ruimte **beheer** en kies **beveiligings rollen**.  
3. Selecteer de aangepaste beveiligingsrol die u wilt wijzigen.  
4. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  
5. Kies het tabblad **machtigingen** .  
6. Vouw in **Toewijzingen beveiligingsbewerking**het knooppunt **Beveiligingsbewerkingen** uit om de beschikbare acties weer te geven.  
7. Als u de instelling voor een beveiligings bewerking wilt wijzigen, kiest u de pijl omlaag in de kolom **waarde** en kiest u **Ja** of **Nee**.  

    > [!CAUTION]  
    > Wanneer u een aangepaste beveiligingsrol configureert, moet u ervoor zorgen dat u geen machtigingen verleent die niet vereist zijn door gebruikers met beheerders rechten die zijn gekoppeld aan de nieuwe beveiligingsrol. De **wijzigings** waarde voor de beveiligings bewerking **beveiligings rollen** geeft bijvoorbeeld gebruikers met beheerders rechten machtigingen voor het bewerken van een toegankelijke beveiligingsrol, zelfs als ze niet aan die beveiligingsrol zijn gekoppeld.  

8. Wanneer u klaar bent met het configureren van de beveiligings bewerkings toewijzingen, kiest u **OK** om de nieuwe beveiligingsrol op te slaan.  

##  <a name="configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a>Beveiligingsbereiken voor een object configureren
 U beheert de koppeling van een beveiligings bereik voor een object uit het-object, niet uit het beveiligings bereik. De enige directe configuraties die beveiligingsbereiken ondersteunen zijn wijzigingen aan zijn naam en beschrijving. Om de naam en beschrijving van een beveiligingsbereik te wijzigen wanneer u de eigenschappen van het beveiligingsbereik ziet, moet u de **Wijzig** -machtiging hebben voor het met **Beveiligingsbereiken** te beveiligen object.  

 Wanneer u een nieuw object in Configuration Manager maakt, wordt het gekoppeld aan elk beveiligings bereik dat is gekoppeld aan de beveiligings rollen van het account dat wordt gebruikt om het object te maken. Dit gedrag treedt op wanneer deze beveiligings rollen de machtiging **maken** hebben of een **beveiligings bereik instellen** . U kunt de beveiligingsbereiken voor het object wijzigen nadat u het hebt gemaakt.  

 U hebt bijvoorbeeld een beveiligingsrol toegewezen waarmee u toestemming krijgt om een nieuwe grens groep te maken. Wanneer u een nieuwe grens groep maakt, hebt u geen optie waaraan u specifieke beveiligingsbereiken kunt toewijzen. In plaats daarvan worden de beveiligingsbereiken die beschikbaar zijn van de beveiligings rollen die u aan het koppelen bent, automatisch toegewezen aan de nieuwe grens groep. Nadat u de nieuwe grens groep hebt opgeslagen, kunt u de beveiligingsbereiken die zijn gekoppeld aan de nieuwe grens groep bewerken.  

 Gebruik de volgende procedure voor het configureren van de beveiligingsbereiken die aan een object zijn toegewezen.  

### <a name="to-configure-security-scopes-for-an-object"></a><a name="bkmk_config-sec-scope"></a>Beveiligingsbereiken voor een object configureren  

1. Selecteer in de Configuration Manager-console een object dat ondersteuning biedt voor het toewijzen aan een beveiligings bereik.  
2. Kies op het tabblad **Start** in de groep **classificeren** de optie **beveiligingsbereiken instellen**.
3. Selecteer of wis de beveiligingsbereiken waarmee dit object is gekoppeld in het dialoogvenster **Beveiligingsbereiken instellen** . Elk object dat beveiligingsbereiken ondersteunt, moet toegewezen zijn aan minstens één beveiligingsbereik.  
4. Kies **OK** om de toegewezen beveiligingsbereiken op te slaan.  

    > [!NOTE]  
    > Wanneer u een nieuw object maakt, moet u het object toewijzen aan verschillende beveiligingsbereiken. Als u het aantal beveiligingsbereiken wilt wijzigen dat aan het object is gekoppeld, moet u deze toewijzing wijzigen nadat het object is gemaakt.

### <a name="to-configure-security-scopes-for-a-folder-starting-in-version-1906"></a><a name="bkmk_config-folder"></a>Beveiligingsbereiken configureren voor een map (vanaf versie 1906)
<!--3600867-->

1. Selecteer een map in de Configuration Manager-console.  
1. Kies op het tabblad **map** in het lint de optie **beveiligingsbereiken instellen**.
   - U kunt ook met de rechter muisknop op **de map klikken** > en**beveiligingsbereiken instellen**selecteren.
1. Schakel in het dialoog venster **Beveiligingsbereiken instellen** het selectie vakje beveiligingsbereiken voor de map in of uit. Elke map moet aan ten minste één beveiligings bereik worden toegewezen. Alle mappen worden toegewezen aan het **standaard** beveiligings bereik totdat u het wijzigt.
1. Kies **OK** om de toegewezen beveiligingsbereiken op te slaan.  

    > [!IMPORTANT]  
    > - Aan bestaande beveiligings rollen worden automatisch **mapmachtigingen opgehaald wanneer** u Configuration Manager versie 1906. U moet machtigingen voor **mapmachtigingen** toevoegen voor nieuwe beveiligings rollen en controleren of bestaande rollen de juiste machtigingen hebben voor uw omgeving.
    > 
    > - Een item kan worden doorzocht in een map buiten het beveiligings bereik van een gebruiker als die gebruiker een beveiligings bereik deelt met de persoon die het object heeft gemaakt. <!--5602690-->

## <a name="configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a>Verzamelingen configureren voor het beheren van beveiliging

 Er zijn geen procedures voor het configureren van verzamelingen voor rolgebaseerd beheer. Verzamelingen hebben geen beheer configuratie op basis van rollen. In plaats daarvan wijst u verzamelingen toe aan een gebruiker met beheerders rechten wanneer u de gebruiker met beheerders rechten configureert. De beveiligings bewerkingen voor de verzameling die zijn ingeschakeld in de door de gebruiker toegewezen beveiligings rollen bepalen de machtigingen die een gebruiker met beheerders rechten heeft voor verzamelingen en verzamelings bronnen (verzamelings leden).  

 Wanneer een gebruiker met beheerdersrechten machtigingen heeft voor een verzameling, heeft hij ook machtigingen voor verzamelingen die beperkt zijn tot deze verzameling. Uw organisatie gebruikt bijvoorbeeld een verzameling met de naam alle Bureau bladen. Er is ook een verzameling met de naam alle Noord-Amerika Bureau bladen die beperkt zijn tot de verzameling alle Bureau bladen. Indien een gebruiker met beheerdersrechten machtigingen heeft tot Alle bureaubladen, hebben ze ook dezelfde machtigingen tot de verzameling Alle bureaubladen van Noord-Amerika.

 Daarnaast kan een gebruiker met beheerders rechten de machtiging **verwijderen** of **wijzigen** niet gebruiken voor een verzameling die direct aan hen is toegewezen. Maar ze kunnen deze machtigingen gebruiken op de verzamelingen die beperkt zijn tot deze verzameling. In het vorige voor beeld kan de gebruiker met beheerders rechten de verzameling alle Noord-Amerika Bureau bladen verwijderen of wijzigen, maar de verzameling alle Bureau bladen kan niet worden verwijderd of gewijzigd.  

## <a name="create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a>Een nieuwe gebruiker met beheerders rechten maken

 Als u individuen of leden van een beveiligings groep toegang wilt verlenen tot het beheren van Configuration Manager, maakt u een gebruiker met beheerders rechten in Configuration Manager en geeft u het Windows-account van de gebruiker of gebruikers groep op. Aan elke gebruiker met beheerders rechten in Configuration Manager moet ten minste één beveiligingsrol en één beveiligings bereik worden toegewezen. U kunt tevens verzamelingen toewijzen om het beheerbereik van de gebruiker met beheerdersrechten te beperken.  

 Gebruik de volgende procedures om nieuwe gebruikers met beheerdersrechten te maken.  

### <a name="to-create-a-new-administrative-user"></a>Maken van een nieuwe gebruiker met beheerdersrechten  

1. Klik in de Configuration Manager-console op **beheer**.  
2. Vouw **beveiliging**uit in de werk ruimte **beheer** en kies vervolgens **gebruikers met beheerders rechten**.  
3. Klik op het tabblad **Start** in de groep **maken** op **gebruiker of groep toevoegen**.  
4. Kies **Bladeren**en selecteer vervolgens het gebruikers account of de groep die moet worden gebruikt voor deze nieuwe gebruiker met beheerders rechten.  

    > [!NOTE]  
    > Bij beheer via de console kunnen alleen domeingebruikers of beveiligingsgroepen worden gespecificeerd als een gebruiker met beheerdersrechten.

5. Klik voor **gekoppelde beveiligings rollen**op **toevoegen** om een lijst met beschik bare beveiligings rollen te openen, schakel het selectie vakje in voor een of meer beveiligings rollen en klik vervolgens op **OK**.  

6. Kies een van de volgende twee opties om het gedrag van het Beveilig bare object voor de nieuwe gebruiker te definiëren:  

    - **Alle exemplaren van de objecten die verwant zijn aan de toegewezen beveiligings rollen**: met deze optie wordt de gebruiker met beheerders rechten gekoppeld aan het beveiligings bereik **alle** en de verzamelingen **alle systemen** en **alle gebruikers en gebruikers groepen** . De aan de gebruiker toegewezen beveiligingsrollen definiëren de toegang tot objecten. Nieuwe objecten die door deze gebruiker met beheerdersrechten worden gemaakt, worden toegewezen aan het beveiligingsbereik **Standaard** .  

    - **Alleen de exemplaren van objecten die zijn toegewezen aan de gespecificeerde beveiligingsbereiken en verzamelingen**: met deze optie wordt de gebruiker met beheerders rechten standaard gekoppeld aan het beveiligings bereik **standaard** en de verzamelingen **alle systemen** en **alle gebruikers en gebruikers groepen** . De werkelijke beveiligingsbereiken en verzamelingen zijn echter beperkt tot die welke gekoppeld zijn aan het account dat u hebt gebruikt om de nieuwe gebruiker met beheerdersrechten te maken. Deze optie ondersteunt het toevoegen of verwijderen van beveiligingsbereiken en verzamelingen om het beheerbereik van de gebruiker met beheerdersrechten aan te passen.  

    > [!IMPORTANT]  
    > De voor gaande opties koppelen elk toegewezen beveiligings bereik en verzameling aan elke beveiligingsrol die aan de gebruiker met beheerders rechten is toegewezen. U kunt een derde optie gebruiken, **toegewezen beveiligings rollen koppelen aan specifieke beveiligingsbereiken en verzamelingen**, om afzonderlijke beveiligings rollen te koppelen aan specifieke beveiligingsbereiken en verzamelingen. Deze derde optie is beschikbaar nadat u de nieuwe gebruiker met beheerdersrechten maakt, wanneer u de gebruiker met beheerdersrechten wijzigt.  

7. Voer, afhankelijk van uw selectie in stap 6, de volgende handeling uit:  

    - Als u **alle exemplaren van de objecten die zijn gerelateerd aan de toegewezen beveiligings rollen**hebt geselecteerd, kiest u **OK** om deze procedure te volt ooien.  

    - Als u **alleen de instanties van objecten die zijn toegewezen aan de gespecificeerde beveiligingsbereiken en verzamelingen**hebt geselecteerd, kunt u **toevoegen** kiezen om extra verzamelingen en beveiligingsbereiken te selecteren. Of selecteer een of meer objecten in de lijst en kies **verwijderen** om ze te verwijderen. Kies **OK** om deze procedure te volt ooien.  

## <a name="modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a>Het beheer bereik van een gebruiker met beheerders rechten wijzigen

 U kunt het beheerbereik van een gebruiker met beheerdersrechten wijzigen door beveiligingsrollen, beveiligingsbereiken, en verzamelingen die aan de gebruiker gekoppeld zijn, toe te voegen of te verwijderen. Aan elke gebruiker met beheerdersrechten moet minimaal één beveiligingsrol en één beveiligingsbereik zijn gekoppeld. Mogelijk moet u één of meer verzamelingen aan het beheerbereik van de gebruiker toewijzen. De meeste beveiligings rollen communiceren met verzamelingen en functioneren niet goed zonder een toegewezen verzameling.  

 Wanneer u een gebruiker met beheerdersrechten wijzigt, kunt u het gedrag wijzigen voor hoe beveiligbare objecten zijn gekoppeld aan de toegewezen beveiligingsrollen. Dit zijn de drie soorten gedrag die u kunt selecteren:  

- **Alle exemplaren van de objecten die verwant zijn aan de toegewezen beveiligings rollen**: met deze optie wordt de gebruiker met beheerders rechten gekoppeld aan het bereik **alle** en de verzamelingen **alle systemen** en **alle gebruikers en gebruikers groepen** . De aan de gebruiker toegewezen beveiligingsrollen definiëren de toegang tot objecten.  

- **Alleen de exemplaren van objecten die zijn toegewezen aan de gespecificeerde beveiligingsbereiken en verzamelingen: met**deze optie wordt de gebruiker met beheerders rechten gekoppeld aan dezelfde beveiligingsbereiken en verzamelingen die aan het account dat u gebruikt om de gebruiker met beheerders rechten te configureren. Deze optie ondersteunt het toevoegen of verwijderen van beveiligingsrollen en verzamelingen om het beheerbereik van de gebruiker met beheerdersrechten aan te passen.  

- **Toegewezen beveiligings rollen koppelen aan specifieke beveiligingsbereiken en verzamelingen: met**deze optie kunt u specifieke koppelingen maken tussen de afzonderlijke beveiligings rollen en de specifieke beveiligingsbereiken en verzamelingen voor de gebruiker.  

    > [!NOTE]  
    > Deze optie is alleen beschikbaar wanneer u de eigenschappen van een gebruiker met beheerdersrechten wijzigt.  

De huidige configuratie voor het gedrag van het beveiligbare object verandert het proces dat u gebruikt om aanvullende beveiligingsrollen toe te wijzen. Gebruik de volgende procedures die gebaseerd zijn op de verschillende opties voor beveiligbare objecten om u te helpen een gebruiker met beheerdersrechten te beheren.  

Gebruik de volgende procedure om de configuratie voor Beveilig bare objecten voor een gebruiker met beheerders rechten weer te geven en te beheren.  

### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Bekijken en beheren van het gedrag van een beveiligbaar object voor een gebruiker met beheerdersrechten  

1. Klik in de Configuration Manager-console op **beheer**.  
2. Vouw **beveiliging**uit in de werk ruimte **beheer** en kies vervolgens **gebruikers met beheerders rechten**.  
3. Selecteer de gebruiker met beheerdersrechten die u wilt wijzigen.  
4. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  
5. Klik op het tabblad **beveiligingsbereiken** om de huidige configuratie voor Beveilig bare objecten voor deze gebruiker met beheerders rechten weer te geven.  
6. Om het gedrag van een beveiligbaar object te wijzigen, selecteert u een nieuwe optie voor het gedrag van een beveiligbaar object. Nadat u deze configuratie hebt gewijzigd, raadpleegt u de relevante procedure voor meer informatie over het configureren van beveiligingsbereiken en verzamelingen en beveiligings rollen voor deze gebruiker met beheerders rechten.  
7. Kies **OK** om de procedure te volt ooien.  

Gebruik de volgende procedure om een gebruiker met beheerders rechten te wijzigen waarvoor het gedrag van het Beveilig bare object is ingesteld op **alle exemplaren van de objecten die zijn gerelateerd aan de toegewezen beveiligings rollen**.  

### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>Voor optie: alle exemplaren van de objecten die verwant zijn aan de toegewezen beveiligings rollen  

1. Klik in de Configuration Manager-console op **beheer**.  
2. Vouw **beveiliging**uit in de werk ruimte **beheer** en kies vervolgens **gebruikers met beheerders rechten**.  
3. Selecteer de gebruiker met beheerdersrechten die u wilt wijzigen.  
4. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  
5. Kies het tabblad **beveiligingsbereiken** om te bevestigen dat de gebruiker met beheerders rechten geconfigureerd is voor **alle exemplaren van de objecten die zijn gerelateerd aan de toegewezen beveiligings rollen**.  
6. Klik op het tabblad **beveiligings rollen** om de toegewezen beveiligings rollen te wijzigen.  

    - Om aanvullende beveiligings rollen aan deze gebruiker met beheerders rechten toe te wijzen, klikt u op **toevoegen**, schakelt u het selectie vakje in voor elke aanvullende beveiligingsrol die u wilt toewijzen en kiest u vervolgens **OK**.  
    - Als u beveiligings rollen wilt verwijderen, selecteert u een of meer beveiligings rollen in de lijst en kiest u vervolgens **verwijderen**.

7. Als u het gedrag van het Beveilig bare object wilt wijzigen, kiest u het tabblad **beveiligingsbereiken** en kiest u een nieuwe optie voor het gedrag van het Beveilig bare object. Nadat u deze configuratie hebt gewijzigd, raadpleegt u de relevante procedure voor meer informatie over het configureren van beveiligingsbereiken en verzamelingen en beveiligings rollen voor deze gebruiker met beheerders rechten.  

    > [!NOTE]  
    > Wanneer het gedrag van het Beveilig bare object is ingesteld op **alle exemplaren van de objecten die verwant zijn aan de toegewezen beveiligings rollen**, kunt u geen specifieke beveiligingsbereiken en verzamelingen toevoegen of verwijderen.  

8. Kies **OK** om deze procedure te volt ooien.  

Gebruik de volgende procedure om een gebruiker met beheerders rechten te wijzigen waarvoor het gedrag van het Beveilig bare object is ingesteld op **alleen de exemplaren van objecten die zijn toegewezen aan de gespecificeerde beveiligingsbereiken en verzamelingen**.  

### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>Voor optie: alleen de exemplaren van objecten die zijn toegewezen aan de gespecificeerde beveiligingsbereiken en verzamelingen  

1. Klik in de Configuration Manager-console op **beheer**.  
2. Vouw **beveiliging**uit in de werk ruimte **beheer** en kies vervolgens **gebruikers met beheerders rechten**.  
3. Selecteer de gebruiker met beheerdersrechten die u wilt wijzigen.  
4. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  
5. Klik op het tabblad **beveiligingsbereiken** om te bevestigen dat de gebruiker is geconfigureerd voor **alleen de instanties van objecten die zijn toegewezen aan de gespecificeerde beveiligingsbereiken en verzamelingen**.  
6. Klik op het tabblad **beveiligings rollen** om de toegewezen beveiligings rollen te wijzigen.  

    - Om aanvullende beveiligings rollen aan deze gebruiker toe te wijzen, klikt u op **toevoegen**, schakelt u het selectie vakje in voor elke aanvullende beveiligingsrol die u wilt toewijzen en klikt u vervolgens op **OK**.  
    - Als u beveiligings rollen wilt verwijderen, selecteert u een of meer beveiligings rollen in de lijst en kiest u vervolgens **verwijderen**.  
7. Klik op het tabblad **beveiligingsbereiken** om de beveiligingsbereiken en verzamelingen te wijzigen die zijn gekoppeld aan beveiligings rollen.  

    - Om nieuwe beveiligingsbereiken of verzamelingen te koppelen aan alle beveiligings rollen die aan deze gebruiker met beheerders rechten zijn toegewezen, klikt u op **toevoegen** en selecteert u een van de vier opties. Als u **beveiligings bereik** of **verzameling**selecteert, schakelt u het selectie vakje in voor een of meer objecten om die selectie te volt ooien en kiest u vervolgens **OK**.  
    - Als u een beveiligings bereik of verzameling wilt verwijderen, kiest u het object en kiest u vervolgens **verwijderen**.

8. Kies **OK** om deze procedure te volt ooien.  

Gebruik de volgende procedure om een gebruiker met beheerders rechten te wijzigen waarvoor het gedrag van het Beveilig bare object is ingesteld om **toegewezen beveiligings rollen te koppelen aan specifieke beveiligingsbereiken en verzamelingen**.  

### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>Voor optie: toegewezen beveiligings rollen koppelen aan specifieke beveiligingsbereiken en verzamelingen  

1. Klik in de Configuration Manager-console op **beheer**.  
2. Vouw **beveiliging**uit in de werk ruimte **beheer** en kies vervolgens **gebruikers met beheerders rechten**.  
3. Selecteer de gebruiker met beheerdersrechten die u wilt wijzigen.  
4. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  
5. Kies het tabblad **beveiligingsbereiken** om te bevestigen dat de gebruiker met beheerders rechten is geconfigureerd voor het **koppelen van toegewezen beveiligings rollen aan specifieke beveiligingsbereiken en verzamelingen**.  
6. Klik op het tabblad **beveiligings rollen** om de toegewezen beveiligings rollen te wijzigen.  

    - Klik op **toevoegen**om aanvullende beveiligings rollen aan deze gebruiker met beheerders rechten toe te wijzen. Selecteer in het dialoog venster **beveiligingsrol toevoegen** een of meer beschik bare beveiligings rollen, kies **toevoegen**en selecteer een object type dat u aan de geselecteerde beveiligings rollen wilt koppelen. Als u **beveiligings bereik** of **verzameling**selecteert, schakelt u het selectie vakje in voor een of meer objecten om die selectie te volt ooien en kiest u vervolgens **OK**.  

        > [!NOTE]  
        > U moet minimaal één beveiligingsbereik configureren voordat de geselecteerde beveiligingsrollen aan de gebruiker met beheerdersrechten kunnen worden toegewezen. Wanneer u meerdere beveiligingsrollen selecteert, wordt elk beveiligingsbereik en elke verzameling die u configureert gekoppeld aan elk van deze geselecteerde beveiligingsrollen.  

    - Als u beveiligings rollen wilt verwijderen, selecteert u een of meer beveiligings rollen in de lijst en kiest u vervolgens **verwijderen**.  

7. Als u de beveiligingsbereiken en verzamelingen wilt wijzigen die zijn gekoppeld aan een specifieke beveiligingsrol, kiest u het tabblad **beveiligingsbereiken** , selecteert u de beveiligingsrol en vervolgens kiest u **bewerken**.  

    - Om nieuwe objecten aan deze beveiligingsrol te koppelen, klikt u op **toevoegen**en selecteert u een object type dat u aan de geselecteerde beveiligings rollen wilt koppelen. Als u **beveiligings bereik** of **verzameling**selecteert, schakelt u het selectie vakje in voor een of meer objecten om die selectie te volt ooien en kiest u vervolgens **OK**.  

        > [!NOTE]  
        > U moet ten minste één beveiligings bereik configureren.  

    - Als u een beveiligings bereik of verzameling wilt verwijderen die is gekoppeld aan deze beveiligingsrol, selecteert u het object en kiest u vervolgens **verwijderen**.  

    - Wanneer u klaar bent met het wijzigen van de gekoppelde objecten, kiest u **OK**.  

8. Kies **OK** om deze procedure te volt ooien.  

    > [!CAUTION]  
    > Wanneer een beveiligingsrol gebruikers met beheerdersrechten de machtiging voor het implementeren van verzamelingen verleent, kunnen die gebruikers met beheerdersrechten objecten distribueren uit elk beveiligingsbereik waarvoor ze een **leesmachtiging** hebben, ook als dat beveiligingsbereik gekoppeld is aan een andere beveiligingsrol.  

## <a name="next-steps"></a>Volgende stappen

[Accounts die worden gebruikt in Configuration Manager](../../../plan-design/hierarchy/accounts.md)

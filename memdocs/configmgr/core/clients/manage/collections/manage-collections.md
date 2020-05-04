---
title: Verzamelingen beheren
titleSuffix: Configuration Manager
description: Voer algemene beheer taken voor verzamelingen uit in Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2fc8347ae766cbd16075ef4170efa2f8042371f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714337"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Verzamelingen beheren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de overzichts informatie in dit artikel om u te helpen bij het uitvoeren van beheer taken voor verzamelingen in Configuration Manager.  

> [!NOTE]  
>  Zie [verzamelingen maken](create-collections.md)voor informatie over het maken van Configuration Manager verzamelingen.



## <a name="how-to-manage-device-collections"></a><a name="bkmk_device"></a>Verzamelingen beheren  

In de werkruimte **Activa en naleving** selecteert u **Apparaatverzamelingen**, selecteert u de te beheren verzameling en selecteert u vervolgens een beheertaak.  


#### <a name="show-members"></a>Leden weergeven
Hiermee worden alle resources die lid zijn van de geselecteerde verzameling weergegeven in een tijdelijk knooppunt onder het knooppunt **Apparaten** .


#### <a name="add-selected-items"></a>Geselecteerde items toevoegen
Biedt de volgende opties: 

- **Geselecteerde items toevoegen aan de bestaande verzameling apparaten**: Hiermee opent u het dialoog venster **verzameling selecteren** . Selecteer de verzameling waaraan u de leden van de geselecteerde verzameling wilt toevoegen. De geselecteerde verzameling is opgenomen in deze verzameling met behulp van de lidmaatschapsregel **Verzamelingen opnemen** .  

- **Geselecteerde items toevoegen aan de nieuwe verzameling apparaten**: Hiermee opent u de **wizard apparaatbesturing maken** , waarin u een nieuwe verzameling kunt maken. De geselecteerde verzameling is opgenomen in deze verzameling met behulp van de lidmaatschapsregel **Verzamelingen opnemen** .  


Zie [verzamelingen maken](create-collections.md)voor meer informatie.


#### <a name="install-client"></a>Client installeren
Hiermee opent u de **wizard Client installeren**. Deze wizard maakt gebruik van client push installatie om een Configuration Manager-client te installeren op alle computers in de geselecteerde verzameling. Zie [client push Installation](../../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)(Engelstalig) voor meer informatie.


#### <a name="run-script"></a>Script uitvoeren
Hiermee opent u de wizard **script uitvoeren** om een Power shell-script uit te voeren op alle clients in de verzameling. Zie [Power shell-scripts maken en uitvoeren](../../../../apps/deploy-use/create-deploy-scripts.md)voor meer informatie.


#### <a name="manage-affinity-requests"></a>Affiniteitsaanvragen beheren
Hiermee opent u het dialoog venster **affiniteits aanvragen van gebruikers apparaten beheren** . In behandeling zijnde aanvragen goed keuren of afwijzen voor het instellen van affiniteit van gebruikers apparaten voor apparaten in de geselecteerde verzameling. Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) voor meer informatie


#### <a name="clear-required-pxe-deployments"></a>Vereiste PXE-implementaties wissen
Hiermee wist u alle vereiste PXE-opstartimplementaties van alle leden van de geselecteerde verzameling. Zie [PXE gebruiken om Windows via het netwerk te implementeren](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie.


#### <a name="update-membership"></a>Lidmaatschap bijwerken
Hiermee evalueert u het lidmaatschap voor de geselecteerde verzameling. Voor verzamelingen met veel leden kan deze update even duren. Gebruik de actie **Vernieuwen** om de weergave bij te werken met de nieuwe leden van de verzamelingen nadat de update is voltooid.


#### <a name="add-resources"></a>Resources toevoegen
Hiermee opent u het dialoog venster **resources toevoegen aan verzameling** . Zoeken naar nieuwe resources om toe te voegen aan de geselecteerde verzameling. Het pictogram voor de geselecteerde verzameling geeft een zand loper weer terwijl de update wordt uitgevoerd.


#### <a name="client-notification"></a>Clientmeldingen
Zie [client meldingen](../client-notification.md)voor meer informatie.


#### <a name="endpoint-protection"></a>Endpoint Protection
Zie [client meldingen](../client-notification.md)voor meer informatie.


#### <a name="export"></a>Exporteren
Hiermee opent u de **wizard verzameling exporteren** waarmee u deze verzameling kunt exporteren naar een MOF-bestand (Managed Object Format). Dit bestand kan vervolgens worden gearchiveerd of geïmporteerd op een andere Configuration Manager-site. Wanneer u een verzameling exporteert, worden verzamelingen waarnaar wordt verwezen, niet geëxporteerd. Naar een verzameling waarnaar wordt verwezen, wordt verwezen door de geselecteerde verzameling door het gebruik van een regel voor **opnemen** of **uitsluiten** .


#### <a name="copy"></a>Exemplaar
Hiermee wordt een kopie gemaakt van de geselecteerde verzameling. De nieuwe verzameling gebruikt de geselecteerde verzameling als een beperkende verzameling.


#### <a name="refresh"></a>Vernieuwen
Vernieuw de weer gave.


#### <a name="delete"></a>Verwijderen
Hiermee verwijdert u de geselecteerde verzameling. U kunt ook alle resources in de verzameling verwijderen uit de sitedatabase. 

U kunt de verzamelingen die in Configuration Manager zijn ingebouwd, niet verwijderen. Zie [Inleiding tot verzamelingen](introduction-to-collections.md#built-in-collections)voor een lijst van de ingebouwde verzamelingen.


#### <a name="simulate-deployment"></a>Implementatie simuleren
Hiermee opent u de **wizard implementatie van toepassing simuleren**. Met deze wizard kunt u de resultaten van een toepassings implementatie testen zonder de toepassing te installeren of te verwijderen. Zie voor meer informatie [toepassings implementaties simuleren](../../../../apps/deploy-use/simulate-application-deployments.md).


#### <a name="deploy"></a>Implementeren
De opties zijn als volgt:  

- **Toepassing**: Hiermee opent u de **wizard software implementeren**. Een toepassings implementatie selecteren en configureren voor de geselecteerde verzameling. Zie [toepassingen implementeren](../../../../apps/deploy-use/deploy-applications.md)voor meer informatie.  

- **Programma**: Hiermee opent u de **wizard software implementeren**. Een pakket-en programma-implementatie selecteren en configureren voor de geselecteerde verzameling. Zie [pakketten en Program ma's](../../../../apps/deploy-use/packages-and-programs.md)voor meer informatie.  

- **Configuratie basislijn**: Hiermee opent u het dialoog venster **configuratie basislijnen implementeren** . De implementatie van een of meer configuratie basislijnen configureren voor de geselecteerde verzameling. Zie [configuratie basislijnen implementeren](../../../../compliance/deploy-use/deploy-configuration-baselines.md)voor meer informatie.  

- **Taken reeks**: Hiermee opent u de **wizard software implementeren**. Een taken reeks implementatie selecteren en configureren voor de geselecteerde verzameling. Raadpleeg taken [reeksen beheren om taken te automatiseren](../../../../osd/deploy-use/deploy-a-task-sequence.md)voor meer informatie.  

- **Software-updates**: Hiermee opent u de **wizard software-updates implementeren**. Configureer de implementatie van software-updates voor resources in de geselecteerde verzameling. Zie [software-updates beheren](../../../../sum/understand/software-updates-introduction.md)voor meer informatie.  


#### <a name="clear-server-group-deployment-locks"></a>Implementatie vergrendelingen Server groep wissen
Alle implementatie vergrendelingen van de Server groep hand matig vrijgeven voor de verzameling. Zie [service a Server Group](../../../../sum/deploy-use/service-a-server-group.md)(Engelstalig) voor meer informatie.


#### <a name="move"></a>Verplaatsen
Verplaats de geselecteerde verzameling naar een andere map in het knoop punt **apparaat Collections** . 


#### <a name="properties"></a>Eigenschappen
Zie [verzamelings eigenschappen](#BKMK_CollProp)voor meer informatie.  


## <a name="how-to-manage-user-collections"></a><a name="bkmk_user"></a>Gebruikers verzamelingen beheren  

In de werkruimte **Activa en naleving** selecteert u **Gebruikersverzamelingen**, selecteert u de te beheren verzameling en selecteert u vervolgens een beheertaak.  

> [!Note]  
> De volgende acties zijn beschikbaar voor gebruikers verzamelingen, maar het gedrag is hetzelfde als bij verzamelingen met apparaten. Dit is niet van toepassing op gebruikers verzamelingen en de gebruikers binnen. Zie voor meer informatie de betreffende actie in het [beheer van apparaat verzamelingen](#bkmk_device).  

- **Leden weergeven**  
- **Geselecteerde items toevoegen**  
    - **Geselecteerde items toevoegen aan de bestaande gebruikers verzameling**  
    - **Geselecteerde items toevoegen aan de nieuwe gebruikers verzameling**  
- **Affiniteitsaanvragen beheren**  
- **Lidmaatschap bijwerken**  
- **Resources toevoegen**  
- **Exporteren**  
- **Kopieer**  
- **Vernieuwen**  
- **Verwijderen**  
- **Implementatie simuleren**  
- **Implementeren**  
    - **Toepassing**  
    - **Programma**  
    - **Configuratie basislijn**
- **Verplaatsen**  
- **Eigenschappen**


##  <a name="collection-properties"></a><a name="BKMK_CollProp"></a> Verzamelingseigenschappen  

Wanneer u het dialoog venster **Eigenschappen** opent voor een verzameling, kunt u de volgende opties weer geven en configureren:  

#### <a name="general"></a>Algemeen
Algemene informatie weer geven en configureren over de geselecteerde verzameling, met inbegrip van de naam van de verzameling en de beperkende verzameling.

#### <a name="membership-rules"></a>Lidmaatschapsregels
De lidmaatschaps regels configureren waarmee het lidmaatschap van deze verzameling wordt gedefinieerd. Zie [verzamelingen maken](create-collections.md)voor meer informatie.  

#### <a name="power-management"></a>Energiebeheer
Energiebeheer plannen configureren die u hebt toegewezen aan computers in de geselecteerde verzameling. Zie [Introduction to Power Management](../power/introduction-to-power-management.md)(Engelstalig) voor meer informatie.  

#### <a name="deployments"></a>Implementaties
Geeft alle software weer die u hebt geïmplementeerd op leden van de geselecteerde verzameling.  

#### <a name="maintenance-windows"></a>Onderhoudsvensters
Onderhouds vensters weer geven en configureren die worden toegepast op leden van de geselecteerde verzameling. Zie [onderhouds Vensters gebruiken](use-maintenance-windows.md)voor meer informatie.

#### <a name="collection-variables"></a>Verzamelings variabelen
Configureer variabelen die van toepassing zijn op deze verzameling en die kunnen worden gebruikt door taken reeksen. Zie [taken reeks variabelen instellen](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set)voor meer informatie.  

#### <a name="distribution-point-groups"></a>Distributiepuntgroepen
Een of meer distributiepunten groepen koppelen aan leden van de geselecteerde verzameling. Zie [inhoud en infra structuur voor inhoud beheren](../../../servers/deploy/configure/manage-content-and-content-infrastructure.md)voor meer informatie.

#### <a name="aad-group-sync"></a>Synchronisatie van AAD-groep
De resultaten van het verzamelings lidmaatschap synchroniseren met Azure Active Directory groepen. Deze synchronisatie is een [voorlopige versie](../../../servers/manage/pre-release-features.md) van het onderdeel vanaf versie 1906. Zie [verzamelingen maken](create-collections.md#bkmk_aadcollsync)voor meer informatie.

#### <a name="security"></a>Beveiliging
Hiermee worden de gebruikers met beheerdersrechten weergegeven die beschikken over machtigingen voor de geselecteerde verzameling via bijbehorende rollen en beveiligingsbereiken. Zie [basis principes van beheer op basis van rollen](../../../understand/fundamentals-of-role-based-administration.md)voor meer informatie.  

#### <a name="alerts"></a>Waarschuwingen 
Configureren wanneer waarschuwingen worden gegenereerd voor de client status en de Endpoint Protection. Zie [How to configure client status](../../deploy/configure-client-status.md) and [how to monitor Endpoint Protection](../../../../protect/deploy-use/monitor-endpoint-protection.md)voor meer informatie.  
## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Power shell gebruiken

Power shell kan worden gebruikt om verzamelingen te beheren.  Zie voor meer informatie:

* [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection)
* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Kopiëren-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/copy-cmcollection)
* [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmcollection)
* [Exporteren-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke-CMCollectionUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Remove-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-CMCollectionToAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remove-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Remove-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Add-CMCollectionToDistributionPointGroup](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remove-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remove-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remove-CMCollectionFromAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)

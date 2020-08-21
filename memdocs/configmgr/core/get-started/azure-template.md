---
title: Een lab maken in Azure
titleSuffix: Configuration Manager
description: Het maken van een Configuration Manager Technical Preview Lab of het huidige branch Evaluation Lab automatiseren met behulp van Azure-sjablonen
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ea1965d6cae90808156957be1c9634e4c1631aa8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694522"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Een Configuration Manager Lab maken in azure

*Van toepassing op: Configuration Manager (huidige vertakking, Technical Preview-vertakking)*

<!--3556017-->

In deze hand leiding wordt beschreven hoe u een Configuration Manager test omgeving bouwt in Microsoft Azure. Azure-sjablonen worden gebruikt voor het vereenvoudigen en automatiseren van het maken van een Lab met Azure-resources. Er worden twee Azure-sjablonen meegeleverd: 

- Met Configuration Manager Technical Preview Azure-sjabloon wordt de nieuwste versie van de Configuration Manager Technical Preview-vertakking geïnstalleerd.
- Met Configuration Manager huidige branch Azure-sjabloon wordt de evaluatie van de nieuwste versie van Configuration Manager current branch geïnstalleerd. 

Zie [Configuration Manager op Azure](../understand/configuration-manager-on-azure.md)voor meer informatie.



## <a name="prerequisites"></a>Vereisten

Dit proces vereist een Azure-abonnement waarin u de volgende objecten kunt maken: 
- Twee Standard_B2s virtuele machines voor domein controller, beheer punt en distributie punt.
- Eén Standard_B2ms virtuele machine voor de primaire site server en de SQL database-server.
- Standard_LRS Storage-account

> [!Tip]  
> Zie de [Azure-prijs calculator](https://azure.microsoft.com/pricing/calculator/)om mogelijke kosten te bepalen.  



## <a name="process"></a>Proces

1. Ga naar de [Configuration Manager Technical Preview-sjabloon](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) of [Configuration Manager current branch-sjabloon](https://azure.microsoft.com/resources/templates/sccm-currentbranch/).  

2. Selecteer **implementeren naar Azure**, waarmee de Azure portal wordt geopend.  

3. Voltooi de Azure Quick Start-sjabloon met de volgende informatie:

    - Basisbeginselen  

        - **Abonnement**: de naam van het abonnement waarin de vm's moeten worden gemaakt  

        - **Resource groep**: Selecteer een resource groep die voor deze vm's moet worden gebruikt  

        - **Locatie**: Selecteer een Azure-Data Center om deze test omgeving te hosten  

    - Instellingen  

        - **Voor voegsel**: de naam van het voor voegsel van de machines. Zie [Azure VM-info](#azure-vm-info)voor meer informatie.  

        - **Beheerder gebruikers naam**: de naam van een gebruiker op de vm's met beheerders rechten. U gebruikt deze gebruiker om u aan te melden bij de Vm's.  

        - **Beheerders wachtwoord**: het wacht woord moet voldoen aan de complexiteits vereisten van Azure. Zie [adminPassword](/rest/api/compute/virtualmachines/createorupdate#osprofile)voor meer informatie.  

    > [!Important]  
    > De volgende instellingen zijn vereist voor Azure. Gebruik de standaard waarden. Wijzig deze waarden niet.  
    > 
    > - ** \_ locatie van artefacten**: de locatie van de scripts voor deze sjabloon <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - ** \_ artefacten locatie SAS-token**: de sasToken is vereist voor toegang tot de artefacten locatie  
    > 
    > - **Locatie**: de locatie voor alle resources

4. Lees de voor waarden. Selecteer **Ik ga akkoord met de bovenstaande voorwaarden** als u akkoord gaat. Selecteer vervolgens **aankoop** om door te gaan. 

De instellingen worden gevalideerd door Azure en de implementatie wordt gestart. Controleer de status van de implementatie in het Azure Portal. 

> [!NOTE]
> Het proces kan 2-4 uur duren. Zelfs wanneer de Azure Portal een geslaagde implementatie toont, blijven configuratie scripts worden uitgevoerd. Start de virtuele machines niet opnieuw op tijdens het proces.

Als u de status van de configuratie scripts wilt weer geven, maakt u verbinding met de `<prefix>PS1` Server en bekijkt u het volgende bestand: `%windir%\TEMP\ProvisionScript\PS1.json` . Als alle stappen worden weer gegeven als voltooid, wordt het proces uitgevoerd.

Als u verbinding wilt maken met de virtuele machines, moet u eerst de Azure Portal de open bare IP-adressen voor elke virtuele machine ophalen. Wanneer u verbinding maakt met de virtuele machine, is de domein naam `contoso.com` . Gebruik de referenties die u hebt opgegeven in de implementatie sjabloon. Zie [verbinding maken en aanmelden bij een virtuele Azure-machine met Windows](/azure/virtual-machines/windows/connect-logon)voor meer informatie.



## <a name="azure-vm-info"></a>Informatie over Azure VM

Alle drie de virtuele machines hebben de volgende specificaties:
- 150 GB schijf ruimte
- Zowel een openbaar als een particulier IP-adres. De open bare Ip's bevinden zich in een netwerk beveiligings groep die alleen verbindingen met extern bureau blad toestaat op TCP-poort 3389. 

Het voor voegsel dat u hebt opgegeven in de implementatie sjabloon is het voor voegsel van de VM-naam. Als u bijvoorbeeld ' Contoso ' als voor voegsel hebt ingesteld, is de computer naam van de domein controller `contosoDC` .


### `<prefix>DC01`

- Active Directory-domeincontroller
- Standard_B2s, met twee processors en 4 GB geheugen
- Windows Server 2019 Data Center Edition

#### <a name="windows-features-and-roles"></a>Windows-onderdelen en -rollen
- Active Directory Domain Services (toevoegen)
- .NET
- Externe differentiële compressie (RDC)


### `<prefix>PS01`

- Standard_B2ms, met twee processors en 8 GB aan geheugen
- Windows Server 2016 Data Center Edition
- SQL Server
- Windows 10 ADK met Windows PE 
- Primaire site Configuration Manager

#### <a name="windows-features-and-roles"></a>Windows-onderdelen en -rollen
- .NET
- Externe differentiële compressie (RDC) 
- Internet Information Service (IIS)


### `<prefix>DPMP01`

- Standard_B2s, met twee processors en 4 GB geheugen
- Windows Server 2019 Data Center Edition
- Distributiepunt
- Beheerpunt

#### <a name="windows-features-and-roles"></a>Windows-onderdelen en -rollen
- .NET
- Externe differentiële compressie (RDC) 
- Internet Information Service (IIS)
- Background Intelligent overboeking service (BITS)

### `<prefix>CL01`

- Alleen voor Configuration Manager huidige branch-evaluatie sjabloon
- Windows 10
- Configuration Manager-client
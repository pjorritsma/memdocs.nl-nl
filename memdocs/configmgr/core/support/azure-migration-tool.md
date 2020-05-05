---
title: On-premises site uitbreiden en migreren naar Microsoft Azure
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van het hulp programma voor migratie voor het programmatisch maken van Azure virtual machines voor Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 00f07e20c24ea9bb7d06b18f300e0206696c5e20
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723451"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>On-premises site uitbreiden en migreren naar Microsoft Azure

*Van toepassing op: Configuration Manager (Current Branch)*


Met dit hulp programma, dat is geïntroduceerd in versie 1910, kunt u via programma code virtuele Azure-machines (Vm's) maken voor Configuration Manager. <!--3556022--> Het kan worden geïnstalleerd met de standaard instellingen site rollen zoals een passieve site server, beheer punten en distributie punten. Wanneer u de nieuwe rollen hebt gevalideerd, kunt u deze gebruiken als aanvullende site systemen voor hoge Beschik baarheid. U kunt ook de on-premises site systeemrol verwijderen en alleen de Azure VM-rol blijven gebruiken.

## <a name="prerequisites"></a>Vereisten

- Een Azure-abonnement

- Virtueel Azure-netwerk met ExpressRoute-gateway

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- Uw gebruikers account moet een Configuration Manager **volledige beheerder** zijn en beschikt over beheerders rechten op de primaire site server.

- Als u een passieve server wilt toevoegen, moet de primaire site voldoen aan de [vereisten voor hoge Beschik baarheid van de site server](../servers/deploy/configure/site-server-high-availability.md#prerequisites). Hiervoor is bijvoorbeeld een [externe inhouds bibliotheek](../plan-design/hierarchy/the-content-library.md#bkmk_remote)vereist.

### <a name="required-azure-permissions"></a>Vereiste machtigingen voor Azure

U hebt de volgende machtigingen nodig in azure wanneer u het hulp programma uitvoert:
<!--5789222-->
Micro soft. resources/abonnementen/resourceGroups/lezen <br>
Micro soft. resources/abonnementen/resourceGroups/schrijven <br>
Micro soft. resources/implementaties/lezen <br>
Micro soft. resources/implementaties/schrijven <br>
Micro soft. resources/implementaties/valideren/actie <br>
Micro soft. Compute/informatie/uitbrei dingen/lezen <br>
Micro soft. Compute/informatie/Extensions/write <br>
Micro soft. Compute/informatie/lezen <br>
Micro soft. Compute/informatie/schrijven <br>
Micro soft. Network/virtualNetworks/lezen <br>
Microsoft.Network/virtualNetworks/subnets/read <br>
Microsoft.Network/virtualNetworks/subnets/join/action <br>
Micro soft. Network/networkInterfaces/lezen <br>
Micro soft. Network/networkInterfaces/schrijven <br>
Micro soft. Network/networkInterfaces/samen voegen/actie <br>
Micro soft. Network/networkSecurityGroups/schrijven <br>
Micro soft. Network/networkSecurityGroups/lezen <br>
Micro soft. Network/networkSecurityGroups/samen voegen/actie <br>
Micro soft. Storage/Storage accounts/schrijven <br>
Micro soft. Storage/Storage accounts/lezen <br>
Micro soft. Storage/Storage accounts/listkeys ophalen/Action <br>
Micro soft. Storage/Storage accounts/listServiceSas/Action <br>
Micro soft. Storage/Storage accounts/blobServices/containers/schrijven <br>
Micro soft. Storage/Storage accounts/blobServices/containers/lezen <br>
Micro soft.-sleutel kluis/-kluizen/implementeren/actie <br>
Micro soft.-sleutel kluis/-kluizen/lezen <br>


Zie [toegang tot Azure-resources beheren met RBAC](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal)voor meer informatie over machtigingen en het toewijzen van rollen.

## <a name="run-the-tool"></a>Het hulp programma uitvoeren

1. Meld u aan bij de primaire site server en voer het volgende hulp programma uit in de map Configuration Manager Installation:`Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. Bekijk de informatie op het tabblad **Algemeen** en schakel over naar het tabblad **Azure Information** .

1. Kies op het tabblad **Azure Information** uw **Azure-omgeving**en **Meld**u aan.

    > [!TIP]
    > Mogelijk moet u toevoegen `https://*.microsoft.com` aan de lijst met vertrouwde websites om u op de juiste manier aan te melden.

    [![Het tabblad Azure Information van het hulp programma Extend and migrate](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. Nadat u zich hebt aangemeld, selecteert u de **abonnements-id** en het **virtuele netwerk**. Het hulp programma vermeldt alleen netwerken met een ExpressRoute-gateway.

## <a name="site-server-high-availability"></a>Hoge Beschik baarheid site server

1. Selecteer op het tabblad **maximale Beschik baarheid van site server** de optie **controleren** om de gereedheid van uw site te evalueren.

    Als een van de controles mislukt, selecteert u **meer details** om te bepalen hoe het probleem moet worden opgelost. Zie [hoge Beschik baarheid van site server](../servers/deploy/configure/site-server-high-availability.md#prerequisites)voor meer informatie over deze vereisten.

2. Als u de site server wilt uitbreiden of migreren naar Azure, selecteert u **een site server maken in azure**. Vul vervolgens de volgende velden in:

    |Naam|Beschrijving|
    |---|---|
    |**Abonnement**|Alleen-lezen. Hier worden de abonnements naam en-ID weer gegeven.|
    |**Resourcegroep**| Een lijst met beschik bare resource groepen. Als u een nieuwe resource groep wilt maken, gebruikt u de [Azure Portal](https://portal.azure.com)en voert u dit hulp programma opnieuw uit.|
    |**Locatie**| Alleen-lezen. Bepaald door de locatie van uw virtuele netwerk|
    |**VM-grootte**|Kies een grootte die past bij uw werk belasting. Micro soft adviseert de **Standard_DS3_v2**.|
    |**Besturingssysteem**|Alleen-lezen. Het hulp programma maakt gebruik van Windows Server 2019.|
    |**Schijf type**|Alleen-lezen. Het hulp programma gebruikt Premium-SSD voor de beste prestaties.|
    |**Virtueel netwerk**|Alleen-lezen.|
    |**Subnetrouter**|Selecteer het subnet dat u wilt gebruiken. Als u een nieuw subnet moet maken, gebruikt u de [Azure Portal](https://portal.azure.com).|
    |**Computer naam**|Voer de naam in van de passieve Site Server-VM in Azure. Dit is dezelfde naam die wordt weer gegeven in de [Azure Portal](https://portal.azure.com).|
    |**Lokale gebruikers naam beheerder**|Voer de naam in van de lokale gebruiker met beheerders rechten die de Azure VM maakt voordat deze lid wordt van het domein.|
    |**Wacht woord van lokale beheerder**|Het wacht woord van de lokale gebruiker met beheerders rechten. Als u het wacht woord tijdens de Azure-implementatie wilt beveiligen, slaat u het wacht woord op als geheim in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Gebruik vervolgens de verwijzing hier. Als dat nodig is, kunt u een nieuwe maken op basis van de [Azure Portal](https://portal.azure.com).|
    |**Domein-FQDN**|De Fully Qualified Domain Name voor het Active Directory domein om lid te worden. Het hulp programma haalt standaard deze waarde op van uw huidige computer.|
    |**Domein gebruikers naam**|De naam van de domein gebruiker die lid mag worden van het domein. Het hulp programma gebruikt standaard de naam van de momenteel aangemelde gebruiker.|
    |**Domein wachtwoord**|Het wacht woord van de domein gebruiker om lid te worden van het domein. Het hulp programma controleert dit nadat u **starten**hebt geselecteerd. Als u het wacht woord tijdens de Azure-implementatie wilt beveiligen, slaat u het wacht woord op als geheim in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Gebruik vervolgens de verwijzing hier. Als dat nodig is, kunt u een nieuwe maken op basis van de [Azure Portal](https://portal.azure.com).|
    |**DNS IP van domein**|Wordt gebruikt om lid te worden van het domein. Het hulp programma maakt standaard gebruik van de huidige DNS van uw huidige computer.|
    |**Type**|Alleen-lezen. Er wordt een *passieve site server* als het type weer gegeven.|

    > [!IMPORTANT]
    > Standaard zijn de virtuele machines ingesteld op **Nee** voor het **gebruik van een bestaande Windows Server-licentie**. Als u gebruik wilt maken van uw on-premises Windows Server-licenties met Software Assurance, configureert u deze instelling in de [Azure Portal](https://portal.azure.com) nadat de virtuele machines zijn ingericht. Zie [Azure Hybrid Benefit voor Windows Server](https://docs.microsoft.com/windows-server/get-started/azure-hybrid-benefit)voor meer informatie.

1. Selecteer **Start**om te beginnen met het inrichten van de Azure VM. Als u de implementatie status wilt controleren, gaat u naar het tabblad **implementaties in azure** in het hulp programma. Als u de meest recente status wilt ophalen, selecteert u **Implementatie status vernieuwen**.

    > [!TIP]
    > U kunt ook de [Azure Portal](https://portal.azure.com) gebruiken om de status te controleren, fouten te vinden en mogelijke oplossingen te bepalen.

1. Wanneer de implementatie is voltooid, gaat u naar uw SQL-servers en verleent u machtigingen voor de nieuwe virtuele machine van Azure. Zie [vereisten voor hoge Beschik baarheid van site server](../servers/deploy/configure/site-server-high-availability.md#prerequisites)voor meer informatie.

1. Als u de Azure-VM als een site server in de passieve modus wilt toevoegen, selecteert u **site server toevoegen in de passieve modus**.

1. Zodra de site server in de passieve modus is toegevoegd, wordt de status weer gegeven op het tabblad **maximale Beschik baarheid** van de site server.

   [![Passieve site server toegevoegd aan site server-tabblad maximale Beschik baarheid](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. Ga vervolgens naar het tabblad [implementaties in azure](#bkmk_deploy-azure) om de implementatie te volt ooien.

## <a name="site-database"></a>Sitedatabase

Het hulp programma heeft momenteel geen taken om de data base van on-premises naar Azure te migreren. U kunt ervoor kiezen om de data base te verplaatsen van een on-premises SQL-Server naar een Azure SQL Server VM. In het hulp programma worden de volgende artikelen op het tabblad **site database** weer gegeven om te helpen:

- [Back-up en herstel de database](../servers/manage/backup-and-recovery.md)
- [SQL always on configureren en toestaan dat de gegevens worden gerepliceerd](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [Een SQL database migreren naar een Azure SQL Server VM](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>Sitesysteemrollen

1. Schakel over naar het tabblad **site systeem rollen** . Selecteer **Nieuw maken**om een nieuwe site systeemrol in te richten met de standaard instellingen. U kunt rollen inrichten zoals het beheer punt, het distributie punt en het software-update punt. Niet alle rollen zijn momenteel beschikbaar in het hulp programma.

    [![Tabblad site systeem rollen in het hulp programma uitbreiden en migreren](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. In het inrichtings venster vult u de velden in voor het inrichten van de VM van de siterol in Azure. Deze details zijn vergelijkbaar met de bovenstaande lijst voor de site server.

1. Selecteer **Start**om te beginnen met het inrichten van de Azure VM. Als u de implementatie status wilt controleren, gaat u naar het tabblad **implementaties in azure** in het hulp programma. Als u de meest recente status wilt ophalen, selecteert u **Implementatie status vernieuwen**.

    > [!TIP]
    > U kunt ook de [Azure Portal](https://portal.azure.com) gebruiken om de status te controleren, fouten te vinden en mogelijke oplossingen te bepalen.

1. Herhaal dit proces om meer site systeem rollen toe te voegen.

1. Ga vervolgens naar het tabblad [implementaties in azure](#bkmk_deploy-azure) om de implementatie te volt ooien.

1. Wanneer de implementatie is voltooid, gaat u naar de Configuration Manager-console om aanvullende wijzigingen aan te brengen in de siterol.

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a>Implementaties in azure

1. Als de virtuele machine door Azure is gemaakt, gaat u naar het tabblad **implementaties in azure** in het hulp programma. Selecteer **implementeren** om de rol te configureren met de standaard instellingen.

1. Selecteer **uitvoeren** om het Power shell-script te starten.

    [![Site rollen implementeren door het gegenereerde Power shell-script uit te voeren](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. Herhaal dit proces om meer functies te configureren.

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a>Site rollen toevoegen aan een bestaande implementatie van een virtuele machine
<!--5665775, 6307931-->
Met ingang van Configuration Manager versie 2002, de on-premises site uitbreiden en migreren naar Microsoft Azure, wordt ondersteuning geboden voor het inrichten van meerdere site systeem rollen op één virtuele Azure-machine. U kunt site systeem rollen toevoegen nadat de eerste implementatie van de virtuele Azure-machine is voltooid. Voer de volgende stappen uit om een nieuwe rol toe te voegen aan een bestaande virtuele machine:
1. Klik op het tabblad **implementaties in azure** op een implementatie van een virtuele machine met de status **voltooid** .
1. Klik op de knop **nieuwe maken** om een extra rol toe te voegen aan de virtuele machine.


## <a name="next-steps"></a>Volgende stappen

Controleer uw wijzigingen in de [Azure Portal](https://portal.azure.com)

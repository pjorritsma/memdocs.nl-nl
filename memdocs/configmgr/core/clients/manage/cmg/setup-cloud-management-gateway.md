---
title: Een cloudbeheergateway instellen
titleSuffix: Configuration Manager
description: Gebruik dit stapsgewijze proces voor het instellen van een CMG (Cloud Management Gateway).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 9ba4466a40d49c4b78b75e6f85137dfd0a4ff5ce
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129134"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Cloud beheer gateway instellen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit proces bevat de stappen die nodig zijn voor het instellen van een Cloud beheer gateway (CMG).

> [!Note]  
> Configuration Manager schakelt deze optionele functie standaard niet in. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).

## <a name="before-you-begin"></a>Voordat u begint

Lees eerst het artikel [plan voor Cloud beheer gateway](plan-cloud-management-gateway.md). Gebruik dit artikel om uw CMG-ontwerp te bepalen.

Gebruik de volgende controle lijst om ervoor te zorgen dat u over de benodigde informatie en vereisten beschikt voor het maken van een CMG:  

- De Azure-omgeving die moet worden gebruikt. Bijvoorbeeld de open bare Azure-Cloud of de Azure-Cloud voor de Amerikaanse overheid.  

- U hebt een of meer certificaten nodig voor CMG, afhankelijk van uw ontwerp. Zie [certificaten voor Cloud beheer gateway](certificates-for-cloud-management-gateway.md)voor meer informatie.  

- U hebt de volgende vereisten nodig voor een [Azure Resource Manager](plan-cloud-management-gateway.md#azure-resource-manager) implementatie van CMG:  

  - Integratie met [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) voor **Cloud beheer**. Azure AD-gebruikers detectie is niet vereist. Als u de site wilt integreren met Azure AD om de CMG te implementeren met behulp van Azure Resource Manager, moet u een **globale beheerder**hebben.

  - De resource providers **micro soft. ClassicCompute**  &  **micro soft. Storage** moeten zijn geregistreerd in het Azure-abonnement. Zie [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services)voor meer informatie.

  - De **eigenaar** van een abonnement moet zich aanmelden om de CMG te implementeren.

- Een wereld wijd unieke naam voor de service. Deze naam is afkomstig uit het [certificaat voor CMG-Server verificatie](certificates-for-cloud-management-gateway.md#bkmk_serverauth).  

- Als CMG wordt ingeschakeld als een Cloud distributiepunt, moet dezelfde globale unieke CMG-service naam ook beschikbaar zijn als een globaal unieke opslag accountnaam. Deze naam is afkomstig uit het [certificaat voor CMG-Server verificatie](certificates-for-cloud-management-gateway.md#bkmk_serverauth).

- De Azure-regio voor deze CMG-implementatie.  

- Hoeveel VM-exemplaren u nodig hebt voor schaal en redundantie.  

- Als u de implementatie van de klassieke Azure-service nog steeds moet gebruiken in Configuration Manager versie 1810 of eerder, hebt u de volgende vereisten nodig:  

    > [!Important]  
    > Vanaf versie 1810 worden de klassieke service-implementaties in azure afgeschaft in Configuration Manager. Gebruik Azure Resource Manager-implementaties voor de Cloud beheer gateway. Zie [plan for CMG](plan-cloud-management-gateway.md#azure-resource-manager)voor meer informatie.  
    >
    > Vanaf Configuration Manager versie 1902 is Azure Resource Manager het enige implementatie mechanisme voor nieuwe exemplaren van de Cloud beheer gateway.<!-- 3605704 -->

  - Azure-abonnements-ID  

  - Azure-beheer certificaat  

## <a name="set-up-a-cmg"></a>Een CMG instellen

Voer deze procedure uit op de site op het hoogste niveau. Deze site is een zelfstandige primaire site of de centrale beheer site.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer **cloudbeheergateway**.  

2. Selecteer **Cloudbeheergateway maken** op het lint.  

3. Selecteer **Aanmelden**op de pagina Algemeen van de wizard. Verifieer met een Azure- **abonnements eigenaar** -account. De wizard vult automatisch de resterende velden in van de gegevens die zijn opgeslagen tijdens de vereisten voor Azure AD-integratie. Als u meerdere abonnementen hebt, selecteert u de **abonnements-id** van het abonnement dat u wilt gebruiken.

    > [!Note]  
    > Vanaf versie 1810 zijn de klassieke service-implementaties in azure afgeschaft in Configuration Manager. Selecteer in versie 1902 en eerder **Azure Resource Manager implementatie** als de implementatie methode CMG.
    >
    > Als u een klassieke service-implementatie wilt gebruiken, selecteert u die optie op deze pagina. Voer eerst uw Azure **-abonnements-id**in. Selecteer vervolgens **Bladeren**en kies de. PFX-bestand voor het Azure-beheer certificaat.

4. Geef de **Azure-omgeving** voor deze CMG op. De opties in de vervolg keuzelijst kunnen variëren, afhankelijk van de implementatie methode.  

5. Selecteer **Next**. Wacht tot de site de verbinding met Azure test.  

6. Selecteer op de pagina instellingen van de wizard eerst **Bladeren** en kies de. PFX-bestand voor het CMG-Server verificatie certificaat. De naam van dit certificaat vult de vereiste velden **FQDN** en **service naam** van de service in.  

   > [!NOTE]  
   > Het certificaat voor CMG-Server verificatie ondersteunt joker tekens. Als u een certificaat met Joker tekens gebruikt, vervangt u het sterretje ( `*` ) in het veld **FQDN van service** door de gewenste HOSTNAAM voor de CMG.<!--491233-->  

7. Selecteer de vervolg keuzelijst **regio** om de Azure-regio voor deze CMG te kiezen.  

8. Selecteer een **resource groeps** optie.
   1. Als u **bestaande gebruiken**kiest, selecteert u een bestaande resource groep in de vervolg keuzelijst. De geselecteerde resource groep moet al bestaan in de regio die u hebt geselecteerd in stap 7. Als u een bestaande resource groep selecteert en deze zich in een andere regio bevindt dan de eerder geselecteerde regio, kan CMG niet worden ingericht.
   2. Als u **Nieuw maken**kiest, voert u de naam van de nieuwe resource groep in.

9. Voer in het veld **VM-exemplaar** het aantal vm's voor deze service in. De standaard waarde is één, maar u kunt Maxi maal 16 Vm's per CMG schalen.  

10. Selecteer **certificaten** om door client vertrouwde basis certificaten toe te voegen. Voeg alle certificaten in de vertrouwens keten toe.  

    > [!Note]  
    > Een vertrouwd basis certificaat is niet vereist wanneer u Azure Active Directory (Azure AD) gebruikt voor client verificatie. Als u certificaten voor PKI-client verificatie gebruikt, moet u een vertrouwd basis certificaat toevoegen aan de CMG.<!--SCCMDocs-pr issue #2872-->
    >
    > In versie 1902 en eerder kunt u slechts twee vertrouwde basis certificerings instanties en vier tussenliggende (onderliggende) Ca's toevoegen.<!-- SCCMDocs-pr#4022 -->

11. Met de wizard kunt u de optie voor het **intrekken van client certificaten standaard controleren**. Een certificaatintrekkingslijst (CRL) moet openbaar worden gepubliceerd om deze verificatie te kunnen gebruiken. Zie voor meer informatie [de certificaatintrekkingslijst publiceren](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

12. Vanaf versie 1906 kunt u **TLS 1,2 afdwingen**. Deze instelling is alleen van toepassing op de Azure Cloud service-VM. Dit geldt niet voor on-premises Configuration Manager site servers of-clients. Raadpleeg [How to Enable tls 1,2](../../../plan-design/security/enable-tls-1-2.md)(Engelstalig) voor meer informatie over TLS 1,2.<!-- SCCMDocs-pr#4021 -->

13. Standaard maakt de wizard de volgende optie: **CMG toestaan als een Cloud distributiepunt te functioneren en inhoud van Azure Storage te bewaren**. Een CMG kan ook inhoud leveren aan clients. Deze functionaliteit vermindert de vereiste certificaten en kosten van virtuele Azure-machines.

14. Selecteer **Next**.  

15. Als u CMG-verkeer met een drempel van 14 dagen wilt bewaken, kiest u het selectie vakje om de drempel waarschuwing in te scha kelen. Geef vervolgens de drempel waarde en het percentage op waarmee de verschillende waarschuwings niveaus moeten worden verhoogd. Kies **volgende** wanneer u klaar bent.  

16. Controleer de instellingen en klik op **volgende**. Configuration Manager begint met het instellen van de service. Nadat u de wizard hebt gesloten, duurt het vijf tot 15 minuten voordat de service volledig is ingericht in Azure. Controleer de kolom **status** voor het nieuwe CMG om te bepalen wanneer de service gereed is.  

    > [!NOTE]
    > Gebruik **CloudMgr. log** en **CMGSetup. log**om problemen met CMG-implementaties op te lossen. Zie [logboek bestanden](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)voor meer informatie.

## <a name="configure-primary-site-for-client-certificate-authentication"></a>Primaire site configureren voor verificatie van client certificaten

Als u certificaten voor [client verificatie](certificates-for-cloud-management-gateway.md#bkmk_clientauth) gebruikt voor het verifiëren van clients met de CMG, volgt u deze procedure voor het configureren van elke primaire site.  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer **sites**.  

2. Selecteer de primaire site waaraan uw op internet gebaseerde clients zijn toegewezen en kies **Eigenschappen**.  

3. Ga naar het tabblad **communicatie beveiliging** van het eigenschappen venster van de primaire site en schakel het selectie vakje **PKI-client certificaat gebruiken (client verificatie) in wanneer dit beschikbaar is**.  

    > [!NOTE]
    > In versie 1902 en eerder wordt dit tabblad **client computer communicatie**genoemd.<!-- SCCMDocs#1645 -->

4. Als u geen CRL publiceert, schakelt u de optie voor **clients uit de certificaatintrekkingslijst (CRL) voor site systemen uit**.  

## <a name="add-the-cmg-connection-point"></a>Het CMG-verbindings punt toevoegen

Het CMG-verbindings punt is de site systeemrol voor het communiceren met de CMG. Volg de algemene instructies voor het [installeren van site systeem rollen](../../../servers/deploy/configure/install-site-system-roles.md)om het CMG-verbindings punt toe te voegen. Selecteer op de pagina selectie van systeem rollen van de wizard site Systeemrol toevoegen het **verbindings punt van de Cloud beheer gateway**. Selecteer vervolgens de **naam van de Cloud beheer gateway** waarmee deze server verbinding maakt. De wizard toont de regio voor de geselecteerde CMG.

> [!IMPORTANT]
> Het CMG-verbindings punt moet in sommige scenario's een [certificaat voor client verificatie](certificates-for-cloud-management-gateway.md#bkmk_clientauth) hebben.

Gebruik **CMGService. log** en **SMS_Cloud_ProxyConnector. log**om de CMG-service status op te lossen. Zie [logboek bestanden](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)voor meer informatie.

## <a name="configure-client-facing-roles-for-cmg-traffic"></a><a name="bkmk_role"></a>Client gerichte rollen configureren voor CMG-verkeer

Configureer de site systemen van het beheer punt en het software-update punt om CMG verkeer te accepteren. Voer deze procedure uit op de primaire site voor alle beheer punten en software-update punten die service op internet gebaseerde clients.  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **servers en site systeem rollen** . Selecteer op het tabblad Start van het lint in de groep weer gave de optie **servers met rol**. Selecteer vervolgens **beheer punt** in de lijst.  

2. Selecteer de site systeem server die u wilt configureren voor CMG-verkeer. Selecteer de rol **beheer punt** in het detail venster en selecteer vervolgens **Eigenschappen** in het lint.  

3. Schakel in het eigenschappen venster beheer punt onder client verbindingen het selectie vakje in naast het verkeer van de **Cloud beheer gateway Configuration Manager toestaan**.

    Afhankelijk van uw CMG-ontwerp en Configuration Manager-versie, moet u mogelijk de **https** -optie inschakelen. Zie [beheer punt voor HTTPS inschakelen](certificates-for-cloud-management-gateway.md#bkmk_mphttps)voor meer informatie.  

4. Selecteer **OK** om het venster Eigenschappen van beheer punt te sluiten.  

Herhaal deze stappen voor extra beheer punten, indien nodig, en voor alle software-update punten.

## <a name="configure-boundary-groups"></a>Grens groepen configureren
 
<!--3640932-->
Vanaf versie 1902 kunt u een CMG koppelen aan een grens groep. Met deze configuratie kunnen clients standaard of terugvallen op de CMG voor client communicatie, afhankelijk van de relaties tussen grens groepen.

Zie [grens groepen configureren](../../../servers/deploy/configure/boundary-groups.md)voor meer informatie over grens groepen.

Wanneer u [een grens groep maakt of configureert](../../../servers/deploy/configure/boundary-group-procedures.md), voegt u op het tabblad **verwijzingen** een Cloud beheer gateway toe. Met deze actie wordt de CMG gekoppeld aan deze grens groep.

## <a name="configure-clients-for-cmg"></a>Clients configureren voor CMG

Zodra de CMG-en site systeem rollen worden uitgevoerd, krijgen clients automatisch de locatie van de CMG-service op de volgende locatie aanvraag. Clients moeten zich op het intranet bevindt om de locatie van de CMG-service te kunnen ontvangen, tenzij u [Windows 10-clients installeert en toewijst met behulp van Azure AD voor authenticatie](../../deploy/deploy-clients-cmg-azure.md). De polling cyclus voor locatie aanvragen is elke 24 uur. Als u niet wilt wachten op de normale geplande locatie aanvraag, kunt u de aanvraag afdwingen. Als u de aanvraag wilt afdwingen, start u de SMS agent host-service (ccmexec.exe) opnieuw op de computer.

> [!NOTE]
> Standaard ontvangen alle clients het CMG-beleid. Dit gedrag beheren met de client instelling, [clients toestaan om een Cloud beheer gateway te gebruiken](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway).

De Configuration Manager-client bepaalt automatisch of deze zich op het intranet of Internet bevindt. Als de client verbinding kan maken met een domein controller of een on-premises beheer punt, wordt het verbindings type ingesteld op **momenteel intranet**. Als dat niet het geval **is, wordt**de locatie van de CMG-service gebruikt om te communiceren met de site.

> [!NOTE]
> U kunt afdwingen dat de client altijd de CMG gebruikt, ongeacht of deze zich op het intranet of Internet bevindt. Deze configuratie is handig voor test doeleinden of voor clients die u wilt dwingen om altijd de CMG te gebruiken. Stel de volgende register sleutel in op de client:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> U kunt deze instelling ook opgeven tijdens client installatie met behulp van de eigenschap [CCMALWAYSINF](../../deploy/about-client-installation-properties.md#ccmalwaysinf) .
>
> Deze instelling is altijd van toepassing, zelfs als de client naar een locatie gaat waar grens groeps configuraties anderszins gebruikmaken van lokale bronnen.

Als u wilt controleren of clients over het beleid beschikken met de CMG, opent u een Windows Power shell-opdracht prompt als beheerder op de client computer en voert u de volgende opdracht uit:

```powershell
Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`
```

Met deze opdracht worden alle beheer punten op internet weer gegeven die de client kent. Hoewel de CMG niet technisch een beheer punt op internet is, zien clients deze als één.

> [!NOTE]  
> Als u het CMG-client verkeer wilt oplossen, gebruikt u **CMGHttpHandler. log**, **CMGService. log**en **SMS_Cloud_ProxyConnector. log**. Zie [logboek bestanden](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)voor meer informatie.

### <a name="install-off-premises-clients-using-a-cmg"></a>On-premises clients installeren met behulp van een CMG

Als u de Configuration Manager-client wilt installeren op systemen die momenteel niet zijn verbonden met uw intranet, moet aan een van de volgende voor waarden worden voldaan. In alle gevallen is een lokaal Administrator-account op de doel systemen vereist.

1. De Configuration Manager site is op de juiste wijze geconfigureerd voor het gebruik van PKI-certificaten voor client verificatie. Daarnaast hebben de client systemen een geldig, uniek en vertrouwd certificaat voor client verificatie dat eerder aan hen is uitgegeven.

2. De systemen zijn lid van een Azure AD-domein en zijn lid van een hybride Azure AD-domein.

3. Op de site wordt Configuration Manager versie 2002 of hoger uitgevoerd.

Voor opties 1 en 2, wanneer u **ccmsetup.exe**uitvoert, gebruikt u de para meter **/MP** om de URL van de CMG op te geven. Zie [over para meters en eigenschappen van client installatie](../../deploy/about-client-installation-properties.md#mp)voor meer informatie.

Voor optie 3, vanaf Configuration Manager versie 2002, kunt u de-client installeren op systemen die niet zijn verbonden met uw intranet met behulp van een bulk registratie token. Zie [een token voor bulk registratie maken](../../deploy/deploy-clients-cmg-token.md#create-a-bulk-registration-token)voor meer informatie over deze methode.

### <a name="configure-off-premises-clients-for-cmg"></a>On-premises clients configureren voor CMG

U kunt systemen verbinden met een recent geconfigureerde CMG, waarbij de volgende voor waarden waar zijn:  

- Op systemen is de Configuration Manager-client al geïnstalleerd.

- Systemen zijn niet verbonden en kunnen niet worden verbonden met uw intranet.

- Systemen voldoen aan een van de volgende voor waarden:

  - Elk is een geldig, uniek en vertrouwd certificaat voor client verificatie dat eerder is uitgegeven

  - Lid van Azure AD-domein

  - Hybride Azure AD-domein toegevoegd

- U wilt de bestaande client niet volledig opnieuw installeren.

- U hebt een methode om een register waarde voor de machine te wijzigen en de **SMS agent host** -service opnieuw te starten met een lokaal beheerders account.

Als u de verbinding op deze systemen wilt forceren, maakt u de **REG_SZ** register vermelding `CMGFQDNs` in de sleutel `HKLM\Software\Microsoft\CCM` . Stel de waarde ervan in op de URL van de CMG, bijvoorbeeld `https://contoso-cmg.contoso.com` . Start de service **SMS agent host** Windows opnieuw op het apparaat.

Als de Configuration Manager-client geen huidig CMG of Internet gericht beheer punt in het REGI ster heeft ingesteld, wordt de `CMGFQDNs` register waarde automatisch gecontroleerd. Deze controle vindt plaats om de 25 uur, wanneer de **SMS agent host** -service wordt gestart, of wanneer een netwerk wijziging wordt gedetecteerd. Wanneer de client verbinding maakt met de site en informatie over een CMG, wordt deze waarde automatisch bijgewerkt.

## <a name="modify-a-cmg"></a>Een CMG wijzigen

### <a name="cmg-properties"></a>CMG-eigenschappen

Nadat u een CMG hebt gemaakt, kunt u enkele instellingen wijzigen. Selecteer de CMG in de console Configuration Manager en selecteer **Eigenschappen**. Configureer instellingen op de volgende tabbladen:  

#### <a name="general"></a>Algemeen

- **Azure-beheer certificaat**: Wijzig het Azure-beheer certificaat voor de CMG. Deze optie is handig wanneer u het certificaat bijwerkt voordat het verloopt.  

#### <a name="settings"></a>Instellingen

- **Certificaat bestand**: Wijzig het Server verificatie certificaat voor de CMG. Deze optie is handig wanneer u het certificaat bijwerkt voordat het verloopt.  

  > [!NOTE]
  > Wanneer u het Server verificatie certificaat voor de CMG verlengt, is de FQDN die is opgegeven voor de algemene naam (CN) van het certificaat hoofdletter gevoelig.  Als het certificaat dat momenteel in gebruik is, bijvoorbeeld een CN van heeft `https://contoso-cmg.contoso.com` , maakt u het nieuwe certificaat met dezelfde kleine letter cn. De wizard accepteert geen certificaat met de CN `https://CONTOSO-CMG.CONTOSO.COM` .

- **VM-exemplaar**: Wijzig het aantal virtuele machines dat door de service in azure wordt gebruikt. Met deze instelling kunt u de service dynamisch omhoog of omlaag schalen op basis van gebruik of kosten overwegingen.  

- **Certificaten**: vertrouwde basis-of tussenliggende CA-certificaten toevoegen of verwijderen. Deze optie is handig bij het toevoegen van nieuwe Ca's of het buiten gebruik stellen van verlopen certificaten.  

- **Intrekking van client certificaat controleren**: als u deze instelling niet hebt ingeschakeld bij het maken van de CMG, kunt u deze later opnieuw inschakelen nadat u de CRL hebt gepubliceerd. Zie voor meer informatie [de certificaatintrekkingslijst publiceren](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

- **Toestaan dat CMG als een Cloud distributiepunt fungeert en inhoud van Azure Storage**bewaart: deze optie is standaard ingeschakeld. Een CMG kan ook inhoud leveren aan clients. Deze functionaliteit vermindert de vereiste certificaten en kosten van virtuele Azure-machines.<!--1358651-->

#### <a name="alerts"></a>Waarschuwingen

U kunt de waarschuwingen op elk gewenst moment opnieuw configureren nadat u de CMG hebt gemaakt.

### <a name="redeploy-the-service"></a>De service opnieuw implementeren

Meer belang rijke wijzigingen, zoals de volgende configuraties, vereisen het opnieuw implementeren van de service:

- Klassieke implementatie methode voor het Azure Resource Manager
- Abonnement
- Servicenaam
- Privé voor open bare PKI
- Regio

Behoud altijd ten minste één actieve CMG voor Internet-clients om bijgewerkte beleids regels te ontvangen. clients op internet kunnen niet communiceren met een verwijderde CMG. Clients weten een nieuw abonnement pas wanneer ze teruggaan naar het intranet. Wanneer u een tweede CMG-exemplaar maakt om de eerste te verwijderen, maakt u ook een ander CMG-verbindings punt.

Clients vernieuwen het beleid standaard elke 24 uur. wacht daarom ten minste één dag nadat u een nieuwe CMG hebt gemaakt voordat u de oude verwijdert. Als clients zijn uitgeschakeld of zonder Internet verbinding, moet u mogelijk langer wachten.

Als u een bestaande CMG hebt voor de klassieke implementatie methode, moet u een nieuwe CMG implementeren om de implementatie methode Azure Resource Manager te gebruiken.<!--509753--> Er zijn twee opties:  

- Als u dezelfde service naam opnieuw wilt gebruiken:  

    1. Verwijder eerst de klassieke CMG, waarbij rekening wordt gehouden met de richt lijnen om altijd ten minste één actieve CMG te hebben voor clients op internet.  

    2. Maak een nieuwe CMG met behulp van een Resource Manager-implementatie. Het certificaat voor Server verificatie opnieuw gebruiken.  

    3. Configureer het CMG-verbindings punt opnieuw om het nieuwe CMG-exemplaar te gebruiken.  

- Als u een nieuwe service naam wilt gebruiken:  

    1. Maak een nieuwe CMG met behulp van een Resource Manager-implementatie. Gebruik een nieuw certificaat voor Server verificatie.  

    2. Maak een nieuw CMG-verbindings punt en koppeling met de nieuwe CMG.  

    3. Wacht ten minste één dag voor op internet gebaseerde clients beleid ontvangen over de nieuwe CMG.  

    4. Verwijder de klassieke CMG.  

> [!TIP]
> Het huidige implementatie model van een CMG bepalen:<!--SCCMDocs issue #611-->  
>
> 1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **cloudbeheergateway** .  
> 2. Selecteer het CMG-exemplaar.  
> 3. Zoek in het detail venster onder aan het venster naar het kenmerk **implementatie model** . Dit kenmerk is **Azure Resource Manager**voor een Resource Manager-implementatie. Het verouderde implementatie model met het Azure-beheer certificaat wordt weer gegeven als **azure Service Manager**.
>
> U kunt ook het kenmerk **implementatie model** toevoegen als een kolom aan de lijst weergave.  

### <a name="modifications-in-the-azure-portal"></a>Wijzigingen in de Azure Portal

Wijzig de CMG alleen van de Configuration Manager-console. Het is niet mogelijk om wijzigingen aan te brengen in de service of onderliggende Vm's rechtstreeks in Azure. Eventuele wijzigingen kunnen zonder kennisgeving verloren gaan. Net als bij elk PaaS kan de service op elk gewenst moment de Vm's opnieuw bouwen. Deze opnieuw opgebouwden kunnen zich voordoen voor het onderhoud van de back-end-hardware of het Toep assen van updates op het VM-besturings systeem.

### <a name="delete-the-service"></a>De service verwijderen

Als u de CMG wilt verwijderen, kunt u dit ook doen via de Configuration Manager-console. Het hand matig verwijderen van onderdelen in azure zorgt ervoor dat het systeem inconsistent is. Deze status blijft zwevende informatie en er kan onverwachte problemen optreden.

## <a name="next-steps"></a>Volgende stappen

- [Clients controleren op Cloud beheer gateway](monitor-clients-cloud-management-gateway.md)
- [Veelgestelde vragen over de Cloud beheer gateway](cloud-management-gateway-faq.md)

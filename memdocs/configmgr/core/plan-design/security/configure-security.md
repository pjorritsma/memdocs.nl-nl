---
title: Beveiliging configureren
titleSuffix: Configuration Manager
description: Configureer beveiligings opties voor Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc9718bef61544b45a1432099ebb9d0911367ea7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718663"
---
# <a name="configure-security-in-configuration-manager"></a>Beveiliging configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de informatie in dit artikel om u te helpen bij het instellen van beveiligings opties voor Configuration Manager. Dit omvat de volgende beveiligings opties:
- [Communicatie van client computers](#BKMK_ConfigureClientPKI) voor PKI-client certificaten  
- [Ondertekening en versleuteling](#BKMK_ConfigureSigningEncryption)  
- [Op rollen gebaseerd beheer](#BKMK_ConfigureRBA)  
- [Accounts beheren](#BKMK_ManageAccounts)  
- [Azure Active Directory configureren](#bkmk_azuread)  
- [Verificatie van de SMS-provider configureren](#bkmk_auth)  



##  <a name="configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a>Instellingen configureren voor PKI-client certificaten  

Indien u wilt de openbare-sleutelinfrastructuur (PKI)-certificaten te gebruiken voor clientverbindingen naar sitesystemen die Internet Information Services (IIS) gebruiken, gebruik dan de volgende procedure om instellingen te configureren voor deze instellingen.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Clientinstellingen PKI-certificaat configureren  

1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** . Selecteer de primaire site die u wilt configureren.  

2.  Kies **Eigenschappen**in het lint. Ga vervolgens naar het tabblad **communicatie van client computer** .  

    > [!Note]
    > Vanaf versie 1906 wordt dit tabblad **communicatie beveiliging**genoemd.<!-- SCCMDocs#1645 -->  

3.  Selecteer de instellingen voor site systemen die gebruikmaken van IIS.  

    - **Alleen https**: clients die aan de site zijn toegewezen, gebruiken altijd een PKI-client certificaat wanneer ze verbinding maken met site systemen die IIS gebruiken.  

    - **Https of http**: u hebt geen clients nodig om PKI-certificaten te gebruiken.  

    - Door **Configuration Manager gegenereerde certificaten gebruiken voor HTTP-site systemen**: Zie [Enhanced http](../hierarchy/enhanced-http.md)(Engelstalig) voor meer informatie over deze instelling.  

4.  Selecteer de instellingen voor client computers.  

    - **Client-PKI-certificaat gebruiken (verificatie mogelijkheid voor client) indien beschikbaar**: als u de **https-of http-** site server instelling hebt gekozen, kiest u deze optie als u een PKI-client certificaat wilt gebruiken voor http-verbindingen. De client gebruikt dit certificaat in plaats van een zelfondertekend certificaat om zichzelf te laten verifiëren door sitesystemen. Als u **alleen https**hebt gekozen, wordt deze optie automatisch gekozen.  

    Wanneer meer dan één geldig PKI-client certificaat beschikbaar is op een client, kiest u **wijzigen** om de selectie methoden voor client certificaten te configureren.  

    Voor meer informatie over de selectiemethode voor clientcertificaat, zie [Planning for PKI client certificate selection](plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

    - **Clients controleren de certificaatintrekkingslijst (CRL) voor site systemen**: Schakel deze instelling in voor clients om de CRL van uw organisatie voor ingetrokken certificaten te controleren.  

    Voor meer informatie over CRL-controle voor clients, zie [Planning for PKI certificate revocation](plan-for-security.md#BKMK_PlanningForCRLs).  

5.  Als u de certificaten voor vertrouwde basis certificerings instanties wilt importeren, bekijken en verwijderen, kiest u **instellen**.  

    Zie [planning voor de vertrouwde PKI-basis certificaten en de lijst met certificaat verleners](plan-for-security.md#BKMK_PlanningForRootCAs)voor meer informatie.  


Herhaal deze procedure voor alle primaire sites in de hiërarchie.  



##  <a name="configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a>Ondertekening en versleuteling configureren  

Configureer de meest beveiligde ondertekenings- en versleutelingsinstellingen voor sitesystemen die alle clients in de site kunnen ondersteunen. Deze instellingen zijn in het bijzonder belangrijk wanneer u clients laat communiceren met sitesystemen door gebruik te maken van zelfondertekende certificaten via HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Ondertekening en versleuteling voor een site configureren  

1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** . Selecteer de primaire site die u wilt configureren.  

2.  Selecteer in het lint **Eigenschappen**en schakel vervolgens over naar het tabblad **ondertekening en versleuteling** .  

    Dit tabblad is enkel beschikbaar op een primaire site. Als u het tabblad **ondertekening en versleuteling** niet ziet, zorg er dan voor dat u niet verbonden bent met een centrale beheer site of een secundaire site.  

3.  Configureer de ondertekenings-en versleutelings opties voor clients om te communiceren met de-site.  

    - **Ondertekening vereisen**: clients ondertekenen gegevens voordat ze naar het beheer punt verzenden.  

    - **SHA-256 vereisen**: clients gebruiken de SHA-256-algoritme bij het ondertekenen van gegevens.  

    > [!WARNING]  
    >  Geen **SHA-256 vereisen** zonder eerst te bevestigen dat alle clients dit hash-algoritme ondersteunen. Deze clients bevatten koppelingen die in de toekomst kunnen worden toegewezen aan de site.  
    >   
    >  Als u deze optie kiest en clients met zelfondertekende certificaten SHA-256 niet ondersteunen, worden ze door Configuration Manager geweigerd. Het onderdeel SMS_MP_CONTROL_MANAGER registreert de bericht-ID 5443.  

    - **Versleuteling gebruiken**: clients inventarisatie gegevens en status berichten versleutelen voordat ze naar het beheer punt worden verzonden. Ze gebruiken de 3DES-algoritme.  

Herhaal deze procedure voor alle primaire sites in de hiërarchie.  



##  <a name="configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a>Op rollen gebaseerd beheer configureren  

Beheer op basis van rollen combineert beveiligingsrollen, beveiligingsbereiken en toegewezen verzamelingen om het beheerbereik te definiëren voor elke gebruiker met beheerdersrechten. Een bereik bevat de objecten die een gebruiker kan weer geven in de-console en de taken die betrekking hebben op deze objecten waarvoor ze machtigingen hebben. Configuraties voor beheer op basis van rollen worden toegepast op elke site in een hiërarchie.  

Zie [op rollen gebaseerd beheer configureren](../../servers/deploy/configure/configure-role-based-administration.md)voor meer informatie. In dit artikel vindt u meer informatie over de volgende acties:  

-  Aangepaste beveiligingsrollen maken  

- Beveiligingsrollen configureren  

- Beveiligingsbereiken voor een object configureren  

- Verzamelingen voor het beheren van beveiliging configureren  

- Een nieuwe gebruiker met beheerdersrechten maken  

- Het beheerbereik van een gebruiker met beheerdersrechten wijzigen  

> [!IMPORTANT]  
>  Uw eigen beheerdersbereik definieert de objecten en instellingen die u kunt toewijzen wanneer u beheer op basis van rollen configureert voor een andere gebruiker met beheerdersrechten. Zie voor meer informatie over het plannen van op rollen gebaseerd beheer de [basis principes van beheer op basis van rollen](../../understand/fundamentals-of-role-based-administration.md).  



##  <a name="manage-accounts-that-configuration-manager-uses"></a><a name="BKMK_ManageAccounts"></a>Accounts beheren die door Configuration Manager worden gebruikt  

Configuration Manager ondersteunt Windows-accounts voor veel verschillende taken en maakt gebruik van. Gebruik de volgende procedure om accounts weer te geven die voor verschillende taken zijn geconfigureerd en om het wacht woord te beheren dat Configuration Manager gebruikt voor elk account:  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Accounts beheren die door Configuration Manager worden gebruikt  

1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **beveiliging**uit en kies vervolgens het knoop punt **accounts** .  

2.  Als u het wacht woord voor een account wilt wijzigen, selecteert u het account in de lijst. Kies vervolgens **Eigenschappen** in het lint.  

3.  Kies **instellen** om het dialoog venster **Windows-gebruikers account** te openen. Geef het nieuwe wacht woord op waarmee Configuration Manager voor dit account moet worden gebruikt.  

    > [!NOTE]  
    >  Het wacht woord dat u opgeeft, moet overeenkomen met het wacht woord van dit account in Active Directory.  

Zie [accounts die worden gebruikt in Configuration Manager](../hierarchy/accounts.md)voor meer informatie.



##  <a name="configure-azure-active-directory"></a><a name="bkmk_azuread"></a>Azure Active Directory configureren

Integreer Configuration Manager met Azure Active Directory (Azure AD) om uw omgeving te vereenvoudigen en in de cloud in te scha kelen. De site en clients in staat stellen om te verifiëren met behulp van Azure AD. Zie voor meer informatie de **Cloud beheer** service in [Azure-Services configureren](../../servers/deploy/configure/azure-services-wizard.md).



## <a name="configure-sms-provider-authentication"></a><a name="bkmk_auth"></a>Verificatie van de SMS-provider configureren

Vanaf versie 1810 kunt u het minimale verificatie niveau voor beheerders opgeven om toegang te krijgen tot Configuration Manager-sites. Deze functie dwingt beheerders af om zich aan te melden bij Windows met het vereiste niveau. Zie [de SMS-provider plannen](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth)voor meer informatie. <!--1357013-->  



## <a name="see-also"></a>Zie ook

- [De beveiliging plannen](plan-for-security.md)  

- [Beveiliging en privacy voor Configuration Manager-clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Communicatie tussen eind punten](../hierarchy/communications-between-endpoints.md)  

- [Technische naslaginformatie voor cryptografische besturingselementen](cryptographic-controls-technical-reference.md)  

- [Vereisten voor PKI-certificaten](../network/pki-certificate-requirements.md)  

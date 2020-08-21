---
title: Vereisten voor sites
titleSuffix: Configuration Manager
description: Meer informatie over vereisten voor het installeren van de verschillende typen Configuration Manager sites.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bf9ad15266c4e6615ba100d5ea5270e23b93ece7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699123"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Vereisten voor het installeren van Configuration Manager-sites

*Van toepassing op: Configuration Manager (huidige vertakking)*

Meer informatie over de vereisten voor het installeren van de verschillende typen Configuration Manager sites vindt u voordat u begint met het installeren van een site.


## <a name="primary-sites-and-the-central-administration-site"></a>Primaire sites en de centrale beheer site

De volgende vereisten zijn van toepassing op het installeren van een van de volgende typen:

- Een centrale beheer site als de eerste site van een hiërarchie
- Een zelfstandige primaire site
- Een onderliggende primaire site

Als u een centrale beheer site wilt installeren als onderdeel van een hiërarchie-uitbrei ding, raadpleegt u [een zelfstandige primaire site uitbreiden](#bkmk_expand).

### <a name="prerequisites-for-installing-a-primary-site-or-a-central-administration-site"></a><a name="bkmk_PrereqPri"></a> Vereisten voor het installeren van een primaire site of een centrale beheer site  

- De benodigde Windows Server-functies,-onderdelen en Windows-onderdelen moeten worden geïnstalleerd. Zie [vereisten voor site systemen](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012sspreq) voor meer informatie.  

- Het gebruikers account waarmee de site wordt geïnstalleerd, moet over de volgende rechten beschikken:  

    - **Beheerder** op de volgende servers:  
        - De site server  
        - Elke server die als host fungeert voor de **site database**  
        - Elk exemplaar van de **SMS-provider** voor de site  

    - **Sysadmin** op het exemplaar van SQL Server dat als host fungeert voor de site database  

        > [!IMPORTANT]  
        > Wanneer Configuration Manager Setup is voltooid, moet het computer account van de site server sysadmin-rechten voor SQL Server behouden. Verwijder de SQL sysadmin-rechten van dit account niet.  

    > [!NOTE]
    > Zie [verhoogde machtigingen](../../../plan-design/hierarchy/accounts.md#elevated-permissions)voor meer informatie over de nood zaak van deze machtigingen nadat de installatie is voltooid.

- Als u een primaire site installeert, hebt u de volgende aanvullende rechten nodig:  

    - **Beheerder** op extra servers waarop u het initiële beheer punt en distributie punt installeert, indien niet op de site server  

- Als u een nieuwe onderliggende primaire site wilt installeren onder een centrale beheer site, hebt u de volgende aanvullende rechten nodig:  

    - **Beheerder** op de server die als host fungeert voor de centrale beheer site  

    - Op rollen gebaseerde beheer rechten binnen Configuration Manager die gelijk zijn aan de beveiligingsrol van **infrastructuur beheerder** of **volledige beheerder**  

- Gebruik de juiste installatie bron bestanden en voer Setup uit vanaf die locatie. Zie [Opties voor het installeren van verschillende typen sites](prepare-to-install-sites.md#bkmk_options)voor meer informatie over de juiste bron bestanden die u kunt gebruiken om verschillende typen sites te installeren.  

- De site server moet toegang hebben tot bijgewerkte Setup-bestanden van micro soft, op een van de volgende manieren:  

    - Voordat u met de installatie begint, moet u een kopie van deze bestanden downloaden en opslaan op uw lokale netwerk. Zie het [Download programma](setup-downloader.md)voor meer informatie.  

    - Als een lokale kopie van dit bestand niet beschikbaar is, moet de site server toegang hebben tot internet. Deze bestanden worden tijdens de installatie van micro soft gedownload.  

- De site server en de site database server moeten voldoen aan alle vereiste configuraties. Voordat u begint met Configuration Manager Setup, voert u de [prerequisite Checker hand matig uit](prerequisite-checker.md) om problemen te identificeren en op te lossen.  

### <a name="prerequisites-to-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Vereisten voor het uitbreiden van een zelfstandige primaire site

Een zelfstandige primaire site moet voldoen aan de volgende vereisten voordat u deze kunt uitbreiden naar een hiërarchie met een centrale beheer site:

#### <a name="source-file-version-matches-site-version"></a>Versie van bron bestand komt overeen met site versie

Installeer de nieuwe centrale beheer site met media vanaf een CD. De meest recente map die overeenkomt met de versie van de zelfstandige primaire site. Gebruik de bron bestanden in de cd om ervoor te zorgen dat de versies overeenkomen [. Meest recente map](../../manage/the-cd.latest-folder.md) op de zelfstandige primaire site.

Zie [Opties voor het installeren van verschillende typen sites](prepare-to-install-sites.md#bkmk_options)voor meer informatie over de juiste bron bestanden die u kunt gebruiken om verschillende sites te installeren.  

#### <a name="stop-active-migration-from-another-hierarchy"></a>De actieve migratie van een andere hiërarchie stoppen

U kunt de zelfstandige primaire site niet configureren om gegevens van een andere Configuration Manager-hiërarchie te migreren. Stop de actieve migratie naar de zelfstandige primaire site vanuit andere Configuration Manager-hiërarchieën en verwijder alle configuraties voor migratie. Deze configuraties zijn onder andere:

- Migratie taken die nog niet zijn voltooid  
- Gegevens verzamelen  
- De configuratie van de actieve bron hiërarchie  

Deze configuratie is nood zakelijk omdat Configuration Manager gegevens migreert van de site op het hoogste niveau van de hiërarchie. Wanneer u een zelfstandige primaire site uitbreidt, worden de configuraties voor migratie niet overgedragen naar de centrale beheer site.  

Wanneer u de zelfstandige primaire site uitbreidt en u de migratie op de primaire site opnieuw configureert, worden de migratie bewerkingen uitgevoerd op de centrale beheer site.

Zie voor meer informatie over het configureren van de migratie [bron hiërarchieën en bron sites configureren voor migratie](../../../migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

#### <a name="computer-account-as-administrator"></a>Computer account als beheerder

Het computer account van de server die als host fungeert voor de nieuwe centrale beheer site moet lid zijn van de groep **Administrators** op de zelfstandige primaire site server.

Om de zelfstandige primaire site uit te breiden, moet het computer account van de nieuwe centrale beheer site over **beheerders** rechten beschikken voor de zelfstandige primaire site. Dit is alleen vereist tijdens de site-uitbrei ding. Wanneer de site-uitbrei ding is voltooid, kunt u het account uit de gebruikers groep op de primaire site verwijderen.  

#### <a name="installation-account-permissions"></a>Machtigingen voor het installatie account

Het gebruikers account dat Configuration Manager Setup uitvoert om de nieuwe centrale beheer site te installeren, moet op rollen gebaseerde beheer rechten hebben op de zelfstandige primaire site.

Als u een centrale beheer site wilt installeren als onderdeel van een site-uitbrei ding, moet het gebruikers account dat Setup uitvoert om de centrale beheer site te installeren, worden gedefinieerd in op rollen gebaseerd beheer op de zelfstandige primaire site als ofwel een **volledige beheerder** of een **infrastructuur beheerder**zijn.

Zie [site-installatie account](../../../plan-design/hierarchy/accounts.md#site-installation-account)voor meer informatie, waaronder de volledige lijst met vereiste machtigingen.

#### <a name="top-level-site-roles"></a>Site rollen op het hoogste niveau

Voordat u de site uitbreidt, verwijdert u de volgende site systeem rollen van de zelfstandige primaire site:

- Asset Intelligence synchronisatie punt  
- Endpoint Protection-punt  
- Serviceverbindingspunt  

Configuration Manager ondersteunt alleen deze rollen op de site op het hoogste niveau van de hiërarchie. Verwijder deze site systeem rollen voordat u de zelfstandige primaire site uitbreidt. Nadat u de site hebt uitgebreid, installeert u deze site systeem rollen opnieuw op de centrale beheer site.  

Alle andere site systeem rollen kunnen geïnstalleerd blijven op de primaire site.  

#### <a name="open-the-sql-server-service-broker-port"></a>Open de SQL Server Service Broker poort

De netwerk poort moet open zijn voor de SQL Server Service Broker (SSB) tussen de zelfstandige primaire site en de server voor de centrale beheer site.  

Als u gegevens wilt repliceren tussen een centrale beheer site en een primaire site, moet Configuration Manager een open poort hebben tussen de twee sites voor het gebruik van SSB. Wanneer u een centrale beheer site installeert en een zelfstandige primaire site uitbreidt, wordt door de controle op vereisten niet gecontroleerd of de poort die u voor de SSB opgeeft, open is op de primaire site.  

#### <a name="known-issues-with-azure-services"></a>Bekende problemen met Azure-Services

Nadat u de site hebt uitgebreid, moet u de volgende Azure-Services opnieuw configureren met Configuration Manager:

- [Log Analytics](/azure/azure-monitor/platform/collect-sccm)  
- [Microsoft Store voor bedrijven](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  
- [Cloudbeheergateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

De eenvoudigste methode is het vernieuwen van de geheime sleutel van de Azure Active Directory-Tenant. Zie [geheime sleutel vernieuwen](../configure/azure-services-wizard.md#bkmk_renew)voor meer informatie.

U kunt ook de verbinding met die service verwijderen en opnieuw maken:

1. In de Configuration Manager-console verwijdert u de Azure-service uit het knoop punt **Azure-Services** .  

2. In de Azure Portal verwijdert u de Tenant die is gekoppeld aan de service vanuit het knoop punt Azure Active Directory tenants. Met deze actie wordt ook de Azure AD-web-app verwijderd die is gekoppeld aan de service.  

3. Configureer de verbinding met de Azure-service opnieuw voor gebruik met Configuration Manager.  


## <a name="secondary-sites"></a><a name="bkmk_secondary"></a> Secundaire sites

Hier volgen de vereisten voor het installeren van secundaire sites:  

- De benodigde Windows Server-functies,-onderdelen en Windows-onderdelen moeten worden geïnstalleerd. Zie [vereisten voor site systemen](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012secpreq) voor meer informatie.  

- De beheerder die de installatie van de secundaire site configureert in de Configuration Manager-console moet beschikken over op rollen gebaseerde beheer rechten die gelijk zijn aan de beveiligingsrol van **infrastructuur beheerder** of **volledige beheerder**.  

- Het computer account van de bovenliggende primaire site moet een **beheerder** zijn op de secundaire site server.  

- Wanneer de secundaire site een eerder geïnstalleerd exemplaar van SQL Server gebruikt voor het hosten van de data base van de secundaire site:  

    - Het computer account van de bovenliggende primaire site moet over **sysadmin** -rechten beschikken voor het exemplaar van SQL Server op de secundaire site server.  

    - Het **lokale systeem** account van de secundaire site Server computer moet over **sysadmin** -rechten beschikken voor het exemplaar van SQL Server op de secundaire site server.  

        > [!IMPORTANT]  
        > Wanneer Configuration Manager Setup is voltooid, moeten beide accounts sysadmin-rechten behouden voor SQL Server. Verwijder de sysadmin-rechten niet uit deze accounts.  

- De secundaire site server moet voldoen aan alle vereiste configuraties. Deze configuraties omvatten SQL Server en de standaard site systeem rollen van het beheer punt en distributie punt.  


## <a name="next-steps"></a>Volgende stappen

Nadat u de vereisten hebt bevestigd, bent u klaar om Setup uit te voeren. Zie [de installatie wizard gebruiken om Configuration Manager-sites te installeren](use-the-setup-wizard-to-install-sites.md)voor meer informatie.
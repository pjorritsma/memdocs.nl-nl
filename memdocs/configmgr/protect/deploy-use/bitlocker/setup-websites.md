---
title: BitLocker-portals instellen
titleSuffix: Configuration Manager
description: De BitLocker-beheer onderdelen voor de Self-Service Portal en de beheer-en bewakings website installeren
ms.date: 09/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6834090cd2a58113fb26e298c0c451f846f5ce9
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574589"
---
# <a name="set-up-bitlocker-portals"></a>BitLocker-portals instellen

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3601034-->

Als u de volgende BitLocker-beheer onderdelen in Configuration Manager wilt gebruiken, moet u deze eerst installeren:

- Self-Service Portal voor gebruikers
- Website voor beheer en controle (helpdesk Portal)

U kunt de portals installeren op een bestaande site server of site systeem server waarop IIS is geïnstalleerd, of een zelfstandige webserver gebruiken om ze te hosten.

> [!NOTE]
> Vanaf versie 2006 kunt u de BitLocker Self-Service Portal en de beheer-en bewakings website op de centrale beheer site installeren.<!-- 5925693 -->
>
> In versie 2002 en eerder installeert u alleen de Self-Service Portal en de beheer-en bewakings website met een primaire site database. Installeer deze websites voor elke primaire site in een hiërarchie.

Voordat u begint, moet u de [vereisten](../../plan-design/bitlocker-management.md#prerequisites) voor deze onderdelen bevestigen.

## <a name="run-the-script"></a>Het script uitvoeren

Voer op de doel webserver de volgende acties uit:

> [!NOTE]
> Afhankelijk van het ontwerp van uw site moet u het script mogelijk meerdere keren uitvoeren. Voer bijvoorbeeld het script uit op het beheer punt om de website beheer en controle te installeren. Voer de agent vervolgens opnieuw uit op een zelfstandige webserver om de Self-Service Portal te installeren.

1. Kopieer de volgende bestanden vanuit `SMSSETUP\BIN\X64` de installatiemap Configuration Manager op de site server naar een lokale map op de doel server:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. Voer Power shell uit als beheerder en voer het script uit dat vergelijkbaar is met de volgende opdracht regel:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    Bijvoorbeeld:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > In dit voor beeld wordt gebruikgemaakt van alle mogelijke para meters om het gebruik ervan weer te geven. Pas uw gebruik aan volgens uw vereisten in uw omgeving.

Na de installatie krijgt u toegang tot de portals via de volgende Url's:

- Self-Service Portal: `https://webserver.contoso.com/SelfService`
- Beheer-en bewakings website: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Micro soft raadt u aan, maar het gebruik van HTTPS is niet vereist. Zie [SSL instellen in IIS](/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)voor meer informatie.

## <a name="script-usage"></a>Script gebruik

Dit proces maakt gebruik van een Power shell-script, MBAMWebSiteInstaller.ps1, om deze onderdelen te installeren op de webserver. Het accepteert de volgende para meters:

- `-SqlServerName <ServerName>` (vereist): de Fully Qualified Domain Name van de database server van de primaire site.

- `-SqlInstanceName <InstanceName>`: De SQL Server exemplaar naam voor de data base van de primaire site. Als SQL het standaard exemplaar gebruikt, neemt u deze para meter niet op.

- `-SqlDatabaseName <DatabaseName>` (vereist): de naam van de data base van de primaire site, bijvoorbeeld `CM_ABC` .

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: De URL van de webservice van het Reporting service-punt van de primaire site. Dit is de **URL** van de webservice in **Reporting Services Configuration Manager**.

    > [!NOTE]
    > Met deze para meter wordt het **herstel controle rapport** geïnstalleerd dat is gekoppeld via de website beheer en controle. Standaard Configuration Manager de andere BitLocker-beheer rapporten bevat.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: Bijvoorbeeld `contoso\BitLocker help desk users` . Een domein gebruikers groep waarvan de leden toegang hebben tot de modules TPM en **stations herstellen** **beheren** van de website beheer en controle. Wanneer u deze opties gebruikt, moet deze rol alle velden invullen, met inbegrip van het domein en de account naam van de gebruiker.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: Bijvoorbeeld `contoso\BitLocker help desk admins` . Een domein gebruikers groep waarvan de leden toegang hebben tot alle herstel gebieden van de beheer-en bewakings website. Wanneer gebruikers helpen hun stations te herstellen, hoeft deze rol alleen de herstel sleutel in te voeren.

- `-MbamReportUsersGroupName <DomainUserGroup>`: Bijvoorbeeld `contoso\BitLocker report users` . Een domein gebruikers groep waarvan de leden alleen-lezen toegang hebben tot het gebied **rapporten** van de website beheer en controle.

    > [!NOTE]
    > Het installatie script maakt geen domein gebruikers groepen die u opgeeft in de para meters **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**en **-MbamReportUsersGroupName** . Voordat u het script uitvoert, moet u ervoor zorgen dat u deze groepen maakt.
    >
    > Wanneer u de para meters **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**en **-MbamReportUsersGroupName** opgeeft, moet u de domein naam en de groeps naam opgeven. Gebruik de indeling `"domain\user_group"`. Sluit de domein naam niet uit. Als de domein naam of de groeps naam spaties of speciale tekens bevat, plaatst u de para meter tussen aanhalings tekens ( `"` ).

- `-SiteInstall Both`: Geef op welke onderdelen moeten worden geïnstalleerd. Geldige opties zijn:
  - `Both`: Installeer beide onderdelen
  - `HelpDesk`: Alleen de beheer-en bewakings website installeren
  - `SSP`: Alleen de Self-Service Portal installeren

- `-IISWebSite`: De website waarop het script de MBAM-webtoepassingen installeert. Standaard wordt de IIS-standaard website gebruikt. Maak de aangepaste website voordat u deze para meter gebruikt.

- `-InstallDirectory`: Het pad waarin het script de Web-toepassings bestanden installeert. Dit pad is standaard `C:\inetpub` . Maak de aangepaste map voordat u deze para meter gebruikt.

- `-DomainName`*is van toepassing op versie 2002 en hoger*: Geef de NetBIOS-domein naam van de server op met de Help Desk of selfservice Web Portal Role. Alleen vereist als de NetBIOS-domein naam niet overeenkomt met de DNS-domein naam. Deze configuratie wordt ook wel een niet-aaneengesloten domein naam ruimte genoemd. Bijvoorbeeld, `-DomainName fabrikham` waarbij de DNS-domein naam is `contoso.com` .<!-- MEMDocs #759 -->

- `-Uninstall`: Hiermee verwijdert u de BitLocker Management Help Desk/self-service portal sites op een webserver waarop ze eerder zijn geïnstalleerd.

## <a name="verify"></a>Verifiëren

Controleren en problemen oplossen met behulp van de volgende logboeken:

- Windows-gebeurtenis Logboeken onder **micro soft-Windows-MBAM-Web**. Zie [informatie over BitLocker-gebeurtenis logboeken](../../tech-ref/bitlocker/about-event-logs.md) en [server gebeurtenis logboeken](../../tech-ref/bitlocker/server-event-logs.md)voor meer informatie.

- Traceer logboeken voor elk onderdeel bevinden zich op de volgende standaard locaties:

  - Self-Service Portal: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Beheer-en bewakings website: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

Zie [problemen met BitLocker oplossen](../../tech-ref/bitlocker/troubleshoot.md)voor meer informatie over probleem oplossing.

## <a name="next-steps"></a>Volgende stappen

[Selfservice portal implementeren](customize-self-service-portal.md)

Raadpleeg de volgende artikelen voor meer informatie over het gebruik van de onderdelen die u hebt geïnstalleerd:

- [Website voor BitLocker-beheer en-bewaking](helpdesk-portal.md)
- [BitLocker Self-Service Portal](self-service-portal.md)

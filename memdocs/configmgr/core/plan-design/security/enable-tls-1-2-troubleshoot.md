---
title: Veelvoorkomende problemen bij het inschakelen van Transport Layer Security (TLS) 1,2
titleSuffix: Configuration Manager
description: Hierin worden veelvoorkomende problemen beschreven bij het inschakelen van Transport Layer Security (TLS) 1,2
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c07b0af1b3063619ac5f71965d96f611aefafd9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720525"
---
# <a name="common-issues-when-enabling-tls-12"></a>Algemene problemen bij het inschakelen van TLS 1.2

In dit artikel vindt u adviezen voor veelvoorkomende problemen die zich voordoen wanneer u TLS 1,2-ondersteuning inschakelt in Configuration Manager.

## <a name="unsupported-platforms"></a>Niet-ondersteunde platforms

De volgende client platforms worden ondersteund door Configuration Manager, maar worden niet ondersteund in een TLS 1,2-omgeving:

- Windows CE
- Apple OS X
- Windows 10-apparaten die worden beheerd met on-premises MDM

## <a name="reports-dont-show-in-the-console"></a>Rapporten worden niet weer gegeven in de console

Als rapporten niet worden weer gegeven in de Configuration Manager-console, moet u ervoor zorgen dat u de computer waarop de-console wordt uitgevoerd, bijwerkt. [Werk de .NET Framework](enable-tls-1-2-client.md#bkmk_net)bij en schakel sterke crypto grafie in.

## <a name="fips-security-policy-enabled"></a>FIPS-beveiligings beleid ingeschakeld

Als u de instelling voor het FIPS-beveiligings beleid voor de client of een server inschakelt, kan de onderhandeling door een beveiligd kanaal (Schannel) ervoor zorgen dat ze TLS 1,0 gebruiken. Dit gedrag treedt zelfs op als u het protocol in het REGI ster uitschakelt.

Als u wilt onderzoeken, schakelt u logboek registratie van beveiligde kanalen in en bekijkt u Schannel-gebeurtenissen in het systeem logboek. Zie [het gebruik van bepaalde cryptografische algoritmen en protocollen in Schannel. dll beperken](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc)voor meer informatie.

## <a name="sql-server-communication-failure"></a>Communicatie fout SQL Server

Als SQL Server communicatie mislukt en een **SslSecurityError** -fout retourneert, controleert u de volgende instellingen:

- [.NET Framework bijwerken](enable-tls-1-2-server.md#bkmk_net)en sterke crypto grafie op elke computer inschakelen
- [SQL Server](enable-tls-1-2-server.md#bkmk_sql) op de hostserver bijwerken
- [Werk SQL-Client onderdelen](enable-tls-1-2-server.md#bkmk_sql-client) bij op alle systemen die met SQL communiceren. Bijvoorbeeld de site servers, SMS-provider en siterol servers.

## <a name="configuration-manager-client-communication-failures"></a>Client communicatie fouten Configuration Manager

Als de Configuration Manager-client niet communiceert met site rollen, controleert u of u [Windows hebt bijgewerkt](enable-tls-1-2-client.md#bkmk_winhttp) ter ondersteuning van TLS 1,2 voor client-server communicatie met behulp van WinHTTP. Algemene site rollen zijn onder andere distributie punten, beheer punten en status migratie punten.

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Reporting Services-punt mislukt en retourneert een verwachte fout

Als het Reporting Services-punt geen rapporten configureert, controleert u het **SRSRP. log** op de volgende fout vermelding:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Volg deze stappen om dit probleem op te lossen:

1. [Werk .NET Framework](enable-tls-1-2-client.md#bkmk_net)bij en schakel sterke crypto grafie in op alle relevante computers.

1. Nadat u de updates hebt geïnstalleerd, start u de SMS_Executive-service opnieuw.

## <a name="application-catalog-doesnt-initialize"></a>Application Catalog wordt niet geïnitialiseerd

> [!Important]  
> Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [verwijderde en afgeschafte functies](../changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.

Als de toepassings catalogus niet wordt geïnitialiseerd, controleert u het bestand **ServicePortalWebSite. svclog** voor de volgende fout vermelding:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Volg deze stappen om dit probleem op te lossen:

1. [Werk .NET Framework](enable-tls-1-2-client.md#bkmk_net)bij en schakel sterke crypto grafie in op alle relevante computers.

1. Maak in `%WinDir%\System32\InetSrv` de map van de Application Catalog-server een bestand **W2SP. exe. config** met de volgende inhoud:

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Dit bestand is het standaard bestand dat wordt gemaakt als de toepassing is gebouwd met behulp van .NET Framework 4.6.3.

1. HTTPS-transport beveiliging gebruiken voor Application Catalog-rollen.

    > [!Important]
    > Wanneer u HTTP-bericht beveiliging voor Application Catalog-rollen gebruikt, wordt WCF hard gecodeerd voor het gebruik van SSL 3,0 en TLS 1,0. Dit voor komt het gebruik van TLS 1,2.

1. Als u wijzigingen hebt aangebracht, start u de computer opnieuw op.

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>Software Center of browser communiceert niet met de toepassings catalogus

> [!Important]  
> Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [verwijderde en afgeschafte functies](../changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.

De beste manier om software Center te laten werken met voor gebruikers beschik bare apps in een TLS 1,2-ingeschakelde site, verwijdert u de rol Application Catalog. Laat Software Center vervolgens rechtstreeks communiceren met een beheer punt. Zie [de Application Catalog verwijderen](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)voor meer informatie.

Als u communicatie fouten tussen de Application Catalog en het Software Center moet oplossen, controleert u de volgende voor waarden:

- [.NET Framework bijwerken](enable-tls-1-2-client.md#bkmk_net)en sterke crypto grafie op elke computer inschakelen.

- Nadat u de wijzigingen hebt aangebracht, start u alle betreffende computers opnieuw op.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>Upload fouten van het service verbindings punt

Als het service verbindings punt geen gegevens uploadt naar SCCMConnectedService, [werkt u de .NET Framework](enable-tls-1-2-server.md#bkmk_net)bij en schakelt u sterke crypto grafie in op elke computer. Nadat u de wijzigingen hebt aangebracht, moet u de computers opnieuw opstarten.

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Configuration Manager-console geeft het dialoog venster intune-onboarding weer

Als het dialoog venster intune-onboarding wordt weer gegeven wanneer de console verbinding probeert te maken met de intune-Portal, moet u [de .NET Framework bijwerken](enable-tls-1-2-client.md#bkmk_net)en sterke crypto grafie op elke computer inschakelen. Nadat u de wijzigingen hebt aangebracht, moet u de computers opnieuw opstarten.

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Configuration Manager-console geeft aan dat het aanmelden bij Azure niet is geslaagd

Wanneer u probeert toepassingen te maken in Azure Active Directory (Azure AD), wordt het dialoog venster voor de onboarding van Azure-Services onmiddellijk niet meer uitgevoerd nadat u aanmelden hebt geselecteerd, [de .NET Framework](enable-tls-1-2-server.md#bkmk_net) **bij**te werken en sterke crypto grafie in te scha kelen. Nadat u de wijzigingen hebt aangebracht, moet u de computers opnieuw opstarten.

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Configuration Manager Cloud Services en TLS 1,2

De virtuele machines van Azure die worden gebruikt door de Cloud beheer gateway en Cloud distributiepunten ondersteunen TLS 1,2. Ondersteunde client versies gebruiken automatisch TLS 1,2.

**SMSAdminui. log** kan een fout bevatten die vergelijkbaar is met het volgende voor beeld:

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

In het gebeurtenis logboek van het systeem kan SChannel-gebeurtenis-36874 worden geregistreerd met de volgende beschrijving:`An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>Aanvullende bronnen

- [Aanbevolen procedures voor trans port Layer Security (TLS) met de .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: TLS 1,2-ondersteuning voor Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [Technische naslaginformatie voor cryptografische besturingselementen](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>Volgende stappen

- [TLS 1.2 inschakelen op clients](enable-tls-1-2-client.md)
- [TLS 1,2 inschakelen op de site servers en externe site systemen](enable-tls-1-2-server.md)


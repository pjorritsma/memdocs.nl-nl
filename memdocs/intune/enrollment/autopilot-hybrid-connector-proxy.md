---
title: Proxyinstellingen configureren voor de Intune Connector voor Active Directory
description: Hierin leest u hoe u de Intune Connector voor Active Directory moet configureren om te gebruiken in combinatie met bestaande on-premises proxyservers.
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tanvira
ms.suite: ems
search.appverid: ''
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 227ed78b593ce10d47b9a1cdcc14dfbd58acdd93
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "79339511"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Werken met bestaande on-premises proxyservers

In dit artikel wordt uitgelegd hoe u de Intune Connector voor Active Directory configureert zodat u met uitgaande proxyservers kunt werken. Het is bedoeld voor klanten met netwerkomgevingen met bestaande proxy's.

De Intune-connector voor Active Directory probeert standaard automatisch een proxyserver in het netwerk te zoeken met behulp van Web Proxy Auto-Discovery (WPAD). Als dit in uw netwerk is geconfigureerd, is er mogelijk geen aanvullende configuratie vereist.  Als er wijzigingen nodig zijn, wordt in de volgende secties beschreven hoe u de standaardinstellingen overschrijft, gebruikmakend van [de standaard .NET Framework-mogelijkheden voor het configureren van proxy-instellingen](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).  In deze documentatie worden extra opties beschreven.

Zie [Meer informatie over Azure AD-toepassingsproxyconnectoren](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors) voor meer informatie over de werking van connectoren.

## <a name="completely-bypass-outbound-proxies"></a>Uitgaande proxy's volledig overslaan

U kunt de connector configureren om uw on-premises proxy over te slaan, zodat u zeker weet dat de connector rechtstreeks is verbonden met de Azure-services. Dit is de aanbevolen methode zolang deze mogelijk is volgens uw netwerkbeleid, omdat u in dit geval één configuratie minder hoeft te onderhouden.

Als u het proxygebruik voor de connector wilt uitschakelen, bewerkt u het bestand :\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config en voegt u het proxyadres en de proxypoort toe in het deel dat in dit codevoorbeeld wordt weergegeven:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

U moet een vergelijkbare wijziging doorvoeren in het bestand C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config om ervoor te zorgen dat ook de Connector Updater-service de proxy overslaat.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Vergeet niet om kopieën van de oorspronkelijke bestanden te maken, in het geval u de .config-bestanden naar de standaardinstellingen moet terugzetten.

Zodra de configuratiebestanden zijn aangepast, moet u de Intune-connectorservice opnieuw opstarten. 

1. Open **services.msc**.
2. Zoek en selecteer de **Intune ODJConnector-service**.
3. Selecteer **Opnieuw opstarten**.

![Schermopname van het opnieuw opstarten van de service](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>Een alternatieve proxyserver opgeven

Als een andere proxyserver (bijvoorbeeld een die verificatie overslaat) moet worden gebruikt met de Intune-connector voor Active Directory, kan dit op een vergelijkbare manier worden opgegeven. Hiertoe bewerkt u het bestand :\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config en voegt u het proxyadres en de proxypoort toe in het deel dat in dit codevoorbeeld wordt weergegeven:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

U moet een vergelijkbare wijziging doorvoeren in het bestand C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config om ervoor te zorgen dat ook de Connector Updater-service de proxy overslaat.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Vergeet niet om kopieën van de oorspronkelijke bestanden te maken, in het geval u de .config-bestanden naar de standaardinstellingen moet terugzetten.

Zodra de configuratiebestanden zijn aangepast, moet u de Intune-connectorservice opnieuw opstarten. 

1. Open **services.msc**.
2. Zoek en selecteer de **Intune ODJConnector-service**.
3. Selecteer **Opnieuw opstarten**.

![Schermopname van het opnieuw opstarten van de service](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>Volgende stappen

[Uw apparaten beheren](../remote-actions/device-management.md)

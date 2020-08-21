---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 0f91860ad591e20c6f199e098a8c957f50294386
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704500"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>.NET-versie bepalen

Bepaal eerst welke .NET-versies zijn geïnstalleerd. Zie [bepalen welke versies en Service Pack niveaus van het Microsoft .NET Framework zijn geïnstalleerd](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso)voor meer informatie.

### <a name="install-net-updates"></a>.NET-updates installeren

Installeer de .NET-updates zodat u sterke crypto grafie kunt inschakelen. Voor sommige versies van .NET Framework zijn mogelijk updates vereist om sterke crypto grafie mogelijk te maken. Gebruik deze richt lijnen:

- NET Framework 4.6.2 en hoger ondersteunt TLS 1,1 en TLS 1,2. Bevestig de Register instellingen, maar u hoeft geen verdere wijzigingen aan te brengen.

- Werk NET Framework 4,6 en eerdere versies bij om TLS 1,1 en TLS 1,2 te ondersteunen. Zie [.NET Framework versies en afhankelijkheden](/dotnet/framework/migration-guide/versions-and-dependencies)voor meer informatie.

- Als u .NET Framework 4.5.1 of 4.5.2 gebruikt in Windows 8,1 of Windows Server 2012, zijn de relevante updates en details ook beschikbaar in het [Download centrum](https://www.microsoft.com/download/details.aspx?id=42883).


### <a name="configure-for-strong-cryptography"></a>Configureren voor sterke crypto grafie

Configureer .NET Framework ter ondersteuning van sterke crypto grafie. Stel de `SchUseStrongCrypto` register instelling in op `DWORD:00000001` . Met deze waarde wordt de RC4-stroom versleuteling uitgeschakeld en moet de computer opnieuw worden opgestart. Zie [micro soft security advisory 296038](/security-updates/SecurityAdvisories/2015/2960358)(Engelstalig) voor meer informatie over deze instelling.

Zorg ervoor dat u de volgende register sleutels instelt op elke computer die communiceert via het netwerk met een TLS 1,2-systeem. Bijvoorbeeld Configuration Manager-clients, systeem rollen van externe sites die niet zijn geïnstalleerd op de site server en de site server zelf.

Voor 32-bits toepassingen die worden uitgevoerd op 32-bits OSs en voor 64-bits toepassingen die worden uitgevoerd op 64-bits OSs, werkt u de volgende subsleutel waarden bij:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

Voor 32-bits toepassingen die worden uitgevoerd op 64-bits OSs, werkt u de volgende subsleutel waarden bij:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> `SchUseStrongCrypto`Met deze instelling kan .net TLS 1,1 en tls 1,2 gebruiken. `SystemDefaultTlsVersions`Met deze instelling kan .net de configuratie van het besturings systeem gebruiken. Zie [Aanbevolen procedures voor TLS met de .NET Framework](/dotnet/framework/network-programming/tls)voor meer informatie.
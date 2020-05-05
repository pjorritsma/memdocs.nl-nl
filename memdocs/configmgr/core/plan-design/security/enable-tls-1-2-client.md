---
title: Transport Layer Security (TLS) 1,2 op clients inschakelen
titleSuffix: Configuration Manager
description: Informatie over het inschakelen van TLS 1,2 voor Configuration Manager-clients.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720553"
---
# <a name="how-to-enable-tls-12-on-clients"></a>TLS 1,2 op clients inschakelen

*Van toepassing op: Configuration Manager (Current Branch)*

Wanneer u TLS 1,2 inschakelt voor uw Configuration Manager-omgeving, moet u eerst controleren of de clients geschikt zijn en op de juiste wijze zijn geconfigureerd voor het gebruik van TLS 1,2 voordat TLS 1,2 wordt ingeschakeld en de oudere protocollen op de site servers en externe site systemen worden uitgeschakeld. Er zijn drie taken voor het inschakelen van TLS 1,2 op clients:

- Windows en WinHTTP bijwerken
- Zorg ervoor dat TLS 1,2 is ingeschakeld als een protocol voor SChannel op het niveau van het besturings systeem
- De .NET Framework bijwerken en configureren ter ondersteuning van TLS 1,2

Zie [about TLS 1,2](enable-tls-1-2.md)(Engelstalig) voor meer informatie over afhankelijkheden voor specifieke Configuration Manager-functies en-scenario's.

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a>Windows en WinHTTP bijwerken

Windows 8,1, Windows Server 2012 R2, Windows 10, Windows Server 2016 en latere versies van Windows ondersteunen TLS 1,2 voor client-server communicatie via WinHTTP. 

Eerdere versies van Windows, zoals Windows 7 of Windows Server 2012, maken TLS 1,1 of TLS 1,2 niet standaard voor beveiligde communicatie met WinHTTP. Voor deze eerdere versies van Windows installeert u [Update 3140245](https://support.microsoft.com/help/3140245) om de onderstaande register waarde in te scha kelen, die kan worden ingesteld om TLS 1,1 en TLS 1,2 toe te voegen aan de lijst met beveiligde standaard protocollen voor WinHTTP. Wanneer de patch is geïnstalleerd, maakt u de volgende register waarden:

> [!IMPORTANT]
> Schakel deze instellingen in op alle clients met eerdere versies van Windows *voordat* u TLS 1,2 inschakelt en de oudere protocollen op de Configuration Manager servers uitschakelt. Als dat niet het geval is, kunt u ze per ongeluk zweven.

Controleer de waarde van de `DefaultSecureProtocols` register instelling, bijvoorbeeld:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Als u deze waarde wijzigt, start u de computer opnieuw op.

In het bovenstaande voor beeld ziet u `0xAA0` de waarde van `DefaultSecureProtocols` voor de WinHTTP-instelling. [KB 3140245: bijwerken om tls 1,1 en tls 1,2 in te scha kelen als beveiligde protocollen die standaard worden beveiligd in WinHTTP in Windows](https://support.microsoft.com/help/3140245) bevat de hexadecimale waarde voor elk protocol. In Windows is `0x0A0` deze waarde standaard om SSL 3,0 en TLS 1,0 voor WinHTTP in te scha kelen. In het bovenstaande voor beeld worden deze standaard waarden behouden en wordt TLS 1,1 en TLS 1,2 voor WinHTTP ingeschakeld. Deze configuratie zorgt ervoor dat de wijziging geen andere toepassing verbreekt die mogelijk nog steeds afhankelijk is van SSL 3,0 of TLS 1,0. U kunt de waarde van `0xA00` gebruiken om alleen TLS 1,1 en TLS 1,2 in te scha kelen. Configuration Manager ondersteunt het veiligste protocol dat door Windows wordt onderhandeld tussen beide apparaten.

 Als u SSL 3,0 en TLS 1,0 volledig wilt uitschakelen, gebruikt u de instelling SChannel-uitgeschakelde protocollen in Windows. Zie [het gebruik van bepaalde cryptografische algoritmen en protocollen in Schannel. dll beperken](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc)voor meer informatie.

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a>Zorg ervoor dat TLS 1,2 is ingeschakeld als een protocol voor SChannel op het niveau van het besturings systeem

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a>De .NET Framework bijwerken en configureren ter ondersteuning van TLS 1,2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>Volgende stappen

- [TLS 1,2 inschakelen op de site servers en externe site systemen](enable-tls-1-2-server.md)
- [Algemene problemen bij het inschakelen van TLS 1.2](enable-tls-1-2-troubleshoot.md)


---
title: Algemene fouten voor Intune Exchange Connector oplossen
titleSuffix: Microsoft Intune
description: Problemen oplossen en algemene fouten oplossen voor de on-premises Microsoft Intune Exchange Connector
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cea8981b9fdd16e0d8da9dd36445b8fbdfe3d53f
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193943"
---
# <a name="resolve-common-errors-for-the-intune-exchange-connector"></a>Algemene fouten voor Intune Exchange Connector oplossen

Intune-beheerders kunnen aan de hand van dit artikel specifieke fouten oplossen en berichten ontvangen over de werking van Intune Exchange Connector.  

## <a name="configuration-failed-and-returned-error-code-0x0000001"></a>Configuratie is mislukt en foutcode 0x0000001 is geretourneerd

**Probleem**:  
Tijdens het configureren van Microsoft Intune Exchange Connector ontvangt u het volgende foutbericht:

```
   The Microsoft Intune Exchange Connector cannot connect to the Microsoft Exchange server.  
   The following Microsoft Exchange Server address could not be reached <Exchange server Name FQDN>  
   Verify that the FQDN of the exchange server address and credentials that you entered is correct and the server is running. The Microsoft Intune Exchange Connector does not support Exchange server arrays.  
   Error code: 0x0000001  
```

Dit probleem kan zich voordoen als internetproxy-instellingen niet goed zijn geconfigureerd.

**Oplossing**:  
Proxy-instellingen configureren
1. Neem contact op met de lokale netwerkbeheerder om te controleren of de proxy-instellingen goed zijn geconfigureerd. 
2. Gebruik de opdracht **Netsh winhttp** om de proxyserver te configureren en de vereiste lijst met uitzonderingen toe te voegen. Bijvoorbeeld:  

   ```
   Netsh winhttp set proxy proxy-server="http=proxy.corp.domain.com" bypass-list"34*.*;134.132.*.*;10.*.*;localhost;*.corp.domain.com;*.staging.domain.com"
   ```

## <a name="configuration-failed-and-returned-error-code-0x000000b"></a>Configuratie mislukt en foutcode 0x000000b is geretourneerd   

**Probleem**:  
Tijdens het configureren van Microsoft Intune Exchange Connector ontvangt u het volgende foutbericht:  

```
   The Microsoft Intune Exchange Connector experienced an error:  
   CertEnroll::CX509PrivateKey::Create: The system cannot find the file specified. 0x80070002 (WIN32: 2  
   ERROR_FILE_NOT_FOUND  
   Error code: 0x000000b  
```
Dit probleem kan zich voordoen als het account dat u hebt gebruikt om u bij Intune aan te melden geen globaal Intune-beheerdersaccount is.

**Oplossing**:  
Meld u aan bij Intune met een globaal beheerdersaccount of voeg uw account toe aan de groep Globale beheerder. Zie [Op rollen gebaseerd toegangsbeheer (RBAC) met Microsoft Intune](../fundamentals/role-based-access-control.md) voor meer informatie.

## <a name="configuration-failed-and-returned-error-code-0x0000006"></a>Configuratie mislukt en foutcode 0x0000006 is geretourneerd

**Probleem**:  
Tijdens het configureren van Microsoft Intune Exchange Connector ontvangt u het volgende foutbericht:  

```  
   The Microsoft Intune Exchange Connector cannot connect to Microsoft Intune  
   Verify that you are connected to the Internet, check the Microsoft Intune Service Status, and try to connect again.  
   Error code: 0x00000006  
```  
Deze fout kan zich voordoen als een proxyserver wordt gebruikt om verbinding te maken met internet en verkeer naar de Intune-service wordt geblokkeerd. Ga naar **Configuratiescherm** > **Internetopties**, selecteer het tabblad **Verbinding** en klik vervolgens op **LAN-instellingen** om te bepalen of er een proxy wordt gebruikt.

**Oplossing**:  

- **Optie 1**: verwijder de proxy-instellingen zodat de computer verbinding kan maken met internet zonder via de proxy te lopen.  

- **Optie 2**: configureer uw proxyserver zodat communicatie met de Intune-service is toegestaan, zoals u kunt lezen bij de [Intune Exchange Connector-vereisten](exchange-connector-install.md#intune-exchange-connector-requirements).



## <a name="event-7000-or-7041-microsoft-intune-exchange-connector-service-wont-start"></a>Gebeurtenis 7000 of 7041: De Exchange Connector-service voor Microsoft Intune kan niet worden gestart

**Probleem**:  
Een iOS-apparaat kan niet worden ingeschreven bij Intune en genereert een van de volgende foutberichten:  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Task Category: None
   Level:               Error
   Keywords:        Classic
   User:                N/A
   Computer:      <computer>
   Description:
   The Microsoft Intune Exchange Connector Service service failed to start because of the following error:  
   The service did not start because of a logon failure.
```  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Event ID:          7041
   Task Category: None
   Level:               Error   
   Keywords:        Classic
   User:                N/A
   Computer:       <computer>
   Description:
   The WIEC service was unable to log on as .\WIEC_USER with the currently configured password because of the following error:
   Logon failure: the user has not been granted the requested logon type at this computer.
   Service: WIEC
   Domain and account: .\WIEC_USER
   This service account does not have the required user right "Log on as a service."  
```
Dit probleem kan zich voordoen als het account **WIEC_User** niet over het gebruikersrecht **Aanmelden als service** beschikt in het lokale beleid.

**Oplossing**:  
Op de computer waarop Intune Exchange Connector wordt uitgevoerd, wijst u het gebruikersrecht **Aanmelden als een service** toe aan het serviceaccount **WIEC_User**. Als de computer een knooppunt in een cluster is, moet u ervoor zorgen dat u het gebruikersrecht *Aanmelden als een service* toewijst aan het serviceaccount op alle knooppunten in de cluster.  

Volg deze stappen om het gebruikersrecht **Aanmelden als een service** toe te wijzen aan het serviceaccount **WIEC_User** op de computer:

1. Meld u aan op de computer als een beheerder of een lid van de beheerdersgroep.
2. Voer **secpol.msc** uit om het lokale beveiligingsbeleid te openen.
3. Ga naar **Beveiligingsinstellingen** > **Lokale beleidsregels** en selecteer vervolgens **Toewijzing van gebruikersrechten**.
4. Dubbelklik in het rechterdeelvenster op **Aanmelden als een service**.
5. Selecteer **Gebruiker of groep toevoegen**, voeg **WIEC_USER** toe aan het beleid en selecteer vervolgens twee keer **OK**.

Als het gebruikersrecht **Aanmelden als een service** is toegewezen aan **WIEC_User** maar later is verwijderd, neemt u contact op met de domeinbeheerder om te bepalen of deze door een groepsbeleidsinstelling wordt overschreven.  

## <a name="next-steps"></a>Volgende stappen  

U kunt het volgende artikel gebruiken voor het oplossen van specifieke fouten:
- [Algemene problemen voor Intune Exchange Connector oplossen](troubleshoot-exchange-connector-common-problems.md).git 

Hulp krijgen van het ondersteuningsteam of van de Intune-community.
- Zie [Ondersteuning krijgen](../fundamentals/get-support.md) om de Intune-console te gebruiken voor het oplossen van het probleem of om een ondersteuningscase bij Microsoft te openen. 
- Plaats uw probleem in de [Microsoft Intune fora](/answers/products/mem).
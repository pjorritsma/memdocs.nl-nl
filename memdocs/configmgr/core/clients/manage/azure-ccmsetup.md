---
title: Azure AD-verificatiewerkstroom
titleSuffix: Configuration Manager
description: Details van het installatie proces van de Configuration Manager-client op een Windows 10-apparaat met Azure Active Directory-verificatie
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714120"
---
# <a name="azure-ad-authentication-workflow"></a>Azure AD-verificatiewerkstroom

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat technische Naslag informatie over het installatie proces van de Configuration Manager-client op een Windows 10-apparaat dat is gekoppeld aan Azure Active Directory (Azure AD). Er wordt een overzicht van het werk stroom proces voor de verificatie van het apparaat en de client installatie beschreven.  
 

## <a name="azure-ad-token-request-workflow"></a>Azure AD-token aanvraag werk stroom

![Diagram van Azure AD CCMSetup-werk stroom](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. Azure AD-token aanvraag

Een client die lid is van een Windows 10 Azure AD-domein maakt gebruik van Azure AD-para meters om een token aan te vragen. De volgende vermeldingen worden vastgelegd in **ccmsetup. log**:

- Azure AD-apparaat-token aanvragen:

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- Als een token niet kan worden opgehaald, wordt een Azure AD-gebruikers token aangevraagd:

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> Een client moet een WPJ-certificaat (werk plek toevoegen) krijgen wanneer het lid wordt van Azure AD. Als er geen Workplace-koppelings certificaat wordt gevonden, probeert de client de aanvraag niet te maken met behulp van het communicatie kanaal van de beveiligings token service (CCM_STS). Dit gedrag is omdat de client geen Azure AD-token kan toevoegen aan de aanvraag. Het apparaat beschikt doorgaans niet over dit certificaat wanneer de client niet goed is gekoppeld aan Azure AD.
>
> Als het token niet geldig is, stuurt de Cloud Management Gateway (CMG) de aanvraag ook niet door naar de interne site rollen. Het token kan ongeldig zijn als de Tenant niet is geregistreerd als een Cloud beheer service in Configuration Manager.


### <a name="2-configuration-manager-client-token-request"></a>2. aanvraag voor Configuration Manager-client token

Zodra de client een Azure AD-token heeft, vraagt het een Configuration Manager-client-token (CCM) aan.

De volgende vermeldingen worden vastgelegd in **ccmsetup. log** van de virtuele machine CMG:

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2,1 CMG ontvangt een aanvraag

De volgende vermeldingen worden vastgelegd in **IIS. log**:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2,2 CMG stuurt aanvraag naar CMG-verbindings punt door.

De volgende vermeldingen worden vastgelegd in **CMGService. log**:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2,3 CMG-verbindings punt transformeert CMG client aanvraag aan de beheer punt client aanvraag

De volgende vermeldingen worden vastgelegd in **SMS_CLOUD_PROXYCONNECTOR. log**:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2,4 beheer punt verifieert het token van de gebruiker in de site database

De volgende vermeldingen worden vastgelegd in **CCM_STS. log**:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>Inhouds locatie aanvraag

Zodra de client een reactie krijgt met het CCM-token, wordt deze in de cache opgeslagen en gebruikt om site-informatie en inhouds locatie via de CMG aan te vragen. De volgende vermeldingen worden vastgelegd in **ccmsetup. log**:

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>Clientinstallatie

Het apparaat downloadt de client inhoud en start de installatie.

### <a name="communication-validation"></a>Communicatie validatie

- CMG valideert client token via CMG, CMG Connection Point en HTTP (S), en de data base-aanvraag van het beheer punt.
- Client controleert het CMG-service certificaat of het beheer certificaat
- PKI for CMG-service certificaat: client vereist basis certificerings instantie (CA) van het CMG-certificaat in het lokale archief
- CMG-service certificaat van derden: clients valideren automatisch een certificaat met de basis certificerings instantie die is gepubliceerd op Internet


## <a name="common-issues"></a>Algemene problemen

- De basis-CA is niet aanwezig
- CRL-controle ingeschakeld: Publiceer CRL op internet of gebruik de optie **/NoCRLcheck** in de opdracht regel
- WPJ-certificaat niet gevonden: client is geregistreerd bij Azure AD, maar niet toegevoegd aan Azure AD

Het gebruik van/NoCRLCheck is alleen geschikt voor ccmsetup Boots trap. Voor een volledig functionele client moet u de CRL publiceren op internet. Als tijdelijke oplossing kunt u de CRL-controle uitschakelen op de client communicatie configuratie van de site. Als u de beveiligings instellingen op locatie service hebt vernieuwd, kunnen de clients niet meer communiceren met de server.


## <a name="client-registration"></a>Client registratie

![Werk stroom diagram van Azure AD-registratie](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1. registratie van Configuration Manager client-aanvraag

De volgende vermeldingen worden vastgelegd in **ClientIDManagerStartup. log**:

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2. de Azure AD-token Configuration Manager aanvragen voor het registreren van de client

De volgende vermeldingen worden vastgelegd in **ADALOperationProvider. log**:

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>2,1 Configuration Manager-client is geregistreerd  

De volgende vermeldingen worden vastgelegd in **ClientIDManagerStartup. log**:

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> Tijdens de registratie van de client wordt de certificaat validatie altijd uitgevoerd. Dit proces gebeurt zelfs als u de Azure AD-verificatie methode gebruikt om de-client te registreren.


### <a name="3-configuration-manager-client-token-request"></a>3. aanvraag voor Configuration Manager-client token

Zodra de-site de client registreert, vraagt de client een CCM-token aan. Het CCM-token is versleuteld voor het lokale systeem account (S-1-5-18) en gedurende acht uur in de cache. Na acht uur verloopt het token en de client vraagt het vernieuwen van het token.

De volgende vermeldingen worden vastgelegd in **ClientIDManagerStartup. log**:

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3,1 CMG ontvangt een aanvraag

De volgende vermeldingen worden vastgelegd in **IIS. log**:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3,2 CMG stuurt aanvraag naar CMG-verbindings punt door.

De volgende vermeldingen worden vastgelegd in **CMGService. log**:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3,3 CMG-verbindings punt transformeert CMG client aanvraag aan de beheer punt client aanvraag

De volgende vermeldingen worden vastgelegd in **SMS_CLOUD_PROXYCONNECTOR. log**:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>3,4 beheer punt verifieert het token van de gebruiker in de site database

De volgende vermeldingen worden vastgelegd in **CCM_STS. log**:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```

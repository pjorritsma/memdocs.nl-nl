---
title: Algemene problemen voor Intune Exchange Connector oplossen
titleSuffix: Microsoft Intune
description: Algemene problemen voor on-premises Microsoft Intune Exchange Connector oplossen.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/06/2020
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
ms.openlocfilehash: b1ed3cd24c05586bd5dc9d9a2443a33ffcdc2a48
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914800"
---
# <a name="resolve-common-problems-with-the-intune-exchange-connector"></a>Algemene problemen met Intune Exchange Connector oplossen
 
Intune-beheerders kunnen aan de hand van dit artikel algemene problemen met de werking van Intune Exchange Connector oplossen.

Voordat u begint met het oplossen van het probleem, leest u [Problemen met de on-premises Intune Exchange Connector oplossen](troubleshoot-exchange-connector.md) voor basisinformatie over de connector. Bekijk ook algemene problemen voor de connectorconfiguratie.

## <a name="an-exchange-activesync-device-isnt-discovered-from-exchange"></a>Een Exchange ActiveSync-apparaat wordt niet gedetecteerd door Exchange

Wanneer een Exchange ActiveSync-apparaat niet door Exchange wordt gedetecteerd, moet u [activiteit van de Exchange-connector controleren](exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support) om te zien of de Exchange-connector wordt gesynchroniseerd met de Exchange-server. Als er geen synchronisatie heeft plaatsgevonden sinds het apparaat werd gekoppeld, moet u de synchronisatielogboeken verzamelen en deze bij een ondersteuningsaanvraag voegen. Als een volledige synchronisatie of snelle synchronisatie is voltooid sinds het apparaat is gekoppeld, controleert u of er sprake is van de volgende problemen:

- Controleer of gebruikers over een Intune-licentie beschikken. Als dat niet het geval is, kunnen hun apparaten niet door de Exchange-connector worden gedetecteerd.

- Als het primaire SMTP-adres van een gebruiker anders is dan de UPN (user principal name) in Azure Active Directory (Azure AD), detecteert de Exchange-connector geen enkel apparaat voor die gebruiker. Corrigeer het primaire SMTP-adres om het probleem op te lossen.

- Als u zowel een Exchange 2010- als Exchange 2013-postvakserver in uw omgeving hebt, kunt u de Exchange-connector het beste laten verwijzen naar een Exchange 2013-CAS (Client Access Aerver). Als de Exchange-connector is ingesteld om te communiceren met een Exchange 2010-CAS, kan de Exchange-connector geen apparaten van gebruikers detecteren in Exchange 2013.

- Voor omgevingen met Exchange Online Dedicated moet u de Exchange-connector tijdens de eerste installatie laten verwijzen naar een Exchange 2013-CAS (geen Exchange 2010-CAS) in de toegewezen omgeving. De connector communiceert namelijk alleen met een Exchange 2013-CAS wanneer hiermee PowerShell-cmdlets worden uitgevoerd.

## <a name="problems-with-the-notification-email-message"></a>Problemen met het e-mailbericht met de melding

Ter ondersteuning van voorwaardelijke toegang voor on-premises postvakken op apparaten waarop Android Knox niet wordt uitgevoerd, moet u ervoor zorgen dat de Intune-inschrijving begint met het e-mailbericht 'Nu aan de slag' dat door Intune Exchange Connector wordt verzonden. Door de inschrijving al te starten vanuit dat e-mailbericht, zorgt u ervoor dat het apparaat een unieke ActiveSyncID ontvangt op alle platformen (Exchange, Azure AD, Intune).

Een gebruiker heeft het e-mailbericht met de melding mogelijk niet ontvangen omdat:

- Het meldingsaccount onjuist is ingesteld.
- De functie Automatisch opsporen is mislukt voor het meldingsaccount.
- De EWS-aanvraag (Exchange Web Services) voor het verzenden van het e-mailbericht is mislukt.

Lees de volgende secties door om problemen met e-mailmeldingen op te lossen.

### <a name="check-the-notification-account-that-retrieves-autodiscover-settings"></a>Controleer het meldingsaccount waarop u de instellingen voor Automatisch opsporen ontvangt

1. Zorg ervoor dat de Autodiscover-service en EWS zijn geconfigureerd op de Exchange Client Access-services. Zie [Client Access-services](/Exchange/architecture/client-access/client-access) en de [service voor Automatisch opsporen in de Exchange-server](/Exchange/architecture/client-access/autodiscover?view=exchserver-2019) voor meer informatie.

2. Controleer of uw meldingsaccount aan de volgende vereisten voldoet:

   - Het account beschikt over een actief postvak dat wordt gehost op uw on-premises Exchange-server.

   - De UPN van het account komt overeen met het SMTP-adres.

3. Voor automatisch opsporen is een DNS-server vereist waarop een DNS-record beschikbaar is voor **Autodiscover.SMTPdomain.com** (bijvoorbeeld Autodiscover.contoso.com) dat naar uw Exchange Client Access-server wijst. Controleer of u over dit record beschikt door in plaats van *Autodiscover.SMTPdomain.com* uw FQDN op te geven en volg deze stappen:

   1. Voer bij de opdrachtprompt *NSLOOKUP* in.

   2. Voer *Autodiscover.SMTPdomain.com* in. De uitvoer moet er ongeveer uitzien zoals in de volgende afbeelding: ![Nslookup-resultaten](./media/troubleshoot-exchange-connector-common-problems/nslookup-results.png
      )

   U kunt ook de service voor Automatisch opsporen testen vanaf internet, op https://testconnectivity.microsoft.com. Of test de service vanaf een lokaal domein met behulp van het hulpprogramma Microsoft Connectivity Analyzer. Zie [Het hulpprogramma Microsoft Connectivity Analyzer](/previous-versions/office/exchange-remote-connectivity/jj851141(v=exchg.80)) voor meer informatie.


### <a name="check-autodiscover"></a>Automatisch opsporen controleren

Als Automatisch opsporen niet kan worden uitgevoerd, probeert u de volgende stappen:

1. [Configureer een geldige DNS-record voor Automatisch opsporen](/previous-versions/exchange-server/exchange-150/mt473798(v=exchg.150)).

2. Leg de EWS-URL in code vast in het configuratiebestand van de Intune Exchange-connector:

   1. Bepaal de EWS-URL. De standaard EWS-URL voor Exchange is `https://<mailServerFQDN>/ews/exchange.asmx`, maar uw URL ziet er mogelijk anders uit. Neem contact op met de Exchange-beheerder om de juiste URL voor uw omgeving te verifiëren.

   2. Bewerk het bestand *OnPremisesExchangeConnectorServiceConfiguration.xml*. Het bestand bevindt zich standaard in de map *%ProgramData%\Microsoft\Windows Intune Exchange Connector* op de computer waarop de Exchange-connector wordt uitgevoerd. Open het bestand in een tekst editor en wijzig vervolgens de volgende regel zodat de EWS-URL voor uw omgeving wordt weer gegeven: `<ExchangeWebServiceURL>https://<YourExchangeHOST>/EWS/Exchange.asmx</ExchangeWebServiceURL>`

3. Sla het bestand op en start de computer opnieuw op of start de Microsoft Intune Exchange Connector-service opnieuw.

>[!NOTE]
> In deze configuratie wordt Automatisch opsporen niet meer door Intune Exchange Connector gebruikt en wordt in plaats daarvan rechtstreeks verbinding gemaakt met de EWS-URL.

## <a name="next-steps"></a>Volgende stappen

Probeer [Algemene fouten voor Intune Exchange Connector oplossen](troubleshoot-exchange-connector-common-errors.md) voor hulp bij specifieke fouten.

U kunt als volgt ondersteuning of hulp van de Intune-community krijgen:

- Zie [Ondersteuning krijgen](../fundamentals/get-support.md) om de Intune-console te gebruiken voor het oplossen van het probleem of om een ondersteuningscase bij Microsoft te openen.
- Plaats uw probleem in de [Microsoft Intune-fora](https://social.technet.microsoft.com/Forums/home?forum=microsoftintuneprod).
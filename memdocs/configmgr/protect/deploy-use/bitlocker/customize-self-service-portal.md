---
title: Selfservice portal implementeren
titleSuffix: Configuration Manager
description: Aangepaste organisatie-specifieke informatie toevoegen aan de selfservice portal voor BitLocker-beheer
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 220ebb558a0e01f701cab621381ad951a8fd0738
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88123898"
---
# <a name="customize-the-self-service-portal"></a>Selfservice portal implementeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3601034-->

Nadat u [de BitLocker Self-Service Portal hebt geïnstalleerd](setup-websites.md), kunt u deze aanpassen voor uw organisatie. Voeg een aangepaste kennisgeving, uw organisatie naam en andere organisatie-specifieke informatie toe.

## <a name="branding"></a>Huisstijl

Merk de Self-Service Portal met de naam van uw organisatie, de Help Desk-URL en de tekst van de melding.

1. Meld u aan als beheerder op de webserver die als host fungeert voor de Self-Service Portal.

1. Start de **Internet Information Services (IIS) Manager** (Voer **inetmgr.exe**) uit.

1. Vouw **sites**uit, vouw **standaard**website uit en selecteer het knoop punt **selfservice** . Open in het detail venster, de groep **ASP.net** , de instellingen van de **toepassing**.

    [![Voor beeld van een scherm opname van SelfService toepassings instellingen in IIS-beheer](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. Selecteer het item dat u wilt wijzigen en selecteer in het deel venster **acties** de optie **bewerken**. Wijzig de **waarde** in de nieuwe naam die u wilt gebruiken.

    > [!CAUTION]
    > Wijzig de **naam** waarden niet. U kunt bijvoorbeeld niet wijzigen `CompanyName` , wijzigen `Contoso IT` . Als u de **naam** waarden wijzigt, werkt de Self-Service Portal niet meer.

De wijzigingen zijn onmiddellijk van kracht.

### <a name="supported-branding-values"></a>Ondersteunde huisstijl waarden

Voor de waarden die u kunt instellen, raadpleegt u de volgende tabel:

|Naam|Beschrijving|Standaard &nbsp; waarde|
|--- |--- |--- |
|CompanyName|De naam van de organisatie die de Self-Service Portal weergeeft, wordt boven aan elke pagina weer gegeven als een koptekst.|`Contoso IT`|
|DisplayNotice|Een eerste melding weer geven dat de gebruiker moet bevestigen.|`true`|
|HelpdeskText|De teken reeks in het rechterdeel venster onder "voor alle andere verwante problemen"|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|De koppeling voor de teken reeks HelpdeskText.|gelaten|
|NoticeTextPath|De tekst van de eerste melding die de gebruiker moet erkennen. Standaard is het volledige bestandspad op de webserver `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt` . Bewerk het bestand en sla het op in een tekst editor zonder opmaak. Deze waarde voor het pad is relatief ten opzichte van de SelfService-toepassing.|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

Zie [BitLocker Self-Service Portal](self-service-portal.md)voor een scherm opname van de standaard selfservice Portal.

> [!TIP]
> Als dat nodig is, kunt u enkele van deze teken reeksen lokaliseren om weer te geven in verschillende talen. Zie [lokalisatie](#bkmk_localize)voor meer informatie.

## <a name="session-time-out"></a>Sessietime-out

Als u de sessie van de gebruiker wilt laten verlopen na een opgegeven periode van inactiviteit, kunt u de time-outinstellingen voor de sessie voor de self-service portal wijzigen.

1. Meld u aan als beheerder op de webserver die als host fungeert voor de Self-Service Portal.

1. Start de **Internet Information Services (IIS) Manager** (Voer **inetmgr.exe**) uit.

1. Vouw **sites**uit, vouw **standaard**website uit en selecteer het knoop punt **selfservice** . Open in het detail venster, de groep **ASP.net** , de **sessie status**.

1. Wijzig de time-outwaarde **(in minuten)** in de groep **cookie-instellingen** . Het is het aantal minuten waarna de sessie van de gebruiker verloopt. De standaardwaarde is `5`. Als u de instelling wilt uitschakelen, zodat er geen time-out is, stelt u de waarde in op `0` .

1. Selecteer in het deel venster **acties** de optie **Toep assen**.

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a>Help Desk-tekst en-URL lokaliseren

U kunt gelokaliseerde versies van de instructie Self-Service Portal configureren `HelpdeskText` en `HelpdeskUrl` koppelen. Met deze teken reeks worden gebruikers geïnformeerd over aanvullende ondersteuning bij het gebruik van de portal. Als u gelokaliseerde tekst configureert, wordt in de Portal de gelokaliseerde versie voor webbrowsers in die taal weer gegeven. Als er geen gelokaliseerde versie wordt gevonden, wordt de standaard waarde in de `HelpdeskText` instellingen en weer gegeven `HelpdeskUrl` .

1. Meld u aan als beheerder op de webserver die als host fungeert voor de Self-Service Portal.

1. Start de **Internet Information Services (IIS) Manager** (Voer **inetmgr.exe**) uit.

1. Vouw **sites**uit, vouw **standaard**website uit en selecteer het knoop punt **selfservice** . Open in het detail venster, de groep **ASP.net** , de instellingen van de **toepassing**.

1. Selecteer in het deel venster **acties** de optie **toevoegen**.

1. Configureer in het venster **toepassings instelling toevoegen** de volgende waarden:

    - **Name**: Enter `HelpdeskText_<language>` , waarbij `<language>` de taal code voor de tekst is.

      Als u bijvoorbeeld een gelokaliseerde `HelpdeskText` instructie in Spaans (Spanje) wilt maken, is de naam `HelpdeskText_es-es` .

    - **Waarde**: de gelokaliseerde teken reeks die moet worden weer gegeven in het rechterdeel venster van de self-service portal onder "voor alle andere verwante problemen"

1. Selecteer **OK** om de nieuwe instelling op te slaan.

1. Herhaal dit proces om een nieuwe toepassings instelling toe te voegen voor `HelpdeskUrl_<language>` die overeenkomt met de bijbehorende `HelpdeskText_<language>` instelling.

Herhaal dit proces voor het toevoegen van een paar instellingen voor alle talen die u in uw organisatie ondersteunt.

## <a name="localize-the-notice-file"></a>Het mededelingen bestand lokaliseren

U kunt gelokaliseerde versies van de eerste melding configureren dat de gebruiker in de Self-Service Portal moet erkennen. Standaard is het volledige bestandspad op de webserver `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt` .

Als u gelokaliseerde bericht tekst wilt weer geven, maakt u een gelokaliseerd notice.txt bestand. Sla het vervolgens op onder een specifieke taalmap. Bijvoorbeeld: `Self Service Website\es-es\Notice.txt` voor Spaans (Spanje).

De Self-Service Portal geeft de bericht tekst weer op basis van de volgende regels:

- Als het bestand met de standaard waarschuwing ontbreekt, wordt in de portal een bericht weer gegeven dat het standaard bestand ontbreekt.

- Als u een gelokaliseerd mededelingen bestand maakt in de desbetreffende taalmap, wordt de gelokaliseerde tekst weer gegeven.

- Als de webserver geen gelokaliseerde versie van het mededelingen bestand vindt, wordt de standaard melding weer gegeven.

- Als de gebruiker de browser instelt op een taal die geen gelokaliseerde kennisgeving heeft, wordt de standaard melding weer gegeven in de portal.

### <a name="create-a-localized-notice-file"></a>Een gelokaliseerd kennisgevings bestand maken

1. Meld u aan als beheerder op de webserver die als host fungeert voor de Self-Service Portal.

1. Maak een `<language>` map voor elke ondersteunde taal in het `Self Service Website` pad van de toepassing. Bijvoorbeeld `es-es` voor Spaans (Spanje). Het volledige pad is standaard `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es` .

    Voor een lijst met geldige taal codes die u kunt gebruiken, raadpleegt u [API-naslag informatie over nationale talen ondersteuning (NLS)](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers).

    > [!TIP]
    > De naam van de taal map kan ook de taalneutrale-naam zijn. Bijvoorbeeld: **es** voor Spaans in plaats van **es-es** voor Spaans (Spanje) en **es-ar** voor Spaans (Argentinië). Als de gebruiker de browser instelt op **es-es**en die taalmap niet bestaat, controleert de webserver de bovenliggende landinstellings map (**sen**) recursief. (De bovenliggende land instellingen worden gedefinieerd in .NET.) Bijvoorbeeld `Self Service Website\es\Notice.txt` . Deze recursieve terugval simuleert de regels voor het laden van .NET-resources.

1. Maak een kopie van het standaard gegevensbestand met de gelokaliseerde tekst. Sla het bestand op in de map voor de taal code. Bijvoorbeeld: voor Spaans (Spanje) is standaard het volledige pad `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt` .

Herhaal dit proces naar een gelokaliseerd mededelingen bestand voor alle talen die u in uw organisatie ondersteunt.

## <a name="next-steps"></a>Volgende stappen

Nu u de Self-Service Portal hebt geïnstalleerd en aangepast, probeer het dan eens. Zie voor meer informatie [BitLocker Self-Service Portal](self-service-portal.md).

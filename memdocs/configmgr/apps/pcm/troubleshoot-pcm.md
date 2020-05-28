---
title: Problemen met Package Conversion Manager oplossen
titleSuffix: Configuration Manager
description: Meer informatie over het oplossen van problemen met de package Conversion Manager in Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05110714d3aa8ca48ff9384f0116338b0092fde1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877623"
---
# <a name="troubleshoot-package-conversion-manager"></a>Problemen met Package Conversion Manager oplossen

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1357861-->

Gebruik de informatie in dit artikel voor hulp bij het oplossen van problemen bij het gebruik van package Conversion Manager.



## <a name="sms-provider"></a>SMS-provider

Pakket conversie beheer maakt gebruik van de SMS-provider. Zie [de SMS-provider plannen](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)voor meer informatie.

Als de SMS-provider niet goed werkt, werkt de Configuration Manager-console, inclusief de package Conversion Manager, niet.



## <a name="package-readiness"></a>Gereedheid voor pakket

Voordat u een pakket converteert naar een toepassing, analyseer het pakket met de functie voor het **analyseren** van package Conversion Manager. Voeg na de analyse de kolom **gereedheid** toe aan het knoop punt **pakketten** van de Configuration Manager-console. In de lijst met pakketten wordt een van de volgende gereedheids statussen van het geanalyseerde pakket weer gegeven:

- **Automatisch**: het pakket kan rechtstreeks worden geconverteerd met de functie **Convert** .      

  > [!NOTE]  
  > Met een automatische conversie worden WQL-query's niet omgezet in toepassings vereisten. Gebruik het **herstel-en conversie** proces om deze query's te converteren.  

- **Hand matig**: het pakket moet enkele toevoegingen of wijzigingen hebben voordat u het kunt converteren met de functie **Fix en Convert** .  

- **Niet van toepassing**: het pakket is niet geschikt voor conversie. Los eventuele problemen met het pakket op of ga door met het implementeren van een pakket.  

- **Fout**: het pakket bevat fouten. Corrigeer deze fouten hand matig voordat u deze kunt analyseren en converteren.  

Het deel venster met details van het knoop punt **pakketten** in de Configuration Manager-console bevat problemen met de voor bereidingen. Selecteer een pakket en selecteer vervolgens het tabblad **samen vatting** in het detail venster.



## <a name="log-files"></a>Logboekbestanden

### <a name="enable-logging"></a>Logboekregistratie inschakelen

Wanneer u logboek registratie inschakelt voor package Conversion Manager, worden alle acties, uitzonde ringen en fouten in het logboek geregistreerd.

Als u logboek registratie voor dit onderdeel wilt inschakelen in de Configuration Manager, wijzigt u **micro soft. ConfigurationManagement. exe. config**. Dit configuratie bestand bevindt zich standaard in het volgende pad:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

> [!IMPORTANT]
> Vanaf versie 1910 is dit pad gewijzigd om de map te gebruiken `Microsoft Endpoint Manager` . Zorg ervoor dat u geen oudere versie van het bestand gebruikt dat in een andere map kan voor komen.

Voeg de volgende **switches** en **traceer** XML-elementen in het element **System. Diagnostics** toe na het laatste **bron** element:

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

In dit voor beeld wordt het bestand **PCMTrace. log**gebruikt. Dit logboek bevindt zich op de computer waarop de Configuration Manager-console wordt uitgevoerd in het volgende pad:  
`%UserProfile%\AppData\Local\Temp`

Als u het detail niveau wilt configureren, wijzigt u de instelling van de **PcmLogging** Trace switch. Stel deze waarde in op vier detail niveaus, van minst gedetailleerd ( `1` ) tot de meest gedetailleerde ( `4` ).


### <a name="smsprovlog"></a>SMSProv.log

In sommige gevallen bevindt de informatie die relevant is voor het oplossen van het pakket conversie proces zich in het bestand **SMSProv. log** . Met dit bestand worden gegevens van de Configuration Manager SMS-provider vastgelegd.

Dit logboek bestand bevindt zich standaard op de Configuration Manager site server op het volgende pad:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Als u een van de volgende fout berichten ziet, bevat het bestand **SMSProv. log** mogelijk relevante informatie over het oplossen van problemen:

- `The SMS Provider reported an error`

- `Generic Failure`

Deze fout berichten geven doorgaans aan dat er een fout is opgetreden op de site server en dat de fout informatie niet is verzonden naar de Configuration Manager-console.

Zie voor meer informatie [technische documentatie voor package Conversion Manager-fout berichten](error-messages.md).



## <a name="changing-package-attributes-after-analysis"></a>Pakket kenmerken na analyse wijzigen

Nadat u een pakket hebt geanalyseerd en het de gereedheids status **automatisch** of **hand matig**heeft, kan het conversie proces mislukken als u een van de relevante kenmerken wijzigt.

U kunt bijvoorbeeld een pakket analyseren en de gereedheids status is **automatisch**. Vervolgens voegt u een ander programma toe aan het pakket. De pakket conversie kan mislukken.

Als u na de analyse wijzigingen moet aanbrengen in een pakket, voert u de analyse uit vóór de conversie. 



## <a name="see-also"></a>Zie ook

[Technische documentatie voor fout berichten van package Conversion Manager](error-messages.md)

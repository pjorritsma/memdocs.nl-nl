---
title: Ondersteunings centrum aanpassen
titleSuffix: Configuration Manager
description: Pas het configuratie bestand van het ondersteunings centrum aan.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fc17437e508ea69a19043c29bf9ad4501cbac3e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078512"
---
# <a name="customize-support-center"></a>Ondersteunings centrum aanpassen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het hulp programma [ondersteunings centrum](support-center.md) bevat een configuratie bestand dat u kunt aanpassen. Wanneer u het ondersteunings centrum installeert, bevindt het bestand zich standaard in `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`het volgende pad:. Het configuratie bestand wijzigt het gedrag van het programma:

- [Gegevens verzameling aanpassen](#bkmk_datacoll): Bewerk de sets register sleutels en WMI-naam ruimten die tijdens het verzamelen van gegevens worden opgenomen  

- [Logboek groepen aanpassen](#bkmk_loggroups): Definieer nieuwe groepen logboek bestanden met reguliere expressies. Voeg ook andere logboek bestanden toe aan logboek groepen.  

- [Aanvullende logboek bestanden verzamelen met Joker tekens](#bkmk_wildcards): gebruik Zoek opdrachten met Joker tekens om aanvullende logboek bestanden te verzamelen  

Als u deze wijzigingen wilt aanbrengen, moet u lokale beheerders machtigingen hebben op de client waarop u het ondersteunings centrum hebt geïnstalleerd. U kunt deze aanpassingen aanbrengen met behulp van een tekst-of XML-editor, zoals Klad blok of Visual Studio.

> [!Important]  
> Het configuratie bestand van het ondersteunings centrum is een bestand met XML-indeling. Het is essentieel voor de werking van het ondersteunings centrum. Het wijzigen van dit bestand wordt alleen aanbevolen voor gebruikers die bekend zijn met XML en reguliere expressies.  

Voordat u het configuratie bestand van het ondersteunings centrum aanpast, moet u een back-up van het origineel opslaan. Met deze back-up kunt u de oorspronkelijke functionaliteit van het ondersteunings centrum herstellen als u fouten maakt tijdens het bewerken van het bestand. Als u geen back-up maakt en het ondersteunings centrum niet goed werkt nadat u het configuratie bestand hebt gewijzigd, installeert u het ondersteunings centrum opnieuw. U kunt ook een configuratie bestand kopiëren van een andere installatie van het ondersteunings centrum.



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a>Gegevens verzameling aanpassen

Om het verzamelen van gegevens op de client aan te passen, wijzigt u het configuratie bestand van het ondersteunings `<dataCollectorSettings>` centrum met behulp van XML-elementen in het-element.


### <a name="wmi-data-collection"></a>WMI-gegevens verzameling

Het `<CcmWmiDataCollector>` element bevat een `<collectionScopes>` -element. Gebruik dit element om de WMI-naam ruimten te wijzigen waaruit de gegevens worden verzameld in ondersteunings centrum. Het bevat ook een `<ignoreScopes>` element. Gebruik dit element om het verzamelen van gegevens uit delen van de naam ruimten die in het `<collectionScopes>` element zijn gedefinieerd, te filteren.  
    
#### <a name="example"></a>Voorbeeld
Het standaard configuratie bestand verzamelt gegevens uit de `root\ccm` naam ruimte. Dit pad wordt in een `<add/>` -element in `<collectionScopes>`opgenomen. 

Ook worden `\cimodels`alles onder de paden, `\invagt` `\events`, en `\policy` voor deze naam ruimte genegeerd. Deze paden zijn opgenomen in `<add/>` elementen in `<ignoreScopes>`.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Verzameling van register gegevens

Het `<RegistryDataCollector>` element bevat een `<registryKeys>` -element. Gebruik dit element om de register sleutels en subsleutels te wijzigen die ondersteunings `HKEY_LOCAL_MACHINE` centrum onder het pad verzamelt. Ondersteunings centrum biedt geen ondersteuning voor het verzamelen van register gegevens uit andere register paden voor het hoofd bestand.

#### <a name="example"></a>Voorbeeld
Als u register sleutels wilt verzamelen voor de klassieke Program ma's die op het apparaat zijn `<add/>` geïnstalleerd, voegt `<registryKeys>` u het volgende element toe aan het element:`<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a>Logboek bestands groepen aanpassen

Als u wilt aanpassen welk logboek bestand in ondersteunings centrum wordt verzameld en hoe deze worden weer gegeven in de lijst **logboek groepen** , gebruikt u elementen in het `<logGroups>` element. Wanneer u het ondersteunings centrum start, wordt deze sectie van het configuratie bestand gescand. Vervolgens wordt er een groep gemaakt in de lijst **logboek groepen** voor elke unieke sleutel kenmerk waarde die is `<add/>` gevonden in de elementen `<logGroups>` in het element.

- **Onderdeel logboek groep**: het `<componentLogGroup>` element gebruikt een sleutel kenmerk om de naam van de logboek groep te definiëren die in de lijst wordt weer gegeven. Er wordt ook een value-kenmerk gebruikt dat een reguliere expressie (regex) bevat. Deze reguliere expressie wordt gebruikt om een reeks gerelateerde logboek bestanden te verzamelen.  

- **Statische logboek groep:** Het `<staticLogGroup>` element gebruikt een sleutel kenmerk voor het definiëren van de naam van de logboek groep die in de lijst wordt weer gegeven. Er wordt ook een value-kenmerk gebruikt dat een naam van een logboek bestand definieert.  

Als dezelfde sleutel kenmerk waarde wordt gebruikt in een `<add/>` element binnen het `<componentLogGroup>` element en het `<staticLogGroup>` element, maakt het ondersteunings centrum één groep. Deze groep bevat de logboek bestanden die zijn gedefinieerd door beide elementen die dezelfde sleutel gebruiken.

#### <a name="example"></a>Voorbeeld
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a>Aanvullende logboek bestanden verzamelen met Joker tekens

Als u aanvullende logboek bestanden wilt verzamelen, gebruikt u Joker tekens in het bestandspad of bestands naam. Deze Joker tekens zijn onder andere omgevings variabelen voor het `%WINDIR%`hele systeem, zoals, maar geen omgevings variabelen met `%USERPROFILE%`gebruikers bereik, zoals. Voor het verzamelen van aanvullende logboek bestanden met dit niet-recursieve logboek bestand, gebruikt u `<add/>` een element in `<additionalLogFiles>` het-element. 

In deze voor beelden ziet u hoe het ondersteunings centrum gebruikmaakt van deze functie in het standaard configuratie bestand.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Voor beeld 1: alle Windows Update logboek bestanden verzamelen in de Windows-map
Het volgende element verzamelt elk bestand met `WindowsUpdate.log` de naam die wordt gevonden in de Windows-map: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Voor beeld 2: alle logboek bestanden verzamelen in de map Windows logs
Het volgende element verzamelt alle bestanden die eindigen op `.log` in de map Windows logs: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>Volledig XML-voor beeld
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```

---
title: Configuratie-XML van invoeg toepassing
titleSuffix: Configuration Manager
description: Technische documentatie voor de XML-elementen van de invoeg toepassing package Conversion Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9178b595ba67723c623979b4c29290e42fe5f6ac
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877738"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Technische documentatie voor de invoeg toepassing configuratie-XML van package Conversion Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1357861-->

In dit artikel worden de XML-elementen in het configuratie bestand van de Configuration Manager (Microsoft. ConfigurationManagement. exe. config) beschreven waarmee de werking van de package Conversion Manager-invoeg toepassing wordt beheerd. Zie [de invoeg toepassing package Conversion Manager gebruiken](how-to-use-plug-in.md)voor meer informatie over het gebruik van deze invoeg toepassing.



## <a name="xml-configuration-elements"></a>XML-configuratie-elementen

In de volgende tabel worden de XML-elementen in het configuratie bestand van de Configuration Manager beschreven die betrekking hebben op de invoeg toepassing pakket conversie beheer.

|Element  |Type  |Beschrijving  |
|---------|---------|---------|
|**PcmPlugIn**|Tekenreeks|De naam van het script of het uitvoer bare bestand dat moet worden gebruikt als de pakket conversie beheer-invoeg toepassing.|
|**PcmPlugInTimeoutMilliseconds**|Geheel getal|De maximale tijds duur, in milliseconden, dat moet worden gewacht op het script of uitvoer bare pakket conversie beheer-invoeg toepassing voor het volt ooien van de verwerking van een pakket.|
|**PcmPluginExitCode**|Geheel getal|De verwachte afsluit code van het invoeg toepassings proces. Deze waarde geeft aan dat het geslaagd is. Alle andere codes worden als een fout beschouwd.|
|**ForceRequirementsExtraction**|Boolean|Automatische conversie toestaan om verzamelings vereisten te gebruiken die zijn gekoppeld aan een pakket. Dit moet alleen worden ingesteld op true wanneer u werkt met een package Conversion Manager-invoeg toepassing die is ontworpen om beslissingen te nemen over welke vereisten moeten worden gebruikt.|



## <a name="sample-configuration-xml"></a>XML voor voorbeeld configuratie

In deze sectie vindt u een voor beeld van de XML-elementen voor de configuratie van package Conversion Manager in het Configuration Manager-configuratie bestand **micro soft. ConfigurationManagement. exe. config**. Dit bestand bevindt zich standaard in het volgende pad:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

> [!IMPORTANT]
> Vanaf versie 1910 is dit pad gewijzigd om de map te gebruiken `Microsoft Endpoint Manager` . Zorg ervoor dat u geen oudere versie van het bestand gebruikt dat in een andere map kan voor komen. 

In het voor beeld bevinden de elementen die betrekking hebben op package Conversion Manager zich in het volgende-element:`Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```


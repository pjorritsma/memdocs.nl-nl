---
title: Hulpprogramma voor het opnieuw instellen van updates
titleSuffix: Configuration Manager
description: Gebruik het hulp programma voor het opnieuw instellen van updates voor de update in de console voor Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b4aa67280c879d6f7feaf549ac7f13ba0136ca91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720749"
---
# <a name="update-reset-tool"></a>Hulpprogramma voor het opnieuw instellen van updates

*Van toepassing op: Configuration Manager (huidige vertakking)*  


Vanaf versie 1706, Configuration Manager primaire sites en centrale beheer sites bevatten het hulp programma Configuration Manager Update reset, **CMUpdateReset. exe**. Gebruik het hulp programma om problemen op te lossen bij het downloaden of repliceren van updates in de console. Het hulp programma bevindt zich in de map ***\Cd.latest\SMSSETUP\TOOLS*** van de site server.

U kunt dit hulp programma gebruiken met alle versies van de huidige vertakking die in ondersteuning blijven.

Gebruik dit hulp programma wanneer een [Update in de console](install-in-console-updates.md) nog niet is geïnstalleerd en zich in een mislukte status bevindt. Een mislukte status betekent dat het downloaden van de update wordt uitgevoerd, maar vastgelopen of veel tijd in beslag neemt. Lange tijd wordt gezien als uren langer dan uw historische verwachtingen voor update pakketten met een vergelijk bare grootte. Het kan ook een fout zijn bij het repliceren van de update op onderliggende primaire sites.  

Wanneer u het hulp programma uitvoert, wordt het uitgevoerd op basis van de update die u opgeeft. Het hulp programma heeft standaard de installatie of gedownloade updates niet verwijderd.  

### <a name="prerequisites"></a>Vereisten
Het account dat u gebruikt om het hulp programma uit te voeren, vereist de volgende machtigingen:
- **Lees** -en **Schrijf** machtigingen voor de site database van de centrale beheer site en alle primaire sites in uw hiërarchie. Als u deze machtigingen wilt instellen, kunt u het gebruikers account toevoegen als lid van de **db_datawriter** en **db_datareader** [vaste database rollen](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) op de Configuration Manager-Data Base van elke site. Het hulp programma heeft geen interactie met secundaire sites.
- **Lokale beheerder** op de site op het hoogste niveau van uw hiërarchie.
- **Lokale beheerder** op de computer die het service verbindings punt host.

U hebt de GUID nodig van het update pakket dat u opnieuw wilt instellen. De GUID ophalen:
  1.   Ga in de-console naar **beheer** > **updates en onderhoud**.
  2.   Klik in het weergave paneel met de rechter muisknop op de kop van een van de kolommen (zoals **status**) en selecteer vervolgens **pakket-GUID** om die kolom toe te voegen aan de weer gave.
  3.   In de kolom wordt nu de GUID van het update pakket weer gegeven.

> [!TIP]  
> Als u de GUID wilt kopiëren, selecteert u de rij voor het update pakket dat u opnieuw wilt instellen en gebruikt u vervolgens CTRL + C om die rij te kopiëren. Als u de gekopieerde selectie in een tekst editor plakt, kunt u vervolgens alleen de GUID kopiëren voor gebruik als een opdracht regel parameter wanneer u het hulp programma uitvoert.

### <a name="run-the-tool"></a>Het hulp programma uitvoeren    
Het hulp programma moet worden uitgevoerd op de site op het hoogste niveau van de hiërarchie.

Wanneer u het hulp programma uitvoert, gebruikt u de opdracht regel parameters om het volgende op te geven:
- De SQL Server op de site op het hoogste niveau van de hiërarchie.
- De naam van de site database op de site op het hoogste niveau.
- De GUID van het update pakket dat u opnieuw wilt instellen.

Op basis van de status van de update identificeert het hulp programma de extra servers die moeten worden geopend.   

Als het update pakket een status *na het downloaden* heeft, wordt het pakket niet opgeschoond met het hulp programma. Als optie kunt u het verwijderen van een geslaagde Update afdwingen met behulp van de para meter Force Delete (Zie opdracht regel parameters verderop in dit onderwerp).

Wanneer het hulp programma wordt uitgevoerd:
- Als een pakket is verwijderd, start u de SMS_Executive-service opnieuw op de site op het hoogste niveau. Controleer vervolgens op updates zodat u het pakket opnieuw kunt downloaden.
- Als een pakket niet is verwijderd, hoeft u geen actie te ondernemen. De update initialiseert opnieuw en start de replicatie of installatie opnieuw.

**Opdracht regel parameters:**  


|                        Parameter                         |                                                       Beschrijving                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;FQDN van de SQL Server van uw site op het hoogste niveau>** | *Vereist* <br> Geef de FQDN op van de SQL Server die als host fungeert voor de site database voor de bovenste site van uw hiërarchie. |
|                **-D &lt;Database naam>**                 |                          *Vereist* <br> Geef de naam op van de Data Base op de site op het hoogste niveau.                          |
|                 **-P &lt;Package GUID>**                 |                        *Vereist* <br> Geef de GUID op voor het update pakket dat u opnieuw wilt instellen.                        |
|           **-I &lt;SQL Server exemplaar naam>**           |                    *Beschrijving* <br> Identificeer het exemplaar van SQL Server dat als host fungeert voor de site database.                     |
|                       **-FDELETE**                       |                       *Beschrijving* <br> Het verwijderen van een geslaagd update pakket afdwingen.                        |

**Voorbeelden:**  
In een typisch scenario wilt u een update met Download problemen opnieuw instellen. De FQDN van de SQL-servers is *Server1.fabrikam.com*, de site database is *CM_XYZ*en de pakket-GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  U voert de volgende handelingen uit: ***CMUpdateReset. exe-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

In een meer extreme scenario wilt u het verwijderen van problematische update pakketten afdwingen. De FQDN van de SQL-servers is *Server1.fabrikam.com*, de site database is *CM_XYZ*en de pakket-GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  U voert de volgende handelingen uit: ***CMUpdateReset. exe-FDELETE-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716171"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a>Hardware-inventaris rapporten

<!--5468413-->
Als u probeert een rapport uit te voeren dat afhankelijk is van de hardware-inventaris, wordt een fout bericht weer gegeven. Een BitLocker-rapport retourneert bijvoorbeeld een fout die vergelijkbaar is met het volgende bericht:

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

Mogelijk ziet u ook de volgende fout in het bestand **dataldr. log** :

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

Console dashboards die afhankelijk zijn van hardware-inventarisatie kunnen ook worden beïnvloed.

Dit probleem wordt veroorzaakt door een wijziging in het database schema voor specifieke hardware-inventarisatie tabellen.

#### <a name="workaround"></a>Tijdelijke oplossing

De tijdelijke oplossing bestaat uit het verwijderen van het vooraf bestaande kenmerk uit de data base. Het dataloader-site onderdeel kan vervolgens een nieuw kenmerk maken. Voer het volgende SQL-script uit op de site database server om het tabel schema te herstellen:

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```

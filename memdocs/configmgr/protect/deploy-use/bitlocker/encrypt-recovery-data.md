---
title: Herstelgegevens versleutelen
titleSuffix: Configuration Manager
description: Versleutel BitLocker-herstel sleutels, herstel pakketten en TPM-wachtwoord hashes via het netwerk en in de Configuration Manager-Data Base.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2c74f1ac74b120fac2dabcd5f84f288b41368324
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697293"
---
# <a name="encrypt-recovery-data"></a>Herstelgegevens versleutelen

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3601034-->

Wanneer u een beleid voor BitLocker-beheer maakt, implementeert Configuration Manager de herstel service op een beheer punt. Wanneer u **BitLocker-beheer Services configureert**op de pagina **client beheer** van het beleid voor BitLocker-beheer, maakt de client back-ups van sleutel herstel gegevens naar de site database. Deze informatie omvat BitLocker-herstel sleutels, herstel pakketten en TPM-wachtwoord hashes. Wanneer gebruikers zijn vergrendeld op hun beveiligde apparaat, kunt u deze informatie gebruiken om de toegang tot het apparaat te herstellen.

Gezien de gevoelige aard van deze informatie, moet u deze beveiligen in de volgende omstandigheden:

- Configuration Manager is een HTTPS-verbinding tussen de client en de Recovery-service nodig om de gegevens in de overdracht via het netwerk te versleutelen. Er zijn twee opties:

  - HTTPS: Schakel de IIS-website in op het beheer punt dat als host fungeert voor de Recovery-service, niet de volledige rol van het beheer punt. Deze optie is alleen van toepassing op Configuration Manager versie 2002.<!-- 5925660 -->

  - Configureer het beheer punt voor HTTPS. Op de eigenschappen van het beheer punt moet de instelling voor **client verbindingen** **https**zijn. Deze optie is van toepassing op Configuration Manager versie 1910 of 2002.

    > [!NOTE]
    > Het biedt momenteel geen ondersteuning voor verbeterde HTTP.

- U kunt deze gegevens ook versleutelen wanneer deze worden opgeslagen in de site database. Als u een SQL-certificaat installeert, worden uw gegevens in SQL Configuration Manager versleuteld.

    Als u geen BitLocker-versleutelings certificaat wilt maken, moet u zich aanmelden voor onbewerkte tekst opslag van de herstel gegevens. Wanneer u een BitLocker-beheer beleid maakt, schakelt u de optie in om te **zorgen dat herstel gegevens worden opgeslagen als tekst zonder opmaak**.

    > [!NOTE]
    > Een andere beveiligingslaag is het versleutelen van de hele site database. Als u versleuteling inschakelt voor de data base, zijn er geen functionele problemen in Configuration Manager.
    >
    > Versleutelen met voorzichtigheid, met name in grootschalige omgevingen. Afhankelijk van de tabellen die u versleutelt en de versie van SQL, kunt u een prestatie vermindering van 25% opmerken. Werk uw back-up-en herstel plannen bij, zodat u de versleutelde gegevens kunt herstellen.

## <a name="certificate-requirements"></a>Certificaatvereisten

### <a name="https-server-authentication-certificate"></a>Certificaat voor HTTPS-server verificatie

<!--5925660-->

In Configuration Manager huidige branch versie 1910 om de BitLocker Recovery-service te integreren, moet u een beheer punt inschakelen. De HTTPS-verbinding is nodig voor het versleutelen van de herstel sleutels in het netwerk van de Configuration Manager-client naar het beheer punt. Het configureren van het beheer punt en alle clients voor HTTPS kunnen veel klanten lastig zijn.

Vanaf versie 2002 is de HTTPS-vereiste voor de IIS-website die als host fungeert voor de Recovery-service, niet de volledige rol van het beheer punt. Met deze wijziging worden de certificaat vereisten versoepeld en worden de herstel sleutels tijdens de overdracht nog steeds versleuteld.

De eigenschap **client verbindingen** van het beheer punt kan nu **http** of **https**zijn. Als het beheer punt is geconfigureerd voor **http**, ter ondersteuning van de BitLocker Recovery-service:

1. Haal een server verificatie certificaat op. Koppel het certificaat aan de IIS-website op het beheer punt dat als host fungeert voor de BitLocker Recovery-service.

2. Configureer clients om het server authenticatie certificaat te vertrouwen. Er zijn twee methoden om deze vertrouwens relatie uit te voeren:

    - Gebruik een certificaat van een open bare en wereld wijd vertrouwde certificaat provider. Bijvoorbeeld, maar niet beperkt tot, DigiCert, Thawte of VeriSign. Windows-clients bevatten vertrouwde basis certificerings instanties (Ca's) van deze providers. Door gebruik te maken van een server verificatie certificaat dat is uitgegeven door een van deze providers, moeten uw clients deze automatisch vertrouwen.

    - Gebruik een certificaat dat is uitgegeven door een certificerings instantie uit de open bare-sleutel infrastructuur (PKI) van uw organisatie. De meeste PKI-implementaties voegen de vertrouwde basis certificerings instanties toe aan Windows-clients. U kunt bijvoorbeeld Active Directory Certificate Services gebruiken met groeps beleid. Als u het Server verificatie certificaat uitgeeft van een certificerings instantie die niet automatisch wordt vertrouwd door uw clients, voegt u het vertrouwde basis certificaat van de certificerings instantie toe aan clients.

> [!TIP]
> De enige clients die moeten communiceren met de Recovery-service, zijn de clients die u wilt richten op het beheer beleid van BitLocker en die een regel voor **client beheer** bevatten.

Gebruik op de client de **BitLockerManagementHandler. log** om de verbinding op te lossen. Voor de connectiviteit met de herstel service wordt in het logboek de URL weer gegeven die door de client wordt gebruikt. Zoek een item dat begint met `Checking for Recovery Service at` .

> [!NOTE]
> Als uw site meer dan één beheer punt heeft, schakelt u HTTPS in op alle beheer punten op de site waarmee een door BitLocker beheerde client mogelijk zou kunnen communiceren. Als het HTTPS-beheer punt niet beschikbaar is, kan de client een failover uitvoeren naar een HTTP-beheer punt en vervolgens de herstel sleutel niet meer borgen.
>
> Deze aanbeveling is van toepassing op beide opties: Schakel het beheer punt in voor HTTPS of schakel de IIS-website in die als host fungeert voor de herstel service op het beheer punt.

### <a name="sql-encryption-certificate"></a>SQL-versleutelings certificaat

Gebruik dit SQL-certificaat voor Configuration Manager voor het versleutelen van BitLocker-herstel gegevens in de site database. U kunt uw eigen proces gebruiken voor het maken en implementeren van het versleutelings certificaat voor BitLocker-beheer, mits dit aan de volgende vereisten voldoet:

- De naam van het BitLocker-beheer versleutelings certificaat moet zijn `BitLockerManagement_CERT` .

- Dit certificaat versleutelen met een hoofd sleutel van de data base.

- De volgende SQL-gebruikers hebben **beheer** machtigingen nodig voor het certificaat:
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Implementeer hetzelfde certificaat op elke site database in uw hiërarchie.

- Maak het certificaat met de nieuwste versie van SQL Server in uw omgeving. Bijvoorbeeld:
  - Certificaten die zijn gemaakt met SQL Server 2016 of hoger zijn compatibel met SQL Server 2014 of eerder.
  - Certificaten die zijn gemaakt met SQL Server 2014 of een eerdere versie zijn niet compatibel met SQL Server 2016 of hoger.

## <a name="example-scripts"></a>Voorbeeld scripts

Deze SQL-scripts zijn voor beelden van het maken en implementeren van een versleutelings certificaat voor BitLocker-beheer in de Configuration Manager-site database.

### <a name="create-certificate"></a>Certificaat maken

Met dit voorbeeld script worden de volgende acties uitgevoerd:

- Hiermee maakt u een certificaat
- Hiermee stelt u de machtigingen in
- Hiermee maakt u een database hoofd sleutel

Voordat u dit script in een productie omgeving gebruikt, wijzigt u de volgende waarden:

- Site database naam ( `CM_ABC` )
- Wacht woord voor het maken van de hoofd sleutel ( `MyMasterKeyPassword` )
- Verval datum van het certificaat ( `20391022` )

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>Back-up van certificaat

Met dit voorbeeld script maakt u een back-up van een certificaat. Wanneer u het certificaat opslaat in een bestand, kunt u het [herstellen](#restore-certificate) naar andere site databases in de hiërarchie.

Voordat u dit script in een productie omgeving gebruikt, wijzigt u de volgende waarden:

- Site database naam ( `CM_ABC` )
- Bestandspad en-naam ( `C:\BitLockerManagement_CERT_KEY` )
- Sleutel wachtwoord exporteren ( `MyExportKeyPassword` )

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> Sla het geëxporteerde certificaat bestand en het bijbehorende wacht woord op een beveiligde locatie op.

### <a name="restore-certificate"></a>Certificaat herstellen

Met dit voorbeeld script wordt een certificaat uit een bestand hersteld. Gebruik dit proces voor het implementeren van een certificaat dat u hebt gemaakt op een andere site database.

Voordat u dit script in een productie omgeving gebruikt, wijzigt u de volgende waarden:

- Site database naam ( `CM_ABC` )
- Hoofd sleutel wachtwoord ( `MyMasterKeyPassword` )
- Bestandspad en-naam ( `C:\BitLockerManagement_CERT_KEY` )
- Sleutel wachtwoord exporteren ( `MyExportKeyPassword` )

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>Certificaat verifiëren

Gebruik dit SQL-script om te controleren of SQL het certificaat met de vereiste machtigingen heeft gemaakt.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

Als het certificaat geldig is, retourneert het script een waarde van `1` .

## <a name="see-also"></a>Zie ook

Raadpleeg de volgende artikelen voor meer informatie over deze SQL-opdrachten:

- [Versleutelings sleutels voor SQL Server en data base](/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [Certificaat maken](/sql/t-sql/statements/create-certificate-transact-sql)
- [Back-upcertificaat](/sql/t-sql/statements/backup-certificate-transact-sql)
- [Hoofd sleutel maken](/sql/t-sql/statements/create-master-key-transact-sql)
- [Hoofd sleutel voor back-up](/sql/t-sql/statements/backup-master-key-transact-sql)
- [Certificaat machtigingen verlenen](/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
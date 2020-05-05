---
title: Op rollen gebaseerd beheer programma
titleSuffix: Configuration Manager
description: Gebruik het op rollen gebaseerd beheer en controle programma om beveiligings rollen en bereiken in Configuration Manager te model leren en te controleren.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff940db21711aabb5d57a45b05d90d04415639bb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723185"
---
# <a name="role-based-administration-and-auditing-tool"></a>Hulpprogramma voor beheer en controle op basis van rollen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het beheer-en controle programma op basis van rollen is een van de [Configuration Manager-hulpprogram ma's](tools.md). Gebruik dit hulp programma voor de volgende taken:

- Model beveiligings rollen met specifieke machtigingen  

- Controleer de beveiligingsbereiken en beveiligings rollen die andere gebruikers hebben



## <a name="requirements"></a>Vereisten

- Uitvoeren op dezelfde computer als de Configuration Manager-console  

- U hebt de rol **volledige beheerder**, **alleen-lezen analist**of **beveiligings beheerder**  

- Uw account toewijzen aan het beveiligings bereik **alle** en alle verzamelingen  

- (*Optioneel*) Voor het analyseren van de beveiliging van rapportmap moet u SQL-toegang hebben  

- (*Optioneel*) Als u rapport analyse wilt analyseren, voert u dit hulp programma uit op de site systeem server met de rapportage punt rol



## <a name="procedures"></a>Procedures


### <a name="model-permissions-for-a-new-role"></a>Model machtigingen voor een nieuwe rol

Gebruik de volgende procedure om machtigingen te modelsen voor een nieuwe rol die u wilt maken: 

1. Voer **RBAViewer. exe**uit.  

2. Selecteer de basis beveiligings rollen die u wilt bouwen, of begin met een lege machtigingenset. Selecteer de benodigde machtigingen.  

3. Klik op **analyseren** om de gebruikers interface te zien die door deze aangepaste rol wordt weer geven.  

    > [!Note]  
    > Als u wilt zien of er een bestaande beveiligingsrol is die aan uw vereisten voldoet, gaat u naar het tabblad **gelijkenis** .  

4. Klik op **exporteren** om de rol op te slaan als een XML-bestand. Importeer deze vervolgens naar de Configuration Manager-console. Zie [aangepaste beveiligings rollen maken](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)voor meer informatie.


### <a name="audit-existing-security-scopes"></a>Bestaande beveiligingsbereiken controleren

Gebruik de volgende procedure om alle bestaande gebruikers met beheerders rechten, verzamelingen en beveiligingsbereiken in Configuration Manager te controleren:

1. Voer **RBAViewer. exe**uit.  

2. Selecteer de knop **controle RBA** in de werk balk.  

    1. Als u de relaties verzameling-beperkt in een structuur weergave wilt weer geven, gaat u naar het tabblad Overzicht van de **verzameling** .  

    2. Als u objecten wilt weer geven die aan een beveiligingsrol zijn toegewezen, gaat u naar het tabblad **Scope Summary** .  


### <a name="audit-a-specific-user"></a>Een specifieke gebruiker controleren

Gebruik de volgende procedure om de op rollen gebaseerde beheer configuratie voor een specifieke gebruiker te controleren:

1. Voer **RBAViewer. exe**uit.  

2. Selecteer de knop **uitvoeren als** op de werk balk.  

3. Voer de specifieke gebruikers naam in om de machtigingen voor dat account te controleren.  

4. In het hulp programma worden de beveiligings rollen weer gegeven die zijn toegewezen aan de gebruiker of de beveiligings groep waartoe de gebruiker behoort. Ook worden de objecten weer gegeven die deze gebruiker kan zien en de acties die ze in de-console kunnen uitvoeren.  



## <a name="see-also"></a>Zie ook

- [Basisprincipes voor beheer op basis van rollen](../understand/fundamentals-of-role-based-administration.md)
- [Beheer op basis van rollen configureren](../servers/deploy/configure/configure-role-based-administration.md)

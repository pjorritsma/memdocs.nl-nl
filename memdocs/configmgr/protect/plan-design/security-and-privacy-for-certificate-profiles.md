---
title: Beveiliging en privacy voor certificaatprofielen
titleSuffix: Configuration Manager
description: Meer informatie over de aanbevolen beveiligings procedures voor het beheren van certificaat profielen voor gebruikers en apparaten in Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f73a556f28f8ebe4abf6e762104776b40b0cd0e8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697021"
---
# <a name="security-and-privacy-for-certificate-profiles-in-configuration-manager"></a>Beveiliging en privacy voor certificaat profielen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Aanbevolen beveiligingsprocedures voor certificaatprofielen  
 Gebruik de volgende aanbevolen beveiligingsprocedures wanneer u certificaatprofielen beheert voor gebruikers en apparaten.  

|Aanbevolen beveiligingsprocedure|Meer informatie|  
|----------------------------|----------------------|  
|Bepaal en volg alle aanbevolen beveiligingsprocedures voor de registratieservice voor netwerkapparaten, waaronder het configureren van de website van de Registratieservice voor netwerkapparaten in Internet Information Services (IIS) om SSL te vereisen en clientcertificaten te negeren.|Zie [richt lijnen voor registratie service voor netwerk apparaten](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11))voor meer informatie.|  
|Kies bij het configureren van SCEP-certificaatprofielen de veiligste opties die door de apparaten en uw infrastructuur worden ondersteund.|Bepaal, implementeer en volg alle 'best practice' beveiligingsprocedures die voor uw apparaten en infrastructuur worden aanbevolen.|  
|Geef handmatig de gebruikersaffiniteit met apparaat op in plaats van gebruikers toe te staan hun primaire apparaat te identificeren. Zorg daarnaast dat op gebruik gebaseerde configuratie niet is ingeschakeld.|Als u op de optie **Alleen certificaatinschrijving op het primaire apparaat van gebruikers toestaan** in een SCEP-certificaatprofiel klikt, moet u de informatie die van gebruikers of van het apparaat wordt verzameld niet als gezaghebbend beschouwen. Als u SCEP-certifcaatprofielen bij deze configuratie implementeert en een vertrouwde gebruiker met beheerdersrechten geeft de gebruikersaffiniteit met apparaat niet op, dan kunnen onbevoegde gebruikers verhoogde bevoegdheden krijgen en kunnen certificaten worden verleend voor verificatie.<br /><br /> **Opmerking:** Als u de op gebruik gebaseerde configuratie inschakelt, wordt deze informatie verzameld met behulp van status berichten die niet zijn beveiligd door Configuration Manager. Gebruik om deze dreiging te voorkomen, SMB-ondertekening of IPsec tussen clientcomputers en het beheerpunt.|  
|Voeg geen lees- en registratiemachtigingen toe aan de certificaatsjablonen of configureer het certificaatregistratiepunt om de certificaatsjablooncontrole over te slaan.|Hoewel Configuration Manager de aanvullende controle ondersteunt als u de beveiligings machtigingen voor lezen en inschrijven voor gebruikers toevoegt en u het certificaat registratiepunt kunt configureren om deze controle over te slaan als verificatie niet mogelijk is, is de configuratie geen beveiligings best practice. Zie [plannen voor certificaat sjabloon machtigingen voor certificaat profielen](../../protect/plan-design/planning-for-certificate-template-permissions.md)voor meer informatie.|  

## <a name="privacy-information-for-certificate-profiles"></a>Privacyinformatie voor certificaatprofielen  
 U kunt certificaatprofielen gebruiken om de basiscertificeringsinstantie (CA) en clientcertificaten te implementeren en om te evalueren of die apparaten compatibel zijn nadat de profielen zijn toegepast. Het beheer punt verzendt compatibiliteits informatie naar de site server en Configuration Manager die informatie opslaat in de site database. Compatibiliteitsinformatie omvat certificaateigenschappen zoals onderwerpnaam en vingerafdruk. De informatie wordt versleuteld wanneer apparaten deze naar het beheerpunt verzenden, maar deze wordt niet in een versleutelde indeling opgeslagen in de sitedatabase. De informatie wordt in de database behouden totdat deze door de siteonderhoudstaak **Verouderde gegevens van Configuration Manager verwijderen** na de standaardintervaltijd van 90 dagen wordt verwijderd. U kunt het verwijderingsinterval configureren. Er wordt geen compatibiliteitsinformatie naar Microsoft verzonden.  

 Certificaat profielen gebruiken informatie die Configuration Manager verzameld met behulp van detectie. Voor meer informatie over privacy-informatie voor detectie raadpleegt u de sectie **Privacy-informatie voor detectie** in [beveiliging en privacy voor Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

> [!NOTE]  
>  Aan gebruikers of apparaten uitgegeven certificaten staan mogelijk toegang toe tot vertrouwelijke informatie.  

 Standaard worden certificaatprofielen niet door apparaten geëvalueerd. Bovendien moet u de certificaatprofielen configureren en vervolgens implementeren voor gebruikers of apparaten.  

 Voordat u certificaatprofielen configureert, moet u nadenken over uw privacyvereisten.
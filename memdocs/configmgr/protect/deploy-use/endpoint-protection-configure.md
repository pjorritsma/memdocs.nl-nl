---
title: Endpoint Protection configureren
titleSuffix: Configuration Manager
description: Meer informatie over het instellen van Configuration Manager voor het bijwerken en distribueren van malware-definities voor Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e48f20dd56f445a10faa485b8bb7e86dbb05f75a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720882"
---
# <a name="configure-endpoint-protection"></a>Endpoint Protection configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u Endpoint Protection kunt gebruiken om beveiliging en malware op Configuration Manager-client computers te beheren, moet u de configuratie stappen uitvoeren die in dit artikel worden beschreven.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Endpoint Protection configureren in Configuration Manager  
 Endpoint Protection in Configuration Manager heeft externe afhankelijkheden en afhankelijkheden in het product.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Stappen voor het configureren van Endpoint Protection in Configuration Manager  
 In de volgende tabel vindt u de stappen, gegevens en overige informatie voor het configureren van Endpoint Protection.  

> [!IMPORTANT]  
>  Als u Endpoint Protection voor Windows 10-computers beheert, moet u Configuration Manager configureren voor het bijwerken en distribueren van malware-definities voor Windows Defender. Windows Defender is opgenomen in Windows 10, maar SCEPInstall moet nog steeds zijn geïnstalleerd en aangepaste client instellingen voor Endpoint Protection (**stap 5** hieronder) zijn nog steeds vereist. </br> </br>
> Vanaf Configuration Manager 1802 kunnen Windows 10-apparaten de Endpoint Protection-agent (SCEPInstall) niet installeren. Als deze al is geïnstalleerd op Windows 10-apparaten, wordt deze niet door Configuration Manager verwijderd. Beheerders kunnen de Endpoint Protection-agent op Windows 10-apparaten waarop ten minste de 1802-client versie wordt uitgevoerd, verwijderen. SCEPInstall. exe is mogelijk nog wel aanwezig in C:\Windows\ccmsetup op sommige computers, maar moet niet worden gedownload op nieuwe client installaties. Aangepaste client instellingen voor Endpoint Protection (**stap 5** hieronder) zijn nog steeds vereist. <!--503654-->

|Stappen|Details|  
|-----------|-------------|  
|**Stap 1:** [een site systeemrol Endpoint Protection punt maken](endpoint-protection-site-role.md)|De sitesysteemrol Endpoint Protection-punt moet zijn geïnstalleerd voordat u Endpoint Protection kunt gebruiken. Het moet slechts op één sitesysteemserver en op het hoogste niveau in de hiërarchie op een centrale beheersite of een zelfstandige primaire site worden geïnstalleerd. |  
|**Stap 2:** [waarschuwingen voor Endpoint Protection configureren](endpoint-configure-alerts.md)|Met waarschuwingen wordt de beheerder op de hoogte gebracht van specifieke gebeurtenissen die hebben plaatsgevonden, zoals een malware-infectie. Waarschuwingen worden weergegeven in het knooppunt **Waarschuwingen** van de werkruimte **Bewaking** of kunnen eventueel via e-mail naar de opgegeven gebruikers worden verzonden. |  
|**Stap 3:** [definitie-update bronnen voor Endpoint Protection-clients configureren](endpoint-definition-updates.md)|Endpoint Protection kunnen worden geconfigureerd voor het gebruik van verschillende bronnen voor het downloaden van definitie-updates. |  
|**Stap 4:** [het standaard beleid voor antimalware configureren en aangepaste antimalwarebeleid maken](endpoint-antimalware-policies.md)|Het standaard beleid voor antimalware wordt toegepast wanneer de Endpoint Protection-client wordt geïnstalleerd. Aangepaste beleidsregels die u hebt geïmplementeerd, worden standaard binnen 60 minuten na het implementeren van de client toegepast. Zorg ervoor dat u het antimalwarebeleid hebt geconfigureerd voordat u de Endpoint Protection-client implementeert. |  
|**Stap 5:** [aangepaste client instellingen voor Endpoint Protection configureren](endpoint-protection-configure-client.md)|Gebruik aangepaste client instellingen voor het configureren van Endpoint Protection instellingen voor verzamelingen computers in uw hiërarchie.<br /><br /> Opmerking: Configureer de standaard instellingen voor de client Endpoint Protection alleen als u zeker weet dat u deze instellingen wilt Toep assen op alle computers in uw hiërarchie. |  

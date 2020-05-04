---
title: Clientmeldingen
titleSuffix: Configuration Manager
description: Clients beheren door onmiddellijk actie te ondernemen vanuit de console Central Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a00f77a5a902728a7c41905314511cffcfa81a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714092"
---
# <a name="client-notification-in-configuration-manager"></a>Client melding in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u onmiddellijk actie wilt ondernemen op externe clients, verzendt u een actie voor client meldingen vanuit de Configuration Manager-console. Start deze acties op een afzonderlijk apparaat of op een verzameling apparaten.

## <a name="actions"></a>Acties

De volgende acties bevinden zich op het lint van het tabblad Start in het apparaat of de verzamelings groep.

### <a name="install-client"></a>Client installeren

Hiermee opent u de **wizard Client installeren**. Deze wizard maakt gebruik van client push installatie om een Configuration Manager-client te installeren. Zie [client push Installation](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)(Engelstalig) voor meer informatie.

#### <a name="permissions---install-client"></a>Machtigingen-client installeren

Deze actie vereist de machtigingen **resource wijzigen** en **lezen** voor het **verzamelings** object.

De volgende ingebouwde rollen hebben standaard deze machtigingen:

- Toepassingsbeheerder  
- Volledige beheerder  
- Infrastructuurbeheerder  
- Bewerkingenbeheerder  
- Deployment Manager van besturings systeem  

Voeg deze machtigingen toe aan aangepaste rollen die de client moeten pushen.

### <a name="run-script"></a>Script uitvoeren

Hiermee opent u de wizard **script uitvoeren** om een Power shell-script uit te voeren op alle clients in de verzameling. Zie [Power shell-scripts maken en uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md)voor meer informatie.

#### <a name="permissions---run-script"></a>Machtigingen-Script uitvoeren

Deze actie vereist de machtiging voor het uitvoeren van een **script** voor het **verzamelings** object.

De volgende ingebouwde rollen hebben standaard deze machtiging:

- Volledige beheerder  
- Infrastructuurbeheerder  
- Bewerkingenbeheerder  

Voeg deze machtiging toe aan aangepaste rollen die scripts moeten uitvoeren.

### <a name="start-cmpivot"></a>CMPivot starten

Start **CMPivot**, waarmee realtime query's worden uitgevoerd op de doel apparaten. Zie [CMPivot](../../servers/manage/cmpivot.md)voor meer informatie.

#### <a name="permissions---start-cmpivot"></a>Machtigingen-start CMPivot

Voor deze actie zijn dezelfde machtigingen vereist als voor de actie [script uitvoeren](#run-script) .

Vanaf versie 1906 kunt u de machtiging **CMPivot uitvoeren** gebruiken voor het object **verzameling** .

## <a name="client-notification"></a>Clientmeldingen

Deze acties bevinden zich onder het menu voor **client meldingen** op het lint in het apparaat of de groep met verzamelingen van het tabblad Start.

In versie 1806 of eerder is de optie **client melding** alleen beschikbaar via het knoop punt van de verzameling apparaten of wanneer u het lidmaatschap van een verzameling apparaten hebt bekeken. Vanaf versie 1810 kunt u een **client melding** rechtstreeks starten vanuit het knoop punt **apparaten** . Het is niet meer nodig om binnen de weer gave van het verzamelings lidmaatschap te vallen. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>Machtigingen-client melding

<!--SCCMDocs-pr issue #2972-->
Vanaf versie 1810 is voor client meldings acties nu de machtiging **resource waarschuwen** voor het verzamelings object. Deze machtiging is van toepassing op alle acties in het **client meldings** menu.

De volgende ingebouwde rollen hebben standaard deze machtiging:

- Volledige beheerder  
- Bewerkingenbeheerder  

Voeg deze machtiging toe aan aangepaste rollen die client meldings acties moeten gebruiken.

### <a name="download-computer-policy"></a>Computer beleid downloaden

Het apparaatbeleid vernieuwen. Zie [het ophalen van beleid initiëren voor een Configuration Manager-client](manage-clients.md#BKMK_PolicyRetrieval)voor meer informatie.  

### <a name="download-user-policy"></a>Gebruikers beleid downloaden

Het gebruikers beleid vernieuwen.  

### <a name="collect-discovery-data"></a>Detectie gegevens verzamelen

Clients activeren om een detectie gegevens record (DDR) te verzenden. Zie [heartbeat-detectie](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)voor meer informatie.  

### <a name="collect-software-inventory"></a>Software-inventaris verzamelen

Clients activeren om een software-inventarisatie cyclus uit te voeren. Zie [Inleiding tot software-inventarisatie](inventory/introduction-to-software-inventory.md)voor meer informatie.  

### <a name="collect-hardware-inventory"></a>Hardware-inventaris verzamelen

Clients activeren om een hardware-inventarisatie cyclus uit te voeren. Zie [Inleiding op Hardware-inventarisatie](inventory/introduction-to-hardware-inventory.md)voor meer informatie.  

### <a name="evaluate-application-deployments"></a>Toepassings implementaties evalueren

Clients activeren om een evaluatie cyclus voor de implementatie van een toepassing uit te voeren. Zie [opnieuw evaluatie voor implementaties plannen](../deploy/about-client-settings.md#schedule-re-evaluation-for-deployments)voor meer informatie.  

### <a name="evaluate-software-update-deployments"></a>Implementaties van software-updates evalueren

Clients activeren om een evaluatie cyclus voor implementatie van software-updates uit te voeren. Zie [Introduction to software updates](../../../sum/understand/software-updates-introduction.md)(Engelstalig) voor meer informatie.  

### <a name="switch-to-the-next-software-update-point"></a>Overschakelen naar het volgende software-update punt

Clients activeren om over te scha kelen naar het volgende beschik bare software-update punt. Zie [Software-update punt switching](../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching)(Engelstalig) voor meer informatie.  

### <a name="evaluate-device-health-attestation"></a>Apparaatstatusverklaring evalueren

Activeer Windows 10-clients om de nieuwste Apparaatstatus te controleren en te verzenden. Zie [Health Attestation](../../servers/manage/health-attestation.md)voor meer informatie.  

### <a name="wake-up"></a>Word wakker

Vanaf versie 1810 worden apparaten geactiveerd die zijn geconfigureerd voor ondersteuning van Wake-on-LAN om te activeren met andere apparaten in hetzelfde subnet om het Wake-on-LAN-pakket te verzenden. Zie [Wake on LAN configureren](../deploy/configure-wake-on-lan.md)voor meer informatie.

### <a name="restart"></a>Opnieuw starten

De geselecteerde apparaten activeren om opnieuw op te starten. Zie [clients opnieuw starten](manage-clients.md#restart-clients)voor meer informatie.

## <a name="client-diagnostics"></a>Diagnostische gegevens van client
<!--4433455-->

Vanaf versie 1910 zijn er nieuwe acties voor **client diagnostiek** in de Configuration Manager-console. De volgende acties zijn toegevoegd:

- **Uitgebreide logboek registratie inschakelen**: Wijzig het globale logboek niveau voor het onderdeel CCM in uitgebreid en schakel logboek registratie voor fout opsporing in.
- **Uitgebreide logboek registratie uitschakelen**: Wijzig het globale logboek niveau in standaard en schakel logboek registratie voor fout opsporing uit.
- **Client logboeken verzamelen** (vanaf 2002): er wordt een bericht voor client meldingen verzonden naar de geselecteerde clients om de CCM-logboeken te verzamelen. De logboeken worden geretourneerd met behulp van de bestands verzameling van de software-inventarisatie. <!--4226618-->
   - De maximale grootte voor de gecomprimeerde client Logboeken is 100 MB. <!--6366098-->
   - [Resource Explorer](inventory/use-resource-explorer-to-view-software-inventory.md#bkmk_diag) gebruiken om deze bestanden te beheren en weer te geven.

   [![Client logboeken verzamelen via de-console](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - Met deze acties wordt alleen de uitgebreidheid van het logboek gewijzigd, niet de grootte of de geschiedenis. Uitgebreide logboek registratie kan meer logboek inhoud genereren.
> - De rol beheer punt gebruikt ook het onderdeel CCM. Als het doel apparaat ook een beheer punt is, is deze actie ook van toepassing op die rol.

Zie [over logboek bestanden](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client)voor meer informatie over deze instellingen.

Volg de status van de taak in het **diagnose. log** op de client. Wanneer client logboeken worden verzameld, wordt er aanvullende informatie geregistreerd in **MP_SinvCollFile. log** op het beheer punt en **bestand sinvproc. log** op de site server.

### <a name="prerequisites---client-diagnostics"></a>Vereisten-diagnostische gegevens van client

- Werk de doel-client bij naar de meest recente versie.

- Uw Configuration Manager gebruiker met beheerders rechten heeft de machtiging **resource melden** nodig.

  De volgende ingebouwde rollen hebben standaard deze machtiging:

  - Volledige beheerder  
  - Infrastructuurbeheerder  

  Voeg deze machtiging toe aan aangepaste rollen die client meldings acties moeten gebruiken.


## <a name="endpoint-protection"></a>Endpoint Protection

De volgende acties bevinden zich onder het **Endpoint Protection** -menu. Dit menu bevindt zich op het lint in de verzamelings groep van het tabblad Start. Wanneer u een of meer apparaten selecteert, bevinden deze acties zich op het **geselecteerde object** tabblad van het lint.

Zie [Endpoint Protection in Configuration Manager](../../../protect/deploy-use/endpoint-protection.md)voor meer informatie.

### <a name="permissions---endpoint-protection"></a>Machtigingen-Endpoint Protection

Deze actie vereist de machtiging **beveiliging afdwingen** voor het **verzamelings** object.

De volgende ingebouwde rollen hebben standaard deze machtiging:

- Volledige beheerder  
- Endpoint Protection-beheerder  
- Bewerkingenbeheerder  

Voeg deze machtiging toe aan aangepaste rollen die Endpoint Protection acties moeten activeren.

### <a name="full-scan"></a>Volledige scan

Activeer Endpoint Protection of Windows Defender om een *volledige* malware-scan uit te voeren.  

### <a name="quick-scan"></a>Snelle scan

Activeer Endpoint Protection of Windows Defender om een *snelle* antimalware-scan uit te voeren.  

### <a name="download-definition"></a>Definitie downloaden

Activeer Endpoint Protection of Windows Defender om de nieuwste antimalware-definities te downloaden.  

## <a name="see-also"></a>Zie ook

- [Clients beheren](manage-clients.md)
- [Verzamelingen beheren](collections/manage-collections.md)

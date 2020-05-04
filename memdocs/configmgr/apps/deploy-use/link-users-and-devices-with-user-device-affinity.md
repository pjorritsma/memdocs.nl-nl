---
title: Gebruikers en apparaten koppelen met affiniteit met apparaat van gebruiker
titleSuffix: Configuration Manager
description: Gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat en apps automatisch implementeren op alle apparaten die aan een gebruiker zijn gekoppeld.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2e74f969016d79254ceb8e8323b6e3914969ecc7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710095"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-configuration-manager"></a>Gebruikers en apparaten koppelen met affiniteit tussen gebruiker en apparaat in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruikers affiniteit apparaat in Configuration Manager koppelt een gebruiker aan een of meer apparaten. Dit gedrag kan de nood zaak om de namen van de apparaten van een gebruiker te weten, te elimineren voor het implementeren van een toepassing voor de gebruiker. In plaats van de toepassing te implementeren op elk van de apparaten van de gebruiker, implementeert u de toepassing voor de gebruiker. Gebruikers affiniteit met apparaat zorgt er dan automatisch voor dat de toepassing wordt geïnstalleerd op alle apparaten die aan die gebruiker zijn gekoppeld.  

Definieer primaire apparaten die gebruikers elke dag voor hun werk gebruiken. Wanneer u affiniteit tussen een gebruiker en een apparaat instelt, beschikt u over meer implementatieopties voor apps. Als een gebruiker bijvoorbeeld micro soft Visio vereist, kunt u deze op het primaire apparaat van de gebruiker installeren met behulp van een Windows Installer-implementatie. Op een apparaat dat geen primair apparaat is, kunt u echter Visio als een virtuele toepassing implementeren. U kunt gebruikers affiniteit met apparaat ook gebruiken om software te implementeren op het apparaat van een gebruiker wanneer de gebruiker niet is aangemeld. Wanneer de gebruiker zich aanmeldt, is de app al geïnstalleerd en klaar om te worden uitgevoerd.  

U kunt gegevens van affiniteit van gebruikers apparaat alleen voor computers beheren. Configuration Manager beheert automatisch affiniteiten tussen gebruikers en apparaten voor de mobiele apparaten die het registreert.  

## <a name="manually-set-up-user-device-affinity"></a>Gebruikers affiniteit met apparaat hand matig instellen  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **apparaten** .  

1. Selecteer een apparaat. Klik op het tabblad **Start** in het lint in de groep **apparaat** op **primaire gebruikers bewerken**.  

1. Zoek en selecteer in het dialoog venster **primaire gebruikers bewerken** de gebruikers die u wilt toevoegen als primaire gebruikers voor het geselecteerde apparaat. Kies **toevoegen**.  

    > [!NOTE]  
    > In de lijst **primaire gebruikers** worden de gebruikers weer gegeven die al primaire gebruikers van dit apparaat zijn en de methode waarmee elke relatie tussen gebruikers en apparaten is toegewezen.  

## <a name="set-up-primary-devices-for-a-user"></a>Primaire apparaten voor een gebruiker instellen  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **gebruikers** .  

1. Selecteer een gebruiker. Kies op het tabblad **apparaat** in het lint de optie **primaire apparaten bewerken**.  

1. Zoek in het dialoog venster **primaire apparaten bewerken** de apparaten die u als primaire apparaten voor de geselecteerde gebruiker wilt toevoegen en selecteer deze. Kies **toevoegen**.  

    > [!NOTE]  
    > In de lijst **primaire apparaten** worden de apparaten weer gegeven die al zijn ingesteld als primaire apparaten voor deze gebruiker en de methode waarmee elke relatie tussen gebruikers en apparaten is toegewezen.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Automatisch affiniteit tussen gebruikers en apparaten instellen (alleen Windows-pc's)

Configuration Manager leest gegevens over gebruikers aanmeldings gebeurtenissen vanuit het Windows-gebeurtenis logboek. Als u automatisch affiniteiten tussen gebruikers en apparaten wilt maken, schakelt u deze twee opties in het lokale beveiligings beleid op client computers in om aanmeldings gebeurtenissen op te slaan in het Windows-gebeurtenis logboek:  

- **Aanmeldingsgebeurtenissen voor accounts controleren**  
- **Aanmeldingsgebeurtenissen controleren**  

Als u deze instellingen wilt configureren, gebruikt u Windows groepsbeleid.  

> [!IMPORTANT]  
> Als er een fout optreedt in het Windows-gebeurtenis logboek om een groot aantal vermeldingen te genereren, kan er een nieuw gebeurtenis logboek worden gemaakt. Als dit probleem zich voordoet, zijn bestaande aanmeldings gebeurtenissen mogelijk niet beschikbaar voor Configuration Manager.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>De site instellen om automatisch gebruikers affiniteit met apparaten te maken  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **client instellingen** .  

1. Als u de standaard client instellingen wilt wijzigen, selecteert u **standaard client instellingen**. Klik op het tabblad **Start** in het lint in de groep **Eigenschappen** op **Eigenschappen**.

    Als u aangepaste instellingen voor de client agent wilt maken, kiest u in het tabblad **Start** van het lint in de groep **maken** de optie **aangepaste instellingen voor client apparaten maken**.

    > [!NOTE]  
    > Als u de standaard client instellingen wijzigt, wordt deze door de site geïmplementeerd op alle computers in de hiërarchie. Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor meer informatie.  

1. Stel in de **affiniteits groep van gebruiker en apparaat** de volgende instellingen in:  

    - **Drempel waarde voor affiniteit van gebruiker met apparaat (minuten)**: Stel het aantal minuten in dat het apparaat wordt gebruikt voordat de site een gebruikers affiniteit apparaat maakt.  

    - **Drempel waarde voor affiniteit van gebruiker met apparaat (dagen)**: Stel het aantal dagen in waarover de site de drempel waarde voor affiniteit op basis van het gebruik meet.  

    - **Affiniteit van gebruiker met apparaat automatisch configureren op basis van gebruiks gegevens**: Selecteer **waar** om de site automatisch affiniteit tussen gebruikers en apparaten te laten maken. Als u **Onwaar**selecteert, moet u alle toewijzingen van affiniteit tussen gebruikers en apparaten hand matig goed keuren.  

    > [!TIP]  
    > Als u bijvoorbeeld de **drempel waarde voor affiniteit tussen gebruikers en apparaten (minuten)** instelt op **60** minuten en u de **drempel waarde voor gebruikers affiniteit (dagen)** instelt op **5** dagen, moet de gebruiker het apparaat gedurende een periode van 5 dagen ten minste 60 minuten gebruiken om automatisch een gebruikers affiniteit met apparaat te maken.  

Nadat Configuration Manager een automatische gebruikers affiniteit voor apparaten hebt gemaakt, blijft de drempel waarde van de gebruikers affiniteit van het apparaat worden bewaakt. Als de activiteit van de gebruiker voor het apparaat onder de drempel waarden valt die u hebt ingesteld, wordt de gebruikers affiniteit met apparaat verwijderd. Stel de **affiniteits drempel van het gebruikers apparaat (dagen)** in op een waarde van ten minste zeven dagen. Deze configuratie vermijdt situaties waarin een automatisch geconfigureerde gebruikers affiniteit van het apparaat mogelijk verloren gaat wanneer de gebruiker niet is aangemeld, bijvoorbeeld tijdens het weekend.  


## <a name="import-user-device-affinities-from-a-file"></a>Affiniteiten tussen gebruikers en apparaten importeren vanuit een bestand

Als u een groot aantal relaties tegelijk wilt maken, importeert u een bestand met de Details voor meerdere gebruikers affiniteit met apparaat. Zorg ervoor dat de doel apparaten al zijn gedetecteerd door de site en als resources zijn opgenomen in de Configuration Manager-Data Base.  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **gebruikers** of **apparaten** .  

1. Klik op het tabblad **Start** in het lint, in de groep **maken** , op **gebruiker apparaat-affiniteit importeren**.  

1. Stel in de wizard affiniteit van gebruiker met apparaat importeren op de pagina **toewijzing kiezen** de volgende gegevens in:  

    - **Bestands naam**. Geef een bestand met door komma's gescheiden waarden (CSV) op dat een lijst bevat met gebruikers en apparaten waartussen u een affiniteit wilt maken. In dit bestand moet elke combi natie van een gebruiker en apparaat op een eigen rij staan, met waarden gescheiden door een komma. Gebruik deze indeling:`<domain>\<username>,<device NetBIOS name>`  

    - **Dit bestand heeft kolom koppen voor referentie doeleinden**. Selecteer deze optie als het CSV-bestand een kop van de bovenste rij bevat. De-site negeert de veldnamenrij tijdens het importeren.  

1. Als het bestand dat u importeert meer dan twee items in elke rij bevat, gebruikt u **kolom** en **toewijzen** om op te geven welke kolommen gebruikers en apparaten vertegenwoordigen en welke kolommen tijdens het importeren moeten worden genegeerd.  

1. Voltooi de wizard.  


## <a name="let-users-create-their-own-device-affinities"></a>Gebruikers de mogelijkheid geven om hun eigen affiniteit voor apparaten te maken

Stel een gebruiker in om een eigen gebruikers affiniteit met apparaat te maken in Software Center.

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>De site instellen zodat gebruikers affiniteits aanvragen van gebruikers apparaten kunnen maken  

1 Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **client instellingen** .  

1. Als u de standaard client instellingen wilt wijzigen, selecteert u **standaard client instellingen**. Klik op het tabblad **Start** in het lint in de groep **Eigenschappen** op **Eigenschappen**.

    Als u aangepaste instellingen voor client agent wilt maken, klikt u op het tabblad **Start** in het lint in de groep **maken** op **aangepaste client gebruikers instellingen maken**.

    > [!NOTE]  
    > Als u de standaard client instellingen wijzigt, wordt deze door de site geïmplementeerd op alle computers in de hiërarchie. Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor meer informatie.  

1. Schakel in de **affiniteits groep van gebruiker en apparaat** de instelling in om de **gebruiker toe te staan hun primaire apparaten te definiëren**.  

### <a name="set-up-a-user-device-affinity-in-software-center"></a>Gebruikers affiniteit met apparaat instellen in Software Center

Vanaf versie 1902 gebruikt u Software Center om affiniteit in te stellen.

1. Ga in Software Center naar het tabblad **Opties** .

1. Selecteer in het gedeelte **werk informatie** de optie **Ik gebruik deze computer regel matig voor mijn werk**.

### <a name="set-up-a-user-device-affinity-in-the-application-catalog"></a>Een affiniteit tussen gebruikers en apparaten instellen in de toepassings catalogus

> [!Important]
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

1. Kies in de Application Catalog **Mijn systemen**.  

1. Selecteer de optie **Ik gebruik deze computer regel matig voor mijn werk**.  


## <a name="manage-user-device-affinity-requests-from-users"></a>Aanvragen van gebruikers voor affiniteit tussen gebruikers en apparaten beheren

Wanneer u de client instelling uitschakelt om de **gebruikers affiniteit van het apparaat automatisch te configureren op basis van gebruiks gegevens**, moet u alle toewijzingen van affiniteit tussen gebruikers en apparaten hand matig goed keuren.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Een affiniteits aanvraag van een gebruiker met apparaat goed keuren of afwijzen  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** .  

1. Selecteer de gebruiker of het apparaat waarvoor u affiniteits aanvragen wilt beheren.  

1. Klik op het tabblad **Start** op het lint in de groep **verzameling** op **affiniteits aanvragen beheren**.  

1. Selecteer een affiniteits aanvraag in het dialoog venster **affiniteits aanvragen van gebruikers apparaten beheren** en kies vervolgens **goed keuren** of **afwijzen**.  


## <a name="next-steps"></a>Volgende stappen

U kunt ook Microsoft Intune gebruiken om het primaire gebruik van een geregistreerd apparaat te zoeken. Zie [de primaire gebruiker van een intune-apparaat zoeken](https://docs.microsoft.com/intune/find-primary-user) in de intune-documentatie voor meer informatie.

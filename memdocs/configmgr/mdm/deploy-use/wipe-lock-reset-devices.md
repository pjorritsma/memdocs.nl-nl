---
title: Apparaten beheren met on-premises MDM
titleSuffix: Configuration Manager
description: Beveilig apparaatgegevens met volledig wissen, selectief wissen, vergren delen op afstand of wachtwoord code opnieuw instellen met behulp van Configuration Manager on-premises Mobile Device Management (MDM).
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9849f3bef5aa67dcc45b00f64487242230edc2e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721869"
---
# <a name="manage-devices-and-protect-data-with-on-premises-mdm-in-configuration-manager"></a>Apparaten beheren en gegevens beveiligen met on-premises MDM in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Mobiele apparaten kunnen gevoelige gegevens opslaan en eenvoudig toegang bieden tot veel organisatie bronnen. Als u apparaten en gegevens wilt beveiligen, gebruikt u Configuration Manager voor de volgende acties voor Apparaatbeheer:

- **Volledig wissen**: de fabrieks instellingen van het apparaat herstellen

- **Selectief wissen**: alleen organisatie gegevens verwijderen

- **Wachtwoord code opnieuw instellen**: de wachtwoord code verwijderen of opnieuw instellen wanneer een gebruiker deze vergeet

- **Extern vergren delen**: een apparaat beveiligen dat mogelijk verloren is gegaan

## <a name="full-wipe"></a>Volledig wissen  

Wanneer u een apparaat wilt beveiligen of wanneer u een apparaat buiten gebruik wilt stellen, kunt u het volledig wissen. Met deze actie wordt het apparaat teruggezet naar de fabrieks instellingen. Hiermee worden alle bedrijfs-en gebruikers gegevens en-instellingen verwijderd.

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en kies het knoop punt **apparaten** . U kunt ook **apparaat verzamelingen** kiezen en een verzameling selecteren waarvan het apparaat lid is.

1. Selecteer het apparaat dat u wilt wissen.

1. Selecteer op het lint, in de groep apparaat, **acties extern apparaat**en kies vervolgens **buiten gebruik stellen/wissen**.

1. Selecteer in het venster **buiten gebruik stellen vanuit Configuration Manager** de optie voor **het wissen van het mobiele apparaat en het buiten gebruik stellen van Configuration Manager**.

## <a name="selective-wipe"></a>Selectief wissen

Als u alleen de organisatie gegevens van een apparaat wilt verwijderen, start u een selectief wissen.

### <a name="behaviors-by-os-version"></a>Gedragingen op besturingssysteem versie

In de volgende tabellen wordt beschreven welke gegevens worden verwijderd en wat het effect is op de gegevens die op het apparaat achterblijven na selectief wissen.

#### <a name="windows-10-windows-81-windows-rt-81-and-windows-rt"></a>Windows 10, Windows 8,1, Windows RT 8,1 en Windows RT

|Inhoud|Gedrag van selectief wissen|  
|-------|--------|
|Apps en gekoppelde gegevens die door Configuration Manager zijn geïnstalleerd|De apps worden verwijderd en alle sideloading-codes worden verwijderd. De versleutelings sleutel wordt ingetrokken voor apps die gebruikmaken van Windows selectief wissen, en de gegevens zijn niet meer toegankelijk.|
|VPN- en Wi-Fi-profielen|Hiermee verwijdert u de profielen|
|Certificaten|Hiermee worden de certificaten verwijderd en ingetrokken|
|Instellingen|Vereisten worden verwijderd|
|E-mailprofielen|Hiermee verwijdert u e-mail berichten waarvoor EFS is ingeschakeld. Dit omvat de e-mail-app voor Windows-e-mail en bijlagen.|

#### <a name="windows-10-mobile-windows-phone-80-and-windows-phone-81"></a>Windows 10 Mobile, Windows Phone 8,0 en Windows Phone 8,1

|Inhoud|Gedrag van selectief wissen|  
|-------|--------|
|Bedrijfs-apps en de bijbehorende gegevens die zijn geïnstalleerd door Configuration Manager|Hiermee worden de apps verwijderd en worden de app-gegevens van de organisatie verwijderd.|
|VPN- en Wi-Fi-profielen|Hiermee verwijdert u de profielen voor Windows 10 Mobile en Windows Phone 8,1|
|Certificaten|Hiermee verwijdert u de certificaten voor Windows Phone 8,1|
|E-mailprofielen|Hiermee verwijdert u de profielen (met uitzonde ring van Windows Phone 8,0)|

De volgende instellingen worden ook verwijderd van Windows 10 Mobile-en Windows Phone 8,1-apparaten:  

- **Wachtwoord vereist voor het ontgrendelen van mobiele apparaten**  
- **Eenvoudige wachtwoorden toestaan**  
- **Minimale wachtwoordlengte**  
- **Vereist wachtwoordtype**
- **Wacht woord verloopt (dagen)**  
- **Wachtwoordgeschiedenis onthouden**  
- **Aantal mislukte aanmeldingen dat is toegestaan voordat het apparaat wordt gewist**  
- **Minuten inactief voordat wachtwoord is vereist**  
- **Vereist wachtwoordtype – minimum aantal tekensets**  
- **Camera toestaan**
- **Versleuteling vereisen op mobiel apparaat**  
- **Verwisselbare opslag toestaan**  
- **Webbrowser toestaan**  
- **Toepassingsarchief toestaan**  
- **Schermopname toestaan**  
- **Geolocatie toestaan**  
- **Micro soft-account toestaan**  
- **Kopiëren en plakken toestaan**  
- **Wi-Fi-tethering toestaan**  
- **Automatische verbinding met gratis Wi-Fi-hotspots toestaan**  
- **Melden van Wi-Fi-hotspots toestaan**  
- **Fabrieksinstellingen terugzetten toestaan**
- **Bluetooth toestaan**  
- **NFC toestaan**
- **Wi-Fi toestaan**

### <a name="start-a-selective-wipe"></a>Een selectief wissen starten

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en kies het knoop punt **apparaten** . U kunt ook **apparaat verzamelingen** kiezen en een verzameling selecteren waarvan het apparaat lid is.

1. Selecteer het apparaat dat u wilt wissen.

1. Selecteer op het lint, in de groep apparaat, **acties extern apparaat**en kies vervolgens **buiten gebruik stellen/wissen**.

1. Selecteer in het venster **buiten gebruik stellen vanuit Configuration Manager** de volgende optie: **bedrijfs inhoud wissen en het mobiele apparaat buiten gebruik stellen vanuit Configuration Manager**.

### <a name="recommendations-for-selective-wipe"></a>Aanbevelingen voor selectief wissen

- Als u e-mail berichten wilt wissen, stelt u e-mail profielen in op Windows Phone 8,1-apparaten.

- Zorg ervoor dat de apps zijn gedistribueerd via app-beheer voor mobiele apparaten voor een geslaagde wissen van apps.

## <a name="passcode-reset"></a>Wachtwoordcode opnieuw instellen

Als een gebruiker de wachtwoord code vergeet, kunt u met deze actie een nieuwe tijdelijke wachtwoord code op het apparaat afdwingen. U kunt de wachtwoord code ook volledig verwijderen. In de volgende tabel wordt aangegeven hoe de wachtwoordcode opnieuw moet worden ingesteld op verschillende mobiele platforms.

| Versie van het besturingssysteem | Wachtwoordcode opnieuw instellen |
|------------|----------------|
| Windows 10 | Niet ondersteund |
| Windows 10 Mobile | Ondersteund, met uitzonde ring van Azure Active Directory gekoppelde apparaten |
| Windows Phone 8 en Windows Phone 8.1 | Ondersteund |
| Windows RT 8.1 | Niet ondersteund |
| Windows 8.1 | Niet ondersteund |

> [!Note]
> Start de actie wachtwoord code opnieuw instellen op de site op het hoogste niveau. Als u bijvoorbeeld een centrale beheer site gebruikt, kunt u alleen de actie uitvoeren op die site. Als u een zelfstandige primaire site gebruikt, kunt u alleen de actie uitvoeren vanaf die site.

### <a name="remotely-reset-the-passcode-on-a-mobile-device"></a>De wachtwoord code op afstand opnieuw instellen op een mobiel apparaat

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en kies het knoop punt **apparaten** . U kunt ook **apparaat verzamelingen** kiezen en een verzameling selecteren waarvan het apparaat lid is.

1. Selecteer het apparaat of de apparaten waarop u de wachtwoordcode opnieuw wilt instellen.

1. Selecteer op het lint, in de groep apparaat, **acties extern apparaat**en kies vervolgens **wachtwoord code opnieuw instellen**.  

### <a name="show-the-state-of-the-passcode-reset"></a>De status van het opnieuw instellen van de wachtwoord code weer geven  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en kies het knoop punt **apparaten** . U kunt ook **apparaat verzamelingen** kiezen en een verzameling selecteren waarvan het apparaat lid is.

1. Selecteer het apparaat of de apparaten waarop u de status van het opnieuw instellen van de wachtwoordcode wilt weergeven.

1. Selecteer op het lint, in de groep apparaat, **acties extern apparaat**en kies vervolgens **wachtwoord code weer geven**.  

## <a name="remote-lock"></a>Vergrendelen op afstand

Als een gebruiker het apparaat verliest, kunt u het apparaat op afstand vergren delen. In de volgende tabel wordt vermeld hoe vergrendelen op afstand werkt op verschillende mobiele platforms.  

|Versie van het besturingssysteem|Vergrendelen op afstand|
|----------|-----------|
|Windows 10|Niet ondersteund|
|Windows Phone 8 en Windows Phone 8.1|Ondersteund|
|Windows RT 8.1|Wordt ondersteund als de huidige gebruiker van het apparaat dezelfde gebruiker is die het apparaat heeft geregistreerd.|
|Windows 8.1|Wordt ondersteund als de huidige gebruiker van het apparaat dezelfde gebruiker is die het apparaat heeft geregistreerd.|

> [!Note]
> De actie extern vergren delen starten vanaf de site op het hoogste niveau. Als u bijvoorbeeld een centrale beheer site gebruikt, kunt u alleen de actie uitvoeren op die site. Als u een zelfstandige primaire site gebruikt, voert u de actie uit vanaf die site.

### <a name="remotely-lock-a-mobile-device"></a>Een mobiel apparaat op afstand vergren delen

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en kies het knoop punt **apparaten** . U kunt ook **apparaat verzamelingen** kiezen en een verzameling selecteren waarvan het apparaat lid is.

1. Selecteer het apparaat dat of de apparaten die u wilt vergrendelen.

1. Selecteer op het lint, in de groep apparaat, **acties voor extern apparaat**en kies vervolgens **extern vergren delen**. Bevestig de actie.

### <a name="show-the-state-of-the-remote-lock"></a>De status van de externe vergren deling weer geven

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en kies het knoop punt **apparaten** . U kunt ook **apparaat verzamelingen** kiezen en een verzameling selecteren waarvan het apparaat lid is.

1. Selecteer het apparaat waarop u de status van de externe vergrendeling wilt weergeven.

1. Selecteer op het lint in de groep apparaat de optie **acties voor extern apparaat**en kies vervolgens **status van externe vergren deling weer geven**.

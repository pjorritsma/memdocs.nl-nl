---
title: Wi-Fi-profielen maken
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van Wi-Fi-profielen in Configuration Manager om instellingen voor draadloze netwerken te implementeren voor gebruikers in uw organisatie.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710767"
---
# <a name="create-wi-fi-profiles"></a>Wi-Fi-profielen maken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik Wi-Fi-profielen in Configuration Manager om instellingen voor draadloze netwerken te implementeren voor gebruikers in uw organisatie. Door deze instellingen te implementeren, maakt u het voor gebruikers gemakkelijker om verbinding te maken met Wi-Fi.  

Stel dat u een Wi-Fi-netwerk hebt waarop u alle Windows-laptops wilt inschakelen om verbinding mee te maken. Maak een Wi-Fi-profiel met de instellingen die nodig zijn om verbinding te maken met het draadloze netwerk. Implementeer vervolgens het profiel voor alle gebruikers met Windows-laptops in uw-hiërarchie. Gebruikers van deze apparaten zien uw netwerk in de lijst met draadloze netwerken en kunnen gemakkelijk verbinding maken met dit netwerk.  

U kunt Wi-Fi-profielen configureren voor de volgende versies van het besturings systeem:

- Windows 8,1 32-bits of 64-bits

- Windows RT 8.1

- Windows 10 of Windows 10 Mobile

U kunt Configuration Manager ook gebruiken om instellingen voor draadloze netwerken te implementeren op mobiele apparaten met behulp van on-premises Mobile Device Management (MDM). Zie [Wat is on-premises MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)? voor meer algemene informatie.

Wanneer u een Wi-Fi-profiel maakt, kunt u een grote verscheidenheid aan beveiligingsinstellingen opnemen. Deze instellingen omvatten certificaten voor Server validatie en client verificatie die zijn gepusht met Configuration Manager-certificaat profielen. Zie [certificaat profielen](introduction-to-certificate-profiles.md)voor meer informatie over certificaat profielen.

## <a name="create-a-wi-fi-profile"></a>Een Wi-Fi-profiel maken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit, vouw **toegang tot bedrijfs bronnen**uit en selecteer het knoop punt **Wi-Fi-profielen** .

1. Kies op het tabblad **Start** in de groep **maken** de optie **Wi-Fi-profiel maken**.

1. Geef op de pagina **Algemeen** van de wizard Wi-Fi-profiel maken de volgende informatie op:

    - **Naam**: Voer een unieke naam in om het profiel in de-console te identificeren.

    - **Beschrijving**: Voeg eventueel een beschrijving toe om meer informatie over het Wi-Fi-profiel op te geven.

    - **Een bestaand Wi-Fi-profiel item uit een bestand importeren**: Selecteer deze optie om de instellingen van een ander Wi-Fi-profiel te gebruiken. Wanneer u deze optie selecteert, vereenvoudigen de resterende pagina's van de wizard op twee pagina's: **Wi-Fi-profiel** en **ondersteunde platforms**importeren.

        > [!IMPORTANT]
        > Zorg ervoor dat het Wi-Fi-profiel dat u importeert geldige XML bevat voor een Wi-Fi-profiel. Wanneer u het bestand importeert, valideert Configuration Manager het profiel niet.

    - **Ernst van niet-compliantie voor rapporten**: Kies een van de volgende Ernst niveaus die het apparaat rapporteert als het Wi-Fi-profiel wordt geëvalueerd als niet-compatibel. Als de installatie van het profiel bijvoorbeeld mislukt, is het niet-compatibel.

        - **Geen**: voor computers die niet voldoen aan deze nalevings regel wordt geen fout Ernst gerapporteerd voor Configuration Manager-rapporten.

        - **Informatie**

        - **Waarschuwing**

        - **Kritiek**

        - **Kritiek met gebeurtenis**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **kritiek** gerapporteerd voor Configuration Manager-rapporten. Apparaten registreren de niet-compatibele status ook als een Windows-gebeurtenis in het logboek voor toepassings gebeurtenissen.

1. Geef op de pagina **Wi-Fi-profiel** van de wizard de volgende informatie op:

    - **Netwerk naam**: Geef de naam op die door apparaten wordt weer gegeven als de netwerk naam.

        > [!IMPORTANT]
        > Configuration Manager biedt geen ondersteuning voor het gebruik`'`van aanhalings tekens`,`() of komma () in de netwerk naam.

    - **SSID**: Geef de hoofdletter gevoelige id op van het draadloze netwerk.

    - **Automatisch verbinding maken wanneer dit netwerk binnen bereik is**
    - **Andere draadloze netwerken zoeken tijdens verbinding met dit netwerk**
    - **Verbinden wanneer het netwerk de naam (SSID) niet uitzendt**

1. Geef op de pagina **beveiligings configuratie** de volgende informatie op:

    > [!IMPORTANT]
    > Als u een Wi-Fi-profiel voor [on-premises MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)maakt, ondersteunt de huidige vertakking van Configuration Manager alleen de volgende Wi-Fi-beveiligings configuraties:  
    >
    > - Beveiligingstypen: **WPA2-Enterprise** of **WPA2-Personal**  
    > - Versleutelingstypen : **AES** of **TKIP**  
    > - EAP-typen: **smartcard of ander certificaat** of **PEAP**  

    - **Beveiligings type**: Selecteer het beveiligings protocol dat wordt gebruikt door het draadloze netwerk of selecteer **geen verificatie (open)** als het netwerk niet is beveiligd.

    - **Versleuteling**: als het beveiligings type dit ondersteunt, stelt u de versleutelings methode in voor het draadloze netwerk.

    - **EAP-type**: Selecteer het verificatie protocol voor de geselecteerde versleutelings methode.

        > [!NOTE]
        > Alleen voor Windows Phone apparaten: de EAP- **typen** worden **versneld en EAP-Fast** worden niet ondersteund.

        Selecteer **configureren** om de eigenschappen voor het geselecteerde EAP-type op te geven. Deze optie is niet beschikbaar voor alle geselecteerde EAP-typen.

        > [!IMPORTANT]
        > Het venster configuratie van EAP-type is van Windows. Zorg ervoor dat u de Configuration Manager-console uitvoert op een computer die ondersteuning biedt voor het geselecteerde EAP-type.

    - **De gebruikers referenties onthouden bij elke aanmelding**: Selecteer deze optie om gebruikers referenties op te slaan, zodat gebruikers niet elke keer dat ze zich aanmelden bij Windows, hun referenties voor het draadloze netwerk hoeven in te voeren.

1. Geef op de pagina **Geavanceerde instellingen** van de wizard aanvullende instellingen op voor het Wi-Fi-profiel. Geavanceerde instellingen zijn mogelijk niet beschikbaar of kunnen variëren, afhankelijk van de opties die u selecteert op de pagina **beveiligings configuratie** van de wizard. Bijvoorbeeld de verificatie modus of opties voor eenmalige aanmelding.

1. Als uw draadloze netwerk gebruikmaakt van een proxy server, selecteert u op de pagina **proxy-instellingen** de optie voor het **configureren van proxy-instellingen voor dit Wi-Fi-profiel**. Geef vervolgens de configuratie gegevens voor de proxy op.

1. Selecteer op de pagina **ondersteunde platforms** de versies van het besturings systeem waarop dit Wi-Fi-Profiel van toepassing is.

1. Voltooi de wizard.

## <a name="next-step"></a>Volgende stap

> [!div class="nextstepaction"]
> [Wi-Fi-profielen implementeren](deploy-wifi-vpn-email-cert-profiles.md)

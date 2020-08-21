---
title: Profielen voor externe verbindingen maken
titleSuffix: Configuration Manager
description: Gebruik Configuration Manager profielen voor externe verbindingen om uw gebruikers in staat te stellen extern verbinding te maken met werk computers.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 1434d7802eb1ed68cb0a575778bdae1e5e99c9ec
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694743"
---
# <a name="remote-connection-profiles-in-configuration-manager"></a>Profielen voor externe verbindingen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik Configuration Manager profielen voor externe verbindingen zodat uw gebruikers extern verbinding kunnen maken met werk computers. Met deze profielen kunt u Verbinding met extern bureaublad-instellingen implementeren voor gebruikers in uw hiërarchie. Gebruikers hebben via een VPN-verbinding toegang tot een van hun primaire werk computers via Extern bureaublad.  

> [!IMPORTANT]  
> Wanneer u instellingen voor profielen voor externe verbindingen met Configuration Manager opgeeft, slaat de client de instellingen op in het lokale Windows-beleid. Deze instellingen kunnen Extern bureaublad instellingen die u configureert met een andere toepassing negeren. Daarnaast kunt u, als u Windows groepsbeleid gebruikt om Extern bureaublad-instellingen te configureren, de instellingen die zijn opgegeven in de groepsbeleid Configuration Manager instellingen overschrijven.

Configuration Manager maakt een beveiligings groep op clients, **verbinding met externe PC**. Wanneer u een profiel voor externe verbindingen implementeert, voegt de client de primaire gebruikers van de computer toe aan deze groep. Een lokale beheerder kan hand matig gebruikers toevoegen aan of verwijderen uit deze groep, maar Configuration Manager het lidmaatschap bij te houden wanneer de volgende keer de naleving van het profiel evalueert.

> [!IMPORTANT]  
> Als de affiniteits relatie tussen een gebruiker en een apparaat wordt gewijzigd, Configuration Manager het profiel voor externe verbindingen en de Windows Firewall-instellingen uitschakelen om verbindingen met de computer te voor komen.

## <a name="prerequisites"></a>Vereisten  

### <a name="external-dependencies"></a>Externe afhankelijkheden  

- Als u wilt dat gebruikers verbinding kunnen maken via internet, moet u een Extern bureaublad-gateway-server installeren en configureren. Zie [extern bureaublad-services-Access vanaf elke locatie](/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere)voor meer informatie over het installeren en configureren van een extern bureaublad-gateway server.

- Als clients een op een host gebaseerde Firewall uitvoeren, moet het mstsc.exe-programma worden ingeschakeld. Wanneer u een profiel voor externe verbindingen configureert, schakelt u de instelling in om **Windows Firewall-uitzonde ring voor verbindingen in Windows-domeinen en particuliere netwerken toe te staan**. Met deze instelling kunt Configuration Manager automatisch Windows Firewall configureren.

    > [!TIP]
    > Met de groepsbeleidinstellingen voor het configureren van Windows Firewall kunt u de configuratie die u instelt in Configuration Manager overschrijven. Als u groepsbeleid gebruikt om Windows Firewall te configureren, moet u ervoor zorgen dat groepsbeleid instellingen geen mstsc.exe blok keren.

    Als clients een andere, op een host gebaseerde Firewall uitvoeren, moet u deze firewall-afhankelijkheid hand matig configureren.  

### <a name="configuration-manager-dependencies"></a>Configuration Manager-afhankelijkheden  

- Een gebruiker kan alleen verbinding maken met een werk computer als deze computer een primair apparaat van de gebruiker is. Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie.

- Voor het beheren van externe verbindings profielen heeft uw gebruikers account specifieke machtigingen nodig in Configuration Manager. De ingebouwde rol voor **nalevings instellingen Manager** bevat de machtigingen die nodig zijn voor het beheren van deze profielen. Zie [op rollen gebaseerd beheer configureren](../../core/servers/deploy/configure/configure-role-based-administration.md)voor meer informatie.

## <a name="security-and-privacy-considerations"></a>Aandachtspunten voor beveiliging en privacy

### <a name="security-considerations"></a>Beveiligingsoverwegingen  

- Geef handmatig de gebruikersaffiniteit met apparaat op in plaats van gebruikers toe te staan hun primaire apparaat te identificeren. Geen op gebruik gebaseerde configuratie inschakelen.

  - Voordat u een profiel voor externe verbindingen kunt implementeren, moet u de optie inschakelen om **alle primaire gebruikers van de werk computer in staat te stellen extern verbinding te maken**. Met deze configuratie moet u altijd hand matig de gebruikers affiniteit van het apparaat opgeven. Houd geen rekening met de informatie die Configuration Manager verzameld van gebruikers of van het apparaat om gezaghebbend te zijn. Als u een profiel implementeert en een vertrouwde gebruiker met beheerders rechten geen gebruikers affiniteit voor apparaten opgeeft, kunnen niet-geautoriseerde gebruikers bevoegdheden voor verhoogde bevoegdheid ontvangen en kunnen ze op afstand verbinding maken met computers.

  - Configuration Manager verzamelt gegevens op basis van gebruik via status berichten, een snel maar niet-beveiligd communicatie kanaal. Gebruik, om te helpen deze bedreiging af te zwakken, Server Message Block (SMB) ondertekening of Internet protocolbeveiliging (IPsec) tussen clientcomputers en het beheerpunt.

- Beperk lokale beheerrechten op de siteservercomputer. Een lokale beheerder op de site server kan hand matig leden toevoegen aan de **Remote PC Connect** -beveiligings groep die Configuration Manager automatisch maakt en onderhoudt. Deze actie kan een verhoging van bevoegdheden veroorzaken omdat leden Extern bureaublad machtigingen ontvangen.

### <a name="privacy-considerations"></a>Privacyoverwegingen  

Wanneer een gebruiker extern verbinding maakt met een werk computer, downloaden ze een. wsrdp-bestand. Dit bestand bevat de naam van het apparaat en de naam van de Extern bureaublad-gateway-server. Deze waarden zijn vereist om de Extern bureaublad-sessie te maken. Het bestand .wsrdp wordt gedownload en automatisch lokaal opgeslagen. Dit bestand wordt overschreven de volgende keer dat de gebruiker een sessie met een extern bureaublad uitvoert.  

## <a name="create-a-profile"></a>Een profiel maken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit en selecteer profielen voor **externe verbindingen**.  

1. Klik op het tabblad **Start** van het lint in de groep **maken** op **profiel voor externe verbinding maken**.  

1. Geef op de pagina **Algemeen** van de **wizard Profiel voor externe verbinding maken**een naam en een optionele beschrijving voor het profiel op. Beide waarden hebben een maximum limiet van 256 tekens.  

1. Geef op de pagina **Profiel instellingen** de volgende instellingen op:  

    - **Volledige naam en poort van de Extern bureaublad-gateway server (optioneel)**: Geef de naam op van de Extern bureaublad-gateway-server die moet worden gebruikt voor verbindingen. Deze waarde heeft de volgende vereisten:

        - De server naam mag niet langer zijn dan 256 tekens.
        - Het kan bestaan uit hoofd letters, kleine letters en cijfers.
        - Afgezien van punten ( `.` ) tussen segmenten en een dubbele punt ( `:` ) voor de poort, zijn de enige speciale tekens streepje ( `–` ) en onderstrepings teken ( `_` ).
        - Configuration Manager biedt geen ondersteuning voor het gebruik van een internationale domein naam voor deze waarde.

    - **Alleen verbindingen toestaan vanaf computers waarop Extern bureaublad wordt uitgevoerd met verificatie op netwerkniveau**: standaard ingeschakeld, wordt met deze instelling een extra beveiligings niveau voor de verbinding toegevoegd. Zie [granting extern bureaublad Access](/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication)(Engelstalig) voor meer informatie.

    - Schakel de volgende Verbindings instellingen in:

        - **Externe verbindingen met werkcomputers toestaan**

        - **Alle primaire gebruikers van de werkcomputer toestaan om extern verbinding te maken**

        - **Windows Firewall-uitzondering toestaan voor verbindingen in Windows-domeinen en in particuliere netwerken**

        > [!IMPORTANT]  
        > Alle drie de instellingen moeten hetzelfde zijn voordat u kunt door gaan.

        Schakel deze instellingen alleen uit wanneer u een profiel implementeert om externe verbindingen uit te scha kelen.

1. Voltooi de wizard.

Het nieuwe profiel wordt weer gegeven in het knoop punt **profielen voor externe verbinding** in de werk ruimte **activa en naleving** .  

## <a name="deploy"></a>Implementeren

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit en selecteer profielen voor **externe verbindingen**.

1. Selecteer in de lijst **profielen voor externe verbinding** het profiel dat u wilt implementeren. Klik op het tabblad **Start** van het lint in de groep **implementatie** op **implementeren**.  

1. Geef in het venster **profiel voor externe verbinding implementeren** de volgende informatie op:

    - **Verzameling**: Blader om de apparaten verzameling te selecteren waarvoor u het profiel wilt implementeren.

    - **Regels die niet compliant zijn herstellen, indien ondersteund**: Schakel deze instelling in om de profiel instellingen automatisch te herstellen als deze niet compatibel zijn op een apparaat. Het profiel kan niet-compatibel zijn wanneer het niet bestaat.

    - **Herstel toestaan buiten het onderhouds venster**: als u een onderhouds venster configureert voor de verzameling waarnaar u het profiel implementeert, schakelt u deze optie in om het te Configuration Manager laten herstellen buiten het onderhouds venster. Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie.

    - **Waarschuwing genereren**: Schakel deze optie in om een compatibiliteits waarschuwing te configureren.

    - **Geef het evaluatie schema voor compatibiliteit op voor deze configuratie basislijn**: Geef een eenvoudige of aangepaste planning op waarmee de client het profiel evalueert.

1. Selecteer **OK** om het venster te sluiten en de implementatie te maken.

### <a name="client-evaluation"></a>Client evaluatie

De client evalueert het profiel wanneer een gebruiker zich aanmeldt.

Als een apparaat een verzameling verlaat waarop u een profiel voor externe verbindingen implementeert, Configuration Manager de instellingen op het apparaat uitschakelt. Dit proces kan echter alleen correct plaatsvinden als u al minstens één configuratie-item of configuratiebasislijn hebt geïmplementeerd die een configuratie-item van uw site bevat.

### <a name="conflict-resolution"></a>Conflictoplossing

Implementeer niet meer dan een profiel voor externe verbindingen met conflicterende instellingen op hetzelfde apparaat. U implementeert bijvoorbeeld twee profielen met verschillende instellingen voor dezelfde verzameling. U kunt slechts één profiel implementatie configureren om niet- **compatibele regels te herstellen wanneer**deze worden ondersteund. Deze implementatie kan de instellingen in het andere profiel overschrijven. Configuration Manager biedt geen ondersteuning voor dit type implementatie van een profiel voor externe verbindingen.

## <a name="monitor"></a>Controleren

Ga in de Configuration Manager-console naar de werk ruimte **bewaking** en selecteer **implementaties**. Selecteer in de lijst **implementaties** de implementatie van het profiel voor externe verbindingen.

U kunt samenvattingsgegevens over de compatibiliteit van de implementatie van het profiel voor externe verbindingen bekijken op de hoofdpagina. Als u meer gedetailleerde informatie wilt weer geven, selecteert u de profiel implementatie. Selecteer vervolgens op het tabblad **Start** van het lint in de groep **implementatie** de optie **status weer geven**. Met deze actie wordt de pagina **Implementatie status** geopend.  

De pagina **Implementatiestatus** bevat de volgende tabbladen:  

- **Compatibel**: hier wordt de compatibiliteit van het profiel voor externe verbindingen weer gegeven op basis van het aantal activa dat is beïnvloed.

    > [!IMPORTANT]  
    > De client evalueert geen profiel voor externe verbindingen als het niet van toepassing is. Het rapport blijft echter wel compatibel.

- **Fout**: hier wordt een lijst met alle fouten voor de geselecteerde implementatie van het profiel voor externe verbindingen weer gegeven op basis van het aantal activa dat is beïnvloed.

- **Niet-compatibel**: geeft een lijst met alle niet-compatibele regels binnen het profiel voor externe verbindingen weer op basis van het aantal activa dat is beïnvloed.

- **Onbekend**: geeft een lijst weer van alle apparaten die geen naleving rapporteren voor de geselecteerde implementatie van het profiel voor externe verbindingen, samen met de huidige client status van de apparaten.

Open op elk tabblad een regel om een tijdelijk subknooppunt te maken onder het knoop punt **gebruikers** in de werk ruimte **activa en naleving** . Dit subknooppunt bevat alle apparaten met de compatibiliteits status van het geselecteerde tabblad.

In het deel venster **activum gegevens** worden de apparaten weer gegeven met de geselecteerde compatibiliteits status voor dit profiel. Open een apparaat in de lijst om aanvullende informatie weer te geven.

## <a name="reports"></a>Rapporten

Configuration Manager bevat ingebouwde rapporten die u kunt gebruiken om informatie over profielen voor externe verbindingen te bewaken. Deze rapporten hebben de rapportcategorie van **Compatibiliteit en instellingen beheren**.  

> [!IMPORTANT]  
> Gebruik het Joker teken ( `%` ) wanneer u de para meters **apparaat filter** en **gebruikers filter** in de rapporten voor nalevings instellingen gebruikt.  

Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over het configureren van rapportage in Configuration Manager.
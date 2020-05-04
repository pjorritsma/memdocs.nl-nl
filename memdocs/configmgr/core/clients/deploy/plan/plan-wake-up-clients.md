---
title: Clients inschakelen
titleSuffix: Configuration Manager
description: Plan het activeren van clients in Configuration Manager met behulp van Wake On LAN (WOL).
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feea1cdea52b76b900497e84eea210444535fcd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713259"
---
# <a name="plan-how-to-wake-up-clients-in-configuration-manager"></a>Plannen hoe clients in Configuration Manager moeten worden geactiveerd

*Van toepassing op: Configuration Manager (huidige vertakking)*

 Configuration Manager ondersteunt traditionele Ontwaak pakketten om computers in de slaap stand te activeren wanneer u vereiste software, zoals software-updates en toepassingen, wilt installeren.

> [!NOTE]
> In dit artikel wordt beschreven hoe een oudere versie van Wake on LAN-functies. Deze functionaliteit bestaat nog steeds in Configuration Manager versie 1810, die ook een nieuwere versie van Wake on LAN bevat. Beide versies van Wake on LAN kunnen en in veel gevallen tegelijk worden ingeschakeld. Zie [Wake on LAN configureren](../configure-wake-on-lan.md)voor meer informatie over de werking van de nieuwe versie van Wake on LAN-functies vanaf 1810 en het inschakelen van een of beide versies.  

## <a name="how-to-wake-up-clients-in-configuration-manager"></a>Clients in Configuration Manager ontwaken

 Configuration Manager ondersteunt traditionele Ontwaak pakketten om computers in de slaap stand te activeren wanneer u vereiste software, zoals software-updates en toepassingen, wilt installeren.  

U kunt de traditionele Wake-uppakket methode aanvullen met behulp van de Wake-up Proxy client instellingen. Wake-up proxy gebruikt een peer-to-peer-protocol en gestuurde computers om te controleren of andere computers op het subnet actief zijn, en om ze indien nodig te activeren. Wanneer de site is geconfigureerd voor Wake On LAN en clients zijn geconfigureerd voor wake-up proxy, werkt het proces als volgt:  

1. Computers waarop de Configuration Manager-client is geïnstalleerd en die zich niet in de slaap stand bevinden, controleren of andere computers in het subnet actief zijn. Ze controleren deze controle door elke vijf seconden een ping-opdracht voor TCP/IP te sturen.  

2. Als er geen reactie is van andere computers, wordt ervan uitgegaan dat de slaap stand actief is. De computers die actief zijn, krijgen de *Manager-computer* voor het subnet.  

    Omdat het mogelijk is dat een computer niet reageert vanwege een andere reden dan de slaap stand (bijvoorbeeld omdat het is uitgeschakeld, verwijderd uit het netwerk of de instelling voor de Wake-up-client voor de proxy niet meer wordt toegepast), worden de computers elke dag om de datum verzonden. lokale tijd. Computers die niet reageren, worden niet langer beschouwd als een slaap stand en worden niet meer gewekt door Wake-up proxy.  

    Ter ondersteuning van Wake-up proxy moeten op elk subnet ten minste drie computers actief zijn. Om aan deze vereiste te voldoen, zijn drie computers niet-deterministisch gekozen als *Guardian-computers* voor het subnet. Deze status betekent dat ze actief blijven, ondanks het geconfigureerde energie beleid in de slaap stand of sluimer stand na een periode van inactiviteit. Guardian-computers voldoen aan de opdrachten afsluiten of opnieuw starten, bijvoorbeeld als gevolg van onderhouds taken. Als deze actie wordt uitgevoerd, wordt op de resterende Guardian-computers een andere computer in het subnet geactiveerd zodat het subnet drie Guardian-computers blijft.  

3. Beheer computers vragen de netwerk switch om netwerk verkeer voor de slapende computers naar zichzelf om te leiden.  

    De omleiding wordt bereikt door de manager-computer die een Ethernet-frame uitzendt dat gebruikmaakt van het MAC-adres van de slapende computer als het bron adres. Dit gedrag zorgt ervoor dat de netwerk switch zich gedraagt alsof de computer in de slaap stand is verplaatst naar de poort waarop de beheer computer zich bevindt. De manager-computer verzendt ook ARP-pakketten voor de slapende computers om de vermelding in de ARP-cache te laten staan. De manager-computer reageert ook op ARP-aanvragen namens de slaap computer en beantwoordt met het MAC-adres van de computer in de slaap stand.  

   > [!WARNING]  
   >  Tijdens dit proces blijft de IP-to-MAC-toewijzing voor de slaap computer hetzelfde. Wake-up proxy werkt door de netwerk switch te informeren dat een andere netwerk adapter de poort gebruikt die is geregistreerd door een andere netwerk adapter. Dit gedrag wordt echter wel een MAC-druk genoemd en is ongebruikelijk voor een standaard netwerk bewerking. Sommige hulpprogram ma's voor netwerk controle zoeken naar dit gedrag en kunnen ervan uitgaan dat er iets mis is. Deze bewakings hulpprogramma's kunnen daarom waarschuwingen genereren of poorten uitschakelen wanneer u Wake-up proxy gebruikt.  
   >   
   >  Gebruik de Wake-up proxy niet als uw netwerk controle hulpprogramma's en-services geen MAC-druk geven.  

4. Wanneer een manager-computer een nieuwe TCP-verbindings aanvraag voor een slapende computer ziet en de aanvraag is verzonden naar een poort waarop de slaap computer werd geluisterd voordat de slaap stand werd ingeschakeld, stuurt de manager-computer een Ontwaak pakket naar de slapende computer en stopt vervolgens het omleiden van verkeer voor deze computer.  

5. De computer in de slaap stand ontvangt het Ontwaak pakket en wordt geactiveerd. De verzendende computer probeert automatisch de verbinding te verbreken, de computer is actief en kan reageren.  

   Wake-up proxy heeft de volgende vereisten en beperkingen:  

> [!IMPORTANT]  
>  Als u een afzonderlijk team hebt dat verantwoordelijk is voor de netwerk infrastructuur en netwerk services, stelt u dit team op de hoogte tijdens uw evaluatie-en test periode. In een netwerk dat bijvoorbeeld gebruikmaakt van 802.1 X-netwerk toegangs beheer, werkt Wake-up proxy niet en kan de netwerk service worden verstoord. Daarnaast kan Wake-up proxy een aantal hulpprogram ma's voor netwerk bewaking ertoe leiden dat er waarschuwingen worden gegenereerd wanneer de hulpprogram ma's het verkeer voor wake-up andere computers detecteren.  

-   Alle Windows-besturings systemen die worden vermeld als ondersteunde clients in [ondersteunde besturings systemen voor clients en apparaten](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) , worden ondersteund voor Wake on LAN.  

-   Gast besturingssystemen die op een virtuele machine worden uitgevoerd, worden niet ondersteund.  

-   Clients moeten zijn ingeschakeld voor wake-up proxy met behulp van client instellingen. Hoewel de Wake-up proxy niet afhankelijk is van de hardware-inventaris, rapporteren clients niet de installatie van de Wake-up proxy service, tenzij ze zijn ingeschakeld voor hardware-inventaris en minstens één hardware-inventaris hebben verzonden.  

-   Netwerk adapters (en mogelijk het BIOS) moeten zijn ingeschakeld en geconfigureerd voor Ontwaak pakketten. Als de netwerk adapter niet is geconfigureerd voor Ontwaak pakketten of deze instelling is uitgeschakeld, wordt deze door Configuration Manager automatisch geconfigureerd en ingeschakeld voor een computer wanneer de client instelling wordt ontvangen om wake-up proxy in te scha kelen.  

-   Als een computer meer dan één netwerk adapter heeft, kunt u niet configureren welke adapter moet worden gebruikt voor wake-up proxy. de keuze is niet-deterministisch. De gekozen adapter wordt echter vastgelegd in het SleepAgent_<domein\> @SYSTEM_0.log bestand.  

-   Het netwerk moet ICMP-echo aanvragen (ten minste binnen het subnet) toestaan. U kunt het interval van vijf seconden dat wordt gebruikt voor het verzenden van de ICMP-ping-opdrachten niet configureren.  

-   Communicatie wordt niet versleuteld en niet-geverifieerd en IPsec wordt niet ondersteund.  

-   De volgende netwerk configuraties worden niet ondersteund:  

    -   802.1 x met poort verificatie  

    -   Draadloze netwerken  

    -   Netwerk switches die MAC-adressen aan specifieke poorten binden  

    -   Alleen IPv6-netwerken  

    -   Duur van DHCP-leases minder dan 24 uur  

Als u computers wilt activeren voor geplande software-installatie, moet u elke primaire site configureren voor het gebruik van Ontwaak pakketten.  

 Als u Wake-up proxy wilt gebruiken, moet u client instellingen voor wake-up proxy voor energie beheer implementeren naast het configureren van de primaire site.  

Bepaal of u op subnet gerichte broadcast pakketten of unicast-pakketten wilt gebruiken en welk UDP-poort nummer u wilt gebruiken. Standaard worden traditionele Wake-uppakketten verzonden via UDP-poort 9, maar om de beveiliging te verbeteren, kunt u een alternatieve poort voor de site selecteren als deze alternatieve poort wordt ondersteund door tussenliggende routers en firewalls.  

## <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Kiezen tussen unicast en op het subnet gerichte broadcast voor Wake-on-LAN  
 Als u ervoor kiest om computers te ontwaken door traditionele Ontwaak pakketten te verzenden, moet u beslissen of u unicast-pakketten of subnet-direct broadcast-pakketten wilt verzenden. Als u Wake-up proxy gebruikt, moet u unicast-pakketten gebruiken. U kunt ook de volgende tabel gebruiken om te bepalen welke verzend wijze u moet kiezen.  

|Verzendings methode|Voordeel|Nadeel|  
|-------------------------|---------------|------------------|  
|Unicast|Veiliger oplossing dan op het subnet gerichte broadcasts, omdat het pakket rechtstreeks naar een computer wordt verzonden in plaats van naar alle computers in een subnet.<br /><br /> Het opnieuw configureren van routers is mogelijk niet vereist (mogelijk moet u de ARP-cache configureren).<br /><br /> Verbruikt minder netwerk bandbreedte dan op het subnet gerichte broadcast-verzen dingen.<br /><br /> Ondersteund met IPv4 en IPv6.|Ontwaak pakketten vinden doel computers waarvan het subnetadres is gewijzigd na de laatste planning van de hardware-inventarisatie niet.<br /><br /> Switches moeten mogelijk worden geconfigureerd voor het door sturen van UDP-pakketten.<br /><br /> Sommige netwerk adapters reageren mogelijk niet op Ontwaak pakketten in alle slaap standen wanneer ze unicast als de verzend methode gebruiken.|  
|Op subnet gerichte broadcast|Meer slagen dan unicast als u computers hebt die regel matig hun IP-adres in hetzelfde subnet wijzigen.<br /><br /> Opnieuw configureren van de switch is niet vereist.<br /><br /> Hoge compatibiliteits snelheden met computer adapters voor alle slaap standen, omdat op het subnet gerichte broadcasts de oorspronkelijke verzendings methode waren voor het verzenden van Ontwaak pakketten.|Minder veilige oplossing dan het gebruik van unicast omdat een aanvaller doorlopende stromen van ICMP-echo aanvragen van een vervalst bron adres naar het gerichte broadcast adres kan verzenden. Dit heeft tot gevolg dat alle hosts het desbetreffende bron adres beantwoorden. Als routers zijn geconfigureerd voor het toestaan van op het subnet gerichte broadcasts, wordt de volgende configuratie aanbevolen om veiligheids redenen:<br /><br /> -Routers configureren voor het toestaan van alleen IP-gerichte broadcasts van de Configuration Manager site server met behulp van een opgegeven UDP-poort nummer.<br />-Configureer Configuration Manager om het opgegeven niet-standaard poort nummer te gebruiken.<br /><br /> Vereist mogelijk dat alle tussenliggende routers opnieuw worden geconfigureerd om op het subnet gerichte broadcasts in te scha kelen.<br /><br /> Verbruikt meer netwerk bandbreedte dan unicast-verzen dingen.<br /><br /> Alleen ondersteund met IPv4; IPv6 wordt niet ondersteund.|  

> [!WARNING]  
>  Er zijn beveiligings Risico's gekoppeld aan op het subnet gerichte broadcasts: een aanvaller zou doorlopende stromen van Internet Control Message Protocol (ICMP) Echo aanvragen van een vervalst bron adres naar het gerichte broadcast adres kunnen verzenden, waardoor alle hosts het desbetreffende bron adres beantwoorden. Dit type DOS-aanval (Denial of service) wordt meestal een Smurf-aanval genoemd en wordt doorgaans verholpen door het niet inschakelen van op het subnet gerichte broadcasts.

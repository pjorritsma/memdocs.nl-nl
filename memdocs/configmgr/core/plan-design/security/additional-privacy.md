---
title: Aanvullende privacy-informatie
titleSuffix: Configuration Manager
description: Meer informatie over hoe micro soft gegevens van Configuration Manager verzamelt en gebruikt.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6d3f6dbbbb407ee63eb8253cbf3ca740a10479c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699786"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Aanvullende informatie over privacy voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*


## <a name="updates-and-servicing"></a>Updates en onderhoud

Configuration Manager maakt gebruik van een update model waarmee u uw omgeving up-to-date kunt blijven met de meest recente updates en functies. Deze functie maakt gebruik van een site systeemrol die het service verbindings punt wordt genoemd. U kiest de server waarop deze functie moet worden geïnstalleerd. 

Zie [gebruiks gegevens](#usage-data)voor meer informatie over verzamelde gegevens en hoe deze worden gebruikt.



## <a name="usage-data"></a>Gebruiksgegevens

Configuration Manager verzamelt diagnose-en gebruiks gegevens over zichzelf, die door micro soft worden gebruikt voor het verbeteren van de installatie-ervaring, kwaliteit en beveiliging van toekomstige releases.
Diagnostische en gebruiks gegevens zijn ingeschakeld voor elke Configuration Manager-hiërarchie. Het bestaat uit SQL Server query's die wekelijks worden uitgevoerd op elke primaire site en op de centrale beheer site. Als de hiërarchie een centrale beheersite gebruikt, worden de gegevens vervolgens vanaf de primaire sites gerepliceerd naar die site. Op de site op het hoogste niveau van uw hiërarchie wordt deze informatie door het service aansluitpunt verzonden wanneer er wordt gecontroleerd op updates. Als het serviceverbindingspunt zich in de offlinemodus bevindt, wordt de informatie overgedragen met het hulpprogramma voor serviceverbindingen.

Configuration Manager verzamelt alleen gegevens uit de SQL Server-Data Base van de site en verzamelt geen gegevens rechtstreeks van clients of site servers.

Beheerders kunnen het niveau van verzamelde gegevens wijzigen door te gaan naar de sectie **gebruiks gegevens** van de Configuration Manager-console.

Zie voor meer informatie over niveaus en instellingen voor gebruiks gegevens [Diagnostische en gebruiks gegevens](../diagnostics/diagnostics-and-usage-data.md).



## <a name="log-analytics-connector"></a>Log Analytics-connector

De Log Analytics-Connector synchroniseert gegevens, zoals verzamelingen, van Configuration Manager tot de Azure-Cloud service. De Azure-abonnements-ID en de geheime sleutel worden opgeslagen in de Configuration Manager-Data Base wanneer een beheerder de functie configureert. Zowel het Azure Active Directory client geheim als de gedeelde Azure Workspace-sleutel worden opgeslagen in de on-premises Configuration Manager-Data Base. Alle communicatie tussen Configuration Manager en Azure gebruiken HTTPS. Er is geen aanvullende informatie over de verzamelingen aan micro soft verstrekt Buiten wille keurige diagnose-en gebruiks gegevens. 

Zie [log Analytics Data Security](/azure/log-analytics/log-analytics-data-security)(Engelstalig) voor meer informatie over de informatie die log Analytics verzameld.



## <a name="asset-intelligence"></a>Asset Intelligence

Met Asset Intelligence kunnen beheerders conformiteit met configuratie standaarden definiëren, traceren en proactief beheren. Meten van en rapporteren over de implementatie en het gebruik van zowel fysieke als virtuele toepassingen helpt organisaties om betere zakelijke beslissingen te nemen met betrekking tot softwarelicenties en het behouden van compatibiliteit met licentieovereenkomsten. Nadat u gebruiks gegevens van Configuration Manager-clients hebt verzameld, kunt u verschillende functies gebruiken om de gegevens weer te geven, inclusief verzamelingen, query's en rapportage.

Tijdens elke synchronisatie wordt een catalogus met bekende software gedownload van micro soft. U kunt ervoor kiezen om micro soft-informatie over gecategoriseerde software titels die in uw organisatie worden gedetecteerd, te verzenden en toe te voegen aan de catalogus. Voordat u deze informatie uploadt, worden in een dialoog venster de gegevens weer gegeven die worden geüpload. Geüploade gegevens kunnen niet worden ingetrokken. Asset Intelligence verzendt geen informatie over gebruikers en computers of licentie gebruik naar micro soft.

Nadat een software titel is geüpload, identificeren en categoriseren micro soft-onderzoekers deze, en vervolgens wordt deze kennis beschikbaar voor alle klanten die deze functie gebruiken en voor andere gebruikers van de catalogus. De titel van de geüploade software wordt openbaar. De toepassing en de categorisatie worden onderdeel van de catalogus en kunnen vervolgens worden gedownload naar andere gebruikers van de catalogus. Neem kennis van de privacyverklaring van uw organisatie vóór u Asset Intelligence gegevensverzameling configureert en beslist of informatie dient verzonden te worden naar Microsoft.

Asset Intelligence is standaard niet ingeschakeld in Configuration Manager. Het uploaden van niet-gecategoriseerde titels gebeurt nooit automatisch en het systeem is niet ontworpen om deze taak te automatiseren. U moet het uploaden van elke softwaretitel handmatig selecteren en goedkeuren.



## <a name="endpoint-protection"></a>Endpoint Protection

Microsoft Cloud Protection-Service voorheen bekend als Microsoft Active Protection Service of MAPS.

De betreffende producten zijn System Center Endpoint Protection en de Endpoint Protection functie van Configuration Manager (voor het beheren van System Center Endpoint Protection en Windows Defender voor Windows 10). Deze functie is niet geïmplementeerd voor System Center Endpoint Protection voor Linux of System Center Endpoint Protection voor Mac.

De antimalware-community van de Microsoft Cloud Protection-Service is een vrijwillige wereld wijde online community die System Center Endpoint Protection gebruikers bevat. Wanneer u Microsoft Cloud Protection-Service toevoegt, verzendt System Center Endpoint Protection automatisch informatie naar micro soft. Micro soft gebruikt de informatie om te bepalen welke software moet worden onderzocht op mogelijke dreigingen en om de effectiviteit van System Center-Endpoint Protection te verbeteren. Deze community helpt de verspreiding van nieuwe schadelijke software infecties te stoppen. Als een rapport van de Microsoft Cloud Protection-Service gegevens bevat over malware of mogelijk ongewenste software die de Endpoint Protection-client mogelijk kan verwijderen, wordt de meest recente hand tekening door Microsoft Cloud beveiligings service gedownload om het probleem op te lossen. Microsoft Cloud Protection-Service kan ook ' valse positieven ' vinden en deze herstellen. (Fout-positieven zijn waar iets dat oorspronkelijk is geïdentificeerd als schadelijke software niet.) 

Rapporten van Microsoft Cloud Protection-Service bevatten informatie over mogelijke malware-bestanden, zoals bestands namen, cryptografische hash, leverancier, grootte en datum stempels. Daarnaast kan Microsoft Cloud Protection-Service volledige Url's verzamelen om de oorsprong van het bestand aan te geven. Deze Url's kunnen af en toe persoonlijke gegevens bevatten, zoals zoek termen of gegevens die zijn ingevoerd in formulieren. Rapporten kunnen ook acties bevatten die u hebt uitgevoerd toen Endpoint Protection u op de hoogte was van ongewenste software. Rapporten van Microsoft Cloud Protection-Service bevatten deze informatie om micro soft meter te helpen bij het effectief Endpoint Protection van malware en mogelijk ongewenste software te detecteren en te verwijderen en om nieuwe malware te identificeren.

U kunt lid worden van Microsoft Cloud Protection-Service als u een basis-of geavanceerd lidmaatschap hebt. Rapporten van basis leden bevatten de gegevens die eerder zijn beschreven. Rapporten van geavanceerde leden zijn uitgebreider en kunnen aanvullende informatie bevatten over de software die Endpoint Protection detecteert, zoals de locatie van dergelijke software, bestands namen, hoe de software werkt en hoe deze uw computer heeft beïnvloed. Deze rapporten en rapporten van andere Endpoint Protection gebruikers die deel nemen aan Microsoft Cloud-beveiligings service helpen micro soft-onderzoekers nieuwe dreigingen sneller te ontdekken. Vervolgens worden de definities van schadelijke software gemaakt voor Program ma's die voldoen aan de analyse criteria, en worden de bijgewerkte definities beschikbaar gesteld aan alle gebruikers via Microsoft Update.

Om bepaalde soorten malware-infecties te detecteren en op te lossen, stuurt het product regel matig informatie over Microsoft Cloud Protection-Service over de beveiligings status van uw PC. Deze informatie bevat informatie over de beveiligings instellingen en logboek bestanden van uw PC waarin de Stuur Programma's en andere software worden beschreven die worden geladen tijdens het opstarten van uw PC.

Er wordt ook een getal met de unieke identificatie van uw PC verzonden. Ook kan Microsoft Cloud Protection-Service de IP-adressen verzamelen waarmee de mogelijke malware-bestanden verbinding maken.

Microsoft Cloud-beveiligings service rapporten worden gebruikt om micro soft-software en-services te verbeteren. De rapporten kunnen ook worden gebruikt voor statistische tests of andere test-of analyse doeleinden en voor het genereren van definities. Alleen werk nemers, contract ANTEN, partners en leveranciers van micro soft die een bedrijf nodig hebben om de rapporten te gebruiken, hebben toegang tot hen.

Microsoft Cloud Protection-Service verzamelt geen opzettelijk persoonlijke gegevens. In zoverre Microsoft Cloud beveiligings service persoonlijke gegevens verzamelt, gebruikt micro soft de informatie niet om u te identificeren of contact met u op te nemen.

Zie [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)voor meer informatie.



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Sitehiërarchie – Geografische weergave met Bing Maps

Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , selecteer het knoop punt **site hiërarchie** en schakel over naar de **geografische weer gave**. Met deze weer gave kunt u kaarten gebruiken die micro soft Bing Maps biedt om uw Configuration Manager fysieke server topologie weer te geven. Om deze functie in te scha kelen, wordt de locatie-informatie die u opgeeft van uw server naar de Bing Maps-webservice verzonden.

Microsoft gebruikt de informatie voor de werking van Microsoft Bing Maps en voor de verbetering van de werking hiervan en voor andere Microsoft-sites en -diensten. Zie de [privacyverklaring van micro soft](https://privacy.microsoft.com/privacystatement)voor meer informatie.

U kunt kiezen om de geografische weergave voor de sitehiërarchie niet te gebruiken. In de weer gave standaard hiërarchie diagram kunt u de hiërarchie zien en de Bing Maps-service niet gebruiken.
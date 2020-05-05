---
title: Beveiliging en privacy voor besturingssysteemimplementatie
titleSuffix: Configuration Manager
description: Meer informatie over aanbevolen procedures voor beveiliging en privacy voor de implementatie van besturings systemen in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53256889b8bbd6a9608748a57de33b38be77cfd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724424"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Beveiliging en privacy voor de implementatie van het besturings systeem in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat beveiligings-en privacy-informatie voor de implementatie functie van het besturings systeem in Configuration Manager.  



##  <a name="security-best-practices-for-os-deployment"></a><a name="bkmk_security"></a>Aanbevolen beveiligings procedures voor besturingssysteem implementatie  

Gebruik de volgende aanbevolen beveiligings procedures voor wanneer u besturings systemen implementeert met Configuration Manager:  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Toegangsbeheer implementeren om opstartbare media te beveiligen

Als u opstartbare media maakt, dient u steeds een wachtwoord toe te wijzen om de media te helpen beveiligen. Zelfs met een wacht woord worden alleen bestanden die gevoelige informatie bevatten, gecodeerd en kunnen alle bestanden worden overschreven.  

Beheer de fysieke toegang tot de media door te voorkomen dat aanvallers cryptografische aanvallen kunnen gebruiken om het clientverificatiecertificaat te verkrijgen.  

De inhoud wordt gehasht en moet worden gebruikt met het oorspronkelijke beleid. Zo wordt voorkomen dat een client inhoud of clientbeleid installeert waarmee is geknoeid. Als de hash van de inhoud mislukt of als de controleren of de inhoud overeenkomt met het beleid, gebruikt de client de opstart bare media niet. Alleen de inhoud wordt gehasht. Het beleid is niet gehasht, maar wordt versleuteld en beveiligd wanneer u een wacht woord opgeeft. Dit gedrag maakt het moeilijker voor een aanvaller om het beleid te wijzigen.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>Een veilige locatie gebruiken wanneer u media maakt voor installatie kopieën van besturings systemen

Als niet-geautoriseerde gebruikers toegang hebben tot de locatie, kunnen ze knoeien met de bestanden die u maakt. Ze kunnen ook alle beschik bare schijf ruimte gebruiken, zodat het maken van de media mislukt.  


### <a name="protect-certificate-files"></a>Certificaat bestanden beveiligen 

Beveilig certificaat bestanden (. pfx) met een sterk wacht woord. Als u ze op het netwerk opslaat, beveiligt u het netwerk kanaal wanneer u ze importeert in Configuration Manager

Wanneer u een wacht woord vereist om het certificaat voor client verificatie te importeren dat u gebruikt voor opstart bare media, helpt deze configuratie bij het beveiligen van het certificaat van een aanvaller.  

Gebruik SMB-ondertekening of IPsec tussen de netwerklocatie en de siteserver om te voorkomen dat kwaadwillende personen knoeien met het certificaatbestand.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Aangetaste certificaten blok keren of intrekken 

Als het client certificaat is aangetast, blokkeert u het certificaat van Configuration Manager. Als het een PKI-certificaat is, kunt u dit intrekken.  

Als u een besturings systeem wilt implementeren met opstart bare media en PXE-opstart bewerkingen, moet u een certificaat voor client verificatie hebben met een persoonlijke sleutel. Blokkeer het certificaat als ermee is geknoeid, in het knooppunt **Beveiliging** van de werkruimte **Beheer** in het knooppunt **Certificaten**.  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Het communicatie kanaal tussen de site server en de SMS-provider beveiligen

Wanneer de SMS-provider extern van de site server is, moet u het communicatie kanaal beveiligen voor het beveiligen van opstart installatie kopieën.

Wanneer u opstart installatie kopieën wijzigt en de SMS-provider wordt uitgevoerd op een server die niet de site server is, zijn de opstart installatie kopieën kwetsbaar voor aanvallen. Beveilig het netwerkkanaal tussen deze computer door gebruik te maken van SMB-ondertekening of IPsec.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Schakel distributiepunten voor PXE-clientcommunicatie alleen in op beveiligde netwerksegmenten

Wanneer een client een PXE-opstart aanvraag verstuurt, hebt u geen manier om ervoor te zorgen dat de aanvraag wordt verwerkt door een geldig distributie punt met PXE-functionaliteit. Voor dit scenario gelden de volgende beveiligingsrisico's:  

- Een rogue distributiepunt dat antwoordt op PXE-aanvragen kan mogelijk een geknoeide installatiekopie aan clients bezorgen.  

- Een aanvaller zou een man-in-the-middle-aanval kunnen starten op het TFTP-protocol dat wordt gebruikt door PXE. Deze aanval kan schadelijke code met de OS-bestanden verzenden. De aanvaller zou ook een Rogue-client kunnen maken om TFTP-aanvragen rechtstreeks naar het distributie punt te maken.  

- Een aanvaller zou een schadelijke client kunnen gebruiken om een Denial of Service-aanval uit te voeren tegen het distributiepunt.  

Gebruik verdediging in de diepte om de netwerk segmenten te beveiligen waar clients toegang hebben tot distributie punten met PXE-functionaliteit.  

> [!WARNING]  
>  Als gevolg van deze beveiligings Risico's kunt u geen distributie punt voor PXE-communicatie inschakelen wanneer het zich in een niet-vertrouwd netwerk bevinden, zoals een perimeter netwerk.  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>Configureer distributiepunten met PXE-functionaliteit om alleen op gespecificeerde netwerkinterfaces op PXE-aanvragen te reageren  

Als u toestaat dat het distributiepunt antwoordt op PXE-aanvragen op alle netwerkinterfaces, is het mogelijk dat deze configuratie de PXE-service blootstelt aan niet-vertrouwde netwerken.  


### <a name="require-a-password-to-pxe-boot"></a>Wachtwoord vereisen voor PXE-opstartbewerking

Wanneer u een wacht woord vereist voor PXE-opstart bewerking, voegt deze configuratie een extra beveiligings niveau toe aan het PXE-opstart proces. Deze configuratie helpt bij het beveiligen van Rogue-clients die lid zijn van de Configuration Manager-hiërarchie.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>Inhoud in besturingssysteem installatie kopieën beperken die worden gebruikt voor PXE-opstart bewerkingen of multi cast

Neem geen line-of-business-toepassingen of software met gevoelige gegevens op in een installatie kopie die u gebruikt voor PXE-opstart bewerkingen of multi cast.  

Als gevolg van de inherente beveiligings Risico's met betrekking tot het opstarten van PXE en multi cast, vermindert u de Risico's als een Rogue-computer de installatie kopie van het besturings systeem downloadt.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Inhoud beperken die wordt geïnstalleerd door taken reeks variabelen

Neem geen line-of-business-toepassingen of software met gevoelige gegevens op in pakketten van toepassingen die u installeert met behulp van taken reeks variabelen.  

Wanneer u software implementeert met behulp van taken reeks variabelen, kan deze worden geïnstalleerd op computers en voor gebruikers die niet zijn geautoriseerd om die software te ontvangen.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Het netwerk kanaal beveiligen bij het migreren van de gebruikers status

Wanneer u de gebruikers status migreert, moet u het netwerk kanaal tussen de client en het status migratie punt beveiligen met behulp van SMB-ondertekening of IPsec.  

Na de initiële verbinding via HTTP worden de statusmigratiegegevens overgedragen via SMB. Als u het netwerk kanaal niet beveiligt, kan een aanvaller deze gegevens lezen en wijzigen.  


### <a name="use-the-latest-version-of-usmt"></a>De meest recente versie van USMT gebruiken

Gebruik de nieuwste versie van de Hulpprogramma voor migratie van gebruikersstatus (USMT) die Configuration Manager ondersteunt.  

De meest recente versie van USMT biedt beveiligingsverbeteringen en grotere controle voor wanneer u de gebruikersstatusgegevens migreert.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Verwijder mappen hand matig op status migratie punten wanneer u ze buiten gebruik stelt  

Wanneer u een map van een status migratie punt verwijdert in de Configuration Manager-console op de eigenschappen van het status migratie punt, wordt de fysieke map niet verwijderd door de site. Als u de migratie gegevens van de gebruikers status wilt beveiligen tegen het vrijgeven van informatie, moet u de netwerk share hand matig verwijderen en de map verwijderen.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>Configureer het verwijderings beleid niet om de gebruikers status onmiddellijk te verwijderen  

Als u het verwijderings beleid configureert op het status migratie punt om gegevens die zijn gemarkeerd voor verwijdering onmiddellijk te verwijderen, en als een aanvaller beheert om de gebruikers status gegevens op te halen vóór de geldige computer, verwijdert de site de gebruikers status gegevens onmiddellijk. Stel het interval **Verwijderen na** lang genoeg in om het succesvolle herstellen van gebruikersstatusgegevens te verifiëren.  


### <a name="manually-delete-computer-associations"></a>Computer koppelingen hand matig verwijderen 

Verwijder computer koppelingen hand matig wanneer het terugzetten van de migratie gegevens van de gebruikers status is voltooid en geverifieerd.

Configuration Manager computer koppelingen worden niet automatisch verwijderd. Help de identiteit van gebruikers status gegevens te beschermen door hand matig computer koppelingen te verwijderen die niet meer nodig zijn.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Voer een handmatige back-up uit van de gegevens van de gebruikersstatusmigratie op het statusmigratiepunt  

Configuration Manager back-up bevat geen migratie gegevens voor de gebruikers status in de site back-up.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Implementeer toegangsbeheer om de vooraf geplaatste media te beschermen  

Beheer de fysieke toegang tot de media door te voorkomen dat aanvallers cryptografische aanvallen kunnen gebruiken om het clientverificatiecertificaat en gevoelige gegevens te verkrijgen.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Implementeer toegangsbeheer om het installatiekopieproces van de referentiecomputer te beschermen  

Zorg ervoor dat de referentie computer die u gebruikt voor het vastleggen van installatie kopieën van het besturings systeem zich in een beveiligde omgeving bevindt. Gebruik de juiste toegangs controles zodat onverwachte of schadelijke software niet kan worden geïnstalleerd en per ongeluk is opgenomen in de vastgelegde installatie kopie. Wanneer u de installatie kopie vastlegt, moet u ervoor zorgen dat de doel locatie van het netwerk veilig is. Dit proces zorgt ervoor dat er niet met de installatie kopie kan worden geknoeid nadat u deze hebt vastgelegd.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Installeer altijd de meest recente beveiligingsupdates op de referentiecomputer  

Wanneer de referentiecomputer actuele beveiligingsupdates heeft, helpt het om de kwetsbaarheid te verminderen voor nieuwe computers wanneer deze voor de eerste keer worden opgestart.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Toegangs beheer implementeren bij het implementeren van een besturings systeem op een onbekende computer

Als u een besturings systeem moet implementeren op een onbekende computer, implementeert u toegangs beheer om te voor komen dat onbevoegde computers verbinding maken met het netwerk.  

Het inrichten van onbekende computers biedt een handige methode om nieuwe computers op aanvraag te implementeren. Maar het kan ook een aanvaller in staat stellen om op een efficiënte manier een vertrouwde client op uw netwerk te worden. Beperk de fysieke toegang tot het netwerk en bewaak clients om onbevoegde computers te detecteren. 

Op computers die reageren op een door PXE geïnitieerde besturingssysteem implementatie, worden mogelijk alle gegevens tijdens het proces vernietigd. Dit gedrag kan leiden tot een verlies van Beschik baarheid van systemen die onbedoeld opnieuw worden geformatteerd.  


### <a name="enable-encryption-for-multicast-packages"></a>Schakel versleuteling voor multicast-pakketten in  

Voor elk implementatie pakket voor het besturings systeem kunt u versleuteling inschakelen wanneer het pakket door Configuration Manager wordt overgedragen met behulp van multi cast. Deze configuratie helpt voor komen dat Rogue-computers deel nemen aan de multi cast-sessie. Het helpt ook voor komen dat aanvallers knoeien met de verzen ding.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Bewaking voor onbevoegde distributiepunten met ingeschakelde multicast  

Als aanvallers toegang kunnen krijgen tot uw netwerk, kunnen ze Rogue multi cast-servers configureren voor de implementatie van een spoofing-besturings systeem.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>Beveilig de locatie en het netwerkkanaal als u takenreeksen naar een netwerklocatie exporteert

Beperk wie toegang heeft tot de netwerkmap.  

Gebruik SMB-ondertekening of IPsec tussen de netwerklocatie en de siteserver om te voorkomen dat kwaadwillende personen knoeien met de geëxporteerde takenreeks.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Neem extra beveiligings maatregelen als u het run as-account van de taken reeks gebruikt

Als u het [uitvoeren als-account van de taken reeks](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)gebruikt, voert u de volgende voorzorgsmaatregelen uit:  

- Gebruik een account met zo weinig mogelijk machtigingen.  

- Gebruik niet het netwerk toegangs account voor dit account.  

- Maak nooit een domeinbeheerder van het account.  

- Configureer nooit zwervende profielen voor dit account. Wanneer de taken reeks wordt uitgevoerd, wordt het zwervende profiel voor het account gedownload, waardoor het profiel kwetsbaar is voor toegang op de lokale computer.  

- Beperk het bereik van het account. Maak bijvoorbeeld verschillende run as-accounts voor taken reeksen voor elke taken reeks. Als er met één account is geknoeid, zijn alleen de client computers waarvoor dat account toegang heeft, aangetast. Als de opdracht regel beheerders toegang op de computer vereist, kunt u overwegen om alleen een lokaal beheerders account te maken voor het run as-account van de taken reeks. Maak dit lokale account op alle computers waarop de taken reeks wordt uitgevoerd en verwijder het account zodra het niet meer nodig is.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>Beperk en bewaak de gebruikers met beheerders rechten die de beveiligingsrol van de besturingssysteem implementatie Manager zijn.

Gebruikers met beheerders rechten die de beveiligingsrol **OS Deployment Manager** hebben, kunnen zelfondertekende certificaten maken. Deze certificaten kunnen vervolgens worden gebruikt om een client te imiteren en client beleid van Configuration Manager te verkrijgen.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Verbeterde HTTP gebruiken om het netwerk toegangs account te verminderen

Vanaf versie 1806, wanneer u [Enhanced http](../../core/plan-design/hierarchy/enhanced-http.md)inschakelt, is voor verschillende implementatie scenario's voor besturings systemen geen netwerk toegangs account nodig om inhoud te downloaden vanaf een distributie punt. Zie [taken reeksen en het netwerk toegangs account](planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount)voor meer informatie.<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>Beveiligings problemen voor besturingssysteem implementatie  

Hoewel implementatie van het besturings systeem een handige manier kan zijn om de meest beveiligde besturings systemen en configuraties voor computers in uw netwerk te implementeren, heeft dit de volgende beveiligings Risico's:  


### <a name="information-disclosure-and-denial-of-service"></a>Openbaarmaking van informatie en Denial of Service  

Als een aanvaller controle kan krijgen over uw Configuration Manager-infra structuur, kan deze taken reeksen uitvoeren. Dit proces omvat mogelijk het format teren van de harde schijven van alle client computers. Takenreeksen kunnen worden geconfigureerd om gevoelige informatie te bevatten, zoals accounts die machtigingen hebben om lid te worden van de domein- en volumelicentiesleutels.  


### <a name="impersonation-and-elevation-of-privileges"></a>Imitatie en verhoging van bevoegdheden  

Takenreeksen kunnen een computer toevoegen aan een domein, wat een rogue computer mogelijk geverifieerde netwerktoegang kan geven. 

Beveilig het client verificatie certificaat dat wordt gebruikt voor opstart bare taken reeks media en voor de PXE-opstart implementatie. Wanneer u een certificaat voor client verificatie vastlegt, geeft dit proces een aanvaller de mogelijkheid om de persoonlijke sleutel in het certificaat te verkrijgen. Met dit certificaat kunnen ze een geldige client op het netwerk imiteren. In dit scenario kan de malafide computer beleid downloaden dat gevoelige gegevens kan bevatten.  

Als clients het netwerk toegangs account gebruiken voor toegang tot gegevens die zijn opgeslagen op het status migratie punt, delen deze clients effectief dezelfde identiteit. Ze hebben toegang tot status migratie gegevens van een andere client die het netwerk toegangs account gebruikt. De gegevens zijn versleuteld, zodat alleen de oorspronkelijke client deze kan lezen, maar met deze gegevens kan worden geknoeid en deze kunnen worden verwijderd.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>Client verificatie voor het status migratie punt wordt bereikt door gebruik te maken van een Configuration Manager token dat is uitgegeven door het beheer punt.  

Configuration Manager de hoeveelheid gegevens die is opgeslagen op het status migratie punt niet te beperken of te beheren. Een aanvaller zou de beschik bare schijf ruimte kunnen opvullen en een DOS-aanval veroorzaken.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Als u verzamelingsvariabelen gebruikt, kunnen lokale beheerders potentieel gevoelige informatie lezen.  

Hoewel verzamelings variabelen een flexibele methode bieden om besturings systemen te implementeren, kan deze functie ertoe leiden dat informatie wordt vrijgegeven.  



##  <a name="privacy-information-for-os-deployment"></a><a name="bkmk_privacy"></a>Privacy-informatie voor besturingssysteem implementatie  

Naast het implementeren van een besturings systeem op computers zonder één, Configuration Manager kan worden gebruikt om de bestanden en instellingen van gebruikers van de ene computer naar de andere te migreren. De beheerder configureert welke informatie moet worden overgedragen, waaronder bestanden met persoonsgegevens, configuratie-instellingen en cookies van de browser.  

Configuration Manager slaat de informatie op een status migratie punt op en versleutelt deze tijdens de overdracht en opslag. Alleen de nieuwe computer die aan de status informatie is gekoppeld, kan de opgeslagen informatie ophalen. Als de nieuwe computer de sleutel verliest om de informatie op te halen, kan een Configuration Manager beheerder met het recht **herstel gegevens weer geven** op computer koppelings exemplaar objecten toegang hebben tot de gegevens en deze koppelen aan een nieuwe computer. Nadat de nieuwe computer de status informatie heeft teruggezet, worden de gegevens na één dag standaard verwijderd. U kunt configureren wanneer het statusmigratiepunt de voor verwijdering aangemerkte gegevens verwijdert. Configuration Manager slaat de status migratie gegevens niet op in de site database en verzendt deze niet naar micro soft.  

Als u opstart media gebruikt voor het implementeren van installatie kopieën van besturings systemen, moet u altijd de standaard optie gebruiken om de opstart media met een wacht woord te beveiligen. Het wachtwoord versleutelt eventuele in de takenreeks opgeslagen variabelen, maar eventuele niet in een variabele opgeslagen informatie is mogelijk kwetsbaar voor openbaarmaking.  

Implementatie van het besturings systeem kan gebruikmaken van taken reeksen om veel verschillende taken uit te voeren tijdens het implementatie proces, waaronder het installeren van toepassingen en software-updates. Wanneer u takenreeksen configureert, dient u zich bewust te zijn van de gevolgen van het installeren van software ten aanzien van privacy.  

Configuration Manager implementeert standaard de implementatie van het besturings systeem niet. Er zijn verschillende configuratie stappen vereist voordat u gebruikers status gegevens verzamelt of taken reeksen of opstart installatie kopieën maakt.  

Voordat u de implementatie van het besturings systeem configureert, moet u rekening houden met uw privacy-vereisten.  



## <a name="see-also"></a>Zie ook

[Diagnostische gegevens en gebruiksgegevens](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

[Beveiliging en privacy voor Configuration Manager](../../core/plan-design/security/security-and-privacy.md)

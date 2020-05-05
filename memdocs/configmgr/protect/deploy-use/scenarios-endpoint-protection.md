---
title: Computers beveiligen tegen schadelijke software
titleSuffix: Configuration Manager
description: Meer informatie over het implementeren van Endpoint Protection in Configuration Manager om computers te beveiligen tegen schadelijke software.
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.openlocfilehash: 6e0e350fe490de50a053e93f2922feba5e0ea8c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722387"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Voorbeeld scenario: Endpoint Protection gebruiken om computers te beveiligen tegen schadelijke software

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat een voorbeeld scenario voor het implementeren van Endpoint Protection in Configuration Manager om computers in uw organisatie te beveiligen tegen aanvallen via malware.  



## <a name="scenario-overview"></a>Overzicht van scenario's

 Configuration Manager wordt geïnstalleerd en gebruikt bij Woodgrove Bank. De Bank gebruikt momenteel System Center Endpoint Protection om computers te beveiligen tegen schadelijke software. Daarnaast gebruikt de bank Windows-groepsbeleid om te zorgen dat Windows Firewall is ingeschakeld op alle computers in het bedrijf en dat gebruikers een melding krijgen wanneer Windows Firewall een nieuw programma blokkeert.  

De Configuration Manager beheerders hebben gevraagd om de software van de Woodgrove Bank te upgraden naar System Center Endpoint Protection, zodat de Bank kan profiteren van de nieuwste functies van de antimalware en de oplossing van de antimalware centraal kunt beheren via de Configuration Manager-console. 


## <a name="business-requirements"></a>Zakelijke vereisten

Voor deze implementatie gelden de volgende vereisten:  

- Gebruik Configuration Manager om de Windows Firewall-instellingen te beheren die momenteel door groepsbeleid worden beheerd.  

- Gebruik Configuration Manager software-updates om definities van schadelijke software te downloaden naar computers. Als er geen software-updates beschikbaar zijn, bijvoorbeeld als de computer niet is verbonden met het bedrijfs netwerk, moeten computers definitie-updates downloaden van Microsoft Update.  

- Computers van gebruikers moeten elke dag een snelle scan op malware uitvoeren. Op servers moet echter elke zaterdag om 01:00 uur, buiten werkuren, een volledige scan worden uitgevoerd  

- Een waarschuwing per e-mail verzenden wanneer een van de volgende gebeurtenissen optreedt:  

  -   Er wordt malware gedetecteerd op een computer  

  -   Dezelfde malwarebedreiging wordt op meer dan 5 procent van de computers gedetecteerd  

  -   Dezelfde bedreiging voor schadelijke software is binnen een periode van 24 uur meer dan vijf keer gedetecteerd  

  -   In een periode van 24 uur zijn meer dan drie verschillende typen malware gedetecteerd  

  De beheerders voeren vervolgens de volgende stappen uit om Endpoint Protection te implementeren:  



##  <a name="steps-to-implement-endpoint-protection"></a> Stappen voor het implementeren van Endpoint Protection  

|Proces|Naslaginformatie|  
|-------------|---------------|  
|De beheerders bekijken de beschik bare informatie over de basis concepten voor Endpoint Protection in Configuration Manager.|Zie [Endpoint Protection](endpoint-protection.md)voor overzichts informatie over Endpoint Protection.|  
|De beheerders controleren en implementeren de vereiste onderdelen voor het gebruik van Endpoint Protection.|Zie [planning for Endpoint Protection](../plan-design/planning-for-endpoint-protection.md)voor meer informatie over de vereisten voor Endpoint Protection.|  
|De beheerders installeren de Endpoint Protection-site systeemrol op slechts één site systeem server, boven aan de hiërarchie van Woodgrove Bank.|Zie ' vereisten ' in [Endpoint Protection configureren](endpoint-protection-configure.md)voor meer informatie over het installeren van de Endpoint Protection-site systeemrol.|  
|De beheerders configureren Configuration Manager voor het gebruik van een SMTP-server om de e-mail waarschuwingen te verzenden.<br /><br /> **Opmerking:** U moet een SMTP-server alleen configureren als u per e-mail een melding wilt ontvangen wanneer een Endpoint Protection waarschuwing wordt gegenereerd.|Zie [Configure Alerts in Endpoint Protection](endpoint-configure-alerts.md)voor meer informatie.|  
|De beheerders maken een verzameling apparaten die alle computers en servers bevat om de Endpoint Protection-client te installeren. Ze noemen deze verzameling **alle computers die worden beveiligd door Endpoint Protection**.<br /><br /> **Tip:** U kunt geen waarschuwingen voor gebruikers verzamelingen configureren.|Zie [verzamelingen maken](../../core/clients/manage/collections/create-collections.md) voor meer informatie over het maken van verzamelingen.|  
|De beheerders configureren de volgende waarschuwingen voor de verzameling: <br /><br />1) **malware gedetecteerd**: de beheerders configureren de ernst van de waarschuwing **kritiek**. <br /><br />2) **hetzelfde type malware wordt gedetecteerd op een aantal computers**: de beheerders configureren de **ernst van de** waarschuwing en geven aan dat de waarschuwing wordt gegenereerd wanneer er meer dan 5 procent van de computers malware heeft gedetecteerd. <br /><br />3) **hetzelfde type malware wordt herhaaldelijk gedetecteerd binnen het opgegeven interval op een computer**: de beheerders configureren de ernst van de waarschuwing en opgeven dat de waarschuwing wordt gegenereerd wanneer Malware meer dan 5 keer in een periode van 24 uur wordt gedetecteerd. <br /><br />4) **Er zijn meerdere typen malware gedetecteerd op dezelfde computer binnen het opgegeven interval**: de beheerders configureren de ernst van de waarschuwing en opgeven dat de waarschuwing wordt gegenereerd wanneer meer dan 3 soorten malware worden gegenereerd binnen een periode van 24 uur.<br /><br /> De waarde voor **ernst van waarschuwing** geeft het waarschuwings niveau aan dat wordt weer gegeven in de Configuration Manager-console en in waarschuwingen die ze ontvangen in een e-mail bericht.<br /><br /> Ze selecteren ook de optie **deze verzameling weer geven in het dash board van Endpoint Protection** , zodat ze de waarschuwingen in de Configuration Manager-console kunnen bewaken.|Zie ' Configuring alerts for Endpoint Protection ' in [configuring Endpoint Protection](endpoint-configure-alerts.md).|  
|De beheerders configureren Configuration Manager software-updates om de definitie-updates drie keer per dag te downloaden en implementeren met behulp van een automatische implementatie regel.|Zie de sectie ' Configuration Manager software-updates gebruiken voor het leveren van definitie-updates ' in [Configuration Manager software-updates gebruiken voor het leveren van definitie-updates](endpoint-definitions-configmgr.md)voor meer informatie.|  
|De beheerders onderzoeken de instellingen in het standaard beleid voor antimalware, dat aanbevolen beveiligings instellingen van micro soft bevat. Om computers elke dag een snelle scan uit te voeren, worden de volgende instellingen gewijzigd:<br /><br /> 1) **dagelijks een snelle scan uitvoeren op client computers**: **Ja**.<br /><br /> 2) **dagelijkse tijd van snelle scan**: **9:00 uur**.<br /><br /> De beheerders zien dat updates die zijn **gedistribueerd via Microsoft Update** , standaard worden geselecteerd als een bron voor definitie-updates. Hiermee wordt voldaan aan de zakelijke vereiste dat computers definities downloaden van Microsoft Update wanneer ze geen Configuration Manager software-updates kunnen ontvangen.|Bekijk [hoe u antimalwarebeleid voor Endpoint Protection maakt en implementeert](endpoint-antimalware-policies.md).|  
|De beheerders maken een verzameling die alleen de Woodgrove Bank servers met de naam **Woodgrove Bank servers**bevat.|Meer informatie [over het maken van verzamelingen](../../core/clients/manage/collections/create-collections.md)|  
|De beheerders maken een aangepast antimalwarebeleid met de naam **Woodgrove Bank Server-beleid**. U voegt alleen de instellingen voor **geplande scans** toe en brengt de volgende wijzigingen aan:<br /><br /> **Type scan**:  **Volledig**<br /><br /> **Scandag**:  **Zaterdag**<br /><br /> **Scantijd**: **01:00**<br /><br /> **Dagelijks een snelle scan uitvoeren op clientcomputers**:  **Nee**.|Bekijk [hoe u antimalwarebeleid voor Endpoint Protection maakt en implementeert](endpoint-antimalware-policies.md).|  
|De beheerders implementeren het aangepaste antimalwarebeleid van het **Woodgrove Bank Server-beleid** voor de verzameling **Woodgrove Bank-servers** .|Zie "een antimalwarebeleid implementeren op client computers" [antimalwarebeleid voor Endpoint Protection-artikel maken en implementeren](endpoint-antimalware-policies.md) .|  
|De beheerders maken een nieuwe set aangepaste instellingen voor client apparaten voor Endpoint Protection en namen deze instellingen voor de **Woodgrove Bank Endpoint Protection**.<br /><br /> **Opmerking:** Als u Endpoint Protection niet wilt installeren en inschakelen op alle clients in uw hiërarchie, moet u ervoor zorgen dat de opties **Endpoint Protection-client op client computers beheren** en **Endpoint Protection client op client computers installeren** zijn geconfigureerd als **Nee** in de standaard instellingen van de client.|Zie [aangepaste client instellingen configureren voor Endpoint Protection](endpoint-protection-configure-client.md)voor meer informatie.|  
|Ze configureren de volgende instellingen voor Endpoint Protection:<br /><br /> **Endpoint Protection-client op client computers beheren**: **Ja**<br /><br /> Met deze instelling en waarde zorgt u ervoor dat bestaande Endpoint Protection-client die wordt geïnstalleerd, wordt beheerd door Configuration Manager.<br /><br /> **Endpoint Protection-client op clientcomputers installeren**:  **Ja**.</br></br>**Opmerking** Op Windows 10-apparaten hoeft de Endpoint Protection agent niet te zijn geïnstalleerd vanaf Configuration Manager 1802. Als de app al is geïnstalleerd op Windows 10-apparaten, wordt deze niet door Configuration Manager verwijderd. Beheerders kunnen de Endpoint Protection-agent op Windows 10-apparaten waarop ten minste de 1802-client versie wordt uitgevoerd, verwijderen.|Zie [aangepaste client instellingen configureren voor Endpoint Protection](endpoint-protection-configure-client.md)voor meer informatie.|  
|De beheerders implementeren de client instellingen voor de **Woodgrove Bank Endpoint Protection-instellingen** op **alle computers die worden beveiligd door Endpoint Protection** verzameling.|Zie ' aangepaste client instellingen configureren voor Endpoint Protection ' bij het [configureren van Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md).|  
|De beheerders gebruiken de wizard Windows Firewall beleid maken om een beleid te maken door de volgende instellingen te configureren voor het domein profiel:<br /><br /> 1) **inschakelen Windows Firewall**: **Ja**<br /><br /> twee<br />                    **De gebruiker waarschuwen wanneer een nieuw programma door Windows Firewall wordt geblokkeerd**: **Ja**|Zie [Windows Firewall beleid maken en implementeren voor Endpoint Protection](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|De beheerders implementeren het nieuwe firewall beleid voor het verzamelen **van alle computers die worden beveiligd door Endpoint Protection** die ze eerder hebben gemaakt.|Zie ' een Windows Firewall beleid implementeren ' in het [beleid voor het maken en implementeren van Windows Firewall voor Endpoint Protection](create-windows-firewall-policies.md)|  
|De beheerders gebruiken de beschik bare beheer taken voor Endpoint Protection voor het beheren van antimalware-en Windows Firewall-beleid, het uitvoeren van scans op aanvraag van computers indien nodig, het afdwingen van computers om de nieuwste definities te downloaden en om eventuele verdere acties op te geven die moeten worden ondernomen wanneer schadelijke software wordt gedetecteerd.|Meer informatie [over het beheren van antimalwarebeleid en Firewall instellingen voor Endpoint Protection](endpoint-antimalware-firewall.md)|  
|De beheerders gebruiken de volgende methoden om de status van Endpoint Protection en de acties die worden uitgevoerd door Endpoint Protection te controleren:<br /><br /> 1) met behulp van het knoop punt **Endpoint Protection status** onder **beveiliging** in de werk ruimte **bewaking** .<br /><br /> 2) met behulp van het knoop punt **Endpoint Protection** in de werk ruimte **activa en naleving** .<br /><br /> 3) met behulp van de ingebouwde Configuration Manager rapporten.|Zie [Endpoint Protection bewaken](monitor-endpoint-protection.md)|  

 De beheerder rapporteert een geslaagde implementatie van Endpoint Protection naar hun manager en bevestigt dat de computers van Woodgrove Bank nu zijn beschermd tegen antimalware, op basis van de bedrijfs vereisten die ze hebben gekregen. 

## <a name="next-steps"></a>Volgende stappen

Zie [Endpoint Protection configureren](endpoint-protection-configure.md) voor meer informatie
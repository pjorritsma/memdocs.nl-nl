---
title: Mogelijkheden van Technical Preview 1512
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1512.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f52d6956cf860de8e45ac4e532500d32bcf077ba
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074500"
---
# <a name="capabilities-in-technical-preview-1512-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1512 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1512. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.  

 Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.  

##  <a name="device-health-attestation"></a><a name="bkmk_devicehealth"></a>Apparaatstatusverklaring  
 Vanaf Technical Preview 1512 kunnen beheerders de status van Windows 10-Apparaatstatusverklaring in de Configuration Manager-console bekijken.  Deze functionaliteit is beschikbaar voor Configuration Manager en Configuration Manager met Microsoft Intune. Met Health Attestation van apparaten kan de beheerder zorgen dat clientcomputers over betrouwbare configuraties van BIOS, TPM en opstartsoftware beschikken. Voor de ondersteuning van apparaatstatusverklaring moeten op client apparaten Win10 worden uitgevoerd met TPM 2 ingeschakeld. Met Health Attestation van apparaten wordt het aantal apparaten weergegeven dat is ingeschakeld voor elk van de volgende:  

-   Vroegtijdig starten van anti-malware  

-   BitLocker  

-   Secure Boot  

-   Code-integriteit  

In de-console worden ook de belangrijkste ontbrekende instellingen voor status attesten met het aantal apparaten weer gegeven.  

Als u de weer gave van de apparaatstatusverklaring wilt bekijken, gaat u in de Configuration Manager-console naar de werk ruimte **bewaking** van, klikt u op **beveiligings** knooppunt en klikt u vervolgens op **Health Attestation**.  

##  <a name="in-console-monitoring-for-terms-and-conditions"></a><a name="bkmk_viewterms"></a>Bewaking in de console voor voor waarden  
Met ingang van Technical Preview 1512, wanneer u Configuration Manager integreert met Microsoft Intune, kunt u de Configuration Manager-console gebruiken om te zien welke gebruikers de voor waarden hebben geaccepteerd die zijn geconfigureerd door uw IT-afdeling en welke gebruikers dat niet hebben.  

**Samenvattings informatie weer geven:**  

-   Ga in de Configuration Manager-console naar **bewakings** > **overzicht** > **implementaties** en selecteer de implementatie van de voor waarden die u wilt weer geven.  

**Gedetailleerde informatie weer geven:**  

1.  Ga in de Configuration Manager-console naar **activa en naleving** > **overzicht** > **voor waarden voor****nalevings instellingen** > en selecteer de voor waarden die u wilt weer geven.  

2.  Selecteer aan de onderkant van de console het tabblad **implementaties** , selecteer de implementatie en klik vervolgens op **status weer geven.**  

##  <a name="improvements-to-endpoint-protection-policy-settings"></a><a name="bkmk_EPpolicy"></a>Verbeteringen aan Endpoint Protection-beleids instellingen  
In de 1512 Technical Preview zijn de volgende nieuwe instellingen toegevoegd in Endpoint Protection antimalware-beleid:  

-   Real-time beveiliging: **mogelijk ongewenste toepassingen blok keren tijdens het downloaden en voorafgaand aan de installatie**  

    -   Potentieel ongewenste toepassingen (PUA’s) is een bedreigingsclassificatie op basis van reputatie en op onderzoek gebaseerde identificatie. Meestal betreft dit partijen die ongewenste toepassingen bundelen of hun gebundelde toepassingen.  

    -   De beveiligings beleids instelling is standaard ingeschakeld (ingesteld op Ja). Wanneer deze optie is ingeschakeld, worden PUA’s geblokkeerd tijdens downloaden en installeren. U kunt echter specifieke bestanden of mappen uitsluiten om te voldoen aan de specifieke behoeften van uw omgeving.  

-   Scan instellingen: **toegewezen netwerk stations scannen bij het uitvoeren van een volledige scan**  

    -   Deze instelling biedt een grotere nauw keurigheid voor de beheerder om scans op aanvraag van netwerk bestanden toe te staan zonder het risico dat toegewezen netwerk stations altijd worden gescand tijdens een geplande volledige scan.  

    -   De instelling **netwerk bestanden scannen** moet eerst worden ingeschakeld (Ja) om deze instelling te kunnen configureren.  

    -   Standaard is deze instelling Nee, wat betekent dat een volledige scan geen toegang krijgt tot toegewezen netwerk stations.  

-   Instellingen voor automatisch verzenden van voorbeeld bestanden:  

     De antimalware-engine kan aanvragen dat bestands voorbeelden naar micro soft worden verzonden voor verdere analyse. Standaard wordt altijd om bevestiging gevraagd voordat dergelijke voorbeeldbestanden worden verzonden. Beheerders kunnen nu de volgende instellingen beheren om dit gedrag te configureren:  

    -   Geavanceerd: **automatisch verzenden van voorbeeld bestanden inschakelen zodat micro soft kan bepalen of bepaalde gedetecteerde items schadelijk zijn**: Stel deze instelling in op Ja om automatisch verzenden van voorbeeld bestanden in te scha kelen. Deze instelling is standaard Nee. Dit houdt in dat automatisch verzenden van voorbeeld bestanden is uitgeschakeld en dat gebruikers wordt gevraagd om voor beelden te verzenden.   (Deze instelling werd voor het eerst geïntroduceerd in System Center 2012 R2 Configuration Manager SP1)  

    -   Geavanceerd: **toestaan dat gebruikers instellingen voor automatisch verzenden van voorbeeld bestanden wijzigen**: deze instelling bepaalt of een gebruiker met lokale beheerders rechten op een apparaat de instelling voor automatisch verzenden van voorbeeld bestanden kan wijzigen in de client interface. Deze instelling is standaard ingesteld op Nee. Dit betekent dat de instellingen alleen kunnen worden gewijzigd vanuit de Configuration Manager-console en dat lokale beheerders op een apparaat deze configuratie niet kunnen wijzigen.  

         In het volgende voor beeld ziet u de Windows Defender-instelling in Windows 10 die door de beheerder is ingesteld als ingeschakeld en de gebruiker deze niet mag wijzigen:  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    Daarnaast is de bestaande instelling **bestanden en mappen uitsluiten** in de sectie uitsluitings instellingen van het antimalwarebeleid van Endpoint Protection verbeterd zodat het apparaat kan worden uitgesloten. U kunt nu bijvoorbeeld het volgende opgeven als een uitsluiting: **\device\mvfs** (voor Multiversion-bestandssysteem). Met het beleid wordt het pad naar het apparaat niet gevalideerd. het Endpoint Protection-beleid wordt aan de antimalware-engine op de client door gegeven dat de teken reeks van het apparaat moet kunnen interpreteren.  

**Vereisten voor het gebruik van Endpoint Protection-beleid:**  

Voordat u Endpoint Protection-beleid kunt gebruiken, moet u de Endpoint Protection-client installeren en beheren door gebruik te maken van de Endpoint Protection client instellingen. Dit wordt gedaan met behulp van de System Center Endpoint Protection-client voor Windows 7, Windows 8, Windows 8,1 of beheerde Windows Defender voor Windows 10. Zie [Endpoint Protection](../../protect/deploy-use/endpoint-protection.md).  

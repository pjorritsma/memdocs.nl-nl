---
title: Inleiding tot certificaatprofielen
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van certificaat profielen in Configuration Manager met Active Directory Certificate Services.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 35269e7c727031a9cd66072985f3d9ec362978cf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722303"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>Inleiding tot certificaat profielen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Certificaat profielen werken met Active Directory Certificate Services en de rol registratie service voor netwerk apparaten (NDES). Maak en implementeer verificatie certificaten voor beheerde apparaten zodat gebruikers eenvoudig toegang kunnen krijgen tot bedrijfs resources. U kunt bijvoorbeeld certificaat profielen maken en implementeren om gebruikers de benodigde certificaten te geven om verbinding te maken met VPN-en draadloze verbindingen.

Met certificaat profielen kunnen gebruikers apparaten automatisch worden geconfigureerd voor toegang tot bedrijfs bronnen zoals Wi-Fi-netwerken en VPN-servers. Gebruikers hebben toegang tot deze bronnen zonder hand matig certificaten te installeren of een out-of-band-proces te gebruiken. Certificaat profielen helpen bij het beveiligen van resources omdat u veiligere instellingen kunt gebruiken die worden ondersteund door uw open bare-sleutel infrastructuur (PKI). Bijvoorbeeld Server verificatie vereisen voor alle Wi-Fi-en VPN-verbindingen omdat u de vereiste certificaten op de beheerde apparaten hebt geïmplementeerd.

Certificaatprofielen bieden de volgende beheermogelijkheden:  

- Certificaat registratie en-vernieuwing van een certificerings instantie (CA) voor apparaten met verschillende typen besturings systemen en versies. Deze certificaten kunnen vervolgens worden gebruikt voor Wi-Fi-en VPN-verbindingen.  

- Implementatie van vertrouwde basis-CA-certificaten en tussenliggende CA-certificaten. Deze certificaten configureren een vertrouwens keten op apparaten voor VPN-en Wi-Fi-verbindingen wanneer Server verificatie is vereist.  

- De geïnstalleerde certificaten bewaken en hierover rapporteren.  

**Voor beeld 1**: alle werk nemers moeten verbinding maken met Wi-Fi-HOTS pots op meerdere kantoor locaties. Als u eenvoudige gebruikers verbinding wilt inschakelen, moet u eerst de certificaten implementeren die nodig zijn om verbinding te maken met Wi-Fi. Implementeer vervolgens Wi-Fi-profielen die naar het certificaat verwijzen.  

**Voor beeld 2**: er is een PKI aanwezig. U wilt overstappen op een flexibeler, veilige methode voor het implementeren van certificaten. Gebruikers moeten toegang hebben tot de resources van uw organisatie vanaf hun eigen apparaten zonder dat dit van beveiliging in gevaar komt. Certificaat profielen configureren met instellingen en protocollen die worden ondersteund voor het specifieke platform van het apparaat. De apparaten kunnen deze certificaten vervolgens automatisch aanvragen van een inschrijvings server op internet. Configureer vervolgens VPN-profielen om deze certificaten te gebruiken, zodat het apparaat toegang kan krijgen tot de bronnen van de organisatie.  

## <a name="types"></a>Typen

Er zijn drie typen certificaat profielen:  

- **Vertrouwd CA-certificaat**: Implementeer een vertrouwde basis-CA of een tussenliggend CA-certificaat. Deze certificaten vormen een vertrouwens keten wanneer het apparaat een server moet verifiëren.  

- **Simple Certificate Enrollment Protocol (SCEP)**: een certificaat voor een apparaat of gebruiker aanvragen door het SCEP-protocol te gebruiken. Dit type vereist de NDES-rol (Network Device Enrollment Service) op een server met Windows Server 2012 R2 of hoger.

    Als u een **Simple Certificate Enrollment Protocol SCEP-** certificaat profiel wilt maken, moet u eerst een profiel voor een **vertrouwd CA-certificaat** maken.

- **Personal Information Exchange (. pfx)**: een pfx-certificaat (ook wel PKCS #12 genoemd) aanvragen voor een apparaat of gebruiker.<!--1321368--> Er zijn twee methoden voor het maken van PFX-certificaat profielen:

  - [Referenties importeren](../../mdm/deploy-use/import-pfx-certificate-profiles.md) uit bestaande certificaten
  - [Een certificerings](../../mdm/deploy-use/create-pfx-certificate-profiles.md) instantie voor het verwerken van aanvragen definiëren

  > [!Note]  
  > Configuration Manager schakelt deze optionele functie standaard niet in. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

  U kunt micro soft of de vertrouwens bevoegdheid gebruiken als certificerings instantie voor **PFX-certificaten (Personal Information Exchange)** .

## <a name="requirements"></a>Vereisten

Als u certificaat profielen wilt implementeren die gebruikmaken van SCEP, installeert u het certificaat registratiepunt op een site systeem server. Installeer ook een beleids module voor NDES, de Configuration Manager-beleids module, op een server met Windows Server 2012 R2 of hoger. Voor deze server is de Active Directory-rol Certificate Services vereist. Er is ook een werkende NDES vereist die toegankelijk is voor de apparaten die de certificaten nodig hebben. Als uw apparaten moeten worden inge schreven voor certificaten van Internet, moet uw NDES-server toegankelijk zijn via internet. Als u bijvoorbeeld veilig verkeer naar de NDES-server via internet wilt inschakelen, kunt u [Azure-toepassing proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy)gebruiken.

Voor PFX-certificaten is ook een certificaat registratiepunt vereist. Geef ook de certificerings instantie (CA) voor het certificaat en de relevante toegangs referenties op. U kunt micro soft of de belasters als certificerings instantie opgeven.  

Zie [een beleids module gebruiken met de registratie service voor netwerk apparaten](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\))voor meer informatie over hoe NDES een beleids module ondersteunt, zodat Configuration Manager certificaten kan implementeren.

Afhankelijk van de vereisten ondersteunt Configuration Manager de implementatie van certificaten in verschillende certificaat archieven op verschillende apparaattypen en besturings systemen. De volgende apparaten en besturingssystemen worden ondersteund:  

- Windows 10

- Windows 10 Mobile

- Windows 8.1  

- Windows Phone 8.1  

> [!NOTE]  
> Gebruik Configuration Manager on-premises MDM om Windows Phone 8,1 en Windows 10 Mobile te beheren. Zie [on-premises MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)voor meer informatie.

Een typisch scenario voor Configuration Manager is het installeren van vertrouwde basis-CA-certificaten voor het verifiëren van Wi-Fi-en VPN-servers. Typische verbindingen gebruiken de volgende protocollen:

- Verificatie protocollen: EAP-TLS, EAP-TTLS en PEAP
- Protocollen voor VPN-tunneling: IKEv2, L2TP/IPsec en Cisco IPsec

Een basis-CA-certificaat van de onderneming moet worden geïnstalleerd op het apparaat voordat het apparaat certificaten kan aanvragen met behulp van een SCEP-certificaat profiel.  

U kunt instellingen opgeven in een SCEP-certificaat profiel om aangepaste certificaten aan te vragen voor verschillende omgevingen of connectiviteits vereisten. De **wizard Certificaat profiel maken** heeft twee pagina's voor registratie parameters. De eerste, **SCEP-inschrijving**, bevat instellingen voor de registratie aanvraag en waar het certificaat moet worden geïnstalleerd. Op de tweede pagina, **Certificaateigenschappen**, wordt het aangevraagde certificaat zelf beschreven.  

## <a name="deploy"></a>Implementeren

Wanneer u een SCEP-certificaat profiel implementeert, verwerkt de Configuration Manager-client het beleid. Vervolgens wordt er een wacht woord voor de SCEP-controle aangevraagd vanaf het beheer punt. Het apparaat maakt een openbaar/persoonlijk sleutel paar en genereert een aanvraag voor certificaat ondertekening (CSR). Deze aanvraag wordt verzonden naar de NDES-server. De NDES-server stuurt de aanvraag door naar het site systeem van het certificaat registratiepunt via de NDES-beleids module. Het certificaat registratiepunt valideert de aanvraag, controleert het wacht woord voor de SCEP-vraag en controleert of de aanvraag niet is geknoeid. Vervolgens wordt de aanvraag goedgekeurd of geweigerd. Indien goedgekeurd, verzendt de NDES-server de handtekening aanvraag naar de verbonden certificerings instantie (CA) voor ondertekening. De CA ondertekent de aanvraag en retourneert vervolgens het certificaat naar het aangevraagde apparaat.

Certificaat profielen implementeren in verzamelingen van gebruikers of apparaten. U kunt het doel Archief voor elk certificaat opgeven. Regels voor toepasselijkheid bepalen of het apparaat het certificaat kan installeren.

Wanneer u een certificaat profiel implementeert voor een gebruikers verzameling, bepaalt de [gebruikers affiniteit](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) van het apparaat op welke van de apparaten van de gebruikers de certificaten worden geïnstalleerd. Wanneer u een certificaat profiel implementeert met een gebruikers certificaat naar een apparaatgroep, worden standaard de certificaten door elk van de primaire apparaten van de gebruiker geïnstalleerd. Als u het certificaat op een van de apparaten van de gebruiker wilt installeren, wijzigt u dit gedrag op de pagina **SCEP-registratie** van de **wizard Certificaat profiel maken**. Als de apparaten zich in een werk groep bevinden, wordt Configuration Manager gebruikers certificaten niet geïmplementeerd.  

## <a name="monitor"></a>Controleren

U kunt de implementaties van certificaat profielen bewaken door nalevings resultaten of-rapporten te bekijken. Zie [certificaat profielen bewaken](monitor-certificate-profiles.md)voor meer informatie.

## <a name="automatic-revocation"></a>Automatische intrekking

Configuration Manager worden automatisch gebruikers-en computer certificaten ingetrokken die zijn geïmplementeerd met behulp van certificaat profielen in de volgende omstandigheden:  

- Het apparaat wordt buiten gebruik gesteld Configuration Manager beheer.  

- Het apparaat is geblokkeerd voor de Configuration Manager-hiërarchie.  

Om de certificaten in te trekken, wordt er vanaf de siteserver een intrekkingsopdracht verzonden naar de uitgevende certificeringsinstantie. De reden voor de intrekking is **Activiteit gestaakt**.

> [!NOTE]
> Voor een correcte intrekking van een certificaat moet het computer account voor de site op het hoogste niveau in de-hiërarchie de machtiging hebben om **certificaten te verlenen en te beheren** op de ca.
>
> Voor een betere beveiliging kunt u ook CA-beheerders op de CA beperken. Geef deze account vervolgens alleen machtigingen op het specifieke certificaat sjabloon dat u voor de SCEP-profielen op de site gebruikt.

## <a name="next-steps"></a>Volgende stappen

- [Certificaatprofielen maken](create-certificate-profiles.md)

- [Certificaatinfrastructuur configureren](certificate-infrastructure.md)

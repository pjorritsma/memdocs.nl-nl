---
title: Instellingen voor Windows Hello voor Bedrijven in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk een lijst met alle pincodes, biometrische instellingen, en instellingen voor anti-adresvervalsing in een Identity Protection-profiel om Windows Hello voor Bedrijven te gebruiken op Windows 10-apparaten in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/20/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: b4581ba6bdc8b5be41d5cf567c631ffaad40d418
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351965"
---
# <a name="windows-10-device-settings-to-enable-windows-hello-for-business-in-intune"></a>Windows 10 device settings to enable Windows Hello for Business in Intune (Instellingen voor Windows 10-apparaten om Windows Hello voor Bedrijven in Intune in te schakelen)

Dit artikel bevat een overzicht en beschrijving van de instellingen voor Windows Hello voor Bedrijven die u kunt beheren op Windows 10-apparaten in Intune. Als Intune-beheerder kunt u deze instellingen configureren en toewijzen aan Windows 10-apparaten als onderdeel van uw MDM-oplossing (Mobile Device Management). 

U kunt meer informatie over deze instellingen vinden in [Beleidsinstellingen configureren voor Windows Hello voor Bedrijven](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings) in de Windows Hello-documentatie.


Zie [Identity Protection configureren](identity-protection-configure.md) voor meer informatie over Windows Hello voor Bedrijven-profielen in Intune.

## <a name="before-you-begin"></a>Voordat u begint

[Een configuratieprofiel maken](identity-protection-configure.md#create-the-device-profile).

## <a name="windows-hello-for-business"></a>Windows Hello voor Bedrijven
- **Windows Hello voor Bedrijven configureren**:
  - **Niet geconfigureerd**: selecteer deze instelling als u niet met Intune instellingen voor Windows Hello voor Bedrijven wilt beheren. Alle eventueel bestaande Windows Hello voor Bedrijven-instellingen voor Windows 10-apparaten worden niet gewijzigd. Alle andere instellingen in het deelvenster zijn niet beschikbaar.

  - **Uitgeschakeld**: als u Windows Hello voor Bedrijven niet wilt gebruiken, selecteert u deze instelling. Alle andere instellingen op het scherm zijn niet beschikbaar.
  - **Ingeschakeld**: selecteer deze instelling als u instellingen voor Windows Hello voor Business wilt configureren.  
  
  **Standaardinstelling**: Niet geconfigureerd

  Indien ingesteld op *Ingeschakeld* zijn de volgende instellingen beschikbaar:

  - **Minimale lengte pincode**  
    Geef een minimale lengte voor de pincode voor apparaten op om het aanmelden beter te beveiligen. De standaardwaarden van Windows-apparaten zijn zes tekens, maar met deze instelling kunnen minimaal vier tot 127 tekens worden afdwongen. 

    **Standaardinstelling**: *Niet geconfigureerd*

  - **Maximale lengte pincode**  
  Geef een maximale lengte voor de pincode voor apparaten op om het aanmelden beter te beveiligen. De standaardwaarden van Windows-apparaten zijn zes tekens, maar met deze instelling kunnen minimaal vier tot 127 tekens worden afdwongen.  

    **Standaardinstelling**: *Niet geconfigureerd*  

  - **Kleine letters in pincode**  
    U kunt een sterkere pincode afdwingen door te vereisen dat eindgebruikers kleine letters opnemen. Uw opties zijn:

    - **Niet toegestaan**: blokkeren dat gebruikers kleine letters gebruiken in de pincode. Dit gedrag treedt ook op als de instelling niet is geconfigureerd.
    - **Toegestaan**: toestaan dat gebruikers kleine letters gebruiken in de pincode. Dit is echter niet vereist.
    - **Vereist**: gebruikers moeten minstens één kleine letter opnemen in hun pincode. Het is bijvoorbeeld gebruikelijk om ten minste één hoofdletter en één speciaal teken verplicht te stellen.

  - **Hoofdletters in pincode**  
    U kunt een sterkere pincode afdwingen door te vereisen dat eindgebruikers hoofdletters opnemen. Uw opties zijn:

    - **Niet toegestaan**: blokkeren dat gebruikers hoofdletters gebruiken in de pincode. Dit gedrag treedt ook op als de instelling niet is geconfigureerd.
    - **Toegestaan**: toestaan dat gebruikers hoofdletters gebruiken in de pincode. Dit is echter niet vereist.
    - **Vereist**: gebruikers moeten minstens één hoofdletter opnemen in hun pincode. Het is bijvoorbeeld gebruikelijk om ten minste één hoofdletter en één speciaal teken verplicht te stellen.

  - **Speciale tekens in pincode**  
    U kunt een sterkere pincode afdwingen door te vereisen dat eindgebruikers speciale tekens opnemen. Tot de speciale tekens behoren: `! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~`  

    Uw opties zijn:
    - **Niet toegestaan**: blokkeren dat gebruikers speciale tekens gebruiken in de pincode. Dit gedrag treedt ook op als de instelling niet is geconfigureerd.
    - **Toegestaan**: toestaan dat gebruikers hoofdletters gebruiken in de pincode. Dit is echter niet vereist.
    - **Vereist**: gebruikers moeten minstens één hoofdletter opnemen in hun pincode. Het is bijvoorbeeld gebruikelijk om ten minste één hoofdletter en één speciaal teken verplicht te stellen.

    **Standaardinstelling**: Niet toegestaan

  - **Verlooptijd pincode (dagen)**  
    Het is raadzaam om een verloopperiode voor een pincode op te geven, waarna gebruikers deze moeten wijzigen. De standaardinstelling voor Windows-apparaten is 41 dagen.

    **Standaardinstelling**: Niet geconfigureerd

  - **Pincodegeschiedenis onthouden**  
    Beperkt het hergebruik van eerder gebruikte pincodes. De standaard voor Windows-apparaten is hergebruik van de laatste vijf pincodes te voorkomen.  

    **Standaardinstelling**: Niet geconfigureerd  

  - **Herstel van pincode inschakelen**   
    Hiermee kan de gebruiker gebruikmaken van de pincodeherstelservice van Windows Hello voor Bedrijven. 
    
    - **Ingeschakeld**: het geheim voor pincodeherstel wordt opgeslagen op het apparaat en de gebruiker kan de pincode zo nodig wijzigen.  
    - **Uitgeschakeld**: er wordt geen geheim voor pincodeherstel gemaakt of opgeslagen.

    **Standaardinstelling**: Niet geconfigureerd

  - **Een TPM (Trusted Platform Module) gebruiken**   
    Een TPM-chip biedt een extra laag gegevensbeveiliging.  

    - **Ingeschakeld**: alleen apparaten met een toegankelijke TPM kunnen Windows Hello voor Bedrijven inrichten.
    - **Niet geconfigureerd**: apparaten proberen eerst een TPM te gebruiken. Als deze niet beschikbaar is, kunnen ze softwareversleuteling gebruiken.
    
    **Standaardinstelling**: Niet geconfigureerd

  - **Biometrische verificatie toestaan**  
     Hiermee kunt u biometrische verificatie, zoals gezichtsherkenning of een vingerafdruk, inschakelen als alternatief voor een pincode voor Windows Hello voor Bedrijven. Gebruikers moeten toch een pincode voor Passport for Work configureren voor het geval dat biometrische verificatie mislukt. U kunt kiezen uit:

    - **Inschakelen**: Windows Hello voor bedrijven staat biometrische verificatie toe.
    - **Niet geconfigureerd**: het gebruik van biometrische verificatie (voor alle accounttypen) is niet toegestaan in Windows Hello voor Bedrijven.

    **Standaardinstelling**: Niet geconfigureerd

  - **Verbeterde anti-adresvervalsing gebruiken, indien beschikbaar**  
    Hiermee configureert u of de functies voor anti-adresvervalsing van Windows Hello worden gebruikt op apparaten die deze functie ondersteunen (bijvoorbeeld een foto van een gezicht in plaats van een echt gezicht detecteren).  
    - **Inschakelen**: Windows verplicht alle gebruikers om anti-adresvervalsing te gebruiken voor gezichtskenmerken, indien dit wordt ondersteund.
    - **Niet geconfigureerd**: Windows houdt zich aan de anti-adresvervalsingsconfiguraties van het apparaat.

    **Standaardinstelling**: Niet geconfigureerd

  - **Certificaat voor on-premises resources**  

    - **Inschakelen**: hiermee staat u Windows Hello voor Bedrijven toe certificaten te gebruiken voor verificatie bij on-premises resources.
    - **Niet geconfigureerd**: hiermee voorkomt u dat Windows Hello voor Bedrijven certificaten gebruikt voor verificatie bij on-premises resources. In plaats daarvan maken apparaten gebruik van het standaardgedrag van *On-premises verificatie met sleutelvertrouwen*. Zie [Gebruikerscertificaat voor on-premises verificatie](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings#use-certificate-for-on-premises-authentication) in de Windows Hello-documentatie voor meer informatie.  

  **Standaardinstelling**: Niet geconfigureerd

- **Beveiligingssleutels gebruiken voor aanmelden**  
  Deze instelling is beschikbaar voor apparaten waarop Windows 10 versie 1903 of hoger wordt uitgevoerd. Maak er gebruik van om ondersteuning te beheren voor het gebruik van Windows Hello-beveiligingssleutels voor aanmelden.  

  - **Ingeschakeld**: gebruikers kunnen een Windows Hello-beveiligingssleutel gebruiken als aanmeldingsreferentie voor pc's waarop dit beleid is gericht. 
  - **Uitgeschakeld**: beveiligingssleutels zijn uitgeschakeld en gebruikers kunnen deze niet gebruiken om zich aan te melden bij pc's.   

  **Standaardinstelling**: Niet geconfigureerd

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](../configuration/device-profile-assign.md) en [de status ervan controleren](../configuration/device-profile-monitor.md).

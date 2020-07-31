---
title: Windows Hello voor Bedrijven integreren in Microsoft Intune
titleSuffix: Microsoft Intune
description: In dit onderwerp leest u hoe u een beleid kunt maken om het gebruik van Windows Hello voor Bedrijven op beheerde apparaten te beheren tijdens de apparaatinschrijving.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: d120ee0f55651ab1661e426e5889aaf8a4c7e670
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262860"
---
# <a name="integrate-windows-hello-for-business-with-microsoft-intune"></a>Windows Hello voor Bedrijven integreren in Microsoft Intune  

U kunt Windows Hello voor Bedrijven (voorheen Microsoft Passport for Work) integreren in Microsoft Intune tijdens een apparaatinschrijving.

Hello voor Bedrijven biedt een alternatieve aanmeldingsmethode waarbij Active Directory of een Azure Active Directory-account wordt gebruikt om een wachtwoord, smartcard of virtuele smartcard te vervangen. Hiermee kan de gebruiker zich aanmelden met een *gebaar* in plaats van met een wachtwoord. Een gebaar van de gebruiker kan een pincode zijn, biometrische verificatie zoals Windows Hello of een extern apparaat zoals een vingerafdruklezer.

Intune integreert op twee manieren met Hello voor bedrijven:

- **Voor de hele tenant** (*dit artikel)* : Een Intune-beleid kan worden gemaakt onder *apparaatinschrijving*. Dit beleid is gericht op de hele organisatie (tenant-breed). Het biedt ondersteuning voor het Windows AutoPilot out-of-box-experience (OOBE) en wordt toegepast wanneer een apparaat wordt ingeschreven.
- **Discrete groepen**: Voor apparaten die eerder zijn geregistreerd bij Intune gebruikt u een [identiteitsbeveiligings**profiel voor** apparaatconfiguratie](../protect/identity-protection-configure.md) voor het configureren van apparaten voor Windows Hello voor Bedrijven. Identiteitsbeveiligingsprofielen zijn gericht op toegewezen gebruikers of apparaten en gelden tijdens het inchecken.

Daarnaast biedt Intune ondersteuning voor de volgende typen beleid voor het beheren van bepaalde instellingen voor Windows Hello voor Bedrijven:

- [**Beveiligingsbasislijnen**](../protect/security-baselines.md). De volgende basislijnen bevatten instellingen voor Windows Hello voor Bedrijven:
  - [Microsoft Defender Advanced Threat Protection-basislijninstellingen](../protect/security-baseline-settings-defender-atp.md#windows-hello-for-business)
  - [Instellingen voor Windows MDM-beveiligingsbasislijn](../protect/security-baseline-settings-mdm-all.md#windows-hello-for-business)
- [Eindpuntbeveiligingsbeleid**voor**accountbeveiliging](../protect/endpoint-security-account-protection-policy.md). Bekijk de [beveiligingsinstellingen voor het account](../protect/endpoint-security-account-protection-profile-settings.md#account-protection).

De rest van dit artikel gaat over het maken van een standaard Windows Hello voor Bedrijven-beleid dat gericht is op uw hele organisatie.

> [!IMPORTANT]
> In Windows 10 Desktop en Windows 10 Mobile vóór de jubileumupdate kunt u twee verschillende pincodes instellen voor het verifiëren van resources:
>
> - U kunt de **pincode van het apparaat** gebruiken om het apparaat te ontgrendelen en verbinding te maken met cloudresources.
> - De **pincode voor werk** werd gebruikt om toegang tot krijgen tot de Azure AD-resources op de persoonlijke apparaten van de gebruiker (BYOD).
> 
> In de jubileumupdate zijn deze twee pincodes samengevoegd tot één pincode voor het apparaat.
> De waarde voor deze nieuwe pincode wordt ingesteld op basis van de Intune-configuratiebeleidsregels die u hebt ingesteld voor het beheer van de pincode van het apparaat, en eventuele Windows Hello-bedrijfsbeleidsregels die u hebt geconfigureerd.
> Als u beide beleidstypen voor het beheren van de pincode hebt ingesteld, wordt het Windows Hello-bedrijfsbeleid toegepast op apparaten met zowel Windows 10 Desktop als apparaten met Windows 10 Mobile.
> Als u ervoor wilt zorgen dat beleidsconflicten worden opgelost en het pincodebeleid correct wordt toegepast, werkt u het Windows Hello-bedrijfsbeleid bij zodat dit overeenkomt met de instellingen in het configuratiebeleid. Vervolgens vraagt u de gebruikers hun apparaten te synchroniseren in de bedrijfsportal-app.



## <a name="create-a-windows-hello-for-business-policy"></a>Een beleid voor Windows Hello voor Bedrijven maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Ga naar **Apparaten** >  **Inschrijving** > **Apparaten inschrijven** > **Windows-inschrijving** > **Windows Hello voor Bedrijven**. Het deelvenster Windows Hello voor Bedrijven wordt geopend.

3. Selecteer een van de volgende opties voor **Windows Hello voor Bedrijven configureren**:

     - **Ingeschakeld**. Selecteer deze instelling als u instellingen voor Windows Hello voor Business wilt configureren.  Wanneer u *Ingeschakeld* selecteert, worden extra instellingen voor Windows Hello zichtbaar en kunnen ze voor apparaten worden geconfigureerd.

    - **Uitgeschakeld**. Selecteer deze optie als u Windows Hello voor Bedrijven niet wilt inschakelen tijdens de apparaatinschrijving. Als deze optie is uitgeschakeld, kunnen gebruikers Windows Hello voor Bedrijven niet inrichten, behalve op aan Azure Active Directory gekoppelde mobiele telefoons waarvoor het inrichten mogelijk vereist is. Wanneer deze optie is ingesteld op *Uitgeschakeld*, kunt u nog steeds de volgende instellingen voor Windows Hello voor Bedrijven configureren, zelfs als met dit beleid Windows Hello voor Bedrijven niet wordt ingeschakeld.

    - **Niet geconfigureerd**. Selecteer deze instelling als u niet met Intune instellingen voor Windows Hello voor Bedrijven wilt beheren. Alle eventueel bestaande Windows Hello voor Bedrijven-instellingen voor Windows 10-apparaten worden niet gewijzigd. Alle andere instellingen in het deelvenster zijn niet beschikbaar.

4. Als u in de vorige stap **Ingeschakeld** hebt geselecteerd, configureert u de vereiste instellingen die worden toegepast op alle ingeschreven Windows 10- en Windows 10 Mobile-apparaten. Nadat u deze instellingen hebt geconfigureerd, selecteert u **Opslaan**.

   - **Een TPM (Trusted Platform Module) gebruiken**:

     Een TPM-chip biedt een extra laag gegevensbeveiliging. Kies een van de volgende waarden:

     - **Vereist** (standaard). Alleen apparaten met een toegankelijke TPM kunnen Windows Hello voor Bedrijven inrichten.
     - **Voorkeur**. Apparaten proberen eerst een TPM te gebruiken. Als deze optie niet beschikbaar is, kunnen ze softwareversleuteling gebruiken.

   - **Minimumlengte voor pincode** en **Maximumlengte voor pincode**:

     Hiermee configureert u apparaten om de opgegeven minimum- en maximumlengte van de pincode te gebruiken voor het beveiligen van de aanmelding. De standaardwaarde voor de pincode is zes tekens, maar u kunt een minimumlengte van vier tekens afdwingen. De maximumlengte voor de pincode is 127 tekens.

   - **Kleine letters in pincode**, **Hoofdletters in pincode** en **Speciale tekens in pincode**.

     U kunt zorgen voor sterkere pincodes door het gebruik van kleine letters, hoofdletters en speciale tekens voor de pincode af te dwingen. Selecteer voor elk tekentype een van de volgende opties:

     - **Toegestaan**. Gebruikers kunnen het tekentype gebruiken in hun pincode, maar dit is niet verplicht.

     - **Vereist**. Gebruikers moeten ten minste een van de tekentypen in hun pincode opnemen. Het is bijvoorbeeld gebruikelijk om ten minste één hoofdletter en één speciaal teken verplicht te stellen.

     - **Niet toegestaan** (standaardinstelling). Gebruikers mogen deze tekentypen niet in hun pincode gebruiken. (Dit is ook het gedrag als de instelling niet is geconfigureerd.)

       Tot de speciale tekens behoren: **! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~**

   - **Verlooptijd pincode (dagen)** :

     Het is raadzaam om een verloopperiode voor een pincode op te geven, waarna gebruikers deze moeten wijzigen. De standaardwaarde is 41 dagen.

   - **Pincodegeschiedenis onthouden**:

     Beperkt het hergebruik van eerder gebruikte pincodes. Standaard kunnen de laatste 5 gebruikte pincodes niet opnieuw worden gebruikt.

   - **Biometrische verificatie toestaan**:

     Hiermee kunt u biometrische verificatie, zoals gezichtsherkenning of een vingerafdruk, inschakelen als alternatief voor een pincode voor Windows Hello voor Bedrijven. Gebruikers moeten toch een pincode voor Passport for Work configureren voor het geval dat biometrische verificatie mislukt. U kunt kiezen uit:

     - **Ja**. Windows Hello voor bedrijven staat biometrische verificatie toe.
     - **Nee**. Windows Hello voor Bedrijven staat biometrische verificatie niet toe (voor alle typen accounts).

   - **Verbeterde anti-adresvervalsing gebruiken, indien beschikbaar**:

     hiermee wordt geconfigureerd of de anti-adresvervalsingsfuncties van Windows Hello worden gebruikt op apparaten die hier ondersteuning voor bieden. Bijvoorbeeld een foto van een gezicht detecteren in plaats van een echt gezicht.

     Als deze optie is ingesteld op **Ja**, moeten alle gebruikers anti-adresvervalsing gebruiken voor gezichtskenmerken, indien dat wordt ondersteund.

   - **Aanmelding via de telefoon toestaan**:

     Als u deze optie instelt op **Ja**, kunnen gebruikers een extern passport gebruiken als draagbaar begeleidingsapparaat voor verificatie op desktopcomputers. De computer moet zijn toegevoegd aan Azure Active Directory en het begeleidingsapparaat moet worden geconfigureerd met een pincode voor Windows Hello voor Bedrijven.

## <a name="windows-holographic-for-business-support"></a>Ondersteuning voor Windows Holographic for Business

De volgende instellingen voor Windows Hello for Business worden in Windows Holographic for Business ondersteund:

- Een Trusted Platform Module (TPM) gebruiken
- Minimumlengte voor pincode
- Maximumlengte voor pincode
- Kleine letters in pincode
- Hoofdletters in pincode
- Speciale tekens in pincode
- Verlooptijd pincode (dagen)
- Pincodegeschiedenis onthouden

## <a name="next-steps"></a>Volgende stappen

Zie [de gids](https://technet.microsoft.com/library/mt589441.aspx) in de documentatie van Windows 10 voor meer informatie over Windows Hello voor Bedrijven.

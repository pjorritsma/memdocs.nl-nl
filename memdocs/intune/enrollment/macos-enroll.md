---
title: Inschrijving voor macOS-apparaten instellen
titleSuffix: Microsoft Intune
description: Meer informatie over hoe u de inschrijving voor iOS-apparaten in Intune instelt.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/12/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 46429114-2e26-4ba7-aa21-b2b1a5643e01
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1de1b015daad50837142ce9628543f0b2d7587d7
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093749"
---
# <a name="set-up-enrollment-for-macos-devices-in-intune"></a>Inschrijving voor macOS-apparaten instellen in Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Met Intune kunt u macOS-apparaten beheren om gebruikers toegang te geven tot zakelijke e-mail en apps.

Als Intune-beheerder kunt u inschrijving instellen voor bedrijfseigen macOS-apparaten en macOS-apparaten in privé-eigendom (Bring-Your-Own-Device of BYOD). 

## <a name="prerequisites"></a>Vereisten

Voer de volgende vereisten uit voordat u inschrijving van macOS-apparaten instelt:

- [Zorg ervoor dat uw apparaat in aanmerking komt voor apparaatinschrijving bij Apple](https://support.apple.com/en-us/HT204142#eligibility).
- [Domeinen configureren](../fundamentals/custom-domain-name-configure.md)
- [MDM-instantie instellen](../fundamentals/mdm-authority-set.md)
- [Groepen maken](../fundamentals/groups-add.md)
- [De bedrijfsportal configureren](../apps/company-portal-app.md)
- Gebruikerslicenties toewijzen in het [Microsoft 365-beheercentrum](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Een Apple MDM-pushcertificaat ophalen](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="user-owned-macos-devices-byod"></a>macOS-apparaten die het eigendom van gebruikers zijn (BYOD)

U kunt gebruikers hun eigen persoonlijke apparaten laten registreren in Intune-beheer. Dit staat bekend als 'Bring Your Own Device' of BYOD. Nadat u aan de vereisten hebt voldaan en gebruikerslicenties hebt toegewezen, kunnen de gebruikers hun apparaten als volgt inschrijven:
- door naar de [bedrijfsportalwebsite](https://portal.manage.microsoft.com) te gaan; of
- door de Mac-bedrijfsportal-app te downloaden via [aka.ms/EnrollMyMac](https://aka.ms/EnrollMyMac).

U kunt uw gebruikers ook een koppeling sturen naar de stappen voor online registratie: [Uw Mac OS-apparaat registreren in Intune](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp).

Zie de volgende artikelen voor meer informatie over andere taken voor eindgebruikers:

- [Bronnen over de eindgebruikerservaring in Microsoft Intune](../fundamentals/end-user-educate.md)
- [Uw macOS-apparaat gebruiken met Intune](../user-help/enroll-your-device-in-intune-macos-cp.md)

## <a name="company-owned-macos-devices"></a>Bedrijfseigen macOS-apparaten
Voor organisaties die apparaten voor hun gebruikers aanschaffen, ondersteunt Intune de volgende inschrijvingsmethoden voor macOS-apparaten die bedrijfseigendom zijn:
- [Automatische apparaatinschrijving (Automated Device Enrollment of ADE) van Apple](device-enrollment-program-enroll-macos.md): Organisaties kunnen macOS-apparaten aanschaffen via ADE. Met ADE kunt u een inschrijvingsprofiel draadloos implementeren om apparaten voor beheer in te schrijven.
- [Apparaatinschrijvingsmanager (DEM)](device-enrollment-manager-enroll.md): U kunt een DEM-account gebruiken om maximaal duizend apparaten te registreren.

## <a name="block-macos-enrollment"></a>macOS-inschrijving blokkeren
Standaard kunt u met Intune macOS-apparaten registreren. Zie [Beperkingen voor apparaattypen instellen](enrollment-restrictions-set.md) als u de inschrijving van macOS-apparaten wilt blokkeren.

## <a name="enroll-virtual-macos-machines-for-testing"></a>Virtuele macOS-machines inschrijven voor testen

> [!NOTE]
> Virtuele macOS-machines worden alleen ondersteund voor het testen. Gebruik geen virtuele macOS-machines als productieapparaten voor uw eindgebruikers. 

U kunt virtuele macOS-machines inschrijven voor het testen met ofwel Parallels Desktop of VMware Fusion. 

Voor Parallels Desktop moet u het hardwaretype en het serienummer voor de virtuele machines instellen zodat deze kunnen worden herkend door Intune. Volg de instructies van Parallels voor het instellen van het hardwaretype en [serienummer](http://kb.parallels.com/123455) om de vereiste instellingen voor het testen op te geven. U wordt aangeraden het hardwaretype van het apparaat waarop de virtuele machines worden uitgevoerd, af te stemmen op het hardwaretype van de virtuele machines die u maakt. U vindt dit hardwaretype in **Apple-menu** > **Over deze Mac** > **Systeeminformatie** > **Modelnaam**. 

Voor VMware Fusion moet u [het VMX-bestand bewerken](https://kb.vmware.com/s/article/1014782) om het hardwaremodel en serienummer van de virtuele machine in te stellen. U wordt aangeraden het hardwaretype van het apparaat waarop de virtuele machines worden uitgevoerd, af te stemmen op het hardwaretype van de virtuele machines die u maakt. U vindt dit hardwaretype in **Apple-menu** > **Over deze Mac** > **Systeeminformatie** > **Modelnaam**. 

## <a name="user-approved-enrollment"></a>Door de gebruiker goedgekeurde inschrijving

Door de gebruiker goedgekeurde MDM-inschrijving is een type macOS-inschrijving die u kunt gebruiken om bepaalde vertrouwelijke instellingen te beheren. Zie de [ondersteuningsdocumentatie van Apple](https://support.apple.com/HT208019) voor meer informatie.  
 
Vanaf 2020 juni worden alle nieuwe macOS MDM-inschrijvingen in Intune, inclusief inschrijvingen die niet worden uitgevoerd via automatische apparaatregistratie (ADE), beschouwd als zijnde door de gebruiker goedgekeurd. De eindgebruiker moet het beheerprofiel handmatig installeren in **Systeemvoorkeuren** > **Profielen** en zo goedkeuring van het beheerprofiel bieden. Systeemvoorkeuren wordt automatisch gestart vanuit de Bedrijfsportal-app voor BYOD macOS-gebruikers. [Instructies voor het installeren van het beheerprofiel](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp) zijn beschikbaar in de bedrijfsportal-app.     

BYOD macOS MDM-inschrijvingen voorafgaand aan juni 2020 kunnen niet door de gebruiker worden goedgekeurd als de eindgebruiker niet handmatig goedkeuring van het beheerprofiel heeft gegeven in **Systeemvoorkeuren** > **Profielen**. Voor BYOD-inschrijvingen na juni 2020 start de Bedrijfsportal-app **Systeemvoorkeuren** voor de gebruiker en moet de gebruiker Installeren selecteren. Als de gebruiker het beheerprofiel niet heeft goedgekeurd tijdens de registratie, kan de gebruiker naar **Systeemvoorkeuren** > **Profielen** gaan, het beheerprofiel kiezen en **Goedkeuren** selecteren om het profiel later goed te keuren.

### <a name="find-out-if-a-device-is-user-approved"></a>Nagaan of een apparaat 'Goedgekeurd door de gebruiker' is
1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Kies **Apparaten** > **Alle apparaten** > kies het apparaat > **Hardware**.
3. Schakel het veld **Door gebruiker goedgekeurde registratie** in.


## <a name="next-steps"></a>Volgende stappen

Nadat macOS-apparaten zijn geregistreerd, kunt u [aangepaste instellingen voor macOS-apparaten maken](../configuration/custom-settings-macos.md).

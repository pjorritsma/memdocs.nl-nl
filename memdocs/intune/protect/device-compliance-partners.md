---
title: Nalevingspartners voor apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Gebruik een externe apparaatnalevingspartner als bron van nalevingsgegevens voor apparaten die u met Intune beheert.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/17/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe6a46c10f55378292e57548494852c4014c062a
ms.sourcegitcommit: 21b6c0c054e5371f32d611a2411ccd166b0e03bc
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643700"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>Ondersteuning voor apparaatnalevingspartners in Intune

Microsoft Intune kan nalevingsstatusgegevens toevoegen aan Azure Active Directory (Azure AD) voor de apparaten die u beheert met een of meer apparaatnalevingspartners. Met deze configuratie kunnen nalevingsgegevens van die apparaten worden gebruikt met uw beleid voor voorwaardelijke toegang.

Intune is standaard ingesteld als MDM-instantie (Mobile Device Management) voor uw apparaten. Wanneer u een nalevingspartner toevoegt aan Azure AD en Intune, configureert u die partner als bron van de MDM-instantie (Mobile Device Management) voor de apparaten die u aan die partner toewijst via een Azure AD-gebruikersgroep.

Voer de volgende taken uit om het gebruik van gegevens van apparaatnalevingspartners in te schakelen:

1. **Configureer Intune voor gebruik met de apparaatnalevingspartner** en configureer groepen gebruikers waarvan de apparaten door die nalevingspartner worden beheerd.

2. **Configureer uw nalevingspartner om gegevens te verzenden naar Intune**.

3. **Schrijf uw iOS- of Android-apparaten in bij die apparaatnalevingspartner**.

Wanneer deze taken zijn voltooid, verzendt de apparaatnalevingspartner de details van de apparaatstatus naar Intune. Intune voegt deze gegevens toe aan Azure AD. Voor apparaten die bijvoorbeeld de status niet-conform hebben, wordt deze status toegevoegd aan hun apparaatgegevens in Azure AD.

De nalevingsstatus wordt vervolgens geëvalueerd aan de hand van het beleid voor voorwaardelijke toegang, net zoals de nalevingsstatusgegevens voor apparaten die door Intune worden beheerd.  Intune is standaard een geregistreerde nalevingspartner voor iOS en Android. Wanneer u extra partners toevoegt, kunt u de volgorde van prioriteit instellen om ervoor te zorgen dat de juiste partner het apparaat beheert, zodat het aan uw bedrijfsbehoeften voldoet.

## <a name="supported-device-compliance-partners"></a>Ondersteunde apparaatnalevingspartners

In openbare preview:

- VMware Workspace ONE UEM (voorheen AirWatch)

## <a name="prerequisites"></a>Vereisten

- Een abonnement op Microsoft Intune en toegang tot het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

- Een abonnement op de apparaatnalevingspartner.

- Raadpleeg de documentatie voor uw nalevingspartner voor ondersteunde platformen en aanvullende vereisten.

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>Intune configureren voor gebruik met een apparaatnalevingspartner

Schakel ondersteuning voor een apparaatnalevingspartner in als u de nalevingsstatusgegevens van die partner wilt gebruiken met uw beleid voor voorwaardelijke toegang.

### <a name="add-a-compliance-partner-to-intune"></a>Een nalevingspartner toevoegen aan Intune

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Ga naar **Tenantbeheer** > **Connectors en tokens** > **Partnernalevingsbeheer** > **Nalevingspartner toevoegen**.

   > [!div class="mx-imgBorder"]
   > ![Een apparaatnalevingspartner toevoegen](./media/device-compliance-partners/add-compliance-partner.png)

3. Vouw op de pagina **Basisprincipes** de vervolgkeuzelijst **Nalevingspartner** uit en selecteer de partner die u wilt toevoegen.

   - Als u VMware Workspace ONE wilt gebruiken als de nalevingspartner voor iOS- of Android-platforms, selecteert u **VMware Workspace ONE mobiele naleving**.

   Selecteer vervolgens de vervolgkeuzelijst voor **Platform**en selecteer het platform. macOS wordt niet ondersteund met deze preview.

   U bent beperkt tot één partner per platform, zelfs als u meerdere nalevingspartners aan Azure AD hebt toegevoegd.

4. Selecteer op **Toewijzingen** de gebruikersgroepen die apparaten hebben die door deze partner worden beheerd. Bij deze toewijzing wijzigt u de MDM-instantie voor toepasselijke apparaten voor gebruik van deze partner. Gebruikers met apparaten die door de partner worden beheerd, moeten ook een licentie voor Intune toegewezen krijgen.

5. Controleer uw selecties op de pagina **Beoordelen + maken** en selecteer **Maken** om deze configuratie te voltooien.

Uw configuratie wordt nu weergegeven op de pagina Partnernalevingsbeheer.

### <a name="modify-the-configuration-for-a-compliance-partner"></a>De configuratie voor een nalevingspartner wijzigen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Ga naar **Tenantbeheer** > **Connectors en tokens** > **Partnernalevingsbeheer** en selecteer de partnerconfiguratie die u wilt wijzigen. Configuraties worden gesorteerd op platformtype.

3. Selecteer op de partnerconfiguratiepagina **Overzicht** **Eigenschappen** om de pagina Eigenschappen te openen waar u de toewijzingen kunt bewerken.

4. Selecteer op de pagina **Eigenschappen** de optie **Bewerken** om de weergave Toewijzingen te openen, waar u de groepen kunt wijzigen die deze configuratie zullen gebruiken.

5. Selecteer **Beoordelen + opslaan** en **Opslaan** om uw wijzigingen op te slaan.

6. *Deze stap is alleen van toepassing wanneer u VMware Workspace ONE* gebruikt:

   Vanuit de Workspace ONE UEM-console moet u de wijzigingen die u hebt opgeslagen in het beheercentrum van Microsoft Endpoint Manager handmatig synchroniseren. Totdat u wijzigingen handmatig synchroniseert, is de Workspace ONE UEM niet op de hoogte van configuratiewijzigingen en kunnen gebruikers in nieuwe groepen die u hebt toegewezen de naleving niet rapporteren.

   Om handmatig te synchroniseren vanuit Azure-Services:
   1. Meld u aan bij uw VMware Workspace ONE UEM-console.
   2. Ga naar **Instellingen** > **Systeem** > **Enterprise Integration** > **Directory Services**.
   3. Klik voor *Azure-Services synchroniseren*op **Synchroniseren**.

      Alle wijzigingen die u hebt aangebracht sinds de eerste configuratie of de laatste handmatige synchronisatie, worden gesynchroniseerd vanuit Azure-Services naar UEM.  

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>Uw nalevingspartner configureren voor gebruik met Intune

Als u een apparaatnalevingspartner wilt inschakelen voor gebruik met Intune, moet u de configuraties die specifiek zijn voor die partner voltooien. Zie voor meer informatie over deze taak de documentatie voor de betreffende partner:

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>Schrijf uw iOS- of Android-apparaten in bij die apparaatnalevingspartner

Raadpleeg de documentatie van de apparaatnalevingspartners voor informatie over het inschrijven van apparaten bij die partner. Nadat apparaten nalevingsgegevens hebben geregistreerd en verzonden naar de partner, worden deze nalevingsgegevens doorgestuurd naar Intune en toegevoegd aan Azure AD.

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>Apparaten bewaken die worden beheerd door externe apparaatnalevingspartners

Nadat u externe apparaatnalevingspartners hebt geconfigureerd en apparaten bij hen hebt ingeschreven, worden de nalevingsgegevens door de partner doorgestuurd naar Intune. Nadat Intune die gegevens heeft ontvangen, kunt u informatie over de apparaten bekijken in de Azure Portal.

Meld u aan bij Azure Portal en ga naar **Azure AD** > **Apparaten** > [**Alle apparaten**](https://portal.azure.com/#blade/Microsoft_AAD_Devices/DevicesMenuBlade/Devices/menuId/).

## <a name="next-steps"></a>Volgende stappen

Gebruik de documentatie van uw externe partner om het nalevingsbeleid voor apparaten te maken.

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)

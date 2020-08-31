---
title: Beleid voor voorwaardelijke toegang tot Exchange maken
titleSuffix: Microsoft Intune
description: Configureer voorwaardelijke toegang voor Exchange On-Premises en oudere Exchange Online Dedicated in Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 127dafcb-3f30-4745-a561-f62c9f095907
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 19a2d82f23abef49f193859c46a17cbb44a61f49
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663341"
---
# <a name="configure-exchange-on-premises-access-for-intune"></a>Toegang tot Exchange On-Premises voor Intune configureren

In dit artikel leest u hoe u de voorwaardelijke toegang voor Exchange On-Premises configureert op basis van apparaatnaleving.

Als u een Exchange Online Dedicated-omgeving hebt en wilt weten of deze de nieuwe of oudere configuratie heeft, neem dan contact op met uw accountmanager. Als u de toegang tot e-mail op Exchange On-Premises of de oude zelfstandige Exchange Online-omgeving wilt beheren, configureer dan beleid voor voorwaardelijke toegang tot Exchange On-premises in Intune.

> [!IMPORTANT]
> De informatie in dit artikel is van toepassing op klanten die worden ondersteund voor het gebruik van een Exchange-connector.
>
> Vanaf juli 2020 wordt de ondersteuning voor de Exchange connector afgeschaft en vervangen door Exchange [HMA](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) (Hybrid Modern Authentication, hybride moderne verificatie).  Als u een Exchange-connector hebt ingesteld in uw omgeving, blijft de Intune-tenant ondersteund voor het gebruik ervan en houdt u toegang tot de gebruikersinterface die de configuratie ervan ondersteunt. U kunt de connector blijven gebruiken of HMA configureren en vervolgens de connector verwijderen.
>
> U hebt Intune niet nodig om via HMA de Exchange-connector in te stellen en te gebruiken. Met deze wijziging wordt de gebruikersinterface voor het configureren en beheren van de Exchange-connector voor Intune verwijderd uit het Microsoft Endpoint Manager-beheercentrum, tenzij u al een Exchange-connector gebruikt met uw abonnement.

## <a name="before-you-begin"></a>Voordat u begint

Controleer of aan de volgende voorwaarden is voldaan voordat u voorwaardelijke toegang configureert:

- Uw versie van Exchange is **Exchange 2010 SP3 of hoger**. De CAS-matrix (Client Access Server) voor Exchange-servers wordt ondersteund.

- U hebt de [on-premises Exchange-connector Exchange ActiveSync](exchange-connector-install.md), die Intune verbindt met Exchange On-Premises, geïnstalleerd en in gebruik.

    >[!IMPORTANT]  
    >Intune ondersteunt meerdere on-premises Exchange-connectors per abonnement.  Elke Exchange On-Premises-connector is uitsluitend bestemd voor één Intune-tenant en mag niet worden gebruikt met een andere tenant.  Als u meer dan één on-premises Exchange-organisatie hebt, kunt u voor elke Exchange-organisatie een afzonderlijke connector instellen.

- De connector voor een on-premises Exchange-organisatie kan op elke machine worden geïnstalleerd, zolang die machine maar kan communiceren met de Exchange-server.

- De connector ondersteunt de **Exchange CAS-omgeving**. InTune biedt ondersteuning voor het rechtstreeks installeren van de connector op de Exchange CAS-server. U wordt aangeraden deze op een andere computer te installeren vanwege de extra belasting die de connector voor de server betekent. Wanneer u de connector configureert, moet u deze zodanig instellen dat deze communiceert met een van de Exchange CAS-servers.

- **Exchange ActiveSync** kan worden geconfigureerd met verificatie op basis van certificaten of door het invoeren van gebruikersreferenties.

- Wanneer beleid voor voorwaardelijke toegang wordt geconfigureerd en een gebruiker deel uitmaakt van de doelgroep voor het beleid, moet het volgende met het **apparaat** zijn gedaan voordat een gebruiker verbinding kan maken met zijn e-mail:
  - Het apparaat moet zijn **ingeschreven** bij Intune of lid zijn van een domein.
  - Het apparaat moet zijn **geregistreerd bij Azure Active Directory**. Bovendien moet de client-id van Exchange ActiveSync zijn geregistreerd bij Azure Active Directory.

- De Azure AD Device Registration Service (DRS) wordt automatisch geactiveerd voor Intune- en Office 365-klanten. Klanten die de ADFS Device Registration Service al hebben geïmplementeerd, zien geen geregistreerde apparaten in hun on-premises Active Directory. **Dit geldt niet voor Windows-pc's en -apparaten**.

- Het apparaat moet **compatibel** zijn met alle soorten nalevingsbeleid die worden geïmplementeerd op het apparaat.

- Als het apparaat niet aan de instellingen voor voorwaardelijke toegang voldoet, krijgt de gebruiker een van de volgende berichten te zien wanneer deze zich aanmeldt:
  - Als het apparaat niet is geregistreerd bij Intune of niet is geregistreerd bij Azure Active Directory, verschijnt er een bericht met instructies over het installeren van de bedrijfsportal-app, het registreren van het apparaat en het activeren van e-mail. Dit proces zorgt er ook voor dat de Exchange ActiveSync-id van het apparaat wordt gekoppeld aan de apparaatrecord in Azure Active Directory.
  - Als het apparaat niet aan het beleid voldoet, wordt er een bericht weergegeven waarin de gebruiker naar de website van de Intune-bedrijfsportal of de bedrijfsportal-app wordt verwezen. In de bedrijfsportal staat informatie over het probleem en hoe het kan worden opgelost.

### <a name="support-for-mobile-devices"></a>Ondersteuning voor mobiele apparaten

- **Systeemeigen e-mailapp op iOS/iPadOS**: zie [Beleid voor voorwaardelijke toegang maken](../protect/create-conditional-access-intune.md) om een beleid voor voorwaardelijke toegang te maken
- **EAS-mailclients zoals Gmail op Android 4 of hoger**: zie [Beleid voor voorwaardelijke toegang maken](../protect/create-conditional-access-intune.md) om een beleid voor voorwaardelijke toegang te maken

- **EAS-mailclients op Android-apparaatbeheerder**: zie [Beleid voor voorwaardelijke toegang maken](../protect/create-conditional-access-intune.md) om een beleid voor voorwaardelijke toegang te maken

- **EAS-mailclients op apparaten met een Android-werkprofiel**: alleen *Gmail* en *Nine Work for Android Enterprise* worden ondersteund op apparaten met een Android-werkprofiel. Voorwaardelijke toegang werkt alleen in combinatie met Android-werkprofielen als u een e-mailprofiel voor de app *Gmail* of *Nine Work for Android Enterprise* implementeert en die apps ook implementeert als verplicht te installeren apps. Nadat u de app hebt geïmplementeerd, kunt u voorwaardelijke toegang op basis van het apparaat instellen.

#### <a name="to-set-up-conditional-access-for-android-work-profile-devices"></a>Voorwaardelijke toegang instellen voor apparaten met een Android-werkprofiel

  1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
  
  2. Implementeer de Gmail- of Nine Work-app wanneer dat **Vereist** is.

  3. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken** en voer een **Naam** en **Beschrijving** in voor het profiel.

  4. Selecteer **Android Enterprise** bij **Platform** en selecteer **E-mail** bij **Profieltype**.

  5. Configureer de [instellingen van het e-mailprofiel](https://docs.microsoft.com/intune/configuration/email-settings-android-enterprise#android-enterprise).

  6. Wanneer u klaar bent, selecteert u **OK** > **Maken** om uw wijzigingen op te slaan.

  7. Nadat u het e-mailprofiel hebt gemaakt, moet u deze [toewijzen aan groepen](https://docs.microsoft.com/intune/device-profile-assign).

  8. Stel [Voorwaardelijke toegang op basis van het apparaat](https://docs.microsoft.com/intune/protect/conditional-access-intune-common-ways-use#device-based-conditional-access) in.

> [!NOTE]
> Microsoft Outlook voor Android en iOS/iPadOS wordt niet ondersteund via de on-premises Exchange-connector. Als u wilt gebruikmaken van Azure Active Directory-beleid voor voorwaardelijke toegang en beleid voor Intune-app-beveiliging met Outlook voor iOS/iPadOS en Android voor uw on-premises postvakken, raadpleegt u [Hybride moderne verificatie gebruiken met Outlook voor iOS/iPadOS en Android](https://docs.microsoft.com/Exchange/clients/outlook-for-ios-and-android/use-hybrid-modern-auth).

### <a name="support-for-pcs"></a>Ondersteuning voor pc's

De native **Mail**-toepassing voor Windows 8.1 en hoger (indien ingeschreven in MDM bij Intune)

## <a name="configure-exchange-on-premises-access"></a>Toegang tot Exchange On-Premises configureren

Voordat u de volgende procedure kunt gebruiken om Toegangsbeheer van Exchange On-premises in te stellen, moet u ten minste één [Intune-connector voor Exchange On-premises](exchange-connector-install.md) installeren en configureren.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Ga naar **Tenantbeheer** > **Exchange-toegang** en selecteer vervolgens **On-premises toegang tot Exchange**.

3. Kies **Ja** in het deelvenster **On-premises toegang tot Exchange** om *on-premises toegang tot Exchange in te schakelen*.

   > [!div class="mx-imgBorder"]
   > ![Voorbeeldschermopname van het scherm voor on-premises toegang tot Exchange](./media/conditional-access-exchange-create/exchange-on-premises-access.png)

4. Onder **Toewijzing** kiest u **Groepen selecteren om op te nemen**. Vervolgens selecteert u een of meer groepen om de toegang te configureren.

   Op leden van de groepen die u selecteert, wordt het beleid voor voorwaardelijke toegang tot Exchange On-premises toegepast. Gebruikers die dit beleid ontvangen, moeten hun apparaten inschrijven bij Intune en voldoen aan de nalevingsprofielen voordat ze toegang tot Exchange On-premises kunnen krijgen.

   > [!div class="mx-imgBorder"]
   > ![Groepen selecteren die moeten worden opgenomen](./media/conditional-access-exchange-create/select-groups.png)

5. Als u groepen wilt uitsluiten, kiest u **Groepen voor uitsluiten selecteren** en selecteert u vervolgens een of meer groepen die u wilt vrijstellen van apparaatregistratie en de nalevingsprofielen voor toegang tot Exchange On-premises.

   Selecteer **Opslaan** om uw configuratie op te slaan en terug te keren naar het deelvenster **Exchange-toegang**.

6. Configureer vervolgens de instellingen voor de Intune on-premises Exchange-connector. Selecteer in de console **Tenantbeheer** > **Exchange-toegang**> **On-premises Exchange ActiveSync-connector** en selecteer vervolgens de connector voor de Exchange-organisatie die u wilt configureren.

7. Selecteer voor **Gebruikersmeldingen** de optie **Bewerken** om de werkstroom **Organisatie bewerken** te openen, waar u het bericht *Gebruikersmelding* kunt aanpassen.

   > [!div class="mx-imgBorder"]
   > ![Voorbeeldschermopname van de werkstroom Organisatie bewerken voor meldingen](./media/conditional-access-exchange-create/edit-organization-user-notification.png)

   Wijzig het standaard-e-mailbericht dat wordt verzonden naar gebruikers als hun apparaat niet compatibel is en ze toegang willen krijgen tot on-premises Exchange. Voor de berichtsjabloon wordt Markup Language gebruikt. Tijdens het typen ziet u een voorbeeld van het bericht

   Selecteer **Beoordelen en opslaan** en vervolgens **Opslaan** om uw wijzigingen op te slaan en de configuratie voor toegang tot on-premises Exchange te voltooien.

   > [!TIP]
   > Zie dit Wikipedia-[artikel](https://en.wikipedia.org/wiki/Markup_language) voor meer informatie over Markup Language.

8. Selecteer vervolgens **Geavanceerde toegangsinstellingen voor Exchange ActiveSync** om de werkstroom *Geavanceerde toegangsinstellingen voor Exchange ActiveSync* te openen. Hierin configureert u regels voor apparaattoegang.

   > [!div class="mx-imgBorder"]
   > ![Voorbeeldschermopname van de werkstroom Organisatie bewerken voor geavanceerde instellingen](./media/conditional-access-exchange-create/edit-organization-advanced-settings.png)

   - Stel voor **Toegang tot onbeheerde apparaten** de globale standaardregel in voor toegang van apparaten die niet worden beïnvloed door voorwaardelijke toegang of andere regels:

     - **Toegang toestaan**: alle apparaten krijgen direct toegang tot Exchange On-Premises. Apparaten van de gebruikers in groepen die u hebt geconfigureerd als opgenomen in de vorige procedure, worden geblokkeerd als later wordt vastgesteld dat ze niet aan het nalevingsbeleid voldoen of niet zijn ingeschreven in Intune.

     - **Toegang blokkeren** en **Quarantaine**: wanneer u de toegang blokkeert, wordt de toegang van alle apparaten tot Exchange On-Premises in eerste instantie geblokkeerd. Apparaten van gebruikers in de groepen die u hebt geconfigureerd als opgenomen in de vorige procedure, krijgen toegang nadat de apparaten zijn ingeschreven in Intune en als compatibel zijn beoordeeld.

       Android-apparaten waarop Samsung Knox Standard *niet* wordt uitgevoerd, worden altijd geblokkeerd omdat deze instelling niet wordt ondersteund op deze apparaten.

   - Voor **Uitzonderingen van apparaatplatform** selecteert u **Toevoegen** en geeft u waar nodig details voor uw omgeving op.

      Als de instelling **Toegang tot onbeheerde apparaten** is ingesteld op **Geblokkeerd**, kunnen apparaten die zijn ingeschreven en compatibel zijn ook toegang krijgen, zelfs als er een platformuitzondering van toepassing is waardoor de apparaten worden geblokkeerd.  

9. Selecteer **OK** om de gewijzigde instellingen op te slaan.

10. Selecteer **Beoordelen en opslaan** en vervolgens **Opslaan** om het beleid voor voorwaardelijke toegang tot Exchange op te slaan.

## <a name="next-steps"></a>Volgende stappen

Vervolgens maakt u een nalevingsbeleid en wijst u dit toe aan de gebruikers zodat Intune hun mobiele apparaten kan evalueren. Zie [Aan de slag met apparaatcompatibiliteit](device-compliance-get-started.md).

[Problemen met de Intune On-premises Exchange-connector in Microsoft Intune oplossen](https://support.microsoft.com/help/4471887)

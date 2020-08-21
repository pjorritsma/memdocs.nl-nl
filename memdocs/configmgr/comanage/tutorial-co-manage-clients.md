---
title: Zelf studie&#58; co-beheer in te scha kelen voor bestaande clients
titleSuffix: Configuration Manager
description: Configureer co-beheer met Microsoft Intune wanneer u Windows 10-apparaten al beheert met Configuration Manager.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc05ae5a9be6c437fab60f8c4c5a45d61e8c3e65
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694879"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Zelf studie: co-beheer inschakelen voor bestaande Configuration Manager-clients

Met co-beheer kunt u uw goed opgezette processen voor het gebruik van Configuration Manager voor het beheren van Pc's in uw organisatie. Terzelfder tijd bevestt u in de Cloud door intune te gebruiken voor beveiliging en moderne inrichting.  

In deze zelf studie stelt u het co-beheer in van uw Windows 10-apparaten die al zijn Inge schreven bij Configuration Manager. Deze zelf studie begint met de locatie die u al gebruikt Configuration Manager voor het beheren van uw Windows 10-apparaten.

Gebruik deze zelf studie wanneer:  

- U hebt een on-premises Active Directory waarmee u verbinding kunt maken met Azure Active Directory (Azure AD) in een hybride Azure AD-configuratie.

  Als u geen Hybrid Azure Active Directory (AD) kunt implementeren die uw on-premises AD met Azure AD verbindt, kunt u het beste de volgende aanvullende zelf studie [gebruiken om co-beheer in te scha kelen voor nieuwe Windows 10-apparaten die zijn gebaseerd op Internet](tutorial-co-manage-new-devices.md).
- U hebt bestaande Configuration Manager-clients die u wilt koppelen aan de Cloud.

**In deze zelf studie doet u het volgende:**  
> [!div class="checklist"]
> * Controleer de vereisten voor Azure en uw on-premises omgeving
> * Hybride Azure AD instellen  
> * Configuration Manager-client agenten configureren om te registreren bij Azure AD  
> * InTune configureren voor het automatisch inschrijven van apparaten  
> * Co-beheer inschakelen in Configuration Manager  

## <a name="prerequisites"></a>Vereisten  

### <a name="azure-services-and-environment"></a>Azure-Services en-omgeving

- Azure-abonnement ([gratis proef versie](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune-abonnement
  > [!TIP]  
  > Een Enterprise Mobility + Security EMS-abonnement omvat zowel Azure Active Directory Premium als Microsoft Intune. EMS-abonnement ([gratis proef versie](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Als deze nog niet aanwezig is in uw omgeving, kunt u tijdens deze zelf studie het volgende doen:

- Configureer [Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-install-select-installation) tussen uw on-premises Active Directory en uw Azure Active Directory (AD)-Tenant.

> [!TIP]
> U hoeft geen afzonderlijke intune-of EMS-licenties meer aan uw gebruikers te kopen en toe te wijzen. Zie [Veelgestelde vragen over producten en licenties](../core/understand/product-and-licensing-faq.md#bkmk_mem)voor meer informatie.

### <a name="on-premises-infrastructure"></a>Lokale infrastructuur

- Een [ondersteunde versie](../core/servers/manage/updates.md#supported-versions) van Configuration Manager current branch
- De Mobile Device Management-instantie (MDM) moet zijn ingesteld op intune.  

### <a name="permissions"></a>Machtigingen

In deze zelf studie gebruikt u de volgende machtigingen om taken uit te voeren:

- Een account dat een *domein beheerder* is in uw on-premises infra structuur  
- Een account dat een *volledige beheerder* is voor *alle* bereiken in Configuration Manager
- Een account dat een *globale beheerder* is in azure Active Directory (Azure AD)
   - Zorg ervoor dat u een intune-licentie hebt toegewezen aan het account dat u gebruikt om u aan te melden bij uw Tenant. Als dat niet het geval is, mislukt de fout melding ' de gebruiker wordt niet herkend '. <!--mem issue 169-->

## <a name="set-up-hybrid-azure-ad"></a>Hybride Azure AD instellen

Bij het instellen van een hybride Azure AD moet u de integratie van een on-premises AD met Azure AD instellen met behulp van Azure AD Connect en Active Directory Federated Services (ADFS). Met succes volle configuratie kunnen uw werk nemers zich probleemloos aanmelden bij externe systemen met behulp van hun on-premises AD-referenties.

> [!IMPORTANT]  
> In deze zelf studie wordt een proces voor bare bones beschreven voor het instellen van hybride Azure AD voor een beheerd domein. We raden u aan om vertrouwd te raken met het proces en niet te vertrouwen op deze zelf studie als uw gids voor het leren en implementeren van hybride Azure AD.
>
> Voor meer informatie over hybride Azure AD begint u met de volgende artikelen in de Azure Active Directory-documentatie:
>
> - [Uw implementatie van Azure AD-deelname plannen](/azure/active-directory/devices/azureadjoin-plan)
> - [Uw implementatie van hybride Azure AD-deelname plannen](/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [De hybride Azure AD-deelname van uw apparaten beheren](/azure/active-directory/devices/hybrid-azuread-join-control)
> - [Hybride Azure AD-deelname configureren voor federatieve domeinen](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>Azure AD Connect instellen

Hybride Azure AD vereist configuratie van Azure AD Connect om computer accounts in uw on-premises Active Directory (AD) en het apparaatobject in azure AD in de synchronisatie te blijven gebruiken.

Vanaf versie 1.1.819.0 bevat Azure AD Connect een wizard om hybride Azure AD-koppeling te configureren. Het gebruik van die wizard vereenvoudigt het configuratie proces.  

Als u Azure AD Connect wilt configureren, hebt u referenties nodig van een globale beheerder voor Azure AD.  

> [!TIP]  
> De volgende procedure mag niet worden beschouwd als gezaghebbend voor het instellen van Azure AD Connect, maar deze wordt hier beschreven om het configureren van co-beheer tussen intune en Configuration Manager te stroom lijnen. Zie [Configure Hybrid Azure AD join's for Managed domains](/azure/active-directory/devices/hybrid-azuread-join-managed-domains) in de Azure AD-documentatie voor de gezaghebbende inhoud op deze en gerelateerde procedures voor het instellen van Azure AD.  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Een hybride Azure AD-deelname configureren met Azure AD Connect

1. Down load en installeer de [nieuwste versie van Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 of hoger).  
2. Start Azure AD Connect en selecteer vervolgens **configureren**.
3. Selecteer op de pagina **Extra taken** de optie **Apparaatopties configureren** en selecteer **Volgende**.
4. Selecteer **Volgende** op de pagina **Overzicht**.
5. Op de pagina **verbinding maken met Azure AD** voert u de referenties in van een globale beheerder voor Azure AD.
6. Selecteer op de pagina **Apparaatopties** de optie **Hybride Azure AD-koppeling configureren** en selecteer **Volgende**.
7. Selecteer op de pagina **besturings systemen** voor apparaten de besturings systemen die door apparaten in uw Active Directory omgeving worden gebruikt en selecteer vervolgens **volgende**.  

   U kunt de optie selecteren voor de ondersteuning van Windows-apparaten die lid zijn van een domein, maar u moet er wel voor zorgen dat gezamenlijk beheer van apparaten alleen wordt ondersteund voor Windows 10.
8. Voer de volgende stappen uit op de **SCP** -pagina voor elk on-premises forest dat Azure AD Connect het SCP (Service Connection Point) wilt configureren, en selecteer vervolgens **volgende**:  
   1. Selecteer de forest.  
   2. Selecteer de verificatieservice.  Als u een federatief domein hebt, selecteert u AD FS server, tenzij uw organisatie uitsluitend Windows 10-clients heeft en u de synchronisatie van computer/apparaat hebt geconfigureerd of als uw organisatie gebruikmaakt van [SeamlessSSO](/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Klik op **Toevoegen** om de referenties van een ondernemingsbeheerder in te voeren.  
9. Als u een beheerd domein hebt, slaat u deze stap over.  

   Voer op de pagina **Federatieconfiguratie** de referenties van uw AD FS-beheerder in en selecteer **Volgende**.
10. Selecteer op de pagina **Gereed om te configureren** op **Configureren**.
11. Selecteer de pagina **Configuratie voltooid** op **Afsluiten**.

Als u problemen ondervindt met het volt ooien van hybride Azure AD join voor Windows-apparaten die lid zijn van een domein, raadpleegt u [problemen oplossen hybride Azure AD join voor Windows huidige apparaten](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>Client instellingen configureren om clients te laten registreren bij Azure AD

Gebruik client instellingen om Configuration Manager-clients zodanig te configureren dat deze automatisch worden geregistreerd bij Azure AD.  

1. Open de **Configuration Manager-console**  >  **beheer**  >  **overzicht**  >  **client instellingen**en bewerk vervolgens de **standaard client instellingen**.  

2. Selecteer **Cloud Services**.  

3. Stel op de pagina **standaard instellingen** **automatisch nieuwe Windows 10-domein apparaten in die zijn toegevoegd aan Azure Active Directory** in = **Ja**.  

4. Selecteer **OK** om deze configuratie op te slaan.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>De automatische inschrijving van apparaten met intune configureren

Vervolgens stellen we de automatische inschrijving van apparaten in met intune. Met automatische inschrijving worden apparaten die u beheert met Configuration Manager automatisch Inge schreven bij intune.

Met automatische inschrijving kunnen gebruikers hun Windows 10-apparaten inschrijven bij intune. Apparaten worden inge schreven wanneer een gebruiker hun werk account toevoegt aan hun persoonlijk apparaat of wanneer een apparaat in bedrijfs eigendom is gekoppeld aan Azure Active Directory.  

1. Meld u aan bij de [Azure Portal](https://portal.azure.com/) en selecteer **Azure Active Directory**  >  Mobility-Microsoft intune **(MDM en mam)**  >  **Microsoft Intune**.  

2. **MDM-gebruikers bereik**configureren. Geef een van de volgende opties op om te configureren welke apparaten van gebruikers worden beheerd door Microsoft Intune en accepteer de standaard waarden voor de URL-waarden.  

   - **Sommige**: Selecteer de **groepen** die automatisch hun Windows 10-apparaten kunnen inschrijven  

   - **Alle**: alle gebruikers kunnen automatisch hun Windows 10-apparaten inschrijven

   - **Geen**: automatische inschrijving voor MDM uitschakelen

   > [!IMPORTANT]  
   > Als zowel **Gebruikersbereik van MAM** als automatische MDM-inschrijving (**Gebruikersbereik van MDM**) wordt ingeschakeld voor een groep, wordt alleen MAM ingeschakeld. Alleen Mobile Application Management (MAM) wordt toegevoegd aan gebruikers in die groep wanneer deze werk plek lid worden van een persoonlijk apparaat. Apparaten zijn niet automatisch MDM-registratie.  

3. Selecteer **Opslaan** om de configuratie van automatische inschrijving te volt ooien.  

4. Ga terug naar **mobiliteit (MDM en mam)** en selecteer vervolgens **Microsoft intune registratie**.  

    > [!NOTE]
    > Sommige tenants hebben mogelijk niet de volgende opties om te configureren.<!-- SCCMDocs#1230 -->
    >
    > **Microsoft intune** is het configureren van de MDM-app voor Azure AD. **Microsoft intune-inschrijving** is een specifieke Azure AD-app die wordt gemaakt wanneer u multi-factor Authentication-beleid toepast voor IOS-en Android-registratie. Zie [multi-factor Authentication vereisen voor inschrijvingen van intune-apparaten](/intune/enrollment/multi-factor-authentication)voor meer informatie.

5. Voor MDM-gebruikers bereik selecteert u **alle**en vervolgens **Opslaan**.  

## <a name="enable-co-management-in-configuration-manager"></a>Co-beheer inschakelen in Configuration Manager

Met hybride Azure AD-configuratie en Configuration Manager-client configuraties, bent u klaar om de switch te spie gelen en co-beheer van uw Windows 10-apparaten mogelijk te maken.  

> [!TIP]
> - Als u co-beheer inschakelt, wijst u een verzameling toe als een *test groep*. Dit is een groep die een klein aantal clients bevat om uw configuraties voor co-beheer te testen. We raden u aan een geschikte verzameling te maken voordat u de procedure start. Vervolgens kunt u die verzameling selecteren zonder de procedure te verlaten.
> - Vanaf Configuration Manager versie 1906 hebt u mogelijk meerdere verzamelingen nodig omdat u voor elke werk belasting een andere *test groep* kunt toewijzen.

### <a name="enable-co-management-starting-in-version-1906"></a>Co-beheer inschakelen vanaf versie 1906

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Co-beheer inschakelen in versie 1902 en lager

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>Volgende stappen

- Bekijk de status van gezamenlijk beheerde apparaten met het [dash board voor co-beheer](how-to-monitor.md)
- Beginnen met het ophalen van [onmiddellijke waarde](quickstarts.md#immediate-value) van co-beheer
- [Voorwaardelijke toegang](quickstart-conditional-access.md) en intune-nalevings regels gebruiken voor het beheren van de gebruikers toegang tot bedrijfs resources
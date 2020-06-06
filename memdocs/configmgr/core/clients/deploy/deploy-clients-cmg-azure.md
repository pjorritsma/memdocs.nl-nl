---
title: De-client installeren met Azure AD
titleSuffix: Configuration Manager
description: De Configuration Manager-client op Windows 10-apparaten installeren en toewijzen met behulp van Azure Active Directory voor verificatie
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 39d6bf22cb24492a0f4e3f59313184ce522b5d09
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455001"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Configuration Manager Windows 10-clients installeren en toewijzen met behulp van Azure AD voor verificatie

Als u de Configuration Manager-client op Windows 10-apparaten wilt installeren met behulp van Azure AD-verificatie, integreert u Configuration Manager met Azure Active Directory (Azure AD). Clients kunnen zich op het intranet bevindt, rechtstreeks communiceren met een HTTPS-beheer punt of een beheer punt in een site die is ingeschakeld voor verbeterde HTTP. Ze kunnen ook communiceren via internet via de CMG of met een beheer punt op internet. Dit proces maakt gebruik van Azure AD om clients te verifiëren op de Configuration Manager-site. Azure AD vervangt de nood zaak voor het configureren en gebruiken van certificaten voor client verificatie.

Het instellen van Azure AD kan voor sommige klanten eenvoudiger zijn dan het instellen van een open bare-sleutel infrastructuur voor verificatie op basis van certificaten. Er zijn functies waarvoor u de site naar Azure AD moet voorbereiden, maar waarvoor de clients geen lid hoeven te zijn van Azure AD.<!-- SCCMDocs issue 1259 --> Raadpleeg voor meer informatie de volgende artikelen:

- [Azure Active Directory plannen](../../plan-design/security/plan-for-security.md#bkmk_planazuread)
- [Azure AD gebruiken voor co-beheer](../../../comanage/quickstart-hybrid-aad.md)

## <a name="before-you-begin"></a>Voordat u begint

- Een Azure AD-Tenant is een vereiste  

- Apparaat vereisten:  

  - Windows 10  

  - Toegevoegd aan Azure AD, ofwel zuivere Cloud domein lid of hybride Azure AD-lid  

- Gebruikers vereisten:  

  - De aangemelde gebruiker moet een Azure AD-identiteit zijn.

  - Als de gebruiker een federatieve of gesynchroniseerde identiteit is, configureert u zowel Configuration Manager [Active Directory gebruikers detectie](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) als [Azure AD-gebruikers detectie](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc). Zie [een strategie voor het implementeren van een hybride identiteit definiëren](https://docs.microsoft.com/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-identity-adoption-strategy)voor meer informatie over hybride identiteiten.<!--497750-->

- Naast de [bestaande vereisten](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012MPpreq) voor de site systeemrol van het beheer punt, schakelt u ook **ASP.net 4,5** in op deze server. Andere opties bevatten die automatisch worden geselecteerd bij het inschakelen van ASP.NET 4,5.  

- Bepaal of het beheer punt HTTPS vereist. Zie [beheer punt voor HTTPS inschakelen](../manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)voor meer informatie.  

- Stel eventueel een CMG ( [Cloud Management Gateway](../manage/cmg/plan-cloud-management-gateway.md) ) in voor het implementeren van clients op internet. Voor on-premises clients die worden geverifieerd met Azure AD, hebt u geen CMG nodig.  

> [!TIP]
> Vanaf versie 2002,<!--5686290--> Configuration Manager breidt de ondersteuning uit voor apparaten op Internet die niet vaak verbinding maken met het interne netwerk, geen lid kunnen worden van Azure Active Directory (Azure AD) en geen methode hebben om een door PKI uitgegeven certificaat te installeren. Zie [verificatie op basis van tokens voor CMG](deploy-clients-cmg-token.md)voor meer informatie.

## <a name="configure-azure-services-for-cloud-management"></a>Azure-Services configureren voor Cloud beheer

Verbind uw Configuration Manager-site als de eerste stap met Azure AD. Zie [Azure-Services configureren](../../servers/deploy/configure/azure-services-wizard.md)voor meer informatie over dit proces. Maak een verbinding met de **Cloud beheer** service.

Schakel [Azure AD-gebruikers detectie](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc) in als onderdeel van onboarding voor **Cloud beheer**.

Nadat u deze acties hebt voltooid, is uw Configuration Manager-site verbonden met Azure AD.

## <a name="configure-client-settings"></a>Clientinstellingen configureren

Met deze client instellingen kunt u Windows 10-apparaten configureren voor Hybrid-join. Ze kunnen ook clients op internet in staat stellen het CMG-en Cloud distributiepunt te gebruiken.

1. Configureer de volgende client instellingen in de groep **Cloud Services** . Zie [client instellingen configureren](configure-client-settings.md)voor meer informatie.

    - **Toegang tot Cloud distributiepunt toestaan**: Schakel deze instelling in om op internet apparaten te helpen de vereiste inhoud op te halen om de Configuration Manager-client te installeren. Als de inhoud niet beschikbaar is op het Cloud distributiepunt, kunnen apparaten de inhoud ophalen uit de CMG. Met de Boots trap van de client installatie wordt een nieuwe poging gedaan om het Cloud distributiepunt voor vier uur voordat het terugvalt op de CMG.<!--495533-->  

    - **Nieuwe Windows 10-apparaten die lid zijn van een domein automatisch registreren bij Azure Active Directory**: ingesteld op **Ja** of **Nee**. De standaard instelling is **Ja**. Dit is ook de standaard instelling in Windows 10, versie 1709.

        > [!TIP]
        > Hybride apparaten zijn gekoppeld aan een on-premises Active Directory domein en zijn geregistreerd bij Azure AD. Zie voor meer informatie [Hybrid Azure AD joined devices](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid)(Engelstalig).<!-- MEMDocs#325 -->

    - **Clients inschakelen om een Cloud beheer gateway te gebruiken**: ingesteld op **Ja** (standaard) of **Nee**.  

2. Implementeer de client instellingen op de vereiste verzameling apparaten. Implementeer deze instellingen niet voor gebruikers verzamelingen.

Om te bevestigen dat het apparaat is toegevoegd aan een Hybrid join, voert u `dsregcmd.exe /status` uit vanaf een opdracht prompt. Als het apparaat is toegevoegd aan Azure AD of een hybride lid is, wordt **Ja**weer gegeven in het veld **AzureAdjoined** in de resultaten. Zie [dsregcmd Command-Apparaatstatus](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-device-dsregcmd)voor meer informatie.

## <a name="install-and-register-the-client-using-azure-ad-identity"></a>De client installeren en registreren met Azure AD-identiteit

Als u de-client hand matig wilt installeren met behulp van Azure AD-identiteit, raadpleegt u eerst het algemene proces voor het [hand matig installeren van clients](deploy-clients-to-windows-computers.md#BKMK_Manual).

> [!Note]  
> Het apparaat moet toegang hebben tot het internet om contact op te nemen met Azure AD, maar dit is niet nodig op internet.

In het volgende voor beeld ziet u de algemene structuur van de opdracht regel:`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Zie [Eigenschappen van client installatie](about-client-installation-properties.md)voor meer informatie.

De para meter **/MP** en de eigenschap **CCMHOSTNAME** geven een van de volgende op, afhankelijk van het scenario:

- On-premises beheer punt. Geef alleen de para meter **/MP** op. De eigenschap **CCMHOSTNAME** is niet vereist.
- Cloudbeheergateway
-  Beheerpunt op internet

De eigenschap **SMSMP** geeft het on-premises beheer punt op. Het is niet vereist. Het wordt aanbevolen voor apparaten die lid zijn van Azure AD die zwerven op het intranet, zodat ze een on-premises beheer punt kunnen vinden.

In dit voor beeld wordt een Cloud beheer gateway gebruikt. De voorbeeld waarden worden vervangen:`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

De site publiceert extra Azure AD-gegevens naar de Cloud beheer gateway (CMG). Een client die lid is van Azure AD, haalt deze informatie op uit de CMG tijdens het ccmsetup-proces, waarbij dezelfde Tenant wordt gebruikt waaraan deze is gekoppeld. Dit gedrag vereenvoudigt het installeren van de client in een omgeving met meer dan één Azure AD-Tenant. De enige twee vereiste ccmsetup-eigenschappen zijn **CCMHOSTNAME** en **SMSSiteCode**.<!--3607731-->

Zie op [Internet gebaseerde apparaten voorbereiden voor co-beheer](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)om de client installatie te automatiseren met behulp van de Azure AD-identiteit via Microsoft intune.

## <a name="next-steps"></a>Volgende stappen

Zodra het proces is voltooid, kunt u door gaan met het [bewaken en beheren van clients](../manage/monitor-clients.md).

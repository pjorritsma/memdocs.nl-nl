---
title: Azure AD gebruiken voor co-beheer
titleSuffix: Configuration Manager
description: Met Azure AD kunt u profiteren van verbeterde productiviteit voor uw gebruikers en beveiliging voor uw resources, zowel in de Cloud als on-premises omgevingen
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c757632e96eb9bdaca829d4a19e5e156fcf52577
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694981"
---
# <a name="use-azure-ad-for-co-management"></a>Azure AD gebruiken voor co-beheer

In de Cloud is identiteit het nieuwe besturings element. Met Azure Active Directory (Azure AD) kunt u uw gebruikers, apparaten en toepassingen koppelen in zowel de Cloud als on-premises omgevingen. Door uw apparaten te registreren bij Azure AD, kunt u de productiviteit van uw gebruikers en de beveiliging van uw resources verbeteren. Het gebruik van apparaten in azure AD vormt de basis voor zowel beheer als op apparaten gebaseerde voorwaardelijke toegang.

Zie [How to: Managed devices voor Cloud app Access with Conditional Access](/azure/active-directory/conditional-access/require-managed-devices) (Engelstalig) voor meer informatie over voorwaardelijke toegang op basis van apparaten.

In de volgende video is Senior Program Manager Sandeep Deo en product marketing manager Adam-haven voor het bespreken en demo van Azure AD voor co-beheer:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD biedt twee opties voor apparaten die eigendom zijn van het bedrijf, afhankelijk van de behoeften van uw organisatie:  

- Aan **Azure AD toegevoegd apparaat**: uw Windows 10-apparaten toevoegen aan Azure AD zonder dat u deze hoeft te koppelen aan uw on-premises Active Directory  

  - Ondersteunt Windows 10

  - Instellen zonder dat er aanvullende configuratie is vereist voor uw on-premises omgevingen  

  - Door een paar instellingen in azure AD in te scha kelen, kunt u uw gebruikers in staat stellen om apparaten te koppelen aan Azure AD via de Windows Setup-ervaring (OOBE)  

  - Zie [How to: uw Azure AD-deelname-implementatie plannen](/azure/active-directory/devices/azureadjoin-plan) voor meer informatie.  

- **Hybride Azure AD-apparaat**: uw bestaande aan het domein gekoppelde apparaten koppelen aan Azure AD  

  - Ondersteunt Windows 10, Windows 8,1 en Windows 7

  - Instellen met behulp van AD FS claims of Azure AD Connect  

  - Voor Windows 10 wordt de samen voeging uitgevoerd in de context van de computer, zodat gebruikers geen extra stappen hoeven uit te voeren  

  - Zie [de implementatie van hybride Azure Active Directory-deelname plannen](/azure/active-directory/devices/hybrid-azuread-join-plan) voor meer informatie  

Beide opties bieden een vergelijk bare functionaliteit voor gebruikers. U kunt kiezen uit een van de mogelijkheden op basis van uw behoeften. U kunt bijvoorbeeld [toegang krijgen tot uw on-premises resources](/azure/active-directory/devices/azuread-join-sso) vanaf computers die lid zijn van Azure AD, zelfs als ze niet zijn gekoppeld aan Active Directory.

U kunt apparaten toevoegen aan Azure AD in verschillende omgevingen, ongeacht uw [verificatie methode](/azure/active-directory/hybrid/choose-ad-authn). Bijvoorbeeld Federated Authentication of Cloud authenticatie.

Als u al een on-premises Active Directory hebt, is het instellen van een van beide opties eenvoudig.

## <a name="benefits"></a>Voordelen

Het toevoegen van apparaten aan Azure AD biedt de volgende voor delen voor uw organisatie:

### <a name="single-sign-on-to-cloud-resources"></a>Eenmalige aanmelding bij cloud resources

Op apparaten die zijn gekoppeld aan Azure AD, beschikt u over een geïntegreerde ervaring om toegang te krijgen tot alle Cloud-en on-premises resources. Nadat u zich hebt aangemeld bij een Windows-machine die is gekoppeld aan Azure AD, kunt u eenmalige aanmelding voor alle toepassingen zonder extra aanmeldings prompts.  

### <a name="windows-hello-for-business"></a>Windows Hello voor Bedrijven

Windows hello voor bedrijven biedt een sterk wacht woord-minder verificatie voor Windows 10. Als u uw apparaten aan Azure AD koppelt, kunt u Windows hello voor bedrijven in uw gebruikers database inschakelen voor zowel de Cloud als on-premises resources. Windows hello voor bedrijven elimineert het probleem van het onthouden van complexe wacht woorden of het onbedoeld weer geven hiervan. Het aanmeldings proces is eenvoudig en veilig.

Zie [Windows hello voor bedrijven](/windows/security/identity-protection/hello-for-business/hello-identity-verification)voor meer informatie.  

### <a name="device-based-conditional-access"></a>Voorwaardelijke toegang op basis van het apparaat

Schakel voorwaardelijke toegang in op basis van de status van het apparaat om de gegevens van uw organisatie beter te beveiligen. Voor voorwaardelijke toegang op basis van een apparaat is een beheerd apparaat vereist. Dit apparaat moet een compatibel apparaat of een hybride Azure AD-apparaat zijn. Voor apparaten die lid zijn van Azure AD moet intune het apparaat markeren als compatibel. Voor hybride apparaten die lid zijn van Azure AD, wordt de apparaatstatus zelf gebruikt om voorwaardelijke toegang te evalueren. Co-beheer biedt u een extra voor deel van de evaluatie van de naleving via intune voor hybride apparaten die deel uitmaken van Azure AD. Deze functie zorgt ervoor dat de apparaatconfiguratie intact is.

Zie [How to: Managed devices voor Cloud app Access with Conditional Access](/azure/active-directory/conditional-access/require-managed-devices)(Engelstalig) voor meer informatie over voorwaardelijke toegang op basis van apparaten.  

### <a name="automatic-device-licensing"></a>Automatische apparaat-licentie verlening

Alle Windows 10-apparaten die zijn gekoppeld aan Azure AD, gaan via licentie controles. Met deze controles kunt u ze automatisch upgraden van Pro naar Enter prise via de micro soft-Cloud. Wanneer u het relevante abonnement van de gebruiker verwijdert, downgradet het apparaat de licentie automatisch. Deze functie biedt één deel venster voor het beheren van Windows-licenties, zonder ingewikkelde processen of on-premises systemen.

### <a name="self-service-functionality"></a>Selfservice functionaliteit

Selfservice functionaliteit omvat self-service voor wachtwoord herstel en BitLocker-herstel sleutel. Azure AD biedt u ook directe opties om uw wacht woord opnieuw in te stellen of BitLocker-herstel sleutels te openen. U kunt Azure AD gebruiken om uw wacht woord rechtstreeks opnieuw in te stellen vanuit het Windows-vergrendelings scherm, in plaats van vanuit een webbrowser. Deze functies verminderen wrijving voor gebruikers en helpen bij het knippen van de helpdesk kosten voor uw organisatie.  

Zie voor meer informatie [zelf studie: gebruikers in staat stellen hun account te ontgrendelen of wacht woorden opnieuw in te stellen met Azure Active Directory selfservice voor het opnieuw instellen van wacht](/azure/active-directory/authentication/tutorial-enable-sspr)woorden.

### <a name="enterprise-state-roaming"></a>Enter prise State roaming

Alle apparaten die aan Azure AD zijn gekoppeld, kunnen hun instellingen synchroniseren met de Cloud. Elk apparaat waarop een gebruiker zich aanmeldt, synchroniseert al hun instellingen voor een productievere ervaring.  

## <a name="value-proposition"></a>Toegevoegde waarde

Door uw apparaten via een van beide methoden te koppelen aan Azure AD wordt uw digitale trans formatie versneld. Het biedt meer functionaliteit van Microsoft 365. U hebt betere ervaringen en u hebt meer beveiliging voor uw gegevens.

Azure AD biedt verschillende opties om de werk belasting te vereenvoudigen, bijvoorbeeld:

- Alle apparaat-id's in uw organisatie vanaf één plek beheren  

- Verlaag de kosten van uw Help Desk door selfservice voor wacht woord opnieuw instellen in te scha kelen. Vervolgens kunnen gebruikers uw wacht woord op elk gewenst moment opnieuw instellen op het vergrendelings scherm van Windows 10 op het apparaat.  

## <a name="configure"></a>Configureren

Als u al een on-premises Active Directory-omgeving hebt en u wilt deel nemen aan uw apparaten die aan het domein zijn toegevoegd aan Azure AD, configureert u hybride apparaten die deel uitmaken van Azure AD. Voor meer informatie kunt u [het volgende doen: uw hybride Azure Active Directory deelname-implementatie plannen](/azure/active-directory/devices/hybrid-azuread-join-plan).

Configuration Manager heeft een client instelling om [automatisch nieuwe Windows 10-apparaten die lid zijn van een domein te registreren bij Azure AD](../core/clients/deploy/about-client-settings.md#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Zie [client instellingen configureren](../core/clients/deploy/configure-client-settings.md)voor meer informatie over het configureren van client instellingen.

Als u Azure AD-join wilt configureren voor uw apparaten zonder ze ook toe te voegen aan uw on-premises domein, raadpleegt u de overwegingen voor Azure AD-join in uw omgeving. Zodra u hebt besloten om te gaan met Azure AD-deelname, hebt u veel opties om deze te implementeren op basis van de behoeften van uw organisatie. Raadpleeg voor meer informatie de volgende artikelen:

- [Procedure: uw Azure AD-koppelings implementatie plannen](/azure/active-directory/devices/azureadjoin-plan)  
- [Inzicht in uw inrichtings opties](/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)
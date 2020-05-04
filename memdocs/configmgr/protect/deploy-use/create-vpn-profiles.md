---
title: VPN-profielen maken
titleSuffix: Configuration Manager
description: Meer informatie over het maken van VPN-profielen in Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713595"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>VPN-profielen maken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager ondersteunt meerdere VPN-verbindings typen. Zie [VPN-profielen](vpn-profiles.md)voor meer informatie over de beschik bare verbindings typen voor de verschillende platformen.

Voor VPN-verbindingen van derden distribueert u de VPN-app voordat u het VPN-profiel implementeert. Als u de app niet implementeert, wordt gebruikers gevraagd om dit te doen wanneer ze verbinding proberen te maken met het VPN. Zie [toepassingen implementeren](../../apps/deploy-use/deploy-applications.md)voor meer informatie.

## <a name="create-a-vpn-profile"></a>Een VPN-profiel maken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit, vouw **toegang tot bedrijfs bronnen**uit en selecteer het knoop punt **VPN-profielen** .

1. Klik op het tabblad **Start** van het lint in de groep **maken** op **VPN-profiel maken**.

1. Geef op de pagina **Algemeen** van de wizard VPN-profiel maken de volgende informatie op:

    - **Naam**: Voer een unieke naam in om het VPN-profiel in de-console te identificeren.

        > [!NOTE]
        > Gebruik niet de volgende tekens in de naam van het VPN `\/:*?<>|; `-profiel:. Het Windows VPN-profiel ondersteunt deze speciale tekens niet.

    - **Beschrijving**: Voer eventueel een beschrijving in om meer informatie over het VPN-profiel op te geven.

    - **VPN-profiel type**: Selecteer het juiste platform.

        Als u het **Windows 8,1** -platform selecteert, kunt u ook **importeren uit een bestand**. Met deze actie worden VPN-profiel gegevens uit een XML-bestand geïmporteerd. Als u deze optie selecteert, vereenvoudigt de rest van de wizard de volgende pagina's: **ondersteunde platforms** en **import VPN-profiel**.

1. Selecteer op de pagina **ondersteunde platforms** de versies van het besturings systeem die dit VPN-profiel ondersteunt.

1. Geef op de pagina **verbinding** de volgende informatie op:

    - **Verbindings type**: Kies het type VPN-verbinding. Zie [VPN-profielen](vpn-profiles.md)voor meer informatie over de ondersteunde typen.

    - **Server lijst**: Voeg een nieuwe server toe om te gebruiken voor de VPN-verbinding. Afhankelijk van het verbindings type, kunt u een of meer VPN-servers toevoegen en opgeven welke server de standaard instelling is.

    - **VPN overs Laan bij verbinding met bedrijfs netwerk**: Configureer clients niet om de VPN te gebruiken wanneer ze zich in het interne netwerk bevinden. Geef indien nodig een verbindingsspecifieke DNS-naam op.

1. Kies op de pagina **verificatie methode** van de wizard een methode die wordt ondersteund door het verbindings type. De instellingen en de beschik bare opties op deze pagina variëren afhankelijk van het geselecteerde verbindings type. Zie [referentie voor verificatie methoden](#bkmk_auth)voor meer informatie.

1. Als uw VPN gebruikmaakt van een proxy server, selecteert u op de pagina **proxy-instellingen** een van de opties die geschikt zijn voor uw omgeving. Geef vervolgens de configuratie gegevens voor de proxy op.

1. De pagina **toepassingen** is alleen van toepassing op Windows 10-profielen. Voeg bureau blad-en universele apps toe die automatisch verbinding maken met deze VPN. Het type app bepaalt de App-ID:

    - Geef voor een *bureau blad-app*het bestandspad van de app op.

    - Voor een *universele app*geeft u de naam van het pakket familie (PFN) op. Zie [een familie naam van een pakket zoeken voor VPN per app](find-a-pfn-for-per-app-vpn.md)voor meer informatie over het vinden van de PFN voor een app.

    U kunt ook een optie configureren zodat **alleen de apps in de lijst deze VPN kunnen gebruiken**.

    > [!IMPORTANT]
    > Beveilig alle lijsten met gekoppelde apps die u wilt compileren voor het configureren van een VPN per app. Als een niet-gemachtigde gebruiker uw lijst wijzigt en u deze importeert in de lijst met VPN-apps per app, kunt u VPN-toegang verlenen aan apps die geen toegang mogen hebben.

1. De pagina **boundary's** is alleen van toepassing op Windows 10-profielen voor het configureren van VPN-grenzen. U kunt de volgende opties toevoegen:

    - **Regels voor netwerk verkeer**: Stel de protocollen, de lokale poort, de externe poort en de adresbereiken in die moeten worden ingeschakeld voor de VPN-verbinding.  

        > [!Note]
        > Als u geen regel voor netwerk verkeer maakt, worden alle protocollen, poorten en adresbereiken ingeschakeld. Nadat u een regel hebt gemaakt, worden alleen de protocollen, poorten en adresbereiken die u in die regel opgeeft of in aanvullende regels gebruikt door de VPN-verbinding.

    - **DNS-namen en-servers**: DNS-servers die worden gebruikt door de VPN-verbinding nadat het apparaat de verbinding tot stand heeft gebracht.

    - **Routes**: netwerk routes die gebruikmaken van de VPN-verbinding. Het maken van meer dan 60 routes kan ertoe leiden dat het beleid mislukt.

1. Voltooi de wizard.

Het nieuwe WPN-profiel wordt weergegeven in het knooppunt **VPN-profielen** van de werkruimte **Activa en naleving**.

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a>Naslag informatie voor verificatie methoden

Beschik bare VPN-verificatie methoden zijn afhankelijk van het verbindings type:

### <a name="certificates"></a>Certificaten

Als het client certificaat wordt geverifieerd bij een RADIUS-server, zoals een Network Policy Server, stelt u de alternatieve naam voor het onderwerp in het certificaat in op de UPN (User Principal Name).

Ondersteunde verbindings typen:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### <a name="username-and-password"></a>Gebruikersnaam en wachtwoord

Ondersteunde verbindings typen:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

Ondersteunde verbindings typen:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Door micro soft beveiligd EAP (PEAP

Ondersteunde verbindings typen:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Beveiligd Microsoft-wachtwoord (EAP-MSCHAP v2)

Ondersteunde verbindings typen:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>Smartcard of ander certificaat

Ondersteunde verbindings typen:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

Ondersteunde verbindings typen:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>Computercertificaten gebruiken

Ondersteunde verbindings typen:

- IKEv2

### <a name="additional-authentication-options"></a>Aanvullende verificatie opties

Wanneer de Windows-client versie dit ondersteunt, is de optie voor het **configureren** van de verificatie methode beschikbaar. Met deze optie wordt het venster Windows-Eigenschappen geopend om de verificatie methode te configureren.

Afhankelijk van de geselecteerde opties wordt u mogelijk gevraagd om meer informatie op te geven, bijvoorbeeld:

- **Onthoud de gebruikers referenties bij elke aanmelding**: gebruikers referenties worden onthouden zodat gebruikers ze niet telkens hoeven in te voeren wanneer ze verbinding maken.  

- **Selecteer een client certificaat voor client verificatie**: Selecteer een eerder gemaakt SCEP-certificaat profiel voor client om de VPN-verbinding te verifiëren. Zie [PFX-certificaat profielen maken](create-certificate-profiles.md)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

- Voor VPN-verbindingen van derden distribueert u de VPN-app voordat u het VPN-profiel implementeert. Als u de app niet implementeert, wordt gebruikers gevraagd om dit te doen wanneer ze verbinding proberen te maken met het VPN. Zie [toepassingen implementeren](../../apps/deploy-use/deploy-applications.md)voor meer informatie.

- Implementeer het VPN-profiel. Zie [profielen implementeren](deploy-wifi-vpn-email-cert-profiles.md)voor meer informatie.

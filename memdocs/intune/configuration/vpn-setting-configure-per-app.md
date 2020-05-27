---
title: VPN-instellingen per app instellen voor iOS/iPadOS-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk de voorwaarden, maak een groep voor VPN-gebruikers (Virtual Private Network), voeg een SCEP-certificaatprofiel toe, configureer VPN-profiel per app en wijs enkele apps toe aan het VPN-profiel in Microsoft Intune op iOS/iPadOS-apparaten. Vermeld ook de stappen om de VPN-verbinding op het apparaat te verifiëren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: D9958CBF-34BF-41C2-A86C-28F832F87C94
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24663f8338f03fab53369689b4a61b5bd1bec63f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83991213"
---
# <a name="set-up-per-app-virtual-private-network-vpn-for-iosipados-devices-in-intune"></a>VPN per app instellen voor iOS/iPadOS-apparaten in Intune

In Microsoft Intune kunt u VPN’s (virtuele privénetwerken) maken en gebruiken die aan een app zijn toegewezen. Deze functie wordt VPN per app genoemd. U kiest de beheerde apps die uw VPN kunnen gebruiken op apparaten die door Intune worden beheerd. Wanneer u VPN’s per app gebruikt, maken eindgebruikers automatisch verbinding via het VPN en krijgen zij toegang tot organisatieresources, zoals documenten.

Deze functie is van toepassing op:

- iOS 9 en nieuwer
- iPadOS 13.0 en hoger

Controleer de documentatie van uw VPN-provider om te zien of VPN per app door uw VPN wordt ondersteund.

In dit artikel leest u hoe u een VPN-profiel per app maakt en dit profiel aan uw apps toewijst. Maak aan de hand van deze stappen een naadloze VPN-ervaring per app voor uw eindgebruikers. Voor de meeste VPN’s die VPN per app ondersteunen zal de gebruiker een app openen en automatisch verbinding maken met het VPN.

Voor een aantal VPN’s is verificatie met een gebruikersnaam en een wachtwoord toegestaan bij een VPN per app. Dit betekent dat gebruikers een gebruikersnaam en wachtwoord moeten invoeren om verbinding met het VPN te maken.

> [!IMPORTANT]
> VPN per app wordt niet ondersteund voor IKEv2 VPN-profielen voor iOS/iPadOS.

## <a name="per-app-vpn-with-zscaler"></a>VPN per app met Zscaler

Voor verificatie kan Zscaler Private Access (ZPA) met Azure Active Directory (Azure AD) worden geïntegreerd. Wanneer u ZPA gebruikt, hebt u niet de profielen met een [vertrouwd certificaat](#create-a-trusted-certificate-profile) of met een [SCEP- of PKCS-certificaat](#create-a-scep-or-pkcs-certificate-profile) nodig (zie de beschrijving in dit artikel). Als u een profiel met een VPN per app hebt ingesteld voor Zscaler, wordt er niet automatisch verbinding gemaakt met ZPA als u een van de bijbehorende apps opent. In plaats daarvan moet de gebruiker zich eerst aanmelden bij de Zscaler-app. Daarna is toegang op afstand beperkt tot de bijbehorende apps.

## <a name="prerequisites-for-per-app-vpn"></a>Vereisten voor VPN per app

> [!IMPORTANT]
> Uw VPN-leverancier heeft wellicht andere vereisten voor VPN per app, zoals bepaalde hardware of -licentieverlening. Raadpleeg de documentatie en zorg ervoor dat u voldoet aan deze vereisten voordat u Per-App VPN in Intune instelt.

Ter bevestiging van de identiteit van de VPN-server legt deze het certificaat voor. Dit moet door het apparaat zonder prompt worden geaccepteerd. Als u wilt bevestigen dat het certificaat automatisch wordt goedgekeurd, moet u een vertrouwd certificaatprofiel maken dat het door de certificeringsinstantie (CA) uitgegeven basiscertificaat van de VPN-server bevat.

### <a name="export-the-certificate-and-add-the-ca"></a>Het certificaat exporteren en de CA toevoegen

1. Open de beheerconsole op de VPN-server.
2. Bevestig dat door de VPN-server verificatie op basis van certificaten wordt gebruikt. 
3. Exporteer het bestand met het vertrouwde basiscertificaat. Dit bestand heeft de extensie .CER. U voegt dit toe wanneer u een vertrouwd certificaatprofiel maakt.
4. Voeg de naam toe van de CA die het certificaat heeft uitgegeven voor verificatie bij de VPN-server.

    Als de CA die door het apparaat wordt voorgelegd, overeenkomt met een CA in de lijst met vertrouwde CA's op de VPN-server, wordt het apparaat door de VPN-server geverifieerd.

## <a name="create-a-group-for-your-vpn-users"></a>Een groep maken voor uw VPN-gebruikers

Maak of kies een bestaande groep in Azure Active Directory (Azure AD) voor de gebruikers of apparaten die VPN per app gebruiken. Zie [Groepen toevoegen om gebruikers en apparaten in te delen](../fundamentals/groups-add.md) om een nieuwe groep te maken.

## <a name="create-a-trusted-certificate-profile"></a>Een vertrouwd certificaatprofiel maken

Importeer het door de CA uitgegeven basiscertificaat van de VPN-server in een profiel dat in Intune is gemaakt. Op basis van het vertrouwde certificaatprofiel vertrouwt het iOS/iPadOS-apparaat automatisch de CA die door de VPN-server wordt voorgelegd.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: Selecteer **iOS/iPadOS**.
    - **Profiel**: Selecteer **Vertrouwd certificaat**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld **iOS/iPadOS VPN-profiel met een vertrouwd certificaat voor hele bedrijf**.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.
7. Selecteer in **Configuratie-instellingen** het mappictogram en blader naar het VPN-certificaat (.cer-bestand) dat u vanuit de VPN-beheerconsole hebt geëxporteerd.
8. Selecteer **Volgende**en ga door met het maken van uw profiel. Zie [Een VPN-profiel maken](vpn-settings-configure.md#create-the-profile) voor meer informatie.

    > [!div class="mx-imgBorder"]
    > ![Een vertrouwd certificaatprofiel voor iOS/iPadOS-apparaten in Microsoft Intune maken](./media/vpn-setting-configure-per-app/vpn-per-app-create-trusted-cert.png)

## <a name="create-a-scep-or-pkcs-certificate-profile"></a>Een SCEP- of PKCS-certificaatprofiel maken

Op basis van het vertrouwde certificaatprofiel vertrouwt het apparaat automatisch de VPN-server. Het SCEP- of PKCS-certificaat geeft referenties van de iOS/iPadOS-VPN-client door aan de VPN-server. Door het certificaat kan het apparaat op de achtergrond verifiëren zonder dat de gebruiker om een gebruikersnaam en wachtwoord wordt gevraagd. 

Lees een van de volgende artikelen om het clientverificatiecertificaat te configureren en toe te wijzen:

- [Infrastructuur configureren om SCEP te ondersteunen in Intune](../protect/certificates-scep-configure.md)
- [PKCS-certificaten configureren en beheren met Intune](../protect/certficates-pfx-configure.md)

Configureer het certificaat voor clientverificatie. U kunt clientverificatie rechtstreeks in SCEP-certificaatprofielen instellen (de lijst **Uitgebreide-sleutelgebruik** > **Clientverificatie**). Voor PKCS stelt u de clientverificatie in op het certificaatsjabloon in de certificeringsinstantie (CA).

> [!div class="mx-imgBorder"]
> ![Een SCEP-certificaatprofiel in Microsoft Intune maken, inclusief indeling onderwerpnaam, sleutelgebruik, uitgebreide-sleutelgebruik en meer](./media/vpn-setting-configure-per-app/vpn-per-app-create-scep-cert.png)

## <a name="create-a-per-app-vpn-profile"></a>Een profiel voor VPN per app maken

Het VPN-profiel bevat het SCEP- of PKCS-certificaat met de referenties van de client, de VPN-verbindingsgegevens en de VPN-vlag per app voor het inschakelen van VPN per app die wordt gebruikt door de iOS/iPadOS-toepassing.

1. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: Selecteer **iOS/iPadOS**.
    - **Profiel**: Selecteer **VPN**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het aangepaste profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld **iOS/iPadOS VPN-profiel voor apps voor hele bedrijf**.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Configureer in **Configuratie-instellingen** de volgende instellingen:

    - **Type verbinding**: Selecteer uw VPN-client-app.
    - **Basis-VPN**: Configureer uw instellingen. Onder [iOS/iPadOS VPN-instellingen](vpn-settings-ios.md) vindt u alle instellingen en de beschrijving daarvan. Wanneer u VPN per app gebruikt, moet u de volgende eigenschappen instellen:

      - **Verificatiemethode**: Selecteer **Certificaten**. 
      - **Verificatiecertificaat**: Selecteer een bestaand SCEP- of PKCS-certificaat > **OK**.
      - **Split tunneling**: Selecteer **Uitschakelen** om te forceren dat al het verkeer de VPN-tunnel gebruikt wanneer de VPN-verbinding actief is. 

      > [!div class="mx-imgBorder"]
      > ![In een VPN per app-profiel voert u een verbinding, een IP-adres of FQDN, een verificatiemethode en Split tunneling in Microsoft Intune in](./media/vpn-setting-configure-per-app/vpn-per-app-create-vpn-profile.png)

    Zie [iOS/iPadOS VPN-instellingen](vpn-settings-ios.md) voor informatie over de overige instellingen.

    - **Automatisch VPN** > **Het type automatisch VPN** > **VPN per app**

      > [!div class="mx-imgBorder"]
      > ![In Intune stelt u Automatisch VPN in op VPN per app in iOS/iPadOS-apparaten](./media/vpn-setting-configure-per-app/vpn-per-app-automatic.png)

7. Selecteer **Volgende**en ga door met het maken van uw profiel. Zie [Een VPN-profiel maken](vpn-settings-configure.md#create-the-profile) voor meer informatie.

## <a name="associate-an-app-with-the-vpn-profile"></a>Een app aan het VPN-profiel koppelen

Na het toevoegen van uw VPN-profiel moet u de app en de Azure AD-groep (Microsoft Azure Active Directory) aan het profiel koppelen.

1. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apps** > **Alle apps**.
2. Selecteer een app uit de lijst > **Eigenschappen** > **Toewijzingen** > **Groep toevoegen**.
3. Bij **Toewijzingstype** selecteert u **Vereist** of **Beschikbaar voor geregistreerde apparaten**.
4. Selecteer **Opgenomen groepen** > **Selecteer de groepen die u wilt opnemen** > Selecteer de groep [die u hebt gemaakt](#create-a-group-for-your-vpn-users) (in dit artikel) > **Selecteren**.
5. Bij **VPN's** selecteert u het VPN per app-profiel [dat u hebt gemaakt ](#create-a-per-app-vpn-profile) (in dit artikel).

    > [!div class="mx-imgBorder"]
    > ![Een app toewijzen aan het VPN per app-profiel in Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-app-to-vpn.png)

6. Selecteer **OK** > **Opslaan**.

Een koppeling tussen een app en een profiel wordt verwijderd wanneer het apparaat de volgende keer wordt ingecheckt als aan alle volgende voorwaarden wordt voldaan:

- De app is het doel van vereiste installatie.
- Zowel het profiel als de app zijn gericht op dezelfde groep.
- U kunt de configuratie van VPN per app verwijderen uit de app-toewijzing.

Een koppeling tussen een app en een profiel blijft bestaan totdat de gebruiker opnieuw installeren vanuit de bedrijfsportal aanvraagt als aan alle volgende voorwaarden is voldaan:

- De app is het doel van de intentie beschikbare installatie.
- Zowel het profiel als de app zijn gericht op dezelfde groep.
- De eindgebruiker heeft installatie van de app aangevraagd vanuit de bedrijfsportal. Hierdoor worden de app en het profiel op het apparaat geïnstalleerd.
- U kunt de configuratie van VPN per app verwijderen of wijzigen uit de app-toewijzing.

## <a name="verify-the-connection-on-the-iosipados-device"></a>De verbinding controleren op het iOS/iPadOS-apparaat

Wanneer uw VPN per app is geconfigureerd en aan uw app is gekoppeld, controleert u vanaf een apparaat of de verbinding werkt.

### <a name="before-you-attempt-to-connect"></a>Voordat u verbinding probeert te maken

- Zorg ervoor dat u alle hierboven genoemde beleidsregels implementeert naar dezelfde groep. Anders werkt de VPN per app-ervaring niet.
- Als u de Pulse Secure VPN-app of een aangepaste VPN-client-app gebruikt, kunt u ervoor kiezen om tunneling op app-niveau of pakketniveau te gebruiken. Stel de waarde **ProviderType** in op **app-proxy** voor tunneling op app-niveau of **pakkettunnel** voor tunneling op pakketniveau. Lees de documentatie van uw VPN-provider om te controleren of u de juiste waarde gebruikt.

### <a name="connect-using-the-per-app-vpn"></a>Verbinding maken via VPN per app

Controleer de zero-touch-ervaring door verbinding te maken zonder dat u de VPN-verbinding hoeft te selecteren of uw referenties hoeft te typen. De zero-touch-ervaring betekent:

- Het apparaat vraagt u niet of u de VPN-server wilt vertrouwen. Dat betekent dat de gebruiker het dialoogvenster **Dynamisch vertrouwen** niet ziet.
- De gebruiker hoeft geen aanmeldingsgegevens te typen.
- Het apparaat van de gebruiker wordt verbonden met het VPN wanneer de gebruiker een van de gekoppelde apps opent.

## <a name="next-steps"></a>Volgende stappen

- Raadpleeg [VPN-instellingen voor iOS/iPadOS-apparaten in Microsoft Intune](vpn-settings-ios.md) om iOS/iPadOS-instellingen te controleren.
- Zie [VPN-instellingen configureren in Microsoft Intune](vpn-settings-configure.md) voor meer informatie over VPN-instellingen en Intune.

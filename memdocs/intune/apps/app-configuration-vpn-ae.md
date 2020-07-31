---
title: Een VPN of VPN per app configureren voor Android Enterprise-apparaten in Microsoft Intune | Microsoft Docs
titleSuffix: Microsoft Intune
description: Een app-configuratiebeleid gebruiken om een VPN- of VPN per app-profiel toe te voegen of te maken voor Android Enterprise-apparaten in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e869ad933e86d9330dbb8d6a26b1886a71cee07
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262894"
---
# <a name="use-a-vpn-and-per-app-vpn-policy-on-android-enterprise-devices-in-microsoft-intune"></a>Een VPN- of VPN per app-beleid gebruiken op Android Enterprise-apparaten in Microsoft Intune

Met een virtueel particulier netwerk (VPN) kunnen gebruikers op afstand toegang tot bedrijfsbronnen krijgen, zoals vanuit huis, een hotel of café. In Microsoft Intune kunt u VPN-client-apps configureren op Android Enterprise-apparaten met behulp van een app-configuratiebeleid. Vervolgens implementeert u dit beleid met de bijbehorende VPN-configuratie op apparaten in uw organisatie.

U kunt ook VPN-beleid maken dat wordt gebruikt door specifieke apps. Deze functie wordt VPN per app genoemd. Wanneer de app actief is, kan deze verbinding maken met het VPN en toegang krijgen tot bronnen via het VPN. Wanneer de app niet actief is, wordt de VPN-verbinding niet gebruikt.

Deze functie is van toepassing op:

- Android Enterprise

U kunt het app-configuratiebeleid voor uw VPN-client-app op twee manieren maken:

- Configuration Designer
- JSON-gegevens

In dit artikel wordt beschreven hoe u een VPN- en VPN per app-configuratiebeleid kunt maken met behulp van beide opties.

> [!NOTE]
> Veel van de parameters voor de VPN-clientconfiguratie zijn vergelijkbaar. Maar elke app heeft zijn unieke sleutels en opties. Neem contact op met uw VPN-leverancier als u vragen hebt.

## <a name="before-you-begin"></a>Voordat u begint

- In Android wordt niet automatisch een VPN-clientverbinding geactiveerd wanneer een app wordt geopend. De VPN-verbinding moet handmatig worden gestart. U kunt ook [always-on-VPN](../configuration/vpn-settings-android-enterprise.md) gebruiken om de verbinding te starten.

- De volgende VPN-clients ondersteunen configuratiebeleidsregels voor Intune-apps:

  - Cisco AnyConnect
  - Citrix SSO
  - F5-toegang
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - SonicWall Mobile Connect

- Wanneer u het VPN-beleid in Intune maakt, selecteert u verschillende sleutels om te configureren. Deze sleutelnamen zijn afhankelijk van de verschillende VPN-client-apps. De sleutelnamen in uw omgeving kunnen dus afwijken van de voorbeelden in dit artikel.

- De Configuration Designer- en JSON-gegevens kunnen gebruikmaken van verificatie op basis van certificaten. Als voor VPN-verificatie clientcertificaten zijn vereist, moet u de certificaatprofielen maken voordat u het VPN-beleid maakt. Het configuratiebeleid voor de VPN-app gebruikt de waarden uit de certificaatprofielen.

  Apparaten met een Android Enterprise-werkprofiel bieden ondersteuning voor SCEP-en PKCS-certificaten. Volledig beheerde, toegewezen en in bedrijfseigendom zijnde apparaten met een Android Enterprise-werkprofiel bieden alleen ondersteuning voor SCEP-certificaten. Zie [Certificaten gebruiken voor verificatie](../protect/certificates-configure.md) in Microsoft Intune voor meer informatie.

## <a name="per-app-vpn-overview"></a>Overzicht van VPN per app

De basisstroom voor het maken en testen van VPN per app bestaat uit de volgende stappen:

1. Selecteer de VPN-clienttoepassing. In [Voordat u begint](#before-you-begin) (in dit artikel) worden de ondersteunde apps vermeld.
2. Haal de toepassingspakket-id's op van de apps die gebruik gaan maken van de VPN-verbinding. In [De id voor het app-pakket ophalen](#get-the-app-package-id) (in dit artikel) ziet u hoe u dit doet.
3. Als u certificaten gebruikt om de VPN-verbinding te verifiëren, maakt en implementeert u de certificaatprofielen voordat u het VPN-beleid implementeert. Zorg ervoor dat de certificaatprofielen goed zijn geïmplementeerd. Zie [Certificaten gebruiken voor verificatie](../protect/certificates-configure.md) in Microsoft Intune voor meer informatie.
4. Voeg de [VPN-clienttoepassing toe](apps-add-android-for-work.md) aan Intune en implementeer de app voor uw gebruikers en apparaten.
5. Het VPN-app-configuratiebeleid maken. Gebruik de app-pakket-id's en certificaatgegevens in het beleid.
6. Implementeer het nieuwe VPN-beleid.
7. Controleer of de VPN-client-app verbinding maakt met de VPN-server.
8. Wanneer de app actief is, controleert u of het verkeer van uw app via de VPN-verbinding verloopt.

## <a name="get-the-app-package-id"></a>De id voor het app-pakket ophalen

Haal de pakket-id op voor elke toepassing die het VPN gaat gebruiken. Voor openbaar beschikbare toepassingen kunt u de app-pakket-id ophalen in de Google Play Store. De weergegeven URL voor elke toepassing bevat de pakket-id.

In het volgende voorbeeld is de pakket-id van de Microsoft Edge-browser-app `com.microsoft.emmx`. De pakket-id maakt deel uit van de URL:

:::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png" alt-text="Haal de app-pakket-id in de URL op in Google Play Store.":::

Voor Line-of-Business-apps (LOB) haalt u de pakket-id op bij de leverancier of ontwikkelaar of toepassing.

## <a name="certificates"></a>Certificaten

In dit artikel wordt ervan uitgegaan dat uw VPN-verbinding gebruikmaakt van verificatie op basis van certificaten. Ook wordt ervan uitgegaan dat u alle certificaten in de keten die nodig zijn voor het verifiëren van clients hebt geïmplementeerd. Deze certificaatketen bevat normaal gesproken het clientcertificaat, eventuele tussenliggende certificaten en het basiscertificaat.

Zie [Certificaten gebruiken voor verificatie in Microsoft Intune](../protect/certificates-configure.md) voor meer informatie over certificaten.

Wanneer uw certificaatprofiel voor clientverificatie wordt geïmplementeerd, maakt het een certificaattoken in het certificaatprofiel. Dit token wordt gebruikt om het configuratiebeleid voor de VPN-app te maken.

Als u niet bekend bent met het maken van app-configuratieprofielen, raadpleegt u [App-configuratiebeleidsregels toevoegen voor beheerde Android Enterprise-apparaten](app-configuration-policies-use-android.md).

## <a name="use-the-configuration-designer"></a>De Configuration Designer gebruiken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **App-configuratiebeleid** > **Toevoegen** > **Beheerde apparaten**.
3. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **App-configuratiebeleid: Cisco AnyConnect VPN-beleid voor apparaten met een Android Enterprise-werkprofiel**.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.
    - **Platform**: Selecteer **Android Enterprise**.
    - **Profieltype**: Uw opties zijn:
      - **Alle profieltypen**: Deze optie biedt ondersteuning voor verificatie op basis van gebruikersnaam en wachtwoord. Gebruik deze optie niet als u verificatie op basis van certificaten gebruikt.
      - **Alleen volledig beheerde en toegewezen werkprofielen in bedrijfseigendom**: Deze optie biedt ondersteuning voor verificatie op basis van certificaten en verificatie op basis van gebruikersnaam en wachtwoord.
      - **Alleen werkprofiel**: Deze optie biedt ondersteuning voor verificatie op basis van certificaten en verificatie op basis van gebruikersnaam en wachtwoord.
    - **Beoogde app**: Selecteer de VPN-client-app die u eerder hebt toegevoegd. In het volgende voorbeeld wordt de Cisco AnyConnect VPN-client-app gebruikt:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png" alt-text="Een app-configuratiebeleid maken om VPN of VPN per app in Microsoft Intune te configureren":::

4. Selecteer **Volgende**.
5. Voer in **Instellingen** de volgende eigenschappen in:

    - **Indeling van de configuratie-instellingen**: Selecteer **Configuration Designer gebruiken**:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png" alt-text="Een configuratiebeleid voor VPN-apps maken in Microsoft Intune met Configuration Designer.":::

    - **Toevoegen**: Hiermee wordt de lijst met configuratiesleutels weergegeven. Selecteer alle configuratiesleutels die nodig zijn voor uw configuratie > **OK**.

      In het volgende voorbeeld gebruiken we een minimale lijst voor AnyConnect VPN, inclusief verificatie op basis van certificaten en VPN per app:
  
      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" alt-text="Configuratiesleutels toevoegen aan een configuratiebeleid voor VPN-apps maken in Microsoft Intune met Configuration Designer - voorbeeld.":::

    - **Configuratiewaarde**: Voer de waarden in voor de configuratiesleutels die u hebt geselecteerd. Houd er rekening mee dat de sleutelnamen afhankelijk zijn van de VPN-client-app die u gebruikt. In de geselecteerde sleutels in het voorbeeld:

      - **Toegestane apps voor VPN per app**: Voer de toepassingspakket-id('s) in die u eerder hebt verzameld. Bijvoorbeeld:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png" alt-text="De toegestane app-pakket-id’s invoeren voor een configuratiebeleid voor VPN-apps in Microsoft Intune met Configuration Designer - voorbeeld.":::

      - **Certificaatalias voor sleutelhanger** (optioneel): Wijzig het **Waardetype** van **tekenreeks** in **certificaat**. Selecteer het clientcertificaatprofiel dat u wilt gebruiken met VPN-verificatie. Bijvoorbeeld:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png" alt-text="De certificaatalias voor de sleutelhanger wijzigen in een configuratiebeleid voor VPN-apps in Microsoft Intune met Configuration Designer - voorbeeld.":::

      - **Protocol**: Selecteer het **SSL**- of **IPsec**-tunnelprotocol van de VPN-verbinding.
      - **Verbindingsnaam**: Voer een beschrijvende naam voor de VPN-verbinding in. Gebruikers zien deze verbindingsnaam op hun apparaat. Voer bijvoorbeeld `ContosoVPN` in.
      - **Host**: Voer de hostnaam-URL naar de head-endrouter in. Voer bijvoorbeeld `vpn.contoso.com` in.

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png" alt-text="Voorbeelden van protocol, verbindingsnaam en hostnaam in een configuratiebeleid voor VPN-apps in Microsoft Intune met Configuration Designer":::

6. Selecteer **Volgende**.
7. Selecteer in **Toewijzingen** de groepen waaraan u het configuratiebeleid voor VPN-apps wilt toewijzen.

    Selecteer **Volgende**.

8. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken** selecteert, worden uw wijzigingen opgeslagen en wordt het beleid geïmplementeerd in uw groepen. Het beleid wordt ook weergegeven in de lijst met app-configuratiebeleid.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png" alt-text="Het app-configuratiebeleid controleren met behulp van de Configuration Designer-stroom in Microsoft Intune - voorbeeld.":::

## <a name="use-json"></a>JSON gebruiken

Gebruik deze optie als u niet beschikt over alle vereiste VPN-instellingen die in **Configuration Designer** worden gebruikt of deze niet weet. Neem voor hulp contact op met de leverancier van uw VPN.

### <a name="get-the-certificate-token"></a>Het certificaattoken ophalen

In deze stappen maakt u een tijdelijk beleid. Het beleid wordt niet opgeslagen. Het doel is om het certificaattoken te kopiëren. U gebruikt dit token bij het maken van het VPN-beleid met behulp van JSON (volgende sectie).

1. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apps** > **App-configuratiebeleid** > **Toevoegen** > **Beheerde apparaten**.
2. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een willekeurige naam in. Dit beleid is tijdelijk en wordt niet opgeslagen.
    - **Platform**: Selecteer **Android Enterprise**.
    - **Profieltype**: Selecteer **Alleen werkprofiel**.
    - **Beoogde app**: Selecteer de VPN-client-app die u eerder hebt toegevoegd.

3. Selecteer **Volgende**.
4. Voer in **Instellingen** de volgende eigenschappen in:

    - **Indeling van de configuratie-instellingen**: Selecteer **Configuration Designer gebruiken**.
    - **Toevoegen**: Hiermee wordt de lijst met configuratiesleutels weergegeven. Selecteer een willekeurige sleutel met een **tekenreeks** als **Waardetype**. Selecteer **OK**.

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" alt-text="In Configuration Designer een willekeurige sleutel met een tekenreeks als waardetype selecteren in configuratiebeleid voor VPN-apps van Microsoft Intune":::

5. Wijzig het **Waardetype** van **tekenreeks** in **certificaat**. Met deze stap kunt u het juiste clientcertificaatprofiel selecteren dat de VPN verifieert:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png" alt-text="De naam van de verbinding wijzigen in een configuratiebeleid voor VPN-apps in Microsoft Intune - voorbeeld":::

6. Wijzig direct het **Waardetype** weer in **tekenreeks**. De **Configuratiewaarde** verandert in een token `{{cert:GUID}}`:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png" alt-text="De configuratiewaarde toont het certificaattoken in een configuratiebeleid voor VPN-apps in Microsoft Intune":::

7. Kopieer en plak dit certificaattoken in een ander bestand, zoals een teksteditor.

8. Negeer dit beleid. Sla het niet op. Het enige doel is het certificaattoken te kopiëren en te plakken.

### <a name="create-the-vpn-policy-using-json"></a>Het VPN-beleid maken met behulp van JSON

1. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apps** > **App-configuratiebeleid** > **Toevoegen** > **Beheerde apparaten**.

2. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **App-configuratiebeleid: Cisco AnyConnect VPN-beleid voor apparaten met een Android Enterprise-werkprofiel in het hele bedrijf**.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.
    - **Platform**: Selecteer **Android Enterprise**.
    - **Profieltype**: Uw opties zijn:
      - **Alle profieltypen**: Deze optie biedt ondersteuning voor verificatie op basis van gebruikersnaam en wachtwoord. Gebruik deze optie niet als u verificatie op basis van certificaten gebruikt.
      - **Alleen volledig beheerde en toegewezen werkprofielen in bedrijfseigendom**: Deze optie biedt ondersteuning voor verificatie op basis van certificaten en verificatie op basis van gebruikersnaam en wachtwoord.
      - **Alleen werkprofiel**: Deze optie biedt ondersteuning voor verificatie op basis van certificaten en verificatie op basis van gebruikersnaam en wachtwoord.
    - **Beoogde app**: Selecteer de VPN-client-app die u eerder hebt toegevoegd. 

3. Selecteer **Volgende**.
4. Voer in **Instellingen** de volgende eigenschappen in:

    - **Indeling van de configuratie-instellingen**: Selecteer **JSON-gegevens invoeren**. U kunt de JSON rechtstreeks bewerken.
    - **JSON-sjabloon downloaden**: Gebruik deze optie om de sjabloon in een externe editor te downloaden en bij te werken. Wees voorzichtig met teksteditors die gebruikmaken van **gekrulde aanhalingstekens**, omdat deze mogelijk een ongeldige JSON maken.

    Nadat u de benodigde waarden voor uw configuratie hebt opgegeven, verwijdert u alle instellingen die `"STRING_VALUE"` of `STRING_VALUE` hebben.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png" alt-text="Voorbeeld van het gebruik van de JSON-stroom: JSON bewerken.":::

5. Selecteer **Volgende**.
6. Selecteer in **Toewijzingen** de groepen waaraan u het configuratiebeleid voor VPN-apps wilt toewijzen.

    Selecteer **Volgende**.

7. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken** selecteert, worden uw wijzigingen opgeslagen en wordt het beleid geïmplementeerd in uw groepen. Het beleid wordt ook weergegeven in de lijst met app-configuratiebeleid.

#### <a name="json-example-for-f5-access-vpn"></a>Voorbeeld van JSON voor F5 Access VPN

``` JSON
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "app:com.f5.edge.client_ics",
    "managedProperty": [
        {
            "key": "disallowUserConfig",
            "valueBool": false
        },
        {
            "key": "vpnConfigurations",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "name",
                            "valueString": "MyCorpVPN"
                        },
                        {
                            "key": "server",
                            "valueString": "vpn.contoso.com"
                        },
                        {
                            "key": "weblogonMode",
                            "valueBool": false
                        },
                        {
                            "key": "fipsMode",
                            "valueBool": false
                        },
                        {
                            "key": "clientCertKeychainAlias",
                            "valueString": "{{cert:77333880-14e9-0aa0-9b2c-a1bc6b913829}}"
                        },
                        {
                            "key": "allowedApps",
                            "valueString": "com.microsoft.emmx"
                        },
                        {
                            "key": "mdmAssignedId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmInstanceId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceUniqueId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceWifiMacAddress",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceSerialNumber",
                            "valueString": ""
                        },
                        {
                            "key": "allowBypass",
                            "valueBool": false
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="additional-information"></a>Aanvullende informatie

- [App-configuratiebeleid toevoegen voor beheerde Android Enterprise-apparaten](app-configuration-policies-use-android.md)
- [Instellingen voor Android Enterprise-apparaten voor het configureren van VPN in Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Volgende stappen

- [VPN-profielen maken om verbinding te maken met VPN-servers in Intune](../configuration/vpn-settings-configure.md)

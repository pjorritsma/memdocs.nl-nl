---
title: Een VPN voor Android Enterprise-apparaten configureren
titleSuffix: Microsoft Intune
description: Gebruik een app-beveiligingsbeleid om een VPN te configureren voor Android Enterprise-apparaten.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/01/2020
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
ms.openlocfilehash: bcb7bd506d92befa3c73faf7270de28765f5b192
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347415"
---
# <a name="configure-a-vpn-for-android-enterprise-devices"></a>Een VPN voor Android Enterprise-apparaten configureren

In dit onderwerp wordt beschreven hoe u een app-configuratiebeleid maakt dat in combinatie met een VPN-client kan worden geïmplementeerd op Android Enterprise-apparaten. Met deze configuratie kan het netwerkverkeer voor gekozen toepassingen toegang krijgen tot bedrijfsbronnen.

> [!NOTE]
> Het Android-platform biedt momenteel geen ondersteuning voor de automatische activering van een VPN-clientverbinding wanneer een van de gekozen toepassingen wordt geopend. De VPN-verbinding moet eerst handmatig worden geïnitieerd of u kunt [Always-on-VPN](../configuration/vpn-settings-android-enterprise.md) gebruiken.

De vereisten voor het maken van een configuratiebeleid om succesvolle VPN-toegang te verkrijgen, omvat de mogelijkheid van de gekozen VPN-client om configuratieprofielen voor beheerde toepassingen te ondersteunen. Op dit moment bieden de volgende VPN-clients ondersteuning voor het configuratiebeleid van Intune-apps:
- Cisco AnyConnect
- Citrix SSO
- F5-toegang
- Palo Alto Global Protect
- Pulse Secure
- SonicWall Mobile Connect

Als voor de verificatiemethode voor toegang tot het VPN-eindpunt clientcertificaten moeten worden gebruikt, moeten de certificaatprofielen vooraf worden gemaakt om de vereiste waarden voor het app-configuratiebeleid in te vullen.

> [!NOTE]
> De scenario's van het Android Enterprise-werkprofiel ondersteunen zowel SCEP- als PKCS-certificaten, maar scenario's voor Android Enterprise-apparaateigenaar ondersteunen alleen SCEP-certificaten. 

De basisstroom voor het maken en testen van het per-app VPN-profiel bestaat uit de volgende stappen:
1.  Kies de juiste VPN-clienttoepassing voor uw infrastructuur.
2.  Identificeer de toepassingspakket-id's van de productiviteitsapps die u wilt gebruiken met de VPN-verbinding.
3.  Implementeer certificaatprofielen die vereist zijn om te voldoen aan de verificatievereisten van de VPN-verbinding. Controleer of de implementatie is geslaagd.
4.  Implementeer de VPN-clienttoepassing.
5.  Bereid het op app-configuratie gebaseerde VPN-profiel voor met behulp van de gegevens die tijdens de eerdere stappen zijn verzameld.
6.  Implementeer het zojuist gemaakte VPN-profiel.
7.  Controleer of de VPN-client-app verbinding kan maken met de VPN-serverinfrastructuur.
8.  Controleer of het verkeer van uw gekozen productiviteitsapps door de VPN-verbinding wordt geleid wanneer deze actief is.

## <a name="get-the-app-package-id"></a>De id voor het app-pakket ophalen

Identificeer de pakket-id voor elke toepassing waaraan u VPN-toegang wilt verlenen. Voor openbaar beschikbare toepassingen kunt u de pakket-id's ophalen voor elk van de toepassingen in de Google Play Store. De weergegeven URL voor elke toepassing bevat de pakket-id. De pakket-id voor de Android-versie van de Microsoft Edge-browser is bijvoorbeeld `com.microsoft.emmx`. De pakket-id is opgenomen als onderdeel van de URL.

![Een voorbeeld van het zoeken naar de pakket-id van een app.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png)

Voor Line-of-Business-apps (LOB) vraagt u uw leverancier of het ontwikkelteam van de toepassing naar de relevante pakket-id.

## <a name="certificates"></a>Certificaten

In dit onderwerp wordt ervan uitgegaan dat uw VPN-verbinding gebruikmaakt van verificatie op basis van certificaten en dat u alle certificaten in de keten hebt geïmplementeerd die nodig zijn voor het slagen van de clientverificatie. Dit zijn normaal gesproken het clientcertificaat, eventuele tussenliggende certificaten en het basiscertificaat.
Als u meer informatie wilt over de implementatie van certificaten voor Android Enterprise, bestudeert u eerst het onderwerp [Certificaten voor verificatie gebruiken in Microsoft Intune](../protect/certificates-configure.md).

Wanneer het certificaatprofiel voor clientverificatie is geïmplementeerd, hebt u enkele details over dat profiel nodig om het configuratiebeleid voor de VPN-app te maken.
Als u niet bekend bent met het maken van app-configuratieprofielen, raadpleegt u het onderwerp [App-configuratiebeleidsregels toevoegen voor beheerde Android Enterprise-apparaten](../apps/app-configuration-policies-use-android.md).
 

## <a name="build-the-vpn-profile"></a>Het VPN-profiel bouwen

U kunt op twee manieren het app-configuratiebeleid voor uw VPN-app maken. U kunt de **Configuratieontwerper** gebruiken of de optie **JSON-gegevens**. De optie **JSON-gegevens** is vereist wanneer niet alle vereiste VPN-instellingen beschikbaar zijn in de methode **Configuratieontwerper**. Neem contact op met de leverancier van uw VPN voor ondersteuning als u hebt vastgesteld dat de JSON-optie nodig is. In dit onderwerp ziet u voorbeelden van beide methoden. In zowel de methode **JSON-gegevens** als de methode **Configuratieontwerper** kunt u verificatie op basis van certificaten implementeren. Wanneer u de methode **JSON-gegevens** gebruikt, kunt u beginnen met behulp van de **Configuratieontwerper** om de benodigde profielwaarden uit te pakken.

> [!NOTE]
> Hoewel veel van de configuratieparameters voor de VPN-client vergelijkbaar zijn, heeft elke app zijn unieke sleutels en opties. Neem contact op met uw VPN-leverancier als er vragen ontstaan. 

## <a name="use-the-configuration-designer-flow"></a>De stroom Configuratieontwerper gebruiken

1.  Begin met het toevoegen van een nieuw app-configuratiebeleid voor **Beheerde apparaten**.
2.  Voer een geschikte naam in.
3.  Selecteer **Android Enterprise** als het platform.
4.  Selecteer ofwel **Alleen werkprofiel** ofwel **Alleen apparaateigenaar** als het profieltype als verificatie op basis van een certificaat is vereist. Het **Profiel werkeigenaar en apparaateigenaar** is niet compatibel met verificatie op basis van certificaten.
5.  Selecteer voor de doeltoepassing de VPN-client die u hebt geïmplementeerd. In dit voorbeeld gebruiken we de eerder geïmplementeerde Cisco AnyConnect VPN-client

  ![Voorbeeld van het maken van een app-configuratiebeleid: basisbeginselen.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png)

6. Op de volgende pagina gebruikt u de vervolgkeuzelijst met configuratie-instellingen en selecteert u de optie **Configuratieontwerper gebruiken**.

  ![Voorbeeld van het gebruiken van de stroom Configuratieontwerper: instellingen.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png)

7. Klik op **Toevoegen** om de lijst met configuratiesleutels weer te geven.
8.  Selecteer alle configuratiesleutels die u nodig hebt voor de gekozen configuratie. In dit voorbeeld gebruiken we een minimale lijst om in te stellen voor een AnyConnect VPN, inclusief verificatie op basis van certificaten en VPN per app.
  
  <img alt="Example of using the Configuration Designer Flow - Configuration keys." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" width="350">

9. Voer de juiste waarden in voor de sleutels **Verbindingsnaam**, **Host** en **Protocol**.

  ![Voorbeeld van het gebruiken van de stroom Configuratieontwerper: selectie van configuratiesleutel.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png)  

  > [!NOTE]
  > De namen van deze sleutels kunnen variëren en zijn afhankelijk van de VPN-clienttoepassing waarvoor u het beleid bouwt.

10. Voer de toepassingspakket-id('s) in die u eerder hebt verzameld in de sleutel **Toegestane apps per-app VPN**.

  ![Voorbeeld van het gebruiken van de stroom Configuratieontwerper: toepassingspakket-id's.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png)  

11. Wijzig in de sleutel **Alias sleutelhangercertificaat** (optioneel) het **Waardetype** van **tekenreeks** in **certificaat**, zodat u het juiste clientcertificaatprofiel kunt kiezen dat moet worden gebruikt voor VPN-verificatie.

  ![Voorbeeld van het gebruik van de stroom Configuratieontwerper: certificaatalias sleutelhanger bijwerken.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png)  

12. Kies op de volgende pagina de gewenste bereiktags.
13. Voer op de volgende pagina de juiste groepen in waarop u het app-configuratiebeleid wilt implementeren.
14. Selecteer **Maken** om het maken en implementeren van het beleid te voltooien.

  ![Voorbeeld van het gebruiken van de stroom Configuratieontwerper: controle.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png)  

## <a name="use-the-json-flow"></a>De JSON-stroom gebruiken

Maak een tijdelijk profiel:
1.  Begin met het toevoegen van een nieuw app-configuratiebeleid voor **Beheerde apparaten**.
2.  Voer een passende naam in (het gebruik van dit profiel is tijdelijk, omdat het niet wordt opgeslagen).
3.  Selecteer **Android Enterprise** als het platform.
4.  Selecteer voor de doeltoepassing de VPN-client die u hebt geïmplementeerd.
5.  Selecteer ofwel **Alleen werkprofiel** ofwel **Alleen apparaateigenaar** als het profieltype als verificatie op basis van een certificaat is vereist. Het **Profiel werkeigenaar en apparaateigenaar** is niet compatibel met verificatie op basis van certificaten.

  ![Voorbeeld van het gebruik van de JSON-stroom: basisbeginselen.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-09.png)  

6.  Op de volgende pagina gebruikt u de vervolgkeuzelijst **Configuratie-instellingen** en selecteert u de optie **Configuratieontwerper** gebruiken.

  ![Voorbeeld van het gebruik van de JSON-stroom: indeling van de configuratie-instellingen.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-10.png)  

7.  Klik op **Toevoegen** om de lijst met configuratiesleutels weer te geven.
8.  Selecteer een van de sleutels met het **Waardetype** **tekenreeks** en klik op **OK**.

  <img alt="Example of using the JSON Flow - Select a key." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" width="350">

9.  Wijzig nu het **Waardetype** van **tekenreeks** in **certificaat**. Zo kunt u het juiste clientcertificaatprofiel kiezen dat moet worden gebruikt voor VPN-verificatie.

  ![Voorbeeld van het gebruik van de JSON-stroom: verbindingsnaam.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png)  

10. Wijzig direct het **Waardetype** weer in **tekenreeks**. Denk erom dat de **Configuratiewaarde** verandert in een token met de indeling `{{cert:GUID}}`.
11. Selecteer de tokenweergave van het certificaat en kopieer deze naar een alternatieve locatie, zoals een teksteditor.

  ![Voorbeeld van het gebruik van de JSON-stroom: configuratiewaarde.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png)  

12. Negeer het profiel dat wordt gemaakt: het enige doel van de vorige stappen is om het certificaattoken te bepalen.

### <a name="create-the-vpn-profile"></a>Het VPN-profiel maken

1.  Begin met het toevoegen van een nieuw toepassingsconfiguratieprofiel voor **Beheerde apparaten**.
2.  Voer een geschikte naam in.
3.  Selecteer **Android Enterprise** als het platform.
4.  Selecteer voor de doeltoepassing de VPN-client die u hebt geïmplementeerd.
5.  Selecteer ofwel **Alleen werkprofiel** ofwel **Alleen apparaateigenaar** als het profieltype als verificatie op basis van een certificaat is vereist. Het **Profiel werkeigenaar en apparaateigenaar** is niet compatibel met verificatie op basis van certificaten.
6.  Gebruik de vervolgkeuzelijst **Configuratie-instellingen** en selecteer de optie **JSON-gegevens invoeren**.
7.  U kunt de JSON rechtstreeks bewerken, maar u kunt ook de knop **JSON-sjabloon downloaden** gebruiken om het sjabloon te downloaden en vervolgens te wijzigen in een externe editor van uw keuze. Pas op met teksteditors die de optie hebben om **Gekrulde aanhalingstekens** te gebruiken, omdat hiermee de JSON ongeldig zou worden.

  ![Voorbeeld van het gebruik van de JSON-stroom: JSON bewerken.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png)  

8.  Welke methode u ook gebruikt, nadat u de waarden hebt ingevuld die u nodig hebt voor de gewenste configuratie, moeten alle resterende instellingen met een 'STRING_VALUE'- of STRING_VALUE-waarde in de volledige JSON worden verwijderd.

#### <a name="example-json-for-f5-access-vpn"></a>Voorbeeld van JSON voor F5 Access VPN

Hierna volgt een voorbeeld van JSON-gegevens voor F5 Acces VPN.

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

## <a name="summary"></a>Samenvatting

Door gebruik te maken van een app-configuratiebeleid voor in Android Enterprise ingeschreven apparaten kunt u gebruikmaken van per-app VPN-gedrag, ondanks dat er geen rechtstreekse ondersteuning voor is in het platform. 

## <a name="additional-information"></a>Aanvullende informatie

Zie de volgende onderwerpen voor gerelateerde informatie:
- [App-configuratiebeleid toevoegen voor beheerde Android Enterprise-apparaten](../apps/app-configuration-policies-use-android.md)
- [Instellingen voor Android Enterprise-apparaten voor het configureren van VPN in Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Volgende stappen

- [VPN-profielen maken om verbinding te maken met VPN-servers in Intune](../configuration/vpn-settings-configure.md)

---
title: App-configuratiebeleidsregels voor beheerde iOS-/iPadOS-apparaten toevoegen
titleSuffix: Microsoft Intune
description: Informatie over het gebruiken van app-configuratiebeleidsregels om configuratiegegevens te leveren aan een iOS-/iPadOS-app wanneer dit wordt uitgevoerd.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c9163693-d748-46e0-842a-d9ba113ae5a8
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a8480ec3f7d83ad5819e21ad34b9dfbc67f38999
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907337"
---
# <a name="add-app-configuration-policies-for-managed-iosipados-devices"></a>App-configuratiebeleidsregels voor beheerde iOS-/iPadOS-apparaten toevoegen

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Gebruik app-configuratiebeleidsregels in Microsoft Intune om aangepaste configuratie-instellingen te leveren voor een iOS-/iPadOS-app. Met deze configuratie-instellingen kan een app worden aangepast op basis van de richting van de leverancier van de app. U krijgt deze configuratie-instellingen (sleutels en waarden) van de leverancier van de app. Als u de app wilt configureren, geeft u de instellingen op als sleutels en waarden, of als XML die de sleutels en waarden bevat.

Als Microsoft Intune-beheerder kunt u bepalen welke gebruikersaccounts worden toegevoegd aan Microsoft Office-toepassingen op beheerde apparaten. U kunt de toegang beperken tot uitsluitend toegestane gebruikersaccounts van de organisatie, en persoonlijke accounts blokkeren op ingeschreven apparaten. De app-configuratie wordt verwerkt op de ondersteunende toepassingen, en niet-goedgekeurde accounts worden verwijderd en geblokkeerd. De instellingen van het configuratiebeleid worden gebruikt wanneer de app deze controleert, doorgaans bij de eerste keer dat de app wordt uitgevoerd.

Zodra u een appconfiguratiebeleid hebt toegevoegd, kunt u de toewijzingen voor het appconfiguratiebeleid instellen. Wanner u de toewijzingen voor het beleid instelt, kunt u ervoor kiezen de groep gebruikers voor wie het beleid van toepassing is op te nemen of uit te sluiten. Als u ervoor kiest een of meer groepen op te nemen, kunt u specifieke groepen selecteren waarvoor u ingebouwde groepen wilt opnemen of selecteren. Ingebouwde groepen zijn **Alle gebruikers**, **Alle apparaten** en **Alle gebruikers + alle apparaten**. 

> [!NOTE]
> Intune biedt vooraf gemaakte de groepen **Alle gebruikers** en **Alle apparaten** in de console met handige, ingebouwde optimalisaties. Het wordt ten zeerste aanbevolen deze groepen te gebruiken om u op alle gebruikers en alle apparaten te richten in plaats van de groepen 'Alle gebruikers' en 'Alle apparaten' die u mogelijk zelf hebt gemaakt.

Nadat u de opgenomen groepen hebt geselecteerd voor het configuratiebeleid van uw toepassing, kunt u de specifieke groepen selecteren die moeten worden uitgesloten. Zie [App-toewijzingen opnemen en uitsluiten in Microsoft Intune](apps-inc-exl-assignments.md) voor meer informatie.

> [!TIP]
> Dit beleidstype is momenteel alleen beschikbaar voor apparaten met iOS/iPadOS 8.0 en hoger. Ondersteunt de volgende typen app-installaties:
>
> - **Beheerde iOS-/iPadOS-app uit de App Store**
> - **App-pakket voor iOS**
>
> Zie [Apps toevoegen aan Microsoft Intune](apps-add.md) voor meer informatie over app-installatietypen. Zie Managed App Configuration in de [documentatie voor iOS-ontwikkelaars](https://developer.apple.com/library/archive/samplecode/sc2279/Introduction/Intro.html) voor meer informatie over het opnemen van de app-configuratie in uw IPA-app-pakket voor beheerde apparaten.

## <a name="create-an-app-configuration-policy"></a>Een app-configuratiebeleid maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Kies de opties **Apps** > **App-configuratiebeleid** > **Toevoegen** > **Beheerde apparaten**. U kunt kiezen tussen **Beheerde apparaten** en **Beheerde apps**. Zie [Apps die app-configuratie ondersteunen](app-configuration-policies-overview.md#apps-that-support-app-configuration) voor meer informatie.
3. Stel op de pagina **Basisinformatie** de volgende gegevens in:
    - **Naam**: de naam van het profiel zoals deze in Azure Portal wordt weergegeven.
    - **Beschrijving**: de beschrijving van het profiel dat wordt weergegeven in Azure Portal.
    - **Type apparaatinschrijving** - deze instelling is ingesteld op **Beheerde apparaten**.
4. Selecteer **iOS/iPadOS** als **Platform**.
5. Klik op **App selecteren** naast **Beoogde app**. Het deelvenster **Gekoppelde app** wordt weergegeven. 
6. Kies in het deelvenster **Beoogde app** de beheerde app die u wilt koppelen aan het configuratiebeleid en klik op **OK**.
7. Klik op **Volgende** om de pagina **Instelling** weer te geven.
8. Selecteer in de vervolgkeuzelijst de **Indeling van de configuratie-instellingen**. Selecteer een van de volgende methoden om configuratiegegevens toe te voegen:
    - **Configuration Designer gebruiken**
    - **XML-gegevens invoeren**<br><br>
    Zie [Configuration Designer gebruiken](#use-configuration-designer) voor meer informatie over het gebruik van Configuration Designer. Zie [XML-gegevens invoeren](#enter-xml-data) voor meer informatie over het invoeren van XML-gegevens. 
9. Klik op **Volgende** om de pagina **Toewijzingen** weer te geven.
10. Selecteer in de vervolgkeuzelijst naast **Toewijzen aan** de optie **Geselecteerde groepen**, **Alle gebruikers**, **Alle apparaten** of **Alle gebruikers en alle apparaten** om het app-configuratiebeleid aan toe te wijzen.

    ![Schermafbeelding van Beleidstoewijzingen op het tabblad Opnemen](./media/app-configuration-policies-use-ios/app-config-policy01.png)

11. Selecteer **Alle gebruikers** in de vervolgkeuzelijst.

    ![Schermafbeelding van Beleidstoewijzingen met de vervolgkeuzemenu-optie Alle gebruikers](./media/app-configuration-policies-use-ios/app-config-policy02.png)

12. Klik op **Groepen voor uitsluiten selecteren** om het gerelateerde deelvenster weer te geven.

    ![Schermopname van Beleidstoewijzingen - het deelvenster Groepen selecteren die moeten worden uitgesloten](./media/app-configuration-policies-use-ios/app-config-policy03.png)

13. Kies de groepen die u wilt uitsluiten en klik vervolgens op **Selecteren**.

    >[!NOTE]
    >Wanneer u een groep toevoegt en als er al een andere groep is opgenomen voor een gegeven toewijzingstype, wordt deze groep vooraf geselecteerd. Dit kan niet worden gewijzigd voor andere toewijzingstypen voor opnemen. De groep die is gebruikt, kan daarom niet als een uitgesloten groep worden gebruikt.

14. Klik op **Volgende** om naar de pagina **Controleren en maken** weer te geven.
15. Klik op **Maken** om het configuratiebeleid toe te voegen aan Intune.

## <a name="use-configuration-designer"></a>Configuration Designer gebruiken

Microsoft Intune biedt configuratie-instellingen die uniek zijn voor een app. U kunt Configuration Designer gebruiken voor apps op apparaten die wel of niet zijn ingeschreven bij Microsoft Intune. Met de ontwerper kunt u specifieke configuratiesleutels en -waarden instellen waarmee u de onderliggende XML kunt maken. U kunt tevens het gegevenstype voor elke waarde opgeven. Deze instellingen worden automatisch aan apps geleverd wanneer de apps worden geïnstalleerd.

### <a name="add-a-setting"></a>Een instelling toevoegen

1. Stel voor elke sleutel en waarde in de configuratie het volgende in:
   - **Configuratiesleutel**: de sleutel waarmee de specifieke instellingsconfiguratie wordt geïdentificeerd.
   - **Waardetype**: het gegevenstype van de configuratiewaarde. Typen zijn onder meer geheel getal, reëel, tekenreeks of booleaans.
   - **Configuratiewaarde**: de waarde voor de configuratie.
2. Kies **OK** om uw configuratiewaarden in te stellen.

### <a name="delete-a-setting"></a>Een instelling verwijderen

1. Kies het weglatingsteken ( **...** ) naast de instelling.
2. Selecteer **Verwijderen**.

De tekens \{\{ en \}\} worden alleen gebruikt door tokentypen en mogen niet worden gebruikt voor andere doeleinden.

### <a name="allow-only-configured-organization-accounts-in-multi-identity-apps"></a>Alleen geconfigureerde organisatieaccounts toestaan in apps met meerdere identiteiten 

Als Microsoft Intune-beheerder kunt u bepalen welke werk- of schoolaccounts worden toegevoegd aan Microsoft-apps op beheerde apparaten. U kunt de toegang beperken tot uitsluitend toegestane gebruikersaccounts van de organisatie, en persoonlijke accounts blokkeren op ingeschreven apparaten. Voor iOS-en iPadOS-apparaten gebruikt u de volgende sleutel/waarde-paren in een app-configuratiebeleid voor beheerde apparaten:

| **Sleutel** | **Waarden** |
|----|----|
| IntuneMAMAllowedAccountsOnly | <ul><li>**Ingeschakeld**: Het enige account dat is toegestaan, is het beheerde gebruikersaccount dat wordt gedefinieerd door de sleutel [IntuneMAMUPN](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).</li><li>**Uitgeschakeld** (of een andere waarde die geen hoofdletterongevoelige overeenkomst is met **Ingeschakeld**): Elk account is toegestaan.</li></ul> |
| IntuneMAMUPN | <ul><li>De UPN van het account waarvoor aanmelden bij de app is toegestaan.</li><li> Voor apparaten die zijn ingeschreven bij Intune, kan het <code>{{userprincipalname}}</code>-token worden gebruikt voor het ingeschreven gebruikersaccount.</li></ul>  |

   > [!NOTE]
   > De volgende apps verwerken de bovenstaande app-configuratie en staan alleen organisatieaccounts toe:
   > - Edge voor iOS (44.8.7 en hoger)
   > - OneDrive voor iOS (10.34 en hoger)
   > - Outlook voor iOS (2.99.0 en hoger)
   > - Teams voor iOS (2.0.15 en hoger)

## <a name="enter-xml-data"></a>XML-gegevens invoeren

U kunt een XML-eigenschappenlijst typen of plakken die de app-configuratie-instellingen bevat voor bij Intune ingeschreven apparaten. De indeling van de XML-eigenschappenlijst is afhankelijk van de app die u wilt configureren. Neem contact op met de leverancier van de app voor meer informatie over de precieze indeling die moet worden gebruikt.

Intune valideert de XML-indeling. Intune controleert echter niet of de XML-eigenschappenlijst (Plist) met de doelapp werkt.

Voor meer informatie over XML-eigenschappenlijsten:

- Raadpleeg [Uitleg van XML Plists](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) in de iOS Developer-bibliotheek.

### <a name="example-format-for-an-app-configuration-xml-file"></a>Voorbeeld van een indeling voor het XML-configuratiebestand voor een app

Wanneer u een configuratiebestand voor een app maakt, kunt u een of meer van de volgende waarden opgeven door van deze indeling gebruik te maken:

```xml
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
  <key>aaddeviceid</key>
  <string>{{aaddeviceid}}</string>
</dict>
```

### <a name="supported-xml-plist-data-types"></a>Ondersteunde XML PList-gegevenstypen

Intune ondersteunt de volgende gegevenstypen in een eigenschappenlijst:

- &lt;geheel getal&gt;
- &lt;reëel&gt;
- &lt;tekenreeks&gt;
- &lt;matrix&gt;
- &lt;woordenlijst&gt;
- &lt;waar /&gt; of &lt;onwaar /&gt;

### <a name="tokens-used-in-the-property-list"></a>In de eigenschappenlijst gebruikte tokens

Intune ondersteunt verder de volgende typen tokens in de lijst met eigenschappen:
- \{\{userprincipalname\}\} – bijvoorbeeld **Jan\@contoso.com**
- \{\{mail\}\} – bijvoorbeeld **Jan\@contoso.com**
- \{\{partialupn\}\} - bijvoorbeeld**Jan**
- \{\{accountid\}\} - bijvoorbeeld **fc0dc142-71d8-4b12-bbea-bae2a8514c81**
- \{\{deviceid\}\} - bijvoorbeeld **b9841cd9-9843-405f-be28-b2265c59ef97**
- \{\{userid\}\} - bijvoorbeeld **3ec2c00f-b125-4519-acf0-302ac3761822**
- \{\{username\}\} - bijvoorbeeld **Jan de Vries**
- \{\{serialnumber\}\} -bijvoorbeeld **F4KN99ZUG5V2** (voor iOS-/iPadOS-apparaten)
- \{\{serialnumberlast4digits\}\} - bijvoorbeeld **G5V2** (voor iOS-/iPadOS-apparaten)
- \{\{aaddeviceid\}\}— bijvoorbeeld **ab0dc123-45d6-7e89-aabb-cde0a1234b56**

## <a name="configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices"></a>De bedrijfsportal-app configureren voor ondersteuning van iOS en iPadOS DEP-apparaten

DEP-inschrijvingen (Device Enrollment Program van Apple) zijn niet compatibel met de App Store-versie van de bedrijfsportal-app. U kunt de bedrijfsportal-app echter configureren voor ondersteuning van iOS/iPadOS DEP-apparaten met behulp van de volgende stappen.

1. Voeg in Intune zo nodig de Intune-bedrijfsportal-app toe. Hiervoor gaat u naar **Intune** > **Apps** > **Alle apps** > **Toevoegen**.
2. Ga naar **Apps** > **App-configuratiebeleid** om een app-configuratiebeleid voor de bedrijfsportal-app te maken.
3. Maak een app-configuratiebeleid met de onderstaande XML. Meer informatie over het maken van een app-configuratiebeleid en het invoeren van XML-gegevens vindt u in [Add app configuration policies for managed iOS/iPadOS devices](app-configuration-policies-use-ios.md) (App-configuratiebeleidsregels voor beheerde iOS-/iPadOS-apparaten toevoegen).

    - **Gebruik de Bedrijfsportal op een DEP-apparaat dat is ingeschreven met gebruikersaffiniteit:**

        ``` xml
        <dict>
            <key>IntuneCompanyPortalEnrollmentAfterUDA</key>
            <dict>
                <key>IntuneDeviceId</key>
                <string>{{deviceid}}</string>
                <key>UserId</key>
                <string>{{userid}}</string>
            </dict>
        </dict>
        ```
    - **Gebruik de Bedrijfsportal op een DEP-apparaat dat is ingeschreven zonder gebruikersaffiniteit**:

        > [!NOTE]
        > De gebruiker die zich aanmeldt bij de Bedrijfsportal wordt ingesteld als de primaire gebruiker van het apparaat.

        ``` xml
        <dict>
            <key>IntuneUDAUserlessDevice</key>
            <string>{{SIGNEDDEVICEID}}</string>
        </dict>
        ```     

4. Implementeer de bedrijfsportal op apparaten met het app-configuratiebeleid voor de gewenste groepen. Implementeer het beleid alleen voor groepen apparaten die al via DEP zijn ingeschreven.
5. Informeer eindgebruikers dat ze zich bij de bedrijfsportal-app moeten aanmelden nadat deze automatisch is geïnstalleerd.

## <a name="monitor-iosipados--app-configuration-status-per-device"></a>Configuratiestatus van een iOS-/iPadOS-app per apparaat controleren 
Nadat een configuratiebeleid is toegewezen, kunt u de configuratiestatus van een iOS-/iPadOS-app voor elk beheerd apparaat controleren. Selecteer vanaf **Microsoft Intune** in Azure Portal de optie **Apparaten** > **Alle apparaten**. Selecteer in de lijst met beheerde apparaten een specifiek apparaat om een deelvenster voor het apparaat weer te geven. Selecteer **App-configuratie** op het deelvenster van het apparaat.  

## <a name="additional-information"></a>Aanvullende informatie

- [Configuratie-instellingen voor de Outlook-app voor iOS/iPadOS en Android implementeren](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

## <a name="next-steps"></a>Volgende stappen

Ga verder met het [toewijzen](apps-deploy.md) en [controleren](apps-monitor.md) van de app.
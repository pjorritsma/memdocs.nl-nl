---
title: Microsoft Defender ATP in Microsoft Intune gebruiken - Azure | Microsoft Docs
description: Gebruik Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) met Intune voor het instellen, configureren en onboarden van uw Intune-apparaten met ATP. Gebruik vervolgens een ATP-risicobeoordeling voor uw apparaten met Intune-beleid voor apparaatcompatibiliteit en voorwaardelijke toegang om uw netwerkresources te beveiligen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1141879a282219cdac72273e47c84b51df172d04
ms.sourcegitcommit: 397ec824f1368dcf06c3870c89f52347852062bd
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/23/2020
ms.locfileid: "85264053"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Naleving voor Microsoft Defender ATP met voorwaardelijke toegang in Intune afdwingen

U kunt Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) integreren met Microsoft Intune als een Mobile Threat Defense-oplossing. Dankzij integratie kunt u beveiligingsrisico's helpen voorkomen en de impact van beveiligingsschending binnen een organisatie beperken. Microsoft Defender ATP werkt op apparaten waarop Windows 10 of hoger wordt uitgevoerd, en op Android-apparaten.

Gebruik voor het beste resultaat een combinatie van de volgende configuraties:

- **Maak een service-naar-service-verbinding tussen Intune en Microsoft Defender ATP**. Met deze verbinding kan Microsoft Defender ATP gegevens verzamelen over risico's voor ondersteunde apparaten die u beheert met Intune.
- **Gebruik een profiel voor apparaatconfiguratie om apparaten te onboarden met Microsoft Defender ATP**. U kunt apparaten onboarden om deze te configureren zodat ze communiceren met Microsoft Defender ATP en de gegevens aanleveren om hun risiconiveau te bepalen.
- **Gebruik een nalevingsbeleid voor apparaten om het risiconiveau dat u wilt toestaan te bepalen**. Risiconiveaus worden gerapporteerd door Microsoft Defender ATP. Apparaten die het toegestane risiconiveau overschrijden, worden aangeduid als niet-compatibel.
- **Gebruik beleid voor voorwaardelijke toegang** om te voorkomen dat gebruikers toegang krijgen tot bedrijfsresources vanaf apparaten die niet-compatibel zijn.

Wanneer u Intune integreert met Microsoft Defender ATP, hebt u ook toegang tot Threat & Vulnerability Management (TVM) van Microsoft Defender ATP en kunt u [Intune gebruiken voor het wegnemen van beveiligingsproblemen die door TVM op eindpunten zijn geïdentificeerd](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Voorbeeld van het gebruik van Microsoft Defender ATP met Intune

In het volgende voorbeeld wordt uitgelegd hoe deze oplossingen samenwerken om uw organisatie te beschermen. Voor dit voorbeeld zijn Microsoft Defender ATP en Intune al geïntegreerd.

Denk bijvoorbeeld aan een situatie waarin iemand een Word-bijlage met ingesloten schadelijke code verzendt naar een gebruiker binnen uw organisatie.

- De gebruiker opent de bijlage en activeert de inhoud.
- Een aanval met verhoogde bevoegdheden wordt gestart en een aanvaller vanaf een externe computer heeft beheerdersrechten op het apparaat van het slachtoffer.
- De aanvaller krijgt vervolgens extern toegang tot de andere apparaten van de gebruiker. Deze beveiligingsschending kan invloed hebben op de hele organisatie.

Microsoft Defender ATP kan beveiligingsgebeurtenissen zoals dit scenario helpen oplossen.

- In ons voorbeeld detecteert Microsoft Defender ATP dat het apparaat abnormale code uitvoerde, een escalatie van procesbevoegdheden onderging, schadelijke code injecteerde en een verdachte remote shell uitgaf.
- Op basis van deze acties van het apparaat [classificeert Microsoft Defender ATP het apparaat als een hoog risico](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) en wordt een gedetailleerd rapport over de verdachte activiteiten bijgevoegd in de portal van Microsoft Defender Security Center.

Omdat u Intune-nalevingsbeleid voor apparaten gebruikt dat apparaten met *Medium* of *Hoog* risiconiveau als niet-compatibel classificeert, wordt het gecompromitteerde apparaat als niet-compatibel geclassificeerd. Deze classificatie zorgt ervoor dat het beleid voor voorwaardelijke toegang wordt toegepast en de toegang tot uw bedrijfsresources voor dit apparaat wordt geblokkeerd.

U kunt ook Intune-beleid gebruiken om enkele configuraties voor Microsoft Defender ATP op Android te wijzigen. Zie voor meer informatie [Webbeveiliging configureren op apparaten waarop Android wordt uitgevoerd ](#configure-web-protection-on-devices-that-run-android) verderop in dit artikel.

## <a name="prerequisites"></a>Vereisten

Als u Microsoft Defender ATP met Intune wilt gebruiken, moet u het volgende geconfigureerd en klaar voor gebruik hebben:

- Tenant met licentie voor Enterprise Mobility + Security E3 en Windows E5 (of Microsoft 365 Enterprise E5)
- Microsoft Intune-omgeving met [door Intune-beheerde](../enrollment/windows-enroll.md) Windows 10- of Android-apparaten die ook aan Azure AD zijn toegevoegd
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) en toegang tot de Microsoft Defender Security Center (ATP-portal)

> [!NOTE]
> Microsoft Defender ATP wordt niet ondersteund met Intune-beleid voor app-beveiliging voor iOS/iPadOS en Android.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Microsoft Defender ATP in Intune inschakelen

De eerste stap is het instellen van een service-naar-service-verbinding tussen Intune en Microsoft Defender ATP. Hiervoor moet u beheerdersrechten hebben tot zowel Microsoft Defender Security Center als voor Intune.

### <a name="to-enable-microsoft-defender-atp"></a>Microsoft Defender ATP inschakelen

U hoeft Microsoft Defender ATP slechts één keer per tenant in te schakelen.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Eindpuntbeveiliging** > **Microsoft Defender ATP**en vervolgens **Het Microsoft Defender-beveiligingscentrum openen**.

   ![Selecteren om het Microsoft Defender Security Center te openen](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

3. In **Microsoft Defender Security Center**:
   1. Selecteer **Instellingen** > **Geavanceerde functies**.
   2. Voor **Microsoft Intune-verbinding**, kiest u **Aan**:

      ![De verbinding met Intune inschakelen](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

   3. Selecteer **Voorkeuren opslaan**.

4. Ga terug naar **Microsoft Defender ATP** in het Microsoft Endpoint Manager-beheercentrum. Ga als volgt te werk onder **Instellingen voor MDM-nalevingsbeleid**, afhankelijk van de behoeften van uw organisatie:
   - Stel **Windows-apparaten met versie 10.0.15063 en hoger verbinden met Microsoft Defender ATP** in op **Aan**
   - Stel **Android-apparaten met versie 6.0.0 en hoger verbinden met Microsoft Defender ATP** in op **Aan**

5. Selecteer **Opslaan**.

> [!TIP]
> Wanneer u een nieuwe toepassing integreert in Intune Mobile Threat Defense en u de verbinding met Intune inschakelt, maakt Intune een klassiek beleid voor voorwaardelijke toegang in Azure Active Directory. Voor elke MTD-app die u integreert, zoals [Microsoft Defender ATP](advanced-threat-protection.md) of een app van een van onze aanvullende [MTD-partners](mobile-threat-defense.md#mobile-threat-defense-partners), wordt een nieuw klassiek beleid voor voorwaardelijke toegang gemaakt. De beleidsregels kunnen worden genegeerd, maar mogen niet worden bewerkt, verwijderd of uitgeschakeld.
>
> Als het klassieke beleid wordt verwijderd, moet u de verbinding met Intune die verantwoordelijk is voor het maken ervan verwijderen en deze vervolgens opnieuw instellen. Hiermee wordt het klassieke beleid opnieuw gemaakt. Het is niet mogelijk om klassiek beleid voor MTD-apps te migreren naar het nieuwe beleidstype voor voorwaardelijke toegang.
>
> Klassiek beleid voor voorwaardelijke toegang voor MTD-apps:
>
> - Wordt door Intune MTD gebruikt om te vereisen dat apparaten in Microsoft Azure Active Directory worden geregistreerd; ze beschikken dan over een apparaat-id voordat ze gaan communiceren met MTD-partners. De id is vereist omdat apparaten anders hun status niet kunnen doorgeven aan Intune.
> - Heeft geen effect op andere cloud-apps of -resources.
> - Verschilt van beleid voor voorwaardelijke toegang dat u normaal wellicht zou maken om MTD te helpen beheren.
> - Standaard wordt er niet gecommuniceerd met andere beleidsregels voor voorwaardelijke toegang die voor evaluatie worden gebruikt.
>
> Als u klassiek beleid voor voorwaardelijke toegang wilt bekijken, gaat u in [Azure](https://portal.azure.com/#home) naar **Azure Active Directory** > **Voorwaardelijke toegang** > **Klassieke beleidsregels**.

## <a name="onboard-windows-devices-by-using-a-configuration-profile"></a>Windows-apparaten onboarden met behulp van een configuratieprofiel

Voor het Windows-platform geldt dat u, na het instellen van de service-naar-serviceverbinding tussen Intune en Microsoft Defender ATP, uw door Intune beheerde apparaten kunt onboarden bij Microsoft Defender ATP, zodat gegevens over het risiconiveau kunnen worden verzameld en gebruikt. U gebruikt een profiel voor apparaatconfiguratie om apparaten te onboarden bij Microsoft Defender ATP.

Wanneer u verbinding maakte met Microsoft Defender ATP, heeft Intune van Microsoft Defender ATP een configuratiepakket voor onboarding gekregen. Dit pakket wordt geïmplementeerd op apparaten met het apparaatconfiguratieprofiel. Het configuratiepakket configureert apparaten zo dat ze communiceren met [Microsoft Defender ATP-services](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) om bestanden te scannen, bedreigingen te detecteren en het risico aan Microsoft Defender ATP te rapporteren. Wanneer u eenmaal onboarding van een apparaat met het configuratiepakket hebt uitgevoerd, dan hoeft u dit niet opnieuw te doen. U kunt apparaten onboarden met behulp van een [groepsbeleid of Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile"></a>Een apparaatconfiguratieprofiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer een **Naam** en **Beschrijving** in.
4. Voor **Platform** selecteert u **Windows 10 en hoger**
5. Voor **Profieltype** selecteert u **Microsoft Defender ATP (Windows 10 Desktop)** .
6. Configureer de gewenste instellingen:

   - **Type clientconfiguratiepakket voor Microsoft Defender ATP**: Selecteer **Onboarding uitvoeren** om het configuratiepakket aan het profiel toe te voegen. Selecteer **Offboarding uitvoeren** om configuratiepakket uit het profiel te verwijderen.
  
     > [!NOTE]
     > Als u een verbinding met Microsoft Defender ATP tot stand hebt gebracht, start **Onboarding uitvoeren** in Intune automatisch en wordt het configuratieprofiel voor u toegevoegd. In dat geval is de instelling **Type clientconfiguratiepakket voor Microsoft Defender ATP** niet beschikbaar.
  
   - **Voorbeelddeling voor alle bestanden**: Met **Inschakelen** staat u toe dat voorbeelden worden verzameld en gedeeld met Microsoft Defender ATP. Als u bijvoorbeeld een verdacht bestand ziet, kunt u het verzenden naar Microsoft Defender ATP voor grondige analyse. **Niet geconfigureerd**: eventuele voorbeelden voor het Microsoft Defender ATP worden niet gedeeld.
   - **Frequentie van telemetrierapporten versnellen**: U kunt deze instelling **inschakelen** voor apparaten met een hoog risico, zodat er vaker telemetrie naar de Microsoft Defender ATP-service wordt gerapporteerd.

     [Windows 10-apparaten onboarden die Microsoft Endpoint Configuration Manager gebruiken](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) bevat meer informatie over deze instellingen voor Microsoft Defender ATP.

7. Selecteer **OK** en **Maken** om wijzigingen op te slaan. Hiermee maakt u het profiel.
8. [Wijs een profiel voor apparaatconfiguratie toe](../configuration/device-profile-assign.md) aan apparaten die u wilt beoordelen met Microsoft Defender ATP.

## <a name="onboard-android-devices"></a>Android-apparaten onboarden
Nadat u de service-naar-service-verbinding tussen Intune en Microsoft Defender ATP hebt ingesteld, moet u uw beheerde apparaten onboarden bij Microsoft Defender ATP, zodat gegevens over het risiconiveau kunnen worden verzameld en gebruikt.

Zie [Microsoft Defender Advanced Threat Protection voor Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) in de Microsoft Defender ATP-documentatie voor gedetailleerde instructies voor het onboarden van Android-apparaten, inclusief de vereisten voor eindgebruikers en beheerders.

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>Het nalevingsbeleid maken en toewijzen om het risiconiveau van het apparaat in te stellen

Voor zowel Windows- als Android-apparaten bepaalt het nalevingsbeleid het risiconiveau dat u aanvaardbaar vindt voor een apparaat.

Als u niet bekend bent met het maken van nalevingsbeleid, raadpleegt u de procedure [Een beleid maken](../protect/create-compliance-policy.md#create-the-policy) in het artikel *Een nalevingsbeleid maken in Microsoft Intune*. De volgende informatie is specifiek voor het configureren van Microsoft Defender ATP als onderdeel van een nalevingsbeleid.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Nalevingsbeleid** > **Beleid** > **Beleid maken**.

3. Selecteer voor **Platform** een van de volgende opties in de vervolgkeuzelijst:
   - **Windows 10 en hoger**
   - **Android-apparaatbeheerder**
   - **Android Enterprise**

   Selecteer vervolgens **Maken** om het configuratievenster **Beleid maken** te openen.

4. Geef een **Naam** op waaraan u dit beleid later kunt herkennen. U kunt er ook voor kiezen om een **Beschrijving** op te geven.
  
5. Vouw op het tabblad **Nalevingsinstellingen** de groep **Microsoft Defender ATP** uit en stel de optie **Vereisen dat het apparaat op of onder het apparaatdreigingsniveau moet zijn** in op het gewenste niveau.

   De classificatie van bedreigingsniveaus wordt [bepaald door Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Veilig**: Dit is het veiligste niveau. Het apparaat heeft geen toegang tot bedrijfsresources als er ook maar één bedreiging is gevonden. Als er bedreigingen worden gevonden, wordt het apparaat geëvalueerd als niet-compatibel. (Microsoft Defender ATP gebruikt de waarde *Veilig*.)
   - **Laag**: Het apparaat is conform als er alleen bedreigingen van een laag niveau aanwezig zijn. Apparaten met een gemiddeld of hoog dreigingsniveau zijn niet conform.
   - **Gemiddeld**: Het apparaat is conform als de bedreigingen op het apparaat van laag of gemiddeld niveau zijn. Als er bedreigingen van hoog niveau worden aangetroffen, wordt het apparaat als niet-compatibel beoordeeld.
   - **Hoog**: Dit niveau is het minst veilig en laat alle bedreigingsniveaus toe. Apparaten met een hoog, gemiddeld of laag bedreigingsniveau worden daarom beschouwd als conform.

6. Voltooi de configuratie van het beleid, inclusief toewijzing van het beleid aan toepasselijke groepen.

## <a name="configure-web-protection-on-devices-that-run-android"></a>Webbeveiliging configureren op apparaten met Android

Microsoft Defender ATP voor Android bevat standaard het onderdeel webbeveiliging en schakelt dit in. [Webbeveiliging](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) helpt bij het beveiligen van apparaten tegen webbedreigingen en beschermt gebruikers tegen phishing-aanvallen.

Hoewel deze optie standaard is ingeschakeld, zijn er geldige redenen om deze beveiliging op sommige Android-apparaten uit te schakelen. U kunt er bijvoorbeeld voor kiezen om alleen de scanfunctie van de Microsoft Defender ATP-app te gebruiken of om te voorkomen dat webbeveiliging gebruikmaakt van uw VPN tijdens het scannen op schadelijke URL's.

Intune ondersteunt het uitschakelen van de gehele of gedeeltelijke webbeveiligingsfunctie. De methode die u gebruikt en de mogelijkheden die u kunt uitschakelen, zijn afhankelijk van hoe het Android-apparaat is ingeschreven bij Intune:

- **Android-apparaatbeheerder**: Gebruik een configuratieprofiel om aangepaste OMA-URI-instellingen op het apparaat in te stellen om de gehele webbeveiligingsfunctie uit te schakelen of alleen het gebruik van VPN's uit te schakelen. Zie voor algemene informatie over aangepaste instellingen voor Android-toestellen [Aangepaste instellingen](../configuration/custom-settings-android.md).

- **Werkprofiel voor Android Enterprise**: Gebruik een app-configuratieprofiel en de *configuratieontwerper* om webbeveiliging uit te schakelen. Deze methode en het inschrijvingstype ondersteunen het uitschakelen van alle webbeveiligingsopties, maar ondersteunen niet het uitschakelen van alleen het gebruik van VPN's. Zie [De configuratieontwerper gebruiken](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer) voor algemene informatie over app-configuratiebeleidsregels.

Als u webbeveiliging op apparaten wilt configureren, gebruikt u de volgende procedures om de toepasselijke configuratie te maken en te implementeren.

### <a name="disable-web-protection-for-android-device-administrator"></a>Webbeveiliging voor Android-apparaatbeheerder uitschakelen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Voer de volgende instellingen in:

   - **Platform**: Selecteer **Android-apparaatbeheerder**
   - **Profiel**: Selecteer **Aangepast**

   Selecteer **Maken**.

4. Voer de volgende gegevens in onder **Basisinformatie**:

   - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Bijvoorbeeld *aangepast Android-profiel voor Microsoft Defender ATP-webbeveiliging*
   - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

5. Selecteer in **Configuratie-instellingen** de optie **Toevoegen**.

   Geef de instellingen op voor de configuratie die u wilt implementeren:

   - **Webbeveiliging uitschakelen**:
     - **Naam**: Voer een unieke naam in voor deze OMA-URI-instelling, zodat u deze gemakkelijk kunt vinden. Bijvoorbeeld *Microsoft Defender ATP-webbeveiliging uitschakelen*
     - **Beschrijving**: (Optioneel) Voer een beschrijving in met een overzicht van de instelling en eventuele andere belangrijke details.
     - **OMA-URI**: Voer **./Vendor/MSFT/DefenderATP/AntiPhishing** in
     - **Gegevenstype**: Selecteer in de vervolgkeuzelijst **Geheel getal**
     - **Waarde**: Voer **0** in om webbeveiliging uit te schakelen, inclusief de op VPN gebaseerde scan.
       > [!NOTE]
       > Voer **1** in om webbeveiliging in te schakelen. Dit is de standaardinstelling voor webbeveiliging.

   - **Schakel alleen het gebruik van VPN via webbeveiliging uit**:
     - **Naam**: Voer een unieke naam in voor deze OMA-URI-instelling, zodat u deze gemakkelijk kunt vinden. Bijvoorbeeld *Microsoft Defender ATP-webbeveiliging VPN uitschakelen*
     - **Beschrijving**: (Optioneel) Voer een beschrijving in met een overzicht van de instelling en eventuele andere belangrijke details.
     - **OMA-URI**: Voer **./Vendor/MSFT/DefenderATP/Vpn** in
     - **Gegevenstype**: Selecteer in de vervolgkeuzelijst **Geheel getal**
     - **Waarde**: Voer **0** in om de op VPN gebaseerde scan uit te schakelen.
       > [!NOTE]
       > Voer **1** in om webbeveiliging in te schakelen. Dit is de standaardinstelling voor webbeveiliging.

   Selecteer **Toevoegen** om de configuratie van de OMA-URI-instellingen op te slaan en selecteer vervolgens **Volgende** om door te gaan.

6. Geef op de pagina **Toewijzingen** de groepen op die dit profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

7. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Webbeveiliging voor Android Enterprise-werkprofiel uitschakelen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apps** > **App-configuratiebeleid** > **Toevoegen** en Beheerde apparaten.

3. Voer de volgende gegevens in onder **Basisinformatie**:

   - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Bijvoorbeeld *Android-app-configuratie voor Microsoft Defender ATP-webbeveiliging*.
   - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.
   - **Platform**: Selecteer **Android Enterprise**
   - **Profieltype**: Selecteer **Alleen werkprofiel**
   - **Beoogde app**: Klik op **App selecteren**.

4. Zoek onder **Gekoppelde app** en selecteer **Defender ATP** en klik op **OK** > **Volgende**.

5. Selecteer onder **Instellingen** in de vervolgkeuzelijst **Indeling van de configuratie-instellingen** de optie **Configuratieontwerper gebruiken** en klik op **Toevoegen**. De JSON-editor wordt geopend.

6. Zoek en selecteer **Webbeveiliging** en selecteer **OK** om terug te gaan naar de pagina **Instellingen**.

7. Voer voor de **configuratiewaarde** **0** in om webbeveiliging uit te schakelen.

   > [!NOTE]
   > Voer **1** in om webbeveiliging in te schakelen. Dit is de standaardinstelling voor webbeveiliging.

   Selecteer **Volgende** om door te gaan.

8. Geef op de pagina **Toewijzingen** de groepen op die dit profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

9. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

## <a name="create-a-conditional-access-policy"></a>Beleid voor voorwaardelijke toegang maken

Voorwaardelijk toegangsbeleid kan gegevens van Microsoft Defender ATP gebruiken om de toegang tot resources te blokkeren voor apparaten die het door u ingestelde dreigingsniveau overschrijden. U kunt de toegang van het apparaat tot bedrijfsresources zoals SharePoint of Exchange Online blokkeren.

> [!TIP]
> Voorwaardelijke toegang is een technologie van Azure Active Directory (Azure AD). Het knooppunt voor *voorwaardelijke toegang* dat in het Microsoft Endpoint Manager-beheercentrum is gevonden, is het knooppunt van *Azure AD*.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Eindpuntbeveiliging** > **Voorwaardelijke toegang** > **Nieuw beleid**.

3. Voer een **Naam** voor het beleid in en selecteer **Gebruikers en groepen**. Gebruik de opties Opnemen of Uitsluiten om uw groepen voor het beleid toe te voegen en selecteer **Klaar**.

4. Selecteer **Cloud-apps** en kies welke apps u wilt beveiligen. Kies bijvoorbeeld **Apps selecteren** en selecteer **Office 365 SharePoint Online** en **Office 365 Exchange Online**.

   Selecteer **OK** om uw wijzigingen op te slaan.

5. Selecteer **Voorwaarden** > **Client-apps** om het beleid toe te passen op apps en browsers. Selecteer bijvoorbeeld **Ja** en schakel vervolgens **Browser** en **Mobiele apps en bureaublad-clients** in.

   Selecteer **OK** om uw wijzigingen op te slaan.

6. Selecteer **Verlenen** om voorwaardelijke toegang toe te passen op basis van de apparaatcompatibiliteit. Selecteer bijvoorbeeld **Toegang verlenen** > **Vereisen dat apparaat wordt gemarkeerd als conform**.

    Kies **Selecteren** om uw wijzigingen op te slaan.

7. Selecteer **Beleid inschakelen** en vervolgens **Maken** om uw wijzigingen op te slaan.

## <a name="monitor-device-compliance"></a>Apparaatcompatibiliteit bewaken

Bewaak vervolgens de status van apparaten die het nalevingsbeleid voor Microsoft Defender ATP hebben.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Bewaken** > **Beleidsnaleving**.

3. Zoek uw Microsoft Defender ATP-beleid in de lijst op en ga na welke apparaten conform of non-conform zijn.

U kunt vanaf dezelfde locatie ook het *operationele* rapport gebruiken voor niet-compatibele apparaten:

1. Selecteer **Apparaten** > **Bewaken** > **Niet-compatibele apparaten**.

Zie [Intune-rapporten](../fundamentals/reports.md) voor meer informatie over rapporten.

## <a name="view-onboarding-status"></a>Status voor onboarding weergeven

Als u de status voor onboarding van alle door Intune beheerde apparaten wilt weergeven, gaat u naar **Eindpuntbeveiliging** > **Microsoft Defender ATP**. Op deze pagina kunt u ook een apparaatconfiguratieprofiel maken om meer apparaten naar Microsoft Defender ATP te onboarden.

## <a name="next-steps"></a>Volgende stappen

[Voorwaardelijke toegang van Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)

[Microsoft Defender ATP-risicodashboard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

[Gebruik beveiligingstaken in combinatie met kwetsbaarheidsbeheer in ATP om problemen op apparaten op te lossen](atp-manage-vulnerabilities.md).

[Aan de slag met apparaatnalevingsbeleid](device-compliance-get-started.md)

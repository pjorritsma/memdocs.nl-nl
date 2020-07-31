---
title: Microsoft Defender ATP configureren in Microsoft Intune - Azure | Microsoft Docs
description: Configureer Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) in Intune, waaronder het maken van verbinding met ATP, het voorbereiden van apparaten, het toewijzen van nalevingsbeleid aan risiconiveaus, en het instellen van beleidsregels voor voorwaardelijke toegang.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e19315f07d803e2aab53b3724fde85f1975c0c5
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264525"
---
# <a name="configure-microsoft-defender-atp-in-intune"></a>Microsoft Defender ATP configureren in Intune

Met de informatie en procedures in dit artikel kunt u de integratie van Microsoft Defender ATP met Intune configureren. De configuratie bevat de volgende algemene stappen:

- Microsoft Defender ATP inschakelen voor uw tenant
- Onboarding van apparaten waarop Windows en Android worden uitgevoerd
- Nalevingsbeleid gebruiken om risiconiveaus voor apparaten in te stellen
- Beleidsregels voor voorwaardelijke toegang gebruiken om apparaten die de verwachte risiconiveaus overschrijden, te blokkeren

Voordat u begint, moet uw omgeving voldoen aan de [vereisten](../protect/advanced-threat-protection.md#prerequisites) voor het gebruik van Microsoft Defender ATP met Intune.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Microsoft Defender ATP in Intune inschakelen

De eerste stap is het instellen van een service-naar-service-verbinding tussen Intune en Microsoft Defender ATP. Voor het instellen moet u beheerdersrechten hebben voor zowel Microsoft Defender Security Center als voor Intune.

U hoeft Microsoft Defender ATP slechts één keer per tenant in te schakelen.

### <a name="to-enable-microsoft-defender-atp"></a>Microsoft Defender ATP inschakelen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Eindpuntbeveiliging** > **Microsoft Defender ATP**en vervolgens **Het Microsoft Defender-beveiligingscentrum openen**.

   ![Selecteren om het Microsoft Defender Security Center te openen](./media/advanced-threat-protection-configure/atp-device-compliance-open-microsoft-defender.png)

3. In **Microsoft Defender Security Center**:
   1. Selecteer **Instellingen** > **Geavanceerde functies**.
   2. Voor **Microsoft Intune-verbinding**, kiest u **Aan**:

      ![De verbinding met Intune inschakelen](./media/advanced-threat-protection-configure/atp-security-center-intune-toggle.png)

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

## <a name="onboard-devices"></a>Onboarding van apparaten

Wanneer u ondersteuning voor Microsoft Defender ATP in Intune hebt ingeschakeld, stelt u een service-naar-service-verbinding in tussen Intune en Microsoft Defender ATP. U kunt de apparaten die u met Intune beheert, vervolgens onboarden naar Microsoft Defender ATP, waarmee u gegevens over de risiconiveaus van het apparaat kunt verzamelen.

### <a name="onboard-windows-devices"></a>Onboarding van Windows-apparaten

Toen u de verbinding tussen Intune en Microsoft Defender ATP tot stand bracht, heeft Intune van Microsoft Defender ATP een configuratiepakket voor onboarding ontvangen. U implementeert dit configuratiepakket op uw Windows-apparaten met een apparaatconfiguratieprofiel voor Microsoft Defender ATP.

Het configuratiepakket configureert apparaten zodanig dat ze communiceren met [Microsoft Defender ATP-services](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) om bestanden te scannen en bedreigingen te detecteren. Het apparaat wordt ook geconfigureerd om het risiconiveau van apparaten te rapporteren aan Microsoft Defender ATP op basis van nalevingsbeleid dat u maakt.

Wanneer u onboarding van een apparaat met het configuratiepakket eenmaal hebt uitgevoerd, hoeft u dit niet opnieuw te doen. U kunt apparaten onboarden met behulp van een [groepsbeleid of Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile-to-onboard-windows-devices"></a>Het configuratieprofiel van het apparaat maken om Windows-apparaten te onboarden

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

### <a name="onboard-android-devices"></a>Android-apparaten onboarden

Nadat u de service-naar-serviceverbinding tussen Intune en Microsoft Defender ATP tot stand hebt gebracht, kunt u Android-apparaten onboarden in Microsoft Defender ATP. Met de onboarding worden apparaten geconfigureerd om te communiceren met Defender ATP, waarna er gegevens over het risiconiveau van de apparaten worden verzameld.

In tegenstelling tot Windows-apparaten is er geen configuratiepakket voor apparaten waarop Android wordt uitgevoerd. Raadpleeg [Overzicht van Microsoft Defender ATP voor Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) in de ATP-documentatie van Microsoft Defender voor vereisten en instructies voor onboarding voor Android.

Voor apparaten met Android kunt u ook Intune-beleid gebruiken om Microsoft Defender ATP op Android te wijzigen. Raadpleeg [Webbeveiliging van Microsoft Defender ATP](../protect/advanced-threat-protection-manage-android.md) voor meer informatie.

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

## <a name="next-steps"></a>Volgende stappen

- [Microsoft Defender ATP-instellingen configureren in Android](../protect/advanced-threat-protection-manage-android.md)
- [Naleving van risiconiveaus bewaken](../protect/advanced-threat-protection-monitor.md)

Meer informatie vindt u in de Intune-documentatie:

- [Beveiligingstaken gebruiken in combinatie met kwetsbaarheidsbeheer in ATP om problemen op apparaten op te lossen](atp-manage-vulnerabilities.md)
- [Aan de slag met apparaatnalevingsbeleid](device-compliance-get-started.md)

Meer informatie vindt u in de Microsoft Defender ATP-documentatie:

- [Voorwaardelijke toegang van Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP-risicodashboard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

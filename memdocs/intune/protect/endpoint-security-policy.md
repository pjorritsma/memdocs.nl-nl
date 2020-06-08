---
title: Eindpuntbeveiligingsbeleid beheren in Microsoft Intune | Microsoft Docs
description: Meer informatie over hoe beveiligingsbeheerders de eindpuntbeveiligingsbeleidsregels en-profielen kunnen gebruiken om zich te richten op de beveiligingsconfiguratie van apparaten in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 9c2e6f742610eb8f2f526c6fc7a5afabfbadcbbf
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990867"
---
# <a name="manage-device-security-with-endpoint-security-policies-in-microsoft-intune"></a>Beveiliging van apparaten beheren met eindpuntbeveiligingsbeleid in Microsoft Intune

Als beveiligingsbeheerder kunt u het beveiligingsbeleid van de *eindpuntbeveiliging* van Intune gebruiken voor het configureren van de beveiliging van apparaten zonder de overhead om te moeten navigeren door het hoofdgedeelte en een breed scala aan instellingen die u in de configuratieprofielen en beveiligingsbasislijnen voor apparaten aantreft.

Elk beleidstype ondersteunt een of meer profielen. Met profielen kunt u instellingen configureren en instellingen groeperen voor verschillende platforms of voor verschillende aandachtsgebieden in het grotere beleidsterrein.

U vindt deze beleidsregels onder *Beheren* in het knooppunt **Eindpuntbeveiliging** van het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

![Beleid beheren](./media/endpoint-security-policy/endpoint-security-policies.png)

Hieronder vindt u een korte beschrijving van elk type eindpuntbeveiligingsbeleid. Als u hierover meer informatie wilt, met inbegrip van de voor elk type beschikbare profielen, kunt u de koppelingen volgen naar inhoud die is gewijd aan elk beleidstype:

- [Antivirus](../protect/endpoint-security-antivirus-policy.md): met antivirusbeleid kunnen beveiligingsbeheerders zich richten op het beheren van de afzonderlijke groep antivirusinstellingen voor beheerde apparaten. U kunt Intune integreren met Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) als Mobile Threat Defense-oplossing.

- [Schijfversleuteling](../protect/endpoint-security-disk-encryption-policy.md): de schijfversleutelingsprofielen voor eindpuntbeveiliging zijn alleen gericht op de instellingen die relevant zijn voor een ingebouwde versleutelingsmethode voor apparaten, zoals FileVault of BitLocker. Op deze manier kunnen beveiligingsbeheerders de instellingen voor schijfversleuteling eenvoudig beheren zonder door een massa niet-gerelateerde instellingen te hoeven navigeren.

- [Firewall](../protect/endpoint-security-firewall-policy.md): gebruik het firewallbeleid voor eindpuntbeveiliging in Intune om een in apparaten ingebouwde firewall te configureren voor apparaten met macOS en Windows 10. Ingebouwde firewalls zijn onder andere BitLocker voor Windows-apparaten en FileVault voor macOS.

- [Eindpuntdetectie en -respons](../protect/endpoint-security-edr-policy.md): wanneer u Microsoft Defender Advanced Threat Protection (Defender ATP) integreert met Intune, kunt u eindpuntbeveiligingsbeleid gebruiken voor eindpuntdetectie en-respons (EDR) voor het beheren van de EDR-instellingen en de onboarding van apparaten naar Defender ATP.

- [Kwetsbaarheid voor aanvallen verminderen](../protect/endpoint-security-asr-policy.md): wanneer Defender-antivirus wordt gebruikt op uw Windows 10-apparaten, gebruikt u Intune-eindpuntbeveiligingsbeleid voor het verminderen van de kwetsbaarheid voor aanvallen om die instellingen voor uw apparaten te beheren.

- [Accountbeveiliging](../protect/endpoint-security-account-protection-policy.md): met accountbeveiligingsbeleid kunt u de identiteit en accounts van uw gebruikers beschermen. Het accountbeveiligingsbeleid is gericht op instellingen voor Windows Hello en Credential Guard, dat deel uitmaakt van de Windows-functionaliteit voor identiteits- en toegangsbeheer.

De volgende secties zijn van toepassing op al het eindpuntbeveiligingsbeleid.

## <a name="create-an-endpoint-security-policy"></a>Een eindpuntbeveiligingsbeleid maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Eindpuntbeveiliging** en selecteer vervolgens het typebeleid dat u wilt configureren. Selecteer daarna **Beleid maken**. Kies uit de volgende beleidstypen:
   - Antivirus
   - Schijfversleuteling
   - Firewall
   - Eindpuntdetectie en -respons
   - Kwetsbaarheid voor aanvallen verminderen
   - Accountbeveiliging

3. Voer de volgende eigenschappen in:
   - **Platform**: Kies het platform waarvoor u beleid wilt maken. De beschikbare opties zijn afhankelijk van het door u geselecteerde type:
     - macOS
     - Windows 10 en hoger
   - **Profiel**: Kies uit de beschikbare profielen voor het platform dat u hebt geselecteerd. Zie de betreffende sectie in dit artikel voor het beleidstype dat u hebt gekozen voor meer informatie over de profielen.

4. Selecteer **Maken**.

5. Voer op de pagina **Basisinformatie** een naam en een beschrijving in voor het profiel en selecteer dan **Volgende**.

6. Vouw elke groep instellingen op de pagina **Configuratie-instellingen** uit en configureer de instellingen die u met dit profiel wilt beheren.

   Wanneer u klaar bent met het configureren van instellingen, selecteert u **Volgende**.

7. Selecteer op de pagina **Bereiktags** de optie **Bereiktags selecteren** om het deelvenster *Tags selecteren* te openen en bereiktags aan het profiel toe te wijzen.
  
   Selecteer **Volgende** om door te gaan.

8. Selecteer op de pagina **Toewijzingen** de groepen die dit profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

   Selecteer **Volgende**.

9. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

## <a name="duplicate-a-policy"></a>Een beleid dupliceren

Eindpuntbeveiligingsbeleid biedt ondersteuning voor duplicatie, waarmee u een kopie van het oorspronkelijke beleid kunt maken. Een scenario voor het dupliceren van een beleid is handig als u gelijksoortige beleidsregels aan verschillende groepen wilt toewijzen, maar niet handmatig het hele beleid opnieuw wilt maken. In plaats daarvan kunt u het oorspronkelijke beleid dupliceren en vervolgens alleen de wijzigingen introduceren die voor het nieuwe beleid nodig zijn. U kunt alleen een specifieke instelling wijzigen en de groep waaraan het beleid is toegewezen.

Wanneer u een duplicaat maakt, geeft u de kopie een nieuwe naam. De kopie wordt gemaakt met dezelfde instellingsconfiguraties en bereiktags als de het oorspronkelijke beleid, maar bevat geen toewijzingen. U moet het nieuwe beleid later bewerken voor het maken van toewijzingen.  

De volgende beleidstypen ondersteunen duplicatie:

- Antivirus
- Schijfversleuteling
- Firewall
- Eindpuntdetectie en -respons
- Kwetsbaarheid voor aanvallen verminderen
- Accountbeveiliging

Nadat u het nieuwe beleid hebt gemaakt, controleert en bewerkt u het beleid om wijzigingen in de configuratie aan te brengen.

### <a name="to-duplicate-a-policy"></a>Een beleid dupliceren

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer het beleid dat u wilt kopiëren. Selecteer vervolgens **Dupliceren** of selecteer het beletselteken ( **...** ) rechts van het beleid en selecteer **Dupliceren**.
3. Geef een **nieuwe naam** op voor het beleid en selecteer vervolgens **Opslaan**.

### <a name="to-edit-a-policy"></a>Een beleid bewerken

1. Selecteer het nieuwe beleid en selecteer vervolgens **Eigenschappen**.
2. Selecteer Instellingen om een lijst met configuratie-instellingen in het beleid uit te vouwen. U kunt de instellingen in deze weergave niet wijzigen, maar u kunt controleren hoe ze zijn geconfigureerd.
3. Als u het beleid wilt wijzigen, selecteert u **Bewerken** voor elke categorie waarvoor u een wijziging wilt aanbrengen:
   - Basisbeginselen
   - Toewijzingen
   - Bereiktags
   - Configuratie-instellingen
4. Nadat u wijzigingen hebt aangebracht, selecteert u **Opslaan** om uw bewerkingen op te slaan.  Bewerkingen van één categorie moeten worden opgeslagen voordat u bewerkingen kunt aanbrengen in andere categorieën.

## <a name="manage-conflicts"></a>Conflicten beheren

Veel van de apparaatinstellingen die u kunt beheren met eindpuntbeveiligingsbeleid (beveiligingsbeleid) kunt u via andere beleidstypen beheren in Intune. Deze andere beleidstypen zijn onder meer het beleid voor *apparaatconfiguratie* en *beveiligingsbasislijnen*. Omdat u een instelling met verschillende beleidstypen of meerdere exemplaren van hetzelfde beleidstype kunt beheren, moet u voorbereid zijn om beleidsconflicten te identificeren en op te lossen als een apparaat niet naar verwachting voldoet aan de configuraties.

- Beveiligingsbasislijnen kunnen een niet-standaardwaarde instellen voor een instelling om te voldoen aan de aanbevolen configuratie die deze basislijn behandelt.
- Voor andere beleidstypen, met inbegrip van het eindpuntbeveiligingsbeleid, wordt standaard een waarde ingesteld van *Niet geconfigureerd*. Voor deze andere beleidstypen moet u instellingen expliciet configureren in het beleid.

Ongeacht de beleidsmethode kan het beheer van dezelfde instelling op hetzelfde apparaat via meerdere beleidstypen of via meerdere instanties van hetzelfde beleidstype mogelijk tot conflicten leiden die u beter kunt vermijden.

De informatie in de volgende koppelingen kan u helpen om conflicten vast te stellen en op te lossen:

- [Beleidsregels en profielen voor het oplossen van problemen in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Uw beveiligingsbasislijnen bewaken](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Volgende stappen

[Eindpuntbeveiliging in Intune beheren](../protect/endpoint-security.md)

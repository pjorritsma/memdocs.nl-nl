---
title: Apparaten met eindpuntbeveiliging beheren in Microsoft Intune | Microsoft Docs
description: Meer informatie over hoe beveiligingsbeheerders het knooppunt eindpuntbeveiliging kunnen gebruiken om apparaten weer te geven en wat ze kunnen doen om ze te beheren in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 98b1380254a784dfe8939c607ab574f7bdaa8752
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914987"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>Apparaten met eindpuntbeveiliging beheren in Microsoft Intune

Als beveiligingsbeheerder gebruikt u de weergave *Alle apparaten* in het Beheercentrum van Microsoft Endpoint Manager om uw apparaten te controleren en te beheren. In de weergave wordt een lijst weergegeven met alle apparaten uit uw Azure Active Directory (Azure AD). Dit omvat apparaten die worden beheerd door Intune, Configuration Manager en via [co-beheer](/configmgr/comanage/overview) door zowel Intune als Configuration Manager. Apparaten kunnen zich in de cloud en in uw on-premises infrastructuur bevinden wanneer deze zijn geïntegreerd met uw Azure AD.

 Als u de weergave wilt vinden, opent u het [Beheercentrum voor Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) en selecteert u **Eindpuntbeveiliging** > **Alle apparaten**.

De eerste weergave *Alle apparaten* geeft uw apparaten weer en bevat informatie over de belangrijkste gegevens:

- Hoe het apparaat wordt beheerd
- Status van naleving
- Gegevens van het besturingssysteem
- Wnneer het apparaat voor het laatst heeft ingecheckt
- En meer

![Weergave van alle apparaten in het beheercentrum](./media/endpoint-security-manage-devices/all-device-view.png)

Bij het weergeven van de details van het apparaat kunt u een apparaat selecteren om in te zoomen voor meer informatie.

## <a name="available-details-by-management-type"></a>Beschikbare details per beheertype

Wanneer u apparaten bekijkt in het Beheercentrum van Microsoft Endpoint Manager, moet u nagaan hoe het apparaat wordt beheerd. De beheerbron heeft invloed op de informatie die wordt weergegeven in het beheercentrum en de acties die beschikbaar zijn voor het beheren van het apparaat.

Overweeg de volgende velden:

- **Beheerd door**: deze kolom geeft aan hoe het apparaat wordt beheerd. Beheerd door-opties zijn onder andere:

  - **MDM**: deze apparaten worden beheerd met Intune. Compatibiliteitsgegevens worden verzameld en door Intune gerapporteerd aan het beheercentrum.

  - **ConfigMgr**: deze apparaten worden weergegeven in het Beheercentrum van Microsoft Endpoint Manager wanneer u gebruikmaakt van *tenant koppelen* om de apparaten toe te voegen die u met Configuration Manager beheert. Om te worden beheerd, moet het apparaat de Configuration Manager-client uitvoeren en de volgende kenmerken hebben:

    - In een Werkgroep (AAD-deelname en anderszins)
    - Domein toegevoegd
    - Hybrid AAD-deelname (gekoppeld aan de AD en AAD)

    De nalevingsstatus voor apparaten die worden beheerd door Configuration Manager is niet zichtbaar in het beheercentrum van Microsoft Endpoint Manager.

    Raadpleeg de Configuration Manager-documentatie [Tenant koppelen inschakelen](/configmgr/tenant-attach/device-sync-actions) voor meer informatie.

  - **MDM/ConfigMgr-agent**: deze apparaten staan onder co-beheer tussen Intune en Configuration Manager.

    Met co-beheer kiest u [verschillende workloads in co-beheer](/configmgr/comanage/how-to-switch-workloads) om te bepalen welke aspecten door Configuration Manager of door Intune worden beheerd. Deze opties zijn van invloed op het beleid dat op het apparaat van toepassing is, en hoe compatibiliteitsgegevens worden gerapporteerd aan het beheercentrum.

    U kunt bijvoorbeeld Intune gebruiken voor het configureren van een beleid voor antivirus, firewall en versleuteling. Deze beleidstypen worden beschouwd als beleid voor het *Endpoint Protection*. Als u wilt dat een co-beheerd apparaat het Intune-beleid gebruikt en niet het Configuration Manager-beleid, stelt u de schuifregelaar voor co-beheer voor Endpoint Protection in op *Intune-* of *Pilot Intune*. Als de schuifregelaar is ingesteld op Configuration Manager, gebruikt het apparaat het beleid en de instellingen van Configuration Manager.

- **Naleving**: Naleving wordt geëvalueerd op basis van het nalevingsbeleid dat aan het apparaat is toegewezen. De bron van deze beleidsregels en welke informatie zich in de console bevindt, is afhankelijk van hoe het apparaat wordt beheerd. Intune, Configuration Manager of co-beheer. Stel de schuifregelaar voor co-beheer in voor de naleving van de compatibiliteit van apparaten met Intune of Pilot Intune zodat co-beheerde apparaten naleving rapporteren.  

  Nadat de naleving is gerapporteerd aan het beheercentrum voor een apparaat, kunt u inzoomen op de details om meer details weer te geven. Wanneer een apparaat niet voldoet aan het beleid, kunt u inzoomen op de details om informatie weer te geven over welke beleidsregels niet compatibel zijn. Deze informatie kan u helpen bij het onderzoeken en u helpen om het apparaat compatibel te maken.

- **Laatste check-in**: Dit veld identificeert de laatste keer dat het apparaat de status heeft gerapporteerd.

## <a name="review-a-devices-policy"></a>Een beleid voor apparaten controleren

Bij het weergeven van de lijst met apparaten kunt u een apparaat selecteren waarop u wilt inzoomen voor meer informatie hierover door de pagina *Overzicht* van dat apparaat te openen.

Op de pagina Overzicht van een apparaat kunt u vervolgens **eindpuntbeveiligingsconfiguratie** selecteren om de beleidsregels voor eindpuntbeveiligings weer te geven die van toepassing zijn op dat apparaat. Er zijn beleidsdetails beschikbaar voor apparaten die worden beheerd door MDM en Intune.

![Details over eindpuntbeveiligingsbeleid weergeven](./media/endpoint-security-manage-devices/view-policy-details.png)

Voor apparaten die worden beheerd door Configuration Manager worden geen beleidsdetails weergegeven. Als u meer informatie over deze apparaten wilt weergeven, gebruikt u de Configuration Manager-console.

## <a name="remote-actions-for-devices"></a>Externe acties voor apparaten

Externe acties zijn acties die u kunt starten of toepassen op een apparaat vanuit het beheercentrum van Microsoft Endpoint Manager. Wanneer u details voor een apparaat bekijkt, hebt u toegang tot externe acties die van toepassing zijn op het apparaat.

Externe acties worden weergegeven aan de bovenkant van de pagina *Overzicht* van het apparaat. Acties die niet kunnen worden weergegeven vanwege een beperkte ruimte op het scherm, zijn beschikbaar door het ellipsteken aan de rechterkant te selecteren:

![Aanvullende acties weergeven](./media/endpoint-security-manage-devices/view-additional-actions.png)

De externe acties die beschikbaar zijn, zijn afhankelijk van de manier waarop het apparaat wordt beheerd:

- **Intune**: Alle [externe acties van Intune](../remote-actions/device-management.md) die van toepassing zijn op het platform van het apparaat, zijn beschikbaar.  
- **Configuration Manager**: U kunt de volgende Configuration Manager-acties gebruiken:

  - Computerbeleid synchroniseren
  - Gebruikersbeleid synchroniseren
  - App-evaluatiecyclus

- **Co-beheer**: U kunt zowel externe acties van Intune als Configuration Manager-acties gebruiken.

Sommige externe acties van Intune kunnen helpen bij het beveiligen van apparaten of het beveiligen van gegevens die zich op het apparaat bevinden. Met externe acties kunt u het volgende doen:

- Een apparaat vergrendelen
- Instellingen terugzetten op een apparaat
- Bedrijfsgegevens verwijderen
- Controleren op malware buiten een geplande uitvoering
- BitLocker-sleutels draaien

De volgende externe acties van Intune zijn van belang voor de beveiligingsbeheerder en zijn een subset van de [volledige lijst](../remote-actions/device-inventory.md#view-the-device-details). Niet alle acties zijn beschikbaar voor alle apparaatplatforms. De koppelingen gaan naar inhoud die gedetailleerde informatie bevat voor elke actie.

- [Apparaat synchroniseren](../remote-actions/device-sync.md): laat het apparaat direct inchecken bij Intune. Wanneer een apparaat wordt ingecheckt, worden eventuele openstaande acties of toegewezen beleidsregels ontvangen die erop zijn toegepast.  

- [Opnieuw opstarten](../remote-actions/device-restart.md): u kunt een Windows 10-apparaat geforceerd opnieuw opstarten binnen vijf minuten. De eigenaar van het apparaat wordt niet automatisch op de hoogte gesteld dat het apparaat opnieuw wordt opgestart. Hierdoor kan eventueel werk verloren gaan.

- [Snelle scan](../configuration/device-restrictions-windows-10.md): laat Defender een snelle scan uitvoeren op het apparaat voor malware en verzend de resultaten vervolgens naar Intune. Een snelle scan bekijkt de gebruikelijke locaties waar malware kan zijn geregistreerd worden bekeken, zoals registersleutels en bekende opstartmappen in Windows.

- [Volledige scan](../configuration/device-restrictions-windows-10.md): laat Defender een scan uitvoeren op het apparaat voor malware en verzend de resultaten vervolgens naar Intune. Een volledige scan bekijkt de gebruikelijke locaties waar malware kan zijn geregistreerd worden bekeken en alle mappen en bestanden op het apparaat worden gescand.

- Beveiligingsinformatie van Windows Defender bijwerken: laat het apparaat de malware-definities voor Microsoft Defender Antivirus bijwerken. Met deze actie wordt geen scan gestart.

- [Sleutelrotatie van BitLocker](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key): u kunt een Intune-apparaatactie gebruiken om de BitLocker-herstelsleutel van een apparaat met Windows 10 versie 1909 of hoger op afstand te roteren.

U kunt ook **Bulkacties voor apparaat** gebruiken om bepaalde acties te beheren, zoals *Buiten gebruik stellen* en *Wissen* voor meerdere apparaten tegelijk. [Bulkacties](../remote-actions/bulk-device-actions.md) zijn beschikbaar via de weergave *Alle apparaten*. U selecteert het platform, de actie en vervolgens geeft u maximaal 100 apparaten op.

![Bulkacties selecteren](./media/endpoint-security-manage-devices/select-bulk-actions.png)

De opties die u beheert voor apparaten, worden pas van kracht nadat het apparaat is ingecheckt met Intune.

## <a name="next-steps"></a>Volgende stappen

[Eindpuntbeveiliging in Intune beheren](../protect/endpoint-security.md)
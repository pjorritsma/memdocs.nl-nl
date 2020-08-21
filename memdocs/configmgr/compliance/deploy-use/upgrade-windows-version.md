---
title: Windows-apparaten upgraden naar een andere versie
titleSuffix: Configuration Manager
description: Gebruik Configuration Manager om Windows 10-apparaten automatisch te upgraden naar een andere Windows-editie.
ms.date: 07/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 920f3c9aabcdec1242a6f5e5fc8e6b65c5cc0b53
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694607"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>Windows-apparaten upgraden naar een nieuwe versie met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met het **beleid voor editie-upgrades** kunt u Windows 10-apparaten automatisch bijwerken naar een andere editie.

De volgende upgradepaden worden ondersteund:

- Van Windows 10 Pro naar Windows 10 Enterprise
- Van Windows 10 Home naar Windows 10 Education
- Van Windows 10 Mobile naar Windows 10 Mobile Enterprise

Op de apparaten moet de Configuration Manager-client software worden uitgevoerd. Apparaten die worden beheerd door [on-premises MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) , worden niet ondersteund.

## <a name="before-you-start"></a>Voordat u begint

Voordat u begint met het upgraden van apparaten naar de nieuwste versie, controleert u de volgende vereisten:  

- Voor desktop-edities van Windows 10: een geldige product code voor de nieuwe versie van Windows op alle apparaten waarop het beleid is gericht. Deze product code kan een meervoudige activerings code (MAK) of een algemene volume licentie code (GVLK) zijn. Een GVLK wordt ook wel een configuratie sleutel voor de KMS-client (Key Management service) genoemd. Zie [volume activering plannen](/windows/deployment/volume-activation/plan-for-volume-activation-client)voor meer informatie. Zie [bijlage a](/windows-server/get-started/kmsclientkeys) van de Windows Server-activerings handleiding voor een lijst met installatie sleutels voor KMS-clients. <!--496871-->  

- Voor Windows 10 Mobile: een XML-licentie bestand van de Microsoft Volume Licensing Service Center (VLSC). Dit bestand bevat de licentie gegevens voor de nieuwe versie van Windows op alle apparaten waarop het beleid is gericht. Down load het ISO-bestand voor **Windows 10 Mobile Enter prise**, dat de licentie-XML bevat.<!-- SCCMDocs#2033 -->

- Als u dit beleids type wilt beheren, moet u de beveiligingsrol **volledige beheerder** Configuration Manager hebben.

## <a name="configure-the-policy"></a>Het beleid configureren  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit en selecteer het knoop punt upgrade van  **Windows 10-editie** .  

2. Selecteer **editie-upgrade beleid maken**op het tabblad **Start** van het lint in de groep **maken** .  

3. Selecteer **beleid maken**.  

4. Geef op de pagina **Algemeen** van de **Wizard Editie-upgradebeleid maken**de volgende informatie op:  

    - **Naam** : Voer een naam in voor het beleid voor editie-upgrades  

    - **Beschrijving** (optioneel): Voer desgewenst een beschrijving in voor het beleid waarmee u het kunt herkennen in de Configuration Manager-console  

    - **SKU om het apparaat bij te werken naar** : Selecteer in de vervolg keuzelijst de doel editie van Windows 10 Desktop of Windows 10 Mobile  

    - **Licentie gegevens** -Selecteer een van de volgende opties:  

        - **Product code** : Voer een geldige product code in voor de doel computer met Windows 10 Desktop Edition  

            > [!NOTE]  
            > Nadat u een beleid met een product code hebt gemaakt, kunt u de product code later niet meer bewerken. Configuration Manager de sleutel uit veiligheids overwegingen verborgen. Als u de product code wilt wijzigen, voert u de volledige sleutel opnieuw in.  

        - **Licentie bestand** : Selecteer **Bladeren** om een geldig licentie bestand in XML-indeling te kiezen. Configuration Manager gebruikt dit licentie bestand om Windows 10 Mobile-apparaten bij te werken.  

5. Voltooi de wizard.  

## <a name="deploy-the-policy"></a>Het beleid implementeren  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit en selecteer het knoop punt upgrade van  **Windows 10-editie** .  

2. Selecteer het beleid voor editie-upgrades voor Windows 10 dat u wilt implementeren. Klik op het tabblad **Start** van het lint in de groep **implementatie** op **implementeren**.  

3. Kies de verzameling apparaten waarop u het beleid wilt implementeren.

4. Selecteer het schema waarmee de client het beleid evalueert.

5. Voltooi de wizard.

## <a name="next-steps"></a>Volgende stappen

Bewaak deze implementatie vanuit het knoop punt **implementaties** van de werk ruimte **bewaking** . Als u fouten ziet die duiden op een mislukte implementatie, bijvoorbeeld:

- **Niet van toepassing voor dit apparaat**
- **Conversie van gegevenstype is mislukt**

Deze fouten betekenen niet dat de implementatie is mislukt. Controleer op het doel apparaat dat de upgrade is uitgevoerd.

Zodra de client het doel beleid evalueert, wordt de upgrade binnen twee uur toegepast. Voor [sommige versies van Windows](/windows/deployment/upgrade/windows-10-edition-upgrades) moet op dat moment opnieuw worden opgestart. Zorg ervoor dat u alle gebruikers op de hoogte stelt waarvoor u het beleid implementeert of plan het beleid om buiten de werk uren van de gebruiker te worden uitgevoerd.

Als de volgende fout wordt weer gegeven in **DcmWmiProvider. log** op de client, controleert u of u de juiste sleutel gebruikt voor het activerings scenario. Zie de sectie [voordat u begint](#before-you-start) voor meer informatie. Als u een Key Management service (KMS) gebruikt voor activering, moet u ervoor zorgen dat u een [configuratie sleutel voor KMS-clients](/windows-server/get-started/kmsclientkeys)gebruikt.  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>Zie ook

- [Volume activering plannen](/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Upgrade Windows 10-editie](/windows/deployment/upgrade/windows-10-edition-upgrades)

- [Upgrade Windows 10-edities of schakel op apparaten de S-modus uit met behulp van Microsoft Intune](/intune/edition-upgrade-configure-windows-10)
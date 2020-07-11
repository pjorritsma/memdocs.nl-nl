---
title: Instellingen voor Microsoft Edge configureren
titleSuffix: Configuration Manager
description: Instellingen configureren voor de micro soft Edge verouderde webbrowser op Windows 10-clients
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 57eb9bbaed39ec463afc00d12202a9829729a086
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240543"
---
# <a name="configure-microsoft-edge-legacy-settings-in-configuration-manager"></a>Verouderde instellingen voor micro soft Edge configureren in Configuration Manager

> [!IMPORTANT]
> Als u micro soft Edge versie 77 of hoger gebruikt en u probeert het deel venster instellingen te openen, voert u `edge://settings/profiles` in de adres balk van de browser in plaats van de zoek opdracht in. Zie voor meer informatie [kennis Making met micro soft Edge](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know).
>
> In dit artikel wordt voor IT-professionals verouderde instellingen van micro soft Edge met micro soft endpoint Configuration Manager beheerd.

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!-- 1357310 -->
Voor klanten die de [micro soft Edge verouderde](https://docs.microsoft.com/microsoft-edge/deploy/) webbrowser op Windows 10-clients gebruiken, maakt u een Configuration Manager nalevings beleid om de browser instellingen te configureren.

Dit beleid is alleen van toepassing op clients met Windows 10, versie 1703 of hoger en micro soft Edge verouderde versie 45 en eerder. <!--511552-->

Zie voor meer informatie over het beheren van micro soft Edge versie 77 of hoger met Configuration Manager de [implementatie van micro soft Edge, versie 77 en hoger](../../apps/deploy-use/deploy-edge.md). Zie [micro soft Edge-policies (](https://docs.microsoft.com/DeployEdge/microsoft-edge-policies)Engelstalig) voor meer informatie over het configureren van beleids regels voor micro soft edge versie 77 of hoger.

## <a name="policy-settings"></a>Beleidsinstellingen

Dit beleid bevat momenteel de volgende instellingen:

- **Stel de micro soft Edge-browser in als standaard**: Hiermee wordt de Windows 10-standaard instelling voor apps voor de webbrowser geconfigureerd in micro soft Edge

- **Vervolg keuzelijst voor de adres balk toestaan**: vereist Windows 10, versie 1703 of hoger. Zie [AllowAddressBarDropdown-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)voor meer informatie.

- **Synchronisatie van favorieten tussen micro soft-browsers toestaan**: vereist Windows 10, versie 1703 of hoger. Zie [SyncFavoritesBetweenIEAndMicrosoftEdge-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)voor meer informatie.

- **Browse gegevens wissen bij afsluiten toestaan**: vereist Windows 10, versie 1703 of hoger. Zie [ClearBrowsingDataOnExit-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)voor meer informatie.

- **Do not track-headers toestaan**: Zie [AllowDoNotTrack-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)voor meer informatie.

- **Automatisch invullen toestaan**: Zie [AllowAutofill-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)voor meer informatie.

- **Cookies toestaan**: Zie [AllowCookies-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)voor meer informatie.

- **Pop-upblokkering toestaan**: Zie [AllowPopups-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)voor meer informatie.

- **Zoek suggesties in de adres balk toestaan**: Zie [AllowSearchSuggestionsinAddressBar-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)voor meer informatie.

- **Verzenden van intranet verkeer naar Internet Explorer toestaan**: Zie [SendIntranetTraffictoInternetExplorer-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)voor meer informatie.

- **Wachtwoord beheer toestaan**: Zie [AllowPasswordManager-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)voor meer informatie.

- **Ontwikkelhulpprogramma's toestaan**: Zie [AllowDeveloperTools-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)voor meer informatie.

- **Extensies toestaan**: Zie [AllowExtensions-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)voor meer informatie.

> [!TIP]
> Zie voor meer informatie over het gebruik van groeps beleid voor het configureren van deze en andere instellingen [micro soft Edge verouderd groeps beleid](https://docs.microsoft.com/microsoft-edge/deploy/group-policies/).

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge-legacy"></a>Windows Defender SmartScreen-instellingen voor micro soft Edge verouderd configureren
<!--1353701-->
Dit beleid voegt drie instellingen voor [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview)toe. Het beleid bevat nu de volgende aanvullende instellingen op de pagina **SmartScreen-instellingen** :

- **SmartScreen toestaan**: Hiermee geeft u op of Windows Defender SmartScreen is toegestaan. Zie het [AllowSmartScreen-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)voor meer informatie.

- **Gebruikers kunnen SmartScreen-prompts voor sites overschrijven**: Hiermee geeft u op of gebruikers de waarschuwingen van het Windows Defender SmartScreen-filter kunnen negeren over mogelijk schadelijke websites. Zie het [PreventSmartScreenPromptOverride-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)voor meer informatie.

- **Gebruikers kunnen SmartScreen-prompts negeren voor bestanden**: Hiermee geeft u aan of gebruikers de waarschuwingen van het Windows Defender SmartScreen-filter kunnen negeren over het downloaden van niet-geverifieerde bestanden. Zie het [PreventSmartScreenPromptOverrideForFiles-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)voor meer informatie.

## <a name="create-the-browser-profile"></a>Het browser profiel maken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Vouw **instellingen voor naleving** uit en selecteer het knoop punt **micro soft Edge-browser profielen** . Selecteer **micro soft Edge-profiel maken**op het lint.

2. Geef een **naam** op voor het beleid, geef eventueel een **Beschrijving**op en selecteer **volgende**.

3. Wijzig op de pagina **algemene instellingen** de waarde die moet worden **geconfigureerd** voor de instellingen die in dit beleid moeten worden meegenomen. Als u wilt door gaan met de wizard, moet u de instelling configureren om de **Edge-browser in te stellen als standaard**.

4. Configureer instellingen op de pagina **SmartScreen-instellingen** .

5. Selecteer op de pagina **ondersteunde platforms** de versies van het besturings systeem en de architecturen waarop dit beleid van toepassing is.

6. Voltooi de wizard.

## <a name="deploy-the-policy"></a>Het beleid implementeren

1. Selecteer uw beleid en selecteer **implementeren**in het lint.

2. **Blader** om de gebruiker of de apparaatgroep te selecteren waarvoor u het beleid wilt implementeren.

3. Selecteer desgewenst extra opties:

    1. Waarschuwingen genereren wanneer het beleid niet compatibel is.

    2. Stel het schema in waarmee de client de naleving van het apparaat evalueert met dit beleid.

4. Selecteer **OK** om de implementatie te maken.

## <a name="next-steps"></a>Volgende stappen

Net als bij elk beleid voor nalevings instellingen herstelt de client de instellingen op de door u opgegeven planning. [Controleer en meld op](monitor-compliance-settings.md) apparaatcompatibiliteit in de Configuration Manager-console.

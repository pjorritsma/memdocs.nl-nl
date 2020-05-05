---
title: Instellingen voor Microsoft Edge configureren
titleSuffix: Configuration Manager
description: Instellingen configureren voor de micro soft Edge-webbrowser op Windows 10-clients
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 91c11e133c74cd3b55db09e8bf80fd6c4df7774d
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210091"
---
# <a name="configure-microsoft-edge-settings-in-configuration-manager"></a>Instellingen voor micro soft Edge configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!-- 1357310 -->
Vanaf versie 1802, voor klanten die de [micro soft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) -webbrowser op Windows 10-clients gebruiken, maakt u een Configuration Manager beleid voor nalevings instellingen om verschillende micro soft Edge-instellingen te configureren. 

Dit beleid is alleen van toepassing op clients met Windows 10, versie 1703 of hoger. <!--511552-->


## <a name="policy-settings"></a>Beleidsinstellingen
Dit beleid bevat momenteel de volgende instellingen:
- **Stel de micro soft Edge-browser in als standaard**: Hiermee wordt de Windows 10-standaard instelling voor apps voor de webbrowser geconfigureerd in micro soft Edge
- **Vervolg keuzelijst voor de adres balk toestaan**: vereist Windows 10, versie 1703 of hoger. Zie [AllowAddressBarDropdown-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)voor meer informatie.
- **Synchronisatie van favorieten tussen micro soft-browsers toestaan**: vereist Windows 10, versie 1703 of hoger. Zie [SyncFavoritesBetweenIEAndMicrosoftEdge-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)voor meer informatie.
- **Browse gegevens wissen bij afsluiten toestaan**: vereist Windows 10, versie 1703 of hoger. Zie [ClearBrowsingDataOnExit-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)voor meer informatie.
- **Do not track-headers toestaan**: Zie [AllowDoNotTrack-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)voor meer informatie.
- **Automatisch invullen toestaan**: Zie [AllowAutofill-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)voor meer informatie.
- **Cookies toestaan**: Zie [AllowCookies-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)voor meer informatie.
- **Pop-upblokkering toestaan**: Zie [AllowPopups-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)voor meer informatie.
- **Zoek suggesties in de adres balk toestaan**: Zie [AllowSearchSuggestionsinAddressBar-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)voor meer informatie.
- **Verzenden van intranet verkeer naar Internet Explorer toestaan**: Zie [SendIntranetTraffictoInternetExplorer-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)voor meer informatie.
- **Wachtwoord beheer toestaan**: Zie [AllowPasswordManager-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)voor meer informatie.
- **Ontwikkelhulpprogramma's toestaan**: Zie [AllowDeveloperTools-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)voor meer informatie.
- **Extensies toestaan**: Zie [AllowExtensions-browser beleid](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)voor meer informatie.


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Windows Defender SmartScreen-instellingen voor micro soft Edge configureren
<!--1353701-->
Vanaf versie 1806 voegt dit beleid drie instellingen voor [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview)toe. Het beleid bevat nu de volgende aanvullende instellingen op de pagina **SmartScreen-instellingen** :

- **SmartScreen toestaan**: Hiermee geeft u op of Windows Defender SmartScreen is toegestaan. Zie het [AllowSmartScreen-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)voor meer informatie.
- **Gebruikers kunnen SmartScreen-prompts voor sites overschrijven**: Hiermee geeft u op of gebruikers de waarschuwingen van het Windows Defender SmartScreen-filter kunnen negeren over mogelijk schadelijke websites. Zie het [PreventSmartScreenPromptOverride-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)voor meer informatie.
- **Gebruikers kunnen SmartScreen-prompts negeren voor bestanden**: Hiermee geeft u aan of gebruikers de waarschuwingen van het Windows Defender SmartScreen-filter kunnen negeren over het downloaden van niet-geverifieerde bestanden. Zie het [PreventSmartScreenPromptOverrideForFiles-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)voor meer informatie.



## <a name="create-the-microsoft-edge-browser-profile"></a>Het micro soft Edge-browser profiel maken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Vouw **instellingen voor naleving** uit en selecteer het knoop punt **micro soft Edge-browser profielen** . Klik op de lint optie om een **micro soft Edge-profiel te maken**.
2. Geef een **naam** op voor het beleid, geef eventueel een **Beschrijving**op en klik op **volgende**.
3. Wijzig op de pagina **algemene instellingen** de waarde die u wilt **configureren** voor de instellingen die u in dit beleid wilt gebruiken en klik op **volgende**. De instelling voor het instellen van de **rand browser als standaard** moet worden geconfigureerd om door te gaan.
4. Configureer in versie 1806 en hoger de instellingen op de pagina **SmartScreen-instellingen** en klik vervolgens op **volgende**. 
5. Selecteer op de pagina **ondersteunde platforms** de versies van het besturings systeem en de architecturen waarop dit beleid van toepassing is en klik op **volgende**. 
6. Voltooi de wizard.



## <a name="deploy-the-policy"></a>Het beleid implementeren

1. Selecteer uw beleid en klik op de lint optie die u wilt **implementeren**.
2. Klik op **Bladeren** om de verzameling van de gebruiker of het apparaat te selecteren waarvoor u het beleid wilt implementeren. 
3. Selecteer indien nodig extra opties.  
     a. Waarschuwingen genereren wanneer het beleid niet compatibel is.  
     b. Stel het schema in waarmee de client de naleving van het apparaat evalueert met dit beleid. 
4. Klik op **OK** om de implementatie te maken.



## <a name="next-steps"></a>Volgende stappen

Net als bij elk beleid voor nalevings instellingen herstelt de client de instellingen op de door u opgegeven planning. [Controleer en meld op](monitor-compliance-settings.md) apparaatcompatibiliteit in de Configuration Manager-console.

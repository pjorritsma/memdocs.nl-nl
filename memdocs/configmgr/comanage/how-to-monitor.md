---
title: Co-beheer bewaken
titleSuffix: Configuration Manager
description: Gebruik het dash board voor co-beheer om informatie over gezamenlijk beheerde apparaten te bekijken.
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ac3bbb7c755be82b171f35442d2dbaf446dfea84
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695117"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Co-beheer in Configuration Manager controleren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u co-beheer hebt ingeschakeld, controleert u met behulp van de volgende methoden de apparaten voor co-beheer:

- [Dashboard voor co-beheer](#co-management-dashboard)  

- [Implementatie beleid](#deployment-policies)

- [WMI-apparaatgegevens](#wmi-device-data)

## <a name="co-management-dashboard"></a>Dashboard voor co-beheer

Met dit dash board kunt u computers bekijken die in uw omgeving worden beheerd. De grafieken kunnen helpen bij het identificeren van apparaten die mogelijk aandacht vereisen.<!--1356648,1358980-->

Ga in de Configuration Manager-console naar de werk ruimte **bewaking** en selecteer het knoop punt voor **co-beheer** .

![Scherm opname van het dash board voor co-beheer](media/co-management-dashboard.png)

### <a name="client-os-distribution"></a>Distributie van client besturingssysteem

Toont het aantal client apparaten per besturings systeem op versie. De functie maakt gebruik van de volgende groeperingen:  

- Windows 7 & 8. x
- Windows 10 lager dan 1709  
- Windows 10 1709 en hoger  

    > [!Tip]  
    > Windows 10, versie 1709 en hoger, is een vereiste voor co-beheer.  

Beweeg de muis aanwijzer over een grafiek sectie om het percentage van de apparaten in die besturings systeem groep weer te geven.

![Distributie tegel van client besturingssysteem](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status"></a>Status van co-beheer

Een trechter diagram waarin het aantal apparaten met de volgende statussen van het registratie proces wordt weer gegeven:
  
- In aanmerking komende apparaten
- Gepland  
- Inschrijving gestart  
- Geregistreerd  

![Tegel status van co-beheer (trechter)](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>Inschrijvings status van co-beheer

Toont de uitsplitsing van de apparaatstatus in de volgende categorieën:

- Geslaagd, hybride Azure AD-lid  
- Geslaagd, Azure AD-lid  
- Inschrijven, hybride Azure AD-lid  
- Fout, hybride Azure AD-lid  
- Fout, lid van Azure AD  
- Gebruikers aanmelding in behandeling  

    > [!NOTE]
    > Vanaf versie 1906, om het aantal apparaten met deze status in behandeling te verminderen, wordt nu automatisch een nieuw, door co beheerd apparaat Inge schreven bij de Microsoft Intune-service op basis van het Azure AD- *apparaat* -token. U hoeft niet te wachten totdat een gebruiker zich bij het apparaat aanmeldt voor het starten van de automatische inschrijving. Ter ondersteuning van dit gedrag moet Windows 10, versie 1803 of hoger worden uitgevoerd op het apparaat.
    >
    > Als het token van het apparaat mislukt, wordt het terugvallen op het vorige gedrag met het gebruikers token. Zoek in het **ComanagementHandler. log** naar de volgende vermelding: `Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

Selecteer een status in de tegel om uit te zoomen op een lijst met apparaten in die staat.  

![Tegel inschrijvings status van co-beheer](media/co-management-dashboard/1358980-enrollment-status.png)

### <a name="workload-transition"></a>Werkbelasting overgang

Geeft een staaf diagram weer met het aantal apparaten dat u hebt overgezet naar Microsoft Intune voor de beschik bare werk belastingen.

De lijst met werk belastingen is afhankelijk van de versie van Configuration Manager. Zie [workloads kunnen worden overgezet naar intune](workloads.md)voor meer informatie.

Beweeg de muis aanwijzer over een grafiek sectie om het aantal apparaten weer te geven dat is overgezet voor de werk belasting.

![Grafiek van de werk belasting overgangs balk](media/co-management-dashboard/Workload-Transition.PNG)

### <a name="enrollment-errors"></a>Inschrijvingsfouten

Deze tabel bevat een lijst met registratie fouten van apparaten. Deze fouten kunnen afkomstig zijn van het MDM-onderdeel in Windows, het Windows-basis besturingssysteem of de Configuration Manager-client.

Er zijn honderden mogelijke fouten. De volgende tabel bevat de meest voorkomende fouten.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Fout | Beschrijving |
|---------|---------|
| 2147549183 (0x8000FFFF) | MDM-registratie is nog niet geconfigureerd op Azure AD of de inschrijvings-URL wordt niet verwacht.<br><br>[Automatische inschrijving voor Windows 10 inschakelen](/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | De licentie van de gebruiker heeft de inschrijving van een ongeldige status geblokkeerd<br><br>[Licenties toewijzen aan gebruikers](/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Bij het automatisch inschrijven bij intune, maar de Azure AD-configuratie is niet volledig toegepast. Dit probleem moet tijdelijk zijn, omdat het apparaat na een korte tijd opnieuw wordt geprobeerd. |
| 2149056554 (0x 8018002A)<br>&nbsp; | De gebruiker heeft de bewerking geannuleerd<br><br>Als voor MDM-inschrijving multi-factor Authentication is vereist en de gebruiker niet is aangemeld met een ondersteunde tweede factor, wordt door Windows een pop-upmelding voor de gebruiker weer gegeven die moet worden inge schreven. Deze fout treedt op als de gebruiker niet reageert op de pop-upmelding. Dit probleem zou tijdelijk moeten zijn, omdat Configuration Manager een nieuwe poging doet en de gebruiker wordt gevraagd. Gebruikers moeten gebruikmaken van multi-factor Authentication wanneer ze zich aanmelden bij Windows. Wees er ook aan om dit gedrag te verwachten, en als hierom wordt gevraagd, actie te ondernemen. |
| 2149056532 (0x80180014)<br>MENROLL_E_DEVICENOTSUPPORTED | Het beheer van mobiele apparaten wordt niet ondersteund. Controleer de beperkingen van apparaten. |
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Het beheer van mobiele apparaten wordt niet ondersteund. Controleer de beperkingen van apparaten. |
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Verificatie van de gebruiker door de server is mislukt<br><br> Er is geen Azure AD-token voor de gebruiker. Zorg ervoor dat de gebruiker zich kan verifiëren bij Azure AD. |
| 2147942450 (0x 80070032)<br>&nbsp; | Automatische MDM-inschrijving wordt alleen ondersteund op Windows RS3 en hoger.<br><br>Zorg ervoor dat het apparaat voldoet aan de [minimum vereisten](overview.md#windows-10) voor co-beheer. |
| 3400073293 | Onbekende reactie van ADAL-gebruikers realm-account<br><br>Controleer uw Azure AD-configuratie en zorg ervoor dat de verificatie van gebruikers goed kan worden uitgevoerd. |
| 3399548929 | Gebruikers aanmelding vereist<br><br>Dit probleem zou tijdelijk moeten zijn. Deze gebeurtenis treedt op wanneer de gebruiker zich snel afmeldt voordat de inschrijvings taak plaatsvindt. |
| 3400073236 | De aanvraag voor het ADAL-beveiligings token is mislukt.<br><br>Controleer uw Azure AD-configuratie en zorg ervoor dat de verificatie van gebruikers goed kan worden uitgevoerd. |
| 2149122477 | Algemeen HTTP-probleem |
| 3400073247 | ADAL geïntegreerde Windows-authenticatie wordt alleen ondersteund in federatieve stroom<br><br>[De implementatie van uw hybride Azure Active Directory-deelname plannen](/azure/active-directory/devices/hybrid-azuread-join-plan) |
| 3399942148 | De server of proxy is niet gevonden.<br><br>Dit probleem zou zich moeten voordoen als de client niet kan communiceren met de Cloud. Als het probleem blijft bestaan, controleert u of de client een consistente verbinding met Azure heeft. | 
| 2149056532 | Een specifiek platform of specifieke versie wordt niet ondersteund<br><br>Zorg ervoor dat het apparaat voldoet aan de [minimum vereisten](overview.md#windows-10) voor co-beheer. |
| 2147943568 | Het element is niet gevonden<br><br>Dit probleem zou tijdelijk moeten zijn. Als het probleem blijft bestaan, neemt u contact op met Microsoft Ondersteuning. |
| 2192179208 | Er zijn onvoldoende geheugen bronnen beschikbaar om deze opdracht te verwerken.<br><br>Dit probleem zou zich moeten voordoen, maar moeten zichzelf oplossen wanneer de client nieuwe pogingen doet. |
| 3399614467 | Grant voor ADAL-autorisatie is mislukt voor deze bevestiging<br><br>Controleer uw Azure AD-configuratie en zorg ervoor dat de verificatie van gebruikers goed kan worden uitgevoerd. |
| 2149056517 | Algemene fout van de beheer server, zoals de toegangs fout van de data base<br><br>Dit probleem zou tijdelijk moeten zijn. Als het probleem blijft bestaan, neemt u contact op met Microsoft Ondersteuning. |
| 2149134055 | WinHTTP-naam is niet omgezet<br><br>De client kan de naam van de service niet omzetten. Controleer de DNS-configuratie. |
| 2149134050 | Internet time-out<br><br>Dit probleem zou zich moeten voordoen als de client niet kan communiceren met de Cloud. Als het probleem blijft bestaan, controleert u of de client een consistente verbinding met Azure heeft. |

Zie [MDM-registratie fout waarden](/windows/desktop/mdmreg/mdm-registration-constants)voor meer informatie.

## <a name="deployment-policies"></a>Implementatie beleid

Er worden twee beleids regels gemaakt in het knoop punt **implementaties** van de werk ruimte **bewaking** . Een beleid is voor de test groep en één voor productie. Dit beleid rapporteert alleen het aantal apparaten waarop Configuration Manager het beleid heeft toegepast. Het is niet belang rijk om te bepalen hoeveel apparaten zijn Inge schreven bij intune. Dit is een vereiste voordat apparaten gezamenlijk kunnen worden beheerd.

Het productie beleid (CoMgmtSettingsProd) is gericht op de verzameling **alle systemen** . Het heeft een toepas baarheids voorwaarde waarmee het type en de versie van het besturings systeem wordt gecontroleerd. Als de client een server besturingssysteem of niet Windows 10 is, is het beleid niet van toepassing en wordt er geen actie ondernomen.

## <a name="wmi-device-data"></a>WMI-apparaatgegevens

Een query uitvoeren op de WMI-klasse **SMS_Client_ComanagementState** in de naam ruimte **root\sms\ site_ site code &lt;>** op de site server. U kunt aangepaste verzamelingen maken in Configuration Manager, waarmee u de status van uw implementatie voor co-beheer bepaalt. Zie [verzamelingen maken](../core/clients/manage/collections/create-collections.md)voor meer informatie over het maken van aangepaste verzamelingen.

De volgende velden zijn beschikbaar in de WMI-klasse:

- **MachineId**: een unieke apparaat-id voor de Configuration Manager-client

- **MDMEnrolled**: Hiermee geeft u op of het apparaat is inge SCHREVEN bij MDM

- **Instantie**: de instantie waarvoor het apparaat is inge schreven

- **ComgmtPolicyPresent**: Hiermee geeft u op of de Configuration Manager beleid voor co-beheer bestaat op de client. Als de **MDMEnrolled** -waarde is `0` , wordt het apparaat niet gezamenlijk beheerd, ongeacht het beleid voor co-beheer bestaat op de client.

Een apparaat wordt gezamenlijk beheerd wanneer het veld **MDMEnrolled** en **ComgmtPolicyPresent** de waarde beide hebben `1` .
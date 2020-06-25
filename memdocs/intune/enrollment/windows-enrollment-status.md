---
title: De pagina Status van de inschrijving instellen
titleSuffix: Microsoft Intune
description: Stel een begroetingspagina in voor gebruikers die Windows 10-apparaten registreren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/26/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f8991b772f5562538403492735f1f4c2fdc87e8
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093452"
---
# <a name="set-up-the-enrollment-status-page"></a>De pagina Status van de inschrijving instellen
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
De pagina Status van de inschrijving (ESP) geeft de voortgang van de inrichting weer nadat een nieuw apparaat is geregistreerd, en wanneer nieuwe gebruikers zich aanmelden bij het apparaat.  Zo kunnen IT-beheerders toegang tot het apparaat voorkomen totdat het volledig is ingericht en tegelijkertijd gebruikers informatie geven over de taken die in het inrichtingsproces resteren.

De ESP kan worden gebruikt als onderdeel van een [Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/)-inrichtingsscenario en kan ook afzonderlijk van Windows Autopilot worden gebruikt als onderdeel van de standaard out-of-box experience (OOBE) voor Azure AD-deelname, en voor nieuwe gebruikers die zich voor het eerst aanmelden bij het apparaat.

U kunt voor de pagina Status van de inschrijving meerdere profielen met verschillende configuraties die het volgende doen:

- De voortgang van de installatie weergeven
- Toegang blokkeren tot het inrichtingsproces is voltooid
- Tijdslimieten
- Toegestane probleemoplossingsbewerkingen

Deze profielen worden opgegeven in een volgorde van prioriteit. De hoogste prioriteit die van toepassing is, wordt gebruikt.  Elk ESP-profiel kan worden gericht op groepen die apparaten of gebruikers bevatten.  Bij het bepalen welk profiel u moet gebruiken, worden de volgende criteria gevolgd:

- Het profiel met de hoogste prioriteit dat op het apparaat is gericht, wordt het eerst gebruikt.
- Als er geen profielen zijn gericht op het apparaat, wordt het profiel met de hoogste prioriteit gebruikt dat is gericht op de huidige gebruiker.  (Dit geldt alleen voor scenario's waar een gebruiker aanwezig is. Bij scenario’s waar gebruikersregistratie met ondersteuning of automatisch implementeren wordt gebruikt, kan u zich alleen op een apparaat richten.)
- Als er geen profielen zijn die zijn gericht op specifieke groepen, wordt het standaard ESP-profiel gebruikt.

## <a name="available-settings"></a>Beschikbare instellingen

De volgende instellingen kunnen worden geconfigureerd om de werking van de pagina Status van de inschrijving aan te passen:

<table>
<th align="left">Instelling<th align="left">Ja<th align="left">Nee
<tr><td>Voortgang van installatie van app en profiel weergeven<td>De pagina Status van de inschrijving wordt weergegeven.<td>De pagina Status van de inschrijving wordt niet weergegeven.
<tr><td>Apparaatgebruik blokkeren totdat alle apps en profielen zijn geïnstalleerd<td>Met de instellingen in deze tabel kan de werking van de pagina Status van de inschrijving worden aangepast, zodat de gebruiker mogelijke installatieproblemen kan oplossen.
<td>De pagina Status van de inschrijving wordt weergegeven zonder extra opties om installatieproblemen op te lossen.
<tr><td>Toestaan dat gebruikers het apparaat opnieuw instellen als er een installatiefout optreedt<td>Er wordt een knop <b>Apparaat opnieuw instellen</b> weergegeven als er een installatieprobleem is.<td>Er wordt geen knop <b>Apparaat opnieuw instellen</b> weergegeven als er een installatieprobleem is.
<tr><td>Toestaan dat gebruikers het apparaat gebruiken als er een installatiefout optreedt<td>Er wordt een knop <b>Toch doorgaan</b> weergegeven als er een installatieprobleem is.<td>Er wordt geen knop <b>Toch doorgaan</b> weergegeven als er een installatieprobleem is.
<tr><td>Een foutbericht voor de tijdslimiet weergeven als de installatie langer duurt dan het opgegeven aantal minuten<td colspan="2">Geef het aantal minuten op dat moet worden gewacht totdat de installatie is voltooid. De standaardwaarde is 60 minuten.
<tr><td>Aangepast bericht weergeven als er een fout optreedt<td>Er wordt een tekstvak weergegeven waarin u een aangepast bericht kunt invoeren dat wordt weergegeven als er een installatiefout optreedt.<td>Dit is het bericht dat standaard wordt weergegeven: <br><b>De installatie heeft de tijdslimiet overschreden die door uw organisatie is ingesteld. Probeer het opnieuw of neem contact op met de IT-ondersteuning voor hulp.<b>
<tr><td>Gebruikers toestaan om logboeken over installatiefouten te verzamelen<td>Als er een installatiefout optreedt, wordt er een knop <b>Logboeken verzamelen</b> weergegeven. <br>Als de gebruiker op deze knop klikt, kunnen ze een locatie kiezen voor het opslaan van het logboekbestand <b>MDMDiagReport.cab</b>.<td>De knop <b>Apparaat opnieuw instellen</b> wordt niet weergegeven als er een installatieprobleem is.
<tr><td>Gebruik van het apparaat blokkeren totdat de vereiste apps zijn geïnstalleerd als deze zijn toegewezen aan de gebruiker/het apparaat<td colspan="2">Kies <b>Alle</b> of <b>Geselecteerd</b>. <br><br>Als u <b>Geselecteerd</b> kiest, wordt er een knop <b>Apps selecteren</b> weergegeven waarmee u kunt kiezen welke apps moeten worden geïnstalleerd voordat het apparaat wordt ingeschakeld.
</table>

## <a name="turn-on-default-enrollment-status-page-for-all-users"></a>De standaardpagina Status van de inschrijving voor alle gebruikers inschakelen

Volg de onderstaande stappen om de pagina Status van de registratie in te schakelen.
 
1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **Windows** > **Windows-inschrijving** > **Inschrijvingsstatuspagina**.
2. In de blade **Pagina Status van de inschrijving** kiest u **Standaard** > **Instellingen**.
3. Bij **Voortgang van installatie van app en profiel weergeven** kiest u **Ja**.
4. Kies de andere instellingen die u wilt inschakelen en kies vervolgens **Opslaan**.

## <a name="create-enrollment-status-page-profile-and-assign-to-a-group"></a>Profiel voor pagina Status van de registratie maken en dit aan een groep toewijzen

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **Windows** > **Windows-inschrijving** > **Inschrijvingsstatuspagina** > **Profiel maken**.
2. Geef een **naam** en **beschrijving** op.
3. Kies **Maken**.
4. Kies het nieuwe profiel in de lijst **Pagina Status van de inschrijving**.
5. Kies **Toewijzingen** > **Groepen selecteren** > kies de groepen waarvoor u dit profiel wilt instellen > **Selecteren** > **Opslaan**.
6. Kies **Instellingen** > kies de instellingen die u op dit profiel wilt toepassen > **Opslaan**.

## <a name="set-the-enrollment-status-page-priority"></a>De prioriteit instellen voor de pagina Status van de registratie

Een apparaat of gebruiker kan zich in veel groepen bevinden en gericht zijn op meerdere profielen voor de pagina Status van de inschrijving. Als u wilt bepalen welke profielen het eerst worden beschouwd, kunt u de prioriteiten voor elk profiel instellen. Gebruikers met een hogere prioriteit worden als eerste overwogen.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **Windows** > **Windows-inschrijving** > **Inschrijvingsstatuspagina**.
2. Beweeg de muisaanwijzer over het profiel in de lijst.
3. Sleep met behulp van de drie verticale puntjes het profiel naar de gewenste positie in de lijst.

## <a name="block-access-to-a-device-until-a-specific-application-is-installed"></a>Toegang blokkeren tot een apparaat tot een bepaalde toepassing is geïnstalleerd

U kunt opgeven welke apps moeten worden geïnstalleerd voordat de pagina Status van de inschrijving (ESP) is voltooid.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **Windows** > **Windows-inschrijving** > **Inschrijvingsstatuspagina**.
2. Kies een profiel > **Instellingen**.
3. Kies **Ja** bij **Voortgang van installatie van app en profiel weergeven**.
4. Kies **Ja** bij **Apparaatgebruik blokkeren totdat alle apps en profielen zijn geïnstalleerd**.
5. Kies **Geselecteerd** bij **Gebruik van het apparaat blokkeren totdat de vereiste apps zijn geïnstalleerd als deze zijn toegewezen aan de gebruiker/het apparaat**.
6. Kies **Apps selecteren** > kies de apps > **selecteer** > **Opslaan**.

De apps in deze lijst worden door Intune gebruikt om de lijst te filteren die als blokkering moet worden beschouwd.  De lijst geeft niet aan welke apps moeten worden geïnstalleerd.  Als u in deze lijst bijvoorbeeld 'App 1,'App 2' en 'App 3' opneemt en 'App 3', 'App 4 'aan het apparaat of de gebruiker worden gekoppeld, wordt op de inschrijvingsstatuspagina alleen 'App 3' bijgehouden.  'App 4' wordt wel nog geïnstalleerd, maar op de inschrijvingsstatuspagina wordt niet gewacht op voltooiing ervan.

Er kunnen maximaal 100 apps worden opgegeven.

## <a name="enrollment-status-page-tracking-information"></a>Traceringsinformatie op de pagina Status van de inschrijving

Er zijn drie fasen waarvoor gegevens worden bijgehouden op de pagina Status van de inschrijving: voorbereiding van het apparaat, installatie van het apparaat en installatie van het account.

### <a name="device-preparation"></a>Voorbereiding van het apparaat

Deze gegevens worden bijgehouden voor de voorbereiding van het apparaat:

- Verklaring van TPM-sleutels (Trusted Platform Module) (indien van toepassing)
- Toevoegingsproces voor Azure Active Directory
- Intune (MDM)-inschrijving
- Installatie van de Intune-beheerextensies (gebruikt voor het installeren van Win32-apps)

### <a name="device-setup"></a>Installatie van het apparaat

De pagina voor de status van de inschrijving houdt de volgende items voor de installatie van het apparaat:

- Beveiligingsbeleid
  - Eén configuratieprovider (CSP) voor alle inschrijvingen.
  - Werkelijke CSP's die door Intune zijn geconfigureerd, worden hier niet bijgehouden.
- Toepassingen
  - LOB (Line-of-Business) MSI-apps per apparaat.
  - LOB (Line-of-Business) opslag-apps met installatiecontext = apparaat.
  - Offline opslag- en LOB (Line-of-Business) opslag-apps met installatiecontext = apparaat.
  - Win32-toepassingen (alleen Windows 10 versie 1903 en nieuwer) 
- Connectiviteitsprofielen
  - VPN- of Wi-Fi-profielen die zijn toegewezen aan **Alle apparaten** of een groep apparaten waarvan het apparaat dat wordt geregistreerd lid is, maar alleen voor Autopilot-apparaten
- Certificaatprofielen die zijn toegewezen aan **Alle apparaten** of een groep apparaten waarvan het apparaat dat wordt geregistreerd lid is, maar alleen voor Autopilot-apparaten

### <a name="account-setup"></a>Account instellen

Voor de installatie van het account worden op de pagina Status van de inschrijving de volgende items bijgehouden als deze zijn toegewezen aan de huidige aangemelde gebruiker:

- Beveiligingsbeleid
  - Eén CSP voor alle inschrijvingen.
  - Werkelijke CSP's die door Intune zijn geconfigureerd, worden hier niet bijgehouden.
- Toepassingen
  - LOB (Line-of-Business) MSI-apps per gebruiker die worden toegewezen aan alle apparaten, aan alle gebruikers of aan een gebruikersgroep waarvan de gebruiker die het apparaat inschrijft, lid is.
  - LOB (Line-of-Business) MSI-apps per apparaat die worden toegewezen aan alle gebruikers of aan een gebruikersgroep waarvan de gebruiker die het apparaat inschrijft, lid is.
  - LOB Store-apps, online Store-apps en offline Store-apps die aan een van de volgende objecten zijn toegewezen:
    - Alle apparaten
    - Alle gebruikers
    - Een gebruikersgroep waarvan de gebruiker die het apparaat inschrijft, lid is, met de installatiecontext ingesteld op Gebruiker.
  - Win32-toepassingen (alleen Windows 10 versie 1903 en nieuwer) 
- Connectiviteitsprofielen
  - VPN- of Wi-Fi-profielen die worden toegewezen aan alle gebruikers of aan een gebruikersgroep waarvan de gebruiker die het apparaat inschrijft, lid is.
- Certificaten
  - Certificaatprofielen die worden toegewezen aan alle gebruikers of aan een gebruikersgroep waarvan de gebruiker die het apparaat inschrijft, lid is.

### <a name="troubleshooting"></a>Probleemoplossing

Hieronder volgen enkele veelgestelde vragen over het oplossen van problemen met betrekking tot de pagina Status van de inschrijving.

- Waarom zijn mijn toepassingen niet geïnstalleerd en getraceerd met de pagina Inschrijvingsstatus?
  - Om te garanderen dat toepassingen worden geïnstalleerd en getraceerd met de pagina Inschrijvingsstatus, zorgt u ervoor dat:
      - De apps zijn toegewezen aan een Azure AD-groep met het apparaat (voor op apparaten gerichte apps) of de gebruiker (voor op gebruikers gerichte apps), met behulp van de toewijzing 'vereist'.  (Op apparaten gerichte apps worden getraceerd tijdens de apparaatfase van ESP, terwijl op gebruikers gerichte apps worden getraceerd tijdens de gebruikersfase van ESP.)
      - U geeft **Apparaatgebruik blokkeren totdat alle apps en profielen zijn geïnstalleerd** op of neemt de app op in de lijst **Apparaatgebruik blokkeren tot deze vereiste apps zijn geïnstalleerd**.
      - De apps worden geïnstalleerd in apparaatcontext en hebben geen toepasselijkheidsregels voor gebruikerscontext.

- Waarom wordt de pagina Status van de inschrijving weergegeven voor implementaties zonder Autopilot, bijvoorbeeld wanneer een gebruiker zich voor de eerste keer aanmeldt op een apparaat dat voor co-beheer is ingeschreven bij Configuration Manager?  
  - Op de pagina Status van de inschrijving wordt de installatiestatus voor alle inschrijvingsmethoden vermeld, met inbegrip van
      - Autopilot
      - co-beheer met Configuration Manager
      - wanneer een nieuwe gebruiker zich voor de eerste keer aanmeldt bij een apparaat waarop het beleid voor de pagina Status van de inschrijving is toegepast
      - wanneer de instelling **Alleen pagina weergeven voor apparaten die zijn ingericht door Out-of-Box Experience (OOBE)** is ingeschakeld en het beleid is ingesteld, krijgt alleen de eerste gebruiker die zich bij het apparaat aanmeldt de pagina Status van de inschrijving

- Hoe kan ik de pagina Status van de inschrijving uitschakelen als deze is geconfigureerd op het apparaat?
  - Het beleid voor de pagina Status van de inschrijving wordt ingesteld op een apparaat op het moment van inschrijving. Als u de pagina Status van de inschrijving wilt uitschakelen, moet u de secties Disable User ESP en Disable Device ESP van de pagina Status van de inschrijving uitschakelen. U kunt dit doen door aangepaste OMA-URI-instellingen te maken met de volgende configuraties.

      Pagina Status van de inschrijving voor gebruikers uitschakelen:

      ```
      Name:  Disable User ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipUserStatusPage
      Data type:  Boolean
      Value:  True 
      ```
      Pagina Status van de inschrijving voor apparaten uitschakelen:

      ```
      Name:  Disable Device ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipDeviceStatusPage
      Data type:  Boolean
      Value:  True 
      ```
- Hoe kan ik logboekbestanden verzamelen?
  - Er zijn twee manieren om logboekbestanden te verzamelen voor de pagina Status van de inschrijving:
      - Schakel in het ESP-beleid de mogelijkheid voor gebruikers in om logboeken te verzamelen. Wanneer er een time-out optreedt op de pagina Status van de inschrijving, kan de eindgebruiker de optie **Logboeken verzamelen** kiezen. Door een USB-stick te plaatsen, kunnen de logboekbestanden worden gekopieerd.
      - Open een opdrachtprompt met Shift-F10 en voer vervolgens de volgende opdrachtregel in om logboekbestanden te genereren: 

      ```
      mdmdiagnosticstool.exe -area Autopilot -cab <pathToOutputCabFile>.cab 
      ```

### <a name="known-issues"></a>Bekende problemen

Hieronder vindt u bekende problemen met betrekking tot de pagina Status van de inschrijving.

- Als u het ESP-profiel uitschakelt, blijft het ESP-beleid van kracht op apparaten en zien gebruikers nog steeds de pagina Status van de inschrijving wanneer ze zich voor de eerste keer aanmelden bij het apparaat. Het beleid wordt niet verwijderd wanneer het ESP-profiel wordt uitgeschakeld. U moet OMA-URI implementeren om de pagina Status van de inschrijving uit te schakelen. Hierboven vindt u instructies voor het uitschakelen van de pagina Status van de inschrijving met OMA-URI. 
- Opnieuw opstarten tijdens apparaatinstallatie dwingt de gebruiker om referenties in te voeren voordat de fase voor installatie van het account wordt ingegaan. Gebruikersreferenties blijven niet behouden tijdens het opnieuw opstarten. Laat de gebruiker zijn of haar referenties invoeren, waarna de pagina Status van de inschrijving wordt weergegeven. 
- Er treedt altijd een time-out op voor de pagina Status van de inschrijving tijdens een inschrijving met Werk- en schoolaccount toevoegen in Windows 10-versie 1903 en lager. De pagina Status van de inschrijving wacht totdat de Azure AD-registratie is voltooid. Het probleem is opgelost in Windows 10-versie 1903 en hoger.  
- Hybride Azure AD Auto Pilot-implementatie met ESP duurt langer dan de time-outperiode die is gedefinieerd in het ESP-profiel. Bij hybride Azure AD Auto Pilot-implementaties duurt de ESP 40 minuten langer dan de waarde die is ingesteld in het ESP-profiel. Deze vertraging geeft de on-premises AD-connector tijd om de nieuwe apparaatrecord te maken in Azure AD. 
- De Windows-aanmeldingspagina wordt niet vooraf ingevuld met de gebruikersnaam in de modus Op basis van gebruiker van Autopilot. Als het apparaat opnieuw wordt opgestart tijdens de installatiefase van het apparaat van ESP, gebeurt het volgende:
  - de gebruikersreferenties blijven niet behouden
  - de gebruiker moet de referenties opnieuw invoeren voordat de installatie van het apparaat kan worden gevolgd door de installatie van het account
- De ESP wordt erg lang weergegeven of de identificatiefase wordt nooit voltooid. In Intune worden de ESP-beleidsregels berekend tijdens de identificatiefase. De kans bestaat dat een apparaat nooit de ESP-beleidsregels kan berekenen als aan de huidige gebruiker geen Intune-licentie is toegewezen.  
- De configuratie van Microsoft Defender Application Control heeft tot gevolg dat tijdens Autopilot een verzoek wordt weergegeven om het apparaat opnieuw op te starten. Het configureren van Microsoft Defender Application (AppLocker CSP) vereist opnieuw opstarten. Wanneer dit beleid is geconfigureerd, kan dit ertoe leiden dat het apparaat opnieuw wordt opgestart tijdens Autopilot. Op dit moment is er geen manier om het opnieuw opstarten te onderdrukken of uit te stellen.
- Als het DeviceLock-beleid (https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) ) is ingeschakeld als onderdeel van een ESP-profiel, kan de OOBE of het automatisch aanmelden bij het bureaublad van de gebruiker om twee redenen onverwacht mislukken.
  - Als het apparaat niet opnieuw is opgestart vóór de ESP-installatiefase van het apparaat, wordt de gebruiker mogelijk gevraagd om Azure AD-referenties in te voeren. Deze vraag wordt gesteld in plaats van een geslaagde automatische aanmelding waarbij de gebruiker de eerste aanmeldingsanimatie van Windows ziet.
  - De automatische aanmelding mislukt als het apparaat opnieuw is opgestart nadat de gebruiker Azure AD-referenties heeft ingevoerd, maar voordat de ESP-installatiefase van het apparaat is afgesloten. Deze fout treedt op omdat de ESP-installatiefase van het apparaat nooit is voltooid. De tijdelijke oplossing is om het apparaat opnieuw in te stellen.

## <a name="next-steps"></a>Volgende stappen

Nadat u Windows-inschrijvingspagina's hebt ingesteld, kunt u leren hoe u Windows-apparaten beheert. Zie [Wat is Microsoft Intune-apparaatbeheer?](../remote-actions/device-management.md) voor meer informatie.

---
title: Windows Defender Application Control beheren
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van Configuration Manager voor het beheren van Windows Defender-toepassings beheer.
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0dcd519a7703b5de94f779dc5dbe48aa0d34a3bc
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700460"
---
# <a name="windows-defender-application-control-management-with-configuration-manager"></a>Beheer van Windows Defender-toepassings beheer met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

## <a name="introduction"></a>Inleiding
Windows Defender Application Control is ontworpen om Pc's te beschermen tegen malware en andere niet-vertrouwde software. Hiermee wordt voor komen dat schadelijke code wordt uitgevoerd door ervoor te zorgen dat alleen goedgekeurde code, die u kent, kan worden uitgevoerd.

Windows Defender Application Control is een op software gebaseerde beveiligingslaag die een expliciete lijst van software afdwingt die op een PC mag worden uitgevoerd. Op eigen toepassings beheer heeft geen hardware-of firmware vereisten. Met het beleid voor toepassings beheer dat is geïmplementeerd met Configuration Manager wordt een beleid ingeschakeld op Pc's in doel verzamelingen die voldoen aan de minimale Windows-versie en SKU-vereisten die in dit artikel worden beschreven. U kunt op Hyper Visor gebaseerde beveiliging van beleids regels voor toepassings beheer die via Configuration Manager zijn geïmplementeerd, eventueel inschakelen via groepsbeleid op geschikte hardware.

Lees de [implementatie handleiding voor Windows Defender Application Control](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)voor meer informatie over Windows Defender Application Control.

   > [!NOTE]
   > - Vanaf Windows 10, versie 1709, kan het Configureer bare code-integriteits beleid Windows Defender Application Control worden genoemd.
   > - Vanaf Configuration Manager versie 1710 is de naam van het Device Guard-beleid gewijzigd in Windows Defender Application Control-beleid.

## <a name="using-windows-defender-application-control-with-configuration-manager"></a>Windows Defender Application Control gebruiken met Configuration Manager

U kunt Configuration Manager gebruiken om een Windows Defender Application Control-beleid te implementeren. Met dit beleid kunt u de modus configureren waarin Windows Defender Application Control wordt uitgevoerd op Pc's in een verzameling. 

U kunt een van de volgende modi configureren:

1. **Afdwinging ingeschakeld** : alleen vertrouwde uitvoer bare bestanden mogen worden uitgevoerd.
2. **Alleen controle** : toestaan dat alle uitvoer bare bestanden worden uitgevoerd, maar niet-vertrouwde uitvoer bare bestanden die worden uitgevoerd in het gebeurtenis logboek van de lokale client worden vastgelegd.

> [!Tip]  
> Deze functie werd voor het eerst in versie 1702 geïntroduceerd als een [voorlopige functie](../../core/servers/manage/pre-release-features.md). Vanaf versie 1906 is het niet langer een functie van de voorlopige versie.  

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Wat kan worden uitgevoerd wanneer u een Windows Defender Application Control-beleid implementeert?

Met Windows Defender Application Control kunt u sterk bepalen wat er kan worden uitgevoerd op Pc's die u beheert. Deze functie kan handig zijn voor Pc's in afdelingen met een hoge beveiliging, waar het essentieel is dat ongewenste software niet kan worden uitgevoerd.

Wanneer u een beleid implementeert, kunnen de volgende uitvoer bare bestanden doorgaans worden uitgevoerd:

- Onderdelen van het Windows-besturings systeem
- Hardware-ontwikkelaars centrum Stuur programma's (met hand tekeningen voor Windows Hardware Quality Labs)
- Windows Store-apps
- De Configuration Manager-client 
- Alle software die via Configuration Manager dat Pc's worden geïnstalleerd nadat het Windows Defender Application Control-beleid is verwerkt. 
- Updates voor Windows-onderdelen van:
    - Windows Update
    - Windows Update voor Bedrijven
    - Windows Server Update Services
    - Configuration Manager
    - Optioneel software met een goede reputatie, zoals bepaald door de Microsoft Intelligent Security Graph (ISG). De ISG bevat Windows Defender SmartScreen en andere micro soft-Services. Op het apparaat moet Windows Defender SmartScreen en Windows 10 versie 1709 of hoger worden uitgevoerd om deze software te kunnen vertrouwen.

>[!IMPORTANT]
>Deze items bevatten geen software die *niet* is ingebouwd in Windows die automatisch wordt bijgewerkt van het internet of software-updates van derden, ongeacht of deze zijn geïnstalleerd via een van de eerder genoemde update mechanismen of via internet. Alleen software wijzigingen die worden geïmplementeerd als de Configuration Manager-client kan worden uitgevoerd.

## <a name="before-you-start"></a>Voordat u begint

Lees de volgende informatie voordat u beleid voor Windows Defender-toepassings beheer configureert of implementeert:

- Windows Defender Application Control Management is een voorlopige functie voor Configuration Manager en kan worden gewijzigd.
- Als u Windows Defender Application Control met Configuration Manager wilt gebruiken, moet op de Pc's die u beheert, Windows 10 Enter prise versie 1703 of hoger worden uitgevoerd.
- Nadat een beleid is verwerkt op een client-PC, wordt Configuration Manager geconfigureerd als een beheerd installatie programma op die client. Software die via IT wordt geïmplementeerd, wordt na de beleids verwerking automatisch vertrouwd. Software die door Configuration Manager is geïnstalleerd voordat de beleids processen van het Windows Defender-toepassings beheer worden niet automatisch vertrouwd.
- Het standaard schema voor de nalevings evaluatie voor toepassings beheer beleid dat kan worden geconfigureerd tijdens de implementatie, is om de één dag. Als er problemen met de verwerking van het beleid worden waargenomen, kan het nuttig zijn om het evaluatie schema voor naleving zo te configureren dat deze korter is, bijvoorbeeld elk uur. Dit schema bepaalt hoe vaak clients opnieuw proberen een Windows Defender Application Control-beleid te verwerken als er een fout optreedt.
- Ongeacht de afdwingings modus die u selecteert, wanneer u een Windows Defender Application Control-beleid implementeert, kunnen client-Pc's geen HTML-toepassingen met de extensie. HTA uitvoeren.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Een Windows Defender Application Control-beleid maken
1. Klik op **Activa en naleving**op de Configuration Manager-console.
2. Vouw in de werk ruimte **activa en naleving** de optie **Endpoint Protection**uit en klik vervolgens op **Windows Defender Application Control**.
3. Klik op het tabblad **Start** in de groep **maken** op **beleid voor toepassings beheer maken**.
4. Geef op de pagina **Algemeen** van de **wizard beleid voor toepassings beheer maken**de volgende instellingen op:
    - **Naam** : Voer een unieke naam in voor dit Windows Defender Application Control-beleid. 
    - **Beschrijving** : Voer eventueel een beschrijving in voor het beleid waarmee u het kunt herkennen in de Configuration Manager-console.
    - **Een herstart van apparaten afdwingen zodat dit beleid kan worden afgedwongen voor alle processen** -nadat het beleid is verwerkt op een client-PC, wordt opnieuw opstarten gepland op de client volgens de **client instellingen** voor het **opnieuw opstarten**van de computer.
        - Apparaten met Windows 10 versie 1703 of eerder worden altijd automatisch opnieuw gestart.
        - Vanaf Windows 10 versie 1709 worden toepassingen die momenteel op het apparaat worden uitgevoerd, pas nadat de computer opnieuw is opgestart op het nieuwe toepassings beheer beleid toegepast. Toepassingen die worden gestart nadat het beleid van toepassing is, voldoen echter aan het nieuwe beleid voor toepassings beheer. 
    - **Afdwingings modus** : Kies een van de volgende afdwing methoden voor Windows Defender Application Control op de client-PC.
        - **Afdwinging ingeschakeld** : alleen uitvoering van vertrouwde uitvoer bare bestanden toestaan.
        - **Alleen controle** : toestaan dat alle uitvoer bare bestanden worden uitgevoerd, maar niet-vertrouwde uitvoer bare bestanden die worden uitgevoerd in het gebeurtenis logboek van de lokale client worden vastgelegd.
5. Kies op het tabblad **insluitingen** van de **wizard beleid voor toepassings beheer maken**of u **software wilt autoriseren die wordt vertrouwd door de Intelligent Security Graph**.
6. Klik op **toevoegen** als u een vertrouwens relatie wilt toevoegen voor specifieke bestanden of mappen op pc's. In het dialoog venster **vertrouwd bestand of map toevoegen** kunt u een lokaal bestand of een mappad opgeven dat u wilt vertrouwen. U kunt ook een pad naar een bestand of map opgeven op een extern apparaat waarop u gemachtigd bent om verbinding te maken. Wanneer u een vertrouwens relatie toevoegt voor specifieke bestanden of mappen in een Windows Defender Application Control-beleid, kunt u het volgende doen:
    - Problemen oplossen met het gedrag van beheerde installatie Programma's
    - Regel-of-Business-Apps vertrouwen die niet met Configuration Manager kunnen worden geïmplementeerd
    - Vertrouw apps die zijn opgenomen in een installatie kopie van een besturings systeem. 
8. Klik op **volgende**om de wizard te volt ooien.

>[!IMPORTANT]
>Het opnemen van vertrouwde bestanden of mappen wordt alleen ondersteund op client-Pc's waarop versie 1706 of hoger van de Configuration Manager-client wordt uitgevoerd. Als er insluitings regels zijn opgenomen in een Windows Defender Application Control-beleid en het beleid vervolgens wordt geïmplementeerd op een client computer met een eerdere versie op de Configuration Manager-client, wordt het beleid niet toegepast. Dit probleem wordt opgelost als u deze oudere clients bijwerkt. Beleids regels die geen insluitings regels bevatten, kunnen nog steeds worden toegepast op oudere versies van de Configuration Manager-client.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Een Windows Defender Application Control-beleid implementeren
1. Klik op **Activa en naleving**op de Configuration Manager-console.
2. Vouw in de werk ruimte **activa en naleving** de optie **Endpoint Protection**uit en klik vervolgens op **Windows Defender Application Control**.
3. Selecteer in de lijst met beleids regels het beleid dat u wilt implementeren en klik vervolgens op het tabblad **Start** in de groep **implementatie** op **beleid voor toepassings beheer implementeren**.
4. Selecteer in het dialoog venster **beleid voor toepassings beheer implementeren** de verzameling waarvoor u het beleid wilt implementeren. Configureer vervolgens een schema voor wanneer clients het beleid evalueren. Selecteer ten slotte of de client het beleid kan evalueren buiten het geconfigureerde onderhouds venster.
5. Wanneer u klaar bent, klikt u op **OK** om het beleid te implementeren. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Een beleid voor Windows Defender-toepassings beheer controleren

Gebruik de informatie in het artikel [nalevings instellingen controleren](../../compliance/deploy-use/monitor-compliance-settings.md) om u te helpen controleren of het geïmplementeerde beleid correct is toegepast op alle pc's.

Als u de verwerking van een Windows Defender-toepassings beheer beleid wilt controleren, gebruikt u het volgende logboek bestand op client-Pc's:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Als u wilt controleren of de specifieke software die wordt geblokkeerd of gecontroleerd, raadpleegt u de volgende gebeurtenis logboeken van de lokale client:

1. Voor het blok keren en controleren van uitvoer bare bestanden, kunt u met **toepassingen en services**  >  **micro soft**  >  **Windows**-  >  **code-integriteit**  >  **operationeel**vastleggen.
2. Voor het blok keren en controleren van Windows Installer-en script bestanden, gebruikt u **toepassingen en services**om  >  **micro soft**  >  **Windows**  >  **AppLocker**  >  **MSI en script**te gebruiken.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-windows-defender-application-control"></a>Beveiligings-en privacy-informatie voor Windows Defender Application Control

- In deze voorlopige versie moet u Windows Defender Application Control-beleid niet implementeren met de controle van de afdwingings modus **alleen** in een productie omgeving. Deze modus is bedoeld om u te helpen de mogelijkheid alleen in een Lab-instelling te testen.
- Apparaten waarop een beleid is geïmplementeerd in de modus **alleen controle** of **afdwinging** die niet opnieuw is gestart om het beleid af te dwingen, zijn kwetsbaar voor niet-vertrouwde software die wordt geïnstalleerd.
In dit geval kan de software blijven worden uitgevoerd, zelfs als het apparaat opnieuw wordt opgestart of als er een beleid wordt gebruikt in de modus **afdwinging** .
- Om ervoor te zorgen dat het beleid voor toepassings beheer van Windows Defender effectief is, moet u het apparaat voorbereiden in een test omgeving. Implementeer vervolgens het beleid voor **afdwinging** en start het apparaat opnieuw op voordat u het apparaat aan een eind gebruiker geeft.
- Implementeer geen beleid waarvoor **afdwinging is ingeschakeld**en implementeer het beleid later met **alleen controle** op hetzelfde apparaat. Deze configuratie kan ertoe leiden dat niet-vertrouwde software mag worden uitgevoerd.
- Wanneer u Configuration Manager gebruikt om Windows Defender Application Control in te scha kelen op client-Pc's, wordt het beleid niet voor komen dat gebruikers met lokale beheerders rechten het beleid voor toepassings beheer omzeilen of anderszins niet-vertrouwde software kunnen uitvoeren. 
- De enige manier om te voor komen dat gebruikers met lokale beheerders rechten toepassings beheer uitschakelen, is door een ondertekend binair beleid te implementeren. Deze implementatie is mogelijk via groepsbeleid, maar wordt momenteel niet ondersteund in Configuration Manager.
- Het instellen van Configuration Manager als een beheerd installatie programma op client-Pc's maakt gebruik van AppLocker-beleid. AppLocker wordt alleen gebruikt voor het identificeren van beheerde installatie Programma's en alle afdwinging treedt op met Windows Defender Application Control. 

## <a name="next-steps"></a>Volgende stappen

 [Instellingen voor antimalware-beleid en firewalls beheren](endpoint-antimalware-firewall.md)
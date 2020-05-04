---
title: Configuratie-items maken voor Windows 10
titleSuffix: Configuration Manager
description: Gebruik het configuratie-item voor Windows 10 om instellingen te beheren voor Windows 10-computers die worden beheerd door de Configuration Manager-client.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9a1bda440ab3ccd02432f0b023a134b9f54cdafb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712398"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>Configuratie-items maken voor Windows 10-apparaten

Gebruik het configuratie-item Configuration Manager **Windows 10** om instellingen te beheren voor Windows 10-computers die worden beheerd door de Configuration Manager-client.  
  
> [!IMPORTANT]  
>  Als u in deze release een **wachtwoord** instelling hebt gemaakt als onderdeel van een configuratie-item van het type **Windows 10** (voor een apparaat dat wordt beheerd met de Configuration Manager-client), moet u rekening houden met het volgende probleem. Als de instelling nog niet bestaat of niet is geconfigureerd op het Windows 10-apparaat, wordt deze onjuist geëvalueerd als compatibel.  
>   
>  Wanneer u een instelling voor deze apparaten maakt, kunt u er als tijdelijke oplossing voor zorgen dat **Niet-compliante instellingen herstellen** is geselecteerd op de pagina's met instellingen van de wizard Configuratie-item maken. Als u bovendien een configuratie basislijn met een Windows 10-configuratie-item met wachtwoord instellingen implementeert, selecteert u regels die niet **compliant zijn herstellen wanneer**deze worden ondersteund. U maakt deze selectie in het dialoog venster configuratie basislijnen implementeren. Met deze tijdelijke oplossing wordt de instelling gecontroleerd en hersteld als deze niet compatibel is. Na herstel wordt de instelling correct gerapporteerd als **compatibel** (tenzij er een probleem is opgetreden, in welk geval wordt er een **fout**melding weer gegeven).  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Een Windows 10-configuratie-item maken  
  
1. Selecteer in de Configuration Manager-console **activa en naleving**.  
  
2. Vouw in de werk ruimte **activa en naleving** de sectie **instellingen voor naleving**uit en selecteer vervolgens **configuratie-items**.  
  
3. Selecteer **configuratie-item maken**in het tabblad **Start** , in de groep **maken** .  
  
4. Geef op de pagina **Algemeen** van de wizard **configuratie-item maken** een naam en een optionele beschrijving voor het configuratie-item op.  
  
5. Selecteer onder **Geef het type configuratie-item op dat u wilt maken**de optie **Windows 10**.  
  
6. Selecteer **Categorieën**als u categorieën maakt en toewijst om configuratie-items te zoeken en te filteren in de Configuration Manager-console.  
  
7. Selecteer op de pagina **Ondersteunde platforms** van de wizard de specifieke Windows 10-platforms die het configuratie-item evalueren.  
  
8. Op de pagina **Apparaatinstellingen** van de wizard selecteert u de instellingengroep die u wilt configureren. (Zie de [Windows 10-configuratie-item instellingen](#BKMK_Ref) in dit artikel voor meer informatie.) Selecteer **volgende**.  
  
   > [!TIP]  
   >  Als de instelling die u wilt, niet wordt weer gegeven, selecteert u het **selectie vakje aanvullende instellingen configureren die niet in het veld standaard instellings groepen staan**.  
  
9. Configureer op elke pagina instellingen de instellingen die u nodig hebt en of u deze wilt herstellen wanneer ze niet compatibel zijn op apparaten (wanneer dit wordt ondersteund).  
  
10. U kunt voor elke instellingen groep ook de ernst configureren die wordt gerapporteerd wanneer wordt vastgesteld dat een configuratie-item niet compliant is:  
  
    -   **Geen**: voor apparaten die niet voldoen aan deze nalevings regel wordt geen fout Ernst gerapporteerd voor Configuration Manager-rapporten.  
  
    -   **Informatie**: voor apparaten die niet voldoen aan deze compliantie regel wordt de fout Ernst **informatie** voor Configuration Manager-rapporten gerapporteerd.  
  
    -   **Waarschuwing**: voor apparaten die niet voldoen aan deze compliantie regel wordt de fout Ernst **waarschuwing** gerapporteerd voor Configuration Manager-rapporten.  
  
    -   **Kritiek**: voor apparaten die niet voldoen aan deze compliantie regel wordt de fout Ernst **kritiek** gerapporteerd voor Configuration Manager-rapporten.  
  
    -   **Kritiek met gebeurtenis**: voor apparaten die niet voldoen aan deze compliantie regel wordt de fout Ernst **kritiek** gerapporteerd voor Configuration Manager-rapporten. Dit ernstniveau wordt ook vastgelegd als een Windows-gebeurtenis in het logboek voor toepassingsgebeurtenissen.  
  
11. Op de pagina **platform toepas baarheid** van de wizard controleert u alle instellingen die niet compatibel zijn met de ondersteunde platforms die u eerder hebt geselecteerd. U kunt teruggaan en deze instellingen verwijderen of u kunt doorgaan.  
  
    > [!TIP]  
    >  Niet-ondersteunde instellingen worden niet beoordeeld op compliantie.  
  
12. Voltooi de wizard.  
  
    U kunt het nieuwe configuratie-item weergeven in het knooppunt **Configuratie-items** van de werkruimte **Activa en naleving** .  
  
## <a name="windows-10-configuration-item-settings-reference"></a><a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>Wachtwoord  
  
|Instelling|Details|  
|-------------|-------------|  
|**Wachtwoordinstellingen vereisen op mobiele apparaten**|Vereist een wacht woord op ondersteunde apparaten.|  
|**Minimale wachtwoordlengte (tekens)**|Het minimum aantal tekens voor het wachtwoord.|  
|**Wachtwoordverlooptijd in dagen**|Het aantal dagen voordat het wachtwoord moet worden gewijzigd.|  
|**Aantal onthouden wachtwoorden**|Hiermee wordt voor komen dat eerdere wacht woorden opnieuw worden gebruikt.|  
|**Aantal mislukte aanmeldingspogingen voordat het apparaat wordt gewist**|Hiermee wordt het apparaat gewist als het aanmelden dit aantal keren mislukt.|  
|**Niet-actieve periode waarna apparaat wordt vergrendeld**|Hiermee geeft u op hoeveel minuten het apparaat inactief moet zijn voordat het automatisch wordt vergrendeld.|  
|**Wachtwoordcomplexiteit**|Kies of u een pincode kunt opgeven, zoals ' 1234 ', of dat u een sterk wacht woord moet invoeren.|
|**Aantal complexe teken sets dat is vereist in het wacht woord**|Als u een **sterk** wacht woord hebt geselecteerd, gebruikt u deze instelling om het aantal complexe teken sets dat is vereist, te configureren. Voor een sterk wacht woord moet deze instelling worden ingesteld op ten minste **3**, wat betekent dat zowel letters als cijfers zijn vereist. Selecteer **4** als u een wacht woord wilt afdwingen dat extra tekens vereist, zoals **(% $**).<br>(Alleen Windows 10)  |
  
###  <a name="device"></a>Apparaat  
  
|Naam van instelling|Details|  
|------------------|-------------|  
|**Bluetooth**|Staat het gebruik van de Bluetooth-functie op het apparaat toe.|  
  
### <a name="cloud"></a>Cloud  
  
|Naam van instelling|Details|  
|------------------|-------------|  
|**Synchronisatie van instellingen**|De synchronisatie van instellingen tussen apparaten toestaan.|  
|**Synchronisatie van referenties**|De synchronisatie van referenties tussen apparaten toestaan.|  
|**Synchronisatie van instellingen via verbindingen met een datalimiet**|Hiermee kunnen instellingen worden gesynchroniseerd wanneer de Internet verbinding wordt gemeten.|  
  
### <a name="roaming"></a>Roaming  
  
|Naam van instelling|Details|  
|------------------|-------------|  
|**Gegevens roaming**|Staat roaming tussen netwerken toe tijdens het verkrijgen van toegang tot gegevens.|  
  
### <a name="encryption"></a>Versleuteling  
  
|Naam van instelling|Details|  
|------------------|-------------|  
|**Bestandsversleuteling op apparaat**|Vereist dat bestanden op het apparaat zijn versleuteld.|  
  
### <a name="system-security"></a>Systeembeveiliging  
  
|Naam van instelling|Details|  
|------------------|-------------|  
|**Gebruikersaccountbeheer**|Hiermee configureert u hoe Windows Gebruikersaccountbeheer werkt op het apparaat.<br />U kunt het bijvoorbeeld uitschakelen of het niveau instellen waarbij u een melding moet ontvangen.|  
|**Netwerkfirewall**|Schakelt de Windows-firewall in of uit.|  
|**SmartScreen**|Hiermee wordt Windows SmartScreen in-of uitgeschakeld.|  
|**Virusbeveiliging**|Hiermee vereist u dat antivirussoftware wordt geïnstalleerd en geconfigureerd.|  
|**Handtekeningen voor virusbeveiliging zijn bijgewerkt**|Hiervoor moet de handtekening bestanden voor de antivirus software op het apparaat up-to-date zijn.|  
  
### <a name="windows-information-protection"></a>Windows Information Protection

Met de toename van apparaten die eigendom zijn van werk nemers in de onderneming, is er ook een verhoogd risico op onbedoeld gegevens lekken via apps en services, zoals e-mail, sociale media en de open bare Cloud. Deze bevinden zich buiten het besturings element van de organisatie. Voor beelden zijn wanneer een werk nemer:

- Verzendt de nieuwste technische afbeeldingen vanuit hun persoonlijke e-mail account.
- Hiermee worden product gegevens in een Tweet gekopieerd en geplakt.
- Hiermee wordt een omzet rapport in uitvoering opgeslagen naar de open bare Cloud opslag.

Met Windows Information Protection (WIP, voorheen Enter prise Data Protection) kunt u zich beschermen tegen deze mogelijke gegevens lekkage, zonder dat dit de ervaring van de werk nemer verstoort. WIP helpt ook zakelijke apps en gegevens te beschermen tegen onbedoelde gegevens lekken op apparaten in bedrijfs eigendom en persoonlijke apparaten die werk nemers meenemen. OHW vereist geen wijzigingen in uw omgeving of andere apps.

Configuration Manager configuratie-items van Windows Information Protection het volgende beheren:

- De lijst met apps die worden beveiligd door OHW
- Netwerk locaties van het bedrijf
- Beveiligings niveau
- Versleutelingsinstellingen
  
Zie voor informatie over het configureren van OHW met Configuration Manager:

- [Uw bedrijfs gegevens beveiligen met behulp van Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Een beleid voor Windows Information Protection (WIP) maken en implementeren met behulp van Configuration Manager](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [Beperkingen bij het gebruik van Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## <a name="see-also"></a>Zie ook  
[Configuratie-items voor apparaten die worden beheerd met de Configuration Manager-client](../../compliance/deploy-use/create-configuration-items.md)

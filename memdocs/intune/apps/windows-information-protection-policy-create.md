---
title: WIP-appbeveiligingsbeleid (Windows Information Protection)
titleSuffix: Microsoft Intune
description: 'Met Microsoft Intune WIP-beleid (WIP: Windows Information Protection) maken en implementeren'
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/25/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4e3627bd-a9fd-49bc-b95e-9b7532f0ed55
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88eabe07cadf45644f3e10be338a23454c5d1711
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911978"
---
# <a name="create-and-deploy-windows-information-protection-wip-policy-with-intune"></a>Met Intune WIP-beleid (WIP: Windows Information Protection) maken en implementeren

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

U kunt WIP-beleid gebruiken met Windows 10-apps om apps zonder apparaatinschrijving te beveiligen.

## <a name="before-you-begin"></a>Voordat u begint

U moet enkele concepten begrijpen voor het toevoegen van WIP-beleid:

### <a name="list-of-allowed-and-exempt-apps"></a>Lijst met toegestane en vrijgestelde apps

- **Beveiligde apps:** dit zijn de apps die aan dit beleid moeten voldoen.

- **Vrijgestelde apps:** deze apps zijn vrijgesteld van dit beleid en hebben zonder beperkingen toegang tot bedrijfsgegevens.

### <a name="types-of-apps"></a>Typen apps

- **Aanbevolen apps:** een vooraf gevulde lijst met apps (voornamelijk van Microsoft Office) die u gemakkelijk in het beleid kunt importeren.
- **Store-apps:** u kunt elke app uit Microsoft Store toevoegen aan het beleid.
- **Windows-bureaublad-apps:** u kunt traditionele Windows-bureaublad-apps toevoegen aan het beleid (zoals .exe, of .dll)

## <a name="prerequisites"></a>Vereisten

U moet de MAM-provider configureren voordat u een WIP-beleid kunt maken. Meer informatie over [de configuratie van uw MAM-provider met Intune](app-protection-policies-configure-windows-10.md).  

> [!IMPORTANT]
> WIP biedt geen ondersteuning voor meerdere identiteiten; er kan slechts één beheerde identiteit tegelijkertijd bestaan. Zie [Uw ondernemingsgegevens beveiligen met Windows Information Protection (WIP)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip) voor meer informatie over de mogelijkheden en beperkingen van WIP.

U moet bovendien beschikken over de volgende licentie en update:

- Een [Azure AD Premium](/azure/active-directory/active-directory-get-started-premium)-licentie
- [Update voor Windows Creators](https://blogs.windows.com/windowsexperience/2017/04/11/how-to-get-the-windows-10-creators-update/#o61bC2PdrHslHG5J.97)





## <a name="to-add-a-wip-policy"></a>WIP-beleid toevoegen

Nadat u Intune hebt ingesteld in uw organisatie, kunt u specifiek WIP-beleid maken.

> [!TIP]  
> Zie [Een WIP-beleid (Windows Information Protection) maken met MAM via Azure Portal voor Microsoft Intune](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-mam-intune-azure) in de Windows-bibliotheek voor beveiligingsdocumentatie voor gerelateerde informatie over het maken van een WIP-beleid voor Intune, waaronder de beschikbare instellingen en hoe u deze configureert. 


1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **App-beveiligingsbeleid** > **Beleid maken**.
3. Voeg de volgende waarden toe:
    - **Naam:** typ een naam (vereist) voor het nieuwe beleid.
    - **Beschrijving:** (optioneel) typ een beschrijving.
    - **Platform:** Kies **Windows 10** als het ondersteunde platform voor uw WIP-beleid.
    - **Status van de inschrijving:** kies **Zonder inschrijving** als status van de inschrijving voor het beleid.
4. Kies **Maken**. Het beleid wordt gemaakt en weergegeven in de tabel in het deelvenster **App-beveiligingsbeleid**.

## <a name="to-add-recommended-apps-to-your-protected-apps-list"></a>Aanbevolen apps toevoegen aan de lijst met beschermde apps

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Beleid voor app-beveiliging**.
3. Kies het beleid dat u wilt wijzigen in het deelvenster **App-beveiligingsbeleid**. Het deelvenster **Intune-app-beveiliging** wordt weergegeven.
4. Kies **Beveiligde apps** in het deelvenster **Intune-app-beveiliging**. Het deelvenster **Beveiligde apps** wordt geopend, waarop alle apps worden weergegeven die al zijn opgenomen in de lijst voor het beveiligingsbeleid voor deze app.
5. Selecteer **Apps toevoegen**. In **Apps toevoegen** ziet u een lijst gefilterde apps. Met de lijst boven in het deelvenster kunt u de lijstfilter wijzigen.
6. Selecteer elke app die u toegang wilt bieden tot uw bedrijfsgegevens.
7. Klik op **OK**. Het deelvenster **Beveiligde apps** wordt bijgewerkt met alle geselecteerde apps.
8. Klik op **Opslaan**.

## <a name="add-a-store-app-to-your-protected-apps-list"></a>Een Store-app toevoegen aan de lijst met beschermde apps

**Een Store-app toevoegen**

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Beleid voor app-beveiliging**.
3. Kies het beleid dat u wilt wijzigen in het deelvenster **App-beveiligingsbeleid**. Het deelvenster **Intune-app-beveiliging** wordt weergegeven.
4. Kies **Beveiligde apps** in het deelvenster **Intune-app-beveiliging**. Het deelvenster **Beveiligde apps** wordt geopend, waarop alle apps worden weergegeven die al zijn opgenomen in de lijst voor het beveiligingsbeleid voor deze app.
5. Selecteer **Apps toevoegen**. In **Apps toevoegen** ziet u een lijst gefilterde apps. Met de lijst boven in het deelvenster kunt u de lijstfilter wijzigen.
6. In de lijst selecteert u **Store-apps**.
7. Voer waarden in voor **Naam**, **Uitgever**, **Productnaam** en **Actie**. Stel de waarde van **Actie** in op **Toestaan** zodat de app toegang heeft tot uw zakelijke gegevens.
9. Klik op **OK**. Het deelvenster **Beveiligde apps** wordt bijgewerkt met alle geselecteerde apps.
10. Klik op **Opslaan**.

## <a name="add-a-desktop-app-to-your-protected-apps-list"></a>Een desktop-app toevoegen aan de lijst met beschermde apps

**Een bureaublad-app toevoegen**
1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Beleid voor app-beveiliging**.
3. Kies het beleid dat u wilt wijzigen in het deelvenster **App-beveiligingsbeleid**. Het deelvenster **Intune-app-beveiliging** wordt weergegeven.
4. Kies **Beveiligde apps** in het deelvenster **Intune-app-beveiliging**. Het deelvenster **Beveiligde apps** wordt geopend, waarop alle apps worden weergegeven die al zijn opgenomen in de lijst voor het beveiligingsbeleid voor deze app.
5. Selecteer **Apps toevoegen**. In **Apps toevoegen** ziet u een lijst gefilterde apps. Met de lijst boven in het deelvenster kunt u de lijstfilter wijzigen.
6. In de lijst selecteert u **Bureaublad-apps**.
7. Voer waarden in voor **Naam**, **Uitgever**, **Productnaam**, **Bestand**, **Minimale versie**, **Maximale versie** en **Actie**. Stel de waarde van **Actie** in op **Toestaan** zodat de app toegang heeft tot uw zakelijke gegevens.
9. Klik op **OK**. Het deelvenster **Beveiligde apps** wordt bijgewerkt met alle geselecteerde apps.
10. Klik op **Opslaan**.

## <a name="wip-learning"></a>WIP Learning
Nadat u de apps hebt toegevoegd die u wilt beveiligen met WIP, moet u een beveiligingsmodus toepassen via **WIP Learning**.

### <a name="before-you-begin"></a>Voordat u begint

WIP Learning is een rapport waarmee u uw apps met WIP-functionaliteit en uw voor WIP onbekende apps in de gaten kunt houden. Onbekende apps zijn apps die niet zijn geïmplementeerd door de IT-afdeling van uw organisatie. U kunt deze apps uit het rapport exporteren en toevoegen aan uw WIP-beleid om te voorkomen dat de productiviteit wordt onderbroken voordat WIP in de modus Blokkeren wordt afgedwongen.

<!-- 1631908 -->
Er wordt informatie over WIP-apps weergegeven en u kunt een overzicht bekijken van de apparaten die zakelijke gegevens hebben gedeeld met websites. Met deze informatie kunt u bepalen welke websites er moeten worden toegevoegd aan WIP-beleid voor groepen en gebruikers. In het overzicht ziet u welke website-URL's worden gebruikt door apps waarvoor WIP is ingeschakeld.

Wanneer u met apps met WIP-functionaliteit en voor WIP onbekende apps werkt, wordt het aanbevolen dat u start met **Stil** of **Onderdrukkingen toestaan** als u met een kleine groep controleert of de juiste apps in de lijst met beschermde apps staan. Vervolgens kunt u uw uiteindelijke afdwingingsbeleid wijzigen via **Blokkeren**.

### <a name="what-are-the-protection-modes"></a>Wat zijn de beveiligingsmodi ?

#### <a name="block"></a>Blokkeren
WIP zoekt naar ongeschikte gegevensuitwisselingsprocedures en zorgt ervoor dat de gebruiker de actie niet verder kan uitvoeren. Geblokkeerde acties kan ook het delen van gegevens in niet-zakelijke beveiligde apps en het delen van bedrijfsgegevens met personen en apparaten buiten uw organisatie omvatten.

#### <a name="allow-overrides"></a>Onderdrukkingen toestaan
WIP zoekt naar het delen van onjuiste gegevens en waarschuwt gebruikers als ze een onveilige actie uitvoeren. In deze modus kan de gebruiker echter het beleid negeren en de gegevens delen, waarbij de actie wordt toegevoegd aan uw controlelogboek.

#### <a name="silent"></a>Achtergrond
WIP wordt op de achtergrond uitgevoerd en maakt een registratie van onjuiste gegevensdeling, zonder dat een actie wordt geblokkeerd waarvoor de interactie van een werknemer is vereist in de modus Onderdrukkingen toestaan. Acties die niet zijn toegestaan, zoals apps die ten onrechte toegang willen krijgen tot een netwerkbron of door WIP beveiligde gegevens, worden echter onderbroken.

#### <a name="off-not-recommended"></a>Uit (niet aanbevolen)
WIP is uitgeschakeld en uw gegevens worden niet beveiligd of gecontroleerd.

Als u WIP hebt uitgeschakeld, wordt een poging gedaan om door WIP gemarkeerde bestanden op de lokaal aangesloten schijven te ontsleutelen. Let erop dat de vorige gegevens over de ontsleuteling en het beleid niet automatisch worden toegepast als u de WIP-beveiliging weer inschakelt.

### <a name="add-a-protection-mode"></a>Beschermingsmodus toevoegen

1. Kies in het deelvenster **App-beleid** de naam van uw beleid en kies vervolgens **Verplichte instellingen**.

    ![Schermopname van het deelvenster Oefenmodus](./media/windows-information-protection-policy-create/learning-mode-sc1.png)

1. Selecteer een instelling en kies vervolgens **Opslaan**.

### <a name="use-wip-learning"></a>WIP Learning gebruiken

1. Open [Azure Portal](https://portal.azure.com). Kies **Alle services**. Type **Intune** in het tekstvakfilter.

3. Kies **Intune-**  > **Apps**.

4. Kies **Status van de app-beveiliging** > **Rapporten** > **Kennismaken met Windows Information Protection**.  

    Zodra de apps worden weergegeven in het rapport voor de logboekregistratie van WIP, kunt u deze toevoegen aan de beveiligingsbeleidsregels voor uw app.

## <a name="allow-windows-search-indexer-to-search-encrypted-items"></a>De Windows Search-indexeerfunctie toestaan om versleutelde items te zoeken
Hiermee kunt u het indexeren van items toestaan of verbieden. Deze schakeloptie dient voor de Windows Search-indexeerfunctie. Hiermee bepaalt u of items die zijn versleuteld, worden geïndexeerd, zoals de bestanden met Windows-gegevensbescherming (WIP).

Deze optie voor app-beveiligingsbeleid bevindt zich in de **geavanceerde instellingen** van het beleid voor Windows-gegevensbescherming. Het beveiligingsbeleid van de app moet worden ingesteld op het *Windows 10*-platform en de **inschrijvingsstatus** van het app-beleid moet worden ingesteld op **Bij inschrijving**.

Wanneer het beleid wordt ingeschakeld, worden de items met WIP-beveiliging geïndexeerd en worden de metagegevens opgeslagen op een niet-versleutelde locatie. De metagegevens bevatten gegevens zoals het bestandspad en de wijzigingsdatum.

Als het beleid is uitgeschakeld, worden de items met WIP-beveiliging niet geïndexeerd en worden ze niet weergegeven in de resultaten in Cortana of Verkenner. Als er te veel mediabestanden met WIP-beveiliging op het apparaat staan, kunnen de prestaties bij gebruik van foto's en Groove-apps ook worden beïnvloed.

## <a name="add-encrypted-file-extensions"></a>Extensies van versleutelde bestanden toevoegen

U kunt niet alleen de optie om de **Windows Search-indexeerfunctie toe te staan om te zoeken naar versleutelde items** gebruiken, maar u kunt ook een lijst bestandsextensies opgeven. De bestanden met deze extensies worden versleuteld wanneer ze vanaf een Server Message Block-share (SMB) binnen het bedrijf worden gekopieerd, zoals gedefinieerd in de lijst netwerklocaties. Als dit beleid niet is opgegeven, wordt het bestaande gedrag voor automatisch versleutelen toegepast. Als dit beleid is geconfigureerd, worden alleen bestanden met de extensies van de lijst versleuteld.

## <a name="deploy-your-wip-app-protection-policy"></a>Uw WIP-beveiligingsbeleid voor apps implementeren

> [!IMPORTANT]
> Deze informatie is van toepassing op WIP zonder apparaatinschrijving.

<!---not sure why you need the Important note. Isn't this what the topic is about? app protection w/o enrollment?--->

Nadat u het beveiligingsbeleid van uw OHW app hebt gemaakt, moet u deze implementeren in uw organisatie met MAM.

1. Kies in het deelvenster **App-beleid** het nieuwe beveiligingsbeleid voor uw app, kies **Gebruikersgroepen** > **Gebruikersgroep toevoegen**.

    Er wordt een lijst met gebruikersgroepen op basis van de beveiligingsgroepen in uw Azure Active Directory geopend in het deelvenster **Gebruikersgroep toevoegen**.

2. Kies de groep waarop u uw beleid wilt toepassen en kies vervolgens **Selecteren** om het beleid te implementeren.

## <a name="next-steps"></a>Volgende stappen

Zie [Uw ondernemingsgegevens beveiligen met Windows-gegevensbescherming (WIP)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip) voor meer informatie over Windows-gegevensbescherming.
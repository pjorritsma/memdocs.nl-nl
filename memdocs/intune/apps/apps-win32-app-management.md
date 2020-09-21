---
title: Win32-app-beheer in Microsoft Intune
titleSuffix: ''
description: Ontdek hoe u Win32-apps beheert met Microsoft Intune. Dit onderwerp bevat een overzicht van de Intune functies voor het leveren en beheren van Win32-apps.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: db28653207d7bf4341d614aeecb769dcc145caaa
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083927"
---
# <a name="win32-app-management-in-microsoft-intune"></a>Win32-app-beheer in Microsoft Intune

Met Microsoft Intune beschikt u over beheermogelijkheden voor Win32-apps. Hoewel cloudklanten Microsoft Endpoint Configuration Manager kunnen gebruiken voor het beheer van Win32-apps, hebben klanten met alleen Intune uitgebreidere beheermogelijkheden voor hun Win32 LOB-apps (Line-Of-Business). Dit document bevat een overzicht van de Intune-beheerfuncties voor Win32-apps en relevante informatie.

> [!NOTE]
> Deze app-beheermogelijkheid biedt ondersteuning voor zowel 32- als 64-bits besturingssysteemarchitecturen voor Windows-toepassingen.

> [!IMPORTANT]
> Wanneer u Win32-apps implementeert, kunt u de [Intune-beheeruitbreiding](../apps/intune-management-extension.md) exclusief gebruiken, met name wanneer u een Win32-app-installatieprogramma voor meerdere bestanden hebt. Als u de installatie van Win32-apps en Line-Of-Business-apps tijdens de Autopilot-registratie combineert, is het mogelijk dat de installatie van de app mislukt. De Intune-beheeruitbreiding wordt altijd automatisch geïnstalleerd wanneer een PowerShell-script of Win32-app wordt toegewezen aan de gebruiker of het apparaat.

## <a name="prerequisites"></a>Vereisten

Als u Win32-app-beheer wilt gebruiken, moet u aan de volgende criteria voldoen:

- Gebruik Windows 10 versie 1607 of hoger (Enterprise, Pro en Education).
- Apparaten moeten worden gekoppeld aan Azure Active Directory (Azure AD) en automatisch ingeschreven. De Intune-beheeruitbreiding biedt ondersteuning voor apparaten die zijn toegevoegd aan Azure AD, aan een hybride domein zijn toegevoegd en via een groepsbeleid zijn ingeschreven. 
  > [!NOTE]
  > Voor het scenario met inschrijving via het groepsbeleid maakt de gebruiker gebruik van het lokale gebruikersaccount om hun Windows 10-apparaat met Azure AD samen te voegen. Gebruikers moeten zich op het apparaat aanmelden met hun Azure AD-gebruikersaccount en zich bij inschrijven bij Intune. Intune installeert de Intune-beheerextensie op het apparaat als een PowerShell-script of een Win32-app op de gebruiker of het apparaat is gericht.
- De grootte van Windows-toepassingen is beperkt tot 8 GB per app.

## <a name="prepare-the-win32-app-content-for-upload"></a>De Win32-app-inhoud voor upload voorbereiden

Voordat u een Win32-app kunt toevoegen aan Microsoft Intune, moet u de app voorbereiden met behulp van het hulpprogramma voor voorbereiding van Microsoft Win32-inhoud. U gebruikt het hulpprogramma voor voorbereiding van Microsoft Win32-inhoud om klassieke Windows-apps (Win32) voor te verwerken. Met het hulpprogramma converteert u de app-installatiebestanden naar de indeling *.intunewin*. Zie [Inhoud van Win32-apps voorbereiden om te uploaden](apps-win32-prepare.md) voor meer informatie en stappen. 

## <a name="add-assign-and-monitor-a-win32-app"></a>Een Win32-app toevoegen, toewijzen en bewaken

Nadat u een [Win32-app hebt voorbereid om te worden geüpload naar Intune](apps-win32-prepare.md) met behulp van het hulpprogramma voor voorbereiding van Microsoft Win32-inhoud, kunt u de app aan Intune toevoegen. Zie [Een Win32-app toevoegen, toewijzen en bewaken in Microsoft Intune](apps-win32-add.md) voor meer informatie en stappen.

## <a name="delivery-optimization"></a>Delivery Optimization

Clients van Windows 10 1709 en hoger downloaden Intune Win32-app-inhoud met behulp van een delivery optimization-onderdeel in de Windows 10-client. Delivery optimization biedt peer-to-peer-functionaliteit die standaard is ingeschakeld. 

U kunt de Delivery Optimization-agent configureren zodat inhoud voor de Win32-app op de achtergrond of voorgrond wordt gedownload op basis van de toewijzing. Delivery Optimization kan worden geconfigureerd via groepsbeleid en via de Intune-apparaatconfiguratie. Raadpleeg [Delivery Optimization voor Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) voor meer informatie. 

> [!NOTE]
> U kunt ook een Microsoft Connected Cache-server op uw Configuration Manager-distributiepunten installeren om inhoud van Intune Win32-apps op te slaan in de cache. Zie [Microsoft Verbonden cache in Configuration Manager](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune) voor meer informatie.

## <a name="install-required-and-available-apps-on-devices"></a>Vereiste installatie en beschikbare apps op apparaten

De gebruiker ziet Windows-meldingen voor de vereiste en beschikbare app-installaties. De volgende afbeelding toont een voorbeeld van een melding dat de app-installatie pas wordt voltooid wanneer het apparaat opnieuw wordt opgestart. 

![Schermafbeelding van Windows-meldingen voor een app-installatie.](./media/apps-win32-app-management/apps-win32-app-08.png)    

De volgende afbeelding informeert de gebruiker dat er app-wijzigingen worden aangebracht aan het apparaat.

![Schermafbeelding die aan de gebruiker meldt dat er wijzigingen aan de app worden uitgevoerd.](./media/apps-win32-app-management/apps-win32-app-09.png)    

Verder worden in de bedrijfsportal-app meer berichten over de status van de app-installatie weergegeven voor gebruikers. De volgende voorwaarden zijn van toepassing op Win32-afhankelijkheidsfuncties:
- De app kon niet worden geïnstalleerd. Er is niet voldaan aan afhankelijkheden die zijn gedefinieerd door de beheerder.
- De app is geïnstalleerd, maar moet opnieuw worden opgestart.
- De app wordt momenteel geïnstalleerd, maar moet opnieuw worden opgestart om door te gaan.

## <a name="set-win32-app-availability-and-notifications"></a>Beschikbaarheid en meldingen voor Win32-apps instellen
U kunt de begintijd en deadline voor een Win32-app configureren. Bij de begintijd start de Intune-beheerextensie het downloaden van de app-inhoud en slaat deze op in de cache voor de vereiste intentie. De app wordt geïnstalleerd op het tijdstip van de deadline. 

Voor beschikbare apps bepaalt de begintijd wanneer de app wordt weergegeven in de bedrijfsportal en wordt de inhoud gedownload wanneer de gebruiker de app vanuit de bedrijfsportal aanvraagt. U kunt ook een respijtperiode voor opnieuw opstarten inschakelen. 

> [!IMPORTANT]
> De instelling **Respijtperiode opnieuw opstarten** in het gedeelte **Toewijzing** is alleen beschikbaar wanneer het **Gedrag apparaat bij opnieuw starten** van het gedeelte **Programma** is ingesteld op een van de volgende opties:
> - **Gedrag op basis van retourcodes bepalen**
> - **Via Intune wordt opnieuw opstarten van het apparaat afgedwongen**

Stel de beschikbaarheid van de app in op basis van een datum en tijd voor een vereiste app door de volgende stappen uit te voeren:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Alle apps**.
3. Selecteer een app in de lijst met **Windows-apps (Win32)** . 
4. Selecteer in het app-deelvenster **Eigenschappen** > **Bewerken** naast het gedeelte **Toewijzingen**. Selecteer vervolgens **Groep toevoegen** onder het toewijzingstype **Vereist**. 
   
   De beschikbaarheid van apps kan worden ingesteld op basis van het toewijzingstype. **Toewijzingstype** kan **Vereist**, **Beschikbaar voor ingeschreven apparaten** of **Verwijderen** zijn.
5. Selecteer een groep in het deelvenster **Groep selecteren** om aan te geven aan welke groep gebruikers de app moet worden toegewezen. 

    > [!NOTE]
    > Opties voor **Toewijzingstype** zijn:<br>
    > - **Vereist**: U kunt kiezen voor **Deze app vereist maken voor alle gebruikers** en/of **Deze app vereist te maken op alle apparaten**.<br>
    > - **Beschikbaar voor ingeschreven apparaten**: U kunt kiezen voor **Deze app beschikbaar maken voor alle gebruikers met ingeschreven apparaten**.<br>
    > - **Verwijderen**: U kunt kiezen voor **Deze app verwijderen voor alle gebruikers** en/of **Deze app verwijderen van alle apparaten**.

6. Als u de opties voor **Melding voor de eindgebruiker** wilt wijzigen, selecteert u **Alle pop-upmeldingen weergeven**.
7. Stel in het deelvenster **Toewijzing bewerken** de **Meldingen voor eindgebruiker** in op **Alle pop-upmeldingen weergeven**. U kunt **Meldingen van eindgebruiker** instellen op **Alle pop-upmeldingen weergeven**, **Pop-upmeldingen voor de computer opnieuw opstarten weergeven** of **Alle pop-upmeldingen verbergen**.
8. Stel **App-beschikbaarheid** in op **Een specifieke datum en tijd** en selecteer de datum en tijd. Deze datum en tijd geven aan wanneer de app is gedownload naar het apparaat van de gebruiker. 
9. Stel **Deadline voor app-installatie** in op **Een specifieke datum en tijd** en selecteer de datum en tijd. Deze datum en tijd geven aan wanneer de app is geïnstalleerd op het apparaat van de gebruiker. Wanneer meer dan één toewijzing wordt gemaakt voor dezelfde gebruiker of hetzelfde apparaat, wordt de deadline voor de installatie van de app gekozen op basis van de vroegst mogelijke tijd.

10. Selecteer **Ingeschakeld** naast de **Respijtperiode voor opnieuw opstarten**. De respijtperiode voor opnieuw opstarten gaat in zodra de installatie van de app op het apparaat is voltooid. Wanneer de instelling is uitgeschakeld, kan het apparaat zonder waarschuwing opnieuw worden opgestart. 

    U kunt de volgende opties aanpassen:
    
    - **Respijtperiode voor opnieuw opstarten van apparaat (in minuten)** : De standaardwaarde is 1440 minuten (24 uur). Deze waarde kan maximaal 2 weken zijn.
    - **Selecteer wanneer u het afteldialoogvenster voor opnieuw opstarten wilt weergeven voordat het opnieuw opstarten plaatsvindt (in minuten)** : De standaardwaarde is 15 minuten.
    - **Gebruiker toestaan de melding voor opnieuw opstarten uit te stellen**: U kunt kiezen tussen **Ja** en **Nee**.
        - **De uitstelduur (in minuten) selecteren**: De standaardwaarde is 240 minuten (4 uur). Het uitstel mag niet langer zijn dan de respijtperiode voor opnieuw opstarten.

11. Selecteer **Beoordelen en opslaan**.

## <a name="notifications-for-win32-apps"></a>Meldingen voor Win32-apps 
Indien nodig, kunt u per app-toewijzing onderdrukken dat meldingen voor gebruikers worden weergegeven. Selecteer vanuit Intune de optie **Apps** > **Alle apps** > *de app* > **Toewijzingen** > **Groepen opnemen**. 

> [!NOTE]
> Win32-apps die via de Intune-beheerextensie zijn geïnstalleerd, worden niet verwijderd van apparaten die niet meer ingeschreven zijn. Beheerders kunnen gebruikmaken van uitsluiting van toewijzingen, zodat Win32-apps niet worden aangeboden op BYOD-apparaten (Bring Your Own Device).

## <a name="next-steps"></a>Volgende stappen

- Zie [Apps toevoegen aan Microsoft Intune](apps-add.md) voor meer informatie over apps toevoegen aan Intune.

---
title: Op rollen gebaseerd toegangsbeheer (RBAC) en bereiktags voor gedistribueerde IT in Intune | Microsoft Docs
description: Bereiktags gebruiken voor het filteren van configuratieprofielen op specifieke rollen.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: a21d3039-f2ed-4f43-b6fa-d00c071edbc4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 665b88932c88f523b19fec596bfd969bb93ecdd4
ms.sourcegitcommit: 5f15a3abf33ce7bfd6855ffeef2ec3cd4cd48a7f
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721904"
---
# <a name="use-role-based-access-control-rbac-and-scope-tags-for-distributed-it"></a>Op rollen gebaseerd toegangsbeheer (RBAC) en bereiktags gebruiken voor gedistribueerde IT

U kunt op rollen gebaseerd toegangsbeheer (RBAC) en bereiktags gebruiken om ervoor te zorgen dat de juiste beheerders de juiste toegang tot en zichtbaarheid van de juiste Intune-objecten hebben. Rollen bepalen welke toegang beheerders hebben tot welke objecten. Bereiktags bepalen welke objecten zichtbaar zijn voor beheerders.

Stel bijvoorbeeld dat een beheerder van het regionale kantoor in Seattle de rol van beleids- en profielbeheerder heeft. U wilt dat deze beheerder alleen de profielen en beleidsregels ziet en beheert die van toepassing zijn op de apparaten in Seattle. Als u deze toegang wilt instellen, doet u het volgende:

1. Maak een bereiktag met de naam Seattle.
2. Maak een roltoewijzing voor de rol beleids- en profielbeheerder met: 
    - Leden (groepen) = een beveiligingsgroep met de naam IT-beheerders in Seattle. Alle beheerders in deze groep hebben toestemming voor het beheren van beleidsregels en profielen voor gebruikers/apparaten binnen het bereik (Groepen).
    - Bereik (Groepen) = een beveiligingsgroep met de naam gebruikers in Seattle. Alle gebruikers/apparaten in deze groep kunnen hun profielen en beleidsregels laten beheren door de beheerders in Leden (Groepen). 
    - Bereik(tags) = Seattle. Beheerders in Leden (Groepen) zien Intune-objecten die ook de bereiktag Seattle hebben.
3. Voeg de bereiktag Seattle toe aan beleidsregels en profielen waartoe beheerders in Leden (Groepen) toegang moeten hebben.
4. Voeg de bereiktag Seattle toe aan apparaten die zichtbaar moeten zijn voor beheerders in Leden (Groepen). 

## <a name="default-scope-tag"></a>Standaardbereiktag
De standaard bereiktag wordt automatisch toegevoegd aan alle niet-getagde objecten die ondersteuning bieden voor bereiktags.

Deze functie voor standaardbereiktags is vergelijkbaar met de functie voor beveiligingsbereiken in Microsoft Endpoint Configuration Manager. 

## <a name="to-create-a-scope-tag"></a>Een bereiktag maken

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Tenantbeheer** > **Rollen** > **Bereik (tags)**  > **Maken**.
2. Geef op de pagina **Basisinformatie** een waarde op voor **Naam** en eventueel ook voor **Beschrijving**. Kies **Volgende**.
3. Kies op de pagina **Toewijzingen** de groepen met de apparaten die u wilt toewijzen aan deze bereiktag. Kies **Volgende**.
4. Kies op de pagina **Beoordelen en maken** de optie **Maken**.

## <a name="to-assign-a-scope-tag-to-a-role"></a>Een bereiktag toewijzen aan een rol

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Tenantbeheer** > **Rollen** > **Alle rollen** > kies een rol > **Toewijzingen** > **Toewijzen**.
2. Geef op de pagina **Basisinformatie** een **Toewijzingsnaam** en **Beschrijving** op. Kies **Volgende**.
3. Kies op de pagina **Beheerdersgroepen** de optie **Groepen selecteren die moeten worden opgenomen** en selecteer de groepen die deel moeten uitmaken van deze toewijzing. Gebruikers in deze groep zijn gemachtigd om gebruikers/apparaten binnen het Bereik (Groepen) te beheren. Kies **Volgende**.

    ![Schermopname van Lidgroepen selecteren.](./media/scope-tags/select-member-groups.png)

4. Selecteer op de pagina **Bereikgroepen** een van de volgende opties voor **Toewijzen aan**
    - **Geselecteerde groepen**: selecteer de groepen met de gebruikers/apparaten die u wilt beheren. Alle gebruikers/apparaten in de geselecteerde groepen worden beheerd door de gebruikers in de Beheerdersgroep.
    - **Alle gebruikers**: alle gebruikers kunnen worden beheerd door de gebruikers in de Beheerdersgroepen.
    - **Alle apparaten**: alle apparaten kunnen worden beheerd door de gebruikers in de Beheerdersgroepen.
    - **Alle gebruikers en alle apparaten**: alle gebruikers en apparaten kunnen worden beheerd door de gebruikers in de Beheerdersgroepen.

5. Kies **Volgende**
6. Selecteer op de pagina **Bereik(tags)** de tags die u aan deze rol wilt toevoegen. Gebruikers in de Beheerdersgroepen hebben toegang tot Intune-objecten die ook dezelfde bereiktag hebben. U kunt maximaal 100 bereiktags toewijzen aan een rol.
7. Kies **Volgende** om naar de pagina **Beoordelen en maken** te gaan en kies **Maken**.

## <a name="assign-scope-tags-to-other-objects"></a>Bereiktags toewijzen aan andere objecten

In het geval van objecten die bereiktags ondersteunen, worden bereiktags meestal weergegeven onder **Eigenschappen**. Als u bijvoorbeeld een bereiktag wilt toewijzen aan een configuratieprofiel, volgt u deze stappen:

1. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **Configuratieprofielen** > kies een profiel.

2. Kies **Eigenschappen** > **Bereik(tags)**  > **Bewerken** > **Bereiktags selecteren** > kies de tags die u wilt toevoegen aan het profiel. U kunt maximaal 100 bereiktags toewijzen aan een object.
4. Kies **Selecteren** > **Beoordelen en opslaan**.

## <a name="scope-tag-details"></a>Details bereiktags
Wanneer u met bereiktags werkt, moet u deze details onthouden: 

- U kunt bereiktags toewijzen aan een Intune-objecttype als de tenant meerdere versies van dat object kan hebben (zoals roltoewijzingen of apps).
  De volgende Intune-objecten zijn uitzonderingen op deze regel en ondersteunen momenteel geen bereiktags:
    - Windows ESP-profielen
    - Registratiebeperkingen
    - Bedrijfsapparaat-id's
    - Autopilot-apparaten
    - Nalevingslocaties voor apparaat
    - Jamf-apparaten
- VPP-apps en ebooks die zijn gekoppeld aan het VPP-token nemen de bereiktags over die zijn toegewezen aan het gekoppelde VPP-token.
- DEP-apparaten (Device Enrollment Program) en DEP-profielen die zijn gekoppeld aan het DEP-token, nemen de bereiktags over die zijn toegewezen aan het bijbehorende DEP-token.
- Wanneer een beheerder een object in Intune maakt, worden alle aan die beheerder toegewezen bereiktags automatisch toegewezen aan het nieuwe object.
- Intune RBAC is niet van toepassing op Azure Active Directory-rollen. Dus hebben de rollen Intune-servicebeheerders en Globale beheerders volledige beheerderstoegang tot Intune, ongeacht welke bereiktags ze hebben.
- Als een roltoewijzing geen bereiktag heeft, kan de IT-beheerder alle objecten zien op basis van de machtigingen voor de IT-beheerder. Beheerders die geen bereiktags hebben, hebben in wezen alle bereiktags.
- U kunt alleen een bereiktag toewijzen die zich in uw roltoewijzingen bevindt.
- U kunt alleen groepen die worden vermeld in Bereik (Groepen) van uw roltoewijzing als doelwit kiezen.
- Als een bereiktag aan uw rol is toegewezen, kunt u niet alle bereiktags voor een Intune-object verwijderen. Er is ten minste één bereiktag vereist.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe bereiktags zich gedragen wanneer er [meerdere roltoewijzingen](role-based-access-control.md#multiple-role-assignments) zijn.
Beheer uw [rollen](role-based-access-control.md) en [profielen](../configuration/device-profile-assign.md).



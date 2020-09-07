---
title: Gebruikers toevoegen en machtigingen verlenen
titleSuffix: Microsoft Intune
description: On-premises gebruikers met Azure AD synchroniseren en beheerdersmachtigingen voor uw Intune-abonnement verlenen.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/28/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6e9ec662-465b-4ed4-94c1-cff0fe18f126
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 56d632da8480e0beedac7f086928638633dbe49c
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996313"
---
# <a name="add-users-and-grant-administrative-permission-to-intune"></a>Gebruikers toevoegen en beheerdersmachtigingen aan Intune toekennen

Als beheerder kunt u gebruikers rechtstreeks toevoegen of gebruikers synchroniseren via uw on-premises Active Directory. Zodra gebruikers zijn toegevoegd, kunnen ze apparaten registreren en hebben ze toegang tot bedrijfsresources. U kunt gebruikers ook aanvullende machtigingen geven, zoals de machtigingen *globale beheerder* en *servicebeheerder*.

## <a name="add-users-to-intune"></a>Gebruikers toevoegen aan Intune

U kunt handmatig gebruikers aan uw Intune-abonnement toevoegen via het [Microsoft 365-beheercentrum](https://admin.microsoft.com) of de [Azure-portal](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/overview). Een beheerder kan gebruikersaccounts bewerken om Intune-licenties toe te wijzen. U kunt licenties toewijzen in het Microsoft 365-beheercentrum of in de Intune Azure-portal. Zie [Gebruikers afzonderlijk of bulksgewijs toevoegen aan het Microsoft 365-beheercentrum](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec) voor meer informatie over het gebruik van het Microsoft 365-beheercentrum.

### <a name="add-intune-users-in-the-microsoft-365-admin-center"></a>Intune-gebruikers toevoegen in het Microsoft 365-beheercentrum

1. Meld u aan bij het [Microsoft 365-beheercentrum](https://admin.microsoft.com) met een account voor globale beheerders of beheerders voor gebruikerstoegang.
2. Selecteer **Beheerder** in het Microsoft 365-menu.
3. Selecteer **Nieuwe gebruiker** in het beheercentrum.

   ![Schermafbeelding van de sectie Een gebruiker toevoegen](./media/users-add/office-add-user.png)

4. Geef de volgende gebruikersgegevens op:
   - **Voornaam**
   - **Achternaam**
   - **Weergavenaam**
   - **Gebruikersnaam**: user principal name (UPN), opgeslagen in Azure Active Directory (voor toegang tot de service)
   - **Locatie**
   - **Contactgegevens** (optioneel)
   - **Wachtwoord**: automatisch genereren of opgeven

     ![Schermafbeelding van de sectie Nieuwe gebruiker](./media/users-add/office-add-user-details.png)

5. Wijs een Intune-licentie toe. Selecteer **Productlicenties** en kies de productlicentie. Er is een licentie voor Intune vereist.
6. Kies **Toevoegen** om de nieuwe gebruiker te maken.

### <a name="add-intune-users-in-the-azure-portal"></a>Intune-gebruikers toevoegen in de Azure-portal

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Gebruikers** > **Alle gebruikers**.
2. Selecteer **Nieuwe gebruiker** in het beheercentrum.
3. Geef de volgende gebruikersgegevens op:
   - **Naam**
   - **Gebruikersnaam**: de nieuwe naam in de Azure Active Directory-portal ![Schermafbeelding van het toevoegen van naam en gebruikersnaam](./media/users-add/intune-add-user-info.png) Kies **OK** om door te gaan.
4. U kunt desgewenst de volgende gebruikerseigenschappen opgeven:
   - **Profiel**: werkinformatie zoals **Functie** en **Afdeling**
   - **Groepen**: selecteer groepen die u wilt toevoegen voor de gebruiker
   - **Directory-rol**: verleen de gebruiker beheerdersmachtigingen, inclusief een Intune-servicebeheerdersrol.

   Selecteer **Maken** om de nieuwe gebruiker toe te voegen aan Intune.
5. Selecteer **Profiel** en kies vervolgens een **gebruikslocatie** voor de nieuwe gebruiker. Een gebruikslocatie is vereist om een licentie voor Intune te kunnen toewijzen aan de nieuwe gebruiker. Kies **Opslaan** om door te gaan.
    ![Schermafbeelding van de gebruikslocatie](./media/users-add/intune-add-user-loc.png)
6. Selecteer **Licenties** en kies vervolgens **Toewijzen** om een Intune-licentie voor deze gebruiker toe te wijzen. Een Intune-licentie is vereist voor het registreren van apparaten of om toegang te krijgen tot bedrijfsresources. Selecteer **Producten**, kies het licentietype, kies **Selecteren** en kies ten slotte **Toewijzen**.

## <a name="grant-admin-permissions"></a>Beheerdersmachtigingen verlenen

Nadat u gebruikers aan uw Intune-abonnement hebt toegevoegd, kunt u het beste enkele gebruikers beheerdersmachtigingen verlenen.  Voer hiertoe de volgende stappen uit:

### <a name="give-admin-permissions-in-microsoft-365"></a>Beheerdersmachtigingen verlenen in Microsoft 365

1. Meld u aan bij het [Microsoft 365-beheercentrum](https://admin.microsoft.com) met een account voor globale beheerders.
2. Selecteer **Beheerder** in het Microsoft 365-menu.
3. Kies in het beheercentrum de optie **Actieve gebruikers** en kies vervolgens de gebruiker waaraan u beheerdersmachtigingen wilt verlenen.

4. Kies in de kolom **Rollen** de optie **Bewerken**.

    ![Schermafbeelding van gebruiker met beheerdersrechten](./media/users-add/office-assign-roles-open.png)

5. Kies in de lijst met beschikbare rollen de beheerdersmachtiging die u wilt verlenen.
![Schermopname van het toewijzen van rollen](./media/users-add/office-assign-roles.png)
6. Kies **Opslaan**.

### <a name="give-admin-permissions-in-the-azure-portal"></a>Beheerdersmachtigingen verlenen in de Azure-portal

1. Meld u aan bij de [Azure-portal](https://portal.azure.com) met een account voor globale beheerders.
2. Kies in de Azure-portal de optie **Gebruiker** en kies vervolgens de gebruiker die u beheerdersmachtigingen wilt verlenen.
3. Selecteer **Directory-rol** en vervolgens de machtiging.
  ![Schermopname van Directory-rol](./media/users-add/add-intune-directory-role.png)
4. Kies **Opslaan**.

### <a name="types-of-administrators"></a>Typen beheerders

Wijs gebruikers een of meer beheerdersmachtigingen toe. Deze machtigingen bepalen het beheerbereik voor gebruikers en de taken die ze kunnen beheren. De beheerdersmachtigingen voor de verschillende Microsoft-cloudservices komen overeen, hoewel bepaalde machtigingen mogelijk niet worden ondersteund door sommige services. In zowel de Azure-portal als het Microsoft 365-beheercentrum worden beperkte beheerdersrollen vermeld die niet door Intune worden gebruikt. Intune-beheerdersmachtigingen bevatten de volgende opties:

- **Globale beheerder**: (Microsoft 365 en Intune) heeft toegang tot alle beheerfuncties in Intune. De persoon die zich voor Intune aanmeldt, wordt standaard een globale beheerder. Globale beheerders zijn de enige beheerders die andere beheerdersrollen kunnen toewijzen. U kunt meer dan één globale beheerder hebben in uw organisatie. Als best practice is het raadzaam dat slechts een paar mensen in uw bedrijf deze rol vervullen om het risico voor uw bedrijf te reduceren.
- **Wachtwoordbeheerder**: (Microsoft 365 en Intune) stelt wachtwoorden opnieuw in, beheert serviceaanvragen en bewaakt de servicestatus. Wachtwoordbeheerders zijn beperkt tot het opnieuw instellen van wachtwoorden voor gebruikers.
- **Servicebeheerder**: (Microsoft 365 en Intune) opent ondersteuningsaanvragen voor Microsoft en bekijkt het servicedashboard en berichtencentrum. Ze beschikken alleen over weergavemachtigingen, met uitzondering voor het openen en lezen van ondersteuningstickets.
- **Factureringsbeheerder**: (Microsoft 365 en Intune) doet aankopen, beheert abonnementen, beheert ondersteuningstickets en bewaakt de servicestatus.
- **Beheerder**: (Microsoft 365 en Intune) stelt wachtwoorden opnieuw in, bewaakt de servicestatus, voegt gebruikersaccounts toe en verwijdert deze, en beheert serviceaanvragen. De beheerder van de gebruikerstoegang kan geen globale beheerder verwijderen, andere beheerdersrollen maken of wachtwoorden opnieuw instellen voor andere beheerders.
- **Intune-servicebeheerder**: beschikt over alle machtigingen voor globale beheerders van Intune, behalve machtigingen voor het aanmaken van beheerders met opties voor **directory-rollen**.

Het account dat u gebruikt om uw Microsoft Intune-abonnement te maken, heeft de rol van globale beheerder. Het is een best practice om de rol van globale beheerder niet te gebruiken voor dagelijkse beheertaken. Een beheerder heeft geen Intune-licentie nodig voor toegang tot Intune op het Azure-portal, maar om bepaalde beheertaken zoals het instellen van de Exchange-serverconnector uit te kunnen voeren, is wel een Intune-licentie vereist.

Voor toegang tot het Microsoft 365-beheercentrum moet **Toegestane gebruikers aanmelden** zijn ingesteld voor uw account. Ga in de Azure-portal naar **Profiel** en stel **Aanmelden blokkeren** in op **Nee** om toegang te verlenen. Deze status is niet hetzelfde als wanneer u een licentie voor het abonnement hebt. Standaard hebben alle gebruikersaccounts de status **Toegestaan**. Gebruikers zonder beheerdersmachtigingen kunnen het Microsoft 365-beheercentrum gebruiken om Intune-wachtwoorden opnieuw in te stellen.

## <a name="sync-active-directory-and-add-users-to-intune"></a>Active Directory synchroniseren en gebruikers toevoegen aan Intune

U kunt adreslijstsynchronisatie configureren voor het importeren van gebruikersaccounts uit de on-premises Active Directory in Microsoft Azure Active Directory (Azure AD) die Intune-gebruikers bevat. Het koppelen van uw on-premises Active Directory-service aan alle Azure Active Directory-services zorgt ervoor dat het beheer van gebruikersidentiteiten veel eenvoudiger wordt. U kunt ook eenmalige aanmelding configureren om de verificatie vertrouwd en eenvoudig te maken voor uw gebruikers. Door dezelfde [Azure AD-tenant](/azure/active-directory/hybrid/whatis-hybrid-identity) te koppelen met meerdere services, zijn de gebruikersaccounts die u eerder hebt gesynchroniseerd, beschikbaar voor alle cloudservices.

### <a name="how-to-sync-on-premises-users-with-azure-ad"></a>On-premises gebruikers synchroniseren met Azure AD

Het enige hulpprogramma dat u nodig hebt om uw gebruikersaccounts te synchroniseren met Azure AD, is de [Azure AD Connect-wizard](https://www.microsoft.com/download/details.aspx?id=47594). De Azure AD Connect-wizard biedt een vereenvoudigde begeleiding voor het verbinden van de on-premises infrastructuur voor identiteiten aan de cloud. Kies uw topologie en behoeften (één of meerdere mappen, synchronisatie van wachtwoordhashes, pass-through-verificatie of federatie). De wizard implementeert en configureert alle onderdelen die zijn vereist om de verbinding mogelijk te maken. Inclusief: synchronisatieservices, Active Directory Federation Services (AD FS) en de Azure AD PowerShell-module.

> [!TIP]
> Azure AD Connect bevat functionaliteit die eerder is uitgebracht als Dirsync en Azure AD Sync. Lees meer over [adreslijstintegratie](/previous-versions/azure/azure-services/jj573653(v=azure.100)). Zie [Overeenkomsten tussen Active Directory en Azure AD](/previous-versions/azure/azure-services/dn518177(v=azure.100)) voor meer informatie over het synchroniseren van gebruikersaccounts vanuit de lokale directory naar Azure AD.
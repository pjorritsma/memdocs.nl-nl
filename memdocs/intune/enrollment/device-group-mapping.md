---
title: Apparaten categoriseren in groepen in Intune
titleSuffix: Microsoft Intune
description: Ontdek hoe u apparaten categoriseert in groepen voor eenvoudiger beheer.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7b668c37-40b9-4c69-8334-5d8344e78c24
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6dae19e466d3d0e88ae07d1c82a63b098439632
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908612"
---
# <a name="categorize-devices-into-groups"></a>Apparaten categoriseren in groepen

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Met apparaatcategorieën van Microsoft Intune kunnen apparaten automatisch worden toegevoegd aan groepen op basis van categorieën die u definieert, zodat het voor u eenvoudiger wordt om die apparaten te beheren.

Voor apparaatcategorieën wordt de volgende werkstroom gebruikt:
1. Maak categorieën die gebruikers kunnen kiezen bij het registreren van hun apparaat.
2. Wanneer gebruikers van iOS-/iPadOS- en Android-apparaten een apparaat registreren, moeten ze een categorie kiezen uit de lijst met categorieën die u hebt geconfigureerd. Als u een categorie wilt toewijzen aan een Windows-apparaat, moeten gebruikers de bedrijfsportal-website gebruiken.
3. Vervolgens kunt u beleidsregels en apps implementeren naar deze groepen.

U kunt alle apparaatcategorieën maken die u maar wilt. Bijvoorbeeld:
- Verkooppuntapparaat
- Demonstratieapparaat
- Sales
- Boekhouding
- Manager

## <a name="how-to-configure-device-categories"></a>Apparaatcategorieën configureren

### <a name="step-1-create-device-categories-on-the-intune-blade-of-the-azure-portal"></a>Stap 1: apparaatcategorieën maken op de blade Intune in Azure Portal
1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en kies **Apparaten** > **Apparaatcategorieën**.
2. Kies **Maken** op de pagina **Apparaatcategorieën** om een nieuwe categorie toe te voegen.
3. Voer op de blade **Apparaatcategorie maken** een **Naam** in voor de nieuwe categorie en een optionele **Beschrijving**.
4. Selecteer **Maken** wanneer u klaar bent. De nieuwe categorie wordt weergegeven in de lijst met categorieën.

Als u Azure Active Directory-beveiligingsgroepen (Azure AD) maakt in stap 2, gebruikt u de naam van de apparaatcategorie.

### <a name="step-2-create-azure-active-directory-security-groups"></a>Stap 2: Azure Active Directory-beveiligingsgroepen maken
In deze stap maakt u dynamische groepen in Azure Portal op basis van de apparaatcategorie en de naam van de apparaatcategorie.

Zie [Geavanceerde regels maken met kenmerken](/azure/active-directory/users-groups-roles/groups-dynamic-membership#using-attributes-to-create-rules-for-device-objects) in de documentatie van Azure AD om door te gaan.

Gebruik de informatie in deze sectie om een apparaatgroep met een geavanceerde regel te maken op basis van het kenmerk **deviceCategory**. Bijvoorbeeld: (**device.deviceCategory -eq***de naam van de apparaatcategorie in Azure Portal*.

Wanneer u apparaatgroepen hebt geconfigureerd en gebruikers hun apparaat registreren, krijgen ze een lijst te zien met de categorieën die u hebt geconfigureerd. Wanneer ze een categorie hebben gekozen en de inschrijving voltooien, wordt hun apparaat toegevoegd aan de Active Directory-beveiligingsgroep die overeenkomt met de gekozen categorie.

### <a name="view-the-categories-of-devices-that-you-manage"></a>De apparaatcategorieën weergeven die u beheert

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en kies **Apparaten** > **Alle apparaten**.

2. Bekijk de kolom **Apparaatcategorie** in de lijst met apparaten.

Als de kolom **Apparaatcategorie** niet wordt weergegeven, selecteert u **Kolommen** > **Categorie** > **Toepassen**.

### <a name="change-the-category-of-a-device"></a>De categorie van een apparaat wijzigen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en kies **Apparaten** > **Alle apparaten** > kies het gewenste apparaat > **Eigenschappen**.
2. Op de volgende blade kunt u de **apparaatcategorie** van het geselecteerde apparaat wijzigen in een van de categorienamen die u eerder hebt geconfigureerd.

## <a name="after-you-configure-device-groups"></a>Na het configureren van apparaatgroepen

Wanneer gebruikers van iOS-/iPadOS- en Android-apparaten hun apparaat registreren, moeten ze een categorie kiezen uit de lijst met categorieën die u hebt geconfigureerd. Wanneer ze een categorie hebben gekozen en de registratie voltooien, wordt hun apparaat toegevoegd aan de Intune-apparaatgroep of Active Directory-beveiligingsgroep die overeenkomt met de gekozen categorie.

Windows-gebruikers moeten de website van de bedrijfsportal gebruiken om een categorie te selecteren.

Uw gebruikers kunnen bij elk platform altijd naar portal.manage.microsoft.com gaan nadat het apparaat is geregistreerd. Laat de gebruiker naar de bedrijfsportalwebsite en vervolgens **Mijn apparaten** gaan. De gebruiker kan een geregistreerd apparaat op de pagina kiezen en vervolgens een categorie kiezen.

Nadat de categorie is gekozen, wordt het apparaat automatisch toegevoegd aan de bijbehorende groep die u hebt gemaakt. Als een apparaat al is geregistreerd voordat u categorieën configureert, ziet de gebruiker een melding over het apparaat op de bedrijfsportal-website. Hierdoor weten gebruikers dat ze de volgende keer dat ze de bedrijfsportal-app in iOS/iPadOS of Android openen, een categorie moeten selecteren.

## <a name="further-information"></a>Meer informatie
- U kunt een apparaatcategorie bewerken in Azure Portal. U moet de Azure AD-beveiligingsgroepen die naar deze categorie verwijzen dan echter handmatig bijwerken.

- Als u een categorie verwijdert, wordt voor apparaten die aan de categorie zijn toegewezen de categorienaam **Niet-toegewezen** weergegeven.
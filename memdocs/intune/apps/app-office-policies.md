---
title: Beleidsregels voor Office-apps
titleSuffix: Microsoft Intune
description: Het beleid dat beschikbaar is voor Office-apps.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca558b40ad3d006aa764819a0fbccc16a03fd0e2
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/10/2020
ms.locfileid: "89644024"
---
# <a name="policies-for-office-apps"></a>Beleidsregels voor Office-apps

Intune biedt specifiek beleid voor Microsoft Office-apps. U kunt specifieke opties selecteren voor het maken van beheerbeleid voor mobiele apps die verbinding maken met Microsoft 365-services. Er zijn veel beleidsregels voor Office-apps die u kunt toevoegen aan Microsoft Intune en die van toepassing zijn op groepen eindgebruikers.

Voorbeelden van slechts enkele van de Office-app-beleidsregels zijn:
- Microsoft Word: *Beveiligde weergave uitschakelen voor bijlagen die worden geopend vanuit Outlook*
- Microsoft Visio: *Macro's voor uitvoering blokkeren in Office-bestanden vanaf internet*
- Microsoft Project: *Vertrouwde locaties op het netwerk toestaan*
- Microsoft Publisher: *Automatiseringsbeveiliging van Publisher*
- Microsoft PowerPoint: *Beveiligde weergave uitschakelen voor bijlagen die worden geopend vanuit Outlook*

> [!NOTE]
> Wanneer u selecteert om elk specifiek app-beleid te configureren, worden er aanvullende beleidsgegevens gegeven. U kunt de lijst met Office-beleidsregels filteren om snel het aanbevolen **beveiligingsbasis**beleid te selecteren.

U kunt de toegang tot Exchange on-premises mailboxen tevens beveiligen door beveiligingsbeleid voor Intune-apps te maken voor Outlook voor iOS/iPadOS en Android met hybride moderne verificatie. Voordat u deze functie kunt gebruiken, moet u voldoen aan de vereisten voor het gebruik van de Office-cloudbeleidsservice. Beveiligingsbeleid voor apps wordt niet ondersteund voor andere apps die verbinding maken met on-premises Exchange- of SharePoint-services. Zie [Overzicht van de Office-cloudbeleidsservice voor Microsoft 365-apps for enterprise](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service) voor meer informatie.

## <a name="prerequisites"></a>Vereisten

U moet voldoen aan de vereisten voor het gebruik van beleidsregels voor Office-apps. Zie [Vereisten voor het gebruik van de Office-cloudbeleidsservice](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service) voor meer informatie.

## <a name="to-add-an-office-app-policy"></a>Een Office-app-beleid toevoegen

Nadat u Intune hebt ingesteld in uw organisatie, kunt u een Office-app-beleid maken.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Beleid voor Office-apps** > **Maken**.
3. Voeg de volgende waarden toe:
    - **Naam:** typ een naam (vereist) voor het nieuwe beleid.
    - **Beschrijving:** (optioneel) typ een beschrijving.
    - **Type selecteren**: Selecteer hoe deze beleidsconfiguratie wordt toegepast.
    - **Groep selecteren:** Selecteer de groep voor deze beleidsconfiguratie.
    - **Beleidsregels configureren:** Selecteer het Office-beleid dat u wilt toepassen. U kunt de verstrekte lijst sorteren op basis van beleid, platform, toepassing, aanbeveling en status.
4. Selecteer **Maken**. Het beleid wordt gemaakt en wordt weergegeven in de tabel in het deelvenster **Beleidsconfiguraties**.

   > [!TIP]
   > Het deelvenster **Beleidsconfiguraties** bevat de **Integriteitsstatus** voor elk beleid.

## <a name="additional-information"></a>Aanvullende informatie

- [Overzicht van de Office-cloudbeleidsservice voor Microsoft 365-apps for enterprise](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)
- [Beleidsinstellingen gebruiken voor het beheer van privacybesturingselementen voor Microsoft 365 Apps for enterprise](https://docs.microsoft.com/deployoffice/privacy/manage-privacy-controls)
- [Voorkeuren gebruiken voor het beheer van privacybesturingselementen voor Office voor Mac](https://docs.microsoft.com/deployoffice/privacy/mac-privacy-preferences)
- [Voorkeuren gebruiken voor het beheer van privacybesturings elementen voor Office op iOS-apparaten](https://docs.microsoft.com/deployoffice/privacy/ios-privacy-preferences)
- [Beleidsinstellingen gebruiken voor het beheer van privacybesturingselementen voor Office op Android-apparaten](https://docs.microsoft.com/deployoffice/privacy/android-privacy-controls)

## <a name="next-steps"></a>Volgende stappen

- [App-gegevens en -toewijzingen controleren met Microsoft Intune](apps-monitor.md)
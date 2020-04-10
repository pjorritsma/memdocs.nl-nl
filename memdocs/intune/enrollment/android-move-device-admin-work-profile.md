---
title: Android-apparaten verplaatsen van beheer door apparaatbeheerder naar werkprofielbeheer
titleSuffix: Microsoft Intune
description: Verplaats Android-apparaten van apparaatbeheerder naar werkprofielbeheer in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f16c39ff0af44918099863be5d23ec9fe564493
ms.sourcegitcommit: 954b3aae7916ad14065e6e86a577c5205103a50e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/03/2020
ms.locfileid: "80624917"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Android-apparaten verplaatsen van beheer door apparaatbeheerder naar werkprofielbeheer

U kunt gebruikers helpen hun Android-apparaten te verplaatsen van beheer door apparaatbeheerder naar werkprofielbeheer met behulp van de nalevingsinstelling **Apparaten blokkeren die met de apparaatbeheerder worden beheerd**. Met deze instelling zorg u ervoor dat apparaten niet-compatibel zijn als ze worden beheerd met apparaatbeheerder. 

Wanneer gebruikers zien dat ze om die reden niet meer compatibel zijn, kunnen ze op **Oplossen** tikken. Ze krijgen dan een controlelijst te zien die hen begeleidt bij de volgende stappen:
1. Uitschrijven bij Beheer door apparaatbeheerder
2. Inschrijven bij werkprofielbeheer
3. Het oplossen van nalevingsproblemen. 

## <a name="prerequisites"></a>Vereisten

- Gebruikers moeten werken met [apparaten die zijn ingeschreven bij Android-apparaatbeheerder](android-enroll-device-administrator.md) met Android-bedrijfsportal versie 5.0.4720.0 of hoger.
- Stel Android-werkprofielbeheer in door [uw Intune-tenantaccount te koppelen aan uw Android Enterprise-account](connect-intune-android-enterprise.md).
- [Stel de inschrijving van uw Android Enterprise-werkprofiel in](android-work-profile-enroll.md) voor de groep gebruikers die wordt verplaatst naar Android-werkprofiel.
- Overweeg de limieten voor uw gebruikersapparaten te verhogen. Bij het uitschrijven van apparaten voor beheer door apparaatbeheerder worden apparaatregistraties mogelijk niet onmiddellijk verwijderd. Om tijdens deze periode een buffer te hebben, moet u mogelijk de capaciteit van de apparaatlimiet verhogen, zodat de gebruikers zich kunnen inschrijven voor werkprofielbeheer.
  - [Configureer apparaatinstellingen voor Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) voor het maximum aantal apparaten per gebruiker.
  - Pas de [beperkingen voor Intune-apparaatlimieten](enrollment-restrictions-set.md#create-a-device-limit-restriction) aan door de apparaatlimiet in te stellen. 

## <a name="create-device-compliance-policy"></a>Nalevingsbeleid voor apparaat maken

1. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apparaten** > **Nalevingsbeleid** > **Beleid** > **Beleid maken**.

    ![Beleid maken](./media/android-move-device-admin-work-profile/create-policy.png)

2. Stel op de pagina **Een beleid maken** de optie **Platform** in op **Android-apparaatbeheerder** > **Maken**.
3. Geef op de pagina **Basisinformatie** een waarde op voor **Naam** en **Beschrijving** > **Volgende**.

    ![Pagina Basisinformatie](./media/android-move-device-admin-work-profile/basics.png)
    
4. Stel op de pagina **Instellingen voor naleving** in de sectie **Apparaatstatus** de optie **Apparaten blokkeren die met de apparaatbeheerder worden beheerd** in op **Ja** > **Volgende**.

    ![Apparaten blokkeren](./media/android-move-device-admin-work-profile/block-devices.png)

5. Op de pagina **Locaties** kunt u locaties toevoegen als u dat wilt > **Volgende**.
6. In **Acties voor niet-naleving** kunt u de actie **E-mail verzenden naar de eindgebruiker** instellen.

    ![E-mail verzenden](./media/android-move-device-admin-work-profile/send-email.png)


    In het e-mailbericht kunt u de onderstaande URL in uw berichten aan gebruikers toevoegen. Met de URL wordt de pagina **Apparaatinstellingen bijwerken** van de Android-bedrijfsportal geopend. Op deze pagina wordt het proces gestart om over te stappen op werkprofielbeheer.
    - `https://portal.manage.microsoft.com/UpdateSettings.aspx`.
    - Voor de Amerikaanse overheid kunt u in plaats hiervan deze koppeling gebruiken: `https://portal.manage.microsoft.us/UpdateSettings.aspx`.
  
    > [!NOTE]
    > - Natuurlijk kunt u gebruikersvriendelijke hypertekst gebruiken voor de koppelingen in uw communicatie met gebruikers. Gebruik echter geen URL-verkorters omdat de koppelingen dan misschien niet werken.
    > - Als de Android-bedrijfsportal op de achtergrond is geopend wanneer een gebruiker op de koppeling tikt, kan het zijn dat in plaats daarvan de laatst geopende pagina wordt weergegeven.
    > - Gebruikers moeten op een Android-apparaat op de koppeling tikken. Als ze de koppeling in plaats daarvan in een browser plakken, wordt de Android-bedrijfsportal niet gestart. 

    Kies **Volgende**.

7. Selecteer op de pagina **Bereiktags** eventuele bereiktags die u wilt opnemen.
8. Wijs op de pagina **Toewijzingen** het beleid toe aan een groep met apparaten die zijn ingeschreven bij beheer door apparaatbeheerder > **Volgende**.
9. Bevestig alle instellingen op de pagina **Beoordelen en maken** en selecteer **Maken**.

## <a name="troubleshooting"></a>Probleemoplossing

Het [eindgebruikersproces om over te stappen op de nieuwe instellingen voor apparaatbeheer](../user-help/move-to-new-device-management-setup.md) begeleidt gebruikers bij het uitschrijven bij beheer door apparaatbeheerder en het instellen van werkprofielbeheer. Gebruikers moeten werken met [apparaten die zijn ingeschreven bij Android-apparaatbeheerder](android-enroll-device-administrator.md) met Android-bedrijfsportal versie 5.0.4720.0 of hoger.

### <a name="user-sees-an-error-after-tapping-resolve"></a>De gebruiker ziet een fout nadat op Oplossen is getikt
Als gebruikers een fout zien nadat ze op de knop **Oplossen** hebben getikt, is dit waarschijnlijk om een van de volgende redenen:
- De inschrijving van het werkprofiel is niet juist ingesteld (er is geen Android Enterprise-account gekoppeld of er zijn inschrijvingsbeperkingen ingesteld die inschrijving voor een werkprofiel blokkeren).
- Op het apparaat wordt Android 4.4 of eerder uitgevoerd. Deze versie biedt geen ondersteuning voor werkprofielinschrijving. 
- De fabrikant van het apparaat biedt geen ondersteuning voor werkprofielinschrijving op dit apparaatmodel.

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>De knop Oplossen wordt niet weergegeven op het apparaat van de gebruiker
De knop **Oplossen** wordt niet weergegeven op het apparaat van de gebruiker als de gebruiker zich inschrijft voor beheer door apparaatbeheerder, als het hierboven uitgelegde nalevingsbeleid voor apparaat van kracht is.

De knop **Oplossen** wordt weergegeven nadat de gebruiker de installatie heeft uitgesteld en het proces opnieuw heeft gestart vanuit de melding.

U kunt deze situatie vermijden door inschrijvingsbeperkingen te gebruiken om inschrijving voor beheer door apparaatbeheerder te blokkeren.

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>De gebruiker ziet een fout nadat hij/zij op URL heeft getikt om de pagina Apparaatinstellingen bijwerken te openen
Gebruikers zien mogelijk een foutpagina in de browser wanneer ze op de URL tikken naar de pagina **Apparaatinstellingen bijwerken** van de Android-bedrijfsportal. Deze fout kan een van de volgende oorzaken hebben:
- Het apparaat is geen Android.
- Het Android-apparaat heeft geen bedrijfsportal-app.
- De Android-bedrijfsportal versie is ouder dan 5.0.4720.0.
- Op het Android-apparaat wordt Android 6 of eerder gebruikt. 

## <a name="next-steps"></a>Volgende stappen
[Zie de stroom voor eindgebruikers](../user-help/move-to-new-device-management-setup.md)
[Android-werkprofielapparaten beheren met Intune](android-enterprise-overview.md)

---
title: 'Snelstartgids: automatische inschrijving in Intune instellen'
description: 'Snelstartgids: automatische inschrijving voor Windows 10-apparaten in Intune instellen.'
services: microsoft-intune
author: ErikjeMS
manager: dougeby
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 01/17/2020
ms.author: erikje
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 599a5f6e6e355a37e909182fc14a07d489f45558
ms.sourcegitcommit: 2e0bc4859f7e27dea20c6cc59d537a31f086c019
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/21/2020
ms.locfileid: "86872032"
---
# <a name="quickstart-set-up-automatic-enrollment-for-windows-10-devices"></a>Snelstartgids: automatische inschrijving voor Windows 10-apparaten instellen

In deze snelstartgids stelt u Microsoft Intune zo in dat apparaten automatisch worden ingeschreven wanneer bepaalde gebruikers zich aanmelden bij Windows 10-apparaten.

Als u niet over een Intune-abonnement beschikt, kunt u [zich registreren voor een gratis proefaccount](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Vereisten

- Microsoft Intune-abonnement - [Registreren voor een gratis proefaccount](../fundamentals/free-trial-sign-up.md).
- Als u de stappen in deze snelstart wilt uitvoeren, moet u eerst [een gebruiker maken](../fundamentals/quickstart-create-user.md) en [een groep maken](../fundamentals/quickstart-create-group.md).

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Aanmelden bij Intune in de Microsoft Endpoint Manager

Meld u bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) aan als globale beheerder of Intune-beheerder. Als u een Intune-proefabonnement hebt gemaakt, is het account waarmee u het abonnement hebt gemaakt de globale beheerder.

## <a name="set-up-windows-10-automatic-enrollment"></a>Automatische inschrijving voor Windows 10 instellen

Voor dit voorbeeld gebruikt u MDM-inschrijving, zodat zowel bedrijfsapparaten als Bring Your Own-apparaten automatisch kunnen worden ingeschreven. U gaat zich registreren voor een gratis Azure Active Directory Premium-abonnement.

1. Kies in het [beheercentrum van Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Alle services** > **M365 Azure Active Directory** > **Azure Active Directory** > **Mobility (MDM en MAM)** .
2. Selecteer **Een gratis Premium-proefversie krijgen om deze functie te gebruiken**. Wanneer u deze optie selecteert, is automatische inschrijving mogelijk met de gratis proefversie van Azure Active Directory Premium. 

    ![De gratis proefversie van Azure Active Directory Premium selecteren](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-01.png)

3. Kies de gratis proefversie van **Enterprise Mobility + Security E5**. 
4. Klik op **Gratis proefversie** > **Activeren** om de gratis proefversie te activeren.

    ![De gratis proefversie van Enterprise Mobility + Security E5 kiezen](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-02.png)

    > [!NOTE]
    > Het kan even duren voordat deze is geactiveerd. 

3. Selecteer **Microsoft Intune** om Intune te configureren. 

    ![Microsoft Intune in de lijst kiezen](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-03.png)

4. Selecteer **Sommige** in het **gebruikersbereik van MDM** om automatische inschrijving voor MDM te gebruiken om bedrijfsgegevens op Windows-apparaten van uw werknemers te beheren. De automatische inschrijving voor MDM wordt geconfigureerd voor aan AAD toegevoegde apparaten en Bring-Your-Own-Device-scenario's.

    ![Selecteer Sommige in de lijst Configureren](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-04.png)

5. Klik op **Groepen selecteren** > **Contoso-testers** > **Selecteren** als toegewezen groep.

    ![De in te schrijven groep selecteren](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-05.png)

6. Selecteer **Sommige** in het **gebruikersbereik van MAM** om gegevens op apparaten van uw werknemers te beheren.

    ![De in te schrijven groep selecteren](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-06.png)

7. Kies **Groepen selecteren** > **Contoso-testers** > **Selecteren** als toegewezen groep. 
8. Gebruik voor de rest van de configuratiewaarden de standaardwaarden.
9. Kies **Opslaan**.

## <a name="clean-up-resources"></a>Resources opschonen

Bekijk [Inschrijving voor Windows-apparaten instellen](windows-enroll.md) als u de automatische inschrijving bij Intune opnieuw wilt configureren.

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u geleerd om de automatische inschrijving voor Windows 10-apparaten in te stellen. Zie [Wat is apparaatinschrijving?](device-enrollment.md) voor meer informatie over apparaatinschrijving.

Ga door naar de volgende snelstartgids om deze serie met snelstartgidsen voor Intune te volgen.

> [!div class="nextstepaction"]
> [Snelstartgids: Uw Windows 10-apparaat registreren](quickstart-enroll-windows-device.md)

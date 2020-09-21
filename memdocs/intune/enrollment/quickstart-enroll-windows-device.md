---
title: Snelstartgids - Uw Windows 10 Desktop-apparaat inschrijven bij Microsoft Intune
description: Snelstartgids - Uw Windows 10 Desktop-apparaat inschrijven bij Microsoft Intune via de bedrijfsportal.
services: microsoft-intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/30/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 658a7655-a6df-4dbe-b56c-22c7fc60e706
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67de7db6587c1f80d849808c139bf1ae94f4bbd5
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643632"
---
# <a name="quickstart-enroll-your-windows-10-device"></a>Snelstartgids: Uw Windows 10-apparaat inschrijven

In deze snelstartgids neemt u eerst de rol van de Intune-gebruiker op zich en schrijft u uw Windows 10-apparaat in bij Microsoft Intune. Vervolgens gaat u terug naar Intune om het ingeschreven apparaat te bevestigen.

Door uw apparaten in te schrijven bij Microsoft Intune, krijgen uw Windows 10-apparaten toegang tot beveiligde gegevens van uw organisatie, inclusief e-mail, bestanden en andere resources. Dit geldt voor zowel Windows 10 Desktop- als Windows 10 Mobile-apparaten. Door uw apparaten in te schrijven, is deze toegang zowel voor u als voor uw organisatie beveiligd en staan uw werkgegevens los van uw persoonlijke gegevens.

> [!TIP]
> Ontdek wat er gebeurt wanneer u [uw apparaat inschrijft in Intune](../user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-windows.md) en wat betekent dat voor de [informatie op het apparaat](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md).

Als u niet over een Intune-abonnement beschikt, kunt u [zich registreren voor een gratis proefaccount](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Vereisten

- Microsoft Intune-abonnement - [Registreren voor een gratis proefaccount](../fundamentals/free-trial-sign-up.md)
- Als u wilt deze snelstartgids hebt voltooid, moet u de stappen uitvoeren om [automatische inschrijving in Intune in te stellen](quickstart-setup-auto-enrollment.md).

## <a name="confirm-your-windows-10-desktop-version"></a>Uw Windows 10 Desktop-versie bevestigen

Voordat u uw Windows 10 Desktop inschrijft, moet u controleren welke versie van Windows u hebt geïnstalleerd.

1. Klik met de rechtermuisknop op het Windows-pictogram **Start** en selecteer **Instellingen** om de opties voor Windows-instellingen weer te geven.

   ![Schermopname van de Windows-instellingen - Systeem](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-01.png)

2. Selecteer **Systeem** > **Info**. 

   ![Schermafbeelding van de systeeminstellingen](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-02.png)

    > [!TIP]
    > Typ de zin 'Info over uw pc' in de **zoekbalk** en selecteer vervolgens **Info over uw pc**.

3. In het venster **Instellingen** ziet u een lijst met **Windows-specificaties** voor uw pc. Zoek in deze lijst naar de **versie**.

4. Controleer of de Windows 10-**versie** **1607 of hoger is**.

    > [!IMPORTANT]
    > De stappen die in deze snelstartgids worden weergegeven zijn voor Windows 10-versie **1607 of hoger**. Als uw versie **1511 of lager** is, gaat u verder met [deze stappen](../user-help/enroll-windows-10-device.md).  

## <a name="enroll-windows-10-desktop"></a>Windows 10 Desktop inschrijven

1. Ga terug naar Windows-instellingen en selecteer **Accounts**.

   ![Schermopname van de systeeminstellingen - Accounts](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-03.png)

2. Selecteer **Werk- of schoolaccount openen** > **Verbinden**.

    ![Selecteer Werk- of school-account openen](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-04.png)

3. Meld u aan bij Intune met uw werk- of schoolaccount en selecteer **Volgende**. Als u de quickstart [Een gebruiker maken en een licentie toewijzen](../fundamentals/quickstart-create-user.md) hebt gevolgd, kunt u zich aanmelden met het gebruikersaccount dat u hebt gemaakt.

    > [!NOTE]
    > Als u een '.onmicrosoft.com' hebt ingesteld, bevat het gebruikersaccount **.onmicrosoft.com** als onderdeel van het accountadres. 

   ![Voer uw werk- of schoolaccount in](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-05.png)

    U ziet een bericht waarin staat dat bij uw bedrijf of school uw apparaat wordt geregistreerd.

4. Wanneer u het scherm **U bent klaar** ziet ziet, selecteert u **Gereed**. U bent klaar.

5. U ziet nu het toegevoegde account als onderdeel van de instellingen voor **Werk- of schoolaccount openen** op uw Windows-bureaublad.

   ![Schermopname van nieuw toegevoegde account](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-06.png)

    Als u de voorgaande stappen hebt uitgevoerd, maar nog steeds geen toegang hebt tot uw werk- of schoolaccount en -bestanden, volgt u de stappen in [Problemen met Windows 10-apparaten oplossen](../user-help/troubleshoot-your-windows-10-device-windows.md).  

## <a name="confirm-your-device-enrollment-in-intune"></a>De inschrijving van uw apparaat controleren in Intune

1. Meld u bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) aan als een globale beheerder of een Intune-servicebeheerder.
2. Selecteer **Apparaten** > **Alle apparaten** om de ingeschreven apparaten weer te geven in Intune.
3. Controleer of er een extra apparaat is ingeschreven in Intune.

   ![Schermopname bij Intune ingeschreven apparaten](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-07.png)

## <a name="clean-up-resources"></a>Resources opschonen

Als u uw Windows-apparaat wilt uitschrijven, raadpleegt u [Uw Windows-apparaat uit beheer verwijderen](../user-help/unenroll-your-device-from-intune-windows.md).

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u ontdekt hoe u Windows 10-apparaten in Intune kunt inschrijven. U kunt meer lezen over andere manieren om apparaten voor alle platformen in te schrijven. Zie [Werk gedaan krijgen met beheerde apparaten](../user-help/use-managed-devices-to-get-work-done.md) voor meer informatie over het gebruik van apparaten met Intune.

Ga door naar de volgende snelstartgids om deze serie met snelstartgidsen voor Intune te volgen.

> [!div class="nextstepaction"]
> [Snelstartgids: Een vereiste wachtwoordlengte instellen voor Android-apparaten](../protect/quickstart-set-password-length-android.md)

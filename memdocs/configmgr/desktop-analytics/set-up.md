---
title: Desktop Analytics instellen
titleSuffix: Configuration Manager
description: Een hand leiding voor het instellen en voorbereiden van Desktop Analytics.
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: a90f3260782f08fdf8f7424a95e09b34e38e97d3
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268144"
---
# <a name="how-to-set-up-desktop-analytics"></a>Desktop Analytics instellen

Gebruik deze procedure om u aan te melden bij Desktop Analytics en deze te configureren in uw abonnement. Deze procedure is een eenmalig proces voor het instellen van Desktop Analytics voor uw organisatie.  

> [!Important]  
> Zie [vereisten](overview.md#prerequisites)voor meer informatie over de algemene vereisten voor desktop Analytics met Configuration Manager.  

## <a name="initial-onboarding"></a>Eerste onboarding

1. Open de [Portal voor desktop Analytics](https://aka.ms/desktopanalytics) in Microsoft 365 Apparaatbeheer als gebruiker met de rol **globale beheerder** . Selecteer **Starten**. U kunt ook in de Configuration Manager-console naar de werk ruimte **software bibliotheek** gaan, het knoop punt voor **onderhoud van Desktop Analytics** selecteren en **implementaties van abonnementen**selecteren.

2. Controleer de service overeenkomst op de pagina **Service overeenkomst accepteren** en selecteer **accepteren**.  

3. Bekijk op de pagina **uw abonnement bevestigen** de lijst met vereiste licenties die in aanmerking komen. Schakel de instelling in op **Ja** als **u een van de ondersteunde of hogere abonnementen hebt**, en selecteer vervolgens **volgende**.  

4. Op de pagina **gebruikers toegang geven** :

    - **Desktop Analytics toestaan Directory rollen namens u te beheren**: Desktop Analytics wijst automatisch de eigenaar van de **werk ruimte** toe aan de Administrator-rol van **Desktop Analytics** . Als deze groepen al een **globale beheerder**zijn, is er geen wijziging.

        Als u deze optie niet selecteert, voegt Desktop Analytics nog steeds gebruikers toe als leden van de beveiligings groep. Een **globale beheerder** moet hand matig de rol **Desktop Analytics-beheerder** voor de gebruikers toewijzen.

        Zie [Administrator role permissions](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)(Engelstalig) in azure Active Directory voor meer informatie over het toewijzen van machtigingen voor beheerdersrol in azure Active Directory en de machtigingen die zijn toegewezen aan **bureau blad Analytics-beheerders**.  

    - Met Desktop Analytics wordt de beveiligings groep **eigen aren van werk ruimten** vooraf geconfigureerd in azure Active Directory voor het maken en beheren van werk ruimten en implementatie plannen.

        Als u een gebruiker aan de groep wilt toevoegen, typt u de naam of het e-mail adres in de sectie **naam of e-mail adres invoeren** . Selecteer **Volgende** als u klaar bent.

5. Op de pagina om **uw werk ruimte**in te stellen:  

    > [!NOTE]  
    > Voor het volt ooien van deze stap moet de gebruiker machtigingen voor de **werkruimte eigenaar** hebben en aanvullende toegang tot het Azure-abonnement en de resource groep. Zie [vereisten](overview.md#prerequisites)voor meer informatie.  

    - Als u een bestaande werk ruimte voor desktop Analytics wilt gebruiken, selecteert u deze en gaat u verder met de volgende stap.  

        > [!TIP]  
        > U kunt slechts één desktop Analytics-werk ruimte hebben per Azure AD-Tenant. Apparaten kunnen alleen diagnostische gegevens verzenden naar één werk ruimte.  

    - Als u een werk ruimte voor desktop Analytics wilt maken, selecteert u **werk ruimte toevoegen**.  

        1. Voer een globaal unieke **naam voor de werk ruimte**in.

        2. Selecteer de vervolg keuzelijst om **de naam van het Azure-abonnement voor deze werk ruimte te selecteren**en kies het Azure-abonnement voor deze werk ruimte.  

        3. **Nieuwe maken** Resource groep of **gebruik bestaande**.

        4. Selecteer de **regio** in de lijst en selecteer vervolgens **toevoegen**.  

6. Selecteer een nieuwe of bestaande werk ruimte en selecteer vervolgens **instellen als werk ruimte voor desktop Analytics**.  Selecteer vervolgens **door gaan** in het dialoog venster **bevestigen en toegang verlenen** .  

7. Kies op het tabblad nieuwe browser een account om u aan te melden. Selecteer de optie om **namens uw organisatie toestemming** te geven en selecteer **accepteren**.  

    > [!Note]  
    > Deze toestemming is het toewijzen van de MALogAnalyticsReader-toepassing de rol van Log Analytics lezer voor de werk ruimte. Deze toepassingsrol is vereist voor desktop Analytics. Zie [MALogAnalyticsReader Application Role](troubleshooting.md#bkmk_MALogAnalyticsReader)(Engelstalig) voor meer informatie.  

8. Selecteer **volgende**op de pagina om **uw werk ruimte**in te stellen.  

9. Selecteer op de pagina **laatste stappen** **naar bureau blad Analytics**.

De **Start** pagina van bureau blad Analytics wordt weer gegeven op de Azure Portal.

## <a name="next-steps"></a>Volgende stappen

Ga naar het volgende artikel om Configuration Manager met Desktop Analytics te verbinden.
> [!div class="nextstepaction"]  
> [Verbinding maken met Configuration Manager](connect-configmgr.md)  

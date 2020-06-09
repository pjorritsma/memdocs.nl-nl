---
title: Delivery Optimization-instellingen voor Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Configureer hoe Windows 10-apparaten die u met Intune beheert, gebruikmaken van Delivery Optimization. Maak in Intune een apparaatconfiguratieprofiel om updates van internet te installeren. Kijk ook hoe u bestaande updateringen kunt vervangen door een Delivery Optimization-profiel.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: 4d491a3210229d5dd6c74ccaed7f44c4ae4eb83c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990054"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Delivery Optimization-instellingen in Microsoft Intune

Met Intune gebruikt u instellingen voor Delivery Optimization voor uw Windows 10-apparaten om gebruik van bandbreedte te beperken als op die apparaten toepassingen en updates worden gedownload. Configureer Delivery Optimization als onderdeel van uw apparaatconfiguratieprofielen.  

In dit artikel wordt beschreven hoe u instellingen voor Delivery Optimization configureert als onderdeel van een apparaatconfiguratieprofiel. Nadat u een profiel hebt gemaakt, kunt u dat profiel toewijzen aan of implementeren naar uw Windows 10-apparaten.

Zie [Instellingen voor Delivery Optimization voor Intune](delivery-optimization-settings.md) voor een lijst met de instellingen voor Delivery Optimization die door Intune worden ondersteund.  

Raadpleeg [Delivery Optimization-updates](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) in de Windows-documentatie voor meer informatie over Delivery Optimization in Windows 10.  

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.

3. Voer de volgende eigenschappen in:

   - **Platform**: Kies **Windows 10 en hoger**.
   - **Profiel**: Selecteer **Delivery Optimization**.

4. Selecteer **Maken**.

5. Voer in **Basisinformatie** de volgende eigenschappen in:

   - **Naam**: Voer een beschrijvende naam in voor het nieuwe profiel.
   - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Op de pagina **Configuratie-instellingen** definieert u hoe updates en apps moeten worden gedownload. Zie [Instellingen voor Delivery Optimization voor Intune](delivery-optimization-settings.md) voor meer informatie over beschikbare instellingen.

   Wanneer u klaar bent met het configureren van instellingen, selecteert u **Volgende**.

8. Selecteer op de pagina **Bereik (tags)** de optie **Bereiktags selecteren** om het deelvenster *Tags selecteren* te openen en bereiktags toe te wijzen aan het profiel.
  
   Selecteer **Volgende** om door te gaan.

9. Selecteer op de pagina **Toewijzingen** de groepen die dit profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

   Selecteer **Volgende**.

10. Gebruik op de pagina **Toepasselijkheidregels** de opties **Regel**, **Eigenschap** en **Waarde** om te definiëren hoe dit profiel van toepassing is op toegewezen groepen.

11. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het profiel wordt gemaakt en weergegeven in de lijst.

De volgende keer dat elk apparaat incheckt, wordt het beleid toegepast.

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Delivery Optimization verwijderen uit Windows 10-updateringen

Delivery Optimization is eerder geconfigureerd als onderdeel van software-updateringen. Met ingang van februari 2019 worden de instellingen voor Delivery Optimization geconfigureerd als onderdeel van een configuratieprofiel voor een Delivery Optimization-profiel. Dit omvat extra instellingen die meer invloed hebben dan de levering van software-updates op apparaten. Als dat nog niet is gebeurd, verwijdert u de Delivery Optimization-instelling uit uw update-ringen door deze in te stellen op *Niet geconfigureerd*. Gebruik vervolgens een Delivery Optimization-profiel om het grotere aantal beschikbare opties te beheren.

1. Een configuratieprofiel voor een Delivery Optimization voor een apparaat maken:

    1. Selecteer in het Microsoft Endpoint Manager-beheercentrum de opties **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
    2. Voer de volgende eigenschappen in:

        - **Platform**: Kies **Windows 10 en hoger**.
        - **Profiel**: Selecteer **Delivery Optimization**.

    3. Selecteer **Maken**.
    4. Voer in **Basisinformatie** de volgende eigenschappen in:

        - **Naam**: Voer een beschrijvende naam in voor het nieuwe profiel.
        - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

    5. Selecteer **Volgende**.
    6. Kies in **Configuratie-instellingen** > **Downloadmodus** dezelfde modus die door de bestaande software-update-ring wordt gebruikt, *tenzij* u de instellingen die u op uw apparaten toepast, wilt wijzigen. Uw opties zijn:

        - **Niet geconfigureerd**
        - **Alleen HTTP, geen peering**
        - **HTTP gemengd met peering achter dezelfde NAT**
        - **HTTP gemengd met peering in een privégroep**
        - **HTTP met internetpeering**
        - **Eenvoudige downloadmodus zonder peering**
        - **Bypass-modus**

    7. Configureer [eventuele extra instellingen](delivery-optimization-settings.md) die u wilt beheren en ga door met het maken van het profiel.

        Wijs in **Toewijzingen** dit nieuwe profiel toe aan dezelfde apparaten en gebruikers als de bestaande software-updatering. Zie [het profiel toewijzen](device-profile-assign.md) voor meer informatie.

2. Maak de configuratie van de bestaande softwarering ongedaan:

    1. Ga in het Microsoft Endpoint Manager-beheercentrum naar **Software-updates** > Windows 10-updateringen.
    2. Selecteer uw updatering in de lijst.
    3. Stel in de instellingen **Delivery Optimization-downloadmodus** in op **Niet geconfigureerd**.
    4. Kies **OK** > **Opslaan** voor uw wijzigingen.

## <a name="next-steps"></a>Volgende stappen

Nadat u het [profiel hebt toegewezen](device-profile-assign.md), [controleert u de status](device-profile-monitor.md) van het profiel.

Bekijk de [instellingen voor Delivery Optimization](delivery-optimization-settings.md) voor Intune.

---
title: Toegangsprofielen voor resources implementeren
titleSuffix: Configuration Manager
description: Meer informatie over het implementeren van Wi-Fi-, VPN-en certificaat profielen in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0272c50429973cc3e15c295303b91593075ebe01
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724515"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>Resource toegangs profielen in Configuration Manager implementeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u een van de volgende toegangs profielen voor bronnen hebt gemaakt, implementeert u deze in een of meer verzamelingen:

- [Wi-Fi](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [Certificaat](create-certificate-profiles.md)

Wanneer u deze profielen implementeert, geeft u de doel verzameling op en geeft u op hoe vaak de client het profiel voor naleving evalueert.  

## <a name="deploy-a-profile"></a>Een profiel implementeren

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Vouw **instellingen voor naleving**uit, vouw **toegang tot bedrijfs bronnen**uit en kies vervolgens het juiste profiel knooppunt. Bijvoorbeeld **Wi-Fi-profielen**.

1. Selecteer in de lijst met profielen het profiel dat u wilt implementeren. Selecteer vervolgens op het tabblad **Start** van het lint in de groep **implementatie** de optie **implementeren**.  

1. Geef in het venster profiel implementeren de volgende informatie op:  

    - **Verzameling**: Selecteer de verzameling waarvoor u het profiel wilt implementeren.

    - **Waarschuwing genereren**: Schakel deze optie in om een waarschuwing te configureren. Deze waarschuwing wordt door de site gegenereerd als de naleving van het profiel minder is dan het opgegeven percentage met de opgegeven datum en tijd. U kunt ook selecteren of u wilt dat een waarschuwing wordt verzonden naar System Center Operations Manager.

    - **Wille keurige vertraging (uren)**: Geef voor certificaat profielen die Simple Certificate Enrollment Protocol SCEP-instellingen bevatten, een vertragings venster op om te voor komen dat de registratie service voor netwerk apparaten overmatig wordt verwerkt (NDES). De standaard waarde is `64` uren.  

    - **Geef het evaluatie schema voor naleving op voor dit... Profiel**: Geef op hoe vaak de client naleving voor dit profiel evalueert. Selecteer een **eenvoudige planning** of configureer een **aangepaste planning**. Standaard is het eenvoudige schema elke `12` uur.

1. Selecteer **OK** om het venster te sluiten en de implementatie te maken.

## <a name="delete-a-deployment"></a>Een implementatie verwijderen

Als u een implementatie wilt verwijderen, selecteert u deze in de lijst. Ga in het detail venster naar het tabblad **implementaties** . Selecteer de implementatie en selecteer vervolgens op het tabblad **implementatie** van het lint de optie **verwijderen**.

> [!IMPORTANT]
> Wanneer u de implementatie van een VPN-profiel verwijdert, verwijdert Configuration Manager het VPN-profiel niet uit Windows. Als u het profiel wilt verwijderen van apparaten, moet u dit hand matig verwijderen.

## <a name="next-steps"></a>Volgende stappen

[Wi-Fi-en VPN-profielen bewaken](monitor-wifi-email-vpn-profiles.md)

[Certificaatprofielen controleren](monitor-certificate-profiles.md)

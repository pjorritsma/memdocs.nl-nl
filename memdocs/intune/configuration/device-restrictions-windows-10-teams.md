---
title: Apparaatbeperkingen voor Surface Hub met Windows 10 Team in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Gebruik Intune om instellingen voor Surface Hub-apparaten met Windows 10 team toe te voegen of te configureren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b57bc0b7c76a6b67a26c7b1fdacb7880173a055c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429695"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>Instellingen voor Windows 10 om functies toe te staan of te beperken op Surface Hub-apparaten met behulp van Intune

In dit artikel komt u meer te weten over de Microsoft Intune-apparaatbeperkingsinstellingen die u kunt configureren voor apparaten waarop Windows 10 Team wordt uitgevoerd, inclusief de Surface Hub-apparaten.

## <a name="before-you-begin"></a>Voordat u begint

[Maak het apparaatprofiel](device-restrictions-configure.md#create-the-profile).

## <a name="apps-and-experience"></a>Apps en ervaring

Deze instellingen maken gebruik van de [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Scherm activeren wanneer iemand in de ruimte is**: Met **Blokkeren** wordt voorkomen dat het scherm automatisch wordt geactiveerd als de sensor detecteert dat er iemand in de ruimte aanwezig is. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Informatie over de vergadering die wordt weergegeven op het aanmeldingsscherm**: Kies de informatie die wordt weergegeven op de tegel Vergaderingen van het welkomstscherm. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Alleen de organisator en tijd**
  - **Organisator, tijd en onderwerp (onderwerp verborgen bij privévergaderingen)**
- **URL van de achtergrondafbeelding voor het aanmeldingsscherm**: Voer de URL van een PNG-afbeelding in die als aangepaste achtergrond moet worden weergegeven op het **welkomstscherm** op Windows 10 team-apparaten. De afbeelding moet een bestand met PNG-indeling zijn en de URL moet beginnen met `https://`.
- **Verbinding maken automatisch starten**: Met **Blokkeren** wordt voorkomen dat de app voor het maken van verbinding automatisch wordt geopend wanneer een projectie wordt gestart. Als deze is geblokkeerd, kunnen gebruikers de app voor het maken van verbinding handmatig starten vanuit de instellingen van de Hub. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Aanmeldingssuggesties**: Met **Blokkeren** wordt het automatisch vullen van het dialoogvenster voor aanmelding met genodigden van de geplande vergaderingen uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Mijn vergaderingen en bestanden**: Met **Blokkeren** wordt de functie **Mijn vergaderingen en bestanden** in het menu Start uitgeschakeld. Met deze functie worden de vergaderingen en bestanden uit Office 365 van de aangemelde gebruiker weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

## <a name="azure-operational-insights"></a>Operational Insights van Azure

- **Azure Operational Insights**: Met **Inschakelen** kunnen logboekgegevens van Windows 10 Team-apparaten worden verzameld, opgeslagen en geanalyseerd met Azure Operational Insights. Azure Operational Insights maakt deel uit van de Microsoft Operations Manager-suite. Voer de **Werkruimte-id** en een **Werkruimtesleutel** in om verbinding te maken met Azure Operational Insights.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze gegevens niet verzamelt.

## <a name="maintenance"></a>Onderhoud

Deze instellingen maken gebruik van de [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Onderhoudsvenster voor updates**: Met **Inschakelen** wordt er een onderhoudsvenster gemaakt wanneer updates kunnen worden geïnstalleerd. Voer de **Begintijd** en de **Duur in uren** (tussen 1-5 uur) in voor het onderhoudsvenster.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

## <a name="session"></a>Sessie

Deze instellingen maken gebruik van de [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Volume**: Voer de standaardvolumewaarde voor een nieuwe sessie in, van 0-100. Als u dit leeg laat, wordt deze instelling niet gewijzigd of bijgewerkt door Intune. Standaard kan het volume zijn ingesteld op 45.
- **Time-out van het scherm**: Voer het aantal minuten in waarna het hubscherm moet worden uitgeschakeld.
- **Sessietime-out**: Voer het aantal minuten in waarna er een time-out moet optreden voor de sessie.
- **Time-out voor de slaapstand**: Voer het aantal minuten in waarna het hubscherm moet overschakelen naar de slaapstand.
- **Hervatten van de sessie**: Met **Blokkeren** wordt voorkomen dat gebruikers een sessie kunnen hervatten wanneer er een time-out is opgetreden voor de sessie. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

## <a name="wireless-projection"></a>Draadloze projectie

Deze instellingen maken gebruik van de [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Pincode voor draadloze projectie**: Met **Vereisen** wordt afgedwongen dat gebruikers een pincode invoeren voordat ze de functies voor draadloze projectie op het apparaat gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Draadloze Miracast-projectie**: Met **Blokkeren** wordt voorkomen dat apparaten met Miracast-functionaliteit worden geprojecteerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Draadloos Miracast-projectiekanaal**: Selecteer het Miracast-kanaal om de verbinding tot stand te brengen.

## <a name="next-steps"></a>Volgende stappen

Zie [Apparaatbeperkingsinstellingen configureren](device-restrictions-configure.md) voor meer informatie.

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

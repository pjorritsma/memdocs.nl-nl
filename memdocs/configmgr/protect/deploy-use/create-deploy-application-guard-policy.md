---
title: Beleid voor toepassings beveiliging beheren
titleSuffix: Configuration Manager
description: Meer informatie over het maken en implementeren van micro soft Defender Application Guard-beleid
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1189f8c89215bc228c533a88f38f5ae59b6855ee
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/05/2020
ms.locfileid: "84454933"
---
# <a name="create-and-deploy-microsoft-defender-application-guard-policy"></a>Micro soft Defender Application Guard-beleid maken en implementeren

*Van toepassing op: Configuration Manager (huidige vertakking)*
<!-- 1351960 -->  
U kunt beleids regels voor [micro soft Defender Application Guard (toepassings beveiligings beleid)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview) maken en implementeren met behulp van de Configuration Manager Endpoint Protection. Met deze beleids regels kunt u uw gebruikers beschermen door niet-vertrouwde websites te openen in een beveiligde geïsoleerde container die niet toegankelijk is voor andere onderdelen van het besturings systeem.

## <a name="prerequisites"></a>Vereisten

Als u een micro soft Defender Application Guard-beleid wilt maken en implementeren, moet u de update van Windows 10 najaar Maker (1709) gebruiken. De Windows 10-apparaten waarop u het beleid implementeert, moeten worden geconfigureerd met een [netwerk isolatie beleid](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard#network-isolation-settings). Zie voor meer informatie het [overzicht van micro soft Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Een beleid maken en bladeren door de beschik bare instellingen

1. Kies in de Configuration Manager-console **activa en naleving**.
2. Kies **overzicht**Endpoint Protection **Assets and Compliance**  >  **Endpoint Protection**  >  **Windows Defender Application Guard**in de werk ruimte activa en naleving.
3. Klik op het tabblad **Start** in de groep **maken** op **Windows Defender Application Guard-beleid maken**.
4. Met behulp van het [artikel](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard) als referentie kunt u de beschik bare instellingen bekijken en configureren. Met Configuration Manager kunt u bepaalde beleids instellingen instellen:
   - [Instellingen voor interactie met host](#bkmk_HIS)
   - [Toepassings gedrag](#bkmk_ABS)
   - [Bestands beheer](#bkmk_FM)
5. Geef op de pagina **netwerk definitie** de bedrijfs identiteit op en definieer de grens van uw bedrijfs netwerk.

    > [!NOTE]
    > Windows 10-Pc's slaan slechts één netwerk isolatie lijst op de client op. U kunt twee verschillende soorten netwerk isolatie lijsten maken en deze op de client implementeren:
    >
    >  - een van Windows Information Protection
    >  - een van micro soft Defender Application Guard
    >
    > Als u beide beleids regels implementeert, moeten deze netwerk isolatie lijsten overeenkomen. Als u lijsten implementeert die niet overeenkomen met dezelfde client, mislukt de implementatie. Zie de [Windows Information Protection-documentatie](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)voor meer informatie.

6. Wanneer u klaar bent, voltooit u de wizard en implementeert u het beleid op een of meer Windows 10 1709-apparaten.

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a>Instellingen voor interactie met host

Hiermee configureert u interacties tussen hostcomputers en de Application Guard-container. Vóór Configuration Manager versie 1802 bevonden zowel het toepassings gedrag als de interactie met de host zich op het tabblad **instellingen** .

- **Klem bord** -onder instellingen vóór Configuration Manager 1802
  - Toegestaan inhouds type
    - Tekst
    - Installatiekopieën
- **Afdrukken**
  - Afdrukken naar XPS inschakelen
  - Afdrukken naar PDF inschakelen
  - Afdrukken naar lokale printers inschakelen
  - Afdrukken naar netwerk printers inschakelen
- **Graphics:** (vanaf Configuration Manager versie 1802)
  - Toegang tot virtuele grafische processor
- **Bestanden:** (vanaf Configuration Manager versie 1802)
  - Gedownloade bestanden opslaan op de host

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a>Instellingen voor toepassings gedrag

Hiermee configureert u het gedrag van de toepassing in de Application Guard-sessie. Vóór Configuration Manager versie 1802 bevonden zowel het toepassings gedrag als de interactie met de host zich op het tabblad **instellingen** .

- **Inhoudbeheer**
  - Enter prise-sites kunnen niet-bedrijfs inhoud laden, zoals invoeg toepassingen van derden.
- **Daarenteg**
  - Door de gebruiker gegenereerde browsergegevens behouden
  - Beveiligings gebeurtenissen in de geïsoleerde Application Guard-sessie controleren

### <a name="file-management"></a><a name="bkmk_FM"></a>Bestands beheer
<!--3555858-->
Vanaf Configuration Manager versie 1906 is er een beleids instelling waarmee gebruikers bestanden kunnen vertrouwen die normaal in Application Guard worden geopend. Wanneer de uitvoering is voltooid, worden de bestanden geopend op het hostapparaat in plaats van in Application Guard. Zie [beleids instellingen voor micro soft Defender Application Guard configureren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard)voor meer informatie over het beleid voor toepassings beveiliging.

- **Gebruikers toestaan bestanden te vertrouwen die worden geopend in Windows Defender Application Guard** : Hiermee stelt u de gebruiker in staat om bestanden te markeren als vertrouwd. Wanneer een bestand wordt vertrouwd, wordt het geopend op de host in plaats van in Application Guard. Is van toepassing op Windows 10-versie 1809 of hoger.
  - **Verboden:** Gebruikers niet toestaan om bestanden te markeren als vertrouwd (standaard).
  - **Bestand gecontroleerd door anti virus:** Gebruikers toestaan om bestanden te markeren als vertrouwd na een antivirus controle.
  - **Alle bestanden:** Gebruikers toestaan om een bestand als vertrouwd te markeren.

Wanneer u bestands beheer inschakelt, ziet u mogelijk fouten die zijn vastgelegd in het DCMReporting. log van de client. De volgende fouten hebben doorgaans geen invloed op de functionaliteit: <!--4619457-->

- Op compatibele apparaten:
  - FileTrustCriteria_condition niet gevonden
- Op niet-compatibele apparaten:
  - FileTrustCriteria_condition niet gevonden
  - FileTrustCriteria_condition kan niet worden gevonden in de kaart
  - FileTrustCriteria_condition niet gevonden in samen vatting

Als u de instellingen voor Application Guard wilt bewerken, vouwt u **Endpoint Protection** uit in de werk ruimte **activa en naleving** en klikt u vervolgens op het knoop punt **Windows Defender Application Guard** . Klik met de rechter muisknop op het beleid dat u wilt bewerken en selecteer vervolgens **Eigenschappen**.

## <a name="known-issues"></a>Bekende problemen

Op apparaten met Windows 10, versie 2004 worden fouten weer gegeven in nalevings rapportage voor de vertrouwens criteria van micro soft Defender Application Guard-bestanden. Dit probleem treedt op omdat sommige subklassen zijn verwijderd uit de WMI-klasse `MDM_WindowsDefenderApplicationGuard_Settings01` in Windows 10, versie 2004. Alle andere micro soft Defender Application Guard-instellingen zijn nog steeds van toepassing. alleen de vertrouwens criteria van het bestand zullen mislukken. Er zijn momenteel geen tijdelijke oplossingen om de fout te omzeilen. <!--7099444,5946790-->

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over micro soft Defender Application Guard
 - [Overzicht van micro soft Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview).
- [Veelgestelde vragen over micro soft Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/faq-md-app-guard).

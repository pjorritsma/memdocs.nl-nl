---
title: Problemen met e-mailprofielen oplossen in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk veelvoorkomende problemen met en oplossingen voor e-mailprofielen in Microsoft Intune, waaronder dubbele e-mailprofielen en fouten op Samsung KNOX Standard Android-apparaten.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d011d6111ede4bb5879e53e771d20b792bf00d3
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995123"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Veelvoorkomende problemen met en oplossingen voor e-mailprofielen in Microsoft Intune

Lees welke problemen met e-mailprofielen zich vaak voordoen en hoe u deze kunt oplossen.

## <a name="users-are-repeatedly-prompted-to-enter-their-password"></a>Gebruikers worden herhaaldelijk gevraagd om hun wachtwoord in te voeren

Gebruikers worden herhaaldelijk gevraagd om hun wachtwoord in te voeren voor het e-mailprofiel. Als er certificaten worden gebruikt voor het verifiëren en autoriseren van de gebruiker, controleert u de toewijzingen van alle certificaatprofielen. Deze certificaatprofielen worden normaal gesproken toegewezen aan gebruikersgroepen, niet aan apparaatgroepen. Als een van de certificaatprofielen niet is gericht op een gebruiker, blijft Intune proberen het e-mailprofiel opnieuw te implementeren.

Als de keten van e-mailprofielen is toegewezen aan gebruikersgroepen, moet u ervoor zorgen dat uw certificaatprofielen ook aan gebruikersgroepen worden toegewezen.

## <a name="profiles-deployed-to-device-groups-show-errors-and-latency"></a>Profielen die zijn geïmplementeerd op apparaatgroepen vertonen fouten en latentie

E-mailprofielen worden meestal toegewezen aan gebruikersgroepen. Er kunnen bepaalde gevallen zijn waarin ze aan apparaatgroepen worden toegewezen.

- U wilt bijvoorbeeld een e-mailprofiel op basis van een certificaat implementeren op alleen Surface-apparaten, niet op bureaubladen. In dit scenario kunnen apparaatgroepen zinvol zijn. U weet dat deze apparaten kunnen worden weergegeven als niet-compatibel, fouten kunnen retourneren en uw e-mailprofielen mogelijk niet direct ophalen.

  In dit voorbeeld maakt u het e-mailprofiel en wijst u het profiel aan apparaatgroepen toe. Het apparaat wordt opnieuw opgestart en er is een vertraging voordat een gebruiker zich aanmeldt. Tijdens deze vertraging wordt uw PKCS-certificaatprofiel, dat is toegewezen aan gebruikersgroepen, geïmplementeerd. Omdat er nog geen gebruiker is, zorgt het PKCS-certificaatprofiel ervoor dat het apparaat niet compatibel is. Logboeken kan ook fouten op het apparaat weergeven.

  Als de gebruiker het apparaat compatibel wil maken, meldt deze zich aan bij het apparaat en synchroniseert het met Intune om het beleid te ontvangen. Gebruikers kunnen handmatig opnieuw synchroniseren of wachten op de volgende synchronisatie.

- U gebruikt bijvoorbeeld dynamische groepen. Als de dynamische groepen niet onmiddellijk door Azure AD worden bijgewerkt, worden deze apparaten mogelijk weergegeven als niet-compatibel.

In deze scenario's bepaalt u of het belangrijker is om apparaatgroepen te gebruiken, of belangrijker om alle beleidsregels als compatibel weer te geven.

## <a name="device-already-has-an-email-profile-installed"></a>Er is al een e-mailprofiel geïnstalleerd op het apparaat

Als gebruikers een e-mailprofiel maken voordat ze zich inschrijven in Intune of Microsoft 365 MDM, werkt het e-mailprofiel dat door Intune is geïmplementeerd mogelijk niet zoals verwacht:

- **iOS/iPadOS**: Intune detecteert een bestaand, dubbel e-mailprofiel op basis van hostnaam en e-mailadres. Het door de gebruiker gemaakte e-mailprofiel blokkeert de implementatie van het in Intune gemaakte profiel. Dit scenario is een veelvoorkomend probleem, omdat iOS-/iPadOS-gebruikers vaak zelf een e-mailprofiel maken en het apparaat vervolgens inschrijven. De bedrijfsportal-app geeft aan dat de gebruiker niet compatibel is en kan de gebruiker vragen om het e-mailprofiel te verwijderen.

  De gebruiker moet het e-mailprofiel verwijderen, zodat het Intune-profiel kan worden geïmplementeerd. Voorkom dit probleem door gebruikers te vertellen dat ze zich moeten inschrijven en Intune toe te staan het e-mailprofiel te implementeren. Vervolgens kunnen gebruikers hun e-mailprofiel aanmaken.

- **Windows**: Intune detecteert een bestaand, dubbel e-mailprofiel op basis van hostnaam en e-mailadres. Intune overschrijft het bestaande e-mailprofiel dat is gemaakt door de gebruiker.

- **Samsung KNOX Standard**: Intune identificeert een dubbel e-mailaccount op basis van het e-mailadres, en overschrijft het met het Intune-profiel. Als de gebruiker dat account configureert, wordt het opnieuw overschreven door het Intune-profiel. Dit gedrag kan leiden tot enige verwarring bij de gebruiker van wie de accountconfiguratie wordt overschreven.

Samsung KNOX gebruikt geen hostnaam om het profiel te identificeren. U kunt het beste niet meerdere e-mailprofielen maken om hetzelfde e-mailadres op verschillende hosts te implementeren, aangezien deze profielen door elkaar worden overschreven.

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>Fout 0x87D1FDE8 voor KNOX Standard-apparaat

**Probleem**: na het maken en implementeren van een Exchange Active Sync-e-mailprofiel voor Samsung KNOX Standard voor verschillende Android-apparaten, wordt door de apparaten **0x87D1FDE8** of de fout **Doorvoeren is mislukt** weergegeven in het tabblad Beleid van de eigenschappen van het apparaat.

Controleer de configuratie van uw EAS-profiel voor Samsung KNOX en het bronbeleid. De synchronisatieoptie voor Samsung Notes wordt niet meer ondersteund en deze optie moet niet worden geselecteerd in uw profiel. Geef de apparaten voldoende tijd (maximaal 24 uur) om het beleid te verwerken.

## <a name="unable-to-send-images-from--email-account"></a>Kan geen afbeeldingen verzenden vanuit e-mailaccount

Gebruikers met automatisch geconfigureerde e-mailaccounts kunnen geen afbeeldingen of foto's verzenden vanaf hun apparaat. Dit scenario kan zich voordoen als de optie **Toestaan dat e-mails worden verzonden vanuit toepassingen van derden** niet is ingeschakeld.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen**.
3. Selecteer uw e-mailprofiel > **Eigenschappen** > **Instellingen**.
4. Stel **Toestaan dat e-mails worden verzonden vanuit toepassingen van derden** in op **Inschakelen**.

## <a name="next-steps"></a>Volgende stappen

Krijg [ondersteuning van Microsoft](../fundamentals/get-support.md) of gebruik de [communityforums](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).

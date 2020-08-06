---
title: Een vereist certificaat dat ontbreekt, installeren
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/29/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f0ba4cbb-ef0a-4335-86bf-f1d006867fa2
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 162a5c2ff02a762578fb6f52b60b6ff404862329
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546705"
---
# <a name="install-missing-certificate-required-by-your-organization"></a>Een ontbrekend certificaat installeren dat is vereist voor uw organisatie  

Als uw apparaat niet bij Intune is geregistreerd en er ontbreekt een vereist certificaat, kunt u zich niet aanmelden bij de bedrijfsportal-app. Wanneer u zich probeert aan te melden, wordt het volgende bericht weergegeven:

![screenshot-error-message-about-missing-certificate](./media/andr-cert_install-1-cert_missing.png)

Er zijn twee opties die u kunt proberen om het vereiste certificaat te downloaden en uw apparaat in te schrijven. 

- Browsertoegang inschakelen in de bedrijfsportal-app.
- Identificeer het ontbrekende certificaat op een pc op uw werk of school. Zoek dan op internet om het ontbrekende certificaat te downloaden. 

Voltooi eerst de stappen voor het inschakelen van browsertoegang. Als u het apparaat nog steeds niet kunt registreren, volgt u de stappen om het certificaat op internet te vinden. 

## <a name="enable-browser-access"></a>Browsertoegang inschakelen
Voer deze stappen uit om browsertoegang in te schakelen. Nadat u toegang hebt ingeschakeld, installeert de bedrijfsportal het juiste certificaat en wordt de registratie voortgezet.    

1. Ga in de bedrijfsportal-app naar de rechterbovenhoek en selecteer het menu.  
2. Selecteer **Instellingen**.  
3. Selecteer **Inschakelen** naast **Browsertoegang inschakelen**.  
4. Selecteer **ACTIVEREN** in het venster Apparaatbeheerder. 

## <a name="identify-and-download-the-missing-certificate-through-web-search"></a>Het ontbrekende certificaat identificeren en downloaden door te zoeken op internet
Voer deze stappen uit om het certificaat handmatig te identificeren en te installeren op uw apparaat.  

1. Open Internet Explorer op een pc. Als u voor dit doel niet over een pc beschikt, neemt u contact op met het ondersteuningsteam van uw bedrijf. Ga naar de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980) voor de contactgegevens van het ondersteuningsteam van uw bedrijf.

2. Ga naar de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980) en meld u aan met de referenties van uw werk- of schoolaccount.

3. Rechts van de adresbalk van de browser kiest u het symbool dat lijkt op een hangslot, zoals hieronder is weergegeven.

    ![screenshot-internet-explorer-address-bar-padlock-symbol](./media/andr-missing-cert-ie-padlock-symbol.png)

    Als u het hangslot niet ziet, stopt u en neemt u contact op met het ondersteuningsteam van uw bedrijf. Het hangslot betekent dat u veilig bent aangemeld. Ga dus alleen verder als u dit symbool ziet.

4. Kies **Certificaten weergeven**.

    ![screenshot-internet-explorer-view-certificates-button-on-website-identification-dialog](./media/andr-missg-cert-ie-view-cert-button.png)

5. Kies het tabblad **Certificaatpad** en identificeer vervolgens het certificaat dat u van internet moet ophalen. De naam van het certificaat dat u nodig hebt, bevindt zich op dezelfde positie als het gemarkeerde certificaat in het voorgaande voorbeeld.

6. Gebruik een zoekmachine zoals Bing of Google, en zoek op de naam van het ontbrekende certificaat dat u in het vorige gedeelte hebt geïdentificeerd. Het certificaat kan verschillende extensies hebben, zoals '.crt' of '.pem', enzovoort.

7. Download het basiscertificaat van de website.

8. Nadat het certificaat is gedownload, sleept u omlaag vanaf de bovenkant van uw apparaat om de meldingen te openen en vervolgens tikt u op de naam van het certificaat in de lijst met meldingen.

4. In het dialoogvenster **Benoem het certificaat** dat hieronder wordt weergegeven, accepteert u de standaardcertificaatnaam.

5. Zorg ervoor dat **Gebruik van referenties** is ingesteld op **Worden gebruikt voor VPN en apps** en tik op **OK**.

    ![screenshot-certificate-name-dialog-showing-certificate-name](./media/andr-missing-cert-cert-name.png)

6. Sluit de bedrijfsportal-app.

7. Open de bedrijfsportal-app opnieuw. Nu moet u zich bij de bedrijfsportal-app kunnen aanmelden. Neem contact op met het ondersteuningsteam van uw bedrijf als u hulp nodig hebt.

Als u dezelfde melding over een 'ontbrekend certificaat' ziet als de melding die eerder werd weergegeven en u de procedure al hebt uitgevoerd, is er waarschijnlijk nog een ander certificaat dat door het ondersteuningsteam van uw bedrijf moet worden geïnstalleerd. Neem contact op met het ondersteuningsteam van uw bedrijf voor hulp bij het gebruik van de contactgegevens die beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).

## <a name="next-steps"></a>Volgende stappen  

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).  

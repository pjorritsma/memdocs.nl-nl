---
title: Windows-apps sideloaden
titleSuffix: Microsoft Intune
description: Leer hoe u Line-Of-Business-apps ondertekent, zodat u Intune kunt gebruiken voor de implementatie van deze apps.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e44f1756-52e1-4ed5-bf7d-0e80363a8674
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb981563c2d98389f6d1dda4d050e391e9ad5637
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910465"
---
# <a name="sign-line-of-business-apps-so-they-can-be-deployed-to-windows-devices-with-intune"></a>Line-of-business-apps ondertekenen, zodat ze kunnen worden geïmplementeerd op Windows-apparaten met Intune

Als Intune-beheerder kunt u universele LOB-apps (Line-of-Business) implementeren op Windows 8.1 Desktop of Windows 10 Desktop en Mobile-apparaten, met inbegrip van de bedrijfsportal-app. Als u *APPX*-apps wilt implementeren op Windows 8.1 Desktop- of Windows 10 Desktop- en Mobile-apparaten, kunt u een certificaat voor ondertekening bij programmacode van een openbare certificeringsinstantie gebruiken die al wordt vertrouwd op uw Windows-apparaten, of u kunt uw eigen certificeringsinstantie gebruiken.

 > [!NOTE]
 > Voor Windows 8.1 Desktop is bedrijfsbeleid vereist om sideloaden mogelijk te maken, of u moet sideloadsleutels gebruiken (automatisch ingeschakeld voor aan een domein toegevoegde apparaten). Zie [Windows 8 sideloaden](/archive/blogs/scd-odtsp/windows-8-sideloading-requirements-from-technet)voor meer informatie.

## <a name="windows-10-sideloading"></a>Sideloaden in Windows 10

In Windows 10 is sideloaden anders dan in eerdere versies van Windows:

- Met behulp van bedrijfsbeleid kunt u een apparaat ontgrendelen voor sideloaden. Intune biedt configuratiebeleid voor apparaten genaamd Vertrouwde app-installatie. U hoeft dit beleid alleen maar in stellen op <allow> voor apparaten waarop het certificaat dat wordt gebruikt om de APPX-app te ondertekenen, al wordt vertrouwd.

- Symantec Phone-certificaten en sideloadlicentiesleutels zijn niet vereist. Als er echter geen on-premises certificeringsinstantie beschikbaar is, moet u mogelijk een certificaat voor ondertekening van programmacode verkrijgen bij een openbare certificeringsinstantie. Zie [Inleiding tot ondertekening van programmacode](/windows/desktop/SecCrypto/cryptography-tools#introduction-to-code-signing) voor meer informatie.

### <a name="code-sign-your-app"></a>Ondertekenen van programmacode voor uw app

De eerste stap is het ondertekenen van programmacode voor uw appx-pakket. Zie [Sign app package using SignTool](/windows/uwp/packaging/sign-app-package-using-signtool) (App-pakket ondertekenen met behulp van SignTool) voor meer informatie.

### <a name="upload-your-app"></a>Uw app uploaden

Vervolgens moet u het ondertekende appx-bestand uploaden. Zie [Een Windows Line-Of-Business-app toevoegen aan Microsoft Intune](lob-apps-windows.md) voor meer informatie.

Als u de app, zoals vereist, implementeert voor gebruikers of apparaten, hebt u de Intune-bedrijfsportal-app niet nodig. Als u de app echter implementeert als beschikbaar voor gebruikers, kunnen zij de bedrijfsportal-app gebruiken vanuit de openbare Microsoft Store of vanuit de persoonlijke Microsoft Store voor Bedrijven, of u moet de Intune-bedrijfsportal-app handmatig implementeren.

### <a name="upload-the-code-signing-certificate"></a>Het certificaat voor ondertekening van programmacode uploaden

Als op uw Windows 10-apparaat de certificeringsinstantie nog niet wordt vertrouwd, moet u - nadat u het APPX-pakket hebt ondertekend en geüpload naar de Intune-service - het certificaat voor ondertekening van programmacode uploaden naar de Intune-portal:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Klik op **Tenantbeheer** > **Connectors en tokens** > **Windows Enterprise-certificaten**.
3. Selecteer een bestand onder **Certificaatbestand voor handtekening bij programmacode**.
4. Selecteer uw *CER*-bestand en klik op **Openen**.
5. Klik op **Uploaden** om uw certificaatbestand aan Intune toe te voegen.

Nu wordt op elk Windows 10 Desktop en Mobile-apparaat met een APPX-implementatie van de Intune-service, automatisch het bijbehorende ondernemingscertificaat gedownload. Na de installatie kan de toepassing worden gestart.

In Intune wordt alleen het meest recent geüploade CER-bestand geïmplementeerd. Als u meerdere APPX-bestanden hebt die zijn gemaakt door verschillende ontwikkelaars die niet zijn verbonden aan uw organisatie, moet u hun vragen niet-ondertekende APPX-bestanden te leveren om te ondertekenen met uw certificaat, of moet u hun het certificaat voor ondertekening van programmacode geven dat wordt gebruikt in uw organisatie.

## <a name="how-to-renew-the-symantec-enterprise-code-signing-certificate"></a>Het zakelijke Symantec-certificaat voor ondertekening van programmacode vernieuwen

Het certificaat dat is gebruikt om mobiele Windows Phone 8.1-apps te implementeren is op 28 februari 2019 buiten gebruik gesteld, en kan niet meer worden vernieuwd bij Symantec. Daarnaast heeft Intune de ondersteuning voor Windows 10 Mobile vanaf 10 augustus 2020 beëindigd.

## <a name="how-to-install-the-updated-certificate-for-line-of-business-lob-apps"></a>Het bijgewerkte certificaat voor LOB-apps (line-of-business) installeren

Windows Phone 8.1

LOB-apps voor dit platform kunnen niet meer worden geïmplementeerd in de Intune-service zodra het bestaande certificaat voor ondertekening van programmacode voor Symantec Mobile Enterprise verloopt.

Windows 8.1 Desktop/Windows 10 Desktop en Mobile

Als de certificaatperiode is verlopen, kunnen de APPX-bestanden mogelijk niet meer worden gestart. U moet een nieuw CER-bestand verkrijgen en de instructies volgen voor het ondertekenen van programmacode voor elk geïmplementeerd APPX-bestand. En u moet alle APPX-bestanden en het bijgewerkte CER-bestand opnieuw uploaden naar de sectie Windows Enterprise-certificaten van de Intune-portal

## <a name="manually-deploy-windows-10-company-portal-app"></a>De Windows 10-bedrijfsportal-app handmatig implementeren

Als u geen toegang wilt bieden tot de Microsoft Store, kunt u de Bedrijfsportal-app voor Windows 10 handmatig rechtstreeks implementeren vanuit Intune, zelfs als u Intune niet hebt geïntegreerd met MSFB (Microsoft Store voor Bedrijven). Als u MSFB wel hebt geïntegreerd, kunt u de bedrijfsportal-app ook implementeren met [apps implementeren met behulp van MSFB.](store-apps-windows.md)

 > [!NOTE]
 > Voor deze optie is handmatige implementatie van updates vereist voor elke app-update.

1. Meld u aan bij uw account in [Microsoft Store voor Bedrijven](https://www.microsoft.com/business-store) en schaf de versie met de **offlinelicentie** aan in de bedrijfsportal-app.  
2. Zodra de app is aangeschaft, selecteert u de app op de pagina **Inventaris**.  
3. Selecteer **Windows 10 alle apparaten** als **Platform**. Klik vervolgens op de betreffende **Architectuur** en download. Een app-licentiebestand is niet nodig voor deze app.
   ![Afbeelding van Windows 10 X86-pakketdetails voor downloaden](./media/app-sideload-windows/Win10CP-all-devices.png)
4. Download alle pakketten onder 'Vereiste frameworks'. Dit moet worden uitgevoerd voor x86-, x64-, ARM- en ARM64-architecturen. In totaal zijn dit 9 pakketten, zoals hieronder weergegeven.

   ![Afbeelding van afhankelijkheidsbestanden voor downloaden ](./media/app-sideload-windows/Win10CP-dependent-files.png)
5. Voordat u de bedrijfsportal-app uploadt naar Intune, maakt u een map (bijvoorbeeld C:&#92;Company Portal) waarin de pakketten als volgt zijn gestructureerd:
   1. Plaats het bedrijfsportalpakket in C:\Bedrijfsportal. Maak op deze locatie tevens een submap Afhankelijkheden.  
      ![Afbeelding van de map Afhankelijkheden waarin het APPXBUN-bestand is opgeslagen](./media/app-sideload-windows/Win10CP-Dependencies-save.png)
   2. Plaats de negen afhankelijkheidspakketten in de map Afhankelijkheden.  
      Als de afhankelijkheden niet in deze indeling worden geplaatst, worden ze niet herkend door Intune en kunnen ze niet worden geüpload tijdens de pakket-upload. Het uploaden mislukt met de volgende fout.  
      <img alt="Error message - The Windows app dependency must be provided." src="./media/app-sideload-windows/Win10CP-error-message.png" width="200">
6. Ga terug naar Intune en upload the Bedrijfsportal-app als nieuwe app. Implementeer als vereiste app naar de gewenste set doelgebruikers.  

Zie [Deploying an appxbundle with dependencies via Microsoft Intune MDM](/archive/blogs/configmgrdogs/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm) (Een appxbundle met afhankelijkheden implementeren via Microsoft Intune MDM) voor meer informatie over hoe Intune afhankelijkheden voor universele apps verwerkt.  

### <a name="how-do-i-update-the-company-portal-on-my-users-devices-if-they-have-already-installed-the-older-apps-from-the-store"></a>Hoe kan ik de Bedrijfsportal op de apparaten van mijn gebruikers bijwerken als hierop al de oudere apps uit de Store zijn geïnstalleerd?

Als uw gebruikers de Windows 8.1-bedrijfsportal-apps al hebben geïnstalleerd vanuit de Store, moeten deze automatisch worden bijgewerkt naar de nieuwe versie, zonder dat hiervoor actie door u of uw gebruikers is vereist. Als de update niet wordt uitgevoerd, vraagt u uw gebruikers om te controleren of automatische updates voor Store-apps op hun apparaten is ingeschakeld.

### <a name="how-do-i-upgrade-my-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Hoe ik een upgrade uitvoeren van mijn gesideloade Windows 8.1-bedrijfsportal-app naar de Windows 10-bedrijfsportal-app?

Het wordt aanbevolen de implementatie voor de Bedrijfsportal-app voor Windows 8.1 te verwijderen door de implementatieactie in te stellen op 'Installatie ongedaan maken'. Zodra deze actie is uitgevoerd, kan de Windows 10-bedrijfsportal-app worden geïmplementeerd via een van de bovenstaande opties.  

Als u de app moet sideloaden en de Windows 8.1-bedrijfsportal hebt geïmplementeerd zonder deze ondertekenen met het Symantec-certificaat, volgt u de stappen in de bovenstaande sectie Deploy directly via Intune (Rechtstreeks implementeren via Intune) om de upgrade te voltooien.

Als u de app moet sideloaden en de Windows 8.1-bedrijfsportal hebt ondertekend en geïmplementeerd met het Symantec-certificaat voor ondertekening van programmacode, volgt u de stappen in de onderstaande sectie.  

### <a name="how-do-i-upgrade-my-signed-and-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Hoe kan ik een upgrade uitvoeren van mijn ondertekende en gesideloade Windows 8.1-bedrijfsportal-app naar de Windows 10-bedrijfsportal-app?

Het wordt aanbevolen de bestaande implementatie voor de Bedrijfsportal-app voor Windows 8.1 te verwijderen door de implementatieactie in te stellen op 'Installatie ongedaan maken'. Zodra deze actie is uitgevoerd, kan de Windows 10-bedrijfsportal-app normaal worden geïmplementeerd.  

Anders moet de Windows 10-bedrijfsportal-app op de juiste manier worden bijgewerkt en ondertekend om ervoor te zorgen dat het upgradepad in acht wordt genomen.  

Als de Windows 10-bedrijfsportal-app op deze manier is ondertekend en geïmplementeerd, moet u dit proces herhalen voor elke nieuwe app-update wanneer deze beschikbaar is in de Store. De app wordt niet automatisch bijgewerkt wanneer de Store wordt bijgewerkt.  

U ondertekent en implementeert de app als volgt:

1. Download het ondertekeningsscript voor de Microsoft Intune Windows 10-bedrijfsportal-app van [https://aka.ms/win10cpscript](https://aka.ms/win10cpscript).  Voor dit script moet de Windows SDK voor Windows 10 moet zijn geïnstalleerd op de hostcomputer. Ga naar [https://go.microsoft.com/fwlink/?LinkId=619296](https://go.microsoft.com/fwlink/?LinkId=619296) om de Windows SDK voor Windows 10 te downloaden.
2. Download de Windows 10-bedrijfsportal-app vanuit Microsoft Store voor Bedrijven, zoals hierboven beschreven.  
3. Voer het script uit met de invoerparameters die zijn opgegeven in de koptekst van het script om de Windows-10-bedrijfsportal-app (hieronder uitgepakt) te ondertekenen. Afhankelijkheden hoeven niet in het script te worden doorgegeven. Deze zijn alleen vereist wanneer de app wordt geüpload naar de Intune-beheerconsole.

|       Parameter       |                                                                    Beschrijving                                                                    |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| InputWin10AppxBundle  |                                             Het pad naar het bron-appxbundle-bestand.                                              |
| OutputWin10AppxBundle |                                                  Het uitvoerpad voor het ondertekende appxbundle-bestand.                                                  |
|       Win81Appx       |                          Het pad naar het Windows 8.1-bedrijfsportalbestand (het appx-bestand).                           |
|      PfxFilePath      |                                   Het pad naar het certificaat voor ondertekening van programmacode voor mobiele bedrijfsapparaten van Symantec (het PFX-bestand).                                    |
|      PfxPassword      |                                     Het wachtwoord voor het certificaat voor ondertekening van programmacode voor mobiele bedrijfsapparaten van Symantec.                                      |
|      PublisherId      |      De uitgevers-id van de onderneming. Als deze niet is opgegeven, wordt het veld Onderwerp van Symantec Enterprise-certificaat voor ondertekening van mobiele code gebruikt.       |
|        SdkPath        | Het pad naar de hoofdmap van de Windows-SDK voor Windows 10. Dit argument is optioneel en wordt standaard ingesteld op ${env:ProgramFiles(x86)} \Windows Kits\10 |

Via het script wordt de ondertekende versie van de Windows 10-bedrijfsportal-app uitgevoerd wanneer het uitvoeren van de app is voltooid. Vervolgens implementeert u de ondertekende versie van de app als een LOB-app via Intune. De huidige geïmplementeerde versies worden bijgewerkt naar deze nieuwe app.
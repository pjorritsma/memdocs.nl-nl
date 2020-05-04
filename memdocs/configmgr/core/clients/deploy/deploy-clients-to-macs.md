---
title: Mac-clients implementeren
titleSuffix: Configuration Manager
description: Meer informatie over het implementeren van clients op Mac-computers in Configuration Manager.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8993f4c05b7156f3aecf6fcc9c8ea3790e49e98d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713441"
---
# <a name="how-to-deploy-clients-to-macs"></a>Clients op Macs implementeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel wordt beschreven hoe u de Configuration Manager-client op Mac-computers implementeert en onderhoudt. Zie voor [bereiding voor het implementeren van client software op Macs](prepare-to-deploy-mac-clients.md)voor meer informatie over wat u moet configureren voordat u clients implementeert voor Mac-computers.

Wanneer u een nieuwe client voor Mac-computers installeert, moet u mogelijk ook Configuration Manager updates installeren om de nieuwe client informatie in de Configuration Manager-console weer te geven.

In deze procedures hebt u twee opties voor het installeren van client certificaten. Meer informatie over client certificaten voor Macs vindt u in de voor [bereiding van het implementeren van client software op Macs](prepare-to-deploy-mac-clients.md#certificate-requirements).  

- Gebruik het [CMEnroll-hulp programma](#bkmk_enroll)om Configuration Manager-inschrijving te gebruiken. Het registratie proces biedt geen ondersteuning voor automatische certificaat vernieuwing. Schrijf de Mac-computer opnieuw in voordat het geïnstalleerde certificaat verloopt.    

- [Gebruik een certificaat aanvraag en installatie methode die onafhankelijk is van Configuration Manager](#bkmk_external).  

> [!IMPORTANT]  
> Als u de-client wilt implementeren op apparaten met macOS Sierra, moet de **onderwerpnaam** van het beheer punt certificaat correct worden geconfigureerd. Gebruik bijvoorbeeld de FQDN-naam van de beheer punt server.



## <a name="configure-client-settings"></a>Clientinstellingen configureren  

De [standaard client instellingen](about-client-settings.md) gebruiken om de inschrijving voor Mac-computers te configureren. U kunt geen aangepaste client instellingen gebruiken. Om het certificaat aan te vragen en te installeren, moeten voor de Configuration Manager-client voor Mac de standaard client instellingen worden ingesteld.  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Selecteer het knoop punt **client instellingen** en selecteer vervolgens **standaard client instellingen**.  

2. Klik op het tabblad **Start** van het lint in de groep **Eigenschappen** op **Eigenschappen**.  

3. Selecteer de sectie **inschrijving** en configureer de volgende instellingen:  

    1. **Gebruikers toestaan mobiele apparaten en Mac-computers in te schrijven**: **Ja**  

    2. **Inschrijvings profiel:** Kies **profiel instellen**.  

4. Kies in het dialoog venster **inschrijvings profiel voor mobiele apparaten** **maken**.  

5. Voer in het dialoog venster **inschrijvings profiel maken** een naam in voor dit inschrijvings profiel. Configureer vervolgens de **beheer site code**. Selecteer de Configuration Manager primaire site die de beheer punten voor deze Mac-computers bevat.  

    > [!NOTE]  
    >  Als u de site niet kunt selecteren, moet u ervoor zorgen dat u ten minste één beheer punt in de site configureert ter ondersteuning van mobiele apparaten.  

6. Kies **toevoegen**.  

7. Selecteer in het venster **certificerings instantie voor mobiele apparaten toevoegen** de certificerings instantie server die certificaten uitgeeft aan Mac-computers.  

8. Selecteer in het dialoog venster **inschrijvings profiel maken** het certificaat sjabloon van de Mac-computer die u eerder hebt gemaakt.  

9. Selecteer **OK** om het dialoog venster **inschrijvings profiel** te sluiten en klik vervolgens in het dialoog venster **standaard client instellingen** .  

    > [!TIP]  
    > Als u het client beleid-interval wilt wijzigen, gebruikt u **polling interval voor client beleid** in de groep **client beleid** client instelling.  

De volgende keer dat de apparaten client beleid downloaden, Configuration Manager deze instellingen Toep assen voor alle gebruikers. Zie [het ophalen van beleid initiëren voor een Configuration Manager-client](../manage/manage-clients.md#BKMK_PolicyRetrieval)om het ophalen van het beleid voor één client te initiëren.  

Naast de instellingen voor de registratie-client, moet u ervoor zorgen dat u de volgende instellingen voor client apparaten hebt geconfigureerd:  

- **Hardware-inventaris**: Schakel deze functie in en configureer deze als u hardware-inventaris van Mac-en Windows-client computers wilt verzamelen. Zie [Hardware-inventarisatie uitbreiden](../manage/inventory/extend-hardware-inventory.md)voor meer informatie.  

- **Instellingen voor naleving**: Schakel deze functie in en configureer deze als u instellingen op Mac-en Windows-client computers wilt evalueren en herstellen. Zie [nalevings instellingen plannen en configureren](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)voor meer informatie.  

Zie [client instellingen configureren](configure-client-settings.md)voor meer informatie.  



## <a name="download-the-client-for-macos"></a><a name="bkmk_download"></a>Down load de client voor macOS

1. Down load het macOS client-bestands pakket, [micro soft Endpoint Configuration Manager-MacOS client (64-bits)](https://www.microsoft.com/download/details.aspx?id=100850). Sla **ConfigmgrMacClient. msi** op op een computer waarop Windows wordt uitgevoerd. Dit bestand bevindt zich niet op de Configuration Manager-installatie media.  

2. Voer het installatie programma uit op de Windows-computer. Pak het Mac-client pakket, **Macclient. dmg**, uit naar een map op de lokale schijf. Het standaardpad is `C:\Program Files\Microsoft\System Center Configuration Manager for Mac client`.  

3. Kopieer het bestand **Macclient. dmg** naar een map op de Mac-computer.  

4. Voer op de Mac-computer **Macclient. dmg** uit om de bestanden uit te pakken naar een map op de lokale schijf.  

5. Zorg er in de map voor dat deze de volgende bestanden bevat: 

    - **Ccmsetup**: installeert de Configuration Manager-client op uw Mac-computers met behulp van **CMClient. pak**  

    - **CMDiagnostics**: verzamelt diagnostische gegevens met betrekking tot de Configuration Manager-client op uw Mac-computers  

    - **CMUninstall**: Hiermee wordt de installatie van de client op uw Mac-computers ongedaan gemaakt  

    - **CMAppUtil**: converteert Apple-toepassings pakketten naar een indeling die u als Configuration Manager-toepassing kunt implementeren  

    - **CMEnroll**: het client certificaat voor een Mac-computer aanvragen en installeren, zodat u de Configuration Manager-client vervolgens kunt installeren  



## <a name="enroll-the-mac-client"></a><a name="bkmk_enroll"></a>De Mac-client registreren  

Registreer afzonderlijke clients bij de [Registratie wizard voor Mac-computers](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Gebruik het [CMEnroll-hulp programma](#client-and-certificate-automation-with-cmenroll)om de inschrijving voor veel clients te automatiseren.   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>De client inschrijven met de wizard Mac-computer registratie  

1. Nadat u de-client hebt geïnstalleerd, wordt de wizard computer registratie geopend. Als u de wizard hand matig wilt starten, selecteert u **Inschrijven** via de pagina **Configuration Manager** voor keuren.  

2. Geef op de tweede pagina van de wizard de volgende informatie op:  

   - **Gebruikers naam**: de gebruikers naam kan de volgende notatie hebben:  

     - `domain\name`. Bijvoorbeeld: `contoso\mnorth`  

     - `user@domain`. Bijvoorbeeld: `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  Wanneer u een e-mail adres gebruikt om het veld **gebruikers naam** in te vullen, vult Configuration Manager automatisch het veld **Server naam** in. De standaard naam van de server van het inschrijvings proxy punt en de domein naam van het e-mail adres wordt gebruikt. Als deze namen niet overeenkomen met de naam van de server van het inschrijvings proxy punt, corrigeert u de **Server naam** tijdens de registratie.  

       De gebruikers naam en het bijbehorende wacht woord moeten overeenkomen met een Active Directory gebruikers account met **Lees** -en **Schrijf** machtigingen voor het certificaat sjabloon van de Mac-client.  

   - **Server naam**: de naam van de server van het inschrijvings proxy punt.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Client-en certificaat automatisering met CMEnroll  

Gebruik deze procedure voor het automatiseren van client installatie en het aanvragen en inschrijven van client certificaten met het CMEnroll-hulp programma. Als u het hulp programma wilt uitvoeren, moet u een Active Directory-gebruikers account hebben.

1. Navigeer op de Mac-computer naar de map waar u de inhoud van het **Macclient. dmg** -bestand hebt uitgepakt.  

2. Voer de volgende opdracht in:`sudo ./ccmsetup`  

3. Wacht tot u de boodschap **Installatie voltooid** ziet. Hoewel in het installatie programma een bericht wordt weer gegeven dat u nu opnieuw moet opstarten, start u niet opnieuw op en gaat u verder met de volgende stap.  

4. Typ in de map **Hulpprogram ma's** op de Mac-computer de volgende opdracht:`sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    Nadat de client is geïnstalleerd, wordt de wizard Inschrijving voor Mac-computers geopend waarmee u de Mac-computer kunt inschrijven. Zie [de client inschrijven met de wizard Mac-computer registratie](#bkmk_enroll)voor meer informatie.  

     Voor beeld: als de server van het inschrijvings proxy punt **server02.contoso.com**heet en u **contoso\mnorth** machtigingen voor het certificaat sjabloon van de Mac-client verleent, typt u de volgende opdracht:`sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > Als de gebruikers naam een van de volgende tekens bevat, mislukt de inschrijving `<>"+=,`:. Gebruik een out-of-band-certificaat met een gebruikers naam die deze tekens niet bevat.  
    >  
    > Voor een meer naadloze gebruikers ervaring scripteert u de installatie stappen. Gebruikers hoeven dan alleen hun gebruikers naam en wacht woord op te geven.  

5. Typ het wacht woord voor de Active Directory gebruikers account. Wanneer u deze opdracht invoert, wordt u gevraagd om twee wacht woorden. Het eerste wacht woord is voor de supergebruikers account om de opdracht uit te voeren. De tweede vraag is voor de Active Directory-gebruikersaccount. De vragen zien er identiek uit, zorg er dus voor dat u ze in de juiste volgorde ingeeft.  

6. Wacht tot u de boodschap **Inschrijving geslaagd** ziet.  

7. Om het Inge schreven certificaat te beperken tot Configuration Manager, opent u op de Mac-computer een Terminal venster en brengt u de volgende wijzigingen aan:  

    1. Voer de opdracht in`sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. Kies in het venster **sleutel hanger toegang** in het gedeelte hoofd **ketens** de optie **systeem**. Kies vervolgens in de sectie **categorie** de optie **sleutels**.  

    3. Vouw de sleutels uit om de clientcertificaten weer te geven. Zoek het certificaat met een persoonlijke sleutel die u hebt geïnstalleerd en open de sleutel.  

    4. Klik op het tabblad **Access Control** op **bevestigen voordat u toegang toestaat**.  

    5. Blader naar **/Library/Application Support/micro soft/CCM**, selecteer **CCMClient**en kies vervolgens **toevoegen**.  

    6. Kies **wijzigingen opslaan** en sluit het dialoog venster **toegang tot sleutel hanger** .  

8. Start de Mac-computer opnieuw op.  

Als u wilt controleren of de client installatie is voltooid, opent u het item **Configuration Manager** in **systeem voorkeuren** op de Mac-computer. U kunt de verzameling **alle systemen** ook bijwerken en weer geven in de Configuration Manager-console. Controleer of de Mac-computer wordt weer gegeven in deze verzameling als een beheerde client.  

> [!TIP]  
> Gebruik het **CMDiagnostics** -hulp programma dat is opgenomen in het Mac-client pakket voor hulp bij het oplossen van problemen met de Mac-client. Gebruik het om de volgende diagnostische informatie te verzamelen:  
>   
> - Een lijst met actieve processen  
> - De versie van Mac OS X als besturingssysteem  
> - Mac OS X-fouten rapporten met betrekking tot de Configuration Manager-client, zoals **CCM\*. crash** en **systeem voorkeur. crash**.  
> - Het bestand met de stuk lijst (BOM) bestand en de eigenschappen lijst (. plist) dat is gemaakt door de Configuration Manager-client installatie.  
> - De inhoud van de map **/Library/Application Support/micro soft/CCM/logs**.  
>   
> De gegevens die worden verzameld door CmDiagnostics, worden toegevoegd aan een zip-bestand dat wordt opgeslagen op het bureau blad van de computer en de naam`cmdiag-<hostname>-<datetime>.zip`



## <a name="manage-certificates-external-to-configuration-manager"></a><a name="bkmk_external"></a>Certificaten extern beheren op Configuration Manager

U kunt een certificaat aanvraag en installatie methode onafhankelijk van Configuration Manager gebruiken. Gebruik hetzelfde algemene proces, maar neem de volgende extra stappen: 

- Wanneer u de Configuration Manager-client installeert, gebruikt u de opdracht regel opties **MP** en **subjectnaam** . Voer de volgende opdracht in `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`:. De onderwerpnaam van het certificaat is hoofdletter gevoelig, dus typ de naam precies zoals deze wordt weer gegeven in de details van het certificaat.  

     Voor beeld: de Internet-FQDN van het beheer punt is **server03.contoso.com**. Het Mac-client certificaat heeft de FQDN van **mac12.contoso.com** als algemene naam in het certificaat onderwerp. Gebruik de volgende opdracht:`sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- Als u meer dan één certificaat met dezelfde onderwerpwaarde hebt, geeft u het serie nummer van het certificaat op dat moet worden gebruikt voor de Configuration Manager-client. Gebruik de volgende opdracht: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     Bijvoorbeeld: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Het Mac-client certificaat vernieuwen  

Met deze procedure wordt de SMSID verwijderd. De Configuration Manager-client voor Mac vereist een nieuwe ID voor het gebruik van een nieuw of vernieuwd certificaat.  

> [!IMPORTANT]  
> Nadat u de client SMSID hebt vervangen en u de oude resource in de Configuration Manager-console verwijdert, verwijdert u ook alle opgeslagen client geschiedenis. Bijvoorbeeld geschiedenis van hardware-inventaris voor die client.  


1. Maak en vul een verzameling apparaten in voor de Mac-computers die de computer certificaten moeten vernieuwen.  

2. Start in de werkruimte **Activa en naleving** de wizard **Configuratie-item maken**.  

3. Geef op de pagina **Algemeen** van de wizard de volgende instellingen op:  

    - **Naam**: **Verwijder SMSID voor Mac**  

    - **Type**: **Mac OS X**  

4. Selecteer alle Mac OS X-versies op de pagina **ondersteunde platforms** .  

5. Selecteer op de pagina **Instellingen** de optie **Nieuw**. Geef in het venster **instelling maken** de volgende informatie op:  

    - **Naam**: **Verwijder SMSID voor Mac**  

    - **Instellings type**: **script**  

    - **Gegevens type**: **teken reeks**  

6. Selecteer in het venster **instelling maken** voor **detectie script**de optie **script toevoegen**. Met deze actie wordt een script opgegeven om Mac-computers te detecteren die zijn geconfigureerd met een SMSID.  

7. Voer in het venster **detectie script bewerken** het volgende shell script in:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Kies **OK** om het venster **detectie script bewerken** te sluiten.  

9. Kies in het venster **instelling maken** voor **herstel script (optioneel)** **script toevoegen**. Met deze actie wordt een script opgegeven voor het verwijderen van de SMSID wanneer deze op Mac-computers wordt gevonden.  

10. Voer in het venster **herstel script maken** het volgende shell script in:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Kies **OK** om het venster **herstel script maken** te sluiten.  

12. Kies op de pagina **nalevings regels** de optie **Nieuw**. Geef vervolgens in het venster **regel maken** de volgende informatie op:  

    - **Naam**: **Verwijder SMSID voor Mac**  

    - **Geselecteerde instelling**: Klik op **Bladeren** en selecteer vervolgens het detectie script dat u eerder hebt opgegeven.  

    - In **het volgende veld waarden** : **het domein/standaard paar (com. micro soft. ccmclient, SMSID) bestaat niet**.  

    - Schakel de optie in om **het opgegeven herstel script uit te voeren wanneer deze instelling niet compatibel is**.  

13. Voltooi de wizard.  

14. Maak een configuratie basislijn die dit configuratie-item bevat. Implementeer de basis lijn in de doel verzameling.  

     Zie [configuratie basislijnen maken](../../../compliance/deploy-use/create-configuration-baselines.md)voor meer informatie.  

15. Nadat u een nieuw certificaat op Mac-computers hebt geïnstalleerd waarop de SMSID is verwijderd, voert u de volgende opdracht uit om de client te configureren voor het gebruik van het nieuwe certificaat:  

    ``` Shell
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Zie ook

[Implementatie van clients op Macs voorbereiden](prepare-to-deploy-mac-clients.md)

[Mac-clients onderhouden](../manage/maintain-mac-clients.md)

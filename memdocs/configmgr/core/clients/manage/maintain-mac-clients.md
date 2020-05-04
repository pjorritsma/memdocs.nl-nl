---
title: Mac-clients onderhouden
titleSuffix: Configuration Manager
description: Onderhouds taken voor Configuration Manager Mac-clients.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 520315c4bb740f23a9534e532f75c3bd3ee66a2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710648"
---
# <a name="maintain-mac-clients"></a>Mac-clients onderhouden
*Van toepassing op: Configuration Manager (huidige vertakking)*

Hier vindt u procedures voor het verwijderen van Mac-clients en voor het vernieuwen van de certificaten.

##  <a name="uninstalling-the-mac-client"></a>Uninstalling the Mac client  

1.  Open op een Mac-computer een Terminal venster en navigeer naar de map met **macclient. dmg**.  

2.  Ga naar de map Hulpprogramma's en geef de volgende opdrachtregel in:  

     `./CMUninstall -c`

    > [!NOTE]  
    >  De eigenschap **-c** geeft aan dat de client wordt verwijderd om ook client crash logs en logboek bestanden te verwijderen. U wordt aangeraden Verwar ring te voor komen als u de client later opnieuw installeert.  

3.  Indien nodig moet u het client verificatie certificaat dat Configuration Manager gebruikt, hand matig verwijderen of intrekken. CMUnistall verwijdert of trekt dit certificaat niet in.  

##  <a name="renewing-the-mac-client-certificate"></a>Het certificaat van de Mac-client vernieuwen  
 Gebruik een van de volgende methodes om het certificaat van de Mac-client te vernieuwen:  

-   [Wizard Certificaat vernieuwen](#renew-certificate-wizard)  

-   [Certificaat hand matig vernieuwen](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Wizard Certificaat vernieuwen  

1. Configureer de volgende waarden als *teken reeksen* in het ccmclient. plist-bestand dat bepaalt wanneer de wizard voor het vernieuwen van het certificaat wordt geopend:  

   - **RenewalPeriod1** : geeft, in seconden, de eerste vernieuwings periode waarin gebruikers het certificaat kunnen vernieuwen. De standaardwaarde is 3.888.000 seconden (45 dagen). Configureer geen waarde die kleiner is dan 300, omdat de periode wordt teruggezet naar de standaard instelling. 

   - **RenewalPeriod2** : geeft, in seconden, de tweede vernieuwings periode waarin gebruikers het certificaat kunnen vernieuwen. De standaardwaarde is 259.200 seconden (3 dagen). Als deze waarde is geconfigureerd en groter is dan of gelijk is aan 300 seconden en kleiner is dan of gelijk is aan **RenewalPeriod1**, wordt de waarde gebruikt. Als de waarde voor **RenewalPeriod1** groter is dan 3 dagen, wordt een waarde van 3 dagen gebruikt voor **RenewalPeriod2**.  Als de waarde voor **RenewalPeriod1** kleiner is dan 3 dagen, wordt **RenewalPeriod2** vervolgens ingesteld op dezelfde waarde als **RenewalPeriod1**.  

   - **RenewalReminderInterval1** : Hiermee geeft u, in seconden, de frequentie op waarmee de wizard Certificaat vernieuwen wordt weer gegeven voor gebruikers tijdens de eerste vernieuwings periode. De standaardwaarde is 86.400 seconden (1 dag). Als **RenewalReminderInterval1** groter is dan 300 seconden en kleiner dan de waarde die is geconfigureerd voor **RenewalPeriod1**, dan zal de geconfigureerde waarde worden gebruikt. Anders wordt de standaardwaarde van 1 dag gebruikt.  

   - **RenewalReminderInterval2** : Hiermee geeft u, in seconden, de frequentie op waarmee de wizard Certificaat vernieuwen wordt weer gegeven voor gebruikers tijdens de tweede vernieuwings periode. De standaardwaarde is 28.800 seconden (8 uur). Als de waarde voor **RenewalReminderInterval2** groter is dan 300 seconden, kleiner dan of gelijk aan **RenewalReminderInterval1** is en kleiner dan of gelijk aan **RenewalPeriod2**is, wordt de geconfigureerde waarde gebruikt. Anders wordt een waarde van 8 uur gebruikt.  

     **Voorbeeld:** als de standaardwaarden worden gehandhaafd, wordt de wizard, 45 dagen voordat het certificaat verloopt, elke 24 uur geopend.  Vanaf 3 dagen vóór het verlopen van het certificaat wordt de wizard elke 8 uur geopend.  

     **Voorbeeld:** gebruik de volgende opdrachtregel, of een script, om de eerste vernieuwingsperiode op 20 dagen in te stellen.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2. Wanneer de wizard voor het vernieuwen van het certificaat wordt geopend, zijn de velden **gebruikers naam** en **Server naam** doorgaans vooraf ingevuld en kan de gebruiker alleen een wacht woord invoeren om het certificaat te vernieuwen.  

   > [!NOTE]  
   >  Als de wizard niet wordt geopend, of als u de wizard onopzettelijk sluit, klik dan op **Vernieuwen** op de **Configuration Manager** -voorkeurspagina om de wizard te openen.  

###  <a name="renew-certificate-manually"></a>Certificaat hand matig vernieuwen  
 De geldigheidsperiode voor het Mac-clientcertificaat is doorgaans 1 jaar. Configuration Manager het gebruikers certificaat dat tijdens de registratie wordt aangevraagd, wordt niet automatisch vernieuwd. u moet de volgende procedure gebruiken om het certificaat hand matig te vernieuwen.  

> [!IMPORTANT]  
>  Als het certificaat verloopt, moet u de Mac-client verwijderen, opnieuw installeren en vervolgens opnieuw inschrijven.  

 Deze procedure verwijdert de SMSID, die vereist is om een nieuw certificaat aan te vragen voor dezelfde Mac-computer. Wanneer u de client-SMSID verwijdert en vervangt, worden alle opgeslagen client geschiedenis, zoals inventarisatie, verwijderd nadat u de client uit de Configuration Manager-console hebt verwijderd.  

1.  Maak en vul een verzameling apparaten in voor de Mac-computers die de gebruikers certificaten moeten vernieuwen.  

    > [!WARNING]  
    >  Configuration Manager controleert de geldigheids periode van het certificaat dat voor Mac-computers is inge schreven. U moet dit onafhankelijk van Configuration Manager controleren om de Mac-computers te identificeren die aan deze verzameling moeten worden toegevoegd.  

2.  Start in de werkruimte **Activa en naleving** de wizard **Configuratie-item maken**.  

3.  Geef op de pagina **Algemeen** de volgende gegevens op:  

    -   **Naam:Verwijder SMSID voor Mac**  

    -   **Type:Mac OS X**  

4.  Controleer op de pagina **ondersteunde platforms** of alle Mac OS X-versies zijn geselecteerd.  

5.  Kies op de pagina **instellingen** de optie **Nieuw** en geef vervolgens in het dialoog venster **instelling maken** de volgende gegevens op:  

    -   **Naam:Verwijder SMSID voor Mac**  

    -   **Instellingstype:script**  

    -   **Gegevenstype:tekenreeks**  

6.  Klik in het dialoog venster **instelling maken** voor **detectie script**op **script toevoegen** om een script op te geven dat Mac-computers detecteert waarop een SMSID is geconfigureerd.  

7.  Geef in het dialoogvenster **Detectiescript bewerken** het volgende Shellscript in:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Kies **OK** om het dialoog venster **detectie script bewerken** te sluiten.  

9. Klik in het dialoog venster **instelling maken** voor **herstel script (optioneel)** op **script toevoegen** om een script op te geven dat de SMSID verwijdert wanneer deze op Mac-computers wordt gevonden.  

10. Geef in het dialoogvenster **Herstelscript maken** het volgende Shellscript in:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Kies **OK** om het dialoog venster **herstel script maken** te sluiten.  

12. Klik, op de pagina **Compliantieregels** van de wizard, op **Nieuw**en geef dan in het dialoogvenster **Regel maken** de volgende informatie:  

    -   **Naam:Verwijder SMSID voor Mac**  

    -   **Geselecteerde instelling:** Kies **Bladeren** en selecteer vervolgens het detectie script dat u eerder hebt opgegeven.  

    -   Typ in **het volgende waarden** veld de waarde **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Schakel de optie **Het opgegeven herstelscript uitvoeren wanneer deze instelling niet compatibel is**.  

13. Voer de wizard Configuratie-item maken uit.  

14. Maak een configuratie basislijn die het configuratie-item bevat dat u zojuist hebt gemaakt en implementeert in de verzameling apparaten die u in stap 1 hebt gemaakt.  

     Zie [configuratie basislijnen maken](../../../compliance/deploy-use/create-configuration-baselines.md) en [configuratie basislijnen implementeren](../../../compliance/deploy-use/deploy-configuration-baselines.md)voor meer informatie over het maken en implementeren van configuratie basislijnen.  

15. Voer op Mac-computers waarvan de SMSID is verwijderd, de volgende opdracht uit om een nieuw certificaat te installeren.  

    ``` Shell
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Geef, wanneer dit wordt gevraagd, het wachtwoord voor de supergebruikersaccount om de opdracht uit te voeren en dan het wachtwoord voor de Active Directory-gebruikersaccount.  

16. Om het Inge schreven certificaat te beperken tot Configuration Manager, opent u op de Mac-computer een Terminal venster en brengt u de volgende wijzigingen aan:  

    a.  Voer de opdracht in`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`

    b.  Kies in het dialoog venster **toegang tot sleutel hanger** in het gedeelte hoofd **ketens** de optie **systeem**en kies vervolgens in de sectie **categorie** de optie **sleutels**.  

    c.  Vouw de sleutels uit om de clientcertificaten weer te geven. Wanneer u het certificaat met een persoonlijke sleutel hebt geïdentificeerd dat u zojuist hebt geïnstalleerd, dubbelklikt u op de sleutel.  

    d.  Klik op het tabblad **Access Control** op **bevestigen voordat u toegang toestaat**.  

    e.  Blader naar **/Library/Application Support/micro soft/CCM**, selecteer **CCMClient**en kies vervolgens **toevoegen**.  

    f.  Kies **wijzigingen opslaan** en sluit het dialoog venster **toegang tot sleutel hanger** .  

17. Start de Mac-computer opnieuw op.  


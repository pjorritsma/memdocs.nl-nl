---
title: De pc-clientsoftware installeren
description: Gebruik deze handleiding om uw Windows-pc's te laten beheren door de Microsoft Intune-clientsoftware.
keywords: ''
author: ErikjeMS
ms.author: erikje
ms.date: 07/13/2017
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 99dcf916-d80f-42c5-863b-a4595e1ec67a
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: d9e6806e8d755163d5ae1701ca49ad2daeff464f
ms.sourcegitcommit: 2ee50bfc416182362ae0b8070b096e1cc792bf68
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865870"
---
# <a name="install-the-intune-software-client-on-windows-pcs"></a>De Intune-softwareclient installeren op Windows-pc's

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> U kunt Microsoft Intune gebruiken voor het beheren van Windows-pc's [als mobiele apparaten met Mobile Device Management (MDM)](../enrollment/windows-enroll.md) of als computers met de Intune-softwareclient, zoals hieronder beschreven. Microsoft adviseert klanten echter om indien mogelijk [de MDM-beheeroplossing te gebruiken](../enrollment/windows-enroll.md). Raadpleeg [Beheer van Windows-pc's als computers of mobiele apparaten vergelijken](pc-management-comparison.md) voor meer informatie 


Windows-pc's kunnen worden geregistreerd door de Intune-clientsoftware te installeren. De Intune-clientsoftware kan via de volgende methoden worden geïnstalleerd:

- Handmatige installatie, installatie via groepsbeleid of installatie opgenomen in een schijfinstallatiekopie door de IT-beheerder

- Handmatige installatie van de softwareclient door eindgebruikers

De Intune-clientsoftware bevat de minimale software die nodig is om de pc bij Intune-beheer in te schrijven. Nadat een pc is ingeschreven, downloadt de Intune-clientsoftware de volledige clientsoftware die nodig is om de pc te beheren.

Deze reeks downloads beperkt de impact voor de bandbreedte van het netwerk en minimaliseert de tijd die nodig is om de oorspronkelijke registratie van de pc bij Intune uit te voeren. Ook wordt er op die manier voor gezorgd dat zich op de client de nieuwste versie van de software bevindt nadat de tweede download is voltooid.

Een Intune-licentie staat de installatie van de Intune-clientsoftware op maximaal vijf pc's toe.

## <a name="download-the-intune-client-software"></a>De Intune-clientsoftware downloaden

Voor alle methoden, behalve die waarbij gebruikers de Intune-clientsoftware zelf installeren, moeten IT-beheerders eerst de software downloaden zodat deze vervolgens kan worden geïmplementeerd voor eindgebruikers.

1. Klik in de [Microsoft Intune-beheerconsole](https://manage.microsoft.com/) op **Administrator** &gt; **Clientsoftware downloaden**.

   ![De Intune-pc-client downloaden](./media/install-the-windows-pc-client-with-microsoft-intune/pc-sa-client-download.png)

2. Klik op de pagina **Clientsoftware downloaden** op **Clientsoftware downloaden**. Sla het pakket **Microsoft_Intune_Setup.zip** met de software vervolgens op een beveiligde locatie op uw netwerk op.

   Het installatiepakket voor de Intune-clientsoftware bevat unieke en specifieke informatie over uw account, die beschikbaar is via een ingesloten certificaat. Als niet-gemachtigde gebruikers toegang krijgen tot het installatiepakket, kunnen ze pc’s inschrijven bij het account van het certificaat dat is ingesloten in het pakket en krijgen ze mogelijk toegang tot bedrijfsbronnen.

3. Pak de inhoud van het installatiepakket uit naar een beveiligde locatie in het netwerk.

    > [!IMPORTANT]
    > Hernoem of verwijder het uitgepakte bestand **ACCOUNTCERT** niet, anders mislukt de installatie van de clientsoftware.

## <a name="deploy-the-client-software-manually"></a>De clientsoftware handmatig implementeren

Ga op de computer(s) waarop de clientsoftware moet worden geïnstalleerd naar de map met de installatiebestanden van de clientsoftware. Voer vervolgens **Microsoft_Intune_Setup.exe** uit om de clientsoftware te installeren.

> [!NOTE]
> De status van de installatie wordt weergegeven wanneer u met de muisaanwijzer over het pictogram in het systeemvak van de client-pc beweegt.

## <a name="deploy-the-client-software-by-using-group-policy"></a>De clientsoftware implementeren met Groepsbeleid

1. Voer onderstaande opdracht uit in de map met de bestanden **Microsoft_Intune_Setup.exe** en **MicrosoftIntune.accountcert** om de op Windows Installer gebaseerde installatieprogramma's voor 32-bits en 64-bits computers te extraheren:

    ```cmd
    Microsoft_Intune_Setup.exe/Extract <destination folder>
    ```

2. Kopieer de bestanden **Microsoft_Intune_x86.msi**, **Microsoft_Intune_x64.msi** en **MicrosoftIntune.accountcert** naar een netwerklocatie die toegankelijk is voor alle computers waarop de clientsoftware moet worden geïnstalleerd.

    > [!IMPORTANT]
    > Scheid of hernoem de bestanden niet om te voorkomen de installatie van clientsoftware mislukt.

3. Gebruik Groepsbeleid om de software te implementeren op de computers in uw netwerk.

    Zie [Groepsbeleid voor beginners](https://technet.microsoft.com/library/hh147307.aspx) voor meer informatie over het gebruik van groepsbeleid om software automatisch te implementeren.

## <a name="deploy-the-client-software-as-part-of-an-image"></a>De clientsoftware als onderdeel van een installatiekopie implementeren
U kunt de Intune-clientsoftware op computers implementeren met een installatiekopie van het besturingssysteem door de volgende procedure als richtlijn te hanteren:

1. Kopieer de clientinstallatiebestanden **Microsoft_Intune_Setup.exe** en **MicrosoftIntune.accountcert** naar de map **%Systemdrive%\Temp\Microsoft_Intune_Setup** op de referentiecomputer.

2. Maak de registervermelding **WindowsIntuneEnrollPending** door de volgende opdracht toe te voegen aan het script **SetupComplete.cmd** :

    ```cmd
    %windir%\system32\reg.exe add HKEY_LOCAL_MACHINE\Software\Microsoft\Onlinemanagement\Deployment /v
    WindowsIntuneEnrollPending /t REG_DWORD /d 1
    ```

3. Voeg de volgende opdracht toe aan **setupcomplete.cmd** om het inschrijvingspakket uit te voeren met het opdrachtregelargument /PrepareEnroll:

    ```cmd
    %systemdrive%\temp\Microsoft_Intune_Setup\Microsoft_Intune_Setup.exe /PrepareEnroll
    ```

    > [!TIP]
    > Het script **SetupComplete.cmd** staat Windows Setup toe om wijzigingen aan te brengen in het systeem voordat een gebruiker zich aanmeldt. Het opdrachtregelargument **/PrepareEnroll** bereidt een doelcomputer voor om automatisch te worden ingeschreven in Intune nadat Windows Setup is voltooid.

4. Plaats **SetupComplete.cmd** in de map **%Windir%\Setup\Scripts** op de referentiecomputer.

5. Leg een installatiekopie van de referentiecomputer vast en implementeer deze vervolgens op de doelcomputers.

    Wanneer de doelcomputer opnieuw wordt opgestart om Windows Setup te voltooien, wordt de registervermelding **WindowsIntuneEnrollPending** gemaakt. Het inschrijvingspakket controleert of de computer is ingeschreven. Als de computer is ingeschreven, is er geen verdere actie nodig. Als de computer niet is ingeschreven, maakt het inschrijvingspakket een automatische inschrijvingstaak voor Microsoft Intune.

    Wanneer de automatische inschrijvingstaak wordt uitgevoerd op het volgende geplande tijdstip, wordt gecontroleerd of de registerwaarde **WindowsIntuneEnrollPending** bestaat en wordt geprobeerd om de doel-pc in te schrijven bij Intune. Als de inschrijving om een of andere reden mislukt, wordt een nieuwe poging ondernomen de volgende keer dat de taak wordt uitgevoerd. De nieuwe pogingen worden een maand lang uitgevoerd.

    De automatische inschrijvingstaak voor Intune, de registerwaarde **WindowsIntuneEnrollPending** en het accountcertificaat worden van de doelcomputer verwijderd wanneer de inschrijving is geslaagd of, als dit eerder is, na één maand.

## <a name="instruct-users-to-self-enroll"></a>Registratie door de gebruikers zelf

Gebruikers kunnen de Intune-clientsoftware installeren door naar [de website van de bedrijfsportal](https://portal.manage.microsoft.com) te gaan. De exacte informatie die gebruikers in de webportal zien, verschilt afhankelijk van de MDM-instantie voor uw account en het OS-platform/versie van de pc van de gebruiker.

Als er geen Intune-licentie is toegewezen aan gebruikers of als de MDM-instantie van de organisatie niet op Intune is ingesteld, zien gebruikers geen inschrijvingsopties.

Als er wel een Intune-licentie is toegewezen aan gebruikers en de MDM-instantie van de organisatie wel op Intune is ingesteld:

- Gebruikers van Windows 7- of Windows 8-pc’s zien ALLEEN de optie om zich in te schrijven voor Intune door de pc-clientsoftware te downloaden en installeren die uniek is voor hun organisatie.

- Gebruikers van Windows 10- of Windows 8.1-pc’s zien twee inschrijvingsopties:

  - **Pc inschrijven als mobiel apparaat**: Als gebruikers de knop **Meer informatie over inschrijven** kiezen, worden ze naar instructies geleid voor het inschrijven van hun pc als mobiel apparaat. Deze knop wordt prominent weergegeven, omdat MDM-inschrijving als de standaard inschrijvingsoptie wordt beschouwd die de voorkeur heeft. De MDM-optie is echter niet van toepassing op dit onderwerp, dat alleen de installatie van de clientsoftware dekt.
  - **Pc inschrijven met behulp van de Intune-clientsoftware**: U moet uw gebruikers vertellen dat ze de link **Klik hier om het te downloaden** moeten selecteren, zodat ze door de installatie van de clientsoftware worden geleid.

De volgende tabel geeft een overzicht van de opties.

  ![Standaard inschrijvingsopties per platform](./media/install-the-windows-pc-client-with-microsoft-intune/default-enrollment-options-table.png)

De volgende schermafbeeldingen tonen wat gebruikers zien wanneer ze hun apparaat inschrijven met behulp van de clientsoftware.

Gebruikers worden eerst gevraagd hun apparaat te identificeren of in te schrijven.

  ![apparaat identificeren of inschrijven](./media/install-the-windows-pc-client-with-microsoft-intune/identify-device-or-enroll.png)

Als u wilt dat uw gebruikers de pc-clientsoftware installeren, moet u hen vertellen dat ze de link **Klik hier om het te downloaden** moeten selecteren om de pc-clientsoftware te downloaden en door het installatieproces te worden geleid. De knop **Meer informatie over inschrijven** leidt gebruikers naar documentatie over MDM-inschrijving, wat niet relevant is voor deze clientsoftware-instructies.

  ![link Klik hier om het te downloaden kiezen](./media/install-the-windows-pc-client-with-microsoft-intune/enroll-your-windows-device.png)

Wanneer gebruikers op de link klikken, zien ze de knop **Software downloaden**, die ze moeten selecteren om de installatie van de pc-clientsoftware te starten.

  ![knop Software downloaden kiezen](./media/install-the-windows-pc-client-with-microsoft-intune/download-pc-client-software.png)

Gebruikers worden vervolgens gevraagd zich aan te melden met hun bedrijfsreferenties.

  ![Aanmelden met uw referenties](./media/install-the-windows-pc-client-with-microsoft-intune/sign-in-to-intune.png)

Gebruikers worden naar de welkomstpagina voor de installatie geleid.

  ![Welkomstpagina voor installatie van pc-clientsoftware](./media/install-the-windows-pc-client-with-microsoft-intune/welcome-to-pc-agent-install-wizard.png)

Gebruikers kiezen **Volgende**, waarna de installatie wordt gestart.

  ![Welkomstpagina voor installatie van pc-clientsoftware](./media/install-the-windows-pc-client-with-microsoft-intune/welcome-to-pc-agent-install-wizard.png)

Wanneer de installatie is voltooid, kiezen gebruikers **Voltooien**.

  ![De installatie van de pc-clientsoftware voltooien](./media/install-the-windows-pc-client-with-microsoft-intune/completed-the-setup-wizard.png)

Als gebruikers hun pc als mobiel apparaat proberen in te schrijven nadat ze het al hebben ingeschreven met behulp van de Intune-pc-clientsoftware, zien ze het volgende foutscherm.

  ![Weergegeven scherm als pc al is ingeschreven](./media/install-the-windows-pc-client-with-microsoft-intune/page-shown-if-pc-already-enrolled.png)

## <a name="monitor-and-validate-successful-client-deployment"></a>Geslaagde clientimplementatie controleren en valideren
Gebruik een van de volgende procedures om de clientimplementatie te controleren en te valideren.

### <a name="to-verify-the-installation-of-the-client-software-from-the-microsoft-intune-administrator-console"></a>De installatie van de clientsoftware vanaf de Microsoft Intune-beheerconsole verifiëren

1. Klik in de [Microsoft Intune-beheerconsole](https://manage.microsoft.com/) op **Groepen** &gt; **Alle apparaten** &gt; **Alle computers**.

2. Zoek in de lijst naar de computers die met Intune communiceren, of zoek naar een specifieke beheerde computer door de naam van de computer, of een deel van de naam, te typen in het vak **Apparaten zoeken**.

3. Controleer de status van de computer in het onderste deelvenster van de console. Los eventuele fouten op.

### <a name="to-create-a-computer-inventory-report-to-display-all-enrolled-computers"></a>Een computerinventarisrapport maken om alle ingeschreven computers weer te geven

1. Klik in de [Microsoft Intune-beheerconsole](https://manage.microsoft.com/) op **Rapporten** &gt; **Computerinventarisatierapporten**.

2. Behoud op de pagina **Nieuw rapport maken** de standaardwaarde voor alle velden (tenzij u filters wilt toepassen) en klik vervolgens op **Rapport weergeven**.

3. De pagina **Computerinventarisrapport** wordt in een nieuw venster geopend met alle computers die zijn ingeschreven bij Intune.

    > [!TIP]
    > Klik op een kolomkop in het rapport om de lijst te sorteren op de inhoud van die kolom.

## <a name="uninstall-the-windows-client-software"></a>De Windows-clientsoftware verwijderen

Er zijn twee manieren om de Windows-clientsoftware uit te schrijven:

- Via de Intune-beheerconsole (aanbevolen methode)
- Via een opdrachtprompt op de client

### <a name="unenroll-by-using-the-intune-admin-console"></a>Uitschrijven via de Intune-beheerconsole

Als u de softwareclient wilt uitschrijven via de Intune-beheerconsole, gaat u naar **Groepen** > **Alle computers** > **Apparaten**. Klik met de rechtermuisknop op de client en selecteer **Buiten gebruik stellen/wissen**.

### <a name="unenroll-by-using-a-command-prompt-on-the-client"></a>Uitschrijven via een opdrachtprompt op de client

Voer vanaf een opdrachtprompt met verhoogde bevoegdheid een van de volgende opdrachten uit.

**Methode 1**:

```cmd
"C:\Program Files\Microsoft\OnlineManagement\Common\ProvisioningUtil.exe" /UninstallAgents /MicrosoftIntune
```

**Methode 2** onthoud dat al deze agents zijn geïnstalleerd op elke SKU van Windows:

```cmd
wmic product where name="Microsoft Endpoint Protection Management Components" call uninstall
wmic product where name="Microsoft Intune Notification Service" call uninstall
wmic product where name="System Center 2012 - Operations Manager Agent" call uninstall
wmic product where name="Microsoft Online Management Policy Agent" call uninstall
wmic product where name="Microsoft Policy Platform" call uninstall
wmic product where name="Microsoft Security Client" call uninstall
wmic product where name="Microsoft Online Management Client" call uninstall
wmic product where name="Microsoft Online Management Client Service" call uninstall
wmic product where name="Microsoft Easy Assist v2" call uninstall
wmic product where name="Microsoft Intune Monitoring Agent" call uninstall
wmic product where name="Windows Intune Endpoint Protection Agent" call uninstall
wmic product where name="Windows Firewall Configuration Provider" call uninstall
wmic product where name="Microsoft Intune Center" call uninstall
wmic product where name="Microsoft Online Management Update Manager" call uninstall
wmic product where name="Microsoft Online Management Agent Installer" call uninstall
wmic product where name="Microsoft Intune" call uninstall
wmic product where name="Windows Endpoint Protection Management Components" call uninstall
wmic product where name="Windows Intune Notification Service" call uninstall
wmic product where name="System Center 2012 - Operations Manager Agent" call uninstall
wmic product where name="Windows Online Management Policy Agent" call uninstall
wmic product where name="Windows Policy Platform" call uninstall
wmic product where name="Windows Security Client" call uninstall
wmic product where name="Windows Online Management Client" call uninstall
wmic product where name="Windows Online Management Client Service" call uninstall
wmic product where name="Windows Easy Assist v2" call uninstall
wmic product where name="Windows Intune Monitoring Agent" call uninstall
wmic product where name="Windows Intune Endpoint Protection Agent" call uninstall
wmic product where name="Windows Firewall Configuration Provider" call uninstall
wmic product where name="Windows Intune Center" call uninstall
wmic product where name="Windows Online Management Update Manager" call uninstall
wmic product where name="Windows Online Management Agent Installer" call uninstall
wmic product where name="Windows Intune" call uninstall
```

> [!TIP]
> Na de uitschrijving blijft er een verouderde record voor de betrokken client achter op de server. Het uitschrijven is een asynchroon proces dat voor negen agents moet worden uitgevoerd, en kan dus tot wel 30 minuten duren.

### <a name="check-the-unenrollment-status"></a>Status van de uitschrijving controleren

Ga naar "%ProgramFiles%\Microsoft\OnlineManagement" en controleer of alleen de volgende mappen worden weergegeven aan de linkerkant:

- AgentInstaller
- Logs
- Updates
- Common

### <a name="remove-the-onlinemanagement-folder"></a>De map OnlineManagement verwijderen

Tijdens het uitschrijvingsproces wordt de map OnlineManagement niet verwijderd. Wacht na de uitschrijving 30 minuten en voer vervolgens deze opdracht uit. Als u deze opdracht te vroeg uitvoert, krijgt de verwijdering mogelijk een onbekende status. Als u de map wilt verwijderen, opent u een opdrachtprompt met verhoogde bevoegdheid en voert u de volgende opdracht uit:

```cmd
rd /s /q %ProgramFiles%\Microsoft\OnlineManagement
```

## <a name="next-steps"></a>Volgende stappen
[Algemene beheertaken voor Windows-pc's met de Intune-softwareclient](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)

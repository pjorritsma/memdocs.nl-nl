---
title: UNIX/Linux-clients implementeren
titleSuffix: Configuration Manager
description: Meer informatie over het implementeren van een-client op een UNIX-of Linux-server in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9e8e40a6bdfa129a03e6042985e4956ffb21b5c
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906323"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Clients implementeren op UNIX-en Linux-servers in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> Vanaf versie 1902 biedt Configuration Manager geen ondersteuning voor Linux-of UNIX-clients. 
> 
> Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.


Voordat u een Linux-of UNIX-server met Configuration Manager kunt beheren, moet u de Configuration Manager-client voor Linux en UNIX installeren op elke Linux-of UNIX-server. U kunt de installatie van de client handmatig op elke computer uitvoeren of een shell-script gebruiken waarmee de client op afstand wordt geïnstalleerd. Configuration Manager biedt geen ondersteuning voor het gebruik van client push installatie voor Linux-of UNIX-servers. U kunt eventueel een runbook voor System Center Orchestrator configureren om de installatie van de client op de Linux-of UNIX-server te automatiseren.  

 Welke installatiemethode u ook gebruikt, het installatieproces vereist het gebruik van een script met de naam **install** om het installatieproces te beheren. Dit script is opgenomen in de download voor de client voor Linux en UNIX.  

 Het installatie script voor de Configuration Manager-client voor Linux en UNIX ondersteunt opdracht regel eigenschappen. Bepaalde opdracht regel eigenschappen zijn vereist, terwijl andere optioneel zijn. Als u bijvoorbeeld de client installeert, moet u een beheerpunt opgeven via de site die door de Linux- of UNIX-server wordt gebruikt voor het eerste contact met de site. Zie [opdracht regel eigenschappen voor het installeren van de client op Linux-en UNIX-servers](#BKMK_CmdLineInstallLnUClient)voor de volledige lijst met opdracht regel eigenschappen.  

 Nadat u de client hebt geïnstalleerd, geeft u de client instellingen op in de Configuration Manager-console om de client agent op dezelfde manier te configureren als Windows-clients. Zie  [Clientinstellingen voor Linux- en UNIX-servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU)voor meer informatie.  

##  <a name="about-client-installation-packages-and-the-universal-agent"></a><a name="BKMK_AboutInstallPackages"></a>Over client installatie pakketten en de universele agent  
 Als u de client voor Linux en UNIX op een bepaald platform wilt installeren, moet u het desbetreffende clientinstallatiepakket gebruiken voor de computer waarop u de client installeert. Elke clientdownload uit het [Microsoft Downloadcentrum](https://www.microsoft.com/download/details.aspx?id=47719)bevat de betreffende clientinstallatiepakketten. Naast de clientinstallatiepakketten bevat de clientdownload het **installatie** script waarmee de installatie van de client op elke computer wordt beheerd.  

 Wanneer u een client installeert, kunt u hetzelfde proces en de opdracht regel eigenschappen gebruiken, ongeacht het client installatie pakket dat u gebruikt.  

 Zie [Linux-en UNIX-servers](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers)voor informatie over de besturings systemen, platformen en client installatie pakketten die door elke versie van de Configuration Manager-client voor Linux en UNIX worden ondersteund.  

##  <a name="install-the-client-on-linux-and-unix-servers"></a><a name="BKMK_InstallLnUClient"></a>De-client installeren op Linux-en UNIX-servers  
 Als u de client voor Linux en UNIX wilt installeren, voert u op elke Linux- of UNIX-computer een script uit. Het script heeft de naam **install** en ondersteunt opdracht regel eigenschappen die het installatie gedrag wijzigen en verwijzen naar het client installatie pakket. Het installatiescript en clientinstallatiepakket moeten zich op de client bevinden. Het client installatie pakket bevat de Configuration Manager-client bestanden voor een specifiek Linux-of UNIX-besturings systeem en-platform.
Elk client installatie pakket bevat alle benodigde bestanden om de client installatie te volt ooien, in tegens telling tot Windows-computers, downloadt geen aanvullende bestanden van een beheer punt of andere bron locatie.  

 Nadat u de Configuration Manager-client voor Linux en UNIX hebt geïnstalleerd, hoeft u de computer niet opnieuw op te starten. Zodra de software-installatie is voltooid, is de client operationeel. Als u de computer opnieuw opstart, wordt de Configuration Manager-client automatisch opnieuw opgestart.  

 De geïnstalleerde client wordt uitgevoerd met hoofdreferenties. Hoofd referenties zijn vereist om de hardware-inventaris te verzamelen en software-implementaties uit te voeren.  

 Gebruik de volgende opdracht indeling:  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install`is de naam van het script bestand waarmee de client voor Linux en UNIX wordt geïnstalleerd. Dit bestand wordt geleverd bij de clientsoftware.  

-   `-mp <computer>`Hiermee geeft u het initiële beheer punt op dat door de client wordt gebruikt. Voorbeeld: `smsmp.contoso.com`  

-   `-sitecode <site code>`Hiermee geeft u de site code op waaraan de client is toegewezen. Voorbeeld: `S01`  

-   `<property #1> <property #2>`Hiermee geeft u de opdracht regel eigenschappen moet worden gebruikt met het installatie script.  

    > [!NOTE]  
    >  Zie [opdracht regel eigenschappen voor het installeren van de client op Linux-en UNIX-servers](#BKMK_CmdLineInstallLnUClient)voor meer informatie.  

-   **clientinstallatiepakket** is de naam van het TAR-clientinstallatiepakket voor het besturingssysteem, de versie en de CPU-architectuur van deze computer. Het TAR-bestand voor de clientinstallatie moet als laatste worden opgegeven. Voorbeeld: `ccm-Universal-x64.<build>.tar`  

###  <a name="to-install-the-configuration-manager-client-on-linux-and-unix-servers"></a><a name="BKMK_ToInstallLnUClinent"></a>De Configuration Manager-client installeren op Linux-en UNIX-servers  

1.  Op een Windows-computer: [download het betreffende clientbestand voor de Linux- of UNIX-server](https://www.microsoft.com/download/details.aspx?id=47719) die u wilt beheren.  

2.  Voer het zelfuitpakkende .exe-bestand uit op de Windows-computer om het installatiescript en het .tar-bestand voor de clientinstallatie uit te pakken.  

3.  Kopieer het **installatie** script en het .tar-bestand naar een map op de server die u wilt beheren.  

4.  Voer op de UNIX-of Linux-server de volgende opdracht uit om het script uit te voeren als een programma:`chmod +x install`  

    > [!IMPORTANT]  
    >  U moet hoofdreferenties gebruiken om de client te installeren.  

5.  Voer vervolgens de volgende opdracht uit om de Configuration Manager-client te installeren:`./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     Wanneer u deze opdracht opgeeft, gebruikt u aanvullende opdrachtregeleigenschappen die u nodig hebt. Zie [opdracht regel eigenschappen voor het installeren van de client op Linux-en UNIX-servers](#BKMK_CmdLineInstallLnUClient) voor de lijst met opdracht regel eigenschappen.  

6.  Nadat het script is uitgevoerd, valideert u de installatie door het bestand **/var/opt/microsoft/scxcm.log** te controleren. Daarnaast kunt u controleren of de client is geïnstalleerd en communiceert met de site door Details voor de client te bekijken in het knoop punt **apparaten** van de werk ruimte **activa en naleving** in de Configuration Manager-console.  

###  <a name="command-line-properties-for-installing-the-client-on-linux-and-unix-servers"></a><a name="BKMK_CmdLineInstallLnUClient"></a>Opdracht regel eigenschappen voor het installeren van de client op Linux-en UNIX-servers  
 De volgende eigenschappen zijn beschikbaar om het gedrag van het installatie script te wijzigen:  

> [!NOTE]  
>  Gebruik de eigenschap `-h` om deze lijst met ondersteunde eigenschappen weer te geven.  

-   `-mp <server FQDN>`  

     Vereist. Hiermee geeft u met FQDN-naam de beheer punt server op die door de client wordt gebruikt als een eerste contact punt.  

    > [!IMPORTANT]  
    >  Met deze eigenschap geeft u niet het beheer punt op waaraan de client na de installatie wordt toegewezen.  

    > [!NOTE]  
    >  Wanneer u de `-mp` eigenschap gebruikt om een beheer punt op te geven dat is geconfigureerd om alleen https-client verbindingen te accepteren, moet u ook de `-UsePKICert` eigenschap gebruiken.  

-   `-sitecode <sitecode>`  

     Vereist. Hiermee geeft u de Configuration Manager primaire site waaraan de Configuration Manager-client moet worden toegewezen. Voorbeeld: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     Optioneel. Hiermee geeft u met FQDN-naam de server van het terugvalstatuspunt op dat door de client wordt gebruikt om statusberichten te verzenden. Zie [bepalen of u een terugval status punt nodig hebt](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)voor meer informatie.  

-   `-dir <directory>`  

     Optioneel. Hiermee geeft u een alternatieve locatie op voor de installatie van de Configuration Manager-client bestanden. Standaard wordt de client geïnstalleerd op de volgende locatie:`/opt/microsoft`  

-   `-nostart`  

     Optioneel. Hiermee voor komt u dat de Configuration Manager-client service, **ccmexec. bin**, automatisch wordt gestart nadat de client installatie is voltooid.  

     Nadat de client is geïnstalleerd, moet u de clientservice handmatig starten.  

     Standaard wordt de clientservice gestart nadat de clientinstallatie is voltooid en telkens wanneer de computer opnieuw wordt opgestart.  

-   `-clean`  

     Optioneel. Hiermee geeft u aan dat alle clientbestanden en -gegevens van een eerder geïnstalleerde client voor Linux en UNIX moeten worden verwijderd voordat de nieuwe installatie wordt gestart. Met deze actie worden de data base en het certificaat archief van de client verwijderd.  

-   `-keepdb`  

     Optioneel. Hiermee geeft u op dat de lokale client database wordt bewaard en opnieuw wordt gebruikt wanneer u een client opnieuw installeert. Standaard wordt deze database verwijderd wanneer u een client opnieuw installeert.  

-   `-UsePKICert <parameter>`  

     Optioneel. Hiermee geeft u het volledige pad naar en de bestandsnaam van een X.509 PKI-certificaat in de PKCS#12-notatie (Public Key Certificate Standard) op. Dit certificaat wordt gebruikt voor clientverificatie. Als er tijdens de installatie geen certificaat is opgegeven en u een certificaat moet toevoegen of wijzigen, gebruikt u het hulpprogramma **certutil** . Zie [certificaten beheren op de client voor Linux en UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts)voor meer informatie.  

     Wanneer u gebruikt `-UsePKICert` , moet u ook het wacht woord opgeven dat is gekoppeld aan het PKCS # 12-bestand met behulp van de `-certpw` opdracht regel parameter.  

     Als u deze eigenschap niet gebruikt om een PKI-certificaat op te geven, gebruikt de client een zelfondertekend certificaat en zijn alle communicatie naar site systemen via HTTP.  

     Als u een ongeldig certificaat opgeeft op de opdrachtregel voor het installeren van de client, worden er geen fouten geretourneerd. Certificaat validatie vindt plaats nadat de client is geïnstalleerd. Wanneer de client wordt gestart, worden de certificaten gevalideerd met het beheer punt. Als een certificaat niet kan worden gevalideerd, wordt het volgende bericht weer gegeven in **scxcm. log**: **het valideren van het certificaat voor het beheer punt is mislukt**. De standaardlocatie van het logboek is  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > U moet deze eigenschap opgeven wanneer u een client installeert en de `-mp` eigenschap gebruiken om een beheer punt op te geven dat is geconfigureerd om alleen https-client verbindingen te accepteren.  

     Voorbeeld: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     Optioneel. Hiermee geeft u het wacht woord op dat is gekoppeld aan het PKCS # 12-bestand dat u hebt opgegeven met behulp van de `-UsePKICert` eigenschap.  

     Voorbeeld: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     Optioneel. Hiermee geeft u op dat een client de certificaatintrekkingslijst (CRL) niet moet controleren wanneer deze via HTTPS communiceert met behulp van een PKI-certificaat. Als deze optie niet is opgegeven, controleert de client de CRL voordat er een HTTPS-verbinding wordt gemaakt door gebruik te maken van PKI-certificaten. Zie 'Planning voor PKI-certificaatintrekking' voor meer informatie over de CRL-controle voor clients.  

     Voorbeeld: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     Optioneel. Hiermee geeft u het volledige pad en de bestands naam op voor de Configuration Manager vertrouwde basis sleutel. De Configuration Manager vertrouwde basis sleutel biedt een mechanisme dat door Linux-en UNIX-clients wordt gebruikt om te controleren of ze zijn verbonden met een site systeem dat bij de juiste hiërarchie hoort.  

     Als u geen vertrouwde basis sleutel opgeeft op de opdracht regel, vertrouwt de client het eerste beheer punt waarmee wordt gecommuniceerd en wordt automatisch de vertrouwde basis sleutel opgehaald van dat beheer punt.  

     Zie [Planning voor de vertrouwde basissleutel](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) voor meer informatie.  

     Voorbeeld: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     Optioneel. Hiermee geeft u de poort op die is geconfigureerd op beheerpunten die de client gebruikt voor de communicatie met beheerpunten via HTTP. Als de poort niet is opgegeven, wordt de standaard waarde van 80 gebruikt.  

     Voorbeeld: `-httpport 80`  

-   `-httpsport <port>`  

     Optioneel. Hiermee geeft u de poort op die is geconfigureerd op beheerpunten die de client gebruikt voor de communicatie met beheerpunten via HTTPS. Als de poort niet is opgegeven, wordt de standaard waarde van 443 gebruikt.  

     Voorbeeld: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     Optioneel. Hiermee geeft u op dat de clientinstallatie de SHA-256-validatie overslaat. Gebruik deze optie wanneer u de-client installeert op besturings systemen die niet zijn uitgebracht met een versie van OpenSSL die ondersteuning biedt voor SHA-256. Zie voor meer informatie [over Linux-en UNIX-besturings systemen die geen ondersteuning bieden voor SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     Optioneel. Geeft het volledige pad en de **CER** -bestandsnaam van het geëxporteerde zelfondertekende certificaat op de siteserver. Als er geen PKI-certificaten beschikbaar zijn, genereert de Configuration Manager-site server automatisch zelfondertekende certificaten.  

     Deze certificaten worden gebruikt om te valideren dat het clientbeleid dat via het beheerpunt is gedownload, is verzonden vanaf de gewenste site. Als er tijdens de installatie geen zelfondertekend bestand is opgegeven of u het certificaat moet wijzigen, gebruikt u het hulpprogramma **certutil** . Zie [certificaten beheren op de client voor Linux en UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts)voor meer informatie.  

     Dit certificaat kan worden opgehaald via het **SMS** -certificaatarchief en heeft de objectnaam **Site Server** en de beschrijvende naam **Site Server Signing Certificate**.  

     Als deze optie niet tijdens de installatie wordt opgegeven, vertrouwen Linux-en UNIX-clients het eerste beheer punt waarmee ze communiceren. Het handtekening certificaat wordt automatisch opgehaald van dat beheer punt.  

     Voorbeeld: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     Optioneel. Hiermee geeft u aanvullende PKI-certificaten op die geen deel uitmaken van een hiërarchie van een beheer punt certificerings instantie (CA). Als u meerdere certificaten op de opdrachtregel opgeeft, moeten ze worden gescheiden door komma's.  

     Gebruik deze optie als u PKI-client certificaten gebruikt die niet zijn gekoppeld aan een basis-CA-certificaat dat wordt vertrouwd door de beheer punten van uw sites. Beheer punten weigeren de client als het client certificaat niet is gekoppeld aan een vertrouwd basis certificaat in de lijst met certificaat verleners van de site.  

     Als u deze optie niet gebruikt, zal de Linux-en UNIX-client de vertrouwens hiërarchie alleen verifiëren met het certificaat in de `-UsePKICert` optie.  

     Voorbeeld: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="uninstalling-the-client-from-linux-and-unix-servers"></a><a name="BKMK_UninstallLnUClient"></a>De client van Linux-en UNIX-servers verwijderen  
 Als u de Configuration Manager-client voor Linux en UNIX wilt verwijderen, gebruikt u het hulp **programma uninstall.** Dit bestand bevindt zich standaard in de map **/opt/microsoft/configmgr/bin/** op de clientcomputer. Deze uninstall-opdracht biedt geen ondersteuning voor opdracht regel parameters en verwijdert alle bestanden met betrekking tot de client software van de-server.  

 Als u de client wilt verwijderen, gebruikt u de volgende opdrachtregel: **/opt/microsoft/configmgr/bin/uninstall**  

 U hoeft de computer niet opnieuw op te starten nadat u de Configuration Manager-client voor Linux en UNIX hebt verwijderd.  

##  <a name="configure-request-ports-for-the-client-for-linux-and-unix"></a><a name="BKMK_ConfigLnUClientCommuincations"></a> Aanvraagpoorten configureren voor de client voor Linux en UNIX  
 Net als op Windows-clients gebruikt de Configuration Manager-client voor Linux en UNIX HTTP en HTTPS om te communiceren met Configuration Manager-site systemen. De poorten die de Configuration Manager-client gebruikt om te communiceren, worden aanvraag poorten genoemd.  

 Wanneer u de Configuration Manager-client voor Linux en UNIX installeert, kunt u de standaard poort voor client aanvragen wijzigen door de installatie **-Eigenschappen-http Port** en **-https Port** op te geven. Wanneer u geen installatie-eigenschap en aangepaste waarde opgeeft, gebruikt de client de standaard waarden. De standaardwaarde voor HTTP-verkeer is **80** en de standaardwaarde voor HTTPS-verkeer is **443** .  

 Nadat u de client hebt geïnstalleerd, kunt u de configuratie van de aanvraag poort niet meer wijzigen. Als u de poortconfiguratie wilt wijzigen, moet u de client opnieuw installeren en de nieuwe poortconfiguratie opgeven. Wanneer u de-client opnieuw installeert om de aanvraag poort nummers te wijzigen, voert u de **installatie** opdracht uit die vergelijkbaar is met de nieuwe client installatie, maar gebruikt u de aanvullende opdracht regel eigenschap van **-keepdb**. Met deze switch wordt de installatie van de client database en de bestanden met de GUID en het certificaat archief van de clients.  

 Zie [client communicatie poorten configureren](../../../core/clients/deploy/configure-client-communication-ports.md)voor meer informatie over poort nummers voor client communicatie.  

##  <a name="configure-the-client-for-linux-and-unix-to-locate-management-points"></a><a name="BKMK_ConfigClientMP"></a> De client voor Linux en UNIX configureren om beheerpunten te zoeken  
 Wanneer u de Configuration Manager-client voor Linux en UNIX installeert, moet u een beheer punt opgeven dat moet worden gebruikt als eerste contact punt.  

 De Configuration Manager-client voor Linux en UNIX maakt contact met dit beheer punt op het moment dat de client wordt geïnstalleerd. Als de client geen contact kan maken met het beheerpunt, blijft de clientsoftware opnieuw proberen totdat er contact is gemaakt.  

 Zie [Zoeken naar beheerpunten](assign-clients-to-a-site.md#locating-management-points)voor meer informatie over hoe clients beheerpunten zoeken.

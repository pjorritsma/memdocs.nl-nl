---
title: Uw lab instellen
titleSuffix: Configuration Manager
description: Stel een lab in voor het evalueren van Configuration Manager met gesimuleerde real-life activiteiten.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 7623663e340d964593854883fa588484e239b4d0
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607871"
---
# <a name="set-up-a-configuration-manager-lab"></a>Een Configuration Manager Lab instellen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u de instructies in dit onderwerp volgt, kunt u een Lab instellen voor het evalueren van Configuration Manager met gesimuleerde activiteiten in realtime.  

> [!NOTE]
> Micro soft biedt een vooraf geconfigureerde versie van dit lab met behulp van een evaluatie versie van Configuration Manager. Zie [Windows and Office Deployment and Management Lab kit](/microsoft-365/enterprise/modern-desktop-deployment-and-management-lab)(Engelstalig) voor meer informatie. 

##  <a name="core-components"></a><a name="BKMK_LabCore"></a> Kernonderdelen  
 Voor het instellen van uw omgeving voor Configuration Manager zijn enkele kern onderdelen nodig om de installatie van Configuration Manager te ondersteunen.    

-   **De test omgeving maakt gebruik van Windows Server 2012 R2**, waarin we Configuration Manager zullen installeren.  

     U kunt een evaluatie versie van Windows Server 2012 R2 downloaden van het [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012).  

     Overweeg de verbeterde beveiliging van Internet Explorer te wijzigen of uit te scha kelen zodat u eenvoudiger toegang hebt tot bepaalde down loads waarnaar wordt verwezen tijdens het verloop van deze oefeningen. Zie [Internet Explorer: verbeterde beveiliging](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10))voor meer informatie.  

-   In **de test omgeving wordt SQL Server 2012 SP2 gebruikt** voor de site database.  

     U kunt een evaluatie versie van SQL Server 2012 downloaden van het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=43340).  

     SQL Server heeft [ondersteunde versies van SQL Server](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) die moeten worden voldaan voor gebruik met Configuration Manager.  

    -   Configuration Manager is een 64-bits versie van SQL Server om de site database te hosten.  

    -   **SQL_Latin1_General_CP1_CI_AS** als de **SQL-sorterings** klasse.  

    -   **Windows**-verificatie [in plaats van SQL-verificatie](/sql/relational-databases/security/choose-an-authentication-mode)is vereist.  

    -   Een toegewezen **SQL Server-exemplaar** is vereist.  

    -   Beperk het systeem niet- **adresseer bare geheugen** voor SQL Server.  

    -   Configureer het **SQL Server-service account** om uit te voeren met een domein gebruikers account met weinig rechten.  

    -   U moet **SQL Server Reporting Services**installeren.  

    -   **Intersite-communicatie** gebruikt de SQL Server Service Broker op de standaard poort TCP 4022.  

    -   **Intra site-communicatie** tussen de SQL server data base-engine en selecteer Configuration Manager site systeem rollen gebruiken standaard poort TCP 1433.  

-   **De domein controller maakt gebruik van Windows Server 2008 R2** met Active Directory Domain Services geïnstalleerd. De domein controller functioneert ook als host voor de DHCP-en de DNS-servers voor gebruik met een Fully Qualified Domain Name.  

     Zie [overzicht van Active Directory Domain Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831484(v=ws.11))voor meer informatie.  

-   **Hyper-V wordt gebruikt met een aantal virtuele machines** om te controleren of de beheer stappen die in deze oefeningen zijn uitgevoerd, werken zoals verwacht. Er worden mini maal drie virtuele machines aanbevolen, waarop Windows 10 is geïnstalleerd.  

     Zie [overzicht van Hyper-V](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11))voor meer informatie.  

-   Er zijn **beheerders machtigingen** vereist voor al deze onderdelen.  

    -   Voor Configuration Manager is een beheerder met lokale machtigingen in de Windows Server-omgeving vereist  

    -   Active Directory vereist een beheerder met machtigingen voor het wijzigen van het schema  

    -   Voor virtuele machines zijn lokale machtigingen op de computers zelf vereist  

Hoewel dit lab niet vereist is, kunt u [ondersteunde configuraties voor Configuration Manager](../../core/plan-design/configs/supported-configurations.md) controleren voor aanvullende informatie over de vereisten voor het implementeren van Configuration Manager. Raadpleeg de documentatie voor andere software versies dan waarnaar hier wordt verwezen.  

Nadat u al deze onderdelen hebt geïnstalleerd, moet u extra stappen ondernemen om uw Windows-omgeving te configureren voor Configuration Manager:  

##  <a name="prepare-active-directory-content-for-the-lab"></a><a name="BKMK_LabADPrep"></a> Active Directory-inhoud voor de testomgeving voorbereiden  
 Voor deze testomgeving maakt u een beveiligingsgroep en vervolgens voegt u een domeingebruiker eraan toe.  

-   Beveiligingsgroep: **Evaluation**  

    -   Groepsbereik: **Universal**  

    -   Groeps type: **beveiliging**  

-   Domeingebruiker: **ConfigUser**  

     Onder normale omstandigheden zou u geen universele toegang verlenen aan alle gebruikers binnen uw omgeving. U doet dit met deze gebruiker om het online brengen van uw testomgeving te stroomlijnen.  

De volgende stappen die vereist zijn om Configuration Manager-clients in te scha kelen Active Directory Domain Services om site bronnen te vinden, worden weer gegeven in de volgende procedures.  

##  <a name="create-the-system-management-container"></a><a name="BKMK_CreateSysMgmtLab"></a> De container voor systeembeheer maken  
 Configuration Manager wordt niet automatisch de vereiste System Management-container in Active Directory Domain Services gemaakt wanneer het schema wordt uitgebreid. Daarom maakt u deze voor uw testomgeving. Voor deze stap moet u [ADSI bewerken installeren](/previous-versions/windows/it-pro/windows-server-2003/cc773354(v=ws.10)).

 Zorg dat u bent aangemeld als een account waaraan de machtiging **Alle onderliggende objecten maken** is verleend voor de container **Systeem** in Active Directory Domain Services.  

#### <a name="to-create-the-system-management-container"></a>De container voor systeembeheer maken:  

1.  Voer **ADSI Bewerken**uit en maak verbinding met het domein waaronder de siteserver zich bevindt.  

2.  Vouw **domein &lt; computer Fully Qualified Domain name \> **uit, vouw **<DN \> -naam**uit, klik met de rechter muisknop op **CN = systeem**, klikt u op **Nieuw**en klik vervolgens op **object**.  

3.  Selecteer, in het **Maak object** dialoogvenster, **Container**, en klik dan op **Volgende**.  

4.  Tik in het vak **Waarde** , typ **System Management**en klik vervolgens op **Volgende**.  

5.  Klik op **Beëindig** om de procedure te vervolledigen.  

##  <a name="set-security-permissions-for-the-system-management-container"></a><a name="BKMK_SetSecPermLab"></a> Beveiligingsrechten instellen voor de container voor systeembeheer  
 Verleen het computeraccount van de siteserver de machtigingen die nodig zijn voor het publiceren van site-informatie naar de container. Voor deze taak gebruikt u ook ADSI Bewerken.  

> [!IMPORTANT]  
>  Bevestig dat u met het domein van de siteserver bent verbonden vóór het begin van de volgende procedure.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>Beveiligingsrechten instellen voor de container voor systeembeheer:  

1.  Vouw in het console venster het **domein van de site server**uit, vouw **DC = &lt; Server Distinguished name \> **uit en vouw **CN = System**. Klik met de rechter muisknop op **CN = systeem beheer**en klik vervolgens op **Eigenschappen**.  

2.  Klik in het dialoogvenster **CN=Eigenschappen voor systeembeheer** op het tabblad **Beveiliging** en klik vervolgens op **Toevoegen** om het computeraccount van de siteserver toe te voegen. Verleen aan het account de machtigingen **Volledig beheer** .  

3.  Klik op **Geavanceerd**, selecteer het computer account van de site server en klik vervolgens op **bewerken**.  

4.  Selecteer, in de lijst **Toepassen op** , de optie **Dit object en de onderliggende objecten**.  

5.  Klik op **OK** om de **ADSI Bewerken** -console te sluiten en de procedure te voltooien.  

     Zie voor meer informatie [het Active Directory schema voor Configuration Manager uitbreiden](../../core/plan-design/network/extend-the-active-directory-schema.md)  

##  <a name="extend-the-active-directory-schema-using-extadschexe"></a><a name="BKMK_ExtADSchLab"></a> Het Active Directory-schema met behulp van extadsch.exe uitbreiden  
 U gaat het Active Directory schema voor dit lab uitbreiden, zodat u alle Configuration Manager functies en functionaliteit kunt gebruiken met de minste administratieve overhead. Het uitbreiden van het Active Directory-schema is een configuratie voor het hele forest, die één keer per forest wordt uitgevoerd. Permanente uitbreiding van het schema wijzigt de set klassen en kenmerken in de basisconfiguratie van Active Directory. Deze actie kan niet ongedaan worden gemaakt. Als u het schema uitbreidt, hebben Configuration Manager toegang tot onderdelen waarmee het effectief kan worden gebruikt in uw test omgeving.  

> [!IMPORTANT]  
>  Verzeker u ervan dat u bent aangemeld op de schemamaster-domeincontroller met een account dat lid is van de beveiligingsgroep **Schemabeheerders** . Elke poging tot het gebruik van alternatieve referenties zal mislukken.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>Het Active Directory-schema met behulp van extadsch.exe uitbreiden:  

1.  Maak een back-up van de systeem status van de schema master-domein controller. Zie [Windows Server back-up](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770757(v=ws.11)) voor meer informatie over het maken van een back-up van de Master domein controller.  

2.  Navigeer naar **\SMSSETUP\BIN\X64** op het installatiemedium.  

3.  Voer **extadsch.exe**uit.  

4.  Controleer of de schema-uitbreiding is geslaagd door het **extadsch.log** te controleren dat zich in de hoofdmap van het systeemstation bevindt.  

     Zie [het Active Directory schema voor Configuration Manager uitbreiden](../../core/plan-design/network/extend-the-active-directory-schema.md)voor meer informatie.  

##  <a name="other-required-tasks"></a><a name="BKMK_OtherTasksLab"></a> Andere vereiste taken  
 U moet ook de volgende taken vóór de installatie voltooien.  

 **Een map maken voor het opslaan van alle downloads**  

 Er zijn tijdens deze oefening meerdere downloads vereist voor onderdelen van het installatiemedium. Voordat u begint met een installatieprocedure, kiest u een locatie waarbij u deze bestanden niet meer hoeft te verplaatsen totdat u de testomgeving weer buiten gebruik stelt. Eén map met afzonderlijke submappen voor het opslaan van deze downloads wordt aanbevolen.  

 **.NET installeren en Windows Communication Foundation activeren**  

 U moet eerst twee .NET Frameworks installeren: eerst .NET 3.5.1 en vervolgens .NET 4.5.2+. U moet ook Windows Communication Foundation (WCF) activeren. WCF is ontworpen om een beheerbare benadering te bieden voor gedistribueerde computing, brede interoperabiliteit en rechtstreekse ondersteuning voor service-oriëntatie. WCF vereenvoudigt ook de ontwikkeling van verbonden toepassingen via een servicegericht programmeermodel. Zie [Wat Is Windows Communication Foundation?](/previous-versions/dotnet/netframework-3.5/ms731082(v=vs.90))voor meer informatie.

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>.NET installeren en Windows Communication Foundation activeren:  

1.  Open **Server Manager**en navigeer vervolgens naar **Beheren**. Klik op **functies en onderdelen toevoegen** om de **wizard functies en onderdelen toevoegen** te openen.  

2.  Bekijk de informatie in het paneel **Voordat u begint** en klik vervolgens op **Volgende**.  

3.  Selecteer **Installatie die op de functie of het onderdeel is gebaseerd**en klik vervolgens op **Volgende**.  

4.  Selecteer de server in de **Servergroep**en klik vervolgens op **Volgende**.  

5.  Controleer het paneel **Serverfuncties** en klik vervolgens op **Volgende**.  

6.  Voeg de volgende **Functies** toe door deze te selecteren in de lijst:  

    -   **.NET Framework 3.5-functies**  

        -   **.NET Framework 3.5 (inclusief .NET 2.0 en 3.0)**  

    -   **Functies van .NET Framework 4.5**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **WCF-services**  

            -   **HTTP-activering**  

            -   **TCP-poort delen**  

7.  Controleer het scherm **Webserverrol (IIS)** en **Functieservices** en klik vervolgens op **Volgende**.  

8.  Controleer het scherm **Bevestiging** en klik vervolgens op **Volgende**.  

9. Klik op **Installeren** en controleer of de installatie is gelukt aan de hand van het deelvenster **Meldingen** van **Serverbeheer**.  

10. Nadat de basisinstallatie van .NET is voltooid, gaat u naar het [Microsoft Downloadcentrum](https://www.microsoft.com/download/details.aspx?id=42643) om het webinstallatieprogramma voor .NET Framework 4.5.2 op te halen. Klik op de knop **Downloaden** en kies vervolgens **Uitvoeren** voor het installatieprogramma. De vereiste onderdelen worden automatisch gedetecteerd en in de geselecteerde taal geïnstalleerd.  

**BITS, IIS en RDC inschakelen**  

[Background Intelligent Transfer Service (BITS)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282296(v=ws.11)) wordt gebruikt voor toepassingen die asynchroon bestanden moeten overbrengen tussen een client en een server. Door de stroom van de overdrachten op de voor- en achtergrond te reguleren, houdt BITS het reactievermogen van andere netwerktoepassingen intact. Ook worden automatisch bestandsoverdrachten hervat als een overdrachtssessie wordt onderbroken.  

U installeert BITS voor deze testomgeving, omdat deze siteserver ook wordt gebruikt als beheerpunt.  

Internet Information Services (IIS) is een flexibele, schaalbare webserver die kan worden gebruikt voor het hosten van alles op het web. Deze wordt door Configuration Manager gebruikt voor een aantal site systeem rollen. Raadpleeg [websites voor site systeem servers](../../core/plan-design/network/websites-for-site-system-servers.md)voor meer informatie over IIS.  

[Externe differentiële compressie (RDC)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754372(v=ws.11)) is een reeks API's dat toepassingen kunnen gebruiken om te bepalen of eventuele wijzigingen zijn aangebracht in een set bestanden. Via RDC kan de toepassing alleen de gewijzigde gedeelten van een bestand repliceren, waardoor netwerkverkeer tot een minimum wordt beperkt.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>De siteserverrollen BITS, IIS en RDC inschakelen:  

1.  Open op de siteserver **Server Manager**. Ga naar **Beheren**. Klik op **Functies en onderdelen toevoegen** om de **Wizard Functies en onderdelen toevoegen**te openen.  

2.  Bekijk de informatie in het paneel **Voordat u begint** en klik vervolgens op **Volgende**.  

3.  Selecteer **Installatie die op de functie of het onderdeel is gebaseerd**en klik vervolgens op **Volgende**.  

4.  Selecteer de server in de **Servergroep**en klik vervolgens op **Volgende**.  

5.  Voeg de volgende **Serverfuncties** toe door deze te selecteren in de lijst:  

    -   **Webserver (IIS)**  

        -   **Veelvoorkomende HTTP-functies**  

            -   **Standaard document**  

            -   **Bladeren door mappen**  

            -   **HTTP-fouten**  

            -   **Statische inhoud**  

            -   **HTTP-omleiding**  

        -   **Status en Diagnostische gegevens**  

            -   **HTTP-logboek registratie**  

            -   **Logboekregistratieprogramma's**  

            -   **Monitor aanvragen**  

            -   **Tracering**  

    -   **Prestaties**  

        -   **Compressie van statische inhoud**  

        -   **Compressie van dynamische inhoud**  

    -   **Beveiliging**  

        -   **Aanvraagfiltering**  

        -   **Basisverificatie**  

        -   **Verificatie van client certificaat toewijzing**  

        -   **IP-en domein beperkingen**  

        -   **URL-autorisatie**  

        -   **Windows-verificatie**  

    -   **Toepassings ontwikkeling**  

        -   **.NET Extensibility 3.5**  

        -   **.NET Extensibility 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **ISAPI-uitbreidingen**  

        -   **ISAPI-filters**  

        -   **Insluiten vanaf server**  

    -   **FTP-server**  

        -   **FTP-service**  

    -   **Beheerprogramma's**  

        -   **IIS-beheerconsole**  

        -   **Compatibiliteit met IIS 6-beheer**  

            -   **Compatibiliteit met IIS 6-metabase**  

            -   **IIS 6-beheerconsole**  

            -   **IIS 6-scripthulpprogramma's**  

            -   **Compatibiliteit met IIS 6 WMI**  

        -   **Scripts en hulpprogramma's voor IIS 6-beheer**  

        -   **Beheerservice**  

6.  Voeg de volgende **Functies** toe door deze te selecteren in de lijst:  

    -   **Background Intelligent Transfer Service (BITS)**  

          -   **IIS-serveruitbreiding**  

    -   **Externe-serverbeheerprogramma's**  

          -   **Beheerprogramma's voor onderdelen**  

          -   **Hulpprogramma's voor BITS-serveruitbreidingen**  

7.  Klik op **Installeren** en controleer of de installatie is gelukt aan de hand van het deelvenster **Meldingen** van **Serverbeheer**.  

IIS blokkeert standaard de toegang tot verschillende bestandsextensies en locaties voor HTTP- of HTTPS-communicatie. U moet aanvraagfiltering voor IIS op het distributiepunt configureren zodat deze bestanden kunnen worden gedistribueerd naar clientsystemen. Zie [IIS-aanvraag filtering voor distributie punten](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering)voor meer informatie.  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>IIS-filtering configureren voor distributiepunten:  

1.  Open **IIS Manager** en selecteer de naam van de server in de zijbalk. Hierdoor komt u in het scherm **Start** .  

2.  Controleer of **Functieweergave** is geselecteerd onder aan het scherm **Start** . Ga naar **IIS** en open **Filteren aanvragen**.  

3.  Klik in het deelvenster **Acties** op **Bestandsnaamextensie toestaan**.  

4.  Typ **.msi** in het dialoogvenster en klik op **OK**.  

##  <a name="installing-configuration-manager"></a><a name="BKMK_InstallCMLab"></a> Configuration Manager installeren  
U maakt een [bepalen wanneer u een primaire site wilt gebruiken](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) om clients rechtstreeks te beheren. Hierdoor kan uw test omgeving ondersteuning bieden voor het beheer van de [site systeem schaal](../plan-design/configs/size-and-scale-numbers.md) van potentiële apparaten.  
Tijdens dit proces installeert u ook de Configuration Manager-console, die wordt gebruikt voor het beheren van uw evaluatie apparaten.  

Voordat u de installatie begint, start u  [Prerequisite Checker](../servers/deploy/install/prerequisite-checker.md) op de server met Windows Server 2012 om te bevestigen dat alle instellingen correct zijn ingeschakeld.  

#### <a name="to-download-and-install-configuration-manager"></a>Configuration Manager downloaden en installeren:  

1.  Ga naar de pagina [System Center-evaluaties](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) om de nieuwste evaluatie versie van Configuration Manager te downloaden.  

2.  Decomprimeer het downloadmedium naar de vooraf gedefinieerde locatie.  

3.  Volg de installatie procedure die wordt vermeld bij [een site installeren met de Wizard Configuration Manager Setup](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md). In deze procedure geeft u de volgende invoer op:  

    |Stap in de procedure voor site-installatie|Selectie|  
    |-----------------------------------------|---------------|  
    |Stap 4: de pagina **Productcode**|Selecteer **Evaluatie**.|  
    |Stap 7:  **Vereiste downloads**|Selecteer **Vereiste bestanden downloaden** en geef de vooraf gedefinieerde locatie op.|  
    |Stap 10: **Site en installatie-instellingen**|-   **Sitecode:LAB**<br />-   **Sitenaam:Evaluation**<br />-   **Installatiemap:** geef de vooraf gedefinieerde locatie op.|  
    |Stap 11: **Primaire site-installatie**|Selecteer **De primaire site installeren als een zelfstandige site**en klik vervolgens op **Volgende**.|  
    |Stap 12: **Database-installatie**|-   **SQL Server-naam (FQDN):** voer hier de FQDN in.<br />-   **Exemplaarnaam:** laat dit leeg, omdat u het standaardexemplaar van SQL gebruikt dat u eerder hebt geïnstalleerd.<br />-   **Service Broker-poort:** laat de standaardpoort 4022 staan.|  
    |Stap 13: **Database-installatie**|Laat deze instellingen als standaard.|  
    |Stap 14: **SMS-provider**|Laat deze instellingen als standaard.|  
    |Stap 15: **Communicatie-instellingen voor clients**|Bevestig dat **Alle sitesysteemrollen accepteren alleen HTTPS-communicatie van clients** niet is ingeschakeld.|  
    |Stap 16: **Sitesysteemrollen**|Voer de FQDN-naam in en bevestig dat **Alle sitesysteemrollen accepteren alleen HTTPS-communicatie van clients** nog steeds is uitgeschakeld.|  

##  <a name="enable-publishing-for-the-configuration-manager-site"></a><a name="BKMK_EnablePubLab"></a> Publiceren inschakelen voor de Configuration Manager-site  
Elke Configuration Manager-site publiceert haar eigen site-specifieke informatie naar de systeem beheer-container binnen de domein partitie in het Active Directory-schema. Bidirectionele kanalen voor communicatie tussen Active Directory en Configuration Manager moeten worden geopend voor het afhandelen van dit verkeer. U schakelt bovendien ook forestdetectie in om bepaalde onderdelen van uw Active Directory en de netwerkinfrastructuur te bepalen.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Handel als volgt om Active Directory-forests voor publicatie te configureren:  

1.  Klik in de linkerbenedenhoek van de Configuration Manager-console op **beheer**.  

2.  Vouw in de werkruimte **Beheer** de optie **Hiërarchieconfiguratie**uit en klik vervolgens op **Detectiemethoden**.  

3.  Selecteer **Detectie van Active Directory-forests** en klik op **Eigenschappen**.  

4.  Selecteer in het dialoogvenster **Eigenschappen** de optie **Active Directory-forestdetectie inschakelen**. Als deze optie actief is, selecteert u **Automatisch Active Directory-sitegrenzen maken na detectie**. Er wordt een dialoogvenster weergegeven waarin wordt aangegeven **Wilt u zo snel mogelijk een volledige detectie uitvoeren?** Klik op **Ja**.  

5.  In de groep **Detectiemethode** aan de bovenkant van het scherm klikt u op **Forestdetectie nu uitvoeren**en vervolgens gaat u naar **Active Directory-forests** in de zijbalk. Uw Active Directory-forest moet worden weergegeven in de lijst met gedetecteerde forests.  

6.  Navigeer naar de bovenkant van het scherm op het tabblad **Algemeen** .  

7.  Vouw in de werkruimte **Beheer** de optie **Hiërarchieconfiguratie**uit en klik vervolgens op **Active Directory-forests**.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Een Configuration Manager site in staat stellen site-informatie te publiceren naar uw Active Directory-forest:  

1.  Klik op **Beheer**in de Configuration Manager-console.  

2.  U configureert een nieuw forest dat nog niet is gedetecteerd.  

3.  Klik op **Active Directory-forests** in de werkruimte **Beheer**.  

4.  Op het tabblad **Publiceren** van de site-eigenschappen selecteert u het verbonden forest en klikt u vervolgens op **Ok** om de configuratie op te slaan.
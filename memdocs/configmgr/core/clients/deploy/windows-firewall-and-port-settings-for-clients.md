---
title: Firewall-en poort instellingen voor Windows-clients
titleSuffix: Configuration Manager
description: Selecteer Windows Firewall-en poort instellingen voor clients in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2290899c0159221c5f45ce6c34332b766984e4c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713966"
---
# <a name="windows-firewall-and-port-settings-for-clients-in-configuration-manager"></a>Windows Firewall-en poort instellingen voor clients in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Client computers in Configuration Manager met Windows Firewall vaak vereisen dat u uitzonde ringen configureert om communicatie met hun site toe te staan. De uitzonde ringen die u moet configureren, zijn afhankelijk van de beheer functies die u gebruikt met de Configuration Manager-client.  

 Gebruik de volgende secties om deze beheerfuncties te identificeren en voor meer informatie over hoe Windows Firewall te configureren voor deze uitzonderingen.  

##  <a name="modifying-the-ports-and-programs-permitted-by-windows-firewall"></a><a name="BKMK_ModifyingWindowsFirewall"></a> De poorten en programma's toegestaan door Windows Firewall wijzigen  
 Gebruik de volgende procedure om de poorten en Program ma's op Windows Firewall voor de Configuration Manager-client te wijzigen.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>De door Windows Firewall toegstane poorten en programma's wijzigen  

1.  Open configuratiescherm op de computer waarop Windows Firewall uitgevoerd wordt.  

2.  Klik met de rechtermuisknop op **Windows Firewall**en klik dan op **Open**.  

3.  Configureer vereiste uitzonderingen en aangepaste programma's en poorten die u wenst.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Programma's en poorten die Configuration Manager vereist  
 De volgende Configuration Manager-functies vereisen uitzonde ringen op de Windows Firewall:  

### <a name="queries"></a>Query's  
 Als u de Configuration Manager-console uitvoert op een computer waarop Windows Firewall wordt uitgevoerd, mislukken query's de eerste keer dat ze worden uitgevoerd en wordt in het besturings systeem een dialoog venster weer gegeven waarin wordt gevraagd of u Statview. exe wilt deblokkeren. Indien u statview.exe deblokkeert zullen volgende query's zonder problemen uitgevoerd worden. U kunt ook handmatig Statview.exe toevoegen aan de lijst van prgramma's en diensten op het tabblad **Uitzonderingen** van de Windows Firewall vóór u een query uitvoert.  

### <a name="client-push-installation"></a>Clientpushinstallatie  
 Als u client-push wilt gebruiken om de Configuration Manager-client te installeren, voegt u het volgende als uitzonde ringen toe aan de Windows Firewall:  

-   Uitgaand en binnenkomend: **Bestands- en printerdeling**  

-   Binnenkomend: **Windows Management Instrumentation (WMI)**  

### <a name="client-installation-by-using-group-policy"></a>Installatie van de client via groepsbeleid  
 Als u groepsbeleid wilt gebruiken om de Configuration Manager-client te installeren, voegt u **Bestands-en printer deling** toe als uitzonde ring aan de Windows Firewall.  

### <a name="client-requests"></a>Aanvragen van client  
 Als u wilt dat client computers met Configuration Manager-site systemen communiceren, voegt u het volgende als uitzonde ringen toe aan de Windows Firewall:  

 Uitgaand: TCP-poort **80** (voor HTTP-communicatie)  

 Uitgaand: TCP-poort **443** (voor HTTPS-communicatie)  

> [!IMPORTANT]  
>  Dit zijn standaard poort nummers die kunnen worden gewijzigd in Configuration Manager. Zie How [to configure client communication ports](../../../core/clients/deploy/configure-client-communication-ports.md)(Engelstalig) voor meer informatie. Indien deze poorten gewijzigd zijn ten opzichte van hun standaardwaarden, moet u ook overeenkomstige uitzonderingen configureren op de Windows Firewall.  

### <a name="client-notification"></a>Clientmeldingen  
 Voeg het volgende toe als een uitzonde ring voor de Windows Firewall om client computers op de hoogte te stellen van een actie die moet worden uitgevoerd wanneer een gebruiker met beheerders rechten een client actie selecteert in de Configuration Manager-console, zoals het downloaden van computer beleid of het starten van een malware-scan.  

 Uitgaand: TCP-poort **10123**  

 Als deze communicatie mislukt, wordt Configuration Manager automatisch terugvallen op het gebruik van de bestaande client-naar-beheer punt communicatie poort van HTTP of HTTPS:  

 Uitgaand: TCP-poort **80** (voor HTTP-communicatie)  

 Uitgaand: TCP-poort **443** (voor HTTPS-communicatie)  

> [!IMPORTANT]  
>  Dit zijn standaard poort nummers die kunnen worden gewijzigd in Configuration Manager. Zie [client communicatie poorten configureren](../../../core/clients/deploy/configure-client-communication-ports.md)voor meer informatie. Indien deze poorten gewijzigd zijn ten opzichte van hun standaardwaarden, moet u ook overeenkomstige uitzonderingen configureren op de Windows Firewall.  

### <a name="remote-control"></a>Afstandsbediening  
 Als u Configuration Manager beheer op afstand wilt gebruiken, moet u de volgende poort toestaan:  

-   Binnenkomend: TCP-poort **2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Hulp op afstand en extern bureaublad  
 Om hulp op afstand vanuit de Configuration Manager-console te initiëren, voegt u het aangepaste programma **Helpsvc. exe** en de binnenkomende aangepaste poort TCP **135** toe aan de lijst met toegestane Program ma's en services in Windows Firewall op de client computer. U moet ook **Hulp op afstand** en **Extern bureaublad**toestaan. Indien u Hulp op afstand initieert van de clientcomputer, configureert Firewall automatisch **Hulp op afstand** en **Extern bureaublad**en laat ze ook toe.  

### <a name="wake-up-proxy"></a>Wake-Up proxy  
 Indien u de instelling voor wake-up proxy client inschakelt, gebruikt een nieuwe service met de naam ConfigMgr wake-up proxy een peer-to-peer protocol om te controleren of er computers actief zijn op het subnet en om ze indien nodig te activeren. Deze mededeling maakt gebruik van de volgende poorten:  

 Uitgaand: UDP-poort **25536**  

 Uitgaand: UDP-poort **9**  

 Dit zijn de standaard poort nummers die kunnen worden gewijzigd in Configuration Manager met behulp van de **Energiebeheer** instellingen voor clients van **Wake-up Proxy poort nummer (udp)** en **Wake on LAN poort nummer (UDP)**. Als u de clientinstelling **Energiebeheer:****Windows Firewall-uitzondering voor wake-up proxy** opgeeft, worden deze poorten automatisch geconfigureerd in Windows Firewall voor clients. Indien clients evenwel een verschillende firewall uitvoeren, moet u handmatig de uitzonderingen voor deze poortnummers configureren.  

 Behalve deze poorten gebruikt wake-up proxy ook Internet Control Message Protocol (ICMP) echoaanvraagberichten van één clientcomputer aan een andere clientcomputer. Deze communicatie wordt gebruikt om te bevestigen of de andere clientcomputer actief is op het netwerk. Naar ICMP wordt soms verwezen als TCP/IP-pingopdrachten.  

 Zie [plan How to wake up clients](../../../core/clients/deploy/plan/plan-wake-up-clients.md)(Engelstalig) voor meer informatie over Wake-up proxy.  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Logboeken van Windows, prestatiemeter van Windows en Windows diagnostische gegevens  
 Als u toegang wilt krijgen tot Windows Logboeken, prestatie meter van Windows en Windows diagnostische gegevens vanuit de Configuration Manager console, schakelt u **Bestands-en printer deling** in als een uitzonde ring op de Windows Firewall.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Poorten die worden gebruikt tijdens de implementatie van de Configuration Manager-client  
 De volgende tabellen geeft de lijst van de poorten die gebruikt worden tijdens het installatieproces van de klant.  

> [!IMPORTANT]  
>  Bevestig, indien er een firewall is tussen de sitesysteemservers en de clientcomputer, of de firewall verkeer toestaat voor de poorten die vereist zijn voor de clientinstallatiemethode die u kiest. Firewalls verhinderen bijvoorbeeld dikwijls het succes van clientpushinstallatie omdat ze Server Message Block (SMB) en Remote Procedure Calls (RPC) blokkeren. Gebruik in dit scenario een andere clientinstallatiemethode, zoals handmatige installatie (uitvoeren van CCMSetup.exe) of groepsbeleid-gebaseerde clientinstallatie. Deze alternatieve clientinstallatiemethodes vereisen geen SMB of RPC.  

 Voor informatie over hoe Windows Firewall te configureren op de clientcomputer, zie [De poorten en programma's toegestaan door Windows Firewall wijzigen](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Poorten die worden gebruikt voor alle installatiemethoden  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP) van de clientcomputer naar een terugvalstatuspunt, wanneer een terugvalstatuspunt toegekend is aan de client.|--|80 (zie opmerking 1, **alternatieve poort beschikbaar**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>Poorten die worden gebruikt met clientpushinstallatie  
 Behalve de poorten die voorkomen in de lijst in de volgende tabel, gebruikt clientpushinstallatie ook Internet Control Message Protocol (ICMP) echoaanvraagberichten van de siteserver naar de clientcomputer om te bevestigen of de clientcomputer beschikbaar is op het netwerk. Naar ICMP wordt soms verwezen als TCP/IP-pingopdrachten. ICMP heeft geen UDP- of TCP-protocolnummer en komt dus niet voor op de lijst in de volgende tabel. Alle tussenliggende netwerkapparaten, zoals firewalls, moeten evenwel ICMP-verkeer toestaan opdat de clientpushinstallatie zou slagen.  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB) tussen de siteserver en clientcomputer.|--|445|  
|RPC eindpunttoewijzer tussen de siteserver en de clientcomputer.|135|135|  
|RPC dynamische poorten tussen de siteserver en de clientcomputer.|--|DYNAMISCH|  
|Hypertext Transfer Protocol (HTTP) van de clientcomputer naar een beheerpunt, wanneer de verbinding over HTTP gebeurt.|--|80 (zie opmerking 1, **alternatieve poort beschikbaar**)|  
|Secure Hypertext Transfer Protocol (HTTPS) van de clientcomputer naar een beheerpunt, wanneer de verbinding over HTTPS gebeurt.|--|443 (zie opmerking 1, **alternatieve poort beschikbaar**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Poorten die worden gebruikt met punt-gebaseerde installatie van software-update  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP) van de clientcomputer naar het software-updatepunt.|--|80 of 8530 (zie opmerking 2, **Windows Server Update Services**)|  
|Secure Hypertext Transfer Protocol (HTTPS) van de clientcomputer naar het software-updatepunt.|--|443 of 8531 (zie opmerking 2, **Windows Server Update Services**)|  
|Server Message Block (SMB) tussen de bron server en de client computer wanneer u de CCMSetup-opdracht regel eigenschap **/Source:&lt;Path\>** opgeeft.|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Poorten die worden gebruikt met installatie op basis van groepsbeleid  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP) van de clientcomputer naar een beheerpunt, wanneer de verbinding over HTTP gebeurt.|--|80 (zie opmerking 1, **alternatieve poort beschikbaar**)|  
|Secure Hypertext Transfer Protocol (HTTPS) van de clientcomputer naar een beheerpunt, wanneer de verbinding over HTTPS gebeurt.|--|443 (zie opmerking 1, **alternatieve poort beschikbaar**)|  
|Server Message Block (SMB) tussen de bron server en de client computer wanneer u de CCMSetup-opdracht regel eigenschap **/Source:&lt;Path\>** opgeeft.|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Poorten die gebruikt worden bij handmatige installatie en bij installatie gebaseerd op aanmeldingsscript  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB) tussen de clientcomputer en een netwerkshare van waaruit u CCMSetup.exe uitvoert.<br /><br /> Wanneer u Configuration Manager installeert, worden de bron bestanden van de client installatie gekopieerd en automatisch gedeeld * &lt;vanuit\>* de map InstallationPath \Client op beheer punten. U kunt evenwel deze bestanden kopiëren en een nieuwe share creëren op een computer op het netwerk. Alternatief kunt u dit netwerkverkeer elimineren door lokaal CCMSetup.exe uit te voeren door, bijvoorbeeld, verwisselbare media te gebruiken.|--|445|  
|Hypertext Transfer Protocol (HTTP) van de client computer naar een beheer punt wanneer de verbinding over HTTP is en u de CCMSetup-opdracht regel eigenschap **/Source:&lt;Path\>** niet opgeeft.|--|80 (zie opmerking 1, **alternatieve poort beschikbaar**)|  
|Beveilig Hypertext Transfer Protocol (HTTPS) van de client computer naar een beheer punt wanneer de verbinding over HTTPS is en geef de CCMSetup-opdracht regel eigenschap **/Source:&lt;Path\>** niet op.|--|443 (zie opmerking 1, **alternatieve poort beschikbaar**)|  
|Server Message Block (SMB) tussen de bron server en de client computer wanneer u de CCMSetup-opdracht regel eigenschap **/Source:&lt;Path\>** opgeeft.|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Poorten die worden gebruikt met installatie gebaseerd op softwaredistributie  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB) tussen het distributiepunt en de clientcomputer.|--|445|  
|Hypertext Transfer Protocol (HTTP) van de client naar een distributiepunt, wanneer de verbinding over HTTP gebeurt.|--|80 (zie opmerking 1, **alternatieve poort beschikbaar**)|  
|Secure Hypertext Transfer Protocol (HTTPS) van de client naar een distributiepunt, wanneer de verbinding over HTTPS gebeurt.|--|443 (zie opmerking 1, **alternatieve poort beschikbaar**)|  

## <a name="notes"></a>Opmerkingen  
 **1 alternatieve poort beschikbaar** In Configuration Manager kunt u een alternatieve poort definiëren voor deze waarde. Indien een aangepaste poort is gedefinieerd, vervang dan deze aangepaste poort wanneer u de IP-filter informatie definieert voor IPsec beleidslijnen of om firewalls te configureren.  

 **2 Windows Server Update Services** U kunt Windows Server Update Service (WSUS) installeren op de standaardwebsite (poort 80) of op een aangepaste website (poort 8530).  

 Na de installatie kunt u de poort te wijzigen. U moet niet hetzelfde poortnummer gebruiken over de hele sitehiërarchie.  

 Als de HTTP-poort 80 is, moet de HTTPS-poort 443 zijn.  

 Als de HTTP-poort iets anders is, moet de HTTPS-poort 1 hoger zijn. Bijvoorbeeld 8530 en 8531.

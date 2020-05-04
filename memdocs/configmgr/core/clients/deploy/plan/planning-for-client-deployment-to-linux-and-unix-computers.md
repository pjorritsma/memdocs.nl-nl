---
title: Client implementatie op Linux-en UNIX-computers plannen
titleSuffix: Configuration Manager
description: Plan voor client implementatie op Linux-en UNIX-computers in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfede7594224ff48af2a1e4066e69d551c3c576e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713231"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Planning voor client implementatie op Linux-en UNIX-computers in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> Vanaf versie 1902 biedt Configuration Manager geen ondersteuning voor Linux-of UNIX-clients. 
> 
> Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.

U kunt de Configuration Manager-client installeren op computers waarop Linux of UNIX wordt uitgevoerd. Deze client is ontworpen voor servers die als werkgroepcomputer fungeren en de client ondersteunt geen interactie met aangemelde gebruikers. Nadat u de-client software hebt geïnstalleerd en de client communicatie tot stand brengt met de Configuration Manager-site, beheert u de client met behulp van de Configuration Manager-console en-rapporten.  

> [!NOTE]
>  De Configuration Manager-client voor Linux-en UNIX-computers biedt geen ondersteuning voor de volgende beheer mogelijkheden:  
> 
> - Clientpushinstallatie  
>   -   Implementatie van besturingssystemen  
>   -   Toepassingsimplementatie; implementeer in plaats daarvan software met behulp van pakketten en programma's.  
>   -   Software-inventaris  
>   -   Software-updates  
>   -   Instellingen voor naleving  
>   -   Extern beheer  
>   -   Energiebeheer  
>   -   Clientcontrole en herstel van de clientstatus  
>   -   Clientbeheer via internet  

 Voor informatie over de ondersteunde Linux-en UNIX-distributies en de vereiste hardware voor ondersteuning van de-client voor Linux en UNIX raadpleegt u [Aanbevolen hardware voor Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Gebruik de informatie in dit artikel om u te helpen bij het implementeren van de Configuration Manager-client voor Linux en UNIX.  

##  <a name="prerequisites-for-client-deployment-to-linux-and-unix-servers"></a><a name="BKMK_ClientDeployPrereqforLnU"></a>Vereisten voor client implementatie op Linux-en UNIX-servers  
 Gebruik de volgende informatie om te bepalen aan welke vereisten moet worden voldaan om de client voor Linux en UNIX te implementeren.  

###  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ClientDeployExternalforLnU"></a>Externe afhankelijkheden voor Configuration Manager:  
 In de volgende tabellen worden de vereiste UNIX- en Linux-besturingssystemen en pakketafhankelijkheden beschreven.  

 **Red Hat Enterprise Linux Server versie 5.1 (Tikanga)**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|glibc|Standaardbibliotheken voor C|2.5-12|  
|Openssl|OpenSSL-bibliotheken; Secure Network Communications-protocol|0.9.8b-8.3.el5|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server versie 6**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|glibc|Standaardbibliotheken voor C|2.12-1.7|  
|Openssl|OpenSSL-bibliotheken; Secure Network Communications-protocol|1.0.0-4|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

 **Red Hat Enterprise Linux Server versie 7**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|glibc|Standaardbibliotheken voor C|2.17|  
|Openssl|OpenSSL-bibliotheken; Secure Network Communications-protocol|1.0.1|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

 **Solaris 10 SPARC**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|Vereiste besturingssysteempatch|PAM-geheugenlek|117463-05|  
|SUNWlibC|Sun Workshop gebundelde samenstellers libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Math & Microtasking-bibliotheken (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Math & Microtasking-bibliotheken (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Core Solaris-bibliotheken (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Core Solaris-bibliotheken (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|OpenSSL|SUNopenssl-bibliotheken (Usr)<br /><br /> Sun biedt de OpenSSL-bibliotheken voor Solaris 10 SPARC. Ze worden gebundeld met het besturingssysteem.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Pluggable Authentication Modules<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|Vereiste besturingssysteempatch|PAM-geheugenlek|117464-04|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Math & Microtasking-bibliotheken (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris, (gedeelde bibliotheken) (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|Core Solaris-bibliotheken (Root) (i386)|11.10.0, REV=2005.01.21.16.34|  
|OpenSSL|SUNWopenssl-bibliotheken; OpenSSL-bibliotheken (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Pluggable Authentication Modules<br /><br /> SUNWcsr Core Solaris, (Root)(i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking-bibliotheken (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris-bibliotheken (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (gedeelde bibliotheken)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL-bibiotheken (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking-bibliotheken (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris-bibliotheken (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (gedeelde bibliotheken)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL-bibiotheken (Usr)|11.11.0,REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|glibc-2,4-31,30|Standaard gedeelde bibliotheek voor C|2.4-31.30|  
|OpenSSL|OpenSSL-bibliotheken; Secure Network Communications-protocol|0.90,8a-18,15|  
|PAM|Pluggable Authentication Modules|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Standaard gedeelde bibliotheek voor C|2.9-13.2|  
|PAM|Pluggable Authentication Modules|pam-1.0.2-20.1|  

 **Universal Linux (Debian-pakket) Debian, Ubuntu Server**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|libc6|Standaard gedeelde bibliotheek voor C|2.3.6|  
|OpenSSL|OpenSSL-bibliotheken; Secure Network Communications-protocol|0.9.8 of 1.0|  
|PAM|Pluggable Authentication Modules|0.79-3|  

 **Universal Linux (RPM-pakket) CentOS, Oracle Linux**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|glibc|Standaard gedeelde bibliotheek voor C|2.5-12|  
|OpenSSL|OpenSSL-bibliotheken; Secure Network Communications-protocol|0.9.8 of 1.0|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|Versie van het besturingssysteem|Versie van besturingssysteem|AIX 6,1: elk technologie niveau en Service Pack|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|OpenSSL-bibliotheken; Secure Network Communications-protocol|0.9.8.4|  

 **IBM AIX 7,1 (voeding)**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|Versie van het besturingssysteem|Versie van besturingssysteem|AIX 7,1: elk technologie niveau en Service Pack|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|OpenSSL-bibliotheken; Secure Network Communications-protocol||  


 **HP-UX 11i v3 IA64**  

|Vereist pakket|Beschrijving|Minimale versie|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation-besturingsomgeving|B.110,310,0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Specifieke IA-ontwikkelbibliotheken|B.110,31|  
|SysMgmtMin|Hulpprogramma's voor minimale software-implementatie|B.110,310,0709|  
|SysMgmtMin.openssl|OpenSSL-bibliotheken; Secure Network Communications-protocol|A.00.09.08d.002|  
|PAM|Pluggable Authentication Modules|Op HP is PAM onderdeel van de kernonderdelen van het besturingssysteem. Er zijn geen andere afhankelijkheden.|  

 **Configuration Manager afhankelijkheden:** De volgende tabel geeft een lijst van site systeem rollen die ondersteuning bieden voor Linux-en UNIX-clients. Zie [de site systeem rollen voor Configuration Manager-clients bepalen](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)voor meer informatie over deze site systeem rollen.  

|Configuration Manager site systeem|Meer informatie|  
|---------------------------------------|----------------------|  
|Beheerpunt|Hoewel een beheer punt niet vereist is om een Configuration Manager-client voor Linux en UNIX te installeren, moet u een beheer punt hebben om informatie over te dragen tussen client computers en Configuration Manager-servers. Zonder een beheer punt kunt u geen client computers beheren.|  
|Distributiepunt|Het distributie punt is niet vereist voor de installatie van een Configuration Manager-client voor Linux en UNIX. De sitesysteemrol is echter wel vereist als u software naar Linux- en UNIX-servers implementeert.<br /><br /> Omdat de Configuration Manager-client voor Linux en UNIX geen ondersteuning biedt voor communicatie die gebruikmaakt van SMB, moeten de distributie punten die u met de client gebruikt, HTTP-of HTTPS-communicatie ondersteunen.|  
|Terugvalstatuspunt|Het terugval status punt is niet vereist om een Configuration Manager-client voor Linux en UNIX te installeren. Het terugval status punt stelt computers in de Configuration Manager-site echter in staat om status berichten te verzenden wanneer ze niet kunnen communiceren met een beheer punt. Clients kunnen ook hun installatiestatus naar het terugvalstatuspunt verzenden.|  

 **Firewall vereisten**: Zorg ervoor dat firewalls geen communicatie blok keren over de poorten die u opgeeft als poort voor client aanvragen. De client voor Linux en UNIX communiceert rechtstreeks met beheerpunten, distributiepunten en terugvalstatuspunten.  

 Voor meer informatie over poorten op de client voor communicatie en aanvragen, zie [De client voor Linux en UNIX configureren om beheerpunten te zoeken](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="planning-for-communication-across-forest-trusts-for-linux-and-unix-servers"></a><a name="BKMK_PlanningforCommunicationsforLnU"></a>Planning voor de communicatie tussen forest-vertrouwens relaties voor Linux-en UNIX-servers  
 Linux-en UNIX-servers die u beheert met Configuration Manager fungeren als werkgroepcomputers en vereisen soort gelijke configuraties als Windows-clients die zich in een werk groep bevinden. Zie voor meer informatie over communicatie van computers in werk groepen [communicatie over Active Directory forests](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).  

###  <a name="service-location-by-the-client-for-linux-and-unix"></a><a name="BKMK_ServiceLocationforLnU"></a>Service locatie door de client voor Linux en UNIX  
 De taak om een sitesysteemserver te zoeken die clients van services voorzien, wordt een servicelocatie genoemd. In tegens telling tot een Windows-client gebruikt de client voor Linux en UNIX geen Active Directory voor service locatie. Daarnaast biedt de Configuration Manager-client voor Linux en UNIX geen ondersteuning voor een client eigenschap die het domein achtervoegsel van een beheer punt opgeeft. In plaats daarvan leert de client over aanvullende sitesysteemservers die services aan clients leveren via een bekend beheerpunt dat u toewijst wanneer u de clientsoftware installeert.  

 Zie [service locatie en hoe clients het toegewezen beheer punt bepalen](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)voor meer informatie.  

##  <a name="planning-for-security-and-certificates-for-linux-and-unix-servers"></a><a name="BKMK_SecurityforLnU"></a>Planning voor beveiliging en certificaten voor Linux-en UNIX-servers  
 Voor beveiligde en geverifieerde communicatie met Configuration Manager-sites gebruikt de Configuration Manager-client voor Linux en UNIX hetzelfde model voor communicatie als de Configuration Manager-client voor Windows.  

 Wanneer u de Linux-en UNIX-client installeert, kunt u een PKI-certificaat toewijzen aan de client, zodat deze HTTPS kan gebruiken om te communiceren met Configuration Manager-sites. Als u geen PKI-certificaat toewijst, maakt de client een zelfondertekend certificaat en communiceert deze alleen via HTTP.  

 Clients die worden voorzien van een PKI-certificaat wanneer ze worden geïnstalleerd, gebruiken HTTPS om te communiceren met beheerpunten. Wanneer een client geen beheerpunt kan vinden dat HTTPS ondersteunt, wordt HTTP met het opgegeven PKI-certificaat gebruikt.  

 Wanneer een Linux-of UNIX-client een PKI-certificaat gebruikt, hoeft u deze niet goed te keuren. Wanneer een client een zelfondertekend certificaat gebruikt, controleert u de hiërarchie-instellingen voor goed keuring van de client in de Configuration Manager-console. Wanneer niet de goedkeuringsmethode **Alle computers automatisch goedkeuren (niet aanbevolen)** voor de client wordt gebruikt, moet u de client handmatig goedkeuren.  

 Zie [clients beheren vanaf het knoop punt apparaten](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)voor meer informatie over het hand matig goed keuren van de client.  

 Zie [PKI-certificaat vereisten](../../../plan-design/network/pki-certificate-requirements.md)voor meer informatie over het gebruik van certificaten in Configuration Manager.  

###  <a name="about-certificates-for-use-by-linux-and-unix-servers"></a><a name="BKMK_AboutCertsforLnU"></a>Over certificaten voor gebruik door Linux-en UNIX-servers  
 De Configuration Manager-client voor Linux en UNIX gebruikt een zelfondertekend certificaat of een X. 509 PKI-certificaat, net als Windows-clients. Er zijn geen wijzigingen in de PKI-vereisten voor Configuration Manager-site systemen wanneer u Linux-en UNIX-clients beheert.  

 De certificaten die u gebruikt voor Linux-en UNIX-clients die met Configuration Manager-site systemen communiceren, moeten een PKCS # 12-indeling (Public Key Certificate Standard) hebben en het wacht woord moet bekend zijn, zodat u het op de client kunt opgeven wanneer u het PKI-certificaat opgeeft.  

 De Configuration Manager-client voor Linux en UNIX ondersteunt één PKI-certificaat en biedt geen ondersteuning voor meerdere certificaten. Daarom zijn de selectie criteria voor certificaten die u configureert voor een Configuration Manager site niet van toepassing.  

###  <a name="configuring-certificates-for-linux-and-unix-servers"></a><a name="BKMK_ConfigCertsforLnU"></a>Certificaten voor Linux-en UNIX-servers configureren  
 Als u een Configuration Manager-client voor Linux-en UNIX-servers wilt configureren voor het gebruik van HTTPS-communicatie, moet u de client configureren voor het gebruik van een PKI-certificaat op het moment dat u de client installeert. U kunt geen certificaat inrichten voordat u de-client software installeert.  

 Wanneer u een client installeert die gebruikmaakt van een PKI-certificaat, gebruikt u de opdracht regel `-UsePKICert` parameter om de locatie en naam op te geven van een PKCS # 12-bestand dat het PKI-certificaat bevat. Daarnaast moet u de opdracht regel parameter `-certpw` gebruiken om het wacht woord voor het certificaat op te geven.  

 Als u niet opgeeft `-UsePKICert`, genereert de client een zelfondertekend certificaat en probeert ze te communiceren met de site systeem servers met behulp van http.  

##  <a name="versions-that-dont-support-sha-256"></a><a name="BKMK_NoSHA-256"></a>Versies die SHA-256 niet ondersteunen  
 De volgende Linux en UNIX-besturings systemen die worden ondersteund als clients voor Configuration Manager, zijn uitgebracht met versies van OpenSSL die geen ondersteuning bieden voor SHA-256:  

-   Solaris-versie 10 (SPARC/x86)  


 Als u deze besturings systemen met Configuration Manager wilt beheren, moet u de Configuration Manager-client voor Linux en UNIX installeren met een opdracht regel parameter waarmee de client de validatie van SHA-256 kan overs Laan. Configuration Manager-clients die worden uitgevoerd op deze besturingssysteem versies werken in een minder veilige modus dan clients die SHA-256 ondersteunen. Deze minder veilige werkmodus wordt gekenmerkt door het volgende gedrag:  

-   Clients valideren de hand tekening van de site server niet die is gekoppeld aan het beleid dat ze aanvragen van een beheer punt.  

-   Clients valideren de hash niet voor pakketten die ze downloaden van een distributie punt.  

> [!IMPORTANT]  
>  Met `ignoreSHA256validation` deze optie kunt u de client voor Linux-en UNIX-computers in een minder veilige modus uitvoeren. Dit is bedoeld voor gebruik op oudere platforms die geen ondersteuning voor SHA-256 bieden. Dit is een beveiligingsonderdrukking en wordt niet door Microsoft wordt aanbevolen, maar wordt ondersteund voor gebruik in een veilige en vertrouwde datacenteromgeving.  

 Wanneer de Configuration Manager-client voor Linux en UNIX wordt geïnstalleerd, controleert het installatie script de versie van het besturings systeem. Standaard, als de versie van het besturings systeem wordt geïdentificeerd zonder een versie van OpenSSL die ondersteuning biedt voor SHA-256, mislukt de installatie van de Configuration Manager-client.  

 Als u de Configuration Manager-client wilt installeren op Linux-en UNIX-besturings systemen die niet zijn uitgebracht met een versie van OpenSSL die ondersteuning biedt voor SHA-256, moet `ignoreSHA256validation`u de installatie opdracht regel optie gebruiken. Wanneer u deze opdracht regel optie op een toepasselijk Linux-of UNIX-besturings systeem gebruikt, slaat de Configuration Manager-client de SHA-256-validatie over en na de installatie, gebruikt de client SHA-256 niet om gegevens te ondertekenen die via HTTP naar site systemen worden verzonden. Zie voor meer informatie over het configureren van Linux-en UNIX-clients voor het gebruik van certificaten [plannen voor beveiliging en certificaten voor Linux-en UNIX-servers](#BKMK_SecurityforLnU). Zie [ondertekening en versleuteling configureren](../../../plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption)voor meer informatie over het vereisen van SHA-256.  

> [!NOTE]  
>  De opdracht regel optie `ignoreSHA256validation` wordt genegeerd op computers waarop een versie van Linux en UNIX wordt uitgevoerd die is uitgebracht met versies van openssl die ondersteuning bieden voor SHA-256.  

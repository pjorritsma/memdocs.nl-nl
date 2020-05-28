---
title: De implementatie van de client naar Macs voorbereiden
titleSuffix: Configuration Manager
description: Configuratie taken voorafgaand aan de implementatie van de Configuration Manager-client naar Macs.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2b5bcbce659601e10f44f06af94eb939767a389a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906627"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Voorbereiden voor het implementeren van client software op Macs

*Van toepassing op: Configuration Manager (huidige vertakking)*

Volg deze stappen om ervoor te zorgen dat u klaar bent om [de Configuration Manager-client op Mac-computers te implementeren](deploy-clients-to-macs.md).



## <a name="mac-prerequisites"></a>Mac-vereisten

Het Mac-client installatie pakket wordt niet geleverd met de Configuration Manager media. Down load de **clients voor aanvullende besturings systemen** via het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=47719).  

Zie [ondersteunde besturings systemen voor clients en apparaten](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)voor een lijst met ondersteunde versies.



## <a name="certificate-requirements"></a>Certificaatvereisten

Voor client installatie en-beheer voor Mac-computers zijn open bare-sleutel infrastructuur (PKI)-certificaten vereist. PKI-certificaten beveiligen de communicatie tussen de Mac-computers en de Configuration Manager-site met behulp van wederzijdse verificatie en versleutelde gegevens overdracht. Configuration Manager kunt een gebruikers client certificaat aanvragen en installeren. Het maakt gebruik van Certificate Services met een certificerings instantie voor ondernemingen en het Configuration Manager inschrijvings punt en het inschrijvings proxy punt. U kunt ook een computer certificaat aanvragen en installeren onafhankelijk van Configuration Manager. Dit certificaat moet voldoen aan de Configuration Manager certificaat vereisten.  

Configuration Manager Mac-clients controleren altijd op intrekken van certificaten. U kunt deze functie niet uitschakelen.  

Als Mac-clients de certificaatintrekkingslijst (CRL) niet kunnen vinden, kunnen ze geen verbinding maken met Configuration Manager-site systemen. In het bijzonder voor Mac-clients in een ander forest naar de uitgevende certificerings instantie, controleert u uw CRL-ontwerp. Zorg ervoor dat Mac-clients een CRL kunnen vinden en downloaden.  

Voordat u de Configuration Manager-client op een Mac-computer installeert, moet u bepalen hoe u het client certificaat installeert:  

-   Gebruik het [CMEnroll-hulp programma](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll)om Configuration Manager-inschrijving te gebruiken. Het registratie proces biedt geen ondersteuning voor automatische certificaat vernieuwing. Opnieuw registreren van Mac-computers voordat het certificaat verloopt.  

-   [Gebruik een certificaat aanvraag en installatie methode die onafhankelijk is van Configuration Manager](deploy-clients-to-macs.md#bkmk_external).  

Zie [PKI-certificaat vereisten voor Configuration Manager](../../plan-design/network/pki-certificate-requirements.md)voor meer informatie over de vereisten voor Mac-client certificaten.  

Mac-clients worden automatisch toegewezen aan de Configuration Manager-site die ze beheert. Mac-clients worden geïnstalleerd als clients met alleen Internet verbinding, zelfs als communicatie is beperkt tot het intranet. Deze configuratie betekent dat ze communiceren met beheer punten en distributie punten die zijn ingeschakeld op internet in hun toegewezen site. Mac-computers communiceren niet met site systemen buiten hun toegewezen site.  

> [!IMPORTANT]  
>  De Configuration Manager-client voor macOS kan niet worden gebruikt om verbinding te maken met een beheer punt dat is geconfigureerd voor het gebruik van een [database replica](../../servers/deploy/configure/database-replicas-for-management-points.md).  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Een webserver certificaat implementeren op site systeem servers  

Als deze site systemen dit niet hebben, implementeert u een webserver certificaat op de computers die deze site systeem rollen hebben:  

-   Beheerpunt  

-   Distributiepunt  

-   Inschrijvingspunt  

-   Proxypunt voor inschrijving  

Het webserver certificaat moet de Internet-FQDN bevatten die is opgegeven in de eigenschappen van het site systeem. De server hoeft geen toegang te hebben tot het internet om Mac-computers te ondersteunen. Als u geen client beheer op internet nodig hebt, kunt u de intranet-FQDN-waarde voor de Internet-FQDN opgeven.  

Specificeer de Internet-FQDN-waarde van het site systeem in het webserver certificaat voor het beheer punt, het distributie punt en het inschrijvings proxy punt.

Zie [het webserver certificaat implementeren voor site systemen die IIS uitvoeren](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)voor meer informatie over een voorbeeld implementatie.  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Een certificaat voor client verificatie implementeren op site systeem servers  

Als deze site systemen dit niet hebben, implementeert u een certificaat voor client verificatie op de computers die als host fungeren voor deze site systeem rollen:  

-   Beheerpunt  

-   Distributiepunt  

Zie het [client certificaat voor Windows-computers implementeren](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)voor een voorbeeld implementatie waarbij het client certificaat voor beheer punten wordt gemaakt en geïnstalleerd.  

Zie het [client certificaat voor distributie punten implementeren](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)voor een voorbeeld implementatie waarbij het client certificaat voor distributie punten wordt gemaakt en geïnstalleerd.  

> [!IMPORTANT]  
>  Als u de-client wilt implementeren op apparaten met macOS Sierra, moet de onderwerpnaam van het certificaat van het beheer punt correct worden geconfigureerd. Gebruik bijvoorbeeld de FQDN-naam van de beheer punt server.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Het client certificaat sjabloon voor Macs voorbereiden  

De certificaat sjabloon moet de machtigingen **lezen** en **registreren** hebben voor de gebruikers account die het certificaat op de Mac-computer inschrijft.  

Zie [het client certificaat voor Mac-computers implementeren](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1)voor meer informatie.  



## <a name="configure-the-management-point-and-distribution-point"></a>Het beheer punt en distributie punt configureren  

Configureer beheerpunten voor de volgende opties:  

-   HTTPS  

-   Client verbindingen via Internet toestaan. Deze configuratiewaarde is vereist voor het beheren van Mac-computers. Het betekent echter niet dat site systeem servers toegankelijk moeten zijn vanaf internet.  

-   Laat mobiele apparaten en Mac-computers dit beheerpunt gebruiken  

Distributie punten zijn niet vereist voor de installatie van de client voor Mac. Als u na de installatie van de client software op deze computers wilt implementeren, moet u distributie punten configureren om client verbindingen van het Internet toe te staan.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Beheer punten en distributie punten configureren voor de ondersteuning van Macs  

Voordat u met deze procedure begint, moet u ervoor zorgen dat u het beheer punt en distributie punt configureert met een Internet-FQDN. Als deze servers geen ondersteuning bieden voor client beheer op internet, geeft u de intranet-FQDN op als de Internet-FQDN-waarde.

De site systeem rollen moeten zich in een primaire site bestaan.  

1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **servers en site systeem rollen** . Selecteer vervolgens de server met de juiste site systeem rollen.  

2.  Selecteer in het detail venster de rol **beheer punt** en selecteer **Eigenschappen** in het lint. In het venster **Eigenschappen van beheer punt** configureert u de volgende opties:  

    1.  Kies **https**.  

    2.  Kies **alleen client verbindingen via Internet toestaan** of **intranet-en Internet-client verbindingen**toestaan. Voor deze opties is een Internet-of intranet-FQDN vereist.  

    3.  Kies **mobiele apparaten en Mac-computers toestaan dit beheer punt te gebruiken**.  

    4. Selecteer **OK** om deze configuratie op te slaan.  

3.  Selecteer in het detail venster van het knoop punt server en site systeem rollen de **distributiepunt** rol en selecteer **Eigenschappen** in het lint. Configureer de volgende opties in het venster **Eigenschappen van distributie punt** :  

    -   Kies **https**.  

    -   Kies **alleen client verbindingen via Internet toestaan** of **intranet-en Internet-client verbindingen**toestaan. Voor deze opties is een Internet-of intranet-FQDN vereist.  

    -   Kies **certificaat importeren**, blader naar het geëxporteerde certificaat bestand van het client distributiepunt en geef het wacht woord op.  

4.  Herhaal deze procedure voor alle beheer punten en distributie punten in primaire sites voor het beheren van Mac-computers.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Het inschrijvings proxy punt en het inschrijvings punt configureren  

Installeer beide rollen in dezelfde site. U hoeft ze niet op dezelfde site systeem server of in hetzelfde Active Directory forest te installeren.  

Zie [site systeem rollen](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)voor meer informatie over de plaatsing van site systeem rollen en overwegingen.  

Zie [site systeem rollen installeren](../../servers/deploy/configure/install-site-system-roles.md)om de site systeem rollen toe te voegen ter ondersteuning van Mac-computers.

Selecteer op de pagina **selectie van systeem functies** **inschrijvings proxy punt** en **inschrijvings punt** uit de lijst met beschik bare rollen.  



## <a name="install-the-reporting-services-point"></a>Het Reporting Services-punt installeren  

Zie [het Reporting Services-punt installeren](../../servers/manage/configuring-reporting.md)voor meer informatie.  



## <a name="next-steps"></a>Volgende stappen

[De Configuration Manager-client op Mac-computers implementeren](deploy-clients-to-macs.md)  

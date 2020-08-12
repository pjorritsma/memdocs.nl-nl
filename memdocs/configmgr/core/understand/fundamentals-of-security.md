---
title: Basisprincipes van beveiliging
titleSuffix: Configuration Manager
description: Meer informatie over de beveiligings lagen in Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c702916f73d1fbc842966161a6958a61d24044a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126066"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Basis principes van beveiliging voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat een overzicht van de volgende fundamentele beveiligings onderdelen van een Configuration Manager omgeving:
- [Beveiligingslagen](#bkmk_layers)
- [Op rollen gebaseerd beheer](#bkmk_rba)
- [Clienteindpunten beveiligen](#bkmk_endpoints)
- [Configuration Manager-accounts en -groepen](#bkmk_accounts)
- [Privacy](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a>Beveiligings lagen

De beveiliging voor Configuration Manager bestaat uit de volgende lagen: 
- [Windows-besturings systeem en netwerk beveiliging](#bkmk_layer-windows)
- [Netwerk infrastructuur: firewalls, inbraak detectie, open bare-sleutel infrastructuur (PKI)](#bkmk_layer-network)
- [Beveiligings besturings elementen Configuration Manager](#bkmk_layer-cm)
- [SMS-provider](#bkmk_layer-provider)
- [Site database machtigingen](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a>Windows-besturings systeem en netwerk beveiliging
De eerste laag wordt verzorgd door Windows-beveiligings functies voor zowel het besturings systeem als het netwerk. Deze laag bevat de volgende onderdelen:  

-   Bestanden delen voor bestands overdracht tussen Configuration Manager onderdelen  

-   Toegangsbeheerlijsten (ACLs) om bestanden en registersleutels veilig te stellen  

-   Internet Protocol Security (IPsec) om de communicatie te helpen beveiligen  

-   groepsbeleid beveiligings beleid instellen  

-   DCOM-machtigingen (Distributed Component Object Model) voor gedistribueerde toepassingen, zoals de Configuration Manager-console  

-   Active Directory Domain Services voor het opslaan van beveiligings-principals  

-   Windows-account beveiliging, inclusief bepaalde groepen die tijdens de installatie Configuration Manager maken  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a>Netwerk infrastructuur

Aanvullende beveiligings onderdelen, zoals firewalls en inbraak detectie, helpen bij het bieden van beveiliging voor de hele omgeving. Certificaten die zijn uitgegeven door de industrie standaard PKI-implementaties, bieden ondersteuning voor verificatie, ondertekening en versleuteling.  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a>Beveiligings besturings elementen Configuration Manager

Naast de beveiliging die door de Windows-Server en de netwerk infrastructuur wordt gegeven, beheert Configuration Manager de toegang tot de console en bronnen op verschillende manieren. Standaard hebben alleen lokale beheerders rechten op de bestanden en register sleutels die de Configuration Manager-console nodig heeft op computers waarop u deze installeert.  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a>SMS-provider

De volgende beveiligingslaag is gebaseerd op toegang via WMI (Windows Management Instrumentation), in het bijzonder de SMS-provider. De SMS-provider is een Configuration Manager onderdeel waarmee gebruikers toegang kunnen krijgen tot de site database voor informatie. Standaard is de SMS-provider beperkt tot leden van de lokale groep SMS Admins . Deze groep bevat eerst alleen de gebruiker die Configuration Manager heeft geïnstalleerd. Als u andere account wilt machtigen voor de CIM-opslagplaats (CIM: Common Information Model) en de SMS-provider, voegt u de andere accounts toe aan de groep SMS Admins.  

Vanaf versie 1810 kunt u het minimale verificatie niveau voor beheerders opgeven om toegang te krijgen tot Configuration Manager-sites. Deze functie dwingt beheerders af om zich aan te melden bij Windows met het vereiste niveau. <!--1357013-->  

Zie [de SMS-provider plannen](../plan-design/hierarchy/plan-for-the-sms-provider.md)voor meer informatie.

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a>Site database machtigingen

De laatste beveiligingslaag is gebaseerd op machtigingen voor objecten in de sitedatabase. Standaard kan het lokale systeem account en de gebruikers account die u hebt gebruikt voor het installeren van Configuration Manager, alle objecten in de site database beheren. Machtigingen verlenen en beperken voor extra gebruikers met beheerders rechten in de Configuration Manager-console door gebruik te maken van beheer op basis van rollen.  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a>Op rollen gebaseerd beheer  

 Configuration Manager maakt gebruik van op rollen gebaseerd beheer om objecten zoals verzamelingen, implementaties en sites te beveiligen. Dit beheermodel definieert en beheert centraal instellingen voor beveiligingstoegang van alle sites in de hiërarchie en site-instellingen. 

 Een beheerder wijst *beveiligings rollen* toe aan gebruikers met beheerders rechten en groeps machtigingen. De machtigingen zijn verbonden met verschillende Configuration Manager-object typen, bijvoorbeeld om client instellingen te maken of te wijzigen. 

 Met beveiligingsbereiken worden specifieke exemplaren van *objecten gegroepeerd die* door een gebruiker met beheerders rechten moeten worden beheerd, zoals een toepassing die Microsoft 365-apps installeert. 

 De combi natie van beveiligings rollen, beveiligingsbereiken en verzamelingen definiëren de objecten die een gebruiker met beheerders rechten kan weer geven en beheren. Configuration Manager installeert sommige standaard beveiligings rollen voor veelvoorkomende beheer taken. Maak uw eigen beveiligings rollen ter ondersteuning van uw specifieke bedrijfs vereisten.  

 Zie [op rollen gebaseerd beheer configureren](../servers/deploy/configure/configure-role-based-administration.md)voor meer informatie.  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a>Client eindpunten beveiligen  

 Configuration Manager client communicatie met site systeem rollen beveiligt door gebruik te maken van zelfondertekende of PKI-certificaten of met Azure Active Directory Azure AD-tokens. Voor sommige scenario's is het gebruik van PKI-certificaten vereist. Bijvoorbeeld [client beheer op Internet](../clients/manage/plan-internet-based-client-management.md)en voor [clients van mobiele apparaten](../../mdm/plan-design/plan-on-premises-mdm.md).  

 U kunt de site systeem rollen configureren waarmee clients verbinding maken voor de HTTPS-of HTTP-client communicatie. Client computers communiceren altijd met de veiligste methode die beschikbaar is. Client computers vallen alleen terug op het gebruik van de minder veilige communicatie methode als u site systeem rollen hebt die HTTP-communicatie toestaan.  

 Zie [Beveiliging plannen](../plan-design/security/plan-for-security.md)voor meer informatie.



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a>Configuration Manager accounts en-groepen  

 Configuration Manager gebruikt het lokale systeem account voor de meeste site bewerkingen. Voor sommige beheer taken moet u mogelijk extra accounts maken en onderhouden. Configuration Manager maakt verschillende standaard groepen en SQL Server rollen tijdens de installatie. Mogelijk moet u computer-of gebruikers accounts hand matig toevoegen aan de standaard groepen en SQL Server rollen.  

 Zie [accounts die worden gebruikt in Configuration Manager](../plan-design/hierarchy/accounts.md)voor meer informatie.  



## <a name="privacy"></a><a name="bkmk_privacy"></a>Privacybescherming  

 Voordat u Configuration Manager implementeert, moet u rekening houden met uw privacy-vereisten. Zakelijke beheer producten bieden veel voor delen omdat ze de meeste clients effectief kunnen beheren, maar deze software kan van invloed zijn op de privacy van gebruikers in uw organisatie. Configuration Manager bevat veel hulpprogram ma's om gegevens te verzamelen en apparaten te bewaken. Sommige hulpprogram ma's kunnen privacy-problemen in uw organisatie veroorzaken.  

 Wanneer u bijvoorbeeld de Configuration Manager-client installeert, worden standaard veel beheer instellingen ingeschakeld. Deze configuratie zorgt ervoor dat de client software gegevens naar de Configuration Manager-site verzendt. De site slaat client informatie op in de site database. De client gegevens worden niet rechtstreeks naar micro soft verzonden. Zie [diagnostiek en gebruiks gegevens](../plan-design/diagnostics/diagnostics-and-usage-data.md)voor meer informatie.



## <a name="see-also"></a>Zie ook

- [De beveiliging plannen](../plan-design/security/plan-for-security.md)  

- [Beveiliging en privacy voor Configuration Manager-clients](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Beveiliging configureren](../plan-design/security/configure-security.md)   

- [Communicatie tussen eind punten](../plan-design/hierarchy/communications-between-endpoints.md)  

- [Technische naslaginformatie voor cryptografische besturingselementen](../plan-design/security/cryptographic-controls-technical-reference.md)  

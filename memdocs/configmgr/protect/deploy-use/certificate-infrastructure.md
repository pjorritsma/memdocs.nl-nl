---
title: Certificaatinfrastructuur configureren
titleSuffix: Configuration Manager
description: Meer informatie over het configureren van certificaat inschrijving in Configuration Manager.
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 590c6fd336ec19949b5f5b99b25b3104524a52d6
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210108"
---
# <a name="configure-certificate-infrastructure"></a>Certificaatinfrastructuur configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Meer informatie over het configureren van de certificaat infrastructuur in Configuration Manager. Voordat u begint, moet u controleren op vereisten die worden vermeld in [vereisten voor certificaat profielen](../../protect/plan-design/prerequisites-for-certificate-profiles.md).  

Gebruik deze stappen voor het configureren van uw infra structuur voor SCEP-of PFX-certificaten.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>Stap 1: de registratie service en afhankelijkheden voor netwerk apparaten installeren en configureren (alleen voor SCEP-certificaten)

 U moet de rolservice registratieservice voor netwerkapparaten voor Active Directory Certificate Services (AD CS) installeren en configureren, de beveiligingsmachtigingen op de certificaatsjablonen wijzigen, een PKI (Public Key Infrastructure) verificatievergadering implementeren en het register bewerken om de standaard URL-groottelimiet van Internet Information Services (IIS) te verhogen. Indien nodig moet u ook de uitgevende certificeringsinstantie (CA) configureren om een aangepaste geldigheidsperiode toe te staan.  

> [!IMPORTANT]  
>  Voordat u Configuration Manager configureert om te werken met de registratie service voor netwerk apparaten, controleert u de installatie en configuratie van de registratie service voor netwerk apparaten. Als deze afhankelijkheden niet correct werken, kunt u problemen met het inschrijven van certificaten oplossen met behulp van Configuration Manager.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>De registratieservice en afhankelijkheden voor netwerkapparaten installeren en configureren  

1. Installeer en configureer op een server met Windows Server 2012 R2 de rolservice Registratieservice voor netwerkapparaten voor de serverrol Active Directory Certificate Services. Zie [richt lijnen voor registratie service voor netwerk apparaten](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\))voor meer informatie.

2. Controleer en wijzig indien nodig de beveiligingsmachtigingen voor de certificaatsjablonen die worden gebruikt door de registratieservice voor netwerkapparaten:  

   -   Voor het account dat de Configuration Manager-console uitvoert: machtiging **lezen** .  

        Deze machtiging is vereist voor het uitvoeren van de wizard Certificaatprofiel maken, u kunt bladeren om het certificaatsjabloon te selecteren dat u wilt gebruiken wanneer u een SCEP- instellingenprofiel maakt. Bij het selecteren van een certificaatsjabloon worden bepaalde instellingen in de wizard automatisch ingevuld, zodat u minder moet configureren en er minder kans bestaat om instellingen te selecteren die niet compatibel zijn met de certificaatsjablonen die de registratieservice voor netwerkapparaten gebruikt.  

   -   De machtigingen **Lezen** en **Inschrijven** voor het SCEP-serviceaccount waarvan de groep toepassingen in de registratieservice voor netwerkapparaten gebruikmaakt.  

        Deze vereiste is niet specifiek voor Configuration Manager, maar maakt deel uit van het configureren van de registratie service voor netwerk apparaten. Zie [richt lijnen voor registratie service voor netwerk apparaten](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\))voor meer informatie.  

   > [!TIP]  
   >  Gebruik de volgende registersleutel op de server die wordt uitgevoerd met de registratieservice voor netwerkapparaten om te identificeren welke sjablonen door de registratieservice voor netwerkapparaten worden gebruikt: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

   > [!NOTE]  
   >  Dit zijn de standaardbeveiligingsmachtigingen die geschikt zijn voor de meeste omgevingen. U kunt echter een alternatieve beveiligingsconfiguratie gebruiken. Zie [plannen voor certificaat sjabloon machtigingen voor certificaat profielen](../../protect/plan-design/planning-for-certificate-template-permissions.md)voor meer informatie.  

3. Een PKI-certificaat dat clientverificatie ondersteunt naar deze server implementeren. Mogelijk hebt u al een geschikt certificaat geïnstalleerd op de computer dat u kunt gebruiken, of mogelijk moet u (of verkiest u) speciaal voor dit doel een certificaat te implementeren. Voor meer informatie over de vereisten voor dit certificaat raadpleegt u de Details voor servers waarop de Configuration Manager-beleids module wordt uitgevoerd met de functie Service registratie service voor netwerk apparaten in de sectie **PKI-certificaten voor servers** in het onderwerp [PKI-certificaat vereisten voor Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md) .  

   > [!TIP]
   >  Als u hulp nodig hebt bij de implementatie van dit certificaat, kunt u de instructies voor [het implementeren van het client certificaat voor distributie punten](../../core/plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)gebruiken, omdat de certificaat vereisten hetzelfde zijn met één uitzonde ring:  
   > 
   > - Het selectievakje **De persoonlijke sleutel exporteerbaar maken** niet selecteren op tabblad **Afhandeling van aanvragen** van de eigenschappen voor de certificaatsjabloon.  
   > 
   >   U moet dit certificaat niet exporteren met de persoonlijke sleutel omdat u naar het lokale computer archief kunt bladeren en dit moet selecteren wanneer u de Configuration Manager-beleids module configureert.  

4. Zoek het basiscertificaat waarnaar het clientverificatiecertificaat overeenkomt. Exporteer vervolgens dit basis-CA-certificaat naar een certificaat (.cer)-bestand. Dit bestand op een veilige locatie opslaan voor veilige toegang wanneer u later de sitesysteemserver voor het certificaatregistratiepunt installeert en configureert.  

5. Gebruik op dezelfde server de register-editor om de standaard URL-groottelimiet voor IIS te verhogen, door de volgende DWORD-waarden voor de registersleutel HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP in te stellen op:  

   - Stel de **MaxFieldLength**-sleutel in op **65534**.  

   - Stel de **MaxRequestBytes-sleutel** in op **16777216**.  

     Zie Microsoft Ondersteuning artikel [820129: http. sys Registry Settings for Windows](https://support.microsoft.com/help/820129)(Engelstalig) voor meer informatie.

6. Op dezelfde server, in IIS-beheerder (Internet Information Services), de instellingen voor aanvraagfiltering voor de toepassing /certsrv/mscep wijzigen en vervolgens de server opnieuw opstarten. In het dialoogvenster **Instellingen voor aanvraagfiltering bewerken** moeten de instellingen van **Aanvraaglimieten** de volgende zijn:  

   - **Maximale toegestane inhoudslengte (bytes)**: **30000000**  

   - **Maximale URL-lengte (bytes)**: **65534**  

   - **Maximale queryreeks (bytes)**: **65534**  

     Zie [limieten voor IIS-aanvragen](https://docs.microsoft.com/iis/configuration/system.webServer/security/requestFiltering/requestLimits/)voor meer informatie over deze instellingen en hoe u deze kunt configureren.

7. Als u een certificaat wilt aanvragen met een kortere geldigheidsperiode dan de certificaatsjabloon die u gebruikt: deze configuratie is voor een ondernemings-CA standaard uitgeschakeld. Het opdrachtregelprogramma Certutil gebruiken, vervolgens de certificaatservice stopzetten en opnieuw opstarten met behulp de volgende opdrachten, om deze optie op een ondernemings-CA in te schakelen:  

   1. **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      Zie [Certificate Services Tools and Settings](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc780742\(v=ws.10\))(Engelstalig) voor meer informatie.

8. Controleer of de registratie service voor netwerk apparaten werkt door de volgende koppeling als voor beeld te gebruiken `https://server.contoso.com/certsrv/mscep/mscep.dll`:. U zou de ingebouwde webpagina van de registratieservice voor netwerkapparaten moeten zien. Deze webpagina legt uit waaruit de service bestaat en legt uit dat netwerkapparaten de URL gebruiken om certificaataanvragen te verzenden.  

   Nu dat de registratieservice voor netwerkapparaten en afhankelijkheden zijn geconfigureerd, bent u klaar om het certificaatregistratiepunt nu te installeren en configureren.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>Stap 2: het certificaat registratiepunt installeren en configureren.

U moet ten minste één certificaat registratiepunt installeren en configureren in de hiërarchie van de Configuration Manager. u kunt deze site systeemrol installeren op de centrale beheer site of in een primaire site.  

> [!IMPORTANT]  
>  Voordat u het certificaat registratiepunt installeert, raadpleegt u de sectie **site systeem vereisten** in het onderwerp [ondersteunde configuraties voor Configuration Manager](../../core/plan-design/configs/supported-configurations.md) voor de besturingssysteem vereisten en afhankelijkheden voor het certificaat registratiepunt.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Het certificaatregistratiepunt installeren en configureren  

1. Klik op **Beheer**in de Configuration Manager-console.  

2. Vouw in de werkruimte **Beheer**, **Siteconfiguratie** uit, klik op **Servers en sitesysteemrollen** en selecteer vervolgens de server die u wilt gebruiken voor het certificaatregistratiepunt.  

3. Klik op **Sitesysteemrollen toevoegen** in het tabblad **Start** in de groep **Server**.  

4. Configureer de algemene instellingen voor het sitesysteem op de pagina **Algemeen** en klik vervolgens op **Volgende**.  

5. Klik op de pagina **Proxy** op **Volgende**. Het certificaatregistratiepunt gebruikt geen internetproxy-instellingen.  

6. Selecteer **Certificaatregistratiepunt** uit de lijst beschikbare rollen op de pagina **Systeemrolselectie** en klik vervolgens op **Volgende**. 

7. Selecteer op de pagina **certificaat registratie modus** of u wilt dat dit certificaat registratiepunt **SCEP-certificaat aanvragen verwerkt**of **PFX-certificaat aanvragen verwerkt**. Een certificaat registratiepunt kan niet beide soorten aanvragen verwerken, maar u kunt meerdere certificaat registratie punten maken als u met beide certificaat typen werkt.

   Als u PFX-certificaten verwerkt, moet u een certificerings instantie kiezen, hetzij micro soft of de belasters.

8. De pagina instellingen voor het **certificaat registratiepunt** is afhankelijk van het certificaat type:
   - Als u **SCEP-certificaat aanvragen verwerken**hebt geselecteerd, configureert u het volgende:
     -   De naam van de **website**, het **HTTPS-poort nummer**en de naam van de **virtuele toepassing** voor het certificaat registratiepunt. Deze velden worden automatisch ingevuld met standaard waarden. 
     -   **URL voor de registratie service voor netwerk apparaten en het basis-CA-certificaat** : Klik op **toevoegen**en geef in het dialoog venster **URL en basis-CA-certificaat toevoegen** het volgende op:
         - **URL voor de registratieservice voor netwerkapparaten**: geef de URL in de volgende indeling op: https://*<server_FQDN>*/certsrv/mscep/mscep.dll. Als de FQDN-naam van de server waarop de registratie service voor netwerk apparaten wordt uitgevoerd bijvoorbeeld server1.contoso.com is, `https://server1.contoso.com/certsrv/mscep/mscep.dll`typt u.
         - **Basis-CA-certificaat**: blader naar en selecteer het certificaatbestand (.cer) dat u in **Stap 1: De registratieservice en afhankelijkheden voor netwerkapparaten installeren en configureren hebt gemaakt en opgeslagen**. Met dit basis-CA-certificaat kan het certificaat registratiepunt het client verificatie certificaat valideren dat door de Configuration Manager-beleids module wordt gebruikt.  

   - Als u **PFX-certificaat aanvragen verwerken**hebt geselecteerd, configureert u de verbindings gegevens en referenties voor de geselecteerde certificerings instantie.

     - Als u micro soft als de certificerings instantie wilt gebruiken, klikt u op **toevoegen** en geeft u het volgende op in het dialoog venster **een certificerings instantie en een account toevoegen** :
         - **Naam van de certificerings instantie server** : Voer de naam van de certificerings instantie server in.
         - **Account** van de certificerings instantie: Klik op **instellen** om te selecteren of maak het account dat machtigingen heeft om in te schrijven in sjablonen van de certificerings instantie.
         - **Verbindings account voor certificaat registratiepunt** : Selecteer of maak het account dat het certificaat registratiepunt verbindt met de Configuration Manager-Data Base. Alteratively kunt u het lokale computer account gebruiken van de computer die als host fungeert voor het certificaat registratiepunt.
         - **Active Directory certificaat publicatie account** : Selecteer een account of maak een nieuw account dat wordt gebruikt voor het publiceren van certificaten voor gebruikers objecten in Active Directory.

         - Geef in het dialoog venster **URL voor registratie van netwerk apparaten en basis-CA-certificaat** het volgende op en klik vervolgens op **OK**:  

     - Als u de machtiging wilt gebruiken als de certificerings instantie, geeft u het volgende op:

       - De **URL** van de MDM-webservice
       - De gebruikers naam en het wacht woord voor de URL.

         Wanneer u de MDM-API gebruikt voor het definiëren van de URL van de reserverings webservice, moet u ervoor zorgen dat u ten minste versie 9 van de API gebruikt, zoals wordt weer gegeven in het volgende voor beeld:

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         Eerdere versies van de API bieden geen ondersteuning voor de vertrouwens service.

9. Klik op **Volgende** en voltooi de wizard.  

10. Wacht enkele minuten zodat de installatie kan worden voltooid en controleer vervolgens dat het certificaatregistratiepunt geïnstalleerd is aan de hand van een van de volgende methodes:  

    -   Vouw in de werkruimte **Bewaking****Systeemstatus**, klik op **Onderdeelstatus** en zoek naar statusberichten van het onderdeel **SMS_CERTIFICATE_REGISTRATION_POINT**.  

    -   Gebruik op de sitesysteemserver de bestanden *<Installatiepad Configuration Manager\>* \Logs\crpsetup.log en *<Installatiepad Configuration Manager\>* \Logs\crpmsi.log. Een geslaagde installatie retourneert een afsluitcode 0.  

    -   Controleer met behulp van een browser of u verbinding kunt maken met de URL van het certificaat registratiepunt. Bijvoorbeeld `https://server1.contoso.com/CMCertificateRegistration`. U moet een **Serverfout**-pagina zien voor de toepassingsnaam, met een HTTP 404-beschrijving.  

11. Zoek het geëxporteerde certificaatbestand voor de basis-CA dat het certificaatregistratiepunt automatisch in de volgende map op de primaire siteservercomputer heeft gemaakt: *<Installatiepad ConfigMgr\>* \inboxes\certmgr.box. Sla dit bestand op een beveiligde locatie op waartoe u veilig toegang kunt krijgen wanneer u later de Configuration Manager-beleids module installeert op de server waarop de registratie service voor netwerk apparaten wordt uitgevoerd.  

    > [!TIP]  
    >  Dit certificaat is niet onmiddellijk beschikbaar in deze map. Mogelijk moet u een tijdje wachten (bijvoorbeeld een half uur) voordat Configuration Manager het bestand naar deze locatie kopieert.  


## <a name="step-3----install-the-configuration-manager-policy-module-for-scep-certificates-only"></a>Stap 3: Installeer de Configuration Manager-beleids module (alleen voor SCEP-certificaten).

U moet de Configuration Manager-beleids module installeren en configureren op elke server die u hebt opgegeven in **stap 2: het certificaat registratiepunt installeren en configureren** als **URL voor de registratie service voor netwerk apparaten** in de eigenschappen voor het certificaat registratiepunt.  

##### <a name="to-install-the-policy-module"></a>De beleidsmodule installeren  

1. Op de server waarop de registratie service voor netwerk apparaten wordt uitgevoerd, meldt u zich aan als een domein beheerder en kopieert u de\>volgende bestanden uit de map <ConfigMgrInstallationMedia \SMSSETUP\POLICYMODULE\X64 op de Configuration Manager installatie media naar een tijdelijke map:  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   Als u een taalpakketmap hebt op de installatiemedia, kopieert u bovendien deze map en de inhoud hiervan.  

2. Voer in de tijdelijke map PolicyModuleSetup. exe uit om de installatie wizard voor de Configuration Manager-beleids module te starten.  

3. Klik op de eerste pagina van de wizard op **Volgende**, aanvaard de licentievoorwaarden en klik vervolgens op **Volgende**.  

4. Op de pagina **Installatiemap**, aanvaardt u de standaardinstallatiemap voor de beleidsmodule of geeft u een alternatieve map op. Klik vervolgens op **Volgende**.  

5. Geef op de pagina **Certificaatregistratiepunt** de URL van het certificaatregistratiepunt op met behulp van de FQDN van de sitesysteemserver en de virtuele toepassingsnaam die is opgegeven in de eigenschappen voor het certificaatregistratiepunt. De standaardnaam van de virtuele toepassing is CMCertificateRegistration. Bijvoorbeeld, als de site systeem server een FQDN van server1.contoso.com heeft en u de standaard naam van de virtuele toepassing hebt gebruikt `https://server1.contoso.com/CMCertificateRegistration`, geeft u op.

6. Aanvaard de standaardpoort **443** of geef het alternatieve poortnummer op dat door certificaatregistratiepunt wordt gebruikt en klik vervolgens op **Volgende**.  

7. Geef op de pagina **Clientcertificaat voor de beleidsmodule**het clientverificatiecertificaat op dat u in **Stap 1: De registratieservice en afhankelijkheden voor netwerkapparaten installeren en configureren** hebt geïmplementeerd en klik vervolgens op **Volgende**.  

8. Klik op de pagina **Certificaat voor certificaatregistratiepunt** op **Bladeren** om het geëxporteerde certificaatbestand voor de basis-CA te selecteren dat u aan het einde van **Stap 2: Het certificaatregistratiepunt installeren en configureren hebt opgeslagen**.  

   > [!NOTE]  
   >  Als u dit certificaatbestand nog niet hebt opgeslagen, bevindt het zich in <Installatiepad Configuration Manager\>\inboxes\certmgr.box op de siteservercomputer.  

9. Klik op **Volgende** en voltooi de wizard.  

   Als u de Configuration Manager-beleids module wilt verwijderen, gebruikt u **Program ma's en onderdelen** in het configuratie scherm. 

 
Nu u de configuratie stappen hebt voltooid, bent u klaar om certificaten te implementeren voor gebruikers en apparaten door certificaat profielen te maken en te implementeren. Zie [certificaat profielen maken](../../protect/deploy-use/create-certificate-profiles.md)voor meer informatie over het maken van certificaat profielen.  

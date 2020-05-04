---
title: Zelf studie&#58; co-beheer in te scha kelen voor Internet apparaten
titleSuffix: Configuration Manager
description: Meer informatie over het configureren van co-beheer voor nieuwe Windows 10-apparaten op internet met Configuration Manager en Microsoft Intune.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/12/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 7fb02a5c-e286-46b1-a972-6335c858429a
ms.openlocfilehash: 75016e8028dde29c83ae7e7f5a23a1f6dbb4417f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712713"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Zelf studie: co-beheer inschakelen voor nieuwe apparaten op Internet

Met co-beheer kunt u uw goed opgezette processen voor het gebruik van Configuration Manager voor het beheren van Pc's in uw organisatie. Terzelfder tijd bevestt u in de Cloud door intune te gebruiken voor beveiliging en moderne inrichting.

In deze zelf studie kunt u het co-beheer van Windows 10-apparaten instellen in een omgeving waarin u zowel Azure Active Directory (AD) als een on-premises AD gebruikt, maar geen [hybrid Azure Active Directory](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (AD) hebt. De Configuration Manager omgeving bevat één primaire site met alle site systeem rollen die zich op dezelfde server bevinden, de site server. Deze zelf studie begint met de locatie waar uw Windows 10-apparaten al zijn Inge schreven bij intune. 

Als u een hybride Azure AD hebt die uw on-premises AD verbindt met Azure AD, kunt u het beste de volgende aanvullende zelf studie [gebruiken om co-beheer in te scha kelen voor Configuration Manager-clients](tutorial-co-manage-clients.md).

Gebruik deze zelf studie wanneer:
  
- U hebt Windows 10-apparaten die u wilt meenemen in co-beheer. Deze apparaten zijn mogelijk ingericht via Windows auto pilot of zijn rechtstreeks afkomstig van uw OEM.
- U hebt Windows 10-apparaten op het Internet die u momenteel beheert met intune, waaraan u de Configuration Manager-client wilt toevoegen.

**In deze zelf studie doet u het volgende:**  
> [!div class="checklist"]  
> * Controleer de vereisten voor Azure en uw on-premises omgeving
> * Een openbaar SSL-certificaat voor de Cloud beheer gateway (CMG) aanvragen
> * Azure-Services inschakelen in Configuration Manager
> * Een Cloud beheer Gateway implementeren en configureren  
> * Het beheer punt en clients configureren voor het gebruik van de CMG
> * Co-beheer inschakelen in Configuration Manager
> * InTune configureren om de Configuration Manager-client te installeren

## <a name="prerequisites"></a>Vereisten  

### <a name="azure-services-and-environment"></a>Azure-Services en-omgeving

- Azure-abonnement ([gratis proef versie](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune-abonnement
  > [!TIP]  
  > Een Enter prise Mobility and Security (EMS)-abonnement omvat zowel Azure Active Directory Premium als Microsoft Intune. EMS-abonnement ([gratis proef versie](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

- InTune is geconfigureerd voor het [automatisch inschrijven van apparaten](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune)  

> [!TIP]
> U hoeft geen afzonderlijke intune-of EMS-licenties meer aan uw gebruikers te kopen en toe te wijzen. Zie [Veelgestelde vragen over producten en licenties](../core/understand/product-and-licensing-faq.md#bkmk_mem)voor meer informatie.

### <a name="on-premises-infrastructure"></a>Lokale infrastructuur

- Configuration Manager huidige vertakking versie 1810 of hoger.
  
  Versie 1810 introduceert [verbeterde http](../core/plan-design/hierarchy/enhanced-http.md), die in deze zelf studie wordt gebruikt om complexere PKI-vereisten te voor komen. Door gebruik te maken van verbeterde HTTP moet de primaire site die u gebruikt voor het beheren van clients worden geconfigureerd voor het gebruik van door Configuration Manager gegenereerde certificaten voor HTTP-site systemen.  

  Versie 1810 introduceert ook een eenvoudigere opdracht regel voor de installatie van de Configuration Manager-client op internet.

- De MDM-instantie moet worden ingesteld op intune  

### <a name="external-certificates"></a>Externe certificaten

- Certificaat voor CMG-Server verificatie. Dit certificaat is een SSL-certificaat van een open bare en algemeen vertrouwde certificaat provider. Bijvoorbeeld, maar niet beperkt tot, DigiCert, Thawte of VeriSign. U exporteert dit certificaat als. PFX-bestand met persoonlijke sleutel.  

- Verderop in deze zelf studie bieden we richt lijnen voor het configureren van de aanvraag voor dit certificaat.

### <a name="permissions"></a>Machtigingen

In deze zelf studie gebruikt u de volgende machtigingen om taken uit te voeren:

- Een account dat een *globale beheerder* is voor Azure Active Directory (Azure AD)
- Een account dat een *domein beheerder* is in uw on-premises infra structuur  
- Een account dat een *volledige beheerder* is voor *alle* bereiken in Configuration Manager

## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Een openbaar certificaat voor de Cloud beheer gateway aanvragen

Als uw apparaten zijn verbonden met het Internet, vereist co-beheer de Configuration Manager CMG (Cloud Management Gateway). Met de CMG kunnen uw op internet gebaseerde Windows 10-apparaten communiceren met uw on-premises Configuration Manager-implementatie. Voor de CMG is een SSL-certificaat vereist om een vertrouwens relatie tussen apparaten en uw Configuration Manager omgeving tot stand te brengen.

In deze zelf studie wordt een openbaar certificaat met de naam **CMG Server-verificatie certificaat** gebruikt dat de autoriteit afleidt van een algemeen vertrouwde certificaat provider. Hoewel het mogelijk is om co-beheer te configureren met behulp van certificaten die toestemming van uw on-premises micro soft-certificerings instantie afleiden, is het gebruik van zelfondertekende certificaten buiten het bereik van deze zelf studie.

Het **CMG-Server verificatie certificaat** wordt gebruikt voor het versleutelen van het communicatie verkeer tussen de Configuration Manager-client en de CMG. Het certificaat traceert terug naar een vertrouwde basis om de identiteit van de server naar de client te verifiëren. Het open bare certificaat bevat een vertrouwde basis die Windows-clients al vertrouwen.

Over dit certificaat: 

- U identificeert een unieke naam voor uw CMG-service in Azure en geeft die naam op in uw certificaat aanvraag.  
- U genereert uw certificaat aanvraag op een specifieke server en verzendt de aanvraag vervolgens naar een open bare certificaat provider om het benodigde SSL-certificaat te verkrijgen.  
- U importeert naar het systeem dat de aanvraag heeft gegenereerd het certificaat dat u hebt ontvangen van de provider. U gebruikt dezelfde computer voor het exporteren van het certificaat voor gebruik wanneer u later de CMG implementeert in Azure.  
- Wanneer de CMG wordt geïnstalleerd, wordt er een CMG-service in azure gemaakt met behulp van de naam die u in het certificaat hebt opgegeven.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Een unieke naam voor uw Cloud beheer gateway in azure identificeren

Wanneer u het CMG Server-verificatie certificaat aanvraagt, geeft u aan wat een unieke naam moet zijn om uw *Cloud service (klassiek)* in azure te identificeren. De open bare Azure-Cloud maakt standaard gebruik van *cloudapp.net*en de CMG wordt in het cloudapp.net-domein gehost als * \<YourUniqueDnsName>. cloudapp.net*.  

> [!TIP]  
> In deze zelf studie gebruikt het **certificaat voor CMG-Server verificatie** een FQDN die eindigt op *contoso.com*.  Nadat we de CMG hebben gemaakt, configureren we een canonieke naam record (CNAME) in de open bare DNS van de organisatie. Met deze record wordt een alias gemaakt voor de CMG die wordt toegewezen aan de naam die wordt gebruikt in het open bare certificaat.  

Controleer voordat u uw open bare certificaat aanvraagt of de naam die u wilt gebruiken, beschikbaar is in Azure. U maakt de service niet rechtstreeks in Azure. In plaats daarvan wordt de naam die is opgegeven in het open bare certificaat dat u hebt aangevraagd, gebruikt door Configuration Manager om de Cloud service te maken wanneer u de CMG installeert.  

1. Meld u aan bij de [Microsoft Azure-Portal](https://portal.azure.com/).  

2. Selecteer **een resource maken**, kies de categorie **berekening** en selecteer vervolgens **Cloud service**. De pagina Cloud service (klassiek) wordt geopend.

3. Voor de **DNS-naam**geeft u de naam van het voor voegsel op voor de Cloud service die u gaat gebruiken. Dit voor voegsel moet hetzelfde zijn als de waarde die u later gebruikt bij het aanvragen van een publicatie certificaat voor het certificaat voor CMG-Server verificatie. We gebruiken *MyCSG*om de naam ruimte van *MyCSG.cloudapp.net*te maken. De interface bevestigt of de naam beschikbaar is of al door een andere service wordt gebruikt.  
 Nadat u hebt gecontroleerd of de naam die u wilt gebruiken, beschikbaar is, kunt u de aanvraag voor certificaat ondertekening (CSR) indienen.

### <a name="request-the-certificate"></a>Het certificaat aanvragen

Gebruik de volgende informatie om een aanvraag voor certificaat ondertekening voor uw CMG in te dienen bij een open bare certificaat provider. Wijzig de volgende waarden zodat deze relevant zijn voor uw omgeving.  

- *MyCMG* voor het identificeren van de service naam van de Cloud beheer gateway
- *Contoso* als bedrijfs naam
- *Contoso.com* als het open bare domein

U wordt aangeraden om de server van de primaire site te gebruiken om de aanvragen voor certificaat ondertekening (CSR) te genereren. Wanneer u het certificaat ontvangt, moet u dit registreren op dezelfde server die de CSR heeft gegenereerd of u kunt de persoonlijke sleutel certificaten niet exporteren. deze is vereist.  

Vraag een provider type van versie 2 aan wanneer u een CSR genereert. Alleen certificaten van versie 2 worden ondersteund.  

> [!TIP]  
> Wanneer we de CMG implementeren, zullen we ook een Cloud distributiepunt (CDP) tegelijkertijd installeren. Wanneer u bijvoorbeeld een CMG implementeert, kan de optie **CMG als een Cloud distributiepunt functioneren en inhoud van Azure Storage verwerken** worden geselecteerd. Als u de CDP op de server met de CMG, verwijdert u de nood zaak voor afzonderlijke certificaten en configuraties om de CDP te ondersteunen. Hoewel de CDP niet vereist is voor het gebruik van co-beheer, is het nuttig in de meeste omgevingen.  
>
> Als u aanvullende Cloud distributiepunten voor co-beheer wilt gebruiken, moet u afzonderlijke certificaten aanvragen voor elke extra server. Als u een openbaar certificaat voor de CDP wilt aanvragen, gebruikt u dezelfde Details als voor de CSR van de Cloud beheer gateway. U hoeft alleen de algemene naam te wijzigen zodat deze uniek is voor elke CDP.  

#### <a name="details-for-the-cloud-management-gateway-csr"></a>Details voor de CSR van de Cloud beheer gateway

- **Algemene naam**: CloudServiceNameCMG.YourCompanyPubilcDomainName.com  
Voor beeld: MyCSG.contoso.com  
- **Alternatieve naam voor onderwerp**: hetzelfde als de algemene naam (CN)  
- **Organisatie**: de naam van uw organisatie  
- **Afdeling**: per organisatie  
- **Plaats**: per organisatie  
- **Status**: per organisatie  
- **Land**: per organisatie  
- **Sleutel grootte: 2048**  
- **Provider: micro soft RSA SChannel Cryptographic Provider**  

### <a name="import-the-certificate"></a>Het certificaat importeren

Nadat u het open bare certificaat hebt ontvangen, importeert u het in het lokale certificaat archief van de computer die de CSR heeft gemaakt. Exporteer het certificaat vervolgens als een. PFX-bestand zodat u het kunt gebruiken voor uw CMG in Azure.  

Providers van open bare certificaten bevatten doorgaans instructies voor het importeren van het certificaat. Het proces voor het importeren van het certificaat moet er als volgt uitzien:  

1. Zoek het pfx-bestand van het certificaat op de computer waarop het certificaat moet worden geïmporteerd.  

2. Klik met de rechter muisknop op het bestand en selecteer vervolgens **PFX installeren**  

3. Wanneer de wizard Certificaat importeren wordt gestart, selecteert u **volgende**.  

4. Selecteer **volgende**op de pagina **te importeren bestand** .

5. Op de pagina **wacht** woord voert u het wacht woord voor de persoonlijke sleutel in het vak wacht woord in en selecteert u **volgende**.  
  
   Selecteer de optie om de sleutel exporteerbaar te maken.

6. Kies op de **pagina certificaat archief** **automatisch het certificaat archief selecteren op basis van het type certificaat**en selecteer vervolgens **volgende**.  

7. Selecteer **Finish**.

### <a name="export-the-certificate"></a>Het certificaat exporteren

Exporteer het *certificaat voor CMG-Server verificatie* van uw server. Als u het certificaat opnieuw exporteert, is het bruikbaar voor uw Cloud beheer gateway in Azure.  

1. Op de server waarop u het open bare SSL-certificaat hebt geïmporteerd, voert u **certlm. msc** uit om de Certificate Manager-console te openen.  

2. Selecteer in de Certificate Manager-console **persoonlijke > certificaten**. Klik vervolgens met de rechter muisknop op het *certificaat voor CMG-Server verificatie* dat u in de vorige procedure hebt geregistreerd en selecteer vervolgens **alle taken > exporteren**.  

3. Selecteer in de wizard Certificaat exporteren de optie **volgende**, selecteer **Ja, de persoonlijke sleutel exporteren**en vervolgens op **volgende**.  

4. Selecteer op de pagina bestands indeling voor export de optie **Personal Information Exchange-PKCS #12 (. PFX)**, selecteer **volgende**en geef een wacht woord op. Geef bij bestands naam een naam op zoals **C:\ConfigMgrCloudMGServer**. U verwijst naar dit bestand wanneer u de CMG maakt in Azure.  

5. Selecteer **volgende**en bevestig de volgende instellingen voordat u **volt ooien** selecteert om het exporteren te volt ooien:  

   - Sleutels exporteren = Ja  
   - Alle certificaten in het certificeringspad toevoegen = Ja  
   - Bestands indeling = Personal Information Exchange (*. pfx)  

6. Nadat u de export bewerking hebt voltooid, gaat u naar het. pfx-bestand en plaatst u een kopie ervan in **C:\Certs** op de primaire site server van Configuration Manager waarmee clients op internet worden beheerd. De map certs is een tijdelijke map die moet worden gebruikt bij het verplaatsen van certificaten tussen servers. U hebt toegang tot het certificaat bestand vanaf de primaire site server wanneer u de Cloud beheer gateway in azure implementeert.  

Nadat u het certificaat naar de primaire site server hebt gekopieerd, kunt u het certificaat uit het persoonlijke certificaat archief op de lidserver verwijderen.

## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Azure Cloud Services inschakelen in Configuration Manager

Als u Azure-Services vanuit de Configuration Manager-console wilt configureren, gebruikt u de wizard Azure-Services configureren en maakt u twee Azure Active Directory (Azure AD)-apps.  

- **Server-app** : een *Web-app* in azure AD  
- **Client-app** : een *systeem eigen client* -app in azure AD  

Voer de volgende procedure uit vanaf de primaire site server.  

1. Open op de primaire site server de Configuration Manager-console en ga naar **beheer > Cloud Services > Azure-Services**en selecteer **Azure-Services configureren**.  

   Geef op de pagina Azure-service configureren een beschrijvende naam op voor de Cloud beheer service die u wilt configureren. Bijvoorbeeld: *mijn Cloud beheer service*.

   Selecteer vervolgens **Cloud beheer**en selecteer vervolgens **volgende**.  

   > [!TIP]  
   > Zie [de wizard Azure-Services starten](../core/servers/deploy/configure/Azure-services-wizard.md#start-the-azure-services-wizard) voor meer informatie over de configuraties die u in de wizard maakt

2. Selecteer op de pagina **App-eigenschappen** voor **Web**-app **Bladeren** om het dialoog venster **server-app** te openen en selecteer vervolgens **maken**. Configureer de volgende velden:

   - **Toepassings naam**: Geef een beschrijvende naam op voor de app, zoals de *Web-app voor Cloud beheer*.  

   - **URL van start pagina**: deze waarde wordt niet gebruikt door Configuration Manager, maar is vereist voor Azure AD. Deze waarde is `https://ConfigMgrService`standaard ingesteld op.  

   - **App-ID-URI**: deze waarde moet uniek zijn in uw Azure AD-Tenant. Het bevindt zich in het toegangs token dat door de Configuration Manager-client wordt gebruikt om toegang tot de service aan te vragen. Deze waarde is `https://ConfigMgrService`standaard ingesteld op.  

   Selecteer vervolgens **Aanmelden**en geef een Azure AD Global Administrator-account op. Deze referenties worden niet opgeslagen door Configuration Manager. Deze persoon heeft geen machtigingen nodig in Configuration Manager en hoeft niet hetzelfde account te zijn dat de wizard Azure-Services uitvoert.

   Nadat u zich hebt aangemeld, worden de resultaten weer gegeven. Selecteer **OK** om het dialoog venster Server toepassing maken te sluiten en terug te keren naar de pagina app-eigenschappen.

3. Voor **native client-app**selecteert u **Bladeren** om het dialoog venster **client-app** te openen.

4. Selecteer **maken** om het dialoog venster **client toepassing maken** te openen en configureer vervolgens de volgende velden:  

   - **Toepassings naam**: Geef een beschrijvende naam op voor de app, zoals de *systeem eigen client-app voor Cloud beheer*.

   - **Antwoord-URL**: deze waarde wordt niet gebruikt door Configuration Manager, maar is vereist voor Azure AD. Deze waarde is `https://ConfigMgrClient`standaard ingesteld op.
   Selecteer vervolgens **Aanmelden**en geef een Azure AD Global Administrator-account op. Net als de web-app worden deze referenties niet opgeslagen en zijn er geen machtigingen vereist in Configuration Manager.

   Nadat u zich hebt aangemeld, worden de resultaten weer gegeven. Selecteer **OK** om het dialoog venster client toepassing maken te sluiten en terug te keren naar de pagina app-eigenschappen. Selecteer vervolgens **volgende** om door te gaan.

5. Schakel op de pagina **detectie-instellingen configureren** het selectie vakje **Azure Active Directory gebruikers detectie inschakelen**in, selecteer **volgende**en voltooi vervolgens de configuratie van de detectie dialoogvensters voor uw omgeving.  

6. Ga door met de samen vatting, voortgang en de voltooiings pagina's en sluit de wizard.  

   Azure-Services voor Azure AD-gebruikers detectie is nu ingeschakeld in Configuration Manager.  Houd de console nu geopend.  

7. Open een browser en meld u aan bij de [Azure Portal](https://portal.azure.com/).  

8. Selecteer **alle services > Azure Active Directory > app-registraties**en voer vervolgens de volgende handelingen uit:

   1. Selecteer de web-app die u hebt gemaakt.

   2. Ga naar **instellingen > vereiste machtigingen**, selecteer **machtigingen verlenen**en selecteer vervolgens **Ja**.  

   3. Selecteer de systeem eigen client-app die u hebt gemaakt.

   4. Ga naar **instellingen > vereiste machtigingen**, selecteer **machtigingen verlenen**en selecteer vervolgens **Ja**.  

9. Ga in de Configuration Manager-console naar **beheer > overzicht > Cloud Services > Azure-Services**en selecteer uw Azure-service. Klik vervolgens met de rechter muisknop op **Azure Active Directory gebruiker Discover** en selecteer **nu volledige detectie uitvoeren**. Selecteer **Ja** om de actie te bevestigen.  

10. Open op de primaire site server de Configuration Manager **SMS_AZUREAD_DISCOVERY_AGENT. log** en zoek de volgende vermelding om te bevestigen dat de detectie werkt: de *UDX voor Azure Active Directory gebruikers is gepubliceerd*  

    Het logboek bestand bevindt zich standaard in *% Program_Files% \ micro soft Configuration Manager\Logs*.  

## <a name="create-the-cloud-services-in-azure"></a>Cloud Services maken in azure

**In deze sectie van de zelf studie doet u het**volgende:

- De CMG-Cloud service maken  
- DNS CNAME-records maken voor beide services  

### <a name="create-the-cmg"></a>De CMG maken

Gebruik deze procedure voor het installeren van een Cloud beheer gateway als een service in Azure. De CMG wordt geïnstalleerd op de site op het hoogste niveau van de hiërarchie. In deze zelf studie blijven we de primaire site gebruiken waar certificaten zijn Inge schreven en geëxporteerd.

1. Open op de primaire site server de Configuration Manager-console, ga naar **beheer > overzicht > Cloud Services > cloudbeheergateway**en selecteer vervolgens **cloudbeheergateway maken**.  

2. Op de pagina **Algemeen**:  

   1. Selecteer uw cloud omgeving voor **Azure-omgeving**. In deze zelf studie wordt gebruikgemaakt van **AzurePublicCloud**.  

   2. Selecteer **Azure Resource Manager-implementatie**.  
  
   3. **Meld** u aan bij uw Azure-abonnement. Configuration Manager vult aanvullende informatie op basis van de informatie die u hebt geconfigureerd tijdens het inschakelen van Azure Cloud Services voor Configuration Manager.  

   Selecteer **Volgende** om door te gaan.  

3. Blader op de pagina **instellingen** naar en selecteer het bestand met de naam **ConfigMgrCloudMGServer. pfx.** dit is het bestand dat u hebt geëxporteerd na het importeren van het certificaat voor de CMG-Server verificatie. Nadat u het wacht woord hebt opgegeven, wordt de naam van de **service** en de **implementatie** automatisch ingevuld op basis van de details in het pfx-certificaat bestand.

4. Stel uw **regio**in.

5. Voor **resource groep**gebruikt u een bestaande resource groep of maakt u een groep met een beschrijvende naam die geen spaties gebruikt, zoals **CofigMgrCloudServices**. Als u ervoor kiest om een groep te maken, wordt de groep toegevoegd als een resource groep in Azure.  

6. Tenzij u klaar bent om op schaal te configureren, gebruikt u een (1) voor het aantal **VM-exemplaren**. Met het aantal VM-exemplaren kan één cloudbeheergateway (CMG) Cloud service uitschalen om meer client verbindingen te ondersteunen. Later kunt u de Configuration Manager-console gebruiken om het aantal VM-exemplaren dat u gebruikt, te retour neren en te bewerken.  

7. Schakel het selectie vakje in om het **intrekken van client certificaten te controleren**.

8. Schakel het selectie vakje voor **toestaan dat CMG als een Cloud distributiepunt werkt en inhoud van Azure Storage te leveren** als u een Cloud distributiepunt wilt implementeren met de CMG.

9. Selecteer **Volgende** om door te gaan.

10. Controleer de waarden op de pagina **waarschuwing** en selecteer **volgende**.

11. Controleer de pagina **samen vatting** en klik op **volgende** om de Cloud beheer gateway-Cloud service te maken. Selecteer **sluiten** om de wizard te volt ooien.  

12. In het knoop punt cloudbeheergateway van de Configuration Manager-console kunt u nu de nieuwe service weer geven.  

### <a name="create-dns-cname-records"></a>DNS CNAME-records maken

Wanneer u een DNS-vermelding voor de CMG maakt, kunt u ervoor zorgen dat uw Windows 10-apparaten zowel binnen als buiten uw bedrijfs netwerk naam omzetting gebruiken om de CMG-Cloud service in azure te vinden.

In het voor beeld van de CNAME-record worden de volgende details gebruikt:  

- De bedrijfs naam is **Contoso** met een open bare DNS-naam ruimte van ***contoso.com***.  

- De CMG-service naam is **MyCMG**, die wordt ***MyCMG.CloudApp.net*** in Azure.  

CNAME-record voorbeeld: *MyCMG.contoso.com => my.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Het beheer punt en clients configureren voor het gebruik van de CMG

Instellingen configureren waarmee on-premises beheer punten en-clients de Cloud beheer gateway kunnen gebruiken.

Omdat we uitgebreide HTTP voor client communicatie gebruiken, is het niet nodig om een HTTPS-beheer punt te gebruiken.  

### <a name="create-the-cmg-connection-point"></a>Het CMG-verbindings punt maken

Configureer de site ter ondersteuning van verbeterde HTTP.  

1. Ga in de Configuration Manager-console naar **beheer > overzicht > site configuratie > sites**en open de eigenschappen van de primaire site.  

2. Op het tabblad **communicatie client computer** selecteert u de *https-of http-* optie voor het gebruik van door **Configuration Manager gegenereerde certificaten voor http-site systemen**en selecteert u vervolgens **OK** om de configuratie op te slaan.

    > [!Note]
    > Vanaf versie 1906 wordt dit tabblad **communicatie beveiliging**genoemd.<!-- SCCMDocs#1645 -->  

3. Ga nu naar **beheer > overzicht > site configuratie > servers en site systeem rollen** en selecteer de server met een beheer punt waarop u het verbindings punt van de Cloud beheer gateway wilt installeren.  

4. Selecteer **site systeem rollen toevoegen** **en vervolgens**> **Next**volgende.  

5. Selecteer het **verbindings punt van de Cloud beheer gateway** en selecteer **volgende** om door te gaan.  

6. Controleer de standaard selecties op de pagina **verbindings punt van de Cloud beheer gateway** en controleer of de juiste CMG is geselecteerd. Als u meerdere Cloud beheer gateways hebt, kunt u de vervolg keuzelijst gebruiken om een andere CMG op te geven. U kunt na de installatie ook de CMG wijzigen die in gebruik is. Selecteer **Volgende** om door te gaan.

7. Selecteer **volgende** om de installatie te starten en Bekijk de resultaten op de pagina voltooiing.  Selecteer **sluiten** om de installatie van het verbindings punt te volt ooien.

8. Ga nu naar **beheer > overzicht > site configuratie > servers en site systeem rollen** en open de **Eigenschappen** voor het beheer punt waarop u het verbindings punt hebt geïnstalleerd. Schakel op het tabblad **Algemeen** het selectie vakje **Configuration Manager verkeer van de Cloud beheer gateway toestaan**in en selecteer **OK** om de configuratie op te slaan.
   > [!TIP]  
   > Hoewel het niet vereist is om co-beheer in te scha kelen, wordt u aangeraden dezelfde bewerking te maken voor software-update punten.

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>Client instellingen configureren om clients te leiden om de CMG te gebruiken

Gebruik client instellingen om Configuration Manager-clients te configureren om te communiceren met de CMG.  

1. Open de **Configuration Manager-console > beheer > overzicht > client instellingen**en bewerk vervolgens de **standaard client instellingen**.  

2. Selecteer **Cloud Services**.

3. Stel op de pagina **standaard instellingen** de volgende instellingen in op = **Ja**.  

   - **Automatisch nieuwe aan Windows 10-domein gekoppelde apparaten registreren met Azure Active Directory**  

   - **Clients inschakelen om een Cloud beheer gateway te gebruiken**

   - **Toegang tot Cloud distributiepunt toestaan**

4. Stel op de pagina **client beleid**  =  **gebruikers beleids aanvragen van internetclients inschakelen in****Ja**.

5. Selecteer **OK** om deze configuratie op te slaan.

## <a name="enable-co-management-in-configuration-manager"></a>Co-beheer inschakelen in Configuration Manager

Met de Azure-configuraties, site systeem rollen en client instellingen op locatie kunt u Configuration Manager configureren om co-beheer in te scha kelen. U moet echter nog steeds enkele configuraties in intune maken nadat u co-beheer hebt ingeschakeld voordat deze zelf studie is voltooid. Een van deze taken is het configureren van intune voor het implementeren van de Configuration Manager-client. Deze taak wordt eenvoudiger gemaakt door de opdracht regel op te slaan voor client implementatie die beschikbaar is in de wizard voor co-beheer configuratie. Daarom scha kelen we nu co-beheer in, voordat we de configuraties voor intune volt ooien.

> [!TIP]
> - Als u co-beheer inschakelt, wijst u een verzameling toe als een *test groep*. Dit is een groep die een klein aantal clients bevat om uw configuraties voor co-beheer te testen. We raden u aan een geschikte verzameling te maken voordat u de procedure start. Vervolgens kunt u die verzameling selecteren zonder de procedure te verlaten.
> - Vanaf Configuration Manager versie 1906 hebt u mogelijk meerdere verzamelingen nodig omdat u voor elke werk belasting een andere *test groep* kunt toewijzen.

### <a name="enable-co-management-starting-in-version-1906"></a>Co-beheer inschakelen vanaf versie 1906

Als u co-beheer vanaf Configuration Manager versie 1906 wilt inschakelen, volgt u de onderstaande instructies:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Co-beheer inschakelen in versie 1902 en lager

Volg de onderstaande instructies om co-beheer in te scha kelen voor Configuration Manager versie 1902 en eerder:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>InTune gebruiken om de Configuration Manager-client te implementeren

U kunt intune gebruiken om de Configuration Manager-client te installeren op Windows 10-apparaten die momenteel alleen worden beheerd met intune.  

Wanneer een eerder niet-beheerd Windows 10-apparaat wordt geregistreerd bij intune, wordt de Configuration Manager-client automatisch geïnstalleerd.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Een intune-app maken om de Configuration Manager-client te installeren

1. Meld u vanaf de primaire site server aan bij de [Azure Portal](https://portal.azure.com/) en ga naar de **intune-> Client-apps > apps > toevoegen**.

2. Voor **app-type**: Selecteer **line-of-Business-app**.

3. Selecteer **app-pakket bestand**, blader naar de locatie van het Configuration Manager bestand **ccmsetup. msi**en selecteer vervolgens **openen > OK**.
Bijvoorbeeld: *C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*

4. Selecteer **app-gegevens**en geef vervolgens de volgende gegevens op:
   - **Beschrijving**: Configuration Manager-client  

   - **Uitgever**: micro soft  

   - **Opdracht regel argumenten**: * \<Geef de **CCMSETUPCMD** -opdracht regel op. U kunt de opdracht regel gebruiken die u hebt opgeslagen op de* *pagina activering van de wizard voor het configureren van co-beheer. Deze opdracht regel bevat de namen van uw Cloud service en aanvullende waarden waarmee apparaten de Configuration Manager-client software kunnen installeren. >*  

     De opdracht regel structuur moet er als volgt uitzien in dit voor beeld met alleen de para meters CCMSETUPCMD en SMSSiteCode:  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > Als u de opdracht regel niet beschikbaar hebt, kunt u de eigenschappen van *CoMgmtSettingsProd* weer geven in de console van Configuration Manager om een kopie van de opdracht regel op te halen.

5. Selecteer **OK > toevoegen**.  De app wordt gemaakt en wordt beschikbaar in de intune-console. Nadat de app beschikbaar is, kunt u de volgende sectie gebruiken om intune te configureren om deze toe te wijzen aan Windows 10-apparaten.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>De intune-app toewijzen voor het installeren van de Configuration Manager-client

De volgende procedure implementeert de app voor het installeren van de Configuration Manager-client die u in de vorige procedure hebt gemaakt.

1. Meld u aan bij de [Azure-portal](https://portal.azure.com/).  Selecteer **alle services > intune-> client-apps > apps**en selecteer vervolgens **Boots trap client installeren**de app die u hebt gemaakt om de Configuration Manager-client te implementeren.  

2. Selecteer **toewijzingen > groep toevoegen**.  Stel **toewijzings type** in als **vereist**en gebruik vervolgens **opgenomen groepen** en **uitgesloten groepen** om de Azure Active Directory (AD) groepen in te stellen met gebruikers en apparaten die u wilt deel nemen aan co-beheer.  

3. Selecteer **OK** en **Sla** de configuratie op.
De app is nu vereist voor gebruikers en apparaten waaraan u deze hebt toegewezen. Nadat de app de Configuration Manager-client op een apparaat heeft geïnstalleerd, wordt deze beheerd door co-beheer.

## <a name="summary"></a>Samenvatting

Nadat u de configuratie stappen van deze zelf studie hebt voltooid, kunt u uw apparaten gezamenlijk beheren.

## <a name="next-steps"></a>Volgende stappen

- Bekijk de status van gezamenlijk beheerde apparaten met het [dash board voor co-beheer](how-to-monitor.md)
- [Windows auto pilot](quickstart-autopilot.md) gebruiken om nieuwe apparaten in te richten
- [Voorwaardelijke toegang](quickstart-conditional-access.md) en intune-nalevings regels gebruiken voor het beheren van de gebruikers toegang tot bedrijfs resources

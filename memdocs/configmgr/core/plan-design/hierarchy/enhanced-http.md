---
title: Verbeterde HTTP
titleSuffix: Configuration Manager
description: Gebruik moderne verificatie om client communicatie te beveiligen zonder dat PKI-certificaten nodig zijn.
ms.date: 03/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb14830e99600da1b71c516a44d51a0090cdc673
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720175"
---
# <a name="enhanced-http"></a>Verbeterde HTTP

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1356889,1358460-->

> [!Tip]  
> Deze functie werd voor het eerst in versie 1806 geïntroduceerd als een [voorlopige functie](../../servers/manage/pre-release-features.md). Vanaf versie 1810 is deze functie niet langer een functie van de voorlopige versie.  

Micro soft raadt u aan om HTTPS-communicatie te gebruiken voor alle Configuration Manager communicatie paden, maar het is lastig voor sommige klanten vanwege de overhead van het beheer van PKI-certificaten.

Configuration Manager versie 1806 bevat verbeteringen in de manier waarop clients communiceren met site systemen. Er zijn twee primaire doelen voor deze verbeteringen:  

- U kunt gevoelige client communicatie beveiligen zonder dat er PKI-Server verificatie certificaten nodig zijn.  

- Clients hebben veilig toegang tot inhoud vanaf distributie punten zonder dat hiervoor een netwerk toegangs account, client-PKI-certificaat en Windows-verificatie nodig zijn.  

Alle andere client communicatie is via HTTP. Verbeterde HTTP is niet hetzelfde als HTTPS inschakelen voor client communicatie of een site systeem.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> PKI-certificaten zijn nog steeds een geldige optie voor klanten die aan de volgende vereisten voldoen:  
>
> - Alle client communicatie overschrijdt HTTPS  
> - Geavanceerd beheer van de infra structuur voor ondertekening
>
> Als u al gebruikmaakt van PKI, wordt het PKI-certificaat dat is gebonden in IIS, ook gebruikt als verbeterde HTTP is ingeschakeld.



## <a name="scenarios"></a><a name="bkmk_scenario"></a>Denkbaar

De volgende scenario's profiteren van deze verbeteringen:  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a>Scenario 1: client naar beheer punt

<!--1356889-->
[Apparaten die zijn toegevoegd aan Azure Active Directory (Azure AD)](/azure/active-directory/devices/concept-azure-ad-join) kunnen communiceren met een beheer punt dat is geconfigureerd voor http. De site server genereert een certificaat voor het beheer punt zodat het kan communiceren via een beveiligd kanaal.

> [!Note]  
> Dit gedrag is gewijzigd ten opzichte van Configuration Manager 1802 versie van de huidige vertakking, waarvoor een HTTPS-ingeschakeld beheer punt is vereist voor Azure AD-gekoppelde clients die communiceren via een Cloud beheer gateway. Zie [beheer punt voor HTTPS inschakelen](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)voor meer informatie.  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a>Scenario 2: client naar distributie punt

<!--1358228-->
Een client die lid is van een AD-machine of een klant die deelneemt aan Azure, kan inhoud verifiëren en downloaden via een beveiligd kanaal van een distributie punt dat is geconfigureerd voor HTTP. Deze typen apparaten kunnen ook inhoud verifiëren en downloaden vanaf een distributie punt dat is geconfigureerd voor HTTPS zonder dat hiervoor een PKI-certificaat is vereist op de client. Het is lastig om een certificaat voor client verificatie toe te voegen aan een werk groep of een client die lid is van Azure AD.

Dit gedrag omvat implementatie scenario's voor besturings systemen met een taken reeks die wordt uitgevoerd vanaf opstart media, PXE of software Center. Zie [netwerk toegangs account](accounts.md#network-access-account)voor meer informatie.<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a>Scenario 3: Azure AD-apparaat-id

<!--1358460-->
Een Azure AD-of [Hybrid Azure AD-apparaat](/azure/active-directory/devices/concept-azure-ad-join-hybrid) zonder een aangemelde Azure AD-gebruiker kan veilig communiceren met de toegewezen site. De identiteit van het apparaat in de Cloud is nu voldoende om te verifiëren bij de CMG en het beheer punt voor op het apparaat gerichte scenario's. (Er is nog een gebruikers token vereist voor gebruikers gerichte scenario's.)  


## <a name="features"></a>Functies

De volgende Configuration Manager functies ondersteunen of vereisen verbeterde HTTP:

- [Cloudbeheergateway](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Implementatie van het besturings systeem zonder een netwerk toegangs account](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [Co-beheer inschakelen voor nieuwe Windows 10-apparaten die zijn gebaseerd op Internet](../../../comanage/tutorial-co-manage-new-devices.md)
- [App-goed keuringen via e-mail](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [Beheer service](../../../develop/adminservice/overview.md)
- [Recent verbonden consoles weer geven](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> Het software-update punt en de bijbehorende scenario's bevatten altijd het beveiligde HTTP-verkeer met clients en de Cloud beheer gateway. Er wordt gebruikgemaakt van een mechanisme met het beheer punt dat verschilt van verificatie op basis van certificaten of tokens.<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>Vereisten  

- Een beheer punt dat is geconfigureerd voor HTTP-client verbindingen. Stel deze optie in op het tabblad **Algemeen** van de eigenschappen van de beheer punt rollen.  

- Een distributie punt dat is geconfigureerd voor HTTP-client verbindingen. Stel deze optie in op het tabblad **communicatie** van de eigenschappen van het distributie punt. Schakel de optie niet in om **toe te staan dat clients anoniem verbinding maken**.  

- Onboarding van de site naar Azure AD voor Cloud beheer.  

    - Als u al aan deze vereiste voor uw site hebt voldaan, moet u de Azure AD-toepassing bijwerken. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer **Azure Active Directory tenants**. Selecteer de Azure AD-Tenant, selecteer de webtoepassing in het deel venster **toepassingen** en selecteer vervolgens **toepassings instelling bijwerken** in het lint.  

- *Alleen voor [scenario 3](#bkmk_scenario3) *: een client met Windows 10 versie 1803 of hoger en is gekoppeld aan Azure AD. Voor de client is deze configuratie vereist voor de verificatie van Azure AD-apparaten.<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>De site configureren

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** . Selecteer de site en kies **Eigenschappen** in het lint.  

2. Schakel over naar het tabblad **communicatie client computer** .

    > [!Note]
    > Vanaf versie 1906 wordt dit tabblad **communicatie beveiliging**genoemd.<!-- SCCMDocs#1645 -->  

    Selecteer de optie voor **https of http**. Schakel vervolgens de optie voor het **gebruik van door Configuration Manager gegenereerde certificaten voor HTTP-site systemen**.

> [!Tip]
> Wacht tot 30 minuten op het beheer punt om het nieuwe certificaat van de site te ontvangen en te configureren.

<!--3798957-->
Vanaf versie 1902 kunt u ook Enhanced HTTP inschakelen voor de centrale beheer site. Gebruik hetzelfde proces en open de eigenschappen van de centrale beheer site. Met deze actie wordt alleen uitgebreide HTTP ingeschakeld voor de SMS-provider functies op de centrale beheer site. Het is geen globale instelling die van toepassing is op alle sites in de hiërarchie.

U kunt deze certificaten bekijken in de Configuration Manager-console. Ga naar de werk ruimte **beheer** , vouw **beveiliging**uit en selecteer het knoop punt **certificaten** . Zoek naar het basis certificaat van de **SMS-uitgifte** en de certificaten van de site server functie die zijn uitgegeven door de SMS-uitgevende basis.

Zie [communicatie van clients naar site systemen en-services](communications-between-endpoints.md#Planning_Client_to_Site_System)voor meer informatie over hoe de client communiceert met het beheer punt en distributie punt met deze configuratie.


## <a name="see-also"></a>Zie ook

- [De beveiliging plannen](../security/plan-for-security.md)  

- [Beveiliging en privacy voor Configuration Manager-clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Beveiliging configureren](../security/configure-security.md)  

- [Communicatie tussen eind punten](communications-between-endpoints.md)  

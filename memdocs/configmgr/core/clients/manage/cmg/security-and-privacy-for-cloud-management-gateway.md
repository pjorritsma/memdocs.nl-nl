---
title: CMG beveiliging en privacy
titleSuffix: Configuration Manager
description: Meer informatie over richt lijnen en aanbevelingen voor beveiliging en privacy met de Cloud beheer gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: 93427cb34b2216bf16f713818481e69573a4b0de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712888"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Beveiliging en privacy voor de Cloud beheer gateway

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat beveiligings-en privacy-informatie voor de Configuration Manager Cloud Management Gateway (CMG). Zie voor meer informatie [plannen voor Cloud beheer gateway](plan-cloud-management-gateway.md).

## <a name="cmg-security-details"></a>CMG-beveiligings Details

- De CMG accepteert en beheert verbindingen van CMG-verbindings punten. Hierbij wordt gebruikgemaakt van wederzijdse SSL-verificatie met behulp van certificaten en verbindings-Id's.
- De CMG accepteert en stuurt client aanvragen via de volgende methoden:
    - Verifieert verbindingen met wederzijdse SSL met het client verificatie certificaat op basis van PKI of Azure AD.
      - IIS op de CMG-VM-instanties verifieert het certificaatpad op basis van het vertrouwde basis certificaat (en) dat is geüpload naar de CMG.
      - IIS in het VM-exemplaar verifieert ook het intrekken van client certificaten, indien ingeschakeld. Zie voor meer informatie [de certificaatintrekkingslijst publiceren](#bkmk_crl).
    - De certificaat vertrouwens lijst controleert de hoofdmap van het certificaat voor client verificatie. Ook wordt dezelfde validatie uitgevoerd als het beheer punt voor de client. Zie [controle vermeldingen in de certificaat vertrouwens lijst van de site](#bkmk_ctl)voor meer informatie.
    - Valideert en filtert client aanvragen (Url's) om te controleren of een CMG-verbindings punt de aanvraag kan verwerken.  
    - Controleert de lengte van de inhoud voor elk publicatie-eind punt.
    - Maakt gebruik van Round Robin-gedrag voor het verdelen van CMG-verbindings punten in dezelfde site.
- Het CMG-verbindings punt maakt gebruik van de volgende methoden:
    - Bouwt consistente HTTPS/TCP-verbindingen met alle VM-exemplaren van de CMG. Deze verbindingen worden elke minuut gecontroleerd en onderhouden.
    - Maakt gebruik van wederzijdse SSL-verificatie met de CMG met behulp van certificaten.
    - Client aanvragen worden doorgestuurd op basis van URL-toewijzingen.
    - Rapporteert verbindings status om de status van de service status weer te geven in de-console.
    - Rapporteert het verkeer per eind punt om de vijf minuten.

### <a name="configuration-manager-client-facing-roles"></a>Client gerichte rollen Configuration Manager

De host-eind punten van het beheer punt en het software-update punt in IIS om client aanvragen te verwerken. De CMG maakt geen enkele interne eind punten zichtbaar. Elk eind punt dat is gepubliceerd naar de CMG heeft een URL-toewijzing.

- De externe URL is de client die wordt gebruikt om te communiceren met de CMG.
- De interne URL is het CMG-verbindings punt dat wordt gebruikt voor het door sturen van aanvragen naar de interne server.

#### <a name="url-mapping-example"></a>Voor beeld van URL-toewijzing

Wanneer u CMG-verkeer inschakelt op een beheer punt, maakt Configuration Manager een interne set URL-toewijzingen voor elke beheer punt server. Bijvoorbeeld: ccm_system, ccm_incoming en sms_mp. De externe URL voor het ccm_system eind punt van het beheer punt kan er als volgt uitzien:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
De URL is uniek voor elk beheer punt. De Configuration Manager-client plaatst vervolgens de naam van het CMG-beheer punt in de lijst met internet beheer punten. Deze naam ziet er als volgt uit:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
De site uploadt automatisch alle gepubliceerde externe Url's naar het CMG. Dit gedrag zorgt ervoor dat de CMG URL-filtering kan uitvoeren. Alle URL-toewijzingen worden gerepliceerd naar het CMG-verbindings punt. Vervolgens wordt de communicatie doorgestuurd naar interne servers op basis van de externe URL van de client aanvraag.


## <a name="security-guidance-for-cmg"></a>Beveiligings richtlijnen voor CMG

<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>De certificaatintrekkingslijst publiceren

Publiceer de certificaatintrekkingslijst (CRL) van uw PKI voor toegang tot Internet-clients. Wanneer u een CMG implementeert met behulp van PKI, moet u de service configureren om het **intrekken van client certificaten te verifiëren** op het tabblad instellingen. Met deze instelling wordt de service geconfigureerd voor het gebruik van een gepubliceerde certificaatintrekkingslijst (CRL). Zie het [intrekken van het PKI-certificaat plannen](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)voor meer informatie.

Met deze CMG-optie wordt het certificaat voor client verificatie gecontroleerd.

- Als de client gebruikmaakt van Azure AD-verificatie, is de CRL niet van belang.
- Als u PKI gebruikt en de CRL extern publiceert, schakelt u deze optie in (aanbevolen).
- Als u PKI gebruikt, publiceert u de CRL niet en schakelt u deze optie uit.
- Als u deze optie onjuist configureert, kan dit extra verkeer van clients naar de CMG veroorzaken. Dit extra verkeer kan de Azure-uitvoerige gegevens verhogen, waardoor uw Azure-kosten kunnen worden verhoogd.<!-- SCCMDocs#1434 -->

<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Vermeldingen in de certificaat vertrouwens lijst van de site controleren

<!--503739-->
Elke Configuration Manager site bevat een lijst met vertrouwde basis certificerings instanties, de certificaat vertrouwens lijst (CTL). Ga naar de werk ruimte beheer, vouw site configuratie uit en selecteer sites om de lijst weer te geven en te wijzigen. Selecteer een site en klik op Eigenschappen in het lint. Ga naar het tabblad **communicatie client computer** en klik vervolgens op **instellen** onder vertrouwde basis certificerings instanties.

> [!Note]
> Vanaf versie 1906 wordt dit tabblad **communicatie beveiliging**genoemd.<!-- SCCMDocs#1645 -->  

Gebruik een meer beperkende CTL voor een site met een CMG met PKI-client verificatie. Anders worden clients met client verificatie certificaten die zijn uitgegeven door een vertrouwde basis die al op het beheer punt bestaan, automatisch geaccepteerd voor client registratie.

Deze subset biedt beheerders meer controle over de beveiliging. De CTL beperkt de server om alleen client certificaten te accepteren die zijn uitgegeven door de certificerings instanties in de CTL. Windows wordt bijvoorbeeld geleverd met een aantal bekende certificaten van certificerings instanties van derden, zoals VeriSign en Thawte. Standaard vertrouwt de computer met IIS certificaten die zijn gekoppeld aan deze bekende certificerings instanties. Zonder IIS te configureren met een CTL, worden computers met een client certificaat dat is uitgegeven door deze Ca's, geaccepteerd als een geldige Configuration Manager-client. Als u IIS configureert met een CTL die deze certificerings instanties niet bevat, worden client verbindingen geweigerd als het certificaat aan deze certificerings instanties is gekoppeld.

### <a name="enforce-tls-12"></a><a name="bkmk_tls"></a>TLS 1,2 afdwingen

<!-- SCCMDocs-pr#4021 -->

Vanaf versie 1906 gebruikt u de instelling CMG om **TLS 1,2**af te dwingen. Dit is alleen van toepassing op de Azure Cloud service-VM. Dit geldt niet voor on-premises Configuration Manager site servers of-clients. Raadpleeg [How to Enable tls 1,2](../../../plan-design/security/enable-tls-1-2.md)(Engelstalig) voor meer informatie over TLS 1,2.


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Volgende stappen

- [Een cloudbeheergateway plannen](plan-cloud-management-gateway.md)
- [Een cloudbeheergateway instellen](setup-cloud-management-gateway.md)
- [Veelgestelde vragen over de Cloud beheer gateway](cloud-management-gateway-faq.md)
- [Certificaten voor cloudbeheergateway](certificates-for-cloud-management-gateway.md)

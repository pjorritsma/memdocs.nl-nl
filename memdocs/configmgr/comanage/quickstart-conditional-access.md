---
title: Voorwaardelijke toegang met co-beheer
titleSuffix: Configuration Manager
description: Gebruikers toegang tot bedrijfs resources beheren op basis van nalevings regels van intune
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d35f36b6578359f62f21b4e2208a70ace22cf0d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711502"
---
# <a name="conditional-access-with-co-management"></a>Voorwaardelijke toegang met co-beheer

Met voorwaardelijke toegang wordt ervoor te zorgen dat alleen vertrouwde gebruikers toegang hebben tot de resources van de organisatie op vertrouwde apparaten met behulp van vertrouwde apps. Het is volledig gemaakt in de Cloud. Of u nu apparaten beheert met intune of uw Configuration Manager-implementatie met co-beheer uitbreidt, werkt op dezelfde manier.

In de volgende video is Senior Program Manager Joey Glocke en de vergren deling van productmarketing Manager Locky Ainley met co-beheer beschreven en voorwaardelijke toegang voor de demo:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Met co-beheer evalueert intune elk apparaat in uw netwerk om te bepalen hoe betrouwbaar het is. Dit kan op de volgende twee manieren worden geëvalueerd:

1. Met intune wordt gecontroleerd of een apparaat of app wordt beheerd en veilig geconfigureerd. Deze controle is afhankelijk van hoe u het nalevings beleid van uw organisatie instelt. Controleer bijvoorbeeld of op alle apparaten versleuteling is ingeschakeld en niet opengebroken.  

    - Deze evaluatie is een inbreuk op de beveiliging en op basis van configuratie  

    - Voor door co beheerde apparaten is Configuration Manager ook evaluatie op basis van een configuratie. Bijvoorbeeld vereiste updates of apps voldoen aan het beleid. InTune combineert deze evaluatie samen met een eigen evaluatie.  

2. InTune detecteert actieve beveiligings incidenten op een apparaat. Er wordt gebruikgemaakt van de intelligente beveiliging van [micro soft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (voorheen Windows Defender ATP) en andere providers voor de [bescherming van mobiele bedreigingen](https://www.lookout.com/about/partners/microsoft). Deze partners voeren doorlopende gedrags analyse uit op apparaten. Deze analyse detecteert actieve incidenten en geeft deze informatie door aan intune voor een real-time compatibiliteits evaluatie.  

    - Deze evaluatie is na beveiligings schending en op incident gebaseerd  

Micro soft Corporate Vice President Anderson heeft betrekking op voorwaardelijke toegang uitgebreid met Live-demo's tijdens de Ignite 2018-toespraak. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Voorwaardelijke toegang biedt ook een centrale locatie om de status van alle apparaten die met het netwerk zijn verbonden te bekijken. U profiteert van de voor delen van de Cloud schaal. Dit is met name nuttig voor het testen van Configuration Manager productie-exemplaren.


## <a name="benefits"></a>Voordelen

Elk IT-team is Obsessed met netwerk beveiliging. Het is verplicht om ervoor te zorgen dat elk apparaat aan uw beveiligings-en bedrijfs vereisten voldoet voordat ze toegang krijgen tot uw netwerk. Met voorwaardelijke toegang kunt u de volgende factoren bepalen: 
- Als elk apparaat is versleuteld  
- Als er malware is geïnstalleerd  
- Als de instellingen zijn bijgewerkt  
- Als de service is opengebroken of geroot  

Voorwaardelijke toegang combineert gedetailleerde controle over de organisatie gegevens met een gebruikers ervaring die de productiviteit van werk nemers op elk apparaat in een wille keurige locatie optimaliseert.

In de volgende video ziet u hoe [Advanced thread Protection](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) is geïntegreerd in algemene scenario's die u regel matig ondervindt:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Met co-beheer kunnen intune de verantwoordelijkheden van Configuration Manager bevatten voor het beoordelen van de naleving van uw beveiligings vereisten voor vereiste updates of apps. Dit gedrag is belang rijk voor elke IT-organisatie die Configuration Manager wilt blijven gebruiken voor complexe apps en patch beheer.

Voorwaardelijke toegang is ook een belang rijk onderdeel van het ontwikkelen van de architectuur van de [vertrouwens relatie met nul](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) . Met voorwaardelijke toegang bedekken de besturings elementen voor compatibele apparaten de kern lagen van het vertrouwens netwerk van nul. Deze functionaliteit is een belang rijk onderdeel van hoe u uw organisatie in de toekomst kunt beveiligen.

Zie voor meer informatie het blog bericht over het [verbeteren van voorwaardelijke toegang met computer risico gegevens van micro soft Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Casestudy's

De IT Consulting Fiat Wipro maakt gebruik van voorwaardelijke toegang om de apparaten te beschermen en te beheren die worden gebruikt door alle werk nemers van 91.000. In een studie met recente casestudy's, de vice president van IT, op Wipro vermeld:

> *Het bereiken van voorwaardelijke toegang is een Big win voor Wipro. Nu hebben alle werk nemers mobiele toegang tot informatie op aanvraag.* 
>  *We hebben onze beveiligings postuur en productiviteit van werk nemers verbeterd. Nu 91.000 werk nemers profiteren van zeer veilige toegang tot meer dan 100 apps vanaf elk apparaat, overal.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Andere voor beelden zijn: 

- Nestlé, die gebruikmaakt van op apps gebaseerde voorwaardelijke toegang voor meer dan 150.000 werk nemers  

- Het Automation-Software bedrijf, uitgebracht, kan er nu voor zorgen dat alleen beheerde apparaten toegang hebben tot Office 365-apps zoals teams en het intranet van het bedrijf. " Ze kunnen ook hun werk nemers veilig toegang bieden tot andere Cloud-apps, zoals workday en Sales Force. Meer informatie over de ervaring van uitgebracht met intune vindt u [in uitgebracht verhoogt het bedrijfs tempo met mobiele samenwerkings Programma's in Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

InTune is ook volledig geïntegreerd met partners zoals Cisco ISE, Aruba Clear Pass en Citrix NetScaler. Met deze partners kunt u toegangs beheer op basis van de intune-inschrijving en de nalevings status van het apparaat op deze andere platformen onderhouden.

Zie de volgende Video's voor meer informatie:
- [Nils Anderson demo's in detail voorwaardelijke toegang](https://youtu.be/8321obNofgM?t=547)  
- [Aanvullende details van de eindpunt zone 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Toegevoegde waarde

Met voorwaardelijke toegang en ATP-integratie hebt u een fundamenteel onderdeel van elke IT-organisatie fortifying: veilige toegang tot de Cloud.

In meer dan 63% van alle gegevens schendingen krijgen de aanvallers toegang tot het netwerk van de organisatie via zwakke, standaard of gestolen gebruikers referenties. Omdat voorwaardelijke toegang zich richt op het beveiligen van de identiteit van de gebruiker, wordt de dief stal van referenties beperkt. Met voorwaardelijke toegang kunt u identiteiten, of privileged of niet-Privileged, beheren en beveiligen. Er is geen betere manier om de apparaten en de gegevens erop te beveiligen.

Aangezien voorwaardelijke toegang een kern onderdeel is van Enterprise Mobility + Security (EMS), is er geen on-premises installatie of architectuur vereist. Met intune en Azure Active Directory (Azure AD) kunt u snel voorwaardelijke toegang configureren in de Cloud. Als u momenteel gebruikmaakt van Configuration Manager, kunt u uw omgeving eenvoudig uitbreiden naar de Cloud met co-beheer en nu aan de slag gaan met het gebruik hiervan.

Voor meer informatie over de ATP-integratie raadpleegt u dit blog bericht [micro soft Defender ATP Device risico Score maakt nieuwe cyberattack, biedt de schijf voorwaardelijke toegang tot het beveiligen van netwerken](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). In dit artikel wordt uitgelegd hoe een geavanceerde hacker-groep nooit voor de weer gegeven hulpprogram ma's wordt gebruikt. De micro soft-Cloud heeft deze gedetecteerd en gestopt omdat de doel gebruikers voorwaardelijke toegang hadden. De indringing heeft het beleid voor voorwaardelijke toegang op basis van het apparaat geactiveerd. Hoewel de aanvaller al een aanvaller binnen in het netwerk heeft ingesteld, zijn de gebruikte computers automatisch beperkt van toegang tot organisatie Services en gegevens die worden beheerd door Azure AD.



## <a name="configure"></a>Configureren

Voorwaardelijke toegang is gemakkelijk te gebruiken wanneer u [co-beheer inschakelt](how-to-enable.md). Hiervoor moet de werk belasting van het **nalevings beleid** worden verplaatst naar intune. Zie [Configuration Manager workloads naar intune overschakelen](how-to-switch-workloads.md)voor meer informatie. 

Raadpleeg de volgende artikelen voor meer informatie over het gebruik van voorwaardelijke toegang: 

- [Voorwaardelijke toegang in azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Intune apparaatnalevingsbeleid](https://docs.microsoft.com/intune/device-compliance)  

- [Op apps gebaseerde voorwaardelijke toegang met Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Functies voor voorwaardelijke toegang worden onmiddellijk beschikbaar gesteld voor hybride apparaten die lid zijn van Azure AD. Deze functies omvatten multi-factor Authentication en hybride toegangs beheer voor Azure AD. Dit gedrag is omdat ze zijn gebaseerd op Azure AD-eigenschappen. Schakel het co-beheer in om de evaluatie op basis van een configuratie van intune en Configuration Manager te benutten. Met deze configuratie hebt u rechtstreeks toegang tot het beheer van intune voor compatibele apparaten. Het biedt ook de evaluatie functie van het nalevings beleid van intune.  


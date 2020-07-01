---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: Een overzicht van de Desktop Analytics-service die is geïntegreerd met Configuration Manager.
ms.date: 06/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 3a1aa67c51998de62f6390db848a458876327ea7
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590912"
---
# <a name="what-is-desktop-analytics"></a>Wat is Desktop Analytics?

Desktop Analytics is een Cloud service die kan worden geïntegreerd met Configuration Manager. De service biedt inzicht en intelligentie waarmee u meer weloverwogen beslissingen kunt nemen over de update gereedheids van uw Windows-clients. Gegevens uit uw organisatie worden gecombineerd met gegevens die zijn geaggregeerd van miljoenen apparaten die zijn verbonden met micro soft-Cloud Services.

Gebruik Desktop Analytics met Configuration Manager voor het volgende:  

- Een inventaris maken van apps die in uw organisatie worden uitgevoerd  

- Compatibiliteit van apps evalueren met de nieuwste updates voor Windows 10-onderdelen  

- Compatibiliteits problemen identificeren en suggesties voor risico beperking ontvangen op basis van gegevens inzichten die in de Cloud zijn ingeschakeld  

- Test groepen maken die de volledige toepassing en het stuur programma voor een minimale set apparaten vertegenwoordigen  

- Windows 10 implementeren op pilot-en productie-beheerde apparaten  

![Scherm opname van de start pagina van Desktop Analytics in de Azure Portal](media/portal-home.png)

De volgende video is een sessie van Ignite 2019, met meer informatie over desktop Analytics:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[Desktop Analytics en Configuration Manager gebruiken om de totale eigendoms kosten van Windows te verminderen door middel van gegevensgestuurde inzichten voor beheer, onderhoud en ondersteuning](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions)

Ga naar 10:00 voor een diep gaande demo.

> [!Note]  
> Desktop Analytics is een opvolger van Windows Analytics, die is ingetrokken op 31 januari 2020.
>
> De mogelijkheden van Windows Analytics worden gecombineerd in de Desktop Analytics-service. Desktop Analytics is ook nauw keuriger geïntegreerd met Configuration Manager. Zie [Veelgestelde vragen over klanten met Windows Analytics](faq.md#existing-windows-analytics-customers)voor meer informatie.

## <a name="benefits"></a>Voordelen

Veel klanten hebben problemen met het ophalen en blijven actueel hebben van Windows 10. De primaire uitdaging is het testen van toepassingen. Dit proces is doorgaans hand matig. Het is tijdrovender dat IT-beheerders en toepassings eigenaren voortdurend bestaande toepassingen kunnen analyseren. Vervolgens eventuele problemen oplossen die zich voordoen.

Desktop Analytics biedt de volgende voor delen:

- **Hardware-en software-inventaris**: inventarisatie van belang rijke factoren zoals apps en versies van Windows.  

- **Pilot-identificatie**: identificatie van de kleinste set apparaten die de breedste dekking van factoren bieden. Het richt zich op de factoren die het belangrijkst zijn voor een pilot van Windows-upgrades en-updates. Als u er zeker van wilt zijn dat de pilot meer succes biedt, kunt u sneller en veiliger door gaan met grote implementaties in de productie omgeving.  

- **Probleem identificatie**: het gebruik van geaggregeerde markt gegevens en gegevens uit uw omgeving, de service voor spelt mogelijke problemen met het verkrijgen en blijven gebruiken van Windows. Vervolgens worden mogelijke oplossingen voorgesteld.  

- **Configuration Manager-integratie**: de Service Cloud-maakt uw bestaande on-premises infra structuur mogelijk. Gebruik deze gegevens en analyse om Windows op uw apparaten te implementeren en te beheren.  

## <a name="prerequisites"></a>Vereisten

Als u Desktop Analytics wilt gebruiken, moet u ervoor zorgen dat uw omgeving voldoet aan de volgende vereisten.

### <a name="technical"></a>Technisch

- Een actief globaal Azure-abonnement met [globale beheerders](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) machtigingen. [Micro soft-accounts](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) worden niet ondersteund.  

    > [!IMPORTANT]
    > Desktop Analytics is een Windows-service die wordt gehost in azure Global en gebruikmaakt van diagnostische gegevens van Windows. De wereld wijde Azure-service is beschikbaar voor klanten van de Amerikaanse overheid, maar komt niet overeen met de [gcc-kenmerken (Government compliance) van de Amerikaanse overheid](https://docs.microsoft.com/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc#us-government-community-compliance) . Zie het [vertrouwens centrum van micro soft](https://docs.microsoft.com/microsoft-365/compliance/offering-home?view=o365-worldwide)voor een lijst met compliance-aanbiedingen voor micro soft-producten en-services. Desktop Analytics is niet beschikbaar voor klanten met een hoog of Amerikaans Ministerie van defensie (DOD) van GCC. Het gebruik van Azure Government-abonnementen voor het hosten van Desktop Analytics-werk ruimten wordt niet ondersteund.

    - **Eigenaars machtigingen voor werk ruimten** voor het **instellen van uw werk ruimte**en de volgende rollen:  

      - Rol van [**Desktop Analytics-beheerder**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) .

      - [**Log Analytics Inzender**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) en [**beheerder van gebruikers toegang**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) voor de resource groep een bestaande werk ruimte te gebruiken of een nieuwe werk ruimte in een bestaande resource groep te maken.

      - De machtigingen [**eigenaar**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner), of [**Inzender**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) en [**gebruikers toegang**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) voor het abonnement om een werk ruimte te maken in een nieuwe resource groep.  

    - Voor toegang tot de portal na onboarding hebt u het volgende nodig:

      - De rol en [**eigenaar**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)van de [**beheerder van Desktop Analytics**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) of [**inzender**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) machtigingen voor de gemaakte log Analytics werk ruimte.

- Configuration Manager, versie 1902 met update pakket (4500571) of hoger. Zie [Update Configuration Manager](connect-configmgr.md#bkmk_hotfix)voor meer informatie.  

    - [**Volledige beheerdersrol**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) in Configuration Manager  

    > [!NOTE]
    > Desktop Analytics ondersteunt meerdere Configuration Manager hiërarchieën die rapporteren aan één Azure AD-Tenant.<!-- 4814075 --> Als u meerdere hiërarchieën in uw omgeving hebt, hebt u de volgende opties:
    >
    > - Gebruik verschillende commerciële Id's en Azure AD-tenants.
    > - Configureer beide hiërarchieën zodat deze dezelfde commerciële ID gebruiken om het exemplaar van de Azure AD-Tenant en het bureau blad Analytics te delen. Gebruik [verschillende apps](connect-configmgr.md#bkmk_connect) voor het verbinden van elke hiërarchie. Het kan tot 30 dagen duren nadat u een hiearchy voor de portal hebt losgekoppeld om wijzigingen weer te geven. 

- Apparaten met Windows 7, Windows 8,1 of Windows 10  

    - Installeer de laatste updates. Zie [apparaten bijwerken](enroll-devices.md#update-devices)voor meer informatie.  

    - Apparaten moeten ook beschikken over de Configuration Manager-client versie 1902 met update pakket (4500571) of hoger. Zie [Update Configuration Manager](connect-configmgr.md#bkmk_hotfix)voor meer informatie.  

    > [!Note]  
    > Desktop Analytics biedt geen ondersteuning voor upgrades naar Windows 10 Long-term Servicing Channel (LTSC). Zie [Windows as a Service Overview](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)(Engelstalig) voor meer informatie.
    >
    > Desktop Analytics is ontworpen om het in-place upgrade-scenario het beste te ondersteunen. Als u belang rijke wijzigingen wilt aanbrengen, zoals van 32-bits tot 64-bits architectuur, gebruikt u een Imaging-scenario. Desktop Analytics Insights is nog steeds waardevol in deze klassieke implementatie scenario's voor besturings systemen, maar u kunt de in-place upgrade specifieke richt lijnen negeren. Zie [scenario's voor het implementeren van ENTER prise-besturings systemen met Configuration Manager](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)voor meer informatie.

- Diagnostische gegevens van Windows. Raadpleeg voor meer informatie de volgende artikelen:  

    - [Niveaus van diagnostische gegevens](enable-data-sharing.md#diagnostic-data-levels)  

    - [Privacy van Desktop Analytics](privacy.md)  

- Netwerk verbinding van apparaten met de open bare cloud van micro soft. Zie [How to Enable Data Sharing](enable-data-sharing.md) (Engelstalig) voor meer informatie.  

> [!Important]
> Micro soft heeft een sterke toezeg ging voor het leveren van de hulpprogram ma's en resources die u in staat stellen om uw privacy te beheren. Als gevolg hiervan verzamelt micro soft niet de volgende gegevens van apparaten die zich in Europese landen (EER en Zwitser land) bevinden:
>
> - Windows diagnostische gegevens van Windows 8,1-apparaten
> - Gebruiks gegevens van de app voor Windows 7

### <a name="licensing-and-costs"></a>Licentie verlening en kosten

- Een actief globaal Azure-abonnement.

    > [!NOTE]
    > De meeste equivalente abonnementen voor Configuration Manager omvatten ook Azure AD. Zie bijvoorbeeld [Microsoft 365 plannen](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans) en Enterprise Mobility + Security- [licenties](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security).

- Apparaten die zijn Inge schreven in Desktop Analytics, moeten een geldige Configuration Manager licentie hebben. Zie [Configuration Manager Licensing](../core/understand/product-and-licensing-faq.md)voor meer informatie.

- Gebruikers van het apparaat hebben een van de volgende licenties nodig:

  - Windows 10 Enter prise E3 of E5 (opgenomen in Microsoft 365 F3, E3 of E5)

  - Windows 10-onderwijs a3 of A5 (opgenomen in Microsoft 365 a3 of A5)

  - Windows Virtual Desktop Access E3 of E5  

> [!NOTE]
> Naast de kosten van deze licentie abonnementen zijn er geen extra kosten verbonden aan het gebruik van Desktop Analytics in azure Log Analytics. De gegevens typen die door Desktop Analytics worden opgenomen, zijn gratis van de Log Analytics gegevens opname en de retentie kosten. In het geval van niet-factureer bare gegevens typen zijn deze gegevens ook niet onderhevig aan Log Analytics dagelijkse gegevens opname limiet. Zie [log Analytics gebruik en kosten](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

De volgende zelf studie bevat een stapsgewijze hand leiding om aan de slag te gaan met Desktop Analytics en Configuration Manager:
  
> [!div class="nextstepaction"]
> [Windows 10 implementeren naar pilot](tutorial-windows10.md)

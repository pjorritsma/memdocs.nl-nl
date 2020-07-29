---
title: Scenario's voor voorwaardelijke toegang
titleSuffix: Microsoft Intune
description: Meer informatie over hoe voorwaardelijke toegang van Intune doorgaans wordt gebruikt voor voorwaardelijke toegang op basis van apparaten of apps.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a0b8e55e-c3d8-4599-be25-dc10c1027b62
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9c1d4dacf29aa0c87a8356306d10bf05acbf3afb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462164"
---
# <a name="what-are-common-ways-to-use-conditional-access-with-intune"></a>Wat zijn gebruikelijke manieren om voorwaardelijke toegang met Intune te gebruiken?

Er zijn twee soorten voorwaardelijke toegang met Intune: voorwaardelijke toegang op basis van apparaten en voorwaardelijke toegang op basis van apps. U moet het gerelateerde nalevingsbeleid configureren voor naleving van de voorwaardelijke toegang binnen uw organisatie. Voorwaardelijke toegang wordt meestal gebruikt voor zaken als toegang tot Exchange toestaan of blokkeren, toegang tot het netwerk bepalen of integratie realiseren met een Mobile Threat Defense-oplossing.
 
Met de informatie in dit artikel kunt u meer inzicht krijgen in hoe u de Intune-nalevingsmogelijkheden voor mobiele *apparaten* kunt gebruiken én in hoe Intune Mobile *Application* Management (MAM) werkt. 

> [!NOTE]
> Voorwaardelijke toegang is een Azure Active Directory-functie die is opgenomen in een Azure Active Directory Premium-licentie. Deze mogelijkheid wordt verbeterd door Intune door het toevoegen van nalevingsbeleid voor mobiele apparaten en beheer van mobiele apps aan de oplossing. Het knooppunt voor voorwaardelijke toegang dat via *Intune* wordt geopend, is hetzelfde als het knooppunt dat u opent via *Azure AD*.  

## <a name="device-based-conditional-access"></a>Voorwaardelijke toegang op basis van het apparaat

Intune en Azure Active Directory werken samen om ervoor te zorgen dat alleen beheerde en compatibele apparaten toegang kunnen krijgen tot e-mail, Office 365-services, SaaS-apps (Software as a Service) en [on-premises apps](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started). U kunt daarnaast een beleid in Azure Active Directory instellen, zodat alleen computers die zijn toegevoegd aan een domein of mobiele apparaten die zijn ingeschreven in Intune, toegang tot Office 365-services hebben.

Met Intune beschikt u over mogelijkheden voor apparaatnalevingsbeleid waarmee u de nalevingsstatus van het apparaat kunt evalueren. De nalevingsstatus wordt gerapporteerd aan Azure Active Directory om het voorwaardelijke toegangsbeleid af te dwingen dat in Azure Active Directory wordt gemaakt wanneer de gebruiker zich toegang tot uw bedrijfsresources probeert te verschaffen.

De op apparaten gebaseerde beleidsregels voor voorwaardelijke toegang voor Exchange Online en andere Office 365-producten geconfigureerd via de [Azure-portal](../fundamentals/what-is-intune.md).

- Meer informatie over [het vereisen van beheerde apparaten met voorwaardelijke toegang in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).

- Meer informatie over [Intune-apparaatnaleving](device-compliance-get-started.md).

- Meer informatie over [ondersteunde browsers met voorwaardelijke toegang in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/technical-reference#supported-browsers).

> [!NOTE]
> Als u op Android-apparaten Op apparaten gebaseerde toegang voor Sharepoint Online of Op browsers gebaseerde toegang tot Exchange Online inschakelt, moeten gebruikers de optie **Browsertoegang inschakelen** als volgt op het ingeschreven apparaat inschakelen:
> 1. Open de **app Bedrijfsportal**.
> 2. Ga naar de pagina **Instellingen** via de drie puntjes (...) of via de menuknop van de hardware.
> 3. Selecteer **Browsertoegang inschakelen**. 
> 4. In de browser Chrome meldt u zich af bij Office 365. Start vervolgens Chrome opnieuw op.

### <a name="conditional-access-based-on-network-access-control"></a>Voorwaardelijke toegang op basis van netwerktoegangsbeheer

Intune kan worden geïntegreerd met partners als Cisco ISE, Aruba Clear Pass en Citrix NetScaler voor toegangsbeheer op basis van de Intune-inschrijving en de nalevingsstatus van het apparaat.

Gebruikers kan toegang tot het Wi-Fi-netwerk of de VPN-resources worden verleend of geweigerd door te controleren of het apparaat dat ze gebruiken, wordt beheerd met en voldoet aan het Intune-nalevingsbeleid voor apparaten.

- Meer informatie over de [NAC-integratie met Intune](network-access-control-integrate.md).

### <a name="conditional-access-based-on-device-risk"></a>Voorwaardelijk op basis van het apparaatrisico

Intune werkt samen met leveranciers van Mobile Threat Defense, die een beveiligingsoplossing bieden voor het detecteren van malware, Trojaans paarden en andere bedreigingen op mobiele apparaten.

#### <a name="how-the-intune-and-mobile-threat-defense-integration-works"></a>Hoe de integratie van Intune en Mobile Threat Defense werkt

Wanneer de Mobile Threat Defense-agent op een mobiel apparaat is geïnstalleerd, stuurt de agent berichten over de nalevingsstatus naar Intune om te melden wanneer er op het mobiele apparaat zelf een bedreiging wordt gevonden.

De integratie van Intune en Mobile Threat Defense speelt een rol bij de beslissingen die op basis van de apparaatrisico's worden genomen voor de voorwaardelijke toegang.

- Meer informatie over [Intune Mobile Threat Defense](mobile-threat-defense.md).

### <a name="conditional-access-for-windows-pcs"></a>Voorwaardelijke toegang voor Windows-pc's

Voorwaardelijke toegang voor pc's biedt mogelijkheden die vergelijkbaar zijn met de mogelijkheden voor mobiele apparaten. Laten we eens kijken op welke manieren u voorwaardelijke toegang kunt gebruiken wanneer u pc's met Intune beheert.

#### <a name="corporate-owned"></a>In bedrijfseigendom

- **Hybrid Azure AD joined:** Deze optie wordt doorgaans gebruikt door organisaties die redelijk tevreden zijn over de manier waarop hun pc's al worden beheerd met AD-groepsbeleid of Configuration Manager.

- **Azure AD-domein toegevoegd en Intune-beheerprogramma:** Dit scenario is bedoeld voor organisaties die voornamelijk cloudservices gebruiken, met het doel om het gebruik van een on-premises infrastructuur te beperken, of alleen cloudservices gebruiken (geen on-premises infrastructuur). Azure AD Join werkt goed in een hybride omgeving en biedt toegang tot zowel cloud- als on-premises apps en bronnen. Het apparaat wordt toegevoegd aan Azure AD en wordt geregistreerd bij Intune, dat kan worden gebruikt als criterium voor voorwaardelijke toegang bij het openen van bedrijfsresources.

#### <a name="bring-your-own-device-byod"></a>BYOD (Bring Your Own Device)

- **Workplace join en Intune-beheer:** Hier kan de gebruiker de eigen persoonlijke apparaten toevoegen voor toegang tot bedrijfsresources en -services. U kunt Workplace Join gebruiken en apparaten bij Intune MDM registreren om beleidsregels op apparaatniveau te ontvangen. Dit is een alternatieve optie om de criteria voor voorwaardelijke toegang te evalueren.

Meer informatie over [apparaatbeheer in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/overview).

## <a name="app-based-conditional-access"></a>Voorwaardelijke toegang op basis van apps

Intune en Azure Active Directory werken samen om ervoor te zorgen dat alleen beheerde apps toegang hebben tot de bedrijfs-e-mail of andere Office 365-services.

- Meer informatie over [op apps gebaseerde voorwaardelijke toegang met Intune](app-based-conditional-access-intune.md).

### <a name="intune-conditional-access-for-exchange-on-premises"></a>Voorwaardelijke toegang van Intune voor Exchange On-Premises

Voorwaardelijke toegang kan worden gebruikt de toegang tot **Exchange On-Premises** toe te staan of te blokkeren op basis van de beleidsregels voor apparaatcompatibiliteit en de registratiestatus. Wanneer voorwaardelijke toegang wordt gebruikt in combinatie met een nalevingsbeleid voor apparaten, hebben alleen apparaten die voldoen aan het beleid toegang voor Exchange On-Premises.

U kunt geavanceerde instellingen configureren voor de voorwaardelijke toegang. Zodoende hebt u voor gedetailleerdere controle over onder meer het volgende:

- Toestaan of blokkeren van bepaalde platforms.

- Onmiddellijk blokkeren van apparaten die niet worden beheerd door Intune.

Wanneer er beleidsregels voor apparaatcompatibiliteit en voorwaardelijke toegang zijn toegepast, wordt voor elk apparaat dat wordt gebruikt voor toegang tot Exchange On-Premises gecontroleerd of de beleidsregels worden nageleefd.

Wanneer apparaten niet voldoen aan de gestelde voorwaarden, wordt de eindgebruiker door de registratieprocedure voor het apparaat geleid om het probleem te verhelpen dat ervoor zorgt dat het apparaat niet-compatibel is.

> [!NOTE]
> Vanaf juli 2020 wordt de ondersteuning voor de Exchange connector afgeschaft en vervangen door Exchange [HMA](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) (Hybrid Modern Authentication, hybride moderne verificatie). Voor het gebruik van HMA hebt u Intune niet nodig om de Exchange-connector in te stellen en te gebruiken. Met deze wijziging wordt de gebruikersinterface voor het configureren en beheren van de Exchange-connector voor Intune verwijderd uit het Microsoft Endpoint Manager-beheercentrum, tenzij u al een Exchange-connector gebruikt met uw abonnement.
>
> Als u een Exchange-connector hebt ingesteld in uw omgeving, blijft de Intune-tenant ondersteund voor het gebruik ervan en houdt u toegang tot de gebruikersinterface die de configuratie ervan ondersteunt. Raadpleeg [Exchange on-premises-connector installeren](../protect/exchange-connector-install.md) voor meer informatie. U kunt de connector blijven gebruiken of HMA configureren en vervolgens de connector verwijderen.
>
> Hybrid Modern Authentication biedt functionaliteit die eerder is geleverd door de Exchange connector voor Intune: Toewijzing van een apparaat-id aan het Exchange-record.  Deze toewijzing vindt nu plaats buiten een configuratie die u in Intune maakt of de vereiste van de Intune-connector om Intune en Exchange te koppelen. Met HMA is de vereiste voor het gebruik van de specifieke configuratie voor ‘Intune’ (de connector) verwijderd.


<!-- Deprecated with change from the connector to Exchange hybrid modern authentication)

#### How conditional access for Exchange on-premises works

Conditional access for Exchange on-premises works differently than Azure Conditional Access based policies. You install the Intune Exchange on-premises connector to directly interact with Exchange server. The Intune Exchange connector pulls in all the Exchange Active Sync (EAS) records that exist at the Exchange server so Intune can take these EAS records and map them to Intune device records. These records are devices enrolled and recognized by Intune. This process allows or blocks e-mail access.

If the EAS record is new and Intune isn't aware of it, Intune issues a cmdlet (pronounced "command-let") that directs the Exchange server to block access to e-mail. Following are more details on how this process works:

![Exchange on-premises with CA flow-chart](./media/conditional-access-intune-common-ways-use/ca-intune-common-ways-1.png)

1. User tries to access corporate email, which is hosted on Exchange on-premises 2010 SP1 or later.

2. If the device is not managed by Intune, access to email will be blocked. Intune sends a block notification to the EAS client.

3. EAS receives the block notification, moves the device to quarantine, and sends the quarantine email with remediation steps that contain links so the users can enroll their devices.

4. The Workplace join process happens, which is the first step to have the device managed by Intune.

5. The device gets enrolled into Intune.

6. Intune maps the EAS record to a device record, and saves the device compliance state.

7. The EAS client ID gets registered by the Azure AD Device Registration process, which creates a relationship between the Intune device record, and the EAS client ID.

8. The Azure AD Device Registration saves the device state information.

9. If the user meets the conditional access policies, Intune issues a cmdlet through the Intune Exchange connector that allows the mailbox to sync.

10. Exchange server sends the notification to EAS client so the user can access e-mail.
-->

#### <a name="whats-the-intune-role"></a>Wat is de rol van Intune?

Met Intune wordt de apparaatstatus beoordeeld en beheerd.

#### <a name="whats-the-exchange-server-role"></a>Wat is de rol van de Exchange-server?

De Exchange-server biedt de API en infrastructuur om apparaten in quarantaine te plaatsen.

> [!IMPORTANT]
> Houd er rekening mee dat er een nalevingsprofiel en Intune-licentie moet worden toegewezen aan de gebruiker van het apparaat, zodat het apparaat op naleving kan worden gecontroleerd. Als er geen nalevingsbeleid wordt geïmplementeerd voor de gebruiker, wordt het apparaat beschouwd als een apparaat dat voldoet aan het beleid en worden er geen toegangsbeperkingen toegepast.

## <a name="next-steps"></a>Volgende stappen

[Voorwaardelijke toegang in Azure Active Directory configureren](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)

[Op apps gebaseerd beleid voor voorwaardelijke toegang instellen](app-based-conditional-access-intune-create.md)

[Beleid maken voor voorwaardelijke toegang voor Exchange On-premises](conditional-access-exchange-create.md)

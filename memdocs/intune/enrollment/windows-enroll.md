---
title: Inschrijving voor Windows-apparaten instellen met Microsoft Intune
titleSuffix: ''
description: Stel inschrijving in voor Windows-apparaten.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 48560af1ff31d5660f00e775a2f510b88c08fd9c
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820592"
---
# <a name="set-up-enrollment-for-windows-devices"></a>Inschrijving voor Windows-apparaten instellen

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Met de informatie in dit artikel kunnen IT-beheerders de inschrijving van Windows-apparaten vereenvoudigen voor hun gebruikers. Zodra u [Intune hebt ingesteld](../fundamentals/setup-steps.md), kunnen gebruikers Windows-apparaten registreren door zich [aan te melden](https://docs.microsoft.com/mem/intune/user-help/windows-enrollment-company-portal) met hun werk- of schoolaccount.  

Als Intune-beheerder kunt u de registratie op de volgende manieren vereenvoudigen:

- [Automatische registratie inschakelen](#enable-windows-10-automatic-enrollment) (vereist Azure AD Premium)
- [CNAME-registratie](#simplify-windows-enrollment-without-azure-ad-premium)
- [Bulkinschrijving inschakelen](windows-bulk-enroll.md) (vereist Azure AD Premium en Windows Configuration Designer)

Vereenvoudiging van Windows-apparaatregistratie is afhankelijk van twee factoren:

- **Gebruikt u Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) is opgenomen in Enterprise Mobility + Security en andere licentieplannen.
- **Welke versies van Windows-clients worden er geregistreerd door gebruikers?** <br>Windows 10-apparaten kunnen automatisch worden ingeschreven door het toevoegen van een werk- of schoolaccount. Eerdere versies moeten worden ingeschreven met de bedrijfsportal-app.

||**Azure AD Premium**|**Overige AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Automatische inschrijving](#enable-windows-10-automatic-enrollment) |Gebruikersinschrijving|
|**Eerdere Windows-versies**|Gebruikersinschrijving|Gebruikersinschrijving|

Organisaties die gebruik kunnen maken van automatische registratie kunnen ook instellen dat [apparaten bulksgewijs worden geregistreerd](windows-bulk-enroll.md) via de Windows Configuration Designer-app.

## <a name="device-enrollment-prerequisites"></a>Vereisten voor apparaatinschrijving

Voordat een beheerder apparaten bij Intune kan inschrijven voor beheer, moeten de licenties al zijn toegewezen aan het account van de beheerder. [Meer informatie over het toewijzen van licenties voor apparaatinschrijving](../fundamentals/licenses-assign.md)

## <a name="multi-user-support"></a>Ondersteuning voor meerdere gebruikers

Intune ondersteunt meerdere gebruikers op apparaten waarop

- de Windows 10 Creator-update wordt uitgevoerd
- en die lid zijn van een Azure Active Directory-domein.

Als standaardgebruikers zich aanmelden met hun Azure AD-referenties, krijgen ze apps en beleidsregels die zijn toegewezen aan hun gebruikersnaam. Alleen de [primaire gebruiker](../remote-actions/find-primary-user.md) van het apparaat kan gebruikmaken van de bedrijfsportal voor selfservicescenario's zoals het installeren van apps en het uitvoeren van acties op apparaten (Verwijderen, Opnieuw instellen). Voor gedeelde Windows 10-apparaten waaraan geen primaire gebruiker is toegewezen, kan de bedrijfsportal nog wel worden gebruikt om beschikbare apps te installeren.

[!INCLUDE [AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]

## <a name="simplify-windows-enrollment-without-azure-ad-premium"></a>Windows-inschrijving vereenvoudigen zonder Azure AD Premium
Om de inschrijving te vereenvoudigen, maakt u een DNS-alias (domeinnaamserver) (CNAME-recordtype) waardoor inschrijvingsaanvragen worden doorgestuurd naar Intune-servers. Anders moeten gebruikers die verbinding met Intune proberen te maken, tijdens de inschrijving de naam van de Intune-server invoeren.

**Stap 1: CNAME maken** (optioneel)<br>
Maak CNAME-DNS-bronrecords voor uw bedrijfsdomein. Als de website van uw bedrijf bijvoorbeeld contoso.com is, maakt u een CNAME in DNS die EnterpriseEnrollment.contoso.com omleidt naar enterpriseenrollment-s.manage.microsoft.com.

Hoewel het maken van CNAME-DNS-vermeldingen optioneel is, maken CNAME-records het voor gebruikers makkelijker om zich in te schrijven. Als er geen CNAME-inschrijvingsrecord wordt gevonden, wordt gebruikers gevraagd de MDM-servernaam (enrollment.manage.microscoft.com) handmatig in te voeren.

|Type|Hostnaam|Verwijst naar|TTL|
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.bedrijfsdomein.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 uur|
|CNAME|EnterpriseRegistration.bedrijfsdomein.com|EnterpriseRegistration.windows.net|1 uur|

Als het bedrijf meer dan één UPN-achtervoegsel gebruikt, moet u een CNAME maken voor elke domeinnaam en die allemaal laten verwijzen naar EnterpriseEnrollment-s.manage.microsoft.com. Gebruikers van Contoso gebruiken bijvoorbeeld de volgende indelingen voor hun e-mail/UPN:

- name@contoso.com
- name@us.contoso.com
- name@eu.contoso.com

De Contoso DNS-beheerder moet de volgende CNAME’s maken:

|Type|Hostnaam|Verwijst naar|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 uur|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 uur|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 uur|

`EnterpriseEnrollment-s.manage.microsoft.com`: biedt ondersteuning voor een omleiding naar de Intune-service met domeinherkenning vanuit de domeinnaam van het e-mailadres

Het kan 72 uur duren voordat wijzigingen in DNS-records zijn doorgegeven. U kunt de DNS-wijziging in Intune pas controleren wanneer de DNS-record is doorgegeven.

## <a name="additional-endpoints-are-used-but-no-longer-supported"></a>Aanvullende eindpunten worden gebruikt, maar niet langer ondersteund
EnterpriseEnrollment-s.manage.microsoft.com is de voorkeurs-FQDN voor inschrijving. Er zijn nog twee andere eindpunten die in het verleden door klanten zijn gebruikt en nog werken, maar deze worden niet meer ondersteund. EnterpriseEnrollment.manage.microsoft.com (zonder de -s) en manage.microsoft.com werken beide als het doel voor de server met automatische detectie, maar de gebruiker moet op OK in een bevestigingsbericht tikken. Als u naar EnterpriseEnrollment-s.manage.microsoft.com verwijst, hoeft de gebruiker de extra bevestigingsstap niet uit te voeren. Dit is dus de aanbevolen configuratie

## <a name="alternate-methods-of-redirection-are-not-supported"></a>Alternatieve omleidingsmethoden worden niet ondersteund
Het gebruik van een andere methode dan de CNAME-configuratie wordt niet ondersteund. Het gebruik van een proxyserver om enterpriseenrollment.contoso.com/EnrollmentServer/Discovery.svc om te leiden naar enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc of manage.microsoft.com/EnrollmentServer/Discovery.svc, wordt bijvoorbeeld niet ondersteund.

**Stap 2: CNAME controleren** (optioneel)<br>
1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apparaten** > **Windows** > **Windows-inschrijving** > **CNAME-validatie**.
2. Voer in het vak **Domein** de bedrijfswebsite in en kies **Testen**.

## <a name="tell-users-how-to-enroll-windows-devices"></a>Gebruikers uitleggen hoe ze Windows-apparaten inschrijven
Laat uw gebruikers weten hoe ze hun Windows-apparaten kunnen inschrijven en wat ze kunnen verwachten nadat deze onder beheer zijn gebracht.

> [!NOTE]
> Eindgebruikers moeten toegang hebben tot de bedrijfsportalwebsite via Microsoft Edge om Windows-apps te bekijken die u hebt toegewezen voor specifieke versies van Windows. Andere browsers, zoals Google Chrome, Mozilla Firefox en Internet Explorer bieden geen ondersteuning voor deze manier van filteren.

Zie [Uw Windows-apparaat inschrijven bij Intune](../user-help/windows-enrollment-company-portal.md) voor inschrijvingsinstructies voor eindgebruikers. U kunt gebruikers ook verwijzen naar het artikel [Welke gegevens kan mijn bedrijf zien wanneer ik mijn apparaat inschrijf in Intune?](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md)

>[!IMPORTANT]
> Als u automatische MDM-inschrijving niet hebt ingeschakeld maar Windows 10-apparaten hebt die zijn samengevoegd in Azure AD, worden na de inschrijving twee records weergegeven in de Intune-console. U kunt dit gedrag beëindigen. Hiervoor moeten gebruikers met samengevoegde apparaten in Azure AD met hetzelfde account naar **Accounts** > **Toegang tot werk- of schoolaccount** en **Verbinden** gaan. 

Zie [Bronnen over de eindgebruikerservaring in Microsoft Intune](../fundamentals/end-user-educate.md) voor meer informatie over taken voor eindgebruikers.

## <a name="registration-and-enrollment-cnames"></a>CNAME's voor registratie en inschrijving
Azure Active Directory heeft een andere CNAME die wordt gebruikt voor apparaatregistratie voor iOS-/iPadOS-, Android- en Windows-apparaten. Voor voorwaardelijke toegang van Intune moeten apparaten worden geregistreerd, ook wel 'aan werkplek toegevoegd' genoemd. Als u voorwaardelijke toegang wilt gebruiken, moet u ook de CNAME voor EnterpriseRegistration configureren voor elke bedrijfsnaam die u hebt.

| Type | Hostnaam | Verwijst naar | TTL |
| --- | --- | --- | --- |
| CNAME | EnterpriseRegistration. company_domain.com | EnterpriseRegistration.windows.net | 1 uur|

Zie [Apparaat-id's beheren met de Azure-portal voor meer informatie over het registreren van apparaten.](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal)

## <a name="windows-10-auto-enrollment-and-device-registration"></a>Windows 10 auto-enrollment and device registration (Automatische inschrijving en apparaatregistratie in Windows 10)

Deze sectie is van toepassing op klanten van Cloud voor de Amerikaanse overheid.

Hoewel het maken van CNAME-DNS-vermeldingen optioneel is, maken CNAME-records het voor gebruikers makkelijker om zich in te schrijven. Als er geen CNAME-inschrijvingsrecord wordt gevonden, wordt gebruikers gevraagd de MDM-servernaam (enrollment.manage.microscoft.us) handmatig in te voeren.

| Type | Hostnaam | Verwijst naar | TTL |
| --- | --- | --- | --- |
| CNAME | EnterpriseEnrollment.bedrijfsdomein.com | EnterpriseEnrollment-s.manage.microsoft.us | 1 uur|
|CNAME | EnterpriseRegistration.bedrijfsdomein.com | EnterpriseRegistration.windows.net | 1 uur |


## <a name="next-steps"></a>Volgende stappen

- [Overwegingen bij het beheren van Windows-apparaten met Intune in Azure](../fundamentals/intune-legacy-pc-client.md).

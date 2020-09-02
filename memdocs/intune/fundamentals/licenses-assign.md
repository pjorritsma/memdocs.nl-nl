---
title: Microsoft Intune-licenties toewijzen
description: Licenties toewijzen aan gebruikers zodat ze kunnen inschrijven bij Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/12/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: bb4314ea-88b5-44d3-92ce-4c6aff0587a4
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d770ee040044cdaee9e4a717e9ee3045874952b2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88906902"
---
# <a name="assign-licenses-to-users-so-they-can-enroll-devices-in-intune"></a>Licenties toewijzen aan gebruikers zodat ze kunnen apparaten inschrijven bij Intune

U moet eerst aan elke gebruiker een Intune-licentie toewijzen voordat gebruikers hun apparaten bij Intune kunnen inschrijven, ongeacht of u handmatig gebruikers toevoegt of deze synchroniseert vanuit uw on-premises Active Directory. Zie [Licenties met Intune](licenses.md) voor een lijst met licenties.

> [!NOTE]
> Gebruikers die het Intune-beveiligingsbeleid voor apps hebben toegewezen en hun apparaten niet hebben geregistreerd bij Microsoft Intune, hebben ook een Intune-licentie nodig om beleid te ontvangen.

## <a name="assign-an-intune-license-microsoft-endpoint-manager-admin-center"></a>Een Intune-licentie toewijzen in het beheercentrum voor Microsoft Endpoint Manager

U kunt het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) gebruiken om handmatig cloudgebruikers toe te voegen en licenties toe te wijzen aan zowel cloudgebruikersaccounts als accounts die vanuit uw on-premises Active Directory Domain Services zijn gesynchroniseerd met Azure Active Directory.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Gebruikers** > **Alle gebruikers** > selecteer de gebruiker > **Licenties** > **Toewijzingen**.

2. Kies het vak voor **Intune** > **Opslaan**. Als u de Enterprise Mobility + Security E5 of een andere licentie wilt gebruiken, kiest u dat vak.

   ![Schermafbeelding van het gedeelte Productlicenties in het Microsoft 365-beheercentrum.](./media/licenses-assign/mem-assign-license.png)

3. Het gebruikersaccount beschikt nu over de benodigde machtigingen om de service te gebruiken en apparaten in te schrijven bij het beheer.

> [!NOTE]
> Gebruikers worden pas weergegeven in de klassieke Intune-portal nadat ze een apparaat hebben ingeschreven met behulp van de Intune-pc-client. U kunt ook een groep gebruikers in één keer bewerken door de optie voor het toevoegen of vervangen van een licentie voor alle geselecteerde gebruikers te selecteren.

## <a name="assign-an-intune-license-by-using-azure-active-directory"></a>Een Intune-licentie toewijzen met behulp van Azure Active Directory

U kunt ook Intune-licenties aan gebruikers toewijzen met behulp van Azure Active Directory. Raadpleeg het artikel [License users in Azure Active Directory](/azure/active-directory/active-directory-licensing-group-assignment-azure-portal) (Gebruikers een licentie verlenen via Azure Active Directory) voor meer informatie. 

## <a name="use-school-data-sync-to-assign-licenses-to-users-in-intune-for-education"></a>Schoolgegevens synchroniseren gebruiken om licenties toe te wijzen aan gebruikers met Intune for Education

Als uw organisatie een onderwijsinstelling is, kunt u met Schoolgegevens synchroniseren(SDS) licenties voor Intune for Education toewijzen aan gesynchroniseerde gebruikers. Kies het selectievakje Intune for Education tijdens het instellen van uw SDS-profiel.  

![Schermafbeelding van de SDS-profielinstelling](./media/licenses-assign/i4e-sds-profile-setup-setting.png)

Als u een licentie voor Intune for Education toewijst, zorg er dan voor dat er ook een Intune A Direct-licentie wordt toegewezen.

![Schermafbeelding van het instellen van de productlicentie](./media/licenses-assign/i4e-set-licenses.png)

Zie [Overzicht van Schoolgegevens synchroniseren](https://support.office.com/article/Overview-of-School-Data-Sync-and-Classroom-f3d1147b-4ade-4905-8518-508e729f2e91) voor meer informatie over SDS.

## <a name="how-user-and-device-licenses-affect-access-to-services"></a>Invloed van gebruikers en apparaatlicenties op toegang tot services

* Elke **gebruiker** aan wie u een gebruikerslicentie voor software toewijst, kan de onlineservices en bijbehorende software (inclusief System Center-software) openen en gebruiken voor het beheren van toepassingen en maximaal 15 MDM-apparaten. De Intune-pc-agent staat 5 fysieke en 1 virtuele machine per gebruikerslicentie toe.
* U kunt los van gebruikerslicenties voor alle apparaten licenties kopen. Apparaatlicenties hoeven niet te worden toegewezen aan de apparaten. Elk apparaat dat toegang heeft tot en gebruikmaakt van de onlineservices en bijbehorende software (inclusief System Center-software) moet een apparaatlicentie hebben.
* Als een apparaat wordt gebruikt door meer dan een gebruiker, is voor elke gebruiker een apparaatlicentie voor de software vereist of is voor alle gebruikers een gebruikerslicentie voor software vereist.

## <a name="understanding-the-type-of-licenses-you-have-purchased"></a>Inzicht in het type licenties dat u hebt aangeschaft

Hoe u Intune hebt aangeschaft, bepaalt de gegevens van uw abonnementen:

- Als u Intune via een Enterprise Agreement hebt aangeschaft, kunt u uw abonnementsgegevens vinden in de portal voor volumelicenties onder **Abonnementen**.
- Als u Intune via een Cloud Solution Provider hebt aangeschaft, kunt u contact opnemen met uw reseller.
- Als u Intune met een CC# of factuur hebt aangeschaft, zijn uw licenties op gebruikers gebaseerd.

## <a name="use-powershell-to-selectively-manage-ems-user-licenses"></a>PowerShell gebruiken om EMS-gebruikerslicenties selectief te beheren
In organisaties die gebruikmaken van Enterprise Mobility + Security (voorheen Enterprise Mobility Suite) van Microsoft, werken mogelijk gebruikers die alleen Azure Active Directory Premium of Intune-services in het EMS-pakket nodig hebben. Met [Azure Active Directory PowerShell-cmdlets](/previous-versions/azure/jj151815(v=azure.100)) kunt u één service of een subset van services toewijzen.

Als u selectief gebruikerslicenties voor EMS-services wilt toewijzen, opent u PowerShell als beheerder op een computer waarop de [Azure Active Directory-module voor Windows PowerShell](/previous-versions/azure/jj151815(v=azure.100)#bkmk_installmodule) is geïnstalleerd. U kunt PowerShell installeren op een lokale computer of op de ADFS-server.

U moet een nieuwe licentie-SKU-definitie maken die alleen van toepassing is op de gewenste serviceplannen. Daarvoor schakelt u de plannen uit die u niet wilt toepassen. U kunt bijvoorbeeld een licentie-SKU-definitie maken waarmee geen licentie voor Intune wordt toegewezen. Typ het volgende om een lijst met beschikbare services weer te geven:

```powershell
(Get-MsolAccountSku | Where {$_.SkuPartNumber -eq "EMS"}).ServiceStatus
```

U kunt de volgende opdracht uitvoeren om het Intune-serviceplan uit te sluiten. Met dezelfde methode kunt u een complete beveiligingsgroep uitbreiden. U kunt echter ook gedetailleerdere filters gebruiken.

**Voorbeeld 1**<br>
Maak een nieuwe gebruiker via de opdrachtregel en wijs een EMS-licentie toe zonder het Intune-gedeelte van de licentie in te schakelen:

```powershell
Connect-MsolService

New-MsolUser -DisplayName "Test User" -FirstName FName -LastName LName -UserPrincipalName user@<TenantName>.onmicrosoft.com –Department DName -UsageLocation US

$CustomEMS = New-MsolLicenseOptions -AccountSkuId "<TenantName>:EMS" -DisabledPlans INTUNE_A
Set-MsolUserLicense -UserPrincipalName user@<TenantName>.onmicrosoft.com -AddLicenses <TenantName>:EMS -LicenseOptions $CustomEMS
```

Controleer met:

```powershell
(Get-MsolUser -UserPrincipalName "user@<TenantName>.onmicrosoft.com").Licenses.ServiceStatus
```

**Voorbeeld 2**<br>
Schakel het Intune-gedeelte van de EMS-licentie uit voor een gebruiker aan wie al een licentie is toegewezen:

```powershell
Connect-MsolService

$CustomEMS = New-MsolLicenseOptions -AccountSkuId "<TenantName>:EMS" -DisabledPlans INTUNE_A
Set-MsolUserLicense -UserPrincipalName user@<TenantName>.onmicrosoft.com -LicenseOptions $CustomEMS
```

Controleer met:

```powershell
(Get-MsolUser -UserPrincipalName "user@<TenantName>.onmicrosoft.com").Licenses.ServiceStatus
```

![PoSH-AddLic-Verify](./media/licenses-assign/posh-addlic-verify.png)
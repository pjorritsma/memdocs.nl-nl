---
title: PFX-certificaatprofielen importeren
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van PFX-bestanden in Configuration Manager om gebruikersspecifieke certificaten te genereren die ondersteuning bieden voor versleutelde gegevens uitwisseling.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3304d480f0650191a784a9152ae464e81c2207a1
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906399"
---
# <a name="import-pfx-certificate-profiles"></a>PFX-certificaatprofielen importeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Meer informatie over het maken van een certificaat profiel door referenties van externe certificaten te importeren. In dit artikel wordt specifieke informatie over PFX-certificaat profielen (Personal Information Exchange) uitgelegd. Zie [certificaat profielen](../../protect/deploy-use/introduction-to-certificate-profiles.md)voor meer informatie over het maken en configureren van deze profielen.

Configuration Manager ondersteunt verschillende soorten certificaat archieven voor verschillende apparaten en versies van besturings systemen. Bijvoorbeeld Windows 10 en Windows 10 Mobile. Zie [vereisten voor certificaat profielen](../../protect/plan-design/prerequisites-for-certificate-profiles.md)voor meer informatie.

Gebruik Configuration Manager om certificaat referenties te importeren en vervolgens PFX-bestanden op apparaten in te richten. U kunt deze bestanden gebruiken om gebruikersspecifieke certificaten te genereren voor de ondersteuning van versleutelde gegevens uitwisseling.

> [!TIP]  
> Zie het blog bericht [How to Create en DEPLOY pfx Certificate profiles in Configuration Manager](https://docs.microsoft.com/archive/blogs/karanrustagi/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager)(Engelstalig) voor stapsgewijze instructies voor het uitvoeren van dit proces.  

## <a name="create-a-profile"></a>Een profiel maken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit, vouw **toegang tot bedrijfs bronnen**uit en selecteer **certificaat profielen**.

1. Selecteer **certificaat profiel maken**op het tabblad **Start** van het lint in de groep **maken** .

1. Geef op de pagina **Algemeen** van de **wizard Certificaat profiel maken**de volgende informatie op:  

    - **Naam**: voer een unieke naam in voor het certificaatprofiel. U kunt maximaal 256 tekens gebruiken.  

    - **Beschrijving**: Geef een beschrijving op die een overzicht geeft van het certificaat profiel waarmee het kan worden geïdentificeerd in de Configuration Manager-console. U kunt maximaal 256 tekens gebruiken.  

1. Selecteer **Personal Information Exchange-PKCS #12 (PFX) instellingen-importeren**. Met deze optie wordt informatie uit een bestaand certificaat geïmporteerd om een certificaat profiel te maken.

    > [!NOTE]
    > De optie **maken** vraagt een certificaat namens een gebruiker aan bij een verbonden on-premises certificerings instantie (CA). Dit proces levert vervolgens veilig het certificaat aan clients als PFX-bestanden. Zie [PFX-certificaat profielen maken met behulp van een certificerings instantie](create-pfx-certificate-profiles.md)voor meer informatie.

1. Geef op de pagina **PFX-certificaat** van de **wizard Certificaat profiel maken**de sleutelarchiefprovider op:

    - **Installeren op TPM (Trusted Platform Module) indien aanwezig**  
    - **Installeren in Trusted Platform Module (TPM), anders niet**
    - **Installeren in Windows hello voor bedrijven, anders niet**
    - **Installeren op sleutelarchiefprovider van software**

1. Kies op de pagina **ondersteunde platforms** de ondersteunde platformen.

1. Voltooi de wizard.

## <a name="deploy-the-profile"></a>Het profiel implementeren

Nadat u een certificaat profiel hebt gemaakt en ingericht, is het nu beschikbaar in het knoop punt **certificaat profielen** . Zie voor meer informatie over het implementeren van de implementatie van [resource toegangs profielen](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="assign-primary-users"></a>Primaire gebruikers toewijzen

Wijs de doel gebruikers toe als primaire gebruikers op de Windows 10-apparaten waarop u de PFX-certificaten moet installeren. Zie [gebruikers affiniteit met apparaat](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie.

## <a name="provision-a-create-pfx-script"></a>Een PFX-script maken

Als u een PFX-certificaat wilt importeren, gebruikt u de volgende Configuration Manager Power shell-cmdlets voor het inrichten van een PFX-script maken:

- [Get-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmclientcertificatepfx?view=sccm-ps)
- [Import-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmclientcertificatepfx?view=sccm-ps)
- [Remove-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmclientcertificatepfx?view=sccm-ps)

### <a name="example-script"></a>Voorbeeldscript

Als u een PFX-bestand wilt inrichten voor een certificaat profiel voor een gebruiker, opent u Power shell op een computer met de Configuration Manager-console. Wijzig de variabelen met waarden uit uw omgeving.

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>Zie ook

[Een nieuw certificaat profiel maken](../../protect/deploy-use/create-certificate-profiles.md)

[PFX-certificaat profielen maken met behulp van een certificerings instantie](create-pfx-certificate-profiles.md)

[Wi-Fi-, VPN-, e-mail- en certificaatprofielen implementeren](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)

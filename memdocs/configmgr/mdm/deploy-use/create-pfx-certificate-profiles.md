---
title: PFX-certificaatprofielen maken
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van PFX-bestanden in Configuration Manager om gebruikersspecifieke certificaten te genereren die ondersteuning bieden voor versleutelde gegevens uitwisseling.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711173"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>PFX-certificaat profielen maken met behulp van een certificerings instantie

*Van toepassing op: Configuration Manager (huidige vertakking)*

Meer informatie over het maken van een certificaat profiel dat gebruikmaakt van een certificerings instantie voor referenties. In dit artikel wordt specifieke informatie over PFX-certificaat profielen (Personal Information Exchange) uitgelegd. Zie [certificaat profielen](../../protect/deploy-use/introduction-to-certificate-profiles.md)voor meer informatie over het maken en configureren van deze profielen.

Met Configuration Manager kunt u een PFX-certificaat profiel maken met behulp van referenties die zijn uitgegeven door een certificerings instantie. U kunt micro soft of uw vertrouwens bevoegdheid kiezen als uw certificerings instantie. Wanneer een PFX-bestand wordt geïmplementeerd op gebruikers apparaten, worden er gebruikersspecifieke certificaten gegenereerd ter ondersteuning van versleutelde gegevens uitwisseling.

Zie [PFX-certificaat profielen importeren](import-pfx-certificate-profiles.md)voor informatie over het importeren van certificaat referenties uit bestaande certificaat bestanden.

## <a name="prerequisites"></a>Vereisten

Voordat u begint met het maken van een certificaat profiel, moet u ervoor zorgen dat de benodigde vereisten gereed zijn. Zie [vereisten voor certificaat profielen](../../protect/plan-design/prerequisites-for-certificate-profiles.md)voor meer informatie. Voor PFX-certificaat profielen hebt u bijvoorbeeld een site systeemrol voor het [certificaat registratiepunt](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point) nodig.

## <a name="create-a-profile"></a>Een profiel maken  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit, vouw **toegang tot bedrijfs bronnen**uit en selecteer **certificaat profielen**.

1. Selecteer **certificaat profiel maken**op het tabblad **Start** van het lint in de groep **maken** .

1. Geef op de pagina **Algemeen** van de **wizard Certificaat profiel maken**de volgende informatie op:  

    - **Naam**: voer een unieke naam in voor het certificaatprofiel. U kunt maximaal 256 tekens gebruiken.  

    - **Beschrijving**: Geef een beschrijving op die een overzicht geeft van het certificaat profiel waarmee het kan worden geïdentificeerd in de Configuration Manager-console. U kunt maximaal 256 tekens gebruiken.  

1. Selecteer **Personal Information Exchange-PKCS #12-instellingen (PFX)-maken**. Met deze optie wordt een certificaat aangevraagd namens een gebruiker van een verbonden on-premises certificerings instantie (CA). Kies uw certificerings instantie: **micro soft** of **Entrust datacard**.

    > [!NOTE]
    > De optie **importeren** haalt gegevens op uit een bestaand certificaat om een certificaat profiel te maken. Zie [PFX-certificaat profielen importeren](import-pfx-certificate-profiles.md)voor meer informatie.

1. Selecteer op de pagina **ondersteunde platforms** de versies van het besturings systeem die dit certificaat profiel ondersteunt. Zie [ondersteunde versies van besturings systemen voor clients en apparaten](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)voor meer informatie over de ondersteunde versies van besturings systemen voor uw versie van Configuration Manager.

1. Kies op de pagina **certificerings instanties** het certificaat registratiepunt (CRP) om de PFX-certificaten te verwerken:

    1. **Primaire site**: Kies de server met de CRP-rol voor de ca.
    1. **Certificerings instanties**: Selecteer de relevante certificerings instantie.

    Zie [certificaat infrastructuur](../../protect/deploy-use/certificate-infrastructure.md)voor meer informatie.

De instellingen op de **PFX-certificaat** pagina variëren, afhankelijk van de geselecteerde certificerings instantie op de pagina **Algemeen** :

- [Micro soft-CA](#bkmk_microsoft)
- [Entrust Datacard CA](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>**PFX-certificaat** instellingen configureren voor micro soft-ca

1. Kies de certificaat sjabloon voor de naam van het **certificaat sjabloon**.

1. Als u het certificaat profiel voor S/MIME-ondertekening of versleuteling wilt gebruiken, schakelt u het **gebruik van certificaten**in.

    Wanneer u deze optie inschakelt, worden alle PFX-certificaten die aan de doel gebruiker zijn gekoppeld, aan al hun apparaten geleverd. Als u deze optie niet inschakelt, ontvangt elk apparaat een uniek certificaat.  

1. Stel de indeling van de **object naam** in op **algemene naam** of **volledig DN-naam**. Als u niet zeker weet welke u moet gebruiken, neemt u contact op met uw CA-beheerder.

1. Schakel voor de **alternatieve naam**voor het onderwerp het **e-mail adres** en de **UPN (User Principle Name)** in die van toepassing zijn voor uw ca.

1. **Drempel waarde voor verlenging**: Hiermee wordt bepaald wanneer certificaten automatisch worden vernieuwd, op basis van het percentage resterende tijd voordat het verloopt.

1. Stel de **geldigheids periode** van het certificaat in op de levens duur van het certificaat.

1. Schakel **Active Directory publiceren**in wanneer het certificaat registratiepunt Active Directory referenties opgeeft.

1. Als u een of meer Windows 10-ondersteunde platforms hebt geselecteerd:

    1. Stel het **Windows-certificaat archief** in op **gebruiker**. (De optie **lokale computer** implementeert geen certificaten, kies deze niet.)

    1. Selecteer een van de volgende **sleutelarchiefprovider**:

        - **Installeren op TPM (Trusted Platform Module) indien aanwezig**  
        - **Installeren in Trusted Platform Module (TPM), anders niet**
        - **Installeren in Windows hello voor bedrijven, anders niet**
        - **Installeren op sleutelarchiefprovider van software**

1. Voltooi de wizard.

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>**PFX-certificaat** instellingen configureren voor Entrust datacard ca

1. Kies het configuratie profiel voor de **digitale ID-configuratie**. De beheerder van de vertrouwens groep maakt de configuratie opties voor de digitale ID.

1. Als u het certificaat profiel voor S/MIME-ondertekening of versleuteling wilt gebruiken, schakelt u het **gebruik van certificaten**in.

    Wanneer u deze optie inschakelt, worden alle PFX-certificaten die aan de doel gebruiker zijn gekoppeld, aan al hun apparaten geleverd. Als u deze optie niet inschakelt, ontvangt elk apparaat een uniek certificaat.  

1. Als u de **naam van de ondername** tokens wilt toewijzen aan Configuration Manager velden, selecteert u **Format teren**.

    In het dialoog venster **indeling van certificaat naam** worden de variabelen voor de configuratie van de vertrouwens instellingen voor de digitale id Kies voor elke variabelen variabele de juiste Configuration Manager velden.

1. Als u de tokens voor **alternatieve naam** voor het onderwerp wilt toewijzen aan ondersteunde LDAP-variabelen, selecteert u **indeling**.

    In het dialoog venster **indeling van certificaat naam** worden de variabelen voor de configuratie van de vertrouwens instellingen voor de digitale id Kies voor elke verlastings variabele de juiste LDAP-variabele.

1. **Drempel waarde voor verlenging**: Hiermee wordt bepaald wanneer certificaten automatisch worden vernieuwd, op basis van het percentage resterende tijd voordat het verloopt.

1. Stel de **geldigheids periode** van het certificaat in op de levens duur van het certificaat.

1. Schakel **Active Directory publiceren**in wanneer het certificaat registratiepunt Active Directory referenties opgeeft.

1. Als u een of meer Windows 10-ondersteunde platforms hebt geselecteerd:

    1. Stel het **Windows-certificaat archief** in op **gebruiker**. (De optie **lokale computer** implementeert geen certificaten, kies deze niet.)

    1. Selecteer een van de volgende **sleutelarchiefprovider**:

        - **Installeren op TPM (Trusted Platform Module) indien aanwezig**  
        - **Installeren in Trusted Platform Module (TPM), anders niet**
        - **Installeren in Windows hello voor bedrijven, anders niet**
        - **Installeren op sleutelarchiefprovider van software**

1. Voltooi de wizard.

## <a name="deploy-the-profile"></a>Het profiel implementeren

Nadat u een certificaat profiel hebt gemaakt, is het nu beschikbaar in het knoop punt **certificaat profielen** . Zie voor meer informatie over het implementeren van de implementatie van [resource toegangs profielen](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="see-also"></a>Zie ook

[Een nieuw certificaat profiel maken](../../protect/deploy-use/create-certificate-profiles.md)

[PFX-certificaatprofielen importeren](import-pfx-certificate-profiles.md)

[Wi-Fi-, VPN-, e-mail- en certificaatprofielen implementeren](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)

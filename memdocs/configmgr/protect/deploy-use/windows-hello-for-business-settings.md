---
title: Instellingen voor Windows Hello voor Bedrijven
titleSuffix: Configuration Manager
description: Meer informatie over hoe u Windows hello voor bedrijven integreert met Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c60f30e306c6ff52849cfcdd4696d67a7d26f395
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722233"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Instellingen voor Windows hello voor bedrijven in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1245704-->
Configuration Manager integreert met Windows hello voor bedrijven. (Deze functie was voorheen bekend als Microsoft Passport for Work.) Windows hello voor bedrijven is een alternatieve aanmeldings methode voor Windows 10-apparaten. Er wordt gebruikgemaakt van Active Directory of een Azure Active Directory Azure AD-account om een wacht woord, Smart Card of virtuele Smart Card te vervangen. Met Hello voor bedrijven kunt u een *gebruikers beweging* gebruiken om u aan te melden in plaats van een wacht woord. Een gebaar van de gebruiker is mogelijk een pincode, biometrische verificatie of een extern apparaat zoals een vingerafdruk lezer.

> [!Important]  
> Vanaf versie 1910 wordt verificatie op basis van certificaten met instellingen voor Windows hello voor bedrijven in Configuration Manager niet ondersteund. Zie [afgeschafte functies](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie. Verificatie op basis van een sleutel is nog geldig.
>
> De implementatie van de registratie-instantie (ADFS RA) is eenvoudiger, biedt een betere gebruikers ervaring en heeft een meer deterministische certificaat registratie. Active Directory Federation Services Gebruik ADFS RA voor verificatie op basis van certificaten met Windows hello voor bedrijven.
>
> Voor gezamenlijk beheerde apparaten kunt u overwegen om de [werk belasting van het **resource toegangs beleid** ](../../comanage/workloads.md#resource-access-policies) te verplaatsen naar intune. Gebruik vervolgens intune-beleid om deze certificaten te beheren. Zie [werk belastingen overschakelen](../../comanage/how-to-switch-workloads.md)voor meer informatie.

Zie [Windows hello voor bedrijven](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)voor meer informatie.

> [!Note]  
> Configuration Manager schakelt deze optionele functie standaard niet in. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Configuration Manager integreert met Windows hello voor bedrijven op de volgende manieren:  

- Bepalen welke gebaren gebruikers kunnen gebruiken om zich aan te melden.  

- Sla verificatie certificaten op in de SLEUTELARCHIEFPROVIDER van Windows hello voor bedrijven. Zie [certificaat profielen](introduction-to-certificate-profiles.md)voor meer informatie.  

- Maak en implementeer een Windows hello voor bedrijven-profiel om de instellingen te beheren op Windows 10-apparaten die lid zijn van een domein waarop de Configuration Manager-client wordt uitgevoerd. Vanaf versie 1910 kunt u geen authenticatie op basis van certificaten gebruiken. Wanneer u verificatie op basis van een sleutel gebruikt, hoeft u geen certificaat profiel te implementeren.

## <a name="configure-a-profile"></a>Een profiel configureren  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Vouw **instellingen voor naleving**uit, vouw **toegang tot bedrijfs bronnen**uit en selecteer het knoop punt **Windows hello voor bedrijven-profielen** .

1. Selecteer in het lint de optie **Windows hello voor bedrijven-profiel maken** om de wizard Profiel te starten.

1. Geef op de pagina **Algemeen** een naam en een optionele beschrijving op voor dit profiel.

1. Selecteer op de pagina **ondersteunde platforms** de versies van het besturings systeem waarop dit profiel moet worden toegepast.

1. Configureer op de pagina **instellingen** de volgende instellingen:

    - **Windows hello voor bedrijven configureren**: Geef op of dit profiel Hello voor bedrijven kan in-of uitschakelen of niet kan configureren.

    - **Een Trusted Platform Module (TPM) gebruiken**: een TPM biedt een extra laag voor gegevens beveiliging. Kies een van de volgende waarden:  

      - **Vereist**: alleen apparaten met een toegankelijke TPM kunnen Windows hello voor bedrijven inrichten.  

      - **Voor keur**: apparaten proberen eerst een TPM te gebruiken. Als deze niet beschikbaar is, kunnen ze software versleuteling gebruiken.

    - **Verificatie methode**: Stel deze optie in op **niet geconfigureerd** of **op basis van sleutels**.

        > [!NOTE]
        > Vanaf versie 1910 wordt verificatie op basis van certificaten met instellingen voor Windows hello voor bedrijven in Configuration Manager niet ondersteund.

    - **Minimum lengte voor pincode configureren**: als u een minimum lengte voor de pincode van de gebruiker wilt vereisen, schakelt u deze optie in en geeft u een waarde op. Als deze functie is ingeschakeld, is `4`de standaard waarde.

    - **Maximum lengte voor pincode configureren**: als u een maximum lengte voor de pincode van de gebruiker wilt vereisen, schakelt u deze optie in en geeft u een waarde op. Wanneer dit is ingeschakeld, is `127`de standaard waarde.

    - **Verlopen van pincode vereisen (dagen)**: Hiermee geeft u het aantal dagen op voordat de gebruiker de pincode van het apparaat moet wijzigen.

    - **Hergebruik van vorige pincodes voor komen**: gebruikers mogen geen pincodes gebruiken die ze eerder hebben gebruikt.

    - **Hoofd letters in pincode vereisen**: Hiermee geeft u aan of gebruikers hoofd letters moeten bevatten in de pincode voor Windows hello voor bedrijven. U kunt kiezen uit:  

      - **Toegestaan**: gebruikers mogen hoofd letters gebruiken in hun pincode, maar hoeven niet.

      - **Vereist**: gebruikers moeten ten minste één hoofd letter in hun pincode opnemen.  

      - **Niet toegestaan**: gebruikers mogen geen hoofd letters gebruiken in hun pincode.  

    - **Kleine letters in pincode vereisen**: Hiermee geeft u aan of gebruikers kleine letters in de pincode voor Windows hello voor bedrijven moeten bevatten. U kunt kiezen uit:  

      - **Toegestaan**: gebruikers mogen kleine letters gebruiken in hun pincode, maar hoeven dit niet te doen.

      - **Vereist**: gebruikers moeten ten minste één kleine letter in hun pincode opnemen.  

      - **Niet toegestaan**: gebruikers mogen geen kleine letters gebruiken in hun pincode.  

    - **Speciale tekens configureren**: Hiermee geeft u het gebruik van speciale tekens in de pincode. U kunt kiezen uit:  

        > [!NOTE]
        > Speciale tekens zijn onder andere de volgende set:
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **Toegestaan**: gebruikers kunnen speciale tekens gebruiken in hun pincode, maar hoeven dit niet te doen.  

      - **Vereist**: gebruikers moeten ten minste één speciaal teken opnemen in hun pincode.  

      - **Niet toegestaan**: gebruikers mogen geen speciale tekens gebruiken in hun pincode. Dit gedrag is ook als de instelling **niet is geconfigureerd**.  

    - **Het gebruik van cijfers in pincode configureren**: Hiermee geeft u het gebruik van getallen in de pincode op. U kunt kiezen uit:

      - **Toegestaan**: gebruikers kunnen cijfers gebruiken in hun pincode, maar hoeven dit niet te doen.  

      - **Vereist**: gebruikers moeten ten minste één cijfer opnemen in hun pincode.  

      - **Niet toegestaan**: gebruikers kunnen geen cijfers gebruiken in hun pincode.

    - **Biometrische gebaren inschakelen**: gebruik Biometrische verificatie, zoals gezichts herkenning of vinger afdruk. Deze modi zijn een alternatief voor een pincode voor Windows hello voor bedrijven. Gebruikers kunnen nog steeds een pincode configureren als biometrische verificatie mislukt.  

      Als deze instelling is ingesteld op **Ja**, is Biometrische verificatie toegestaan in Windows hello voor bedrijven. Als deze optie is ingesteld op **Nee**, voor komt Windows hello voor bedrijven Biometrische verificatie voor alle account typen.  

    - **Verbeterde anti-adres vervalsing gebruiken**: Hiermee configureert u verbeterde anti-adres vervalsing op apparaten die dit ondersteunen. Indien ingesteld op **Ja**, waar ondersteund, moeten alle gebruikers anti-spoofing gebruiken voor gezichts functies.  

    - **Aanmelding via telefoon gebruiken**: Hiermee configureert u twee ledige verificatie met een mobiele telefoon.

1. Voltooi de wizard.

De volgende scherm afbeelding is een voor beeld van Windows hello voor bedrijven-Profiel instellingen:  

![Wizard Windows hello voor bedrijven-beleid, waarin de lijst met beschik bare instellingen wordt weer gegeven](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>Machtigingen configureren

1. Meld u als domein beheerder of gelijkwaardige referenties aan bij een beveiligd beheer werkstation waarop de volgende optionele functie is geïnstalleerd: RSAT: Active Directory Domain Services en Lightweight Directory Services-Hulpprogram Ma's.

1. Open de console **Active Directory gebruikers en computers** .

1. Selecteer het domein, ga naar het **actie** menu en selecteer **Eigenschappen**.

1. Ga naar het tabblad **beveiliging** en selecteer **Geavanceerd**.

    > [!TIP]
    > Als het tabblad **beveiliging** niet wordt weer gegeven, sluit u het venster Eigenschappen. Ga naar het menu **weer gave** en selecteer **geavanceerde functies**.

1. Selecteer **Toevoegen**.

1. Kies **een principal selecteren** en voer `Key Admins`in.

1. Selecteer in de lijst **van toepassing op** de optie **onderliggende gebruikers objecten**.

1. Selecteer onder aan de pagina **alle wissen**.

1. Selecteer in de sectie **Eigenschappen** de optie **MsDS-KeyCredentialLink lezen**.

1. Selecteer **OK** om uw wijzigingen op te slaan en alle vensters te sluiten.

## <a name="next-steps"></a>Volgende stappen

[Certificaatprofielen](introduction-to-certificate-profiles.md)

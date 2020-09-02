---
title: Nalevingsbeleid voor Jamf-apparaten
titleSuffix: Microsoft Intune
description: Gebruik Microsoft Intune-nalevingsbeleid met voorwaardelijke toegang van Azure Active Directory om met Jamf beheerde apparaten te beveiligen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c87fd2bd-7f53-4f1b-b985-c34f2d85a7bc
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08586879f3523d1188f18e2d7024f32fae83febc
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911196"
---
# <a name="enforce-compliance-on-macs-managed-with-jamf-pro"></a>Nalevingsbeleid afdwingen op Macs die door Jamf Pro worden beheerd

Wanneer u Jamf Pro integreert met Intune, kunt u beleid voor voorwaardelijke toegang gebruiken om naleving op uw Mac-apparaten af te dwingen met de vereisten van uw organisatie. Dit artikel is bedoeld om u te helpen bij de volgende taken:  

- Beleid voor voorwaardelijke toegang maken.
- Jamf Pro configureren voor implementatie van de Intune-bedrijfsportal-app op apparaten die u beheert met Jamf.
- Apparaten configureren voor registratie bij Azure AD wanneer de gebruiker zich aanmeldt bij de Bedrijfsportal-app die ze starten vanuit de selfservice-app van Jamf. Met apparaatregistratie wordt een identiteit in Azure AD gemaakt waarmee het apparaat kan worden geëvalueerd met beleidsregels voor voorwaardelijke toegang om toegang te krijgen tot bedrijfsbronnen.  
 
Voor de procedures in dit artikel is toegang vereist tot de Intune-console en de Jamf Pro-console.
Intune ondersteunt twee methoden om Jamf Pro te integreren, die u afzonderlijk kunt configureren van de procedures in dit artikel:

- Aanbevolen: [De Jamf-cloudconnector gebruiken om Jamf Pro te integreren met Intune](conditional-access-jamf-cloud-connector.md)
- [De integratie van Jamf Pro met Intune handmatig configureren](conditional-access-integrate-jamf.md)

## <a name="set-up-device-compliance-policies-in-intune"></a>Nalevingsbeleid voor apparaten in Intune instellen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Nalevingsbeleid**. Als u een eerder gemaakt beleid gebruikt, selecteert u dat beleid in de-console en gaat u naar de volgende stap van deze procedure. Als u een nieuw beleid wilt maken, selecteert u **Beleid maken** en geeft u vervolgens details op voor een beleid en selecteert u **macOS** bij *Platform*. Configureer *Instellingen* en *Acties voor niet-naleving* om te voldoen aan de vereisten van uw organisatie en selecteer vervolgens **Maken** om het beleid op te slaan.

3. Selecteer **Toewijzingen** in het deelvenster *Overzicht*. Gebruik de beschikbare opties om te configureren welke Azure AD-gebruikers (Azure Active Directory) en beveiligingsgroepen dit beleid ontvangen. **Jamf-integratie met Intune ondersteunt geen nalevingsbeleid voor apparaatgroepen.**

> [!NOTE]
> Jamf-integratie met Intune biedt alleen ondersteuning voor AAD-gebruikersgroepen. Nalevingsbeleid voor apparaten dat is gericht op apparaatgroepen wordt niet toegepast.

4. Wanneer u **Opslaan** selecteert, wordt het beleid geïmplementeerd voor de gebruikers.  

Beleidsregels die u implementeert richten zich op de apparaten die worden gebruikt door de toegewezen gebruikers. Die apparaten worden beoordeeld op compatibiliteit. Compatibele apparaten worden gemarkeerd als compatibel voor de instelling *Vereisen dat het apparaat moet worden gemarkeerd als compatibel* in Azure AD.  

> [!NOTE]
> Voor Intune moet de schijf volledig worden versleuteld om aan het beleid te voldoen.

## <a name="deploy-the-company-portal-app-for-macos-in-jamf-pro"></a>De bedrijfsportal-app voor macOS in Jamf Pro implementeren

Maak een beleid in Jamf Pro om de Intune-bedrijfsportal te implementeren. Met dit beleid wordt de bedrijfsportal-app geïmplementeerd, zodat deze beschikbaar is in de selfservice van Jamf. Maak dit beleid voordat u een beleid voor gebruikers in Jamf Pro maakt om apparaten te registreren bij Azure AD.  

U hebt toegang tot een macOS-apparaat en de Jamf Pro-portal nodig om de volgende procedure te voltooien. 

### <a name="to-deploy-the-company-portal-app"></a>De bedrijfsportal-app implementeren  

1. Download de huidige versie van de [bedrijfsportal-app voor macOS](https://go.microsoft.com/fwlink/?linkid=862280) op een macOS-apparaat, maar installeer deze nog niet. U hebt alleen een kopie van de app nodig zodat u de app kunt uploaden naar Jamf Pro.  

2. Open Jamf Pro en ga naar **Computer management** > **Packages**.

3. Maak een nieuw pakket met de bedrijfsportal-app voor macOS en selecteer **Save**.

4. Open **Computers** > **Policies** en selecteer **New**.

5. Gebruik de nettolading **General** om instellingen voor het beleid te configureren. Deze instellingen zijn:
   - Trigger: selecteer **Enrollment Complete** en **Recurring Check-in**
   - Uitvoeringsfrequentie: selecteer **Once per computer**

6. Selecteer de nettolading **Packages** en klik op **Configure**.

7. Klik op **Add** om het pakket met de bedrijfsportal-app te selecteren.

8. Selecteer **Install** in het contextmenu **Action**.
9. Configureer de instellingen voor het pakket.

10. Selecteer het tabblad **Scope** om op te geven op welke computers de bedrijfsportal-app moet worden geïnstalleerd. Selecteer **Opslaan**. Door het beleid worden apparaten binnen het bereik uitgevoerd de volgende keer dat de geselecteerde trigger op de computer plaatsvindt en voldoet aan de criteria in de nettolading **General**.

## <a name="create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory"></a>Een beleid in Jamf Pro maken waarmee gebruikers hun apparaten met Azure Active Directory kunnen registreren  

Na de [implementatie van de bedrijfsportal](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro) voor macOS via de selfservice van Jamf Pro kunt u het Jamf Pro-beleid maken waarmee het apparaat van een gebruiker wordt geregistreerd bij Azure AD. 

Voor de registratie van het apparaat moet de gebruiker van het apparaat handmatig de app Intune-bedrijfsportal selecteren in de selfservice van Jamf. U wordt aangeraden te [communiceren met uw eindgebruikers](../fundamentals/end-user-educate.md) via e-mail, Jamf Pro-meldingen of een andere methode die door uw organisatie wordt gebruikt, om ervoor te zorgen dat ze deze actie uitvoeren om hun apparaten registreren. 

> [!WARNING]
> Als de bedrijfsportal-app handmatig wordt gestart (bijvoorbeeld via de map Toepassingen of Downloads), wordt het apparaat niet geregistreerd. Als een apparaatgebruiker de bedrijfsportal handmatig start, verschijnt de waarschuwing **AccountNotOnboarded**.

### <a name="to-create-the-registration-policy"></a>Het registratiebeleid maken  

1. Ga in Jamf Pro naar **Computers** > **Policies** en maak een nieuw beleid voor apparaatregistratie.

2. Configureer de nettolading **Microsoft Intune Integration**, inclusief de frequentie voor triggers en uitvoering.

3. Selecteer het tabblad **Scope** en pas het beleid toe op alle doelapparaten.

4. Selecteer het tabblad **Self Service** om het beleid beschikbaar te maken in de selfservice van Jamf. Neem het beleid op in de categorie **Device Compliance**. Klik op **Opslaan**.

## <a name="validate-intune-and-jamf-integration"></a>Intune-integratie met Jamf valideren  

Gebruik de Jamf Pro-console om te controleren of de communicatie tussen Jamf Pro en Microsoft Intune naar behoren verloopt. 

- Ga in Jamf Pro naar **Settings** > **Global Management** > **Microsoft Intune Integration** en selecteer vervolgens **Test**.

    In de console wordt een bericht weergegeven of de verbinding tot stand is gebracht.  

Als de verbindingstest van de Jamf Pro-console mislukt, controleert u de Jamf-configuratie. 


## <a name="removing-a-jamf-managed-device-from-intune"></a>Een door Jamf beheerd apparaat verwijderen uit Intune

Als u een door Jamf beheerd apparaat wilt verwijderen, opent u het beheercentrum voor Microsoft Endpoint Manager en selecteert u **Apparaten** > **Alle apparaten**, selecteert u het apparaat en selecteert u vervolgens **Verwijderen**.  Bulkverwijdering van apparaten kan worden ingeschakeld door meerdere apparaten te selecteren en op **Verwijderen** te klikken.

U vindt meer informatie over [het verwijderen van door Jamf beheerde apparaten in de Jamf Pro-documenten](https://www.jamf.com/jamf-nation/articles/80/unmanaging-computers-while-preserving-their-inventory-information). U kunt ook een ondersteuningsticket indienen met [Jamf-ondersteuning](https://www.jamf.com/support/) voor meer informatie. 

## <a name="next-steps"></a>Volgende stappen

- [Voorwaardelijke toegang in Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal)
- [Aan de slag met voorwaardelijke toegang in Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)
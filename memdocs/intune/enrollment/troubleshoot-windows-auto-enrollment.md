---
title: Problemen oplossen met automatische inschrijving in Windows 10
titleSuffix: Microsoft Intune
description: Ontdek hoe u problemen met automatische inschrijving kunt oplossen.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 8/3/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jchombe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 968aa9b2f7127e9b7f092f36a99b491a75f0b78c
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546863"
---
# <a name="troubleshoot-windows-10-group-policy-based-auto-enrollment-in-intune"></a>Probleem oplossen met automatische, op beleid gebaseerde inschrijving van Windows 10-groepen in Intune

U kunt groepsbeleid gebruiken om automatische inschrijving bij MDM te activeren voor aan een domein gekoppelde Active Directory-apparaten (AD). Zie [Windows 10-apparaten automatisch inschrijven aan de hand van groepsbeleid](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) voor meer informatie over deze functie.

## <a name="verify-the-configuration"></a>De configuratie controleren

Voordat u met de probleemoplossing begint, kunt u het beste eerst controleren of alles goed is geconfigureerd. Als u het probleem niet tijdens de verificatie kunt oplossen, kunt u verder kijken door een aantal belangrijke logboekbestanden te controleren.

- Controleer of er een geldige Intune-licentie is toegewezen aan de gebruiker die het apparaat probeert in te schrijven.

   ![De Intune-licentie controleren](./media/troubleshoot-windows-auto-enrollment/intune-license.png)

- Controleer of automatische inschrijving is ingeschakeld voor alle gebruikers die de apparaten gaan inschrijven in Intune. Zie [Azure AD en Microsoft Intune: automatische MDM-inschrijving in de nieuwe portal](https://docs.microsoft.com/windows/client-management/mdm/azure-ad-and-microsoft-intune-automatic-mdm-enrollment-in-the-new-portal) voor meer informatie.

   ![Automatische inschrijving controleren](./media/troubleshoot-windows-auto-enrollment/verify-auto-enrollment.png)

   - Controleer of het **MDM-gebruikersbereik** is ingesteld op **Alle** om toe te staan dat alle gebruikers een apparaat in Intune kunnen inschrijven.
   - Controleer of het **MDM-gebruikersbereik** is ingesteld op **Geen**. Anders heeft deze instelling een hogere prioriteit dan het MDM-bereik en kunnen er problemen ontstaan.
   - Controleer of de **MDM-detectie-URL** is ingesteld op **https://enrollment.manage.microsoft.com/enrollmentserver/discovery** .

- Controleer of Windows 10, versie 1709 of een latere versie op het apparaat wordt uitgevoerd.

- Controleer of de apparaten zijn ingesteld op  **hybride Azure AD-gekoppeld**. Deze instelling betekent dat de apparaten zowel aan een domein als aan Azure AD zijn toegevoegd.

   Voor het controleren van de instellingen voert u **dsregcmd/status** uit in de opdrachtregel. Controleer daarna de volgende statuswaarden in de uitvoer:

   - Apparaatstatus
 
     ```asciidoc
     AzureAdJoined: YES
     DomainJoined: YES
     ```

   - SSO-status

     ```asciidoc
     AzureAdPrt: YES
     ```

   In de lijst met aan Azure AD toegevoegde apparaten vindt u dezelfde informatie:

   ![Lijst met aan Azure AD toegevoegde apparaten](./media/troubleshoot-windows-auto-enrollment/ad-joined-devices.png)

- U vindt zowel **Microsoft Intune** als  **Microsoft Intune-inschrijving** onder  **Mobiliteit (MDM en MAM)**  in de Azure AD-blade. Als u beide aantreft, moet u automatische-inschrijvingsinstellingen configureren onder  **Microsoft Intune**.

- Controleer of de volgende beleidsinstelling Groepsbeleid is geïmplementeerd op alle apparaten die moeten worden ingeschreven in Intune:

   **Computerconfiguratie** > **Beleidsregels** > **Beheersjablonen** > **Windows-onderdelen** > **MDM** > **Automatische MDM-inschrijving inschakelen met behulp van Azure AD-standaardreferenties**

   U kunt contact opnemen met uw domeinbeheerders om te controleren of de beleidsinstelling Groepsbeleid goed is geïmplementeerd.

- Controleer of het apparaat niet is ingeschreven in Intune met behulp van de klassieke pc-agent.
- Controleer de volgende instellingen in Azure AD en Intune:

   **Bij Azure AD-apparaatinstellingen:**

   ![Azure AD-apparaatinstellingen](./media/troubleshoot-windows-auto-enrollment/device-setting.png)

   - De instelling **Gebruikers mogen apparaten aan Azure AD toevoegen** is ingesteld op **Alle**.
   - Het aantal apparaten waarover een gebruiker in Azure AD beschikt, is niet hoger dan het quotum voor het **Maximumaantal apparaten per gebruiker**.
   
   **Bij registratiebeperkingen in Intune:**

   - Inschrijving van Windows-apparaten is toegestaan.

     ![Toegestane inschrijving van Windows-apparaten](./media/troubleshoot-windows-auto-enrollment/restrictions.png)

## <a name="troubleshooting"></a>Probleemoplossing

Bestudeer de MDM-logboeken op de apparaat op de volgende locatie in Logboeken als het probleem zich blijft voordoen:

**Logboeken Toepassingen en Services** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostic-Provider** > **Beheerder**

Zoek gebeurtenis-id 75 (gebeurtenisbericht MDM automatisch inschrijven: geslaagd). Deze gebeurtenis geeft aan dat de automatische inschrijving is voltooid.

Gebeurtenis-id 75 wordt in de volgende situaties niet aan een logboek toegevoegd:

- De registratie is mislukt.

  Als u deze fout wilt controleren, zoekt u gebeurtenis-id 76 (gebeurtenisbericht: Automatische MDM-inschrijving: Mislukt (onbekende Win32-foutcode: 0x8018002b)). Deze gebeurtenis geeft aan dat een automatische inschrijving is mislukt.

  Zie [Problemen met inschrijving van Windows-apparaten in Microsoft Intune oplossen](https://docs.microsoft.com/intune/troubleshoot-windows-enrollment-errors) om deze fout op te lossen.

- De inschrijving is helemaal niet geactiveerd. In dit geval worden gebeurtenis-id 75 en gebeurtenis-id 76 niet aan een logboek toegevoegd.
  
  Het proces voor automatische inschrijving wordt geactiveerd door de taak **Planning gemaakt door inschrijvingsclient voor automatische inschrijving in MDM vanuit AAD**, te vinden onder **Microsoft** > **Windows** > **EnterpriseMgmt** in Task Scheduler.

  ![De inschrijving is niet geactiveerd](./media/troubleshoot-windows-auto-enrollment/trigger.png)

  Deze taak wordt gemaakt wanneer de beleidsinstelling Groepsbeleid **Automatische MDM-inschrijving inschakelen met Azure AD-standaardreferenties** is geïmplementeerd op het doelapparaat. De taak staat gepland om gedurende één dag om de vijf minuten te worden uitgevoerd.

  Om te controleren of de taak is gestart, controleert u de gebeurtenislogboeken van Task Scheduler onder de volgende locatie in Logboeken:

  **Logboeken van toepassingen en services > Microsoft > Windows > Task Scheduler > Operationeel**

  Wanneer de taak wordt geactiveerd in de Scheduler, wordt gebeurtenis-id 107 aan een logboek toegevoegd.

  Wanneer de taak is voltooid, wordt gebeurtenis-id 102 aan een logboek toegevoegd. De gebeurtenis wordt aan een logboek toegevoegd, of de automatische inschrijving nu wel of niet is gelukt.

  > [!NOTE]
  > U kunt het Task Scheduler-logboek gebruiken om te controleren of automatische inschrijving wordt geactiveerd. U kunt het logboek echter niet gebruiken om te bepalen of automatische inschrijving is gelukt.

  Door de volgende situatie is het mogelijk dat het schema, dat door de inschrijvingsclient is gemaakt voor automatische inschrijving in MDM vanuit de AAD-taak, niet wordt gestart:

  - Het apparaat is al ingeschreven bij een andere MDM-oplossing. In dit geval wordt gebeurtenis-id 7016 in combinatie met foutcode 2149056522 aan een logboek toegevoegd in het gebeurtenislogboek onder **Logboeken van toepassingen en services** > **Microsoft** > **Windows** > **Task Scheduler** > **Operationeel**.

    U lost dit probleem op door de inschrijving van het apparaat in de MDM ongedaan te maken.

  - Er bestaat een probleem met het groepsbeleid. Voer in dit geval de volgende opdracht uit om een update van de Groepsbeleid-instellingen af te dwingen:

    **gpupdate/force**

    Voer aanvullende probleemoplossing uit in Active Directory als het probleem zich blijft voordoen.

## <a name="next-steps"></a>Volgende stappen
[Problemen met Windows-apparaten inschrijven oplossen](troubleshoot-windows-enrollment-errors.md)
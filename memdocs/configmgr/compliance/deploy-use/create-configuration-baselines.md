---
title: Configuratiebasislijnen maken
titleSuffix: Configuration Manager
description: Configuratie basislijnen maken in Configuration Manager die u kunt implementeren in een verzameling.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2028974c166e060f445b255db6c5af707725a3f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712923"
---
# <a name="create-configuration-baselines-in-configuration-manager"></a>Configuratie basislijnen maken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*


Configuratie basislijnen in Configuration Manager bevatten vooraf gedefinieerde configuratie-items en optioneel andere configuratie basislijnen. Nadat u een configuratiebasislijn hebt gemaakt, kunt u deze implementeren bij een verzameling, zodat apparaten in die verzameling de configuratiebasislijn downloaden en naleving ervan beoordelen.  

## <a name="configuration-baselines"></a>Configuratiebasislijn

 Configuratie basislijnen in Configuration Manager kunnen specifieke revisies van configuratie-items bevatten of kunnen worden geconfigureerd om altijd de nieuwste versie van een configuratie-item te gebruiken. Zie [Beheer taken voor configuratie gegevens](../../compliance/deploy-use/management-tasks-for-configuration-data.md)voor meer informatie over configuratie-item revisies.  

 Er zijn twee methoden die u kunt gebruiken om configuratie basislijnen te maken:  

- Configuratiegegevens uit een bestand importeren. Als u de **Wizard Configuratiegegevens importeren**wilt starten, moet u in het knooppunt **Configuratie-items** of **Configuratiebasislijnen** in de werkruimte **Activa en naleving** op **Configuratiegegevens importeren**klikken. Zie [configuratie gegevens importeren](import-configuration-data.md)voor meer informatie.

- Gebruik het dialoogvenster **Configuratiebasislijn maken** om een nieuwe configuratiebasislijn te maken.  

## <a name="create-a-configuration-baseline"></a>Een configuratiebasislijn maken

Gebruik de volgende procedure om een configuratie basislijn te maken met behulp van het dialoog venster **configuratie basislijn maken** :  

1. Klik in de Configuration Manager-console op **activa en naleving** > **instellingen** > **configuratie basislijnen**.  

2. Klik op het tabblad **Start** in de groep **Maken** op **Configuratiebasislijn maken**.  

3. Voer in het dialoogvenster **Configuratiebasislijn maken** een unieke naam en een beschrijving voor de configuratiebasislijn in. U kunt maximaal 255 tekens voor de naam en 512 tekens voor de beschrijving gebruiken.  

4. De lijst **Configuratiegegevens** geeft alle configuratie-items of configuratiebasislijnen weer die in deze configuratiebasislijn zijn opgenomen. Klik op **Toevoegen** om een nieuw configuratie-item of een nieuwe configuratiebasislijn toe te voegen aan de lijst. U kunt kiezen uit de volgende items:  

   - **Configuratie-items**  

   - **Software-updates**  

   - **Configuratie basislijnen**  
     > [!IMPORTANT]
     > U moet elke configuratie basislijn beperken tot Maxi maal 1000 software-updates.
5. Gebruik de lijst **doel wijzigen** om het gedrag op te geven van een configuratie-item dat u hebt geselecteerd in de lijst **configuratie gegevens** . U kunt kiezen uit de volgende items:  

   -   **Vereist**: de configuratie basislijn wordt beoordeeld als niet-compatibel als het configuratie-item niet op een client apparaat wordt gedetecteerd. Als het wordt gedetecteerd, wordt het beoordeeld op naleving  

   -   **Optioneel**: het configuratie-item wordt alleen beoordeeld op naleving als de toepassing waarnaar wordt verwezen op client computers is gevonden. Als de toepassing niet wordt gevonden, wordt de configuratie basislijn niet gemarkeerd als niet-compatibel (alleen van toepassing op configuratie-items van toepassingen).  

   -   **Verboden**: de configuratie basislijn wordt beoordeeld als niet-compatibel als het configuratie-item wordt gedetecteerd op client computers (alleen van toepassing op configuratie-items van toepassingen).  

   > [!NOTE]
   >  De lijst **Doel wijzigen** is alleen beschikbaar als u op de optie **Dit configuratie-item bevat toepassingsinstellingen** hebt geklikt op de pagina **Algemeen** van de **Wizard Configuratie-item maken**.  

6. Gebruik de lijst **Herziening wijzigen** om een specifieke of de nieuwste herziening van het configuratie-item te selecteren om te beoordelen op naleving op clientapparaten, of selecteer **Altijd nieuwste gebruiken** om altijd de nieuwste herziening te gebruiken. Zie [Beheer taken voor configuratie gegevens](../../compliance/deploy-use/management-tasks-for-configuration-data.md)voor meer informatie over configuratie-item revisies.  

7. Als u een configuratie-item uit de configuratie basislijn wilt verwijderen, selecteert u een configuratie-item en klikt u vervolgens op **verwijderen**.  

8. Vanaf versie 1806 selecteert u deze optie als u **deze basis lijn altijd wilt Toep assen op clients die gezamenlijk worden beheerd**. Wanneer dit selectie vakje is ingeschakeld, geldt deze basis lijn ook voor clients die worden beheerd door intune.  Deze uitzonde ring kan worden gebruikt om instellingen te configureren die vereist zijn voor uw organisatie, maar die nog niet beschikbaar zijn in intune.

9. Klik desgewenst op **Categorieën** om categorieën toe te wijzen aan de basis lijn voor zoeken en filteren. 

10. Klik op **OK** om het dialoogvenster **Configuratiebasislijn maken** te sluiten en de configuratiebasislijn te maken.  

>[!NOTE]
> Als u een bestaande basis lijn wijzigt, zoals instelling **altijd deze basis lijn Toep assen voor gezamenlijk beheerde clients**, wordt de versie van de basislijn inhoud verhoogd. Clients moeten de nieuwe versie evalueren om de basislijn rapportage bij te werken.

## <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a><a name="bkmk_CAbaselines"></a>Aangepaste configuratie basislijnen opnemen als onderdeel van de beoordeling van het nalevings beleid
<!--3608345-->
*(Geïntroduceerd in versie 1910)*

Vanaf versie 1910 kunt u evaluatie van aangepaste configuratie basislijnen toevoegen als beoordelings regel voor het nalevings beleid. Wanneer u een configuratie basislijn maakt of bewerkt, hebt u de optie om **deze basis lijn te evalueren als onderdeel van de beoordeling van het nalevings beleid**. Wanneer u een nalevings beleids regel toevoegt of bewerkt, hebt u een voor waarde met de naam **inclusief geconfigureerde basis lijnen in de beoordeling van het nalevings beleid**. Voor gezamenlijk beheerde apparaten en wanneer u intune configureert om de resultaten van de nalevings beoordeling te Configuration Manager als onderdeel van de algemene nalevings status, wordt deze informatie verzonden naar Azure AD. U kunt dit vervolgens gebruiken voor voorwaardelijke toegang tot uw Office 365-resources. Zie [voorwaardelijke toegang met co-beheer](../../comanage/quickstart-conditional-access.md)voor meer informatie.

Ga als volgt te werk om aangepaste configuratie basislijnen op te nemen als onderdeel van de evaluatie van het nalevings beleid:

- Maak en implementeer een nalevings beleid voor een gebruikers verzameling met een regel om [**geconfigureerde basis lijnen op te nemen in de beoordeling van het nalevings beleid**](#bkmk_CA).
- Selecteer [**deze basis lijn evalueren als onderdeel van de beoordeling van het nalevings beleid**](#bkmk_eval-baseline) in een configuratie basislijn die is geïmplementeerd op een verzameling apparaten.

> [!IMPORTANT]
> Zorg ervoor dat u voldoet aan de [vereisten voor co-beheer](../../comanage/overview.md#prerequisites)bij het richten van apparaten die gezamenlijk worden beheerd.

### <a name="example-evaluation-scenario"></a>Voor beeld van een evaluatie scenario

Wanneer een gebruiker deel uitmaakt van een verzameling die is gericht op een nalevings beleid dat de regel voorwaarde bevat, **inclusief geconfigureerde basis lijnen in de beoordeling van het nalevings beleid**, worden alle basis lijnen met de optie **deze basis lijn evalueren als onderdeel van de beoordeling van het nalevings beleid** geselecteerd die zijn geïmplementeerd voor de gebruiker of het apparaat van de gebruiker worden geëvalueerd voor naleving. Bijvoorbeeld:

- `User1`maakt deel uit `User Collection 1`van.
- `User1`gebruikt `Device1`in `Device Collection 1` en `Device Collection 2`.
- `Compliance Policy 1`bevat de voor waarde voor het **evalueren van geconfigureerde basis lijnen in nalevings beleid** en wordt geïmplementeerd naar `User Collection 1`.
- `Configuration Baseline 1`heeft **deze basis lijn geëvalueerd als onderdeel van de beoordeling van het nalevings beleid** geselecteerd en wordt geïmplementeerd naar `Device Collection 1`.
- `Configuration Baseline 2`heeft **deze basis lijn geëvalueerd als onderdeel van de beoordeling van het nalevings beleid** geselecteerd en wordt geïmplementeerd naar `Device Collection 2`.

`Compliance Policy 1` Als in dit scenario wordt geëvalueerd voor `User1` gebruik `Device1`, worden beide `Configuration Baseline 1` en `Configuration Baseline 2` ook geëvalueerd.

- `User1`soms gebruikt `Device2`.
- `Device2`is lid van `Device Collection 2` en `Device Collection 3`.
- `Device Collection 3`is `Configuration Baseline 3` geïmplementeerd, maar **deze basis lijn evalueren als onderdeel van de beoordeling van het nalevings beleid** is niet geselecteerd.

Wanneer `User1` wordt `Device2`gebruikt, `Configuration Baseline 2` wordt alleen geëvalueerd `Compliance Policy 1` als er wordt geëvalueerd.

> [!NOTE]
><!--5582516-->
> Als het nalevings beleid een nieuwe basis lijn evalueert die nog nooit eerder is beoordeeld op de client, kan de niet-naleving worden gerapporteerd. Dit probleem treedt op als de basislijn evaluatie nog steeds wordt uitgevoerd wanneer de naleving wordt geëvalueerd. Klik op **naleving controleren** in **Software Center**om dit probleem op te lossen.

### <a name="create-and-deploy-a-compliance-policy-with-a-rule-for-baseline-compliance-policy-assessment"></a><a name="bkmk_CA"></a>Een nalevings beleid maken en implementeren met een regel voor de beoordeling van het nalevings beleid voor de basis lijn

1. Vouw in de werk ruimte **activa en naleving** de sectie **instellingen voor naleving**uit en selecteer vervolgens het knoop punt **nalevings beleid** .
1. Klik op **nalevings beleid maken** in het lint om de **wizard nalevings beleid maken**weer te geven. 
1. Selecteer op de pagina **Algemeen** de optie **nalevings regels voor apparaten die worden beheerd met de Configuration Manager-client**.
   - Apparaten moeten worden beheerd met de Configuration Manager-client om aangepaste configuratie basislijnen op te nemen als onderdeel van de beoordeling van het nalevings beleid.
1. Selecteer uw platformen op de pagina's met **ondersteunde platforms** .
1. Selecteer op de pagina **regels** de optie **Nieuw**en selecteer vervolgens de **evaluatie voorwaarde geconfigureerde basis lijnen insluiten in nalevings beleid** .

   ![Geconfigureerde basis lijnen in de beoordelings voorwaarde van het nalevings beleid toevoegen](./media/3608345-create-compliance-policy-rule.png)

1. Klik op **OK**en vervolgens op **volgende** om naar de **overzichts** pagina te gaan.
1. Controleer uw selecties en klik op **volgende** en vervolgens op **sluiten**.
1. Klik in het knoop punt **nalevings beleid** met de rechter muisknop op het beleid dat u hebt gemaakt en selecteer **implementeren**.
1. Kies uw verzameling, instellingen voor het genereren van waarschuwingen en het evaluatie schema voor naleving voor het beleid.
1. Klik op **OK** om het nalevings beleid te implementeren.

### <a name="select-a-configuration-baseline-and-check-evaluate-this-baseline-as-part-of-compliance-policy-assessment"></a><a name="bkmk_eval-baseline"></a>Selecteer een configuratie basislijn en controleer de basis lijn evalueren als onderdeel van de evaluatie van het nalevings beleid.

1. Vouw in de werk ruimte **activa en naleving** de sectie **instellingen voor naleving**uit en selecteer vervolgens het knoop punt **configuratie basislijnen** .
1. Klik met de rechter muisknop op een bestaande basis lijn die wordt geïmplementeerd in een apparaat verzameling en selecteer vervolgens **Eigenschappen**. Als dat nodig is, kunt u een nieuwe basis lijn maken.
   - De basis lijn moet worden geïmplementeerd voor een apparaat-verzameling, niet voor een gebruikers verzameling.
1. Schakel de instelling **deze basis lijn evalueren als onderdeel van de beoordeling van het nalevings beleid** in.
   - Zorg ervoor dat voor gezamenlijk beheerde apparaten die intune als de configuratie-instantie van de **apparaat** , de **basis lijn altijd Toep assen, zelfs voor door co beheerde clients** , ook is geselecteerd.
1. Klik op **OK** om de wijzigingen in de configuratie basislijn op te slaan.

   ![Dialoog venster Eigenschappen van configuratie basislijn](./media/3608345-configuration-baseline-properties.png)

### <a name="log-files-for-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Logboek bestanden voor aangepaste configuratie basislijnen als onderdeel van de beoordeling van het nalevings beleid

- ComplianceHandler. log
- SettingsAgent. log
- DCMAgent.log
- CIAgent.log

## <a name="next-steps"></a>Volgende stappen

[Configuratiegegevens importeren](import-configuration-data.md)

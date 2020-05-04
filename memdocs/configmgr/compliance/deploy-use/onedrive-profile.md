---
title: Profielen van OneDrive voor Bedrijven
titleSuffix: Configuration Manager
description: Windows bekende mappen omleiden naar OneDrive voor bedrijven met een OneDrive voor bedrijven-profiel in Configuration Manager.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 47d44c96e0ae63504278c58a5838c54648665505
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712237"
---
# <a name="onedrive-for-business-profiles"></a>Profielen van OneDrive voor Bedrijven

Vanaf Configuration Manager versie 1902 kunt u OneDrive voor bedrijven-profielen maken voor het verplaatsen van bekende Windows-mappen naar OneDrive voor bedrijven. Deze mappen omvatten bureau blad, documenten en afbeeldingen. In elk profiel kunt u instellingen opgeven voor het verplaatsen van de bekende Windows-mappen. Zie [Windows bekende mappen omleiden en verplaatsen naar OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders)voor meer informatie over Onedrive voor bedrijven. <!--3556021-->

## <a name="prerequisites"></a>Vereisten

- [Uw Office 365-Tenant-ID zoeken](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- Implementeer de OneDrive Sync Client-versie 18.111.0603.0004 of hoger. Zie voor meer informatie [OneDrive-Apps implementeren met behulp van Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a>Bekende Windows-mappen naar OneDrive verplaatsen
<!--3556021-->
Gebruik Configuration Manager om bekende mappen van Windows te verplaatsen naar OneDrive voor bedrijven. Deze mappen omvatten bureau blad, documenten en afbeeldingen. Als u uw Windows 10-upgrades wilt vereenvoudigen, implementeert u deze instellingen voor Windows 7-clients voordat u een taken reeks implementeert. 

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit en selecteer het knoop punt **OneDrive voor bedrijven-profielen** .  

   ![Knoop punt voor OneDrive voor bedrijven-profielen](media/onedrive-for-business-profiles-node.png)
2. Selecteer in het lint het **profiel OneDrive voor bedrijven maken**.  

3. Geef een naam op om dit beleid aan te duiden en selecteer **volgende**.  

4. Selecteer de platformen die worden ingericht met het OneDrive voor bedrijven-profiel. Klik op **volgende**wanneer u klaar bent met het selecteren van de platformen.

    ![Platforms selecteren voor het OneDrive voor bedrijven-profiel](media/onedrive-for-business-profile-select-platforms.png) 

5. Op de pagina **instellingen** :

    1. Geef uw Office 365-Tenant-ID op.  

    2. Selecteer een van de volgende opties om de bekende mappen naar OneDrive te verplaatsen:  

        - **Gebruikers vragen om Windows bekende mappen te verplaatsen naar OneDrive**: met deze optie ziet de gebruiker een wizard voor het verplaatsen van de bestanden. Als ze ervoor kiezen om het verplaatsen van hun mappen uit te stellen of te weigeren, worden ze door OneDrive regel matig geherinnert.  

        - **Windows bekende mappen op de achtergrond verplaatsen naar onedrive**: wanneer dit beleid van toepassing is op het apparaat, worden de bekende mappen door de OneDrive-client automatisch omgeleid naar OneDrive voor bedrijven.  

            - **Melding voor gebruikers weer geven nadat mappen zijn omgeleid**: als u deze optie inschakelt, wordt de gebruiker door de OneDrive-client op de hoogte gebracht nadat de mappen zijn verplaatst.  

    3. **Voor komen dat gebruikers hun herkende Windows-mappen weer naar hun PC omleiden**: Hiermee schakelt u de optie in OneDrive voor bedrijven op de client uit zodat gebruikers deze mappen weer naar het apparaat kunnen verplaatsen.  

       ![Instellingen voor het verplaatsen van bekende mappen in OneDrive voor bedrijven](media/onedrive-for-business-profile-move-folder-settings.png)

6. Voltooi de wizard en implementeer het beleid.  


## <a name="deploy-the-onedrive-for-business-profile"></a>Het OneDrive voor bedrijven-profiel implementeren

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit en selecteer het knoop punt **OneDrive voor bedrijven-profielen** .  


2. Selecteer het profiel en selecteer vervolgens **implementeren** in het lint.

3. Geef de volgende instellingen op voor uw implementatie:

   1. **Verzameling**: Klik op **Bladeren...** en selecteer vervolgens de verzameling waarvoor u het profiel wilt implementeren.  
   1. **Waarschuwing genereren**:

      - **Wanneer naleving lager is dan**: minimum percentage van client compatibiliteit om te onderhouden, anders wordt er een waarschuwing gegenereerd.
      -  **Datum en tijd**: de datum waarschuwingen worden eerst gegenereerd op basis van de naleving van het profiel.
      - **System Center Operations Manager waarschuwing genereren**: een nalevings waarschuwing verzenden naar System Center Operations Manager.
   1. **Planning**:

      - **Eenvoudig schema**: deze instelling maakt standaard gebruik van een eenvoudig schema om elke zeven dagen de evaluatie van de naleving te starten.
      - **Aangepaste planning**: definiëren wanneer de nalevings evaluatie moet worden uitgevoerd. De start tijd is gebaseerd op de lokale tijd voor de computer die de Configuration Manager-console uitvoert op het moment dat u de planning maakt of u kunt UTC gebruiken.
 
      ![OneDrive voor bedrijven-profiel implementeren](media/onedrive-for-business-deploy-profile.png)

4. Klik op **OK** om het OneDrive voor bedrijven-profiel te implementeren.


## <a name="next-steps"></a>Volgende stappen

[Profielen voor externe verbindingen maken](create-remote-connection-profiles.md)

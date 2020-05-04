---
title: 'Algemene taken voor configuratie basislijnen '
titleSuffix: Configuration Manager
description: Meer informatie over het maken en implementeren van Configuration Manager configuratie basislijnen.
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52e83639029db9eeb4ef64657e70e3dc11aab8f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712202"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-configuration-manager"></a>Algemene taken voor het maken en implementeren van configuratie basislijnen met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit onderwerp bevat algemene scenario's voor informatie over het maken en implementeren van Configuration Manager configuratie basislijnen.  

 Als u al bekend bent met de instellingen voor naleving, vindt u gedetailleerde documentatie over alle functies die u gebruikt in de onderwerpen [configuratie basislijnen maken](../../compliance/deploy-use/create-configuration-baselines.md) en [configuratie basislijnen implementeren](../../compliance/deploy-use/deploy-configuration-baselines.md) .  

 Voordat u begint, leest u aan de [slag met nalevings instellingen](../../compliance/get-started/get-started-with-compliance-settings.md) voor een aantal basis beginselen van nalevings instellingen en kunt u ook het [plan voor de nalevings instellingen lezen en configureren](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) om de benodigde vereisten te implementeren.  

## <a name="create-a-configuration-baseline"></a>Een configuratiebasislijn maken  
 In dit voor beeld hebt u een configuratie-item gemaakt voor alleen Windows 10-Pc's waarop de Configuration Manager-client wordt uitgevoerd.  

 Dit configuratie-item dwingt een vereist wachtwoord op Windows 10-computers af van ten minste 6 tekens. De naam van het configuratie-item is **Windows 10-wachtwoordafdwinging**.  

Gebruik de volgende procedure om te leren hoe u dit configuratie-item toevoegt aan een configuratie basislijn om dit voor te bereiden voor implementatie.  

1. Klik in de Configuration Manager-console op **activa en naleving** > **instellingen** > **configuratie basislijnen**.  

2. Klik op het tabblad **Start** in de groep **Maken** op **Configuratiebasislijn maken**.  

3. Configureer in het dialoog venster **configuratie basislijn maken** de volgende instellingen:  

   -   **Naam** : voer **Windows 10-wachtwoorden** (of een andere naam van uw keuze) in  

4. Klik op**configuratie-items** **toevoegen** > .  

5. Selecteer in het dialoogvenster **Configuratie-items toevoegen** het configuratie-item **Windows 10-wachtwoordafdwinging** dat u eerder hebt gemaakt en klik op **Toevoegen**.  

6. Klik op OK om het dialoog venster **configuratie-items toevoegen** te sluiten en terug te keren naar het dialoog venster **configuratie basislijn maken** .

7. Klik op **OK** om het dialoogvenster **Configuratiebasislijn maken** te sluiten.  

   U kunt nu de configuratie basislijn bekijken in het knoop punt **configuratie basislijnen** van de Configuration Manager-console.  

## <a name="deploy-the-configuration-baseline"></a>De configuratie basislijn implementeren  
 In dit voor beeld implementeert u de configuratie basislijn die u in de vorige procedure hebt gemaakt voor een verzameling computers.  

1. Klik in de Configuration Manager-console op **activa en naleving** > **instellingen** > **configuratie basislijnen**.  

2. Selecteer **Windows 10-wachtwoorden**in de lijst met configuratiebasislijnen.  

3. Klik op het tabblad **Start** in de groep **Implementatie** op **Implementeren**.  

4. Configureer de volgende instellingen in het dialoog venster **configuratie basislijnen implementeren** :  

   -   **Geselecteerd configuratiebasislijnen** : zorg ervoor dat de configuratiebasislijn **Windows 10-wachtwoorden** automatisch aan deze lijst is toegevoegd.  

   -   **Regels die niet compliant zijn herstellen, indien ondersteund** : Schakel dit selectie vakje in om ervoor te zorgen dat als de juiste instellingen niet aanwezig zijn op de doel apparaten, worden hersteld door Configuration Manager.  

   -   **Verzameling** : Klik op **Bladeren** om de verzameling computers te kiezen waarop de configuratie basislijn wordt geëvalueerd en hersteld voor naleving. In dit voorbeeld is de configuratiebasislijn geïmplementeerd in de ingebouwde verzameling **Alle desktop- en serverclients** .  

       > [!TIP]  
       >  Het is niet erg als uw verzameling computers of apparaten bevat waarop Windows 10 niet is geïnstalleerd. Zolang u ondersteunde platforms hebt geconfigureerd in het configuratie-item dat u hebt gemaakt, worden alleen Windows 10-Pc's beoordeeld op naleving.  

   -   Configureer zo nodig het schema waarmee de configuratie basislijn wordt geëvalueerd. Gebruik anders de standaardwaarde **7 dagen**.  

5. Klik op **OK** om het dialoogvenster **Configuratiebasislijnen implementeren** te sluiten en implementatie te maken.  

   Als u een beknopt overzicht van de nalevingsstatistieken voor deze implementatie wilt bekijken, klikt u in de werkruimte **Bewaking** op **Implementaties**. Aan de onderkant van het scherm ziet u een grafiek met **nalevings statistieken** .  

## <a name="next-steps"></a>Volgende stappen 

Zie [nalevings instellingen controleren](../../compliance/deploy-use/monitor-compliance-settings.md)voor meer informatie over het bewaken van configuratie basislijnen.  

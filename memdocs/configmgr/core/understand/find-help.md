---
title: Help-informatie zoeken
titleSuffix: Configuration Manager
description: Zoek bronnen voor aanvullende informatie over Configuration Manager.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ae2d837179e3b661bfbfa68d1db429674e20de5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699395"
---
# <a name="find-help-for-using-configuration-manager"></a>Hulp zoeken voor het gebruik van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u de volgende secties met meerdere bronnen voor hulp bij het gebruik van Configuration Manager:  

- [Productdocumentatie](#bkmk_Info)  

- [Feedback over het delen van producten](#product-feedback)  

- [Volg de Configuration Manager team blog](#BKMK_ProductGroupBlog)  

- [Ondersteuningsopties en bronnen van de community](#BKMK_SupportOptions)  

Zie [toegankelijkheids functies](accessibility-features.md)voor meer informatie over de toegankelijkheid van het product.  



##  <a name="product-documentation"></a><a name="bkmk_Info"></a> Product documentatie  

Begin bij de [bibliotheek index](/sccm/)om toegang te krijgen tot de meest actuele product documentatie.  

<a name="BKMK_SearchTips"></a>  

Zie [How to use the docs](use-docs.md)(Engelstalig) voor tips over het zoeken, het geven van feedback en meer informatie over het gebruik van de product documentatie.  



<a name="product-feedback"></a>

## <a name="product-feedback-starting-with-version-1806"></a><a name="BKMK_1806Feedback"></a> Product feedback vanaf versie 1806

Vanaf Configuration Manager versie 1806 kunt u rechtstreeks vanuit de-console product feedback verzenden. Als u logboeken wilt toevoegen, gebruikt u de [feedback hub](#BKMK_FeedbackHub). U kunt het volgende doen: <!--1357542-->

- **Glim lach verzenden**: feedback verzenden over wat u leuk vindt.
- **Een frons verzenden**: feedback verzenden over wat u niet bevalt.
- **Een suggestie verzenden**: gaat u naar de [UserVoice-website](https://configurationmanager.uservoice.com/) om uw idee te delen.

  ![Feedback verzenden in Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile-or-send-a-frown"></a>Glim lach verzenden of frons verzenden

Als u feedback wilt geven over iets dat u leuk vindt, volgt u de onderstaande instructies:

1. Klik in de rechter bovenhoek van de console op het lachebekje gezicht.
2. Selecteer in de vervolg keuzelijst **een glim lach verzenden** of **frons verzenden**.
3. Gebruik het tekstvak om uit te leggen wat u vindt of wat u niet bevalt. 
4. Kies of u uw e-mail adres en een scherm opname wilt delen.
5. Klik op **Feedback verzenden**
     - Als u geen verbinding met internet hebt, klikt u onderaan op **Opslaan** . Volg de instructies in de sectie [Feedback verzenden die u hebt opgeslagen voor een latere verzen](#BKMK_NoInternet) ding om deze naar micro soft te verzenden. 

![Feedback formulier verzenden in Configuration Manager 1806](media/1806-feedback-form.png)

#### <a name="status-messages-for-send-a-smile"></a>Status berichten voor een glim lach verzenden
<!--5891852-->
Vanaf Configuration Manager 2002, wanneer u **een glim lach verzendt** of **een frons verzendt**, wordt een status bericht gemaakt wanneer de feedback wordt verzonden. Deze verbetering bevat een overzicht van:
- Wanneer de feedback is verzonden
- Die de feedback heeft verzonden
- De feedback-ID
- Als het verzenden van de feedback is geslaagd of niet
   - Bericht-ID 53900 voor een succes volle verzen ding.
   - Bericht-ID 53901 voor een mislukte verzen ding.

Status berichten weer geven van status bericht query's van **bewakings**  >  **systeem status**  >  **Status Message Queries**. Begin met de query **alle status berichten** en selecteer uw tijds bestek. Wanneer de berichten worden geladen, klikt u op de knop **berichten filteren** en filtert u op bericht-id 53900 of 53901.

Status berichten worden niet gemaakt als u [feedback verzendt die u hebt opgeslagen om deze later te](find-help.md#BKMK_NoInternet)verzenden.

[![Status bericht voor het verzenden van feedback](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### <a name="send-a-suggestion"></a>Een suggestie verzenden

Wanneer u **een suggestie verzendt**, wordt u doorgestuurd naar [UserVoice](https://configurationmanager.uservoice.com/), een website van derden, om uw idee te delen. Het Configuration Manager-product team maakt gebruik van de volgende UserVoice-status waarden:

- **Genoteerd** : we begrijpen het verzoek en het is zinvol. We hebben dit toegevoegd aan onze achterstand.
- **Gepland** : we hebben de code ring voor deze functie gestart en verwachten dat deze in de komende maanden wordt weer gegeven in een Technical Preview-build.
- **Gestart** : de functie is nu beschikbaar in een Tech Preview. Bekijk dit en geef ons feedback. Laat het ons weten als de functie op het juiste spoor is of niet. Plaats extra feedback in het gedeelte met opmerkingen van de oorspronkelijke aanvraag zodat anderen deze kunnen zien en opmerkingen over. We lezen die en gebruiken de feedback om te proberen de functie te verbeteren.
- **Voltooid** : de eerste versie van de functie bevindt zich in een productie-build. Deze status betekent niet dat er 100% is uitgevoerd met de functie en dat deze niet meer wordt verbeterd. Maar dat betekent dat v1 van de functies zich in een productie-build bevindt, en u kunt het gebruiken voor real. Het markeren is voltooid omdat:
  - We willen u weten dat de functie gereed is voor productie.
  - We willen uw UserVoice-stemmen teruggeven zodat u ze op andere items kunt gebruiken.
  - U kunt nieuwe ontwerp wijzigings aanvragen naar deze functie verzenden om ons te helpen bij de volgende belang rijke verbetering van deze functie.

### <a name="information-sent-with-feedback"></a>Informatie verzonden met feedback

Wanneer u **een glim lach verzendt** of **een frons verzendt**, wordt de volgende informatie verzonden met de feedback:

- Buildgegevens van besturings systeem
- Configuration Manager hiërarchie-ID
- Informatie over product build
- Taal informatie
- Apparaat-id 
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SQMClient: MachineId



### <a name="send-feedback-that-you-saved-for-later-submission"></a><a name="BKMK_NoInternet"></a> Feedback verzenden die u hebt opgeslagen om deze later te verzenden

1. Klik op **Opslaan** onder aan het venster **feedback geven** . 
2. Sla het zip-bestand op. Als de lokale computer geen toegang tot internet heeft, kopieert u het bestand naar een computer die is verbonden met internet. 
3. Als dat nodig is, kopieert u de map UploadOfflineFeedback in `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`
    - Zie de CD voor meer informatie over de map cd. latest [. Meest recente map](../servers/manage/the-cd.latest-folder.md)

4. Open een opdracht prompt op een computer die is verbonden met internet. 
5. Voer de volgende opdracht uit: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - U kunt desgewenst de volgende para meters opgeven:
        -  `-t, --timeout` Time-out in seconden voor het verzenden van de gegevens. 0 is onbeperkt. De standaard waarde is 30.
        - `-s --silent`  Geen logboek registratie naar de console (kan niet combi neren met--verbose)
        - `-v, --verbose` Uitvoer uitgebreide logboek registratie naar de console (kan niet combi neren met--Silent)
        - `--help` Hiermee wordt het Help-scherm weer gegeven
    
    - Vanaf versie 1910 biedt het hulp programma UploadOfflineFeedback ondersteuning voor het gebruik van een proxy server. U kunt de volgende para meters opgeven:
        - `-x, --proxy` Hiermee geeft u een proxy server op om verbinding te maken met internet.
        - `-o, --port` Hiermee geeft u de poort op waarmee de proxy server verbinding maakt met internet.
        - `-u, --user` Hiermee geeft u de gebruikers naam op voor de proxy server om verbinding te maken met internet.
        - `-w, --password` Hiermee geeft u het wacht woord op voor de proxy server om verbinding te maken met internet. Typ een asterisk (&#42;) om een prompt voor het wacht woord te maken. Het wachtwoord wordt niet weergegeven als u deze na de wachtwoordprompt invoert. We raden u ten zeerste aan een asterisk (&#42;) te gebruiken om een prompt te maken voor het invoeren van wacht woorden, omdat tekst zonder opmaak op de opdracht regel minder veilig is.
        - `-i` Verbindings controle overs Laan: Hiermee slaat u de controle van de netwerk verbinding over, worden de feedback met de opgegeven instellingen geüpload.

## <a name="confirmation-of-console-feedback"></a><a name="bkmk_feedbackid"></a> Bevestiging van console feedback

<!--3556010-->
Vanaf versie 1902 wordt er een bevestigings bericht weer gegeven wanneer u feedback verzendt via de Configuration Manager-console of UploadOfflineFeedback.exe. Dit bericht bevat een **feedback-id**, die u aan micro soft kunt geven als tracking-ID.

- Als u de **feedback-id**wilt kopiëren, selecteert u het Kopieer pictogram naast de id of gebruikt u de sneltoets **CTRL**  +  **C** .
  - Deze ID is niet opgeslagen op uw computer. Zorg er daarom voor dat u deze kopieert voordat u het venster sluit.
- Als **u op dit bericht niet opnieuw weer geven** klikt, wordt het dialoog venster onderdrukt en wordt voor komen dat het wordt weer gegeven in de toekomst.

   ![Feedback bevestiging van de-console in Configuration Manager 1902](media/1902-feedback-id-example.png)
- De **UploadOfflineFeedback** opdracht tool schrijft de **FeedbackID** naar de console tenzij-s of--Silent wordt gebruikt.

  ![Feedback bevestiging van UploadOfflineFeedback.exe in Configuration Manager 1902](media/1902-offline-feedback-id-example.png)

##  <a name="product-feedback-for-versions-1802-and-earlier"></a><a name="BKMK_FeedbackHub"></a> Product feedback voor versie 1802 en eerder

Meld potentiële product defecten door de ingebouwde [app feedback hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) van Windows 10. Wanneer u **nieuwe feedback toevoegt**, moet u ervoor zorgen dat u de categorie **ondernemings beheer** selecteert en vervolgens een van de volgende subcategorieën kiest:
- Configuration Manager-client
- Configuration Manager-Console
- Implementatie van Configuration Manager besturings systeem
- Configuration Manager server

Ga door met de [UserVoice-pagina](https://configurationmanager.uservoice.com/) om te stemmen met nieuwe ideeën voor functies in Configuration Manager. Het Configuration Manager-product team maakt gebruik van de volgende UserVoice-status waarden:

- **Genoteerd** : we begrijpen het verzoek en het is zinvol. We hebben dit toegevoegd aan onze achterstand.
- **Gepland** : we hebben de code ring voor deze functie gestart en verwachten dat deze in de komende maanden wordt weer gegeven in een Technical Preview-build.
- **Gestart** : de functie is nu beschikbaar in een Tech Preview. Bekijk dit en geef ons feedback. Laat het ons weten als de functie op het juiste spoor is of niet. Plaats extra feedback in het gedeelte met opmerkingen van de oorspronkelijke aanvraag zodat anderen deze kunnen zien en opmerkingen over. We lezen die en gebruiken de feedback om te proberen de functie te verbeteren.
- **Voltooid** : de eerste versie van de functie bevindt zich in een productie-build. Deze status betekent niet dat er 100% is uitgevoerd met de functie en dat deze niet meer wordt verbeterd. Maar dat betekent dat v1 van de functies zich in een productie-build bevindt, en u kunt het gebruiken voor real. Het markeren is voltooid omdat:
  - We willen u weten dat de functie gereed is voor productie.
  - We willen uw UserVoice-stemmen teruggeven zodat u ze op andere items kunt gebruiken.
  - U kunt nieuwe ontwerp wijzigings aanvragen naar deze functie verzenden om ons te helpen bij de volgende belang rijke verbetering van deze functie.

##  <a name="configuration-manager-team-blog"></a><a name="BKMK_ProductGroupBlog"></a> Blog van Configuration Manager team  

De Configuration Manager Engineering en partner teams gebruiken de [Enterprise Mobility + Security Blog](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) om u te voorzien van technische informatie en ander nieuws over Configuration Manager en gerelateerde technologieën. Onze blogberichten vormen een aanvulling op de productdocumentatie en ondersteunende informatie.  


##  <a name="support-options-and-community-resources"></a><a name="BKMK_SupportOptions"></a> Ondersteunings opties en community-resources  

Via de volgende koppelingen vindt u informatie over ondersteuningsopties en bronnen van de community:  

-   [Micro soft ondersteuning](https://aka.ms/cmcbsupport)  

-   [Configuration Manager Community: Configuration Manager (Current Branch) overlevings gids](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Pagina met Configuration Manager forums](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
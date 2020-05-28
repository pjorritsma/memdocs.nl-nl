---
title: Toepassingen bewaken vanaf de console
titleSuffix: Configuration Manager
description: Bewaak de implementatie van software, inclusief updates, instellingen voor naleving en toepassingen met behulp van de werk ruimte bewaking in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 892a55ad4f3518794bef017f1d4e3a7a4de14e13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710053"
---
# <a name="monitor-applications-from-the-configuration-manager-console"></a>Toepassingen bewaken vanuit de Configuration Manager-console

*Van toepassing op: Configuration Manager (huidige vertakking)*


In Configuration Manager kunt u de implementatie van alle software bewaken, inclusief software-updates, compatibiliteits instellingen, toepassingen, taken reeksen, pakketten en Program ma's. U kunt implementaties bewaken met behulp van de werk ruimte **bewaking** in de Configuration Manager-console of door rapporten te gebruiken.  

 Toepassingen in Configuration Manager ondersteunings bewaking op basis van status, waarmee u de laatste implementatie status van een toepassing kunt bijhouden voor gebruikers en apparaten. In deze statusberichten wordt informatie over afzonderlijke apparaten weergegeven. Als een toepassing bijvoorbeeld wordt geïmplementeerd in een verzameling gebruikers, kunt u de nalevings status van de implementatie en het implementatie doel weer geven in de Configuration Manager-console.  

## <a name="learn-about-compliance-states"></a>Meer informatie over nalevings status
 De implementatiestatus van een toepassing heeft een van de volgende compatibiliteitsstatussen:  

-   **Geslaagd** – De implementatie van de toepassing is geslaagd of er is gebleken dat de toepassing al is geïnstalleerd.  

-   **Wordt uitgevoerd** – De implementatie van de toepassing wordt uitgevoerd.  

-   **Onbekend** – De status van de toepassingsimplementatie kan niet worden bepaald. Deze status is niet van toepassing op implementaties met als doel **Beschikbaar**. Deze status wordt doorgaans weergegeven wanneer er nog geen statusberichten van de client zijn ontvangen.  

-   **Niet voldaan aan vereisten** – De toepassing is niet geïmplementeerd omdat deze niet voldeed aan een afhankelijkheid of een vereisteregel, of omdat het besturingssysteem waarop het werd geïmplementeerd, niet van toepassing is.  

-   **Fout** – De toepassing kon niet worden geïmplementeerd wegens een fout.  

U kunt aanvullende informatie weer geven voor elke compatibiliteits status, inclusief subcategorieën binnen de compatibiliteits status en het aantal gebruikers en apparaten in deze categorie. Zo bevat de compatibiliteitsstatus **Fout** bijvoorbeeld de volgende subcategorieën:  

- Fout bij het evalueren van de vereisten  

- Aan inhoud gerelateerde fouten  

- Installatiefouten  

  Wanneer er meer dan één compatibiliteitsstatus van toepassing is op de implementatie van een toepassing, kunt u de geaggregeerde status zien die de laagste compatibiliteit aangeeft. Bijvoorbeeld:  

  -   Als een gebruiker zich bij twee apparaten aanmeldt en de toepassing op een apparaat is geïnstalleerd maar niet op het tweede apparaat kan worden geïnstalleerd, wordt de cumulatieve implementatie status van de toepassing voor die gebruiker weer gegeven als **fout**.  

  -   Als een toepassing wordt geïmplementeerd voor alle gebruikers die zich aanmelden bij een computer, ontvangt u meerdere implementatie resultaten voor die computer. Als een van de implementaties mislukt, wordt de geaggregeerde implementatiestatus voor de computer weergegeven als **Fout**.  

De implementatiestatus voor pakket- en programma-implementaties wordt niet geaggregeerd.  

 Gebruik deze subcategorieën om snel eventuele belangrijke problemen met een toepassingsomgeving vast te stellen. U kunt ook aanvullende informatie weergeven over de apparaten die tot een bepaalde subcategorie van een conformiteitsstatus behoren.  

 Toepassings beheer in Configuration Manager bevat een aantal ingebouwde rapporten waarmee u informatie over toepassingen en implementaties kunt bewaken. Deze rapporten hebben de rapportcategorie **Softwaredistributie - Toepassingscontrole**.  

 Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over het configureren van rapportage in Configuration Manager.  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>De status van een toepassing in de Configuration Manager-console bewaken  

1.  Kies in de Configuration Manager-console **bewakings**  >  **implementaties**.  

3.  Als u de implementatie Details voor elke compatibiliteits status en de apparaten in die status wilt bekijken, selecteert u een implementatie en kiest u vervolgens op het tabblad **Start** in de groep **implementatie** de optie **status weer geven** om het deel venster **Implementatie status** te openen. In dit deelvenster kunt u de assets met elke conformiteitsstatus weergeven. Kies een wille keurige Asset om gedetailleerdere informatie over de implementatie status voor die Asset weer te geven.  

    > [!NOTE]  
    >  Er kunnen maximaal 20.000 items worden weergegeven in het deelvenster **Implementatiestatus** . Als u meer items wilt zien, gebruikt u Configuration Manager-rapporten om de status gegevens van de toepassing weer te geven.  
    >   
    >  De status van implementatietypes wordt geaggregeerd in het deelvenster **Implementatiestatus** . Als u gedetailleerdere informatie over de implementatietypen wilt weergeven, gebruikt u het rapport **Fouten in toepassingsinfrastructuur** in de rapportcategorie **Softwaredistributie - Toepassingscontrole**.  

4.  Als u algemene status informatie over een toepassings implementatie wilt bekijken, selecteert u een implementatie en kiest u vervolgens het tabblad **samen vatting** in het venster **geselecteerde implementatie** .  

5.  Als u informatie over het implementatie type van de toepassing wilt bekijken, selecteert u een implementatie en kiest u vervolgens het tabblad **implementatie typen** in het venster **geselecteerde implementatie** .  

De informatie die wordt weer gegeven in het deel venster **Implementatie status** , nadat u de optie **status weer geven** hebt gekozen, is live gegevens uit de Configuration Manager Data Base. De gegevens die worden weer gegeven op het tabblad **samen vatting** en het tabblad **implementatie typen** , zijn samengevatte gegevens.

Als de gegevens die worden weer gegeven op het tabblad **samen vatting** en het tabblad **implementatie typen** niet overeenkomen met de gegevens die worden weer gegeven in het deel venster **Implementatie status** , kiest u **samen vatting uitvoeren** om de gegevens op deze tabbladen bij te werken. U kunt de standaardsamenvattingsinterval voor toepassingsimplementaties als volgt configureren:  

1. Klik in de Configuration Manager-console op **beheer**  >  **site configuratie**  >  **sites**.

2. Selecteer in de lijst **sites** de site waarvoor u het samenvattings interval wilt configureren en klik vervolgens op het tabblad **Start** in de groep **instellingen** op **status overzichten**.

3. Kies in het dialoog venster **status overzichten** de optie **samenvattings programma voor implementatie van toepassing**en kies vervolgens **bewerken**.  

4. Configureer in het dialoog venster **Eigenschappen van samenvattings programma voor toepassings implementatie** de vereiste samenvattings intervallen en klik vervolgens op **OK**.  

---
title: 'Configuratie-items maken voor door client beheerde Macs '
titleSuffix: Configuration Manager
description: Gebruik het configuratie-item Configuration Manager Mac OS X voor het beheren van instellingen voor Mac OS X-apparaten.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 9323fc3c1203d20c77af1f2fd27cee0a377e8d68
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240079"
---
# <a name="create-configuration-items-for-mac-os-x-devices"></a>Configuratie-items maken voor Mac OS X-apparaten
Gebruik het configuratie **-item Configuration Manager Mac OS X (aangepast)** om instellingen te beheren voor Mac OS X-apparaten die worden beheerd door de Configuration Manager-client.  
  
Het Mac OS X-besturings systeem gebruikt eigenschappen lijst bestanden (. plist) om toepassings instellingen op te slaan. Gebruik nalevingsinstellingen om instellingen in een eigenschappenlijstbestand te beoordelen en herstellen. U kunt ook Mac OS X-instellingen beheren door een shell script te schrijven dat een waarde retourneert die u voor naleving kunt evalueren en herstellen.  
  
## <a name="create-a-custom-mac-os-x-configuration-item"></a>Een aangepast Mac OS X-configuratie-item maken  
  
1. Selecteer in de Configuration Manager-console **activa en naleving**.  
  
2. Vouw in de werk ruimte **activa en naleving** de sectie **instellingen voor naleving**uit en selecteer vervolgens **configuratie-items**.  
  
3. Selecteer **configuratie-item maken**in het tabblad **Start** , in de groep **maken** .  
  
4. Geef op de pagina **Algemeen** van de wizard **configuratie-item maken** een naam en een optionele beschrijving voor het configuratie-item op.  
  
5. Selecteer onder **Geef het type configuratie-item op dat u wilt maken** de optie **Mac OS X (aangepast)**.  
  
6. Selecteer **Categorieën**als u categorieën maakt en toewijst om configuratie-items te zoeken en te filteren in de Configuration Manager-console.  
  
7. Selecteer op de pagina **Ondersteunde platforms** van de wizard de specifieke Mac OS X-versies die het configuratie-item beoordelen.  
  
8. Voeg op de pagina **instellingen** van de wizard nieuwe instellingen toe die worden beoordeeld op naleving op Mac-computers. Selecteer **Nieuw** om het dialoog venster **instelling maken** te openen.  
  
9. Geef in het dialoogvenster **Instelling maken** een unieke naam en een beschrijving voor de instelling op.  
  
10. Kies het **instellings type** dat u wilt en geef de vereiste gegevens op:  
  
    -   **Mac OS X-voorkeuren**  
  
        -   **Toepassings-id**: Geef de toepassings-id op van het eigenschappen lijst bestand van waaruit u een sleutel voor naleving wilt evalueren.  
  
             Bijvoorbeeld, als u instellingen voor de Safari-webbrowser wilt bewerken, kunt u **com.apple.Safari.plist** gebruiken.  
  
        -   **Sleutel**: Geef de naam op van de sleutel die u wilt evalueren voor naleving op Mac-computers. Gebruik de volgende syntaxis: */<woordenlijst\>/<sleutelnaam\>*.  
  
            > [!IMPORTANT]  
            >  De sleutel naam is hoofdletter gevoelig en wordt niet geëvalueerd als deze verschilt van de sleutel naam op de Mac-computer. Daarnaast kunt u de sleutel naam niet bewerken nadat u deze hebt opgegeven. Als u de sleutel naam wilt bewerken, verwijdert u de instelling en maakt u deze opnieuw.  
  
    -   **Script**  
  
        -   **Detectie script**: Selecteer **script toevoegen**en voer vervolgens een shell script in om de instellingen op de Mac-computer te beoordelen op naleving. Gebruik de **echo** opdracht in het shell script om waarden te retour neren die moeten worden Configuration Manager voor naleving. Configuration Manager gebruikt de resultaten die in **stdout** worden geretourneerd om de naleving te evalueren.  
  
            > [!IMPORTANT]  
            >  Neem de opdracht **reboot** niet op in het detectie script. Omdat het detectie script elke keer wordt uitgevoerd wanneer de client opnieuw wordt opgestart, zorgt dit ervoor dat de Mac-computer voortdurend opnieuw wordt opgestart.  
  
        -   **Herstel script (optioneel)**: Selecteer eventueel **script toevoegen**en voer vervolgens een shell script in dat wordt gebruikt voor het herstellen van niet-compatibele instellingen op Mac-client computers.  
  
            > [!IMPORTANT]  
            >  Om ervoor te zorgen dat u geen opmaak tekens introduceert die de Mac-computer niet kan interpreteren, gebruikt u kopiëren en plakken niet. In plaats daarvan typt u het script.  
  
11. Kies het **gegevens type**. Dit is de indeling waarin de voor waarde de gegevens retourneert voordat deze wordt gebruikt om de instelling te evalueren.  
  
    > [!NOTE]  
    >  Het gegevenstype **Drijvende komma** ondersteunt alleen 3 cijfers na het decimaalteken.  
    >   
    >  Configuration Manager biedt geen ondersteuning voor het gebruik van het gegevens type **Boolean** voor script instellingen voor Mac-configuratie-items. Stel in plaats daarvan het gegevens type in op **geheel getal**en zorg ervoor dat het script een geheel getal retourneert.  
  
12. Selecteer **OK** om de instelling op te slaan en het dialoog venster **instelling maken** te sluiten. Ga vervolgens door met het toevoegen van zoveel instellingen als nodig is.  
  
13. Geef op de pagina **compliantie regels** van de wizard de voor waarden op waarmee de compatibiliteit van een configuratie-item wordt gedefinieerd. Voordat een instelling kan worden beoordeeld op naleving, moet de instelling minimaal één compliantieregel hebben. Selecteer **Nieuw** om een nieuwe regel toe te voegen.  
  
14. Geef in het dialoogvenster **Regel maken** de volgende informatie op:  
  
    -   **Naam**: Voer een naam in voor de nalevings regel.  
  
    -   **Beschrijving**: Voer een beschrijving in voor de nalevings regel.  
  
    -   **Geselecteerde instelling**: Selecteer **Bladeren** om het dialoog venster **instelling selecteren** te openen. Selecteer de instelling waarvoor u een regel wilt definiëren of selecteer **nieuwe instelling**. Wanneer u klaar bent, kiest u **selecteren**.  
  
        > [!TIP]  
        >  U kunt ook **Eigenschappen** selecteren om informatie over de geselecteerde instelling weer te geven.  
  
    -   **Regel type**: Selecteer het type nalevings regel dat u wilt gebruiken:  
  
        -   **Waarde**: Maak een regel waarmee de waarde die door het configuratie-item wordt geretourneerd, wordt vergeleken met een waarde die u opgeeft.  
  
        -   **Existentieel**: Maak een regel die de instelling evalueert, afhankelijk van of deze op een apparaat bestaat.  
  
    -   Geef voor het regeltype **Waarde** de volgende informatie op:  
  
        -   **De instelling moet voldoen aan de volgende regel**: Selecteer een operator en een waarde die wordt beoordeeld op naleving van de geselecteerde instelling. U kunt de volgende operatoren gebruiken:  
  
            -   **Gelijk aan**  
  
            -   **Niet gelijk aan**  
  
            -   **Groter dan**  
  
            -   **Kleiner dan**  
  
            -   **Verdeeld**  
  
            -   **Groter dan of gelijk aan**  
  
            -   **Kleiner dan of gelijk aan**  
  
            -   **Een van**: Geef in het tekstvak één vermelding per regel op.  
  
            -   **Geen van**: Geef in het tekstvak één vermelding per regel op.  
  
        -   **Regels die niet compliant zijn herstellen, indien ondersteund**: Selecteer deze optie als u wilt dat Configuration Manager niet-compatibele regels automatisch herstelt.  
  
            > [!IMPORTANT]  
            >  U kunt niet-compatibele regels alleen herstellen als de regeloperator is ingesteld op **Is gelijk aan**.  
  
        -   **Niet-compliantie melden als dit instellings exemplaar niet wordt gevonden**: het configuratie-item rapporteert niet-naleving als deze instelling niet op de Mac-computer is gevonden.  
  
        -   **Ernst van niet-compliantie voor rapporten**: Geef de ernst op die moet worden gerapporteerd als deze compliantie regel mislukt. U kunt kiezen uit de volgende ernstniveaus:  
  
            -   **Geen**: voor computers die niet voldoen aan deze nalevings regel wordt geen fout Ernst gerapporteerd voor Configuration Manager-rapporten.  
  
            -   **Informatie**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **informatie** voor Configuration Manager-rapporten gerapporteerd.  
  
            -   **Waarschuwing**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **waarschuwing** gerapporteerd voor Configuration Manager-rapporten.  
  
            -   **Kritiek**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **kritiek** gerapporteerd voor Configuration Manager-rapporten.  
  
            -   **Kritiek met gebeurtenis**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **kritiek** gerapporteerd voor Configuration Manager-rapporten. De Mac-client computer registreert ook dit Ernst niveau.  
  
    -   Geef voor het regeltype **Existentieel** de volgende informatie op:  
  
        -   Kies een van de volgende opties:  
  
            -   **De instelling moet bestaan op clientapparaten**  
  
            -   **De instelling mag niet bestaan op clientapparaten**  
  
        -   **Ernst van niet-compliantie voor rapporten**: Geef de ernst op die moet worden gerapporteerd als deze compliantie regel mislukt. U kunt kiezen uit de volgende ernstniveaus:  
  
            -   **Geen**: voor computers die niet voldoen aan deze nalevings regel wordt geen fout Ernst gerapporteerd voor Configuration Manager-rapporten.  
  
            -   **Informatie**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **informatie** voor Configuration Manager-rapporten gerapporteerd.  
  
            -   **Waarschuwing**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **waarschuwing** gerapporteerd voor Configuration Manager-rapporten.  
  
            -   **Kritiek**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **kritiek** gerapporteerd voor Configuration Manager-rapporten.  
  
            -   **Kritiek met gebeurtenis**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **kritiek** gerapporteerd voor Configuration Manager-rapporten. De Mac-client computer registreert ook dit Ernst niveau.  
  
        > [!NOTE]  
        >  De weer gegeven opties kunnen variëren, afhankelijk van het instellings type waarvoor u een regel configureert.  
  
15. Selecteer **OK** om het dialoog venster **regel maken** te sluiten.  
  
16. Bevestig de instellingen voor het nieuwe configuratie-item op de pagina **samen vatting** . Daarna voltooit u de wizard.  
  
Zie het nieuwe configuratie-item in het knoop punt **configuratie-items** van de werk ruimte **activa en naleving** .  
  
Als u dit configuratie-item nu wilt toevoegen aan een configuratie basislijn, raadpleegt u [configuratie basislijnen maken](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="next-steps"></a>Volgende stappen

 [Configuratie-items voor apparaten die worden beheerd met de Configuration Manager-client](../../compliance/deploy-use/create-configuration-items.md)

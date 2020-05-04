---
title: Algemene beheer taken voor naleving
titleSuffix: Configuration Manager
description: Meer informatie over het Configuration Manager van de instellingen voor naleving door enkele algemene scenario's te door lopen.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1ccb0f0a042a0dd82817e030f96bbbc729e752f0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712174"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>Algemene taken voor het beheren van de naleving op apparaten met de Configuration Manager-client

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u een inleiding op het gebruik van Configuration Manager instellingen voor naleving door een aantal veelvoorkomende scenario's die u kunt door lopen.  

 Als u al bekend bent met de instellingen voor naleving, vindt u gedetailleerde informatie over alle functies die u gebruikt in [configuratie-items voor apparaten die worden beheerd met de Configuration Manager-client](../../compliance/deploy-use/create-configuration-items.md).  

 Voordat u begint, leest u aan de [slag met nalevings instellingen](../../compliance/get-started/get-started-with-compliance-settings.md) voor een aantal basis beginselen van nalevings instellingen. [Plan de instellingen voor naleving en configureer](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) deze voor informatie over de benodigde vereisten.  

## <a name="general-information-for-each-scenario"></a>Algemene informatie voor elk scenario  
 In elk scenario maakt u een configuratie-item waarmee een specifieke taak wordt uitgevoerd. Ga als volgt te werk om de wizard Configuratie-item maken te openen en aan de slag te gaan:  

1.  Selecteer in de Configuration Manager-console **assets en** > **Compliance Settings** > **configuratie-items**voor nalevings instellingen voor naleving.  

1.  Selecteer **configuratie-item maken**in het tabblad **Start** , in de groep **maken** .  

1.  Geef op de pagina **Algemeen** van de wizard Configuratie-item maken in de volgende scherm afbeelding een naam en beschrijving op voor het configuratie-item. Kies vervolgens het juiste configuratie-item type voor elk scenario in dit artikel.  

     ![Pagina Algemeen van de wizard Configuratie-item maken](../../mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Scenario: Bluetooth op Windows 10-apparaten uitschakelen

 In dit scenario heeft uw beveiligings afdeling vastgesteld dat de Bluetooth-functionaliteit op apparaten kan worden gebruikt voor het verzenden van gevoelige bedrijfs informatie buiten het bedrijf. U hebt onlangs al uw computers bijgewerkt naar Windows 10. U besluit Bluetooth op deze apparaten uit te scha kelen.  

1. Selecteer op de pagina **Algemeen** van de wizard Configuratie-item maken het configuratie-item type **Windows 10** en selecteer vervolgens **volgende**.  

2. Selecteer op de pagina **Ondersteunde platforms** van de wizard alle Windows 10-platforms.  

3. Selecteer op de pagina **Apparaatinstellingen** de optie **apparaat**en selecteer vervolgens **volgende**.  

4. Selecteer op de pagina **Apparaat** de optie **Niet toegestaan** als waarde voor **Bluetooth**.  

5. Selecteer **Niet-compliante instellingen herstellen** om ervoor te zorgen dat de wijziging wordt toegepast op alle Windows 10-apparaten.  

6. Voltooi de wizard om het configuratie-item te maken.  

 U kunt nu de informatie in de [algemene taken voor het maken en implementeren van configuratie basislijnen met Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) artikel gebruiken om u te helpen bij het implementeren van de configuratie die u hebt gemaakt op apparaten.  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Scenario: een onjuiste registersleutel op Windows-desktopcomputers herstellen

> [!NOTE] 
> Op Mac-computers met de Configuration Manager-client hebt u twee opties om de naleving te beoordelen:  
> - Een bestand met Mac OS X-voorkeuren (PLIST-bestand) evalueren.
> - Een aangepast script gebruiken en de geretourneerde resultaten evalueren.  
>
>Zie [configuratie-items maken voor Mac OS X-apparaten die worden beheerd met de Configuration Manager-client](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)voor meer informatie.  

 In dit scenario ontdekt u dat een belang rijke line-of-Business-app niet goed wordt uitgevoerd op bepaalde Windows 8,1-computers die u beheert. U bepaalt dat dit omdat een register sleutel met de naam **HKEY_LOCAL_MACHINE \Software\woodgrove\lob App\Configuration\Configuration1** op sommige computers op een waarde van **0** is ingesteld. De line-of-Business-app kan alleen worden uitgevoerd als deze waarde is ingesteld op **1**.  

 In deze procedure maakt u een configuratie-item dat controleert op en automatisch eventuele onjuiste register sleutel waarden die worden gevonden worden hersteld.  

1. Selecteer op de pagina **Algemeen** van de wizard Configuratie-item maken het configuratie-item type **Windows-Desk tops en-servers (aangepast)** en selecteer vervolgens **volgende**.  

2. Selecteer op de pagina **ondersteunde platforms** van de wizard de optie **Windows 8,1** (om ervoor te zorgen dat het configuratie-item alleen van toepassing is op de betreffende computers).  

3. Selecteer op de pagina **instellingen** de optie **Nieuw** om een nieuwe instelling te maken.  

4. Configureer de volgende instellingen op het tabblad **Algemeen** van het dialoog venster **instelling maken** :  

   -   **Name** > **Instelling voor beeld** van naam  

   -   **Instelling type** > **register waarde**  

   -   **Data type** > **Geheel getal** gegevens type (omdat de waarde alleen een getal bevat)  

   -   **Hive** > **HKEY_LOCAL_MACHINE**  

   -   **Key** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Waarde** > **1** (de vereiste waarde)  

5. Selecteer op het tabblad **compliantie regels** van het dialoog venster **instelling maken** de optie **Nieuw**. Configureer in het dialoog venster **regel maken** de volgende instellingen:  

   -   **Naam** > **voorbeeld regel**  

   -   De **geselecteerde instelling** > Controleer of de instelling **voor beeld**is geselecteerd.

   -   **Rule type** > **Waarde** van regel type  

   -   **De instelling moet voldoen aan de volgende regel** > Controleer of de naam van de instelling juist is en configureer de optie om op te geven dat de waarde van de instelling gelijk moet zijn aan **1**.  

   -   **Regels die niet compliant zijn herstellen, wanneer ondersteund** > Schakel dit selectie vakje in om ervoor te zorgen dat Configuration Manager de waarde van de register sleutel opnieuw instelt op de juiste waarde als deze onjuist is.  

6. Voltooi de wizard om het configuratie-item te maken.  

 U kunt nu de informatie in het artikel [algemene taken voor het maken en implementeren van configuratie basislijnen](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) gebruiken om u te helpen bij het implementeren van de configuratie die u hebt gemaakt op apparaten.  

## <a name="next-steps"></a>Volgende stappen

[Configuratiebasislijnen maken en implementeren](common-tasks-for-creating-and-deploying-configuration-baselines.md)

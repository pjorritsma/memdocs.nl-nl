---
title: Het app-gebruik controleren met softwaremeter
titleSuffix: Configuration Manager
description: Meer informatie over bewerkingen die beschikbaar zijn in Configuration Manager software meter.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13d8cce1811c4a27f6a3e7485eea4d65132c2888
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710081"
---
# <a name="software-metering-in-configuration-manager"></a>Software licentie controle in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit onderwerp bevat een verwijzing voor alle bewerkingen die u kunt uitvoeren wanneer u Configuration Manager software licentie controle gebruikt.

> [!IMPORTANT]
>  Softwarelicentiecontrole wordt gebruikt om bureaublad-apps voor Windows-computers te bewaken die een bestandsnaam hebben die eindigt op **.exe**. Softwarelicentiecontrole controleert geen moderne Windows-apps (zoals die worden gebruikt door Windows 8).

##  <a name="prerequisites-for-software-metering"></a>Vereisten voor softwarelicentiecontrole
Softwarelicentiecontrole heeft geen externe afhankelijkheden, alleen afhankelijkheden binnen het product.

|Afhankelijkheid|Meer informatie|
|----------------|----------------------|
|Clientinstellingen voor softwarelicentiecontrole|Om softwarelicentiecontrole te gebruiken moet de clientinstelling **Softwaremeter op clients inschakelen** zijn ingeschakeld en geïmplementeerd op computers. U kunt instellingen voor softwarelicentiecontrole implementeren op alle computers in de hiërarchie of aangepaste instellingen implementeren op computergroepen. Zie **Software meters configureren** in dit onderwerp.|
|Het reporting services-punt.|U moet een reporting services-punt configureren voordat u softwarelicentiecontrolerapporten kunt weergeven. Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.|

##  <a name="configure-software-metering"></a>Configure software metering
 Met deze procedure configureert u de standaardclientinstellingen voor softwarelicentiecontrole en past u deze toe op alle computers in uw hiërarchie. Als u dat deze instellingen alleen op enkele computers wilt implementeren, maakt u een aangepaste apparaatclientinstelling en implementeert u deze in een verzameling waartoe de computers behoren die u voor softwarelicentiecontrole wilt gebruiken. Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor meer informatie over het maken van aangepaste apparaatinstellingen.

1. Klik in de Configuration Manager-console op**client** > instellingen voor **beheerders** > **standaard client instellingen**.

2. Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.

3. In het dialoogvenster **Standaardinstellingen** klikt u op **Softwarelicentiecontrole**.

4. In de lijst **Apparaatinstellingen** configureert u dan het volgende:

   -   **Softwaremeter op clients inschakelen**: selecteer **Waar** om softwarelicentiecontrole in te schakelen.

   -   **Planning gegevensverzameling**: configureer hoe vaak gegevens van softwarelicentiecontrole bij clientcomputers worden verzameld. Gebruik de standaardwaarde van elke **7 dagen** of klik op **Planning** om een aangepaste planning op te geven.

5. Klik op **OK** om het dialoogvenster **Standaardinstellingen** te sluiten.

   De volgende keer dat clientcomputers clientbeleid downloaden, worden deze geconfigureerd met deze instellingen. Zie [clients beheren](../../core/clients/manage/manage-clients.md)om het ophalen van het beleid voor één client te starten.

##  <a name="create-software-metering-rules"></a> Softwaremeterregels maken
 Gebruik de wizard software meter regel maken om een nieuwe software meter regel te maken voor uw Configuration Manager-site.

1.  Klik in de Configuration Manager-console op **activa en naleving** > **Software meter**.

3.  Op het tabblad **Start** in de groep **Maken** klikt u op **Softwaremeterregel maken**.

4.  Geef op de pagina **Algemeen** van de wizard software meter regel maken de volgende informatie op:

    -   **Naam** : de naam van de softwaremeterregel. Deze moet uniek zijn en beschrijvend.

        > [!NOTE]
        >  Softwaremeterregels kunnen dezelfde naam hebben als de bestandsnaam in de regels anders is.

    -   **Bestandsnaam** : de naam van het programmabestand dat u wilt meten. U kunt klikken op **Bladeren** om het dialoogvenster **Openen** weer te geven, waarin u het te gebruiken programmabestand kunt selecteren.

        > [!NOTE]
        >  Als u de naam van het uitvoerbare bestand in het vak **Bestandsnaam** typt, worden er geen controles uitgevoerd om te bepalen of dit bestand bestaat, en of dit de benodigde berichtkopinformatie bevat. Klik indien mogelijk op **Bladeren** en selecteer het uitvoerbare bestand dat moet worden gemeten.
        >
        >  Jokertekens zijn niet toegestaan in de bestandsnaam.
        >
        >  Dit vak is optioneel als er een waarde voor **Originele bestandsnaam** is opgegeven.

    -   **Originele bestandsnaam** : de naam van het uitvoerbare bestand dat u wilt meten. Deze naam komt overeen met de informatie in de koptekst van het bestand, niet de bestandsnaam zelf, zodat dit nuttig kan zijn in gevallen waarin de naam van het uitvoerbare bestand is gewijzigd maar u het met zijn oorspronkelijke naam wilt meten.

        > [!NOTE]
        >  Jokertekens zijn niet toegestaan in de oorspronkelijke bestandsnaam.
        >
        >  Dit vak is optioneel als er een waarde voor **Bestandsnaam** is opgegeven.

    -   **Versie** : de versie van het uitvoerbare bestand dat u deze wilt meten. U kunt het Joker teken (&#42;) gebruiken om een wille keurige teken reeks of het Joker teken (?) weer te geven. ) om één wille keurig teken aan te duiden. Als u een meting wilt voor alle versies van een uitvoerbaar bestand, gebruikt u de standaard waarde (&#42;).

    -   **Taal** : de taal van het uitvoerbare bestand dat u wilt meten. De standaardwaarde is de huidige landinstelling van het besturingssysteem dat u gebruikt. Als u een uitvoerbaar bestand selecteert om te meten door te klikken op de knop **Bladeren** , wordt dit vak automatisch ingevuld als er taalinformatie in de koptekst van het bestand aanwezig is. Als u alle taalversies van een bestand wilt meten, selecteert u **Elke** in de vervolgkeuzelijst.

    -   **Beschrijving** : een optionele beschrijving voor de softwaremeterregel.

    -   **Deze softwaremeterregel toepassen op de volgende clients** : selecteer of u de softwaremeterregel wilt toepassen op alle clients in de hiërarchie of aan de clients die zijn toegewezen aan de site die is opgegeven in de lijst **Site** .

5.  Als u wilt doorgaan, klikt u op **Volgende**.

6.  Controleer en bevestig de instellingen en voltooi de wizard om de softwaremeterregel te maken. De nieuwe softwaremeterregel wordt weergegeven in het knooppunt **Softwarelicentiecontrole** in de werkruimte **Activa en naleving** .

##  <a name="configure-automatic-software-metering-rules"></a> Automatische softwaremeterregels configureren
 U kunt software meter in Configuration Manager configureren om automatisch uitgeschakelde software meter regels te genereren van recente inventaris gegevens over gebruik in de site database. U kunt deze inventarisgegevens zodanig configureren dat er alleen softwaremeterregels worden gemaakt voor toepassingen die worden gebruikt met een opgegeven percentage computers. Ook kunt u het maximum aantal automatisch gegenereerde softwaremeterregels opgeven dat op de site is toegestaan.

> [!NOTE]
>  Softwaremeterregels die automatisch worden gemaakt, worden standaard uitgeschakeld. Voordat u kunt beginnen met het verzamelen van gegevens met deze regels, moet u deze inschakelen.

1.  Klik in de Configuration Manager-console op **assets en naleving** > **software licentie controle**en klik vervolgens op het tabblad **Start** in de groep **instellingen** op Eigenschappen van **Software meter**.

3.  In het dialoogvenster **Eigenschappen van softwaremeter** configureert u het volgende:

    -   **Bewaren van gegevens (in dagen)** : geeft de tijd aan dat gegevens behouden blijven die door softwaremeterregels in de sitedatabase worden gegenereerd. De standaardwaarde is **90** dagen.

    -   Schakel de optie **Automatisch uitgeschakelde meterregels maken van inventarisgegevens over recent gebruik**in.

    -   **Geef op welk percentage van computers in de hiërarchie een programma moet gebruiken voordat automatisch een softwaremeterregel wordt gemaakt** : de standaardwaarde is **10** procent.

    -   **Geef het aantal softwaremeterregels op dat moet worden overschreden in de hiërarchie voordat het automatisch maken regels wordt uitgeschakeld** : de standaardwaarde is **100** regels.

4.  Klik op **OK** om het dialoogvenster **Eigenschappen van softwaremeter** te sluiten.

##  <a name="manage-software-metering-rules"></a> Softwaremeterregels beheren
 In de werkruimte **Activa en naleving** selecteert u **Softwarelicentiecontrole**, selecteert u de te beheren softwaremeterregel en selecteert u vervolgens een beheertaak.

 Gebruik de volgende tabel voor meer informatie over de beheertaken waarvoor u mogelijk meer uitleg nodigt hebt voordat u ze selecteert.

|Beheertaak|Details|
|---------------------|-------------|
|**Inschakelen**<br /><br /> **Uitschakelen**|Hiermee schakelt u een softwaremeterregel in of uit. Deze instelling wordt gedownload naar clientcomputers volgens de **Pollinginterval voor clientbeleid** in de sectie **Clientbeleid** van de clientinstellingen (standaard elke 60 minuten).<br /><br /> Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md) .|

##  <a name="monitor-software-metering"></a>Software licentie controle bewaken
 Software licentie controle in Configuration Manager bevat een aantal ingebouwde rapporten waarmee u informatie over software meter bewerkingen kunt bewaken. Deze rapporten hebben de rapportcategorie **Softwaremeter**.

 Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over het configureren van rapportage in Configuration Manager.

 Daarnaast kunt u query's en verzamelingen maken op basis van de gegevens die zijn opgeslagen in de Configuration Manager-Data Base door software meter.

 Zie [Inleiding tot verzamelingen](../../core/clients/manage/collections/introduction-to-collections.md)voor meer informatie over verzamelingen in Configuration Manager.

 Zie [Inleiding tot query's](../../core/servers/manage/introduction-to-queries.md)voor meer informatie over query's in Configuration Manager.

##  <a name="security-and-privacy-for-software-metering"></a>Beveiliging en privacy voor softwarelicentiecontrole

### <a name="security-issues-for-software-metering"></a>Beveiligingsproblemen voor softwarelicentiecontrole
 Een aanvaller kan ongeldige software licentie controle gegevens naar Configuration Manager verzenden, die door het beheer punt worden geaccepteerd, zelfs wanneer de client instelling voor software licentie controle is uitgeschakeld. Dit kan leiden tot een groot aantal meet regels die in de gehele hiërarchie worden gerepliceerd, waardoor er een DOS-aanval (Denial of service) wordt veroorzaakt op het netwerk en Configuration Manager site servers.

 Omdat een aanvaller ongeldige softwaremetergegevens kan maken, dient u softwaremetergegevens niet als gezaghebbend te beschouwen.

 Softwaremeter is standaard ingeschakeld als een clientinstelling.

###  <a name="privacy-information-for-software-metering"></a> Privacyinformatie voor softwaremeter
 Softwaremeter bewaakt het gebruik van toepassingen op clientcomputers. Softwaremeter is standaard ingeschakeld. U moet configureren welke toepassingen moeten worden gemeten. Meet gegevens worden opgeslagen in de Configuration Manager-Data Base. De gegevens worden versleuteld tijdens de overdracht naar een beheer punt, maar worden niet in versleutelde vorm opgeslagen in de Configuration Manager-Data Base.

 Deze gegevens blijven in de database bewaard tot deze worden verwijderd door de siteonderhoudstaak **Verouderde gegevens van softwaremeter verwijderen** (elke vijf dagen) en **Verouderde samenvattingsgegevens van softwaremeter verwijderen** (elke 270 dagen). U kunt het verwijderingsinterval configureren. Er worden geen metergegevens naar Microsoft verzonden.

 Voordat u softwaremeter configureert, moet u nadenken over uw privacyvereisten.

## <a name="example-scenario-for-using-software-metering"></a>Voorbeeldscenario voor het gebruik van softwaremeter
 In deze sectie maakt u een voorbeeld van een softwaremeterregel waarmee u de volgende bedrijfsvereisten kunt oplossen:

- Bepalen hoeveel exemplaren van een bepaalde app uw bedrijf heeft

- Alle ongebruikte exemplaren van een app detecteren

- Bepalen welke gebruikers een bepaalde app regelmatig gebruiken

  Woodgrove Bank heeft Microsoft Office 2010 geïmplementeerd als standaard Office-productiviteitssuite. Ter ondersteuning van een oudere toepassing, moet Microsoft Office Word 2003 op bepaalde computer worden uitgevoerd. De IT-afdeling wil ondersteuning en licentiekosten reduceren door deze exemplaren van Word 2003 te verwijderen als de oude toepassing niet meer wordt gebruikt. De helpdesk wil ook bepalen welke gebruikers de oude toepassing gebruiken.

  De IT-beheerder van Woodgrove Bank gebruikt software meter in Configuration Manager om deze zakelijke doel stellingen te bereiken. De beheerder voert de volgende acties uit:

- Controleert de vereisten voor software licentie controle en bevestigt dat het Reporting Services-punt geïnstalleerd en operationeel is.
- Hiermee configureert u de standaard client instellingen voor software licentie controle:<br>De beheerder schakelt software meter in en gebruikt het standaard schema voor gegevens verzameling van elke zeven dagen.<br>De beheerder configureert software-inventarisatie bestanden met de extensie. exe door de client instelling voor software-inventaris **Deze bestands typen**te configureren.<br>De beheerder voegt een nieuwe software meter regel, met de naam **Woodgrove. exe**, om de oudere toepassing te bewaken.
- Wacht zeven dagen, waarna de client computers gebruiks gegevens gaan rapporteren voor het uitvoer bare bestand **Woodgrove. exe** .
- De beheerder gebruikt de Configuration Manager rapport **installatie basis voor alle Program ma's met gecontroleerde licenties** om te zien welke computers de toepassing **Woodgrove. exe** hebben geladen.
- Na zes maanden voert de beheerder het rapport **computers uit waarop een programma met gecontroleerde licentie is geïnstalleerd, maar het programma sinds een opgegeven datum is niet uitgevoerd**, waarbij de software meter regel en een datum zes maanden in het verleden zijn ingesteld. Dit rapport identificeert 120 computers waarop het programma de afgelopen zes maanden niet is uitgevoerd.
- De beheerder voert een aantal verdere controles uit om te bevestigen dat de verouderde toepassing niet is vereist op de geïdentificeerde computers. De beheerder verwijdert de oudere toepassing en het exemplaar van Word 2003 van deze computers.<br>De beheerder voert het rapport **gebruikers die een specifiek programma met gecontroleerde licenties hebben uitgevoerd uit** om de Help Desk te voorzien van een lijst met gebruikers die de oudere toepassing blijven gebruiken.
- De beheerder blijft de software licentie controle rapporten wekelijks controleren en neemt indien nodig de herstel actie.

  Als gevolg van deze maatregel worden de toepassingen die niet meer nodig zijn, verwijderd en worden de IT-ondersteuning en licentiekosten gereduceerd. Daarnaast beschikt de helpdesk nu over de gewenste lijst met gebruikers die de oudere toepassing uitvoeren.

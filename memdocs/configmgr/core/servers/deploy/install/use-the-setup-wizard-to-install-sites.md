---
title: Wizard Setup
titleSuffix: Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
description: Gebruik de installatie wizard van Configuration Manager om een nieuwe site te installeren.
ms.openlocfilehash: a0956e53af0d8ca4dd182dd3c2be944d3a0a703d
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606179"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>De installatie wizard gebruiken om Configuration Manager-sites te installeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u een nieuwe Configuration Manager-site wilt installeren met behulp van een begeleide gebruikers interface, gebruikt u de wizard Configuration Manager Setup (setup.exe). De wizard ondersteunt het installeren van een primaire site of een centrale beheer site. U kunt de wizard ook gebruiken om [een evaluatie-installatie](upgrade-an-evaluation-install-to-a-full-install.md) van Configuration Manager naar een volledig gelicentieerde installatie bij te werken. Wanneer u de wizard niet wilt gebruiken, kunt u in plaats daarvan een [installatie script](use-a-command-line-to-install-sites.md) gebruiken en een installatie zonder toezicht uitvoeren vanaf de opdracht regel.

Installeer een secundaire site vanuit de Configuration Manager-console. Secundaire sites bieden geen ondersteuning voor een script opdracht regel installatie.

> [!Note]  
> Vanaf versie 1906 komt het bestand met de **welkomst. HTA** niet meer voor in de hoofdmap van het installatie medium. Het heeft koppelingen naar de volgende informatie verstrekt:<!--SCCMDocs-pr#3545-->
>
> - **Installatie site**: `smssetup\bin\x64\setup.exe` . Zie [install a Central Administration of Primary Site](#bkmk_primary)(Engelstalig) voor meer informatie.
> - **Voordat u begint**: [een hiërarchie van sites ontwerpen](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626543 -->
> - **Gereedheid van de server evalueren**: [prerequisite Checker](prerequisite-checker.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626546 -->
> - **Vereiste bestanden downloaden**: `smssetup\bin\x64\setupdl.exe` . Zie het [Download programma](setup-downloader.md)voor meer informatie.
> - **Configuration Manager-console installeren**: `smssetup\bin\i386\consolesetup.exe` . Zie [consoles installeren](install-consoles.md)voor meer informatie.
> - [**System Center Updates Publisher downloaden**](../../../../sum/tools/updates-publisher.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626548 -->
> - **Clients downloaden voor extra besturings systemen**: <!-- https://go.microsoft.com/fwlink/p/?LinkId=626550 -->
>   - [Micro soft endpoint Configuration Manager-macOS-client (64-bits)](https://www.microsoft.com/download/details.aspx?id=100850)
>   - [Clients voor UNIX en Linux](https://www.microsoft.com/download/details.aspx?id=47719)
> - [**Releaseopmerkingen**](release-notes.md) <!-- https://go.microsoft.com/fwlink/?LinkID=626571 -->
> - [**Documentatie lezen**](/sccm)<!-- https://go.microsoft.com/fwlink/p/?LinkId=626547 -->
> - **Ondersteuning bij de installatie verkrijgen**: [TechNet forums: Configuration Manager (current branch) – site-en client implementatie](https://social.technet.microsoft.com/Forums/en-us/home?forum=ConfigMgrDeployment) <!--NOTE: this link requires en-us locale to work-->   <!-- https://go.microsoft.com/fwlink/p/?LinkId=626549 -->
> - **Configuration Manager Community**: [System Center Community: deel nemen aan](https://social.technet.microsoft.com/wiki/contents/articles/11504.system-center-community-how-to-participate.aspx) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626544 -->
> - [**Start pagina Configuration Manager**](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626545 -->


## <a name="install-a-central-administration-or-primary-site"></a><a name="bkmk_primary"></a> Een centrale beheer-of primaire site installeren

Gebruik de volgende procedure om een centrale beheer site of een primaire site te installeren. U kunt dit ook gebruiken om een evaluatie site bij te werken naar een volledig gelicentieerde Configuration Manager-site.

Voordat u met de installatie van de site begint, moet u bekend zijn met de informatie in de volgende artikelen:

- [De installatie van sites voorbereiden](prepare-to-install-sites.md)
- [Vereisten voor het installeren van sites](prerequisites-for-installing-sites.md)

Als u een centrale beheer site installeert als onderdeel van een scenario voor site-uitbrei ding, raadpleegt u [een zelfstandige primaire site uitbreiden](use-the-setup-wizard-to-install-sites.md#bkmk_expand) voordat u de volgende procedure uitvoert.

### <a name="process-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a> Proces voor het installeren van een primaire of centrale beheer site

1. Op de computer waarop u de site wilt installeren, voert `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` u uit om de **wizard Configuration Manager Setup**te starten.  

    > [!NOTE]  
    > Wanneer u een centrale beheer site installeert om uit te breiden op een zelfstandige primaire site of een nieuwe onderliggende primaire site in een bestaande hiërarchie installeert, gebruikt u installatie media (bron bestanden) die overeenkomen met de versie van de bestaande site of sites. Als u in-console-updates hebt geïnstalleerd die de versie van eerder geïnstalleerde sites hebben gewijzigd, gebruikt u de oorspronkelijke installatie media niet. Gebruik in plaats daarvan bron bestanden van de [cd. Meest recente map](../../manage/the-cd.latest-folder.md) van een bijgewerkte site. Configuration Manager moet u bron bestanden gebruiken die overeenkomen met de versie van de bestaande site waarmee de nieuwe site verbinding maakt.  

2. Klik op de pagina **voordat u begint** op **volgende**.  

3. Selecteer op de pagina **aan** de slag het type site dat u wilt installeren:  

    - **Centrale beheer site**, als de eerste site van een nieuwe hiërarchie, of bij het uitbreiden van een zelfstandige primaire site:  

        Selecteer **een Configuration Manager centrale beheer site installeren**.  

        Tijdens een latere stap van deze procedure krijgt u de keuze om een centrale beheer site te installeren als de eerste site van een nieuwe hiërarchie, of om een centrale beheer site te installeren om uit te breiden op een zelfstandige primaire site.  

    - **Primaire site**, als een zelfstandige primaire site die de eerste site van een nieuwe hiërarchie is, of als een onderliggende primair:  

        Selecteer **een Configuration Manager primaire site installeren**.  

        > [!TIP]  
        > Normaal gesp roken selecteert u alleen de optie **standaard installatie opties gebruiken voor een zelfstandige primaire site** wanneer u een zelfstandige primaire site wilt installeren in een test omgeving. Wanneer u deze optie selecteert, voert Setup de volgende acties uit:  
        >
        > - Hiermee wordt de site automatisch geconfigureerd als een zelfstandige primaire site.  
        > - Maakt gebruik van een standaard installatiepad.  
        > - Maakt gebruik van een lokale installatie van het standaard exemplaar van SQL Server voor de site database.  
        > - Hiermee installeert u een beheer punt en een distributie punt op de site Server computer.  
        > - Hiermee configureert u de site met het Engels en de weergave taal van het besturings systeem op de primaire site server als deze overeenkomt met een van de talen die Configuration Manager ondersteunt.  

4. Op de pagina **product code** :  

    - Kies of u Configuration Manager wilt installeren als een evaluatie-editie of een gelicentieerde versie.  

        - Als u een gelicentieerde editie selecteert, voert u uw product code in en kiest u **volgende**.  

        - Als u een evaluatie-editie selecteert, kiest u **volgende**. (U kunt later een evaluatie-installatie bijwerken naar een volledige installatie.)  

    - U kunt ook de **verval datum van de Software Assurance** van uw licentie overeenkomst opgeven. Het is een handige herinnering voor die datum. Als u deze datum niet opgeeft tijdens de installatie, kunt u deze later opgeven in de Configuration Manager-console.  

        > [!NOTE]  
        > Micro soft valideert niet de verval datum die u hebt ingevoerd en gebruikt deze datum niet voor validatie van licenties. U kunt deze gebruiken als herinnering voor uw verval datum. Deze datum is handig omdat Configuration Manager regel matig controleert of nieuwe software-updates online worden aangeboden. De licentie status van uw Software Assurance moet actueel zijn, zodat u in aanmerking komt voor het gebruik van deze aanvullende updates.  

    Zie [Licentiëring en vertakkingen](../../../understand/learn-more-editions.md)voor meer informatie.  

5. Lees en accepteer de licentie voorwaarden op de pagina **licentie voorwaarden voor micro soft-software** .  

6. Lees en accepteer de licentie voorwaarden voor de vereiste software op de pagina **vereiste licenties** . Setup downloadt en installeert de software automatisch op site systemen of clients wanneer deze vereist is. Accepteer alle voor waarden voordat u doorgaat naar de volgende pagina.  

7. Geef op de pagina **vereiste down loads** op of het installatie programma de meest recente vereiste herdistribueerbare bestanden moet downloaden van het internet of dat eerder gedownloade bestanden moeten worden gebruikt:  

    - Als u wilt dat Setup de bestanden op dit moment downloadt, selecteert u **vereiste bestanden downloaden**. Geef vervolgens een locatie op voor het opslaan van de bestanden.  

    - Als u de bestanden eerder hebt gedownload met behulp van het [Download programma](setup-downloader.md)voor de installatie, selecteert u **eerder gedownloade bestanden gebruiken**. Geef vervolgens de downloadmap op.  

        > [!TIP]  
        > Als u eerder gedownloade bestanden gebruikt, controleert u of het pad naar de downloadmap de meest recente versie van de bestanden bevat.  

8. Selecteer op de pagina **selectie van server taal** de talen die beschikbaar zijn voor de Configuration Manager-console en voor rapporten. (Engels is standaard geselecteerd en kan niet worden verwijderd.) Zie [taal pakketten](language-packs.md)voor meer informatie.  

9. Selecteer op de pagina **selectie van client taal** de talen die beschikbaar zijn voor client computers. Geef ook op of alle client talen moeten worden ingeschakeld voor clients van mobiele apparaten. (Engels is standaard geselecteerd en kan niet worden verwijderd.)  

    > [!IMPORTANT]  
    > Wanneer u een centrale beheer site gebruikt, moet u ervoor zorgen dat de client talen die u configureert op de centrale beheer site, alle client talen bevatten die u op elke onderliggende primaire site configureert. Clients die vanaf een distributie punt installeren, hebben toegang tot de client talen vanaf de site op het hoogste niveau, terwijl clients die vanaf een beheer punt installeren, toegang hebben tot de client talen vanuit hun toegewezen primaire site.  

10. Geef op de pagina **site-en installatie-instellingen** de volgende instellingen op voor de nieuwe site die u installeert:  

    - **Site code**: [elke site code in een hiërarchie moet uniek zijn](prepare-to-install-sites.md#bkmk_sitecodes). Gebruik drie alfanumerieke cijfers: A t/m Z en 0 t/m 9. Omdat de site code in mapnamen wordt gebruikt, gebruikt u geen door Windows gereserveerde namen, waaronder:  
        - AUX  
        - CON  
        - NUL  
        - PRN  
        - Sms  

        > [!NOTE]  
        > Het installatie programma controleert niet of de door u opgegeven site code al wordt gebruikt, of dat het een gereserveerde naam is.  

    - **Site naam**: voor elke site is deze beschrijvende naam vereist, die u kan helpen bij het identificeren van de site.  

    - **Installatiemap**: deze map is het pad naar de Configuration Manager-installatie. U kunt de locatie niet wijzigen nadat de site is geïnstalleerd. Het pad mag geen Unicode-tekens of afsluitende spaties bevatten.  

        > [!NOTE]  
        > Overweeg of u de standaardinstallatiemap wilt gebruiken. Als u de standaard besturingssysteem partitie in een productie omgeving gebruikt, kunnen de volgende problemen in de toekomst optreden:  
        >
        > - Als Configuration Manager de extra vrije schijf ruimte op de partitie van het besturings systeem gebruikt, werken Windows of Configuration Manager niet goed. Als u Configuration Manager op een afzonderlijke partitie installeert, heeft dit geen invloed op het schijf gebruik van het besturings systeem.
        > - Configuration Manager prestaties zijn beter met een snelle schijf. Bij sommige server ontwerpen wordt de besturingssysteem schijf niet geoptimaliseerd voor snelheid.
        > - U kunt het besturings systeem onderhouden, herstellen of opnieuw installeren zonder dat dit van invloed is op uw Configuration Manager-installatie.  

11. Gebruik op de pagina **site-installatie** de volgende optie die overeenkomt met uw scenario:  

    - **Ik installeer een centrale beheer site:**  

        Selecteer op de pagina **installatie van centrale beheer site** de optie **installeren als de eerste site in een nieuwe hiërarchie**en klik vervolgens op **volgende** om door te gaan.  

    - **Ik Breid een zelfstandige primaire toepassing uit in een hiërarchie met een centrale beheer site:**  

        Selecteer op de pagina **installatie van centrale beheer site** de optie **een bestaande zelfstandige primaire toepassing uitbreiden naar een hiërarchie**. Geef vervolgens de FQDN van de zelfstandige primaire site server op en kies **volgende** om door te gaan.  

        De media die u gebruikt voor het installeren van de nieuwe centrale beheer site moeten overeenkomen met de versie van de primaire site.  

    - **Ik installeer een zelfstandige primaire site:**  

        Selecteer op de pagina **primaire site** -installatie **de optie de primaire site installeren als een zelfstandige site**en klik vervolgens op **volgende**.  

    - **Ik installeer een onderliggende primaire site:**  

        Selecteer op de pagina **primaire site** -installatie **de optie de primaire site toevoegen aan een bestaande hiërarchie**. Geef vervolgens de FQDN voor de centrale beheer site op en kies **volgende**.  

12. Geef op de pagina **database gegevens** de volgende informatie op:  

    - **SQL Server naam (FQDN)**: deze waarde is standaard ingesteld op de site Server computer.  

        Als u een aangepaste poort gebruikt, voegt u die poort toe aan de FQDN van de SQL Server. Volg de FQDN-namen van de SQL Server met een komma en vervolgens het poort nummer. Gebruik bijvoorbeeld voor server *SQLServer1.fabrikam.com*het volgende om poort *1551*op te geven: `SQLServer1.fabrikam.com,1551`  

    - **Exemplaar naam**: deze waarde is standaard leeg. Het maakt gebruik van het standaard exemplaar van SQL op de site Server computer.  

    - **Database naam**: deze waarde is standaard ingesteld op `CM_<Sitecode>` . U kunt deze waarde aanpassen.  

    - **Service Broker poort**: deze waarde is standaard ingesteld op het gebruik van de standaard poort voor SQL Server service BROKER (SSB) van 4022. SQL gebruikt IT om rechtstreeks te communiceren met de site database op andere sites.  

13. Op de tweede pagina **database gegevens** kunt u aangepaste locaties opgeven voor het SQL Server gegevens bestand en het SQL Server logboek bestand voor de site database:  

    - Standaard worden de standaard bestands locaties gebruikt voor SQL Server.  

    - Wanneer u een SQL Server cluster gebruikt, is de optie voor het opgeven van aangepaste bestands locaties niet beschikbaar.  

    - De prerequisite Checker voert geen controle uit op vrije schijf ruimte voor aangepaste bestands locaties.  

14. Geef op de pagina **SMS-provider instellingen** de FQDN op voor de server waarop u de SMS-provider wilt installeren.  

    - Standaard wordt de site server opgegeven.  

    - Nadat de site is geïnstalleerd, kunt u aanvullende SMS-providers configureren. Zie [de SMS-provider plannen](../../../plan-design/hierarchy/plan-for-the-sms-provider.md)voor meer informatie.  

15. Kies op de pagina **instellingen voor client communicatie** of alle site systemen zo moeten worden geconfigureerd dat ze alleen https-communicatie van clients accepteren of dat de communicatie methode voor elke site systeemrol moet worden geconfigureerd.  

    Wanneer u **Alle site systeem rollen selecteert alleen https-communicatie van clients accepteert**, moet de client computer een geldig PKI-certificaat voor client verificatie hebben. Zie [PKI-certificaat vereisten](../../../plan-design/network/pki-certificate-requirements.md)voor meer informatie.  

    > [!NOTE]  
    > Deze stap is alleen van toepassing wanneer u een primaire site installeert. Als u een centrale beheer site installeert, kunt u deze stap overs Laan.  

16. Kies op de pagina **site systeem rollen** of u een beheer punt of distributie punt wilt installeren. Voor elke rol die u tijdens de installatie wilt laten installeren:  

    - Voer de **FQDN** in voor de server die als host moet fungeren voor de rol. Kies vervolgens de client verbindings methode die door de server wordt ondersteund: HTTP of HTTPS.  

    - Als u **Alle site systeem rollen hebt geselecteerd, accepteren alleen https-communicatie van clients** op de vorige pagina, worden de client Verbindings instellingen automatisch geconfigureerd voor HTTPS. U kunt deze instelling niet wijzigen, tenzij u teruggaat naar de vorige pagina.  

    > [!NOTE]  
    > Deze stap is alleen van toepassing wanneer u een primaire site installeert. Als u een centrale beheer site installeert, kunt u deze stap overs Laan.  

    > [!NOTE]  
    > Om site systeem rollen te installeren, wordt het **installatie account van het site systeem**gebruikt. Dit maakt standaard gebruik van het computer account van de primaire site. Dit account moet een lokale beheerder zijn op een externe computer om de site systeemrol te installeren. Als dit account niet over de vereiste machtigingen beschikt, schakelt u de site systeem rollen uit en installeert u deze later vanuit de Configuration Manager-console, nadat u extra accounts hebt geconfigureerd om te gebruiken als installatie accounts voor site systemen. Zie [accounts](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)voor meer informatie.  

17. Controleer op de pagina **gebruiks gegevens** de informatie over de gegevens die door micro soft worden verzameld en kies **volgende**. Zie [diagnostiek en gebruiks gegevens](../../../plan-design/diagnostics/diagnostics-and-usage-data.md)voor meer informatie.  

18. De pagina voor het instellen van het **service verbindings punt** is alleen beschikbaar in de volgende scenario's:  

    - Wanneer u een zelfstandige primaire site installeert.  

    - Wanneer u een centrale beheer site installeert.  

    > [!NOTE]  
    > Als u een onderliggende primaire site installeert, slaat u deze stap over.  

     Als u een centrale beheer site installeert als onderdeel van een scenario voor site-uitbrei ding en deze rol al is geïnstalleerd op de zelfstandige primaire site, verwijdert u eerst deze rol van de zelfstandige primaire site. Er is slechts één exemplaar van deze rol toegestaan in een hiërarchie en wordt alleen ondersteund op de site op het hoogste niveau van de hiërarchie.  

     Nadat u een configuratie voor het **service verbindings punt**hebt geselecteerd, kiest u **volgende**. Nadat de installatie is voltooid, kunt u deze configuratie wijzigen vanuit de Configuration Manager-console. Zie [about the Service Connection Point](../configure/about-the-service-connection-point.md)(Engelstalig) voor meer informatie.  

19. Controleer op de pagina **samen vatting van instellingen** de instelling die u hebt geselecteerd. Wanneer u klaar bent, kiest u **volgende** om de prerequisite Checker te starten.  

20. Op de pagina **controle van vereiste installatie** worden eventuele problemen weer gegeven die door de controle kunnen worden geïdentificeerd.  

    - Wanneer de prerequisite Checker een probleem heeft gevonden, kiest u een item in de lijst voor meer informatie over het oplossen van het probleem.  

    - Voordat u kunt door gaan met het installeren van de-site, moet u **mislukte** items oplossen. Probeer ook items met de status **waarschuwing**op te lossen, maar de installatie van de site wordt niet geblokkeerd.  

    - Klik na het oplossen van problemen op **controle uitvoeren** om de prerequisite Checker opnieuw uit te voeren.  

        Wanneer de prerequisite checker wordt uitgevoerd en er geen controles zijn die een **mislukte** status krijgen, kunt u **installeren** starten om de installatie van de site te beginnen.  

    > [!TIP]  
    > Naast de feedback die de wizard biedt, vindt u in het bestand **ConfigMgrPrereq. log** aanvullende informatie over de vereiste problemen. Deze bevindt zich in de hoofdmap van het systeem station van de computer waarop u de site installeert. Zie [lijst met vereisten controles](list-of-prerequisite-checks.md)voor meer informatie.  

21. Op de pagina **installatie** wordt de installatie status weer gegeven. Wanneer de installatie van de basis site server is voltooid, kunt u de installatie wizard **sluiten** . Wanneer u de wizard sluit, worden de installatie en de eerste site configuraties op de achtergrond voortgezet.  

    - U kunt een Configuration Manager-console verbinden met de site voordat de installatie is voltooid. Deze console maakt verbinding als alleen-lezen en Hiermee kunt u objecten en instellingen weer geven, maar u kunt niets wijzigen.  

    - Nadat de installatie is voltooid, kunt u verbinding maken met een console die objecten en instellingen kan bewerken.  


## <a name="expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Een zelfstandige primaire site uitbreiden

Wanneer u een zelfstandige primaire site hebt geïnstalleerd als uw eerste site, hebt u de optie later om die site uit te breiden naar een grotere hiërarchie door een centrale beheer site te installeren.

Wanneer u een zelfstandige primaire site uitbreidt, installeert u een nieuwe centrale beheer site die gebruikmaakt van de bestaande zelfstandige primaire site database als referentie. Nadat de nieuwe centrale beheer site is geïnstalleerd, fungeert de zelfstandige primaire site als een onderliggende primaire site.

- U kunt een zelfstandige primaire site alleen uitbreiden naar een nieuwe hiërarchie.  

- U kunt slechts één zelfstandige primaire site uitbreiden naar een specifieke hiërarchie. U kunt deze optie niet gebruiken voor het toevoegen van extra zelfstandige primaire sites in dezelfde hiërarchie. Gebruik in plaats daarvan de migratie wizard om gegevens te migreren van de ene hiërarchie naar een andere. Zie voor meer informatie [migreren van gegevens tussen hiërarchieën](../../../migration/migrate-data-between-hierarchies.md).  

- Nadat u een zelfstandige site hebt uitgebreid naar een hiërarchie met een centrale beheer site, kunt u extra onderliggende primaire sites toevoegen.  

- Als u een primaire site van een hiërarchie met een centrale beheer site wilt verwijderen, moet u eerst de primaire site verwijderen.  

Als u de site wilt uitbreiden, gebruikt u de installatie wizard van Configuration Manager om een nieuwe centrale beheer site te installeren met de volgende voor behoud:  

- De centrale beheer site installeren met behulp van dezelfde versie van Configuration Manager als zelfstandige primaire site.  

- Selecteer op de pagina **aan de slag** van de installatie wizard de optie voor het installeren van een centrale beheer site. In een later stadium van Setup kiest u een optie om een bestaande zelfstandige primaire site uit te breiden.  

- Wanneer u de **client taal selectie** pagina voor de nieuwe centrale beheer site configureert, selecteert u dezelfde client talen die zijn geconfigureerd voor de zelfstandige primaire site die u wilt uitbreiden.  

- Selecteer op de pagina **site-installatie** de optie om de zelfstandige primaire site uit te breiden.  

Als u een zelfstandige primaire site wilt uitbreiden, raadpleegt u eerst de [vereisten om een site uit te breiden](prerequisites-for-installing-sites.md#bkmk_expand). Gebruik vervolgens de procedure om eerder in dit artikel [een primaire of centrale beheer site te installeren](use-the-setup-wizard-to-install-sites.md#bkmk_installpri) .


## <a name="install-a-secondary-site"></a><a name="bkmk_secondary"></a> Een secundaire site installeren

Gebruik de Configuration Manager-console om een secundaire site te installeren.  

- Als de console die u gebruikt, niet is verbonden met de primaire site die de bovenliggende site wordt naar de nieuwe secundaire site, wordt de opdracht voor het installeren van de site gerepliceerd naar de juiste primaire site.  

- Voordat u de site-installatie start, moet u ervoor zorgen dat uw gebruikers account over de vereiste machtigingen beschikt. Zorg er ook voor dat de server die als host zal fungeren voor de nieuwe secundaire site voldoet aan alle vereisten voor gebruik als secundaire site server.  

- Wanneer u de secundaire site installeert, configureert Configuration Manager de nieuwe site voor het gebruik van de client communicatie poorten die zijn geconfigureerd op de bovenliggende primaire site.  

### <a name="process-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a> Proces voor het installeren van een secundaire site  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** . Selecteer de site die de bovenliggende primaire site van de nieuwe secundaire site wordt.  

2. Klik op **secundaire site maken** op het lint om de **wizard secundaire site maken**te starten.  

3. Controleer op de pagina **voordat u begint** of de primaire site die wordt vermeld, de site is die u als bovenliggend element van de nieuwe secundaire site wilt maken. Kies vervolgens **volgende**.  

4. Geef op het tabblad **Algemeen** de volgende instellingen op:  

    - **Site code**: elke site code in een hiërarchie moet uniek zijn. Gebruik drie alfanumerieke cijfers: A t/m Z en 0 t/m 9. Omdat de site code in mapnamen wordt gebruikt, gebruikt u geen door Windows gereserveerde namen, waaronder:  

        - AUX  
        - CON  
        - NUL  
        - PRN  
        - Sms  

    > [!NOTE]  
    > Het installatie programma controleert niet of de door u opgegeven site code al wordt gebruikt, of dat het een gereserveerde naam is.  

    - **Naam site server**: deze waarde is de FQDN van de server waarop de nieuwe secundaire site wordt geïnstalleerd.  

    - **Site naam**: voor elke site is deze beschrijvende naam vereist, die u kan helpen bij het identificeren van de site.  

    - **Installatiemap**: deze map is het pad naar de Configuration Manager-installatie. U kunt de locatie niet wijzigen nadat de site is geïnstalleerd. Het pad mag geen Unicode-tekens of afsluitende spaties bevatten.  

    > [!IMPORTANT]  
    > Nadat u de details op deze pagina hebt opgegeven, kunt u **samen vatting** kiezen om rechtstreeks naar de **overzichts** pagina van de wizard te gaan. Bij deze actie worden de standaard instellingen voor de rest van de secundaire site opties gebruikt.  
    > 
    > - Gebruik deze optie alleen wanneer u bekend bent met de standaard instellingen in deze wizard. Dit zijn de instellingen die u wilt gebruiken.  
    > - Wanneer u de standaard instellingen gebruikt, worden grens groepen niet gekoppeld aan het distributie punt. Voordat u grens groepen configureert die de secundaire site server bevatten, gebruiken clients niet het distributie punt dat op deze secundaire site is geïnstalleerd als locatie van de inhouds bron.  

5. Kies op de pagina **bron bestanden voor installatie** hoe de secundaire site computer bron bestanden voor de installatie van de site verkrijgt.  

    Wanneer u CD gebruikt. De meest recente bron bestanden die worden gedeeld op het netwerk of lokaal naar de secundaire site server van de doel locatie worden gekopieerd:  

    - **Versie 1802 en lager**

        - De CD. De meest recente bron bestands locatie bevat een map met de naam **redist**. Verplaats deze map **redist** als een submap onder de map **SMSSETUP** .  

            > [!Note]  
            > Als tijdens de installatie niet-overeenkomende hashes optreden, werkt u de map **redist** bij. Gebruik het [Download programma](setup-downloader.md) voor de installatie om de meest recente bestanden op te halen. Voor bestanden die een fout met een niet-overeenkomende hash veroorzaken, kopieert u deze ook vanuit de bijgewerkte **redist** -map naar de map **SMSSETUP\BIN\X64** .

    - **Versie 1806 en hoger**<!-- SCCMDocs-pr issue 3164 -->

        - De CD. De meest recente bron bestands locatie bevat een map met de naam **redist**. Verplaats deze map **redist** als een submap onder de map **SMSSETUP** .  

        - Kopieer de volgende bestanden van de map **redist** naar de map **SMSSETUP\BIN\X64** :  
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Als een van de bestanden van **redist** niet beschikbaar is, mislukt de installatie van de secundaire site.  

    - Het computer account van de secundaire site server moet **Lees** machtigingen hebben voor de map van het bron bestand en de share.  

6. Geef op de pagina **SQL Server instellingen** de versie van SQL Server op die moet worden gebruikt en configureer vervolgens de gerelateerde instellingen.  

    > [!NOTE]  
    > Het installatie programma valideert de gegevens die u op deze pagina invoert pas wanneer de installatie wordt gestart. Voordat u doorgaat, controleert u deze instellingen.  

    - **Een lokale kopie van SQL Express installeren en configureren op de secundaire site computer**  

        - **SQL Server service poort**: geef de SQL Server service poort op die door SQL Server Express moet worden gebruikt. De service poort is doorgaans geconfigureerd voor het gebruik van TCP-poort 1433, maar u kunt een andere poort configureren.  

        - **SQL Server Broker-poort**: geef de SQL Server service BROKER (SSB)-poort op die SQL Server Express moet gebruiken. De Service Broker is doorgaans geconfigureerd voor het gebruik van TCP-poort 4022, maar u kunt een andere poort configureren. Geef een geldige poort op die niet wordt gebruikt door een andere site of service en dat er geen beperkingen voor de firewall worden geblokkeerd.  

    - **Een bestaand SQL Server exemplaar gebruiken**  

        - **SQL Server FQDN**: Controleer de FQDN-naam voor de computer met SQL Server. U moet een lokale server met SQL Server gebruiken om de data base van de secundaire site te hosten, en u kunt deze instelling niet wijzigen.  

        - **SQL Server exemplaar**: Geef het exemplaar van SQL Server op dat moet worden gebruikt als de secundaire site database. Laat deze optie leeg als u het standaard exemplaar wilt gebruiken.  

        - **Naam van ConfigMgr-site database**: Geef de naam op die moet worden gebruikt voor de secundaire site database.  

        - **SQL Server Broker-poort**: geef de SQL Server service BROKER (SSB)-poort op die SQL Server moet gebruiken. Geef een geldige poort op die niet wordt gebruikt door een andere site of service en die geen firewall beperkingen blok keren.  

    > [!TIP]  
    > Zie [ondersteunde SQL Server versies](../../../plan-design/configs/support-for-sql-server-versions.md)voor een lijst met de SQL Server versies die Configuration Manager ondersteunt.  

7. Configureer op de pagina **distributie punt** de instellingen voor het distributie punt dat wordt geïnstalleerd op de secundaire site server.  

    - **Vereiste instellingen:**  

        - **Opgeven hoe client apparaten communiceren met het distributie punt**: Kies tussen http en HTTPS.  

        - **Een zelfondertekend certificaat maken of een PKI-client certificaat importeren**: Kies tussen het gebruik van een zelfondertekend certificaat of het importeren van een certificaat uit uw PKI. Met een zelfondertekend certificaat kunt u ook anonieme verbindingen van Configuration Manager clients met de inhouds bibliotheek toestaan. Het certificaat wordt gebruikt om het distributie punt te verifiëren bij een beheer punt voordat het distributie punt status berichten verzendt. Zie [PKI-certificaat vereisten](../../../plan-design/network/pki-certificate-requirements.md)voor meer informatie.  

    - **Optionele instellingen:**  

        - **Installeer en CONFIGUREER IIS indien vereist door Configuration Manager**: Selecteer deze instelling Configuration Manager om Internet Information Services (IIS) te installeren en te configureren op de server, als deze nog niet is geïnstalleerd. IIS is vereist op alle distributie punten.  

            > [!NOTE]  
            > Hoewel deze instelling optioneel is, moet IIS op de server worden geïnstalleerd voordat een distributie punt kan worden geïnstalleerd.  

        - **BranchCache inschakelen en configureren voor dit distributie punt**  

        - **Beschrijving**: deze waarde is een beschrijvende beschrijving voor het distributie punt, zodat u deze kunt herkennen.  

        - **Dit distributie punt inschakelen voor voor bereide inhoud**  

8. Geef op de pagina **stations-instellingen** de instellingen van het station op voor het secundaire site distributiepunt.  

    U kunt Maxi maal twee schijf stations configureren voor de inhouds bibliotheek en twee schijf stations voor de pakket share. Configuration Manager kunnen echter extra stations gebruiken wanneer de eerste twee de geconfigureerde schijf ruimte reserveren. Op de pagina **Station Settings** configureert u de prioriteit voor de schijf stations en de hoeveelheid beschik bare schijf ruimte op elk schijf station.  

    - **Gereserveerde ruimte op station (MB)**: de waarde die u configureert voor deze instelling bepaalt de hoeveelheid vrije ruimte op een station voordat Configuration Manager een ander station kiest en het kopieer proces naar dat station doorloopt. Inhoudsbestanden kunnen meerdere stations omvatten.  

    - **Inhouds locaties**: Geef de inhouds locaties op voor de inhouds bibliotheek en de pakket share. Configuration Manager kopieert inhoud naar de primaire inhouds locatie totdat de hoeveelheid beschik bare ruimte de waarde bereikt die is opgegeven voor **gereserveerde ruimte op station (MB)**.  

    Standaard zijn de inhouds locaties ingesteld op **automatisch**. De primaire locatie van inhoud wordt ingesteld op het schijf station met de meeste schijf ruimte op de installatie tijd. De secundaire locatie wordt ingesteld op het schijf station met de meeste vrije schijf ruimte na de primaire schijf. Wanneer de primaire en secundaire schijven de reserve ring van de schijf ruimte bereiken, Configuration Manager een andere beschik bare schijf met de meeste vrije schijf ruimte selecteren en het kopieer proces voortzetten.  

9. Geef op de pagina **inhouds validatie** op of de integriteit van inhouds bestanden op het distributie punt moet worden gevalideerd.  

    - Wanneer u inhouds validatie op een planning inschakelt, wordt Configuration Manager het proces op het geplande tijdstip gestart. Alle inhoud op het distributie punt wordt gecontroleerd.  

    - U kunt ook de prioriteit van de **inhouds validatie**configureren.  

    - Als u de resultaten van het proces voor het valideren van de inhoud wilt weer geven, gaat u in de Configuration Manager-console naar de werk ruimte **bewaking** , vouwt u **distributie status**uit en selecteert u het knoop punt **inhouds status** . De inhoud voor elk pakket type wordt weer gegeven. Deze typen zijn onder andere toepassingen, software-update pakketten en opstart installatie kopieën.  

10. Beheer op de pagina **grens groepen** de grens groepen waaraan dit distributie punt is toegewezen:  

    - Tijdens de implementatie van inhoud moeten clients zich in een grens groep bevindt die is gekoppeld aan het distributie punt om deze te gebruiken als bron locatie voor inhoud.  

    - U kunt de optie **terugval bron locatie voor inhoud toestaan** selecteren om clients buiten deze grens groepen toe te staan om terug te vallen en het distributie punt te gebruiken als bron locatie voor inhoud wanneer er geen voorkeurs distributiepunten beschikbaar zijn.  

        Zie de [basis concepten voor inhouds beheer](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)voor meer informatie.  

11. Controleer op de pagina **samen vatting** de instellingen en kies vervolgens **volgende** om de secundaire site te installeren. Wanneer de wizard de **voltooiings** pagina presenteert, kunt u de wizard sluiten. De installatie van de secundaire site wordt op de achtergrond voortgezet.  

### <a name="how-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a> De status van de secundaire site-installatie controleren  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Selecteer de secundaire site die u wilt installeren en kies vervolgens **installatie status weer geven** in het lint.  

    > [!TIP]  
    > Wanneer u meer dan één secundaire site tegelijk installeert, wordt de prerequisite Checker uitgevoerd op één site tegelijk. Het moet een site volt ooien voordat de volgende site wordt gecontroleerd.
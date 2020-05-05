---
title: Windows Autopilot implementeren voor bestaande apparaten
titleSuffix: Configuration Manager
description: Een Configuration Manager taken reeks gebruiken om een Windows 7-apparaat te herstellen en in te richten voor de door de gebruiker gestuurde modus Windows auto pilot
ms.date: 03/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9f2ddf106c641c4433ddd1d09a2457900f670e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724207"
---
# <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot implementeren voor bestaande apparaten
<!--3607717, fka 1358333-->

*Van toepassing op: Configuration Manager (huidige vertakking)*

[Windows auto pilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) biedt organisaties een manier om nieuwe, ongewijzigde Windows 10-apparaten rechtstreeks naar de eind gebruiker te verzenden en de inrichtings stroom te definiëren die de gebruiker gaat passeren om een veilig, productief Windows 10-apparaat te krijgen. Het apparaat is geregistreerd bij de Windows auto pilot-service, zodat u het benodigde Windows auto pilot-profiel kunt toewijzen. Dit profiel definieert de out-of-Box Experience (OOBE) voor dat apparaat. 

[Windows auto pilot voor bestaande apparaten](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) is beschikbaar in Windows 10 versie 1809 of hoger. Met deze functie kunt u de installatie kopie van een Windows 7-apparaat voor de door de [gebruiker gestuurde Windows-modus voor automatische Piloting](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) en het inrichten met één systeem eigen Configuration Manager taken reeks. 



## <a name="prerequisites"></a>Vereisten

- Verkrijg de installatie media voor Windows 10 versie 1809 of hoger. Maak vervolgens een installatie kopie van het besturings systeem Configuration Manager. Zie [installatie kopieën van besturings systemen beheren](../get-started/manage-operating-system-images.md)voor meer informatie.

- In Microsoft Intune maakt u profielen voor Windows auto pilot. Zie [Windows-apparaten registreren bij intune met behulp van Windows auto pilot](https://docs.microsoft.com/intune/enrollment-autopilot)voor meer informatie.

- Een apparaat dat nog niet is geregistreerd bij de Windows auto pilot-service. Als het apparaat al is geregistreerd, heeft het toegewezen profiel voor rang. Het profiel auto pilot voor bestaande apparaten is alleen van toepassing als er een time-out optreedt voor het online profiel.



## <a name="create-the-configuration-file"></a>Het configuratie bestand maken

1. Open op een Windows-apparaat met Internet connectiviteit een Power shell-opdracht venster met beheerders rechten en voer de volgende opdrachten uit:  

    1. Installeer de vereiste modules en accepteer de prompts om door te gaan  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Aanmelden bij intune met beheerders referenties  
        ``` PowerShell  
        connect-msgraph 
        ```

    3. Alle Windows auto pilot-profielen ophalen die zijn gekoppeld aan uw intune-Tenant  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Maak een configuratie bestand voor elk profiel. De bestanden hebben de naam van de weergave naam van het profiel en worden opgeslagen op het bureau blad van de huidige gebruiker.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > Het configuratie bestand kan slechts één profiel bevatten. Elk profiel moet tussen accolades worden geplaatst `{}`.  

2. Sla een van de profielen op in een ANSI-gecodeerd bestand met de naam **AutopilotConfigurationFile. json**. Sla het bestand op een locatie op die geschikt is voor een Configuration Manager pakket bron.  

    > [!Tip]  
    > Als u de Power shell **-cmdlet uit het bestand** gebruikt om de JSON-uitvoer om te leiden naar een bestand, wordt standaard Unicode-code ring gebruikt. Met deze cmdlet kunnen ook lange regels worden afgekapt. Gebruik de cmdlet **set-content** met de `-Encoding ASCII` para meter om de juiste tekst codering in te stellen.   
    > 
    > Windows Klad blok maakt standaard gebruik van ANSI-code ring.  

3. Een Configuration Manager-pakket maken dat dit bestand bevat. Er is geen programma vereist. Zie [een pakket maken](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program)voor meer informatie.  

    > [!NOTE]  
    > Windows vereist dat dit bestand de naam **AutopilotConfigurationFile. json**heeft. Als u meer dan één auto pilot-profiel wilt gebruiken, maakt u afzonderlijke Configuration Manager-pakketten.  



## <a name="create-the-task-sequence"></a>De taken reeks maken

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer het knoop punt **taken reeksen** . Selecteer **taken reeks maken** in het lint.  

2. Selecteer op de pagina **nieuwe taken reeks maken** de optie voor het **implementeren van Windows auto pilot voor bestaande apparaten**.  

3. Geef op de pagina **taken reeks informatie** een naam op, eventueel een beschrijving toevoegen en een opstart installatie kopie selecteren. Zie [ondersteuning voor Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)voor meer informatie over ondersteunde versies van opstart installatie kopieën.  

4. Selecteer op de pagina **Windows installeren** het **installatie kopie pakket**voor Windows 10. Configureer vervolgens de volgende instellingen:  

    - **Afbeeldings index**: Selecteer Enter prise, education of Professional, zoals vereist door uw organisatie  

    - Schakel de optie voor het **partitioneren en Format teren van de doel computer in voordat u het besturings systeem installeert**  

    - **Taken reeks configureren voor gebruik met BitLocker**: als u deze optie inschakelt, bevat de taken reeks de stappen die nodig zijn om BitLocker in te scha kelen  

    - **Product code**: als u een product code voor Windows-activering wilt opgeven, voert u deze hier in  

    - Selecteer een van de volgende opties voor het configureren van het lokale Administrator-account in Windows 10:  
        - **Wille keurig wacht woord genereren voor lokale beheerder en het account uitschakelen op alle ondersteunings platforms (aanbevolen)**
        - **Het account inschakelen en lokaal beheerderswachtwoord instellen**

5. Selecteer op de pagina **netwerk configureren** de optie om **lid te worden van een werk groep**. Deze taken reeks maakt gebruik van het Windows-hulp programma voor systeem voorbereiding (Sysprep). Als het apparaat is toegevoegd aan een domein, mislukt de Sysprep.  

6. Voeg op de pagina **Configuration Manager installeren** de benodigde installatie-eigenschappen voor uw omgeving toe.  

    > [!Tip]  
    > De taken reeks heeft deze informatie alleen nodig als de Configuration Manager-client onderdelen nodig zijn tijdens de taken reeks voordat Sysprep wordt uitgevoerd. Bijvoorbeeld om software-updates of-toepassingen te installeren. Als u deze acties niet uitvoert, hoeft de client niet te worden gebruikt. Het wordt verwijderd voordat de taken reeks Sysprep uitvoert.  

7. De pagina **include updates** selecteert standaard de optie voor het **installeren van software-updates**.  

    > [!Tip]  
    > Gebruik offline-installatie kopie onderhoud om de installatie kopie up-to-date te houden met de nieuwste kwaliteits updates voor Windows 10. Zie [software-updates Toep assen op een installatie kopie van een besturings systeem](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)voor meer informatie.  

8. Op de pagina **toepassingen installeren** kunt u toepassingen selecteren die tijdens de taken reeks moeten worden geïnstalleerd. Micro soft raadt u echter aan de aanpak van de handtekening afbeelding te spie gelen met dit scenario. Nadat het apparaat is ingericht met auto pilot, moet u alle toepassingen en configuraties van Microsoft Intune of Configuration Manager co-beheer Toep assen. Dit proces vormt een consistente ervaring tussen gebruikers die nieuwe apparaten ontvangen en die gebruikmaken van Windows auto pilot voor bestaande apparaten.  

8. Selecteer op de pagina **systeem voorbereiding** het pakket dat het auto pilot-configuratie bestand bevat. De taken reeks start de computer standaard opnieuw op nadat Windows Sysprep is uitgevoerd. U kunt ook de optie voor het **afsluiten van de computer selecteren nadat deze taken reeks is voltooid**. Met deze optie kunt u een apparaat voorbereiden en vervolgens aan een gebruiker leveren voor een consistente auto pilot-ervaring.  

9. Voltooi de wizard.  

Als u de taken reeks bewerkt, is deze vergelijkbaar met de standaard taken reeks om een bestaande installatie kopie van het besturings systeem toe te passen. Deze taken reeks bevat de volgende aanvullende stappen:  

- **Windows auto pilot-configuratie Toep assen**: in deze stap wordt het auto pilot-configuratie bestand van het opgegeven pakket toegepast. Het is geen nieuw type stap, het is een **opdracht regel stap uitvoeren** om het bestand te kopiëren.  

- **Windows voorbereiden voor vastleggen**: met deze stap wordt Windows Sysprep uitgevoerd en wordt de instelling ingeschakeld om **de computer af te afsluiten nadat deze actie is uitgevoerd**. Zie [voorbereiden voor het vastleggen van Windows voor](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture)meer informatie.  

De taken reeks Windows auto pilot voor bestaande apparaten resulteert in een apparaat dat is gekoppeld aan Azure Active Directory (Azure AD). 

> [!NOTE]  
> Met Windows 10 versie 1903 en versie 1909 heeft auto pilot een bekend probleem waarbij Sysprep het bestand **AutopilotConfigurationFile. json** verwijdert. Als u deze methode gebruikt om Windows 10 versie 1903 of versie 1909 te implementeren, bewerkt u deze taken reeks en brengt u de volgende wijzigingen aan:
>
> 1. Schakel de stap **Windows voorbereiden voor vastleggen** uit.
> 2. Nadat u de stap **voor het voorbereiden van Windows voor vastleggen** hebt uitgeschakeld, voegt u een nieuwe stap **opdracht regel uitvoeren** toe. Configureer deze voor het uitvoeren van de volgende opdracht regel:`c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`
>
> Zie [Windows auto pilot-bekende problemen](https://docs.microsoft.com/windows/deployment/windows-autopilot/known-issues)voor meer informatie.

Gebruik de [bekende map](https://docs.microsoft.com/onedrive/redirect-known-folders) voor OneDrive voor bedrijven om ervoor te zorgen dat er een back-up wordt gemaakt van de gegevens van de gebruiker voordat de upgrade van Windows 10 wordt uitgevoerd.



## <a name="next-steps"></a>Volgende stappen

Gebruik co-beheer om de beheer functies van uw Windows 10-apparaten te verbeteren. Het tweede pad naar co-beheer is via modern inrichten met Windows auto pilot. Raadpleeg voor meer informatie de volgende artikelen:

- [Wat is co-beheer?](../../comanage/overview.md)
- [Paden naar co-beheer](../../comanage/quickstart-paths.md)
- [Windows Autopilot met co-beheer](../../comanage/quickstart-autopilot.md)

## <a name="see-also"></a>Zie ook

- [Windows-apparaten in Intune inschrijven met Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)

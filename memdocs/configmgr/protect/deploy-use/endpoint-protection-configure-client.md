---
title: Client instellingen Endpoint Protection
titleSuffix: Configuration Manager
description: Meer informatie over het configureren van aangepaste client instellingen voor Endpoint Protection.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25a1803d7a2feebe7947478c0671e0112830b0d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724319"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Aangepaste clientinstellingen configureren voor Endpoint Protection

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met deze procedure configureert u aangepaste client instellingen voor Endpoint Protection, die u kunt implementeren op verzamelingen apparaten in uw-hiërarchie.

> [!IMPORTANT]  
>  Configureer alleen de standaard instellingen voor Endpoint Protection-client als u zeker weet dat u deze wilt Toep assen op alle computers in uw hiërarchie. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Endpoint Protection inschakelen en aangepaste clientinstellingen configureren

1. Klik op **Beheer**in de Configuration Manager-console.  

2. Klik op **Clientinstellingen** in de werkruimte **Beheer**.  

3. Klik op het tabblad **Start** in de groep **Maken** op **Aangepaste clientapparaatinstellingen maken**.  

4. Geef in het dialoogvenster **Aangepaste clientapparaatinstellingen maken** een naam en een beschrijving op voor de groep instellingen en selecteer vervolgens **Endpoint Protection**.  

5. Configureer de Endpoint Protection client instellingen die u nodig hebt. Zie de sectie Endpoint Protection in [about client settings](../../core/clients/deploy/about-client-settings.md#endpoint-protection)(Engelstalig) voor een volledige lijst met Endpoint Protection client instellingen die u kunt configureren.  

   > [!IMPORTANT]  
   >  Installeer de Endpoint Protection-site systeemrol voordat u client instellingen voor Endpoint Protection configureert.  

6. Klik op **OK** om het dialoogvenster **Aangepaste clientapparaatinstellingen maken** te sluiten. De nieuwe clientinstellingen worden weergegeven in het knooppunt **Clientinstellingen** van de werkruimte **Beheer** .  

7. Implementeer vervolgens de aangepaste client instellingen voor een verzameling. Selecteer de aangepaste client instellingen die u wilt implementeren. Klik op het tabblad **Start** in de groep **client instellingen** op **implementeren**.  

8. Kies in het dialoogvenster **Verzameling selecteren** de verzameling waarin u de clientinstellingen wilt implementeren en klik vervolgens op **OK**. De nieuwe implementatie wordt weergegeven op het tabblad **Implementaties** van het detailvenster.  

Clients worden geconfigureerd met deze instellingen wanneer ze de volgende keer het client beleid downloaden. Zie [het ophalen van beleid initiëren voor een Configuration Manager-client](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)voor meer informatie.  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>De Endpoint Protection-client inrichten in een schijf installatie kopie

Installeer de Endpoint Protection-client op een computer die u wilt gebruiken als bron voor schijf installatie kopieën voor de implementatie van het besturings systeem Configuration Manager. Deze computer wordt doorgaans de referentiecomputer genoemd. Nadat u de installatie kopie van het besturings systeem hebt gemaakt, gebruikt u Configuration Manager implementatie van het besturings systeem om de installatie kopie te implementeren.

> [!Important]  
> Windows Defender is standaard geïnstalleerd op Windows 10 en Windows Server 2016. U hebt deze procedure niet nodig voor die versies van Windows.  

Gebruik de volgende procedures om u te helpen bij het installeren en configureren van de Endpoint Protection-client op een referentie computer.


### <a name="prerequisites"></a>Vereisten

De volgende lijst bevat de vereiste onderdelen voor het installeren van de Endpoint Protection-client software op een referentie computer.

- U moet toegang hebben tot het Endpoint Protection-client installatie pakket, **scepinstall. exe**. Dit pakket vindt u in de map **client** van de installatiemap Configuration Manager op de site server.  

- Als u de Endpoint Protection-client wilt implementeren met de vereiste configuratie van uw organisatie, maakt en exporteert u een antimalwarebeleid. Geef dit beleid vervolgens op wanneer u de Endpoint Protection-client hand matig installeert. Zie [How to Create and Deploy antimalware policies](endpoint-antimalware-policies.md)(Engelstalig) voor meer informatie.  

  > [!NOTE]  
  >  U kunt het **standaard-Antimalwarebeleid**van de client niet exporteren.  

- Als u de Endpoint Protection-client met de meest recente definities wilt installeren, downloadt u deze van [Windows Defender-beveiligings informatie](https://www.microsoft.com/wdsi).  

> [!NOTE]  
> Vanaf Configuration Manager 1802 hoeft u de Endpoint Protection agent (SCEPInstall) niet te installeren op Windows 10-apparaten. Als de app al is geïnstalleerd op Windows 10-apparaten, wordt deze niet door Configuration Manager verwijderd. Beheerders kunnen de Endpoint Protection-agent op Windows 10-apparaten waarop ten minste de 1802-client versie wordt uitgevoerd, verwijderen. SCEPInstall. exe kan nog steeds aanwezig zijn in C:\Windows\ccmsetup op sommige computers, maar nieuwe client installaties mogen deze niet downloaden. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>De Endpoint Protection-client installeren op de referentie computer

Installeer de Endpoint Protection-client lokaal op de referentie computer vanaf een opdracht prompt. Down load eerst het installatie bestand **scepinstall. exe**. Zie [de Endpoint Protection-client installeren vanaf een opdracht prompt](#bkmk_manual-install)voor meer informatie.

Als dat nodig is, moet u ook een vooraf geconfigureerd antimalwarebeleid of met een antimalwarebeleid dat u eerder hebt geëxporteerd. 



## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a><a name="bkmk_manual-install"></a>De Endpoint Protection-client installeren vanaf een opdracht prompt

1. Kopieer **scepinstall. exe** vanuit de map **client** van de map Configuration Manager-installatiemap naar de computer waarop u de Endpoint Protection-client software wilt installeren.  

2. Open een opdrachtprompt als beheerder. Wijzig de Directory in de map met het installatie programma. Voer `scepinstall.exe`vervolgens de volgende opdracht regel eigenschappen toe die u nodig hebt:


   |  Eigenschap   |                                  Beschrijving                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Het installatie programma op de achtergrond uitvoeren                           |
   |    `/q`     |                        De installatie bestanden op de achtergrond extra heren                        |
   |    `/i`     |                           Het installatie programma normaal uitvoeren                           |
   |  `/policy`  | Een antimalwarebeleid opgeven voor het configureren van de client tijdens de installatie |
   | `/sqmoptin` |     Aanmelden bij de micro soft-Customer Experience Improvement Program (CEIP)     |


3. Volg de instructies op het scherm om de client installatie te volt ooien.  

4. Als u het meest recente pakket met updatedefinities hebt gedownload, kopieert u dit pakket naar de clientcomputer en dubbelklikt u op het pakket om het te installeren.  

   > [!NOTE]  
   >  Nadat de Endpoint Protection-client installatie is voltooid, voert de client automatisch een controle van de definitie-update uit. Als deze update is geslaagd, hoeft u het meest recente definitie-update pakket niet hand matig te installeren.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Voor beeld: de client installeren met een antimalwarebeleid

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>De installatie van de Endpoint Protection-client controleren

Nadat u de Endpoint Protection-client op uw referentie computer hebt geïnstalleerd, controleert u of de client correct werkt.

1.  Open op de referentie computer **System Center Endpoint Protection** uit het systeemvak van Windows.  

2.  Controleer op het tabblad **Start** van het dialoog venster **System Center Endpoint Protection** of **realtime-beveiliging** is ingesteld op **aan**.  

3.  Controleer of **up-to-date** wordt weer gegeven voor **virus-en Spyware definities**.  

4.  Als u er zeker van wilt zijn dat uw referentie computer gereed is voor Imaging, selecteert u onder **Scan opties**de optie **volledig**en klikt u vervolgens op **Nu scannen**.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>De Endpoint Protection-client voorbereiden voor Imaging

Voer de volgende stappen uit om de Endpoint Protection-client voor te bereiden voor Imaging:

1. Meld u op de referentie computer aan als beheerder.  

2. Down load en Installeer **PsExec** van [Windows Sysinternals](https://docs.microsoft.com/sysinternals/downloads/psexec).  

3. Voer een opdracht prompt als beheerder uit, wijzig de Directory naar de map waarin u PsTools hebt geïnstalleerd en typ de volgende opdracht:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Wees voorzichtig wanneer u de REGI ster-editor op deze manier uitvoert. PsExec. exe wordt uitgevoerd in de context LocalSystem.  

4. Verwijder in de REGI ster-editor de volgende register sleutels:  

   > [!IMPORTANT]  
   >  Verwijder deze register sleutels als laatste stap voordat u de referentie computer Imaging. De Endpoint Protection-client maakt deze sleutels opnieuw wanneer het wordt gestart. Als u de referentie computer opnieuw opstart, moet u de register sleutels opnieuw verwijderen.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

U bent nu klaar om de referentie computer voor te bereiden voor Imaging.

Wanneer u een installatie kopie van een besturings systeem implementeert die de Endpoint Protection-client bevat, rapporteert deze automatisch informatie over de toegewezen Configuration Manager site van het apparaat. De client downloadt en past elk beoogd antimalwarebeleid toe.  



## <a name="see-also"></a>Zie ook

Zie [installatie kopieën van besturings systemen beheren](../../osd/get-started/manage-operating-system-images.md)voor meer informatie over de implementatie van het besturings systeem in Configuration Manager.


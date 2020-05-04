---
title: Client upgrades testen vóór productie verzameling
titleSuffix: Configuration Manager
description: Client upgrades testen in een pre-productie verzameling in Configuration Manager.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3098356eb96609867c0cc16b70d7b141e2a91c26
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715408"
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-configuration-manager"></a>Client upgrades testen in een pre-productie verzameling in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt een nieuwe Configuration Manager-client versie testen in een pre-productie verzameling voordat u de rest van de site bijwerkt.  Wanneer u dit doet, worden alleen de apparaten bijgewerkt die deel uitmaken van de test verzameling. Wanneer u de client hebt getest, kunt u de client promo veren, waardoor de nieuwe versie van de client software beschikbaar is voor de rest van de site.

> [!NOTE]
> Als u een test client wilt promo veren naar productie, moet u zijn aangemeld als een gebruiker met de beveiligingsrol **volledige beheerder** en een beveiligings bereik van **alle**. Zie [basis principes van beheer op basis van rollen](../../../understand/fundamentals-of-role-based-administration.md)voor meer informatie. U moet ook worden aangemeld bij een server die is verbonden met de centrale beheer site of een zelfstandige primaire site op het hoogste niveau.

 Er zijn 3 basis stappen voor het testen van clients in de pre-productie omgeving.  

1.  Automatische Client upgrades configureren voor het gebruik van een pre-productie verzameling.  

2.  Installeer een Configuration Manager update die een nieuwe versie van de client bevat.  

3.  Promoot de nieuwe client naar productie.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Automatische Client upgrades configureren voor het gebruik van een pre-productie verzameling  
> [!IMPORTANT]
> Client implementatie vóór productie wordt niet ondersteund voor werkgroepcomputers. Ze kunnen de verificatie niet gebruiken die vereist is voor het distributie punt om toegang te krijgen tot het client pakket vóór de productie.  Ze ontvangen de nieuwste-client wanneer deze is gepromoveerd tot de productie-client.

1. [Stel een verzameling](../collections/create-collections.md) in die de computers bevat waarvoor u de pre-productie-client wilt implementeren.   

2. Open **beheer** > **site configuratie** > **sites**in de Configuration Manager-console en kies **hiërarchie-instellingen**.  

    Op het tabblad **Clientupgrade** van de **Eigenschappen van de hiërarchie-instellingen**:  

   -   Selecteer **Automatisch upgrade uitvoeren voor alle clients in de pre-productieverzameling met gebruik van pre-productieclient**  

   -   Geef de naam van een verzameling op om te gebruiken als pre-productieverzameling  

![Client upgrades testen](media/test-client-upgrades.png)

>[!NOTE]
>Als u deze instellingen wilt wijzigen, moet uw account lid zijn van de beveiligingsrol **volledige beheerder** en het beveiligings bereik **alle** .


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Een Configuration Manager-update met een nieuwe versie van de client te installeren  

1.  Open in de console Configuration Manager **beheer** > **updates en onderhoud**, selecteer een **beschik bare** update en kies vervolgens **Update pakket installeren**. (Vóór versie 1702 werden updates en onderhoud onder **beheer** > **Cloud Services**.)

     Zie [updates voor Configuration Manager](../../../../core/servers/manage/updates.md) voor meer informatie over het installeren van updates.  

2.  Tijdens de installatie van de update selecteert u op de pagina **client opties** van de wizard de optie **testen in pre-productie verzameling**.  

3.  Voltooi de rest van de wizard en installeer het updatepakket.  

     Nadat de wizard is voltooid, beginnen clients in de pre-productieverzameling met het implementeren van de bijgewerkte client. U kunt de implementatie van bijgewerkte clients bewaken door te gaan naar **bewaking** > **client status** > **pre-productie client implementatie**. Zie de [client implementatie status controleren](../../../../core/clients/deploy/monitor-client-deployment-status.md)voor meer informatie.

    > [!NOTE]
    > De implementatie status op computers die site systeem rollen in een pre-productie verzameling hosten, kan worden gerapporteerd als **niet-compatibel** , zelfs als de client met succes is geïmplementeerd. Wanneer u promoveert naar productie, wordt de status van de implementatie correct gerapporteerd.

##  <a name="to-promote-the-new-client-to-production"></a>De nieuwe client naar productie promoten  

1.  Open **beheer** > **updates en onderhoud**in de Configuration Manager-console en kies vervolgens **client voor preproductie promo veren**. (Vóór versie 1702 werden updates en onderhoud onder **beheer** > **Cloud Services**.)

    > [!TIP]
    > De knop **Niveau van de pre-productieclient verhogen** is ook beschikbaar als u clientimplementaties controleert in de console via **Controleren** > **Clientstatus** > **Clientimplementatie vóór productie**.

2.  Controleer de client versies in productie en preproductie, zorg ervoor dat de juiste pre-productie verzameling is opgegeven en klik vervolgens op **niveau verhogen**en vervolgens op **Ja**.  

3.  Nadat het dialoog venster is gesloten, vervangt de bijgewerkte client versie de client versie die wordt gebruikt in uw-hiërarchie. Vervolgens kunt u de clients voor de gehele site upgraden. Zie [clients voor Windows-computers bijwerken](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) voor meer informatie.  

>[!NOTE]
>Als u de client vóór productie wilt inschakelen, of als u een pre-productie client wilt promo veren naar een productie-client, moet uw account lid zijn van een beveiligingsrol met de machtigingen **lezen** en **wijzigen** voor het object **update pakketten** .
>Bij Client upgrades worden Configuration Manager onderhouds Vensters geaccepteerd die u hebt geconfigureerd.

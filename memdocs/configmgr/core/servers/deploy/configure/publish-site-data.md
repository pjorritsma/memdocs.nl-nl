---
title: Sitegegevens publiceren
titleSuffix: Configuration Manager
description: Meer informatie over het publiceren van Configuration Manager-sites naar Active Directory Domain Services.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 77ca6711f86250f4a6f937d919893cf95e022567
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718362"
---
# <a name="publish-site-data-for-configuration-manager"></a>Site gegevens publiceren voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u het Active Directory schema voor Configuration Manager hebt uitgebreid, kunt u Configuration Manager-sites publiceren naar Active Directory Domain Services (AD DS). Hiermee kunnen Active Directory computers veilig site gegevens ophalen van een vertrouwde bron. Hoewel het publiceren van site-informatie naar AD DS niet is vereist voor de basis functionaliteit van Configuration Manager, kan dit de administratieve overhead verminderen.  

-   **Wanneer een site is geconfigureerd om naar AD DS te publiceren**, kunnen Configuration Manager-clients automatisch beheer punten vinden via Active Directory Publishing. Ze gebruiken een LDAP-query voor een globale catalogus server.  

-   **Wanneer een site niet naar AD DS publiceert**, moeten clients over een alternatief mechanisme beschikken om hun standaardbeheerpunt te zoeken.  

Zie [begrijpen hoe clients site resources en-services vinden voor Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)voor meer informatie over hoe clients een beheer punt vinden.  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Sites configureren om naar AD DS te publiceren  
 Hier volgen de hoofdstappen:  

-   U moet [het Active Directory schema voor Configuration Manager uitbreiden](../../../../core/plan-design/network/extend-the-active-directory-schema.md) in elk forest waar u site gegevens gaat publiceren. Zorg er ook voor dat de container voor **systeem beheer** aanwezig is.  

-   U moet het computer account van elke primaire site verlenen waarmee gegevens volledig worden **beheerd** naar de **systeem beheer** -container en alle onderliggende objecten.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Een Configuration Manager site inschakelen om site-informatie naar Active Directory forest te publiceren

1.  Klik op **Beheer**in de Configuration Manager-console.  

2.  Vouw in **Administration** de werk ruimte beheer **site configuratie**uit en klik op **sites**. Selecteer de site waarvan u de site gegevens wilt publiceren. Klik vervolgens op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

3.  Selecteer op het tabblad **publiceren** van de eigenschappen van de site de forests waarnaar deze site site gegevens gaat publiceren.  

4.  Klik op **OK** om de configuratie op te slaan.  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Active Directory bossen instellen voor publicatie  

1.  Klik op **Beheer**in de Configuration Manager-console.  

2.  Vouw in de werk ruimte **beheer** het knoop punt **hiërarchie configuratie**uit en klik op **Active Directory forests**. Als Active Directory-forestdetectie eerder is uitgevoerd, ziet u iedere gedetecteerde forest in het resultatenvenster. De lokale forest en vertrouwde forests worden gedetecteerd wanneer Active Directory-forestdetectie wordt uitgevoerd. U kunt niet-vertrouwde forests alleen handmatig toevoegen.  

    -   Als u een eerder gedetecteerd forest wilt instellen, selecteert u het forest in het resultaten venster. Klik vervolgens op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen** om de forest-eigenschappen te openen. Ga door met stap 3.  

    -   Als u een nieuw forest wilt instellen dat niet wordt vermeld, klikt u op het tabblad **Start** in de groep **maken** op **forest toevoegen** om het dialoog venster **forests toevoegen** te openen. Ga door met stap 3.  

3.  Op het tabblad **Algemeen** voert u de configuraties uit voor de forest die u wilt detecteren en geeft u het **Active Directory forest-account**op.  

    > [!NOTE]  
    >  Voor Active Directory-forestdetectie is een globaal account nodig om niet-vertrouwde forests te detecteren en ernaar te publiceren. Als u geen computeraccount van de siteserver gebruikt, kunt alleen een globaal account selecteren.  

4.  Als u van plan bent om sites sitegegevens te laten publiceren naar dit forest, vult u op het tabblad **Publiceren** de configuraties in voor publicatie naar dit forest.  

    > [!NOTE]  
    >  Als u sites inschakelt om te publiceren naar een forest, moet u het Active Directory schema van dat forest uitbreiden voor Configuration Manager. Het Active Directory forest-account moet machtigingen voor volledig beheer hebben voor de systeem container in dat forest.  

5.  Na voltooiing van de configuratie van deze forest voor Active Directory-forestdetectie, klikt u op **OK** om de configuratie op te slaan.  

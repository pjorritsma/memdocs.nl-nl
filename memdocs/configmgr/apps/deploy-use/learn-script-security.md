---
title: Meer informatie over Power shell-script beveiliging
titleSuffix: Configuration Manager
description: Bronnen voor meer informatie over de beveiliging van Power shell-scripts.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6b519d60be094bb7c39f738d04322009b36a409f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075860"
---
# <a name="learn-more-about-powershell-script-security"></a>Meer informatie over Power shell-script beveiliging

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het is de verantwoordelijkheid van de beheerder om het voorgestelde gebruik van Power shell-en Power shell-para meters in hun omgeving te valideren. Hier volgen enkele nuttige bronnen om beheerders te helpen informeren over de kracht van Power shell en mogelijke risico oppervlakken. Dit is om mogelijke risico oppervlakken te beperken en te voor komen dat veilige scripts worden gebruikt.

## <a name="powershell-script-security"></a>Beveiliging van Power shell-script
Ingebouwde scripts zijn een functie voor het visueel controleren en goed keuren van scripts die in de omgeving moeten worden uitgevoerd. Beheerders moeten er rekening mee houden dat Power shell-scripts een verborgen script kunnen hebben: script dat schadelijk is en moeilijk te detecteren is met visuele inspectie tijdens het goedkeurings proces van het script. Als best practice, kunt u met bepaalde inspectie Programma's, in aanvulling op het visueel controleren van Power shell-scripts, problemen met verdachte scripts detecteren. Met deze hulpprogram ma's kunt u niet altijd de intentie van de Power shell-Auteur bepalen, zodat er een verdacht script kan worden gemaakt. Voor de hulpprogram ma's moet de beheerder echter beoordelen of het een kwaad aardige of opzettelijke script syntaxis is.

## <a name="recommendations"></a>Aanbevelingen
- Lees meer over de aanbevolen procedures voor het gebruik van Power shell-beveiliging met behulp van de verschillende koppelingen waarnaar hieronder wordt verwezen.
- **Uw scripts ondertekenen**: een andere methode voor het beveiligen van scripts is door ze gecontroleerd en vervolgens te laten ondertekenen voordat ze worden geïmporteerd voor gebruik.
- Sla geheimen (zoals wacht woorden) niet op in Power shell-scripts en lees meer over het afhandelen van geheimen.


## <a name="general-information-about-powershell-security-best-practices"></a>Algemene informatie over best practices voor Power shell-beveiliging

Deze verzameling koppelingen is gekozen om Configuration Manager beheerders een start punt te geven voor het leren over de aanbevolen procedures voor het uitvoeren van Power shell-scripts.  

[Inleiding tot de aanbevolen procedures voor Power shell-beveiliging](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[Power shell-aanbevolen procedures voor beveiliging](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Beschermen tegen Power shell-aanvallen, Power shell-team blog](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Het beschermen tegen Power shell-aanvallen Twitter, vanuit een micro soft power shell en Security advocaat Lee Holmes](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Bescherming tegen schadelijke code injectie](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[Het blauwe team van Power shell, behandelt logboek registratie van uitgebreide script blokken, beveiligde logboek registratie, anti-malware-scan interface, Api's voor het genereren van code](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[Voor Windows 10 is er een API voor een anti-malware-scan interface](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Beveiliging van Power shell-para meters
Het door geven van para meters is een manier om flexibiliteit te bieden bij uw scripts en beslissingen uit te stellen tot de uitvoerings tijd. Er wordt ook een ander risico oppervlak geopend. Aanbevolen procedures voor het voor komen van schadelijke para meters of het afinjecteren van scripts:

- Alleen gebruik van vooraf gedefinieerde para meters toestaan.
- Gebruik de functie reguliere expressie om toegestane para meters te valideren.
    - Voor beeld: als slechts een bepaald bereik van waarden is toegestaan, gebruikt u een reguliere expressie om alleen te controleren of er tekens of waarden zijn die het bereik kunnen vormen.
    - Het valideren van para meters kan helpen voor komen dat gebruikers bepaalde tekens gebruiken die kunnen worden geescaped, zoals citaten. Houd er rekening mee dat er meerdere soorten aanhalings tekens kunnen zijn, zodat het gebruik van reguliere expressies kan worden gebruikt om te controleren welke tekens niet zijn toegestaan. Dit is vaak eenvoudiger dan het definiëren van alle invoer die niet is toegestaan.
- Gebruik de Power shell-module [' jagers Injection '](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) in de PowerShell Gallery.
    - Er kunnen valse positieven zijn, dus zoek naar opzet wanneer iets is gemarkeerd als verdacht om te bepalen of het een echt probleem is of niet. 
- Micro soft Visual Studio heeft een script analyse waarmee u de Power shell-syntaxis kunt controleren.
- Deze video met de titel: ' DEF CON 25-Lee Holmes-Get $pwnd: issued issued Windows Server ' geeft een overzicht van de soorten problemen die u kunt beveiligen (met name de sectie 12:20 tot 17:50):    <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Omgevings aanbevelingen
Algemene aanbevelingen voor Power shell-beheerders.
1. Implementeer de meest recente versie van Power shell, zoals versie 5 of hoger, ingebouwd in Windows 10. U kunt ook het [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616)implementeren. 
2. Power shell-logboeken inschakelen en verzamelen, eventueel inclusief beveiligde logboek registratie. Neem deze logboeken op in uw hand tekeningen, jacht en respons werk stromen voor incidenten.
3. Implementeer net voldoende beheer op hoogwaardige systemen om onbeperkte beheerders toegang tot deze systemen te elimineren of te verminderen.
4. Implementeer Windows Defender Application Control-beleid zodat vooraf goedgekeurde beheer taken de volledige mogelijkheid van de Power shell-taal kunnen gebruiken, terwijl interactief en niet-goedgekeurd gebruik wordt beperkt tot een beperkte subset van de Power shell-taal.
5. Implementeer Windows 10 om uw antivirus provider volledige toegang te geven tot alle inhoud (inclusief inhoud die tijdens runtime is gegenereerd of ongebruikt) die is verwerkt door Windows-Scripting hosts, waaronder Power shell.

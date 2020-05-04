---
title: Gegevens privacy voor desktop Analytics
titleSuffix: Configuration Manager
description: Desktop Analytics wordt toegepast op privacy van klant gegevens
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d6eaf5c8d7f1a58c944f175f2515c49267c1ee36
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714526"
---
# <a name="desktop-analytics-data-privacy"></a>Gegevens privacy voor desktop Analytics

Desktop Analytics is volledig doorgevoerd in de privacy van klant gegevens, gecentreerd op deze grond beginselen:

- **Transparantie:** De Windows-diagnose gebeurtenissen worden volledig gedocumenteerd. Bekijk ze met de beveiligings-en nalevings teams van uw bedrijf. Met de viewer voor diagnostische gegevens van Windows kunt u Diagnostische gegevens bekijken die vanaf een bepaald apparaat zijn verzonden. Zie voor meer informatie [overzicht van diagnostische gegevens Viewer](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Besturings element:** U bepaalt het niveau van diagnostische gegevens dat moet worden gedeeld met micro soft. Windows 10, versie 1709, voegt een nieuw beleid toe om uitgebreide diagnostische gegevens te beperken tot de minimale vereisten voor desktop Analytics.  

- **Beveiliging:** Micro soft beveiligt uw gegevens met sterke beveiliging en versleuteling.  

- **Vertrouwen:** Desktop Analytics ondersteunt de micro soft- [privacyverklaring](https://privacy.microsoft.com/privacystatement) en de [voor waarden voor Online Services](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  

Zie voor meer informatie [Windows-services waarbij micro soft de processor onder de AVG is](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr).<!-- 5353168 -->

## <a name="data-flow"></a>Gegevensstroom

In de volgende afbeelding ziet u hoe diagnostische gegevens van afzonderlijke apparaten stromen via de diagnostische gegevens service, tijdelijke opslag en naar uw Log Analytics-werk ruimte:

![Diagram illustreren van de stroom van diagnostische gegevens van apparaten](media/da-data-flow.png)

1. U meldt zich aan bij de Azure Portal en onboarding op Desktop Analytics. U maakt de Azure AD-app om verbinding te maken met Configuration Manager. Wanneer u Desktop Analytics instelt, maakt u een Azure Log Analytics-werk ruimte op de gewenste locatie.  

2. U verbindt Configuration Manager en registreert apparaten  

    1. U configureert de Desktop Analytics-Cloud service in Configuration Manager met de details van de Azure AD-app.  

    2. Binnen 15 minuten synchroniseert Configuration Manager de volgende gegevens met Desktop Analytics met behulp van uw Tenant-ID. Dit proces wordt elk uur herhaald.

      - Informatie over de verzamelingen die nodig zijn om [implementatie plannen te maken](create-deployment-plans.md). Deze informatie omvat de verzamelings-ID, de hiërarchie-ID, de naam van de verzameling en het aantal apparaten. 
      - Gegevens die nodig zijn voor het [inschrijven van apparaten](enroll-devices.md). Deze informatie omvat de verzamelings-ID, unieke id voor SMS, build-versie van het besturings systeem, de naam van het apparaat en het serie nummer.
      - Informatie van het dash board [verbindings status controleren](monitor-connection-health.md) . Deze informatie omvat het aantal apparaten per status en apparaateigenschappen.
      - Informatie over implementatie plannen, met inbegrip van de verzamelings-ID, implementatie-ID, test-of productie-implementatie type en het aantal apparaten per upgrade besluit.

    3. Configuration Manager stelt de commerciële ID, het niveau van diagnostische gegevens en andere instellingen voor de apparaten in de doel verzameling in. Met deze configuratie geeft u de apparaten op die moeten worden weer gegeven in de werk ruimte van uw bureau blad Analytics.  

    4. U implementeert compatibiliteits updates op alle doel apparaten.  

3. Apparaten verzenden diagnostische gegevens naar de micro soft Diagnostic Gegevensbeheer-service voor Windows. Deze service wordt gehost in de Verenigde Staten.  

4. Micro soft produceert elke dag een moment opname van de inzichten die IT-gericht zijn. In deze moment opname worden de diagnostische gegevens van Windows gecombineerd met de invoer voor de Inge schreven apparaten. Dit proces treedt op in tijdelijke opslag, wat alleen wordt gebruikt door Desktop Analytics. De tijdelijke opslag wordt gehost in micro soft-data centers in de Verenigde Staten. Alle gegevens worden verzonden via een met SSL (HTTPS) versleuteld kanaal. De moment opnamen worden gescheiden door de commerciële ID.  

5. De moment opnamen worden vervolgens gekopieerd naar uw Azure Log Analytics-werk ruimte. Deze gegevens overdracht vindt plaats via HTTPS via het webhook-opname protocol, een functie van Log Analytics. Desktop Analytics heeft geen lees-of schrijf machtigingen voor uw Log Analytics-opslag. Desktop Analytics roept de webhook-API aan met een SAS-URI (Shared Access Signature). Vervolgens haalt Log Analytics de gegevens op uit de opslag tabellen via HTTPS.

6. Desktop Analytics slaat uw invoer op in Log Analytics opslag. Deze configuraties omvatten implementatie plannen en activa beslissingen voor upgrade en urgentie.  

## <a name="other-resources"></a>Meer informatie

Zie [Veelgestelde vragen over privacy](faq.md#privacy)voor privacy-gerelateerde Veelgestelde vragen over desktop Analytics.

Raadpleeg de volgende artikelen voor meer informatie over verwante privacy-aspecten:

- [Windows 10 en de AVG voor IT-besluit vormers](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Windows diagnostische gegevens configureren in uw organisatie](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Gebeurtenissen en velden van diagnostische gegevens voor Windows 7, Windows 8 en Windows 8,1-beoordeling](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10, versie 1809 basis niveau Windows diagnostische gebeurtenissen en velden](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10, versie 1709 uitgebreide diagnostische gegevens gebeurtenissen en velden die worden gebruikt door Desktop Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Overzicht van viewer voor diagnostische gegevens](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Licentie voorwaarden en documentatie](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Log Analytics gegevens beveiliging](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Beveiliging en privacy op Microsoft Azure data centers](https://azure.microsoft.com/global-infrastructure/)  

- [Vertrouwen in de vertrouwde Cloud](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Vertrouwenscentrum](https://www.microsoft.com/trustcenter)  

- [Privacy-schild](https://www.privacyshield.gov/)  

Configuration Manager worden de diagnostische en gebruiks gegevens naar micro soft verzonden, gescheiden van de Desktop Analytics. Micro soft gebruikt deze gegevens voor het verbeteren van de installatie-ervaring, kwaliteit en beveiliging van toekomstige releases van Configuration Manager. Zie [Diagnostische en gebruiks gegevens voor Configuration Manager](../core/plan-design/diagnostics/diagnostics-and-usage-data.md)voor meer informatie.

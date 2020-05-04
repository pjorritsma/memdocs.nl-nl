---
title: Apparaten automatisch categoriseren in verzamelingen
titleSuffix: Configuration Manager
description: Apparaten automatisch in verzamelingen categoriseren.
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f91f150a095838484c516226da0d3e44e1f5b331
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714309"
---
# <a name="automatically-categorize-devices-into-collections"></a>Apparaten automatisch categoriseren in verzamelingen

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt apparaatcategorieën maken die kunnen worden gebruikt om apparaten automatisch in apparaatsets te plaatsen wanneer u Configuration Manager gebruikt met Microsoft Intune. Gebruikers moeten dan een apparaatcategorie kiezen wanneer ze een apparaat registreren bij intune. U kunt een apparaatcategorie wijzigen via de Configuration Manager-console.

> [!IMPORTANT]
>  Deze functie werkt met de versie van Microsoft Intune van **juni 2016** en hoger. Zorg ervoor dat u bent bijgewerkt naar deze release voordat u deze procedures uitprobeert.

## <a name="create-device-categories"></a>Apparaatcategorieën maken

1.  Ga naar **activa en naleving** > **overzicht** > **apparaat verzamelingen**.
2.  Klik op het tabblad **Start** in de groep **apparaat Collections** op **apparaatcategorieën beheren**.
3.  Categorieën maken, bewerken of verwijderen.

## <a name="associate-a-collection-with-a-device-category"></a>Een verzameling koppelen aan een apparaatcategorie

Wanneer u een verzameling aan een apparaatcategorie koppelt, worden alle apparaten in die categorie toegevoegd aan de verzameling. U kunt geen regel voor een apparaatcategorie toevoegen aan een ingebouwde verzameling zoals **alle systemen**.

1.  Kies op het tabblad **lidmaatschaps regels** van het dialoog venster **Eigenschappen** voor een verzameling apparaten de**regel regel categorie apparaat** **toevoegen** > .
2.  Selecteer in het dialoog venster **apparaatcategorieën selecteren** een of meer apparaatcategorieën die worden toegepast op alle apparaten in de verzameling.

## <a name="change-the-category-of-a-device"></a>De categorie van een apparaat wijzigen

1.  Selecteer een apparaat in de lijst **apparaten** in **activa en nalevings** > **overzicht** > **apparaten**.
2.  Klik op het tabblad **Start** in de groep **apparaat** op **categorie wijzigen**.
3.  Kies een categorie en klik vervolgens op **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Weer geven van welke categorie een apparaat behoort

In **activa en naleving** > **overzicht** > **apparaten**in de lijst met **apparaten** wordt de categorie in de kolom **apparaatcategorie** weer gegeven.

Als de kolom **apparaatcategorie** niet wordt weer gegeven, klikt u met de rechter muisknop op de kop van een van de kolommen in de lijst met **apparaten** (zoals **naam**) en selecteert u **apparaatcategorie**.

Als u een apparaat toewijst aan een categorie en vervolgens de categorie verwijdert, wordt in de **lijst met apparaten die per gebruiker zijn Inge schreven in Microsoft intune** een GUID weer gegeven in **de kolom apparaatcategorie** , in plaats van een categorie naam.

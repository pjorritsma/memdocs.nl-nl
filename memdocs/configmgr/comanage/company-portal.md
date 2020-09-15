---
title: Apps in de bedrijfsportal
titleSuffix: Configuration Manager
description: Geef een consistente gebruikers ervaring op voor gezamenlijk beheerde apparaten om de Bedrijfsportal-app te gebruiken.
ms.date: 09/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: 26456bb7-f46b-4d8d-bb0b-e3fd9a52fe14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d44116ee022f2f01fb8b84244fb903fa6d440345
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076155"
---
# <a name="use-the-company-portal-app-on-co-managed-devices"></a>Gebruik de bedrijfsportal-app op gezamenlijk beheerde apparaten

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--CMADO-3601237,INADO-4297660-->

Vanaf versie 2006 is de Bedrijfsportal nu de platform ervaring voor platformoverschrijdende apps voor micro soft Endpoint Manager. Door gezamenlijk beheerde apparaten te configureren om ook gebruik te maken van de Bedrijfsportal, kunt u op alle apparaten een consistente gebruikers ervaring bieden.

De Bedrijfsportal ondersteunt de volgende acties:

- Start de app Bedrijfsportal op gezamenlijk beheerde apparaten en meld u aan met Azure Active Directory (Azure AD) eenmalige aanmelding (SSO).
- Beschik bare en geïnstalleerde Configuration Manager-apps weer geven in de Bedrijfsportal naast intune-apps.
- Installeer beschik bare Configuration Manager apps via de Bedrijfsportal en ontvang informatie over de installatie status.

:::image type="content" source="media/3601237-company-portal.png" alt-text="Bedrijfsportal met app vanuit Configuration Manager" lightbox="media/3601237-company-portal.png":::

Het gedrag van de Bedrijfsportal is afhankelijk van de configuratie van de werk belasting voor co-beheer:

| Workload | Instelling | Gedrag |
|----------|---------|----------|
| Client-apps | **Configuration Manager** | U kunt alleen Configuration Manager client-apps weer geven |
| Client-apps | InTune of **intune** **testen** | U kunt zowel Configuration Manager als intune-client-apps zien |
| Office klik-en-klaar-apps | **Configuration Manager** | U kunt alleen Configuration Manager Office klik-en-klaar-apps weer geven |
| Office klik-en-klaar-apps | InTune of **intune** **testen** | U kunt alleen apps van intune Office-klik-en-klaar weer geven |

Raadpleeg voor meer informatie de volgende artikelen:

- [Diagram voor app-workloads](workloads.md#diagram-for-app-workloads)

- [Configuration Manager-workloads overschakelen naar Intune](how-to-switch-workloads.md)

## <a name="prerequisites"></a>Vereisten

- Configuration Manager huidige branch-versie 2006 of hoger <sup>([Zie Veelgestelde vragen](#bkmk_ver-prereq))</sup>

- App-versie 11.0.8980.0 of hoger Bedrijfsportal

- Windows 10, versie 1803 of hoger:

  - Inge schreven bij [co-beheer](how-to-enable.md)

  - Toegang tot [Internet eindpunten voor intune](../../intune/fundamentals/intune-endpoints.md)

- Voor de gebruikers accounts die zich aanmelden bij deze apparaten zijn de volgende configuraties vereist:

  - Een Azure AD-identiteit

  - Een intune-licentie toegewezen

## <a name="configure-and-deploy"></a>Configureren en implementeren

### <a name="configuration-manager-client-settings"></a>Client instellingen Configuration Manager

Configureer Configuration Manager client instellingen om ervoor te zorgen dat gebruikers alleen meldingen ontvangen van Bedrijfsportal. Wijzig in de **Software Center** -groep van Apparaatinstellingen **de optie de gebruikers Portal** die u wilt **bedrijfsportal**.

Raadpleeg de volgende artikelen voor meer informatie over client instellingen:

- [Clientinstellingen configureren](../core/clients/deploy/configure-client-settings.md)
- [Clientinstellingen](../core/clients/deploy/about-client-settings.md#software-center)

### <a name="deploy-the-company-portal-app"></a>De app Bedrijfsportal implementeren

- Gebruikers kunnen de Bedrijfsportal-app hand matig installeren vanuit de [Microsoft Store](https://www.microsoft.com/p/company-portal/9wzdncrfj3pz?activetab=pivot:overviewtab).

- Het implementatie proces is afhankelijk van de status van de werk belasting van de co-Management-client- [apps](workloads.md#client-apps) om de app op co-beheerde apparaten te vereisen:

  - Als de workload van de client-apps bestaat uit Configuration Manager, [maakt en implementeert u een toepassing met Configuration Manager](../apps/get-started/create-and-deploy-an-application.md). Down load de app voor offline Bedrijfsportal van de [Microsoft Store voor bedrijven](https://www.microsoft.com/business-store).

  - Als de workload van de client-apps met intune wordt uitgevoerd, kunt u deze implementeren via Configuration Manager of [de Windows 10 bedrijfsportal-app toevoegen met behulp van Microsoft intune](../../intune/apps/store-apps-company-portal-app.md).

Zie [How to Customize the intune-bedrijfsportal app](../../intune/apps/company-portal-app.md)(Engelstalig) voor meer informatie over het huis stijl van de bedrijfsportal voor uw organisatie.

## <a name="use-the-company-portal"></a>De Bedrijfsportal gebruiken

1. Start de Bedrijfsportal vanuit het menu Start. De momenteel aangemelde gebruiker wordt automatisch aangemeld bij de Bedrijfsportal op basis van hun Azure AD-identiteit.

1. Selecteer de pagina **apps** . U ziet Configuration Manager apps in de lijst.

1. Selecteer een van de apps die zijn geïmplementeerd vanuit Configuration Manager.

    - Het tabblad **overzicht** bevat details over de app, zoals grootte, versie en datum gepubliceerd.

    - Als u wilt zien dat Configuration Manager de beheer service voor deze app is, gaat u naar het tabblad **aanvullende informatie** .

    - Selecteer **installeren**om de app te installeren. De Bedrijfsportal geeft de installatie status weer en er wordt een melding weer gegeven wanneer deze is voltooid.

    - Als de app al is geïnstalleerd, selecteert u **verwijderen** om de app te verwijderen.

    - Selecteer het beletsel teken ( `...` ) voor aanvullende acties, zoals **herstellen** en **delen**.

        :::image type="content" source="media/3601237-company-portal-app-details.png" alt-text="Configuration Manager app met details in Bedrijfsportal" lightbox="media/3601237-company-portal-app-details.png":::

    - Nadat u een Configuration Manager web-app hebt geïnstalleerd, selecteert u het menu met weglatings tekens en selecteert u vervolgens **openen in browser** om de web-app te starten.

    - Als een Configuration Manager toepassing niet kan worden geïnstalleerd met een bekende fout code, selecteert u de koppeling mislukte status om te zoeken naar de fout code.

Als u de client instelling voor Bedrijfsportal wijzigt, wordt de Bedrijfsportal gestart wanneer een gebruiker een Configuration Manager melding selecteert. Als de melding betrekking heeft op een scenario, wordt de Bedrijfsportal niet ondersteund door het selecteren van de melding Software Center.

Als u problemen met de installatie van Configuration Manager-Apps wilt oplossen, gaat u naar de sectie **help & ondersteuning** in bedrijfsportal. Wanneer u de optie **Help ophalen** gebruikt, kunt u Configuration Manager-logboek bestanden verzenden als onderdeel van de aanvraag.

## <a name="frequently-asked-questions-faq"></a>Veelgestelde vragen

### <a name="im-using-configuration-manager-version-2002-why-is-the-new-company-portal-showing-configuration-manager-apps"></a><a name="bkmk_ver-prereq"></a> Ik gebruik Configuration Manager versie 2002, waarom is de nieuwe Bedrijfsportal Configuration Manager apps weer gegeven?

Bedrijfsportal versie 11.0.8980.0 of nieuwer bevat Configuration Manager geïmplementeerde toepassingen voor alle clients met co-beheer die deze gebruiken. Configuration Manager versie 2006 is de vereiste omdat hiermee de client instelling voor het beheren van meldingen wordt toegevoegd. Als u de Bedrijfsportal installeert op een gezamenlijk beheerd apparaat van een eerdere versie of als u de client instelling niet configureert, veroorzaakt dit gedrag dat voor gebruikers verwarrend is. Meldingen van Configuration Manager Software Center starten, terwijl meldingen van intune de Bedrijfsportal starten.

Micro soft raadt het volgende aan:

- Gebruik Bedrijfsportal versie 11.0.8980.0 of hoger op door co beheerde clients met Configuration Manager versie 2006 of hoger.
- De client instelling configureren **Selecteer de gebruikers Portal** die u wilt **bedrijfsportal**

### <a name="does-company-portal-support-applications-deployed-as-software-updates-from-configuration-manager"></a>Ondersteunt Bedrijfsportal toepassingen die worden geïmplementeerd als software-updates van Configuration Manager?

Ja. Als u een app implementeert met de functie software-updates, behandelt de client deze hetzelfde, ongeacht of de gebruikers ervaring is Bedrijfsportal of software Center.

### <a name="can-users-repair-uninstall-and-update-configuration-manager-apps-in-company-portal"></a>Kunnen gebruikers Configuration Manager-apps in Bedrijfsportal herstellen, verwijderen en bijwerken?

Ja. Als u de Configuration Manager-app configureert ter ondersteuning van deze aanvullende acties, ondersteunt Bedrijfsportal reparatie, verwijderen en bijwerken.

## <a name="known-issues"></a>Bekende problemen

De volgende functies van software Center zijn momenteel niet beschikbaar in de Bedrijfsportal:

- Bepaalde app-gegevens, bijvoorbeeld als opnieuw opstarten is vereist of de geschatte tijd voor de installatie

- [App-groepen](../apps/deploy-use/create-app-groups.md)

Andere bekende problemen:

- Als u dezelfde app implementeert vanuit zowel Configuration Manager als intune, wordt deze twee keer weer gegeven in de Bedrijfsportal.

- Wanneer u Bedrijfsportal zoekt, worden intune-apps altijd vóór Configuration Manager apps weer gegeven.

## <a name="next-steps"></a>Volgende stappen

[Configuration Manager-workloads overschakelen naar Intune](how-to-switch-workloads.md)

[De Intune-bedrijfsportal-App aanpassen](../../intune/apps/company-portal-app.md)

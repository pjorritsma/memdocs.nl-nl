---
title: Microsoft Launcher voor Android Enterprise configureren met Intune
titleSuffix: ''
description: Gebruik Intune-configuratiebeleid met Microsoft Launcher.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d9fe4c3a48cbf333fffd83d013b6a2d5fcf4ed9
ms.sourcegitcommit: ded11a8b999450f4939dcfc3d1c1adbc35c42168
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/01/2020
ms.locfileid: "89281129"
---
# <a name="configure-microsoft-launcher"></a>Microsoft Launcher configureren

Microsoft Launcher is een Android-toepassing waarmee gebruikers hun telefoon kunnen personaliseren, onderweg georganiseerd kunnen blijven, en kunnen overschakelen van werken op hun telefoon naar werken op de pc. 

In Launcher mogen IT-beheerders van bedrijven startschermen van volledig beheerde Android Enterprise-apparaten aanpassen, door de achtergrond, apps en posities van pictogrammen te selecteren. Hierdoor wordt het uiterlijk van alle beheerde Android-apparaten gestandaardiseerd op verschillende OEM-apparaten en systeemversies. 

## <a name="how-to-configure-the-microsoft-launcher-app"></a>De Microsoft Launcher-app configureren 

Nadat de Microsoft Launcher-app is [toegevoegd aan Intune](../apps/apps-add.md), navigeert u naar het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en selecteert u **Apps** > **Configuratiebeleid voor apps**. Voeg een configuratiebeleid toe voor **Beheerde apparaten** met **Android**, en kies **Microsoft Launcher** als bijbehorende app. Klik op **Configuratie-instellingen** om de verschillende beschikbare instellingen voor Microsoft Launcher te configureren. 

## <a name="choosing-a-configuration-settings-format"></a>Een indeling voor de configuratie-instellingen kiezen 

Er zijn twee methoden waarmee u configuratie-instellingen kunt definiëren voor Microsoft Launcher: 

- Met **Configuration Designer** kunt u instellingen configureren met een gebruiksvriendelijke gebruikersinterface waarmee u functies in of uit kunt schakelen en waarden kunt instellen. In deze methode zijn er enkele uitgeschakelde configuratiesleutels met waardetype BundleArray. Deze configuratiesleutels kunnen alleen worden geconfigureerd door JSON-gegevens in te voeren. 

- Met **JSON-gegevens** kunt u alle mogelijke configuratiesleutels definiëren met een JSON-script. 

Als u eigenschappen toevoegt met **Configuration Designer**, kunt u deze eigenschappen automatisch omzetten in JSON door **JSON-gegevens invoeren** te selecteren in de vervolgkeuzelijst **Indeling voor configuratie-instellingen**.

   ![Indeling voor configuratie-instellingen - Configuration Designer gebruiken](./media/configure-microsoft-launcher/configure-microsoft-launcher-01.png)

   > [!NOTE]
   > Zodra eigenschappen zijn geconfigureerd via Configuration Designer, worden de JSON-gegevens ook bijgewerkt zodat alleen deze eigenschappen worden weergegeven. Als u extra configuratiesleutels wilt toevoegen aan de JSON-gegevens, gebruikt u het [JSON-scriptvoorbeeld](../apps/configure-microsoft-launcher.md#microsoft-launcher-configuration-example) om de benodigde regels voor elke configuratiesleutel te kopiëren. 

Bij het bewerken van eerder gemaakte beleidsregels voor app-configuraties en als er complexe eigenschappen zijn geconfigureerd, wordt tijdens het bewerkingsproces de JSON-gegevenseditor weergegeven. Alle eerder geconfigureerde instellingen blijven behouden en u kunt overschakelen op het gebruik van Configuration Designer om ondersteunde instellingen te wijzigen.

## <a name="using-configuration-designer"></a>Configuration Designer gebruiken

Met Configuration Designer kunt u vooraf gevulde instellingen en de bijbehorende waarden selecteren.

   ![Indeling voor configuratie-instellingen - JSON-gegevens invoeren](./media/configure-microsoft-launcher/configure-microsoft-launcher-02.png)

De volgende tabel bevat de configuratiesleutels, waardetypen, standaardwaarden en beschrijvingen die beschikbare zijn in Microsoft Launcher. De beschrijving voorziet in het verwachte apparaatgedrag op basis van de geselecteerde waarden. Configuratiesleutels die zijn uitgeschakeld in Configuration Designer worden niet in de tabel weergegeven.

|    Configuratiesleutel    |    Waardetype    |    Standaardwaarde    |    Beschrijving     |
|---------------------------------------------------|------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Inschrijvingstype    |    Tekenreeks     |    Standaard    |    Hiermee kunt u het inschrijvingstype instellen waarop u dit beleid wilt toepassen. Momenteel verwijst de waarde **Standaard** naar **CorporateOwnedBuisnessOnly**. Er zijn momenteel geen andere ondersteunde inschrijvingstypen.        JSON-sleutelnaam: management_mode_key        |
|    Gebruiker toestaan de Home Screen-app-volgorde te wijzigen    |    Boolean-waarde    |    True    |    Hiermee kunt u opgeven of de **Home Screen-app-volgorde** kan worden gewijzigd door de eindgebruiker.<ul><li>Als dit is ingesteld op **True**, wordt de app-volgorde die is gedefinieerd in het beleid, alleen afgedwongen bij de eerste implementatie. Vervolgens wordt het beleid niet afgedwongen om eventuele wijzigingen door te voeren die zijn aangebracht door de gebruiker.</li><li>Als dit is ingesteld op **False**, wordt de app-volgorde afgedwongen bij elke synchronisatie.</li></ul><br>**Opmerking:** De Home Screen-app-volgorde kan alleen worden geconfigureerd met de JSON-editor.<br><br>JSON-sleutelnaam:<br>`com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed`    |
|    De rastergrootte instellen    |    Tekenreeks    |    Automatisch    |    Hiermee kunt u de rastergrootte instellen voor apps die op het startscherm moeten worden geplaatst. U kunt het aantal rijen en kolommen van de app instellen om de rastergrootte te definiëren in de volgende indeling: `columns;rows`. Als u de rastergrootte definieert, is het maximale aantal apps dat wordt weergegeven in een rij op het startscherm, het aantal rijen dat u instelt. Het maximale aantal apps dat wordt weergegeven in een kolom in het startscherm, is het aantal kolommen dat u instelt.<br><br>        JSON-sleutelnaam:<br>`com.microsoft.launcher.HomeScreen.GridSize`    |
|    Achtergrond van apparaat instellen    |    Tekenreeks    |    Null    |    Hiermee kunt u een achtergrond van uw keuze instellen, door de URL van de afbeelding in te voeren die u wilt instellen als achtergrond.<br><br>JSON-sleutelnaam:<br>`com.microsoft.launcher.Wallpaper.URL`    |
|    Gebruiker toestaan de achtergrond te wijzigen    |    Booleaanse waarde    |    True    |    Hiermee kunt u opgeven of de instelling Achtergrond van apparaat instellen kan worden gewijzigd door de eindgebruiker.<ul><li>Als dit is ingesteld op **True**, wordt de achtergrond in het beleid alleen afgedwongen bij de eerste implementatie. Vervolgens wordt het beleid niet afgedwongen om eventuele wijzigingen door te voeren die zijn aangebracht door de gebruiker.</li><li>Als dit is ingesteld op **False**, wordt de achtergrond afgedwongen bij elke synchronisatie.</li></ul><br>JSON-sleutelnaam:<br>`com.microsoft.launcher.Wallpaper.URL.UserChangeAllowed`        |
|    Feed inschakelen    |    Boolean-waarde    |    True    |    Hiermee kunt u de startfeed inschakelen op het apparaat, wanneer de gebruiker naar rechts swipet op het startscherm.<ul><li>Als dit is ingesteld op **True**, wordt de feed ingeschakeld.</li><li>Als dit is ingesteld op **False**, wordt de feed uitgeschakeld.</li></ul><br>JSON-sleutelnaam:<br>`com.microsoft.launcher.Feed.Enabled`    |
|    Gebruiker toestaan het inschakelen van de feed te wijzigen    |    Boolean-waarde    |    True    |     Hiermee kunt u opgeven of de instelling **Feed inschakelen** kan worden gewijzigd door de eindgebruiker.<ul><li>Als dit is ingesteld op **True**, wordt de feed alleen afgedwongen bij de eerste implementatie. Vervolgens wordt het beleid niet afgedwongen om eventuele wijzigingen door te voeren die zijn aangebracht door de gebruiker.</li><li>Als dit is ingesteld op **False**, wordt de feed afgedwongen bij elke synchronisatie.</li></ul><br>JSON-sleutelnaam:`com.microsoft.launcher.Feed.Enabled.UserChangeAllowed`    |
|    Plaatsing van de zoekbalk   |    Tekenreeks    |    Onderste    |  Hiermee kunt u de **plaatsing van de zoekbalk** op het startscherm opgeven. <ul><li>Als dit is ingesteld op **Onder**, bevindt de zoekbalk zich onderaan het startscherm.</li><li>Als dit is ingesteld op **Boven**, bevindt de zoekbalk zich bovenaan het startscherm.</li><li>Als dit is ingesteld op **Verborgen**, wordt de zoekbalk verwijderd uit het startscherm.</li></ul><br>JSON-sleutelnaam:<br>`com.microsoft.launcher.Search.SearchBar.Placement`    |
|    Gebruikers toestaan de plaatsing van de zoekbalk te wijzigen   |    Booleaanse waarde    |    True    |  Hiermee kunt u opgeven of de instelling **Plaatsing van de zoekbalk** kan worden gewijzigd door de eindgebruiker. <ul><li>Als dit is ingesteld op **True**, wordt de plaatsing van de zoekbalk alleen afgedwongen bij de eerste implementatie. Vervolgens wordt het beleid niet afgedwongen om eventuele wijzigingen door te voeren die zijn aangebracht door de gebruiker.</li><li>Als dit is ingesteld op **False**, wordt de plaatsing van de zoekbalk afgedwongen bij elke synchronisatie.</li></ul><br>JSON-sleutelnaam:<br>`com.microsoft.launcher.Search.SearchBar.Placement.UserChangeAllowed`<p>**OPMERKING:** Voor Microsoft Launcher v 6.2 en hoger wordt deze instelling niet meer afgedwongen. Daarom heeft het ook geen effect als u deze op `True` instelt. Uw eindgebruikers kunnen de locatie voor plaatsing van de zoekbalk niet aanpassen op hun apparaat.    |
|    Dock-modus  |    Tekenreeks    |    Weergeven    | Hiermee kunt u het dock inschakelen op het apparaat, wanneer de gebruiker naar rechts veegt op het startscherm.<ul><li>Als dit is ingesteld op **Weergeven**, wordt het dock ingeschakeld.</li><li>Als dit is ingesteld op **Verborgen**, wordt het dock verborgen in het startscherm. De gebruiker kan het dock echter weergeven wanneer dat nodig is.</li><li>Als dit is ingesteld op **Uitgeschakeld**, wordt het dock uitgeschakeld.</li></ul><br>JSON-sleutelnaam:<br>`com.microsoft.launcher.Dock.Mode`    |
|   Gebruiker toestaan het inschakelen van het dock te wijzigen   |    Tekenreeks    |    True    |  Hiermee kunt u opgeven of de instelling voor de Dock-modus kan worden gewijzigd door de eindgebruiker.<ul><li>Als dit is ingesteld op **True**, wordt de instelling voor de Dock-modus alleen afgedwongen bij de eerste implementatie. Vervolgens wordt het beleid niet afgedwongen om eventuele wijzigingen door te voeren die zijn aangebracht door de gebruiker.</li><li>Als dit is ingesteld op **False**, wordt de instelling voor de Dock-modus afgedwongen bij elke synchronisatie.</li></ul><br>JSON-sleutelnaam:<br>`com.microsoft.launcher.Dock.Mode.UserChangeAllowed`    |

## <a name="enter-json-data"></a>JSON-gegevens invoeren

Voer JSON-gegevens in voor het configureren van alle beschikbare instellingen voor Microsoft Launcher, evenals de instellingen die zijn uitgeschakeld in **Configuration Designer**, zoals hieronder weergegeven.

   ![Configuration Designer - JSON-gegevens](./media/configure-microsoft-launcher/configure-microsoft-launcher-03.png)

Naast de lijst met configureerbare instellingen in de tabel Configuration Designer (hierboven) biedt de volgende tabel de configuratiesleutels die u alleen kunt configureren via JSON-gegevens.

|    Configuratiesleutel    |    Waardetype    |    Standaardwaarde    |    Beschrijving     |
|----------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    De in de whitelist opgenomen toepassingen instellen<br>JSON-sleutel:`com.microsoft.launcher.HomeScreen.Applications`    |    BundleArray    | Zie: [De in de whitelist opgenomen toepassingen instellen](configure-microsoft-launcher.md#set-allow-listed-applications)</sup>    |    Hiermee kunt u de apps definiëren die op het startscherm worden weergegeven. U kunt kiezen uit alle apps die zijn geïnstalleerd op het apparaat. U definieert de apps door de naam van het app-pakket in te voeren van de apps die u zichtbaar wilt maken. Met `com.android.settings` voegt u bijvoorbeeld instellingen toe aan het startscherm. De apps die u in deze sectie op de whitelist plaatst, moeten al op het apparaat zijn geïnstalleerd om te worden weergegeven op het startscherm.<p>Eigenschappen:<ul><li>**Pakket:** Naam van het toepassingspakket</li><li>**Klasse:** De toepassingsactiviteit die specifiek is voor een bepaalde app-pagina. Als deze waarde leeg is, wordt de standaardpagina van de app gebruikt.</li></ul>      |
|    Home Screen-app-volgorde<br>JSON-sleutel: `com.microsoft.launcher.HomeScreen.AppOrder`    |    BundleArray    |    Zie: [Home Screen-app-volgorde](configure-microsoft-launcher.md#home-screen-app-order)      |    Hiermee kunt u de app-volgorde op het startscherm opgeven.<p>Eigenschappen:<br><ul><li>**Type:** Als u posities van apps wilt opgeven, wordt alleen `application` ondersteund. Als u posities van webkoppelingen wilt opgeven, is het type `weblink`.</li><li>**Positie:** Hiermee geeft u de sleuf voor het toepassingspictogram op het startscherm op. Deze begint vanaf positie 1 linksboven en gaat van links naar rechts, en van boven naar beneden.</li><li>**Pakket:** Dit is de naam van het toepassingspakket dat wordt gebruikt om de app-volgorde op te geven.</li><li>**Klasse:** De toepassingsactiviteit die specifiek is voor een bepaalde app-pagina. Als deze waarde leeg is, wordt de standaardpagina van de app gebruikt. Deze eigenschap wordt gebruikt voor de app.</li><li>**Label**: De toepassingsactiviteit die specifiek is voor een bepaalde app-pagina. Als deze waarde leeg is, wordt de standaardpagina van de app gebruikt. Deze eigenschap wordt gebruikt voor de app.</li><li>**Koppeling**: De URL die moet worden gestart nadat de eindgebruiker op het pictogram voor de webkoppeling klikt. Deze eigenschap wordt gebruikt voor de webkoppeling.</li></ul>    |
|    Vastgemaakte webkoppelingen instellen<br>JSON-sleutel: `com.microsoft.launcher.HomeScreen.WebLinks`    |    BundleArray    |    Zie: [Vastgemaakte webkoppelingen instellen](configure-microsoft-launcher.md#set-pinned-web-link)      |    Met deze sleutel kunt u websites vastmaken op het startscherm als pictogrammen voor snel starten. Op die manier kunt u ervoor zorgen dat de eindgebruiker snel en eenvoudig toegang tot essentiële websites heeft. U kunt de locatie van elk pictogram van een webkoppeling in de configuratie van Home Screen-app-volgorde wijzigen.<p>Eigenschappen:<br><ul><li>**•  Label**: De titel van de webkoppeling wordt weergegeven op het startscherm van MS Launcher.</li><li>**Koppeling**: De URL die moet worden gestart nadat de eindgebruiker op het pictogram voor de webkoppeling klikt.</li></ul>    |


### <a name="set-allow-listed-applications"></a>De in de whitelist opgenomen toepassingen instellen

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.Applications",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="home-screen-app-order"></a>Home Screen-app-volgorde

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "type",
                    "valueString": "application"
                },
                {
                    "key": "position",
                    "valueInteger": 0
                },
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="set-pinned-web-link"></a>Vastgemaakte webkoppeling instellen

```JSON
{ 
    "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "label",
                    "valueString": "" 
                },  
                { 
                    "key": "link", 
                    "valueString": "" 
                } 
            ] 
        }
    ] 
},
{ 
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "type",  
                    "valueString": "" 
                },  
                { 
                    "key": "position",  
                    "valueInteger": 
                },  
                { 
                    "key": "label",  
                    "valueString": "" 
                },  
                { 
                    "key": "link",  
                    "valueString": "" 
                } 
            ] 
        }
    ] 
}
```



### <a name="microsoft-launcher-configuration-example"></a>Configuratievoorbeeld van Microsoft Launcher

Hier volgt een voorbeeld-JSON-script met alle beschikbare configuratiesleutels die erin zijn opgenomen:

```JSON
{
    "kind": "androidenterprise#managedConfiguration", 
    "productId": "app:com.microsoft.launcher", 
    "managedProperty": [
        {
            "key": "management_mode_key", 
            "valueString": "Default"
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable", 
            "valueBool": true
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url", 
            "valueString": "http://www.contoso.com/wallpaper.png"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.GridSize", 
            "valueString": "5;5"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.Applications", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }
            ]
        }, 
        { 
            "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
            "valueBundleArray": [ 
                { 
                    "managedProperty": [ 
                        { 
                            "key": "label",
                            "valueString": "News" 
                        },  
                        { 
                            "key": "link", 
                            "valueString": "https://www.bbc.com" 
                        } 
                    ] 
                }
            ] 
        },
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 17
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 18
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 19
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "weblink"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 20
                        }, 
                        {
                            "key": "label", 
                            "valueString": "News"
                        }, 
                        {
                            "key": "link", 
                            "valueString": "https://www.bbc.com"
                        }
                    ]
                }
            ]
        }
    ]
}

```

## <a name="next-steps"></a>Volgende stappen

- Zie [Intune-inschrijving van volledig beheerde Android Enterprise-apparaten instellen](../enrollment/android-fully-managed-enroll.md) voor meer informatie over volledig beheerde Android Enterprise-apparaten.

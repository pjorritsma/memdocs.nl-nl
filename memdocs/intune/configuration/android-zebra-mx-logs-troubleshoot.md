---
title: StageNow-logboeken gebruiken op Android Zebra-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Zie veelvoorkomende problemen en oplossingen wanneer u StageNow op Android-apparaten gebruikt met Microsoft Intune. U krijgt ook meer informatie over het ophalen van logboeken en voorbeelden van hoe u de logboeken controleert op succes of fouten.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d8c7c60b4d9d1831aaabb9886345865234ce6351
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364614"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>Problemen oplossen en potentiële problemen op Android Zebra-apparaten in Microsoft Intune weergeven



In Microsoft Intune kunt u [Zebra Mobility Extensions (MX) gebruiken om Android Zebra-apparaten te beheren](android-zebra-mx-overview.md). Wanneer u Zebra-apparaten gebruikt, maakt u profielen in StageNow om instellingen te beheren en uploadt u deze naar Intune. Intune maakt gebruik van de StageNow-app om de instellingen op de apparaten toe te passen. De StageNow-app maakt ook een gedetailleerd logboekbestand op het apparaat dat wordt gebruikt voor het oplossen van problemen.

Deze functie is van toepassing op:

- Android

U maakt bijvoorbeeld een profiel in StageNow om een apparaat te configureren. Wanneer u het StageNow-profiel maakt, genereert u met de laatste stap een bestand voor het testen van het profiel. U verbruikt dit bestand met de StageNow-app op het apparaat.

In een ander voorbeeld maakt u een profiel in StageNow en test u het. In Intune voegt u het StageNow-profiel toe en wijst u dit toe aan uw Zebra-apparaten. Bij het controleren van de status van het toegewezen profiel wordt in het profiel een status op hoog niveau weer gegeven.

In beide gevallen kunt u meer details ophalen uit het StageNow-logboekbestand dat steeds wordt opgeslagen op het apparaat wanneer een StageNow-profiel van toepassing is.

Sommige problemen zijn niet gerelateerd aan de inhoud van het StageNow-profiel en worden niet weergegeven in de logboeken.

In dit artikel zien u hoe u de StageNow-logboeken kunt lezen en leest u over een aantal andere potentiële problemen met Zebra-apparaten die mogelijk niet in de logboeken worden weergegeven.

In [Zebra-apparaten gebruiken en beheren met Zebra Mobility-extensies](android-zebra-mx-overview.md) vindt u meer informatie over deze functie.

## <a name="get-the-logs"></a>De logboeken ophalen

### <a name="use-the-stagenow-app-on-the-device"></a>De StageNow-app op het apparaat gebruiken
Wanneer u een profiel rechtstreeks op uw computer test met StageNow, in plaats van [Intune te gebruiken om het profiel te implementeren](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow), slaat de StageNow-app op het apparaat de logboeken uit de test op. Als u het logboekbestand wilt ophalen, gebruikt u de optie **Meer (...)** in de StageNow-app op het apparaat.

### <a name="get-logs-using-android-debug-bridge"></a>Logboeken ophalen met Android Debug Bridge
Als u logboeken wilt ophalen nadat het profiel al is geïmplementeerd met Intune, verbindt u het apparaat met een computer met [Android debug Bridge (ADB)](https://developer.android.com/studio/command-line/adb) (opent de website van Android).

Op het apparaat worden logboeken opgeslagen in `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files`

### <a name="get-logs-from-email"></a>Logboeken ophalen van e-mail
Als u logboeken wilt ophalen nadat het profiel al is geïmplementeerd met Intune, kunnen eindgebruikers u de logboeken via e-mail verzenden via een e-mail-app op het apparaat. Open de bedrijfsportal-app op het Zebra-apparaat en [verzend de logboeken](https://docs.microsoft.com/user-help/send-logs-to-your-it-admin-by-email-android). Met de functie Logboeken verzenden wordt ook een PowerLift-incident-id gemaakt, waarnaar u kunt verwijzen als u contact opneemt met Microsoft Ondersteuning.

## <a name="read-the-logs"></a>De logboeken lezen

Wanneer u de logboeken bekijkt, wordt er een foutbericht weergegeven wanneer u de tag `<characteristic-error>` ziet. Foutdetails worden geschreven naar de tag `<parm-error>` > eigenschap `desc`.

## <a name="error-types"></a>Fouttypen

Zebra-apparaten bevatten verschillende foutrapportageniveaus:

- De CSP wordt niet ondersteund op het apparaat. Het apparaat is bijvoorbeeld geen mobiel apparaat en heeft geen mobiele manager.
- De MX-of OSX-versie komt niet overeen. Elke CSP heeft een versienummer. Raadpleeg de [documentatie van Zebra](http://techdocs.zebra.com/mx/) (opent de website van Zebra) voor een volledige ondersteuningsmatrix.
- Het apparaat rapporteert nog een probleem of fout.

## <a name="examples"></a>Voorbeelden

U hebt bijvoorbeeld het volgende invoerprofiel:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

In het logboek is de XML identiek aan de invoer. Deze overeenkomende uitvoer betekent dat het profiel zonder fouten is toegepast op het apparaat:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

U hebt bijvoorbeeld het volgende invoerprofiel:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

In het logboek wordt een fout weergegeven, aangezien het een `<characteristic-error>`-tag bevat. In dit scenario heeft het profiel geprobeerd een Android-pakket (APK) te installeren dat niet voorkomt in het opgegeven pad:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Andere potentiële problemen met Zebra-apparaten

In deze sectie vindt u andere mogelijke problemen die kunnen optreden wanneer u Zebra-apparaten met een Apparaatbeheerder gebruikt. Deze problemen worden niet gerapporteerd in de StageNow-logboeken.

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView is verouderd

Wanneer oudere apparaten zich aanmelden met behulp van de bedrijfsportal-app, zien gebruikers mogelijk een bericht dat het onderdeel System WebView is verouderd en dat het moet worden bijgewerkt. Als Google Play is geïnstalleerd op het apparaat, kunt u verbinding maken met internet en controleren op updates. Als Google Play niet is geïnstalleerd op het apparaat, kunt u de bijgewerkte versie van het onderdeel ophalen en op de apparaten toepassen. U kunt ook bijwerken naar het meest recente besturingssysteem van het apparaat dat is uitgegeven door Zebra.

### <a name="management-actions-take-a-long-time"></a>Beheeracties nemen veel tijd in beslag

Als Google Play-services niet beschikbaar zijn, duurt het maximaal acht uur voordat sommige taken zijn voltooid. [Beperkingen van de Intune-bedrijfsportal-app voor Android](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china) (opent een andere Microsoft-website) kan een goede resource zijn.

### <a name="device-spoofing-suspected-shows-in-intune"></a>'Vermoedelijke apparaatspoofing' wordt weergegeven in Intune

Deze fout betekent dat Intune vermoedt dat een niet-Zebra Android-apparaat het model en de fabrikant weergeeft als een Zebra-apparaat.

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>De bedrijfsportal-app is ouder dan de minimaal vereiste versie

Intune kan de minimaal vereiste versie van de bedrijfsportal-app bijwerken. Als Google Play niet op het apparaat is geïnstalleerd, wordt de bedrijfsportal-app niet automatisch bijgewerkt. Als de minimaal vereiste versie nieuwer is dan de geïnstalleerde versie, werkt de bedrijfsportal-app niet meer. Update naar de nieuwste bedrijfsportal-app met behulp van [sideloaden op Zebra-apparaten](android-zebra-mx-overview.md#sideload-the-company-portal-app).

## <a name="next-steps"></a>Volgende stappen

[Zebra-discussieforums](https://developer.zebra.com/community/home/discussions) (opent de website van Zebra)

[Zebra-apparaten gebruiken en beheren met Zebra Mobility Extensions in Intune](android-zebra-mx-overview.md)

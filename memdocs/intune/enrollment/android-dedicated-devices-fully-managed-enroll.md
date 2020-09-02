---
title: Toegewezen Android Enterprise-apparaten, volledig beheerde apparaten of apparaten met een werkprofiel in bedrijfseigendom inschrijven in Intune
titleSuffix: Microsoft Intune
description: Meer informatie over toegewezen Android Enterprise-apparaten, volledig beheerde apparaten of apparaten met een werkprofiel in bedrijfseigendom inschrijven in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9fafc6a48e933fbcce692c560532736808cbf7c4
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915242"
---
# <a name="enroll-your-android-enterprise-dedicated-fully-managed-or-corporate-owned-with-work-profile-devices"></a>Uw toegewezen Android Enterprise-apparaten, volledig beheerde apparaten of apparaten met een werkprofiel in bedrijfseigendom inschrijven

Nadat u uw [toegewezen Android Enterprise-apparaten](android-kiosk-enroll.md), [volledig beheerde apparaten](android-fully-managed-enroll.md) of [apparaten met een werkprofiel in bedrijfseigendom](android-corporate-owned-work-profile-enroll.md) in Intune hebt ingesteld, kunt u de apparaten inschrijven. Registratie van Intune voor zowel toegewezen apparaten als volledig beheerde apparaten begint met het terugzetten van de fabrieksinstellingen. De manier waarop u uw Android Enterprise-apparaten inschrijft, is afhankelijk van het besturingssysteem.

| Inschrijvingsmethode | Minimumversie van het Android-besturingssysteem voor toegewezen en volledig beheerde apparaten |
| ----- | ----- |
| Near Field Communication | 6.0 |
| Tokenvermelding | 6.0 |
| QR-code | 7.0 |
| Zero Touch  | 8.0<br><br> Van deelnemende fabrikanten. |
| [Knox Mobile Enrollment](./android-samsung-knox-mobile-enroll.md)  | 6.0<br><br> Alleen op apparaten met Samsung Knox 2.8 of hoger. |

## <a name="enroll-by-using-near-field-communication-nfc"></a>Registreren met Near Field Communication

Apparaten met 6 en hoger die ondersteuning bieden voor NFC, kunnen worden ingericht door een speciaal opgemaakte NFC-tag te maken. U kunt uw eigen app of een hulpprogramma voor het maken van NFC-tags gebruiken. Zie [NFC-based Android Enterprise device enrollment with Microsoft Intune](/archive/blogs/cbernier/nfc-based-android-enterprise-device-enrollment-with-microsoft-intune) (Op NFC gebaseerde inschrijving van Android Enterprise-apparaten met Microsoft Intune) en [Google's Android Management API documentation](https://developers.google.com/android/management/provision-device#nfc_method) (Android Management API-documentatie van Google) voor meer informatie.

## <a name="enroll-by-using-a-token"></a>Registreren met een token

Op apparaten met Android 6 en hoger kunt u het token gebruiken om het apparaat te registreren. Bij Android 6.1 en latere versies kan ook gebruik worden gemaakt van de QR-code, in combinatie met de inschrijvingsmethode **afw#setup**.

1. Schakel uw gewiste apparaat in.
2. Selecteer uw taal in het scherm **Welkom**.
3. Maak verbinding met uw **Wi-Fi** en kies vervolgens **VOLGENDE**.
4. Accepteer de Google-voorwaarden en kies **VOLGENDE**.
5. Voer in plaats van een Gmail-account in het aanmeldscherm van Google **afw #setup** in en kies **VOLGENDE**.
6. Kies **INSTALLEREN** voor de app **Beleid voor Android-apparaat**.
7. Ga door met de installatie van dit beleid.  Op sommige apparaten moet u mogelijk aanvullende voorwaarden accepteren.
8. Sta in het scherm **Dit apparaat registreren** toe dat uw apparaat de QR-code mag scannen of stel in dat u het token handmatig invoert.
9. Volg de aanwijzingen op het scherm om de inschrijving te voltooien.

## <a name="enroll-by-using-a-qr-code"></a>Registreren met een QR-code

Op apparaten met Android 7 en hoger kunt u de QR-code scannen van het inschrijvingsprofiel om het apparaat in te schrijven.

> [!Note]
> Inzoomen op de browser kan ertoe leiden dat apparaten geen QR-code kunnen scannen. Dit probleem wordt opgelost door de zoomfactor van de browser te vergroten.

1. Tik meerdere keren op het eerste scherm dat u ziet nadat het apparaat is gewist om een QR te starten die op het Android-apparaat wordt gelezen.
2. Voor apparaten met Android 7 en 8 wordt u gevraagd om een QR-lezer te installeren. Op Android-apparaten 9 of hoger is al een QR-lezer geïnstalleerd.
3. Gebruik de QR-lezer om de QR-code van het inschrijvingsprofiel te scannen en volg de aanwijzingen op het scherm om het apparaat in te schrijven.

## <a name="enroll-by-using-google-zero-touch"></a>Registreren met Zero Touch van Google

Voor het gebruik van het Google Zero Touch-systeem moet het apparaat hiervoor ondersteuning bieden en kunnen worden gekoppeld aan een leverancier die deel uitmaakt van de service.  Zie [de programmawebsite van Zero Touch van Google](https://www.android.com/enterprise/management/zero-touch/) voor meer informatie.

1. Maak een nieuwe configuratie in de Zero Touch-console.
2. Kies **Microsoft Intune** in de vervolgkeuzelijst EMM DPC.
3. Kopieer en plak de volgende JSON in het veld DPC-extra's in de Google Zero Touch-console. Vervang de tekenreeks *YourEnrollmentToken* door het inschrijvingstoken dat u hebt gemaakt als onderdeel van het inschrijvingsprofiel. Zet het inschrijvingstoken tussen dubbele aanhalingstekens.

    ```json
    {
        "android.app.extra.PROVISIONING_DEVICE_ADMIN_COMPONENT_NAME": "com.google.android.apps.work.clouddpc/.receivers.CloudDeviceAdminReceiver",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_SIGNATURE_CHECKSUM": "I5YvS0O5hXY46mb01BlRjq4oJJGs2kuUcHvVkAPEXlg",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_PACKAGE_DOWNLOAD_LOCATION": "https://play.google.com/managed/downloadManagingApp?identifier=setup",

        "android.app.extra.PROVISIONING_ADMIN_EXTRAS_BUNDLE": {
            "com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "YourEnrollmentToken"
        }
    }
    ```

4. Kies **Toepassen**.

## <a name="enroll-by-using-knox-mobile-enrollment"></a>Inschrijven met Knox Mobile Enrollment
Voor het gebruik van Knox Mobile Enrollment van Samsung moet op het apparaat Android OS versie 6 of hoger en Samsung Knox 2.8 of hoger worden uitgevoerd. Leer [hoe u uw apparaten automatisch kunt inschrijven met Knox Mobile Enrollment](./android-samsung-knox-mobile-enroll.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
- [Android-apps implementeren](../apps/apps-deploy.md)
- [Configuratiebeleid voor Android toevoegen](../configuration/device-profiles.md)
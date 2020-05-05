---
title: Statusberichten
titleSuffix: Configuration Manager
description: Beschrijvingen van status berichten in de ondersteunde versies van Configuration Manager.
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720931"
---
# <a name="state-messages-in-configuration-manager"></a>Status berichten in Configuration Manager 

*Van toepassing op: Configuration Manager (huidige vertakking)*

Status berichten bevatten beknopte informatie over de voor waarden van de Configuration Manager-client. Het status berichten systeem wordt gebruikt door specifieke onderdelen van Configuration Manager, zoals software-updates en configuratie-instellingen.

Configuration Manager-clients verzenden status berichten naar terugval status punt of beheer punt site systemen om de huidige status van de bewerkingen te rapporteren. U kunt rapporten maken om status berichten weer te geven die zijn verzonden door Configuration Manager-clients.

Elke Configuration Manager-functie die gebruikmaakt van status berichten wordt geïdentificeerd door het onderwerp type van het status bericht. De typen voor het status bericht onderwerp die in dit artikel worden vermeld, kunnen worden gebruikt voor het definiëren van de Configuration Manager-functie waarmee een status bericht is gekoppeld.

> [!NOTE]  
> De waarde van de status bericht-ID nul (0) geeft meestal aan dat het type van het onderwerp een onbekende status heeft.

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 0 | Nalevings status is onbekend|
| 1 | Compatibel | 
| 2 | Niet-compatibel | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 0  | Afdwingings status is onbekend |
| 1  | Update (s) installeren        | 
| 2  | Wachten op opnieuw opstarten          | 
| 3  | Wachten tot een andere installatie is voltooid         | 
| 4  | De update is geïnstalleerd (2)          | 
| 5  | Opnieuw starten van systeem in behandeling         | 
| 6  | Kan de update (s) niet installeren         | 
| 7  | De update (s) downloaden   | 
| 8  | Gedownloade update (s)    | 
| 9  | Kan update (s) niet downloaden     | 
| 10 | Wachten op het onderhouds venster vóór de installatie         | 
| 11 | Wachten op indeling         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|      
| 0 | Evaluatie status is onbekend|                 
| 1 |Evaluatie is geactiveerd      |
| 2 |De evaluatie is voltooid      |
| 3 |De evaluatie is mislukt      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 0 | Detectie status is onbekend|
| 1 | Niet vereist   |
| 2 | Niet gedetecteerd    |
| 3 | Gedetecteerd   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 0 | Nalevings status is onbekend|
| 1 |Compatibel     |
| 2 |Niet-compatibel     |
| 3 |Conflict gedetecteerd    |
| 4 |Fout      |
| 5 |Onbekend     |
| 6 |Gedeeltelijke naleving   |
| 7 |Naleving niet geconfigureerd    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 0  | Afdwingings status is onbekend|
| 1  |Afdwinging is gestart          |
| 2  |Afdwinging wacht op inhoud         |
| 3  | Wachten tot een andere installatie is voltooid        |
| 4  |Wachten op het onderhouds venster vóór de installatie         |
| 5  |Opnieuw opstarten is vereist voor de installatie         |
| 6  |Algemene fout        |
| 7  |Wachtend op installatie         |
| 8  |Update installeren          |
| 9  |Opnieuw starten van systeem in behandeling        |
| 10 |De update is geïnstalleerd         |
| 11 |Kan de update niet installeren        |
| 12 |Update downloaden        |
| 13 | Gedownloade update        |
| 14 |Kan de update niet downloaden        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
|0 |Detectie status is onbekend|
| 1 | Update is niet vereist  |
| 2 | Update is vereist   |
| 3 | Update is geïnstalleerd  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 0 |Scan status is onbekend|
| 1 | De scan wacht op inhoud   |
| 2 | De scan wordt uitgevoerd    |
| 3 | De scan is voltooid    |
| 4 | Nieuwe poging voor scannen is in behandeling   |
| 5 | Kan niet scannen   |
| 6 | De scan is voltooid met fouten |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

Geen status-Id's.

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

Geen status-Id's.

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
Geen status-Id's.

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 100 |Client implementatie is gestart      |       
| 101 |Wachten op downloaden       |       
| 102 |Implementatie gepland       |       
| 103 | Wachten op het venster vóór de implementatie |
| 104 |De implementatie is overgeslagen       |       
| 301 |Fout bij onbekende client implementatie |       
| 302 |Kan de ccmsetup-service niet maken  |       
| 303 |Kan de ccmsetup-service niet verwijderen |       
| 304 |Kan niet installeren over het Inge sloten besturings systeem met op file-based Write Filter (FBWF) ingeschakeld op het systeem station |       
| 305 |De native beveiligings modus is niet geldig voor Windows 2000  |       
| 306 |Kan het ccmsetup-download proces niet starten  |       
| 307 |Niet-geldige ccmsetup-opdracht regel |       
| 308 |Kan het bestand niet downloaden via WINHTTP op het adres |       
| 309 |Kan de bestanden niet downloaden via BITS op het adres |       
| 310 |Kan BITS-versie niet installeren |       
| 311 |Kan niet controleren of het vereiste bestand is ondertekend met MS  |       
| 312 |Kan het bestand niet kopiëren omdat de schijf vol is |       
| 313 |Installatie van client. msi is mislukt met MSI-fout |       
| 314 |Kan manifest bestand ccmsetup. XML niet laden |       
| 315 |Kan geen client certificaat verkrijgen  |       
| 316 |Vereist bestand is niet ondertekend door MS |       
| 317 |Opnieuw opstarten is vereist om door te gaan met de installatie  |       
| 318 |De client kan niet worden geïnstalleerd op het MP omdat de MP-en client versies niet overeenkomen |       
| 319 |Het besturings systeem of Service Pack wordt niet ondersteund  |       
| 320 |Implementatie wordt niet ondersteund       |       
| 321 |Ontbrekende bits        |       
| 322 |Bronmap is niet beschikbaar       |       
| 323 |Appv wordt niet ondersteund              |       
| 324 |Onjuiste site versie              |       
| 325 |De vereiste hash-waarden komen niet overeen       |       
| 326 |Kan MDM-verwijdering niet opheffen      |       
| 327 |MDM-registratie gedetecteerd      |       
| 328 |InTune gedetecteerd       |       
| 329 |Netwerk met data limiet niet toegestaan      |       
| 400 |Client implementatie is voltooid |  
| 401 |De implementatie is voltooid opnieuw opstarten is vereist     |       
| 402 |De implementatie is voltooid     |
| 500 |Client toewijzing is gestart|
| 601 |Fout bij onbekende client toewijzing|
| 602 |De volgende site code is ongeldig|
| 603 |Kan niet toewijzen aan MP|
| 604 |Kan het standaard beheer punt niet detecteren|
| 605 |Kan het handtekening certificaat van de site niet downloaden|
| 606 |Kan site code niet automatisch detecteren|
| 607 |Site toewijzing is mislukt; de client versie is hoger dan de site versie|
| 608 |Kan de site versie van Active Directory Domain Services en SLP niet ophalen|
| 609 |Kan de client versie niet ophalen|
| 700 |Client toewijzing is voltooid|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

Geen status-Id's.

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 100 | Status van inschrijving   |
| 101 | Geplande inschrijving   |
| 102 | Inschrijving geannuleerd   |
| 105 | Inschrijving is gestart   |
| 106 | De inschrijving is voltooid, maar is niet ingericht
| 107 | De inschrijving is voltooid en is ingericht
| 108 | Geen actieve gebruiker inschrijven   |
| 110 | Inschrijving is mislukt   |


## <a name="820--state_topictype_client_wufb"></a>820 STATE_TOPICTYPE_CLIENT_WUFB

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 | Status van Windows Update voor zakelijke client| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 | Schijf ruimte   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

Geen status-Id's.

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

Geen status-Id's.

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

Geen status-Id's.

## <a name="1000--state_topictype_client_framework_comm"></a>1000 STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 | De client communiceert met het beheer punt |
| 2 | Client kan niet communiceren met het beheer punt |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Client heeft het certificaat opgehaald uit het lokale certificaat archief    |
| 2 |Client kan het certificaat niet ophalen uit het lokale certificaat archief |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

Geen status-Id's.

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

Geen status-Id's.

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

Geen status-Id's.

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

Geen status-Id's.

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

Geen status-Id's.

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

Geen status-Id's.

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

Geen status-Id's.

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

Geen status-Id's.

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

Geen status-Id's.

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

Geen status-Id's.

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

Geen status-Id's.

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

Geen status-Id's.

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

Geen status-Id's.

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

Geen status-Id's.

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Client is niet gereed voor native modus  |
| 2 |Client gereed voor native modus     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 | Geslaagd|
| 2 | Niet geslaagd |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

Geen status-Id's.

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

Geen status-Id's.

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

Geen status-Id's.

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

Geen status-Id's. 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Gebruikers affiniteit instellen       |
| 2 |Gebruikers affiniteit verwijderd       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

Geen status-Id's.

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

Geen status-Id's.

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1000  |Configuratie-item is voltooid           |
| 1001 |Het configuratie-item is al geïnstalleerd         |
| 1002 |Geslaagde configuratie-item Preflight          |
| 1003 |Snelle status van configuratie-item is voltooid          |
| 2000 |Configuratie-item wordt uitgevoerd           |
| 2001 |Configuratie-item wordt uitgevoerd wacht op inhoud         |
| 2002 |Configuratie-item wordt geïnstalleerd          |
| 2003 |Configuratie-item wordt uitgevoerd wacht op opnieuw opstarten         |
| 2004 |Configuratie-item wordt uitgevoerd wacht op onderhouds venster        |
| 2005 |Wacht tijd van configuratie-item in behandeling         |
| 2006 |Bezig met downloaden van afhankelijke inhoud door configuratie-item     |
| 2007 |Configuratie-item bezig met installeren van afhankelijkheden        |
| 2008 |Configuratie-item wordt uitgevoerd in afwachting van opnieuw opstarten         |
| 2009 |Inhoud van configuratie-item wordt gedownload         |
| 2010 |Update van configuratie-item wordt uitgevoerd in behandeling         |
| 2011 |Configuratie-item wordt uitgevoerd wacht op opnieuw verbinden met gebruiker        |
| 2012 |Configuratie-item wordt uitgevoerd wacht totdat de gebruiker zich afmeldt         |
| 2013 |Configuratie-item wordt uitgevoerd wacht op aanmelding van gebruiker         |
| 2014 |Configuratie-item wordt uitgevoerd wacht op installatie         |
| 2015 |Configuratie-item wordt uitgevoerd wacht op nieuwe poging         |
| 2016 |Configuratie-item wordt uitgevoerd wacht op presmode         |
| 2017 |Configuratie-item wordt uitgevoerd wacht op orchestration        |
| 2018 |Configuratie-item wordt uitgevoerd wacht op netwerk         |
| 2019 |Configuratie-item wordt uitgevoerd in afwachting van update VE         |
| 2020 |Configuratie-item wordt bijgewerkt         |
| 3000 |Niet voldaan aan configuratie-item vereisten           |
| 3001 |Niet voldaan aan de vereisten voor configuratie-items waarvoor de host niet van toepassing is        |
| 4000 |Configuratie-item onbekend           |
| 5000 |Fout in configuratie-item            |
| 5001 |Fout bij evaluatie van configuratie-item          |
| 5002 |Fout bij het installeren van configuratie-item          |
| 5003 |Fout bij het ophalen van inhoud door configuratie-item         |
| 5004 |Fout bij het installeren van afhankelijkheid configuratie-item         |
| 5005 |Fout bij het ophalen van de inhouds afhankelijkheid van het configuratie-item        |
| 5006 |Conflict met fout regels voor configuratie-item          |
| 5007 |Fout in configuratie-item tijdens wachten op nieuwe poging          |
| 5008 |Fout in configuratie-item bij verwijderen van vervanging        |
| 5009 |Fout bij het downloaden van configuratie-item vervangen         |
| 5010 |Fout bij het bijwerken van configuratie-item VE          |
| 5011 |Fout bij het installeren van de licentie voor configuratie-item         |
| 5012 |Fout bij ophalen configuratie-item alle vertrouwde apps toestaan       |
| 5013 |Fout in configuratie-item er zijn geen licenties beschikbaar         |
| 5014 |Fout besturings systeem configuratie-item niet ondersteund          |
| 6000 |Het configuratie-item is gestart            |
| 6010 |Fout bij starten van configuratie-item            |
| 6020 |Starten configuratie-item onbekend|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

Geen status-Id's.

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

Geen status-Id's.

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

Geen status-Id's.

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

Geen status-Id's.

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

Geen status-Id's.

## <a name="1901-state_topictype_ep_am_health"></a>1901 State_Topictype_Ep_Am_Health

Geen status-Id's.

## <a name="1902-state_topictype_ep_malware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

Geen status-Id's.

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

Geen status-Id's.

## <a name="2001-state_topictype_ep_client_deployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Endpoint Protection niet-beheerd   |
| 2 |Endpoint Protection wachten op installatie  |
| 3 |Beheerd door Endpoint Protection   |
| 4 |Installatie van Endpoint Protection is mislukt  |
| 5 |Endpoint Protection opnieuw opstarten in behandeling  |
| 6 |Endpoint Protection wordt niet ondersteund   |
| 7 |Endpoint Protection gezamenlijk beheerd   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 0 |Status van Endpoint Protection-beleids toepassing onbekend    |
| 1 |Toepassing Endpoint Protection beleid is voltooid    |
| 2 |Toepassing Endpoint Protection beleid is mislukt    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 0 |  Onbekend    |
| 1 |  Actief    |
| 2 |  Niet-actief    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 | De activerings proxy is niet geïnstalleerd    |
| 2 | De activerings proxy wacht op installatie   |
| 3 | De activerings proxy is geïnstalleerd    |
| 4 | Kan de installatie van de activerings proxy niet uitvoeren   |
| 5 | De activerings proxy wacht op opnieuw opstarten   |
| 6 | De activerings proxy wordt niet ondersteund voor dit besturings systeem  |
| 7 | Opt-out voor de proxy server uitschakelen   |
| 8 | Verwijderen van Ontwaak proxy is mislukt   |
| 9 | Runtime voor activerings proxy wordt niet ondersteund   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

Geen status-Id's.

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

Geen status-Id's.

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

Geen status-Id's.

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
|0 | Channel set van Windows Push Notification-Service|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

Geen status-Id's.

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

Geen status-Id's.

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

Geen status-Id's.

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

Geen status-Id's.

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

Geen status-Id's.

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

Geen status-Id's.

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

Geen status-Id's.

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

Geen status-Id's.

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

Geen status-Id's.

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

Geen status-Id's.

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

Geen status-Id's.

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

Geen status-Id's.

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Vraag uitgegeven         |
| 2 |Controle probleem mislukt        |
| 3 |Het maken van de aanvraag is mislukt        |
| 4 |Verzenden van aanvraag is mislukt        |
| 5 |Validatie van Challenge geslaagd       |
| 6 |Validatie van controle is mislukt       |
| 7 |Probleem mislukt         |
| 8 |Probleem in behandeling         |
| 9 |Gepubliceerd          |
| 10 |Verwerking van antwoord is mislukt       |
| 11 |Antwoord in behandeling         |
| 12 |Inschrijving geslaagd         |
| 13 |Inschrijving niet vereist         |
| 14 |Revoked          |
| 15 |Verwijderd uit verzameling        |
| 16 |Gecontroleerd vernieuwen         |
| 17 |Installatie mislukt        |
| 18 |Geïnstalleerd         |
| 19 |Kan niet verwijderen         |
| 20 |Verwijderen         |
| 21 |Verlenging aangevraagd        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Vraag uitgegeven         |
| 2 |Controle probleem mislukt        |
| 3 |Het maken van de aanvraag is mislukt        |
| 4 |Verzenden van aanvraag is mislukt        |
| 5 |Validatie van Challenge geslaagd       |
| 6 |Validatie van controle is mislukt       |
| 7 |Probleem mislukt         |
| 8 |Probleem in behandeling         |
| 9 |Gepubliceerd          |
| 10 |Verwerking van antwoord is mislukt       |
| 11 |Antwoord in behandeling         |
| 12 |Inschrijving geslaagd         |
| 13 |Inschrijving niet vereist         |
| 14 |Revoked          |
| 15 |Verwijderd uit verzameling        |
| 16 |Gecontroleerd vernieuwen         |
| 17 |Installatie mislukt        |
| 18 |Geïnstalleerd         |
| 19 |Kan niet verwijderen         |
| 20 |Verwijderen         |
| 21 |Verlenging aangevraagd        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 | De status pincode is ingesteld       |
| 2 | Instellen van status pincode is mislukt       |
| 3 | Het instellen van de status pincode wordt niet ondersteund      |
| 4 | Status pincode instellen wordt uitgevoerd      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

Geen status-Id's.

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

Geen status-Id's.

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

Geen status-Id's.

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

Geen status-Id's.

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

Geen status-Id's.

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

Geen status-Id's.

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Vraag uitgegeven    |
| 2 |Controle probleem mislukt   |
| 3 |Het maken van de aanvraag is mislukt   |
| 4 |Verzenden van aanvraag is mislukt   |
| 5 |Validatie van Challenge geslaagd  |
| 6 |Validatie van controle is mislukt  |
| 7 |Probleem mislukt    |
| 8 |Probleem in behandeling    |
| 9 |Gepubliceerd     |
| 10 |Verwerking van antwoord is mislukt  |
| 11 |Antwoord in behandeling    |
| 12 |Inschrijving geslaagd    |
| 13 |Inschrijving niet vereist    |
| 14 |Revoked     |
| 15 |Verwijderd uit verzameling   |
| 16 |Gecontroleerd vernieuwen    |
| 17 |Installatie mislukt   |
| 18 |Geïnstalleerd    |
| 19 |Kan niet verwijderen    |
| 20 |Verwijderen    |
| 21 |Verlenging aangevraagd   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
|| 1 | Naleving geslaagd    |
| 2 | Compatibiliteit mislukt op MP   |
| 3 | Naleving mislukt op de client   |
| 4 | Compatibiliteit mislukt bij intune   |
| 5 | Naleving mislukt bij AAD   |
| 6 | InTune-compatibiliteits beheer   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Peer-cache bron toegevoegd       |
| 2 |Peer-cache bron verwijderd      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Peer-cache-bron gedeactiveerd       |
| 2 |Bron van peer-cache is actief       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Uploaden van verzamelde gegevens downloaden       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Gegevens voor afwijzing van peer bron uploaden     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

Geen status-Id's.

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

Geen status-Id's.

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

Geen status-Id's.

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

Geen status-Id's.

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     ID van status bericht     |  Beschrijving van status bericht |
|:-------------|:------|
| 1 |Health Attestation wordt ondersteund      |
| 2 |Health Attestation wordt niet ondersteund      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

Geen status-Id's.

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

Geen status-Id's.

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

Geen status-Id's.

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

Geen status-Id's.

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

Geen status-Id's.

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

Geen status-Id's.

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

Geen status-Id's.

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

Geen status-Id's.

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

Geen status-Id's.

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

Geen status-Id's.

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

Geen status-Id's.

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

Geen status-Id's.

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

Geen status-Id's.

## <a name="next-steps"></a>Volgende stappen

- [Beschrijving van status berichten in Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Technisch document voor het beheer van software-updates voor Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)

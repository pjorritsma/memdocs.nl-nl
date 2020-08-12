---
title: Clientgebeurtenislogboeken
titleSuffix: Configuration Manager
description: Technische Naslag informatie voor de mogelijke BitLocker (MBAM)-client vermeldingen in het Windows-gebeurtenis logboek
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d108f56032b1ca3cf4a41a836a7e9096afe41d0d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127964"
---
# <a name="client-event-logs"></a>Clientgebeurtenislogboeken

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3601034-->

Op een Configuration Manager-client waarop u een BitLocker-beheer beleid implementeert, gebruikt u de Windows Logboeken om gebeurtenis logboeken van BitLocker-client weer te geven. Ga naar **Logboeken van toepassingen en services**, **micro soft**, **Windows**, **MBAM** voor zowel de [beheerder](#admin) als de [operationele](#operational) gebeurtenis Logboeken.

## <a name="admin"></a>Beheerder

### <a name="2-volumeenactmentfailed"></a>2: VolumeEnactmentFailed

Er is een fout opgetreden tijdens het Toep assen van MBAM-beleid.

#### <a name="error-code--2144272219"></a>Fout code:-2144272219

Details: de BitLocker-stationsversleuteling ondersteunt alleen gebruik van alleen gebruikte ruimte voor een thin provisioned-opslag.

Deze fout treedt op als u probeert BitLocker te gebruiken om een virtuele machine te versleutelen waarop Windows 10 versie 1803 of eerder wordt uitgevoerd. Eerdere versies van Windows 10 bieden geen ondersteuning voor de versleuteling van de volledige schijf. Met het beleid voor BitLocker-beheer wordt versleuteling van de volledige schijf afgedwongen.

#### <a name="error-code--2147024774"></a>Fout code:-2147024774

Details: het gegevens gebied dat aan een systeem aanroep is door gegeven, is te klein.

U kunt dit probleem oplossen door de computer opnieuw op te starten.

### <a name="4-transferstatusdatafailed"></a>4: TransferStatusDataFailed

Er is een fout opgetreden tijdens het verzenden van de versleutelings status gegevens.

### <a name="8-systemvolumenotfound"></a>8: SystemVolumeNotFound

Het systeem volume ontbreekt. SystemVolume is vereist voor het versleutelen van het station met het besturings systeem.

### <a name="9-tpmnotfound"></a>9: TPMNotFound

De TPM-hardware ontbreekt. TPM is nodig om het besturingssysteem station te versleutelen met een TPM-beveiliging.

### <a name="10-machinehwexempted"></a>10: MachineHWExempted

De computer wordt uitgesloten van versleuteling. Hardware-status van computer: vrijgesteld

### <a name="11-machinehwunknown"></a>11: MachineHWUnknown

De computer wordt uitgesloten van versleuteling. Hardware-status van computer: onbekend

### <a name="12-hwcheckfailed"></a>12: HWCheckFailed

Controle van hardware-uitzonde ring is mislukt.

### <a name="13-userisexempted"></a>13: UserIsExempted

De gebruiker is uitgesloten van versleuteling.

### <a name="14-useriswaiting"></a>14: UserIsWaiting

De gebruiker heeft een uitzonde ring aangevraagd.

### <a name="15-userexemptioncheckfailed"></a>15: UserExemptionCheckFailed

Controle van gebruikers uitzondering is mislukt.

### <a name="16-userpostponed"></a>16: UserPostponed

De gebruiker heeft het versleutelings proces uitgesteld.

### <a name="17-tpminitializationfailed"></a>17: TPMInitializationFailed

De TPM-initialisatie is mislukt. De gebruiker heeft de BIOS-wijzigingen afgewezen.

### <a name="18-coreservicedown"></a>18: CoreServiceDown

Kan geen verbinding maken met de MBAM-herstel-en-hardware-service.

#### <a name="error-code--2147024809"></a>Fout code:-2147024809

Details: de para meter is onjuist.

Deze fout treedt op als de website niet HTTPS is of als de client geen PKI-certificaat heeft.

### <a name="20-policymismatch"></a>20: PolicyMismatch

Het beheer beleid voor BitLocker is strijdig of beschadigd.

### <a name="21-conflictingosvolumepolicies"></a>21: ConflictingOSVolumePolicies

Er is een conflict gedetecteerd voor het versleutelings beleid van het OS Controleer het BitLocker-beleid met betrekking tot beveiligingen van het besturings systeem station.

### <a name="22-conflictingfddvolumepolicies"></a>22: ConflictingFDDVolumePolicies

Er is een conflict gedetecteerd tussen het volume versleutelings beleid van de vaste schijf. Controleer het BitLocker-beleid met betrekking tot beveiligingen van station met vaste gegevens stations.

### <a name="27-encryptionfailednodra"></a>27: EncryptionFailedNoDra

Er is een fout opgetreden tijdens het versleutelen. Er is een Data Recovery agent (DRA) Protector vereist in de FIPS-modus voor pre-Windows 8,1-computers.

### <a name="34-tpmlockoutresetfailed"></a>34: TpmLockOutResetFailed

Kan TPM-vergren deling niet opnieuw instellen.

### <a name="36-tpmownerauthretrievalfailed"></a>36: TpmOwnerAuthRetrievalFailed

Kan TPM-OwnerAuth niet ophalen uit MBAM-Services.

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37: WmiProviderDllSearchPathUpdateFailed

Kan het DLL-zoekpad voor de WMI-provider niet bijwerken.

### <a name="38-timedoutwaitingforwmiprovider"></a>38: TimedOutWaitingForWmiProvider

Agent wordt gestopt. Time-out tijdens het wachten op het exemplaar van de WMI-provider MBAM.

## <a name="operational"></a>Operationeel

### <a name="1-volumeenactmentsuccessful"></a>1: VolumeEnactmentSuccessful

Het beheer beleid voor BitLocker is toegepast.

### <a name="3-transferstatusdatasuccessful"></a>3: TransferStatusDataSuccessful

De versleutelings status gegevens zijn verzonden.

### <a name="19-coreserviceup"></a>19: CoreServiceUp

De verbinding met de MBAM-herstel en de hardware-service is voltooid.

### <a name="28-tpmownerauthescrowed"></a>28: TpmOwnerAuthEscrowed

De TPM-OwnerAuth is geborgd.

### <a name="29-recoverykeyescrowed"></a>29: RecoveryKeyEscrowed

De BitLocker-herstel sleutel voor het volume is borgend.

### <a name="30-recoverykeyreset"></a>30: RecoveryKeyReset

De BitLocker-herstel sleutel voor het volume is bijgewerkt.

### <a name="31-enforcepolicydateset"></a>31: EnforcePolicyDateSet

De datum van het afdwingen van beleid... is ingesteld voor het volume

### <a name="32-enforcepolicydatecleared"></a>32: EnforcePolicyDateCleared

De datum van het afdwingen van beleid... is voor het volume gewist.

### <a name="33-tpmlockoutresetsucceeded"></a>33: TpmLockOutResetSucceeded

TPM-vergren deling is opnieuw ingesteld.

### <a name="35-tpmownerauthretrievalsucceeded"></a>35: TpmOwnerAuthRetrievalSucceeded

TPM-OwnerAuth is opgehaald uit MBAM-Services.

### <a name="39-removabledrivemounted"></a>39: RemovableDriveMounted

Verwisselbaar station is gekoppeld.

### <a name="40-removabledrivedismounted"></a>40: RemovableDriveDismounted

Verwisselbaar station is ontkoppeld.

### <a name="41-failedtoenactendpointunreachable"></a>41: FailedToEnactEndpointUnreachable

Als er geen verbinding kan worden gemaakt met de MBAM-herstel bewerking en de hardware-service, kan het BitLocker-beheer beleid niet worden toegepast op het volume.

### <a name="42-failedtoenactlockedvolume"></a>42: FailedToEnactLockedVolume

Status van vergrendeld volume kan niet worden toegepast op het Toep assen van BitLocker-beheer beleid voor het volume.

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43: TransferStatusDataFailedEndpointUnreachable

Als er geen verbinding kan worden gemaakt met de MBAM-compatibiliteit en de status service, kan de overdracht van de versleutelings status gegevens niet worden overgedragen.

## <a name="see-also"></a>Zie ook

Zie [BitLocker-gebeurtenis logboeken](about-event-logs.md)voor meer informatie over het gebruik van deze logboeken.

Zie [problemen met BitLocker oplossen](troubleshoot.md)voor meer informatie over probleem oplossing.

---
title: Standaard inventaris klassen van resource Explorer
titleSuffix: Configuration Manager
description: Toont de klassen die in resource Explorer worden weer gegeven
ms.date: 11/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d333f4c-0f85-4278-b421-064cf01529a5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 81cf8e1779e072d3eee6a5ed7080b6a63fd07451
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710732"
---
# <a name="resource-explorer-default-inventory-classes"></a>Standaard inventaris klassen van resource Explorer

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel worden de standaard inventaris klassen in resource Explorer beschreven.

Dit zijn de standaard inventaris klassen:

## <a name="1394-controller"></a>1394-controller

Naam ruimte: root\cimv2

klasse Win32_1394Controller


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- UInt32 MaxNumberControlled

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt16 ProtocolSupported

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- DateTime TimeOfLastReset



## <a name="account-sid"></a>Account-SID

Naam ruimte: root\cimv2

klasse Win32_AccountSID

- Tekenreeksexpressie ElementName

- Tekenreeksexpressie Stelt



## <a name="activesync-service"></a>ActiveSync-Service

Naam ruimte: root\SmsDm

klasse SMS_ActiveSyncService


- UInt32 MajorVersion

- UInt32 MinorVersion

- Tekenreeksexpressie LastSyncTime



## <a name="amt-agent"></a>AMT-agent

Naam ruimte: root\cimv2\sms

klasse SMS_AMTObject


- UInt32 DeviceID

- Tekenreeksexpressie AMT

- Tekenreeksexpressie AMTApps

- Tekenreeksexpressie BiosVersion

- Tekenreeksexpressie BuildNumber

- Tekenreeksexpressie Flits

- Tekenreeksexpressie LegacyMode

- Tekenreeksexpressie Netstack

- UInt32 ProvisionMode

- UInt32 ProvisionState

- Tekenreeksexpressie RecoveryBuildNum

- Tekenreeksexpressie RecoveryVersion

- Tekenreeksexpressie SKU

- UInt32 TLSMode

- Tekenreeksexpressie Leverancier

- UInt32 ZTCEnabled



## <a name="appv-client-application"></a>AppV-client toepassing

Naam ruimte: root\AppV

klasse AppvClientApplication


- Tekenreeksexpressie ApplicationId

- Tekenreeksexpressie PackageId

- Tekenreeksexpressie PackageVersionId

- True EnabledForUser

- True EnabledGlobally

- Tekenreeksexpressie Naam

- Tekenreeksexpressie TargetPath

- Tekenreeksexpressie Versie



## <a name="appv-client-package"></a>AppV-client pakket

Naam ruimte: root\AppV

klasse AppvClientPackage


- Tekenreeksexpressie PackageId

- Tekenreeksexpressie VersionId

- Tekenreeksexpressie Assets []

- Tekenreeksexpressie DeploymentMachineData

- Tekenreeksexpressie DeploymentUserData

- True HasAssetIntelligence

- True Een

- True IsPublishedGlobally

- True IsPublishedToUser

- Tekenreeksexpressie Naam

- UInt64 PackageSize

- Tekenreeksexpressie Programmapad

- UInt16 PercentLoaded

- Tekenreeksexpressie UserConfigurationData

- Tekenreeksexpressie Versie



## <a name="autostart-software"></a>Software automatisch starten

Naam ruimte: root\cimv2\sms

klasse SMS_AutoStartSoftware


- Tekenreeksexpressie FilePropertiesHash

- Tekenreeksexpressie BinFileVersion

- Tekenreeksexpressie BinProductVersion

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie Bestands

- Tekenreeksexpressie FilePropertiesHashEx

- Tekenreeksexpressie FileVersion

- Tekenreeksexpressie Locatie

- Tekenreeksexpressie Voortplant

- Tekenreeksexpressie ProductVersion

- Tekenreeksexpressie Uitgever

- Tekenreeksexpressie Opstart type

- Tekenreeksexpressie StartupValue



## <a name="baseboard"></a>Kaart

Naam ruimte: root\cimv2

klasse Win32_BaseBoard


- Tekenreeksexpressie Tag

- Tekenreeksexpressie Kop

- Tekenreeksexpressie ConfigOptions[]

- Tekenreeksexpressie Beschrijvingen

- True HostingBoard

- True HotSwappable

- DateTime InstallDate

- Tekenreeksexpressie Fabricage

- Tekenreeksexpressie Activiteitsmodel

- Tekenreeksexpressie Naam

- Tekenreeksexpressie OtherIdentifyingInfo

- Tekenreeksexpressie PartNumber

- True PoweredOn

- Tekenreeksexpressie Voortplant

- True Verwissel bare

- True Replaceable

- Tekenreeksexpressie RequirementsDescription

- True RequiresDaughterBoard

- Tekenreeksexpressie SerialNumber

- Tekenreeksexpressie SKU

- Tekenreeksexpressie SlotLayout

- True SpecialRequirements

- Tekenreeksexpressie Hebben

- Tekenreeksexpressie Versie



## <a name="battery"></a>Batterij

Naam ruimte: root\cimv2

klasse Win32_Battery


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- UInt16 BatteryStatus

- Tekenreeksexpressie Kop

- UInt16 Chemische

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- UInt32 DesignCapacity

- UInt64 DesignVoltage

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- UInt16 EstimatedChargeRemaining

- UInt32 EstimatedRunTime

- UInt32 ExpectedLife

- UInt32 FullChargeCapacity

- DateTime InstallDate

- UInt32 LastErrorCode

- UInt32 MaxRechargeTime

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie SmartBatteryVersion

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- UInt32 TimeOnBattery

- UInt32 TimeToFullCharge



## <a name="bitlocker"></a>BitLocker

Naam ruimte: root\cimv2\security\MicrosoftVolumeEncryption

klasse Win32_EncryptableVolume


- Tekenreeksexpressie DeviceID

- Tekenreeksexpressie Stationsaanduiding

- Tekenreeksexpressie PersistentVolumeID

- UInt32 ProtectionStatus



## <a name="bitlocker-encryption-details"></a>BitLocker-versleutelings Details

Naam ruimte: root\cimv2

klasse Win32_BitLockerEncryptionDetails


- Tekenreeksexpressie BitlockerPersistentVolumeId

- (SInt32) ACPI

- (SInt32) ConversionStatus

- Tekenreeksexpressie DeviceId

- Tekenreeksexpressie Stationsaanduiding

- (SInt32) EncryptionMethod

- Tekenreeksexpressie EnforcePolicyDate

- True IsAutoUnlockEnabled

- (SInt32) KeyProtectorTypes[]

- Tekenreeksexpressie MbamPersistentVolumeId

- (SInt32) MbamVolumeType

- Tekenreeksexpressie NoncomplianceDetectedDate

- (SInt32) ProtectionStatus

- (SInt32) ReasonsForNonCompliance[]



## <a name="bitlocker-policy"></a>BitLocker-beleid

Naam ruimte: root\cimv2

klasse Win32Reg_MBAMPolicy


- Tekenreeksexpressie EncodedComputerName

- UInt32 EncryptionMethod

- UInt32 FixedDataDriveAutoUnlock

- UInt32 FixedDataDriveEncryption

- UInt32 FixedDataDrivePassphrase

- Tekenreeksexpressie KeyName

- Tekenreeksexpressie LastConsoleUser

- UInt32 MBAMMachineError

- UInt32 MBAMPolicyEnforced

- UInt32 OsDriveEncryption

- UInt32 OsDriveProtector

- DateTime UserExemptionDate



## <a name="boot-configuration"></a>Opstart configuratie

Naam ruimte: root\cimv2

klasse Win32_BootConfiguration


- Tekenreeksexpressie Naam

- Tekenreeksexpressie BootDirectory

- Tekenreeksexpressie ConfigurationPath

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie Last

- Tekenreeksexpressie ScratchDirectory

- Tekenreeksexpressie SettingID

- Tekenreeksexpressie TempDirectory



## <a name="browser-helper-object"></a>Browser helper-object

Naam ruimte: root\cimv2\sms

klasse SMS_BrowserHelperObject


- Tekenreeksexpressie FilePropertiesHash

- Tekenreeksexpressie BinFileVersion

- Tekenreeksexpressie BinProductVersion

- Tekenreeksexpressie GEACTIVEERD

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie Bestands

- Tekenreeksexpressie FilePropertiesHashEx

- Tekenreeksexpressie FileVersion

- Tekenreeksexpressie Voortplant

- Tekenreeksexpressie ProductVersion

- Tekenreeksexpressie Uitgever

- Tekenreeksexpressie Versie



## <a name="ccm_rax"></a>CCM_RAX

Naam ruimte: root\ccm\cimodels

klasse CCM_RAXInfo


- Tekenreeksexpressie AppID

- Tekenreeksexpressie FeedURL

- Tekenreeksexpressie UserSID



## <a name="cd-rom"></a>CD-ROM

Naam ruimte: root\cimv2

klasse Win32_CDROMDrive


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- UInt16 Mogelijkheden []

- Tekenreeksexpressie CapabilityDescriptions[]

- Tekenreeksexpressie Kop

- Tekenreeksexpressie CompressionMethod

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- UInt64 DefaultBlockSize

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie Stationsletter

- True DriveIntegrity

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- Tekenreeksexpressie ErrorMethodology

- UInt16 FileSystemFlags

- UInt32 FileSystemFlagsEx

- Tekenreeksexpressie ID

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- UInt64 MaxBlockSize

- UInt32 MaximumComponentLength

- UInt64 MaxMediaSize

- True MediaLoaded

- Tekenreeksexpressie Type

- UInt64 MinBlockSize

- Tekenreeksexpressie Naam

- True NeedsCleaning

- UInt32 NumberOfMediaSupported

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie RevisionLevel

- UInt32 SCSIBus

- UInt16 SCSILogicalUnit

- UInt16 SCSIPort

- UInt16 SCSITargetId

- UInt64 Size

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- Tekenreeksexpressie VolumeName

- Tekenreeksexpressie VolumeSerialNumber



## <a name="client-events"></a>Client gebeurtenissen

Naam ruimte: root\ccm\invagt

klasse ClientEvents


- Tekenreeksexpressie EventName

- UInt16 Aantal



## <a name="computer-system"></a>Computersysteem

Naam ruimte: root\cimv2

klasse Win32_ComputerSystem


- Tekenreeksexpressie Naam

- UInt16 AdminPasswordStatus

- True AutomaticResetBootOption

- True AutomaticResetCapability

- UInt16 BootOptionOnLimit

- UInt16 BootOptionOnWatchDog

- True BootROMSupported

- Tekenreeksexpressie BootupState

- Tekenreeksexpressie Kop

- UInt16 ChassisBootupState

- (SInt16) CurrentTimeZone

- True DaylightInEffect

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie Domeinen

- UInt16 DomainRole

- UInt16 FrontPanelResetStatus

- True InfraredSupported

- Tekenreeksexpressie InitialLoadInfo[]

- DateTime InstallDate

- UInt16 KeyboardPasswordStatus

- Tekenreeksexpressie LastLoadInfo

- Tekenreeksexpressie Fabricage

- Tekenreeksexpressie Activiteitsmodel

- Tekenreeksexpressie NameFormat

- True NetworkServerModeEnabled

- UInt32 NumberOfProcessors

- Tekenreeksexpressie OEMLogoBitmap

- Tekenreeksexpressie OEMStringArray[]

- (SInt64) PauseAfterReset

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt16 PowerOnPasswordStatus

- UInt16 PowerState

- UInt16 PowerSupplyState

- Tekenreeksexpressie PrimaryOwnerContact

- Tekenreeksexpressie PrimaryOwnerName

- UInt16 ResetCapability

- (SInt16) ResetCount

- (SInt16) ResetLimit

- Tekenreeksexpressie Rollen []

- Tekenreeksexpressie Hebben

- Tekenreeksexpressie SupportContactDescription[]

- UInt16 SystemStartupDelay

- Tekenreeksexpressie SystemStartupOptions[]

- (UInt8) SystemStartupSetting

- Tekenreeksexpressie System type

- UInt16 ThermalState

- UInt64 TotalPhysicalMemory

- Tekenreeksexpressie Gebruikers

- UInt16 WakeUpType



## <a name="computer-system-ex"></a>Computer systeem ex

Naam ruimte: root\cimv2

klasse CCM_ComputerSystemExtended


- Tekenreeksexpressie Naam

- UInt16 PCSystemType



## <a name="computer-system-product"></a>Computer systeem product

Naam ruimte: root\cimv2

klasse Win32_ComputerSystemProduct


- Tekenreeksexpressie Nummer

- Tekenreeksexpressie Naam

- Tekenreeksexpressie Versie

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie SKUNumber

- Tekenreeksexpressie MEE

- Tekenreeksexpressie Leverancierspecifieke



## <a name="sms-advanced-client-ports"></a>SMS-Advanced Client poorten

Naam ruimte: root\cimv2

klasse Win32Reg_SMSAdvancedClientPorts


- Tekenreeksexpressie InstanceKey

- UInt32 HttpsPortName

- UInt32 Poortnaam



## <a name="sms-advanced-client-ssl-configurations"></a>SMS-Advanced Client SSL-configuraties

Naam ruimte: root\cimv2

klasse Win32Reg_SMSAdvancedClientSSLConfiguration


- Tekenreeksexpressie InstanceKey

- Tekenreeksexpressie CertificateSelectionCriteria

- Tekenreeksexpressie CertificateStore

- UInt32 ClientAlwaysOnInternet

- UInt32 HttpsStateFlags

- Tekenreeksexpressie InternetMPHostName

- UInt32 SelectFirstCertificate



## <a name="sms-advanced-client-state"></a>SMS-Advanced Client status

Naam ruimte: root\ccm

klasse CCM_InstalledComponent


- Tekenreeksexpressie Naam

- Tekenreeksexpressie DisplayName

- Tekenreeksexpressie Versie



## <a name="connected-device"></a>Verbonden apparaat

Naam ruimte: root\SmsDm

klasse SMS_ActiveSyncConnectedDevice


- Tekenreeksexpressie DeviceOEMInfo

- Tekenreeksexpressie DeviceType

- Tekenreeksexpressie OS_Major

- Tekenreeksexpressie OS_Minor

- Tekenreeksexpressie OS_Platform

- Tekenreeksexpressie ProcessorArchitecture

- Tekenreeksexpressie ProcessorLevel

- Tekenreeksexpressie ProcessorRevision

- Tekenreeksexpressie InstalledClientID

- Tekenreeksexpressie InstalledClientServer

- Tekenreeksexpressie InstalledClientVersion

- Tekenreeksexpressie LastSyncTime

- Tekenreeksexpressie OS_AdditionalInfo

- Tekenreeksexpressie OS_Build



## <a name="sms_defaultbrowser"></a>SMS_DefaultBrowser

Naam ruimte: root\cimv2\sms

klasse SMS_DefaultBrowser


- Tekenreeksexpressie BrowserProgId



## <a name="desktop"></a>Desktop

Naam ruimte: root\cimv2

klasse Win32_Desktop


- Tekenreeksexpressie Naam

- UInt32 Breedte

- Tekenreeksexpressie Kop

- True CoolSwitch

- UInt32 CursorBlinkRate

- Tekenreeksexpressie Beschrijvingen

- True DragFullWindows

- UInt32 GridGranularity

- UInt32 IconSpacing

- Tekenreeksexpressie IconTitleFaceName

- UInt32 IconTitleSize

- True IconTitleWrap

- Tekenreeksexpressie Pattern

- True ScreenSaverActive

- Tekenreeksexpressie ScreenSaverExecutable

- True ScreenSaverSecure

- UInt32 ScreenSaverTimeout

- Tekenreeksexpressie SettingID

- Tekenreeksexpressie Bitmapindeling

- True WallpaperStretched

- True WallpaperTiled



## <a name="desktop-monitor"></a>Bureaublad monitor

Naam ruimte: root\cimv2

klasse Win32_DesktopMonitor


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- UInt32 BAP

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- UInt16 Weergave

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- True IsLocked

- UInt32 LastErrorCode

- Tekenreeksexpressie MonitorManufacturer

- Tekenreeksexpressie Monitor

- Tekenreeksexpressie Naam

- UInt32 PixelsPerXLogicalInch

- UInt32 PixelsPerYLogicalInch

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt32 ScreenHeight

- UInt32 ScreenWidth

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam



## <a name="device-info"></a>Apparaatgegevens

Naam ruimte: gereserveerd

klasse Device_Info


- Tekenreeksexpressie Verval datum certificaat

- Tekenreeksexpressie DeviceName

- Tekenreeksexpressie Fabricage

- Tekenreeksexpressie Activiteitsmodel

- Tekenreeksexpressie VERMELDING



## <a name="mdm-devdetail"></a>MDM-DevDetail

Naam ruimte: root\cimv2\mdm\dmmap

klasse MDM_DevDetail_Ext01


- Tekenreeksexpressie InstanceID

- Tekenreeksexpressie ParentID

- Tekenreeksexpressie DeviceHardwareData

- Tekenreeksexpressie WLANMACAddress



## <a name="disk"></a>Schijf

Naam ruimte: root\cimv2

klasse Win32_DiskDrive


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- UInt32 BytesPerSector

- UInt16 Mogelijkheden []

- Tekenreeksexpressie CapabilityDescriptions[]

- Tekenreeksexpressie Kop

- Tekenreeksexpressie CompressionMethod

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- UInt64 DefaultBlockSize

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- Tekenreeksexpressie ErrorMethodology

- UInt32 TabIndex

- DateTime InstallDate

- Tekenreeksexpressie Interface type

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- UInt64 MaxBlockSize

- UInt64 MaxMediaSize

- True MediaLoaded

- Tekenreeksexpressie Type

- UInt64 MinBlockSize

- Tekenreeksexpressie Activiteitsmodel

- Tekenreeksexpressie Naam

- True NeedsCleaning

- UInt32 NumberOfMediaSupported

- UInt32 Partition

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt32 SCSIBus

- UInt16 SCSILogicalUnit

- UInt16 SCSIPort

- UInt16 SCSITargetId

- UInt32 SectorsPerTrack

- UInt64 Size

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- UInt64 TotalCylinders

- UInt32 TotalHeads

- UInt64 TotalSectors

- UInt64 TotalTracks

- UInt32 TracksPerCylinder



## <a name="partition"></a>Partitie

Naam ruimte: root\cimv2

klasse Win32_DiskPartition


- Tekenreeksexpressie DeviceID

- UInt16 Access

- UInt16 Availability

- UInt64 Blok

- True Opgestart

- True BootPartition

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- UInt32 DiskIndex

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- Tekenreeksexpressie ErrorMethodology

- UInt32 HiddenSectors

- UInt32 TabIndex

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Naam

- UInt64 NumberOfBlocks

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- True Primaire partitie

- Tekenreeksexpressie Doel

- True RewritePartition

- UInt64 Size

- UInt64 StartingOffset

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- Tekenreeksexpressie Voert



## <a name="dma"></a>DMA

Naam ruimte: root\cimv2

klasse Win32_DeviceMemoryAddress

- UInt64 StartingAddress

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- UInt64 EndingAddress

- DateTime InstallDate

- Tekenreeksexpressie MemoryType

- Tekenreeksexpressie Naam

- Tekenreeksexpressie Hebben



## <a name="dma-channel"></a>DMA-kanaal

Naam ruimte: root\cimv2

klasse Win32_DMAChannel


- UInt32 DMAChannel

- UInt16 AddressSize

- UInt16 Availability

- True BurstMode

- UInt16 ByteMode

- Tekenreeksexpressie Kop

- UInt16 ChannelTiming

- Tekenreeksexpressie Beschrijvingen

- DateTime InstallDate

- UInt32 MaxTransferSize

- Tekenreeksexpressie Naam

- UInt32 Importeer

- Tekenreeksexpressie Hebben

- UInt16 TransferWidths[]

- UInt16 TypeCTiming

- UInt16 WordMode



## <a name="driver---vxd"></a>Stuur programma-VxD

Naam ruimte: root\cimv2

klasse Win32_DriverVXD


- Tekenreeksexpressie Naam

- Tekenreeksexpressie SoftwareElementID

- UInt16 SoftwareElementState

- UInt16 TargetOperatingSystem

- Tekenreeksexpressie Versie

- Tekenreeksexpressie BuildNumber

- Tekenreeksexpressie Kop

- Tekenreeksexpressie CodeSet

- Tekenreeksexpressie Over

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie DeviceDescriptorBlock

- Tekenreeksexpressie IdentificationCode

- DateTime InstallDate

- Tekenreeksexpressie LanguageEdition

- Tekenreeksexpressie Fabricage

- Tekenreeksexpressie OtherTargetOS

- Tekenreeksexpressie PM_API

- Tekenreeksexpressie SerialNumber

- UInt32 ServiceTableSize

- Tekenreeksexpressie Hebben

- Tekenreeksexpressie V86_API



## <a name="embedded-device-information"></a>Informatie over Inge sloten apparaat

Naam ruimte: root\cimv2\sms

klasse CCM_EmbeddedDeviceInformation


- Tekenreeksexpressie DeviceType

- Tekenreeksexpressie Activiteitsmodel

- Tekenreeksexpressie OEMName



## <a name="environment"></a>Omgeving

Naam ruimte: root\cimv2

klasse Win32_Environment


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Gebruikers

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- DateTime InstallDate

- Tekenreeksexpressie Hebben

- True SystemVariable

- Tekenreeksexpressie VariableValue



## <a name="firmware"></a>Firmware

Naam ruimte: root\cimv2\sms

klasse SMS_Firmware


- True UEFI

- True SecureBoot



## <a name="usm-folder-redirection-health"></a>Status van Mapomleiding van eigenschappen van

Naam ruimte: root\cimv2\sms

klasse SMS_FolderRedirectionHealth


- Tekenreeksexpressie Mapnaam

- Tekenreeksexpressie GEVAL

- (UInt8) HealthStatus

- DateTime LastSuccessfulSyncTime

- (UInt8) LastSyncStatus

- DateTime LastSyncTime

- True OfflineAccessEnabled

- Tekenreeksexpressie OfflineFileNameFolderGUID

- True Omgeleid



## <a name="ide-controller"></a>IDE-controller

Naam ruimte: root\cimv2

klasse Win32_IDEController


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- UInt32 MaxNumberControlled

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt16 ProtocolSupported

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- DateTime TimeOfLastReset



## <a name="add-remove-programs-64"></a>Software toevoegen (64)

Naam ruimte: root\cimv2

klasse Win32Reg_AddRemovePrograms64


- Tekenreeksexpressie ProdID

- Tekenreeksexpressie DisplayName

- Tekenreeksexpressie InstallDate

- Tekenreeksexpressie Uitgever

- Tekenreeksexpressie Versie



## <a name="add-remove-programs"></a>Software toevoegen

Naam ruimte: root\cimv2

klasse Win32Reg_AddRemovePrograms


- Tekenreeksexpressie ProdID

- Tekenreeksexpressie DisplayName

- Tekenreeksexpressie InstallDate

- Tekenreeksexpressie Uitgever

- Tekenreeksexpressie Versie



## <a name="installed-executable"></a>Geïnstalleerd uitvoerbaar bestand

Naam ruimte: root\cimv2\sms

klasse SMS_InstalledExecutable


- Tekenreeksexpressie Uitvoer bare bestand

- Tekenreeksexpressie Code

- Tekenreeksexpressie BinFileVersion

- Tekenreeksexpressie BinProductVersion

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie FilePropertiesHash

- Tekenreeksexpressie FilePropertiesHashEx

- UInt32 FileSize

- Tekenreeksexpressie FileVersion

- True HasPatchAdded

- Tekenreeksexpressie InstalledFilePath

- True IsSystemFile

- True IsVitalFile

- UInt32 Japanse

- Tekenreeksexpressie Voortplant

- Tekenreeksexpressie ProductVersion

- Tekenreeksexpressie Uitgever



## <a name="installed-software"></a>Geïnstalleerde software

Naam ruimte: root\cimv2\sms

klasse SMS_InstalledSoftware


- Tekenreeksexpressie SoftwareCode

- Tekenreeksexpressie ARPDisplayName

- Tekenreeksexpressie ChannelCode

- Tekenreeksexpressie ChannelID

- Tekenreeksexpressie CM_DSLID

- Tekenreeksexpressie EvidenceSource

- DateTime InstallDate

- UInt32 InstallDirectoryValidation

- Tekenreeksexpressie InstalledLocation

- Tekenreeksexpressie InstallSource

- UInt32 InstallType

- UInt32 Japanse

- Tekenreeksexpressie LocalPackage

- Tekenreeksexpressie MPC

- UInt32 OsComponent

- Tekenreeksexpressie PackageCode

- Tekenreeksexpressie ProductID

- Tekenreeksexpressie Product

- Tekenreeksexpressie ProductVersion

- Tekenreeksexpressie Uitgever

- Tekenreeksexpressie RegisteredUser

- Tekenreeksexpressie ServicePack

- Tekenreeksexpressie SoftwarePropertiesHash

- Tekenreeksexpressie SoftwarePropertiesHashEx

- Tekenreeksexpressie UninstallString

- Tekenreeksexpressie UpgradeCode

- UInt32 VersionMajor

- UInt32 VersionMinor



## <a name="irq-table"></a>IRQ-tabel

Naam ruimte: root\cimv2

klasse Win32_IRQResource


- UInt32 IRQNumber

- UInt16 Availability

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- True Hardwaresleutel

- DateTime InstallDate

- Tekenreeksexpressie Naam

- True Deelbaar

- Tekenreeksexpressie Hebben

- UInt16 TriggerLevel

- UInt16 Trigger type

- UInt32 Via



## <a name="keyboard"></a>Toetsenbord

Naam ruimte: root\cimv2

klasse Win32_Keyboard


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- True IsLocked

- UInt32 LastErrorCode

- Tekenreeksexpressie Opmaak

- Tekenreeksexpressie Naam

- UInt16 NumberOfFunctionKeys

- UInt16 Wacht woord

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam



## <a name="load-order-group"></a>Volgorde groep laden

Naam ruimte: root\cimv2

klasse Win32_LoadOrderGroup


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- True DriverEnabled

- UInt32 GroupOrder

- DateTime InstallDate

- Tekenreeksexpressie Hebben



## <a name="logical-disk"></a>Logische schijf

Naam ruimte: root\cimv2\sms

klasse SMS_LogicalDisk


- Tekenreeksexpressie DeviceID

- UInt16 Access

- UInt16 Availability

- UInt64 Blok

- Tekenreeksexpressie Kop

- True Eerst

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- UInt32 DriveType

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- Tekenreeksexpressie ErrorMethodology

- Tekenreeksexpressie System

- UInt64 Frees Pace

- DateTime InstallDate

- UInt32 LastErrorCode

- UInt32 MaximumComponentLength

- UInt32 Type

- Tekenreeksexpressie Naam

- UInt64 NumberOfBlocks

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie ProviderName

- Tekenreeksexpressie Doel

- UInt64 Size

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- True SupportsFileBasedCompression

- Tekenreeksexpressie Systemnaam

- Tekenreeksexpressie VolumeName

- Tekenreeksexpressie VolumeSerialNumber



## <a name="memory"></a>Geheugen

Naam ruimte: root\cimv2

klasse CCM_LogicalMemoryConfiguration


- Tekenreeksexpressie Naam

- UInt64 AvailableVirtualMemory

- UInt64 TotalPageFileSpace

- UInt64 TotalPhysicalMemory

- UInt64 TotalVirtualMemory



## <a name="device-bluetooth"></a>Bluetooth van apparaat

Naam ruimte: gereserveerd

klasse Device_Bluetooth


- True Ingeschakeld



## <a name="device-camera"></a>Camera van apparaat

Naam ruimte: gereserveerd

klasse Device_Camera


- True Ingeschakeld



## <a name="device-certificates"></a>Certificaten van apparaten

Naam ruimte: gereserveerd

klasse Device_Certificates


- Tekenreeksexpressie Vingerafdruk

- Tekenreeksexpressie Voert

- Tekenreeksexpressie IssuedBy

- Tekenreeksexpressie IssuedTo

- DateTime ValidFrom

- DateTime ValidTo



## <a name="device-client"></a>Apparaatclient

Naam ruimte: gereserveerd

klasse Device_Client


- True DownloadWhenRoaming

- True SyncWhenRoaming



## <a name="device-client-agent-version"></a>Versie van client agent voor apparaat

Naam ruimte: gereserveerd

klasse Device_ClientAgentVersion


- Tekenreeksexpressie Versie



## <a name="device-computer-system"></a>Computer systeem van apparaat

Naam ruimte: gereserveerd

klasse Device_ComputerSystem


- Tekenreeksexpressie CellularTechnology

- Tekenreeksexpressie DeviceClientID

- Tekenreeksexpressie DeviceManufacturer

- Tekenreeksexpressie DeviceModel

- Tekenreeksexpressie DMVersion

- Tekenreeksexpressie FirmwareVersion

- Tekenreeksexpressie HardwareVersion

- Tekenreeksexpressie IMEI

- Tekenreeksexpressie IMSI

- (UInt8) IsActivationLockEnabled

- (UInt8) Opengebroken

- Tekenreeksexpressie MEID

- Tekenreeksexpressie LEVERANCIER

- Tekenreeksexpressie PhoneNumber

- Tekenreeksexpressie Type

- UInt32 ProcessorArchitecture

- UInt32 ProcessorLevel

- UInt32 ProcessorRevision

- Tekenreeksexpressie Voortplant

- Tekenreeksexpressie ProductVersion

- Tekenreeksexpressie SerialNumber

- Tekenreeksexpressie SoftwareVersion

- Tekenreeksexpressie SubscriberCarrierNetwork



## <a name="device-display"></a>Apparaat weer geven

Naam ruimte: gereserveerd

klasse Device_Display


- UInt32 HorizontalResolution

- UInt64 NumberOfColors

- UInt32 VerticalResolution



## <a name="device-email"></a>E-mail van apparaat

Naam ruimte: gereserveerd

klasse Device_Email


- Tekenreeksexpressie OwnerEmailAddress

- Tekenreeksexpressie SyncDomain

- Tekenreeksexpressie SyncServer

- Tekenreeksexpressie SyncUser

- Tekenreeksexpressie Voert



## <a name="device-encryption"></a>Apparaatversleuteling

Naam ruimte: gereserveerd

klasse Device_Encryption


- UInt32 EmailEncryptionAlgorithm

- UInt32 EmailEncryptionNegotiation

- True EmailEncryptionRequired

- True EmailSigningAlgorithm

- True EmailSigningRequired

- True EncryptionCompliance

- True PhoneMemoryEncrypted

- True StorageCardEncrypted



## <a name="device-exchange"></a>Apparaat uitwisselen

Naam ruimte: gereserveerd

klasse Device_Exchange


- True ConflictResolution

- (SInt32) HTMLEmailTruncation

- UInt32 MailFormat

- UInt32 MaxCalendarAge

- UInt32 MaxEmailAge

- (SInt32) MaxMailFileAttachmentSize

- UInt32 OffPeakSyncFrequency

- UInt32 PeakDays

- Tekenreeksexpressie PeakEndTime

- Tekenreeksexpressie PeakStartTime

- UInt32 PeakSyncFrequency

- (SInt32) PlainTextEmailTruncation

- True SendEmailImmediately

- True SyncCalendar

- True SyncContacts

- True SyncEmail

- True SyncTasks

- True SyncWhenRoaming



## <a name="device-installed-applications"></a>Geïnstalleerde toepassingen

Naam ruimte: gereserveerd

klasse Device_InstalledApplications


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Versie



## <a name="device-irda"></a>Device IrDA

Naam ruimte: gereserveerd

klasse Device_IrDA


- True Ingeschakeld



## <a name="mobile-device-location"></a>Locatie van mobiel apparaat

Naam ruimte: gereserveerd

klasse MDM_RemoteFind


- (Real32) Breedte graad

- (Real32) Lengte graad



## <a name="device-memory"></a>Geheugen van apparaat

Naam ruimte: gereserveerd

klasse Device_Memory


- UInt64 ProgramFree

- UInt64 ProgramTotal

- UInt64 RemovableStorageFree

- UInt64 RemovableStorageTotal

- UInt64 StorageFree

- UInt64 StorageTotal



## <a name="device-os-information"></a>BESTURINGSSYSTEEM gegevens van het apparaat

Naam ruimte: gereserveerd

klasse Device_OSInformation


- Tekenreeksexpressie Japanse

- Tekenreeksexpressie Onafhankelijk

- Tekenreeksexpressie Versie



## <a name="device-password"></a>Apparaatwachtwoord

Naam ruimte: gereserveerd

klasse Device_Password


- True AllowRecoveryPassword

- UInt32 AutolockTimeout

- True Ingeschakeld

- UInt32 Verval

- UInt32 Transactie

- UInt32 MaxAttemptsBeforeWipe

- UInt32 MinComplexChars

- UInt32 MinLength

- (UInt8) PasswordQuality

- UInt32 Voert



## <a name="device-policy"></a>Apparaatbeleid

Naam ruimte: gereserveerd

klasse Device_Policy


- Tekenreeksexpressie Naam

- True Afgedwongen



## <a name="device-power"></a>Apparaat inschakelen

Naam ruimte: gereserveerd

klasse Device_Power


- UInt32 BacklightACTimeout

- UInt32 BacklightBatTimeout

- (SInt32) BackupPercent

- (SInt32) BatteryPercent



## <a name="mobile-device-security-status"></a>Beveiligings status van mobiel apparaat

Naam ruimte: gereserveerd

klasse MDM_SecurityStatus


- UInt32 HardwareEncryptionCaps

- (UInt8) PasscodeCompliant

- (UInt8) PasscodeCompliantWithProfiles

- (UInt8) PasscodePresent

- (UInt8) RequireEncryption



## <a name="device-windows-security-policy"></a>Windows-beveiligings beleid voor apparaat

Naam ruimte: gereserveerd

klasse Device_WindowsSecurityPolicy


- UInt32 ID

- Tekenreeksexpressie Naam

- UInt32 Value



## <a name="device-wlan"></a>Apparaat-WLAN

Naam ruimte: gereserveerd

klasse Device_WLAN


- True Ingeschakeld

- Tekenreeksexpressie EthernetMAC

- Tekenreeksexpressie WiFiMAC



## <a name="modem"></a>Nulmodem

Naam ruimte: root\cimv2

klasse Win32_POTSModem


- Tekenreeksexpressie DeviceID

- UInt16 AnswerMode

- Tekenreeksexpressie AttachedTo

- UInt16 Availability

- Tekenreeksexpressie BlindOff

- Tekenreeksexpressie BlindOn

- Tekenreeksexpressie Kop

- Tekenreeksexpressie CompatibilityFlags

- UInt16 CompressionInfo

- Tekenreeksexpressie CompressionOff

- Tekenreeksexpressie CompressionOn

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie ConfigurationDialog

- Tekenreeksexpressie CountriesSupported[]

- Tekenreeksexpressie CountrySelected

- Tekenreeksexpressie CurrentPasswords[]

- Tekenreeksexpressie DCB

- Tekenreeksexpressie Prijs

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie DeviceLoader

- Tekenreeksexpressie DeviceType

- UInt16 DialType

- DateTime DriverDate

- True ErrorCleared

- Tekenreeksexpressie ErrorControlForced

- UInt16 ErrorControlInfo

- Tekenreeksexpressie ErrorControlOff

- Tekenreeksexpressie ErrorControlOn

- Tekenreeksexpressie ErrorDescription

- Tekenreeksexpressie FlowControlHard

- Tekenreeksexpressie FlowControlOff

- Tekenreeksexpressie FlowControlSoft

- Tekenreeksexpressie InactivityScale

- UInt32 InactivityTimeout

- UInt32 TabIndex

- DateTime InstallDate

- UInt32 LastErrorCode

- UInt32 MaxBaudRateToPhone

- UInt32 MaxBaudRateToSerialPort

- UInt16 MaxNumberOfPasswords

- Tekenreeksexpressie Activiteitsmodel

- Tekenreeksexpressie ModemInfPath

- Tekenreeksexpressie ModemInfSection

- Tekenreeksexpressie ModulationBell

- Tekenreeksexpressie ModulationCCITT

- UInt16 ModulationScheme

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- Tekenreeksexpressie PortSubClass

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie Beleids

- Tekenreeksexpressie Eigenschappen

- Tekenreeksexpressie ProviderName

- Tekenreeksexpressie Pulse

- Tekenreeksexpressie Wijzigen

- Tekenreeksexpressie ResponsesKeyName

- (UInt8) RingsBeforeAnswer

- Tekenreeksexpressie SpeakerModeDial

- Tekenreeksexpressie SpeakerModeOff

- Tekenreeksexpressie SpeakerModeOn

- Tekenreeksexpressie SpeakerModeSetup

- Tekenreeksexpressie SpeakerVolumeHigh

- UInt16 SpeakerVolumeInfo

- Tekenreeksexpressie SpeakerVolumeLow

- Tekenreeksexpressie SpeakerVolumeMed

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie StringFormat

- True SupportsCallback

- True SupportsSynchronousConnect

- Tekenreeksexpressie Systemnaam

- Tekenreeksexpressie Eind teken

- DateTime TimeOfLastReset

- Tekenreeksexpressie Geluid

- Tekenreeksexpressie VoiceSwitchFeature



## <a name="motherboard"></a>Beschikt

Naam ruimte: root\cimv2

klasse Win32_MotherboardDevice


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie PrimaryBusType

- Tekenreeksexpressie RevisionNumber

- Tekenreeksexpressie SecondaryBusType

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam


## <a name="nap-client"></a>NAP-client

Naam ruimte: root\Nap

klasse NAP_Client


- Naam (teken reeks)

- (Teken reeks) beschrijving

- (Teken reeks) fixupURL

- (Booleaans) napEnabled

- (Teken reeks) napProtocolVersion

- (Teken reeks) probationTime

- (UInt32) systemIsolationState



## <a name="nap-system-health-agent"></a>NAP-systeem status agent

Naam ruimte: root\Nap

klasse NAP_SystemHealthAgent


- UInt32 ID

- (Teken reeks) beschrijving

- (UInt32) fixupState

- (Teken reeks) FriendlyName

- (Teken reeks) infoClsid

- (Booleaans) isBound

- (UInt8) percentage

- (Teken reeks) registrationDate

- (Teken reeks) leveranciers naam

- (Teken reeks) versie



## <a name="network-adapter"></a>Netwerk adapter

Naam ruimte: root\cimv2

klasse Win32_NetworkAdapter


- Tekenreeksexpressie DeviceID

- Tekenreeksexpressie AdapterType

- True AutoSense

- UInt16 Availability

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- UInt32 TabIndex

- DateTime InstallDate

- True Nstalleerd

- UInt32 LastErrorCode

- Tekenreeksexpressie MACAddress

- Tekenreeksexpressie Fabricage

- UInt32 MaxNumberControlled

- UInt64 MaxSpeed

- Tekenreeksexpressie Naam

- Tekenreeksexpressie NetworkAddresses []

- Tekenreeksexpressie PermanentAddress

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie Product

- Tekenreeksexpressie ServiceName

- UInt64 Waarmee

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- DateTime TimeOfLastReset



## <a name="network-adapter-configuration"></a>Configuratie van netwerk adapter

Naam ruimte: root\cimv2

klasse Win32_NetworkAdapterConfiguration


- UInt32 TabIndex

- True ArpAlwaysSourceRoute

- True ArpUseEtherSNAP

- Tekenreeksexpressie Kop

- Tekenreeksexpressie DatabasePath

- True DeadGWDetectEnabled

- Tekenreeksexpressie DefaultIPGateway[]

- (UInt8) DefaultTOS

- (UInt8) DefaultTTL

- Tekenreeksexpressie Beschrijvingen

- True DHCPEnabled

- DateTime DHCPLeaseExpires

- DateTime DHCPLeaseObtained

- Tekenreeksexpressie DHCP

- Tekenreeksexpressie DNSDomain

- Tekenreeksexpressie DNSDomainSuffixSearchOrder[]

- True DNSEnabledForWINSResolution

- Tekenreeksexpressie DNSHostName

- Tekenreeksexpressie DNSServerSearchOrder[]

- True DomainDNSRegistrationEnabled

- UInt32 Forward

- True FullDNSRegistrationEnabled

- UInt16 GatewayCostMetric[]

- (UInt8) IGMPLevel

- Tekenreeksexpressie IP-adres []

- UInt32 IPConnectionMetric

- True IPEnabled

- True IPFilterSecurityEnabled

- True IPPortSecurityEnabled

- Tekenreeksexpressie IPSecPermitIPProtocols[]

- Tekenreeksexpressie IPSecPermitTCPPorts[]

- Tekenreeksexpressie IPSecPermitUDPPorts[]

- Tekenreeksexpressie IPSubnet []

- True IPUseZeroBroadcast

- Tekenreeksexpressie IPXAddress

- True IPXEnabled

- Tekenreeksexpressie IPXFrameType

- UInt32 IPXMediaType

- Tekenreeksexpressie IPXNetworkNumber[]

- Tekenreeksexpressie IPXVirtualNetNumber

- UInt32 KeepAliveInterval

- UInt32 KeepAliveTime

- Tekenreeksexpressie MACAddress

- UInt32 MTU

- UInt32 NumForwardPackets

- True PMTUBHDetectEnabled

- True PMTUDiscoveryEnabled

- Tekenreeksexpressie ServiceName

- Tekenreeksexpressie SettingID

- UInt32 TcpipNetbiosOptions

- UInt32 TcpMaxConnectRetransmissions

- UInt32 TcpMaxDataRetransmissions

- UInt32 TcpNumConnections

- True TcpUseRFC1122UrgentPointer

- UInt16 TcpWindowSize

- True WINSEnableLMHostsLookup

- Tekenreeksexpressie WINSHostLookupFile

- Tekenreeksexpressie WINSPrimaryServer

- Tekenreeksexpressie WINSScopeID

- Tekenreeksexpressie WINSSecondaryServer



## <a name="network-client"></a>Netwerkclient

Naam ruimte: root\cimv2

klasse Win32_NetworkClient


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- DateTime InstallDate

- Tekenreeksexpressie Fabricage

- Tekenreeksexpressie Hebben



## <a name="network-login-profile"></a>Aanmeldings profiel voor netwerk

Naam ruimte: root\cimv2

klasse Win32_NetworkLoginProfile


- Tekenreeksexpressie Naam

- DateTime AccountExpires

- UInt32 AuthorizationFlags

- UInt32 BadPasswordCount

- Tekenreeksexpressie Kop

- UInt32 Tabel

- Tekenreeksexpressie Heffen

- UInt32 CountryCode

- Tekenreeksexpressie Beschrijvingen

- UInt32 Markering

- Tekenreeksexpressie Juiste

- Tekenreeksexpressie HomeDirectory

- Tekenreeksexpressie HomeDirectoryDrive

- DateTime LastLogoff

- DateTime LastLogon

- Tekenreeksexpressie LogonHours

- Tekenreeksexpressie LogonServer

- UInt64 MaximumStorage

- UInt32 NumberOfLogons

- Tekenreeksexpressie Instellen

- DateTime Wacht woord

- DateTime PasswordExpires

- UInt32 PrimaryGroupId

- UInt32 Bevoegdheden

- Tekenreeksexpressie Uplinkpoortprofiel

- Tekenreeksexpressie ScriptPath

- Tekenreeksexpressie SettingID

- UInt32 UnitsPerWeek

- Tekenreeksexpressie UserComment

- UInt32 Naam

- Tekenreeksexpressie User type

- Tekenreeksexpressie Werk stations



## <a name="nt-eventlog-file"></a>NT-gebeurtenis logboek bestand

Naam ruimte: root\cimv2

klasse Win32_NTEventlogFile


- Tekenreeksexpressie Naam

- UInt32 AccessMask

- True Faxberichten

- Tekenreeksexpressie Kop

- True Eerst

- Tekenreeksexpressie CompressionMethod

- DateTime CreationDate

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie Stationsletter

- Tekenreeksexpressie EightDotThreeFileName

- True Decodeer

- Tekenreeksexpressie EncryptionMethod

- Tekenreeksexpressie Switch

- Tekenreeksexpressie Bestands

- UInt64 FileSize

- Tekenreeksexpressie Type

- Tekenreeksexpressie FSName

- True Zit

- DateTime InstallDate

- UInt64 InUseCount

- DateTime LastAccessed

- DateTime LastModified

- Tekenreeksexpressie LogfileName

- Tekenreeksexpressie Fabricage

- UInt32 MaxFileSize

- UInt32 NumberOfRecords

- UInt32 OverwriteOutDated

- Tekenreeksexpressie OverWritePolicy

- Tekenreeksexpressie Programmapad

- True Lees bare

- Tekenreeksexpressie Bronnen []

- Tekenreeksexpressie Hebben

- True Opgehaald

- Tekenreeksexpressie Versie

- True Beschrijf bare



## <a name="office365proplusconfigurations"></a>Office365ProPlusConfigurations

Naam ruimte: root\cimv2

klasse Office365ProPlusConfigurations


- Tekenreeksexpressie KeyName

- Tekenreeksexpressie Autoupgrade

- Tekenreeksexpressie CCMManaged

- Tekenreeksexpressie CDNBaseUrl

- (Teken reeks) cfgUpdateChannel

- Tekenreeksexpressie ClientCulture

- Tekenreeksexpressie ClientFolder

- Tekenreeksexpressie GPOChannel

- Tekenreeksexpressie GPOOfficeMgmtCOM

- Tekenreeksexpressie InstallationPath

- Tekenreeksexpressie LastScenario

- Tekenreeksexpressie LastScenarioResult

- Tekenreeksexpressie OfficeMgmtCOM

- Tekenreeksexpressie Onafhankelijk

- Tekenreeksexpressie SharedComputerLicensing

- Tekenreeksexpressie UpdateChannel

- Tekenreeksexpressie UpdatePath

- Tekenreeksexpressie UpdatesEnabled

- Tekenreeksexpressie UpdateUrl

- Tekenreeksexpressie VersionToReport



## <a name="office-addin"></a>Office-invoeg toepassing

Naam ruimte: root\ccm\InvAgt

klasse CCM_OfficeAddin


- Tekenreeksexpressie Opstelling

- Tekenreeksexpressie ID

- Tekenreeksexpressie OfficeApp

- Tekenreeksexpressie Voert

- UInt32 AverageLoadTimeInMilliseconds

- Tekenreeksexpressie GEACTIVEERD

- Tekenreeksexpressie CompanyName

- UInt32 CrashCount

- Tekenreeksexpressie Beschrijvingen

- UInt32 ErrorCount

- Tekenreeksexpressie Bestands

- UInt64 FileSize

- UInt32 FileTimestamp

- Tekenreeksexpressie FileVersion

- Tekenreeksexpressie FriendlyName

- Tekenreeksexpressie FriendlyNameHash

- Tekenreeksexpressie IdHash

- UInt32 LoadBehavior

- UInt32 LoadCount

- UInt32 LoadFailCount

- Tekenreeksexpressie Product

- Tekenreeksexpressie ProductVersion



## <a name="office-client-metric"></a>Metrische Office-client

Naam ruimte: root\ccm\InvAgt

klasse CCM_OfficeClientMetric


- Tekenreeksexpressie OfficeApp

- UInt32 CompatibilityErrorCount

- UInt32 CrashedSessionCount

- UInt32 MacroCompileErrorCount

- UInt32 MacroRuntimeErrorCount

- UInt32 SessionCount



## <a name="office-device-summary"></a>Overzicht van Office-apparaten

Naam ruimte: root\ccm\InvAgt

klasse CCM_OfficeDeviceSummary


- True IsProPlusInstalled

- True IsTelemetryEnabled



## <a name="office-document-metric"></a>Metrische gegevens van Office-document

Naam ruimte: root\ccm\InvAgt

klasse CCM_OfficeDocumentMetric


- Tekenreeksexpressie OfficeApp

- UInt32 TotalCloudDocs

- UInt32 TotalLegacyDocs

- UInt32 TotalLocalDocs

- UInt32 TotalMacroDocs

- UInt32 TotalNonMacroDocs

- UInt32 TotalUncDocs



## <a name="office-document-solution"></a>Office-document oplossing

Naam ruimte: root\ccm\InvAgt

klasse CCM_OfficeDocumentSolution


- Tekenreeksexpressie DocumentSolutionId

- Tekenreeksexpressie OfficeApp

- UInt32 CompatibilityErrorCount

- UInt32 CrashCount

- Tekenreeksexpressie ExampleFileName

- UInt32 LoadCount

- UInt32 LoadFailCount

- UInt32 MacroCompileErrorCount

- UInt32 MacroRuntimeErrorCount

- Tekenreeksexpressie Voert



## <a name="office-macro-error"></a>Office-macro fout

Naam ruimte: root\ccm\InvAgt

klasse CCM_OfficeMacroError


- Tekenreeksexpressie DocumentSolutionId

- UInt32 Code

- UInt32 Aantal

- UInt64 LastOccurrence

- Tekenreeksexpressie Voert



## <a name="office-product-info"></a>Office-product informatie

Naam ruimte: root\ccm\InvAgt

klasse CCM_OfficeProductInfo


- Tekenreeksexpressie Product

- Tekenreeksexpressie ProductVersion

- Tekenreeksexpressie Opstelling

- Tekenreeksexpressie Kanalen

- UInt32 IsProPlusInstalled

- Tekenreeksexpressie Japanse

- Tekenreeksexpressie LicenseState



## <a name="office-vba-rule-violation"></a>Schending Office VBA-regel

Naam ruimte: root\ccm\InvAgt

klasse CCM_OfficeVbaRuleViolation


- UInt32 RuleId

- UInt32 FileCount

- Tekenreeksexpressie OfficeApp



## <a name="office-vbasummary"></a>Office-VbaSummary

Naam ruimte: root\ccm\InvAgt

klasse CCM_OfficeVbaScanResultsSummary


- UInt32 Aangepast

- UInt32 Design64

- UInt32 DuplicateVba

- True HasResults

- UInt32 HasVba

- UInt32 Niet toegankelijk

- UInt32 Taken

- UInt32 Issues64

- UInt32 IssuesNone

- UInt32 IssuesNone64

- UInt32 Lock

- UInt32 NoVba

- UInt32 Dergelijke

- UInt32 RemLimited

- UInt32 RemLimited64

- UInt32 RemSignificant

- UInt32 RemSignificant64

- UInt32 Score

- UInt32 Score64

- UInt32 Eind

- UInt32 /Categorievalidatie

- UInt32 Validation64



## <a name="operating-system"></a>Besturingssysteem

Naam ruimte: root\cimv2

klasse Win32_OperatingSystem


- Tekenreeksexpressie Naam

- Tekenreeksexpressie BootDevice

- Tekenreeksexpressie BuildNumber

- Tekenreeksexpressie BuildType

- Tekenreeksexpressie Kop

- Tekenreeksexpressie CodeSet

- Tekenreeksexpressie CountryCode

- Tekenreeksexpressie CSDVersion

- (SInt16) CurrentTimeZone

- True Fout opsporing

- Tekenreeksexpressie Beschrijvingen

- True Gedistribueerde

- (UInt8) ForegroundApplicationBoost

- UInt64 FreePhysicalMemory

- UInt64 FreeSpaceInPagingFiles

- UInt64 FreeVirtualMemory

- DateTime InstallDate

- DateTime LastBootUpTime

- DateTime LocalDateTime

- Tekenreeksexpressie Instelling

- Tekenreeksexpressie Fabricage

- UInt32 MaxNumberOfProcesses

- UInt64 MaxProcessMemorySize

- Tekenreeksexpressie MUILanguages[]

- UInt32 NumberOfLicensedUsers

- UInt32 NumberOfProcesses

- UInt32 NumberOfUsers

- UInt32 OperatingSystemSKU

- Tekenreeksexpressie Organisatie

- Tekenreeksexpressie OSArchitecture

- UInt32 OSLanguage

- UInt32 OSProductSuite

- UInt16 OSType

- Tekenreeksexpressie OtherTypeDescription

- Tekenreeksexpressie PlusProductID

- Tekenreeksexpressie PlusVersionNumber

- True Basis

- UInt32 Product type

- Tekenreeksexpressie RegisteredUser

- Tekenreeksexpressie SerialNumber

- UInt16 ServicePackMajorVersion

- UInt16 ServicePackMinorVersion

- UInt64 SizeStoredInPagingFiles

- Tekenreeksexpressie Hebben

- Tekenreeksexpressie SystemDevice

- Tekenreeksexpressie SystemDirectory

- UInt64 TotalSwapSpaceSize

- UInt64 TotalVirtualMemorySize

- UInt64 TotalVisibleMemorySize

- Tekenreeksexpressie Versie

- Tekenreeksexpressie WindowsDirectory



## <a name="operating-system-ex"></a>Besturings systeem ex

Naam ruimte: root\cimv2

klasse CCM_OperatingSystemExtended


- Tekenreeksexpressie Naam

- UInt32 SKU



## <a name="operating-system-recovery-configuration"></a>Configuratie van het besturings systeem herstellen

Naam ruimte: root\cimv2

klasse Win32_OSRecoveryConfiguration


- Tekenreeksexpressie Naam

- True Opnieuw opstarten

- Tekenreeksexpressie Kop

- Tekenreeksexpressie DebugFilePath

- Tekenreeksexpressie Beschrijvingen

- True KernelDumpOnly

- True OverwriteExistingDebugFile

- True SendAdminAlert

- Tekenreeksexpressie SettingID

- True WriteDebugInfo

- True WriteToSystemLog



## <a name="optional-feature"></a>Optionele functie

Naam ruimte: root\cimv2

klasse Win32_OptionalFeature


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- DateTime InstallDate

- UInt32 InstallState

- Tekenreeksexpressie Hebben



## <a name="page-file-setting"></a>Instelling voor pagina bestand

Naam ruimte: root\cimv2

klasse Win32_PageFileSetting


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- UInt32 InitialSize

- UInt32 MaximumSize

- Tekenreeksexpressie SettingID



## <a name="parallel-port"></a>Parallelle poort

Naam ruimte: root\cimv2

klasse Win32_ParallelPort


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- UInt16 Mogelijkheden []

- Tekenreeksexpressie CapabilityDescriptions[]

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- True DMASupport

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- UInt32 MaxNumberControlled

- Tekenreeksexpressie Naam

- True OSAutoDiscovered

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt16 ProtocolSupported

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- DateTime TimeOfLastReset



## <a name="bios"></a>BIOS

Naam ruimte: root\cimv2

klasse Win32_BIOS


- Tekenreeksexpressie Naam

- Tekenreeksexpressie SoftwareElementID

- UInt16 SoftwareElementState

- UInt16 TargetOperatingSystem

- Tekenreeksexpressie Versie

- UInt16 BiosCharacteristics[]

- Tekenreeksexpressie BIOSVersion[]

- Tekenreeksexpressie BuildNumber

- Tekenreeksexpressie Kop

- Tekenreeksexpressie CodeSet

- Tekenreeksexpressie CurrentLanguage

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie IdentificationCode

- UInt16 InstallableLanguages

- DateTime InstallDate

- Tekenreeksexpressie LanguageEdition

- Tekenreeksexpressie ListOfLanguages[]

- Tekenreeksexpressie Fabricage

- Tekenreeksexpressie OtherTargetOS

- True PrimaryBIOS

- DateTime ReleaseDate

- Tekenreeksexpressie SerialNumber

- Tekenreeksexpressie SMBIOSBIOSVersion

- UInt16 SMBIOSMajorVersion

- UInt16 SMBIOSMinorVersion

- True SMBIOSPresent

- Tekenreeksexpressie Hebben



## <a name="pcmcia-controller"></a>PCMCIA-controller

Naam ruimte: root\cimv2

klasse Win32_PCMCIAController


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- UInt32 MaxNumberControlled

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt16 ProtocolSupported

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- DateTime TimeOfLastReset



## <a name="physical-memory"></a>Fysiek geheugen

Naam ruimte: root\cimv2

klasse Win32_PhysicalMemory


- Tekenreeksexpressie CreationClassName

- Tekenreeksexpressie Tag

- Tekenreeksexpressie BankLabel

- UInt64 Capaciteit

- Tekenreeksexpressie Kop

- UInt16 DataWidth

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie DeviceLocator

- UInt16 FormFactor

- True HotSwappable

- DateTime InstallDate

- UInt16 InterleaveDataDepth

- UInt32 InterleavePosition

- Tekenreeksexpressie Fabricage

- UInt16 MemoryType

- Tekenreeksexpressie Activiteitsmodel

- Tekenreeksexpressie Naam

- Tekenreeksexpressie OtherIdentifyingInfo

- Tekenreeksexpressie PartNumber

- UInt32 PositionInRow

- True PoweredOn

- True Verwissel bare

- True Replaceable

- Tekenreeksexpressie SerialNumber

- Tekenreeksexpressie SKU

- UInt32 Waarmee

- Tekenreeksexpressie Hebben

- UInt16 TotalWidth

- UInt16 TypeDetail

- Tekenreeksexpressie Versie



## <a name="physicaldisk"></a>PhysicalDisk

Naam ruimte: root\microsoft\windows\storage

klasse MSFT_PhysicalDisk


- Tekenreeksexpressie Id

- UInt64 AllocatedSize

- UInt16 BusType

- UInt16 CannotPoolReason[]

- True CanPool

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie DeviceId

- UInt16 EnclosureNumber

- Tekenreeksexpressie FirmwareVersion

- Tekenreeksexpressie FriendlyName

- UInt16 HealthStatus

- True IsIndicationEnabled

- True IsPartial

- UInt64 LogicalSectorSize

- Tekenreeksexpressie Fabricage

- UInt16 Type

- Tekenreeksexpressie Activiteitsmodel

- UInt16 OperationalStatus[]

- Tekenreeksexpressie OtherCannotPoolReasonDescription

- Tekenreeksexpressie PartNumber

- Tekenreeksexpressie PhysicalLocation

- UInt64 PhysicalSectorSize

- Tekenreeksexpressie SerialNumber

- UInt64 Size

- UInt16 SlotNumber

- Tekenreeksexpressie SoftwareVersion

- UInt32 SpindleSpeed

- UInt16 SupportedUsages[]

- Tekenreeksexpressie UniqueId

- UInt16 Belasting



## <a name="pnp-device-driver"></a>PNP-APPARAATSTUURPROGRAMMA

Naam ruimte: root\cimv2

klasse Win32_PnpEntity


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- Tekenreeksexpressie Kop

- Tekenreeksexpressie ClassGuid

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie CreationClassName

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie Service

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie SystemCreationClassName

- Tekenreeksexpressie Systemnaam



## <a name="pointing-device"></a>Aanwijs apparaat

Naam ruimte: root\cimv2

klasse Win32_PointingDevice


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- UInt16 DeviceInterface

- UInt32 DoubleSpeedThreshold

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- UInt16 Handig

- Tekenreeksexpressie HardwareType

- Tekenreeksexpressie InfFileName

- Tekenreeksexpressie InfSection

- DateTime InstallDate

- True IsLocked

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- Tekenreeksexpressie Naam

- (UInt8) NumberOfButtons

- Tekenreeksexpressie PNPDeviceID

- UInt16 PointingType

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt32 QuadSpeedThreshold

- UInt32 Opgelost

- UInt32 SampleRate

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- UInt32 Synchronisatie

- Tekenreeksexpressie Systemnaam



## <a name="portable-battery"></a>Draag bare batterij

Naam ruimte: root\cimv2

klasse Win32_PortableBattery


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- UInt16 BatteryStatus

- UInt16 CapacityMultiplier

- Tekenreeksexpressie Kop

- UInt16 Chemische

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- UInt32 DesignCapacity

- UInt64 DesignVoltage

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- UInt16 EstimatedChargeRemaining

- UInt32 EstimatedRunTime

- UInt32 ExpectedLife

- UInt32 FullChargeCapacity

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Locatie

- Tekenreeksexpressie ManufactureDate

- Tekenreeksexpressie Fabricage

- UInt16 MaxBatteryError

- UInt32 MaxRechargeTime

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie SmartBatteryVersion

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- UInt32 TimeOnBattery

- UInt32 TimeToFullCharge



## <a name="ports"></a>Poorten

Naam ruimte: root\cimv2

klasse Win32_PortResource

- UInt64 StartingAddress

- True Toe

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- UInt64 EndingAddress

- DateTime InstallDate

- Tekenreeksexpressie Naam

- Tekenreeksexpressie Hebben



## <a name="power-capabilities"></a>Energie mogelijkheden

Naam ruimte: root\CCM\powermanagementagent

klasse CCM_PwrMgmtSystemPowerCapabilities


- UInt32 PreferredPMProfile

- True ApmPresent

- True BatteriesAreShortTerm

- True FullWake

- True LidPresent

- Tekenreeksexpressie MinDeviceWakeState

- True ProcessorThrottle

- Tekenreeksexpressie RtcWake

- True SystemBatteriesPresent

- True SystemS1

- True SystemS2

- True SystemS3

- True SystemS4

- True SystemS5

- True UpsPresent

- True VideoDimPresent



## <a name="power-configurations"></a>Energie configuraties

Naam ruimte: root\CCM\policy\machine\actualconfig

klasse CCM_PowerConfig


- Tekenreeksexpressie PowerConfigID

- UInt32 DurationInSec

- Tekenreeksexpressie NonPeakPowerPlan

- Tekenreeksexpressie NonPeakPowerPlanName

- Tekenreeksexpressie PeakPowerPlan

- Tekenreeksexpressie PeakPowerPlanName

- Tekenreeksexpressie PeakStartTimeHoursMin

- Tekenreeksexpressie WakeUpTimeHoursMin



## <a name="power-management-insomnia-reasons"></a>Slapeloosheid redenen voor energie beheer

Naam ruimte: root\CCM\powermanagementagent

klasse CCM_PwrMgmtLastSuspendError


- Tekenreeksexpressie Aanvrager

- Tekenreeksexpressie RequesterType

- Tekenreeksexpressie RequestType

- DateTime Tegelijk

- UInt32 AdditionalCode

- Tekenreeksexpressie AdditionalInfo

- Tekenreeksexpressie RequesterInfo

- True UnknownRequester



## <a name="power-management-daily"></a>Energie beheer dagelijks

Naam ruimte: root\CCM\powermanagementagent

klasse CCM_PwrMgmtActualDay


- DateTime Vallen

- Tekenreeksexpressie TypeOfEvent

- (UInt32) hr0_1

- (UInt32) hr1_2

- (UInt32) hr10_11

- (UInt32) hr11_12

- (UInt32) hr12_13

- (UInt32) hr13_14

- (UInt32) hr14_15

- (UInt32) hr15_16

- (UInt32) hr16_17

- (UInt32) hr17_18

- (UInt32) hr18_19

- (UInt32) hr19_20

- (UInt32) hr2_3

- (UInt32) hr20_21

- (UInt32) hr21_22

- (UInt32) hr22_23

- (UInt32) hr23_0

- (UInt32) hr3_4

- (UInt32) hr4_5

- (UInt32) hr5_6

- (UInt32) hr6_7

- (UInt32) hr7_8

- (UInt32) hr8_9

- (UInt32) hr9_10

- (UInt32) minutesTotal



## <a name="power-client-opt-out-settings"></a>Instellingen voor afmelden energie client

Naam ruimte: root\ccm\ClientSDK

klasse CCM_PowerManagementClientOptoutSetting


- True AdminAllowOptout

- True EffectiveClientOptOut

- True IsClientOptOut



## <a name="power-management-monthly"></a>Energie beheer-maandelijks

Naam ruimte: root\CCM\powermanagementagent

klasse CCM_PwrMgmtMonth


- DateTime MonthStart

- (UInt32) minutesComputerActive

- (UInt32) minutesComputerOn

- (UInt32) minutesComputerShutdown

- (UInt32) minutesComputerSleep

- (UInt32) minutesMonitorOn

- (UInt32) minutesTotal

- Tekenreeksexpressie TypeOfEvent



## <a name="power-settings"></a>Energie-instellingen

Naam ruimte: root\cimv2\sms

klasse SMS_PowerSettings


- Tekenreeksexpressie GPT

- Tekenreeksexpressie ACSettingIndex

- Tekenreeksexpressie ACValue

- Tekenreeksexpressie DCSettingIndex

- Tekenreeksexpressie DCValue

- Tekenreeksexpressie Naam

- Tekenreeksexpressie UnitSpecifier



## <a name="print-jobs"></a>Afdruk taken

Naam ruimte: root\cimv2

klasse Win32_PrintJob


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Param1

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie Document

- Tekenreeksexpressie Stuurprogrammanaam

- DateTime ElapsedTime

- Tekenreeksexpressie HostPrintQueue

- DateTime InstallDate

- UInt32 JobId

- Tekenreeksexpressie JobStatus

- Tekenreeksexpressie Meldingen

- Tekenreeksexpressie Bent

- UInt32 PagesPrinted

- Tekenreeksexpressie Instellen

- Tekenreeksexpressie PrintProcessor

- UInt32 Prioriteiten

- UInt32 Size

- DateTime StartTime

- Tekenreeksexpressie Hebben

- UInt32 StatusMask

- DateTime TimeSubmitted

- UInt32 Total pages

- DateTime UntilTime



## <a name="printer-configuration"></a>Printer configuratie

Naam ruimte: root\cimv2

klasse Win32_PrinterConfiguration


- Tekenreeksexpressie Naam

- UInt32 BitsPerPel

- Tekenreeksexpressie Kop

- True Collate

- UInt32 Kleur

- UInt32 Versies

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie DeviceName

- UInt32 DisplayFlags

- UInt32 DisplayFrequency

- UInt32 DitherType

- UInt32 DriverVersion

- True Modus

- Tekenreeksexpressie Formuliernaam

- UInt32 HorizontalResolution

- UInt32 ICMIntent

- UInt32 ICMMethod

- UInt32 LogPixels

- UInt32 Type

- UInt32 Opstelling

- UInt32 PaperLength

- Tekenreeksexpressie Formaat

- UInt32 PaperWidth

- UInt32 PelsHeight

- UInt32 PelsWidth

- UInt32 Afdruk

- UInt32 Tarieven

- Tekenreeksexpressie SettingID

- UInt32 SpecificationVersion

- UInt32 TTOption

- UInt32 VerticalResolution

- UInt32 XResolution

- UInt32 YResolution



## <a name="printer-device"></a>Printer apparaat

Naam ruimte: root\cimv2

klasse Win32_Printer


- Tekenreeksexpressie DeviceID

- UInt32 Eigenschappen

- UInt16 Availability

- UInt32 AveragePagesPerMinute

- UInt16 Mogelijkheden []

- Tekenreeksexpressie CapabilityDescriptions[]

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- UInt32 DefaultPriority

- Tekenreeksexpressie Beschrijvingen

- UInt16 DetectedErrorState

- Tekenreeksexpressie Stuurprogrammanaam

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- UInt32 HorizontalResolution

- DateTime InstallDate

- UInt32 JobCountSinceLastReset

- UInt16 LanguagesSupported[]

- UInt32 LastErrorCode

- Tekenreeksexpressie Locatie

- Tekenreeksexpressie Naam

- UInt16 PaperSizesSupported[]

- Tekenreeksexpressie PNPDeviceID

- Tekenreeksexpressie Poortnaam

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie PrinterPaperNames[]

- UInt32 PrinterState

- UInt16 PrinterStatus

- Tekenreeksexpressie PrintJobDataType

- Tekenreeksexpressie PrintProcessor

- Tekenreeksexpressie SeparatorFile

- Tekenreeksexpressie ServerName

- Tekenreeksexpressie ShareName

- True SpoolEnabled

- DateTime StartTime

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- DateTime TimeOfLastReset

- DateTime UntilTime

- UInt32 VerticalResolution



## <a name="process"></a>Proces

Naam ruimte: root\cimv2

klasse Win32_Process


- Tekenreeksexpressie Afhandeling

- Tekenreeksexpressie Kop

- DateTime CreationDate

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie ExecutablePath

- UInt16 ExecutionState

- UInt32 HandleCount

- DateTime InstallDate

- UInt64 KernelModeTime

- UInt32 MaximumWorkingSetSize

- UInt32 MinimumWorkingSetSize

- Tekenreeksexpressie Naam

- Tekenreeksexpressie OSName

- UInt64 OtherOperationCount

- UInt64 OtherTransferCount

- UInt32 PageFaults

- UInt32 PageFileUsage

- UInt32 ParentProcessId

- UInt32 PeakPageFileUsage

- UInt64 PeakVirtualSize

- UInt32 PeakWorkingSetSize

- UInt32 Prioriteiten

- UInt64 PrivatePageCount

- UInt32 Process

- UInt32 QuotaNonPagedPoolUsage

- UInt32 QuotaPagedPoolUsage

- UInt32 QuotaPeakNonPagedPoolUsage

- UInt32 QuotaPeakPagedPoolUsage

- UInt64 ReadOperationCount

- UInt64 ReadTransferCount

- UInt32 SessionId

- Tekenreeksexpressie Hebben

- DateTime TerminationDate

- UInt32 ThreadCount

- UInt64 UserModeTime

- UInt64 VirtualSize

- Tekenreeksexpressie WindowsVersion

- UInt64 WorkingSetSize

- UInt64 WriteOperationCount

- UInt64 WriteTransferCount



## <a name="processor"></a>Processor

Naam ruimte: root\cimv2\sms

klasse SMS_Processor


- Tekenreeksexpressie DeviceID

- UInt16 AddressWidth

- UInt16 Opstelling

- UInt16 Availability

- UInt16 BrandID

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie CPUHash

- Tekenreeksexpressie CPUKey

- UInt16 CpuStatus

- UInt32 CurrentClockSpeed

- UInt16 CurrentVoltage

- UInt16 DataWidth

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- UInt32 ExtClock

- UInt16 Gezinslid

- DateTime InstallDate

- True Is64Bit

- True IsHyperthreadCapable

- True IsHyperthreadEnabled

- True IsMobile

- True IsTrustedExecutionCapable

- True IsVitualizationCapable

- UInt32 L2CacheSize

- UInt32 L2CacheSpeed

- UInt32 L3CacheSize

- UInt32 L3CacheSpeed

- UInt32 LastErrorCode

- UInt16 Afvlakking

- UInt16 LoadPercentage

- Tekenreeksexpressie Fabricage

- UInt32 MaxClockSpeed

- Tekenreeksexpressie Naam

- UInt32 NormSpeed

- UInt32 NumberOfCores

- UInt32 NumberOfLogicalProcessors

- Tekenreeksexpressie OtherFamilyDescription

- True PartOfDomain

- UInt32 PCache

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie ProcessorId

- UInt16 Processor type

- UInt16 Feedback

- Tekenreeksexpressie Rolvak

- Tekenreeksexpressie SocketDesignation

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Lopen

- Tekenreeksexpressie Systemnaam

- Tekenreeksexpressie UniqueId

- UInt16 UpgradeMethod

- Tekenreeksexpressie Versie

- UInt32 VoltageCaps

- Tekenreeksexpressie Groep



## <a name="protected-volume-information"></a>Gegevens van beveiligd volume

Naam ruimte: root\cimv2\sms

klasse CCM_ProtectedVolumeInfo


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Stationsaanduiding

- UInt32 Beveiligings type hebben



## <a name="protocol"></a>Protocol

Naam ruimte: root\cimv2

klasse Win32_NetworkProtocol


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Kop

- True ConnectionlessService

- Tekenreeksexpressie Beschrijvingen

- True GuaranteesDelivery

- True GuaranteesSequencing

- DateTime InstallDate

- UInt32 MaximumAddressSize

- UInt32 MaximumMessageSize

- True MessageOriented

- UInt32 MinimumAddressSize

- True PseudoStreamOriented

- Tekenreeksexpressie Hebben

- True SupportsBroadcasting

- True SupportsConnectData

- True SupportsDisconnectData

- True SupportsEncryption

- True SupportsExpeditedData

- True SupportsFragmentation

- True SupportsGracefulClosing

- True SupportsGuaranteedBandwidth

- True SupportsMulticasting

- True SupportsQualityofService



## <a name="quick-fix-engineering"></a>Quick Fix Engineering

Naam ruimte: root\cimv2

klasse Win32_QuickFixEngineering


- Tekenreeksexpressie HotFixID

- Tekenreeksexpressie ServicePackInEffect

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie FixComments

- DateTime InstallDate

- Tekenreeksexpressie InstalledBy

- Tekenreeksexpressie InstalledOn

- Tekenreeksexpressie Naam

- Tekenreeksexpressie Hebben



## <a name="ccm-recently-used-applications"></a>Recent gebruikte toepassingen CCM

Naam ruimte: root\cimv2\sms

klasse CCM_RecentlyUsedApps


- Tekenreeksexpressie ExplorerFileName

- Tekenreeksexpressie FolderPath

- Tekenreeksexpressie LastUserName

- Tekenreeksexpressie AdditionalProductCodes

- Tekenreeksexpressie CompanyName

- Tekenreeksexpressie FileDescription

- Tekenreeksexpressie FilePropertiesHash

- UInt32 FileSize

- Tekenreeksexpressie FileVersion

- DateTime LastUsedTime

- UInt32 LaunchCount

- (Teken reeks) msiDisplayName

- (Teken reeks) msiPublisher

- (Teken reeks) msiVersion

- Tekenreeksexpressie OriginalFileName

- Tekenreeksexpressie Code

- UInt32 ProductLanguage

- Tekenreeksexpressie Product

- Tekenreeksexpressie ProductVersion

- Tekenreeksexpressie SoftwarePropertiesHash



## <a name="registry"></a>Register

Naam ruimte: root\cimv2

klasse Win32_Registry


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Kop

- UInt32 CurrentSize

- Tekenreeksexpressie Beschrijvingen

- DateTime InstallDate

- UInt32 MaximumSize

- UInt32 ProposedSize

- Tekenreeksexpressie Hebben



## <a name="scsi-controller"></a>SCSI-controller

Naam ruimte: root\cimv2

klasse Win32_SCSIController


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- UInt32 ControllerTimeouts

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie DeviceMap

- Tekenreeksexpressie Stuurprogrammanaam

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- Tekenreeksexpressie HardwareVersion

- UInt32 TabIndex

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- UInt32 MaxDataWidth

- UInt32 MaxNumberControlled

- UInt64 MaxTransferRate

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt16 ProtectionManagement

- UInt16 ProtocolSupported

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- DateTime TimeOfLastReset



## <a name="serial-port-configuration"></a>Configuratie van seriële poort

Naam ruimte: root\cimv2

klasse Win32_SerialPortConfiguration


- Tekenreeksexpressie Naam

- True AbortReadWriteOnError

- UInt32 Snelheid

- True BinaryModeEnabled

- UInt32 BitsPerByte

- Tekenreeksexpressie Kop

- True ContinueXMitOnXOff

- True CTSOutflowControl

- Tekenreeksexpressie Beschrijvingen

- True DiscardNULLBytes

- True DSROutflowControl

- True DSRSensitivity

- Tekenreeksexpressie DTRFlowControlType

- UInt32 EOFCharacter

- UInt32 ErrorReplaceCharacter

- True ErrorReplacementEnabled

- UInt32 EventCharacter

- True IsBusy

- Tekenreeksexpressie Parity

- True ParityCheckEnabled

- Tekenreeksexpressie RTSFlowControlType

- Tekenreeksexpressie SettingID

- Tekenreeksexpressie StopBits

- UInt32 XOffCharacter

- UInt32 XOffXMitThreshold

- UInt32 XOnCharacter

- UInt32 XOnXMitThreshold

- UInt32 XOnXOffInFlowControl

- UInt32 XOnXOffOutFlowControl



## <a name="serial-ports"></a>Seriële poorten

Naam ruimte: root\cimv2

klasse Win32_SerialPort


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- True Waarde

- UInt16 Mogelijkheden []

- Tekenreeksexpressie CapabilityDescriptions[]

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- UInt32 MaxBaudRate

- UInt32 MaximumInputBufferSize

- UInt32 MaximumOutputBufferSize

- UInt32 MaxNumberControlled

- Tekenreeksexpressie Naam

- True OSAutoDiscovered

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt16 ProtocolSupported

- Tekenreeksexpressie ProviderType

- True SettableBaudRate

- True SettableDataBits

- True SettableFlowControl

- True SettableParity

- True SettableParityCheck

- True SettableRLSD

- True SettableStopBits

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- True Supports16BitMode

- True SupportsDTRDSR

- True SupportsElapsedTimeouts

- True SupportsIntTimeouts

- True SupportsParityCheck

- True SupportsRLSD

- True SupportsRTSCTS

- True SupportsSpecialCharacters

- True SupportsXOnXOff

- True SupportsXOnXOffSet

- Tekenreeksexpressie Systemnaam

- DateTime TimeOfLastReset



## <a name="server-feature"></a>Serverfunctie

Naam ruimte: root\cimv2

klasse Win32_ServerFeature


- UInt32 ID

- Tekenreeksexpressie Naam

- UInt32 ParentID



## <a name="services"></a>Services

Naam ruimte: root\cimv2

klasse Win32_Service


- Tekenreeksexpressie Naam

- True AcceptPause

- True AcceptStop

- Tekenreeksexpressie Kop

- UInt32 Points

- Tekenreeksexpressie Beschrijvingen

- True DesktopInteract

- Tekenreeksexpressie DisplayName

- Tekenreeksexpressie ErrorControl

- UInt32 ExitCode

- DateTime InstallDate

- Tekenreeksexpressie PathName

- UInt32 Process

- UInt32 ServiceSpecificExitCode

- Tekenreeksexpressie Service

- True Helpen

- Tekenreeksexpressie Start mode

- Tekenreeksexpressie StartName

- Tekenreeksexpressie Overheids

- Tekenreeksexpressie Hebben

- Tekenreeksexpressie Systemnaam

- UInt32 TagId

- UInt32 WaitHint



## <a name="shares"></a>Shares

Naam ruimte: root\cimv2

klasse Win32_Share


- Tekenreeksexpressie Naam

- UInt32 AccessMask

- True AllowMaximum

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- DateTime InstallDate

- UInt32 MaximumAllowed

- Tekenreeksexpressie Programmapad

- Tekenreeksexpressie Hebben

- UInt32 Voert



## <a name="sw-licensing-product"></a>SOFTWARE licentie verlenings product

Naam ruimte: root\cimv2

klasse SoftwareLicensingProduct


- Tekenreeksexpressie ID

- Tekenreeksexpressie ApplicationID

- Tekenreeksexpressie Beschrijvingen

- DateTime EvaluationEndDate

- UInt32 GracePeriodRemaining

- UInt32 LicenseStatus

- Tekenreeksexpressie MachineURL

- Tekenreeksexpressie Naam

- Tekenreeksexpressie OfflineInstallationId

- Tekenreeksexpressie PartialProductKey

- Tekenreeksexpressie ProcessorURL

- Tekenreeksexpressie ProductKeyID

- Tekenreeksexpressie ProductKeyURL

- Tekenreeksexpressie UseLicenseURL



## <a name="sw-licensing-service"></a>SW-licentie service

Naam ruimte: root\cimv2

klasse SoftwareLicensingService


- Tekenreeksexpressie Versie

- Tekenreeksexpressie ClientMachineID

- UInt32 IsKeyManagementServiceMachine

- UInt32 KeyManagementServiceCurrentCount

- Tekenreeksexpressie KeyManagementServiceMachine

- Tekenreeksexpressie KeyManagementServiceProductKeyID

- UInt32 PolicyCacheRefreshRequired

- UInt32 RequiredClientCount

- UInt32 VLActivationInterval

- UInt32 VLRenewalInterval



## <a name="software-shortcut"></a>Software snelkoppeling

Naam ruimte: root\cimv2\sms

klasse SMS_SoftwareShortcut


- Tekenreeksexpressie ShortcutKey

- Tekenreeksexpressie BinFileVersion

- Tekenreeksexpressie BinProductVersion

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie FilePropertiesHash

- Tekenreeksexpressie FilePropertiesHashEx

- UInt32 FileSize

- Tekenreeksexpressie FileVersion

- UInt32 Japanse

- Tekenreeksexpressie ParentName

- Tekenreeksexpressie Voortplant

- Tekenreeksexpressie Code

- Tekenreeksexpressie ProductVersion

- Tekenreeksexpressie Uitgever

- Tekenreeksexpressie Snelkoppelings

- UInt32 ShortcutType

- Tekenreeksexpressie TargetExecutable



## <a name="sms_softwaretag"></a>SMS_SoftwareTag

Naam ruimte: root\cimv2\sms

klasse SMS_SoftwareTag


- Tekenreeksexpressie TagCreatorRegid

- Tekenreeksexpressie UniqueID

- Tekenreeksexpressie DisplayVersion

- True EntitlementRequired

- Tekenreeksexpressie Product

- Tekenreeksexpressie SoftwareCreator

- Tekenreeksexpressie SoftwareCreatorRegid

- Tekenreeksexpressie SoftwareLicensor

- Tekenreeksexpressie SoftwareLicensorRegid

- Tekenreeksexpressie TagCreator

- (SInt32) VersionMajor

- (SInt32) VersionMinor



## <a name="sound-devices"></a>Geluids apparaten

Naam ruimte: root\cimv2

klasse Win32_SoundDevice


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- UInt16 DMABufferSize

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- UInt32 MPU401Address

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie Product

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam



## <a name="system-account"></a>Systeemaccount

Naam ruimte: root\cimv2

klasse Win32_SystemAccount


- Tekenreeksexpressie Domeinen

- Tekenreeksexpressie Naam

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- DateTime InstallDate

- Tekenreeksexpressie GEVAL

- (UInt8) SIDType

- Tekenreeksexpressie Hebben



## <a name="system-boot-data"></a>Opstart gegevens van het systeem

Naam ruimte: root\CCM

klasse CCM_SystemBootData


- UInt64 SystemStartTime

- UInt32 BiosDuration

- UInt16 BootDiskMediaType

- UInt32 BootDuration

- UInt32 EventLogStart

- UInt32 GPDuration

- Tekenreeksexpressie OSVersion

- UInt32 UpdateDuration



## <a name="system-boot-summary"></a>Samen vatting van systeem opstarten

Naam ruimte: root\CCM

klasse CCM_SystemBootSummary


- UInt32 AverageBootFrequency

- UInt32 LatestBiosDuration

- UInt32 LatestBootDuration

- UInt32 LatestCoreBootDuration

- UInt32 LatestEventLogStart

- UInt32 LatestGPDuration

- UInt32 LatestUpdateDuration

- UInt32 MaxBiosDuration

- UInt32 MaxBootDuration

- UInt32 MaxCoreBootDuration

- UInt32 MaxEventLogStart

- UInt32 MaxGPDuration

- UInt32 MaxUpdateDuration

- UInt32 MedianBiosDuration

- UInt32 MedianBootDuration

- UInt32 MedianCoreBootDuration

- UInt32 MedianEventLogStart

- UInt32 MedianGPDuration

- UInt32 MedianUpdateDuration



## <a name="system-console-usage"></a>Gebruik van systeem console

Naam ruimte: root\cimv2\sms

klasse SMS_SystemConsoleUsage


- DateTime SecurityLogStartDate

- Tekenreeksexpressie TopConsoleUser

- UInt32 TotalConsoleTime

- UInt32 TotalConsoleUsers

- UInt32 TotalSecurityLogTime



## <a name="system-console-user"></a>Gebruiker van systeem console

Naam ruimte: root\cimv2\sms

klasse SMS_SystemConsoleUser


- Tekenreeksexpressie SystemConsoleUser

- DateTime LastConsoleUse

- UInt32 NumberOfConsoleLogons

- UInt32 TotalUserConsoleMinutes



## <a name="system-devices"></a>Systeem apparaten

Naam ruimte: root\cimv2\sms

klasse CCM_SystemDevices


- Tekenreeksexpressie Naam

- Tekenreeksexpressie CompatibleIDs[]

- Tekenreeksexpressie DeviceID

- Tekenreeksexpressie HardwareIDs[]

- True IsPnP



## <a name="system-drivers"></a>Systeem Stuur Programma's

Naam ruimte: root\cimv2

klasse Win32_SystemDriver


- Tekenreeksexpressie Naam

- True AcceptPause

- True AcceptStop

- Tekenreeksexpressie Kop

- Tekenreeksexpressie Beschrijvingen

- True DesktopInteract

- Tekenreeksexpressie DisplayName

- Tekenreeksexpressie ErrorControl

- UInt32 ExitCode

- DateTime InstallDate

- Tekenreeksexpressie PathName

- UInt32 ServiceSpecificExitCode

- Tekenreeksexpressie Service

- True Helpen

- Tekenreeksexpressie Start mode

- Tekenreeksexpressie StartName

- Tekenreeksexpressie Overheids

- Tekenreeksexpressie Hebben

- Tekenreeksexpressie Systemnaam

- UInt32 TagId



## <a name="system-enclosure"></a>Systeembehuizing

Naam ruimte: root\cimv2

klasse Win32_SystemEnclosure


- Tekenreeksexpressie Tag

- True AudibleAlarm

- Tekenreeksexpressie BreachDescription

- Tekenreeksexpressie CableManagementStrategy

- Tekenreeksexpressie Kop

- UInt16 ChassisTypes[]

- (SInt16) CurrentRequiredOrProduced

- Tekenreeksexpressie Beschrijvingen

- UInt16 HeatGeneration

- True HotSwappable

- DateTime InstallDate

- True LockPresent

- Tekenreeksexpressie Fabricage

- Tekenreeksexpressie Activiteitsmodel

- Tekenreeksexpressie Naam

- UInt16 NumberOfPowerCords

- Tekenreeksexpressie OtherIdentifyingInfo

- Tekenreeksexpressie PartNumber

- True PoweredOn

- True Verwissel bare

- True Replaceable

- UInt16 SecurityBreach

- UInt16 SecurityStatus

- Tekenreeksexpressie SerialNumber

- Tekenreeksexpressie ServiceDescriptions[]

- UInt16 ServicePhilosophy[]

- Tekenreeksexpressie SKU

- Tekenreeksexpressie SMBIOSAssetTag

- Tekenreeksexpressie Hebben

- Tekenreeksexpressie TypeDescriptions[]

- Tekenreeksexpressie Versie

- True VisibleAlarm



## <a name="tape-drive"></a>Tape station

Naam ruimte: root\cimv2

klasse Win32_TapeDrive


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- UInt16 Mogelijkheden []

- Tekenreeksexpressie CapabilityDescriptions[]

- Tekenreeksexpressie Kop

- UInt32 Compressie

- Tekenreeksexpressie CompressionMethod

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- UInt64 DefaultBlockSize

- Tekenreeksexpressie Beschrijvingen

- UInt32 ECC

- UInt32 EOTWarningZoneSize

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- Tekenreeksexpressie ErrorMethodology

- UInt32 FeaturesHigh

- UInt32 FeaturesLow

- Tekenreeksexpressie ID

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- UInt64 MaxBlockSize

- UInt64 MaxMediaSize

- UInt32 MaxPartitionCount

- Tekenreeksexpressie Type

- UInt64 MinBlockSize

- Tekenreeksexpressie Naam

- True NeedsCleaning

- UInt32 NumberOfMediaSupported

- UInt32 Opvulling

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt32 ReportSetMarks

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam



## <a name="time-zone"></a>Tijdzone

Naam ruimte: root\cimv2

klasse Win32_TimeZone


- Tekenreeksexpressie StandardName

- (SInt32) Oordelen

- Tekenreeksexpressie Kop

- (SInt32) DaylightBias

- UInt32 DaylightDay

- (UInt8) DaylightDayOfWeek

- UInt32 DaylightHour

- UInt32 DaylightMillisecond

- UInt32 DaylightMinute

- UInt32 DaylightMonth

- Tekenreeksexpressie DaylightName

- UInt32 DaylightSecond

- UInt32 DaylightYear

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie SettingID

- UInt32 Standard bias

- UInt32 StandardDay

- (UInt8) StandardDayOfWeek

- UInt32 StandardHour

- UInt32 StandardMillisecond

- UInt32 StandardMinute

- UInt32 StandardMonth

- UInt32 StandardSecond

- UInt32 StandardYear



## <a name="tpm"></a>TPM

Naam ruimte: root\CIMv2\Security\MicrosoftTpm

klasse Win32_Tpm


- True IsActivated_InitialValue

- True IsEnabled_InitialValue

- True IsOwned_InitialValue

- UInt32 ManufacturerId

- Tekenreeksexpressie ManufacturerVersion

- Tekenreeksexpressie ManufacturerVersionInfo

- Tekenreeksexpressie PhysicalPresenceVersionInfo

- Tekenreeksexpressie SpecVersion



## <a name="tpm-status"></a>TPM-status

Naam ruimte: root\cimv2\sms

klasse SMS_TPM


- True IsReady

- UInt32 Gegevens

- True IsApplicable



## <a name="ts-issued-license"></a>Uitgegeven TS-licentie

Naam ruimte: root\cimv2

klasse Win32_TSIssuedLicense


- UInt32 LicenseId

- DateTime ExpirationDate

- DateTime IssueDate

- UInt32 KeyPackId

- UInt32 LicenseStatus

- (Teken reeks) sHardwareId

- (Teken reeks) sIssuedToComputer

- (Teken reeks) sIssuedToUser



## <a name="ts-license-key-pack"></a>TS-licentie sleutel pakket

Naam ruimte: root\cimv2

klasse Win32_TSLicenseKeyPack


- UInt32 KeyPackId

- UInt32 AvailableLicenses

- Tekenreeksexpressie Beschrijvingen

- UInt32 IssuedLicenses

- UInt32 KeyPackType

- UInt32 Product type

- Tekenreeksexpressie ProductVersion

- UInt32 TotalLicenses



## <a name="uninterruptible-power-supply"></a>Uninterruptible Power Supply

Naam ruimte: root\cimv2

klasse Win32_UninterruptiblePowerSupply


- Tekenreeksexpressie DeviceID

- UInt16 ActiveInputVoltage

- UInt16 Availability

- True BatteryInstalled

- True CanTurnOffRemotely

- Tekenreeksexpressie Kop

- Tekenreeksexpressie CommandFile

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- UInt16 EstimatedChargeRemaining

- UInt32 EstimatedRunTime

- UInt32 FirstMessageDelay

- DateTime InstallDate

- True IsSwitchingSupply

- UInt32 LastErrorCode

- True LowBatterySignal

- UInt32 MessageInterval

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- True PowerFailSignal

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt32 Range1InputFrequencyHigh

- UInt32 Range1InputFrequencyLow

- UInt32 Range1InputVoltageHigh

- UInt32 Range1InputVoltageLow

- UInt32 Range2InputFrequencyHigh

- UInt32 Range2InputFrequencyLow

- UInt32 Range2InputVoltageHigh

- UInt32 Range2InputVoltageLow

- UInt16 RemainingCapacityStatus

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- UInt32 TimeOnBackup

- UInt32 TotalOutputPower

- UInt16 TypeOfRangeSwitching

- Tekenreeksexpressie Upsport



## <a name="usb-controller"></a>USB-controller

Naam ruimte: root\cimv2

klasse Win32_USBController


- Tekenreeksexpressie DeviceID

- UInt16 Availability

- Tekenreeksexpressie Kop

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie Beschrijvingen

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Tekenreeksexpressie Fabricage

- UInt32 MaxNumberControlled

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt16 ProtocolSupported

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- DateTime TimeOfLastReset



## <a name="usb-device"></a>USB-apparaat

Naam ruimte: root\cimv2

klasse Win32_USBDevice


- Tekenreeksexpressie DeviceID

- Tekenreeksexpressie Kop

- Tekenreeksexpressie ClassGuid

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie CreationClassName

- Tekenreeksexpressie Beschrijvingen

- Tekenreeksexpressie Fabricage

- Tekenreeksexpressie Naam

- Tekenreeksexpressie PNPDeviceID

- Tekenreeksexpressie Service

- Tekenreeksexpressie Hebben

- Tekenreeksexpressie SystemCreationClassName

- Tekenreeksexpressie Systemnaam



## <a name="usm-user-profile"></a>EIGENSCHAPPEN van-gebruikers profiel

Naam ruimte: root\cimv2

klasse Win32_UserProfile


- Tekenreeksexpressie GEVAL

- (UInt8) HealthStatus

- Tekenreeksexpressie LastAttemptedProfileDownloadTime

- Tekenreeksexpressie LastAttemptedProfileUploadTime

- Tekenreeksexpressie LastBackgroundRegistryUploadTime

- DateTime LastDownloadTime

- DateTime LastUploadTime

- DateTime LastUseTime

- True Waren

- Tekenreeksexpressie LocalPath

- UInt32 Stance

- True RoamingConfigured

- Tekenreeksexpressie RoamingPath

- True RoamingPreference

- True Specifiek

- UInt32 Hebben



## <a name="video-controller"></a>Video controller

Naam ruimte: root\cimv2

klasse Win32_VideoController


- Tekenreeksexpressie DeviceID

- UInt16 AcceleratorCapabilities[]

- Tekenreeksexpressie AdapterCompatibility

- Tekenreeksexpressie AdapterDACType

- UInt32 AdapterRAM

- UInt16 Availability

- Tekenreeksexpressie CapabilityDescriptions[]

- Tekenreeksexpressie Kop

- UInt32 ColorTableEntries

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- UInt32 CurrentBitsPerPixel

- UInt32 CurrentHorizontalResolution

- UInt64 CurrentNumberOfColors

- UInt32 CurrentNumberOfColumns

- UInt32 CurrentNumberOfRows

- UInt32 CurrentRefreshRate

- UInt16 CurrentScanMode

- UInt32 CurrentVerticalResolution

- Tekenreeksexpressie Beschrijvingen

- UInt32 DeviceSpecificPens

- UInt32 DitherType

- DateTime DriverDate

- Tekenreeksexpressie DriverVersion

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- UInt32 ICMIntent

- UInt32 ICMMethod

- Tekenreeksexpressie InfFilename

- Tekenreeksexpressie InfSection

- DateTime InstallDate

- Tekenreeksexpressie InstalledDisplayDrivers

- UInt32 LastErrorCode

- UInt32 MaxMemorySupported

- UInt32 MaxNumberControlled

- UInt32 MaxRefreshRate

- UInt32 MinRefreshRate

- True Afdrukken

- Tekenreeksexpressie Naam

- UInt16 NumberOfColorPlanes

- UInt32 NumberOfVideoPages

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- UInt16 ProtocolSupported

- UInt32 ReservedSystemPaletteEntries

- UInt32 SpecificationVersion

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- Tekenreeksexpressie Systemnaam

- UInt32 SystemPaletteEntries

- DateTime TimeOfLastReset

- UInt16 VideoArchitecture

- UInt16 VideoMemoryType

- UInt16 VideoMode

- Tekenreeksexpressie VideoModeDescription

- Tekenreeksexpressie VideoProcessor



## <a name="virtual-application-packages"></a>Virtuele toepassings pakketten

Naam ruimte: root\Microsoft\appvirt\client

Class-pakket


- Tekenreeksexpressie PackageGUID

- UInt64 CachedLaunchSize

- UInt16 CachedPercentage

- UInt64 CachedSize

- UInt64 LaunchSize

- Tekenreeksexpressie Naam

- Tekenreeksexpressie SftPath

- UInt64 TotalSize

- Tekenreeksexpressie Versie

- Tekenreeksexpressie VersionGUID



## <a name="virtual-applications"></a>Virtuele toepassingen

Naam ruimte: root\Microsoft\appvirt\client

klasse-toepassing


- Tekenreeksexpressie Naam

- Tekenreeksexpressie Versie

- Tekenreeksexpressie CachedOsdPath

- UInt32 GlobalRunningCount

- DateTime LastLaunchOnSystem

- True Van

- Tekenreeksexpressie OriginalOsdPath

- Tekenreeksexpressie PackageGUID



## <a name="virtual-machine-64"></a>Virtuele machine (64)

Naam ruimte: root\cimv2

klasse Win32Reg_SMSGuestVirtualMachine64


- Tekenreeksexpressie InstanceKey

- Tekenreeksexpressie PhysicalHostName

- Tekenreeksexpressie PhysicalHostNameFullyQualified



## <a name="virtual-machine"></a>Virtuele machine

Naam ruimte: root\cimv2

klasse Win32Reg_SMSGuestVirtualMachine


- Tekenreeksexpressie InstanceKey

- Tekenreeksexpressie PhysicalHostName

- Tekenreeksexpressie PhysicalHostNameFullyQualified



## <a name="virtual-machine-details"></a>Details van de virtuele machine

Naam ruimte: root\vm\VirtualServer

klasse VirtualMachine


- Tekenreeksexpressie Naam

- UInt32 CpuUtilization

- UInt64 DiskBytesRead

- UInt64 DiskBytesWritten

- UInt64 DiskSpaceUsed

- UInt64 HeartbeatCount

- UInt32 HeartbeatInterval

- UInt32 HeartbeatPercentage

- UInt32 HeartbeatRate

- UInt64 NetworkBytesReceived

- UInt64 NetworkBytesSent

- UInt64 PhysicalMemoryAllocated

- UInt32 Systeem



## <a name="volume"></a>Volume

Naam ruimte: root\cimv2

klasse Win32_Volume


- Tekenreeksexpressie DeviceID

- UInt16 Access

- True Automount

- UInt16 Availability

- UInt64 Blok

- UInt64 Capaciteit

- Tekenreeksexpressie Kop

- True Eerst

- UInt32 ConfigManagerErrorCode

- True ConfigManagerUserConfig

- Tekenreeksexpressie CreationClassName

- Tekenreeksexpressie Beschrijvingen

- True DirtyBitSet

- Tekenreeksexpressie Stationsaanduiding

- UInt32 DriveType

- True ErrorCleared

- Tekenreeksexpressie ErrorDescription

- Tekenreeksexpressie ErrorMethodology

- Tekenreeksexpressie System

- UInt64 Frees Pace

- True IndexingEnabled

- DateTime InstallDate

- Tekenreeksexpressie Adres

- UInt32 LastErrorCode

- UInt32 MaximumFileNameLength

- Tekenreeksexpressie Naam

- UInt64 NumberOfBlocks

- Tekenreeksexpressie PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- True PowerManagementSupported

- Tekenreeksexpressie Doel

- True QuotasEnabled

- True QuotasIncomplete

- True QuotasRebuilding

- UInt32 SerialNumber

- Tekenreeksexpressie Hebben

- UInt16 StatusInfo

- True SupportsDiskQuotas

- True SupportsFileBasedCompression

- Tekenreeksexpressie SystemCreationClassName

- Tekenreeksexpressie Systemnaam



## <a name="ccm_webappinstallinfo"></a>CCM_WebAppInstallInfo

Naam ruimte: root\ccm\cimodels

klasse CCM_WebAppInstallInfo


- Tekenreeksexpressie AppDeliveryTypeId

- UInt32 AppDtRevision

- Tekenreeksexpressie TargetURL

- Tekenreeksexpressie UserSID

- Tekenreeksexpressie URLFileName

- Tekenreeksexpressie URLPath



## <a name="sms_windows8application"></a>SMS_Windows8Application

Naam ruimte: root\cimv2\sms

klasse SMS_Windows8Application


- Tekenreeksexpressie Juiste

- Tekenreeksexpressie ApplicationName

- Tekenreeksexpressie Opstelling

- True ConfigMgrManaged

- Tekenreeksexpressie DependencyApplicationNames

- Tekenreeksexpressie FamilyName

- Tekenreeksexpressie InstalledLocation

- True IsFramework

- Tekenreeksexpressie Uitgever

- Tekenreeksexpressie PublisherId

- Tekenreeksexpressie Versie



## <a name="sms_windows8applicationuserinfo"></a>SMS_Windows8ApplicationUserInfo

Naam ruimte: root\cimv2\sms

klasse SMS_Windows8ApplicationUserInfo


- Tekenreeksexpressie Juiste

- Tekenreeksexpressie UserSecurityId

- Tekenreeksexpressie InstallState

- Tekenreeksexpressie UserAccountName



## <a name="windows-update"></a>Windows Update

Naam ruimte: root\cimv2

klasse Win32Reg_SMSWindowsUpdate


- Tekenreeksexpressie InstanceKey

- UInt32 AUOptions

- UInt32 NoAutoUpdate

- UInt32 UseWUServer



## <a name="windows-update-agent-version"></a>Versie van Windows Update Agent

Naam ruimte: root\cimv2\sms

klasse Win32_WindowsUpdateAgentVersion


- Tekenreeksexpressie Versie



## <a name="write-filter-state"></a>Status van schrijf filter

Naam ruimte: root\cimv2\sms

klasse CCM_WriteFilterState


- True WriteFilterEnabled

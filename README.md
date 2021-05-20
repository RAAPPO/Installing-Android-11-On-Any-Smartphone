# Installing-Android-11-On-Any-Smartphone
 INSTALL ANDROID 11 R IN ANY SMARTPHONE FOR FREE WITHOUT DATA LOSS
THIS PROJECT IS AN INITIATIVE TO TURN A OLD SMARTPHONE WHICH DOES NOT GET ANY OS UPDATE DUE TO THE PRIVACY POLICY OF SMARTPHONE COMPANIES
PLEASE SUPPORT THIS PROJECT

For more detailed view you can visit our website
www.techiehera.epizy.com


Android 11 release notes

This page summarizes the major features in the Android 11 release, and provides links to additional information. These feature summaries are organized according to the feature's documentation location on this site.
Architecture
API quotas

The Android 11 release introduces the API quotas feature, which limits how often apps can call certain APIs. It's implemented only in JobScheduler API calls. Any changes you make to the preset limits must still pass CTS testing. You can disable and enable API quotas using the setEnabled method in QuotaTracker.java. The default is enabled. Disabling the feature allows apps to call the affected APIs without limitation.

Unit tests for QuotaTracker and associated classes are provided. Detailed documentation is in the comments in the QuotaTracker class. This feature introduces the new LimitExceededException public API.
Bootloader
Boot header version 3

Android 11 supports boot header version 3. For details, see Boot image Header.
Partitions
Boot partitions

Android 11 introduces the concept of the Generic Kernel Image. To enable easily booting an arbitrary device with a Generic Kernel Image, all vendor-specific information is factored out of the boot partition and relocated into a vendor-boot-partition. A device launching with Android 11 must support the vendor-boot partition and updated boot partition format to pass testing with the GKI.
Vendor boot header

The Vendor boot header can be more than one page.
Product partition interfaces enforcement

Android 11 unbundles the product partition, making it independent of the system and vendor partitions. As part of these changes, you can now control the product partition’s access to native and Java interfaces.
Recovery images

Android 11 updates the recovery image requirements and includes new release-based options for including a recovery DTBO/ACPIO as part of the boot/recovery image. For details, see Recovery images. 
Soft restarts

Android 11 supports Soft restarts , which are runtime restarts of processes in the user space used to apply updates that require a reboot (for example, updates to APEX packages).
Kernel
Android common kernels

Android 11 introduces significant changes to how Android common kernels are developed and integerated. 
Android kernel ABI Monitoring

Android 11 introduces ABI Monitoring tooling to stabilize the in-kernel ABI of Android kernels.
Generic Kernel Image

Android 11 introduces the Generic Kernel image (GKI) , which addresses kernel fragmentation by unifying the core kernel and moving SoC and board support out of the core kernel into loadable modules.
Modular kernels
Kernel Module support

A Generic Kernel Image (GKI) may not contain the required driver support to enable a device to mount partitions. To enable a device to mount partitions and to continue booting, first-stage init is enhanced to Load the kerenel modules present on ramdisk . The ramdisk is split into generic and vendor ramdisks. Vendor kernel modules are stored in the vendor ramdisk. The order in which kernel modules are loaded is configurable.
DebugFS

Android 11 removes platform support for debugFS and requires that it not be mounted or accessed on production devices. While DebugFS was created for debugging purposes, it has been included in user and usedebug builds for generic and vendor-specific components. DebugFS is being deprecated because it creates:

    Unstable and undocumented API. Android depends on well-defined and stable Linux kernel interfaces and HALs to function correctly. VTS tests enforce the presence and correctness of these interfaces. DebugFS can't be enforced because its ABI is neither stable nor documented.

    Poor code quality. Because they are for debugging, nodes added to debugfs aren't reviewed and tested as rigorously as those in other file systems. When bugs are discovered in debugfs, they are treated as less of a priority, which contributes to security vulnerabilities that originate from debugfs.

    Security vulnerabilities. DebugFS was created with the intention of helping kernel developers debug the system and not with a focus on security.Currently, there is no efficient method to verify that all DebugFS nodes exposed on a production device are secure. Although SEpolicy tightening has reduced the severity of security vulnerabilities originating from debugfs, disallowing mounting debugfs is the only way to completely eliminate the attack surface.

In Android 11, VTS enforces that CONFIG_DEBUG_FS isn't enabled in the device’s kernel config and debugfs isn't listed under /proc/filesystems.
ION heaps for GKI

In Android 11, the Android Common Kernel v5.4 introduces a framework for modularizing vendor specific ION heaps while keeping the core ION driver built in, enabling OEMs to retain ION kernel driver modifications when using the Generic Kernel Image (GKI).
Modular system components
Auto Revoke Permissions

In Android 11, the Permissions control module can automatically revoke runtime permissions for apps that haven't been used for an extended period of time.
Mainline module updates

Android 11 introduces several new modules and updates several existing modules that were introduced in Android 10.
Runtime resource overlays

Android 11 or higher supports a new mechanism for RROs Enhancements include reserved resource ID space, a res/xml/overlays.xml file for enumerating target resources, a Soong build rule for overlays, an OverlayConfig file for configuring the mutability, default state, and priority of overlays.
Vendor NDK
Vendor snapshots

Android 11 supports VNDK snapshot build artifacts and vendor snapshot, which you can use to build vendor.img regardless of the Android version on the source tree. This enables mixed versions of images, such as an older vendor and a newer system image.
Audio
Audio capture from FM tuner requires a privileged permission

In Android 11, audio source MediaRecorder.AudioSource.RADIO_TUNER is visible as @SystemApi and using it when capturing audio with an AudioRecord or MediaRecorder requires privileged permission android.permission.CAPTURE_AUDIO_OUTPUT
Audio effects

Starting in Android 11, the device manufacturers have the ability to automatically attach and enable specific audio effects when a given audio device is selected for audio capture or playback.
Device type limit

In Android 11, we have removed the limit on the number of audio device types to allow new audio device types to be added.
Implementation
Audio implementation

Android 11 features stricter enforcement of sound trigger HAL implementations at runtime than lower versions.
Automotive
Release details

To learn about new Automotive features and enhancements, see Automotive release details.
USB Port Reset API

Device manufacturers can implement the USB Port reset API in Android 11 to reset the USB gadget connection with connected hosts.
Camera
Camera bokeh

Starting in Android 11, the Android platform supports camera bokeh implementation and provides APIs to make the bokeh feature available to third-party apps.
Camera zoom

In Android 11, an app can use a camera's zoom (digital and optical) through the ANDROID_CONTROL_ZOOM_RATIO setting. This setting is a floating point factor that allows for better precision for zoom as compared to using integer values with the ANDROID_SCALER_CROP_REGION setting and it allows for zooming out (< 1.0f).
Concurrent camera streaming

Starting in Android 11, the Camera2 API includes methods that app can call to determine if the cameras support concurrent streaming and which stream configurations are supported.
Improved camera support for Android virtual devices

Android 11 introduces a revamped emulated Camera HAL implementation on cuttlefish and Android Emulator virtual devices that adds support for more camera features including:

    RAW capture
    YUV reprocessing
    Level 3 devices
    Logical camera support
    Depth only camera support

This emulated camera HAL can be found at /platform/hardware/google/camera/devices/EmulatedCamera/hwl.
Multi-camera best practices

To fully take advantage of features enabled by multi-camera while maintaining app compatibility, follow these best practices when implementing a logical multi-camera device. This includes best practices on using the ANDROID_CONTROL_ZOOM_RATIO API introduced in Android 11.
System cameras

Android 11 introduces support for system cameras through the android.permission.SYSTEM_CAMERA permission. System cameras allow you to implement camera features that can be used on privileged or system apps but aren't available to third-party public apps.
Compatibility

The Android ccompatiblity definition document iterates upon previous versions with updates for new features and changes to requirements for previously released functionality.
Connectivity
Bluetooth and NFC
NFC off-host payment synchronization

Android supports NFC card emulation with a secure element for off-host card emulation but it's possible that the preferred payment service specified in the Tap & pay setting isn't synchronized with the app in the secure element.

Android 11 addresses this issue with off-host payment synchronization, a mechanism that allows you to synchronize the payment configuration in Tap & pay, the routing configuration on the contactless front-end (CLF), and the app-selected state in the secure element.
Quick Access Wallet

The Quick access wallet feature allows the user to access payment cards and relevant passes directly from the power menu.
Calling and messaging
Emergency call behavior

Android 11 introduces changes to how emergency calls are handled to better support carrier requirements. The behavior for handling emergency calls is described below:

    When a user places an emergency call while on an ongoing call, depending on how the KEY_ALLOW_HOLD_ON_DURING_EMERGENCY_BOOL key is set, the device automatically disconnects the ongoing call or places the ongoing call on hold and disallows swapping back to the ongoing call until the emergency call is disconnected.
    During an emergency call, incoming calls are automatically rejected and are displayed as missed calls to the user. During an active emergency call, outgoing nonemergency calls can't be placed.
    In emergency callback mode, placing a nonemergency call causes the device to exit emergency callback mode. If an emergency call is placed, the device re-enters emergency callback mode when the call ends. Incoming calls don't cause the device to exit emergency callback mode.
    Active emergency calls can't be swapped or held.

Updatable emergency number database

Android 11 introduces an emergency database that can be updated through OTA updates. The database contains a list of emergency phone numbers with corresponding countries and service categories.
Carrier
eSIM
eSIM activation flow through carrier app

Android 11 improves the process of activating an eSIM profile through a carrier app. When using an activation code to download a profile, the LPA can launch the carrier app's user interface to retrieve additional information from the user. The carrier app can also launch the LUI to activate an eSIM profile.
eUICC API error handling

Android 11 introduces additional keys and values to improve error handling by allowing the caller of the eUICC API to handle specific errors individually.
Option parameter for the erase subscriptions method

Starting from Android 11, when using the eraseSubscriptions method in EuiccManager, you should provide an EuiccCardManager#ResetOptionenum value to specify whether to erase all test, operational, or both types of subscriptions.
Multi-operator network support

Devices launching with Android 11 can provide support for multiple public land mobile networks (PLMNs). Multi-PLMN support provides flexibility to mobile network operators (MNOs) by allowing them to broadcast multiple identities.
Small cell support

Devices launched with Android 11 can provide support for closed subscriber groups (CSGs) through methods in the cell identification APIs that get information about a cell's CSG information. This is useful for mobile network operators (MNOs) that manage small cells through closed subscriber groups.
Connectivity Diagnostics API

The Connectivity Diagnostics API allows apps that own or manage networks, such as carrier apps, VPN apps, and Wi-Fi suggestion apps, to receive diagnostic network connectivity information from the framework.
Open Mobile API changes

Android 11 introduces additional functionality for Open Mobile API (OMAPI):

    Parsing rules for carrier privileges.

    Customizing embedded Secure Element (eSE) access or provision an eSE using one or more of the following:
        SECURE_ELEMENT_PRIVILEGED_OPERATION system privileged permission
        Configurable access rule application master (ARA-M) application identifiers (AIDs)
        reset system API to reset OMAPI reader

    Providing readers a clear indicator for apps to filter device capabilities.

Signal strength reporting

In Android 11, you can select and customize multiple signal measurement types for the framework to use to report the signal strength of 4G LTE and 5G NR radio access networks (RANs). You can then use the reported signal strengths to control how signal bars are displayed on your devices.
Wi-Fi
Carrier Wi-Fi network configurations

In Android 11, you can use the Wi-Fi suggestion API to add carrier Wi-Fi network configurations instead of configuring the carrier_wifi_string_array parameter in the carrier config manager.
Wi-Fi hotspot (soft AP) support for tethering

Android 11 introduces improved Wi-Fi hotspot (soft AP) configuration, providing more support for carrier use cases and customizations. These changes let device manufacturers configure the following:

    SSID and BSSID
    Security type (including WPA3)
    Hidden SSID
    Operating band and channel (including ACS)
    Maximum number of allowed clients
    Autoshutdown timeout value
    Allowlist and blocklist to allow user control of associated devices

Wi-Fi network selection enhancements

Android 11 introduces enhancements to Wi-Fi network selection to improve Wi-Fi network connectivity.
Wi-Fi Passpoint enhancements

Android 11 introduces the following enhancements to the Passpoint feature:

    Profile expiration support allowing the system to notify the user and enforce profile expiration dates. This requires a profile with the SubscriptionParameters/ExpirationDate field initialized.
    Support for private, self-signed CA certificates for Passpoint R1 profiles.
    Support for Passpoint R1 profiles with no CA certificate. The system uses the default trust store to authenticate the connection.
    Support for configuring a named AAA domain separately from ANQP FQDN (using the Extension/Android node in PPS-MO). This allows you to specify an AAA domain that is different from the advertised domain without compromising connection security.
    Support for multiple installed Passpoint configurations with the same FQDN. This is useful for carriers that deploy more than one combination of mobile country code (MCC) and mobile network code (MNC) on their network, but has only a single FQDN.
    Ability to detect and accept Passpoint R3 access points.
    Improved network matching:
        Supports home provider matching for HomeSP/HomeOIList.
        Supports home provider matching for HomeSP/OtherHomePartners.
        Removes EAP method matching requirement that isn't required by the Passpoint specification.

Wi-Fi profiles improved common name support

In Android 11, Wi-Fi profiles remain valid when a root certificate authority (CA) of a carrier changes if the common name is specified in the optional Android extension subtree. In previous versions, users must download a new profile from the carrier if the root CA changes.
WPA3 password identifier

Android 11 introduces support for the password identifier feature in Wi-Fi Protected Access 3 (WPA3). To support the feature, you must implement supplicant HAL 1.3.
Data
Data access auditing

Android 11 introduces data access auditing, allowing app developers to better identify how their apps and dependencies access private data (such as location and camera data) from users. For complex, multipurpose apps, developers can define attribution tags to identify different parts of the app.

For more information, see Data access auditing.
Display
Bubbles notification API updates

Android 10 introduced the Bubbles notification API, which let users easily multi-task from anywhere on their device. Android 11 includes several Bubbles enhancements. The most notable changes are turning Bubbles on by default and moving the settings out of developer options. No work is required to implement Bubbles in the Android platform.
Device Controls

The Device Controls feature, available starting in Android 11, allows the user to quickly view and control external devices such as lights, thermostats, and cameras from the Android power menu. Device aggregators (for example, Google Home) and third-party vendor apps can provide devices for display in this space. No platform implementation work is required to support this feature. The default implementation is included in the AOSP System UI. For information about adding support for device controls to your control app, see the Control external devices Android developers page.
Text classifier updates

Android 11 introduces an updatable default implementation of the text classifier service that is in the ExtServices Mainline module. Device manufacturers are recommended to use this implementation of TextClassifierService as it can be updated through Mainline OTA updates.
Enterprise
Work profile improvements

Android 11 contains privacy and usability enhancements for work profiles, designed to address key usability challenges. It's crucial that these improvements are implemented consistently across the ecosystem.

IT administrators who support Android must support the experience on any Android device their users bring to work. Improving UX consistency of critical workflows significantly decreases the cost of supporting Android in BYOD environments. Consistent implementation of privacy features across devices also increases user confidence. Some updates include:

    The apps list has separate tabs labeled Personal and Work.
    The work tab has a toggle to turn off work profile.
    When the work profile is turned off, work app icons turn gray and an overlay on the work tab says that Work apps are paused.

Interaction
Context Hub Runtime Environment updates

Android 11 introduces CHRE API v1.4, which includes support for 5G cell information, nanoapp debug dump, and other improvements. It also includes support for using TensorFlow Lite for Microcontrollers in nanoapps. For more information, see Context Hub Runtime Environment (CHRE).
Haptics

Android 11 includes a new guide about implementing haptics and assessing haptics performance on your device.
Input
Gamepads

Android 11 adds support for third party gaming controllers including:

    Nintendo Switch Pro controller: Android adds support for both USB and Bluetooth connectivity for the Nintendo Switch Pro controller. CTS testing is required for all implementations, use NintendoSwitchProTest to validate your implementation.

    Steam controller: Android adds USB connectivity for the Steam controller.

Neural Networks
Best Practices

To encourage adoption of the NNAPI by app developers, follow these best practices when implementing an NNAPI driver on devices running Android 11.
Control flow

In Android 11, the NNAPI adds two control flow operations, IF and WHILE, that take other models as arguments and execute them conditionally (IF) or repeatedly (WHILE). This allows for constructing models that execute different operations based on the input values or execute operations multiple times without unrolling.
Fenced executions

In Android 11, NNAPI allows executions to wait for a list of sync_fence handles and optionally return a sync_fence object, which is signaled when the execution is completed. This reduces overhead for small sequence models and streaming use cases. Fenced execution also allows for more efficient interoperability with other components that can signal or wait for sync_fence.
Memory domains

For devices running Android 11 or higher, NNAPI supports memory domains that provide allocator interfaces for driver-managed buffers. This allows for passing device native memories across executions, suppressing unnecessary data copying and transformation between consecutive executions on the same driver.
Quality of service

Starting in Android 11, the NNAPI offers improved quality of service (QoS) by allowing an app to indicate the relative priorities of its models, the maximum amount of time expected for a model to be prepared, and the maximum amount of time expected for an execution to be completed.
Signed 8-bit quantization

The Neural Network HAL (NN HAL) 1.3, introduced in Android 11, supports signed 8-bit quantization for the Neural Networks API. For more information, see NN HAL updates in Android 11.
Testing improvements

Android 11 includes a testing utility to perform fuzz testing on NNAPI driver implementations and a series of crash tests to validate the resilience of drivers under heavy usage conditions.

For more information, see:

    Fuzz testing
    Stress testing

Sensors
Hinge angle sensor type

Android 11 introduces a hinge angle sensor type to represent a sensor that measures the angle between two integral parts of a device.
Sensors Multi-HAL 2.1

Sensors Multi-HAL 2.1, available on Android 11, is an iteration of Sensors Multi-HAL 2.0, which supports loading sub-HALs that can expose the hinge angle sensor type. To support this sensor type, sub-HALs must use the sub-HAL APIs defined in the 2.1 SubHal header.
Media
DRM

Android 11 simplifies the MediaDrm/Crypto IPC path through MediaDrmService removal. A new MediaDrm API is added to enumerate available DRM plugins.
Low latency decoding in MediaCodec

Android 11 includes MediaCodec 2.0 to enable media decoding with low latency, which is critical for real-time apps.
Miscellaneous
Update to AOSP Gallery app requirements

Starting in Android 11, the AOSP Gallery app isn't required to support the application/sdp MIME type for the ACTION_VIEW intent. The ACTION_VIEW intent filter for the application/sdp MIME type has been removed from the AOSP Gallery app manifest file.

These requirements are documented in section 3.2.3.1. Core Application Intents of the CDD.
Performance
Userspace lmkd

Android 11 introduces a new killing strategy to prevent memory starvation and performance degradation.
Power
Inattentive sleep for TV standby

In Android 11, a new feature called inattentive sleep is added for TV standby. It's a power-saving feature that allows a user inactivity timeout to be set after which the device goes to sleep, even if wakelocks are held.
Secure
OEMCrypto

Android 11 supports OEMCrypto API version 16.
Storage
Scoped storage

Android 11 supports scoped storage, which limits app access to external storage. In addition, MediaProvider becomes the file system handler (for FUSE) for external storage, making the file system on external storage and the MediaProvider database consistent.
SDCardFS Deprecation

SDCardFS support is deprecated in Android 11. VTS testing doesn't allow mounted file systems listed as SDCardFS. SDCardFS's functions are replaced by other methods.
Tests
Compatibility Test Suite (CTS)

For Android 11, many new key modules and test changes are introduced for CTS. See CTS Release Notes for more information.
CTS tests for APEX management APIs

Starting with Android 11, the CtsShimApex package contains two prebuilt apps that CTS uses to test privileges and permissions.

If your device doesn't support APEX package management or if the device is running version 10 or lower, the two prebuilt apps must be preinstalled in the system separately.

For more details, see CTS shim packages.
CTS Release Notes

Android 11 introduces many new key modules and test changes.
Debugging
Scoped vendor logging

Android 11 adds a new HAL, IDumpstateDevice (version 1.1). This HAL exposes new methods to more tightly scope vendor logs that are included in standard bug reports, as well as to allow user builds to turn vendor logging on and off (the default for user builds is off). This gives OEMs more control over what gets included in particular types of bug reports.
GWP-ASan: heap corruption detection

GWP-ASan is a native memory allocator feature that helps find use-after-free and heap-buffer-overflow bugs in both 32- and 64-bit processes.

GWP-ASan is automatically enabled in Android 11 for system applications and platform executables. Please do not disable it in the platform, and enable it in your apps.
Updates
Dynamic System Update (DSU) Enhancements

Android 10 includes enhancements to Dynamic System Updates (DSU), including:

    A new frontend, the one-click DSU loader
    Support for multiple-partition DSUs
    OEM-signed DSUs, for enhanced security
    New ways to manage compatibility between DSUs and devices

OTA packages for multiple SKUs

Android 11 or higher supports using a single OTA package for multiple devices with different SKUs. Doing so requires configuring the target devices to use dynamic fingerprints and updating the OTA metadata (using OTA tools) to include the device name and fingerprint in the pre and post condition entries.
Signing builds for release

Several CLI commands for signing builds for release are changed in Android 11.
Vendor Test Suite (VTS) 11

Android 11 Vendor Test Suite (VTS) provides extensive testing on the kernel and the hardware abstraction layer (HAL).
Virtual A/B

Android 11 unifies A/B updates and non-A/B updates by providing virtual A/B. Virtual A/B brings seamless updates to devices while minimizing the cost of storage.
Testing
Scudo heap allocator by default

Starting in Android 11, the scudo heap allocator is used for for all native code (except on low-memory devices, where jemalloc is still used). So you no longer need to enable scudo on a per-binary basis. For more information about scudo, see the Scudo page.
TV
CAS framework

Android 11 supports Media conditional access systems (Media CAS) framework for Android TV, which provides standard Java APIs for third-party developers and OEMs. See CAS Framework for more details.
Multimedia tunneling

For Android 11, users can implement multimedia tunneling with audio and video content directly fed from Tuner.
Tuner framework

Android 11 supports Tuner Framework for Android TV, which delivers A/V content using Tuner HAL, Tuner SDK API, and Tuner Resource Manager.
TV Input Framework

The Android TV Input Framework (TIF) simplifies delivery of live content to Android TV, providing a standard API for manufacturers to create input modules for controlling Android TV, and enabling live TV search and recommendations. Android 11 introduces three new components to TIF.


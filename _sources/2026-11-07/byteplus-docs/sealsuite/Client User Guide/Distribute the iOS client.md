---
title: "Distribute the iOS client"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/distribute-ios-client"
---

This article is intended for enterprise IT administrators and application release owners. It describes distribution and version updates for the SealSuite custom iOS client. Select the initial distribution or version update procedure based on the distribution method your enterprise uses. For employees who need to download and install the standard client, see [Download the SealSuite client](https://docs.byteplus.com/en/docs/sealsuite/downloding-the-sealsuite-client).

## Choose a distribution method

Select App Store unlisted distribution or enterprise internal distribution based on your enterprise account qualifications and distribution requirements. The installation entry points and version update procedures are as follows.

|Distribution method |Applicable scenario |Employee installation method |Version update method |
|---|---|---|---|
|App Store unlisted distribution |Distribute a custom app through the official Apple store. The app does not appear in search results. |Download and install the app through the unified download link [CorpSuite](https://apps.apple.com/us/app/corpsuite/id6760535092) provided by SealSuite. |SealSuite publishes new versions, and employees update the app through the App Store. |
|Enterprise internal distribution |Use an enterprise distribution certificate to provide the custom app to employees in your enterprise. |Install the app through an installation link or QR code provided by the enterprise. |Update the signed package, installation manifest, and related upgrade configurations. App Store publishing is not required. |

SealSuite is responsible for publishing the app for App Store unlisted distribution and providing a unified download link. Enterprise internal distribution requires the corresponding enterprise developer qualifications, enterprise distribution certificate, and provisioning profiles. Enterprise internal distribution uses the enterprise's own signing materials.

## App Store unlisted distribution

SealSuite is responsible for publishing the client for unlisted distribution. Enterprises and employees use the unified download link [CorpSuite](https://apps.apple.com/us/app/corpsuite/id6760535092). The app does not appear in App Store search results.

### Initial distribution

Enterprise IT Administrators can provide the unified download link to employees. Employees install the client through the App Store.

1. Open the unified download link provided by SealSuite: [CorpSuite](https://apps.apple.com/us/app/corpsuite/id6760535092).

2. Download and install the client on a test device, then verify enterprise login and required features.

3. After verification is complete, provide the link to employees for download and installation.

### Update the version

SealSuite is responsible for publishing new versions. The enterprise continues to use the unified download link described above.

1. After a new version is available, update the client through the App Store on a test device.

2. Verify enterprise login and required features, then notify employees to update through the App Store.

## Enterprise internal distribution

With enterprise internal distribution, the enterprise hosts the installation package and provides an installation entry point to its employees. Initial distribution requires creating a download entry point. Subsequent updates require maintaining the installation package, manifest, and upgrade configurations.

### Initial distribution

Initial distribution requires preparing an installation package with a valid enterprise signature, uploading it to the enterprise server, and generating a link for employees to install the app.

#### Prepare custom materials

The customer must provide basic app information and visual assets before building the custom package. Before submission, check naming, dimensions, and usage consistently to prevent noncompliant assets from affecting the build or review.

|Material |Description |Example or requirement |
|---|---|---|
|Chinese name |App name displayed when the system language is Chinese. |飞连 |
|English name |App name displayed when the system language is English. It can be configured based on enterprise requirements. |SealSuite |
|Bundle ID |Unique identifier of the iOS app. It must match the certificate and provisioning profile. |`com.example.app` |
|Enterprise identifier |Used to identify the enterprise tenant or enterprise configuration. |Enterprise\-defined identifier |
|Portal domain name |Enterprise access entry domain name. Ensure that the format and port are correct. |`https://example.com:443` |
|App icon |Used for display in the App Store and on the device home screen. |1024 × 1024 px, square with no rounded corners |
|Splash screen assets |Used for the client launch page. They can be customized based on the enterprise brand. |Prepare assets according to the dimension specifications provided by SealSuite |
|App screenshots |Used for display on the App Store app details page. |Upload according to current App Store Connect device size requirements |

#### Prepare the installation package and complete signing

Confirm enterprise customization requirements with SealSuite. SealSuite provides the IPA package to be distributed. The enterprise prepares its own enterprise distribution certificate, private key, and provisioning profiles. When building a custom package for the first time, refer to "Prepare custom materials" in this section for material requirements.

After receiving the package to be re\-signed, generate an IPA package for enterprise internal distribution according to "Re\-signing operation reference" below. If the installation package has been correctly signed with valid signing materials for the corresponding enterprise, proceed directly with subsequent distribution.

#### Upload the installation package and generate an installation link

Upload the re\-signed IPA package to the enterprise file server or CDN, and generate an HTTPS\-accessible download URL. Then generate a plist file based on information such as the IPA download URL, app version number, and Bundle ID.

The plist file must also be uploaded to an HTTPS\-accessible location. After obtaining the plist link, URL\-encode the link, and then generate an iOS installation link in the following format:

```Text
itms-services://?action=download-manifest&url={{URL-encoded plist URL}}
```

Users can open this link in Safari on an iPhone or iPad to complete installation. You can also generate a QR code from the link, and users can scan it with the system camera to install the app. After installing the app through the enterprise method, users must trust the corresponding enterprise developer certificate in iOS settings. The entry point is usually located in **Settings** \> **General** \> **VPN & Device Management** or **Settings** \> **General** \> **Device Management**.

First confirm that installation, enterprise login, and required features work correctly on a test device. Then provide the installation link or QR code to employees in your enterprise.

### Update the version

After obtaining the new custom package, update the signed package and installation manifest, then verify whether the old version can be upgraded properly. This process does not require App Store review.

1. Obtain the new custom package from SealSuite, and check the app identifier, enterprise configuration, and extension capabilities.

2. Check whether the enterprise distribution certificate and provisioning profiles are valid. Packages to be re\-signed must be signed again. If the certificate, provisioning profile, or extension capabilities change, update the corresponding signing materials.

3. Upload the new IPA package, and update the installation package URL, version number, Bundle ID, and other information in the plist file. Ensure that the information matches the actual installation package. If the plist URL changes, regenerate the installation link and QR code.

4. If the enterprise uses in\-client upgrade, update the corresponding upgrade configuration.

5. Verify update, login, and related features on a test device with the old version installed. Then provide the update entry point to employees.

Enterprise internal distribution does not require App Store review. Signing materials must remain valid, and the installation package and plist file must always be accessible by target devices.

## Re\-signing operation reference

Re\-signing uses the enterprise's own Apple distribution certificate and provisioning profiles to re\-sign the IPA package provided by SealSuite. Perform this operation after obtaining a package to be re\-signed or when signing materials must be replaced. Do not re\-sign packages that are already correctly signed and meet distribution requirements. After completion, return to the enterprise internal distribution process to continue.

### Prerequisites

Before re\-signing, prepare a macOS device and ensure that the system version is macOS 12 or later. The device must have an Xcode or xcodebuild environment for signing\-related operations.

The customer must also prepare an Apple distribution certificate, the certificate private key, and provisioning profiles. Provisioning profiles must match the app Bundle ID and extension capabilities. Otherwise, installation failure, unavailable extensions, or abnormal app startup may occur after re\-signing.

|File or environment |Purpose |Provider |
|---|---|---|
|IPA package to be re\-signed |Original installation package of the SealSuite custom iOS package. |SealSuite |
|Apple distribution certificate |Used for enterprise signing or distribution signing of iOS apps. |Customer |
|Certificate private key |Used together with the distribution certificate. It is usually exported as a `.p12` file. |Customer |
|Provisioning profile |Defines signing permissions and capabilities for the app and extensions. |Customer |
|macOS environment |Used to install certificates, run scripts, and complete re\-signing. |Customer |

### Provisioning profile requirements

If the app includes multiple extension capabilities, prepare provisioning profiles for the main project and each extension separately, and name them consistently as required by the script. If the enterprise does not need screen casting, the broadcast provisioning profile is not required.

|Module |Provisioning profile name |Description |
|---|---|---|
|Main project |`host.mobileprovision` |Provisioning profile for the main app. |
|Tunnel extension |`packettunnel.mobileprovision` |Used for network tunnel\-related capabilities. |
|Today extension |`today.mobileprovision` |Used for Today Extension. |
|Broadcast extension |`broadcast.mobileprovision` |Used for screen casting\-related capabilities. It is not required if screen casting is not used. |
|Widget extension |`widget.mobileprovision` |Used for home screen widget\-related capabilities. |

### Certificate installation and environment check

Use **Keychain Access** on macOS to install the Apple distribution certificate, and confirm that the certificate is trusted and available. If the certificate was created on another device, export a `.p12` file that contains the private key from the original device, and then import it to the re\-signing device.

If the certificate is untrusted after import, or the terminal reports that the certificate chain cannot be built, install the Apple Worldwide Developer Relations certificate. Obtain the latest certificate from the Apple certificate authority page: [Apple PKI - Apple](https://www.apple.com/certificateauthority/)

After installing the certificate, run the following command in the terminal to confirm that the Xcode command\-line environment is available:

```Bash
xcodebuild -usage
```

### Run re\-signing

Place the IPA package to be re\-signed, the re\-signing script, and the provisioning profiles in the same working directory, or record the directory that contains the provisioning profiles. Before running the script, confirm that the file names, certificate, provisioning profiles, and Bundle ID all match.

```Bash
./AutoResign.sh ${inputFilePath} ${provisionFilePath}
```

Here, `${inputFilePath}` is the path of the IPA package to be re\-signed, and `${provisionFilePath}` is the directory that contains the provisioning profiles. If the provisioning profiles and re\-signing script are in the same directory, you can omit this parameter as described in the script instructions.

> **Execution reminder**: Re\-signing failures are usually related to missing private keys in certificates, mismatches between provisioning profiles and Bundle IDs, expired provisioning profiles, or abnormal Xcode environments. Check the certificate chain, provisioning profile validity period, and whether all extension provisioning profiles are complete first.

## FAQ

The following describes common issues and solutions during distribution, re\-signing, and installation.

### Does an unlisted link app require Apple review?

Yes. SealSuite is responsible for app publishing and review. Enterprises and employees download and install the app through the unified link provided by SealSuite.

### Can users search for an unlisted link app?

No. Unlisted link apps do not appear in App Store search results, charts, categories, or recommendations. Users must open the download page through a link.

### Can the custom package be published as a public app?

This is not recommended. Custom packages are usually intended for specific enterprise scenarios. Public publishing may trigger review risks related to similar apps or duplicate apps. Use unlisted link distribution first.

### Why can a re\-signed enterprise package not be published directly as a public App Store app?

Enterprise\-signed packages are used for enterprise internal distribution and cannot be submitted directly as App Store distribution packages. For App Store unlisted distribution, use the unified download link [CorpSuite](https://apps.apple.com/us/app/corpsuite/id6760535092) published and provided by SealSuite.

### Does a missing broadcast provisioning profile affect re\-signing?

If the enterprise does not need screen casting, `broadcast.mobileprovision` is usually not required. If screen casting is required, the corresponding provisioning profile must be provided.

### What should I do if the installation link cannot be opened?

Confirm that both the IPA and plist files are accessible through HTTPS, that the plist link has been correctly URL\-encoded, and that Safari is used to open the itms\-services link. Built\-in WebViews in some browsers or chat apps may not trigger installation directly.

### What should I do if the app is shown as untrusted after installation?

Trust the corresponding enterprise developer certificate in iOS settings. If the certificate cannot be trusted, or the app still cannot be opened after trust is enabled, check the certificate status, signature validity, and installation package source.

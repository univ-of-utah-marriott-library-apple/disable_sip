# disable_sip
This script is used in the recovery partition to automatically disable SIP.
## Contents

* [Download](#download) - get the script
* [Contact](#contact) - how to reach us
* [Purpose](#purpose) - what is this script for?
* [Usage](#usage) - details of invocation

## Download

[Download the latest version of disable_sip here!](../../releases/)


## Contact

If you have any comments, questions, or other input, either [file an issue](../../issues) or [send an email to us](mailto:mlib-its-mac-github@lists.utah.edu). Thanks!

## Purpose
System Integrity Protection (SIP), sometimes referred to as rootless, is a security feature implemented in OS X El Capitan. It protects certain system processes, files and folders from being modified or tampered with by other processes even when executed by the root user or by a user with root privileges (sudo). Apple says that the root user can be a significant risk factor to the system’s security, especially on systems with a single user account on which that user is also the administrator. System Integrity Protection is enabled by default, but can be disabled.

Since we haven’t migrated completely to our new client management system, called Casper Suite, we decided to temporarily disable SIP since it conflicts with our current client management system called Radmind. Radmind operates as a tripwire with the ability to detect any modifications to the file system and reverse those changes to a known state. We also had hardware that required running the latest OS, OS X El Capitan that needed to be deployed.

We didn’t want to touch every system to disable or enable System Integrity Protection (SIP), so, we developed a automated method of disabling it during OS X El Capitan upgrade. This process will be discussed at this presentation.

## Usage
The bash script `SIPFix.sh` and the Launch Daemons Property List `edu.utah.scl.SIPFix.plist` are used to disable SIP in a modified recovery partition. 

The Recovery Partition is a disk image (dmg) that is stored in the Recovery HD partition on the main hard drive or in the OS X Installer Package. The `BaseSystem.dmg` is the disk image that the Recovery Partition uses to boot the system. For the Recovery HD,  `BaseSystem.dmg` can be found in the `com.apple.recovery.boot` folder. For the OS X Installer, it can be found in the `Contents/SharedSupport/InstallerESD.dmg` in the Installer Package. The disk image mounts as read-only. To customize the Recovery Partition to disable SIP during installation or each time you boot from the Recovery Partition follow these steps:

  1. Make a copy of the original disk image
  2. Convert the disk image to a read/write disk image using Disk Utility.
  3. Add the SIP Disable script to `/usr/local/bin`
  4. Add the Launch Daemons Property List
  5. Remove Safari to make room for the script.
  6. Compress the disk image back to a read-only image.
  7. Replace the original disk image with the modified one.

You can use these above steps to add whatever customization, like an application or administrative tool to the recovery partition. However, the recovery partition is a specific disk quota and you could get an error like this if your modifications don’t leave enough disk space. `Error (async): The new recovery partition would be too large (-69668)`

For detailed instructions on how to modfiy the recovery parition, check out:  [Automatic Disabling SIP with El Capitan Upgrade](https://apple.lib.utah.edu/?p=1444)


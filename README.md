# windows-esd-to-iso

A tool to convert a Windows 11 electronic software distribution (ESD) to a bootable ISO image.

Since Microsoft does not distribute Windows ARM ISO images, [a way to download ESDs](#downloading-esds) plus this tool allows you to obtain a Windows ARM ISO image—e.g. for use in a virtual machine, such as [UTM](https://getutm.app) or [the free VMware Fusion Player](https://www.vmware.com/go/getfusionplayer).

## Requirements

- The command-line tools from [wimlib](https://wimlib.net) (available in [Homebrew](https://brew.sh))

All remaining requirements are already included in macOS. Patches are welcome for portability.

## Usage

```
windows-esd-to-iso ESD_FILE
```

Converts the ESD in ESD_FILE to ISO format.

## How it works

[windows-esd-to-iso](./windows-esd-to-iso) will use the wimlib tools to inspect, deconstruct, and assemble into an installation tree the images inside an ESD.

Specifically, it assumes:

- Image 1 is the base Windows setup media, which serves as the base of the installation tree
- Image 2 is Windows PE, exported to sources/boot.wim
- Image 3 is Windows Setup, appended to sources/boot.wim, and set bootable
- All remaining images are Windows editions, which will be exported into sources/install.esd

These steps are performed into a temporary directory. When finished, [hdiutil](https://ss64.com/osx/hdiutil.html) is used to create the ISO image from this temporary tree.

If the script exits for any reason—successful or otherwise—the temporary directory is cleaned.

## Downloading ESDs

There are a few ways you can get an ESD to convert with this tool.

- [My own download-windows-esd tool](https://github.com/mattieb/download-windows-esd) will get the Windows 11 ESD catalog from Microsoft, then download any ESD you wish that is referenced in that catalog and verify its SHA1 checksum.
- Paul Rockwell's [w11arm_esd2iso](https://communities.vmware.com/t5/VMware-Fusion-Documents/w11arm-esd2iso-a-utility-to-create-Windows-11-ARM-ISOs-from/ta-p/2957381) does both downloading and conversion of ARM images in a single shot.
- Bogdan's [ESD to ISO on macOS](https://gist.github.com/b0gdanw/e36ea84828dbd19e03eff6158f1fc77c) explains how to get and search through the catalog and download manually.

## Converting to USB drives

You can convert an ISO produced with this tool to a USB drive with [windows-iso-to-usb](https://github.com/mattieb/windows-iso-to-usb).

## Licensing

While this tool itself is [already licensed to you](./LICENSE.md), Windows itself may require licensing and activation.

You must address this; this tool does not.

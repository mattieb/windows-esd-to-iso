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

On completion or on error, this tool removes its temporary directory (which can be large.) If you don't want this, set `NO_CLEANUP` to any value:

```
NO_CLEANUP=1 windows-esd-to-iso ESD_FILE
```

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

You can use [download-windows-esd](https://github.com/mattieb/download-windows-esd) to get the Windows 11 ESD catalog from Microsoft, then download any ESD you wish that is referenced in that catalog and verify its checksum.

## Converting to USB drives

You can convert an ISO produced with this tool to a USB drive with [windows-iso-to-usb](https://github.com/mattieb/windows-iso-to-usb).

## Licensing

While this tool itself is [already licensed to you](./LICENSE.md), Windows itself may require licensing and activation.

You must address this; this tool does not.

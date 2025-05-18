# Changes

## Unreleased

1.  Added dual-boot capability to the generated ISO image to allow it to be booted on either BIOS or EFI. Note that this does _not_ circumvent [the Windows 11 UEFI requirement](https://www.microsoft.com/en-us/windows/windows-11-specifications#table1), which the installer may check for.

2.  Added support for Ubuntu.

## 1.0.0 - 2024-10-15

This is the first actual release. Before this point, windows-esd-to-iso was a rolling repository. All changes here are from the original version.

1.  Replaced status messages with nicer, easier-to-read messages in color.

2.  Added error checking for presence of wimlib tools and ESD image before starting.

3.  Added error checking to image count check.

4.  Various improvements to code quality.

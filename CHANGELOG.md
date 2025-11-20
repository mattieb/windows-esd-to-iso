# Changes

## 1.1.0 - 2025-11-19

1.  Additional preflight checks were added to warn if trying to run this script on anything besides macOS (it's only designed and tested there) as well as error if "hdiutil" is missing.

2.  The `NO_CLEANUP` environment variable was added to prevent the temporary directory from being removed on error or completion.

## 1.0.0 - 2024-10-15

This is the first actual release. Before this point, windows-esd-to-iso was a rolling repository. All changes here are from the original version.

1.  Replaced status messages with nicer, easier-to-read messages in color.

2.  Added error checking for presence of wimlib tools and ESD image before starting.

3.  Added error checking to image count check.

4.  Various improvements to code quality.

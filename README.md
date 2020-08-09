## GHC macOS Installer

The purpose of this is to build a GHC macOS Installer to demonstrate how to code sign, package, and notarize an application.

GHC macOS Installer was originally created and influenced by Kosala Sananthana's tool at [KosalaHerath/macos-installer-builder](https://github.com/KosalaHerath/macos-installer-builder).

## Requirements

- macOS 10.15.6 or greater

- Xcode 11.6 or greater

## Installation, Setup, and Usage

1. Download and Uncompress a recent GHC version

   ```zsh
   gunzip -dc ghc-X.Y.Z-x86_64-apple-darwin.tar.xz | tar xf -
   ```

2. copy files to macOS Installer `application` directory

   ```zsh
   cp -r /path/to/ghc-X.Y.Z/* /path/to/ghc-macos-installer/macOS-x64/application
   ```

3. Download and Run Installer

   ```zsh
   cd /path/to/ghc-macos-installer
   ./build-macos-x64.sh <product> <version>
   ```

## References

- https://developer.apple.com/developer-id

- https://developer.apple.com/documentation/xcode/notarizing_macos_software_before_distribution

- https://developer.apple.com/videos/play/wwdc2019/703

- https://medium.com/swlh/the-easiest-way-to-build-macos-installer-for-your-application-34a11dd08744

## Support

Bug reports and feature requests can be filed for the cassandra-example-using-rails project here:

- [File Bug Reports and Features](https://github.com/conradwt/ghc-macos-installer/issues)

## Contributors

- Conrad Taylor (@conradwt)

- Kosala Sananthana (@KosalaHerath)

## License

This repository is released un the [MIT License](./LICENSE.md)

## Copyright

&copy; Copyright 2020 Conrad Taylor. All Rights Reserved.

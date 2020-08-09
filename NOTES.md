## Haskell macOS Installer Notes

## uncompress tarball

```zsh
gunzip -dc ghc-X.Y.Z-x86_64-apple-darwin.tar.xz | tar xf -
```

## copy files to macOS Installer `application` directory

````zsh
cp -r /path/to/ghc-X.Y.Z/* /path/to/macos-installer-builder/macOS-x64/application
```

## code sign all executables

```zsh
codesign --force --sign "Developer ID Application: <identityIdentifier>" <path-executable-file>
````

```zsh
codesign \
  --deep \
  --force \
  --verify \
  --verbose \
  --sign "Developer ID Application:<developer-id-application>" \
  --timestamp \
  --options runtime <path-to-executable-file>
```

Note: One needs to code sign all executable file here. Please see `./scripts/codesign_files`

## verify code signing (optional)

```zsh
spctl -a -t open --context context:primary-signature -v <path-to-executable-file>
```

Note: Please see `./scripts/codesign_verify_files`

## notarize package

```zsh
xcrun altool \
  --notarize-app \
  --primary-bundle-id "org.haskell.ghc" \
  --username "AC_USERNAME" \
  --password "@keychain:AC_PASSWORD" \
  --file <path-to-pkg-file>
```

Note: `AC_USERNAME` is Apple Developer e-mail address and `AC_PASSWORD` is your password added to the Apple Keychain app.

## check status of notarization

```zsh
xcrun altool --notarization-history 0 -u "AC_USERNAME" -p "@keychain:AC_PASSWORD"
```

Note: `AC_USERNAME` is Apple Developer e-mail address and `AC_PASSWORD` is your password added to the Apple Keychain app.

## after notarization completes sucessfully, staple the package

```zsh
xcrun stapler staple <path-to-pkg-file>
```

e.g.

```zsh
xcrun stapler staple ghc-X.Y.Z-macos-darwin-x86_64.pkg
```

## verify notarization of package

```zsh
xcrun stapler validate <path-to-pkg-file>
```

## verify notarization of a downloaded application

```zsh
spctl --assess --verbose <path-to-pkg-file>
```

## References

- https://developer.apple.com/developer-id

- https://developer.apple.com/documentation/xcode/notarizing_macos_software_before_distribution

- https://developer.apple.com/videos/play/wwdc2019/703

- https://medium.com/swlh/the-easiest-way-to-build-macos-installer-for-your-application-34a11dd08744

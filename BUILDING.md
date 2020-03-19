# Building SailfishOS for Note 7

## Clone/Patch the trees
Before building hybris-hal, we have to run this as libhybris isn't cloned:
```
cd $ANDROID_ROOT/external
git clone --recurse-submodules https://github.com/mer-hybris/libhybris.git
cd $ANDROID_ROOT
hybris-patches/apply-patches.sh --mb
```
The last line patches the trees so that they can compile via HADK.

## Build errors
### No provider of 'pkgconfig(libnciplugin)'
```
No provider of 'pkgconfig(libnciplugin)' found.
Setting version: 1.1.1
error: Failed build dependencies:
        pkgconfig(libncicore) is needed by nfcd-binder-plugin-1.1.1-0.armv7hl
        pkgconfig(libnciplugin) is needed by nfcd-binder-plugin-1.1.1-0.armv7hl
        pkgconfig(nfcd-plugin) >= 1.0.20 is needed by nfcd-binder-plugin-1.1.1-0.armv7hl
Building target platforms: armv7hl-meego-linux
Building for target armv7hl-meego-linux
```

To fix this, we need to build libncicore:
```
PlatformSDK $ rpm/dhd/helpers/build_packages.sh --mw=https://github.com/mer-hybris/libncicore.git
PlatformSDK $ rpm/dhd/helpers/build_packages.sh --mw=https://git.sailfishos.org/mer-core/nfcd.git
PlatformSDK $ rpm/dhd/helpers/build_packages.sh --mw=https://github.com/mer-hybris/libnciplugin.git
PlatformSDK $ rpm/dhd/helpers/build_packages.sh --mw=https://github.com/mer-hybris/nfcd-binder-plugin.git
```

After that, it should build just fine.

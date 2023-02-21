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
A few missing dependencies might pop up which can be fixed by installing them if needed. Don't run then all at once.
```
PlatformSDK $ rpm/dhd/helpers/build_packages.sh --mw=https://github.com/mer-hybris/libncicore.git
PlatformSDK $ rpm/dhd/helpers/build_packages.sh --mw=https://git.sailfishos.org/mer-core/nfcd.git
PlatformSDK $ rpm/dhd/helpers/build_packages.sh --mw=https://github.com/mer-hybris/libnciplugin.git
PlatformSDK $ rpm/dhd/helpers/build_packages.sh --mw=https://github.com/mer-hybris/nfcd-binder-plugin.git
PlatformSDK $ sb2 -t $VENDOR-$DEVICE-$PORT_ARCH -m sdk-install -R zypper in "ssu-kickstart-configuration"
PlatformSDK $ rpm/dhd/helpers/build_packages.sh --mw=https://github.com/sailfishos/repomd-pattern-builder
PlatformSDK $ sb2 -t $VENDOR-$DEVICE-$PORT_ARCH -m sdk-install -R zypper in "qt5-qttools-kmap2qmap"
PlatformSDK $ sb2 -t $VENDOR-$DEVICE-$PORT_ARCH -msdk-install -R zypper in ccache
```

After that, it should build just fine.

# Building SailfishOS 4.5 for Note 7

## Build errors
Before building anything with build_package make sure to run
```
PlatformSDK $ sb2 -t $VENDOR-$DEVICE-$PORT_ARCH -msdk-install -R zypper in ccache
PlatformSDK $ sb2 -t $VENDOR-$DEVICE-$PORT_ARCH -m sdk-install -R zypper -n rm bluez5-configs-mer
```

To build --version the following are needed
```
PlatformSDK $ sdk-assistant maintain $VENDOR-$DEVICE-$PORT_ARCH zypper -n --plus-repo $ANDROID_ROOT/droid-local-repo/lavender/ install --allow-unsigned-rpm droid-hal-lavender droid-hal-lavender-kernel
PlatformSDK $ sdk-assistant maintain $VENDOR-$DEVICE-$PORT_ARCH zypper -n --plus-repo $ANDROID_ROOT/droid-local-repo/$DEVICE install --allow-unsigned-rpm hybris-libsensorfw-qt5 mce-plugin-libhybris ngfd-plugin-native-vibrator pulseaudio-modules-droid qtscenegraph-adaptation
PlatformSDK $ sb2 -t $VENDOR-$DEVICE-$PORT_ARCH -R -m sdk-install zypper in droid-config-$DEVICE -ofono-configs-binder
PlatformSDK $ sdk-assistant maintain $VENDOR-$DEVICE-$PORT_ARCH zypper -n --plus-repo $ANDROID_ROOT/droid-local-repo/$DEVICE install --allow-unsigned-rpm droid-config droid-config-preinit-plugins droid-config-pulseaudio-settings droid-config-sailfish qt5-qpa-hwcomposer-plugin
```

After that, it should build just fine.

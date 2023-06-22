# DiamondAOSP 5.15 kernel

```shell
repo init -u git@github.com:DiamondAOSP/kernel_manifest-5.15.git -b 13 --submodules

./patcher apply

BUILD_CONFIG=common/build.config.gki.x86_64 build/build.sh
cp -a out out-vendor-modules && rm out-vendor-modules/android13-5.15/dist/kernelsu.ko
BUILD_CONFIG=common-modules/virtual-device/build.config.virtual_device.x86_64 OUT_DIR=out-vendor-modules/android13-5.15 build/build.sh
find out-vendor-modules/android13-5.15/dist -type f -name '*.ko' -exec out/android13-5.15/common/scripts/sign-file sha256 out/android13-5.15/common/certs/signing_key.pem out/android13-5.15/common/certs/signing_key.x509 {} \;

ANDROID_BUILD_TOP=../../diamondaosp
cp out/android13-5.15/dist/bzImage $ANDROID_BUILD_TOP/kernel/prebuilts/5.15/x86_64/kernel-5.15
cp out/android13-5.15/dist/System.map $ANDROID_BUILD_TOP/kernel/prebuilts/5.15/x86_64/System.map
cp out/android13-5.15/dist/kernelsu.ko $ANDROID_BUILD_TOP/kernel/prebuilts/5.15/x86_64/kernelsu/kernelsu.ko
cp out-vendor-modules/android13-5.15/dist/*.ko $ANDROID_BUILD_TOP/kernel/prebuilts/common-modules/virtual-device/5.15/x86-64/
```

Based on [GrapheneOS](https://github.com/GrapheneOS/kernel_manifest-5.15)

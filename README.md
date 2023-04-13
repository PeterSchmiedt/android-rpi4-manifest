# Android default manifest for RaspberryPi 4

## Setup

Follow the official guide https://source.android.com/docs/setup/start/initializing

    $ sudo apt install bc coreutils dosfstools e2fsprogs fdisk kpartx mtools ninja-build pkg-config python3-pip
    $ sudo pip3 install meson mako jinja2 ply pyyaml
    $ sudo apt-get install libncurses5

## Setup Android repo

    $ repo init -u https://android.googlesource.com/platform/manifest -b android-13.0.0_r41
    $ curl --create-dirs -L -o .repo/local_manifests/manifest_brcm_rpi4.xml -O -L https://raw.githubusercontent.com/PeterSchmiedt/android-rpi4-manifest/main/manifest_bcrm_rpi4.xml

Sync the repo

    $ repo sync -j$(nproc)

## Compile

    $ . build/envsetup.sh
    $ lunch aosp_rpi4-eng
    $ make bootimage systemimage vendorimage -j$(nproc)

## Make flashable image

    $ ./rpi4-mkimg.sh

# Android Kernel

    $ repo init -u https://android.googlesource.com/kernel/manifest -b common-android13-5.15-lts
    $ curl --create-dirs -L -o .repo/local_manifests/manifest_brcm_rpi4.xml -O -L https://raw.githubusercontent.com/raspberry-vanilla/android_kernel_manifest/android-13.0/manifest_brcm_rpi4.xml

## Sync source code

    $ repo sync -j$(nproc)

## Compile

    $ BUILD_CONFIG=common/build.config.rpi4 build/build.sh

Compiled kernel Image, dtbs, and overlays can be found in out/common/arch/arm64/boot directory.

Replace existing files in device/brcm/rpi4-kernel directory of the Android source tree to include them in Android 13 build. You can also replace existing files in the boot partition of Raspberry Pi 4 Android 13 image.
# Android default manifest for RaspberryPi 4

# Setup

Follow the official guide https://source.android.com/docs/setup/start/initializing

    $ sudo apt install libssl-dev python3-setuptools 

## Download

Clone existing manifest to android source repo.

    $ repo init -u https://android.googlesource.com/platform/manifest -b android-12.1.0_r21
    $ git clone https://github.com/PeterSchmiedt/android-rpi4-manifest.git .repo/local_manifests
    $ repo sync -j10

# Patch

https://github.com/android-rpi/device_arpi_rpi4/wiki/arpi-12-:-framework-patch

## Build Android

    $ source build/envsetup.sh
    $ lunch rpi4-eng
    $ make ramdisk systemimage vendorimage -j10
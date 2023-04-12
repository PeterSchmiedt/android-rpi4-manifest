# Android default manifest for RaspberryPi 4

## Setup

Follow the official guide https://source.android.com/docs/setup/start/initializing

    $ sudo apt install bc coreutils dosfstools e2fsprogs fdisk kpartx mtools ninja-build pkg-config python3-pip
    $ sudo pip3 install meson mako jinja2 ply pyyaml

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

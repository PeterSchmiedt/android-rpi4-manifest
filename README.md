# Android default manifest for RaspberryPi 4

## Setup

Follow the official guide https://source.android.com/docs/setup/start/initializing

    $ sudo apt install libssl-dev python3-setuptools 

## Download

Clone existing manifest to android source repo.

    $ repo init -u https://android.googlesource.com/platform/manifest -b android-12.1.0_r21
    $ git clone https://github.com/PeterSchmiedt/android-rpi4-manifest.git .repo/local_manifests
    $ repo sync -j10

## Patch

https://github.com/android-rpi/device_arpi_rpi4/wiki/arpi-12-:-framework-patch

## Build Android

    $ source build/envsetup.sh
    $ lunch rpi4-eng
    $ make ramdisk systemimage vendorimage -j10

## Prepare the SD card

Partitions of the card should be set-up like followings.
  - p1  128MB for boot : Do fdisk, set W95 FAT32(LBA) & Bootable type, mkfs.vfat
  - p2 1024MB for /system : Do fdisk, new primary partition
  - p3  128MB for /vendor : Do fdisk, new primary partition
  - p4 remainings for /data : Do fdisk, mkfs.ext4
 
Set volume label of /data partition as userdata
  : use -L option for mkfs.ext4



# Linux Kernel

## Download

    $ repo init -u https://github.com/android-rpi/kernel_manifest -b arpi-5.15
    $ repo sync

## Build

    $ build/build.sh

Output files are under out/arpi-5.15/dist/
  - Image.gz
  - bcm2711-rpi-*.dtb
  - vc4-kms-v3d-pi4.dtbo

# Build Android for Raspberry Pi 4

  https://github.com/android-rpi/device_arpi_rpi4
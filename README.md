Device configuration for Sony Xperia XZ1 dual (poplar_dsds)
========================================================

Description
-----------

This repository is for Hentai OS on Sony Xperia XZ1 dual (poplar_dsds).

How to build Hentai OS
----------------------

* Make a workspace:

        mkdir -p ~/hentai
        cd ~/

* Initialize the repo:

        repo init -u https://github.com/HentaiOS/platform_manifest -b queenslave

* Create a local manifest:

        cd .repo
        mkdir local_manifests
        cd local_manifests
        touch roomservice.xml

        <?xml version="1.0" encoding="UTF-8"?>
        <manifest>
            <!-- SONY -->
            <project name="cryptomilk/android_kernel_sony_msm8998" path="kernel/sony/msm8998" remote="github" revision="lineage-17.1" />
            <project name="cryptomilk/android_device_sony_common-treble" path="device/sony/common-treble" remote="github" revision="lineage-17.1" />
            <project name="cryptomilk/android_device_sony_yoshino" path="device/sony/yoshino" remote="github" revision="lineage-17.1" />
            <project name="HentaiOS-Devices-Sony/android_device_sony_poplar_dsds" path="device/sony/poplar_dsds" remote="github" revision="queenslave" />
            
            <!-- PixelExperience -->
              <project path="device/qcom/sepolicy-legacy-um" name="PixelExperience/device_qcom_sepolicy-legacy-um" remote="github" revision="ten" />

            <!-- Pinned blobs for poplar_dsds -->
            <project name="derfelot/android_vendor_sony_poplar_dsds" path="vendor/sony/poplar_dsds" remote="github" revision="lineage-17.1" />
        </manifest>

* Sync the repo:

        repo sync -c -j6 --no-clone-bundle -no-tags

* Extract vendor blobs

        cd device/sony/poplar_dsds
        ./extract-files.sh

* Setup the environment

        source build/envsetup.sh
        lunch hentai_poplar_dsds-userdebug

* Build LineageOS

        make -j&(nproc)

thanks to @shank03 for the help and reference: https://github.com/shank03/android_device_sony_lilac

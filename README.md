# PRISM

1. Unlock the bootloader of Google Pixel 7.
   https://source.android.com/docs/core/architecture/bootloader/locking_unlocking
   or https://xdaforums.com/t/guide-january-3-2024-root-pixel-7-pro-unlock-bootloader-pass-safetynet-both-slots-bootable-more.4505353/
2. install repo
   https://source.android.com/docs/setup/download
3. Sync AOSP source code version Android 13
4. Merge aosp forlder to AOSP source code
5. Build AOSP
   enter source code folder
   source build/envsetup.sh
   lunch aosp_panther-userdebug
   export SANITIZE_TARGET=hwaddress
   m -jx
6. Flash AOSP
   Enable OEM unlock in developer options.
   Enable USB debug

   adb reboot bootloader (or power + V-)
   fastboot flashing unlock
   cd ~/AOSP/out/target/product/panther
   ANDROID_PRODUCT_OUT=`pwd` fastboot flashall -w --disable-verity --disable-verification            //if failed, chand pwd to  ~/AOSP/out/target/product/panther
   
8. Sync host Linux kernel. The pVM guest kernel is the same version with host.
   repo init -u https://android.googlesource.com/kernel/manifest -b android-gs-pantah-5.10-android13-d1
   repo sync -jx                   

#WIP NOT WORKING YET. SEE: http://forum.xda-developers.com/showpost.php?p=62778371&postcount=25

local manifest for https://github.com/chrmhoffmann/android_kernel_fp_FP1 and https://github.com/chrmhoffmann/android_device_fp_FP1
local manifest belongs into "YOURBUILDFOLDER/.repo/local_manifests"

# Build with precompiled kernel
I'm unsuccesful at building kernel right now, so I'm switching to the prekompiled kernel, which is in the _android_ files. 
Last thing I tried was cherrypicking these: https://gerrit.omnirom.org/#/c/4834/ where Building failed as well.

#Build instructions 
(see http://wiki.cyanogenmod.org/w/Doc:_porting_intro)

// Follow http://wiki.cyanogenmod.org/w/Build_for_one to get all prerequisites until: "Initialize the CyanogenMod source repository"

// Download Cyanogenmod 11.0 into working directory (take a double coffee)
- cd ~/android/system/
- repo init -u https://github.com/CyanogenMod/android.git -b cm-11.0
- repo sync

// Get FP1 specific Android Kernel and Android Device (take a coffee): Copy local_manifest.xml into .repo/local_manifests and then
- repo sync

// Check if you have succesfully downloaded folders kernel/fp/ and device/fp

// Get proprietary builds (ADB connect your device)
- cd fp/FP1
- ./extract-files.sh

// Check if there is a folder vendor/fp/FP1 and if it's full according to list in extract-files.sh

//Start building (take a double coffee)
- croot
- . build/envsetup.sh
- brunch FP1

#Errors:
- If build fails due to "make: *** No rule to make target 'vendor/fp/FP1/proprietary/lib/hw/audio.primary.mt6589.so', needed by '/home/martin/android/system/out/target/product/FP1/system/lib/hw/audio.primary.mt6589.so'.  Stop."
Manually pull lib/hw/audio.primary.mt6589.so from your device and put into folder in vendor/fp/FP1/proprietary/...


- find: `bootable/recovery/res-540': No such file or directory
No private recovery resources for TARGET_DEVICE FP1
build/core/tasks/kernel.mk:91: **********************************************************
build/core/tasks/kernel.mk:92: * Kernel source found, but no configuration was defined  *
build/core/tasks/kernel.mk:93: * Please add the TARGET_KERNEL_CONFIG variable to your   *
build/core/tasks/kernel.mk:94: * BoardConfig.mk file                                    *
build/core/tasks/kernel.mk:95: **********************************************************
Install: /home/martin/android/system/out/host/linux-x86/bin/mkbootimg
Install: /home/martin/android/system/out/host/linux-x86/bin/mkbootfs
Install: /home/martin/android/system/out/host/linux-x86/bin/checkpolicy
Install: /home/martin/android/system/out/host/linux-x86/bin/checkfc
Install: /home/martin/android/system/out/host/linux-x86/bin/clang-tblgen

Solution: TARGET_KERNEL_CONFIG := ../../../kernel/fp/FP1/mediatek/config/ahong89_wet_jb2/configs/ in device/fp/FP1/BoardConfig.mk
Install: /home/martin/android/system/out/host/linux-x86/bin/tblgen
Install: /home/martin/android/system/out/target/product/FP1/system/usr/share/zoneinfo/tzdata
Install: /home/martin/android/system/out/target/product/FP1/root/init.rc
target Prebuilt:  (/home/martin/android/system/out/target/product/FP1/kernel)
Install: /home/martin/android/system/out/target/product/FP1/recovery/root/sbin/killrecovery.sh
acp: missing destination file
build/core/tasks/kernel.mk:212: recipe for target '/home/martin/android/system/out/target/product/FP1/kernel' failed
make: *** [/home/martin/android/system/out/target/product/FP1/kernel] Error 2
make: *** Waiting for unfinished jobs....

local manifest for https://github.com/chrmhoffmann/android_kernel_fp_FP1 and https://github.com/chrmhoffmann/android_device_fp_FP1
local manifest belongs into "YOURBUILDFOLDER/.repo/local_manifests"

#Build instructions 
(see http://wiki.cyanogenmod.org/w/Doc:_porting_intro)

// Follow http://wiki.cyanogenmod.org/w/Build_for_one to get all prerequisites until: 
// "Initialize the CyanogenMod source repository"

// Download Cyanogenmod 11.0 into working directory (take a double coffee)
- cd ~/android/system/
- repo init -u https://github.com/CyanogenMod/android.git -b cm-11.0
- repo sync

// Get FP1 specific Android Kernel and Android Device (take a coffee)
// Copy local_manifest.xml into .repo/local_manifests
- repo sync
// Check if you have succesfully downloaded folders kernel/fp/ and device/fp

// Get proprietary builds (ADB connect your device)
- cd fp/FP1
- ./extract-files.sh
// Check if there is a folder vendor/fp/FP1 and if it's full according to list in extract-files.sh

//Start building (take a double coffee)
- croot
- brunch FP1

/* Errors: */

// If build fails due to "make: *** No rule to make target 'vendor/fp/FP1/proprietary/lib/hw/audio.primary.mt6589.so', needed by '/home/martin/android/system/out/target/product/FP1/system/lib/hw/audio.primary.mt6589.so'.  Stop."
// Manually pull lib/hw/audio.primary.mt6589.so from your device and put into folder in vendor/fp/FP1/proprietary/...

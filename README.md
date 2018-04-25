# Android_Build
Instructions to build android-5.0.0_r2.0.1 and goldfish3.4
## Build android 
### please find the offical instruction here: https://source.android.com/setup/build/downloading
* repo init -u https://android.googlesource.com/platform/manifest -b android-5.0.0_r2.0.1
* repo sync -f
* make clobber
* source ./build/envsetup.sh
* lunch aosp_eng
* make -j4

## Build goldfish
* Clone goldfish  
`git clone http://android.googlesource.com/kernel/goldfish.git`  
`$cd goldfish`  
`$git branch -a //check all branch`  
`$git checkout remotes/origin/android-goldfish-3.4`  
* Compile goldfish  
`$export PATH=$PATH:~/WORKING_DIRECTORY/prebuilts/gcc/linux-x86/arm/arm-eabi-4.8/bin (replace the address accordingly)`  
`$export ARCH=arm`  
`$export SUBARCH=arm`  
`$export CROSS_COMPILE=arm-eabi-`  
`$cd /path/to/android/source/code`  
`$source ./build/envsetup.sh`  
`$lunch aosp_eng`  
`$cd /path/to/goldfish`  
`$make goldfish_armv7_defconfig`  
`$make`  

## Troubleshooting common android build errors:
* For android-5.0.0, do the following steps before make  
`rm -rf ~/<android_art_source>/out`  
`cp /usr/bin/ld.gold ~/<android_art_source>prebuilts/gcc/Linux-x86/host/x86_64-linux-glibc2.11-4.6/x86_64-linux/bin/ld`  
`make update-api`  
* patching build/core/clang/HOST_x86_common.mk  
`ifeq ($(HOST_OS),linux)`  
`CLANG_CONFIG_x86_LINUX_HOST_EXTRA_ASFLAGS := \`  
`   --gcc-toolchain=$($(clang_2nd_arch_prefix)HOST_TOOLCHAIN_FOR_CLANG) \`  
`-  --sysroot=$($(clang_2nd_arch_prefix)HOST_TOOLCHAIN_FOR_CLANG)/sysroot`  
`+  --sysroot=$($(clang_2nd_arch_prefix)HOST_TOOLCHAIN_FOR_CLANG)/sysroot \`  
`+  -B$($(clang_2nd_arch_prefix)HOST_TOOLCHAIN_FOR_CLANG)/x86_64-linux/bin`  


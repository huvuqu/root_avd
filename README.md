
# root_avd

how to root Android AVD (and required files!)

Android SDK is required with an already created AVD. For this guide we will call it `RootAVD`.

This was written and tested on a Nexus 5X AVD running Nougat on an Ubuntu Linux host.

1. Start emulator `$SDK_PATH/emulator/emulator` with args `-avd RootAVD -writable-system -selinux disabled -qemu -enable-kvm`
1. Wait for boot.
1. Restart `adbd` as root and remount system as writable: `adb root && adb remount`
1. Install `Superuser.apk`: `adb install SuperSU/common/Superuser.apk`
1. Push `su` and update permissions: you will have to pick the corresponding architecture `$ARCH`. `adb push SuperSU/$ARCH/su /system/xbin/su`, then update permissions: `adb shell  chmod 0755 /system/xbin/su`
1. Set SELinux Permissive: `adb shell setenforce 0`
1. Install SuperSU's `su` to system: `adb shell su --install`
1. Run SuperSU's `su` as daemon. `adb shell su --daemon&`
1. Finally, open the SuperSU app on the device, and it will tell you the `su` binary needs to be updated. Accept and use normal installation.
1. Installation will fail. Don't reboot, just move on. It will still work.
1. Congratulations! You now have a rooted AVD with SuperSU.

**TIP: Superuser may not always persist after reboot, to fix:**
1. From a root shell, start `su --daemon&`
1. Root should now work.

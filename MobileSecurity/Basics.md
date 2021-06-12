# Mobile Security - Basics
Some basic **ADB** commands

Installing an app on the device
```bash
adb install <path-to-apk>
```

Take a screenshot of the device
```bash
adb shell screencap /mnt/sdcard/Download/test.png           # Takes screen and writes it to a location
adb pull /mnt/sdcard/Download/screenshot.png test.png       # Pulls the screen from the device to the host
```

Remove lockscreen from device (only on older devices, newer devices will just break :) )
```bash
adb shell rm /data/system/locksettings.db
adb reboot
```

Fake keyboard input using adb
```bash
adb shell
input text <what you want to type>
```

###Rooting a device
make sure the emulator has write enables
```bash
emulator -avd <device> -writable-system -selinux permissive
```

Connect via adb as root and remount the filesystem
```bash
adb root
adb remount
```

Copy the [SuperSU](https://github.com/0xFireball/root_avd) to /system/xbin/su
```bash
adb push root_avd/SuperSU/x86/su /system/xbin/su
```

Add permissions to our new su
```bash
adb shell chmod 0755 /system/xbin/su # extra permissions
adb shell setenforce 0 # disable firewall
adb shell su --install # install the su command
adb shell su --daemon& # This command will Run SuperSU’s su as daemon.
```

(optional) to ask apps for root permissions before giving them, install
```bash
adb install root_avd/SuperSU/common/Superuser.apk
```
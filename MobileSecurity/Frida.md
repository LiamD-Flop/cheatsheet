# Mobile Security - Frida

Setup frida server
```bash
adb root
adb push frida-server /data/local/tmp/
adb shell chmod 0755 /data/local/tmp/frida-server
adb shell /data/local/tmp/frida-server &
```

List all devices
```bash
frida-ls-devices
```

List all processes on specific device
```bash
frida-ps -D <device-id>
```

List all processes on usb connected device (also on emulated device)
```bash
frida-ps -U
```

Kill a process using frida
```bash
frida-kill -D <device-id> <process-id>
```

### Frida scripting
Make sure the frida-server is running and then create py / js files and run them on your host so they connect to the server
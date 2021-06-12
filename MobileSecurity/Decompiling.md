# Mobile Security - Decompiling

Decompile using apktool
```bash
apktool d -o <output-dir> <apk-file>
```

Recompile using apktool
```bash
apktool b -o <apk-name> <dir-to-build>
```

Sign the apk
```bash
java -jar uber-apk-signer.jar --apks <apk-to-sign>
```


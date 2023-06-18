Android Samsung Internet browser patch remove brand "SamsungBrowser/" when Desktop mode make it like Chromium.

Website can not detect and will service good content (Example Facebook comment).

> **Warning**
> This need uninstall current Samsung Browser in your mobile phone, and sign apk with new keystore. So backup/sync data of Samsung Browser first.

> **Note**
> Windows users recommend use `sed` of `Git bash for Windows` with `-b` option. If wrong replace hex when patch maybe can not open Samsung Internet. Then use HxD for edit file manually follow `patch`

## REQUIRED TOOLS

- Android SDK
- apktool
- zipalign
- apksigner
- patch
- sed

## HOW TO

- put `base.apk` (Samsung Internet browser apk) into `apk`
- run command to decode apk into `base` folder:
    ```
    ./command/decode
    ```
- check versionInfo versionCode in `base/apktool.yml`
- run command to patch:
    ```
    ./patch/[your_apk_version_code]/patch
    ```
- place `keystore.jks` in root folder
- run command to build:
    ```
    ./command/build keystore_alias keystore.jks
    ```
- patched apk in ./base/dist/base-aligned.apk

## ARM IDA

ADRL = ADRP ADD

```
C1 2F FF D0            21 AC 04 91
ADRP X1, #0xB64000     ADD X1, X1, #0x12B

Want change to new location, change last 4 hex to 00 00 00 00 for break ADRL => ADRP,
Then use IDA keypatch.
```

```
Example:
old rodata at B6412B
C1 2F FF D0 (page B64000) 21 AC 04 91 (address 12B)

new rodata at B63FB5 then
C1 2F FF B0 (page B63000) 21 D4 3E 91 (address FB5)
```

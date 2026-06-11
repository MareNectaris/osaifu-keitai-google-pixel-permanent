# Permanently Enabling osaifu-keitai(Suica) on Non-Japanese Pixel Models

## Requirements

Pixel 4(or later), with unlocked bootloader and root access; Bootloader can be locked and stock firmware can be flashed later on

## Pull the sdd Partition (Root Required)

```bash
adb shell
su
dd if=/dev/block/by-name/sdd of=/storage/emulated/0/sdd.img
```

## Edit the Model ID in Hex Editor

Search for the model ID in a hex editor.

Model ID available at: Settings - About Phone - Regulatory Labels

e.g. Search for string `G020I` for American Pixel 4. Edit to `G020N` to use Japanese model ID.

Refer to [this page](https://support.google.com/pixelphone/answer/16043605) for model IDs on other Pixels.

NOTE: If the img file seems empty, that means you are using a newer Pixel phone where the model ID is stored in `/dev/block/by-name/devinfo` instead of `/dev/block/by-name/sdd`.

## Push the Changes to the sdd Partition (Root Required)

```bash
adb shell
su
dd if=(whatever the path to the modified sdd.img is) of=/dev/block/by-name/sdd
```

## Confirm the Changes

Check for model ID at Settings-About Phone-Regulatory Labels.

This change is permanent; You can revert to stock ROM and lock the bootloader if you want to.

## Install Dependencies for osaifu-keitai

With a Japanese Google account, search for these apps on the Play Store and install them:

* `com.felicanetworks.mfm.main`
* `com.felicanetworks.mfc`
* `com.felicanetworks.mfs`
* `com.google.android.gms.pay.sidecar`

After that, install the Mobile Suica app (`com.mobilesuica.msb.android`) or fire up the Google Wallet app; at this point it should just work.

## Caveats

Cellular band/frequency support may or may not change after editing the model ID.

Your warranty may be voided. I am not responsible for any changes or damages made to your device.

## Resources

* <https://xdaforums.com/t/converting-japanese-pixel-6-to-global-version.4365275/page-9#post-89084361>
* <https://github.com/kormax/osaifu-keitai-google-pixel>

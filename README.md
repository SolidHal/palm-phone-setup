# palm-phone-setup


## Original fourm posts
https://forum.xda-developers.com/t/release-palm-debloat-fixes-script-2020-03-11.4052477/
https://forum.xda-developers.com/t/release-root-the-palm-phone.4021201/


## Root

```
Here is a rooting method for the Plam Phone either the US variant or the Vodafone variant this has not been tested or confirmed working on any other device. This root method may break in the future because it is using a tool that isn't designed for the public i tried getting the firehose packaged with the tool to work in other edl flashing tools but was not able to get it working. So this is all we have for now. There is minimal risk in doing this it just has a lot of steps and it requires a pc running windows.

Note: This will wipe your device so anything stored on it will be lost please backup anything important like photos/contacts/etc

    1) Download and install Sugar QCT from here (Be sure to install the usb drivers as well)
    2) Included in the zip is the username and password that you will need to use to run the program please do not post it here.
    3) Boot the device into recovery by turning the device off and then holding the power button until it restarts 3-4 times and boots to recovery
    4) Select the option to go into emergency download mode
    5) Now plug the device into your computer and open Sugar QCT
    6) From the list select pepito/PVG100 (US) or pepito_vdf (Vodafone)
    7) Now select Upgrade this will download the palms firmware package and flash it to the device
    8) *IMPORTANT* When it finishes do not close sugar
    9) Unplug your device and hold the power button for a few minutes so it will restart out of EDL mode, use a rubber band or something to apply pressure to it so you don't have to hold it
    10) Go to where Sugar QCT is installed (C:\Program Files (x86)\SUGAR QCT_SP_Gotu2\bin\)
    11) In there you should see a folder called PVG100-xxxx (The x's are your serial number)
    12) Copy that to your desktop or anywhere else that you like. If you don't make a copy, closing sugar will delete these files
    13) In the folder, there should be some random looking mbn files these are actually the firmware files just names are randomized to make using them harder.
    14) There should be a file called B1AMD0D0CV00.mbn if not look for a file that starts with a B it will be the boot.img
    15) You will need to push that to an android device and patch it with magisk manager.
    16) Once that is done replace the B1AMD0D0CV00.mbn in your copy of the firmware with the patched boot.img
    17) Boot it back into emergency download mode as previously stated
    18) Close and reopen sugar
    19) Copy your firmware copy back into C:\Program Files (x86)\SUGAR QCT_SP_Gotu2\bin\ be sure it is the same folder structure
    20) Now select your model again and then press the upgrade button in sugar this will now flash your modified firmware to the device.
    21) Once it finishes hold the power button for a few minutes so it will restart out of EDL mode, use a rubber band or something to apply pressure to it so you don't have to hold it
    22) When it restarts and powers up then go through setting the phone up and install magisk manager and you're rooted.

```


## Disable DM-Verity

this is required to 


## General Debloat

### replace proprietary keyboard

```
adb install keyboard_apk/rkr.simplekeyboard.inputmethod_94.apk
```
Go to Settings -> System -> Languages & Input -> Virtual Keyboard -> Manage Keyboards
Enable "Simple Keyboard".

Make it a system app,
adb shell:
```
su
mount -o rw,remount /system; mount -o rw,remount /vendor
mv /data/app/rkr.simplekeyboard.inputmethod-* /system/app  ## required in case user forces pin on boot
```

## Uninstall a bunch of verizon apps


adb shell:
```
su
mount -o rw,remount /system; mount -o rw,remount /vendor


echo "Removing user installs..."
pm uninstall -k --user 0 'com.verizon.cloudsetupwizard'
pm uninstall -k --user 0 'com.verizon.mips.services'
pm uninstall -k --user 0 'com.vzw.hss.myverizon'
pm uninstall -k --user 0 'com.jrd.verizonuriintentservice'
pm uninstall -k --user 0 'com.verizon.messaging.vzmsgs'
pm uninstall -k --user 0 'com.verizon.llkagent'
pm uninstall -k --user 0 'com.vzw.apnlib'
pm uninstall -k --user 0 'com.tcl.vzwintents'
pm uninstall -k --user 0 'com.tct.vzwwifioffload'
pm uninstall -k --user 0 'com.vzw.ecid'
pm uninstall -k --user 0 'com.vzw.easvalidation'
pm uninstall -k --user 0 'com.customermobile.preload.vzw'
pm uninstall -k --user 0 'com.vcast.mediamanager'
pm uninstall -k --user 0 'com.ts.setupwizard.overlay.overlay'
pm uninstall -k --user 0 'com.jrdcom.Elabel.overlay'
pm uninstall -k --user 0 'com.android.dreams.phototable.overlay'
pm uninstall -k --user 0 'com.android.email.partnerprovider.overlay'
pm uninstall -k --user 0 'com.telecomsys.directedsms.android.SCG'
pm uninstall -k --user 0 'com.google.android.marvin.talkback'
pm uninstall -k --user 0 'com.android.wallpaper.livepicker.overlay'
pm uninstall -k --user 0 'com.google.android.ext.services'



echo "Removing system bloatware..."
cd /system/app
## WARN: no remove (will brick): GoogleExtShared SecureExtAuthService
rm -rf MMITest talkback SecureSampleAuthService EasValidation SampleExtAuthService SampleAuthenticatorService LiveWallpapersPicker AutoRegistration EmailPartnerProvider StatsPollManager FidoCryptoService OneTouchFeedback CloudSetupWizardOverlay BasicDreams Gmail2 SuperEngineerMode CompanionDeviceManager GmsSampleIntegration PartnerBookmarksProvider GoogleContactsSyncAdapter PhotoTable BluetoothMidiService Photos TestMode remotesimlockservice CalendarGoogle GooglePrintRecommendationService VerizonUrintentService verizon-wifi-offload Videos vzwintents YGPS YouTube Music2 EasterEgg Drive Duo 


cd /system/priv-app
rm -rf AutoKillService Fota ConfigUpdater GoogleBackupTransport StatementService VerizonNameID TagGoogle WiFiActivation com.customermobile.preload.vzw Elabel GoogleFeedback GoogleOneTimeInitializer GooglePartnerSetup SetupWizardOverlay SetupWizard VZWAPNLib Velvet verizon-llk-agent


cd /vendor/app
rm -rf ChromeCustomizations VzwDMClient unremoveable/Fleksy-9.7.6-palm-2860-armeabi-v7a-palmPlayStoreRelease.apk


cd /vendor/priv-app
rm -rf MVM_vzw_app-release-phone-13.1.1-278.apk VZMessages-mobile-6.7.12-94-market-release-signed.apk Verizon_LocationAgent_vzw_v0.0.3.120_Production_NoDebug_release_signed.apk client-17.6.14-prod-phone-release.apk


mv /vendor/bin/mmid /vendor/bin/mmid.bak  ## couldn't find anything on the net about this, and it has lots of wakeups & logcat writing.
```


## Fix Incorrect APN settings

```
adb push apn_settings/apns-conf.xml /sdcard/
```

adb shell:
```
su
mount -o rw,remount /system; mount -o rw,remount /vendor
echo "Fixing APN list..."
cp -F /sdcard/apns-conf.xml /vendor/etc
chmod 755 /vendor/etc/apns-conf.xml
```

The APN database must be manually repopulated. After the phone reboots go to Mobile APN Settings and Restore Default.


## Remove verizon boot animation
adb shell:
```
su
mount -o rw,remount /vendor
cd /vendor
rm JRD_custres/media/bootanimation.zip
```

## Remove GAPPs


## Credits
- Thanks to deadman96385 on xda for the root method
- Thanks to snoopy20 on xda for the debloat script


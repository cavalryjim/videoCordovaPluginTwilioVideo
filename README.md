**Using this plugin**

## Configure Twilio
To work correctly, this Twilio plugin requires configuring.

### iOS
If one does not exist, build an iOS version of the app.
Note: this command may fail because of a missing library that gets added below. (most likely libc++).  If so, complete the commands below and try again.
```
$ ionic cordova build ios  
```

Download the [Twilio Video SDK iOS 1.4.0](https://github.com/twilio/twilio-video-ios/releases/download/1.4.0/TwilioVideo.framework.zip) file.  Unzip the file and identify the `TwilioVideo.framework` folder.

Note: videoCordovaPluginTwilioVideo does not work with SDK versions 2.*

Open the project in Xcode and navigate to the General settings page. Drag and drop `TwilioVideo.framework` onto the Embedded Binaries section. Ensure that "Copy items if needed" is checked and press Finish. This will add TwilioVideo.framework to both the Embedded Binaries and Linked Frameworks and Libraries sections.

Next, you will need to open your project's Linked Frameworks and Libraries configuration. You should see the TwilioVideo.framework there already. Add the following frameworks to that list:

- AudioToolbox.framework
- VideoToolbox.framework
- AVFoundation.framework
- CoreTelephony.framework
- GLKit.framework
- CoreMedia.framework
- SystemConfiguration.framework
- libc++.tbd

In your Build Settings, you will also need to modify "Other Linker Flags" to include -ObjC.

![xcode settings](https://relieftelemed.com/assets/img/twilio_xcode_settings.png)

Before distributing your app to the  App Store, you will need to strip the simulator binaries from the embedded framework. Navigate to your target's Build Phases screen and create a new "Run Script Phase". Ensure that this new run script phase is after the Embed Frameworks phase. Paste the following command in the script text field:
```
/bin/bash "${BUILT_PRODUCTS_DIR}/${FRAMEWORKS_FOLDER_PATH}/TwilioVideo.framework/remove_archs"
```

### Android
The Twilio plugin may be problematic for certain node / ionic / cordova / android versions.  This is what worked for me.
```
$ java -version
java version "1.8.0_131"
$ npm --version
5.7.1
$ ionic --version
3.20.0
$ cordova --version
7.1.0
$ ionic cordova plugin add ../videoCordovaPluginTwilioVideo --nofetch
$ ionic cordova platform rm android  
$ ionic cordova platform add android@6.4.0
```

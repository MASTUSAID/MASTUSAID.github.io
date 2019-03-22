# MAST Mobile Application
## APK Setup
The easiest way to get started with MAST mobile application is to download it from the latest releases on GitHub. Check https://github.com/MASTUSAID/MAST-MOBILE/releases/ and look for the latest release. Download mast.apk from the assets list, copy to your Android mobile device and run for installation. At the time of writing this guide, the latest release is 3.1, available at https://github.com/MASTUSAID/MAST-MOBILE/releases/download/3.1/mast.apk. 

## Fresh Compilation
###IDE Setup
First, download and install Android Studio from https://developer.android.com/studio/index.html. During setup, you will be prompted to download any versions of the Android SDK that you wish to use. For the purposes of MAST, download the SDK for Android 6.0 Nougat (API level 23).
If you wish to test the application before building, create an Android Virtual Device to ensure your install works properly. Click **Tools > Android > AVD Manager**, and click the **Create Virtual Device** button. Choose a phone and SDK level to emulate, such as the Pixel with the latest Android version. Before clicking Finish, click on **Show Advanced Settings**. Under **Memory and Storage**, ensure that the SD card is set to **Studio-Managed** and is at least 200 MB.

### Configure, Compile, and deploy application
To build the application package, first fetch the source code from GitHub:
```
$ git clone https://github.com/MASTUSAID/MAST-MOBILE.git
```
If you are using Android Studio version greater than 2.2.3, open the gradle.build file and ensure that the following value is set for the gradle version:
```
dependencies {
        classpath 'com.android.tools.build:gradle:2.3.3'
    }
```

To build the application package (APK file), select **Build > Generate Signed APK**. Android Studio will request that you create a signed keystore and key file to use to sign the application, if you have not already. Follow the onscreen instructions. Further information is available [online](https://developer.android.com/studio/publish/app-signing.html).

Once you have the final APK, transfer a copy to each device that you plan on using. To install the application, use a file browser application to open and run the APK. Note that you will have to ensure that the devices are set to run applications from alternative sources (i.e. not the Google store), by going to the devices security settings. The exact location of the setting varies from device to device.

## Known Issues
### Google Maps API Key
When compiling the MAST-MOBILE project, the Google Maps API key may not be working and it will require replacement with a new key. Open `AndroidManifest.xml` file and replace value for the following setting:
```
<meta-data
    android:name="com.google.android.maps.v2.API_KEY"
    android:value="MAPS_API_KEY" />
```
Put new key instead of MAPS_API_KEY value.

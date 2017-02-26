# Exercise 1 

## Install and Introduction with Google Maps app

### Install

Download [Android Studio](https://developer.android.com/studio/index.html)

* Install with defaults, Android Studio now installs the SDK for you to the user app data folder
* Run Android Studio that will update dependencies further.


### Start a new Android Studio project

* Configure new project - Might want to move the location from the default!
* Form factors - Phone and Tablet - Minimum API 15 is a good
* Add Activity - Google Maps activity

The Main UI of Android studio opens.

Key buttons

[logo]: https://github.com/ajchellew/android-exercises/raw/master/resources/images/AS-Overview-NewProject.png "AS Interface"

1. Run button
2. Project view
3. Code Window
4. Android Monitor - View Logcat of connected device.

See [Android Studio User Guide](https://developer.android.com/studio/intro/index.html) for more

## Running App

### Get Google API key

The new project's `google_maps_api.xml` file contains a link for getting an API key directly when you already have a developer account, **Note: this key is specific for each app namespace/SHA fingerprint**

For more instructions see [Google Map API documentation](https://developers.google.com/maps/documentation/android-api/start#get-key)

1. Get API key
2. Update the YOUR_KEY_HERE variable in `google_maps_api.xml` with the API key from Google, this key will start with 'AIza'

### Run

Press the 'Run' button 

##### Instant Run

Instant run sounds like a great idea but in personal experience it causes confusion when it fails to update correctly or resource files change.

Advise this is turned off:

`File > Settings > Build, Execution, Deployment > Instant Run`

Uncheck enable.

##### _DexIndexOverflowException_

Does it work? Likely not if _DexIndexOverflowException_ occurs this is because adding Maps as added the huge Google Maps library and Android has an limit of 65536 Methods in the DEX files.

To fix this: 

Open, Under Project > Gradle Scripts > build.gradle (module: app) 

add `multiDexEnabled true`  to the `defaultConfig` block inside the `android` block


```
android {
    compileSdkVersion 25
    buildToolsVersion "25.0.2"
    defaultConfig {
        applicationId "com.example.mapapp"
        minSdkVersion 15
        targetSdkVersion 25
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
        multiDexEnabled true
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}
```

### Run again

This should now build and install

## Understanding the app

##### App/Manifests

The `AndroidManifest.xml` describes the app, its permissions, linking its name, icons, themes and activities.

> Activities created in the app must be defined here, otherwise the app will crash when they are created.


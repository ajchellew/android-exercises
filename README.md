# android-exercises
Attempting to teach the fundamentals of Android (circa Nougat, Android Studio 2.2.3)

This page contains an overview of various concepts of Android exercises are found in subdirectories.

[Exercise 1](/exercise-1/): Installing Android Studio and creating a first app

## Android Development Principles
This is a supplement to the larger [Application Fundamentals](https://developer.android.com/guide/components/fundamentals.html) guide provided by Google, also undoubtfully more subjective.

### ADB
Android Debug Bridge is used to communicate over USB (or wifi) to a device to perform the tasks required to develop in Android. 

This is installed and managed by Android Studio but must be [enabled on devices](https://developer.android.com/studio/command-line/adb.html#Enabling) and ADB drivers for the device installed, i.e. [Samsung ADB drivers](http://developer.samsung.com/galaxy/others/android-usb-driver-for-windows)

A physical device does not have to be used, the emulator works the same way.

### Activities
Could have been called a "Form" or "Page". Its worth understanding the [Activity lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle.html) of Create, Resume, Pause, Destroy. 

* Calling Activities from other Activities:
`startActivity(new Intent(CurrentActivityClass.this, ActivityToCreateClass.class));`

### Services
Allow background processing without a UI

* Services can be killed by the operating system if RAM is needed!

* Foreground services are safer from being killed by the OS but need to show an icon. Icon can be hidden so its only shown in the pull down.

### Application
Allows for a globally accessible Singleton (optional and specified in manifest)

### Intents
Allow data to be passed around.
Used everywhere.

### Context
Used everywhere, an activity is a context, as is a service.
Always need one, never have it when needed.

### System Services 
Get services directly from an activity.

e.g. Location
```
locationManager = (LocationManager)getSystemService(Context.LOCATION_SERVICE); 
locationManager.requestLocationUpdates(LOCATION_PROVIDER, currentRate, -1, this); 
```
Equally this could be from any context reference

`locationManager = (LocationManager)context.getSystemService(Context.LOCATION_SERVICE); `

### Broadcast Receivers
* Ordered
* Sticky/Not (deprecated)

### Preferences
* XML defines it
* Activity to show it
* Remember to Commit!

### Manifest
* Permissions - Only list those needed. i.e. is READ_CONTACTS needed!?
> Android 6+ you need to check the user has granted permissions!
* If an Activity isn’t in the manifest it will not run!
Can register broadcast receivers that fire without the application needing to be running!

For example this will call a AutoStart class that inherits from BroadcastReceiver when the device starts up.

```
<receiver android:name=".utils.receivers.AutoStarter">
	<intent-filter android:priority="100">
    	<action android:name="android.intent.action.BOOT_COMPLETED" />
    </intent-filter>
</receiver>
```

### R file
The R file is a class automatically generated to allow Resource files to be referenced in code.
For example a layout file `activity_main.xml` is given an ID which can then be referenced by `R.layout.activity_main`

It can be a pain, clean and rebuild if the resources fail.

### Debugging
See LogCat under Android Monitor in Android Studio


# Useful Resources

Android Asset Studio - Icon Generator 
https://romannurik.github.io/AndroidAssetStudio/

Icons 
https://materialdesignicons.com/

Libraries
https://android-arsenal.com/

CommonsGuy Blog
https://commonsware.com/blog/

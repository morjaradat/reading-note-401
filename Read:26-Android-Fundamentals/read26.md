# Application Fundamentals

- Android apps can be written using Kotlin, Java, and C++ languages.
- the android package have extension .apk or .app suffix and it contain the content to run the application .
- the android bundle have extension .aab  suffix and its contain the contents of an Android app project including some additional metadata that is not required at runtime.

- Android security features:

1. The Android operating system is a multi-user Linux system in which each app is a different user.
2. By default, the system assigns each app a unique Linux user ID (the ID is used only by the system and is unknown to the app). The system sets permissions for all the files in an app so that only the user ID assigned to that app can access them.
3. Each process has its own virtual machine (VM), so an app's code runs in isolation from other apps.
4. By default, every app runs in its own Linux process. The Android system starts the process when any of the app's components need to be executed, and then shuts down the process when it's no longer needed or when the system must recover memory for other apps.

- you can share teh data between two apps .

## App components

- its the core of the application that build the android app.
- each component have entry point.
- some components depends on other components.

### types of app components

1. **Activities**
2. **Services**
3. **Broadcast receivers**
4. **Content providers**

## Activities

- An activity is the entry point for interacting with the user.
- it represents a single screen with a user interface .
- An activity facilitates the following key interactions between system and app:

1. Keeping track of what the user currently cares about (what is on screen) to ensure that the system keeps running the process that is hosting the activity.
2. Knowing that previously used processes contain things the user may return to (stopped activities), and thus more highly prioritize keeping those processes around.
3. Helping the app handle having its process killed so the user can return to activities with their previous state restored.
4. Providing a way for apps to implement user flows between each other, and for the system to coordinate these flows. (The most classic example here being share.)

- we implement an activity as a subclass of the Activity class.

## Services

- A service is a general-purpose entry point for keeping an app running in the background for all kinds of reasons.
- It is a component that runs in the background to perform long-running operations or to perform work for remote processes.
- A service does not provide a user interface.

## Broadcast receivers

- A broadcast receiver is a component that enables the system to deliver events to the app outside of a regular user flow, allowing the app to respond to system-wide broadcast announcements.
- Because broadcast receivers are another well-defined entry into the app, the system can deliver broadcasts even to apps that aren't currently running.
- A broadcast receiver is implemented as a subclass of BroadcastReceiver and each broadcast is delivered as an Intent object.

## Content providers

- A content provider manages a shared set of app data that you can store in the file system, in a SQLite database, on the web, or on any other persistent storage location that your app can access.
- Through the content provider, other apps can query or modify the data if the content provider allows it.

## Activating components

- activities, services, and broadcast receivers—are activated by an asynchronous message called an intent.
- An intent is created with an Intent object, which defines a message to activate either a specific component (explicit intent) or a specific type of component (implicit intent).
- For activities and services, an intent defines the action to perform (for example, to view or send something) and may specify the URI of the data to act on, among other things that the component being started might need to know.
- content providers are not activated by intents. Rather, they are activated when targeted by a request from a ContentResolver.
- The content resolver handles all direct transactions with the content provider so that the component that's performing transactions with the provider doesn't need to and instead calls methods on the ContentResolver object.

- There are separate methods for activating each type of component:

1. You can start an activity or give it something new to do by passing an Intent to startActivity() or startActivityForResult() (when you want the activity to return a result).
2. With Android 5.0 (API level 21) and later, you can use the JobScheduler class to schedule actions.
3. You can initiate a broadcast by passing an Intent to methods such as sendBroadcast(), sendOrderedBroadcast(), or sendStickyBroadcast().
4. You can perform a query to a content provider by calling query() on a ContentResolver.

## The manifest file

- AndroidManifest.xml is the file will contain all you application component.

- the order of manifest to declare a components :

1. Identifies any user permissions the app requires
2. Declares the minimum API Level required by the app
3. Declares hardware and software features used or required by the app
4. Declares API libraries the app needs to be linked against

## Declaring components

```
<?xml version="1.0" encoding="utf-8"?>
<manifest ... >
    <application android:icon="@drawable/app_icon.png" ... >
        <activity android:name="com.example.project.ExampleActivity"
                  android:label="@string/example_label" ... >
        </activity>
        ...
    </application>
</manifest>
```

- in the application the android attribute point to icon that define the app .
- In the activity element, the android:name attribute specifies the fully qualified class name of the Activity subclass and the android:label attribute specifies a string to use as the user-visible label for the activity.

- we  must declare all app components using the following elements:

1. ``<activity>`` elements for activities.
2. ``<service>`` elements for services.
3. ``<receiver>`` elements for broadcast receivers.
4. ``<provider>`` elements for content providers.

## Declaring component capabilities

- you can use an Intent to start activities, services, and broadcast receivers.
- You can use an Intent by explicitly naming the target component (using the component class name) in the intent. - - You can also use an implicit intent, which describes the type of action to perform and, optionally, the data upon which you’d like to perform the action.
- The implicit intent allows the system to find a component on the device that can perform the action and start it. - If there are multiple components that can perform the action described by the intent, the user selects which one to use.
- You can declare an intent filter for your component by adding an ``<intent-filter>`` element as a child of the component's declaration element.

## Declaring app requirements

- we need to specifies the drives that can run the app and its handle that by Google Play .
- we can specifies that devices on the build.gradle file .
- The values for minSdkVersion and targetSdkVersion are set in your app module's build.gradle file:

```
android {
  ...
  defaultConfig {
    ...
    minSdkVersion 26
    targetSdkVersion 29
  }
}
```

- Declare the camera feature directly in your app's manifest file:

```
<manifest ... >
    <uses-feature android:name="android.hardware.camera.any"
                  android:required="true" />
    ...
</manifest>
```

## App resources

- An Android app is composed of more than just code—it requires resources that are separate from the source code, such as images, audio files, and anything relating to the visual presentation of the app.
- For every resource that you include in your Android project, the SDK build tools define a unique integer ID, which you can use to reference the resource from your app code or from other resources defined in XML



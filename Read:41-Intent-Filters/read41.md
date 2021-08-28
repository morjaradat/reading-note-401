# Intent Filters

## Allowing Other Apps to Start Your Activity

* If your app can perform an action that might be useful from another app
* your app should be prepared to respond to action requests by specifying the appropriate intent filter in your activity.
* To allow other apps to start your activity in this way, you need to add an ``<intent-filter>`` element in your manifest file for the corresponding ``<activity>``element.

***Add an Intent Filter***

* In order to properly define which intents your activity can handle, each intent filter you add should be as specific as possible in terms of the type of action and data the activity accepts.
* The system may send a given Intent to an activity if that activity has an intent filter fulfills the following criteria of the Intent object:

1. Action

* A string naming the action to perform. Usually one of the platform-defined values such as ACTION_SEND or ACTION_VIEW.
* Specify this in your intent filter with the ``<action>`` element.

2. Data

* A description of the data associated with the intent.
Specify this in your intent filter with the ``<data>`` element.
* Using one or more attributes in this element, you can specify just the MIME type, just a URI prefix, just a URI scheme, or a combination of these and others that indicate the data type accepted.

3. Category

* Provides an additional way to characterize the activity handling the intent, usually related to the user gesture or location from which it's started.
* all implicit intents are defined with CATEGORY_DEFAULT by default.
* Specify this in your intent filter with the ``<category>`` element.
* In your intent filter, you can declare which criteria your activity accepts by declaring each of them with corresponding XML elements nested in the ``<intent-filter>`` element.

```XML
<activity android:name="ShareActivity">
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="text/plain"/>
        <data android:mimeType="image/*"/>
    </intent-filter>
</activity>
```

* we can  declare multiple instances of the ``<action>``, ``<category>``, and ``<data>`` elements in each ``<intent-filter>``.

```declare multiple instances
<activity android:name="ShareActivity">
    <!-- filter for sending text; accepts SENDTO action with sms URI schemes -->
    <intent-filter>
        <action android:name="android.intent.action.SENDTO"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:scheme="sms" />
        <data android:scheme="smsto" />
    </intent-filter>
    <!-- filter for sending text or images; accepts SEND action and text or image data -->
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="image/*"/>
        <data android:mimeType="text/plain"/>
    </intent-filter>
</activity>
```

***Handle the Intent in Your Activity***

* call getIntent() to retrieve the Intent that started the activity.

```call getIntent
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    setContentView(R.layout.main);

    // Get the intent that started this activity
    Intent intent = getIntent();
    Uri data = intent.getData();

    // Figure out what to do based on the intent type
    if (intent.getType().indexOf("image/") != -1) {
        // Handle intents with image data ...
    } else if (intent.getType().equals("text/plain")) {
        // Handle intents with text ...
    }
}
```

***Return a Result***

* call setResult() to specify the result code and result Intent.
* When your operation is done and the user should return to the original activity, call finish() to close (and destroy) your activity.

```Return a Result
// Create intent to deliver some kind of result data
Intent result = new Intent("com.example.RESULT_ACTION", Uri.parse("content://result_uri"));
setResult(Activity.RESULT_OK, result);
finish();
```

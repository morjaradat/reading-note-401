# Location

* Using the Google Play services location APIs, your app can request the last known location of the user's device.

***Set up Google Play services***

* To access the fused location provider, your app's development project must include Google Play services.
* Download and install the Google Play services component via the SDK Manager and add the library to your project.

* add the dependencies :

```dependencies
dependencies {
    implementation 'com.google.android.gms:play-services-location:18.0.0'
}
```

***Specify app permissions***

1. Foreground location

```Foreground location
<service
    android:name="MyNavigationService"
    android:foregroundServiceType="location" ... >
    <!-- Any inner elements would go here. -->
</service>
```

* the manifest :

```manifest
<manifest ... >
  <!-- To request foreground location access, declare one of these permissions. -->
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
</manifest>
````

2. Background location :

```Background location
<manifest ... >
  <!-- Required only when requesting background location access on
       Android 10 (API level 29) and higher. -->
  <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
</manifest>
```

***Request background location***

* App targets Android 11 or higher:

  * If your app hasn't been granted the ACCESS_BACKGROUND_LOCATION permission, and shouldShowRequestPermissionRationale() returns true.

    * A clear explanation of why your app's feature needs access to background location.
    * The user-visible label of the settings option that grants background location (for example, Allow all the time in figure 3). You can call getBackgroundPermissionOptionLabel() to get this label. The return value of this method is localized to the user's device language preference.
    * An option for users to decline the permission. If users decline background location access, they should be able to continue using your app.

* App targets Android 10 or lower :

  * When a feature in your app requests background location access, users see a system dialog. This dialog includes an option to navigate to your app's location permission options on a settings page.

***Create location services client***

* In your activity's onCreate() method:

```Create location services client
private FusedLocationProviderClient fusedLocationClient;

// ..

@Override
protected void onCreate(Bundle savedInstanceState) {
    // ...

    fusedLocationClient = LocationServices.getFusedLocationProviderClient(this);
}
```

***Get the last known location***

```last known location
fusedLocationClient.getLastLocation()
        .addOnSuccessListener(this, new OnSuccessListener<Location>() {
            @Override
            public void onSuccess(Location location) {
                // Got last known location. In some rare situations this can be null.
                if (location != null) {
                    // Logic to handle location object
                }
            }
        });
```

***Choose the best location estimate***

* The FusedLocationProviderClient provides several methods to retrieve device location information. Choose from one of the following, depending on your app's use case:

1. getLastLocation() gets a location estimate more quickly and minimizes battery usage that can be attributed to your app.
2. getCurrentLocation() gets a fresher, more accurate location more consistently.

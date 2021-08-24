# ANALYTICS

* The Analytics category enables you to collect analytics data for your App.

***Set up Analytics backend***

* write the command :

```command
amplify add analytics
```

* then

```command
 amplify push
```

***dependencies***

```dependencies
  implementation 'com.amplifyframework:aws-analytics-pinpoint:1.24.0'
    implementation 'com.amplifyframework:aws-auth-cognito:1.24.0'
}
```

***Initialize Amplify Analytics***

* by add the plugin :

```plugin
Amplify.addPlugin(new AWSPinpointAnalyticsPlugin(this));
```

***Record events***

* To record an event, create an AnalyticsEvent and call Amplify.Analytics.

```record
AnalyticsEvent event = AnalyticsEvent.builder()
    .name("PasswordReset")
    .addProperty("Channel", "SMS")
    .addProperty("Successful", true)
    .addProperty("ProcessDuration", 792)
    .addProperty("UserAge", 120.3)
    .build();

Amplify.Analytics.recordEvent(event);
```

***View Analytics console***

```View Analytics console
amplify console analytics
```

***Flush events***

* Events have default configuration to flush out to the network every 30 seconds. * If you would like to change this, update ``amplifyconfiguration.json`` with the value in milliseconds you would like for autoFlushEventsInterval.

```Flush events
{
    "UserAgent": "aws-amplify-cli/2.0",
    "Version": "1.0",
    "analytics": {
        "plugins": {
            "awsPinpointAnalyticsPlugin": {
                "pinpointAnalytics": {
                    "appId": "AppID",
                    "region": "Region"
                },
                "pinpointTargeting": {
                    "region": "Region"
                },
                "autoFlushEventsInterval": 10000
            }
        }
    }
}
```

* To manually flush events, call:

```manually flush events
Amplify.Analytics.flushEvents();
```

***Global Properties***

* You can register global properties which will be sent along with all invocations of Amplify.Analytics.recordEvent.

```global
Amplify.Analytics.registerGlobalProperties(
    AnalyticsProperties.builder()
        .add("AppStyle", "DarkMode")
        .build());
```

* To unregister a global property, call Amplify.Analytics.unregisterGlobalProperties():

```unregister
Amplify.Analytics.unregisterGlobalProperties("AppStyle", "OtherProperty");
```

***Disable Analytics***

```Disable Analytics
Amplify.Analytics.disable();
```

***Enable Analytics***

```Enable Analytics
Amplify.Analytics.enable();
```

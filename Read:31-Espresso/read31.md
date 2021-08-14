## Espresso Testing (read Overview, Basics, and Recipes, plus any others that look interesting)
**Espresso**
  * Espresso - used to write concise, beautiful, and reliable Android UI tests.
  * Espresso test example:

```
    @Test
    public void greeterSaysHello() {
      onView(withId(R.id.name_field)).perform(typeText("Steve"));
      onView(withId(R.id.greet_button)).perform(click());
      onView(withText("Hello Steve!")).check(matches(isDisplayed()));
    }
```

  * Espresso tests state expectations, interactions, and assertions clearly without the distraction of boilerplate content, custom infrastructure, or messy implementation details getting in the way.
  * Target audience - developers, who believe that automated testing is an integral part of the development lifecycle. 
  * Synchronization capabilities
    - Each time your test invokes onView(), Espresso waits to perform the corresponding UI action or assertion until the following synchronization conditions are met:
      * message queue is empty
      * no instances of AsyncTask currently executing a task
      * all developer-defined idling resources are idle
  * Packages
    - espresso-core - contains core and basic View matchers, actions, and assertions
    - espresso-web - contains resources for WebView support
    - espresso-idling-resource - Espresso's mechanism for synchronization with background jobs
    - espresso-contrib - external contributions that contain DatePicker, RecyclerView and Drawer actions, accessibility checks, and CountingIdlingResource
    - espresso-intents - extension to validate and stub intents for hermetic testing
    - espresso-remote - location of Espresso's multi-process functionality

## Ridiculous superpower: the Espresso Test Recorder
**Create UI tests with Espresso Test Recorder**
  * Espresso Test Recorder tool - lets you create UI tests for your app without writing any test code. Takes the saved recording and automatically generates a corresponding UI test that you can run to test your app. Writes tests based on the Espresso Testing framework, an API in AndroidX Test. 
  * Turn off animations on your test device
    - Before using Espresso Test Recorder, make sure you turn off animations on your test device to prevent unexpected results. Follow the "Set Up Espresso" instructions on the Testing UI for a Single App page, but note that you do not need to manually set a dependency reference. 
  * Record an Espresso test
    - Espresso tests consist of two primary components: 
      * UI interactions - tap and type actions that a person may use to interact with your app.
      * Assertions - verify the existence or contents of visual elements on the screen.
  * Record UI interactions
    - To start recording a test - click Run > Record Espresso Test, choose the device on which you want to record the test in the Select Deployment Target window, and then Espresso Test Recorder triggers a build of your project, and the app must install and launch. The Record Your Test window appears after the app launches, and then you can interact with it.
  * Add assertions to verify UI elements
    - Three main types - text is, exists, and does not exist
    - To add assertions - click Add Assertions, to select a View element click on the element in the screenshot or use the first drop-down menu in the Edit assertion box at the bottom of the window, elect the assertion you want to use from the second drop-down menu in the Edit assertion box, and then click Save and Add Another to create another assertion or click Save Assertion to close the assertion panels.
  * Save a recording - click Complete Recording, pick a test class name for your test window appears, use the Test class name text field if you want to change the suggested name, and click Save. 
  * Run an Espresso test locally - use the Project  window on the left side of the Android Studio IDE, open the desired app module folder and navigate to the test you want to run, right-click on the test and click Run ‘testName', and in the Select Deployment Target window, choose the device on which you want to run the test.
  * To run Espresso tests with Firebase Test Lab, create a Firebase project for your app and then follow the instructions to Run your tests with Firebase Test Lab from Android Studio.
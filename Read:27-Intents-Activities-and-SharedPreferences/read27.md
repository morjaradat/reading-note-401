# Android Tasks and the Back Stack

## Understand Tasks and Back Stack

- its collection of active that user  interact with when performing a certain job.
- The activities are arranged in a stack—the back stack)—in the order in which each activity is opened.
- when the user start new activity the activity is push in to the stack and when its precess back its pop up from the stack.

## Managing Tasks

the principal ``<activity>`` attributes you can use are:

1. taskAffinity
2. launchMode
3. allowTaskReparenting
4. clearTaskOnLaunch
5. alwaysRetainTaskState
6. finishOnTaskLaunch

- And the principal intent flags you can use are:

1. FLAG_ACTIVITY_NEW_TASK
2. FLAG_ACTIVITY_CLEAR_TOP
3. FLAG_ACTIVITY_SINGLE_TOP

### Defining launch modes

- Launch modes allow you to define how a new instance of an activity is associated with the current task
- we can define it by :

1. Using the manifest file
2. Using Intent flags

**Using the manifest file**

- by using element's launchMode attribute specifies an instruction on how the activity should be launched into a task.

- there are three type of launchMode attribute : 

1. standard (the default mode)

- The system creates a new instance of the activity in the task 

2. singleTop

- If an instance of the activity already exists at the top of the current task, the system routes the intent to that instance through a call to its onNewIntent() method

3. singleTask

- The system creates a new task and instantiates the activity at the root of the new task.

4. singleInstance

- Same as "singleTask", except that the system doesn't launch any other activities into the task holding the instance. The activity is always the single and only member of its task; any activities started by this one open in a separate task.

**Using Intent flags**

- you can modify the default association of an activity to its task by including flags in the intent that you deliver to startActivity() .

- The flags you can use to modify the default behavior are:

1. FLAG_ACTIVITY_NEW_TASK 

- Start the activity in a new task

2. FLAG_ACTIVITY_SINGLE_TOP

- If the activity being started is the current activity (at the top of the back stack), then the existing instance receives a call to onNewIntent()

3. FLAG_ACTIVITY_CLEAR_TOP

- If the activity being started is already running in the current task,  all of the other activities on top of it are destroyed and this intent is delivered to the resumed instance of the activity (now on top).

## Handling affinities

- The affinity indicates which task an activity prefers to belong to.
- By default, all the activities from the same app have an affinity for each other.
- You can modify the affinity for any given activity with the taskAffinity attribute of the ``<activity>`` element..

- The taskAffinity attribute takes a string value, which must be unique from the default package name declared in the ``<manifest>`` element .

## Clearing the back stack

- If the user leaves a task for a long time, the system clears the task of all activities except the root activity.

- There are some activity attributes that you can use to modify this behavior:

1. alwaysRetainTaskState

- If this attribute is set to "true" in the root activity of a task.
- the default behavior just described does not happen.
- The task retains all activities in its stack even after a long period.

2. clearTaskOnLaunch

- If this attribute is set to "true" in the root activity of a task.
- the task is cleared down to the root activity whenever the user leaves the task and returns to it.
- In other words, it's the opposite of alwaysRetainTaskState.
- The user always returns to the task in its initial state, even after leaving the task for only a moment.

3. finishOnTaskLaunch

- This attribute is like clearTaskOnLaunch, but it operates on a single activity, not an entire task.
- It can also cause any activity to finish, except for the root activity.
- When it's set to "true", the activity remains part of the task only for the current session.
- If the user leaves and then returns to the task, it is no longer present.

## Starting a task

```
<activity ... >
    <intent-filter ... >
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
    ...
</activity>
```

## Save key-value data

- we should use the SharedPreferences APIs to save the data.
- A SharedPreferences object points to a file containing key-value pairs and provides simple methods to read and write them.
- Each SharedPreferences file is managed by the framework and can be private or shared.

## Get a handle to shared preferences

- we can create a new shared preference file or access an existing one by calling one of these methods:

1. getSharedPreferences()
 — Use this if you need multiple shared preference files identified by name, which you specify with the first parameter. You can call this from any Context in your app.

2. getPreferences()
— Use this from an Activity if you need to use only one shared preference file for the activity. Because this retrieves a default shared preference file that belongs to the activity, you don't need to supply a name.

```
Context context = getActivity();
SharedPreferences sharedPref = context.getSharedPreferences(
    getString(R.string.preference_file_key), Context.MODE_PRIVATE);
```

```
SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
```

- If you're using the SharedPreferences API to save app settings, you should instead use getDefaultSharedPreferences() to get the default shared preference file for your entire app .

## Write to shared preferences

- To write to a shared preferences file, create a SharedPreferences.Editor by calling edit() on your SharedPreferences.
- Pass the keys and values you want to write with methods such as putInt() and putString(). Then call apply() or commit() to save the changes.

```
SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
SharedPreferences.Editor editor = sharedPref.edit();
editor.putInt(getString(R.string.saved_high_score_key), newHighScore);
editor.apply();
```

- apply() changes the in-memory SharedPreferences object immediately but writes the updates to disk asynchronously
- we can use commit() to write the data to disk synchronously. But because commit() is synchronous, you should avoid calling it from your main thread because it could pause your UI rendering.



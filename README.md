# AProfiler

<img src="https://github.com/MaheshPatial/Images/blob/master/Aprofiler1.png" width="180px"/>
<img src="https://github.com/MaheshPatial/Images/blob/master/Aprofiler2.png" width="180px" />


Aprofiler monitors and records the CPU and memory usage of Android devices.

## IMPORTANT NOTICE for Android 7.0+ users

Due to undocumented changes made by Google, on Android 7.0 CPU usage information for processes others than the own Aprofiler one will not be available (not even with root access). Rest of the app will work normally. For devices with Android 8.0 Aprofiler will not even show the CPU usage of the own app process. Read the below [Retriving processes info since Android 7.0](#retrieving-processes-info-since-android-nougat-70-api-24-august-2016) for more info.

## Details

Aprofiler shows the device CPU and memory status in real time.

It has two main options:
- It shows a chart and several labels wherein the values of the CPU and memory usage are updated every 0.5, 1, 2 or 4 seconds.
- It can record on a CSV file the read values for a later usage on a spreadsheet program.

When Aprofiler is running on the background it consumes little resources. Then it can monitor and record the CPU and memory usage of other applications on the foreground.

Aprofiler adds a *Record* and *Close* button to the Aprofiler entry on the notification drawer.

#### How CPU and memory usage are obtained

In order to get the CPU usage the app does NOT make use of the [`top`](https://en.wikipedia.org/wiki/Top_(software)) command from Linux but instead it parses `/proc/stat` and rest of process folders from the [`procfs`](https://en.wikipedia.org/wiki/Procfs) file system and work out the calculations with the user and system time. This is implemented on [`ServiceReader.class`]

https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk65143

#### About multi-core devices

The app does not support showing values for a specific core in multi-core devices. It will show an average of all the device's cores.

#### Retrieving processes info since Android Lollipop 5.1 (API 22, March 2015)

For devices running Android 5.1.1 it is not possible any more to retrieve the processes list with [`ActivityManager.getRunningAppProcesses()`](http://developer.android.com/reference/android/app/ActivityManager.html#getRunningAppProcesses%28%29). This change has not been documented anywhere on the official documentation nor an alternative way to retrieve the list has been provided. Thankfully the community at Stack Overflow came out with some [satisfying solution](http://stackoverflow.com/questions/30619349/android-5-1-1-and-above-getrunningappprocesses-returns-my-application-packag). For devices with Android 5.1 Aprofiler now uses the unofficial [AndroidProcesses](https://github.com/jaredrummler/AndroidProcesses) library to retrieve the processes list. The drawback of this is that for some processes there is no way to retrieve the app name nor the icon and instead only the long package name is shown.

#### Retrieving processes info since Android Nougat 7.0 (API 24, August 2016)

In Android 7.0 Google once again has made undocumented changes and has significantly restricted access to the `proc` file system. This means that since this new API level it is not possible anymore to retrieve processes info. Aprofiler running on devices with Android 7.0 will only show total CPU usage, Aprofiler CPU usage and memory usage, but not CPU usage for other processes. Running the app on a rooted device does not make difference. More info on [File system changes in Android Nougat - Stack Overflow](https://stackoverflow.com/questions/38590140/file-system-changes-in-android-nougat). [Star this Android issue](https://issuetracker.google.com/issues/37091475) to push Google to implement an alternative API.


#### Retrieving processes info since Android Oreo 8.0 (API 26, August 2017)

In Android 8.0 Google has further restricted access to the `proc` file system. Until now it was possible to at least get process info of the process running Aprofiler and total CPU usage. This does not work any more. Aprofiler running on devices with Android 8.0 will only show memory usage, but not total CPU usage or CPU usage for any process, including the own app process. Running the app on a rooted device does not make difference.


## Resolving dependencies

Aprofiler only has one external dependency, [AndroidProcesses](https://github.com/jaredrummler/AndroidProcesses). It is used to retrieve the device processes list and populate the 'Processes' screen.
